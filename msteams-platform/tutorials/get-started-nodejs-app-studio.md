---
title: チュートリアル - アプリを使用して最初のアプリをNode.js
description: Microsoft Teams アプリの作成を開始する方法については、Node.js。
keywords: nodejs App Studio node.jsの開始方法
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: ae1b8b2b5b671488ff6f86a3a3295f448ebb6006
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020962"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a>ユーザー設定を使用して最初の Microsoft Teams アプリをNode.js

このチュートリアルでは、アプリを使用して Microsoft Teams アプリの作成を開始Node.js。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>アプリをダウンロードしてホストする

Teams で簡単な "hello world" アプリをダウンロードしてホストするには、次の手順に従います。

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>前提条件の取得

このチュートリアルを完了するには、次のツールが必要です。 まだインストールしていない場合は、これらのリンクからインストールできます。

- [Git](https://git-scm.com/downloads)
- [Node.js NPM](https://nodejs.org/)
- 任意のテキスト エディターまたは IDE を取得します。 コードを無料でインストール [Visual Studio使用](https://code.visualstudio.com/download) できます。

インストール中に、追加、および PATH のオプションが表示される場合は `git` `node` `npm` `code` 、そのオプションを選択します。 便利です。

ターミナル ウィンドウで次のコマンドを実行して、ツールが使用可能な状態を確認します。

> [!NOTE]
> プラットフォームで最も快適なターミナル ウィンドウを使用します。 これらの例では Bash (Git に含まれています) を使用しますが、これらのスクリプトはほとんどのプラットフォームで実行されます。

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

gulp がインストールされていない (または正しいバージョンがインストールされている) 場合は、ターミナル ウィンドウで `npm install gulp` 実行します。

コードをインストールしたVisual Studio、次のコマンドを実行してインストールを確認できます。

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

このターミナル ウィンドウを引き続き使用して、このチュートリアルに従うコマンドを実行できます。

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>サンプルをダウンロードする

シンプルな Hello, [World を提供しました。](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs) サンプルを使用して開始します。 ターミナル ウィンドウで、次のコマンドを実行して、サンプル リポジトリをローカル コンピューターに複製します。

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> 今後の [参照のために](https://help.github.com/articles/fork-a-repo/) [GitHub](https://github.com/OfficeDev/Microsoft-Teams-Samples) リポジトリへの変更を変更してチェックインする場合は、このリポジトリをフォークできます。

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a>サンプルの構築と実行

リポジトリが複製された後、サンプルを保持するディレクトリに変更します。

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

サンプルをビルドするには、すべての依存関係をインストールする必要があります。 これを行うには、次のコマンドを実行します。

```bash
npm install
```

多くの依存関係がインストールされているのが表示されます。 完了したら、アプリを実行できます。

```bash
npm start
```

hello-world アプリが起動すると、ターミナル `App started listening on port 3333` ウィンドウに表示されます。

> [!NOTE]
> 上記のメッセージに別のポート番号が表示される場合は、PORT 環境変数が設定されているためです。 引き続きそのポートを使用するか、環境変数を 3333 に変更できます。

この時点で、ブラウザー ウィンドウを開き、次の URL に移動して、すべてのアプリ URL が読み込まれるか確認できます。

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>サンプル アプリをホストする

Microsoft Teams のアプリは、1 つ以上の機能を公開する Web アプリケーションです。 Teams プラットフォームでアプリを読み込むには、アプリにインターネットからアクセスできる必要があります。 インターネットからアプリにアクセスするには、アプリを *ホストする* 必要があります。

ローカル テストでは、ローカル コンピューターでアプリを実行し、Web エンドポイントを使用してトンネルを作成できます。 [ngrok](https://ngrok.com) は無料のツールで、それを実行できます。 *ngrok を使用* すると、次のような Web アドレスを取得できます `https://d0ac14a5.ngrok.io` (この URL は単なる例です)。 環境に [合った](https://ngrok.com/download) *ngrok をダウンロード* してインストールできます。 必ず、このファイルを自分の場所に追加してください `PATH` 。

インストールしたら、新しいターミナル ウィンドウを開き、次のコマンドを実行してトンネルを作成できます。 このサンプルではポート 3333 を使用します。

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok は* インターネットからの要求をリッスンし、ポート 3333 で実行されているアプリにルーティングします。 ブラウザーを開き、アプリの hello ページを読み込 `https://d0ac14a5.ngrok.io/hello` む方法で確認できます。 この URL ではなく、コンソール セッションで *ngrok* によって表示される転送アドレスを必ず使用してください。

> [!NOTE]
> 上記のビルドと実行手順で別の [](#build-and-run-the-sample)ポートを使用している場合は、同じポート番号を使用して *ngrok トンネルをセットアップ* してください。
> [!TIP]
> 別のターミナル ウィンドウで *ngrok* を実行して、後で停止、再構築、再実行が必要になるノード アプリを妨げることなく実行し続けるのをお考えください。 *ngrok セッションは*、このウィンドウで有用なデバッグ情報を返します。

永続的な名前を許可する *有料バージョンの ngrok* があります。 無料版を使用する場合、アプリは開発マシンの現在のセッション中にのみ利用できます。 コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。 他のユーザーがテスト用にアプリを共有する場合は、このことを覚えておいてください。 サービスを再起動する必要がある場合は、新しいアドレスが返され、そのアドレスを使用する場所を更新する必要があります。

アプリを Teams に登録するときに後で必要になるアプリの URL をメモしてください。 メモ帳は、この目的のために正常に動作します。

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>アプリを Microsoft Teams に展開する

この時点で、アプリはインターネット上でホストされますが、検索場所やアプリの呼び出し先を Teams にまだ伝える方法はありません。 これを行うには、アプリ パッケージを作成する必要があります。 これは、アプリ マニフェストと、Teams クライアントがアプリを適切に表示およびブランド化するために使用するアイコンを含むテキスト ファイルにすら及びしません。 このアプリ パッケージを手動で作成するか、アプリの登録プロセスを簡略化する Teams で実行されるツールである App Studio を使用できます。 App Studio は、アプリ パッケージを作成および更新する推奨される方法です。

どちらの方法でも、次の値が必要です。

- アプリがインターネット上で見つかる URL。
- Teams がアプリのブランド化に使用するアイコン。 サンプルには、"src\static\images" にあるプレースホルダー アイコンが付属しています。 App Studio では、必要に応じて既定のアイコンも表示されます。

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>ホストされたアプリを更新する

サンプル アプリでは、前にメモした値に次の環境変数を設定する必要があります。

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

その方法は、アプリのホスト方法によって異なります。 環境変数を使用する重要な点は、これらの値は環境の一部であり、アプリのコードからアクセスできますが、サイトを構成するファイルを調べるサードパーティには公開されません。

ngrok を使用してアプリを実行している場合は、いくつかのローカル環境変数を設定する必要があります。 これを行うには多くの方法がありますが、コードを使用している場合は、Visual Studio起動構成を [追加するのが最も簡単です](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)。

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
NODE_DEBUGコード デバッグ コンソールでボットで何が起こっているかVisual Studio表示されます。
NODE_CONFIG_DIRリポジトリのルートにあるディレクトリをポイントします (既定では、アプリをローカルで実行すると、src フォルダーで検索されます)。

> [!Note]
> チュートリアルの前のバージョンから npm を停止していない場合は、Visual Studio コードで起動構成変数を正しく取得するために実行する `npm stop` 必要があります。

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>[アプリ] タブの構成

アプリをチームにインストールしたら、コンテンツを表示するためにアプリを構成する必要があります。 チーム内のチャネルに移動し **、[+]** ボタンをクリックして新しいタブを追加します。次に、[タブ `Hello World` の追加 **] リストから選択** できます。 その後、構成ダイアログが表示されます。 このダイアログでは、このチャネルに表示するタブを選択できます。 タブを選択してクリックすると `Save` 、選択したタブが読 `Hello World` み込まれたタブが表示されます。

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>Teams でボットをテストする

Teams でボットを操作できます。 アプリを登録したチーム内のチャネルを選択し、「」と入力し `@your-bot-name` 、その後にメッセージを入力します。 これはメンションと呼 **\@ ばれる.** ボットに送信したメッセージは、返信として返されます。

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

メッセージング拡張機能をテストするには、会話ビューの入力ボックスの下にある 3 つのドットをクリックします。 メニューに「Hello **World」アプリが** 表示されます。 クリックすると、ランダムなテキストが多数表示されます。 任意の 1 つを選択すると、会話に挿入されます。

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

ランダムなテキストのいずれかを選択すると、カードが書式設定され、下部に独自のメッセージを送信する準備が整いました。

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
