---
title: Microsoft Graphを使用して外部プラットフォーム メッセージをTeamsにインポートする
description: Microsoft Graphを使用して外部プラットフォームからTeamsにメッセージをインポートする方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: チームインポートメッセージ API グラフ マイクロソフト移行の投稿
ms.openlocfilehash: 5ea06e8b490bae0595abb31086848d0b050bded0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566160"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="ea359-104">Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする</span><span class="sxs-lookup"><span data-stu-id="ea359-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

<span data-ttu-id="ea359-105">Microsoft Graphでは、ユーザーの既存のメッセージ履歴とデータを外部システムからTeamsチャネルに移行できます。</span><span class="sxs-lookup"><span data-stu-id="ea359-105">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="ea359-106">Teams内のサードパーティのプラットフォームメッセージング階層の再作成を可能にすることで、ユーザーはシームレスな方法で通信を継続し、中断することなく続行できます。</span><span class="sxs-lookup"><span data-stu-id="ea359-106">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE] 
> <span data-ttu-id="ea359-107">今後、Microsoft は、インポートされるデータの量に基づいて、お客様またはお客様の顧客に追加料金の支払いを要求する場合があります。</span><span class="sxs-lookup"><span data-stu-id="ea359-107">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="ea359-108">インポートの概要</span><span class="sxs-lookup"><span data-stu-id="ea359-108">Import overview</span></span>

<span data-ttu-id="ea359-109">大まかに言えば、インポートプロセスは次の要素で構成されます。</span><span class="sxs-lookup"><span data-stu-id="ea359-109">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="ea359-110">バックインタイムタイムスタンプを持つチームを作成する</span><span class="sxs-lookup"><span data-stu-id="ea359-110">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="ea359-111">バックインタイムタイムスタンプを使用してチャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="ea359-111">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel) 
1. [<span data-ttu-id="ea359-112">外部バックインタイムの日付付きメッセージをインポートする</span><span class="sxs-lookup"><span data-stu-id="ea359-112">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="ea359-113">チームとチャネルの移行プロセスを完了する</span><span class="sxs-lookup"><span data-stu-id="ea359-113">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="ea359-114">チーム メンバーの追加</span><span class="sxs-lookup"><span data-stu-id="ea359-114">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="ea359-115">必要な要件</span><span class="sxs-lookup"><span data-stu-id="ea359-115">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="ea359-116">メッセージ データの分析と準備</span><span class="sxs-lookup"><span data-stu-id="ea359-116">Analyze and prepare message data</span></span>

<span data-ttu-id="ea359-117">✔ サード パーティのデータを確認して、移行する内容を決定します。</span><span class="sxs-lookup"><span data-stu-id="ea359-117">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="ea359-118">✔ 選択したデータをサードパーティのチャット システムから抽出します。</span><span class="sxs-lookup"><span data-stu-id="ea359-118">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="ea359-119">✔ サードパーティのチャット構造をTeams構造にマップします。</span><span class="sxs-lookup"><span data-stu-id="ea359-119">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="ea359-120">✔ インポート データを移行に必要な形式に変換します。</span><span class="sxs-lookup"><span data-stu-id="ea359-120">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="ea359-121">Office 365 テナントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="ea359-121">Set up your Office 365 tenant</span></span>

<span data-ttu-id="ea359-122">✔ インポート データのOffice 365テナントが存在することを確認します。</span><span class="sxs-lookup"><span data-stu-id="ea359-122">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="ea359-123">Teams用のOffice 365テナントの設定の詳細については[、「Office 365 テナントの準備](../../concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea359-123">For more information on setting up an Office 365 tenancy for Teams, see [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="ea359-124">✔ チーム メンバーが Azure Active Directory (AAD) に所属していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ea359-124">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="ea359-125">詳細については[、「Azure Active Directoryに新しいユーザーを追加](/azure/active-directory/fundamentals/add-users-azure-active-directory)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea359-125">For more information, see [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="ea359-126">ステップ 1: チームを作成する</span><span class="sxs-lookup"><span data-stu-id="ea359-126">Step One: Create a team</span></span>

<span data-ttu-id="ea359-127">既存のデータが移行されるため、移行プロセス中に元のメッセージ・タイム・スタンプを維持し、メッセージング・アクティビティーを防止することが、Teamsでユーザーの既存のメッセージ・フローを再作成する鍵となります。</span><span class="sxs-lookup"><span data-stu-id="ea359-127">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="ea359-128">これは、次のように行われます。</span><span class="sxs-lookup"><span data-stu-id="ea359-128">This is achieved as follows:</span></span>

> <span data-ttu-id="ea359-129">チーム リソース プロパティを使用して、バックイン タイム タイムスタンプを使用して[新しい](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true)チームを作成 `createdDateTime` します。</span><span class="sxs-lookup"><span data-stu-id="ea359-129">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="ea359-130">新しいチームを `migration mode` に配置し、移行プロセスが完了するまで、チーム内のほとんどのアクティビティからユーザーを禁止する特別な状態にします。</span><span class="sxs-lookup"><span data-stu-id="ea359-130">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="ea359-131">POST `teamCreationMode` 要求に値を持つインスタンス属性を含めて `migration` 、新しいチームを移行用に作成するチームとして明示的に識別します。</span><span class="sxs-lookup"><span data-stu-id="ea359-131">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> [!Note]
> <span data-ttu-id="ea359-132">この `createdDateTime` フィールドは、移行されたチームまたはチャネルのインスタンスに対してのみ設定されます。</span><span class="sxs-lookup"><span data-stu-id="ea359-132">The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="ea359-133">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="ea359-133">Permissions</span></span>

|<span data-ttu-id="ea359-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="ea359-134">ScopeName</span></span>|<span data-ttu-id="ea359-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="ea359-135">DisplayName</span></span>|<span data-ttu-id="ea359-136">説明</span><span class="sxs-lookup"><span data-stu-id="ea359-136">Description</span></span>|<span data-ttu-id="ea359-137">型</span><span class="sxs-lookup"><span data-stu-id="ea359-137">Type</span></span>|<span data-ttu-id="ea359-138">管理者の同意?</span><span class="sxs-lookup"><span data-stu-id="ea359-138">Admin Consent?</span></span>|<span data-ttu-id="ea359-139">対象となるエンティティ/API</span><span class="sxs-lookup"><span data-stu-id="ea359-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="ea359-140">Microsoft Teams への移行の管理</span><span class="sxs-lookup"><span data-stu-id="ea359-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="ea359-141">Microsoft Teamsへの移行用リソースの作成、管理。</span><span class="sxs-lookup"><span data-stu-id="ea359-141">Creating, managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="ea359-142">**アプリケーションのみ**</span><span class="sxs-lookup"><span data-stu-id="ea359-142">**Application-only**</span></span>|<span data-ttu-id="ea359-143">**はい**</span><span class="sxs-lookup"><span data-stu-id="ea359-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="ea359-144">リクエスト (移行状態でチームを作成する)</span><span class="sxs-lookup"><span data-stu-id="ea359-144">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="ea359-145">応答</span><span class="sxs-lookup"><span data-stu-id="ea359-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-messages"></a><span data-ttu-id="ea359-146">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="ea359-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="ea359-147">`createdDateTime`  将来に向けて設定します。</span><span class="sxs-lookup"><span data-stu-id="ea359-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="ea359-148">`createdDateTime`  正しく指定されていますが、 `teamCreationMode`  インスタンス属性が見つからないか、無効な値に設定されています。</span><span class="sxs-lookup"><span data-stu-id="ea359-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="ea359-149">ステップ 2: チャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="ea359-149">Step Two: Create a channel</span></span>

<span data-ttu-id="ea359-150">インポートされたメッセージのチャネルの作成は、チーム作成シナリオと似ています。</span><span class="sxs-lookup"><span data-stu-id="ea359-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="ea359-151">チャネル リソース プロパティを使用して、バックイン タイム タイムスタンプを使用して[新しい](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true)チャネルを作成 `createdDateTime` します。</span><span class="sxs-lookup"><span data-stu-id="ea359-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="ea359-152">新しいチャネルを `migration mode` に配置する特別な状態では、移行プロセスが完了するまで、チャネル内のほとんどのチャット アクティビティからユーザーを表示します。</span><span class="sxs-lookup"><span data-stu-id="ea359-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="ea359-153">POST `channelCreationMode` 要求に値を持つインスタンス属性を含めて `migration` 、新しいチームを移行用に作成するチームとして明示的に識別します。</span><span class="sxs-lookup"><span data-stu-id="ea359-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="ea359-154">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="ea359-154">Permissions</span></span>

|<span data-ttu-id="ea359-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="ea359-155">ScopeName</span></span>|<span data-ttu-id="ea359-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="ea359-156">DisplayName</span></span>|<span data-ttu-id="ea359-157">説明</span><span class="sxs-lookup"><span data-stu-id="ea359-157">Description</span></span>|<span data-ttu-id="ea359-158">型</span><span class="sxs-lookup"><span data-stu-id="ea359-158">Type</span></span>|<span data-ttu-id="ea359-159">管理者の同意?</span><span class="sxs-lookup"><span data-stu-id="ea359-159">Admin Consent?</span></span>|<span data-ttu-id="ea359-160">対象となるエンティティ/API</span><span class="sxs-lookup"><span data-stu-id="ea359-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="ea359-161">Microsoft Teams への移行の管理</span><span class="sxs-lookup"><span data-stu-id="ea359-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="ea359-162">Microsoft Teamsへの移行用リソースの作成、管理。</span><span class="sxs-lookup"><span data-stu-id="ea359-162">Creating, managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="ea359-163">**アプリケーションのみ**</span><span class="sxs-lookup"><span data-stu-id="ea359-163">**Application-only**</span></span>|<span data-ttu-id="ea359-164">**はい**</span><span class="sxs-lookup"><span data-stu-id="ea359-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="ea359-165">要求 (移行状態でチャネルを作成する)</span><span class="sxs-lookup"><span data-stu-id="ea359-165">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="ea359-166">応答</span><span class="sxs-lookup"><span data-stu-id="ea359-166">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="ea359-167">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="ea359-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="ea359-168">`createdDateTime`  将来に向けて設定します。</span><span class="sxs-lookup"><span data-stu-id="ea359-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="ea359-169">`createdDateTime`  正しく指定されていますが `channelCreationMode`  、インスタンス属性が欠落しているか、無効な値に設定されています。</span><span class="sxs-lookup"><span data-stu-id="ea359-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="ea359-170">手順 3: メッセージをインポートする</span><span class="sxs-lookup"><span data-stu-id="ea359-170">Step Three: Import messages</span></span>

<span data-ttu-id="ea359-171">チームとチャネルを作成した後、要求本文の キーと キーを使用して、バックインタイム メッセージの送信を開始できます `createdDateTime` `from`  。</span><span class="sxs-lookup"><span data-stu-id="ea359-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="ea359-172">**メモ**: メッセージ `createdDateTime` スレッドより前のバージョンでインポートされたメッセージ `createdDateTime` はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="ea359-172">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="ea359-173">`createdDateTime` 同じスレッド内のメッセージ間で一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea359-173">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="ea359-174">`createdDateTime` はミリ秒精度のタイムスタンプをサポートします。</span><span class="sxs-lookup"><span data-stu-id="ea359-174">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="ea359-175">たとえば、着信要求メッセージの値が `createdDateTime` *2020-09-16T05:50:31.0025302Z* に設定されている場合、メッセージの取り込み時に *2020-09-16T05:50:31.002Z* に変換されます。</span><span class="sxs-lookup"><span data-stu-id="ea359-175">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="ea359-176">要求 (テキストのみである POST メッセージ)</span><span class="sxs-lookup"><span data-stu-id="ea359-176">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="ea359-177">応答</span><span class="sxs-lookup"><span data-stu-id="ea359-177">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="ea359-178">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="ea359-178">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="ea359-179">要求 (インライン 画像を含むメッセージを POST)</span><span class="sxs-lookup"><span data-stu-id="ea359-179">Request (POST a message with inline image)</span></span>

> [!Note]
> <span data-ttu-id="ea359-180">要求は chatMessage の一部であるため、このシナリオには特別なアクセス許可スコープはありません。チャットメッセージのスコープもここに適用されます。</span><span class="sxs-lookup"><span data-stu-id="ea359-180">There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="ea359-181">応答</span><span class="sxs-lookup"><span data-stu-id="ea359-181">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="ea359-182">ステップ 4: 移行モードを完了する</span><span class="sxs-lookup"><span data-stu-id="ea359-182">Step Four: Complete migration mode</span></span>

<span data-ttu-id="ea359-183">メッセージの移行プロセスが完了すると、チームとチャネルの両方が、このメソッドを使用して移行モードから除外されます  `completeMigration`  。</span><span class="sxs-lookup"><span data-stu-id="ea359-183">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="ea359-184">この手順では、チーム メンバーが一般的に使用するチームリソースとチャネル リソースを開きます。</span><span class="sxs-lookup"><span data-stu-id="ea359-184">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="ea359-185">アクションはインスタンスにバインドされます `team` 。</span><span class="sxs-lookup"><span data-stu-id="ea359-185">The action is bound to the `team` instance.</span></span> <span data-ttu-id="ea359-186">チームを完了するには、すべてのチャネルを移行モードから終了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea359-186">All channels must be completed out of migration mode before the team can be completed.</span></span>

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="ea359-187">要求 (エンド チャネル移行モード)</span><span class="sxs-lookup"><span data-stu-id="ea359-187">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a><span data-ttu-id="ea359-188">応答</span><span class="sxs-lookup"><span data-stu-id="ea359-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="ea359-189">要求 (エンド チーム移行モード)</span><span class="sxs-lookup"><span data-stu-id="ea359-189">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a><span data-ttu-id="ea359-190">応答</span><span class="sxs-lookup"><span data-stu-id="ea359-190">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

* <span data-ttu-id="ea359-191">にはない 、 に対して呼び出 `team` `channel` されるアクション `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="ea359-191">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="ea359-192">ステップ 5: チーム メンバーを追加する</span><span class="sxs-lookup"><span data-stu-id="ea359-192">Step Five: Add team members</span></span>

<span data-ttu-id="ea359-193">Teams UI または Microsoft の [メンバーの追加] API[を使用して](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9)、[チームにメンバー](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) Graph追加できます。</span><span class="sxs-lookup"><span data-stu-id="ea359-193">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="ea359-194">要求 (メンバーの追加)</span><span class="sxs-lookup"><span data-stu-id="ea359-194">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="ea359-195">応答</span><span class="sxs-lookup"><span data-stu-id="ea359-195">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="ea359-196">ヒントと追加情報</span><span class="sxs-lookup"><span data-stu-id="ea359-196">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="ea359-197">要求が `completeMigration` 完了すると、チームにメッセージをインポートすることはできません。</span><span class="sxs-lookup"><span data-stu-id="ea359-197">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="ea359-198">チーム メンバーは、要求が正常な応答を返した後にのみ新しいチームに追加できます `completeMigration` 。</span><span class="sxs-lookup"><span data-stu-id="ea359-198">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="ea359-199">スロットル: チャネルあたり 5 RPS でメッセージをインポートします。</span><span class="sxs-lookup"><span data-stu-id="ea359-199">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="ea359-200">移行結果を修正する必要がある場合は、チームを削除し、チームとチャネルを作成し、メッセージを再移行する手順を繰り返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea359-200">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="ea359-201">現在、インライン イメージは、インポート メッセージ API スキーマでサポートされるメディアの唯一の種類です。</span><span class="sxs-lookup"><span data-stu-id="ea359-201">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="ea359-202">コンテンツの範囲をインポートする</span><span class="sxs-lookup"><span data-stu-id="ea359-202">Import content scope</span></span>

|<span data-ttu-id="ea359-203">スコープ内</span><span class="sxs-lookup"><span data-stu-id="ea359-203">In-scope</span></span> | <span data-ttu-id="ea359-204">現在範囲外</span><span class="sxs-lookup"><span data-stu-id="ea359-204">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="ea359-205">チームおよびチャネルメッセージ</span><span class="sxs-lookup"><span data-stu-id="ea359-205">Team and channel messages</span></span>|<span data-ttu-id="ea359-206">1:1 とグループ チャット メッセージ</span><span class="sxs-lookup"><span data-stu-id="ea359-206">1:1 and group chat messages</span></span>|
|<span data-ttu-id="ea359-207">元のメッセージの作成時刻</span><span class="sxs-lookup"><span data-stu-id="ea359-207">Created time of the original message</span></span>|<span data-ttu-id="ea359-208">プライベート チャネル</span><span class="sxs-lookup"><span data-stu-id="ea359-208">Private channels</span></span>|
|<span data-ttu-id="ea359-209">メッセージの一部としてのインライン 画像</span><span class="sxs-lookup"><span data-stu-id="ea359-209">Inline images as part of the message</span></span>|<span data-ttu-id="ea359-210">言及時</span><span class="sxs-lookup"><span data-stu-id="ea359-210">At mentions</span></span>|
|<span data-ttu-id="ea359-211">SPO/OneDrive内の既存のファイルへのリンク</span><span class="sxs-lookup"><span data-stu-id="ea359-211">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="ea359-212">反応</span><span class="sxs-lookup"><span data-stu-id="ea359-212">Reactions</span></span>|
|<span data-ttu-id="ea359-213">リッチ テキストを含むメッセージ</span><span class="sxs-lookup"><span data-stu-id="ea359-213">Messages with rich text</span></span>|<span data-ttu-id="ea359-214">ビデオ</span><span class="sxs-lookup"><span data-stu-id="ea359-214">Videos</span></span>|
|<span data-ttu-id="ea359-215">メッセージ応答チェーン</span><span class="sxs-lookup"><span data-stu-id="ea359-215">Message reply chain</span></span>|<span data-ttu-id="ea359-216">お知らせ</span><span class="sxs-lookup"><span data-stu-id="ea359-216">Announcements</span></span>|
|<span data-ttu-id="ea359-217">高スループット処理</span><span class="sxs-lookup"><span data-stu-id="ea359-217">High throughput processing</span></span>|<span data-ttu-id="ea359-218">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="ea359-218">Code snippets</span></span>|
||<span data-ttu-id="ea359-219">ステッカー</span><span class="sxs-lookup"><span data-stu-id="ea359-219">Stickers</span></span>|
||<span data-ttu-id="ea359-220">絵文字</span><span class="sxs-lookup"><span data-stu-id="ea359-220">Emojis</span></span>|
||<span data-ttu-id="ea359-221">引用符</span><span class="sxs-lookup"><span data-stu-id="ea359-221">Quotes</span></span>|
||<span data-ttu-id="ea359-222">チャネル間のクロスポスト</span><span class="sxs-lookup"><span data-stu-id="ea359-222">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="ea359-223">関連項目</span><span class="sxs-lookup"><span data-stu-id="ea359-223">See also</span></span>

[<span data-ttu-id="ea359-224">マイクロソフトのGraphとTeams統合の詳細</span><span class="sxs-lookup"><span data-stu-id="ea359-224">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
