---
title: 開発者プレビューマニフェストスキーマの参照
description: Microsoft Teams のマニフェストによってサポートされるスキーマについて説明します。
keywords: teams マニフェストスキーマ開発者プレビュー
ms.date: 05/20/2019
ms.openlocfilehash: b99e1ae99b7fd1edd4c695f43f3ac25270f0c710
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674647"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="6b7db-104">Microsoft Teams の開発者プレビューマニフェストスキーマ</span><span class="sxs-lookup"><span data-stu-id="6b7db-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="6b7db-105">このプログラムの詳細と参加方法については、「[開発者プレビュー](~/resources/dev-preview/developer-preview-intro.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6b7db-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="6b7db-106">開発者プレビューを使用していない場合は、このバージョンのマニフェストを使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="6b7db-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="6b7db-107">マニフェストの公開バージョンについては、「 [Reference: manifest schema For Microsoft Teams](~/resources/schema/manifest-schema.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6b7db-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="6b7db-108">Microsoft Teams のマニフェストでは、アプリを Microsoft Teams 製品に統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="6b7db-109">マニフェストは、で[`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json)ホストされているスキーマに準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="6b7db-110">利用可能な機能の詳細については[、「Microsoft Teams の一般開発者向けプレビュー」](~/resources/dev-preview/developer-preview-features.md)の「機能」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6b7db-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="6b7db-111">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="6b7db-111">Sample full manifest</span></span>

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
  ]
}
```

<span data-ttu-id="6b7db-112">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="6b7db-113">$schema</span><span class="sxs-lookup"><span data-stu-id="6b7db-113">$schema</span></span>

<span data-ttu-id="6b7db-114">*省略可能。ただし、推奨* &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="6b7db-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="6b7db-115">マニフェストの JSON スキーマを参照する https://URL。</span><span class="sxs-lookup"><span data-stu-id="6b7db-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="6b7db-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="6b7db-116">manifestVersion</span></span>

<span data-ttu-id="6b7db-117">**必要な** &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="6b7db-117">**Required** &ndash; String</span></span>

<span data-ttu-id="6b7db-118">このマニフェストが使用しているマニフェストスキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="6b7db-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="6b7db-119">"DevPreview" である必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="6b7db-120">バージョン</span><span class="sxs-lookup"><span data-stu-id="6b7db-120">version</span></span>

<span data-ttu-id="6b7db-121">**必要な** &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="6b7db-121">**Required** &ndash; String</span></span>

<span data-ttu-id="6b7db-122">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="6b7db-122">The version of the specific app.</span></span> <span data-ttu-id="6b7db-123">マニフェスト内の内容を更新する場合は、そのバージョンも同時にインクリメントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="6b7db-124">このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="6b7db-125">このアプリがストアに送信された場合は、新しいマニフェストを再送信して再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="6b7db-126">その後、このアプリのユーザーは、承認後に数時間以内に新しい更新されたマニフェストを自動的に取得します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="6b7db-127">アプリによって要求されたアクセス許可が変更された場合、ユーザーはアプリをアップグレードして再同意するように求められます。</span><span class="sxs-lookup"><span data-stu-id="6b7db-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="6b7db-128">このバージョンの文字列は、 [semver](http://semver.org/)標準 (メジャー) に従う必要があります。間隔.パッチ)。</span><span class="sxs-lookup"><span data-stu-id="6b7db-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="6b7db-129">ID</span><span class="sxs-lookup"><span data-stu-id="6b7db-129">id</span></span>

<span data-ttu-id="6b7db-130">**必要な** &ndash; Microsoft アプリ ID</span><span class="sxs-lookup"><span data-stu-id="6b7db-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="6b7db-131">このアプリの一意の Microsoft 生成識別子。</span><span class="sxs-lookup"><span data-stu-id="6b7db-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="6b7db-132">Microsoft Bot フレームワークを介して bot を登録した場合、またはタブの web アプリが Microsoft によって既にサインインしている場合は、既に ID があるので、ここで入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="6b7db-133">それ以外の場合は、Microsoft アプリケーション登録ポータル ([My Applications](https://apps.dev.microsoft.com)) で新しい ID を生成し、ここで入力してから、 [bot を追加](~/bots/how-to/create-a-bot-for-teams.md)するときにそれを再利用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="6b7db-134">packageName</span><span class="sxs-lookup"><span data-stu-id="6b7db-134">packageName</span></span>

<span data-ttu-id="6b7db-135">**必要な** &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="6b7db-135">**Required** &ndash; String</span></span>

<span data-ttu-id="6b7db-136">逆引きドメイン表記でのこのアプリの一意識別子。たとえば、例のようになります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="6b7db-137">developer</span><span class="sxs-lookup"><span data-stu-id="6b7db-137">developer</span></span>

<span data-ttu-id="6b7db-138">**必須**</span><span class="sxs-lookup"><span data-stu-id="6b7db-138">**Required**</span></span>

<span data-ttu-id="6b7db-139">会社に関する情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-139">Specifies information about your company.</span></span> <span data-ttu-id="6b7db-140">AppSource (旧称 Office ストア) に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="6b7db-141">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-141">Name</span></span>| <span data-ttu-id="6b7db-142">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-142">Maximum size</span></span> | <span data-ttu-id="6b7db-143">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-143">Required</span></span> | <span data-ttu-id="6b7db-144">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="6b7db-145">32文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-145">32 characters</span></span>|<span data-ttu-id="6b7db-146">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-146">✔</span></span>|<span data-ttu-id="6b7db-147">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="6b7db-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="6b7db-148">2048 文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-148">2048 characters</span></span>|<span data-ttu-id="6b7db-149">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-149">✔</span></span>|<span data-ttu-id="6b7db-150">開発者の web サイトへの https://URL。</span><span class="sxs-lookup"><span data-stu-id="6b7db-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="6b7db-151">このリンクは、ユーザーを会社または製品固有のランディングページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="6b7db-152">2048 文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-152">2048 characters</span></span>|<span data-ttu-id="6b7db-153">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-153">✔</span></span>|<span data-ttu-id="6b7db-154">開発者のプライバシーポリシーへの https://URL。</span><span class="sxs-lookup"><span data-stu-id="6b7db-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="6b7db-155">2048 文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-155">2048 characters</span></span>|<span data-ttu-id="6b7db-156">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-156">✔</span></span>|<span data-ttu-id="6b7db-157">開発者の使用条件への https://URL。</span><span class="sxs-lookup"><span data-stu-id="6b7db-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="6b7db-158">10文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-158">10 characters</span></span>|<span data-ttu-id="6b7db-159">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-159">✔</span></span>|<span data-ttu-id="6b7db-160">**省略可能**アプリを構築するパートナー組織を識別する Microsoft パートナーのネットワーク ID。</span><span class="sxs-lookup"><span data-stu-id="6b7db-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="6b7db-161">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="6b7db-161">localizationInfo</span></span>

<span data-ttu-id="6b7db-162">**Optional**</span><span class="sxs-lookup"><span data-stu-id="6b7db-162">**Optional**</span></span>

<span data-ttu-id="6b7db-163">既定の言語の指定、および追加の言語ファイルへのポインターを許可します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="6b7db-164">「[ローカライズ](~/concepts/build-and-test/apps-localization.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6b7db-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="6b7db-165">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-165">Name</span></span>| <span data-ttu-id="6b7db-166">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-166">Maximum size</span></span> | <span data-ttu-id="6b7db-167">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-167">Required</span></span> | <span data-ttu-id="6b7db-168">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="6b7db-169">4文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-169">4 characters</span></span>|<span data-ttu-id="6b7db-170">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-170">✔</span></span>|<span data-ttu-id="6b7db-171">このトップレベルマニフェストファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="6b7db-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="6b7db-172">localizationInfo. additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="6b7db-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="6b7db-173">追加の言語の翻訳を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="6b7db-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="6b7db-174">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-174">Name</span></span>| <span data-ttu-id="6b7db-175">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-175">Maximum size</span></span> | <span data-ttu-id="6b7db-176">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-176">Required</span></span> | <span data-ttu-id="6b7db-177">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="6b7db-178">4文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-178">4 characters</span></span>|<span data-ttu-id="6b7db-179">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-179">✔</span></span>|<span data-ttu-id="6b7db-180">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="6b7db-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="6b7db-181">4文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-181">4 characters</span></span>|<span data-ttu-id="6b7db-182">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-182">✔</span></span>|<span data-ttu-id="6b7db-183">翻訳された文字列を含む json ファイルへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="6b7db-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="6b7db-184">name</span><span class="sxs-lookup"><span data-stu-id="6b7db-184">name</span></span>

<span data-ttu-id="6b7db-185">**必須**</span><span class="sxs-lookup"><span data-stu-id="6b7db-185">**Required**</span></span>

<span data-ttu-id="6b7db-186">Teams でユーザーに表示されるアプリの動作の名前です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="6b7db-187">AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="6b7db-188">との`short`値を`full`同じにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="6b7db-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="6b7db-189">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-189">Name</span></span>| <span data-ttu-id="6b7db-190">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-190">Maximum size</span></span> | <span data-ttu-id="6b7db-191">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-191">Required</span></span> | <span data-ttu-id="6b7db-192">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="6b7db-193">30 文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-193">30 characters</span></span>|<span data-ttu-id="6b7db-194">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-194">✔</span></span>|<span data-ttu-id="6b7db-195">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="6b7db-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="6b7db-196">100 文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-196">100 characters</span></span>||<span data-ttu-id="6b7db-197">アプリの完全な名前。アプリの完全な名前が30文字を超えている場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="6b7db-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="6b7db-198">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-198">description</span></span>

<span data-ttu-id="6b7db-199">**必須**</span><span class="sxs-lookup"><span data-stu-id="6b7db-199">**Required**</span></span>

<span data-ttu-id="6b7db-200">ユーザーに対してアプリを記述します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-200">Describes your app to users.</span></span> <span data-ttu-id="6b7db-201">AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="6b7db-202">説明に正確に表示されていることを確認し、お客様が快適な動作を理解するのに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="6b7db-203">また、外部アカウントが使用するために必要な場合は、詳細な説明にも注意してください。</span><span class="sxs-lookup"><span data-stu-id="6b7db-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="6b7db-204">との`short`値を`full`同じにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="6b7db-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="6b7db-205">短い説明を長い説明の中で繰り返すことはできません。他のアプリ名を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="6b7db-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="6b7db-206">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-206">Name</span></span>| <span data-ttu-id="6b7db-207">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-207">Maximum size</span></span> | <span data-ttu-id="6b7db-208">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-208">Required</span></span> | <span data-ttu-id="6b7db-209">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="6b7db-210">80文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-210">80 characters</span></span>|<span data-ttu-id="6b7db-211">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-211">✔</span></span>|<span data-ttu-id="6b7db-212">スペースが制限されている場合に使用する、アプリの使用状況の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="6b7db-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="6b7db-213">4000文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-213">4000 characters</span></span>|<span data-ttu-id="6b7db-214">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-214">✔</span></span>|<span data-ttu-id="6b7db-215">アプリの詳細な説明。</span><span class="sxs-lookup"><span data-stu-id="6b7db-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="6b7db-216">アイコン</span><span class="sxs-lookup"><span data-stu-id="6b7db-216">icons</span></span>

<span data-ttu-id="6b7db-217">**必須**</span><span class="sxs-lookup"><span data-stu-id="6b7db-217">**Required**</span></span>

<span data-ttu-id="6b7db-218">Teams アプリ内で使用されるアイコン。</span><span class="sxs-lookup"><span data-stu-id="6b7db-218">Icons used within the Teams app.</span></span> <span data-ttu-id="6b7db-219">アイコンファイルは、アップロードパッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="6b7db-220">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-220">Name</span></span>| <span data-ttu-id="6b7db-221">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-221">Maximum size</span></span> | <span data-ttu-id="6b7db-222">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-222">Required</span></span> | <span data-ttu-id="6b7db-223">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="6b7db-224">2048 文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-224">2048 characters</span></span>|<span data-ttu-id="6b7db-225">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-225">✔</span></span>|<span data-ttu-id="6b7db-226">透明な32x32 の PNG アウトラインアイコンへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="6b7db-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="6b7db-227">2048 文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-227">2048 characters</span></span>|<span data-ttu-id="6b7db-228">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-228">✔</span></span>|<span data-ttu-id="6b7db-229">フルカラー 192x192 PNG アイコンへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="6b7db-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="6b7db-230">アクセントカラー</span><span class="sxs-lookup"><span data-stu-id="6b7db-230">accentColor</span></span>

<span data-ttu-id="6b7db-231">**必要な** &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="6b7db-231">**Required** &ndash; String</span></span>

<span data-ttu-id="6b7db-232">とと組み合わせてアウトラインアイコンの背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="6b7db-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="6b7db-233">この値は、' # ' で始まる有効な HTML カラーコードである必要`#4464ee`があります (例:)。</span><span class="sxs-lookup"><span data-stu-id="6b7db-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="6b7db-234">の各タブ</span><span class="sxs-lookup"><span data-stu-id="6b7db-234">configurableTabs</span></span>

<span data-ttu-id="6b7db-235">**Optional**</span><span class="sxs-lookup"><span data-stu-id="6b7db-235">**Optional**</span></span>

<span data-ttu-id="6b7db-236">アプリの機能に、追加の構成を必要とするチームチャネルのタブがある場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="6b7db-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="6b7db-237">構成可能なタブは teams スコープでのみサポートされており、現在、アプリごとに1つのタブのみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="6b7db-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="6b7db-238">Object は、型`object`のすべての要素を含む配列です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="6b7db-239">このブロックは、構成可能なチャネルのタブソリューションを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="6b7db-240">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-240">Name</span></span>| <span data-ttu-id="6b7db-241">型</span><span class="sxs-lookup"><span data-stu-id="6b7db-241">Type</span></span>| <span data-ttu-id="6b7db-242">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-242">Maximum size</span></span> | <span data-ttu-id="6b7db-243">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-243">Required</span></span> | <span data-ttu-id="6b7db-244">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="6b7db-245">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-245">String</span></span>|<span data-ttu-id="6b7db-246">2048 文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-246">2048 characters</span></span>|<span data-ttu-id="6b7db-247">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-247">✔</span></span>|<span data-ttu-id="6b7db-248">タブを構成するときに使用する https://URL。</span><span class="sxs-lookup"><span data-stu-id="6b7db-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="6b7db-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="6b7db-249">Boolean</span></span>|||<span data-ttu-id="6b7db-250">作成後にタブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="6b7db-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="6b7db-251">限り`true`</span><span class="sxs-lookup"><span data-stu-id="6b7db-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="6b7db-252">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-252">Array of enum</span></span>|<span data-ttu-id="6b7db-253">1 </span><span class="sxs-lookup"><span data-stu-id="6b7db-253">1</span></span>|<span data-ttu-id="6b7db-254">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-254">✔</span></span>|<span data-ttu-id="6b7db-255">現在、構成可能なタブで`team`は`groupchat` 、およびスコープのみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="6b7db-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="6b7db-256">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-256">String</span></span>|<span data-ttu-id="6b7db-257">2048</span><span class="sxs-lookup"><span data-stu-id="6b7db-257">2048</span></span>||<span data-ttu-id="6b7db-258">SharePoint で使用するタブプレビュー画像への相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="6b7db-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="6b7db-259">サイズ1024x768。</span><span class="sxs-lookup"><span data-stu-id="6b7db-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="6b7db-260">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-260">Array of enum</span></span>|<span data-ttu-id="6b7db-261">1 </span><span class="sxs-lookup"><span data-stu-id="6b7db-261">1</span></span>||<span data-ttu-id="6b7db-262">SharePoint でどのようにタブを使用できるようにするかを定義します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="6b7db-263">オプション`sharePointFullPage`と`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="6b7db-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="6b7db-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="6b7db-264">staticTabs</span></span>

<span data-ttu-id="6b7db-265">**Optional**</span><span class="sxs-lookup"><span data-stu-id="6b7db-265">**Optional**</span></span>

<span data-ttu-id="6b7db-266">ユーザーが手動で追加せずに、既定で "固定" できるタブのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="6b7db-267">スコープ内で`personal`宣言されている静的タブは、常にアプリの個人の環境に固定されます。</span><span class="sxs-lookup"><span data-stu-id="6b7db-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="6b7db-268">`team`スコープ内で宣言されている静的タブは現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="6b7db-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="6b7db-269">Object は、型`object`のすべての要素を含む配列 (最大16個の要素) です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="6b7db-270">このブロックは、静的なタブソリューションを提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="6b7db-271">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-271">Name</span></span>| <span data-ttu-id="6b7db-272">型</span><span class="sxs-lookup"><span data-stu-id="6b7db-272">Type</span></span>| <span data-ttu-id="6b7db-273">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-273">Maximum size</span></span> | <span data-ttu-id="6b7db-274">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-274">Required</span></span> | <span data-ttu-id="6b7db-275">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="6b7db-276">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-276">String</span></span>|<span data-ttu-id="6b7db-277">64文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-277">64 characters</span></span>|<span data-ttu-id="6b7db-278">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-278">✔</span></span>|<span data-ttu-id="6b7db-279">タブに表示されるエンティティの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="6b7db-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="6b7db-280">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-280">String</span></span>|<span data-ttu-id="6b7db-281">128文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-281">128 characters</span></span>|<span data-ttu-id="6b7db-282">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-282">✔</span></span>|<span data-ttu-id="6b7db-283">チャネルインターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="6b7db-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="6b7db-284">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-284">String</span></span>|<span data-ttu-id="6b7db-285">2048 文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-285">2048 characters</span></span>|<span data-ttu-id="6b7db-286">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-286">✔</span></span>|<span data-ttu-id="6b7db-287">Teams キャンバスに表示されるエンティティ UI をポイントする https://URL。</span><span class="sxs-lookup"><span data-stu-id="6b7db-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="6b7db-288">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-288">String</span></span>|<span data-ttu-id="6b7db-289">2048 文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-289">2048 characters</span></span>||<span data-ttu-id="6b7db-290">ユーザーがブラウザーで表示をポイントしたかどうかを示す https://URL。</span><span class="sxs-lookup"><span data-stu-id="6b7db-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="6b7db-291">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-291">Array of enum</span></span>|<span data-ttu-id="6b7db-292">1 </span><span class="sxs-lookup"><span data-stu-id="6b7db-292">1</span></span>|<span data-ttu-id="6b7db-293">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-293">✔</span></span>|<span data-ttu-id="6b7db-294">現時点では、静的タブで`personal`はスコープのみがサポートされます。つまり、個人の利便性の一環としてのみプロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="6b7db-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="6b7db-295">bot</span><span class="sxs-lookup"><span data-stu-id="6b7db-295">bots</span></span>

<span data-ttu-id="6b7db-296">**Optional**</span><span class="sxs-lookup"><span data-stu-id="6b7db-296">**Optional**</span></span>

<span data-ttu-id="6b7db-297">Bot ソリューションと、既定のコマンドプロパティなどのオプション情報を定義します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="6b7db-298">オブジェクトが配列の場合 (現時点では1つ&mdash;の要素のうちの最大値は1つですが、現在は`object`アプリごとに1つの bot のみが許可されます)、型のすべての要素を使用します</span><span class="sxs-lookup"><span data-stu-id="6b7db-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="6b7db-299">このブロックは、bot の環境を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="6b7db-300">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-300">Name</span></span>| <span data-ttu-id="6b7db-301">型</span><span class="sxs-lookup"><span data-stu-id="6b7db-301">Type</span></span>| <span data-ttu-id="6b7db-302">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-302">Maximum size</span></span> | <span data-ttu-id="6b7db-303">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-303">Required</span></span> | <span data-ttu-id="6b7db-304">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="6b7db-305">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-305">String</span></span>|<span data-ttu-id="6b7db-306">64文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-306">64 characters</span></span>|<span data-ttu-id="6b7db-307">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-307">✔</span></span>|<span data-ttu-id="6b7db-308">Bot フレームワークに登録された bot の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="6b7db-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="6b7db-309">これは、アプリの全体的な[ID](#id)と同じである場合もあります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="6b7db-310">Boolean</span><span class="sxs-lookup"><span data-stu-id="6b7db-310">Boolean</span></span>|||<span data-ttu-id="6b7db-311">Bot がユーザーヒントを利用して、特定のチャネルに bot を追加するかどうかを記述します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="6b7db-312">限り`false`</span><span class="sxs-lookup"><span data-stu-id="6b7db-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="6b7db-313">Boolean</span><span class="sxs-lookup"><span data-stu-id="6b7db-313">Boolean</span></span>|||<span data-ttu-id="6b7db-314">Bot が、話し言葉とは異なり、単一の通知のみの bot であるかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="6b7db-315">限り`false`</span><span class="sxs-lookup"><span data-stu-id="6b7db-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="6b7db-316">Boolean</span><span class="sxs-lookup"><span data-stu-id="6b7db-316">Boolean</span></span>|||<span data-ttu-id="6b7db-317">Bot が個人チャットでファイルをアップロード/ダウンロードする機能をサポートしているかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="6b7db-318">限り`false`</span><span class="sxs-lookup"><span data-stu-id="6b7db-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="6b7db-319">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-319">Array of enum</span></span>|<span data-ttu-id="6b7db-320">3 </span><span class="sxs-lookup"><span data-stu-id="6b7db-320">3</span></span>|<span data-ttu-id="6b7db-321">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-321">✔</span></span>|<span data-ttu-id="6b7db-322">Bot が a `team`内のチャネル、グループチャット (`groupchat`)、または個別のユーザー単独 (`personal`) に限定された環境での動作を提供するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="6b7db-323">これらのオプションは排他的ではありません。</span><span class="sxs-lookup"><span data-stu-id="6b7db-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="6b7db-324">bot リスト</span><span class="sxs-lookup"><span data-stu-id="6b7db-324">bots.commandLists</span></span>

<span data-ttu-id="6b7db-325">Bot がユーザーに推奨できるコマンドのオプションの一覧。</span><span class="sxs-lookup"><span data-stu-id="6b7db-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="6b7db-326">Object は、型`object`のすべての要素を含む配列 (最大2つの要素) です。bot がサポートするスコープごとに個別のコマンドリストを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="6b7db-327">詳細については、「 [Bot メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6b7db-327">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="6b7db-328">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-328">Name</span></span>| <span data-ttu-id="6b7db-329">型</span><span class="sxs-lookup"><span data-stu-id="6b7db-329">Type</span></span>| <span data-ttu-id="6b7db-330">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-330">Maximum size</span></span> | <span data-ttu-id="6b7db-331">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-331">Required</span></span> | <span data-ttu-id="6b7db-332">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="6b7db-333">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-333">array of enum</span></span>|<span data-ttu-id="6b7db-334">3 </span><span class="sxs-lookup"><span data-stu-id="6b7db-334">3</span></span>|<span data-ttu-id="6b7db-335">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-335">✔</span></span>|<span data-ttu-id="6b7db-336">コマンドリストが有効である範囲を指定します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="6b7db-337">オプションは`team`、 `personal`、、 `groupchat`です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="6b7db-338">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-338">array of objects</span></span>|<span data-ttu-id="6b7db-339">10 </span><span class="sxs-lookup"><span data-stu-id="6b7db-339">10</span></span>|<span data-ttu-id="6b7db-340">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-340">✔</span></span>|<span data-ttu-id="6b7db-341">Bot がサポートするコマンドの配列。</span><span class="sxs-lookup"><span data-stu-id="6b7db-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="6b7db-342">`title`: bot コマンド名 (string, 32)</span><span class="sxs-lookup"><span data-stu-id="6b7db-342">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="6b7db-343">`description`: コマンド構文とその引数の簡単な説明または例 (string, 128)</span><span class="sxs-lookup"><span data-stu-id="6b7db-343">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="6b7db-344">コネクタ</span><span class="sxs-lookup"><span data-stu-id="6b7db-344">connectors</span></span>

<span data-ttu-id="6b7db-345">**Optional**</span><span class="sxs-lookup"><span data-stu-id="6b7db-345">**Optional**</span></span>

<span data-ttu-id="6b7db-346">ブロック`connectors`は、アプリの Office 365 コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="6b7db-347">Object は、type `object`のすべての要素を含む配列 (最大1つの要素) です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="6b7db-348">このブロックは、コネクタを提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="6b7db-349">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-349">Name</span></span>| <span data-ttu-id="6b7db-350">型</span><span class="sxs-lookup"><span data-stu-id="6b7db-350">Type</span></span>| <span data-ttu-id="6b7db-351">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-351">Maximum size</span></span> | <span data-ttu-id="6b7db-352">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-352">Required</span></span> | <span data-ttu-id="6b7db-353">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="6b7db-354">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-354">String</span></span>|<span data-ttu-id="6b7db-355">2048 文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-355">2048 characters</span></span>|<span data-ttu-id="6b7db-356">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-356">✔</span></span>|<span data-ttu-id="6b7db-357">コネクタを構成するときに使用する https://URL。</span><span class="sxs-lookup"><span data-stu-id="6b7db-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="6b7db-358">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-358">String</span></span>|<span data-ttu-id="6b7db-359">64文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-359">64 characters</span></span>|<span data-ttu-id="6b7db-360">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-360">✔</span></span>|<span data-ttu-id="6b7db-361">コネクタ[開発者ダッシュボード](https://aka.ms/connectorsdashboard)の ID と一致するコネクタの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="6b7db-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="6b7db-362">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-362">Array of enum</span></span>|<span data-ttu-id="6b7db-363">1 </span><span class="sxs-lookup"><span data-stu-id="6b7db-363">1</span></span>|<span data-ttu-id="6b7db-364">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-364">✔</span></span>|<span data-ttu-id="6b7db-365">コネクタが内`team`のチャネルのコンテキストで、または個別のユーザー単独 (`personal`) にスコープ設定された環境での動作を提供するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="6b7db-366">現時点では、 `team`範囲のみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="6b7db-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="6b7db-367">この機能</span><span class="sxs-lookup"><span data-stu-id="6b7db-367">composeExtensions</span></span>

<span data-ttu-id="6b7db-368">**Optional**</span><span class="sxs-lookup"><span data-stu-id="6b7db-368">**Optional**</span></span>

<span data-ttu-id="6b7db-369">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="6b7db-370">この機能の名前は、2017年11月に「[作成] 拡張機能」から「messaging extension」に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は同じままです。</span><span class="sxs-lookup"><span data-stu-id="6b7db-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="6b7db-371">Object は、type `object`のすべての要素を含む配列 (最大1つの要素) です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="6b7db-372">このブロックは、メッセージング拡張機能を提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="6b7db-373">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-373">Name</span></span>| <span data-ttu-id="6b7db-374">型</span><span class="sxs-lookup"><span data-stu-id="6b7db-374">Type</span></span> | <span data-ttu-id="6b7db-375">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-375">Maximum Size</span></span> | <span data-ttu-id="6b7db-376">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-376">Required</span></span> | <span data-ttu-id="6b7db-377">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="6b7db-378">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-378">String</span></span>|<span data-ttu-id="6b7db-379">64</span><span class="sxs-lookup"><span data-stu-id="6b7db-379">64</span></span>|<span data-ttu-id="6b7db-380">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-380">✔</span></span>|<span data-ttu-id="6b7db-381">Bot フレームワークに登録されているメッセージング拡張機能をバックアップする bot の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="6b7db-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="6b7db-382">これは、アプリの全体的な[ID](#id)と同じである場合もあります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="6b7db-383">Boolean</span><span class="sxs-lookup"><span data-stu-id="6b7db-383">Boolean</span></span>|||<span data-ttu-id="6b7db-384">メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="6b7db-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="6b7db-385">既定値は `false` です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="6b7db-386">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-386">Array of object</span></span>|<span data-ttu-id="6b7db-387">10 </span><span class="sxs-lookup"><span data-stu-id="6b7db-387">10</span></span>|<span data-ttu-id="6b7db-388">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-388">✔</span></span>|<span data-ttu-id="6b7db-389">メッセージング拡張機能がサポートするコマンドの配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="6b7db-390">このコマンドの機能</span><span class="sxs-lookup"><span data-stu-id="6b7db-390">composeExtensions.commands</span></span>

<span data-ttu-id="6b7db-391">メッセージング拡張機能は、1つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="6b7db-392">各コマンドは、Microsoft Teams に UI ベースのエントリポイントからの潜在的な操作として表示されます。</span><span class="sxs-lookup"><span data-stu-id="6b7db-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="6b7db-393">最大10個のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="6b7db-394">各コマンド項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="6b7db-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="6b7db-395">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-395">Name</span></span>| <span data-ttu-id="6b7db-396">型</span><span class="sxs-lookup"><span data-stu-id="6b7db-396">Type</span></span>| <span data-ttu-id="6b7db-397">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-397">Maximum size</span></span> | <span data-ttu-id="6b7db-398">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-398">Required</span></span> | <span data-ttu-id="6b7db-399">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="6b7db-400">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-400">String</span></span>|<span data-ttu-id="6b7db-401">64文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-401">64 characters</span></span>|<span data-ttu-id="6b7db-402">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-402">✔</span></span>|<span data-ttu-id="6b7db-403">コマンドの ID</span><span class="sxs-lookup"><span data-stu-id="6b7db-403">The ID for the command</span></span>|
|`type`|<span data-ttu-id="6b7db-404">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-404">String</span></span>|<span data-ttu-id="6b7db-405">64文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-405">64 characters</span></span>||<span data-ttu-id="6b7db-406">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="6b7db-406">Type of the command.</span></span> <span data-ttu-id="6b7db-407">または`query` `action`のいずれかです。</span><span class="sxs-lookup"><span data-stu-id="6b7db-407">One of `query` or `action`.</span></span> <span data-ttu-id="6b7db-408">限り`query`</span><span class="sxs-lookup"><span data-stu-id="6b7db-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="6b7db-409">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-409">String</span></span>|<span data-ttu-id="6b7db-410">32文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-410">32 characters</span></span>|<span data-ttu-id="6b7db-411">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-411">✔</span></span>|<span data-ttu-id="6b7db-412">ユーザーフレンドリなコマンド名</span><span class="sxs-lookup"><span data-stu-id="6b7db-412">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="6b7db-413">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-413">String</span></span>|<span data-ttu-id="6b7db-414">128文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-414">128 characters</span></span>||<span data-ttu-id="6b7db-415">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="6b7db-415">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="6b7db-416">Boolean</span><span class="sxs-lookup"><span data-stu-id="6b7db-416">Boolean</span></span>|||<span data-ttu-id="6b7db-417">パラメーターを指定せずにコマンドを最初に実行する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="6b7db-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="6b7db-418">限り`false`</span><span class="sxs-lookup"><span data-stu-id="6b7db-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="6b7db-419">文字列 (String) の配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-419">Array of Strings</span></span>|<span data-ttu-id="6b7db-420">3 </span><span class="sxs-lookup"><span data-stu-id="6b7db-420">3</span></span>||<span data-ttu-id="6b7db-421">メッセージの内線番号をから呼び出すことができる場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="6b7db-422">、 `commandBox`、 `message`の`compose`任意の組み合わせ。</span><span class="sxs-lookup"><span data-stu-id="6b7db-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="6b7db-423">既定値は`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="6b7db-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="6b7db-424">Boolean</span><span class="sxs-lookup"><span data-stu-id="6b7db-424">Boolean</span></span>|||<span data-ttu-id="6b7db-425">タスクモジュールを動的に取得する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="6b7db-425">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="6b7db-426">オブジェクト</span><span class="sxs-lookup"><span data-stu-id="6b7db-426">Object</span></span>|||<span data-ttu-id="6b7db-427">メッセージ拡張コマンドの使用時にプリロードするタスクモジュールを指定する</span><span class="sxs-lookup"><span data-stu-id="6b7db-427">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="6b7db-428">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-428">String</span></span>|<span data-ttu-id="6b7db-429">64</span><span class="sxs-lookup"><span data-stu-id="6b7db-429">64</span></span>||<span data-ttu-id="6b7db-430">最初のダイアログのタイトル</span><span class="sxs-lookup"><span data-stu-id="6b7db-430">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="6b7db-431">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-431">String</span></span>|||<span data-ttu-id="6b7db-432">ダイアログの幅。ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="6b7db-433">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-433">String</span></span>|||<span data-ttu-id="6b7db-434">ダイアログの高さ-ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="6b7db-435">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-435">String</span></span>|||<span data-ttu-id="6b7db-436">最初の webview の URL</span><span class="sxs-lookup"><span data-stu-id="6b7db-436">Initial webview URL</span></span>|
|`messageHandlers`|<span data-ttu-id="6b7db-437">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-437">Array of Objects</span></span>|<span data-ttu-id="6b7db-438">5 </span><span class="sxs-lookup"><span data-stu-id="6b7db-438">5</span></span>||<span data-ttu-id="6b7db-439">特定の条件が満たされたときにアプリを呼び出せるようにするハンドラーの一覧。</span><span class="sxs-lookup"><span data-stu-id="6b7db-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="6b7db-440">ドメインも、にリストされている必要があります。`validDomains`</span><span class="sxs-lookup"><span data-stu-id="6b7db-440">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="6b7db-441">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-441">String</span></span>|||<span data-ttu-id="6b7db-442">メッセージハンドラの種類。</span><span class="sxs-lookup"><span data-stu-id="6b7db-442">The type of message handler.</span></span> <span data-ttu-id="6b7db-443">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="6b7db-444">文字列 (String) の配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-444">Array of Strings</span></span>|||<span data-ttu-id="6b7db-445">リンクメッセージハンドラが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="6b7db-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="6b7db-446">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-446">Array of object</span></span>|<span data-ttu-id="6b7db-447">5 </span><span class="sxs-lookup"><span data-stu-id="6b7db-447">5</span></span>|<span data-ttu-id="6b7db-448">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-448">✔</span></span>|<span data-ttu-id="6b7db-449">コマンドが実行するパラメーターの一覧。</span><span class="sxs-lookup"><span data-stu-id="6b7db-449">The list of parameters the command takes.</span></span> <span data-ttu-id="6b7db-450">最小値: 1、最大: 5</span><span class="sxs-lookup"><span data-stu-id="6b7db-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="6b7db-451">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-451">String</span></span>|<span data-ttu-id="6b7db-452">64文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-452">64 characters</span></span>|<span data-ttu-id="6b7db-453">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-453">✔</span></span>|<span data-ttu-id="6b7db-454">クライアントに表示されるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="6b7db-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="6b7db-455">これは、ユーザー要求に含まれています。</span><span class="sxs-lookup"><span data-stu-id="6b7db-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="6b7db-456">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-456">String</span></span>|<span data-ttu-id="6b7db-457">32文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-457">32 characters</span></span>|<span data-ttu-id="6b7db-458">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-458">✔</span></span>|<span data-ttu-id="6b7db-459">パラメーターのユーザーフレンドリなタイトル。</span><span class="sxs-lookup"><span data-stu-id="6b7db-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="6b7db-460">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-460">String</span></span>|<span data-ttu-id="6b7db-461">128文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-461">128 characters</span></span>||<span data-ttu-id="6b7db-462">このパラメーターの目的を説明するユーザーフレンドリ文字列。</span><span class="sxs-lookup"><span data-stu-id="6b7db-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="6b7db-463">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-463">String</span></span>|<span data-ttu-id="6b7db-464">128文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-464">128 characters</span></span>||<span data-ttu-id="6b7db-465">の`fetchTask: true`タスクモジュールに表示されるコントロールの種類を定義します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="6b7db-466">、 `text` `textarea` `number` `date`、、、、、のいずれかの`time` `toggle``choiceset`</span><span class="sxs-lookup"><span data-stu-id="6b7db-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="6b7db-467">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-467">Array of Objects</span></span>|<span data-ttu-id="6b7db-468">10 </span><span class="sxs-lookup"><span data-stu-id="6b7db-468">10</span></span>||<span data-ttu-id="6b7db-469">の選択オプション`choiceset`。</span><span class="sxs-lookup"><span data-stu-id="6b7db-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="6b7db-470">がである`parameter.inputType`場合にのみ使用します`choiceset`</span><span class="sxs-lookup"><span data-stu-id="6b7db-470">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="6b7db-471">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-471">String</span></span>|<span data-ttu-id="6b7db-472">128</span><span class="sxs-lookup"><span data-stu-id="6b7db-472">128</span></span>||<span data-ttu-id="6b7db-473">選択肢のタイトル</span><span class="sxs-lookup"><span data-stu-id="6b7db-473">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="6b7db-474">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-474">String</span></span>|<span data-ttu-id="6b7db-475">512</span><span class="sxs-lookup"><span data-stu-id="6b7db-475">512</span></span>||<span data-ttu-id="6b7db-476">選択肢の値</span><span class="sxs-lookup"><span data-stu-id="6b7db-476">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="6b7db-477">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="6b7db-477">permissions</span></span>

<span data-ttu-id="6b7db-478">**Optional**</span><span class="sxs-lookup"><span data-stu-id="6b7db-478">**Optional**</span></span>

<span data-ttu-id="6b7db-479">アプリが要求`string`するアクセス許可を指定する配列。これにより、エンドユーザーは拡張機能の動作を知ることができます。</span><span class="sxs-lookup"><span data-stu-id="6b7db-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="6b7db-480">非排他的なオプションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="6b7db-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="6b7db-481">`identity`&emsp;ユーザー id 情報が必要</span><span class="sxs-lookup"><span data-stu-id="6b7db-481">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="6b7db-482">`messageTeamMembers`&emsp;チームメンバーに直接メッセージを送信するためのアクセス許可が必要</span><span class="sxs-lookup"><span data-stu-id="6b7db-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="6b7db-483">アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは、更新されたアプリを初めて実行したときに同意プロセスを繰り返すようになります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="6b7db-484">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="6b7db-484">devicePermissions</span></span>

<span data-ttu-id="6b7db-485">**省略可能**文字列の配列</span><span class="sxs-lookup"><span data-stu-id="6b7db-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="6b7db-486">アプリがアクセスを要求することができる、ユーザーのデバイスのネイティブ機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="6b7db-487">オプションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="6b7db-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="6b7db-488">validDomains</span><span class="sxs-lookup"><span data-stu-id="6b7db-488">validDomains</span></span>

<span data-ttu-id="6b7db-489">**省略可能**(記載個所に**必要な**場合を除く)</span><span class="sxs-lookup"><span data-stu-id="6b7db-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="6b7db-490">アプリがコンテンツを読み込むことを想定している有効なドメインの一覧。</span><span class="sxs-lookup"><span data-stu-id="6b7db-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="6b7db-491">ドメインリストには、たとえば`*.example.com`、ワイルドカードを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="6b7db-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="6b7db-492">これは、1つのドメインのセグメントに一致します。に一致`a.b.example.com`させる必要がある`*.*.example.com`場合は、を使用します。</span><span class="sxs-lookup"><span data-stu-id="6b7db-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="6b7db-493">タブ構成またはコンテンツ UI が他のドメインに移動する必要がある場合 (タブの構成に使用するものを除く)、そのドメインをここで指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="6b7db-494">ただし、アプリでサポートする id プロバイダーのドメインを含める必要は**ありません**。</span><span class="sxs-lookup"><span data-stu-id="6b7db-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="6b7db-495">たとえば、Google ID を使用して認証するには、accounts.google.com にリダイレクトする必要がありますが、に`validDomains[]`accounts.google.com を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="6b7db-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b7db-496">直接に、またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しないでください。</span><span class="sxs-lookup"><span data-stu-id="6b7db-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="6b7db-497">たとえば、は`yourapp.onmicrosoft.com`有効`*.onmicrosoft.com`ですが、有効ではありません。</span><span class="sxs-lookup"><span data-stu-id="6b7db-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="6b7db-498">Object は、型`string`のすべての要素を含む配列です。</span><span class="sxs-lookup"><span data-stu-id="6b7db-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="6b7db-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="6b7db-499">webApplicationInfo</span></span>

<span data-ttu-id="6b7db-500">**Optional**</span><span class="sxs-lookup"><span data-stu-id="6b7db-500">**Optional**</span></span>

<span data-ttu-id="6b7db-501">Aad アプリ ID とグラフ情報を指定して、ユーザーが AAD アプリにシームレスにサインインできるようにします。</span><span class="sxs-lookup"><span data-stu-id="6b7db-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="6b7db-502">名前</span><span class="sxs-lookup"><span data-stu-id="6b7db-502">Name</span></span>| <span data-ttu-id="6b7db-503">型</span><span class="sxs-lookup"><span data-stu-id="6b7db-503">Type</span></span>| <span data-ttu-id="6b7db-504">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="6b7db-504">Maximum size</span></span> | <span data-ttu-id="6b7db-505">必須</span><span class="sxs-lookup"><span data-stu-id="6b7db-505">Required</span></span> | <span data-ttu-id="6b7db-506">説明</span><span class="sxs-lookup"><span data-stu-id="6b7db-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="6b7db-507">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-507">String</span></span>|<span data-ttu-id="6b7db-508">36文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-508">36 characters</span></span>|<span data-ttu-id="6b7db-509">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-509">✔</span></span>|<span data-ttu-id="6b7db-510">アプリの AAD アプリケーション id。</span><span class="sxs-lookup"><span data-stu-id="6b7db-510">AAD application id of the app.</span></span> <span data-ttu-id="6b7db-511">この id は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="6b7db-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="6b7db-512">String</span><span class="sxs-lookup"><span data-stu-id="6b7db-512">String</span></span>|<span data-ttu-id="6b7db-513">2048 文字</span><span class="sxs-lookup"><span data-stu-id="6b7db-513">2048 characters</span></span>|<span data-ttu-id="6b7db-514">✔</span><span class="sxs-lookup"><span data-stu-id="6b7db-514">✔</span></span>|<span data-ttu-id="6b7db-515">SSO の認証トークンを取得するためのアプリのリソース url。</span><span class="sxs-lookup"><span data-stu-id="6b7db-515">Resource url of app for acquiring auth token for SSO.</span></span>|