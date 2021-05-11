---
title: ボットからのファイルの送受信
description: ボットからファイルを送受信する方法について説明します。
keywords: teams ボット ファイルが受信を送信する
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: c5ee32d10e5a6adc5a08d1a0556a18be8367460a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020654"
---
# <a name="send-and-receive-files-through-your-bot"></a>ボットを介してファイルを送受信する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットにファイルを送受信するには、次の 2 つの方法があります。

* Microsoft Graph API を使用します。 このメソッドは、次に示すすべてのスコープのボットTeams。
  * `personal`
  * `channel`
  * `groupchat`
* API のTeams使用します。 これらは、1 つのコンテキストでファイルのみをサポートします。
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a>Microsoft Graph API の使用

Microsoft Graph API を使用して、既存のファイルを参照するSharePoint添付ファイルを含むメッセージOneDrive[投稿SharePoint。](/onedrive/developer/rest-api/) Graph API を使用するには、標準の `personal` `groupchat` OAuth 2.0 承認フローを使用して、ユーザーの OneDrive フォルダー (for and files) またはチームのチャネル (ファイル用) のファイルへのアクセスを取得する必要があります。 `channel` このメソッドは、すべてのスコープでTeamsします。

## <a name="using-the-teams-bot-apis"></a>ボット API Teams使用する

> [!NOTE]
> このメソッドは、コンテキストでのみ機能 `personal` します。 またはコンテキストでは `channel` 動作 `groupchat` しません。

ボットは、ユーザーがコンテキスト内のユーザー (個人チャットとも呼ばれる) とファイルを直接送受信するには、api を使用Teams `personal` できます。 これにより、経費報告、画像認識、ファイル アーカイブ、電子署名、およびファイル コンテンツの直接操作に関するその他のシナリオを実装できます。 通常、Teamsファイルはカードとして表示され、豊富なアプリ内表示が可能です。

次のセクションでは、メッセージの送信など、ユーザーが直接やり取りした結果としてファイル コンテンツを送信する方法について説明します。 この API は、ボット プラットフォームの一部Microsoft Teams提供されます。

### <a name="configure-your-bot-to-support-files"></a>ファイルをサポートするためにボットを構成する

ボットでファイルを送受信するには、マニフェストのプロパティをに設定 `supportsFiles` する必要があります `true` 。 このプロパティについては、Manifest [リファレンスの bots](~/resources/schema/manifest-schema.md#bots) セクションで説明します。

定義は次のように表示されます `"supportsFiles": true` 。 ボットが有効にしない場合 `supportsFiles` 、次の機能は機能しません。

### <a name="receiving-files-in-personal-chat"></a>個人用チャットでのファイルの受信

ユーザーがボットにファイルを送信すると、最初にユーザーのストレージにファイルがOneDrive for Businessされます。 その後、ボットはユーザーのアップロードを通知するメッセージ アクティビティを受信します。 アクティビティには、名前やコンテンツ URL などのファイル メタデータが含まれます。 この URL から直接読み取って、バイナリ コンテンツを取得できます。

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

次の表に、添付ファイルのコンテンツ プロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `downloadUrl` | OneDriveファイルのコンテンツをフェッチする URL。 この URL から `HTTP GET` 直接発行できます。 |
| `uniqueId` | 一意のファイル ID。 これは、ユーザー OneDriveボットにファイルを送信する場合のドライブ アイテム ID の一部です。 |
| `fileType` | ファイル拡張子の種類 (pdf や docx など)。 |

ベスト プラクティスとして、ユーザーにメッセージを送信してファイルのアップロードを確認する必要があります。

### <a name="uploading-files-to-personal-chat"></a>個人用チャットへのファイルのアップロード

ユーザーにファイルをアップロードするには、次の手順を実行します。

1. ファイルの書き込み許可を要求するメッセージをユーザーに送信します。 このメッセージには、アップロード `FileConsentCard` するファイルの名前を含む添付ファイルが含まれている必要があります。
2. ユーザーがファイルのダウンロードを受け入れる場合、ボットは場所 URL を含む *Invoke* アクティビティを受信します。
3. ファイルを転送するために、ボットは指定された場所 `HTTP POST` の URL に直接実行します。
4. 必要に応じて、ユーザーが同じファイルのそれ以上のアップロードを受け入れるのを許可しない場合は、元の同意カードを削除できます。

#### <a name="message-requesting-permission-to-upload"></a>アップロードするアクセス許可を要求するメッセージ

このデスクトップ メッセージには、ファイルをアップロードするユーザーのアクセス許可を要求する簡単な添付ファイル オブジェクトが含まれている。

![ファイルのアップロード許可をユーザーに要求する同意カードのスクリーンショット](../../assets/images/bots/bot-file-consent-card.png)

このモバイル メッセージには、ファイルをアップロードするユーザーのアクセス許可を要求する添付ファイル オブジェクトが含まれている。

![モバイルでファイルをアップロードするユーザーのアクセス許可を要求する同意カードのスクリーンショット](../../assets/images/bots/mobile-bot-file-consent-card.png)

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

次の表に、添付ファイルのコンテンツ プロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `description` | ファイルの説明。 目的を説明したり、その内容を要約したりするために、ユーザーに表示される場合があります。 |
| `sizeInBytes` | ユーザーに、ファイル サイズと、ファイルに含む容量の見積もりをOneDrive。 |
| `acceptContext` | ユーザーがファイルを受け入れるときにボットに無音で送信される追加のコンテキスト。 |
| `declineContext` | ユーザーがファイルを拒否した場合にボットに無音で送信される追加のコンテキスト。 |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>ユーザーがファイルを受け入れるときにアクティビティを呼び出す

ユーザーがファイルを受け入れる場合、呼び出しアクティビティがボットに送信されます。 このページには、OneDrive for Businessコンテンツを転送するためにボットが発行できるプレース ホルダー URL `PUT` が含まれている。 この記事を読んで、OneDrive URL へのアップロードの詳細については、アップロード[バイトを参照してください](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)。

次の例は、ボットが受け取る呼び出しアクティビティの簡橋的なバージョンを示しています。

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

同様に、ユーザーがファイルを拒否した場合、ボットは同じアクティビティ名で次のイベントを受け取る予定です。

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

ユーザーの OneDrive にファイルをアップロードした後、上記のメカニズムを使用するか、または OneDrive ユーザーが委任した API を使用するかに関わり、ユーザーに確認メッセージを送信する必要があります。 このメッセージには、ユーザーがクリックできる添付ファイルが含まれている必要があります。そのメッセージをプレビューしたり、ファイルを開OneDriveローカルで `FileCard` ダウンロードしたりします。

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

次の表に、添付ファイルのコンテンツ プロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `uniqueId` | OneDrive/SharePointアイテム ID。 |
| `fileType` | pdf や docx などのファイルの種類。 |

### <a name="basic-example-in-c"></a>C の基本例#

次のサンプルは、ファイルのアップロードを処理し、ボットのダイアログでファイル同意要求を送信する方法を示しています。

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
