---
title: アプリをパッケージ化する
description: テスト、アップロード、およびストア発行のために Microsoft Teams アプリをパッケージ化する方法について説明します。
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: c8341f3d83b5e6610e44276d6732affa1d1c1e91
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020141"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="6dea7-103">Microsoft Teams アプリのアプリ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="6dea7-103">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="6dea7-104">Teams のアプリは、アプリ マニフェスト JSON ファイルによって定義され、各アイコンがアプリ パッケージにバンドルされます。</span><span class="sxs-lookup"><span data-stu-id="6dea7-104">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="6dea7-105">アプリを Teams にアップロードしてインストールし、Line of Business アプリ カタログまたは AppSource に発行するには、アプリ パッケージが必要です。</span><span class="sxs-lookup"><span data-stu-id="6dea7-105">You'll need an app package to upload and install your app in Teams and publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="6dea7-106">Teams アプリ パッケージは、次のものを含む .zip ファイルです。</span><span class="sxs-lookup"><span data-stu-id="6dea7-106">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="6dea7-107">アプリの属性を指定し、そのタブ構成ページの場所やボットの Microsoft アプリ ID など、エクスペリエンスに必要なリソースを示すという名前のマニフェスト ファイル `manifest.json` 。</span><span class="sxs-lookup"><span data-stu-id="6dea7-107">A manifest file named `manifest.json`, which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="6dea7-108">[アプリの色とアウトラインのアイコン](#app-icons)です。</span><span class="sxs-lookup"><span data-stu-id="6dea7-108">[Color and outline icons for your app](#app-icons).</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="6dea7-109">マニフェストの作成</span><span class="sxs-lookup"><span data-stu-id="6dea7-109">Creating a manifest</span></span>

<span data-ttu-id="6dea7-110">**Teams App Studio** は、マニフェストを構成する際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="6dea7-110">**Teams App Studio** can help configure your manifest.</span></span> <span data-ttu-id="6dea7-111">React 制御ライブラリとカード用の構成可能なサンプルも含まれています。</span><span class="sxs-lookup"><span data-stu-id="6dea7-111">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="6dea7-112">詳細については [、「App Studio の概要」を参照してください](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6dea7-112">For more information, see [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="6dea7-113">マニフェスト ファイルは、"manifest.json" という名前で、アップロード パッケージの最上位レベルになければなりません。</span><span class="sxs-lookup"><span data-stu-id="6dea7-113">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="6dea7-114">以前に作成されたマニフェストとパッケージは、古いバージョンのスキーマをサポートしている可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6dea7-114">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="6dea7-115">Teams アプリ、特に AppSource (以前の Office ストア) 配信の場合は、最新の[マニフェスト スキーマ](~/resources/schema/manifest-schema.md)を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dea7-115">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="6dea7-116">マニフェストの最初にスキーマを指定して、コード エディターで IntelliSense または同様のサポートを有効にします。</span><span class="sxs-lookup"><span data-stu-id="6dea7-116">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",`
 
## <a name="app-icons"></a><span data-ttu-id="6dea7-117">アプリのアイコン</span><span class="sxs-lookup"><span data-stu-id="6dea7-117">App icons</span></span>

<span data-ttu-id="6dea7-118">アプリ パッケージには、色アイコンとアウトライン アイコンという 2 つの PNG バージョンのアプリ アイコンが含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dea7-118">Your app package must include two PNG versions of your app icon—a color icon and an outline icon.</span></span> <span data-ttu-id="6dea7-119">アプリが AppSource レビューに合格するには、これらのアイコンが次のサイズ要件を満たしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dea7-119">For your app to pass the AppSource review, these icons must meet the following size requirements.</span></span>

> [!Note]
> <span data-ttu-id="6dea7-120">アプリにボットまたはメッセージング拡張機能がある場合は、Microsoft Azure Bot Service 登録にもアイコンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="6dea7-120">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

### <a name="color-icon"></a><span data-ttu-id="6dea7-121">色アイコン</span><span class="sxs-lookup"><span data-stu-id="6dea7-121">Color icon</span></span>

<span data-ttu-id="6dea7-122">アイコンの色バージョンは、ほとんどの Teams シナリオに表示され、192x192 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dea7-122">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="6dea7-123">アイコン 記号 (96x96 ピクセル) は、任意の色または色を指定できますが、単色または完全に透明な四角形の背景に位置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dea7-123">Your icon symbol (96x96 pixels) can be any color or colors, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="6dea7-124">Teams では、アイコンが自動的にトリミングされ、複数のシナリオで角が丸く、ボットのシナリオでは六角形が表示されます。</span><span class="sxs-lookup"><span data-stu-id="6dea7-124">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="6dea7-125">シンボルの周囲に 48 ピクセルのパディングを含めるので、詳細を失わずにこれらのトリミングを行います。</span><span class="sxs-lookup"><span data-stu-id="6dea7-125">Include 48 pixels of padding around your symbol so these crops can be made without losing any detail.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams の色のアイコンとデザインのガイダンス。" border="false":::

### <a name="outline-icon"></a><span data-ttu-id="6dea7-127">アウトライン アイコン</span><span class="sxs-lookup"><span data-stu-id="6dea7-127">Outline icon</span></span>

<span data-ttu-id="6dea7-128">アウトライン アイコンは、次の 2 つのシナリオで表示されます。</span><span class="sxs-lookup"><span data-stu-id="6dea7-128">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="6dea7-129">Teams の左側のアプリ バーでアプリが使用され、"起重" されている場合。</span><span class="sxs-lookup"><span data-stu-id="6dea7-129">When your app is in use and “hoisted” on the app bar on the left of Teams.</span></span>
* <span data-ttu-id="6dea7-130">ユーザーがアプリのメッセージング拡張機能をピンで固定する場合。</span><span class="sxs-lookup"><span data-stu-id="6dea7-130">when a user pins your app's messaging extension.</span></span>

<span data-ttu-id="6dea7-131">アイコンは 32x32 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dea7-131">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="6dea7-132">透明な背景を持つ白、または白い背景を持つ透明な色を指定できます (他の色は使用できません)。</span><span class="sxs-lookup"><span data-stu-id="6dea7-132">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="6dea7-133">アウトライン アイコンには、シンボルの周囲に余分なパディングを配置する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6dea7-133">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams のアウトライン アイコンの設計ガイダンス。" border="false":::

### <a name="best-practices"></a><span data-ttu-id="6dea7-135">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="6dea7-135">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="アプリ アイコンを設計する方法を示す図。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="6dea7-137">Do: 正確なアウトライン アイコンのガイドラインに従います</span><span class="sxs-lookup"><span data-stu-id="6dea7-137">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="6dea7-138">アイコンで使用する白の RGB 値は、赤: 255、緑: 255、青: 255 である必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dea7-138">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="6dea7-139">アウトライン アイコンの他のすべての部分は完全に透明で、アルファ チャネルは 0 に設定されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dea7-139">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="アプリ アイコンをデザインしない方法を示す図。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="6dea7-141">[しない]: 円形または丸い四角形でトリミングする</span><span class="sxs-lookup"><span data-stu-id="6dea7-141">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="6dea7-142">アプリ パッケージで送信される色アイコンは正方形である必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dea7-142">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="6dea7-143">アイコンの角を丸めない。</span><span class="sxs-lookup"><span data-stu-id="6dea7-143">Don’t round the corners of your icon.</span></span> <span data-ttu-id="6dea7-144">Teams はコーナーの半径を自動的に調整します。</span><span class="sxs-lookup"><span data-stu-id="6dea7-144">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

### <a name="examples"></a><span data-ttu-id="6dea7-145">例</span><span class="sxs-lookup"><span data-stu-id="6dea7-145">Examples</span></span>

<span data-ttu-id="6dea7-146">さまざまな Teams の機能とコンテキストでアプリ アイコンを表示する方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6dea7-146">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="6dea7-147">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="6dea7-147">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="個人用アプリでアプリ アイコンがどのように表示されるのか示す例。" border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="6dea7-149">ボット (チャネル)</span><span class="sxs-lookup"><span data-stu-id="6dea7-149">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="チャネル内のボットでアプリ アイコンがどのように表示されるのか示す例。" border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="6dea7-151">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="6dea7-151">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<代替テキスト>" border="false":::
