---
title: Developer Preview
description: パブリック サーバーの機能について説明Developer Preview Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: teams プレビュー開発者向け機能
ms.openlocfilehash: f19268afd81fe9fa7ae2116740e7b9d4ff8225cb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019721"
---
# <a name="public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="16291-104">開発者向けパブリック プレビュー Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="16291-104">Public developer preview for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="16291-105">プレビューに含まれる機能は完全ではない可能性があります。また、パブリック リリースで利用可能になる前に変更が加わる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="16291-105">Features included in preview may not be complete, and may undergo changes before becoming available in the public release.</span></span> <span data-ttu-id="16291-106">これらは、テストおよび探索の目的でのみ提供されます。</span><span class="sxs-lookup"><span data-stu-id="16291-106">They are provided for testing and exploration purposes only.</span></span> <span data-ttu-id="16291-107">これらは、実稼働アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="16291-107">They should not be used in production applications.</span></span>

<span data-ttu-id="16291-108">Developer Previewは、開発者向けの公開プログラムで、開発者は、開発中の未発表の機能に早期にアクセスMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="16291-108">Developer Preview is a public program for developers which provides early access to unreleased features in Microsoft Teams.</span></span> <span data-ttu-id="16291-109">これにより、今後の機能を確認してテストし、アプリに潜在的に組み込Microsoft Teamsできます。</span><span class="sxs-lookup"><span data-stu-id="16291-109">This allows you to explore and test upcoming features for potential inclusion in your Microsoft Teams app.</span></span> <span data-ttu-id="16291-110">開発者プレビューの [機能](~/feedback.md) に関するフィードバックも歓迎します。</span><span class="sxs-lookup"><span data-stu-id="16291-110">We also welcome [feedback](~/feedback.md) on any feature in developer preview.</span></span> <span data-ttu-id="16291-111">開発者プレビューはクライアントMicrosoft Teams有効になっているので、組織全体に影響を与える心配はありません。</span><span class="sxs-lookup"><span data-stu-id="16291-111">Developer preview is enabled per Microsoft Teams client, so you don't need to worry about affecting your entire organization.</span></span>

## <a name="developer-preview-app-manifest"></a><span data-ttu-id="16291-112">開発者プレビュー アプリ マニフェスト</span><span class="sxs-lookup"><span data-stu-id="16291-112">Developer preview app manifest</span></span>

<span data-ttu-id="16291-113">開発者プレビューで有効になっている多くの機能では、アプリ マニフェスト JSON ファイルを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="16291-113">Many features enabled in developer preview will require alterations to your app manifest JSON file.</span></span> <span data-ttu-id="16291-114">これを行うには、開発者プレビュー マニフェスト スキーマ[](~/resources/schema/manifest-schema-dev-preview.md)を使用する必要があります このスキーマを使用する場合は[、App Studio](~/concepts/build-and-test/app-studio-overview.md)を使用してこれらの変更を加え、テスト用にアプリをアップロードすることはできません。</span><span class="sxs-lookup"><span data-stu-id="16291-114">To do so you'll need to use the [developer preview manifest schema](~/resources/schema/manifest-schema-dev-preview.md) If you use this schema, you will not be able to use [App Studio](~/concepts/build-and-test/app-studio-overview.md) to make these changes, nor will you be able to use it to upload your app for testing.</span></span> <span data-ttu-id="16291-115">アプリをアップロードするには、アプリ バーのアイコンをクリックし、 を `More apps` 選択する必要があります `Upload a custom app link` 。</span><span class="sxs-lookup"><span data-stu-id="16291-115">To upload your app you'll need to click the `More apps` icon on the app bar, then select the `Upload a custom app link`.</span></span> <span data-ttu-id="16291-116">このメソッドを使用すると、圧縮されたバージョンのアプリ パッケージのみをアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="16291-116">Using this method you can only upload a zipped version of your app package.</span></span>

<span data-ttu-id="16291-117">App Studio を使用してアプリ パッケージの開発者以外のプレビュー部分を作成し、そのパッケージをエクスポートし、ファイルを手動で編集して、使用する開発者プレビュー機能を追加すると便利です `manifest.json` 。</span><span class="sxs-lookup"><span data-stu-id="16291-117">You may find it useful to use App Studio to create the non-developer preview portions of your app package, then export that package and manually edit the `manifest.json` file to add the developer preview features you wish to use.</span></span> <span data-ttu-id="16291-118">開発者プレビュー機能をファイルに追加すると、パッケージを App Studio に再 `manifest.json` インポートできない。</span><span class="sxs-lookup"><span data-stu-id="16291-118">Once you've added developer preview features to the `manifest.json` file you will not be able to re-import the package into App Studio.</span></span>

## <a name="enable-developer-preview"></a><span data-ttu-id="16291-119">開発者プレビューを有効にする</span><span class="sxs-lookup"><span data-stu-id="16291-119">Enable developer preview</span></span>

<span data-ttu-id="16291-120">開発者プレビューはクライアント単位で有効になっていますが、開発者プレビューを有効にするオプションは組織レベルで制御されます。</span><span class="sxs-lookup"><span data-stu-id="16291-120">Developer preview is enabled on a per-client basis, but the option to turn on developer preview is controlled at the organization level.</span></span> <span data-ttu-id="16291-121">個人の開発者プレビューを有効にするオプションを有効にするには、ユーザーがカスタム アプリをアップロードできる機能を持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="16291-121">To enable the option to turn on developer preview for an individual, you must ensure that they have the ability to upload custom apps.</span></span> <span data-ttu-id="16291-122">詳細については [、「テナントのセットアップ](~/concepts/build-and-test/prepare-your-o365-tenant.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="16291-122">See [setting up your tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md) for additional information.</span></span>

<span data-ttu-id="16291-123">開発者プレビュー機能を含むアプリを使用すると、開発者プレビューを有効にしていないクライアントが予期せず動作する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="16291-123">Using an app that contains developer preview features may cause clients that have not enabled developer preview to behave unexpectedly.</span></span> <span data-ttu-id="16291-124">開発者プレビューのエントリが表示されない場合、最も可能性の高い理由は、組織がアプリのアップロード用に構成されていないことです。</span><span class="sxs-lookup"><span data-stu-id="16291-124">If you do not see an entry for developer preview the most likely reason is your organization is not configured for app uploading.</span></span>

### <a name="on-a-desktop-or-web-client"></a><span data-ttu-id="16291-125">デスクトップまたは Web クライアント上</span><span class="sxs-lookup"><span data-stu-id="16291-125">On a desktop or web client</span></span>

<span data-ttu-id="16291-126">デスクトップまたは Web クライアントでパブリック開発者プレビューを有効にするには、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="16291-126">To enable the public developer preview on a desktop or web client, you need to do the following:</span></span>

1. <span data-ttu-id="16291-127">ここで説明するように、テナントの管理コンソールでアプリのアップロードを有効 [にします](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="16291-127">Enabling uploading of apps in the admin console of your tenant as described [here](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
1. <span data-ttu-id="16291-128">プロファイル (インターフェイスの右上または左下) をクリックしてTeamsメニュー Teamsします。</span><span class="sxs-lookup"><span data-stu-id="16291-128">Click on your profile (either in the upper right or lower left of the Teams interface) to display the Teams menu.</span></span>
1. <span data-ttu-id="16291-129">[開発者プレビュー→について] を選択します。</span><span class="sxs-lookup"><span data-stu-id="16291-129">Select About → Developer preview.</span></span>
1. <span data-ttu-id="16291-130">[開発者 **プレビューに切り替える] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="16291-130">Select **Switch to Developer preview**.</span></span>

### <a name="on-a-mobile-client"></a><span data-ttu-id="16291-131">モバイル クライアント上</span><span class="sxs-lookup"><span data-stu-id="16291-131">On a mobile client</span></span>

<span data-ttu-id="16291-132">モバイル クライアントでパブリック開発者プレビューを有効にするには、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="16291-132">To enable the public developer preview on a mobile client, you need to do the following:</span></span>

1. <span data-ttu-id="16291-133">ここで説明するように、テナントの管理コンソールでアプリのアップロードを有効 [にします](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="16291-133">Enabling uploading of apps in the admin console of your tenant as described [here](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
1. <span data-ttu-id="16291-134">左上のハンバーガー メニューを開き、[次へ]**を設定。**</span><span class="sxs-lookup"><span data-stu-id="16291-134">Open the hamburger menu on the top left, then select **Settings**.</span></span>
1. <span data-ttu-id="16291-135">[概要 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="16291-135">Select **About**.</span></span>
1. <span data-ttu-id="16291-136">[開発者プレビュー] トグルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16291-136">Click the Developer preview toggle.</span></span>

## <a name="disable-developer-preview"></a><span data-ttu-id="16291-137">開発者プレビューを無効にする</span><span class="sxs-lookup"><span data-stu-id="16291-137">Disable developer preview</span></span>

<span data-ttu-id="16291-138">[開発者向けプレビューについて] で同→を使用し、それをクリックしてオフにします。</span><span class="sxs-lookup"><span data-stu-id="16291-138">Use the same menu item under About → Developer preview, and click on it to turn it off.</span></span>

## <a name="features-available-in-developer-preview"></a><span data-ttu-id="16291-139">開発者プレビューで使用可能な機能</span><span class="sxs-lookup"><span data-stu-id="16291-139">Features available in developer preview</span></span>

<span data-ttu-id="16291-140">開発者プレビューで現在有効になっている機能の完全な一覧については、「パブリック開発者プレビューの [機能」を参照してください](../../resources/dev-preview/developer-preview-features.md)。</span><span class="sxs-lookup"><span data-stu-id="16291-140">For a full list of the features currently enabled in developer preview see: [Features in the public developer preview](../../resources/dev-preview/developer-preview-features.md).</span></span>
