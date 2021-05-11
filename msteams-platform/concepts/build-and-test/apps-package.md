---
title: アプリをパッケージ化する
description: テスト、アップロード、およびストア発行Microsoft Teamsアプリをパッケージ化する方法について学習します。
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: e477539a9b8eaa0c869a2070fcd20b74aecfe490
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101703"
---
# <a name="create-a-microsoft-teams-app-package"></a><span data-ttu-id="1a534-103">アプリ パッケージMicrosoft Teams作成する</span><span class="sxs-lookup"><span data-stu-id="1a534-103">Create a Microsoft Teams app package</span></span>

<span data-ttu-id="1a534-104">ただし、アプリ パッケージは必要ですが、アプリパッケージを配布Microsoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="1a534-104">You need an app package however you plan to distribute your Microsoft Teams app.</span></span> <span data-ttu-id="1a534-105">有効なパッケージは、次を含む ZIP ファイルです。</span><span class="sxs-lookup"><span data-stu-id="1a534-105">A valid package is a ZIP file that contains the following:</span></span>

* <span data-ttu-id="1a534-106">**アプリ マニフェスト**: アプリの機能、必要なリソース、その他の重要な属性など、アプリの構成方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1a534-106">**App manifest**: Describes how your app is configured, including its capabilities, required resources, and other important attributes.</span></span>
* <span data-ttu-id="1a534-107">**アプリアイコン**: 各パッケージには、アプリの色とアウトラインアイコンが必要です。</span><span class="sxs-lookup"><span data-stu-id="1a534-107">**App icons**: Each package requires a color and outline icon for your app.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="1a534-108">アプリ マニフェスト</span><span class="sxs-lookup"><span data-stu-id="1a534-108">App manifest</span></span>

<span data-ttu-id="1a534-109">アプリ マニフェスト ファイルは、パッケージのトップ レベルに名前が付けられている必要があります `manifest.json` 。</span><span class="sxs-lookup"><span data-stu-id="1a534-109">Your app manifest file must be at the top level of the package with the name `manifest.json`.</span></span> 

<span data-ttu-id="1a534-110">ストアに発行するTeams、マニフェストが最新のスキーマを[参照してください。](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="1a534-110">When publishing to the Teams store, make sure your manifest references the latest [schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="app-icons"></a><span data-ttu-id="1a534-111">アプリのアイコン</span><span class="sxs-lookup"><span data-stu-id="1a534-111">App icons</span></span>

<span data-ttu-id="1a534-112">アプリ パッケージには、2 つの PNG バージョンのアプリ アイコン (色とアウトライン バージョン) が含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a534-112">Your app package must include two PNG versions of your app icon: A color and outline version.</span></span>

> [!Note]
> <span data-ttu-id="1a534-113">アプリにボットまたはメッセージング拡張機能がある場合は、ボット サービスの登録にアイコンMicrosoft Azure含まれます。</span><span class="sxs-lookup"><span data-stu-id="1a534-113">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

<span data-ttu-id="1a534-114">アプリがストア レビューに合格Teams、これらのアイコンは次のサイズ要件を満たしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a534-114">For your app to pass Teams store review, these icons must meet the following size requirements.</span></span>

### <a name="color-icon"></a><span data-ttu-id="1a534-115">色アイコン</span><span class="sxs-lookup"><span data-stu-id="1a534-115">Color icon</span></span>

<span data-ttu-id="1a534-116">アイコンの色バージョンは、ほとんどのシナリオで表示Teams 192x192 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a534-116">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="1a534-117">アイコン 記号 (96x96 ピクセル) は任意の色を指定できますが、単色または完全に透明な四角形の背景に位置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a534-117">Your icon symbol (96x96 pixels) can be any color, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="1a534-118">Teamsアイコンが自動的にトリミングされ、複数のシナリオで角が丸く、ボットのシナリオでは六角形が表示されます。</span><span class="sxs-lookup"><span data-stu-id="1a534-118">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="1a534-119">詳細を失わずにシンボルをトリミングするには、シンボルの周囲に 48 ピクセルのパディングを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a534-119">To crop the symbol without losing any detail, include 48 pixels of padding around your symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teamsアイコンとデザインガイダンスを参照してください。" border="false":::

### <a name="outline-icon"></a><span data-ttu-id="1a534-121">アウトライン アイコン</span><span class="sxs-lookup"><span data-stu-id="1a534-121">Outline icon</span></span>

<span data-ttu-id="1a534-122">アウトライン アイコンは、次の 2 つのシナリオで表示されます。</span><span class="sxs-lookup"><span data-stu-id="1a534-122">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="1a534-123">アプリが使用されている場合は、アプリの左側にあるアプリ バーに "起Teams。</span><span class="sxs-lookup"><span data-stu-id="1a534-123">When your app is in use and “hoisted” on the app bar on the left side of Teams.</span></span>
* <span data-ttu-id="1a534-124">ユーザーがアプリのメッセージング拡張機能をピンで固定する場合。</span><span class="sxs-lookup"><span data-stu-id="1a534-124">When a user pins your app's messaging extension.</span></span>

<span data-ttu-id="1a534-125">アイコンは 32x32 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a534-125">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="1a534-126">透明な背景を持つ白、または白い背景を持つ透明な色を指定できます (他の色は使用できません)。</span><span class="sxs-lookup"><span data-stu-id="1a534-126">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="1a534-127">アウトライン アイコンには、シンボルの周囲に余分なパディングを配置する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="1a534-127">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teamsアイコンの設計ガイダンスを参照してください。" border="false":::

### <a name="best-practices"></a><span data-ttu-id="1a534-129">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="1a534-129">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="アプリ アイコンを設計する方法を示す図。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="1a534-131">Do: 正確なアウトライン アイコンのガイドラインに従います</span><span class="sxs-lookup"><span data-stu-id="1a534-131">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="1a534-132">アイコンで使用する白の RGB 値は、赤: 255、緑: 255、青: 255 である必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a534-132">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="1a534-133">アウトライン アイコンの他のすべての部分は完全に透明で、アルファ チャネルは 0 に設定されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a534-133">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="アプリ アイコンをデザインしない方法を示す図。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="1a534-135">[しない]: 円形または丸い四角形でトリミングする</span><span class="sxs-lookup"><span data-stu-id="1a534-135">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="1a534-136">アプリ パッケージで送信される色アイコンは正方形である必要があります。</span><span class="sxs-lookup"><span data-stu-id="1a534-136">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="1a534-137">アイコンの角を丸めない。</span><span class="sxs-lookup"><span data-stu-id="1a534-137">Don’t round the corners of your icon.</span></span> <span data-ttu-id="1a534-138">Teamsコーナーの半径を自動的に調整します。</span><span class="sxs-lookup"><span data-stu-id="1a534-138">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a><span data-ttu-id="1a534-139">[しない]: 他のブランドをコピーする</span><span class="sxs-lookup"><span data-stu-id="1a534-139">Don't: Copy other brands</span></span>

<span data-ttu-id="1a534-140">アイコンは、自分が所有していない著作権で保護された製品 (Microsoft 製品やブランドに似たデザインなど) を模倣しなけってはいけない。</span><span class="sxs-lookup"><span data-stu-id="1a534-140">Your icons must not mimic any copyrighted products that you don't own (for example, a design similar to a Microsoft product or brand).</span></span>

### <a name="examples"></a><span data-ttu-id="1a534-141">例</span><span class="sxs-lookup"><span data-stu-id="1a534-141">Examples</span></span>

<span data-ttu-id="1a534-142">さまざまな機能とコンテキストでアプリ アイコンTeams次に示します。</span><span class="sxs-lookup"><span data-stu-id="1a534-142">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="1a534-143">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="1a534-143">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="個人用アプリでアプリ アイコンがどのように表示されるのか示す例。" border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="1a534-145">ボット (チャネル)</span><span class="sxs-lookup"><span data-stu-id="1a534-145">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="チャネル内のボットでアプリ アイコンがどのように表示されるのか示す例。" border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="1a534-147">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="1a534-147">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<代替テキスト>" border="false":::

## <a name="next-step"></a><span data-ttu-id="1a534-149">次の手順</span><span class="sxs-lookup"><span data-stu-id="1a534-149">Next step</span></span>

<span data-ttu-id="1a534-150">アプリの配布方法を選択します。</span><span class="sxs-lookup"><span data-stu-id="1a534-150">Choose how you plan to distribute your app:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1a534-151">アプリをサイドロードTeams</span><span class="sxs-lookup"><span data-stu-id="1a534-151">Sideload your app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="1a534-152">組織にアプリを発行する</span><span class="sxs-lookup"><span data-stu-id="1a534-152">Publish your app to your org</span></span>](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [<span data-ttu-id="1a534-153">アプリをストアに発行する</span><span class="sxs-lookup"><span data-stu-id="1a534-153">Publish your app to the store</span></span>](~/concepts/deploy-and-publish/appsource/publish.md)
