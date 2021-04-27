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
# <a name="build-a-personal-tab-for-microsoft-teams"></a>Microsoft Teams の個人用タブを作成する

タブは、基本的に Teams に Web ページを埋め込み、アプリ内のコンテンツを表示する簡単な方法です。

Teams には 2 種類のタブがあります。 このチュートリアルでは、基本的な個人用タブ 、個々のユーザーのフルスクリーン コンテンツ ページを作成します。 (個人用タブは、Teams の従来の Web サイト エクスペリエンスに最も近いものです)。

## <a name="before-you-begin"></a>はじめに

開始するには、基本的な個人用タブが必要です。 まだインストールされていない場合は、「ビルドして最初の [Teams アプリを実行する」を参照してください](../build-your-first-app/build-and-run.md)。

## <a name="your-assignment"></a>割り当て

組織内のユーザーは、重要な機能 (ヘルプ デスク、人事など) の基本的な連絡先情報を見つけるのに問題があります。 この情報をすばやく 1 か所で見つけ出す必要があります。 どのように行いますか? もちろん、Teams の個人用タブ。

## <a name="what-youll-learn"></a>学習する情報

> [!div class="checklist"]
>
> * 個人用タブに関連するアプリ構成とスキャフォールディングの一部を特定する
> * タブ コンテンツの作成
> * ユーザー設定に基づいてタブの色テーマを更新する

## <a name="1-identify-relevant-app-project-components"></a>1. 関連するアプリ プロジェクト コンポーネントを特定する

Teams を使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的にToolkit。 個人用タブを作成する主要なコンポーネントについて説明します。

### <a name="app-configurations"></a>アプリの構成

ツールキットで、App Studio に **移動して** 、アプリ構成を表示および更新します。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングは、Teams で個人用タブをレンダリングするコンポーネントを提供します。 多くの作業が可能ですが、今のところ、次の作業に集中する必要があります。

* `Tab.js` ファイルをプロジェクト `src/components` のディレクトリに保存します。 これは、タブ コンテンツ ページのレンダリング用です。
* プロジェクトのフロントエンド コンポーネントに事前に読み込まれた Microsoft Teams JavaScript クライアント SDK。

## <a name="2-customize-your-tab-content-page"></a>2. タブ コンテンツ ページをカスタマイズする

組織内の重要な連絡先の一覧をコンパイルします。 次のスニペットを、自分に関連する情報でコピーして更新するか、時間の間はコードを使用します。

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

ディレクトリに移動 `src/components` して開きます `Tab.js` 。 関数を見 `render()` つけて、コンテンツを (図のように) `return()` 内部に貼り付けます。

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

次のルールを追加して、使用するテーマに関係なく電子メール リンク `App.css` を読みやすくします。

```CSS
a {
  color: inherit;
}
```

変更内容を保存します。 Teams のアプリのタブに移動して、新しいコンテンツを表示します。

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="静的コンテンツを含む個人用タブのスクリーンショット。":::

## <a name="3-update-the-tab-theme"></a>3. タブ テーマを更新する

優れたアプリは Teams にネイティブだと感じるので、タブがユーザーが好む Teams テーマ (既定 (明るい、暗い、またはハイ コントラスト) とブレンドすることが重要です。 前回のスクリーンショットで確認した場合と同様に、クライアントが暗いテーマを使用している場合、タブの背景は明るい色で表示されます。 これは推奨されるユーザー エクスペリエンスではありません。

[Teams JavaScript クライアント SDK は](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)、アプリを認識し、クライアントのテーマの変更に対応できます。 これを行う方法を見てみよ。

### <a name="get-context-about-the-teams-client"></a>Teams クライアントに関するコンテキストを取得する

ファイルには、構成済みのクライアント テーマについて、その他の詳細を示す `Tab.js` `microsoftTeams.getContext()` 呼び [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) 出しがあります。 アプリのスキャフォールディングのおかげで、インターフェイスとそのプロパティにアクセスするには、このコード `context` を使用します。

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

プロパティを使用すると、アプリは Teams の周囲で何が起こっているのかを `context` しっかりと理解できます。 ただし、アプリは、ユーザーが選択したテーマを反映する必要がある外観をまだ知りません。

アプリの状態がテーマと一緒に変更されるハンドラーが必要です。 呼び出しの直後に、次のテーマ変更ハンドラーを挿入 `microsoftTeams.getContext()` します。

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a>テーマのスタイルを一致する

テーマ変更ハンドラーが配置されますが、これらの変更に応答し、タブの色を現在のテーマに合わせて配置するコードが必要です。

> [!NOTE]
> 次の例は、タブにスタイルを適用する方法の 1 つです。コードを現在の方法で使用するか、展開するか、独自のコードを作成します。

関数で `render()` 、テーマ変更ハンドラーによって提供される状態をに格納します `isTheme` 。

```JavaScript
  const isTheme = this.state.theme
```

テーマ変更ハンドラーによって提供される状態を格納した後、現在のテーマに基づいてタブのスタイルをレンダリングするための条件付きロジックを提供します。 次の例は、これを行う基本的な方法を示しています。
1. で現在のテーマを確認します `isTheme` 。
2. 現在の `newTheme` テーマに関連する CSS プロパティを持つオブジェクトを作成します。
3. タブ コンテンツのルート HTML 要素 () に CSS を適用します `<div style={newTheme}>` 。

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

Teams でタブを確認します。 外観は暗いテーマと密接に一致する必要があります。

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="静的コンテンツ ビューを含む個人用タブのスクリーンショット。":::

## <a name="well-done"></a>よくやりましたね

お疲れさまでした。 組織の重要な連絡先を簡単に見つけやすくする個人用タブを持つ Teams アプリがあります。

## <a name="learn-more"></a>詳細情報

* シームレスな [エクスペリエンスを作成するには、](../tabs/design/tabs.md) 設計ガイドラインに従い、実稼働対応 [の UI](../concepts/design/design-teams-app-ui-templates.md) テンプレートを使用してビルドします。
* タブ [のモバイルに関する考慮事項](../tabs/design/tabs-mobile.md) について説明します。
* [タブに SSO 認証を追加します](../tabs/how-to/authentication/auth-aad-sso.md)。
* Microsoft Graph で Teams データ [を利用する](https://docs.microsoft.com/graph/teams-concept-overview)。
* [ツールキットを使用せずにタブを作成します](../tabs/quickstarts/create-personal-tab-node-yeoman.md)。

## <a name="next-lesson"></a>次のレッスン

個人用のタブを作成する方法を知っている。 チーム チャネルとチャットのタブを作成するために必要な情報を見てみ取る。

> [!div class="nextstepaction"]
> [チャネルのタブを作成する](../build-your-first-app/build-channel-tab.md)
