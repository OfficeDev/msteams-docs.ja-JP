---
title: Developer Preview マニフェスト スキーマ参照
description: マニフェストでサポートされているスキーマについて説明Microsoft Teams
ms.topic: reference
keywords: teams マニフェスト スキーマ Developer Preview
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: c2009038341a22664b0f055fa9756a9d1eba87b9
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915091"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="501f2-104">開発者プレビュー マニフェスト スキーマ (Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="501f2-104">Developer preview manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="501f2-105">開発者プレビューを有効にする方法については、「開発者向けパブリック プレビュー」[を参照Microsoft Teams。](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="501f2-105">For information on how to enable developer preview, see [public developer preview for Microsoft Teams](~/resources/dev-preview/developer-preview-intro.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="501f2-106">開発者プレビュー機能を使用していない場合は、代わりに GA 機能の [アプリ マニフェストを](~/resources/schema/manifest-schema.md) 使用します。</span><span class="sxs-lookup"><span data-stu-id="501f2-106">If you aren't using developer preview features, use the [app manifest for GA features](~/resources/schema/manifest-schema.md) instead.</span></span>

<span data-ttu-id="501f2-107">このMicrosoft Teamsマニフェストは、アプリが製品に統合する方法Microsoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="501f2-107">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="501f2-108">マニフェストは、 でホストされるスキーマに準拠している必要があります [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="501f2-108">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="501f2-109">利用可能な機能の詳細については、「パブリック サイトの機能」を参照Developer Preview[を参照Microsoft Teams。](~/resources/dev-preview/developer-preview-features.md)</span><span class="sxs-lookup"><span data-stu-id="501f2-109">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="501f2-110">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="501f2-110">Sample full manifest</span></span>

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
      "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
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
  ],
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  }
}
```

<span data-ttu-id="501f2-111">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="501f2-111">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="501f2-112">$schema</span><span class="sxs-lookup"><span data-stu-id="501f2-112">$schema</span></span>

<span data-ttu-id="501f2-113">*省略可能ですが、推奨* &ndash; 文字列</span><span class="sxs-lookup"><span data-stu-id="501f2-113">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="501f2-114">マニフェスト https:// JSON スキーマを参照する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-114">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="501f2-115">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="501f2-115">manifestVersion</span></span>

<span data-ttu-id="501f2-116">**必須** &ndash; 文字列</span><span class="sxs-lookup"><span data-stu-id="501f2-116">**Required** &ndash; String</span></span>

<span data-ttu-id="501f2-117">このマニフェストが使用しているマニフェスト スキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="501f2-117">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="501f2-118">"devPreview" である必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-118">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="501f2-119">version</span><span class="sxs-lookup"><span data-stu-id="501f2-119">version</span></span>

<span data-ttu-id="501f2-120">**必須** &ndash; 文字列</span><span class="sxs-lookup"><span data-stu-id="501f2-120">**Required** &ndash; String</span></span>

<span data-ttu-id="501f2-121">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="501f2-121">The version of the specific app.</span></span> <span data-ttu-id="501f2-122">マニフェストで何かを更新する場合は、バージョンも増分する必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-122">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="501f2-123">このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。</span><span class="sxs-lookup"><span data-stu-id="501f2-123">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="501f2-124">このアプリがストアに送信された場合、新しいマニフェストを再送信して再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-124">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="501f2-125">次に、このアプリのユーザーは、承認された後、数時間で新しい更新されたマニフェストを自動的に取得します。</span><span class="sxs-lookup"><span data-stu-id="501f2-125">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="501f2-126">アプリがアクセス許可の変更を要求した場合、ユーザーはアプリのアップグレードと再同意を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="501f2-126">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="501f2-127">このバージョンの文字列は [、semver](http://semver.org/) 標準 (MAJOR) に従う必要があります。MINOR。PATCH)。</span><span class="sxs-lookup"><span data-stu-id="501f2-127">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="501f2-128">id</span><span class="sxs-lookup"><span data-stu-id="501f2-128">id</span></span>

<span data-ttu-id="501f2-129">**必須** &ndash; Microsoft アプリ ID</span><span class="sxs-lookup"><span data-stu-id="501f2-129">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="501f2-130">このアプリの Microsoft が生成した一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="501f2-130">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="501f2-131">ボットを Microsoft Bot Framework 経由で登録している場合、またはタブの Web アプリが既に Microsoft にサインインしている場合は、既に ID を持っている必要があります。ここで入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-131">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="501f2-132">それ以外の場合は、Microsoft アプリケーション登録ポータル[(My Applications)](https://apps.dev.microsoft.com)で新しい ID を生成し、ここに入力し、ボットを追加するときに再利用 [する必要があります](~/bots/how-to/create-a-bot-for-teams.md)。</span><span class="sxs-lookup"><span data-stu-id="501f2-132">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="501f2-133">packageName</span><span class="sxs-lookup"><span data-stu-id="501f2-133">packageName</span></span>

<span data-ttu-id="501f2-134">**必須** &ndash; 文字列</span><span class="sxs-lookup"><span data-stu-id="501f2-134">**Required** &ndash; String</span></span>

<span data-ttu-id="501f2-135">逆ドメイン表記でこのアプリの一意の識別子。たとえば、com.example.myapp などです。</span><span class="sxs-lookup"><span data-stu-id="501f2-135">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="501f2-136">developer</span><span class="sxs-lookup"><span data-stu-id="501f2-136">developer</span></span>

<span data-ttu-id="501f2-137">**必須**</span><span class="sxs-lookup"><span data-stu-id="501f2-137">**Required**</span></span>

<span data-ttu-id="501f2-138">会社に関する情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-138">Specifies information about your company.</span></span> <span data-ttu-id="501f2-139">AppSource に送信されたアプリ (以前Officeストア) の場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-139">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="501f2-140">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-140">Name</span></span>| <span data-ttu-id="501f2-141">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-141">Maximum size</span></span> | <span data-ttu-id="501f2-142">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-142">Required</span></span> | <span data-ttu-id="501f2-143">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="501f2-144">32 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-144">32 characters</span></span>|<span data-ttu-id="501f2-145">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-145">✔</span></span>|<span data-ttu-id="501f2-146">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="501f2-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="501f2-147">2048 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-147">2048 characters</span></span>|<span data-ttu-id="501f2-148">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-148">✔</span></span>|<span data-ttu-id="501f2-149">開発者 https:// WEB サイトの URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="501f2-150">このリンクは、ユーザーを会社または製品固有のランディング ページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="501f2-151">2048 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-151">2048 characters</span></span>|<span data-ttu-id="501f2-152">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-152">✔</span></span>|<span data-ttu-id="501f2-153">開発者 https:// のプライバシー ポリシーの URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="501f2-154">2048 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-154">2048 characters</span></span>|<span data-ttu-id="501f2-155">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-155">✔</span></span>|<span data-ttu-id="501f2-156">開発者 https:// の使用条件の URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="501f2-157">10 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-157">10 characters</span></span>|<span data-ttu-id="501f2-158">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-158">✔</span></span>|<span data-ttu-id="501f2-159">**省略可能** アプリを構築するパートナー組織を識別する Microsoft パートナー ネットワーク ID。</span><span class="sxs-lookup"><span data-stu-id="501f2-159">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="501f2-160">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="501f2-160">localizationInfo</span></span>

<span data-ttu-id="501f2-161">**Optional**</span><span class="sxs-lookup"><span data-stu-id="501f2-161">**Optional**</span></span>

<span data-ttu-id="501f2-162">既定の言語の指定と、追加の言語ファイルへのポインターを許可します。</span><span class="sxs-lookup"><span data-stu-id="501f2-162">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="501f2-163">「ローカライズ」 [を参照してください](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="501f2-163">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="501f2-164">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-164">Name</span></span>| <span data-ttu-id="501f2-165">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-165">Maximum size</span></span> | <span data-ttu-id="501f2-166">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-166">Required</span></span> | <span data-ttu-id="501f2-167">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-167">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="501f2-168">4 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-168">4 characters</span></span>|<span data-ttu-id="501f2-169">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-169">✔</span></span>|<span data-ttu-id="501f2-170">このトップ レベルのマニフェスト ファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="501f2-170">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="501f2-171">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="501f2-171">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="501f2-172">追加の言語変換を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="501f2-172">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="501f2-173">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-173">Name</span></span>| <span data-ttu-id="501f2-174">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-174">Maximum size</span></span> | <span data-ttu-id="501f2-175">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-175">Required</span></span> | <span data-ttu-id="501f2-176">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-176">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="501f2-177">4 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-177">4 characters</span></span>|<span data-ttu-id="501f2-178">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-178">✔</span></span>|<span data-ttu-id="501f2-179">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="501f2-179">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="501f2-180">4 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-180">4 characters</span></span>|<span data-ttu-id="501f2-181">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-181">✔</span></span>|<span data-ttu-id="501f2-182">翻訳された文字列を含む .json ファイルへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="501f2-182">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="501f2-183">name</span><span class="sxs-lookup"><span data-stu-id="501f2-183">name</span></span>

<span data-ttu-id="501f2-184">**必須**</span><span class="sxs-lookup"><span data-stu-id="501f2-184">**Required**</span></span>

<span data-ttu-id="501f2-185">アプリ エクスペリエンスのユーザーに表示されるアプリ エクスペリエンスのTeamsします。</span><span class="sxs-lookup"><span data-stu-id="501f2-185">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="501f2-186">AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-186">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="501f2-187">の値 `short` と `full` 同じ値にしない必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-187">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="501f2-188">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-188">Name</span></span>| <span data-ttu-id="501f2-189">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-189">Maximum size</span></span> | <span data-ttu-id="501f2-190">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-190">Required</span></span> | <span data-ttu-id="501f2-191">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-191">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="501f2-192">30 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-192">30 characters</span></span>|<span data-ttu-id="501f2-193">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-193">✔</span></span>|<span data-ttu-id="501f2-194">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="501f2-194">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="501f2-195">100 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-195">100 characters</span></span>||<span data-ttu-id="501f2-196">完全なアプリ名が 30 文字を超える場合に使用されるアプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="501f2-196">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="501f2-197">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-197">description</span></span>

<span data-ttu-id="501f2-198">**必須**</span><span class="sxs-lookup"><span data-stu-id="501f2-198">**Required**</span></span>

<span data-ttu-id="501f2-199">アプリをユーザーに説明します。</span><span class="sxs-lookup"><span data-stu-id="501f2-199">Describes your app to users.</span></span> <span data-ttu-id="501f2-200">AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-200">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="501f2-201">説明がエクスペリエンスを正確に説明し、潜在的な顧客がエクスペリエンスの内容を理解するのに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="501f2-201">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="501f2-202">また、外部アカウントの使用が必要な場合は、完全な説明に注意してください。</span><span class="sxs-lookup"><span data-stu-id="501f2-202">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="501f2-203">の値 `short` と `full` 同じ値にしない必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-203">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="501f2-204">短い説明は、長い説明の中で繰り返し実行し、他のアプリ名を含めずに行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-204">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="501f2-205">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-205">Name</span></span>| <span data-ttu-id="501f2-206">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-206">Maximum size</span></span> | <span data-ttu-id="501f2-207">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-207">Required</span></span> | <span data-ttu-id="501f2-208">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-208">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="501f2-209">80 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-209">80 characters</span></span>|<span data-ttu-id="501f2-210">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-210">✔</span></span>|<span data-ttu-id="501f2-211">スペースが制限されている場合に使用されるアプリ エクスペリエンスの簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="501f2-211">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="501f2-212">4000 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-212">4000 characters</span></span>|<span data-ttu-id="501f2-213">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-213">✔</span></span>|<span data-ttu-id="501f2-214">アプリの完全な説明。</span><span class="sxs-lookup"><span data-stu-id="501f2-214">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="501f2-215">アイコン</span><span class="sxs-lookup"><span data-stu-id="501f2-215">icons</span></span>

<span data-ttu-id="501f2-216">**必須**</span><span class="sxs-lookup"><span data-stu-id="501f2-216">**Required**</span></span>

<span data-ttu-id="501f2-217">アプリ内で使用Teamsアイコン。</span><span class="sxs-lookup"><span data-stu-id="501f2-217">Icons used within the Teams app.</span></span> <span data-ttu-id="501f2-218">アイコン ファイルは、アップロード パッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-218">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="501f2-219">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-219">Name</span></span>| <span data-ttu-id="501f2-220">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-220">Maximum size</span></span> | <span data-ttu-id="501f2-221">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-221">Required</span></span> | <span data-ttu-id="501f2-222">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-222">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="501f2-223">2048 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-223">2048 characters</span></span>|<span data-ttu-id="501f2-224">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-224">✔</span></span>|<span data-ttu-id="501f2-225">透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="501f2-225">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="501f2-226">2048 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-226">2048 characters</span></span>|<span data-ttu-id="501f2-227">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-227">✔</span></span>|<span data-ttu-id="501f2-228">フル カラーの 192x192 PNG アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="501f2-228">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="501f2-229">accentColor</span><span class="sxs-lookup"><span data-stu-id="501f2-229">accentColor</span></span>

<span data-ttu-id="501f2-230">**必須** &ndash; 文字列</span><span class="sxs-lookup"><span data-stu-id="501f2-230">**Required** &ndash; String</span></span>

<span data-ttu-id="501f2-231">アウトライン アイコンと組み合わせて、背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="501f2-231">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="501f2-232">値は、'#' で始まる有効な HTML カラー コードである必要があります `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-232">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="501f2-233">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="501f2-233">configurableTabs</span></span>

<span data-ttu-id="501f2-234">**Optional**</span><span class="sxs-lookup"><span data-stu-id="501f2-234">**Optional**</span></span>

<span data-ttu-id="501f2-235">アプリ エクスペリエンスに、追加する前に追加の構成が必要なチーム チャネル タブ エクスペリエンスがある場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="501f2-235">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="501f2-236">構成可能なタブは teams スコープでのみサポートされ、現在はアプリごとに 1 つのタブしかサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="501f2-236">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="501f2-237">オブジェクトは、型のすべての要素を持つ配列です `object` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-237">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="501f2-238">このブロックは、構成可能なチャネル タブ ソリューションを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="501f2-238">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="501f2-239">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-239">Name</span></span>| <span data-ttu-id="501f2-240">型</span><span class="sxs-lookup"><span data-stu-id="501f2-240">Type</span></span>| <span data-ttu-id="501f2-241">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-241">Maximum size</span></span> | <span data-ttu-id="501f2-242">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-242">Required</span></span> | <span data-ttu-id="501f2-243">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-243">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="501f2-244">String</span><span class="sxs-lookup"><span data-stu-id="501f2-244">String</span></span>|<span data-ttu-id="501f2-245">2048 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-245">2048 characters</span></span>|<span data-ttu-id="501f2-246">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-246">✔</span></span>|<span data-ttu-id="501f2-247">タブ https:// する際に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-247">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="501f2-248">Boolean</span><span class="sxs-lookup"><span data-stu-id="501f2-248">Boolean</span></span>|||<span data-ttu-id="501f2-249">作成後に、タブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="501f2-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="501f2-250">既定値: `true`</span><span class="sxs-lookup"><span data-stu-id="501f2-250">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="501f2-251">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="501f2-251">Array of enum</span></span>|<span data-ttu-id="501f2-252">1</span><span class="sxs-lookup"><span data-stu-id="501f2-252">1</span></span>|<span data-ttu-id="501f2-253">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-253">✔</span></span>|<span data-ttu-id="501f2-254">現在、構成可能なタブは、スコープ `team` とスコープ `groupchat` のみをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="501f2-254">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="501f2-255">String</span><span class="sxs-lookup"><span data-stu-id="501f2-255">String</span></span>|<span data-ttu-id="501f2-256">2048</span><span class="sxs-lookup"><span data-stu-id="501f2-256">2048</span></span>||<span data-ttu-id="501f2-257">タブ プレビュー イメージへの相対ファイル パスを使用して、SharePoint。</span><span class="sxs-lookup"><span data-stu-id="501f2-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="501f2-258">サイズは 1024x768 です。</span><span class="sxs-lookup"><span data-stu-id="501f2-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="501f2-259">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="501f2-259">Array of enum</span></span>|<span data-ttu-id="501f2-260">1</span><span class="sxs-lookup"><span data-stu-id="501f2-260">1</span></span>||<span data-ttu-id="501f2-261">タブをタブで使用する方法を定義SharePoint。</span><span class="sxs-lookup"><span data-stu-id="501f2-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="501f2-262">オプションは `sharePointFullPage` 次のとおりです。 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="501f2-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="501f2-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="501f2-263">staticTabs</span></span>

<span data-ttu-id="501f2-264">**Optional**</span><span class="sxs-lookup"><span data-stu-id="501f2-264">**Optional**</span></span>

<span data-ttu-id="501f2-265">ユーザーが手動で追加せずに、既定で "ピン留め" できるタブのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="501f2-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="501f2-266">スコープ内で宣言された静的タブ `personal` は、常にアプリの個人用エクスペリエンスにピン留めされます。</span><span class="sxs-lookup"><span data-stu-id="501f2-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="501f2-267">スコープで宣言されている静的タブ `team` は現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="501f2-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="501f2-268">staticTabs ブロックではなく、アダプティブ カードを使用してタブ `contentBotId` `contentUrl` **をレンダリング** します。</span><span class="sxs-lookup"><span data-stu-id="501f2-268">Render tabs with Adaptive Cards by specifying `contentBotId` instead of `contentUrl` in the **staticTabs** block.</span></span>

<span data-ttu-id="501f2-269">オブジェクトは、型のすべての要素を持つ配列 (最大 16 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="501f2-270">このブロックは、静的タブ ソリューションを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="501f2-270">This block is required only for solutions that provide a static tab solution.</span></span>


|<span data-ttu-id="501f2-271">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-271">Name</span></span>| <span data-ttu-id="501f2-272">型</span><span class="sxs-lookup"><span data-stu-id="501f2-272">Type</span></span>| <span data-ttu-id="501f2-273">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-273">Maximum size</span></span> | <span data-ttu-id="501f2-274">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-274">Required</span></span> | <span data-ttu-id="501f2-275">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="501f2-276">String</span><span class="sxs-lookup"><span data-stu-id="501f2-276">String</span></span>|<span data-ttu-id="501f2-277">64 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-277">64 characters</span></span>|<span data-ttu-id="501f2-278">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-278">✔</span></span>|<span data-ttu-id="501f2-279">タブが表示されるエンティティの一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="501f2-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="501f2-280">String</span><span class="sxs-lookup"><span data-stu-id="501f2-280">String</span></span>|<span data-ttu-id="501f2-281">128 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-281">128 characters</span></span>|<span data-ttu-id="501f2-282">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-282">✔</span></span>|<span data-ttu-id="501f2-283">チャネル インターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="501f2-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="501f2-284">String</span><span class="sxs-lookup"><span data-stu-id="501f2-284">String</span></span>|<span data-ttu-id="501f2-285">2048 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-285">2048 characters</span></span>|<span data-ttu-id="501f2-286">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-286">✔</span></span>|<span data-ttu-id="501f2-287">この https:// キャンバスに表示するエンティティ UI を示すTeamsします。</span><span class="sxs-lookup"><span data-stu-id="501f2-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`contentBotId`|   | | | <span data-ttu-id="501f2-288">ボット Microsoft Teamsで指定されたアプリ ID を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-288">The Microsoft Teams app ID specified for the bot in the Bot Framework portal.</span></span> |
|`websiteUrl`|<span data-ttu-id="501f2-289">String</span><span class="sxs-lookup"><span data-stu-id="501f2-289">String</span></span>|<span data-ttu-id="501f2-290">2048 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-290">2048 characters</span></span>||<span data-ttu-id="501f2-291">ユーザー https:// ブラウザーで表示することを選択した場合に示す URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-291">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="501f2-292">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="501f2-292">Array of enum</span></span>|<span data-ttu-id="501f2-293">1</span><span class="sxs-lookup"><span data-stu-id="501f2-293">1</span></span>|<span data-ttu-id="501f2-294">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-294">✔</span></span>|<span data-ttu-id="501f2-295">現在、静的タブはスコープのみをサポートしています。つまり、個人用エクスペリエンスの一部としてのみ `personal` プロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="501f2-295">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="501f2-296">bots</span><span class="sxs-lookup"><span data-stu-id="501f2-296">bots</span></span>

<span data-ttu-id="501f2-297">**Optional**</span><span class="sxs-lookup"><span data-stu-id="501f2-297">**Optional**</span></span>

<span data-ttu-id="501f2-298">既定のコマンド プロパティなどのオプションの情報と共に、ボット ソリューションを定義します。</span><span class="sxs-lookup"><span data-stu-id="501f2-298">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="501f2-299">オブジェクトは、型のすべての要素を持つ配列 (現在、1 つのボットにつき 1 つのボットしか許可されていない &mdash; 最大 1 つの要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-299">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="501f2-300">このブロックは、ボット エクスペリエンスを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="501f2-300">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="501f2-301">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-301">Name</span></span>| <span data-ttu-id="501f2-302">型</span><span class="sxs-lookup"><span data-stu-id="501f2-302">Type</span></span>| <span data-ttu-id="501f2-303">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-303">Maximum size</span></span> | <span data-ttu-id="501f2-304">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-304">Required</span></span> | <span data-ttu-id="501f2-305">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-305">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="501f2-306">String</span><span class="sxs-lookup"><span data-stu-id="501f2-306">String</span></span>|<span data-ttu-id="501f2-307">64 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-307">64 characters</span></span>|<span data-ttu-id="501f2-308">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-308">✔</span></span>|<span data-ttu-id="501f2-309">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="501f2-309">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="501f2-310">これは、アプリ全体の ID と同じ [可能性があります](#id)。</span><span class="sxs-lookup"><span data-stu-id="501f2-310">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="501f2-311">Boolean</span><span class="sxs-lookup"><span data-stu-id="501f2-311">Boolean</span></span>|||<span data-ttu-id="501f2-312">ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。</span><span class="sxs-lookup"><span data-stu-id="501f2-312">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="501f2-313">既定値: `false`</span><span class="sxs-lookup"><span data-stu-id="501f2-313">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="501f2-314">Boolean</span><span class="sxs-lookup"><span data-stu-id="501f2-314">Boolean</span></span>|||<span data-ttu-id="501f2-315">ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="501f2-315">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="501f2-316">既定値: `false`</span><span class="sxs-lookup"><span data-stu-id="501f2-316">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="501f2-317">Boolean</span><span class="sxs-lookup"><span data-stu-id="501f2-317">Boolean</span></span>|||<span data-ttu-id="501f2-318">パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="501f2-318">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="501f2-319">既定値: `false`</span><span class="sxs-lookup"><span data-stu-id="501f2-319">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="501f2-320">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="501f2-320">Array of enum</span></span>|<span data-ttu-id="501f2-321">3</span><span class="sxs-lookup"><span data-stu-id="501f2-321">3</span></span>|<span data-ttu-id="501f2-322">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-322">✔</span></span>|<span data-ttu-id="501f2-323">ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-323">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="501f2-324">これらのオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="501f2-324">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="501f2-325">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="501f2-325">bots.commandLists</span></span>

<span data-ttu-id="501f2-326">ボットがユーザーに推奨できるコマンドのオプションの一覧。</span><span class="sxs-lookup"><span data-stu-id="501f2-326">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="501f2-327">オブジェクトは、型のすべての要素を持つ配列 (最大 2 つの要素) です。ボットがサポートするスコープごとに個別のコマンド リストを `object` 定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-327">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="501f2-328">詳細については、「Bot メニュー [」を参照してください](~/bots/how-to/create-a-bot-commands-menu.md)。</span><span class="sxs-lookup"><span data-stu-id="501f2-328">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="501f2-329">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-329">Name</span></span>| <span data-ttu-id="501f2-330">型</span><span class="sxs-lookup"><span data-stu-id="501f2-330">Type</span></span>| <span data-ttu-id="501f2-331">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-331">Maximum size</span></span> | <span data-ttu-id="501f2-332">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-332">Required</span></span> | <span data-ttu-id="501f2-333">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-333">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="501f2-334">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="501f2-334">array of enum</span></span>|<span data-ttu-id="501f2-335">3</span><span class="sxs-lookup"><span data-stu-id="501f2-335">3</span></span>|<span data-ttu-id="501f2-336">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-336">✔</span></span>|<span data-ttu-id="501f2-337">コマンド リストが有効なスコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-337">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="501f2-338">`team`、`personal`、`groupchat` の中から選択できます。</span><span class="sxs-lookup"><span data-stu-id="501f2-338">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="501f2-339">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="501f2-339">array of objects</span></span>|<span data-ttu-id="501f2-340">10</span><span class="sxs-lookup"><span data-stu-id="501f2-340">10</span></span>|<span data-ttu-id="501f2-341">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-341">✔</span></span>|<span data-ttu-id="501f2-342">ボットがサポートするコマンドの配列:</span><span class="sxs-lookup"><span data-stu-id="501f2-342">An array of commands the bot supports:</span></span><br><span data-ttu-id="501f2-343">`title`: bot コマンド名 (文字列、32)。</span><span class="sxs-lookup"><span data-stu-id="501f2-343">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="501f2-344">`description`: コマンド構文とその引数の簡単な説明または例 (文字列、128)。</span><span class="sxs-lookup"><span data-stu-id="501f2-344">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="501f2-345">コネクタ</span><span class="sxs-lookup"><span data-stu-id="501f2-345">connectors</span></span>

<span data-ttu-id="501f2-346">**Optional**</span><span class="sxs-lookup"><span data-stu-id="501f2-346">**Optional**</span></span>

<span data-ttu-id="501f2-347">ブロック `connectors` は、アプリOffice 365コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="501f2-347">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="501f2-348">オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-348">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="501f2-349">このブロックは、Connector を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="501f2-349">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="501f2-350">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-350">Name</span></span>| <span data-ttu-id="501f2-351">型</span><span class="sxs-lookup"><span data-stu-id="501f2-351">Type</span></span>| <span data-ttu-id="501f2-352">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-352">Maximum size</span></span> | <span data-ttu-id="501f2-353">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-353">Required</span></span> | <span data-ttu-id="501f2-354">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-354">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="501f2-355">String</span><span class="sxs-lookup"><span data-stu-id="501f2-355">String</span></span>|<span data-ttu-id="501f2-356">2048 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-356">2048 characters</span></span>|<span data-ttu-id="501f2-357">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-357">✔</span></span>|<span data-ttu-id="501f2-358">コネクタ https:// する際に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-358">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="501f2-359">String</span><span class="sxs-lookup"><span data-stu-id="501f2-359">String</span></span>|<span data-ttu-id="501f2-360">64 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-360">64 characters</span></span>|<span data-ttu-id="501f2-361">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-361">✔</span></span>|<span data-ttu-id="501f2-362">コネクタ開発者ダッシュボードの ID に一致するコネクタの一 [意の識別子](https://aka.ms/connectorsdashboard)です。</span><span class="sxs-lookup"><span data-stu-id="501f2-362">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="501f2-363">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="501f2-363">Array of enum</span></span>|<span data-ttu-id="501f2-364">1</span><span class="sxs-lookup"><span data-stu-id="501f2-364">1</span></span>|<span data-ttu-id="501f2-365">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-365">✔</span></span>|<span data-ttu-id="501f2-366">Connector がチャネルのコンテキストでエクスペリエンスを提供するかどうか、または個々のユーザー () にスコープを設定したエクスペリエンスを提供するかどうかを `team` 指定します `personal` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-366">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="501f2-367">現在、スコープ `team` だけがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="501f2-367">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="501f2-368">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="501f2-368">composeExtensions</span></span>

<span data-ttu-id="501f2-369">**Optional**</span><span class="sxs-lookup"><span data-stu-id="501f2-369">**Optional**</span></span>

<span data-ttu-id="501f2-370">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="501f2-370">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="501f2-371">機能の名前は、2017 年 11 月に "作成拡張機能" から "メッセージング拡張機能" に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は変わりません。</span><span class="sxs-lookup"><span data-stu-id="501f2-371">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="501f2-372">オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-372">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="501f2-373">このブロックは、メッセージング拡張機能を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="501f2-373">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="501f2-374">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-374">Name</span></span>| <span data-ttu-id="501f2-375">型</span><span class="sxs-lookup"><span data-stu-id="501f2-375">Type</span></span> | <span data-ttu-id="501f2-376">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-376">Maximum Size</span></span> | <span data-ttu-id="501f2-377">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-377">Required</span></span> | <span data-ttu-id="501f2-378">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-378">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="501f2-379">String</span><span class="sxs-lookup"><span data-stu-id="501f2-379">String</span></span>|<span data-ttu-id="501f2-380">64</span><span class="sxs-lookup"><span data-stu-id="501f2-380">64</span></span>|<span data-ttu-id="501f2-381">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-381">✔</span></span>|<span data-ttu-id="501f2-382">ボット フレームワークに登録されているメッセージング拡張機能をバックするボットの一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="501f2-382">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="501f2-383">これは、アプリ全体の ID と同じ [可能性があります](#id)。</span><span class="sxs-lookup"><span data-stu-id="501f2-383">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="501f2-384">Boolean</span><span class="sxs-lookup"><span data-stu-id="501f2-384">Boolean</span></span>|||<span data-ttu-id="501f2-385">メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="501f2-385">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="501f2-386">既定値は `false` です。</span><span class="sxs-lookup"><span data-stu-id="501f2-386">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="501f2-387">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="501f2-387">Array of object</span></span>|<span data-ttu-id="501f2-388">10</span><span class="sxs-lookup"><span data-stu-id="501f2-388">10</span></span>|<span data-ttu-id="501f2-389">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-389">✔</span></span>|<span data-ttu-id="501f2-390">メッセージング拡張機能がサポートするコマンドの配列</span><span class="sxs-lookup"><span data-stu-id="501f2-390">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="501f2-391">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="501f2-391">composeExtensions.commands</span></span>

<span data-ttu-id="501f2-392">メッセージング拡張機能は、1 つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-392">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="501f2-393">各コマンドは、MICROSOFT TEAMSエントリ ポイントからの潜在的な対話として表示されます。</span><span class="sxs-lookup"><span data-stu-id="501f2-393">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="501f2-394">最大 10 のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="501f2-394">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="501f2-395">各コマンド 項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="501f2-395">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="501f2-396">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-396">Name</span></span>| <span data-ttu-id="501f2-397">型</span><span class="sxs-lookup"><span data-stu-id="501f2-397">Type</span></span>| <span data-ttu-id="501f2-398">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-398">Maximum size</span></span> | <span data-ttu-id="501f2-399">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-399">Required</span></span> | <span data-ttu-id="501f2-400">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-400">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="501f2-401">String</span><span class="sxs-lookup"><span data-stu-id="501f2-401">String</span></span>|<span data-ttu-id="501f2-402">64 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-402">64 characters</span></span>|<span data-ttu-id="501f2-403">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-403">✔</span></span>|<span data-ttu-id="501f2-404">コマンドの ID。</span><span class="sxs-lookup"><span data-stu-id="501f2-404">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="501f2-405">String</span><span class="sxs-lookup"><span data-stu-id="501f2-405">String</span></span>|<span data-ttu-id="501f2-406">64 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-406">64 characters</span></span>||<span data-ttu-id="501f2-407">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="501f2-407">Type of the command.</span></span> <span data-ttu-id="501f2-408">または `query` の 1 `action` つ。</span><span class="sxs-lookup"><span data-stu-id="501f2-408">One of `query` or `action`.</span></span> <span data-ttu-id="501f2-409">既定値: `query`</span><span class="sxs-lookup"><span data-stu-id="501f2-409">Default: `query`</span></span>|
|`title`|<span data-ttu-id="501f2-410">String</span><span class="sxs-lookup"><span data-stu-id="501f2-410">String</span></span>|<span data-ttu-id="501f2-411">32 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-411">32 characters</span></span>|<span data-ttu-id="501f2-412">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-412">✔</span></span>|<span data-ttu-id="501f2-413">ユーザーフレンドリーなコマンド名。</span><span class="sxs-lookup"><span data-stu-id="501f2-413">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="501f2-414">String</span><span class="sxs-lookup"><span data-stu-id="501f2-414">String</span></span>|<span data-ttu-id="501f2-415">128 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-415">128 characters</span></span>||<span data-ttu-id="501f2-416">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="501f2-416">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="501f2-417">Boolean</span><span class="sxs-lookup"><span data-stu-id="501f2-417">Boolean</span></span>|||<span data-ttu-id="501f2-418">パラメーターを指定してコマンドを最初に実行するかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="501f2-418">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="501f2-419">既定値: `false`</span><span class="sxs-lookup"><span data-stu-id="501f2-419">Default: `false`</span></span>|
|`context`|<span data-ttu-id="501f2-420">文字列 (String) の配列</span><span class="sxs-lookup"><span data-stu-id="501f2-420">Array of Strings</span></span>|<span data-ttu-id="501f2-421">3</span><span class="sxs-lookup"><span data-stu-id="501f2-421">3</span></span>||<span data-ttu-id="501f2-422">メッセージ拡張機能の呼び出し先を定義します。</span><span class="sxs-lookup"><span data-stu-id="501f2-422">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="501f2-423">`compose`、 の任意の `commandBox` 組み合 `message` わせ。</span><span class="sxs-lookup"><span data-stu-id="501f2-423">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="501f2-424">既定値は `["compose", "commandBox"]` です</span><span class="sxs-lookup"><span data-stu-id="501f2-424">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="501f2-425">Boolean</span><span class="sxs-lookup"><span data-stu-id="501f2-425">Boolean</span></span>|||<span data-ttu-id="501f2-426">タスク モジュールを動的にフェッチする必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="501f2-426">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="501f2-427">オブジェクト</span><span class="sxs-lookup"><span data-stu-id="501f2-427">Object</span></span>|||<span data-ttu-id="501f2-428">メッセージング拡張機能コマンドを使用するときにプリロードするタスク モジュールを指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-428">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="501f2-429">String</span><span class="sxs-lookup"><span data-stu-id="501f2-429">String</span></span>|<span data-ttu-id="501f2-430">64</span><span class="sxs-lookup"><span data-stu-id="501f2-430">64</span></span>||<span data-ttu-id="501f2-431">最初のダイアログ タイトル。</span><span class="sxs-lookup"><span data-stu-id="501f2-431">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="501f2-432">String</span><span class="sxs-lookup"><span data-stu-id="501f2-432">String</span></span>|||<span data-ttu-id="501f2-433">ダイアログの幅 - ピクセル単位の数値または既定のレイアウト ('large'、'medium'、または 'small' など)。</span><span class="sxs-lookup"><span data-stu-id="501f2-433">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="501f2-434">String</span><span class="sxs-lookup"><span data-stu-id="501f2-434">String</span></span>|||<span data-ttu-id="501f2-435">ダイアログの高さ - ピクセル単位の数値、または 'large'、'medium'、または 'small' などの既定のレイアウト。</span><span class="sxs-lookup"><span data-stu-id="501f2-435">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="501f2-436">String</span><span class="sxs-lookup"><span data-stu-id="501f2-436">String</span></span>|||<span data-ttu-id="501f2-437">初期 Webview URL。</span><span class="sxs-lookup"><span data-stu-id="501f2-437">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="501f2-438">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="501f2-438">Array of Objects</span></span>|<span data-ttu-id="501f2-439">5</span><span class="sxs-lookup"><span data-stu-id="501f2-439">5</span></span>||<span data-ttu-id="501f2-440">特定の条件が満たされた場合にアプリを呼び出すことができるハンドラーの一覧。</span><span class="sxs-lookup"><span data-stu-id="501f2-440">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="501f2-441">ドメインもに一覧表示する必要があります `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-441">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="501f2-442">String</span><span class="sxs-lookup"><span data-stu-id="501f2-442">String</span></span>|||<span data-ttu-id="501f2-443">メッセージ ハンドラーの種類。</span><span class="sxs-lookup"><span data-stu-id="501f2-443">The type of message handler.</span></span> <span data-ttu-id="501f2-444">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-444">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="501f2-445">文字列 (String) の配列</span><span class="sxs-lookup"><span data-stu-id="501f2-445">Array of Strings</span></span>|||<span data-ttu-id="501f2-446">リンク メッセージ ハンドラーが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="501f2-446">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="501f2-447">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="501f2-447">Array of object</span></span>|<span data-ttu-id="501f2-448">5</span><span class="sxs-lookup"><span data-stu-id="501f2-448">5</span></span>|<span data-ttu-id="501f2-449">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-449">✔</span></span>|<span data-ttu-id="501f2-450">コマンドが受け取るパラメーターの一覧。</span><span class="sxs-lookup"><span data-stu-id="501f2-450">The list of parameters the command takes.</span></span> <span data-ttu-id="501f2-451">最小: 1;最大: 5</span><span class="sxs-lookup"><span data-stu-id="501f2-451">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="501f2-452">String</span><span class="sxs-lookup"><span data-stu-id="501f2-452">String</span></span>|<span data-ttu-id="501f2-453">64 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-453">64 characters</span></span>|<span data-ttu-id="501f2-454">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-454">✔</span></span>|<span data-ttu-id="501f2-455">クライアントに表示されるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="501f2-455">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="501f2-456">これは、ユーザー要求に含まれます。</span><span class="sxs-lookup"><span data-stu-id="501f2-456">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="501f2-457">String</span><span class="sxs-lookup"><span data-stu-id="501f2-457">String</span></span>|<span data-ttu-id="501f2-458">32 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-458">32 characters</span></span>|<span data-ttu-id="501f2-459">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-459">✔</span></span>|<span data-ttu-id="501f2-460">パラメーターのユーザーフレンドリーなタイトル。</span><span class="sxs-lookup"><span data-stu-id="501f2-460">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="501f2-461">String</span><span class="sxs-lookup"><span data-stu-id="501f2-461">String</span></span>|<span data-ttu-id="501f2-462">128 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-462">128 characters</span></span>||<span data-ttu-id="501f2-463">このパラメーターの目的を説明するユーザーフレンドリーな文字列。</span><span class="sxs-lookup"><span data-stu-id="501f2-463">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="501f2-464">String</span><span class="sxs-lookup"><span data-stu-id="501f2-464">String</span></span>|<span data-ttu-id="501f2-465">128 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-465">128 characters</span></span>||<span data-ttu-id="501f2-466">タスク モジュールに表示されるコントロールの種類を定義します `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-466">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="501f2-467">、 `text` `textarea` 、 、 、 、 の `number` `date` `time` `toggle` 1 `choiceset` つ。</span><span class="sxs-lookup"><span data-stu-id="501f2-467">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="501f2-468">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="501f2-468">Array of Objects</span></span>|<span data-ttu-id="501f2-469">10</span><span class="sxs-lookup"><span data-stu-id="501f2-469">10</span></span>||<span data-ttu-id="501f2-470">の選択肢 `choiceset` オプションです。</span><span class="sxs-lookup"><span data-stu-id="501f2-470">The choice options for the `choiceset`.</span></span> <span data-ttu-id="501f2-471">の場合にのみ `parameter.inputType` 使用します `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-471">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="501f2-472">String</span><span class="sxs-lookup"><span data-stu-id="501f2-472">String</span></span>|<span data-ttu-id="501f2-473">128</span><span class="sxs-lookup"><span data-stu-id="501f2-473">128</span></span>||<span data-ttu-id="501f2-474">選択したタイトル。</span><span class="sxs-lookup"><span data-stu-id="501f2-474">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="501f2-475">String</span><span class="sxs-lookup"><span data-stu-id="501f2-475">String</span></span>|<span data-ttu-id="501f2-476">512</span><span class="sxs-lookup"><span data-stu-id="501f2-476">512</span></span>||<span data-ttu-id="501f2-477">Value of the choice.</span><span class="sxs-lookup"><span data-stu-id="501f2-477">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="501f2-478">permissions</span><span class="sxs-lookup"><span data-stu-id="501f2-478">permissions</span></span>

<span data-ttu-id="501f2-479">**Optional**</span><span class="sxs-lookup"><span data-stu-id="501f2-479">**Optional**</span></span>

<span data-ttu-id="501f2-480">アプリが要求するアクセス許可を指定する配列で、エンド ユーザーは拡張機能の実行 `string` 方法を知る必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-480">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="501f2-481">次のオプションは、非排他的です。</span><span class="sxs-lookup"><span data-stu-id="501f2-481">The following options are non-exclusive:</span></span>

* <span data-ttu-id="501f2-482">`identity`&emsp;ユーザー ID 情報が必要です。</span><span class="sxs-lookup"><span data-stu-id="501f2-482">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="501f2-483">`messageTeamMembers`&emsp;チーム メンバーに直接メッセージを送信するためのアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="501f2-483">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="501f2-484">アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは更新されたアプリを初めて実行するときに同意プロセスを繰り返します。</span><span class="sxs-lookup"><span data-stu-id="501f2-484">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="501f2-485">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="501f2-485">devicePermissions</span></span>

<span data-ttu-id="501f2-486">**省略可能** 文字列の配列</span><span class="sxs-lookup"><span data-stu-id="501f2-486">**Optional** Array of Strings</span></span>

<span data-ttu-id="501f2-487">アプリがアクセスを要求できるユーザーのデバイス上のネイティブ機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-487">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="501f2-488">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="501f2-488">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="501f2-489">validDomains</span><span class="sxs-lookup"><span data-stu-id="501f2-489">validDomains</span></span>

<span data-ttu-id="501f2-490">**省略** 可能です ( **必須の場合** は除く)</span><span class="sxs-lookup"><span data-stu-id="501f2-490">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="501f2-491">アプリがコンテンツの読み込みを期待する有効なドメインの一覧。</span><span class="sxs-lookup"><span data-stu-id="501f2-491">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="501f2-492">ドメインの一覧には、ワイルドカードを含め、たとえば、 を含めできます `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-492">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="501f2-493">これは、ドメインの 1 つのセグメントと完全に一致します。一致する必要がある場合は、 `a.b.example.com` を使用します `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-493">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="501f2-494">タブ構成またはコンテンツ UI で、タブ構成に使用するドメイン以外のドメインに移動する必要がある場合は、ここでそのドメインを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-494">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="501f2-495">ただし、 **サポート** する ID プロバイダーのドメインをアプリに含める必要はありません。</span><span class="sxs-lookup"><span data-stu-id="501f2-495">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="501f2-496">たとえば、Google ID を使用して認証するには、Accounts.google.com にリダイレクトする必要がありますが、accounts.google.com に含める必要はありません `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-496">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="501f2-497">直接またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しません。</span><span class="sxs-lookup"><span data-stu-id="501f2-497">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="501f2-498">たとえば、有効 `yourapp.onmicrosoft.com` ですが、 `*.onmicrosoft.com` 無効です。</span><span class="sxs-lookup"><span data-stu-id="501f2-498">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="501f2-499">オブジェクトは、型のすべての要素を持つ配列です `string` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-499">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="501f2-500">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="501f2-500">webApplicationInfo</span></span>

<span data-ttu-id="501f2-501">**Optional**</span><span class="sxs-lookup"><span data-stu-id="501f2-501">**Optional**</span></span>

<span data-ttu-id="501f2-502">ユーザーが AAD アプリにシームレスにサインインGraphに役立つ AAD アプリ ID とユーザー情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-502">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="501f2-503">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-503">Name</span></span>| <span data-ttu-id="501f2-504">型</span><span class="sxs-lookup"><span data-stu-id="501f2-504">Type</span></span>| <span data-ttu-id="501f2-505">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-505">Maximum size</span></span> | <span data-ttu-id="501f2-506">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-506">Required</span></span> | <span data-ttu-id="501f2-507">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-507">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="501f2-508">String</span><span class="sxs-lookup"><span data-stu-id="501f2-508">String</span></span>|<span data-ttu-id="501f2-509">36 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-509">36 characters</span></span>|<span data-ttu-id="501f2-510">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-510">✔</span></span>|<span data-ttu-id="501f2-511">アプリの AAD アプリケーション ID。</span><span class="sxs-lookup"><span data-stu-id="501f2-511">AAD application id of the app.</span></span> <span data-ttu-id="501f2-512">この ID は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-512">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="501f2-513">String</span><span class="sxs-lookup"><span data-stu-id="501f2-513">String</span></span>|<span data-ttu-id="501f2-514">2048 文字</span><span class="sxs-lookup"><span data-stu-id="501f2-514">2048 characters</span></span>|<span data-ttu-id="501f2-515">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-515">✔</span></span>|<span data-ttu-id="501f2-516">SSO の認証トークンを取得するためのアプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="501f2-516">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="501f2-517">配列</span><span class="sxs-lookup"><span data-stu-id="501f2-517">Array</span></span>|<span data-ttu-id="501f2-518">最大 100 アイテム</span><span class="sxs-lookup"><span data-stu-id="501f2-518">Maximum 100 items</span></span>|<span data-ttu-id="501f2-519">✔</span><span class="sxs-lookup"><span data-stu-id="501f2-519">✔</span></span>|<span data-ttu-id="501f2-520">アプリケーションのリソースのアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="501f2-520">Resource permissions for application.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="501f2-521">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="501f2-521">configurableProperties</span></span>

<span data-ttu-id="501f2-522">**オプション** - 配列</span><span class="sxs-lookup"><span data-stu-id="501f2-522">**Optional** - array</span></span>

<span data-ttu-id="501f2-523">この `configurableProperties` ブロックは、管理者がカスタマイズできるアプリTeams定義します。</span><span class="sxs-lookup"><span data-stu-id="501f2-523">The `configurableProperties` block defines the app properties that Teams admins can customize.</span></span> <span data-ttu-id="501f2-524">詳細については、「アプリのカスタマイズを [有効にする」を参照してください](~/concepts/design/enable-app-customization.md)。</span><span class="sxs-lookup"><span data-stu-id="501f2-524">For more information, see [enable app customization](~/concepts/design/enable-app-customization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="501f2-525">少なくとも 1 つのプロパティを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="501f2-525">A minimum of one property must be defined.</span></span> <span data-ttu-id="501f2-526">このブロックでは、最大 9 つのプロパティを定義できます。</span><span class="sxs-lookup"><span data-stu-id="501f2-526">You can define a maximum of nine properties in this block.</span></span>

<span data-ttu-id="501f2-527">次のプロパティを定義できます。</span><span class="sxs-lookup"><span data-stu-id="501f2-527">You can define any of the following properties:</span></span>

* <span data-ttu-id="501f2-528">`name`: アプリの表示名。</span><span class="sxs-lookup"><span data-stu-id="501f2-528">`name`: The app's display name.</span></span>
* <span data-ttu-id="501f2-529">`shortDescription`: アプリの簡単な説明です。</span><span class="sxs-lookup"><span data-stu-id="501f2-529">`shortDescription`: The app's short description.</span></span>
* <span data-ttu-id="501f2-530">`longDescription`: アプリの詳細な説明。</span><span class="sxs-lookup"><span data-stu-id="501f2-530">`longDescription`: The app's detailed description.</span></span>
* <span data-ttu-id="501f2-531">`smallImageUrl`: アプリのアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="501f2-531">`smallImageUrl`: The app's outline icon.</span></span>
* <span data-ttu-id="501f2-532">`largeImageUrl`: アプリの色アイコン。</span><span class="sxs-lookup"><span data-stu-id="501f2-532">`largeImageUrl`: The app's color icon.</span></span>
* <span data-ttu-id="501f2-533">`accentColor`: アウトライン アイコンと組み合わせて、背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="501f2-533">`accentColor`: The color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="501f2-534">`developerUrl`: 開発者の Web サイトの HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="501f2-534">`developerUrl`: The HTTPS URL of the developer's website.</span></span>
* <span data-ttu-id="501f2-535">`privacyUrl`: 開発者のプライバシー ポリシーの HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="501f2-535">`privacyUrl`: The HTTPS URL of the developer's privacy policy.</span></span>
* <span data-ttu-id="501f2-536">`termsOfUseUrl`: 開発者の使用条件の HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="501f2-536">`termsOfUseUrl`: The HTTPS URL of the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="501f2-537">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="501f2-537">defaultInstallScope</span></span>

<span data-ttu-id="501f2-538">**省略** 可能 - 文字列</span><span class="sxs-lookup"><span data-stu-id="501f2-538">**Optional** - string</span></span>

<span data-ttu-id="501f2-539">既定では、このアプリに対して定義されているインストール スコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-539">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="501f2-540">定義されたスコープは、ユーザーがアプリを追加しようとするときにボタンに表示されるオプションになります。</span><span class="sxs-lookup"><span data-stu-id="501f2-540">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="501f2-541">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="501f2-541">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="501f2-542">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="501f2-542">defaultGroupCapability</span></span>

<span data-ttu-id="501f2-543">**省略可能** - オブジェクト</span><span class="sxs-lookup"><span data-stu-id="501f2-543">**Optional** - object</span></span>

<span data-ttu-id="501f2-544">グループ インストール スコープを選択すると、ユーザーがアプリをインストールするときに既定の機能が定義されます。</span><span class="sxs-lookup"><span data-stu-id="501f2-544">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="501f2-545">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="501f2-545">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="501f2-546">名前</span><span class="sxs-lookup"><span data-stu-id="501f2-546">Name</span></span>| <span data-ttu-id="501f2-547">型</span><span class="sxs-lookup"><span data-stu-id="501f2-547">Type</span></span>| <span data-ttu-id="501f2-548">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="501f2-548">Maximum size</span></span> | <span data-ttu-id="501f2-549">必須</span><span class="sxs-lookup"><span data-stu-id="501f2-549">Required</span></span> | <span data-ttu-id="501f2-550">説明</span><span class="sxs-lookup"><span data-stu-id="501f2-550">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="501f2-551">string</span><span class="sxs-lookup"><span data-stu-id="501f2-551">string</span></span>|||<span data-ttu-id="501f2-552">選択したインストール スコープが次の場合 `team` 、このフィールドは使用可能な既定の機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-552">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="501f2-553">オプション: `tab` `bot` 、、または `connector` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-553">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="501f2-554">string</span><span class="sxs-lookup"><span data-stu-id="501f2-554">string</span></span>|||<span data-ttu-id="501f2-555">選択したインストール スコープが次の場合 `groupchat` 、このフィールドは使用可能な既定の機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-555">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="501f2-556">オプション: `tab` `bot` 、、または `connector` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-556">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="501f2-557">string</span><span class="sxs-lookup"><span data-stu-id="501f2-557">string</span></span>|||<span data-ttu-id="501f2-558">選択したインストール スコープが次の場合 `meetings` 、このフィールドは使用可能な既定の機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="501f2-558">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="501f2-559">オプション: `tab` `bot` 、、または `connector` 。</span><span class="sxs-lookup"><span data-stu-id="501f2-559">Options: `tab`, `bot`, or `connector`.</span></span>|
