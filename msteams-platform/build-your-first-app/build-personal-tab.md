---
title: '[スタート] - [個人用] タブを作成する'
author: girliemac
description: Microsoft Teams を使用して Microsoft Teams の個人用タブをすばやく作成Toolkit。
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
# <a name="build-a-basic-personal-tab-for-microsoft-teams"></a>Microsoft Teams の基本的な個人用タブを作成する

このチュートリアルでは、Microsoft Teams で基本的な個人用タブを作成する方法について説明します。 タブは、Teams で Web コンテンツをホストしてアプリ内の情報を表示する簡単な方法です。 タブは、個々のユーザーにプライベート ワークスペースを提供する個人用アプリの一般的な機能です。 個人用タブは、Teams の従来の Web エクスペリエンスに最も近いものです。 

## <a name="what-youll-learn"></a>学習する情報

* 個人用タブに関連するアプリの構成とスキャフォールディングについて理解します。
* 組織の連絡先リストを含むタブ コンテンツを作成します。
* ユーザー設定に基づいてタブのカラー テーマを更新します。

## <a name="prerequisites"></a>前提条件

簡単な Teams アプリをセットアップしてビルドする方法を理解してください。 詳細については、「Hello, World!」アプリの最初の Microsoft Teams の作成 [に関するページをご覧ください](../build-your-first-app/build-and-run.md)。

## <a name="1-understand-your-app-project-components"></a>1. アプリ プロジェクト コンポーネントを理解する

基本的な個人用タブを作成した後、生成されたアプリスキャフォールディングは、Teams で個人用タブをレンダリングするコンポーネントを提供します。 多くの作業が可能ですが、ここでは次の作業に重点を置いてください。 

* `Tab.js` ファイルをプロジェクト `src/components` のディレクトリに保存します。 これは、タブ コンテンツ ページのレンダリング用です。
* プロジェクトのフロントエンド コンポーネントに事前に読み込まれている Microsoft Teams JavaScript クライアント SDK。

ファイルの上部にあるセクションから分かるために、サンプル コードでは、ユーザー インターフェイスを構築するためにオープンソースの JavaScript ライブラリである `import` `Tabs.js` React を使用します。 [](https://reactjs.org/) 

> [!NOTE]
> Teams 開発では React _を使用_ する必要はありませんが、このチュートリアルでは React について説明します。

## <a name="2-customize-your-tab-content-page"></a>2. タブ コンテンツ ページをカスタマイズする

タブ コンテンツ ページをカスタマイズして、組織内の重要な連絡先のリストを表示できます。 

**タブ コンテンツ ページをカスタマイズするには**

1. 関連する情報を使用して、次のコード サンプルをコピーして変更します。 コードは次のように使用できます。 
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
1. ディレクトリに移動 `src/components` し、ファイルを開 `Tab.js` きます。 
1. 次の例に示すように、テンプレート コードに移動して、内部の変更 `render()` `return()` されたコードに置き換えます。
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
1. ディレクトリに移動し、次のコードを使用してファイルを変更して、使用されているテーマで電子メール リンクを読みやすく `src/components` `App.css` します。
    ```CSS
    a {
      color: inherit;
    }
    ```
1. 変更内容を保存します。 

   新しいコンテンツは、Teams のアプリのタブで表示できます。

   :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-content.png" alt-text="静的コンテンツを含む個人用タブのスクリーンショット。":::

## <a name="3-update-your-tab-theme"></a>3. タブテーマを更新する

タブに Teams のネイティブなテーマを設定することが重要です。 タブと Teams テーマをブレンドする必要があります。 通常、ユーザーは既定 (明るいテーマ、濃色テーマ、ハイ コントラスト テーマ) を好む。 前回のスクリーンショットで確認した場合と同様に、ユーザーが暗いテーマを使用している場合、タブには明るい背景が残ります。 これは推奨されるユーザー エクスペリエンスではありません。

Teams JavaScript クライアント SDK は、アプリを認識し、クライアントのテーマの変更に対応できます。 これを行うには、次の手順を実行します。

1. **構成済みの Teams クライアント テーマに関するコンテキストを取得する** ファイル `microsoftTeams.getContext()` 内の呼び出しは、構成済みのクライアント テーマ (暗いテーマなど) に関するコンテキスト `Tab.js` を提供します。 次のコードは、インターフェイスとその `context` プロパティにアクセスします。

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
1. **テーマ変更ハンドラーを作成する** プロパティを使用すると、アプリは Teams の周囲で何が起こっているのかを `context` しっかりと理解できます。 ただし、アプリは、ユーザーがテーマを更新しても、テーマを反映した外観を持つわけではありません。

   テーマを使用してアプリの状態を更新するハンドラーが必要です。 ハンドラーを作成するには、呼び出しの直後に次のテーマ変更ハンドラーを挿入 `microsoftTeams.getContext()` します。

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
1. **テーマのスタイルに一致する** ただし、テーマ変更ハンドラーは配置されています。ただし、変更に応答し、タブの色を現在のテーマに合わせて配置する必要があります。

   関数で `render()` 、テーマ変更ハンドラーによって提供される状態を次に格納します `isTheme` 。

    ```JavaScript
      const isTheme = this.state.context.theme
    ```
    
    > [!NOTE]
    > この例は、タブにスタイルを適用する方法の 1 つです。コードを現在の方法で使用するか、展開するか、独自のコードを作成します。

    テーマ変更ハンドラーによって提供される状態を格納した後、現在のテーマに基づいてタブのスタイルをレンダリングするための条件付きロジックを提供します。 次の例は、これを行う基本的な方法を示しています。

    1. に移動 `render()` して、現在のテーマを確認します `isTheme` 。
    1. 現在の `newTheme` テーマに関連する CSS プロパティを持つオブジェクトを作成します。
    1. タブ コンテンツのルート HTML 要素 ( ) に次の CSS を適用します `<div style={newTheme}>` 。

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

       Teams でタブを確認します。 外観が暗いテーマと密接に一致する。

       :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-updated-theme.png" alt-text="静的コンテンツ ビューを含む個人用タブのスクリーンショット。":::

## <a name="see-also"></a>関連項目

* [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Microsoft Teams デスクトップと Web 用のタブの設計](../tabs/design/tabs.md) 
* [コンテキスト インターフェイス](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)
* [UI テンプレートを使用した Microsoft Teams アプリの設計](../concepts/design/design-teams-app-ui-templates.md) 
* [モバイルのタブ](../tabs/design/tabs-mobile.md)
* [タブのシングル サインオン (SSO) のサポート](../tabs/how-to/authentication/auth-aad-sso.md)
* [Microsoft Teams API の概要](https://docs.microsoft.com/graph/teams-concept-overview)
* [Microsoft Teams 用のユーザー設定Node.js Yeoman Generator を使用してカスタム個人用タブを作成する](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [チャネルのタブを作成する](../build-your-first-app/build-channel-tab.md)