---
title: チュートリアル - C を使用して最初のアプリを作成する#
description: アプリまたは .NET を使用してアプリMicrosoft TeamsをC#する方法について学習します。
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.localizationpriority: medium
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 9e830b6681797fcac032c2345a56163e634c446c
ms.sourcegitcommit: 6573881f7e69d8e5ec8861f54df84e7d519f0511
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2021
ms.locfileid: "60096694"
---
# <a name="build-your-first-teams-app-using-c"></a>C を使用してTeamsアプリをビルドする#

このチュートリアルでは、.NET またはアプリを使用して最初のアプリをMicrosoft Teamsする方法をC#。 また、以下の手順を実行します。

1. [環境を準備する](#prepare-your-environment)
1. [前提条件の取得](#GetPrerequisites)
1. [サンプルをダウンロードする](#DownloadSample)
1. [サンプルのビルドと実行](#BuildRun)
1. [サンプル アプリをホストする](#hostsample)
1. [ホストされたアプリの資格情報を更新する](#updatecredentials)
1. [[アプリ] タブの構成](#configureapptab)

<a name="prepare-your-environment"></a>
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

サンプルは、複製後にビルドして実行できます。 

**複製されたサンプルをビルドして実行するには**

1. ソリューション ファイル **Microsoft.Teams を開きます。サンプルの** **Microsoft-Teams-Samples/samples/app-hello-world/csharp** ディレクトリの Samples.HelloWorld.sln。
1. [ビルド **] メニューから [** ソリューションの **ビルド] を** 選択します。
1. **F5 キーを選択** するか、[**デバッグ]** メニューから [デバッグの開始] を **選択** してサンプルを実行します。

    アプリが起動すると、ブラウザー ウィンドウが開き、アプリのルートが起動します。 次の URL に移動して、すべてのアプリ URL が読み込み中か確認できます。

    - `https://localhost:44327/`
    - `https://localhost:44327/hello`
    - `https://localhost:44327/first`
    - `https://localhost:44327/second`

    > [!Note]
    > エラーが発生した場合は `Could not find a part of the path … bin\roslyn\csc.exe` 、コマンドを使用してパッケージを更新します `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。 詳細については、「スタック オーバーフロー [」のこの質問を参照してください](https://stackoverflow.com/questions/32780315)。

    <a name="hostsample"></a>
    ## <a name="deploy-your-sample-app"></a>サンプル アプリの展開

    アプリはMicrosoft Teams 1 つ以上の機能を提供する Web アプリケーションです。 アプリをTeamsするには、アプリをインターネットで利用できる必要があります。 これを行うには、アプリをホストする必要があります。 無料でホストするかMicrosoft Azureを使用して、コンピューター上のローカル プロセスへのトンネルを作成できます `ngrok` 。 アプリをホストした後、ルート URL (またはなど) をメモ `https://yourteamsapp.ngrok.io` します `https://yourteamsapp.azurewebsites.net` 。

### <a name="tunnel-using-ngrok"></a>Tunnel ngrok の使用

クイック テストでは、コンピューターでアプリを実行し、Web エンドポイントを介してトンネルを作成できます。 [`ngrok`](https://ngrok.com) は、 などの Web アドレスを取得できる無料のツールです `https://d0ac14a5.ngrok.io` 。 ngrok [をダウンロードしてインストール](https://ngrok.com/download) し、それを自分の場所に追加できます `PATH` 。

インストール後、 `ngrok` 新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成します。

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` インターネットからの要求に応答し、ポート 44327 で実行されているアプリにルーティングします。 

**応答を確認するには**

1. ブラウザーを開き、`https://d0ac14a5.ngrok.io/hello` に移動します。 これにより、アプリの Hello ページが読み込まれる。
1. 手順 1 で説明した URL の代わりに、コンソール セッションに表示される転送 `ngrok` アドレスを使用します。
    > [!NOTE]
    > ビルドと実行の手順で別のポート[](#build-and-run-the-sample)を使用している場合は、同じポート番号を使用してトンネルをセットアップ `ngrok` してください。
    > [!TIP]
    > 別のターミナル ウィンドウで実行 `ngrok` すると良い考えです。 これは、アプリに干渉 `ngrok` することなく実行を維持するために行われます。 アプリを停止、再構築、再実行する必要があります。 セッション `ngrok` は、このウィンドウで役立つデバッグ情報を提供します。

    アプリは、コンピューター上の現在のセッション中にのみ使用できます。 コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。 テスト用アプリを他のユーザーと共有する場合は、このことを覚えておいてください。 サービスを再起動する必要がある場合、アプリは新しいアドレスを返し、そのアドレスを使用する場所を更新する必要があります。 有料版には `ngrok` 、この制限はありません。

### <a name="host-in-azure"></a>Azure のホスト

Microsoft Azure共有インフラストラクチャを使用して、.NET アプリケーションを無料層でホストします。 これは、サンプルを実行するのに十分 `Hello World` です。 詳細については、「新しい無料の [Azure アカウントの作成」を参照してください](https://azure.microsoft.com/free/)。

Visual Studio Azure を含むさまざまなプロバイダーへのアプリ展開の組み込みのサポートがあります。

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

**アプリ パッケージを更新する**

> [!NOTE]
>  App Studio は間もなく奪われる予定です。 新しい開発者ポータルを使用して、Teamsアプリを構成、配布、[および管理します](https://dev.teams.microsoft.com/)。

# <a name="app-studio"></a>[App Studio](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[開発者ポータル](#tab/DP)

**開発者ポータル (プレビュー) でアプリ パッケージを構成するには、Teams**


1. 1.開発者ポータル **[に移動します](https://dev.teams.microsoft.com/)**。

     <img width="600px" alt="Screenshot of TDP" src="~/assets/images/tdp/tdp_home_1.png"/>

1. [アプリ] に **移動します**。

    <img width="600px" alt="Open Apps" src="~/assets/images/tdp/screen2.png"/>

1. [既存 **のアプリをインポートする] を選択します**。

    <img width="600px" alt="Screenshot of import app in tdp" src="~/assets/images/tdp/screen3.png"/>

1. [Hello **World] を選択し** 、[インポート] **を選択します**。 **Hello World アプリ** は開発者ポータルにインポートされます。 

    開発者ポータルを使用してアプリTeamsできます。 マニフェストは [配布] の下に表示されます。 マニフェストを使用して、アプリの機能、必要なリソース、その他の重要な属性を構成できます。 開発者ポータルを使用してアプリを構成する方法の詳細については、「開発者ポータル」[を参照Teamsしてください](../concepts/build-and-test/teams-developer-portal.md)。

    <img width="600px" alt="Screenshot of configure tdp" src="~/assets/images/tdp/Screen4.png"/>
---

<a name="updatecredentials"></a>
## <a name="update-the-credentials-for-your-hosted-app"></a>ホストされたアプリの資格情報を更新する

サンプル アプリでは、テキスト ファイルに保存した値に環境変数を設定する必要があります。

**ホストされているアプリの資格情報を更新するには**

1. `appsettings.json` ファイルを開きます。 
1. テキスト ファイルに保存したボット ID で **MicrosoftAppId** 値を更新します。 
1. 保存した **ボット パスワードを使用して MicrosoftAppPassword** を更新します。

    <img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

    これらの変更が行われた後、アプリを再構築します。 ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合は、アプリを再展開します。

<a name="configureapptab"></a>
## <a name="configure-the-app-tab"></a>[アプリ] タブの構成

アプリをチームにインストールしたら、コンテンツを表示するためにアプリを構成する必要があります。 

**アプリ タブを構成するには**

1. サンプル アプリをインストールしたチームのチャネルに移動し **、[+]** ボタンを選択して新しいタブを追加します。
1. [ **タブの追加] リスト** から **[Hello World] を選択** します。 構成ダイアログ ボックスが表示され、このチャネルに表示するタブを選択できます。 
1. **[保存]** を選択します。 タブ `Hello World` はタブと一緒に読み込まれます。

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>ボットをテストTeams

これで、ボットをテストできます。Teams。 

**ボットをテストするには**

* アプリを登録して入力したチーム内のチャネルを選択します `@your-bot-name` 。 これはメンションと呼 **\@ ばれる.** ボットは、送信したメッセージに返信します。

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

**メッセージング拡張機能をテストするには**
1. 会話ビューの入力ボックスの下にある **[...]** を選択します。 「Hello **World」アプリを含むメニュー** が表示されます。 
1. メニューを選択すると、ランダムなテキストのセットが表示されます。 ランダムなテキストの 1 つを選択し、会話に挿入できます。

    <img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. ランダムなテキストのいずれかを選択します。 独自のメッセージを使用して送信する準備が整ったカードが表示されます。

    <img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

## <a name="see-also"></a>関連項目

* [チュートリアルの概要](code-samples.md)
* [会話ボット アプリを作成する](first-app-bot.md)
* [メッセージング拡張機能を作成する](first-message-extension.md)
* [コード サンプル](https://github.com/OfficeDev/Microsoft-Teams-Samples)
