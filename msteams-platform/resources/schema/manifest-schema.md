---
title: マニフェストスキーマの参照
description: Microsoft Teams のマニフェストスキーマについて説明します。
keywords: teams マニフェストスキーマ
author: laujan
ms.author: lajanuar
ms.openlocfilehash: e25f50fc8da357553c1f0a8b01dc51af079ed2bb
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604614"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="fb691-104">リファレンス: Microsoft Teams のマニフェストスキーマ</span><span class="sxs-lookup"><span data-stu-id="fb691-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="fb691-105">Microsoft Teams のマニフェストでは、アプリを Microsoft Teams 製品に統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="fb691-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="fb691-106">マニフェストは、でホストされているスキーマに準拠している必要があり [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) ます。</span><span class="sxs-lookup"><span data-stu-id="fb691-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="fb691-107">以前のバージョン 1.0-1.4 もサポートされています (URL で "v1" を使用します)。</span><span class="sxs-lookup"><span data-stu-id="fb691-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="fb691-108">次のスキーマサンプルは、すべての拡張オプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="fb691-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="fb691-109">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="fb691-109">Sample full manifest</span></span>

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

<span data-ttu-id="fb691-110">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="fb691-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="fb691-111">$schema</span><span class="sxs-lookup"><span data-stu-id="fb691-111">$schema</span></span>

<span data-ttu-id="fb691-112">*省略可能 (ただし推奨* ) 文字列</span><span class="sxs-lookup"><span data-stu-id="fb691-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="fb691-113">マニフェストの JSON スキーマを参照する https://URL。</span><span class="sxs-lookup"><span data-stu-id="fb691-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="fb691-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="fb691-114">manifestVersion</span></span>

<span data-ttu-id="fb691-115">**必須** -文字列</span><span class="sxs-lookup"><span data-stu-id="fb691-115">**Required** — string</span></span>

<span data-ttu-id="fb691-116">このマニフェストが使用しているマニフェストスキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="fb691-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="fb691-117">"1.7" である必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-117">It should be "1.7".</span></span>

## <a name="version"></a><span data-ttu-id="fb691-118">バージョン</span><span class="sxs-lookup"><span data-stu-id="fb691-118">version</span></span>

<span data-ttu-id="fb691-119">**必須** -文字列</span><span class="sxs-lookup"><span data-stu-id="fb691-119">**Required** — string</span></span>

<span data-ttu-id="fb691-120">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="fb691-120">The version of the specific app.</span></span> <span data-ttu-id="fb691-121">マニフェスト内の内容を更新する場合は、そのバージョンも同時にインクリメントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="fb691-122">このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。</span><span class="sxs-lookup"><span data-stu-id="fb691-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="fb691-123">このアプリがストアに送信された場合は、新しいマニフェストを再送信して再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="fb691-124">その後、このアプリのユーザーは、承認後に数時間以内に新しい更新されたマニフェストを自動的に取得します。</span><span class="sxs-lookup"><span data-stu-id="fb691-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="fb691-125">アプリによって要求されたアクセス許可が変更された場合、ユーザーはアプリをアップグレードして再同意するように求められます。</span><span class="sxs-lookup"><span data-stu-id="fb691-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="fb691-126">このバージョンの文字列は、 [semver](http://semver.org/) 標準 (メジャー) に従う必要があります。間隔.パッチ)。</span><span class="sxs-lookup"><span data-stu-id="fb691-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="fb691-127">id</span><span class="sxs-lookup"><span data-stu-id="fb691-127">id</span></span>

<span data-ttu-id="fb691-128">**必須** -MICROSOFT アプリ ID</span><span class="sxs-lookup"><span data-stu-id="fb691-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="fb691-129">このアプリの一意の Microsoft 生成識別子。</span><span class="sxs-lookup"><span data-stu-id="fb691-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="fb691-130">Microsoft Bot フレームワークを介して bot を登録した場合、またはタブの web アプリが Microsoft によって既にサインインしている場合は、既に ID があるので、ここで入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="fb691-131">それ以外の場合は、Microsoft アプリケーション登録ポータル ([My Applications](https://apps.dev.microsoft.com)) で新しい ID を生成し、ここで入力してから、bot を追加するときにそれを再利用する必要があります。注: AppSource で既存のアプリに更新を送信する場合は、マニフェスト内の ID を変更しないでください。</span><span class="sxs-lookup"><span data-stu-id="fb691-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="fb691-132">developer</span><span class="sxs-lookup"><span data-stu-id="fb691-132">developer</span></span>

<span data-ttu-id="fb691-133">**Required** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="fb691-133">**Required** — object</span></span>

<span data-ttu-id="fb691-134">会社に関する情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="fb691-134">Specifies information about your company.</span></span> <span data-ttu-id="fb691-135">AppSource (旧称 Office ストア) に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="fb691-136">追加情報については、 [発行に関するガイドライン](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fb691-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="fb691-137">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-137">Name</span></span>| <span data-ttu-id="fb691-138">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-138">Maximum size</span></span> | <span data-ttu-id="fb691-139">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-139">Required</span></span> | <span data-ttu-id="fb691-140">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="fb691-141">32文字</span><span class="sxs-lookup"><span data-stu-id="fb691-141">32 characters</span></span>|<span data-ttu-id="fb691-142">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-142">✔</span></span>|<span data-ttu-id="fb691-143">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="fb691-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="fb691-144">2048 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-144">2048 characters</span></span>|<span data-ttu-id="fb691-145">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-145">✔</span></span>|<span data-ttu-id="fb691-146">開発者の web サイトへの https://URL。</span><span class="sxs-lookup"><span data-stu-id="fb691-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="fb691-147">このリンクは、ユーザーを会社または製品固有のランディングページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="fb691-148">2048 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-148">2048 characters</span></span>|<span data-ttu-id="fb691-149">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-149">✔</span></span>|<span data-ttu-id="fb691-150">開発者のプライバシーポリシーへの https://URL。</span><span class="sxs-lookup"><span data-stu-id="fb691-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="fb691-151">2048 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-151">2048 characters</span></span>|<span data-ttu-id="fb691-152">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-152">✔</span></span>|<span data-ttu-id="fb691-153">開発者の使用条件への https://URL。</span><span class="sxs-lookup"><span data-stu-id="fb691-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="fb691-154">10文字</span><span class="sxs-lookup"><span data-stu-id="fb691-154">10 characters</span></span>| |<span data-ttu-id="fb691-155">**省略可能** アプリを構築するパートナー組織を識別する Microsoft パートナーのネットワーク ID。</span><span class="sxs-lookup"><span data-stu-id="fb691-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="fb691-156">name</span><span class="sxs-lookup"><span data-stu-id="fb691-156">name</span></span>

<span data-ttu-id="fb691-157">**Required** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="fb691-157">**Required** — object</span></span>

<span data-ttu-id="fb691-158">Teams でユーザーに表示されるアプリの動作の名前です。</span><span class="sxs-lookup"><span data-stu-id="fb691-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="fb691-159">AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="fb691-160">との値 `short` を同じにすることはでき `full` ません。</span><span class="sxs-lookup"><span data-stu-id="fb691-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="fb691-161">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-161">Name</span></span>| <span data-ttu-id="fb691-162">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-162">Maximum size</span></span> | <span data-ttu-id="fb691-163">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-163">Required</span></span> | <span data-ttu-id="fb691-164">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="fb691-165">30 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-165">30 characters</span></span>|<span data-ttu-id="fb691-166">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-166">✔</span></span>|<span data-ttu-id="fb691-167">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="fb691-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="fb691-168">100 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-168">100 characters</span></span>||<span data-ttu-id="fb691-169">アプリの完全な名前。アプリの完全な名前が30文字を超えている場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="fb691-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="fb691-170">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-170">description</span></span>

<span data-ttu-id="fb691-171">**Required** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="fb691-171">**Required** — object</span></span>

<span data-ttu-id="fb691-172">ユーザーに対してアプリを記述します。</span><span class="sxs-lookup"><span data-stu-id="fb691-172">Describes your app to users.</span></span> <span data-ttu-id="fb691-173">AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="fb691-174">説明に正確に表示されていることを確認し、お客様が快適な動作を理解するのに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="fb691-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="fb691-175">また、外部アカウントが使用するために必要な場合は、詳細な説明にも注意してください。</span><span class="sxs-lookup"><span data-stu-id="fb691-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="fb691-176">との値 `short` を同じにすることはでき `full` ません。</span><span class="sxs-lookup"><span data-stu-id="fb691-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="fb691-177">短い説明を長い説明の中で繰り返すことはできません。他のアプリ名を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="fb691-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="fb691-178">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-178">Name</span></span>| <span data-ttu-id="fb691-179">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-179">Maximum size</span></span> | <span data-ttu-id="fb691-180">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-180">Required</span></span> | <span data-ttu-id="fb691-181">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="fb691-182">80文字</span><span class="sxs-lookup"><span data-stu-id="fb691-182">80 characters</span></span>|<span data-ttu-id="fb691-183">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-183">✔</span></span>|<span data-ttu-id="fb691-184">スペースが制限されている場合に使用する、アプリの使用状況の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="fb691-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="fb691-185">4000文字</span><span class="sxs-lookup"><span data-stu-id="fb691-185">4000 characters</span></span>|<span data-ttu-id="fb691-186">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-186">✔</span></span>|<span data-ttu-id="fb691-187">アプリの詳細な説明。</span><span class="sxs-lookup"><span data-stu-id="fb691-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="fb691-188">packageName</span><span class="sxs-lookup"><span data-stu-id="fb691-188">packageName</span></span>

<span data-ttu-id="fb691-189">**省略可能** (string)</span><span class="sxs-lookup"><span data-stu-id="fb691-189">**Optional** — string</span></span>

<span data-ttu-id="fb691-190">逆引きドメイン表記でのこのアプリの一意識別子。たとえば、例のようになります。</span><span class="sxs-lookup"><span data-stu-id="fb691-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="fb691-191">最大長: 64 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="fb691-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="fb691-192">localizationInfo</span></span>

<span data-ttu-id="fb691-193">**Optional** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="fb691-193">**Optional** — object</span></span>

<span data-ttu-id="fb691-194">既定の言語の指定、および追加の言語ファイルへのポインターを許可します。</span><span class="sxs-lookup"><span data-stu-id="fb691-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="fb691-195">「 [ローカライズ](~/concepts/build-and-test/apps-localization.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fb691-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="fb691-196">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-196">Name</span></span>| <span data-ttu-id="fb691-197">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-197">Maximum size</span></span> | <span data-ttu-id="fb691-198">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-198">Required</span></span> | <span data-ttu-id="fb691-199">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="fb691-200">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-200">✔</span></span>|<span data-ttu-id="fb691-201">このトップレベルマニフェストファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="fb691-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="fb691-202">localizationInfo. additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="fb691-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="fb691-203">追加の言語の翻訳を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="fb691-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="fb691-204">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-204">Name</span></span>| <span data-ttu-id="fb691-205">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-205">Maximum size</span></span> | <span data-ttu-id="fb691-206">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-206">Required</span></span> | <span data-ttu-id="fb691-207">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="fb691-208">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-208">✔</span></span>|<span data-ttu-id="fb691-209">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="fb691-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="fb691-210">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-210">✔</span></span>|<span data-ttu-id="fb691-211">翻訳された文字列を含む json ファイルへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="fb691-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="fb691-212">アイコン</span><span class="sxs-lookup"><span data-stu-id="fb691-212">icons</span></span>

<span data-ttu-id="fb691-213">**Required** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="fb691-213">**Required** — object</span></span>

<span data-ttu-id="fb691-214">Teams アプリ内で使用されるアイコン。</span><span class="sxs-lookup"><span data-stu-id="fb691-214">Icons used within the Teams app.</span></span> <span data-ttu-id="fb691-215">アイコンファイルは、アップロードパッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="fb691-216">詳細については、「 [アイコン](../../concepts/build-and-test/apps-package.md#app-icons) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fb691-216">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="fb691-217">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-217">Name</span></span>| <span data-ttu-id="fb691-218">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-218">Maximum size</span></span> | <span data-ttu-id="fb691-219">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-219">Required</span></span> | <span data-ttu-id="fb691-220">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="fb691-221">32 x 32 ピクセル</span><span class="sxs-lookup"><span data-stu-id="fb691-221">32 x 32 pixels</span></span>|<span data-ttu-id="fb691-222">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-222">✔</span></span>|<span data-ttu-id="fb691-223">透明な32x32 の PNG アウトラインアイコンへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="fb691-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="fb691-224">192 x 192 ピクセル</span><span class="sxs-lookup"><span data-stu-id="fb691-224">192 x 192 pixels</span></span>|<span data-ttu-id="fb691-225">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-225">✔</span></span>|<span data-ttu-id="fb691-226">フルカラー 192x192 PNG アイコンへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="fb691-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="fb691-227">アクセントカラー</span><span class="sxs-lookup"><span data-stu-id="fb691-227">accentColor</span></span>

<span data-ttu-id="fb691-228">**オプション** -HTML 16 進カラーコード</span><span class="sxs-lookup"><span data-stu-id="fb691-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="fb691-229">とと組み合わせてアウトラインアイコンの背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="fb691-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="fb691-230">この値は、' # ' で始まる有効な HTML カラーコードである必要があります (例 `#4464ee` :)。</span><span class="sxs-lookup"><span data-stu-id="fb691-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="fb691-231">の各タブ</span><span class="sxs-lookup"><span data-stu-id="fb691-231">configurableTabs</span></span>

<span data-ttu-id="fb691-232">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="fb691-232">**Optional** — array</span></span>

<span data-ttu-id="fb691-233">アプリの機能に、追加の構成を必要とするチームチャネルのタブがある場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="fb691-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="fb691-234">構成可能なタブは teams スコープ (個人ではない) でのみサポートされており、現在、アプリごとに **1 つ** のタブのみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="fb691-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="fb691-235">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-235">Name</span></span>| <span data-ttu-id="fb691-236">型</span><span class="sxs-lookup"><span data-stu-id="fb691-236">Type</span></span>| <span data-ttu-id="fb691-237">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-237">Maximum size</span></span> | <span data-ttu-id="fb691-238">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-238">Required</span></span> | <span data-ttu-id="fb691-239">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="fb691-240">string</span><span class="sxs-lookup"><span data-stu-id="fb691-240">string</span></span>|<span data-ttu-id="fb691-241">2048 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-241">2048 characters</span></span>|<span data-ttu-id="fb691-242">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-242">✔</span></span>|<span data-ttu-id="fb691-243">タブを構成するときに使用する https://URL。</span><span class="sxs-lookup"><span data-stu-id="fb691-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="fb691-244">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-244">array of enums</span></span>|<span data-ttu-id="fb691-245">1 </span><span class="sxs-lookup"><span data-stu-id="fb691-245">1</span></span>|<span data-ttu-id="fb691-246">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-246">✔</span></span>|<span data-ttu-id="fb691-247">現在、構成可能なタブでは、およびスコープのみがサポートさ `team` `groupchat` れています。</span><span class="sxs-lookup"><span data-stu-id="fb691-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="fb691-248">ブール値</span><span class="sxs-lookup"><span data-stu-id="fb691-248">boolean</span></span>|||<span data-ttu-id="fb691-249">作成後にタブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="fb691-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="fb691-250">既定値は **true** です。</span><span class="sxs-lookup"><span data-stu-id="fb691-250">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="fb691-251">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-251">array of enums</span></span>|<span data-ttu-id="fb691-252">6 </span><span class="sxs-lookup"><span data-stu-id="fb691-252">6</span></span>||<span data-ttu-id="fb691-253">`contextItem`タブがサポートされているスコープのセット。</span><span class="sxs-lookup"><span data-stu-id="fb691-253">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="fb691-254">既定値: **[Channeltab、privateChatTab、meetingChatTab、会議の設定]**。</span><span class="sxs-lookup"><span data-stu-id="fb691-254">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="fb691-255">string</span><span class="sxs-lookup"><span data-stu-id="fb691-255">string</span></span>|<span data-ttu-id="fb691-256">2048</span><span class="sxs-lookup"><span data-stu-id="fb691-256">2048</span></span>||<span data-ttu-id="fb691-257">SharePoint で使用するタブプレビュー画像への相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="fb691-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="fb691-258">サイズ1024x768。</span><span class="sxs-lookup"><span data-stu-id="fb691-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="fb691-259">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-259">array of enums</span></span>|<span data-ttu-id="fb691-260">1 </span><span class="sxs-lookup"><span data-stu-id="fb691-260">1</span></span>||<span data-ttu-id="fb691-261">SharePoint でどのようにタブを使用できるようにするかを定義します。</span><span class="sxs-lookup"><span data-stu-id="fb691-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="fb691-262">オプション `sharePointFullPage` と `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="fb691-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="fb691-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="fb691-263">staticTabs</span></span>

<span data-ttu-id="fb691-264">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="fb691-264">**Optional** — array</span></span>

<span data-ttu-id="fb691-265">ユーザーが手動で追加せずに、既定で "固定" できるタブのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="fb691-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="fb691-266">スコープ内で宣言 `personal` されている静的タブは、常にアプリの個人の環境に固定されます。</span><span class="sxs-lookup"><span data-stu-id="fb691-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="fb691-267">スコープ内で宣言されている静的タブ `team` は現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="fb691-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="fb691-268">この項目は、型のすべての要素を含む配列 (最大16個の要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="fb691-268">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="fb691-269">このブロックは、静的なタブソリューションを提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="fb691-269">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="fb691-270">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-270">Name</span></span>| <span data-ttu-id="fb691-271">型</span><span class="sxs-lookup"><span data-stu-id="fb691-271">Type</span></span>| <span data-ttu-id="fb691-272">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-272">Maximum size</span></span> | <span data-ttu-id="fb691-273">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-273">Required</span></span> | <span data-ttu-id="fb691-274">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-274">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="fb691-275">string</span><span class="sxs-lookup"><span data-stu-id="fb691-275">string</span></span>|<span data-ttu-id="fb691-276">64 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-276">64 characters</span></span>|<span data-ttu-id="fb691-277">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-277">✔</span></span>|<span data-ttu-id="fb691-278">タブに表示されるエンティティの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="fb691-278">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="fb691-279">string</span><span class="sxs-lookup"><span data-stu-id="fb691-279">string</span></span>|<span data-ttu-id="fb691-280">128文字</span><span class="sxs-lookup"><span data-stu-id="fb691-280">128 characters</span></span>|<span data-ttu-id="fb691-281">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-281">✔</span></span>|<span data-ttu-id="fb691-282">チャネルインターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="fb691-282">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="fb691-283">string</span><span class="sxs-lookup"><span data-stu-id="fb691-283">string</span></span>||<span data-ttu-id="fb691-284">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-284">✔</span></span>|<span data-ttu-id="fb691-285">Teams キャンバスに表示されるエンティティ UI をポイントする https://URL。</span><span class="sxs-lookup"><span data-stu-id="fb691-285">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="fb691-286">string</span><span class="sxs-lookup"><span data-stu-id="fb691-286">string</span></span>|||<span data-ttu-id="fb691-287">ユーザーがブラウザーで表示をポイントしたかどうかを示す https://URL。</span><span class="sxs-lookup"><span data-stu-id="fb691-287">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="fb691-288">string</span><span class="sxs-lookup"><span data-stu-id="fb691-288">string</span></span>|||<span data-ttu-id="fb691-289">ユーザーの検索クエリを指す https://URL。</span><span class="sxs-lookup"><span data-stu-id="fb691-289">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="fb691-290">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-290">array of enums</span></span>|<span data-ttu-id="fb691-291">1 </span><span class="sxs-lookup"><span data-stu-id="fb691-291">1</span></span>|<span data-ttu-id="fb691-292">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-292">✔</span></span>|<span data-ttu-id="fb691-293">現時点では、静的タブではスコープのみがサポート `personal` されます。つまり、個人の利便性の一環としてのみプロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="fb691-293">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="fb691-294">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-294">array of enums</span></span>| <span data-ttu-id="fb691-295">2 </span><span class="sxs-lookup"><span data-stu-id="fb691-295">2</span></span>|| <span data-ttu-id="fb691-296">`contextItem`タブがサポートされているスコープのセット。</span><span class="sxs-lookup"><span data-stu-id="fb691-296">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="fb691-297">関連するコンテンツを表示したり、認証フローを開始したりするために、タブにコンテキスト依存情報が必要な場合は、「 [Microsoft Teams のコンテキストを取得する」タブ](../../tabs/how-to/access-teams-context.md)を *参照してください*。</span><span class="sxs-lookup"><span data-stu-id="fb691-297">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="fb691-298">bot</span><span class="sxs-lookup"><span data-stu-id="fb691-298">bots</span></span>

<span data-ttu-id="fb691-299">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="fb691-299">**Optional** — array</span></span>

<span data-ttu-id="fb691-300">Bot ソリューションと、既定のコマンドプロパティなどのオプション情報を定義します。</span><span class="sxs-lookup"><span data-stu-id="fb691-300">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="fb691-301">アイテムが配列の場合 (現時点では1つの要素のみ &mdash; が可能)、その型のすべての要素が含まれ `object` ます。</span><span class="sxs-lookup"><span data-stu-id="fb691-301">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="fb691-302">このブロックは、bot の環境を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="fb691-302">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="fb691-303">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-303">Name</span></span>| <span data-ttu-id="fb691-304">型</span><span class="sxs-lookup"><span data-stu-id="fb691-304">Type</span></span>| <span data-ttu-id="fb691-305">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-305">Maximum size</span></span> | <span data-ttu-id="fb691-306">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-306">Required</span></span> | <span data-ttu-id="fb691-307">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-307">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="fb691-308">string</span><span class="sxs-lookup"><span data-stu-id="fb691-308">string</span></span>|<span data-ttu-id="fb691-309">64 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-309">64 characters</span></span>|<span data-ttu-id="fb691-310">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-310">✔</span></span>|<span data-ttu-id="fb691-311">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="fb691-311">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="fb691-312">これは、アプリの全体的な [ID](#id)と同じである場合もあります。</span><span class="sxs-lookup"><span data-stu-id="fb691-312">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="fb691-313">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-313">array of enums</span></span>|<span data-ttu-id="fb691-314">3 </span><span class="sxs-lookup"><span data-stu-id="fb691-314">3</span></span>|<span data-ttu-id="fb691-315">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-315">✔</span></span>|<span data-ttu-id="fb691-316">ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。</span><span class="sxs-lookup"><span data-stu-id="fb691-316">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="fb691-317">これらのオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="fb691-317">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="fb691-318">ブール値</span><span class="sxs-lookup"><span data-stu-id="fb691-318">boolean</span></span>|||<span data-ttu-id="fb691-319">ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。</span><span class="sxs-lookup"><span data-stu-id="fb691-319">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="fb691-320">限り **`false`**</span><span class="sxs-lookup"><span data-stu-id="fb691-320">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="fb691-321">ブール値</span><span class="sxs-lookup"><span data-stu-id="fb691-321">boolean</span></span>|||<span data-ttu-id="fb691-322">ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="fb691-322">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="fb691-323">限り `**false**`</span><span class="sxs-lookup"><span data-stu-id="fb691-323">Default: `**false**`</span></span>|
|`supportsFiles`|<span data-ttu-id="fb691-324">ブール値</span><span class="sxs-lookup"><span data-stu-id="fb691-324">boolean</span></span>|||<span data-ttu-id="fb691-325">パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="fb691-325">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="fb691-326">限り **`false`**</span><span class="sxs-lookup"><span data-stu-id="fb691-326">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="fb691-327">ブール値</span><span class="sxs-lookup"><span data-stu-id="fb691-327">boolean</span></span>|||<span data-ttu-id="fb691-328">Bot が音声通話をサポートするかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="fb691-328">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="fb691-329">**重要**: このプロパティは現在実験的なものです。</span><span class="sxs-lookup"><span data-stu-id="fb691-329">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="fb691-330">実験的なプロパティは完成していない可能性があり、完全に使用できるようになる前に変更が行われる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-330">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="fb691-331">テストと調査の目的でのみ提供されており、運用アプリケーションでは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="fb691-331">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="fb691-332">限り **`false`**</span><span class="sxs-lookup"><span data-stu-id="fb691-332">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="fb691-333">ブール値</span><span class="sxs-lookup"><span data-stu-id="fb691-333">boolean</span></span>|||<span data-ttu-id="fb691-334">Bot がビデオ通話をサポートする場所を示す値。</span><span class="sxs-lookup"><span data-stu-id="fb691-334">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="fb691-335">**重要**: このプロパティは現在実験的なものです。</span><span class="sxs-lookup"><span data-stu-id="fb691-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="fb691-336">実験的なプロパティは完成していない可能性があり、完全に使用できるようになる前に変更が行われる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="fb691-337">テストと調査の目的でのみ提供されており、運用アプリケーションでは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="fb691-337">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="fb691-338">限り **`false`**</span><span class="sxs-lookup"><span data-stu-id="fb691-338">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="fb691-339">bot リスト</span><span class="sxs-lookup"><span data-stu-id="fb691-339">bots.commandLists</span></span>

<span data-ttu-id="fb691-340">Bot がユーザーに推奨できるコマンドのオプションの一覧。</span><span class="sxs-lookup"><span data-stu-id="fb691-340">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="fb691-341">Object は、型のすべての要素を含む配列 (最大2つの要素) です `object` 。 bot がサポートするスコープごとに個別のコマンドリストを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-341">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="fb691-342">詳細については、「 [Bot メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fb691-342">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="fb691-343">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-343">Name</span></span>| <span data-ttu-id="fb691-344">型</span><span class="sxs-lookup"><span data-stu-id="fb691-344">Type</span></span>| <span data-ttu-id="fb691-345">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-345">Maximum size</span></span> | <span data-ttu-id="fb691-346">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-346">Required</span></span> | <span data-ttu-id="fb691-347">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-347">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="fb691-348">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-348">array of enums</span></span>|<span data-ttu-id="fb691-349">3 </span><span class="sxs-lookup"><span data-stu-id="fb691-349">3</span></span>|<span data-ttu-id="fb691-350">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-350">✔</span></span>|<span data-ttu-id="fb691-351">コマンド リストが有効なスコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="fb691-351">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="fb691-352">`team`、`personal`、`groupchat` の中から選択できます。</span><span class="sxs-lookup"><span data-stu-id="fb691-352">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="fb691-353">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="fb691-353">array of objects</span></span>|<span data-ttu-id="fb691-354">10 </span><span class="sxs-lookup"><span data-stu-id="fb691-354">10</span></span>|<span data-ttu-id="fb691-355">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-355">✔</span></span>|<span data-ttu-id="fb691-356">ボットがサポートするコマンドの配列:</span><span class="sxs-lookup"><span data-stu-id="fb691-356">An array of commands the bot supports:</span></span><br><span data-ttu-id="fb691-357">`title`: ボット コマンドの名前 (文字列、32)</span><span class="sxs-lookup"><span data-stu-id="fb691-357">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="fb691-358">`description`: コマンドの構文およびその構文の引数
の簡単な説明または例 (文字列、128)</span><span class="sxs-lookup"><span data-stu-id="fb691-358">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="fb691-359">bot のリストコマンド</span><span class="sxs-lookup"><span data-stu-id="fb691-359">bots.commandLists.commands</span></span>

|<span data-ttu-id="fb691-360">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-360">Name</span></span>| <span data-ttu-id="fb691-361">型</span><span class="sxs-lookup"><span data-stu-id="fb691-361">Type</span></span>| <span data-ttu-id="fb691-362">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-362">Maximum size</span></span> | <span data-ttu-id="fb691-363">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-363">Required</span></span> | <span data-ttu-id="fb691-364">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-364">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="fb691-365">title</span><span class="sxs-lookup"><span data-stu-id="fb691-365">title</span></span>|<span data-ttu-id="fb691-366">string</span><span class="sxs-lookup"><span data-stu-id="fb691-366">string</span></span>|<span data-ttu-id="fb691-367">12 </span><span class="sxs-lookup"><span data-stu-id="fb691-367">12</span></span>|<span data-ttu-id="fb691-368">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-368">✔</span></span>|<span data-ttu-id="fb691-369">Bot コマンド名</span><span class="sxs-lookup"><span data-stu-id="fb691-369">The bot command name</span></span>|
|<span data-ttu-id="fb691-370">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-370">description</span></span>|<span data-ttu-id="fb691-371">string</span><span class="sxs-lookup"><span data-stu-id="fb691-371">string</span></span>|<span data-ttu-id="fb691-372">128文字</span><span class="sxs-lookup"><span data-stu-id="fb691-372">128 characters</span></span>|<span data-ttu-id="fb691-373">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-373">✔</span></span>|<span data-ttu-id="fb691-374">簡単なテキストの説明、またはコマンド構文とその引数の例。</span><span class="sxs-lookup"><span data-stu-id="fb691-374">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="fb691-375">コネクタ</span><span class="sxs-lookup"><span data-stu-id="fb691-375">connectors</span></span>

<span data-ttu-id="fb691-376">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="fb691-376">**Optional** — array</span></span>

<span data-ttu-id="fb691-377">ブロックは、 `connectors` アプリの Office 365 コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="fb691-377">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="fb691-378">Object は、type のすべての要素を含む配列 (最大1つの要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="fb691-378">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="fb691-379">このブロックは、コネクタを提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="fb691-379">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="fb691-380">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-380">Name</span></span>| <span data-ttu-id="fb691-381">型</span><span class="sxs-lookup"><span data-stu-id="fb691-381">Type</span></span>| <span data-ttu-id="fb691-382">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-382">Maximum size</span></span> | <span data-ttu-id="fb691-383">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-383">Required</span></span> | <span data-ttu-id="fb691-384">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-384">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="fb691-385">string</span><span class="sxs-lookup"><span data-stu-id="fb691-385">string</span></span>|<span data-ttu-id="fb691-386">2048 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-386">2048 characters</span></span>|<span data-ttu-id="fb691-387">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-387">✔</span></span>|<span data-ttu-id="fb691-388">コネクタを構成するときに使用する https://URL。</span><span class="sxs-lookup"><span data-stu-id="fb691-388">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="fb691-389">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-389">array of enums</span></span>|<span data-ttu-id="fb691-390">1 </span><span class="sxs-lookup"><span data-stu-id="fb691-390">1</span></span>|<span data-ttu-id="fb691-391">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-391">✔</span></span>|<span data-ttu-id="fb691-392">コネクタが内のチャネルのコンテキストで、 `team` または個別のユーザー単独 () にスコープ設定された環境での動作を提供するかどうかを指定し `personal` ます。</span><span class="sxs-lookup"><span data-stu-id="fb691-392">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="fb691-393">現時点では、 `team` 範囲のみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="fb691-393">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="fb691-394">string</span><span class="sxs-lookup"><span data-stu-id="fb691-394">string</span></span>|<span data-ttu-id="fb691-395">64 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-395">64 characters</span></span>|<span data-ttu-id="fb691-396">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-396">✔</span></span>|<span data-ttu-id="fb691-397">コネクタ [開発者ダッシュボード](https://aka.ms/connectorsdashboard)の ID と一致するコネクタの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="fb691-397">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="fb691-398">この機能</span><span class="sxs-lookup"><span data-stu-id="fb691-398">composeExtensions</span></span>

<span data-ttu-id="fb691-399">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="fb691-399">**Optional** — array</span></span>

<span data-ttu-id="fb691-400">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="fb691-400">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="fb691-401">この機能の名前は、2017年11月に「[作成] 拡張機能」から「messaging extension」に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は同じままです。</span><span class="sxs-lookup"><span data-stu-id="fb691-401">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="fb691-402">Item は、type のすべての要素を含む配列 (最大1つの要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="fb691-402">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="fb691-403">このブロックは、メッセージング拡張機能を提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="fb691-403">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="fb691-404">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-404">Name</span></span>| <span data-ttu-id="fb691-405">型</span><span class="sxs-lookup"><span data-stu-id="fb691-405">Type</span></span> | <span data-ttu-id="fb691-406">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-406">Maximum Size</span></span> | <span data-ttu-id="fb691-407">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-407">Required</span></span> | <span data-ttu-id="fb691-408">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-408">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="fb691-409">string</span><span class="sxs-lookup"><span data-stu-id="fb691-409">string</span></span>|<span data-ttu-id="fb691-410">64</span><span class="sxs-lookup"><span data-stu-id="fb691-410">64</span></span>|<span data-ttu-id="fb691-411">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-411">✔</span></span>|<span data-ttu-id="fb691-412">Bot フレームワークに登録されているメッセージング拡張機能をバックアップする bot の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="fb691-412">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="fb691-413">これは、アプリの全体的な ID と同じである場合もあります。</span><span class="sxs-lookup"><span data-stu-id="fb691-413">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="fb691-414">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="fb691-414">array of objects</span></span>|<span data-ttu-id="fb691-415">10 </span><span class="sxs-lookup"><span data-stu-id="fb691-415">10</span></span>|<span data-ttu-id="fb691-416">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-416">✔</span></span>|<span data-ttu-id="fb691-417">メッセージング拡張機能がサポートするコマンドの配列</span><span class="sxs-lookup"><span data-stu-id="fb691-417">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="fb691-418">ブール値</span><span class="sxs-lookup"><span data-stu-id="fb691-418">boolean</span></span>|||<span data-ttu-id="fb691-419">メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="fb691-419">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="fb691-420">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="fb691-420">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="fb691-421">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="fb691-421">array of Objects</span></span>|<span data-ttu-id="fb691-422">5 </span><span class="sxs-lookup"><span data-stu-id="fb691-422">5</span></span>||<span data-ttu-id="fb691-423">特定の条件が満たされたときにアプリを呼び出せるようにするハンドラーの一覧。</span><span class="sxs-lookup"><span data-stu-id="fb691-423">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="fb691-424">ドメインも、にリストされている必要があります。 `validDomains`</span><span class="sxs-lookup"><span data-stu-id="fb691-424">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="fb691-425">string</span><span class="sxs-lookup"><span data-stu-id="fb691-425">string</span></span>|||<span data-ttu-id="fb691-426">メッセージハンドラの種類。</span><span class="sxs-lookup"><span data-stu-id="fb691-426">The type of message handler.</span></span> <span data-ttu-id="fb691-427">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-427">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="fb691-428">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-428">array of Strings</span></span>|||<span data-ttu-id="fb691-429">リンクメッセージハンドラが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="fb691-429">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="fb691-430">このコマンドの機能</span><span class="sxs-lookup"><span data-stu-id="fb691-430">composeExtensions.commands</span></span>

<span data-ttu-id="fb691-431">メッセージング拡張機能は、1つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-431">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="fb691-432">各コマンドは、Microsoft Teams に UI ベースのエントリポイントからの潜在的な操作として表示されます。</span><span class="sxs-lookup"><span data-stu-id="fb691-432">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="fb691-433">最大10個のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="fb691-433">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="fb691-434">各コマンド項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="fb691-434">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="fb691-435">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-435">Name</span></span>| <span data-ttu-id="fb691-436">型</span><span class="sxs-lookup"><span data-stu-id="fb691-436">Type</span></span>| <span data-ttu-id="fb691-437">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-437">Maximum size</span></span> | <span data-ttu-id="fb691-438">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-438">Required</span></span> | <span data-ttu-id="fb691-439">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-439">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="fb691-440">string</span><span class="sxs-lookup"><span data-stu-id="fb691-440">string</span></span>|<span data-ttu-id="fb691-441">64 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-441">64 characters</span></span>|<span data-ttu-id="fb691-442">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-442">✔</span></span>|<span data-ttu-id="fb691-443">コマンドの ID。</span><span class="sxs-lookup"><span data-stu-id="fb691-443">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="fb691-444">string</span><span class="sxs-lookup"><span data-stu-id="fb691-444">string</span></span>|<span data-ttu-id="fb691-445">32文字</span><span class="sxs-lookup"><span data-stu-id="fb691-445">32 characters</span></span>|<span data-ttu-id="fb691-446">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-446">✔</span></span>|<span data-ttu-id="fb691-447">ユーザーフレンドリなコマンド名。</span><span class="sxs-lookup"><span data-stu-id="fb691-447">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="fb691-448">string</span><span class="sxs-lookup"><span data-stu-id="fb691-448">string</span></span>|<span data-ttu-id="fb691-449">64 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-449">64 characters</span></span>||<span data-ttu-id="fb691-450">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="fb691-450">Type of the command.</span></span> <span data-ttu-id="fb691-451">またはのいずれか `query` `action` です。</span><span class="sxs-lookup"><span data-stu-id="fb691-451">One of `query` or `action`.</span></span> <span data-ttu-id="fb691-452">既定値: **query**。</span><span class="sxs-lookup"><span data-stu-id="fb691-452">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="fb691-453">string</span><span class="sxs-lookup"><span data-stu-id="fb691-453">string</span></span>|<span data-ttu-id="fb691-454">128文字</span><span class="sxs-lookup"><span data-stu-id="fb691-454">128 characters</span></span>||<span data-ttu-id="fb691-455">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="fb691-455">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="fb691-456">ブール値</span><span class="sxs-lookup"><span data-stu-id="fb691-456">boolean</span></span>|||<span data-ttu-id="fb691-457">パラメーターを指定せずにコマンドを最初に実行する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="fb691-457">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="fb691-458">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="fb691-458">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="fb691-459">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-459">array of Strings</span></span>|<span data-ttu-id="fb691-460">3 </span><span class="sxs-lookup"><span data-stu-id="fb691-460">3</span></span>||<span data-ttu-id="fb691-461">メッセージの内線番号をから呼び出すことができる場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="fb691-461">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="fb691-462">、、の任意の組み合わせ `compose` `commandBox` `message` 。</span><span class="sxs-lookup"><span data-stu-id="fb691-462">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="fb691-463">既定値は `["compose","commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="fb691-463">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="fb691-464">ブール値</span><span class="sxs-lookup"><span data-stu-id="fb691-464">boolean</span></span>|||<span data-ttu-id="fb691-465">タスクモジュールを動的にフェッチする必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="fb691-465">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="fb691-466">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="fb691-466">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="fb691-467">object</span><span class="sxs-lookup"><span data-stu-id="fb691-467">object</span></span>|||<span data-ttu-id="fb691-468">メッセージ拡張コマンドの使用時に、タスクモジュールを事前に読み込むように指定します。</span><span class="sxs-lookup"><span data-stu-id="fb691-468">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="fb691-469">string</span><span class="sxs-lookup"><span data-stu-id="fb691-469">string</span></span>|<span data-ttu-id="fb691-470">64 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-470">64 characters</span></span>||<span data-ttu-id="fb691-471">最初のダイアログのタイトル。</span><span class="sxs-lookup"><span data-stu-id="fb691-471">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="fb691-472">string</span><span class="sxs-lookup"><span data-stu-id="fb691-472">string</span></span>|||<span data-ttu-id="fb691-473">ダイアログの幅。ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="fb691-473">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="fb691-474">string</span><span class="sxs-lookup"><span data-stu-id="fb691-474">string</span></span>|||<span data-ttu-id="fb691-475">ダイアログの高さ-ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="fb691-475">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="fb691-476">string</span><span class="sxs-lookup"><span data-stu-id="fb691-476">string</span></span>|||<span data-ttu-id="fb691-477">最初の webview の URL。</span><span class="sxs-lookup"><span data-stu-id="fb691-477">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="fb691-478">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="fb691-478">array of object</span></span>|<span data-ttu-id="fb691-479">5アイテム</span><span class="sxs-lookup"><span data-stu-id="fb691-479">5 items</span></span>|<span data-ttu-id="fb691-480">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-480">✔</span></span>|<span data-ttu-id="fb691-481">コマンドが実行するパラメーターの一覧。</span><span class="sxs-lookup"><span data-stu-id="fb691-481">The list of parameters the command takes.</span></span> <span data-ttu-id="fb691-482">最小値: 1、最大: 5</span><span class="sxs-lookup"><span data-stu-id="fb691-482">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="fb691-483">string</span><span class="sxs-lookup"><span data-stu-id="fb691-483">string</span></span>|<span data-ttu-id="fb691-484">64 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-484">64 characters</span></span>|<span data-ttu-id="fb691-485">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-485">✔</span></span>|<span data-ttu-id="fb691-486">クライアントに表示されるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="fb691-486">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="fb691-487">これは、ユーザー要求に含まれています。</span><span class="sxs-lookup"><span data-stu-id="fb691-487">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="fb691-488">string</span><span class="sxs-lookup"><span data-stu-id="fb691-488">string</span></span>|<span data-ttu-id="fb691-489">32文字</span><span class="sxs-lookup"><span data-stu-id="fb691-489">32 characters</span></span>|<span data-ttu-id="fb691-490">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-490">✔</span></span>|<span data-ttu-id="fb691-491">パラメーターのユーザーフレンドリなタイトル。</span><span class="sxs-lookup"><span data-stu-id="fb691-491">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="fb691-492">string</span><span class="sxs-lookup"><span data-stu-id="fb691-492">string</span></span>|<span data-ttu-id="fb691-493">128文字</span><span class="sxs-lookup"><span data-stu-id="fb691-493">128 characters</span></span>||<span data-ttu-id="fb691-494">このパラメーターの目的を説明するユーザーフレンドリ文字列。</span><span class="sxs-lookup"><span data-stu-id="fb691-494">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="fb691-495">string</span><span class="sxs-lookup"><span data-stu-id="fb691-495">string</span></span>|<span data-ttu-id="fb691-496">512文字</span><span class="sxs-lookup"><span data-stu-id="fb691-496">512 characters</span></span>||<span data-ttu-id="fb691-497">パラメータの初期値。</span><span class="sxs-lookup"><span data-stu-id="fb691-497">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="fb691-498">string</span><span class="sxs-lookup"><span data-stu-id="fb691-498">string</span></span>|<span data-ttu-id="fb691-499">128文字</span><span class="sxs-lookup"><span data-stu-id="fb691-499">128 characters</span></span>||<span data-ttu-id="fb691-500">のタスクモジュールに表示されるコントロールの種類を定義 `fetchTask: true` します。</span><span class="sxs-lookup"><span data-stu-id="fb691-500">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="fb691-501">のいずれか `text, textarea, number, date, time, toggle, choiceset` です。</span><span class="sxs-lookup"><span data-stu-id="fb691-501">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="fb691-502">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="fb691-502">array of objects</span></span>|<span data-ttu-id="fb691-503">10アイテム</span><span class="sxs-lookup"><span data-stu-id="fb691-503">10 items</span></span>||<span data-ttu-id="fb691-504">の選択オプション `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="fb691-504">The choice options for the`choiceset`.</span></span> <span data-ttu-id="fb691-505">がである場合にのみ使用 `parameter.inputType` `choiceset` します。</span><span class="sxs-lookup"><span data-stu-id="fb691-505">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="fb691-506">string</span><span class="sxs-lookup"><span data-stu-id="fb691-506">string</span></span>|<span data-ttu-id="fb691-507">128文字</span><span class="sxs-lookup"><span data-stu-id="fb691-507">128 characters</span></span>|<span data-ttu-id="fb691-508">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-508">✔</span></span>|<span data-ttu-id="fb691-509">選択項目のタイトル。</span><span class="sxs-lookup"><span data-stu-id="fb691-509">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="fb691-510">string</span><span class="sxs-lookup"><span data-stu-id="fb691-510">string</span></span>|<span data-ttu-id="fb691-511">512文字</span><span class="sxs-lookup"><span data-stu-id="fb691-511">512 characters</span></span>|<span data-ttu-id="fb691-512">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-512">✔</span></span>|<span data-ttu-id="fb691-513">Value of the choice.</span><span class="sxs-lookup"><span data-stu-id="fb691-513">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="fb691-514">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="fb691-514">permissions</span></span>

<span data-ttu-id="fb691-515">**省略可能** -文字列の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-515">**Optional** — array of strings</span></span>

<span data-ttu-id="fb691-516">`string`アプリが要求するアクセス許可を指定する配列。これにより、エンドユーザーは拡張機能の動作を知ることができます。</span><span class="sxs-lookup"><span data-stu-id="fb691-516">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="fb691-517">非排他的なオプションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="fb691-517">The following options are non-exclusive:</span></span>

* <span data-ttu-id="fb691-518">`identity`&emsp;ユーザー id 情報が必要</span><span class="sxs-lookup"><span data-stu-id="fb691-518">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="fb691-519">`messageTeamMembers`&emsp;チームメンバーに直接メッセージを送信するためのアクセス許可が必要</span><span class="sxs-lookup"><span data-stu-id="fb691-519">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="fb691-520">アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは、更新されたアプリを初めて実行したときに同意プロセスを繰り返すようになります。</span><span class="sxs-lookup"><span data-stu-id="fb691-520">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="fb691-521">詳細については [、「アプリの更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fb691-521">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="fb691-522">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="fb691-522">devicePermissions</span></span>

<span data-ttu-id="fb691-523">**省略可能** -文字列の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-523">**Optional** — array of strings</span></span>

<span data-ttu-id="fb691-524">アプリがアクセスを要求することができる、ユーザーのデバイスのネイティブ機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="fb691-524">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="fb691-525">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="fb691-525">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="fb691-526">validDomains</span><span class="sxs-lookup"><span data-stu-id="fb691-526">validDomains</span></span>

<span data-ttu-id="fb691-527">**省略可能**(記載個所に **必要な** 場合を除く)</span><span class="sxs-lookup"><span data-stu-id="fb691-527">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="fb691-528">アプリが Teams クライアント内で読み込むことが想定されている web サイトの有効なドメインの一覧。</span><span class="sxs-lookup"><span data-stu-id="fb691-528">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="fb691-529">ドメインリストには、たとえば、ワイルドカードを含めることができ `*.example.com` ます。</span><span class="sxs-lookup"><span data-stu-id="fb691-529">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="fb691-530">これは、1つのドメインのセグメントに一致します。に一致させる必要がある場合は `a.b.example.com` 、を使用 `*.*.example.com` します。</span><span class="sxs-lookup"><span data-stu-id="fb691-530">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="fb691-531">タブ構成またはコンテンツ UI が他のドメインに移動する必要がある場合 (タブの構成に使用するものを除く)、そのドメインをここで指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-531">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="fb691-532">ただし、アプリでサポートする id プロバイダーのドメインを含める必要は **ありません** 。</span><span class="sxs-lookup"><span data-stu-id="fb691-532">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="fb691-533">たとえば、Google ID を使用して認証するには、accounts.google.com にリダイレクトする必要がありますが、に accounts.google.com を含めることはできません `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="fb691-533">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="fb691-534">自分の sharepoint Url が適切に機能する必要がある Teams アプリは、有効なドメインリストに "{teamsitedomain}" を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="fb691-534">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb691-535">直接に、またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しないでください。</span><span class="sxs-lookup"><span data-stu-id="fb691-535">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="fb691-536">たとえば、は有効ですが、有効では `yourapp.onmicrosoft.com` `*.onmicrosoft.com` ありません。</span><span class="sxs-lookup"><span data-stu-id="fb691-536">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="fb691-537">Object は、型のすべての要素を含む配列です `string` 。</span><span class="sxs-lookup"><span data-stu-id="fb691-537">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="fb691-538">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="fb691-538">webApplicationInfo</span></span>

<span data-ttu-id="fb691-539">**Optional** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="fb691-539">**Optional** — object</span></span>

<span data-ttu-id="fb691-540">ユーザーがアプリにシームレスにサインインできるようにするには、Azure Active Directory (Azure AD) アプリ ID と Microsoft Graph 情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="fb691-540">Specify your Azure Active Directory (Azure AD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="fb691-541">アプリが Azure AD に登録されている場合は、管理者が簡単にアクセス許可を確認し、Teams 管理センターで同意を付与できるように、アプリ ID を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-541">If your app is registered in Azure AD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="fb691-542">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-542">Name</span></span>| <span data-ttu-id="fb691-543">型</span><span class="sxs-lookup"><span data-stu-id="fb691-543">Type</span></span>| <span data-ttu-id="fb691-544">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-544">Maximum size</span></span> | <span data-ttu-id="fb691-545">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-545">Required</span></span> | <span data-ttu-id="fb691-546">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-546">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="fb691-547">string</span><span class="sxs-lookup"><span data-stu-id="fb691-547">string</span></span>|<span data-ttu-id="fb691-548">36文字</span><span class="sxs-lookup"><span data-stu-id="fb691-548">36 characters</span></span>|<span data-ttu-id="fb691-549">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-549">✔</span></span>|<span data-ttu-id="fb691-550">アプリの AAD アプリケーション id。</span><span class="sxs-lookup"><span data-stu-id="fb691-550">AAD application id of the app.</span></span> <span data-ttu-id="fb691-551">この id は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-551">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="fb691-552">string</span><span class="sxs-lookup"><span data-stu-id="fb691-552">string</span></span>|<span data-ttu-id="fb691-553">2048 文字</span><span class="sxs-lookup"><span data-stu-id="fb691-553">2048 characters</span></span>|<span data-ttu-id="fb691-554">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-554">✔</span></span>|<span data-ttu-id="fb691-555">SSO の認証トークンを取得するためのアプリのリソース url。</span><span class="sxs-lookup"><span data-stu-id="fb691-555">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="fb691-556">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="fb691-556">array of strings</span></span>|<span data-ttu-id="fb691-557">128文字</span><span class="sxs-lookup"><span data-stu-id="fb691-557">128 characters</span></span>||<span data-ttu-id="fb691-558">[リソース固有の](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)詳細な同意を指定する</span><span class="sxs-lookup"><span data-stu-id="fb691-558">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="fb691-559">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="fb691-559">showLoadingIndicator</span></span>

<span data-ttu-id="fb691-560">**Optional** -boolean</span><span class="sxs-lookup"><span data-stu-id="fb691-560">**Optional** — boolean</span></span>

<span data-ttu-id="fb691-561">アプリ/タブが読み込まれているときに、読み込みインジケーターを表示するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="fb691-561">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="fb691-562">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="fb691-562">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="fb691-563">アプリマニフェストで "showLoadingIndicator: true" を設定した場合、ページが正しく読み込まれるようにするには、「 [ネイティブロードインジケーター](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) ドキュメントを表示する」で説明されているプロトコルに従って、タブおよびタスクモジュールのコンテンツページを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb691-563">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="fb691-564">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="fb691-564">isFullScreen</span></span>

 <span data-ttu-id="fb691-565">**Optional** -boolean</span><span class="sxs-lookup"><span data-stu-id="fb691-565">**Optional** — boolean</span></span>

<span data-ttu-id="fb691-566">個人用アプリがタブヘッダーバーを使用して、または表示せずにレンダリングされる場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="fb691-566">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="fb691-567">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="fb691-567">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="fb691-568">アクティビティ</span><span class="sxs-lookup"><span data-stu-id="fb691-568">activities</span></span>

<span data-ttu-id="fb691-569">**Optional** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="fb691-569">**Optional** — object</span></span>

<span data-ttu-id="fb691-570">アプリがユーザーアクティビティフィードに投稿するときに使用するプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="fb691-570">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="fb691-571">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-571">Name</span></span>| <span data-ttu-id="fb691-572">型</span><span class="sxs-lookup"><span data-stu-id="fb691-572">Type</span></span>| <span data-ttu-id="fb691-573">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-573">Maximum size</span></span> | <span data-ttu-id="fb691-574">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-574">Required</span></span> | <span data-ttu-id="fb691-575">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-575">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="fb691-576">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="fb691-576">array of Objects</span></span>|<span data-ttu-id="fb691-577">128アイテム</span><span class="sxs-lookup"><span data-stu-id="fb691-577">128 items</span></span>| | <span data-ttu-id="fb691-578">アプリがユーザーアクティビティフィードに投稿できるアクティビティの種類を指定します。</span><span class="sxs-lookup"><span data-stu-id="fb691-578">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="fb691-579">アクティビティの種類</span><span class="sxs-lookup"><span data-stu-id="fb691-579">activities.activityTypes</span></span>

|<span data-ttu-id="fb691-580">名前</span><span class="sxs-lookup"><span data-stu-id="fb691-580">Name</span></span>| <span data-ttu-id="fb691-581">型</span><span class="sxs-lookup"><span data-stu-id="fb691-581">Type</span></span>| <span data-ttu-id="fb691-582">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="fb691-582">Maximum size</span></span> | <span data-ttu-id="fb691-583">必須</span><span class="sxs-lookup"><span data-stu-id="fb691-583">Required</span></span> | <span data-ttu-id="fb691-584">説明</span><span class="sxs-lookup"><span data-stu-id="fb691-584">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="fb691-585">string</span><span class="sxs-lookup"><span data-stu-id="fb691-585">string</span></span>|<span data-ttu-id="fb691-586">32文字</span><span class="sxs-lookup"><span data-stu-id="fb691-586">32 characters</span></span>|<span data-ttu-id="fb691-587">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-587">✔</span></span>|<span data-ttu-id="fb691-588">通知の種類。</span><span class="sxs-lookup"><span data-stu-id="fb691-588">The notification type.</span></span> <span data-ttu-id="fb691-589">*以下を参照して* ください。</span><span class="sxs-lookup"><span data-stu-id="fb691-589">*See below*.</span></span>|
|`description`|<span data-ttu-id="fb691-590">string</span><span class="sxs-lookup"><span data-stu-id="fb691-590">string</span></span>|<span data-ttu-id="fb691-591">128文字</span><span class="sxs-lookup"><span data-stu-id="fb691-591">128 characters</span></span>|<span data-ttu-id="fb691-592">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-592">✔</span></span>|<span data-ttu-id="fb691-593">通知の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="fb691-593">A brief description of the notification.</span></span> <span data-ttu-id="fb691-594">*以下を参照して* ください。</span><span class="sxs-lookup"><span data-stu-id="fb691-594">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="fb691-595">string</span><span class="sxs-lookup"><span data-stu-id="fb691-595">string</span></span>|<span data-ttu-id="fb691-596">128文字</span><span class="sxs-lookup"><span data-stu-id="fb691-596">128 characters</span></span>|<span data-ttu-id="fb691-597">✔</span><span class="sxs-lookup"><span data-stu-id="fb691-597">✔</span></span>|<span data-ttu-id="fb691-598">Ex: "{actor} ' のタスク {taskId} が作成されました"</span><span class="sxs-lookup"><span data-stu-id="fb691-598">Ex: "{actor} created task {taskId} for you"</span></span>|

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
