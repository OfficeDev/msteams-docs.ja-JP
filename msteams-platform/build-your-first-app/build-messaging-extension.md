---
title: 開始する - メッセージング拡張機能を構築する
author: heath-hamilton
description: Microsoft Teams を使用して、Microsoft Teams メッセージング拡張機能をすばやく作成Toolkit。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 86d44740feaa2cd33aff0e1dde14d757420d90d6
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911920"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a>Microsoft Teams のメッセージング拡張機能を構築する

Teams アプリのメッセージング拡張機能には、検索コマンド *と* アクション コマンドの 2 [種類](../messaging-extensions/how-to/search-commands/define-search-command.md)[があります](../messaging-extensions/how-to/action-commands/define-action-command.md)。

このレッスンでは、外部コンテンツを検索して Teams で共有するショートカットである検索コマンド *(検索* ベースのメッセージング拡張機能とも呼ばれる) を作成します。 ユーザーは、Teams の作成またはコマンド ボックス [から検索コマンドにアクセスできます](../messaging-extensions/what-are-messaging-extensions.md)。

## <a name="your-assignment"></a>割り当て

組織のヘルプ デスクは Teams を通じてユーザーと通信しますが、チケットは別のシステムに存在します。 つまり、サポート スタッフは常にアプリ間を行き来する必要があります。 Teams の単純な検索ベースのメッセージング拡張機能を作成することで、このようなコンテキスト切り替えの量を減らす方法を調査します。

## <a name="what-youll-learn"></a>学習する情報

> [!div class="checklist"]
>
> * Microsoft Teams Toolkit for Visual Studio Code を使用してアプリ プロジェクトとメッセージング拡張機能ボットを作成する
> * アプリの構成とメッセージング拡張機能に関連するスキャフォールディングの一部を特定する
> * アプリをローカルでホストする
> * メッセージング拡張機能用にボットを構成する
> * Teams でメッセージング拡張機能をサイドロードしてテストする

## <a name="before-you-begin"></a>はじめに

まだ理解していない場合は、Teams 開発の前提条件 [を理解してインストールしてください](build-first-app-overview.md#get-prerequisites)。

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

Microsoft Teams Toolkitは、メッセージング拡張機能用に次のコンポーネントを設定するのに役立ちます。

* **メッセージング拡張機能に関連するアプリ** の構成とスキャフォールディング
*  Microsoft Azure Bot Service に自動的に登録されるメッセージング拡張機能のボット

> [!TIP]
> Teams アプリ プロジェクトをまだ作成していない場合は、プロジェクトについて詳しく説明する次[](../build-your-first-app/build-and-run.md)の手順に従うのが役に立つ場合があります。

1. [Visual Studioコード] で、左側のアクティビティ バーで **Microsoft Teams** を選択し、[新しい Teams アプリの作成 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: ] **を選択します**。
1. ダイアログが表示されたら、Microsoft 365 開発アカウントでサインインします。
1. [機能 **の追加] 画面で、[****メッセージング拡張機能]** を選択し、[次へ] を **選択します**。
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前と、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です)。
1. [メッセージング **拡張機能の構成] 画面で** 、次の操作を行います。
    1. メッセージング拡張機能 **の種類に対して** 検索ベースのオプションのみを選択します。
    1. [新 **しいボットの作成] を選択し、[****ボット登録の作成] を選択します**。 成功した場合、新しいボットの状態は **登録済み** になります。
    1. ここで、リンクの **分岐オプション** として [いいえ] を選択します。
1. 画面 **の** 下部にある [完了] を選択して、プロジェクトを構成します。

## <a name="2-identify-relevant-app-project-components"></a>2. 関連するアプリ プロジェクト コンポーネントを特定する

アプリの構成とスキャフォールディングの多くが、Teams アプリを使用してプロジェクトを作成するときに自動的に設定Toolkit。

### <a name="app-configurations"></a>アプリの構成

メッセージング拡張機能の構成を表示または更新するには、ツールキットで **App Studio** を選択し、 **メッセージング拡張機能に移動します**。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングは、メッセージング拡張機能 (または技術的にはメッセージング拡張機能のボット) が Teams の検索クエリに応答する方法を処理するために、プロジェクトのルート ディレクトリにあるファイルを提供します。 `botActivityHandler.js` [](#4-configure-the-bot-for-your-messaging-extension)

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. アプリへのセキュリティで保護されたトンネルを設定する

テストの目的で、メッセージング拡張機能をローカル Web サーバー (ポート 3978) でホストします。

1. まだインストールしていない場合は [、ngrok をインストールします](https://ngrok.com/download)。
1. ターミナルで、次を実行します `ngrok http -host-header=rewrite 3978` 。
1. Teams は HTTPS 接続を必要としますので、出力内の HTTPS URL (たとえば `https://468b9ab725e9.ngrok.io` ) をコピーします。

この URL を使用すると、Teams (HTTPS 接続が必要) は、アプリをホストしている場所 (ポート `localhost` 3978) にトンネリングできます。

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. メッセージング拡張機能用にボットを構成する

メッセージング拡張機能はボットに依存して、Teams からホストされたサービスにユーザー要求を送信および処理します。 ボットは Azure Bot Service に登録する必要があります。このサービスは、Teams サービスを使用してアプリをセットアップToolkit。

メッセージング拡張機能で検索クエリを受信および処理するには、ボット エンドポイント URL を指定する必要があります。 通常、URL は次のように表示されます `https://HOST_URL/api/messages` 。 この設定は、ツールキットですばやく構成できます。

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Open Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Toolkit.**
1. 既存の **ボット登録>ボットに移動し** 、セットアップ時に作成したボットを選択します。
1. [Bot **endpoint address]** フィールドに、ボットをホストしている ngrok URL (たとえば) を入力し、 `https://468b9ab725e9.ngrok.io` ボットに `/api/messages` 追加します。

ボットはメッセージング拡張機能でクエリを処理できます。

## <a name="5-build-and-run-your-app"></a>5. アプリをビルドして実行する

メッセージング拡張機能をホストする URL を設定し、検索を処理するように構成しました。 次に、アプリを起動して実行します。

1. ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、実行します `npm install` 。
1. `npm start` を実行します。

成功した場合は、メッセージング拡張機能サービスが自分のアクティビティをリッスン中であることを示す次のメッセージが表示されます `localhost` 。

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. Teams でメッセージング拡張機能をサイドロードする

メッセージング拡張機能を実行すると、Teams にインストールできます。

> [!TIP]
> 以前に Teams アプリをサイドローディングして問題が発生していない場合は、次の手順に [従います](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。

1. コードVisual Studio **F5** キーを押して、Teams Web クライアントを起動します。
1. アプリのインストール ダイアログで、[追加] **を選択します**。

## <a name="7-test-your-messaging-extension"></a>7. メッセージング拡張機能をテストする

Teams チャットでのメッセージング拡張機能の動作について説明します。

1. 新しいチャットを開始します。 作成ボックスで [その他] **を** 選択し、サイドローディングした :::image type="icon" source="../assets/icons/teams-client-more.png"::: メッセージング拡張機能アプリを選択します。
1. 何か (チケットなど) を **検索してみてください**。 アプリが動作している場合は、サンプルの検索結果が表示されます (後で独自の検索結果を追加できます)。<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Teams の作成ボックスで検索ベースのメッセージング拡張機能がどのように使用されるのか示すスクリーンショット。":::

## <a name="well-done"></a>よくやりましたね

おめでとうございます! 作成ボックスまたはコマンド ボックスで外部コンテンツを検索するように設定されている基本的な Teams メッセージング拡張機能があります。

## <a name="next-steps"></a>次の手順

すべての機能を備ったメッセージング拡張機能を続行して構築するには、次のページを参照してください。

1. [サービスに関連する](../messaging-extensions/how-to/search-commands/define-search-command.md) 検索コマンドを定義します。
1. ユーザーの検索に [応答するサービスを構成します](../messaging-extensions/how-to/search-commands/respond-to-search.md)。

## <a name="troubleshooting"></a>トラブルシューティング

このチュートリアルを完了する上で問題が発生した場合は、次の情報が役立つ場合があります。

### <a name="bot-isnt-connected-to-teams"></a>ボットが Teams に接続されていない

アプリをインストールしたが動作しない場合は、メッセージング拡張機能のボットが Azure Bot Service の Teams チャネルに接続 [されていることを確認 *します*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

これは Teams のチャネルと同じではないという点を理解することが重要です。 この場合、チャネルは、Azure Bot Service がボットを Teams または別のサポートされている Microsoft またはサード パーティ通信アプリに接続 [する方法です](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="learn-more"></a>詳細情報

* [リンクの分岐機能を含める](../messaging-extensions/how-to/link-unfurling.md)
* 設計ガイドライン [に従い](../messaging-extensions/design/messaging-extension-design.md) 、実稼働対応 [の UI](../concepts/design/design-teams-app-ui-templates.md) テンプレートを使用してビルドし、シームレスなエクスペリエンスを作成します。
* [認証を追加する](../messaging-extensions/how-to/add-authentication.md)
* [アクション ベースのメッセージング拡張機能を作成する](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
