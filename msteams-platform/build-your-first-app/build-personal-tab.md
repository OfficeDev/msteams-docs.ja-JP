---
title: 作業の開始-個人用タブの作成
author: heath-hamilton
description: Microsoft Teams ツールキットを使用して、Microsoft Teams の [個人] タブをすばやく作成できます。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: 89d9a2109a863402dd7641d0882c530a0c2e6f66
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409072"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a>Microsoft Teams 用の個人用タブを作成する

タブは、Teams に web ページを埋め込むことで、アプリ内にコンテンツを表示する簡単な方法です。

Teams には、2種類のタブがあります。 このチュートリアルでは、個々のユーザーのために全画面表示のコンテンツページである [個人用の基本 *] タブ* を作成します。 (個人タブは、Teams で従来の web サイトの操作に最も近いものです)。

## <a name="before-you-begin"></a>はじめに

開始するには、基本的に実行中の [個人用] タブが必要です。 まだお持ちでない場合は、「 [最初の Teams アプリを構築して実行](../build-your-first-app/build-and-run.md)する」を参照してください。

## <a name="your-assignment"></a>自分の割り当て

組織内のユーザーが重要な機能 (ヘルプデスク、人事など) に関する基本的な連絡先情報を見つける際にトラブルが発生しています。 この情報を1か所ですばやく見つけることができるようにしています。 その方法 Teams の [個人] タブ。もちろん。

## <a name="what-youll-learn"></a>学習内容

> [!div class="checklist"]
>
> * 個人用タブに関連するアプリの構成とスキャフォールディングの一部を特定する
> * タブのコンテンツを作成する
> * ユーザーの設定に基づいてタブの色のテーマを更新する

## <a name="1-identify-relevant-app-project-components"></a>1. 関連するアプリプロジェクトコンポーネントを特定する

Teams ツールキットを使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。 個人タブを作成するための主なコンポーネントについて説明します。

### <a name="app-configurations"></a>アプリの構成

アプリの構成は、ツールキットに含まれる App Studio を使用して表示および更新できます。

セットアップ時に、ツールキットは最初にタブコンテンツページを構成しました。これには、プライマリコンテンツが表示されます。 ツールキットで、[ **App Studio** ] に移動し、[ **タブ** ] を選択して構成を表示します。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングは、Teams で個人用タブを表示するためのコンポーネントを提供します。 多くの作業を行うことができますが、現時点では、次の点を重視するだけで十分です。

* `Tab.js``src/components`プロジェクトのディレクトリ内のファイル。 これは、タブのコンテンツページをレンダリングするためのものです。
* Microsoft Teams JavaScript クライアント SDK。これは、プロジェクトのフロントエンドコンポーネントに事前に読み込まれています。

## <a name="2-customize-your-tab-content-page"></a>2. タブのコンテンツページをカスタマイズする

組織内の重要な連絡先の一覧をコンパイルします。 次のスニペットをコピーして、自分に関連する情報で更新するか、または時間のためにコードをそのものとして使用します。

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

ディレクトリに移動 `src/components` し、を開き `Tab.js` ます。 関数を検索し、その `render()` 中にコンテンツを貼り付け `return()` ます (図を参照)。

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

`App.css`どのテーマが使用されていても、電子メールリンクが読みやすくなるように、次のルールを追加します。

```CSS
a {
  color: inherit;
}
```

変更内容を保存します。 Teams のアプリのタブに移動して、新しいコンテンツを表示します。

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="静的コンテンツを含む個人用タブのスクリーンショット。":::

## <a name="3-update-the-tab-theme"></a>3. タブテーマを更新する

優れたアプリは Teams にネイティブであるため、タブは、ユーザーが推奨する Teams のテーマ (既定値 (淡色)、濃い色、またはハイコントラスト) と融合することが重要です。 最後のスクリーンショットで気付いたかもしれませんが、クライアントが暗いテーマを使用している場合は、タブの背景が淡色で表示されます。 これは推奨されるユーザー環境ではありません。

[Teams JavaScript クライアント SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)を使用すると、アプリでクライアントのテーマの変更を認識し、対応することができます。 これを実行する方法について説明します。

### <a name="get-context-about-the-teams-client"></a>Teams クライアントに関するコンテキストを取得する

ファイルには `Tab.js` 、構成されている `microsoftTeams.getContext()` クライアントテーマをいくつかの詳細情報とともに提供する呼び出しがあり [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) ます。 アプリのスキャフォールディングにより、このコードをとして使用して、 `context` インターフェイスおよびそのプロパティにアクセスします。

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

これらの `context` プロパティを用意することで、アプリは Teams で何が起こっているのかをしっかりと理解できます。 しかし、アプリでは、ユーザーが選択したテーマについて、その外観が反映されているとは認識できません。

アプリの状態がテーマに合わせて変更されるように、ハンドラーが必要です。 呼び出しの直後に、次のテーマ変更ハンドラーを挿入し `microsoftTeams.getContext()` ます。

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a>一致テーマのスタイル

テーマの変更ハンドラーは準備が整っていますが、それらの変更に応答して、タブの色を現在のテーマと揃えるコードを記述する必要があります。

> [!NOTE]
> 次の例は、タブにスタイルを適用する方法の1つにすぎません。そのコードをそのまま使用するか、それを展開するか、独自のコードを記述します。

のテーマ変更ハンドラーによって提供される状態を格納 `isTheme` します。

```JavaScript
  const isTheme = this.state.theme
```

現在のテーマに基づいてタブのスタイルをレンダリングするための条件付きロジックを指定します。 次の例は、1) 現在のテーマをチェックし、2) 現在の `isTheme` `newTheme` テーマに関連する css プロパティを使用してオブジェクトを作成し、その css をタブコンテンツのルート HTML 要素 () に適用する基本的な方法を示して `<div>` います。

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

Teams のタブを確認します。 外観は、暗いテーマに密接に一致する必要があります。

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="静的コンテンツビューを含む [個人用] タブのスクリーンショット。":::

## <a name="well-done"></a>よくやりましたね

おめでとうございます! Teams アプリに [個人用] タブがあり、組織内で重要な連絡先を簡単に見つけられるようになりました。

## <a name="learn-more"></a>詳細情報

* [認証タブのユーザーに SSO を使用](../tabs/how-to/authentication/auth-aad-sso.md)する: 承認されたユーザーのみにタブを表示する場合は、Azure Active DIRECTORY (AD) を使用してシングルサインオン (SSO) を設定します。
* [既存の web アプリまたは web ページからコンテンツを埋め込む](../tabs/how-to/add-tab.md#tab-requirements): [個人用] タブの新しいコンテンツを作成する方法を示しましたが、外部 URL からコンテンツを読み込むこともできます。
* [タブに対してシームレスな環境を作成する](../tabs/design/tabs.md): Teams タブの設計に関する推奨ガイドラインを参照してください。
* [モバイル用のタブの作成](../tabs/design/tabs-mobile.md): 電話とタブレットのタブを開発する方法について理解します。
* [Microsoft Graph API で Teams データを利用する](https://docs.microsoft.com/graph/teams-concept-overview)
* [ツールキットなしでタブを作成する](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>次のレッスン

個人用のタブを作成する方法を理解していること。 チームチャネルとチャットのタブを構築するために必要な作業を見てみましょう。

> [!div class="nextstepaction"]
> [チャネルのタブを作成する](../build-your-first-app/build-channel-tab.md)
