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
# <a name="using-the-control-library-in-app-studio"></a>アプリ Studio でコントロールライブラリを使用する

[Microsoft Teams App Studio](~/get-started/get-started-app-studio.md)には、独自のアプリで使用できる一連のコントロールが用意されています。 これらのコントロールは、App Studio の [*コントロールライブラリ*] タブに表示されます。

これらのコントロールは、独自のワークフローを合理化し、コントロールの動作とサポートチームの既定のテーマを標準化するために、Microsoft Teams の設計者によって作成されました。 このライブラリを独自のアプリで使用して、一貫性のある外観を実現できます。

次のようなコントロールがあります。

* ボタン
* ドロップ
* ックス
* ラジオボタン
* 切り替え
* テスト領域
* リンク
* タブ
* テーブル
* アイコン

## <a name="optionally-use-react-controls"></a>オプションで応答コントロールを使用する

完全な Teams コントロールライブラリでは、 [JAVASCRIPT ui フレームワークの反応](https://reactjs.org/)を使用していますが、これは、特定の ui フレームワークに縛られないようにビルドされています。 Npm パッケージには、次の4つの種類があります。

* **msteams-コア**UI コンポーネントの主要な CSS スタイル。 UI フレームワークに依存しません。
* **msteams-コア**チームの主要なアイコンのセット。
* **msteams-コンポーネント-反応**応答バインディングライブラリ。 これは、msteams-コアに依存します。
* **msteams-ui-アイコン-反応**一連の Teams アイコンの応答バインドライブラリ。 これは、msteams-ui のコアに依存します。

これらのライブラリはすべてオープンソースであり、msteams-core および msteams-ui を使用して、対応することはできません。

## <a name="adding-the-control-library"></a>コントロールライブラリの追加

コントロールライブラリとそのピアの依存関係`typestyle`をインストールします。

```terminal
npm install --save typestyle && npm install --save msteams-ui-components-react
```

*省略可能:* Teams アイコンをインストールします。

```terminal
npm install --save msteams-ui-icons-react
```

次のコード`src/App.js`を使用して、そのコンテンツを検索して置換します。

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

アプリの実行

```terminal
npm run start
```

にhttp://localhost:3000移動すると、次の画面が表示されます。

<img width="530px" src="~/assets/images/get-started/control-library-button.png" title="コントロールライブラリボタン"/>

## <a name="dynamically-handling-theme-changes"></a>テーマの変更を動的に処理する

アプリでは、次のような場合にテーマを処理する必要があります。

* タブが最初に読み込まれます。
* タブが既に読み込まれた後にユーザーがテーマを変更した

テーマはタブの[コンテキスト](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest)に含まれています。これは、タブが URL プレースホルダー値で読み込まれる前に取得できます。または、 [Microsoft Teams の JavaScript クライアント SDK](/javascript/api/%40microsoft/teams-js/context)を使用していつでも取得できます。

現在のテーマを取得する方法と、テーマの変更に対応する方法については、「 [Microsoft Teams タブのコンテキストを取得する」](~/concepts/tabs/tabs-context.md)を参照してください。

このサンプルコードは、この操作の実行方法を示しています。

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

## <a name="connect-your-own-component-to-the-teamscomponentcontext"></a>独自のコンポーネントを TeamsComponentContext に接続する

独自の CSS コードを使用する場合でも、テーマの変更に対応し、teams で定義された色を使用することができます。 TeamsComponentContext を使用すると、これを行うことができます。

もう一度、 `src/App.js`ファイルを編集して、その内容を次のコードで置き換えます。

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

このコードでは、MyComponent という新しいコンポーネントが定義されています。 その後、コントロールライブラリの "ConnectedComponent" と呼ばれる特別なコンポーネントが追加されます。 ConnectedComponent には、と`render`いう名前のプロパティがあります。これは、パラメーターとして関数を受け取ります。 レンダリング時に、この関数はタブの適切なコンテキストを使用して呼び出されます。このコンテキストには、ページがレンダリングされるテーマと、チームの色をタブに適用するために使用できるグローバルカラーオブジェクトが含まれています。`switch`ステートメントでは、テーマに基づいて適切な`<div>`が選択されています。

テーマを変更するには、ルートレベルの TeamsComponentContext を異なるテーマに渡す必要があります。 テーマを変更すると、ConnectedComponent でラップされたすべての子要素が再表示されます。 前のセクション「テーマの変更を動的に処理する」を参照してください。

コンポーネントを TeamsComponentContext に接続する方法は他にもあります。 [Redux](https://redux.js.org/basics/usage-with-react)に習熟している場合は、次のパターンを使用することをお勧めします。

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

この方法では、ConnectedComponent を使用する代わりに、connectTeamsComponent 関数を使用します。 ConnectTeamsComponent 関数は、現在のコンポーネントを取得し、コンテキストオブジェクトが挿入された新しいコンポーネントを返します。

## <a name="next-steps"></a>次のステップ

Teams App Studio に移動し、提供されているすべてのコントロールと、それらの使用方法を示すサンプルコードを確認します。 さまざまなテーマでそれらを調査することを忘れないでください。