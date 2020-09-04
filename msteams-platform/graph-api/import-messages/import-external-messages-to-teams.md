---
title: Microsoft Graph を使用して外部プラットフォームのメッセージを Teams にインポートする
description: Microsoft Graph を使用して外部プラットフォームから Teams にメッセージをインポートする方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams 余裕期間インポートメッセージ api グラフ microsoft は移行の投稿を移行する
ms.openlocfilehash: 0e0aa96373d29f07893456adf54986ec23bdec3c
ms.sourcegitcommit: 02ab2cb7820dc8665bb4ec6a1a40c3b8b8f29d66
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2020
ms.locfileid: "47340950"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="846e4-104">Microsoft Graph を使用してサードパーティのプラットフォーム メッセージを Teams にインポートする</span><span class="sxs-lookup"><span data-stu-id="846e4-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="846e4-105">Microsoft Graph と Microsoft Teams の公開プレビューは、早期アクセスおよびフィードバックに使用できます。</span><span class="sxs-lookup"><span data-stu-id="846e4-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="846e4-106">このリリースは広範なテストを経ていますが、運用環境での使用は想定されていません。</span><span class="sxs-lookup"><span data-stu-id="846e4-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="846e4-107">Microsoft Graph を使用すると、ユーザーの既存のメッセージ履歴やデータを外部システムから Teams チャネルに移行できます。</span><span class="sxs-lookup"><span data-stu-id="846e4-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="846e4-108">Teams 内にサードパーティ製のプラットフォームのメッセージング階層を再利用できるようにすることで、ユーザーはシームレスな方法で通信を継続し、中断することなく処理を進めることができます。</span><span class="sxs-lookup"><span data-stu-id="846e4-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="846e4-109">インポートの概要</span><span class="sxs-lookup"><span data-stu-id="846e4-109">Import overview</span></span>

<span data-ttu-id="846e4-110">高レベルでは、インポートプロセスは次の要素で構成されます。</span><span class="sxs-lookup"><span data-stu-id="846e4-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="846e4-111">バックタイムタイムスタンプを使用してチームを作成する</span><span class="sxs-lookup"><span data-stu-id="846e4-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="846e4-112">バックタイムタイムスタンプを使用してチャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="846e4-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="846e4-113">外部のバックインタイムの日付のメッセージをインポートする</span><span class="sxs-lookup"><span data-stu-id="846e4-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="846e4-114">チームおよびチャネルの移行プロセスを完了する</span><span class="sxs-lookup"><span data-stu-id="846e4-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="846e4-115">チームメンバーを追加する</span><span class="sxs-lookup"><span data-stu-id="846e4-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="846e4-116">必要な要件</span><span class="sxs-lookup"><span data-stu-id="846e4-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="846e4-117">メッセージデータを分析して準備する</span><span class="sxs-lookup"><span data-stu-id="846e4-117">Analyze and prepare message data</span></span>

<span data-ttu-id="846e4-118">✔では、サードパーティのデータを確認して、移行対象を決定します。</span><span class="sxs-lookup"><span data-stu-id="846e4-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="846e4-119">✔サードパーティのチャットシステムから選択されたデータを抽出します。</span><span class="sxs-lookup"><span data-stu-id="846e4-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="846e4-120">✔、移行に必要な形式にインポートデータを変換します。</span><span class="sxs-lookup"><span data-stu-id="846e4-120">✔ Convert import data into format needed for migration.</span></span>  
<span data-ttu-id="846e4-121">✔、サードパーティのチャット構造を Teams 構造にマップします。</span><span class="sxs-lookup"><span data-stu-id="846e4-121">✔ Map the third-party chat structure to the Teams structure.</span></span>

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="846e4-122">Office 365 テナントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="846e4-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="846e4-123">✔インポートデータに Office 365 テナントが存在することを確認してください。</span><span class="sxs-lookup"><span data-stu-id="846e4-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="846e4-124">Teams 用の Office 365 テナントの設定の詳細については、「 [office 365 テナントを準備](../../concepts/build-and-test/prepare-your-o365-tenant.md)する *」を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="846e4-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="846e4-125">✔チームメンバーが Azure Active Directory (AAD) に含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="846e4-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="846e4-126">詳細につい*て*[は、](/azure/active-directory/fundamentals/add-users-azure-active-directory) 「Azure Active Directory に新しいユーザーを追加する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="846e4-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="846e4-127">手順 1: チームを作成する</span><span class="sxs-lookup"><span data-stu-id="846e4-127">Step One: Create a team</span></span>

<span data-ttu-id="846e4-128">既存のデータは移行されているため、移行プロセス中の元のメッセージのタイムスタンプを維持し、メッセージングの動作を防ぐために、ユーザーの既存のメッセージフローを Teams に再作成するための鍵となります。</span><span class="sxs-lookup"><span data-stu-id="846e4-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="846e4-129">これは次のようにして実現されます。</span><span class="sxs-lookup"><span data-stu-id="846e4-129">This is achieved as follows:</span></span>

1. <span data-ttu-id="846e4-130">チームリソースプロパティを使用して、タイムスタンプを持つ[新しいチームを作成](/graph/api/team-post?view=graph-rest-beta&tabs=http)し `createdDateTime` ます。</span><span class="sxs-lookup"><span data-stu-id="846e4-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span>  

1. <span data-ttu-id="846e4-131">`migration mode`移行プロセスが完了するまで、チーム内のほとんどのアクティビティからのユーザーを表示する特別な状態で、新しいチームをに配置します。</span><span class="sxs-lookup"><span data-stu-id="846e4-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="846e4-132">`teamCreationMode` `migration` 移行のために作成される新しいチームを明示的に識別するために、POST 要求に値のインスタンス属性を含めます。</span><span class="sxs-lookup"><span data-stu-id="846e4-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="846e4-133">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="846e4-133">Permissions</span></span>

|<span data-ttu-id="846e4-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="846e4-134">ScopeName</span></span>|<span data-ttu-id="846e4-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="846e4-135">DisplayName</span></span>|<span data-ttu-id="846e4-136">説明</span><span class="sxs-lookup"><span data-stu-id="846e4-136">Description</span></span>|<span data-ttu-id="846e4-137">型</span><span class="sxs-lookup"><span data-stu-id="846e4-137">Type</span></span>|<span data-ttu-id="846e4-138">管理者の同意</span><span class="sxs-lookup"><span data-stu-id="846e4-138">Admin Consent?</span></span>|<span data-ttu-id="846e4-139">対象となるエンティティ/Api</span><span class="sxs-lookup"><span data-stu-id="846e4-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="846e4-140">Microsoft Teams への移行を管理する</span><span class="sxs-lookup"><span data-stu-id="846e4-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="846e4-141">Microsoft Teams への移行のためのリソースの作成、管理</span><span class="sxs-lookup"><span data-stu-id="846e4-141">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="846e4-142">**アプリケーション専用**</span><span class="sxs-lookup"><span data-stu-id="846e4-142">**Application-only**</span></span>|<span data-ttu-id="846e4-143">**はい**</span><span class="sxs-lookup"><span data-stu-id="846e4-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="846e4-144">要求 (移行状態でチームを作成する)</span><span class="sxs-lookup"><span data-stu-id="846e4-144">Request (create a team in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a><span data-ttu-id="846e4-145">応答</span><span class="sxs-lookup"><span data-stu-id="846e4-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="846e4-146">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="846e4-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="846e4-147">`createdDateTime`  将来のために設定します。</span><span class="sxs-lookup"><span data-stu-id="846e4-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="846e4-148">`createdDateTime`  正しく指定されていますが、 `teamCreationMode`  インスタンス属性がないか、無効な値に設定されています。</span><span class="sxs-lookup"><span data-stu-id="846e4-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="846e4-149">手順 2: チャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="846e4-149">Step Two: Create a channel</span></span>

<span data-ttu-id="846e4-150">インポートされたメッセージのチャネルの作成は、「チームを作成する」シナリオに似ています。</span><span class="sxs-lookup"><span data-stu-id="846e4-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span> 

1. <span data-ttu-id="846e4-151">Channel リソースプロパティを使用して、タイムスタンプがある[新しいチャネルを作成](/graph/api/channel-post?view=graph-rest-beta&tabs=http)し `createdDateTime` ます。</span><span class="sxs-lookup"><span data-stu-id="846e4-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span>

1. <span data-ttu-id="846e4-152">新しいチャネルを `migration mode` 、移行プロセスが完了するまで、チャネル内のほとんどのチャットアクティビティからのユーザーを示す特別な状態で、その新しいチャネルを配置します。</span><span class="sxs-lookup"><span data-stu-id="846e4-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="846e4-153">`channelCreationMode` `migration` 移行のために作成される新しいチームを明示的に識別するために、POST 要求に値のインスタンス属性を含めます。</span><span class="sxs-lookup"><span data-stu-id="846e4-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="846e4-154">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="846e4-154">Permissions</span></span>

|<span data-ttu-id="846e4-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="846e4-155">ScopeName</span></span>|<span data-ttu-id="846e4-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="846e4-156">DisplayName</span></span>|<span data-ttu-id="846e4-157">説明</span><span class="sxs-lookup"><span data-stu-id="846e4-157">Description</span></span>|<span data-ttu-id="846e4-158">型</span><span class="sxs-lookup"><span data-stu-id="846e4-158">Type</span></span>|<span data-ttu-id="846e4-159">管理者の同意</span><span class="sxs-lookup"><span data-stu-id="846e4-159">Admin Consent?</span></span>|<span data-ttu-id="846e4-160">対象となるエンティティ/Api</span><span class="sxs-lookup"><span data-stu-id="846e4-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="846e4-161">Microsoft Teams への移行を管理する</span><span class="sxs-lookup"><span data-stu-id="846e4-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="846e4-162">Microsoft Teams への移行のためのリソースの作成、管理</span><span class="sxs-lookup"><span data-stu-id="846e4-162">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="846e4-163">**アプリケーション専用**</span><span class="sxs-lookup"><span data-stu-id="846e4-163">**Application-only**</span></span>|<span data-ttu-id="846e4-164">**はい**</span><span class="sxs-lookup"><span data-stu-id="846e4-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="846e4-165">要求 (移行状態でチャネルを作成する)</span><span class="sxs-lookup"><span data-stu-id="846e4-165">Request (create a channel in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a><span data-ttu-id="846e4-166">応答</span><span class="sxs-lookup"><span data-stu-id="846e4-166">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a><span data-ttu-id="846e4-167">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="846e4-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="846e4-168">`createdDateTime`  将来のために設定します。</span><span class="sxs-lookup"><span data-stu-id="846e4-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="846e4-169">`createdDateTime`  正しく指定されていますが、 `channelCreationMode`  インスタンス属性がないか、無効な値に設定されています。</span><span class="sxs-lookup"><span data-stu-id="846e4-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="846e4-170">手順 3: メッセージをインポートする</span><span class="sxs-lookup"><span data-stu-id="846e4-170">Step Three: Import messages</span></span>

<span data-ttu-id="846e4-171">チームとチャネルを作成したら、 `createdDateTime`  要求本文のキーとキーを使用して、タイムラインメッセージの送信を開始することができ `from`  ます。</span><span class="sxs-lookup"><span data-stu-id="846e4-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="846e4-172">要求 (テキストのみの投稿メッセージ)</span><span class="sxs-lookup"><span data-stu-id="846e4-172">Request (POST message that is text-only)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
    "replyToId": null,
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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

#### <a name="response"></a><span data-ttu-id="846e4-173">応答</span><span class="sxs-lookup"><span data-stu-id="846e4-173">Response</span></span>

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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="846e4-174">要求 (インラインの ' image を含むメッセージを投稿する)</span><span class="sxs-lookup"><span data-stu-id="846e4-174">Request (POST a message with inline \`image)</span></span>

> <span data-ttu-id="846e4-175">**注**: 要求は chatmessage の一部であるため、このシナリオでは特別なアクセス許可スコープがありません。チャットメッセージのスコープも同様に適用されます。</span><span class="sxs-lookup"><span data-stu-id="846e4-175">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="846e4-176">応答</span><span class="sxs-lookup"><span data-stu-id="846e4-176">Response</span></span>

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
    {
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="846e4-177">手順 4: 移行モードを完了する</span><span class="sxs-lookup"><span data-stu-id="846e4-177">Step Four: Complete migration mode</span></span>

<span data-ttu-id="846e4-178">メッセージの移行プロセスが完了すると、チームとチャネルの両方が、メソッドを使用して移行モードから除外され  `completeMigration`  ます。</span><span class="sxs-lookup"><span data-stu-id="846e4-178">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="846e4-179">この手順では、チームメンバーによって一般的に使用されるチームとチャネルのリソースを開きます。</span><span class="sxs-lookup"><span data-stu-id="846e4-179">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="846e4-180">アクションはインスタンスにバインドされ `team` ます。</span><span class="sxs-lookup"><span data-stu-id="846e4-180">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="846e4-181">要求 (エンドチーム移行モード)</span><span class="sxs-lookup"><span data-stu-id="846e4-181">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="846e4-182">応答</span><span class="sxs-lookup"><span data-stu-id="846e4-182">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="846e4-183">要求 (エンドチャネル移行モード)</span><span class="sxs-lookup"><span data-stu-id="846e4-183">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="846e4-184">応答</span><span class="sxs-lookup"><span data-stu-id="846e4-184">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="846e4-185">エラー応答</span><span class="sxs-lookup"><span data-stu-id="846e4-185">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="846e4-186">に呼び出され `team` た、または `channel` のでないアクション `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="846e4-186">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="846e4-187">手順 5: チームメンバーを追加する</span><span class="sxs-lookup"><span data-stu-id="846e4-187">Step Five: Add team members</span></span>

<span data-ttu-id="846e4-188">Teams UI または Microsoft Graph [add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) API[を使用して](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9)、チームにメンバーを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="846e4-188">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="846e4-189">要求 (メンバーの追加)</span><span class="sxs-lookup"><span data-stu-id="846e4-189">Request (add member)</span></span>

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a><span data-ttu-id="846e4-190">応答</span><span class="sxs-lookup"><span data-stu-id="846e4-190">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="846e4-191">ヒントと追加情報</span><span class="sxs-lookup"><span data-stu-id="846e4-191">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="846e4-192">Teams に含まれていないユーザーからメッセージをインポートできます。</span><span class="sxs-lookup"><span data-stu-id="846e4-192">You can import messages from users who are not in Teams.</span></span>

* <span data-ttu-id="846e4-193">`completeMigration`要求が行われると、チームにさらにメッセージをインポートすることはできません。</span><span class="sxs-lookup"><span data-stu-id="846e4-193">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="846e4-194">チームメンバーは、 `completeMigration` 要求が正常な応答を返した後は、新しいチームにのみ追加できます。</span><span class="sxs-lookup"><span data-stu-id="846e4-194">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="846e4-195">調整: チャネルごとに5個の RPS でメッセージがインポートされます。</span><span class="sxs-lookup"><span data-stu-id="846e4-195">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="846e4-196">移行結果に訂正を加える必要がある場合は、チームを削除して、チームとチャネルを作成してメッセージを再移行するための手順を繰り返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="846e4-196">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="846e4-197">現在、インライン画像は、インポートメッセージ API スキーマでサポートされている唯一の種類のメディアです。</span><span class="sxs-lookup"><span data-stu-id="846e4-197">Currently, Inline images is the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="846e4-198">コンテンツスコープのインポート</span><span class="sxs-lookup"><span data-stu-id="846e4-198">Import content scope</span></span>

|<span data-ttu-id="846e4-199">範囲内</span><span class="sxs-lookup"><span data-stu-id="846e4-199">In-scope</span></span> | <span data-ttu-id="846e4-200">現在スコープ外</span><span class="sxs-lookup"><span data-stu-id="846e4-200">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="846e4-201">チームおよびチャネルのメッセージ</span><span class="sxs-lookup"><span data-stu-id="846e4-201">Team and channel messages</span></span>|<span data-ttu-id="846e4-202">1:1 およびグループチャットメッセージ</span><span class="sxs-lookup"><span data-stu-id="846e4-202">1:1 and group chat messages</span></span>|
|<span data-ttu-id="846e4-203">元のメッセージの作成日時</span><span class="sxs-lookup"><span data-stu-id="846e4-203">Created time of the original message</span></span>|<span data-ttu-id="846e4-204">プライベート チャネル</span><span class="sxs-lookup"><span data-stu-id="846e4-204">Private channels</span></span>|
|<span data-ttu-id="846e4-205">メッセージの一部としてのインライン画像</span><span class="sxs-lookup"><span data-stu-id="846e4-205">Inline images as part of the message</span></span>|<span data-ttu-id="846e4-206">メンション</span><span class="sxs-lookup"><span data-stu-id="846e4-206">At mentions</span></span>|
|<span data-ttu-id="846e4-207">SPO/OneDrive の既存ファイルへのリンク</span><span class="sxs-lookup"><span data-stu-id="846e4-207">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="846e4-208">感想</span><span class="sxs-lookup"><span data-stu-id="846e4-208">Reactions</span></span>|
|<span data-ttu-id="846e4-209">リッチテキスト付きのメッセージ</span><span class="sxs-lookup"><span data-stu-id="846e4-209">Messages with rich text</span></span>|<span data-ttu-id="846e4-210">動画</span><span class="sxs-lookup"><span data-stu-id="846e4-210">Videos</span></span>|
|<span data-ttu-id="846e4-211">メッセージの返信チェーン</span><span class="sxs-lookup"><span data-stu-id="846e4-211">Message reply chain</span></span>|<span data-ttu-id="846e4-212">お知らせ</span><span class="sxs-lookup"><span data-stu-id="846e4-212">Announcements</span></span>|
|<span data-ttu-id="846e4-213">高スループット処理</span><span class="sxs-lookup"><span data-stu-id="846e4-213">High throughput processing</span></span>|<span data-ttu-id="846e4-214">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="846e4-214">Code snippets</span></span>|
||<span data-ttu-id="846e4-215">アダプティブカード</span><span class="sxs-lookup"><span data-stu-id="846e4-215">Adaptive cards</span></span>|
||<span data-ttu-id="846e4-216">シール</span><span class="sxs-lookup"><span data-stu-id="846e4-216">Stickers</span></span>|
||<span data-ttu-id="846e4-217">絵文字</span><span class="sxs-lookup"><span data-stu-id="846e4-217">Emojis</span></span>|
||<span data-ttu-id="846e4-218">括る</span><span class="sxs-lookup"><span data-stu-id="846e4-218">Quotes</span></span>|
||<span data-ttu-id="846e4-219">チャネル間でのクロス投稿</span><span class="sxs-lookup"><span data-stu-id="846e4-219">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="846e4-220">Microsoft Graph と Teams の統合の詳細情報</span><span class="sxs-lookup"><span data-stu-id="846e4-220">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
