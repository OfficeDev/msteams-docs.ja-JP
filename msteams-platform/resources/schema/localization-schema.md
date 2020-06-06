---
title: ローカリゼーションファイル JSON スキーマリファレンス
description: Microsoft Teams のローカリゼーションファイルでサポートされているローカライズスキーマについて説明します。
keywords: teams マニフェストスキーマのローカライズ
ms.date: 05/20/2019
ms.openlocfilehash: 14e08c582f065d1b09ff0f4906ca6788037460f1
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "44590866"
---
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="6d67b-104">リファレンス: ローカライズファイル JSON スキーマ</span><span class="sxs-lookup"><span data-stu-id="6d67b-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="6d67b-105">Microsoft Teams のローカリゼーションファイルでは、クライアントの言語設定に基づいて提供される言語の翻訳について説明します。</span><span class="sxs-lookup"><span data-stu-id="6d67b-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="6d67b-106">ファイルは、でホストされているスキーマに準拠している必要があり [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) ます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="6d67b-107">詳細については、「[アプリのローカライズ](~/concepts/build-and-test/apps-localization.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6d67b-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="6d67b-108">サンプル</span><span class="sxs-lookup"><span data-stu-id="6d67b-108">Sample</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

<span data-ttu-id="6d67b-109">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="6d67b-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="6d67b-110">$schema</span><span class="sxs-lookup"><span data-stu-id="6d67b-110">$schema</span></span>

<span data-ttu-id="6d67b-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="6d67b-111">**URI**</span></span>

<span data-ttu-id="6d67b-112">マニフェストの JSON スキーマを参照する https://URL。</span><span class="sxs-lookup"><span data-stu-id="6d67b-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="6d67b-113">マニフェストの最初にスキーマを指定して、コードエディターで IntelliSense または同様のサポートを有効にします。`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="6d67b-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="6d67b-114">名前。 short</span><span class="sxs-lookup"><span data-stu-id="6d67b-114">name.short</span></span>

<span data-ttu-id="6d67b-115">**文字列、最大長30**</span><span class="sxs-lookup"><span data-stu-id="6d67b-115">**String, Max Length 30**</span></span>

<span data-ttu-id="6d67b-116">アプリマニフェストの対応する文字列を、ここで指定した値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="6d67b-117">名前。完全</span><span class="sxs-lookup"><span data-stu-id="6d67b-117">name.full</span></span>

<span data-ttu-id="6d67b-118">**文字列、最大長100**</span><span class="sxs-lookup"><span data-stu-id="6d67b-118">**String, Max Length 100**</span></span>

<span data-ttu-id="6d67b-119">アプリマニフェストの対応する文字列を、ここで指定した値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="6d67b-120">説明。 short</span><span class="sxs-lookup"><span data-stu-id="6d67b-120">description.short</span></span>

<span data-ttu-id="6d67b-121">**文字列、最大長80**</span><span class="sxs-lookup"><span data-stu-id="6d67b-121">**String, Max Length 80**</span></span>

<span data-ttu-id="6d67b-122">アプリマニフェストの対応する文字列を、ここで指定した値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="6d67b-123">詳細</span><span class="sxs-lookup"><span data-stu-id="6d67b-123">description.full</span></span>

<span data-ttu-id="6d67b-124">**文字列、最大長4000**</span><span class="sxs-lookup"><span data-stu-id="6d67b-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="6d67b-125">アプリマニフェストの対応する文字列を、ここで指定した値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="6d67b-126">staticTabs \\ [([0-9] | 1 [0-5]) \\ ] \\ . 名前</span><span class="sxs-lookup"><span data-stu-id="6d67b-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="6d67b-127">**文字列、最大長128**</span><span class="sxs-lookup"><span data-stu-id="6d67b-127">**String, Max Length 128**</span></span>

<span data-ttu-id="6d67b-128">対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="6d67b-129">bot \\ [0 \\ ] \\ commandlists \\ [[0-2]] \\ \\ . コマンド \\ [[0-9] \\ \\ ]. title</span><span class="sxs-lookup"><span data-stu-id="6d67b-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="6d67b-130">**文字列、最大長32**</span><span class="sxs-lookup"><span data-stu-id="6d67b-130">**String, Max Length 32**</span></span>

<span data-ttu-id="6d67b-131">対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="6d67b-132">bot \\ [0 \\ ] \\ commandlists \\ [[0-2]] \\ \\ . コマンド \\ [[0-9] \\ \\ ]. 説明</span><span class="sxs-lookup"><span data-stu-id="6d67b-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="6d67b-133">**文字列、最大長128**</span><span class="sxs-lookup"><span data-stu-id="6d67b-133">**String, Max Length 128**</span></span>

<span data-ttu-id="6d67b-134">対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="6d67b-135">この機能 \\ [0 \\ ] \\ コマンド \\ [[0-9] \\ ] \\ . タイトル</span><span class="sxs-lookup"><span data-stu-id="6d67b-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="6d67b-136">**文字列、最大長32**</span><span class="sxs-lookup"><span data-stu-id="6d67b-136">**String, Max Length 32**</span></span>

<span data-ttu-id="6d67b-137">対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="6d67b-138">この機能 \\ [0 \\ ] \\ コマンド \\ [[0-9] \\ ] \\ . 説明</span><span class="sxs-lookup"><span data-stu-id="6d67b-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="6d67b-139">**文字列、最大長128**</span><span class="sxs-lookup"><span data-stu-id="6d67b-139">**String, Max Length 128**</span></span>

<span data-ttu-id="6d67b-140">対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="6d67b-141">スキーマの [ \\ 0 \\ ] \\ コマンド \\ [[0-9]]. \\ \\ パラメーター \\ [[0-4] \\ ] \\ . タイトル</span><span class="sxs-lookup"><span data-stu-id="6d67b-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="6d67b-142">**文字列、最大長32**</span><span class="sxs-lookup"><span data-stu-id="6d67b-142">**String, Max Length 32**</span></span>

<span data-ttu-id="6d67b-143">対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="6d67b-144">この機能 [ \\ 0 \\ ] \\ コマンド \\ [[0-9]]. \\ \\ パラメーター \\ [[0-4] \\ ] \\ . 説明</span><span class="sxs-lookup"><span data-stu-id="6d67b-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="6d67b-145">**文字列、最大長128**</span><span class="sxs-lookup"><span data-stu-id="6d67b-145">**String, Max Length 128**</span></span>

<span data-ttu-id="6d67b-146">対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="6d67b-147">この機能 [ \\ 0 \\ ] \\ コマンド \\ [[0-9]]. \\ \\ パラメーター \\ [[0-4]] \\ \\ . 値</span><span class="sxs-lookup"><span data-stu-id="6d67b-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="6d67b-148">**文字列、最大長512**</span><span class="sxs-lookup"><span data-stu-id="6d67b-148">**String, Max Length 512**</span></span>

<span data-ttu-id="6d67b-149">対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="6d67b-150">\\色の設定 [0 \\ ] \\ コマンド \\ [[0-9]]. \\ \\ パラメーター [[ \\ 0-4] \\ ]. \\ 選択肢 \\ [[0-9] \\ ] \\ . タイトル</span><span class="sxs-lookup"><span data-stu-id="6d67b-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="6d67b-151">**文字列、最大長128**</span><span class="sxs-lookup"><span data-stu-id="6d67b-151">**String, Max Length 128**</span></span>

<span data-ttu-id="6d67b-152">対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="6d67b-153">オブジェクトの \\ [0 \\ ] \\ . コマンド \\ [[0-9] \\ ] \\ \\ .</span><span class="sxs-lookup"><span data-stu-id="6d67b-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="6d67b-154">**文字列、最大長64**</span><span class="sxs-lookup"><span data-stu-id="6d67b-154">**String, Max Length 64**</span></span>

<span data-ttu-id="6d67b-155">対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="6d67b-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>