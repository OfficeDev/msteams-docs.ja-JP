---
title: アプリをパッケージ化する
description: 発行をテスト、アップロード、および保存するために Microsoft Teams アプリをパッケージ化する方法について説明します。
ms.topic: conceptual
ms.openlocfilehash: 6929375c8d6a1602f01d83d15bfa0dab7f02a664
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605289"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="8ae7f-103">Microsoft Teams アプリのアプリ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="8ae7f-103">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="8ae7f-104">Teams のアプリは、アプリ マニフェスト JSON ファイルによって定義され、各アイコンがアプリ パッケージにバンドルされます。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-104">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="8ae7f-105">アプリをアップロードして Teams にインストールし、基幹業務アプリカタログまたは AppSource に発行するには、アプリパッケージが必要です。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-105">You'll need an app package to upload and install your app in Teams and publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="8ae7f-106">Teams アプリ パッケージは、次のものを含む .zip ファイルです。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-106">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="8ae7f-107">という名前のマニフェストファイル。アプリの属性を指定して、その機能に `manifest.json` 必要なリソースをポイントします。たとえば、そのタブの構成ページの場所や、その bot の Microsoft アプリ ID を指定します。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-107">A manifest file named `manifest.json`, which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="8ae7f-108">[アプリの色とアウトラインアイコン](#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-108">[Color and outline icons for your app](#app-icons).</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="8ae7f-109">マニフェストの作成</span><span class="sxs-lookup"><span data-stu-id="8ae7f-109">Creating a manifest</span></span>

<span data-ttu-id="8ae7f-110">*Teams App Studio* は、マニフェストを構成する際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-110">*Teams App Studio* can help configure your manifest.</span></span> <span data-ttu-id="8ae7f-111">React 制御ライブラリとカード用の構成可能なサンプルも含まれています。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-111">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="8ae7f-112">「[App Studio の概要](~/concepts/build-and-test/app-studio-overview.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-112">See [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="8ae7f-113">マニフェスト ファイルは、"manifest.json" という名前で、アップロード パッケージの最上位レベルになければなりません。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-113">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="8ae7f-114">以前に作成されたマニフェストとパッケージは、古いバージョンのスキーマをサポートしている可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-114">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="8ae7f-115">Teams アプリ、特に AppSource (以前の Office ストア) 配信の場合は、最新の[マニフェスト スキーマ](~/resources/schema/manifest-schema.md)を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-115">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="8ae7f-116">マニフェストの最初にスキーマを指定して、コード エディターで IntelliSense または同様のサポートを有効にします。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-116">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="app-icons"></a><span data-ttu-id="8ae7f-117">アプリのアイコン</span><span class="sxs-lookup"><span data-stu-id="8ae7f-117">App icons</span></span>

<span data-ttu-id="8ae7f-118">アプリパッケージには、2つの PNG バージョンのアプリアイコン (カラーアイコンとアウトラインアイコン) が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-118">Your app package must include two PNG versions of your app icon—a color icon and an outline icon.</span></span> <span data-ttu-id="8ae7f-119">アプリが AppSource レビューに合格するには、これらのアイコンが次のサイズ要件を満たしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-119">For your app to pass the AppSource review, these icons must meet the following size requirements.</span></span>

> [!Note]
> <span data-ttu-id="8ae7f-120">アプリに bot またはメッセージングの拡張機能がある場合は、それらのアイコンも Microsoft Azure Bot サービスの登録に含まれます。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-120">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

### <a name="color-icon"></a><span data-ttu-id="8ae7f-121">色アイコン</span><span class="sxs-lookup"><span data-stu-id="8ae7f-121">Color icon</span></span>

<span data-ttu-id="8ae7f-122">アイコンのカラーバージョンは、ほとんどの Teams のシナリオで表示され、192x192 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-122">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="8ae7f-123">アイコン記号 (96x96 ピクセル) は任意の色または色にすることができますが、単色または完全に透明な四角形の背景上に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-123">Your icon symbol (96x96 pixels) can be any color or colors, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="8ae7f-124">Teams では、複数のシナリオで角の丸い四角形が表示されるように自動的にアイコンがトリミングされます。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-124">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="8ae7f-125">シンボルの周囲に48ピクセルのパディングを含めることにより、ディテールを失わずにこれらのトリミングを行うことができるようにします。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-125">Include 48 pixels of padding around your symbol so these crops can be made without losing any detail.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams のカラーアイコン設計ガイダンス。" border="false":::

### <a name="outline-icon"></a><span data-ttu-id="8ae7f-127">アウトラインアイコン</span><span class="sxs-lookup"><span data-stu-id="8ae7f-127">Outline icon</span></span>

<span data-ttu-id="8ae7f-128">アウトラインアイコンは2つのシナリオで表示されます。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-128">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="8ae7f-129">アプリが使用中で、Teams の左側にあるアプリバーで "ホイストされた"。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-129">When your app is in use and “hoisted” on the app bar on the left of Teams.</span></span>
* <span data-ttu-id="8ae7f-130">ユーザーがアプリのメッセージング拡張機能を固定するとき。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-130">when a user pins your app's messaging extension.</span></span>

<span data-ttu-id="8ae7f-131">アイコンは32x32 ピクセルでなければなりません。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-131">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="8ae7f-132">背景を透明にする、または背景を透明にすることができます (他の色は使用できません)。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-132">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="8ae7f-133">アウトラインアイコンには、記号の周りに特別なスペースを含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-133">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams のカラーアイコン設計ガイダンス。" border="false":::

### <a name="best-practices"></a><span data-ttu-id="8ae7f-135">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="8ae7f-135">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="アプリアイコンを設計する方法を示す図。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="8ae7f-137">Do: 正確なアウトラインアイコンのガイドラインに従う</span><span class="sxs-lookup"><span data-stu-id="8ae7f-137">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="8ae7f-138">アイコンで使用される白の RGB 値は、赤である必要があります: 255、Green: 255、Blue: 255。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-138">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="8ae7f-139">アウトラインアイコンの他の部分はすべて完全に透明にする必要があり、アルファチャネルを0に設定します。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-139">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="アプリアイコンをデザインする方法を示す図。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="8ae7f-141">[いいえ: 円形または角丸正方形] 図形でトリミングします。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-141">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="8ae7f-142">アプリパッケージで送信されるカラーアイコンは、正方形である必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-142">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="8ae7f-143">アイコンの角を丸くしないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-143">Don’t round the corners of your icon.</span></span> <span data-ttu-id="8ae7f-144">Teams では、角の半径が自動的に調整されます。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-144">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

### <a name="examples"></a><span data-ttu-id="8ae7f-145">例</span><span class="sxs-lookup"><span data-stu-id="8ae7f-145">Examples</span></span>

<span data-ttu-id="8ae7f-146">アプリアイコンをさまざまなチームの機能やコンテキストで表示する方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="8ae7f-146">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="8ae7f-147">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="8ae7f-147">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="アプリアイコンが個人用アプリでどのように表示されるかを示す例。" border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="8ae7f-149">Bot (チャネル)</span><span class="sxs-lookup"><span data-stu-id="8ae7f-149">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="アプリアイコンがチャネル内のボットをどのように表示されるかを示す例。" border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="8ae7f-151">メッセージング拡張機能</span><span class="sxs-lookup"><span data-stu-id="8ae7f-151">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<代替テキスト>" border="false":::
