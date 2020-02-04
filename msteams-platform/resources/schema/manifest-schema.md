---
title: マニフェストスキーマの参照
description: Microsoft Teams のマニフェストによってサポートされるスキーマについて説明します。
keywords: teams マニフェストスキーマ
ms.openlocfilehash: d4a2864c18a5066673bafab42a46733a0ab5f116
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674900"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="003fe-104">リファレンス: Microsoft Teams のマニフェストスキーマ</span><span class="sxs-lookup"><span data-stu-id="003fe-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="003fe-105">Microsoft Teams のマニフェストでは、アプリを Microsoft Teams 製品に統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="003fe-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="003fe-106">マニフェストは、で[`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json)ホストされているスキーマに準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="003fe-107">以前のバージョン 1.0-1.4 もサポートされています (URL で "v1" を使用します)。</span><span class="sxs-lookup"><span data-stu-id="003fe-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="003fe-108">次のスキーマサンプルは、すべての拡張オプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="003fe-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="003fe-109">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="003fe-109">Sample full manifest</span></span>

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

<span data-ttu-id="003fe-110">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="003fe-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="003fe-111">$schema</span><span class="sxs-lookup"><span data-stu-id="003fe-111">$schema</span></span>

<span data-ttu-id="003fe-112">*省略可能。ただし、推奨* &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="003fe-112">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="003fe-113">マニフェストの JSON スキーマを参照する https://URL。</span><span class="sxs-lookup"><span data-stu-id="003fe-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="003fe-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="003fe-114">manifestVersion</span></span>

<span data-ttu-id="003fe-115">**必要な** &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="003fe-115">**Required** &ndash; String</span></span>

<span data-ttu-id="003fe-116">このマニフェストが使用しているマニフェストスキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="003fe-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="003fe-117">"1.5" である必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="003fe-118">バージョン</span><span class="sxs-lookup"><span data-stu-id="003fe-118">version</span></span>

<span data-ttu-id="003fe-119">**必要な** &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="003fe-119">**Required** &ndash; String</span></span>

<span data-ttu-id="003fe-120">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="003fe-120">The version of the specific app.</span></span> <span data-ttu-id="003fe-121">マニフェスト内の内容を更新する場合は、そのバージョンも同時にインクリメントする必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="003fe-122">このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。</span><span class="sxs-lookup"><span data-stu-id="003fe-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="003fe-123">このアプリがストアに送信された場合は、新しいマニフェストを再送信して再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="003fe-124">その後、このアプリのユーザーは、承認後に数時間以内に新しい更新されたマニフェストを自動的に取得します。</span><span class="sxs-lookup"><span data-stu-id="003fe-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="003fe-125">アプリによって要求されたアクセス許可が変更された場合、ユーザーはアプリをアップグレードして再同意するように求められます。</span><span class="sxs-lookup"><span data-stu-id="003fe-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="003fe-126">このバージョンの文字列は、 [semver](http://semver.org/)標準 (メジャー) に従う必要があります。間隔.パッチ)。</span><span class="sxs-lookup"><span data-stu-id="003fe-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="003fe-127">ID</span><span class="sxs-lookup"><span data-stu-id="003fe-127">id</span></span>

<span data-ttu-id="003fe-128">**必要な** &ndash; Microsoft アプリ ID</span><span class="sxs-lookup"><span data-stu-id="003fe-128">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="003fe-129">このアプリの一意の Microsoft 生成識別子。</span><span class="sxs-lookup"><span data-stu-id="003fe-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="003fe-130">Microsoft Bot フレームワークを介して bot を登録した場合、またはタブの web アプリが Microsoft によって既にサインインしている場合は、既に ID があるので、ここで入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="003fe-131">それ以外の場合は、Microsoft アプリケーション登録ポータル ([My Applications](https://apps.dev.microsoft.com)) で新しい ID を生成し、ここで入力してから、bot を追加するときにそれを再利用する必要があります。注: AppSource で既存のアプリに更新を送信する場合は、マニフェスト内の ID を変更しないでください。</span><span class="sxs-lookup"><span data-stu-id="003fe-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="packagename"></a><span data-ttu-id="003fe-132">packageName</span><span class="sxs-lookup"><span data-stu-id="003fe-132">packageName</span></span>

<span data-ttu-id="003fe-133">**必要な** &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="003fe-133">**Required** &ndash; String</span></span>

<span data-ttu-id="003fe-134">逆引きドメイン表記でのこのアプリの一意識別子。たとえば、例のようになります。</span><span class="sxs-lookup"><span data-stu-id="003fe-134">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="003fe-135">developer</span><span class="sxs-lookup"><span data-stu-id="003fe-135">developer</span></span>

<span data-ttu-id="003fe-136">**必須**</span><span class="sxs-lookup"><span data-stu-id="003fe-136">**Required**</span></span>

<span data-ttu-id="003fe-137">会社に関する情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="003fe-137">Specifies information about your company.</span></span> <span data-ttu-id="003fe-138">AppSource (旧称 Office ストア) に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="003fe-139">追加情報については、[発行に関するガイドライン](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="003fe-139">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="003fe-140">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-140">Name</span></span>| <span data-ttu-id="003fe-141">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-141">Maximum size</span></span> | <span data-ttu-id="003fe-142">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-142">Required</span></span> | <span data-ttu-id="003fe-143">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="003fe-144">32文字</span><span class="sxs-lookup"><span data-stu-id="003fe-144">32 characters</span></span>|<span data-ttu-id="003fe-145">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-145">✔</span></span>|<span data-ttu-id="003fe-146">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="003fe-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="003fe-147">2048 文字</span><span class="sxs-lookup"><span data-stu-id="003fe-147">2048 characters</span></span>|<span data-ttu-id="003fe-148">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-148">✔</span></span>|<span data-ttu-id="003fe-149">開発者の web サイトへの https://URL。</span><span class="sxs-lookup"><span data-stu-id="003fe-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="003fe-150">このリンクは、ユーザーを会社または製品固有のランディングページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="003fe-151">2048 文字</span><span class="sxs-lookup"><span data-stu-id="003fe-151">2048 characters</span></span>|<span data-ttu-id="003fe-152">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-152">✔</span></span>|<span data-ttu-id="003fe-153">開発者のプライバシーポリシーへの https://URL。</span><span class="sxs-lookup"><span data-stu-id="003fe-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="003fe-154">2048 文字</span><span class="sxs-lookup"><span data-stu-id="003fe-154">2048 characters</span></span>|<span data-ttu-id="003fe-155">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-155">✔</span></span>|<span data-ttu-id="003fe-156">開発者の使用条件への https://URL。</span><span class="sxs-lookup"><span data-stu-id="003fe-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="003fe-157">10文字</span><span class="sxs-lookup"><span data-stu-id="003fe-157">10 characters</span></span>| |<span data-ttu-id="003fe-158">**省略可能**アプリを構築するパートナー組織を識別する Microsoft パートナーのネットワーク ID。</span><span class="sxs-lookup"><span data-stu-id="003fe-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="003fe-159">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="003fe-159">localizationInfo</span></span>

<span data-ttu-id="003fe-160">**Optional**</span><span class="sxs-lookup"><span data-stu-id="003fe-160">**Optional**</span></span>

<span data-ttu-id="003fe-161">既定の言語の指定、および追加の言語ファイルへのポインターを許可します。</span><span class="sxs-lookup"><span data-stu-id="003fe-161">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="003fe-162">「[ローカライズ](~/concepts/build-and-test/apps-localization.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="003fe-162">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="003fe-163">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-163">Name</span></span>| <span data-ttu-id="003fe-164">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-164">Maximum size</span></span> | <span data-ttu-id="003fe-165">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-165">Required</span></span> | <span data-ttu-id="003fe-166">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-166">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="003fe-167">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-167">✔</span></span>|<span data-ttu-id="003fe-168">このトップレベルマニフェストファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="003fe-168">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="003fe-169">localizationInfo. additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="003fe-169">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="003fe-170">追加の言語の翻訳を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="003fe-170">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="003fe-171">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-171">Name</span></span>| <span data-ttu-id="003fe-172">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-172">Maximum size</span></span> | <span data-ttu-id="003fe-173">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-173">Required</span></span> | <span data-ttu-id="003fe-174">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-174">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="003fe-175">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-175">✔</span></span>|<span data-ttu-id="003fe-176">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="003fe-176">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="003fe-177">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-177">✔</span></span>|<span data-ttu-id="003fe-178">翻訳された文字列を含む json ファイルへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="003fe-178">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="003fe-179">name</span><span class="sxs-lookup"><span data-stu-id="003fe-179">name</span></span>

<span data-ttu-id="003fe-180">**必須**</span><span class="sxs-lookup"><span data-stu-id="003fe-180">**Required**</span></span>

<span data-ttu-id="003fe-181">Teams でユーザーに表示されるアプリの動作の名前です。</span><span class="sxs-lookup"><span data-stu-id="003fe-181">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="003fe-182">AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-182">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="003fe-183">との`short`値を`full`同じにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="003fe-183">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="003fe-184">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-184">Name</span></span>| <span data-ttu-id="003fe-185">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-185">Maximum size</span></span> | <span data-ttu-id="003fe-186">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-186">Required</span></span> | <span data-ttu-id="003fe-187">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-187">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="003fe-188">30 文字</span><span class="sxs-lookup"><span data-stu-id="003fe-188">30 characters</span></span>|<span data-ttu-id="003fe-189">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-189">✔</span></span>|<span data-ttu-id="003fe-190">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="003fe-190">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="003fe-191">100 文字</span><span class="sxs-lookup"><span data-stu-id="003fe-191">100 characters</span></span>||<span data-ttu-id="003fe-192">アプリの完全な名前。アプリの完全な名前が30文字を超えている場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="003fe-192">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="003fe-193">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-193">description</span></span>

<span data-ttu-id="003fe-194">**必須**</span><span class="sxs-lookup"><span data-stu-id="003fe-194">**Required**</span></span>

<span data-ttu-id="003fe-195">ユーザーに対してアプリを記述します。</span><span class="sxs-lookup"><span data-stu-id="003fe-195">Describes your app to users.</span></span> <span data-ttu-id="003fe-196">AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-196">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="003fe-197">説明に正確に表示されていることを確認し、お客様が快適な動作を理解するのに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="003fe-197">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="003fe-198">また、外部アカウントが使用するために必要な場合は、詳細な説明にも注意してください。</span><span class="sxs-lookup"><span data-stu-id="003fe-198">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="003fe-199">との`short`値を`full`同じにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="003fe-199">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="003fe-200">短い説明を長い説明の中で繰り返すことはできません。他のアプリ名を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="003fe-200">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="003fe-201">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-201">Name</span></span>| <span data-ttu-id="003fe-202">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-202">Maximum size</span></span> | <span data-ttu-id="003fe-203">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-203">Required</span></span> | <span data-ttu-id="003fe-204">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-204">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="003fe-205">80文字</span><span class="sxs-lookup"><span data-stu-id="003fe-205">80 characters</span></span>|<span data-ttu-id="003fe-206">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-206">✔</span></span>|<span data-ttu-id="003fe-207">スペースが制限されている場合に使用する、アプリの使用状況の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="003fe-207">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="003fe-208">4000文字</span><span class="sxs-lookup"><span data-stu-id="003fe-208">4000 characters</span></span>|<span data-ttu-id="003fe-209">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-209">✔</span></span>|<span data-ttu-id="003fe-210">アプリの詳細な説明。</span><span class="sxs-lookup"><span data-stu-id="003fe-210">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="003fe-211">アイコン</span><span class="sxs-lookup"><span data-stu-id="003fe-211">icons</span></span>

<span data-ttu-id="003fe-212">**必須**</span><span class="sxs-lookup"><span data-stu-id="003fe-212">**Required**</span></span>

<span data-ttu-id="003fe-213">Teams アプリ内で使用されるアイコン。</span><span class="sxs-lookup"><span data-stu-id="003fe-213">Icons used within the Teams app.</span></span> <span data-ttu-id="003fe-214">アイコンファイルは、アップロードパッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-214">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="003fe-215">詳細については、「[アイコン](~/concepts/build-and-test/apps-package.md#icons)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="003fe-215">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="003fe-216">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-216">Name</span></span>| <span data-ttu-id="003fe-217">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-217">Maximum size</span></span> | <span data-ttu-id="003fe-218">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-218">Required</span></span> | <span data-ttu-id="003fe-219">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-219">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="003fe-220">2048 文字</span><span class="sxs-lookup"><span data-stu-id="003fe-220">2048 characters</span></span>|<span data-ttu-id="003fe-221">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-221">✔</span></span>|<span data-ttu-id="003fe-222">透明な32x32 の PNG アウトラインアイコンへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="003fe-222">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="003fe-223">2048 文字</span><span class="sxs-lookup"><span data-stu-id="003fe-223">2048 characters</span></span>|<span data-ttu-id="003fe-224">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-224">✔</span></span>|<span data-ttu-id="003fe-225">フルカラー 192x192 PNG アイコンへの相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="003fe-225">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="003fe-226">アクセントカラー</span><span class="sxs-lookup"><span data-stu-id="003fe-226">accentColor</span></span>

<span data-ttu-id="003fe-227">**必要な** &ndash;文字列</span><span class="sxs-lookup"><span data-stu-id="003fe-227">**Required** &ndash; String</span></span>

<span data-ttu-id="003fe-228">とと組み合わせてアウトラインアイコンの背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="003fe-228">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="003fe-229">この値は、' # ' で始まる有効な HTML カラーコードである必要`#4464ee`があります (例:)。</span><span class="sxs-lookup"><span data-stu-id="003fe-229">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="003fe-230">の各タブ</span><span class="sxs-lookup"><span data-stu-id="003fe-230">configurableTabs</span></span>

<span data-ttu-id="003fe-231">**Optional**</span><span class="sxs-lookup"><span data-stu-id="003fe-231">**Optional**</span></span>

<span data-ttu-id="003fe-232">アプリの機能に、追加の構成を必要とするチームチャネルのタブがある場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="003fe-232">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="003fe-233">構成可能なタブは teams スコープでのみサポートされており、現在、アプリごとに1つのタブのみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="003fe-233">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="003fe-234">Object は、型`object`のすべての要素を含む配列です。</span><span class="sxs-lookup"><span data-stu-id="003fe-234">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="003fe-235">このブロックは、構成可能なチャネルのタブソリューションを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="003fe-235">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="003fe-236">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-236">Name</span></span>| <span data-ttu-id="003fe-237">型</span><span class="sxs-lookup"><span data-stu-id="003fe-237">Type</span></span>| <span data-ttu-id="003fe-238">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-238">Maximum size</span></span> | <span data-ttu-id="003fe-239">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-239">Required</span></span> | <span data-ttu-id="003fe-240">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-240">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="003fe-241">String</span><span class="sxs-lookup"><span data-stu-id="003fe-241">String</span></span>|<span data-ttu-id="003fe-242">2048 文字</span><span class="sxs-lookup"><span data-stu-id="003fe-242">2048 characters</span></span>|<span data-ttu-id="003fe-243">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-243">✔</span></span>|<span data-ttu-id="003fe-244">タブを構成するときに使用する https://URL。</span><span class="sxs-lookup"><span data-stu-id="003fe-244">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="003fe-245">Boolean</span><span class="sxs-lookup"><span data-stu-id="003fe-245">Boolean</span></span>|||<span data-ttu-id="003fe-246">作成後にタブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="003fe-246">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="003fe-247">限り`true`</span><span class="sxs-lookup"><span data-stu-id="003fe-247">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="003fe-248">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="003fe-248">Array of enum</span></span>|<span data-ttu-id="003fe-249">1 </span><span class="sxs-lookup"><span data-stu-id="003fe-249">1</span></span>|<span data-ttu-id="003fe-250">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-250">✔</span></span>|<span data-ttu-id="003fe-251">現在、構成可能なタブで`team`は`groupchat` 、およびスコープのみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="003fe-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="003fe-252">String</span><span class="sxs-lookup"><span data-stu-id="003fe-252">String</span></span>|<span data-ttu-id="003fe-253">2048</span><span class="sxs-lookup"><span data-stu-id="003fe-253">2048</span></span>||<span data-ttu-id="003fe-254">SharePoint で使用するタブプレビュー画像への相対ファイルパス。</span><span class="sxs-lookup"><span data-stu-id="003fe-254">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="003fe-255">サイズ1024x768。</span><span class="sxs-lookup"><span data-stu-id="003fe-255">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="003fe-256">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="003fe-256">Array of enum</span></span>|<span data-ttu-id="003fe-257">1 </span><span class="sxs-lookup"><span data-stu-id="003fe-257">1</span></span>||<span data-ttu-id="003fe-258">SharePoint でどのようにタブを使用できるようにするかを定義します。</span><span class="sxs-lookup"><span data-stu-id="003fe-258">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="003fe-259">オプション`sharePointFullPage`と`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="003fe-259">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="003fe-260">staticTabs</span><span class="sxs-lookup"><span data-stu-id="003fe-260">staticTabs</span></span>

<span data-ttu-id="003fe-261">**Optional**</span><span class="sxs-lookup"><span data-stu-id="003fe-261">**Optional**</span></span>

<span data-ttu-id="003fe-262">ユーザーが手動で追加せずに、既定で "固定" できるタブのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="003fe-262">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="003fe-263">スコープ内で`personal`宣言されている静的タブは、常にアプリの個人の環境に固定されます。</span><span class="sxs-lookup"><span data-stu-id="003fe-263">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="003fe-264">`team`スコープ内で宣言されている静的タブは現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="003fe-264">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="003fe-265">Object は、型`object`のすべての要素を含む配列 (最大16個の要素) です。</span><span class="sxs-lookup"><span data-stu-id="003fe-265">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="003fe-266">このブロックは、静的なタブソリューションを提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="003fe-266">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="003fe-267">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-267">Name</span></span>| <span data-ttu-id="003fe-268">型</span><span class="sxs-lookup"><span data-stu-id="003fe-268">Type</span></span>| <span data-ttu-id="003fe-269">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-269">Maximum size</span></span> | <span data-ttu-id="003fe-270">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-270">Required</span></span> | <span data-ttu-id="003fe-271">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-271">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="003fe-272">String</span><span class="sxs-lookup"><span data-stu-id="003fe-272">String</span></span>|<span data-ttu-id="003fe-273">64文字</span><span class="sxs-lookup"><span data-stu-id="003fe-273">64 characters</span></span>|<span data-ttu-id="003fe-274">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-274">✔</span></span>|<span data-ttu-id="003fe-275">タブに表示されるエンティティの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="003fe-275">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="003fe-276">String</span><span class="sxs-lookup"><span data-stu-id="003fe-276">String</span></span>|<span data-ttu-id="003fe-277">128文字</span><span class="sxs-lookup"><span data-stu-id="003fe-277">128 characters</span></span>|<span data-ttu-id="003fe-278">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-278">✔</span></span>|<span data-ttu-id="003fe-279">チャネルインターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="003fe-279">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="003fe-280">String</span><span class="sxs-lookup"><span data-stu-id="003fe-280">String</span></span>|<span data-ttu-id="003fe-281">2048 文字</span><span class="sxs-lookup"><span data-stu-id="003fe-281">2048 characters</span></span>|<span data-ttu-id="003fe-282">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-282">✔</span></span>|<span data-ttu-id="003fe-283">Teams キャンバスに表示されるエンティティ UI をポイントする https://URL。</span><span class="sxs-lookup"><span data-stu-id="003fe-283">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="003fe-284">String</span><span class="sxs-lookup"><span data-stu-id="003fe-284">String</span></span>|<span data-ttu-id="003fe-285">2048 文字</span><span class="sxs-lookup"><span data-stu-id="003fe-285">2048 characters</span></span>||<span data-ttu-id="003fe-286">ユーザーがブラウザーで表示をポイントしたかどうかを示す https://URL。</span><span class="sxs-lookup"><span data-stu-id="003fe-286">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="003fe-287">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="003fe-287">Array of enum</span></span>|<span data-ttu-id="003fe-288">1 </span><span class="sxs-lookup"><span data-stu-id="003fe-288">1</span></span>|<span data-ttu-id="003fe-289">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-289">✔</span></span>|<span data-ttu-id="003fe-290">現時点では、静的タブで`personal`はスコープのみがサポートされます。つまり、個人の利便性の一環としてのみプロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="003fe-290">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="003fe-291">bot</span><span class="sxs-lookup"><span data-stu-id="003fe-291">bots</span></span>

<span data-ttu-id="003fe-292">**Optional**</span><span class="sxs-lookup"><span data-stu-id="003fe-292">**Optional**</span></span>

<span data-ttu-id="003fe-293">Bot ソリューションと、既定のコマンドプロパティなどのオプション情報を定義します。</span><span class="sxs-lookup"><span data-stu-id="003fe-293">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="003fe-294">オブジェクトが配列の場合 (現時点では1つ&mdash;の要素のうちの最大値は1つですが、現在は`object`アプリごとに1つの bot のみが許可されます)、型のすべての要素を使用します</span><span class="sxs-lookup"><span data-stu-id="003fe-294">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="003fe-295">このブロックは、bot の環境を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="003fe-295">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="003fe-296">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-296">Name</span></span>| <span data-ttu-id="003fe-297">型</span><span class="sxs-lookup"><span data-stu-id="003fe-297">Type</span></span>| <span data-ttu-id="003fe-298">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-298">Maximum size</span></span> | <span data-ttu-id="003fe-299">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-299">Required</span></span> | <span data-ttu-id="003fe-300">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-300">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="003fe-301">String</span><span class="sxs-lookup"><span data-stu-id="003fe-301">String</span></span>|<span data-ttu-id="003fe-302">64文字</span><span class="sxs-lookup"><span data-stu-id="003fe-302">64 characters</span></span>|<span data-ttu-id="003fe-303">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-303">✔</span></span>|<span data-ttu-id="003fe-304">Bot フレームワークに登録された bot の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="003fe-304">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="003fe-305">これは、アプリの全体的な[ID](#id)と同じである場合もあります。</span><span class="sxs-lookup"><span data-stu-id="003fe-305">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="003fe-306">Boolean</span><span class="sxs-lookup"><span data-stu-id="003fe-306">Boolean</span></span>|||<span data-ttu-id="003fe-307">Bot がユーザーヒントを利用して、特定のチャネルに bot を追加するかどうかを記述します。</span><span class="sxs-lookup"><span data-stu-id="003fe-307">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="003fe-308">限り`false`</span><span class="sxs-lookup"><span data-stu-id="003fe-308">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="003fe-309">Boolean</span><span class="sxs-lookup"><span data-stu-id="003fe-309">Boolean</span></span>|||<span data-ttu-id="003fe-310">Bot が、話し言葉とは異なり、単一の通知のみの bot であるかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="003fe-310">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="003fe-311">限り`false`</span><span class="sxs-lookup"><span data-stu-id="003fe-311">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="003fe-312">Boolean</span><span class="sxs-lookup"><span data-stu-id="003fe-312">Boolean</span></span>|||<span data-ttu-id="003fe-313">Bot が個人チャットでファイルをアップロード/ダウンロードする機能をサポートしているかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="003fe-313">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="003fe-314">限り`false`</span><span class="sxs-lookup"><span data-stu-id="003fe-314">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="003fe-315">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="003fe-315">Array of enum</span></span>|<span data-ttu-id="003fe-316">3 </span><span class="sxs-lookup"><span data-stu-id="003fe-316">3</span></span>|<span data-ttu-id="003fe-317">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-317">✔</span></span>|<span data-ttu-id="003fe-318">Bot が a `team`内のチャネル、グループチャット (`groupchat`)、または個別のユーザー単独 (`personal`) に限定された環境での動作を提供するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="003fe-318">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="003fe-319">これらのオプションは排他的ではありません。</span><span class="sxs-lookup"><span data-stu-id="003fe-319">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="003fe-320">bot リスト</span><span class="sxs-lookup"><span data-stu-id="003fe-320">bots.commandLists</span></span>

<span data-ttu-id="003fe-321">Bot がユーザーに推奨できるコマンドのオプションの一覧。</span><span class="sxs-lookup"><span data-stu-id="003fe-321">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="003fe-322">Object は、型`object`のすべての要素を含む配列 (最大2つの要素) です。bot がサポートするスコープごとに個別のコマンドリストを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-322">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="003fe-323">詳細については、「 [Bot メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="003fe-323">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="003fe-324">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-324">Name</span></span>| <span data-ttu-id="003fe-325">型</span><span class="sxs-lookup"><span data-stu-id="003fe-325">Type</span></span>| <span data-ttu-id="003fe-326">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-326">Maximum size</span></span> | <span data-ttu-id="003fe-327">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-327">Required</span></span> | <span data-ttu-id="003fe-328">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-328">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="003fe-329">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="003fe-329">array of enum</span></span>|<span data-ttu-id="003fe-330">3 </span><span class="sxs-lookup"><span data-stu-id="003fe-330">3</span></span>|<span data-ttu-id="003fe-331">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-331">✔</span></span>|<span data-ttu-id="003fe-332">コマンドリストが有効である範囲を指定します。</span><span class="sxs-lookup"><span data-stu-id="003fe-332">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="003fe-333">オプションは`team`、 `personal`、、 `groupchat`です。</span><span class="sxs-lookup"><span data-stu-id="003fe-333">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="003fe-334">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="003fe-334">array of objects</span></span>|<span data-ttu-id="003fe-335">10 </span><span class="sxs-lookup"><span data-stu-id="003fe-335">10</span></span>|<span data-ttu-id="003fe-336">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-336">✔</span></span>|<span data-ttu-id="003fe-337">Bot がサポートするコマンドの配列。</span><span class="sxs-lookup"><span data-stu-id="003fe-337">An array of commands the bot supports:</span></span><br><span data-ttu-id="003fe-338">`title`: bot コマンド名 (string, 32)</span><span class="sxs-lookup"><span data-stu-id="003fe-338">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="003fe-339">`description`: コマンド構文とその引数の簡単な説明または例 (string, 128)</span><span class="sxs-lookup"><span data-stu-id="003fe-339">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="003fe-340">コネクタ</span><span class="sxs-lookup"><span data-stu-id="003fe-340">connectors</span></span>

<span data-ttu-id="003fe-341">**Optional**</span><span class="sxs-lookup"><span data-stu-id="003fe-341">**Optional**</span></span>

<span data-ttu-id="003fe-342">ブロック`connectors`は、アプリの Office 365 コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="003fe-342">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="003fe-343">Object は、type `object`のすべての要素を含む配列 (最大1つの要素) です。</span><span class="sxs-lookup"><span data-stu-id="003fe-343">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="003fe-344">このブロックは、コネクタを提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="003fe-344">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="003fe-345">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-345">Name</span></span>| <span data-ttu-id="003fe-346">型</span><span class="sxs-lookup"><span data-stu-id="003fe-346">Type</span></span>| <span data-ttu-id="003fe-347">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-347">Maximum size</span></span> | <span data-ttu-id="003fe-348">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-348">Required</span></span> | <span data-ttu-id="003fe-349">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-349">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="003fe-350">String</span><span class="sxs-lookup"><span data-stu-id="003fe-350">String</span></span>|<span data-ttu-id="003fe-351">2048 文字</span><span class="sxs-lookup"><span data-stu-id="003fe-351">2048 characters</span></span>|<span data-ttu-id="003fe-352">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-352">✔</span></span>|<span data-ttu-id="003fe-353">コネクタを構成するときに使用する https://URL。</span><span class="sxs-lookup"><span data-stu-id="003fe-353">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="003fe-354">String</span><span class="sxs-lookup"><span data-stu-id="003fe-354">String</span></span>|<span data-ttu-id="003fe-355">64文字</span><span class="sxs-lookup"><span data-stu-id="003fe-355">64 characters</span></span>|<span data-ttu-id="003fe-356">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-356">✔</span></span>|<span data-ttu-id="003fe-357">コネクタ[開発者ダッシュボード](https://aka.ms/connectorsdashboard)の ID と一致するコネクタの一意識別子。</span><span class="sxs-lookup"><span data-stu-id="003fe-357">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="003fe-358">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="003fe-358">Array of enum</span></span>|<span data-ttu-id="003fe-359">1 </span><span class="sxs-lookup"><span data-stu-id="003fe-359">1</span></span>|<span data-ttu-id="003fe-360">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-360">✔</span></span>|<span data-ttu-id="003fe-361">コネクタが内`team`のチャネルのコンテキストで、または個別のユーザー単独 (`personal`) にスコープ設定された環境での動作を提供するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="003fe-361">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="003fe-362">現時点では、 `team`範囲のみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="003fe-362">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="003fe-363">この機能</span><span class="sxs-lookup"><span data-stu-id="003fe-363">composeExtensions</span></span>

<span data-ttu-id="003fe-364">**Optional**</span><span class="sxs-lookup"><span data-stu-id="003fe-364">**Optional**</span></span>

<span data-ttu-id="003fe-365">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="003fe-365">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="003fe-366">この機能の名前は、2017年11月に「[作成] 拡張機能」から「messaging extension」に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は同じままです。</span><span class="sxs-lookup"><span data-stu-id="003fe-366">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="003fe-367">Object は、type `object`のすべての要素を含む配列 (最大1つの要素) です。</span><span class="sxs-lookup"><span data-stu-id="003fe-367">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="003fe-368">このブロックは、メッセージング拡張機能を提供するソリューションに対してのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="003fe-368">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="003fe-369">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-369">Name</span></span>| <span data-ttu-id="003fe-370">型</span><span class="sxs-lookup"><span data-stu-id="003fe-370">Type</span></span> | <span data-ttu-id="003fe-371">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-371">Maximum Size</span></span> | <span data-ttu-id="003fe-372">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-372">Required</span></span> | <span data-ttu-id="003fe-373">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-373">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="003fe-374">String</span><span class="sxs-lookup"><span data-stu-id="003fe-374">String</span></span>|<span data-ttu-id="003fe-375">64</span><span class="sxs-lookup"><span data-stu-id="003fe-375">64</span></span>|<span data-ttu-id="003fe-376">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-376">✔</span></span>|<span data-ttu-id="003fe-377">Bot フレームワークに登録されているメッセージング拡張機能をバックアップする bot の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="003fe-377">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="003fe-378">これは、アプリの全体的な ID と同じである場合もあります。</span><span class="sxs-lookup"><span data-stu-id="003fe-378">This may well be the same as the overall App ID.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="003fe-379">Boolean</span><span class="sxs-lookup"><span data-stu-id="003fe-379">Boolean</span></span>|||<span data-ttu-id="003fe-380">メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="003fe-380">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="003fe-381">既定値は `false` です。</span><span class="sxs-lookup"><span data-stu-id="003fe-381">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="003fe-382">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="003fe-382">Array of object</span></span>|<span data-ttu-id="003fe-383">10 </span><span class="sxs-lookup"><span data-stu-id="003fe-383">10</span></span>|<span data-ttu-id="003fe-384">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-384">✔</span></span>|<span data-ttu-id="003fe-385">メッセージング拡張機能がサポートするコマンドの配列</span><span class="sxs-lookup"><span data-stu-id="003fe-385">Array of commands the messaging extension supports</span></span>|
|`messageHandlers`|<span data-ttu-id="003fe-386">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="003fe-386">Array of Objects</span></span>|<span data-ttu-id="003fe-387">5 </span><span class="sxs-lookup"><span data-stu-id="003fe-387">5</span></span>||<span data-ttu-id="003fe-388">特定の条件が満たされたときにアプリを呼び出せるようにするハンドラーの一覧。</span><span class="sxs-lookup"><span data-stu-id="003fe-388">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="003fe-389">ドメインも、にリストされている必要があります。`validDomains`</span><span class="sxs-lookup"><span data-stu-id="003fe-389">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="003fe-390">String</span><span class="sxs-lookup"><span data-stu-id="003fe-390">String</span></span>|||<span data-ttu-id="003fe-391">メッセージハンドラの種類。</span><span class="sxs-lookup"><span data-stu-id="003fe-391">The type of message handler.</span></span> <span data-ttu-id="003fe-392">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-392">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="003fe-393">文字列 (String) の配列</span><span class="sxs-lookup"><span data-stu-id="003fe-393">Array of Strings</span></span>|||<span data-ttu-id="003fe-394">リンクメッセージハンドラが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="003fe-394">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="003fe-395">このコマンドの機能</span><span class="sxs-lookup"><span data-stu-id="003fe-395">composeExtensions.commands</span></span>

<span data-ttu-id="003fe-396">メッセージング拡張機能は、1つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-396">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="003fe-397">各コマンドは、Microsoft Teams に UI ベースのエントリポイントからの潜在的な操作として表示されます。</span><span class="sxs-lookup"><span data-stu-id="003fe-397">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="003fe-398">最大10個のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="003fe-398">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="003fe-399">各コマンド項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="003fe-399">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="003fe-400">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-400">Name</span></span>| <span data-ttu-id="003fe-401">型</span><span class="sxs-lookup"><span data-stu-id="003fe-401">Type</span></span>| <span data-ttu-id="003fe-402">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-402">Maximum size</span></span> | <span data-ttu-id="003fe-403">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-403">Required</span></span> | <span data-ttu-id="003fe-404">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-404">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="003fe-405">String</span><span class="sxs-lookup"><span data-stu-id="003fe-405">String</span></span>|<span data-ttu-id="003fe-406">64文字</span><span class="sxs-lookup"><span data-stu-id="003fe-406">64 characters</span></span>|<span data-ttu-id="003fe-407">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-407">✔</span></span>|<span data-ttu-id="003fe-408">コマンドの ID</span><span class="sxs-lookup"><span data-stu-id="003fe-408">The ID for the command</span></span>|
|`type`|<span data-ttu-id="003fe-409">String</span><span class="sxs-lookup"><span data-stu-id="003fe-409">String</span></span>|<span data-ttu-id="003fe-410">64文字</span><span class="sxs-lookup"><span data-stu-id="003fe-410">64 characters</span></span>||<span data-ttu-id="003fe-411">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="003fe-411">Type of the command.</span></span> <span data-ttu-id="003fe-412">または`query` `action`のいずれかです。</span><span class="sxs-lookup"><span data-stu-id="003fe-412">One of `query` or `action`.</span></span> <span data-ttu-id="003fe-413">限り`query`</span><span class="sxs-lookup"><span data-stu-id="003fe-413">Default: `query`</span></span>|
|`title`|<span data-ttu-id="003fe-414">String</span><span class="sxs-lookup"><span data-stu-id="003fe-414">String</span></span>|<span data-ttu-id="003fe-415">32文字</span><span class="sxs-lookup"><span data-stu-id="003fe-415">32 characters</span></span>|<span data-ttu-id="003fe-416">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-416">✔</span></span>|<span data-ttu-id="003fe-417">ユーザーフレンドリなコマンド名</span><span class="sxs-lookup"><span data-stu-id="003fe-417">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="003fe-418">String</span><span class="sxs-lookup"><span data-stu-id="003fe-418">String</span></span>|<span data-ttu-id="003fe-419">128文字</span><span class="sxs-lookup"><span data-stu-id="003fe-419">128 characters</span></span>||<span data-ttu-id="003fe-420">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="003fe-420">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="003fe-421">Boolean</span><span class="sxs-lookup"><span data-stu-id="003fe-421">Boolean</span></span>|||<span data-ttu-id="003fe-422">パラメーターを指定せずにコマンドを最初に実行する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="003fe-422">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="003fe-423">限り`false`</span><span class="sxs-lookup"><span data-stu-id="003fe-423">Default: `false`</span></span>|
|`context`|<span data-ttu-id="003fe-424">文字列 (String) の配列</span><span class="sxs-lookup"><span data-stu-id="003fe-424">Array of Strings</span></span>|<span data-ttu-id="003fe-425">3 </span><span class="sxs-lookup"><span data-stu-id="003fe-425">3</span></span>||<span data-ttu-id="003fe-426">メッセージの内線番号をから呼び出すことができる場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="003fe-426">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="003fe-427">、 `commandBox`、 `message`の`compose`任意の組み合わせ。</span><span class="sxs-lookup"><span data-stu-id="003fe-427">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="003fe-428">既定値は`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="003fe-428">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="003fe-429">Boolean</span><span class="sxs-lookup"><span data-stu-id="003fe-429">Boolean</span></span>|||<span data-ttu-id="003fe-430">タスクモジュールを動的に取得する必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="003fe-430">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="003fe-431">オブジェクト</span><span class="sxs-lookup"><span data-stu-id="003fe-431">Object</span></span>|||<span data-ttu-id="003fe-432">メッセージ拡張コマンドの使用時にプリロードするタスクモジュールを指定する</span><span class="sxs-lookup"><span data-stu-id="003fe-432">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="003fe-433">String</span><span class="sxs-lookup"><span data-stu-id="003fe-433">String</span></span>|<span data-ttu-id="003fe-434">64</span><span class="sxs-lookup"><span data-stu-id="003fe-434">64</span></span>||<span data-ttu-id="003fe-435">最初のダイアログのタイトル</span><span class="sxs-lookup"><span data-stu-id="003fe-435">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="003fe-436">String</span><span class="sxs-lookup"><span data-stu-id="003fe-436">String</span></span>|||<span data-ttu-id="003fe-437">ダイアログの幅。ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="003fe-437">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="003fe-438">String</span><span class="sxs-lookup"><span data-stu-id="003fe-438">String</span></span>|||<span data-ttu-id="003fe-439">ダイアログの高さ-ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。</span><span class="sxs-lookup"><span data-stu-id="003fe-439">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="003fe-440">String</span><span class="sxs-lookup"><span data-stu-id="003fe-440">String</span></span>|||<span data-ttu-id="003fe-441">最初の webview の URL</span><span class="sxs-lookup"><span data-stu-id="003fe-441">Initial webview URL</span></span>|
|`parameters`|<span data-ttu-id="003fe-442">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="003fe-442">Array of object</span></span>|<span data-ttu-id="003fe-443">5 </span><span class="sxs-lookup"><span data-stu-id="003fe-443">5</span></span>|<span data-ttu-id="003fe-444">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-444">✔</span></span>|<span data-ttu-id="003fe-445">コマンドが実行するパラメーターの一覧。</span><span class="sxs-lookup"><span data-stu-id="003fe-445">The list of parameters the command takes.</span></span> <span data-ttu-id="003fe-446">最小値: 1、最大: 5</span><span class="sxs-lookup"><span data-stu-id="003fe-446">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="003fe-447">String</span><span class="sxs-lookup"><span data-stu-id="003fe-447">String</span></span>|<span data-ttu-id="003fe-448">64文字</span><span class="sxs-lookup"><span data-stu-id="003fe-448">64 characters</span></span>|<span data-ttu-id="003fe-449">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-449">✔</span></span>|<span data-ttu-id="003fe-450">クライアントに表示されるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="003fe-450">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="003fe-451">これは、ユーザー要求に含まれています。</span><span class="sxs-lookup"><span data-stu-id="003fe-451">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="003fe-452">String</span><span class="sxs-lookup"><span data-stu-id="003fe-452">String</span></span>|<span data-ttu-id="003fe-453">32文字</span><span class="sxs-lookup"><span data-stu-id="003fe-453">32 characters</span></span>|<span data-ttu-id="003fe-454">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-454">✔</span></span>|<span data-ttu-id="003fe-455">パラメーターのユーザーフレンドリなタイトル。</span><span class="sxs-lookup"><span data-stu-id="003fe-455">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="003fe-456">String</span><span class="sxs-lookup"><span data-stu-id="003fe-456">String</span></span>|<span data-ttu-id="003fe-457">128文字</span><span class="sxs-lookup"><span data-stu-id="003fe-457">128 characters</span></span>||<span data-ttu-id="003fe-458">このパラメーターの目的を説明するユーザーフレンドリ文字列。</span><span class="sxs-lookup"><span data-stu-id="003fe-458">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="003fe-459">String</span><span class="sxs-lookup"><span data-stu-id="003fe-459">String</span></span>|<span data-ttu-id="003fe-460">128文字</span><span class="sxs-lookup"><span data-stu-id="003fe-460">128 characters</span></span>||<span data-ttu-id="003fe-461">の`fetchTask: true`タスクモジュールに表示されるコントロールの種類を定義します。</span><span class="sxs-lookup"><span data-stu-id="003fe-461">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="003fe-462">、 `text` `textarea` `number` `date`、、、、、のいずれかの`time` `toggle``choiceset`</span><span class="sxs-lookup"><span data-stu-id="003fe-462">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="003fe-463">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="003fe-463">Array of Objects</span></span>|<span data-ttu-id="003fe-464">10 </span><span class="sxs-lookup"><span data-stu-id="003fe-464">10</span></span>||<span data-ttu-id="003fe-465">の選択オプション`choiceset`。</span><span class="sxs-lookup"><span data-stu-id="003fe-465">The choice options for the `choiceset`.</span></span> <span data-ttu-id="003fe-466">がである`parameter.inputType`場合にのみ使用します`choiceset`</span><span class="sxs-lookup"><span data-stu-id="003fe-466">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="003fe-467">String</span><span class="sxs-lookup"><span data-stu-id="003fe-467">String</span></span>|<span data-ttu-id="003fe-468">128</span><span class="sxs-lookup"><span data-stu-id="003fe-468">128</span></span>||<span data-ttu-id="003fe-469">選択肢のタイトル</span><span class="sxs-lookup"><span data-stu-id="003fe-469">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="003fe-470">String</span><span class="sxs-lookup"><span data-stu-id="003fe-470">String</span></span>|<span data-ttu-id="003fe-471">512</span><span class="sxs-lookup"><span data-stu-id="003fe-471">512</span></span>||<span data-ttu-id="003fe-472">選択肢の値</span><span class="sxs-lookup"><span data-stu-id="003fe-472">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="003fe-473">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="003fe-473">permissions</span></span>

<span data-ttu-id="003fe-474">**Optional**</span><span class="sxs-lookup"><span data-stu-id="003fe-474">**Optional**</span></span>

<span data-ttu-id="003fe-475">アプリが要求`string`するアクセス許可を指定する配列。これにより、エンドユーザーは拡張機能の動作を知ることができます。</span><span class="sxs-lookup"><span data-stu-id="003fe-475">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="003fe-476">非排他的なオプションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="003fe-476">The following options are non-exclusive:</span></span>

* <span data-ttu-id="003fe-477">`identity`&emsp;ユーザー id 情報が必要</span><span class="sxs-lookup"><span data-stu-id="003fe-477">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="003fe-478">`messageTeamMembers`&emsp;チームメンバーに直接メッセージを送信するためのアクセス許可が必要</span><span class="sxs-lookup"><span data-stu-id="003fe-478">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="003fe-479">アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは、更新されたアプリを初めて実行したときに同意プロセスを繰り返すようになります。</span><span class="sxs-lookup"><span data-stu-id="003fe-479">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="003fe-480">詳細については[、「アプリの更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="003fe-480">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="003fe-481">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="003fe-481">devicePermissions</span></span>

<span data-ttu-id="003fe-482">**省略可能**文字列の配列</span><span class="sxs-lookup"><span data-stu-id="003fe-482">**Optional** Array of Strings</span></span>

<span data-ttu-id="003fe-483">アプリがアクセスを要求することができる、ユーザーのデバイスのネイティブ機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="003fe-483">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="003fe-484">オプションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="003fe-484">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="003fe-485">validDomains</span><span class="sxs-lookup"><span data-stu-id="003fe-485">validDomains</span></span>

<span data-ttu-id="003fe-486">**省略可能**(記載個所に**必要な**場合を除く)</span><span class="sxs-lookup"><span data-stu-id="003fe-486">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="003fe-487">アプリが Teams クライアント内で読み込むことが想定されている web サイトの有効なドメインの一覧。</span><span class="sxs-lookup"><span data-stu-id="003fe-487">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="003fe-488">ドメインリストには、たとえば`*.example.com`、ワイルドカードを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="003fe-488">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="003fe-489">これは、1つのドメインのセグメントに一致します。に一致`a.b.example.com`させる必要がある`*.*.example.com`場合は、を使用します。</span><span class="sxs-lookup"><span data-stu-id="003fe-489">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="003fe-490">タブ構成またはコンテンツ UI が他のドメインに移動する必要がある場合 (タブの構成に使用するものを除く)、そのドメインをここで指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-490">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="003fe-491">ただし、アプリでサポートする id プロバイダーのドメインを含める必要は**ありません**。</span><span class="sxs-lookup"><span data-stu-id="003fe-491">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="003fe-492">たとえば、Google ID を使用して認証するには、accounts.google.com にリダイレクトする必要がありますが、に`validDomains[]`accounts.google.com を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="003fe-492">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="003fe-493">自分の sharepoint Url が適切に機能する必要がある Teams アプリは、有効なドメインリストに "{teamsitedomain}" を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="003fe-493">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="003fe-494">直接に、またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しないでください。</span><span class="sxs-lookup"><span data-stu-id="003fe-494">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="003fe-495">たとえば、は`yourapp.onmicrosoft.com`有効`*.onmicrosoft.com`ですが、有効ではありません。</span><span class="sxs-lookup"><span data-stu-id="003fe-495">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="003fe-496">Object は、型`string`のすべての要素を含む配列です。</span><span class="sxs-lookup"><span data-stu-id="003fe-496">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="003fe-497">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="003fe-497">webApplicationInfo</span></span>

<span data-ttu-id="003fe-498">**Optional**</span><span class="sxs-lookup"><span data-stu-id="003fe-498">**Optional**</span></span>

<span data-ttu-id="003fe-499">Aad アプリ ID とグラフ情報を指定して、ユーザーが AAD アプリにシームレスにサインインできるようにします。</span><span class="sxs-lookup"><span data-stu-id="003fe-499">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="003fe-500">名前</span><span class="sxs-lookup"><span data-stu-id="003fe-500">Name</span></span>| <span data-ttu-id="003fe-501">型</span><span class="sxs-lookup"><span data-stu-id="003fe-501">Type</span></span>| <span data-ttu-id="003fe-502">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="003fe-502">Maximum size</span></span> | <span data-ttu-id="003fe-503">必須</span><span class="sxs-lookup"><span data-stu-id="003fe-503">Required</span></span> | <span data-ttu-id="003fe-504">説明</span><span class="sxs-lookup"><span data-stu-id="003fe-504">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="003fe-505">String</span><span class="sxs-lookup"><span data-stu-id="003fe-505">String</span></span>|<span data-ttu-id="003fe-506">36文字</span><span class="sxs-lookup"><span data-stu-id="003fe-506">36 characters</span></span>|<span data-ttu-id="003fe-507">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-507">✔</span></span>|<span data-ttu-id="003fe-508">アプリの AAD アプリケーション id。</span><span class="sxs-lookup"><span data-stu-id="003fe-508">AAD application id of the app.</span></span> <span data-ttu-id="003fe-509">この id は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="003fe-509">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="003fe-510">String</span><span class="sxs-lookup"><span data-stu-id="003fe-510">String</span></span>|<span data-ttu-id="003fe-511">2048 文字</span><span class="sxs-lookup"><span data-stu-id="003fe-511">2048 characters</span></span>|<span data-ttu-id="003fe-512">✔</span><span class="sxs-lookup"><span data-stu-id="003fe-512">✔</span></span>|<span data-ttu-id="003fe-513">SSO の認証トークンを取得するためのアプリのリソース url。</span><span class="sxs-lookup"><span data-stu-id="003fe-513">Resource url of app for acquiring auth token for SSO.</span></span>|
