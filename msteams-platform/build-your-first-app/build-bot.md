---
title: はじめに - ボットを構築する
author: girliemac
description: Microsoft Teams Toolkitを使用して、Microsoft Teamsボットをすばやく作成します。
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: 2cbd90b293e8ac8343febc7b3d23278d5bb5bf82
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565887"
---
# <a name="create-your-first-bot-for-teams"></a>Teams用の最初のボットを作成する

このチュートリアルでは、基本的なボット アプリを構築する方法について説明します。 ボットは、Teamsユーザーと、会話型インターフェイスを使用して Web アプリまたはサービスの間の仲介役を果たし、 ボットとチャットすることで、サービスで実行される情報をすばやく取得したり、ワークフローやタスクを開始したりできます。

## <a name="what-youll-learn"></a>あなたが学ぶこと

* Visual Studio CodeのMicrosoft Teams Toolkitを使用して、アプリ プロジェクトとボットを作成します。
* ボットに関連するTeamsアプリの構成を理解する。
* ローカル ホスト トンネリング ソリューションを使用して、ローカルでアプリをホストして実行します。
* Teamsでボットをサイドロードしてテストします。

## <a name="prerequisites"></a>前提条件

簡単なTeams アプリを設定して構築する方法を理解していることを確認します。 詳細については、[最初のMicrosoft Teams "Hello, World!" アプリを作成する](../build-your-first-app/build-and-run.md)を参照してください。 

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

Microsoft Teams Toolkitは、アプリの次のコンポーネントを設定するのに役立ちます。 

* ボット **に関連するアプリの構成とスキャフォールディング**。
* **Microsoft Azure ボット** サービスに自動的に登録されるボット。

**アプリ プロジェクトを作成するには**

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Teams Toolkitでアプリを作成する方法を示すスクリーンショット。":::

1. メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。 
1. [プロジェクトの選択] 画面で、[会話ボット] を選択します。 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Teams Toolkitで新しいボットを作成する方法を示すスクリーンショット。":::

1. [ **プロジェクトの構成]** 画面で、ボットの名前を入力します。 これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前でもあります。
1. 次の図に示すように、[**新しい**  >  **ボット作成ボット登録の作成]** を選択します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Teams Toolkitで新しいボットの名前を付けるスクリーンショット。":::

    成功した場合、新しいボットは **登録済み** ステータスになります。 これで、ボットが Microsoft Azure Bot サービスに自動的に登録されます。 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Teams Toolkitでの新しいボットの登録を示すスクリーンショット。":::

1. 画面の下部にある **[完了] を** 選択し、プロジェクトをコンピューターに保存します。  

## <a name="2-understand-your-app-project-components"></a>2. アプリ プロジェクト コンポーネントを理解する

アプリの構成とスキャフォールディングの多くは、Teams Toolkitを使用してプロジェクトを作成するときに自動的に設定されます。 ボットを構築するための主なコンポーネントを見てみましょう。

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Teams Toolkit内のプロジェクト スキャフォールディングを示すスクリーンショット。":::

別のチュートリアルでタブを作成した場合、ボットのアプリスキャフォールディングは異なります。 タブとは異なり、ボット開発では、フロントエンド Web コンポーネントを構築したり、JavaScript クライアント SDK Teamsを使用したりする必要はありません。  代わりに、スキャフォールディングは、ウェブ、モバイル、そしてもちろんTeamsで動作できるインテリジェントなエンタープライズグレードのボットを構築するためのオープンソースSDKである[Microsoft Bot Framework](https://dev.botframework.com/)を使用します。 

`botActivityHandler.js`プロジェクトのルート ディレクトリにあるファイルは、特定のメッセージに対するボットの応答など、ボットアクティビティを処理するTeams固有のハンドラーです。 アプリのスキャフォールディングは `botActivityHandler.js` 、プロジェクトのルート ディレクトリにあるファイルを提供する、特定のメッセージに対するボットの応答などのボット アクティビティを処理するTeams固有のハンドラーです。

## <a name="3-securely-expose-your-localhost-to-the-internet"></a>3. ローカルホストをインターネットに安全に公開する

`index.js`HTTP サーバーを作成し、ボットへの着信要求をリッスンするルーティングを処理するファイルを見てみましょう。 `/api/messages`は、クライアント要求に応答するためのアプリのエンドポイント URL です。 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

リクエストをボットのロジックに転送するには、 の代わりに、 など、パブリックにアクセスできる URL を設定する必要があります `https://example.com/api/messages` `https://localhost` 。 アプリは現在ローカルホストから実行されているため、ネットワークを *トンネル* する必要があります。

トンネリングは、ネットワークを介してデータを転送できるようにするプロトコルです。 ローカルホストトンネリングを使用すると、ローカルマシンとリモート接続の間の接続が提供されます。 ローカルホストをインターネットに安全に公開するには **、ngrok** というサードパーティ製ツールを使用することをお勧めします。 これにより、安全な URL が提供されます。 

1. [ngrok.com](https://ngrok.com/download)サイトにアクセスし、指示に従って、ご使用の環境にngrokをインストールして設定します。 
    
    システム PATH 環境変数にインストールしたngrok.exe ファイルへの完全パスを追加します。 正確な手順は、使用しているシェルに固有のものです。

1.  設定が完了したら、ターミナルを開いて `ngrok http -host-header=rewrite 3978` を実行します。 

    ngrok は、ポート 3978 でローカルホストに転送するパブリックで安全な URL を提供します `https://287a4f4223bc.ngrok.io` Teams。 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="ngrok を使用したローカルホストのトンネリングを示すスクリーンショット。":::

1. アプリ マニフェストに URL を登録します。 

## <a name="4-register-your-bot-endpoint"></a>4. ボットエンドポイントを登録する

Teamsでボットを使用するには、Azure Bot サービスに登録する必要があります。 これは、Teams Toolkitを使用してアプリを設定すると自動的に行われます。

ユーザー メッセージ、またはボットに送信される要求を受信および処理するエンドポイント アドレスを指定する必要があります。 通常、URL は `https://HOST_URL/api/messages` のようになります。 これは、ツールキットで構成できます。

1. Visual Studio Codeで、 **Microsoft Teams Toolkit** を開きます。
1. [**ボット**  >  **] 既存のボット登録を** 選択し、セットアップ中に作成したボットを選択します。 
1. [ **ボット エンドポイント アドレス]** フィールドに、たとえば、ボットをホストしている ngrok URL `https://287a4f4223bc.ngrok.io` を入力し、その URL に追加 `/api/messages` します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="ngrok でローカルホストをトンネルする方法を示すスクリーンショット。":::

    エンドポイントを正しく設定すると、ボットはTeamsのメッセージに応答できるようになります。 

## <a name="5-build-and-run-your-app"></a>5. アプリをビルドして実行する

ボットをホストする URL を設定し、メッセージを処理するように設定しました。 アプリを起動して実行する時間です。

1. ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、`npm install` を実行します。
1. `npm start` を実行します。

   成功した場合は、ボットがでアクティビティをリッスンしている、という次のメッセージが表示されます `localhost` 。

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. Teamsでボットをサイドロードする

ボットを実行すると、Teamsにインストールできます。

> [!TIP]
> Teamsアプリを以前にサイドロードし、問題が発生していない場合は、次の[手順](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)に従ってください。

1. Visual Studio Codeで **、F5** キーを選択して、Teams Web クライアントを起動します。
1. [アプリのインストール] ダイアログで、[ **追加**] を選択します。 

   > [!Note]
   > 既定では、アプリは 1:1 のダイレクト チャット メッセージに追加されていますが、チームにインストールするか、または [ **自分のために追加**] の横にある小さな矢印をクリックしてチャットをインストールするかを選択できます。 このチュートリアルでは、[追加] をクリックします。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="ngrok でローカル ホストをトンネリングするスクリーンショット。":::

## <a name="7-test-your-bot"></a>7. ボットをテストする

ボットに「こんにちは」と言いましょう。

* 作成ボックスで、メッセージを送信 `Hello` します。
    ボットは次のようなメッセージで返信します。

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="ユーザーがボットに「こんにちは」と答えてTeamsを示すスクリーンショット。":::

    これで、ユーザーと 1 対 1 またはグループ設定 (チャネルとチャット) 🎉と通信できる基本的なTeamsボットが作成されました。

## <a name="troubleshoot-your-bot"></a>ボットのトラブルシューティング

このチュートリアルを完了する際に問題が発生した場合は、次の情報が役立ちます。

### <a name="bot-isnt-connected-to-teams"></a>ボットがTeamsに接続されていない


アプリをインストールしてもボットが機能していない場合は、ボットが Azure Bot [サービスのTeams *チャネル* に接続](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)されていることを確認します。

これはTeamsのチャンネルと同じではないことを理解することが重要です。 この場合、チャネルとは、Azure Bot サービスがボットをTeamsまたは[サポートされている別の Microsoft またはサードパーティの通信アプリ](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)に接続する方法です。

## <a name="see-also"></a>関連項目

* [ボットの基本](../bots/bot-basics.md)
* [Microsoft Teams用の個人用タブを作成する](../build-your-first-app/build-personal-tab.md)
* [Teamsのサンプルで他に何ができるのかを確認する](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [ボット会話の基本](../bots/how-to/conversations/conversation-basics.md)
* [デザインのガイドライン](../bots/design/bots.md) 
* [プロダクション対応の UI テンプレート](../concepts/design/design-teams-app-ui-templates.md)
* [Teamsでのボット認証](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [ツールキットを使用せずにボットを作成する](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [メッセージングの拡張機能を作成する](../build-your-first-app/build-messaging-extension.md)
