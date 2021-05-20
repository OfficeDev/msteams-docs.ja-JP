---
title: チュートリアル - C を使用して最初のアプリを作成します。#
description: C# または .NET を使用してMicrosoft Teams アプリの構築を開始する方法について説明します。
keywords: .net c# csharp の開始
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
# <a name="create-your-first-teams-app-using-c"></a>C を使用して最初のTeams アプリを作成する#

このチュートリアルでは、C# を使用してMicrosoft Teamsアプリを作成する方法について説明します。 そのためには、次のことを行う必要があります。

* 環境を準備する
* 前提条件の取得
* サンプルをダウンロードする
* サンプルの構築と実行
* サンプル アプリをホストする
* ホストされたアプリの資格情報を更新する
* アプリ タブを構成する

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>前提条件の取得

このチュートリアルを完了するには、次のツールをインストールする必要があります。

- [Git をインストールする](https://git-scm.com/downloads)
- [Visual Studio のインストール](https://www.visualstudio.com/downloads/)

無料のコミュニティ版のVisual Studioをインストールできます。 インストール中にパスに追加するオプションがある場合 `git` は、パスを選択します。 ターミナル ウィンドウで、次のコマンドを実行してインストールを確認 `git` します。

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> プラットフォーム上で適切なターミナルウィンドウを使用します。 これらの例では Git Bash を使用していますが、ほとんどのプラットフォームで実行できます。

最新バージョンのVisual Studioを開き、更新プログラムをインストールします。

同じターミナル ウィンドウを使用して、このチュートリアルのコマンドを実行できます。

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>サンプルをダウンロードする

あなたは簡単な [こんにちは、世界で始めることができます!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) C# のサンプル。 ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをコンピューターに複製します。

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> この[レポ](https://github.com/OfficeDev/Microsoft-Teams-Samples)[をフォーク](https://help.github.com/articles/fork-a-repo/)して変更を変更し、GitHubに保存することができます。

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>サンプルの構築と実行

リポジトリの複製が作成されたら、Visual Studioを使用してソリューション ファイル **Microsoft.Teamsを開きます。サンプルの****マイクロソフトTeamsサンプル/サンプル/アプリ-hello-world/csharp** ディレクトリから.sln。 次に、[ビルド] メニューの **[ソリューションのビルド** ] **を選択** します。 サンプルを実行するには **、F5** キーを押すか、[**デバッグ**] メニューから **[デバッグの開始**] を選択します。

アプリが起動すると、起動したアプリのルートを示すブラウザー ウィンドウが開きます。 次の URL に移動して、すべてのアプリ URL が読み込まれているかどうかを確認できます。

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

<a name="HostSample"></a>

> [!Note]
> エラーが表示された場合は、 `Could not find a part of the path … bin\roslyn\csc.exe` コマンドを使用してパッケージを更新 `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` します。 詳細については、 [この「スタック オーバーフロー」の質問を](https://stackoverflow.com/questions/32780315)参照してください。

## <a name="host-the-sample-app"></a>サンプル アプリをホストする

Microsoft Teamsのアプリは、1 つ以上の機能を提供する Web アプリケーションです。 Teams プラットフォームでアプリを読み込むには、アプリがインターネット上で利用可能である必要があります。 これを行うには、アプリをホストする必要があります。 無料でホストMicrosoft Azure、または を使用してコンピュータ上のローカル プロセスへのトンネルを作成することができます `ngrok` 。 アプリをホストしたら、そのルート URL (または など) `https://yourteamsapp.ngrok.io` `https://yourteamsapp.azurewebsites.net` をメモします。

### <a name="tunnel-using-ngrok"></a>ngrok を使用したTunnel

迅速なテストを行うために、コンピューターでアプリを実行し、Web エンドポイントを介してアプリへのトンネルを作成できます。 [`ngrok`](https://ngrok.com) は、Web アドレスを取得できる無料ツールです `https://d0ac14a5.ngrok.io` 。 ngrok [をダウンロードしてインストール](https://ngrok.com/download) し、それを `PATH` .

をインストールした後 `ngrok` 、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成します。

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` インターネットからのリクエストをリッスンし、ポート 44327 で実行されているアプリにルーティングします。 確認するには、ブラウザーを開き、 `https://d0ac14a5.ngrok.io/hello` に移動してアプリの hello ページを読み込みます。 この URL の代わりに、コンソール セッションで表示される転送先アドレス `ngrok` を使用します。

> [!NOTE]
> [ビルドと実行](#build-and-run-the-sample)の手順で別のポートを使用している場合は、トンネルをセットアップするのに同じポート番号を使用することを確認します `ngrok` 。

> [!TIP]
> 別のターミナル ウィンドウで実行することをお勧めします `ngrok` 。 これは、 `ngrok` アプリに干渉することなく実行されないようにするために行われます。 アプリを停止、再構築、再実行する必要があります。 `ngrok`セッションは、このウィンドウでデバッグに役立つ情報を提供します。

アプリは、コンピューター上の現在のセッション中にのみ使用できます。 マシンがシャットダウンまたはスリープ状態になった場合、サービスは利用できなくなります。 テスト用のアプリを他のユーザーと共有する場合は、この点に注意してください。 サービスを再起動する必要がある場合は、アプリは新しいアドレスを返し、そのアドレスを使用するすべての場所を更新する必要があります。 有料版のの場合 `ngrok` 、この制限はありません。

### <a name="host-in-azure"></a>Azure でホストする

Microsoft Azureは、共有インフラストラクチャを使用して、無料のレベルで .NET アプリケーションをホストします。 この方法でサンプルを実行できます `Hello World` 。 詳細については、「 [無料の Azure アカウントを新しく作成する](https://azure.microsoft.com/free/)」を参照してください。

Visual Studioには、Azure を含むさまざまなプロバイダーへのアプリのデプロイが組み込まれています。

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>ホストされたアプリの資格情報を更新する

サンプル アプリでは、テキスト ファイルに保存した値に設定する環境変数が必要です。

`appsettings.json` ファイルを開きます。 テキスト ファイルに保存したボット ID で **MicrosoftAppId** 値を更新します。 保存したボット **パスワードでアプリ パスワード** を更新します。

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

これらの変更が行われた後、アプリを再構築します。 ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合はアプリを再デプロイします。

## <a name="configure-the-app-tab"></a>アプリ タブを構成する

チームにアプリをインストールしたら、コンテンツを表示するように構成する必要があります。 サンプル アプリをインストールしたチームのチャンネルに移動し **、[+]** ボタンを選択して新しいタブを追加します。**[タブの追加]** ボックスの一覧から **[Hello World]** を選択します。 このチャネルに表示するタブを選択できる構成ダイアログ ボックスが表示されます。 タブを選択し、[ **保存]** を選択すると `Hello World` 、タブがタブに読み込まれます。

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Teamsでボットをテストする

これで、Teamsでボットをテストできます。 アプリを登録したチームのチャンネルを選択し、「 」と入力 `@your-bot-name` します。 これはメンションと呼 **\@ ばれます**。 ボットは、送信したメッセージに返信します。

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある **[.]** を選択します。 **「ハローワールド」** アプリを使ったメニューが表示されます。 選択すると、ランダムなテキストのセットが表示されます。 ランダムテキストの 1 つを選択して、会話に挿入できます。

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

ランダムテキストの 1 つを選択します。 独自のメッセージを使用してフォーマットされ、送信できる状態のカードが表示されます。

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
