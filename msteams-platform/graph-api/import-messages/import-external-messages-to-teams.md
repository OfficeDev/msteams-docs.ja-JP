---
title: Microsoft Graphを使用して外部プラットフォーム メッセージをインポートTeams
description: Microsoft Graph を使用して外部プラットフォームからメッセージをインポートする方法についてTeams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 1b5a8ccc243c795801552519b4b52f51366e047d
ms.sourcegitcommit: c9446200b8e76fbd434d012dc11dd9f191776d13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/29/2021
ms.locfileid: "51403970"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="9e298-104">Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする</span><span class="sxs-lookup"><span data-stu-id="9e298-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

<span data-ttu-id="9e298-105">Microsoft Graphを使用すると、ユーザーの既存のメッセージ履歴とデータを外部システムから別のチャネルにTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="9e298-105">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="9e298-106">Teams 内のサード パーティプラットフォーム メッセージング階層のレクリエーションを有効にすると、ユーザーはシームレスな方法で通信を続行し、中断することなく続行できます。</span><span class="sxs-lookup"><span data-stu-id="9e298-106">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE] 
> <span data-ttu-id="9e298-107">今後、Microsoft は、インポートされるデータの量に基づいて、お客様またはお客様の顧客に追加料金の支払いを要求する場合があります。</span><span class="sxs-lookup"><span data-stu-id="9e298-107">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="9e298-108">インポートの概要</span><span class="sxs-lookup"><span data-stu-id="9e298-108">Import overview</span></span>

<span data-ttu-id="9e298-109">高レベルでは、インポート プロセスは次で構成されます。</span><span class="sxs-lookup"><span data-stu-id="9e298-109">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="9e298-110">タイム スタンプを使用してチームを作成する</span><span class="sxs-lookup"><span data-stu-id="9e298-110">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="9e298-111">タイム スタンプを使用してチャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="9e298-111">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="9e298-112">外部のバックインタイム日付メッセージのインポート</span><span class="sxs-lookup"><span data-stu-id="9e298-112">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="9e298-113">チームとチャネルの移行プロセスを完了する</span><span class="sxs-lookup"><span data-stu-id="9e298-113">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="9e298-114">チーム メンバーの追加</span><span class="sxs-lookup"><span data-stu-id="9e298-114">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="9e298-115">必要な要件</span><span class="sxs-lookup"><span data-stu-id="9e298-115">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="9e298-116">メッセージ データの分析と準備</span><span class="sxs-lookup"><span data-stu-id="9e298-116">Analyze and prepare message data</span></span>

<span data-ttu-id="9e298-117">✔サード パーティのデータを確認して、移行するデータを決定します。</span><span class="sxs-lookup"><span data-stu-id="9e298-117">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="9e298-118">✔サード パーティチャット システムから選択したデータを抽出します。</span><span class="sxs-lookup"><span data-stu-id="9e298-118">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="9e298-119">✔サード パーティのチャット構造を、他のユーザーのチャット構造Teamsします。</span><span class="sxs-lookup"><span data-stu-id="9e298-119">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="9e298-120">✔移行に必要な形式にインポート データを変換します。</span><span class="sxs-lookup"><span data-stu-id="9e298-120">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="9e298-121">Office 365 テナントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="9e298-121">Set up your Office 365 tenant</span></span>

<span data-ttu-id="9e298-122">✔インポート データOffice 365テナントが存在することを確認します。</span><span class="sxs-lookup"><span data-stu-id="9e298-122">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="9e298-123">ユーザーのテナントを設定する方法Office 365については、「Teamsテナントを準備する」[をOffice 365してください](../../concepts/build-and-test/prepare-your-o365-tenant.md)。 </span><span class="sxs-lookup"><span data-stu-id="9e298-123">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="9e298-124">✔チーム メンバーが (AAD) にAzure Active Directory確認します。</span><span class="sxs-lookup"><span data-stu-id="9e298-124">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="9e298-125">詳細については、「新 *しい*[ユーザーを新しいユーザーに追加する](/azure/active-directory/fundamentals/add-users-azure-active-directory)」を参照Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="9e298-125">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="9e298-126">手順 1: チームを作成する</span><span class="sxs-lookup"><span data-stu-id="9e298-126">Step One: Create a team</span></span>

<span data-ttu-id="9e298-127">既存のデータは移行中ですから、元のメッセージ タイムスタンプを維持し、移行プロセス中のメッセージング アクティビティを防止する方法は、Teams でユーザーの既存のメッセージ フローを再作成する際に重要です。</span><span class="sxs-lookup"><span data-stu-id="9e298-127">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="9e298-128">これは、次のように実現されます。</span><span class="sxs-lookup"><span data-stu-id="9e298-128">This is achieved as follows:</span></span>

> <span data-ttu-id="9e298-129">[チーム リソース プロパティを使用して](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) 、タイム スタンプを使用して新しいチームを作成  `createdDateTime`  します。</span><span class="sxs-lookup"><span data-stu-id="9e298-129">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="9e298-130">移行プロセスが完了するまで、チーム内のほとんどのアクティビティからユーザーをバーする特別な状態で、新しいチーム `migration mode` を配置します。</span><span class="sxs-lookup"><span data-stu-id="9e298-130">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="9e298-131">新しいチームが移行用に作成されているとして明示的に識別するには、POST 要求に値を持つ `teamCreationMode` `migration` instance 属性を含める。</span><span class="sxs-lookup"><span data-stu-id="9e298-131">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="9e298-132">**注**: このフィールドは、移行されたチームまたはチャネルのインスタンス `createdDateTime` に対してのみ設定されます。</span><span class="sxs-lookup"><span data-stu-id="9e298-132">**NOTE**:  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="9e298-133">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="9e298-133">Permissions</span></span>

|<span data-ttu-id="9e298-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="9e298-134">ScopeName</span></span>|<span data-ttu-id="9e298-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="9e298-135">DisplayName</span></span>|<span data-ttu-id="9e298-136">説明</span><span class="sxs-lookup"><span data-stu-id="9e298-136">Description</span></span>|<span data-ttu-id="9e298-137">型</span><span class="sxs-lookup"><span data-stu-id="9e298-137">Type</span></span>|<span data-ttu-id="9e298-138">管理者の同意</span><span class="sxs-lookup"><span data-stu-id="9e298-138">Admin Consent?</span></span>|<span data-ttu-id="9e298-139">対象のエンティティ/API</span><span class="sxs-lookup"><span data-stu-id="9e298-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="9e298-140">Microsoft Teams への移行の管理</span><span class="sxs-lookup"><span data-stu-id="9e298-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="9e298-141">ユーザーへの移行用のリソースの作成、管理Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9e298-141">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="9e298-142">**アプリケーション専用**</span><span class="sxs-lookup"><span data-stu-id="9e298-142">**Application-only**</span></span>|<span data-ttu-id="9e298-143">**はい**</span><span class="sxs-lookup"><span data-stu-id="9e298-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="9e298-144">要求 (移行状態でチームを作成する)</span><span class="sxs-lookup"><span data-stu-id="9e298-144">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="9e298-145">応答</span><span class="sxs-lookup"><span data-stu-id="9e298-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-messages"></a><span data-ttu-id="9e298-146">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="9e298-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="9e298-147">`createdDateTime`  将来に向け設定されます。</span><span class="sxs-lookup"><span data-stu-id="9e298-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="9e298-148">`createdDateTime`  正しく指定されますが `teamCreationMode`  、インスタンス属性が見つからないか、無効な値に設定されています。</span><span class="sxs-lookup"><span data-stu-id="9e298-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="9e298-149">手順 2: チャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="9e298-149">Step Two: Create a channel</span></span>

<span data-ttu-id="9e298-150">インポートされたメッセージのチャネルの作成は、チームの作成シナリオに似ています。</span><span class="sxs-lookup"><span data-stu-id="9e298-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="9e298-151">[チャネル リソース プロパティを使用](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) して、タイム スタンプをバックインする新しいチャネルを作成 `createdDateTime` します。</span><span class="sxs-lookup"><span data-stu-id="9e298-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="9e298-152">移行プロセスが完了するまで、チャネル内のほとんどのチャット アクティビティからユーザーをバーする特別な状態で、新しいチャネル `migration mode` を配置します。</span><span class="sxs-lookup"><span data-stu-id="9e298-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="9e298-153">新しいチームが移行用に作成されているとして明示的に識別するには、POST 要求に値を持つ `channelCreationMode` `migration` instance 属性を含める。</span><span class="sxs-lookup"><span data-stu-id="9e298-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="9e298-154">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="9e298-154">Permissions</span></span>

|<span data-ttu-id="9e298-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="9e298-155">ScopeName</span></span>|<span data-ttu-id="9e298-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="9e298-156">DisplayName</span></span>|<span data-ttu-id="9e298-157">説明</span><span class="sxs-lookup"><span data-stu-id="9e298-157">Description</span></span>|<span data-ttu-id="9e298-158">型</span><span class="sxs-lookup"><span data-stu-id="9e298-158">Type</span></span>|<span data-ttu-id="9e298-159">管理者の同意</span><span class="sxs-lookup"><span data-stu-id="9e298-159">Admin Consent?</span></span>|<span data-ttu-id="9e298-160">対象のエンティティ/API</span><span class="sxs-lookup"><span data-stu-id="9e298-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="9e298-161">Microsoft Teams への移行の管理</span><span class="sxs-lookup"><span data-stu-id="9e298-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="9e298-162">ユーザーへの移行用のリソースの作成、管理Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9e298-162">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="9e298-163">**アプリケーション専用**</span><span class="sxs-lookup"><span data-stu-id="9e298-163">**Application-only**</span></span>|<span data-ttu-id="9e298-164">**はい**</span><span class="sxs-lookup"><span data-stu-id="9e298-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="9e298-165">要求 (移行状態でチャネルを作成する)</span><span class="sxs-lookup"><span data-stu-id="9e298-165">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="9e298-166">応答</span><span class="sxs-lookup"><span data-stu-id="9e298-166">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="9e298-167">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="9e298-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="9e298-168">`createdDateTime`  将来に向け設定されます。</span><span class="sxs-lookup"><span data-stu-id="9e298-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="9e298-169">`createdDateTime`  正しく指定されますが `channelCreationMode`  、インスタンス属性が見つからないか、無効な値に設定されています。</span><span class="sxs-lookup"><span data-stu-id="9e298-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="9e298-170">手順 3: メッセージのインポート</span><span class="sxs-lookup"><span data-stu-id="9e298-170">Step Three: Import messages</span></span>

<span data-ttu-id="9e298-171">チームとチャネルを作成したら、要求本文のキーとキーを使用して、バックインタイム メッセージ `createdDateTime` `from`  の送信を開始できます。</span><span class="sxs-lookup"><span data-stu-id="9e298-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="9e298-172">**注**: メッセージ スレッドより前 `createdDateTime` にインポートされたメッセージ `createdDateTime` はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="9e298-172">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="9e298-173">`createdDateTime` 同じスレッド内のメッセージ間で一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="9e298-173">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="9e298-174">`createdDateTime` ミリ秒単位の精度のタイムスタンプをサポートします。</span><span class="sxs-lookup"><span data-stu-id="9e298-174">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="9e298-175">たとえば、受信要求メッセージの値が `createdDateTime` *2020-09-16T05:50:31.0025302Z* の場合、メッセージが取り込まれたときに *2020-09-16T05:50:31.002Z* に変換されます。</span><span class="sxs-lookup"><span data-stu-id="9e298-175">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="9e298-176">要求 (テキスト専用の POST メッセージ)</span><span class="sxs-lookup"><span data-stu-id="9e298-176">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="9e298-177">応答</span><span class="sxs-lookup"><span data-stu-id="9e298-177">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="9e298-178">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="9e298-178">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="9e298-179">要求 (インライン イメージを含むメッセージを POST する)</span><span class="sxs-lookup"><span data-stu-id="9e298-179">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="9e298-180">**注**: 要求は chatMessage の一部のため、このシナリオには特別なアクセス許可スコープはありません。chatMessage のスコープもここに適用されます。</span><span class="sxs-lookup"><span data-stu-id="9e298-180">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="9e298-181">応答</span><span class="sxs-lookup"><span data-stu-id="9e298-181">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="9e298-182">手順 4: 移行モードの完了</span><span class="sxs-lookup"><span data-stu-id="9e298-182">Step Four: Complete migration mode</span></span>

<span data-ttu-id="9e298-183">メッセージの移行プロセスが完了すると、チームとチャネルの両方がメソッドを使用して移行モードから取り出  `completeMigration`  されます。</span><span class="sxs-lookup"><span data-stu-id="9e298-183">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="9e298-184">この手順では、チーム メンバーが一般的に使用するチームリソースとチャネル リソースを開きます。</span><span class="sxs-lookup"><span data-stu-id="9e298-184">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="9e298-185">アクションはインスタンスにバインド `team` されます。</span><span class="sxs-lookup"><span data-stu-id="9e298-185">The action is bound to the `team` instance.</span></span> <span data-ttu-id="9e298-186">チームを完了するには、移行モードからすべてのチャネルを完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9e298-186">All channels must be completed out of migration mode before the team can be completed.</span></span>

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="9e298-187">要求 (エンド チャネル移行モード)</span><span class="sxs-lookup"><span data-stu-id="9e298-187">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a><span data-ttu-id="9e298-188">応答</span><span class="sxs-lookup"><span data-stu-id="9e298-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="9e298-189">要求 (チーム移行モードの終了)</span><span class="sxs-lookup"><span data-stu-id="9e298-189">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a><span data-ttu-id="9e298-190">応答</span><span class="sxs-lookup"><span data-stu-id="9e298-190">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

* <span data-ttu-id="9e298-191">a に対して呼び `team` 出されたアクション、 `channel` またはに含めされていないアクション `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="9e298-191">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="9e298-192">手順 5: チーム メンバーを追加する</span><span class="sxs-lookup"><span data-stu-id="9e298-192">Step Five: Add team members</span></span>

<span data-ttu-id="9e298-193">メンバーをチームに追加するには、次の UI または Microsoft Teams[メンバー API](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9)をGraph[使用](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true)します。</span><span class="sxs-lookup"><span data-stu-id="9e298-193">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="9e298-194">要求 (メンバーの追加)</span><span class="sxs-lookup"><span data-stu-id="9e298-194">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="9e298-195">応答</span><span class="sxs-lookup"><span data-stu-id="9e298-195">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="9e298-196">ヒントと追加情報</span><span class="sxs-lookup"><span data-stu-id="9e298-196">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="9e298-197">要求が `completeMigration` 行われたら、チームに追加のメッセージをインポートすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9e298-197">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="9e298-198">チーム メンバーは、要求が正常に応答を返した後にのみ、新 `completeMigration` しいチームに追加できます。</span><span class="sxs-lookup"><span data-stu-id="9e298-198">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="9e298-199">調整: チャネルごとに 5 RPS でメッセージがインポートされます。</span><span class="sxs-lookup"><span data-stu-id="9e298-199">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="9e298-200">移行結果を修正する必要がある場合は、チームを削除し、手順を繰り返してチームとチャネルを作成し、メッセージを再移行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9e298-200">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="9e298-201">現在、インライン イメージは、インポート メッセージ API スキーマでサポートされているメディアの唯一の種類です。</span><span class="sxs-lookup"><span data-stu-id="9e298-201">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="9e298-202">コンテンツ スコープのインポート</span><span class="sxs-lookup"><span data-stu-id="9e298-202">Import content scope</span></span>

|<span data-ttu-id="9e298-203">スコープ内</span><span class="sxs-lookup"><span data-stu-id="9e298-203">In-scope</span></span> | <span data-ttu-id="9e298-204">現在のスコープ外</span><span class="sxs-lookup"><span data-stu-id="9e298-204">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="9e298-205">チームメッセージとチャネル メッセージ</span><span class="sxs-lookup"><span data-stu-id="9e298-205">Team and channel messages</span></span>|<span data-ttu-id="9e298-206">1:1 およびグループ チャット メッセージ</span><span class="sxs-lookup"><span data-stu-id="9e298-206">1:1 and group chat messages</span></span>|
|<span data-ttu-id="9e298-207">元のメッセージの作成時刻</span><span class="sxs-lookup"><span data-stu-id="9e298-207">Created time of the original message</span></span>|<span data-ttu-id="9e298-208">プライベート チャネル</span><span class="sxs-lookup"><span data-stu-id="9e298-208">Private channels</span></span>|
|<span data-ttu-id="9e298-209">メッセージの一部としてのインライン イメージ</span><span class="sxs-lookup"><span data-stu-id="9e298-209">Inline images as part of the message</span></span>|<span data-ttu-id="9e298-210">メンション</span><span class="sxs-lookup"><span data-stu-id="9e298-210">At mentions</span></span>|
|<span data-ttu-id="9e298-211">SPO/OneDrive の既存のファイルへのOneDrive</span><span class="sxs-lookup"><span data-stu-id="9e298-211">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="9e298-212">リアクション</span><span class="sxs-lookup"><span data-stu-id="9e298-212">Reactions</span></span>|
|<span data-ttu-id="9e298-213">リッチ テキストを含むメッセージ</span><span class="sxs-lookup"><span data-stu-id="9e298-213">Messages with rich text</span></span>|<span data-ttu-id="9e298-214">ビデオ</span><span class="sxs-lookup"><span data-stu-id="9e298-214">Videos</span></span>|
|<span data-ttu-id="9e298-215">メッセージ返信チェーン</span><span class="sxs-lookup"><span data-stu-id="9e298-215">Message reply chain</span></span>|<span data-ttu-id="9e298-216">お知らせ</span><span class="sxs-lookup"><span data-stu-id="9e298-216">Announcements</span></span>|
|<span data-ttu-id="9e298-217">高スループット処理</span><span class="sxs-lookup"><span data-stu-id="9e298-217">High throughput processing</span></span>|<span data-ttu-id="9e298-218">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="9e298-218">Code snippets</span></span>|
||<span data-ttu-id="9e298-219">ステッカー</span><span class="sxs-lookup"><span data-stu-id="9e298-219">Stickers</span></span>|
||<span data-ttu-id="9e298-220">絵文字</span><span class="sxs-lookup"><span data-stu-id="9e298-220">Emojis</span></span>|
||<span data-ttu-id="9e298-221">引用符</span><span class="sxs-lookup"><span data-stu-id="9e298-221">Quotes</span></span>|
||<span data-ttu-id="9e298-222">チャネル間のクロス投稿</span><span class="sxs-lookup"><span data-stu-id="9e298-222">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="9e298-223">関連項目</span><span class="sxs-lookup"><span data-stu-id="9e298-223">See also</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9e298-224">Microsoft GraphとTeams詳細</span><span class="sxs-lookup"><span data-stu-id="9e298-224">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
