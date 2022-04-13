---
title: ボットを介してファイルを送受信する
description: 個人用、チャネル、およびグループチャットのスコープに対してGraph API を使用して、ボットを介してファイルを送受信する方法について説明します。 v4 Bot Framework SDK に基づくコード サンプルを使用して、Teams ボット API を使用します。
keywords: teams bots files send receive
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: ebfa6bf24899d8bc88a15018b0d74d395bb56c79
ms.sourcegitcommit: 5201e7f390fbb2a9190cae1781c2f09e1746c8f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2022
ms.locfileid: "64820301"
---
# <a name="send-and-receive-files-through-the-bot"></a>ボットを介してファイルを送受信する

> [!IMPORTANT]
> このドキュメントの記事は、v4 Bot Framework SDK に基づいています。

ボットとの間でファイルを送受信するには、次の 2 つの方法があります。

* [**Microsoft Graph API を使用する:**](#use-the-graph-apis) このメソッドは、すべてのMicrosoft Teams スコープ内のボットに対して機能します。
  * `personal`
  * `channel`
  * `groupchat`

* [**Teams ボット API を使用します。**](#use-the-teams-bot-apis)これらはコンテキスト内の`personal`ファイルのみをサポートします。

## <a name="use-the-graph-apis"></a>Graph API を使用する

OneDriveとSharePointのGraph API を使用して、既存のSharePoint ファイルを参照するカード添付ファイルを含むメッセージ[を](/onedrive/developer/rest-api/)投稿します。 Graph API を使用するには、標準の OAuth 2.0 承認フローを使用して、次のいずれかにアクセスします。

* ユーザーのOneDrive フォルダー`personal`と`groupchat`ファイル。
* チームのチャネル内のファイルの `channel` ファイル。

Graph API は、すべてのTeamsスコープで機能します。 詳細については、「 [チャット メッセージ ファイルの添付ファイルの送信](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true)」を参照してください。

または、Teams ボット API を使用して、ボットとの間でファイルを送受信することもできます。

## <a name="use-the-teams-bot-apis"></a>Teams ボット API を使用する

> [!NOTE]
> Teams ボット API はコンテキストでのみ`personal`機能します。 これらは、コンテキスト内では`channel``groupchat`機能しません。

Teams API を使用して、ボットは、コンテキスト内のユーザーと直接ファイルを`personal`送受信できます。これは、個人用チャットとも呼ばれます。 経費レポート、画像認識、ファイル アーカイブ、ファイル コンテンツの編集に関連する電子署名などの機能を実装します。 Teamsで共有されているファイルは通常、カードとして表示され、アプリ内で豊富な表示が可能になります。

次のセクションでは、メッセージの送信など、ファイル コンテンツを直接ユーザー操作として送信する方法について説明します。 この API は、Teams ボット プラットフォームの一部として提供されます。

### <a name="configure-the-bot-to-support-files"></a>ファイルをサポートするようにボットを構成する

ボット内のファイルを送受信するには、マニフェスト`true`のプロパティを `supportsFiles` . このプロパティについては、マニフェストリファレンスの [bots](~/resources/schema/manifest-schema.md#bots) セクションで説明されています。

定義は次のようになります `"supportsFiles": true`。 ボットが有効 `supportsFiles`になっていない場合、このセクションに記載されている機能は機能しません。

### <a name="receive-files-in-personal-chat"></a>個人用チャットでファイルを受信する

ユーザーがボットにファイルを送信すると、最初にビジネス ストレージ用のユーザーのOneDriveにファイルがアップロードされます。 その後、ボットは、ユーザーのアップロードについてユーザーに通知するメッセージ アクティビティを受け取ります。 アクティビティには、ファイルの名前やコンテンツ URL などのファイル メタデータが含まれます。 ユーザーはこの URL から直接読み取ってバイナリ コンテンツをフェッチできます。

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

次の表では、添付ファイルのコンテンツ プロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `downloadUrl` | ファイルのコンテンツをフェッチするための URL をOneDriveします。 ユーザーはこの URL から直接発行 `HTTP GET` できます。 |
| `uniqueId` | 一意のファイル ID。 これは、ユーザーがボットにファイルを送信する場合に備えて、OneDriveドライブ項目 ID です。 |
| `fileType` | .pdfや.docxなどのファイルの種類。 |

ベスト プラクティスとして、ユーザーにメッセージを送信してファイルのアップロードを確認します。

### <a name="upload-files-to-personal-chat"></a>個人用チャットにファイルをアップロードする

ユーザーにファイルをアップロードするには:

1. ファイルを書き込むアクセス許可を要求するメッセージをユーザーに送信します。 このメッセージには、アップロードする `FileConsentCard` ファイルの名前を含む添付ファイルが含まれている必要があります。
2. ユーザーがファイルのダウンロードを受け入れた場合、ボットは場所 URL を含む呼び出しアクティビティを受け取ります。
3. ファイルを転送するために、ボットは指定された場所 URL に直接実行 `HTTP POST` します。
4. 必要に応じて、ユーザーが同じファイルの追加のアップロードを受け入れたくない場合は、元の同意カードを削除します。

#### <a name="message-requesting-permission-to-upload"></a>アップロードするアクセス許可を要求するメッセージ

次のデスクトップ メッセージには、ファイルをアップロードするためのユーザーアクセス許可を要求する単純な添付ファイル オブジェクトが含まれています。

![ファイルをアップロードするためのユーザーアクセス許可を要求する同意カード](../../assets/images/bots/bot-file-consent-card.png)

次のモバイル メッセージには、ファイルをアップロードするためのユーザーアクセス許可を要求する添付ファイル オブジェクトが含まれています。

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

次の表では、添付ファイルのコンテンツ プロパティについて説明します。

| プロパティ | 用途 |
| --- | --- |
| `description` | ファイルの目的を説明するか、その内容を要約します。 |
| `sizeInBytes` | ファイル サイズの見積もりと、OneDriveに必要な領域の量をユーザーに提供します。 |
| `acceptContext` | ユーザーがファイルを受け入れたときにボットにサイレントで送信される追加のコンテキスト。 |
| `declineContext` | ユーザーがファイルを拒否すると、ボットに自動的に送信される追加のコンテキスト。 |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>ユーザーがファイルを受け入れたときにアクティビティを呼び出す

ユーザーがファイルを受け入れた場合、呼び出しアクティビティがボットに送信されます。 これには、ボットがファイルの内容を転送するために発行`PUT`できるOneDrive for Businessプレースホルダー URL が含まれています。 OneDrive URL へのアップロードの詳細については、「[アップロード セッションへのアップロード バイト数](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)」を参照してください。

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

ユーザーのOneDriveにファイルをアップロードした後、確認メッセージをユーザーに送信します。 メッセージには、ユーザーが選択できる次`FileCard`の添付ファイルが含まれている必要があります。プレビューまたはOneDriveで開くか、ローカルでダウンロードします。

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
| `uniqueId` | ドライブアイテム ID をOneDriveまたはSharePointします。 |
| `fileType` | .pdfや.docxなどのファイルの種類。 |

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

### <a name="basic-example-in-c"></a>C の基本的な例#

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

次のコード サンプルは、ファイルの同意を取得し、ボットからTeamsにファイルをアップロードする方法を示しています。

|**サンプルの名前** | **説明** | **.NET** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| ファイルのアップロード | ファイルの同意を取得し、ボットからTeamsにファイルをアップロードする方法を示します。 また、ボットに送信されたファイルを受信する方法についても説明します。 | [表示](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [表示](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [表示](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

ステップ [バイ ステップ ガイド](../../sbs-file-handling-in-bot.yml)に従って、ボットを使用してTeamsにファイルをアップロードします。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [Teams でレートを制限してボットを最適化する](~/bots/how-to/rate-limit.md)
