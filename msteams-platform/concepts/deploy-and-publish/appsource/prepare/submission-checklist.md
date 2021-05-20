---
title: ストア送信を準備する
description: ストアに掲載するアプリを提出する前の最後の手順Microsoft Teams説明します。
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 975d3ef8fc8bdc8d6d7c336cf3a61a3a42ef5315
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566034"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a><span data-ttu-id="b2804-103">Microsoft Teams ストアの提出を準備する</span><span class="sxs-lookup"><span data-stu-id="b2804-103">Prepare your Microsoft Teams store submission</span></span>

<span data-ttu-id="b2804-104">Microsoft Teams アプリを設計、構築、およびテストしました。</span><span class="sxs-lookup"><span data-stu-id="b2804-104">You've designed, built, and tested your Microsoft Teams app.</span></span> <span data-ttu-id="b2804-105">これで、ユーザーがアプリを見つけて使い始めることができるように、リストする準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="b2804-105">Now you're ready to list it so people can discover and start using your app.</span></span>

<span data-ttu-id="b2804-106">[アプリをパートナー センター](/office/dev/store/use-partner-center-to-submit-to-appsource)に提出する前に、次の手順を実行していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="b2804-106">Before you submit your app to [Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource), make sure you've done the following.</span></span>

## <a name="validate-your-app-package"></a><span data-ttu-id="b2804-107">アプリ パッケージの検証</span><span class="sxs-lookup"><span data-stu-id="b2804-107">Validate your app package</span></span>

<span data-ttu-id="b2804-108">アプリがテスト環境で動作している場合は、アプリ パッケージをチェックして、申請プロセス中に問題が発生しないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2804-108">While your app may be working in a test environment, you should check your app package to avoid running into issues during the submission process.</span></span>

<span data-ttu-id="b2804-109">Microsoft Teams アプリ検証ツールを使用すると、パートナー センターに提出する前に問題を特定して修正できます。</span><span class="sxs-lookup"><span data-stu-id="b2804-109">The Microsoft Teams app validation tool helps you identify and fix issues before submitting to Partner Center.</span></span> <span data-ttu-id="b2804-110">このツールは、ストアの検証中に使用されたのと同じテスト ケースに対して、アプリの構成を自動的にチェックします。</span><span class="sxs-lookup"><span data-stu-id="b2804-110">The tool automatically checks your app's configurations against the same test cases used during store validation.</span></span>

1. <span data-ttu-id="b2804-111">[Microsoft Teams アプリ検証ツール](https://dev.teams.microsoft.com/appvalidation.html)に移動します。</span><span class="sxs-lookup"><span data-stu-id="b2804-111">Go to the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html).</span></span> <span data-ttu-id="b2804-112">(注:ツールは [、アプリケーションスタジオ](../../../build-and-test/app-studio-overview.md)でも利用可能です。</span><span class="sxs-lookup"><span data-stu-id="b2804-112">(Note: The tool is also available in [App Studio](../../../build-and-test/app-studio-overview.md).)</span></span>
1. <span data-ttu-id="b2804-113">アプリ パッケージをアップロードして、自動テストを実行します。</span><span class="sxs-lookup"><span data-stu-id="b2804-113">Upload your app package to run the automated tests.</span></span>
1. <span data-ttu-id="b2804-114">**予備チェックリスト** に移動し、自動化が困難なテスト ケースを確認します。</span><span class="sxs-lookup"><span data-stu-id="b2804-114">Go to the **Preliminary checklist** and review the test cases that are difficult to automate.</span></span>
1. <span data-ttu-id="b2804-115">自動テストでエラーが発生した場合や、チェックリストのすべての条件を満たしていない場合は、一般的に構成またはアプリの[問題を修正](~/resources/schema/manifest-schema.md)します。</span><span class="sxs-lookup"><span data-stu-id="b2804-115">[Fix issues with your configurations](~/resources/schema/manifest-schema.md) or app in general if the automated tests give you errors or you haven't met all the criteria in the checklist.</span></span>

## <a name="compile-testing-instructions"></a><span data-ttu-id="b2804-116">コンパイルテストの手順</span><span class="sxs-lookup"><span data-stu-id="b2804-116">Compile testing instructions</span></span>

<span data-ttu-id="b2804-117">レビュー担当者がアプリをテストするための手順とリソースを提供します。</span><span class="sxs-lookup"><span data-stu-id="b2804-117">Provide instructions and resources to help the reviewers test your app, including test accounts, credentials, and license keys.</span></span> <span data-ttu-id="b2804-118">パートナー センターで指示を追加するか、SharePointで一般に公開されている場所にアップロードできます。</span><span class="sxs-lookup"><span data-stu-id="b2804-118">You can add instructions in Partner Center or upload them to a publicly available location on SharePoint.</span></span>

### <a name="feature-list"></a><span data-ttu-id="b2804-119">機能一覧</span><span class="sxs-lookup"><span data-stu-id="b2804-119">Feature list</span></span>

<span data-ttu-id="b2804-120">アプリの機能の詳細については、Teamsと各機能をテストするための手順を説明します。</span><span class="sxs-lookup"><span data-stu-id="b2804-120">Provide details about your app's capabilities in Teams and steps for testing each one.</span></span>

### <a name="accounts"></a><span data-ttu-id="b2804-121">アカウント</span><span class="sxs-lookup"><span data-stu-id="b2804-121">Accounts</span></span>

<span data-ttu-id="b2804-122">アプリでライセンスまたはバックエンドのセーフリストが必要な場合は、テスト アカウントを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2804-122">You must provide test accounts if your app requires a license or backend safelisting.</span></span> <span data-ttu-id="b2804-123">テストを容易にするために、すべてのアカウントに事前入力データを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2804-123">All accounts you provide must include pre-populated data to facilitate testing.</span></span>

<span data-ttu-id="b2804-124">アプリの機能によっては、次のすべてを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2804-124">Depending on your app's features, you may need to provide all of the following:</span></span>

* <span data-ttu-id="b2804-125">管理者アカウント (必須)</span><span class="sxs-lookup"><span data-stu-id="b2804-125">Admin account (required)</span></span>
* <span data-ttu-id="b2804-126">管理者以外のアカウント (必須)</span><span class="sxs-lookup"><span data-stu-id="b2804-126">Non-admin account (required)</span></span>
* <span data-ttu-id="b2804-127">初回実行サインイン エクスペリエンスを適切にテストするために事前設定されていないアカウント (必須)</span><span class="sxs-lookup"><span data-stu-id="b2804-127">An account that isn't pre-configured in order to properly test the first-run sign-in experience (required)</span></span>
* <span data-ttu-id="b2804-128">プレミアムまたはアップグレードされた機能へのアクセス権を持つアカウント(該当する場合)</span><span class="sxs-lookup"><span data-stu-id="b2804-128">An account with access to premium or upgraded features (if applicable)</span></span>
* <span data-ttu-id="b2804-129">共有コンテキストで動作するアプリのコラボレーション エクスペリエンスをテストする同じテナント内の 2 つのアカウント (該当する場合)</span><span class="sxs-lookup"><span data-stu-id="b2804-129">Two accounts in the same tenant to test the collaboration experience for apps that work in shared contexts (if applicable)</span></span>

### <a name="tenant-configurations"></a><span data-ttu-id="b2804-130">テナント構成</span><span class="sxs-lookup"><span data-stu-id="b2804-130">Tenant configurations</span></span>

<span data-ttu-id="b2804-131">アプリを使用するようにTeamsテナントを構成する必要がある場合は、それらの手順と、検証用の管理者アカウントと管理者以外のアカウントを含めます。</span><span class="sxs-lookup"><span data-stu-id="b2804-131">If you must configure a Teams tenant to use your app, include those instructions and admin and non-admin accounts for validation.</span></span>

### <a name="video-optional"></a><span data-ttu-id="b2804-132">ビデオ (オプション)</span><span class="sxs-lookup"><span data-stu-id="b2804-132">Video (optional)</span></span>

<span data-ttu-id="b2804-133">Microsoft がアプリの機能を完全に理解できるように、アプリの記録を提供します。</span><span class="sxs-lookup"><span data-stu-id="b2804-133">Provide a recording of your app so that Microsoft can fully understand its functionality.</span></span>

## <a name="create-your-store-listing-details"></a><span data-ttu-id="b2804-134">ストア登録情報の詳細を作成する</span><span class="sxs-lookup"><span data-stu-id="b2804-134">Create your store listing details</span></span>

<span data-ttu-id="b2804-135">[パートナー センター](https://partner.microsoft.com)に送信する情報&#8212;、名前、説明、アイコン、およびイメージ&#8212;アプリのTeams ストアと Microsoft AppSource の一覧になります。</span><span class="sxs-lookup"><span data-stu-id="b2804-135">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="b2804-136">ストアの登録内容は、アプリの第一印象である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b2804-136">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="b2804-137">アプリのメリット、機能、ブランドを効果的に伝えるリストを使用して、インストールを増やします。</span><span class="sxs-lookup"><span data-stu-id="b2804-137">Increase installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

### <a name="specify-a-short-name"></a><span data-ttu-id="b2804-138">短い名前を指定してください</span><span class="sxs-lookup"><span data-stu-id="b2804-138">Specify a short name</span></span>

<span data-ttu-id="b2804-139">アプリの名前 (具体的には、 [*その短い名前*](~/resources/schema/manifest-schema.md#name)) は、ユーザーがストア内でそれを検出する方法で重要な役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="b2804-139">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="サンプル のスクリーンショットは、ストアの一覧にアプリの短い名前が表示される場所を示しています。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="b2804-141">短縮名が [ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name)に準拠していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="b2804-141">Make sure your short name adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name).</span></span>

### <a name="write-descriptions"></a><span data-ttu-id="b2804-142">説明を書く</span><span class="sxs-lookup"><span data-stu-id="b2804-142">Write descriptions</span></span>

<span data-ttu-id="b2804-143">アプリの短い説明と長い説明が必要です。</span><span class="sxs-lookup"><span data-stu-id="b2804-143">You must have a short and long description of your app.</span></span>

#### <a name="short-description"></a><span data-ttu-id="b2804-144">簡潔な説明</span><span class="sxs-lookup"><span data-stu-id="b2804-144">Short description</span></span>

<span data-ttu-id="b2804-145">ターゲットオーディエンスに対してオリジナルで魅力的で、指示するアプリの簡潔な概要。</span><span class="sxs-lookup"><span data-stu-id="b2804-145">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="b2804-146">短い説明は 1 文に保ちます。</span><span class="sxs-lookup"><span data-stu-id="b2804-146">Keep the short description to one sentence.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="サンプル のスクリーンショットは、ストアの一覧でアプリの簡単な説明が表示される場所を示しています。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="b2804-148">簡単な説明が [ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description)に準拠していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="b2804-148">Make sure your short description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description).</span></span>

#### <a name="long-description"></a><span data-ttu-id="b2804-149">詳しい説明</span><span class="sxs-lookup"><span data-stu-id="b2804-149">Long description</span></span>

<span data-ttu-id="b2804-150">詳しい説明は、アプリの主な機能、解決する問題、ターゲット ユーザーを強調する説明を提供します。</span><span class="sxs-lookup"><span data-stu-id="b2804-150">The long description can provide a narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="b2804-151">この説明は 4,000 文字まで可能ですが、ほとんどのユーザーは 300 ~ 500 語の間でのみ読み取ります。</span><span class="sxs-lookup"><span data-stu-id="b2804-151">While this description can be as long as 4,000 characters, most users will only read between 300-500 words.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="サンプル のスクリーンショットは、アプリの長い説明がストアの一覧に表示される場所を示しています。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="b2804-153">長い説明が [ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description)に準拠していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="b2804-153">Make sure your long description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description).</span></span>

### <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="b2804-154">アイコンのデザインガイドラインに従う</span><span class="sxs-lookup"><span data-stu-id="b2804-154">Adhere to icon design guidelines</span></span>

<span data-ttu-id="b2804-155">アイコンは、ストアを参照するときにユーザーが表示する主な要素の 1 つです。</span><span class="sxs-lookup"><span data-stu-id="b2804-155">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="b2804-156">アイコンは、アプリのブランドと目的を伝える一方で、Teams要件にも準拠する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2804-156">Your icons should communicate your app's brand and purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="b2804-157">詳細については、「アプリ[アイコンの作成に関するガイダンスTeams](~/concepts/build-and-test/apps-package.md#app-icons)参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2804-157">For more information, see [guidance on creating Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

### <a name="capture-screenshots"></a><span data-ttu-id="b2804-158">スクリーンショットをキャプチャする</span><span class="sxs-lookup"><span data-stu-id="b2804-158">Capture screenshots</span></span>

<span data-ttu-id="b2804-159">スクリーンショットは、アプリの名前、アイコン、説明を補完する、目立つ視覚的プレビューを提供します。</span><span class="sxs-lookup"><span data-stu-id="b2804-159">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="サンプル のスクリーンショットは、ストアの一覧でアプリのスクリーンショットが表示される場所を示しています。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="b2804-161">スクリーンショットについて次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="b2804-161">Remember the following about screenshots:</span></span>

* <span data-ttu-id="b2804-162">リストごとに最大 5 つのスクリーンショットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b2804-162">You can have up to five screenshots per listing.</span></span>
* <span data-ttu-id="b2804-163">サポートされるファイルの種類には、PNG、JPEG、GIF などがあります。</span><span class="sxs-lookup"><span data-stu-id="b2804-163">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="b2804-164">寸法は 1366x768 ピクセルにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2804-164">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="b2804-165">最大サイズは 1,024 KB です。</span><span class="sxs-lookup"><span data-stu-id="b2804-165">Maximum size of 1,024 KB.</span></span>

<span data-ttu-id="b2804-166">ベスト プラクティスについては、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2804-166">For best practices, see the following resources:</span></span>

* [<span data-ttu-id="b2804-167">ストア検証ガイドラインTeams</span><span class="sxs-lookup"><span data-stu-id="b2804-167">Teams store validation guidelines</span></span>](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#44-screenshots)
* [<span data-ttu-id="b2804-168">マイクロソフトのアプリ ストアの効果的な画像を作成する</span><span class="sxs-lookup"><span data-stu-id="b2804-168">Craft effective images for Microsoft app stores</span></span>](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a><span data-ttu-id="b2804-169">ビデオを作成する</span><span class="sxs-lookup"><span data-stu-id="b2804-169">Create a video</span></span>

<span data-ttu-id="b2804-170">リスト内のビデオは、ユーザーがアプリを使用する理由を伝える最も効果的な方法です。</span><span class="sxs-lookup"><span data-stu-id="b2804-170">A video in your listing can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="b2804-171">ビデオでは、次の質問に対処する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2804-171">You should address the following questions in a video:</span></span>

* <span data-ttu-id="b2804-172">アプリはWhoですか?</span><span class="sxs-lookup"><span data-stu-id="b2804-172">Who is your app for?</span></span>
* <span data-ttu-id="b2804-173">アプリで解決できる問題は何ですか。</span><span class="sxs-lookup"><span data-stu-id="b2804-173">What problems can your app solve?</span></span>
* <span data-ttu-id="b2804-174">アプリの動作方法</span><span class="sxs-lookup"><span data-stu-id="b2804-174">How does your app work?</span></span>
* <span data-ttu-id="b2804-175">アプリを使用すると、他にどのようなメリットがありますか?</span><span class="sxs-lookup"><span data-stu-id="b2804-175">What other benefits do you get from using your app?</span></span>

#### <a name="best-practices-for-videos"></a><span data-ttu-id="b2804-176">ビデオのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="b2804-176">Best practices for videos</span></span>

* <span data-ttu-id="b2804-177">30~90秒の間で動画を保存します。</span><span class="sxs-lookup"><span data-stu-id="b2804-177">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="b2804-178">品質を目指す。</span><span class="sxs-lookup"><span data-stu-id="b2804-178">Aim for quality.</span></span> <span data-ttu-id="b2804-179">リストでは、スクリーンショットの前にユーザーにビデオが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b2804-179">In a listing, users will see your video before screenshots.</span></span>

### <a name="select-a-category-for-your-app"></a><span data-ttu-id="b2804-180">アプリのカテゴリを選択する</span><span class="sxs-lookup"><span data-stu-id="b2804-180">Select a category for your app</span></span>

<span data-ttu-id="b2804-181">申請中に、アプリを分類するように求められます。</span><span class="sxs-lookup"><span data-stu-id="b2804-181">During submission, you're asked to categorize your app.</span></span> <span data-ttu-id="b2804-182">次の表は、ストア カテゴリTeams パートナー[センター](https://aka.ms/PartnerCenterHomePage)に一覧表示されるカテゴリに対応付けます。</span><span class="sxs-lookup"><span data-stu-id="b2804-182">The following table maps Teams store categories to the categories listed in [Partner Center](https://aka.ms/PartnerCenterHomePage).</span></span>

| <span data-ttu-id="b2804-183">Teamsカテゴリ</span><span class="sxs-lookup"><span data-stu-id="b2804-183">Teams categories</span></span>       | <span data-ttu-id="b2804-184">パートナー センターのカテゴリ</span><span class="sxs-lookup"><span data-stu-id="b2804-184">Partner Center categories</span></span>  |
|:---------------------|:---------------|
| <span data-ttu-id="b2804-185">分析と BI</span><span class="sxs-lookup"><span data-stu-id="b2804-185">Analytics and BI</span></span> | <span data-ttu-id="b2804-186">分析、データ可視化、BI</span><span class="sxs-lookup"><span data-stu-id="b2804-186">Analytics, Data Visualization and BI</span></span> |
| <span data-ttu-id="b2804-187">開発者と IT</span><span class="sxs-lookup"><span data-stu-id="b2804-187">Developer and IT</span></span> | <span data-ttu-id="b2804-188">開発者ツール、 IT 管理者</span><span class="sxs-lookup"><span data-stu-id="b2804-188">Developer Tools, IT Admin</span></span> |
| <span data-ttu-id="b2804-189">教育</span><span class="sxs-lookup"><span data-stu-id="b2804-189">Education</span></span> | <span data-ttu-id="b2804-190">教育</span><span class="sxs-lookup"><span data-stu-id="b2804-190">Education</span></span> |
| <span data-ttu-id="b2804-191">人事管理</span><span class="sxs-lookup"><span data-stu-id="b2804-191">Human resources</span></span> | <span data-ttu-id="b2804-192">人材・人材採用</span><span class="sxs-lookup"><span data-stu-id="b2804-192">Human Resources and Recruiting</span></span> |
| <span data-ttu-id="b2804-193">生産性</span><span class="sxs-lookup"><span data-stu-id="b2804-193">Productivity</span></span> | <span data-ttu-id="b2804-194">コンテンツ管理、ファイルとドキュメント、生産性、トレーニングとチュートリアル、およびユーティリティ</span><span class="sxs-lookup"><span data-stu-id="b2804-194">Content Management, Files and documents, Productivity, Training and Tutorials, and Utilities</span></span> |
| <span data-ttu-id="b2804-195">プロジェクト管理</span><span class="sxs-lookup"><span data-stu-id="b2804-195">Project management</span></span> | <span data-ttu-id="b2804-196">コミュニケーション、Project管理、ワークフロー、およびビジネス管理</span><span class="sxs-lookup"><span data-stu-id="b2804-196">Communication, Project Management, Workflow, and Business Management</span></span> |
| <span data-ttu-id="b2804-197">販売とサポート</span><span class="sxs-lookup"><span data-stu-id="b2804-197">Sales and support</span></span> | <span data-ttu-id="b2804-198">顧客と連絡先の管理、カスタマーサポート、財務管理、販売およびマーケティング</span><span class="sxs-lookup"><span data-stu-id="b2804-198">Customer and Contact Management, Customer Support, Financial Management, Sales and Marketing</span></span> |
| <span data-ttu-id="b2804-199">社会的で楽しい</span><span class="sxs-lookup"><span data-stu-id="b2804-199">Social and fun</span></span> | <span data-ttu-id="b2804-200">画像ギャラリーとビデオギャラリー、ライフスタイル、ニュースと天気、ソーシャル、旅行、ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="b2804-200">Image and Video Galleries, Lifestyle, News and Weather, Social, Travel, and Navigation</span></span> |

### <a name="localize-your-store-listing"></a><span data-ttu-id="b2804-201">店舗登録情報のローカライズ</span><span class="sxs-lookup"><span data-stu-id="b2804-201">Localize your store listing</span></span>

<span data-ttu-id="b2804-202">パートナー センターでは [、ローカライズされたストア の一覧をサポートしています](/office/dev/store/prepare-localized-solutions)。</span><span class="sxs-lookup"><span data-stu-id="b2804-202">Partner Center supports [localized store listings](/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="b2804-203">詳細については、「 [Teams アプリの一覧をローカライズする方法](../../../../concepts/build-and-test/apps-localization.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2804-203">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="complete-publisher-verification"></a><span data-ttu-id="b2804-204">Publisher検証の完了</span><span class="sxs-lookup"><span data-stu-id="b2804-204">Complete Publisher Verification</span></span>

<span data-ttu-id="b2804-205">[ストア](/azure/active-directory/develop/publisher-verification-overview)に一覧表示されているアプリTeams Publisher確認が必要です。</span><span class="sxs-lookup"><span data-stu-id="b2804-205">[Publisher Verification](/azure/active-directory/develop/publisher-verification-overview) is required for Teams apps listed in the store.</span></span> <span data-ttu-id="b2804-206">詳細については、「 [よく寄せられる質問](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)」、パブリッシャー [検証済みとしてアプリをマークする方法](/azure/active-directory/develop/mark-app-as-publisher-verified)、および [発行元の検証のトラブルシューティング](/azure/active-directory/develop/troubleshoot-publisher-verification)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2804-206">For more information, see [frequently asked questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [how to mark your app as publisher verified](/azure/active-directory/develop/mark-app-as-publisher-verified), and [troubleshoot publisher verification](/azure/active-directory/develop/troubleshoot-publisher-verification).</span></span>

## <a name="complete-publisher-attestation"></a><span data-ttu-id="b2804-207">完全なPublisher構成証明</span><span class="sxs-lookup"><span data-stu-id="b2804-207">Complete Publisher Attestation</span></span>

<span data-ttu-id="b2804-208">[Publisher構成証明](/microsoft-365-app-certification/docs/attestation)は、ストアに登録されているTeamsアプリにも必要です。</span><span class="sxs-lookup"><span data-stu-id="b2804-208">[Publisher Attestation](/microsoft-365-app-certification/docs/attestation) is also required for Teams apps listed in the store.</span></span> <span data-ttu-id="b2804-209">このプロセスには、アプリのセキュリティ、データ処理、コンプライアンスの実践に関する自己評価が含まれており、潜在的な顧客がアプリの使用に関する情報に基づいた意思決定を行う際に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="b2804-209">The process includes completing a self-assessment of your app's security, data handling, and compliance practices that can help potential customers make informed decisions about using your app.</span></span>

> [!NOTE]
> <span data-ttu-id="b2804-210">新しいアプリを申請する場合、アプリがTeams ストアに表示されるまで、Publisher構成証明を正式に完了することはできません。</span><span class="sxs-lookup"><span data-stu-id="b2804-210">If you're submitting a new app, you can't officially complete Publisher Attestation until your app is listed on the Teams store.</span></span> <span data-ttu-id="b2804-211">一覧に表示されているアプリを更新する場合は、検証のためにアプリの最新バージョンを提出する前に、Publisher構成証明を完了します。</span><span class="sxs-lookup"><span data-stu-id="b2804-211">If you're updating a listed app, complete Publisher Attestation before you submit the latest version of the app for validation.</span></span>

## <a name="next-step"></a><span data-ttu-id="b2804-212">次の手順</span><span class="sxs-lookup"><span data-stu-id="b2804-212">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b2804-213">アプリを送信する</span><span class="sxs-lookup"><span data-stu-id="b2804-213">Submit your app</span></span>](/office/dev/store/add-in-submission-guide)
