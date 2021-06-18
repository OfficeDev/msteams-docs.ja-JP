---
title: 開始方法 - 前提条件
author: adrianhall
description: Microsoft Teams アプリの開発を開始し、環境をセットアップする方法について説明します。
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 6496d238b3858c1df974732fa57c28eed7c54eb2
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994190"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a>前提条件: Microsoft Teams アプリ開発の開始

最初の Teams アプリを作成する前に、いくつかのツールをインストールし、開発環境をセットアップする必要があります。

## <a name="install-required-tools"></a>必要なツールのインストール

必要なツールの一部は、Teams アプリの構築方法によって異なっています。

- [Node.js](https://nodejs.org/en/download/) (最新の v14 LTS リリースを使用する)
- Microsoft [Edge](https://www.microsoft.com/edge) (推奨) や[Google Chrome](https://www.google.com/chrome/)などの開発者ツールを含むブラウザー
- JavaScript、TypeScript、または SharePoint Framework (SPFx) を使用して開発する場合は、Visual Studio [コードバージョン](https://code.visualstudio.com/download)1.55 以降をインストールします。  
- .NET を使用して開発する場合は [、2019 Visual Studioインストールします](https://visualstudio.com/download)。 必ず、ASP.NET **Web 開発ワークロードまたは** **.NET Core クロスプラットフォーム開発ワークロードをインストール** します。

> [!WARNING]
> Node v15 以降でパッケージ `npm@7` 化された既知の問題があります。 実行中に問題がある場合は `npm install` 、Node v14 (LTS) を使用している必要があります。

## <a name="install-the-teams-toolkit"></a>Teams サーバーをインストールToolkit

Teams Toolkitは、アプリ用のクラウド リソースのプロビジョニングと展開、Teams ストアへの発行など、ツールを使用して開発プロセスを簡略化するのに役立ちます。 ツールキットは、コード、Visual Studio、または CLI (Visual Studio) として使用できます `teamsfx` 。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Visual Studio Code を開きます。
1. [拡張機能] ビューを選択します **(Ctrl + Shift +**  /   **>** X
1. 検索ボックスに **、「Teams」と入力Toolkit。**
1. Teams サーバーの横にある緑色のインストール ボタンをToolkit。

Teams ファイルは、コード マーケットプレースToolkitでVisual Studio [できます](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

次のツールは、必要に応Visual Studioコード拡張機能によってインストールできます。 既にインストールされている場合は、インストールされているバージョンを代わりに使用できます。 WSL を含む Linux を使用する場合は、使用する前に次のツールをインストールする必要があります。

- [Azure Functions コア ツール](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools は、Azure でサービスを実行するときに必要な認証ヘルパーを含む、ローカル デバッグ実行時にバックエンド コンポーネントをローカルで実行するために使用されます。 プロジェクト ディレクトリ内にインストールされます (npm を使用 `devDependencies` )。

- [.NET SDK](/dotnet/core/install/)

    .NET SDK は、ローカル デバッグと Azure Functions アプリの展開用にカスタマイズされたバインドをインストールするために使用されます。 .NET 3.1 (以降) SDK をグローバルにインストールしていない場合は、ポータブル バージョンをインストールできます。

- [ngrok](https://ngrok.com/download)

    Teams アプリの一部の機能 (会話型ボット、メッセージング拡張機能、受信 Webhook) では、受信接続が必要です。 開発システムをトンネル経由で Teams に公開する必要があります。 タブのみを含むアプリでは、トンネルは必要ありません。 このパッケージは、(npm を使用して) プロジェクト ディレクトリ内にインストールされます `devDependencies` 。

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

2019 Visual Studioを使用して、.NET で Blazor Server を使用して Teams アプリを開発できます。 .NET で Teams アプリを開発する予定がない場合は、Teams アプリの Visual Studio コード バージョンをインストールToolkit。

Teams の拡張機能をToolkitするには、次の手順を実行します。

1. 2019 Visual Studioを開きます。
1. [拡張機能 **の管理**  >  **] を選択します**。
1. 検索ボックスに **、「Teams」と入力Toolkit。**
1. Teams の拡張機能をToolkitし、[ダウンロード] を **選択します**。

拡張機能はダウンロードできます。 2019 Visual Studio閉じて、拡張機能をインストールします。

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

アプリ開発用のブラウザー ツールをインストールします。 たとえば、アプリが React で記述されている場合は、React 開発者ツールを使用できます。

- [React Developer Tools for Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

Azure に格納されているデータにアクセスするか、Azure で Teams アプリのクラウドベースのバックエンドを展開する場合は、次のツールをインストールします。

- [Azure Tools for Visual Studio コード](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [Azure CLI](/cli/azure/install-azure-cli)

Microsoft Graph データを使用する場合は、Microsoft Graph エクスプローラーについて説明し、ブックマークする必要があります。 このブラウザー ベースのツールを使用すると、アプリの外部で Microsoft Graph にクエリを実行できます。

- [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)

Teams の開発者ポータルを使用すると、組織や Teams ストアを含む Teams アプリを構成、管理、配布できます。

- [Teams の開発者ポータル](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a>サイドローディングを有効にする

開発中は、配布せずに Teams 内でアプリを読み込む必要があります。 これは"サイドローディング" と呼ばれる。

1. Teams アカウントを持っている場合は、Teams でアプリをサイドロードできる場合を確認します。

    1. Teams クライアントで、[アプリ] を **選択します**。
    1. カスタム アプリをアップロードする **オプションを探します**。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Teams でカスタム アプリをアップロードできる場所を示す図。":::

> [!NOTE]
> アプリをサイドロードできない場合は、Teams 管理者に問い合わせてください。 詳細については [、「カスタム Teams アプリを有効にする」と「カスタム アプリのアップロードを有効にする」](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) を参照してください。

## <a name="get-a-free-teams-developer-tenant-optional"></a>無料の Teams 開発者テナントを取得する (オプション)

サイドロード オプションが表示されない場合、または Teams アカウントがない場合は、M365 開発者プログラムに参加することで、無料の Teams 開発者アカウントを取得できます。  登録プロセスには約 2 分かかります。

1. [Microsoft 365 開発者プログラムに移動します](https://developer.microsoft.com/microsoft-365/dev-program)。
1. [今 **すぐ参加] を** 選択し、画面の指示に従います。
1. ようこそ画面にアクセスすると **、[E5 サブスクリプションの設定] を選択します**。
1. 管理者アカウントを設定します。 完了すると、次のような画面が表示されます。

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Microsoft 365 開発者プログラムにサインアップした後に表示される例。":::

1. セットアップした管理者アカウントを使用して Teams にサインインします。
1. [カスタム アプリをアップロードする **] オプションが追加されたのか確認** します。

## <a name="get-a-free-azure-account"></a>無料の Azure アカウントを取得する

アプリをホストするか、Azure 内のリソースにアクセスする場合は、Azure サブスクリプションが必要です。  開始する [前に無料アカウント](https://azure.microsoft.com/free/) を作成できます。

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a>Microsoft 365 および Azure アカウントにサインインする

次の 2 つのアカウントにアクセスできる必要があります。

- Microsoft 365 アカウントの資格情報。 これは、Teams へのサインインに使用するアカウントです。 Microsoft 365 開発者プログラム テナントを使用している場合は、プログラムの登録時に設定した管理者アカウントです。
- - Azure 資格情報。 これは、Azure Portal へのアクセスと、アプリをサポートする新しいクラウド リソースのプロビジョニングに使用するアカウントです。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Open Visual Studio コード
1. サイドバーでTeamsアイコンを選択します。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. **[M365 にサインインする] を選択します**。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="サインインに使用する [アカウント] セクションの場所。":::

1. サインイン プロセスは、通常の Web ブラウザーの使用を開始します。 M365 アカウントのサインイン プロセスを完了します。 ブラウザーを閉じて、ブラウザーに戻るメッセージが表示Visual Studio Code。
1. データ内のTeams Toolkitに戻Visual Studio Code。
1. [Azure **にサインインする] を選択します**。

    > [!TIP]
    > Azure Account 拡張機能がインストールされ、同じアカウントを使用している場合は、この手順を省略できます。 他の拡張機能で使用しているアカウントと同じアカウントを使用します。

1. サインイン プロセスは、通常の Web ブラウザーの使用を開始します。  Azure アカウントのサインイン プロセスを完了します。 ブラウザーを閉じて、ブラウザーに戻るメッセージが表示Visual Studio Code。

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

---

開発環境が構成されたので、最初のアプリを作成、ビルド、およびTeamsできます。

## <a name="see-also"></a>関連項目

- [Blazor を使用してTeamsアプリを作成する](first-app-blazor.md)
- [アプリを使用してTeamsアプリをSharePoint Frameworkする (SPFx)](first-app-spfx.md)
- [会話ボット アプリを作成する](first-app-bot.md)
- [メッセージング拡張機能を作成する](first-message-extension.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アプリを使用してTeamsアプリをReact](first-app-react.md)
