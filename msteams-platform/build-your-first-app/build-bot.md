---
title: '[スタート] - ボットを作成する'
author: girliemac
description: Microsoft Teams ボットを使用して Microsoft Teams ボットをすばやく作成Toolkit。
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: dbb6f0a2497a0914d8e14473f1dbd6b2b225fc96
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068631"
---
# <a name="create-your-first-bot-for-teams"></a>Teams 用の最初のボットを作成する

このチュートリアルでは、基本的なボット アプリを構築する方法について説明します。 ボットは、Teams ユーザーと会話型インターフェイスを使用した Web アプリまたはサービス間の仲介として機能します。 ユーザーはボットとチャットして、情報をすばやく取得したり、サービスによって実行されるワークフローやタスクを開始できます。

## <a name="what-youll-learn"></a>学習する情報

* Microsoft Teams を使用してアプリ プロジェクトとボットを作成し、ToolkitコードVisual Studioします。
* ボットに関連する Teams アプリの構成について理解します。
* ローカル ホスト トンネリング ソリューションを使用してアプリをローカルでホストして実行します。
* Teams でボットをサイドロードしてテストします。

## <a name="prerequisites"></a>前提条件

簡単な Teams アプリをセットアップしてビルドする方法を理解してください。 詳細については、「Hello, World!」アプリの最初の Microsoft Teams の作成 [に関するページをご覧ください](../build-your-first-app/build-and-run.md)。 

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

Microsoft Teams Toolkitは、アプリの次のコンポーネントをセットアップするのに役立ちます。 

* **ボットに関連するアプリの構成** とスキャフォールディング
*  Microsoft Azure Bot Service に自動的に登録されるボット

**アプリ プロジェクトを作成するには**

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Teams アプリケーションでアプリを作成する方法を示すスクリーンショットToolkit。":::

1. メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。 
1. [プロジェクトの選択] 画面で、[会話ボット] を選択します。 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Teams サーバーで新しいボットを作成する方法を示すスクリーンショットToolkit。":::

1. [プロジェクトの **構成] 画面** で、ボットの名前を入力します。 これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です。
1. 次 **の図に示すように、[ボット**  >  **登録の** 作成] を選択します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Teams アプリケーションで新しいボットに名前を付けるToolkit。":::

    成功した場合、新しいボットの状態は **[** 登録済み] になります。 これで、ボットが Microsoft Azure Bot Service に自動的に登録されます。 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Teams サーバーに新しいボットを登録するToolkit。":::

1. 画面 **の下部** にある [完了] を選択し、プロジェクトをコンピューターに保存します。  

## <a name="2-understand-your-app-project-components"></a>2. アプリ プロジェクト コンポーネントについて

Teams を使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的にToolkit。 ボットを構築する主なコンポーネントを見てみ取る:

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Teams のプロジェクト スキャフォールディングを示すスクリーンショットToolkit。":::

別のチュートリアルでタブを作成した場合、ボットのアプリスキャフォールディングは異なります。 タブとは異なり、ボットの開発では、フロントエンド Web コンポーネントをビルドしたり、Teams JavaScript クライアント SDK を使用する必要は一切ない。  代わりに、スキャフォールディングは [Microsoft Bot Framework](https://dev.botframework.com/)を使用します。これは、Web、モバイル、およびもちろん Teams で動作するインテリジェントなエンタープライズ レベルのボットを構築するオープンソース SDK です。 

プロジェクトのルート ディレクトリにあるファイルは、ボットが特定のメッセージに応答する方法など、ボットアクティビティを処理する Teams 固有の `botActivityHandler.js` ハンドラーです。 アプリのスキャフォールディングは、プロジェクトのルート ディレクトリにあるファイルを提供し、ボットが特定のメッセージに応答する方法などのボット アクティビティを処理する Teams 固有のハンドラー `botActivityHandler.js` です。

## <a name="3-securely-expose-your-localhost-to-the-internet"></a>3. localhost をインターネットに安全に公開する

HTTP サーバーを作成し、ボットへの受信要求をリッスンするルーティングを処理するファイル `index.js` を確認します。 クライアント `/api/messages` 要求に応答するアプリのエンドポイント URL を次に示します。 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

ボットのロジックに要求を転送するには、. `https://example.com/api/messages` `https://localhost` アプリは現在 localhost から実行されているので、ネットワークを *トンネリングする* 必要があります。

トンネリングは、ネットワーク間でデータを転送できるプロトコルです。 localhost トンネリングを使用すると、ローカル コンピューターとリモート接続間の接続が提供されます。 localhost をインターネットに安全に公開するには **、ngrok** というサードパーティ製のツールを使用することをお勧めします。 これにより、セキュリティで保護された URL が提供されます。 

1. サイトに移動 [ngrok.com](https://ngrok.com/download) 指示に従って、環境に ngrok をインストールしてセットアップします。 
    
    システム PATH 環境変数にインストールngrok.exeファイルへの完全パスを追加します。 正確な手順は、使用しているシェルに固有です。

1.  セットアップが完了したら、ターミナルを開いて実行します `ngrok http -host-header=rewrite 3978` 。 

    次に、ngrok はポート 3978 でローカル ホストに転送するパブリックで安全な URL を提供します。Teams では HTTPS 接続が必要なので、次のスクリーンショットに示すように HTTPS URL をコピーします `https://287a4f4223bc.ngrok.io` 。 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="ngrok を使用した localhost のトンネリングを示すスクリーンショット。":::

1. アプリ マニフェストに URL を登録します。 

## <a name="4-register-your-bot-endpoint"></a>4. ボット エンドポイントを登録する

Teams でボットを使用するには、Azure Bot Service にボットを登録する必要があります。 これは、Teams アプリケーションを使用してアプリをセットアップするときに自動的にToolkit。

引き続き、ボットに送信されるユーザー メッセージ (要求) を受信および処理するエンドポイント アドレスを指定する必要があります。 通常、URL は次のように表示されます `https://HOST_URL/api/messages` 。 この設定はツールキットですばやく構成できます。

1. [Visual Studioコード] で **、[Microsoft Teams] を開Toolkit。**
1. [**ボット]**  >  **[既存のボット登録] を選択し**、セットアップ時に作成したボットを選択します。 
1. [ **ボット エンドポイント アドレス** ] フィールドに、ボットをホストしている ngrok URL を入力し、その URL `https://287a4f4223bc.ngrok.io` に `/api/messages` 追加します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="ngrok を使用して localhost をトンネリングする方法を示すスクリーンショット。":::

    エンドポイントを正しくセットアップした後、ボットは Teams のメッセージに応答できます。 

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

1. [Visual Studioコード] で **、F5** キーを選択して Teams Web クライアントを起動します。
1. [アプリのインストール] ダイアログで、[追加] **を選択します**。 

   > [!Note]
   > 既定では、アプリは 1:1 ダイレクト チャット メッセージに追加されます。ただし、[追加] の横にある小さな矢印をクリックして、チームまたはチャットにインストール **することもできます。** このチュートリアルでは、[追加] をクリックします。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="ngrok を使用したローカル ホストのトンネリングを示すスクリーンショット。":::

## <a name="7-test-your-bot"></a>7. ボットをテストする

ボットに "Hello" と言います。

* 作成ボックスで、メッセージを送信 `Hello` します。
    ボットは次のようなメッセージで返信します。

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="ユーザーが Teams ボットに 「Hello」 と答え、応答を取得するスクリーンショット。":::

    これで、ユーザーと 1 対 1 またはグループ設定 (チャネルとチャット) で通信できる基本的な Teams ボットを作成🎉

## <a name="troubleshoot-your-bot"></a>ボットのトラブルシューティング

このチュートリアルの完了に問題がある場合は、次の情報が役立つ場合があります。

### <a name="bot-isnt-connected-to-teams"></a>ボットが Teams に接続されていない


アプリをインストールしたがボットが機能しない場合は、ボットが Azure Bot Service の Teams チャネルに接続 [されていることを確認 *します*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

これは Teams のチャネルと同じではないと理解することが重要です。 この場合、チャネルとは、Azure Bot Service がボットを Teams または別のサポートされている Microsoft またはサード パーティの通信アプリに接続 [する方法です](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="see-also"></a>関連項目

* [ボットの基本](../bots/bot-basics.md)
* [Microsoft Teams の個人用タブを作成する](../build-your-first-app/build-personal-tab.md)
* [Teams ボットがサンプルの 1 つで実行できるその他の操作を参照する](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [ボット会話の基本](../bots/how-to/conversations/conversation-basics.md)
* [デザインのガイドライン](../bots/design/bots.md) 
* [実稼働対応の UI テンプレート](../concepts/design/design-teams-app-ui-templates.md)
* [Teams でのボット認証](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [ツールキットなしでボットを作成する](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [メッセージングの拡張機能を作成する](../build-your-first-app/build-messaging-extension.md)
