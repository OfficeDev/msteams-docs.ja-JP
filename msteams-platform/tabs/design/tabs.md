---
title: デスクトップと Web 用のタブの設計
description: '[デスクトップ] タブ (Teams Web) を設計し、UI キットをMicrosoft Teamsする方法について説明します。'
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: baa17cd97ff4e2cad91615dced5c4e4cf5e533c8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566881"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="166a1-103">デスクトップと Web のタブMicrosoft Teamsデザインする</span><span class="sxs-lookup"><span data-stu-id="166a1-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="166a1-104">タブは、コンテンツの大きなキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="166a1-104">A tab is a large canvas for your content.</span></span> <span data-ttu-id="166a1-105">アプリの設計をガイドするために、次の情報は、ユーザーがアプリのタブを追加、使用、および管理する方法をTeams。</span><span class="sxs-lookup"><span data-stu-id="166a1-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="166a1-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="166a1-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="166a1-107">必要に応じて取得および変更できる要素を含む、包括的なタブ設計ガイドラインについては、「UI キットMicrosoft Teams参照してください。</span><span class="sxs-lookup"><span data-stu-id="166a1-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="166a1-108">UI キットには、ここでは説明しないアクセシビリティや応答性のサイジングなどの重要なトピックも含まれています。</span><span class="sxs-lookup"><span data-stu-id="166a1-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="166a1-109">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="166a1-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="166a1-110">タブの追加</span><span class="sxs-lookup"><span data-stu-id="166a1-110">Add a tab</span></span>

<span data-ttu-id="166a1-111">タブは、ストア (AppSource) Teams、または次のいずれかのコンテキストで追加できます。</span><span class="sxs-lookup"><span data-stu-id="166a1-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="166a1-112">チャット</span><span class="sxs-lookup"><span data-stu-id="166a1-112">Chat</span></span>
* <span data-ttu-id="166a1-113">チャネル</span><span class="sxs-lookup"><span data-stu-id="166a1-113">Channel</span></span>
* <span data-ttu-id="166a1-114">会議 (会議の前、中、または後)</span><span class="sxs-lookup"><span data-stu-id="166a1-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="166a1-115">次の例は、タブがチャネルに追加される方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="166a1-115">The following example shows how a tab is added in a channel:</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="例は、チャネルに追加されるタブを示しています。" border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="166a1-117">タブを設定する</span><span class="sxs-lookup"><span data-stu-id="166a1-117">Set up a tab</span></span>

<span data-ttu-id="166a1-118">チャネル、チャット、または会議タブとしてアプリを追加する短いセットアップ プロセスがあります。エクスペリエンスは主にユーザーが行います。</span><span class="sxs-lookup"><span data-stu-id="166a1-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="166a1-119">たとえば、アプリの使い方とオプションの設定について説明できます。</span><span class="sxs-lookup"><span data-stu-id="166a1-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="166a1-120">ユーザーを認証する必要がある場合は、ここにサインイン 手順を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="166a1-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="166a1-121">タブ構成モーダル</span><span class="sxs-lookup"><span data-stu-id="166a1-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="例は、タブ構成モーダルを示しています。" border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="166a1-123">構造: タブ構成モーダル</span><span class="sxs-lookup"><span data-stu-id="166a1-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="タブ構成モーダルの UI 構造を示す図。" border="false":::

|<span data-ttu-id="166a1-125">カウンター</span><span class="sxs-lookup"><span data-stu-id="166a1-125">Counter</span></span>|<span data-ttu-id="166a1-126">説明</span><span class="sxs-lookup"><span data-stu-id="166a1-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="166a1-127">1</span><span class="sxs-lookup"><span data-stu-id="166a1-127">1</span></span>|<span data-ttu-id="166a1-128">**アプリのロゴ**: アプリのフルカラー アプリ ロゴ。</span><span class="sxs-lookup"><span data-stu-id="166a1-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="166a1-129">2</span><span class="sxs-lookup"><span data-stu-id="166a1-129">2</span></span>|<span data-ttu-id="166a1-130">**アプリ名**: アプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="166a1-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="166a1-131">3</span><span class="sxs-lookup"><span data-stu-id="166a1-131">3</span></span>|<span data-ttu-id="166a1-132">**iframe**: アプリのコンテンツの応答性の高い領域。</span><span class="sxs-lookup"><span data-stu-id="166a1-132">**iframe**: Responsive space for your app’s content.</span></span> <span data-ttu-id="166a1-133">たとえば、タブ設定や認証などです。</span><span class="sxs-lookup"><span data-stu-id="166a1-133">For example, tab settings or authentication.</span></span>|
|<span data-ttu-id="166a1-134">4</span><span class="sxs-lookup"><span data-stu-id="166a1-134">4</span></span>|<span data-ttu-id="166a1-135">**リンクについて**: アプリの詳細、アプリで必要なアクセス許可、プライバシー ポリシーと利用規約へのリンクなど、アプリに関する詳細を示すダイアログを開きます。</span><span class="sxs-lookup"><span data-stu-id="166a1-135">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="166a1-136">5</span><span class="sxs-lookup"><span data-stu-id="166a1-136">5</span></span>|<span data-ttu-id="166a1-137">**[閉じる**] ボタン: モーダルを閉じます。</span><span class="sxs-lookup"><span data-stu-id="166a1-137">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="166a1-138">6</span><span class="sxs-lookup"><span data-stu-id="166a1-138">6</span></span>|<span data-ttu-id="166a1-139">**[チーム メンバーに通知する] オプション**: モーダルは、他のユーザーがタブを追加したと知らせる投稿を作成する場合に尋ねるメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="166a1-139">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="166a1-140">7</span><span class="sxs-lookup"><span data-stu-id="166a1-140">7</span></span>|<span data-ttu-id="166a1-141">**[戻る**] ボタン: ダイアログが開いた場所に基づいて、前の手順に進みます。</span><span class="sxs-lookup"><span data-stu-id="166a1-141">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="166a1-142">8</span><span class="sxs-lookup"><span data-stu-id="166a1-142">8</span></span>|<span data-ttu-id="166a1-143">**[保存]** ボタン: タブのセットアップを完了します。</span><span class="sxs-lookup"><span data-stu-id="166a1-143">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="166a1-144">シングル サインオンを使用したタブ認証</span><span class="sxs-lookup"><span data-stu-id="166a1-144">Tab authentication with single sign-on</span></span>

<span data-ttu-id="166a1-145">ユーザーが Microsoft 資格情報を使用して最初にサインインする必要がある手順を追加できます。</span><span class="sxs-lookup"><span data-stu-id="166a1-145">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="166a1-146">この認証方法は、シングル サインオン (SSO) と呼ばれています。</span><span class="sxs-lookup"><span data-stu-id="166a1-146">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="例では、タブ認証画面を表示します。" border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="166a1-148">UI テンプレートを使用したタブセットアップの設計</span><span class="sxs-lookup"><span data-stu-id="166a1-148">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="166a1-149">次のいずれかの UI テンプレートを使用Teams、タブセットアップエクスペリエンスの設計に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="166a1-149">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="166a1-150">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="166a1-150">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="166a1-151">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。</span><span class="sxs-lookup"><span data-stu-id="166a1-151">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="166a1-152">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="166a1-152">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="166a1-153">タブを表示する</span><span class="sxs-lookup"><span data-stu-id="166a1-153">View a tab</span></span>

<span data-ttu-id="166a1-154">タブは、タスク ボードやダッシュボードTeams重要な情報など、共同作業コンテンツを表示できる画面全体の Web エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="166a1-154">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="例では、タスク ボードを含むタブを示します。" border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="166a1-156">構造: タブ</span><span class="sxs-lookup"><span data-stu-id="166a1-156">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="タブの UI 構造を示す図。" border="false":::

|<span data-ttu-id="166a1-158">カウンター</span><span class="sxs-lookup"><span data-stu-id="166a1-158">Counter</span></span>|<span data-ttu-id="166a1-159">説明</span><span class="sxs-lookup"><span data-stu-id="166a1-159">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="166a1-160">1</span><span class="sxs-lookup"><span data-stu-id="166a1-160">1</span></span>|<span data-ttu-id="166a1-161">**タブ名**: タブのナビゲーション ラベル。</span><span class="sxs-lookup"><span data-stu-id="166a1-161">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="166a1-162">2</span><span class="sxs-lookup"><span data-stu-id="166a1-162">2</span></span>|<span data-ttu-id="166a1-163">**タブ オーバーフロー**: 名前の変更や削除などのタブ アクションを開きます。</span><span class="sxs-lookup"><span data-stu-id="166a1-163">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="166a1-164">3</span><span class="sxs-lookup"><span data-stu-id="166a1-164">3</span></span>|<span data-ttu-id="166a1-165">**タブ チャット**: 右側にチャット スレッドを開き、ユーザーがコンテンツの横で会話を行えます。</span><span class="sxs-lookup"><span data-stu-id="166a1-165">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="166a1-166">4</span><span class="sxs-lookup"><span data-stu-id="166a1-166">4</span></span>|<span data-ttu-id="166a1-167">**iframe**: タブのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="166a1-167">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="166a1-168">UI テンプレートを使用したタブの設計</span><span class="sxs-lookup"><span data-stu-id="166a1-168">Designing a tab with UI templates</span></span>

<span data-ttu-id="166a1-169">次のいずれかの UI テンプレートを使用Teams、タブ エクスペリエンスの設計に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="166a1-169">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="166a1-170">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連するアイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="166a1-170">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="166a1-171">[タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): カンバン ボードやスイム レーンとも呼ばれるタスク ボードは、作業アイテムやチケットの状態を追跡するためによく使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="166a1-171">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="166a1-172">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を示す複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="166a1-172">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="166a1-173">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、送信するためのフォームです。</span><span class="sxs-lookup"><span data-stu-id="166a1-173">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="166a1-174">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="166a1-174">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="166a1-175">[左ナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左側のナビゲーション テンプレートは、タブにナビゲーションが必要な場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="166a1-175">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="166a1-176">一般に、タブ ナビゲーションは最小限に抑えます。</span><span class="sxs-lookup"><span data-stu-id="166a1-176">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="166a1-177">タブを使用して共同作業を行う</span><span class="sxs-lookup"><span data-stu-id="166a1-177">Use a tab to collaborate</span></span>

<span data-ttu-id="166a1-178">タブは、中央の場所でのコンテンツに関する会話を容易にするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="166a1-178">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="166a1-179">スレッドディスカッション</span><span class="sxs-lookup"><span data-stu-id="166a1-179">Thread discussion</span></span>

<span data-ttu-id="166a1-180">ユーザーは、新しいタブを追加すると、チャネルまたはチャットに自動的に投稿できます。これにより、チーム メンバーに新しいコンテンツが通知され、タブへのリンクが提供されるだけでなく、ユーザーはタブについて話し始めできます。</span><span class="sxs-lookup"><span data-stu-id="166a1-180">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="例は、チャネル スレッドで説明されているタブを示しています。" border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="166a1-182">サイド バイ サイドディスカッション</span><span class="sxs-lookup"><span data-stu-id="166a1-182">Side-by-side discussion</span></span>

<span data-ttu-id="166a1-183">タブのコンテンツを表示している間、ユーザーは次に会話をすることができます。</span><span class="sxs-lookup"><span data-stu-id="166a1-183">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="例では、右側にチャットが開いているタブが表示されます。" border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="166a1-185">アクセス許可と役割ベースのビュー</span><span class="sxs-lookup"><span data-stu-id="166a1-185">Permissions and role-based views</span></span>

<span data-ttu-id="166a1-186">ユーザーのアクセス許可に応じて、タブエクスペリエンスが異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="166a1-186">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="166a1-187">たとえば、1 人のユーザーがサインインせずにタブにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="166a1-187">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="166a1-188">ただし、別のユーザーは署名する必要があります。また、若干異なるコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="166a1-188">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="166a1-189">タブの管理</span><span class="sxs-lookup"><span data-stu-id="166a1-189">Manage a tab</span></span>

<span data-ttu-id="166a1-190">タブの名前の変更、削除、または変更を行うオプションを含めできます。</span><span class="sxs-lookup"><span data-stu-id="166a1-190">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="166a1-191">構造: タブ メニュー</span><span class="sxs-lookup"><span data-stu-id="166a1-191">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="タブ メニューの UI 構造を示す図。" border="false":::

|<span data-ttu-id="166a1-193">カウンター</span><span class="sxs-lookup"><span data-stu-id="166a1-193">Counter</span></span>|<span data-ttu-id="166a1-194">説明</span><span class="sxs-lookup"><span data-stu-id="166a1-194">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="166a1-195">1</span><span class="sxs-lookup"><span data-stu-id="166a1-195">1</span></span>|<span data-ttu-id="166a1-196">**設定**: (オプション) 追加後にタブの設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="166a1-196">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="166a1-197">2</span><span class="sxs-lookup"><span data-stu-id="166a1-197">2</span></span>|<span data-ttu-id="166a1-198">**名前** の変更 : ユーザーは、チームにとってより意味のある名前をタブに付けることができます。</span><span class="sxs-lookup"><span data-stu-id="166a1-198">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="166a1-199">3</span><span class="sxs-lookup"><span data-stu-id="166a1-199">3</span></span>|<span data-ttu-id="166a1-200">**[削除**] : チャネル、チャット、または会議からタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="166a1-200">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="166a1-201">タブ通知とディープ リンク</span><span class="sxs-lookup"><span data-stu-id="166a1-201">Tab notifications and deep linking</span></span>

<span data-ttu-id="166a1-202">タブへのディープ リンクを含むメッセージを送信できます。たとえば、カードには、ユーザーがタブ内のバグ全体を表示するために選択できるバグ データの概要が表示されます。タブ アクティビティに関するメッセージを送信すると、全員に明示的に通知することなく (つまり、ノイズのないアクティビティ) 意識が向上します。</span><span class="sxs-lookup"><span data-stu-id="166a1-202">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="166a1-203">必要に応じて@mentionユーザーを追加できます。</span><span class="sxs-lookup"><span data-stu-id="166a1-203">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="166a1-204">タブ アクティビティをユーザーに通知するには、次のいずれかの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="166a1-204">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="166a1-205">**ボット**: タブ スレッドが対象の場合は特に、このメソッドが優先されます。</span><span class="sxs-lookup"><span data-stu-id="166a1-205">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="166a1-206">タブのスレッドスレッドスレッドは、最近アクティブな状態で表示されます。</span><span class="sxs-lookup"><span data-stu-id="166a1-206">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="166a1-207">また、このメソッドを使用すると、通知の送信方法を洗練できます。</span><span class="sxs-lookup"><span data-stu-id="166a1-207">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="166a1-208">**メッセージ**: タブへの深いリンクを含むメッセージがユーザーのアクティビティ [フィードに表示されます](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="166a1-208">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="166a1-209">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="166a1-209">Best practices</span></span>

<span data-ttu-id="166a1-210">品質の高いアプリ エクスペリエンスを作成するには、次の推奨事項を使用します。</span><span class="sxs-lookup"><span data-stu-id="166a1-210">Use these recommendations to create a quality app experience:</span></span>

### <a name="collaboration"></a><span data-ttu-id="166a1-211">グループ作業</span><span class="sxs-lookup"><span data-stu-id="166a1-211">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="図は、タブ ナビゲーションデザインの操作方法を示しています。" border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="166a1-213">Do: 会話を促進する</span><span class="sxs-lookup"><span data-stu-id="166a1-213">Do: Facilitate conversation</span></span>

<span data-ttu-id="166a1-214">ユーザーが話せるコンテンツとコンポーネントを含める。</span><span class="sxs-lookup"><span data-stu-id="166a1-214">Include content and components people can talk about.</span></span> <span data-ttu-id="166a1-215">チャット、チャネル、または会議のコンテキスト内に収まらない場合は、タブに属していない。</span><span class="sxs-lookup"><span data-stu-id="166a1-215">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="例は、タブ ナビゲーションデザインで何をしないかを示しています。" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="166a1-217">[しない]: タブを他の Web ページと同様に扱う</span><span class="sxs-lookup"><span data-stu-id="166a1-217">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="166a1-218">タブは、誰かが一度表示する可能性がある Web ページではない。</span><span class="sxs-lookup"><span data-stu-id="166a1-218">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="166a1-219">タブには、ユーザーが一緒に何かを達成するために必要な、最も重要で関連性の高いコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="166a1-219">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="166a1-220">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="166a1-220">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="タブ ナビゲーションデザインの操作方法を示す例。" border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="166a1-222">Do: タスクとデータを制限する</span><span class="sxs-lookup"><span data-stu-id="166a1-222">Do: Limit tasks and data</span></span>

<span data-ttu-id="166a1-223">タブは、特定のニーズに対応する場合に最適です。</span><span class="sxs-lookup"><span data-stu-id="166a1-223">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="166a1-224">チームまたはグループに関連するタスクとデータのセットを制限します。</span><span class="sxs-lookup"><span data-stu-id="166a1-224">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="タブ ナビゲーションデザインで何をしないかを示す図。" border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="166a1-226">[しない]: アプリ全体を埋め込む</span><span class="sxs-lookup"><span data-stu-id="166a1-226">Don't: Embed your entire app</span></span>

<span data-ttu-id="166a1-227">タブを使用して、複数レベルのナビゲーションと複雑な操作でアプリ全体を表示すると、情報の過負荷が発生します。</span><span class="sxs-lookup"><span data-stu-id="166a1-227">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="166a1-228">セットアップ</span><span class="sxs-lookup"><span data-stu-id="166a1-228">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="タブ セットアップの設計を実行する方法を示す図。" border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="166a1-230">Do: シンプルに保つ</span><span class="sxs-lookup"><span data-stu-id="166a1-230">Do: Keep it simple</span></span>

<span data-ttu-id="166a1-231">アプリで認証が必要な場合は、Microsoft シングル サインオン (SSO) を統合して、よりシームレスなサインイン エクスペリエンスを実現してください。</span><span class="sxs-lookup"><span data-stu-id="166a1-231">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="166a1-232">また、タブを追加するための重要な情報と手順のみを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="166a1-232">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="タブ セットアップデザインで何をしないかを示す図。" border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="166a1-234">[しない]: 手順が多すぎます</span><span class="sxs-lookup"><span data-stu-id="166a1-234">Don't: Have too many steps</span></span>

<span data-ttu-id="166a1-235">タブを追加するための不要な手順を削除します。</span><span class="sxs-lookup"><span data-stu-id="166a1-235">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="166a1-236">テーマ</span><span class="sxs-lookup"><span data-stu-id="166a1-236">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="タブの表示方法を示す図。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="166a1-238">Do: 色トークンのTeams活用する</span><span class="sxs-lookup"><span data-stu-id="166a1-238">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="166a1-239">各Teamsテーマには、独自の配色があります。</span><span class="sxs-lookup"><span data-stu-id="166a1-239">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="166a1-240">テーマの変更を自動的に処理するには、デザインでカラー <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">トークン (Fluent UI)</a> を使用します。</span><span class="sxs-lookup"><span data-stu-id="166a1-240">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="タブの表示方法を示す図。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="166a1-242">[しない] : ハード コードの色の値</span><span class="sxs-lookup"><span data-stu-id="166a1-242">Don't: Hard code color values</span></span>

<span data-ttu-id="166a1-243">色トークンを使用しないTeamsデザインの拡張性が低く、管理に時間がかかる場合があります。</span><span class="sxs-lookup"><span data-stu-id="166a1-243">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::
