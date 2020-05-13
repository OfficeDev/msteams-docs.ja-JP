---
title: C#/.NET を使用して作業を開始する
description: C#/.NET を使用して Microsoft Teams での高度なアプリの作成を始める
keywords: .net c# csharp の概要
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: c29fdde23ff6ff0e8269ccaf256c5154c0145a7b
ms.sourcegitcommit: b9e8839858ea8e9e33fe5e20e14bbe86c75fd510
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "44210695"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-cnet-and-app-studio"></a>Microsoft Teams プラットフォームで C#/.NET とアプリ Studio を使用して作業を開始する

[Microsoft teams](/microsoftteams/)開発者プラットフォームを使用すると、teams の拡張が容易になり、独自のアプリケーションやサービスを teams ワークスペースにシームレスに統合することができます。 これらのアプリは、企業または世界中の teams に配布できます。

Microsoft Teams を拡張するには、Microsoft Teams アプリを作成する必要があります。 Microsoft Teams アプリは、ホストする web アプリケーションです。 このアプリは、Teams のユーザーのワークスペースに統合できます。

このチュートリアルでは、.NET での C# を使用した Microsoft Teams アプリの作成を開始する際に役立つ情報が得られます。 アプリをテストするには、アクセス許可を持っているチームに読み込むか、Office 開発者プログラムを使用して作成したテストテナントに取り込む必要があります。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>前提条件を取得する

このチュートリアルを完了するには、次のツールを入手する必要があります。

- [Git をインストールする](https://git-scm.com/downloads)
- [Visual Studio をインストール](https://www.visualstudio.com/downloads/)します。 無料のコミュニティエディションをインストールすることができます。

インストール時にパスに追加するオプションが表示された場合は `git` 、それを選択します。 これは便利です。

`git`ターミナルウィンドウで次のように実行して、インストールを確認します。
> [!NOTE]
> ご使用のプラットフォームで最も快適なターミナルウィンドウを使用してください。 これらの例では Bash を使用していますが、ほとんどのプラットフォームで実行されます。

```bash
$ git --version
git version 2.17.1.windows.2

```

必要に応じて、最新バージョンの Visual Studio を起動し、更新プログラムをインストールします。

このターミナルウィンドウを引き続き使用して、このチュートリアルの後のコマンドを実行できます。

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>サンプルをダウンロードする

シンプルな Hello を提供してい[ます。](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) 開始する方法については、C# のサンプルをご確認ください。 ターミナルウィンドウで、次のコマンドを実行して、サンプルリポジトリをローカルコンピューターに複製します。

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> 後で参照できるように GitHub への変更を変更してチェックインする場合は、この[リポジトリ](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)を[fork](https://help.github.com/articles/fork-a-repo/)することができます。

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>サンプルの構築と実行

リポジトリのクローンを作成したら、Visual Studio を使用して、 `Microsoft.Teams.Samples.HelloWorld.sln` サンプルのルートディレクトリからソリューションファイルを開き、メニューから [] をクリックし `Build Solution` `Build` ます。 このサンプルを実行するには `F5` `Start Debugging` 、メニューから [] を押すか、選択し `Debug` ます。

アプリが開始すると、アプリのルートが起動されたブラウザーウィンドウが開きます。 次の Url に移動して、すべてのアプリ Url が読み込まれていることを確認できます。

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> そのようなエラーが表示された場合は `Could not find a part of the path … bin\roslyn\csc.exe` 、コマンドを使用してパッケージを更新してみてください `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。 詳細については、[スタックオーバーフローでこの質問](https://stackoverflow.com/questions/32780315)を参照してください。

## <a name="host-the-sample-app"></a>サンプルアプリをホストする

Microsoft Teams のアプリは、1つまたは複数の機能を公開している web アプリケーションであることに注意してください。 Teams プラットフォームでアプリを読み込むには、インターネットからアプリにアクセスできる必要があります。 アプリをインターネットからアクセスできるようにするには、アプリをホストする必要があります。 Microsoft Azure で無料でホストすることも、を使用して開発用コンピューター上のローカルプロセスへのトンネルを作成することもでき `ngrok` ます。 アプリのホストが終了したら、ルート URL を書き留めておきます。 これは、またはというようになり `https://yourteamsapp.ngrok.io` `https://yourteamsapp.azurewebsites.net` ます。

### <a name="tunnel-using-ngrok"></a>Ngrok を使用したトンネル

迅速なテストのために、ローカルコンピューター上でアプリを実行し、web エンドポイント経由でそのアプリケーションへのトンネルを作成することができます。 [ngrok](https://ngrok.com)は、そのようなことを可能にする無償のツールです。 Ngrok を使用すると、などの web アドレスを取得でき `https://d0ac14a5.ngrok.io` ます (この URL は例にすぎません)。 環境の ngrok を[ダウンロードしてインストール](https://ngrok.com/download)することができます。 がの場所に追加されていることを確認してください `PATH` 。

インストールすると、新しいターミナルウィンドウを開き、次のコマンドを実行してトンネルを作成できます。 このサンプルではポート3333を使用しているため、ここで必ず指定してください。

```bash
ngrok http 3333 -host-header=localhost:3333
```

Ngrok は、インターネットからの要求をリスンし、ポート3333で実行されているアプリにルーティングします。 ブラウザーを開き、アプリの hello ページを読み込むことによって確認でき `https://d0ac14a5.ngrok.io/hello` ます。 この URL ではなく、コンソールセッションで ngrok によって表示される転送アドレスを使用してください。

> [!NOTE]
> 上記の[ビルド](#build-and-run-the-sample)で別のポートを使用している場合は、同じポート番号を使用してトンネルを設定してください `ngrok` 。
> [!TIP]
> 後で停止して `ngrok` 再構築して再実行する必要があるアプリケーションに影響を与えることなく、別のターミナルウィンドウで実行して、そのまま実行することをお勧めします。 `ngrok`このウィンドウでは、セッションが有用なデバッグ情報を返します。

アプリは、開発コンピューター上の現在のセッション中にのみ使用できます。 コンピューターがシャットダウンされるかスリープ状態になると、サービスは使用できなくなります。 他のユーザーによるテスト用にアプリを共有する場合は、この点に注意してください。 サービスを再起動する必要がある場合は、新しいアドレスを返し、そのアドレスを使用するすべての場所を更新する必要があります。 Ngrok の有料バージョンには、この制限はありません。

### <a name="host-in-azure"></a>Azure でのホスト

Microsoft Azure を使用すると、共有インフラストラクチャを使用して、.NET アプリケーションを自由層でホストできます。 このサンプルを実行するには、この方法で十分 `Hello World` です。 詳細について[は、「新しい無料アカウントの作成](https://azure.microsoft.com/free/)」を参照してください。

Visual Studio には、Azure を含むさまざまなプロバイダーへのアプリ展開のサポートが組み込まれています。

<img width="530px" src="~/assets/images/get-started/publishtoazure1.png" title="Visual Studio"/>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>ホストされているアプリの資格情報を更新する

サンプルアプリでは、以下の環境変数を事前にメモした値に設定する必要があります。

Appsettings ファイルを開きます。 以前に保存した Bot ID を使用して、 *Microsoft appid*の値を更新します。 以前に保存した Bot パスワードを使用して、 *Microsoft Apppassword*を更新します。

<img width="560px" src="~/assets/images/get-started/get-started-net-azure-add-keys.png" title="キーの設定"/>

これらの変更を行った後、アプリを再構築します。 Ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合はアプリを再展開します。

## <a name="configure-the-app-tab"></a>[アプリ] タブを構成する

アプリをチームにインストールしたら、コンテンツを表示するように構成する必要があります。 サンプルアプリをインストールしたチームのチャネルに移動し、[ **+** ] ボタンをクリックして新しいタブを追加します。その後、[ `Hello World` **タブの追加]** ボックスの一覧から選択できます。 構成ダイアログが表示されます。 このダイアログボックスを使用すると、このチャネルに表示するタブを選択できます。 タブを選択して、[] をクリックすると、 `Save` 選択したタブが読み込まれたタブが表示され `Hello World` ます。

<img width="530px" src="~/assets/images/samples-hello-world-tab-configure.png" title="構成のスクリーンショット" />

### <a name="test-your-bot-in-teams"></a>Teams でボットをテストする

Teams で bot と対話できるようになりました。 アプリを登録したチームでチャネルを選択し、と入力し `@your-bot-name` ます。 これは、 ** \@ メンション**と呼ばれます。 Bot に送信するすべてのメッセージは、返信として返送されます。

<img width="450px" title="ボット応答" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

メッセージング拡張機能をテストするには、スレッドビューの入力ボックスの下にある3つのドットをクリックします。 **' Hello World '** アプリが含まれるメニューが表示されます。 これをクリックすると、一連のランダムなテキストが表示されます。 いずれかを選択して、会話に挿入することができます。

<img width="530px" title="メッセージング拡張メニュー" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" title="メッセージング拡張機能の結果" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

ランダムなテキストの1つを選択すると、カードが書式設定されており、メッセージの下部に自分のメッセージで送信する準備ができます。

<img width="530px" title="メッセージング拡張送信" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
