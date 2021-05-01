---
title: タスク モジュールをデザインする
author: heath-hamilton
description: アプリのタスク モジュールを設計し、Teams UI キットをMicrosoft Teamsする方法について学習します。
localization_priority: Normal
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 347ce42c41706f698e2f8897a0518aae0850a275
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101731"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a><span data-ttu-id="0a324-103">アプリ用のタスク モジュールMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="0a324-103">Designing task modules for your Microsoft Teams app</span></span>

<span data-ttu-id="0a324-104">タスク モジュールを使用して、Teamsポップアップ エクスペリエンスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="0a324-104">You can create modal popup experiences in your Teams app with task modules.</span></span> <span data-ttu-id="0a324-105">リッチ メディアと情報を表示したり、複雑なタスクを完了したりするには、この機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="0a324-105">Use this capability to display rich media and information or complete a complex task.</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="タスク モジュールの例を示します。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="0a324-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="0a324-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="0a324-108">必要に応じて取得および変更できる要素を含む、より包括的なタスク モジュール設計ガイドラインについては、「UI キットMicrosoft Teams参照してください。</span><span class="sxs-lookup"><span data-stu-id="0a324-108">You can find more comprehensive task module design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a324-109">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="0a324-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a><span data-ttu-id="0a324-110">タスク モジュールを開く</span><span class="sxs-lookup"><span data-stu-id="0a324-110">Open a task module</span></span>

<span data-ttu-id="0a324-111">タスク モジュールは、アプリのほぼすべての場所から起動できます。</span><span class="sxs-lookup"><span data-stu-id="0a324-111">Task modules can be launched from almost anywhere in your app.</span></span>

* <span data-ttu-id="0a324-112">**Tab**: タブ内の任意のリンクからタスク モジュールを起動できます。ユーザーが対話に集中するシナリオで使用します。</span><span class="sxs-lookup"><span data-stu-id="0a324-112">**Tab**: A task module can be launched from any link within a tab. Use in scenarios where you want the user to focus on an interaction.</span></span>
* <span data-ttu-id="0a324-113">**ボット**: ボット メッセージ内のリンクからタスク モジュールを起動できます。</span><span class="sxs-lookup"><span data-stu-id="0a324-113">**Bot**: A task module can be launched from a link inside a bot message.</span></span>
* <span data-ttu-id="0a324-114">**アダプティブ カード**: ユーザーがボタンを選択すると、アダプティブ カード (メッセージング拡張機能またはボットによって送信される) からタスク モジュールを起動できます。</span><span class="sxs-lookup"><span data-stu-id="0a324-114">**Adaptive Card**: A task module can be launched from an Adaptive Card (sent with a messaging extension or by a bot) when a user selects a button.</span></span>
* <span data-ttu-id="0a324-115">**メッセージング拡張機能 (アクション コマンド)**: メッセージング拡張機能を使用すると、メッセージ コンテンツに対して特定のアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="0a324-115">**Messaging extension (action commands)**: Messaging extensions allow you to take a particular action on message content.</span></span> <span data-ttu-id="0a324-116">アクションを選択すると、タスク モジュールが開きます。</span><span class="sxs-lookup"><span data-stu-id="0a324-116">Selecting an action opens a task module.</span></span>
* <span data-ttu-id="0a324-117">**メッセージング拡張機能 (作成ボックス** コンテキスト) : 作成ボックスで、メッセージング拡張機能を設計して、一般的なフライアウトではなくタスク モジュールを開くことができます。</span><span class="sxs-lookup"><span data-stu-id="0a324-117">**Messaging extension (compose box context)**: In the compose box, you can design a messaging extension to open a task module instead of the typical flyout.</span></span> <span data-ttu-id="0a324-118">フォームの入力など、複雑な操作のためにタスク モジュールを予約します。</span><span class="sxs-lookup"><span data-stu-id="0a324-118">Reserve task modules for complex interactions, such as completing a form.</span></span>

## <a name="anatomy"></a><span data-ttu-id="0a324-119">構造</span><span class="sxs-lookup"><span data-stu-id="0a324-119">Anatomy</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="タスク モジュールの UI 構造を示す図。" border="false":::

<span data-ttu-id="0a324-121">タスク モジュールは非常に柔軟なサーフェスです。</span><span class="sxs-lookup"><span data-stu-id="0a324-121">Task modules are very flexible surfaces.</span></span> <span data-ttu-id="0a324-122">iframes を使用して構築し、他の UI テンプレートを引き込み、パートナーが構築したエクスペリエンスをホストできます。</span><span class="sxs-lookup"><span data-stu-id="0a324-122">They can be built with iframes, pulling in other UI templates, to host partner-built experiences.</span></span> <span data-ttu-id="0a324-123">これは、最も洗練されたエクスペリエンスに優先されます。</span><span class="sxs-lookup"><span data-stu-id="0a324-123">This is preferred for the most polished experience.</span></span>

<span data-ttu-id="0a324-124">また、アダプティブ カード フレームワーク[](../../task-modules-and-cards/cards/design-effective-cards.md)を使用して構築することもできます。これは、一般的なシナリオ (フォームなど) をより簡単かつ迅速に実行できます。</span><span class="sxs-lookup"><span data-stu-id="0a324-124">They can also be built with the [Adaptive Card](../../task-modules-and-cards/cards/design-effective-cards.md) framework, which can be a simpler and faster way to execute common scenarios (such as forms).</span></span>

|<span data-ttu-id="0a324-125">カウンター</span><span class="sxs-lookup"><span data-stu-id="0a324-125">Counter</span></span>|<span data-ttu-id="0a324-126">説明</span><span class="sxs-lookup"><span data-stu-id="0a324-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0a324-127">1</span><span class="sxs-lookup"><span data-stu-id="0a324-127">1</span></span>|<span data-ttu-id="0a324-128">**アプリ アイコン**</span><span class="sxs-lookup"><span data-stu-id="0a324-128">**App icon**</span></span>|
|<span data-ttu-id="0a324-129">2</span><span class="sxs-lookup"><span data-stu-id="0a324-129">2</span></span>|<span data-ttu-id="0a324-130">**アプリ名**: アプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="0a324-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="0a324-131">3</span><span class="sxs-lookup"><span data-stu-id="0a324-131">3</span></span>|<span data-ttu-id="0a324-132">**ヘッダー**: ヘッダーを明確かつ簡潔にします。</span><span class="sxs-lookup"><span data-stu-id="0a324-132">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="0a324-133">ユーザーが完了するタスクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="0a324-133">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="0a324-134">4</span><span class="sxs-lookup"><span data-stu-id="0a324-134">4</span></span>|<span data-ttu-id="0a324-135">**[閉じる**] ボタン: ユーザーが挿入するアプリ コンテンツを検索できます。</span><span class="sxs-lookup"><span data-stu-id="0a324-135">**Close button**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="0a324-136">5</span><span class="sxs-lookup"><span data-stu-id="0a324-136">5</span></span>|<span data-ttu-id="0a324-137">**iframe**: アプリ コンテンツをホストするレスポンシブ スペース。</span><span class="sxs-lookup"><span data-stu-id="0a324-137">**iframe**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="0a324-138">6</span><span class="sxs-lookup"><span data-stu-id="0a324-138">6</span></span>|<span data-ttu-id="0a324-139">**アクション (省略可能)**: アプリコンテンツに関連するボタン。</span><span class="sxs-lookup"><span data-stu-id="0a324-139">**Actions (optional)**: Buttons related to your app content.</span></span>|

## <a name="designing-with-ui-templates"></a><span data-ttu-id="0a324-140">UI テンプレートを使用した設計</span><span class="sxs-lookup"><span data-stu-id="0a324-140">Designing with UI templates</span></span>

<span data-ttu-id="0a324-141">タスク モジュール内の一般的なレイアウトにテンプレートを使用する方法を検討してください。</span><span class="sxs-lookup"><span data-stu-id="0a324-141">Consider using templates for common layouts inside your task modules.</span></span> <span data-ttu-id="0a324-142">各コンポーネントは、小規模なコンポーネントで構成され、使い慣れた、またはシナリオやブランドの外観に合わせてカスタマイズできる、エレガントで応答性の高いデザインを作成します。</span><span class="sxs-lookup"><span data-stu-id="0a324-142">Each one is made up of smaller components to create an elegant, responsive design that can be used out of the box or customized for your scenario or with your brand look and feel.</span></span>

* <span data-ttu-id="0a324-143">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="0a324-143">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="0a324-144">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。</span><span class="sxs-lookup"><span data-stu-id="0a324-144">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="0a324-145">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="0a324-145">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="examples"></a><span data-ttu-id="0a324-146">例</span><span class="sxs-lookup"><span data-stu-id="0a324-146">Examples</span></span>

### <a name="list"></a><span data-ttu-id="0a324-147">一覧表示</span><span class="sxs-lookup"><span data-stu-id="0a324-147">List</span></span>

<span data-ttu-id="0a324-148">リストはスキャンが簡単なので、タスク モジュールでうまく機能します。</span><span class="sxs-lookup"><span data-stu-id="0a324-148">Lists work nicely in a task module because they’re easy to scan.</span></span>

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="タスク モジュールのリストの例。" border="false":::

### <a name="form"></a><span data-ttu-id="0a324-150">フォーム</span><span class="sxs-lookup"><span data-stu-id="0a324-150">Form</span></span>

<span data-ttu-id="0a324-151">タスク モジュールは、シーケンシャル ユーザー入力とインライン検証を備え、フォームを表面化する最適な場所です。</span><span class="sxs-lookup"><span data-stu-id="0a324-151">Task modules are a great place to surface forms with sequential user inputs and inline validation.</span></span> <span data-ttu-id="0a324-152">フォーム要素を埋め込む方法としてアダプティブ カードを活用できます。</span><span class="sxs-lookup"><span data-stu-id="0a324-152">You can leverage Adaptive Cards as a way to embed form elements.</span></span>

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="タスク モジュール内のフォームの例。" border="false":::

### <a name="sign-in"></a><span data-ttu-id="0a324-154">サインインする</span><span class="sxs-lookup"><span data-stu-id="0a324-154">Sign in</span></span>

<span data-ttu-id="0a324-155">一連のタスク モジュールを使用して、フォーカスのあるサインインフローまたはサインアップ フローを作成し、ユーザーが順次ステップを簡単に移動できます。</span><span class="sxs-lookup"><span data-stu-id="0a324-155">Create a focused sign in or sign-up flow with a series of task modules, letting users move easily through sequential steps.</span></span>

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="タスク モジュールでのサインイン エクスペリエンスの例。" border="false":::

### <a name="media"></a><span data-ttu-id="0a324-157">メディア</span><span class="sxs-lookup"><span data-stu-id="0a324-157">Media</span></span>

<span data-ttu-id="0a324-158">フォーカスされた表示エクスペリエンスのために、タスク モジュールにメディア コンテンツを埋め込む。</span><span class="sxs-lookup"><span data-stu-id="0a324-158">Embed media content in a task module for a focused viewing experience.</span></span>

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="タスク モジュールのメディア コンテンツの例。" border="false":::

### <a name="empty-state"></a><span data-ttu-id="0a324-160">空の状態</span><span class="sxs-lookup"><span data-stu-id="0a324-160">Empty state</span></span>

<span data-ttu-id="0a324-161">ウェルカム メッセージ、エラー メッセージ、成功メッセージに使用します。</span><span class="sxs-lookup"><span data-stu-id="0a324-161">Use for welcome, error, and success messages.</span></span>

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="タスク モジュールの空の状態の例。" border="false":::

### <a name="image-gallery"></a><span data-ttu-id="0a324-163">イメージ ギャラリー</span><span class="sxs-lookup"><span data-stu-id="0a324-163">Image gallery</span></span>

<span data-ttu-id="0a324-164">ギャラリーカルーセルを iframe に埋め込む。</span><span class="sxs-lookup"><span data-stu-id="0a324-164">Embed a gallery carousel in an iframe.</span></span>

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="タスク モジュールのイメージ ギャラリーの例。" border="false":::

### <a name="poll"></a><span data-ttu-id="0a324-166">Poll</span><span class="sxs-lookup"><span data-stu-id="0a324-166">Poll</span></span>

<span data-ttu-id="0a324-167">次の使用例は、アダプティブ カードから起動されたポーリング結果を示しています。</span><span class="sxs-lookup"><span data-stu-id="0a324-167">This example shows poll results launched from an Adaptive Card.</span></span> <span data-ttu-id="0a324-168">ポーリングは、タスク モジュール内に配置できます。</span><span class="sxs-lookup"><span data-stu-id="0a324-168">The poll can be placed inside a task module, too.</span></span>

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="タスク モジュールのポーリングの例。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="0a324-170">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="0a324-170">Best practices</span></span>

<span data-ttu-id="0a324-171">これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="0a324-171">Use these recommendations to create a quality app experience.</span></span>

### <a name="usability"></a><span data-ttu-id="0a324-172">使いやすさ</span><span class="sxs-lookup"><span data-stu-id="0a324-172">Usability</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="タスク モジュールのベスト プラクティス (一度に 1 つのタスク モジュール) を表示する例。" border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a><span data-ttu-id="0a324-174">Do: 一度に 1 つのタスク モジュールを使用する</span><span class="sxs-lookup"><span data-stu-id="0a324-174">Do: Use one task module at a time</span></span>

<span data-ttu-id="0a324-175">目標は、ユーザーが結局タスクを完了する作業に集中する方法です。</span><span class="sxs-lookup"><span data-stu-id="0a324-175">The goal is to focus the user on completing a task after all!</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="タスク モジュールのベスト プラクティスを表示する例 (タスク モジュールの上にダイアログを表示する)。" border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a><span data-ttu-id="0a324-177">[しない] タスク モジュールの上にダイアログを表示する</span><span class="sxs-lookup"><span data-stu-id="0a324-177">Don't: Pop a dialog on top of a task module</span></span>

<span data-ttu-id="0a324-178">これにより、焦点が合わされ、わかりにくいユーザー エクスペリエンスが作成されます。</span><span class="sxs-lookup"><span data-stu-id="0a324-178">This creates an unfocused, confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive"></a><span data-ttu-id="0a324-179">速い</span><span class="sxs-lookup"><span data-stu-id="0a324-179">Responsive</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (コンテンツが応答可能な状態を確認してください)。" border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a><span data-ttu-id="0a324-181">Do: コンテンツの応答性を確認する</span><span class="sxs-lookup"><span data-stu-id="0a324-181">Do: Make sure the content is responsive</span></span>

<span data-ttu-id="0a324-182">タスク モジュールでホストされているアダプティブ カードはモバイル デバイスで適切にレンダリングされます。iframe を使用してアプリ コンテンツをホストする場合は、UI が応答性に優れた、デバイス間で適切に動作する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0a324-182">While Adaptive Cards hosted in a task module render well on mobile devices, if you choose to use an iframe to host app content, make sure the UI is responsive and works well across devices.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (水平方向のスクロール バーを使用しない)。" border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a><span data-ttu-id="0a324-184">[しない]: 水平方向のスクロール バーを使用する</span><span class="sxs-lookup"><span data-stu-id="0a324-184">Don't: Use horizontal scroll bars</span></span>

<span data-ttu-id="0a324-185">コンテンツに焦点を当て、長すぎずに維持するベスト プラクティスです。</span><span class="sxs-lookup"><span data-stu-id="0a324-185">It's a best practice to keep content focused and not too lengthy.</span></span> <span data-ttu-id="0a324-186">スクロールが必要な場合は、水平方向ではなく垂直方向にスクロールします。</span><span class="sxs-lookup"><span data-stu-id="0a324-186">If a scroll is necessary, scroll vertically and not horizontally.</span></span>

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a><span data-ttu-id="0a324-187">シンプルさ</span><span class="sxs-lookup"><span data-stu-id="0a324-187">Simplicity</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (短くする)。" border="false":::

#### <a name="do-keep-it-short"></a><span data-ttu-id="0a324-189">Do: 短くする</span><span class="sxs-lookup"><span data-stu-id="0a324-189">Do: Keep it short</span></span>

<span data-ttu-id="0a324-190">マルチステップ ウィザードは簡単に作成できますが、必ずしも必要とは限りません。</span><span class="sxs-lookup"><span data-stu-id="0a324-190">You can easily create a multi-step wizard, but that doesn't necessarily mean you should!</span></span> <span data-ttu-id="0a324-191">複数画面のタスク モジュールは、受信メッセージが気を散らし、ユーザーが終了を思い出すので、問題になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0a324-191">A multi-screen task module can be problematic because incoming messages are distracting and tempt users to exit.</span></span> <span data-ttu-id="0a324-192">タスクが実際に関係している場合は、タスク モジュールの代わりに完全な Web ページにポップアウトします。</span><span class="sxs-lookup"><span data-stu-id="0a324-192">If your task is really involved, pop out to a full webpage instead of a task module.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (長い対話を行う必要があります)。" border="false":::

#### <a name="dont-have-long-interactions"></a><span data-ttu-id="0a324-194">Don't: 長い対話を行う</span><span class="sxs-lookup"><span data-stu-id="0a324-194">Don't: Have long interactions</span></span>

<span data-ttu-id="0a324-195">やり取りを短くしてポイントにしてください。</span><span class="sxs-lookup"><span data-stu-id="0a324-195">Try to keep your interactions short and to the point.</span></span>

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a><span data-ttu-id="0a324-196">エラー メッセージ</span><span class="sxs-lookup"><span data-stu-id="0a324-196">Error messages</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (インライン エラー メッセージを使用)。" border="false":::

#### <a name="do-use-inline-error-messages"></a><span data-ttu-id="0a324-198">Do: インライン エラー メッセージを使用する</span><span class="sxs-lookup"><span data-stu-id="0a324-198">Do: Use inline error messages</span></span>

<span data-ttu-id="0a324-199">インライン エラー処理のガイドラインについては、フォーム UI テンプレートを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0a324-199">See the forms UI template for guidelines on inline error handling.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="タスク モジュールのベスト プラクティスを示す例 (ダイアログにエラー メッセージを表示する)。" border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a><span data-ttu-id="0a324-201">[しない] ダイアログにエラー メッセージを表示する</span><span class="sxs-lookup"><span data-stu-id="0a324-201">Don't: Put error messages in dialogs</span></span>

<span data-ttu-id="0a324-202">タスク モジュールの上のダイアログにエラー メッセージを表示しません。</span><span class="sxs-lookup"><span data-stu-id="0a324-202">Don't pop an error message in a dialog on top of a task modules.</span></span> <span data-ttu-id="0a324-203">わかりにくいユーザー エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="0a324-203">It creates a confusing user experience.</span></span>

   :::column-end:::
:::row-end:::
