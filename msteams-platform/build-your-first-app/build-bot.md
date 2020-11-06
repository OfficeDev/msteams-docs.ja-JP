---
title: 作業の開始-bot をビルドする
author: heath-hamilton
description: Microsoft Teams ツールキットを使用して、Microsoft Teams bot をすばやく作成できます。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 1229064ac6b7aab73c50048f0764c6a2353ab54a
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931741"
---
# <a name="build-a-bot-for-microsoft-teams"></a>Microsoft Teams の bot を構築する

このチュートリアルでは、基本的な *bot* アプリを構築します。 Bot は Teams ユーザーと web サービス間の仲介者として機能します。 ユーザーは bot とチャットして、サービスによって実行された情報をすばやく取得したり、ワークフローやタスクを開始したりできます。

## <a name="your-assignment"></a>自分の割り当て

Workplace は、 [タブ](../build-your-first-app/build-personal-tab.md) を使用して重要な連絡先情報を表示する Teams アプリを作成しました。 たとえば、仕事仲間は、ヘルプデスクの電話番号にすばやくアクセスできます。 しかし、通話の代わりに、ユーザーが chatbot を使用してヘルプデスクに連絡することができた場合はどうなりますか。 上司からは、Teams での基本的な会話をすばやく実行する方法を確認するように求められています。

## <a name="what-youll-learn"></a>学習内容

> [!div class="checklist"]
>
> * Microsoft Teams Toolkit for Visual Studio Code を使用してアプリプロジェクトとボットを作成する
> * Bot に関連するアプリの構成とスキャフォールディングの一部を特定する
> * アプリをローカルでホストする
> * Teams の bot を構成する
> * Teams でボットをサイドロードおよびテストする

## <a name="before-you-begin"></a>はじめに

まだお持ちでない場合は、 [Teams 開発の前提条件を理解し、インストール](build-first-app-overview.md#get-prerequisites)してください。

## <a name="1-create-your-app-project"></a>1. アプリプロジェクトを作成します。

Microsoft Teams Toolkit は、アプリ用に次のコンポーネントをセットアップするのに役に立ちます。

* **アプリの構成と** ボットに関連するスキャフォールディング
* Microsoft Azure Bot サービスに自動的に登録された **Bot**

> [!TIP]
> 以前に Teams アプリプロジェクトを作成していない場合は、 [以下の手順](../build-your-first-app/build-and-run.md) に従って、プロジェクトについて詳しく説明することをお勧めします。

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成** ] を選択します。
1. メッセージが表示されたら、Microsoft 365 開発アカウントでサインインします。
1. [ **機能の追加** ] 画面で、[ **Bot** ] を選択し、[ **次へ** ] を選択します。
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)
1. [ **Bot を構成** する] に移動して、[ **新しい bot を作成し、** **ボット登録を作成** する] を選択します。 成功した場合、新しい bot は **登録済み** の状態になります。
1. 画面の下部にある [ **完了** ] を選択し、プロジェクトを作成する場所を選択します。

## <a name="2-identify-relevant-app-project-components"></a>2. 関連するアプリプロジェクトコンポーネントを特定する

Teams ツールキットを使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。 Bot を構築するための主なコンポーネントを見てみましょう。

### <a name="app-configurations"></a>アプリの構成

Bot の構成を表示または更新するには、ツールキットで [ **App Studio** ] を選択し、[ **bot** ] に移動します。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングは、 `botActivityHandler.js` ボットが Teams でのアクティビティを処理する方法について、プロジェクトのルートディレクトリにあるファイルを提供します (たとえば、"Hello" のような特定のメッセージに bot が応答する方法)。

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. アプリへのセキュリティで保護されたトンネルをセットアップする

テストのために、アプリケーションをローカル web サーバーでホストします (ポート 3978)。

1. まだインストールしていない場合は、 [ngrok](https://ngrok.com/download)をインストールします。
1. ターミナルで、を実行 `ngrok http -host-header=rewrite 3978` します。
1. Teams で HTTPS 接続が必要になったため、出力に HTTPS URL (たとえば、) をコピーし `https://468b9ab725e9.ngrok.io` ます。

この URL を使用すると、Teams (HTTPS 接続を必要とする) は、アプリをホストしている場所にトンネルでき `localhost` ます (ポート 3978)。

## <a name="4-configure-your-bot"></a>4. bot を構成する

Teams でボットを使用するには、その bot を Azure Bot サービスに登録する必要があります。 さいわい、Teams ツールキットを使用してアプリをセットアップすると、これは自動的に実行されます。

その場合でも、bot に送信されるユーザーメッセージ (つまり、要求) を受信して処理するために、エンドポイントアドレスを指定する必要があります。 通常、URL はのように `https://HOST_URL/api/messages` なります。 これは、ツールキットですばやく構成できます。

1. Visual Studio Code で、左側のアクティビティバーで [ **Microsoft teams** ] を選択し、 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: [ **microsoft Teams ツールキットを開く** ] を選択します。
1. [ **ボット > 既存の bot 登録** ] に移動し、セットアップ時に作成した bot を選択します。
1. **Bot エンドポイントアドレス** フィールドに、bot をホストしている ngrok URL (たとえば、) を入力 `https://468b9ab725e9.ngrok.io` し `/api/messages` ます。<br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Teams ツールキットで bot エンドポイント URL を構成できる場所を示す図。":::

Bot は Teams のメッセージに応答できるようになります。

## <a name="5-build-and-run-your-app"></a>5. アプリをビルドして実行する

Bot をホストする URL を設定し、メッセージを処理するように構成します。 アプリを起動して実行します。

1. ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。
1. `npm start` を実行します。

成功した場合、ボットが自分のアクティビティをリッスンしていることを示す次のメッセージが表示され `localhost` ます。

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6 Teams での bot のサイドロード

Bot を実行している場合は、Teams にインストールできます。

> [!TIP]
> 以前に Teams アプリをサイドロードしていない場合は、以下の [手順](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)を実行します。

1. Visual Studio Code で、 **F5** キーを押して Teams web クライアントを起動します。
1. [アプリのインストール] ダイアログで、[ **追加** ] を選択します。 (Bot をチャネルやチャットに追加することはできますが、1対1のチャットで bot をテストするには他の人には邪魔されません)。

## <a name="7-test-your-bot"></a>7. bot をテストする

おもしろい部分は、次のようにしてください。 bot に "Hello" と言うことができます。

1. [新規作成] ボックスで、 `Hello` メッセージを送信します。

Bot は次のようなメッセージに返信します。

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="ユーザーが Teams の bot に &quot;Hello&quot; と言って、応答を取得することを示すスクリーンショット。":::

## <a name="well-done"></a>よくやりましたね

おめでとうございます。 ユーザーが1対1で、またはグループ設定 (チャネルとチャット) で通信できる基本的な Teams bot があります。

## <a name="troubleshooting"></a>トラブルシューティング

このチュートリアルを完了する際に問題が発生した場合は、次の情報が役立ちます。

### <a name="bot-isnt-connected-to-teams"></a>Bot が Teams に接続されていない

アプリをインストールしたが、bot が動作していない場合は、ボットが [Azure Bot サービスの Teams *チャネル* に接続](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)されていることを確認してください。

これは Teams のチャネルと同じではないことを理解しておくことが重要です。 この場合、チャネルは、Azure Bot サービスが Bot を Teams または他の [サポートされている Microsoft またはサードパーティの通信アプリ](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)に接続する方法を示しています。

## <a name="learn-more"></a>詳細情報

* [サンプルのいずれかで、他の Teams のボットができることを確認する](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [ボット会話の基本](../bots/how-to/conversations/conversation-basics.md)
* [Teams での Bot 認証](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot フレームワーク](https://dev.botframework.com/)
* [ツールキットなしでボットを作成する](../bots/how-to/create-a-bot-for-teams.md)
