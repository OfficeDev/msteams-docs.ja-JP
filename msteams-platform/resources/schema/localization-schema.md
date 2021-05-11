---
title: ローカライズ ファイル JSON スキーマ参照
description: ローカライズ ファイルでサポートされているローカライズ スキーマについて説明Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: teams マニフェスト スキーマのローカライズ
ms.date: 05/20/2019
ms.openlocfilehash: 3e4207fb3e862eac18c80ffc49e7c5648ae05c28
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019707"
---
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="b505e-104">リファレンス: ローカライズ ファイル JSON スキーマ</span><span class="sxs-lookup"><span data-stu-id="b505e-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="b505e-105">ローカライズ Microsoft Teamsは、クライアント言語の設定に基づいて提供される言語翻訳について説明します。</span><span class="sxs-lookup"><span data-stu-id="b505e-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="b505e-106">ファイルは、 でホストされるスキーマに準拠している必要があります [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="b505e-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="b505e-107">詳細については、「アプリのローカライズ [」を参照してください](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="b505e-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="b505e-108">サンプル</span><span class="sxs-lookup"><span data-stu-id="b505e-108">Sample</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "name.short": "Le App Studio",
  "name.full": "App Studio pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App Studio.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App Studio.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

<span data-ttu-id="b505e-109">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="b505e-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="b505e-110">$schema</span><span class="sxs-lookup"><span data-stu-id="b505e-110">$schema</span></span>

<span data-ttu-id="b505e-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="b505e-111">**URI**</span></span>

<span data-ttu-id="b505e-112">マニフェスト https:// JSON スキーマを参照する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="b505e-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="b505e-113">マニフェストの先頭にスキーマを指定して、コード エディター IntelliSenseサポートを有効にしてください。`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="b505e-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="b505e-114">name.short</span><span class="sxs-lookup"><span data-stu-id="b505e-114">name.short</span></span>

<span data-ttu-id="b505e-115">**文字列、最大長 30**</span><span class="sxs-lookup"><span data-stu-id="b505e-115">**String, Max Length 30**</span></span>

<span data-ttu-id="b505e-116">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。</span><span class="sxs-lookup"><span data-stu-id="b505e-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="b505e-117">name.full</span><span class="sxs-lookup"><span data-stu-id="b505e-117">name.full</span></span>

<span data-ttu-id="b505e-118">**文字列、最大長 100**</span><span class="sxs-lookup"><span data-stu-id="b505e-118">**String, Max Length 100**</span></span>

<span data-ttu-id="b505e-119">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。</span><span class="sxs-lookup"><span data-stu-id="b505e-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="b505e-120">description.short</span><span class="sxs-lookup"><span data-stu-id="b505e-120">description.short</span></span>

<span data-ttu-id="b505e-121">**文字列、最大長 80**</span><span class="sxs-lookup"><span data-stu-id="b505e-121">**String, Max Length 80**</span></span>

<span data-ttu-id="b505e-122">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。</span><span class="sxs-lookup"><span data-stu-id="b505e-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="b505e-123">description.full</span><span class="sxs-lookup"><span data-stu-id="b505e-123">description.full</span></span>

<span data-ttu-id="b505e-124">**文字列、最大長 4000**</span><span class="sxs-lookup"><span data-stu-id="b505e-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="b505e-125">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。</span><span class="sxs-lookup"><span data-stu-id="b505e-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="b505e-126">staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name</span><span class="sxs-lookup"><span data-stu-id="b505e-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="b505e-127">**文字列、最大長 128**</span><span class="sxs-lookup"><span data-stu-id="b505e-127">**String, Max Length 128**</span></span>

<span data-ttu-id="b505e-128">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="b505e-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="b505e-129">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .command \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="b505e-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="b505e-130">**文字列、最大長 32**</span><span class="sxs-lookup"><span data-stu-id="b505e-130">**String, Max Length 32**</span></span>

<span data-ttu-id="b505e-131">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="b505e-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="b505e-132">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .command \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="b505e-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="b505e-133">**文字列、最大長 128**</span><span class="sxs-lookup"><span data-stu-id="b505e-133">**String, Max Length 128**</span></span>

<span data-ttu-id="b505e-134">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="b505e-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="b505e-135">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="b505e-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="b505e-136">**文字列、最大長 32**</span><span class="sxs-lookup"><span data-stu-id="b505e-136">**String, Max Length 32**</span></span>

<span data-ttu-id="b505e-137">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="b505e-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="b505e-138">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="b505e-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="b505e-139">**文字列、最大長 128**</span><span class="sxs-lookup"><span data-stu-id="b505e-139">**String, Max Length 128**</span></span>

<span data-ttu-id="b505e-140">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="b505e-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="b505e-141">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="b505e-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="b505e-142">**文字列、最大長 32**</span><span class="sxs-lookup"><span data-stu-id="b505e-142">**String, Max Length 32**</span></span>

<span data-ttu-id="b505e-143">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="b505e-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="b505e-144">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="b505e-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="b505e-145">**文字列、最大長 128**</span><span class="sxs-lookup"><span data-stu-id="b505e-145">**String, Max Length 128**</span></span>

<span data-ttu-id="b505e-146">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="b505e-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="b505e-147">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value</span><span class="sxs-lookup"><span data-stu-id="b505e-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="b505e-148">**文字列、最大長 512**</span><span class="sxs-lookup"><span data-stu-id="b505e-148">**String, Max Length 512**</span></span>

<span data-ttu-id="b505e-149">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="b505e-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="b505e-150">composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="b505e-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="b505e-151">**文字列、最大長 128**</span><span class="sxs-lookup"><span data-stu-id="b505e-151">**String, Max Length 128**</span></span>

<span data-ttu-id="b505e-152">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="b505e-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="b505e-153">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title</span><span class="sxs-lookup"><span data-stu-id="b505e-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="b505e-154">**文字列、最大長 64**</span><span class="sxs-lookup"><span data-stu-id="b505e-154">**String, Max Length 64**</span></span>

<span data-ttu-id="b505e-155">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="b505e-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>
