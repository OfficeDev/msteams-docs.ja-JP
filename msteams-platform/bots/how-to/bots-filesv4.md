---
title: ボットを介してファイルを送受信する
description: ボットを介してファイルを送受信する方法について説明します。
keywords: teams ボット ファイルが受信を送信する
ms.date: 05/20/2019
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 7d5ea3434b10d60e20574ca6d1935943c687f4d7
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020941"
---
# <a name="send-and-receive-files-through-the-bot"></a>ボットを介してファイルを送受信する

> [!IMPORTANT]
> このドキュメントの記事は、v4 Bot Framework SDK に基づいて作成されています。

ボットにファイルを送受信するには、次の 2 つの方法があります。

* [**Microsoft Graph API を使用します。**](#use-the-graph-apis) このメソッドは、すべての Microsoft Teams スコープのボットで動作します。
  * `personal`
  * `channel`
  * `groupchat`

* [**Teams ボット API を使用します。**](#use-the-teams-bot-apis) これらはコンテキスト内のファイルのみを `personal` サポートします。

## <a name="use-the-graph-apis"></a>グラフ API の使用

OneDrive および SharePoint のグラフ API を使用して、既存の SharePoint ファイルを参照するカード添付ファイルを含むメッセージ [を投稿します](/onedrive/developer/rest-api/)。 Graph API を使用するには、標準の OAuth 2.0 承認フローを使用して、次のいずれかのアクセス権を取得します。

* ユーザーの OneDrive フォルダーと `personal` ファイル `groupchat` 。
* チームのチャネル内のファイルをファイル用 `channel` に指定します。

グラフ API は、すべての Teams スコープで機能します。 詳細については、「チャット メッセージ ファイル [の添付ファイルの送信」を参照してください](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true)。

または、Teams ボット API を使用して、ボットにファイルを送信し、ボットからファイルを受信することもできます。

## <a name="use-the-teams-bot-apis"></a>Teams ボット API の使用

> [!NOTE]
> Teams ボット API はコンテキストでのみ機能 `personal` します。 これらは、コンテキストで `channel` 動作 `groupchat` しません。

Teams API を使用すると、ボットはコンテキスト内のユーザー (個人用チャットとも呼ばれる) でファイルを直接送受信 `personal` できます。 経費レポート、画像認識、ファイル アーカイブ、ファイル コンテンツの編集に関する電子署名などの機能を実装します。 Teams で共有されるファイルは、通常、カードとして表示され、アプリ内での豊富な表示を許可します。

次のセクションでは、メッセージの送信など、ファイル コンテンツを直接ユーザー操作として送信する方法について説明します。 この API は、Teams ボット プラットフォームの一部として提供されます。

### <a name="configure-the-bot-to-support-files"></a>ファイルをサポートするボットを構成する

ボットでファイルを送受信するには、マニフェスト `supportsFiles` のプロパティをに設定します `true` 。 このプロパティについては、Manifest [リファレンスの bots](~/resources/schema/manifest-schema.md#bots) セクションで説明します。

定義は次のように見えます `"supportsFiles": true` 。 ボットが有効にしない場合 `supportsFiles` 、このセクションに記載されている機能は機能しません。

### <a name="receive-files-in-personal-chat"></a>個人用チャットでファイルを受信する

ユーザーがボットにファイルを送信すると、最初にユーザーの OneDrive for business ストレージにファイルがアップロードされます。 その後、ボットはユーザーのアップロードについてユーザーに通知するメッセージ アクティビティを受信します。 アクティビティには、名前やコンテンツ URL などのファイル メタデータが含まれます。 ユーザーは、この URL から直接読み取ってバイナリ コンテンツを取得できます。

#### <a name="message-activity-with-file-attachment-example"></a>添付ファイルを含むメッセージ アクティビティの例

次のコードは、添付ファイルを含むメッセージ アクティビティの例を示しています。

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
| `downloadUrl` | ファイルのコンテンツをフェッチする OneDrive URL。 ユーザーは、この `HTTP GET` URL から直接発行できます。 |
| `uniqueId` | 一意のファイル ID。 これは、ユーザーがボットにファイルを送信する場合に備え、OneDrive ドライブアイテム ID です。 |
| `fileType` | ファイルの種類 (.pdf や .docx など)。 |

ベスト プラクティスとして、ユーザーにメッセージを送信してファイルのアップロードを確認します。

### <a name="upload-files-to-personal-chat"></a>個人用チャットにファイルをアップロードする

**ユーザーにファイルをアップロードするには**

1. ファイルの書き込み許可を要求するメッセージをユーザーに送信します。 このメッセージには、アップロード `FileConsentCard` するファイルの名前を含む添付ファイルが含まれている必要があります。
2. ユーザーがファイルのダウンロードを受け入れる場合、ボットは場所 URL を持つ呼び出しアクティビティを受け取ります。
3. ファイルを転送するために、ボットは指定された場所 `HTTP POST` の URL に直接実行します。
4. 必要に応じて、ユーザーが同じファイルのアップロードをさらに受け入れたくない場合は、元の同意カードを削除します。

#### <a name="message-requesting-permission-to-upload"></a>アップロードするアクセス許可を要求するメッセージ

次のデスクトップ メッセージには、ファイルをアップロードするユーザーのアクセス許可を要求する簡単な添付ファイル オブジェクトが含まれます。

![ファイルをアップロードするユーザーのアクセス許可を要求する同意カード](../../assets/images/bots/bot-file-consent-card.png)

次のモバイル メッセージには、ファイルをアップロードするユーザーのアクセス許可を要求する添付ファイル オブジェクトが含まれます。

<img src="../../assets/images/bots/mobile-bot-file-consent-card.png" alt="Consent card requesting user permission to upload file on mobile" width="350"/>

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
| `description` | ファイルの目的を説明するか、その内容を要約します。 |
| `sizeInBytes` | ユーザーに、ファイル サイズと OneDrive に必要な領域の量の推定値を提供します。 |
| `acceptContext` | ユーザーがファイルを受け入れるときにボットに無音で送信される追加のコンテキスト。 |
| `declineContext` | ユーザーがファイルを拒否するとボットに無音で送信される追加のコンテキスト。 |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>ユーザーがファイルを受け入れるときにアクティビティを呼び出す

ユーザーがファイルを受け入れる場合、呼び出しアクティビティがボットに送信されます。 OneDrive for Business プレースホルダー URL が含まれているので、ボットはファイルの内容を転送するために a `PUT` を発行できます。 OneDrive URL へのアップロードの詳細については、「アップロード セッションへのアップロード [バイト数」を参照してください](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)。

次のコードは、ボットが受け取る呼び出しアクティビティの簡潔なバージョンの例を示しています。

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

同様に、ユーザーがファイルを拒否した場合、ボットは同じ全体的なアクティビティ名を持つ次のイベントを受け取ります。

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

ユーザーの OneDrive にファイルをアップロードした後、ユーザーに確認メッセージを送信します。 メッセージには、OneDrive でプレビューまたは開く、またはローカルでダウンロードするために、ユーザーが選択できる次の添付ファイル `FileCard` が含まれている必要があります。

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
| `uniqueId` | OneDrive または SharePoint ドライブアイテム ID。 |
| `fileType` | ファイルの種類 (.pdf や .docx など)。 |

### <a name="fetch-inline-images-from-message"></a>メッセージからインライン イメージをフェッチする

ボットのアクセス トークンを使用して、メッセージの一部であるインライン イメージをフェッチします。

![インライン イメージ](../../assets/images/bots/inline-image.png)

次のコードは、メッセージからインライン イメージをフェッチする例を示しています。

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

### <a name="basic-example-in-c"></a>C の基本例#

次のコードは、ファイルのアップロードを処理し、ボットのダイアログでファイル同意要求を送信する方法の例を示しています。

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

## <a name="code-sample"></a>コード サンプル

次のコード サンプルは、ファイルの同意を取得し、ボットから Teams にファイルをアップロードする方法を示しています。

|**サンプル名** | **説明** | **.NET** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| ファイルのアップロード | ボットからファイルの同意を取得し、Teams にファイルをアップロードする方法を示します。 また、ボットに送信されたファイルを受信する方法も示します。 | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Teams でレートを制限してボットを最適化する](~/bots/how-to/rate-limit.md)
