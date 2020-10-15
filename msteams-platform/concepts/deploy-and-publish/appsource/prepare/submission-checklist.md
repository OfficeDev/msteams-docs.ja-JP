---
title: 提出のチェックリスト
description: Microsoft Teams アプリを AppSource に公開する前に使用するチェックリスト
keywords: teams 発行ストア office 発行チェックリスト Teams Teams アプリアプリソースの検証
ms.openlocfilehash: 4bbf5adb8594db0f7163db610b192dd8aaec37fb
ms.sourcegitcommit: 25afe104d10c9a6a2849decf5ec1d08969d827c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "48465923"
---
# <a name="prepare-for-appsource-submission"></a><span data-ttu-id="f96be-104">AppSource 提出の準備</span><span class="sxs-lookup"><span data-stu-id="f96be-104">Prepare for AppSource submission</span></span>  

<span data-ttu-id="f96be-105">AppSource にリストされるようにするには、アプリが承認プロセスを経る必要があります。</span><span class="sxs-lookup"><span data-stu-id="f96be-105">To be listed on AppSource, your app must go through an approval process.</span></span> <span data-ttu-id="f96be-106">これは Microsoft Teams グループによって提供される無料のサービスで、アプリが説明どおりに動作することを確認し、適切なメタデータをすべて含み、エンドユーザーにとって有益なコンテンツを提供します。</span><span class="sxs-lookup"><span data-stu-id="f96be-106">This is a free service provided by the Microsoft Teams group that verifies that your app works as described, contains all appropriate metadata, and provides content that would be valuable to an end user.</span></span> <span data-ttu-id="f96be-107">迅速な承認を得るために、アプリが以下の要件とガイドラインを満たしていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="f96be-107">To help you achieve rapid approval, ensure your app meets the following requirements and guidelines:</span></span>

* <span data-ttu-id="f96be-108">**Distribution メソッド:** アプリがストアプラットフォームで公開されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="f96be-108">**Distribution method:** Make sure your app is meant for publication on a store platform.</span></span> <span data-ttu-id="f96be-109">AppSource に発行せずにアプリを配布するため [のその他のオプション](../../overview.md) があります。</span><span class="sxs-lookup"><span data-stu-id="f96be-109">There are [other options](../../overview.md) to distribute your app without publishing to AppSource.</span></span>
* <span data-ttu-id="f96be-110">**検証ポリシー:** アプリは、現在のすべての [Appsource 検証ポリシー](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams)に合格する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f96be-110">**Validation policies:** Your app must pass all current [AppSource validation policies](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams).</span></span> <span data-ttu-id="f96be-111">提出する前に [検証ツール](#teams-app-validation-tool) に対してアプリをチェックしてください。</span><span class="sxs-lookup"><span data-stu-id="f96be-111">Check your app against the [validation tool](#teams-app-validation-tool) before submission.</span></span> <span data-ttu-id="f96be-112">これらのポリシーは変更される可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f96be-112">Please note that these policies are subject to change.</span></span>
* <span data-ttu-id="f96be-113">**アプリの詳細ページ:** アプリは、  [アプリの詳細ページチェックリスト](detail-page-checklist.md)と連携する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f96be-113">**App detail page:** Your app must align with the  [App detail page checklist](detail-page-checklist.md).</span></span>
* <span data-ttu-id="f96be-114">**ヒントとよく発生するケース:** リストされている [ヒントおよび頻繁に失敗するケース](frequently-failed-cases.md)  に、アプリの提出と承認の時間を向上させるために、さらに注意を払ってください。</span><span class="sxs-lookup"><span data-stu-id="f96be-114">**Tips and frequently failed cases:** Pay extra attention to the listed [Tips and frequently failed cases](frequently-failed-cases.md)  to improve your app submission and approval time.</span></span>
* <span data-ttu-id="f96be-115">**アプリマニフェスト:** アプリのマニフェストをアプリの [マニフェストチェックリスト](app-manifest-checklist.md)に照らして確認します。</span><span class="sxs-lookup"><span data-stu-id="f96be-115">**App manifest:** Check your app manifest against the [App manifest checklist](app-manifest-checklist.md).</span></span>
* <span data-ttu-id="f96be-116">**テストとデバッグ:** アプリを完全に [テストおよびデバッグ](../../../build-and-test/debug.md)していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="f96be-116">**Testing and debugging:** Make certain that you have fully [tested and debugged your app](../../../build-and-test/debug.md).</span></span>
* <span data-ttu-id="f96be-117">**メモのテスト:**[検証のためのテストメモを](#test-notes-for-validation)含める</span><span class="sxs-lookup"><span data-stu-id="f96be-117">**Testing notes:** Include your [test notes for validation](#test-notes-for-validation)</span></span>
* <span data-ttu-id="f96be-118">**プライバシーポリシー:**[プライバシーポリシー、使用条件、サポート url の](#privacy-policy-terms-of-use-and-support-urls)ガイドラインに従っていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f96be-118">**Privacy policies:** Ensure your [privacy policy, terms of use and support URLs](#privacy-policy-terms-of-use-and-support-urls) follow our guidelines.</span></span>

<span data-ttu-id="f96be-119">上記のすべての要件を完了したら、 [パートナーセンター](/office/dev/store/use-partner-center-to-submit-to-appsource)を使用してパッケージを appsource に提出します。</span><span class="sxs-lookup"><span data-stu-id="f96be-119">Once you have completed all of the above requirements, submit your package to AppSource through [Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource).</span></span>

## <a name="teams-app-validation-tool"></a><span data-ttu-id="f96be-120">Teams アプリ検証ツール</span><span class="sxs-lookup"><span data-stu-id="f96be-120">Teams App Validation Tool</span></span>

<span data-ttu-id="f96be-121">アプリ検証ツールは、 [アプリ検証](#teams-app-validator) ツールと [事前チェックリスト](#preliminary-checklist)で構成されています。</span><span class="sxs-lookup"><span data-stu-id="f96be-121">The app validation tool consists of an [app validator](#teams-app-validator) and a [preliminary checklist](#preliminary-checklist).</span></span> <span data-ttu-id="f96be-122">このツールは、 [Appsource](/office/dev/store/submit-to-appsource-via-partner-center) で使用されているものと同じテストケースをレプリケートして、アプリの送信を評価します。</span><span class="sxs-lookup"><span data-stu-id="f96be-122">The tool replicates the same test cases used by [AppSource](/office/dev/store/submit-to-appsource-via-partner-center) to evaluate your app submission.</span></span> <span data-ttu-id="f96be-123">したがって、承認のためにソリューションを AppSource に提出する前に、すべてのテストケースに合格することが重要です。このツールは Teams プラットフォーム内のいくつかの領域にあります。</span><span class="sxs-lookup"><span data-stu-id="f96be-123">Therefore,  it's crucial to pass all the test cases prior to submitting your solution to AppSource for approval.The tool can be found in several areas within the Teams platform:</span></span>

> [!div class="checklist"]
>
> * [<span data-ttu-id="f96be-124">**アプリの検証のホームページ**</span><span class="sxs-lookup"><span data-stu-id="f96be-124">**App Validator homepage**</span></span>](https://dev.teams.microsoft.com/appvalidation.html)
> * [<span data-ttu-id="f96be-125">**Teams Visual Studio Code toolkit**</span><span class="sxs-lookup"><span data-stu-id="f96be-125">**Teams Visual Studio Code toolkit**</span></span>](/toolkit/visual-studio-code-overview.md)
> * [<span data-ttu-id="f96be-126">**App Studio**</span><span class="sxs-lookup"><span data-stu-id="f96be-126">**App Studio**</span></span>](/concepts/build-and-test/app-studio-overview.md)

### <a name="teams-app-validator"></a><span data-ttu-id="f96be-127">Teams アプリの検証</span><span class="sxs-lookup"><span data-stu-id="f96be-127">Teams app validator</span></span>

<span data-ttu-id="f96be-128">[ **検証** ] ページでは、appsource に提出する前にアプリパッケージを確認できます。</span><span class="sxs-lookup"><span data-stu-id="f96be-128">The **Validate** page allows you to check your app package before submission to AppSource.</span></span> <span data-ttu-id="f96be-129">アプリパッケージをアップロードすると、検証ツールは、すべてのマニフェスト関連のテストケースに対してアプリをチェックします。</span><span class="sxs-lookup"><span data-stu-id="f96be-129">Simply upload your app package and the validation tool will check your app against all manifest-related test cases.</span></span> <span data-ttu-id="f96be-130">失敗した各テストの説明には、エラーを解決するためのドキュメントリンクが記載されています。</span><span class="sxs-lookup"><span data-stu-id="f96be-130">For each failed test, the description provides a documentation link to help you fix the error.</span></span>

![検証ツール](../../../../assets/images/validation-tool/validator.png)

### <a name="preliminary-checklist"></a><span data-ttu-id="f96be-132">事前チェックリスト</span><span class="sxs-lookup"><span data-stu-id="f96be-132">Preliminary checklist</span></span>

<span data-ttu-id="f96be-133">自動化が困難なテストシナリオでは、最も一般的に失敗しているテストケースの7つの事前チェックリストがあります。</span><span class="sxs-lookup"><span data-stu-id="f96be-133">For test scenarios that are difficult to automate, the preliminary checklist surfaces seven of the most commonly failed test cases.</span></span>

![事前チェックリスト](../../../../assets/images/validation-tool/preliminary-checklist.png)

## <a name="privacy-policy-terms-of-use-and-support-urls"></a><span data-ttu-id="f96be-135">プライバシーポリシー、使用条件、およびサポート Url</span><span class="sxs-lookup"><span data-stu-id="f96be-135">Privacy policy, terms of use and support URLs</span></span>

### <a name="privacy-policy"></a><span data-ttu-id="f96be-136">プライバシーポリシー</span><span class="sxs-lookup"><span data-stu-id="f96be-136">Privacy policy</span></span>

<span data-ttu-id="f96be-137">プライバシーポリシーのガイドライン:</span><span class="sxs-lookup"><span data-stu-id="f96be-137">Privacy policy guidelines:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="f96be-138">プライバシーポリシーは、アプリや、すべてのサービスの全体的なポリシーに固有のものにすることができます。</span><span class="sxs-lookup"><span data-stu-id="f96be-138">The privacy policy can be specific to your app and/or an overall policy for all of your services.</span></span>
> * <span data-ttu-id="f96be-139">汎用プライバシーポリシーを使用する場合は、「サービス」、「アプリケーション」、および「プラットフォーム」を参照して、自分の web サイトだけでなく、Teams アプリを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f96be-139">If you use a generic privacy policy, it must reference "services", "applications", and "platforms" to include your Teams app as well as your website.</span></span>
> * <span data-ttu-id="f96be-140">ユーザーデータストレージ、ユーザーデータの保存、削除、およびセキュリティ制御の処理方法を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f96be-140">It must include how you handle user data storage, user data retention, deletion, and security controls.</span></span>
> * <span data-ttu-id="f96be-141">連絡先情報を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="f96be-141">It must include your contact information.</span></span>
> * <span data-ttu-id="f96be-142">壊れたリンク、ベータ版 Url、またはステージング Url を含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="f96be-142">It should not contain broken links, beta URLs, or staging URLs.</span></span>

### <a name="terms-of-use"></a><span data-ttu-id="f96be-143">利用規約</span><span class="sxs-lookup"><span data-stu-id="f96be-143">Terms of use</span></span>

<span data-ttu-id="f96be-144">使用条件ステートメントは、アプリまたはアドインオファーリングに固有であり、適用される必要があります。</span><span class="sxs-lookup"><span data-stu-id="f96be-144">Your terms of use statement should be specific and applicable to your app and/or add-in offering.</span></span>

### <a name="support-urls"></a><span data-ttu-id="f96be-145">サポート Url</span><span class="sxs-lookup"><span data-stu-id="f96be-145">Support URLs</span></span>

<span data-ttu-id="f96be-146">アプリの問題については、サポート Url で認証やログイン資格情報を要求する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f96be-146">Your support URLs should not require authentication or login credential to contact you for any issues with your app.</span></span>

## <a name="test-notes-for-validation"></a><span data-ttu-id="f96be-147">検証のためのテストメモ</span><span class="sxs-lookup"><span data-stu-id="f96be-147">Test notes for validation</span></span>

<span data-ttu-id="f96be-148">以下を含めるようにしてください。</span><span class="sxs-lookup"><span data-stu-id="f96be-148">Please include the following:</span></span>

* <span data-ttu-id="f96be-149">少なくとも2つのログイン資格情報、1人の管理者、および1つの非管理者を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f96be-149">You must provide at least two login credentials, one admin and one non-admin.</span></span>

* <span data-ttu-id="f96be-150">確認のため、提供するアカウントには事前に十分なデータが事前に設定されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f96be-150">For verification purposes, the accounts you provide should have sufficient pre-populated data.</span></span>

* <span data-ttu-id="f96be-151">エンタープライズアプリ、サブスクリプションが必要なアプリ、または Office 365 テナント/ドメインの依存関係があるアプリについては、アプリが事前に構成されていないドメインで3番目のアカウントを指定する必要があります。これにより、初回実行のユーザー環境を検証することができます。</span><span class="sxs-lookup"><span data-stu-id="f96be-151">For enterprise apps, apps where a subscription is required, or apps where there is an Office 365 tenant/domain dependency, you must provide a third account in the same domain that is not pre-configured for your app so that we can validate the first-run user experience.</span></span>

* <span data-ttu-id="f96be-152">アプリにプレミアム/アップグレード機能がある場合は、その機能をテストするために必要なアクセス権を持つアカウントを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f96be-152">If your app has premium/upgraded features, an account with the necessary access must be provided to test that experience.</span></span>

* <span data-ttu-id="f96be-153">テストメモは、SharePoint にアップロードすることを選択できます。</span><span class="sxs-lookup"><span data-stu-id="f96be-153">You may choose to upload your test notes to SharePoint.</span></span> <span data-ttu-id="f96be-154">その場合は、ファイルへのパブリックリンクを提供してください。</span><span class="sxs-lookup"><span data-stu-id="f96be-154">If so, please provide a public link to the file.</span></span>

* <span data-ttu-id="f96be-155">**アカウントをテスト**します。</span><span class="sxs-lookup"><span data-stu-id="f96be-155">**Test Accounts**.</span></span> <span data-ttu-id="f96be-156">アプリがバックエンドからライセンスアカウントまたは安全なライセンスのみを許可する場合は、テストアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="f96be-156">A test account is required if your app only allows licensed accounts or safelisting from the backend.</span></span> <span data-ttu-id="f96be-157">また、アプリで許可されているチーム/グループのチャットスコープがある場合は、チームのグループ作業のシナリオを検証するために、同じテナント内の2つのテストアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="f96be-157">Also, if there is a team/group chat scope allowed in your app,  two test accounts in the same tenant are required to validate the team collaboration scenario.</span></span>

* <span data-ttu-id="f96be-158">**統合手順**。</span><span class="sxs-lookup"><span data-stu-id="f96be-158">**Integration steps**.</span></span> <span data-ttu-id="f96be-159">アプリを使用するためにテナント管理者が事前構成する必要がある場合は、この手順を実行するか、検証のために構成された管理者と管理者以外のアカウントを指定してください。</span><span class="sxs-lookup"><span data-stu-id="f96be-159">If pre-configuration by a tenant admin is required to use the app, include the steps and/or provide configured admin and non-admin accounts for validation.</span></span> <span data-ttu-id="f96be-160">注: [Office 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) サブスクリプションにサインアップできます。</span><span class="sxs-lookup"><span data-stu-id="f96be-160">Note: you can sign up for an [Office 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="f96be-161">これは90日間 *無料* で、開発アクティビティに使用している間は継続的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="f96be-161">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span>

* <span data-ttu-id="f96be-162">**Teams のアプリ機能に関するメモ**: teams 内でアプリが提供するすべての機能の詳細を確認し、各機能をテストするための手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="f96be-162">**Notes regarding the app features in Teams**: Detail all of the capabilities the app offers within Teams and steps for testing each feature.</span></span>

* <span data-ttu-id="f96be-163">**アプリの機能を示すビデオ (オプション)**: アプリの機能を完全に理解するために、製品のビデオ録画を提供することができます。</span><span class="sxs-lookup"><span data-stu-id="f96be-163">**Video showing the app functionality (Optional)**: You can provide a video recording of the product for us to fully understand the functionality of the app.</span></span>
