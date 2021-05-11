---
title: '[スタート] - [チャネルとグループ] タブを作成する'
author: girliemac
description: '[チャネルとグループ] Microsoft Teamsを使用して、チャネルとグループ タブをすばやく作成Microsoft Teams Toolkit。'
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: 868a471499bf2015196b7b741e340d070d0ed458
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068753"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a>ユーザーの最初のチャネルとグループ タブをMicrosoft Teams

このチュートリアルでは、チーム チャネルまたはチャットのフルスクリーン ページであるグループタブとも呼ばれる基本的なチャネル タブを作成する方法について説明します。 また、この種のタブのいくつかの側面を構成することもできます。たとえば、タブの名前を変更して、個人用タブでは行えないチャネルにとって意味のあるものにすることもできます。

## <a name="what-youll-learn"></a>学習する情報

* アプリプロジェクトを作成するには、アプリのMicrosoft Teams ToolkitをVisual Studio Code。
* チャネル タブに関連するアプリの構成とスキャフォールディングについて理解します。
* タブコンテンツとタブ構成を作成します。
* テスト用にチームでアプリをビルドして実行します。

## <a name="prerequisites"></a>前提条件

簡単なアプリをセットアップして構築する方法を理解Teamsしてください。 詳細については[、「Hello, World!」アプリMicrosoft Teamsを作成するを参照してください](../build-your-first-app/build-and-run.md)。

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

このMicrosoft Teams Toolkitは、アプリを構成し、チャネルタブとグループ タブに関連するスキャフォールディングを設定するのに役立ちます。 また、基本的な構成ページと、"Hello, World! メッセージ。

**アプリ プロジェクトを作成するには**

1. [アクティビティ] Visual Studio Code左側の [アクティビティ バー **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択します。
1. 開発アカウントでサインインMicrosoft 365求めるメッセージが表示されたら、そのアカウントを使用します。
1. [プロジェクトの **選択] 画面** で、[チャネルとグループ アプリ] の下の **[JS** (JavaScript)] **を選択します**。
1. Teams アプリの名前を入力します。 

    > [!NOTE]
    > これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です。

1. [**グループまたはチャネルTeams] タブを選択します**。
1. 画面 **の下部** にある [完了] を選択してプロジェクトを構成し、プロジェクトをローカル コンピューターに保存します。  

## <a name="2-understand-your-app-project-components"></a>2. アプリ プロジェクト コンポーネントについて

ツールキットを使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。 チャネル タブを作成する主要なコンポーネントを見てみ取ってみろ。

* **アプリの構成**: ツールキット **で App Studio** を開き、アプリ構成を表示および更新します。
* **アプリのスキャフォール** ディング: アプリのスキャフォールディングは、チャネル タブのレンダリングに必要なコンポーネントを提供Teams。 ただし、ここでは次の作業に重点を置き、多くの作業を行います。
  * プロジェクトのディレクトリにある `src/components` ファイル:
    * `Tab.js` タブのコンテンツ ページをレンダリングします。
    * `TabConfig.js` タブの構成ページをレンダリングします。
  * Microsoft TeamsJavaScript クライアント SDK は、プロジェクトのフロントエンド コンポーネントに事前に読み込まれます。

## <a name="3-customize-your-tab-content-page"></a>3. タブ コンテンツ ページをカスタマイズする

1. 組織に関連する情報を使用して、次のコード サンプルをコピーして変更します。 スニペットは次のように使用することもできます。
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
1. ディレクトリに移動 `src/components` し、ファイルを開 `Tab.js` きます。 次の例 `render()` に示すように、関数を見つけて `return()` コードを内部に貼り付けます。
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
1. ディレクトリに移動し、次のコードでファイルを更新して、使用されているテーマで電子メール リンクを読みやすく `src/components` `App.css` します。
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a>4. タブ構成ページをカスタマイズする

チャネルまたはチャットのすべてのタブには構成ページがあります。モーダルで、ユーザーがアプリを追加するときに少なくとも 1 つのセットアップ オプションが表示されます。 既定では、構成ページは、タブがインストールされているときにチャネルまたはチャットに通知する必要がある場合に、ユーザーに通知を求めるメッセージを表示します。 カスタム コンテンツを追加することで、構成ページをカスタマイズできます。

カスタム コンテンツを追加するには、ディレクトリからファイルを開き、次の例に示すようにプレースホルダー コンテンツ `TabConfig.js` `src/components` `return()` を内部で更新します。

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
> ユーザーがアプリについて初めて読むので、このページでアプリに関する簡単な情報を提供します。 カスタム構成オプションや、タブ構成ページで一般的 [な](../tabs/how-to/authentication/auth-aad-sso.md)認証ワークフローを含めすることもできます。

## <a name="5-customize-your-tab-name"></a>5. タブ名をカスタマイズする

チャネル タブを追加すると、アプリ名が既定で表示されます (たとえば、 **ファースト** アプリ)。 グループの共同作業のコンテキストで意味のある名前を指定できます 。たとえば、 **チーム** 連絡先:

1. ディレクトリに移動 `src/components` し、ファイルを開 `TabConfig.js` きます。
1. 次の例に示すように、既定で表示するタブ名を持 `suggestedDisplayName` つ `microsoftTeams.settings.setSettings` プロパティを追加します。

  ```JavaScript
    microsoftTeams.settings.setSettings({
    "contentUrl": "https://localhost:3000/tab",
    "suggestedDisplayName": "Team Contacts"
  });
  ```

## <a name="6-build-and-run-your-app"></a>6. アプリをビルドして実行する

このチュートリアルでは、アプリをローカルでビルドして実行する方法について説明します。 

1. ターミナルのアプリ プロジェクトのルート ディレクトリに移動します。
1. `npm install` を実行します。
1. `npm start` を実行します。

この情報は、ツールキットの `README` セクションにも表示されます。
コンパイルが正常に完了 `https://localhost:3000` した後、 **アプリが実行されています。** メッセージがターミナルに表示されます。 

## <a name="7-sideload-your-app-in-teams"></a>7. アプリをサイドロードTeams

お使いのアプリは Teams でテストする準備ができています。 これを行うには、アプリのサイドローディングを許可するアカウントが必要です。 

1. F5 キー Teamsを使用して、Visual Studio Code Web クライアント **を開** きます。
1. 次の手順に従って信頼できる ( ) を追加し、アプリ コンテンツをアプリ コンテンツを次の手順 `localhost` で表示Teams。

   1. F5 キーで開いたのと同じブラウザー ウィンドウ (既定では Google Chrome) で新しいタブ **を開** きます。
   1. ページ `https://localhost:3000/tab` を開いて続行します。

1. [**チームに追加] または**[チャット **に** 追加] を選択し、チャットのモーダルからテストに使用できるチャネルまたはチャットTeams。
1. [タブ **の設定] を選択します**。構成ページはモーダルで表示されます。

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="チャネル タブ構成ページのスクリーンショット。":::

1. [保存 **] を** 選択してタブを構成します。次のコンテンツ ページが表示されます。

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="静的コンテンツ ビューを含むチャネル タブのスクリーンショット。":::

## <a name="see-also"></a>関連項目

* [最初の Microsoft Teams アプリを構築して実行する](../build-your-first-app/build-and-run.md) 
* [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [デスクトップと Web のタブMicrosoft Teamsデザインする](../tabs/design/tabs.md) 
* [UI テンプレートをMicrosoft Teamsアプリを設計する](../concepts/design/design-teams-app-ui-templates.md) 
* [モバイルのタブ](../tabs/design/tabs-mobile.md)
* [タブのシングル サインオン (SSO) のサポート](../tabs/how-to/authentication/auth-aad-sso.md)
* [Microsoft Teams API の概要](https://docs.microsoft.com/graph/teams-concept-overview)
* [カスタム個人用タブを作成し、Node.jsの Yeoman Generator を使用Microsoft Teams](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Bot を作成する](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [メッセージングの拡張機能を作成する](../build-your-first-app/build-messaging-extension.md)