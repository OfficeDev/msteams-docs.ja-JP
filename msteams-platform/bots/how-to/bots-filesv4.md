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
# <a name="send-and-receive-files-through-the-bot"></a><span data-ttu-id="3da0d-104">ボットを介してファイルを送受信する</span><span class="sxs-lookup"><span data-stu-id="3da0d-104">Send and receive files through the bot</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3da0d-105">このドキュメントの記事は、v4 Bot Framework SDK に基づいて作成されています。</span><span class="sxs-lookup"><span data-stu-id="3da0d-105">The articles in this document are based on the v4 Bot Framework SDK.</span></span>

<span data-ttu-id="3da0d-106">ボットに対してファイルを送受信するには、次の 2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="3da0d-106">There are two ways to send files to and receive files from a bot:</span></span>

* <span data-ttu-id="3da0d-107">**Microsoft Graph API の使用:** このメソッドは、すべての Microsoft Teams スコープのボットに対して機能します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-107">**Using the Microsoft Graph APIs:** This method works for bots in all Microsoft Teams scopes:</span></span>
  * `personal`
  * `channel`
  * `groupchat`

* <span data-ttu-id="3da0d-108">**Teams ボット API の使用:** これらはコンテキスト内のファイルのみをサポート `personal` します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-108">**Using the Teams bot APIs:** These only support files in `personal` context.</span></span>

## <a name="using-the-graph-apis"></a><span data-ttu-id="3da0d-109">Graph API の使用</span><span class="sxs-lookup"><span data-stu-id="3da0d-109">Using the Graph APIs</span></span>

<span data-ttu-id="3da0d-110">OneDrive と SharePoint の Graph API を使用して、既存の SharePoint ファイルを参照するカード添付ファイルを含むメッセージ [を投稿します](/onedrive/developer/rest-api/)。</span><span class="sxs-lookup"><span data-stu-id="3da0d-110">Post messages with card attachments that refer to existing SharePoint files, using the Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="3da0d-111">Graph API を使用するには、標準の OAuth 2.0 承認フローを通じて次のいずれかのアクセス権を取得します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-111">To use the Graph APIs, obtain access to either of the following through the standard OAuth 2.0 authorization flow:</span></span>
* <span data-ttu-id="3da0d-112">ユーザーの OneDrive フォルダーと `personal` `groupchat` ファイル。</span><span class="sxs-lookup"><span data-stu-id="3da0d-112">A user's OneDrive folder for `personal` and `groupchat` files.</span></span>
* <span data-ttu-id="3da0d-113">チームのチャネル内のファイルの `channel` ファイル。</span><span class="sxs-lookup"><span data-stu-id="3da0d-113">The files in a team's channel for `channel` files.</span></span>

<span data-ttu-id="3da0d-114">Graph API は、すべての Teams スコープで動作します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-114">Graph APIs work in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="3da0d-115">Teams ボット API の使用</span><span class="sxs-lookup"><span data-stu-id="3da0d-115">Using the Teams bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="3da0d-116">Teams ボット API はコンテキストでのみ機能 `personal` します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-116">Teams bot APIs work only in the `personal` context.</span></span> <span data-ttu-id="3da0d-117">これらは、コンテキストで `channel` 機能 `groupchat` しません。</span><span class="sxs-lookup"><span data-stu-id="3da0d-117">They do not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="3da0d-118">Teams API を使用すると、ボットはコンテキスト内のユーザー (個人チャットとも呼ばれる) とファイルを直接送受信 `personal` できます。</span><span class="sxs-lookup"><span data-stu-id="3da0d-118">Using Teams APIs, the bot can directly send and receive files with users in the `personal` context, also known as personal chats.</span></span> <span data-ttu-id="3da0d-119">経費報告、画像認識、ファイル アーカイブ、ファイル コンテンツの編集に関連する電子署名などの機能を実装します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-119">Implement features, such as expense reporting, image recognition, file archival, and e-signatures involving the editing of file content.</span></span> <span data-ttu-id="3da0d-120">Teams で共有されるファイルは通常、カードとして表示され、豊富なアプリ内表示が可能です。</span><span class="sxs-lookup"><span data-stu-id="3da0d-120">Files shared in Teams typically appear as cards and allow rich in-app viewing.</span></span>

<span data-ttu-id="3da0d-121">以下のセクションでは、メッセージの送信など、ファイル コンテンツを直接のユーザー操作として送信する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-121">The following sections describe how to send file content as a direct user interaction, like sending a message.</span></span> <span data-ttu-id="3da0d-122">この API は、Teams ボット プラットフォームの一部として提供されます。</span><span class="sxs-lookup"><span data-stu-id="3da0d-122">This API is provided as part of the Teams bot platform.</span></span>

### <a name="configuring-the-bot-to-support-files"></a><span data-ttu-id="3da0d-123">ファイルをサポートするためのボットの構成</span><span class="sxs-lookup"><span data-stu-id="3da0d-123">Configuring the bot to support files</span></span>

<span data-ttu-id="3da0d-124">ボットでファイルを送受信するには、マニフェスト `supportsFiles` のプロパティを次に設定します `true` 。</span><span class="sxs-lookup"><span data-stu-id="3da0d-124">To send and receive files in the bot, set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="3da0d-125">このプロパティについては、マニフェスト リファレンス [の bots](~/resources/schema/manifest-schema.md#bots) セクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-125">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="3da0d-126">定義は次のように表示されます `"supportsFiles": true` 。</span><span class="sxs-lookup"><span data-stu-id="3da0d-126">The definition looks like this, `"supportsFiles": true`.</span></span> <span data-ttu-id="3da0d-127">ボットが有効ではない場合、このセクションに記載されている機能 `supportsFiles` は機能しません。</span><span class="sxs-lookup"><span data-stu-id="3da0d-127">If the bot does not enable `supportsFiles`, the features listed in this section do not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="3da0d-128">個人用チャットでのファイルの受信</span><span class="sxs-lookup"><span data-stu-id="3da0d-128">Receiving files in personal chat</span></span>

<span data-ttu-id="3da0d-129">ユーザーがボットにファイルを送信すると、そのファイルが最初にユーザーの OneDrive for Business ストレージにアップロードされます。</span><span class="sxs-lookup"><span data-stu-id="3da0d-129">When a user sends a file to the bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="3da0d-130">ボットは、ユーザーのアップロードについてユーザーに通知するメッセージ アクティビティを受信します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-130">The bot then receives a message activity notifying the user about the user upload.</span></span> <span data-ttu-id="3da0d-131">アクティビティには、名前やコンテンツ URL などのファイル メタデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="3da0d-131">The activity contains file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="3da0d-132">ユーザーは、この URL から直接読み取って、バイナリ コンテンツを取得できます。</span><span class="sxs-lookup"><span data-stu-id="3da0d-132">The user can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="3da0d-133">添付ファイルを含むメッセージ アクティビティの例</span><span class="sxs-lookup"><span data-stu-id="3da0d-133">Message activity with file attachment example</span></span>

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

<span data-ttu-id="3da0d-134">次の表では、添付ファイルのコンテンツ プロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-134">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="3da0d-135">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3da0d-135">Property</span></span> | <span data-ttu-id="3da0d-136">用途</span><span class="sxs-lookup"><span data-stu-id="3da0d-136">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="3da0d-137">ファイルのコンテンツをフェッチする OneDrive URL。</span><span class="sxs-lookup"><span data-stu-id="3da0d-137">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="3da0d-138">ユーザーは、この `HTTP GET` URL から直接発行できます。</span><span class="sxs-lookup"><span data-stu-id="3da0d-138">The user can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="3da0d-139">一意のファイル ID。</span><span class="sxs-lookup"><span data-stu-id="3da0d-139">Unique file ID.</span></span> <span data-ttu-id="3da0d-140">これは、ユーザーがボットにファイルを送信する場合の OneDrive ドライブアイテム ID です。</span><span class="sxs-lookup"><span data-stu-id="3da0d-140">This is the OneDrive drive item ID, in case the user sends a file to the bot.</span></span> |
| `fileType` | <span data-ttu-id="3da0d-141">ファイルの種類 (.pdf、.docx など)。</span><span class="sxs-lookup"><span data-stu-id="3da0d-141">Type of file, such as .pdf or .docx.</span></span> |

<span data-ttu-id="3da0d-142">ベスト プラクティスとして、ユーザーにメッセージを送信してファイルのアップロードを確認します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-142">As a best practice, acknowledge the file upload by sending a message back to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="3da0d-143">個人用チャットへのファイルのアップロード</span><span class="sxs-lookup"><span data-stu-id="3da0d-143">Uploading files to personal chat</span></span>

<span data-ttu-id="3da0d-144">ユーザーにファイルをアップロードするには、次の手順が必要です。</span><span class="sxs-lookup"><span data-stu-id="3da0d-144">The following steps are required to upload a file to a user:</span></span>

1. <span data-ttu-id="3da0d-145">ファイルを書き込む権限を要求しているユーザーにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-145">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="3da0d-146">このメッセージには、アップロード `FileConsentCard` するファイルの名前を含む添付ファイルが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="3da0d-146">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="3da0d-147">ユーザーがファイルのダウンロードを受け入れる場合、ボットは場所 URL を含む呼び出しアクティビティを受信します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-147">If the user accepts the file download, the bot receives an invoke activity with a location URL.</span></span>
3. <span data-ttu-id="3da0d-148">ファイルを転送するために、ボットは指定された場所の `HTTP POST` URL に直接実行します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-148">To transfer the file, the bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="3da0d-149">必要に応じて、ユーザーが同じファイルのそれ以上のアップロードを受け入れたくない場合は、元の同意カードを削除します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-149">Optionally, remove the original consent card if you do not want the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="3da0d-150">アップロードするアクセス許可を要求しているメッセージ</span><span class="sxs-lookup"><span data-stu-id="3da0d-150">Message requesting permission to upload</span></span>

<span data-ttu-id="3da0d-151">次のデスクトップ メッセージには、ファイルをアップロードするユーザーのアクセス許可を要求する簡単な添付ファイル オブジェクトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="3da0d-151">The following desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![ファイルをアップロードするユーザーのアクセス許可を要求している同意カード](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="3da0d-153">次のモバイル メッセージには、ファイルをアップロードするユーザーのアクセス許可を要求する添付ファイル オブジェクトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="3da0d-153">The following mobile message contains an attachment object requesting user permission to upload the file:</span></span>

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

<span data-ttu-id="3da0d-155">次の表では、添付ファイルのコンテンツ プロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-155">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="3da0d-156">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3da0d-156">Property</span></span> | <span data-ttu-id="3da0d-157">用途</span><span class="sxs-lookup"><span data-stu-id="3da0d-157">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="3da0d-158">ファイルの目的を説明するか、コンテンツを要約します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-158">Describes the purpose of the file or summarizes its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="3da0d-159">ユーザーに、OneDrive でのファイル サイズと必要な領域の量の見積もりを提供します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-159">Provides the user an estimate of the file size and the amount of space it takes in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="3da0d-160">ユーザーがファイルを受け入れるときにボットにサイレントモードで送信される追加のコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="3da0d-160">Additional context that is silently transmitted to the bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="3da0d-161">ユーザーがファイルを拒否するとボットにサイレント送信される追加のコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="3da0d-161">Additional context that is silently transmitted to the bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="3da0d-162">ユーザーがファイルを受け入れるときにアクティビティを呼び出す</span><span class="sxs-lookup"><span data-stu-id="3da0d-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="3da0d-163">ユーザーがファイルを受け入れる場合、いつ、呼び出しアクティビティがボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="3da0d-163">An invoke activity is sent to the bot if and when the user accepts the file.</span></span> <span data-ttu-id="3da0d-164">ボットがファイルの内容を転送するために発行できる OneDrive for Business プレースホルダー URL `PUT` が含まれている。</span><span class="sxs-lookup"><span data-stu-id="3da0d-164">It contains the OneDrive for Business placeholder URL that the bot can then issue a `PUT` to transfer the file contents.</span></span> <span data-ttu-id="3da0d-165">OneDrive URL へのアップロードの詳細については、アップロード セッションへの [アップロード バイトを参照してください](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)。</span><span class="sxs-lookup"><span data-stu-id="3da0d-165">For information on uploading to the OneDrive URL, see [upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="3da0d-166">次の例は、ボットが受け取る呼び出しアクティビティの簡潔なバージョンを示しています。</span><span class="sxs-lookup"><span data-stu-id="3da0d-166">The following example shows a concise version of the invoke activity that the bot receives:</span></span>

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

<span data-ttu-id="3da0d-167">同様に、ユーザーがファイルを辞退すると、ボットは同じアクティビティ名で次のイベントを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="3da0d-167">Similarly, if the user declines the file, the bot receives the following event with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="3da0d-168">アップロードされたファイルについてユーザーに通知する</span><span class="sxs-lookup"><span data-stu-id="3da0d-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="3da0d-169">ユーザーの OneDrive にファイルをアップロードした後、ユーザーに確認メッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-169">After uploading a file to the user's OneDrive, send a confirmation message to the user.</span></span> <span data-ttu-id="3da0d-170">メッセージには、OneDrive でプレビューまたは開く、またはローカルにダウンロードするために、ユーザーが選択できる次の添付ファイルが `FileCard` 含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="3da0d-170">The message must contain the following `FileCard` attachment that the user can select, either to preview or open it in OneDrive, or download locally:</span></span>

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

<span data-ttu-id="3da0d-171">次の表では、添付ファイルのコンテンツ プロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-171">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="3da0d-172">プロパティ</span><span class="sxs-lookup"><span data-stu-id="3da0d-172">Property</span></span> | <span data-ttu-id="3da0d-173">用途</span><span class="sxs-lookup"><span data-stu-id="3da0d-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="3da0d-174">OneDrive または SharePoint ドライブアイテム ID。</span><span class="sxs-lookup"><span data-stu-id="3da0d-174">OneDrive or SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="3da0d-175">ファイルの種類 (.pdf、.docx など)。</span><span class="sxs-lookup"><span data-stu-id="3da0d-175">Type of file, such as .pdf or .docx.</span></span> |

### <a name="fetching-inline-images-from-message"></a><span data-ttu-id="3da0d-176">メッセージからインライン 画像を取得する</span><span class="sxs-lookup"><span data-stu-id="3da0d-176">Fetching inline images from message</span></span>

<span data-ttu-id="3da0d-177">ボットのアクセス トークンを使用して、メッセージの一部であるインライン 画像を取得します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-177">Fetch inline images that are part of the message using the Bot's access token.</span></span>

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

### <a name="basic-example-in-c"></a><span data-ttu-id="3da0d-179">C の基本的な例#</span><span class="sxs-lookup"><span data-stu-id="3da0d-179">Basic example in C#</span></span>

<span data-ttu-id="3da0d-180">次のサンプルは、ボットのダイアログでファイルのアップロードを処理し、ファイル同意要求を送信する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3da0d-180">The following sample shows how to handle file uploads and send file consent requests in the bot's dialog:</span></span>

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

### <a name="code-sample"></a><span data-ttu-id="3da0d-181">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="3da0d-181">Code sample</span></span>

|<span data-ttu-id="3da0d-182">**サンプルの名前**</span><span class="sxs-lookup"><span data-stu-id="3da0d-182">**Sample name**</span></span> | <span data-ttu-id="3da0d-183">**説明**</span><span class="sxs-lookup"><span data-stu-id="3da0d-183">**Description**</span></span> | <span data-ttu-id="3da0d-184">**.NETCore**</span><span class="sxs-lookup"><span data-stu-id="3da0d-184">**.NETCore**</span></span> | <span data-ttu-id="3da0d-185">**Javascript**</span><span class="sxs-lookup"><span data-stu-id="3da0d-185">**Javascript**</span></span> | <span data-ttu-id="3da0d-186">**Python**</span><span class="sxs-lookup"><span data-stu-id="3da0d-186">**Python**</span></span>|
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="3da0d-187">ファイルのアップロード</span><span class="sxs-lookup"><span data-stu-id="3da0d-187">File upload</span></span> | <span data-ttu-id="3da0d-188">ボットからファイルの同意を取得し、Teams にファイルをアップロードする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-188">Demonstrates how to obtain file consent and upload files to Teams from a bot.</span></span> <span data-ttu-id="3da0d-189">また、ボットに送信されたファイルを受信する方法も示します。</span><span class="sxs-lookup"><span data-stu-id="3da0d-189">Also, how to receive a file sent to a bot.</span></span> | [<span data-ttu-id="3da0d-190">View</span><span class="sxs-lookup"><span data-stu-id="3da0d-190">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [<span data-ttu-id="3da0d-191">View</span><span class="sxs-lookup"><span data-stu-id="3da0d-191">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [<span data-ttu-id="3da0d-192">View</span><span class="sxs-lookup"><span data-stu-id="3da0d-192">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |
