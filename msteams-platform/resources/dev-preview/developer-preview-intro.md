---
title: 開発者プレビュー
description: Microsoft Teams の公開開発者プレビューの機能について説明します。
keywords: teams のプレビュー開発者向け機能
ms.openlocfilehash: a09e715e4e2d4aba72726cc96c4d248c550a3ab1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674917"
---
# <a name="public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="881f8-104">Microsoft Teams の公開開発者向けプレビュー</span><span class="sxs-lookup"><span data-stu-id="881f8-104">Public developer preview for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="881f8-105">プレビューに含まれている機能は完了していない可能性があり、公開リリースで利用できるようになる前に変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="881f8-105">Features included in preview may not be complete, and may undergo changes before becoming available in the public release.</span></span> <span data-ttu-id="881f8-106">テストと調査の目的のみに提供されています。</span><span class="sxs-lookup"><span data-stu-id="881f8-106">They are provided for testing and exploration purposes only.</span></span> <span data-ttu-id="881f8-107">運用アプリケーションでは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="881f8-107">They should not be used in production applications.</span></span>

<span data-ttu-id="881f8-108">開発者向けプレビューは、Microsoft Teams でリリースされていない機能に早期にアクセスできる開発者向けのパブリックプログラムです。</span><span class="sxs-lookup"><span data-stu-id="881f8-108">Developer Preview is a public program for developers which provides early access to unreleased features in Microsoft Teams.</span></span> <span data-ttu-id="881f8-109">これにより、Microsoft Teams アプリに含まれる可能性のある潜在的な機能を調査およびテストすることができます。</span><span class="sxs-lookup"><span data-stu-id="881f8-109">This allows you to explore and test upcoming features for potential inclusion in your Microsoft Teams app.</span></span> <span data-ttu-id="881f8-110">また、開発者向けプレビューのすべての機能についての[フィードバック](~/feedback.md)も歓迎します。</span><span class="sxs-lookup"><span data-stu-id="881f8-110">We also welcome [feedback](~/feedback.md) on any feature in developer preview.</span></span> <span data-ttu-id="881f8-111">開発者向けのプレビューは Microsoft Teams クライアントごとに有効になっているため、組織全体への影響について心配する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="881f8-111">Developer preview is enabled per Microsoft Teams client, so you don't need to worry about affecting your entire organization.</span></span>

## <a name="developer-preview-app-manifest"></a><span data-ttu-id="881f8-112">開発者プレビューアプリのマニフェスト</span><span class="sxs-lookup"><span data-stu-id="881f8-112">Developer preview app manifest</span></span>

<span data-ttu-id="881f8-113">開発者向けプレビューで有効になっている多くの機能では、アプリマニフェスト JSON ファイルを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="881f8-113">Many features enabled in developer preview will require alterations to your app manifest JSON file.</span></span> <span data-ttu-id="881f8-114">そのためには、このスキーマを使用する必要があります。このスキーマを使用[する場合は、](~/resources/schema/manifest-schema-dev-preview.md) [アプリ Studio](~/concepts/build-and-test/app-studio-overview.md)を使用してこれらの変更を行うことはできません。また、アプリを使用してテスト用アプリをアップロードすることもできません。</span><span class="sxs-lookup"><span data-stu-id="881f8-114">To do so you'll need to use the [developer preview manifest schema](~/resources/schema/manifest-schema-dev-preview.md) If you use this schema, you will not be able to use [App Studio](~/concepts/build-and-test/app-studio-overview.md) to make these changes, nor will you be able to use it to upload your app for testing.</span></span> <span data-ttu-id="881f8-115">アプリをアップロードするには、アプリバーの`More apps`アイコンをクリックしてから、 `Upload a custom app link`を選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="881f8-115">To upload your app you'll need to click the `More apps` icon on the app bar, then select the `Upload a custom app link`.</span></span> <span data-ttu-id="881f8-116">このメソッドを使用すると、アプリパッケージの zip 版のみをアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="881f8-116">Using this method you can only upload a zipped version of your app package.</span></span>

<span data-ttu-id="881f8-117">アプリ Studio を使用して、アプリパッケージの開発者以外のプレビュー部分を作成してから、そのパッケージをエクスポートし、 `manifest.json`ファイルを手動で編集して、使用する開発者向けプレビュー機能を追加すると便利な場合があります。</span><span class="sxs-lookup"><span data-stu-id="881f8-117">You may find it useful to use App Studio to create the non-developer preview portions of your app package, then export that package and manually edit the `manifest.json` file to add the developer preview features you wish to use.</span></span> <span data-ttu-id="881f8-118">開発者向けの`manifest.json`プレビュー機能をファイルに追加すると、そのパッケージをアプリ Studio に再インポートすることはできません。</span><span class="sxs-lookup"><span data-stu-id="881f8-118">Once you've added developer preview features to the `manifest.json` file you will not be able to re-import the package into App Studio.</span></span>

## <a name="enable-developer-preview"></a><span data-ttu-id="881f8-119">開発者プレビューを有効にする</span><span class="sxs-lookup"><span data-stu-id="881f8-119">Enable developer preview</span></span>

<span data-ttu-id="881f8-120">開発者プレビューはクライアントごとに有効になっていますが、開発者向けプレビューを有効にするオプションは、組織レベルで制御されています。</span><span class="sxs-lookup"><span data-stu-id="881f8-120">Developer preview is enabled on a per-client basis, but the option to turn on developer preview is controlled at the organization level.</span></span> <span data-ttu-id="881f8-121">個人に対して開発者プレビューを有効にするオプションを有効にするには、ユーザーがカスタムアプリをアップロードできるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="881f8-121">To enable the option to turn on developer preview for an individual, you must ensure that they have the ability to upload custom apps.</span></span> <span data-ttu-id="881f8-122">追加情報については[、「テナントの設定](~/concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="881f8-122">See [setting up your tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md) for additional information.</span></span>

<span data-ttu-id="881f8-123">開発者プレビュー機能を含むアプリを使用すると、開発者プレビューを有効にしていないクライアントが予期せず動作することがあります。</span><span class="sxs-lookup"><span data-stu-id="881f8-123">Using an app that contains developer preview features may cause clients that have not enabled developer preview to behave unexpectedly.</span></span> <span data-ttu-id="881f8-124">開発者プレビューのエントリが表示されない場合は、組織がアプリのアップロード用に構成されていないことが考えられます。</span><span class="sxs-lookup"><span data-stu-id="881f8-124">If you do not see an entry for developer preview the most likely reason is your organization is not configured for app uploading.</span></span>

### <a name="on-a-desktop-or-web-client"></a><span data-ttu-id="881f8-125">デスクトップまたは web クライアント上</span><span class="sxs-lookup"><span data-stu-id="881f8-125">On a desktop or web client</span></span>

<span data-ttu-id="881f8-126">デスクトップまたは web クライアント上で公開開発者プレビューを有効にするには、次の操作を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="881f8-126">To enable the public developer preview on a desktop or web client, you need to do the following:</span></span>

1. <span data-ttu-id="881f8-127">[ここで](~/concepts/build-and-test/prepare-your-o365-tenant.md)説明するように、テナントの管理コンソールでアプリのアップロードを有効にします。</span><span class="sxs-lookup"><span data-stu-id="881f8-127">Enabling uploading of apps in the admin console of your tenant as described [here](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
1. <span data-ttu-id="881f8-128">[Teams] インターフェイスの右上または左下にあるプロフィールをクリックして、[Teams] メニューを表示します。</span><span class="sxs-lookup"><span data-stu-id="881f8-128">Click on your profile (either in the upper right or lower left of the Teams interface) to display the Teams menu.</span></span>
1. <span data-ttu-id="881f8-129">[バージョン情報] → [開発者プレビュー] を選択します。</span><span class="sxs-lookup"><span data-stu-id="881f8-129">Select About → Developer preview.</span></span>
1. <span data-ttu-id="881f8-130">[**開発者向けプレビューに切り替え**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="881f8-130">Select **Switch to Developer preview**.</span></span>

### <a name="on-a-mobile-client"></a><span data-ttu-id="881f8-131">モバイルクライアントの場合</span><span class="sxs-lookup"><span data-stu-id="881f8-131">On a mobile client</span></span>

<span data-ttu-id="881f8-132">モバイルクライアントで公開開発者プレビューを有効にするには、次の手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="881f8-132">To enable the public developer preview on a mobile client, you need to do the following:</span></span>

1. <span data-ttu-id="881f8-133">[ここで](~/concepts/build-and-test/prepare-your-o365-tenant.md)説明するように、テナントの管理コンソールでアプリのアップロードを有効にします。</span><span class="sxs-lookup"><span data-stu-id="881f8-133">Enabling uploading of apps in the admin console of your tenant as described [here](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
1. <span data-ttu-id="881f8-134">左上の [ハンバーガー] メニューを開き、[**設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="881f8-134">Open the hamburger menu on the top left, then select **Settings**.</span></span>
1. <span data-ttu-id="881f8-135">[**バージョン情報**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="881f8-135">Select **About**.</span></span>
1. <span data-ttu-id="881f8-136">[開発者向けプレビュー] の切り替えをクリックします。</span><span class="sxs-lookup"><span data-stu-id="881f8-136">Click the Developer preview toggle.</span></span>

## <a name="disable-developer-preview"></a><span data-ttu-id="881f8-137">開発者プレビューを無効にする</span><span class="sxs-lookup"><span data-stu-id="881f8-137">Disable developer preview</span></span>

<span data-ttu-id="881f8-138">[バージョン情報] > [開発者向けプレビュー] の下にある同じメニュー項目を使用し、それをクリックしてオフにします。</span><span class="sxs-lookup"><span data-stu-id="881f8-138">Use the same menu item under About → Developer preview, and click on it to turn it off.</span></span>

## <a name="features-available-in-developer-preview"></a><span data-ttu-id="881f8-139">開発者向けプレビューで利用可能な機能</span><span class="sxs-lookup"><span data-stu-id="881f8-139">Features available in developer preview</span></span>

<span data-ttu-id="881f8-140">開発者プレビューで現在有効になっている機能の完全な一覧については[、「一般開発者プレビューの機能](../../resources/dev-preview/developer-preview-features.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="881f8-140">For a full list of the features currently enabled in developer preview see: [Features in the public developer preview](../../resources/dev-preview/developer-preview-features.md).</span></span>
