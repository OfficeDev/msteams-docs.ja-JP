---
title: '[開始] - [個人用] タブの作成'
author: heath-hamilton
description: Microsoft Teams を使用して、Microsoft Teams の個人用タブをすばやく作成Toolkit。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: 17263303207ffb5bee333f1ec0e655096b1062ee
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911913"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a>Microsoft Teams の個人用タブを作成する

タブは、基本的に Teams に Web ページを埋め込み、アプリにコンテンツを表示する簡単な方法です。

Teams には 2 種類のタブがあります。 このチュートリアルでは、個人の基本的なタブ、個々のユーザー用の全画面コンテンツ ページを作成します。 (個人用タブは、Teams での従来の Web サイト エクスペリエンスに最も近いものです)。

## <a name="before-you-begin"></a>はじめに

開始するには、基本的な個人用タブが必要です。 If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).

## <a name="your-assignment"></a>割り当て

組織内のユーザーは、重要な機能 (ヘルプ デスク、人事など) の基本的な連絡先情報を見つけるのに問題があります。 この情報を 1 か所ですばやく見つけ出す必要があります。 これをどのように行いますか? もちろん、Teams の個人用タブ。

## <a name="what-youll-learn"></a>学習する情報

> [!div class="checklist"]
>
> * アプリ構成の一部を特定し、個人用タブに関連するスキャフォールディングを行う
> * タブ コンテンツを作成する
> * ユーザー設定に基づいてタブの配色テーマを更新する

## <a name="1-identify-relevant-app-project-components"></a>1. 関連するアプリ プロジェクト コンポーネントを特定する

アプリの構成とスキャフォールディングの多くが、Teams アプリを使用してプロジェクトを作成するときに自動的に設定Toolkit。 個人用タブを作成する主なコンポーネントを見てみしましょう。

### <a name="app-configurations"></a>アプリの構成

ツールキットで **、App Studio に移動して** 、アプリの構成を表示および更新します。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングは、Teams で個人用タブをレンダリングするコンポーネントを提供します。 作業できる作業は多くあるのですが、今のところは次の作業にのみ重点を置く必要があります。

* `Tab.js` ファイルを `src/components` プロジェクトのディレクトリに保存します。 これは、タブ コンテンツ ページをレンダリングする場合に使用します。
* Microsoft Teams JavaScript クライアント SDK。プロジェクトのフロントエンド コンポーネントに事前に読み込まれます。

## <a name="2-customize-your-tab-content-page"></a>2. タブ コンテンツ ページをカスタマイズする

組織内の重要な連絡先の一覧をコンパイルします。 次のスニペットを、自分に関連する情報でコピーして更新するか、時間を取り合い、コードを使用します。

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

ディレクトリに移動 `src/components` して開きます `Tab.js` 。 関数を見 `render()` つけて、コンテンツを内部 `return()` に貼り付けます (図を参照)。

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

次のルールを追加して、使用するテーマに関係なく電子メール リンクを読 `App.css` みやすくします。

```CSS
a {
  color: inherit;
}
```

変更内容を保存します。 Teams のアプリのタブに移動して、新しいコンテンツを表示します。

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="静的コンテンツを含む [個人] タブのスクリーンショット。":::

## <a name="3-update-the-tab-theme"></a>3. タブ テーマを更新する

優れたアプリは Teams にネイティブだと感じるので、ユーザーが優先する Teams テーマ (既定 (明るい)、暗い、ハイ コントラスト) とタブをブレンドすることが重要です。 前のスクリーンショットでお気付きのように、クライアントが濃色テーマを使用している場合でも、タブの背景は明るい色になります。 これは推奨されるユーザー エクスペリエンスではありません。

[Teams JavaScript クライアント SDK を使用](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)すると、アプリがクライアントのテーマの変更を認識して対応できます。 これを行う方法を見てみしましょう。

### <a name="get-context-about-the-teams-client"></a>Teams クライアントに関するコンテキストを取得する

ファイルには、構成済みのクライアント テーマに関する情報を提供する呼び出し `Tab.js` `microsoftTeams.getContext()` [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) があります。 アプリのスキャフォールディングにより、このコードを使用してインターフェイスとそのプロパティ `context` にアクセスします。

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

### <a name="create-a-theme-change-handler"></a>テーマ変更ハンドラーを作成する

プロパティを利用すると、アプリは Teams で何が起こっているかをしっかりと `context` 理解できます。 ただし、アプリは、ユーザーが選択したテーマを反映する必要がある外観をまだ知りません。

テーマによってアプリの状態が変化するハンドラーが必要です。 呼び出しの直後に、次のテーマ変更ハンドラーを挿入 `microsoftTeams.getContext()` します。

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a>一致するテーマのスタイル

テーマ変更ハンドラーは配置されますが、これらの変更に応答し、タブの色を現在のテーマに合わせて調整するコードが必要です。

> [!NOTE]
> 次の例は、タブにスタイルを適用する方法の 1 つを示しています。コードは、この方法で使用するか、展開するか、独自のコードを記述します。

この関数 `render()` では、テーマ変更ハンドラーによって提供される状態を格納します `isTheme` 。

```JavaScript
  const isTheme = this.state.theme
```

テーマ変更ハンドラーによって提供される状態を格納した後、現在のテーマに基づいてタブのスタイルをレンダリングするための条件ロジックを提供します。 次の例は、これを行う基本的な方法を示しています。
1. で現在のテーマを確認します `isTheme` 。
2. 現在の `newTheme` テーマに関連する CSS プロパティを持つオブジェクトを作成します。
3. CSS をタブ コンテンツのルート HTML 要素 ( ) に適用します `<div>` 。

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

Teams でタブを確認します。 外観は濃色テーマと密接に一致している必要があります。

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="静的コンテンツ ビューを含む [個人用] タブのスクリーンショット。":::

## <a name="well-done"></a>よくやりましたね

おめでとうございます! 組織の重要な連絡先を簡単に検索できる個人用タブを含む Teams アプリがあります。

## <a name="learn-more"></a>詳細情報

* 設計ガイドライン [に従い](../tabs/design/tabs.md) 、実稼働対応 [の UI](../concepts/design/design-teams-app-ui-templates.md) テンプレートを使用してビルドし、シームレスなエクスペリエンスを作成します。
* タブ [のモバイルに関する考慮事項](../tabs/design/tabs-mobile.md) について説明します。
* [SSO 認証をタブに追加します](../tabs/how-to/authentication/auth-aad-sso.md)。
* Microsoft Graph で Teams データ [を利用します](https://docs.microsoft.com/graph/teams-concept-overview)。
* [ツールキットを使わずにタブを作成します](../tabs/quickstarts/create-personal-tab-node-yeoman.md)。

## <a name="next-lesson"></a>次のレッスン

個人用のタブを作成する方法を知っている。 チーム チャネルとチャットのタブを作成するために必要なことを見てみしましょう。

> [!div class="nextstepaction"]
> [チャネルのタブを作成する](../build-your-first-app/build-channel-tab.md)
