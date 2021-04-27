---
title: '[スタート] - [チャネルとグループ] タブを作成する'
author: heath-hamilton
description: Microsoft Teams チャネルとグループ タブを Microsoft Teams チャネルとグループ タブを使用してすばやく作成Toolkit。
ms.author: lajanuar
localization_priority: Normal
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: aadab4b6826b026eadd5ed564b6e5de5c29b4b1d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020878"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="29630-103">Microsoft Teams のチャネルとグループ タブを作成する</span><span class="sxs-lookup"><span data-stu-id="29630-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="29630-104">このチュートリアルでは、チーム チャネルまたはチャットのフルスクリーン ページである基本的なチャネルタブ *(グループ* タブとも呼ばれる) を作成します。</span><span class="sxs-lookup"><span data-stu-id="29630-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="29630-105">個人用タブとは異なり、ユーザーは、この種のタブのいくつかの側面を構成できます (たとえば、タブの名前を変更して、チャネルにとって意味のあるものにします)。</span><span class="sxs-lookup"><span data-stu-id="29630-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="29630-106">割り当て</span><span class="sxs-lookup"><span data-stu-id="29630-106">Your assignment</span></span>

<span data-ttu-id="29630-107">少し前に、組織はタブを使用して重要な連絡先情報 (ヘルプ デスク、人事など) を表示する Teams アプリを作成しました。</span><span class="sxs-lookup"><span data-stu-id="29630-107">Not long ago, your organization created a Teams app that uses a tab to display important contact information (help desk, HR, etc.).</span></span> <span data-ttu-id="29630-108">ただし、個人用タブだから、各ユーザーがタブをインストールして表示し、導入が予想より低くなります。</span><span class="sxs-lookup"><span data-stu-id="29630-108">However, since it's a personal tab, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="29630-109">つまり、ヘルプ デスクに到達する方法をまだ知らないワーカーが多すぎます。</span><span class="sxs-lookup"><span data-stu-id="29630-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="29630-110">チャネル タブを作成すると、この情報を見つけやすくすることができます。これにより、すべてのユーザーにアプリのインストールを要求する負担が軽減されます。</span><span class="sxs-lookup"><span data-stu-id="29630-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="29630-111">代わりに、1 人のユーザーがグループ全体の利益のために、チャネルまたはチャットにタブを追加できます。</span><span class="sxs-lookup"><span data-stu-id="29630-111">Instead, one user can add the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="29630-112">学習する情報</span><span class="sxs-lookup"><span data-stu-id="29630-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="29630-113">Microsoft Teams を使用してアプリ プロジェクトを作成ToolkitコードVisual Studioする</span><span class="sxs-lookup"><span data-stu-id="29630-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="29630-114">チャネル タブに関連するアプリ構成とスキャフォールディングの一部を特定する</span><span class="sxs-lookup"><span data-stu-id="29630-114">Identify some of the app configurations and scaffolding relevant to channel tabs</span></span>
> * <span data-ttu-id="29630-115">タブ コンテンツの作成</span><span class="sxs-lookup"><span data-stu-id="29630-115">Create tab content</span></span>
> * <span data-ttu-id="29630-116">タブの構成ページのコンテンツを作成する</span><span class="sxs-lookup"><span data-stu-id="29630-116">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="29630-117">推奨されるタブ名を指定する</span><span class="sxs-lookup"><span data-stu-id="29630-117">Provide a suggested tab name</span></span>
> * <span data-ttu-id="29630-118">アプリをローカルでビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="29630-118">Build and run your app locally</span></span>
> * <span data-ttu-id="29630-119">テスト用に Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="29630-119">Sideload your app in Teams for testing</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="29630-120">はじめに</span><span class="sxs-lookup"><span data-stu-id="29630-120">Before you begin</span></span>

<span data-ttu-id="29630-121">まだインストールしていない場合は、Teams 開発の [前提条件を理解してインストールしてください](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="29630-121">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="29630-122">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="29630-122">1. Create your app project</span></span>

<span data-ttu-id="29630-123">Microsoft Teams Toolkitは、アプリを構成し、チャネルタブとグループ タブに関連するスキャフォールディングを設定するのに役立ちます。基本的な構成ページや、"Hello, World!</span><span class="sxs-lookup"><span data-stu-id="29630-123">The Microsoft Teams Toolkit helps configure your app and set up scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="29630-124">メッセージ。</span><span class="sxs-lookup"><span data-stu-id="29630-124">message.</span></span>

> [!TIP]
> <span data-ttu-id="29630-125">以前に Teams アプリ プロジェクトを作成したことがない場合は、プロジェクトの詳細を[](../build-your-first-app/build-and-run.md)説明する手順に従うのが役に立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="29630-125">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。
1. <span data-ttu-id="29630-127">メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="29630-127">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="29630-128">[**機能の追加**] 画面で、[**タブ**] を選択し、[**次へ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="29630-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="29630-129">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="29630-129">Enter a name for your Teams app.</span></span> <span data-ttu-id="29630-130">(これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です)。[グループ **] または [Teams チャネル] タブを選択します**。</span><span class="sxs-lookup"><span data-stu-id="29630-130">(This is the default name for your app and also the name of the app project directory on your local machine.) Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="29630-131">画面 **の下部** にある [完了] を選択して、プロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="29630-131">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="29630-132">2. 関連するアプリ プロジェクト コンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="29630-132">2. Identify relevant app project components</span></span>

<span data-ttu-id="29630-133">ツールキットを使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="29630-133">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="29630-134">チャネル タブを作成する主要なコンポーネントを見てみ取ってみろ。</span><span class="sxs-lookup"><span data-stu-id="29630-134">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="29630-135">アプリの構成</span><span class="sxs-lookup"><span data-stu-id="29630-135">App configurations</span></span>

<span data-ttu-id="29630-136">ツールキットで、App Studio に **移動して** 、アプリ構成を表示および更新します。</span><span class="sxs-lookup"><span data-stu-id="29630-136">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="29630-137">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="29630-137">App scaffolding</span></span>

<span data-ttu-id="29630-138">アプリのスキャフォールディングは、Teams でチャネル タブをレンダリングするコンポーネントを提供します。</span><span class="sxs-lookup"><span data-stu-id="29630-138">The app scaffolding provides the components for rendering your channel tab in Teams.</span></span> <span data-ttu-id="29630-139">多くの作業が可能ですが、今のところ、次の作業に集中する必要があります。</span><span class="sxs-lookup"><span data-stu-id="29630-139">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="29630-140">プロジェクトのディレクトリに 2 `src/components` つのファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="29630-140">Two files located in the `src/components` directory of your project:</span></span>
  * <span data-ttu-id="29630-141">`Tab.js` タブのコンテンツ ページをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="29630-141">`Tab.js` for rendering your tab's content page.</span></span>
  * <span data-ttu-id="29630-142">`TabConfig.js` タブの構成ページをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="29630-142">`TabConfig.js` for rendering your tab's configuration page.</span></span>
* <span data-ttu-id="29630-143">プロジェクトのフロントエンド コンポーネントに事前に読み込まれた Microsoft Teams JavaScript クライアント SDK。</span><span class="sxs-lookup"><span data-stu-id="29630-143">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="29630-144">3. タブ コンテンツ ページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="29630-144">3. Customize your tab content page</span></span>

<span data-ttu-id="29630-145">組織に関連する情報を含む次のスニペットをコピーして更新するか、時間の間はコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="29630-145">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="29630-146">ディレクトリに移動 `src/components` して開きます `Tab.js` 。</span><span class="sxs-lookup"><span data-stu-id="29630-146">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="29630-147">関数を見 `render()` つけて、コンテンツを (図のように) `return()` 内部に貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="29630-147">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="29630-148">使用するテーマに関係なく、電子メール リンクを読みやすくするために、次のルールを (に含む `App.css` `src/components` ) に追加します。</span><span class="sxs-lookup"><span data-stu-id="29630-148">Add the following rule to `App.css` (also located in `src/components`) so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="29630-149">4. タブ構成ページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="29630-149">4. Customize your tab configuration page</span></span>

<span data-ttu-id="29630-150">チャネルまたはチャットのすべてのタブには構成ページがあります。モーダルで、ユーザーがアプリを追加するときに少なくとも 1 つのセットアップ オプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="29630-150">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="29630-151">既定では、構成ページは、タブがインストールされているときにチャネルまたはチャットに通知する必要がある場合に、ユーザーに通知を求めるメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="29630-151">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="29630-152">構成ページにカスタム コンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="29630-152">Add some custom content to your configuration page.</span></span> <span data-ttu-id="29630-153">プロジェクトのディレクトリに移動し、開き、内部のプレースホルダー コンテンツ `src/components` `TabConfig.js` を更新します (次 `return()` の例に示すように)。</span><span class="sxs-lookup"><span data-stu-id="29630-153">Go to your project's `src/components` directory, open `TabConfig.js`, and update the placeholder content inside `return()` (as shown in the following example).</span></span>

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
> <span data-ttu-id="29630-154">少なくとも、このページでアプリに関する簡単な情報は、ユーザーが初めて学習する場合があります。</span><span class="sxs-lookup"><span data-stu-id="29630-154">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="29630-155">カスタム構成オプションや、タブ構成ページで一般的 [な](../tabs/how-to/authentication/auth-aad-sso.md)認証ワークフローを含めすることもできます。</span><span class="sxs-lookup"><span data-stu-id="29630-155">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-provide-a-suggested-tab-name"></a><span data-ttu-id="29630-156">5. 推奨されるタブ名を指定する</span><span class="sxs-lookup"><span data-stu-id="29630-156">5. Provide a suggested tab name</span></span>

<span data-ttu-id="29630-157">チャネル タブを追加すると、既定でアプリ名が表示されます (ファースト アプリ **など**)。</span><span class="sxs-lookup"><span data-stu-id="29630-157">When you add a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="29630-158">これは、アプリの呼び出し内容に応じて問題ありませんが、グループの共同作業 (チーム連絡先など) のコンテキストで意味のある名前を指定することもできます **。**</span><span class="sxs-lookup"><span data-stu-id="29630-158">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

1. <span data-ttu-id="29630-159">に `TabConfig.js` 移動します `microsoftTeams.settings.setSettings` 。</span><span class="sxs-lookup"><span data-stu-id="29630-159">In `TabConfig.js`, go to `microsoftTeams.settings.setSettings`.</span></span>
2. <span data-ttu-id="29630-160">既定で `suggestedDisplayName` 表示するタブ名を含むプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="29630-160">Add the `suggestedDisplayName` property with the tab name you want to display by default.</span></span> 
3. <span data-ttu-id="29630-161">次の例に示す名前を使用するか、名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="29630-161">Use the name provided in the following example or type your name.</span></span> <span data-ttu-id="29630-162">(既定では、ユーザーは名前を変更できます)。</span><span class="sxs-lookup"><span data-stu-id="29630-162">(By default, users can change the name.)</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="29630-163">6. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="29630-163">6. Build and run your app</span></span>

<span data-ttu-id="29630-164">時間に関して、アプリをローカルでビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="29630-164">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="29630-165">(この情報はツールキットでも利用 `README` できます。)</span><span class="sxs-lookup"><span data-stu-id="29630-165">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="29630-166">ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、`npm install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="29630-166">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="29630-167">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="29630-167">Run `npm start`.</span></span>

<span data-ttu-id="29630-168">完了すると、[**正常にコンパイルされました**] と表示されます。</span><span class="sxs-lookup"><span data-stu-id="29630-168">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="29630-169">ターミナルのメッセージ。</span><span class="sxs-lookup"><span data-stu-id="29630-169">message in the terminal.</span></span> <span data-ttu-id="29630-170">お使いのアプリは `https://localhost:3000` で動作しています。</span><span class="sxs-lookup"><span data-stu-id="29630-170">Your app is running on `https://localhost:3000`.</span></span>

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="29630-171">7. Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="29630-171">7. Sideload your app in Teams</span></span>

<span data-ttu-id="29630-172">お使いのアプリは Teams でテストする準備ができています。</span><span class="sxs-lookup"><span data-stu-id="29630-172">Your app is ready to test in Teams.</span></span> <span data-ttu-id="29630-173">これを行うには、アプリのサイドローディングを許可するアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="29630-173">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="29630-174">(確信が持てない場合は、Teams 開発アカウントを取得する方法 [について説明します](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)。)</span><span class="sxs-lookup"><span data-stu-id="29630-174">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

1. <span data-ttu-id="29630-175">[Visual Studioコード] で **、F5** キーを押して Teams Web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="29630-175">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="29630-176">アプリ コンテンツを Teams で表示するには、信頼できるアプリを実行する場所 (`localhost`) を指定します。</span><span class="sxs-lookup"><span data-stu-id="29630-176">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="29630-177">**F5** を押した後に開いたのと同じブラウザー ウィンドウ (既定では Google Chrome) で新しいタブを開きます。</span><span class="sxs-lookup"><span data-stu-id="29630-177">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="29630-178">`https://localhost:3000/tab` に進み、ページを進めます。</span><span class="sxs-lookup"><span data-stu-id="29630-178">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="29630-179">Teams に戻ります。</span><span class="sxs-lookup"><span data-stu-id="29630-179">Go back to Teams.</span></span> <span data-ttu-id="29630-180">モーダルで、[チームに追加 **]** または[チャットに追加] を選択し、テストに使用できるチャネルまたはチャットを探します。</span><span class="sxs-lookup"><span data-stu-id="29630-180">In the modal, select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="29630-181">[タブ **の設定] を選択します**。構成ページはモーダルで表示されます。</span><span class="sxs-lookup"><span data-stu-id="29630-181">Select **Set up a tab**. The configuration page displays in a modal.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="チャネル タブ構成ページのスクリーンショット。":::
1. <span data-ttu-id="29630-183">[保存 **] を** 選択してタブを構成します。コンテンツ ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="29630-183">Select **Save** to configure the tab. The content page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="静的コンテンツ ビューを含むチャネル タブのスクリーンショット。":::

## <a name="well-done"></a><span data-ttu-id="29630-185">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="29630-185">Well done</span></span>

<span data-ttu-id="29630-186">お疲れさまでした。</span><span class="sxs-lookup"><span data-stu-id="29630-186">Congratulations!</span></span> <span data-ttu-id="29630-187">チャネルやチャットに便利なコンテンツを表示するためのタブを含む Teams アプリがあります。</span><span class="sxs-lookup"><span data-stu-id="29630-187">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="29630-188">詳細情報</span><span class="sxs-lookup"><span data-stu-id="29630-188">Learn more</span></span>

* <span data-ttu-id="29630-189">シームレスな [エクスペリエンスを作成するには、](../tabs/design/tabs.md) 設計ガイドラインに従い、実稼働対応 [の UI](../concepts/design/design-teams-app-ui-templates.md) テンプレートを使用してビルドします。</span><span class="sxs-lookup"><span data-stu-id="29630-189">Follow our [design guidelines](../tabs/design/tabs.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* <span data-ttu-id="29630-190">タブ [のモバイルに関する考慮事項](../tabs/design/tabs-mobile.md) について説明します。</span><span class="sxs-lookup"><span data-stu-id="29630-190">Understand [mobile considerations](../tabs/design/tabs-mobile.md) for tabs.</span></span>
* <span data-ttu-id="29630-191">[タブに SSO 認証を追加します](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="29630-191">[Add SSO authentication to your tab](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>
* <span data-ttu-id="29630-192">Microsoft Graph で Teams データ [を利用する](https://docs.microsoft.com/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="29630-192">Utilize Teams data with [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>
* [<span data-ttu-id="29630-193">ツールキットを使用せずにタブを作成する</span><span class="sxs-lookup"><span data-stu-id="29630-193">Create a tab without the toolkit</span></span>](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)

## <a name="next-lesson"></a><span data-ttu-id="29630-194">次のレッスン</span><span class="sxs-lookup"><span data-stu-id="29630-194">Next lesson</span></span>

<span data-ttu-id="29630-195">コラボレーション用のタブを作成する方法を知っています。</span><span class="sxs-lookup"><span data-stu-id="29630-195">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="29630-196">別の種類の Teams アプリの構築を試みませんか?</span><span class="sxs-lookup"><span data-stu-id="29630-196">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="29630-197">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="29630-197">Build a bot</span></span>](../build-your-first-app/build-bot.md)
