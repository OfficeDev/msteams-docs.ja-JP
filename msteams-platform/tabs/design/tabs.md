---
title: デスクトップと web 用のタブの設計
description: Teams タブ (デスクトップと web) を設計し、Microsoft Teams UI キットを取得する方法について説明します。
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 692a21c78dc86cbca5bf248e55d0332bd71c6b92
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604702"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="9060d-103">Microsoft Teams デスクトップおよび web 用のタブの設計</span><span class="sxs-lookup"><span data-stu-id="9060d-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="9060d-104">タブは、コラボレーションを促進するコンテンツの大きなキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="9060d-104">A tab is a large canvas for content that facilitates collaboration.</span></span> <span data-ttu-id="9060d-105">アプリの設計をガイドするには、次の情報を参照して、Teams でのタブの追加、使用、管理を行う方法を示します。</span><span class="sxs-lookup"><span data-stu-id="9060d-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="9060d-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="9060d-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="9060d-107">Microsoft Teams UI キットでは、必要に応じて取得および変更できる要素を含む、包括的なタブデザインガイドラインを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="9060d-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="9060d-108">UI キットには、ここでは説明していないアクセシビリティや応答性の高いサイズ変更などの重要なトピックもあります。</span><span class="sxs-lookup"><span data-stu-id="9060d-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9060d-109">Microsoft Teams UI Kit (Figma) を取得する</span><span class="sxs-lookup"><span data-stu-id="9060d-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="9060d-110">タブの追加</span><span class="sxs-lookup"><span data-stu-id="9060d-110">Add a tab</span></span>

<span data-ttu-id="9060d-111">Teams ストア (AppSource) または次のいずれかのコンテキストからタブを追加できます。</span><span class="sxs-lookup"><span data-stu-id="9060d-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="9060d-112">チャット</span><span class="sxs-lookup"><span data-stu-id="9060d-112">Chat</span></span>
* <span data-ttu-id="9060d-113">チャネル</span><span class="sxs-lookup"><span data-stu-id="9060d-113">Channel</span></span>
* <span data-ttu-id="9060d-114">会議 (会議の前、中、または後)</span><span class="sxs-lookup"><span data-stu-id="9060d-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="9060d-115">次の例は、チャネルにタブを追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="9060d-115">The following example shows how a tab is added in a channel.</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="例は、チャネルで追加されているタブを示しています。" border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="9060d-117">タブを設定する</span><span class="sxs-lookup"><span data-stu-id="9060d-117">Set up a tab</span></span>

<span data-ttu-id="9060d-118">アプリをチャネル、チャット、または会議のタブとして追加するための短いセットアッププロセスがあります。これらの機能は、ユーザーにとって非常に大きくなります。</span><span class="sxs-lookup"><span data-stu-id="9060d-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="9060d-119">たとえば、アプリの使用方法とオプションの設定を行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="9060d-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="9060d-120">ユーザーを認証する必要がある場合は、ここにサインイン手順を含めます。</span><span class="sxs-lookup"><span data-stu-id="9060d-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="9060d-121">タブの構成のモーダル</span><span class="sxs-lookup"><span data-stu-id="9060d-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="例は、タブの構成のモーダルを示しています。" border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="9060d-123">構造: タブの構成のモーダル</span><span class="sxs-lookup"><span data-stu-id="9060d-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="タブ構成モーダルの UI 構造を示す図" border="false":::

|<span data-ttu-id="9060d-125">カウンター</span><span class="sxs-lookup"><span data-stu-id="9060d-125">Counter</span></span>|<span data-ttu-id="9060d-126">説明</span><span class="sxs-lookup"><span data-stu-id="9060d-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9060d-127">1</span><span class="sxs-lookup"><span data-stu-id="9060d-127">1</span></span>|<span data-ttu-id="9060d-128">**アプリロゴ**: アプリのフルカラーアプリのロゴ。</span><span class="sxs-lookup"><span data-stu-id="9060d-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="9060d-129">2 </span><span class="sxs-lookup"><span data-stu-id="9060d-129">2</span></span>|<span data-ttu-id="9060d-130">**アプリ名**: アプリの完全な名前。</span><span class="sxs-lookup"><span data-stu-id="9060d-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="9060d-131">3 </span><span class="sxs-lookup"><span data-stu-id="9060d-131">3</span></span>|<span data-ttu-id="9060d-132">**iframe**: アプリのコンテンツ (タブ設定または認証など) に対する応答性の高いスペース。</span><span class="sxs-lookup"><span data-stu-id="9060d-132">**iframe**: Responsive space for your app’s content (for example, tab settings or authentication).</span></span>|
|<span data-ttu-id="9060d-133">4 </span><span class="sxs-lookup"><span data-stu-id="9060d-133">4</span></span>|<span data-ttu-id="9060d-134">**リンクについて**: 詳細な説明、アプリに必要なアクセス許可など、アプリに関する詳細情報を示すダイアログボックスを開き、プライバシーポリシーおよびサービス条件へのリンクを表示します。</span><span class="sxs-lookup"><span data-stu-id="9060d-134">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="9060d-135">5 </span><span class="sxs-lookup"><span data-stu-id="9060d-135">5</span></span>|<span data-ttu-id="9060d-136">**[閉じる] ボタン**: モーダルを閉じます。</span><span class="sxs-lookup"><span data-stu-id="9060d-136">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="9060d-137">6 </span><span class="sxs-lookup"><span data-stu-id="9060d-137">6</span></span>|<span data-ttu-id="9060d-138">[**チームメンバーに通知する] オプション**: 他のユーザーにタブを追加することを知らせる投稿を作成するかどうかを確認するには、[モーダル] を選択します。</span><span class="sxs-lookup"><span data-stu-id="9060d-138">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="9060d-139">7 </span><span class="sxs-lookup"><span data-stu-id="9060d-139">7</span></span>|<span data-ttu-id="9060d-140">[**戻る] ボタン**: ダイアログが開いている場所に基づいて、前の手順に進みます。</span><span class="sxs-lookup"><span data-stu-id="9060d-140">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="9060d-141">8 </span><span class="sxs-lookup"><span data-stu-id="9060d-141">8</span></span>|<span data-ttu-id="9060d-142">[**保存] ボタン**: タブの設定を完了します。</span><span class="sxs-lookup"><span data-stu-id="9060d-142">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="9060d-143">シングルサインオンを使用したタブ認証</span><span class="sxs-lookup"><span data-stu-id="9060d-143">Tab authentication with single sign-on</span></span>

<span data-ttu-id="9060d-144">ユーザーが Microsoft 資格情報を使用して最初にサインインする必要がある手順を追加できます。</span><span class="sxs-lookup"><span data-stu-id="9060d-144">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="9060d-145">この認証方法は、シングルサインオン (SSO) と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="9060d-145">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="例は、タブ認証画面を示しています。" border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="9060d-147">UI テンプレートを使用してタブ設定を設計する</span><span class="sxs-lookup"><span data-stu-id="9060d-147">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="9060d-148">次の Teams UI テンプレートのいずれかを使用して、タブのセットアップ環境を設計します。</span><span class="sxs-lookup"><span data-stu-id="9060d-148">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="9060d-149">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストでは、関連するアイテムを scannable 形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="9060d-149">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="9060d-150">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および提出するためのものです。</span><span class="sxs-lookup"><span data-stu-id="9060d-150">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="9060d-151">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行時のエクスペリエンス、エラーメッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="9060d-151">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="9060d-152">タブを表示する</span><span class="sxs-lookup"><span data-stu-id="9060d-152">View a tab</span></span>

<span data-ttu-id="9060d-153">タブは、チームで全画面表示の web 環境を提供します。これにより、コラボレーションコンテンツ (タスクボードやダッシュボードなど) や重要な情報を表示できます。</span><span class="sxs-lookup"><span data-stu-id="9060d-153">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="例は、タスクボードを含むタブを示しています。" border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="9060d-155">[構造]: タブ</span><span class="sxs-lookup"><span data-stu-id="9060d-155">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="タブの UI の構造を示す図。" border="false":::

|<span data-ttu-id="9060d-157">カウンター</span><span class="sxs-lookup"><span data-stu-id="9060d-157">Counter</span></span>|<span data-ttu-id="9060d-158">説明</span><span class="sxs-lookup"><span data-stu-id="9060d-158">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9060d-159">1</span><span class="sxs-lookup"><span data-stu-id="9060d-159">1</span></span>|<span data-ttu-id="9060d-160">**[タブ名**]: タブのナビゲーションラベル。</span><span class="sxs-lookup"><span data-stu-id="9060d-160">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="9060d-161">2 </span><span class="sxs-lookup"><span data-stu-id="9060d-161">2</span></span>|<span data-ttu-id="9060d-162">**Tab overflow**: 名前の変更や削除などのタブアクションを開きます。</span><span class="sxs-lookup"><span data-stu-id="9060d-162">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="9060d-163">3 </span><span class="sxs-lookup"><span data-stu-id="9060d-163">3</span></span>|<span data-ttu-id="9060d-164">**タブチャット**: チャットスレッドを右側に開き、ユーザーがコンテンツの横に会話できるようにします。</span><span class="sxs-lookup"><span data-stu-id="9060d-164">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="9060d-165">4 </span><span class="sxs-lookup"><span data-stu-id="9060d-165">4</span></span>|<span data-ttu-id="9060d-166">**iframe**: タブのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="9060d-166">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="9060d-167">UI テンプレートを使用してタブを設計する</span><span class="sxs-lookup"><span data-stu-id="9060d-167">Designing a tab with UI templates</span></span>

<span data-ttu-id="9060d-168">次の Teams UI テンプレートのいずれかを使用して、タブの動作を設計します。</span><span class="sxs-lookup"><span data-stu-id="9060d-168">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="9060d-169">[リスト](../../concepts/design/design-teams-app-ui-templates.md#list): リストでは、関連するアイテムを scannable 形式で表示し、ユーザーがリスト全体または個々のアイテムに対してアクションを実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="9060d-169">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="9060d-170">[タスクボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): タスクボード (かんばんボードまたはスイムレーンと呼ばれることもあります) は、多くの場合、作業項目またはチケットの状態を追跡するために使用されるカードのコレクションです。</span><span class="sxs-lookup"><span data-stu-id="9060d-170">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="9060d-171">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="9060d-171">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="9060d-172">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および提出するためのものです。</span><span class="sxs-lookup"><span data-stu-id="9060d-172">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="9060d-173">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行時のエクスペリエンス、エラーメッセージなど、多くのシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="9060d-173">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="9060d-174">[左](../../concepts/design/design-teams-app-ui-templates.md#left-nav)ナビゲーション: タブにいくつかのナビゲーションが必要な場合は、左側のナビゲーションテンプレートが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="9060d-174">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="9060d-175">一般的に、タブナビゲーションは最小限にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9060d-175">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="9060d-176">タブを使用して共同作業する</span><span class="sxs-lookup"><span data-stu-id="9060d-176">Use a tab to collaborate</span></span>

<span data-ttu-id="9060d-177">タブを使用すると、コンテンツに関する会話を一元的に容易に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="9060d-177">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="9060d-178">スレッドディスカッション</span><span class="sxs-lookup"><span data-stu-id="9060d-178">Thread discussion</span></span>

<span data-ttu-id="9060d-179">新しいタブを追加すると、ユーザーはチャネルまたはチャットに自動的に投稿できるようになります。これにより、新しいコンテンツのチームメンバーに通知されるだけでなく、tab へのリンクも表示されるので、ユーザーはタブについての会話を開始できます。</span><span class="sxs-lookup"><span data-stu-id="9060d-179">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="例は、チャネルスレッドで説明されているタブを示しています。" border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="9060d-181">Side-by-side ディスカッション</span><span class="sxs-lookup"><span data-stu-id="9060d-181">Side-by-side discussion</span></span>

<span data-ttu-id="9060d-182">タブのコンテンツを表示しているときに、ユーザーは次の会話を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="9060d-182">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="例は、右側にチャットが開いているタブを示しています。" border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="9060d-184">アクセス許可と役割ベースのビュー</span><span class="sxs-lookup"><span data-stu-id="9060d-184">Permissions and role-based views</span></span>

<span data-ttu-id="9060d-185">ユーザーのアクセス許可によっては、タブの動作が異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="9060d-185">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="9060d-186">たとえば、1人のユーザーがサインインせずにタブにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="9060d-186">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="9060d-187">ただし、別のユーザーが署名する必要があり、多少異なる内容が表示されます。</span><span class="sxs-lookup"><span data-stu-id="9060d-187">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="9060d-188">タブを管理する</span><span class="sxs-lookup"><span data-stu-id="9060d-188">Manage a tab</span></span>

<span data-ttu-id="9060d-189">タブの名前変更、削除、または変更を行うオプションを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="9060d-189">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="9060d-190">分析: タブメニュー</span><span class="sxs-lookup"><span data-stu-id="9060d-190">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="タブメニューの UI の構造を示す図。" border="false":::

|<span data-ttu-id="9060d-192">カウンター</span><span class="sxs-lookup"><span data-stu-id="9060d-192">Counter</span></span>|<span data-ttu-id="9060d-193">説明</span><span class="sxs-lookup"><span data-stu-id="9060d-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="9060d-194">1</span><span class="sxs-lookup"><span data-stu-id="9060d-194">1</span></span>|<span data-ttu-id="9060d-195">**設定**: (オプション) ユーザーが追加されたタブの設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="9060d-195">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="9060d-196">2 </span><span class="sxs-lookup"><span data-stu-id="9060d-196">2</span></span>|<span data-ttu-id="9060d-197">[**名前の変更**]: ユーザーは、チームにとってわかりやすい名前をタブに付けることができます。</span><span class="sxs-lookup"><span data-stu-id="9060d-197">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="9060d-198">3 </span><span class="sxs-lookup"><span data-stu-id="9060d-198">3</span></span>|<span data-ttu-id="9060d-199">**削除**: チャネル、チャット、または会議からタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="9060d-199">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="9060d-200">タブ通知とディープリンク</span><span class="sxs-lookup"><span data-stu-id="9060d-200">Tab notifications and deep linking</span></span>

<span data-ttu-id="9060d-201">詳細なリンクを持つメッセージをタブに送信できます。たとえば、カードはバグデータの概要を示しています。これは、ユーザーが選択してバグ全体をタブに表示することができます。Tab アクティビティに関するメッセージを送信すると、ユーザーに明示的に通知することなく (つまり、ノイズのないアクティビティ)、認識が向上します。</span><span class="sxs-lookup"><span data-stu-id="9060d-201">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="9060d-202">必要に応じて特定のユーザーを @mention することもできます。</span><span class="sxs-lookup"><span data-stu-id="9060d-202">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="9060d-203">Tab アクティビティをユーザーに通知するには、次のいずれかの方法を実行します。</span><span class="sxs-lookup"><span data-stu-id="9060d-203">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="9060d-204">**Bot**: このメソッドは、特に tab スレッドが対象の場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="9060d-204">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="9060d-205">タブのスレッドスレッドは、最近アクティブになったときと同じように表示に移動します。</span><span class="sxs-lookup"><span data-stu-id="9060d-205">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="9060d-206">また、このメソッドを使用すると、通知の送信方法をいくらか洗練することができます。</span><span class="sxs-lookup"><span data-stu-id="9060d-206">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="9060d-207">**メッセージ**: ユーザーのアクティビティフィードにメッセージが表示され、 [タブへの詳細なリンク](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)が表示されます。</span><span class="sxs-lookup"><span data-stu-id="9060d-207">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="9060d-208">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="9060d-208">Best practices</span></span>

### <a name="collaboration"></a><span data-ttu-id="9060d-209">グループ作業</span><span class="sxs-lookup"><span data-stu-id="9060d-209">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="タブナビゲーションデザインの操作を示す図" border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="9060d-211">Do: 会話を促進する</span><span class="sxs-lookup"><span data-stu-id="9060d-211">Do: Facilitate conversation</span></span>

<span data-ttu-id="9060d-212">ユーザーが説明できるコンテンツとコンポーネントを含めます。</span><span class="sxs-lookup"><span data-stu-id="9060d-212">Include content and components people can talk about.</span></span> <span data-ttu-id="9060d-213">チャット、チャネル、または会議のコンテキスト内に収まらない場合は、タブに含まれません。</span><span class="sxs-lookup"><span data-stu-id="9060d-213">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="タブナビゲーションデザインではできないことを示す図" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="9060d-215">いいえ: 他の web ページと同じようにタブを扱います</span><span class="sxs-lookup"><span data-stu-id="9060d-215">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="9060d-216">タブは、誰かが一度に表示する可能性がある web ページではありません。</span><span class="sxs-lookup"><span data-stu-id="9060d-216">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="9060d-217">タブには、ユーザーが共同作業を行うために必要とする、最も重要な関連コンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="9060d-217">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="9060d-218">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="9060d-218">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="タブナビゲーションデザインの操作を示す図" border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="9060d-220">Do: タスクとデータを制限する</span><span class="sxs-lookup"><span data-stu-id="9060d-220">Do: Limit tasks and data</span></span>

<span data-ttu-id="9060d-221">タブは特定のニーズに対応するために最適に機能します。</span><span class="sxs-lookup"><span data-stu-id="9060d-221">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="9060d-222">チームまたはグループに関連するタスクとデータの限定されたセットを含めます。</span><span class="sxs-lookup"><span data-stu-id="9060d-222">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="タブナビゲーションデザインではできないことを示す図" border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="9060d-224">いいえ: アプリ全体を埋め込む</span><span class="sxs-lookup"><span data-stu-id="9060d-224">Don't: Embed your entire app</span></span>

<span data-ttu-id="9060d-225">タブを使用して、複数レベルのナビゲーションを備えたアプリ全体を表示し、複雑な対話によって情報の過負荷につながります。</span><span class="sxs-lookup"><span data-stu-id="9060d-225">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="9060d-226">セットアップ</span><span class="sxs-lookup"><span data-stu-id="9060d-226">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="タブセットアップデザインの操作を示す図" border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="9060d-228">Do: シンプルを維持する</span><span class="sxs-lookup"><span data-stu-id="9060d-228">Do: Keep it simple</span></span>

<span data-ttu-id="9060d-229">アプリで認証が必要な場合は、Microsoft シングルサインオン (SSO) を統合して、よりシームレスなサインイン操作を実行してみてください。</span><span class="sxs-lookup"><span data-stu-id="9060d-229">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="9060d-230">また、基本的な情報と、タブを追加する手順についても記載します。</span><span class="sxs-lookup"><span data-stu-id="9060d-230">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="タブセットアップデザインでは実行しないことを示す図" border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="9060d-232">いいえ: 手順が多すぎます</span><span class="sxs-lookup"><span data-stu-id="9060d-232">Don't: Have too many steps</span></span>

<span data-ttu-id="9060d-233">タブを追加するための不要な手順を削除します。</span><span class="sxs-lookup"><span data-stu-id="9060d-233">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="9060d-234">テーマ</span><span class="sxs-lookup"><span data-stu-id="9060d-234">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="タブのテーマの操作を示す図" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="9060d-236">Do: Teams のカラートークンを活用する</span><span class="sxs-lookup"><span data-stu-id="9060d-236">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="9060d-237">各 Teams テーマには独自の配色があります。</span><span class="sxs-lookup"><span data-stu-id="9060d-237">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="9060d-238">テーマの変更を自動的に処理するには、設計で <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color token (FLUENT UI)</a> を使用します。</span><span class="sxs-lookup"><span data-stu-id="9060d-238">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="タブのテーマを使用していないことを示す図" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="9060d-240">いいえ: ハードコードの色の値</span><span class="sxs-lookup"><span data-stu-id="9060d-240">Don't: Hard code color values</span></span>

<span data-ttu-id="9060d-241">Teams のカラートークンを使用しない場合、設計のスケーラビリティが低下し、管理にかかる時間が長くなります。</span><span class="sxs-lookup"><span data-stu-id="9060d-241">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="9060d-242">設計を検証する</span><span class="sxs-lookup"><span data-stu-id="9060d-242">Validate your design</span></span>

<span data-ttu-id="9060d-243">アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="9060d-243">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9060d-244">設計検証ガイドラインの確認</span><span class="sxs-lookup"><span data-stu-id="9060d-244">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
