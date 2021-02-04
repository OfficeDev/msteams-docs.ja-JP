---
title: Microsoft Graph を使用して外部プラットフォーム メッセージを Teams にインポートする
description: Microsoft Graph を使用して外部プラットフォームから Teams にメッセージをインポートする方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 97f24c34ebb825aad0fd104c9a814e46f9b5fa0d
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093261"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="9af13-104">Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする</span><span class="sxs-lookup"><span data-stu-id="9af13-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="9af13-105">Microsoft Graph と Microsoft Teams のパブリック プレビューは、早期アクセスとフィードバックに利用できます。</span><span class="sxs-lookup"><span data-stu-id="9af13-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="9af13-106">このリリースでは広範なテストが実施されましたが、実稼働環境での使用を意図した方法ではありません。</span><span class="sxs-lookup"><span data-stu-id="9af13-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="9af13-107">Microsoft Graph を使用すると、ユーザーの既存のメッセージ履歴とデータを外部システムから Teams チャネルに移行できます。</span><span class="sxs-lookup"><span data-stu-id="9af13-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="9af13-108">Teams 内でサード パーティ製プラットフォームのメッセージング階層を作成することで、ユーザーはシームレスな方法で通信を続行し、中断することなく続行できます。</span><span class="sxs-lookup"><span data-stu-id="9af13-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="9af13-109">インポートの概要</span><span class="sxs-lookup"><span data-stu-id="9af13-109">Import overview</span></span>

<span data-ttu-id="9af13-110">大きなレベルでは、インポート プロセスは次の要素で構成されます。</span><span class="sxs-lookup"><span data-stu-id="9af13-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="9af13-111">バックインタイム タイムスタンプを使用してチームを作成する</span><span class="sxs-lookup"><span data-stu-id="9af13-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="9af13-112">バックインタイム タイムスタンプを使用してチャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="9af13-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="9af13-113">外部のバックインタイム日付メッセージをインポートする</span><span class="sxs-lookup"><span data-stu-id="9af13-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="9af13-114">チームとチャネルの移行プロセスを完了する</span><span class="sxs-lookup"><span data-stu-id="9af13-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="9af13-115">チーム メンバーを追加する</span><span class="sxs-lookup"><span data-stu-id="9af13-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="9af13-116">必要な要件</span><span class="sxs-lookup"><span data-stu-id="9af13-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="9af13-117">メッセージ データの分析と準備</span><span class="sxs-lookup"><span data-stu-id="9af13-117">Analyze and prepare message data</span></span>

<span data-ttu-id="9af13-118">✔サード パーティのデータを確認して、移行するデータを決定します。</span><span class="sxs-lookup"><span data-stu-id="9af13-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="9af13-119">✔サード パーティのチャット システムから選択したデータを抽出します。</span><span class="sxs-lookup"><span data-stu-id="9af13-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="9af13-120">✔サード パーティのチャット構造を Teams の構造にマップします。</span><span class="sxs-lookup"><span data-stu-id="9af13-120">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="9af13-121">✔データを移行に必要な形式に変換します。</span><span class="sxs-lookup"><span data-stu-id="9af13-121">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="9af13-122">Office 365 テナントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="9af13-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="9af13-123">✔データ用に Office 365 テナントが存在することを確認します。</span><span class="sxs-lookup"><span data-stu-id="9af13-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="9af13-124">Teams の Office 365 テナントのセットアップの詳細については、「Office  [365](../../concepts/build-and-test/prepare-your-o365-tenant.md)テナントを準備する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9af13-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="9af13-125">✔チーム メンバーが Azure Active Directory (AAD) に存在するようにします。</span><span class="sxs-lookup"><span data-stu-id="9af13-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="9af13-126">詳細 *については、「Azure* Active Directory [に新しいユーザーを追加](/azure/active-directory/fundamentals/add-users-azure-active-directory) する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9af13-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="9af13-127">手順 1: チームを作成する</span><span class="sxs-lookup"><span data-stu-id="9af13-127">Step One: Create a team</span></span>

<span data-ttu-id="9af13-128">既存のデータは移行中ですから、元のメッセージのタイムスタンプを維持し、移行プロセス中のメッセージング アクティビティを防ぐことが、Teams でユーザーの既存のメッセージ フローを再作成する鍵になります。</span><span class="sxs-lookup"><span data-stu-id="9af13-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="9af13-129">これは、次のように行われます。</span><span class="sxs-lookup"><span data-stu-id="9af13-129">This is achieved as follows:</span></span>

> <span data-ttu-id="9af13-130">[チーム リソース プロパティを使用](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) して、バックインタイム タイムスタンプを持つ新しいチームを作成  `createdDateTime`  します。</span><span class="sxs-lookup"><span data-stu-id="9af13-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="9af13-131">新しいチームを配置します。移行プロセスが完了するまで、チーム内のほとんどのアクティビティからユーザーを選択できる `migration mode` 特別な状態です。</span><span class="sxs-lookup"><span data-stu-id="9af13-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="9af13-132">新しいチームを移行用に作成されたチームとして明示的に識別するには、POST 要求に値を持つ `teamCreationMode` `migration` instance 属性を含める。</span><span class="sxs-lookup"><span data-stu-id="9af13-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="9af13-133">**注**: このフィールドには、移行されたチームまたはチャネルのインスタンス `createdDateTime` に対するデータだけが入力されます。</span><span class="sxs-lookup"><span data-stu-id="9af13-133">**NOTE**:  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="9af13-134">許可</span><span class="sxs-lookup"><span data-stu-id="9af13-134">Permissions</span></span>

|<span data-ttu-id="9af13-135">ScopeName</span><span class="sxs-lookup"><span data-stu-id="9af13-135">ScopeName</span></span>|<span data-ttu-id="9af13-136">DisplayName</span><span class="sxs-lookup"><span data-stu-id="9af13-136">DisplayName</span></span>|<span data-ttu-id="9af13-137">説明</span><span class="sxs-lookup"><span data-stu-id="9af13-137">Description</span></span>|<span data-ttu-id="9af13-138">型</span><span class="sxs-lookup"><span data-stu-id="9af13-138">Type</span></span>|<span data-ttu-id="9af13-139">管理者の同意</span><span class="sxs-lookup"><span data-stu-id="9af13-139">Admin Consent?</span></span>|<span data-ttu-id="9af13-140">対象となるエンティティ/API</span><span class="sxs-lookup"><span data-stu-id="9af13-140">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="9af13-141">Microsoft Teams への移行の管理</span><span class="sxs-lookup"><span data-stu-id="9af13-141">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="9af13-142">Microsoft Teams に移行するためのリソースの作成、管理</span><span class="sxs-lookup"><span data-stu-id="9af13-142">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="9af13-143">**アプリケーション専用**</span><span class="sxs-lookup"><span data-stu-id="9af13-143">**Application-only**</span></span>|<span data-ttu-id="9af13-144">**はい**</span><span class="sxs-lookup"><span data-stu-id="9af13-144">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="9af13-145">要求 (移行状態でチームを作成する)</span><span class="sxs-lookup"><span data-stu-id="9af13-145">Request (create a team in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a><span data-ttu-id="9af13-146">応答</span><span class="sxs-lookup"><span data-stu-id="9af13-146">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="9af13-147">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="9af13-147">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="9af13-148">`createdDateTime`  を設定します。</span><span class="sxs-lookup"><span data-stu-id="9af13-148">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="9af13-149">`createdDateTime`  が正しく指定されているが `teamCreationMode`  、instance 属性が見つからないか無効な値に設定されている。</span><span class="sxs-lookup"><span data-stu-id="9af13-149">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="9af13-150">手順 2: チャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="9af13-150">Step Two: Create a channel</span></span>

<span data-ttu-id="9af13-151">インポートされたメッセージのチャネルの作成は、チーム作成シナリオに似ています。</span><span class="sxs-lookup"><span data-stu-id="9af13-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="9af13-152">[チャネル リソース プロパティを使用](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) して、バックインタイム タイムスタンプを持つ新しいチャネルを作成 `createdDateTime` します。</span><span class="sxs-lookup"><span data-stu-id="9af13-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="9af13-153">新しいチャネルを配置します。移行プロセスが完了するまで、チャネル内のほとんどのチャット アクティビティからユーザーをバーする `migration mode` 特別な状態です。</span><span class="sxs-lookup"><span data-stu-id="9af13-153">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="9af13-154">新しいチームを移行用に作成されたチームとして明示的に識別するには、POST 要求に値を持つ `channelCreationMode` `migration` instance 属性を含める。</span><span class="sxs-lookup"><span data-stu-id="9af13-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="9af13-155">許可</span><span class="sxs-lookup"><span data-stu-id="9af13-155">Permissions</span></span>

|<span data-ttu-id="9af13-156">ScopeName</span><span class="sxs-lookup"><span data-stu-id="9af13-156">ScopeName</span></span>|<span data-ttu-id="9af13-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="9af13-157">DisplayName</span></span>|<span data-ttu-id="9af13-158">説明</span><span class="sxs-lookup"><span data-stu-id="9af13-158">Description</span></span>|<span data-ttu-id="9af13-159">型</span><span class="sxs-lookup"><span data-stu-id="9af13-159">Type</span></span>|<span data-ttu-id="9af13-160">管理者の同意</span><span class="sxs-lookup"><span data-stu-id="9af13-160">Admin Consent?</span></span>|<span data-ttu-id="9af13-161">対象となるエンティティ/API</span><span class="sxs-lookup"><span data-stu-id="9af13-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="9af13-162">Microsoft Teams への移行の管理</span><span class="sxs-lookup"><span data-stu-id="9af13-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="9af13-163">Microsoft Teams への移行に関するリソースの作成、管理</span><span class="sxs-lookup"><span data-stu-id="9af13-163">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="9af13-164">**アプリケーション専用**</span><span class="sxs-lookup"><span data-stu-id="9af13-164">**Application-only**</span></span>|<span data-ttu-id="9af13-165">**はい**</span><span class="sxs-lookup"><span data-stu-id="9af13-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="9af13-166">要求 (移行状態でチャネルを作成する)</span><span class="sxs-lookup"><span data-stu-id="9af13-166">Request (create a channel in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.047Z"
}
```

#### <a name="response"></a><span data-ttu-id="9af13-167">応答</span><span class="sxs-lookup"><span data-stu-id="9af13-167">Response</span></span>

```http
HTTP/1.1 202 Accepted

{
   "@odata.context":"https://canary.graph.microsoft.com/testprodbetateamsgraphsvcncus/$metadata#teams('9cc6d6ab-07d8-4d14-bc2b-7db8995d6d23')/channels/$entity",
   "id":"19:e90f6814ce674072a4126206e7de485e@thread.tacv2",
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

#### <a name="error-message"></a><span data-ttu-id="9af13-168">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="9af13-168">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="9af13-169">`createdDateTime`  を設定します。</span><span class="sxs-lookup"><span data-stu-id="9af13-169">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="9af13-170">`createdDateTime`  が正しく指定 `channelCreationMode`  されましたが、インスタンス属性が見つからないか、無効な値に設定されています。</span><span class="sxs-lookup"><span data-stu-id="9af13-170">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="9af13-171">手順 3: メッセージをインポートする</span><span class="sxs-lookup"><span data-stu-id="9af13-171">Step Three: Import messages</span></span>

<span data-ttu-id="9af13-172">チームとチャネルを作成したら、要求本文のキーとキーを使用して、バックインタイム メッセージ `createdDateTime` `from`  の送信を開始できます。</span><span class="sxs-lookup"><span data-stu-id="9af13-172">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="9af13-173">**注**: メッセージ スレッドより `createdDateTime` 前のバージョンでインポートされたメッセージ `createdDateTime` はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="9af13-173">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="9af13-174">`createdDateTime` は、同じスレッド内のメッセージ間で一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="9af13-174">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="9af13-175">`createdDateTime` は、ミリ秒単位の精度でのタイムスタンプをサポートします。</span><span class="sxs-lookup"><span data-stu-id="9af13-175">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="9af13-176">たとえば、受信要求メッセージの値が `createdDateTime` *2020-09-16T05:50:31.0025302Z* に設定されている場合、メッセージが取り込まれたときに *2020-09-16T05:50:31.002Z* に変換されます。</span><span class="sxs-lookup"><span data-stu-id="9af13-176">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="9af13-177">要求 (テキスト専用の POST メッセージ)</span><span class="sxs-lookup"><span data-stu-id="9af13-177">Request (POST message that is text-only)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

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

#### <a name="response"></a><span data-ttu-id="9af13-178">応答</span><span class="sxs-lookup"><span data-stu-id="9af13-178">Response</span></span>

```http
HTTP/1.1 200 OK

{
   "@odata.context":"https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
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

#### <a name="error-messages"></a><span data-ttu-id="9af13-179">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="9af13-179">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="9af13-180">要求 (インライン画像を含むメッセージを POST する)</span><span class="sxs-lookup"><span data-stu-id="9af13-180">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="9af13-181">**注**: 要求は chatMessage の一部のため、このシナリオには特別なアクセス許可スコープはありません。chatMessage のスコープもここに適用されます。</span><span class="sxs-lookup"><span data-stu-id="9af13-181">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

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

#### <a name="response"></a><span data-ttu-id="9af13-182">応答</span><span class="sxs-lookup"><span data-stu-id="9af13-182">Response</span></span>

```http
HTTP/1.1 200 OK

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="9af13-183">手順 4: 移行モードの完了</span><span class="sxs-lookup"><span data-stu-id="9af13-183">Step Four: Complete migration mode</span></span>

<span data-ttu-id="9af13-184">メッセージ移行プロセスが完了すると、この方法を使用してチームとチャネルの両方が移行モードから抜  `completeMigration`  け出されます。</span><span class="sxs-lookup"><span data-stu-id="9af13-184">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="9af13-185">この手順では、チーム メンバーが一般的に使用するチームリソースとチャネル リソースを開きます。</span><span class="sxs-lookup"><span data-stu-id="9af13-185">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="9af13-186">アクションはインスタンスにバインド `team` されます。</span><span class="sxs-lookup"><span data-stu-id="9af13-186">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="9af13-187">要求 (チーム移行モードの終了)</span><span class="sxs-lookup"><span data-stu-id="9af13-187">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="9af13-188">応答</span><span class="sxs-lookup"><span data-stu-id="9af13-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="9af13-189">要求 (終了チャネル移行モード)</span><span class="sxs-lookup"><span data-stu-id="9af13-189">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="9af13-190">応答</span><span class="sxs-lookup"><span data-stu-id="9af13-190">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="9af13-191">エラー応答</span><span class="sxs-lookup"><span data-stu-id="9af13-191">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="9af13-192">に対して呼び `team` 出されたアクション `channel` 、または呼び出されていないアクション `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="9af13-192">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="9af13-193">手順 5: チーム メンバーを追加する</span><span class="sxs-lookup"><span data-stu-id="9af13-193">Step Five: Add team members</span></span>

<span data-ttu-id="9af13-194">Teams UI または Microsoft Graph メンバー [追加 API](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) を使用して、チームに [メンバーを追加](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) できます。</span><span class="sxs-lookup"><span data-stu-id="9af13-194">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="9af13-195">要求 (メンバーの追加)</span><span class="sxs-lookup"><span data-stu-id="9af13-195">Request (add member)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/{id}/members
Content-type: application/json
Content-length: 30
{
"@odata.type": "#microsoft.graph.aadUserConversationMember",
"roles": [],
"user@odata.bind": "https://graph.microsoft.com/beta/users/{user-id}"
}
```

#### <a name="response"></a><span data-ttu-id="9af13-196">応答</span><span class="sxs-lookup"><span data-stu-id="9af13-196">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="9af13-197">ヒントと追加情報</span><span class="sxs-lookup"><span data-stu-id="9af13-197">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="9af13-198">Teams に存在しないユーザーからメッセージをインポートできます。</span><span class="sxs-lookup"><span data-stu-id="9af13-198">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="9af13-199">**注**: テナントに存在しないユーザーにインポートされたメッセージは、パブリック プレビュー中に Teams クライアントまたはコンプライアンス ポータルで検索できません。</span><span class="sxs-lookup"><span data-stu-id="9af13-199">**NOTE**: Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="9af13-200">要求が `completeMigration` 行われたら、それ以上のメッセージをチームにインポートすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9af13-200">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="9af13-201">要求が正常に応答を返した後にのみ、チーム メンバーを新しい `completeMigration` チームに追加できます。</span><span class="sxs-lookup"><span data-stu-id="9af13-201">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="9af13-202">調整: メッセージはチャネルごとに 5 RPS でインポートされます。</span><span class="sxs-lookup"><span data-stu-id="9af13-202">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="9af13-203">移行結果を修正する必要がある場合は、チームを削除し、手順を繰り返してチームとチャネルを作成し、メッセージを再移行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9af13-203">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="9af13-204">現在、インライン画像は、インポート メッセージ API スキーマでサポートされている唯一の種類のメディアです。</span><span class="sxs-lookup"><span data-stu-id="9af13-204">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="9af13-205">コンテンツ 範囲をインポートする</span><span class="sxs-lookup"><span data-stu-id="9af13-205">Import content scope</span></span>

|<span data-ttu-id="9af13-206">スコープ内</span><span class="sxs-lookup"><span data-stu-id="9af13-206">In-scope</span></span> | <span data-ttu-id="9af13-207">現在、スコープ外</span><span class="sxs-lookup"><span data-stu-id="9af13-207">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="9af13-208">チームメッセージとチャネル メッセージ</span><span class="sxs-lookup"><span data-stu-id="9af13-208">Team and channel messages</span></span>|<span data-ttu-id="9af13-209">1:1 およびグループ チャット メッセージ</span><span class="sxs-lookup"><span data-stu-id="9af13-209">1:1 and group chat messages</span></span>|
|<span data-ttu-id="9af13-210">元のメッセージの作成時刻</span><span class="sxs-lookup"><span data-stu-id="9af13-210">Created time of the original message</span></span>|<span data-ttu-id="9af13-211">プライベート チャネル</span><span class="sxs-lookup"><span data-stu-id="9af13-211">Private channels</span></span>|
|<span data-ttu-id="9af13-212">メッセージの一部としてのインライン画像</span><span class="sxs-lookup"><span data-stu-id="9af13-212">Inline images as part of the message</span></span>|<span data-ttu-id="9af13-213">At mentions</span><span class="sxs-lookup"><span data-stu-id="9af13-213">At mentions</span></span>|
|<span data-ttu-id="9af13-214">SPO/OneDrive の既存のファイルへのリンク</span><span class="sxs-lookup"><span data-stu-id="9af13-214">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="9af13-215">リアクション</span><span class="sxs-lookup"><span data-stu-id="9af13-215">Reactions</span></span>|
|<span data-ttu-id="9af13-216">リッチ テキストを含むメッセージ</span><span class="sxs-lookup"><span data-stu-id="9af13-216">Messages with rich text</span></span>|<span data-ttu-id="9af13-217">ビデオ</span><span class="sxs-lookup"><span data-stu-id="9af13-217">Videos</span></span>|
|<span data-ttu-id="9af13-218">メッセージの返信チェーン</span><span class="sxs-lookup"><span data-stu-id="9af13-218">Message reply chain</span></span>|<span data-ttu-id="9af13-219">お知らせ</span><span class="sxs-lookup"><span data-stu-id="9af13-219">Announcements</span></span>|
|<span data-ttu-id="9af13-220">高スループット処理</span><span class="sxs-lookup"><span data-stu-id="9af13-220">High throughput processing</span></span>|<span data-ttu-id="9af13-221">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="9af13-221">Code snippets</span></span>|
||<span data-ttu-id="9af13-222">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="9af13-222">Adaptive cards</span></span>|
||<span data-ttu-id="9af13-223">ステッカー</span><span class="sxs-lookup"><span data-stu-id="9af13-223">Stickers</span></span>|
||<span data-ttu-id="9af13-224">Emojis</span><span class="sxs-lookup"><span data-stu-id="9af13-224">Emojis</span></span>|
||<span data-ttu-id="9af13-225">引用符</span><span class="sxs-lookup"><span data-stu-id="9af13-225">Quotes</span></span>|
||<span data-ttu-id="9af13-226">チャネル間のクロス投稿</span><span class="sxs-lookup"><span data-stu-id="9af13-226">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="9af13-227">Microsoft Graph と Teams の統合の詳細</span><span class="sxs-lookup"><span data-stu-id="9af13-227">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
