---
title: デスクトップと Web 用のタブの設計
description: Teamsタブ(デスクトップとウェブ)を設計し、UIキットMicrosoft Teamsを入手する方法を学びます。
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
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a><span data-ttu-id="a2a25-103">デスクトップと Web Microsoft Teams用のタブの設計</span><span class="sxs-lookup"><span data-stu-id="a2a25-103">Designing your tab for Microsoft Teams desktop and web</span></span>

<span data-ttu-id="a2a25-104">タブは、コンテンツ用の大きなキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="a2a25-104">A tab is a large canvas for your content.</span></span> <span data-ttu-id="a2a25-105">アプリのデザインをガイドするために、次の情報は、ユーザーがTeamsでタブを追加、使用、および管理する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="a2a25-105">To guide your app design, the following information describes and illustrates how people can add, use, and manage tabs in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="a2a25-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="a2a25-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="a2a25-107">必要に応じて取得および変更できる要素を含む、包括的なタブデザインガイドラインは、Microsoft Teams UI キットで確認できます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-107">You can find comprehensive tab design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="a2a25-108">UI キットには、ここでは説明されていないアクセシビリティやレスポンシブ サイジングなどの重要なトピックもあります。</span><span class="sxs-lookup"><span data-stu-id="a2a25-108">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a2a25-109">Microsoft Teams UI Kit (Figma) を入手する</span><span class="sxs-lookup"><span data-stu-id="a2a25-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a><span data-ttu-id="a2a25-110">タブの追加</span><span class="sxs-lookup"><span data-stu-id="a2a25-110">Add a tab</span></span>

<span data-ttu-id="a2a25-111">Teams ストア (AppSource) または次のいずれかのコンテキストでタブを追加できます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-111">You can add a tab from the Teams store (AppSource) or in one of the following contexts:</span></span>

* <span data-ttu-id="a2a25-112">チャット</span><span class="sxs-lookup"><span data-stu-id="a2a25-112">Chat</span></span>
* <span data-ttu-id="a2a25-113">チャネル</span><span class="sxs-lookup"><span data-stu-id="a2a25-113">Channel</span></span>
* <span data-ttu-id="a2a25-114">会議 (会議の前、中、または後)</span><span class="sxs-lookup"><span data-stu-id="a2a25-114">Meeting (before, during, or after the meeting)</span></span>

<span data-ttu-id="a2a25-115">次の例は、チャネルにタブを追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="a2a25-115">The following example shows how a tab is added in a channel:</span></span>

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="例は、チャネルに追加されるタブを示しています。" border="false":::

## <a name="set-up-a-tab"></a><span data-ttu-id="a2a25-117">タブを設定する</span><span class="sxs-lookup"><span data-stu-id="a2a25-117">Set up a tab</span></span>

<span data-ttu-id="a2a25-118">アプリをチャンネル、チャット、または会議タブとして追加する短いセットアッププロセスがあります。経験は主にあなた次第です。</span><span class="sxs-lookup"><span data-stu-id="a2a25-118">There's a short setup process to add an app as a channel, chat, or meeting tab. The experience is largely up to you.</span></span> <span data-ttu-id="a2a25-119">たとえば、アプリの使用方法といくつかのオプション設定の説明を持つことができます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-119">For example, you could have a description of how to use the app and some optional settings.</span></span> <span data-ttu-id="a2a25-120">ユーザーを認証する必要がある場合は、ここにサインイン手順を含めます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-120">Include a sign-in step here if you need to authenticate users.</span></span>

### <a name="tab-configuration-modal"></a><span data-ttu-id="a2a25-121">タブコンフィギュレーションモーダル</span><span class="sxs-lookup"><span data-stu-id="a2a25-121">Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="例は、タブ構成モーダルを示しています。" border="false":::

### <a name="anatomy-tab-configuration-modal"></a><span data-ttu-id="a2a25-123">構造: タブ構成モーダル</span><span class="sxs-lookup"><span data-stu-id="a2a25-123">Anatomy: Tab configuration modal</span></span>

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="タブ構成モーダルの UI 構造を示す図。" border="false":::

|<span data-ttu-id="a2a25-125">カウンター</span><span class="sxs-lookup"><span data-stu-id="a2a25-125">Counter</span></span>|<span data-ttu-id="a2a25-126">説明</span><span class="sxs-lookup"><span data-stu-id="a2a25-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a2a25-127">1</span><span class="sxs-lookup"><span data-stu-id="a2a25-127">1</span></span>|<span data-ttu-id="a2a25-128">**アプリロゴ**: アプリのフルカラーアプリロゴ。</span><span class="sxs-lookup"><span data-stu-id="a2a25-128">**App logo**: Full color app logo of your app.</span></span>|
|<span data-ttu-id="a2a25-129">2</span><span class="sxs-lookup"><span data-stu-id="a2a25-129">2</span></span>|<span data-ttu-id="a2a25-130">**アプリ名**: アプリのフルネーム。</span><span class="sxs-lookup"><span data-stu-id="a2a25-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="a2a25-131">3</span><span class="sxs-lookup"><span data-stu-id="a2a25-131">3</span></span>|<span data-ttu-id="a2a25-132">**iframe**: アプリのコンテンツのレスポンシブスペース。</span><span class="sxs-lookup"><span data-stu-id="a2a25-132">**iframe**: Responsive space for your app’s content.</span></span> <span data-ttu-id="a2a25-133">たとえば、タブ設定や認証などです。</span><span class="sxs-lookup"><span data-stu-id="a2a25-133">For example, tab settings or authentication.</span></span>|
|<span data-ttu-id="a2a25-134">4</span><span class="sxs-lookup"><span data-stu-id="a2a25-134">4</span></span>|<span data-ttu-id="a2a25-135">**リンクについて**: 完全な説明、アプリで必要なアクセス許可、プライバシー ポリシーや利用規約へのリンクなど、アプリに関する詳細情報を示すダイアログが開きます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-135">**About link**: Opens a dialog showing more information about the app, such as a full description, permissions required by the app, and links to your privacy policy and terms of service.</span></span>
|<span data-ttu-id="a2a25-136">5</span><span class="sxs-lookup"><span data-stu-id="a2a25-136">5</span></span>|<span data-ttu-id="a2a25-137">**閉じるボタン**: モーダルを閉じます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-137">**Close button**: Closes the modal.</span></span>|
|<span data-ttu-id="a2a25-138">6</span><span class="sxs-lookup"><span data-stu-id="a2a25-138">6</span></span>|<span data-ttu-id="a2a25-139">**チームメンバーに通知オプション**: モーダルは、タブを追加した投稿を他の人に知らせる投稿を作成するかどうかを尋ねます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-139">**Notify team members option**: The modal asks if you want to create a post letting others know you added a tab.</span></span>|
|<span data-ttu-id="a2a25-140">7</span><span class="sxs-lookup"><span data-stu-id="a2a25-140">7</span></span>|<span data-ttu-id="a2a25-141">**戻るボタン**: ダイアログが開いた場所に基づいて、前のステップに進みます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-141">**Back button**: Goes to the previous step based on where the dialog opened.</span></span>|
|<span data-ttu-id="a2a25-142">8</span><span class="sxs-lookup"><span data-stu-id="a2a25-142">8</span></span>|<span data-ttu-id="a2a25-143">**保存ボタン**: タブ設定を完了します。</span><span class="sxs-lookup"><span data-stu-id="a2a25-143">**Save button**: Completes tab setup.</span></span>|

### <a name="tab-authentication-with-single-sign-on"></a><span data-ttu-id="a2a25-144">シングル サインオンによるタブ認証</span><span class="sxs-lookup"><span data-stu-id="a2a25-144">Tab authentication with single sign-on</span></span>

<span data-ttu-id="a2a25-145">ユーザーが最初に Microsoft 資格情報でサインインする必要がある手順を追加できます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-145">You can add a step in which users must first sign in with their Microsoft credentials.</span></span> <span data-ttu-id="a2a25-146">この認証方法は、シングル サインオン (SSO) と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-146">This authentication method is called single sign-on (SSO).</span></span>

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="例はタブ認証画面を示しています。" border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a><span data-ttu-id="a2a25-148">UI テンプレートを使用したタブ設定の設計</span><span class="sxs-lookup"><span data-stu-id="a2a25-148">Designing a tab setup with UI templates</span></span>

<span data-ttu-id="a2a25-149">次の Teams UI テンプレートのいずれかを使用して、タブのセットアップ エクスペリエンスを設計します。</span><span class="sxs-lookup"><span data-stu-id="a2a25-149">Use one of the following Teams UI templates to help design your tab setup experience:</span></span>

* <span data-ttu-id="a2a25-150">[List](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連アイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々の項目に対してアクションを実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="a2a25-150">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="a2a25-151">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および送信するためのものです。</span><span class="sxs-lookup"><span data-stu-id="a2a25-151">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="a2a25-152">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、さまざまなシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-152">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="view-a-tab"></a><span data-ttu-id="a2a25-153">タブを表示する</span><span class="sxs-lookup"><span data-stu-id="a2a25-153">View a tab</span></span>

<span data-ttu-id="a2a25-154">タブは、タスクボードやダッシュボードなどのコラボレーションコンテンツや重要な情報を表示できるTeamsでの全画面表示の Web エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="a2a25-154">Tabs provide a full-screen web experience in Teams where you can display collaborative content—such task boards and dashboards—and important information.</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="例は、タスク ボードを含むタブを示しています。" border="false":::

### <a name="anatomy-tab"></a><span data-ttu-id="a2a25-156">解剖学: タブ</span><span class="sxs-lookup"><span data-stu-id="a2a25-156">Anatomy: Tab</span></span>

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="タブの UI の解剖学を示す図。" border="false":::

|<span data-ttu-id="a2a25-158">カウンター</span><span class="sxs-lookup"><span data-stu-id="a2a25-158">Counter</span></span>|<span data-ttu-id="a2a25-159">説明</span><span class="sxs-lookup"><span data-stu-id="a2a25-159">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a2a25-160">1</span><span class="sxs-lookup"><span data-stu-id="a2a25-160">1</span></span>|<span data-ttu-id="a2a25-161">**タブ名**: タブのナビゲーション ラベル。</span><span class="sxs-lookup"><span data-stu-id="a2a25-161">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="a2a25-162">2</span><span class="sxs-lookup"><span data-stu-id="a2a25-162">2</span></span>|<span data-ttu-id="a2a25-163">**タブオーバーフロー**: 名前の変更や削除などのタブアクションを開きます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-163">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="a2a25-164">3</span><span class="sxs-lookup"><span data-stu-id="a2a25-164">3</span></span>|<span data-ttu-id="a2a25-165">**タブチャット**: 右側にチャットスレッドを開き、ユーザーがコンテンツの横で会話をすることができます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-165">**Tab chat**: Opens a chat thread on the right, allowing users to have a conversation next to the content.</span></span>|
|<span data-ttu-id="a2a25-166">4</span><span class="sxs-lookup"><span data-stu-id="a2a25-166">4</span></span>|<span data-ttu-id="a2a25-167">**iframe**: タブのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="a2a25-167">**iframe**: Displays your tab’s content.</span></span>

### <a name="designing-a-tab-with-ui-templates"></a><span data-ttu-id="a2a25-168">UI テンプレートを使用したタブの設計</span><span class="sxs-lookup"><span data-stu-id="a2a25-168">Designing a tab with UI templates</span></span>

<span data-ttu-id="a2a25-169">次のTeams UI テンプレートのいずれかを使用して、タブエクスペリエンスを設計します。</span><span class="sxs-lookup"><span data-stu-id="a2a25-169">Use one of the following Teams UI templates to help design your tab experience:</span></span>

* <span data-ttu-id="a2a25-170">[List](../../concepts/design/design-teams-app-ui-templates.md#list): リストは、関連アイテムをスキャン可能な形式で表示し、ユーザーがリスト全体または個々の項目に対してアクションを実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="a2a25-170">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="a2a25-171">[タスク ボード](../../concepts/design/design-teams-app-ui-templates.md#task-board): タスク ボードは、かんばんボードまたはスイム レーンとも呼ばれ、作業項目やチケットの状態を追跡するためによく使用されるカードの集まりです。</span><span class="sxs-lookup"><span data-stu-id="a2a25-171">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="a2a25-172">[ダッシュボード](../../concepts/design/design-teams-app-ui-templates.md#dashboard): ダッシュボードは、データまたはコンテンツの概要を提供する複数のカードを含むキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="a2a25-172">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="a2a25-173">[フォーム](../../concepts/design/design-teams-app-ui-templates.md#form): フォームは、構造化された方法でユーザー入力を収集、検証、および送信するためのものです。</span><span class="sxs-lookup"><span data-stu-id="a2a25-173">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="a2a25-174">[空の状態](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空の状態テンプレートは、サインイン、初回実行エクスペリエンス、エラー メッセージなど、さまざまなシナリオで使用できます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-174">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="a2a25-175">[左ナビゲーション](../../concepts/design/design-teams-app-ui-templates.md#left-nav): 左のナビゲーション テンプレートは、タブが何らかのナビゲーションを必要とする場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-175">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="a2a25-176">通常、タブ ナビゲーションは最小限に抑える必要があります。</span><span class="sxs-lookup"><span data-stu-id="a2a25-176">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-tab-to-collaborate"></a><span data-ttu-id="a2a25-177">タブを使用して共同作業を行う</span><span class="sxs-lookup"><span data-stu-id="a2a25-177">Use a tab to collaborate</span></span>

<span data-ttu-id="a2a25-178">タブを使用すると、コンテンツに関する会話を一元的に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-178">Tabs help facilitate conversations about content in a central location.</span></span>

### <a name="thread-discussion"></a><span data-ttu-id="a2a25-179">スレッドディスカッション</span><span class="sxs-lookup"><span data-stu-id="a2a25-179">Thread discussion</span></span>

<span data-ttu-id="a2a25-180">ユーザーは、新しいタブを追加すると、チャンネルやチャットに自動的に投稿できます。これにより、チーム メンバーに新しいコンテンツが通知され、タブへのリンクが提供されるだけでなく、ユーザーがタブについて話し始めることができます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-180">Users can automatically post to a channel or chat once they’ve added a new tab. This not only notifies team members of the new content and provides a link to tab, it allows people to start talking about the tab.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="例は、チャネル スレッドで説明されているタブを示しています。" border="false":::

### <a name="side-by-side-discussion"></a><span data-ttu-id="a2a25-182">サイドバイサイドディスカッション</span><span class="sxs-lookup"><span data-stu-id="a2a25-182">Side-by-side discussion</span></span>

<span data-ttu-id="a2a25-183">ユーザーは、タブのコンテンツを表示しながら、次に会話をすることができます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-183">Users can have a conversation next while viewing the tab’s content.</span></span>

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="例は、右側にチャットを開いたタブを示しています。" border="false":::

### <a name="permissions-and-role-based-views"></a><span data-ttu-id="a2a25-185">権限とロールベースのビュー</span><span class="sxs-lookup"><span data-stu-id="a2a25-185">Permissions and role-based views</span></span>

<span data-ttu-id="a2a25-186">ユーザーのアクセス許可によって、タブの操作性が異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="a2a25-186">The tab experience may be different for users depending on their permissions.</span></span> <span data-ttu-id="a2a25-187">たとえば、1 人のユーザーがサインインしなくてもタブにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-187">For example, one user can access the tab without having to sign in.</span></span> <span data-ttu-id="a2a25-188">ただし、別のユーザーは署名する必要があり、わずかに異なるコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-188">Another user, however, must sign and will see slightly different content.</span></span>

## <a name="manage-a-tab"></a><span data-ttu-id="a2a25-189">タブの管理</span><span class="sxs-lookup"><span data-stu-id="a2a25-189">Manage a tab</span></span>

<span data-ttu-id="a2a25-190">タブの名前変更、削除、または変更を行うオプションを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-190">You can include options to rename, remove, or modify a tab.</span></span>

### <a name="anatomy-tab-menu"></a><span data-ttu-id="a2a25-191">解剖学:タブメニュー</span><span class="sxs-lookup"><span data-stu-id="a2a25-191">Anatomy: Tab menu</span></span>

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="タブ メニューの UI の概要を示す図。" border="false":::

|<span data-ttu-id="a2a25-193">カウンター</span><span class="sxs-lookup"><span data-stu-id="a2a25-193">Counter</span></span>|<span data-ttu-id="a2a25-194">説明</span><span class="sxs-lookup"><span data-stu-id="a2a25-194">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="a2a25-195">1</span><span class="sxs-lookup"><span data-stu-id="a2a25-195">1</span></span>|<span data-ttu-id="a2a25-196">**設定**: (オプション)タブを追加した後にタブの設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-196">**Settings**: (Optional) Allows users to modify a tab’s settings after it’s been added.</span></span>|
|<span data-ttu-id="a2a25-197">2</span><span class="sxs-lookup"><span data-stu-id="a2a25-197">2</span></span>|<span data-ttu-id="a2a25-198">**名前の変更**: ユーザーは、チームにとってよりわかりやすい名前をタブに付けできます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-198">**Rename**: Allows users to give the tab a name that’s more meaningful to the team.</span></span>|
|<span data-ttu-id="a2a25-199">3</span><span class="sxs-lookup"><span data-stu-id="a2a25-199">3</span></span>|<span data-ttu-id="a2a25-200">**削除**: チャンネル、チャット、または会議からタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="a2a25-200">**Remove**: Removes the tab from the channel, chat, or meeting.</span></span>|

## <a name="tab-notifications-and-deep-linking"></a><span data-ttu-id="a2a25-201">タブ通知とディープリンク</span><span class="sxs-lookup"><span data-stu-id="a2a25-201">Tab notifications and deep linking</span></span>

<span data-ttu-id="a2a25-202">あなたのタブへの深いリンクを含むメッセージを送信することができます。たとえば、カードには、ユーザーが選択できるバグ データの概要がタブに表示されます。タブアクティビティに関するメッセージを送信すると、すべてのユーザーに明示的に通知することなく、認識が高まります(ノイズのないアクティビティ)。</span><span class="sxs-lookup"><span data-stu-id="a2a25-202">You can send a message with a deep link to your tab. For example, a card shows a summary of bug data a user can select to see the entire bug in a tab. Sending messages about tab activity increases awareness without explicitly notifying everyone (i.e., activity without noise).</span></span> <span data-ttu-id="a2a25-203">必要に応じて特定のユーザーを@mentionすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-203">You also can @mention specific users if needed.</span></span>

<span data-ttu-id="a2a25-204">次のいずれかの方法でタブアクティビティをユーザーに通知します。</span><span class="sxs-lookup"><span data-stu-id="a2a25-204">Notify users of tab activity one of the following ways:</span></span>

* <span data-ttu-id="a2a25-205">**Bot**: このメソッドは、特にタブ スレッドが対象となる場合に推奨されます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-205">**Bot**: This method is preferred especially if the tab thread is targeted.</span></span> <span data-ttu-id="a2a25-206">タブのスレッド化された会話は、最近アクティブになった時点で表示されます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-206">The tab’s threaded conversation is moved into view as recently active.</span></span> <span data-ttu-id="a2a25-207">このメソッドは、通知の送信方法をいくらか高度に行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-207">This method also allows for some sophistication in how the notification is sent.</span></span>
* <span data-ttu-id="a2a25-208">**メッセージ**: ユーザーのアクティビティ フィードに、 [タブへのディープ リンク](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)を示すメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-208">**Message**: A message shows up in the user’s activity feed with a [deep link to the tab](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true).</span></span>

## <a name="best-practices"></a><span data-ttu-id="a2a25-209">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="a2a25-209">Best practices</span></span>

<span data-ttu-id="a2a25-210">次の推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="a2a25-210">Use these recommendations to create a quality app experience:</span></span>

### <a name="collaboration"></a><span data-ttu-id="a2a25-211">グループ作業</span><span class="sxs-lookup"><span data-stu-id="a2a25-211">Collaboration</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="図は、タブ ナビゲーションのデザインをどうするか示しています。" border="false":::

#### <a name="do-facilitate-conversation"></a><span data-ttu-id="a2a25-213">行う: 会話を促進する</span><span class="sxs-lookup"><span data-stu-id="a2a25-213">Do: Facilitate conversation</span></span>

<span data-ttu-id="a2a25-214">ユーザーが話すことができるコンテンツとコンポーネントを含めます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-214">Include content and components people can talk about.</span></span> <span data-ttu-id="a2a25-215">チャット、チャンネル、会議のコンテキストに合わない場合は、タブに含めることができません。</span><span class="sxs-lookup"><span data-stu-id="a2a25-215">If it doesn’t fit within the context of a chat, channel, or meeting, it doesn’t belong in your tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="例は、タブ ナビゲーションのデザインを使用しない方法を示しています。" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a><span data-ttu-id="a2a25-217">しない: タブを他のウェブページと同じように扱う</span><span class="sxs-lookup"><span data-stu-id="a2a25-217">Don't: Treat your tab like any other webpage</span></span>

<span data-ttu-id="a2a25-218">タブは、ユーザーが一度表示する Web ページではありません。</span><span class="sxs-lookup"><span data-stu-id="a2a25-218">A tab isn’t a webpage someone might view once.</span></span> <span data-ttu-id="a2a25-219">タブには、ユーザーが一緒に何かを達成するために必要な最も重要で関連性の高いコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-219">A tab should display your most important, relevant content that people need to accomplish something together.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="a2a25-220">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="a2a25-220">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="タブ ナビゲーションのデザインの操作方法を示す例。" border="false":::

#### <a name="do-limit-tasks-and-data"></a><span data-ttu-id="a2a25-222">実行: タスクとデータを制限する</span><span class="sxs-lookup"><span data-stu-id="a2a25-222">Do: Limit tasks and data</span></span>

<span data-ttu-id="a2a25-223">タブは、特定のニーズに対応する場合に最適に機能します。</span><span class="sxs-lookup"><span data-stu-id="a2a25-223">Tabs work best when they address specific needs.</span></span> <span data-ttu-id="a2a25-224">チームまたはグループに関連するタスクとデータの限定されたセットを含めます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-224">Include a limited set of tasks and data relevant to the team or group.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="タブ ナビゲーションのデザインを使用しない操作を示す図。" border="false":::

#### <a name="dont-embed-your-entire-app"></a><span data-ttu-id="a2a25-226">しない: アプリ全体を埋め込む</span><span class="sxs-lookup"><span data-stu-id="a2a25-226">Don't: Embed your entire app</span></span>

<span data-ttu-id="a2a25-227">タブを使用して、マルチレベルナビゲーションと複雑な操作を含むアプリ全体を表示すると、情報の過負荷につながります。</span><span class="sxs-lookup"><span data-stu-id="a2a25-227">Using a tab to display an entire app with multi-level navigation and complex interactions leads to information overload.</span></span>

   :::column-end:::
:::row-end:::

### <a name="setup"></a><span data-ttu-id="a2a25-228">セットアップ</span><span class="sxs-lookup"><span data-stu-id="a2a25-228">Setup</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="タブ設定デザインの処理方法を示す図。" border="false":::

#### <a name="do-keep-it-simple"></a><span data-ttu-id="a2a25-230">行う:それをシンプルに保つ</span><span class="sxs-lookup"><span data-stu-id="a2a25-230">Do: Keep it simple</span></span>

<span data-ttu-id="a2a25-231">アプリで認証が必要な場合は、Microsoft シングル サインオン (SSO) を統合して、よりシームレスなサインイン エクスペリエンスを実現してください。</span><span class="sxs-lookup"><span data-stu-id="a2a25-231">If your app requires authentication, try integrating Microsoft single sign-on (SSO) for a more seamless sign-in experience.</span></span> <span data-ttu-id="a2a25-232">また、タブを追加するための重要な情報と手順のみを含めます。</span><span class="sxs-lookup"><span data-stu-id="a2a25-232">Also, only include essential information and steps to add the tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="タブ設定デザインを使用しない操作を示す図。" border="false":::

#### <a name="dont-have-too-many-steps"></a><span data-ttu-id="a2a25-234">しない: 手順が多すぎます</span><span class="sxs-lookup"><span data-stu-id="a2a25-234">Don't: Have too many steps</span></span>

<span data-ttu-id="a2a25-235">タブを追加するための不要な手順を削除します。</span><span class="sxs-lookup"><span data-stu-id="a2a25-235">Remove any unnecessary steps for adding a tab.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="a2a25-236">テーマ</span><span class="sxs-lookup"><span data-stu-id="a2a25-236">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="タブテーマの処理方法を示す図。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="a2a25-238">行う: カラートークンTeams活用する</span><span class="sxs-lookup"><span data-stu-id="a2a25-238">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="a2a25-239">各Teamsテーマには独自の配色があります。</span><span class="sxs-lookup"><span data-stu-id="a2a25-239">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="a2a25-240">テーマの変更を自動的に処理するには、 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">デザインでカラー トークン (Fluent UI) を</a> 使用します。</span><span class="sxs-lookup"><span data-stu-id="a2a25-240">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="タブテーマを使用しない内容を示す図。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="a2a25-242">しない: ハードコードのカラー値</span><span class="sxs-lookup"><span data-stu-id="a2a25-242">Don't: Hard code color values</span></span>

<span data-ttu-id="a2a25-243">Teams色のトークンを使用しない場合、デザインの拡張性が低下し、管理に時間がかかります。</span><span class="sxs-lookup"><span data-stu-id="a2a25-243">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::
