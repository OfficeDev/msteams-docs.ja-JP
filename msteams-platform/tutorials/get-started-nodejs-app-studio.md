---
title: チュートリアル - アプリを使用して最初のアプリをNode.js
description: Microsoft Teams アプリの構築を開始する方法について説明Node.js。
keywords: nodejs App Studio node.jsの開始
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 03dcf79a46266321e54c7e99bf01cdd2a87075fa
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037047"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a>アプリを使用して最初の Microsoft Teams アプリをNode.js

このチュートリアルでは、Microsoft Teams アプリの作成を開始する際に役立つNode.js。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>アプリをダウンロードしてホストする

次の手順に従って、Teams で簡単な "hello world" アプリをダウンロードしてホストします。

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>前提条件を取得する

このチュートリアルを完了するには、次のツールが必要です。 まだインストールしていない場合は、これらのリンクからインストールできます。

- [Git](https://git-scm.com/downloads)
- [Node.js NPM](https://nodejs.org/)
- 任意のテキスト エディターまたは IDE を取得します。 このコードは、無料で [Visual Studioして](https://code.visualstudio.com/download) 使用できます。

インストール中に PATH を追加するオプションが表示された場合は、追加 `git` `node` `npm` `code` するオプションを選択します。 便利です。

ターミナル ウィンドウで次のコマンドを実行して、ツールが利用可能な状態を確認します。

> [!NOTE]
> プラットフォームで最も使いやすいターミナル ウィンドウを使用します。 これらの例では Bash (Git に含まれています) を使用していますが、これらのスクリプトはほとんどのプラットフォームで実行されます。

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

これらのアプリケーションのバージョンが異なる場合があります。 gulp を除き、これは問題ではありません。 gulp の場合は、バージョン 4.0.0 以降を使用する必要があります。

gulp がインストールされていない場合 (または正しいバージョンがインストールされていない場合) は、ターミナル ウィンドウで実行して `npm install gulp` 、今すぐインストールします。

コードをインストールしたVisual Studio、次のコマンドを実行してインストールを確認できます。

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

このターミナル ウィンドウを引き続き使用して、このチュートリアルに従うコマンドを実行できます。

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>サンプルをダウンロードする

シンプルな [Hello, World が用意されています。](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) サンプルを使用して開始してください。 ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをローカル コンピューターに複製します。

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> 今後の[参照のために](https://help.github.com/articles/fork-a-repo/) [](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) GitHub リポジトリの変更を変更してチェックインする場合は、このリポジトリをフォークできます。

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a>サンプルの構築と実行

リポジトリを複製したら、サンプルを保持するディレクトリに移動します。

```bash
cd msteams-samples-hello-world-nodejs
```

サンプルをビルドするには、すべての依存関係をインストールする必要があります。 これを行うには、次のコマンドを実行します。

```bash
npm install
```

一連の依存関係がインストールされている必要があります。 完了したら、アプリを実行できます。

```bash
npm start
```

hello-world アプリが起動すると、ターミナル `App started listening on port 3333` ウィンドウに表示されます。

> [!NOTE]
> 上記のメッセージに別のポート番号が表示される場合は、PORT 環境変数が設定されているためです。 引き続きそのポートを使用するか、環境変数を 3333 に変更できます。

この時点で、ブラウザー ウィンドウを開き、次の URL に移動して、すべてのアプリ URL が読み込み中か確認できます。

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>サンプル アプリをホストする

Microsoft Teams のアプリは、1 つ以上の機能を公開する Web アプリケーションです。 Teams プラットフォームでアプリを読み込むには、インターネットからアプリにアクセスできる必要があります。 インターネットからアプリにアクセスするには、アプリをホスト *する* 必要があります。

ローカル テストでは、ローカル コンピューターでアプリを実行し、Web エンドポイントを使用してそのコンピューターへのトンネルを作成できます。 [ngrok は](https://ngrok.com) 、それを実行できる無料のツールです。 *ngrok を使用* すると、次のような Web アドレス `https://d0ac14a5.ngrok.io` を取得できます (この URL は単なる例です)。 環境に [合った](https://ngrok.com/download) *ngrok をダウンロード* してインストールできます。 自分の場所に追加してください `PATH` 。

インストールしたら、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成できます。 サンプルではポート 3333 を使用します。そのため、ここで指定してください。

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok は* インターネットからの要求をリッスンし、ポート 3333 で実行されているアプリにルーティングします。 確認するには、ブラウザーを開き、アプリの Hello ページを読 `https://d0ac14a5.ngrok.io/hello` み込む方法があります。 この URL の代わりに、コンソール セッションで *ngrok* によって表示される転送アドレスを使用してください。

> [!NOTE]
> ビルドで別のポートを使用して上記 [](#build-and-run-the-sample)の手順を実行した場合は、同じポート番号を使用して *ngrok トンネルをセットアップ* してください。
> [!TIP]
> *ngrok* を別のターミナル ウィンドウで実行し、後で停止、リビルド、再実行が必要になる可能性があるノード アプリを妨げずに実行し続けます。 *ngrok セッションは*、このウィンドウで役立つデバッグ情報を返します。

永続的な名前を許可する *有料版の ngrok* があります。 無料版を使う場合は、開発用コンピューターの現在のセッション中にのみアプリを利用できます。 コンピューターがシャットダウンするか、スリープ状態になった場合、サービスは利用できなくなりました。 他のユーザーがテスト用にアプリを共有する場合は、このことを覚えておいてください。 サービスを再起動する必要がある場合は、新しいアドレスが返され、そのアドレスを使用する場所ごとに更新する必要があります。

アプリの URL は、後で App Studio を使用して Teams に登録するときに必要になりますので、メモに書き込む必要があります。 メモ帳は、この目的に合った機能を提供します。

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>アプリを Microsoft Teams に展開する

この時点で、アプリはインターネットでホストされますが、検索する場所やアプリの呼び出し先を Teams にまだ伝える方法はありません。 これを行うには、アプリ パッケージを作成する必要があります。 これは、アプリ マニフェストと、Teams クライアントがアプリを適切に表示およびブランド化するために使用する一部のアイコンを含むテキスト ファイルに近いファイルです。 このアプリ パッケージを手動で作成するか、アプリを登録するプロセスを簡素化する Teams で実行されるツールである App Studio を使用できます。 App Studio は、アプリ パッケージの作成と更新を行う場合に推奨される方法です。

どちらの方法でも、以下が必要です。

- アプリがインターネット上で見つかる URL。
- Teams がアプリのブランド化に使用するアイコン。 サンプルには、"src\static\images" にあるプレースホルダー アイコンが付属しています。 App Studio では、必要に応じて既定のアイコンも提供されます。

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>ホストされているアプリを更新する

サンプル アプリでは、前にメモした値に次の環境変数を設定する必要があります。

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

その方法は、アプリのホスト方法によって異なります。 環境変数の使用に関する重要な点は、これらの値は環境の一部であり、アプリのコードからアクセスできますが、サイトを構成するファイルを調べるサード パーティには公開されません。

ngrok を使ってアプリを実行している場合は、ローカル環境変数を設定する必要があります。 これを行うには多くの方法がありますが、Visual Studio Code を使用している場合は、起動構成を [追加するのが最も簡単です](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)。

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

MICROSOFT_APP_IDとMICROSOFT_APP_PASSWORDは、ボットの ID とパスワードです。
NODE_DEBUGコード デバッグ コンソールでボットで何が起きているVisual Studio表示されます。
NODE_CONFIG_DIRリポジトリのルートにあるディレクトリをポイントします (既定では、アプリがローカルで実行されている場合は、src フォルダーで検索されます)。

> [!Note]
> このチュートリアルの前の方から npm を停止していない場合は、Visual Studio Code が起動構成変数を正しくピックアップするために実行する `npm stop` 必要があります。

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>[アプリ] タブを構成する

アプリをチームにインストールしたら、コンテンツを表示するためにアプリを構成する必要があります。 チーム内のチャネルに移動し **、[+]** ボタンをクリックして新しいタブを追加します。その後、[タブ `Hello World` の追加] **ボックスの一覧から選択** できます。 構成ダイアログが表示されます。 このダイアログでは、このチャネルに表示するタブを選択できます。 タブを選択してクリックすると、選択したタブと一緒に読み `Save` `Hello World` 込まれたタブが表示されます。

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" alt-text="Screenshot of configure" />

### <a name="test-your-bot-in-teams"></a>Teams でボットをテストする

Teams でボットを操作できます。 アプリを登録したチームのチャネルを選択し、メッセージを入力して `@your-bot-name` 入力します。 これはメンションと呼 **\@ ばれる。** ボットに送信したメッセージは、返信として返送されます。

<img width="450px" alt-text="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある 3 つのドットをクリックします。 メニューに **"Hello World"** アプリが表示されます。 クリックすると、ランダムなテキストが多数表示されます。 You can choose any one of them and it will be inserted it into your conversation.

<img width="430px" alt-text="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt-text="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

ランダムなテキストのいずれかを選択すると、カードがフォーマットされ、下部に独自のメッセージと一緒に送信する準備が整っているのが表示されます。

<img width="430px" alt-text="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
