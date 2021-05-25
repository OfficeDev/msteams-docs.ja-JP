---
title: 個人用アプリをデザインする
description: 個人用アプリを設計し、Teams UI キットをMicrosoft Teamsする方法について学習します。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 83fad746d71dd196f6efa6526f5c6c28ceac9e20
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644898"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="9e1b3-103">アプリの個人用アプリを設計Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9e1b3-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="9e1b3-104">個人用アプリには、ボット、プライベート ワークスペース、または両方を指定できます。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="9e1b3-105">コンテンツを作成または表示する場所のように機能する場合や、アプリが複数のチャネルのタブとして構成されている場合に、ユーザーが自分のコンテンツを一目で見る場合があります。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that's theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="9e1b3-106">アプリの設計をガイドするために、次の情報は、ユーザーがアプリで個人用アプリを追加、使用、および管理する方法をTeams。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="9e1b3-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="9e1b3-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="9e1b3-108">必要に応じて取得および変更できる要素を含む、包括的な個人用アプリ設計ガイドラインについては、「UI キットMicrosoft Teams参照してください。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="9e1b3-109">UI キットには、ここでは説明しないアクセシビリティや応答性のサイジングなどの重要なトピックも含まれています。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9e1b3-110">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="9e1b3-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="9e1b3-111">個人用アプリを追加する</span><span class="sxs-lookup"><span data-stu-id="9e1b3-111">Add a personal app</span></span>

<span data-ttu-id="9e1b3-112">Teams ストア (AppSource) またはアプリ のフライアウトから個人用アプリを追加するには、Teams の左側にある [その他] アイコンを選択します (次の例を参照)。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="例は、アプリのフライアウトから個人用アプリを追加する方法を示しています。" border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="9e1b3-114">個人用アプリを使用する (プライベート ワークスペース)</span><span class="sxs-lookup"><span data-stu-id="9e1b3-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="9e1b3-115">プライベート ワークスペースを使用すると、アプリのコンテンツを一か国間で表示することなく、一Teams。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="9e1b3-116">(実装ノート: プライベート ワークスペースは個人用タブ [*機能に基づいて作成*](../../build-your-first-app/build-personal-tab.md) されます)。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="9e1b3-117">Anatomy: 個人用アプリ (プライベート ワークスペース)</span><span class="sxs-lookup"><span data-stu-id="9e1b3-117">Anatomy: Personal app (private workspace)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9e1b3-118">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="9e1b3-118">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="例は、個人用タブのコンポーネント構造を示しています。" border="false":::

|<span data-ttu-id="9e1b3-120">カウンター</span><span class="sxs-lookup"><span data-stu-id="9e1b3-120">Counter</span></span>|<span data-ttu-id="9e1b3-121">説明</span><span class="sxs-lookup"><span data-stu-id="9e1b3-121">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9e1b3-122">A</span><span class="sxs-lookup"><span data-stu-id="9e1b3-122">A</span></span>|<span data-ttu-id="9e1b3-123">**アプリの属性**: アプリのロゴと名前。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-123">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="9e1b3-124">B</span><span class="sxs-lookup"><span data-stu-id="9e1b3-124">B</span></span>|<span data-ttu-id="9e1b3-125">**タブ**: 個人用アプリのナビゲーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-125">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="9e1b3-126">C</span><span class="sxs-lookup"><span data-stu-id="9e1b3-126">C</span></span>|<span data-ttu-id="9e1b3-127">**Popout ビュー**: 親ウィンドウからスタンドアロンの子ウィンドウにアプリコンテンツをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="9e1b3-128">D</span><span class="sxs-lookup"><span data-stu-id="9e1b3-128">D</span></span>|<span data-ttu-id="9e1b3-129">**[その他]** メニュー: 追加のアプリのオプションと情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-129">**More menu**: Includes additional app options and information.</span></span> <span data-ttu-id="9e1b3-130">(代わりに、タブ **設定** することもできます)。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="例は、個人用タブの構造構造を示しています。" border="false":::

|<span data-ttu-id="9e1b3-132">カウンター</span><span class="sxs-lookup"><span data-stu-id="9e1b3-132">Counter</span></span>|<span data-ttu-id="9e1b3-133">説明</span><span class="sxs-lookup"><span data-stu-id="9e1b3-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9e1b3-134">A</span><span class="sxs-lookup"><span data-stu-id="9e1b3-134">A</span></span>|<span data-ttu-id="9e1b3-135">**タブ**: 個人用アプリのナビゲーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="9e1b3-136">1</span><span class="sxs-lookup"><span data-stu-id="9e1b3-136">1</span></span>|<span data-ttu-id="9e1b3-137">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-137">**iframe**: Displays your app content.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="9e1b3-138">モバイル</span><span class="sxs-lookup"><span data-stu-id="9e1b3-138">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="例は、個人用タブのコンポーネント構造を示しています。" border="false":::

|<span data-ttu-id="9e1b3-140">カウンター</span><span class="sxs-lookup"><span data-stu-id="9e1b3-140">Counter</span></span>|<span data-ttu-id="9e1b3-141">説明</span><span class="sxs-lookup"><span data-stu-id="9e1b3-141">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9e1b3-142">A</span><span class="sxs-lookup"><span data-stu-id="9e1b3-142">A</span></span>|<span data-ttu-id="9e1b3-143">**アプリの属性**: アプリ名。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-143">**App attribution**: Your app name.</span></span>|
|<span data-ttu-id="9e1b3-144">B</span><span class="sxs-lookup"><span data-stu-id="9e1b3-144">B</span></span>|<span data-ttu-id="9e1b3-145">**タブ**: 個人用アプリのナビゲーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-145">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="9e1b3-146">C</span><span class="sxs-lookup"><span data-stu-id="9e1b3-146">C</span></span>|<span data-ttu-id="9e1b3-147">**[その他]** メニュー: 追加のアプリのオプションと情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-147">**More menu**: Includes additional app options and information.</span></span>|
|<span data-ttu-id="9e1b3-148">D</span><span class="sxs-lookup"><span data-stu-id="9e1b3-148">D</span></span>|<span data-ttu-id="9e1b3-149">**プライマリ ナビゲーション**: アプリの他の主要な機能へのTeamsします。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-149">**Primary navigation**: Provides navigation to your app other main Teams features.</span></span>|

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="例は、個人用タブの構造構造を示しています。" border="false":::

|<span data-ttu-id="9e1b3-151">カウンター</span><span class="sxs-lookup"><span data-stu-id="9e1b3-151">Counter</span></span>|<span data-ttu-id="9e1b3-152">説明</span><span class="sxs-lookup"><span data-stu-id="9e1b3-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9e1b3-153">A</span><span class="sxs-lookup"><span data-stu-id="9e1b3-153">A</span></span>|<span data-ttu-id="9e1b3-154">**タブ**: 個人用アプリのナビゲーションを提供します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-154">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="9e1b3-155">1</span><span class="sxs-lookup"><span data-stu-id="9e1b3-155">1</span></span>|<span data-ttu-id="9e1b3-156">**webview**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-156">**webview**: Displays your app content.</span></span>|

---

### <a name="designing-with-ui-templates-and-advanced-components"></a><span data-ttu-id="9e1b3-157">UI テンプレートと高度なコンポーネントを使用した設計</span><span class="sxs-lookup"><span data-stu-id="9e1b3-157">Designing with UI templates and advanced components</span></span>

<span data-ttu-id="9e1b3-158">個人用タブを設計するには、Teamsテンプレートとコンポーネントのいずれかを使用します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-158">Use one of the following Teams templates and components to help design your personal tab:</span></span>

* <span data-ttu-id="9e1b3-159">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-159">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="9e1b3-160">[タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): カンバン ボードやスイム レーンとも呼ばれるタスク ボードは、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-160">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="9e1b3-161">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を示す複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-161">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="9e1b3-162">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-162">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="9e1b3-163">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-163">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="9e1b3-164">[左ナビゲーション](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav): 左側のナビゲーション コンポーネントは、個人用アプリでナビゲーションが必要な場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-164">[Left nav](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your personal app requires some navigation.</span></span> <span data-ttu-id="9e1b3-165">一般に、ナビゲーションは最小限に抑えます。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-165">In general, you should keep navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="9e1b3-166">個人用アプリ (ボット) の使用</span><span class="sxs-lookup"><span data-stu-id="9e1b3-166">Use a personal app (bot)</span></span>

<span data-ttu-id="9e1b3-167">個人用アプリには、1 対 1 の会話とプライベート通知用のボットを含めできます (たとえば、同僚がアートボードにコメントを投稿する場合など)。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-167">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="9e1b3-168">ボットは、指定したタブで使用できます。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-168">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="9e1b3-169">解剖学: 個人用アプリ (ボット)</span><span class="sxs-lookup"><span data-stu-id="9e1b3-169">Anatomy: Personal app (bot)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="9e1b3-170">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="9e1b3-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="例は、個人用ボット コンポーネントの構造を示しています。" border="false":::

|<span data-ttu-id="9e1b3-172">カウンター</span><span class="sxs-lookup"><span data-stu-id="9e1b3-172">Counter</span></span>|<span data-ttu-id="9e1b3-173">説明</span><span class="sxs-lookup"><span data-stu-id="9e1b3-173">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9e1b3-174">A</span><span class="sxs-lookup"><span data-stu-id="9e1b3-174">A</span></span>|<span data-ttu-id="9e1b3-175">**[ボット]** タブ: たとえば、[チャット] タブ **を含** め、ボットの会話と通知にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-175">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="9e1b3-176">B</span><span class="sxs-lookup"><span data-stu-id="9e1b3-176">B</span></span>|<span data-ttu-id="9e1b3-177">**ボット メッセージ**: ボットは、多くの場合、メッセージや通知をカード (アダプティブ カードなど) の形式で送信します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-177">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="9e1b3-178">C</span><span class="sxs-lookup"><span data-stu-id="9e1b3-178">C</span></span>|<span data-ttu-id="9e1b3-179">**[作成]** ボックス : ボットにメッセージを送信する入力フィールド。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-179">**Compose box**: Input field for sending messages to the bot.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="9e1b3-180">モバイル</span><span class="sxs-lookup"><span data-stu-id="9e1b3-180">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="例は、個人用ボット コンポーネントの構造を示しています。" border="false":::

|<span data-ttu-id="9e1b3-182">カウンター</span><span class="sxs-lookup"><span data-stu-id="9e1b3-182">Counter</span></span>|<span data-ttu-id="9e1b3-183">説明</span><span class="sxs-lookup"><span data-stu-id="9e1b3-183">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9e1b3-184">A</span><span class="sxs-lookup"><span data-stu-id="9e1b3-184">A</span></span>|<span data-ttu-id="9e1b3-185">**ボット エントリ ポイント**: ユーザーが個人用アプリのボット機能にアクセスするエントリ ポイント。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-185">**Bot entry point**: Entry point for users to access the bot feature in your personal app.</span></span>|
|<span data-ttu-id="9e1b3-186">B</span><span class="sxs-lookup"><span data-stu-id="9e1b3-186">B</span></span>|<span data-ttu-id="9e1b3-187">**[戻る**] ボタン: ユーザーをプライベート ワークスペースに戻します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-187">**Back button**: Takes users back to the private workspace.</span></span>|
|<span data-ttu-id="9e1b3-188">C</span><span class="sxs-lookup"><span data-stu-id="9e1b3-188">C</span></span>|<span data-ttu-id="9e1b3-189">**ボット メッセージ**: ボットは、多くの場合、メッセージや通知をカード (アダプティブ カードなど) の形式で送信します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-189">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="9e1b3-190">D</span><span class="sxs-lookup"><span data-stu-id="9e1b3-190">D</span></span>|<span data-ttu-id="9e1b3-191">**[作成]** ボックス : ボットにメッセージを送信する入力フィールド。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-191">**Compose box**: Input field for sending messages to the bot.</span></span>|

---

## <a name="manage-a-personal-tab"></a><span data-ttu-id="9e1b3-192">個人用タブの管理</span><span class="sxs-lookup"><span data-stu-id="9e1b3-192">Manage a personal tab</span></span>

<span data-ttu-id="9e1b3-193">ユーザーは、アプリのTeamsを右クリックして、他のアプリ オプションをピン留め、削除、構成できます。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-193">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="例では、個人用アプリを管理するためのオプションを示します。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="9e1b3-195">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="9e1b3-195">Best practices</span></span>

<span data-ttu-id="9e1b3-196">これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-196">Use these recommendations to create a quality app experience.</span></span>

### <a name="tab-priority"></a><span data-ttu-id="9e1b3-197">タブの優先度</span><span class="sxs-lookup"><span data-stu-id="9e1b3-197">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="9e1b3-198">Do: 最初のタブに最も関連性の高いコンテンツを表示する</span><span class="sxs-lookup"><span data-stu-id="9e1b3-198">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="9e1b3-199">応答性の高いサイズ設定では、右側のタブが切り捨てられたり、見えなくなる場合があります。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-199">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="例は、最初のタブで最も関連性の高いコンテンツを表示する個人用アプリを示しています。" border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="9e1b3-201">[しない] セカンダリ コンテンツまたはメタデータを含むリード</span><span class="sxs-lookup"><span data-stu-id="9e1b3-201">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="9e1b3-202">標準の Web アプリと同様に、タブ ナビゲーションはアプリの主な機能を意味する順序で進む必要があります。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-202">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="例は、セカンダリ コンテンツまたはメタデータを先頭に個人アプリを示しています。" border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="9e1b3-204">タブ階層</span><span class="sxs-lookup"><span data-stu-id="9e1b3-204">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="9e1b3-205">Do: タブは等しい階層で、主要なアプリ ページを表す必要があります</span><span class="sxs-lookup"><span data-stu-id="9e1b3-205">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="9e1b3-206">タブは、アプリの主な機能とコンテンツを分類する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-206">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="9e1b3-207">応答性の高いサイズ設定では、右側のコンテンツが切り捨てられたり、見えなくなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-207">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="例は、同じ階層のタブを持つ個人用アプリを示しています。" border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="9e1b3-209">[しない]: 階層の異なるレベルを含める</span><span class="sxs-lookup"><span data-stu-id="9e1b3-209">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="9e1b3-210">コンテンツは論理的な順序で進行し、ユーザーが意味を持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-210">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="9e1b3-211">密接に関連する 2 つのタブがある場合は、それらを 1 つのタブに組み合わせることを検討してください。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-211">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="例では、階層レベルが異なる個人用アプリを示します。" border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="9e1b3-213">初回実行時エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="9e1b3-213">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="9e1b3-214">Do: 初回実行エクスペリエンスを含める</span><span class="sxs-lookup"><span data-stu-id="9e1b3-214">Do: Include a first-run experience</span></span>

<span data-ttu-id="9e1b3-215">個人用アプリを初めて使用する場合は、少なくともウェルカム 画面が表示される必要があります。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-215">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="9e1b3-216">ボットの場合は、ボットが実行できる操作を説明し、サインイン ボタンなどのクイック アクションを提供します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-216">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="例は、個人用アプリの初回実行時の操作を示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="別の例は、個人用アプリの初回実行時の操作を示しています。" border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="9e1b3-219">[しない]: 空白の画面から開始する</span><span class="sxs-lookup"><span data-stu-id="9e1b3-219">Don't: Start with a blank screen</span></span>

<span data-ttu-id="9e1b3-220">ユーザーがアプリを初めて実行した時に何も表示しない場合、ユーザーは混乱する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-220">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="例は、個人用アプリの初回実行時に実行しない操作を示しています。" border="false":::

### <a name="personalized-content"></a><span data-ttu-id="9e1b3-222">パーソナライズされたコンテンツ</span><span class="sxs-lookup"><span data-stu-id="9e1b3-222">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="9e1b3-223">Do: ユーザーに関連するアプリ コンテンツを集約する</span><span class="sxs-lookup"><span data-stu-id="9e1b3-223">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="9e1b3-224">個人用タブでもボットでも、アプリ内のユーザーのアクティビティにのみ関連するコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-224">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="例では、個人用アプリと個人用コンテンツを操作する方法を示します。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="別の例は、個人用アプリと個人用コンテンツを操作する方法を示しています。" border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="9e1b3-227">[しない]: 関連のないコンテンツまたは広いコンテンツを表示する</span><span class="sxs-lookup"><span data-stu-id="9e1b3-227">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="9e1b3-228">個人のコンテキストでは、ユーザーが参加しないチームのコンテンツを表示しない。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-228">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="9e1b3-229">個人用ボットのコンテンツは、グループではなく、個人に焦点を当てる必要があります。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-229">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="例は、個人用アプリと個人用設定されたコンテンツで何をしないかを示しています。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="別の例は、個人用アプリと個人用コンテンツを使用しない方法を示しています。" border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="9e1b3-232">複雑なアプリ機能</span><span class="sxs-lookup"><span data-stu-id="9e1b3-232">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="9e1b3-233">Do: ユーザーがブラウザーの複雑な機能にアクセスするを許可する</span><span class="sxs-lookup"><span data-stu-id="9e1b3-233">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="9e1b3-234">アプリは、Teamsのコア タスクに集中する必要がありますが、完全なスタンドアロン アプリはブラウザーで表示できます。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-234">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="例は、個人用アプリで複雑なアプリ機能を処理する方法を示しています。" border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="9e1b3-236">[しない]: アプリ全体を含める</span><span class="sxs-lookup"><span data-stu-id="9e1b3-236">Don’t: Include your entire app</span></span>

<span data-ttu-id="9e1b3-237">アプリを特別に作成しない限り、Teamsツールでは意味のない機能を使用している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-237">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="例は、個人用アプリで複雑なアプリ機能を処理しない方法を示しています。" border="false":::

## <a name="see-also"></a><span data-ttu-id="9e1b3-239">関連項目</span><span class="sxs-lookup"><span data-stu-id="9e1b3-239">See also</span></span>

<span data-ttu-id="9e1b3-240">これらの他の設計ガイドラインは、個人用アプリの範囲に応じて役立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="9e1b3-240">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="9e1b3-241">タブの設計</span><span class="sxs-lookup"><span data-stu-id="9e1b3-241">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="9e1b3-242">ボットの設計</span><span class="sxs-lookup"><span data-stu-id="9e1b3-242">Designing you bot</span></span>](../../bots/design/bots.md)
