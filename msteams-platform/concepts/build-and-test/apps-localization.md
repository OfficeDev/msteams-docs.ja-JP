---
title: アプリをローカライズする
description: アプリのローカライズに関する考慮事項Microsoft Teamsします。
ms.topic: conceptual
localization_priority: Normal
keywords: teams publishs store office publishing AppSource ローカライズ言語
ms.date: 05/15/2018
ms.openlocfilehash: 5410d6f829c3fec9b5d631452e459bd276df472e
ms.sourcegitcommit: c145d52b2d4daa7655e6c3ddfa739fa1beeb8d6a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2021
ms.locfileid: "53455214"
---
# <a name="localize-your-app"></a><span data-ttu-id="02f92-104">アプリをローカライズする</span><span class="sxs-lookup"><span data-stu-id="02f92-104">Localize your app</span></span>

<span data-ttu-id="02f92-105">アプリをローカライズするには、次の要素Microsoft Teams必要があります。</span><span class="sxs-lookup"><span data-stu-id="02f92-105">You must consider the following factors to localize your Microsoft Teams app:</span></span>

1. <span data-ttu-id="02f92-106">[AppSource リストをローカライズします](#localize-your-appsource-listing)。</span><span class="sxs-lookup"><span data-stu-id="02f92-106">[Localize your AppSource listing](#localize-your-appsource-listing).</span></span>
1. <span data-ttu-id="02f92-107">[アプリ マニフェスト内の文字列をローカライズします](#localize-strings-in-your-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="02f92-107">[Localize strings in your app manifest](#localize-strings-in-your-app-manifest).</span></span> 
1. <span data-ttu-id="02f92-108">[ユーザーからのローカライズされたテキスト送信を処理します](#handle-localized-text-submissions-from-your-users)。</span><span class="sxs-lookup"><span data-stu-id="02f92-108">[Handle localized text submissions from your users](#handle-localized-text-submissions-from-your-users).</span></span>

## <a name="localize-your-appsource-listing"></a><span data-ttu-id="02f92-109">AppSource リストをローカライズする</span><span class="sxs-lookup"><span data-stu-id="02f92-109">Localize your AppSource listing</span></span>

<span data-ttu-id="02f92-110">アプリをストアに発行する場合は、AppSource リストのローカライズがまだサポートされていないことに注意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02f92-110">If you are publishing the app to the store, you must be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="02f92-111">アプリ ストアでローカライズされたリストをサポートするには、リスティングに追加の言語を追加できます。</span><span class="sxs-lookup"><span data-stu-id="02f92-111">To support localized listings in the app store, you can add additional languages to your listing.</span></span> <span data-ttu-id="02f92-112">登録情報のパートナー センターで[](/office/dev/store/submit-to-appsource-via-partner-center)指定した既定の言語情報は、アプリの[AppSource Web](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource は、チームのすべてのニーズに対応する 1 つの場所です。チャット、会議、通話、ファイル、ツールなど、すべての情報をまとめ、チームワークを高めることができます。")サイトの一覧に表示されます。</span><span class="sxs-lookup"><span data-stu-id="02f92-112">The default language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing appears in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource is one place for all your team needs. bring everything together including chats, meetings, calls, files, and tools to enable more productive teamwork.") listing for your app.</span></span> <span data-ttu-id="02f92-113">現在、既定の言語は英語です。</span><span class="sxs-lookup"><span data-stu-id="02f92-113">Currently, the default language is English.</span></span>

### <a name="configure-localization"></a><span data-ttu-id="02f92-114">ローカライズの構成</span><span class="sxs-lookup"><span data-stu-id="02f92-114">Configure localization</span></span>

<span data-ttu-id="02f92-115">アプリの追加の言語を構成するには、 [パートナー](/office/dev/store/submit-to-appsource-via-partner-center)センターで、英語とアプリの追加言語の両方を選択します。</span><span class="sxs-lookup"><span data-stu-id="02f92-115">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="02f92-116">次の例では、フランス語を追加の言語として使用します。</span><span class="sxs-lookup"><span data-stu-id="02f92-116">French is used as an additional language in the following example:</span></span>

1. <span data-ttu-id="02f92-117">英語を追加する</span><span class="sxs-lookup"><span data-stu-id="02f92-117">Add English language</span></span>
    * <span data-ttu-id="02f92-118">アプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="02f92-118">Enter the app name.</span></span>
    * <span data-ttu-id="02f92-119">アプリの簡単な説明を英語で入力します。</span><span class="sxs-lookup"><span data-stu-id="02f92-119">Enter a short description of the app in English.</span></span>
    * <span data-ttu-id="02f92-120">アプリの長い説明を英語で入力します。</span><span class="sxs-lookup"><span data-stu-id="02f92-120">Enter the long description of the app in English.</span></span>
    * <span data-ttu-id="02f92-121">長い説明で、「このアプリ **はフランス語で使用できます。」と入力します**。</span><span class="sxs-lookup"><span data-stu-id="02f92-121">In the long description, enter: **This app is available in French**.</span></span>
    * <span data-ttu-id="02f92-122">アップロード UI のイメージを確認します (英語)。</span><span class="sxs-lookup"><span data-stu-id="02f92-122">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="02f92-123">フランス語を追加する</span><span class="sxs-lookup"><span data-stu-id="02f92-123">Add French language</span></span>
    * <span data-ttu-id="02f92-124">アプリ名を入力します。</span><span class="sxs-lookup"><span data-stu-id="02f92-124">Enter the app name.</span></span>
    * <span data-ttu-id="02f92-125">アプリの簡単な説明をフランス語で入力します。</span><span class="sxs-lookup"><span data-stu-id="02f92-125">Enter a short description of the app in French.</span></span>
    * <span data-ttu-id="02f92-126">アプリの長い説明をフランス語で入力します。</span><span class="sxs-lookup"><span data-stu-id="02f92-126">Enter the long description of the app in French.</span></span>
    * <span data-ttu-id="02f92-127">アップロード UI のイメージを確認します (フランス語)。</span><span class="sxs-lookup"><span data-stu-id="02f92-127">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="02f92-128">英語でアップロードする画像は、AppSource で使用されます。</span><span class="sxs-lookup"><span data-stu-id="02f92-128">The images that you upload with the English language are used in AppSource.</span></span>

## <a name="localize-strings-in-your-app-manifest"></a><span data-ttu-id="02f92-129">アプリ マニフェスト内の文字列をローカライズする</span><span class="sxs-lookup"><span data-stu-id="02f92-129">Localize strings in your app manifest</span></span>

<span data-ttu-id="02f92-130">アプリをローカライズするには、Microsoft Teamsスキーマ以降を使用 `v1.5` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02f92-130">You must use the Microsoft Teams app schema `v1.5` and later to localize your app.</span></span> <span data-ttu-id="02f92-131">この操作を行うには、manifest.jsの属性をファイルに設定し、プロパティをバージョン (この場合) `$schema` **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** `manifestVersion` `$schema` に `1.5` 更新します。</span><span class="sxs-lookup"><span data-stu-id="02f92-131">You can do this by setting the `$schema` attribute in your manifest.json file to **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** or higher and updating the `manifestVersion` property to `$schema` version (`1.5` in this case).</span></span> 

<span data-ttu-id="02f92-132">アプリケーションでサポートされている `localizationInfo` 既定の言語でプロパティを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02f92-132">You must add the `localizationInfo` property with the default language that your application supports.</span></span> <span data-ttu-id="02f92-133">既定の言語は、ユーザーのクライアント設定が追加の言語と一致しない場合、最終的なフォールバック言語として使用されます。</span><span class="sxs-lookup"><span data-stu-id="02f92-133">The default language is used as the final fallback language if the user's client settings do not match with any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="02f92-134">変更時manifest.js例</span><span class="sxs-lookup"><span data-stu-id="02f92-134">Example manifest.json change</span></span>

<span data-ttu-id="02f92-135">次のmanifest.jsは、アプリケーションでサポートされている既定の言語でプロパティを追加 `localizationInfo` するのに役立ちます `additionalLanguages` 。</span><span class="sxs-lookup"><span data-stu-id="02f92-135">The following manifest.json helps to add the `localizationInfo` property with the default language that your application supports along with `additionalLanguages`:</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "localizationInfo": {
        "defaultLanguageTag": "en",
        "additionalLanguages": [
            {
                "languageTag": "es-mx",
                "file": "es-mx.json"
            }
        ]
    }
  ...
}
```

### <a name="example-localization-json-change"></a><span data-ttu-id="02f92-136">ローカライズ .json の変更例</span><span class="sxs-lookup"><span data-stu-id="02f92-136">Example localization .json change</span></span>

<span data-ttu-id="02f92-137">ローカライズ .json の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="02f92-137">Following is an example for localization .json:</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```


<span data-ttu-id="02f92-138">マニフェスト内のすべてのユーザー向け文字列の翻訳を含む追加の .json ファイルを提供できます。</span><span class="sxs-lookup"><span data-stu-id="02f92-138">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="02f92-139">これらのファイルは、ローカライズ ファイル JSON スキーマに準拠している [必要があります](../../resources/schema/localization-schema.md) 。マニフェストの `localizationInfo` プロパティに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02f92-139">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the `localizationInfo` property of your manifest.</span></span> <span data-ttu-id="02f92-140">各ファイルは言語タグに関連付け、Teamsを使用して適切な文字列を選択します。</span><span class="sxs-lookup"><span data-stu-id="02f92-140">Each file correlates to a language tag, which the Teams client uses to select the appropriate strings.</span></span> <span data-ttu-id="02f92-141">言語タグの形式を使用しますが、目的の言語をサポートしているすべての地域を対象とする部分 `<language>-<region>` `<region>` を省略できます。</span><span class="sxs-lookup"><span data-stu-id="02f92-141">The language tag takes the form of `<language>-<region>` but you can omit the `<region>` portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="02f92-142">Teams クライアントは、既定の言語文字列 -> ユーザーの言語のみ -> ユーザーの言語 + ユーザーの地域文字列の順序で文字列を適用します。</span><span class="sxs-lookup"><span data-stu-id="02f92-142">The Teams client applies the strings in the following order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="02f92-143">たとえば、'fr' (フランス語、すべての地域) の既定の言語と、'en' (英語、すべての地域) と 'en-gb' (英語、英国) の追加言語ファイルを指定すると、ユーザーの言語は 'en-gb' に設定されます。</span><span class="sxs-lookup"><span data-stu-id="02f92-143">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain), the user's language is set to 'en-gb'.</span></span> <span data-ttu-id="02f92-144">次の変更は、言語の選択に基づいて行います。</span><span class="sxs-lookup"><span data-stu-id="02f92-144">The following changes take place based on the language selection:</span></span>

1. <span data-ttu-id="02f92-145">クライアントTeams'fr' 文字列を受け取り、'en' 文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="02f92-145">The Teams client takes the 'fr' strings and overwrite them with the 'en' strings.</span></span>
1. <span data-ttu-id="02f92-146">'en' 文字列を 'en-gb' 文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="02f92-146">Overwrite the 'en' strings with the 'en-gb' strings.</span></span>

<span data-ttu-id="02f92-147">ユーザーの言語が 'en-ca' に設定されている場合、言語の選択に基づいて次の変更が行います。</span><span class="sxs-lookup"><span data-stu-id="02f92-147">If the user's language is set to 'en-ca', the following changes take place based on the language selection:</span></span> 

1. <span data-ttu-id="02f92-148">クライアントTeams'fr' 文字列を受け取り、'en' 文字列で上書きします。</span><span class="sxs-lookup"><span data-stu-id="02f92-148">The Teams client takes the 'fr' strings and overwrite them with the 'en' strings.</span></span>
1. <span data-ttu-id="02f92-149">'en-ca' ローカライズは指定されていないので、'en' ローカライズが使用されます。</span><span class="sxs-lookup"><span data-stu-id="02f92-149">Since no 'en-ca' localization is supplied, the 'en\` localizations are used.</span></span>

<span data-ttu-id="02f92-150">ユーザーの言語が 'es-es' に設定されている場合、クライアントは 'fr' Teamsを受け取る。</span><span class="sxs-lookup"><span data-stu-id="02f92-150">If the user's language is set to 'es-es', the Teams client takes the 'fr' strings.</span></span> <span data-ttu-id="02f92-151">このTeamsクライアントは、言語ファイルの文字列を上書きしません。'es' または 'es-es' 変換が提供されていない。</span><span class="sxs-lookup"><span data-stu-id="02f92-151">The Teams client does not override the strings with any of the language files as no 'es' or 'es-es' translation is provided.</span></span>

<span data-ttu-id="02f92-152">したがって、マニフェストにトップ レベルの言語翻訳のみを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02f92-152">Therefore, you must provide top level, language only translations in your manifest.</span></span> <span data-ttu-id="02f92-153">たとえば、'en-us' の代わりに 'en' を使用します。</span><span class="sxs-lookup"><span data-stu-id="02f92-153">For example, 'en' instead of 'en-us'.</span></span> <span data-ttu-id="02f92-154">地域レベルのオーバーライドは、必要な少数の文字列にのみ指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02f92-154">You must provide region level overrides only for the few strings that need them.</span></span> 

### <a name="example-manifestjson-change"></a><span data-ttu-id="02f92-155">変更時manifest.js例</span><span class="sxs-lookup"><span data-stu-id="02f92-155">Example manifest.json change</span></span>

<span data-ttu-id="02f92-156">変更manifest.js次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="02f92-156">The manifest.json change is shown in the following example:</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="02f92-157">ローカライズ .json ファイルの例</span><span class="sxs-lookup"><span data-stu-id="02f92-157">Example localization .json file</span></span>

 <span data-ttu-id="02f92-158">変更localization.js次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="02f92-158">The localization.json change is shown in the following example:</span></span>

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

## <a name="handle-localized-text-submissions-from-your-users"></a><span data-ttu-id="02f92-159">ユーザーからのローカライズされたテキスト送信を処理する</span><span class="sxs-lookup"><span data-stu-id="02f92-159">Handle localized text submissions from your users</span></span>

<span data-ttu-id="02f92-160">アプリケーションのローカライズされたバージョンを提供する場合、ユーザーは同じ言語で応答します。</span><span class="sxs-lookup"><span data-stu-id="02f92-160">If your provide localized versions of your application, the users respond with the same language.</span></span> <span data-ttu-id="02f92-161">ユーザー Teams既定の言語に変換されないので、アプリはローカライズされた言語の応答を処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02f92-161">As Teams does not translate the user submissions back to the default language, your app must handle the localized language responses.</span></span> <span data-ttu-id="02f92-162">たとえば、ローカライズされた言語を指定した場合、ボットに対する応答はコマンドのローカライズされたテキストで、既定の言語 `commandList` ではありません。</span><span class="sxs-lookup"><span data-stu-id="02f92-162">For example, if you provide a localized `commandList`, the responses to your bot are the localized text of the command, not the default language.</span></span> <span data-ttu-id="02f92-163">アプリは適切に対応する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02f92-163">Your app must respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="02f92-164">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="02f92-164">Code sample</span></span>

| <span data-ttu-id="02f92-165">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="02f92-165">Sample name</span></span> | <span data-ttu-id="02f92-166">説明</span><span class="sxs-lookup"><span data-stu-id="02f92-166">Description</span></span> | <span data-ttu-id="02f92-167">.NET</span><span class="sxs-lookup"><span data-stu-id="02f92-167">.NET</span></span> | <span data-ttu-id="02f92-168">Node.js</span><span class="sxs-lookup"><span data-stu-id="02f92-168">Node.js</span></span> |
|-------------|-------------|------|------|
| <span data-ttu-id="02f92-169">アプリのローカライズ</span><span class="sxs-lookup"><span data-stu-id="02f92-169">App Localization</span></span> | <span data-ttu-id="02f92-170">Microsoft Teamsタブを使用してアプリのローカライズを行います。</span><span class="sxs-lookup"><span data-stu-id="02f92-170">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="02f92-171">表示</span><span class="sxs-lookup"><span data-stu-id="02f92-171">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[<span data-ttu-id="02f92-172">表示</span><span class="sxs-lookup"><span data-stu-id="02f92-172">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

