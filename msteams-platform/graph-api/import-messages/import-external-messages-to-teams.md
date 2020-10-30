---
title: Microsoft Graph を使用して外部プラットフォームのメッセージを Teams にインポートする
description: Microsoft Graph を使用して外部プラットフォームから Teams にメッセージをインポートする方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams インポートメッセージ api graph microsoft は移行の投稿を移行する
ms.openlocfilehash: 934e00541773140c90c270a616d6bc50aacac6e1
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796296"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="ed238-104">Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする</span><span class="sxs-lookup"><span data-stu-id="ed238-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="ed238-105">Microsoft Graph と Microsoft Teams の公開プレビューは、早期アクセスおよびフィードバックに使用できます。</span><span class="sxs-lookup"><span data-stu-id="ed238-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="ed238-106">このリリースは広範なテストを経ていますが、運用環境での使用は想定されていません。</span><span class="sxs-lookup"><span data-stu-id="ed238-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="ed238-107">Microsoft Graph を使用すると、ユーザーの既存のメッセージ履歴やデータを外部システムから Teams チャネルに移行できます。</span><span class="sxs-lookup"><span data-stu-id="ed238-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="ed238-108">Teams 内にサードパーティ製のプラットフォームのメッセージング階層を再利用できるようにすることで、ユーザーはシームレスな方法で通信を継続し、中断することなく処理を進めることができます。</span><span class="sxs-lookup"><span data-stu-id="ed238-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="ed238-109">インポートの概要</span><span class="sxs-lookup"><span data-stu-id="ed238-109">Import overview</span></span>

<span data-ttu-id="ed238-110">高レベルでは、インポートプロセスは次の要素で構成されます。</span><span class="sxs-lookup"><span data-stu-id="ed238-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="ed238-111">バックタイムタイムスタンプを使用してチームを作成する</span><span class="sxs-lookup"><span data-stu-id="ed238-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="ed238-112">バックタイムタイムスタンプを使用してチャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="ed238-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="ed238-113">外部のバックインタイムの日付のメッセージをインポートする</span><span class="sxs-lookup"><span data-stu-id="ed238-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="ed238-114">チームおよびチャネルの移行プロセスを完了する</span><span class="sxs-lookup"><span data-stu-id="ed238-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="ed238-115">チームメンバーを追加する</span><span class="sxs-lookup"><span data-stu-id="ed238-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="ed238-116">必要な要件</span><span class="sxs-lookup"><span data-stu-id="ed238-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="ed238-117">メッセージデータを分析して準備する</span><span class="sxs-lookup"><span data-stu-id="ed238-117">Analyze and prepare message data</span></span>

<span data-ttu-id="ed238-118">✔では、サードパーティのデータを確認して、移行対象を決定します。</span><span class="sxs-lookup"><span data-stu-id="ed238-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="ed238-119">✔サードパーティのチャットシステムから選択されたデータを抽出します。</span><span class="sxs-lookup"><span data-stu-id="ed238-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="ed238-120">✔、サードパーティのチャット構造を Teams 構造にマップします。</span><span class="sxs-lookup"><span data-stu-id="ed238-120">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="ed238-121">✔、移行に必要な形式にインポートデータを変換します。</span><span class="sxs-lookup"><span data-stu-id="ed238-121">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="ed238-122">Office 365 テナントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="ed238-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="ed238-123">✔インポートデータに Office 365 テナントが存在することを確認してください。</span><span class="sxs-lookup"><span data-stu-id="ed238-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="ed238-124">Teams 用の Office 365 テナントの設定の詳細については、「 [office 365 テナントを準備](../../concepts/build-and-test/prepare-your-o365-tenant.md)する *」を参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="ed238-124">For more information on setting up an Office 365 tenancy for Teams, *see* , [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="ed238-125">✔チームメンバーが Azure Active Directory (AAD) に含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ed238-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="ed238-126">詳細につい *て*[は、](/azure/active-directory/fundamentals/add-users-azure-active-directory) 「Azure Active Directory に新しいユーザーを追加する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed238-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="ed238-127">手順 1: チームを作成する</span><span class="sxs-lookup"><span data-stu-id="ed238-127">Step One: Create a team</span></span>

<span data-ttu-id="ed238-128">既存のデータは移行されているため、移行プロセス中の元のメッセージのタイムスタンプを維持し、メッセージングの動作を防ぐために、ユーザーの既存のメッセージフローを Teams に再作成するための鍵となります。</span><span class="sxs-lookup"><span data-stu-id="ed238-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="ed238-129">これは次のようにして実現されます。</span><span class="sxs-lookup"><span data-stu-id="ed238-129">This is achieved as follows:</span></span>

> <span data-ttu-id="ed238-130">チームリソースプロパティを使用して、タイムスタンプを持つ[新しいチームを作成](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true)し `createdDateTime` ます。</span><span class="sxs-lookup"><span data-stu-id="ed238-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="ed238-131">`migration mode`移行プロセスが完了するまで、チーム内のほとんどのアクティビティからのユーザーを表示する特別な状態で、新しいチームをに配置します。</span><span class="sxs-lookup"><span data-stu-id="ed238-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="ed238-132">`teamCreationMode` `migration` 移行のために作成される新しいチームを明示的に識別するために、POST 要求に値のインスタンス属性を含めます。</span><span class="sxs-lookup"><span data-stu-id="ed238-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="ed238-133">**注** : フィールドは、 `createdDateTime` 移行されたチームまたはチャネルのインスタンスに対してのみ設定されます。</span><span class="sxs-lookup"><span data-stu-id="ed238-133">**NOTE** :  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="ed238-134">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="ed238-134">Permissions</span></span>

|<span data-ttu-id="ed238-135">ScopeName</span><span class="sxs-lookup"><span data-stu-id="ed238-135">ScopeName</span></span>|<span data-ttu-id="ed238-136">DisplayName</span><span class="sxs-lookup"><span data-stu-id="ed238-136">DisplayName</span></span>|<span data-ttu-id="ed238-137">説明</span><span class="sxs-lookup"><span data-stu-id="ed238-137">Description</span></span>|<span data-ttu-id="ed238-138">型</span><span class="sxs-lookup"><span data-stu-id="ed238-138">Type</span></span>|<span data-ttu-id="ed238-139">管理者の同意</span><span class="sxs-lookup"><span data-stu-id="ed238-139">Admin Consent?</span></span>|<span data-ttu-id="ed238-140">対象となるエンティティ/Api</span><span class="sxs-lookup"><span data-stu-id="ed238-140">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="ed238-141">Microsoft Teams への移行の管理</span><span class="sxs-lookup"><span data-stu-id="ed238-141">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="ed238-142">Microsoft Teams への移行のためのリソースの作成、管理</span><span class="sxs-lookup"><span data-stu-id="ed238-142">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="ed238-143">**アプリケーション専用**</span><span class="sxs-lookup"><span data-stu-id="ed238-143">**Application-only**</span></span>|<span data-ttu-id="ed238-144">**はい**</span><span class="sxs-lookup"><span data-stu-id="ed238-144">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="ed238-145">要求 (移行状態でチームを作成する)</span><span class="sxs-lookup"><span data-stu-id="ed238-145">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="ed238-146">応答</span><span class="sxs-lookup"><span data-stu-id="ed238-146">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="ed238-147">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="ed238-147">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="ed238-148">`createdDateTime`  将来のために設定します。</span><span class="sxs-lookup"><span data-stu-id="ed238-148">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="ed238-149">`createdDateTime`  正しく指定されていますが、 `teamCreationMode`  インスタンス属性がないか、無効な値に設定されています。</span><span class="sxs-lookup"><span data-stu-id="ed238-149">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="ed238-150">手順 2: チャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="ed238-150">Step Two: Create a channel</span></span>

<span data-ttu-id="ed238-151">インポートされたメッセージのチャネルの作成は、「チームを作成する」シナリオに似ています。</span><span class="sxs-lookup"><span data-stu-id="ed238-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="ed238-152">Channel リソースプロパティを使用して、タイムスタンプがある[新しいチャネルを作成](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true)し `createdDateTime` ます。</span><span class="sxs-lookup"><span data-stu-id="ed238-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="ed238-153">新しいチャネルを `migration mode` 、移行プロセスが完了するまで、チャネル内のほとんどのチャットアクティビティからのユーザーを示す特別な状態で、その新しいチャネルを配置します。</span><span class="sxs-lookup"><span data-stu-id="ed238-153">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="ed238-154">`channelCreationMode` `migration` 移行のために作成される新しいチームを明示的に識別するために、POST 要求に値のインスタンス属性を含めます。</span><span class="sxs-lookup"><span data-stu-id="ed238-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="ed238-155">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="ed238-155">Permissions</span></span>

|<span data-ttu-id="ed238-156">ScopeName</span><span class="sxs-lookup"><span data-stu-id="ed238-156">ScopeName</span></span>|<span data-ttu-id="ed238-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="ed238-157">DisplayName</span></span>|<span data-ttu-id="ed238-158">説明</span><span class="sxs-lookup"><span data-stu-id="ed238-158">Description</span></span>|<span data-ttu-id="ed238-159">型</span><span class="sxs-lookup"><span data-stu-id="ed238-159">Type</span></span>|<span data-ttu-id="ed238-160">管理者の同意</span><span class="sxs-lookup"><span data-stu-id="ed238-160">Admin Consent?</span></span>|<span data-ttu-id="ed238-161">対象となるエンティティ/Api</span><span class="sxs-lookup"><span data-stu-id="ed238-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="ed238-162">Microsoft Teams への移行の管理</span><span class="sxs-lookup"><span data-stu-id="ed238-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="ed238-163">Microsoft Teams への移行のためのリソースの作成、管理</span><span class="sxs-lookup"><span data-stu-id="ed238-163">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="ed238-164">**アプリケーション専用**</span><span class="sxs-lookup"><span data-stu-id="ed238-164">**Application-only**</span></span>|<span data-ttu-id="ed238-165">**はい**</span><span class="sxs-lookup"><span data-stu-id="ed238-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="ed238-166">要求 (移行状態でチャネルを作成する)</span><span class="sxs-lookup"><span data-stu-id="ed238-166">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="ed238-167">応答</span><span class="sxs-lookup"><span data-stu-id="ed238-167">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="ed238-168">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="ed238-168">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="ed238-169">`createdDateTime`  将来のために設定します。</span><span class="sxs-lookup"><span data-stu-id="ed238-169">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="ed238-170">`createdDateTime`  正しく指定されていますが、 `channelCreationMode`  インスタンス属性がないか、無効な値に設定されています。</span><span class="sxs-lookup"><span data-stu-id="ed238-170">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="ed238-171">手順 3: メッセージをインポートする</span><span class="sxs-lookup"><span data-stu-id="ed238-171">Step Three: Import messages</span></span>

<span data-ttu-id="ed238-172">チームとチャネルを作成したら、 `createdDateTime`  要求本文のキーとキーを使用して、タイムラインメッセージの送信を開始することができ `from`  ます。</span><span class="sxs-lookup"><span data-stu-id="ed238-172">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="ed238-173">**注** : `createdDateTime` メッセージスレッドより前にインポートしたメッセージ `createdDateTime` はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="ed238-173">**NOTE** : messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> <span data-ttu-id="ed238-174">指定した Datetime は、同じスレッド内のメッセージ間で一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed238-174">createdDateTime must be unique across messages in the same thread.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="ed238-175">要求 (テキストのみの投稿メッセージ)</span><span class="sxs-lookup"><span data-stu-id="ed238-175">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="ed238-176">応答</span><span class="sxs-lookup"><span data-stu-id="ed238-176">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="ed238-177">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="ed238-177">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="ed238-178">要求 (インライン画像を含むメッセージを投稿する)</span><span class="sxs-lookup"><span data-stu-id="ed238-178">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="ed238-179">**注** : 要求は chatmessage の一部であるため、このシナリオでは特別なアクセス許可スコープがありません。チャットメッセージのスコープも同様に適用されます。</span><span class="sxs-lookup"><span data-stu-id="ed238-179">**Note** : There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="ed238-180">応答</span><span class="sxs-lookup"><span data-stu-id="ed238-180">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="ed238-181">手順 4: 移行モードを完了する</span><span class="sxs-lookup"><span data-stu-id="ed238-181">Step Four: Complete migration mode</span></span>

<span data-ttu-id="ed238-182">メッセージの移行プロセスが完了すると、チームとチャネルの両方が、メソッドを使用して移行モードから除外され  `completeMigration`  ます。</span><span class="sxs-lookup"><span data-stu-id="ed238-182">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="ed238-183">この手順では、チームメンバーによって一般的に使用されるチームとチャネルのリソースを開きます。</span><span class="sxs-lookup"><span data-stu-id="ed238-183">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="ed238-184">アクションはインスタンスにバインドされ `team` ます。</span><span class="sxs-lookup"><span data-stu-id="ed238-184">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="ed238-185">要求 (エンドチーム移行モード)</span><span class="sxs-lookup"><span data-stu-id="ed238-185">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="ed238-186">応答</span><span class="sxs-lookup"><span data-stu-id="ed238-186">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="ed238-187">要求 (エンドチャネル移行モード)</span><span class="sxs-lookup"><span data-stu-id="ed238-187">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="ed238-188">応答</span><span class="sxs-lookup"><span data-stu-id="ed238-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="ed238-189">エラー応答</span><span class="sxs-lookup"><span data-stu-id="ed238-189">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="ed238-190">に呼び出され `team` た、または `channel` のでないアクション `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="ed238-190">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="ed238-191">手順 5: チームメンバーを追加する</span><span class="sxs-lookup"><span data-stu-id="ed238-191">Step Five: Add team members</span></span>

<span data-ttu-id="ed238-192">Teams UI または Microsoft Graph [add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API[を使用して](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9)、チームにメンバーを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="ed238-192">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="ed238-193">要求 (メンバーの追加)</span><span class="sxs-lookup"><span data-stu-id="ed238-193">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="ed238-194">応答</span><span class="sxs-lookup"><span data-stu-id="ed238-194">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="ed238-195">ヒントと追加情報</span><span class="sxs-lookup"><span data-stu-id="ed238-195">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="ed238-196">Teams に含まれていないユーザーからメッセージをインポートできます。</span><span class="sxs-lookup"><span data-stu-id="ed238-196">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="ed238-197">**注** : テナントに存在しないユーザーのためにインポートされたメッセージは、パブリックプレビュー時に Teams クライアントまたはコンプライアンスポータルで検索できません。</span><span class="sxs-lookup"><span data-stu-id="ed238-197">**NOTE** : Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="ed238-198">`completeMigration`要求が行われると、チームにさらにメッセージをインポートすることはできません。</span><span class="sxs-lookup"><span data-stu-id="ed238-198">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="ed238-199">チームメンバーは、 `completeMigration` 要求が正常な応答を返した後は、新しいチームにのみ追加できます。</span><span class="sxs-lookup"><span data-stu-id="ed238-199">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="ed238-200">調整: チャネルごとに5個の RPS でメッセージがインポートされます。</span><span class="sxs-lookup"><span data-stu-id="ed238-200">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="ed238-201">移行結果に訂正を加える必要がある場合は、チームを削除して、チームとチャネルを作成してメッセージを再移行するための手順を繰り返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed238-201">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="ed238-202">現時点では、インライン画像は、インポートメッセージ API スキーマでサポートされている唯一の種類のメディアです。</span><span class="sxs-lookup"><span data-stu-id="ed238-202">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="ed238-203">コンテンツスコープのインポート</span><span class="sxs-lookup"><span data-stu-id="ed238-203">Import content scope</span></span>

|<span data-ttu-id="ed238-204">範囲内</span><span class="sxs-lookup"><span data-stu-id="ed238-204">In-scope</span></span> | <span data-ttu-id="ed238-205">現在スコープ外</span><span class="sxs-lookup"><span data-stu-id="ed238-205">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="ed238-206">チームおよびチャネルのメッセージ</span><span class="sxs-lookup"><span data-stu-id="ed238-206">Team and channel messages</span></span>|<span data-ttu-id="ed238-207">1:1 およびグループチャットメッセージ</span><span class="sxs-lookup"><span data-stu-id="ed238-207">1:1 and group chat messages</span></span>|
|<span data-ttu-id="ed238-208">元のメッセージの作成日時</span><span class="sxs-lookup"><span data-stu-id="ed238-208">Created time of the original message</span></span>|<span data-ttu-id="ed238-209">プライベート チャネル</span><span class="sxs-lookup"><span data-stu-id="ed238-209">Private channels</span></span>|
|<span data-ttu-id="ed238-210">メッセージの一部としてのインライン画像</span><span class="sxs-lookup"><span data-stu-id="ed238-210">Inline images as part of the message</span></span>|<span data-ttu-id="ed238-211">メンション</span><span class="sxs-lookup"><span data-stu-id="ed238-211">At mentions</span></span>|
|<span data-ttu-id="ed238-212">SPO/OneDrive の既存ファイルへのリンク</span><span class="sxs-lookup"><span data-stu-id="ed238-212">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="ed238-213">感想</span><span class="sxs-lookup"><span data-stu-id="ed238-213">Reactions</span></span>|
|<span data-ttu-id="ed238-214">リッチテキスト付きのメッセージ</span><span class="sxs-lookup"><span data-stu-id="ed238-214">Messages with rich text</span></span>|<span data-ttu-id="ed238-215">動画</span><span class="sxs-lookup"><span data-stu-id="ed238-215">Videos</span></span>|
|<span data-ttu-id="ed238-216">メッセージの返信チェーン</span><span class="sxs-lookup"><span data-stu-id="ed238-216">Message reply chain</span></span>|<span data-ttu-id="ed238-217">Announcements</span><span class="sxs-lookup"><span data-stu-id="ed238-217">Announcements</span></span>|
|<span data-ttu-id="ed238-218">高スループット処理</span><span class="sxs-lookup"><span data-stu-id="ed238-218">High throughput processing</span></span>|<span data-ttu-id="ed238-219">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="ed238-219">Code snippets</span></span>|
||<span data-ttu-id="ed238-220">アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="ed238-220">Adaptive cards</span></span>|
||<span data-ttu-id="ed238-221">シール</span><span class="sxs-lookup"><span data-stu-id="ed238-221">Stickers</span></span>|
||<span data-ttu-id="ed238-222">絵文字</span><span class="sxs-lookup"><span data-stu-id="ed238-222">Emojis</span></span>|
||<span data-ttu-id="ed238-223">括る</span><span class="sxs-lookup"><span data-stu-id="ed238-223">Quotes</span></span>|
||<span data-ttu-id="ed238-224">チャネル間でのクロス投稿</span><span class="sxs-lookup"><span data-stu-id="ed238-224">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="ed238-225">Microsoft Graph と Teams の統合の詳細情報</span><span class="sxs-lookup"><span data-stu-id="ed238-225">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
