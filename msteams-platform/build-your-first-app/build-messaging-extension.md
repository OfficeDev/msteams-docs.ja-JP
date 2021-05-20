---
title: はじめに - メッセージング拡張機能を構築する
author: girliemac
description: Microsoft Teams Toolkitを使用して、Microsoft Teamsメッセージング拡張機能をすばやく作成します。
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: c120a5b5d878c549cde008c3e1ccc71743a4e24f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566062"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a>Microsoft Teamsの最初のメッセージング拡張機能を構築する

*Teamsメッセージング拡張機能* には、[検索コマンド](../messaging-extensions/how-to/search-commands/define-search-command.md)と [アクションコマンド](../messaging-extensions/how-to/action-commands/define-action-command.md)の 2 種類があります。

このチュートリアルでは、外部コンテンツを検索してTeamsで共有するためのショートカットである *検索コマンド*(*検索ベースのメッセージング拡張機能* とも呼ばれます) を作成する方法について説明します。 ユーザーは、Teams作成またはコマンド ボックスから検索コマンドにアクセスできます。

## <a name="what-youll-learn"></a>あなたが学ぶこと

* Visual Studio CodeのMicrosoft Teams Toolkitを使用して、アプリ プロジェクトとメッセージング拡張機能のボットを作成します。
* アプリの構成と、メッセージング拡張機能に関連するスキャフォールディングについて理解する。
* アプリをローカルでホストします。
* メッセージング拡張機能のボットを構成します。
* Teamsでメッセージング拡張機能をサイドロードしてテストします。

## <a name="prerequisites"></a>前提条件

簡単なTeams アプリを設定して構築する方法を理解していることを確認します。 詳細については、[最初のMicrosoft Teams "Hello, World!" アプリを作成する](../build-your-first-app/build-and-run.md)を参照してください。

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

Microsoft Teams Toolkitは、メッセージング拡張機能の次のコンポーネントを設定するのに役立ちます。

* メッセージング拡張機能に関連 **するアプリの構成とスキャフォールディング**。
* **Microsoft Azure Bot** サービスに自動的に登録されるメッセージング拡張機能のボット。

**アプリ プロジェクトを作成するには**

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。
1. メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。
1. [**プロジェクトの選択**] 画面 **の [メッセージング拡張機能**  >  **検索**] で **、[JS (JavaScript)]** をクリックします。 
1. Teams アプリの名前を入力します。 これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前でもあります。
1. [ **新しいボットを作成する** ] を選択し、[ **ボット登録の作成** ] ボタンをクリックします。 成功した場合、新しいボットは *登録済み* ステータスになります。 これで、ボットが Microsoft Azure Bot サービスに自動的に登録されます。 
1. 画面の下部にある **[完了] を** 選択してプロジェクトを構成し、プロジェクトをローカル コンピューターに保存します。

## <a name="2-understand-your-app-project-components"></a>2. アプリ プロジェクト コンポーネントを理解する

アプリの構成とスキャフォールディングの多くは、Teams Toolkitを使用してプロジェクトを作成するときに自動的に設定されます。

* アプリの構成: メッセージング拡張機能の構成を表示または更新するには、ツールキットで **[App Studio]** を選択し、[ **メッセージング拡張機能**] に移動します。
* アプリのスキャフォールディング: アプリのスキャフォールディングは `botActivityHandler.js` 、メッセージング拡張機能 (または技術的にはメッセージング拡張機能[のボット](#4-configure-the-bot-for-your-messaging-extension)) がTeamsの検索クエリにどのように応答するかを処理するために、プロジェクトのルート ディレクトリにあるファイルを提供します。

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. アプリへの安全なトンネルを設定する

テスト目的で、ローカル Web サーバー (ポート 3978) でメッセージング拡張機能をホストしましょう。 ローカルホストへのセキュアなトンネルを設定するために [ngrok](https://ngrok.com/download) を使用します。 詳細については[、最初のボットの構築Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet)参照してください。 

1. まだインストールしていない場合は [、ngrok](https://ngrok.com/download)をインストールします。
1. ターミナルで、 `ngrok http -host-header=rewrite 3978` を実行します。
1. Teamsには HTTPS 接続が必要なので、出力内の HTTPS URL をコピーします (例: `https://468b9ab725e9.ngrok.io` ) 。

   この URL を使用すると、Teams (HTTPS 接続が必要) は、(ポート 3978 上の) アプリをホストしている場所にトンネルを作成できます `localhost` 。

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. メッセージング拡張機能のボットを構成する

メッセージング拡張機能は、ボットに依存して、Teamsからホストされたサービスへのユーザー要求を送信および処理します。 ボットは、Teams Toolkitを使用してアプリを設定するときに実行された Azure Bot サービスに登録する必要があります。

メッセージング拡張機能で検索クエリを受信および処理するには、ボット エンドポイント URL を指定する必要があります。 通常、URL は `https://HOST_URL/api/messages` のようになります。 この設定は、ツールキットですばやく構成できます。

1. Visual Studio Codeで、 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 左側のアクティビティ バーのMicrosoft Teamsを選択し **、[Microsoft Teams Toolkitを開く**] を選択します。
1. **[ボット>既存のボットの登録]** に移動し、セットアップ中に作成したボットを選択します。
1. [ **ボット エンドポイント アドレス]** フィールドに、ボットをホストしている ngrok URL (たとえば) を入力し、その URL `https://468b9ab725e9.ngrok.io` `/api/messages` に追加します。

   ボットは、メッセージング拡張機能でクエリを処理できるようになります。

## <a name="5-build-and-run-your-app"></a>5. アプリをビルドして実行する

メッセージング拡張機能をホストする URL を設定し、検索を処理するように構成しました。 アプリを起動して実行する時間です。

1. ターミナルを開き、アプリ プロジェクトのルート ディレクトリに移動します。
1. `npm install` を実行します。
1. `npm start` を実行します。

   正常に実行された場合、メッセージング拡張サービスが でのアクティビティをリッスンしていることを示す次のメッセージが表示されます `localhost` 。

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. Teamsでメッセージング拡張機能をサイドロードする

メッセージング拡張機能を実行すると、Teamsでインストールできます。

> [!TIP]
> Teamsアプリを以前にサイドロードし、問題が発生していない場合は、次の[手順](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)に従ってください。

1. Visual Studio Codeで **、F5** キーを選択して、Teams Web クライアントを起動します。
1. [アプリのインストール] ダイアログで、[ **追加**] を選択します。

## <a name="7-test-your-messaging-extension"></a>7. メッセージング拡張機能をテストする

Teams チャットでメッセージング拡張機能がどのように機能するかを説明します。

1. 新しいチャットを開始します。 [新規作成] ボックスで [ **詳細**] を選択 :::image type="icon" source="../assets/icons/teams-client-more.png"::: し、サイドロードしたメッセージング拡張機能アプリを選択します。
1. 何か (たとえば、 **チケット**) を検索してみてください。 アプリが動作している場合は、サンプル検索結果が表示されます (後で独自に追加できます)。

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Teams作成ボックスで検索ベースのメッセージング拡張機能を使用する方法を示すスクリーンショット。":::

## <a name="troubleshooting"></a>トラブルシューティング

このチュートリアルを完了する際に問題が発生した場合は、次の情報が役立ちます。

**ボットがTeamsに接続されていない**

アプリをインストールしても動作しない場合は、メッセージング拡張機能のボットが Azure Bot Service の [Teams *チャネル* に接続](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)されていることを確認します。

これはTeamsのチャンネルと同じではないことを理解することが重要です。 この場合、チャネルとは、Azure Bot サービスがボットをTeamsまたは[サポートされている別の Microsoft またはサードパーティの通信アプリ](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)に接続する方法です。

## <a name="see-also"></a>関連項目

* [Teams作成またはコマンド ボックス](../messaging-extensions/what-are-messaging-extensions.md) 
* [リンクを展開する機能を含める](../messaging-extensions/how-to/link-unfurling.md)
* [デザインのガイドライン](../messaging-extensions/design/messaging-extension-design.md) 
* [プロダクション対応の UI テンプレート](../concepts/design/design-teams-app-ui-templates.md) 
* [認証を追加する](../messaging-extensions/how-to/add-authentication.md)
* [アクションベースのメッセージング拡張機能を作成する](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [検索コマンドを定義する](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [ユーザーの検索に応答する](../messaging-extensions/how-to/search-commands/respond-to-search.md)
