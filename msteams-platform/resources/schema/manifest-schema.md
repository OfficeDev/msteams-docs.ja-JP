---
title: マニフェスト スキーマ参照
description: アプリケーションのマニフェスト スキーマについてMicrosoft Teams
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: teams マニフェスト スキーマ
ms.openlocfilehash: 75c29a1cf9c2897d7b419b45bfc1a4f0447c7aa3
ms.sourcegitcommit: 37325179a532897fafbe827dcf9a7ca5fa5e7d0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2021
ms.locfileid: "52853530"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="ed88f-104">リファレンス: マニフェスト スキーマのMicrosoft Teams</span><span class="sxs-lookup"><span data-stu-id="ed88f-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="ed88f-105">このTeamsマニフェストは、アプリが製品に統合する方法Microsoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="ed88f-105">The Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="ed88f-106">マニフェストは、 でホストされるスキーマに準拠している必要があります [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="ed88f-107">以前のバージョン 1.0、1.1,..., 1.6 もサポートされています (URL で "v1.x" を使用)。</span><span class="sxs-lookup"><span data-stu-id="ed88f-107">Previous versions 1.0, 1.1,..., 1.6, and so on are also supported (using "v1.x" in the URL).</span></span>
<span data-ttu-id="ed88f-108">各バージョンで行われた変更の詳細については、「マニフェスト変更 [ログ」を参照してください](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)。</span><span class="sxs-lookup"><span data-stu-id="ed88f-108">For more information on the changes made in each version, see [manifest change log](https://github.com/OfficeDev/microsoft-teams-app-schema/releases).</span></span>

<span data-ttu-id="ed88f-109">次のスキーマ サンプルは、すべての機能拡張オプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="ed88f-109">The following schema sample shows all extensibility options:</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="ed88f-110">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="ed88f-110">Sample full manifest</span></span>

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
     "developerUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ]              
}
```

<span data-ttu-id="ed88f-111">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-111">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="ed88f-112">$schema</span><span class="sxs-lookup"><span data-stu-id="ed88f-112">$schema</span></span>

<span data-ttu-id="ed88f-113">省略可能ですが、推奨される — string</span><span class="sxs-lookup"><span data-stu-id="ed88f-113">Optional, but recommended — string</span></span>

<span data-ttu-id="ed88f-114">マニフェスト https:// JSON スキーマを参照する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-114">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="ed88f-115">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="ed88f-115">manifestVersion</span></span>

<span data-ttu-id="ed88f-116">**必須** — 文字列</span><span class="sxs-lookup"><span data-stu-id="ed88f-116">**Required** — string</span></span>

<span data-ttu-id="ed88f-117">このマニフェストが使用しているマニフェスト スキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="ed88f-117">The version of manifest schema this manifest is using.</span></span> <span data-ttu-id="ed88f-118">1.10 である必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-118">It must be 1.10.</span></span>

## <a name="version"></a><span data-ttu-id="ed88f-119">version</span><span class="sxs-lookup"><span data-stu-id="ed88f-119">version</span></span>

<span data-ttu-id="ed88f-120">**必須** — 文字列</span><span class="sxs-lookup"><span data-stu-id="ed88f-120">**Required** — string</span></span>

<span data-ttu-id="ed88f-121">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="ed88f-121">The version of a specific app.</span></span> <span data-ttu-id="ed88f-122">マニフェストで何かを更新する場合は、バージョンもインクリメントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-122">If you update something in your manifest, the version must be incremented too.</span></span> <span data-ttu-id="ed88f-123">これにより、新しいマニフェストがインストールされた場合、既存のマニフェストが上書きされ、ユーザーは新しい機能を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-123">This way, when the new manifest is installed, it overwrites the existing one and the user receives the new functionality.</span></span> <span data-ttu-id="ed88f-124">このアプリがストアに送信された場合は、新しいマニフェストを再送信して再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-124">If this app was submitted to the store, the new manifest must be re-submitted and re-validated.</span></span> <span data-ttu-id="ed88f-125">アプリユーザーは、マニフェストが承認された後、数時間以内に新しい更新されたマニフェストを自動的に受信します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-125">The app users receive the new updated manifest automatically within few hours after the manifest is approved.</span></span>

<span data-ttu-id="ed88f-126">アプリでアクセス許可の要求が変更された場合、ユーザーはアプリのアップグレードと再同意を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ed88f-126">If the app requests for permissions change, the users are prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="ed88f-127">このバージョンの文字列は [、semver](http://semver.org/) 標準 (MAJOR) に従う必要があります。MINOR。PATCH)。</span><span class="sxs-lookup"><span data-stu-id="ed88f-127">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="ed88f-128">id</span><span class="sxs-lookup"><span data-stu-id="ed88f-128">id</span></span>

<span data-ttu-id="ed88f-129">**必須** — Microsoft アプリ ID</span><span class="sxs-lookup"><span data-stu-id="ed88f-129">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="ed88f-130">ID は、アプリの Microsoft が生成する一意の識別子です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-130">The ID is a unique Microsoft-generated identifier for the app.</span></span> <span data-ttu-id="ed88f-131">ボットが Microsoft で既にサインインしている場合は、Microsoft Bot Frameworkタブの Web アプリを使用して登録されている場合は、ID を持っています。</span><span class="sxs-lookup"><span data-stu-id="ed88f-131">You have an ID if your bot is registered through the Microsoft Bot Framework or your tab's web app already signs in with Microsoft.</span></span> <span data-ttu-id="ed88f-132">ここに ID を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-132">You must enter the ID here.</span></span> <span data-ttu-id="ed88f-133">それ以外の場合は、Microsoft アプリケーション登録ポータルで新しい ID [を生成する必要があります](https://aka.ms/appregistrations)。</span><span class="sxs-lookup"><span data-stu-id="ed88f-133">Otherwise, you must generate a new ID at the [Microsoft Application Registration Portal](https://aka.ms/appregistrations).</span></span> <span data-ttu-id="ed88f-134">ボットを追加する場合は、同じ ID を使用します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-134">Use the same ID if you add a bot.</span></span>

> [!NOTE]
> <span data-ttu-id="ed88f-135">AppSource で既存のアプリに更新プログラムを提出する場合は、マニフェスト内の ID を変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="ed88f-135">If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="ed88f-136">developer</span><span class="sxs-lookup"><span data-stu-id="ed88f-136">developer</span></span>

<span data-ttu-id="ed88f-137">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="ed88f-137">**Required** — object</span></span>

<span data-ttu-id="ed88f-138">会社に関する情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-138">Specifies information about your company.</span></span> <span data-ttu-id="ed88f-139">アプリがストアに送信Teams、これらの値はストア登録情報の情報と一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-139">For apps submitted to the Teams store, these values must match the information in your store listing.</span></span> <span data-ttu-id="ed88f-140">詳細については、「ストア発行ガイドラインTeams[を参照してください](~/concepts/deploy-and-publish/appsource/publish.md)。</span><span class="sxs-lookup"><span data-stu-id="ed88f-140">For more information, see the [Teams store publishing guidelines](~/concepts/deploy-and-publish/appsource/publish.md).</span></span>

|<span data-ttu-id="ed88f-141">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-141">Name</span></span>| <span data-ttu-id="ed88f-142">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-142">Maximum size</span></span> | <span data-ttu-id="ed88f-143">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-143">Required</span></span> | <span data-ttu-id="ed88f-144">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="ed88f-145">32 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-145">32 characters</span></span>|<span data-ttu-id="ed88f-146">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-146">✔</span></span>|<span data-ttu-id="ed88f-147">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="ed88f-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="ed88f-148">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-148">2048 characters</span></span>|<span data-ttu-id="ed88f-149">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-149">✔</span></span>|<span data-ttu-id="ed88f-150">開発者 https:// WEB サイトの URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="ed88f-151">このリンクは、ユーザーを会社または製品固有のランディング ページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-151">This link must take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="ed88f-152">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-152">2048 characters</span></span>|<span data-ttu-id="ed88f-153">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-153">✔</span></span>|<span data-ttu-id="ed88f-154">開発者 https:// のプライバシー ポリシーの URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="ed88f-155">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-155">2048 characters</span></span>|<span data-ttu-id="ed88f-156">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-156">✔</span></span>|<span data-ttu-id="ed88f-157">開発者 https:// の使用条件の URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="ed88f-158">10 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-158">10 characters</span></span>| |<span data-ttu-id="ed88f-159">**省略可能** アプリを構築するパートナー組織を識別する Microsoft パートナー ネットワーク ID。</span><span class="sxs-lookup"><span data-stu-id="ed88f-159">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="ed88f-160">name</span><span class="sxs-lookup"><span data-stu-id="ed88f-160">name</span></span>

<span data-ttu-id="ed88f-161">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="ed88f-161">**Required** — object</span></span>

<span data-ttu-id="ed88f-162">アプリ エクスペリエンスのユーザーに表示されるアプリ エクスペリエンスのTeamsします。</span><span class="sxs-lookup"><span data-stu-id="ed88f-162">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="ed88f-163">AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-163">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="ed88f-164">の値と `short` 異 `full` なる値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-164">The values of `short` and `full` must be different.</span></span>

|<span data-ttu-id="ed88f-165">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-165">Name</span></span>| <span data-ttu-id="ed88f-166">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-166">Maximum size</span></span> | <span data-ttu-id="ed88f-167">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-167">Required</span></span> | <span data-ttu-id="ed88f-168">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-168">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="ed88f-169">30 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-169">30 characters</span></span>|<span data-ttu-id="ed88f-170">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-170">✔</span></span>|<span data-ttu-id="ed88f-171">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="ed88f-171">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="ed88f-172">100 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-172">100 characters</span></span>||<span data-ttu-id="ed88f-173">完全なアプリ名が 30 文字を超える場合に使用されるアプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="ed88f-173">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="ed88f-174">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-174">description</span></span>

<span data-ttu-id="ed88f-175">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="ed88f-175">**Required** — object</span></span>

<span data-ttu-id="ed88f-176">アプリをユーザーに説明します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-176">Describes your app to users.</span></span> <span data-ttu-id="ed88f-177">AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-177">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="ed88f-178">説明がエクスペリエンスを正確に説明し、潜在的な顧客がエクスペリエンスの内容を理解するのに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-178">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="ed88f-179">外部アカウントを使用する必要がある場合は、完全な説明に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-179">You must note in the full description, if an external account is required for use.</span></span> <span data-ttu-id="ed88f-180">の値と `short` 異 `full` なる値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-180">The values of `short` and `full` must be different.</span></span> <span data-ttu-id="ed88f-181">短い説明は、長い説明の中で繰り返し実行し、他のアプリ名を含めずに行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-181">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="ed88f-182">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-182">Name</span></span>| <span data-ttu-id="ed88f-183">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-183">Maximum size</span></span> | <span data-ttu-id="ed88f-184">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-184">Required</span></span> | <span data-ttu-id="ed88f-185">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-185">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="ed88f-186">80 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-186">80 characters</span></span>|<span data-ttu-id="ed88f-187">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-187">✔</span></span>|<span data-ttu-id="ed88f-188">スペースが制限されている場合に使用されるアプリ エクスペリエンスの簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="ed88f-188">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="ed88f-189">4000 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-189">4000 characters</span></span>|<span data-ttu-id="ed88f-190">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-190">✔</span></span>|<span data-ttu-id="ed88f-191">アプリの完全な説明。</span><span class="sxs-lookup"><span data-stu-id="ed88f-191">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="ed88f-192">packageName</span><span class="sxs-lookup"><span data-stu-id="ed88f-192">packageName</span></span>

<span data-ttu-id="ed88f-193">**省略** 可能 — 文字列</span><span class="sxs-lookup"><span data-stu-id="ed88f-193">**Optional** — string</span></span>

<span data-ttu-id="ed88f-194">逆ドメイン表記のアプリの一意の識別子。たとえば、com.example.myapp などです。</span><span class="sxs-lookup"><span data-stu-id="ed88f-194">A unique identifier for the app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="ed88f-195">最大長: 64 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-195">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="ed88f-196">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="ed88f-196">localizationInfo</span></span>

<span data-ttu-id="ed88f-197">**省略可能** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="ed88f-197">**Optional** — object</span></span>

<span data-ttu-id="ed88f-198">既定の言語の指定と、追加の言語ファイルへのポインターを許可します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-198">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="ed88f-199">詳細については、「ローカライズ」を [参照してください](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="ed88f-199">For more information, see [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="ed88f-200">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-200">Name</span></span>| <span data-ttu-id="ed88f-201">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-201">Maximum size</span></span> | <span data-ttu-id="ed88f-202">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-202">Required</span></span> | <span data-ttu-id="ed88f-203">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-203">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="ed88f-204">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-204">✔</span></span>|<span data-ttu-id="ed88f-205">このトップ レベルのマニフェスト ファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="ed88f-205">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="ed88f-206">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="ed88f-206">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="ed88f-207">追加の言語変換を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="ed88f-207">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="ed88f-208">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-208">Name</span></span>| <span data-ttu-id="ed88f-209">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-209">Maximum size</span></span> | <span data-ttu-id="ed88f-210">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-210">Required</span></span> | <span data-ttu-id="ed88f-211">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-211">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="ed88f-212">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-212">✔</span></span>|<span data-ttu-id="ed88f-213">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="ed88f-213">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="ed88f-214">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-214">✔</span></span>|<span data-ttu-id="ed88f-215">翻訳された文字列を含む .json ファイルへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="ed88f-215">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="ed88f-216">アイコン</span><span class="sxs-lookup"><span data-stu-id="ed88f-216">icons</span></span>

<span data-ttu-id="ed88f-217">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="ed88f-217">**Required** — object</span></span>

<span data-ttu-id="ed88f-218">アプリ内で使用Teamsアイコン。</span><span class="sxs-lookup"><span data-stu-id="ed88f-218">Icons used within the Teams app.</span></span> <span data-ttu-id="ed88f-219">アイコン ファイルは、アップロード パッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-219">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="ed88f-220">詳細については [、「アイコン](../../concepts/build-and-test/apps-package.md#app-icons) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed88f-220">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="ed88f-221">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-221">Name</span></span>| <span data-ttu-id="ed88f-222">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-222">Maximum size</span></span> | <span data-ttu-id="ed88f-223">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-223">Required</span></span> | <span data-ttu-id="ed88f-224">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-224">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="ed88f-225">32 x 32 ピクセル</span><span class="sxs-lookup"><span data-stu-id="ed88f-225">32 x 32 pixels</span></span>|<span data-ttu-id="ed88f-226">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-226">✔</span></span>|<span data-ttu-id="ed88f-227">透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="ed88f-227">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="ed88f-228">192 x 192 ピクセル</span><span class="sxs-lookup"><span data-stu-id="ed88f-228">192 x 192 pixels</span></span>|<span data-ttu-id="ed88f-229">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-229">✔</span></span>|<span data-ttu-id="ed88f-230">フル カラーの 192x192 PNG アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="ed88f-230">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="ed88f-231">accentColor</span><span class="sxs-lookup"><span data-stu-id="ed88f-231">accentColor</span></span>

<span data-ttu-id="ed88f-232">**省略** 可能 — HTML の 16 進カラー コード</span><span class="sxs-lookup"><span data-stu-id="ed88f-232">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="ed88f-233">アウトライン アイコンと組み合わせて、背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="ed88f-233">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="ed88f-234">値は、'#' で始まる有効な HTML カラー コードである必要があります `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-234">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="ed88f-235">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="ed88f-235">configurableTabs</span></span>

<span data-ttu-id="ed88f-236">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-236">**Optional** — array</span></span>

<span data-ttu-id="ed88f-237">アプリ エクスペリエンスに、追加する前に追加の構成が必要なチーム チャネル タブ エクスペリエンスがある場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-237">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="ed88f-238">構成可能なタブは teams スコープでのみサポートされ、同じタブを複数回構成できます。</span><span class="sxs-lookup"><span data-stu-id="ed88f-238">Configurable tabs are supported only in the teams scope and you can configure the same tabs multiple times.</span></span> <span data-ttu-id="ed88f-239">ただし、マニフェストで定義できるのは 1 回のみです。</span><span class="sxs-lookup"><span data-stu-id="ed88f-239">However, you can define it in the manifest only once.</span></span>

|<span data-ttu-id="ed88f-240">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-240">Name</span></span>| <span data-ttu-id="ed88f-241">型</span><span class="sxs-lookup"><span data-stu-id="ed88f-241">Type</span></span>| <span data-ttu-id="ed88f-242">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-242">Maximum size</span></span> | <span data-ttu-id="ed88f-243">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-243">Required</span></span> | <span data-ttu-id="ed88f-244">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="ed88f-245">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-245">string</span></span>|<span data-ttu-id="ed88f-246">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-246">2048 characters</span></span>|<span data-ttu-id="ed88f-247">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-247">✔</span></span>|<span data-ttu-id="ed88f-248">タブ https:// する際に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-248">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="ed88f-249">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-249">array of enums</span></span>|<span data-ttu-id="ed88f-250">1</span><span class="sxs-lookup"><span data-stu-id="ed88f-250">1</span></span>|<span data-ttu-id="ed88f-251">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-251">✔</span></span>|<span data-ttu-id="ed88f-252">現在、構成可能なタブは、スコープ `team` とスコープ `groupchat` のみをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ed88f-252">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="ed88f-253">ブール値</span><span class="sxs-lookup"><span data-stu-id="ed88f-253">boolean</span></span>|||<span data-ttu-id="ed88f-254">作成後に、タブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="ed88f-254">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="ed88f-255">既定値: **true 。**</span><span class="sxs-lookup"><span data-stu-id="ed88f-255">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="ed88f-256">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-256">array of enums</span></span>|<span data-ttu-id="ed88f-257">6</span><span class="sxs-lookup"><span data-stu-id="ed88f-257">6</span></span>||<span data-ttu-id="ed88f-258">タブが `contextItem` サポートされているスコープ [のセット](../../tabs/how-to/access-teams-context.md)です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-258">The set of `contextItem` scopes where a [tab is supported](../../tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="ed88f-259">既定値: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="ed88f-259">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="ed88f-260">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-260">string</span></span>|<span data-ttu-id="ed88f-261">2048</span><span class="sxs-lookup"><span data-stu-id="ed88f-261">2048</span></span>||<span data-ttu-id="ed88f-262">タブ プレビュー イメージへの相対ファイル パスを使用して、SharePoint。</span><span class="sxs-lookup"><span data-stu-id="ed88f-262">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="ed88f-263">サイズは 1024x768 です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-263">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="ed88f-264">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-264">array of enums</span></span>|<span data-ttu-id="ed88f-265">1</span><span class="sxs-lookup"><span data-stu-id="ed88f-265">1</span></span>||<span data-ttu-id="ed88f-266">タブを使用してタブを使用する方法をSharePoint。</span><span class="sxs-lookup"><span data-stu-id="ed88f-266">Defines how your tab is made available in SharePoint.</span></span> <span data-ttu-id="ed88f-267">オプションは `sharePointFullPage` 次のとおりです。 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="ed88f-267">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="ed88f-268">staticTabs</span><span class="sxs-lookup"><span data-stu-id="ed88f-268">staticTabs</span></span>

<span data-ttu-id="ed88f-269">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-269">**Optional** — array</span></span>

<span data-ttu-id="ed88f-270">ユーザーが手動で追加せずに、既定で "ピン留め" できるタブのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-270">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="ed88f-271">スコープ内で宣言された静的タブ `personal` は、常にアプリの個人用エクスペリエンスにピン留めされます。</span><span class="sxs-lookup"><span data-stu-id="ed88f-271">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="ed88f-272">スコープで宣言されている静的タブ `team` は現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="ed88f-272">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="ed88f-273">このアイテムは、型のすべての要素を持つ配列 (最大 16 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-273">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="ed88f-274">このブロックは、静的タブ ソリューションを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-274">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="ed88f-275">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-275">Name</span></span>| <span data-ttu-id="ed88f-276">型</span><span class="sxs-lookup"><span data-stu-id="ed88f-276">Type</span></span>| <span data-ttu-id="ed88f-277">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-277">Maximum size</span></span> | <span data-ttu-id="ed88f-278">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-278">Required</span></span> | <span data-ttu-id="ed88f-279">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-279">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="ed88f-280">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-280">string</span></span>|<span data-ttu-id="ed88f-281">64 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-281">64 characters</span></span>|<span data-ttu-id="ed88f-282">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-282">✔</span></span>|<span data-ttu-id="ed88f-283">タブが表示されるエンティティの一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="ed88f-283">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="ed88f-284">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-284">string</span></span>|<span data-ttu-id="ed88f-285">128 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-285">128 characters</span></span>|<span data-ttu-id="ed88f-286">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-286">✔</span></span>|<span data-ttu-id="ed88f-287">チャネル インターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="ed88f-287">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="ed88f-288">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-288">string</span></span>||<span data-ttu-id="ed88f-289">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-289">✔</span></span>|<span data-ttu-id="ed88f-290">この https:// キャンバスに表示するエンティティ UI を示すTeamsします。</span><span class="sxs-lookup"><span data-stu-id="ed88f-290">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="ed88f-291">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-291">string</span></span>|||<span data-ttu-id="ed88f-292">ユーザー https:// ブラウザーで表示することを選択した場合に示す URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-292">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="ed88f-293">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-293">string</span></span>|||<span data-ttu-id="ed88f-294">ユーザー https:// 検索クエリを参照する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-294">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="ed88f-295">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-295">array of enums</span></span>|<span data-ttu-id="ed88f-296">1</span><span class="sxs-lookup"><span data-stu-id="ed88f-296">1</span></span>|<span data-ttu-id="ed88f-297">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-297">✔</span></span>|<span data-ttu-id="ed88f-298">現在、静的タブはスコープのみをサポートしています。つまり、個人用エクスペリエンスの一部としてのみ `personal` プロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="ed88f-298">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="ed88f-299">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-299">array of enums</span></span>| <span data-ttu-id="ed88f-300">2</span><span class="sxs-lookup"><span data-stu-id="ed88f-300">2</span></span>|| <span data-ttu-id="ed88f-301">タブが `contextItem` サポートされているスコープのセット。</span><span class="sxs-lookup"><span data-stu-id="ed88f-301">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
>  <span data-ttu-id="ed88f-302">サード パーティの開発者は searchUrl 機能を使用できません。</span><span class="sxs-lookup"><span data-stu-id="ed88f-302">The searchUrl feature is not available for the third-party developers.</span></span>
> <span data-ttu-id="ed88f-303">関連するコンテンツを表示したり、認証フローを開始したりするために、タブにコンテキスト依存の情報が必要な場合は、「Get context for your [Microsoft Teams タブ」を参照してください](../../tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="ed88f-303">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="ed88f-304">bots</span><span class="sxs-lookup"><span data-stu-id="ed88f-304">bots</span></span>

<span data-ttu-id="ed88f-305">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-305">**Optional** — array</span></span>

<span data-ttu-id="ed88f-306">既定のコマンド プロパティなどのオプションの情報と共に、ボット ソリューションを定義します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-306">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="ed88f-307">アイテムは、型のすべての要素を持つ配列 (現在、アプリごとにボットが 1 つしか許可されていない要素が最大 1 つ) &mdash; です `object` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-307">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="ed88f-308">このブロックは、ボット エクスペリエンスを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-308">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="ed88f-309">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-309">Name</span></span>| <span data-ttu-id="ed88f-310">型</span><span class="sxs-lookup"><span data-stu-id="ed88f-310">Type</span></span>| <span data-ttu-id="ed88f-311">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-311">Maximum size</span></span> | <span data-ttu-id="ed88f-312">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-312">Required</span></span> | <span data-ttu-id="ed88f-313">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-313">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="ed88f-314">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-314">string</span></span>|<span data-ttu-id="ed88f-315">64 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-315">64 characters</span></span>|<span data-ttu-id="ed88f-316">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-316">✔</span></span>|<span data-ttu-id="ed88f-317">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="ed88f-317">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="ed88f-318">これは、アプリ全体の ID と同じ [可能性があります](#id)。</span><span class="sxs-lookup"><span data-stu-id="ed88f-318">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="ed88f-319">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-319">array of enums</span></span>|<span data-ttu-id="ed88f-320">3</span><span class="sxs-lookup"><span data-stu-id="ed88f-320">3</span></span>|<span data-ttu-id="ed88f-321">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-321">✔</span></span>|<span data-ttu-id="ed88f-322">ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="ed88f-323">これらのオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-323">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="ed88f-324">ブール値</span><span class="sxs-lookup"><span data-stu-id="ed88f-324">boolean</span></span>|||<span data-ttu-id="ed88f-325">ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。</span><span class="sxs-lookup"><span data-stu-id="ed88f-325">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="ed88f-326">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="ed88f-326">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="ed88f-327">ブール値</span><span class="sxs-lookup"><span data-stu-id="ed88f-327">boolean</span></span>|||<span data-ttu-id="ed88f-328">ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-328">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="ed88f-329">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="ed88f-329">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="ed88f-330">ブール値</span><span class="sxs-lookup"><span data-stu-id="ed88f-330">boolean</span></span>|||<span data-ttu-id="ed88f-331">パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-331">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="ed88f-332">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="ed88f-332">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="ed88f-333">ブール値</span><span class="sxs-lookup"><span data-stu-id="ed88f-333">boolean</span></span>|||<span data-ttu-id="ed88f-334">ボットがオーディオ通話をサポートする場所を示す値。</span><span class="sxs-lookup"><span data-stu-id="ed88f-334">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="ed88f-335">**重要**: このプロパティは現在実験的です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="ed88f-336">実験的なプロパティは完全ではない可能性があります。また、完全に利用可能になる前に変更が加わる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="ed88f-337">これはテストと探索の目的でのみ提供され、実稼働アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="ed88f-337">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="ed88f-338">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="ed88f-338">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="ed88f-339">ブール値</span><span class="sxs-lookup"><span data-stu-id="ed88f-339">boolean</span></span>|||<span data-ttu-id="ed88f-340">ボットがビデオ通話をサポートする場所を示す値。</span><span class="sxs-lookup"><span data-stu-id="ed88f-340">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="ed88f-341">**重要**: このプロパティは現在実験的です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-341">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="ed88f-342">実験的なプロパティは完全ではない可能性があります。また、完全に利用可能になる前に変更が加わる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-342">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="ed88f-343">これはテストと探索の目的でのみ提供され、実稼働アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="ed88f-343">It is provided for testing and exploration purposes only and must not be used in production applications.</span></span> <span data-ttu-id="ed88f-344">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="ed88f-344">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="ed88f-345">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="ed88f-345">bots.commandLists</span></span>

<span data-ttu-id="ed88f-346">ボットがユーザーに推奨できるコマンドのオプションの一覧。</span><span class="sxs-lookup"><span data-stu-id="ed88f-346">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="ed88f-347">オブジェクトは、型のすべての要素を持つ配列 (最大 2 つの要素) です。ボットがサポートするスコープごとに個別のコマンド リストを `object` 定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-347">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="ed88f-348">詳細については [、「ボット メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed88f-348">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="ed88f-349">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-349">Name</span></span>| <span data-ttu-id="ed88f-350">型</span><span class="sxs-lookup"><span data-stu-id="ed88f-350">Type</span></span>| <span data-ttu-id="ed88f-351">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-351">Maximum size</span></span> | <span data-ttu-id="ed88f-352">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-352">Required</span></span> | <span data-ttu-id="ed88f-353">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-353">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="ed88f-354">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-354">array of enums</span></span>|<span data-ttu-id="ed88f-355">3</span><span class="sxs-lookup"><span data-stu-id="ed88f-355">3</span></span>|<span data-ttu-id="ed88f-356">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-356">✔</span></span>|<span data-ttu-id="ed88f-357">コマンド リストが有効なスコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-357">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="ed88f-358">`team`、`personal`、`groupchat` の中から選択できます。</span><span class="sxs-lookup"><span data-stu-id="ed88f-358">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="ed88f-359">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-359">array of objects</span></span>|<span data-ttu-id="ed88f-360">10</span><span class="sxs-lookup"><span data-stu-id="ed88f-360">10</span></span>|<span data-ttu-id="ed88f-361">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-361">✔</span></span>|<span data-ttu-id="ed88f-362">ボットがサポートするコマンドの配列:</span><span class="sxs-lookup"><span data-stu-id="ed88f-362">An array of commands the bot supports:</span></span><br><span data-ttu-id="ed88f-363">`title`: ボット コマンドの名前 (文字列、32)</span><span class="sxs-lookup"><span data-stu-id="ed88f-363">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="ed88f-364">`description`: コマンド構文とその引数の簡単な説明または例 (文字列、128)。</span><span class="sxs-lookup"><span data-stu-id="ed88f-364">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="ed88f-365">bots.commandLists.command</span><span class="sxs-lookup"><span data-stu-id="ed88f-365">bots.commandLists.commands</span></span>

|<span data-ttu-id="ed88f-366">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-366">Name</span></span>| <span data-ttu-id="ed88f-367">型</span><span class="sxs-lookup"><span data-stu-id="ed88f-367">Type</span></span>| <span data-ttu-id="ed88f-368">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-368">Maximum size</span></span> | <span data-ttu-id="ed88f-369">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-369">Required</span></span> | <span data-ttu-id="ed88f-370">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-370">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="ed88f-371">title</span><span class="sxs-lookup"><span data-stu-id="ed88f-371">title</span></span>|<span data-ttu-id="ed88f-372">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-372">string</span></span>|<span data-ttu-id="ed88f-373">12 </span><span class="sxs-lookup"><span data-stu-id="ed88f-373">12</span></span>|<span data-ttu-id="ed88f-374">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-374">✔</span></span>|<span data-ttu-id="ed88f-375">ボット コマンド名。</span><span class="sxs-lookup"><span data-stu-id="ed88f-375">The bot command name.</span></span>|
|<span data-ttu-id="ed88f-376">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-376">description</span></span>|<span data-ttu-id="ed88f-377">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-377">string</span></span>|<span data-ttu-id="ed88f-378">128 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-378">128 characters</span></span>|<span data-ttu-id="ed88f-379">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-379">✔</span></span>|<span data-ttu-id="ed88f-380">単純なテキストの説明、またはコマンド構文とその引数の例。</span><span class="sxs-lookup"><span data-stu-id="ed88f-380">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="ed88f-381">コネクタ</span><span class="sxs-lookup"><span data-stu-id="ed88f-381">connectors</span></span>

<span data-ttu-id="ed88f-382">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-382">**Optional** — array</span></span>

<span data-ttu-id="ed88f-383">ブロック `connectors` は、アプリOffice 365コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-383">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="ed88f-384">オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-384">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="ed88f-385">このブロックは、Connector を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-385">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="ed88f-386">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-386">Name</span></span>| <span data-ttu-id="ed88f-387">型</span><span class="sxs-lookup"><span data-stu-id="ed88f-387">Type</span></span>| <span data-ttu-id="ed88f-388">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-388">Maximum size</span></span> | <span data-ttu-id="ed88f-389">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-389">Required</span></span> | <span data-ttu-id="ed88f-390">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-390">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="ed88f-391">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-391">string</span></span>|<span data-ttu-id="ed88f-392">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-392">2048 characters</span></span>|<span data-ttu-id="ed88f-393">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-393">✔</span></span>|<span data-ttu-id="ed88f-394">コネクタ https:// する際に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-394">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="ed88f-395">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-395">array of enums</span></span>|<span data-ttu-id="ed88f-396">1</span><span class="sxs-lookup"><span data-stu-id="ed88f-396">1</span></span>|<span data-ttu-id="ed88f-397">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-397">✔</span></span>|<span data-ttu-id="ed88f-398">Connector がチャネルのコンテキストでエクスペリエンスを提供するかどうか、または個々のユーザー () にスコープを設定したエクスペリエンスを提供するかどうかを `team` 指定します `personal` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-398">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="ed88f-399">現在、スコープ `team` だけがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ed88f-399">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="ed88f-400">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-400">string</span></span>|<span data-ttu-id="ed88f-401">64 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-401">64 characters</span></span>|<span data-ttu-id="ed88f-402">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-402">✔</span></span>|<span data-ttu-id="ed88f-403">コネクタ開発者ダッシュボードの ID に一致するコネクタの一 [意の識別子](https://aka.ms/connectorsdashboard)です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-403">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="ed88f-404">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="ed88f-404">composeExtensions</span></span>

<span data-ttu-id="ed88f-405">**省略** 可能 — 配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-405">**Optional** — array</span></span>

<span data-ttu-id="ed88f-406">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-406">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="ed88f-407">機能の名前は、2017 年 11 月に "作成拡張機能" から "メッセージング拡張機能" に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は変わりません。</span><span class="sxs-lookup"><span data-stu-id="ed88f-407">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="ed88f-408">アイテムは、型のすべての要素を持つ配列 (最大 1 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-408">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="ed88f-409">このブロックは、メッセージング拡張機能を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-409">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="ed88f-410">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-410">Name</span></span>| <span data-ttu-id="ed88f-411">種類</span><span class="sxs-lookup"><span data-stu-id="ed88f-411">Type</span></span> | <span data-ttu-id="ed88f-412">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-412">Maximum Size</span></span> | <span data-ttu-id="ed88f-413">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-413">Required</span></span> | <span data-ttu-id="ed88f-414">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-414">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="ed88f-415">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-415">string</span></span>|<span data-ttu-id="ed88f-416">64</span><span class="sxs-lookup"><span data-stu-id="ed88f-416">64</span></span>|<span data-ttu-id="ed88f-417">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-417">✔</span></span>|<span data-ttu-id="ed88f-418">ボット フレームワークに登録されているメッセージング拡張機能をバックするボットの一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="ed88f-418">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="ed88f-419">これは、アプリ ID 全体と同じ可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-419">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="ed88f-420">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-420">array of objects</span></span>|<span data-ttu-id="ed88f-421">10</span><span class="sxs-lookup"><span data-stu-id="ed88f-421">10</span></span>|<span data-ttu-id="ed88f-422">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-422">✔</span></span>|<span data-ttu-id="ed88f-423">メッセージング拡張機能がサポートするコマンドの配列。</span><span class="sxs-lookup"><span data-stu-id="ed88f-423">Array of commands the messaging extension supports.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="ed88f-424">ブール値</span><span class="sxs-lookup"><span data-stu-id="ed88f-424">boolean</span></span>|||<span data-ttu-id="ed88f-425">メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="ed88f-425">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="ed88f-426">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="ed88f-426">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="ed88f-427">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-427">array of Objects</span></span>|<span data-ttu-id="ed88f-428">5</span><span class="sxs-lookup"><span data-stu-id="ed88f-428">5</span></span>||<span data-ttu-id="ed88f-429">特定の条件が満たされた場合にアプリを呼び出すことができるハンドラーの一覧。</span><span class="sxs-lookup"><span data-stu-id="ed88f-429">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="ed88f-430">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-430">string</span></span>|||<span data-ttu-id="ed88f-431">メッセージ ハンドラーの種類。</span><span class="sxs-lookup"><span data-stu-id="ed88f-431">The type of message handler.</span></span> <span data-ttu-id="ed88f-432">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-432">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="ed88f-433">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-433">array of Strings</span></span>|||<span data-ttu-id="ed88f-434">リンク メッセージ ハンドラーが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="ed88f-434">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="ed88f-435">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="ed88f-435">composeExtensions.commands</span></span>

<span data-ttu-id="ed88f-436">メッセージング拡張機能は、1 つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-436">Your messaging extension must declare one or more commands.</span></span> <span data-ttu-id="ed88f-437">各コマンドは、MICROSOFT TEAMSエントリ ポイントからの潜在的な対話として表示されます。</span><span class="sxs-lookup"><span data-stu-id="ed88f-437">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="ed88f-438">最大 10 のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-438">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="ed88f-439">各コマンド 項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="ed88f-439">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="ed88f-440">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-440">Name</span></span>| <span data-ttu-id="ed88f-441">型</span><span class="sxs-lookup"><span data-stu-id="ed88f-441">Type</span></span>| <span data-ttu-id="ed88f-442">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-442">Maximum size</span></span> | <span data-ttu-id="ed88f-443">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-443">Required</span></span> | <span data-ttu-id="ed88f-444">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-444">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="ed88f-445">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-445">string</span></span>|<span data-ttu-id="ed88f-446">64 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-446">64 characters</span></span>|<span data-ttu-id="ed88f-447">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-447">✔</span></span>|<span data-ttu-id="ed88f-448">コマンドの ID。</span><span class="sxs-lookup"><span data-stu-id="ed88f-448">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="ed88f-449">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-449">string</span></span>|<span data-ttu-id="ed88f-450">32 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-450">32 characters</span></span>|<span data-ttu-id="ed88f-451">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-451">✔</span></span>|<span data-ttu-id="ed88f-452">ユーザーフレンドリーなコマンド名。</span><span class="sxs-lookup"><span data-stu-id="ed88f-452">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="ed88f-453">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-453">string</span></span>|<span data-ttu-id="ed88f-454">64 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-454">64 characters</span></span>||<span data-ttu-id="ed88f-455">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="ed88f-455">Type of the command.</span></span> <span data-ttu-id="ed88f-456">または `query` の 1 `action` つ。</span><span class="sxs-lookup"><span data-stu-id="ed88f-456">One of `query` or `action`.</span></span> <span data-ttu-id="ed88f-457">既定: **クエリ** です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-457">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="ed88f-458">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-458">string</span></span>|<span data-ttu-id="ed88f-459">128 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-459">128 characters</span></span>||<span data-ttu-id="ed88f-460">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="ed88f-460">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="ed88f-461">ブール値</span><span class="sxs-lookup"><span data-stu-id="ed88f-461">boolean</span></span>|||<span data-ttu-id="ed88f-462">ブール値は、コマンドがパラメーターを使用して最初に実行されるかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-462">A boolean value indicates whether the command runs initially with no parameters.</span></span> <span data-ttu-id="ed88f-463">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-463">Default is **false**.</span></span>|
|`context`|<span data-ttu-id="ed88f-464">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-464">array of Strings</span></span>|<span data-ttu-id="ed88f-465">3</span><span class="sxs-lookup"><span data-stu-id="ed88f-465">3</span></span>||<span data-ttu-id="ed88f-466">メッセージ拡張機能の呼び出し先を定義します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-466">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="ed88f-467">`compose`、 の任意の `commandBox` 組み合 `message` わせ。</span><span class="sxs-lookup"><span data-stu-id="ed88f-467">Any combination of`compose`,`commandBox`,`message`.</span></span> <span data-ttu-id="ed88f-468">既定値は `["compose","commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-468">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="ed88f-469">ブール値</span><span class="sxs-lookup"><span data-stu-id="ed88f-469">boolean</span></span>|||<span data-ttu-id="ed88f-470">タスク モジュールを動的にフェッチする必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="ed88f-470">A boolean value that indicates if it must fetch the task module dynamically.</span></span> <span data-ttu-id="ed88f-471">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-471">Default is **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="ed88f-472">object</span><span class="sxs-lookup"><span data-stu-id="ed88f-472">object</span></span>|||<span data-ttu-id="ed88f-473">メッセージング拡張機能コマンドを使用する場合に事前読み込みするタスク モジュールを指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-473">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="ed88f-474">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-474">string</span></span>|<span data-ttu-id="ed88f-475">64 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-475">64 characters</span></span>||<span data-ttu-id="ed88f-476">最初のダイアログ タイトル。</span><span class="sxs-lookup"><span data-stu-id="ed88f-476">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="ed88f-477">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-477">string</span></span>|||<span data-ttu-id="ed88f-478">ダイアログの幅 - ピクセル単位の数値または既定のレイアウト ('large'、'medium'、または 'small' など)。</span><span class="sxs-lookup"><span data-stu-id="ed88f-478">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="ed88f-479">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-479">string</span></span>|||<span data-ttu-id="ed88f-480">ダイアログの高さ - ピクセル単位の数値、または 'large'、'medium'、または 'small' などの既定のレイアウト。</span><span class="sxs-lookup"><span data-stu-id="ed88f-480">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="ed88f-481">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-481">string</span></span>|||<span data-ttu-id="ed88f-482">初期 Webview URL。</span><span class="sxs-lookup"><span data-stu-id="ed88f-482">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="ed88f-483">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-483">array of object</span></span>|<span data-ttu-id="ed88f-484">5 つのアイテム</span><span class="sxs-lookup"><span data-stu-id="ed88f-484">5 items</span></span>|<span data-ttu-id="ed88f-485">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-485">✔</span></span>|<span data-ttu-id="ed88f-486">コマンドが受け取るパラメーターの一覧。</span><span class="sxs-lookup"><span data-stu-id="ed88f-486">The list of parameters the command takes.</span></span> <span data-ttu-id="ed88f-487">最小: 1;最大: 5。</span><span class="sxs-lookup"><span data-stu-id="ed88f-487">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="ed88f-488">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-488">string</span></span>|<span data-ttu-id="ed88f-489">64 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-489">64 characters</span></span>|<span data-ttu-id="ed88f-490">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-490">✔</span></span>|<span data-ttu-id="ed88f-491">クライアントに表示されるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="ed88f-491">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="ed88f-492">これは、ユーザー要求に含まれます。</span><span class="sxs-lookup"><span data-stu-id="ed88f-492">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="ed88f-493">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-493">string</span></span>|<span data-ttu-id="ed88f-494">32 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-494">32 characters</span></span>|<span data-ttu-id="ed88f-495">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-495">✔</span></span>|<span data-ttu-id="ed88f-496">パラメーターのユーザーフレンドリーなタイトル。</span><span class="sxs-lookup"><span data-stu-id="ed88f-496">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="ed88f-497">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-497">string</span></span>|<span data-ttu-id="ed88f-498">128 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-498">128 characters</span></span>||<span data-ttu-id="ed88f-499">このパラメーターの目的を説明するユーザーフレンドリーな文字列。</span><span class="sxs-lookup"><span data-stu-id="ed88f-499">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="ed88f-500">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-500">string</span></span>|<span data-ttu-id="ed88f-501">512 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-501">512 characters</span></span>||<span data-ttu-id="ed88f-502">パラメーターの初期値。</span><span class="sxs-lookup"><span data-stu-id="ed88f-502">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="ed88f-503">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-503">string</span></span>|<span data-ttu-id="ed88f-504">128 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-504">128 characters</span></span>||<span data-ttu-id="ed88f-505">タスク モジュールに表示されるコントロールの種類を定義します `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-505">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="ed88f-506">の 1 `text, textarea, number, date, time, toggle, choiceset` つ。</span><span class="sxs-lookup"><span data-stu-id="ed88f-506">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="ed88f-507">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-507">array of objects</span></span>|<span data-ttu-id="ed88f-508">10 アイテム</span><span class="sxs-lookup"><span data-stu-id="ed88f-508">10 items</span></span>||<span data-ttu-id="ed88f-509">の選択肢 `choiceset` オプションです。</span><span class="sxs-lookup"><span data-stu-id="ed88f-509">The choice options for the`choiceset`.</span></span> <span data-ttu-id="ed88f-510">の場合にのみ `parameter.inputType` 使用します `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-510">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="ed88f-511">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-511">string</span></span>|<span data-ttu-id="ed88f-512">128 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-512">128 characters</span></span>|<span data-ttu-id="ed88f-513">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-513">✔</span></span>|<span data-ttu-id="ed88f-514">選択したタイトル。</span><span class="sxs-lookup"><span data-stu-id="ed88f-514">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="ed88f-515">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-515">string</span></span>|<span data-ttu-id="ed88f-516">512 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-516">512 characters</span></span>|<span data-ttu-id="ed88f-517">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-517">✔</span></span>|<span data-ttu-id="ed88f-518">Value of the choice.</span><span class="sxs-lookup"><span data-stu-id="ed88f-518">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="ed88f-519">permissions</span><span class="sxs-lookup"><span data-stu-id="ed88f-519">permissions</span></span>

<span data-ttu-id="ed88f-520">**省略** 可能 - 文字列の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-520">**Optional** — array of strings</span></span>

<span data-ttu-id="ed88f-521">アプリが要求するアクセス許可を指定する配列で、エンド ユーザーは拡張機能の実行 `string` 方法を知る必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-521">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension performs.</span></span> <span data-ttu-id="ed88f-522">次のオプションは、非排他的です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-522">The following options are non-exclusive:</span></span>

* <span data-ttu-id="ed88f-523">`identity`&emsp;ユーザー ID 情報が必要です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-523">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="ed88f-524">`messageTeamMembers`&emsp;チーム メンバーに直接メッセージを送信するためのアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-524">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="ed88f-525">アプリの更新中にこれらのアクセス許可を変更すると、更新されたアプリの実行後にユーザーが同意プロセスを繰り返します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-525">Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app.</span></span> <span data-ttu-id="ed88f-526">詳細については [、「アプリの更新」](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed88f-526">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="ed88f-527">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="ed88f-527">devicePermissions</span></span>

<span data-ttu-id="ed88f-528">**省略** 可能 - 文字列の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-528">**Optional** — array of strings</span></span>

<span data-ttu-id="ed88f-529">アプリがアクセスを要求するユーザーのデバイス上のネイティブ機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-529">Provides the native features on a user's device that your app requests access to.</span></span> <span data-ttu-id="ed88f-530">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ed88f-530">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="ed88f-531">validDomains</span><span class="sxs-lookup"><span data-stu-id="ed88f-531">validDomains</span></span>

<span data-ttu-id="ed88f-532">**省略** 可能です 。ただし **、必須の** 場合は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-532">**Optional**, except **Required** where noted.</span></span>

<span data-ttu-id="ed88f-533">アプリがクライアント内で読み込むと予想される Web サイトの有効なドメインTeamsします。</span><span class="sxs-lookup"><span data-stu-id="ed88f-533">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="ed88f-534">ドメインの一覧には、ワイルドカード (たとえば) を含めできます `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-534">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="ed88f-535">これは、ドメインの 1 つのセグメントと完全に一致します。一致する必要がある場合は、 `a.b.example.com` を使用します `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-535">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="ed88f-536">タブ構成またはコンテンツ UI で、タブ構成に使用するドメイン以外のドメインに移動する必要がある場合は、ここでそのドメインを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-536">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="ed88f-537">サポート **する** ID プロバイダーのドメインをアプリに含める必要はありません。</span><span class="sxs-lookup"><span data-stu-id="ed88f-537">It is **not** necessary to include the domains of identity providers you want to support in your app.</span></span> <span data-ttu-id="ed88f-538">たとえば、Google ID を使用して認証を行う場合は、accounts.google.com にリダイレクトする必要があります。ただし、accounts.google.com を含 accounts.google.com 必要があります `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-538">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="ed88f-539">Teams機能するために独自の sharepoint URL を必要とするアプリには、有効なドメイン リストに "{teamsitedomain}" が含まれます。</span><span class="sxs-lookup"><span data-stu-id="ed88f-539">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed88f-540">直接またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しません。</span><span class="sxs-lookup"><span data-stu-id="ed88f-540">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="ed88f-541">たとえば、 `yourapp.onmicrosoft.com` 有効ですが、 `*.onmicrosoft.com` 無効です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-541">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="ed88f-542">オブジェクトは、型のすべての要素を持つ配列です `string` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-542">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="ed88f-543">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="ed88f-543">webApplicationInfo</span></span>

<span data-ttu-id="ed88f-544">**省略可能** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="ed88f-544">**Optional** — object</span></span>

<span data-ttu-id="ed88f-545">ユーザーがアプリAzure Active Directoryシームレスにサインインするのに役立つ、アプリ ID と Microsoft Graph情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-545">Provide your Azure Active Directory (AAD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="ed88f-546">アプリが AAD に登録されている場合は、管理者が管理センターでアクセス許可を簡単に確認し、同意を与Teamsする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-546">If your app is registered in AAD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="ed88f-547">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-547">Name</span></span>| <span data-ttu-id="ed88f-548">型</span><span class="sxs-lookup"><span data-stu-id="ed88f-548">Type</span></span>| <span data-ttu-id="ed88f-549">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-549">Maximum size</span></span> | <span data-ttu-id="ed88f-550">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-550">Required</span></span> | <span data-ttu-id="ed88f-551">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-551">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="ed88f-552">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-552">string</span></span>|<span data-ttu-id="ed88f-553">36 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-553">36 characters</span></span>|<span data-ttu-id="ed88f-554">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-554">✔</span></span>|<span data-ttu-id="ed88f-555">アプリの AAD アプリケーション ID。</span><span class="sxs-lookup"><span data-stu-id="ed88f-555">AAD application id of the app.</span></span> <span data-ttu-id="ed88f-556">この ID は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-556">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="ed88f-557">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-557">string</span></span>|<span data-ttu-id="ed88f-558">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-558">2048 characters</span></span>|<span data-ttu-id="ed88f-559">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-559">✔</span></span>|<span data-ttu-id="ed88f-560">SSO の認証トークンを取得するためのアプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="ed88f-560">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="ed88f-561">**注:** SSO を使用していない場合は、エラー応答を回避するために、このフィールドにダミーの文字列値をアプリ マニフェストに https://notapplicable 入力してください。</span><span class="sxs-lookup"><span data-stu-id="ed88f-561">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="ed88f-562">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-562">array of strings</span></span>|<span data-ttu-id="ed88f-563">128 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-563">128 characters</span></span>||<span data-ttu-id="ed88f-564">詳細なリソース [固有の同意を指定します](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="ed88f-564">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="ed88f-565">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="ed88f-565">showLoadingIndicator</span></span>

<span data-ttu-id="ed88f-566">**省略** 可能 - ブール型 (Boolean)</span><span class="sxs-lookup"><span data-stu-id="ed88f-566">**Optional** — boolean</span></span>

<span data-ttu-id="ed88f-567">アプリまたはタブの読み込み時に読み込みインジケーターを表示するかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-567">Indicates whether or not to show the loading indicator when an app or tab is loading.</span></span> <span data-ttu-id="ed88f-568">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-568">Default is **false**.</span></span>
>[!NOTE]
><span data-ttu-id="ed88f-569">アプリ マニフェストで true を選択した場合、ページを正しく読み込むには、「ネイティブ読み込みインジケーター ドキュメントを表示する」の説明に従って、タブとタスク モジュールのコンテンツ ページを `showLoadingIndicator` [変更](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-569">If you select`showLoadingIndicator` as true in your app manifest, to load the page correctly, modify the content pages of your tabs and task modules as described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="ed88f-570">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="ed88f-570">isFullScreen</span></span>

 <span data-ttu-id="ed88f-571">**省略** 可能 - ブール型 (Boolean)</span><span class="sxs-lookup"><span data-stu-id="ed88f-571">**Optional** — boolean</span></span>

<span data-ttu-id="ed88f-572">タブ ヘッダー バーの付きまたはなしで個人用アプリがレンダリングされる場所を示します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-572">Indicate where a personal app is rendered with or without a tab header bar.</span></span> <span data-ttu-id="ed88f-573">既定値は **false** です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-573">Default is **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="ed88f-574">activities</span><span class="sxs-lookup"><span data-stu-id="ed88f-574">activities</span></span>

<span data-ttu-id="ed88f-575">**省略可能** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="ed88f-575">**Optional** — object</span></span>

<span data-ttu-id="ed88f-576">アプリがユーザー アクティビティ フィードの投稿に使用するプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-576">Define the properties your app uses to post a user activity feed.</span></span>

|<span data-ttu-id="ed88f-577">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-577">Name</span></span>| <span data-ttu-id="ed88f-578">型</span><span class="sxs-lookup"><span data-stu-id="ed88f-578">Type</span></span>| <span data-ttu-id="ed88f-579">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-579">Maximum size</span></span> | <span data-ttu-id="ed88f-580">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-580">Required</span></span> | <span data-ttu-id="ed88f-581">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-581">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="ed88f-582">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-582">array of Objects</span></span>|<span data-ttu-id="ed88f-583">128 アイテム</span><span class="sxs-lookup"><span data-stu-id="ed88f-583">128 items</span></span>| | <span data-ttu-id="ed88f-584">アプリがユーザーアクティビティ フィードに投稿できるアクティビティの種類を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-584">Provide the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="ed88f-585">activity.activityTypes</span><span class="sxs-lookup"><span data-stu-id="ed88f-585">activities.activityTypes</span></span>

|<span data-ttu-id="ed88f-586">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-586">Name</span></span>| <span data-ttu-id="ed88f-587">型</span><span class="sxs-lookup"><span data-stu-id="ed88f-587">Type</span></span>| <span data-ttu-id="ed88f-588">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-588">Maximum size</span></span> | <span data-ttu-id="ed88f-589">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-589">Required</span></span> | <span data-ttu-id="ed88f-590">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-590">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="ed88f-591">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-591">string</span></span>|<span data-ttu-id="ed88f-592">32 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-592">32 characters</span></span>|<span data-ttu-id="ed88f-593">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-593">✔</span></span>|<span data-ttu-id="ed88f-594">通知の種類。</span><span class="sxs-lookup"><span data-stu-id="ed88f-594">The notification type.</span></span> <span data-ttu-id="ed88f-595">*以下を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="ed88f-595">*See below*.</span></span>|
|`description`|<span data-ttu-id="ed88f-596">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-596">string</span></span>|<span data-ttu-id="ed88f-597">128 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-597">128 characters</span></span>|<span data-ttu-id="ed88f-598">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-598">✔</span></span>|<span data-ttu-id="ed88f-599">通知の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="ed88f-599">A brief description of the notification.</span></span> <span data-ttu-id="ed88f-600">*以下を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="ed88f-600">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="ed88f-601">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-601">string</span></span>|<span data-ttu-id="ed88f-602">128 文字</span><span class="sxs-lookup"><span data-stu-id="ed88f-602">128 characters</span></span>|<span data-ttu-id="ed88f-603">✔</span><span class="sxs-lookup"><span data-stu-id="ed88f-603">✔</span></span>|<span data-ttu-id="ed88f-604">例: "{actor} が作成したタスク {taskId} for you"</span><span class="sxs-lookup"><span data-stu-id="ed88f-604">Ex: "{actor} created task {taskId} for you"</span></span>|

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

## <a name="defaultinstallscope"></a><span data-ttu-id="ed88f-605">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="ed88f-605">defaultInstallScope</span></span>

<span data-ttu-id="ed88f-606">**省略** 可能 - 文字列</span><span class="sxs-lookup"><span data-stu-id="ed88f-606">**Optional** - string</span></span>

<span data-ttu-id="ed88f-607">既定では、このアプリに対して定義されているインストール スコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-607">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="ed88f-608">定義されたスコープは、ユーザーがアプリを追加しようとするときにボタンに表示されるオプションになります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-608">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="ed88f-609">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ed88f-609">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="ed88f-610">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="ed88f-610">defaultGroupCapability</span></span>

<span data-ttu-id="ed88f-611">**省略可能** - オブジェクト</span><span class="sxs-lookup"><span data-stu-id="ed88f-611">**Optional** - object</span></span>

<span data-ttu-id="ed88f-612">グループ インストール スコープを選択すると、ユーザーがアプリをインストールするときに既定の機能が定義されます。</span><span class="sxs-lookup"><span data-stu-id="ed88f-612">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="ed88f-613">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ed88f-613">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="ed88f-614">名前</span><span class="sxs-lookup"><span data-stu-id="ed88f-614">Name</span></span>| <span data-ttu-id="ed88f-615">型</span><span class="sxs-lookup"><span data-stu-id="ed88f-615">Type</span></span>| <span data-ttu-id="ed88f-616">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ed88f-616">Maximum size</span></span> | <span data-ttu-id="ed88f-617">必須</span><span class="sxs-lookup"><span data-stu-id="ed88f-617">Required</span></span> | <span data-ttu-id="ed88f-618">説明</span><span class="sxs-lookup"><span data-stu-id="ed88f-618">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="ed88f-619">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-619">string</span></span>|||<span data-ttu-id="ed88f-620">選択したインストール スコープが次の場合 `team` 、このフィールドは使用可能な既定の機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-620">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="ed88f-621">オプション: `tab` `bot` 、、または `connector` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-621">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="ed88f-622">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-622">string</span></span>|||<span data-ttu-id="ed88f-623">選択したインストール スコープが次の場合 `groupchat` 、このフィールドは使用可能な既定の機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-623">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="ed88f-624">オプション: `tab` `bot` 、、または `connector` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-624">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="ed88f-625">string</span><span class="sxs-lookup"><span data-stu-id="ed88f-625">string</span></span>|||<span data-ttu-id="ed88f-626">選択したインストール スコープが次の場合 `meetings` 、このフィールドは使用可能な既定の機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-626">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="ed88f-627">オプション: `tab` `bot` 、、または `connector` 。</span><span class="sxs-lookup"><span data-stu-id="ed88f-627">Options: `tab`, `bot`, or `connector`.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="ed88f-628">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="ed88f-628">configurableProperties</span></span>

<span data-ttu-id="ed88f-629">**オプション** - 配列</span><span class="sxs-lookup"><span data-stu-id="ed88f-629">**Optional** - array</span></span>

<span data-ttu-id="ed88f-630">この `configurableProperties` ブロックは、管理者がカスタマイズできるアプリTeams定義します。</span><span class="sxs-lookup"><span data-stu-id="ed88f-630">The `configurableProperties` block defines the app properties that Teams admins can customize.</span></span> <span data-ttu-id="ed88f-631">詳細については、「アプリのカスタマイズを [有効にする」を参照してください](~/concepts/design/enable-app-customization.md)。</span><span class="sxs-lookup"><span data-stu-id="ed88f-631">For more information, see [enable app customization](~/concepts/design/enable-app-customization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ed88f-632">少なくとも 1 つのプロパティを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed88f-632">A minimum of one property must be defined.</span></span> <span data-ttu-id="ed88f-633">このブロックでは、最大 9 つのプロパティを定義できます。</span><span class="sxs-lookup"><span data-stu-id="ed88f-633">You can define a maximum of nine properties in this block.</span></span>

<span data-ttu-id="ed88f-634">次のプロパティを定義できます。</span><span class="sxs-lookup"><span data-stu-id="ed88f-634">You can define any of the following properties:</span></span>

* <span data-ttu-id="ed88f-635">`name`: アプリの表示名。</span><span class="sxs-lookup"><span data-stu-id="ed88f-635">`name`: The app's display name.</span></span>
* <span data-ttu-id="ed88f-636">`shortDescription`: アプリの簡単な説明です。</span><span class="sxs-lookup"><span data-stu-id="ed88f-636">`shortDescription`: The app's short description.</span></span>
* <span data-ttu-id="ed88f-637">`longDescription`: アプリの詳細な説明。</span><span class="sxs-lookup"><span data-stu-id="ed88f-637">`longDescription`: The app's detailed description.</span></span>
* <span data-ttu-id="ed88f-638">`smallImageUrl`: アプリのアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="ed88f-638">`smallImageUrl`: The app's outline icon.</span></span>
* <span data-ttu-id="ed88f-639">`largeImageUrl`: アプリの色アイコン。</span><span class="sxs-lookup"><span data-stu-id="ed88f-639">`largeImageUrl`: The app's color icon.</span></span>
* <span data-ttu-id="ed88f-640">`accentColor`: アウトライン アイコンと組み合わせて、背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="ed88f-640">`accentColor`: The color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="ed88f-641">`developerUrl`: 開発者の Web サイトの HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="ed88f-641">`developerUrl`: The HTTPS URL of the developer's website.</span></span>
* <span data-ttu-id="ed88f-642">`privacyUrl`: 開発者のプライバシー ポリシーの HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="ed88f-642">`privacyUrl`: The HTTPS URL of the developer's privacy policy.</span></span>
* <span data-ttu-id="ed88f-643">`termsOfUseUrl`: 開発者の使用条件の HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="ed88f-643">`termsOfUseUrl`: The HTTPS URL of the developer's terms of use.</span></span>
