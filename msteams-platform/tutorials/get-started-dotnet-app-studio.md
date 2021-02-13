---
title: チュートリアル - C を使用して最初のアプリを作成する#
description: C# または .NET を使用して Microsoft Teams アプリの構築を開始する方法について説明します。
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: b37a8d555117e38383504dc99d82d564439a3ebf
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231528"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a>C# または .NET を使用して最初の Teams アプリを作成する

このチュートリアルでは、C# または .NET を使用して Microsoft Teams アプリを作成する方法について説明します。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>前提条件を取得する

このチュートリアルを完了するには、次のツールを取得する必要があります。

- [Git をインストールする](https://git-scm.com/downloads)
- [インストールVisual Studio](https://www.visualstudio.com/downloads/)。 無料のコミュニティ エディションをインストールできます。

インストール時に PATH に追加するオプションがある場合は、 `git` それを選択します。

ターミナル ウィンドウで、次のコマンドを実行してインストールを確認 `git` します。

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> プラットフォームで適切なターミナル ウィンドウを使用します。 これらの例では Bash を使用していますが、ほとんどのプラットフォームで実行されます。

最新バージョンの更新プログラムを必ず起動し、Visual Studioインストールしてください。

このチュートリアルでは、同じターミナル ウィンドウを使用してコマンドを実行できます。

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>サンプルをダウンロードする

簡単な [Hello, World を使い始めよう!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) C# のサンプル。 ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをローカル コンピューターに複製します。

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> このリポジトリ [をフォーク](https://help.github.com/articles/fork-a-repo/) して [、](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) 変更を変更して GitHub に保存し、参照することができます。

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>サンプルの構築と実行

リポジトリを複製した後、Visual Studio を使用して、サンプルのルート ディレクトリからソリューション ファイルを開き、メニュー `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` から選択 `Build` します。 サンプルを実行するには、メニューを `F5` 押す `Start Debugging` 、またはメニューから選択 `Debug` します。

アプリが起動すると、ブラウザー ウィンドウが開き、アプリのルートが起動します。 次の URL に移動して、すべてのアプリの URL が読み込み中か確認できます。

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second]https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> エラーが発生した場合 `Could not find a part of the path … bin\roslyn\csc.exe` は、コマンドを使用してパッケージを更新します `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。 詳細については [、StackOverflow に関するこの質問を参照してください](https://stackoverflow.com/questions/32780315)。

## <a name="host-the-sample-app"></a>サンプル アプリをホストする

Microsoft Teams のアプリは、1 つ以上の機能を提供する Web アプリケーションです。 Teams プラットフォームでアプリを読み込むには、インターネットからアプリにアクセスできる必要があります。 インターネットからアプリにアクセスするには、アプリをホストする必要があります。 Microsoft Azure で無料でホストするか、開発マシンで使用するローカル プロセスへのトンネルを作成できます `ngrok` 。 アプリのホストが終了したら、そのルート URL をメモします。 たとえば、`https://yourteamsapp.ngrok.io` または `https://yourteamsapp.azurewebsites.net` などです。

### <a name="tunnel-using-ngrok"></a>ngrok を使用したトンネル

簡単なテストを行う場合は、ローカル コンピューターでアプリを実行し、Web エンドポイント経由でトンネルを作成できます。 [ngrok は](https://ngrok.com) 、次のような Web アドレスを取得できる無料のツールです `https://d0ac14a5.ngrok.io` 。 ngrok [をダウンロードして](https://ngrok.com/download) インストールできます。 自分の場所に追加してください `PATH` 。

ngrok をインストールした後、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成します。

```bash
ngrok http 44327 -host-header=localhost:44327
```

このサンプルでは、ポート 44327 を使用して、必ず指定してください。

Ngrok はインターネットからの要求をリッスンし、ポート 44327 で実行されているアプリにルーティングします。 確認するには、ブラウザーを開き、アプリの Hello ページを読み込 `https://d0ac14a5.ngrok.io/hello` むに移動します。 この URL の代わりに、コンソール セッションで ngrok によって表示される転送アドレスを使用します。

> [!NOTE]
> ビルドと実行の手順で別のポート[](#build-and-run-the-sample)を使用した場合は、必ず同じポート番号を使用してトンネルをセットアップ `ngrok` してください。

> [!TIP]
> 別のターミナル ウィンドウで実行 `ngrok` すると良い方法です。 これは、アプリを妨げずに ngrok が実行されるのを止め、再構築し、再実行する必要がある場合に実行されます。 セッション `ngrok` は、このウィンドウで役立つデバッグ情報を提供します。

アプリは、開発用コンピューター上の現在のセッション中にのみ利用できます。 コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは利用できなくなりました。 テスト用のアプリを他のユーザーと共有する場合は、このことを覚えておいてください。 サービスを再起動する必要がある場合、アプリは新しいアドレスを返し、そのアドレスを使用する場所を更新する必要があります。 有料版の ngrok には、この制限はありません。

### <a name="host-in-azure"></a>Azure でのホスト

Microsoft Azure は、共有インフラストラクチャを使用して、無料の階層で .NET アプリケーションをホストします。 これでサンプルを実行するのに十分 `Hello World` です。 詳しくは、新しい [無料アカウントの作成に関するページをご覧ください](https://azure.microsoft.com/free/)。

Visual Studioには、Azure を含むさまざまなプロバイダーへのアプリ展開のサポートが組み込みされています。

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>ホストされているアプリの資格情報を更新する

サンプル アプリでは、前にメモした値に次の環境変数を設定する必要があります。

ファイルのappsettings.js開きます。 *MicrosoftAppId の値を*、以前に保存したボット ID で更新します。 *MicrosoftAppPassword を、以前* に保存した Bot パスワードで更新します。

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

これらの変更が行われたら、アプリをリビルドします。 ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合はアプリを再展開します。

## <a name="configure-the-app-tab"></a>[アプリ] タブを構成する

アプリをチームにインストールしたら、コンテンツを表示するためにアプリを構成する必要があります。 サンプル アプリをインストールしたチームのチャネルに移動し **、[+]** ボタンをクリックして新しいタブを追加します。その後、[タブ `Hello World` の追加] **ボックスの一覧から選択** できます。 構成ダイアログが表示されます。 このダイアログでは、このチャネルに表示するタブを選択できます。 タブを選択してクリックすると、選択したタブと一緒にタブ `Save` `Hello World` が読み込まれるのが表示されます。

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Teams でボットをテストする

Teams でボットを操作できます。 アプリを登録して入力したチームのチャネルを選択します `@your-bot-name` 。 これはメンションと呼 **\@ ばれる。** ボットに送信したメッセージは、返信として返送されます。

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある 3 つのドットをクリックします。 メニューに **"Hello World" アプリが** 表示されます。 クリックすると、一連のランダムなテキストが表示されます。 You can choose any one of them and it is inserted into your conversation.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

ランダムなテキストのいずれかを選択すると、カードがフォーマットされ、下部に独自のメッセージと一緒に送信する準備が整っているのが表示されます。

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
