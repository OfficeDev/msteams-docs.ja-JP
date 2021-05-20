---
title: アプリのローカライズ
description: Microsoft Teams アプリをローカライズする際の考慮事項について説明します。
ms.topic: conceptual
localization_priority: Normal
keywords: チームは、ストア オフィス発行の AppSource ローカライズ言語を公開します。
ms.date: 05/15/2018
ms.openlocfilehash: a55b8af97e5306843858e5844a017dd402ab3516
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566048"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="279f1-104">Microsoft Teamsアプリのローカライズ</span><span class="sxs-lookup"><span data-stu-id="279f1-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="279f1-105">Microsoft Teams アプリをローカライズする際には、次の点を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="279f1-105">When localizing your Microsoft Teams app, you must consider the following:</span></span>

1. <span data-ttu-id="279f1-106">Teamsストアの登録情報 (該当する場合)</span><span class="sxs-lookup"><span data-stu-id="279f1-106">Your Teams store listing (if applicable).</span></span>
1. <span data-ttu-id="279f1-107">アプリ マニフェスト内のエンド ユーザー向け文字列。</span><span class="sxs-lookup"><span data-stu-id="279f1-107">The end-user facing strings in your app manifest.</span></span> <span data-ttu-id="279f1-108">たとえば、ボット コマンドです。</span><span class="sxs-lookup"><span data-stu-id="279f1-108">For example bot commands.</span></span>
1. <span data-ttu-id="279f1-109">ユーザーから送信されたローカライズされたテキストに応答します。</span><span class="sxs-lookup"><span data-stu-id="279f1-109">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="279f1-110">アプリソースの一覧をローカライズする</span><span class="sxs-lookup"><span data-stu-id="279f1-110">Localizing your AppSource listing</span></span>

<span data-ttu-id="279f1-111">ストアに発行する場合は、AppSource のリスティングのローカライズがまだサポートされていない点に注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="279f1-111">If you're publishing to the store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="279f1-112">ただし、アプリ ストアでローカライズされた一覧のサポートの準備として、リストに言語を追加できます。</span><span class="sxs-lookup"><span data-stu-id="279f1-112">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="279f1-113">現在、 [パートナー センター](/office/dev/store/submit-to-appsource-via-partner-center) で提供する既定の (英語) 言語情報のみが、アプリの [AppSource Web サイト](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) の一覧に表示されます。</span><span class="sxs-lookup"><span data-stu-id="279f1-113">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

### <a name="example-of-configuring-localization"></a><span data-ttu-id="279f1-114">ローカリゼーションの構成例</span><span class="sxs-lookup"><span data-stu-id="279f1-114">Example of configuring localization</span></span>

<span data-ttu-id="279f1-115">アプリの追加言語を構成するには、パートナー [センター](/office/dev/store/submit-to-appsource-via-partner-center)で、英語とアプリの追加言語の両方を選択します。</span><span class="sxs-lookup"><span data-stu-id="279f1-115">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="279f1-116">この例ではフランス語が使用されています。</span><span class="sxs-lookup"><span data-stu-id="279f1-116">French is used in this example:</span></span>

1. <span data-ttu-id="279f1-117">英語を追加する</span><span class="sxs-lookup"><span data-stu-id="279f1-117">Add English language</span></span>
    * <span data-ttu-id="279f1-118">アプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="279f1-118">Fill in the app name.</span></span>
    * <span data-ttu-id="279f1-119">英語でアプリの簡単な説明を記入してください。</span><span class="sxs-lookup"><span data-stu-id="279f1-119">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="279f1-120">英語でアプリの長い説明を記入してください。</span><span class="sxs-lookup"><span data-stu-id="279f1-120">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="279f1-121">長い説明では、「このアプリは"フランス語で利用可能です"という行も追加してください。</span><span class="sxs-lookup"><span data-stu-id="279f1-121">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="279f1-122">アプリの UI のイメージをアップロードします (英語)。</span><span class="sxs-lookup"><span data-stu-id="279f1-122">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="279f1-123">フランス語を追加する</span><span class="sxs-lookup"><span data-stu-id="279f1-123">Add French language</span></span>
    * <span data-ttu-id="279f1-124">アプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="279f1-124">Fill in the app name.</span></span>
    * <span data-ttu-id="279f1-125">フランス語でアプリの簡単な説明を入力します。</span><span class="sxs-lookup"><span data-stu-id="279f1-125">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="279f1-126">フランス語でアプリの長い説明を入力します。</span><span class="sxs-lookup"><span data-stu-id="279f1-126">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="279f1-127">アプリの UI のイメージをアップロードします (フランス語)。</span><span class="sxs-lookup"><span data-stu-id="279f1-127">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="279f1-128">英語でアップロードする画像は、AppSource で使用される画像になります。</span><span class="sxs-lookup"><span data-stu-id="279f1-128">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="279f1-129">アプリ マニフェストでの文字列のローカライズ</span><span class="sxs-lookup"><span data-stu-id="279f1-129">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="279f1-130">アプリを適切にローカライズするには、Microsoft Teams アプリ スキーマ v1.5+ を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="279f1-130">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="279f1-131">これを行うには、 `$schema` ファイルのmanifest.jsの属性を ' ' に設定 https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json し、'manifestVersion' プロパティを '1.7' に更新します。</span><span class="sxs-lookup"><span data-stu-id="279f1-131">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="279f1-132">変更時のmanifest.js例</span><span class="sxs-lookup"><span data-stu-id="279f1-132">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="279f1-133">その後、アプリケーションがサポートする既定の言語で 'localizationInfo' プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="279f1-133">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="279f1-134">ユーザーのクライアント設定が追加の言語と一致しない場合、既定の言語が最終的なフォールバック言語として使用されます。</span><span class="sxs-lookup"><span data-stu-id="279f1-134">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="279f1-135">変更時のmanifest.js例</span><span class="sxs-lookup"><span data-stu-id="279f1-135">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="279f1-136">マニフェスト内のすべてのユーザー向け文字列の翻訳を使用して、追加の .json ファイルを提供できます。</span><span class="sxs-lookup"><span data-stu-id="279f1-136">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="279f1-137">これらのファイルは [、ローカライズ ファイルの JSON スキーマ](../../resources/schema/localization-schema.md) に準拠する必要があり、マニフェストの 'localizationInfo' プロパティに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="279f1-137">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="279f1-138">各ファイルは、Teamsクライアントが適切な文字列を選択するために使用する言語タグに関連付けられます。</span><span class="sxs-lookup"><span data-stu-id="279f1-138">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="279f1-139">言語タグはの形式をと <language> - <region> りますが、目的の言語を <region> サポートするすべてのリージョンを対象とする部分を省略することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="279f1-139">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="279f1-140">Teamsクライアントは、既定の言語文字列 ->ユーザーの言語のみの文字列 ->ユーザーの言語 + ユーザーの地域文字列の順に文字列を適用します。</span><span class="sxs-lookup"><span data-stu-id="279f1-140">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="279f1-141">たとえば、既定の言語である 'fr' (フランス語、すべての地域)、および 'en' (英語、すべての地域) と 'en-gb' (英語、英国) の追加言語ファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="279f1-141">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="279f1-142">ユーザーの言語が 'en-gb' に設定されている場合:</span><span class="sxs-lookup"><span data-stu-id="279f1-142">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="279f1-143">Teamsクライアントは'fr'文字列を'en'文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="279f1-143">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="279f1-144">'en-gb' 文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="279f1-144">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="279f1-145">ユーザーの言語が 'en-ca' に設定されている場合:</span><span class="sxs-lookup"><span data-stu-id="279f1-145">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="279f1-146">Teamsクライアントは'fr'文字列を'en'文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="279f1-146">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="279f1-147">'en-ca' のローカライズは提供されていないので、'en' のローカリゼーションが使用されます。</span><span class="sxs-lookup"><span data-stu-id="279f1-147">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="279f1-148">ユーザーの言語が 'es-es' に設定されている場合、Teamsクライアントは 'fr' 文字列を受け取り、どの言語ファイルでも上書きしません。</span><span class="sxs-lookup"><span data-stu-id="279f1-148">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="279f1-149">したがって、マニフェストにトップレベルの言語のみの翻訳を提供し('en-us'ではなく'en')、必要な少数の文字列に対してのみリージョンレベルのオーバーライドを提供することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="279f1-149">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="279f1-150">変更時のmanifest.js例</span><span class="sxs-lookup"><span data-stu-id="279f1-150">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en",
    "additionalLanguages": [
      {
        "languageTag": "en-gb",
        "file": "en-gb.json"
      },
      {
        "languageTag": "fr",
        "file": "fr.json"
      },
      {
        "languageTag": "pl",
        "file": "pl.json"
      }
    ]
  }
  ...
}
```

### <a name="example-localization-json-file"></a><span data-ttu-id="279f1-151">ローカリゼーション .json ファイルの例</span><span class="sxs-lookup"><span data-stu-id="279f1-151">Example localization .json file</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "name.short": "Le App",
  "name.full": "App pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="279f1-152">ユーザーからのローカライズされたテキストの送信の処理</span><span class="sxs-lookup"><span data-stu-id="279f1-152">Handling localized text submissions from your users</span></span>

<span data-ttu-id="279f1-153">アプリケーションのローカライズ版を提供する場合、ユーザーが同じ言語で応答する可能性が非常に高くなります。</span><span class="sxs-lookup"><span data-stu-id="279f1-153">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="279f1-154">Teamsはユーザーの提出を既定の言語に変換しないため、アプリで処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="279f1-154">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="279f1-155">たとえば、ローカライズされた を提供する場合 `commandList` 、ボットへの応答は、既定の言語ではなく、コマンドのローカライズされたテキストになります。</span><span class="sxs-lookup"><span data-stu-id="279f1-155">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="279f1-156">アプリは適切に対応する必要があります。</span><span class="sxs-lookup"><span data-stu-id="279f1-156">Your app will need to respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="279f1-157">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="279f1-157">Code sample</span></span>

| <span data-ttu-id="279f1-158">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="279f1-158">Sample name</span></span> | <span data-ttu-id="279f1-159">説明</span><span class="sxs-lookup"><span data-stu-id="279f1-159">Description</span></span> | <span data-ttu-id="279f1-160">.NET</span><span class="sxs-lookup"><span data-stu-id="279f1-160">.NET</span></span> |
|-------------|-------------|------|
| <span data-ttu-id="279f1-161">アプリのローカライズ</span><span class="sxs-lookup"><span data-stu-id="279f1-161">App Localization</span></span> | <span data-ttu-id="279f1-162">ボットとタブを使用してアプリのローカライズをMicrosoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="279f1-162">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="279f1-163">View</span><span class="sxs-lookup"><span data-stu-id="279f1-163">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


