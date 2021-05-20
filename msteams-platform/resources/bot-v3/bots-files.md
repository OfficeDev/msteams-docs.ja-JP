---
title: ボットからのファイルの送受信
description: ボットからファイルを送受信する方法について説明します。
keywords: チームボットファイル送信受信
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: f69a6ca9cfcdf3b1e559fbe8cf569accf3166f69
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566482"
---
# <a name="send-and-receive-files-through-your-bot"></a>ボットを介してファイルを送受信する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットとの間でファイルを送信するには、次の 2 つの方法があります。

* マイクロソフト Graph API を使用する。 このメソッドは、Teamsのすべてのスコープのボットに対して機能します。
  * `personal`
  * `channel`
  * `groupchat`
* Teams API を使用する。 次の場合、1 つのコンテキストでファイルのみがサポートされます。
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a>マイクロソフト Graph API の使用

OneDrive および SharePoint 用の Microsoft Graph API を使用して、既存のSharePoint ファイルを参照するカード添付ファイルを含むメッセージ[を](/onedrive/developer/rest-api/)投稿できます。 Graph API を使用するには、標準 OAuth 2.0 承認フローを通じて、ユーザーのOneDriveフォルダー ( `personal` ファイル `groupchat` 用) またはチームのチャネル (ファイル用) 内のファイルへのアクセス `channel` を取得する必要があります。 このメソッドは、すべてのTeamsスコープで動作します。

## <a name="using-the-teams-bot-apis"></a>Teamsボット API の使用

> [!NOTE]
> このメソッドは、コンテキストでのみ機能します `personal` 。 または コンテキストでは動作しません `channel` `groupchat` 。

ボットは `personal` 、Teams API を使用して、コンテキスト内のユーザー (個人用チャットとも呼ばれます) でファイルを直接送受信できます。 これにより、経費レポート、画像認識、ファイルアーカイブ、電子署名、およびファイルコンテンツの直接操作に関連するその他のシナリオを実装できます。 Teamsで共有されるファイルは、通常カードとして表示され、豊富なアプリ内表示が可能です。

次のセクションでは、メッセージの送信など、ユーザーが直接操作した結果としてファイル コンテンツを送信する方法について説明します。 この API は、Microsoft Teams Bot プラットフォームの一部として提供されます。

### <a name="configure-your-bot-to-support-files"></a>ファイルをサポートするようにボットを構成する

ボットでファイルを送受信するには、 `supportsFiles` マニフェストのプロパティを に設定する必要があります `true` 。 このプロパティは、マニフェスト リファレンスの [bots](~/resources/schema/manifest-schema.md#bots) セクションで説明されています。

定義は次のようになります `"supportsFiles": true` 。 ボットが 有効にされていない場合 `supportsFiles` 、次の機能は機能しません。

### <a name="receiving-files-in-personal-chat"></a>個人用チャットでファイルを受信する

ユーザーがボットにファイルを送信すると、そのファイルは最初にユーザーのOneDrive for Businessストレージにアップロードされます。 その後、ボットはユーザーのアップロードを通知するメッセージ アクティビティを受信します。 アクティビティには、名前やコンテンツ URL などのファイル メタデータが含まれます。 この URL から直接読み取って、バイナリコンテンツを取得できます。

#### <a name="message-activity-with-file-attachment-example"></a>添付ファイルを含むメッセージ アクティビティの例

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.file.download.info",
    "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
    "name": "file_example.txt",
    "content": {
      "downloadUrl" : "https://download.link",
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C9D",
      "fileType": "txt",
      "etag": "123"
    }
  }]
}
```

次の表に、添付ファイルのコンテンツ プロパティを示します。

| プロパティ | 用途 |
| --- | --- |
| `downloadUrl` | OneDriveファイルの内容を取得するための URL。 この URL `HTTP GET` から直接発行できます。 |
| `uniqueId` | 一意のファイル ID。 これは、ユーザーがボットにファイルを送信する場合のOneDriveドライブ項目 ID になります。 |
| `fileType` | ファイル拡張子の種類 (pdf や docx など)。 |

ベスト プラクティスとして、ユーザーにメッセージを送信して、ファイルのアップロードを承認する必要があります。

### <a name="uploading-files-to-personal-chat"></a>個人用チャットへのファイルのアップロード

ユーザーにファイルをアップロードするには、次の手順を実行します。

1. ファイルを書き込むアクセス許可を要求しているユーザーにメッセージを送信します。 このメッセージには、 `FileConsentCard` アップロードするファイルの名前を添付する必要があります。
2. ユーザーがファイルのダウンロードを受け入れると、ボットは場所 URL を持つ *Invoke* アクティビティを受信します。
3. ファイルを転送するには、ボットが `HTTP POST` 指定された場所の URL に直接実行します。
4. 必要に応じて、ユーザーが同じファイルのアップロードを受け入れることを許可しない場合は、元の同意カードを削除できます。

#### <a name="message-requesting-permission-to-upload"></a>アップロードするアクセス許可を要求しているメッセージ

このデスクトップ メッセージには、ファイルをアップロードするユーザー権限を要求する単純な添付ファイル オブジェクトが含まれています。

![ファイルをアップロードするユーザーの許可を要求する同意カードのスクリーンショット](../../assets/images/bots/bot-file-consent-card.png)

このモバイル メッセージには、ファイルをアップロードするユーザー権限を要求する添付ファイル オブジェクトが含まれています。

![ユーザーがモバイルでファイルをアップロードする許可を要求する同意カードのスクリーンショット](../../assets/images/bots/mobile-bot-file-consent-card.png)

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.card.file.consent",
    "name": "file_example.txt",
    "content": {
      "description": "<Purpose of the file, such as: this is your monthly expense report>",
      "sizeInBytes": 1029393,
      "acceptContext": {
      },
      "declineContext": {
      }
    }
  }]
}
```

次の表に、添付ファイルのコンテンツ プロパティを示します。

| プロパティ | 用途 |
| --- | --- |
| `description` | ファイルの説明。 ユーザーにその目的を説明したり、その内容を要約したりすることが示される場合があります。 |
| `sizeInBytes` | ファイル サイズと、OneDriveに使用する領域の量の見積もりをユーザーに提供します。 |
| `acceptContext` | ユーザーがファイルを受け入れたときにボットに自動的に送信される追加のコンテキスト。 |
| `declineContext` | ユーザーがファイルを拒否したときにボットに自動的に送信される追加のコンテキスト。 |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>ユーザーがファイルを受け入れたときにアクティビティを呼び出す

ユーザーがファイルを受け入れた場合、呼び出しアクティビティがボットに送信されます。 この URL には、ボットが発行して `PUT` ファイルの内容を転送できる、OneDrive for Businessのプレースホルダー URL が含まれています。 OneDrive URL へのアップロードについては、この記事を参照してください:[アップロード セッションにバイトをアップロード](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)します。

次の例は、ボットが受信する呼び出しアクティビティの簡略バージョンを示しています。

```json
{
  ...

  "name": "fileConsent/invoke",
  "value": {
    "type": "fileUpload",
    "action": "accept",
    "context": {
    },
    "uploadInfo": {
      "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
      "name": "file_example.txt",
      "uploadUrl": "https://upload.link",
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C8C",
      "fileType": "txt",
      "etag": "123"
    }
  }
}
```

同様に、ユーザーがファイルを拒否すると、ボットは同じアクティビティ名を持つ次のイベントを受信します。

```json
{
  "name": "fileConsent/invoke",
  "value": {
    "type": "fileUpload",
    "action": "decline",
    "context": {
    }
  }
}
```

### <a name="notifying-the-user-about-an-uploaded-file"></a>アップロードされたファイルについてユーザーに通知する

上述のメカニズムを使用するか、ユーザーが委任した API を使用するかにかかわらず、ファイルをユーザーのOneDrive OneDriveにアップロードした後、ユーザーに確認メッセージを送信する必要があります。 このメッセージには `FileCard` 、OneDrive ユーザーがクリックできる添付ファイルが含まれている必要があります。

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.card.file.info",
    "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
    "name": "file_example.txt",
    "content": {
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C8C",
      "fileType": "txt",
    }
  }]
}
```

次の表に、添付ファイルのコンテンツ プロパティを示します。

| プロパティ | 用途 |
| --- | --- |
| `uniqueId` | OneDrive/SharePointドライブ項目 ID。 |
| `fileType` | pdf や docx などのファイルの種類。 |

### <a name="basic-example-in-c"></a>Cの基本的な例#

次のサンプルは、ボットのダイアログでファイルアップロードを処理し、ファイルの同意要求を送信する方法を示しています。

```csharp

// This sample dialog shows two simple flows:
// 1) A silly example of receiving a file from the user, processing the key elements,
//    and then constructing the attachment and sending it back.
// 2) Creating a new file consent card requesting user permission to upload a file.
private async Task MessageReceivedAsync(IDialogContext context, IAwaitable<object> result)
{
    var replyMessage = context.MakeMessage();
    Attachment returnCard;

    var message = await result as Activity;

    // Check to see if the user is sending the bot a file.
    if (message.Attachments != null && message.Attachments.Any())
    {
        var attachment = message.Attachments.First();

        if (attachment.ContentType == FileDownloadInfo.ContentType)
        {
            FileDownloadInfo downloadInfo = (attachment.Content as JObject).ToObject<FileDownloadInfo>();
            if (downloadInfo != null)
            {
                returnCard = CreateFileInfoAttachment(downloadInfo, attachment.Name, attachment.ContentUrl);
                replyMessage.Attachments.Add(returnCard);
            }
        }
    }
    else
    {
        // Illustrates creating a file consent card.
        returnCard = CreateFileConsentAttachment();
        replyMessage.Attachments.Add(returnCard);
    }
    await context.PostAsync(replyMessage);
}


private static Attachment CreateFileInfoAttachment(FileDownloadInfo downloadInfo, string name, string contentUrl)
{
    FileInfoCard card = new FileInfoCard()
    {
        FileType = downloadInfo.FileType,
        UniqueId = downloadInfo.UniqueId
    };

    Attachment att = card.ToAttachment();
    att.ContentUrl = contentUrl;
    att.Name = name;

    return att;
}

private static Attachment CreateFileConsentAttachment()
{
    JObject acceptContext = new JObject();
    // Fill in any additional context to be sent back when the user accepts the file.

    JObject declineContext = new JObject();
    // Fill in any additional context to be sent back when the user declines the file.

    FileConsentCard card = new FileConsentCard()
    {
        AcceptContext = acceptContext,
        DeclineContext = declineContext,
        SizeInBytes = 102635,
        Description = "File description"
    };

    Attachment att = card.ToAttachment();
    att.Name = "Example file";

    return att;
}
```
