---
title: 開始する - ボットを作成する
author: heath-hamilton
description: Microsoft Teams ボットを使用して、Microsoft Teams ボットをすばやく作成Toolkit。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 3e07c148e1b03431dc419a4e3679abac0229ff72
ms.sourcegitcommit: e08f309f62db2cf0f505f2aadfe728e5b46c17a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "50140469"
---
# <a name="build-a-bot-for-microsoft-teams"></a>Microsoft Teams のボットを構築する

このチュートリアルでは、基本的な *ボット* アプリを作成します。 ボットは、Teams ユーザーと Web サービスの間の仲介者として機能します。 ユーザーはボットとチャットして、情報をすばやく取得したり、サービスによって実行されるワークフローやタスクを開始することができます。

## <a name="your-assignment"></a>割り当て

職場で、タブを使用して重要 [な連絡先情報](../build-your-first-app/build-personal-tab.md) を表示する Teams アプリを作成しました。 たとえば、同僚はヘルプ デスクの電話番号にすばやくアクセスできます。 しかし、ユーザーがチャットボットを使用してヘルプ デスクに問い合わせたらどうでしょうか。 上司から、Teams で基本的な会話ボットをどのくらいの速い時間で実行できるのか確認する必要があります。

## <a name="what-youll-learn"></a>学習する情報

> [!div class="checklist"]
>
> * Microsoft Teams Toolkit for Visual Studio コードを使用してアプリ プロジェクトとボットをVisual Studioする
> * ボットに関連するアプリ構成とスキャフォールディングの一部を特定する
> * アプリをローカルでホストする
> * Teams のボットを構成する
> * Teams でボットをサイドロードしてテストする

## <a name="before-you-begin"></a>はじめに

まだ理解していない場合は、Teams 開発の前提条件 [を理解してインストールしてください](build-first-app-overview.md#get-prerequisites)。

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

Microsoft Teams Toolkitは、アプリ用に次のコンポーネントを設定するのに役立ちます。

* **ボットに関連するアプリの** 構成とスキャフォールディング
*  Microsoft Azure Bot Service に自動的に登録されるボット

> [!TIP]
> Teams アプリ プロジェクトをまだ作成していない場合は、プロジェクトについて詳しく説明する次[](../build-your-first-app/build-and-run.md)の手順に従うのが役に立つ場合があります。

1. [Visual Studioコード] で、左側のアクティビティ バーで **Microsoft Teams** を選択し、[新しい Teams アプリの作成 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: ] **を選択します**。
1. ダイアログが表示されたら、Microsoft 365 開発アカウントでサインインします。
1. [機能 **の追加] 画面で、[** ボット] **を選択** し、[次へ] を **選択します**。
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前と、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です)。
1. [ボットの **構成] に移動し** 、[新しい **ボットの作成] を** 選択し、[ **ボット登録の作成] を選択します**。 成功した場合、新しいボットの状態は **登録済み** になります。
1. 画面 **の** 下部にある [完了] を選択し、プロジェクトを作成する場所を選択します。

## <a name="2-identify-relevant-app-project-components"></a>2. 関連するアプリ プロジェクト コンポーネントを特定する

アプリの構成とスキャフォールディングの多くが、Teams アプリケーションを使用してプロジェクトを作成するときに自動的に設定Toolkit。 ボットを構築する主なコンポーネントを見てみしましょう。

### <a name="app-configurations"></a>アプリの構成

ボットの構成を表示または更新するには、ツールキットで **App Studio** を選択し、[ボット] に **移動します**。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングでは、ボットが Teams でアクティビティを処理する方法 (たとえば、ボットが "Hello" などの特定のメッセージに応答する方法) を処理するために、プロジェクトのルート ディレクトリにあるファイルが提供されます。 `botActivityHandler.js`

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. アプリへのセキュリティで保護されたトンネルを設定する

テストの目的で、ローカル Web サーバー (ポート 3978) でアプリをホストします。

1. まだインストールしていない場合は [、ngrok をインストールします](https://ngrok.com/download)。
1. ターミナルで、次を実行します `ngrok http -host-header=rewrite 3978` 。
1. Teams は HTTPS 接続を必要としますので、出力内の HTTPS URL (例 `https://468b9ab725e9.ngrok.io` : HTTPS URL) をコピーします。

この URL を使用すると、Teams (HTTPS 接続が必要) は、アプリをホストしている場所 (ポート `localhost` 3978) にトンネリングできます。

## <a name="4-configure-your-bot"></a>4. ボットを構成する

Teams でボットを使用するには、Azure Bot Service にボットを登録する必要があります。 Teams アプリを使用してアプリをセットアップすると、自動的に実行Toolkit。

引き続き、ボットに送信されるユーザー メッセージ (要求) を受信および処理するエンドポイント アドレスを指定する必要があります。 通常、URL は次のように表示されます `https://HOST_URL/api/messages` 。 この設定は、ツールキットですばやく構成できます。

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Open Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Toolkit.**
1. 既存の **ボット登録>ボットに移動し** 、セットアップ時に作成したボットを選択します。
1. [Bot **endpoint address]** フィールドに、ボットをホストしている ngrok URL (たとえば) を入力し、 `https://468b9ab725e9.ngrok.io` ボットに `/api/messages` 追加します。<br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Teams アプリケーションでボット エンドポイント URL を構成できる場所を示Toolkit。":::

ボットは Teams のメッセージに応答できます。

## <a name="5-build-and-run-your-app"></a>5. アプリをビルドして実行する

ボットをホストする URL を設定し、メッセージを処理するようにボットを構成しました。 次に、アプリを起動して実行します。

1. ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、実行します `npm install` 。
1. `npm start` を実行します。

成功した場合、ボットが自分のアクティビティをリッスン中であることを示す次のメッセージが表示されます `localhost` 。

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. Teams でボットをサイドロードする

ボットを実行すると、Teams にインストールできます。

> [!TIP]
> 以前に Teams アプリをサイドローディングして問題が発生していない場合は、次の手順に [従います](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。

1. コードVisual Studio **F5** キーを押して、Teams Web クライアントを起動します。
1. アプリのインストール ダイアログで、[追加] **を選択します**。 (ボットをチャネルまたはチャットに追加できますが、1 対 1 のチャットでボットをテストする方が、他のユーザーに対してはあまり邪魔ではありません)。

## <a name="7-test-your-bot"></a>7. ボットをテストする

ここで、楽しい部分について:ボットに "Hello" と言います。

1. 作成ボックスで、メッセージを送信 `Hello` します。

ボットは次のようなメッセージで応答します。

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="ユーザーが Teams ボットに 「Hello」と言って応答を受け取るスクリーンショット。":::

## <a name="well-done"></a>よくやりましたね

おめでとうございます。 1 対 1 またはグループ設定 (チャネルとチャット) でユーザーと通信できる基本的な Teams ボットがあります。

## <a name="troubleshooting"></a>トラブルシューティング

このチュートリアルを完了する上で問題が発生した場合は、次の情報が役立つ場合があります。

### <a name="bot-isnt-connected-to-teams"></a>ボットが Teams に接続されていない

アプリをインストールしたがボットが機能しない場合は、ボットが Azure Bot Service の Teams チャネルに接続 [されていることを確認 *します*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

これは Teams のチャネルと同じではないという点を理解することが重要です。 この場合、チャネルは、Azure Bot Service がボットを Teams または別のサポートされている Microsoft またはサード パーティ通信アプリに接続 [する方法です](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="learn-more"></a>詳細情報

* [サンプルの 1 つで Teams ボットが実行できるその他の操作を参照する](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [ボット会話の基本](../bots/how-to/conversations/conversation-basics.md)
* 設計ガイドライン [に従い](../bots/design/bots.md) 、実稼働環境対応 [の UI](../concepts/design/design-teams-app-ui-templates.md) テンプレートを使用してビルドし、シームレスなエクスペリエンスを作成します。
* [Teams でのボット認証](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [ツールキットを使用せずにボットを作成する](../resources/bot-v3/bots-create.md)
