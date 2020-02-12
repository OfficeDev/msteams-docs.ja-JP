---
title: マニフェストスキーマの参照
description: Microsoft Teams のマニフェストによってサポートされるスキーマについて説明します。
keywords: teams マニフェストスキーマ
ms.openlocfilehash: 1a1a690e6e382dcad3ceb200ec02286e8c9171f8
ms.sourcegitcommit: 060b486c38b72a3e6b63b4d617b759174082a508
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2020
ms.locfileid: "41953489"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="1015c-104">リファレンス: Microsoft Teams のマニフェストスキーマ</span><span class="sxs-lookup"><span data-stu-id="1015c-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="1015c-105">Microsoft Teams のマニフェストでは、アプリを Microsoft Teams 製品に統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1015c-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="1015c-106">マニフェストは、で[`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json)ホストされているスキーマに準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="1015c-107">以前のバージョン 1.0-1.4 もサポートされています (URL で "v1" を使用します)。</span><span class="sxs-lookup"><span data-stu-id="1015c-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="1015c-108">次のスキーマサンプルは、すべての拡張オプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="1015c-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="1015c-109">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="1015c-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
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
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
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
        }
      ],
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
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ]
}
```

<span data-ttu-id="1015c-110">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="1015c-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="1015c-111">$schema</span><span class="sxs-lookup"><span data-stu-id="1015c-111">$schema</span></span>

<span data-ttu-id="1015c-112">*省略可能。ただし、推奨* &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="1015c-112">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="1015c-113">マニフェストの JSON スキーマを参照する https://URL。</span><span class="sxs-lookup"><span data-stu-id="1015c-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="1015c-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="1015c-114">manifestVersion</span></span>

<span data-ttu-id="1015c-115">**必要な** &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="1015c-115">**Required** &ndash; String</span></span>

<span data-ttu-id="1015c-116">このマニフェストが使用しているマニフェストスキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="1015c-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="1015c-117">"1.5" である必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="1015c-118">バージョン</span><span class="sxs-lookup"><span data-stu-id="1015c-118">version</span></span>

<span data-ttu-id="1015c-119">**必要な** &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="1015c-119">**Required** &ndash; String</span></span>

<span data-ttu-id="1015c-120">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="1015c-120">The version of the specific app.</span></span> <span data-ttu-id="1015c-121">マニフェスト内の内容を更新する場合は、そのバージョンも同時にインクリメントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="1015c-122">このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。</span><span class="sxs-lookup"><span data-stu-id="1015c-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="1015c-123">このアプリがストアに送信された場合は、新しいマニフェストを再送信して再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="1015c-124">その後、このアプリのユーザーは、承認後に数時間以内に新しい更新されたマニフェストを自動的に取得します。</span><span class="sxs-lookup"><span data-stu-id="1015c-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="1015c-125">アプリによって要求されたアクセス許可が変更された場合、ユーザーはアプリをアップグレードして再同意するように求められます。</span><span class="sxs-lookup"><span data-stu-id="1015c-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="1015c-126">このバージョンの文字列は、 [semver](http://semver.org/)標準 (メジャー) に従う必要があります。間隔.パッチ)。</span><span class="sxs-lookup"><span data-stu-id="1015c-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="1015c-127">id</span><span class="sxs-lookup"><span data-stu-id="1015c-127">id</span></span>

<span data-ttu-id="1015c-128">**必要な** &ndash; Microsoft アプリ ID</span><span class="sxs-lookup"><span data-stu-id="1015c-128">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="1015c-129">このアプリの一意の Microsoft 生成識別子。</span><span class="sxs-lookup"><span data-stu-id="1015c-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="1015c-130">Microsoft Bot フレームワークを介して bot を登録した場合、またはタブの web アプリが Microsoft によって既にサインインしている場合は、既に ID があるので、ここで入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="1015c-131">それ以外の場合は、Microsoft アプリケーション登録ポータル ([My Applications](https://apps.dev.microsoft.com)) で新しい ID を生成し、ここで入力してから、bot を追加するときにそれを再利用する必要があります。注: AppSource で既存のアプリに更新を送信する場合は、マニフェスト内の ID を変更しないでください。</span><span class="sxs-lookup"><span data-stu-id="1015c-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="packagename"></a><span data-ttu-id="1015c-132">packageName</span><span class="sxs-lookup"><span data-stu-id="1015c-132">packageName</span></span>

<span data-ttu-id="1015c-133">**必要な** &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="1015c-133">**Required** &ndash; String</span></span>

<span data-ttu-id="1015c-134">逆引きドメイン表記でのこのアプリの一意識別子。たとえば、例のようになります。</span><span class="sxs-lookup"><span data-stu-id="1015c-134">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="1015c-135">developer</span><span class="sxs-lookup"><span data-stu-id="1015c-135">developer</span></span>

<span data-ttu-id="1015c-136">**Required**</span><span class="sxs-lookup"><span data-stu-id="1015c-136">**Required**</span></span>

<span data-ttu-id="1015c-137">会社に関する情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="1015c-137">Specifies information about your company.</span></span> <span data-ttu-id="1015c-138">AppSource (旧称 Office ストア) に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="1015c-139">追加情報については、[発行に関するガイドライン](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1015c-139">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="1015c-140">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-140">Name</span></span>| <span data-ttu-id="1015c-141">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-141">Maximum size</span></span> | <span data-ttu-id="1015c-142">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-142">Required</span></span> | <span data-ttu-id="1015c-143">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="1015c-144">32文字</span><span class="sxs-lookup"><span data-stu-id="1015c-144">32 characters</span></span>|<span data-ttu-id="1015c-145">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-145">✔</span></span>|<span data-ttu-id="1015c-146">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="1015c-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="1015c-147">2048 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-147">2048 characters</span></span>|<span data-ttu-id="1015c-148">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-148">✔</span></span>|<span data-ttu-id="1015c-149">開発者の web サイトへの https://URL。</span><span class="sxs-lookup"><span data-stu-id="1015c-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="1015c-150">このリンクは、ユーザーを会社または製品固有のランディングページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="1015c-151">2048 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-151">2048 characters</span></span>|<span data-ttu-id="1015c-152">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-152">✔</span></span>|<span data-ttu-id="1015c-153">開発者のプライバシーポリシーへの https://URL。</span><span class="sxs-lookup"><span data-stu-id="1015c-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="1015c-154">2048 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-154">2048 characters</span></span>|<span data-ttu-id="1015c-155">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-155">✔</span></span>|<span data-ttu-id="1015c-156">開発者の使用条件への https://URL。</span><span class="sxs-lookup"><span data-stu-id="1015c-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="1015c-157">10文字</span><span class="sxs-lookup"><span data-stu-id="1015c-157">10 characters</span></span>| |<span data-ttu-id="1015c-158">**省略可能**アプリを構築するパートナー組織を識別する Microsoft パートナーのネットワーク ID。</span><span class="sxs-lookup"><span data-stu-id="1015c-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="1015c-159">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="1015c-159">localizationInfo</span></span>

<span data-ttu-id="1015c-160">**Optional**</span><span class="sxs-lookup"><span data-stu-id="1015c-160">**Optional**</span></span>

<span data-ttu-id="1015c-161">既定の言語の指定、および追加の言語ファイルへのポインターを許可します。</span><span class="sxs-lookup"><span data-stu-id="1015c-161">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="1015c-162">「[ローカライズ](~/concepts/build-and-test/apps-localization.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1015c-162">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="1015c-163">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-163">Name</span></span>| <span data-ttu-id="1015c-164">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-164">Maximum size</span></span> | <span data-ttu-id="1015c-165">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-165">Required</span></span> | <span data-ttu-id="1015c-166">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-166">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="1015c-167">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-167">✔</span></span>|<span data-ttu-id="1015c-168">このトップレベルマニフェストファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="1015c-168">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="1015c-169">localizationInfo. additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="1015c-169">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="1015c-170">追加の言語の翻訳を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="1015c-170">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="1015c-171">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-171">Name</span></span>| <span data-ttu-id="1015c-172">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-172">Maximum size</span></span> | <span data-ttu-id="1015c-173">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-173">Required</span></span> | <span data-ttu-id="1015c-174">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-174">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="1015c-175">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-175">✔</span></span>|<span data-ttu-id="1015c-176">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="1015c-176">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="1015c-177">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-177">✔</span></span>|<span data-ttu-id="1015c-178">翻訳された文字列を含む json ファイルへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="1015c-178">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="1015c-179">name</span><span class="sxs-lookup"><span data-stu-id="1015c-179">name</span></span>

<span data-ttu-id="1015c-180">**Required**</span><span class="sxs-lookup"><span data-stu-id="1015c-180">**Required**</span></span>

<span data-ttu-id="1015c-181">Teams でユーザーに表示されるアプリの動作の名前です。</span><span class="sxs-lookup"><span data-stu-id="1015c-181">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="1015c-182">AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-182">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="1015c-183">との`short`値を`full`同じにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="1015c-183">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="1015c-184">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-184">Name</span></span>| <span data-ttu-id="1015c-185">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-185">Maximum size</span></span> | <span data-ttu-id="1015c-186">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-186">Required</span></span> | <span data-ttu-id="1015c-187">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-187">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="1015c-188">30 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-188">30 characters</span></span>|<span data-ttu-id="1015c-189">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-189">✔</span></span>|<span data-ttu-id="1015c-190">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="1015c-190">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="1015c-191">100 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-191">100 characters</span></span>||<span data-ttu-id="1015c-192">アプリの完全な名前。アプリの完全な名前が30文字を超えている場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="1015c-192">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="1015c-193">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-193">description</span></span>

<span data-ttu-id="1015c-194">**Required**</span><span class="sxs-lookup"><span data-stu-id="1015c-194">**Required**</span></span>

<span data-ttu-id="1015c-195">ユーザーに対してアプリを記述します。</span><span class="sxs-lookup"><span data-stu-id="1015c-195">Describes your app to users.</span></span> <span data-ttu-id="1015c-196">AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-196">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="1015c-197">説明に正確に表示されていることを確認し、お客様が快適な動作を理解するのに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="1015c-197">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="1015c-198">また、外部アカウントが使用するために必要な場合は、詳細な説明にも注意してください。</span><span class="sxs-lookup"><span data-stu-id="1015c-198">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="1015c-199">との`short`値を`full`同じにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="1015c-199">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="1015c-200">短い説明を長い説明の中で繰り返すことはできません。他のアプリ名を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="1015c-200">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="1015c-201">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-201">Name</span></span>| <span data-ttu-id="1015c-202">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-202">Maximum size</span></span> | <span data-ttu-id="1015c-203">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-203">Required</span></span> | <span data-ttu-id="1015c-204">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-204">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="1015c-205">80文字</span><span class="sxs-lookup"><span data-stu-id="1015c-205">80 characters</span></span>|<span data-ttu-id="1015c-206">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-206">✔</span></span>|<span data-ttu-id="1015c-207">スペースが制限されている場合に使用する、アプリの使用状況の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="1015c-207">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="1015c-208">4000文字</span><span class="sxs-lookup"><span data-stu-id="1015c-208">4000 characters</span></span>|<span data-ttu-id="1015c-209">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-209">✔</span></span>|<span data-ttu-id="1015c-210">アプリの詳細な説明。</span><span class="sxs-lookup"><span data-stu-id="1015c-210">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="1015c-211">アイコン</span><span class="sxs-lookup"><span data-stu-id="1015c-211">icons</span></span>

<span data-ttu-id="1015c-212">**Required**</span><span class="sxs-lookup"><span data-stu-id="1015c-212">**Required**</span></span>

<span data-ttu-id="1015c-213">Teams アプリ内で使用されるアイコン。</span><span class="sxs-lookup"><span data-stu-id="1015c-213">Icons used within the Teams app.</span></span> <span data-ttu-id="1015c-214">アイコンファイルは、アップロードパッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-214">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="1015c-215">詳細については、「[アイコン](~/concepts/build-and-test/apps-package.md#icons)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1015c-215">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="1015c-216">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-216">Name</span></span>| <span data-ttu-id="1015c-217">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-217">Maximum size</span></span> | <span data-ttu-id="1015c-218">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-218">Required</span></span> | <span data-ttu-id="1015c-219">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-219">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="1015c-220">2048 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-220">2048 characters</span></span>|<span data-ttu-id="1015c-221">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-221">✔</span></span>|<span data-ttu-id="1015c-222">透明な32x32 の PNG アウトラインアイコンへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="1015c-222">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="1015c-223">2048 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-223">2048 characters</span></span>|<span data-ttu-id="1015c-224">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-224">✔</span></span>|<span data-ttu-id="1015c-225">フルカラー 192x192 PNG アイコンへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="1015c-225">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="1015c-226">アクセントカラー</span><span class="sxs-lookup"><span data-stu-id="1015c-226">accentColor</span></span>

<span data-ttu-id="1015c-227">**必要な** &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="1015c-227">**Required** &ndash; String</span></span>

<span data-ttu-id="1015c-228">とと組み合わせてアウトラインアイコンの背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="1015c-228">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="1015c-229">この値は、' # ' で始まる有効な HTML カラーコードである必要`#4464ee`があります (例:)。</span><span class="sxs-lookup"><span data-stu-id="1015c-229">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="1015c-230">の各タブ</span><span class="sxs-lookup"><span data-stu-id="1015c-230">configurableTabs</span></span>

<span data-ttu-id="1015c-231">**Optional**</span><span class="sxs-lookup"><span data-stu-id="1015c-231">**Optional**</span></span>

<span data-ttu-id="1015c-232">アプリの機能に、追加の構成を必要とするチームチャネルのタブがある場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="1015c-232">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="1015c-233">構成可能なタブは teams スコープでのみサポートされており、現在、アプリごとに1つのタブのみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1015c-233">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="1015c-234">Object は、型`object`のすべての要素を含む配列です。</span><span class="sxs-lookup"><span data-stu-id="1015c-234">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="1015c-235">このブロックは、構成可能なチャネルのタブソリューションを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="1015c-235">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="1015c-236">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-236">Name</span></span>| <span data-ttu-id="1015c-237">型</span><span class="sxs-lookup"><span data-stu-id="1015c-237">Type</span></span>| <span data-ttu-id="1015c-238">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-238">Maximum size</span></span> | <span data-ttu-id="1015c-239">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-239">Required</span></span> | <span data-ttu-id="1015c-240">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-240">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="1015c-241">String</span><span class="sxs-lookup"><span data-stu-id="1015c-241">String</span></span>|<span data-ttu-id="1015c-242">2048 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-242">2048 characters</span></span>|<span data-ttu-id="1015c-243">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-243">✔</span></span>|<span data-ttu-id="1015c-244">タブを構成するときに使用する https://URL。</span><span class="sxs-lookup"><span data-stu-id="1015c-244">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="1015c-245">ブール値</span><span class="sxs-lookup"><span data-stu-id="1015c-245">Boolean</span></span>|||<span data-ttu-id="1015c-246">作成後にタブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="1015c-246">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="1015c-247">限り`true`</span><span class="sxs-lookup"><span data-stu-id="1015c-247">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="1015c-248">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="1015c-248">Array of enum</span></span>|<span data-ttu-id="1015c-249">1 </span><span class="sxs-lookup"><span data-stu-id="1015c-249">1</span></span>|<span data-ttu-id="1015c-250">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-250">✔</span></span>|<span data-ttu-id="1015c-251">現在、構成可能なタブで`team`は`groupchat` 、およびスコープのみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1015c-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="1015c-252">String</span><span class="sxs-lookup"><span data-stu-id="1015c-252">String</span></span>|<span data-ttu-id="1015c-253">2048</span><span class="sxs-lookup"><span data-stu-id="1015c-253">2048</span></span>||<span data-ttu-id="1015c-254">SharePoint で使用するタブプレビュー画像への相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="1015c-254">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="1015c-255">サイズ1024x768。</span><span class="sxs-lookup"><span data-stu-id="1015c-255">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="1015c-256">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="1015c-256">Array of enum</span></span>|<span data-ttu-id="1015c-257">1 </span><span class="sxs-lookup"><span data-stu-id="1015c-257">1</span></span>||<span data-ttu-id="1015c-258">SharePoint でどのようにタブを使用できるようにするかを定義します。</span><span class="sxs-lookup"><span data-stu-id="1015c-258">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="1015c-259">オプション`sharePointFullPage`と`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="1015c-259">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="1015c-260">staticTabs</span><span class="sxs-lookup"><span data-stu-id="1015c-260">staticTabs</span></span>

<span data-ttu-id="1015c-261">**Optional**</span><span class="sxs-lookup"><span data-stu-id="1015c-261">**Optional**</span></span>

<span data-ttu-id="1015c-262">ユーザーが手動で追加せずに、既定で "固定" できるタブのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="1015c-262">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="1015c-263">スコープ内で`personal`宣言されている静的タブは、常にアプリの個人の環境に固定されます。</span><span class="sxs-lookup"><span data-stu-id="1015c-263">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="1015c-264">`team`スコープ内で宣言されている静的タブは現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="1015c-264">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="1015c-265">Object は、型`object`のすべての要素を含む配列 (最大16個の要素) です。</span><span class="sxs-lookup"><span data-stu-id="1015c-265">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="1015c-266">このブロックは、静的なタブソリューションを提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="1015c-266">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="1015c-267">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-267">Name</span></span>| <span data-ttu-id="1015c-268">型</span><span class="sxs-lookup"><span data-stu-id="1015c-268">Type</span></span>| <span data-ttu-id="1015c-269">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-269">Maximum size</span></span> | <span data-ttu-id="1015c-270">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-270">Required</span></span> | <span data-ttu-id="1015c-271">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-271">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="1015c-272">String</span><span class="sxs-lookup"><span data-stu-id="1015c-272">String</span></span>|<span data-ttu-id="1015c-273">64 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-273">64 characters</span></span>|<span data-ttu-id="1015c-274">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-274">✔</span></span>|<span data-ttu-id="1015c-275">タブに表示されるエンティティの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="1015c-275">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="1015c-276">String</span><span class="sxs-lookup"><span data-stu-id="1015c-276">String</span></span>|<span data-ttu-id="1015c-277">128文字</span><span class="sxs-lookup"><span data-stu-id="1015c-277">128 characters</span></span>|<span data-ttu-id="1015c-278">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-278">✔</span></span>|<span data-ttu-id="1015c-279">チャネルインターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="1015c-279">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="1015c-280">String</span><span class="sxs-lookup"><span data-stu-id="1015c-280">String</span></span>|<span data-ttu-id="1015c-281">2048 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-281">2048 characters</span></span>|<span data-ttu-id="1015c-282">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-282">✔</span></span>|<span data-ttu-id="1015c-283">Teams キャンバスに表示されるエンティティ UI をポイントする https://URL。</span><span class="sxs-lookup"><span data-stu-id="1015c-283">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="1015c-284">String</span><span class="sxs-lookup"><span data-stu-id="1015c-284">String</span></span>|<span data-ttu-id="1015c-285">2048 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-285">2048 characters</span></span>||<span data-ttu-id="1015c-286">ユーザーがブラウザーで表示をポイントしたかどうかを示す https://URL。</span><span class="sxs-lookup"><span data-stu-id="1015c-286">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="1015c-287">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="1015c-287">Array of enum</span></span>|<span data-ttu-id="1015c-288">1 </span><span class="sxs-lookup"><span data-stu-id="1015c-288">1</span></span>|<span data-ttu-id="1015c-289">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-289">✔</span></span>|<span data-ttu-id="1015c-290">現時点では、静的タブで`personal`はスコープのみがサポートされます。つまり、個人の利便性の一環としてのみプロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="1015c-290">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

> [!NOTE]
> <span data-ttu-id="1015c-291">関連するコンテンツを表示したり、認証フローを開始したりするために、タブにコンテキスト依存情報が必要な場合は、「 [Microsoft Teams のコンテキストを取得する」タブ](../../tabs/how-to/access-teams-context.md)を*参照してください*。</span><span class="sxs-lookup"><span data-stu-id="1015c-291">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="1015c-292">bot</span><span class="sxs-lookup"><span data-stu-id="1015c-292">bots</span></span>

<span data-ttu-id="1015c-293">**Optional**</span><span class="sxs-lookup"><span data-stu-id="1015c-293">**Optional**</span></span>

<span data-ttu-id="1015c-294">Bot ソリューションと、既定のコマンドプロパティなどのオプション情報を定義します。</span><span class="sxs-lookup"><span data-stu-id="1015c-294">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="1015c-295">オブジェクトが配列の場合 (現時点では1つ&mdash;の要素のうちの最大値は1つですが、現在は`object`アプリごとに1つの bot のみが許可されます)、型のすべての要素を使用します</span><span class="sxs-lookup"><span data-stu-id="1015c-295">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="1015c-296">このブロックは、bot の環境を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="1015c-296">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="1015c-297">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-297">Name</span></span>| <span data-ttu-id="1015c-298">型</span><span class="sxs-lookup"><span data-stu-id="1015c-298">Type</span></span>| <span data-ttu-id="1015c-299">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-299">Maximum size</span></span> | <span data-ttu-id="1015c-300">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-300">Required</span></span> | <span data-ttu-id="1015c-301">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-301">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="1015c-302">String</span><span class="sxs-lookup"><span data-stu-id="1015c-302">String</span></span>|<span data-ttu-id="1015c-303">64 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-303">64 characters</span></span>|<span data-ttu-id="1015c-304">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-304">✔</span></span>|<span data-ttu-id="1015c-305">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="1015c-305">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="1015c-306">これは、アプリの全体的な[ID](#id)と同じである場合もあります。</span><span class="sxs-lookup"><span data-stu-id="1015c-306">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="1015c-307">ブール値</span><span class="sxs-lookup"><span data-stu-id="1015c-307">Boolean</span></span>|||<span data-ttu-id="1015c-308">ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。</span><span class="sxs-lookup"><span data-stu-id="1015c-308">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="1015c-309">限り`false`</span><span class="sxs-lookup"><span data-stu-id="1015c-309">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="1015c-310">ブール値</span><span class="sxs-lookup"><span data-stu-id="1015c-310">Boolean</span></span>|||<span data-ttu-id="1015c-311">ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="1015c-311">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="1015c-312">限り`false`</span><span class="sxs-lookup"><span data-stu-id="1015c-312">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="1015c-313">Boolean</span><span class="sxs-lookup"><span data-stu-id="1015c-313">Boolean</span></span>|||<span data-ttu-id="1015c-314">パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="1015c-314">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="1015c-315">限り`false`</span><span class="sxs-lookup"><span data-stu-id="1015c-315">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="1015c-316">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="1015c-316">Array of enum</span></span>|<span data-ttu-id="1015c-317">3 </span><span class="sxs-lookup"><span data-stu-id="1015c-317">3</span></span>|<span data-ttu-id="1015c-318">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-318">✔</span></span>|<span data-ttu-id="1015c-319">ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。</span><span class="sxs-lookup"><span data-stu-id="1015c-319">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="1015c-320">これらのオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="1015c-320">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="1015c-321">bot リスト</span><span class="sxs-lookup"><span data-stu-id="1015c-321">bots.commandLists</span></span>

<span data-ttu-id="1015c-322">Bot がユーザーに推奨できるコマンドのオプションの一覧。</span><span class="sxs-lookup"><span data-stu-id="1015c-322">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="1015c-323">Object は、型`object`のすべての要素を含む配列 (最大2つの要素) です。bot がサポートするスコープごとに個別のコマンドリストを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-323">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="1015c-324">詳細については、「 [Bot メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1015c-324">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="1015c-325">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-325">Name</span></span>| <span data-ttu-id="1015c-326">型</span><span class="sxs-lookup"><span data-stu-id="1015c-326">Type</span></span>| <span data-ttu-id="1015c-327">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-327">Maximum size</span></span> | <span data-ttu-id="1015c-328">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-328">Required</span></span> | <span data-ttu-id="1015c-329">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-329">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="1015c-330">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="1015c-330">array of enum</span></span>|<span data-ttu-id="1015c-331">3 </span><span class="sxs-lookup"><span data-stu-id="1015c-331">3</span></span>|<span data-ttu-id="1015c-332">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-332">✔</span></span>|<span data-ttu-id="1015c-333">コマンド リストが有効なスコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="1015c-333">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="1015c-334">`team`、`personal`、`groupchat` の中から選択できます。</span><span class="sxs-lookup"><span data-stu-id="1015c-334">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="1015c-335">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="1015c-335">array of objects</span></span>|<span data-ttu-id="1015c-336">10 </span><span class="sxs-lookup"><span data-stu-id="1015c-336">10</span></span>|<span data-ttu-id="1015c-337">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-337">✔</span></span>|<span data-ttu-id="1015c-338">ボットがサポートするコマンドの配列:</span><span class="sxs-lookup"><span data-stu-id="1015c-338">An array of commands the bot supports:</span></span><br><span data-ttu-id="1015c-339">`title`: ボット コマンドの名前 (文字列、32)</span><span class="sxs-lookup"><span data-stu-id="1015c-339">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="1015c-340">`description`: コマンドの構文およびその構文の引数
の簡単な説明または例 (文字列、128)</span><span class="sxs-lookup"><span data-stu-id="1015c-340">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="1015c-341">コネクタ</span><span class="sxs-lookup"><span data-stu-id="1015c-341">connectors</span></span>

<span data-ttu-id="1015c-342">**Optional**</span><span class="sxs-lookup"><span data-stu-id="1015c-342">**Optional**</span></span>

<span data-ttu-id="1015c-343">ブロック`connectors`は、アプリの Office 365 コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="1015c-343">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="1015c-344">Object は、type `object`のすべての要素を含む配列 (最大1つの要素) です。</span><span class="sxs-lookup"><span data-stu-id="1015c-344">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="1015c-345">このブロックは、コネクタを提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="1015c-345">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="1015c-346">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-346">Name</span></span>| <span data-ttu-id="1015c-347">型</span><span class="sxs-lookup"><span data-stu-id="1015c-347">Type</span></span>| <span data-ttu-id="1015c-348">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-348">Maximum size</span></span> | <span data-ttu-id="1015c-349">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-349">Required</span></span> | <span data-ttu-id="1015c-350">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-350">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="1015c-351">String</span><span class="sxs-lookup"><span data-stu-id="1015c-351">String</span></span>|<span data-ttu-id="1015c-352">2048 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-352">2048 characters</span></span>|<span data-ttu-id="1015c-353">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-353">✔</span></span>|<span data-ttu-id="1015c-354">コネクタを構成するときに使用する https://URL。</span><span class="sxs-lookup"><span data-stu-id="1015c-354">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="1015c-355">String</span><span class="sxs-lookup"><span data-stu-id="1015c-355">String</span></span>|<span data-ttu-id="1015c-356">64 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-356">64 characters</span></span>|<span data-ttu-id="1015c-357">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-357">✔</span></span>|<span data-ttu-id="1015c-358">コネクタ[開発者ダッシュボード](https://aka.ms/connectorsdashboard)の ID と一致するコネクタの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="1015c-358">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="1015c-359">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="1015c-359">Array of enum</span></span>|<span data-ttu-id="1015c-360">1 </span><span class="sxs-lookup"><span data-stu-id="1015c-360">1</span></span>|<span data-ttu-id="1015c-361">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-361">✔</span></span>|<span data-ttu-id="1015c-362">コネクタが内`team`のチャネルのコンテキストで、または個別のユーザー単独 (`personal`) にスコープ設定された環境での動作を提供するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="1015c-362">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="1015c-363">現時点では、 `team`範囲のみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1015c-363">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="1015c-364">この機能</span><span class="sxs-lookup"><span data-stu-id="1015c-364">composeExtensions</span></span>

<span data-ttu-id="1015c-365">**Optional**</span><span class="sxs-lookup"><span data-stu-id="1015c-365">**Optional**</span></span>

<span data-ttu-id="1015c-366">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="1015c-366">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="1015c-367">この機能の名前は、2017年11月に「[作成] 拡張機能」から「messaging extension」に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は同じままです。</span><span class="sxs-lookup"><span data-stu-id="1015c-367">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="1015c-368">Object は、type `object`のすべての要素を含む配列 (最大1つの要素) です。</span><span class="sxs-lookup"><span data-stu-id="1015c-368">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="1015c-369">このブロックは、メッセージング拡張機能を提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="1015c-369">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="1015c-370">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-370">Name</span></span>| <span data-ttu-id="1015c-371">型</span><span class="sxs-lookup"><span data-stu-id="1015c-371">Type</span></span> | <span data-ttu-id="1015c-372">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-372">Maximum Size</span></span> | <span data-ttu-id="1015c-373">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-373">Required</span></span> | <span data-ttu-id="1015c-374">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-374">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="1015c-375">String</span><span class="sxs-lookup"><span data-stu-id="1015c-375">String</span></span>|<span data-ttu-id="1015c-376">64</span><span class="sxs-lookup"><span data-stu-id="1015c-376">64</span></span>|<span data-ttu-id="1015c-377">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-377">✔</span></span>|<span data-ttu-id="1015c-378">Bot フレームワークに登録されているメッセージング拡張機能をバックアップする bot の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="1015c-378">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="1015c-379">これは、アプリの全体的な ID と同じである場合もあります。</span><span class="sxs-lookup"><span data-stu-id="1015c-379">This may well be the same as the overall App ID.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="1015c-380">ブール値</span><span class="sxs-lookup"><span data-stu-id="1015c-380">Boolean</span></span>|||<span data-ttu-id="1015c-381">メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="1015c-381">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="1015c-382">既定値は `false` です。</span><span class="sxs-lookup"><span data-stu-id="1015c-382">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="1015c-383">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="1015c-383">Array of object</span></span>|<span data-ttu-id="1015c-384">10 </span><span class="sxs-lookup"><span data-stu-id="1015c-384">10</span></span>|<span data-ttu-id="1015c-385">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-385">✔</span></span>|<span data-ttu-id="1015c-386">メッセージング拡張機能がサポートするコマンドの配列</span><span class="sxs-lookup"><span data-stu-id="1015c-386">Array of commands the messaging extension supports</span></span>|
|`messageHandlers`|<span data-ttu-id="1015c-387">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="1015c-387">Array of Objects</span></span>|<span data-ttu-id="1015c-388">5 </span><span class="sxs-lookup"><span data-stu-id="1015c-388">5</span></span>||<span data-ttu-id="1015c-389">特定の条件が満たされたときにアプリを呼び出せるようにするハンドラーの一覧。</span><span class="sxs-lookup"><span data-stu-id="1015c-389">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="1015c-390">ドメインも、にリストされている必要があります。`validDomains`</span><span class="sxs-lookup"><span data-stu-id="1015c-390">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="1015c-391">String</span><span class="sxs-lookup"><span data-stu-id="1015c-391">String</span></span>|||<span data-ttu-id="1015c-392">メッセージハンドラの種類。</span><span class="sxs-lookup"><span data-stu-id="1015c-392">The type of message handler.</span></span> <span data-ttu-id="1015c-393">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-393">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="1015c-394">文字列 (String) の配列</span><span class="sxs-lookup"><span data-stu-id="1015c-394">Array of Strings</span></span>|||<span data-ttu-id="1015c-395">リンクメッセージハンドラが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="1015c-395">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="1015c-396">このコマンドの機能</span><span class="sxs-lookup"><span data-stu-id="1015c-396">composeExtensions.commands</span></span>

<span data-ttu-id="1015c-397">メッセージング拡張機能は、1つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-397">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="1015c-398">各コマンドは、Microsoft Teams に UI ベースのエントリポイントからの潜在的な操作として表示されます。</span><span class="sxs-lookup"><span data-stu-id="1015c-398">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="1015c-399">最大10個のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="1015c-399">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="1015c-400">各コマンド項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="1015c-400">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="1015c-401">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-401">Name</span></span>| <span data-ttu-id="1015c-402">型</span><span class="sxs-lookup"><span data-stu-id="1015c-402">Type</span></span>| <span data-ttu-id="1015c-403">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-403">Maximum size</span></span> | <span data-ttu-id="1015c-404">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-404">Required</span></span> | <span data-ttu-id="1015c-405">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-405">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="1015c-406">String</span><span class="sxs-lookup"><span data-stu-id="1015c-406">String</span></span>|<span data-ttu-id="1015c-407">64 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-407">64 characters</span></span>|<span data-ttu-id="1015c-408">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-408">✔</span></span>|<span data-ttu-id="1015c-409">コマンドの ID</span><span class="sxs-lookup"><span data-stu-id="1015c-409">The ID for the command</span></span>|
|`type`|<span data-ttu-id="1015c-410">String</span><span class="sxs-lookup"><span data-stu-id="1015c-410">String</span></span>|<span data-ttu-id="1015c-411">64 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-411">64 characters</span></span>||<span data-ttu-id="1015c-412">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="1015c-412">Type of the command.</span></span> <span data-ttu-id="1015c-413">または`query` `action`のいずれかです。</span><span class="sxs-lookup"><span data-stu-id="1015c-413">One of `query` or `action`.</span></span> <span data-ttu-id="1015c-414">限り`query`</span><span class="sxs-lookup"><span data-stu-id="1015c-414">Default: `query`</span></span>|
|`title`|<span data-ttu-id="1015c-415">String</span><span class="sxs-lookup"><span data-stu-id="1015c-415">String</span></span>|<span data-ttu-id="1015c-416">32文字</span><span class="sxs-lookup"><span data-stu-id="1015c-416">32 characters</span></span>|<span data-ttu-id="1015c-417">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-417">✔</span></span>|<span data-ttu-id="1015c-418">ユーザーフレンドリなコマンド名</span><span class="sxs-lookup"><span data-stu-id="1015c-418">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="1015c-419">String</span><span class="sxs-lookup"><span data-stu-id="1015c-419">String</span></span>|<span data-ttu-id="1015c-420">128文字</span><span class="sxs-lookup"><span data-stu-id="1015c-420">128 characters</span></span>||<span data-ttu-id="1015c-421">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="1015c-421">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="1015c-422">ブール値</span><span class="sxs-lookup"><span data-stu-id="1015c-422">Boolean</span></span>|||<span data-ttu-id="1015c-423">パラメーターを指定せずにコマンドを最初に実行する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="1015c-423">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="1015c-424">限り`false`</span><span class="sxs-lookup"><span data-stu-id="1015c-424">Default: `false`</span></span>|
|`context`|<span data-ttu-id="1015c-425">文字列 (String) の配列</span><span class="sxs-lookup"><span data-stu-id="1015c-425">Array of Strings</span></span>|<span data-ttu-id="1015c-426">3 </span><span class="sxs-lookup"><span data-stu-id="1015c-426">3</span></span>||<span data-ttu-id="1015c-427">メッセージの内線番号をから呼び出すことができる場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="1015c-427">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="1015c-428">、 `commandBox`、 `message`の`compose`任意の組み合わせ。</span><span class="sxs-lookup"><span data-stu-id="1015c-428">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="1015c-429">既定値は`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="1015c-429">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="1015c-430">ブール値</span><span class="sxs-lookup"><span data-stu-id="1015c-430">Boolean</span></span>|||<span data-ttu-id="1015c-431">タスクモジュールを動的に取得する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="1015c-431">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="1015c-432">オブジェクト</span><span class="sxs-lookup"><span data-stu-id="1015c-432">Object</span></span>|||<span data-ttu-id="1015c-433">メッセージ拡張コマンドの使用時にプリロードするタスクモジュールを指定する</span><span class="sxs-lookup"><span data-stu-id="1015c-433">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="1015c-434">String</span><span class="sxs-lookup"><span data-stu-id="1015c-434">String</span></span>|<span data-ttu-id="1015c-435">64</span><span class="sxs-lookup"><span data-stu-id="1015c-435">64</span></span>||<span data-ttu-id="1015c-436">最初のダイアログのタイトル</span><span class="sxs-lookup"><span data-stu-id="1015c-436">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="1015c-437">String</span><span class="sxs-lookup"><span data-stu-id="1015c-437">String</span></span>|||<span data-ttu-id="1015c-438">ダイアログの幅。ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="1015c-438">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="1015c-439">String</span><span class="sxs-lookup"><span data-stu-id="1015c-439">String</span></span>|||<span data-ttu-id="1015c-440">ダイアログの高さ-ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="1015c-440">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="1015c-441">String</span><span class="sxs-lookup"><span data-stu-id="1015c-441">String</span></span>|||<span data-ttu-id="1015c-442">最初の webview の URL</span><span class="sxs-lookup"><span data-stu-id="1015c-442">Initial webview URL</span></span>|
|`parameters`|<span data-ttu-id="1015c-443">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="1015c-443">Array of object</span></span>|<span data-ttu-id="1015c-444">5 </span><span class="sxs-lookup"><span data-stu-id="1015c-444">5</span></span>|<span data-ttu-id="1015c-445">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-445">✔</span></span>|<span data-ttu-id="1015c-446">コマンドが実行するパラメーターの一覧。</span><span class="sxs-lookup"><span data-stu-id="1015c-446">The list of parameters the command takes.</span></span> <span data-ttu-id="1015c-447">最小値: 1、最大: 5</span><span class="sxs-lookup"><span data-stu-id="1015c-447">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="1015c-448">String</span><span class="sxs-lookup"><span data-stu-id="1015c-448">String</span></span>|<span data-ttu-id="1015c-449">64 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-449">64 characters</span></span>|<span data-ttu-id="1015c-450">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-450">✔</span></span>|<span data-ttu-id="1015c-451">クライアントに表示されるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="1015c-451">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="1015c-452">これは、ユーザー要求に含まれています。</span><span class="sxs-lookup"><span data-stu-id="1015c-452">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="1015c-453">String</span><span class="sxs-lookup"><span data-stu-id="1015c-453">String</span></span>|<span data-ttu-id="1015c-454">32文字</span><span class="sxs-lookup"><span data-stu-id="1015c-454">32 characters</span></span>|<span data-ttu-id="1015c-455">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-455">✔</span></span>|<span data-ttu-id="1015c-456">パラメーターのユーザーフレンドリなタイトル。</span><span class="sxs-lookup"><span data-stu-id="1015c-456">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="1015c-457">String</span><span class="sxs-lookup"><span data-stu-id="1015c-457">String</span></span>|<span data-ttu-id="1015c-458">128文字</span><span class="sxs-lookup"><span data-stu-id="1015c-458">128 characters</span></span>||<span data-ttu-id="1015c-459">このパラメーターの目的を説明するユーザーフレンドリ文字列。</span><span class="sxs-lookup"><span data-stu-id="1015c-459">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="1015c-460">String</span><span class="sxs-lookup"><span data-stu-id="1015c-460">String</span></span>|<span data-ttu-id="1015c-461">128文字</span><span class="sxs-lookup"><span data-stu-id="1015c-461">128 characters</span></span>||<span data-ttu-id="1015c-462">の`fetchTask: true`タスクモジュールに表示されるコントロールの種類を定義します。</span><span class="sxs-lookup"><span data-stu-id="1015c-462">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="1015c-463">、 `text` `textarea` `number` `date`、、、、、のいずれかの`time` `toggle``choiceset`</span><span class="sxs-lookup"><span data-stu-id="1015c-463">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="1015c-464">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="1015c-464">Array of Objects</span></span>|<span data-ttu-id="1015c-465">10 </span><span class="sxs-lookup"><span data-stu-id="1015c-465">10</span></span>||<span data-ttu-id="1015c-466">の選択オプション`choiceset`。</span><span class="sxs-lookup"><span data-stu-id="1015c-466">The choice options for the `choiceset`.</span></span> <span data-ttu-id="1015c-467">がである`parameter.inputType`場合にのみ使用します`choiceset`</span><span class="sxs-lookup"><span data-stu-id="1015c-467">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="1015c-468">String</span><span class="sxs-lookup"><span data-stu-id="1015c-468">String</span></span>|<span data-ttu-id="1015c-469">128</span><span class="sxs-lookup"><span data-stu-id="1015c-469">128</span></span>||<span data-ttu-id="1015c-470">選択肢のタイトル</span><span class="sxs-lookup"><span data-stu-id="1015c-470">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="1015c-471">String</span><span class="sxs-lookup"><span data-stu-id="1015c-471">String</span></span>|<span data-ttu-id="1015c-472">512</span><span class="sxs-lookup"><span data-stu-id="1015c-472">512</span></span>||<span data-ttu-id="1015c-473">選択肢の値</span><span class="sxs-lookup"><span data-stu-id="1015c-473">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="1015c-474">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="1015c-474">permissions</span></span>

<span data-ttu-id="1015c-475">**Optional**</span><span class="sxs-lookup"><span data-stu-id="1015c-475">**Optional**</span></span>

<span data-ttu-id="1015c-476">アプリが要求`string`するアクセス許可を指定する配列。これにより、エンドユーザーは拡張機能の動作を知ることができます。</span><span class="sxs-lookup"><span data-stu-id="1015c-476">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="1015c-477">非排他的なオプションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="1015c-477">The following options are non-exclusive:</span></span>

* <span data-ttu-id="1015c-478">`identity`&emsp;ユーザー id 情報が必要</span><span class="sxs-lookup"><span data-stu-id="1015c-478">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="1015c-479">`messageTeamMembers`&emsp;チームメンバーに直接メッセージを送信するためのアクセス許可が必要</span><span class="sxs-lookup"><span data-stu-id="1015c-479">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="1015c-480">アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは、更新されたアプリを初めて実行したときに同意プロセスを繰り返すようになります。</span><span class="sxs-lookup"><span data-stu-id="1015c-480">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="1015c-481">詳細については[、「アプリの更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1015c-481">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="1015c-482">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="1015c-482">devicePermissions</span></span>

<span data-ttu-id="1015c-483">**省略可能**文字列の配列</span><span class="sxs-lookup"><span data-stu-id="1015c-483">**Optional** Array of Strings</span></span>

<span data-ttu-id="1015c-484">アプリがアクセスを要求することができる、ユーザーのデバイスのネイティブ機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="1015c-484">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="1015c-485">オプションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="1015c-485">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="1015c-486">validDomains</span><span class="sxs-lookup"><span data-stu-id="1015c-486">validDomains</span></span>

<span data-ttu-id="1015c-487">**省略可能**(記載個所に**必要な**場合を除く)</span><span class="sxs-lookup"><span data-stu-id="1015c-487">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="1015c-488">アプリが Teams クライアント内で読み込むことが想定されている web サイトの有効なドメインの一覧。</span><span class="sxs-lookup"><span data-stu-id="1015c-488">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="1015c-489">ドメインリストには、たとえば`*.example.com`、ワイルドカードを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="1015c-489">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="1015c-490">これは、1つのドメインのセグメントに一致します。に一致`a.b.example.com`させる必要がある`*.*.example.com`場合は、を使用します。</span><span class="sxs-lookup"><span data-stu-id="1015c-490">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="1015c-491">タブ構成またはコンテンツ UI が他のドメインに移動する必要がある場合 (タブの構成に使用するものを除く)、そのドメインをここで指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-491">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="1015c-492">ただし、アプリでサポートする id プロバイダーのドメインを含める必要は**ありません**。</span><span class="sxs-lookup"><span data-stu-id="1015c-492">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="1015c-493">たとえば、Google ID を使用して認証するには、accounts.google.com にリダイレクトする必要がありますが、に`validDomains[]`accounts.google.com を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="1015c-493">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="1015c-494">自分の sharepoint Url が適切に機能する必要がある Teams アプリは、有効なドメインリストに "{teamsitedomain}" を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="1015c-494">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1015c-495">直接に、またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しないでください。</span><span class="sxs-lookup"><span data-stu-id="1015c-495">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="1015c-496">たとえば、は`yourapp.onmicrosoft.com`有効`*.onmicrosoft.com`ですが、有効ではありません。</span><span class="sxs-lookup"><span data-stu-id="1015c-496">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="1015c-497">Object は、型`string`のすべての要素を含む配列です。</span><span class="sxs-lookup"><span data-stu-id="1015c-497">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="1015c-498">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="1015c-498">webApplicationInfo</span></span>

<span data-ttu-id="1015c-499">**Optional**</span><span class="sxs-lookup"><span data-stu-id="1015c-499">**Optional**</span></span>

<span data-ttu-id="1015c-500">Aad アプリ ID とグラフ情報を指定して、ユーザーが AAD アプリにシームレスにサインインできるようにします。</span><span class="sxs-lookup"><span data-stu-id="1015c-500">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="1015c-501">名前</span><span class="sxs-lookup"><span data-stu-id="1015c-501">Name</span></span>| <span data-ttu-id="1015c-502">型</span><span class="sxs-lookup"><span data-stu-id="1015c-502">Type</span></span>| <span data-ttu-id="1015c-503">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="1015c-503">Maximum size</span></span> | <span data-ttu-id="1015c-504">必須</span><span class="sxs-lookup"><span data-stu-id="1015c-504">Required</span></span> | <span data-ttu-id="1015c-505">説明</span><span class="sxs-lookup"><span data-stu-id="1015c-505">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="1015c-506">String</span><span class="sxs-lookup"><span data-stu-id="1015c-506">String</span></span>|<span data-ttu-id="1015c-507">36文字</span><span class="sxs-lookup"><span data-stu-id="1015c-507">36 characters</span></span>|<span data-ttu-id="1015c-508">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-508">✔</span></span>|<span data-ttu-id="1015c-509">アプリの AAD アプリケーション id。</span><span class="sxs-lookup"><span data-stu-id="1015c-509">AAD application id of the app.</span></span> <span data-ttu-id="1015c-510">この id は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="1015c-510">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="1015c-511">String</span><span class="sxs-lookup"><span data-stu-id="1015c-511">String</span></span>|<span data-ttu-id="1015c-512">2048 文字</span><span class="sxs-lookup"><span data-stu-id="1015c-512">2048 characters</span></span>|<span data-ttu-id="1015c-513">✔</span><span class="sxs-lookup"><span data-stu-id="1015c-513">✔</span></span>|<span data-ttu-id="1015c-514">SSO の認証トークンを取得するためのアプリのリソース url。</span><span class="sxs-lookup"><span data-stu-id="1015c-514">Resource url of app for acquiring auth token for SSO.</span></span>|
