---
title: 個人用アプリを設計する
description: Teams personal app を設計し、Microsoft Teams UI キットを取得する方法について説明します。
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 971071be9f345815f5461646d7970efdf05fd5c4
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605021"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="f31e5-103">Microsoft Teams 用の個人用アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="f31e5-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="f31e5-104">個人アプリは、ボット、プライベートワークスペース、またはその両方にすることができます。</span><span class="sxs-lookup"><span data-stu-id="f31e5-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="f31e5-105">アプリが複数のチャネルのタブとして構成されている場合は、コンテンツを作成または表示する場所のような機能をユーザーに提供することもあります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that’s theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="f31e5-106">アプリの設計をガイドするには、次の情報を参照して、ユーザーが Teams で個人アプリを追加、使用、および管理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f31e5-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="f31e5-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="f31e5-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="f31e5-108">Microsoft Teams UI キットでは、必要に応じて取得および変更できる要素を含む、アプリの総合的な設計ガイドラインを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="f31e5-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="f31e5-109">UI キットには、ここでは説明していないアクセシビリティや応答性の高いサイズ変更などの重要なトピックもあります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f31e5-110">Microsoft Teams UI Kit (Figma) を取得する</span><span class="sxs-lookup"><span data-stu-id="f31e5-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="f31e5-111">個人用アプリを追加する</span><span class="sxs-lookup"><span data-stu-id="f31e5-111">Add a personal app</span></span>

<span data-ttu-id="f31e5-112">Teams ストア (AppSource) またはアプリポップアップから個人用アプリを追加するには、Teams の左側にある [ **その他** ] アイコンを選択します (次の例を参照)。</span><span class="sxs-lookup"><span data-stu-id="f31e5-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="例は、アプリのポップアップから個人用アプリを追加する方法を示しています。" border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="f31e5-114">個人用アプリを使用する (プライベートワークスペース)</span><span class="sxs-lookup"><span data-stu-id="f31e5-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="f31e5-115">プライベートワークスペースを使用すると、Teams を離れずに、中心となる場所で重要なアプリコンテンツを表示できます。</span><span class="sxs-lookup"><span data-stu-id="f31e5-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="f31e5-116">(実装メモ: プライベートワークスペースは、[ [*個人用] タブ*](../../build-your-first-app/build-personal-tab.md) の機能に基づいています。)</span><span class="sxs-lookup"><span data-stu-id="f31e5-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="f31e5-117">分析: 個人アプリ (プライベートワークスペース)</span><span class="sxs-lookup"><span data-stu-id="f31e5-117">Anatomy: Personal app (private workspace)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="例は、個人用タブのコンポーネントの構造を示しています。" border="false":::

|<span data-ttu-id="f31e5-119">カウンター</span><span class="sxs-lookup"><span data-stu-id="f31e5-119">Counter</span></span>|<span data-ttu-id="f31e5-120">説明</span><span class="sxs-lookup"><span data-stu-id="f31e5-120">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f31e5-121">A</span><span class="sxs-lookup"><span data-stu-id="f31e5-121">A</span></span>|<span data-ttu-id="f31e5-122">**アプリの属性**: アプリのロゴと名前。</span><span class="sxs-lookup"><span data-stu-id="f31e5-122">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="f31e5-123">B</span><span class="sxs-lookup"><span data-stu-id="f31e5-123">B</span></span>|<span data-ttu-id="f31e5-124">**タブ**: 個人用アプリのナビゲーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="f31e5-124">**Tabs**: Provides navigation for your personal app.</span></span> <span data-ttu-id="f31e5-125">たとえば、[ **バージョン情報** ] タブまたは [ **ヘルプ** ] タブを含めます。</span><span class="sxs-lookup"><span data-stu-id="f31e5-125">For example, include an **About** or **Help** tab.</span></span>|
|<span data-ttu-id="f31e5-126">C</span><span class="sxs-lookup"><span data-stu-id="f31e5-126">C</span></span>|<span data-ttu-id="f31e5-127">**Popout view**: アプリのコンテンツを親ウィンドウからスタンドアロンの子ウィンドウにプッシュします。</span><span class="sxs-lookup"><span data-stu-id="f31e5-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="f31e5-128">D</span><span class="sxs-lookup"><span data-stu-id="f31e5-128">D</span></span>|<span data-ttu-id="f31e5-129">**[その他のメニュー]**: 追加のアプリ情報とオプションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f31e5-129">**More menu**: Includes additional app information and options.</span></span> <span data-ttu-id="f31e5-130">(または、タブを **設定** することもできます)。</span><span class="sxs-lookup"><span data-stu-id="f31e5-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="例は、個人用タブの構造の構造を示しています。" border="false":::

|<span data-ttu-id="f31e5-132">カウンター</span><span class="sxs-lookup"><span data-stu-id="f31e5-132">Counter</span></span>|<span data-ttu-id="f31e5-133">説明</span><span class="sxs-lookup"><span data-stu-id="f31e5-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f31e5-134">A</span><span class="sxs-lookup"><span data-stu-id="f31e5-134">A</span></span>|<span data-ttu-id="f31e5-135">**タブ**: 個人用アプリのナビゲーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="f31e5-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="f31e5-136">1 </span><span class="sxs-lookup"><span data-stu-id="f31e5-136">1</span></span>|<span data-ttu-id="f31e5-137">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="f31e5-137">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="f31e5-138">UI テンプレートを使用して設計する</span><span class="sxs-lookup"><span data-stu-id="f31e5-138">Designing with UI templates</span></span>

<span data-ttu-id="f31e5-139">次の Teams UI テンプレートのいずれかを使用して、[個人用] タブの設計に役立てることができます。</span><span class="sxs-lookup"><span data-stu-id="f31e5-139">Use one of the following Teams UI templates to help design your personal tab:</span></span>

* <span data-ttu-id="f31e5-140">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストでは、関連するアイテムを scannable 形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="f31e5-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="f31e5-141">[タスクボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): タスクボード (かんばんボードまたはスイムレーンと呼ばれることもあります) は、多くの場合、作業項目またはチケットの状態を追跡するために使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="f31e5-141">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="f31e5-142">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="f31e5-142">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="f31e5-143">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および提出するためのものです。</span><span class="sxs-lookup"><span data-stu-id="f31e5-143">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="f31e5-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行時のエクスペリエンス、エラーメッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="f31e5-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="f31e5-145">[左](../../concepts/design/design-teams-app-ui-templates.md#left-nav)ナビゲーション: タブにいくつかのナビゲーションが必要な場合は、左側のナビゲーションテンプレートが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="f31e5-145">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="f31e5-146">一般的に、タブナビゲーションは最小限にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-146">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="f31e5-147">個人アプリ (bot) を使用する</span><span class="sxs-lookup"><span data-stu-id="f31e5-147">Use a personal app (bot)</span></span>

<span data-ttu-id="f31e5-148">個人用アプリには、1対1の会話およびプライベート通知用の bot を含めることができます (たとえば、同僚がアートボードにコメントを投稿した場合)。</span><span class="sxs-lookup"><span data-stu-id="f31e5-148">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="f31e5-149">Bot は、指定したタブで使用できます。</span><span class="sxs-lookup"><span data-stu-id="f31e5-149">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="f31e5-150">分析: Personal app (bot)</span><span class="sxs-lookup"><span data-stu-id="f31e5-150">Anatomy: Personal app (bot)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="例は、パーソナル bot コンポーネントの分析を示しています。" border="false":::

|<span data-ttu-id="f31e5-152">カウンター</span><span class="sxs-lookup"><span data-stu-id="f31e5-152">Counter</span></span>|<span data-ttu-id="f31e5-153">説明</span><span class="sxs-lookup"><span data-stu-id="f31e5-153">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="f31e5-154">A</span><span class="sxs-lookup"><span data-stu-id="f31e5-154">A</span></span>|<span data-ttu-id="f31e5-155">**Bot タブ**: たとえば、ボット会話や通知にアクセスするための [ **チャット** ] タブを含みます。</span><span class="sxs-lookup"><span data-stu-id="f31e5-155">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="f31e5-156">B</span><span class="sxs-lookup"><span data-stu-id="f31e5-156">B</span></span>|<span data-ttu-id="f31e5-157">**Bot メッセージ**: bot は、メッセージと通知をカード (アダプティブカードなど) 形式で送信することがよくあります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-157">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="f31e5-158">C</span><span class="sxs-lookup"><span data-stu-id="f31e5-158">C</span></span>|<span data-ttu-id="f31e5-159">**新規作成ボックス**: bot にメッセージを送信するための入力フィールド。</span><span class="sxs-lookup"><span data-stu-id="f31e5-159">**Compose box**: Input field for sending messages to the bot.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="f31e5-160">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="f31e5-160">Best practices</span></span>

### <a name="tab-priority"></a><span data-ttu-id="f31e5-161">タブの優先度</span><span class="sxs-lookup"><span data-stu-id="f31e5-161">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="f31e5-162">実行: 最初のタブに最も関連のあるコンテンツを表示する</span><span class="sxs-lookup"><span data-stu-id="f31e5-162">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="f31e5-163">応答性の高いサイズに設定すると、右側のタブが切り捨てられるか、表示されなくなることがあります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-163">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="f31e5-165">いいえ: セカンダリコンテンツまたはメタデータをリードします。</span><span class="sxs-lookup"><span data-stu-id="f31e5-165">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="f31e5-166">標準的な web アプリと同様に、タブナビゲーションは、アプリの主要な機能を理解するために役立つ順序で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-166">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="f31e5-168">タブ階層</span><span class="sxs-lookup"><span data-stu-id="f31e5-168">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="f31e5-169">Do: タブを同じ階層にして、主要なアプリページを表す必要があります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-169">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="f31e5-170">タブでは、アプリの主要な機能とコンテンツを分類する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-170">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="f31e5-171">応答性の高いサイズに設定すると、右側のコンテンツが切り捨てられるか、表示されなくなることがあります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-171">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="f31e5-173">異なる階層のレベルを含めないでください。</span><span class="sxs-lookup"><span data-stu-id="f31e5-173">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="f31e5-174">コンテンツは、ユーザーが理解しやすくなる論理的な順序で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-174">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="f31e5-175">互いに密接な関係がある2つのタブがある場合は、1つのタブに結合することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="f31e5-175">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="f31e5-177">初回実行時エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="f31e5-177">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="f31e5-178">実行: 最初の実行環境を含める</span><span class="sxs-lookup"><span data-stu-id="f31e5-178">Do: Include a first-run experience</span></span>

<span data-ttu-id="f31e5-179">個人用アプリを初めて使用するときは、少なくともようこそ画面が表示されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-179">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="f31e5-180">Bot の場合は、bot が実行できることを説明し、サインインボタンなどのクイック操作を提供します。</span><span class="sxs-lookup"><span data-stu-id="f31e5-180">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="f31e5-183">いいえ: 空の画面で開始します</span><span class="sxs-lookup"><span data-stu-id="f31e5-183">Don't: Start with a blank screen</span></span>

<span data-ttu-id="f31e5-184">アプリを初めて実行したときに何も表示されない場合は、ユーザーが混乱する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-184">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

### <a name="personalized-content"></a><span data-ttu-id="f31e5-186">個人用コンテンツ</span><span class="sxs-lookup"><span data-stu-id="f31e5-186">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="f31e5-187">Do: ユーザーに関連するアプリコンテンツを集計する</span><span class="sxs-lookup"><span data-stu-id="f31e5-187">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="f31e5-188">個人のタブか bot かにかかわらず、アプリ内のユーザーのアクティビティのみに関連するコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f31e5-188">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="f31e5-191">[しない]: 関連性のないコンテンツまたは過度に広いコンテンツを表示する</span><span class="sxs-lookup"><span data-stu-id="f31e5-191">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="f31e5-192">個人コンテキストでは、ユーザーが所属していない teams のコンテンツは表示されません。</span><span class="sxs-lookup"><span data-stu-id="f31e5-192">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="f31e5-193">個人 bot コンテンツは、グループではなく個人に焦点を当てる必要があります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-193">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="f31e5-196">複雑なアプリ機能</span><span class="sxs-lookup"><span data-stu-id="f31e5-196">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="f31e5-197">Do: ブラウザーで複雑な機能にアクセスすることをユーザーに許可する</span><span class="sxs-lookup"><span data-stu-id="f31e5-197">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="f31e5-198">アプリは Teams のコアタスクに焦点を当てる必要がありますが、完全なスタンドアロンアプリをブラウザーで表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="f31e5-198">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="f31e5-200">アプリ全体を含めないでください。</span><span class="sxs-lookup"><span data-stu-id="f31e5-200">Don’t: Include your entire app</span></span>

<span data-ttu-id="f31e5-201">特に Teams 用のアプリを作成していない場合は、コラボレーションツールで意味を持たない機能が存在する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-201">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="例は、個人用アプリのベストプラクティスを示しています。" border="false":::

## <a name="manage-a-personal-tab"></a><span data-ttu-id="f31e5-203">個人用タブを管理する</span><span class="sxs-lookup"><span data-stu-id="f31e5-203">Manage a personal tab</span></span>

<span data-ttu-id="f31e5-204">Teams の左側で、ユーザーは個人用アプリを右クリックして、他のアプリオプションを固定、削除、および構成できます。</span><span class="sxs-lookup"><span data-stu-id="f31e5-204">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="例は、個人用アプリを管理するためのオプションを示しています。" border="false":::

## <a name="learn-more"></a><span data-ttu-id="f31e5-206">詳細情報</span><span class="sxs-lookup"><span data-stu-id="f31e5-206">Learn more</span></span>

<span data-ttu-id="f31e5-207">個人アプリの範囲によっては、次のような設計ガイドラインが役になることがあります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-207">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="f31e5-208">タブのデザイン</span><span class="sxs-lookup"><span data-stu-id="f31e5-208">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="f31e5-209">Bot のデザイン</span><span class="sxs-lookup"><span data-stu-id="f31e5-209">Designing you bot</span></span>](../../bots/design/bots.md)

## <a name="validate-your-design"></a><span data-ttu-id="f31e5-210">設計を検証する</span><span class="sxs-lookup"><span data-stu-id="f31e5-210">Validate your design</span></span>

<span data-ttu-id="f31e5-211">アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="f31e5-211">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f31e5-212">設計検証ガイドラインの確認</span><span class="sxs-lookup"><span data-stu-id="f31e5-212">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
