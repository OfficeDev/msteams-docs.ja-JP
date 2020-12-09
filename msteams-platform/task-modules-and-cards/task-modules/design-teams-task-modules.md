---
title: タスクモジュールを設計する
author: heath-hamilton
description: Teams アプリのタスクモジュールを設計し、Microsoft Teams UI キットを取得する方法について説明します。
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 41584ecf58ca7718290e58e5845549e4579dac64
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606415"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a><span data-ttu-id="d23f1-103">Microsoft Teams アプリのタスクモジュールを設計する</span><span class="sxs-lookup"><span data-stu-id="d23f1-103">Designing task modules for your Microsoft Teams app</span></span>

<span data-ttu-id="d23f1-104">タスクモジュールを使用して、Teams アプリでモーダルポップアップエクスペリエンスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-104">You can create modal popup experiences in your Teams app with task modules.</span></span> <span data-ttu-id="d23f1-105">この機能を使用すると、リッチメディアと情報を表示したり、複雑なタスクを実行したりできます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-105">Use this capability to display rich media and information or complete a complex task.</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="例は、タスクモジュールを示しています。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d23f1-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="d23f1-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d23f1-108">Microsoft Teams UI キットでは、必要に応じて取得および変更できる要素を含む、包括的なタスクモジュールデザインガイドラインを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-108">You can find more comprehensive task module design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d23f1-109">Microsoft Teams UI Kit (Figma) を取得する</span><span class="sxs-lookup"><span data-stu-id="d23f1-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a><span data-ttu-id="d23f1-110">タスクモジュールを開く</span><span class="sxs-lookup"><span data-stu-id="d23f1-110">Open a task module</span></span>

<span data-ttu-id="d23f1-111">タスクモジュールは、アプリのほとんどすべての場所から起動できます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-111">Task modules can be launched from almost anywhere in your app.</span></span>

* <span data-ttu-id="d23f1-112">**Tab**: タスクモジュールは、タブまたは iframe 内の任意のリンクから起動できます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-112">**Tab**: A task module can be launched from any link within a tab or iframe.</span></span> <span data-ttu-id="d23f1-113">ユーザーが相互作用に集中するシナリオで使用します。</span><span class="sxs-lookup"><span data-stu-id="d23f1-113">Use in scenarios where you want the user to focus on an interaction.</span></span>
* <span data-ttu-id="d23f1-114">**Bot**: タスクモジュールは、ボットメッセージ内のリンクから起動できます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-114">**Bot**: A task module can be launched from a link inside a bot message.</span></span>
* <span data-ttu-id="d23f1-115">**アダプティブカード**: タスクモジュールは、ユーザーがボタンを選択したときに、アダプティブカード (メッセージング内線または bot が送信) から起動できます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-115">**Adaptive Card**: A task module can be launched from an Adaptive Card (sent with a messaging extension or by a bot) when a user selects a button.</span></span>
* <span data-ttu-id="d23f1-116">**メッセージング拡張機能 (アクションコマンド)**: メッセージング拡張機能を使用すると、メッセージのコンテンツに対して特定のアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-116">**Messaging extension (action commands)**: Messaging extensions allow you to take a particular action on message content.</span></span> <span data-ttu-id="d23f1-117">アクションを選択すると、タスクモジュールが開きます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-117">Selecting an action opens a task module.</span></span>
* <span data-ttu-id="d23f1-118">**メッセージング拡張機能 (新規作成ボックスコンテキスト)**: [新規作成] ボックスでは、標準のポップアップではなく、タスクモジュールを開くためのメッセージング拡張機能をデザインできます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-118">**Messaging extension (compose box context)**: In the compose box, you can design a messaging extension to open a task module instead of the typical flyout.</span></span> <span data-ttu-id="d23f1-119">フォームの入力など、複雑な対話のためのタスクモジュールを予約します。</span><span class="sxs-lookup"><span data-stu-id="d23f1-119">Reserve task modules for complex interactions, such as completing a form.</span></span>

## <a name="anatomy"></a><span data-ttu-id="d23f1-120">構造</span><span class="sxs-lookup"><span data-stu-id="d23f1-120">Anatomy</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="タスクモジュールの UI 構造を示す図" border="false":::

<span data-ttu-id="d23f1-122">タスクモジュールは非常に柔軟なサーフェスです。</span><span class="sxs-lookup"><span data-stu-id="d23f1-122">Task modules are very flexible surfaces.</span></span> <span data-ttu-id="d23f1-123">これらは、他の UI テンプレートを使用して、パートナーが作成したエクスペリエンスをホストするために、iframe を使用して構築できます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-123">They can be built with iframes, pulling in other UI templates, to host partner-built experiences.</span></span> <span data-ttu-id="d23f1-124">これは、洗練された快適な作業に適しています。</span><span class="sxs-lookup"><span data-stu-id="d23f1-124">This is preferred for the most polished experience.</span></span>

<span data-ttu-id="d23f1-125">また、 [アダプティブカード](../../task-modules-and-cards/cards/design-effective-cards.md) フレームワークを使用してビルドすることもできます。これは、一般的なシナリオ (フォームなど) をより簡単に実行する方法です。</span><span class="sxs-lookup"><span data-stu-id="d23f1-125">They can also be built with the [Adaptive Card](../../task-modules-and-cards/cards/design-effective-cards.md) framework, which can be a simpler and faster way to execute common scenarios (such as forms).</span></span>

|<span data-ttu-id="d23f1-126">カウンター</span><span class="sxs-lookup"><span data-stu-id="d23f1-126">Counter</span></span>|<span data-ttu-id="d23f1-127">説明</span><span class="sxs-lookup"><span data-stu-id="d23f1-127">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d23f1-128">1</span><span class="sxs-lookup"><span data-stu-id="d23f1-128">1</span></span>|<span data-ttu-id="d23f1-129">**アプリ アイコン**</span><span class="sxs-lookup"><span data-stu-id="d23f1-129">**App icon**</span></span>|
|<span data-ttu-id="d23f1-130">2 </span><span class="sxs-lookup"><span data-stu-id="d23f1-130">2</span></span>|<span data-ttu-id="d23f1-131">**アプリ名**: アプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="d23f1-131">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="d23f1-132">3 </span><span class="sxs-lookup"><span data-stu-id="d23f1-132">3</span></span>|<span data-ttu-id="d23f1-133">**ヘッダー**: ヘッダーをクリアで簡潔にします。</span><span class="sxs-lookup"><span data-stu-id="d23f1-133">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="d23f1-134">ユーザーが完了する必要のあるタスクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="d23f1-134">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="d23f1-135">4 </span><span class="sxs-lookup"><span data-stu-id="d23f1-135">4</span></span>|<span data-ttu-id="d23f1-136">**[閉じる] ボタン**: 挿入するアプリコンテンツをユーザーが検索できるようにします。</span><span class="sxs-lookup"><span data-stu-id="d23f1-136">**Close button**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="d23f1-137">5 </span><span class="sxs-lookup"><span data-stu-id="d23f1-137">5</span></span>|<span data-ttu-id="d23f1-138">**iframe**: アプリコンテンツをホストする、応答性の高いスペース。</span><span class="sxs-lookup"><span data-stu-id="d23f1-138">**iframe**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="d23f1-139">6 </span><span class="sxs-lookup"><span data-stu-id="d23f1-139">6</span></span>|<span data-ttu-id="d23f1-140">**アクション (オプション)**: アプリコンテンツに関連するボタン。</span><span class="sxs-lookup"><span data-stu-id="d23f1-140">**Actions (optional)**: Buttons related to your app content.</span></span>|

## <a name="designing-with-ui-templates"></a><span data-ttu-id="d23f1-141">UI テンプレートを使用して設計する</span><span class="sxs-lookup"><span data-stu-id="d23f1-141">Designing with UI templates</span></span>

<span data-ttu-id="d23f1-142">タスクモジュール内の一般的なレイアウトにテンプレートを使用することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="d23f1-142">Consider using templates for common layouts inside your task modules.</span></span> <span data-ttu-id="d23f1-143">それぞれが、自分のシナリオに合わせて、またはカスタマイズしたブランド化された優れたデザインを作成するために、小さなコンポーネントで構成されています。</span><span class="sxs-lookup"><span data-stu-id="d23f1-143">Each one is made up of smaller components to create an elegant, responsive design that can be used out of the box or customized for your scenario or with your brand look and feel.</span></span>

* <span data-ttu-id="d23f1-144">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストでは、関連するアイテムを scannable 形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="d23f1-144">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="d23f1-145">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および提出するためのものです。</span><span class="sxs-lookup"><span data-stu-id="d23f1-145">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="d23f1-146">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行時のエクスペリエンス、エラーメッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-146">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="examples"></a><span data-ttu-id="d23f1-147">例</span><span class="sxs-lookup"><span data-stu-id="d23f1-147">Examples</span></span>

### <a name="list"></a><span data-ttu-id="d23f1-148">リスト</span><span class="sxs-lookup"><span data-stu-id="d23f1-148">List</span></span>

<span data-ttu-id="d23f1-149">タスクモジュールでは、簡単にスキャンできるので、適切に作業できます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-149">Lists work nicely in a task module because they’re easy to scan.</span></span>

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="タスクモジュール内のリストの例です。" border="false":::

### <a name="form"></a><span data-ttu-id="d23f1-151">フォーム</span><span class="sxs-lookup"><span data-stu-id="d23f1-151">Form</span></span>

<span data-ttu-id="d23f1-152">タスクモジュールは、連続したユーザー入力とインライン検証を含むフォームを表示するのに便利な場所です。</span><span class="sxs-lookup"><span data-stu-id="d23f1-152">Task modules are a great place to surface forms with sequential user inputs and inline validation.</span></span> <span data-ttu-id="d23f1-153">フォーム要素を埋め込む方法として、アダプティブカードを活用することができます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-153">You can leverage Adaptive Cards as a way to embed form elements.</span></span>

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="タスクモジュールのフォームの例" border="false":::

### <a name="sign-in"></a><span data-ttu-id="d23f1-155">サインイン</span><span class="sxs-lookup"><span data-stu-id="d23f1-155">Sign in</span></span>

<span data-ttu-id="d23f1-156">一連のタスクモジュールを使用してフォーカスのあるサインインまたはサインアップフローを作成し、ユーザーが連続した手順を簡単に移動できるようにします。</span><span class="sxs-lookup"><span data-stu-id="d23f1-156">Create a focused sign in or sign-up flow with a series of task modules, letting users move easily through sequential steps.</span></span>

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="タスクモジュールでのサインイン操作の例。" border="false":::

### <a name="media"></a><span data-ttu-id="d23f1-158">メディア</span><span class="sxs-lookup"><span data-stu-id="d23f1-158">Media</span></span>

<span data-ttu-id="d23f1-159">タスクモジュールにメディアコンテンツを埋め込んで、フォーカスのある表示環境を実現します。</span><span class="sxs-lookup"><span data-stu-id="d23f1-159">Embed media content in a task module for a focused viewing experience.</span></span>

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="タスクモジュール内のメディアコンテンツの例。" border="false":::

### <a name="empty-state"></a><span data-ttu-id="d23f1-161">空の状態</span><span class="sxs-lookup"><span data-stu-id="d23f1-161">Empty state</span></span>

<span data-ttu-id="d23f1-162">ウェルカムメッセージ、エラーメッセージ、および成功メッセージに使用します。</span><span class="sxs-lookup"><span data-stu-id="d23f1-162">Use for welcome, error, and success messages.</span></span>

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="タスクモジュール内の空の状態の例です。" border="false":::

### <a name="image-gallery"></a><span data-ttu-id="d23f1-164">イメージ ギャラリー</span><span class="sxs-lookup"><span data-stu-id="d23f1-164">Image gallery</span></span>

<span data-ttu-id="d23f1-165">Iframe 内にギャラリーカルーセルを埋め込みます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-165">Embed a gallery carousel inside an iframe.</span></span>

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="タスクモジュール内のイメージギャラリーの例です。" border="false":::

### <a name="poll"></a><span data-ttu-id="d23f1-167">間隔</span><span class="sxs-lookup"><span data-stu-id="d23f1-167">Poll</span></span>

<span data-ttu-id="d23f1-168">この例では、アダプティブカードから起動された投票結果を示します。</span><span class="sxs-lookup"><span data-stu-id="d23f1-168">This example shows poll results launched from an Adaptive Card.</span></span>

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="タスクモジュール内の投票の例" border="false":::

## <a name="best-practices"></a><span data-ttu-id="d23f1-170">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="d23f1-170">Best practices</span></span>

### <a name="usability"></a><span data-ttu-id="d23f1-171">使いやすさ</span><span class="sxs-lookup"><span data-stu-id="d23f1-171">Usability</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a><span data-ttu-id="d23f1-173">Do: 一度に1つのタスクモジュールを使用する</span><span class="sxs-lookup"><span data-stu-id="d23f1-173">Do: Use one task module at a time</span></span>

<span data-ttu-id="d23f1-174">目標は、すべてのタスクを完了した後にユーザーにフォーカスを移動することです。</span><span class="sxs-lookup"><span data-stu-id="d23f1-174">The goal is to focus the user on completing a task after all!</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a><span data-ttu-id="d23f1-176">[いいえ: タスクモジュールの上にダイアログを表示する]</span><span class="sxs-lookup"><span data-stu-id="d23f1-176">Don't: Pop a dialog on top of a task module</span></span>

<span data-ttu-id="d23f1-177">これにより、unfocused で混乱したユーザー環境が作成されます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-177">This creates an unfocused, confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive"></a><span data-ttu-id="d23f1-178">速い</span><span class="sxs-lookup"><span data-stu-id="d23f1-178">Responsive</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a><span data-ttu-id="d23f1-180">実行: コンテンツが応答していることを確認する</span><span class="sxs-lookup"><span data-stu-id="d23f1-180">Do: Make sure the content is responsive</span></span>

<span data-ttu-id="d23f1-181">タスクモジュールでホストされているアダプティブカードはモバイルデバイスで適切に表示されますが、iframe を使用してアプリコンテンツをホストする場合は、UI が応答可能であることと、デバイス間で適切に動作することを確認してください。</span><span class="sxs-lookup"><span data-stu-id="d23f1-181">While Adaptive Cards hosted in a task module render well on mobile devices, if you choose to use an iframe to host app content, make sure the UI is responsive and works well across devices.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="dont-use-horizontal-scrollbars"></a><span data-ttu-id="d23f1-183">いいえ: 水平スクロールバーを使用します。</span><span class="sxs-lookup"><span data-stu-id="d23f1-183">Don't: Use horizontal scrollbars</span></span>

<span data-ttu-id="d23f1-184">コンテンツを重視しすぎないようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d23f1-184">It's a best practice to keep content focused and not too lengthy.</span></span> <span data-ttu-id="d23f1-185">スクロールが必要な場合は、水平方向にスクロールします。</span><span class="sxs-lookup"><span data-stu-id="d23f1-185">If a scroll is necessary, scroll vertically and not horizontally.</span></span>

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a><span data-ttu-id="d23f1-186">合理</span><span class="sxs-lookup"><span data-stu-id="d23f1-186">Simplicity</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="do-keep-it-short"></a><span data-ttu-id="d23f1-188">実行: 短時間で保持する</span><span class="sxs-lookup"><span data-stu-id="d23f1-188">Do: Keep it short</span></span>

<span data-ttu-id="d23f1-189">マルチステップウィザードは簡単に作成できますが、これは必ずしも必要であるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="d23f1-189">You can easily create a multi-step wizard, but that doesn't necessarily mean you should!</span></span> <span data-ttu-id="d23f1-190">複数画面タスクモジュールは、受信メッセージが煩雑で、tempt ユーザーが終了するため、問題を発生させる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d23f1-190">A multi-screen task module can be problematic because incoming messages are distracting and tempt users to exit.</span></span> <span data-ttu-id="d23f1-191">タスクが実際に関係している場合は、タスクモジュールではなく、完全な web ページにポップアウトします。</span><span class="sxs-lookup"><span data-stu-id="d23f1-191">If your task is really involved, pop out to a full webpage instead of a task module.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="dont-do-long-interactions"></a><span data-ttu-id="d23f1-193">いいえ: 長時間の操作を実行する</span><span class="sxs-lookup"><span data-stu-id="d23f1-193">Don't: Do long interactions</span></span>

<span data-ttu-id="d23f1-194">相互作用を短くして、ポイントにするようにしてください。</span><span class="sxs-lookup"><span data-stu-id="d23f1-194">Try to keep your interactions short and to the point.</span></span>

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a><span data-ttu-id="d23f1-195">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="d23f1-195">Error messages</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="do-use-inline-error-messages"></a><span data-ttu-id="d23f1-197">Do: インラインエラーメッセージを使用する</span><span class="sxs-lookup"><span data-stu-id="d23f1-197">Do: Use inline error messages</span></span>

<span data-ttu-id="d23f1-198">インラインエラー処理のガイドラインについては、「forms UI template」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d23f1-198">See the forms UI template for guidelines on inline error handling.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="タスクモジュールのベストプラクティスを示す例。" border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a><span data-ttu-id="d23f1-200">[いいえ: ダイアログにエラーメッセージを表示する。</span><span class="sxs-lookup"><span data-stu-id="d23f1-200">Don't: Put error messages in dialogs</span></span>

<span data-ttu-id="d23f1-201">タスクモジュールの上部にあるダイアログにエラーメッセージを表示しないようにします。</span><span class="sxs-lookup"><span data-stu-id="d23f1-201">Don't pop an error message in a dialog on top of a task modules.</span></span> <span data-ttu-id="d23f1-202">これにより、わかりやすいユーザー環境が作成されます。</span><span class="sxs-lookup"><span data-stu-id="d23f1-202">It creates a confusing user experience.</span></span>

   :::column-end:::
:::row-end:::
