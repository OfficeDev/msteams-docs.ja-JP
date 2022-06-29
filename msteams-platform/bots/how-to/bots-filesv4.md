---
title: ボットを使用してファイルを送受信する
description: 個人用スコープ、チャネル スコープ、グループチャット スコープの Graph API を使用して、ボットを通じてファイルを送受信する方法について説明します。
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 3fdf39c18743c991610c266a58e37e0109ffbf05
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503880"
---
# <a name="send-and-receive-files-using-bot"></a>ボットを使用してファイルを送受信する

> [!IMPORTANT]
> このドキュメントの記事は、v4 Bot Framework SDK に基づいています。

ボットからファイルを送受信するには、次の 2 つの方法があります。

* [**Microsoft Graph API を使用する:**](#use-the-graph-apis) このメソッドは、すべてのMicrosoft Teams スコープ内のボットに対して機能します。
  * `personal`
  * `channel`
  * `groupchat`

* [**Teams ボット API を使用する:**](#use-the-teams-bot-apis) これらは `personal` コンテキスト内のファイルのみをサポートします。

## <a name="use-the-graph-apis"></a>Graph API を使用する

[OneDrive および SharePoint](/onedrive/developer/rest-api/) 用の Graph API を使用して、既存の SharePoint ファイルを参照するカードが添付されたメッセージを投稿します。 Graph API を使用するには、標準の OAuth 2.0 承認フローを使用して、次のいずれかにアクセスします。

* ユーザーの OneDrive フォルダー `personal` および `groupchat` ファイル。
* チームのチャネル内のファイルの `channel` ファイル。

Graph API は、すべての Teams スコープで機能します。 詳細については、「[チャット メッセージ ファイルの添付ファイルの送信](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true)」を参照してください。

または、Teams ボット API を使用して、ボットとの間でファイルを送受信することもできます。

## <a name="use-the-teams-bot-apis"></a>Teams ボット API を使用する

> [!NOTE]
> Teams ボット API は `personal` コンテキストでのみ機能します。 `channel` または `groupchat` のコンテキストでは機能しません。

ボットは、Teams API を使用して、`personal` コンテキスト (個人用チャットとも呼ばれます) のユーザーとファイルを直接送受信できます。 経費レポート、画像認識、ファイル アーカイブ、ファイル コンテンツの編集に関連する電子署名などの機能を実装します。 Teams で共有されるファイルは通常、カードとして表示され、アプリ内で豊富に表示できます。

次のセクションでは、メッセージの送信など、ユーザーとの直接的なやり取りとしてファイル コンテンツを送信する方法について説明します。 この API は、Teams ボット プラットフォームの一部として提供されます。

### <a name="configure-the-bot-to-support-files"></a>ファイルをサポートするようにボットを構成する

ボットでファイルを送受信するには、マニフェストの `supportsFiles` プロパティを `true` に設定する必要があります。 このプロパティは、マニフェスト リファレンスの[ボット](~/resources/schema/manifest-schema.md#bots) セクションで説明されています。

NDR は、次のようになっています: `"supportsFiles": true`。 ボットが `supportsFiles` を有効にしない場合、このセクションにリストされている機能は機能しません。

### <a name="receive-files-in-personal-chat"></a>個人用チャットでファイルを受信する

ユーザーがボットにファイルを送信すると、ファイルは最初にユーザーの OneDrive for Business ストレージにアップロードされます。 その後、ボットは、ユーザーのアップロードについてユーザーに通知するメッセージ アクティビティを受け取ります。 アクティビティには、名前やコンテンツ URL などのファイル メタデータが含まれます。 ユーザーは、この URL から直接読み取って、バイナリ コンテンツを取得できます。

#### <a name="message-activity-with-file-attachment-example"></a>ファイル添付の例を使用したメッセージ アクティビティ

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

次の表で、添付ファイルのコンテンツ プロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `downloadUrl` | ファイルのコンテンツを取得するための OneDrive URL。 この URL から直接 `HTTP GET` を発行できます。 |
| `uniqueId` | 一意のファイル ID。 ユーザーがボットにファイルを送信する場合、これは OneDrive ドライブ アイテム ID になります。 |
| `fileType` | .pdf や .docx などのファイルの種類。 |

ベスト プラクティスとして、ユーザーにメッセージを送信してファイルのアップロードを確認します。

### <a name="upload-files-to-personal-chat"></a>個人用チャットへのファイルのアップロード

ユーザーにファイルをアップロードするには:

1. ファイルの書き込み許可を要求するメッセージをユーザーに送信します。 このメッセージには、アップロードするファイルの名前が記載された `FileConsentCard` 個の添付ファイルが含まれている必要があります。
2. ユーザーがファイルのダウンロードを受け入れると、ボットはロケーション URL を使用して Invoke アクティビティを受け取ります。
3. ファイルを転送するために、ボットは指定されたロケーション URL に直接 `HTTP POST` を実行します。
4. ユーザーが同じファイルのそれ以上のアップロードを受け入れないようにする場合は、必要に応じて、元の同意カードを削除します。

#### <a name="message-requesting-permission-to-upload"></a>アップロードの許可を求めるメッセージ

次のデスクトップ メッセージには、ファイルをアップロードするためのユーザー権限を要求する単純な添付オブジェクトが含まれています。

:::image type="content" source="../../assets/images/bots/bot-file-consent-card.png" alt-text="ファイルのアップロードに対するユーザー権限を要求する同意カード"lightbox="../../assets/images/bots/bot-file-consent-card.png"border="true":::

次のモバイル メッセージには、ファイルをアップロードするためのユーザー権限を要求する添付オブジェクトが含まれています。

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

次の表で、添付ファイルのコンテンツ プロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `description` | ファイルの目的を説明するか、その内容を要約します。 |
| `sizeInBytes` | OneDrive で必要なファイル サイズと容量の見積もりをユーザーに提供します。 |
| `acceptContext` | ファイルを受け入れると、ボットにサイレントに送信される追加のコンテキスト。 |
| `declineContext` | ユーザーがファイルを拒否したときにボットにサイレントに送信される追加のコンテキスト。 |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>ユーザーがファイルを受け入れたときにアクティビティを呼び出す

ユーザーがファイルを受け入れると、呼び出しアクティビティがボットに送信されます。 これには、ボットが `PUT` を発行してファイルの内容を転送できる OneDrive for Business プレースホルダー URL が含まれています。 OneDrive URL へのアップロードについては、「[アップロード セッションにバイトをアップロードする](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)」をご覧ください。

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

同様に、ユーザーがファイルを拒否すると、ボットは同じ全体的なアクティビティ名で次のイベントを受け取ります。

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

ユーザーの OneDrive にファイルをアップロードした後、ユーザーに確認メッセージを送信します。 メッセージには、ユーザーが OneDrive でプレビューまたは開くか、ローカルでダウンロードするために選択できる次の `FileCard` 添付ファイルが含まれている必要があります。

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

次の表で、添付ファイルのコンテンツ プロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `uniqueId` | OneDrive または SharePoint ドライブのアイテム ID。 |
| `fileType` | .pdf や .docx などのファイルの種類。 |

### <a name="fetch-inline-images-from-message"></a>メッセージからインライン イメージをフェッチする

ボットのアクセス トークンを使用して、メッセージの一部であるインライン イメージをフェッチします。

:::image type="content" source="../../assets/images/bots/inline-image.png" alt-text="インライン イメージ"border="true":::

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

### <a name="basic-example-in-c"></a>C の基本的な例 #

次のコードは、ボットのダイアログでファイルのアップロードを処理し、ファイルの同意リクエストを送信する方法の例を示しています。

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

|**サンプルの名前** | **説明** | **.NET** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| ファイルのアップロード | ファイルの同意を取得し、ボットから Teams にファイルをアップロードする方法を示します。 また、ボットに送信されたファイルを受信する方法についても説明します。 | [表示](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [表示](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [表示](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

[ステップ バイ ステップ ガイド](../../sbs-file-handling-in-bot.yml)に従って、ボットを使用して Teams にファイルをアップロードします。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [Teams でレートを制限してボットを最適化する](~/bots/how-to/rate-limit.md)

## <a name="see-also"></a>関連項目

[Microsoft Teams の保護された API](/graph/teams-protected-apis)
