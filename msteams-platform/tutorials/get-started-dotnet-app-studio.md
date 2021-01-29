---
title: チュートリアル - C を使用して最初のアプリを作成する#
description: C#/.NET を使用して Microsoft Teams アプリの構築を開始する方法について説明します。
keywords: getting started .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: c28c4d00c375b8e37f82c343eec2c5405ae0c1c8
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037040"
---
# <a name="create-your-first-microsoft-teams-app-using-c"></a>C を使用して最初の Microsoft Teams アプリを作成する#

このチュートリアルは、.NET で C# を使用して Microsoft Teams アプリの作成を開始する際に役立ちます。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>前提条件を取得する

このチュートリアルを完了するには、次のツールを取得する必要があります。

- [Git をインストールする](https://git-scm.com/downloads)
- [インストールVisual Studio](https://www.visualstudio.com/downloads/)。 無料のコミュニティ エディションをインストールできます。

インストール中に PATH に追加するオプションが表示された場合は、 `git` そのオプションを選択します。 便利です。

ターミナル ウィンドウ `git` で次のコマンドを実行して、インストールを確認します。
> [!NOTE]
> プラットフォームで最も使いやすいターミナル ウィンドウを使用します。 これらの例では Bash を使用していますが、ほとんどのプラットフォームで実行されます。

```bash
$ git --version
git version 2.17.1.windows.2

```

最新バージョンの更新プログラムを必ず起動し、表示Visual Studio更新プログラムをインストールしてください。

このターミナル ウィンドウを引き続き使用して、このチュートリアルに従うコマンドを実行できます。

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>サンプルをダウンロードする

シンプルな [Hello, World が用意されています。](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) C# のサンプルを使用して開始してください。 ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをローカル コンピューターに複製します。

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> 今後の[参照のために](https://help.github.com/articles/fork-a-repo/) [](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) GitHub への変更を変更してチェックインする場合は、このリポジトリをフォークできます。

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>サンプルの構築と実行

リポジトリを複製したら、Visual Studio を使用して、サンプルのルート ディレクトリからソリューション ファイルを開き、メニュー `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` からクリック `Build` します。 メニューを押したり、メニューから選択したりすることで `F5` 、サンプル `Start Debugging` を実行 `Debug` できます。

アプリが起動すると、アプリのルートが表示されたブラウザー ウィンドウが開きます。 次の URL に移動して、すべてのアプリの URL が読み込み中か確認できます。

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe` like, try updating the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` . [StackOverflow の詳細については、この](https://stackoverflow.com/questions/32780315)質問を参照してください。

## <a name="host-the-sample-app"></a>サンプル アプリをホストする

Microsoft Teams のアプリは、1 つ以上の機能を公開する Web アプリケーションです。 Teams プラットフォームでアプリを読み込むには、インターネットからアプリにアクセスできる必要があります。 インターネットからアプリにアクセスするには、アプリをホストする必要があります。 Microsoft Azure で無料でホストするか、開発マシンで使用するローカル プロセスへのトンネルを作成できます `ngrok` 。 アプリのホストが終了したら、そのルート URL をメモします。 次のように表示 `https://yourteamsapp.ngrok.io` されます `https://yourteamsapp.azurewebsites.net` 。

### <a name="tunnel-using-ngrok"></a>ngrok を使用したトンネル

迅速なテストを行う場合は、ローカル コンピューターでアプリを実行し、Web エンドポイント経由でトンネルを作成できます。 [ngrok は](https://ngrok.com) 、それを実行できる無料のツールです。 ngrok を使用すると、次のような Web アドレス `https://d0ac14a5.ngrok.io` を取得できます (この URL は単なる例です)。 環境に [合った](https://ngrok.com/download) ngrok をダウンロードしてインストールできます。 自分の場所に追加してください `PATH` 。

インストールしたら、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成できます。 サンプルではポート 3333 を使用します。そのため、ここで指定してください。

```bash
ngrok http 3333 -host-header=localhost:3333
```

Ngrok はインターネットからの要求をリッスンし、ポート 3333 で実行されているアプリにルーティングします。 確認するには、ブラウザーを開き、アプリの Hello ページを読 `https://d0ac14a5.ngrok.io/hello` み込む方法があります。 この URL の代わりに、コンソール セッションで ngrok によって表示される転送アドレスを使用してください。

> [!NOTE]
> ビルドで別のポートを使用し、[](#build-and-run-the-sample)上記の手順を実行した場合は、必ず同じポート番号を使用してトンネルをセットアップ `ngrok` してください。
> [!TIP]
> 後で停止、リビルド、再実行が必要になる可能性があるアプリを妨げることなく、別のターミナル ウィンドウで実行し続けます `ngrok` 。 セッション `ngrok` は、このウィンドウで有用なデバッグ情報を返します。

アプリは、開発用コンピューター上の現在のセッション中にのみ利用できます。 コンピューターがシャットダウンするか、スリープ状態になった場合、サービスは利用できなくなりました。 他のユーザーがテスト用にアプリを共有する場合は、このことを覚えておいてください。 サービスを再起動する必要がある場合は、新しいアドレスが返され、そのアドレスを使用する場所ごとに更新する必要があります。 Ngrok の有料版には、この制限はありません。

### <a name="host-in-azure"></a>Azure でのホスト

Microsoft Azure では、共有インフラストラクチャを使用して無料の階層で .NET アプリケーションをホストできます。 このサンプルを実行するにはこれで十分 `Hello World` です。 詳 [しくは、新しい無料アカウントの作成](https://azure.microsoft.com/free/) に関するページをご覧ください。

Visual Studioには、Azure を含むさまざまなプロバイダーへのアプリ展開のサポートが組み込みされています。

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>ホストされているアプリの資格情報を更新する

サンプル アプリでは、前にメモした値に次の環境変数を設定する必要があります。

ファイルのappsettings.js開きます。 *MicrosoftAppId の値を*、以前に保存したボット ID で更新します。 *MicrosoftAppPassword を、以前* に保存した Bot パスワードで更新します。

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

これらの変更が行われたら、アプリをリビルドします。 ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合はアプリを再展開します。

## <a name="configure-the-app-tab"></a>[アプリ] タブを構成する

アプリをチームにインストールしたら、コンテンツを表示するためにアプリを構成する必要があります。 サンプル アプリをインストールしたチームのチャネルに移動し **、[+]** ボタンをクリックして新しいタブを追加します。その後、[タブ `Hello World` の追加] **ボックスの一覧から選択** できます。 構成ダイアログが表示されます。 このダイアログでは、このチャネルに表示するタブを選択できます。 タブを選択してクリックすると、選択したタブと一緒に読み込 `Save` `Hello World` まれたタブが表示されます。

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Teams でボットをテストする

Teams でボットを操作できます。 アプリを登録したチームのチャネルを選択し、「」と入力します `@your-bot-name` 。 これはメンションと呼 **\@ ばれる。** ボットに送信したメッセージは、返信として返送されます。

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある 3 つのドットをクリックします。 メニューに **"Hello World"** アプリが表示されます。 クリックすると、一連のランダムなテキストが表示されます。 You can choose any one of them and it will be inserted it into your conversation.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

ランダムなテキストのいずれかを選択すると、カードがフォーマットされ、下部に独自のメッセージと一緒に送信する準備が整っているのが表示されます。

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
