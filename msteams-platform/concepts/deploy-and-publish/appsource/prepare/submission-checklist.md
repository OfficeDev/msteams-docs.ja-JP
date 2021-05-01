---
title: ストア申請の準備
description: ストアに一覧表示するアプリをMicrosoft Teamsする前の最後の手順について説明します。
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: d46d21c3d984b5688c00857e485210b0f0fcf2c7
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101682"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a><span data-ttu-id="51812-103">ストア申請Microsoft Teams準備する</span><span class="sxs-lookup"><span data-stu-id="51812-103">Prepare your Microsoft Teams store submission</span></span>

<span data-ttu-id="51812-104">アプリの設計、構築、テストMicrosoft Teamsしました。</span><span class="sxs-lookup"><span data-stu-id="51812-104">You've designed, built, and tested your Microsoft Teams app.</span></span> <span data-ttu-id="51812-105">これで、ユーザーがアプリを検出して使用を開始できるよう、リストを作成する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="51812-105">Now you're ready to list it so people can discover and start using your app.</span></span>

<span data-ttu-id="51812-106">アプリをパートナー センターに [提出する前](/office/dev/store/use-partner-center-to-submit-to-appsource)に、次の手順を実行してください。</span><span class="sxs-lookup"><span data-stu-id="51812-106">Before you submit your app to [Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource), make sure you've done the following.</span></span>

## <a name="validate-your-app-package"></a><span data-ttu-id="51812-107">アプリ パッケージの検証</span><span class="sxs-lookup"><span data-stu-id="51812-107">Validate your app package</span></span>

<span data-ttu-id="51812-108">アプリがテスト環境で動作している場合は、申請プロセス中に問題が発生しないようにアプリ パッケージを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="51812-108">While your app may be working in a test environment, you should check your app package to avoid running into issues during the submission process.</span></span>

<span data-ttu-id="51812-109">アプリMicrosoft Teamsツールを使用すると、パートナー センターに提出する前に問題を特定して修正できます。</span><span class="sxs-lookup"><span data-stu-id="51812-109">The Microsoft Teams app validation tool helps you identify and fix issues before submitting to Partner Center.</span></span> <span data-ttu-id="51812-110">このツールは、ストアの検証中に使用したのと同じテスト ケースに対して、アプリの構成を自動的にチェックします。</span><span class="sxs-lookup"><span data-stu-id="51812-110">The tool automatically checks your app's configurations against the same test cases used during store validation.</span></span>

1. <span data-ttu-id="51812-111">アプリ検証ツール[Microsoft Teamsに移動します](https://dev.teams.microsoft.com/appvalidation.html)。</span><span class="sxs-lookup"><span data-stu-id="51812-111">Go to the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html).</span></span> <span data-ttu-id="51812-112">(注: このツールは App [Studio でも使用](../../../build-and-test/app-studio-overview.md)できます。)</span><span class="sxs-lookup"><span data-stu-id="51812-112">(Note: The tool is also available in [App Studio](../../../build-and-test/app-studio-overview.md).)</span></span>
1. <span data-ttu-id="51812-113">アップロードテストを実行するには、アプリ パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="51812-113">Upload your app package to run the automated tests.</span></span>
1. <span data-ttu-id="51812-114">[予備チェックリスト] **に移動し** 、自動化が困難なテスト ケースを確認します。</span><span class="sxs-lookup"><span data-stu-id="51812-114">Go to the **Preliminary checklist** and review the test cases that are difficult to automate.</span></span>
1. <span data-ttu-id="51812-115">[自動テストでエラーが](~/resources/schema/manifest-schema.md) 発生したり、チェックリストのすべての条件を満たしていない場合は、構成やアプリの一般的な問題を修正します。</span><span class="sxs-lookup"><span data-stu-id="51812-115">[Fix issues with your configurations](~/resources/schema/manifest-schema.md) or app in general if the automated tests give you errors or you haven't met all the criteria in the checklist.</span></span>

## <a name="compile-testing-instructions"></a><span data-ttu-id="51812-116">テスト手順のコンパイル</span><span class="sxs-lookup"><span data-stu-id="51812-116">Compile testing instructions</span></span>

<span data-ttu-id="51812-117">テスト アカウント、資格情報、ライセンス キーなど、レビュー担当者がアプリをテストするのに役立つ手順とリソースを提供します。</span><span class="sxs-lookup"><span data-stu-id="51812-117">Provide instructions and resources to help the reviewers test your app, including test accounts, credentials, and license keys.</span></span> <span data-ttu-id="51812-118">手順は、パートナー センターに追加するか、一般に公開されている場所にアップロードSharePoint。</span><span class="sxs-lookup"><span data-stu-id="51812-118">You can add instructions in Partner Center or upload them to a publicly available location on SharePoint.</span></span>

### <a name="feature-list"></a><span data-ttu-id="51812-119">機能一覧</span><span class="sxs-lookup"><span data-stu-id="51812-119">Feature list</span></span>

<span data-ttu-id="51812-120">アプリの機能に関する詳細な情報を、Teamsテストする手順を示します。</span><span class="sxs-lookup"><span data-stu-id="51812-120">Provide details about your app's capabilities in Teams and steps for testing each one.</span></span>

### <a name="accounts"></a><span data-ttu-id="51812-121">アカウント</span><span class="sxs-lookup"><span data-stu-id="51812-121">Accounts</span></span>

<span data-ttu-id="51812-122">アプリでライセンスまたはバックエンドセーフリストが必要な場合は、テスト アカウントを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="51812-122">You must provide test accounts if your app requires a license or backend safelisting.</span></span> <span data-ttu-id="51812-123">テストを容易にするために、すべてのアカウントに事前入力されたデータが含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="51812-123">All accounts you provide must include pre-populated data to facilitate testing.</span></span>

<span data-ttu-id="51812-124">アプリの機能によっては、以下の情報を提供する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="51812-124">Depending on your app's features, you may need to provide all of the following:</span></span>

* <span data-ttu-id="51812-125">管理者アカウント (必須)</span><span class="sxs-lookup"><span data-stu-id="51812-125">Admin account (required)</span></span>
* <span data-ttu-id="51812-126">管理者以外のアカウント (必須)</span><span class="sxs-lookup"><span data-stu-id="51812-126">Non-admin account (required)</span></span>
* <span data-ttu-id="51812-127">最初の実行サインイン エクスペリエンスを適切にテストするために事前構成されていないアカウント (必須)</span><span class="sxs-lookup"><span data-stu-id="51812-127">An account that isn't pre-configured in order to properly test the first-run sign-in experience (required)</span></span>
* <span data-ttu-id="51812-128">プレミアム機能またはアップグレードされた機能にアクセスできるアカウント (該当する場合)</span><span class="sxs-lookup"><span data-stu-id="51812-128">An account with access to premium or upgraded features (if applicable)</span></span>
* <span data-ttu-id="51812-129">共有コンテキストで動作するアプリのコラボレーション エクスペリエンスをテストする同じテナント内の 2 つのアカウント (該当する場合)</span><span class="sxs-lookup"><span data-stu-id="51812-129">Two accounts in the same tenant to test the collaboration experience for apps that work in shared contexts (if applicable)</span></span>

### <a name="tenant-configurations"></a><span data-ttu-id="51812-130">テナント構成</span><span class="sxs-lookup"><span data-stu-id="51812-130">Tenant configurations</span></span>

<span data-ttu-id="51812-131">アプリを使用する Teamsテナントを構成する必要がある場合は、検証のためにこれらの手順と管理者アカウントと管理者以外のアカウントを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="51812-131">If you must configure a Teams tenant to use your app, include those instructions and admin and non-admin accounts for validation.</span></span>

### <a name="video-optional"></a><span data-ttu-id="51812-132">ビデオ (オプション)</span><span class="sxs-lookup"><span data-stu-id="51812-132">Video (optional)</span></span>

<span data-ttu-id="51812-133">Microsoft が機能を完全に理解できるよう、アプリの記録を提供します。</span><span class="sxs-lookup"><span data-stu-id="51812-133">Provide a recording of your app so that Microsoft can fully understand its functionality.</span></span>

## <a name="create-your-store-listing-details"></a><span data-ttu-id="51812-134">ストア登録情報の詳細を作成する</span><span class="sxs-lookup"><span data-stu-id="51812-134">Create your store listing details</span></span>

<span data-ttu-id="51812-135">パートナー センター&#8212;[](https://partner.microsoft.com)に送信する情報 (名前、説明、アイコン、画像など)&#8212;は、Teams ストアとアプリの Microsoft AppSource リストになります。</span><span class="sxs-lookup"><span data-stu-id="51812-135">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="51812-136">ストアの登録情報は、アプリの第一印象である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="51812-136">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="51812-137">アプリの利点、機能、ブランドを効果的に伝えるリストを使用してインストールを増やします。</span><span class="sxs-lookup"><span data-stu-id="51812-137">Increase installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

### <a name="specify-a-short-name"></a><span data-ttu-id="51812-138">短い名前を指定する</span><span class="sxs-lookup"><span data-stu-id="51812-138">Specify a short name</span></span>

<span data-ttu-id="51812-139">アプリの名前 (具体的には短い名前 [*)*](~/resources/schema/manifest-schema.md#name)は、ユーザーがストアでアプリを検出する方法において重要な役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="51812-139">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="スクリーンショットの例は、アプリの短い名前がストアの登録情報に表示される場所を強調表示します。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="51812-141">短い名前がストアの検証ガイドラインに [準拠している必要があります](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name)。</span><span class="sxs-lookup"><span data-stu-id="51812-141">Make sure your short name adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name).</span></span>

### <a name="write-descriptions"></a><span data-ttu-id="51812-142">説明の書き込み</span><span class="sxs-lookup"><span data-stu-id="51812-142">Write descriptions</span></span>

<span data-ttu-id="51812-143">アプリの短い説明と長い説明が必要です。</span><span class="sxs-lookup"><span data-stu-id="51812-143">You must have a short and long description of your app.</span></span>

#### <a name="short-description"></a><span data-ttu-id="51812-144">簡潔な説明</span><span class="sxs-lookup"><span data-stu-id="51812-144">Short description</span></span>

<span data-ttu-id="51812-145">対象ユーザーに対して、元の、魅力的で、指示する必要があるアプリの簡潔な概要。</span><span class="sxs-lookup"><span data-stu-id="51812-145">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="51812-146">短い説明を 1 つの文に保つ。</span><span class="sxs-lookup"><span data-stu-id="51812-146">Keep the short description to one sentence.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="スクリーンショットの例では、アプリの短い説明がストアの登録情報に表示される場所を強調表示します。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="51812-148">短い説明がストアの検証ガイドラインに [準拠している必要があります](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description)。</span><span class="sxs-lookup"><span data-stu-id="51812-148">Make sure your short description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description).</span></span>

#### <a name="long-description"></a><span data-ttu-id="51812-149">詳しい説明</span><span class="sxs-lookup"><span data-stu-id="51812-149">Long description</span></span>

<span data-ttu-id="51812-150">長い説明では、アプリの主な機能、解決する問題、ターゲットユーザーを強調する説明を提供できます。</span><span class="sxs-lookup"><span data-stu-id="51812-150">The long description can provide a narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="51812-151">この説明は 4,000 文字までですが、ほとんどのユーザーは 300 ~ 500 語しか読み取りできません。</span><span class="sxs-lookup"><span data-stu-id="51812-151">While this description can be as long as 4,000 characters, most users will only read between 300-500 words.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="スクリーンショットの例では、アプリの長い説明がストア登録情報に表示される場所を強調表示します。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="51812-153">長い説明がストアの検証ガイドラインに [準拠している必要があります](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description)。</span><span class="sxs-lookup"><span data-stu-id="51812-153">Make sure your long description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description).</span></span>

### <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="51812-154">アイコンの設計ガイドラインに従う</span><span class="sxs-lookup"><span data-stu-id="51812-154">Adhere to icon design guidelines</span></span>

<span data-ttu-id="51812-155">アイコンは、ユーザーがストアを閲覧するときに表示される主な要素の 1 つです。</span><span class="sxs-lookup"><span data-stu-id="51812-155">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="51812-156">アイコンは、アプリのブランドと目的を伝える一方で、ユーザーの要件にTeamsがあります。</span><span class="sxs-lookup"><span data-stu-id="51812-156">Your icons should communicate your app's brand and purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="51812-157">詳細については、「アプリ アイコンの[作成に関するガイダンスTeams参照してください](~/concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="51812-157">For more information, see [guidance on creating Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

### <a name="capture-screenshots"></a><span data-ttu-id="51812-158">スクリーンショットのキャプチャ</span><span class="sxs-lookup"><span data-stu-id="51812-158">Capture screenshots</span></span>

<span data-ttu-id="51812-159">スクリーンショットは、アプリ名、アイコン、説明を補完するアプリの目立つ視覚的なプレビューを提供します。</span><span class="sxs-lookup"><span data-stu-id="51812-159">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="スクリーンショットの例では、アプリのスクリーンショットがストアの登録情報に表示される場所を強調表示します。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="51812-161">スクリーンショットについては、次の情報を覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="51812-161">Remember the following about screenshots:</span></span>

* <span data-ttu-id="51812-162">リストごとに最大 5 つのスクリーンショットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="51812-162">You can have up to five screenshots per listing.</span></span>
* <span data-ttu-id="51812-163">サポートされているファイルの種類には、PNG、JPEG、GIF が含まれます。</span><span class="sxs-lookup"><span data-stu-id="51812-163">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="51812-164">ディメンションは 1366x768 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="51812-164">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="51812-165">最大サイズは 1,024 KB です。</span><span class="sxs-lookup"><span data-stu-id="51812-165">Maximum size of 1,024 KB.</span></span>

<span data-ttu-id="51812-166">ベスト プラクティスについては、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="51812-166">For best practices, see the following resources:</span></span>

* [<span data-ttu-id="51812-167">Teamsの検証ガイドライン</span><span class="sxs-lookup"><span data-stu-id="51812-167">Teams store validation guidelines</span></span>](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#44-screenshots)
* [<span data-ttu-id="51812-168">Microsoft アプリ ストアの効果的なイメージを作成する</span><span class="sxs-lookup"><span data-stu-id="51812-168">Craft effective images for Microsoft app stores</span></span>](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a><span data-ttu-id="51812-169">ビデオを作成する</span><span class="sxs-lookup"><span data-stu-id="51812-169">Create a video</span></span>

<span data-ttu-id="51812-170">リスト内のビデオは、ユーザーがアプリを使用する理由を伝える最も効果的な方法です。</span><span class="sxs-lookup"><span data-stu-id="51812-170">A video in your listing can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="51812-171">ビデオで次の質問に対処する必要があります。</span><span class="sxs-lookup"><span data-stu-id="51812-171">You should address the following questions in a video:</span></span>

* <span data-ttu-id="51812-172">Whoアプリは何ですか?</span><span class="sxs-lookup"><span data-stu-id="51812-172">Who is your app for?</span></span>
* <span data-ttu-id="51812-173">アプリで解決できる問題は何ですか?</span><span class="sxs-lookup"><span data-stu-id="51812-173">What problems can your app solve?</span></span>
* <span data-ttu-id="51812-174">アプリの動作方法</span><span class="sxs-lookup"><span data-stu-id="51812-174">How does your app work?</span></span>
* <span data-ttu-id="51812-175">アプリを使用して得るその他の利点は何ですか?</span><span class="sxs-lookup"><span data-stu-id="51812-175">What other benefits do you get from using your app?</span></span>

#### <a name="best-practices-for-videos"></a><span data-ttu-id="51812-176">ビデオのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="51812-176">Best practices for videos</span></span>

* <span data-ttu-id="51812-177">ビデオを 30 ~ 90 秒の間に保持します。</span><span class="sxs-lookup"><span data-stu-id="51812-177">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="51812-178">品質を目指します。</span><span class="sxs-lookup"><span data-stu-id="51812-178">Aim for quality.</span></span> <span data-ttu-id="51812-179">リストでは、スクリーンショットの前にユーザーにビデオが表示されます。</span><span class="sxs-lookup"><span data-stu-id="51812-179">In a listing, users will see your video before screenshots.</span></span>

### <a name="select-a-category-for-your-app"></a><span data-ttu-id="51812-180">アプリのカテゴリを選択する</span><span class="sxs-lookup"><span data-stu-id="51812-180">Select a category for your app</span></span>

<span data-ttu-id="51812-181">申請中に、アプリの分類を求めるメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="51812-181">During submission, you're asked to categorize your app.</span></span> <span data-ttu-id="51812-182">次の表は、Teamsのカテゴリをパートナー センターに一覧表示するカテゴリ[にマップします](https://aka.ms/PartnerCenterHomePage)。</span><span class="sxs-lookup"><span data-stu-id="51812-182">The following table maps Teams store categories to the categories listed in [Partner Center](https://aka.ms/PartnerCenterHomePage).</span></span>

| <span data-ttu-id="51812-183">Teamsカテゴリ</span><span class="sxs-lookup"><span data-stu-id="51812-183">Teams categories</span></span>       | <span data-ttu-id="51812-184">パートナー センターのカテゴリ</span><span class="sxs-lookup"><span data-stu-id="51812-184">Partner Center categories</span></span>  |
|:---------------------|:---------------|
| <span data-ttu-id="51812-185">分析と BI</span><span class="sxs-lookup"><span data-stu-id="51812-185">Analytics and BI</span></span> | <span data-ttu-id="51812-186">分析、データ可視化、BI</span><span class="sxs-lookup"><span data-stu-id="51812-186">Analytics, Data Visualization and BI</span></span> |
| <span data-ttu-id="51812-187">開発者と IT</span><span class="sxs-lookup"><span data-stu-id="51812-187">Developer and IT</span></span> | <span data-ttu-id="51812-188">開発者ツール、IT 管理者</span><span class="sxs-lookup"><span data-stu-id="51812-188">Developer Tools, IT Admin</span></span> |
| <span data-ttu-id="51812-189">教育</span><span class="sxs-lookup"><span data-stu-id="51812-189">Education</span></span> | <span data-ttu-id="51812-190">教育</span><span class="sxs-lookup"><span data-stu-id="51812-190">Education</span></span> |
| <span data-ttu-id="51812-191">人事管理</span><span class="sxs-lookup"><span data-stu-id="51812-191">Human resources</span></span> | <span data-ttu-id="51812-192">人事と採用</span><span class="sxs-lookup"><span data-stu-id="51812-192">Human Resources and Recruiting</span></span> |
| <span data-ttu-id="51812-193">生産性</span><span class="sxs-lookup"><span data-stu-id="51812-193">Productivity</span></span> | <span data-ttu-id="51812-194">コンテンツ管理、ファイルとドキュメント、生産性、トレーニングとチュートリアル、ユーティリティ</span><span class="sxs-lookup"><span data-stu-id="51812-194">Content Management, Files and documents, Productivity, Training and Tutorials, and Utilities</span></span> |
| <span data-ttu-id="51812-195">プロジェクト管理</span><span class="sxs-lookup"><span data-stu-id="51812-195">Project management</span></span> | <span data-ttu-id="51812-196">コミュニケーション、Project管理、ワークフロー、およびビジネス管理</span><span class="sxs-lookup"><span data-stu-id="51812-196">Communication, Project Management, Workflow, and Business Management</span></span> |
| <span data-ttu-id="51812-197">販売とサポート</span><span class="sxs-lookup"><span data-stu-id="51812-197">Sales and support</span></span> | <span data-ttu-id="51812-198">顧客と連絡先の管理、カスタマー サポート、財務管理、営業およびマーケティング</span><span class="sxs-lookup"><span data-stu-id="51812-198">Customer and Contact Management, Customer Support, Financial Management, Sales and Marketing</span></span> |
| <span data-ttu-id="51812-199">ソーシャルで楽しい</span><span class="sxs-lookup"><span data-stu-id="51812-199">Social and fun</span></span> | <span data-ttu-id="51812-200">画像とビデオ ギャラリー、ライフスタイル、ニュースと天気予報、ソーシャル、旅行、ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="51812-200">Image and Video Galleries, Lifestyle, News and Weather, Social, Travel, and Navigation</span></span> |

### <a name="localize-your-store-listing"></a><span data-ttu-id="51812-201">ストアの登録情報をローカライズする</span><span class="sxs-lookup"><span data-stu-id="51812-201">Localize your store listing</span></span>

<span data-ttu-id="51812-202">パートナー センターは、 [ローカライズされたストアの登録情報をサポートしています](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions)。</span><span class="sxs-lookup"><span data-stu-id="51812-202">Partner Center supports [localized store listings](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="51812-203">詳細については、「アプリの登録[情報をローカライズするTeams」を参照してください](../../../../concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="51812-203">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="complete-publisher-verification"></a><span data-ttu-id="51812-204">完全なPublisher検証</span><span class="sxs-lookup"><span data-stu-id="51812-204">Complete Publisher Verification</span></span>

<span data-ttu-id="51812-205">[Publisherストアに](/azure/active-directory/develop/publisher-verification-overview)一覧表示されているアプリTeams検証が必要です。詳細については、「よく寄せられる質問[」、](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)アプリを[](/azure/active-directory/develop/mark-app-as-publisher-verified)発行元の検証済みとしてマークする方法、および発行元の検証の[トラブルシューティングを参照してください](/azure/active-directory/develop/troubleshoot-publisher-verification)。</span><span class="sxs-lookup"><span data-stu-id="51812-205">[Publisher Verification](/azure/active-directory/develop/publisher-verification-overview) is required for Teams apps listed in the store.For more information, see [frequently asked questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [how to mark your app as publisher verified](/azure/active-directory/develop/mark-app-as-publisher-verified), and [troubleshoot publisher verification](/azure/active-directory/develop/troubleshoot-publisher-verification).</span></span>

## <a name="complete-publisher-attestation"></a><span data-ttu-id="51812-206">完全なPublisher構成証明</span><span class="sxs-lookup"><span data-stu-id="51812-206">Complete Publisher Attestation</span></span>

<span data-ttu-id="51812-207">[Publisher一覧に](/microsoft-365-app-certification/docs/attestation)表示されるアプリTeams構成証明も必要です。</span><span class="sxs-lookup"><span data-stu-id="51812-207">[Publisher Attestation](/microsoft-365-app-certification/docs/attestation) is also required for Teams apps listed in the store.</span></span> <span data-ttu-id="51812-208">このプロセスには、潜在的な顧客がアプリの使用に関する情報に基づいた意思決定を行うのに役立つ、アプリのセキュリティ、データ処理、コンプライアンスプラクティスの自己評価が含まれます。</span><span class="sxs-lookup"><span data-stu-id="51812-208">The process includes completing a self-assessment of your app's security, data handling, and compliance practices that can help potential customers make informed decisions about using your app.</span></span>

> [!NOTE]
> <span data-ttu-id="51812-209">新しいアプリを提出する場合は、アプリが Teams ストアに表示されるまで、Publisher 構成証明を正式にTeamsできます。</span><span class="sxs-lookup"><span data-stu-id="51812-209">If you're submitting a new app, you can't officially complete Publisher Attestation until your app is listed on the Teams store.</span></span> <span data-ttu-id="51812-210">リストされているアプリを更新する場合は、検証Publisher最新バージョンのアプリを提出する前に、構成証明を完了してください。</span><span class="sxs-lookup"><span data-stu-id="51812-210">If you're updating a listed app, complete Publisher Attestation before you submit the latest version of the app for validation.</span></span>

## <a name="next-step"></a><span data-ttu-id="51812-211">次の手順</span><span class="sxs-lookup"><span data-stu-id="51812-211">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="51812-212">アプリを提出する</span><span class="sxs-lookup"><span data-stu-id="51812-212">Submit your app</span></span>](https://docs.microsoft.com/office/dev/store/add-in-submission-guide)
