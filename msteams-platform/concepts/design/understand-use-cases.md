---
title: ユース ケースを理解する
author: clearab
description: ユース ケースを理解する
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: a873c3030ee4ed5f5fc98229c058583e64c38de5
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654280"
---
# <a name="understand-your-use-cases"></a><span data-ttu-id="91093-103">ユース ケースを理解する</span><span class="sxs-lookup"><span data-stu-id="91093-103">Understand your use cases</span></span>

<span data-ttu-id="91093-104">Microsoft Teams プラットフォームは、アプリで利用できるさまざまなエントリ ポイントと [UI](../../concepts/extensibility-points.md) 要素を提供します。</span><span class="sxs-lookup"><span data-stu-id="91093-104">The Microsoft Teams platform offers a large variety of [entry points and UI elements](../../concepts/extensibility-points.md) your app can take advantage of.</span></span>
> [!NOTE]
> <span data-ttu-id="91093-105">使用例の構築を開始する前に、Teams の機能と、それらを使用する Teams プラットフォームで可能なことを理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="91093-105">Before you start building your use cases, you must have a good understanding of Teams capabilities and what is possible on the Teams platform using them.</span></span>

<span data-ttu-id="91093-106">ユーザーと対話する各方法には、その長所と短所があります。</span><span class="sxs-lookup"><span data-stu-id="91093-106">Each method of interacting with your users has its strengths and weaknesses.</span></span> <span data-ttu-id="91093-107">素晴らしい Teams アプリの構築は、ユーザーのニーズに合わせて適切な組み合わせを見つけることです。</span><span class="sxs-lookup"><span data-stu-id="91093-107">Building an awesome Teams app is all about finding the right combination to meet your user's needs.</span></span> <span data-ttu-id="91093-108">これらのニーズを満たす場合は、まずそれらを理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91093-108">If you are going to meet those needs, you first need to understand them.</span></span>

## <a name="understand-the-problem"></a><span data-ttu-id="91093-109">問題を理解する</span><span class="sxs-lookup"><span data-stu-id="91093-109">Understand the problem</span></span>

<span data-ttu-id="91093-110">すべての良いアプリには、コアな問題や解決しようとしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="91093-110">Every good app has a core problem or a need it is trying to solve.</span></span> <span data-ttu-id="91093-111">アプリの構築を開始する前に、その問題が何かを明確にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="91093-111">Before you start building an app, you need to articulate what that problem is.</span></span> <span data-ttu-id="91093-112">Teams はコラボレーション プラットフォームなので、効果的なコラボレーションを実現する際のギャップを埋めるアプリは最適です。</span><span class="sxs-lookup"><span data-stu-id="91093-112">At its heart, Teams is a collaboration platform, so apps that bridge gaps in achieving effective collaboration are a great fit.</span></span> <span data-ttu-id="91093-113">また、ソーシャル プラットフォームであり、ネイティブクロスプラットフォームであり、Office 365 の中心に位置し、アプリを作成する個人用キャンバスを提供します。</span><span class="sxs-lookup"><span data-stu-id="91093-113">It is also a social platform, is natively cross-platform, sits at the heart of Office 365, and offers a personal canvas for you to create apps.</span></span> <span data-ttu-id="91093-114">このソーシャル プラットフォームでは、Teams アプリで解決できるさまざまなニーズがあります。</span><span class="sxs-lookup"><span data-stu-id="91093-114">In this social platform, there is a wide variety of needs that can be solved with a Teams app.</span></span> <span data-ttu-id="91093-115">解決しようとしている問題を理解している場合は、さまざまな問題を解決できます。</span><span class="sxs-lookup"><span data-stu-id="91093-115">You can solve wide variety of problems, provided you understand which one you are trying to solve.</span></span> <span data-ttu-id="91093-116">アプリの構築を開始する前に、次のような関連する質問をします。</span><span class="sxs-lookup"><span data-stu-id="91093-116">Before you start building an app, ask relevant questions, such as:</span></span>

* <span data-ttu-id="91093-117">ユーザーが使用している現在の状態システムの長所と短所は何ですか?</span><span class="sxs-lookup"><span data-stu-id="91093-117">What are the pros and cons of the current state system used by your users?</span></span>
* <span data-ttu-id="91093-118">今日のユーザーが直面する、対処する痛みのポイントは何ですか?</span><span class="sxs-lookup"><span data-stu-id="91093-118">What are the pain points your users face as of today that you wish to address?</span></span>
* <span data-ttu-id="91093-119">現在のプロセスのやり方でユーザーが好きと好きな機能は何ですか?</span><span class="sxs-lookup"><span data-stu-id="91093-119">What features or capabilities your users like and love in their current way of doing the process?</span></span>

## <a name="understand-your-user"></a><span data-ttu-id="91093-120">ユーザーを理解する</span><span class="sxs-lookup"><span data-stu-id="91093-120">Understand your user</span></span>

<span data-ttu-id="91093-121">ユーザーが誰か理解し、適切な配布モデルを特定できますが、さらに重要なのは、ユーザーが Teams を使用する方法を特定するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="91093-121">Understand who your user is and you can identify the right distribution model but more importantly, it helps you to identify how users use Teams.</span></span> <span data-ttu-id="91093-122">次のような関連する質問をする。</span><span class="sxs-lookup"><span data-stu-id="91093-122">Ask relevant questions, such as:</span></span>

* <span data-ttu-id="91093-123">ユーザーは主にモバイル クライアント上の第一線のワーカーですか?</span><span class="sxs-lookup"><span data-stu-id="91093-123">Are the users primarily front-line workers on mobile clients?</span></span>
* <span data-ttu-id="91093-124">多くのゲスト ユーザーがアプリにアクセスする必要が生じますか?</span><span class="sxs-lookup"><span data-stu-id="91093-124">Do you expect a lot of guest users to need access to your app?</span></span>
* <span data-ttu-id="91093-125">チームとチャネルを使用するか、主にグループ チャットを使用しますか?</span><span class="sxs-lookup"><span data-stu-id="91093-125">Do they use teams and channels or primarily group chats?</span></span>
* <span data-ttu-id="91093-126">プライマリ ユーザーは技術的に洗練されていますか?</span><span class="sxs-lookup"><span data-stu-id="91093-126">How technically sophisticated are your primary users?</span></span>
* <span data-ttu-id="91093-127">完全なオンボーディング エクスペリエンスが必要か、またはいくつかのポインターが行う可能性がありますか?</span><span class="sxs-lookup"><span data-stu-id="91093-127">Do you need a thorough onboarding experience or a few pointers might do?</span></span>

<span data-ttu-id="91093-128">場合によっては、すべての Teams ユーザーに対してこの問題を解決 *したいと考えている場合があります。*</span><span class="sxs-lookup"><span data-stu-id="91093-128">Sometimes the answer is, *We want to solve this problem for all Teams users everywhere.*</span></span> <span data-ttu-id="91093-129">その場合は、AppSource に発行するために必要なことを理解するのに時間 [を費やしてください](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="91093-129">If that is the case for you, spend some time understanding [what it takes to get published to AppSource](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).</span></span>

## <a name="understand-the-limitations-of-the-app"></a><span data-ttu-id="91093-130">アプリの制限を理解する</span><span class="sxs-lookup"><span data-stu-id="91093-130">Understand the limitations of the app</span></span>

<span data-ttu-id="91093-131">データアクセシビリティとデータ常駐要件に関するアプリの制限を理解すると、より良いアプリを設計するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="91093-131">Knowing the limitations of the apps in terms of data accessibility and data residency requirement will help you design better apps.</span></span> <span data-ttu-id="91093-132">データの所有者に関する情報と API の可用性がソリューション アーキテクチャに影響を与えるので、これは重要です。</span><span class="sxs-lookup"><span data-stu-id="91093-132">This is important, as having information on who owns the data and availability of APIs impacts the solution architecture.</span></span> <span data-ttu-id="91093-133">もう一度、次のような関連する質問をします。</span><span class="sxs-lookup"><span data-stu-id="91093-133">Again, ask relevant questions, such as:</span></span>

* <span data-ttu-id="91093-134">現在のアプリのバック エンド統合に関する課題は何ですか?</span><span class="sxs-lookup"><span data-stu-id="91093-134">What are the challenges with back end integration of the current app?</span></span>
* <span data-ttu-id="91093-135">バック エンド データを所有しているユーザー</span><span class="sxs-lookup"><span data-stu-id="91093-135">Who owns the back end data?</span></span> <span data-ttu-id="91093-136">インハウスまたはサードパーティ。</span><span class="sxs-lookup"><span data-stu-id="91093-136">In-house or third-party.</span></span>
* <span data-ttu-id="91093-137">アプリの機能に影響を与えるファイアウォールはありますか?</span><span class="sxs-lookup"><span data-stu-id="91093-137">Are there firewalls that impact the functioning of the app?</span></span>
* <span data-ttu-id="91093-138">アプリの機能に必要なデータにアクセスする API はありますか?</span><span class="sxs-lookup"><span data-stu-id="91093-138">Are there APIs to access the data you need for functioning of your app?</span></span> 

## <a name="provide-authentication"></a><span data-ttu-id="91093-139">認証の提供</span><span class="sxs-lookup"><span data-stu-id="91093-139">Provide authentication</span></span>

<span data-ttu-id="91093-140">公開しているサービスを保護する必要がある場合や、どのレベルで保護する必要がある場合は、早期に特定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91093-140">You must identify early on if you need to protect the services you are exposing and at what level.</span></span> <span data-ttu-id="91093-141">Teams アプリで公開されている Web サービスは、インターネット上で一般公開されています。</span><span class="sxs-lookup"><span data-stu-id="91093-141">Remember, the web services exposed in your Teams app are publicly available over the internet.</span></span> <span data-ttu-id="91093-142">そのため、セキュリティで保護する必要がある場合は、今すぐ考え始める必要があります。</span><span class="sxs-lookup"><span data-stu-id="91093-142">So, if you need to secure them start thinking about it now.</span></span> <span data-ttu-id="91093-143">テナント外のユーザーにゲスト アクセスを提供する必要があるソリューションが必要な場合は、機密情報を保護するためにアクセス制限とアクセス許可を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91093-143">If you need a solution that requires you to provide guest access for users outside the tenant, access restrictions and permissions need to be placed to protect confidential information.</span></span> <span data-ttu-id="91093-144">ゲスト ユーザー アクセスに関する制限を考慮してアプリを設計する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91093-144">You will need to design apps considering the limitations that come with guest user access.</span></span> <span data-ttu-id="91093-145">したがって、次のような質問をします。</span><span class="sxs-lookup"><span data-stu-id="91093-145">Therefore, ask questions, such as:</span></span> 

* <span data-ttu-id="91093-146">ユーザーは役割に基づいて異なるデータ ビューにアクセスしますか?</span><span class="sxs-lookup"><span data-stu-id="91093-146">Will the users access different views of data based on their roles?</span></span>
* <span data-ttu-id="91093-147">PII が関係していますか?</span><span class="sxs-lookup"><span data-stu-id="91093-147">Is there PII involved?</span></span>
* <span data-ttu-id="91093-148">操作はユーザー の役割にも基づいて行いますか?</span><span class="sxs-lookup"><span data-stu-id="91093-148">Will the interactions also be based on the user roles?</span></span>
* <span data-ttu-id="91093-149">外部ユーザーはアプリにアクセスしますか?</span><span class="sxs-lookup"><span data-stu-id="91093-149">Will external users access the app?</span></span>

## <a name="decide-what-goes-in-teams"></a><span data-ttu-id="91093-150">Teams で行く情報を決定する</span><span class="sxs-lookup"><span data-stu-id="91093-150">Decide what goes in Teams</span></span>

<span data-ttu-id="91093-151">新しいソリューションを構築する場合でも、既存のソリューションを Teams に組み込む場合でも、アプリ全体が Teams クライアント内にあるかどうかを判断することが重要です。</span><span class="sxs-lookup"><span data-stu-id="91093-151">Whether you are building something new or bringing an existing solution into Teams, it is important to decide if the entire app is going to be inside the Teams client.</span></span> <span data-ttu-id="91093-152">エクスペリエンスの一部のみを取り込むのが理にかなっているのか確認します。</span><span class="sxs-lookup"><span data-stu-id="91093-152">Check if it makes sense to only bring in a portion of the experience.</span></span> <span data-ttu-id="91093-153">タブ、メッセージング拡張機能、タスク モジュール、アダプティブ カード、会話型ボットの組み合わせにより、Teams で複雑なアプリを完全に構築できます。</span><span class="sxs-lookup"><span data-stu-id="91093-153">With a combination of tabs, messaging extensions, task modules, Adaptive Cards, and conversational bots you can build complex apps completely in Teams.</span></span>
<span data-ttu-id="91093-154">ユーザーが誰か、解決しようとしている問題を覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="91093-154">Remember who your users are and the problem you are trying to solve.</span></span> <span data-ttu-id="91093-155">問題のほとんどを解決するためのシステムが既にあるか、機能のサブセットを Teams に拡張する必要がありますか?</span><span class="sxs-lookup"><span data-stu-id="91093-155">Do they already have a system for solving most of the problem or you just need to extend a sub-set of the functionality into Teams?</span></span> <span data-ttu-id="91093-156">通常、ソリューションの一部を取り込む場合は、ワークフローの共有、共同作業、開始、監視に集中する必要があります。</span><span class="sxs-lookup"><span data-stu-id="91093-156">Typically, if you are going to bring in a portion of your solution, you must focus on sharing, collaborating, initiating, and monitoring workflows.</span></span>

## <a name="plan-the-onboarding-experience"></a><span data-ttu-id="91093-157">オンボーディング エクスペリエンスを計画する</span><span class="sxs-lookup"><span data-stu-id="91093-157">Plan the onboarding experience</span></span>

<span data-ttu-id="91093-158">オンボーディング エクスペリエンスは、アプリの成功と失敗の違いになります。</span><span class="sxs-lookup"><span data-stu-id="91093-158">Your onboarding experience can be the difference between success or failure for your app.</span></span> <span data-ttu-id="91093-159">アプリの各機能と、機能をインストールできるコンテキストごとに、自己紹介の計画が必要です。</span><span class="sxs-lookup"><span data-stu-id="91093-159">For each capability of your app and each context that capability can be installed in, you must have a plan for how you are going to introduce yourself.</span></span> <span data-ttu-id="91093-160">会話ボットが 1,000 人のチャネルにインストールされている場合の導入方法は、1 対 1 のチャットにインストールされる場合とは異なります。</span><span class="sxs-lookup"><span data-stu-id="91093-160">How you introduce your conversational bot when it is installed in a channel with a thousand people, is different when it is installed in a one-to-one chat.</span></span> <span data-ttu-id="91093-161">ユーザーが最初にチャネルでタブを構成すると、どうなるでしょうか。</span><span class="sxs-lookup"><span data-stu-id="91093-161">What happens when a user first configures your tab in a channel?</span></span> <span data-ttu-id="91093-162">メッセージング拡張機能を使用してカードを共有している場合は、詳細ページへの小さなリンクを追加して、アプリで他に何ができるかをユーザーに紹介するのに役立ちますか?</span><span class="sxs-lookup"><span data-stu-id="91093-162">If you are sharing cards with a messaging extension, does it make sense to add a small link to a **learn more** page to help introduce users to what else your app can do?</span></span>

<span data-ttu-id="91093-163">ユーザーが誰かを知ることにより、適切なエクスペリエンスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="91093-163">Knowing who your users are helps you to craft the right experience.</span></span> <span data-ttu-id="91093-164">ほとんどのユーザーは、アプリが何のためにあるか、または別のコンテキストで既にサービスを使用している必要がありますか?</span><span class="sxs-lookup"><span data-stu-id="91093-164">Do you expect most people to already have some context of what your app is for, or to have already used your services in another context?</span></span> <span data-ttu-id="91093-165">彼らは事前の知識を持ってアプリに来ていますか?</span><span class="sxs-lookup"><span data-stu-id="91093-165">Are they coming to your app with no prior knowledge?</span></span> <span data-ttu-id="91093-166">主要なユーザーを念頭に置いてオンボーディング エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="91093-166">Craft your onboarding experience with your key users in mind.</span></span>

<span data-ttu-id="91093-167">ユーザーは、さまざまな方法でアプリを検出できます。</span><span class="sxs-lookup"><span data-stu-id="91093-167">Remember, users can discover your app in a variety of ways.</span></span> <span data-ttu-id="91093-168">別のユーザーがコンテンツを共有するためにアプリを使用している場合は、アプリをインストールしているユーザーやアプリに導入される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="91093-168">They might be the ones installing it or they might be introduced to your app when another user uses it to share content.</span></span> <span data-ttu-id="91093-169">より多くのユーザーにアプリを使用する場合は、すべてのユーザーに自己紹介する方法を探す必要があります。</span><span class="sxs-lookup"><span data-stu-id="91093-169">If you want more users to use your app, you must look for ways to introduce yourself to everyone.</span></span>

<span data-ttu-id="91093-170">何よりも、誰もスパムを好きになんの気に入らないか覚えておいてください。</span><span class="sxs-lookup"><span data-stu-id="91093-170">Above all else, remember that nobody likes spam.</span></span> <span data-ttu-id="91093-171">個人用メッセージとチャネル メッセージを使用してブラスト処理を行うのは、インストールを迅速に解除するための良い方法です。</span><span class="sxs-lookup"><span data-stu-id="91093-171">Blasting away with personal and channel messages is a good way to get un-installed quickly!</span></span>

## <a name="plan-for-the-future"></a><span data-ttu-id="91093-172">将来の計画</span><span class="sxs-lookup"><span data-stu-id="91093-172">Plan for the future</span></span>

<span data-ttu-id="91093-173">ユーザーが現在のソリューションで使用する新しい機能を特定します。</span><span class="sxs-lookup"><span data-stu-id="91093-173">Identify which new features the user will prefer to have in the current solution.</span></span> <span data-ttu-id="91093-174">アプリに追加する新機能のロードマップがある場合、設計とアーキテクチャに影響が及ぼす可能性があります。</span><span class="sxs-lookup"><span data-stu-id="91093-174">If you have a roadmap for new features to add to the app, the design and architecture will be impacted.</span></span>

## <a name="see-also"></a><span data-ttu-id="91093-175">関連項目</span><span class="sxs-lookup"><span data-stu-id="91093-175">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="91093-176">アプリの配信方法を選ぶ</span><span class="sxs-lookup"><span data-stu-id="91093-176">Choose how to distribute your app</span></span>](../deploy-and-publish/overview.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="91093-177">効果的なタブを設計する</span><span class="sxs-lookup"><span data-stu-id="91093-177">Design effective tabs</span></span>](../../tabs/design/tabs.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="91093-178">すばらしいボットを設計する</span><span class="sxs-lookup"><span data-stu-id="91093-178">Design amazing bots</span></span>](../../bots/design/bots.md)

## <a name="next-step"></a><span data-ttu-id="91093-179">次の手順</span><span class="sxs-lookup"><span data-stu-id="91093-179">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="91093-180">使用例のマップ</span><span class="sxs-lookup"><span data-stu-id="91093-180">Map your use cases</span></span>](../../concepts/design/map-use-cases.md)
