---
title: 「はじめに」-「チャネルとグループの作成」タブ
author: heath-hamilton
description: Microsoft Teams ツールキットを使用して、Microsoft Teams のチャネルとグループタブをすばやく作成できます。
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 46b5410a1ae7c866f8998362765dfe5462df94cb
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931765"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="d5c58-103">Microsoft Teams の [チャネルとグループの作成] タブ</span><span class="sxs-lookup"><span data-stu-id="d5c58-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="d5c58-104">このチュートリアルでは、チームチャネルまたはチャットの全画面ページである基本 *チャネルタブ* ( *グループタブ* とも呼ばれます) を作成します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab* ), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="d5c58-105">[個人用] タブとは異なり、ユーザーはこの種類のタブのいくつかの側面を構成できます (たとえば、タブの名前を変更して、チャネルにとって意味がある場合)。</span><span class="sxs-lookup"><span data-stu-id="d5c58-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="d5c58-106">自分の割り当て</span><span class="sxs-lookup"><span data-stu-id="d5c58-106">Your assignment</span></span>

<span data-ttu-id="d5c58-107">以前は、タブを使用して重要な連絡先情報 (ヘルプデスク、人事など) を表示する Teams アプリを作成しています。</span><span class="sxs-lookup"><span data-stu-id="d5c58-107">Not long ago, your organization created a Teams app that uses a tab to display important contact information (help desk, HR, etc.).</span></span> <span data-ttu-id="d5c58-108">ただし、[個人用] タブなので、各ユーザーは、そのタブをインストールして表示する必要があり、導入が予想よりも低いことを示します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-108">However, since it's a personal tab, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="d5c58-109">つまり、まだ多くのワーカーがヘルプデスクに到達する方法がわからない場合があります。</span><span class="sxs-lookup"><span data-stu-id="d5c58-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="d5c58-110">[チャネル] タブを作成することによって、この情報を見つけやすくすることができます。これにより、アプリのインストールをすべてのユーザーに対して要求する手間が軽減されます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="d5c58-111">代わりに、1人のユーザーがチャネルまたはチャットにタブを追加して、グループ全体の利点を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-111">Instead, one user can add the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="d5c58-112">学習内容</span><span class="sxs-lookup"><span data-stu-id="d5c58-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="d5c58-113">Microsoft Teams Toolkit for Visual Studio Code を使用してアプリプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="d5c58-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="d5c58-114">チャネルおよびグループのタブに関連するアプリの構成とスキャフォールディングの一部を特定する</span><span class="sxs-lookup"><span data-stu-id="d5c58-114">Identify some of the app configurations and scaffolding relevant to channel and group tabs</span></span>
> * <span data-ttu-id="d5c58-115">タブのコンテンツを作成する</span><span class="sxs-lookup"><span data-stu-id="d5c58-115">Create tab content</span></span>
> * <span data-ttu-id="d5c58-116">タブの構成ページのコンテンツを作成する</span><span class="sxs-lookup"><span data-stu-id="d5c58-116">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="d5c58-117">提案されたタブ名を指定する</span><span class="sxs-lookup"><span data-stu-id="d5c58-117">Provide a suggested tab name</span></span>
> * <span data-ttu-id="d5c58-118">アプリをローカルでビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="d5c58-118">Build and run your app locally</span></span>
> * <span data-ttu-id="d5c58-119">テストのために Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="d5c58-119">Sideload your app in Teams for testing</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d5c58-120">はじめに</span><span class="sxs-lookup"><span data-stu-id="d5c58-120">Before you begin</span></span>

<span data-ttu-id="d5c58-121">まだお持ちでない場合は、 [Teams 開発の前提条件を理解し、インストール](build-first-app-overview.md#get-prerequisites)してください。</span><span class="sxs-lookup"><span data-stu-id="d5c58-121">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="d5c58-122">1. アプリプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-122">1. Create your app project</span></span>

<span data-ttu-id="d5c58-123">Microsoft Teams ツールキットは、アプリを構成し、[チャネル] タブおよび [グループ] タブに関連するスキャフォールディングをセットアップするのに役立ちます。これには、基本的な構成ページと、"Hello, World!" を表示するコンテンツページが含まれます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-123">The Microsoft Teams Toolkit helps configure your app and set up scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="d5c58-124">メッセージ。</span><span class="sxs-lookup"><span data-stu-id="d5c58-124">message.</span></span>

> [!TIP]
> <span data-ttu-id="d5c58-125">以前に Teams アプリプロジェクトを作成していない場合は、 [以下の手順](../build-your-first-app/build-and-run.md) に従って、プロジェクトについて詳しく説明することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d5c58-125">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成** ] を選択します。
1. <span data-ttu-id="d5c58-127">メッセージが表示されたら、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="d5c58-127">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="d5c58-128">[ **機能の追加** ] 画面で、[ **タブ]** 、[ **次へ** ] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="d5c58-129">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-129">Enter a name for your Teams app.</span></span> <span data-ttu-id="d5c58-130">(これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)</span><span class="sxs-lookup"><span data-stu-id="d5c58-130">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="d5c58-131">[ **個人用] タブ** および [ **グループ] または [チームチャネル] タブ** のオプションを確認します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-131">Check the **Personal tab** and **Group or Teams channel tab** options.</span></span> <span data-ttu-id="d5c58-132">(両方の種類のタブが必要な理由については、すぐに説明します)。</span><span class="sxs-lookup"><span data-stu-id="d5c58-132">(You'll soon learn why you need both types of tabs.)</span></span>
1. <span data-ttu-id="d5c58-133">画面の下部にある [ **完了** ] を選択して、プロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-133">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="d5c58-134">2. 関連するアプリプロジェクトコンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="d5c58-134">2. Identify relevant app project components</span></span>

<span data-ttu-id="d5c58-135">Teams ツールキットを使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-135">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="d5c58-136">[チャネルとグループ] タブを構築するための主なコンポーネントについて見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="d5c58-136">Let's look at the main components for building a channel and group tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="d5c58-137">アプリの構成</span><span class="sxs-lookup"><span data-stu-id="d5c58-137">App configurations</span></span>

<span data-ttu-id="d5c58-138">アプリの構成は、ツールキットに含まれる App Studio を使用して表示および更新できます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-138">You can view and update your app configurations using App Studio, which is included in the toolkit.</span></span>

<span data-ttu-id="d5c58-139">セットアップ時に、ツールキットは、最初はチャネルとグループのタブの2つの重要なコンポーネントを構成しました。</span><span class="sxs-lookup"><span data-stu-id="d5c58-139">During setup, the toolkit initially configured two essential components of channel and group tabs:</span></span>

* <span data-ttu-id="d5c58-140">[ **構成] ページ** : チャネルまたはチャットにタブを追加するためのダイアログ。</span><span class="sxs-lookup"><span data-stu-id="d5c58-140">**Configuration page** : The dialog for adding a tab to a channel or chat.</span></span> <span data-ttu-id="d5c58-141">(アプリ Studio では、[ **チーム] タブ > タブ** に移動して、このページを見つけることができます)。</span><span class="sxs-lookup"><span data-stu-id="d5c58-141">(In App Studio, you can find this page by going to **Tabs > Team tab**.)</span></span>
* <span data-ttu-id="d5c58-142">**コンテンツページ** : プライマリコンテンツを表示する場所。</span><span class="sxs-lookup"><span data-stu-id="d5c58-142">**Content page** : Where you display your primary content.</span></span> <span data-ttu-id="d5c58-143">(アプリ Studio では、 **タブ > [個人用] タブ** に移動することで、このページを見つけることができます)。</span><span class="sxs-lookup"><span data-stu-id="d5c58-143">(In App Studio, you can find this page by going to **Tabs > Add a personal tab**.)</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="d5c58-144">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="d5c58-144">App scaffolding</span></span>

<span data-ttu-id="d5c58-145">アプリのスキャフォールディングは、Teams で個人用タブを表示するためのコンポーネントを提供します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-145">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="d5c58-146">多くの作業を行うことができますが、現時点では、次の点を重視するだけで十分です。</span><span class="sxs-lookup"><span data-stu-id="d5c58-146">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="d5c58-147">プロジェクトのディレクトリにある2つのファイル `src/components` :</span><span class="sxs-lookup"><span data-stu-id="d5c58-147">Two files located in the `src/components` directory of your project:</span></span>
  * <span data-ttu-id="d5c58-148">`Tab.js` タブのコンテンツページをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="d5c58-148">`Tab.js` for rendering your tab's content page.</span></span>
  * <span data-ttu-id="d5c58-149">`TabConfig.js` タブの構成ページをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="d5c58-149">`TabConfig.js` for rendering your tab's configuration page.</span></span>
* <span data-ttu-id="d5c58-150">Microsoft Teams JavaScript クライアント SDK。これは、プロジェクトのフロントエンドコンポーネントに事前に読み込まれています。</span><span class="sxs-lookup"><span data-stu-id="d5c58-150">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="d5c58-151">3. タブのコンテンツページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="d5c58-151">3. Customize your tab content page</span></span>

<span data-ttu-id="d5c58-152">次のスニペットを、組織に関連する情報でコピーして更新するか、または時間のためにコードをそのように使用します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-152">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="d5c58-153">ディレクトリに移動 `src/components` し、を開き `Tab.js` ます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-153">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="d5c58-154">関数を検索し、その `render()` 中にコンテンツを貼り付け `return()` ます (図を参照)。</span><span class="sxs-lookup"><span data-stu-id="d5c58-154">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="d5c58-155">`App.css` `src/components` どのテーマが使用されていても、電子メールリンクが読みやすくなるように、次のルールを (にも) 追加します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-155">Add the following rule to `App.css` (also located in `src/components`) so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="d5c58-156">4. タブの構成ページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="d5c58-156">4. Customize your tab configuration page</span></span>

<span data-ttu-id="d5c58-157">チャネルまたはチャットのすべてのタブには構成ページがあり、ユーザーがアプリを追加したときに表示されるセットアップオプションが1つ以上あるダイアログ。</span><span class="sxs-lookup"><span data-stu-id="d5c58-157">Every tab in a channel or chat has a configuration page, a dialog with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="d5c58-158">既定では、構成ページは、タブがインストールされたときにチャネルまたはチャットに通知するかどうかをユーザーに確認します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-158">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="d5c58-159">カスタムコンテンツを構成ページに追加します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-159">Add some custom content to your configuration page.</span></span> <span data-ttu-id="d5c58-160">プロジェクトのディレクトリに移動し、 `src/components` `TabConfig.js` プレースホルダーのコンテンツを `return()` (次の例に示すように) 表示して、更新します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-160">Go to your project's `src/components` directory, open `TabConfig.js`, and update the placeholder content inside `return()` (as shown in the following example).</span></span>

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
> <span data-ttu-id="d5c58-161">少なくとも、ユーザーが初めて理解しているときに、このページにあるアプリについて簡単な情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-161">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="d5c58-162">また、タブの構成ページに共通のカスタム構成オプションまたは [認証ワークフロー](../tabs/how-to/authentication/auth-aad-sso.md)を含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-162">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-provide-a-suggested-tab-name"></a><span data-ttu-id="d5c58-163">5. 提案されたタブ名を指定する</span><span class="sxs-lookup"><span data-stu-id="d5c58-163">5. Provide a suggested tab name</span></span>

<span data-ttu-id="d5c58-164">チャネルまたはグループタブを追加すると、既定ではアプリケーション名が表示されます (たとえば、 **最初のアプリ** )。</span><span class="sxs-lookup"><span data-stu-id="d5c58-164">When you add a channel or group tab, by default the app name displays (for example, **first-app** ).</span></span>

<span data-ttu-id="d5c58-165">これは、アプリの呼び出し方法によっては適切な場合もありますが、グループコラボレーションのコンテキスト (たとえば、 **チーム連絡先** ) にとってわかりやすい名前を指定することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d5c58-165">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts** ).</span></span>

<span data-ttu-id="d5c58-166">で `TabConfig.js` 、に移動 `microsoftTeams.settings.setSettings` します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-166">In `TabConfig.js`, go to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="d5c58-167">`suggestedDisplayName`既定で表示するタブ名を持つプロパティを追加します (表示されています)。</span><span class="sxs-lookup"><span data-stu-id="d5c58-167">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="d5c58-168">指定した名前を使用するか、独自の名前を作成します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-168">Use the provided name or create your own.</span></span> <span data-ttu-id="d5c58-169">(既定では、ユーザーは必要に応じて名前を変更できます。)</span><span class="sxs-lookup"><span data-stu-id="d5c58-169">(By default, users to change the name if they want.)</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="d5c58-170">6. アプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-170">6. Build and run your app</span></span>

<span data-ttu-id="d5c58-171">時間の経過とともに、アプリをローカルでビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-171">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="d5c58-172">(この情報は、ツールキットでも利用でき `README` ます。)</span><span class="sxs-lookup"><span data-stu-id="d5c58-172">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="d5c58-173">ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-173">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="d5c58-174">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-174">Run `npm start`.</span></span>

<span data-ttu-id="d5c58-175">完了すると、 **コンパイルに成功** しました。</span><span class="sxs-lookup"><span data-stu-id="d5c58-175">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="d5c58-176">ターミナルのメッセージ。</span><span class="sxs-lookup"><span data-stu-id="d5c58-176">message in the terminal.</span></span> <span data-ttu-id="d5c58-177">アプリが実行されている `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="d5c58-177">Your app is running on `https://localhost:3000`.</span></span>

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="d5c58-178">7. Teams でアプリをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="d5c58-178">7. Sideload your app in Teams</span></span>

<span data-ttu-id="d5c58-179">アプリは Teams でテストする準備ができています。</span><span class="sxs-lookup"><span data-stu-id="d5c58-179">Your app is ready to test in Teams.</span></span> <span data-ttu-id="d5c58-180">これを行うには、アプリのサイドロードを許可するアカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="d5c58-180">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="d5c58-181">(あるかどうかがわからない場合は、 [Teams 開発アカウント](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)の取得についてを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="d5c58-181">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

1. <span data-ttu-id="d5c58-182">Visual Studio Code で、 **F5** キーを押して Teams web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-182">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="d5c58-183">Teams でアプリのコンテンツを表示するには、アプリが実行されている場所 () を信頼するように指定し `localhost` ます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-183">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="d5c58-184">**F5** キーを押した後に開いた同じブラウザーウィンドウ (既定では Google Chrome) で新しいタブを開きます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-184">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="d5c58-185">に移動 `https://localhost:3000/tab` して、ページに進みます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-185">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="d5c58-186">Teams に戻ります。</span><span class="sxs-lookup"><span data-stu-id="d5c58-186">Go back to Teams.</span></span> <span data-ttu-id="d5c58-187">ダイアログで、[ **チームに追加する** ] または [ **チャットに追加** する] を選択し、テストに使用できるチャネルまたはチャットを探します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-187">In the dialog, select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="d5c58-188">[ **タブの設定]** を選択します。構成ページがダイアログボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-188">Select **Set up a tab**. The configuration page displays in a dialog.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="[チャネル] タブの構成ページのスクリーンショット。":::
1. <span data-ttu-id="d5c58-190">[ **保存** ] を選択してタブを構成します。コンテンツページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-190">Select **Save** to configure the tab. The content page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="静的コンテンツビューがある [チャネル] タブのスクリーンショット。":::

## <a name="well-done"></a><span data-ttu-id="d5c58-192">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="d5c58-192">Well done</span></span>

<span data-ttu-id="d5c58-193">おめでとうございます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-193">Congratulations!</span></span> <span data-ttu-id="d5c58-194">Teams アプリには、チャネルとチャットに役立つコンテンツを表示するためのタブがあります。</span><span class="sxs-lookup"><span data-stu-id="d5c58-194">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="d5c58-195">詳細情報</span><span class="sxs-lookup"><span data-stu-id="d5c58-195">Learn more</span></span>

* <span data-ttu-id="d5c58-196">[認証タブのユーザーに SSO を使用](../tabs/how-to/authentication/auth-aad-sso.md)する: 承認されたユーザーのみにタブを表示する場合は、Azure Active DIRECTORY (AD) を使用してシングルサインオン (SSO) を設定します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-196">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="d5c58-197">[既存の web アプリまたは web ページからコンテンツを埋め込む](../tabs/how-to/add-tab.md#tab-requirements): [個人用] タブの新しいコンテンツを作成する方法を示しましたが、外部 URL からコンテンツを読み込むこともできます。</span><span class="sxs-lookup"><span data-stu-id="d5c58-197">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="d5c58-198">[タブに対してシームレスな環境を作成する](../tabs/design/tabs.md): Teams タブの設計に関する推奨ガイドラインを参照してください。</span><span class="sxs-lookup"><span data-stu-id="d5c58-198">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="d5c58-199">[モバイル用のタブの作成](../tabs/design/tabs-mobile.md): 電話とタブレットのタブを開発する方法について理解します。</span><span class="sxs-lookup"><span data-stu-id="d5c58-199">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="d5c58-200">Microsoft Graph API で Teams データを利用する</span><span class="sxs-lookup"><span data-stu-id="d5c58-200">Utilize Teams data with the Microsoft Graph API</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="d5c58-201">ツールキットなしでタブを作成する</span><span class="sxs-lookup"><span data-stu-id="d5c58-201">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="d5c58-202">次のレッスン</span><span class="sxs-lookup"><span data-stu-id="d5c58-202">Next lesson</span></span>

<span data-ttu-id="d5c58-203">グループ作業用のタブを作成する方法を理解していること。</span><span class="sxs-lookup"><span data-stu-id="d5c58-203">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="d5c58-204">別の種類の Teams アプリを作成しようとしていますか?</span><span class="sxs-lookup"><span data-stu-id="d5c58-204">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d5c58-205">Bot を作成する</span><span class="sxs-lookup"><span data-stu-id="d5c58-205">Build a bot</span></span>](../build-your-first-app/build-bot.md)
