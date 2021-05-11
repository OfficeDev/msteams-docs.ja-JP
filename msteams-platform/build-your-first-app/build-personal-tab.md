---
title: '[スタート] - [個人用] タブを作成する'
author: girliemac
description: ユーザー設定を使用してMicrosoft Teams個人用タブをすばやく作成Microsoft Teams Toolkit。
ms.author: timura
ms.date: 03/16/2020
ms.topic: tutorial
ms.openlocfilehash: 05ef9913e338a54c7e6ebc301825b27d4bec9705
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068586"
---
# <a name="build-a-basic-personal-tab-for-microsoft-teams"></a><span data-ttu-id="e49a3-103">ユーザーの基本的な個人用タブをMicrosoft Teams</span><span class="sxs-lookup"><span data-stu-id="e49a3-103">Build a basic personal tab for Microsoft Teams</span></span>

<span data-ttu-id="e49a3-104">このチュートリアルでは、ユーザー設定で基本的な個人用タブを作成Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="e49a3-104">This tutorial teaches you to build a basic personal tab in Microsoft Teams.</span></span> <span data-ttu-id="e49a3-105">タブは、Web コンテンツをホストしてアプリ内の情報を表示する簡単なTeams。</span><span class="sxs-lookup"><span data-stu-id="e49a3-105">Tabs are a simple way to surface information in your app by hosting web content in Teams.</span></span> <span data-ttu-id="e49a3-106">タブは、個々のユーザーにプライベート ワークスペースを提供する個人用アプリの一般的な機能です。</span><span class="sxs-lookup"><span data-stu-id="e49a3-106">Tabs are a common feature of personal apps that provide a private workspace for individual users.</span></span> <span data-ttu-id="e49a3-107">個人用タブは、従来の Web エクスペリエンスに最も近Teams。</span><span class="sxs-lookup"><span data-stu-id="e49a3-107">Personal tabs are the closest thing to a traditional web experience in Teams.</span></span> 

## <a name="what-youll-learn"></a><span data-ttu-id="e49a3-108">学習する情報</span><span class="sxs-lookup"><span data-stu-id="e49a3-108">What you'll learn</span></span>

* <span data-ttu-id="e49a3-109">個人用タブに関連するアプリの構成とスキャフォールディングについて理解します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-109">Understand the app configurations and scaffolding relevant to personal tabs.</span></span>
* <span data-ttu-id="e49a3-110">組織の連絡先リストを含むタブ コンテンツを作成します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-110">Create a tab content with a contact list of your organization.</span></span>
* <span data-ttu-id="e49a3-111">ユーザー設定に基づいてタブのカラー テーマを更新します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-111">Update a tab's color theme based on user preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e49a3-112">前提条件</span><span class="sxs-lookup"><span data-stu-id="e49a3-112">Prerequisites</span></span>

<span data-ttu-id="e49a3-113">簡単なアプリをセットアップして構築する方法を理解Teamsしてください。</span><span class="sxs-lookup"><span data-stu-id="e49a3-113">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="e49a3-114">詳細については[、「Hello, World!」アプリMicrosoft Teamsを作成するを参照してください](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="e49a3-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-understand-your-app-project-components"></a><span data-ttu-id="e49a3-115">1. アプリ プロジェクト コンポーネントを理解する</span><span class="sxs-lookup"><span data-stu-id="e49a3-115">1. Understand your app project components</span></span>

<span data-ttu-id="e49a3-116">基本的な個人用タブを作成した後、生成されたアプリスキャフォールディングは、ユーザー設定で個人用タブをレンダリングするTeams。</span><span class="sxs-lookup"><span data-stu-id="e49a3-116">After you have created a basic personal tab, the generated app scaffold provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="e49a3-117">多くの作業が可能ですが、ここでは次の作業に重点を置いてください。</span><span class="sxs-lookup"><span data-stu-id="e49a3-117">There's a lot you can work with, but for now let us focus on the following:</span></span> 

* <span data-ttu-id="e49a3-118">`Tab.js` ファイルをプロジェクト `src/components` のディレクトリに保存します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-118">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="e49a3-119">これは、タブ コンテンツ ページのレンダリング用です。</span><span class="sxs-lookup"><span data-stu-id="e49a3-119">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="e49a3-120">Microsoft Teamsプロジェクトのフロントエンド コンポーネントに事前に読み込まれている JavaScript クライアント SDK。</span><span class="sxs-lookup"><span data-stu-id="e49a3-120">Microsoft Teams JavaScript client SDK, which is pre-loaded in your project's front-end components.</span></span>

<span data-ttu-id="e49a3-121">ファイルの上部にあるセクションから分かるために、サンプル コードでは、ユーザー インターフェイスを構築するためにReact JavaScript ライブラリである `import` `Tabs.js` React を使用します。 [](https://reactjs.org/)</span><span class="sxs-lookup"><span data-stu-id="e49a3-121">As you may notice from the `import` section at the top of `Tabs.js` file, the sample code uses [React](https://reactjs.org/), an open-source JavaScript library for building user-interface.</span></span> 

> [!NOTE]
> <span data-ttu-id="e49a3-122">このチュートリアルではReactを使用する必要はTeamsですが、このチュートリアルでは、次の方法についてReact。</span><span class="sxs-lookup"><span data-stu-id="e49a3-122">Although using React is _not_ required for Teams development, this tutorial teaches you with React.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="e49a3-123">2. タブ コンテンツ ページをカスタマイズする</span><span class="sxs-lookup"><span data-stu-id="e49a3-123">2. Customize your tab content page</span></span>

<span data-ttu-id="e49a3-124">タブ コンテンツ ページをカスタマイズして、組織内の重要な連絡先のリストを表示できます。</span><span class="sxs-lookup"><span data-stu-id="e49a3-124">You can customize your tab content page to render a list of important contacts in your organization.</span></span> 

<span data-ttu-id="e49a3-125">**タブ コンテンツ ページをカスタマイズするには**</span><span class="sxs-lookup"><span data-stu-id="e49a3-125">**To customize your tab content page**</span></span>

1. <span data-ttu-id="e49a3-126">関連する情報を使用して、次のコード サンプルをコピーして変更します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-126">Copy and modify the following code sample with information that's relevant to you.</span></span> <span data-ttu-id="e49a3-127">コードは次のように使用できます。</span><span class="sxs-lookup"><span data-stu-id="e49a3-127">You can also use the code as is:</span></span> 
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
1. <span data-ttu-id="e49a3-128">ディレクトリに移動 `src/components` し、ファイルを開 `Tab.js` きます。</span><span class="sxs-lookup"><span data-stu-id="e49a3-128">Got to the `src/components` directory and open the `Tab.js` file.</span></span> 
1. <span data-ttu-id="e49a3-129">次の例に示すように、テンプレート コードに移動して、内部の変更 `render()` `return()` されたコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e49a3-129">Go to `render()` and replace the template code with the modified code inside `return()` as shown in the following example:</span></span>
    ```JavaScript
    render() {
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
1. <span data-ttu-id="e49a3-130">ディレクトリに移動し、次のコードを使用してファイルを変更して、使用されているテーマで電子メール リンクを読みやすく `src/components` `App.css` します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-130">Go to the `src/components` directory and modify the `App.css` file with the following code to make the email links easier to read with any theme that is used:</span></span>
    ```CSS
    a {
      color: inherit;
    }
    ```
1. <span data-ttu-id="e49a3-131">変更内容を保存します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-131">Save your changes.</span></span> 

   <span data-ttu-id="e49a3-132">アプリのタブで新しいコンテンツを表示できます。Teams。</span><span class="sxs-lookup"><span data-stu-id="e49a3-132">You can view the new content in your app's tab in Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-content.png" alt-text="静的コンテンツを含む個人用タブのスクリーンショット。":::

## <a name="3-update-your-tab-theme"></a><span data-ttu-id="e49a3-134">3. タブテーマを更新する</span><span class="sxs-lookup"><span data-stu-id="e49a3-134">3. Update your tab theme</span></span>

<span data-ttu-id="e49a3-135">タブには、ネイティブなテーマを設定することが重要Teams。</span><span class="sxs-lookup"><span data-stu-id="e49a3-135">It is important for your tab to have a theme that feels native to Teams.</span></span> <span data-ttu-id="e49a3-136">タブとテーマをブレンドTeamsがあります。</span><span class="sxs-lookup"><span data-stu-id="e49a3-136">You must blend your tab with the Teams theme.</span></span> <span data-ttu-id="e49a3-137">通常、ユーザーは既定 (明るいテーマ、濃色テーマ、ハイ コントラスト テーマ) を好む。</span><span class="sxs-lookup"><span data-stu-id="e49a3-137">Your users generally prefer default (light), dark, or high contrast themes.</span></span> <span data-ttu-id="e49a3-138">前回のスクリーンショットで確認した場合と同様に、ユーザーが暗いテーマを使用している場合、タブには明るい背景が残ります。</span><span class="sxs-lookup"><span data-stu-id="e49a3-138">As you might have noticed in the last screenshot, your tab still has a light background when your user is using the dark theme.</span></span> <span data-ttu-id="e49a3-139">これは推奨されるユーザー エクスペリエンスではありません。</span><span class="sxs-lookup"><span data-stu-id="e49a3-139">This is not a recommended user experience.</span></span>

<span data-ttu-id="e49a3-140">JavaScript Teams SDK を使用すると、アプリを認識し、クライアントのテーマの変更に対応できます。</span><span class="sxs-lookup"><span data-stu-id="e49a3-140">The Teams JavaScript client SDK can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="e49a3-141">これを行うには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-141">To do this, follow these steps:</span></span>

1. <span data-ttu-id="e49a3-142">**構成済みのクライアント テーマに関するTeams取得する** ファイル `microsoftTeams.getContext()` 内の呼び出しは、構成済みのクライアント テーマ (暗いテーマなど) に関するコンテキスト `Tab.js` を提供します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-142">**Get context about the configured Teams client theme** The `microsoftTeams.getContext()` call in your `Tab.js` file, provides some context about the configured client theme (such as dark theme).</span></span> <span data-ttu-id="e49a3-143">次のコードは、インターフェイスとその `context` プロパティにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="e49a3-143">The following code accesses the `context` interface and its properties:</span></span>

    ```JavaScript
    componentDidMount(){
      // Get the user context from Teams and set it in the state
      microsoftTeams.getContext((context, error) => {
        this.setState({
          context: context,
          theme: context.theme
        });
      });
    }
    ```
1. <span data-ttu-id="e49a3-144">**テーマ変更ハンドラーを作成する** プロパティを手にして、アプリはアプリの周囲で何が起こっているかを `context` Teams。</span><span class="sxs-lookup"><span data-stu-id="e49a3-144">**Create a theme change handler** With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="e49a3-145">ただし、アプリは、ユーザーがテーマを更新しても、テーマを反映した外観を持つわけではありません。</span><span class="sxs-lookup"><span data-stu-id="e49a3-145">However, the app still doesn't have an appearance reflecting the theme when a user updates it.</span></span>

   <span data-ttu-id="e49a3-146">テーマを使用してアプリの状態を更新するハンドラーが必要です。</span><span class="sxs-lookup"><span data-stu-id="e49a3-146">You need a handler to update your app's state with the theme.</span></span> <span data-ttu-id="e49a3-147">ハンドラーを作成するには、呼び出しの直後に次のテーマ変更ハンドラーを挿入 `microsoftTeams.getContext()` します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-147">To create a handler, insert the following theme change handler immediately after the `microsoftTeams.getContext()` call:</span></span>

    ```JavaScript
    microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.context.theme) {
    this.setState({
      context: {
      ...this.state.context,
      theme
      }
      })   
      }
    });
      ```
1. <span data-ttu-id="e49a3-148">**テーマのスタイルに一致する** ただし、テーマ変更ハンドラーは配置されています。ただし、変更に応答し、タブの色を現在のテーマに合わせて配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e49a3-148">**Match the theme styles** Your theme change handler is in place, however, you still have to respond to changes and align your tab's colors with the current theme.</span></span>

   <span data-ttu-id="e49a3-149">関数で `render()` 、テーマ変更ハンドラーによって提供される状態を次に格納します `isTheme` 。</span><span class="sxs-lookup"><span data-stu-id="e49a3-149">In the `render()` function, store the state provided by the theme change handler in `isTheme`:</span></span>

    ```JavaScript
      const isTheme = this.state.context.theme
    ```
    
    > [!NOTE]
    > <span data-ttu-id="e49a3-150">この例は、タブにスタイルを適用する方法の 1 つです。コードを現在の方法で使用するか、展開するか、独自のコードを作成します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-150">This example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

    <span data-ttu-id="e49a3-151">テーマ変更ハンドラーによって提供される状態を格納した後、現在のテーマに基づいてタブのスタイルをレンダリングするための条件付きロジックを提供します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-151">After storing the state provided by the theme change handler, provide the conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="e49a3-152">次の例は、これを行う基本的な方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="e49a3-152">The following example shows a basic way to do this:</span></span>

    1. <span data-ttu-id="e49a3-153">に移動 `render()` して、現在のテーマを確認します `isTheme` 。</span><span class="sxs-lookup"><span data-stu-id="e49a3-153">Go to `render()` and check the current theme in `isTheme`.</span></span>
    1. <span data-ttu-id="e49a3-154">現在の `newTheme` テーマに関連する CSS プロパティを持つオブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="e49a3-154">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
    1. <span data-ttu-id="e49a3-155">タブ コンテンツのルート HTML 要素 ( ) に次の CSS を適用します `<div style={newTheme}>` 。</span><span class="sxs-lookup"><span data-stu-id="e49a3-155">Apply the following CSS to your tab content's root HTML element (`<div style={newTheme}>`):</span></span>

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

       <span data-ttu-id="e49a3-156">[ページ] でタブTeams。</span><span class="sxs-lookup"><span data-stu-id="e49a3-156">Check your tab in Teams.</span></span> <span data-ttu-id="e49a3-157">外観が暗いテーマと密接に一致する。</span><span class="sxs-lookup"><span data-stu-id="e49a3-157">The appearance now closely matches the dark theme.</span></span>

       :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-updated-theme.png" alt-text="静的コンテンツ ビューを含む個人用タブのスクリーンショット。":::

## <a name="see-also"></a><span data-ttu-id="e49a3-159">関連項目</span><span class="sxs-lookup"><span data-stu-id="e49a3-159">See also</span></span>

* [<span data-ttu-id="e49a3-160">Teams JavaScript client SDK</span><span class="sxs-lookup"><span data-stu-id="e49a3-160">Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="e49a3-161">デスクトップと Web のタブMicrosoft Teamsデザインする</span><span class="sxs-lookup"><span data-stu-id="e49a3-161">Designing your tab for Microsoft Teams desktop and web</span></span>](../tabs/design/tabs.md) 
* [<span data-ttu-id="e49a3-162">コンテキスト インターフェイス</span><span class="sxs-lookup"><span data-stu-id="e49a3-162">Context interface</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="e49a3-163">UI テンプレートをMicrosoft Teamsアプリを設計する</span><span class="sxs-lookup"><span data-stu-id="e49a3-163">Designing your Microsoft Teams app with UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="e49a3-164">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="e49a3-164">Tabs on mobile</span></span>](../tabs/design/tabs-mobile.md)
* [<span data-ttu-id="e49a3-165">タブのシングル サインオン (SSO) のサポート</span><span class="sxs-lookup"><span data-stu-id="e49a3-165">Single sign-on (SSO) support for tabs</span></span>](../tabs/how-to/authentication/auth-aad-sso.md)
* [<span data-ttu-id="e49a3-166">Microsoft Teams API の概要</span><span class="sxs-lookup"><span data-stu-id="e49a3-166">Microsoft Teams API overview</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="e49a3-167">カスタム個人用タブを作成し、Node.jsの Yeoman Generator を使用Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e49a3-167">Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a><span data-ttu-id="e49a3-168">次の手順</span><span class="sxs-lookup"><span data-stu-id="e49a3-168">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e49a3-169">チャネルのタブを作成する</span><span class="sxs-lookup"><span data-stu-id="e49a3-169">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)