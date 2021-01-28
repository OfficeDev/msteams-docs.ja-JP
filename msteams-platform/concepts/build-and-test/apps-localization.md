---
title: アプリのローカライズ
description: Microsoft Teams アプリをローカライズする際の考慮事項について説明します。
ms.topic: conceptual
keywords: teams publish store office publishing AppSource ローカライズ言語
ms.date: 05/15/2018
ms.openlocfilehash: 69bee0ee11238dc0e461e4fddf8ed01f0cfcccde
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014300"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="d41a0-104">Microsoft Teams アプリのローカライズ</span><span class="sxs-lookup"><span data-stu-id="d41a0-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="d41a0-105">Microsoft Teams アプリをローカライズする場合、考慮する必要がある主な領域は 3 つがあります。</span><span class="sxs-lookup"><span data-stu-id="d41a0-105">When localizing your Microsoft Teams app there are three major areas you need to consider.</span></span>

1. <span data-ttu-id="d41a0-106">AppSource 登録情報 (アプリ ストアに公開する場合)。</span><span class="sxs-lookup"><span data-stu-id="d41a0-106">Your AppSource listing (if you're publishing to the app store).</span></span>
1. <span data-ttu-id="d41a0-107">アプリ マニフェスト内のエンドユーザー向け文字列 (ボット コマンドなど)。</span><span class="sxs-lookup"><span data-stu-id="d41a0-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="d41a0-108">ユーザーから送信されたローカライズされたテキストへの応答。</span><span class="sxs-lookup"><span data-stu-id="d41a0-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="d41a0-109">AppSource 登録情報のローカライズ</span><span class="sxs-lookup"><span data-stu-id="d41a0-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="d41a0-110">アプリ ストアに公開する場合、AppSource 登録情報のローカライズはまだサポートされていないことに注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d41a0-110">If you're publishing to the app store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="d41a0-111">ただし、アプリ ストアでのローカライズされた登録情報のサポートの準備として、登録情報に言語を追加できます。</span><span class="sxs-lookup"><span data-stu-id="d41a0-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="d41a0-112">現在、登録情報のパートナー センターで指定した既定[](/office/dev/store/submit-to-appsource-via-partner-center)の (英語) 言語情報だけが、アプリの[AppSource Web](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1)サイトの登録情報に表示されます。</span><span class="sxs-lookup"><span data-stu-id="d41a0-112">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

<span data-ttu-id="d41a0-113">アプリの追加言語を構成するには、パートナー[](/office/dev/store/submit-to-appsource-via-partner-center)センターで、英語とアプリの追加言語の両方を選択します。</span><span class="sxs-lookup"><span data-stu-id="d41a0-113">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="d41a0-114">この例ではフランス語が使用されています。</span><span class="sxs-lookup"><span data-stu-id="d41a0-114">French is used in this example.</span></span>

1. <span data-ttu-id="d41a0-115">英語を追加する</span><span class="sxs-lookup"><span data-stu-id="d41a0-115">Add English language</span></span>
    * <span data-ttu-id="d41a0-116">アプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="d41a0-116">Fill in the app name.</span></span>
    * <span data-ttu-id="d41a0-117">アプリの簡単な説明を英語で入力します。</span><span class="sxs-lookup"><span data-stu-id="d41a0-117">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="d41a0-118">アプリの詳細な説明を英語で入力します。</span><span class="sxs-lookup"><span data-stu-id="d41a0-118">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="d41a0-119">詳しい説明では、「このアプリはフランス語で利用できます」という行も追加してください。</span><span class="sxs-lookup"><span data-stu-id="d41a0-119">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="d41a0-120">アプリ UI の画像をアップロードします (英語)。</span><span class="sxs-lookup"><span data-stu-id="d41a0-120">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="d41a0-121">フランス語を追加する</span><span class="sxs-lookup"><span data-stu-id="d41a0-121">Add French language</span></span>
    * <span data-ttu-id="d41a0-122">アプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="d41a0-122">Fill in the app name.</span></span>
    * <span data-ttu-id="d41a0-123">アプリの簡単な説明をフランス語で入力します。</span><span class="sxs-lookup"><span data-stu-id="d41a0-123">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="d41a0-124">アプリの詳細な説明をフランス語で入力します。</span><span class="sxs-lookup"><span data-stu-id="d41a0-124">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="d41a0-125">アプリ UI の画像をアップロードします (フランス語)。</span><span class="sxs-lookup"><span data-stu-id="d41a0-125">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="d41a0-126">英語でアップロードする画像は、AppSource で使用される画像です。</span><span class="sxs-lookup"><span data-stu-id="d41a0-126">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="d41a0-127">アプリ マニフェスト内の文字列のローカライズ</span><span class="sxs-lookup"><span data-stu-id="d41a0-127">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="d41a0-128">アプリを適切にローカライズするには、Microsoft Teams アプリ スキーマ v1.5+ を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d41a0-128">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="d41a0-129">これを行うには、manifest.json ファイルの属性を ' に設定し、'manifestVersion' プロパティを `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json '1.7' に更新します。</span><span class="sxs-lookup"><span data-stu-id="d41a0-129">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="d41a0-130">変更manifest.jsの例</span><span class="sxs-lookup"><span data-stu-id="d41a0-130">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="d41a0-131">次に、アプリケーションがサポートする既定の言語で "localizationInfo" プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="d41a0-131">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="d41a0-132">ユーザーのクライアント設定が追加の言語と一致しない場合、既定の言語が最終的なフォールバック言語として使用されます。</span><span class="sxs-lookup"><span data-stu-id="d41a0-132">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="d41a0-133">変更manifest.jsの例</span><span class="sxs-lookup"><span data-stu-id="d41a0-133">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="d41a0-134">マニフェスト内のすべてのユーザー向け文字列の翻訳を含む追加の .json ファイルを提供できます。</span><span class="sxs-lookup"><span data-stu-id="d41a0-134">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="d41a0-135">これらのファイルは、ローカライズ ファイル [の JSON](../../resources/schema/localization-schema.md) スキーマに準拠し、マニフェストの 'localizationInfo' プロパティに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d41a0-135">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="d41a0-136">各ファイルは、Teams クライアントが適切な文字列を選択するために使用する言語タグに関連付けられている。</span><span class="sxs-lookup"><span data-stu-id="d41a0-136">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="d41a0-137">言語タグは形式をとっていますが、目的の言語をサポートしているすべての地域を対象とする部分を省略 <language> - <region> <region> することが推奨されます。</span><span class="sxs-lookup"><span data-stu-id="d41a0-137">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="d41a0-138">Teams クライアントは、次の順序で文字列を適用します。既定の言語文字列 -> ユーザーの言語のみ文字列 -> ユーザーの言語 + ユーザーの地域文字列。</span><span class="sxs-lookup"><span data-stu-id="d41a0-138">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="d41a0-139">たとえば、"fr" (フランス語、すべての地域) の既定の言語と、'en' (英語、すべての地域) と 'en-gb' (英語、英国) の追加の言語ファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="d41a0-139">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="d41a0-140">ユーザーの言語が 'en-gb' に設定されている場合:</span><span class="sxs-lookup"><span data-stu-id="d41a0-140">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="d41a0-141">Teams クライアントは、'fr' 文字列を 'en' 文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="d41a0-141">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="d41a0-142">'en-gb' 文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="d41a0-142">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="d41a0-143">ユーザーの言語が 'en-ca' に設定されている場合:</span><span class="sxs-lookup"><span data-stu-id="d41a0-143">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="d41a0-144">Teams クライアントは、'fr' 文字列を 'en' 文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="d41a0-144">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="d41a0-145">'en-ca' ローカライズは提供されていないので、'en' ローカライズが使用されます。</span><span class="sxs-lookup"><span data-stu-id="d41a0-145">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="d41a0-146">ユーザーの言語が 'es-es' に設定されている場合、Teams クライアントは "fr" 文字列を受け取り、どの言語ファイルでも上書きしません。</span><span class="sxs-lookup"><span data-stu-id="d41a0-146">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="d41a0-147">したがって、言語専用のトップ レベルの翻訳をマニフェストで提供し ('en-us' ではなく'en')、それらを必要とする少数の文字列に対する地域レベルのオーバーライドのみを提供する方法を強く推奨します。</span><span class="sxs-lookup"><span data-stu-id="d41a0-147">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="d41a0-148">変更manifest.jsの例</span><span class="sxs-lookup"><span data-stu-id="d41a0-148">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="d41a0-149">ローカライズ .json ファイルの例</span><span class="sxs-lookup"><span data-stu-id="d41a0-149">Example localization .json file</span></span>

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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="d41a0-150">ユーザーからのローカライズされたテキスト送信の処理</span><span class="sxs-lookup"><span data-stu-id="d41a0-150">Handling localized text submissions from your users</span></span>

<span data-ttu-id="d41a0-151">アプリケーションのローカライズバージョンを提供する場合は、ユーザーが同じ言語で応答する可能性が高い可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d41a0-151">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="d41a0-152">Teams はユーザーの申請を既定の言語に変換し戻すのではないので、アプリで処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d41a0-152">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="d41a0-153">たとえば、ローカライズを指定した場合、ボットへの応答は、既定の言語ではなく、コマンドのローカライズされたテキスト `commandList` になります。</span><span class="sxs-lookup"><span data-stu-id="d41a0-153">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="d41a0-154">アプリは適切に応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d41a0-154">Your app will need to respond appropriately.</span></span>
