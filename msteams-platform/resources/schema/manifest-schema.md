---
title: マニフェストスキーマの参照
description: Microsoft Teams のマニフェストによってサポートされるスキーマについて説明します。
keywords: teams マニフェストスキーマ
author: laujan
ms.author: lajanuar
ms.openlocfilehash: aea75276d37ae0a99ecc55b204d29706cc5a07c8
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237980"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="642a2-104">リファレンス: Microsoft Teams のマニフェストスキーマ</span><span class="sxs-lookup"><span data-stu-id="642a2-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="642a2-105">Microsoft Teams のマニフェストでは、アプリを Microsoft Teams 製品に統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="642a2-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="642a2-106">マニフェストは、でホストされているスキーマに準拠している必要があり [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) ます。</span><span class="sxs-lookup"><span data-stu-id="642a2-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="642a2-107">以前のバージョン 1.0-1.4 もサポートされています (URL で "v1" を使用します)。</span><span class="sxs-lookup"><span data-stu-id="642a2-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="642a2-108">次のスキーマサンプルは、すべての拡張オプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="642a2-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="642a2-109">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="642a2-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.7",
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
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": "Define how your tab wil be made available in SharePoint (full page or web part)"
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser"
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

<span data-ttu-id="642a2-110">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="642a2-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="642a2-111">$schema</span><span class="sxs-lookup"><span data-stu-id="642a2-111">$schema</span></span>

<span data-ttu-id="642a2-112">*省略可能 (ただし推奨* ) 文字列</span><span class="sxs-lookup"><span data-stu-id="642a2-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="642a2-113">マニフェストの JSON スキーマを参照する https://URL。</span><span class="sxs-lookup"><span data-stu-id="642a2-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="642a2-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="642a2-114">manifestVersion</span></span>

<span data-ttu-id="642a2-115">**必須** -文字列</span><span class="sxs-lookup"><span data-stu-id="642a2-115">**Required** — string</span></span>

<span data-ttu-id="642a2-116">このマニフェストが使用しているマニフェストスキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="642a2-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="642a2-117">"1.5" である必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="642a2-118">バージョン</span><span class="sxs-lookup"><span data-stu-id="642a2-118">version</span></span>

<span data-ttu-id="642a2-119">**必須** -文字列</span><span class="sxs-lookup"><span data-stu-id="642a2-119">**Required** — string</span></span>

<span data-ttu-id="642a2-120">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="642a2-120">The version of the specific app.</span></span> <span data-ttu-id="642a2-121">マニフェスト内の内容を更新する場合は、そのバージョンも同時にインクリメントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="642a2-122">このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。</span><span class="sxs-lookup"><span data-stu-id="642a2-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="642a2-123">このアプリがストアに送信された場合は、新しいマニフェストを再送信して再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="642a2-124">その後、このアプリのユーザーは、承認後に数時間以内に新しい更新されたマニフェストを自動的に取得します。</span><span class="sxs-lookup"><span data-stu-id="642a2-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="642a2-125">アプリによって要求されたアクセス許可が変更された場合、ユーザーはアプリをアップグレードして再同意するように求められます。</span><span class="sxs-lookup"><span data-stu-id="642a2-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="642a2-126">このバージョンの文字列は、 [semver](http://semver.org/) 標準 (メジャー) に従う必要があります。間隔.パッチ)。</span><span class="sxs-lookup"><span data-stu-id="642a2-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="642a2-127">id</span><span class="sxs-lookup"><span data-stu-id="642a2-127">id</span></span>

<span data-ttu-id="642a2-128">**必須** -MICROSOFT アプリ ID</span><span class="sxs-lookup"><span data-stu-id="642a2-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="642a2-129">このアプリの一意の Microsoft 生成識別子。</span><span class="sxs-lookup"><span data-stu-id="642a2-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="642a2-130">Microsoft Bot フレームワークを介して bot を登録した場合、またはタブの web アプリが Microsoft によって既にサインインしている場合は、既に ID があるので、ここで入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="642a2-131">それ以外の場合は、Microsoft アプリケーション登録ポータル ([My Applications](https://apps.dev.microsoft.com)) で新しい ID を生成し、ここで入力してから、bot を追加するときにそれを再利用する必要があります。注: AppSource で既存のアプリに更新を送信する場合は、マニフェスト内の ID を変更しないでください。</span><span class="sxs-lookup"><span data-stu-id="642a2-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="642a2-132">developer</span><span class="sxs-lookup"><span data-stu-id="642a2-132">developer</span></span>

<span data-ttu-id="642a2-133">**Required** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="642a2-133">**Required** — object</span></span>

<span data-ttu-id="642a2-134">会社に関する情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="642a2-134">Specifies information about your company.</span></span> <span data-ttu-id="642a2-135">AppSource (旧称 Office ストア) に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="642a2-136">追加情報については、 [発行に関するガイドライン](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="642a2-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="642a2-137">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-137">Name</span></span>| <span data-ttu-id="642a2-138">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-138">Maximum size</span></span> | <span data-ttu-id="642a2-139">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-139">Required</span></span> | <span data-ttu-id="642a2-140">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="642a2-141">32文字</span><span class="sxs-lookup"><span data-stu-id="642a2-141">32 characters</span></span>|<span data-ttu-id="642a2-142">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-142">✔</span></span>|<span data-ttu-id="642a2-143">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="642a2-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="642a2-144">2048 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-144">2048 characters</span></span>|<span data-ttu-id="642a2-145">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-145">✔</span></span>|<span data-ttu-id="642a2-146">開発者の web サイトへの https://URL。</span><span class="sxs-lookup"><span data-stu-id="642a2-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="642a2-147">このリンクは、ユーザーを会社または製品固有のランディングページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="642a2-148">2048 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-148">2048 characters</span></span>|<span data-ttu-id="642a2-149">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-149">✔</span></span>|<span data-ttu-id="642a2-150">開発者のプライバシーポリシーへの https://URL。</span><span class="sxs-lookup"><span data-stu-id="642a2-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="642a2-151">2048 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-151">2048 characters</span></span>|<span data-ttu-id="642a2-152">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-152">✔</span></span>|<span data-ttu-id="642a2-153">開発者の使用条件への https://URL。</span><span class="sxs-lookup"><span data-stu-id="642a2-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="642a2-154">10文字</span><span class="sxs-lookup"><span data-stu-id="642a2-154">10 characters</span></span>| |<span data-ttu-id="642a2-155">**省略可能** アプリを構築するパートナー組織を識別する Microsoft パートナーのネットワーク ID。</span><span class="sxs-lookup"><span data-stu-id="642a2-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="642a2-156">name</span><span class="sxs-lookup"><span data-stu-id="642a2-156">name</span></span>

<span data-ttu-id="642a2-157">**Required** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="642a2-157">**Required** — object</span></span>

<span data-ttu-id="642a2-158">Teams でユーザーに表示されるアプリの動作の名前です。</span><span class="sxs-lookup"><span data-stu-id="642a2-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="642a2-159">AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="642a2-160">との値 `short` を同じにすることはでき `full` ません。</span><span class="sxs-lookup"><span data-stu-id="642a2-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="642a2-161">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-161">Name</span></span>| <span data-ttu-id="642a2-162">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-162">Maximum size</span></span> | <span data-ttu-id="642a2-163">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-163">Required</span></span> | <span data-ttu-id="642a2-164">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="642a2-165">30 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-165">30 characters</span></span>|<span data-ttu-id="642a2-166">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-166">✔</span></span>|<span data-ttu-id="642a2-167">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="642a2-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="642a2-168">100 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-168">100 characters</span></span>||<span data-ttu-id="642a2-169">アプリの完全な名前。アプリの完全な名前が30文字を超えている場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="642a2-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="642a2-170">description</span><span class="sxs-lookup"><span data-stu-id="642a2-170">description</span></span>

<span data-ttu-id="642a2-171">**Required** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="642a2-171">**Required** — object</span></span>

<span data-ttu-id="642a2-172">ユーザーに対してアプリを記述します。</span><span class="sxs-lookup"><span data-stu-id="642a2-172">Describes your app to users.</span></span> <span data-ttu-id="642a2-173">AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="642a2-174">説明に正確に表示されていることを確認し、お客様が快適な動作を理解するのに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="642a2-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="642a2-175">また、外部アカウントが使用するために必要な場合は、詳細な説明にも注意してください。</span><span class="sxs-lookup"><span data-stu-id="642a2-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="642a2-176">との値 `short` を同じにすることはでき `full` ません。</span><span class="sxs-lookup"><span data-stu-id="642a2-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="642a2-177">短い説明を長い説明の中で繰り返すことはできません。他のアプリ名を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="642a2-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="642a2-178">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-178">Name</span></span>| <span data-ttu-id="642a2-179">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-179">Maximum size</span></span> | <span data-ttu-id="642a2-180">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-180">Required</span></span> | <span data-ttu-id="642a2-181">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="642a2-182">80文字</span><span class="sxs-lookup"><span data-stu-id="642a2-182">80 characters</span></span>|<span data-ttu-id="642a2-183">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-183">✔</span></span>|<span data-ttu-id="642a2-184">スペースが制限されている場合に使用する、アプリの使用状況の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="642a2-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="642a2-185">4000文字</span><span class="sxs-lookup"><span data-stu-id="642a2-185">4000 characters</span></span>|<span data-ttu-id="642a2-186">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-186">✔</span></span>|<span data-ttu-id="642a2-187">アプリの詳細な説明。</span><span class="sxs-lookup"><span data-stu-id="642a2-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="642a2-188">packageName</span><span class="sxs-lookup"><span data-stu-id="642a2-188">packageName</span></span>

<span data-ttu-id="642a2-189">**省略可能** (string)</span><span class="sxs-lookup"><span data-stu-id="642a2-189">**Optional** — string</span></span>

<span data-ttu-id="642a2-190">逆引きドメイン表記でのこのアプリの一意識別子。たとえば、例のようになります。</span><span class="sxs-lookup"><span data-stu-id="642a2-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="642a2-191">最大長: 64 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="642a2-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="642a2-192">localizationInfo</span></span>

<span data-ttu-id="642a2-193">**Optional** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="642a2-193">**Optional** — object</span></span>

<span data-ttu-id="642a2-194">既定の言語の指定、および追加の言語ファイルへのポインターを許可します。</span><span class="sxs-lookup"><span data-stu-id="642a2-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="642a2-195">「 [ローカライズ](~/concepts/build-and-test/apps-localization.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="642a2-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="642a2-196">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-196">Name</span></span>| <span data-ttu-id="642a2-197">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-197">Maximum size</span></span> | <span data-ttu-id="642a2-198">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-198">Required</span></span> | <span data-ttu-id="642a2-199">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="642a2-200">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-200">✔</span></span>|<span data-ttu-id="642a2-201">このトップレベルマニフェストファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="642a2-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="642a2-202">localizationInfo. additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="642a2-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="642a2-203">追加の言語の翻訳を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="642a2-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="642a2-204">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-204">Name</span></span>| <span data-ttu-id="642a2-205">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-205">Maximum size</span></span> | <span data-ttu-id="642a2-206">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-206">Required</span></span> | <span data-ttu-id="642a2-207">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="642a2-208">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-208">✔</span></span>|<span data-ttu-id="642a2-209">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="642a2-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="642a2-210">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-210">✔</span></span>|<span data-ttu-id="642a2-211">翻訳された文字列を含む json ファイルへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="642a2-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="642a2-212">アイコン</span><span class="sxs-lookup"><span data-stu-id="642a2-212">icons</span></span>

<span data-ttu-id="642a2-213">**Required** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="642a2-213">**Required** — object</span></span>

<span data-ttu-id="642a2-214">Teams アプリ内で使用されるアイコン。</span><span class="sxs-lookup"><span data-stu-id="642a2-214">Icons used within the Teams app.</span></span> <span data-ttu-id="642a2-215">アイコンファイルは、アップロードパッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="642a2-216">詳細については、「 [アイコン](~/concepts/build-and-test/apps-package.md#icons) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="642a2-216">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="642a2-217">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-217">Name</span></span>| <span data-ttu-id="642a2-218">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-218">Maximum size</span></span> | <span data-ttu-id="642a2-219">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-219">Required</span></span> | <span data-ttu-id="642a2-220">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="642a2-221">32 x 32 ピクセル</span><span class="sxs-lookup"><span data-stu-id="642a2-221">32 x 32 pixels</span></span>|<span data-ttu-id="642a2-222">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-222">✔</span></span>|<span data-ttu-id="642a2-223">透明な32x32 の PNG アウトラインアイコンへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="642a2-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="642a2-224">192 x 192 ピクセル</span><span class="sxs-lookup"><span data-stu-id="642a2-224">192 x 192 pixels</span></span>|<span data-ttu-id="642a2-225">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-225">✔</span></span>|<span data-ttu-id="642a2-226">フルカラー 192x192 PNG アイコンへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="642a2-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="642a2-227">アクセントカラー</span><span class="sxs-lookup"><span data-stu-id="642a2-227">accentColor</span></span>

<span data-ttu-id="642a2-228">**オプション** -HTML 16 進カラーコード</span><span class="sxs-lookup"><span data-stu-id="642a2-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="642a2-229">とと組み合わせてアウトラインアイコンの背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="642a2-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="642a2-230">この値は、' # ' で始まる有効な HTML カラーコードである必要があります (例 `#4464ee` :)。</span><span class="sxs-lookup"><span data-stu-id="642a2-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="642a2-231">の各タブ</span><span class="sxs-lookup"><span data-stu-id="642a2-231">configurableTabs</span></span>

<span data-ttu-id="642a2-232">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="642a2-232">**Optional** — array</span></span>

<span data-ttu-id="642a2-233">アプリの機能に、追加の構成を必要とするチームチャネルのタブがある場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="642a2-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="642a2-234">構成可能なタブは teams スコープ (個人ではない) でのみサポートされており、現在、アプリごとに **1 つ** のタブのみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="642a2-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="642a2-235">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-235">Name</span></span>| <span data-ttu-id="642a2-236">型</span><span class="sxs-lookup"><span data-stu-id="642a2-236">Type</span></span>| <span data-ttu-id="642a2-237">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-237">Maximum size</span></span> | <span data-ttu-id="642a2-238">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-238">Required</span></span> | <span data-ttu-id="642a2-239">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="642a2-240">string</span><span class="sxs-lookup"><span data-stu-id="642a2-240">string</span></span>|<span data-ttu-id="642a2-241">2048 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-241">2048 characters</span></span>|<span data-ttu-id="642a2-242">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-242">✔</span></span>|<span data-ttu-id="642a2-243">タブを構成するときに使用する https://URL。</span><span class="sxs-lookup"><span data-stu-id="642a2-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="642a2-244">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="642a2-244">array of enum</span></span>|<span data-ttu-id="642a2-245">1-d</span><span class="sxs-lookup"><span data-stu-id="642a2-245">1</span></span>|<span data-ttu-id="642a2-246">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-246">✔</span></span>|<span data-ttu-id="642a2-247">現在、構成可能なタブでは、およびスコープのみがサポートさ `team` `groupchat` れています。</span><span class="sxs-lookup"><span data-stu-id="642a2-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="642a2-248">boolean</span><span class="sxs-lookup"><span data-stu-id="642a2-248">boolean</span></span>|||<span data-ttu-id="642a2-249">作成後にタブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="642a2-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="642a2-250">既定値は **true**です。</span><span class="sxs-lookup"><span data-stu-id="642a2-250">Default: **true**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="642a2-251">string</span><span class="sxs-lookup"><span data-stu-id="642a2-251">string</span></span>|<span data-ttu-id="642a2-252">2048</span><span class="sxs-lookup"><span data-stu-id="642a2-252">2048</span></span>||<span data-ttu-id="642a2-253">SharePoint で使用するタブプレビュー画像への相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="642a2-253">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="642a2-254">サイズ1024x768。</span><span class="sxs-lookup"><span data-stu-id="642a2-254">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="642a2-255">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="642a2-255">array of enum</span></span>|<span data-ttu-id="642a2-256">1-d</span><span class="sxs-lookup"><span data-stu-id="642a2-256">1</span></span>||<span data-ttu-id="642a2-257">SharePoint でどのようにタブを使用できるようにするかを定義します。</span><span class="sxs-lookup"><span data-stu-id="642a2-257">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="642a2-258">オプション `sharePointFullPage` と `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="642a2-258">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="642a2-259">staticTabs</span><span class="sxs-lookup"><span data-stu-id="642a2-259">staticTabs</span></span>

<span data-ttu-id="642a2-260">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="642a2-260">**Optional** — array</span></span>

<span data-ttu-id="642a2-261">ユーザーが手動で追加せずに、既定で "固定" できるタブのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="642a2-261">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="642a2-262">スコープ内で宣言 `personal` されている静的タブは、常にアプリの個人の環境に固定されます。</span><span class="sxs-lookup"><span data-stu-id="642a2-262">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="642a2-263">スコープ内で宣言されている静的タブ `team` は現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="642a2-263">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="642a2-264">この項目は、型のすべての要素を含む配列 (最大16個の要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="642a2-264">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="642a2-265">このブロックは、静的なタブソリューションを提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="642a2-265">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="642a2-266">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-266">Name</span></span>| <span data-ttu-id="642a2-267">型</span><span class="sxs-lookup"><span data-stu-id="642a2-267">Type</span></span>| <span data-ttu-id="642a2-268">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-268">Maximum size</span></span> | <span data-ttu-id="642a2-269">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-269">Required</span></span> | <span data-ttu-id="642a2-270">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-270">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="642a2-271">string</span><span class="sxs-lookup"><span data-stu-id="642a2-271">string</span></span>|<span data-ttu-id="642a2-272">64 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-272">64 characters</span></span>|<span data-ttu-id="642a2-273">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-273">✔</span></span>|<span data-ttu-id="642a2-274">タブに表示されるエンティティの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="642a2-274">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="642a2-275">string</span><span class="sxs-lookup"><span data-stu-id="642a2-275">string</span></span>|<span data-ttu-id="642a2-276">128文字</span><span class="sxs-lookup"><span data-stu-id="642a2-276">128 characters</span></span>|<span data-ttu-id="642a2-277">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-277">✔</span></span>|<span data-ttu-id="642a2-278">チャネルインターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="642a2-278">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="642a2-279">string</span><span class="sxs-lookup"><span data-stu-id="642a2-279">string</span></span>|<span data-ttu-id="642a2-280">2048 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-280">2048 characters</span></span>|<span data-ttu-id="642a2-281">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-281">✔</span></span>|<span data-ttu-id="642a2-282">Teams キャンバスに表示されるエンティティ UI をポイントする https://URL。</span><span class="sxs-lookup"><span data-stu-id="642a2-282">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="642a2-283">string</span><span class="sxs-lookup"><span data-stu-id="642a2-283">string</span></span>|<span data-ttu-id="642a2-284">2048 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-284">2048 characters</span></span>||<span data-ttu-id="642a2-285">ユーザーがブラウザーで表示をポイントしたかどうかを示す https://URL。</span><span class="sxs-lookup"><span data-stu-id="642a2-285">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="642a2-286">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="642a2-286">array of enum</span></span>|<span data-ttu-id="642a2-287">1-d</span><span class="sxs-lookup"><span data-stu-id="642a2-287">1</span></span>|<span data-ttu-id="642a2-288">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-288">✔</span></span>|<span data-ttu-id="642a2-289">現時点では、静的タブではスコープのみがサポート `personal` されます。つまり、個人の利便性の一環としてのみプロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="642a2-289">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

> [!NOTE]
> <span data-ttu-id="642a2-290">関連するコンテンツを表示したり、認証フローを開始したりするために、タブにコンテキスト依存情報が必要な場合は、「 [Microsoft Teams のコンテキストを取得する」タブ](../../tabs/how-to/access-teams-context.md)を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="642a2-290">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="642a2-291">bot</span><span class="sxs-lookup"><span data-stu-id="642a2-291">bots</span></span>

<span data-ttu-id="642a2-292">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="642a2-292">**Optional** — array</span></span>

<span data-ttu-id="642a2-293">Bot ソリューションと、既定のコマンドプロパティなどのオプション情報を定義します。</span><span class="sxs-lookup"><span data-stu-id="642a2-293">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="642a2-294">アイテムが配列の場合 (現時点では1つの要素のみ &mdash; が可能)、その型のすべての要素が含まれ `object` ます。</span><span class="sxs-lookup"><span data-stu-id="642a2-294">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="642a2-295">このブロックは、bot の環境を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="642a2-295">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="642a2-296">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-296">Name</span></span>| <span data-ttu-id="642a2-297">型</span><span class="sxs-lookup"><span data-stu-id="642a2-297">Type</span></span>| <span data-ttu-id="642a2-298">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-298">Maximum size</span></span> | <span data-ttu-id="642a2-299">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-299">Required</span></span> | <span data-ttu-id="642a2-300">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-300">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="642a2-301">string</span><span class="sxs-lookup"><span data-stu-id="642a2-301">string</span></span>|<span data-ttu-id="642a2-302">64 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-302">64 characters</span></span>|<span data-ttu-id="642a2-303">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-303">✔</span></span>|<span data-ttu-id="642a2-304">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="642a2-304">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="642a2-305">これは、アプリの全体的な [ID](#id)と同じである場合もあります。</span><span class="sxs-lookup"><span data-stu-id="642a2-305">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="642a2-306">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="642a2-306">array of enum</span></span>|<span data-ttu-id="642a2-307">1/3</span><span class="sxs-lookup"><span data-stu-id="642a2-307">3</span></span>|<span data-ttu-id="642a2-308">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-308">✔</span></span>|<span data-ttu-id="642a2-309">ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。</span><span class="sxs-lookup"><span data-stu-id="642a2-309">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="642a2-310">これらのオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="642a2-310">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="642a2-311">boolean</span><span class="sxs-lookup"><span data-stu-id="642a2-311">boolean</span></span>|||<span data-ttu-id="642a2-312">ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。</span><span class="sxs-lookup"><span data-stu-id="642a2-312">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="642a2-313">限り **`false`**</span><span class="sxs-lookup"><span data-stu-id="642a2-313">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="642a2-314">boolean</span><span class="sxs-lookup"><span data-stu-id="642a2-314">boolean</span></span>|||<span data-ttu-id="642a2-315">ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="642a2-315">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="642a2-316">限り `**false**`</span><span class="sxs-lookup"><span data-stu-id="642a2-316">Default: `**false**`</span></span>|
|`supportsFiles`|<span data-ttu-id="642a2-317">boolean</span><span class="sxs-lookup"><span data-stu-id="642a2-317">boolean</span></span>|||<span data-ttu-id="642a2-318">パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="642a2-318">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="642a2-319">限り **`false`**</span><span class="sxs-lookup"><span data-stu-id="642a2-319">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="642a2-320">bot リスト</span><span class="sxs-lookup"><span data-stu-id="642a2-320">bots.commandLists</span></span>

<span data-ttu-id="642a2-321">Bot がユーザーに推奨できるコマンドのオプションの一覧。</span><span class="sxs-lookup"><span data-stu-id="642a2-321">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="642a2-322">Object は、型のすべての要素を含む配列 (最大2つの要素) です `object` 。 bot がサポートするスコープごとに個別のコマンドリストを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-322">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="642a2-323">詳細については、「 [Bot メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="642a2-323">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="642a2-324">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-324">Name</span></span>| <span data-ttu-id="642a2-325">型</span><span class="sxs-lookup"><span data-stu-id="642a2-325">Type</span></span>| <span data-ttu-id="642a2-326">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-326">Maximum size</span></span> | <span data-ttu-id="642a2-327">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-327">Required</span></span> | <span data-ttu-id="642a2-328">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-328">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="642a2-329">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="642a2-329">array of enum</span></span>|<span data-ttu-id="642a2-330">1/3</span><span class="sxs-lookup"><span data-stu-id="642a2-330">3</span></span>|<span data-ttu-id="642a2-331">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-331">✔</span></span>|<span data-ttu-id="642a2-332">コマンド リストが有効なスコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="642a2-332">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="642a2-333">`team`、`personal`、`groupchat` の中から選択できます。</span><span class="sxs-lookup"><span data-stu-id="642a2-333">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="642a2-334">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="642a2-334">array of objects</span></span>|<span data-ttu-id="642a2-335">10 </span><span class="sxs-lookup"><span data-stu-id="642a2-335">10</span></span>|<span data-ttu-id="642a2-336">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-336">✔</span></span>|<span data-ttu-id="642a2-337">ボットがサポートするコマンドの配列:</span><span class="sxs-lookup"><span data-stu-id="642a2-337">An array of commands the bot supports:</span></span><br><span data-ttu-id="642a2-338">`title`: ボット コマンドの名前 (文字列、32)</span><span class="sxs-lookup"><span data-stu-id="642a2-338">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="642a2-339">`description`: コマンドの構文およびその構文の引数
の簡単な説明または例 (文字列、128)</span><span class="sxs-lookup"><span data-stu-id="642a2-339">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="642a2-340">bot のリストコマンド</span><span class="sxs-lookup"><span data-stu-id="642a2-340">bots.commandLists.commands</span></span>

|<span data-ttu-id="642a2-341">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-341">Name</span></span>| <span data-ttu-id="642a2-342">型</span><span class="sxs-lookup"><span data-stu-id="642a2-342">Type</span></span>| <span data-ttu-id="642a2-343">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-343">Maximum size</span></span> | <span data-ttu-id="642a2-344">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-344">Required</span></span> | <span data-ttu-id="642a2-345">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-345">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="642a2-346">title</span><span class="sxs-lookup"><span data-stu-id="642a2-346">title</span></span>|<span data-ttu-id="642a2-347">string</span><span class="sxs-lookup"><span data-stu-id="642a2-347">string</span></span>|<span data-ttu-id="642a2-348">12 </span><span class="sxs-lookup"><span data-stu-id="642a2-348">12</span></span>|<span data-ttu-id="642a2-349">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-349">✔</span></span>|<span data-ttu-id="642a2-350">Bot コマンド名</span><span class="sxs-lookup"><span data-stu-id="642a2-350">The bot command name</span></span>|
|<span data-ttu-id="642a2-351">description</span><span class="sxs-lookup"><span data-stu-id="642a2-351">description</span></span>|<span data-ttu-id="642a2-352">string</span><span class="sxs-lookup"><span data-stu-id="642a2-352">string</span></span>|<span data-ttu-id="642a2-353">128文字</span><span class="sxs-lookup"><span data-stu-id="642a2-353">128 characters</span></span>|<span data-ttu-id="642a2-354">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-354">✔</span></span>|<span data-ttu-id="642a2-355">簡単なテキストの説明、またはコマンド構文とその引数の例。</span><span class="sxs-lookup"><span data-stu-id="642a2-355">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="642a2-356">コネクタ</span><span class="sxs-lookup"><span data-stu-id="642a2-356">connectors</span></span>

<span data-ttu-id="642a2-357">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="642a2-357">**Optional** — array</span></span>

<span data-ttu-id="642a2-358">ブロックは、 `connectors` アプリの Office 365 コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="642a2-358">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="642a2-359">Object は、type のすべての要素を含む配列 (最大1つの要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="642a2-359">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="642a2-360">このブロックは、コネクタを提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="642a2-360">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="642a2-361">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-361">Name</span></span>| <span data-ttu-id="642a2-362">型</span><span class="sxs-lookup"><span data-stu-id="642a2-362">Type</span></span>| <span data-ttu-id="642a2-363">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-363">Maximum size</span></span> | <span data-ttu-id="642a2-364">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-364">Required</span></span> | <span data-ttu-id="642a2-365">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-365">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="642a2-366">string</span><span class="sxs-lookup"><span data-stu-id="642a2-366">string</span></span>|<span data-ttu-id="642a2-367">2048 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-367">2048 characters</span></span>|<span data-ttu-id="642a2-368">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-368">✔</span></span>|<span data-ttu-id="642a2-369">コネクタを構成するときに使用する https://URL。</span><span class="sxs-lookup"><span data-stu-id="642a2-369">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="642a2-370">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="642a2-370">array of enum</span></span>|<span data-ttu-id="642a2-371">1-d</span><span class="sxs-lookup"><span data-stu-id="642a2-371">1</span></span>|<span data-ttu-id="642a2-372">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-372">✔</span></span>|<span data-ttu-id="642a2-373">コネクタが内のチャネルのコンテキストで、 `team` または個別のユーザー単独 () にスコープ設定された環境での動作を提供するかどうかを指定し `personal` ます。</span><span class="sxs-lookup"><span data-stu-id="642a2-373">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="642a2-374">現時点では、 `team` 範囲のみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="642a2-374">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="642a2-375">string</span><span class="sxs-lookup"><span data-stu-id="642a2-375">string</span></span>|<span data-ttu-id="642a2-376">64 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-376">64 characters</span></span>|<span data-ttu-id="642a2-377">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-377">✔</span></span>|<span data-ttu-id="642a2-378">コネクタ [開発者ダッシュボード](https://aka.ms/connectorsdashboard)の ID と一致するコネクタの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="642a2-378">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="642a2-379">この機能</span><span class="sxs-lookup"><span data-stu-id="642a2-379">composeExtensions</span></span>

<span data-ttu-id="642a2-380">**省略可能** -配列</span><span class="sxs-lookup"><span data-stu-id="642a2-380">**Optional** — array</span></span>

<span data-ttu-id="642a2-381">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="642a2-381">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="642a2-382">この機能の名前は、2017年11月に「[作成] 拡張機能」から「messaging extension」に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は同じままです。</span><span class="sxs-lookup"><span data-stu-id="642a2-382">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="642a2-383">Item は、type のすべての要素を含む配列 (最大1つの要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="642a2-383">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="642a2-384">このブロックは、メッセージング拡張機能を提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="642a2-384">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="642a2-385">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-385">Name</span></span>| <span data-ttu-id="642a2-386">種類</span><span class="sxs-lookup"><span data-stu-id="642a2-386">Type</span></span> | <span data-ttu-id="642a2-387">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-387">Maximum Size</span></span> | <span data-ttu-id="642a2-388">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-388">Required</span></span> | <span data-ttu-id="642a2-389">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-389">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="642a2-390">string</span><span class="sxs-lookup"><span data-stu-id="642a2-390">string</span></span>|<span data-ttu-id="642a2-391">64</span><span class="sxs-lookup"><span data-stu-id="642a2-391">64</span></span>|<span data-ttu-id="642a2-392">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-392">✔</span></span>|<span data-ttu-id="642a2-393">Bot フレームワークに登録されているメッセージング拡張機能をバックアップする bot の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="642a2-393">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="642a2-394">これは、アプリの全体的な ID と同じである場合もあります。</span><span class="sxs-lookup"><span data-stu-id="642a2-394">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="642a2-395">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="642a2-395">array of objects</span></span>|<span data-ttu-id="642a2-396">10 </span><span class="sxs-lookup"><span data-stu-id="642a2-396">10</span></span>|<span data-ttu-id="642a2-397">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-397">✔</span></span>|<span data-ttu-id="642a2-398">メッセージング拡張機能がサポートするコマンドの配列</span><span class="sxs-lookup"><span data-stu-id="642a2-398">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="642a2-399">boolean</span><span class="sxs-lookup"><span data-stu-id="642a2-399">boolean</span></span>|||<span data-ttu-id="642a2-400">メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="642a2-400">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="642a2-401">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="642a2-401">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="642a2-402">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="642a2-402">array of Objects</span></span>|<span data-ttu-id="642a2-403">5 </span><span class="sxs-lookup"><span data-stu-id="642a2-403">5</span></span>||<span data-ttu-id="642a2-404">特定の条件が満たされたときにアプリを呼び出せるようにするハンドラーの一覧。</span><span class="sxs-lookup"><span data-stu-id="642a2-404">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="642a2-405">ドメインも、にリストされている必要があります。 `validDomains`</span><span class="sxs-lookup"><span data-stu-id="642a2-405">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="642a2-406">string</span><span class="sxs-lookup"><span data-stu-id="642a2-406">string</span></span>|||<span data-ttu-id="642a2-407">メッセージハンドラの種類。</span><span class="sxs-lookup"><span data-stu-id="642a2-407">The type of message handler.</span></span> <span data-ttu-id="642a2-408">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-408">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="642a2-409">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="642a2-409">array of Strings</span></span>|||<span data-ttu-id="642a2-410">リンクメッセージハンドラが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="642a2-410">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="642a2-411">このコマンドの機能</span><span class="sxs-lookup"><span data-stu-id="642a2-411">composeExtensions.commands</span></span>

<span data-ttu-id="642a2-412">メッセージング拡張機能は、1つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-412">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="642a2-413">各コマンドは、Microsoft Teams に UI ベースのエントリポイントからの潜在的な操作として表示されます。</span><span class="sxs-lookup"><span data-stu-id="642a2-413">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="642a2-414">最大10個のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="642a2-414">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="642a2-415">各コマンド項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="642a2-415">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="642a2-416">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-416">Name</span></span>| <span data-ttu-id="642a2-417">型</span><span class="sxs-lookup"><span data-stu-id="642a2-417">Type</span></span>| <span data-ttu-id="642a2-418">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-418">Maximum size</span></span> | <span data-ttu-id="642a2-419">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-419">Required</span></span> | <span data-ttu-id="642a2-420">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-420">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="642a2-421">string</span><span class="sxs-lookup"><span data-stu-id="642a2-421">string</span></span>|<span data-ttu-id="642a2-422">64 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-422">64 characters</span></span>|<span data-ttu-id="642a2-423">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-423">✔</span></span>|<span data-ttu-id="642a2-424">コマンドの ID。</span><span class="sxs-lookup"><span data-stu-id="642a2-424">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="642a2-425">string</span><span class="sxs-lookup"><span data-stu-id="642a2-425">string</span></span>|<span data-ttu-id="642a2-426">32文字</span><span class="sxs-lookup"><span data-stu-id="642a2-426">32 characters</span></span>|<span data-ttu-id="642a2-427">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-427">✔</span></span>|<span data-ttu-id="642a2-428">ユーザーフレンドリなコマンド名。</span><span class="sxs-lookup"><span data-stu-id="642a2-428">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="642a2-429">string</span><span class="sxs-lookup"><span data-stu-id="642a2-429">string</span></span>|<span data-ttu-id="642a2-430">64 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-430">64 characters</span></span>||<span data-ttu-id="642a2-431">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="642a2-431">Type of the command.</span></span> <span data-ttu-id="642a2-432">またはのいずれか `query` `action` です。</span><span class="sxs-lookup"><span data-stu-id="642a2-432">One of `query` or `action`.</span></span> <span data-ttu-id="642a2-433">既定値: **query**。</span><span class="sxs-lookup"><span data-stu-id="642a2-433">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="642a2-434">string</span><span class="sxs-lookup"><span data-stu-id="642a2-434">string</span></span>|<span data-ttu-id="642a2-435">128文字</span><span class="sxs-lookup"><span data-stu-id="642a2-435">128 characters</span></span>||<span data-ttu-id="642a2-436">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="642a2-436">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="642a2-437">boolean</span><span class="sxs-lookup"><span data-stu-id="642a2-437">boolean</span></span>|||<span data-ttu-id="642a2-438">パラメーターを指定せずにコマンドを最初に実行する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="642a2-438">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="642a2-439">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="642a2-439">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="642a2-440">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="642a2-440">array of Strings</span></span>|<span data-ttu-id="642a2-441">1/3</span><span class="sxs-lookup"><span data-stu-id="642a2-441">3</span></span>||<span data-ttu-id="642a2-442">メッセージの内線番号をから呼び出すことができる場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="642a2-442">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="642a2-443">、、の任意の組み合わせ `compose` `commandBox` `message` 。</span><span class="sxs-lookup"><span data-stu-id="642a2-443">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="642a2-444">既定値は `["compose","commandBox"]` です。</span><span class="sxs-lookup"><span data-stu-id="642a2-444">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="642a2-445">boolean</span><span class="sxs-lookup"><span data-stu-id="642a2-445">boolean</span></span>|||<span data-ttu-id="642a2-446">タスクモジュールを動的にフェッチする必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="642a2-446">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="642a2-447">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="642a2-447">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="642a2-448">object</span><span class="sxs-lookup"><span data-stu-id="642a2-448">object</span></span>|||<span data-ttu-id="642a2-449">メッセージ拡張コマンドの使用時に、タスクモジュールを事前に読み込むように指定します。</span><span class="sxs-lookup"><span data-stu-id="642a2-449">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="642a2-450">string</span><span class="sxs-lookup"><span data-stu-id="642a2-450">string</span></span>|<span data-ttu-id="642a2-451">64 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-451">64 characters</span></span>||<span data-ttu-id="642a2-452">最初のダイアログのタイトル。</span><span class="sxs-lookup"><span data-stu-id="642a2-452">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="642a2-453">string</span><span class="sxs-lookup"><span data-stu-id="642a2-453">string</span></span>|||<span data-ttu-id="642a2-454">ダイアログの幅。ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="642a2-454">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="642a2-455">string</span><span class="sxs-lookup"><span data-stu-id="642a2-455">string</span></span>|||<span data-ttu-id="642a2-456">ダイアログの高さ-ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="642a2-456">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="642a2-457">string</span><span class="sxs-lookup"><span data-stu-id="642a2-457">string</span></span>|||<span data-ttu-id="642a2-458">最初の webview の URL。</span><span class="sxs-lookup"><span data-stu-id="642a2-458">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="642a2-459">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="642a2-459">array of object</span></span>|<span data-ttu-id="642a2-460">5アイテム</span><span class="sxs-lookup"><span data-stu-id="642a2-460">5 items</span></span>|<span data-ttu-id="642a2-461">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-461">✔</span></span>|<span data-ttu-id="642a2-462">コマンドが実行するパラメーターの一覧。</span><span class="sxs-lookup"><span data-stu-id="642a2-462">The list of parameters the command takes.</span></span> <span data-ttu-id="642a2-463">最小値: 1、最大: 5</span><span class="sxs-lookup"><span data-stu-id="642a2-463">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="642a2-464">string</span><span class="sxs-lookup"><span data-stu-id="642a2-464">string</span></span>|<span data-ttu-id="642a2-465">64 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-465">64 characters</span></span>|<span data-ttu-id="642a2-466">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-466">✔</span></span>|<span data-ttu-id="642a2-467">クライアントに表示されるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="642a2-467">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="642a2-468">これは、ユーザー要求に含まれています。</span><span class="sxs-lookup"><span data-stu-id="642a2-468">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="642a2-469">string</span><span class="sxs-lookup"><span data-stu-id="642a2-469">string</span></span>|<span data-ttu-id="642a2-470">32文字</span><span class="sxs-lookup"><span data-stu-id="642a2-470">32 characters</span></span>|<span data-ttu-id="642a2-471">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-471">✔</span></span>|<span data-ttu-id="642a2-472">パラメーターのユーザーフレンドリなタイトル。</span><span class="sxs-lookup"><span data-stu-id="642a2-472">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="642a2-473">string</span><span class="sxs-lookup"><span data-stu-id="642a2-473">string</span></span>|<span data-ttu-id="642a2-474">128文字</span><span class="sxs-lookup"><span data-stu-id="642a2-474">128 characters</span></span>||<span data-ttu-id="642a2-475">このパラメーターの目的を説明するユーザーフレンドリ文字列。</span><span class="sxs-lookup"><span data-stu-id="642a2-475">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="642a2-476">string</span><span class="sxs-lookup"><span data-stu-id="642a2-476">string</span></span>|<span data-ttu-id="642a2-477">512文字</span><span class="sxs-lookup"><span data-stu-id="642a2-477">512 characters</span></span>||<span data-ttu-id="642a2-478">パラメータの初期値。</span><span class="sxs-lookup"><span data-stu-id="642a2-478">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="642a2-479">string</span><span class="sxs-lookup"><span data-stu-id="642a2-479">string</span></span>|<span data-ttu-id="642a2-480">128文字</span><span class="sxs-lookup"><span data-stu-id="642a2-480">128 characters</span></span>||<span data-ttu-id="642a2-481">のタスクモジュールに表示されるコントロールの種類を定義 `fetchTask: true` します。</span><span class="sxs-lookup"><span data-stu-id="642a2-481">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="642a2-482">のいずれか `text, textarea, number, date, time, toggle, choiceset` です。</span><span class="sxs-lookup"><span data-stu-id="642a2-482">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="642a2-483">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="642a2-483">array of objects</span></span>|<span data-ttu-id="642a2-484">10アイテム</span><span class="sxs-lookup"><span data-stu-id="642a2-484">10 items</span></span>||<span data-ttu-id="642a2-485">の選択オプション `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="642a2-485">The choice options for the`choiceset`.</span></span> <span data-ttu-id="642a2-486">がである場合にのみ使用 `parameter.inputType` `choiceset` します。</span><span class="sxs-lookup"><span data-stu-id="642a2-486">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="642a2-487">string</span><span class="sxs-lookup"><span data-stu-id="642a2-487">string</span></span>|<span data-ttu-id="642a2-488">128文字</span><span class="sxs-lookup"><span data-stu-id="642a2-488">128 characters</span></span>|<span data-ttu-id="642a2-489">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-489">✔</span></span>|<span data-ttu-id="642a2-490">選択項目のタイトル。</span><span class="sxs-lookup"><span data-stu-id="642a2-490">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="642a2-491">string</span><span class="sxs-lookup"><span data-stu-id="642a2-491">string</span></span>|<span data-ttu-id="642a2-492">512文字</span><span class="sxs-lookup"><span data-stu-id="642a2-492">512 characters</span></span>|<span data-ttu-id="642a2-493">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-493">✔</span></span>|<span data-ttu-id="642a2-494">Value of the choice.</span><span class="sxs-lookup"><span data-stu-id="642a2-494">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="642a2-495">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="642a2-495">permissions</span></span>

<span data-ttu-id="642a2-496">**省略可能** -文字列の配列</span><span class="sxs-lookup"><span data-stu-id="642a2-496">**Optional** — array of strings</span></span>

<span data-ttu-id="642a2-497">`string`アプリが要求するアクセス許可を指定する配列。これにより、エンドユーザーは拡張機能の動作を知ることができます。</span><span class="sxs-lookup"><span data-stu-id="642a2-497">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="642a2-498">非排他的なオプションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="642a2-498">The following options are non-exclusive:</span></span>

* <span data-ttu-id="642a2-499">`identity`&emsp;ユーザー id 情報が必要</span><span class="sxs-lookup"><span data-stu-id="642a2-499">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="642a2-500">`messageTeamMembers`&emsp;チームメンバーに直接メッセージを送信するためのアクセス許可が必要</span><span class="sxs-lookup"><span data-stu-id="642a2-500">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="642a2-501">アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは、更新されたアプリを初めて実行したときに同意プロセスを繰り返すようになります。</span><span class="sxs-lookup"><span data-stu-id="642a2-501">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="642a2-502">詳細については [、「アプリの更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="642a2-502">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="642a2-503">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="642a2-503">devicePermissions</span></span>

<span data-ttu-id="642a2-504">**省略可能** -文字列の配列</span><span class="sxs-lookup"><span data-stu-id="642a2-504">**Optional** — array of strings</span></span>

<span data-ttu-id="642a2-505">アプリがアクセスを要求することができる、ユーザーのデバイスのネイティブ機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="642a2-505">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="642a2-506">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="642a2-506">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="642a2-507">validDomains</span><span class="sxs-lookup"><span data-stu-id="642a2-507">validDomains</span></span>

<span data-ttu-id="642a2-508">**省略可能**(記載個所に **必要な** 場合を除く)</span><span class="sxs-lookup"><span data-stu-id="642a2-508">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="642a2-509">アプリが Teams クライアント内で読み込むことが想定されている web サイトの有効なドメインの一覧。</span><span class="sxs-lookup"><span data-stu-id="642a2-509">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="642a2-510">ドメインリストには、たとえば、ワイルドカードを含めることができ `*.example.com` ます。</span><span class="sxs-lookup"><span data-stu-id="642a2-510">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="642a2-511">これは、1つのドメインのセグメントに一致します。に一致させる必要がある場合は `a.b.example.com` 、を使用 `*.*.example.com` します。</span><span class="sxs-lookup"><span data-stu-id="642a2-511">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="642a2-512">タブ構成またはコンテンツ UI が他のドメインに移動する必要がある場合 (タブの構成に使用するものを除く)、そのドメインをここで指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-512">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="642a2-513">ただし、アプリでサポートする id プロバイダーのドメインを含める必要は **ありません** 。</span><span class="sxs-lookup"><span data-stu-id="642a2-513">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="642a2-514">たとえば、Google ID を使用して認証するには、accounts.google.com にリダイレクトする必要がありますが、に accounts.google.com を含めることはできません `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="642a2-514">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="642a2-515">自分の sharepoint Url が適切に機能する必要がある Teams アプリは、有効なドメインリストに "{teamsitedomain}" を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="642a2-515">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="642a2-516">直接に、またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しないでください。</span><span class="sxs-lookup"><span data-stu-id="642a2-516">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="642a2-517">たとえば、は有効ですが、有効では `yourapp.onmicrosoft.com` `*.onmicrosoft.com` ありません。</span><span class="sxs-lookup"><span data-stu-id="642a2-517">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="642a2-518">Object は、型のすべての要素を含む配列です `string` 。</span><span class="sxs-lookup"><span data-stu-id="642a2-518">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="642a2-519">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="642a2-519">webApplicationInfo</span></span>

<span data-ttu-id="642a2-520">**Optional** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="642a2-520">**Optional** — object</span></span>

<span data-ttu-id="642a2-521">Aad アプリ ID とグラフ情報を指定して、ユーザーが AAD アプリにシームレスにサインインできるようにします。</span><span class="sxs-lookup"><span data-stu-id="642a2-521">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="642a2-522">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-522">Name</span></span>| <span data-ttu-id="642a2-523">型</span><span class="sxs-lookup"><span data-stu-id="642a2-523">Type</span></span>| <span data-ttu-id="642a2-524">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-524">Maximum size</span></span> | <span data-ttu-id="642a2-525">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-525">Required</span></span> | <span data-ttu-id="642a2-526">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-526">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="642a2-527">string</span><span class="sxs-lookup"><span data-stu-id="642a2-527">string</span></span>|<span data-ttu-id="642a2-528">36文字</span><span class="sxs-lookup"><span data-stu-id="642a2-528">36 characters</span></span>|<span data-ttu-id="642a2-529">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-529">✔</span></span>|<span data-ttu-id="642a2-530">アプリの AAD アプリケーション id。</span><span class="sxs-lookup"><span data-stu-id="642a2-530">AAD application id of the app.</span></span> <span data-ttu-id="642a2-531">この id は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-531">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="642a2-532">string</span><span class="sxs-lookup"><span data-stu-id="642a2-532">string</span></span>|<span data-ttu-id="642a2-533">2048 文字</span><span class="sxs-lookup"><span data-stu-id="642a2-533">2048 characters</span></span>||<span data-ttu-id="642a2-534">SSO の認証トークンを取得するためのアプリのリソース url。</span><span class="sxs-lookup"><span data-stu-id="642a2-534">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="642a2-535">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="642a2-535">array of strings</span></span>|<span data-ttu-id="642a2-536">128文字</span><span class="sxs-lookup"><span data-stu-id="642a2-536">128 characters</span></span>||<span data-ttu-id="642a2-537">[リソース固有の](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)詳細な同意を指定する</span><span class="sxs-lookup"><span data-stu-id="642a2-537">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="642a2-538">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="642a2-538">showLoadingIndicator</span></span>

<span data-ttu-id="642a2-539">**Optional** -boolean</span><span class="sxs-lookup"><span data-stu-id="642a2-539">**Optional** — boolean</span></span>

<span data-ttu-id="642a2-540">アプリ/タブが読み込まれているときに、読み込みインジケーターを表示するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="642a2-540">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="642a2-541">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="642a2-541">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="642a2-542">アプリマニフェストで "showLoadingIndicator: true" を設定した場合、ページが正しく読み込まれるようにするには、「 [ネイティブロードインジケーター](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) ドキュメントを表示する」で説明されているプロトコルに従って、タブおよびタスクモジュールのコンテンツページを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642a2-542">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="642a2-543">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="642a2-543">isFullScreen</span></span>

 <span data-ttu-id="642a2-544">**Optional** -boolean</span><span class="sxs-lookup"><span data-stu-id="642a2-544">**Optional** — boolean</span></span>

<span data-ttu-id="642a2-545">個人用アプリがタブヘッダーバーを使用して、または表示せずにレンダリングされる場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="642a2-545">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="642a2-546">既定値: **false**</span><span class="sxs-lookup"><span data-stu-id="642a2-546">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="642a2-547">アクティビティ</span><span class="sxs-lookup"><span data-stu-id="642a2-547">activities</span></span>

<span data-ttu-id="642a2-548">**Optional** -オブジェクト</span><span class="sxs-lookup"><span data-stu-id="642a2-548">**Optional** — object</span></span>

<span data-ttu-id="642a2-549">アプリがユーザーアクティビティフィードに投稿するときに使用するプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="642a2-549">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="642a2-550">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-550">Name</span></span>| <span data-ttu-id="642a2-551">型</span><span class="sxs-lookup"><span data-stu-id="642a2-551">Type</span></span>| <span data-ttu-id="642a2-552">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-552">Maximum size</span></span> | <span data-ttu-id="642a2-553">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-553">Required</span></span> | <span data-ttu-id="642a2-554">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-554">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="642a2-555">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="642a2-555">array of Objects</span></span>|<span data-ttu-id="642a2-556">128アイテム</span><span class="sxs-lookup"><span data-stu-id="642a2-556">128 items</span></span>| | <span data-ttu-id="642a2-557">アプリがユーザーアクティビティフィードに投稿できるアクティビティの種類を指定します。</span><span class="sxs-lookup"><span data-stu-id="642a2-557">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="642a2-558">アクティビティの種類</span><span class="sxs-lookup"><span data-stu-id="642a2-558">activities.activityTypes</span></span>

|<span data-ttu-id="642a2-559">名前</span><span class="sxs-lookup"><span data-stu-id="642a2-559">Name</span></span>| <span data-ttu-id="642a2-560">型</span><span class="sxs-lookup"><span data-stu-id="642a2-560">Type</span></span>| <span data-ttu-id="642a2-561">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="642a2-561">Maximum size</span></span> | <span data-ttu-id="642a2-562">必須</span><span class="sxs-lookup"><span data-stu-id="642a2-562">Required</span></span> | <span data-ttu-id="642a2-563">説明</span><span class="sxs-lookup"><span data-stu-id="642a2-563">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="642a2-564">string</span><span class="sxs-lookup"><span data-stu-id="642a2-564">string</span></span>|<span data-ttu-id="642a2-565">32文字</span><span class="sxs-lookup"><span data-stu-id="642a2-565">32 characters</span></span>|<span data-ttu-id="642a2-566">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-566">✔</span></span>|<span data-ttu-id="642a2-567">通知の種類。</span><span class="sxs-lookup"><span data-stu-id="642a2-567">The notification type.</span></span> <span data-ttu-id="642a2-568">*以下を参照して*ください。</span><span class="sxs-lookup"><span data-stu-id="642a2-568">*See below*.</span></span>|
|`description`|<span data-ttu-id="642a2-569">string</span><span class="sxs-lookup"><span data-stu-id="642a2-569">string</span></span>|<span data-ttu-id="642a2-570">128文字</span><span class="sxs-lookup"><span data-stu-id="642a2-570">128 characters</span></span>|<span data-ttu-id="642a2-571">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-571">✔</span></span>|<span data-ttu-id="642a2-572">通知の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="642a2-572">A brief description of the notification.</span></span> <span data-ttu-id="642a2-573">*以下を参照して*ください。</span><span class="sxs-lookup"><span data-stu-id="642a2-573">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="642a2-574">string</span><span class="sxs-lookup"><span data-stu-id="642a2-574">string</span></span>|<span data-ttu-id="642a2-575">128文字</span><span class="sxs-lookup"><span data-stu-id="642a2-575">128 characters</span></span>|<span data-ttu-id="642a2-576">✔</span><span class="sxs-lookup"><span data-stu-id="642a2-576">✔</span></span>|<span data-ttu-id="642a2-577">Ex: "{actor} ' のタスク {taskId} が作成されました"</span><span class="sxs-lookup"><span data-stu-id="642a2-577">Ex: "{actor} created task {taskId} for you"</span></span>|

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
