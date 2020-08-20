---
title: Microsoft Graph を使用して外部プラットフォームのメッセージを Teams にインポートする
description: Microsoft Graph を使用して、外部プラットフォームから Teams にメッセージをインポートする方法について説明します
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: 'Teams Slack インポート メッセージ API グラフ: Microsoft が移行後の移行を行います'
ms.openlocfilehash: 8e8b21c9a38570d7ede745e27b9316b7aba29956
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "46820370"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="469c6-104">Microsoft Graph を使用して、サードパーティのプラットフォームのメッセージを Teams にインポートする</span><span class="sxs-lookup"><span data-stu-id="469c6-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="469c6-105">Microsoft Graph と Microsoft Teams のパブリック プレビューは、すでにアクセスしてフィードバックを行います。</span><span class="sxs-lookup"><span data-stu-id="469c6-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="469c6-106">このリリースは、拡張的なテストを受けてきてきてきませんが、運用環境での使用を意図したものではありません。</span><span class="sxs-lookup"><span data-stu-id="469c6-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="469c6-107">Microsoft Graph では、ユーザーの既存のメッセージ履歴とデータを外部システムから Teams チャネルに移行できます。</span><span class="sxs-lookup"><span data-stu-id="469c6-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="469c6-108">サードパーティ プラットフォームのメッセージング階層を Teams 内で再作成できるようにすれば、ユーザーは中断することなく通信をシームレスに続行し、操作を続行できます。</span><span class="sxs-lookup"><span data-stu-id="469c6-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="469c6-109">インポートの概要</span><span class="sxs-lookup"><span data-stu-id="469c6-109">Import overview</span></span>

<span data-ttu-id="469c6-110">大まかに説明したインポート プロセスは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="469c6-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="469c6-111">バックタイムスタンプを持つチームを作成する</span><span class="sxs-lookup"><span data-stu-id="469c6-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="469c6-112">バックタイムスタンプを持つチャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="469c6-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="469c6-113">外部の後に戻る日付付きメッセージをインポートする</span><span class="sxs-lookup"><span data-stu-id="469c6-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="469c6-114">チームとチャネルの移行プロセスを完了する</span><span class="sxs-lookup"><span data-stu-id="469c6-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="469c6-115">チーム メンバーを追加する</span><span class="sxs-lookup"><span data-stu-id="469c6-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="469c6-116">必要な要件</span><span class="sxs-lookup"><span data-stu-id="469c6-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="469c6-117">メッセージ データの分析と準備</span><span class="sxs-lookup"><span data-stu-id="469c6-117">Analyze and prepare message data</span></span>

<span data-ttu-id="469c6-118">✔サードパーティのデータを確認して、移行される内容を決定します。</span><span class="sxs-lookup"><span data-stu-id="469c6-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="469c6-119">✔サード パーティのチャット システムから選択したデータを抽出します。</span><span class="sxs-lookup"><span data-stu-id="469c6-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="469c6-120">✔必要な形式にインポート データを変換します。</span><span class="sxs-lookup"><span data-stu-id="469c6-120">✔ Convert import data into format needed for migration.</span></span>  
<span data-ttu-id="469c6-121">✔ーチームのチャット構造を Teams 構造にマップします。</span><span class="sxs-lookup"><span data-stu-id="469c6-121">✔ Map the third-party chat structure to the Teams structure.</span></span>

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="469c6-122">Office 365 テナントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="469c6-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="469c6-123">✔ 365 Officeがインポート データ用に存在することを確認します。</span><span class="sxs-lookup"><span data-stu-id="469c6-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="469c6-124">Teams に対する Office 365 テナンシーのセットアップ*see*の詳細については、「Teams の[Office 365 テナントを準備する」をご覧ください](../../concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="469c6-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="469c6-125">✔メンバーが Azure Active Directory (AAD) に含むことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="469c6-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="469c6-126">詳細 *については、「Azure* Active Directory [に新しいユーザー](/azure/active-directory/fundamentals/add-users-azure-active-directory) を追加する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="469c6-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="469c6-127">手順 1: チームを作成する</span><span class="sxs-lookup"><span data-stu-id="469c6-127">Step One: Create a team</span></span>

<span data-ttu-id="469c6-128">既存のデータを移行するので、元のメッセージ タイムスタンプを維持し、移行プロセス中のメッセージング処理を防止することが、Teams でのユーザーの既存のメッセージ フローを再作成するうえで重要です。</span><span class="sxs-lookup"><span data-stu-id="469c6-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="469c6-129">これは、次のように実現されます。</span><span class="sxs-lookup"><span data-stu-id="469c6-129">This is achieved as follows:</span></span>

1. <span data-ttu-id="469c6-130">[team リソース プロパティを使用](/graph/api/team-post?view=graph-rest-beta&tabs=http) して、バックタイムタイムタイムスタンプを持つ新しいチームを作成  `createdDateTime`  します。</span><span class="sxs-lookup"><span data-stu-id="469c6-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span>  

1. <span data-ttu-id="469c6-131">新しいチームを、移行 `migration mode` プロセスが完了するまでチーム内のほとんどのアクティビティのユーザーを主に主な状態にして配置します。</span><span class="sxs-lookup"><span data-stu-id="469c6-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="469c6-132">移行用 `teamCreationMode` に新しいチーム `migration` を明示的に識別するには、POST 要求にインスタンス属性を含めるようにします。</span><span class="sxs-lookup"><span data-stu-id="469c6-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="469c6-133">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="469c6-133">Permissions</span></span>

|<span data-ttu-id="469c6-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="469c6-134">ScopeName</span></span>|<span data-ttu-id="469c6-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="469c6-135">DisplayName</span></span>|<span data-ttu-id="469c6-136">説明</span><span class="sxs-lookup"><span data-stu-id="469c6-136">Description</span></span>|<span data-ttu-id="469c6-137">型</span><span class="sxs-lookup"><span data-stu-id="469c6-137">Type</span></span>|<span data-ttu-id="469c6-138">管理者の同意を有するか</span><span class="sxs-lookup"><span data-stu-id="469c6-138">Admin Consent?</span></span>|<span data-ttu-id="469c6-139">対象エンティティ/API</span><span class="sxs-lookup"><span data-stu-id="469c6-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="469c6-140">Microsoft Teams への移行を管理する</span><span class="sxs-lookup"><span data-stu-id="469c6-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="469c6-141">Microsoft Teams への移行に使用するリソースの作成、管理</span><span class="sxs-lookup"><span data-stu-id="469c6-141">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="469c6-142">**アプリケーションのみ**</span><span class="sxs-lookup"><span data-stu-id="469c6-142">**Application-only**</span></span>|<span data-ttu-id="469c6-143">**はい**</span><span class="sxs-lookup"><span data-stu-id="469c6-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="469c6-144">要求 (移行状態のチームを作成する)</span><span class="sxs-lookup"><span data-stu-id="469c6-144">Request (create a team in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description"
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a><span data-ttu-id="469c6-145">応答</span><span class="sxs-lookup"><span data-stu-id="469c6-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="469c6-146">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="469c6-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="469c6-147">`createdDateTime`  将来設定します。</span><span class="sxs-lookup"><span data-stu-id="469c6-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="469c6-148">`createdDateTime`  正しく指定されましたが `teamCreationMode`  、インスタンス属性がないか無効な値に設定されています。</span><span class="sxs-lookup"><span data-stu-id="469c6-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="469c6-149">手順 2: チャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="469c6-149">Step Two: Create a channel</span></span>

<span data-ttu-id="469c6-150">インポートされたメッセージのチャネルの作成は、チーム作成シナリオと似ています。</span><span class="sxs-lookup"><span data-stu-id="469c6-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span> 

1. <span data-ttu-id="469c6-151">channel[リソース プロパティを使用](/graph/api/channel-post?view=graph-rest-beta&tabs=http)して、時間内タイムスタンプを持つ新しいチャネルを作成 `createdDateTime` します。</span><span class="sxs-lookup"><span data-stu-id="469c6-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span>

1. <span data-ttu-id="469c6-152">新しいチャネルは、 `migration mode` 移行プロセスが完了するまでチャネル内のほとんどのチャット アクティビティのユーザーをバーでバー表示する特別な状態になります。</span><span class="sxs-lookup"><span data-stu-id="469c6-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="469c6-153">移行用 `channelCreationMode` に新しいチーム `migration` を明示的に識別するには、POST 要求にインスタンス属性を含めるようにします。</span><span class="sxs-lookup"><span data-stu-id="469c6-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="469c6-154">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="469c6-154">Permissions</span></span>

|<span data-ttu-id="469c6-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="469c6-155">ScopeName</span></span>|<span data-ttu-id="469c6-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="469c6-156">DisplayName</span></span>|<span data-ttu-id="469c6-157">説明</span><span class="sxs-lookup"><span data-stu-id="469c6-157">Description</span></span>|<span data-ttu-id="469c6-158">型</span><span class="sxs-lookup"><span data-stu-id="469c6-158">Type</span></span>|<span data-ttu-id="469c6-159">管理者の同意を有するか</span><span class="sxs-lookup"><span data-stu-id="469c6-159">Admin Consent?</span></span>|<span data-ttu-id="469c6-160">対象エンティティ/API</span><span class="sxs-lookup"><span data-stu-id="469c6-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="469c6-161">Microsoft Teams への移行を管理する</span><span class="sxs-lookup"><span data-stu-id="469c6-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="469c6-162">Microsoft Teams への移行に使用するリソースの作成、管理</span><span class="sxs-lookup"><span data-stu-id="469c6-162">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="469c6-163">**アプリケーションのみ**</span><span class="sxs-lookup"><span data-stu-id="469c6-163">**Application-only**</span></span>|<span data-ttu-id="469c6-164">**はい**</span><span class="sxs-lookup"><span data-stu-id="469c6-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="469c6-165">要求 (移行状態でチャネルを作成する)</span><span class="sxs-lookup"><span data-stu-id="469c6-165">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="469c6-166">応答</span><span class="sxs-lookup"><span data-stu-id="469c6-166">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a><span data-ttu-id="469c6-167">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="469c6-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="469c6-168">`createdDateTime`  将来設定します。</span><span class="sxs-lookup"><span data-stu-id="469c6-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="469c6-169">`createdDateTime`  正しく指定された `channelCreationMode`  が、インスタンス属性がないか、無効な値に設定されています。</span><span class="sxs-lookup"><span data-stu-id="469c6-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="469c6-170">手順 3: メッセージをインポートする</span><span class="sxs-lookup"><span data-stu-id="469c6-170">Step Three: Import messages</span></span>

<span data-ttu-id="469c6-171">チームとチャネルの作成が完了したら、要求本文内のキーとキーを使用して、特定の時間 `createdDateTime` `from`  内メッセージの送信を開始できます。</span><span class="sxs-lookup"><span data-stu-id="469c6-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="469c6-172">要求 (テキストのみの POST メッセージ)</span><span class="sxs-lookup"><span data-stu-id="469c6-172">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="469c6-173">応答</span><span class="sxs-lookup"><span data-stu-id="469c6-173">Response</span></span>

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

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="469c6-174">要求 (インライン '画像' を含むメッセージを POST する)</span><span class="sxs-lookup"><span data-stu-id="469c6-174">Request (POST a message with inline \`image)</span></span>

> <span data-ttu-id="469c6-175">**注**: このシナリオでは要求は chatMessage に含まれます。そのため、特別なアクセス許可のスコープはありません。chatMessage のスコープもここに当てはまります。</span><span class="sxs-lookup"><span data-stu-id="469c6-175">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="469c6-176">応答</span><span class="sxs-lookup"><span data-stu-id="469c6-176">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="469c6-177">手順 4: 移行モードを完了する</span><span class="sxs-lookup"><span data-stu-id="469c6-177">Step Four: Complete migration mode</span></span>

<span data-ttu-id="469c6-178">メッセージの移行処理が完了すると、チームとチャネルの両方が移行モードから移行モードから移行モードから移行モードから移行モードから移行モードから移行モードで行  `completeMigration`  います。</span><span class="sxs-lookup"><span data-stu-id="469c6-178">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="469c6-179">この手順を実行すると、チームとチャネルのリソースがチーム メンバーが一般的に使用できるので開きます。</span><span class="sxs-lookup"><span data-stu-id="469c6-179">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="469c6-180">アクションはインスタンスにバインド `team` されます。</span><span class="sxs-lookup"><span data-stu-id="469c6-180">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="469c6-181">要求 (チーム終了モード)</span><span class="sxs-lookup"><span data-stu-id="469c6-181">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="469c6-182">応答</span><span class="sxs-lookup"><span data-stu-id="469c6-182">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="469c6-183">要求 (チャネル移行モードの終了)</span><span class="sxs-lookup"><span data-stu-id="469c6-183">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="469c6-184">応答</span><span class="sxs-lookup"><span data-stu-id="469c6-184">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="469c6-185">エラー応答</span><span class="sxs-lookup"><span data-stu-id="469c6-185">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="469c6-186">指定されている、または `team` 存在しないアクション。 `channel` `migrationMode`</span><span class="sxs-lookup"><span data-stu-id="469c6-186">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="469c6-187">手順 5: チーム メンバーを追加する</span><span class="sxs-lookup"><span data-stu-id="469c6-187">Step Five: Add team members</span></span>

<span data-ttu-id="469c6-188">Teams の UI または Microsoft Graph のメンバー追加 [API を使用して](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 、チーム [にメンバーを追加](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) できます。</span><span class="sxs-lookup"><span data-stu-id="469c6-188">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="469c6-189">要求 (メンバーの追加)</span><span class="sxs-lookup"><span data-stu-id="469c6-189">Request (add member)</span></span>

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a><span data-ttu-id="469c6-190">応答</span><span class="sxs-lookup"><span data-stu-id="469c6-190">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="469c6-191">ヒントと追加情報</span><span class="sxs-lookup"><span data-stu-id="469c6-191">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="469c6-192">Teams のユーザーからメッセージをインポートできます。</span><span class="sxs-lookup"><span data-stu-id="469c6-192">You can import messages from users who are not in Teams.</span></span>

* <span data-ttu-id="469c6-193">要求が `completeMigration` 出された後に、チームにそれ以上のメッセージをインポートすることはできません。</span><span class="sxs-lookup"><span data-stu-id="469c6-193">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="469c6-194">要求が成功応答を返した後にのみ、チーム `completeMigration` メンバーは新しいチームに追加できます。</span><span class="sxs-lookup"><span data-stu-id="469c6-194">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="469c6-195">調整: メッセージはチャネルあたり 5 RPS でインポートされます。</span><span class="sxs-lookup"><span data-stu-id="469c6-195">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="469c6-196">移行結果を修正する必要がある場合は、チームを削除して手順を繰り返し、チームとチャネルを作成し、メッセージを再移行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="469c6-196">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="469c6-197">現在、インライン画像は、インポート メッセージ API スキーマでサポートされているメディアの種類のみをとしています。</span><span class="sxs-lookup"><span data-stu-id="469c6-197">Currently, Inline images is the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="469c6-198">コンテンツ範囲をインポートする</span><span class="sxs-lookup"><span data-stu-id="469c6-198">Import content scope</span></span>

|<span data-ttu-id="469c6-199">スコープ内</span><span class="sxs-lookup"><span data-stu-id="469c6-199">In-scope</span></span> | <span data-ttu-id="469c6-200">現在の対象外</span><span class="sxs-lookup"><span data-stu-id="469c6-200">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="469c6-201">チームおよびチャネル メッセージ</span><span class="sxs-lookup"><span data-stu-id="469c6-201">Team and channel messages</span></span>|<span data-ttu-id="469c6-202">1 対 1 およびグループ チャット メッセージ</span><span class="sxs-lookup"><span data-stu-id="469c6-202">1:1 and group chat messages</span></span>|
|<span data-ttu-id="469c6-203">元のメッセージの作成日時</span><span class="sxs-lookup"><span data-stu-id="469c6-203">Created time of the original message</span></span>|<span data-ttu-id="469c6-204">プライベート チャネル</span><span class="sxs-lookup"><span data-stu-id="469c6-204">Private channels</span></span>|
|<span data-ttu-id="469c6-205">メッセージの一部としてのインライン画像</span><span class="sxs-lookup"><span data-stu-id="469c6-205">Inline images as part of the message</span></span>|<span data-ttu-id="469c6-206">メンション</span><span class="sxs-lookup"><span data-stu-id="469c6-206">At mentions</span></span>|
|<span data-ttu-id="469c6-207">SPO/OneDrive の既存のファイルへのリンク</span><span class="sxs-lookup"><span data-stu-id="469c6-207">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="469c6-208">Reactions</span><span class="sxs-lookup"><span data-stu-id="469c6-208">Reactions</span></span>|
|<span data-ttu-id="469c6-209">リッチ テキスト付きメッセージ</span><span class="sxs-lookup"><span data-stu-id="469c6-209">Messages with rich text</span></span>|<span data-ttu-id="469c6-210">動画</span><span class="sxs-lookup"><span data-stu-id="469c6-210">Videos</span></span>|
|<span data-ttu-id="469c6-211">メッセージ返信チェーン</span><span class="sxs-lookup"><span data-stu-id="469c6-211">Message reply chain</span></span>|<span data-ttu-id="469c6-212">お知らせ</span><span class="sxs-lookup"><span data-stu-id="469c6-212">Announcements</span></span>|
|<span data-ttu-id="469c6-213">高いスループット処理</span><span class="sxs-lookup"><span data-stu-id="469c6-213">High throughput processing</span></span>|<span data-ttu-id="469c6-214">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="469c6-214">Code snippets</span></span>|
||<span data-ttu-id="469c6-215">アダプティブ カード</span><span class="sxs-lookup"><span data-stu-id="469c6-215">Adaptive cards</span></span>|
||<span data-ttu-id="469c6-216">ステッカー</span><span class="sxs-lookup"><span data-stu-id="469c6-216">Stickers</span></span>|
||<span data-ttu-id="469c6-217">Emojis</span><span class="sxs-lookup"><span data-stu-id="469c6-217">Emojis</span></span>|
||<span data-ttu-id="469c6-218">Quotes</span><span class="sxs-lookup"><span data-stu-id="469c6-218">Quotes</span></span>|
||<span data-ttu-id="469c6-219">チャネル間のクロス投稿</span><span class="sxs-lookup"><span data-stu-id="469c6-219">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="469c6-220">Microsoft Graph と Teams の統合に関する詳細情報</span><span class="sxs-lookup"><span data-stu-id="469c6-220">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
