---
title: チュートリアル - C を使用して最初のアプリを作成する#
description: アプリまたは .NET を使用してアプリMicrosoft TeamsをC#する方法について学習します。
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: eaa37f1ccb7944ee18bb62ae47882dc4a715b165
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566888"
---
# <a name="create-your-first-teams-app-using-c"></a>C を使用してTeamsアプリを作成する#

このチュートリアルでは、アプリを使用してアプリMicrosoft Teams作成C#。 そのためには、次のことを行う必要があります。

* 環境を準備する
* 前提条件の取得
* サンプルをダウンロードする
* サンプルの構築と実行
* サンプル アプリをホストする
* ホストされたアプリの資格情報を更新する
* [アプリ] タブの構成

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>前提条件の取得

このチュートリアルを完了するには、次のツールをインストールする必要があります。

- [Git のインストール](https://git-scm.com/downloads)
- [Visual Studio のインストール](https://www.visualstudio.com/downloads/)

無料のコミュニティ エディションの Visual Studio。 インストール中に、パスに追加するオプションがある `git` 場合は、パスを選択します。 ターミナル ウィンドウで、次のコマンドを実行してインストールを確認 `git` します。

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> プラットフォームで適切なターミナル ウィンドウを使用します。 これらの例では Git Bash を使用しますが、ほとんどのプラットフォームで実行できます。

最新バージョンの更新プログラムを開Visual Studio更新プログラムをインストールします。

このチュートリアルでは、同じターミナル ウィンドウを使用してコマンドを実行できます。

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>サンプルをダウンロードする

簡単な Hello、 [World を使い始めよう!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) サンプルをC#。 ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをコンピューターに複製します。

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> このレ[ポをフォーク](https://help.github.com/articles/fork-a-repo/)して[変更](https://github.com/OfficeDev/Microsoft-Teams-Samples)を変更し、変更を保存GitHub。

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>サンプルの構築と実行

リポジトリが複製された後、Visual Studioを使用して **Microsoft.Teams.サンプルの** **Microsoft-Teams-Samples/samples/app-hello-world/csharp** ディレクトリの Samples.HelloWorld.sln。 次に、[ビルド] **メニューから [ソリューション** のビルド **] を** 選択します。 サンプルを実行するには **、F5 キーを押するか、[** デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。

アプリが起動すると、ブラウザー ウィンドウが開き、アプリのルートが起動します。 次の URL に移動して、すべてのアプリ URL が読み込み中か確認できます。

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

<a name="HostSample"></a>

> [!Note]
> エラーが発生した場合は `Could not find a part of the path … bin\roslyn\csc.exe` 、コマンドを使用してパッケージを更新します `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。 詳細については、「スタック オーバーフロー [」のこの質問を参照してください](https://stackoverflow.com/questions/32780315)。

## <a name="host-the-sample-app"></a>サンプル アプリをホストする

アプリはMicrosoft Teams 1 つ以上の機能を提供する Web アプリケーションです。 アプリをTeamsするには、アプリをインターネットで利用できる必要があります。 これを行うには、アプリをホストする必要があります。 無料でホストするかMicrosoft Azureを使用して、コンピューター上のローカル プロセスへのトンネルを作成できます `ngrok` 。 アプリをホストした後、ルート URL (など) を `https://yourteamsapp.ngrok.io` メモします `https://yourteamsapp.azurewebsites.net` 。

### <a name="tunnel-using-ngrok"></a>Tunnel ngrok の使用

クイック テストでは、コンピューターでアプリを実行し、Web エンドポイントを介してトンネルを作成できます。 [`ngrok`](https://ngrok.com) は、 などの Web アドレスを取得できる無料のツールです `https://d0ac14a5.ngrok.io` 。 ngrok [をダウンロードしてインストール](https://ngrok.com/download) し、それを自分の場所に追加できます `PATH` 。

インストール後、 `ngrok` 新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成します。

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` インターネットからの要求をリッスンし、ポート 44327 で実行されているアプリにルーティングします。 確認するには、ブラウザーを開き、アプリの hello ページ `https://d0ac14a5.ngrok.io/hello` を読み込むに移動します。 この URL の代わりに、コンソール セッションに表示される転送 `ngrok` アドレスを使用します。

> [!NOTE]
> ビルドと実行の手順で別のポート[](#build-and-run-the-sample)を使用している場合は、同じポート番号を使用してトンネルをセットアップ `ngrok` してください。

> [!TIP]
> 別のターミナル ウィンドウで実行 `ngrok` すると良い考えです。 これは、アプリに干渉 `ngrok` することなく実行を維持するために行われます。 アプリを停止、再構築、再実行する必要があります。 セッション `ngrok` は、このウィンドウで役立つデバッグ情報を提供します。

アプリは、コンピューター上の現在のセッション中にのみ使用できます。 コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。 テスト用アプリを他のユーザーと共有する場合は、このことを覚えておいてください。 サービスを再起動する必要がある場合、アプリは新しいアドレスを返し、そのアドレスを使用する場所を更新する必要があります。 有料版には `ngrok` 、この制限はありません。

### <a name="host-in-azure"></a>Azure のホスト

Microsoft Azure共有インフラストラクチャを使用して、.NET アプリケーションを無料層でホストします。 これは、サンプルを実行するのに十分 `Hello World` です。 詳細については、「新しい無料の [Azure アカウントの作成」を参照してください](https://azure.microsoft.com/free/)。

Visual Studio Azure を含むさまざまなプロバイダーへのアプリ展開の組み込みのサポートがあります。

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>ホストされたアプリの資格情報を更新する

サンプル アプリでは、テキスト ファイルに保存した値に環境変数を設定する必要があります。

`appsettings.json` ファイルを開きます。 テキスト ファイルに保存したボット ID で **MicrosoftAppId** 値を更新します。 保存した **ボット パスワードを使用して MicrosoftAppPassword** を更新します。

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

これらの変更が行われた後、アプリを再構築します。 ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合は、アプリを再展開します。

## <a name="configure-the-app-tab"></a>[アプリ] タブの構成

アプリをチームにインストールしたら、コンテンツを表示するアプリを構成する必要があります。 サンプル アプリをインストールしたチームのチャネルに移動し **、[+]** ボタンを選択して新しいタブを追加します。[ **タブの追加] リスト** から **[Hello World] を選択** します。 構成ダイアログ ボックスが表示され、このチャネルに表示するタブを選択できます。 タブを選択し、[タブを保存する] **を** `Hello World` 選択すると、タブが読み込まれます。

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>ボットをテストTeams

これで、ボットをテストして、Teams。 アプリを登録して入力したチーム内のチャネルを選択します `@your-bot-name` 。 これはメンションと呼 **\@ ばれる.** ボットは、送信したメッセージに返信します。

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある **...** を選択します。 「Hello **World」アプリを含むメニュー** が表示されます。 選択すると、ランダムなテキストのセットが表示されます。 ランダムなテキストの 1 つを選択し、会話に挿入できます。

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

ランダムなテキストのいずれかを選択します。 独自のメッセージを使用して送信する準備が整ったカードが表示されます。

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
