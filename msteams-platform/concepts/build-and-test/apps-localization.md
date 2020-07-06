---
title: チームアプリのローカライズ
description: アプリのローカライズに関する問題について説明します。
keywords: teams 発行ストア office 発行アプリソースのローカライズ言語
ms.date: 05/15/2018
ms.openlocfilehash: 138b6d66808fc5ed212f1cb0eed8579faea6f764
ms.sourcegitcommit: bac0226d9048c363d96bbaf6f5395388c5f5c45a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "45039273"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="7c187-104">Microsoft Teams アプリのローカライズ</span><span class="sxs-lookup"><span data-stu-id="7c187-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="7c187-105">Microsoft Teams アプリをローカライズする場合は、考慮する必要がある3つの主要な領域があります。</span><span class="sxs-lookup"><span data-stu-id="7c187-105">When localizing your Microsoft Teams app there are three major areas you need to consider.</span></span>

1. <span data-ttu-id="7c187-106">AppSource リスト (アプリストアに公開している場合)。</span><span class="sxs-lookup"><span data-stu-id="7c187-106">Your AppSource listing (if you're publishing to the app store).</span></span>
1. <span data-ttu-id="7c187-107">アプリケーションマニフェスト内のエンドユーザーが使用している文字列 (bot コマンドなど)。</span><span class="sxs-lookup"><span data-stu-id="7c187-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="7c187-108">ユーザーから送信されるローカライズされたテキストに応答する。</span><span class="sxs-lookup"><span data-stu-id="7c187-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="7c187-109">AppSource リストのローカライズ</span><span class="sxs-lookup"><span data-stu-id="7c187-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="7c187-110">アプリストアに発行している場合は、AppSource リストのローカライズがまだサポートされていないことに注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7c187-110">If you're publishing to the app store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="7c187-111">ただし、アプリストアでローカライズされたリストをサポートするための準備として、追加の言語を一覧に追加することができます。</span><span class="sxs-lookup"><span data-stu-id="7c187-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="7c187-112">現在、リストの[パートナーセンター](/dev/store/use-partner-center-to-submit-to-appsource)で提供される既定の (英語) の言語情報のみが、アプリの[appsource web サイト](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1)の一覧に表示されます。</span><span class="sxs-lookup"><span data-stu-id="7c187-112">Currently only the default (English) language information you provide in [Partner Center](/dev/store/use-partner-center-to-submit-to-appsource) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

<span data-ttu-id="7c187-113">アプリの追加の言語を構成するには、[パートナーセンター](/dev/store/use-partner-center-to-submit-to-appsource)で、英語とアプリの追加言語を選択します。</span><span class="sxs-lookup"><span data-stu-id="7c187-113">To configure an additional language for your app, in [Partner Center](/dev/store/use-partner-center-to-submit-to-appsource), select both English and the additional language of the app.</span></span> <span data-ttu-id="7c187-114">この例では、フランス語が使用されています。</span><span class="sxs-lookup"><span data-stu-id="7c187-114">French is used in this example.</span></span>

1. <span data-ttu-id="7c187-115">英語の言語を追加する</span><span class="sxs-lookup"><span data-stu-id="7c187-115">Add English language</span></span>
    * <span data-ttu-id="7c187-116">アプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="7c187-116">Fill in the app name.</span></span>
    * <span data-ttu-id="7c187-117">アプリの簡単な説明を英語で入力します。</span><span class="sxs-lookup"><span data-stu-id="7c187-117">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="7c187-118">アプリの詳しい説明を英語で入力します。</span><span class="sxs-lookup"><span data-stu-id="7c187-118">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="7c187-119">詳細については、「このアプリは、フランス語で利用可能です」という行も追加してください。</span><span class="sxs-lookup"><span data-stu-id="7c187-119">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="7c187-120">アプリ UI の画像 (英語) をアップロードします。</span><span class="sxs-lookup"><span data-stu-id="7c187-120">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="7c187-121">フランス語を追加する</span><span class="sxs-lookup"><span data-stu-id="7c187-121">Add French language</span></span>
    * <span data-ttu-id="7c187-122">アプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="7c187-122">Fill in the app name.</span></span>
    * <span data-ttu-id="7c187-123">フランス語でアプリの簡単な説明を記入します。</span><span class="sxs-lookup"><span data-stu-id="7c187-123">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="7c187-124">アプリの詳しい説明をフランス語で入力します。</span><span class="sxs-lookup"><span data-stu-id="7c187-124">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="7c187-125">アプリの UI のイメージ (フランス語) をアップロードします。</span><span class="sxs-lookup"><span data-stu-id="7c187-125">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="7c187-126">英語を使用してアップロードする画像は、AppSource で使用されているものになります。</span><span class="sxs-lookup"><span data-stu-id="7c187-126">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="7c187-127">アプリマニフェスト内の文字列のローカライズ</span><span class="sxs-lookup"><span data-stu-id="7c187-127">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="7c187-128">アプリを適切にローカライズするには、Microsoft Teams アプリスキーマ v1.1 を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7c187-128">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="7c187-129">これを行うには、 `$schema` ファイルの manifest.jsの属性を ' ' に設定 https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json し、' manifestversion ' プロパティを ' 1.7 ' に更新します。</span><span class="sxs-lookup"><span data-stu-id="7c187-129">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="7c187-130">変更時の manifest.js例</span><span class="sxs-lookup"><span data-stu-id="7c187-130">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="7c187-131">次に、アプリケーションでサポートされている既定の言語で ' localizationInfo ' プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="7c187-131">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="7c187-132">ユーザーのクライアント設定がその他の言語と一致しない場合、既定の言語が最終的なフォールバック言語として使用されます。</span><span class="sxs-lookup"><span data-stu-id="7c187-132">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="7c187-133">変更時の manifest.js例</span><span class="sxs-lookup"><span data-stu-id="7c187-133">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="7c187-134">マニフェスト内のすべてのユーザーが接続した文字列の翻訳を含む、追加の json ファイルを提供できます。</span><span class="sxs-lookup"><span data-stu-id="7c187-134">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="7c187-135">これらのファイルは、[ローカライズファイル JSON スキーマ](../../resources/schema/localization-schema.md)に準拠している必要があり、マニフェストの ' localizationInfo ' プロパティに追加されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="7c187-135">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="7c187-136">各ファイルは、Teams クライアントが適切な文字列を選択するために使用する言語タグに関連付けています。</span><span class="sxs-lookup"><span data-stu-id="7c187-136">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="7c187-137">言語タグはの形式を取り <language> - <region> ますが、目的の言語を <region> サポートするすべての地域を対象とした部分を省略することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7c187-137">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="7c187-138">Teams クライアントは、次の順序で文字列を適用します。 default language strings-> user's language only 文字列-> ユーザーの言語 + ユーザーの地域文字列。</span><span class="sxs-lookup"><span data-stu-id="7c187-138">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="7c187-139">たとえば、既定の言語である "fr" (フランス語、すべての地域)、および ' en ' (英語、すべての地域) と ' en gb ' (英語、英国) の追加の言語ファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="7c187-139">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="7c187-140">ユーザーの言語が "en gb" に設定されている場合:</span><span class="sxs-lookup"><span data-stu-id="7c187-140">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="7c187-141">Teams クライアントは、' fr ' 文字列を ' en ' 文字列で上書きする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7c187-141">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="7c187-142">これらの文字列を ' en gb ' の文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="7c187-142">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="7c187-143">ユーザーの言語が "en-us" に設定されている場合:</span><span class="sxs-lookup"><span data-stu-id="7c187-143">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="7c187-144">Teams クライアントは、' fr ' 文字列を ' en ' 文字列で上書きする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7c187-144">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="7c187-145">' En-ca ' ローカライズは提供されていないため、' en ' ローカライズが使用されます。</span><span class="sxs-lookup"><span data-stu-id="7c187-145">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="7c187-146">ユーザーの言語が "es-es" に設定されている場合、Teams クライアントは ' fr ' 文字列を受け取ります。これらの言語ファイルでは上書きされません。</span><span class="sxs-lookup"><span data-stu-id="7c187-146">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="7c187-147">そのため、マニフェストには、("en-us" の代わりに ' en ' ではなく) 最上位レベルの翻訳を言語のみで提供し、地域レベルの上書きのみを必要とする少数の文字列に対して提供することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7c187-147">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="7c187-148">変更時の manifest.js例</span><span class="sxs-lookup"><span data-stu-id="7c187-148">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="7c187-149">ローカライズの例-json ファイル</span><span class="sxs-lookup"><span data-stu-id="7c187-149">Example localization .json file</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json",
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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="7c187-150">ユーザーからのローカライズされたテキストの送信を処理する</span><span class="sxs-lookup"><span data-stu-id="7c187-150">Handling localized text submissions from your users</span></span>

<span data-ttu-id="7c187-151">アプリケーションのローカライズ版を提供している場合は、ユーザーが同じ言語で応答することが非常に高い可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7c187-151">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="7c187-152">Teams はユーザーの送信を既定の言語に変換しないので、アプリでそれを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7c187-152">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="7c187-153">たとえば、ローカライズを指定すると、 `commandList` ボットへの応答は、既定の言語ではなく、コマンドのローカライズされたテキストになります。</span><span class="sxs-lookup"><span data-stu-id="7c187-153">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="7c187-154">アプリは適切に応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7c187-154">Your app will need to respond appropriately.</span></span>
