---
title: ボットを介してファイルを送受信する
description: ボットを介してファイルを送受信する方法について説明します。
keywords: teams bots ファイルが受信を送信する
ms.date: 05/20/2019
ms.topic: how-to
ms.openlocfilehash: 07967ba4ce6d7e15e64c6f925fa588585f5a2c1d
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093279"
---
# <a name="send-and-receive-files-through-the-bot"></a>ボットを介してファイルを送受信する

> [!IMPORTANT]
> このドキュメントの記事は、v4 Bot Framework SDK に基づいて作成されています。

ボットに対してファイルを送受信するには、次の 2 つの方法があります。

* **Microsoft Graph API の使用:** このメソッドは、すべての Microsoft Teams スコープのボットに対して機能します。
  * `personal`
  * `channel`
  * `groupchat`

* **Teams ボット API の使用:** これらはコンテキスト内のファイルのみをサポート `personal` します。

## <a name="using-the-graph-apis"></a>Graph API の使用

OneDrive と SharePoint の Graph API を使用して、既存の SharePoint ファイルを参照するカード添付ファイルを含むメッセージ [を投稿します](/onedrive/developer/rest-api/)。 Graph API を使用するには、標準の OAuth 2.0 承認フローを通じて次のいずれかのアクセス権を取得します。
* ユーザーの OneDrive フォルダーと `personal` `groupchat` ファイル。
* チームのチャネル内のファイルの `channel` ファイル。

Graph API は、すべての Teams スコープで動作します。

## <a name="using-the-teams-bot-apis"></a>Teams ボット API の使用

> [!NOTE]
> Teams ボット API はコンテキストでのみ機能 `personal` します。 これらは、コンテキストで `channel` 機能 `groupchat` しません。

Teams API を使用すると、ボットはコンテキスト内のユーザー (個人チャットとも呼ばれる) とファイルを直接送受信 `personal` できます。 経費報告、画像認識、ファイル アーカイブ、ファイル コンテンツの編集に関連する電子署名などの機能を実装します。 Teams で共有されるファイルは通常、カードとして表示され、豊富なアプリ内表示が可能です。

以下のセクションでは、メッセージの送信など、ファイル コンテンツを直接のユーザー操作として送信する方法について説明します。 この API は、Teams ボット プラットフォームの一部として提供されます。

### <a name="configuring-the-bot-to-support-files"></a>ファイルをサポートするためのボットの構成

ボットでファイルを送受信するには、マニフェスト `supportsFiles` のプロパティを次に設定します `true` 。 このプロパティについては、マニフェスト リファレンス [の bots](~/resources/schema/manifest-schema.md#bots) セクションで説明します。

定義は次のように表示されます `"supportsFiles": true` 。 ボットが有効ではない場合、このセクションに記載されている機能 `supportsFiles` は機能しません。

### <a name="receiving-files-in-personal-chat"></a>個人用チャットでのファイルの受信

ユーザーがボットにファイルを送信すると、そのファイルが最初にユーザーの OneDrive for Business ストレージにアップロードされます。 ボットは、ユーザーのアップロードについてユーザーに通知するメッセージ アクティビティを受信します。 アクティビティには、名前やコンテンツ URL などのファイル メタデータが含まれます。 ユーザーは、この URL から直接読み取って、バイナリ コンテンツを取得できます。

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

次の表では、添付ファイルのコンテンツ プロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `downloadUrl` | ファイルのコンテンツをフェッチする OneDrive URL。 ユーザーは、この `HTTP GET` URL から直接発行できます。 |
| `uniqueId` | 一意のファイル ID。 これは、ユーザーがボットにファイルを送信する場合の OneDrive ドライブアイテム ID です。 |
| `fileType` | ファイルの種類 (.pdf、.docx など)。 |

ベスト プラクティスとして、ユーザーにメッセージを送信してファイルのアップロードを確認します。

### <a name="uploading-files-to-personal-chat"></a>個人用チャットへのファイルのアップロード

ユーザーにファイルをアップロードするには、次の手順が必要です。

1. ファイルを書き込む権限を要求しているユーザーにメッセージを送信します。 このメッセージには、アップロード `FileConsentCard` するファイルの名前を含む添付ファイルが含まれている必要があります。
2. ユーザーがファイルのダウンロードを受け入れる場合、ボットは場所 URL を含む呼び出しアクティビティを受信します。
3. ファイルを転送するために、ボットは指定された場所の `HTTP POST` URL に直接実行します。
4. 必要に応じて、ユーザーが同じファイルのそれ以上のアップロードを受け入れたくない場合は、元の同意カードを削除します。

#### <a name="message-requesting-permission-to-upload"></a>アップロードするアクセス許可を要求しているメッセージ

次のデスクトップ メッセージには、ファイルをアップロードするユーザーのアクセス許可を要求する簡単な添付ファイル オブジェクトが含まれます。

![ファイルをアップロードするユーザーのアクセス許可を要求している同意カード](../../assets/images/bots/bot-file-consent-card.png)

次のモバイル メッセージには、ファイルをアップロードするユーザーのアクセス許可を要求する添付ファイル オブジェクトが含まれます。

![モバイルでファイルをアップロードするためのユーザーのアクセス許可を要求する同意カード](../../assets/images/bots/mobile-bot-file-consent-card.png)

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

次の表では、添付ファイルのコンテンツ プロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `description` | ファイルの目的を説明するか、コンテンツを要約します。 |
| `sizeInBytes` | ユーザーに、OneDrive でのファイル サイズと必要な領域の量の見積もりを提供します。 |
| `acceptContext` | ユーザーがファイルを受け入れるときにボットにサイレントモードで送信される追加のコンテキスト。 |
| `declineContext` | ユーザーがファイルを拒否するとボットにサイレント送信される追加のコンテキスト。 |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>ユーザーがファイルを受け入れるときにアクティビティを呼び出す

ユーザーがファイルを受け入れる場合、いつ、呼び出しアクティビティがボットに送信されます。 ボットがファイルの内容を転送するために発行できる OneDrive for Business プレースホルダー URL `PUT` が含まれている。 OneDrive URL へのアップロードの詳細については、アップロード セッションへの [アップロード バイトを参照してください](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)。

次の例は、ボットが受け取る呼び出しアクティビティの簡潔なバージョンを示しています。

```json
{
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

同様に、ユーザーがファイルを辞退すると、ボットは同じアクティビティ名で次のイベントを受け取ります。

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

ユーザーの OneDrive にファイルをアップロードした後、ユーザーに確認メッセージを送信します。 メッセージには、OneDrive でプレビューまたは開く、またはローカルにダウンロードするために、ユーザーが選択できる次の添付ファイルが `FileCard` 含まれている必要があります。

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

次の表では、添付ファイルのコンテンツ プロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `uniqueId` | OneDrive または SharePoint ドライブアイテム ID。 |
| `fileType` | ファイルの種類 (.pdf、.docx など)。 |

### <a name="fetching-inline-images-from-message"></a>メッセージからインライン 画像を取得する

ボットのアクセス トークンを使用して、メッセージの一部であるインライン 画像を取得します。

![インライン画像](../../assets/images/bots/inline-image.png)

```csharp
private async Task ProcessInlineImage(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var attachment = turnContext.Activity.Attachments[0];
    var client = _clientFactory.CreateClient();
    // Get Bot's access token to fetch inline image. 
    var token = await new MicrosoftAppCredentials(microsoftAppId, microsoftAppPassword).GetTokenAsync();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    var responseMessage = await client.GetAsync(attachment.ContentUrl);
    // Save the inline image to Files directory.
    var filePath = Path.Combine("Files", "ImageFromUser.png");
    using (var fileStream = new FileStream(filePath, FileMode.Create, FileAccess.Write, FileShare.None))
    {
        await responseMessage.Content.CopyToAsync(fileStream);
    }
    // Create reply with image.
    var reply = MessageFactory.Text($"Attachment of {attachment.ContentType} type and size of {responseMessage.Content.Headers.ContentLength} bytes received.");
    reply.Attachments = new List<Attachment>() { 
        GetInlineAttachment() 
    };
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
private static Attachment GetInlineAttachment()
{
    var imagePath = Path.Combine("Files", "ImageFromUser.png");
    var imageData = Convert.ToBase64String(File.ReadAllBytes(imagePath));
    return new Attachment
    {
        Name = @"ImageFromUser.png",
        ContentType = "image/png",
        ContentUrl = $"data:image/png;base64,{imageData}",
    };
}
```

### <a name="basic-example-in-c"></a>C の基本的な例#

次のサンプルは、ボットのダイアログでファイルのアップロードを処理し、ファイル同意要求を送信する方法を示しています。

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    if (turnContext.Activity.Attachments?[0].ContentType.Contains("image/*") == true)
    {
        // Inline image.
        await ProcessInlineImage(turnContext, cancellationToken);
    }
    else
    {
        string filename = "teams-logo.png";
        string filePath = Path.Combine("Files", filename);
        long fileSize = new FileInfo(filePath).Length;
        await SendFileCardAsync(turnContext, filename, fileSize, cancellationToken);
    }
}
private async Task ProcessInlineImage(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var attachment = turnContext.Activity.Attachments[0];
    var client = _clientFactory.CreateClient();
    // Get Bot's access token to fetch inline image. 
    var token = await new MicrosoftAppCredentials(microsoftAppId, microsoftAppPassword).GetTokenAsync();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    var responseMessage = await client.GetAsync(attachment.ContentUrl);
    // Save the inline image to Files directory.
    var filePath = Path.Combine("Files", "ImageFromUser.png");
    using (var fileStream = new FileStream(filePath, FileMode.Create, FileAccess.Write, FileShare.None))
    {
        await responseMessage.Content.CopyToAsync(fileStream);
    }
    // Create reply with image.
    var reply = MessageFactory.Text($"Attachment of {attachment.ContentType} type and size of {responseMessage.Content.Headers.ContentLength} bytes received.");
    reply.Attachments = new List<Attachment>() { GetInlineAttachment() };
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
private static Attachment GetInlineAttachment()
{
    var imagePath = Path.Combine("Files", "ImageFromUser.png");
    var imageData = Convert.ToBase64String(File.ReadAllBytes(imagePath));
    return new Attachment
    {
        Name = @"ImageFromUser.png",
        ContentType = "image/png",
        ContentUrl = $"data:image/png;base64,{imageData}",
    };
}
private async Task SendFileCardAsync(ITurnContext turnContext, string filename, long filesize, CancellationToken cancellationToken)
{
    var consentContext = new Dictionary<string, string>
    {
        { 
            "filename", filename 
        },
    };
    var fileCard = new FileConsentCard
    {
        Description = "This is the file I want to send you",
        SizeInBytes = filesize,
        AcceptContext = consentContext,
        DeclineContext = consentContext,
    };
    var asAttachment = new Attachment
    {
        Content = fileCard,
        ContentType = FileConsentCard.ContentType,
        Name = filename,
    };
    var replyActivity = turnContext.Activity.CreateReply();
    replyActivity.Attachments = new List<Attachment>() { asAttachment };
    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}
```

### <a name="code-sample"></a>コード サンプル

|**サンプルの名前** | **説明** | **.NETCore** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| ファイルのアップロード | ボットからファイルの同意を取得し、Teams にファイルをアップロードする方法を示します。 また、ボットに送信されたファイルを受信する方法も示します。 | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |
