---
title: ローカライズ ファイルの JSON スキーマ リファレンス
description: Microsoft Teams のローカライズ ファイルでサポートされているローカライズ スキーマについて説明します。
ms.topic: reference
keywords: teams マニフェスト スキーマのローカライズ
ms.date: 05/20/2019
ms.openlocfilehash: 696a65de70a63e767f8fcdb040364fe90cde8716
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014601"
---
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="48af2-104">リファレンス: ローカライズ ファイルの JSON スキーマ</span><span class="sxs-lookup"><span data-stu-id="48af2-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="48af2-105">Microsoft Teams ローカライズ ファイルには、クライアントの言語設定に基づいて提供される言語翻訳が記述されています。</span><span class="sxs-lookup"><span data-stu-id="48af2-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="48af2-106">ファイルは、ホストされているスキーマに準拠している必要があります [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="48af2-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="48af2-107">詳しくは、アプリのローカライズ [に関するページをご覧ください](~/concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="48af2-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="48af2-108">サンプル</span><span class="sxs-lookup"><span data-stu-id="48af2-108">Sample</span></span>

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

<span data-ttu-id="48af2-109">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="48af2-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="48af2-110">$schema</span><span class="sxs-lookup"><span data-stu-id="48af2-110">$schema</span></span>

<span data-ttu-id="48af2-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="48af2-111">**URI**</span></span>

<span data-ttu-id="48af2-112">次https://マニフェストの JSON スキーマを参照する URL を示します。</span><span class="sxs-lookup"><span data-stu-id="48af2-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="48af2-113">マニフェストの先頭にスキーマを指定して、コード エディター IntelliSense同様のサポートを有効にしてください。 `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="48af2-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="48af2-114">name.short</span><span class="sxs-lookup"><span data-stu-id="48af2-114">name.short</span></span>

<span data-ttu-id="48af2-115">**String、Max Length 30**</span><span class="sxs-lookup"><span data-stu-id="48af2-115">**String, Max Length 30**</span></span>

<span data-ttu-id="48af2-116">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="48af2-117">name.full</span><span class="sxs-lookup"><span data-stu-id="48af2-117">name.full</span></span>

<span data-ttu-id="48af2-118">**文字列、最大長 100**</span><span class="sxs-lookup"><span data-stu-id="48af2-118">**String, Max Length 100**</span></span>

<span data-ttu-id="48af2-119">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="48af2-120">description.short</span><span class="sxs-lookup"><span data-stu-id="48af2-120">description.short</span></span>

<span data-ttu-id="48af2-121">**文字列、最大長 80**</span><span class="sxs-lookup"><span data-stu-id="48af2-121">**String, Max Length 80**</span></span>

<span data-ttu-id="48af2-122">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="48af2-123">description.full</span><span class="sxs-lookup"><span data-stu-id="48af2-123">description.full</span></span>

<span data-ttu-id="48af2-124">**String、Max Length 4000**</span><span class="sxs-lookup"><span data-stu-id="48af2-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="48af2-125">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="48af2-126">staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name</span><span class="sxs-lookup"><span data-stu-id="48af2-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="48af2-127">**文字列、最大長 128**</span><span class="sxs-lookup"><span data-stu-id="48af2-127">**String, Max Length 128**</span></span>

<span data-ttu-id="48af2-128">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="48af2-129">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ \\ .title</span><span class="sxs-lookup"><span data-stu-id="48af2-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="48af2-130">**文字列、最大長 32**</span><span class="sxs-lookup"><span data-stu-id="48af2-130">**String, Max Length 32**</span></span>

<span data-ttu-id="48af2-131">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="48af2-132">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ \\ .description</span><span class="sxs-lookup"><span data-stu-id="48af2-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="48af2-133">**文字列、最大長 128**</span><span class="sxs-lookup"><span data-stu-id="48af2-133">**String, Max Length 128**</span></span>

<span data-ttu-id="48af2-134">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="48af2-135">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ \\ .title</span><span class="sxs-lookup"><span data-stu-id="48af2-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="48af2-136">**文字列、最大長 32**</span><span class="sxs-lookup"><span data-stu-id="48af2-136">**String, Max Length 32**</span></span>

<span data-ttu-id="48af2-137">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="48af2-138">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="48af2-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="48af2-139">**文字列、最大長 128**</span><span class="sxs-lookup"><span data-stu-id="48af2-139">**String, Max Length 128**</span></span>

<span data-ttu-id="48af2-140">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="48af2-141">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ \\ .title</span><span class="sxs-lookup"><span data-stu-id="48af2-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="48af2-142">**文字列、最大長 32**</span><span class="sxs-lookup"><span data-stu-id="48af2-142">**String, Max Length 32**</span></span>

<span data-ttu-id="48af2-143">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="48af2-144">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ . \\ description</span><span class="sxs-lookup"><span data-stu-id="48af2-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="48af2-145">**文字列、最大長 128**</span><span class="sxs-lookup"><span data-stu-id="48af2-145">**String, Max Length 128**</span></span>

<span data-ttu-id="48af2-146">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="48af2-147">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value</span><span class="sxs-lookup"><span data-stu-id="48af2-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="48af2-148">**文字列、最大長 512**</span><span class="sxs-lookup"><span data-stu-id="48af2-148">**String, Max Length 512**</span></span>

<span data-ttu-id="48af2-149">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="48af2-150">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ \\ .title</span><span class="sxs-lookup"><span data-stu-id="48af2-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="48af2-151">**文字列、最大長 128**</span><span class="sxs-lookup"><span data-stu-id="48af2-151">**String, Max Length 128**</span></span>

<span data-ttu-id="48af2-152">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="48af2-153">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title</span><span class="sxs-lookup"><span data-stu-id="48af2-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="48af2-154">**文字列、最大長 64**</span><span class="sxs-lookup"><span data-stu-id="48af2-154">**String, Max Length 64**</span></span>

<span data-ttu-id="48af2-155">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。</span><span class="sxs-lookup"><span data-stu-id="48af2-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>
