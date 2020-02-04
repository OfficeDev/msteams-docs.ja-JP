---
title: アプリをパッケージ化する
description: Microsoft Teams でのテスト、アップロード、発行用にアプリをパッケージ化する方法について説明します。
keywords: teams アプリのパッケージ化
ms.topic: conceptual
ms.openlocfilehash: b76041b129e766dba2b401aaac0e12958a4e9b0d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674994"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="636cf-104">Microsoft Teams アプリ用のアプリパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="636cf-104">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="636cf-105">Teams のアプリは、アプリマニフェスト JSON ファイルによって定義され、アプリパッケージにアイコンが付いてバンドルされます。</span><span class="sxs-lookup"><span data-stu-id="636cf-105">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="636cf-106">アプリをアップロードして Teams にインストールし、基幹業務アプリカタログまたは AppSource に発行するには、アプリパッケージが必要です。</span><span class="sxs-lookup"><span data-stu-id="636cf-106">You'll need an app package to upload and install your app in Teams, and to publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="636cf-107">Teams アプリパッケージは、次のものを含む .zip ファイルです。</span><span class="sxs-lookup"><span data-stu-id="636cf-107">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="636cf-108">"Manifest.xml" という名前のマニフェストファイル。このファイルには、アプリの属性を指定し、そのユーザーのために必要なリソースをポイントします。たとえば、そのタブの構成ページの場所や、その bot の Microsoft アプリ ID があります。</span><span class="sxs-lookup"><span data-stu-id="636cf-108">A manifest file named "manifest.json", which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="636cf-109">透明な "アウトライン" アイコンと完全な "色" アイコン。</span><span class="sxs-lookup"><span data-stu-id="636cf-109">A transparent "outline" icon and a full "color" icon.</span></span> <span data-ttu-id="636cf-110">詳細については、このトピックで後述する[アイコン](#icons)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="636cf-110">See [Icons](#icons) later in this topic for more information.</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="636cf-111">マニフェストの作成</span><span class="sxs-lookup"><span data-stu-id="636cf-111">Creating a manifest</span></span>

<span data-ttu-id="636cf-112">*Teams App Studio*は、マニフェストを構成する際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="636cf-112">*Teams App Studio* can help configure your manifest.</span></span> <span data-ttu-id="636cf-113">また、カードの反応コントロールライブラリと構成可能なサンプルも含まれています。</span><span class="sxs-lookup"><span data-stu-id="636cf-113">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="636cf-114">「 [App Studio の概要](~/concepts/build-and-test/app-studio-overview.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="636cf-114">See [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="636cf-115">マニフェストファイルの名前は "manifest.xml" で、アップロードパッケージのトップレベルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="636cf-115">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="636cf-116">以前に作成されたマニフェストとパッケージは、古いバージョンのスキーマをサポートしている可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="636cf-116">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="636cf-117">Teams アプリおよび特に AppSource (以前の Office ストア) 送信の場合は、現在の[マニフェストスキーマ](~/resources/schema/manifest-schema.md)を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="636cf-117">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="636cf-118">マニフェストの最初にスキーマを指定して、コードエディターで IntelliSense または同様のサポートを有効にします。</span><span class="sxs-lookup"><span data-stu-id="636cf-118">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",`

## <a name="icons"></a><span data-ttu-id="636cf-119">アイコン</span><span class="sxs-lookup"><span data-stu-id="636cf-119">Icons</span></span>

> [!Note]
> <span data-ttu-id="636cf-120">アプリに bot またはメッセージングの拡張機能が含まれている場合、使用されるアイコンは bot フレームワークの bot 登録にアップロードされます。</span><span class="sxs-lookup"><span data-stu-id="636cf-120">If your app contains a bot or messaging extension, the icons used will be the icons uploaded to your bot registration in the Bot Framework.</span></span>

<span data-ttu-id="636cf-121">Microsoft Teams では、アプリの環境で使用するために、2つのアイコンが必要です。</span><span class="sxs-lookup"><span data-stu-id="636cf-121">Microsoft Teams requires two icons for your app experience, to be used within the product.</span></span> <span data-ttu-id="636cf-122">アイコンは、パッケージに含める必要があり、マニフェストの相対パスで参照されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="636cf-122">Icons must be included in the package and referenced via relative paths in the manifest.</span></span> <span data-ttu-id="636cf-123">各パスの最大長は2048バイトで、アイコンの形式は .png です。</span><span class="sxs-lookup"><span data-stu-id="636cf-123">The maximum length of each path is 2048 bytes, and the format of the icon is .png.</span></span>

### <a name="color"></a><span data-ttu-id="636cf-124">color</span><span class="sxs-lookup"><span data-stu-id="636cf-124">color</span></span>

<span data-ttu-id="636cf-125">この`color`アイコンは、Microsoft Teams (アプリとタブ、ボット、flyouts など) 全体で使用されます。</span><span class="sxs-lookup"><span data-stu-id="636cf-125">The `color` icon is used throughout Microsoft Teams (in app and tab galleries, bots, flyouts, and so on).</span></span> <span data-ttu-id="636cf-126">このアイコンは、192x192 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="636cf-126">This icon should be 192x192 pixels.</span></span> <span data-ttu-id="636cf-127">アイコンには色 (または色) を指定できますが、背景はブランド化された色にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="636cf-127">Your icon can be any color (or colors), but the background should be your branded accent color.</span></span> <span data-ttu-id="636cf-128">また、アイコンの bot バージョンのトリミングに対応するために、アイコンの周囲のパディングを小さくする必要があります。</span><span class="sxs-lookup"><span data-stu-id="636cf-128">It should also have a small amount of padding surrounding the icon to accommodate the hexagonal cropping for the bot version of the icon.</span></span>

### <a name="outline"></a><span data-ttu-id="636cf-129">outline</span><span class="sxs-lookup"><span data-stu-id="636cf-129">outline</span></span>

<span data-ttu-id="636cf-130">この`outline`アイコンは、次の場所で使用されます。ユーザーが "お気に入り" としてマークしたアプリバーとメッセージング拡張機能。</span><span class="sxs-lookup"><span data-stu-id="636cf-130">The `outline` icon is used in these places: the app bar and messaging extensions the user has marked as a "favorite."</span></span> <span data-ttu-id="636cf-131">このアイコンは32x32 ピクセルでなければなりません。</span><span class="sxs-lookup"><span data-stu-id="636cf-131">This icon must be 32x32 pixels.</span></span> <span data-ttu-id="636cf-132">アウトラインアイコンには、白と透明度のみが含まれている必要があります (その他の色は使用できません)。</span><span class="sxs-lookup"><span data-stu-id="636cf-132">Your outline icon must contain only white and transparency (no other colors).</span></span> <span data-ttu-id="636cf-133">このアイコンは、背景が透明な白色または白の背景で透明にすることができます。</span><span class="sxs-lookup"><span data-stu-id="636cf-133">The icon can be white with transparent background or transparent with a white background.</span></span> <span data-ttu-id="636cf-134">アウトラインアイコンは、アイコンの周囲に特別なパディングを持たないようにする必要があります。32x32 の次元を維持したまま、できるだけトリミングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="636cf-134">The outline icon should not have extra padding surrounding the icon and should be as tightly cropped as possible while still maintaining the 32x32 dimensions.</span></span> <span data-ttu-id="636cf-135">次に、いくつかの良い例を示します。</span><span class="sxs-lookup"><span data-stu-id="636cf-135">Here are a few good examples:</span></span>

![サンプルのアウトラインアイコン](~/assets/images/icons/sample20x20s.png)

<span data-ttu-id="636cf-137">たとえば、会社が Contoso であるとします。</span><span class="sxs-lookup"><span data-stu-id="636cf-137">For example, say your company is Contoso.</span></span> <span data-ttu-id="636cf-138">2つのアイコンを送信します。</span><span class="sxs-lookup"><span data-stu-id="636cf-138">You'd submit two icons:</span></span>

![アイコンショーケース](~/assets/images/framework/framework_submit_icon.png)

<span data-ttu-id="636cf-140">UI にアイコンを表示する方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="636cf-140">Here's how the icons would appear in the UI:</span></span>

#### <a name="bot-and-chiclet-in-channel-view"></a><span data-ttu-id="636cf-141">[チャネル] ビューのボットと chiclet</span><span class="sxs-lookup"><span data-stu-id="636cf-141">Bot and chiclet in Channel view</span></span>

![Bot と chiclet UX](~/assets/images/icons/botandchiclet.png)

#### <a name="flyout"></a><span data-ttu-id="636cf-143">ポップアップ</span><span class="sxs-lookup"><span data-stu-id="636cf-143">Flyout</span></span>

![サンプルの Contoso アイコン](~/assets/images/icons/flyout.png)

#### <a name="app-bar-and-home-screen"></a><span data-ttu-id="636cf-145">アプリバーとホーム画面</span><span class="sxs-lookup"><span data-stu-id="636cf-145">App bar and home screen</span></span>

![サンプルの Contoso アイコン](~/assets/images/icons/appbarhomescreen.png)
