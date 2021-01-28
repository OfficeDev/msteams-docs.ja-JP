---
title: Developer Preview
description: Microsoft Teams のパブリック アプリケーションのDeveloper Previewについて説明します。
ms.topic: conceptual
keywords: Teams プレビュー開発者向け機能
ms.openlocfilehash: b8e8847d71ec3a571d434f952c79f3dd6a8f5bf1
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014076"
---
# <a name="public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="00de7-104">Microsoft Teams のパブリック開発者プレビュー</span><span class="sxs-lookup"><span data-stu-id="00de7-104">Public developer preview for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="00de7-105">プレビューに含まれる機能は完全ではなく、一般リリースで利用可能になる前に変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="00de7-105">Features included in preview may not be complete, and may undergo changes before becoming available in the public release.</span></span> <span data-ttu-id="00de7-106">これらは、テストおよび調査のみを目的として提供されます。</span><span class="sxs-lookup"><span data-stu-id="00de7-106">They are provided for testing and exploration purposes only.</span></span> <span data-ttu-id="00de7-107">これらは、実稼働アプリケーションでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="00de7-107">They should not be used in production applications.</span></span>

<span data-ttu-id="00de7-108">Developer Previewは、Microsoft Teams で未公開の機能に早期にアクセスできる開発者向けのパブリック プログラムです。</span><span class="sxs-lookup"><span data-stu-id="00de7-108">Developer Preview is a public program for developers which provides early access to unreleased features in Microsoft Teams.</span></span> <span data-ttu-id="00de7-109">これにより、Microsoft Teams アプリに組み込まれる可能性がある機能について、今後の機能を確認してテストできます。</span><span class="sxs-lookup"><span data-stu-id="00de7-109">This allows you to explore and test upcoming features for potential inclusion in your Microsoft Teams app.</span></span> <span data-ttu-id="00de7-110">開発者プレビューの [機能](~/feedback.md) に関するフィードバックも歓迎します。</span><span class="sxs-lookup"><span data-stu-id="00de7-110">We also welcome [feedback](~/feedback.md) on any feature in developer preview.</span></span> <span data-ttu-id="00de7-111">開発者プレビューは Microsoft Teams クライアントごとに有効になっているので、組織全体に影響を与える心配はありません。</span><span class="sxs-lookup"><span data-stu-id="00de7-111">Developer preview is enabled per Microsoft Teams client, so you don't need to worry about affecting your entire organization.</span></span>

## <a name="developer-preview-app-manifest"></a><span data-ttu-id="00de7-112">開発者プレビュー アプリ マニフェスト</span><span class="sxs-lookup"><span data-stu-id="00de7-112">Developer preview app manifest</span></span>

<span data-ttu-id="00de7-113">開発者プレビューで有効になっている多くの機能では、アプリ マニフェストの JSON ファイルを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="00de7-113">Many features enabled in developer preview will require alterations to your app manifest JSON file.</span></span> <span data-ttu-id="00de7-114">これを行うには、開発者プレビュー マニフェスト スキーマ[](~/resources/schema/manifest-schema-dev-preview.md)を使用する必要があります。このスキーマを使用する場合[、App Studio](~/concepts/build-and-test/app-studio-overview.md)を使用してこれらの変更を加え、テスト用にアプリをアップロードすることはできません。</span><span class="sxs-lookup"><span data-stu-id="00de7-114">To do so you'll need to use the [developer preview manifest schema](~/resources/schema/manifest-schema-dev-preview.md) If you use this schema, you will not be able to use [App Studio](~/concepts/build-and-test/app-studio-overview.md) to make these changes, nor will you be able to use it to upload your app for testing.</span></span> <span data-ttu-id="00de7-115">アプリをアップロードするには、アプリ バーのアイコンをクリックし、 `More apps` `Upload a custom app link`</span><span class="sxs-lookup"><span data-stu-id="00de7-115">To upload your app you'll need to click the `More apps` icon on the app bar, then select the `Upload a custom app link`.</span></span> <span data-ttu-id="00de7-116">この方法では、zip 形式のアプリ パッケージのみをアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="00de7-116">Using this method you can only upload a zipped version of your app package.</span></span>

<span data-ttu-id="00de7-117">App Studio を使用してアプリ パッケージの開発者以外のプレビュー部分を作成し、そのパッケージをエクスポートし、ファイルを手動で編集して、使用する開発者プレビュー機能を追加すると便利な場合があります。 `manifest.json`</span><span class="sxs-lookup"><span data-stu-id="00de7-117">You may find it useful to use App Studio to create the non-developer preview portions of your app package, then export that package and manually edit the `manifest.json` file to add the developer preview features you wish to use.</span></span> <span data-ttu-id="00de7-118">ファイルに開発者向けのプレビュー機能を追加すると、パッケージを App Studio に再 `manifest.json` インポートできます。</span><span class="sxs-lookup"><span data-stu-id="00de7-118">Once you've added developer preview features to the `manifest.json` file you will not be able to re-import the package into App Studio.</span></span>

## <a name="enable-developer-preview"></a><span data-ttu-id="00de7-119">開発者プレビューを有効にする</span><span class="sxs-lookup"><span data-stu-id="00de7-119">Enable developer preview</span></span>

<span data-ttu-id="00de7-120">開発者プレビューはクライアントごとに有効になりますが、開発者プレビューを有効にするオプションは組織レベルで制御されます。</span><span class="sxs-lookup"><span data-stu-id="00de7-120">Developer preview is enabled on a per-client basis, but the option to turn on developer preview is controlled at the organization level.</span></span> <span data-ttu-id="00de7-121">個人の開発者プレビューを有効にするオプションを有効にするには、カスタム アプリをアップロードする機能をユーザーが持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="00de7-121">To enable the option to turn on developer preview for an individual, you must ensure that they have the ability to upload custom apps.</span></span> <span data-ttu-id="00de7-122">詳細 [については、テナントの設定](~/concepts/build-and-test/prepare-your-o365-tenant.md) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="00de7-122">See [setting up your tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md) for additional information.</span></span>

<span data-ttu-id="00de7-123">開発者プレビュー機能を含むアプリを使用すると、開発者プレビューを有効にしていないクライアントが予期せず動作する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="00de7-123">Using an app that contains developer preview features may cause clients that have not enabled developer preview to behave unexpectedly.</span></span> <span data-ttu-id="00de7-124">開発者プレビューのエントリが表示されない場合、組織がアプリのアップロード用に構成されていない可能性が最も高い理由です。</span><span class="sxs-lookup"><span data-stu-id="00de7-124">If you do not see an entry for developer preview the most likely reason is your organization is not configured for app uploading.</span></span>

### <a name="on-a-desktop-or-web-client"></a><span data-ttu-id="00de7-125">デスクトップまたは Web クライアント上</span><span class="sxs-lookup"><span data-stu-id="00de7-125">On a desktop or web client</span></span>

<span data-ttu-id="00de7-126">デスクトップまたは Web クライアントでパブリック開発者プレビューを有効にするには、次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="00de7-126">To enable the public developer preview on a desktop or web client, you need to do the following:</span></span>

1. <span data-ttu-id="00de7-127">ここで説明するように、テナントの管理コンソールでアプリのアップロードを有効 [にします](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="00de7-127">Enabling uploading of apps in the admin console of your tenant as described [here](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
1. <span data-ttu-id="00de7-128">自分のプロファイル (Teams インターフェイスの右上または左下) をクリックして、Teams メニューを表示します。</span><span class="sxs-lookup"><span data-stu-id="00de7-128">Click on your profile (either in the upper right or lower left of the Teams interface) to display the Teams menu.</span></span>
1. <span data-ttu-id="00de7-129">[開発者向けプレビュー→について] を選択します。</span><span class="sxs-lookup"><span data-stu-id="00de7-129">Select About → Developer preview.</span></span>
1. <span data-ttu-id="00de7-130">[開発者 **向けプレビューに切り替える] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="00de7-130">Select **Switch to Developer preview**.</span></span>

### <a name="on-a-mobile-client"></a><span data-ttu-id="00de7-131">モバイル クライアントの場合</span><span class="sxs-lookup"><span data-stu-id="00de7-131">On a mobile client</span></span>

<span data-ttu-id="00de7-132">モバイル クライアントでパブリック開発者プレビューを有効にするには、次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="00de7-132">To enable the public developer preview on a mobile client, you need to do the following:</span></span>

1. <span data-ttu-id="00de7-133">ここで説明するように、テナントの管理コンソールでアプリのアップロードを有効 [にします](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="00de7-133">Enabling uploading of apps in the admin console of your tenant as described [here](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
1. <span data-ttu-id="00de7-134">左上のハンバーガー メニューを開き、[設定] を選択 **します**。</span><span class="sxs-lookup"><span data-stu-id="00de7-134">Open the hamburger menu on the top left, then select **Settings**.</span></span>
1. <span data-ttu-id="00de7-135">Select **About**.</span><span class="sxs-lookup"><span data-stu-id="00de7-135">Select **About**.</span></span>
1. <span data-ttu-id="00de7-136">[開発者向けプレビュー] トグルをクリックします。</span><span class="sxs-lookup"><span data-stu-id="00de7-136">Click the Developer preview toggle.</span></span>

## <a name="disable-developer-preview"></a><span data-ttu-id="00de7-137">開発者プレビューを無効にする</span><span class="sxs-lookup"><span data-stu-id="00de7-137">Disable developer preview</span></span>

<span data-ttu-id="00de7-138">[開発者向けプレビューについて] で同じメニュー→クリックしてオフにします。</span><span class="sxs-lookup"><span data-stu-id="00de7-138">Use the same menu item under About → Developer preview, and click on it to turn it off.</span></span>

## <a name="features-available-in-developer-preview"></a><span data-ttu-id="00de7-139">開発者プレビューで利用可能な機能</span><span class="sxs-lookup"><span data-stu-id="00de7-139">Features available in developer preview</span></span>

<span data-ttu-id="00de7-140">開発者プレビューで現在有効になっている機能の完全な一覧については、「パブリック開発者プレビューの [機能」を参照してください](../../resources/dev-preview/developer-preview-features.md)。</span><span class="sxs-lookup"><span data-stu-id="00de7-140">For a full list of the features currently enabled in developer preview see: [Features in the public developer preview](../../resources/dev-preview/developer-preview-features.md).</span></span>
