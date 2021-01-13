---
title: 開始する - チャネルとグループ タブを作成する
author: heath-hamilton
description: Microsoft Teams を使用して、Microsoft Teams チャネルとグループ タブをすばやく作成Toolkit。
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: ae06217cf9ffd99ce94aff981fbbec19136d4aeb
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797877"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="b5ea7-103">Microsoft Teams のチャネルとグループ タブを作成する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="b5ea7-104">このチュートリアルでは、基本的なチャネル タブ *(グループ* タブとも呼ばれる) を作成します。これは、チーム チャネルまたはチャットの全画面ページです。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="b5ea7-105">個人用タブとは異なり、ユーザーは、この種のタブのいくつかの側面を構成できます (たとえば、チャネルにとって意味のある名前にタブの名前を変更します)。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="b5ea7-106">割り当て</span><span class="sxs-lookup"><span data-stu-id="b5ea7-106">Your assignment</span></span>

<span data-ttu-id="b5ea7-107">少し前に、組織はタブを使用して重要な連絡先情報 (ヘルプ デスク、人事など) を表示する Teams アプリを作成しました。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-107">Not long ago, your organization created a Teams app that uses a tab to display important contact information (help desk, HR, etc.).</span></span> <span data-ttu-id="b5ea7-108">ただし、個人用タブの場合は、各ユーザーがタブをインストールして表示する必要があります。また、導入が予想より低くなります。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-108">However, since it's a personal tab, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="b5ea7-109">言い換えると、多すぎるワーカーは、ヘルプ デスクに到達する方法をまだ知りません。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="b5ea7-110">チャネル タブを作成すると、この情報を見つけやすくすることができます。これにより、すべてのユーザーがアプリをインストールする必要が生じやすくなります。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="b5ea7-111">代わりに、1 人のユーザーがチャネルまたはチャットにタブを追加して、グループ全体を利用できます。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-111">Instead, one user can add the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="b5ea7-112">学習する情報</span><span class="sxs-lookup"><span data-stu-id="b5ea7-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="b5ea7-113">Microsoft Teams Toolkit for Visual Studio コードを使用してアプリ プロジェクトをVisual Studioする</span><span class="sxs-lookup"><span data-stu-id="b5ea7-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="b5ea7-114">チャネル タブに関連するアプリ構成とスキャフォールディングの一部を特定する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-114">Identify some of the app configurations and scaffolding relevant to channel tabs</span></span>
> * <span data-ttu-id="b5ea7-115">タブ コンテンツを作成する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-115">Create tab content</span></span>
> * <span data-ttu-id="b5ea7-116">タブの構成ページのコンテンツを作成する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-116">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="b5ea7-117">推奨されるタブ名を指定する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-117">Provide a suggested tab name</span></span>
> * <span data-ttu-id="b5ea7-118">アプリをローカルでビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-118">Build and run your app locally</span></span>
> * <span data-ttu-id="b5ea7-119">テスト用に Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="b5ea7-119">Sideload your app in Teams for testing</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b5ea7-120">はじめに</span><span class="sxs-lookup"><span data-stu-id="b5ea7-120">Before you begin</span></span>

<span data-ttu-id="b5ea7-121">まだ理解していない場合は、Teams 開発の前提条件 [を理解してインストールしてください](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-121">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="b5ea7-122">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-122">1. Create your app project</span></span>

<span data-ttu-id="b5ea7-123">Microsoft Teams Toolkit は、アプリを構成し、基本的な構成ページや "Hello, World!" を表示するコンテンツ ページなど、チャネルとグループのタブに関連するスキャフォールディングを設定するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-123">The Microsoft Teams Toolkit helps configure your app and set up scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="b5ea7-124">メッセージ。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-124">message.</span></span>

> [!TIP]
> <span data-ttu-id="b5ea7-125">Teams アプリ プロジェクトをまだ作成していない場合は、プロジェクトについて詳しく説明する次[](../build-your-first-app/build-and-run.md)の手順に従うのが役に立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-125">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. [Visual Studioコード] で、左側のアクティビティ バーで **Microsoft Teams** を選択し、[新しい Teams アプリの作成 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: ] **を選択します**。
1. <span data-ttu-id="b5ea7-127">ダイアログが表示されたら、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-127">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="b5ea7-128">[機能 **の追加] 画面で、[Tab]** を選択し **、[次へ** ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="b5ea7-129">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-129">Enter a name for your Teams app.</span></span> <span data-ttu-id="b5ea7-130">(これは、アプリの既定の名前と、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です)。[グループ **] または [Teams] チャネル タブを選択します**。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-130">(This is the default name for your app and also the name of the app project directory on your local machine.) Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="b5ea7-131">画面 **の** 下部にある [完了] を選択して、プロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-131">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="b5ea7-132">2. 関連するアプリ プロジェクト コンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-132">2. Identify relevant app project components</span></span>

<span data-ttu-id="b5ea7-133">ツールキットを使ってプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-133">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="b5ea7-134">チャネル タブを構築する主なコンポーネントを見てみしましょう。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-134">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="b5ea7-135">アプリの構成</span><span class="sxs-lookup"><span data-stu-id="b5ea7-135">App configurations</span></span>

<span data-ttu-id="b5ea7-136">ツールキットで **、App Studio に移動して** 、アプリの構成を表示および更新します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-136">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="b5ea7-137">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="b5ea7-137">App scaffolding</span></span>

<span data-ttu-id="b5ea7-138">アプリのスキャフォールディングは、Teams でチャネル タブをレンダリングするコンポーネントを提供します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-138">The app scaffolding provides the components for rendering your channel tab in Teams.</span></span> <span data-ttu-id="b5ea7-139">作業できる作業は多くあるのですが、今のところは次の作業に集中する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-139">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="b5ea7-140">プロジェクトのディレクトリにある 2 `src/components` つのファイル:</span><span class="sxs-lookup"><span data-stu-id="b5ea7-140">Two files located in the `src/components` directory of your project:</span></span>
  * <span data-ttu-id="b5ea7-141">`Tab.js` タブのコンテンツ ページをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-141">`Tab.js` for rendering your tab's content page.</span></span>
  * <span data-ttu-id="b5ea7-142">`TabConfig.js` タブの構成ページをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-142">`TabConfig.js` for rendering your tab's configuration page.</span></span>
* <span data-ttu-id="b5ea7-143">Microsoft Teams JavaScript クライアント SDK。プロジェクトのフロントエンド コンポーネントに事前に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-143">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="b5ea7-144">3. タブ コンテンツ ページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="b5ea7-144">3. Customize your tab content page</span></span>

<span data-ttu-id="b5ea7-145">組織に関連する情報を使用して次のスニペットをコピーして更新するか、時間の間、コードを使用します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-145">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

```JSX
<div>
  <h1>Important Contacts</h1>
    <ul>
      <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
      <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
      <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
    </ul>
</div>
```

<span data-ttu-id="b5ea7-146">ディレクトリに移動 `src/components` して開きます `Tab.js` 。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-146">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="b5ea7-147">関数を見 `render()` つけて、コンテンツを内部 `return()` に貼り付けます (図を参照)。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-147">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

```JavaScript
render() {

    let userName = Object.keys(this.state.context).length > 0 ? this.state.context['upn'] : "";

    return (
    <div>
      <h1>Important Contacts</h1>
        <ul>
          <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
          <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
          <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
        </ul>
    </div>
    );
}
```

<span data-ttu-id="b5ea7-148">使用するテーマに関係なく、電子メール リンクが読みやすくするために、次のルールを (同じ場所に `App.css` `src/components` ) 追加します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-148">Add the following rule to `App.css` (also located in `src/components`) so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="b5ea7-149">4. タブ構成ページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="b5ea7-149">4. Customize your tab configuration page</span></span>

<span data-ttu-id="b5ea7-150">チャネルまたはチャット内のすべてのタブには構成ページがあります。モーダルなモーダルで、ユーザーがアプリを追加するときに少なくとも 1 つのセットアップ オプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-150">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="b5ea7-151">既定では、構成ページは、タブのインストール時にチャネルまたはチャットに通知する必要がある場合にユーザーに確認を求めるメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-151">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="b5ea7-152">構成ページにカスタム コンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-152">Add some custom content to your configuration page.</span></span> <span data-ttu-id="b5ea7-153">プロジェクトのディレクトリに移動し、内部のプレースホルダー コンテンツを開いて更新 `src/components` `TabConfig.js` します (次の例 `return()` を参照)。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-153">Go to your project's `src/components` directory, open `TabConfig.js`, and update the placeholder content inside `return()` (as shown in the following example).</span></span>

```JavaScript
return (
    <div>
      <h1>Add My Contoso Contacts</h1>
      <div>
        Select <b>Save</b> to add our organization's important contacts to this workspace.
      </div>
    </div>
);
```
 
> [!TIP]
> <span data-ttu-id="b5ea7-154">少なくとも、このページでアプリに関する簡単な情報を提供してください。これは、ユーザーが初めて学習する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-154">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="b5ea7-155">また、カスタム構成オプションや、 [タブ構成ページ](../tabs/how-to/authentication/auth-aad-sso.md)で一般的な認証ワークフローを含めすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-155">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-provide-a-suggested-tab-name"></a><span data-ttu-id="b5ea7-156">5. 推奨されるタブ名を指定する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-156">5. Provide a suggested tab name</span></span>

<span data-ttu-id="b5ea7-157">チャネル タブを追加すると、既定でアプリ名 (たとえば、最初のアプリ) **が表示されます**。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-157">When you add a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="b5ea7-158">これは、アプリの呼び出しに応じて問題ありませんが、グループコラボレーションのコンテキスト (チーム連絡先など) で意味のある名前を付け加える必要がある場合 **があります**。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-158">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

1. <span data-ttu-id="b5ea7-159">In `TabConfig.js` に移動します `microsoftTeams.settings.setSettings` 。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-159">In `TabConfig.js`, go to `microsoftTeams.settings.setSettings`.</span></span>
2. <span data-ttu-id="b5ea7-160">既定で `suggestedDisplayName` 表示するタブ名を持つプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-160">Add the `suggestedDisplayName` property with the tab name you want to display by default.</span></span> 
3. <span data-ttu-id="b5ea7-161">次の例に示す名前を使用するか、名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-161">Use the name provided in the following example or type your name.</span></span> <span data-ttu-id="b5ea7-162">(既定では、ユーザーは名前を変更できます)。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-162">(By default, users can change the name.)</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="b5ea7-163">6. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-163">6. Build and run your app</span></span>

<span data-ttu-id="b5ea7-164">時間の問題として、アプリをローカルでビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-164">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="b5ea7-165">(この情報はツールキットでも利用 `README` できます)。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-165">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="b5ea7-166">ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、実行します `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-166">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="b5ea7-167">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-167">Run `npm start`.</span></span>

<span data-ttu-id="b5ea7-168">完了すると、コンパイルに **成功します。**</span><span class="sxs-lookup"><span data-stu-id="b5ea7-168">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="b5ea7-169">メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-169">message in the terminal.</span></span> <span data-ttu-id="b5ea7-170">アプリが実行されています `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-170">Your app is running on `https://localhost:3000`.</span></span>

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="b5ea7-171">7. Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="b5ea7-171">7. Sideload your app in Teams</span></span>

<span data-ttu-id="b5ea7-172">アプリは Teams でテストする準備が整っています。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-172">Your app is ready to test in Teams.</span></span> <span data-ttu-id="b5ea7-173">これを行うには、アプリのサイドローディングを許可するアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-173">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="b5ea7-174">(そのアカウントが分からない場合は、Teams 開発アカウントを取得する方法 [について説明します](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account))。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-174">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

1. <span data-ttu-id="b5ea7-175">コードVisual Studio **F5** キーを押して、Teams Web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-175">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="b5ea7-176">Teams でアプリのコンテンツを表示するには、アプリが実行されている場所 ( `localhost` ) が信頼できる場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-176">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="b5ea7-177">F5 キーを押した後に開いた同じブラウザー ウィンドウ (Google Chrome 既定) で新しいタブ **を開きます**。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-177">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="b5ea7-178">ページに `https://localhost:3000/tab` 移動し、ページに進みます。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-178">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="b5ea7-179">Teams に戻る。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-179">Go back to Teams.</span></span> <span data-ttu-id="b5ea7-180">モーダルで **、[チームに** 追加] または[チャットに追加] を選択し、テストに使用できるチャネルまたはチャットを探します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-180">In the modal, select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="b5ea7-181">[タブ **の設定] を選択します**。構成ページはモーダルで表示されます。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-181">Select **Set up a tab**. The configuration page displays in a modal.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="チャネル タブ構成ページのスクリーンショット。":::
1. <span data-ttu-id="b5ea7-183">[保存 **] を** 選択してタブを構成します。コンテンツ ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-183">Select **Save** to configure the tab. The content page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="静的コンテンツ ビューを含むチャネル タブのスクリーンショット。":::

## <a name="well-done"></a><span data-ttu-id="b5ea7-185">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="b5ea7-185">Well done</span></span>

<span data-ttu-id="b5ea7-186">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="b5ea7-186">Congratulations!</span></span> <span data-ttu-id="b5ea7-187">チャネルやチャットに便利なコンテンツを表示するためのタブを含む Teams アプリがあります。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-187">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="b5ea7-188">詳細情報</span><span class="sxs-lookup"><span data-stu-id="b5ea7-188">Learn more</span></span>

* <span data-ttu-id="b5ea7-189">[SSO を使用して](../tabs/how-to/authentication/auth-aad-sso.md)タブ ユーザーを認証する : 承認されたユーザーにのみタブを表示する場合は、Azure Active Directory (AD) を使用してシングル サインオン (SSO) を設定します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-189">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="b5ea7-190">[既存の Web アプリ](../tabs/how-to/add-tab.md#tab-requirements)または Web ページからコンテンツを埋め込む : タブの新しいコンテンツを作成する方法を説明しましたが、外部 URL からコンテンツを読み込む方法も示しました。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-190">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="b5ea7-191">[シームレスなタブ エクスペリエンスを作成](../tabs/design/tabs.md)する : Teams タブを設計する際の推奨ガイドラインを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-191">[Create a seamless tab experience](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="b5ea7-192">[モバイル用のタブの作成](../tabs/design/tabs-mobile.md): 携帯電話やタブレットのタブを開発する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-192">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="b5ea7-193">ツールキットを使用せずにタブを作成する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-193">Create a tab without the toolkit</span></span>](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)
* [<span data-ttu-id="b5ea7-194">Microsoft Graph で Teams データを利用する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-194">Utilize Teams data with Microsoft Graph</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)

## <a name="next-lesson"></a><span data-ttu-id="b5ea7-195">次のレッスン</span><span class="sxs-lookup"><span data-stu-id="b5ea7-195">Next lesson</span></span>

<span data-ttu-id="b5ea7-196">コラボレーション用のタブを作成する方法を知っている。</span><span class="sxs-lookup"><span data-stu-id="b5ea7-196">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="b5ea7-197">別の種類の Teams アプリを構築する場合</span><span class="sxs-lookup"><span data-stu-id="b5ea7-197">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5ea7-198">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="b5ea7-198">Build a bot</span></span>](../build-your-first-app/build-bot.md)
