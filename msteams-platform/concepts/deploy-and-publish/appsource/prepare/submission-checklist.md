---
title: ストア提出チェックリスト
description: Microsoft Teams アプリを AppSource に発行する前に使用するチェックリスト
ms.topic: reference
localization_priority: Normal
keywords: teams 発行ストア オフィス発行チェックリスト申請 Teams アプリ appsource 検証
ms.openlocfilehash: 1e7698e143d313ce46b834eada608571e3280b8a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020787"
---
# <a name="prepare-for-appsource-submission"></a><span data-ttu-id="48ee5-104">AppSource 申請の準備</span><span class="sxs-lookup"><span data-stu-id="48ee5-104">Prepare for AppSource submission</span></span>  

<span data-ttu-id="48ee5-105">AppSource に一覧表示するには、アプリが承認プロセスを通過する必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-105">To be listed on AppSource, your app must go through an approval process.</span></span> <span data-ttu-id="48ee5-106">これは、Microsoft Teams グループが提供する無料のサービスで、アプリが説明に従って動作し、適切なすべてのメタデータを含み、エンド ユーザーにとって価値のあるコンテンツを提供します。</span><span class="sxs-lookup"><span data-stu-id="48ee5-106">This is a free service provided by the Microsoft Teams group that verifies that your app works as described, contains all appropriate metadata, and provides content that would be valuable to an end user.</span></span> <span data-ttu-id="48ee5-107">迅速な承認を実現するために、アプリが次の要件とガイドラインを満たしていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="48ee5-107">To help you achieve rapid approval, ensure your app meets the following requirements and guidelines:</span></span>

* <span data-ttu-id="48ee5-108">**配布方法:** アプリがストア プラットフォームでの公開を意図することを確認します。</span><span class="sxs-lookup"><span data-stu-id="48ee5-108">**Distribution method:** Make sure your app is meant for publication on a store platform.</span></span> <span data-ttu-id="48ee5-109">AppSource [に発行](../../overview.md) せずにアプリを配布する他のオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-109">There are [other options](../../overview.md) to distribute your app without publishing to AppSource.</span></span>
* <span data-ttu-id="48ee5-110">**検証ポリシー:** アプリは、申請の前に、 [現在のすべての AppSource 検証ポリシーを渡](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) す必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-110">**Validation policies:** Your app must pass all current [AppSource validation policies](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) before submission.</span></span> 
  > [!NOTE] 
  > <span data-ttu-id="48ee5-111">Appsource 検証ポリシーは変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-111">The Appsource validation policies are subject to change.</span></span>
* <span data-ttu-id="48ee5-112">**モバイルの準備:** アプリはモバイル対応である必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-112">**Mobile readiness:** Your app must be mobile responsive.</span></span> <span data-ttu-id="48ee5-113">アプリにタブが含まれている場合は、モバイル設計[](~/tabs/design/tabs-mobile.md)ガイドラインに従う必要があります。アプリはモバイル[](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment)OS (iOS と Android) でアップセルの要件を満たさなければならない必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-113">If your app contains tabs, they must follow the [mobile design guidelines](~/tabs/design/tabs-mobile.md) and your app must comply with [no upsell requirements](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment) on mobile OS (iOS and Android).</span></span>
* <span data-ttu-id="48ee5-114">**アプリの自己テスト:** マニフェスト検証ツールを使用 [してアプリをテストします](#teams-app-validation-tool)。</span><span class="sxs-lookup"><span data-stu-id="48ee5-114">**Self test your app:** Test your app using the [Manifest validation tool](#teams-app-validation-tool).</span></span>
* <span data-ttu-id="48ee5-115">**アプリの詳細ページ:** アプリは、アプリの詳細ページチェックリスト  [と一致している必要があります](detail-page-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="48ee5-115">**App detail page:** Your app must align with the  [App detail page checklist](detail-page-checklist.md).</span></span>
* <span data-ttu-id="48ee5-116">**ヒントと頻繁に失敗するケース:** アプリの申請と承認時間を改善するために、リストされている [ヒント](frequently-failed-cases.md)  と頻繁に失敗したケースに特に注意してください。</span><span class="sxs-lookup"><span data-stu-id="48ee5-116">**Tips and frequently failed cases:** Pay extra attention to the listed [Tips and frequently failed cases](frequently-failed-cases.md)  to improve your app submission and approval time.</span></span>
* <span data-ttu-id="48ee5-117">**アプリ マニフェスト:** アプリ マニフェストのチェックリストに対して [アプリ マニフェストを確認します](app-manifest-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="48ee5-117">**App manifest:** Check your app manifest against the [App manifest checklist](app-manifest-checklist.md).</span></span>
* <span data-ttu-id="48ee5-118">**テストとデバッグ:** アプリを完全にテストしてデバッグ [したと確認します](../../../build-and-test/debug.md)。</span><span class="sxs-lookup"><span data-stu-id="48ee5-118">**Testing and debugging:** Make certain that you have fully [tested and debugged your app](../../../build-and-test/debug.md).</span></span>
* <span data-ttu-id="48ee5-119">**テストノート:** 検証用 [のテスト ノートを含める](#test-notes-for-validation)</span><span class="sxs-lookup"><span data-stu-id="48ee5-119">**Testing notes:** Include your [test notes for validation](#test-notes-for-validation)</span></span>
* <span data-ttu-id="48ee5-120">**プライバシー ポリシー:** プライバシー ポリシー [、使用条件](#privacy-policy-terms-of-use-and-support-urls) 、およびサポート URL がガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-120">**Privacy policies:** Ensure your [privacy policy, terms of use and support URLs](#privacy-policy-terms-of-use-and-support-urls) follow our guidelines.</span></span>

<span data-ttu-id="48ee5-121">上記のすべての要件を完了したら、パートナー センターから AppSource にパッケージを [提出します](/office/dev/store/use-partner-center-to-submit-to-appsource)。</span><span class="sxs-lookup"><span data-stu-id="48ee5-121">Once you have completed all of the above requirements, submit your package to AppSource through [Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource).</span></span>

## <a name="teams-app-validation-tool"></a><span data-ttu-id="48ee5-122">Teams アプリ検証ツール</span><span class="sxs-lookup"><span data-stu-id="48ee5-122">Teams App Validation Tool</span></span>

<span data-ttu-id="48ee5-123">アプリ検証ツールは、アプリ検証ツール [と予備](#teams-app-validator) チェックリスト [で構成されます](#preliminary-checklist)。</span><span class="sxs-lookup"><span data-stu-id="48ee5-123">The app validation tool consists of an [app validator](#teams-app-validator) and a [preliminary checklist](#preliminary-checklist).</span></span> <span data-ttu-id="48ee5-124">このツールは [、AppSource](/office/dev/store/submit-to-appsource-via-partner-center) がアプリの申請を評価するために使用するのと同じテスト ケースをレプリケートします。</span><span class="sxs-lookup"><span data-stu-id="48ee5-124">The tool replicates the same test cases used by [AppSource](/office/dev/store/submit-to-appsource-via-partner-center) to evaluate your app submission.</span></span> <span data-ttu-id="48ee5-125">したがって、ソリューションを承認のために AppSource に提出する前に、すべてのテスト ケースに合格することが重要です。このツールは、Teams プラットフォーム内のいくつかの領域で確認できます。</span><span class="sxs-lookup"><span data-stu-id="48ee5-125">Therefore,  it's crucial to pass all the test cases prior to submitting your solution to AppSource for approval.The tool can be found in several areas within the Teams platform:</span></span>

> [!div class="checklist"]
>
> * [<span data-ttu-id="48ee5-126">**アプリ検証機能のホームページ**</span><span class="sxs-lookup"><span data-stu-id="48ee5-126">**App Validator homepage**</span></span>](https://dev.teams.microsoft.com/appvalidation.html)
> * [<span data-ttu-id="48ee5-127">**Teams Visual Studio コード ツールキット**</span><span class="sxs-lookup"><span data-stu-id="48ee5-127">**Teams Visual Studio Code toolkit**</span></span>](/toolkit/visual-studio-code-overview.md)
> * [<span data-ttu-id="48ee5-128">**App Studio**</span><span class="sxs-lookup"><span data-stu-id="48ee5-128">**App Studio**</span></span>](../../../build-and-test/app-studio-overview.md)

### <a name="teams-app-validator"></a><span data-ttu-id="48ee5-129">Teams アプリ検証機能</span><span class="sxs-lookup"><span data-stu-id="48ee5-129">Teams app validator</span></span>

<span data-ttu-id="48ee5-130">[ **検証]** ページでは、AppSource に申請する前にアプリ パッケージを確認できます。</span><span class="sxs-lookup"><span data-stu-id="48ee5-130">The **Validate** page allows you to check your app package before submission to AppSource.</span></span> <span data-ttu-id="48ee5-131">アプリ パッケージをアップロードするだけで、検証ツールはマニフェスト関連のすべてのテスト ケースに対してアプリをチェックします。</span><span class="sxs-lookup"><span data-stu-id="48ee5-131">Simply upload your app package and the validation tool will check your app against all manifest-related test cases.</span></span> <span data-ttu-id="48ee5-132">失敗したテストごとに、エラーの修正に役立つドキュメント リンクが説明されています。</span><span class="sxs-lookup"><span data-stu-id="48ee5-132">For each failed test, the description provides a documentation link to help you fix the error.</span></span>

![検証ツール](../../../../assets/images/validation-tool/validator.png)

### <a name="preliminary-checklist"></a><span data-ttu-id="48ee5-134">予備チェックリスト</span><span class="sxs-lookup"><span data-stu-id="48ee5-134">Preliminary checklist</span></span>

<span data-ttu-id="48ee5-135">自動化が困難なテスト シナリオでは、予備チェックリストで最も一般的に失敗したテスト ケースの 7 つが表示されます。</span><span class="sxs-lookup"><span data-stu-id="48ee5-135">For test scenarios that are difficult to automate, the preliminary checklist surfaces seven of the most commonly failed test cases.</span></span>

![予備チェックリスト](../../../../assets/images/validation-tool/preliminary-checklist.png)

## <a name="privacy-policy-terms-of-use-and-support-urls"></a><span data-ttu-id="48ee5-137">プライバシー ポリシー、使用条件、サポート URL</span><span class="sxs-lookup"><span data-stu-id="48ee5-137">Privacy policy, terms of use and support URLs</span></span>

### <a name="privacy-policy"></a><span data-ttu-id="48ee5-138">プライバシー ポリシー</span><span class="sxs-lookup"><span data-stu-id="48ee5-138">Privacy policy</span></span>

<span data-ttu-id="48ee5-139">プライバシー ポリシーのガイドライン:</span><span class="sxs-lookup"><span data-stu-id="48ee5-139">Privacy policy guidelines:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="48ee5-140">プライバシー ポリシーは、アプリやすべてのサービスの全体的なポリシーに固有の場合があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-140">The privacy policy can be specific to your app and/or an overall policy for all of your services.</span></span>
> * <span data-ttu-id="48ee5-141">一般的なプライバシー ポリシーを使用する場合は、Teams アプリと Web サイトを含めるには、「サービス」、"アプリケーション"、および "プラットフォーム" を参照する必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-141">If you use a generic privacy policy, it must reference "services", "applications", and "platforms" to include your Teams app as well as your website.</span></span>
> * <span data-ttu-id="48ee5-142">ユーザー データストレージ、ユーザー データ保持、削除、およびセキュリティ制御の処理方法を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-142">It must include how you handle user data storage, user data retention, deletion, and security controls.</span></span>
> * <span data-ttu-id="48ee5-143">連絡先情報が含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-143">It must include your contact information.</span></span>
> * <span data-ttu-id="48ee5-144">リンクの破損、ベータ URL、ステージング URL は含めずにしてください。</span><span class="sxs-lookup"><span data-stu-id="48ee5-144">It should not contain broken links, beta URLs, or staging URLs.</span></span>

### <a name="terms-of-use"></a><span data-ttu-id="48ee5-145">利用規約</span><span class="sxs-lookup"><span data-stu-id="48ee5-145">Terms of use</span></span>

<span data-ttu-id="48ee5-146">使用条件ステートメントは、アプリやアドインの提供に固有で適用可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-146">Your terms of use statement should be specific and applicable to your app and/or add-in offering.</span></span>

### <a name="support-urls"></a><span data-ttu-id="48ee5-147">サポート URL</span><span class="sxs-lookup"><span data-stu-id="48ee5-147">Support URLs</span></span>

<span data-ttu-id="48ee5-148">サポート URL では、アプリに関する問題について連絡するために、認証またはログイン資格情報を必要としない必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-148">Your support URLs should not require authentication or login credential to contact you for any issues with your app.</span></span>

## <a name="test-notes-for-validation"></a><span data-ttu-id="48ee5-149">検証に関するテスト ノート</span><span class="sxs-lookup"><span data-stu-id="48ee5-149">Test notes for validation</span></span>

<span data-ttu-id="48ee5-150">次の情報を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-150">Please include the following:</span></span>

* <span data-ttu-id="48ee5-151">少なくとも 2 つのログイン資格情報 、1 つの管理者と 1 つの管理者以外の資格情報を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-151">You must provide at least two login credentials, one admin and one non-admin.</span></span>

* <span data-ttu-id="48ee5-152">検証の目的で、提供するアカウントには、十分な事前入力データが必要です。</span><span class="sxs-lookup"><span data-stu-id="48ee5-152">For verification purposes, the accounts you provide should have sufficient pre-populated data.</span></span>

* <span data-ttu-id="48ee5-153">エンタープライズ アプリ、サブスクリプションが必要なアプリ、または Office 365 テナント/ドメイン依存関係があるアプリの場合は、最初に実行するユーザー エクスペリエンスを検証するために、アプリ用に事前構成されていない同じドメインに 3 番目のアカウントを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-153">For enterprise apps, apps where a subscription is required, or apps where there is an Office 365 tenant/domain dependency, you must provide a third account in the same domain that is not pre-configured for your app so that we can validate the first-run user experience.</span></span>

* <span data-ttu-id="48ee5-154">アプリにプレミアム/アップグレードされた機能がある場合は、そのエクスペリエンスをテストするために必要なアクセス権を持つアカウントを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="48ee5-154">If your app has premium/upgraded features, an account with the necessary access must be provided to test that experience.</span></span>

* <span data-ttu-id="48ee5-155">テスト ノートを SharePoint にアップロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="48ee5-155">You may choose to upload your test notes to SharePoint.</span></span> <span data-ttu-id="48ee5-156">その場合は、ファイルへのパブリック リンクを指定してください。</span><span class="sxs-lookup"><span data-stu-id="48ee5-156">If so, please provide a public link to the file.</span></span>

* <span data-ttu-id="48ee5-157">**テスト アカウント**.</span><span class="sxs-lookup"><span data-stu-id="48ee5-157">**Test Accounts**.</span></span> <span data-ttu-id="48ee5-158">アプリでライセンスアカウントのみを許可するか、バックエンドからセーフリストに登録できる場合は、テスト アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="48ee5-158">A test account is required if your app only allows licensed accounts or safelisting from the backend.</span></span> <span data-ttu-id="48ee5-159">また、アプリでチーム/グループ のチャット スコープが許可されている場合は、チーム の共同作業シナリオを検証するために、同じテナント内の 2 つのテスト アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="48ee5-159">Also, if there is a team/group chat scope allowed in your app,  two test accounts in the same tenant are required to validate the team collaboration scenario.</span></span>

* <span data-ttu-id="48ee5-160">**統合手順**.</span><span class="sxs-lookup"><span data-stu-id="48ee5-160">**Integration steps**.</span></span> <span data-ttu-id="48ee5-161">テナント管理者による事前構成でアプリを使用する必要がある場合は、手順を含めるか、構成済みの管理者アカウントと管理者以外のアカウントを入力して検証します。</span><span class="sxs-lookup"><span data-stu-id="48ee5-161">If pre-configuration by a tenant admin is required to use the app, include the steps and/or provide configured admin and non-admin accounts for validation.</span></span> <span data-ttu-id="48ee5-162">注: [365 Developer Program サブスクリプションOfficeサインアップ](https://developer.microsoft.com/microsoft-365/dev-program) できます。</span><span class="sxs-lookup"><span data-stu-id="48ee5-162">Note: you can sign up for an [Office 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="48ee5-163">これは 90 日間 *無料* で開発活動に使用する限り継続的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="48ee5-163">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span>

* <span data-ttu-id="48ee5-164">**Teams のアプリ機能に関する注意事項**: Teams 内でアプリが提供する機能の詳細と、各機能のテスト手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="48ee5-164">**Notes regarding the app features in Teams**: Detail all of the capabilities the app offers within Teams and steps for testing each feature.</span></span>

* <span data-ttu-id="48ee5-165">**アプリの機能を示すビデオ (オプション)**: 製品のビデオ録画を提供して、アプリの機能を完全に理解することができます。</span><span class="sxs-lookup"><span data-stu-id="48ee5-165">**Video showing the app functionality (Optional)**: You can provide a video recording of the product for us to fully understand the functionality of the app.</span></span>
