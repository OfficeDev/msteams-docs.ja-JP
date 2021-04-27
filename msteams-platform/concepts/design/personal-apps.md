---
title: 個人用アプリをデザインする
description: Teams 個人用アプリを設計し、Microsoft Teams UI キットを取得する方法について説明します。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 8302f3768034014ef5a446effeee0603afe4a5f4
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020759"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="d1539-103">Microsoft Teams 用の個人用アプリの設計</span><span class="sxs-lookup"><span data-stu-id="d1539-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="d1539-104">個人用アプリには、ボット、プライベート ワークスペース、または両方を指定できます。</span><span class="sxs-lookup"><span data-stu-id="d1539-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="d1539-105">コンテンツを作成または表示する場所のように機能する場合や、アプリが複数のチャネルのタブとして構成されている場合に、ユーザーが自分のコンテンツを一目で見る場合があります。</span><span class="sxs-lookup"><span data-stu-id="d1539-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that's theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="d1539-106">アプリの設計をガイドするために、次の情報は、Teams で個人アプリを追加、使用、および管理する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d1539-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d1539-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="d1539-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d1539-108">Microsoft Teams UI Kit には、必要に応じて取得および変更できる要素を含む、包括的な個人用アプリ設計ガイドラインがあります。</span><span class="sxs-lookup"><span data-stu-id="d1539-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="d1539-109">UI キットには、ここでは説明しないアクセシビリティや応答性のサイジングなどの重要なトピックも含まれています。</span><span class="sxs-lookup"><span data-stu-id="d1539-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d1539-110">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="d1539-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="d1539-111">個人用アプリを追加する</span><span class="sxs-lookup"><span data-stu-id="d1539-111">Add a personal app</span></span>

<span data-ttu-id="d1539-112">Teams ストア (AppSource) またはアプリ のフライアウトから個人用アプリを追加するには、Teamsの左側にある [その他] アイコンを選択します (次の例を参照)。</span><span class="sxs-lookup"><span data-stu-id="d1539-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="例は、アプリのフライアウトから個人用アプリを追加する方法を示しています。" border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="d1539-114">個人用アプリを使用する (プライベート ワークスペース)</span><span class="sxs-lookup"><span data-stu-id="d1539-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="d1539-115">プライベート ワークスペースを使用すると、Teams を離れることなく、中央の場所でユーザーにとって意味のあるアプリ コンテンツを表示できます。</span><span class="sxs-lookup"><span data-stu-id="d1539-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="d1539-116">(実装ノート: プライベート ワークスペースは個人用タブ [*機能に基づいて作成*](../../build-your-first-app/build-personal-tab.md) されます)。</span><span class="sxs-lookup"><span data-stu-id="d1539-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="d1539-117">Anatomy: 個人用アプリ (プライベート ワークスペース)</span><span class="sxs-lookup"><span data-stu-id="d1539-117">Anatomy: Personal app (private workspace)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="例は、個人用タブのコンポーネント構造を示しています。" border="false":::

|<span data-ttu-id="d1539-119">カウンター</span><span class="sxs-lookup"><span data-stu-id="d1539-119">Counter</span></span>|<span data-ttu-id="d1539-120">説明</span><span class="sxs-lookup"><span data-stu-id="d1539-120">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d1539-121">A</span><span class="sxs-lookup"><span data-stu-id="d1539-121">A</span></span>|<span data-ttu-id="d1539-122">**アプリの属性**: アプリのロゴと名前。</span><span class="sxs-lookup"><span data-stu-id="d1539-122">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="d1539-123">B</span><span class="sxs-lookup"><span data-stu-id="d1539-123">B</span></span>|<span data-ttu-id="d1539-124">**タブ**: 個人用アプリのナビゲーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="d1539-124">**Tabs**: Provides navigation for your personal app.</span></span> <span data-ttu-id="d1539-125">たとえば、[概要] タブまたは **[ヘルプ]** タブ **を含** めることができます。</span><span class="sxs-lookup"><span data-stu-id="d1539-125">For example, include an **About** or **Help** tab.</span></span>|
|<span data-ttu-id="d1539-126">C</span><span class="sxs-lookup"><span data-stu-id="d1539-126">C</span></span>|<span data-ttu-id="d1539-127">**Popout ビュー**: 親ウィンドウからスタンドアロンの子ウィンドウにアプリコンテンツをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="d1539-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="d1539-128">D</span><span class="sxs-lookup"><span data-stu-id="d1539-128">D</span></span>|<span data-ttu-id="d1539-129">**[その他]** メニュー: 追加のアプリ情報とオプションが含まれます。</span><span class="sxs-lookup"><span data-stu-id="d1539-129">**More menu**: Includes additional app information and options.</span></span> <span data-ttu-id="d1539-130">(または、[設定] を **タブ** にすることもできます)。</span><span class="sxs-lookup"><span data-stu-id="d1539-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="例は、個人用タブの構造構造を示しています。" border="false":::

|<span data-ttu-id="d1539-132">カウンター</span><span class="sxs-lookup"><span data-stu-id="d1539-132">Counter</span></span>|<span data-ttu-id="d1539-133">説明</span><span class="sxs-lookup"><span data-stu-id="d1539-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d1539-134">A</span><span class="sxs-lookup"><span data-stu-id="d1539-134">A</span></span>|<span data-ttu-id="d1539-135">**タブ**: 個人用アプリのナビゲーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="d1539-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="d1539-136">1</span><span class="sxs-lookup"><span data-stu-id="d1539-136">1</span></span>|<span data-ttu-id="d1539-137">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="d1539-137">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="d1539-138">UI テンプレートを使用した設計</span><span class="sxs-lookup"><span data-stu-id="d1539-138">Designing with UI templates</span></span>

<span data-ttu-id="d1539-139">個人用タブを設計するには、次のいずれかの Teams UI テンプレートを使用します。</span><span class="sxs-lookup"><span data-stu-id="d1539-139">Use one of the following Teams UI templates to help design your personal tab:</span></span>

* <span data-ttu-id="d1539-140">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="d1539-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="d1539-141">[タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): カンバン ボードやスイム レーンとも呼ばれるタスク ボードは、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="d1539-141">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="d1539-142">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を示す複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="d1539-142">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="d1539-143">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。</span><span class="sxs-lookup"><span data-stu-id="d1539-143">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="d1539-144">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="d1539-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="d1539-145">[左ナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左側のナビゲーション テンプレートは、タブにナビゲーションが必要な場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="d1539-145">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="d1539-146">一般に、タブ ナビゲーションは最小限に抑えます。</span><span class="sxs-lookup"><span data-stu-id="d1539-146">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="d1539-147">個人用アプリ (ボット) の使用</span><span class="sxs-lookup"><span data-stu-id="d1539-147">Use a personal app (bot)</span></span>

<span data-ttu-id="d1539-148">個人用アプリには、1 対 1 の会話とプライベート通知用のボットを含めできます (たとえば、同僚がアートボードにコメントを投稿する場合など)。</span><span class="sxs-lookup"><span data-stu-id="d1539-148">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="d1539-149">ボットは、指定したタブで使用できます。</span><span class="sxs-lookup"><span data-stu-id="d1539-149">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="d1539-150">解剖学: 個人用アプリ (ボット)</span><span class="sxs-lookup"><span data-stu-id="d1539-150">Anatomy: Personal app (bot)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="例は、個人用ボット コンポーネントの構造を示しています。" border="false":::

|<span data-ttu-id="d1539-152">カウンター</span><span class="sxs-lookup"><span data-stu-id="d1539-152">Counter</span></span>|<span data-ttu-id="d1539-153">説明</span><span class="sxs-lookup"><span data-stu-id="d1539-153">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d1539-154">A</span><span class="sxs-lookup"><span data-stu-id="d1539-154">A</span></span>|<span data-ttu-id="d1539-155">**[ボット]** タブ: たとえば、[チャット] タブ **を含** め、ボットの会話と通知にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="d1539-155">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="d1539-156">B</span><span class="sxs-lookup"><span data-stu-id="d1539-156">B</span></span>|<span data-ttu-id="d1539-157">**ボット メッセージ**: ボットは、多くの場合、メッセージや通知をカード (アダプティブ カードなど) の形式で送信します。</span><span class="sxs-lookup"><span data-stu-id="d1539-157">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="d1539-158">C</span><span class="sxs-lookup"><span data-stu-id="d1539-158">C</span></span>|<span data-ttu-id="d1539-159">**[作成]** ボックス : ボットにメッセージを送信する入力フィールド。</span><span class="sxs-lookup"><span data-stu-id="d1539-159">**Compose box**: Input field for sending messages to the bot.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="d1539-160">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="d1539-160">Best practices</span></span>

### <a name="tab-priority"></a><span data-ttu-id="d1539-161">タブの優先度</span><span class="sxs-lookup"><span data-stu-id="d1539-161">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="d1539-162">Do: 最初のタブに最も関連性の高いコンテンツを表示する</span><span class="sxs-lookup"><span data-stu-id="d1539-162">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="d1539-163">応答性の高いサイズ設定では、右側のタブが切り捨てられたり、見えなくなる場合があります。</span><span class="sxs-lookup"><span data-stu-id="d1539-163">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="例は、個人用アプリのベスト プラクティスを示しています。" border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="d1539-165">[しない] セカンダリ コンテンツまたはメタデータを含むリード</span><span class="sxs-lookup"><span data-stu-id="d1539-165">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="d1539-166">標準の Web アプリと同様に、タブ ナビゲーションはアプリの主な機能を意味する順序で進む必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1539-166">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="個人用アプリのベスト プラクティスの例。" border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="d1539-168">タブ階層</span><span class="sxs-lookup"><span data-stu-id="d1539-168">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="d1539-169">Do: タブは等しい階層で、主要なアプリ ページを表す必要があります</span><span class="sxs-lookup"><span data-stu-id="d1539-169">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="d1539-170">タブは、アプリの主な機能とコンテンツを分類する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1539-170">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="d1539-171">応答性の高いサイズ設定では、右側のコンテンツが切り捨てられたり、見えなくなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d1539-171">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="例は、個人用アプリのベスト プラクティスを示しています。" border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="d1539-173">[しない]: 階層の異なるレベルを含める</span><span class="sxs-lookup"><span data-stu-id="d1539-173">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="d1539-174">コンテンツは論理的な順序で進行し、ユーザーが意味を持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1539-174">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="d1539-175">密接に関連する 2 つのタブがある場合は、それらを 1 つのタブに組み合わせることを検討してください。</span><span class="sxs-lookup"><span data-stu-id="d1539-175">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="例では、個人用アプリのベスト プラクティスを表示します。" border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="d1539-177">初回実行時エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="d1539-177">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="d1539-178">Do: 初回実行エクスペリエンスを含める</span><span class="sxs-lookup"><span data-stu-id="d1539-178">Do: Include a first-run experience</span></span>

<span data-ttu-id="d1539-179">個人用アプリを初めて使用する場合は、少なくともウェルカム 画面が表示される必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1539-179">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="d1539-180">ボットの場合は、ボットが実行できる操作を説明し、サインイン ボタンなどのクイック アクションを提供します。</span><span class="sxs-lookup"><span data-stu-id="d1539-180">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="図は、個人用アプリのベスト プラクティスを示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="個人用アプリのベスト プラクティスの図。" border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="d1539-183">[しない]: 空白の画面から開始する</span><span class="sxs-lookup"><span data-stu-id="d1539-183">Don't: Start with a blank screen</span></span>

<span data-ttu-id="d1539-184">ユーザーがアプリを初めて実行した時に何も表示しない場合、ユーザーは混乱する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d1539-184">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="図は、個人用アプリのベスト プラクティスを表示します。" border="false":::

### <a name="personalized-content"></a><span data-ttu-id="d1539-186">パーソナライズされたコンテンツ</span><span class="sxs-lookup"><span data-stu-id="d1539-186">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="d1539-187">Do: ユーザーに関連するアプリ コンテンツを集約する</span><span class="sxs-lookup"><span data-stu-id="d1539-187">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="d1539-188">個人用タブでもボットでも、アプリ内のユーザーのアクティビティにのみ関連するコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="d1539-188">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="例では、個人用アプリのベスト プラクティスを示します。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="この例では、個人用アプリのベスト プラクティスを示します。" border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="d1539-191">[しない]: 関連のないコンテンツまたは広いコンテンツを表示する</span><span class="sxs-lookup"><span data-stu-id="d1539-191">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="d1539-192">個人のコンテキストでは、ユーザーが参加しないチームのコンテンツを表示しない。</span><span class="sxs-lookup"><span data-stu-id="d1539-192">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="d1539-193">個人用ボットのコンテンツは、グループではなく、個人に焦点を当てる必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1539-193">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="開示は、個人用アプリのベスト プラクティスの例です。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="サンプルは、個人用アプリのベスト プラクティスを示しています。" border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="d1539-196">複雑なアプリ機能</span><span class="sxs-lookup"><span data-stu-id="d1539-196">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="d1539-197">Do: ユーザーがブラウザーの複雑な機能にアクセスするを許可する</span><span class="sxs-lookup"><span data-stu-id="d1539-197">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="d1539-198">アプリは Teams のコア タスクに集中する必要がありますが、完全なスタンドアロン アプリはブラウザーで表示できます。</span><span class="sxs-lookup"><span data-stu-id="d1539-198">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="サンプルは、個人用アプリのベスト プラクティスを示しています。" border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="d1539-200">[しない]: アプリ全体を含める</span><span class="sxs-lookup"><span data-stu-id="d1539-200">Don’t: Include your entire app</span></span>

<span data-ttu-id="d1539-201">Teams 専用のアプリを作成しない限り、おそらくコラボレーション ツールでは意味のない機能があります。</span><span class="sxs-lookup"><span data-stu-id="d1539-201">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="図は、個人用アプリのベスト プラクティスを示しています。" border="false":::

## <a name="manage-a-personal-tab"></a><span data-ttu-id="d1539-203">個人用タブの管理</span><span class="sxs-lookup"><span data-stu-id="d1539-203">Manage a personal tab</span></span>

<span data-ttu-id="d1539-204">Teams の左側では、ユーザーは個人用アプリを右クリックして、他のアプリ オプションをピン留め、削除、および構成できます。</span><span class="sxs-lookup"><span data-stu-id="d1539-204">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="例では、個人用アプリを管理するためのオプションを示します。" border="false":::

## <a name="learn-more"></a><span data-ttu-id="d1539-206">詳細情報</span><span class="sxs-lookup"><span data-stu-id="d1539-206">Learn more</span></span>

<span data-ttu-id="d1539-207">これらの他の設計ガイドラインは、個人用アプリの範囲に応じて役立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="d1539-207">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="d1539-208">タブの設計</span><span class="sxs-lookup"><span data-stu-id="d1539-208">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="d1539-209">ボットの設計</span><span class="sxs-lookup"><span data-stu-id="d1539-209">Designing you bot</span></span>](../../bots/design/bots.md)

## <a name="validate-your-design"></a><span data-ttu-id="d1539-210">デザインを検証する</span><span class="sxs-lookup"><span data-stu-id="d1539-210">Validate your design</span></span>

<span data-ttu-id="d1539-211">AppSource にアプリを公開する予定がある場合、アプリの提出時に失敗する原因となるデザイン上の問題を理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="d1539-211">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d1539-212">デザイン検証ガイドラインをチェックする</span><span class="sxs-lookup"><span data-stu-id="d1539-212">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
