---
title: アプリ Studio および Node.js の使用を開始する
description: Node.js とアプリ Studio を使用して Microsoft Teams での高度なアプリの作成を開始する
keywords: nodejs App Studio node.js の概要
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 3d86738d32c049d31a84c6c47746e275db5e6349
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931814"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-nodejs-and-app-studio"></a>Node.js とアプリ Studio を使用して Microsoft Teams プラットフォームでの作業を開始する

[Microsoft teams](/microsoftteams/)開発者プラットフォームを使用すると、teams の拡張が容易になり、独自のアプリケーションやサービスを teams ワークスペースにシームレスに統合することができます。 これらのアプリは、企業または世界中の teams に配布できます。

Microsoft Teams を拡張するには、Microsoft Teams アプリを作成する必要があります。 Microsoft Teams アプリは、ホストする web アプリケーションです。 このアプリは、Teams のユーザーのワークスペースに統合できます。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>アプリをダウンロードしてホストする

簡単な "hello world" アプリを Teams にダウンロードしてホストするには、次の手順を実行します。

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>前提条件を取得する

このチュートリアルを完了するには、次のツールが必要です。 これらのリンクからインストールすることはできません。

- [Git](https://git-scm.com/downloads)
- [Node.js と NPM](https://nodejs.org/)
- 任意のテキストエディターまたは IDE を取得します。 [Visual Studio コード](https://code.visualstudio.com/download)を無料でインストールして使用することができます。

インストール時に、、、、およびのパスを追加するオプションが表示さ `git` `node` れたら `npm` `code` 、それを選択します。 これは便利です。

ターミナルウィンドウで次のように実行して、ツールが使用可能であることを確認します。

> [!NOTE]
> ご使用のプラットフォームで最も快適なターミナルウィンドウを使用してください。 これらの例では、Bash (Git に含まれています) を使用していますが、これらのスクリプトはほとんどのプラットフォームで実行されます。

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 2.3.0
Local version 4.0.2
```

これらのアプリケーションのバージョンが異なる場合があります。 これは、gulp を除き、問題になりません。 Gulp の場合は、バージョン4.0.0 以降を使用する必要があります。

Gulp がインストールされていない (または、バージョンが正しくない) 場合は、ターミナルウィンドウでを実行して、これを実行し `npm install gulp` ます。

Visual Studio Code をインストールした場合は、インストールを確認するには、次のように実行します。

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

このターミナルウィンドウを引き続き使用して、このチュートリアルの後のコマンドを実行できます。

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>サンプルをダウンロードする

シンプルな Hello を提供してい [ます。](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) 開始するためのサンプルです。 ターミナルウィンドウで、次のコマンドを実行して、サンプルリポジトリをローカルコンピューターに複製します。

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> 後で参照できるように GitHub リポジトリに加えた変更を変更してチェックインする場合は、この[リポジトリ](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)を[fork](https://help.github.com/articles/fork-a-repo/)することができます。

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a>サンプルの構築と実行

リポジトリが複製されたら、サンプルを保持するディレクトリに変更します。

```bash
cd msteams-samples-hello-world-nodejs
```

サンプルをビルドするには、そのすべての依存関係をインストールする必要があります。 これを行うには、次のコマンドを実行します。

```bash
npm install
```

一連の依存関係がインストールされていることを確認する必要があります。 完了したら、アプリを実行することができます。

```bash
npm start
```

Hello world アプリが開始すると、 `App started listening on port 3333` ターミナルウィンドウに表示されます。

> [!NOTE]
> 上記のメッセージに別のポート番号が表示されている場合は、ポート環境変数が設定されているためです。 そのポートを引き続き使用するか、環境変数を3333に変更することができます。

この時点で、ブラウザーウィンドウを開き、次の Url に移動して、すべてのアプリ Url が読み込まれていることを確認できます。

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>サンプルアプリをホストする

Microsoft Teams のアプリは、1つまたは複数の機能を公開している web アプリケーションであることに注意してください。 Teams プラットフォームでアプリを読み込むには、インターネットからアプリにアクセスできる必要があります。 アプリをインターネットからアクセスできるようにするには、アプリを *ホスト* する必要があります。

ローカルテストでは、ローカルコンピューター上でアプリを実行し、web エンドポイントを使用してそのアプリケーションへのトンネルを作成できます。 [ngrok](https://ngrok.com) は、そのようなことを可能にする無償のツールです。 *Ngrok* を使用すると、などの web アドレスを取得でき `https://d0ac14a5.ngrok.io` ます (この URL は例にすぎません)。 環境の *ngrok* を [ダウンロードしてインストール](https://ngrok.com/download)することができます。 がの場所に追加されていることを確認してください `PATH` 。

インストールすると、新しいターミナルウィンドウを開き、次のコマンドを実行してトンネルを作成できます。 このサンプルではポート3333を使用しているため、ここで必ず指定してください。

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok* は、インターネットからの要求をリスンし、ポート3333で実行されているアプリにルーティングします。 ブラウザーを開き、アプリの hello ページを読み込むことによって確認でき `https://d0ac14a5.ngrok.io/hello` ます。 この URL ではなく、コンソールセッションで *ngrok* によって表示される転送アドレスを使用してください。

> [!NOTE]
> 上記の [ビルド](#build-and-run-the-sample) で別のポートを使用している場合は、同じポート番号を使用して *ngrok* トンネルをセットアップしてください。
> [!TIP]
> *Ngrok* を別のターミナルウィンドウで実行して、ノードアプリに影響を及ぼすことなく、後で停止、再構築、再実行する必要があります。 *Ngrok* セッションは、このウィンドウで役に立つデバッグ情報を返します。

固定名を許可する有料版の *ngrok* があります。 無料バージョンを使用する場合、アプリは開発用コンピューター上の現在のセッション中にのみ使用できます。 コンピューターがシャットダウンされるかスリープ状態になると、サービスは使用できなくなります。 他のユーザーによるテスト用にアプリを共有する場合は、この点に注意してください。 サービスを再起動する必要がある場合は、新しいアドレスを返し、そのアドレスを使用するすべての場所を更新する必要があります。

アプリをアプリを使用して Teams に登録するときに必要になるため、後でアプリの URL を書き留めておいてください。 このため、メモ帳は正常に動作します。

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>アプリを Microsoft Teams に展開する

この時点では、インターネット上でホストされているアプリがありますが、チームに対して、またはアプリの呼び出しについての情報を提供する方法はありません。 これを行うには、アプリパッケージを作成する必要があります。 これは、アプリマニフェストと、Teams クライアントがアプリを適切に表示およびブランド化するために使用するいくつかのアイコンを含むテキストファイルに比べてわずかです。 このアプリパッケージを手動で作成するか、アプリを登録するプロセスを簡略化する Teams で実行されるツールである App Studio を使用することができます。 アプリのパッケージを作成および更新する方法として、アプリ Studio が推奨されています。

どちらの方法でも、次のものが必要になります。

- アプリをインターネット上で見つけることができる URL。
- Teams がアプリをブランド化するために使用するアイコン。 サンプルには、"src\static\images." にあるプレースホルダーアイコンが付属しています。 アプリ Studio では、必要に応じて既定のアイコンも提供されます。

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>ホストされているアプリを更新する

サンプルアプリでは、以下の環境変数を事前にメモした値に設定する必要があります。

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

その方法は、アプリをホストした方法によって異なります。 環境変数を使用する場合の重要な点は、これらの値は環境の一部であり、アプリのコードからアクセスできますが、サイトを構成するファイルを調べる可能性がある第三者には公開されません。

Ngrok を使用してアプリを実行している場合は、いくつかのローカル環境変数を設定する必要があります。 これを行うには多くの方法がありますが、Visual Studio Code を使用している場合は、 [起動構成](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)を追加するのが最も簡単です。

``` 
{
    "type": "node",
    "request": "launch",
    "name": "Launch - Teams Debug",
    "program": "${workspaceRoot}/src/app.js",
    "cwd": "${workspaceFolder}/src",
    "env": {
        "BASE_URI": "https://yourNgrokURL.ngrok.io",
        "MICROSOFT_APP_ID": "00000000-0000-0000-0000-000000000000",
        "MICROSOFT_APP_PASSWORD": "yourBotAppPassword",
        "NODE_DEBUG": "botbuilder",
        "SUPPRESS_NO_CONFIG_WARNING": "y",
        "NODE_CONFIG_DIR": "../config"
    }
}
```

ここで、

MICROSOFT_APP_ID と MICROSOFT_APP_PASSWORD は、それぞれの bot の ID とパスワードです。
NODE_DEBUG は、Visual Studio Code デバッグコンソールで bot で起こっていることを示します。
NODE_CONFIG_DIR リポジトリのルートにあるディレクトリを指します (既定では、アプリがローカルで実行されている場合は、そのフォルダーが src フォルダーで検索されます)。

> [!Note]
> チュートリアルの前半で npm を停止していない場合は、 `npm stop` Visual Studio Code が起動構成変数を正しくピックアップするために実行する必要があります。

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>[アプリ] タブを構成する

アプリをチームにインストールしたら、コンテンツを表示するように構成する必要があります。 チーム内のチャネルに移動し、[ **+** ] ボタンをクリックして新しいタブを追加します。その後、[ `Hello World` **タブの追加]** ボックスの一覧から選択できます。 構成ダイアログが表示されます。 このダイアログボックスを使用すると、このチャネルに表示するタブを選択できます。 タブを選択して [] をクリックすると、選択したタブに読み込まれたタブが表示され `Save` `Hello World` ます。

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" alt-text="Screenshot of configure" />

### <a name="test-your-bot-in-teams"></a>Teams でボットをテストする

Teams で bot と対話できるようになりました。 アプリを登録したチームでチャネルを選択し、「」と入力し `@your-bot-name` て、その後にメッセージを入力します。 これは、 **\@ メンション** と呼ばれます。 Bot に送信するすべてのメッセージは、返信として返送されます。

<img width="450px" alt-text="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

メッセージング拡張機能をテストするには、スレッドビューの入力ボックスの下にある3つのドットをクリックします。 **' Hello World '** アプリが含まれるメニューが表示されます。 これをクリックすると、いくつかのランダムなテキストが表示されます。 いずれかを選択して、会話に挿入することができます。

<img width="430px" alt-text="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt-text="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

ランダムなテキストの1つを選択すると、カードが書式設定されており、メッセージの下部に自分のメッセージで送信する準備ができます。

<img width="430px" alt-text="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
