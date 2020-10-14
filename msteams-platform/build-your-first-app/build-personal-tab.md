---
title: 作業の開始-個人用タブの作成
author: heath-hamilton
description: Microsoft Teams ツールキットを使用して、Microsoft Teams の [個人] タブをすばやく作成できます。
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 7c12c87fff5126662f9473ecb0c5838b61f5faf2
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452744"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a><span data-ttu-id="25fd2-103">Microsoft Teams 用の個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="25fd2-103">Build a personal tab for Microsoft Teams</span></span>

<span data-ttu-id="25fd2-104">タブは、Teams に web ページを埋め込むことで、アプリ内にコンテンツを表示する簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="25fd2-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="25fd2-105">Teams には、2種類のタブがあります。</span><span class="sxs-lookup"><span data-stu-id="25fd2-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="25fd2-106">このチュートリアルでは、個々のユーザーのために全画面表示のコンテンツページである [個人用の基本 *] タブ*を作成します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="25fd2-107">(個人タブは、Teams で従来の web サイトの操作に最も近いものです)。</span><span class="sxs-lookup"><span data-stu-id="25fd2-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="25fd2-108">はじめに</span><span class="sxs-lookup"><span data-stu-id="25fd2-108">Before you begin</span></span>

<span data-ttu-id="25fd2-109">開始するには、基本的に実行中の [個人用] タブが必要です。</span><span class="sxs-lookup"><span data-stu-id="25fd2-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="25fd2-110">まだお持ちでない場合は、「 [最初の Teams アプリを構築して実行](../build-your-first-app/build-and-run.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="25fd2-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="25fd2-111">自分の割り当て</span><span class="sxs-lookup"><span data-stu-id="25fd2-111">Your assignment</span></span>

<span data-ttu-id="25fd2-112">組織内のユーザーが重要な機能 (ヘルプデスク、人事など) に関する基本的な連絡先情報を見つける際にトラブルが発生しています。</span><span class="sxs-lookup"><span data-stu-id="25fd2-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="25fd2-113">この情報を1か所ですばやく見つけることができるようにしています。</span><span class="sxs-lookup"><span data-stu-id="25fd2-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="25fd2-114">その方法</span><span class="sxs-lookup"><span data-stu-id="25fd2-114">How would you do that?</span></span> <span data-ttu-id="25fd2-115">Teams の [個人] タブ。もちろん。</span><span class="sxs-lookup"><span data-stu-id="25fd2-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="25fd2-116">学習内容</span><span class="sxs-lookup"><span data-stu-id="25fd2-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="25fd2-117">個人用タブに関連するアプリマニフェストのプロパティとスキャフォールディングの一部を特定する</span><span class="sxs-lookup"><span data-stu-id="25fd2-117">Identify some of the app manifest properties and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="25fd2-118">タブのコンテンツを作成する</span><span class="sxs-lookup"><span data-stu-id="25fd2-118">Create tab content</span></span>
> * <span data-ttu-id="25fd2-119">ユーザーの設定に基づいてタブの色のテーマを更新する</span><span class="sxs-lookup"><span data-stu-id="25fd2-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="25fd2-120">1. 関連するアプリプロジェクトコンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="25fd2-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="25fd2-121">Teams ツールキットを使用してプロジェクトを作成すると、アプリマニフェストとスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="25fd2-121">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="25fd2-122">個人タブを作成するための主なコンポーネントについて説明します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="25fd2-123">アプリマニフェスト</span><span class="sxs-lookup"><span data-stu-id="25fd2-123">App manifest</span></span>

<span data-ttu-id="25fd2-124">アプリマニフェスト (プロジェクトのディレクトリ内のファイル) にある次のスニペットが表示されます `manifest.json` `.publish` 。これには [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) 、個人用タブに関連するプロパティと既定値が含まれています。</span><span class="sxs-lookup"><span data-stu-id="25fd2-124">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows [`staticTabs`](../resources/schema/manifest-schema.md#statictabs), which includes properties and default values relevant to personal tabs.</span></span>

```JSON
"staticTabs": [
    {
        "entityId": "index",
        "name": "Personal Tab",
        "contentUrl": "{baseUrl0}/tab",
        "scopes": [ "personal" ]
    }
],
```

* <span data-ttu-id="25fd2-125">`entityId`: タブによって表示されるページの一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="25fd2-125">`entityId`: A unique identifier for the page displayed by the tab.</span></span>
* <span data-ttu-id="25fd2-126">`name`: タブの表示名 (たとえば、"個人用連絡先")。</span><span class="sxs-lookup"><span data-stu-id="25fd2-126">`name`: The tab's display name (for example, "My Contacts").</span></span>
* <span data-ttu-id="25fd2-127">`contentUrl`: タブのコンテンツページのホスト URL (HTTPS である必要があります)。</span><span class="sxs-lookup"><span data-stu-id="25fd2-127">`contentUrl`: The host URL the tab content page (must be HTTPS).</span></span>
* <span data-ttu-id="25fd2-128">`scopes`: タブは個人使用のみを対象として指定します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-128">`scopes`: Specifies the tab is for personal use only.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="25fd2-129">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="25fd2-129">App scaffolding</span></span>

<span data-ttu-id="25fd2-130">アプリのスキャフォールディングには、Teams のタブをレンダリングするためのコンポーネントが用意されています。</span><span class="sxs-lookup"><span data-stu-id="25fd2-130">The app scaffolding provides the components for rendering your tab in Teams.</span></span> <span data-ttu-id="25fd2-131">多くの作業を行うことができますが、現時点では、次の点を重視するだけで十分です。</span><span class="sxs-lookup"><span data-stu-id="25fd2-131">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="25fd2-132">`Tab.js``src/components`プロジェクトのディレクトリ内のファイル</span><span class="sxs-lookup"><span data-stu-id="25fd2-132">`Tab.js` file in the `src/components` directory of your project</span></span>
* <span data-ttu-id="25fd2-133">Microsoft Teams JavaScript クライアント SDK (プロジェクトのフロントエンドコンポーネントに事前に読み込まれているもの)</span><span class="sxs-lookup"><span data-stu-id="25fd2-133">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="25fd2-134">2. タブのコンテンツページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="25fd2-134">2. Customize your tab content page</span></span>

<span data-ttu-id="25fd2-135">組織内の重要な連絡先の一覧をコンパイルします。</span><span class="sxs-lookup"><span data-stu-id="25fd2-135">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="25fd2-136">次のスニペットをコピーして、自分に関連する情報で更新するか、または時間のためにコードをそのものとして使用します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-136">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="25fd2-137">ディレクトリに移動 `src/components` し、を開き `Tab.js` ます。</span><span class="sxs-lookup"><span data-stu-id="25fd2-137">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="25fd2-138">関数を検索し、その `render()` 中にコンテンツを貼り付け `return()` ます (図を参照)。</span><span class="sxs-lookup"><span data-stu-id="25fd2-138">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="25fd2-139">`App.css`どのテーマが使用されていても、電子メールリンクが読みやすくなるように、次のルールを追加します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-139">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="25fd2-140">変更内容を保存します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-140">Save your changes.</span></span> <span data-ttu-id="25fd2-141">Teams のアプリのタブに移動して、新しいコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-141">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="静的コンテンツを含む個人用タブのスクリーンショット。":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="25fd2-143">3. タブテーマを更新する</span><span class="sxs-lookup"><span data-stu-id="25fd2-143">3. Update the tab theme</span></span>

<span data-ttu-id="25fd2-144">優れたアプリは Teams にネイティブであるため、タブは、ユーザーが推奨する Teams のテーマ (既定値 (淡色)、濃い色、またはハイコントラスト) と融合することが重要です。</span><span class="sxs-lookup"><span data-stu-id="25fd2-144">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="25fd2-145">最後のスクリーンショットで気付いたかもしれませんが、クライアントが暗いテーマを使用している場合は、タブの背景が淡色で表示されます。</span><span class="sxs-lookup"><span data-stu-id="25fd2-145">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="25fd2-146">これは推奨されるユーザー環境ではありません。</span><span class="sxs-lookup"><span data-stu-id="25fd2-146">This is not a recommended user experience.</span></span>

<span data-ttu-id="25fd2-147">[Teams JavaScript クライアント SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)を使用すると、アプリでクライアントのテーマの変更を認識し、対応することができます。</span><span class="sxs-lookup"><span data-stu-id="25fd2-147">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="25fd2-148">これを実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-148">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="25fd2-149">Teams クライアントに関するコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="25fd2-149">Get context about the Teams client</span></span>

<span data-ttu-id="25fd2-150">ファイルには `Tab.js` 、構成されている `microsoftTeams.getContext()` クライアントテーマをいくつかの詳細情報とともに提供する呼び出しがあり [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) ます。</span><span class="sxs-lookup"><span data-stu-id="25fd2-150">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="25fd2-151">アプリのスキャフォールディングにより、このコードをとして使用して、 `context` インターフェイスおよびそのプロパティにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="25fd2-151">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

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

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="25fd2-152">テーマ変更ハンドラーを作成する</span><span class="sxs-lookup"><span data-stu-id="25fd2-152">Create a theme change handler</span></span>

<span data-ttu-id="25fd2-153">これらの `context` プロパティを用意することで、アプリは Teams で何が起こっているのかをしっかりと理解できます。</span><span class="sxs-lookup"><span data-stu-id="25fd2-153">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="25fd2-154">しかし、アプリでは、ユーザーが選択したテーマについて、その外観が反映されているとは認識できません。</span><span class="sxs-lookup"><span data-stu-id="25fd2-154">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="25fd2-155">アプリの状態がテーマに合わせて変更されるように、ハンドラーが必要です。</span><span class="sxs-lookup"><span data-stu-id="25fd2-155">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="25fd2-156">呼び出しの直後に、次のテーマ変更ハンドラーを挿入し `microsoftTeams.getContext()` ます。</span><span class="sxs-lookup"><span data-stu-id="25fd2-156">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="25fd2-157">一致テーマのスタイル</span><span class="sxs-lookup"><span data-stu-id="25fd2-157">Match theme styles</span></span>

<span data-ttu-id="25fd2-158">テーマの変更ハンドラーは準備が整っていますが、それらの変更に応答して、タブの色を現在のテーマと揃えるコードを記述する必要があります。</span><span class="sxs-lookup"><span data-stu-id="25fd2-158">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="25fd2-159">次の例は、タブにスタイルを適用する方法の1つにすぎません。そのコードをそのまま使用するか、それを展開するか、独自のコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-159">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="25fd2-160">のテーマ変更ハンドラーによって提供される状態を格納 `isTheme` します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-160">Store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="25fd2-161">現在のテーマに基づいてタブのスタイルをレンダリングするための条件付きロジックを指定します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-161">Provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="25fd2-162">次の例は、1) 現在のテーマをチェックし、2) 現在の `isTheme` `newTheme` テーマに関連する css プロパティを使用してオブジェクトを作成し、その css をタブコンテンツのルート HTML 要素 () に適用する基本的な方法を示して `<div>` います。</span><span class="sxs-lookup"><span data-stu-id="25fd2-162">The following example shows a basic way to do this by 1) checking the current theme in `isTheme`, 2) creating a `newTheme` object with CSS properties relevant to the current theme, and 3) applying the CSS to your tab content's root HTML element (`<div>`).</span></span>

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

<span data-ttu-id="25fd2-163">Teams のタブを確認します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-163">Check your tab in Teams.</span></span> <span data-ttu-id="25fd2-164">外観は、暗いテーマに密接に一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="25fd2-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="静的コンテンツを含む個人用タブのスクリーンショット。":::

## <a name="well-done"></a><span data-ttu-id="25fd2-166">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="25fd2-166">Well done</span></span>

<span data-ttu-id="25fd2-167">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="25fd2-167">Congratulations!</span></span> <span data-ttu-id="25fd2-168">Teams アプリに [個人用] タブがあり、組織内で重要な連絡先を簡単に見つけられるようになりました。</span><span class="sxs-lookup"><span data-stu-id="25fd2-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="25fd2-169">詳細情報</span><span class="sxs-lookup"><span data-stu-id="25fd2-169">Learn more</span></span>

* <span data-ttu-id="25fd2-170">[認証タブのユーザーに SSO を使用](../tabs/how-to/authentication/auth-aad-sso.md)する: 承認されたユーザーのみにタブを表示する場合は、Azure Active DIRECTORY (AD) を使用してシングルサインオン (SSO) を設定します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-170">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="25fd2-171">[既存の web アプリまたは web ページからコンテンツを埋め込む](../tabs/how-to/add-tab.md#tab-requirements): [個人用] タブの新しいコンテンツを作成する方法を示しましたが、外部 URL からコンテンツを読み込むこともできます。</span><span class="sxs-lookup"><span data-stu-id="25fd2-171">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="25fd2-172">[タブに対してシームレスな環境を作成する](../tabs/design/tabs.md): Teams タブの設計に関する推奨ガイドラインを参照してください。</span><span class="sxs-lookup"><span data-stu-id="25fd2-172">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="25fd2-173">[モバイル用のタブの作成](../tabs/design/tabs-mobile.md): 電話とタブレットのタブを開発する方法について理解します。</span><span class="sxs-lookup"><span data-stu-id="25fd2-173">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="25fd2-174">Microsoft Graph API との統合</span><span class="sxs-lookup"><span data-stu-id="25fd2-174">Integrate with the Microsoft Graph API</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="25fd2-175">ツールキットなしでタブを作成する</span><span class="sxs-lookup"><span data-stu-id="25fd2-175">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="25fd2-176">次のレッスン</span><span class="sxs-lookup"><span data-stu-id="25fd2-176">Next lesson</span></span>

<span data-ttu-id="25fd2-177">個人用のタブを作成する方法を理解していること。</span><span class="sxs-lookup"><span data-stu-id="25fd2-177">You know how to build a tab for personal use.</span></span> <span data-ttu-id="25fd2-178">チームチャネルとチャットのタブを構築するために必要な作業を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="25fd2-178">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="25fd2-179">チャネルのタブを作成する</span><span class="sxs-lookup"><span data-stu-id="25fd2-179">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
