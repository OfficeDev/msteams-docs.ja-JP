---
title: JSON スキーマ参照のローカライズ
description: ローカライズ ファイルでサポートされているローカライズ スキーマについて説明Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: teams マニフェスト スキーマのローカライズ
ms.date: 05/20/2019
ms.openlocfilehash: 6e8f666cc6bfa693d7f2f469fc58fd6ee4860a80
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140514"
---
# <a name="localize-json-schema-reference"></a><span data-ttu-id="45655-104">JSON スキーマ参照のローカライズ</span><span class="sxs-lookup"><span data-stu-id="45655-104">Localize JSON schema reference</span></span>

<span data-ttu-id="45655-105">ローカライズ Microsoft Teamsは、クライアント言語の設定に基づいて提供される言語の翻訳について説明します。</span><span class="sxs-lookup"><span data-stu-id="45655-105">The Microsoft Teams localization file describes language translations that are served based on the client language settings.</span></span> <span data-ttu-id="45655-106">ファイルは、 でホストされるスキーマに準拠している必要があります [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json) 。</span><span class="sxs-lookup"><span data-stu-id="45655-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json).</span></span> 

> [!TIP]
> <span data-ttu-id="45655-107">マニフェストの先頭にスキーマを指定して、コード エディターからのサポートを有効にするか、同様 `IntelliSense` のサポートを行います。 `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="45655-107">Specify the schema at the beginning of your manifest to enable `IntelliSense` or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",`</span></span>

## <a name="example"></a><span data-ttu-id="45655-108">例</span><span class="sxs-lookup"><span data-stu-id="45655-108">Example</span></span> 

<span data-ttu-id="45655-109">ローカライズ JSON スキーマの例は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="45655-109">Example of localization JSON schema is as follows:</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

<span data-ttu-id="45655-110">スキーマは、次のプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="45655-110">The schema defines the following properties:</span></span>

|<span data-ttu-id="45655-111">プロパティ</span><span class="sxs-lookup"><span data-stu-id="45655-111">Property</span></span>|<span data-ttu-id="45655-112">型</span><span class="sxs-lookup"><span data-stu-id="45655-112">Type</span></span>|<span data-ttu-id="45655-113">最大の長さ</span><span class="sxs-lookup"><span data-stu-id="45655-113">Maximum length</span></span>|<span data-ttu-id="45655-114">説明</span><span class="sxs-lookup"><span data-stu-id="45655-114">Description</span></span>|
|---------------|--------|---------|------------------|
|`$schema`|<span data-ttu-id="45655-115">URI</span><span class="sxs-lookup"><span data-stu-id="45655-115">URI</span></span>|<span data-ttu-id="45655-116">該当なし</span><span class="sxs-lookup"><span data-stu-id="45655-116">NA</span></span>|<span data-ttu-id="45655-117">マニフェスト https:// JSON スキーマを参照する URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="45655-117">The https:// URL referencing the JSON Schema for the manifest.</span></span>|
|`name.short`|<span data-ttu-id="45655-118">String</span><span class="sxs-lookup"><span data-stu-id="45655-118">String</span></span>|<span data-ttu-id="45655-119">30</span><span class="sxs-lookup"><span data-stu-id="45655-119">30</span></span>|<span data-ttu-id="45655-120">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。</span><span class="sxs-lookup"><span data-stu-id="45655-120">Replaces the corresponding string from the app manifest with the value provided here.</span></span>|
|`name.full`|<span data-ttu-id="45655-121">文字列</span><span class="sxs-lookup"><span data-stu-id="45655-121">String</span></span>|<span data-ttu-id="45655-122">100</span><span class="sxs-lookup"><span data-stu-id="45655-122">100</span></span>|<span data-ttu-id="45655-123">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。</span><span class="sxs-lookup"><span data-stu-id="45655-123">Replaces the corresponding string from the app manifest with the value provided here.</span></span>|
|`description.short`|<span data-ttu-id="45655-124">String</span><span class="sxs-lookup"><span data-stu-id="45655-124">String</span></span>|<span data-ttu-id="45655-125">80</span><span class="sxs-lookup"><span data-stu-id="45655-125">80</span></span>|<span data-ttu-id="45655-126">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。</span><span class="sxs-lookup"><span data-stu-id="45655-126">Replaces the corresponding string from the app manifest with the value provided here.</span></span>|
|`description.full`|<span data-ttu-id="45655-127">String</span><span class="sxs-lookup"><span data-stu-id="45655-127">String</span></span>|<span data-ttu-id="45655-128">4000</span><span class="sxs-lookup"><span data-stu-id="45655-128">4000</span></span>|<span data-ttu-id="45655-129">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。</span><span class="sxs-lookup"><span data-stu-id="45655-129">Replaces the corresponding string from the app manifest with the value provided here.</span></span>|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|<span data-ttu-id="45655-130">String</span><span class="sxs-lookup"><span data-stu-id="45655-130">String</span></span>|<span data-ttu-id="45655-131">128</span><span class="sxs-lookup"><span data-stu-id="45655-131">128</span></span>|<span data-ttu-id="45655-132">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="45655-132">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|<span data-ttu-id="45655-133">String</span><span class="sxs-lookup"><span data-stu-id="45655-133">String</span></span>|<span data-ttu-id="45655-134">32</span><span class="sxs-lookup"><span data-stu-id="45655-134">32</span></span>|<span data-ttu-id="45655-135">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="45655-135">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`## bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|<span data-ttu-id="45655-136">String</span><span class="sxs-lookup"><span data-stu-id="45655-136">String</span></span>|<span data-ttu-id="45655-137">128</span><span class="sxs-lookup"><span data-stu-id="45655-137">128</span></span>|<span data-ttu-id="45655-138">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="45655-138">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|<span data-ttu-id="45655-139">String</span><span class="sxs-lookup"><span data-stu-id="45655-139">String</span></span>|<span data-ttu-id="45655-140">32</span><span class="sxs-lookup"><span data-stu-id="45655-140">32</span></span>|<span data-ttu-id="45655-141">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="45655-141">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|<span data-ttu-id="45655-142">String</span><span class="sxs-lookup"><span data-stu-id="45655-142">String</span></span>|<span data-ttu-id="45655-143">128</span><span class="sxs-lookup"><span data-stu-id="45655-143">128</span></span>|<span data-ttu-id="45655-144">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="45655-144">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|<span data-ttu-id="45655-145">String</span><span class="sxs-lookup"><span data-stu-id="45655-145">String</span></span>|<span data-ttu-id="45655-146">32</span><span class="sxs-lookup"><span data-stu-id="45655-146">32</span></span>|<span data-ttu-id="45655-147">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。</span><span class="sxs-lookup"><span data-stu-id="45655-147">Replaces the corresponding string from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|<span data-ttu-id="45655-148">String</span><span class="sxs-lookup"><span data-stu-id="45655-148">String</span></span>|<span data-ttu-id="45655-149">128</span><span class="sxs-lookup"><span data-stu-id="45655-149">128</span></span>|<span data-ttu-id="45655-150">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="45655-150">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|<span data-ttu-id="45655-151">String</span><span class="sxs-lookup"><span data-stu-id="45655-151">String</span></span>|<span data-ttu-id="45655-152">512</span><span class="sxs-lookup"><span data-stu-id="45655-152">512</span></span>|<span data-ttu-id="45655-153">アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。</span><span class="sxs-lookup"><span data-stu-id="45655-153">Replaces the corresponding string from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|<span data-ttu-id="45655-154">String</span><span class="sxs-lookup"><span data-stu-id="45655-154">String</span></span>|<span data-ttu-id="45655-155">128</span><span class="sxs-lookup"><span data-stu-id="45655-155">128</span></span>|<span data-ttu-id="45655-156">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="45655-156">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|<span data-ttu-id="45655-157">String</span><span class="sxs-lookup"><span data-stu-id="45655-157">String</span></span>|<span data-ttu-id="45655-158">64</span><span class="sxs-lookup"><span data-stu-id="45655-158">64</span></span>|<span data-ttu-id="45655-159">アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="45655-159">Replaces the corresponding strings from the app manifest with the value provided here.</span></span>|

## <a name="see-also"></a><span data-ttu-id="45655-160">関連項目</span><span class="sxs-lookup"><span data-stu-id="45655-160">See also</span></span>

> [<span data-ttu-id="45655-161">アプリをローカライズする</span><span class="sxs-lookup"><span data-stu-id="45655-161">Localize your app</span></span>](~/concepts/build-and-test/apps-localization.md)
