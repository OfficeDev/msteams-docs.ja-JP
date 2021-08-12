---
title: 開始方法 - 前提条件
author: adrianhall
description: アプリ開発の開始と環境Microsoft Teamsする方法について学習します。
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 2945490d70023a620bad43b618789164aa915d8a
ms.sourcegitcommit: 6a41c529a423c81a184c7a79125dbaaed0179788
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2021
ms.locfileid: "53585999"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a>前提条件: アプリ開発Microsoft Teams開始する

最初のアプリの作成を開始するTeams、いくつかのツールをインストールして、開発環境をセットアップする必要があります。

## <a name="install-required-tools"></a>必要なツールのインストール

必要なツールの一部は、アプリのビルド方法によってTeamsがあります。

- [Node.js](https://nodejs.org/en/download/) (最新の v14 LTS リリースを使用する)
- 開発者ツール (推奨) や[](https://www.microsoft.com/edge)Google [Chrome](https://www.google.com/chrome/)などのMicrosoft Edgeブラウザー
- JavaScript、TypeScript、または SharePoint Framework (SPFx) を使用して開発する場合は、Visual Studio Code[バージョン](https://code.visualstudio.com/download)1.55 以降をインストールします。  
- .NET を使用して開発している場合は[、2019 Visual Studioインストールします](https://visualstudio.com/download)。 必ず、ASP.NET **Web 開発ワークロードまたは** **.NET Core クロス** プラットフォーム開発ワークロードをインストールします。

> [!WARNING]
> Node v15 以降でパッケージ `npm@7` 化された既知の問題があります。 実行中に問題がある場合は `npm install` 、Node v14 (LTS) を使用している必要があります。

## <a name="install-the-teams-toolkit"></a>サーバーをインストールTeams Toolkit

このTeams Toolkitは、アプリのクラウド リソースをプロビジョニングおよび展開するツール、アプリ ストアに発行するツールを使用して開発プロセスを簡略化Teams役立ちます。 このツールキットは、Visual Studio Code、Visual Studio CLI (呼び出し) として使用できます `teamsfx` 。 詳細については[、「Teams Toolkit」、Visual Studio Code Teams Toolkit](../toolkit/visual-studio-code-overview.md) [Teamsfx](../toolkit/visual-studio-overview.md) CLI ツールVisual Studio[を参照してください](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli)。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Visual Studio Code を開きます。
1. [拡張機能 **] ビューを選択** します **(Ctrl + Shift + X**  /  **の場合は 、2** つ以上の拡張子を>**します**)。
1. 検索ボックスに「Teams Toolkit」**と入力します**。
1. [インストール **] の** 横にある [インストール] をTeams Toolkit。

また、マーケットプレースでTeams ToolkitをVisual Studio Code[できます](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

次のツールは、必要に応Visual Studio Code拡張機能によってインストールできます。 既にインストールされている場合は、インストールされているバージョンを代わりに使用できます。 WSL を含む Linux を使用する場合は、使用する前に次のツールをインストールする必要があります。

- [Azure Functions コア ツール](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools は、Azure でサービスを実行するときに必要な認証ヘルパーを含む、ローカル デバッグ実行時にバックエンド コンポーネントをローカルで実行するために使用されます。 プロジェクト ディレクトリ内にインストールされます (npm を使用 `devDependencies` )。

- [.NET SDK](/dotnet/core/install/)

    .NET SDK は、ローカル デバッグと Azure Functions アプリの展開用にカスタマイズされたバインドをインストールするために使用されます。 .NET 3.1 (以降) SDK をグローバルにインストールしていない場合は、ポータブル バージョンをインストールできます。

- [ngrok](https://ngrok.com/download)

    一部Teamsアプリ機能 (会話型ボット、メッセージング拡張機能、受信 Webhook) では、受信接続が必要です。 開発システムをトンネル経由でTeamsする必要があります。 タブのみを含むアプリでは、トンネルは必要ありません。 このパッケージは、(npm を使用して) プロジェクト ディレクトリ内にインストールされます `devDependencies` 。

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

2019 Visual Studioを使用して、.NET Teams Blazor Server を使用してアプリを開発できます。 .NET でアプリを開発するTeams場合は、Visual Studio CodeバージョンをインストールTeams Toolkit。

拡張機能をインストールTeams Toolkitするには、次の手順を実行します。

1. 2019 Visual Studioを開きます。
1. [拡張機能 **の管理**  >  **] を選択します**。
1. 検索ボックスに「Teams Toolkit」**と入力します**。
1. 拡張機能を選択Teams Toolkitし、[ダウンロード] を **選択します**。 拡張機能がダウンロードされます。
1. 2019 Visual Studio閉じて、拡張機能をインストールします。

# <a name="command-line"></a>[コマンド ライン](#tab/cli)

TeamsFx CLI をインストールするには、パッケージ マネージャーを `npm` 使用します。

``` bash
npm install -g @microsoft/teamsfx-cli
```

構成によっては、CLI のインストールに使用 `sudo` する必要がある場合があります。

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

これは、Linux および macOS システムではより一般的です。

npm グローバル キャッシュを PATH に追加してください。 これは、通常、インストーラーの一部としてNode.jsされます。  

コマンドで CLI を使用 `teamsfx` できます。 コマンドを実行して動作を確認します `teamsfx -h` 。

> [!CAUTION]
> PowerShell ターミナルで TeamsFx を実行する前に、PowerShell の "リモート署名済み" 実行ポリシーを有効にする必要があります。 詳細については [、PowerShell のドキュメントを参照してください](/powershell/module/microsoft.powershell.core/about/about_signing)。

---

## <a name="install-optional-tools"></a>オプション のツールをインストールする

アプリ開発用のブラウザー ツールをインストールします。 たとえば、アプリがアプリを使用して作成されている場合React開発者ツールReact使用できます。

- [ReactChrome の開発者向けツール](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

Azure に格納されているデータにアクセスする場合、または Azure のアプリ用にクラウドベースのバックエンドを展開Teams、次のツールをインストールします。

- [Azure Tools for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [Azure CLI](/cli/azure/install-azure-cli)

Microsoft のデータをGraphする場合は、Microsoft データベース エクスプローラーについて説明し、ブックマークGraph必要があります。 このブラウザー ベースのツールを使用すると、アプリの外部で Microsoft Graphクエリを実行できます。

- [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)

開発者ポータル for Teamsを使用すると、Teams アプリを構成、管理、および配布できます。組織または Teams ストアにTeamsできます。

- [Teams の開発者ポータル](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a>サイドローディングを有効にする

開発中は、アプリを配布せずにアプリTeams読み込む必要があります。 これはサイドローディングと呼ばれる。

アプリ アカウントをお持Teams、アプリをサイドロードできるアプリを次Teams。

1. クライアントで、[Teams] を **選択します**。
1. カスタム **アプリアップロードを選択します**。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="カスタム アプリをアップロードTeams場所を示す図。":::

> [!NOTE]
> アプリをサイドロードできない場合は、管理者にTeamsしてください。 詳細[については、「カスタム Teamsアプリを有効](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)にする」を参照し、カスタム アプリのアップロードを有効にするを参照してください。

## <a name="get-a-free-teams-developer-tenant-optional"></a>開発者テナントの無料Teams取得 (オプション)

サイドロード オプションが表示されない場合、または Teams アカウントがない場合は、M365 開発者プログラムに参加することで無料の Teams 開発者アカウントを取得できます。  登録プロセスには約 2 分かかります。

1. 開発者プログラムの[Microsoft 365に移動します](https://developer.microsoft.com/microsoft-365/dev-program)。
1. [今 **すぐ参加] を** 選択し、画面の指示に従います。
1. ようこそ画面で **、[E5 サブスクリプションの設定] を選択します**。
1. 管理者アカウントを設定します。 完了すると、次のような画面が表示されます。

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="開発者プログラムにサインアップした後に表示されるMicrosoft 365例。":::

1. セットアップしTeams管理者アカウントを使用してサインインします。 カスタム アプリ オプションのアップロード **確認** します。

## <a name="get-a-free-azure-account"></a>無料の Azure アカウントを取得する

アプリをホストするか、Azure 内のリソースにアクセスする場合は、Azure サブスクリプションが必要です。  開始する [前に無料アカウント](https://azure.microsoft.com/free/) を作成できます。

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a>アカウントと Azure アカウントMicrosoft 365サインインする

次の 2 つのアカウントにアクセスできる必要があります。

- アカウントMicrosoft 365資格情報。 これは、アカウントにサインインするために使用するアカウントTeams。 開発者プログラム のテナントMicrosoft 365場合、これはプログラムの登録時に設定した管理者アカウントです。
- Azure 資格情報。 これは、Azure Portal へのアクセスと、アプリをサポートする新しいクラウド リソースのプロビジョニングに使用するアカウントです。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. 開Visual Studio Code
1. サイドバーでTeamsアイコンを選択します。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. **[M365 にサインインする] を選択します**。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="サインインに使用する [アカウント] セクションの場所。":::

    サインイン プロセスは、通常の Web ブラウザーの使用を開始します。 M365 アカウントのサインイン プロセスを完了します。 プロンプトが表示されたら、ブラウザーを閉じて、ブラウザーに戻Visual Studio Code。
1. データ内のTeams Toolkitに戻Visual Studio Code。
1. [Azure **にサインインする] を選択します**。

    > [!TIP]
    > Azure Account 拡張機能がインストールされ、同じアカウントを使用している場合は、この手順を省略できます。 他の拡張機能で使用しているアカウントと同じアカウントを使用します。

1. サインイン プロセスは、通常の Web ブラウザーの使用を開始します。  Azure アカウントのサインイン プロセスを完了します。 プロンプトが表示されたら、ブラウザーを閉じて、ブラウザーに戻Visual Studio Code。

    完了すると、 **サイドバーの [ACCOUNTS]** セクションには、使用可能な Azure サブスクリプションの数と共に、2 つのアカウントが個別に表示されます。 使用可能な Azure サブスクリプションが少なくとも 1 つ用意されている必要があります。 サインインしていない場合は、サインアウトして別のアカウントを使用します。

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Visual Studio 2019 では、必要に応じて各サービスにログインするように求めるメッセージが表示されます。 事前に M365 アカウントと Azure アカウントにサインインする必要はありません。

# <a name="command-line"></a>[コマンド ライン](#tab/cli)

1. TeamsFx CLI を使用Microsoft 365サインインして、次のコマンドを実行します。

    ``` bash
    teamsfx account login m365
    ```

    サインイン プロセスは、通常の Web ブラウザーの使用を開始します。 M365 アカウントのサインイン プロセスを完了します。 ブラウザーを閉じるときにメッセージが表示されます。

2. TeamsFx CLI を使用して Azure にサインインします。

    ``` bash
    teamsfx account login azure
    ```

    サインイン プロセスは、通常の Web ブラウザーの使用を開始します。 Azure アカウントのサインイン プロセスを完了します。 ブラウザーを閉じるときにメッセージが表示されます。

    アカウント ログインは、ユーザーと TeamsFx CLI Visual Studio Code共有されます。



    開発環境が構成されたので、最初のアプリを作成、ビルド、およびTeamsできます。

## <a name="see-also"></a>関連項目

* [チュートリアルの概要](code-samples.md) 
* [アプリを使用してアプリを作成React](first-app-react.md)
* [Blazor を使用してアプリを作成する](first-app-blazor.md)
* [アプリを使用してアプリを作成SPFx](first-app-spfx.md)
* [C# を使用してアプリを作成する](get-started-dotnet-app-studio.md)
* [Node.js を使ってアプリを作成する](get-started-nodejs-app-studio.md)
* [Yeoman ジェネレーターを使用してアプリを作成する](get-started-yeoman.md)
* [会話ボット アプリを作成する](first-app-bot.md)
* [メッセージング拡張機能を作成する](first-message-extension.md)
* [コード サンプル](https://github.com/OfficeDev/Microsoft-Teams-Samples)
