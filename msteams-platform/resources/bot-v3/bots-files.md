---
title: ボットからのファイルの送受信
description: ボットからファイルを送受信する方法について説明します。
keywords: teams ボット ファイルが受信を送信する
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
# <a name="send-and-receive-files-through-your-bot"></a><span data-ttu-id="f4dc6-104">ボットを介してファイルを送受信する</span><span class="sxs-lookup"><span data-stu-id="f4dc6-104">Send and receive files through your bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="f4dc6-105">ボットにファイルを送受信するには、次の 2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-105">There are two ways to send files to and from a bot:</span></span>

* <span data-ttu-id="f4dc6-106">Microsoft Graph API を使用します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-106">Using the Microsoft Graph APIs.</span></span> <span data-ttu-id="f4dc6-107">このメソッドは、次に示すすべてのスコープのボットTeams。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-107">This method works for bots in all scopes in Teams:</span></span>
  * `personal`
  * `channel`
  * `groupchat`
* <span data-ttu-id="f4dc6-108">API のTeams使用します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-108">Using the Teams APIs.</span></span> <span data-ttu-id="f4dc6-109">これらは、1 つのコンテキストでファイルのみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-109">These only support files in one context:</span></span>
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a><span data-ttu-id="f4dc6-110">Microsoft Graph API の使用</span><span class="sxs-lookup"><span data-stu-id="f4dc6-110">Using the Microsoft Graph APIs</span></span>

<span data-ttu-id="f4dc6-111">Microsoft Graph API を使用して、既存のファイルを参照するSharePoint添付ファイルを含むメッセージOneDrive[投稿SharePoint。](/onedrive/developer/rest-api/)</span><span class="sxs-lookup"><span data-stu-id="f4dc6-111">You can post messages with card attachments referencing existing SharePoint files using the Microsoft Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="f4dc6-112">Graph API を使用するには、標準の `personal` `groupchat` OAuth 2.0 承認フローを使用して、ユーザーの OneDrive フォルダー (for and files) またはチームのチャネル (ファイル用) のファイルへのアクセスを取得する必要があります。 `channel`</span><span class="sxs-lookup"><span data-stu-id="f4dc6-112">Using the Graph APIs requires obtaining access to a user's OneDrive folder (for `personal` and `groupchat` files) or the files in a team's channels (for `channel` files) through the standard OAuth 2.0 authorization flow.</span></span> <span data-ttu-id="f4dc6-113">このメソッドは、すべてのスコープでTeamsします。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-113">This method works in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="f4dc6-114">ボット API Teams使用する</span><span class="sxs-lookup"><span data-stu-id="f4dc6-114">Using the Teams Bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="f4dc6-115">このメソッドは、コンテキストでのみ機能 `personal` します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-115">This method works only in the `personal` context.</span></span> <span data-ttu-id="f4dc6-116">またはコンテキストでは `channel` 動作 `groupchat` しません。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-116">It does not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="f4dc6-117">ボットは、ユーザーがコンテキスト内のユーザー (個人チャットとも呼ばれる) とファイルを直接送受信するには、api を使用Teams `personal` できます。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-117">Your bot can directly send and receive files with users in the `personal` context, also known as personal chats, using Teams APIs.</span></span> <span data-ttu-id="f4dc6-118">これにより、経費報告、画像認識、ファイル アーカイブ、電子署名、およびファイル コンテンツの直接操作に関するその他のシナリオを実装できます。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-118">This lets you implement expense reporting, image recognition, file archival, e-signatures, and other scenarios involving direct manipulation of file content.</span></span> <span data-ttu-id="f4dc6-119">通常、Teamsファイルはカードとして表示され、豊富なアプリ内表示が可能です。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-119">Files shared in Teams typically appear as cards, and allow rich in-app viewing.</span></span>

<span data-ttu-id="f4dc6-120">次のセクションでは、メッセージの送信など、ユーザーが直接やり取りした結果としてファイル コンテンツを送信する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-120">The following sections describe how to do this to send file content as a result of direct user interaction, like sending a message.</span></span> <span data-ttu-id="f4dc6-121">この API は、ボット プラットフォームの一部Microsoft Teams提供されます。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-121">This API is provided as part of the Microsoft Teams Bot Platform.</span></span>

### <a name="configure-your-bot-to-support-files"></a><span data-ttu-id="f4dc6-122">ファイルをサポートするためにボットを構成する</span><span class="sxs-lookup"><span data-stu-id="f4dc6-122">Configure your bot to support files</span></span>

<span data-ttu-id="f4dc6-123">ボットでファイルを送受信するには、マニフェストのプロパティをに設定 `supportsFiles` する必要があります `true` 。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-123">In order to send and receive files in your bot, you have to set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="f4dc6-124">このプロパティについては、Manifest [リファレンスの bots](~/resources/schema/manifest-schema.md#bots) セクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-124">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="f4dc6-125">定義は次のように表示されます `"supportsFiles": true` 。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-125">The definition will look like this: `"supportsFiles": true`.</span></span> <span data-ttu-id="f4dc6-126">ボットが有効にしない場合 `supportsFiles` 、次の機能は機能しません。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-126">If your bot does not enable `supportsFiles`, the following features will not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="f4dc6-127">個人用チャットでのファイルの受信</span><span class="sxs-lookup"><span data-stu-id="f4dc6-127">Receiving files in personal chat</span></span>

<span data-ttu-id="f4dc6-128">ユーザーがボットにファイルを送信すると、最初にユーザーのストレージにファイルがOneDrive for Businessされます。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-128">When a user sends a file to your bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="f4dc6-129">その後、ボットはユーザーのアップロードを通知するメッセージ アクティビティを受信します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-129">Your bot will then receive a message activity notifying you of the user upload.</span></span> <span data-ttu-id="f4dc6-130">アクティビティには、名前やコンテンツ URL などのファイル メタデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-130">The activity will contain file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="f4dc6-131">この URL から直接読み取って、バイナリ コンテンツを取得できます。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-131">You can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="f4dc6-132">添付ファイルを含むメッセージ アクティビティの例</span><span class="sxs-lookup"><span data-stu-id="f4dc6-132">Message activity with file attachment example</span></span>

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

<span data-ttu-id="f4dc6-133">次の表に、添付ファイルのコンテンツ プロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-133">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="f4dc6-134">プロパティ</span><span class="sxs-lookup"><span data-stu-id="f4dc6-134">Property</span></span> | <span data-ttu-id="f4dc6-135">用途</span><span class="sxs-lookup"><span data-stu-id="f4dc6-135">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="f4dc6-136">OneDriveファイルのコンテンツをフェッチする URL。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-136">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="f4dc6-137">この URL から `HTTP GET` 直接発行できます。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-137">You can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="f4dc6-138">一意のファイル ID。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-138">Unique file ID.</span></span> <span data-ttu-id="f4dc6-139">これは、ユーザー OneDriveボットにファイルを送信する場合のドライブ アイテム ID の一部です。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-139">This will be the OneDrive drive item ID, in the case of the user sending a file to your bot.</span></span> |
| `fileType` | <span data-ttu-id="f4dc6-140">ファイル拡張子の種類 (pdf や docx など)。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-140">File extension type, such as pdf or docx.</span></span> |

<span data-ttu-id="f4dc6-141">ベスト プラクティスとして、ユーザーにメッセージを送信してファイルのアップロードを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-141">As a best practice, you should acknowledge the file upload by sending back a message to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="f4dc6-142">個人用チャットへのファイルのアップロード</span><span class="sxs-lookup"><span data-stu-id="f4dc6-142">Uploading files to personal chat</span></span>

<span data-ttu-id="f4dc6-143">ユーザーにファイルをアップロードするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-143">Uploading a file to a user involves the following steps:</span></span>

1. <span data-ttu-id="f4dc6-144">ファイルの書き込み許可を要求するメッセージをユーザーに送信します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-144">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="f4dc6-145">このメッセージには、アップロード `FileConsentCard` するファイルの名前を含む添付ファイルが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-145">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="f4dc6-146">ユーザーがファイルのダウンロードを受け入れる場合、ボットは場所 URL を含む *Invoke* アクティビティを受信します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-146">If the user accepts the file download, your bot will receive an *Invoke* activity with a location URL.</span></span>
3. <span data-ttu-id="f4dc6-147">ファイルを転送するために、ボットは指定された場所 `HTTP POST` の URL に直接実行します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-147">To transfer the file, your bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="f4dc6-148">必要に応じて、ユーザーが同じファイルのそれ以上のアップロードを受け入れるのを許可しない場合は、元の同意カードを削除できます。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-148">Optionally, you can remove the original consent card if you do not want to allow the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="f4dc6-149">アップロードするアクセス許可を要求するメッセージ</span><span class="sxs-lookup"><span data-stu-id="f4dc6-149">Message requesting permission to upload</span></span>

<span data-ttu-id="f4dc6-150">このデスクトップ メッセージには、ファイルをアップロードするユーザーのアクセス許可を要求する簡単な添付ファイル オブジェクトが含まれている。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-150">This desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![ファイルのアップロード許可をユーザーに要求する同意カードのスクリーンショット](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="f4dc6-152">このモバイル メッセージには、ファイルをアップロードするユーザーのアクセス許可を要求する添付ファイル オブジェクトが含まれている。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-152">This mobile message contains an attachment object requesting user permission to upload the file:</span></span>

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

<span data-ttu-id="f4dc6-154">次の表に、添付ファイルのコンテンツ プロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-154">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="f4dc6-155">プロパティ</span><span class="sxs-lookup"><span data-stu-id="f4dc6-155">Property</span></span> | <span data-ttu-id="f4dc6-156">用途</span><span class="sxs-lookup"><span data-stu-id="f4dc6-156">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="f4dc6-157">ファイルの説明。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-157">Description of the file.</span></span> <span data-ttu-id="f4dc6-158">目的を説明したり、その内容を要約したりするために、ユーザーに表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-158">May be shown to the user to describe its purpose or to summarize its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="f4dc6-159">ユーザーに、ファイル サイズと、ファイルに含む容量の見積もりをOneDrive。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-159">Provides the user an estimate of the file size and the amount of space it will take in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="f4dc6-160">ユーザーがファイルを受け入れるときにボットに無音で送信される追加のコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-160">Additional context that will be silently transmitted to your bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="f4dc6-161">ユーザーがファイルを拒否した場合にボットに無音で送信される追加のコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-161">Additional context that will be silently transmitted to your bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="f4dc6-162">ユーザーがファイルを受け入れるときにアクティビティを呼び出す</span><span class="sxs-lookup"><span data-stu-id="f4dc6-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="f4dc6-163">ユーザーがファイルを受け入れる場合、呼び出しアクティビティがボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-163">An invoke activity is sent to your bot if and when the user accepts the file.</span></span> <span data-ttu-id="f4dc6-164">このページには、OneDrive for Businessコンテンツを転送するためにボットが発行できるプレース ホルダー URL `PUT` が含まれている。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-164">It contains the OneDrive for Business placeholder URL that your bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="f4dc6-165">この記事を読んで、OneDrive URL へのアップロードの詳細については、アップロード[バイトを参照してください](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-165">for information on uploading to the OneDrive URL read this article: [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="f4dc6-166">次の例は、ボットが受け取る呼び出しアクティビティの簡橋的なバージョンを示しています。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-166">The following example shows an abridged version of the invoke activity that your bot will receive:</span></span>

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

<span data-ttu-id="f4dc6-167">同様に、ユーザーがファイルを拒否した場合、ボットは同じアクティビティ名で次のイベントを受け取る予定です。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-167">Similarly, if the user declines the file, your bot will receive the following event, with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="f4dc6-168">アップロードされたファイルについてユーザーに通知する</span><span class="sxs-lookup"><span data-stu-id="f4dc6-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="f4dc6-169">ユーザーの OneDrive にファイルをアップロードした後、上記のメカニズムを使用するか、または OneDrive ユーザーが委任した API を使用するかに関わり、ユーザーに確認メッセージを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-169">After uploading a file to the user's OneDrive, whether you use the mechanism described above or OneDrive user delegated APIs, you should send a confirmation message to the user.</span></span> <span data-ttu-id="f4dc6-170">このメッセージには、ユーザーがクリックできる添付ファイルが含まれている必要があります。そのメッセージをプレビューしたり、ファイルを開OneDriveローカルで `FileCard` ダウンロードしたりします。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-170">This message should contain  a `FileCard` attachment that the user can click on, either to preview it, open it in OneDrive, or download locally.</span></span>

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

<span data-ttu-id="f4dc6-171">次の表に、添付ファイルのコンテンツ プロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-171">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="f4dc6-172">プロパティ</span><span class="sxs-lookup"><span data-stu-id="f4dc6-172">Property</span></span> | <span data-ttu-id="f4dc6-173">用途</span><span class="sxs-lookup"><span data-stu-id="f4dc6-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="f4dc6-174">OneDrive/SharePointアイテム ID。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-174">OneDrive/SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="f4dc6-175">pdf や docx などのファイルの種類。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-175">File type, such as pdf or docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="f4dc6-176">C の基本例#</span><span class="sxs-lookup"><span data-stu-id="f4dc6-176">Basic example in C#</span></span>

<span data-ttu-id="f4dc6-177">次のサンプルは、ファイルのアップロードを処理し、ボットのダイアログでファイル同意要求を送信する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="f4dc6-177">The following sample shows how you can handle file uploads and send file consent requests in your bot's dialog:</span></span>

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
