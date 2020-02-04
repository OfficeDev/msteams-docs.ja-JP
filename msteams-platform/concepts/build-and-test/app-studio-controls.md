---
title: コントロールライブラリの使用
description: Microsoft Teams アプリ Studio によって提供されるコントロールライブラリを使用する方法
keywords: Teams App Studio コントロールライブラリ
ms.openlocfilehash: d817f55bd75216f77375b7848c5c32cbd29304c2
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674745"
---
# <a name="using-the-control-library-in-app-studio"></a><span data-ttu-id="70747-104">アプリ Studio でコントロールライブラリを使用する</span><span class="sxs-lookup"><span data-stu-id="70747-104">Using the control library in App Studio</span></span>

<span data-ttu-id="70747-105">[Microsoft Teams App Studio](~/get-started/get-started-app-studio.md)には、独自のアプリで使用できる一連のコントロールが用意されています。</span><span class="sxs-lookup"><span data-stu-id="70747-105">[Microsoft Teams App Studio](~/get-started/get-started-app-studio.md) provides you with a set of controls that you can use in your own apps.</span></span> <span data-ttu-id="70747-106">これらのコントロールは、App Studio の [*コントロールライブラリ*] タブに表示されます。</span><span class="sxs-lookup"><span data-stu-id="70747-106">These controls are provided in the *Control Library* tab of App Studio.</span></span>

<span data-ttu-id="70747-107">これらのコントロールは、独自のワークフローを合理化し、コントロールの動作とサポートチームの既定のテーマを標準化するために、Microsoft Teams の設計者によって作成されました。</span><span class="sxs-lookup"><span data-stu-id="70747-107">These controls were created by the Microsoft Teams designers to streamline their own workflows, standardize control behavior and support Team's default themes.</span></span> <span data-ttu-id="70747-108">このライブラリを独自のアプリで使用して、一貫性のある外観を実現できます。</span><span class="sxs-lookup"><span data-stu-id="70747-108">You can use this library in your own apps to achieve a unified look and feel.</span></span>

<span data-ttu-id="70747-109">次のようなコントロールがあります。</span><span class="sxs-lookup"><span data-stu-id="70747-109">Controls include:</span></span>

* <span data-ttu-id="70747-110">ボタン</span><span class="sxs-lookup"><span data-stu-id="70747-110">Buttons</span></span>
* <span data-ttu-id="70747-111">ドロップ</span><span class="sxs-lookup"><span data-stu-id="70747-111">Dropdowns</span></span>
* <span data-ttu-id="70747-112">ックス</span><span class="sxs-lookup"><span data-stu-id="70747-112">Checkboxes</span></span>
* <span data-ttu-id="70747-113">ラジオボタン</span><span class="sxs-lookup"><span data-stu-id="70747-113">Radio Buttons</span></span>
* <span data-ttu-id="70747-114">切り替え</span><span class="sxs-lookup"><span data-stu-id="70747-114">Toggles</span></span>
* <span data-ttu-id="70747-115">テスト領域</span><span class="sxs-lookup"><span data-stu-id="70747-115">Test Areas</span></span>
* <span data-ttu-id="70747-116">リンク</span><span class="sxs-lookup"><span data-stu-id="70747-116">Links</span></span>
* <span data-ttu-id="70747-117">タブ</span><span class="sxs-lookup"><span data-stu-id="70747-117">Tabs</span></span>
* <span data-ttu-id="70747-118">テーブル</span><span class="sxs-lookup"><span data-stu-id="70747-118">Tables</span></span>
* <span data-ttu-id="70747-119">アイコン</span><span class="sxs-lookup"><span data-stu-id="70747-119">Icons</span></span>

## <a name="optionally-use-react-controls"></a><span data-ttu-id="70747-120">オプションで応答コントロールを使用する</span><span class="sxs-lookup"><span data-stu-id="70747-120">Optionally use React controls</span></span>

<span data-ttu-id="70747-121">完全な Teams コントロールライブラリでは、 [JAVASCRIPT ui フレームワークの反応](https://reactjs.org/)を使用していますが、これは、特定の ui フレームワークに縛られないようにビルドされています。</span><span class="sxs-lookup"><span data-stu-id="70747-121">The full Teams control library uses the [React JavaScript UI framework](https://reactjs.org/) however it is built so that it is not tied to a specific UI framework.</span></span> <span data-ttu-id="70747-122">Npm パッケージには、次の4つの種類があります。</span><span class="sxs-lookup"><span data-stu-id="70747-122">There are four different npm packages:</span></span>

* <span data-ttu-id="70747-123">**msteams-コア**UI コンポーネントの主要な CSS スタイル。</span><span class="sxs-lookup"><span data-stu-id="70747-123">**msteams-ui-styles-core** The core CSS styles of UI components.</span></span> <span data-ttu-id="70747-124">UI フレームワークに依存しません。</span><span class="sxs-lookup"><span data-stu-id="70747-124">It’s independent of any UI framework.</span></span>
* <span data-ttu-id="70747-125">**msteams-コア**チームの主要なアイコンのセット。</span><span class="sxs-lookup"><span data-stu-id="70747-125">**msteams-ui-icons-core** The core set of Teams icons.</span></span>
* <span data-ttu-id="70747-126">**msteams-コンポーネント-反応**応答バインディングライブラリ。</span><span class="sxs-lookup"><span data-stu-id="70747-126">**msteams-ui-components-react** The React binding library.</span></span> <span data-ttu-id="70747-127">これは、msteams-コアに依存します。</span><span class="sxs-lookup"><span data-stu-id="70747-127">It depends on msteams-ui-styles-core.</span></span>
* <span data-ttu-id="70747-128">**msteams-ui-アイコン-反応**一連の Teams アイコンの応答バインドライブラリ。</span><span class="sxs-lookup"><span data-stu-id="70747-128">**msteams-ui-icons-react** The React binding library for the set of Teams icons.</span></span> <span data-ttu-id="70747-129">これは、msteams-ui のコアに依存します。</span><span class="sxs-lookup"><span data-stu-id="70747-129">It depends on msteams-ui-icons-core.</span></span>

<span data-ttu-id="70747-130">これらのライブラリはすべてオープンソースであり、msteams-core および msteams-ui を使用して、対応することはできません。</span><span class="sxs-lookup"><span data-stu-id="70747-130">These libraries are all open source, and you can use msteams-ui-styles-core and msteams-ui-icons-core without React.</span></span>

## <a name="adding-the-control-library"></a><span data-ttu-id="70747-131">コントロールライブラリの追加</span><span class="sxs-lookup"><span data-stu-id="70747-131">Adding the control library</span></span>

<span data-ttu-id="70747-132">コントロールライブラリとそのピアの依存関係`typestyle`をインストールします。</span><span class="sxs-lookup"><span data-stu-id="70747-132">Install the control library and its peer dependency `typestyle`:</span></span>

```terminal
npm install --save typestyle && npm install --save msteams-ui-components-react
```

<span data-ttu-id="70747-133">*省略可能:* Teams アイコンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="70747-133">*Optional:* Install the Teams icons.</span></span>

```terminal
npm install --save msteams-ui-icons-react
```

<span data-ttu-id="70747-134">次のコード`src/App.js`を使用して、そのコンテンツを検索して置換します。</span><span class="sxs-lookup"><span data-stu-id="70747-134">Find and open `src/App.js` and replace its content with following code:</span></span>

```javascript
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, PrimaryButton } from ‘msteams-ui-components-react’

class App extends Component {
   render() {
      // Sets up the top-level context for the library. It accepts global
      // configurations such as font size and theme. fontSize is your page’s
      // default font size. We made it a parameter so that you could use this
      // library with CSS frameworks such as Bootstrap. Some CSS frameworks
      // set the default font size for the page; retrieve it and use it
      // instead of {16} in the block.
      // This library uses the power of CSS to do most of the work for you.
      // Instead of passing themes as a parameter to every UI component,
      // we set it on a parent HTML element. All HTML elements nested within
      // that parent will inherit these properties.

      return (
        <TeamsComponentContext
            fontSize={16}
            theme={ThemeStyle.Light}
        />
      );
   }
}
export default App;
```

<span data-ttu-id="70747-135">アプリの実行</span><span class="sxs-lookup"><span data-stu-id="70747-135">Run the app</span></span>

```terminal
npm run start
```

<span data-ttu-id="70747-136">にhttp://localhost:3000移動すると、次の画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="70747-136">When you navigate to http://localhost:3000, you should see the following screen:</span></span>

<img width="530px" src="~/assets/images/get-started/control-library-button.png" title="コントロールライブラリボタン"/>

## <a name="dynamically-handling-theme-changes"></a><span data-ttu-id="70747-138">テーマの変更を動的に処理する</span><span class="sxs-lookup"><span data-stu-id="70747-138">Dynamically handling theme changes</span></span>

<span data-ttu-id="70747-139">アプリでは、次のような場合にテーマを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="70747-139">Your app needs to handle themes when:</span></span>

* <span data-ttu-id="70747-140">タブが最初に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="70747-140">The tab is initially loaded</span></span>
* <span data-ttu-id="70747-141">タブが既に読み込まれた後にユーザーがテーマを変更した</span><span class="sxs-lookup"><span data-stu-id="70747-141">A user changes the theme after the tab is already loaded</span></span>

<span data-ttu-id="70747-142">テーマはタブの[コンテキスト](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest)に含まれています。これは、タブが URL プレースホルダー値で読み込まれる前に取得できます。または、 [Microsoft Teams の JavaScript クライアント SDK](/javascript/api/%40microsoft/teams-js/context)を使用していつでも取得できます。</span><span class="sxs-lookup"><span data-stu-id="70747-142">The theme is included in a tab’s [Context](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest), which can be retrieved before the tab is loaded via URL placeholder values, or at any time by using the [Microsoft Teams JavaScript client SDK](/javascript/api/%40microsoft/teams-js/context).</span></span>

<span data-ttu-id="70747-143">現在のテーマを取得する方法と、テーマの変更に対応する方法については、「 [Microsoft Teams タブのコンテキストを取得する」](~/concepts/tabs/tabs-context.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="70747-143">How the current theme is retrieved and how to respond to theme changes is discussed here: [Get context for your Microsoft Teams tab](~/concepts/tabs/tabs-context.md).</span></span>

<span data-ttu-id="70747-144">このサンプルコードは、この操作の実行方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="70747-144">This sample code shows how this is done.</span></span>

```js
componentWillMount() {
    // If you are deploying your site as a MS Teams static or configurable tab,
    // you should add “?theme={theme}” to your tabs URL in the manifest.
    // That way you will get the current theme before it’s loaded; getContext()
    // is called only after the tab is loaded, which will cause the tab to flash
    // if the current theme is different than the default.
    this.updateTheme(this.getQueryVariable('theme'));
    this.setState({
        fontSize: this.pageFontSize(),
    });

    // If you are not using the MS Teams Javascript SDK, you can remove this entire
    // if block, but if you want theme changes in the MS Teams client to propagate
    // to the tab, leave it here.
    microsoftTeams.initialize();
    microsoftTeams.registerOnThemeChangeHandler(this.updateTheme);
}
```

## <a name="connect-your-own-component-to-the-teamscomponentcontext"></a><span data-ttu-id="70747-145">独自のコンポーネントを TeamsComponentContext に接続する</span><span class="sxs-lookup"><span data-stu-id="70747-145">Connect your own component to the TeamsComponentContext</span></span>

<span data-ttu-id="70747-146">独自の CSS コードを使用する場合でも、テーマの変更に対応し、teams で定義された色を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="70747-146">If you want to use your own CSS code you can still respond to theme changes and use colors defined by teams.</span></span> <span data-ttu-id="70747-147">TeamsComponentContext を使用すると、これを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="70747-147">TeamsComponentContext allows you to do this.</span></span>

<span data-ttu-id="70747-148">もう一度、 `src/App.js`ファイルを編集して、その内容を次のコードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="70747-148">Once again, edit your `src/App.js` file and replace its content with following code:</span></span>

```javascript
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, ConnectedComponent } from ‘msteams-ui-components-react’

class App extends Component {
    render() {
        return (
            <TeamsComponentContext
                fontSize={16}
                theme={ThemeStyle.HighContrast}>
                <MyComponent />
            </TeamsComponentContext>
        );
    }
}

class MyComponent extends Component {
    render() {
        return (
            <ConnectedComponent render={(props) => {
                const context = props.context;

                switch (context.style) {
                case ThemeStyle.Dark:
                    return <div style={{ color: context.colors.dark.brand00 }}>Dark theme!</div>;
                case ThemeStyle.HighContrast:
                    return <div style={{ color: context.colors.highContrast.black }}>High Contrast theme!</div>;
                case ThemeStyle.Light:
                    return <div style={{ color: context.colors.light.brand00 }}>Light theme!</div>;
                }
            }} />
        );
    }
}

export default App;
```

<span data-ttu-id="70747-149">このコードでは、MyComponent という新しいコンポーネントが定義されています。</span><span class="sxs-lookup"><span data-stu-id="70747-149">In this code, a new component is defined called MyComponent.</span></span> <span data-ttu-id="70747-150">その後、コントロールライブラリの "ConnectedComponent" と呼ばれる特別なコンポーネントが追加されます。</span><span class="sxs-lookup"><span data-stu-id="70747-150">Then a special component from the control library called ConnectedComponent is added.</span></span> <span data-ttu-id="70747-151">ConnectedComponent には、と`render`いう名前のプロパティがあります。これは、パラメーターとして関数を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="70747-151">ConnectedComponent has a property called `render` which takes a function as a parameter.</span></span> <span data-ttu-id="70747-152">レンダリング時に、この関数はタブの適切なコンテキストを使用して呼び出されます。このコンテキストには、ページがレンダリングされるテーマと、チームの色をタブに適用するために使用できるグローバルカラーオブジェクトが含まれています。`switch`ステートメントでは、テーマに基づいて適切な`<div>`が選択されています。</span><span class="sxs-lookup"><span data-stu-id="70747-152">At render time this function will be called with the appropriate context for your tab. The context includes the theme that the page is being rendered in as well as the global color object that you can use to apply Teams colors to your tab. As you can see in the `switch` statement, the appropriate `<div>` is chosen based on the theme.</span></span>

<span data-ttu-id="70747-153">テーマを変更するには、ルートレベルの TeamsComponentContext を異なるテーマに渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="70747-153">To change themes, we need to pass the root-level TeamsComponentContext a different theme.</span></span> <span data-ttu-id="70747-154">テーマを変更すると、ConnectedComponent でラップされたすべての子要素が再表示されます。</span><span class="sxs-lookup"><span data-stu-id="70747-154">When a theme changes, all the child elements wrapped in ConnectedComponent will be re-rendered.</span></span> <span data-ttu-id="70747-155">前のセクション「テーマの変更を動的に処理する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="70747-155">See previous section “Dynamically Handle Theme Changes.”</span></span>

<span data-ttu-id="70747-156">コンポーネントを TeamsComponentContext に接続する方法は他にもあります。</span><span class="sxs-lookup"><span data-stu-id="70747-156">There are other ways to connect your component to TeamsComponentContext.</span></span> <span data-ttu-id="70747-157">[Redux](https://redux.js.org/basics/usage-with-react)に習熟している場合は、次のパターンを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="70747-157">If you’re familiar with [Redux](https://redux.js.org/basics/usage-with-react), you may prefer the following pattern:</span></span>

```js
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, connectTeamsComponent } from ‘msteams-ui-components-react’

class App extends Component {
    render() {
        return (
            <TeamsComponentContext
                fontSize={16}
                theme={ThemeStyle.HighContrast}>
                <MyComponent />
            </TeamsComponentContext>
        );
    }
}

class MyComponentInner extends Component {
    render() {
        const context = this.props.context;
        switch (context.style) {
            case ThemeStyle.Dark:
                return <div style={{ color: context.colors.dark.brand00 }}>Dark theme!</div>;
            case ThemeStyle.HighContrast:
                return <div style={{ color: context.colors.highContrast.black }}>High Contrast theme!</div>;
            case ThemeStyle.Light:
                return <div style={{ color: context.colors.light.brand00 }}>Light theme!</div>;
        }
    }
}

const MyComponent = connectTeamsComponent(MyComponentInner);

export default App;
```

<span data-ttu-id="70747-158">この方法では、ConnectedComponent を使用する代わりに、connectTeamsComponent 関数を使用します。</span><span class="sxs-lookup"><span data-stu-id="70747-158">In this method, instead of using ConnectedComponent, you use the connectTeamsComponent function.</span></span> <span data-ttu-id="70747-159">ConnectTeamsComponent 関数は、現在のコンポーネントを取得し、コンテキストオブジェクトが挿入された新しいコンポーネントを返します。</span><span class="sxs-lookup"><span data-stu-id="70747-159">The connectTeamsComponent function takes your current component and returns a new component with the context object injected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70747-160">次のステップ</span><span class="sxs-lookup"><span data-stu-id="70747-160">Next steps</span></span>

<span data-ttu-id="70747-161">Teams App Studio に移動し、提供されているすべてのコントロールと、それらの使用方法を示すサンプルコードを確認します。</span><span class="sxs-lookup"><span data-stu-id="70747-161">Head to Teams App Studio and check out all the controls we offer and sample code of how to use them.</span></span> <span data-ttu-id="70747-162">さまざまなテーマでそれらを調査することを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="70747-162">Don’t forget to explore them in different themes.</span></span>