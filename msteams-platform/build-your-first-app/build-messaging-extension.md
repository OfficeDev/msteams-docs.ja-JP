---
title: 使い始める - メッセージング拡張機能を作成する
author: girliemac
description: アプリケーションを使用してMicrosoft Teamsメッセージング拡張機能をすばやく作成Microsoft Teams Toolkit。
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: 91a5a15697163ee9103607511047a6411a5acf1a
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068760"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a>ユーザー向け最初のメッセージング拡張機能をMicrosoft Teams

メッセージング拡張機能には、検索Teams *アクション コマンド* の 2 [種類](../messaging-extensions/how-to/search-commands/define-search-command.md)[があります](../messaging-extensions/how-to/action-commands/define-action-command.md)。

このチュートリアルでは、外部コンテンツを検索し、Teams で共有するショートカットである検索コマンド *(検索* ベースのメッセージング拡張機能とも呼ばれる) を作成する方法について説明します。 ユーザーは、[新規作成] または [コマンド] ボックスからTeamsコマンドにアクセスできます。

## <a name="what-youll-learn"></a>学習する情報

* アプリ プロジェクトとメッセージング拡張機能ボットを作成するには、アプリ のMicrosoft Teams ToolkitをVisual Studio Code。
* アプリの構成とメッセージング拡張機能に関連するスキャフォールディングについて理解します。
* アプリをローカルでホストします。
* メッセージング拡張機能のボットを構成します。
* メッセージ拡張機能をサイドロードしてテストTeams。

## <a name="prerequisites"></a>前提条件

簡単なアプリをセットアップして構築する方法を理解Teamsしてください。 詳細については[、「Hello, World!」アプリMicrosoft Teamsを作成するを参照してください](../build-your-first-app/build-and-run.md)。

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

このMicrosoft Teams Toolkitは、メッセージング拡張機能用に次のコンポーネントをセットアップするのに役立ちます。

* **メッセージング拡張機能に関連するアプリ** の構成とスキャフォールディング
* **ボット** サービスに自動的に登録されるメッセージング拡張機能Microsoft Azureボット

**アプリ プロジェクトを作成するには**

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。
1. メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。
1. [プロジェクト **の選択]** 画面の [**メッセージング拡張機能** の検索]  >  **で、[JS** **(JavaScript) ] をクリックします**。 
1. Teams アプリの名前を入力します。 これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です。
1. [新 **しいボットの作成] を選択し** 、[ **ボット登録の作成] ボタンをクリック** します。 成功した場合、新しいボットの状態は *[* 登録済み] になります。 これで、ボットは自動的にボット サービスMicrosoft Azure登録されます。 
1. 画面 **の下部** にある [完了] を選択してプロジェクトを構成し、プロジェクトをローカル コンピューターに保存します。

## <a name="2-understand-your-app-project-components"></a>2. アプリ プロジェクト コンポーネントについて

アプリの構成とスキャフォールディングの多くが、プロジェクトを作成するときに自動的に設定Teams Toolkit。

* アプリの構成: メッセージング拡張機能の構成を表示または更新するには、ツールキットで **[App Studio]** を選択し、[メッセージング拡張機能 **] に移動します**。
* アプリのスキャフォールディング: アプリのスキャフォールディングは、メッセージング拡張機能 (または技術的にはメッセージング拡張機能のボット) が Teams で検索クエリに応答する方法を処理するために、プロジェクトのルート ディレクトリにあるファイルを提供します。 `botActivityHandler.js` [](#4-configure-the-bot-for-your-messaging-extension)

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. アプリにセキュリティで保護されたトンネルを設定する

テストの目的で、メッセージング拡張機能をローカル Web サーバー (ポート 3978) でホストします。 [ngrok](https://ngrok.com/download)を使用して localhost へのセキュリティで保護されたトンネルを設定します。 詳細[については、「最初のボットをビルドMicrosoft Teams」](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet)を参照してください。 

1. まだインストールしていない場合は [、ngrok をインストールします](https://ngrok.com/download)。
1. ターミナルで、 を実行します `ngrok http -host-header=rewrite 3978` 。
1. HTTPS 接続が必要な場合は、出力内の HTTPS `https://468b9ab725e9.ngrok.io` URL (たとえば) Teamsコピーします。

   この URL を使用Teams (HTTPS 接続が必要) は、アプリをホストしている場所 (ポート `localhost` 3978) にトンネルを接続できます。

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. メッセージング拡張機能のボットを構成する

メッセージング拡張機能は、ボットを使用して、ホストされているサービスに対して、Teams要求を送信および処理します。 ボットは Azure Bot Service に登録されている必要があります。これは、アプリを使用してアプリをセットアップするときに実行Teams Toolkit。

メッセージング拡張機能で検索クエリを受信および処理するには、ボット エンドポイント URL を指定する必要があります。 通常、URL は次のように表示されます `https://HOST_URL/api/messages` 。 この設定はツールキットですばやく構成できます。

1. [Visual Studio Code] で **Microsoft Teamsの**[アクティビティ バー] を選択し、[開く] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: Microsoft Teams Toolkit。 
1. [ボット] **>既存のボット登録に移動し、** セットアップ中に作成したボットを選択します。
1. [ **ボット エンドポイント アドレス** ] フィールドに、ボットをホストしている ngrok URL (たとえば) を入力し、 `https://468b9ab725e9.ngrok.io` ボットに `/api/messages` 追加します。

   ボットはメッセージング拡張機能でクエリを処理できます。

## <a name="5-build-and-run-your-app"></a>5. アプリをビルドして実行する

メッセージング拡張機能をホストする URL を設定し、検索を処理するように構成しました。 アプリを起動して実行する時間です。

1. ターミナルを開き、アプリ プロジェクトのルート ディレクトリに移動する
1. `npm install` を実行します。
1. `npm start` を実行します。

   成功した場合は、メッセージング拡張機能サービスがアクティビティをリッスン中であることを示す次のメッセージが表示されます `localhost` 。

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. メッセージング拡張機能をサイドロードTeams

メッセージング拡張機能を実行すると、メッセージング拡張機能をインストールTeams。

> [!TIP]
> 以前にアプリをサイドロードTeams問題が発生していない場合は、次の手順に[従います](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。

1. [Visual Studio Code **F5** キーを選択して、Web クライアントTeams起動します。
1. [アプリのインストール] ダイアログで、[追加] **を選択します**。

## <a name="7-test-your-messaging-extension"></a>7. メッセージング拡張機能をテストする

メッセージング拡張機能がチャットでどのように機能Teamsします。

1. 新しいチャットを開始します。 作成ボックスで、[詳細] **を選択** し、サイドロードしたメッセージング :::image type="icon" source="../assets/icons/teams-client-more.png"::: 拡張機能アプリを選択します。
1. 何かを検索してみてください (**チケットなど)。** アプリが動作している場合は、サンプル検索結果が表示されます (後で独自の検索結果を追加できます)。

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="[メッセージ作成] ボックスで検索ベースのメッセージング拡張機能がどのように使用Teamsスクリーンショットです。":::

## <a name="troubleshooting"></a>トラブルシューティング

このチュートリアルの完了に問題がある場合は、次の情報が役立つ場合があります。

**ボットがデバイスに接続Teams**

アプリをインストールしたが機能しない場合は、メッセージング拡張機能のボットが Azure Bot Service のサービス チャネルに接続されていることを [Teams *してください*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

これは、チャネルと同じではないと理解することが重要Teams。 この場合、チャネルとは、Azure Bot Service がボットを他の microsoft またはサード パーティの通信アプリTeamsに接続する[方法です](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="see-also"></a>関連項目

* [Teams作成またはコマンド ボックス](../messaging-extensions/what-are-messaging-extensions.md) 
* [リンクのリンク解除機能を含める](../messaging-extensions/how-to/link-unfurling.md)
* [デザインのガイドライン](../messaging-extensions/design/messaging-extension-design.md) 
* [実稼働対応の UI テンプレート](../concepts/design/design-teams-app-ui-templates.md) 
* [認証を追加する](../messaging-extensions/how-to/add-authentication.md)
* [アクション ベースのメッセージング拡張機能を作成する](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [検索コマンドを定義する](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [ユーザーの検索に応答する](../messaging-extensions/how-to/search-commands/respond-to-search.md)