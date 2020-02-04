---
title: Bot からファイルを送受信する
description: Bot からファイルを送受信する方法について説明します。
keywords: teams の bot ファイル送信受信
ms.date: 05/20/2019
ms.openlocfilehash: ee26b4031c6022ab30ec5b2b58b42105c2dc6b0f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675107"
---
# <a name="send-and-receive-files-through-your-bot"></a>Bot を使用してファイルを送受信する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Bot との間でファイルを送信するには、次の2つの方法があります。

* Microsoft Graph Api を使用します。 このメソッドは Teams のすべてのスコープの bot に対して機能します。
  * `personal`
  * `channel`
  * `groupchat`
* Teams Api を使用します。 これらは、1つのコンテキスト内のファイルのみをサポートします。
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a>Microsoft Graph Api を使用する

[OneDrive および SharePoint](/onedrive/developer/rest-api/)の Microsoft Graph api を使用して、既存の SharePoint ファイルを参照するカードの添付ファイルを含むメッセージを投稿できます。 Graph Api を使用するには、標準の OAuth 2.0 認証フローを`personal`使用`groupchat`して、ユーザーの OneDrive フォルダー (およびファイルの場合`channel` ) またはチームのチャネル内のファイル (ファイルの場合) へのアクセス権を取得する必要があります。 このメソッドは、すべての Teams スコープで機能します。

## <a name="using-the-teams-bot-apis"></a>Teams の Bot Api の使用

> [!NOTE]
> このメソッドは、 `personal`コンテキストでのみ機能します。 または`channel` `groupchat`のコンテキストでは動作しません。

Bot は、Teams Api を使用して、 `personal`コンテキスト内のユーザー (個人チャットとも呼ばれる) でファイルを直接送受信できます。 これにより、経費報告、画像の認識、ファイルアーカイブ、電子署名、およびファイルコンテンツの直接操作を伴うその他のシナリオを実装できます。 Teams で共有されるファイルは、通常、カードとして表示され、アプリ内での表示を許可します。

次のセクションでは、メッセージの送信など、直接的なユーザー操作の結果としてファイルコンテンツを送信する方法について説明します。 この API は、Microsoft Teams の Bot プラットフォームの一部として提供されています。

### <a name="configure-your-bot-to-support-files"></a>ボットを構成してファイルをサポートする

Bot でファイルを送受信するためには、マニフェストの`supportsFiles`プロパティをに`true`設定する必要があります。 このプロパティについては、マニフェストリファレンスの「 [bot](~/resources/schema/manifest-schema.md#bots) 」セクションを参照してください。

定義は、次`"supportsFiles": true`のようになります。 Bot が有効に`supportsFiles`なっていない場合、次の機能は動作しません。

### <a name="receiving-files-in-personal-chat"></a>個人用チャットでのファイルの受信

ユーザーが bot にファイルを送信すると、そのファイルは最初にユーザーの OneDrive for Business ストレージにアップロードされます。 Bot は、ユーザーのアップロードを通知するメッセージアクティビティを受信します。 アクティビティには、ファイルの名前やコンテンツの URL などのファイルメタデータが含まれます。 この URL から直接読み取り、バイナリコンテンツを取得することができます。

### <a name="send-and-receive-files-through-bot-on-teams-mobile-app"></a>Teams モバイルアプリの bot を経由してファイルを送受信する
> [!NOTE] 
> モバイルデバイスでのボットへのファイルの送信と受信はサポートされていません。

#### <a name="message-activity-with-file-attachment-example"></a>添付ファイルを含むメッセージアクティビティの例

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

次の表では、添付ファイルのコンテンツプロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `downloadUrl` | ファイルのコンテンツを取得するための OneDrive URL。 この URL から直接`HTTP GET`を発行することができます。 |
| `uniqueId` | 一意のファイル ID。 これは、ユーザーが bot にファイルを送信する場合に、OneDrive ドライブのアイテム ID になります。 |
| `fileType` | ファイル拡張子の種類 (pdf または .docx など)。 |

ベストプラクティスとして、ユーザーにメッセージを送信して、ファイルのアップロードを確認する必要があります。

### <a name="uploading-files-to-personal-chat"></a>個人用チャットへのファイルのアップロード

ユーザーにファイルをアップロードするには、次の手順を実行します。

1. ファイルを書き込むためのアクセス許可を要求しているユーザーにメッセージを送信します。 このメッセージには、 `FileConsentCard`アップロードするファイルの名前の添付ファイルが含まれている必要があります。
2. ユーザーがファイルのダウンロードを受け入れた場合、ボットは場所の URL を持つ*Invoke*アクティビティを受け取ります。
3. ファイルを転送するため、bot は`HTTP POST` 、指定された場所の URL を直接実行します。
4. 必要に応じて、ユーザーが同じファイルのアップロードをさらに許可しないようにする場合は、元の同意カードを削除できます。

#### <a name="message-requesting-permission-to-upload"></a>アップロード許可を要求するメッセージ

このメッセージには、ファイルをアップロードするためのユーザーアクセス許可を要求する簡単な添付ファイルオブジェクトが含まれています。

![ユーザーがファイルをアップロードするためのアクセス許可を要求している同意カードのスクリーンショット](~/assets/images/bots/bot-file-consent-card.png)

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

次の表では、添付ファイルのコンテンツプロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `description` | ファイルの説明。 ユーザーに対して、その目的を説明したり、コンテンツを要約したりするように表示される場合があります。 |
| `sizeInBytes` | ユーザーに、ファイルサイズと OneDrive で必要な容量の推定値を提供します。 |
| `acceptContext` | ユーザーがファイルを受け取ったときに、ボットに自動的に送信される追加のコンテキスト。 |
| `declineContext` | ユーザーがファイルを拒否したときに、ボットに自動的に送信される追加のコンテキスト。 |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>ユーザーがファイルを受け取ったときにアクティビティを呼び出す

ユーザーがファイルを受け入れるかどうかによって、呼び出しアクティビティが bot に送信されます。 これには、ボットがを使用してファイルコンテンツを転送できる`PUT` 、OneDrive for business のプレースホルダー URL が含まれています。 OneDrive URL へのアップロードの詳細については、「アップロード[セッションにバイトをアップロードする](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)」を参照してください。

次の例は、ボットが受け取る invoke アクティビティの abridged バージョンを示しています。

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

同様に、ユーザーがファイルを拒否した場合、bot は次のイベントを受け取ります。これは、全体的なアクティビティ名と同じです。

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

### <a name="notifying-the-user-about-an-uploaded-file"></a>アップロードしたファイルについてユーザーに通知する

ユーザーの OneDrive にファイルをアップロードした後、前述のメカニズムを使用するか、または OneDrive ユーザーによって委任された Api を使用するかにかかわらず、確認メッセージをユーザーに送信する必要があります。 このメッセージには、 `FileCard`ユーザーがクリックできる添付ファイルが含まれています。これは、プレビューするか、OneDrive で開くか、またはローカルでダウンロードすることができます。

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

次の表では、添付ファイルのコンテンツプロパティについて説明します。 

| プロパティ | 用途 |
| --- | --- |
| `uniqueId` | OneDrive/SharePoint ドライブのアイテム ID。 |
| `fileType` | ファイルの種類 (pdf または .docx など)。 |

### <a name="basic-example-in-c"></a>C の基本的な例#

次の例は、ボットのダイアログでファイルのアップロードを処理し、ファイルの同意要求を送信する方法を示しています。

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
