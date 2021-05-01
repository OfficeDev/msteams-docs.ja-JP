---
title: アプリのローカライズ
description: アプリのローカライズに関する考慮事項Microsoft Teamsします。
ms.topic: conceptual
localization_priority: Normal
keywords: teams publishs store office publishing AppSource ローカライズ言語
ms.date: 05/15/2018
ms.openlocfilehash: 9a939b1990d1b09410af344f79dd39b8b02c404b
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101710"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="9385e-104">アプリのローカライズMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="9385e-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="9385e-105">アプリをローカライズするMicrosoft Teams、次の点を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9385e-105">When localizing your Microsoft Teams app, you must consider the following:</span></span>

1. <span data-ttu-id="9385e-106">ユーザー Teamsストアの登録情報 (該当する場合)。</span><span class="sxs-lookup"><span data-stu-id="9385e-106">Your Teams store listing (if applicable).</span></span>
1. <span data-ttu-id="9385e-107">アプリ マニフェスト内のエンド ユーザー向け文字列 (ボット コマンドなど)。</span><span class="sxs-lookup"><span data-stu-id="9385e-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="9385e-108">ユーザーから送信されたローカライズされたテキストへの応答。</span><span class="sxs-lookup"><span data-stu-id="9385e-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="9385e-109">AppSource リストのローカライズ</span><span class="sxs-lookup"><span data-stu-id="9385e-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="9385e-110">ストアに発行する場合は、AppSource リストのローカライズがまだサポートされていないことに注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9385e-110">If you're publishing to the store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="9385e-111">ただし、アプリ ストアでのローカライズされたリストのサポートに備えて、リスティングに追加の言語を追加できます。</span><span class="sxs-lookup"><span data-stu-id="9385e-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="9385e-112">現在、登録情報のパートナー センターで指定した既定[](/office/dev/store/submit-to-appsource-via-partner-center)の (英語) 言語情報だけが、アプリの[AppSource Web](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1)サイトの一覧に表示されます。</span><span class="sxs-lookup"><span data-stu-id="9385e-112">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

### <a name="example-of-configuring-localization"></a><span data-ttu-id="9385e-113">ローカライズの構成例</span><span class="sxs-lookup"><span data-stu-id="9385e-113">Example of configuring localization</span></span>

<span data-ttu-id="9385e-114">アプリの追加の言語を構成するには、 [パートナー](/office/dev/store/submit-to-appsource-via-partner-center)センターで、英語とアプリの追加言語の両方を選択します。</span><span class="sxs-lookup"><span data-stu-id="9385e-114">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="9385e-115">この例ではフランス語を使用します。</span><span class="sxs-lookup"><span data-stu-id="9385e-115">French is used in this example.</span></span>

1. <span data-ttu-id="9385e-116">英語を追加する</span><span class="sxs-lookup"><span data-stu-id="9385e-116">Add English language</span></span>
    * <span data-ttu-id="9385e-117">アプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="9385e-117">Fill in the app name.</span></span>
    * <span data-ttu-id="9385e-118">アプリの簡単な説明を英語で入力します。</span><span class="sxs-lookup"><span data-stu-id="9385e-118">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="9385e-119">アプリの長い説明を英語で入力します。</span><span class="sxs-lookup"><span data-stu-id="9385e-119">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="9385e-120">長い説明では、「このアプリは"フランス語"で利用可能です」という行も追加してください。</span><span class="sxs-lookup"><span data-stu-id="9385e-120">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="9385e-121">アップロード UI のイメージを確認します (英語)。</span><span class="sxs-lookup"><span data-stu-id="9385e-121">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="9385e-122">フランス語を追加する</span><span class="sxs-lookup"><span data-stu-id="9385e-122">Add French language</span></span>
    * <span data-ttu-id="9385e-123">アプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="9385e-123">Fill in the app name.</span></span>
    * <span data-ttu-id="9385e-124">フランス語でアプリの簡単な説明を入力します。</span><span class="sxs-lookup"><span data-stu-id="9385e-124">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="9385e-125">フランス語でアプリの長い説明を入力します。</span><span class="sxs-lookup"><span data-stu-id="9385e-125">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="9385e-126">アップロード UI のイメージを確認します (フランス語)。</span><span class="sxs-lookup"><span data-stu-id="9385e-126">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="9385e-127">英語でアップロードする画像は、AppSource で使用されるイメージです。</span><span class="sxs-lookup"><span data-stu-id="9385e-127">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="9385e-128">アプリ マニフェスト内の文字列のローカライズ</span><span class="sxs-lookup"><span data-stu-id="9385e-128">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="9385e-129">アプリを適切にローカライズMicrosoft Teamsするには、アプリ スキーマ v1.5 以上を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9385e-129">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="9385e-130">これを行うには、manifest.json ファイルの属性を ' に設定し `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json 、'manifestVersion' プロパティを '1.7' に更新します。</span><span class="sxs-lookup"><span data-stu-id="9385e-130">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="9385e-131">変更時manifest.js例</span><span class="sxs-lookup"><span data-stu-id="9385e-131">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="9385e-132">次に、アプリケーションでサポートされている既定の言語で 'localizationInfo' プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="9385e-132">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="9385e-133">ユーザーのクライアント設定が追加の言語と一致しない場合は、既定の言語が最終的なフォールバック言語として使用されます。</span><span class="sxs-lookup"><span data-stu-id="9385e-133">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="9385e-134">変更時manifest.js例</span><span class="sxs-lookup"><span data-stu-id="9385e-134">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="9385e-135">マニフェスト内のすべてのユーザー向け文字列の翻訳を含む追加の .json ファイルを提供できます。</span><span class="sxs-lookup"><span data-stu-id="9385e-135">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="9385e-136">これらのファイルは、ローカライズ ファイル [JSON](../../resources/schema/localization-schema.md) スキーマに準拠している必要があります。マニフェストの 'localizationInfo' プロパティに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9385e-136">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="9385e-137">各ファイルは、クライアントが適切な文字列を選択するためにTeams言語タグに関連付けされます。</span><span class="sxs-lookup"><span data-stu-id="9385e-137">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="9385e-138">言語タグの形式を使用しますが、目的の言語をサポートしているすべての地域を対象とする部分を省略 <language> - <region> <region> することが推奨されます。</span><span class="sxs-lookup"><span data-stu-id="9385e-138">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="9385e-139">Teams クライアントは、既定の言語文字列 -> ユーザーの言語のみ -> ユーザーの言語 + ユーザーの地域文字列という順序で文字列を適用します。</span><span class="sxs-lookup"><span data-stu-id="9385e-139">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="9385e-140">たとえば、'fr' (フランス語、すべての地域) の既定の言語と、'en' (英語、すべての地域) と 'en-gb' (英語、英国) の追加言語ファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="9385e-140">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="9385e-141">ユーザーの言語が 'en-gb' に設定されている場合:</span><span class="sxs-lookup"><span data-stu-id="9385e-141">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="9385e-142">クライアントTeams'fr' 文字列を受け取り、それらを 'en' 文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="9385e-142">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="9385e-143">'en-gb' 文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="9385e-143">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="9385e-144">ユーザーの言語が 'en-ca' に設定されている場合:</span><span class="sxs-lookup"><span data-stu-id="9385e-144">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="9385e-145">クライアントTeams'fr' 文字列を受け取り、それらを 'en' 文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="9385e-145">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="9385e-146">'en-ca' ローカライズは指定されていないので、'en' ローカライズが使用されます。</span><span class="sxs-lookup"><span data-stu-id="9385e-146">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="9385e-147">ユーザーの言語が 'es-es' に設定されている場合、Teams クライアントは 'fr' 文字列を受け取り、どの言語ファイルでも上書きしません。</span><span class="sxs-lookup"><span data-stu-id="9385e-147">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="9385e-148">したがって、マニフェストに言語専用のトップ レベルの翻訳 ('en-us' ではなく'en') を提供し、それらを必要とする少数の文字列に対して地域レベルのオーバーライドのみを提供する方が強く推奨されます。</span><span class="sxs-lookup"><span data-stu-id="9385e-148">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="9385e-149">変更時manifest.js例</span><span class="sxs-lookup"><span data-stu-id="9385e-149">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="9385e-150">ローカライズ .json ファイルの例</span><span class="sxs-lookup"><span data-stu-id="9385e-150">Example localization .json file</span></span>

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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="9385e-151">ユーザーからのローカライズされたテキスト送信の処理</span><span class="sxs-lookup"><span data-stu-id="9385e-151">Handling localized text submissions from your users</span></span>

<span data-ttu-id="9385e-152">アプリケーションのローカライズされたバージョンを提供する場合、ユーザーが同じ言語で応答する可能性が非常に高い可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9385e-152">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="9385e-153">Teams提出を既定の言語に変換し戻す必要はないので、アプリで処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9385e-153">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="9385e-154">たとえば、ローカライズを指定した場合、ボットに対する応答は、既定の言語ではなく、コマンドのローカライズされたテキスト `commandList` になります。</span><span class="sxs-lookup"><span data-stu-id="9385e-154">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="9385e-155">アプリは適切に対応する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9385e-155">Your app will need to respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="9385e-156">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="9385e-156">Code sample</span></span>

| <span data-ttu-id="9385e-157">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="9385e-157">Sample name</span></span> | <span data-ttu-id="9385e-158">説明</span><span class="sxs-lookup"><span data-stu-id="9385e-158">Description</span></span> | <span data-ttu-id="9385e-159">.NET</span><span class="sxs-lookup"><span data-stu-id="9385e-159">.NET</span></span> |
|-------------|-------------|------|
| <span data-ttu-id="9385e-160">アプリのローカライズ</span><span class="sxs-lookup"><span data-stu-id="9385e-160">App Localization</span></span> | <span data-ttu-id="9385e-161">Microsoft Teamsタブを使用してアプリのローカライズを行います。</span><span class="sxs-lookup"><span data-stu-id="9385e-161">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="9385e-162">View</span><span class="sxs-lookup"><span data-stu-id="9385e-162">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


