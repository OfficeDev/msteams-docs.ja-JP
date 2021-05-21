---
title: マニフェスト スキーマ参照
description: アプリケーションのマニフェスト スキーマについてMicrosoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: teams マニフェスト スキーマ
ms.openlocfilehash: 6c7cd02480f78d19aed269b5d78d0c6f470621d2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566447"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="d7787-104">リファレンス: マニフェスト スキーマのMicrosoft Teams</span><span class="sxs-lookup"><span data-stu-id="d7787-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="d7787-105">このTeamsマニフェストは、アプリが製品に統合する方法Microsoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="d7787-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="d7787-106">マニフェストは、 でホストされるスキーマに準拠している必要があります [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="d7787-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="d7787-107">以前のバージョン 1.0、1.1,..., 1.6 もサポートされています (URL で "v1.x" を使用)。</span><span class="sxs-lookup"><span data-stu-id="d7787-107">Previous versions 1.0, 1.1,..., 1.6, and so on are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="d7787-108">次のスキーマ サンプルは、すべての機能拡張オプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="d7787-108">The following schema sample shows all extensibility options:</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="d7787-109">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="d7787-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json",
  "manifestVersion": "1.10",
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
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  },
  "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "websiteUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ]              
}
```

<span data-ttu-id="d7787-110">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="d7787-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="d7787-111">$schema</span><span class="sxs-lookup"><span data-stu-id="d7787-111">$schema</span></span>

<span data-ttu-id="d7787-112">省略可能ですが、推奨される — string</span><span class="sxs-lookup"><span data-stu-id="d7787-112">Optional, but recommended — string</span></span>

<span data-ttu-id="d7787-113">マニフェスト https:// JSON スキーマを参照する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="d7787-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="d7787-114">manifestVersion</span></span>

<span data-ttu-id="d7787-115">**必須** — 文字列</span><span class="sxs-lookup"><span data-stu-id="d7787-115">**Required** — string</span></span>

<span data-ttu-id="d7787-116">このマニフェストが使用しているマニフェスト スキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="d7787-116">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="d7787-117">1.10 である必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-117">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="d7787-118">version</span><span class="sxs-lookup"><span data-stu-id="d7787-118">version</span></span>

<span data-ttu-id="d7787-119">**必須** — 文字列</span><span class="sxs-lookup"><span data-stu-id="d7787-119">**Required** — string</span></span>

<span data-ttu-id="d7787-120">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="d7787-120">The version of a specific app.</span></span> <span data-ttu-id="d7787-121">マニフェストで何かを更新する場合は、バージョンもインクリメントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-121">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="d7787-122">これにより、新しいマニフェストがインストールされた場合、既存のマニフェストが上書きされ、ユーザーは新しい機能を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="d7787-122">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="d7787-123">このアプリがストアに送信された場合は、新しいマニフェストを再送信して再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-123">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="d7787-124">アプリユーザーは、マニフェストが承認された後、数時間以内に新しい更新されたマニフェストを自動的に受信します。</span><span class="sxs-lookup"><span data-stu-id="d7787-124">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="d7787-125">アプリでアクセス許可の要求が変更された場合、ユーザーはアプリのアップグレードと再同意を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d7787-125">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="d7787-126">このバージョンの文字列は [、semver](http://semver.org/) 標準 (MAJOR) に従う必要があります。MINOR。PATCH)。</span><span class="sxs-lookup"><span data-stu-id="d7787-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="d7787-127">id</span><span class="sxs-lookup"><span data-stu-id="d7787-127">id</span></span>

<span data-ttu-id="d7787-128">**必須** — Microsoft アプリ ID</span><span class="sxs-lookup"><span data-stu-id="d7787-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="d7787-129">ID は、アプリの Microsoft が生成する一意の識別子です。</span><span class="sxs-lookup"><span data-stu-id="d7787-129">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="d7787-130">ボットが Microsoft で既にサインインしている場合は、Microsoft Bot Frameworkタブの Web アプリを使用して登録されている場合は、ID を持っています。</span><span class="sxs-lookup"><span data-stu-id="d7787-130">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="d7787-131">ここに ID を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-131">You must enter the ID here.</span></span> <span data-ttu-id="d7787-132">それ以外の場合は、Microsoft アプリケーション登録ポータルで新しい ID [を生成する必要があります](https://aka.ms/appregistrations)。</span><span class="sxs-lookup"><span data-stu-id="d7787-132">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="d7787-133">ボットを追加する場合は、同じ ID を使用します。</span><span class="sxs-lookup"><span data-stu-id="d7787-133">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="d7787-134">AppSource で既存のアプリに更新プログラムを提出する場合は、マニフェスト内の ID を変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="d7787-134">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="d7787-135">developer</span><span class="sxs-lookup"><span data-stu-id="d7787-135">developer</span></span>

<span data-ttu-id="d7787-136">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="d7787-136">**Required** — object</span></span>

<span data-ttu-id="d7787-137">会社に関する情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-137">Specifies information about your company.</span></span> <span data-ttu-id="d7787-138">アプリがストアに送信Teams、これらの値はストア登録情報の情報と一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-138">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="d7787-139">詳細については、「ストア発行ガイドラインTeams[を参照してください](~/concepts/deploy-and-publish/appsource/publish.md)。</span><span class="sxs-lookup"><span data-stu-id="d7787-139">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="d7787-140">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-140">Name</span></span>| <span data-ttu-id="d7787-141">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-141">Maximum size</span></span> | <span data-ttu-id="d7787-142">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-142">Required</span></span> | <span data-ttu-id="d7787-143">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="d7787-144">32 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-144">32 characters</span></span>|<span data-ttu-id="d7787-145">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-145">✔</span></span>|<span data-ttu-id="d7787-146">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="d7787-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="d7787-147">2048 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-147">2048 characters</span></span>|<span data-ttu-id="d7787-148">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-148">✔</span></span>|<span data-ttu-id="d7787-149">開発者 https:// WEB サイトの URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="d7787-150">このリンクは、ユーザーを会社または製品固有のランディング ページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-150">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="d7787-151">2048 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-151">2048 characters</span></span>|<span data-ttu-id="d7787-152">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-152">✔</span></span>|<span data-ttu-id="d7787-153">開発者 https:// のプライバシー ポリシーの URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="d7787-154">2048 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-154">2048 characters</span></span>|<span data-ttu-id="d7787-155">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-155">✔</span></span>|<span data-ttu-id="d7787-156">開発者 https:// の使用条件の URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="d7787-157">10 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-157">10 characters</span></span>| |<span data-ttu-id="d7787-158">**省略可能** アプリを構築するパートナー組織を識別する Microsoft パートナー ネットワーク ID。</span><span class="sxs-lookup"><span data-stu-id="d7787-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="d7787-159">name</span><span class="sxs-lookup"><span data-stu-id="d7787-159">name</span></span>

<span data-ttu-id="d7787-160">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="d7787-160">**Required** — object</span></span>

<span data-ttu-id="d7787-161">アプリ エクスペリエンスのユーザーに表示されるアプリ エクスペリエンスのTeamsします。</span><span class="sxs-lookup"><span data-stu-id="d7787-161">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="d7787-162">AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-162">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="d7787-163">の値と `short` 異 `full` なる値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-163">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="d7787-164">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-164">Name</span></span>| <span data-ttu-id="d7787-165">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-165">Maximum size</span></span> | <span data-ttu-id="d7787-166">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-166">Required</span></span> | <span data-ttu-id="d7787-167">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-167">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="d7787-168">30 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-168">30 characters</span></span>|<span data-ttu-id="d7787-169">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-169">✔</span></span>|<span data-ttu-id="d7787-170">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="d7787-170">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="d7787-171">100 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-171">100 characters</span></span>||<span data-ttu-id="d7787-172">完全なアプリ名が 30 文字を超える場合に使用されるアプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="d7787-172">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="d7787-173">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-173">description</span></span>

<span data-ttu-id="d7787-174">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="d7787-174">**Required** — object</span></span>

<span data-ttu-id="d7787-175">アプリをユーザーに説明します。</span><span class="sxs-lookup"><span data-stu-id="d7787-175">Describes your app to users.</span></span> <span data-ttu-id="d7787-176">AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-176">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="d7787-177">説明がエクスペリエンスを正確に説明し、潜在的な顧客がエクスペリエンスの内容を理解するのに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="d7787-177">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="d7787-178">外部アカウントを使用する必要がある場合は、完全な説明に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-178">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="d7787-179">の値と `short` 異 `full` なる値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-179">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="d7787-180">短い説明は、長い説明の中で繰り返し実行し、他のアプリ名を含めずに行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-180">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="d7787-181">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-181">Name</span></span>| <span data-ttu-id="d7787-182">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-182">Maximum size</span></span> | <span data-ttu-id="d7787-183">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-183">Required</span></span> | <span data-ttu-id="d7787-184">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-184">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="d7787-185">80 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-185">80 characters</span></span>|<span data-ttu-id="d7787-186">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-186">✔</span></span>|<span data-ttu-id="d7787-187">スペースが制限されている場合に使用されるアプリ エクスペリエンスの簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="d7787-187">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="d7787-188">4000 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-188">4000 characters</span></span>|<span data-ttu-id="d7787-189">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-189">✔</span></span>|<span data-ttu-id="d7787-190">アプリの完全な説明。</span><span class="sxs-lookup"><span data-stu-id="d7787-190">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="d7787-191">packageName</span><span class="sxs-lookup"><span data-stu-id="d7787-191">packageName</span></span>

<span data-ttu-id="d7787-192">**省略** 可能 — 文字列</span><span class="sxs-lookup"><span data-stu-id="d7787-192">**Optional** — string</span></span>

<span data-ttu-id="d7787-193">逆ドメイン表記のアプリの一意の識別子。たとえば、com.example.myapp などです。</span><span class="sxs-lookup"><span data-stu-id="d7787-193">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="d7787-194">最大長: 64 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-194">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="d7787-195">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="d7787-195">localizationInfo</span></span>

<span data-ttu-id="d7787-196">**省略可能** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="d7787-196">**Optional** — object</span></span>

<span data-ttu-id="d7787-197">既定の言語の指定と、追加の言語ファイルへのポインターを許可します。</span><span class="sxs-lookup"><span data-stu-id="d7787-197">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="d7787-198">詳細については、「ローカライズ」を [参照してください](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="d7787-198">For more information, see [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="d7787-199">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-199">Name</span></span>| <span data-ttu-id="d7787-200">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-200">Maximum size</span></span> | <span data-ttu-id="d7787-201">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-201">Required</span></span> | <span data-ttu-id="d7787-202">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-202">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="d7787-203">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-203">✔</span></span>|<span data-ttu-id="d7787-204">このトップ レベルのマニフェスト ファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="d7787-204">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="d7787-205">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="d7787-205">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="d7787-206">追加の言語変換を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="d7787-206">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="d7787-207">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-207">Name</span></span>| <span data-ttu-id="d7787-208">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-208">Maximum size</span></span> | <span data-ttu-id="d7787-209">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-209">Required</span></span> | <span data-ttu-id="d7787-210">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-210">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="d7787-211">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-211">✔</span></span>|<span data-ttu-id="d7787-212">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="d7787-212">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="d7787-213">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-213">✔</span></span>|<span data-ttu-id="d7787-214">翻訳された文字列を含む .json ファイルへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="d7787-214">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="d7787-215">アイコン</span><span class="sxs-lookup"><span data-stu-id="d7787-215">icons</span></span>

<span data-ttu-id="d7787-216">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="d7787-216">**Required** — object</span></span>

<span data-ttu-id="d7787-217">アプリ内で使用Teamsアイコン。</span><span class="sxs-lookup"><span data-stu-id="d7787-217">Icons used within the Teams app.</span></span> <span data-ttu-id="d7787-218">アイコン ファイルは、アップロード パッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-218">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="d7787-219">詳細については [、「アイコン](../../concepts/build-and-test/apps-package.md#app-icons) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d7787-219">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="d7787-220">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-220">Name</span></span>| <span data-ttu-id="d7787-221">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-221">Maximum size</span></span> | <span data-ttu-id="d7787-222">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-222">Required</span></span> | <span data-ttu-id="d7787-223">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="d7787-224">32 x 32 ピクセル</span><span class="sxs-lookup"><span data-stu-id="d7787-224">32 x 32 pixels</span></span>|<span data-ttu-id="d7787-225">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-225">✔</span></span>|<span data-ttu-id="d7787-226">透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="d7787-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="d7787-227">192 x 192 ピクセル</span><span class="sxs-lookup"><span data-stu-id="d7787-227">192 x 192 pixels</span></span>|<span data-ttu-id="d7787-228">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-228">✔</span></span>|<span data-ttu-id="d7787-229">フル カラーの 192x192 PNG アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="d7787-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="d7787-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="d7787-230">accentColor</span></span>

<span data-ttu-id="d7787-231">**省略** 可能 — HTML の 16 進カラー コード</span><span class="sxs-lookup"><span data-stu-id="d7787-231">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="d7787-232">アウトライン アイコンと組み合わせて、背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="d7787-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="d7787-233">値は、'#' で始まる有効な HTML カラー コードである必要があります `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="d7787-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="d7787-234">configurableTabs</span></span>

<span data-ttu-id="d7787-235">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="d7787-235">**Optional** — array</span></span>

<span data-ttu-id="d7787-236">アプリ エクスペリエンスに、追加する前に追加の構成が必要なチーム チャネル タブ エクスペリエンスがある場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="d7787-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="d7787-237">構成可能なタブは teams スコープでのみサポートされ、同じタブを複数回構成できます。</span><span class="sxs-lookup"><span data-stu-id="d7787-237">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="d7787-238">ただし、マニフェストで定義できるのは 1 回のみです。</span><span class="sxs-lookup"><span data-stu-id="d7787-238">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="d7787-239">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-239">Name</span></span>| <span data-ttu-id="d7787-240">型</span><span class="sxs-lookup"><span data-stu-id="d7787-240">Type</span></span>| <span data-ttu-id="d7787-241">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-241">Maximum size</span></span> | <span data-ttu-id="d7787-242">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-242">Required</span></span> | <span data-ttu-id="d7787-243">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-243">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="d7787-244">string</span><span class="sxs-lookup"><span data-stu-id="d7787-244">string</span></span>|<span data-ttu-id="d7787-245">2048 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-245">2048 characters</span></span>|<span data-ttu-id="d7787-246">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-246">✔</span></span>|<span data-ttu-id="d7787-247">タブ https:// する際に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-247">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="d7787-248">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-248">array of enums</span></span>|<span data-ttu-id="d7787-249">1</span><span class="sxs-lookup"><span data-stu-id="d7787-249">1</span></span>|<span data-ttu-id="d7787-250">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-250">✔</span></span>|<span data-ttu-id="d7787-251">現在、構成可能なタブは、スコープ `team` とスコープ `groupchat` のみをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d7787-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="d7787-252">boolean</span><span class="sxs-lookup"><span data-stu-id="d7787-252">boolean</span></span>|||<span data-ttu-id="d7787-253">作成後に、タブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="d7787-253">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="d7787-254">既定値: **true 。**</span><span class="sxs-lookup"><span data-stu-id="d7787-254">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="d7787-255">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-255">array of enums</span></span>|<span data-ttu-id="d7787-256">6</span><span class="sxs-lookup"><span data-stu-id="d7787-256">6</span></span>||<span data-ttu-id="d7787-257">タブが `contextItem` サポートされているスコープ [のセット](../../tabs/how-to/access-teams-context.md)です。</span><span class="sxs-lookup"><span data-stu-id="d7787-257">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="d7787-258">既定値: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="d7787-258">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="d7787-259">string</span><span class="sxs-lookup"><span data-stu-id="d7787-259">string</span></span>|<span data-ttu-id="d7787-260">2048</span><span class="sxs-lookup"><span data-stu-id="d7787-260">2048</span></span>||<span data-ttu-id="d7787-261">タブ プレビュー イメージへの相対ファイル パスを使用して、SharePoint。</span><span class="sxs-lookup"><span data-stu-id="d7787-261">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="d7787-262">サイズは 1024x768 です。</span><span class="sxs-lookup"><span data-stu-id="d7787-262">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="d7787-263">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-263">array of enums</span></span>|<span data-ttu-id="d7787-264">1</span><span class="sxs-lookup"><span data-stu-id="d7787-264">1</span></span>||<span data-ttu-id="d7787-265">タブを使用してタブを使用する方法をSharePoint。</span><span class="sxs-lookup"><span data-stu-id="d7787-265">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="d7787-266">オプションは `sharePointFullPage` 次のとおりです。 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="d7787-266">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="d7787-267">staticTabs</span><span class="sxs-lookup"><span data-stu-id="d7787-267">staticTabs</span></span>

<span data-ttu-id="d7787-268">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="d7787-268">**Optional** — array</span></span>

<span data-ttu-id="d7787-269">ユーザーが手動で追加せずに、既定で "ピン留め" できるタブのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="d7787-269">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="d7787-270">スコープ内で宣言された静的タブ `personal` は、常にアプリの個人用エクスペリエンスにピン留めされます。</span><span class="sxs-lookup"><span data-stu-id="d7787-270">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="d7787-271">スコープで宣言されている静的タブ `team` は現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d7787-271">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="d7787-272">このアイテムは、型のすべての要素を持つ配列 (最大 16 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-272">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="d7787-273">このブロックは、静的タブ ソリューションを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="d7787-273">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="d7787-274">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-274">Name</span></span>| <span data-ttu-id="d7787-275">型</span><span class="sxs-lookup"><span data-stu-id="d7787-275">Type</span></span>| <span data-ttu-id="d7787-276">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-276">Maximum size</span></span> | <span data-ttu-id="d7787-277">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-277">Required</span></span> | <span data-ttu-id="d7787-278">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-278">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="d7787-279">string</span><span class="sxs-lookup"><span data-stu-id="d7787-279">string</span></span>|<span data-ttu-id="d7787-280">64 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-280">64 characters</span></span>|<span data-ttu-id="d7787-281">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-281">✔</span></span>|<span data-ttu-id="d7787-282">タブが表示されるエンティティの一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="d7787-282">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="d7787-283">string</span><span class="sxs-lookup"><span data-stu-id="d7787-283">string</span></span>|<span data-ttu-id="d7787-284">128 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-284">128 characters</span></span>|<span data-ttu-id="d7787-285">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-285">✔</span></span>|<span data-ttu-id="d7787-286">チャネル インターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="d7787-286">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="d7787-287">string</span><span class="sxs-lookup"><span data-stu-id="d7787-287">string</span></span>||<span data-ttu-id="d7787-288">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-288">✔</span></span>|<span data-ttu-id="d7787-289">この https:// キャンバスに表示するエンティティ UI を示すTeamsします。</span><span class="sxs-lookup"><span data-stu-id="d7787-289">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="d7787-290">string</span><span class="sxs-lookup"><span data-stu-id="d7787-290">string</span></span>|||<span data-ttu-id="d7787-291">ユーザー https:// ブラウザーで表示することを選択した場合に示す URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-291">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="d7787-292">string</span><span class="sxs-lookup"><span data-stu-id="d7787-292">string</span></span>|||<span data-ttu-id="d7787-293">ユーザー https:// 検索クエリを参照する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-293">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="d7787-294">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-294">array of enums</span></span>|<span data-ttu-id="d7787-295">1</span><span class="sxs-lookup"><span data-stu-id="d7787-295">1</span></span>|<span data-ttu-id="d7787-296">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-296">✔</span></span>|<span data-ttu-id="d7787-297">現在、静的タブはスコープのみをサポートしています。つまり、個人用エクスペリエンスの一部としてのみ `personal` プロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="d7787-297">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="d7787-298">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-298">array of enums</span></span>| <span data-ttu-id="d7787-299">2</span><span class="sxs-lookup"><span data-stu-id="d7787-299">2</span></span>|| <span data-ttu-id="d7787-300">タブが `contextItem` サポートされているスコープのセット。</span><span class="sxs-lookup"><span data-stu-id="d7787-300">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="d7787-301">サード パーティの開発者は searchUrl 機能を使用できません。</span><span class="sxs-lookup"><span data-stu-id="d7787-301">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="d7787-302">関連するコンテンツを表示したり、認証フローを開始したりするために、タブにコンテキスト依存の情報が必要な場合は、「Get context for your [Microsoft Teams タブ」を参照してください](../../tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="d7787-302">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="d7787-303">bots</span><span class="sxs-lookup"><span data-stu-id="d7787-303">bots</span></span>

<span data-ttu-id="d7787-304">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="d7787-304">**Optional** — array</span></span>

<span data-ttu-id="d7787-305">既定のコマンド プロパティなどのオプションの情報と共に、ボット ソリューションを定義します。</span><span class="sxs-lookup"><span data-stu-id="d7787-305">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="d7787-306">アイテムは、型のすべての要素を持つ配列 (現在、アプリごとにボットが 1 つしか許可されていない要素が最大 1 つ) &mdash; です `object` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-306">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="d7787-307">このブロックは、ボット エクスペリエンスを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="d7787-307">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="d7787-308">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-308">Name</span></span>| <span data-ttu-id="d7787-309">型</span><span class="sxs-lookup"><span data-stu-id="d7787-309">Type</span></span>| <span data-ttu-id="d7787-310">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-310">Maximum size</span></span> | <span data-ttu-id="d7787-311">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-311">Required</span></span> | <span data-ttu-id="d7787-312">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-312">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="d7787-313">string</span><span class="sxs-lookup"><span data-stu-id="d7787-313">string</span></span>|<span data-ttu-id="d7787-314">64 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-314">64 characters</span></span>|<span data-ttu-id="d7787-315">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-315">✔</span></span>|<span data-ttu-id="d7787-316">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="d7787-316">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="d7787-317">これは、アプリ全体の ID と同じ [可能性があります](#id)。</span><span class="sxs-lookup"><span data-stu-id="d7787-317">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="d7787-318">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-318">array of enums</span></span>|<span data-ttu-id="d7787-319">3</span><span class="sxs-lookup"><span data-stu-id="d7787-319">3</span></span>|<span data-ttu-id="d7787-320">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-320">✔</span></span>|<span data-ttu-id="d7787-321">ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-321">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="d7787-322">これらのオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="d7787-322">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="d7787-323">boolean</span><span class="sxs-lookup"><span data-stu-id="d7787-323">boolean</span></span>|||<span data-ttu-id="d7787-324">ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。</span><span class="sxs-lookup"><span data-stu-id="d7787-324">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="d7787-325">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="d7787-325">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="d7787-326">boolean</span><span class="sxs-lookup"><span data-stu-id="d7787-326">boolean</span></span>|||<span data-ttu-id="d7787-327">ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="d7787-327">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="d7787-328">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="d7787-328">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="d7787-329">boolean</span><span class="sxs-lookup"><span data-stu-id="d7787-329">boolean</span></span>|||<span data-ttu-id="d7787-330">パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="d7787-330">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="d7787-331">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="d7787-331">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="d7787-332">boolean</span><span class="sxs-lookup"><span data-stu-id="d7787-332">boolean</span></span>|||<span data-ttu-id="d7787-333">ボットがオーディオ通話をサポートする場所を示す値。</span><span class="sxs-lookup"><span data-stu-id="d7787-333">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="d7787-334">**重要**: このプロパティは現在実験的です。</span><span class="sxs-lookup"><span data-stu-id="d7787-334">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="d7787-335">実験的なプロパティは完全ではない可能性があります。また、完全に利用可能になる前に変更が加わる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-335">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="d7787-336">これはテストと探索の目的でのみ提供され、実稼働アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="d7787-336">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="d7787-337">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="d7787-337">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="d7787-338">boolean</span><span class="sxs-lookup"><span data-stu-id="d7787-338">boolean</span></span>|||<span data-ttu-id="d7787-339">ボットがビデオ通話をサポートする場所を示す値。</span><span class="sxs-lookup"><span data-stu-id="d7787-339">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="d7787-340">**重要**: このプロパティは現在実験的です。</span><span class="sxs-lookup"><span data-stu-id="d7787-340">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="d7787-341">実験的なプロパティは完全ではない可能性があります。また、完全に利用可能になる前に変更が加わる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-341">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="d7787-342">これはテストと探索の目的でのみ提供され、実稼働アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="d7787-342">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="d7787-343">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="d7787-343">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="d7787-344">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="d7787-344">bots.commandLists</span></span>

<span data-ttu-id="d7787-345">ボットがユーザーに推奨できるコマンドのオプションの一覧。</span><span class="sxs-lookup"><span data-stu-id="d7787-345">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="d7787-346">オブジェクトは、型のすべての要素を持つ配列 (最大 2 つの要素) です。ボットがサポートするスコープごとに個別のコマンド リストを `object` 定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-346">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="d7787-347">詳細については [、「ボット メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d7787-347">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="d7787-348">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-348">Name</span></span>| <span data-ttu-id="d7787-349">型</span><span class="sxs-lookup"><span data-stu-id="d7787-349">Type</span></span>| <span data-ttu-id="d7787-350">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-350">Maximum size</span></span> | <span data-ttu-id="d7787-351">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-351">Required</span></span> | <span data-ttu-id="d7787-352">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-352">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="d7787-353">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-353">array of enums</span></span>|<span data-ttu-id="d7787-354">3</span><span class="sxs-lookup"><span data-stu-id="d7787-354">3</span></span>|<span data-ttu-id="d7787-355">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-355">✔</span></span>|<span data-ttu-id="d7787-356">コマンド リストが有効なスコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-356">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="d7787-357">`team`、`personal`、`groupchat` の中から選択できます。</span><span class="sxs-lookup"><span data-stu-id="d7787-357">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="d7787-358">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="d7787-358">array of objects</span></span>|<span data-ttu-id="d7787-359">10</span><span class="sxs-lookup"><span data-stu-id="d7787-359">10</span></span>|<span data-ttu-id="d7787-360">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-360">✔</span></span>|<span data-ttu-id="d7787-361">ボットがサポートするコマンドの配列:</span><span class="sxs-lookup"><span data-stu-id="d7787-361">An array of commands the bot supports:</span></span><br><span data-ttu-id="d7787-362">`title`: ボット コマンドの名前 (文字列、32)</span><span class="sxs-lookup"><span data-stu-id="d7787-362">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="d7787-363">`description`: コマンド構文とその引数の簡単な説明または例 (文字列、128)。</span><span class="sxs-lookup"><span data-stu-id="d7787-363">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="d7787-364">bots.commandLists.command</span><span class="sxs-lookup"><span data-stu-id="d7787-364">bots.commandLists.commands</span></span>

|<span data-ttu-id="d7787-365">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-365">Name</span></span>| <span data-ttu-id="d7787-366">型</span><span class="sxs-lookup"><span data-stu-id="d7787-366">Type</span></span>| <span data-ttu-id="d7787-367">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-367">Maximum size</span></span> | <span data-ttu-id="d7787-368">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-368">Required</span></span> | <span data-ttu-id="d7787-369">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-369">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="d7787-370">title</span><span class="sxs-lookup"><span data-stu-id="d7787-370">title</span></span>|<span data-ttu-id="d7787-371">string</span><span class="sxs-lookup"><span data-stu-id="d7787-371">string</span></span>|<span data-ttu-id="d7787-372">12 </span><span class="sxs-lookup"><span data-stu-id="d7787-372">12</span></span>|<span data-ttu-id="d7787-373">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-373">✔</span></span>|<span data-ttu-id="d7787-374">ボット コマンド名。</span><span class="sxs-lookup"><span data-stu-id="d7787-374">The bot command name.</span></span>|
|<span data-ttu-id="d7787-375">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-375">description</span></span>|<span data-ttu-id="d7787-376">string</span><span class="sxs-lookup"><span data-stu-id="d7787-376">string</span></span>|<span data-ttu-id="d7787-377">128 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-377">128 characters</span></span>|<span data-ttu-id="d7787-378">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-378">✔</span></span>|<span data-ttu-id="d7787-379">単純なテキストの説明、またはコマンド構文とその引数の例。</span><span class="sxs-lookup"><span data-stu-id="d7787-379">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="d7787-380">コネクタ</span><span class="sxs-lookup"><span data-stu-id="d7787-380">connectors</span></span>

<span data-ttu-id="d7787-381">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="d7787-381">**Optional** — array</span></span>

<span data-ttu-id="d7787-382">ブロック `connectors` は、アプリOffice 365コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="d7787-382">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="d7787-383">オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-383">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="d7787-384">このブロックは、Connector を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="d7787-384">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="d7787-385">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-385">Name</span></span>| <span data-ttu-id="d7787-386">型</span><span class="sxs-lookup"><span data-stu-id="d7787-386">Type</span></span>| <span data-ttu-id="d7787-387">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-387">Maximum size</span></span> | <span data-ttu-id="d7787-388">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-388">Required</span></span> | <span data-ttu-id="d7787-389">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-389">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="d7787-390">string</span><span class="sxs-lookup"><span data-stu-id="d7787-390">string</span></span>|<span data-ttu-id="d7787-391">2048 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-391">2048 characters</span></span>|<span data-ttu-id="d7787-392">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-392">✔</span></span>|<span data-ttu-id="d7787-393">コネクタ https:// する際に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-393">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="d7787-394">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-394">array of enums</span></span>|<span data-ttu-id="d7787-395">1</span><span class="sxs-lookup"><span data-stu-id="d7787-395">1</span></span>|<span data-ttu-id="d7787-396">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-396">✔</span></span>|<span data-ttu-id="d7787-397">Connector がチャネルのコンテキストでエクスペリエンスを提供するかどうか、または個々のユーザー () にスコープを設定したエクスペリエンスを提供するかどうかを `team` 指定します `personal` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-397">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="d7787-398">現在、スコープ `team` だけがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="d7787-398">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="d7787-399">string</span><span class="sxs-lookup"><span data-stu-id="d7787-399">string</span></span>|<span data-ttu-id="d7787-400">64 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-400">64 characters</span></span>|<span data-ttu-id="d7787-401">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-401">✔</span></span>|<span data-ttu-id="d7787-402">コネクタ開発者ダッシュボードの ID に一致するコネクタの一 [意の識別子](https://aka.ms/connectorsdashboard)です。</span><span class="sxs-lookup"><span data-stu-id="d7787-402">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="d7787-403">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="d7787-403">composeExtensions</span></span>

<span data-ttu-id="d7787-404">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="d7787-404">**Optional** — array</span></span>

<span data-ttu-id="d7787-405">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="d7787-405">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="d7787-406">機能の名前は、2017 年 11 月に "作成拡張機能" から "メッセージング拡張機能" に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は変わりません。</span><span class="sxs-lookup"><span data-stu-id="d7787-406">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="d7787-407">アイテムは、型のすべての要素を持つ配列 (最大 1 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-407">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="d7787-408">このブロックは、メッセージング拡張機能を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="d7787-408">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="d7787-409">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-409">Name</span></span>| <span data-ttu-id="d7787-410">型</span><span class="sxs-lookup"><span data-stu-id="d7787-410">Type</span></span> | <span data-ttu-id="d7787-411">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-411">Maximum Size</span></span> | <span data-ttu-id="d7787-412">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-412">Required</span></span> | <span data-ttu-id="d7787-413">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-413">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="d7787-414">string</span><span class="sxs-lookup"><span data-stu-id="d7787-414">string</span></span>|<span data-ttu-id="d7787-415">64</span><span class="sxs-lookup"><span data-stu-id="d7787-415">64</span></span>|<span data-ttu-id="d7787-416">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-416">✔</span></span>|<span data-ttu-id="d7787-417">ボット フレームワークに登録されているメッセージング拡張機能をバックするボットの一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="d7787-417">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="d7787-418">これは、アプリ ID 全体と同じ可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-418">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="d7787-419">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="d7787-419">array of objects</span></span>|<span data-ttu-id="d7787-420">10</span><span class="sxs-lookup"><span data-stu-id="d7787-420">10</span></span>|<span data-ttu-id="d7787-421">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-421">✔</span></span>|<span data-ttu-id="d7787-422">メッセージング拡張機能がサポートするコマンドの配列。</span><span class="sxs-lookup"><span data-stu-id="d7787-422">Array of commands the messaging extension supports.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="d7787-423">boolean</span><span class="sxs-lookup"><span data-stu-id="d7787-423">boolean</span></span>|||<span data-ttu-id="d7787-424">メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="d7787-424">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="d7787-425">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="d7787-425">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="d7787-426">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="d7787-426">array of Objects</span></span>|<span data-ttu-id="d7787-427">5</span><span class="sxs-lookup"><span data-stu-id="d7787-427">5</span></span>||<span data-ttu-id="d7787-428">特定の条件が満たされた場合にアプリを呼び出すことができるハンドラーの一覧。</span><span class="sxs-lookup"><span data-stu-id="d7787-428">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="d7787-429">string</span><span class="sxs-lookup"><span data-stu-id="d7787-429">string</span></span>|||<span data-ttu-id="d7787-430">メッセージ ハンドラーの種類。</span><span class="sxs-lookup"><span data-stu-id="d7787-430">The type of message handler.</span></span> <span data-ttu-id="d7787-431">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-431">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="d7787-432">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-432">array of Strings</span></span>|||<span data-ttu-id="d7787-433">リンク メッセージ ハンドラーが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="d7787-433">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="d7787-434">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="d7787-434">composeExtensions.commands</span></span>

<span data-ttu-id="d7787-435">メッセージング拡張機能は、1 つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-435">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="d7787-436">各コマンドは、MICROSOFT TEAMSエントリ ポイントからの潜在的な対話として表示されます。</span><span class="sxs-lookup"><span data-stu-id="d7787-436">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="d7787-437">最大 10 のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="d7787-437">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="d7787-438">各コマンド 項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="d7787-438">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="d7787-439">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-439">Name</span></span>| <span data-ttu-id="d7787-440">型</span><span class="sxs-lookup"><span data-stu-id="d7787-440">Type</span></span>| <span data-ttu-id="d7787-441">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-441">Maximum size</span></span> | <span data-ttu-id="d7787-442">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-442">Required</span></span> | <span data-ttu-id="d7787-443">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-443">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="d7787-444">string</span><span class="sxs-lookup"><span data-stu-id="d7787-444">string</span></span>|<span data-ttu-id="d7787-445">64 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-445">64 characters</span></span>|<span data-ttu-id="d7787-446">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-446">✔</span></span>|<span data-ttu-id="d7787-447">コマンドの ID。</span><span class="sxs-lookup"><span data-stu-id="d7787-447">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="d7787-448">string</span><span class="sxs-lookup"><span data-stu-id="d7787-448">string</span></span>|<span data-ttu-id="d7787-449">32 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-449">32 characters</span></span>|<span data-ttu-id="d7787-450">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-450">✔</span></span>|<span data-ttu-id="d7787-451">ユーザーフレンドリーなコマンド名。</span><span class="sxs-lookup"><span data-stu-id="d7787-451">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="d7787-452">string</span><span class="sxs-lookup"><span data-stu-id="d7787-452">string</span></span>|<span data-ttu-id="d7787-453">64 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-453">64 characters</span></span>||<span data-ttu-id="d7787-454">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="d7787-454">Type of the command.</span></span> <span data-ttu-id="d7787-455">または `query` の 1 `action` つ。</span><span class="sxs-lookup"><span data-stu-id="d7787-455">One of `query` or `action`.</span></span> <span data-ttu-id="d7787-456">既定: **クエリ** です。</span><span class="sxs-lookup"><span data-stu-id="d7787-456">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="d7787-457">string</span><span class="sxs-lookup"><span data-stu-id="d7787-457">string</span></span>|<span data-ttu-id="d7787-458">128 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-458">128 characters</span></span>||<span data-ttu-id="d7787-459">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="d7787-459">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="d7787-460">boolean</span><span class="sxs-lookup"><span data-stu-id="d7787-460">boolean</span></span>|||<span data-ttu-id="d7787-461">ブール値は、コマンドがパラメーターを使用して最初に実行されるかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="d7787-461">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="d7787-462">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="d7787-462">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="d7787-463">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-463">array of Strings</span></span>|<span data-ttu-id="d7787-464">3</span><span class="sxs-lookup"><span data-stu-id="d7787-464">3</span></span>||<span data-ttu-id="d7787-465">メッセージ拡張機能の呼び出し先を定義します。</span><span class="sxs-lookup"><span data-stu-id="d7787-465">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="d7787-466">`compose`、 の任意の `commandBox` 組み合 `message` わせ。</span><span class="sxs-lookup"><span data-stu-id="d7787-466">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="d7787-467">既定値は `["compose","commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="d7787-467">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="d7787-468">boolean</span><span class="sxs-lookup"><span data-stu-id="d7787-468">boolean</span></span>|||<span data-ttu-id="d7787-469">タスク モジュールを動的にフェッチする必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="d7787-469">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="d7787-470">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="d7787-470">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="d7787-471">object</span><span class="sxs-lookup"><span data-stu-id="d7787-471">object</span></span>|||<span data-ttu-id="d7787-472">メッセージング拡張機能コマンドを使用する場合に事前読み込みするタスク モジュールを指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-472">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="d7787-473">string</span><span class="sxs-lookup"><span data-stu-id="d7787-473">string</span></span>|<span data-ttu-id="d7787-474">64 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-474">64 characters</span></span>||<span data-ttu-id="d7787-475">最初のダイアログ タイトル。</span><span class="sxs-lookup"><span data-stu-id="d7787-475">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="d7787-476">string</span><span class="sxs-lookup"><span data-stu-id="d7787-476">string</span></span>|||<span data-ttu-id="d7787-477">ダイアログの幅 - ピクセル単位の数値または既定のレイアウト ('large'、'medium'、または 'small' など)。</span><span class="sxs-lookup"><span data-stu-id="d7787-477">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="d7787-478">string</span><span class="sxs-lookup"><span data-stu-id="d7787-478">string</span></span>|||<span data-ttu-id="d7787-479">ダイアログの高さ - ピクセル単位の数値、または 'large'、'medium'、または 'small' などの既定のレイアウト。</span><span class="sxs-lookup"><span data-stu-id="d7787-479">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="d7787-480">string</span><span class="sxs-lookup"><span data-stu-id="d7787-480">string</span></span>|||<span data-ttu-id="d7787-481">初期 Webview URL。</span><span class="sxs-lookup"><span data-stu-id="d7787-481">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="d7787-482">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="d7787-482">array of object</span></span>|<span data-ttu-id="d7787-483">5 つのアイテム</span><span class="sxs-lookup"><span data-stu-id="d7787-483">5 items</span></span>|<span data-ttu-id="d7787-484">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-484">✔</span></span>|<span data-ttu-id="d7787-485">コマンドが受け取るパラメーターの一覧。</span><span class="sxs-lookup"><span data-stu-id="d7787-485">The list of parameters the command takes.</span></span> <span data-ttu-id="d7787-486">最小: 1;最大: 5。</span><span class="sxs-lookup"><span data-stu-id="d7787-486">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="d7787-487">string</span><span class="sxs-lookup"><span data-stu-id="d7787-487">string</span></span>|<span data-ttu-id="d7787-488">64 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-488">64 characters</span></span>|<span data-ttu-id="d7787-489">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-489">✔</span></span>|<span data-ttu-id="d7787-490">クライアントに表示されるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="d7787-490">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="d7787-491">これは、ユーザー要求に含まれます。</span><span class="sxs-lookup"><span data-stu-id="d7787-491">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="d7787-492">string</span><span class="sxs-lookup"><span data-stu-id="d7787-492">string</span></span>|<span data-ttu-id="d7787-493">32 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-493">32 characters</span></span>|<span data-ttu-id="d7787-494">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-494">✔</span></span>|<span data-ttu-id="d7787-495">パラメーターのユーザーフレンドリーなタイトル。</span><span class="sxs-lookup"><span data-stu-id="d7787-495">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="d7787-496">string</span><span class="sxs-lookup"><span data-stu-id="d7787-496">string</span></span>|<span data-ttu-id="d7787-497">128 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-497">128 characters</span></span>||<span data-ttu-id="d7787-498">このパラメーターの目的を説明するユーザーフレンドリーな文字列。</span><span class="sxs-lookup"><span data-stu-id="d7787-498">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="d7787-499">string</span><span class="sxs-lookup"><span data-stu-id="d7787-499">string</span></span>|<span data-ttu-id="d7787-500">512 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-500">512 characters</span></span>||<span data-ttu-id="d7787-501">パラメーターの初期値。</span><span class="sxs-lookup"><span data-stu-id="d7787-501">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="d7787-502">string</span><span class="sxs-lookup"><span data-stu-id="d7787-502">string</span></span>|<span data-ttu-id="d7787-503">128 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-503">128 characters</span></span>||<span data-ttu-id="d7787-504">タスク モジュールに表示されるコントロールの種類を定義します `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-504">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="d7787-505">の 1 `text, textarea, number, date, time, toggle, choiceset` つ。</span><span class="sxs-lookup"><span data-stu-id="d7787-505">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="d7787-506">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="d7787-506">array of objects</span></span>|<span data-ttu-id="d7787-507">10 アイテム</span><span class="sxs-lookup"><span data-stu-id="d7787-507">10 items</span></span>||<span data-ttu-id="d7787-508">の選択肢 `choiceset` オプションです。</span><span class="sxs-lookup"><span data-stu-id="d7787-508">The choice options for the`choiceset`.</span></span> <span data-ttu-id="d7787-509">の場合にのみ `parameter.inputType` 使用します `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-509">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="d7787-510">string</span><span class="sxs-lookup"><span data-stu-id="d7787-510">string</span></span>|<span data-ttu-id="d7787-511">128 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-511">128 characters</span></span>|<span data-ttu-id="d7787-512">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-512">✔</span></span>|<span data-ttu-id="d7787-513">選択したタイトル。</span><span class="sxs-lookup"><span data-stu-id="d7787-513">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="d7787-514">string</span><span class="sxs-lookup"><span data-stu-id="d7787-514">string</span></span>|<span data-ttu-id="d7787-515">512 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-515">512 characters</span></span>|<span data-ttu-id="d7787-516">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-516">✔</span></span>|<span data-ttu-id="d7787-517">Value of the choice.</span><span class="sxs-lookup"><span data-stu-id="d7787-517">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="d7787-518">permissions</span><span class="sxs-lookup"><span data-stu-id="d7787-518">permissions</span></span>

<span data-ttu-id="d7787-519">**省略** 可能 - 文字列の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-519">**Optional** — array of strings</span></span>

<span data-ttu-id="d7787-520">アプリが要求するアクセス許可を指定する配列で、エンド ユーザーは拡張機能の実行 `string` 方法を知る必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-520">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="d7787-521">次のオプションは、非排他的です。</span><span class="sxs-lookup"><span data-stu-id="d7787-521">The following options are non-exclusive:</span></span>

* <span data-ttu-id="d7787-522">`identity`&emsp;ユーザー ID 情報が必要です。</span><span class="sxs-lookup"><span data-stu-id="d7787-522">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="d7787-523">`messageTeamMembers`&emsp;チーム メンバーに直接メッセージを送信するためのアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="d7787-523">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="d7787-524">アプリの更新中にこれらのアクセス許可を変更すると、更新されたアプリの実行後にユーザーが同意プロセスを繰り返します。</span><span class="sxs-lookup"><span data-stu-id="d7787-524">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="d7787-525">詳細については [、「アプリの更新」](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d7787-525">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="d7787-526">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="d7787-526">devicePermissions</span></span>

<span data-ttu-id="d7787-527">**省略** 可能 - 文字列の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-527">**Optional** — array of strings</span></span>

<span data-ttu-id="d7787-528">アプリがアクセスを要求するユーザーのデバイス上のネイティブ機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="d7787-528">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="d7787-529">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="d7787-529">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="d7787-530">validDomains</span><span class="sxs-lookup"><span data-stu-id="d7787-530">validDomains</span></span>

<span data-ttu-id="d7787-531">**省略** 可能です 。ただし **、必須の** 場合は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="d7787-531">**Optional**, except **Required** where noted.</span></span>

<span data-ttu-id="d7787-532">アプリがクライアント内で読み込むと予想される Web サイトの有効なドメインTeamsします。</span><span class="sxs-lookup"><span data-stu-id="d7787-532">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="d7787-533">ドメインの一覧には、ワイルドカード (たとえば) を含めできます `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-533">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="d7787-534">これは、ドメインの 1 つのセグメントと完全に一致します。一致する必要がある場合は、 `a.b.example.com` を使用します `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-534">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="d7787-535">タブ構成またはコンテンツ UI で、タブ構成に使用するドメイン以外のドメインに移動する必要がある場合は、ここでそのドメインを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-535">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="d7787-536">サポート **する** ID プロバイダーのドメインをアプリに含める必要はありません。</span><span class="sxs-lookup"><span data-stu-id="d7787-536">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="d7787-537">たとえば、Google ID を使用して認証を行う場合は、accounts.google.com にリダイレクトする必要があります。ただし、accounts.google.com を含 accounts.google.com 必要があります `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-537">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="d7787-538">Teams機能するために独自の sharepoint URL を必要とするアプリには、有効なドメイン リストに "{teamsitedomain}" が含まれます。</span><span class="sxs-lookup"><span data-stu-id="d7787-538">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7787-539">直接またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しません。</span><span class="sxs-lookup"><span data-stu-id="d7787-539">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="d7787-540">たとえば、 `yourapp.onmicrosoft.com` 有効ですが、 `*.onmicrosoft.com` 無効です。</span><span class="sxs-lookup"><span data-stu-id="d7787-540">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="d7787-541">オブジェクトは、型のすべての要素を持つ配列です `string` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-541">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="d7787-542">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="d7787-542">webApplicationInfo</span></span>

<span data-ttu-id="d7787-543">**省略可能** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="d7787-543">**Optional** — object</span></span>

<span data-ttu-id="d7787-544">ユーザーがアプリAzure Active Directoryシームレスにサインインするのに役立つ、アプリ ID と Microsoft Graph情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="d7787-544">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="d7787-545">アプリが AAD に登録されている場合は、管理者が管理センターでアクセス許可を簡単に確認し、同意を与Teamsする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-545">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="d7787-546">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-546">Name</span></span>| <span data-ttu-id="d7787-547">型</span><span class="sxs-lookup"><span data-stu-id="d7787-547">Type</span></span>| <span data-ttu-id="d7787-548">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-548">Maximum size</span></span> | <span data-ttu-id="d7787-549">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-549">Required</span></span> | <span data-ttu-id="d7787-550">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-550">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="d7787-551">string</span><span class="sxs-lookup"><span data-stu-id="d7787-551">string</span></span>|<span data-ttu-id="d7787-552">36 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-552">36 characters</span></span>|<span data-ttu-id="d7787-553">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-553">✔</span></span>|<span data-ttu-id="d7787-554">アプリの AAD アプリケーション ID。</span><span class="sxs-lookup"><span data-stu-id="d7787-554">AAD application id of the app.</span></span> <span data-ttu-id="d7787-555">この ID は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-555">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="d7787-556">string</span><span class="sxs-lookup"><span data-stu-id="d7787-556">string</span></span>|<span data-ttu-id="d7787-557">2048 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-557">2048 characters</span></span>|<span data-ttu-id="d7787-558">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-558">✔</span></span>|<span data-ttu-id="d7787-559">SSO の認証トークンを取得するためのアプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="d7787-559">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="d7787-560">**注:** SSO を使用していない場合は、エラー応答を回避するために、このフィールドにダミーの文字列値をアプリ マニフェストに https://notapplicable 入力してください。</span><span class="sxs-lookup"><span data-stu-id="d7787-560">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="d7787-561">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="d7787-561">array of strings</span></span>|<span data-ttu-id="d7787-562">128 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-562">128 characters</span></span>||<span data-ttu-id="d7787-563">詳細なリソース [固有の同意を指定します](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="d7787-563">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="d7787-564">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="d7787-564">showLoadingIndicator</span></span>

<span data-ttu-id="d7787-565">**省略** 可能 - ブール型 (Boolean)</span><span class="sxs-lookup"><span data-stu-id="d7787-565">**Optional** — boolean</span></span>

<span data-ttu-id="d7787-566">アプリまたはタブの読み込み時に読み込みインジケーターを表示するかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="d7787-566">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="d7787-567">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="d7787-567">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="d7787-568">アプリ マニフェストで true を選択した場合、ページを正しく読み込むには、「ネイティブ読み込みインジケーター ドキュメントを表示する」の説明に従って、タブとタスク モジュールのコンテンツ ページを `showLoadingIndicator` [変更](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) します。</span><span class="sxs-lookup"><span data-stu-id="d7787-568">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="d7787-569">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="d7787-569">isFullScreen</span></span>

 <span data-ttu-id="d7787-570">**省略** 可能 - ブール型 (Boolean)</span><span class="sxs-lookup"><span data-stu-id="d7787-570">**Optional** — boolean</span></span>

<span data-ttu-id="d7787-571">タブ ヘッダー バーの付きまたはなしで個人用アプリがレンダリングされる場所を示します。</span><span class="sxs-lookup"><span data-stu-id="d7787-571">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="d7787-572">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="d7787-572">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="d7787-573">activities</span><span class="sxs-lookup"><span data-stu-id="d7787-573">activities</span></span>

<span data-ttu-id="d7787-574">**省略可能** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="d7787-574">**Optional** — object</span></span>

<span data-ttu-id="d7787-575">アプリがユーザー アクティビティ フィードの投稿に使用するプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="d7787-575">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="d7787-576">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-576">Name</span></span>| <span data-ttu-id="d7787-577">型</span><span class="sxs-lookup"><span data-stu-id="d7787-577">Type</span></span>| <span data-ttu-id="d7787-578">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-578">Maximum size</span></span> | <span data-ttu-id="d7787-579">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-579">Required</span></span> | <span data-ttu-id="d7787-580">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-580">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="d7787-581">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="d7787-581">array of Objects</span></span>|<span data-ttu-id="d7787-582">128 アイテム</span><span class="sxs-lookup"><span data-stu-id="d7787-582">128 items</span></span>| | <span data-ttu-id="d7787-583">アプリがユーザーアクティビティ フィードに投稿できるアクティビティの種類を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-583">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="d7787-584">activity.activityTypes</span><span class="sxs-lookup"><span data-stu-id="d7787-584">activities.activityTypes</span></span>

|<span data-ttu-id="d7787-585">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-585">Name</span></span>| <span data-ttu-id="d7787-586">型</span><span class="sxs-lookup"><span data-stu-id="d7787-586">Type</span></span>| <span data-ttu-id="d7787-587">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-587">Maximum size</span></span> | <span data-ttu-id="d7787-588">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-588">Required</span></span> | <span data-ttu-id="d7787-589">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-589">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="d7787-590">string</span><span class="sxs-lookup"><span data-stu-id="d7787-590">string</span></span>|<span data-ttu-id="d7787-591">32 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-591">32 characters</span></span>|<span data-ttu-id="d7787-592">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-592">✔</span></span>|<span data-ttu-id="d7787-593">通知の種類。</span><span class="sxs-lookup"><span data-stu-id="d7787-593">The notification type.</span></span> <span data-ttu-id="d7787-594">*以下を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="d7787-594">*See below*.</span></span>|
|`description`|<span data-ttu-id="d7787-595">string</span><span class="sxs-lookup"><span data-stu-id="d7787-595">string</span></span>|<span data-ttu-id="d7787-596">128 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-596">128 characters</span></span>|<span data-ttu-id="d7787-597">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-597">✔</span></span>|<span data-ttu-id="d7787-598">通知の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="d7787-598">A brief description of the notification.</span></span> <span data-ttu-id="d7787-599">*以下を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="d7787-599">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="d7787-600">string</span><span class="sxs-lookup"><span data-stu-id="d7787-600">string</span></span>|<span data-ttu-id="d7787-601">128 文字</span><span class="sxs-lookup"><span data-stu-id="d7787-601">128 characters</span></span>|<span data-ttu-id="d7787-602">✔</span><span class="sxs-lookup"><span data-stu-id="d7787-602">✔</span></span>|<span data-ttu-id="d7787-603">例: "{actor} が作成したタスク {taskId} for you"</span><span class="sxs-lookup"><span data-stu-id="d7787-603">Ex: "{actor} created task {taskId} for you"</span></span>|

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

## <a name="defaultinstallscope"></a><span data-ttu-id="d7787-604">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="d7787-604">defaultInstallScope</span></span>

<span data-ttu-id="d7787-605">**省略** 可能 - 文字列</span><span class="sxs-lookup"><span data-stu-id="d7787-605">**Optional** - string</span></span>

<span data-ttu-id="d7787-606">既定では、このアプリに対して定義されているインストール スコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-606">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="d7787-607">定義されたスコープは、ユーザーがアプリを追加しようとするときにボタンに表示されるオプションになります。</span><span class="sxs-lookup"><span data-stu-id="d7787-607">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="d7787-608">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="d7787-608">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="d7787-609">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="d7787-609">defaultGroupCapability</span></span>

<span data-ttu-id="d7787-610">**省略可能** - オブジェクト</span><span class="sxs-lookup"><span data-stu-id="d7787-610">**Optional** - object</span></span>

<span data-ttu-id="d7787-611">グループ インストール スコープを選択すると、ユーザーがアプリをインストールするときに既定の機能が定義されます。</span><span class="sxs-lookup"><span data-stu-id="d7787-611">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="d7787-612">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="d7787-612">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="d7787-613">名前</span><span class="sxs-lookup"><span data-stu-id="d7787-613">Name</span></span>| <span data-ttu-id="d7787-614">型</span><span class="sxs-lookup"><span data-stu-id="d7787-614">Type</span></span>| <span data-ttu-id="d7787-615">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="d7787-615">Maximum size</span></span> | <span data-ttu-id="d7787-616">必須</span><span class="sxs-lookup"><span data-stu-id="d7787-616">Required</span></span> | <span data-ttu-id="d7787-617">説明</span><span class="sxs-lookup"><span data-stu-id="d7787-617">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="d7787-618">string</span><span class="sxs-lookup"><span data-stu-id="d7787-618">string</span></span>|||<span data-ttu-id="d7787-619">選択したインストール スコープが次の場合 `team` 、このフィールドは使用可能な既定の機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-619">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="d7787-620">オプション: `tab` `bot` 、、または `connector` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-620">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="d7787-621">string</span><span class="sxs-lookup"><span data-stu-id="d7787-621">string</span></span>|||<span data-ttu-id="d7787-622">選択したインストール スコープが次の場合 `groupchat` 、このフィールドは使用可能な既定の機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-622">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="d7787-623">オプション: `tab` `bot` 、、または `connector` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-623">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="d7787-624">string</span><span class="sxs-lookup"><span data-stu-id="d7787-624">string</span></span>|||<span data-ttu-id="d7787-625">選択したインストール スコープが次の場合 `meetings` 、このフィールドは使用可能な既定の機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7787-625">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="d7787-626">オプション: `tab` `bot` 、、または `connector` 。</span><span class="sxs-lookup"><span data-stu-id="d7787-626">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="d7787-627">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="d7787-627">configurableProperties</span></span>

<span data-ttu-id="d7787-628">**オプション** - 配列</span><span class="sxs-lookup"><span data-stu-id="d7787-628">**Optional** - array</span></span>

<span data-ttu-id="d7787-629">この `configurableProperties` ブロックは、管理者がカスタマイズできるアプリTeams定義します。</span><span class="sxs-lookup"><span data-stu-id="d7787-629">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="d7787-630">詳細については、「アプリのカスタマイズ[」を参照Microsoft Teams。](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="d7787-630">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="d7787-631">少なくとも 1 つのプロパティを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-631">A minimum of one property must be defined.</span></span> <span data-ttu-id="d7787-632">このブロックでは、最大 9 つのプロパティを定義できます。</span><span class="sxs-lookup"><span data-stu-id="d7787-632">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="d7787-633">ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7787-633">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span>

<span data-ttu-id="d7787-634">次のプロパティを定義できます。</span><span class="sxs-lookup"><span data-stu-id="d7787-634">You can define any of the following properties:</span></span>
* <span data-ttu-id="d7787-635">`name`: 管理者がアプリの表示名を変更できます。</span><span class="sxs-lookup"><span data-stu-id="d7787-635">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="d7787-636">`shortDescription`: 管理者がアプリの簡単な説明を変更できます。</span><span class="sxs-lookup"><span data-stu-id="d7787-636">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="d7787-637">`longDescription`: 管理者がアプリの詳細な説明を変更できます。</span><span class="sxs-lookup"><span data-stu-id="d7787-637">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="d7787-638">`smallImageUrl`: マニフェストの `outline` ブロック内 `icons` のプロパティです。</span><span class="sxs-lookup"><span data-stu-id="d7787-638">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="d7787-639">`largeImageUrl`: マニフェストの `color` ブロック内 `icons` のプロパティです。</span><span class="sxs-lookup"><span data-stu-id="d7787-639">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="d7787-640">`accentColor`: アウトライン アイコンと組み合わせて、背景として使用する色です。</span><span class="sxs-lookup"><span data-stu-id="d7787-640">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="d7787-641">`websiteUrl`: 開発者の https:// の URL です。</span><span class="sxs-lookup"><span data-stu-id="d7787-641">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="d7787-642">`privacyUrl`: 開発者の https:// の URL です。</span><span class="sxs-lookup"><span data-stu-id="d7787-642">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="d7787-643">`termsOfUseUrl`: 開発者の https:// の URL です。</span><span class="sxs-lookup"><span data-stu-id="d7787-643">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>


