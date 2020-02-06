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
# <a name="send-and-receive-files-through-your-bot"></a><span data-ttu-id="470a9-104">Bot を使用してファイルを送受信する</span><span class="sxs-lookup"><span data-stu-id="470a9-104">Send and receive files through your bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="470a9-105">Bot との間でファイルを送信するには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="470a9-105">There are two ways to send files to and from a bot:</span></span>

* <span data-ttu-id="470a9-106">Microsoft Graph Api を使用します。</span><span class="sxs-lookup"><span data-stu-id="470a9-106">Using the Microsoft Graph APIs.</span></span> <span data-ttu-id="470a9-107">このメソッドは Teams のすべてのスコープの bot に対して機能します。</span><span class="sxs-lookup"><span data-stu-id="470a9-107">This method works for bots in all scopes in Teams:</span></span>
  * `personal`
  * `channel`
  * `groupchat`
* <span data-ttu-id="470a9-108">Teams Api を使用します。</span><span class="sxs-lookup"><span data-stu-id="470a9-108">Using the Teams APIs.</span></span> <span data-ttu-id="470a9-109">これらは、1つのコンテキスト内のファイルのみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="470a9-109">These only support files in one context:</span></span>
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a><span data-ttu-id="470a9-110">Microsoft Graph Api を使用する</span><span class="sxs-lookup"><span data-stu-id="470a9-110">Using the Microsoft Graph APIs</span></span>

<span data-ttu-id="470a9-111">[OneDrive および SharePoint](/onedrive/developer/rest-api/)の Microsoft Graph api を使用して、既存の SharePoint ファイルを参照するカードの添付ファイルを含むメッセージを投稿できます。</span><span class="sxs-lookup"><span data-stu-id="470a9-111">You can post messages with card attachments referencing existing SharePoint files using the Microsoft Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="470a9-112">Graph Api を使用するには、標準の OAuth 2.0 認証フローを`personal`使用`groupchat`して、ユーザーの OneDrive フォルダー (およびファイルの場合`channel` ) またはチームのチャネル内のファイル (ファイルの場合) へのアクセス権を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="470a9-112">Using the Graph APIs requires obtaining access to a user's OneDrive folder (for `personal` and `groupchat` files) or the files in a team's channels (for `channel` files) through the standard OAuth 2.0 authorization flow.</span></span> <span data-ttu-id="470a9-113">このメソッドは、すべての Teams スコープで機能します。</span><span class="sxs-lookup"><span data-stu-id="470a9-113">This method works in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="470a9-114">Teams の Bot Api の使用</span><span class="sxs-lookup"><span data-stu-id="470a9-114">Using the Teams Bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="470a9-115">このメソッドは、 `personal`コンテキストでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="470a9-115">This method works only in the `personal` context.</span></span> <span data-ttu-id="470a9-116">または`channel` `groupchat`のコンテキストでは動作しません。</span><span class="sxs-lookup"><span data-stu-id="470a9-116">It does not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="470a9-117">Bot は、Teams Api を使用して、 `personal`コンテキスト内のユーザー (個人チャットとも呼ばれる) でファイルを直接送受信できます。</span><span class="sxs-lookup"><span data-stu-id="470a9-117">Your bot can directly send and receive files with users in the `personal` context, also known as personal chats, using Teams APIs.</span></span> <span data-ttu-id="470a9-118">これにより、経費報告、画像の認識、ファイルアーカイブ、電子署名、およびファイルコンテンツの直接操作を伴うその他のシナリオを実装できます。</span><span class="sxs-lookup"><span data-stu-id="470a9-118">This lets you implement expense reporting, image recognition, file archival, e-signatures, and other scenarios involving direct manipulation of file content.</span></span> <span data-ttu-id="470a9-119">Teams で共有されるファイルは、通常、カードとして表示され、アプリ内での表示を許可します。</span><span class="sxs-lookup"><span data-stu-id="470a9-119">Files shared in Teams typically appear as cards, and allow rich in-app viewing.</span></span>

<span data-ttu-id="470a9-120">次のセクションでは、メッセージの送信など、直接的なユーザー操作の結果としてファイルコンテンツを送信する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="470a9-120">The following sections describe how to do this to send file content as a result of direct user interaction, like sending a message.</span></span> <span data-ttu-id="470a9-121">この API は、Microsoft Teams の Bot プラットフォームの一部として提供されています。</span><span class="sxs-lookup"><span data-stu-id="470a9-121">This API is provided as part of the Microsoft Teams Bot Platform.</span></span>

### <a name="configure-your-bot-to-support-files"></a><span data-ttu-id="470a9-122">ボットを構成してファイルをサポートする</span><span class="sxs-lookup"><span data-stu-id="470a9-122">Configure your bot to support files</span></span>

<span data-ttu-id="470a9-123">Bot でファイルを送受信するためには、マニフェストの`supportsFiles`プロパティをに`true`設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="470a9-123">In order to send and receive files in your bot, you have to set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="470a9-124">このプロパティについては、マニフェストリファレンスの「 [bot](~/resources/schema/manifest-schema.md#bots) 」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="470a9-124">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="470a9-125">定義は、次`"supportsFiles": true`のようになります。</span><span class="sxs-lookup"><span data-stu-id="470a9-125">The definition will look like this: `"supportsFiles": true`.</span></span> <span data-ttu-id="470a9-126">Bot が有効に`supportsFiles`なっていない場合、次の機能は動作しません。</span><span class="sxs-lookup"><span data-stu-id="470a9-126">If your bot does not enable `supportsFiles`, the following features will not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="470a9-127">個人用チャットでのファイルの受信</span><span class="sxs-lookup"><span data-stu-id="470a9-127">Receiving files in personal chat</span></span>

<span data-ttu-id="470a9-128">ユーザーが bot にファイルを送信すると、そのファイルは最初にユーザーの OneDrive for Business ストレージにアップロードされます。</span><span class="sxs-lookup"><span data-stu-id="470a9-128">When a user sends a file to your bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="470a9-129">Bot は、ユーザーのアップロードを通知するメッセージアクティビティを受信します。</span><span class="sxs-lookup"><span data-stu-id="470a9-129">Your bot will then receive a message activity notifying you of the user upload.</span></span> <span data-ttu-id="470a9-130">アクティビティには、ファイルの名前やコンテンツの URL などのファイルメタデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="470a9-130">The activity will contain file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="470a9-131">この URL から直接読み取り、バイナリコンテンツを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="470a9-131">You can directly read from this URL to fetch its binary content.</span></span>

### <a name="send-and-receive-files-through-bot-on-teams-mobile-app"></a><span data-ttu-id="470a9-132">Teams モバイルアプリの bot を経由してファイルを送受信する</span><span class="sxs-lookup"><span data-stu-id="470a9-132">Send and receive files through bot on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="470a9-133">モバイルデバイスでのボットへのファイルの送信と受信はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="470a9-133">Sending and receiving files to bots on mobile devices is not supported.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="470a9-134">添付ファイルを含むメッセージアクティビティの例</span><span class="sxs-lookup"><span data-stu-id="470a9-134">Message activity with file attachment example</span></span>

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

<span data-ttu-id="470a9-135">次の表では、添付ファイルのコンテンツプロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="470a9-135">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="470a9-136">プロパティ</span><span class="sxs-lookup"><span data-stu-id="470a9-136">Property</span></span> | <span data-ttu-id="470a9-137">用途</span><span class="sxs-lookup"><span data-stu-id="470a9-137">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="470a9-138">ファイルのコンテンツを取得するための OneDrive URL。</span><span class="sxs-lookup"><span data-stu-id="470a9-138">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="470a9-139">この URL から直接`HTTP GET`を発行することができます。</span><span class="sxs-lookup"><span data-stu-id="470a9-139">You can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="470a9-140">一意のファイル ID。</span><span class="sxs-lookup"><span data-stu-id="470a9-140">Unique file ID.</span></span> <span data-ttu-id="470a9-141">これは、ユーザーが bot にファイルを送信する場合に、OneDrive ドライブのアイテム ID になります。</span><span class="sxs-lookup"><span data-stu-id="470a9-141">This will be the OneDrive drive item ID, in the case of the user sending a file to your bot.</span></span> |
| `fileType` | <span data-ttu-id="470a9-142">ファイル拡張子の種類 (pdf または .docx など)。</span><span class="sxs-lookup"><span data-stu-id="470a9-142">File extension type, such as pdf or docx.</span></span> |

<span data-ttu-id="470a9-143">ベストプラクティスとして、ユーザーにメッセージを送信して、ファイルのアップロードを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="470a9-143">As a best practice, you should acknowledge the file upload by sending back a message to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="470a9-144">個人用チャットへのファイルのアップロード</span><span class="sxs-lookup"><span data-stu-id="470a9-144">Uploading files to personal chat</span></span>

<span data-ttu-id="470a9-145">ユーザーにファイルをアップロードするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="470a9-145">Uploading a file to a user involves the following steps:</span></span>

1. <span data-ttu-id="470a9-146">ファイルを書き込むためのアクセス許可を要求しているユーザーにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="470a9-146">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="470a9-147">このメッセージには、 `FileConsentCard`アップロードするファイルの名前の添付ファイルが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="470a9-147">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="470a9-148">ユーザーがファイルのダウンロードを受け入れた場合、ボットは場所の URL を持つ*Invoke*アクティビティを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="470a9-148">If the user accepts the file download, your bot will receive an *Invoke* activity with a location URL.</span></span>
3. <span data-ttu-id="470a9-149">ファイルを転送するため、bot は`HTTP POST` 、指定された場所の URL を直接実行します。</span><span class="sxs-lookup"><span data-stu-id="470a9-149">To transfer the file, your bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="470a9-150">必要に応じて、ユーザーが同じファイルのアップロードをさらに許可しないようにする場合は、元の同意カードを削除できます。</span><span class="sxs-lookup"><span data-stu-id="470a9-150">Optionally, you can remove the original consent card if you do not want to allow the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="470a9-151">アップロード許可を要求するメッセージ</span><span class="sxs-lookup"><span data-stu-id="470a9-151">Message requesting permission to upload</span></span>

<span data-ttu-id="470a9-152">このメッセージには、ファイルをアップロードするためのユーザーアクセス許可を要求する簡単な添付ファイルオブジェクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="470a9-152">This message contains a simple attachment object requesting user permission to upload the file.</span></span>

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

<span data-ttu-id="470a9-154">次の表では、添付ファイルのコンテンツプロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="470a9-154">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="470a9-155">プロパティ</span><span class="sxs-lookup"><span data-stu-id="470a9-155">Property</span></span> | <span data-ttu-id="470a9-156">用途</span><span class="sxs-lookup"><span data-stu-id="470a9-156">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="470a9-157">ファイルの説明。</span><span class="sxs-lookup"><span data-stu-id="470a9-157">Description of the file.</span></span> <span data-ttu-id="470a9-158">ユーザーに対して、その目的を説明したり、コンテンツを要約したりするように表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="470a9-158">May be shown to the user to describe its purpose or to summarize its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="470a9-159">ユーザーに、ファイルサイズと OneDrive で必要な容量の推定値を提供します。</span><span class="sxs-lookup"><span data-stu-id="470a9-159">Provides the user an estimate of the file size and the amount of space it will take in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="470a9-160">ユーザーがファイルを受け取ったときに、ボットに自動的に送信される追加のコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="470a9-160">Additional context that will be silently transmitted to your bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="470a9-161">ユーザーがファイルを拒否したときに、ボットに自動的に送信される追加のコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="470a9-161">Additional context that will be silently transmitted to your bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="470a9-162">ユーザーがファイルを受け取ったときにアクティビティを呼び出す</span><span class="sxs-lookup"><span data-stu-id="470a9-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="470a9-163">ユーザーがファイルを受け入れるかどうかによって、呼び出しアクティビティが bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="470a9-163">An invoke activity is sent to your bot if and when the user accepts the file.</span></span> <span data-ttu-id="470a9-164">これには、ボットがを使用してファイルコンテンツを転送できる`PUT` 、OneDrive for business のプレースホルダー URL が含まれています。</span><span class="sxs-lookup"><span data-stu-id="470a9-164">It contains the OneDrive for Business placeholder URL that your bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="470a9-165">OneDrive URL へのアップロードの詳細については、「アップロード[セッションにバイトをアップロードする](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="470a9-165">for information on uploading to the OneDrive URL read this article: [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="470a9-166">次の例は、ボットが受け取る invoke アクティビティの abridged バージョンを示しています。</span><span class="sxs-lookup"><span data-stu-id="470a9-166">The following example shows an abridged version of the invoke activity that your bot will receive:</span></span>

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

<span data-ttu-id="470a9-167">同様に、ユーザーがファイルを拒否した場合、bot は次のイベントを受け取ります。これは、全体的なアクティビティ名と同じです。</span><span class="sxs-lookup"><span data-stu-id="470a9-167">Similarly, if the user declines the file, your bot will receive the following event, with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="470a9-168">アップロードしたファイルについてユーザーに通知する</span><span class="sxs-lookup"><span data-stu-id="470a9-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="470a9-169">ユーザーの OneDrive にファイルをアップロードした後、前述のメカニズムを使用するか、または OneDrive ユーザーによって委任された Api を使用するかにかかわらず、確認メッセージをユーザーに送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="470a9-169">After uploading a file to the user's OneDrive, whether you use the mechanism described above or OneDrive user delegated APIs, you should send a confirmation message to the user.</span></span> <span data-ttu-id="470a9-170">このメッセージには、 `FileCard`ユーザーがクリックできる添付ファイルが含まれています。これは、プレビューするか、OneDrive で開くか、またはローカルでダウンロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="470a9-170">This message should contain  a `FileCard` attachment that the user can click on, either to preview it, open it in OneDrive, or download locally.</span></span>

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

<span data-ttu-id="470a9-171">次の表では、添付ファイルのコンテンツプロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="470a9-171">The following table describes the content properties of the attachment:</span></span> 

| <span data-ttu-id="470a9-172">プロパティ</span><span class="sxs-lookup"><span data-stu-id="470a9-172">Property</span></span> | <span data-ttu-id="470a9-173">用途</span><span class="sxs-lookup"><span data-stu-id="470a9-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="470a9-174">OneDrive/SharePoint ドライブのアイテム ID。</span><span class="sxs-lookup"><span data-stu-id="470a9-174">OneDrive/SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="470a9-175">ファイルの種類 (pdf または .docx など)。</span><span class="sxs-lookup"><span data-stu-id="470a9-175">File type, such as pdf or docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="470a9-176">C の基本的な例#</span><span class="sxs-lookup"><span data-stu-id="470a9-176">Basic example in C#</span></span>

<span data-ttu-id="470a9-177">次の例は、ボットのダイアログでファイルのアップロードを処理し、ファイルの同意要求を送信する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="470a9-177">The following sample shows how you can handle file uploads and send file consent requests in your bot's dialog.</span></span>

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