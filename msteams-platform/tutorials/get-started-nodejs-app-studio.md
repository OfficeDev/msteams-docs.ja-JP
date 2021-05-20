---
title: チュートリアル - Node.jsを使用して最初のアプリを作成する
description: Node.jsを使用してMicrosoft Teamsアプリの構築を開始する方法について説明します。
keywords: nodejs アプリケーションスタジオnode.js始める
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 46272671443e07432513b667af424b5c5be05f2e
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566542"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a>Node.jsを使用して初めてのMicrosoft Teams アプリを作成する

このチュートリアルでは、Node.jsを使用してMicrosoft Teams アプリの作成を開始できます。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>アプリをダウンロードしてホストする

Teamsでシンプルな「hello world」アプリをダウンロードしてホストするには、次の手順に従います。

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>前提条件の取得

このチュートリアルを完了するには、次のツールが必要です。 まだお持ちの場合は、これらのリンクからインストールできます。

- [Git](https://git-scm.com/downloads)
- [Node.jsと NPM](https://nodejs.org/)
- 任意のテキスト エディタまたは IDE を取得します。 [Visual Studio Code](https://code.visualstudio.com/download)を無料でインストールして使用できます。

インストール時に 、 `git` 、 、 のインストール時に PATH に追加するオプションが表示された場合 `node` `npm` `code` は、このオプションを選択します。 それは便利になります。

ターミナル ウィンドウで次のツールを実行して、ツールが使用可能であることを確認します。

> [!NOTE]
> プラットフォーム上で最も快適なターミナルウィンドウを使用します。 これらの例では Bash (Git に含まれています) を使用していますが、これらのスクリプトはほとんどのプラットフォームで実行されます。

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

これらのアプリケーションのバージョンが異なる場合があります。 これは、gulp を除いて問題となるべきではありません。 gulp の場合は、バージョン 4.0.0 以降を使用する必要があります。

gulp がインストールされていない場合(または間違ったバージョンがインストールされている場合)は、 `npm install gulp` ターミナルウィンドウで実行して実行してください。

Visual Studio Codeをインストールした場合は、次の手順を実行してインストールを確認できます。

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

このターミナル ウィンドウを引き続き使用して、このチュートリアルのコマンドを実行できます。

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>サンプルをダウンロードする

私たちは、シンプルな [こんにちは、世界を提供しています!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs) サンプルを使用して開始します。 ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをローカル マシンに複製します。

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> 今後の参照のために、GitHub[レポ](https://github.com/OfficeDev/Microsoft-Teams-Samples)への変更を変更してチェックインする場合は、このレポを[フォーク](https://help.github.com/articles/fork-a-repo/)できます。

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a>サンプルの構築と実行

リポジトリのクローンが作成されたら、サンプルを保持しているディレクトリに移動します。

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

サンプルをビルドするには、すべての依存関係をインストールする必要があります。 これを行うには、次のコマンドを実行します。

```bash
npm install
```

インストールされる依存関係の一群が表示されます。 完了したら、アプリを実行できます。

```bash
npm start
```

hello-world アプリが起動すると、 `App started listening on port 3333` ターミナル ウィンドウに表示されます。

> [!NOTE]
> 上記のメッセージに異なるポート番号が表示される場合は、PORT 環境変数が設定されているためです。 そのポートを引き続き使用するか、または環境変数を 3333 に変更できます。

この時点で、ブラウザー ウィンドウを開き、次の URL に移動して、すべてのアプリ URL が読み込まれているかどうかを確認できます。

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>サンプル アプリをホストする

Microsoft Teamsのアプリは、1 つ以上の機能を公開する Web アプリケーションであることを忘れないでください。 アプリを読み込むTeamsプラットフォームでは、インターネットからアプリにアクセスできる必要があります。 インターネットからアプリにアクセスできるようにするには、アプリを *ホスト* する必要があります。

ローカル テストの場合は、ローカル コンピューターでアプリを実行し、Web エンドポイントを使用してアプリへのトンネルを作成できます。 [ngrok](https://ngrok.com) は、あなたがそれを行うことができます無料のツールです。 *ngrok* を使用すると、( `https://d0ac14a5.ngrok.io` このURLは単なる例です)などのウェブアドレスを取得することができます。 ご使用の環境に *合わせて ngrok* を [ダウンロードしてインストール](https://ngrok.com/download)できます。 で、必ず その場所に追加してください `PATH` 。

インストール後、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成できます。 サンプルではポート 3333 を使用するため、ここで指定してください。

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok* はインターネットからのリクエストを聞き、ポート3333で実行されているアプリにルーティングします。 ブラウザーを開いて `https://d0ac14a5.ngrok.io/hello` 、アプリの hello ページを読み込むことで確認できます。 この URL ではなく、コンソール セッションで *ngrok* で表示される転送先アドレスを使用してください。

> [!NOTE]
> 上記の [ビルドと実行](#build-and-run-the-sample) 手順で別のポートを使用している場合は *、ngrok* トンネルを設定するために同じポート番号を使用してください。
> [!TIP]
> ngrok を別のターミナル ウィンドウで実行して、後で停止、再構築、再実行する必要があるノード アプリに干渉することなく *、ngrok* を実行し続けることをお勧めします。 *ngrok* セッションは、このウィンドウで有益なデバッグ情報を返します。

永続的な名前を許可する *ngrok* の有料版があります。 無料版を使用する場合、アプリは開発マシン上の現在のセッション中にのみ利用できます。 マシンがシャットダウンされた場合、またはスリープ状態になると、サービスは利用できなくなります。 他のユーザーによるテスト用アプリを共有する場合は、この点に注意してください。 サービスを再起動する必要がある場合は、新しいアドレスを返し、そのアドレスを使用するすべての場所を更新する必要があります。

アプリスタジオを使用してアプリを登録するときには後で必要になるので、アプリのURL Teams書き留めておいてください。 メモ帳は、この目的のために正常に動作します。

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>アプリをMicrosoft Teamsに展開する

この時点で、インターネット上でホストされているアプリがありますが、Teamsに探す場所やアプリが呼び出される場所を伝える方法はまだありません。 これを行うには、アプリ パッケージを作成する必要があります。 これは、アプリ マニフェストと、Teams クライアントがアプリを適切に表示およびブランド化するために使用するアイコンを含むテキスト ファイルに過ぎません。 このアプリ パッケージを手動で作成することも、アプリの登録プロセスを簡略化するTeamsで実行されるツールである App Studio を使用することもできます。 アプリの Studio は、アプリ パッケージを作成および更新する推奨される方法です。

どちらの方法でも、次のことが必要です。

- インターネット上でアプリを見つけることができる URL。
- アプリのブランド化に使用Teamsアイコン。 サンプルには、"src\static\images" にあるプレースホルダ アイコンが付属しています。 必要に応じて、アプリスタジオにもデフォルトのアイコンが表示されます。

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>ホストされたアプリを更新する

サンプル アプリでは、次の環境変数を、前にメモした値に設定する必要があります。

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

アプリのホスト方法によって、その方法が異なります。 環境変数を使用する場合に重要なことは、これらの値が環境の一部であり、アプリのコードでアクセスできますが、サイトを構成するファイルを調べる可能性のあるサードパーティには公開されないことです。

ngrok を使用してアプリを実行している場合は、いくつかのローカル環境変数を設定する必要があります。 これを行うには多くの方法がありますが、Visual Studio Codeを使用している場合は、[起動設定](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)を追加するのが最も簡単です。

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

MICROSOFT_APP_IDとMICROSOFT_APP_PASSWORDは、それぞれボットの ID とパスワードです。
NODE_DEBUGは、Visual Studio Codeデバッグコンソールでボットで何が起こっているかを示します。
NODE_CONFIG_DIRはリポジトリのルートにあるディレクトリを指します (既定では、アプリがローカルで実行されている場合は、src フォルダー内で検索されます)。

> [!Note]
> チュートリアルの前半で npm を停止していない場合は `npm stop` 、Visual Studio Code起動設定変数を正しくピックアップするために実行する必要があります。

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>アプリ タブを構成する

チームにアプリをインストールしたら、コンテンツを表示するようにアプリを構成する必要があります。 チーム内のチャンネルに移動し **、'+'** ボタンをクリックして新しいタブを追加します。[ `Hello World` **タブの追加]** リストから選択できます。 その後、構成ダイアログが表示されます。 このダイアログでは、このチャンネルに表示するタブを選択できます。 タブを選択してクリックすると `Save` 、 `Hello World` 選択したタブがロードされたタブが表示されます。

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>Teamsでボットをテストする

これで、Teamsでボットと対話できます。 アプリを登録したチームのチャンネルを選択し、「」と入力 `@your-bot-name` し、メッセージを入力します。 これはメンションと呼 **\@ ばれます**。 ボットに送信したメッセージは、返信として返信されます。

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある 3 つのドットをクリックします。 メニューには **「ハローワールド」** アプリが表示されます。 クリックすると、ランダムなテキストが多数表示されます。 あなたはそれらのいずれかを選択することができ、それはあなたの会話にそれを挿入されます:

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

ランダムなテキストのいずれかを選択すると、カードがフォーマットされ、下部に独自のメッセージを送信する準備が整っています。

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
