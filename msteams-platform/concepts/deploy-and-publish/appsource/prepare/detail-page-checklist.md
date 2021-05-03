---
title: アプリのストア登録情報を作成する
description: アプリのストア登録情報を作成するMicrosoft Teamsします。
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 270936ca967c17caaa8a56f85057b20ca3d6a409
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101430"
---
# <a name="create-a-store-listing-for-your-microsoft-teams-app"></a><span data-ttu-id="0fd98-103">アプリのストア登録情報をMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="0fd98-103">Create a store listing for your Microsoft Teams app</span></span>

<span data-ttu-id="0fd98-104">名前、説明、アイコン、[](https://partner.microsoft.com)画像&#8212;を含むパートナー センター&#8212;に送信する情報は、&#8212;アプリの Microsoft Teams ストアと Microsoft AppSource の一覧になります。</span><span class="sxs-lookup"><span data-stu-id="0fd98-104">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Microsoft Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="0fd98-105">ストアの登録情報は、アプリの第一印象である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0fd98-105">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="0fd98-106">アプリの利点、機能、ブランドを効果的に伝えるリストを使用してインストールを増やします。</span><span class="sxs-lookup"><span data-stu-id="0fd98-106">Increase your installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

## <a name="specify-a-short-name"></a><span data-ttu-id="0fd98-107">短い名前を指定する</span><span class="sxs-lookup"><span data-stu-id="0fd98-107">Specify a short name</span></span>

<span data-ttu-id="0fd98-108">アプリの名前 (具体的には短い名前 [*)*](~/resources/schema/manifest-schema.md#name)は、ユーザーがストアでアプリを検出する方法において重要な役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="0fd98-108">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

<span data-ttu-id="0fd98-109">次の例では、アプリの短い名前がストアの登録情報に表示される場所を強調表示します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-109">The following example highlights where an app's short name displays in a store listing.</span></span>

:::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="スクリーンショットの例は、アプリの短い名前がストアの登録情報に表示される場所を強調表示します。":::

### <a name="best-practices-for-names"></a><span data-ttu-id="0fd98-111">名前のベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="0fd98-111">Best practices for names</span></span>

<span data-ttu-id="0fd98-112">**するべきこと**</span><span class="sxs-lookup"><span data-stu-id="0fd98-112">**Do:**</span></span>

* <span data-ttu-id="0fd98-113">アプリの動作をヒントにした、簡単で思い出に残る名前を選択します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-113">Choose a simple, memorable name that hints at what your app does.</span></span>
* <span data-ttu-id="0fd98-114">独特の特徴を持つ。</span><span class="sxs-lookup"><span data-stu-id="0fd98-114">Be distinctive.</span></span>
* <span data-ttu-id="0fd98-115">入力ミスや文法上のエラーを避ける。</span><span class="sxs-lookup"><span data-stu-id="0fd98-115">Avoid typos and grammatical errors.</span></span>

<span data-ttu-id="0fd98-116">**してはいけないこと**</span><span class="sxs-lookup"><span data-stu-id="0fd98-116">**Don't:**</span></span>

* <span data-ttu-id="0fd98-117">不適切な用語または軽蔑的な用語を使用します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-117">Use profane or derogatory terms.</span></span>
* <span data-ttu-id="0fd98-118">人種的または文化的に無神経な言語を使用します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-118">Use racially or culturally insensitive language.</span></span>
* <span data-ttu-id="0fd98-119">既存のアプリに似た一般的な用語または名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-119">Use generic terms or names similar to existing apps.</span></span>
* <span data-ttu-id="0fd98-120">"Teams"、"Microsoft"、既存/今後の Microsoft 製品名、または "app" を名前に含める。</span><span class="sxs-lookup"><span data-stu-id="0fd98-120">Include "Teams", "Microsoft", existing/upcoming Microsoft product names, or  "app" in the name.</span></span>

> [!NOTE]
> <span data-ttu-id="0fd98-121">アプリが Microsoft との公式なパートナーシップの一部である場合は、アプリの名前が最初に指定されている必要があります (たとえば *、Salesforce Connector for microsoft* Microsoft Teams)。</span><span class="sxs-lookup"><span data-stu-id="0fd98-121">If your app is part of an official partnership with Microsoft, the name of your app must come first (for example, *Salesforce Connector for Microsoft Teams*).</span></span>

## <a name="write-descriptions"></a><span data-ttu-id="0fd98-122">説明の書き込み</span><span class="sxs-lookup"><span data-stu-id="0fd98-122">Write descriptions</span></span>

<span data-ttu-id="0fd98-123">アプリの短い説明と長い説明が必要です。</span><span class="sxs-lookup"><span data-stu-id="0fd98-123">You need a short and long description of your app.</span></span>

### <a name="short-description"></a><span data-ttu-id="0fd98-124">簡潔な説明</span><span class="sxs-lookup"><span data-stu-id="0fd98-124">Short description</span></span>

<span data-ttu-id="0fd98-125">対象ユーザーに対して、元の、魅力的で、指示する必要があるアプリの簡潔な概要。</span><span class="sxs-lookup"><span data-stu-id="0fd98-125">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="0fd98-126">理想的には、短い説明を 1 つの文にしてください。</span><span class="sxs-lookup"><span data-stu-id="0fd98-126">Ideally, keep the short description to one sentence.</span></span>

<span data-ttu-id="0fd98-127">次の例では、アプリの短い説明がストアの登録情報に表示される場所を強調表示します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-127">The following example highlights where an app's short description displays in a store listing:</span></span>

:::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="スクリーンショットの例では、アプリの短い説明がストアの登録情報に表示される場所を強調表示します。":::

#### <a name="best-practices-for-short-descriptions"></a><span data-ttu-id="0fd98-129">短い説明のベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="0fd98-129">Best practices for short descriptions</span></span>

<span data-ttu-id="0fd98-130">**するべきこと**</span><span class="sxs-lookup"><span data-stu-id="0fd98-130">**Do:**</span></span>

* <span data-ttu-id="0fd98-131">最も重要な情報を最初に説明します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-131">Put the most important information first.</span></span>
* <span data-ttu-id="0fd98-132">顧客が検索する可能性が高いキーワードを含める。</span><span class="sxs-lookup"><span data-stu-id="0fd98-132">Include keywords that customers are likely to search for.</span></span>

<span data-ttu-id="0fd98-133">**してはいけないこと**</span><span class="sxs-lookup"><span data-stu-id="0fd98-133">**Don't:**</span></span>

* <span data-ttu-id="0fd98-134">アプリ名を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-134">Repeat your app name.</span></span>
* <span data-ttu-id="0fd98-135">専門用語や専門用語に頼る。</span><span class="sxs-lookup"><span data-stu-id="0fd98-135">Rely on jargon or specialized terminology.</span></span> <span data-ttu-id="0fd98-136">(ユーザーが何を探すのかを知っている場合は想定できない)。</span><span class="sxs-lookup"><span data-stu-id="0fd98-136">(You can't assume users know what to look for.)</span></span>

### <a name="long-description"></a><span data-ttu-id="0fd98-137">詳しい説明</span><span class="sxs-lookup"><span data-stu-id="0fd98-137">Long description</span></span>

<span data-ttu-id="0fd98-138">長い説明では、アプリの主な機能、解決する問題、ターゲットユーザーを強調する魅力的な説明を提供できます。</span><span class="sxs-lookup"><span data-stu-id="0fd98-138">The long description can provide an engaging narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="0fd98-139">この説明は 4,000 文字までですが、ほとんどのユーザーは 300 ~ 500 語しか読み取りできません。</span><span class="sxs-lookup"><span data-stu-id="0fd98-139">While this description can be as long as 4000 characters, most users will only read between 300-500 words.</span></span>

<span data-ttu-id="0fd98-140">次の例では、アプリの長い説明がストア登録情報に表示される場所を強調表示します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-140">The following example highlights where an app's long description displays in a store listing:</span></span>

:::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="スクリーンショットの例では、アプリの長い説明がストア登録情報に表示される場所を強調表示します。":::

#### <a name="usage-examples"></a><span data-ttu-id="0fd98-142">使用例</span><span class="sxs-lookup"><span data-stu-id="0fd98-142">Usage examples</span></span>

<span data-ttu-id="0fd98-143">次の語句は、長い説明を書く際に許可される内容の例です。</span><span class="sxs-lookup"><span data-stu-id="0fd98-143">The following phrases are examples of what's allowed when writing long descriptions:</span></span>

* <span data-ttu-id="0fd98-144">"<*アプリ名は、>* で動作Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="0fd98-144">"<*Your app name*> works with Microsoft Teams"</span></span>
* <span data-ttu-id="0fd98-145">"..."<*アプリの>* のMicrosoft Teams"</span><span class="sxs-lookup"><span data-stu-id="0fd98-145">"... a <*type of app*> for Microsoft Teams"</span></span>
* <span data-ttu-id="0fd98-146">"<*アプリ名とアプリ名*> Microsoft Teams統合する"</span><span class="sxs-lookup"><span data-stu-id="0fd98-146">"<*Your app name*> integrates with Microsoft Teams"</span></span>
* <span data-ttu-id="0fd98-147">"...と統合Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="0fd98-147">"... integrated with Microsoft Teams"</span></span>
* <span data-ttu-id="0fd98-148">"...を使用するユーザー Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="0fd98-148">"... for users working with Microsoft Teams"</span></span>
* <span data-ttu-id="0fd98-149">"..."<*内の特定*>タスクMicrosoft Teams"</span><span class="sxs-lookup"><span data-stu-id="0fd98-149">"... for <*specific task*> within Microsoft Teams"</span></span>
* <span data-ttu-id="0fd98-150">"...に構築されています。."</span><span class="sxs-lookup"><span data-stu-id="0fd98-150">"... built on ..."</span></span>
* <span data-ttu-id="0fd98-151">"...で実行されます。."</span><span class="sxs-lookup"><span data-stu-id="0fd98-151">"... runs on ..."</span></span>
* <span data-ttu-id="0fd98-152">"...によって有効になります。."</span><span class="sxs-lookup"><span data-stu-id="0fd98-152">"... enabled by ..."</span></span>
* <span data-ttu-id="0fd98-153">".....用に開発されました。</span><span class="sxs-lookup"><span data-stu-id="0fd98-153">"... developed for ..."</span></span>
* <span data-ttu-id="0fd98-154">"......" 用に設計されています。</span><span class="sxs-lookup"><span data-stu-id="0fd98-154">"... designed for ..."</span></span>

#### <a name="best-practices-for-long-descriptions"></a><span data-ttu-id="0fd98-155">長い説明のベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="0fd98-155">Best practices for long descriptions</span></span>

<span data-ttu-id="0fd98-156">**するべきこと**</span><span class="sxs-lookup"><span data-stu-id="0fd98-156">**Do:**</span></span>

* <span data-ttu-id="0fd98-157">Markdown [を使用して](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) 説明の書式を設定します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-157">Use [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) to format your description.</span></span>
* <span data-ttu-id="0fd98-158">説明を簡単にスキャンするために、箇条書きポイントを含む機能を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-158">List features with bullet points so it's easier to scan the description.</span></span>
* <span data-ttu-id="0fd98-159">アクティブな音声を使用し、ユーザーに直接話します (たとえば *、..)。*</span><span class="sxs-lookup"><span data-stu-id="0fd98-159">Use active voice and speak to users directly (for example, *You can ...*).</span></span>
* <span data-ttu-id="0fd98-160">ヘルプまたはサポート リンクを含める。</span><span class="sxs-lookup"><span data-stu-id="0fd98-160">Include a help or support link.</span></span>
* <span data-ttu-id="0fd98-161">該当する場合は、制限、情報の設定、アカウントの依存関係、リリース更新プログラムを特定します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-161">Identify the following if applicable: limitations, set up information, account dependencies, and release updates.</span></span>

<span data-ttu-id="0fd98-162">**してはいけないこと**</span><span class="sxs-lookup"><span data-stu-id="0fd98-162">**Don't:**</span></span>

* <span data-ttu-id="0fd98-163">500 単語を超える。</span><span class="sxs-lookup"><span data-stu-id="0fd98-163">Exceed 500 words.</span></span>
* <span data-ttu-id="0fd98-164">キーワードが多すぎます。</span><span class="sxs-lookup"><span data-stu-id="0fd98-164">Include too many keywords.</span></span> <span data-ttu-id="0fd98-165">(気を散らすので、アプリを見つけるのに役立つことはありません)。</span><span class="sxs-lookup"><span data-stu-id="0fd98-165">(It's distracting and won't help people find your app.)</span></span>
* <span data-ttu-id="0fd98-166">アプリが公式の認定プロセスを通過しない限り、次の言語を使用します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-166">Use the following language unless the app has gone through an official certification process:</span></span>
  * <span data-ttu-id="0fd98-167">"...の認定を受けています。</span><span class="sxs-lookup"><span data-stu-id="0fd98-167">"... certified for ..."</span></span>
  * <span data-ttu-id="0fd98-168">" ...によって動力を与えられた..."</span><span class="sxs-lookup"><span data-stu-id="0fd98-168">" ... powered by ..."</span></span>

### <a name="best-practices-for-all-descriptions"></a><span data-ttu-id="0fd98-169">すべての説明のベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="0fd98-169">Best practices for all descriptions</span></span>

<span data-ttu-id="0fd98-170">**するべきこと**</span><span class="sxs-lookup"><span data-stu-id="0fd98-170">**Do:**</span></span>

* <span data-ttu-id="0fd98-171">必要な場合にのみ、Microsoft 製品名を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0fd98-171">Reference Microsoft product names only when necessary.</span></span> <span data-ttu-id="0fd98-172">ガイドラインの詳細については、「Microsoft 商標とブランド [ガイドライン」を参照してください](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)。</span><span class="sxs-lookup"><span data-stu-id="0fd98-172">For more information on the guidelines, see [Microsoft Trademark and Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general).</span></span>
* <span data-ttu-id="0fd98-173">ファイルを参照する必要がある **場合Teams** 最初の参照を "Microsoft Teams"**とMicrosoft Teams。**</span><span class="sxs-lookup"><span data-stu-id="0fd98-173">If you need to reference **Teams**, write the first reference as **Microsoft Teams**.</span></span> <span data-ttu-id="0fd98-174">後続の参照は、次の参照に **短縮Teams。**</span><span class="sxs-lookup"><span data-stu-id="0fd98-174">Subsequent references can be shortened to **Teams**.</span></span>
* <span data-ttu-id="0fd98-175">代わりに **Microsoft 365** を参照 **Office 365。**</span><span class="sxs-lookup"><span data-stu-id="0fd98-175">Refer to **Microsoft 365** instead of **Office 365**.</span></span>
* <span data-ttu-id="0fd98-176">入力ミスや文法上のエラーを避ける。</span><span class="sxs-lookup"><span data-stu-id="0fd98-176">Avoid typos and grammatical errors.</span></span>
* <span data-ttu-id="0fd98-177">不要な大文字を避ける (たとえば、**ユーザー** ではなく **ユーザー)。**</span><span class="sxs-lookup"><span data-stu-id="0fd98-177">Avoid unnecessary capitalizations (for example, **Users** instead of **users**).</span></span>
* <span data-ttu-id="0fd98-178">頭字語は避ける。</span><span class="sxs-lookup"><span data-stu-id="0fd98-178">Avoid acronyms.</span></span>

<span data-ttu-id="0fd98-179">**してはいけないこと**</span><span class="sxs-lookup"><span data-stu-id="0fd98-179">**Don't:**</span></span>

* <span data-ttu-id="0fd98-180">Microsoft を MS または **MSFT** と **略します**。</span><span class="sxs-lookup"><span data-stu-id="0fd98-180">Abbreviate Microsoft as **MS** or **MSFT**.</span></span>
* <span data-ttu-id="0fd98-181">Microsoft のスローガンやタグラインの使用を含め、アプリが Microsoft からのオファリングである場合を示します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-181">Indicate the app is an offering from Microsoft, including using Microsoft slogans or taglines.</span></span>
* <span data-ttu-id="0fd98-182">所有しない著作権で保護されたブランド名を使用します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-182">Use copyrighted brand names you don't own.</span></span>

## <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="0fd98-183">アイコンの設計ガイドラインに従う</span><span class="sxs-lookup"><span data-stu-id="0fd98-183">Adhere to icon design guidelines</span></span>

<span data-ttu-id="0fd98-184">アイコンは、ユーザーがストアを閲覧するときに表示される主な要素の 1 つです。</span><span class="sxs-lookup"><span data-stu-id="0fd98-184">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="0fd98-185">アイコンは、アプリのブランドの目的を伝える一方で、ユーザーの要件にTeamsがあります。</span><span class="sxs-lookup"><span data-stu-id="0fd98-185">Your icons should communicate your app's brand purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="0fd98-186">詳細については、「アプリ アイコン[の設計に関する具体的なTeams」を参照してください](~/concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="0fd98-186">For more information, see [specific guidance on designing Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="capture-screenshots"></a><span data-ttu-id="0fd98-187">スクリーンショットのキャプチャ</span><span class="sxs-lookup"><span data-stu-id="0fd98-187">Capture screenshots</span></span>

<span data-ttu-id="0fd98-188">スクリーンショットは、アプリ名、アイコン、説明を補完するアプリの目立つ視覚的なプレビューを提供します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-188">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

### <a name="requirements-for-screenshots"></a><span data-ttu-id="0fd98-189">スクリーンショットの要件</span><span class="sxs-lookup"><span data-stu-id="0fd98-189">Requirements for screenshots</span></span>

* <span data-ttu-id="0fd98-190">リストごとに最大 5 つのスクリーンショット。</span><span class="sxs-lookup"><span data-stu-id="0fd98-190">Up to five screenshots per listing.</span></span>
* <span data-ttu-id="0fd98-191">サポートされているファイルの種類には、PNG、JPEG、GIF が含まれます。</span><span class="sxs-lookup"><span data-stu-id="0fd98-191">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="0fd98-192">ディメンションは 1366x768 ピクセルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="0fd98-192">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="0fd98-193">最大サイズは 1,024 KB です。</span><span class="sxs-lookup"><span data-stu-id="0fd98-193">Maximum size of 1,024 KB.</span></span>

### <a name="best-practices-for-screenshots"></a><span data-ttu-id="0fd98-194">スクリーンショットのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="0fd98-194">Best practices for screenshots</span></span>

<span data-ttu-id="0fd98-195">**するべきこと**</span><span class="sxs-lookup"><span data-stu-id="0fd98-195">**Do:**</span></span>

* <span data-ttu-id="0fd98-196">アプリの機能 (ユーザーがボットと通信する方法など) に集中します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-196">Focus on your app's capabilities (for example, how people can communicate with your bot).</span></span>
* <span data-ttu-id="0fd98-197">アプリを正確に表すコンテンツを含める。</span><span class="sxs-lookup"><span data-stu-id="0fd98-197">Include content that accurately represents your app.</span></span>
* <span data-ttu-id="0fd98-198">テキストを十分に使用します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-198">Use text judiciously.</span></span>
* 次の[Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview)の例と同様に、ブランドを反映し、マーケティング コンテンツを含む色のスクリーンショットをフレーム化します (ディメンション要件は、スクリーンショットではなく画像全体に適用されます):サードパーティアプリ:::image type="content" source="../../../../assets/images/freshdesk.png" alt-text="Freshdesk":::のスクリーンショットの例

<span data-ttu-id="0fd98-200">**してはいけないこと**</span><span class="sxs-lookup"><span data-stu-id="0fd98-200">**Don't:**</span></span>

* <span data-ttu-id="0fd98-201">電話やノート PC などの特定のデバイスを表示します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-201">Show specific devices, such as phones or laptops.</span></span>
* <span data-ttu-id="0fd98-202">アプリに表示されていないクロムまたは UI を表示します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-202">Display chrome or UI that isn't in your app.</span></span>
* <span data-ttu-id="0fd98-203">スクリーンショットにTeamsまたはブラウザーの UI をキャプチャします。</span><span class="sxs-lookup"><span data-stu-id="0fd98-203">Capture any Teams or browser UI in your screenshots.</span></span>
* <span data-ttu-id="0fd98-204">アプリの実際の UI を不正確に反映するモックアップを含める (アプリをブラウザーで表示する場合は、[アプリ] タブではなくTeamsします。</span><span class="sxs-lookup"><span data-stu-id="0fd98-204">Include mockups that inaccurately reflect your app's actual UI, such as showing your app in  a browser instead of a Teams tab.</span></span>

<span data-ttu-id="0fd98-205">ベスト プラクティスの詳細については [、「Microsoft アプリ ストアの効果的なイメージを作成する」を参照してください](/office/dev/store/craft-effective-appsource-store-images)。</span><span class="sxs-lookup"><span data-stu-id="0fd98-205">For more best practices, see [craft effective images for Microsoft app stores](/office/dev/store/craft-effective-appsource-store-images).</span></span>

## <a name="create-a-video"></a><span data-ttu-id="0fd98-206">ビデオを作成する</span><span class="sxs-lookup"><span data-stu-id="0fd98-206">Create a video</span></span>

<span data-ttu-id="0fd98-207">ビデオは、ユーザーがアプリを使用する理由を伝える最も効果的な方法です。</span><span class="sxs-lookup"><span data-stu-id="0fd98-207">A video can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="0fd98-208">ビデオで次の質問に対処する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0fd98-208">You should address the following questions in a video:</span></span>

* <span data-ttu-id="0fd98-209">Whoアプリは何ですか?</span><span class="sxs-lookup"><span data-stu-id="0fd98-209">Who is your app for?</span></span>
* <span data-ttu-id="0fd98-210">アプリで解決できる問題は何ですか?</span><span class="sxs-lookup"><span data-stu-id="0fd98-210">What problems can your app solve?</span></span>
* <span data-ttu-id="0fd98-211">アプリの動作方法</span><span class="sxs-lookup"><span data-stu-id="0fd98-211">How does your app work?</span></span>
* <span data-ttu-id="0fd98-212">アプリを使用して得るその他の利点は何ですか?</span><span class="sxs-lookup"><span data-stu-id="0fd98-212">What other benefits do you get from using your app?</span></span>

<span data-ttu-id="0fd98-213">ビデオを含める場合は、リストにスクリーンショットの前に表示されます。</span><span class="sxs-lookup"><span data-stu-id="0fd98-213">If you include a video, it appears before your screenshots in the listing.</span></span>

### <a name="best-practices-for-videos"></a><span data-ttu-id="0fd98-214">ビデオのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="0fd98-214">Best practices for videos</span></span>

* <span data-ttu-id="0fd98-215">ビデオを 30 ~ 90 秒の間に保持します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-215">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="0fd98-216">品質を目指します。</span><span class="sxs-lookup"><span data-stu-id="0fd98-216">Aim for quality.</span></span> <span data-ttu-id="0fd98-217">リストでは、スクリーンショットの前にユーザーにビデオが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0fd98-217">In a listing, users will see your video before screenshots.</span></span>

## <a name="localize-your-store-listing"></a><span data-ttu-id="0fd98-218">ストアの登録情報をローカライズする</span><span class="sxs-lookup"><span data-stu-id="0fd98-218">Localize your store listing</span></span>

<span data-ttu-id="0fd98-219">パートナー センターは、 [ローカライズされたストアの登録情報をサポートしています](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions)。</span><span class="sxs-lookup"><span data-stu-id="0fd98-219">Partner Center supports [localized store listings](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="0fd98-220">詳細については、「アプリの登録[情報をローカライズするTeams」を参照してください](../../../../concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="0fd98-220">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0fd98-221">関連項目</span><span class="sxs-lookup"><span data-stu-id="0fd98-221">See also</span></span>

* [<span data-ttu-id="0fd98-222">効果的なストアMicrosoft 365を作成する</span><span class="sxs-lookup"><span data-stu-id="0fd98-222">Create effective Microsoft 365 Stores listings</span></span>](/office/dev/store/create-effective-office-store-listings)
* <span data-ttu-id="0fd98-223">Teamsとコンテンツとブランドの表現に関[するアプリ設計](~/concepts/design/design-teams-app-fundamentals.md#copy-and-content)[ガイドライン](~/concepts/design/design-teams-app-fundamentals.md#brand-expression)</span><span class="sxs-lookup"><span data-stu-id="0fd98-223">Teams app design guidelines for [copy and content](~/concepts/design/design-teams-app-fundamentals.md#copy-and-content) and [brand expression](~/concepts/design/design-teams-app-fundamentals.md#brand-expression)</span></span>
* [<span data-ttu-id="0fd98-224">Microsoft 商標とブランド ガイドライン</span><span class="sxs-lookup"><span data-stu-id="0fd98-224">Microsoft Trademark and Brand Guidelines</span></span>](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)

## <a name="next-step"></a><span data-ttu-id="0fd98-225">次の手順</span><span class="sxs-lookup"><span data-stu-id="0fd98-225">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0fd98-226">ストア送信を準備する</span><span class="sxs-lookup"><span data-stu-id="0fd98-226">Prepare your store submission</span></span>](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
