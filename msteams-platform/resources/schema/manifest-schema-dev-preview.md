---
title: Developer Preview マニフェスト スキーマ参照
description: マニフェストでサポートされているスキーマについて説明Microsoft Teams
ms.topic: reference
keywords: teams マニフェスト スキーマ Developer Preview
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: 333ed556ba8ba59c66f66d7eaa41dd0ea66dca0a
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629866"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="ea10f-104">開発者プレビュー マニフェスト スキーマ (Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ea10f-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="ea10f-105">プログラム [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) 参加方法の詳細については、「Developer Preview」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea10f-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="ea10f-106">開発者プレビューを使用していない場合は、このバージョンのマニフェストを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="ea10f-107">マニフェスト[のパブリック バージョンについては、「リファレンス: Microsoft Teams](~/resources/schema/manifest-schema.md)マニフェスト スキーマ」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ea10f-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="ea10f-108">このMicrosoft Teamsマニフェストは、アプリが製品に統合する方法Microsoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="ea10f-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="ea10f-109">マニフェストは、 でホストされるスキーマに準拠している必要があります [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="ea10f-110">利用可能な機能の詳細については、「パブリック サイトの機能」を参照Developer Preview[を参照Microsoft Teams。](~/resources/dev-preview/developer-preview-features.md)</span><span class="sxs-lookup"><span data-stu-id="ea10f-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="ea10f-111">完全なマニフェストのサンプル</span><span class="sxs-lookup"><span data-stu-id="ea10f-111">Sample full manifest</span></span>

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

<span data-ttu-id="ea10f-112">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="ea10f-113">$schema</span><span class="sxs-lookup"><span data-stu-id="ea10f-113">$schema</span></span>

<span data-ttu-id="ea10f-114">*省略可能ですが、推奨* &ndash; 文字列</span><span class="sxs-lookup"><span data-stu-id="ea10f-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="ea10f-115">マニフェスト https:// JSON スキーマを参照する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="ea10f-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="ea10f-116">manifestVersion</span></span>

<span data-ttu-id="ea10f-117">**必須** &ndash; 文字列</span><span class="sxs-lookup"><span data-stu-id="ea10f-117">**Required** &ndash; String</span></span>

<span data-ttu-id="ea10f-118">このマニフェストが使用しているマニフェスト スキーマのバージョン。</span><span class="sxs-lookup"><span data-stu-id="ea10f-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="ea10f-119">"devPreview" である必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="ea10f-120">version</span><span class="sxs-lookup"><span data-stu-id="ea10f-120">version</span></span>

<span data-ttu-id="ea10f-121">**必須** &ndash; 文字列</span><span class="sxs-lookup"><span data-stu-id="ea10f-121">**Required** &ndash; String</span></span>

<span data-ttu-id="ea10f-122">特定のアプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="ea10f-122">The version of the specific app.</span></span> <span data-ttu-id="ea10f-123">マニフェストで何かを更新する場合は、バージョンも増分する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="ea10f-124">このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="ea10f-125">このアプリがストアに送信された場合、新しいマニフェストを再送信して再検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="ea10f-126">次に、このアプリのユーザーは、承認された後、数時間で新しい更新されたマニフェストを自動的に取得します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="ea10f-127">アプリがアクセス許可の変更を要求した場合、ユーザーはアプリのアップグレードと再同意を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ea10f-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="ea10f-128">このバージョンの文字列は [、semver](http://semver.org/) 標準 (MAJOR) に従う必要があります。MINOR。PATCH)。</span><span class="sxs-lookup"><span data-stu-id="ea10f-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="ea10f-129">id</span><span class="sxs-lookup"><span data-stu-id="ea10f-129">id</span></span>

<span data-ttu-id="ea10f-130">**必須** &ndash; Microsoft アプリ ID</span><span class="sxs-lookup"><span data-stu-id="ea10f-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="ea10f-131">このアプリの Microsoft が生成した一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="ea10f-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="ea10f-132">ボットを Microsoft Bot Framework 経由で登録している場合、またはタブの Web アプリが既に Microsoft にサインインしている場合は、既に ID を持っている必要があります。ここで入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="ea10f-133">それ以外の場合は、Microsoft アプリケーション登録ポータル[(My Applications)](https://apps.dev.microsoft.com)で新しい ID を生成し、ここに入力し、ボットを追加するときに再利用 [する必要があります](~/bots/how-to/create-a-bot-for-teams.md)。</span><span class="sxs-lookup"><span data-stu-id="ea10f-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="ea10f-134">packageName</span><span class="sxs-lookup"><span data-stu-id="ea10f-134">packageName</span></span>

<span data-ttu-id="ea10f-135">**必須** &ndash; 文字列</span><span class="sxs-lookup"><span data-stu-id="ea10f-135">**Required** &ndash; String</span></span>

<span data-ttu-id="ea10f-136">逆ドメイン表記でこのアプリの一意の識別子。たとえば、com.example.myapp などです。</span><span class="sxs-lookup"><span data-stu-id="ea10f-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="ea10f-137">developer</span><span class="sxs-lookup"><span data-stu-id="ea10f-137">developer</span></span>

<span data-ttu-id="ea10f-138">**必須**</span><span class="sxs-lookup"><span data-stu-id="ea10f-138">**Required**</span></span>

<span data-ttu-id="ea10f-139">会社に関する情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-139">Specifies information about your company.</span></span> <span data-ttu-id="ea10f-140">AppSource に送信されたアプリ (以前Officeストア) の場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="ea10f-141">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-141">Name</span></span>| <span data-ttu-id="ea10f-142">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-142">Maximum size</span></span> | <span data-ttu-id="ea10f-143">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-143">Required</span></span> | <span data-ttu-id="ea10f-144">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="ea10f-145">32 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-145">32 characters</span></span>|<span data-ttu-id="ea10f-146">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-146">✔</span></span>|<span data-ttu-id="ea10f-147">開発者の表示名。</span><span class="sxs-lookup"><span data-stu-id="ea10f-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="ea10f-148">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-148">2048 characters</span></span>|<span data-ttu-id="ea10f-149">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-149">✔</span></span>|<span data-ttu-id="ea10f-150">開発者 https:// WEB サイトの URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="ea10f-151">このリンクは、ユーザーを会社または製品固有のランディング ページに移動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="ea10f-152">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-152">2048 characters</span></span>|<span data-ttu-id="ea10f-153">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-153">✔</span></span>|<span data-ttu-id="ea10f-154">開発者 https:// のプライバシー ポリシーの URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="ea10f-155">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-155">2048 characters</span></span>|<span data-ttu-id="ea10f-156">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-156">✔</span></span>|<span data-ttu-id="ea10f-157">開発者 https:// の使用条件の URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="ea10f-158">10 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-158">10 characters</span></span>|<span data-ttu-id="ea10f-159">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-159">✔</span></span>|<span data-ttu-id="ea10f-160">**省略可能** アプリを構築するパートナー組織を識別する Microsoft パートナー ネットワーク ID。</span><span class="sxs-lookup"><span data-stu-id="ea10f-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="ea10f-161">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="ea10f-161">localizationInfo</span></span>

<span data-ttu-id="ea10f-162">**Optional**</span><span class="sxs-lookup"><span data-stu-id="ea10f-162">**Optional**</span></span>

<span data-ttu-id="ea10f-163">既定の言語の指定と、追加の言語ファイルへのポインターを許可します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="ea10f-164">「ローカライズ」 [を参照してください](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="ea10f-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="ea10f-165">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-165">Name</span></span>| <span data-ttu-id="ea10f-166">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-166">Maximum size</span></span> | <span data-ttu-id="ea10f-167">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-167">Required</span></span> | <span data-ttu-id="ea10f-168">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="ea10f-169">4 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-169">4 characters</span></span>|<span data-ttu-id="ea10f-170">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-170">✔</span></span>|<span data-ttu-id="ea10f-171">このトップ レベルのマニフェスト ファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="ea10f-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="ea10f-172">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="ea10f-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="ea10f-173">追加の言語変換を指定するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="ea10f-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="ea10f-174">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-174">Name</span></span>| <span data-ttu-id="ea10f-175">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-175">Maximum size</span></span> | <span data-ttu-id="ea10f-176">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-176">Required</span></span> | <span data-ttu-id="ea10f-177">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="ea10f-178">4 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-178">4 characters</span></span>|<span data-ttu-id="ea10f-179">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-179">✔</span></span>|<span data-ttu-id="ea10f-180">指定されたファイル内の文字列の言語タグ。</span><span class="sxs-lookup"><span data-stu-id="ea10f-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="ea10f-181">4 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-181">4 characters</span></span>|<span data-ttu-id="ea10f-182">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-182">✔</span></span>|<span data-ttu-id="ea10f-183">翻訳された文字列を含む .json ファイルへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="ea10f-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="ea10f-184">name</span><span class="sxs-lookup"><span data-stu-id="ea10f-184">name</span></span>

<span data-ttu-id="ea10f-185">**必須**</span><span class="sxs-lookup"><span data-stu-id="ea10f-185">**Required**</span></span>

<span data-ttu-id="ea10f-186">アプリ エクスペリエンスのユーザーに表示されるアプリ エクスペリエンスのTeamsします。</span><span class="sxs-lookup"><span data-stu-id="ea10f-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="ea10f-187">AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="ea10f-188">の値 `short` と `full` 同じ値にしない必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="ea10f-189">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-189">Name</span></span>| <span data-ttu-id="ea10f-190">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-190">Maximum size</span></span> | <span data-ttu-id="ea10f-191">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-191">Required</span></span> | <span data-ttu-id="ea10f-192">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="ea10f-193">30 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-193">30 characters</span></span>|<span data-ttu-id="ea10f-194">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-194">✔</span></span>|<span data-ttu-id="ea10f-195">アプリの短い表示名。</span><span class="sxs-lookup"><span data-stu-id="ea10f-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="ea10f-196">100 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-196">100 characters</span></span>||<span data-ttu-id="ea10f-197">完全なアプリ名が 30 文字を超える場合に使用されるアプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="ea10f-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="ea10f-198">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-198">description</span></span>

<span data-ttu-id="ea10f-199">**必須**</span><span class="sxs-lookup"><span data-stu-id="ea10f-199">**Required**</span></span>

<span data-ttu-id="ea10f-200">アプリをユーザーに説明します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-200">Describes your app to users.</span></span> <span data-ttu-id="ea10f-201">AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="ea10f-202">説明がエクスペリエンスを正確に説明し、潜在的な顧客がエクスペリエンスの内容を理解するのに役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="ea10f-203">また、外部アカウントの使用が必要な場合は、完全な説明に注意してください。</span><span class="sxs-lookup"><span data-stu-id="ea10f-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="ea10f-204">の値 `short` と `full` 同じ値にしない必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="ea10f-205">短い説明は、長い説明の中で繰り返し実行し、他のアプリ名を含めずに行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="ea10f-206">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-206">Name</span></span>| <span data-ttu-id="ea10f-207">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-207">Maximum size</span></span> | <span data-ttu-id="ea10f-208">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-208">Required</span></span> | <span data-ttu-id="ea10f-209">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="ea10f-210">80 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-210">80 characters</span></span>|<span data-ttu-id="ea10f-211">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-211">✔</span></span>|<span data-ttu-id="ea10f-212">スペースが制限されている場合に使用されるアプリ エクスペリエンスの簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="ea10f-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="ea10f-213">4000 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-213">4000 characters</span></span>|<span data-ttu-id="ea10f-214">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-214">✔</span></span>|<span data-ttu-id="ea10f-215">アプリの完全な説明。</span><span class="sxs-lookup"><span data-stu-id="ea10f-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="ea10f-216">アイコン</span><span class="sxs-lookup"><span data-stu-id="ea10f-216">icons</span></span>

<span data-ttu-id="ea10f-217">**必須**</span><span class="sxs-lookup"><span data-stu-id="ea10f-217">**Required**</span></span>

<span data-ttu-id="ea10f-218">アプリ内で使用Teamsアイコン。</span><span class="sxs-lookup"><span data-stu-id="ea10f-218">Icons used within the Teams app.</span></span> <span data-ttu-id="ea10f-219">アイコン ファイルは、アップロード パッケージの一部として含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="ea10f-220">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-220">Name</span></span>| <span data-ttu-id="ea10f-221">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-221">Maximum size</span></span> | <span data-ttu-id="ea10f-222">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-222">Required</span></span> | <span data-ttu-id="ea10f-223">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="ea10f-224">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-224">2048 characters</span></span>|<span data-ttu-id="ea10f-225">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-225">✔</span></span>|<span data-ttu-id="ea10f-226">透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="ea10f-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="ea10f-227">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-227">2048 characters</span></span>|<span data-ttu-id="ea10f-228">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-228">✔</span></span>|<span data-ttu-id="ea10f-229">フル カラーの 192x192 PNG アイコンへの相対ファイル パス。</span><span class="sxs-lookup"><span data-stu-id="ea10f-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="ea10f-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="ea10f-230">accentColor</span></span>

<span data-ttu-id="ea10f-231">**必須** &ndash; 文字列</span><span class="sxs-lookup"><span data-stu-id="ea10f-231">**Required** &ndash; String</span></span>

<span data-ttu-id="ea10f-232">アウトライン アイコンと組み合わせて、背景として使用する色。</span><span class="sxs-lookup"><span data-stu-id="ea10f-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="ea10f-233">値は、'#' で始まる有効な HTML カラー コードである必要があります `#4464ee` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="ea10f-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="ea10f-234">configurableTabs</span></span>

<span data-ttu-id="ea10f-235">**Optional**</span><span class="sxs-lookup"><span data-stu-id="ea10f-235">**Optional**</span></span>

<span data-ttu-id="ea10f-236">アプリ エクスペリエンスに、追加する前に追加の構成が必要なチーム チャネル タブ エクスペリエンスがある場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="ea10f-237">構成可能なタブは teams スコープでのみサポートされ、現在はアプリごとに 1 つのタブしかサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="ea10f-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="ea10f-238">オブジェクトは、型のすべての要素を持つ配列です `object` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="ea10f-239">このブロックは、構成可能なチャネル タブ ソリューションを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="ea10f-240">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-240">Name</span></span>| <span data-ttu-id="ea10f-241">型</span><span class="sxs-lookup"><span data-stu-id="ea10f-241">Type</span></span>| <span data-ttu-id="ea10f-242">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-242">Maximum size</span></span> | <span data-ttu-id="ea10f-243">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-243">Required</span></span> | <span data-ttu-id="ea10f-244">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="ea10f-245">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-245">String</span></span>|<span data-ttu-id="ea10f-246">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-246">2048 characters</span></span>|<span data-ttu-id="ea10f-247">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-247">✔</span></span>|<span data-ttu-id="ea10f-248">タブ https:// する際に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="ea10f-249">ブール型</span><span class="sxs-lookup"><span data-stu-id="ea10f-249">Boolean</span></span>|||<span data-ttu-id="ea10f-250">作成後に、タブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="ea10f-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="ea10f-251">既定値: `true`</span><span class="sxs-lookup"><span data-stu-id="ea10f-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="ea10f-252">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-252">Array of enum</span></span>|<span data-ttu-id="ea10f-253">1</span><span class="sxs-lookup"><span data-stu-id="ea10f-253">1</span></span>|<span data-ttu-id="ea10f-254">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-254">✔</span></span>|<span data-ttu-id="ea10f-255">現在、構成可能なタブは、スコープ `team` とスコープ `groupchat` のみをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ea10f-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="ea10f-256">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-256">String</span></span>|<span data-ttu-id="ea10f-257">2048</span><span class="sxs-lookup"><span data-stu-id="ea10f-257">2048</span></span>||<span data-ttu-id="ea10f-258">タブ プレビュー イメージへの相対ファイル パスを使用して、SharePoint。</span><span class="sxs-lookup"><span data-stu-id="ea10f-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="ea10f-259">サイズは 1024x768 です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="ea10f-260">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-260">Array of enum</span></span>|<span data-ttu-id="ea10f-261">1</span><span class="sxs-lookup"><span data-stu-id="ea10f-261">1</span></span>||<span data-ttu-id="ea10f-262">タブをタブで使用する方法を定義SharePoint。</span><span class="sxs-lookup"><span data-stu-id="ea10f-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="ea10f-263">オプションは `sharePointFullPage` 次のとおりです。 `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="ea10f-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="ea10f-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="ea10f-264">staticTabs</span></span>

<span data-ttu-id="ea10f-265">**Optional**</span><span class="sxs-lookup"><span data-stu-id="ea10f-265">**Optional**</span></span>

<span data-ttu-id="ea10f-266">ユーザーが手動で追加せずに、既定で "ピン留め" できるタブのセットを定義します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="ea10f-267">スコープ内で宣言された静的タブ `personal` は、常にアプリの個人用エクスペリエンスにピン留めされます。</span><span class="sxs-lookup"><span data-stu-id="ea10f-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="ea10f-268">スコープで宣言されている静的タブ `team` は現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="ea10f-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="ea10f-269">オブジェクトは、型のすべての要素を持つ配列 (最大 16 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="ea10f-270">このブロックは、静的タブ ソリューションを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="ea10f-271">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-271">Name</span></span>| <span data-ttu-id="ea10f-272">型</span><span class="sxs-lookup"><span data-stu-id="ea10f-272">Type</span></span>| <span data-ttu-id="ea10f-273">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-273">Maximum size</span></span> | <span data-ttu-id="ea10f-274">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-274">Required</span></span> | <span data-ttu-id="ea10f-275">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="ea10f-276">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-276">String</span></span>|<span data-ttu-id="ea10f-277">64 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-277">64 characters</span></span>|<span data-ttu-id="ea10f-278">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-278">✔</span></span>|<span data-ttu-id="ea10f-279">タブが表示されるエンティティの一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="ea10f-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="ea10f-280">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-280">String</span></span>|<span data-ttu-id="ea10f-281">128 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-281">128 characters</span></span>|<span data-ttu-id="ea10f-282">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-282">✔</span></span>|<span data-ttu-id="ea10f-283">チャネル インターフェイスのタブの表示名。</span><span class="sxs-lookup"><span data-stu-id="ea10f-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="ea10f-284">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-284">String</span></span>|<span data-ttu-id="ea10f-285">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-285">2048 characters</span></span>|<span data-ttu-id="ea10f-286">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-286">✔</span></span>|<span data-ttu-id="ea10f-287">この https:// キャンバスに表示するエンティティ UI を示すTeamsします。</span><span class="sxs-lookup"><span data-stu-id="ea10f-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="ea10f-288">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-288">String</span></span>|<span data-ttu-id="ea10f-289">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-289">2048 characters</span></span>||<span data-ttu-id="ea10f-290">ユーザー https:// ブラウザーで表示することを選択した場合に示す URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="ea10f-291">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-291">Array of enum</span></span>|<span data-ttu-id="ea10f-292">1</span><span class="sxs-lookup"><span data-stu-id="ea10f-292">1</span></span>|<span data-ttu-id="ea10f-293">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-293">✔</span></span>|<span data-ttu-id="ea10f-294">現在、静的タブはスコープのみをサポートしています。つまり、個人用エクスペリエンスの一部としてのみ `personal` プロビジョニングできます。</span><span class="sxs-lookup"><span data-stu-id="ea10f-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="ea10f-295">bots</span><span class="sxs-lookup"><span data-stu-id="ea10f-295">bots</span></span>

<span data-ttu-id="ea10f-296">**Optional**</span><span class="sxs-lookup"><span data-stu-id="ea10f-296">**Optional**</span></span>

<span data-ttu-id="ea10f-297">既定のコマンド プロパティなどのオプションの情報と共に、ボット ソリューションを定義します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="ea10f-298">オブジェクトは、型のすべての要素を持つ配列 (現在、1 つのボットにつき 1 つのボットしか許可されていない &mdash; 最大 1 つの要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="ea10f-299">このブロックは、ボット エクスペリエンスを提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="ea10f-300">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-300">Name</span></span>| <span data-ttu-id="ea10f-301">型</span><span class="sxs-lookup"><span data-stu-id="ea10f-301">Type</span></span>| <span data-ttu-id="ea10f-302">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-302">Maximum size</span></span> | <span data-ttu-id="ea10f-303">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-303">Required</span></span> | <span data-ttu-id="ea10f-304">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="ea10f-305">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-305">String</span></span>|<span data-ttu-id="ea10f-306">64 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-306">64 characters</span></span>|<span data-ttu-id="ea10f-307">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-307">✔</span></span>|<span data-ttu-id="ea10f-308">Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="ea10f-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="ea10f-309">これは、アプリ全体の ID と同じ [可能性があります](#id)。</span><span class="sxs-lookup"><span data-stu-id="ea10f-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="ea10f-310">Boolean</span><span class="sxs-lookup"><span data-stu-id="ea10f-310">Boolean</span></span>|||<span data-ttu-id="ea10f-311">ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。</span><span class="sxs-lookup"><span data-stu-id="ea10f-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="ea10f-312">既定値: `false`</span><span class="sxs-lookup"><span data-stu-id="ea10f-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="ea10f-313">Boolean</span><span class="sxs-lookup"><span data-stu-id="ea10f-313">Boolean</span></span>|||<span data-ttu-id="ea10f-314">ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="ea10f-315">既定値: `false`</span><span class="sxs-lookup"><span data-stu-id="ea10f-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="ea10f-316">Boolean</span><span class="sxs-lookup"><span data-stu-id="ea10f-316">Boolean</span></span>|||<span data-ttu-id="ea10f-317">パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="ea10f-318">既定値: `false`</span><span class="sxs-lookup"><span data-stu-id="ea10f-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="ea10f-319">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-319">Array of enum</span></span>|<span data-ttu-id="ea10f-320">3</span><span class="sxs-lookup"><span data-stu-id="ea10f-320">3</span></span>|<span data-ttu-id="ea10f-321">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-321">✔</span></span>|<span data-ttu-id="ea10f-322">ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="ea10f-323">これらのオプションは非排他的です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="ea10f-324">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="ea10f-324">bots.commandLists</span></span>

<span data-ttu-id="ea10f-325">ボットがユーザーに推奨できるコマンドのオプションの一覧。</span><span class="sxs-lookup"><span data-stu-id="ea10f-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="ea10f-326">オブジェクトは、型のすべての要素を持つ配列 (最大 2 つの要素) です。ボットがサポートするスコープごとに個別のコマンド リストを `object` 定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="ea10f-327">詳細については、「Bot メニュー [」を参照してください](~/bots/how-to/create-a-bot-commands-menu.md)。</span><span class="sxs-lookup"><span data-stu-id="ea10f-327">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="ea10f-328">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-328">Name</span></span>| <span data-ttu-id="ea10f-329">型</span><span class="sxs-lookup"><span data-stu-id="ea10f-329">Type</span></span>| <span data-ttu-id="ea10f-330">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-330">Maximum size</span></span> | <span data-ttu-id="ea10f-331">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-331">Required</span></span> | <span data-ttu-id="ea10f-332">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="ea10f-333">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-333">array of enum</span></span>|<span data-ttu-id="ea10f-334">3</span><span class="sxs-lookup"><span data-stu-id="ea10f-334">3</span></span>|<span data-ttu-id="ea10f-335">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-335">✔</span></span>|<span data-ttu-id="ea10f-336">コマンド リストが有効なスコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="ea10f-337">`team`、`personal`、`groupchat` の中から選択できます。</span><span class="sxs-lookup"><span data-stu-id="ea10f-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="ea10f-338">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-338">array of objects</span></span>|<span data-ttu-id="ea10f-339">10</span><span class="sxs-lookup"><span data-stu-id="ea10f-339">10</span></span>|<span data-ttu-id="ea10f-340">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-340">✔</span></span>|<span data-ttu-id="ea10f-341">ボットがサポートするコマンドの配列:</span><span class="sxs-lookup"><span data-stu-id="ea10f-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="ea10f-342">`title`: bot コマンド名 (文字列、32)。</span><span class="sxs-lookup"><span data-stu-id="ea10f-342">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="ea10f-343">`description`: コマンド構文とその引数の簡単な説明または例 (文字列、128)。</span><span class="sxs-lookup"><span data-stu-id="ea10f-343">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="ea10f-344">コネクタ</span><span class="sxs-lookup"><span data-stu-id="ea10f-344">connectors</span></span>

<span data-ttu-id="ea10f-345">**Optional**</span><span class="sxs-lookup"><span data-stu-id="ea10f-345">**Optional**</span></span>

<span data-ttu-id="ea10f-346">ブロック `connectors` は、アプリOffice 365コネクタを定義します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="ea10f-347">オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="ea10f-348">このブロックは、Connector を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="ea10f-349">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-349">Name</span></span>| <span data-ttu-id="ea10f-350">型</span><span class="sxs-lookup"><span data-stu-id="ea10f-350">Type</span></span>| <span data-ttu-id="ea10f-351">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-351">Maximum size</span></span> | <span data-ttu-id="ea10f-352">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-352">Required</span></span> | <span data-ttu-id="ea10f-353">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="ea10f-354">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-354">String</span></span>|<span data-ttu-id="ea10f-355">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-355">2048 characters</span></span>|<span data-ttu-id="ea10f-356">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-356">✔</span></span>|<span data-ttu-id="ea10f-357">コネクタ https:// する際に使用する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="ea10f-358">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-358">String</span></span>|<span data-ttu-id="ea10f-359">64 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-359">64 characters</span></span>|<span data-ttu-id="ea10f-360">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-360">✔</span></span>|<span data-ttu-id="ea10f-361">コネクタ開発者ダッシュボードの ID に一致するコネクタの一 [意の識別子](https://aka.ms/connectorsdashboard)です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="ea10f-362">列挙型の配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-362">Array of enum</span></span>|<span data-ttu-id="ea10f-363">1</span><span class="sxs-lookup"><span data-stu-id="ea10f-363">1</span></span>|<span data-ttu-id="ea10f-364">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-364">✔</span></span>|<span data-ttu-id="ea10f-365">Connector がチャネルのコンテキストでエクスペリエンスを提供するかどうか、または個々のユーザー () にスコープを設定したエクスペリエンスを提供するかどうかを `team` 指定します `personal` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="ea10f-366">現在、スコープ `team` だけがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="ea10f-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="ea10f-367">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="ea10f-367">composeExtensions</span></span>

<span data-ttu-id="ea10f-368">**Optional**</span><span class="sxs-lookup"><span data-stu-id="ea10f-368">**Optional**</span></span>

<span data-ttu-id="ea10f-369">アプリのメッセージング拡張機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="ea10f-370">機能の名前は、2017 年 11 月に "作成拡張機能" から "メッセージング拡張機能" に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は変わりません。</span><span class="sxs-lookup"><span data-stu-id="ea10f-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="ea10f-371">オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) です `object` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="ea10f-372">このブロックは、メッセージング拡張機能を提供するソリューションにのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="ea10f-373">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-373">Name</span></span>| <span data-ttu-id="ea10f-374">種類</span><span class="sxs-lookup"><span data-stu-id="ea10f-374">Type</span></span> | <span data-ttu-id="ea10f-375">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-375">Maximum Size</span></span> | <span data-ttu-id="ea10f-376">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-376">Required</span></span> | <span data-ttu-id="ea10f-377">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="ea10f-378">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-378">String</span></span>|<span data-ttu-id="ea10f-379">64</span><span class="sxs-lookup"><span data-stu-id="ea10f-379">64</span></span>|<span data-ttu-id="ea10f-380">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-380">✔</span></span>|<span data-ttu-id="ea10f-381">ボット フレームワークに登録されているメッセージング拡張機能をバックするボットの一意の Microsoft アプリ ID。</span><span class="sxs-lookup"><span data-stu-id="ea10f-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="ea10f-382">これは、アプリ全体の ID と同じ [可能性があります](#id)。</span><span class="sxs-lookup"><span data-stu-id="ea10f-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="ea10f-383">ブール型</span><span class="sxs-lookup"><span data-stu-id="ea10f-383">Boolean</span></span>|||<span data-ttu-id="ea10f-384">メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="ea10f-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="ea10f-385">既定値は `false` です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="ea10f-386">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-386">Array of object</span></span>|<span data-ttu-id="ea10f-387">10</span><span class="sxs-lookup"><span data-stu-id="ea10f-387">10</span></span>|<span data-ttu-id="ea10f-388">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-388">✔</span></span>|<span data-ttu-id="ea10f-389">メッセージング拡張機能がサポートするコマンドの配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="ea10f-390">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="ea10f-390">composeExtensions.commands</span></span>

<span data-ttu-id="ea10f-391">メッセージング拡張機能は、1 つ以上のコマンドを宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="ea10f-392">各コマンドは、MICROSOFT TEAMSエントリ ポイントからの潜在的な対話として表示されます。</span><span class="sxs-lookup"><span data-stu-id="ea10f-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="ea10f-393">最大 10 のコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="ea10f-394">各コマンド 項目は、次の構造を持つオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="ea10f-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="ea10f-395">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-395">Name</span></span>| <span data-ttu-id="ea10f-396">型</span><span class="sxs-lookup"><span data-stu-id="ea10f-396">Type</span></span>| <span data-ttu-id="ea10f-397">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-397">Maximum size</span></span> | <span data-ttu-id="ea10f-398">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-398">Required</span></span> | <span data-ttu-id="ea10f-399">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="ea10f-400">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-400">String</span></span>|<span data-ttu-id="ea10f-401">64 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-401">64 characters</span></span>|<span data-ttu-id="ea10f-402">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-402">✔</span></span>|<span data-ttu-id="ea10f-403">コマンドの ID。</span><span class="sxs-lookup"><span data-stu-id="ea10f-403">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="ea10f-404">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-404">String</span></span>|<span data-ttu-id="ea10f-405">64 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-405">64 characters</span></span>||<span data-ttu-id="ea10f-406">コマンドの種類。</span><span class="sxs-lookup"><span data-stu-id="ea10f-406">Type of the command.</span></span> <span data-ttu-id="ea10f-407">または `query` の 1 `action` つ。</span><span class="sxs-lookup"><span data-stu-id="ea10f-407">One of `query` or `action`.</span></span> <span data-ttu-id="ea10f-408">既定値: `query`</span><span class="sxs-lookup"><span data-stu-id="ea10f-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="ea10f-409">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-409">String</span></span>|<span data-ttu-id="ea10f-410">32 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-410">32 characters</span></span>|<span data-ttu-id="ea10f-411">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-411">✔</span></span>|<span data-ttu-id="ea10f-412">ユーザーフレンドリーなコマンド名。</span><span class="sxs-lookup"><span data-stu-id="ea10f-412">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="ea10f-413">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-413">String</span></span>|<span data-ttu-id="ea10f-414">128 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-414">128 characters</span></span>||<span data-ttu-id="ea10f-415">このコマンドの目的を示すためにユーザーに表示される説明。</span><span class="sxs-lookup"><span data-stu-id="ea10f-415">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="ea10f-416">ブール型</span><span class="sxs-lookup"><span data-stu-id="ea10f-416">Boolean</span></span>|||<span data-ttu-id="ea10f-417">パラメーターを指定してコマンドを最初に実行するかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="ea10f-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="ea10f-418">既定値: `false`</span><span class="sxs-lookup"><span data-stu-id="ea10f-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="ea10f-419">文字列 (String) の配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-419">Array of Strings</span></span>|<span data-ttu-id="ea10f-420">3</span><span class="sxs-lookup"><span data-stu-id="ea10f-420">3</span></span>||<span data-ttu-id="ea10f-421">メッセージ拡張機能の呼び出し先を定義します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="ea10f-422">`compose`、 の任意の `commandBox` 組み合 `message` わせ。</span><span class="sxs-lookup"><span data-stu-id="ea10f-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="ea10f-423">既定値は `["compose", "commandBox"]` です</span><span class="sxs-lookup"><span data-stu-id="ea10f-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="ea10f-424">ブール型</span><span class="sxs-lookup"><span data-stu-id="ea10f-424">Boolean</span></span>|||<span data-ttu-id="ea10f-425">タスク モジュールを動的にフェッチする必要があるかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="ea10f-425">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="ea10f-426">オブジェクト</span><span class="sxs-lookup"><span data-stu-id="ea10f-426">Object</span></span>|||<span data-ttu-id="ea10f-427">メッセージング拡張機能コマンドを使用するときにプリロードするタスク モジュールを指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-427">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="ea10f-428">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-428">String</span></span>|<span data-ttu-id="ea10f-429">64</span><span class="sxs-lookup"><span data-stu-id="ea10f-429">64</span></span>||<span data-ttu-id="ea10f-430">最初のダイアログ タイトル。</span><span class="sxs-lookup"><span data-stu-id="ea10f-430">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="ea10f-431">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-431">String</span></span>|||<span data-ttu-id="ea10f-432">ダイアログの幅 - ピクセル単位の数値または既定のレイアウト ('large'、'medium'、または 'small' など)。</span><span class="sxs-lookup"><span data-stu-id="ea10f-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="ea10f-433">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-433">String</span></span>|||<span data-ttu-id="ea10f-434">ダイアログの高さ - ピクセル単位の数値、または 'large'、'medium'、または 'small' などの既定のレイアウト。</span><span class="sxs-lookup"><span data-stu-id="ea10f-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="ea10f-435">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-435">String</span></span>|||<span data-ttu-id="ea10f-436">初期 Webview URL。</span><span class="sxs-lookup"><span data-stu-id="ea10f-436">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="ea10f-437">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-437">Array of Objects</span></span>|<span data-ttu-id="ea10f-438">5</span><span class="sxs-lookup"><span data-stu-id="ea10f-438">5</span></span>||<span data-ttu-id="ea10f-439">特定の条件が満たされた場合にアプリを呼び出すことができるハンドラーの一覧。</span><span class="sxs-lookup"><span data-stu-id="ea10f-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="ea10f-440">ドメインもに一覧表示する必要があります `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-440">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="ea10f-441">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-441">String</span></span>|||<span data-ttu-id="ea10f-442">メッセージ ハンドラーの種類。</span><span class="sxs-lookup"><span data-stu-id="ea10f-442">The type of message handler.</span></span> <span data-ttu-id="ea10f-443">`"link"` である必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="ea10f-444">文字列 (String) の配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-444">Array of Strings</span></span>|||<span data-ttu-id="ea10f-445">リンク メッセージ ハンドラーが登録できるドメインの配列。</span><span class="sxs-lookup"><span data-stu-id="ea10f-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="ea10f-446">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-446">Array of object</span></span>|<span data-ttu-id="ea10f-447">5</span><span class="sxs-lookup"><span data-stu-id="ea10f-447">5</span></span>|<span data-ttu-id="ea10f-448">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-448">✔</span></span>|<span data-ttu-id="ea10f-449">コマンドが受け取るパラメーターの一覧。</span><span class="sxs-lookup"><span data-stu-id="ea10f-449">The list of parameters the command takes.</span></span> <span data-ttu-id="ea10f-450">最小: 1;最大: 5</span><span class="sxs-lookup"><span data-stu-id="ea10f-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="ea10f-451">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-451">String</span></span>|<span data-ttu-id="ea10f-452">64 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-452">64 characters</span></span>|<span data-ttu-id="ea10f-453">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-453">✔</span></span>|<span data-ttu-id="ea10f-454">クライアントに表示されるパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="ea10f-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="ea10f-455">これは、ユーザー要求に含まれます。</span><span class="sxs-lookup"><span data-stu-id="ea10f-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="ea10f-456">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-456">String</span></span>|<span data-ttu-id="ea10f-457">32 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-457">32 characters</span></span>|<span data-ttu-id="ea10f-458">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-458">✔</span></span>|<span data-ttu-id="ea10f-459">パラメーターのユーザーフレンドリーなタイトル。</span><span class="sxs-lookup"><span data-stu-id="ea10f-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="ea10f-460">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-460">String</span></span>|<span data-ttu-id="ea10f-461">128 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-461">128 characters</span></span>||<span data-ttu-id="ea10f-462">このパラメーターの目的を説明するユーザーフレンドリーな文字列。</span><span class="sxs-lookup"><span data-stu-id="ea10f-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="ea10f-463">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-463">String</span></span>|<span data-ttu-id="ea10f-464">128 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-464">128 characters</span></span>||<span data-ttu-id="ea10f-465">タスク モジュールに表示されるコントロールの種類を定義します `fetchTask: true` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="ea10f-466">、 `text` `textarea` 、 、 、 、 の `number` `date` `time` `toggle` 1 `choiceset` つ。</span><span class="sxs-lookup"><span data-stu-id="ea10f-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="ea10f-467">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-467">Array of Objects</span></span>|<span data-ttu-id="ea10f-468">10</span><span class="sxs-lookup"><span data-stu-id="ea10f-468">10</span></span>||<span data-ttu-id="ea10f-469">の選択肢 `choiceset` オプションです。</span><span class="sxs-lookup"><span data-stu-id="ea10f-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="ea10f-470">の場合にのみ `parameter.inputType` 使用します `choiceset` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-470">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="ea10f-471">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-471">String</span></span>|<span data-ttu-id="ea10f-472">128</span><span class="sxs-lookup"><span data-stu-id="ea10f-472">128</span></span>||<span data-ttu-id="ea10f-473">選択したタイトル。</span><span class="sxs-lookup"><span data-stu-id="ea10f-473">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="ea10f-474">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-474">String</span></span>|<span data-ttu-id="ea10f-475">512</span><span class="sxs-lookup"><span data-stu-id="ea10f-475">512</span></span>||<span data-ttu-id="ea10f-476">Value of the choice.</span><span class="sxs-lookup"><span data-stu-id="ea10f-476">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="ea10f-477">permissions</span><span class="sxs-lookup"><span data-stu-id="ea10f-477">permissions</span></span>

<span data-ttu-id="ea10f-478">**Optional**</span><span class="sxs-lookup"><span data-stu-id="ea10f-478">**Optional**</span></span>

<span data-ttu-id="ea10f-479">アプリが要求するアクセス許可を指定する配列で、エンド ユーザーは拡張機能の実行 `string` 方法を知る必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="ea10f-480">次のオプションは、非排他的です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="ea10f-481">`identity`&emsp;ユーザー ID 情報が必要です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-481">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="ea10f-482">`messageTeamMembers`&emsp;チーム メンバーに直接メッセージを送信するためのアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="ea10f-483">アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは更新されたアプリを初めて実行するときに同意プロセスを繰り返します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="ea10f-484">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="ea10f-484">devicePermissions</span></span>

<span data-ttu-id="ea10f-485">**省略可能** 文字列の配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="ea10f-486">アプリがアクセスを要求できるユーザーのデバイス上のネイティブ機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="ea10f-487">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ea10f-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="ea10f-488">validDomains</span><span class="sxs-lookup"><span data-stu-id="ea10f-488">validDomains</span></span>

<span data-ttu-id="ea10f-489">**省略** 可能です ( **必須の場合** は除く)</span><span class="sxs-lookup"><span data-stu-id="ea10f-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="ea10f-490">アプリがコンテンツの読み込みを期待する有効なドメインの一覧。</span><span class="sxs-lookup"><span data-stu-id="ea10f-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="ea10f-491">ドメインの一覧には、ワイルドカードを含め、たとえば、 を含めできます `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="ea10f-492">これは、ドメインの 1 つのセグメントと完全に一致します。一致する必要がある場合は、 `a.b.example.com` を使用します `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="ea10f-493">タブ構成またはコンテンツ UI で、タブ構成に使用するドメイン以外のドメインに移動する必要がある場合は、ここでそのドメインを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="ea10f-494">ただし、 **サポート** する ID プロバイダーのドメインをアプリに含める必要はありません。</span><span class="sxs-lookup"><span data-stu-id="ea10f-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="ea10f-495">たとえば、Google ID を使用して認証するには、Accounts.google.com にリダイレクトする必要がありますが、accounts.google.com に含める必要はありません `validDomains[]` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea10f-496">直接またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しません。</span><span class="sxs-lookup"><span data-stu-id="ea10f-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="ea10f-497">たとえば、有効 `yourapp.onmicrosoft.com` ですが、 `*.onmicrosoft.com` 無効です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="ea10f-498">オブジェクトは、型のすべての要素を持つ配列です `string` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="ea10f-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="ea10f-499">webApplicationInfo</span></span>

<span data-ttu-id="ea10f-500">**Optional**</span><span class="sxs-lookup"><span data-stu-id="ea10f-500">**Optional**</span></span>

<span data-ttu-id="ea10f-501">ユーザーが AAD アプリにシームレスにサインインGraphに役立つ AAD アプリ ID とユーザー情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="ea10f-502">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-502">Name</span></span>| <span data-ttu-id="ea10f-503">型</span><span class="sxs-lookup"><span data-stu-id="ea10f-503">Type</span></span>| <span data-ttu-id="ea10f-504">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-504">Maximum size</span></span> | <span data-ttu-id="ea10f-505">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-505">Required</span></span> | <span data-ttu-id="ea10f-506">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="ea10f-507">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-507">String</span></span>|<span data-ttu-id="ea10f-508">36 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-508">36 characters</span></span>|<span data-ttu-id="ea10f-509">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-509">✔</span></span>|<span data-ttu-id="ea10f-510">アプリの AAD アプリケーション ID。</span><span class="sxs-lookup"><span data-stu-id="ea10f-510">AAD application id of the app.</span></span> <span data-ttu-id="ea10f-511">この ID は GUID である必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="ea10f-512">String</span><span class="sxs-lookup"><span data-stu-id="ea10f-512">String</span></span>|<span data-ttu-id="ea10f-513">2048 文字</span><span class="sxs-lookup"><span data-stu-id="ea10f-513">2048 characters</span></span>|<span data-ttu-id="ea10f-514">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-514">✔</span></span>|<span data-ttu-id="ea10f-515">SSO の認証トークンを取得するためのアプリのリソース URL。</span><span class="sxs-lookup"><span data-stu-id="ea10f-515">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="ea10f-516">配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-516">Array</span></span>|<span data-ttu-id="ea10f-517">最大 100 アイテム</span><span class="sxs-lookup"><span data-stu-id="ea10f-517">Maximum 100 items</span></span>|<span data-ttu-id="ea10f-518">✔</span><span class="sxs-lookup"><span data-stu-id="ea10f-518">✔</span></span>|<span data-ttu-id="ea10f-519">アプリケーションのリソースのアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="ea10f-519">Resource permissions for application.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="ea10f-520">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="ea10f-520">configurableProperties</span></span>

<span data-ttu-id="ea10f-521">**オプション** - 配列</span><span class="sxs-lookup"><span data-stu-id="ea10f-521">**Optional** - array</span></span>

<span data-ttu-id="ea10f-522">この `configurableProperties` ブロックは、管理者がカスタマイズできるアプリTeams定義します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-522">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="ea10f-523">詳細については、「アプリのカスタマイズ[」を参照Microsoft Teams。](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="ea10f-523">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="ea10f-524">少なくとも 1 つのプロパティを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-524">A minimum of one property must be defined.</span></span> <span data-ttu-id="ea10f-525">このブロックでは、最大 9 つのプロパティを定義できます。</span><span class="sxs-lookup"><span data-stu-id="ea10f-525">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="ea10f-526">ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-526">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> 

<span data-ttu-id="ea10f-527">次のプロパティを定義できます。</span><span class="sxs-lookup"><span data-stu-id="ea10f-527">You can define any of the following properties:</span></span>
* <span data-ttu-id="ea10f-528">`name`: 管理者がアプリの表示名を変更できます。</span><span class="sxs-lookup"><span data-stu-id="ea10f-528">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="ea10f-529">`shortDescription`: 管理者がアプリの簡単な説明を変更できます。</span><span class="sxs-lookup"><span data-stu-id="ea10f-529">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="ea10f-530">`longDescription`: 管理者がアプリの詳細な説明を変更できます。</span><span class="sxs-lookup"><span data-stu-id="ea10f-530">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="ea10f-531">`smallImageUrl`: マニフェストの `outline` ブロック内 `icons` のプロパティです。</span><span class="sxs-lookup"><span data-stu-id="ea10f-531">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="ea10f-532">`largeImageUrl`: マニフェストの `color` ブロック内 `icons` のプロパティです。</span><span class="sxs-lookup"><span data-stu-id="ea10f-532">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="ea10f-533">`accentColor`: アウトライン アイコンと組み合わせて、背景として使用する色です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-533">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="ea10f-534">`websiteUrl`: 開発者の https:// の URL です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-534">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="ea10f-535">`privacyUrl`: 開発者の https:// の URL です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-535">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="ea10f-536">`termsOfUseUrl`: 開発者の https:// の URL です。</span><span class="sxs-lookup"><span data-stu-id="ea10f-536">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="ea10f-537">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="ea10f-537">defaultInstallScope</span></span>

<span data-ttu-id="ea10f-538">**省略** 可能 - 文字列</span><span class="sxs-lookup"><span data-stu-id="ea10f-538">**Optional** - string</span></span>

<span data-ttu-id="ea10f-539">既定では、このアプリに対して定義されているインストール スコープを指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-539">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="ea10f-540">定義されたスコープは、ユーザーがアプリを追加しようとするときにボタンに表示されるオプションになります。</span><span class="sxs-lookup"><span data-stu-id="ea10f-540">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="ea10f-541">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ea10f-541">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="ea10f-542">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="ea10f-542">defaultGroupCapability</span></span>

<span data-ttu-id="ea10f-543">**省略可能** - オブジェクト</span><span class="sxs-lookup"><span data-stu-id="ea10f-543">**Optional** - object</span></span>

<span data-ttu-id="ea10f-544">グループ インストール スコープを選択すると、ユーザーがアプリをインストールするときに既定の機能が定義されます。</span><span class="sxs-lookup"><span data-stu-id="ea10f-544">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="ea10f-545">オプションは、次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ea10f-545">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="ea10f-546">名前</span><span class="sxs-lookup"><span data-stu-id="ea10f-546">Name</span></span>| <span data-ttu-id="ea10f-547">型</span><span class="sxs-lookup"><span data-stu-id="ea10f-547">Type</span></span>| <span data-ttu-id="ea10f-548">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="ea10f-548">Maximum size</span></span> | <span data-ttu-id="ea10f-549">必須</span><span class="sxs-lookup"><span data-stu-id="ea10f-549">Required</span></span> | <span data-ttu-id="ea10f-550">説明</span><span class="sxs-lookup"><span data-stu-id="ea10f-550">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="ea10f-551">string</span><span class="sxs-lookup"><span data-stu-id="ea10f-551">string</span></span>|||<span data-ttu-id="ea10f-552">選択したインストール スコープが次の場合 `team` 、このフィールドは使用可能な既定の機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-552">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="ea10f-553">オプション: `tab` `bot` 、、または `connector` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-553">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="ea10f-554">文字列</span><span class="sxs-lookup"><span data-stu-id="ea10f-554">string</span></span>|||<span data-ttu-id="ea10f-555">選択したインストール スコープが次の場合 `groupchat` 、このフィールドは使用可能な既定の機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-555">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="ea10f-556">オプション: `tab` `bot` 、、または `connector` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-556">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="ea10f-557">文字列</span><span class="sxs-lookup"><span data-stu-id="ea10f-557">string</span></span>|||<span data-ttu-id="ea10f-558">選択したインストール スコープが次の場合 `meetings` 、このフィールドは使用可能な既定の機能を指定します。</span><span class="sxs-lookup"><span data-stu-id="ea10f-558">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="ea10f-559">オプション: `tab` `bot` 、、または `connector` 。</span><span class="sxs-lookup"><span data-stu-id="ea10f-559">Options: `tab`, `bot`, or `connector`.</span></span>|

