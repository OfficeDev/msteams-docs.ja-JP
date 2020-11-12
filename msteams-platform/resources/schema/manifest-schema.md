---
title: マニフェストスキーマの参照
description: Microsoft Teams マニフェストでサポートされているスキーマについて説明します。
keywords: teams マニフェストスキーマ
author: laujan
ms.author: lajanuar
ms.openlocfilehash: a158f2ad760078e7d9d7ebb72589437136c24ac5
ms.sourcegitcommit: 0aeb60027f423d8ceff3b377db8c3efbb6da4d17
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "48997952"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="9503f-104">リファレンス: Microsoft Teams のマニフェストスキーマ</span><span class="sxs-lookup"><span data-stu-id="9503f-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="9503f-105">Microsoft Teams のマニフェストでは、アプリを Microsoft Teams 製品に統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="9503f-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="9503f-106">マニフェストは、でホストされているスキーマに準拠している必要があり [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) ます。</span><span class="sxs-lookup"><span data-stu-id="9503f-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="9503f-107">以前のバージョン 1.0-1.4 もサポートされています (URL で "v1" を使用します)。</span><span class="sxs-lookup"><span data-stu-id="9503f-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="9503f-108">次のスキーマサンプルは、すべての拡張オプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="9503f-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="9503f-109">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="9503f-109">Sample full manifest</span></span>

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

<span data-ttu-id="9503f-110">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="9503f-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="9503f-111">$schema</span><span class="sxs-lookup"><span data-stu-id="9503f-111">$schema</span></span>

<span data-ttu-id="9503f-112">*省略可能 (ただし推奨* ) 文字列</span><span class="sxs-lookup"><span data-stu-id="9503f-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="9503f-113">マニフェストの JSON スキーマを参照する https://URL。</span><span class="sxs-lookup"><span data-stu-id="9503f-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="9503f-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="9503f-114">manifestVersion</span></span>

<span data-ttu-id="9503f-115">**必須** -文字列</span><span class="sxs-lookup"><span data-stu-id="9503f-115">**Required** — string</span></span>

<span data-ttu-id="9503f-116">このマニフェストが使用しているマニフェストスキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="9503f-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="9503f-117">"1.7" である必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-117">It should be "1.7".</span></span>

## <a name="version"></a><span data-ttu-id="9503f-118">バージョン</span><span class="sxs-lookup"><span data-stu-id="9503f-118">version</span></span>

<span data-ttu-id="9503f-119">**必須** -文字列</span><span class="sxs-lookup"><span data-stu-id="9503f-119">**Required** — string</span></span>

<span data-ttu-id="9503f-120">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="9503f-120">The version of the specific app.</span></span> <span data-ttu-id="9503f-121">マニフェスト内の内容を更新する場合は、そのバージョンも同時にインクリメントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="9503f-122">このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。</span><span class="sxs-lookup"><span data-stu-id="9503f-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="9503f-123">このアプリがストアに送信された場合は、新しいマニフェストを再送信して再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="9503f-124">その後、このアプリのユーザーは、承認後に数時間以内に新しい更新されたマニフェストを自動的に取得します。</span><span class="sxs-lookup"><span data-stu-id="9503f-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="9503f-125">アプリによって要求されたアクセス許可が変更された場合、ユーザーはアプリをアップグレードして再同意するように求められます。</span><span class="sxs-lookup"><span data-stu-id="9503f-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="9503f-126">このバージョンの文字列は、 [semver](http://semver.org/) 標準 (メジャー) に従う必要があります。間隔.パッチ)。</span><span class="sxs-lookup"><span data-stu-id="9503f-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="9503f-127">id</span><span class="sxs-lookup"><span data-stu-id="9503f-127">id</span></span>

<span data-ttu-id="9503f-128">**必須** -MICROSOFT アプリ ID</span><span class="sxs-lookup"><span data-stu-id="9503f-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="9503f-129">このアプリの一意の Microsoft 生成識別子。</span><span class="sxs-lookup"><span data-stu-id="9503f-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="9503f-130">Microsoft Bot フレームワークを介して bot を登録した場合、またはタブの web アプリが Microsoft によって既にサインインしている場合は、既に ID があるので、ここで入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="9503f-131">それ以外の場合は、Microsoft アプリケーション登録ポータル ([My Applications](https://apps.dev.microsoft.com)) で新しい ID を生成し、ここで入力してから、bot を追加するときにそれを再利用する必要があります。注: AppSource で既存のアプリに更新を送信する場合は、マニフェスト内の ID を変更しないでください。</span><span class="sxs-lookup"><span data-stu-id="9503f-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="9503f-132">developer</span><span class="sxs-lookup"><span data-stu-id="9503f-132">developer</span></span>

<span data-ttu-id="9503f-133">**Required** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="9503f-133">**Required** — object</span></span>

<span data-ttu-id="9503f-134">会社に関する情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="9503f-134">Specifies information about your company.</span></span> <span data-ttu-id="9503f-135">AppSource (旧称 Office ストア) に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="9503f-136">追加情報については、 [発行に関するガイドライン](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9503f-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="9503f-137">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-137">Name</span></span>| <span data-ttu-id="9503f-138">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-138">Maximum size</span></span> | <span data-ttu-id="9503f-139">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-139">Required</span></span> | <span data-ttu-id="9503f-140">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="9503f-141">32文字</span><span class="sxs-lookup"><span data-stu-id="9503f-141">32 characters</span></span>|<span data-ttu-id="9503f-142">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-142">✔</span></span>|<span data-ttu-id="9503f-143">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="9503f-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="9503f-144">2048 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-144">2048 characters</span></span>|<span data-ttu-id="9503f-145">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-145">✔</span></span>|<span data-ttu-id="9503f-146">開発者の web サイトへの https://URL。</span><span class="sxs-lookup"><span data-stu-id="9503f-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="9503f-147">このリンクは、ユーザーを会社または製品固有のランディングページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="9503f-148">2048 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-148">2048 characters</span></span>|<span data-ttu-id="9503f-149">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-149">✔</span></span>|<span data-ttu-id="9503f-150">開発者のプライバシーポリシーへの https://URL。</span><span class="sxs-lookup"><span data-stu-id="9503f-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="9503f-151">2048 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-151">2048 characters</span></span>|<span data-ttu-id="9503f-152">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-152">✔</span></span>|<span data-ttu-id="9503f-153">開発者の使用条件への https://URL。</span><span class="sxs-lookup"><span data-stu-id="9503f-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="9503f-154">10文字</span><span class="sxs-lookup"><span data-stu-id="9503f-154">10 characters</span></span>| |<span data-ttu-id="9503f-155">**省略可能** アプリを構築するパートナー組織を識別する Microsoft パートナーのネットワーク ID。</span><span class="sxs-lookup"><span data-stu-id="9503f-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="9503f-156">name</span><span class="sxs-lookup"><span data-stu-id="9503f-156">name</span></span>

<span data-ttu-id="9503f-157">**Required** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="9503f-157">**Required** — object</span></span>

<span data-ttu-id="9503f-158">Teams でユーザーに表示されるアプリの動作の名前です。</span><span class="sxs-lookup"><span data-stu-id="9503f-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="9503f-159">AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="9503f-160">との値 `short` を同じにすることはでき `full` ません。</span><span class="sxs-lookup"><span data-stu-id="9503f-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="9503f-161">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-161">Name</span></span>| <span data-ttu-id="9503f-162">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-162">Maximum size</span></span> | <span data-ttu-id="9503f-163">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-163">Required</span></span> | <span data-ttu-id="9503f-164">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="9503f-165">30 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-165">30 characters</span></span>|<span data-ttu-id="9503f-166">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-166">✔</span></span>|<span data-ttu-id="9503f-167">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="9503f-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="9503f-168">100 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-168">100 characters</span></span>||<span data-ttu-id="9503f-169">アプリの完全な名前。アプリの完全な名前が30文字を超えている場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="9503f-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="9503f-170">description</span><span class="sxs-lookup"><span data-stu-id="9503f-170">description</span></span>

<span data-ttu-id="9503f-171">**Required** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="9503f-171">**Required** — object</span></span>

<span data-ttu-id="9503f-172">ユーザーに対してアプリを記述します。</span><span class="sxs-lookup"><span data-stu-id="9503f-172">Describes your app to users.</span></span> <span data-ttu-id="9503f-173">AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="9503f-174">説明に正確に表示されていることを確認し、お客様が快適な動作を理解するのに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="9503f-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="9503f-175">また、外部アカウントが使用するために必要な場合は、詳細な説明にも注意してください。</span><span class="sxs-lookup"><span data-stu-id="9503f-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="9503f-176">との値 `short` を同じにすることはでき `full` ません。</span><span class="sxs-lookup"><span data-stu-id="9503f-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="9503f-177">短い説明を長い説明の中で繰り返すことはできません。他のアプリ名を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="9503f-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="9503f-178">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-178">Name</span></span>| <span data-ttu-id="9503f-179">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-179">Maximum size</span></span> | <span data-ttu-id="9503f-180">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-180">Required</span></span> | <span data-ttu-id="9503f-181">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="9503f-182">80文字</span><span class="sxs-lookup"><span data-stu-id="9503f-182">80 characters</span></span>|<span data-ttu-id="9503f-183">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-183">✔</span></span>|<span data-ttu-id="9503f-184">スペースが制限されている場合に使用する、アプリの使用状況の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="9503f-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="9503f-185">4000文字</span><span class="sxs-lookup"><span data-stu-id="9503f-185">4000 characters</span></span>|<span data-ttu-id="9503f-186">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-186">✔</span></span>|<span data-ttu-id="9503f-187">アプリの詳細な説明。</span><span class="sxs-lookup"><span data-stu-id="9503f-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="9503f-188">packageName</span><span class="sxs-lookup"><span data-stu-id="9503f-188">packageName</span></span>

<span data-ttu-id="9503f-189">**省略可能** (string)</span><span class="sxs-lookup"><span data-stu-id="9503f-189">**Optional** — string</span></span>

<span data-ttu-id="9503f-190">逆引きドメイン表記でのこのアプリの一意識別子。たとえば、例のようになります。</span><span class="sxs-lookup"><span data-stu-id="9503f-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="9503f-191">最大長: 64 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="9503f-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="9503f-192">localizationInfo</span></span>

<span data-ttu-id="9503f-193">**Optional** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="9503f-193">**Optional** — object</span></span>

<span data-ttu-id="9503f-194">既定の言語の指定、および追加の言語ファイルへのポインターを許可します。</span><span class="sxs-lookup"><span data-stu-id="9503f-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="9503f-195">「 [ローカライズ](~/concepts/build-and-test/apps-localization.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9503f-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="9503f-196">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-196">Name</span></span>| <span data-ttu-id="9503f-197">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-197">Maximum size</span></span> | <span data-ttu-id="9503f-198">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-198">Required</span></span> | <span data-ttu-id="9503f-199">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="9503f-200">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-200">✔</span></span>|<span data-ttu-id="9503f-201">このトップレベルマニフェストファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="9503f-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="9503f-202">localizationInfo. additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="9503f-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="9503f-203">追加の言語の翻訳を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="9503f-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="9503f-204">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-204">Name</span></span>| <span data-ttu-id="9503f-205">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-205">Maximum size</span></span> | <span data-ttu-id="9503f-206">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-206">Required</span></span> | <span data-ttu-id="9503f-207">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="9503f-208">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-208">✔</span></span>|<span data-ttu-id="9503f-209">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="9503f-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="9503f-210">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-210">✔</span></span>|<span data-ttu-id="9503f-211">翻訳された文字列を含む json ファイルへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="9503f-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="9503f-212">アイコン</span><span class="sxs-lookup"><span data-stu-id="9503f-212">icons</span></span>

<span data-ttu-id="9503f-213">**Required** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="9503f-213">**Required** — object</span></span>

<span data-ttu-id="9503f-214">Teams アプリ内で使用されるアイコン。</span><span class="sxs-lookup"><span data-stu-id="9503f-214">Icons used within the Teams app.</span></span> <span data-ttu-id="9503f-215">アイコンファイルは、アップロードパッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="9503f-216">詳細については、「 [アイコン](~/concepts/build-and-test/apps-package.md#icons) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9503f-216">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="9503f-217">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-217">Name</span></span>| <span data-ttu-id="9503f-218">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-218">Maximum size</span></span> | <span data-ttu-id="9503f-219">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-219">Required</span></span> | <span data-ttu-id="9503f-220">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="9503f-221">32 x 32 ピクセル</span><span class="sxs-lookup"><span data-stu-id="9503f-221">32 x 32 pixels</span></span>|<span data-ttu-id="9503f-222">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-222">✔</span></span>|<span data-ttu-id="9503f-223">透明な32x32 の PNG アウトラインアイコンへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="9503f-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="9503f-224">192 x 192 ピクセル</span><span class="sxs-lookup"><span data-stu-id="9503f-224">192 x 192 pixels</span></span>|<span data-ttu-id="9503f-225">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-225">✔</span></span>|<span data-ttu-id="9503f-226">フルカラー 192x192 PNG アイコンへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="9503f-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="9503f-227">アクセントカラー</span><span class="sxs-lookup"><span data-stu-id="9503f-227">accentColor</span></span>

<span data-ttu-id="9503f-228">**オプション** -HTML 16 進カラーコード</span><span class="sxs-lookup"><span data-stu-id="9503f-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="9503f-229">とと組み合わせてアウトラインアイコンの背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="9503f-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="9503f-230">この値は、' # ' で始まる有効な HTML カラーコードである必要があります (例 `#4464ee` :)。</span><span class="sxs-lookup"><span data-stu-id="9503f-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="9503f-231">の各タブ</span><span class="sxs-lookup"><span data-stu-id="9503f-231">configurableTabs</span></span>

<span data-ttu-id="9503f-232">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="9503f-232">**Optional** — array</span></span>

<span data-ttu-id="9503f-233">アプリの機能に、追加の構成を必要とするチームチャネルのタブがある場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="9503f-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="9503f-234">構成可能なタブは teams スコープ (個人ではない) でのみサポートされており、現在、アプリごとに **1 つ** のタブのみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="9503f-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="9503f-235">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-235">Name</span></span>| <span data-ttu-id="9503f-236">型</span><span class="sxs-lookup"><span data-stu-id="9503f-236">Type</span></span>| <span data-ttu-id="9503f-237">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-237">Maximum size</span></span> | <span data-ttu-id="9503f-238">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-238">Required</span></span> | <span data-ttu-id="9503f-239">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="9503f-240">string</span><span class="sxs-lookup"><span data-stu-id="9503f-240">string</span></span>|<span data-ttu-id="9503f-241">2048 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-241">2048 characters</span></span>|<span data-ttu-id="9503f-242">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-242">✔</span></span>|<span data-ttu-id="9503f-243">タブを構成するときに使用する https://URL。</span><span class="sxs-lookup"><span data-stu-id="9503f-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="9503f-244">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-244">array of enums</span></span>|<span data-ttu-id="9503f-245">1 </span><span class="sxs-lookup"><span data-stu-id="9503f-245">1</span></span>|<span data-ttu-id="9503f-246">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-246">✔</span></span>|<span data-ttu-id="9503f-247">現在、構成可能なタブでは、およびスコープのみがサポートさ `team` `groupchat` れています。</span><span class="sxs-lookup"><span data-stu-id="9503f-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="9503f-248">ブール値</span><span class="sxs-lookup"><span data-stu-id="9503f-248">boolean</span></span>|||<span data-ttu-id="9503f-249">作成後にタブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="9503f-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="9503f-250">既定値は **true** です。</span><span class="sxs-lookup"><span data-stu-id="9503f-250">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="9503f-251">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-251">array of enums</span></span>|<span data-ttu-id="9503f-252">6 </span><span class="sxs-lookup"><span data-stu-id="9503f-252">6</span></span>||<span data-ttu-id="9503f-253">`contextItem`タブがサポートされているスコープのセット。</span><span class="sxs-lookup"><span data-stu-id="9503f-253">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="9503f-254">既定値: **[Channeltab、privateChatTab、meetingChatTab、会議の設定]** 。</span><span class="sxs-lookup"><span data-stu-id="9503f-254">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="9503f-255">string</span><span class="sxs-lookup"><span data-stu-id="9503f-255">string</span></span>|<span data-ttu-id="9503f-256">2048</span><span class="sxs-lookup"><span data-stu-id="9503f-256">2048</span></span>||<span data-ttu-id="9503f-257">SharePoint で使用するタブプレビュー画像への相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="9503f-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="9503f-258">サイズ1024x768。</span><span class="sxs-lookup"><span data-stu-id="9503f-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="9503f-259">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-259">array of enums</span></span>|<span data-ttu-id="9503f-260">1 </span><span class="sxs-lookup"><span data-stu-id="9503f-260">1</span></span>||<span data-ttu-id="9503f-261">SharePoint でどのようにタブを使用できるようにするかを定義します。</span><span class="sxs-lookup"><span data-stu-id="9503f-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="9503f-262">オプション `sharePointFullPage` と `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="9503f-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="9503f-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="9503f-263">staticTabs</span></span>

<span data-ttu-id="9503f-264">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="9503f-264">**Optional** — array</span></span>

<span data-ttu-id="9503f-265">ユーザーが手動で追加せずに、既定で "固定" できるタブのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="9503f-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="9503f-266">スコープ内で宣言 `personal` されている静的タブは、常にアプリの個人の環境に固定されます。</span><span class="sxs-lookup"><span data-stu-id="9503f-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="9503f-267">スコープ内で宣言されている静的タブ `team` は現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="9503f-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="9503f-268">この項目は、型のすべての要素を含む配列 (最大16個の要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="9503f-268">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="9503f-269">このブロックは、静的なタブソリューションを提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="9503f-269">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="9503f-270">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-270">Name</span></span>| <span data-ttu-id="9503f-271">型</span><span class="sxs-lookup"><span data-stu-id="9503f-271">Type</span></span>| <span data-ttu-id="9503f-272">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-272">Maximum size</span></span> | <span data-ttu-id="9503f-273">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-273">Required</span></span> | <span data-ttu-id="9503f-274">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-274">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="9503f-275">string</span><span class="sxs-lookup"><span data-stu-id="9503f-275">string</span></span>|<span data-ttu-id="9503f-276">64 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-276">64 characters</span></span>|<span data-ttu-id="9503f-277">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-277">✔</span></span>|<span data-ttu-id="9503f-278">タブに表示されるエンティティの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="9503f-278">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="9503f-279">string</span><span class="sxs-lookup"><span data-stu-id="9503f-279">string</span></span>|<span data-ttu-id="9503f-280">128文字</span><span class="sxs-lookup"><span data-stu-id="9503f-280">128 characters</span></span>|<span data-ttu-id="9503f-281">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-281">✔</span></span>|<span data-ttu-id="9503f-282">チャネルインターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="9503f-282">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="9503f-283">string</span><span class="sxs-lookup"><span data-stu-id="9503f-283">string</span></span>||<span data-ttu-id="9503f-284">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-284">✔</span></span>|<span data-ttu-id="9503f-285">Teams キャンバスに表示されるエンティティ UI をポイントする https://URL。</span><span class="sxs-lookup"><span data-stu-id="9503f-285">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="9503f-286">string</span><span class="sxs-lookup"><span data-stu-id="9503f-286">string</span></span>|||<span data-ttu-id="9503f-287">ユーザーがブラウザーで表示をポイントしたかどうかを示す https://URL。</span><span class="sxs-lookup"><span data-stu-id="9503f-287">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="9503f-288">string</span><span class="sxs-lookup"><span data-stu-id="9503f-288">string</span></span>|||<span data-ttu-id="9503f-289">ユーザーの検索クエリを指す https://URL。</span><span class="sxs-lookup"><span data-stu-id="9503f-289">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="9503f-290">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-290">array of enums</span></span>|<span data-ttu-id="9503f-291">1 </span><span class="sxs-lookup"><span data-stu-id="9503f-291">1</span></span>|<span data-ttu-id="9503f-292">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-292">✔</span></span>|<span data-ttu-id="9503f-293">現時点では、静的タブではスコープのみがサポート `personal` されます。つまり、個人の利便性の一環としてのみプロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="9503f-293">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="9503f-294">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-294">array of enums</span></span>| <span data-ttu-id="9503f-295">2 </span><span class="sxs-lookup"><span data-stu-id="9503f-295">2</span></span>|| <span data-ttu-id="9503f-296">`contextItem`タブがサポートされているスコープのセット。</span><span class="sxs-lookup"><span data-stu-id="9503f-296">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="9503f-297">関連するコンテンツを表示したり、認証フローを開始したりするために、タブにコンテキスト依存情報が必要な場合は、「 [Microsoft Teams のコンテキストを取得する」タブ](../../tabs/how-to/access-teams-context.md)を *参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="9503f-297">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="9503f-298">bot</span><span class="sxs-lookup"><span data-stu-id="9503f-298">bots</span></span>

<span data-ttu-id="9503f-299">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="9503f-299">**Optional** — array</span></span>

<span data-ttu-id="9503f-300">Bot ソリューションと、既定のコマンドプロパティなどのオプション情報を定義します。</span><span class="sxs-lookup"><span data-stu-id="9503f-300">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="9503f-301">アイテムが配列の場合 (現時点では1つの要素のみ &mdash; が可能)、その型のすべての要素が含まれ `object` ます。</span><span class="sxs-lookup"><span data-stu-id="9503f-301">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="9503f-302">このブロックは、bot の環境を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="9503f-302">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="9503f-303">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-303">Name</span></span>| <span data-ttu-id="9503f-304">型</span><span class="sxs-lookup"><span data-stu-id="9503f-304">Type</span></span>| <span data-ttu-id="9503f-305">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-305">Maximum size</span></span> | <span data-ttu-id="9503f-306">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-306">Required</span></span> | <span data-ttu-id="9503f-307">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-307">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="9503f-308">string</span><span class="sxs-lookup"><span data-stu-id="9503f-308">string</span></span>|<span data-ttu-id="9503f-309">64 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-309">64 characters</span></span>|<span data-ttu-id="9503f-310">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-310">✔</span></span>|<span data-ttu-id="9503f-311">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="9503f-311">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="9503f-312">これは、アプリの全体的な [ID](#id)と同じである場合もあります。</span><span class="sxs-lookup"><span data-stu-id="9503f-312">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="9503f-313">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-313">array of enums</span></span>|<span data-ttu-id="9503f-314">3 </span><span class="sxs-lookup"><span data-stu-id="9503f-314">3</span></span>|<span data-ttu-id="9503f-315">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-315">✔</span></span>|<span data-ttu-id="9503f-316">ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。</span><span class="sxs-lookup"><span data-stu-id="9503f-316">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="9503f-317">これらのオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="9503f-317">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="9503f-318">ブール値</span><span class="sxs-lookup"><span data-stu-id="9503f-318">boolean</span></span>|||<span data-ttu-id="9503f-319">ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。</span><span class="sxs-lookup"><span data-stu-id="9503f-319">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="9503f-320">限り **`false`**</span><span class="sxs-lookup"><span data-stu-id="9503f-320">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="9503f-321">ブール値</span><span class="sxs-lookup"><span data-stu-id="9503f-321">boolean</span></span>|||<span data-ttu-id="9503f-322">ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="9503f-322">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="9503f-323">限り `**false**`</span><span class="sxs-lookup"><span data-stu-id="9503f-323">Default: `**false**`</span></span>|
|`supportsFiles`|<span data-ttu-id="9503f-324">ブール値</span><span class="sxs-lookup"><span data-stu-id="9503f-324">boolean</span></span>|||<span data-ttu-id="9503f-325">パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="9503f-325">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="9503f-326">限り **`false`**</span><span class="sxs-lookup"><span data-stu-id="9503f-326">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="9503f-327">ブール値</span><span class="sxs-lookup"><span data-stu-id="9503f-327">boolean</span></span>|||<span data-ttu-id="9503f-328">Bot が音声通話をサポートするかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="9503f-328">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="9503f-329">**重要** : このプロパティは現在実験的なものです。</span><span class="sxs-lookup"><span data-stu-id="9503f-329">**IMPORTANT** : This property is currently experimental.</span></span> <span data-ttu-id="9503f-330">実験的なプロパティは完成していない可能性があり、完全に使用できるようになる前に変更が行われる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-330">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="9503f-331">テストと調査の目的でのみ提供されており、運用アプリケーションでは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="9503f-331">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="9503f-332">限り **`false`**</span><span class="sxs-lookup"><span data-stu-id="9503f-332">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="9503f-333">ブール値</span><span class="sxs-lookup"><span data-stu-id="9503f-333">boolean</span></span>|||<span data-ttu-id="9503f-334">Bot がビデオ通話をサポートする場所を示す値。</span><span class="sxs-lookup"><span data-stu-id="9503f-334">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="9503f-335">**重要** : このプロパティは現在実験的なものです。</span><span class="sxs-lookup"><span data-stu-id="9503f-335">**IMPORTANT** : This property is currently experimental.</span></span> <span data-ttu-id="9503f-336">実験的なプロパティは完成していない可能性があり、完全に使用できるようになる前に変更が行われる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="9503f-337">テストと調査の目的でのみ提供されており、運用アプリケーションでは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="9503f-337">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="9503f-338">限り **`false`**</span><span class="sxs-lookup"><span data-stu-id="9503f-338">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="9503f-339">bot リスト</span><span class="sxs-lookup"><span data-stu-id="9503f-339">bots.commandLists</span></span>

<span data-ttu-id="9503f-340">Bot がユーザーに推奨できるコマンドのオプションの一覧。</span><span class="sxs-lookup"><span data-stu-id="9503f-340">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="9503f-341">Object は、型のすべての要素を含む配列 (最大2つの要素) です `object` 。 bot がサポートするスコープごとに個別のコマンドリストを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-341">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="9503f-342">詳細については、「 [Bot メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9503f-342">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="9503f-343">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-343">Name</span></span>| <span data-ttu-id="9503f-344">型</span><span class="sxs-lookup"><span data-stu-id="9503f-344">Type</span></span>| <span data-ttu-id="9503f-345">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-345">Maximum size</span></span> | <span data-ttu-id="9503f-346">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-346">Required</span></span> | <span data-ttu-id="9503f-347">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-347">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="9503f-348">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-348">array of enums</span></span>|<span data-ttu-id="9503f-349">3 </span><span class="sxs-lookup"><span data-stu-id="9503f-349">3</span></span>|<span data-ttu-id="9503f-350">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-350">✔</span></span>|<span data-ttu-id="9503f-351">コマンド リストが有効なスコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="9503f-351">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="9503f-352">`team`、`personal`、`groupchat` の中から選択できます。</span><span class="sxs-lookup"><span data-stu-id="9503f-352">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="9503f-353">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="9503f-353">array of objects</span></span>|<span data-ttu-id="9503f-354">10  </span><span class="sxs-lookup"><span data-stu-id="9503f-354">10</span></span>|<span data-ttu-id="9503f-355">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-355">✔</span></span>|<span data-ttu-id="9503f-356">ボットがサポートするコマンドの配列:</span><span class="sxs-lookup"><span data-stu-id="9503f-356">An array of commands the bot supports:</span></span><br><span data-ttu-id="9503f-357">`title`: ボット コマンドの名前 (文字列、32)</span><span class="sxs-lookup"><span data-stu-id="9503f-357">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="9503f-358">`description`: コマンドの構文およびその構文の引数
の簡単な説明または例 (文字列、128)</span><span class="sxs-lookup"><span data-stu-id="9503f-358">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="9503f-359">bot のリストコマンド</span><span class="sxs-lookup"><span data-stu-id="9503f-359">bots.commandLists.commands</span></span>

|<span data-ttu-id="9503f-360">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-360">Name</span></span>| <span data-ttu-id="9503f-361">型</span><span class="sxs-lookup"><span data-stu-id="9503f-361">Type</span></span>| <span data-ttu-id="9503f-362">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-362">Maximum size</span></span> | <span data-ttu-id="9503f-363">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-363">Required</span></span> | <span data-ttu-id="9503f-364">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-364">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="9503f-365">title</span><span class="sxs-lookup"><span data-stu-id="9503f-365">title</span></span>|<span data-ttu-id="9503f-366">string</span><span class="sxs-lookup"><span data-stu-id="9503f-366">string</span></span>|<span data-ttu-id="9503f-367">12 </span><span class="sxs-lookup"><span data-stu-id="9503f-367">12</span></span>|<span data-ttu-id="9503f-368">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-368">✔</span></span>|<span data-ttu-id="9503f-369">Bot コマンド名</span><span class="sxs-lookup"><span data-stu-id="9503f-369">The bot command name</span></span>|
|<span data-ttu-id="9503f-370">description</span><span class="sxs-lookup"><span data-stu-id="9503f-370">description</span></span>|<span data-ttu-id="9503f-371">string</span><span class="sxs-lookup"><span data-stu-id="9503f-371">string</span></span>|<span data-ttu-id="9503f-372">128文字</span><span class="sxs-lookup"><span data-stu-id="9503f-372">128 characters</span></span>|<span data-ttu-id="9503f-373">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-373">✔</span></span>|<span data-ttu-id="9503f-374">簡単なテキストの説明、またはコマンド構文とその引数の例。</span><span class="sxs-lookup"><span data-stu-id="9503f-374">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="9503f-375">コネクタ</span><span class="sxs-lookup"><span data-stu-id="9503f-375">connectors</span></span>

<span data-ttu-id="9503f-376">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="9503f-376">**Optional** — array</span></span>

<span data-ttu-id="9503f-377">ブロックは、 `connectors` アプリの Office 365 コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="9503f-377">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="9503f-378">Object は、type のすべての要素を含む配列 (最大1つの要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="9503f-378">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="9503f-379">このブロックは、コネクタを提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="9503f-379">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="9503f-380">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-380">Name</span></span>| <span data-ttu-id="9503f-381">型</span><span class="sxs-lookup"><span data-stu-id="9503f-381">Type</span></span>| <span data-ttu-id="9503f-382">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-382">Maximum size</span></span> | <span data-ttu-id="9503f-383">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-383">Required</span></span> | <span data-ttu-id="9503f-384">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-384">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="9503f-385">string</span><span class="sxs-lookup"><span data-stu-id="9503f-385">string</span></span>|<span data-ttu-id="9503f-386">2048 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-386">2048 characters</span></span>|<span data-ttu-id="9503f-387">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-387">✔</span></span>|<span data-ttu-id="9503f-388">コネクタを構成するときに使用する https://URL。</span><span class="sxs-lookup"><span data-stu-id="9503f-388">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="9503f-389">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-389">array of enums</span></span>|<span data-ttu-id="9503f-390">1 </span><span class="sxs-lookup"><span data-stu-id="9503f-390">1</span></span>|<span data-ttu-id="9503f-391">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-391">✔</span></span>|<span data-ttu-id="9503f-392">コネクタが内のチャネルのコンテキストで、 `team` または個別のユーザー単独 () にスコープ設定された環境での動作を提供するかどうかを指定し `personal` ます。</span><span class="sxs-lookup"><span data-stu-id="9503f-392">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="9503f-393">現時点では、 `team` 範囲のみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="9503f-393">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="9503f-394">string</span><span class="sxs-lookup"><span data-stu-id="9503f-394">string</span></span>|<span data-ttu-id="9503f-395">64 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-395">64 characters</span></span>|<span data-ttu-id="9503f-396">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-396">✔</span></span>|<span data-ttu-id="9503f-397">コネクタ [開発者ダッシュボード](https://aka.ms/connectorsdashboard)の ID と一致するコネクタの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="9503f-397">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="9503f-398">この機能</span><span class="sxs-lookup"><span data-stu-id="9503f-398">composeExtensions</span></span>

<span data-ttu-id="9503f-399">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="9503f-399">**Optional** — array</span></span>

<span data-ttu-id="9503f-400">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="9503f-400">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="9503f-401">この機能の名前は、2017年11月に「[作成] 拡張機能」から「messaging extension」に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は同じままです。</span><span class="sxs-lookup"><span data-stu-id="9503f-401">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="9503f-402">Item は、type のすべての要素を含む配列 (最大1つの要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="9503f-402">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="9503f-403">このブロックは、メッセージング拡張機能を提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="9503f-403">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="9503f-404">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-404">Name</span></span>| <span data-ttu-id="9503f-405">型</span><span class="sxs-lookup"><span data-stu-id="9503f-405">Type</span></span> | <span data-ttu-id="9503f-406">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-406">Maximum Size</span></span> | <span data-ttu-id="9503f-407">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-407">Required</span></span> | <span data-ttu-id="9503f-408">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-408">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="9503f-409">string</span><span class="sxs-lookup"><span data-stu-id="9503f-409">string</span></span>|<span data-ttu-id="9503f-410">64</span><span class="sxs-lookup"><span data-stu-id="9503f-410">64</span></span>|<span data-ttu-id="9503f-411">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-411">✔</span></span>|<span data-ttu-id="9503f-412">Bot フレームワークに登録されているメッセージング拡張機能をバックアップする bot の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="9503f-412">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="9503f-413">これは、アプリの全体的な ID と同じである場合もあります。</span><span class="sxs-lookup"><span data-stu-id="9503f-413">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="9503f-414">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="9503f-414">array of objects</span></span>|<span data-ttu-id="9503f-415">10  </span><span class="sxs-lookup"><span data-stu-id="9503f-415">10</span></span>|<span data-ttu-id="9503f-416">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-416">✔</span></span>|<span data-ttu-id="9503f-417">メッセージング拡張機能がサポートするコマンドの配列</span><span class="sxs-lookup"><span data-stu-id="9503f-417">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="9503f-418">ブール値</span><span class="sxs-lookup"><span data-stu-id="9503f-418">boolean</span></span>|||<span data-ttu-id="9503f-419">メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="9503f-419">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="9503f-420">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="9503f-420">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="9503f-421">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="9503f-421">array of Objects</span></span>|<span data-ttu-id="9503f-422">5 </span><span class="sxs-lookup"><span data-stu-id="9503f-422">5</span></span>||<span data-ttu-id="9503f-423">特定の条件が満たされたときにアプリを呼び出せるようにするハンドラーの一覧。</span><span class="sxs-lookup"><span data-stu-id="9503f-423">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="9503f-424">ドメインも、にリストされている必要があります。 `validDomains`</span><span class="sxs-lookup"><span data-stu-id="9503f-424">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="9503f-425">string</span><span class="sxs-lookup"><span data-stu-id="9503f-425">string</span></span>|||<span data-ttu-id="9503f-426">メッセージハンドラの種類。</span><span class="sxs-lookup"><span data-stu-id="9503f-426">The type of message handler.</span></span> <span data-ttu-id="9503f-427">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-427">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="9503f-428">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-428">array of Strings</span></span>|||<span data-ttu-id="9503f-429">リンクメッセージハンドラが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="9503f-429">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="9503f-430">このコマンドの機能</span><span class="sxs-lookup"><span data-stu-id="9503f-430">composeExtensions.commands</span></span>

<span data-ttu-id="9503f-431">メッセージング拡張機能は、1つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-431">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="9503f-432">各コマンドは、Microsoft Teams に UI ベースのエントリポイントからの潜在的な操作として表示されます。</span><span class="sxs-lookup"><span data-stu-id="9503f-432">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="9503f-433">最大10個のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="9503f-433">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="9503f-434">各コマンド項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9503f-434">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="9503f-435">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-435">Name</span></span>| <span data-ttu-id="9503f-436">型</span><span class="sxs-lookup"><span data-stu-id="9503f-436">Type</span></span>| <span data-ttu-id="9503f-437">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-437">Maximum size</span></span> | <span data-ttu-id="9503f-438">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-438">Required</span></span> | <span data-ttu-id="9503f-439">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-439">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="9503f-440">string</span><span class="sxs-lookup"><span data-stu-id="9503f-440">string</span></span>|<span data-ttu-id="9503f-441">64 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-441">64 characters</span></span>|<span data-ttu-id="9503f-442">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-442">✔</span></span>|<span data-ttu-id="9503f-443">コマンドの ID。</span><span class="sxs-lookup"><span data-stu-id="9503f-443">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="9503f-444">string</span><span class="sxs-lookup"><span data-stu-id="9503f-444">string</span></span>|<span data-ttu-id="9503f-445">32文字</span><span class="sxs-lookup"><span data-stu-id="9503f-445">32 characters</span></span>|<span data-ttu-id="9503f-446">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-446">✔</span></span>|<span data-ttu-id="9503f-447">ユーザーフレンドリなコマンド名。</span><span class="sxs-lookup"><span data-stu-id="9503f-447">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="9503f-448">string</span><span class="sxs-lookup"><span data-stu-id="9503f-448">string</span></span>|<span data-ttu-id="9503f-449">64 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-449">64 characters</span></span>||<span data-ttu-id="9503f-450">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="9503f-450">Type of the command.</span></span> <span data-ttu-id="9503f-451">またはのいずれか `query` `action` です。</span><span class="sxs-lookup"><span data-stu-id="9503f-451">One of `query` or `action`.</span></span> <span data-ttu-id="9503f-452">既定値: **query** 。</span><span class="sxs-lookup"><span data-stu-id="9503f-452">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="9503f-453">string</span><span class="sxs-lookup"><span data-stu-id="9503f-453">string</span></span>|<span data-ttu-id="9503f-454">128文字</span><span class="sxs-lookup"><span data-stu-id="9503f-454">128 characters</span></span>||<span data-ttu-id="9503f-455">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="9503f-455">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="9503f-456">ブール値</span><span class="sxs-lookup"><span data-stu-id="9503f-456">boolean</span></span>|||<span data-ttu-id="9503f-457">パラメーターを指定せずにコマンドを最初に実行する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="9503f-457">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="9503f-458">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="9503f-458">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="9503f-459">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-459">array of Strings</span></span>|<span data-ttu-id="9503f-460">3 </span><span class="sxs-lookup"><span data-stu-id="9503f-460">3</span></span>||<span data-ttu-id="9503f-461">メッセージの内線番号をから呼び出すことができる場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="9503f-461">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="9503f-462">、、の任意の組み合わせ `compose` `commandBox` `message` 。</span><span class="sxs-lookup"><span data-stu-id="9503f-462">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="9503f-463">既定値は `["compose","commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="9503f-463">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="9503f-464">ブール値</span><span class="sxs-lookup"><span data-stu-id="9503f-464">boolean</span></span>|||<span data-ttu-id="9503f-465">タスクモジュールを動的にフェッチする必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="9503f-465">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="9503f-466">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="9503f-466">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="9503f-467">object</span><span class="sxs-lookup"><span data-stu-id="9503f-467">object</span></span>|||<span data-ttu-id="9503f-468">メッセージ拡張コマンドの使用時に、タスクモジュールを事前に読み込むように指定します。</span><span class="sxs-lookup"><span data-stu-id="9503f-468">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="9503f-469">string</span><span class="sxs-lookup"><span data-stu-id="9503f-469">string</span></span>|<span data-ttu-id="9503f-470">64 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-470">64 characters</span></span>||<span data-ttu-id="9503f-471">最初のダイアログのタイトル。</span><span class="sxs-lookup"><span data-stu-id="9503f-471">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="9503f-472">string</span><span class="sxs-lookup"><span data-stu-id="9503f-472">string</span></span>|||<span data-ttu-id="9503f-473">ダイアログの幅。ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="9503f-473">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="9503f-474">string</span><span class="sxs-lookup"><span data-stu-id="9503f-474">string</span></span>|||<span data-ttu-id="9503f-475">ダイアログの高さ-ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="9503f-475">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="9503f-476">string</span><span class="sxs-lookup"><span data-stu-id="9503f-476">string</span></span>|||<span data-ttu-id="9503f-477">最初の webview の URL。</span><span class="sxs-lookup"><span data-stu-id="9503f-477">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="9503f-478">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="9503f-478">array of object</span></span>|<span data-ttu-id="9503f-479">5アイテム</span><span class="sxs-lookup"><span data-stu-id="9503f-479">5 items</span></span>|<span data-ttu-id="9503f-480">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-480">✔</span></span>|<span data-ttu-id="9503f-481">コマンドが実行するパラメーターの一覧。</span><span class="sxs-lookup"><span data-stu-id="9503f-481">The list of parameters the command takes.</span></span> <span data-ttu-id="9503f-482">最小値: 1、最大: 5</span><span class="sxs-lookup"><span data-stu-id="9503f-482">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="9503f-483">string</span><span class="sxs-lookup"><span data-stu-id="9503f-483">string</span></span>|<span data-ttu-id="9503f-484">64 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-484">64 characters</span></span>|<span data-ttu-id="9503f-485">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-485">✔</span></span>|<span data-ttu-id="9503f-486">クライアントに表示されるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="9503f-486">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="9503f-487">これは、ユーザー要求に含まれています。</span><span class="sxs-lookup"><span data-stu-id="9503f-487">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="9503f-488">string</span><span class="sxs-lookup"><span data-stu-id="9503f-488">string</span></span>|<span data-ttu-id="9503f-489">32文字</span><span class="sxs-lookup"><span data-stu-id="9503f-489">32 characters</span></span>|<span data-ttu-id="9503f-490">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-490">✔</span></span>|<span data-ttu-id="9503f-491">パラメーターのユーザーフレンドリなタイトル。</span><span class="sxs-lookup"><span data-stu-id="9503f-491">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="9503f-492">string</span><span class="sxs-lookup"><span data-stu-id="9503f-492">string</span></span>|<span data-ttu-id="9503f-493">128文字</span><span class="sxs-lookup"><span data-stu-id="9503f-493">128 characters</span></span>||<span data-ttu-id="9503f-494">このパラメーターの目的を説明するユーザーフレンドリ文字列。</span><span class="sxs-lookup"><span data-stu-id="9503f-494">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="9503f-495">string</span><span class="sxs-lookup"><span data-stu-id="9503f-495">string</span></span>|<span data-ttu-id="9503f-496">512文字</span><span class="sxs-lookup"><span data-stu-id="9503f-496">512 characters</span></span>||<span data-ttu-id="9503f-497">パラメータの初期値。</span><span class="sxs-lookup"><span data-stu-id="9503f-497">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="9503f-498">string</span><span class="sxs-lookup"><span data-stu-id="9503f-498">string</span></span>|<span data-ttu-id="9503f-499">128文字</span><span class="sxs-lookup"><span data-stu-id="9503f-499">128 characters</span></span>||<span data-ttu-id="9503f-500">のタスクモジュールに表示されるコントロールの種類を定義 `fetchTask: true` します。</span><span class="sxs-lookup"><span data-stu-id="9503f-500">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="9503f-501">のいずれか `text, textarea, number, date, time, toggle, choiceset` です。</span><span class="sxs-lookup"><span data-stu-id="9503f-501">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="9503f-502">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="9503f-502">array of objects</span></span>|<span data-ttu-id="9503f-503">10アイテム</span><span class="sxs-lookup"><span data-stu-id="9503f-503">10 items</span></span>||<span data-ttu-id="9503f-504">の選択オプション `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="9503f-504">The choice options for the`choiceset`.</span></span> <span data-ttu-id="9503f-505">がである場合にのみ使用 `parameter.inputType` `choiceset` します。</span><span class="sxs-lookup"><span data-stu-id="9503f-505">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="9503f-506">string</span><span class="sxs-lookup"><span data-stu-id="9503f-506">string</span></span>|<span data-ttu-id="9503f-507">128文字</span><span class="sxs-lookup"><span data-stu-id="9503f-507">128 characters</span></span>|<span data-ttu-id="9503f-508">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-508">✔</span></span>|<span data-ttu-id="9503f-509">選択項目のタイトル。</span><span class="sxs-lookup"><span data-stu-id="9503f-509">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="9503f-510">string</span><span class="sxs-lookup"><span data-stu-id="9503f-510">string</span></span>|<span data-ttu-id="9503f-511">512文字</span><span class="sxs-lookup"><span data-stu-id="9503f-511">512 characters</span></span>|<span data-ttu-id="9503f-512">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-512">✔</span></span>|<span data-ttu-id="9503f-513">Value of the choice.</span><span class="sxs-lookup"><span data-stu-id="9503f-513">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="9503f-514">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="9503f-514">permissions</span></span>

<span data-ttu-id="9503f-515">**省略可能** -文字列の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-515">**Optional** — array of strings</span></span>

<span data-ttu-id="9503f-516">`string`アプリが要求するアクセス許可を指定する配列。これにより、エンドユーザーは拡張機能の動作を知ることができます。</span><span class="sxs-lookup"><span data-stu-id="9503f-516">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="9503f-517">非排他的なオプションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="9503f-517">The following options are non-exclusive:</span></span>

* <span data-ttu-id="9503f-518">`identity`&emsp;ユーザー id 情報が必要</span><span class="sxs-lookup"><span data-stu-id="9503f-518">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="9503f-519">`messageTeamMembers`&emsp;チームメンバーに直接メッセージを送信するためのアクセス許可が必要</span><span class="sxs-lookup"><span data-stu-id="9503f-519">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="9503f-520">アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは、更新されたアプリを初めて実行したときに同意プロセスを繰り返すようになります。</span><span class="sxs-lookup"><span data-stu-id="9503f-520">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="9503f-521">詳細については [、「アプリの更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9503f-521">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="9503f-522">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="9503f-522">devicePermissions</span></span>

<span data-ttu-id="9503f-523">**省略可能** -文字列の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-523">**Optional** — array of strings</span></span>

<span data-ttu-id="9503f-524">アプリがアクセスを要求することができる、ユーザーのデバイスのネイティブ機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="9503f-524">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="9503f-525">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="9503f-525">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="9503f-526">validDomains</span><span class="sxs-lookup"><span data-stu-id="9503f-526">validDomains</span></span>

<span data-ttu-id="9503f-527">**省略可能** (記載個所に **必要な** 場合を除く)</span><span class="sxs-lookup"><span data-stu-id="9503f-527">**Optional** , except **Required** where noted</span></span>

<span data-ttu-id="9503f-528">アプリが Teams クライアント内で読み込むことが想定されている web サイトの有効なドメインの一覧。</span><span class="sxs-lookup"><span data-stu-id="9503f-528">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="9503f-529">ドメインリストには、たとえば、ワイルドカードを含めることができ `*.example.com` ます。</span><span class="sxs-lookup"><span data-stu-id="9503f-529">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="9503f-530">これは、1つのドメインのセグメントに一致します。に一致させる必要がある場合は `a.b.example.com` 、を使用 `*.*.example.com` します。</span><span class="sxs-lookup"><span data-stu-id="9503f-530">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="9503f-531">タブ構成またはコンテンツ UI が他のドメインに移動する必要がある場合 (タブの構成に使用するものを除く)、そのドメインをここで指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-531">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="9503f-532">ただし、アプリでサポートする id プロバイダーのドメインを含める必要は **ありません** 。</span><span class="sxs-lookup"><span data-stu-id="9503f-532">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="9503f-533">たとえば、Google ID を使用して認証するには、accounts.google.com にリダイレクトする必要がありますが、に accounts.google.com を含めることはできません `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="9503f-533">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="9503f-534">自分の sharepoint Url が適切に機能する必要がある Teams アプリは、有効なドメインリストに "{teamsitedomain}" を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="9503f-534">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9503f-535">直接に、またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しないでください。</span><span class="sxs-lookup"><span data-stu-id="9503f-535">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="9503f-536">たとえば、は有効ですが、有効では `yourapp.onmicrosoft.com` `*.onmicrosoft.com` ありません。</span><span class="sxs-lookup"><span data-stu-id="9503f-536">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="9503f-537">Object は、型のすべての要素を含む配列です `string` 。</span><span class="sxs-lookup"><span data-stu-id="9503f-537">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="9503f-538">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="9503f-538">webApplicationInfo</span></span>

<span data-ttu-id="9503f-539">**Optional** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="9503f-539">**Optional** — object</span></span>

<span data-ttu-id="9503f-540">Aad アプリ ID とグラフ情報を指定して、ユーザーが AAD アプリにシームレスにサインインできるようにします。</span><span class="sxs-lookup"><span data-stu-id="9503f-540">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="9503f-541">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-541">Name</span></span>| <span data-ttu-id="9503f-542">型</span><span class="sxs-lookup"><span data-stu-id="9503f-542">Type</span></span>| <span data-ttu-id="9503f-543">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-543">Maximum size</span></span> | <span data-ttu-id="9503f-544">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-544">Required</span></span> | <span data-ttu-id="9503f-545">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-545">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="9503f-546">string</span><span class="sxs-lookup"><span data-stu-id="9503f-546">string</span></span>|<span data-ttu-id="9503f-547">36文字</span><span class="sxs-lookup"><span data-stu-id="9503f-547">36 characters</span></span>|<span data-ttu-id="9503f-548">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-548">✔</span></span>|<span data-ttu-id="9503f-549">アプリの AAD アプリケーション id。</span><span class="sxs-lookup"><span data-stu-id="9503f-549">AAD application id of the app.</span></span> <span data-ttu-id="9503f-550">この id は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-550">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="9503f-551">string</span><span class="sxs-lookup"><span data-stu-id="9503f-551">string</span></span>|<span data-ttu-id="9503f-552">2048 文字</span><span class="sxs-lookup"><span data-stu-id="9503f-552">2048 characters</span></span>||<span data-ttu-id="9503f-553">SSO の認証トークンを取得するためのアプリのリソース url。</span><span class="sxs-lookup"><span data-stu-id="9503f-553">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="9503f-554">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="9503f-554">array of strings</span></span>|<span data-ttu-id="9503f-555">128文字</span><span class="sxs-lookup"><span data-stu-id="9503f-555">128 characters</span></span>||<span data-ttu-id="9503f-556">[リソース固有の](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)詳細な同意を指定する</span><span class="sxs-lookup"><span data-stu-id="9503f-556">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="9503f-557">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="9503f-557">showLoadingIndicator</span></span>

<span data-ttu-id="9503f-558">**Optional** -boolean</span><span class="sxs-lookup"><span data-stu-id="9503f-558">**Optional** — boolean</span></span>

<span data-ttu-id="9503f-559">アプリ/タブが読み込まれているときに、読み込みインジケーターを表示するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="9503f-559">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="9503f-560">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="9503f-560">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="9503f-561">アプリマニフェストで "showLoadingIndicator: true" を設定した場合、ページが正しく読み込まれるようにするには、「 [ネイティブロードインジケーター](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) ドキュメントを表示する」で説明されているプロトコルに従って、タブおよびタスクモジュールのコンテンツページを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9503f-561">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="9503f-562">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="9503f-562">isFullScreen</span></span>

 <span data-ttu-id="9503f-563">**Optional** -boolean</span><span class="sxs-lookup"><span data-stu-id="9503f-563">**Optional** — boolean</span></span>

<span data-ttu-id="9503f-564">個人用アプリがタブヘッダーバーを使用して、または表示せずにレンダリングされる場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="9503f-564">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="9503f-565">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="9503f-565">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="9503f-566">アクティビティ</span><span class="sxs-lookup"><span data-stu-id="9503f-566">activities</span></span>

<span data-ttu-id="9503f-567">**Optional** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="9503f-567">**Optional** — object</span></span>

<span data-ttu-id="9503f-568">アプリがユーザーアクティビティフィードに投稿するときに使用するプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="9503f-568">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="9503f-569">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-569">Name</span></span>| <span data-ttu-id="9503f-570">型</span><span class="sxs-lookup"><span data-stu-id="9503f-570">Type</span></span>| <span data-ttu-id="9503f-571">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-571">Maximum size</span></span> | <span data-ttu-id="9503f-572">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-572">Required</span></span> | <span data-ttu-id="9503f-573">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-573">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="9503f-574">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="9503f-574">array of Objects</span></span>|<span data-ttu-id="9503f-575">128アイテム</span><span class="sxs-lookup"><span data-stu-id="9503f-575">128 items</span></span>| | <span data-ttu-id="9503f-576">アプリがユーザーアクティビティフィードに投稿できるアクティビティの種類を指定します。</span><span class="sxs-lookup"><span data-stu-id="9503f-576">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="9503f-577">アクティビティの種類</span><span class="sxs-lookup"><span data-stu-id="9503f-577">activities.activityTypes</span></span>

|<span data-ttu-id="9503f-578">名前</span><span class="sxs-lookup"><span data-stu-id="9503f-578">Name</span></span>| <span data-ttu-id="9503f-579">型</span><span class="sxs-lookup"><span data-stu-id="9503f-579">Type</span></span>| <span data-ttu-id="9503f-580">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="9503f-580">Maximum size</span></span> | <span data-ttu-id="9503f-581">必須</span><span class="sxs-lookup"><span data-stu-id="9503f-581">Required</span></span> | <span data-ttu-id="9503f-582">説明</span><span class="sxs-lookup"><span data-stu-id="9503f-582">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="9503f-583">string</span><span class="sxs-lookup"><span data-stu-id="9503f-583">string</span></span>|<span data-ttu-id="9503f-584">32文字</span><span class="sxs-lookup"><span data-stu-id="9503f-584">32 characters</span></span>|<span data-ttu-id="9503f-585">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-585">✔</span></span>|<span data-ttu-id="9503f-586">通知の種類。</span><span class="sxs-lookup"><span data-stu-id="9503f-586">The notification type.</span></span> <span data-ttu-id="9503f-587">*以下を参照して* ください。</span><span class="sxs-lookup"><span data-stu-id="9503f-587">*See below*.</span></span>|
|`description`|<span data-ttu-id="9503f-588">string</span><span class="sxs-lookup"><span data-stu-id="9503f-588">string</span></span>|<span data-ttu-id="9503f-589">128文字</span><span class="sxs-lookup"><span data-stu-id="9503f-589">128 characters</span></span>|<span data-ttu-id="9503f-590">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-590">✔</span></span>|<span data-ttu-id="9503f-591">通知の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="9503f-591">A brief description of the notification.</span></span> <span data-ttu-id="9503f-592">*以下を参照して* ください。</span><span class="sxs-lookup"><span data-stu-id="9503f-592">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="9503f-593">string</span><span class="sxs-lookup"><span data-stu-id="9503f-593">string</span></span>|<span data-ttu-id="9503f-594">128文字</span><span class="sxs-lookup"><span data-stu-id="9503f-594">128 characters</span></span>|<span data-ttu-id="9503f-595">✔</span><span class="sxs-lookup"><span data-stu-id="9503f-595">✔</span></span>|<span data-ttu-id="9503f-596">Ex: "{actor} ' のタスク {taskId} が作成されました"</span><span class="sxs-lookup"><span data-stu-id="9503f-596">Ex: "{actor} created task {taskId} for you"</span></span>|

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
