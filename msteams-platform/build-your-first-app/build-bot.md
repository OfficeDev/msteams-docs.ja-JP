---
title: '[スタート] - ボットを作成する'
author: heath-hamilton
description: Microsoft Teams ボットを使用して Microsoft Teams ボットをすばやく作成Toolkit。
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 5dfbfa05d2f1e36bbc14bd929cb2592303081522
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020001"
---
# <a name="build-a-bot-for-microsoft-teams"></a>Microsoft Teams 用のボットを作成する

このチュートリアルでは、基本的 *なボット アプリ* を作成します。 ボットは、Teams ユーザーと Web サービスの間の仲介者として機能します。 ユーザーはボットとチャットして、情報をすばやく取得したり、サービスによって実行されるワークフローやタスクを開始できます。

## <a name="your-assignment"></a>割り当て

職場では、タブを使用して重要 [な連絡先情報を](../build-your-first-app/build-personal-tab.md) 表示する Teams アプリを作成しました。 たとえば、同僚はヘルプ デスクの電話番号にすばやくアクセスできます。 しかし、通話の代わりに、チャットボットを使用してヘルプ デスクに問い合わせたらどうしますか? 上司から、Teams で基本的な会話ボットを立ち上げ、実行できる時間を確認するメッセージが表示されます。

## <a name="what-youll-learn"></a>学習する情報

> [!div class="checklist"]
>
> * Microsoft Teams を使用してアプリ プロジェクトとボットを作成ToolkitコードVisual Studioする
> * ボットに関連するアプリ構成とスキャフォールディングの一部を特定する
> * アプリをローカルでホストする
> * Teams のボットを構成する
> * Teams でボットをサイドロードしてテストする

## <a name="before-you-begin"></a>はじめに

まだインストールしていない場合は、Teams 開発の [前提条件を理解してインストールしてください](build-first-app-overview.md#get-prerequisites)。

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

Microsoft Teams Toolkitは、アプリの次のコンポーネントをセットアップするのに役立ちます。

* **ボットに関連するアプリの構成** とスキャフォールディング
*  Microsoft Azure Bot Service に自動的に登録されるボット

> [!TIP]
> 以前に Teams アプリ プロジェクトを作成したことがない場合は、プロジェクトの詳細を[](../build-your-first-app/build-and-run.md)説明する手順に従うのが役に立つ場合があります。

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。
1. メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。
1. [機能の **追加] 画面で、[** ボット] 、[ **次へ] の順** に **選択します**。
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前であり、ローカル コンピューター上のアプリのプロジェクト ディレクトリの名前でもあります)。
1. [ボットの **構成] に移動し**、[**新しいボットの作成] を選択し、[****ボット登録の作成] を選択します**。 成功した場合、新しいボットの状態は **[** 登録済み] になります。
1. 画面 **の下部** にある [完了] を選択し、プロジェクトを作成する場所を選択します。

## <a name="2-identify-relevant-app-project-components"></a>2. 関連するアプリ プロジェクト コンポーネントを特定する

Teams を使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的にToolkit。 ボットを構築する主要なコンポーネントについて説明します。

### <a name="app-configurations"></a>アプリの構成

ボットの構成を表示または更新するには、ツールキットで **[App Studio]** を選択し、[ボット] **に移動します**。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングは、プロジェクトのルート ディレクトリにあるファイルを提供し、ボットが Teams でアクティビティを処理する方法 (たとえば、ボットが "Hello" などの特定のメッセージに応答する方法など) を処理します `botActivityHandler.js` 。

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. アプリにセキュリティで保護されたトンネルを設定する

テストの目的で、アプリをローカル Web サーバー (ポート 3978) でホストします。

1. まだインストールしていない場合は [、ngrok をインストールします](https://ngrok.com/download)。
1. ターミナルで、 を実行します `ngrok http -host-header=rewrite 3978` 。
1. Teams が HTTPS 接続を必要としますので、出力内の HTTPS URL (たとえば `https://468b9ab725e9.ngrok.io` ) をコピーします。

この URL を使用すると、Teams (HTTPS 接続が必要) は、アプリをホストしている場所 (ポート `localhost` 3978) にトンネルを接続できます。

## <a name="4-configure-your-bot"></a>4. ボットを構成する

Teams でボットを使用するには、Azure Bot Service にボットを登録する必要があります。 幸運なことに、Teams アプリケーションを使用してアプリをセットアップすると、自動的にToolkit。

引き続き、ボットに送信されるユーザー メッセージ (要求) を受信および処理するエンドポイント アドレスを指定する必要があります。 通常、URL は次のように表示されます `https://HOST_URL/api/messages` 。 この設定はツールキットですばやく構成できます。

1. [Visual Studioコード] で、左側の [アクティビティ バー] で **[Microsoft Teams]** を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し **、[Microsoft Teams** を開く] Toolkit。
1. [ボット] **>既存のボット登録に移動し、** セットアップ中に作成したボットを選択します。
1. [ **ボット エンドポイント アドレス** ] フィールドに、ボットをホストしている ngrok URL (たとえば) を入力し、 `https://468b9ab725e9.ngrok.io` ボットに `/api/messages` 追加します。<br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Teams サーバーでボット エンドポイント URL を構成できる場所を示すToolkit。":::

ボットは Teams のメッセージに応答できます。

## <a name="5-build-and-run-your-app"></a>5. アプリをビルドして実行する

ボットをホストする URL を設定し、メッセージを処理するように構成しました。 アプリを起動して実行する時間です。

1. ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、`npm install` を実行します。
1. `npm start` を実行します。

成功した場合は、ボットがアクティビティをリッスン中であることを示す次のメッセージが表示されます `localhost` 。

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. Teams でボットをサイドロードする

ボットを実行すると、Teams にインストールできます。

> [!TIP]
> 以前に Teams アプリをサイドロードし、問題が発生していない場合は、次の手順に [従います](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。

1. [Visual Studioコード] で **、F5** キーを押して Teams Web クライアントを起動します。
1. [アプリのインストール] ダイアログで、[追加] **を選択します**。 (ボットをチャネルまたはチャットに追加できますが、1 対 1 のチャットでボットをテストする場合は、他のユーザーにはあまり邪魔ではありません)。

## <a name="7-test-your-bot"></a>7. ボットをテストする

ここでは、ボットに "Hello" と言います。

1. 作成ボックスで、メッセージを送信 `Hello` します。

ボットは次のようなメッセージで返信します。

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="ユーザーが Teams ボットに 「Hello」 と答え、応答を取得するスクリーンショット。":::

## <a name="well-done"></a>よくやりましたね

お疲れさまでした。 ユーザーと 1 対 1 またはグループ設定 (チャネルとチャット) で通信できる基本的な Teams ボットがあります。

## <a name="troubleshooting"></a>トラブルシューティング

このチュートリアルの完了に問題がある場合は、次の情報が役立つ場合があります。

### <a name="bot-isnt-connected-to-teams"></a>ボットが Teams に接続されていない

アプリをインストールしたがボットが機能しない場合は、ボットが Azure Bot Service の Teams チャネルに接続 [されていることを確認 *します*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

これは Teams のチャネルと同じではないと理解することが重要です。 この場合、チャネルとは、Azure Bot Service がボットを Teams または別のサポートされている Microsoft またはサード パーティの通信アプリに接続 [する方法です](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="learn-more"></a>詳細情報

* [Teams ボットがサンプルの 1 つで実行できるその他の操作を参照する](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [ボット会話の基本](../bots/how-to/conversations/conversation-basics.md)
* シームレスな [エクスペリエンスを作成するには、](../bots/design/bots.md) 設計ガイドラインに従い、実稼働対応 [の UI](../concepts/design/design-teams-app-ui-templates.md) テンプレートを使用してビルドします。
* [Teams でのボット認証](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [ツールキットなしでボットを作成する](../resources/bot-v3/bots-create.md)
