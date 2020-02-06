---
title: チームアプリのローカライズ
description: アプリのローカライズに関する問題について説明します。
keywords: teams 発行ストア office 発行アプリソースのローカライズ言語
ms.date: 05/15/2018
ms.openlocfilehash: b09f33e53303587e81b445c012de92b11dd90580
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674742"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="92327-104">Microsoft Teams アプリのローカライズ</span><span class="sxs-lookup"><span data-stu-id="92327-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="92327-105">Microsoft Teams アプリをローカライズする場合は、考慮する必要がある3つの主要な領域があります。</span><span class="sxs-lookup"><span data-stu-id="92327-105">When localizing your Microsoft Teams app there are three major areas you need to consider.</span></span>

1. <span data-ttu-id="92327-106">AppSource リスト (アプリストアに公開している場合)。</span><span class="sxs-lookup"><span data-stu-id="92327-106">Your AppSource listing (if you're publishing to the app store).</span></span>
1. <span data-ttu-id="92327-107">アプリケーションマニフェスト内のエンドユーザーが使用している文字列 (bot コマンドなど)。</span><span class="sxs-lookup"><span data-stu-id="92327-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="92327-108">ユーザーから送信されるローカライズされたテキストに応答する。</span><span class="sxs-lookup"><span data-stu-id="92327-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="92327-109">AppSource リストのローカライズ</span><span class="sxs-lookup"><span data-stu-id="92327-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="92327-110">アプリストアに発行している場合は、AppSource リストのローカライズがまだサポートされていないことに注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92327-110">If you're publishing to the app store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="92327-111">ただし、アプリストアでローカライズされたリストをサポートするための準備として、追加の言語を一覧に追加することができます。</span><span class="sxs-lookup"><span data-stu-id="92327-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="92327-112">現在、リストの[パートナーセンター](/dev/store/use-partner-center-to-submit-to-appsource)で提供される既定の (英語) の言語情報のみが、アプリの[appsource web サイト](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1)の一覧に表示されます。</span><span class="sxs-lookup"><span data-stu-id="92327-112">Currently only the default (English) language information you provide in [Partner Center](/dev/store/use-partner-center-to-submit-to-appsource) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

<span data-ttu-id="92327-113">アプリの追加の言語を構成するには、[パートナーセンター](/dev/store/use-partner-center-to-submit-to-appsource)で、英語とアプリの追加言語を選択します。</span><span class="sxs-lookup"><span data-stu-id="92327-113">To configure an additional language for your app, in [Partner Center](/dev/store/use-partner-center-to-submit-to-appsource), select both English and the additional language of the app.</span></span> <span data-ttu-id="92327-114">この例では、フランス語が使用されています。</span><span class="sxs-lookup"><span data-stu-id="92327-114">French is used in this example.</span></span>

1. <span data-ttu-id="92327-115">英語の言語を追加する</span><span class="sxs-lookup"><span data-stu-id="92327-115">Add English language</span></span>
    * <span data-ttu-id="92327-116">アプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="92327-116">Fill in the app name.</span></span>
    * <span data-ttu-id="92327-117">アプリの簡単な説明を英語で入力します。</span><span class="sxs-lookup"><span data-stu-id="92327-117">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="92327-118">アプリの詳しい説明を英語で入力します。</span><span class="sxs-lookup"><span data-stu-id="92327-118">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="92327-119">詳細については、「このアプリは、フランス語で利用可能です」という行も追加してください。</span><span class="sxs-lookup"><span data-stu-id="92327-119">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="92327-120">アプリ UI の画像 (英語) をアップロードします。</span><span class="sxs-lookup"><span data-stu-id="92327-120">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="92327-121">フランス語を追加する</span><span class="sxs-lookup"><span data-stu-id="92327-121">Add French language</span></span>
    * <span data-ttu-id="92327-122">アプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="92327-122">Fill in the app name.</span></span>
    * <span data-ttu-id="92327-123">フランス語でアプリの簡単な説明を記入します。</span><span class="sxs-lookup"><span data-stu-id="92327-123">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="92327-124">アプリの詳しい説明をフランス語で入力します。</span><span class="sxs-lookup"><span data-stu-id="92327-124">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="92327-125">アプリの UI のイメージ (フランス語) をアップロードします。</span><span class="sxs-lookup"><span data-stu-id="92327-125">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="92327-126">英語を使用してアップロードする画像は、AppSource で使用されているものになります。</span><span class="sxs-lookup"><span data-stu-id="92327-126">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="92327-127">アプリマニフェスト内の文字列のローカライズ</span><span class="sxs-lookup"><span data-stu-id="92327-127">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="92327-128">アプリを適切にローカライズするには、Microsoft Teams アプリスキーマ v1.1 を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92327-128">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="92327-129">これを行うには、マニフェスト`$schema`の json ファイルの属性を 'https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json' に設定し、' manifestversion ' プロパティを ' 1.5 ' に更新します。</span><span class="sxs-lookup"><span data-stu-id="92327-129">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json' and updating the 'manifestVersion' property to '1.5'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="92327-130">サンプルの manifest 変更</span><span class="sxs-lookup"><span data-stu-id="92327-130">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="92327-131">次に、アプリケーションでサポートされている既定の言語で ' localizationInfo ' プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="92327-131">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="92327-132">ユーザーのクライアント設定がその他の言語と一致しない場合、既定の言語が最終的なフォールバック言語として使用されます。</span><span class="sxs-lookup"><span data-stu-id="92327-132">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="92327-133">サンプルの manifest 変更</span><span class="sxs-lookup"><span data-stu-id="92327-133">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="92327-134">マニフェスト内のすべてのユーザーが接続した文字列の翻訳を含む、追加の json ファイルを提供できます。</span><span class="sxs-lookup"><span data-stu-id="92327-134">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="92327-135">これらのファイルは、[ローカライズファイル JSON スキーマ](~/resources/schema/localization-schema.md)に準拠している必要があり、マニフェストの ' localizationInfo ' プロパティに追加されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="92327-135">These files must adhere to the [Localization file JSON schema](~/resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="92327-136">各ファイルは、Teams クライアントが適切な文字列を選択するために使用する言語タグに関連付けています。</span><span class="sxs-lookup"><span data-stu-id="92327-136">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="92327-137">言語タグ<language> - <region>はの形式を取りますが、目的の言語を<region>サポートするすべての地域を対象とした部分を省略することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="92327-137">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="92327-138">Teams クライアントは、次の順序で文字列を適用します。 default language strings-> user's language only 文字列-> ユーザーの言語 + ユーザーの地域文字列。</span><span class="sxs-lookup"><span data-stu-id="92327-138">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="92327-139">たとえば、既定の言語である "fr" (フランス語、すべての地域)、および ' en ' (英語、すべての地域) と ' en gb ' (英語、英国) の追加の言語ファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="92327-139">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="92327-140">ユーザーの言語が "en gb" に設定されている場合:</span><span class="sxs-lookup"><span data-stu-id="92327-140">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="92327-141">Teams クライアントは、' fr ' 文字列を ' en ' 文字列で上書きする必要があります。</span><span class="sxs-lookup"><span data-stu-id="92327-141">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="92327-142">これらの文字列を ' en gb ' の文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="92327-142">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="92327-143">ユーザーの言語が "en-us" に設定されている場合:</span><span class="sxs-lookup"><span data-stu-id="92327-143">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="92327-144">Teams クライアントは、' fr ' 文字列を ' en ' 文字列で上書きする必要があります。</span><span class="sxs-lookup"><span data-stu-id="92327-144">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="92327-145">' En-ca ' localazation 指定されていないため、' en ' ローカライズが使用されます。</span><span class="sxs-lookup"><span data-stu-id="92327-145">Since no 'en-ca' localazation is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="92327-146">ユーザーの言語が "es-es" に設定されている場合、Teams クライアントは ' fr ' 文字列を受け取ります。これらの言語ファイルでは上書きされません。</span><span class="sxs-lookup"><span data-stu-id="92327-146">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="92327-147">そのため、マニフェストには、("en-us" の代わりに ' en ' ではなく) 最上位レベルの翻訳を言語のみで提供し、地域レベルの上書きのみを必要とする少数の文字列に対して提供することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="92327-147">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="92327-148">サンプルの manifest 変更</span><span class="sxs-lookup"><span data-stu-id="92327-148">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="92327-149">ローカライズの例-json ファイル</span><span class="sxs-lookup"><span data-stu-id="92327-149">Example localization .json file</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="92327-150">ユーザーからのローカライズされたテキストの送信を処理する</span><span class="sxs-lookup"><span data-stu-id="92327-150">Handling localized text submissions from your users</span></span>

<span data-ttu-id="92327-151">アプリケーションのローカライズ版を提供している場合は、ユーザーが同じ言語で応答することが非常に高い可能性があります。</span><span class="sxs-lookup"><span data-stu-id="92327-151">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="92327-152">Teams はユーザーの送信を既定の言語に変換しないので、アプリでそれを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92327-152">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="92327-153">たとえば、ローカライズ`commandList`を指定すると、ボットへの応答は、既定の言語ではなく、コマンドのローカライズされたテキストになります。</span><span class="sxs-lookup"><span data-stu-id="92327-153">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="92327-154">アプリは適切に応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92327-154">Your app will need to respond appropriately.</span></span>