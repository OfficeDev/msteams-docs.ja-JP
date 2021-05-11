---
title: '[スタート] - ボットを作成する'
author: girliemac
description: アプリを使用してMicrosoft Teamsボットをすばやく作成Microsoft Teams Toolkit。
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
# <a name="create-your-first-bot-for-teams"></a>ユーザーの最初のボットを作成Teams

このチュートリアルでは、基本的なボット アプリを構築する方法について説明します。 ボットは、会話型インターフェイスを使用Teamsユーザーと Web アプリまたはサービスの間の仲介者として機能します。 ユーザーはボットとチャットして、情報をすばやく取得したり、サービスによって実行されるワークフローやタスクを開始できます。

## <a name="what-youll-learn"></a>学習する情報

* アプリ プロジェクトとボットを作成するには、アプリ のMicrosoft Teams ToolkitをVisual Studio Code。
* ボットにTeamsするアプリ構成の説明について説明します。
* ローカル ホスト トンネリング ソリューションを使用してアプリをローカルでホストして実行します。
* アプリでボットをサイドロードしてテストTeams。

## <a name="prerequisites"></a>前提条件

簡単なアプリをセットアップしてビルドする方法を理解Teamsしてください。 詳細については[、「Hello, World!」アプリMicrosoft Teamsを作成するを参照してください](../build-your-first-app/build-and-run.md)。 

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

このMicrosoft Teams Toolkitは、アプリに対して次のコンポーネントをセットアップするのに役立ちます。 

* **ボットに関連するアプリの構成** とスキャフォールディング
* **ボット** サービスに自動的に登録Microsoft Azureボット

**アプリ プロジェクトを作成するには**

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="アプリをアプリで作成する方法を示すTeams Toolkit。":::

1. メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。 
1. [プロジェクトの選択] 画面で、[会話ボット] を選択します。 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="新しいボットを作成する方法を示すスクリーンショットをTeams Toolkit。":::

1. [プロジェクトの **構成] 画面** で、ボットの名前を入力します。 これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です。
1. 次 **の図に示すように、[ボット**  >  **登録の** 作成] を選択します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="新しいボットに名前を付ける方法を示すスクリーンショットをTeams Toolkit。":::

    成功した場合、新しいボットの状態は **[** 登録済み] になります。 これで、ボットは自動的にボット サービスMicrosoft Azure登録されます。 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="新しいボットの登録を示すスクリーンショットをTeams Toolkit。":::

1. 画面 **の下部** にある [完了] を選択し、プロジェクトをコンピューターに保存します。  

## <a name="2-understand-your-app-project-components"></a>2. アプリ プロジェクト コンポーネントについて

アプリの構成とスキャフォールディングの多くが、プロジェクトを作成するときに自動的に設定Teams Toolkit。 ボットを構築する主なコンポーネントを見てみ取る:

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="プロジェクトのスキャフォールディングを示すスクリーンショットをTeams Toolkit。":::

別のチュートリアルでタブを作成した場合、ボットのアプリスキャフォールディングは異なります。 タブとは異なり、ボットの開発では、フロントエンド Web コンポーネントをビルドしたり、JavaScript クライアント SDK のTeams必要としたりすることはできません。  代わりに、スキャフォールディングは[Microsoft Bot Framework](https://dev.botframework.com/)を使用します。これは、Web、モバイル、およびもちろんモバイルで動作するインテリジェントなエンタープライズ レベルのボットを構築するオープンソース SDK Teams です。 

プロジェクトのルート ディレクトリにあるファイルは、ボットが特定のメッセージに応答する方法など、ボットアクティビティを処理する Teams 固有のハンドラー `botActivityHandler.js` です。 アプリのスキャフォールディングは、プロジェクトのルート ディレクトリにあるファイルを提供し、ボットが特定のメッセージに応答する方法などのボット アクティビティを処理する Teams 固有のハンドラー `botActivityHandler.js` です。

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

    ngrok は、ポート 3978 でローカル ホストに転送するパブリックで安全な URL を提供します。そのため、次のスクリーンショットに示すように、https URL をコピーします。Teams では HTTPS 接続が必要です `https://287a4f4223bc.ngrok.io` 。 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="ngrok を使用した localhost のトンネリングを示すスクリーンショット。":::

1. アプリ マニフェストに URL を登録します。 

## <a name="4-register-your-bot-endpoint"></a>4. ボット エンドポイントを登録する

ボットを使用するには、Teams Azure Bot Service に登録する必要があります。 これは、アプリを使用してアプリをセットアップするときに自動的にTeams Toolkit。

引き続き、ボットに送信されるユーザー メッセージ (要求) を受信および処理するエンドポイント アドレスを指定する必要があります。 通常、URL は次のように表示されます `https://HOST_URL/api/messages` 。 この設定はツールキットですばやく構成できます。

1. [Visual Studio Code]**を開** Microsoft Teams Toolkit。
1. [**ボット]**  >  **[既存のボット登録] を選択し**、セットアップ時に作成したボットを選択します。 
1. [ **ボット エンドポイント アドレス** ] フィールドに、ボットをホストしている ngrok URL を入力し、その URL `https://287a4f4223bc.ngrok.io` に `/api/messages` 追加します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="ngrok を使用して localhost をトンネリングする方法を示すスクリーンショット。":::

    エンドポイントを正しく設定した後、ボットは Teamsメッセージに応答できます。 

## <a name="5-build-and-run-your-app"></a>5. アプリをビルドして実行する

ボットをホストする URL を設定し、メッセージを処理するように構成しました。 アプリを起動して実行する時間です。

1. ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、`npm install` を実行します。
1. `npm start` を実行します。

   成功した場合は、ボットがアクティビティをリッスン中であることを示す次のメッセージが表示されます `localhost` 。

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. ボットをサイドロードTeams

ボットを実行している場合は、ボットをインストールTeams。

> [!TIP]
> 以前にアプリをサイドロードTeams問題が発生していない場合は、次の手順に[従います](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。

1. [Visual Studio Code **F5** キーを選択して、Web クライアントTeams起動します。
1. [アプリのインストール] ダイアログで、[追加] **を選択します**。 

   > [!Note]
   > 既定では、アプリは 1:1 ダイレクト チャット メッセージに追加されます。ただし、[追加] の横にある小さな矢印をクリックして、チームまたはチャットにインストール **することもできます。** このチュートリアルでは、[追加] をクリックします。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="ngrok を使用したローカル ホストのトンネリングを示すスクリーンショット。":::

## <a name="7-test-your-bot"></a>7. ボットをテストする

ボットに "Hello" と言います。

* 作成ボックスで、メッセージを送信 `Hello` します。
    ボットは次のようなメッセージで返信します。

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="ユーザーがボットに 「Hello」 と答え、応答Teams示すスクリーンショット。":::

    これで、ユーザーと 1 対 1 またはグループ設定 (チャネルとチャット) でユーザーと通信できる基本的な Teams ボットを作成しました🎉

## <a name="troubleshoot-your-bot"></a>ボットのトラブルシューティング

このチュートリアルの完了に問題がある場合は、次の情報が役立つ場合があります。

### <a name="bot-isnt-connected-to-teams"></a>ボットがデバイスに接続Teams


アプリをインストールしたがボットが機能しない場合は、ボットが Azure Bot Service のサービス チャネルに接続されていることを [Teams *してください*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

これは、チャネルと同じではないと理解することが重要Teams。 この場合、チャネルとは、Azure Bot Service がボットを他の microsoft またはサード パーティの通信アプリTeamsに接続する[方法です](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="see-also"></a>関連項目

* [ボットの基本](../bots/bot-basics.md)
* [ユーザーの個人用タブを作成Microsoft Teams](../build-your-first-app/build-personal-tab.md)
* [1 つのサンプルTeamsボットが実行できる他の操作を参照する](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [ボット会話の基本](../bots/how-to/conversations/conversation-basics.md)
* [デザインのガイドライン](../bots/design/bots.md) 
* [実稼働対応の UI テンプレート](../concepts/design/design-teams-app-ui-templates.md)
* [ボット認証 (Teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [ツールキットなしでボットを作成する](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [メッセージングの拡張機能を作成する](../build-your-first-app/build-messaging-extension.md)
