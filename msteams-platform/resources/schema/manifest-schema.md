---
title: マニフェスト スキーマ リファレンス
description: Microsoft Teams のマニフェスト スキーマについて説明します。
ms.topic: reference
keywords: teams マニフェスト スキーマ
author: laujan
ms.author: lajanuar
ms.openlocfilehash: 8fff56d229cc137df8356b06214893dc984396a0
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014608"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="0b592-104">リファレンス: Microsoft Teams のマニフェスト スキーマ</span><span class="sxs-lookup"><span data-stu-id="0b592-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="0b592-105">Microsoft Teams マニフェストは、アプリが Microsoft Teams 製品に統合される方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0b592-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="0b592-106">マニフェストは、ホストされているスキーマに準拠している必要があります [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="0b592-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="0b592-107">以前のバージョンの 1.0-1.4 もサポートされています (URL で "v1.x" を使用)。</span><span class="sxs-lookup"><span data-stu-id="0b592-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="0b592-108">次のスキーマ サンプルは、すべての拡張オプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="0b592-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="0b592-109">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="0b592-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.8",
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
  }
}
```

<span data-ttu-id="0b592-110">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="0b592-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="0b592-111">$schema</span><span class="sxs-lookup"><span data-stu-id="0b592-111">$schema</span></span>

<span data-ttu-id="0b592-112">*省略可能、ただし推奨* — 文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="0b592-113">次https://マニフェストの JSON スキーマを参照する URL を示します。</span><span class="sxs-lookup"><span data-stu-id="0b592-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="0b592-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="0b592-114">manifestVersion</span></span>

<span data-ttu-id="0b592-115">**必須** — 文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-115">**Required** — string</span></span>

<span data-ttu-id="0b592-116">このマニフェストが使用しているマニフェスト スキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="0b592-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="0b592-117">"1.7" である必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-117">It should be "1.7".</span></span>

## <a name="version"></a><span data-ttu-id="0b592-118">version</span><span class="sxs-lookup"><span data-stu-id="0b592-118">version</span></span>

<span data-ttu-id="0b592-119">**必須** — 文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-119">**Required** — string</span></span>

<span data-ttu-id="0b592-120">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="0b592-120">The version of the specific app.</span></span> <span data-ttu-id="0b592-121">マニフェストで何かを更新する場合は、バージョンもインクリメントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="0b592-122">このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。</span><span class="sxs-lookup"><span data-stu-id="0b592-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="0b592-123">このアプリがストアに提出された場合、新しいマニフェストを再送信して再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="0b592-124">その後、このアプリのユーザーは、承認された数時間後に新しい更新されたマニフェストを自動的に取得します。</span><span class="sxs-lookup"><span data-stu-id="0b592-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="0b592-125">アプリがアクセス許可の変更を要求した場合、ユーザーはアプリのアップグレードと再同意を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b592-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="0b592-126">このバージョン文字列は [、semver](http://semver.org/) 標準 (MAJOR.マイナー。PATCH)。</span><span class="sxs-lookup"><span data-stu-id="0b592-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="0b592-127">id</span><span class="sxs-lookup"><span data-stu-id="0b592-127">id</span></span>

<span data-ttu-id="0b592-128">**必須** — Microsoft アプリ ID</span><span class="sxs-lookup"><span data-stu-id="0b592-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="0b592-129">このアプリの Microsoft によって生成された一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="0b592-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="0b592-130">Microsoft Bot Framework 経由でボットを登録した場合、またはタブの Web アプリが既に Microsoft にサインインしている場合は、既に ID を持っている必要があります。この ID をここに入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="0b592-131">それ以外の場合は、Microsoft アプリケーション登録ポータル ([マイ](https://apps.dev.microsoft.com)アプリケーション) で新しい ID を生成し、ここに入力して、ボットを追加するときに再利用する必要があります。注: AppSource で既存のアプリに更新プログラムを提出する場合は、マニフェスト内の ID を変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="0b592-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="0b592-132">developer</span><span class="sxs-lookup"><span data-stu-id="0b592-132">developer</span></span>

<span data-ttu-id="0b592-133">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="0b592-133">**Required** — object</span></span>

<span data-ttu-id="0b592-134">会社に関する情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-134">Specifies information about your company.</span></span> <span data-ttu-id="0b592-135">AppSource (以前はストアOffice提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="0b592-136">追加情報については [、発行ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b592-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="0b592-137">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-137">Name</span></span>| <span data-ttu-id="0b592-138">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-138">Maximum size</span></span> | <span data-ttu-id="0b592-139">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-139">Required</span></span> | <span data-ttu-id="0b592-140">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="0b592-141">32 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-141">32 characters</span></span>|<span data-ttu-id="0b592-142">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-142">✔</span></span>|<span data-ttu-id="0b592-143">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="0b592-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="0b592-144">2048 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-144">2048 characters</span></span>|<span data-ttu-id="0b592-145">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-145">✔</span></span>|<span data-ttu-id="0b592-146">このhttps://の Web サイトの URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="0b592-147">このリンクをクリックすると、ユーザーは会社または製品固有のランディング ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="0b592-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="0b592-148">2048 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-148">2048 characters</span></span>|<span data-ttu-id="0b592-149">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-149">✔</span></span>|<span data-ttu-id="0b592-150">このhttps://開発者のプライバシー ポリシーの URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="0b592-151">2048 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-151">2048 characters</span></span>|<span data-ttu-id="0b592-152">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-152">✔</span></span>|<span data-ttu-id="0b592-153">このhttps://開発者の利用規約の URL を示します。</span><span class="sxs-lookup"><span data-stu-id="0b592-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="0b592-154">10 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-154">10 characters</span></span>| |<span data-ttu-id="0b592-155">**省略可能** アプリを構築するパートナー組織を識別する Microsoft Partner Network ID。</span><span class="sxs-lookup"><span data-stu-id="0b592-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="0b592-156">name</span><span class="sxs-lookup"><span data-stu-id="0b592-156">name</span></span>

<span data-ttu-id="0b592-157">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="0b592-157">**Required** — object</span></span>

<span data-ttu-id="0b592-158">Teams エクスペリエンスでユーザーに表示されるアプリ エクスペリエンスの名前。</span><span class="sxs-lookup"><span data-stu-id="0b592-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="0b592-159">AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="0b592-160">値は `short` 同じで `full` 、同じにすべきではありません。</span><span class="sxs-lookup"><span data-stu-id="0b592-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="0b592-161">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-161">Name</span></span>| <span data-ttu-id="0b592-162">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-162">Maximum size</span></span> | <span data-ttu-id="0b592-163">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-163">Required</span></span> | <span data-ttu-id="0b592-164">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="0b592-165">30 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-165">30 characters</span></span>|<span data-ttu-id="0b592-166">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-166">✔</span></span>|<span data-ttu-id="0b592-167">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="0b592-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="0b592-168">100 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-168">100 characters</span></span>||<span data-ttu-id="0b592-169">完全なアプリ名が 30 文字を超える場合に使用される、アプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="0b592-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="0b592-170">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-170">description</span></span>

<span data-ttu-id="0b592-171">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="0b592-171">**Required** — object</span></span>

<span data-ttu-id="0b592-172">アプリをユーザーに説明します。</span><span class="sxs-lookup"><span data-stu-id="0b592-172">Describes your app to users.</span></span> <span data-ttu-id="0b592-173">AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="0b592-174">説明がエクスペリエンスを正確に説明し、潜在的な顧客がエクスペリエンスの内容を理解するのに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="0b592-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="0b592-175">また、外部アカウントの使用が必要な場合は、完全な説明で注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="0b592-176">値は `short` 同じで `full` 、同じにすべきではありません。</span><span class="sxs-lookup"><span data-stu-id="0b592-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="0b592-177">短い説明は、詳細な説明の中で繰り返さず、他のアプリ名を含めずにしてください。</span><span class="sxs-lookup"><span data-stu-id="0b592-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="0b592-178">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-178">Name</span></span>| <span data-ttu-id="0b592-179">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-179">Maximum size</span></span> | <span data-ttu-id="0b592-180">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-180">Required</span></span> | <span data-ttu-id="0b592-181">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="0b592-182">80 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-182">80 characters</span></span>|<span data-ttu-id="0b592-183">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-183">✔</span></span>|<span data-ttu-id="0b592-184">スペースが制限されている場合に使用される、アプリのエクスペリエンスの簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="0b592-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="0b592-185">4,000 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-185">4000 characters</span></span>|<span data-ttu-id="0b592-186">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-186">✔</span></span>|<span data-ttu-id="0b592-187">アプリの完全な説明。</span><span class="sxs-lookup"><span data-stu-id="0b592-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="0b592-188">packageName</span><span class="sxs-lookup"><span data-stu-id="0b592-188">packageName</span></span>

<span data-ttu-id="0b592-189">**省略可能** - 文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-189">**Optional** — string</span></span>

<span data-ttu-id="0b592-190">逆引きドメイン表記でのこのアプリの一意の識別子。たとえば、com.example.myapp などです。</span><span class="sxs-lookup"><span data-stu-id="0b592-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="0b592-191">最大長: 64 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="0b592-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="0b592-192">localizationInfo</span></span>

<span data-ttu-id="0b592-193">**オプション** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="0b592-193">**Optional** — object</span></span>

<span data-ttu-id="0b592-194">既定の言語の指定と、追加の言語ファイルへのポインターを許可します。</span><span class="sxs-lookup"><span data-stu-id="0b592-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="0b592-195">ローカライズを [参照してください](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="0b592-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="0b592-196">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-196">Name</span></span>| <span data-ttu-id="0b592-197">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-197">Maximum size</span></span> | <span data-ttu-id="0b592-198">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-198">Required</span></span> | <span data-ttu-id="0b592-199">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="0b592-200">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-200">✔</span></span>|<span data-ttu-id="0b592-201">このトップ レベルのマニフェスト ファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="0b592-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="0b592-202">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="0b592-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="0b592-203">追加の言語翻訳を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="0b592-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="0b592-204">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-204">Name</span></span>| <span data-ttu-id="0b592-205">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-205">Maximum size</span></span> | <span data-ttu-id="0b592-206">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-206">Required</span></span> | <span data-ttu-id="0b592-207">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="0b592-208">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-208">✔</span></span>|<span data-ttu-id="0b592-209">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="0b592-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="0b592-210">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-210">✔</span></span>|<span data-ttu-id="0b592-211">翻訳された文字列を含む .json ファイルへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="0b592-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="0b592-212">アイコン</span><span class="sxs-lookup"><span data-stu-id="0b592-212">icons</span></span>

<span data-ttu-id="0b592-213">**必須** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="0b592-213">**Required** — object</span></span>

<span data-ttu-id="0b592-214">Teams アプリ内で使用されるアイコン。</span><span class="sxs-lookup"><span data-stu-id="0b592-214">Icons used within the Teams app.</span></span> <span data-ttu-id="0b592-215">アイコン ファイルは、アップロード パッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="0b592-216">詳細 [については、「アイコン](../../concepts/build-and-test/apps-package.md#app-icons) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b592-216">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="0b592-217">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-217">Name</span></span>| <span data-ttu-id="0b592-218">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-218">Maximum size</span></span> | <span data-ttu-id="0b592-219">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-219">Required</span></span> | <span data-ttu-id="0b592-220">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="0b592-221">32 x 32 ピクセル</span><span class="sxs-lookup"><span data-stu-id="0b592-221">32 x 32 pixels</span></span>|<span data-ttu-id="0b592-222">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-222">✔</span></span>|<span data-ttu-id="0b592-223">透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="0b592-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="0b592-224">192 x 192 ピクセル</span><span class="sxs-lookup"><span data-stu-id="0b592-224">192 x 192 pixels</span></span>|<span data-ttu-id="0b592-225">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-225">✔</span></span>|<span data-ttu-id="0b592-226">フル カラーの 192x192 PNG アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="0b592-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="0b592-227">accentColor</span><span class="sxs-lookup"><span data-stu-id="0b592-227">accentColor</span></span>

<span data-ttu-id="0b592-228">**省略可能** - HTML 16 進カラー コード</span><span class="sxs-lookup"><span data-stu-id="0b592-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="0b592-229">アウトライン アイコンと組み合わせて使用し、背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="0b592-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="0b592-230">値は、'#' で始まる有効な HTML カラー コードである必要があります。次に例を示します `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="0b592-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="0b592-231">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="0b592-231">configurableTabs</span></span>

<span data-ttu-id="0b592-232">**省略可能** - 配列</span><span class="sxs-lookup"><span data-stu-id="0b592-232">**Optional** — array</span></span>

<span data-ttu-id="0b592-233">アプリエクスペリエンスにチーム チャネル タブ エクスペリエンスが含み、追加する前に追加の構成が必要な場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="0b592-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="0b592-234">構成可能なタブはチーム スコープでのみサポートされ (個人用ではなく)、現在サポートされているのはアプリごとに 1 つのタブのみです。</span><span class="sxs-lookup"><span data-stu-id="0b592-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="0b592-235">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-235">Name</span></span>| <span data-ttu-id="0b592-236">型</span><span class="sxs-lookup"><span data-stu-id="0b592-236">Type</span></span>| <span data-ttu-id="0b592-237">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-237">Maximum size</span></span> | <span data-ttu-id="0b592-238">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-238">Required</span></span> | <span data-ttu-id="0b592-239">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="0b592-240">string</span><span class="sxs-lookup"><span data-stu-id="0b592-240">string</span></span>|<span data-ttu-id="0b592-241">2048 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-241">2048 characters</span></span>|<span data-ttu-id="0b592-242">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-242">✔</span></span>|<span data-ttu-id="0b592-243">タブhttps://するときに使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="0b592-244">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-244">array of enums</span></span>|<span data-ttu-id="0b592-245">1 </span><span class="sxs-lookup"><span data-stu-id="0b592-245">1</span></span>|<span data-ttu-id="0b592-246">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-246">✔</span></span>|<span data-ttu-id="0b592-247">現在、構成可能なタブは、スコープ `team` とスコープのみを `groupchat` サポートしています。</span><span class="sxs-lookup"><span data-stu-id="0b592-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="0b592-248">ブール値</span><span class="sxs-lookup"><span data-stu-id="0b592-248">boolean</span></span>|||<span data-ttu-id="0b592-249">タブの構成のインスタンスを作成後にユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="0b592-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="0b592-250">既定値: **true 。**</span><span class="sxs-lookup"><span data-stu-id="0b592-250">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="0b592-251">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-251">array of enums</span></span>|<span data-ttu-id="0b592-252">6 </span><span class="sxs-lookup"><span data-stu-id="0b592-252">6</span></span>||<span data-ttu-id="0b592-253">タブが `contextItem` サポートされているスコープのセット。</span><span class="sxs-lookup"><span data-stu-id="0b592-253">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="0b592-254">既定値: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="0b592-254">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="0b592-255">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-255">string</span></span>|<span data-ttu-id="0b592-256">2048</span><span class="sxs-lookup"><span data-stu-id="0b592-256">2048</span></span>||<span data-ttu-id="0b592-257">SharePoint で使用するタブ プレビュー イメージへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="0b592-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="0b592-258">サイズ 1024x768。</span><span class="sxs-lookup"><span data-stu-id="0b592-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="0b592-259">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-259">array of enums</span></span>|<span data-ttu-id="0b592-260">1 </span><span class="sxs-lookup"><span data-stu-id="0b592-260">1</span></span>||<span data-ttu-id="0b592-261">SharePoint でタブを使用する方法を定義します。</span><span class="sxs-lookup"><span data-stu-id="0b592-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="0b592-262">オプション `sharePointFullPage` は次のとおりです。 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="0b592-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="0b592-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="0b592-263">staticTabs</span></span>

<span data-ttu-id="0b592-264">**省略可能** - 配列</span><span class="sxs-lookup"><span data-stu-id="0b592-264">**Optional** — array</span></span>

<span data-ttu-id="0b592-265">ユーザーが手動で追加することなく、既定で "ピン留め" できる一連のタブを定義します。</span><span class="sxs-lookup"><span data-stu-id="0b592-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="0b592-266">スコープ内で宣言された静的タブ `personal` は、常にアプリの個人用エクスペリエンスに固定されます。</span><span class="sxs-lookup"><span data-stu-id="0b592-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="0b592-267">このスコープで宣言されている静的 `team` タブは現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="0b592-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="0b592-268">この項目は、型のすべての要素を持つ配列 (最大 16 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="0b592-268">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="0b592-269">このブロックは、静的タブ ソリューションを提供するソリューションでのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="0b592-269">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="0b592-270">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-270">Name</span></span>| <span data-ttu-id="0b592-271">型</span><span class="sxs-lookup"><span data-stu-id="0b592-271">Type</span></span>| <span data-ttu-id="0b592-272">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-272">Maximum size</span></span> | <span data-ttu-id="0b592-273">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-273">Required</span></span> | <span data-ttu-id="0b592-274">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-274">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="0b592-275">string</span><span class="sxs-lookup"><span data-stu-id="0b592-275">string</span></span>|<span data-ttu-id="0b592-276">64 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-276">64 characters</span></span>|<span data-ttu-id="0b592-277">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-277">✔</span></span>|<span data-ttu-id="0b592-278">タブが表示されるエンティティの一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="0b592-278">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="0b592-279">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-279">string</span></span>|<span data-ttu-id="0b592-280">128 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-280">128 characters</span></span>|<span data-ttu-id="0b592-281">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-281">✔</span></span>|<span data-ttu-id="0b592-282">チャネル インターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="0b592-282">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="0b592-283">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-283">string</span></span>||<span data-ttu-id="0b592-284">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-284">✔</span></span>|<span data-ttu-id="0b592-285">次https:// Teams キャンバスに表示されるエンティティ UI を示す URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-285">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="0b592-286">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-286">string</span></span>|||<span data-ttu-id="0b592-287">ユーザー https://ブラウザーで表示することを選択した場合にポイントする URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-287">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="0b592-288">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-288">string</span></span>|||<span data-ttu-id="0b592-289">ユーザー https://の検索クエリを指す URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-289">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="0b592-290">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-290">array of enums</span></span>|<span data-ttu-id="0b592-291">1 </span><span class="sxs-lookup"><span data-stu-id="0b592-291">1</span></span>|<span data-ttu-id="0b592-292">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-292">✔</span></span>|<span data-ttu-id="0b592-293">現在、静的タブはスコープのみをサポートしています。つまり、個人用エクスペリエンスの一部としてのみ `personal` プロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="0b592-293">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="0b592-294">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-294">array of enums</span></span>| <span data-ttu-id="0b592-295">2</span><span class="sxs-lookup"><span data-stu-id="0b592-295">2</span></span>|| <span data-ttu-id="0b592-296">タブが `contextItem` サポートされているスコープのセット。</span><span class="sxs-lookup"><span data-stu-id="0b592-296">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="0b592-297">タブに関連するコンテンツを表示したり、認証フローを開始したりするためにコンテキストに依存する情報が必要な場合は、「Microsoft Teams タブのコンテキストを[取得する」を参照してください](../../tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="0b592-297">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="0b592-298">bots</span><span class="sxs-lookup"><span data-stu-id="0b592-298">bots</span></span>

<span data-ttu-id="0b592-299">**省略可能** - 配列</span><span class="sxs-lookup"><span data-stu-id="0b592-299">**Optional** — array</span></span>

<span data-ttu-id="0b592-300">既定のコマンド プロパティなどのオプションの情報と共に、ボット ソリューションを定義します。</span><span class="sxs-lookup"><span data-stu-id="0b592-300">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="0b592-301">アイテムは、型のすべての要素を持つ配列 (現在、1 つのボットにつき 1 つのボットしか許可されていない要素が最大 &mdash; 1 つ) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="0b592-301">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="0b592-302">このブロックは、ボット エクスペリエンスを提供するソリューションでのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="0b592-302">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="0b592-303">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-303">Name</span></span>| <span data-ttu-id="0b592-304">型</span><span class="sxs-lookup"><span data-stu-id="0b592-304">Type</span></span>| <span data-ttu-id="0b592-305">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-305">Maximum size</span></span> | <span data-ttu-id="0b592-306">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-306">Required</span></span> | <span data-ttu-id="0b592-307">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-307">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="0b592-308">string</span><span class="sxs-lookup"><span data-stu-id="0b592-308">string</span></span>|<span data-ttu-id="0b592-309">64 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-309">64 characters</span></span>|<span data-ttu-id="0b592-310">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-310">✔</span></span>|<span data-ttu-id="0b592-311">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="0b592-311">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="0b592-312">これは、アプリ全体の ID と同じ [場合があります](#id)。</span><span class="sxs-lookup"><span data-stu-id="0b592-312">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="0b592-313">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-313">array of enums</span></span>|<span data-ttu-id="0b592-314">3</span><span class="sxs-lookup"><span data-stu-id="0b592-314">3</span></span>|<span data-ttu-id="0b592-315">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-315">✔</span></span>|<span data-ttu-id="0b592-316">ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-316">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="0b592-317">これらのオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="0b592-317">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="0b592-318">ブール値</span><span class="sxs-lookup"><span data-stu-id="0b592-318">boolean</span></span>|||<span data-ttu-id="0b592-319">ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。</span><span class="sxs-lookup"><span data-stu-id="0b592-319">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="0b592-320">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="0b592-320">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="0b592-321">ブール値</span><span class="sxs-lookup"><span data-stu-id="0b592-321">boolean</span></span>|||<span data-ttu-id="0b592-322">ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="0b592-322">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="0b592-323">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="0b592-323">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="0b592-324">ブール値</span><span class="sxs-lookup"><span data-stu-id="0b592-324">boolean</span></span>|||<span data-ttu-id="0b592-325">パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="0b592-325">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="0b592-326">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="0b592-326">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="0b592-327">ブール値</span><span class="sxs-lookup"><span data-stu-id="0b592-327">boolean</span></span>|||<span data-ttu-id="0b592-328">ボットが音声通話をサポートする場所を示す値。</span><span class="sxs-lookup"><span data-stu-id="0b592-328">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="0b592-329">**重要**: このプロパティは現在試験的です。</span><span class="sxs-lookup"><span data-stu-id="0b592-329">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="0b592-330">試験的なプロパティは完全ではなく、完全に使用可能になる前に変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-330">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="0b592-331">テストと調査のみを目的として提供され、実稼働アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="0b592-331">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="0b592-332">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="0b592-332">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="0b592-333">ブール値</span><span class="sxs-lookup"><span data-stu-id="0b592-333">boolean</span></span>|||<span data-ttu-id="0b592-334">ボットがビデオ通話をサポートする場所を示す値。</span><span class="sxs-lookup"><span data-stu-id="0b592-334">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="0b592-335">**重要**: このプロパティは現在試験的です。</span><span class="sxs-lookup"><span data-stu-id="0b592-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="0b592-336">試験的なプロパティは完全ではなく、完全に使用可能になる前に変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="0b592-337">テストと調査のみを目的として提供され、実稼働アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="0b592-337">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="0b592-338">既定値: **`false`**</span><span class="sxs-lookup"><span data-stu-id="0b592-338">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="0b592-339">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="0b592-339">bots.commandLists</span></span>

<span data-ttu-id="0b592-340">ボットがユーザーに推奨できるコマンドのオプションの一覧。</span><span class="sxs-lookup"><span data-stu-id="0b592-340">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="0b592-341">オブジェクトは、型のすべての要素を持つ配列 (最大 2 つの要素) です。ボットがサポートするスコープごとに個別のコマンド リストを定義 `object` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-341">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="0b592-342">詳細 [については、「ボット メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0b592-342">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="0b592-343">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-343">Name</span></span>| <span data-ttu-id="0b592-344">型</span><span class="sxs-lookup"><span data-stu-id="0b592-344">Type</span></span>| <span data-ttu-id="0b592-345">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-345">Maximum size</span></span> | <span data-ttu-id="0b592-346">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-346">Required</span></span> | <span data-ttu-id="0b592-347">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-347">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="0b592-348">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-348">array of enums</span></span>|<span data-ttu-id="0b592-349">3</span><span class="sxs-lookup"><span data-stu-id="0b592-349">3</span></span>|<span data-ttu-id="0b592-350">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-350">✔</span></span>|<span data-ttu-id="0b592-351">コマンド リストが有効なスコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-351">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="0b592-352">`team`、`personal`、`groupchat` の中から選択できます。</span><span class="sxs-lookup"><span data-stu-id="0b592-352">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="0b592-353">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="0b592-353">array of objects</span></span>|<span data-ttu-id="0b592-354">10 </span><span class="sxs-lookup"><span data-stu-id="0b592-354">10</span></span>|<span data-ttu-id="0b592-355">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-355">✔</span></span>|<span data-ttu-id="0b592-356">ボットがサポートするコマンドの配列:</span><span class="sxs-lookup"><span data-stu-id="0b592-356">An array of commands the bot supports:</span></span><br><span data-ttu-id="0b592-357">`title`: ボット コマンドの名前 (文字列、32)</span><span class="sxs-lookup"><span data-stu-id="0b592-357">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="0b592-358">`description`: コマンドの構文およびその構文の引数
の簡単な説明または例 (文字列、128)</span><span class="sxs-lookup"><span data-stu-id="0b592-358">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="0b592-359">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="0b592-359">bots.commandLists.commands</span></span>

|<span data-ttu-id="0b592-360">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-360">Name</span></span>| <span data-ttu-id="0b592-361">型</span><span class="sxs-lookup"><span data-stu-id="0b592-361">Type</span></span>| <span data-ttu-id="0b592-362">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-362">Maximum size</span></span> | <span data-ttu-id="0b592-363">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-363">Required</span></span> | <span data-ttu-id="0b592-364">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-364">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="0b592-365">title</span><span class="sxs-lookup"><span data-stu-id="0b592-365">title</span></span>|<span data-ttu-id="0b592-366">string</span><span class="sxs-lookup"><span data-stu-id="0b592-366">string</span></span>|<span data-ttu-id="0b592-367">12 </span><span class="sxs-lookup"><span data-stu-id="0b592-367">12</span></span>|<span data-ttu-id="0b592-368">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-368">✔</span></span>|<span data-ttu-id="0b592-369">ボット コマンド名</span><span class="sxs-lookup"><span data-stu-id="0b592-369">The bot command name</span></span>|
|<span data-ttu-id="0b592-370">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-370">description</span></span>|<span data-ttu-id="0b592-371">string</span><span class="sxs-lookup"><span data-stu-id="0b592-371">string</span></span>|<span data-ttu-id="0b592-372">128 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-372">128 characters</span></span>|<span data-ttu-id="0b592-373">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-373">✔</span></span>|<span data-ttu-id="0b592-374">単純なテキストの説明、またはコマンド構文とその引数の例。</span><span class="sxs-lookup"><span data-stu-id="0b592-374">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="0b592-375">コネクタ</span><span class="sxs-lookup"><span data-stu-id="0b592-375">connectors</span></span>

<span data-ttu-id="0b592-376">**省略可能** - 配列</span><span class="sxs-lookup"><span data-stu-id="0b592-376">**Optional** — array</span></span>

<span data-ttu-id="0b592-377">ブロック `connectors` は、アプリの Office 365 コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="0b592-377">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="0b592-378">オブジェクトは、すべての型の要素を持つ配列 (最大 1 つの要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="0b592-378">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="0b592-379">このブロックは、コネクタを提供するソリューションでのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="0b592-379">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="0b592-380">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-380">Name</span></span>| <span data-ttu-id="0b592-381">型</span><span class="sxs-lookup"><span data-stu-id="0b592-381">Type</span></span>| <span data-ttu-id="0b592-382">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-382">Maximum size</span></span> | <span data-ttu-id="0b592-383">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-383">Required</span></span> | <span data-ttu-id="0b592-384">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-384">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="0b592-385">string</span><span class="sxs-lookup"><span data-stu-id="0b592-385">string</span></span>|<span data-ttu-id="0b592-386">2048 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-386">2048 characters</span></span>|<span data-ttu-id="0b592-387">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-387">✔</span></span>|<span data-ttu-id="0b592-388">コネクタhttps://するときに使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-388">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="0b592-389">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-389">array of enums</span></span>|<span data-ttu-id="0b592-390">1 </span><span class="sxs-lookup"><span data-stu-id="0b592-390">1</span></span>|<span data-ttu-id="0b592-391">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-391">✔</span></span>|<span data-ttu-id="0b592-392">コネクタがチャネルのコンテキストでエクスペリエンスを提供するか、または個々のユーザーを対象範囲としたエクスペリエンス `team` () を提供するかどうかを指定します `personal` 。</span><span class="sxs-lookup"><span data-stu-id="0b592-392">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="0b592-393">現時点では、 `team` スコープだけがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="0b592-393">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="0b592-394">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-394">string</span></span>|<span data-ttu-id="0b592-395">64 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-395">64 characters</span></span>|<span data-ttu-id="0b592-396">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-396">✔</span></span>|<span data-ttu-id="0b592-397">コネクタ開発者ダッシュボードの ID と一致するコネクタの一 [意の識別子](https://aka.ms/connectorsdashboard)。</span><span class="sxs-lookup"><span data-stu-id="0b592-397">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="0b592-398">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="0b592-398">composeExtensions</span></span>

<span data-ttu-id="0b592-399">**省略可能** - 配列</span><span class="sxs-lookup"><span data-stu-id="0b592-399">**Optional** — array</span></span>

<span data-ttu-id="0b592-400">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="0b592-400">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="0b592-401">この機能の名前は、2017 年 11 月に "作成拡張機能" から "メッセージング拡張機能" に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は変わりません。</span><span class="sxs-lookup"><span data-stu-id="0b592-401">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="0b592-402">アイテムは配列 (最大 1 要素) で、すべての型の要素が含まれます `object` 。</span><span class="sxs-lookup"><span data-stu-id="0b592-402">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="0b592-403">このブロックは、メッセージング拡張機能を提供するソリューションでのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="0b592-403">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="0b592-404">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-404">Name</span></span>| <span data-ttu-id="0b592-405">種類</span><span class="sxs-lookup"><span data-stu-id="0b592-405">Type</span></span> | <span data-ttu-id="0b592-406">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-406">Maximum Size</span></span> | <span data-ttu-id="0b592-407">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-407">Required</span></span> | <span data-ttu-id="0b592-408">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-408">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="0b592-409">string</span><span class="sxs-lookup"><span data-stu-id="0b592-409">string</span></span>|<span data-ttu-id="0b592-410">64</span><span class="sxs-lookup"><span data-stu-id="0b592-410">64</span></span>|<span data-ttu-id="0b592-411">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-411">✔</span></span>|<span data-ttu-id="0b592-412">Bot Framework に登録されている、メッセージング拡張機能をサポートするボットの一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="0b592-412">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="0b592-413">これは、アプリ全体の ID と同じ場合があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-413">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="0b592-414">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="0b592-414">array of objects</span></span>|<span data-ttu-id="0b592-415">10 </span><span class="sxs-lookup"><span data-stu-id="0b592-415">10</span></span>|<span data-ttu-id="0b592-416">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-416">✔</span></span>|<span data-ttu-id="0b592-417">メッセージング拡張機能がサポートするコマンドの配列</span><span class="sxs-lookup"><span data-stu-id="0b592-417">Array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="0b592-418">ブール値</span><span class="sxs-lookup"><span data-stu-id="0b592-418">boolean</span></span>|||<span data-ttu-id="0b592-419">ユーザーがメッセージング拡張機能の構成を更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="0b592-419">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="0b592-420">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="0b592-420">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="0b592-421">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="0b592-421">array of Objects</span></span>|<span data-ttu-id="0b592-422">5 </span><span class="sxs-lookup"><span data-stu-id="0b592-422">5</span></span>||<span data-ttu-id="0b592-423">特定の条件が満たされた場合にアプリを呼び出すことができるハンドラーの一覧。</span><span class="sxs-lookup"><span data-stu-id="0b592-423">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="0b592-424">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-424">string</span></span>|||<span data-ttu-id="0b592-425">メッセージ ハンドラーの種類。</span><span class="sxs-lookup"><span data-stu-id="0b592-425">The type of message handler.</span></span> <span data-ttu-id="0b592-426">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-426">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="0b592-427">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-427">array of Strings</span></span>|||<span data-ttu-id="0b592-428">リンク メッセージ ハンドラーが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="0b592-428">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="0b592-429">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="0b592-429">composeExtensions.commands</span></span>

<span data-ttu-id="0b592-430">メッセージング拡張機能では、1 つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-430">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="0b592-431">各コマンドは、UI ベースのエントリ ポイントからの潜在的な対話操作として Microsoft Teams に表示されます。</span><span class="sxs-lookup"><span data-stu-id="0b592-431">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="0b592-432">最大 10 のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="0b592-432">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="0b592-433">各コマンド項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="0b592-433">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="0b592-434">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-434">Name</span></span>| <span data-ttu-id="0b592-435">型</span><span class="sxs-lookup"><span data-stu-id="0b592-435">Type</span></span>| <span data-ttu-id="0b592-436">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-436">Maximum size</span></span> | <span data-ttu-id="0b592-437">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-437">Required</span></span> | <span data-ttu-id="0b592-438">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-438">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="0b592-439">string</span><span class="sxs-lookup"><span data-stu-id="0b592-439">string</span></span>|<span data-ttu-id="0b592-440">64 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-440">64 characters</span></span>|<span data-ttu-id="0b592-441">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-441">✔</span></span>|<span data-ttu-id="0b592-442">コマンドの ID。</span><span class="sxs-lookup"><span data-stu-id="0b592-442">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="0b592-443">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-443">string</span></span>|<span data-ttu-id="0b592-444">32 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-444">32 characters</span></span>|<span data-ttu-id="0b592-445">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-445">✔</span></span>|<span data-ttu-id="0b592-446">ユーザーに分かしいコマンド名。</span><span class="sxs-lookup"><span data-stu-id="0b592-446">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="0b592-447">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-447">string</span></span>|<span data-ttu-id="0b592-448">64 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-448">64 characters</span></span>||<span data-ttu-id="0b592-449">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="0b592-449">Type of the command.</span></span> <span data-ttu-id="0b592-450">次のいずれかを `query` 指定します `action` 。</span><span class="sxs-lookup"><span data-stu-id="0b592-450">One of `query` or `action`.</span></span> <span data-ttu-id="0b592-451">既定値: **クエリ** です。</span><span class="sxs-lookup"><span data-stu-id="0b592-451">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="0b592-452">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-452">string</span></span>|<span data-ttu-id="0b592-453">128 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-453">128 characters</span></span>||<span data-ttu-id="0b592-454">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="0b592-454">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="0b592-455">ブール値</span><span class="sxs-lookup"><span data-stu-id="0b592-455">boolean</span></span>|||<span data-ttu-id="0b592-456">パラメーターを指定してコマンドを最初に実行するかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="0b592-456">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="0b592-457">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="0b592-457">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="0b592-458">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-458">array of Strings</span></span>|<span data-ttu-id="0b592-459">3</span><span class="sxs-lookup"><span data-stu-id="0b592-459">3</span></span>||<span data-ttu-id="0b592-460">メッセージ拡張を呼び出すことができる場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="0b592-460">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="0b592-461">`compose`, の任意の `commandBox` 組み合 `message` わせ。</span><span class="sxs-lookup"><span data-stu-id="0b592-461">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="0b592-462">既定値は `["compose","commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="0b592-462">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="0b592-463">ブール値</span><span class="sxs-lookup"><span data-stu-id="0b592-463">boolean</span></span>|||<span data-ttu-id="0b592-464">タスク モジュールを動的にフェッチする必要かどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="0b592-464">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="0b592-465">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="0b592-465">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="0b592-466">object</span><span class="sxs-lookup"><span data-stu-id="0b592-466">object</span></span>|||<span data-ttu-id="0b592-467">メッセージング拡張機能コマンドを使用するときに事前読み込むタスク モジュールを指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-467">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="0b592-468">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-468">string</span></span>|<span data-ttu-id="0b592-469">64 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-469">64 characters</span></span>||<span data-ttu-id="0b592-470">最初のダイアログ タイトル。</span><span class="sxs-lookup"><span data-stu-id="0b592-470">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="0b592-471">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-471">string</span></span>|||<span data-ttu-id="0b592-472">ダイアログの幅: ピクセル単位の数値、または 'large'、'medium'、'small' などの既定のレイアウトのどちらかです。</span><span class="sxs-lookup"><span data-stu-id="0b592-472">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="0b592-473">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-473">string</span></span>|||<span data-ttu-id="0b592-474">ダイアログの高さ : ピクセル単位の数値、または 'large'、'medium'、'small' などの既定のレイアウトのどちらかです。</span><span class="sxs-lookup"><span data-stu-id="0b592-474">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="0b592-475">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-475">string</span></span>|||<span data-ttu-id="0b592-476">最初の Webview URL。</span><span class="sxs-lookup"><span data-stu-id="0b592-476">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="0b592-477">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="0b592-477">array of object</span></span>|<span data-ttu-id="0b592-478">5 アイテム</span><span class="sxs-lookup"><span data-stu-id="0b592-478">5 items</span></span>|<span data-ttu-id="0b592-479">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-479">✔</span></span>|<span data-ttu-id="0b592-480">コマンドが受け取るパラメーターの一覧。</span><span class="sxs-lookup"><span data-stu-id="0b592-480">The list of parameters the command takes.</span></span> <span data-ttu-id="0b592-481">最小: 1;最大: 5。</span><span class="sxs-lookup"><span data-stu-id="0b592-481">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="0b592-482">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-482">string</span></span>|<span data-ttu-id="0b592-483">64 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-483">64 characters</span></span>|<span data-ttu-id="0b592-484">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-484">✔</span></span>|<span data-ttu-id="0b592-485">クライアントに表示されるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="0b592-485">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="0b592-486">これはユーザー要求に含まれます。</span><span class="sxs-lookup"><span data-stu-id="0b592-486">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="0b592-487">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-487">string</span></span>|<span data-ttu-id="0b592-488">32 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-488">32 characters</span></span>|<span data-ttu-id="0b592-489">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-489">✔</span></span>|<span data-ttu-id="0b592-490">パラメーターのユーザー フレンドリーなタイトル。</span><span class="sxs-lookup"><span data-stu-id="0b592-490">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="0b592-491">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-491">string</span></span>|<span data-ttu-id="0b592-492">128 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-492">128 characters</span></span>||<span data-ttu-id="0b592-493">このパラメーターの目的を説明するユーザー フレンドリーな文字列。</span><span class="sxs-lookup"><span data-stu-id="0b592-493">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="0b592-494">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-494">string</span></span>|<span data-ttu-id="0b592-495">512 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-495">512 characters</span></span>||<span data-ttu-id="0b592-496">パラメーターの初期値。</span><span class="sxs-lookup"><span data-stu-id="0b592-496">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="0b592-497">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-497">string</span></span>|<span data-ttu-id="0b592-498">128 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-498">128 characters</span></span>||<span data-ttu-id="0b592-499">タスク モジュールに表示されるコントロールの種類を定義します `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="0b592-499">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="0b592-500">の 1 つ `text, textarea, number, date, time, toggle, choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="0b592-500">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="0b592-501">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="0b592-501">array of objects</span></span>|<span data-ttu-id="0b592-502">10 アイテム</span><span class="sxs-lookup"><span data-stu-id="0b592-502">10 items</span></span>||<span data-ttu-id="0b592-503">The choice options for the `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="0b592-503">The choice options for the`choiceset`.</span></span> <span data-ttu-id="0b592-504">次の場合にのみ `parameter.inputType` 使用します `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="0b592-504">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="0b592-505">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-505">string</span></span>|<span data-ttu-id="0b592-506">128 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-506">128 characters</span></span>|<span data-ttu-id="0b592-507">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-507">✔</span></span>|<span data-ttu-id="0b592-508">選択したタイトル。</span><span class="sxs-lookup"><span data-stu-id="0b592-508">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="0b592-509">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-509">string</span></span>|<span data-ttu-id="0b592-510">512 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-510">512 characters</span></span>|<span data-ttu-id="0b592-511">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-511">✔</span></span>|<span data-ttu-id="0b592-512">Value of the choice.</span><span class="sxs-lookup"><span data-stu-id="0b592-512">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="0b592-513">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="0b592-513">permissions</span></span>

<span data-ttu-id="0b592-514">**省略** 可能 - 文字列の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-514">**Optional** — array of strings</span></span>

<span data-ttu-id="0b592-515">アプリが要求するアクセス許可を指定する配列です。エンド ユーザーは拡張機能の実行 `string` 方法を知っています。</span><span class="sxs-lookup"><span data-stu-id="0b592-515">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="0b592-516">次のオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="0b592-516">The following options are non-exclusive:</span></span>

* <span data-ttu-id="0b592-517">`identity`&emsp;ユーザー ID 情報が必要</span><span class="sxs-lookup"><span data-stu-id="0b592-517">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="0b592-518">`messageTeamMembers`&emsp;チーム メンバーに直接メッセージを送信するためのアクセス許可が必要</span><span class="sxs-lookup"><span data-stu-id="0b592-518">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="0b592-519">アプリの更新時にこれらのアクセス許可を変更すると、ユーザーは更新されたアプリを初めて実行するときに同意プロセスを繰り返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-519">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="0b592-520">詳 [しくは、「アプリの更新」](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0b592-520">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="0b592-521">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="0b592-521">devicePermissions</span></span>

<span data-ttu-id="0b592-522">**省略** 可能 - 文字列の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-522">**Optional** — array of strings</span></span>

<span data-ttu-id="0b592-523">アプリがアクセスを要求できるユーザーのデバイスのネイティブ機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-523">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="0b592-524">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="0b592-524">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="0b592-525">validDomains</span><span class="sxs-lookup"><span data-stu-id="0b592-525">validDomains</span></span>

<span data-ttu-id="0b592-526">**省略** 可能 (省略 **可能(省略可能)、省略可能 (** 省略可能)、省略可能 (省略可能)</span><span class="sxs-lookup"><span data-stu-id="0b592-526">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="0b592-527">アプリが Teams クライアント内で読み込む Web サイトの有効なドメインの一覧。</span><span class="sxs-lookup"><span data-stu-id="0b592-527">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="0b592-528">たとえば、ドメイン一覧にはワイルドカードを含めできます `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="0b592-528">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="0b592-529">これは、ドメインの 1 つのセグメントと正確に一致します。if you need to match `a.b.example.com` then use `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="0b592-529">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="0b592-530">タブ構成またはコンテンツ UI で、タブ構成に使用するドメイン以外のドメインに移動する必要がある場合は、ここでそのドメインを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-530">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="0b592-531">ただし、 **アプリ** でサポートする ID プロバイダーのドメインを含める必要はありません。</span><span class="sxs-lookup"><span data-stu-id="0b592-531">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="0b592-532">たとえば、Google ID を使用して認証するには、accounts.google.com にリダイレクトする必要がありますが、accounts.google.com含めず `validDomains[]` にしてください。</span><span class="sxs-lookup"><span data-stu-id="0b592-532">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="0b592-533">機能するために独自の SharePoint URL を必要とする Teams アプリでは、有効なドメイン リストに "{teamsitedomain}" が含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-533">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b592-534">直接またはワイルドカードを介して、制御の外部にあるドメインを追加しません。</span><span class="sxs-lookup"><span data-stu-id="0b592-534">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="0b592-535">たとえば、有効 `yourapp.onmicrosoft.com` ですが、 `*.onmicrosoft.com` 無効です。</span><span class="sxs-lookup"><span data-stu-id="0b592-535">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="0b592-536">オブジェクトは、型のすべての要素を持つ配列です `string` 。</span><span class="sxs-lookup"><span data-stu-id="0b592-536">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="0b592-537">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="0b592-537">webApplicationInfo</span></span>

<span data-ttu-id="0b592-538">**オプション** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="0b592-538">**Optional** — object</span></span>

<span data-ttu-id="0b592-539">Azure Active Directory (Azure AD) アプリ ID と Microsoft Graph 情報を指定して、ユーザーがアプリにシームレスにサインインするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="0b592-539">Specify your Azure Active Directory (Azure AD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="0b592-540">アプリが Azure AD に登録されている場合は、管理者が Teams 管理センターでアクセス許可を簡単に確認し、同意を付与できるよう、アプリ ID を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-540">If your app is registered in Azure AD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="0b592-541">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-541">Name</span></span>| <span data-ttu-id="0b592-542">型</span><span class="sxs-lookup"><span data-stu-id="0b592-542">Type</span></span>| <span data-ttu-id="0b592-543">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-543">Maximum size</span></span> | <span data-ttu-id="0b592-544">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-544">Required</span></span> | <span data-ttu-id="0b592-545">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-545">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="0b592-546">string</span><span class="sxs-lookup"><span data-stu-id="0b592-546">string</span></span>|<span data-ttu-id="0b592-547">36 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-547">36 characters</span></span>|<span data-ttu-id="0b592-548">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-548">✔</span></span>|<span data-ttu-id="0b592-549">アプリの AAD アプリケーション ID。</span><span class="sxs-lookup"><span data-stu-id="0b592-549">AAD application id of the app.</span></span> <span data-ttu-id="0b592-550">この ID は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-550">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="0b592-551">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-551">string</span></span>|<span data-ttu-id="0b592-552">2048 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-552">2048 characters</span></span>|<span data-ttu-id="0b592-553">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-553">✔</span></span>|<span data-ttu-id="0b592-554">SSO の認証トークンを取得するためのアプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="0b592-554">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="0b592-555">**注:** SSO を使用していない場合は、エラー応答を回避するために、このフィールドにダミー文字列値をアプリ マニフェストに入力 https://notapplicable してください。</span><span class="sxs-lookup"><span data-stu-id="0b592-555">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="0b592-556">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="0b592-556">array of strings</span></span>|<span data-ttu-id="0b592-557">128 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-557">128 characters</span></span>||<span data-ttu-id="0b592-558">詳細なリソース [固有の同意を指定します](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="0b592-558">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="0b592-559">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="0b592-559">showLoadingIndicator</span></span>

<span data-ttu-id="0b592-560">**省略可能** - ブール値</span><span class="sxs-lookup"><span data-stu-id="0b592-560">**Optional** — boolean</span></span>

<span data-ttu-id="0b592-561">アプリ/タブの読み込み中に読み込みインジケーターを表示するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-561">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="0b592-562">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="0b592-562">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="0b592-563">アプリ マニフェストで "showLoadingIndicator : true" を設定した場合、ページが正しく読み込まれます。「ネイティブ読み込みインジケーター ドキュメントを表示する[](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)」で説明されているプロトコルに従って、タブとタスク モジュールのコンテンツ ページを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0b592-563">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="0b592-564">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="0b592-564">isFullScreen</span></span>

 <span data-ttu-id="0b592-565">**省略可能** - ブール値</span><span class="sxs-lookup"><span data-stu-id="0b592-565">**Optional** — boolean</span></span>

<span data-ttu-id="0b592-566">個人用アプリがタブ ヘッダー バーを使用してレンダリングされる場所または表示しない場所を示します。</span><span class="sxs-lookup"><span data-stu-id="0b592-566">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="0b592-567">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="0b592-567">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="0b592-568">アクティビティ</span><span class="sxs-lookup"><span data-stu-id="0b592-568">activities</span></span>

<span data-ttu-id="0b592-569">**オプション** — オブジェクト</span><span class="sxs-lookup"><span data-stu-id="0b592-569">**Optional** — object</span></span>

<span data-ttu-id="0b592-570">アプリがユーザー アクティビティ フィードに投稿するために使用するプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="0b592-570">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="0b592-571">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-571">Name</span></span>| <span data-ttu-id="0b592-572">型</span><span class="sxs-lookup"><span data-stu-id="0b592-572">Type</span></span>| <span data-ttu-id="0b592-573">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-573">Maximum size</span></span> | <span data-ttu-id="0b592-574">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-574">Required</span></span> | <span data-ttu-id="0b592-575">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-575">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="0b592-576">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="0b592-576">array of Objects</span></span>|<span data-ttu-id="0b592-577">128 アイテム</span><span class="sxs-lookup"><span data-stu-id="0b592-577">128 items</span></span>| | <span data-ttu-id="0b592-578">アプリがユーザー アクティビティ フィードに投稿できるアクティビティの種類を指定します。</span><span class="sxs-lookup"><span data-stu-id="0b592-578">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="0b592-579">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="0b592-579">activities.activityTypes</span></span>

|<span data-ttu-id="0b592-580">名前</span><span class="sxs-lookup"><span data-stu-id="0b592-580">Name</span></span>| <span data-ttu-id="0b592-581">型</span><span class="sxs-lookup"><span data-stu-id="0b592-581">Type</span></span>| <span data-ttu-id="0b592-582">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="0b592-582">Maximum size</span></span> | <span data-ttu-id="0b592-583">必須</span><span class="sxs-lookup"><span data-stu-id="0b592-583">Required</span></span> | <span data-ttu-id="0b592-584">説明</span><span class="sxs-lookup"><span data-stu-id="0b592-584">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="0b592-585">string</span><span class="sxs-lookup"><span data-stu-id="0b592-585">string</span></span>|<span data-ttu-id="0b592-586">32 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-586">32 characters</span></span>|<span data-ttu-id="0b592-587">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-587">✔</span></span>|<span data-ttu-id="0b592-588">通知の種類。</span><span class="sxs-lookup"><span data-stu-id="0b592-588">The notification type.</span></span> <span data-ttu-id="0b592-589">*以下を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="0b592-589">*See below*.</span></span>|
|`description`|<span data-ttu-id="0b592-590">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-590">string</span></span>|<span data-ttu-id="0b592-591">128 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-591">128 characters</span></span>|<span data-ttu-id="0b592-592">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-592">✔</span></span>|<span data-ttu-id="0b592-593">通知の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="0b592-593">A brief description of the notification.</span></span> <span data-ttu-id="0b592-594">*以下を参照してください*。</span><span class="sxs-lookup"><span data-stu-id="0b592-594">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="0b592-595">文字列</span><span class="sxs-lookup"><span data-stu-id="0b592-595">string</span></span>|<span data-ttu-id="0b592-596">128 文字</span><span class="sxs-lookup"><span data-stu-id="0b592-596">128 characters</span></span>|<span data-ttu-id="0b592-597">✔</span><span class="sxs-lookup"><span data-stu-id="0b592-597">✔</span></span>|<span data-ttu-id="0b592-598">例: "{actor} created task {taskId} for you"</span><span class="sxs-lookup"><span data-stu-id="0b592-598">Ex: "{actor} created task {taskId} for you"</span></span>|

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
