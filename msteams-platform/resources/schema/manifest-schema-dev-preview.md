---
title: 開発者プレビュー マニフェスト スキーマ リファレンス
description: マニフェストでサポートされているMicrosoft Teamsのスキーマについて説明します。
ms.topic: reference
keywords: チーム マニフェスト スキーマ 開発者プレビュー
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: b52d52f96312dc2978844b07a0f7ebb1d817166d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566706"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="8d785-104">Microsoft Teamsの開発者プレビュー マニフェスト スキーマ</span><span class="sxs-lookup"><span data-stu-id="8d785-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="8d785-105">プログラムと参加方法については、「 [開発者プレビュー](~/resources/dev-preview/developer-preview-intro.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d785-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="8d785-106">開発者プレビューを使用していない場合は、このバージョンのマニフェストを使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="8d785-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="8d785-107">[「参照: マニフェストの公開バージョンのMicrosoft Teams](~/resources/schema/manifest-schema.md)のマニフェスト スキーマ」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d785-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="8d785-108">Microsoft Teams マニフェストは、アプリがMicrosoft Teams製品にどのように統合するかを示します。</span><span class="sxs-lookup"><span data-stu-id="8d785-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="8d785-109">マニフェストは、 でホストされているスキーマに準拠している必要があります [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="8d785-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="8d785-110">利用可能な機能の詳細については[、「Microsoft Teamsのパブリック開発者向けプレビューの機能](~/resources/dev-preview/developer-preview-features.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d785-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="8d785-111">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="8d785-111">Sample full manifest</span></span>

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "devPreview",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "devicePermissions" : [ "geolocation", "media" ],
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "localizationInfo": {
    "defaultLanguageTag": "es-es",
    "additionalLanguages": [
      {
        "languageTag": "en-us",
        "file": "en-us.json"
      }
    ]
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters"
  },
  "description": {
    "short": "Short description of your app",
    "full": "Full description of your app"
  },
  "icons": {
    "outline": "%FILENAME-32x32px%",
    "color": "%FILENAME-192x192px"
  },
  "accentColor": "%HEX-COLOR%",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content?host=msteams",
      "websiteUrl": "https://contoso.com/content",
      "scopes": [ "personal" ]
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
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
      "configurationUrl": "https://contoso.com/teamsconnector/configure",
      "scopes": [ "team"]
    }
  ],
  "composeExtensions": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "type" : "search",
          "context" : ["compose", "commandBox"],
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "description": "Enter the keywords to search for"
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "type" : "action",
          "fetchTask" : true,
          "context" : ["message"],
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType" : "text"
            }
          ]
        },
        {
          "id": "exampleMessageHandler",
          "title": "Message Handler",
          "description": "Domains that will create a preview when pasted into the compose box",
          "messageHandlers": [
            {
              "type" : "link",
              "value" : {
                "domains" : [
                  "mysite.someplace.com",
                  "othersite.someplace.com"
                ]
              }
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers",
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ],
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
  ],
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  }
}
```

<span data-ttu-id="8d785-112">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="8d785-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="8d785-113">$schema</span><span class="sxs-lookup"><span data-stu-id="8d785-113">$schema</span></span>

<span data-ttu-id="8d785-114">*オプションですが、推奨* &ndash; 糸</span><span class="sxs-lookup"><span data-stu-id="8d785-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="8d785-115">マニフェストの JSON スキーマを参照する https:// URL。</span><span class="sxs-lookup"><span data-stu-id="8d785-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="8d785-116">マニフェストバージョン</span><span class="sxs-lookup"><span data-stu-id="8d785-116">manifestVersion</span></span>

<span data-ttu-id="8d785-117">**必須** &ndash; 糸</span><span class="sxs-lookup"><span data-stu-id="8d785-117">**Required** &ndash; String</span></span>

<span data-ttu-id="8d785-118">このマニフェストが使用しているマニフェスト スキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="8d785-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="8d785-119">"devPreview" にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="8d785-120">version</span><span class="sxs-lookup"><span data-stu-id="8d785-120">version</span></span>

<span data-ttu-id="8d785-121">**必須** &ndash; 糸</span><span class="sxs-lookup"><span data-stu-id="8d785-121">**Required** &ndash; String</span></span>

<span data-ttu-id="8d785-122">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="8d785-122">The version of the specific app.</span></span> <span data-ttu-id="8d785-123">マニフェスト内の何かを更新する場合は、バージョンもインクリメントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="8d785-124">このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。</span><span class="sxs-lookup"><span data-stu-id="8d785-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="8d785-125">このアプリがストアに提出された場合、新しいマニフェストを再提出し、再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="8d785-126">その後、このアプリのユーザーは、それが承認された後、数時間で自動的に新しい更新されたマニフェストを取得します。</span><span class="sxs-lookup"><span data-stu-id="8d785-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="8d785-127">アプリがアクセス許可を要求した場合、ユーザーはアップグレードを要求され、アプリに再び同意するように求められます。</span><span class="sxs-lookup"><span data-stu-id="8d785-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="8d785-128">このバージョンの文字列は [、semver](http://semver.org/) 標準 (MAJOR.マイナー。パッチ)。</span><span class="sxs-lookup"><span data-stu-id="8d785-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="8d785-129">id</span><span class="sxs-lookup"><span data-stu-id="8d785-129">id</span></span>

<span data-ttu-id="8d785-130">**必須** &ndash; マイクロソフト アプリ ID</span><span class="sxs-lookup"><span data-stu-id="8d785-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="8d785-131">このアプリのマイクロソフトが生成した一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="8d785-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="8d785-132">Microsoft Bot Frameworkを介してボットを登録した場合、またはタブの Web アプリが既に Microsoft にサインインしている場合は、ID が既に用意されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="8d785-133">それ以外の場合は、 Microsoft アプリケーション登録ポータル ([マイ アプリケーション](https://apps.dev.microsoft.com)) で新しい ID を生成し、ここに入力し、 [ボットを追加](~/bots/how-to/create-a-bot-for-teams.md)するときに再利用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="8d785-134">パッケージ名</span><span class="sxs-lookup"><span data-stu-id="8d785-134">packageName</span></span>

<span data-ttu-id="8d785-135">**必須** &ndash; 糸</span><span class="sxs-lookup"><span data-stu-id="8d785-135">**Required** &ndash; String</span></span>

<span data-ttu-id="8d785-136">逆ドメイン表記で、このアプリの一意の識別子。たとえば、com.example.myapp を使用します。</span><span class="sxs-lookup"><span data-stu-id="8d785-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="8d785-137">developer</span><span class="sxs-lookup"><span data-stu-id="8d785-137">developer</span></span>

<span data-ttu-id="8d785-138">**必須**</span><span class="sxs-lookup"><span data-stu-id="8d785-138">**Required**</span></span>

<span data-ttu-id="8d785-139">会社に関する情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="8d785-139">Specifies information about your company.</span></span> <span data-ttu-id="8d785-140">AppSource (以前のOfficeストア) に送信されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="8d785-141">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-141">Name</span></span>| <span data-ttu-id="8d785-142">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-142">Maximum size</span></span> | <span data-ttu-id="8d785-143">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-143">Required</span></span> | <span data-ttu-id="8d785-144">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="8d785-145">32 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-145">32 characters</span></span>|<span data-ttu-id="8d785-146">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-146">✔</span></span>|<span data-ttu-id="8d785-147">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="8d785-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="8d785-148">2048 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-148">2048 characters</span></span>|<span data-ttu-id="8d785-149">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-149">✔</span></span>|<span data-ttu-id="8d785-150">開発者の web サイトへの https:// URL。</span><span class="sxs-lookup"><span data-stu-id="8d785-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="8d785-151">このリンクをクリックすると、ユーザーは会社または製品固有のランディング ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="8d785-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="8d785-152">2048 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-152">2048 characters</span></span>|<span data-ttu-id="8d785-153">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-153">✔</span></span>|<span data-ttu-id="8d785-154">開発者のプライバシー ポリシーの https:// URL。</span><span class="sxs-lookup"><span data-stu-id="8d785-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="8d785-155">2048 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-155">2048 characters</span></span>|<span data-ttu-id="8d785-156">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-156">✔</span></span>|<span data-ttu-id="8d785-157">開発者の使用条件の https:// URL。</span><span class="sxs-lookup"><span data-stu-id="8d785-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="8d785-158">10 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-158">10 characters</span></span>|<span data-ttu-id="8d785-159">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-159">✔</span></span>|<span data-ttu-id="8d785-160">**オプション** アプリを構築するパートナー組織を識別するマイクロソフト パートナー ネットワーク ID。</span><span class="sxs-lookup"><span data-stu-id="8d785-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="8d785-161">ローカリゼーション情報</span><span class="sxs-lookup"><span data-stu-id="8d785-161">localizationInfo</span></span>

<span data-ttu-id="8d785-162">**Optional**</span><span class="sxs-lookup"><span data-stu-id="8d785-162">**Optional**</span></span>

<span data-ttu-id="8d785-163">既定の言語の指定と、追加の言語ファイルへのポインタを許可します。</span><span class="sxs-lookup"><span data-stu-id="8d785-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="8d785-164">[ローカライズ](~/concepts/build-and-test/apps-localization.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d785-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="8d785-165">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-165">Name</span></span>| <span data-ttu-id="8d785-166">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-166">Maximum size</span></span> | <span data-ttu-id="8d785-167">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-167">Required</span></span> | <span data-ttu-id="8d785-168">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="8d785-169">4 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-169">4 characters</span></span>|<span data-ttu-id="8d785-170">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-170">✔</span></span>|<span data-ttu-id="8d785-171">この最上位のマニフェスト ファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="8d785-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="8d785-172">ローカリゼーション情報.追加言語</span><span class="sxs-lookup"><span data-stu-id="8d785-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="8d785-173">追加の言語翻訳を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="8d785-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="8d785-174">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-174">Name</span></span>| <span data-ttu-id="8d785-175">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-175">Maximum size</span></span> | <span data-ttu-id="8d785-176">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-176">Required</span></span> | <span data-ttu-id="8d785-177">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="8d785-178">4 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-178">4 characters</span></span>|<span data-ttu-id="8d785-179">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-179">✔</span></span>|<span data-ttu-id="8d785-180">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="8d785-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="8d785-181">4 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-181">4 characters</span></span>|<span data-ttu-id="8d785-182">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-182">✔</span></span>|<span data-ttu-id="8d785-183">翻訳された文字列を含む .json ファイルへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="8d785-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="8d785-184">name</span><span class="sxs-lookup"><span data-stu-id="8d785-184">name</span></span>

<span data-ttu-id="8d785-185">**必須**</span><span class="sxs-lookup"><span data-stu-id="8d785-185">**Required**</span></span>

<span data-ttu-id="8d785-186">Teams エクスペリエンスのユーザーに表示される、アプリ エクスペリエンスの名前。</span><span class="sxs-lookup"><span data-stu-id="8d785-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="8d785-187">AppSource に送信されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="8d785-188">の値 `short` は同 `full` じであってはなりません。</span><span class="sxs-lookup"><span data-stu-id="8d785-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="8d785-189">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-189">Name</span></span>| <span data-ttu-id="8d785-190">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-190">Maximum size</span></span> | <span data-ttu-id="8d785-191">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-191">Required</span></span> | <span data-ttu-id="8d785-192">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="8d785-193">30 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-193">30 characters</span></span>|<span data-ttu-id="8d785-194">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-194">✔</span></span>|<span data-ttu-id="8d785-195">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="8d785-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="8d785-196">100 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-196">100 characters</span></span>||<span data-ttu-id="8d785-197">アプリの完全名は、アプリの完全名が 30 文字を超える場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="8d785-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="8d785-198">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-198">description</span></span>

<span data-ttu-id="8d785-199">**必須**</span><span class="sxs-lookup"><span data-stu-id="8d785-199">**Required**</span></span>

<span data-ttu-id="8d785-200">ユーザーにアプリを記述します。</span><span class="sxs-lookup"><span data-stu-id="8d785-200">Describes your app to users.</span></span> <span data-ttu-id="8d785-201">AppSource に送信されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="8d785-202">説明が自分のエクスペリエンスを正確に説明し、潜在顧客がエクスペリエンスの内容を理解するのに役立つ情報を提供するようにします。</span><span class="sxs-lookup"><span data-stu-id="8d785-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="8d785-203">また、外部アカウントが使用する必要がある場合は、完全な説明に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="8d785-204">の値 `short` は同 `full` じであってはなりません。</span><span class="sxs-lookup"><span data-stu-id="8d785-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="8d785-205">短い説明は、長い説明の中で繰り返してはならず、他のアプリ名を含めてはいけません。</span><span class="sxs-lookup"><span data-stu-id="8d785-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="8d785-206">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-206">Name</span></span>| <span data-ttu-id="8d785-207">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-207">Maximum size</span></span> | <span data-ttu-id="8d785-208">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-208">Required</span></span> | <span data-ttu-id="8d785-209">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="8d785-210">80 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-210">80 characters</span></span>|<span data-ttu-id="8d785-211">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-211">✔</span></span>|<span data-ttu-id="8d785-212">スペースが限られている場合に使用するアプリ エクスペリエンスの簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="8d785-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="8d785-213">4000 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-213">4000 characters</span></span>|<span data-ttu-id="8d785-214">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-214">✔</span></span>|<span data-ttu-id="8d785-215">アプリの完全な説明。</span><span class="sxs-lookup"><span data-stu-id="8d785-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="8d785-216">アイコン</span><span class="sxs-lookup"><span data-stu-id="8d785-216">icons</span></span>

<span data-ttu-id="8d785-217">**必須**</span><span class="sxs-lookup"><span data-stu-id="8d785-217">**Required**</span></span>

<span data-ttu-id="8d785-218">Teams アプリ内で使用されるアイコン。</span><span class="sxs-lookup"><span data-stu-id="8d785-218">Icons used within the Teams app.</span></span> <span data-ttu-id="8d785-219">アイコン ファイルは、アップロード パッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="8d785-220">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-220">Name</span></span>| <span data-ttu-id="8d785-221">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-221">Maximum size</span></span> | <span data-ttu-id="8d785-222">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-222">Required</span></span> | <span data-ttu-id="8d785-223">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="8d785-224">2048 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-224">2048 characters</span></span>|<span data-ttu-id="8d785-225">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-225">✔</span></span>|<span data-ttu-id="8d785-226">透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="8d785-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="8d785-227">2048 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-227">2048 characters</span></span>|<span data-ttu-id="8d785-228">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-228">✔</span></span>|<span data-ttu-id="8d785-229">フルカラーの 192x192 PNG アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="8d785-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="8d785-230">アクセントカラー</span><span class="sxs-lookup"><span data-stu-id="8d785-230">accentColor</span></span>

<span data-ttu-id="8d785-231">**必須** &ndash; 糸</span><span class="sxs-lookup"><span data-stu-id="8d785-231">**Required** &ndash; String</span></span>

<span data-ttu-id="8d785-232">アウトライン アイコンと共に、および背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="8d785-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="8d785-233">値は、たとえば '#' で始まる有効な HTML カラー コードである必要があります `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="8d785-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="8d785-234">構成可能なタブ</span><span class="sxs-lookup"><span data-stu-id="8d785-234">configurableTabs</span></span>

<span data-ttu-id="8d785-235">**Optional**</span><span class="sxs-lookup"><span data-stu-id="8d785-235">**Optional**</span></span>

<span data-ttu-id="8d785-236">アプリエクスペリエンスにチーム チャネル タブ エクスペリエンスがあり、追加前に追加の構成が必要な場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="8d785-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="8d785-237">構成可能なタブはチームスコープでのみサポートされ、現在はアプリごとに 1 つのタブのみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="8d785-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="8d785-238">オブジェクトは、 type のすべての要素を持つ配列です `object` 。</span><span class="sxs-lookup"><span data-stu-id="8d785-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="8d785-239">このブロックは、構成可能なチャネル タブ ソリューションを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="8d785-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="8d785-240">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-240">Name</span></span>| <span data-ttu-id="8d785-241">型</span><span class="sxs-lookup"><span data-stu-id="8d785-241">Type</span></span>| <span data-ttu-id="8d785-242">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-242">Maximum size</span></span> | <span data-ttu-id="8d785-243">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-243">Required</span></span> | <span data-ttu-id="8d785-244">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="8d785-245">String</span><span class="sxs-lookup"><span data-stu-id="8d785-245">String</span></span>|<span data-ttu-id="8d785-246">2048 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-246">2048 characters</span></span>|<span data-ttu-id="8d785-247">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-247">✔</span></span>|<span data-ttu-id="8d785-248">タブの構成時に使用する https:// URL。</span><span class="sxs-lookup"><span data-stu-id="8d785-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="8d785-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="8d785-249">Boolean</span></span>|||<span data-ttu-id="8d785-250">タブの構成のインスタンスを作成後にユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="8d785-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="8d785-251">デフォルト： `true`</span><span class="sxs-lookup"><span data-stu-id="8d785-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="8d785-252">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="8d785-252">Array of enum</span></span>|<span data-ttu-id="8d785-253">1</span><span class="sxs-lookup"><span data-stu-id="8d785-253">1</span></span>|<span data-ttu-id="8d785-254">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-254">✔</span></span>|<span data-ttu-id="8d785-255">現在、構成可能なタブは `team` 、 および スコープのみをサポート `groupchat` します。</span><span class="sxs-lookup"><span data-stu-id="8d785-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="8d785-256">String</span><span class="sxs-lookup"><span data-stu-id="8d785-256">String</span></span>|<span data-ttu-id="8d785-257">2048</span><span class="sxs-lookup"><span data-stu-id="8d785-257">2048</span></span>||<span data-ttu-id="8d785-258">SharePointで使用するタブ プレビュー イメージへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="8d785-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="8d785-259">サイズ 1024x768。</span><span class="sxs-lookup"><span data-stu-id="8d785-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="8d785-260">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="8d785-260">Array of enum</span></span>|<span data-ttu-id="8d785-261">1</span><span class="sxs-lookup"><span data-stu-id="8d785-261">1</span></span>||<span data-ttu-id="8d785-262">SharePointでタブを使用できるようにする方法を定義します。</span><span class="sxs-lookup"><span data-stu-id="8d785-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="8d785-263">オプションは `sharePointFullPage` 、 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="8d785-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="8d785-264">静的タブ</span><span class="sxs-lookup"><span data-stu-id="8d785-264">staticTabs</span></span>

<span data-ttu-id="8d785-265">**Optional**</span><span class="sxs-lookup"><span data-stu-id="8d785-265">**Optional**</span></span>

<span data-ttu-id="8d785-266">ユーザーが手動で追加しなくても、既定で "固定" できるタブのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="8d785-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="8d785-267">スコープで宣言された静的タブ `personal` は、常にアプリの個人的なエクスペリエンスに固定されます。</span><span class="sxs-lookup"><span data-stu-id="8d785-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="8d785-268">スコープで宣言された静的タブ `team` は、現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="8d785-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="8d785-269">オブジェクトは、型のすべての要素を持つ配列 (最大 16 個の要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="8d785-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="8d785-270">このブロックは、静的タブ ソリューションを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="8d785-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="8d785-271">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-271">Name</span></span>| <span data-ttu-id="8d785-272">型</span><span class="sxs-lookup"><span data-stu-id="8d785-272">Type</span></span>| <span data-ttu-id="8d785-273">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-273">Maximum size</span></span> | <span data-ttu-id="8d785-274">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-274">Required</span></span> | <span data-ttu-id="8d785-275">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="8d785-276">String</span><span class="sxs-lookup"><span data-stu-id="8d785-276">String</span></span>|<span data-ttu-id="8d785-277">64 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-277">64 characters</span></span>|<span data-ttu-id="8d785-278">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-278">✔</span></span>|<span data-ttu-id="8d785-279">タブが表示するエンティティの一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="8d785-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="8d785-280">String</span><span class="sxs-lookup"><span data-stu-id="8d785-280">String</span></span>|<span data-ttu-id="8d785-281">128 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-281">128 characters</span></span>|<span data-ttu-id="8d785-282">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-282">✔</span></span>|<span data-ttu-id="8d785-283">チャネル インターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="8d785-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="8d785-284">String</span><span class="sxs-lookup"><span data-stu-id="8d785-284">String</span></span>|<span data-ttu-id="8d785-285">2048 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-285">2048 characters</span></span>|<span data-ttu-id="8d785-286">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-286">✔</span></span>|<span data-ttu-id="8d785-287">Teams キャンバスに表示されるエンティティ UI を指す https:// URL。</span><span class="sxs-lookup"><span data-stu-id="8d785-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="8d785-288">String</span><span class="sxs-lookup"><span data-stu-id="8d785-288">String</span></span>|<span data-ttu-id="8d785-289">2048 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-289">2048 characters</span></span>||<span data-ttu-id="8d785-290">ユーザーがブラウザーで表示することを選択した場合に指す https:// URL。</span><span class="sxs-lookup"><span data-stu-id="8d785-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="8d785-291">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="8d785-291">Array of enum</span></span>|<span data-ttu-id="8d785-292">1</span><span class="sxs-lookup"><span data-stu-id="8d785-292">1</span></span>|<span data-ttu-id="8d785-293">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-293">✔</span></span>|<span data-ttu-id="8d785-294">現在、静的タブはスコープのみをサポート `personal` するため、個人用エクスペリエンスの一部としてのみプロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="8d785-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="8d785-295">ボット</span><span class="sxs-lookup"><span data-stu-id="8d785-295">bots</span></span>

<span data-ttu-id="8d785-296">**Optional**</span><span class="sxs-lookup"><span data-stu-id="8d785-296">**Optional**</span></span>

<span data-ttu-id="8d785-297">ボット ソリューションを、既定のコマンド プロパティなどのオプション情報と共に定義します。</span><span class="sxs-lookup"><span data-stu-id="8d785-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="8d785-298">オブジェクトは配列です (最大 1 つの要素のみ &mdash; 、現在、1 つのアプリに 1 つのボットしか許可されていません) 型のすべての要素を持つ `object` .</span><span class="sxs-lookup"><span data-stu-id="8d785-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="8d785-299">このブロックは、ボット エクスペリエンスを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="8d785-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="8d785-300">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-300">Name</span></span>| <span data-ttu-id="8d785-301">型</span><span class="sxs-lookup"><span data-stu-id="8d785-301">Type</span></span>| <span data-ttu-id="8d785-302">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-302">Maximum size</span></span> | <span data-ttu-id="8d785-303">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-303">Required</span></span> | <span data-ttu-id="8d785-304">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="8d785-305">String</span><span class="sxs-lookup"><span data-stu-id="8d785-305">String</span></span>|<span data-ttu-id="8d785-306">64 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-306">64 characters</span></span>|<span data-ttu-id="8d785-307">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-307">✔</span></span>|<span data-ttu-id="8d785-308">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="8d785-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="8d785-309">これは、 [全体的なアプリ ID](#id)と同じである可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="8d785-310">Boolean</span><span class="sxs-lookup"><span data-stu-id="8d785-310">Boolean</span></span>|||<span data-ttu-id="8d785-311">ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。</span><span class="sxs-lookup"><span data-stu-id="8d785-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="8d785-312">デフォルト： `false`</span><span class="sxs-lookup"><span data-stu-id="8d785-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="8d785-313">Boolean</span><span class="sxs-lookup"><span data-stu-id="8d785-313">Boolean</span></span>|||<span data-ttu-id="8d785-314">ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="8d785-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="8d785-315">デフォルト： `false`</span><span class="sxs-lookup"><span data-stu-id="8d785-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="8d785-316">Boolean</span><span class="sxs-lookup"><span data-stu-id="8d785-316">Boolean</span></span>|||<span data-ttu-id="8d785-317">パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="8d785-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="8d785-318">デフォルト： `false`</span><span class="sxs-lookup"><span data-stu-id="8d785-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="8d785-319">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="8d785-319">Array of enum</span></span>|<span data-ttu-id="8d785-320">3</span><span class="sxs-lookup"><span data-stu-id="8d785-320">3</span></span>|<span data-ttu-id="8d785-321">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-321">✔</span></span>|<span data-ttu-id="8d785-322">ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。</span><span class="sxs-lookup"><span data-stu-id="8d785-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="8d785-323">これらのオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="8d785-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="8d785-324">コマンドリスト</span><span class="sxs-lookup"><span data-stu-id="8d785-324">bots.commandLists</span></span>

<span data-ttu-id="8d785-325">ボットがユーザーに推奨できるコマンドのリスト(オプション)。</span><span class="sxs-lookup"><span data-stu-id="8d785-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="8d785-326">オブジェクトは、型のすべての要素を持つ配列 (最大 2 つの要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="8d785-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="8d785-327">詳細については [、「Bot メニュー](~/bots/how-to/create-a-bot-commands-menu.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d785-327">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="8d785-328">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-328">Name</span></span>| <span data-ttu-id="8d785-329">型</span><span class="sxs-lookup"><span data-stu-id="8d785-329">Type</span></span>| <span data-ttu-id="8d785-330">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-330">Maximum size</span></span> | <span data-ttu-id="8d785-331">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-331">Required</span></span> | <span data-ttu-id="8d785-332">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="8d785-333">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="8d785-333">array of enum</span></span>|<span data-ttu-id="8d785-334">3</span><span class="sxs-lookup"><span data-stu-id="8d785-334">3</span></span>|<span data-ttu-id="8d785-335">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-335">✔</span></span>|<span data-ttu-id="8d785-336">コマンド リストが有効なスコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="8d785-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="8d785-337">`team`、`personal`、`groupchat` の中から選択できます。</span><span class="sxs-lookup"><span data-stu-id="8d785-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="8d785-338">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="8d785-338">array of objects</span></span>|<span data-ttu-id="8d785-339">10</span><span class="sxs-lookup"><span data-stu-id="8d785-339">10</span></span>|<span data-ttu-id="8d785-340">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-340">✔</span></span>|<span data-ttu-id="8d785-341">ボットがサポートするコマンドの配列:</span><span class="sxs-lookup"><span data-stu-id="8d785-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="8d785-342">`title`: ボットコマンド名(文字列、32)。</span><span class="sxs-lookup"><span data-stu-id="8d785-342">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="8d785-343">`description`: コマンド構文とその引数の簡単な説明または例 (文字列、128)。</span><span class="sxs-lookup"><span data-stu-id="8d785-343">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="8d785-344">コネクタ</span><span class="sxs-lookup"><span data-stu-id="8d785-344">connectors</span></span>

<span data-ttu-id="8d785-345">**Optional**</span><span class="sxs-lookup"><span data-stu-id="8d785-345">**Optional**</span></span>

<span data-ttu-id="8d785-346">`connectors`ブロックは、アプリのOffice 365コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="8d785-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="8d785-347">オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) `object` です。</span><span class="sxs-lookup"><span data-stu-id="8d785-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="8d785-348">このブロックは、コネクタを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="8d785-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="8d785-349">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-349">Name</span></span>| <span data-ttu-id="8d785-350">型</span><span class="sxs-lookup"><span data-stu-id="8d785-350">Type</span></span>| <span data-ttu-id="8d785-351">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-351">Maximum size</span></span> | <span data-ttu-id="8d785-352">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-352">Required</span></span> | <span data-ttu-id="8d785-353">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="8d785-354">String</span><span class="sxs-lookup"><span data-stu-id="8d785-354">String</span></span>|<span data-ttu-id="8d785-355">2048 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-355">2048 characters</span></span>|<span data-ttu-id="8d785-356">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-356">✔</span></span>|<span data-ttu-id="8d785-357">コネクタの構成時に使用する https:// URL。</span><span class="sxs-lookup"><span data-stu-id="8d785-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="8d785-358">String</span><span class="sxs-lookup"><span data-stu-id="8d785-358">String</span></span>|<span data-ttu-id="8d785-359">64 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-359">64 characters</span></span>|<span data-ttu-id="8d785-360">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-360">✔</span></span>|<span data-ttu-id="8d785-361">コネクタ開発者ダッシュボード の ID と一致する [コネクタの](https://aka.ms/connectorsdashboard)一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="8d785-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="8d785-362">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="8d785-362">Array of enum</span></span>|<span data-ttu-id="8d785-363">1</span><span class="sxs-lookup"><span data-stu-id="8d785-363">1</span></span>|<span data-ttu-id="8d785-364">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-364">✔</span></span>|<span data-ttu-id="8d785-365">コネクタが、 のチャネルのコンテキストでのエクスペリエンスを提供 `team` するか、個々のユーザーに限定されたエクスペリエンス ( ) を提供するかを指定 `personal` します。</span><span class="sxs-lookup"><span data-stu-id="8d785-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="8d785-366">現在、スコープのみが `team` サポートされています。</span><span class="sxs-lookup"><span data-stu-id="8d785-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="8d785-367">コン成拡張</span><span class="sxs-lookup"><span data-stu-id="8d785-367">composeExtensions</span></span>

<span data-ttu-id="8d785-368">**Optional**</span><span class="sxs-lookup"><span data-stu-id="8d785-368">**Optional**</span></span>

<span data-ttu-id="8d785-369">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="8d785-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="8d785-370">機能の名前は、2017 年 11 月に "拡張の構成" から "メッセージング拡張機能" に変更されましたが、マニフェスト名はそのまま残り、既存の拡張機能が機能し続けます。</span><span class="sxs-lookup"><span data-stu-id="8d785-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="8d785-371">オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) `object` です。</span><span class="sxs-lookup"><span data-stu-id="8d785-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="8d785-372">このブロックは、メッセージング拡張機能を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="8d785-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="8d785-373">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-373">Name</span></span>| <span data-ttu-id="8d785-374">型</span><span class="sxs-lookup"><span data-stu-id="8d785-374">Type</span></span> | <span data-ttu-id="8d785-375">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-375">Maximum Size</span></span> | <span data-ttu-id="8d785-376">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-376">Required</span></span> | <span data-ttu-id="8d785-377">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="8d785-378">String</span><span class="sxs-lookup"><span data-stu-id="8d785-378">String</span></span>|<span data-ttu-id="8d785-379">64</span><span class="sxs-lookup"><span data-stu-id="8d785-379">64</span></span>|<span data-ttu-id="8d785-380">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-380">✔</span></span>|<span data-ttu-id="8d785-381">Bot Framework に登録されているメッセージング拡張機能をサポートするボットの一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="8d785-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="8d785-382">これは、 [全体的なアプリ ID](#id)と同じである可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="8d785-383">Boolean</span><span class="sxs-lookup"><span data-stu-id="8d785-383">Boolean</span></span>|||<span data-ttu-id="8d785-384">メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="8d785-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="8d785-385">既定値は `false` です。</span><span class="sxs-lookup"><span data-stu-id="8d785-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="8d785-386">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="8d785-386">Array of object</span></span>|<span data-ttu-id="8d785-387">10</span><span class="sxs-lookup"><span data-stu-id="8d785-387">10</span></span>|<span data-ttu-id="8d785-388">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-388">✔</span></span>|<span data-ttu-id="8d785-389">メッセージング拡張機能がサポートするコマンドの配列</span><span class="sxs-lookup"><span data-stu-id="8d785-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="8d785-390">コンスタブスエクステンション.コマンド</span><span class="sxs-lookup"><span data-stu-id="8d785-390">composeExtensions.commands</span></span>

<span data-ttu-id="8d785-391">メッセージング拡張機能では、1 つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="8d785-392">各コマンドは、UI ベースのエントリ ポイントからの潜在的な操作としてMicrosoft Teamsに表示されます。</span><span class="sxs-lookup"><span data-stu-id="8d785-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="8d785-393">最大 10 個のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="8d785-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="8d785-394">各コマンド項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="8d785-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="8d785-395">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-395">Name</span></span>| <span data-ttu-id="8d785-396">型</span><span class="sxs-lookup"><span data-stu-id="8d785-396">Type</span></span>| <span data-ttu-id="8d785-397">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-397">Maximum size</span></span> | <span data-ttu-id="8d785-398">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-398">Required</span></span> | <span data-ttu-id="8d785-399">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="8d785-400">String</span><span class="sxs-lookup"><span data-stu-id="8d785-400">String</span></span>|<span data-ttu-id="8d785-401">64 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-401">64 characters</span></span>|<span data-ttu-id="8d785-402">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-402">✔</span></span>|<span data-ttu-id="8d785-403">コマンドの ID。</span><span class="sxs-lookup"><span data-stu-id="8d785-403">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="8d785-404">String</span><span class="sxs-lookup"><span data-stu-id="8d785-404">String</span></span>|<span data-ttu-id="8d785-405">64 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-405">64 characters</span></span>||<span data-ttu-id="8d785-406">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="8d785-406">Type of the command.</span></span> <span data-ttu-id="8d785-407">または の 1 つ `query` `action`</span><span class="sxs-lookup"><span data-stu-id="8d785-407">One of `query` or `action`.</span></span> <span data-ttu-id="8d785-408">デフォルト： `query`</span><span class="sxs-lookup"><span data-stu-id="8d785-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="8d785-409">String</span><span class="sxs-lookup"><span data-stu-id="8d785-409">String</span></span>|<span data-ttu-id="8d785-410">32 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-410">32 characters</span></span>|<span data-ttu-id="8d785-411">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-411">✔</span></span>|<span data-ttu-id="8d785-412">わかりやすいコマンド名。</span><span class="sxs-lookup"><span data-stu-id="8d785-412">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="8d785-413">String</span><span class="sxs-lookup"><span data-stu-id="8d785-413">String</span></span>|<span data-ttu-id="8d785-414">128 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-414">128 characters</span></span>||<span data-ttu-id="8d785-415">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="8d785-415">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="8d785-416">Boolean</span><span class="sxs-lookup"><span data-stu-id="8d785-416">Boolean</span></span>|||<span data-ttu-id="8d785-417">コマンドをパラメーターなしで最初に実行するかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="8d785-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="8d785-418">デフォルト： `false`</span><span class="sxs-lookup"><span data-stu-id="8d785-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="8d785-419">文字列 (String) の配列</span><span class="sxs-lookup"><span data-stu-id="8d785-419">Array of Strings</span></span>|<span data-ttu-id="8d785-420">3</span><span class="sxs-lookup"><span data-stu-id="8d785-420">3</span></span>||<span data-ttu-id="8d785-421">メッセージ拡張を呼び出すことができる場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="8d785-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="8d785-422">、 、、を任意に組み合わせて `compose` `commandBox` `message` 使用できます。</span><span class="sxs-lookup"><span data-stu-id="8d785-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="8d785-423">既定値は `["compose", "commandBox"]` です</span><span class="sxs-lookup"><span data-stu-id="8d785-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="8d785-424">Boolean</span><span class="sxs-lookup"><span data-stu-id="8d785-424">Boolean</span></span>|||<span data-ttu-id="8d785-425">タスク モジュールを動的にフェッチするかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="8d785-425">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="8d785-426">オブジェクト</span><span class="sxs-lookup"><span data-stu-id="8d785-426">Object</span></span>|||<span data-ttu-id="8d785-427">メッセージング拡張コマンドを使用する場合にプリロードするタスクモジュールを指定します。</span><span class="sxs-lookup"><span data-stu-id="8d785-427">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="8d785-428">String</span><span class="sxs-lookup"><span data-stu-id="8d785-428">String</span></span>|<span data-ttu-id="8d785-429">64</span><span class="sxs-lookup"><span data-stu-id="8d785-429">64</span></span>||<span data-ttu-id="8d785-430">初期ダイアログ タイトル。</span><span class="sxs-lookup"><span data-stu-id="8d785-430">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="8d785-431">String</span><span class="sxs-lookup"><span data-stu-id="8d785-431">String</span></span>|||<span data-ttu-id="8d785-432">ダイアログ幅 - ピクセル単位の数値またはデフォルトのレイアウト ("大きい"、"中""、"小" など)</span><span class="sxs-lookup"><span data-stu-id="8d785-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="8d785-433">String</span><span class="sxs-lookup"><span data-stu-id="8d785-433">String</span></span>|||<span data-ttu-id="8d785-434">ダイアログの高さ - ピクセル単位の数値または既定のレイアウト ("大きい"、"中""、"小" など)</span><span class="sxs-lookup"><span data-stu-id="8d785-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="8d785-435">String</span><span class="sxs-lookup"><span data-stu-id="8d785-435">String</span></span>|||<span data-ttu-id="8d785-436">初期の Web ビュー URL。</span><span class="sxs-lookup"><span data-stu-id="8d785-436">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="8d785-437">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="8d785-437">Array of Objects</span></span>|<span data-ttu-id="8d785-438">5</span><span class="sxs-lookup"><span data-stu-id="8d785-438">5</span></span>||<span data-ttu-id="8d785-439">特定の条件が満たされた場合にアプリを呼び出すことを許可するハンドラーのリスト。</span><span class="sxs-lookup"><span data-stu-id="8d785-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="8d785-440">ドメインも に表示する必要があります `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="8d785-440">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="8d785-441">String</span><span class="sxs-lookup"><span data-stu-id="8d785-441">String</span></span>|||<span data-ttu-id="8d785-442">メッセージ ハンドラーの種類。</span><span class="sxs-lookup"><span data-stu-id="8d785-442">The type of message handler.</span></span> <span data-ttu-id="8d785-443">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="8d785-444">文字列 (String) の配列</span><span class="sxs-lookup"><span data-stu-id="8d785-444">Array of Strings</span></span>|||<span data-ttu-id="8d785-445">リンク メッセージ ハンドラーが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="8d785-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="8d785-446">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="8d785-446">Array of object</span></span>|<span data-ttu-id="8d785-447">5</span><span class="sxs-lookup"><span data-stu-id="8d785-447">5</span></span>|<span data-ttu-id="8d785-448">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-448">✔</span></span>|<span data-ttu-id="8d785-449">コマンドが受け取るパラメーターのリスト。</span><span class="sxs-lookup"><span data-stu-id="8d785-449">The list of parameters the command takes.</span></span> <span data-ttu-id="8d785-450">最小: 1;最大: 5</span><span class="sxs-lookup"><span data-stu-id="8d785-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="8d785-451">String</span><span class="sxs-lookup"><span data-stu-id="8d785-451">String</span></span>|<span data-ttu-id="8d785-452">64 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-452">64 characters</span></span>|<span data-ttu-id="8d785-453">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-453">✔</span></span>|<span data-ttu-id="8d785-454">クライアントに表示されるパラメータの名前。</span><span class="sxs-lookup"><span data-stu-id="8d785-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="8d785-455">これはユーザー要求に含まれます。</span><span class="sxs-lookup"><span data-stu-id="8d785-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="8d785-456">String</span><span class="sxs-lookup"><span data-stu-id="8d785-456">String</span></span>|<span data-ttu-id="8d785-457">32 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-457">32 characters</span></span>|<span data-ttu-id="8d785-458">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-458">✔</span></span>|<span data-ttu-id="8d785-459">パラメーターのわかりやすいタイトルです。</span><span class="sxs-lookup"><span data-stu-id="8d785-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="8d785-460">String</span><span class="sxs-lookup"><span data-stu-id="8d785-460">String</span></span>|<span data-ttu-id="8d785-461">128 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-461">128 characters</span></span>||<span data-ttu-id="8d785-462">このパラメーターの目的を説明するわかりやすい文字列。</span><span class="sxs-lookup"><span data-stu-id="8d785-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="8d785-463">String</span><span class="sxs-lookup"><span data-stu-id="8d785-463">String</span></span>|<span data-ttu-id="8d785-464">128 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-464">128 characters</span></span>||<span data-ttu-id="8d785-465">のタスク モジュールに表示されるコントロールの種類を定義 `fetchTask: true` します。</span><span class="sxs-lookup"><span data-stu-id="8d785-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="8d785-466">の一 `text` つ `textarea` 、 、 、 、 `number` 、 `date` 、 `time` `toggle` 、 `choiceset`</span><span class="sxs-lookup"><span data-stu-id="8d785-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="8d785-467">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="8d785-467">Array of Objects</span></span>|<span data-ttu-id="8d785-468">10</span><span class="sxs-lookup"><span data-stu-id="8d785-468">10</span></span>||<span data-ttu-id="8d785-469">の選択肢オプション `choiceset` です。</span><span class="sxs-lookup"><span data-stu-id="8d785-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="8d785-470">の場合にのみ `parameter.inputType` 使用 `choiceset` します。</span><span class="sxs-lookup"><span data-stu-id="8d785-470">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="8d785-471">String</span><span class="sxs-lookup"><span data-stu-id="8d785-471">String</span></span>|<span data-ttu-id="8d785-472">128</span><span class="sxs-lookup"><span data-stu-id="8d785-472">128</span></span>||<span data-ttu-id="8d785-473">選択したタイトル。</span><span class="sxs-lookup"><span data-stu-id="8d785-473">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="8d785-474">String</span><span class="sxs-lookup"><span data-stu-id="8d785-474">String</span></span>|<span data-ttu-id="8d785-475">512</span><span class="sxs-lookup"><span data-stu-id="8d785-475">512</span></span>||<span data-ttu-id="8d785-476">Value of the choice.</span><span class="sxs-lookup"><span data-stu-id="8d785-476">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="8d785-477">permissions</span><span class="sxs-lookup"><span data-stu-id="8d785-477">permissions</span></span>

<span data-ttu-id="8d785-478">**Optional**</span><span class="sxs-lookup"><span data-stu-id="8d785-478">**Optional**</span></span>

<span data-ttu-id="8d785-479">`string`アプリが要求するアクセス許可を指定する配列で、エンド ユーザーに拡張機能の実行方法を知ることができます。</span><span class="sxs-lookup"><span data-stu-id="8d785-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="8d785-480">次のオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="8d785-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="8d785-481">`identity`&emsp;ユーザー ID 情報が必要です。</span><span class="sxs-lookup"><span data-stu-id="8d785-481">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="8d785-482">`messageTeamMembers`&emsp;チーム メンバーにダイレクト メッセージを送信する権限が必要です。</span><span class="sxs-lookup"><span data-stu-id="8d785-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="8d785-483">アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは更新されたアプリを初めて実行するときに同意プロセスを繰り返します。</span><span class="sxs-lookup"><span data-stu-id="8d785-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="8d785-484">デバイスアクセス許可</span><span class="sxs-lookup"><span data-stu-id="8d785-484">devicePermissions</span></span>

<span data-ttu-id="8d785-485">**オプション** 文字列の配列</span><span class="sxs-lookup"><span data-stu-id="8d785-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="8d785-486">アプリがアクセスを要求できるユーザーのデバイスのネイティブ機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="8d785-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="8d785-487">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="8d785-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="8d785-488">有効なドメイン</span><span class="sxs-lookup"><span data-stu-id="8d785-488">validDomains</span></span>

<span data-ttu-id="8d785-489">**省略可能** な ( **省略可能) (省略可能な** 場合は必須)</span><span class="sxs-lookup"><span data-stu-id="8d785-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="8d785-490">アプリがコンテンツを読み込むと想定している有効なドメインのリスト。</span><span class="sxs-lookup"><span data-stu-id="8d785-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="8d785-491">ドメインの一覧には、 などのワイルドカードを含めることができます `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="8d785-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="8d785-492">これは、ドメインの 1 つのセグメントと完全に一致します。一致させる必要がある場合は `a.b.example.com` `*.*.example.com` 、 を使用します。</span><span class="sxs-lookup"><span data-stu-id="8d785-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="8d785-493">タブ構成またはコンテンツ UI がタブ構成の使用以外のドメインに移動する必要がある場合は、ここでそのドメインを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="8d785-494">ただし、アプリでサポートする ID プロバイダーのドメインを含める必要 **はありません** 。</span><span class="sxs-lookup"><span data-stu-id="8d785-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="8d785-495">たとえば、Google ID を使用して認証するには、accounts.google.com にリダイレクトする必要がありますが、accounts.google.com を に含めるべきではありません `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="8d785-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8d785-496">直接またはワイルドカードを使用して、コントロールの外側にあるドメインを追加しないでください。</span><span class="sxs-lookup"><span data-stu-id="8d785-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="8d785-497">たとえば、 `yourapp.onmicrosoft.com` 有効ですが、 `*.onmicrosoft.com` 無効です。</span><span class="sxs-lookup"><span data-stu-id="8d785-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="8d785-498">オブジェクトは、 type のすべての要素を持つ配列です `string` 。</span><span class="sxs-lookup"><span data-stu-id="8d785-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="8d785-499">アプリケーション情報</span><span class="sxs-lookup"><span data-stu-id="8d785-499">webApplicationInfo</span></span>

<span data-ttu-id="8d785-500">**Optional**</span><span class="sxs-lookup"><span data-stu-id="8d785-500">**Optional**</span></span>

<span data-ttu-id="8d785-501">ユーザーが AAD アプリにシームレスにサインインできるように、AAD アプリ ID とGraph情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="8d785-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="8d785-502">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-502">Name</span></span>| <span data-ttu-id="8d785-503">型</span><span class="sxs-lookup"><span data-stu-id="8d785-503">Type</span></span>| <span data-ttu-id="8d785-504">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-504">Maximum size</span></span> | <span data-ttu-id="8d785-505">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-505">Required</span></span> | <span data-ttu-id="8d785-506">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="8d785-507">String</span><span class="sxs-lookup"><span data-stu-id="8d785-507">String</span></span>|<span data-ttu-id="8d785-508">36 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-508">36 characters</span></span>|<span data-ttu-id="8d785-509">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-509">✔</span></span>|<span data-ttu-id="8d785-510">アプリの AAD アプリケーション ID。</span><span class="sxs-lookup"><span data-stu-id="8d785-510">AAD application id of the app.</span></span> <span data-ttu-id="8d785-511">この ID は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="8d785-512">String</span><span class="sxs-lookup"><span data-stu-id="8d785-512">String</span></span>|<span data-ttu-id="8d785-513">2048 文字</span><span class="sxs-lookup"><span data-stu-id="8d785-513">2048 characters</span></span>|<span data-ttu-id="8d785-514">✔</span><span class="sxs-lookup"><span data-stu-id="8d785-514">✔</span></span>|<span data-ttu-id="8d785-515">SSO の認証トークンを取得するためのアプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="8d785-515">Resource url of app for acquiring auth token for SSO.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="8d785-516">構成可能なプロパティ</span><span class="sxs-lookup"><span data-stu-id="8d785-516">configurableProperties</span></span>

<span data-ttu-id="8d785-517">**オプション** - 配列</span><span class="sxs-lookup"><span data-stu-id="8d785-517">**Optional** - array</span></span>

<span data-ttu-id="8d785-518">`configurableProperties`このブロックは、管理者がカスタマイズできるアプリのプロパティTeams定義します。</span><span class="sxs-lookup"><span data-stu-id="8d785-518">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="8d785-519">詳細については、「 [Microsoft Teams でアプリをカスタマイズする](/MicrosoftTeams/customize-apps)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d785-519">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="8d785-520">最低 1 つのプロパティを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-520">A minimum of one property must be defined.</span></span> <span data-ttu-id="8d785-521">このブロックには最大 9 つのプロパティを定義できます。</span><span class="sxs-lookup"><span data-stu-id="8d785-521">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="8d785-522">ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d785-522">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> 

<span data-ttu-id="8d785-523">次のプロパティを定義できます。</span><span class="sxs-lookup"><span data-stu-id="8d785-523">You can define any of the following properties:</span></span>
* <span data-ttu-id="8d785-524">`name`: 管理者がアプリの表示名を変更できるようにします。</span><span class="sxs-lookup"><span data-stu-id="8d785-524">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="8d785-525">`shortDescription`: 管理者がアプリの簡単な説明を変更できるようにします。</span><span class="sxs-lookup"><span data-stu-id="8d785-525">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="8d785-526">`longDescription`: 管理者がアプリの詳細な説明を変更できるようにします。</span><span class="sxs-lookup"><span data-stu-id="8d785-526">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="8d785-527">`smallImageUrl`: マニフェストの `outline` `icons` ブロック内のプロパティです。</span><span class="sxs-lookup"><span data-stu-id="8d785-527">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="8d785-528">`largeImageUrl`: マニフェストの `color` `icons` ブロック内のプロパティです。</span><span class="sxs-lookup"><span data-stu-id="8d785-528">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="8d785-529">`accentColor`: アウトライン アイコンの背景と組み合わせて使用する色です。</span><span class="sxs-lookup"><span data-stu-id="8d785-529">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="8d785-530">`websiteUrl`: 開発者のウェブサイトへの https:// URLです。</span><span class="sxs-lookup"><span data-stu-id="8d785-530">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="8d785-531">`privacyUrl`: 開発者のプライバシー ポリシーへの https:// URL です。</span><span class="sxs-lookup"><span data-stu-id="8d785-531">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="8d785-532">`termsOfUseUrl`: 開発者の利用規約の https:// URL です。</span><span class="sxs-lookup"><span data-stu-id="8d785-532">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="8d785-533">デフォルトインストールスコープ</span><span class="sxs-lookup"><span data-stu-id="8d785-533">defaultInstallScope</span></span>

<span data-ttu-id="8d785-534">**省略可能** - 文字列</span><span class="sxs-lookup"><span data-stu-id="8d785-534">**Optional** - string</span></span>

<span data-ttu-id="8d785-535">既定でこのアプリに対して定義されているインストール スコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="8d785-535">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="8d785-536">定義されたスコープは、ユーザーがアプリを追加しようとしたときにボタンに表示されるオプションになります。</span><span class="sxs-lookup"><span data-stu-id="8d785-536">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="8d785-537">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="8d785-537">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="8d785-538">分類の機能</span><span class="sxs-lookup"><span data-stu-id="8d785-538">defaultGroupCapability</span></span>

<span data-ttu-id="8d785-539">**オプション** - オブジェクト</span><span class="sxs-lookup"><span data-stu-id="8d785-539">**Optional** - object</span></span>

<span data-ttu-id="8d785-540">グループのインストール スコープが選択されると、ユーザーがアプリをインストールするときに既定の機能が定義されます。</span><span class="sxs-lookup"><span data-stu-id="8d785-540">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="8d785-541">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="8d785-541">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="8d785-542">名前</span><span class="sxs-lookup"><span data-stu-id="8d785-542">Name</span></span>| <span data-ttu-id="8d785-543">型</span><span class="sxs-lookup"><span data-stu-id="8d785-543">Type</span></span>| <span data-ttu-id="8d785-544">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="8d785-544">Maximum size</span></span> | <span data-ttu-id="8d785-545">必須</span><span class="sxs-lookup"><span data-stu-id="8d785-545">Required</span></span> | <span data-ttu-id="8d785-546">説明</span><span class="sxs-lookup"><span data-stu-id="8d785-546">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="8d785-547">string</span><span class="sxs-lookup"><span data-stu-id="8d785-547">string</span></span>|||<span data-ttu-id="8d785-548">選択したインストールスコープが `team` の場合、このフィールドは使用可能なデフォルトの機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="8d785-548">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="8d785-549">オプション : `tab` 、 `bot` 、 、 、 `connector`</span><span class="sxs-lookup"><span data-stu-id="8d785-549">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="8d785-550">string</span><span class="sxs-lookup"><span data-stu-id="8d785-550">string</span></span>|||<span data-ttu-id="8d785-551">選択したインストールスコープが `groupchat` の場合、このフィールドは使用可能なデフォルトの機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="8d785-551">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="8d785-552">オプション : `tab` 、 `bot` 、 、 、 `connector`</span><span class="sxs-lookup"><span data-stu-id="8d785-552">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="8d785-553">string</span><span class="sxs-lookup"><span data-stu-id="8d785-553">string</span></span>|||<span data-ttu-id="8d785-554">選択したインストールスコープが `meetings` の場合、このフィールドは使用可能なデフォルトの機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="8d785-554">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="8d785-555">オプション : `tab` 、 `bot` 、 、 、 `connector`</span><span class="sxs-lookup"><span data-stu-id="8d785-555">Options: `tab`, `bot`, or `connector`.</span></span>|

