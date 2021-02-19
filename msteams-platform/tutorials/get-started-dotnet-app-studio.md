---
title: チュートリアル - C を使用して最初のアプリを作成する#
description: C# または .NET を使用して Microsoft Teams アプリの構築を開始する方法について説明します。
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 29cc4e0f434bf9ece9c6073af84627acc048b628
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294755"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a>C# または .NET を使用して最初の Teams アプリを作成する

このチュートリアルでは、C# または .NET を使用して Microsoft Teams アプリを作成できます。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>前提条件の取得

このチュートリアルを完了するには、次のツールを取得する必要があります。

- [Git のインストール](https://git-scm.com/downloads)
- [インストールVisual Studio.](https://www.visualstudio.com/downloads/) 無料のコミュニティ エディションをインストールできます。

インストール中に、PATH に追加するオプションがある `git` 場合は、それを選択します。

ターミナル ウィンドウで、次のコマンドを実行してインストールを確認 `git` します。

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> プラットフォームで適切なターミナル ウィンドウを使用します。 これらの例では Bash を使用しますが、ほとんどのプラットフォームで実行されます。

更新プログラムの最新バージョンを起動しVisual Studioインストールしてください。

このチュートリアルでは、同じターミナル ウィンドウを使用してコマンドを実行できます。

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>サンプルをダウンロードする

簡単な Hello、 [World を使い始めよう!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) C# のサンプル。 ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをローカル コンピューターに複製します。

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> このリポジトリ [をフォーク](https://help.github.com/articles/fork-a-repo/) して [変更](https://github.com/OfficeDev/Microsoft-Teams-Samples) を変更し、GitHub に保存して参照することができます。

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>サンプルの構築と実行

リポジトリを複製した後、Visual Studio を使用して、サンプルの `Microsoft.Teams.Samples.HelloWorld.sln` **Microsoft-Teams-Samples/samples/app-hello-world/csharp** ディレクトリからソリューション ファイルを開き、メニューから選択します `Build Solution` `Build` 。 サンプルを実行するには、メニュー `F5` を押す `Start Debugging` または選択 `Debug` します。

アプリが起動すると、ブラウザー ウィンドウが開き、アプリのルートが起動します。 次の URL に移動して、すべてのアプリ URL が読み込み中か確認できます。

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second]https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> エラーが発生した場合は `Could not find a part of the path … bin\roslyn\csc.exe` 、コマンドを使用してパッケージを更新します `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。 詳細については [、StackOverflow のこの質問を参照してください](https://stackoverflow.com/questions/32780315)。

## <a name="host-the-sample-app"></a>サンプル アプリをホストする

Microsoft Teams のアプリは、1 つ以上の機能を提供する Web アプリケーションです。 Teams プラットフォームでアプリを読み込むには、アプリにインターネットからアクセスできる必要があります。 インターネットからアプリにアクセスするには、アプリをホストする必要があります。 Microsoft Azure で無料でホストするか、開発マシンのローカル プロセスへのトンネルを作成します `ngrok` 。 アプリのホストが完了したら、そのルート URL に注意してください。 たとえば、`https://yourteamsapp.ngrok.io` または `https://yourteamsapp.azurewebsites.net` などです。

### <a name="tunnel-using-ngrok"></a>ngrok を使用したトンネル

クイック テストでは、ローカル コンピューターでアプリを実行し、Web エンドポイントを介してトンネルを作成できます。 [ngrok](https://ngrok.com) は、次のような Web アドレスを取得できる無料のツールです `https://d0ac14a5.ngrok.io` 。 ngrok [をダウンロードして](https://ngrok.com/download) インストールできます。 必ず、このファイルを自分の場所に追加してください `PATH` 。

ngrok をインストールした後、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成します。

```bash
ngrok http 44327 -host-header=localhost:44327
```

このサンプルでは、ポート 44327 を使用します。必ず指定してください。

Ngrok はインターネットからの要求をリッスンし、ポート 44327 で実行されているアプリにルーティングします。 確認するには、ブラウザーを開き、アプリの hello ページ `https://d0ac14a5.ngrok.io/hello` を読み込むに移動します。 この URL の代わりに、コンソール セッションで ngrok によって表示される転送アドレスを使用します。

> [!NOTE]
> ビルドと実行の手順で別のポート[](#build-and-run-the-sample)を使用している場合は、同じポート番号を使用してトンネルをセットアップ `ngrok` してください。

> [!TIP]
> 別のターミナル ウィンドウで実行 `ngrok` すると良い考えです。 これは、停止、再構築、再実行が必要なアプリに干渉することなく ngrok を実行し続ける場合に行います。 セッション `ngrok` は、このウィンドウで役立つデバッグ情報を提供します。

アプリは、開発マシン上の現在のセッション中にのみ使用できます。 コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。 テスト用アプリを他のユーザーと共有する場合は、このことを覚えておいてください。 サービスを再起動する必要がある場合、アプリは新しいアドレスを返し、そのアドレスを使用する場所を更新する必要があります。 有料バージョンの ngrok には、この制限はありません。

### <a name="host-in-azure"></a>Azure のホスト

Microsoft Azure は、共有インフラストラクチャを使用して無料層で .NET アプリケーションをホストします。 これは、サンプルを実行するのに十分 `Hello World` です。 詳細については、「新しい無料アカウント [の作成」を参照してください](https://azure.microsoft.com/free/)。

Visual Studio Azure を含むさまざまなプロバイダーへのアプリ展開の組み込みのサポートがあります。

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>ホストされたアプリの資格情報を更新する

サンプル アプリでは、前にメモした値に次の環境変数を設定する必要があります。

ファイルのappsettings.js開きます。 以前に *保存したボット* ID で MicrosoftAppId 値を更新します。 以前に *保存したボット パスワードを使用して MicrosoftAppPassword* を更新します。

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

これらの変更が行われたら、アプリを再構築します。 ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合はアプリを再展開します。

## <a name="configure-the-app-tab"></a>[アプリ] タブの構成

アプリをチームにインストールしたら、コンテンツを表示するためにアプリを構成する必要があります。 サンプル アプリをインストールしたチームのチャネルに移動し **、[+]** ボタンをクリックして新しいタブを追加します。次に、[タブ `Hello World` の追加 **] リストから選択** できます。 その後、構成ダイアログが表示されます。 このダイアログでは、このチャネルに表示するタブを選択できます。 タブを選択してクリックすると、選択したタブが読 `Save` `Hello World` み込まれたタブが表示されます。

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Teams でボットをテストする

Teams でボットを操作できます。 アプリを登録したチーム内のチャネルを選択し、入力します `@your-bot-name` 。 これはメンションと呼 **\@ ばれる.** ボットに送信したメッセージは、返信として返されます。

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある 3 つのドットをクリックします。 メニューに「Hello **World」アプリが** 表示されます。 クリックすると、ランダムなテキストの束が表示されます。 任意の 1 つを選択すると、会話に挿入されます。

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

ランダムなテキストのいずれかを選択すると、カードが書式設定され、下部に独自のメッセージを送信する準備が整いました。

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
