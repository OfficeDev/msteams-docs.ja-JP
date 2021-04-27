---
title: '[スタート] - [個人用] タブを作成する'
author: heath-hamilton
description: Microsoft Teams を使用して Microsoft Teams の個人用タブをすばやく作成Toolkit。
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: dabe427142dd3e6a1d2f01f83601cbffd4a20dbd
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019980"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a><span data-ttu-id="d6dc3-103">Microsoft Teams の個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="d6dc3-103">Build a personal tab for Microsoft Teams</span></span>

<span data-ttu-id="d6dc3-104">タブは、基本的に Teams に Web ページを埋め込み、アプリ内のコンテンツを表示する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="d6dc3-105">Teams には 2 種類のタブがあります。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="d6dc3-106">このチュートリアルでは、基本的な個人用タブ 、個々のユーザーのフルスクリーン コンテンツ ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="d6dc3-107">(個人用タブは、Teams の従来の Web サイト エクスペリエンスに最も近いものです)。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d6dc3-108">はじめに</span><span class="sxs-lookup"><span data-stu-id="d6dc3-108">Before you begin</span></span>

<span data-ttu-id="d6dc3-109">開始するには、基本的な個人用タブが必要です。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="d6dc3-110">まだインストールされていない場合は、「ビルドして最初の [Teams アプリを実行する」を参照してください](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="d6dc3-111">割り当て</span><span class="sxs-lookup"><span data-stu-id="d6dc3-111">Your assignment</span></span>

<span data-ttu-id="d6dc3-112">組織内のユーザーは、重要な機能 (ヘルプ デスク、人事など) の基本的な連絡先情報を見つけるのに問題があります。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="d6dc3-113">この情報をすばやく 1 か所で見つけ出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="d6dc3-114">どのように行いますか?</span><span class="sxs-lookup"><span data-stu-id="d6dc3-114">How would you do that?</span></span> <span data-ttu-id="d6dc3-115">もちろん、Teams の個人用タブ。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="d6dc3-116">学習する情報</span><span class="sxs-lookup"><span data-stu-id="d6dc3-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="d6dc3-117">個人用タブに関連するアプリ構成とスキャフォールディングの一部を特定する</span><span class="sxs-lookup"><span data-stu-id="d6dc3-117">Identify some of the app configurations and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="d6dc3-118">タブ コンテンツの作成</span><span class="sxs-lookup"><span data-stu-id="d6dc3-118">Create tab content</span></span>
> * <span data-ttu-id="d6dc3-119">ユーザー設定に基づいてタブの色テーマを更新する</span><span class="sxs-lookup"><span data-stu-id="d6dc3-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="d6dc3-120">1. 関連するアプリ プロジェクト コンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="d6dc3-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="d6dc3-121">Teams を使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的にToolkit。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-121">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="d6dc3-122">個人用タブを作成する主要なコンポーネントについて説明します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="d6dc3-123">アプリの構成</span><span class="sxs-lookup"><span data-stu-id="d6dc3-123">App configurations</span></span>

<span data-ttu-id="d6dc3-124">ツールキットで、App Studio に **移動して** 、アプリ構成を表示および更新します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-124">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="d6dc3-125">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="d6dc3-125">App scaffolding</span></span>

<span data-ttu-id="d6dc3-126">アプリのスキャフォールディングは、Teams で個人用タブをレンダリングするコンポーネントを提供します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-126">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="d6dc3-127">多くの作業が可能ですが、今のところ、次の作業に集中する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-127">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="d6dc3-128">`Tab.js` ファイルをプロジェクト `src/components` のディレクトリに保存します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-128">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="d6dc3-129">これは、タブ コンテンツ ページのレンダリング用です。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-129">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="d6dc3-130">プロジェクトのフロントエンド コンポーネントに事前に読み込まれた Microsoft Teams JavaScript クライアント SDK。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-130">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="d6dc3-131">2. タブ コンテンツ ページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="d6dc3-131">2. Customize your tab content page</span></span>

<span data-ttu-id="d6dc3-132">組織内の重要な連絡先の一覧をコンパイルします。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-132">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="d6dc3-133">次のスニペットを、自分に関連する情報でコピーして更新するか、時間の間はコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-133">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="d6dc3-134">ディレクトリに移動 `src/components` して開きます `Tab.js` 。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-134">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="d6dc3-135">関数を見 `render()` つけて、コンテンツを (図のように) `return()` 内部に貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-135">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="d6dc3-136">次のルールを追加して、使用するテーマに関係なく電子メール リンク `App.css` を読みやすくします。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-136">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="d6dc3-137">変更内容を保存します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-137">Save your changes.</span></span> <span data-ttu-id="d6dc3-138">Teams のアプリのタブに移動して、新しいコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-138">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="静的コンテンツを含む個人用タブのスクリーンショット。":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="d6dc3-140">3. タブ テーマを更新する</span><span class="sxs-lookup"><span data-stu-id="d6dc3-140">3. Update the tab theme</span></span>

<span data-ttu-id="d6dc3-141">優れたアプリは Teams にネイティブだと感じるので、タブがユーザーが好む Teams テーマ (既定 (明るい、暗い、またはハイ コントラスト) とブレンドすることが重要です。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-141">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="d6dc3-142">前回のスクリーンショットで確認した場合と同様に、クライアントが暗いテーマを使用している場合、タブの背景は明るい色で表示されます。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-142">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="d6dc3-143">これは推奨されるユーザー エクスペリエンスではありません。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-143">This is not a recommended user experience.</span></span>

<span data-ttu-id="d6dc3-144">[Teams JavaScript クライアント SDK は](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)、アプリを認識し、クライアントのテーマの変更に対応できます。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-144">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="d6dc3-145">これを行う方法を見てみよ。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-145">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="d6dc3-146">Teams クライアントに関するコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="d6dc3-146">Get context about the Teams client</span></span>

<span data-ttu-id="d6dc3-147">ファイルには、構成済みのクライアント テーマについて、その他の詳細を示す `Tab.js` `microsoftTeams.getContext()` 呼び [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) 出しがあります。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-147">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="d6dc3-148">アプリのスキャフォールディングのおかげで、インターフェイスとそのプロパティにアクセスするには、このコード `context` を使用します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-148">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

```JavaScript
componentDidMount(){
  // Get the user context from Teams and set it in the state
  microsoftTeams.getContext((context, error) => {
    this.setState({
      context: context
    });
  });
  // Next steps: Error handling using the error object
}
```

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="d6dc3-149">テーマ変更ハンドラーを作成する</span><span class="sxs-lookup"><span data-stu-id="d6dc3-149">Create a theme change handler</span></span>

<span data-ttu-id="d6dc3-150">プロパティを使用すると、アプリは Teams の周囲で何が起こっているのかを `context` しっかりと理解できます。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-150">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="d6dc3-151">ただし、アプリは、ユーザーが選択したテーマを反映する必要がある外観をまだ知りません。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-151">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="d6dc3-152">アプリの状態がテーマと一緒に変更されるハンドラーが必要です。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-152">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="d6dc3-153">呼び出しの直後に、次のテーマ変更ハンドラーを挿入 `microsoftTeams.getContext()` します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-153">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="d6dc3-154">テーマのスタイルを一致する</span><span class="sxs-lookup"><span data-stu-id="d6dc3-154">Match theme styles</span></span>

<span data-ttu-id="d6dc3-155">テーマ変更ハンドラーが配置されますが、これらの変更に応答し、タブの色を現在のテーマに合わせて配置するコードが必要です。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-155">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="d6dc3-156">次の例は、タブにスタイルを適用する方法の 1 つです。コードを現在の方法で使用するか、展開するか、独自のコードを作成します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-156">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="d6dc3-157">関数で `render()` 、テーマ変更ハンドラーによって提供される状態をに格納します `isTheme` 。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-157">In the `render()` function, store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="d6dc3-158">テーマ変更ハンドラーによって提供される状態を格納した後、現在のテーマに基づいてタブのスタイルをレンダリングするための条件付きロジックを提供します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-158">After storing the state provided by the theme change handler, provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="d6dc3-159">次の例は、これを行う基本的な方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-159">The following example shows a basic way to do this:</span></span>
1. <span data-ttu-id="d6dc3-160">で現在のテーマを確認します `isTheme` 。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-160">Check the current theme in `isTheme`.</span></span>
2. <span data-ttu-id="d6dc3-161">現在の `newTheme` テーマに関連する CSS プロパティを持つオブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-161">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
3. <span data-ttu-id="d6dc3-162">タブ コンテンツのルート HTML 要素 () に CSS を適用します `<div style={newTheme}>` 。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-162">Apply the CSS to your tab content's root HTML element (`<div style={newTheme}>`).</span></span>

```JavaScript
let newTheme

if (isTheme === "default") {
  newTheme = {
    backgroundColor: "#EEF1F5",
    color: "#16233A"
  };
} else {
  newTheme = {
    backgroundColor: "#2B2B30",
    color: "#FFFFFF"
  };
}
```

<span data-ttu-id="d6dc3-163">Teams でタブを確認します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-163">Check your tab in Teams.</span></span> <span data-ttu-id="d6dc3-164">外観は暗いテーマと密接に一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="静的コンテンツ ビューを含む個人用タブのスクリーンショット。":::

## <a name="well-done"></a><span data-ttu-id="d6dc3-166">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="d6dc3-166">Well done</span></span>

<span data-ttu-id="d6dc3-167">お疲れさまでした。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-167">Congratulations!</span></span> <span data-ttu-id="d6dc3-168">組織の重要な連絡先を簡単に見つけやすくする個人用タブを持つ Teams アプリがあります。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="d6dc3-169">詳細情報</span><span class="sxs-lookup"><span data-stu-id="d6dc3-169">Learn more</span></span>

* <span data-ttu-id="d6dc3-170">シームレスな [エクスペリエンスを作成するには、](../tabs/design/tabs.md) 設計ガイドラインに従い、実稼働対応 [の UI](../concepts/design/design-teams-app-ui-templates.md) テンプレートを使用してビルドします。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-170">Follow our [design guidelines](../tabs/design/tabs.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* <span data-ttu-id="d6dc3-171">タブ [のモバイルに関する考慮事項](../tabs/design/tabs-mobile.md) について説明します。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-171">Understand [mobile considerations](../tabs/design/tabs-mobile.md) for tabs.</span></span>
* <span data-ttu-id="d6dc3-172">[タブに SSO 認証を追加します](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-172">[Add SSO authentication to your tab](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>
* <span data-ttu-id="d6dc3-173">Microsoft Graph で Teams データ [を利用する](https://docs.microsoft.com/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-173">Utilize Teams data with [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>
* <span data-ttu-id="d6dc3-174">[ツールキットを使用せずにタブを作成します](../tabs/quickstarts/create-personal-tab-node-yeoman.md)。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-174">[Create a tab without the toolkit](../tabs/quickstarts/create-personal-tab-node-yeoman.md).</span></span>

## <a name="next-lesson"></a><span data-ttu-id="d6dc3-175">次のレッスン</span><span class="sxs-lookup"><span data-stu-id="d6dc3-175">Next lesson</span></span>

<span data-ttu-id="d6dc3-176">個人用のタブを作成する方法を知っている。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-176">You know how to build a tab for personal use.</span></span> <span data-ttu-id="d6dc3-177">チーム チャネルとチャットのタブを作成するために必要な情報を見てみ取る。</span><span class="sxs-lookup"><span data-stu-id="d6dc3-177">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6dc3-178">チャネルのタブを作成する</span><span class="sxs-lookup"><span data-stu-id="d6dc3-178">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
