---
title: はじめに - チャネルとグループ タブを構築する
author: girliemac
description: Microsoft Teams Toolkitを使用して、Microsoft Teamsチャネルとグループ タブをすばやく作成します。
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: ff9cfbfb7d099db52966f119add4ce8729929aa1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566069"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a>Microsoft Teamsの最初のチャンネルとグループタブを作成する

このチュートリアルでは、チーム チャネルまたはチャットの全画面表示ページである *グループ タブ* とも呼ばれる基本的な *チャネル タブ* を作成する方法について説明します。 この種類のタブの一部の要素を構成することもできます(たとえば、タブの名前を変更して、そのタブをチャネルに意味のあるものにすることもできます。

## <a name="what-youll-learn"></a>あなたが学ぶこと

* Visual Studio CodeのMicrosoft Teams Toolkitを使用してアプリ プロジェクトを作成します。
* チャンネルタブに関連するアプリの構成とスキャフォールディングについて理解する。
* タブの内容とタブ構成を作成します。
* テスト用のチームでアプリをビルドして実行します。

## <a name="prerequisites"></a>前提条件

簡単なTeams アプリを設定して構築する方法を理解していることを確認します。 詳細については、[最初のMicrosoft Teams "Hello, World!" アプリを作成する](../build-your-first-app/build-and-run.md)を参照してください。

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

このMicrosoft Teams Toolkitは、アプリを構成し、チャンネルとグループのタブに関連するスキャフォールディングを設定するのに役立ちます。 また、基本的な構成ページとコンテンツ ページが含まれています。 メッセージ。

**アプリ プロジェクトを作成するには**

1. Visual Studio Codeに移動し、 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 左側のアクティビティバーのMicrosoft Teamsを選択します。
1. Microsoft 365開発アカウントでサインインするように求められたらサインインします。
1. [**プロジェクトの選択**] 画面で、[**チャネルとグループ アプリ**] の下の **[JS** (JavaScript)] を選択します。
1. Teams アプリの名前を入力します。 

    > [!NOTE]
    > これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前でもあります。

1. [**グループ] タブまたは [チャンネル] タブTeams** 選択します。
1. 画面の下部にある **[完了] を** 選択してプロジェクトを構成し、プロジェクトをローカル コンピューターに保存します。  

## <a name="2-understand-your-app-project-components"></a>2. アプリ プロジェクト コンポーネントを理解する

ツールキットを使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。 チャネル タブを作成するための主要なコンポーネントを見てみましょう。

* **アプリの構成**: **ツールキットでアプリスタジオ** を開き、アプリの構成を表示および更新します。
* **アプリスキャフォールディング**: アプリスキャフォールディングは、Teamsでチャンネルタブをレンダリングするために必要なコンポーネントを提供します。 作業できる作業はたくさんありますが、ここでは次の点に焦点を当ててみましょう。
  * プロジェクトのディレクトリにあるファイル `src/components` :
    * `Tab.js` タブのコンテンツ ページをレンダリングします。
    * `TabConfig.js` タブの設定ページをレンダリングします。
  * Microsoft TeamsJavaScript クライアント SDK は、プロジェクトのフロントエンド コンポーネントにプリロードされます。

## <a name="3-customize-your-tab-content-page"></a>3. タブコンテンツページをカスタマイズする

1. 次のコード サンプルをコピーして、組織に関連する情報を使用して変更します。 スニペットを次のように使用することもできます。
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
    
1. ディレクトリに移動 `src/components` し、ファイルを開きます `Tab.js` 。 次の `render()` 例に示すように、関数を探して、内部にコードを貼り付けます `return()` 。
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
    
1. ディレクトリに移動 `src/components` し、 `App.css` 使用されているテーマで電子メールリンクを読みやすくするために、次のコードでファイルを更新します。
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a>4. タブ設定ページをカスタマイズする

チャンネルまたはチャットの各タブには、ユーザーがアプリを追加したときに表示される設定オプションを少なくとも 1 つ備えたモーダルの設定ページがあります。 既定では、構成ページは、タブがインストールされたときにチャネルまたはチャットに通知するかどうかをユーザーに確認します。 カスタム コンテンツを追加して、構成ページをカスタマイズできます。

カスタム コンテンツを追加するには、 `TabConfig.js` ディレクトリからファイルを開 `src/components` き、次の `return()` 例に示すように、内部のプレースホルダ コンテンツを更新します。

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
> ユーザーが初めて読むので、このページでアプリに関する簡単な情報を提供します。 タブの設定ページで一般的なカスタム構成オプションまたは [認証ワークフロー](../tabs/how-to/authentication/auth-aad-sso.md)を含めることもできます。

## <a name="5-customize-your-tab-name"></a>5. タブ名をカスタマイズする

チャンネルタブを追加すると、デフォルトでアプリ名が表示されます(たとえば、 **ファーストアプリ**)。 グループの共同作業のコンテキストで、よりわかりやすい名前を指定 **することもできます。**

1. ディレクトリに移動 `src/components` し、ファイルを開きます `TabConfig.js` 。
1. 次の `suggestedDisplayName` 例に示すように、既定で表示するタブ名を持つプロパティ `microsoftTeams.settings.setSettings` を追加します。

    ```JavaScript
        microsoftTeams.settings.setSettings({
        "contentUrl": "https://localhost:3000/tab",
        "suggestedDisplayName": "Team Contacts"
      });
      ```

## <a name="6-build-and-run-your-app"></a>6. アプリをビルドして実行する

このチュートリアルでは、アプリをローカルでビルドして実行する方法について説明します。 

1. ターミナルでアプリ プロジェクトのルート ディレクトリに移動します。
1. `npm install` を実行します。
1. `npm start` を実行します。

この情報は、 `README` ツールキットのセクションにも表示されます。
コンパイルが正常に完了 `https://localhost:3000` した後、アプリが実行 **されています。** メッセージが端末に表示されます。 

## <a name="7-sideload-your-app-in-teams"></a>7. Teamsでアプリをサイドロードする

お使いのアプリは Teams でテストする準備ができています。 これを行うには、アプリのサイドロードを許可するアカウントが必要です。 

1. **F5** キーを使用してVisual Studio CodeでTeams Web クライアントを開きます。
1. 次 `localhost` の手順に従って、アプリのコンテンツをTeamsに表示できるようにして、信頼できるものとして ( ) を追加します。

   1. **F5** キーで開いた同じブラウザー ウィンドウ (既定では Google Chrome) で新しいタブを開きます。
   1. ページ `https://localhost:3000/tab` を開いて、ページに進みます。

1. [**チームに追加**] または **[チャットに追加] を** 選択し、Teamsのモーダルからテストに使用できるチャネルまたはチャットを探します。
1. [ **タブのセットアップ ] を** 選択します。構成ページはモーダルで表示されます。

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="チャンネル タブの構成ページのスクリーンショット。":::

1. [ **保存] を** 選択してタブを構成します。次のコンテンツ ページが表示されます。

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="静的コンテンツ ビューを含むチャネル タブのスクリーンショット。":::

## <a name="see-also"></a>関連項目

* [最初の Microsoft Teams アプリを構築して実行する](../build-your-first-app/build-and-run.md) 
* [Teams JavaScript client SDK](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [デスクトップと Web Microsoft Teams用のタブの設計](../tabs/design/tabs.md) 
* [UI テンプレートを使用したMicrosoft Teams アプリの設計](../concepts/design/design-teams-app-ui-templates.md) 
* [モバイルのタブ](../tabs/design/tabs-mobile.md)
* [タブのシングル サインオン (SSO) サポート](../tabs/how-to/authentication/auth-aad-sso.md)
* [Microsoft Teams API の概要](/graph/teams-concept-overview)
* [Node.jsとヨーマンジェネレータを使用してカスタムパーソナルタブを作成Microsoft Teams](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Bot を作成する](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [メッセージングの拡張機能を作成する](../build-your-first-app/build-messaging-extension.md)
