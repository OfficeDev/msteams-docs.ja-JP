---
title: デスクトップ、Web、モバイルのデザイン タブ
description: デスクトップ、Web、モバイル用のTeamsタブを設計し、UI キットのMicrosoft Teams説明します。
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f1823a064cd182d0271aa97bef58ec724c7819b3
ms.sourcegitcommit: 33a43c61f27ae750776616b2cf90159455d8ba6c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2021
ms.locfileid: "52721844"
---
# <a name="design-your-tab-for-microsoft-teams"></a><span data-ttu-id="b2de3-103">タブをデザインしてMicrosoft Teams</span><span class="sxs-lookup"><span data-stu-id="b2de3-103">Design your tab for Microsoft Teams</span></span>

<span data-ttu-id="b2de3-104">タブは、アプリ コンテンツの大きなキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="b2de3-104">A tab is a large canvas for your app content.</span></span> <span data-ttu-id="b2de3-105">アプリの設計をガイドするために、次の情報は、ユーザーがアプリのタブを追加、使用、および管理する方法をTeams。</span><span class="sxs-lookup"><span data-stu-id="b2de3-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="b2de3-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="b2de3-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="b2de3-107">必要に応じて取得および変更できる要素を含む、包括的なタブ設計ガイドラインについては、「UI キットMicrosoft Teams参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2de3-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="b2de3-108">UI キットには、ここでは説明しないアクセシビリティや応答性のサイジングなどの重要なトピックも含まれています。</span><span class="sxs-lookup"><span data-stu-id="b2de3-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b2de3-109">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="b2de3-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="b2de3-110">タブの追加</span><span class="sxs-lookup"><span data-stu-id="b2de3-110">Add a tab</span></span>

<span data-ttu-id="b2de3-111">タブは、ストア (AppSource) Teams、または次のいずれかのコンテキストで追加できます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="b2de3-112">チャット</span><span class="sxs-lookup"><span data-stu-id="b2de3-112">Chat</span></span>
* <span data-ttu-id="b2de3-113">チャネル</span><span class="sxs-lookup"><span data-stu-id="b2de3-113">Channel</span></span>
* <span data-ttu-id="b2de3-114">会議 (会議の前、中、または後)</span><span class="sxs-lookup"><span data-stu-id="b2de3-114">Meeting (before, during, or after the meeting)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="b2de3-115">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="b2de3-115">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="b2de3-116">次の例は、ユーザーがチャネルにタブを追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="b2de3-116">The following example shows how users can add a tab in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="例は、チャネルに追加されるタブを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="b2de3-118">モバイル</span><span class="sxs-lookup"><span data-stu-id="b2de3-118">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="b2de3-119">ユーザーは、チャネル (下の例) で [その他] ボタンを選択するか、追加したチャットを選択してタブにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-119">Users can access tabs by selecting the **More** button in the channel (example below) or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-design-access-tab.png" alt-text="例は、チャネルに追加されるモバイル タブを示しています。" border="false":::

---

## <a name="set-up-a-tab"></a><span data-ttu-id="b2de3-121">タブを設定する</span><span class="sxs-lookup"><span data-stu-id="b2de3-121">Set up a tab</span></span>

<span data-ttu-id="b2de3-122">チャネル、チャット、または会議タブとしてアプリを追加する短いセットアップ プロセスがあります。エクスペリエンスは主にユーザーが行います。</span><span class="sxs-lookup"><span data-stu-id="b2de3-122">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="b2de3-123">たとえば、アプリの使い方とオプションの設定について説明できます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-123">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="b2de3-124">ユーザーを認証する必要がある場合は、ここにサインイン 手順を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2de3-124">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-dialog"></a><span data-ttu-id="b2de3-125">タブ構成ダイアログ</span><span class="sxs-lookup"><span data-stu-id="b2de3-125">Tab configuration dialog</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="例は、タブ構成モーダルを示しています。" border="false":::

### <a name="anatomy-tab-configuration-dialog"></a><span data-ttu-id="b2de3-127">構造: タブ構成ダイアログ</span><span class="sxs-lookup"><span data-stu-id="b2de3-127">Anatomy: Tab configuration dialog</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="タブ構成モーダルの UI 構造を示す図。" border="false":::

|<span data-ttu-id="b2de3-129">カウンター</span><span class="sxs-lookup"><span data-stu-id="b2de3-129">Counter</span></span>|<span data-ttu-id="b2de3-130">説明</span><span class="sxs-lookup"><span data-stu-id="b2de3-130">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b2de3-131">1</span><span class="sxs-lookup"><span data-stu-id="b2de3-131">1</span></span>|<span data-ttu-id="b2de3-132">**アプリのロゴ**: アプリのフルカラー アプリ ロゴ。</span><span class="sxs-lookup"><span data-stu-id="b2de3-132">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="b2de3-133">2</span><span class="sxs-lookup"><span data-stu-id="b2de3-133">2</span></span>|<span data-ttu-id="b2de3-134">**アプリ名**: アプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="b2de3-134">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="b2de3-135">3</span><span class="sxs-lookup"><span data-stu-id="b2de3-135">3</span></span>|<span data-ttu-id="b2de3-136">**iframe**: アプリのコンテンツのレスポンシブ スペース (タブ設定や認証など)。</span><span class="sxs-lookup"><span data-stu-id="b2de3-136">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="b2de3-137">4</span><span class="sxs-lookup"><span data-stu-id="b2de3-137">4</span></span>|<span data-ttu-id="b2de3-138">**リンクについて**: アプリの詳細、アプリで必要なアクセス許可、プライバシー ポリシーと利用規約へのリンクなど、アプリに関する詳細を示すダイアログを開きます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-138">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>|
|<span data-ttu-id="b2de3-139">5</span><span class="sxs-lookup"><span data-stu-id="b2de3-139">5</span></span>|<span data-ttu-id="b2de3-140">**[閉じる**] ボタン: ダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-140">**Close button**: Closes the dialog.</span></span>|
|<span data-ttu-id="b2de3-141">6</span><span class="sxs-lookup"><span data-stu-id="b2de3-141">6</span></span>|<span data-ttu-id="b2de3-142">**[チーム メンバーに通知する] オプション**: ダイアログボックスは、ユーザーが他のユーザーにタブを追加したと知らせる投稿を作成する必要がある場合に、ユーザーに尋ねるメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-142">**Notify team members option**: The dialog asks users if they want to create a post letting others know they added a tab.</span></span>|
|<span data-ttu-id="b2de3-143">7</span><span class="sxs-lookup"><span data-stu-id="b2de3-143">7</span></span>|<span data-ttu-id="b2de3-144">**[戻る**] ボタン: ダイアログが開いた場所に基づいて、前の手順に進みます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-144">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="b2de3-145">8</span><span class="sxs-lookup"><span data-stu-id="b2de3-145">8</span></span>|<span data-ttu-id="b2de3-146">**[保存]** ボタン: タブのセットアップを完了します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-146">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="b2de3-147">シングル サインオンを使用したタブ認証</span><span class="sxs-lookup"><span data-stu-id="b2de3-147">Tab authentication with single sign-on</span></span>

<span data-ttu-id="b2de3-148">ユーザーが Microsoft 資格情報を使用して最初にサインインする必要がある手順を追加できます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-148">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="b2de3-149">この認証方法は、シングル サインオン (SSO) と呼ばれています。</span><span class="sxs-lookup"><span data-stu-id="b2de3-149">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="例では、タブ認証画面を表示します。" border="false":::

### <a name="design-a-tab-setup-with-ui-templates"></a><span data-ttu-id="b2de3-151">UI テンプレートを使用してタブセットアップを設計する</span><span class="sxs-lookup"><span data-stu-id="b2de3-151">Design a tab setup with UI templates</span></span>

<span data-ttu-id="b2de3-152">次のいずれかの UI テンプレートを使用Teams、タブセットアップエクスペリエンスの設計に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-152">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="b2de3-153">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-153">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="b2de3-154">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。</span><span class="sxs-lookup"><span data-stu-id="b2de3-154">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="b2de3-155">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-155">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="b2de3-156">タブを表示する</span><span class="sxs-lookup"><span data-stu-id="b2de3-156">View a tab</span></span>

<span data-ttu-id="b2de3-157">タブは、タスク ボードやダッシュボードTeams重要な情報など、共同作業コンテンツを表示できる画面全体の Web エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-157">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="b2de3-158">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="b2de3-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="例では、タスク ボードを含むタブを示します。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="b2de3-160">モバイル</span><span class="sxs-lookup"><span data-stu-id="b2de3-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab.png" alt-text="例は、タスク ボードを持つモバイル タブを示しています。" border="false":::

---

### <a name="anatomy-tab"></a><span data-ttu-id="b2de3-162">構造: タブ</span><span class="sxs-lookup"><span data-stu-id="b2de3-162">Anatomy: Tab</span></span>

# <a name="desktop"></a>[<span data-ttu-id="b2de3-163">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="b2de3-163">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="タブの UI 構造を示す図。" border="false":::

|<span data-ttu-id="b2de3-165">カウンター</span><span class="sxs-lookup"><span data-stu-id="b2de3-165">Counter</span></span>|<span data-ttu-id="b2de3-166">説明</span><span class="sxs-lookup"><span data-stu-id="b2de3-166">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b2de3-167">1</span><span class="sxs-lookup"><span data-stu-id="b2de3-167">1</span></span>|<span data-ttu-id="b2de3-168">**タブ名**: タブのナビゲーション ラベル。</span><span class="sxs-lookup"><span data-stu-id="b2de3-168">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="b2de3-169">2</span><span class="sxs-lookup"><span data-stu-id="b2de3-169">2</span></span>|<span data-ttu-id="b2de3-170">**タブ オーバーフロー**: 名前の変更や削除などのタブ アクションを開きます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-170">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="b2de3-171">3</span><span class="sxs-lookup"><span data-stu-id="b2de3-171">3</span></span>|<span data-ttu-id="b2de3-172">**タブ チャット**: 右側にチャットを開き、ユーザーがコンテンツの横で会話を行えます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-172">**Tab chat**: Opens a chat to the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="b2de3-173">4</span><span class="sxs-lookup"><span data-stu-id="b2de3-173">4</span></span>|<span data-ttu-id="b2de3-174">**iframe**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-174">**iframe**: Displays your app content.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="b2de3-175">モバイル</span><span class="sxs-lookup"><span data-stu-id="b2de3-175">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab-anatomy.png" alt-text="タブの UI 構造を示す図。" border="false":::

|<span data-ttu-id="b2de3-177">カウンター</span><span class="sxs-lookup"><span data-stu-id="b2de3-177">Counter</span></span>|<span data-ttu-id="b2de3-178">説明</span><span class="sxs-lookup"><span data-stu-id="b2de3-178">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b2de3-179">1</span><span class="sxs-lookup"><span data-stu-id="b2de3-179">1</span></span>|<span data-ttu-id="b2de3-180">**タブ名**: タブのナビゲーション ラベル。</span><span class="sxs-lookup"><span data-stu-id="b2de3-180">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="b2de3-181">2</span><span class="sxs-lookup"><span data-stu-id="b2de3-181">2</span></span>|<span data-ttu-id="b2de3-182">**タブ チャット**: ユーザーがコンテンツの横で会話を行えるチャットを開きます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-182">**Tab chat**: Opens a chat that allows users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="b2de3-183">3</span><span class="sxs-lookup"><span data-stu-id="b2de3-183">3</span></span>|<span data-ttu-id="b2de3-184">**webview**: アプリのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-184">**webview**: Displays your app content.</span></span>|

---

### <a name="designing-a-tab-with-ui-templates-and-advanced-components"></a><span data-ttu-id="b2de3-185">UI テンプレートと高度なコンポーネントを使用したタブの設計</span><span class="sxs-lookup"><span data-stu-id="b2de3-185">Designing a tab with UI templates and advanced components</span></span>

<span data-ttu-id="b2de3-186">タブ エクスペリエンスの設計に役立Teams、次のいずれかのテンプレートとコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-186">Use one of the following Teams templates and components to help design your tab experience:</span></span>

* <span data-ttu-id="b2de3-187">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-187">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="b2de3-188">[タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): カンバン ボードやスイム レーンとも呼ばれるタスク ボードは、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="b2de3-188">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="b2de3-189">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を示す複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="b2de3-189">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="b2de3-190">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。</span><span class="sxs-lookup"><span data-stu-id="b2de3-190">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="b2de3-191">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-191">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="b2de3-192">[左ナビゲーション](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): 左側のナビゲーション コンポーネントは、タブにナビゲーションが必要な場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-192">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="b2de3-193">一般に、タブ ナビゲーションは最小限に抑えます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-193">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="b2de3-194">タブを使用して共同作業を行う</span><span class="sxs-lookup"><span data-stu-id="b2de3-194">Use a tab to collaborate</span></span>

<span data-ttu-id="b2de3-195">タブは、中央の場所でのコンテンツに関する会話を容易にするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-195">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="b2de3-196">スレッドディスカッション</span><span class="sxs-lookup"><span data-stu-id="b2de3-196">Thread discussion</span></span>

<span data-ttu-id="b2de3-197">ユーザーは、新しいタブを追加すると、チャネルまたはチャットに自動的に投稿できます。これにより、チーム メンバーに新しいコンテンツが通知され、タブへのリンクが提供されるだけでなく、ユーザーはタブについて話し始めできます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-197">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="b2de3-198">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="b2de3-198">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="例は、チャネル スレッドで説明されているタブを示しています。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="b2de3-200">モバイル</span><span class="sxs-lookup"><span data-stu-id="b2de3-200">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-channel.png" alt-text="例は、チャネル スレッドで説明されているモバイル タブを示しています。" border="false":::

---

### <a name="tab-chat"></a><span data-ttu-id="b2de3-202">タブ チャット</span><span class="sxs-lookup"><span data-stu-id="b2de3-202">Tab chat</span></span>

<span data-ttu-id="b2de3-203">ユーザーは、表示しているタブ コンテンツの横で会話を行えます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-203">Users can have a conversation next to the tab content they're viewing.</span></span> <span data-ttu-id="b2de3-204">デスクトップでは、チャットがアプリ コンテンツの横に開きます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-204">On desktop, the chat opens to the side of the app content.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="b2de3-205">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="b2de3-205">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="例では、右側にチャットが開いているタブが表示されます。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="b2de3-207">モバイル</span><span class="sxs-lookup"><span data-stu-id="b2de3-207">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-side-chat.png" alt-text="例は、コンテキスト内のチャット領域を持つモバイル タブを示しています。" border="false":::

---

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="b2de3-209">アクセス許可と役割ベースのビュー</span><span class="sxs-lookup"><span data-stu-id="b2de3-209">Permissions and role-based views</span></span>

<span data-ttu-id="b2de3-210">ユーザーのアクセス許可に応じて、タブエクスペリエンスが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="b2de3-210">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="b2de3-211">たとえば、1 人のユーザーがサインインせずにタブにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-211">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="b2de3-212">ただし、別のユーザーはサインインして、少し異なるコンテンツを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2de3-212">Another user, however, must sign in and see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="b2de3-213">タブの管理</span><span class="sxs-lookup"><span data-stu-id="b2de3-213">Manage a tab</span></span>

<span data-ttu-id="b2de3-214">タブの名前の変更、削除、または変更を行うオプションを含めできます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-214">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="b2de3-215">構造: タブ メニュー</span><span class="sxs-lookup"><span data-stu-id="b2de3-215">Anatomy: Tab menu</span></span>

# <a name="desktop"></a>[<span data-ttu-id="b2de3-216">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="b2de3-216">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="タブ メニューの UI 構造を示す図。" border="false":::

|<span data-ttu-id="b2de3-218">カウンター</span><span class="sxs-lookup"><span data-stu-id="b2de3-218">Counter</span></span>|<span data-ttu-id="b2de3-219">説明</span><span class="sxs-lookup"><span data-stu-id="b2de3-219">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b2de3-220">1</span><span class="sxs-lookup"><span data-stu-id="b2de3-220">1</span></span>|<span data-ttu-id="b2de3-221">**設定**: (オプション) 追加後にタブの設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-221">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="b2de3-222">2</span><span class="sxs-lookup"><span data-stu-id="b2de3-222">2</span></span>|<span data-ttu-id="b2de3-223">**名前** の変更 : ユーザーは、タブにチャネル、チャット、または会議に意味のある名前を付けることができます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-223">**Rename**: Users can give the tab a name that’s meaningful to the channel, chat, or meeting.</span></span>|
|<span data-ttu-id="b2de3-224">3</span><span class="sxs-lookup"><span data-stu-id="b2de3-224">3</span></span>|<span data-ttu-id="b2de3-225">**[削除**] : チャネル、チャット、または会議からタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-225">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="b2de3-226">モバイル</span><span class="sxs-lookup"><span data-stu-id="b2de3-226">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-manage-tab-menu-anatomy.png" alt-text="モバイル タブ メニューの UI 構造を示す図。" border="false":::

|<span data-ttu-id="b2de3-228">カウンター</span><span class="sxs-lookup"><span data-stu-id="b2de3-228">Counter</span></span>|<span data-ttu-id="b2de3-229">説明</span><span class="sxs-lookup"><span data-stu-id="b2de3-229">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b2de3-230">1</span><span class="sxs-lookup"><span data-stu-id="b2de3-230">1</span></span>|<span data-ttu-id="b2de3-231">**ブラウザーで開く**: デバイスの既定のブラウザーでアプリを開きます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-231">**Open in browser**: Opens the app in the device’s default browser.</span></span>|
|<span data-ttu-id="b2de3-232">2</span><span class="sxs-lookup"><span data-stu-id="b2de3-232">2</span></span>|<span data-ttu-id="b2de3-233">**[リンクの** コピー]: ユーザーは、タブへのリンクをコピーして共有できます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-233">**Copy link**: Users can copy and share a link to the tab.</span></span>|
|<span data-ttu-id="b2de3-234">3</span><span class="sxs-lookup"><span data-stu-id="b2de3-234">3</span></span>|<span data-ttu-id="b2de3-235">**設定**: (オプション) タブの設定を追加した後に変更します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-235">**Settings**: (Optional) Modify a tab’s settings after it's been added.</span></span>|
|<span data-ttu-id="b2de3-236">4</span><span class="sxs-lookup"><span data-stu-id="b2de3-236">4</span></span>|<span data-ttu-id="b2de3-237">**名前** の変更 : ユーザーは、タブにチャネル、チャット、または会議に意味のある名前を付けることができます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-237">**Rename**: Users can give the tab a name that's meaningful to the channel, chat, or meeting.</span></span>|
|<span data-ttu-id="b2de3-238">5</span><span class="sxs-lookup"><span data-stu-id="b2de3-238">5</span></span>|<span data-ttu-id="b2de3-239">**削除**: チャネル、チャット、または会議からタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-239">**Delete**: Removes the tab from the channel, chat, or meeting.</span></span>|

---

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="b2de3-240">タブ通知とディープ リンク</span><span class="sxs-lookup"><span data-stu-id="b2de3-240">Tab notifications and deep linking</span></span>

<span data-ttu-id="b2de3-241">タブへのディープ リンクを含むメッセージを送信できます。たとえば、カードには、ユーザーがタブ内のバグ全体を表示するために選択できるバグ データの概要が表示されます。タブ アクティビティに関するメッセージを送信すると、全員に明示的に通知することなく (つまり、ノイズのないアクティビティ) 意識が向上します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-241">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="b2de3-242">必要に応じて@mentionユーザーを追加できます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-242">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="b2de3-243">タブ アクティビティをユーザーに通知するには、次のいずれかの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-243">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="b2de3-244">**ボット**: タブ スレッドが対象の場合は特に、このメソッドが優先されます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-244">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="b2de3-245">タブのスレッドスレッドスレッドは、最近アクティブな状態で表示されます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-245">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="b2de3-246">また、このメソッドを使用すると、通知の送信方法を洗練できます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-246">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="b2de3-247">**メッセージ**: タブへの深いリンクを含むメッセージがユーザーのアクティビティ [フィードに表示されます](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="b2de3-247">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="b2de3-248">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="b2de3-248">Best practices</span></span>

<span data-ttu-id="b2de3-249">品質の高いアプリ エクスペリエンスを作成するには、次の推奨事項を使用します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-249">Use these recommendations to create a quality app experience:</span></span>

### <a name="collaboration"></a><span data-ttu-id="b2de3-250">グループ作業</span><span class="sxs-lookup"><span data-stu-id="b2de3-250">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="図は、タブ ナビゲーションデザインの操作方法を示しています。" border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="b2de3-252">Do: 会話を促進する</span><span class="sxs-lookup"><span data-stu-id="b2de3-252">Do: Facilitate conversation</span></span>

<span data-ttu-id="b2de3-253">ユーザーが話せるコンテンツとコンポーネントを含める。</span><span class="sxs-lookup"><span data-stu-id="b2de3-253">Include content and components people can talk about.</span></span> <span data-ttu-id="b2de3-254">チャット、チャネル、または会議のコンテキスト内に収まらない場合は、タブに属していない。</span><span class="sxs-lookup"><span data-stu-id="b2de3-254">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="例は、タブ ナビゲーションデザインで何をしないかを示しています。" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="b2de3-256">[しない]: タブを他の Web ページと同様に扱う</span><span class="sxs-lookup"><span data-stu-id="b2de3-256">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="b2de3-257">タブは、誰かが一度表示する可能性がある Web ページではない。</span><span class="sxs-lookup"><span data-stu-id="b2de3-257">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="b2de3-258">タブには、ユーザーが一緒に何かを達成するために必要な、最も重要で関連性の高いコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b2de3-258">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="b2de3-259">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="b2de3-259">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="タブ ナビゲーションデザインの操作方法を示す例。" border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="b2de3-261">Do: タスクとデータを制限する</span><span class="sxs-lookup"><span data-stu-id="b2de3-261">Do: Limit tasks and data</span></span>

<span data-ttu-id="b2de3-262">タブは、特定のニーズに対応する場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="b2de3-262">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="b2de3-263">チームまたはグループに関連するタスクとデータのセットを制限します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-263">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="タブ ナビゲーションデザインで何をしないかを示す図。" border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="b2de3-265">[しない]: アプリ全体を埋め込む</span><span class="sxs-lookup"><span data-stu-id="b2de3-265">Don't: Embed your entire app</span></span>

<span data-ttu-id="b2de3-266">タブを使用して、複数レベルのナビゲーションと複雑な操作でアプリ全体を表示すると、情報の過負荷が発生します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-266">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="b2de3-267">セットアップ</span><span class="sxs-lookup"><span data-stu-id="b2de3-267">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="タブ セットアップの設計を実行する方法を示す図。" border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="b2de3-269">Do: シンプルに保つ</span><span class="sxs-lookup"><span data-stu-id="b2de3-269">Do: Keep it simple</span></span>

<span data-ttu-id="b2de3-270">アプリで認証が必要な場合は、Microsoft シングル サインオン (SSO) を統合して、よりシームレスなサインイン エクスペリエンスを実現してください。</span><span class="sxs-lookup"><span data-stu-id="b2de3-270">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="b2de3-271">また、タブを追加するための重要な情報と手順のみを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2de3-271">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="タブ セットアップデザインで何をしないかを示す図。" border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="b2de3-273">[しない]: 手順が多すぎます</span><span class="sxs-lookup"><span data-stu-id="b2de3-273">Don't: Have too many steps</span></span>

<span data-ttu-id="b2de3-274">タブを追加するための不要な手順を削除します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-274">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="b2de3-275">テーマ</span><span class="sxs-lookup"><span data-stu-id="b2de3-275">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="タブの表示方法を示す図。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="b2de3-277">Do: 色トークンのTeams活用する</span><span class="sxs-lookup"><span data-stu-id="b2de3-277">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="b2de3-278">各Teamsテーマには、独自の配色があります。</span><span class="sxs-lookup"><span data-stu-id="b2de3-278">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="b2de3-279">テーマの変更を自動的に処理するには、デザインでカラー <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">トークン (Fluent UI)</a> を使用します。</span><span class="sxs-lookup"><span data-stu-id="b2de3-279">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="タブの表示方法を示す図。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="b2de3-281">[しない] : ハード コードの色の値</span><span class="sxs-lookup"><span data-stu-id="b2de3-281">Don't: Hard code color values</span></span>

<span data-ttu-id="b2de3-282">色トークンを使用しないTeamsデザインの拡張性が低く、管理に時間がかかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="b2de3-282">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::
