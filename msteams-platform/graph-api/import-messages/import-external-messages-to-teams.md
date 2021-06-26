---
title: Microsoft Graphを使用して外部プラットフォーム メッセージをインポートTeams
description: Microsoft Graph を使用して外部プラットフォームからメッセージをインポートする方法についてTeams
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 95cbf6bf2deac4ea71e60fe0fece06c1dd3ad24c
ms.sourcegitcommit: 656a1de9e23e0ad90dddcb93a2bbfcc63848a856
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53130095"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="cebd9-104">Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする</span><span class="sxs-lookup"><span data-stu-id="cebd9-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

<span data-ttu-id="cebd9-105">Microsoft Graphを使用すると、ユーザーの既存のメッセージ履歴とデータを外部システムから別のチャネルにTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-105">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="cebd9-106">Teams 内のサード パーティプラットフォーム メッセージング階層のレクリエーションを有効にすると、ユーザーはシームレスな方法で通信を続行し、中断することなく続行できます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-106">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE]
> <span data-ttu-id="cebd9-107">今後、Microsoft は、インポートされるデータの量に基づいて、お客様またはお客様の顧客に追加料金の支払いを要求する場合があります。</span><span class="sxs-lookup"><span data-stu-id="cebd9-107">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="cebd9-108">インポートの概要</span><span class="sxs-lookup"><span data-stu-id="cebd9-108">Import overview</span></span>

<span data-ttu-id="cebd9-109">高レベルでは、インポート プロセスは次で構成されます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-109">At a high level, the import process consists of the following:</span></span>

1. <span data-ttu-id="cebd9-110">[タイム スタンプを使用してチームを作成します](#step-1-create-a-team)。</span><span class="sxs-lookup"><span data-stu-id="cebd9-110">[Create a team with a back-in-time timestamp](#step-1-create-a-team).</span></span>
1. <span data-ttu-id="cebd9-111">[タイム スタンプを使用してチャネルを作成します](#step-2-create-a-channel)。</span><span class="sxs-lookup"><span data-stu-id="cebd9-111">[Create a channel with a back-in-time timestamp](#step-2-create-a-channel).</span></span>
1. <span data-ttu-id="cebd9-112">[外部のバックインタイム日付メッセージをインポートします](#step-3-import-messages)。</span><span class="sxs-lookup"><span data-stu-id="cebd9-112">[Import external back-in-time dated messages](#step-3-import-messages).</span></span>
1. <span data-ttu-id="cebd9-113">[チームとチャネルの移行プロセスを完了します](#step-4-complete-migration-mode)。</span><span class="sxs-lookup"><span data-stu-id="cebd9-113">[Complete the team and channel migration process](#step-4-complete-migration-mode).</span></span>
1. <span data-ttu-id="cebd9-114">[チーム メンバーを追加します](#step-five-add-team-members)。</span><span class="sxs-lookup"><span data-stu-id="cebd9-114">[Add team members](#step-five-add-team-members).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cebd9-115">前提条件</span><span class="sxs-lookup"><span data-stu-id="cebd9-115">Prerequisites</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="cebd9-116">メッセージ データの分析と準備</span><span class="sxs-lookup"><span data-stu-id="cebd9-116">Analyze and prepare message data</span></span>

* <span data-ttu-id="cebd9-117">サード パーティのデータを確認して、移行するデータを決定します。</span><span class="sxs-lookup"><span data-stu-id="cebd9-117">Review the third-party data to decide what will be migrated.</span></span>  
* <span data-ttu-id="cebd9-118">選択したデータをサードパーティのチャット システムから抽出します。</span><span class="sxs-lookup"><span data-stu-id="cebd9-118">Extract the selected data from the third-party chat system.</span></span>  
* <span data-ttu-id="cebd9-119">サード パーティ製のチャット構造を、その他のTeamsします。</span><span class="sxs-lookup"><span data-stu-id="cebd9-119">Map the third-party chat structure to the Teams structure.</span></span>  
* <span data-ttu-id="cebd9-120">インポート データを移行に必要な形式に変換します。</span><span class="sxs-lookup"><span data-stu-id="cebd9-120">Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="cebd9-121">Office 365 テナントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="cebd9-121">Set up your Office 365 tenant</span></span>

* <span data-ttu-id="cebd9-122">インポート データにOffice 365テナントが存在することを確認します。</span><span class="sxs-lookup"><span data-stu-id="cebd9-122">Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="cebd9-123">ユーザーのテナントを設定する方法のOffice 365については、「Teamsテナントの準備[」をOffice 365してください](../../concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="cebd9-123">For more information on setting up an Office 365 tenancy for Teams, see [prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
* <span data-ttu-id="cebd9-124">チーム メンバーが (AAD) Azure Active Directory確認します。</span><span class="sxs-lookup"><span data-stu-id="cebd9-124">Make sure that team members are in Azure Active Directory (AAD).</span></span> <span data-ttu-id="cebd9-125">詳細については、「AAD に [新しいユーザーを追加する](/azure/active-directory/fundamentals/add-users-azure-active-directory) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cebd9-125">For more information, see [add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to AAD.</span></span>

## <a name="step-1-create-a-team"></a><span data-ttu-id="cebd9-126">手順 1: チームを作成する</span><span class="sxs-lookup"><span data-stu-id="cebd9-126">Step 1: Create a team</span></span>

<span data-ttu-id="cebd9-127">既存のデータを移行する場合は、元のメッセージ タイムスタンプを維持し、移行プロセス中にメッセージング アクティビティを防止する方法が、Teams でユーザーの既存のメッセージ フローを再作成する際に重要です。</span><span class="sxs-lookup"><span data-stu-id="cebd9-127">Since you are migrating existing data, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="cebd9-128">これは、次のように実現されます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-128">This is achieved as follows:</span></span>

> <span data-ttu-id="cebd9-129">[チーム リソース プロパティを使用して](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) 、タイム スタンプを使用して新しいチームを作成 `createdDateTime` します。</span><span class="sxs-lookup"><span data-stu-id="cebd9-129">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource `createdDateTime` property.</span></span> <span data-ttu-id="cebd9-130">移行プロセスが完了するまで、チーム内のほとんどのアクティビティからユーザーを制限する特別な状態で、新しいチーム `migration mode` を配置します。</span><span class="sxs-lookup"><span data-stu-id="cebd9-130">Place the new team in `migration mode`, a special state that restricts users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="cebd9-131">新しいチームが移行用に作成されているとして明示的に識別するには、POST 要求に値を持つ `teamCreationMode` `migration` instance 属性を含める。</span><span class="sxs-lookup"><span data-stu-id="cebd9-131">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> [!NOTE]
> <span data-ttu-id="cebd9-132">この `createdDateTime` フィールドは、移行されたチームまたはチャネルのインスタンスにのみ設定されます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-132">The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permission"></a><span data-ttu-id="cebd9-133">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="cebd9-133">Permission</span></span>

|<span data-ttu-id="cebd9-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="cebd9-134">ScopeName</span></span>|<span data-ttu-id="cebd9-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="cebd9-135">DisplayName</span></span>|<span data-ttu-id="cebd9-136">説明</span><span class="sxs-lookup"><span data-stu-id="cebd9-136">Description</span></span>|<span data-ttu-id="cebd9-137">型</span><span class="sxs-lookup"><span data-stu-id="cebd9-137">Type</span></span>|<span data-ttu-id="cebd9-138">管理者の同意</span><span class="sxs-lookup"><span data-stu-id="cebd9-138">Admin Consent?</span></span>|<span data-ttu-id="cebd9-139">対象のエンティティ/API</span><span class="sxs-lookup"><span data-stu-id="cebd9-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="cebd9-140">Microsoft Teams への移行の管理</span><span class="sxs-lookup"><span data-stu-id="cebd9-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="cebd9-141">ユーザーへの移行用のリソースの作成とMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="cebd9-141">Creating and managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="cebd9-142">**アプリケーション専用**</span><span class="sxs-lookup"><span data-stu-id="cebd9-142">**Application-only**</span></span>|<span data-ttu-id="cebd9-143">**はい**</span><span class="sxs-lookup"><span data-stu-id="cebd9-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="cebd9-144">要求 (移行状態でチームを作成する)</span><span class="sxs-lookup"><span data-stu-id="cebd9-144">Request (create a team in migration state)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/v1.0/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a><span data-ttu-id="cebd9-145">応答</span><span class="sxs-lookup"><span data-stu-id="cebd9-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-message"></a><span data-ttu-id="cebd9-146">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="cebd9-146">Error message</span></span>

```http
400 Bad Request
```

<span data-ttu-id="cebd9-147">次のシナリオでエラー メッセージを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="cebd9-147">You can receive the error message in the following scenarios:</span></span>

* <span data-ttu-id="cebd9-148">If `createdDateTime` は将来に設定されます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-148">If `createdDateTime` is set for future.</span></span>
* <span data-ttu-id="cebd9-149">正 `createdDateTime` しく指定されているが `teamCreationMode` 、instance 属性が見つからないか、無効な値に設定されている場合。</span><span class="sxs-lookup"><span data-stu-id="cebd9-149">If `createdDateTime` is correctly specified, but `teamCreationMode` instance attribute is missing or set to invalid value.</span></span>

## <a name="step-2-create-a-channel"></a><span data-ttu-id="cebd9-150">手順 2: チャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="cebd9-150">Step 2: Create a channel</span></span>

<span data-ttu-id="cebd9-151">インポートされたメッセージのチャネルの作成は、チームの作成シナリオに似ています。</span><span class="sxs-lookup"><span data-stu-id="cebd9-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="cebd9-152">[チャネル リソース プロパティを使用](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) して、タイム スタンプをバックインする新しいチャネルを作成 `createdDateTime` します。</span><span class="sxs-lookup"><span data-stu-id="cebd9-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="cebd9-153">移行プロセスが完了するまで、チャネル内のほとんどのチャット アクティビティからユーザーを制限する特別な状態で、新しいチャネル `migration mode` を配置します。</span><span class="sxs-lookup"><span data-stu-id="cebd9-153">Place the new channel in `migration mode`, a special state that restricts users from most chat activities within the channel until the migration process is complete.</span></span> <span data-ttu-id="cebd9-154">新しいチームが移行用に作成されているとして明示的に識別するには、POST 要求に値を持つ `channelCreationMode` `migration` instance 属性を含める。</span><span class="sxs-lookup"><span data-stu-id="cebd9-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permission"></a><span data-ttu-id="cebd9-155">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="cebd9-155">Permission</span></span>

|<span data-ttu-id="cebd9-156">ScopeName</span><span class="sxs-lookup"><span data-stu-id="cebd9-156">ScopeName</span></span>|<span data-ttu-id="cebd9-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="cebd9-157">DisplayName</span></span>|<span data-ttu-id="cebd9-158">説明</span><span class="sxs-lookup"><span data-stu-id="cebd9-158">Description</span></span>|<span data-ttu-id="cebd9-159">型</span><span class="sxs-lookup"><span data-stu-id="cebd9-159">Type</span></span>|<span data-ttu-id="cebd9-160">管理者の同意</span><span class="sxs-lookup"><span data-stu-id="cebd9-160">Admin Consent?</span></span>|<span data-ttu-id="cebd9-161">対象のエンティティ/API</span><span class="sxs-lookup"><span data-stu-id="cebd9-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="cebd9-162">Microsoft Teams への移行の管理</span><span class="sxs-lookup"><span data-stu-id="cebd9-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="cebd9-163">ユーザーへの移行用のリソースの作成とMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="cebd9-163">Creating and managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="cebd9-164">**アプリケーション専用**</span><span class="sxs-lookup"><span data-stu-id="cebd9-164">**Application-only**</span></span>|<span data-ttu-id="cebd9-165">**はい**</span><span class="sxs-lookup"><span data-stu-id="cebd9-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="cebd9-166">要求 (移行状態でチャネルを作成する)</span><span class="sxs-lookup"><span data-stu-id="cebd9-166">Request (create a channel in migration state)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/{team-id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.047Z"
}
```

#### <a name="response"></a><span data-ttu-id="cebd9-167">応答</span><span class="sxs-lookup"><span data-stu-id="cebd9-167">Response</span></span>

```http
HTTP/1.1 202 Accepted

{
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels/$entity",
   "id":"id-value",
   "createdDateTime":null,
   "displayName":"Architecture Discussion",
   "description":"This channel is where we debate all future architecture plans",
   "isFavoriteByDefault":null,
   "email":null,
   "webUrl":null,
   "membershipType":null,
   "moderationSettings":null
}
```

#### <a name="error-message"></a><span data-ttu-id="cebd9-168">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="cebd9-168">Error message</span></span>

```http
400 Bad Request
```
<span data-ttu-id="cebd9-169">次のシナリオでエラー メッセージを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="cebd9-169">You can receive the error message in the following scenarios:</span></span>

* <span data-ttu-id="cebd9-170">If `createdDateTime` は将来に設定されます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-170">If `createdDateTime` is set for future.</span></span>
* <span data-ttu-id="cebd9-171">正 `createdDateTime` しく指定されているが、 `channelCreationMode` インスタンス属性が見つからないか、無効な値に設定されている場合。</span><span class="sxs-lookup"><span data-stu-id="cebd9-171">If `createdDateTime` is correctly specified but `channelCreationMode` instance attribute is missing or set to invalid value.</span></span>

## <a name="step-3-import-messages"></a><span data-ttu-id="cebd9-172">手順 3: メッセージのインポート</span><span class="sxs-lookup"><span data-stu-id="cebd9-172">Step 3: Import messages</span></span>

<span data-ttu-id="cebd9-173">チームとチャネルを作成したら、要求本文のキーとキーを使用して、バックインタイム メッセージ `createdDateTime` `from` の送信を開始できます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-173">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from` keys in the request body.</span></span>

> [!NOTE]
> * <span data-ttu-id="cebd9-174">メッセージ スレッドより `createdDateTime` 前にインポートされたメッセージ `createdDateTime` はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="cebd9-174">Messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>
> * <span data-ttu-id="cebd9-175">`createdDateTime` 同じスレッド内のメッセージ間で一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="cebd9-175">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="cebd9-176">`createdDateTime` ミリ秒単位の精度のタイムスタンプをサポートします。</span><span class="sxs-lookup"><span data-stu-id="cebd9-176">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="cebd9-177">たとえば、受信要求メッセージの値が `createdDateTime` *2020-09-16T05:50:31.0025302Z* の場合、メッセージが取り込まれたときに *2020-09-16T05:50:31.002Z* に変換されます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-177">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="cebd9-178">要求 (テキスト専用の POST メッセージ)</span><span class="sxs-lookup"><span data-stu-id="cebd9-178">Request (POST message that is text-only)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

{
   "createdDateTime":"2019-02-04T19:58:15.511Z",
   "from":{
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   }
}
```

#### <a name="response"></a><span data-ttu-id="cebd9-179">応答</span><span class="sxs-lookup"><span data-stu-id="cebd9-179">Response</span></span>

```http
HTTP/1.1 200 OK

{
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
   "id":"id-value",
   "replyToId":null,
   "etag":"id-value",
   "messageType":"message",
   "createdDateTime":"2019-02-04T19:58:15.58Z",
   "lastModifiedDateTime":null,
   "deleted":false,
   "subject":null,
   "summary":null,
   "importance":"normal",
   "locale":"en-us",
   "policyViolation":null,
   "from":{
      "application":null,
      "device":null,
      "conversation":null,
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   },
   "attachments":[
   ],
   "mentions":[
   ],
   "reactions":[
   ]
}
```

#### <a name="error-message"></a><span data-ttu-id="cebd9-180">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="cebd9-180">Error message</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="cebd9-181">要求 (インライン イメージを含むメッセージを POST する)</span><span class="sxs-lookup"><span data-stu-id="cebd9-181">Request (POST a message with inline image)</span></span>

> [!NOTE]
> * <span data-ttu-id="cebd9-182">このシナリオでは、要求がに含まれるので、特別なアクセス許可スコープはありません `chatMessage` 。</span><span class="sxs-lookup"><span data-stu-id="cebd9-182">There are no special permission scopes in this scenario since the request is part of `chatMessage`.</span></span>
> * <span data-ttu-id="cebd9-183">対象範囲は、 `chatMessage` ここで適用されます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-183">The scopes for `chatMessage` apply here.</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

{
  "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"../hostedContents/1/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "hostedContents":[
        {
            "@microsoft.graph.temporaryId": "1",
            "contentBytes": "iVBORw0KGgoAAAANSUhEUgAAANcAAAExCAYAAADvFzeeAAAXjklEQVR4Ae2d/XNU1RnH+9e0FFrA0RCIyaS8hRA0HV5KbS1gHRgVpjMClY4GHJ3yYm1HCmXaWttaaZUZtIIFKYi8lFAkvOQ9u5vN225IARVBbX9/Os9NbrLZbMjmhCfJPX5+2Lmb3T25y3O+n/M599x7w9f+++UXwoMakIF7n4GvUdR7X1RqSk01A8CFuZm5GGUAuIwKi72wF3ABF+YyygBwGRUWc2Eu4AIuzGWUAeAyKizmwlzABVyYyygDwGVUWMyFuYALuDCXUQaAy6iwmAtzARdwfWXMdeuzT+TGxz3Sfb1LunrapL07IW3pePDQ5/qavqef0c+OdYAELuAac4jGGkLL9rdvfyo9N9ODQAqBGmmrwGlb/R0u3xG4gMspOC5hG882CoRaaCSA8n1ff9doIQMu4PIOrus3u+8ZVNnw6e/Od5AALuDKOyz5hmqiPnfnzi1J9bSbgRWCpvvQfY307wQu4BoxJCOFaDK8rwsQmQsUIQhWW93XSIsewAVckYdLQ24F0Ui/926AARdwRRounZ6Np7GyYdN9DzdFBC7gijRc43GMlQ1U9s/6HXJNjYELuHI<<-----Removed----->>>>",
            "contentType": "image/png"
        }
    ]
}
```

#### <a name="response"></a><span data-ttu-id="cebd9-184">応答</span><span class="sxs-lookup"><span data-stu-id="cebd9-184">Response</span></span>

```http
HTTP/1.1 200 OK

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
    "id": "id-value",
    "replyToId": null,
    "etag": "id-value",
    "messageType": "message",
    "createdDateTime": "2019-02-04T19:58:15.511Z",
    "lastModifiedDateTime": null,
    "deleted": false,
    "subject": null,
    "summary": null,
    "importance": "normal",
    "locale": "en-us",
    "policyViolation": null,
    "from": {
        "application": null,
        "device": null,
        "conversation": null,
        "user": {
            "id": "id-value",
            "displayName": "Joh Doe",
            "userIdentityType": "aadUser"
        }
    },
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-4-complete-migration-mode"></a><span data-ttu-id="cebd9-185">手順 4: 移行モードの完了</span><span class="sxs-lookup"><span data-stu-id="cebd9-185">Step 4: Complete migration mode</span></span>

<span data-ttu-id="cebd9-186">メッセージの移行プロセスが完了すると、チームとチャネルの両方がメソッドを使用して移行モードから取り出  `completeMigration` されます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-186">After the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration` method.</span></span> <span data-ttu-id="cebd9-187">この手順では、チーム メンバーが一般的に使用するチームリソースとチャネル リソースを開きます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-187">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="cebd9-188">アクションはインスタンスにバインド `team` されます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-188">The action is bound to the `team` instance.</span></span> <span data-ttu-id="cebd9-189">チームが完了する前に、すべてのチャネルを移行モードから完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cebd9-189">Before the team completes, all channels must be completed out of migration mode.</span></span>

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="cebd9-190">要求 (エンド チャネル移行モード)</span><span class="sxs-lookup"><span data-stu-id="cebd9-190">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a><span data-ttu-id="cebd9-191">応答</span><span class="sxs-lookup"><span data-stu-id="cebd9-191">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="cebd9-192">要求 (チーム移行モードの終了)</span><span class="sxs-lookup"><span data-stu-id="cebd9-192">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a><span data-ttu-id="cebd9-193">応答</span><span class="sxs-lookup"><span data-stu-id="cebd9-193">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

<span data-ttu-id="cebd9-194">a に対して呼び `team` 出されたアクション、 `channel` またはに含めされていないアクション `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="cebd9-194">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="cebd9-195">手順 5: チーム メンバーを追加する</span><span class="sxs-lookup"><span data-stu-id="cebd9-195">Step five: Add team members</span></span>

<span data-ttu-id="cebd9-196">メンバーをチームに追加するには、次の UI または Microsoft Teams [API](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9)をGraph[使用](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true)します。</span><span class="sxs-lookup"><span data-stu-id="cebd9-196">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="cebd9-197">要求 (メンバーの追加)</span><span class="sxs-lookup"><span data-stu-id="cebd9-197">Request (add member)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/{team-id}/members
Content-type: application/json
Content-length: 30
{
"@odata.type": "#microsoft.graph.aadUserConversationMember",
"roles": [],
"user@odata.bind": "https://graph.microsoft.com/beta/users/{user-id}"
}
```

#### <a name="response"></a><span data-ttu-id="cebd9-198">応答</span><span class="sxs-lookup"><span data-stu-id="cebd9-198">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="cebd9-199">ヒントと追加情報</span><span class="sxs-lookup"><span data-stu-id="cebd9-199">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="cebd9-200">要求が `completeMigration` 行われた後、チームにそれ以上のメッセージをインポートすることはできません。</span><span class="sxs-lookup"><span data-stu-id="cebd9-200">After the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="cebd9-201">新しいチームにチーム メンバーを追加できるのは、要求が正常に応答 `completeMigration` を返した後のみです。</span><span class="sxs-lookup"><span data-stu-id="cebd9-201">You can only add team members to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="cebd9-202">調整: チャネルごとに 5 つの RPS でメッセージがインポートされます。</span><span class="sxs-lookup"><span data-stu-id="cebd9-202">Throttling: Messages import at five RPS per channel.</span></span>

* <span data-ttu-id="cebd9-203">移行結果を修正する必要がある場合は、チームを削除し、手順を繰り返してチームとチャネルを作成し、メッセージを再移行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cebd9-203">If you need to make a correction to the migration results, you must delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="cebd9-204">現在、インライン イメージは、インポート メッセージ API スキーマでサポートされているメディアの唯一の種類です。</span><span class="sxs-lookup"><span data-stu-id="cebd9-204">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="cebd9-205">コンテンツ スコープのインポート</span><span class="sxs-lookup"><span data-stu-id="cebd9-205">Import content scope</span></span>

<span data-ttu-id="cebd9-206">次の表に、コンテンツ スコープを示します。</span><span class="sxs-lookup"><span data-stu-id="cebd9-206">The following table provides the content scope:</span></span>

|<span data-ttu-id="cebd9-207">スコープ内</span><span class="sxs-lookup"><span data-stu-id="cebd9-207">In-scope</span></span> | <span data-ttu-id="cebd9-208">現在のスコープ外</span><span class="sxs-lookup"><span data-stu-id="cebd9-208">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="cebd9-209">チームメッセージとチャネル メッセージ</span><span class="sxs-lookup"><span data-stu-id="cebd9-209">Team and channel messages</span></span>|<span data-ttu-id="cebd9-210">1:1 およびグループ チャット メッセージ</span><span class="sxs-lookup"><span data-stu-id="cebd9-210">1:1 and group chat messages</span></span>|
|<span data-ttu-id="cebd9-211">元のメッセージの作成時刻</span><span class="sxs-lookup"><span data-stu-id="cebd9-211">Created time of the original message</span></span>|<span data-ttu-id="cebd9-212">プライベート チャネル</span><span class="sxs-lookup"><span data-stu-id="cebd9-212">Private channels</span></span>|
|<span data-ttu-id="cebd9-213">メッセージの一部としてのインライン イメージ</span><span class="sxs-lookup"><span data-stu-id="cebd9-213">Inline images as part of the message</span></span>|<span data-ttu-id="cebd9-214">メンション</span><span class="sxs-lookup"><span data-stu-id="cebd9-214">At mentions</span></span>|
|<span data-ttu-id="cebd9-215">SPO または SPO の既存のファイルへのOneDrive</span><span class="sxs-lookup"><span data-stu-id="cebd9-215">Links to existing files in SPO or OneDrive</span></span>|<span data-ttu-id="cebd9-216">リアクション</span><span class="sxs-lookup"><span data-stu-id="cebd9-216">Reactions</span></span>|
|<span data-ttu-id="cebd9-217">リッチ テキストを含むメッセージ</span><span class="sxs-lookup"><span data-stu-id="cebd9-217">Messages with rich text</span></span>|<span data-ttu-id="cebd9-218">ビデオ</span><span class="sxs-lookup"><span data-stu-id="cebd9-218">Videos</span></span>|
|<span data-ttu-id="cebd9-219">メッセージ返信チェーン</span><span class="sxs-lookup"><span data-stu-id="cebd9-219">Message reply chain</span></span>|<span data-ttu-id="cebd9-220">お知らせ</span><span class="sxs-lookup"><span data-stu-id="cebd9-220">Announcements</span></span>|
|<span data-ttu-id="cebd9-221">高スループット処理</span><span class="sxs-lookup"><span data-stu-id="cebd9-221">High throughput processing</span></span>|<span data-ttu-id="cebd9-222">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="cebd9-222">Code snippets</span></span>|
||<span data-ttu-id="cebd9-223">ステッカー</span><span class="sxs-lookup"><span data-stu-id="cebd9-223">Stickers</span></span>|
||<span data-ttu-id="cebd9-224">絵文字</span><span class="sxs-lookup"><span data-stu-id="cebd9-224">Emojis</span></span>|
||<span data-ttu-id="cebd9-225">見積もり</span><span class="sxs-lookup"><span data-stu-id="cebd9-225">Quotes</span></span>|
||<span data-ttu-id="cebd9-226">チャネル間のクロス投稿</span><span class="sxs-lookup"><span data-stu-id="cebd9-226">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="cebd9-227">関連項目</span><span class="sxs-lookup"><span data-stu-id="cebd9-227">See also</span></span>

[<span data-ttu-id="cebd9-228">Microsoft GraphとTeams統合</span><span class="sxs-lookup"><span data-stu-id="cebd9-228">Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
