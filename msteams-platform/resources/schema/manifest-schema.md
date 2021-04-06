---
title: マニフェスト スキーマ参照
description: Microsoft Teams のマニフェスト スキーマについて説明します。
ms.topic: reference
ms.author: lajanuar
keywords: teams マニフェスト スキーマ
ms.openlocfilehash: fc7af73dd90ae74d76645281d9e761b91678873b
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585842"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="f7990-104">リファレンス: Microsoft Teams のマニフェスト スキーマ</span><span class="sxs-lookup"><span data-stu-id="f7990-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="f7990-105">Teams マニフェストは、アプリが Microsoft Teams 製品に統合される方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f7990-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="f7990-106">マニフェストは、 でホストされるスキーマに準拠している必要があります [`https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="f7990-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="f7990-107">以前のバージョン 1.0-1.4 もサポートされています (URL で "v1.x" を使用)。</span><span class="sxs-lookup"><span data-stu-id="f7990-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="f7990-108">次のスキーマ サンプルは、すべての機能拡張オプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="f7990-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="f7990-109">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="f7990-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",
  "manifestVersion": "1.9",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "localizationInfo": {
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
        "file": "en-us.json"
      }
    ]
  },
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters (<=100 chars)"
  },
  "description": {
    "short": "Short description of your app (<= 80 chars)",
    "full": "Full description of your app (<= 4000 chars)"
  },
  "icons": {
    "outline": "A relative path to a transparent .png icon — 32px X 32px",
    "color": "A relative path to a full color .png icon — 192px X 192px"
  },
  "accentColor": "A valid HTML color code.",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "scopes": [
        "team",
        "groupchat"
      ],
      "canUpdateConfiguration": true,
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
      ],
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": [
         "sharePointFullPage",
         "sharePointWebPart"
      ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "context":[
        "personalTab",
        "channelTab"
        ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser)",
       "searchUrl":  "https://contoso.com/content (displayed in web browser)"
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "scopes": [
        "team",
        "personal",
        "groupchat"
      ],
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "supportsFiles": true,
      "supportsCalling": false,
      "supportsVideo": true,
      "commandLists": [
        {
          "scopes": [
            "team",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command 2",
              "description": "Description of Command 2"
            }
          ]
        },
        {
          "scopes": [
            "personal",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
  "connectors": [
    {
      "connectorId": "GUID-FROM-CONNECTOR-DEV-PORTAL%",
      "scopes": [
        "team"
      ],
      "configurationUrl": "https://contoso.com/teamsconnector/configure"
    }
  ],
  "composeExtensions": [
    {
      "canUpdateConfiguration": true,
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "type": "query",
          "context": [
            "compose",
            "commandBox"
          ],
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "fetchTask": false,
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "inputType": "text",
              "description": "Enter the keywords to search for",
              "value": "Initial value for the parameter",
              "choices": [
                {
                  "title": "Title of the choice",
                  "value": "Value of the choice"
                }
              ]
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "type": "action",
          "context": [
            "message"
          ],
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "fetchTask": true,
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType": "text"
            }
          ]
        }
      ],
      "taskInfo": {
        "title": "Initial dialog title",
        "width": "Dialog width",
        "height": "Dialog height",
        "url": "Initial webview URL"
      },
      "messageHandlers": [
        {
          "type": "link",
          "value": {
            "domains": [
              "mysite.someplace.com",
              "othersite.someplace.com"
            ]
          }
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "devicePermissions": [
    "geolocation",
    "media",
    "notifications",
    "midi",
    "openExternal"
  ],
  "validDomains": [
    "contoso.com",
    "mysite.someplace.com",
    "othersite.someplace.com"
  ],
  "webApplicationInfo": {
    "id": "AAD App ID",
    "resource": "Resource URL for acquiring auth token for SSO",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelSettings.Read.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "ChannelMessage.Read.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group",
      "Member.ReadWrite.Group",
      "Owner.ReadWrite.Group"
    ],
  },
  "showLoadingIndicator": false,
  "isFullScreen": false,
  "activities": {
    "activityTypes": [
      {
        "type": "taskCreated",
        "description": "Task created activity",
        "templateText": "<team member> created task <taskId> for you"
      },
      {
        "type": "userMention",
        "description": "Personal mention activity",
        "templateText": "<team member> mentioned you"
      }
    ]
  },
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {"meetings": "tab" , "team": "bot", "groupchat": "bot"}
}
```

<span data-ttu-id="f7990-110">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="f7990-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="f7990-111">$schema</span><span class="sxs-lookup"><span data-stu-id="f7990-111">$schema</span></span>

<span data-ttu-id="f7990-112">省略可能ですが、推奨される — string</span><span class="sxs-lookup"><span data-stu-id="f7990-112">Optional, but recommended — string</span></span>

<span data-ttu-id="f7990-113">マニフェスト https:// JSON スキーマを参照する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="f7990-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="f7990-114">manifestVersion</span></span>

<span data-ttu-id="f7990-115">**必須** — 文字列</span><span class="sxs-lookup"><span data-stu-id="f7990-115">**Required** — string</span></span>

<span data-ttu-id="f7990-116">このマニフェストが使用しているマニフェスト スキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="f7990-116">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="f7990-117">1.9 である必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-117">It must be 1.9.</span></span>

## <a name="version"></a><span data-ttu-id="f7990-118">version</span><span class="sxs-lookup"><span data-stu-id="f7990-118">version</span></span>

<span data-ttu-id="f7990-119">**必須** — 文字列</span><span class="sxs-lookup"><span data-stu-id="f7990-119">**Required** — string</span></span>

<span data-ttu-id="f7990-120">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="f7990-120">The version of a specific app.</span></span> <span data-ttu-id="f7990-121">マニフェストで何かを更新する場合は、バージョンもインクリメントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-121">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="f7990-122">これにより、新しいマニフェストがインストールされた場合、既存のマニフェストが上書きされ、ユーザーは新しい機能を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="f7990-122">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="f7990-123">このアプリがストアに送信された場合は、新しいマニフェストを再送信して再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-123">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="f7990-124">アプリユーザーは、マニフェストが承認された後、数時間以内に新しい更新されたマニフェストを自動的に受信します。</span><span class="sxs-lookup"><span data-stu-id="f7990-124">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="f7990-125">アプリでアクセス許可の要求が変更された場合、ユーザーはアプリのアップグレードと再同意を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f7990-125">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="f7990-126">このバージョンの文字列は [、semver](http://semver.org/) 標準 (MAJOR) に従う必要があります。MINOR。PATCH)。</span><span class="sxs-lookup"><span data-stu-id="f7990-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="f7990-127">id</span><span class="sxs-lookup"><span data-stu-id="f7990-127">id</span></span>

<span data-ttu-id="f7990-128">**必須** — Microsoft アプリ ID</span><span class="sxs-lookup"><span data-stu-id="f7990-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="f7990-129">ID は、アプリの Microsoft が生成する一意の識別子です。</span><span class="sxs-lookup"><span data-stu-id="f7990-129">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="f7990-130">ボットが Microsoft Bot Framework を通じて登録されている場合、またはタブの Web アプリが既に Microsoft にサインインしている場合は、ID を持っています。</span><span class="sxs-lookup"><span data-stu-id="f7990-130">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="f7990-131">ここに ID を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-131">You must enter the ID here.</span></span> <span data-ttu-id="f7990-132">それ以外の場合は、Microsoft アプリケーション登録ポータル (My Applications) で新しい ID[を生成する必要があります](https://apps.dev.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="f7990-132">Otherwise, you must generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)).</span></span> <span data-ttu-id="f7990-133">ボットを追加する場合は、同じ ID を使用します。</span><span class="sxs-lookup"><span data-stu-id="f7990-133">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="f7990-134">AppSource で既存のアプリに更新プログラムを提出する場合は、マニフェスト内の ID を変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="f7990-134">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="f7990-135">developer</span><span class="sxs-lookup"><span data-stu-id="f7990-135">developer</span></span>

<span data-ttu-id="f7990-136">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="f7990-136">**Required** — object</span></span>

<span data-ttu-id="f7990-137">会社に関する情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="f7990-137">Gives information about your company.</span></span> <span data-ttu-id="f7990-138">AppSource に送信されたアプリ (以前は Officeストア) の場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="f7990-139">詳細については [、発行ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7990-139">See the [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="f7990-140">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-140">Name</span></span>| <span data-ttu-id="f7990-141">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-141">Maximum size</span></span> | <span data-ttu-id="f7990-142">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-142">Required</span></span> | <span data-ttu-id="f7990-143">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="f7990-144">32 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-144">32 characters</span></span>|<span data-ttu-id="f7990-145">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-145">✔</span></span>|<span data-ttu-id="f7990-146">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="f7990-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="f7990-147">2048 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-147">2048 characters</span></span>|<span data-ttu-id="f7990-148">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-148">✔</span></span>|<span data-ttu-id="f7990-149">開発者 https:// WEB サイトの URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="f7990-150">このリンクは、ユーザーを会社または製品固有のランディング ページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-150">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="f7990-151">2048 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-151">2048 characters</span></span>|<span data-ttu-id="f7990-152">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-152">✔</span></span>|<span data-ttu-id="f7990-153">開発者 https:// のプライバシー ポリシーの URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="f7990-154">2048 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-154">2048 characters</span></span>|<span data-ttu-id="f7990-155">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-155">✔</span></span>|<span data-ttu-id="f7990-156">開発者 https:// の使用条件の URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="f7990-157">10 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-157">10 characters</span></span>| |<span data-ttu-id="f7990-158">**省略可能** アプリを構築するパートナー組織を識別する Microsoft パートナー ネットワーク ID。</span><span class="sxs-lookup"><span data-stu-id="f7990-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="f7990-159">name</span><span class="sxs-lookup"><span data-stu-id="f7990-159">name</span></span>

<span data-ttu-id="f7990-160">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="f7990-160">**Required** — object</span></span>

<span data-ttu-id="f7990-161">Teams エクスペリエンスのユーザーに表示されるアプリ エクスペリエンスの名前。</span><span class="sxs-lookup"><span data-stu-id="f7990-161">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="f7990-162">AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-162">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="f7990-163">の値と `short` 異 `full` なる値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-163">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="f7990-164">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-164">Name</span></span>| <span data-ttu-id="f7990-165">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-165">Maximum size</span></span> | <span data-ttu-id="f7990-166">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-166">Required</span></span> | <span data-ttu-id="f7990-167">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-167">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="f7990-168">30 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-168">30 characters</span></span>|<span data-ttu-id="f7990-169">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-169">✔</span></span>|<span data-ttu-id="f7990-170">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="f7990-170">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="f7990-171">100 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-171">100 characters</span></span>||<span data-ttu-id="f7990-172">完全なアプリ名が 30 文字を超える場合に使用されるアプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="f7990-172">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="f7990-173">description</span><span class="sxs-lookup"><span data-stu-id="f7990-173">description</span></span>

<span data-ttu-id="f7990-174">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="f7990-174">**Required** — object</span></span>

<span data-ttu-id="f7990-175">アプリをユーザーに説明します。</span><span class="sxs-lookup"><span data-stu-id="f7990-175">Describes your app to users.</span></span> <span data-ttu-id="f7990-176">AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-176">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="f7990-177">説明がエクスペリエンスを正確に説明し、潜在的な顧客がエクスペリエンスの内容を理解するのに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="f7990-177">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="f7990-178">外部アカウントを使用する必要がある場合は、完全な説明に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-178">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="f7990-179">の値と `short` 異 `full` なる値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-179">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="f7990-180">短い説明は、長い説明の中で繰り返し実行し、他のアプリ名を含めずに行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-180">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="f7990-181">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-181">Name</span></span>| <span data-ttu-id="f7990-182">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-182">Maximum size</span></span> | <span data-ttu-id="f7990-183">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-183">Required</span></span> | <span data-ttu-id="f7990-184">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-184">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="f7990-185">80 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-185">80 characters</span></span>|<span data-ttu-id="f7990-186">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-186">✔</span></span>|<span data-ttu-id="f7990-187">スペースが制限されている場合に使用されるアプリ エクスペリエンスの簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="f7990-187">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="f7990-188">4000 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-188">4000 characters</span></span>|<span data-ttu-id="f7990-189">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-189">✔</span></span>|<span data-ttu-id="f7990-190">アプリの完全な説明。</span><span class="sxs-lookup"><span data-stu-id="f7990-190">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="f7990-191">packageName</span><span class="sxs-lookup"><span data-stu-id="f7990-191">packageName</span></span>

<span data-ttu-id="f7990-192">**省略** 可能 — 文字列</span><span class="sxs-lookup"><span data-stu-id="f7990-192">**Optional** — string</span></span>

<span data-ttu-id="f7990-193">逆ドメイン表記のアプリの一意の識別子。たとえば、com.example.myapp などです。</span><span class="sxs-lookup"><span data-stu-id="f7990-193">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="f7990-194">最大長: 64 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-194">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="f7990-195">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="f7990-195">localizationInfo</span></span>

<span data-ttu-id="f7990-196">**省略可能** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="f7990-196">**Optional** — object</span></span>

<span data-ttu-id="f7990-197">既定の言語の指定と、追加の言語ファイルへのポインターを許可します。</span><span class="sxs-lookup"><span data-stu-id="f7990-197">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="f7990-198">「ローカライズ」 [を参照してください](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="f7990-198">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="f7990-199">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-199">Name</span></span>| <span data-ttu-id="f7990-200">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-200">Maximum size</span></span> | <span data-ttu-id="f7990-201">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-201">Required</span></span> | <span data-ttu-id="f7990-202">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-202">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="f7990-203">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-203">✔</span></span>|<span data-ttu-id="f7990-204">このトップ レベルのマニフェスト ファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="f7990-204">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="f7990-205">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="f7990-205">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="f7990-206">追加の言語変換を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="f7990-206">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="f7990-207">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-207">Name</span></span>| <span data-ttu-id="f7990-208">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-208">Maximum size</span></span> | <span data-ttu-id="f7990-209">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-209">Required</span></span> | <span data-ttu-id="f7990-210">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-210">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="f7990-211">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-211">✔</span></span>|<span data-ttu-id="f7990-212">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="f7990-212">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="f7990-213">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-213">✔</span></span>|<span data-ttu-id="f7990-214">翻訳された文字列を含む .json ファイルへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="f7990-214">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="f7990-215">アイコン</span><span class="sxs-lookup"><span data-stu-id="f7990-215">icons</span></span>

<span data-ttu-id="f7990-216">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="f7990-216">**Required** — object</span></span>

<span data-ttu-id="f7990-217">Teams アプリ内で使用されるアイコン。</span><span class="sxs-lookup"><span data-stu-id="f7990-217">Icons used within the Teams app.</span></span> <span data-ttu-id="f7990-218">アイコン ファイルは、アップロード パッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-218">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="f7990-219">詳細については [、「アイコン](../../concepts/build-and-test/apps-package.md#app-icons) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7990-219">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="f7990-220">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-220">Name</span></span>| <span data-ttu-id="f7990-221">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-221">Maximum size</span></span> | <span data-ttu-id="f7990-222">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-222">Required</span></span> | <span data-ttu-id="f7990-223">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="f7990-224">32 x 32 ピクセル</span><span class="sxs-lookup"><span data-stu-id="f7990-224">32 x 32 pixels</span></span>|<span data-ttu-id="f7990-225">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-225">✔</span></span>|<span data-ttu-id="f7990-226">透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="f7990-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="f7990-227">192 x 192 ピクセル</span><span class="sxs-lookup"><span data-stu-id="f7990-227">192 x 192 pixels</span></span>|<span data-ttu-id="f7990-228">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-228">✔</span></span>|<span data-ttu-id="f7990-229">フル カラーの 192x192 PNG アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="f7990-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="f7990-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="f7990-230">accentColor</span></span>

<span data-ttu-id="f7990-231">**省略** 可能 — HTML の 16 進カラー コード</span><span class="sxs-lookup"><span data-stu-id="f7990-231">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="f7990-232">アウトライン アイコンと組み合わせて、背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="f7990-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="f7990-233">値は、'#' で始まる有効な HTML カラー コードである必要があります `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="f7990-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="f7990-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="f7990-234">configurableTabs</span></span>

<span data-ttu-id="f7990-235">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="f7990-235">**Optional** — array</span></span>

<span data-ttu-id="f7990-236">アプリ エクスペリエンスに、追加する前に追加の構成が必要なチーム チャネル タブ エクスペリエンスがある場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="f7990-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="f7990-237">構成可能なタブは teams スコープでのみサポートされ (個人用ではなく)、現在はアプリごとに 1 **つのタブ** しかサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="f7990-237">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="f7990-238">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-238">Name</span></span>| <span data-ttu-id="f7990-239">型</span><span class="sxs-lookup"><span data-stu-id="f7990-239">Type</span></span>| <span data-ttu-id="f7990-240">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-240">Maximum size</span></span> | <span data-ttu-id="f7990-241">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-241">Required</span></span> | <span data-ttu-id="f7990-242">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-242">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="f7990-243">string</span><span class="sxs-lookup"><span data-stu-id="f7990-243">string</span></span>|<span data-ttu-id="f7990-244">2048 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-244">2048 characters</span></span>|<span data-ttu-id="f7990-245">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-245">✔</span></span>|<span data-ttu-id="f7990-246">タブ https:// する際に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-246">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="f7990-247">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-247">array of enums</span></span>|<span data-ttu-id="f7990-248">1</span><span class="sxs-lookup"><span data-stu-id="f7990-248">1</span></span>|<span data-ttu-id="f7990-249">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-249">✔</span></span>|<span data-ttu-id="f7990-250">現在、構成可能なタブは、スコープ `team` とスコープ `groupchat` のみをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="f7990-250">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="f7990-251">ブール値</span><span class="sxs-lookup"><span data-stu-id="f7990-251">boolean</span></span>|||<span data-ttu-id="f7990-252">作成後に、タブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="f7990-252">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="f7990-253">既定値: **true 。**</span><span class="sxs-lookup"><span data-stu-id="f7990-253">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="f7990-254">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-254">array of enums</span></span>|<span data-ttu-id="f7990-255">6</span><span class="sxs-lookup"><span data-stu-id="f7990-255">6</span></span>||<span data-ttu-id="f7990-256">タブが `contextItem` サポートされているスコープのセット。</span><span class="sxs-lookup"><span data-stu-id="f7990-256">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="f7990-257">既定値: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="f7990-257">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="f7990-258">string</span><span class="sxs-lookup"><span data-stu-id="f7990-258">string</span></span>|<span data-ttu-id="f7990-259">2048</span><span class="sxs-lookup"><span data-stu-id="f7990-259">2048</span></span>||<span data-ttu-id="f7990-260">SharePoint で使用するタブ プレビュー イメージへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="f7990-260">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="f7990-261">サイズは 1024x768 です。</span><span class="sxs-lookup"><span data-stu-id="f7990-261">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="f7990-262">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-262">array of enums</span></span>|<span data-ttu-id="f7990-263">1</span><span class="sxs-lookup"><span data-stu-id="f7990-263">1</span></span>||<span data-ttu-id="f7990-264">SharePoint でタブを使用する方法を定義します。</span><span class="sxs-lookup"><span data-stu-id="f7990-264">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="f7990-265">オプションは `sharePointFullPage` 次のとおりです。 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="f7990-265">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="f7990-266">staticTabs</span><span class="sxs-lookup"><span data-stu-id="f7990-266">staticTabs</span></span>

<span data-ttu-id="f7990-267">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="f7990-267">**Optional** — array</span></span>

<span data-ttu-id="f7990-268">ユーザーが手動で追加せずに、既定で "ピン留め" できるタブのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="f7990-268">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="f7990-269">スコープ内で宣言された静的タブ `personal` は、常にアプリの個人用エクスペリエンスにピン留めされます。</span><span class="sxs-lookup"><span data-stu-id="f7990-269">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="f7990-270">スコープで宣言されている静的タブ `team` は現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="f7990-270">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="f7990-271">このアイテムは、型のすべての要素を持つ配列 (最大 16 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="f7990-271">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="f7990-272">このブロックは、静的タブ ソリューションを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="f7990-272">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="f7990-273">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-273">Name</span></span>| <span data-ttu-id="f7990-274">型</span><span class="sxs-lookup"><span data-stu-id="f7990-274">Type</span></span>| <span data-ttu-id="f7990-275">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-275">Maximum size</span></span> | <span data-ttu-id="f7990-276">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-276">Required</span></span> | <span data-ttu-id="f7990-277">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-277">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="f7990-278">string</span><span class="sxs-lookup"><span data-stu-id="f7990-278">string</span></span>|<span data-ttu-id="f7990-279">64 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-279">64 characters</span></span>|<span data-ttu-id="f7990-280">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-280">✔</span></span>|<span data-ttu-id="f7990-281">タブが表示されるエンティティの一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="f7990-281">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="f7990-282">string</span><span class="sxs-lookup"><span data-stu-id="f7990-282">string</span></span>|<span data-ttu-id="f7990-283">128 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-283">128 characters</span></span>|<span data-ttu-id="f7990-284">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-284">✔</span></span>|<span data-ttu-id="f7990-285">チャネル インターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="f7990-285">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="f7990-286">string</span><span class="sxs-lookup"><span data-stu-id="f7990-286">string</span></span>||<span data-ttu-id="f7990-287">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-287">✔</span></span>|<span data-ttu-id="f7990-288">Teams https:// 表示するエンティティ UI を示す URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-288">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="f7990-289">string</span><span class="sxs-lookup"><span data-stu-id="f7990-289">string</span></span>|||<span data-ttu-id="f7990-290">ユーザー https:// ブラウザーで表示することを選択した場合に示す URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-290">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="f7990-291">string</span><span class="sxs-lookup"><span data-stu-id="f7990-291">string</span></span>|||<span data-ttu-id="f7990-292">ユーザー https:// 検索クエリを参照する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-292">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="f7990-293">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-293">array of enums</span></span>|<span data-ttu-id="f7990-294">1</span><span class="sxs-lookup"><span data-stu-id="f7990-294">1</span></span>|<span data-ttu-id="f7990-295">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-295">✔</span></span>|<span data-ttu-id="f7990-296">現在、静的タブはスコープのみをサポートしています。つまり、個人用エクスペリエンスの一部としてのみ `personal` プロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="f7990-296">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="f7990-297">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-297">array of enums</span></span>| <span data-ttu-id="f7990-298">2</span><span class="sxs-lookup"><span data-stu-id="f7990-298">2</span></span>|| <span data-ttu-id="f7990-299">タブが `contextItem` サポートされているスコープのセット。</span><span class="sxs-lookup"><span data-stu-id="f7990-299">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="f7990-300">関連するコンテンツを表示したり、認証フローを開始したりするために、タブでコンテキストに依存する情報が必要な場合は、「Microsoft Teams タブのコンテキストを取得する」[を参照してください](../../tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="f7990-300">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="f7990-301">bots</span><span class="sxs-lookup"><span data-stu-id="f7990-301">bots</span></span>

<span data-ttu-id="f7990-302">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="f7990-302">**Optional** — array</span></span>

<span data-ttu-id="f7990-303">既定のコマンド プロパティなどのオプションの情報と共に、ボット ソリューションを定義します。</span><span class="sxs-lookup"><span data-stu-id="f7990-303">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="f7990-304">アイテムは、型のすべての要素を持つ配列 (現在、アプリごとにボットが 1 つしか許可されていない要素が最大 1 つ) &mdash; です `object` 。</span><span class="sxs-lookup"><span data-stu-id="f7990-304">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="f7990-305">このブロックは、ボット エクスペリエンスを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="f7990-305">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="f7990-306">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-306">Name</span></span>| <span data-ttu-id="f7990-307">型</span><span class="sxs-lookup"><span data-stu-id="f7990-307">Type</span></span>| <span data-ttu-id="f7990-308">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-308">Maximum size</span></span> | <span data-ttu-id="f7990-309">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-309">Required</span></span> | <span data-ttu-id="f7990-310">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-310">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="f7990-311">string</span><span class="sxs-lookup"><span data-stu-id="f7990-311">string</span></span>|<span data-ttu-id="f7990-312">64 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-312">64 characters</span></span>|<span data-ttu-id="f7990-313">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-313">✔</span></span>|<span data-ttu-id="f7990-314">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="f7990-314">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="f7990-315">これは、アプリ全体の ID と同じ [可能性があります](#id)。</span><span class="sxs-lookup"><span data-stu-id="f7990-315">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="f7990-316">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-316">array of enums</span></span>|<span data-ttu-id="f7990-317">3</span><span class="sxs-lookup"><span data-stu-id="f7990-317">3</span></span>|<span data-ttu-id="f7990-318">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-318">✔</span></span>|<span data-ttu-id="f7990-319">ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-319">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="f7990-320">これらのオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="f7990-320">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="f7990-321">ブール値</span><span class="sxs-lookup"><span data-stu-id="f7990-321">boolean</span></span>|||<span data-ttu-id="f7990-322">ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。</span><span class="sxs-lookup"><span data-stu-id="f7990-322">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="f7990-323">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="f7990-323">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="f7990-324">ブール値</span><span class="sxs-lookup"><span data-stu-id="f7990-324">boolean</span></span>|||<span data-ttu-id="f7990-325">ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="f7990-325">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="f7990-326">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="f7990-326">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="f7990-327">ブール値</span><span class="sxs-lookup"><span data-stu-id="f7990-327">boolean</span></span>|||<span data-ttu-id="f7990-328">パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="f7990-328">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="f7990-329">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="f7990-329">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="f7990-330">ブール値</span><span class="sxs-lookup"><span data-stu-id="f7990-330">boolean</span></span>|||<span data-ttu-id="f7990-331">ボットがオーディオ通話をサポートする場所を示す値。</span><span class="sxs-lookup"><span data-stu-id="f7990-331">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="f7990-332">**重要**: このプロパティは現在実験的です。</span><span class="sxs-lookup"><span data-stu-id="f7990-332">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="f7990-333">実験的なプロパティは完全ではない可能性があります。また、完全に利用可能になる前に変更が加わる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-333">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="f7990-334">これはテストと探索の目的でのみ提供され、実稼働アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="f7990-334">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="f7990-335">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="f7990-335">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="f7990-336">ブール値</span><span class="sxs-lookup"><span data-stu-id="f7990-336">boolean</span></span>|||<span data-ttu-id="f7990-337">ボットがビデオ通話をサポートする場所を示す値。</span><span class="sxs-lookup"><span data-stu-id="f7990-337">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="f7990-338">**重要**: このプロパティは現在実験的です。</span><span class="sxs-lookup"><span data-stu-id="f7990-338">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="f7990-339">実験的なプロパティは完全ではない可能性があります。また、完全に利用可能になる前に変更が加わる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-339">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="f7990-340">これはテストと探索の目的でのみ提供され、実稼働アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="f7990-340">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="f7990-341">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="f7990-341">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="f7990-342">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="f7990-342">bots.commandLists</span></span>

<span data-ttu-id="f7990-343">ボットがユーザーに推奨できるコマンドのオプションの一覧。</span><span class="sxs-lookup"><span data-stu-id="f7990-343">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="f7990-344">オブジェクトは、型のすべての要素を持つ配列 (最大 2 つの要素) です。ボットがサポートするスコープごとに個別のコマンド リストを `object` 定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-344">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="f7990-345">詳細については [、「ボット メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7990-345">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="f7990-346">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-346">Name</span></span>| <span data-ttu-id="f7990-347">型</span><span class="sxs-lookup"><span data-stu-id="f7990-347">Type</span></span>| <span data-ttu-id="f7990-348">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-348">Maximum size</span></span> | <span data-ttu-id="f7990-349">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-349">Required</span></span> | <span data-ttu-id="f7990-350">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-350">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="f7990-351">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-351">array of enums</span></span>|<span data-ttu-id="f7990-352">3</span><span class="sxs-lookup"><span data-stu-id="f7990-352">3</span></span>|<span data-ttu-id="f7990-353">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-353">✔</span></span>|<span data-ttu-id="f7990-354">コマンド リストが有効なスコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-354">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="f7990-355">`team`、`personal`、`groupchat` の中から選択できます。</span><span class="sxs-lookup"><span data-stu-id="f7990-355">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="f7990-356">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="f7990-356">array of objects</span></span>|<span data-ttu-id="f7990-357">10</span><span class="sxs-lookup"><span data-stu-id="f7990-357">10</span></span>|<span data-ttu-id="f7990-358">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-358">✔</span></span>|<span data-ttu-id="f7990-359">ボットがサポートするコマンドの配列:</span><span class="sxs-lookup"><span data-stu-id="f7990-359">An array of commands the bot supports:</span></span><br><span data-ttu-id="f7990-360">`title`: ボット コマンドの名前 (文字列、32)</span><span class="sxs-lookup"><span data-stu-id="f7990-360">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="f7990-361">`description`: コマンドの構文およびその構文の引数
の簡単な説明または例 (文字列、128)</span><span class="sxs-lookup"><span data-stu-id="f7990-361">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="f7990-362">bots.commandLists.command</span><span class="sxs-lookup"><span data-stu-id="f7990-362">bots.commandLists.commands</span></span>

|<span data-ttu-id="f7990-363">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-363">Name</span></span>| <span data-ttu-id="f7990-364">型</span><span class="sxs-lookup"><span data-stu-id="f7990-364">Type</span></span>| <span data-ttu-id="f7990-365">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-365">Maximum size</span></span> | <span data-ttu-id="f7990-366">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-366">Required</span></span> | <span data-ttu-id="f7990-367">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-367">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="f7990-368">title</span><span class="sxs-lookup"><span data-stu-id="f7990-368">title</span></span>|<span data-ttu-id="f7990-369">string</span><span class="sxs-lookup"><span data-stu-id="f7990-369">string</span></span>|<span data-ttu-id="f7990-370">12 </span><span class="sxs-lookup"><span data-stu-id="f7990-370">12</span></span>|<span data-ttu-id="f7990-371">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-371">✔</span></span>|<span data-ttu-id="f7990-372">ボット コマンド名</span><span class="sxs-lookup"><span data-stu-id="f7990-372">The bot command name</span></span>|
|<span data-ttu-id="f7990-373">description</span><span class="sxs-lookup"><span data-stu-id="f7990-373">description</span></span>|<span data-ttu-id="f7990-374">string</span><span class="sxs-lookup"><span data-stu-id="f7990-374">string</span></span>|<span data-ttu-id="f7990-375">128 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-375">128 characters</span></span>|<span data-ttu-id="f7990-376">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-376">✔</span></span>|<span data-ttu-id="f7990-377">単純なテキストの説明、またはコマンド構文とその引数の例。</span><span class="sxs-lookup"><span data-stu-id="f7990-377">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="f7990-378">コネクタ</span><span class="sxs-lookup"><span data-stu-id="f7990-378">connectors</span></span>

<span data-ttu-id="f7990-379">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="f7990-379">**Optional** — array</span></span>

<span data-ttu-id="f7990-380">ブロック `connectors` は、アプリOffice 365 コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="f7990-380">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="f7990-381">オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="f7990-381">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="f7990-382">このブロックは、Connector を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="f7990-382">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="f7990-383">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-383">Name</span></span>| <span data-ttu-id="f7990-384">型</span><span class="sxs-lookup"><span data-stu-id="f7990-384">Type</span></span>| <span data-ttu-id="f7990-385">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-385">Maximum size</span></span> | <span data-ttu-id="f7990-386">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-386">Required</span></span> | <span data-ttu-id="f7990-387">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-387">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="f7990-388">string</span><span class="sxs-lookup"><span data-stu-id="f7990-388">string</span></span>|<span data-ttu-id="f7990-389">2048 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-389">2048 characters</span></span>|<span data-ttu-id="f7990-390">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-390">✔</span></span>|<span data-ttu-id="f7990-391">コネクタ https:// する際に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-391">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="f7990-392">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-392">array of enums</span></span>|<span data-ttu-id="f7990-393">1</span><span class="sxs-lookup"><span data-stu-id="f7990-393">1</span></span>|<span data-ttu-id="f7990-394">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-394">✔</span></span>|<span data-ttu-id="f7990-395">Connector がチャネルのコンテキストでエクスペリエンスを提供するかどうか、または個々のユーザー () にスコープを設定したエクスペリエンスを提供するかどうかを `team` 指定します `personal` 。</span><span class="sxs-lookup"><span data-stu-id="f7990-395">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="f7990-396">現在、スコープ `team` だけがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f7990-396">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="f7990-397">string</span><span class="sxs-lookup"><span data-stu-id="f7990-397">string</span></span>|<span data-ttu-id="f7990-398">64 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-398">64 characters</span></span>|<span data-ttu-id="f7990-399">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-399">✔</span></span>|<span data-ttu-id="f7990-400">コネクタ開発者ダッシュボードの ID に一致するコネクタの一 [意の識別子](https://aka.ms/connectorsdashboard)です。</span><span class="sxs-lookup"><span data-stu-id="f7990-400">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="f7990-401">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="f7990-401">composeExtensions</span></span>

<span data-ttu-id="f7990-402">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="f7990-402">**Optional** — array</span></span>

<span data-ttu-id="f7990-403">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="f7990-403">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="f7990-404">機能の名前は、2017 年 11 月に "作成拡張機能" から "メッセージング拡張機能" に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は変わりません。</span><span class="sxs-lookup"><span data-stu-id="f7990-404">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="f7990-405">アイテムは、型のすべての要素を持つ配列 (最大 1 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="f7990-405">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="f7990-406">このブロックは、メッセージング拡張機能を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="f7990-406">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="f7990-407">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-407">Name</span></span>| <span data-ttu-id="f7990-408">型</span><span class="sxs-lookup"><span data-stu-id="f7990-408">Type</span></span> | <span data-ttu-id="f7990-409">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-409">Maximum Size</span></span> | <span data-ttu-id="f7990-410">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-410">Required</span></span> | <span data-ttu-id="f7990-411">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-411">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="f7990-412">string</span><span class="sxs-lookup"><span data-stu-id="f7990-412">string</span></span>|<span data-ttu-id="f7990-413">64</span><span class="sxs-lookup"><span data-stu-id="f7990-413">64</span></span>|<span data-ttu-id="f7990-414">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-414">✔</span></span>|<span data-ttu-id="f7990-415">ボット フレームワークに登録されているメッセージング拡張機能をバックするボットの一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="f7990-415">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="f7990-416">これは、アプリ ID 全体と同じ可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-416">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="f7990-417">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="f7990-417">array of objects</span></span>|<span data-ttu-id="f7990-418">10</span><span class="sxs-lookup"><span data-stu-id="f7990-418">10</span></span>|<span data-ttu-id="f7990-419">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-419">✔</span></span>|<span data-ttu-id="f7990-420">メッセージング拡張機能がサポートするコマンドの配列</span><span class="sxs-lookup"><span data-stu-id="f7990-420">Array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="f7990-421">ブール値</span><span class="sxs-lookup"><span data-stu-id="f7990-421">boolean</span></span>|||<span data-ttu-id="f7990-422">メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="f7990-422">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="f7990-423">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="f7990-423">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="f7990-424">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="f7990-424">array of Objects</span></span>|<span data-ttu-id="f7990-425">5</span><span class="sxs-lookup"><span data-stu-id="f7990-425">5</span></span>||<span data-ttu-id="f7990-426">特定の条件が満たされた場合にアプリを呼び出すことができるハンドラーの一覧。</span><span class="sxs-lookup"><span data-stu-id="f7990-426">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="f7990-427">string</span><span class="sxs-lookup"><span data-stu-id="f7990-427">string</span></span>|||<span data-ttu-id="f7990-428">メッセージ ハンドラーの種類。</span><span class="sxs-lookup"><span data-stu-id="f7990-428">The type of message handler.</span></span> <span data-ttu-id="f7990-429">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-429">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="f7990-430">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-430">array of Strings</span></span>|||<span data-ttu-id="f7990-431">リンク メッセージ ハンドラーが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="f7990-431">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="f7990-432">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="f7990-432">composeExtensions.commands</span></span>

<span data-ttu-id="f7990-433">メッセージング拡張機能は、1 つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-433">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="f7990-434">各コマンドは、UI ベースのエントリ ポイントからの潜在的な相互作用として Microsoft Teams に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f7990-434">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="f7990-435">最大 10 のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="f7990-435">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="f7990-436">各コマンド 項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="f7990-436">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="f7990-437">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-437">Name</span></span>| <span data-ttu-id="f7990-438">型</span><span class="sxs-lookup"><span data-stu-id="f7990-438">Type</span></span>| <span data-ttu-id="f7990-439">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-439">Maximum size</span></span> | <span data-ttu-id="f7990-440">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-440">Required</span></span> | <span data-ttu-id="f7990-441">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-441">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="f7990-442">string</span><span class="sxs-lookup"><span data-stu-id="f7990-442">string</span></span>|<span data-ttu-id="f7990-443">64 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-443">64 characters</span></span>|<span data-ttu-id="f7990-444">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-444">✔</span></span>|<span data-ttu-id="f7990-445">コマンドの ID。</span><span class="sxs-lookup"><span data-stu-id="f7990-445">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="f7990-446">string</span><span class="sxs-lookup"><span data-stu-id="f7990-446">string</span></span>|<span data-ttu-id="f7990-447">32 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-447">32 characters</span></span>|<span data-ttu-id="f7990-448">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-448">✔</span></span>|<span data-ttu-id="f7990-449">ユーザーフレンドリーなコマンド名。</span><span class="sxs-lookup"><span data-stu-id="f7990-449">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="f7990-450">string</span><span class="sxs-lookup"><span data-stu-id="f7990-450">string</span></span>|<span data-ttu-id="f7990-451">64 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-451">64 characters</span></span>||<span data-ttu-id="f7990-452">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="f7990-452">Type of the command.</span></span> <span data-ttu-id="f7990-453">または `query` の 1 `action` つ。</span><span class="sxs-lookup"><span data-stu-id="f7990-453">One of `query` or `action`.</span></span> <span data-ttu-id="f7990-454">既定: **クエリ** です。</span><span class="sxs-lookup"><span data-stu-id="f7990-454">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="f7990-455">string</span><span class="sxs-lookup"><span data-stu-id="f7990-455">string</span></span>|<span data-ttu-id="f7990-456">128 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-456">128 characters</span></span>||<span data-ttu-id="f7990-457">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="f7990-457">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="f7990-458">ブール値</span><span class="sxs-lookup"><span data-stu-id="f7990-458">boolean</span></span>|||<span data-ttu-id="f7990-459">ブール値は、コマンドがパラメーターを使用して最初に実行されるかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="f7990-459">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="f7990-460">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="f7990-460">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="f7990-461">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-461">array of Strings</span></span>|<span data-ttu-id="f7990-462">3</span><span class="sxs-lookup"><span data-stu-id="f7990-462">3</span></span>||<span data-ttu-id="f7990-463">メッセージ拡張機能の呼び出し先を定義します。</span><span class="sxs-lookup"><span data-stu-id="f7990-463">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="f7990-464">`compose`、 の任意の `commandBox` 組み合 `message` わせ。</span><span class="sxs-lookup"><span data-stu-id="f7990-464">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="f7990-465">既定値は `["compose","commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="f7990-465">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="f7990-466">ブール値</span><span class="sxs-lookup"><span data-stu-id="f7990-466">boolean</span></span>|||<span data-ttu-id="f7990-467">タスク モジュールを動的にフェッチする必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="f7990-467">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="f7990-468">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="f7990-468">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="f7990-469">object</span><span class="sxs-lookup"><span data-stu-id="f7990-469">object</span></span>|||<span data-ttu-id="f7990-470">メッセージング拡張機能コマンドを使用する場合に事前読み込みするタスク モジュールを指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-470">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="f7990-471">string</span><span class="sxs-lookup"><span data-stu-id="f7990-471">string</span></span>|<span data-ttu-id="f7990-472">64 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-472">64 characters</span></span>||<span data-ttu-id="f7990-473">最初のダイアログ タイトル。</span><span class="sxs-lookup"><span data-stu-id="f7990-473">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="f7990-474">string</span><span class="sxs-lookup"><span data-stu-id="f7990-474">string</span></span>|||<span data-ttu-id="f7990-475">ダイアログの幅 - ピクセル単位の数値または既定のレイアウト ('large'、'medium'、または 'small' など)。</span><span class="sxs-lookup"><span data-stu-id="f7990-475">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="f7990-476">string</span><span class="sxs-lookup"><span data-stu-id="f7990-476">string</span></span>|||<span data-ttu-id="f7990-477">ダイアログの高さ - ピクセル単位の数値、または 'large'、'medium'、または 'small' などの既定のレイアウト。</span><span class="sxs-lookup"><span data-stu-id="f7990-477">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="f7990-478">string</span><span class="sxs-lookup"><span data-stu-id="f7990-478">string</span></span>|||<span data-ttu-id="f7990-479">初期 Webview URL。</span><span class="sxs-lookup"><span data-stu-id="f7990-479">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="f7990-480">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="f7990-480">array of object</span></span>|<span data-ttu-id="f7990-481">5 つのアイテム</span><span class="sxs-lookup"><span data-stu-id="f7990-481">5 items</span></span>|<span data-ttu-id="f7990-482">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-482">✔</span></span>|<span data-ttu-id="f7990-483">コマンドが受け取るパラメーターの一覧。</span><span class="sxs-lookup"><span data-stu-id="f7990-483">The list of parameters the command takes.</span></span> <span data-ttu-id="f7990-484">最小: 1;最大: 5。</span><span class="sxs-lookup"><span data-stu-id="f7990-484">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="f7990-485">string</span><span class="sxs-lookup"><span data-stu-id="f7990-485">string</span></span>|<span data-ttu-id="f7990-486">64 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-486">64 characters</span></span>|<span data-ttu-id="f7990-487">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-487">✔</span></span>|<span data-ttu-id="f7990-488">クライアントに表示されるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="f7990-488">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="f7990-489">これは、ユーザー要求に含まれます。</span><span class="sxs-lookup"><span data-stu-id="f7990-489">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="f7990-490">string</span><span class="sxs-lookup"><span data-stu-id="f7990-490">string</span></span>|<span data-ttu-id="f7990-491">32 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-491">32 characters</span></span>|<span data-ttu-id="f7990-492">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-492">✔</span></span>|<span data-ttu-id="f7990-493">パラメーターのユーザーフレンドリーなタイトル。</span><span class="sxs-lookup"><span data-stu-id="f7990-493">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="f7990-494">string</span><span class="sxs-lookup"><span data-stu-id="f7990-494">string</span></span>|<span data-ttu-id="f7990-495">128 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-495">128 characters</span></span>||<span data-ttu-id="f7990-496">このパラメーターの目的を説明するユーザーフレンドリーな文字列。</span><span class="sxs-lookup"><span data-stu-id="f7990-496">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="f7990-497">string</span><span class="sxs-lookup"><span data-stu-id="f7990-497">string</span></span>|<span data-ttu-id="f7990-498">512 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-498">512 characters</span></span>||<span data-ttu-id="f7990-499">パラメーターの初期値。</span><span class="sxs-lookup"><span data-stu-id="f7990-499">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="f7990-500">string</span><span class="sxs-lookup"><span data-stu-id="f7990-500">string</span></span>|<span data-ttu-id="f7990-501">128 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-501">128 characters</span></span>||<span data-ttu-id="f7990-502">タスク モジュールに表示されるコントロールの種類を定義します `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="f7990-502">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="f7990-503">の 1 `text, textarea, number, date, time, toggle, choiceset` つ。</span><span class="sxs-lookup"><span data-stu-id="f7990-503">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="f7990-504">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="f7990-504">array of objects</span></span>|<span data-ttu-id="f7990-505">10 アイテム</span><span class="sxs-lookup"><span data-stu-id="f7990-505">10 items</span></span>||<span data-ttu-id="f7990-506">の選択肢 `choiceset` オプションです。</span><span class="sxs-lookup"><span data-stu-id="f7990-506">The choice options for the`choiceset`.</span></span> <span data-ttu-id="f7990-507">の場合にのみ `parameter.inputType` 使用します `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="f7990-507">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="f7990-508">string</span><span class="sxs-lookup"><span data-stu-id="f7990-508">string</span></span>|<span data-ttu-id="f7990-509">128 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-509">128 characters</span></span>|<span data-ttu-id="f7990-510">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-510">✔</span></span>|<span data-ttu-id="f7990-511">選択したタイトル。</span><span class="sxs-lookup"><span data-stu-id="f7990-511">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="f7990-512">string</span><span class="sxs-lookup"><span data-stu-id="f7990-512">string</span></span>|<span data-ttu-id="f7990-513">512 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-513">512 characters</span></span>|<span data-ttu-id="f7990-514">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-514">✔</span></span>|<span data-ttu-id="f7990-515">Value of the choice.</span><span class="sxs-lookup"><span data-stu-id="f7990-515">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="f7990-516">permissions</span><span class="sxs-lookup"><span data-stu-id="f7990-516">permissions</span></span>

<span data-ttu-id="f7990-517">**省略** 可能 - 文字列の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-517">**Optional** — array of strings</span></span>

<span data-ttu-id="f7990-518">アプリが要求するアクセス許可を指定する配列で、エンド ユーザーは拡張機能の実行 `string` 方法を知る必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-518">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="f7990-519">次のオプションは、非排他的です。</span><span class="sxs-lookup"><span data-stu-id="f7990-519">The following options are non-exclusive:</span></span>

* <span data-ttu-id="f7990-520">`identity`&emsp;ユーザー ID 情報が必要</span><span class="sxs-lookup"><span data-stu-id="f7990-520">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="f7990-521">`messageTeamMembers`&emsp;チーム メンバーに直接メッセージを送信するためのアクセス許可が必要</span><span class="sxs-lookup"><span data-stu-id="f7990-521">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="f7990-522">アプリの更新中にこれらのアクセス許可を変更すると、更新されたアプリの実行後にユーザーが同意プロセスを繰り返します。</span><span class="sxs-lookup"><span data-stu-id="f7990-522">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="f7990-523">詳細については [、「アプリの更新」](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f7990-523">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="f7990-524">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="f7990-524">devicePermissions</span></span>

<span data-ttu-id="f7990-525">**省略** 可能 - 文字列の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-525">**Optional** — array of strings</span></span>

<span data-ttu-id="f7990-526">アプリがアクセスを要求するユーザーのデバイス上のネイティブ機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="f7990-526">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="f7990-527">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="f7990-527">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="f7990-528">validDomains</span><span class="sxs-lookup"><span data-stu-id="f7990-528">validDomains</span></span>

<span data-ttu-id="f7990-529">**省略** 可能です ( **必須の場合** は除く)</span><span class="sxs-lookup"><span data-stu-id="f7990-529">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="f7990-530">アプリが Teams クライアント内で読み込むと予想される Web サイトの有効なドメインの一覧。</span><span class="sxs-lookup"><span data-stu-id="f7990-530">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="f7990-531">ドメインの一覧には、ワイルドカード (たとえば) を含めできます `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="f7990-531">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="f7990-532">これは、ドメインの 1 つのセグメントと完全に一致します。一致する必要がある場合は、 `a.b.example.com` を使用します `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="f7990-532">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="f7990-533">タブ構成またはコンテンツ UI で、タブ構成に使用するドメイン以外のドメインに移動する必要がある場合は、ここでそのドメインを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-533">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="f7990-534">サポート **する** ID プロバイダーのドメインをアプリに含める必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f7990-534">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="f7990-535">たとえば、Google ID を使用して認証を行う場合は、accounts.google.com にリダイレクトする必要があります。ただし、accounts.google.com を含 accounts.google.com 必要があります `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="f7990-535">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="f7990-536">自分の sharepoint URL がうまく機能する必要がある Teams アプリには、有効なドメイン リストに "{teamsitedomain}" が含まれます。</span><span class="sxs-lookup"><span data-stu-id="f7990-536">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7990-537">直接またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しません。</span><span class="sxs-lookup"><span data-stu-id="f7990-537">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="f7990-538">たとえば、 `yourapp.onmicrosoft.com` 有効ですが、 `*.onmicrosoft.com` 無効です。</span><span class="sxs-lookup"><span data-stu-id="f7990-538">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="f7990-539">オブジェクトは、型のすべての要素を持つ配列です `string` 。</span><span class="sxs-lookup"><span data-stu-id="f7990-539">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="f7990-540">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="f7990-540">webApplicationInfo</span></span>

<span data-ttu-id="f7990-541">**省略可能** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="f7990-541">**Optional** — object</span></span>

<span data-ttu-id="f7990-542">ユーザーがアプリにシームレスにサインインするのに役立つ Azure Active Directory (AAD) アプリ ID と Microsoft Graph 情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="f7990-542">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="f7990-543">アプリが AAD に登録されている場合は、管理者が Teams 管理センターでアクセス許可を簡単に確認し、同意を与えできるよう、アプリ ID を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-543">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="f7990-544">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-544">Name</span></span>| <span data-ttu-id="f7990-545">型</span><span class="sxs-lookup"><span data-stu-id="f7990-545">Type</span></span>| <span data-ttu-id="f7990-546">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-546">Maximum size</span></span> | <span data-ttu-id="f7990-547">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-547">Required</span></span> | <span data-ttu-id="f7990-548">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-548">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="f7990-549">string</span><span class="sxs-lookup"><span data-stu-id="f7990-549">string</span></span>|<span data-ttu-id="f7990-550">36 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-550">36 characters</span></span>|<span data-ttu-id="f7990-551">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-551">✔</span></span>|<span data-ttu-id="f7990-552">アプリの AAD アプリケーション ID。</span><span class="sxs-lookup"><span data-stu-id="f7990-552">AAD application id of the app.</span></span> <span data-ttu-id="f7990-553">この ID は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="f7990-553">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="f7990-554">string</span><span class="sxs-lookup"><span data-stu-id="f7990-554">string</span></span>|<span data-ttu-id="f7990-555">2048 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-555">2048 characters</span></span>|<span data-ttu-id="f7990-556">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-556">✔</span></span>|<span data-ttu-id="f7990-557">SSO の認証トークンを取得するためのアプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="f7990-557">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="f7990-558">**注:** SSO を使用していない場合は、エラー応答を回避するために、このフィールドにダミーの文字列値をアプリ マニフェストに https://notapplicable 入力してください。</span><span class="sxs-lookup"><span data-stu-id="f7990-558">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="f7990-559">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="f7990-559">array of strings</span></span>|<span data-ttu-id="f7990-560">128 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-560">128 characters</span></span>||<span data-ttu-id="f7990-561">詳細なリソース [固有の同意を指定します](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="f7990-561">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="f7990-562">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="f7990-562">showLoadingIndicator</span></span>

<span data-ttu-id="f7990-563">**省略** 可能 - ブール型 (Boolean)</span><span class="sxs-lookup"><span data-stu-id="f7990-563">**Optional** — boolean</span></span>

<span data-ttu-id="f7990-564">アプリまたはタブの読み込み時に読み込みインジケーターを表示するかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="f7990-564">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="f7990-565">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="f7990-565">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="f7990-566">アプリ マニフェストで true を選択した場合、ページを正しく読み込むには、「ネイティブ読み込みインジケーター ドキュメントを表示する」の説明に従って、タブとタスク モジュールのコンテンツ ページを `showLoadingIndicator` [変更](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) します。</span><span class="sxs-lookup"><span data-stu-id="f7990-566">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="f7990-567">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="f7990-567">isFullScreen</span></span>

 <span data-ttu-id="f7990-568">**省略** 可能 - ブール型 (Boolean)</span><span class="sxs-lookup"><span data-stu-id="f7990-568">**Optional** — boolean</span></span>

<span data-ttu-id="f7990-569">タブ ヘッダー バーの付きまたはなしで個人用アプリがレンダリングされる場所を示します。</span><span class="sxs-lookup"><span data-stu-id="f7990-569">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="f7990-570">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="f7990-570">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="f7990-571">activities</span><span class="sxs-lookup"><span data-stu-id="f7990-571">activities</span></span>

<span data-ttu-id="f7990-572">**省略可能** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="f7990-572">**Optional** — object</span></span>

<span data-ttu-id="f7990-573">アプリがユーザー アクティビティ フィードの投稿に使用するプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="f7990-573">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="f7990-574">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-574">Name</span></span>| <span data-ttu-id="f7990-575">型</span><span class="sxs-lookup"><span data-stu-id="f7990-575">Type</span></span>| <span data-ttu-id="f7990-576">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-576">Maximum size</span></span> | <span data-ttu-id="f7990-577">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-577">Required</span></span> | <span data-ttu-id="f7990-578">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-578">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="f7990-579">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="f7990-579">array of Objects</span></span>|<span data-ttu-id="f7990-580">128 アイテム</span><span class="sxs-lookup"><span data-stu-id="f7990-580">128 items</span></span>| | <span data-ttu-id="f7990-581">アプリがユーザーアクティビティ フィードに投稿できるアクティビティの種類を指定します。</span><span class="sxs-lookup"><span data-stu-id="f7990-581">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="f7990-582">activity.activityTypes</span><span class="sxs-lookup"><span data-stu-id="f7990-582">activities.activityTypes</span></span>

|<span data-ttu-id="f7990-583">名前</span><span class="sxs-lookup"><span data-stu-id="f7990-583">Name</span></span>| <span data-ttu-id="f7990-584">型</span><span class="sxs-lookup"><span data-stu-id="f7990-584">Type</span></span>| <span data-ttu-id="f7990-585">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="f7990-585">Maximum size</span></span> | <span data-ttu-id="f7990-586">必須</span><span class="sxs-lookup"><span data-stu-id="f7990-586">Required</span></span> | <span data-ttu-id="f7990-587">説明</span><span class="sxs-lookup"><span data-stu-id="f7990-587">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="f7990-588">string</span><span class="sxs-lookup"><span data-stu-id="f7990-588">string</span></span>|<span data-ttu-id="f7990-589">32 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-589">32 characters</span></span>|<span data-ttu-id="f7990-590">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-590">✔</span></span>|<span data-ttu-id="f7990-591">通知の種類。</span><span class="sxs-lookup"><span data-stu-id="f7990-591">The notification type.</span></span> <span data-ttu-id="f7990-592">*以下を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="f7990-592">*See below*.</span></span>|
|`description`|<span data-ttu-id="f7990-593">string</span><span class="sxs-lookup"><span data-stu-id="f7990-593">string</span></span>|<span data-ttu-id="f7990-594">128 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-594">128 characters</span></span>|<span data-ttu-id="f7990-595">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-595">✔</span></span>|<span data-ttu-id="f7990-596">通知の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="f7990-596">A brief description of the notification.</span></span> <span data-ttu-id="f7990-597">*以下を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="f7990-597">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="f7990-598">string</span><span class="sxs-lookup"><span data-stu-id="f7990-598">string</span></span>|<span data-ttu-id="f7990-599">128 文字</span><span class="sxs-lookup"><span data-stu-id="f7990-599">128 characters</span></span>|<span data-ttu-id="f7990-600">✔</span><span class="sxs-lookup"><span data-stu-id="f7990-600">✔</span></span>|<span data-ttu-id="f7990-601">例: "{actor} が作成したタスク {taskId} for you"</span><span class="sxs-lookup"><span data-stu-id="f7990-601">Ex: "{actor} created task {taskId} for you"</span></span>|

```json
{
   "activities":{
      "activityTypes":[
         {
            "type":"taskCreated",
            "description":"Task Created Activity",
            "templateText":"{actor} created task {taskId} for you"
         },
         {
            "type":"teamMention",
            "description":"Team Mention Activity",
            "templateText":"{actor} mentioned team"
         },
         {
            "type":"channelMention",
            "description":"Channel Mention Activity",
            "templateText":"{actor} mentioned channel"
         },
         {
            "type":"userMention",
            "description":"Personal Mention Activity",
            "templateText":"{actor} mentioned user"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"creatorTaskCreated",
            "description":"Created Task Created",
            "templateText":"The Creator created task {taskId} for you"
         }
      ]
   }
}
```

***
>
>
