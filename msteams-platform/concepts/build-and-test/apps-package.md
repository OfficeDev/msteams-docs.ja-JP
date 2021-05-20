---
title: アプリをパッケージ化する
description: テスト、アップロード、ストア発行用にMicrosoft Teams アプリをパッケージ化する方法について説明します。
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 219e2d5341707ed51b7e0a3a8077f93df9eac640
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565215"
---
# <a name="create-a-microsoft-teams-app-package"></a><span data-ttu-id="08296-103">Microsoft Teams アプリ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="08296-103">Create a Microsoft Teams app package</span></span>

<span data-ttu-id="08296-104">Microsoft Teams アプリを配布する予定のアプリ パッケージが必要です。</span><span class="sxs-lookup"><span data-stu-id="08296-104">You need an app package however you plan to distribute your Microsoft Teams app.</span></span> <span data-ttu-id="08296-105">有効なパッケージは、次の内容を含む ZIP ファイルです。</span><span class="sxs-lookup"><span data-stu-id="08296-105">A valid package is a ZIP file that contains the following:</span></span>

* <span data-ttu-id="08296-106">**アプリ マニフェスト**: アプリの機能、必要なリソース、その他の重要な属性など、アプリの構成方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="08296-106">**App manifest**: Describes how your app is configured, including its capabilities, required resources, and other important attributes.</span></span>
* <span data-ttu-id="08296-107">**アプリアイコン**: 各パッケージには、アプリの色とアウトラインアイコンが必要です。</span><span class="sxs-lookup"><span data-stu-id="08296-107">**App icons**: Each package requires a color and outline icon for your app.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="08296-108">アプリ マニフェスト</span><span class="sxs-lookup"><span data-stu-id="08296-108">App manifest</span></span>

<span data-ttu-id="08296-109">アプリ マニフェスト ファイルは、パッケージの最上位レベルにという名前を付ける必要があります `manifest.json` 。</span><span class="sxs-lookup"><span data-stu-id="08296-109">Your app manifest file must be at the top level of the package with the name `manifest.json`.</span></span> 

<span data-ttu-id="08296-110">Teams ストアに発行する場合は、マニフェストが最新[のスキーマ](~/resources/schema/manifest-schema.md)を参照していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="08296-110">When publishing to the Teams store, make sure your manifest references the latest [schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="app-icons"></a><span data-ttu-id="08296-111">アプリアイコン</span><span class="sxs-lookup"><span data-stu-id="08296-111">App icons</span></span>

<span data-ttu-id="08296-112">アプリ パッケージには、アプリ アイコンの 2 つの PNG バージョン (色とアウトライン バージョン) を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="08296-112">Your app package must include two PNG versions of your app icon: A color and outline version.</span></span>

> [!Note]
> <span data-ttu-id="08296-113">アプリにボットまたはメッセージング拡張機能がある場合、アイコンもMicrosoft Azure Bot サービス登録に含まれます。</span><span class="sxs-lookup"><span data-stu-id="08296-113">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

<span data-ttu-id="08296-114">アプリがストアレビュー Teams渡すためには、これらのアイコンが次のサイズ要件を満たしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="08296-114">For your app to pass Teams store review, these icons must meet the following size requirements.</span></span>

### <a name="color-icon"></a><span data-ttu-id="08296-115">カラーアイコン</span><span class="sxs-lookup"><span data-stu-id="08296-115">Color icon</span></span>

<span data-ttu-id="08296-116">アイコンの色バージョンは、ほとんどのTeamsシナリオで表示され、192x192 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="08296-116">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="08296-117">アイコンシンボル(96x96 ピクセル)は任意の色にできますが、塗りつぶされた四角形または完全に透明な四角形の背景に置く必要があります。</span><span class="sxs-lookup"><span data-stu-id="08296-117">Your icon symbol (96x96 pixels) can be any color, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="08296-118">Teamsは自動的にアイコンをトリミングして、複数のシナリオで角丸い四角形、ボットシナリオでは六角形の形状を表示します。</span><span class="sxs-lookup"><span data-stu-id="08296-118">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="08296-119">詳細を失うことなくシンボルをトリミングするには、シンボルの周囲に 48 ピクセルのパディングを含めます。</span><span class="sxs-lookup"><span data-stu-id="08296-119">To crop the symbol without losing any detail, include 48 pixels of padding around your symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="色のアイコンとデザイン ガイダンスをTeamsします。" border="false":::

### <a name="outline-icon"></a><span data-ttu-id="08296-121">アウトライン アイコン</span><span class="sxs-lookup"><span data-stu-id="08296-121">Outline icon</span></span>

<span data-ttu-id="08296-122">アウトライン アイコンは、次の 2 つのシナリオで表示されます。</span><span class="sxs-lookup"><span data-stu-id="08296-122">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="08296-123">アプリが使用中で、Teamsの左側のアプリ バーで "買い上げ" を行った場合。</span><span class="sxs-lookup"><span data-stu-id="08296-123">When your app is in use and “hoisted” on the app bar on the left side of Teams.</span></span>
* <span data-ttu-id="08296-124">ユーザーがアプリのメッセージング拡張機能をピンで固定する場合。</span><span class="sxs-lookup"><span data-stu-id="08296-124">When a user pins your app's messaging extension.</span></span>

<span data-ttu-id="08296-125">アイコンは 32x32 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="08296-125">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="08296-126">透明な背景を持つ白、または白い背景を持つ透明にすることができます(他の色は許可されません)。</span><span class="sxs-lookup"><span data-stu-id="08296-126">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="08296-127">アウトライン アイコンには、記号の周囲に余分なパディングを付けないでください。</span><span class="sxs-lookup"><span data-stu-id="08296-127">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teamsアウトライン アイコンのデザイン ガイダンスです。" border="false":::

### <a name="best-practices"></a><span data-ttu-id="08296-129">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="08296-129">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="アプリ アイコンのデザイン方法を示す図。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="08296-131">行う: アウトライン アイコンのガイドラインに従う</span><span class="sxs-lookup"><span data-stu-id="08296-131">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="08296-132">アイコンで使用する白の RGB 値は、赤:255、緑:255、青:255 でなければなりません。</span><span class="sxs-lookup"><span data-stu-id="08296-132">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="08296-133">アウトライン アイコンの他のすべての部分は、アルファ チャネルが 0 に設定された完全に透明である必要があります。</span><span class="sxs-lookup"><span data-stu-id="08296-133">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="アプリ アイコンをデザインしない方法を示す図。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="08296-135">しない: 円形または丸い正方形の形でトリミング</span><span class="sxs-lookup"><span data-stu-id="08296-135">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="08296-136">アプリ パッケージに提出される色アイコンは、正方形である必要があります。</span><span class="sxs-lookup"><span data-stu-id="08296-136">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="08296-137">アイコンの角を丸めないでください。</span><span class="sxs-lookup"><span data-stu-id="08296-137">Don’t round the corners of your icon.</span></span> <span data-ttu-id="08296-138">Teamsは、コーナー半径を自動的に調整します。</span><span class="sxs-lookup"><span data-stu-id="08296-138">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a><span data-ttu-id="08296-139">しない: 他のブランドをコピーする</span><span class="sxs-lookup"><span data-stu-id="08296-139">Don't: Copy other brands</span></span>

<span data-ttu-id="08296-140">アイコンは、所有していない著作権で保護された製品を模倣してはなりません。</span><span class="sxs-lookup"><span data-stu-id="08296-140">Your icons must not mimic any copyrighted products that you don't own.</span></span> <span data-ttu-id="08296-141">たとえば、Microsoft 製品やブランドに似たデザインです。</span><span class="sxs-lookup"><span data-stu-id="08296-141">For example, a design similar to a Microsoft product or brand.</span></span>

### <a name="examples"></a><span data-ttu-id="08296-142">例</span><span class="sxs-lookup"><span data-stu-id="08296-142">Examples</span></span>

<span data-ttu-id="08296-143">さまざまなTeams機能とコンテキストでアプリアイコンがどのように表示されるのかは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="08296-143">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="08296-144">パーソナルアプリ</span><span class="sxs-lookup"><span data-stu-id="08296-144">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="個人用アプリでのアプリ アイコンの外観を示す例。" border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="08296-146">ボット (チャネル)</span><span class="sxs-lookup"><span data-stu-id="08296-146">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="チャネル内のボットでアプリ アイコンがどのように表示されるかを示す例。" border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="08296-148">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="08296-148">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text=" 代替テキスト>を<" border="false":::

## <a name="next-step"></a><span data-ttu-id="08296-150">次の手順</span><span class="sxs-lookup"><span data-stu-id="08296-150">Next step</span></span>

<span data-ttu-id="08296-151">アプリの配布方法を選択します。</span><span class="sxs-lookup"><span data-stu-id="08296-151">Choose how you plan to distribute your app:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="08296-152">Teamsでアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="08296-152">Sideload your app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="08296-153">組織へのアプリの公開</span><span class="sxs-lookup"><span data-stu-id="08296-153">Publish your app to your org</span></span>](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [<span data-ttu-id="08296-154">アプリをストアに公開する</span><span class="sxs-lookup"><span data-stu-id="08296-154">Publish your app to the store</span></span>](~/concepts/deploy-and-publish/appsource/publish.md)
