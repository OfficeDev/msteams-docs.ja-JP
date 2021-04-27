---
title: デスクトップと Web 用のタブの設計
description: Teams タブ (デスクトップと Web) を設計し、Microsoft Teams UI キットを取得する方法について説明します。
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 840cb9f65f867358615ea006594433d8a1099111
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019686"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="bb3e7-103">Microsoft Teams デスクトップと Web 用のタブの設計</span><span class="sxs-lookup"><span data-stu-id="bb3e7-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="bb3e7-104">タブは、コンテンツの大きなキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-104">A tab is a large canvas for your content.</span></span> <span data-ttu-id="bb3e7-105">アプリの設計をガイドするために、次の情報では、Teams でタブを追加、使用、管理する方法について説明し、説明します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="bb3e7-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="bb3e7-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="bb3e7-107">必要に応じて取得および変更できる要素を含む、包括的なタブ設計ガイドラインについては、Microsoft Teams UI Kit を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="bb3e7-108">UI キットには、ここでは説明しないアクセシビリティや応答性のサイジングなどの重要なトピックも含まれています。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb3e7-109">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="bb3e7-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="bb3e7-110">タブの追加</span><span class="sxs-lookup"><span data-stu-id="bb3e7-110">Add a tab</span></span>

<span data-ttu-id="bb3e7-111">タブは、Teams ストア (AppSource) または次のいずれかのコンテキストから追加できます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="bb3e7-112">チャット</span><span class="sxs-lookup"><span data-stu-id="bb3e7-112">Chat</span></span>
* <span data-ttu-id="bb3e7-113">チャネル</span><span class="sxs-lookup"><span data-stu-id="bb3e7-113">Channel</span></span>
* <span data-ttu-id="bb3e7-114">会議 (会議の前、中、または後)</span><span class="sxs-lookup"><span data-stu-id="bb3e7-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="bb3e7-115">次の例は、チャネルにタブを追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-115">The following example shows how a tab is added in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="例は、チャネルに追加されるタブを示しています。" border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="bb3e7-117">タブを設定する</span><span class="sxs-lookup"><span data-stu-id="bb3e7-117">Set up a tab</span></span>

<span data-ttu-id="bb3e7-118">チャネル、チャット、または会議タブとしてアプリを追加する短いセットアップ プロセスがあります。エクスペリエンスは主にユーザーが行います。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="bb3e7-119">たとえば、アプリの使い方とオプションの設定について説明できます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="bb3e7-120">ユーザーを認証する必要がある場合は、ここにサインイン 手順を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="bb3e7-121">タブ構成モーダル</span><span class="sxs-lookup"><span data-stu-id="bb3e7-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="例は、タブ構成モーダルを示しています。" border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="bb3e7-123">構造: タブ構成モーダル</span><span class="sxs-lookup"><span data-stu-id="bb3e7-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="タブ構成モーダルの UI 構造を示す図。" border="false":::

|<span data-ttu-id="bb3e7-125">カウンター</span><span class="sxs-lookup"><span data-stu-id="bb3e7-125">Counter</span></span>|<span data-ttu-id="bb3e7-126">説明</span><span class="sxs-lookup"><span data-stu-id="bb3e7-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="bb3e7-127">1</span><span class="sxs-lookup"><span data-stu-id="bb3e7-127">1</span></span>|<span data-ttu-id="bb3e7-128">**アプリのロゴ**: アプリのフルカラー アプリ ロゴ。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="bb3e7-129">2</span><span class="sxs-lookup"><span data-stu-id="bb3e7-129">2</span></span>|<span data-ttu-id="bb3e7-130">**アプリ名**: アプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="bb3e7-131">3</span><span class="sxs-lookup"><span data-stu-id="bb3e7-131">3</span></span>|<span data-ttu-id="bb3e7-132">**iframe**: アプリのコンテンツのレスポンシブ スペース (タブ設定や認証など)。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-132">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="bb3e7-133">4</span><span class="sxs-lookup"><span data-stu-id="bb3e7-133">4</span></span>|<span data-ttu-id="bb3e7-134">**リンクについて**: アプリの詳細、アプリで必要なアクセス許可、プライバシー ポリシーと利用規約へのリンクなど、アプリに関する詳細を示すダイアログを開きます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-134">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="bb3e7-135">5</span><span class="sxs-lookup"><span data-stu-id="bb3e7-135">5</span></span>|<span data-ttu-id="bb3e7-136">**[閉じる**] ボタン: モーダルを閉じます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-136">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="bb3e7-137">6</span><span class="sxs-lookup"><span data-stu-id="bb3e7-137">6</span></span>|<span data-ttu-id="bb3e7-138">**[チーム メンバーに通知する] オプション**: モーダルは、他のユーザーがタブを追加したと知らせる投稿を作成する場合に尋ねるメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-138">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="bb3e7-139">7</span><span class="sxs-lookup"><span data-stu-id="bb3e7-139">7</span></span>|<span data-ttu-id="bb3e7-140">**[戻る**] ボタン: ダイアログが開いた場所に基づいて、前の手順に進みます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-140">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="bb3e7-141">8</span><span class="sxs-lookup"><span data-stu-id="bb3e7-141">8</span></span>|<span data-ttu-id="bb3e7-142">**[保存]** ボタン: タブのセットアップを完了します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-142">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="bb3e7-143">シングル サインオンを使用したタブ認証</span><span class="sxs-lookup"><span data-stu-id="bb3e7-143">Tab authentication with single sign-on</span></span>

<span data-ttu-id="bb3e7-144">ユーザーが Microsoft 資格情報を使用して最初にサインインする必要がある手順を追加できます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-144">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="bb3e7-145">この認証方法は、シングル サインオン (SSO) と呼ばれています。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-145">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="例では、タブ認証画面を表示します。" border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="bb3e7-147">UI テンプレートを使用したタブセットアップの設計</span><span class="sxs-lookup"><span data-stu-id="bb3e7-147">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="bb3e7-148">タブセットアップエクスペリエンスを設計するには、次のいずれかの Teams UI テンプレートを使用します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-148">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="bb3e7-149">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-149">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="bb3e7-150">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-150">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="bb3e7-151">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-151">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="bb3e7-152">タブを表示する</span><span class="sxs-lookup"><span data-stu-id="bb3e7-152">View a tab</span></span>

<span data-ttu-id="bb3e7-153">タブは Teams のフルスクリーン Web エクスペリエンスを提供し、共同作業用のコンテンツ (タスク ボードやダッシュボードなど) と重要な情報を表示できます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-153">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="例では、タスク ボードを含むタブを示します。" border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="bb3e7-155">構造: タブ</span><span class="sxs-lookup"><span data-stu-id="bb3e7-155">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="タブの UI 構造を示す図。" border="false":::

|<span data-ttu-id="bb3e7-157">カウンター</span><span class="sxs-lookup"><span data-stu-id="bb3e7-157">Counter</span></span>|<span data-ttu-id="bb3e7-158">説明</span><span class="sxs-lookup"><span data-stu-id="bb3e7-158">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="bb3e7-159">1</span><span class="sxs-lookup"><span data-stu-id="bb3e7-159">1</span></span>|<span data-ttu-id="bb3e7-160">**タブ名**: タブのナビゲーション ラベル。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-160">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="bb3e7-161">2</span><span class="sxs-lookup"><span data-stu-id="bb3e7-161">2</span></span>|<span data-ttu-id="bb3e7-162">**タブ オーバーフロー**: 名前の変更や削除などのタブ アクションを開きます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-162">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="bb3e7-163">3</span><span class="sxs-lookup"><span data-stu-id="bb3e7-163">3</span></span>|<span data-ttu-id="bb3e7-164">**タブ チャット**: 右側にチャット スレッドを開き、ユーザーがコンテンツの横で会話を行えます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-164">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="bb3e7-165">4</span><span class="sxs-lookup"><span data-stu-id="bb3e7-165">4</span></span>|<span data-ttu-id="bb3e7-166">**iframe**: タブのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-166">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="bb3e7-167">UI テンプレートを使用したタブの設計</span><span class="sxs-lookup"><span data-stu-id="bb3e7-167">Designing a tab with UI templates</span></span>

<span data-ttu-id="bb3e7-168">タブ エクスペリエンスを設計するには、次のいずれかの Teams UI テンプレートを使用します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-168">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="bb3e7-169">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-169">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="bb3e7-170">[タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): カンバン ボードやスイム レーンとも呼ばれるタスク ボードは、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-170">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="bb3e7-171">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を示す複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-171">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="bb3e7-172">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-172">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="bb3e7-173">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-173">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="bb3e7-174">[左ナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左側のナビゲーション テンプレートは、タブにナビゲーションが必要な場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-174">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="bb3e7-175">一般に、タブ ナビゲーションは最小限に抑えます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-175">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="bb3e7-176">タブを使用して共同作業を行う</span><span class="sxs-lookup"><span data-stu-id="bb3e7-176">Use a tab to collaborate</span></span>

<span data-ttu-id="bb3e7-177">タブは、中央の場所でのコンテンツに関する会話を容易にするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-177">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="bb3e7-178">スレッドディスカッション</span><span class="sxs-lookup"><span data-stu-id="bb3e7-178">Thread discussion</span></span>

<span data-ttu-id="bb3e7-179">ユーザーは、新しいタブを追加すると、チャネルまたはチャットに自動的に投稿できます。これにより、チーム メンバーに新しいコンテンツが通知され、タブへのリンクが提供されるだけでなく、ユーザーはタブについて話し始めできます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-179">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="例は、チャネル スレッドで説明されているタブを示しています。" border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="bb3e7-181">サイド バイ サイドディスカッション</span><span class="sxs-lookup"><span data-stu-id="bb3e7-181">Side-by-side discussion</span></span>

<span data-ttu-id="bb3e7-182">タブのコンテンツを表示している間、ユーザーは次に会話をすることができます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-182">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="例では、右側にチャットが開いているタブが表示されます。" border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="bb3e7-184">アクセス許可と役割ベースのビュー</span><span class="sxs-lookup"><span data-stu-id="bb3e7-184">Permissions and role-based views</span></span>

<span data-ttu-id="bb3e7-185">ユーザーのアクセス許可に応じて、タブエクスペリエンスが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-185">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="bb3e7-186">たとえば、1 人のユーザーがサインインせずにタブにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-186">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="bb3e7-187">ただし、別のユーザーは署名する必要があります。また、若干異なるコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-187">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="bb3e7-188">タブの管理</span><span class="sxs-lookup"><span data-stu-id="bb3e7-188">Manage a tab</span></span>

<span data-ttu-id="bb3e7-189">タブの名前の変更、削除、または変更を行うオプションを含めできます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-189">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="bb3e7-190">構造: タブ メニュー</span><span class="sxs-lookup"><span data-stu-id="bb3e7-190">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="タブ メニューの UI 構造を示す図。" border="false":::

|<span data-ttu-id="bb3e7-192">カウンター</span><span class="sxs-lookup"><span data-stu-id="bb3e7-192">Counter</span></span>|<span data-ttu-id="bb3e7-193">説明</span><span class="sxs-lookup"><span data-stu-id="bb3e7-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="bb3e7-194">1</span><span class="sxs-lookup"><span data-stu-id="bb3e7-194">1</span></span>|<span data-ttu-id="bb3e7-195">**設定**: (オプション) タブの追加後にタブの設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-195">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="bb3e7-196">2</span><span class="sxs-lookup"><span data-stu-id="bb3e7-196">2</span></span>|<span data-ttu-id="bb3e7-197">**名前** の変更 : ユーザーは、チームにとってより意味のある名前をタブに付けることができます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-197">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="bb3e7-198">3</span><span class="sxs-lookup"><span data-stu-id="bb3e7-198">3</span></span>|<span data-ttu-id="bb3e7-199">**[削除**] : チャネル、チャット、または会議からタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-199">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="bb3e7-200">タブ通知とディープ リンク</span><span class="sxs-lookup"><span data-stu-id="bb3e7-200">Tab notifications and deep linking</span></span>

<span data-ttu-id="bb3e7-201">タブへのディープ リンクを含むメッセージを送信できます。たとえば、カードには、ユーザーがタブ内のバグ全体を表示するために選択できるバグ データの概要が表示されます。タブ アクティビティに関するメッセージを送信すると、全員に明示的に通知することなく (つまり、ノイズのないアクティビティ) 意識が向上します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-201">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="bb3e7-202">必要に応じて@mentionユーザーを追加できます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-202">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="bb3e7-203">タブ アクティビティをユーザーに通知するには、次のいずれかの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-203">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="bb3e7-204">**ボット**: タブ スレッドが対象の場合は特に、このメソッドが優先されます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-204">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="bb3e7-205">タブのスレッドスレッドスレッドは、最近アクティブな状態で表示されます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-205">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="bb3e7-206">また、このメソッドを使用すると、通知の送信方法を洗練できます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-206">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="bb3e7-207">**メッセージ**: タブへの深いリンクを含むメッセージがユーザーのアクティビティ [フィードに表示されます](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-207">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="bb3e7-208">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="bb3e7-208">Best practices</span></span>

### <a name="collaboration"></a><span data-ttu-id="bb3e7-209">グループ作業</span><span class="sxs-lookup"><span data-stu-id="bb3e7-209">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="図は、タブ ナビゲーションデザインの操作方法を示しています。" border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="bb3e7-211">Do: 会話を促進する</span><span class="sxs-lookup"><span data-stu-id="bb3e7-211">Do: Facilitate conversation</span></span>

<span data-ttu-id="bb3e7-212">ユーザーが話せるコンテンツとコンポーネントを含める。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-212">Include content and components people can talk about.</span></span> <span data-ttu-id="bb3e7-213">チャット、チャネル、または会議のコンテキスト内に収まらない場合は、タブに属していない。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-213">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="例は、タブ ナビゲーションデザインで何をしないかを示しています。" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="bb3e7-215">[しない]: タブを他の Web ページと同様に扱う</span><span class="sxs-lookup"><span data-stu-id="bb3e7-215">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="bb3e7-216">タブは、誰かが一度表示する可能性がある Web ページではない。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-216">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="bb3e7-217">タブには、ユーザーが一緒に何かを達成するために必要な、最も重要で関連性の高いコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-217">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="bb3e7-218">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="bb3e7-218">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="タブ ナビゲーションデザインの操作方法を示す例。" border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="bb3e7-220">Do: タスクとデータを制限する</span><span class="sxs-lookup"><span data-stu-id="bb3e7-220">Do: Limit tasks and data</span></span>

<span data-ttu-id="bb3e7-221">タブは、特定のニーズに対応する場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-221">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="bb3e7-222">チームまたはグループに関連するタスクとデータのセットを制限します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-222">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="タブ ナビゲーションデザインで何をしないかを示す図。" border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="bb3e7-224">[しない]: アプリ全体を埋め込む</span><span class="sxs-lookup"><span data-stu-id="bb3e7-224">Don't: Embed your entire app</span></span>

<span data-ttu-id="bb3e7-225">タブを使用して、複数レベルのナビゲーションと複雑な操作でアプリ全体を表示すると、情報の過負荷が発生します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-225">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="bb3e7-226">セットアップ</span><span class="sxs-lookup"><span data-stu-id="bb3e7-226">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="タブ セットアップの設計を実行する方法を示す図。" border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="bb3e7-228">Do: シンプルに保つ</span><span class="sxs-lookup"><span data-stu-id="bb3e7-228">Do: Keep it simple</span></span>

<span data-ttu-id="bb3e7-229">アプリで認証が必要な場合は、Microsoft シングル サインオン (SSO) を統合して、よりシームレスなサインイン エクスペリエンスを実現してください。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-229">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="bb3e7-230">また、タブを追加するための重要な情報と手順のみを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-230">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="タブ セットアップデザインで何をしないかを示す図。" border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="bb3e7-232">[しない]: 手順が多すぎます</span><span class="sxs-lookup"><span data-stu-id="bb3e7-232">Don't: Have too many steps</span></span>

<span data-ttu-id="bb3e7-233">タブを追加するための不要な手順を削除します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-233">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="bb3e7-234">テーマ</span><span class="sxs-lookup"><span data-stu-id="bb3e7-234">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="タブの表示方法を示す図。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="bb3e7-236">Do: Teams カラー トークンを活用する</span><span class="sxs-lookup"><span data-stu-id="bb3e7-236">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="bb3e7-237">各 Teams テーマには、独自の配色があります。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-237">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="bb3e7-238">テーマの変更を自動的に処理するには、デザインでカラー <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">トークン (Fluent UI)</a> を使用します。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-238">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="タブの表示方法を示す図。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="bb3e7-240">[しない] : ハード コードの色の値</span><span class="sxs-lookup"><span data-stu-id="bb3e7-240">Don't: Hard code color values</span></span>

<span data-ttu-id="bb3e7-241">Teams カラー トークンを使用しない場合、デザインの拡張性が低く、管理に時間がかかっています。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-241">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="bb3e7-242">デザインを検証する</span><span class="sxs-lookup"><span data-stu-id="bb3e7-242">Validate your design</span></span>

<span data-ttu-id="bb3e7-243">AppSource にアプリを公開する予定がある場合、アプリの提出時に失敗する原因となるデザイン上の問題を理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb3e7-243">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb3e7-244">デザイン検証ガイドラインをチェックする</span><span class="sxs-lookup"><span data-stu-id="bb3e7-244">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
