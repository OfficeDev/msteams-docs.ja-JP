---
title: Microsoft Teams ツールキットと Visual Studio Code を使用してアプリを構築する
description: アプリを使用して、アプリ内で直接素晴らしいカスタム Visual Studio Codeを構築Microsoft Teams Toolkit
keywords: teams visual studio コード ツールキット
ms.localizationpriority: medium
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 0413edf1e0a724c193570c5828a6f7ca51277bc3
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435818"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>アプリとアプリのTeams ToolkitをVisual Studio Code

Visual Studio Code Teams Toolkit は、開発者が統合 ID、クラウド ストレージへのアクセス、Microsoft Graph からのデータ、Azure および Microsoft 365 の他のサービスを備えた Teams アプリを作成および展開し、開発者エクスペリエンスに対する "ゼロ構成" アプローチで役立ちます。  

また、このツールキットは、Visual Studio CLI (と呼ばれる) として使用することもできます`teamsfx`。

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>インストール用のTeams ToolkitをインストールVisual Studio Code

1. Visual Studio Code を開きます。
1. [拡張機能] ビュー (**Ctrl + Shift +** **X-1** /  または **[拡張機能の表示] >します**)。
1. 検索ボックスに「Teams Toolkit」_と入力します_。
1. [インストール] ウィンドウの横にある緑色のインストール ボタンTeams Toolkit。

また、マーケットプレースTeams Toolkitを[Visual Studio Codeできます](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

次のツールは、必要に応Visual Studio Code拡張機能によってインストールされます。 既にインストールされている場合は、インストールされているバージョンが代わりに使用されます。 Linux (WSL を含む) を使用する場合は、次のツールをインストールしてから使用する必要があります。

- [Azure Functions コア ツール](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools は、Azure でサービスを実行するときに必要な認証ヘルパーを含む、ローカル デバッグ実行時にバックエンド コンポーネントをローカルで実行するために使用されます。 これは、npm を使用してプロジェクト ディレクトリ内にインストールされます `devDependencies`。

- [.NET SDK](/dotnet/core/install/)

    .NET SDK は、ローカル デバッグと Azure Functions アプリの展開用にカスタマイズされたバインドをインストールするために使用されます。 .NET 3.1 以降の SDK をグローバルにインストールしていない場合は、ポータブル バージョンがインストールされます。

- [ngrok](https://ngrok.com/download)

    一部Teamsアプリ機能 (会話型ボット、メッセージング拡張機能、受信 Webhook) では、受信接続が必要です。  開発システムをトンネル経由でTeamsする必要があります。 タブのみを含むアプリでは、トンネルは必要ありません。  このパッケージは、(npm を使用して) プロジェクト ディレクトリ内にインストールされます `devDependencies`。

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a>次のTeams Toolkitを使用Visual Studio Code

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [アプリを構成する](#configure-your-app)
- [アプリをローカルで実行する](#install-and-run-your-app-locally)
- [アプリを公開する](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しいプロジェクトをTeamsする

このTeams Toolkitは、Azure Reactホストされているアプリや、SPFx環境でホストされている web パーツをMicrosoft 365 SharePointできます。 Azure でホストReact新しいアプリを作成するには、次の方法を実行します。

1. Visual Studio Code を開きます。
1. サイド バーの Teams アイコンを選択して、Teams ツールキットを開きます。

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. **[新しいプロジェクトの作成]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. **[新しい Teams アプリを作成]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. [機能 **の選択] ステップ** で、[ **タブ] 機能** が既に選択されています。 必要に応じて、[**ボットとメッセージング拡張機能****] を選択することもできます**。  **[OK]** を押します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. **[フロントエンド ホストの種類]** 手順で、**[Azure]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="新規アプリのホスティングを選択する方法を示すスクリーンショット":::。

1. 必要に応じて、[ **クラウド リソース] ステップ** で、アプリケーションで使用するクラウド リソースを選択します。 CRUD (作成、読み取り、更新、および削除) を選択すると、テーブルまたは API SQLアクセスできます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="新しいアプリにクラウド リソースを追加する方法を示すスクリーンショット":::。

1. [プログラミング **言語] ステップで** 、 **JavaScript または TypeScript** を **選択できます**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. ワークスペース フォルダーを選択します。 作成するプロジェクトのワークスペース フォルダー内にフォルダーが作成されます。

1. `helloworld` のように、アプリに適した名前を入力します。 アプリの名前は、英数字のみで構成されている必要があります。  **Enter** キーを押して続行します。

アプリTeams数秒で作成されます。 スキャフォールディング されたアプリには、シングル サインオンを処理するコードが含Azure Active Directory、Microsoft サービスへのアクセスGraph。  Azure リソースを選択した場合は、それらのリソースのコードも使用できます。

作成および発行プロセスの詳細についてはSPFxチュートリアルを参照[SPFxしてください](../get-started/first-app-spfx.md)。

## <a name="configure-your-app"></a>アプリを構成する

このアプリの中核となるのは、Teams 3 つのコンポーネントです。

  1. ユーザー Microsoft Teamsアプリを操作するクライアント (Web、デスクトップ、モバイル) を指定します。
  1. サーバーに表示されるコンテンツの要求に応答するTeams。 たとえば、HTML タブ コンテンツやボットアダプティブ カードなどです。
  1. アプリ Teamsは、次の 3 つのファイルで構成されます。

      > [!div class="checklist"]
      >
      > - manifest.json。
      > - パブリック [または組織](../resources/schema/manifest-schema.md#icons) のアプリ カタログに表示するアプリの色アイコン。
      > - アクティビティ [バーに](../resources/schema/manifest-schema.md#icons)表示するアウトライン Teamsアイコン。

マニフェストとアイコンは、プロジェクトに`.fx`アップロードされる前にプロジェクトのフォルダーにTeams。 アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。

1. アプリを構成するには、アプリの [**Teams Toolkit] タブ** Visual Studio Code。
1. [**マニフェスト エディター] セクション** の **[マニフェスト Project** 選択します。

[アプリの詳細] ページでフィールドを編集すると、最終的にアプリ パッケージの一部として出荷される manifest.json ファイルの内容が更新されます。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

アプリをローカルに構築して実行するには、以下のようにします。

1. Visual Studio Code で、**F5** を押して、アプリケーションをデバッグ モードで実行します。

   > アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。  ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。  この作業には 3 ～ 5 分かかります。

   必要に応じて、ローカル証明書をインストールするように求めるメッセージがツールキットに表示されます。 この証明書により、Teams は `https://localhost` からアプリケーションを読み込むことができます。 以下のダイアログが表示されたら、「はい」を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Teams がアプリケーションを localhost からロードできるようにするための SSL 証明書のインストールを求めるメッセージが表示される方法を示すスクリーンショット":::。

1. アプリケーションを実行するために Web ブラウザーが起動します。 Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。 また、他の場合は、アプリケーションに切り替Teams表示される場合があります。 このような場合は、Web アプリを選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="起動時に Web 版のチームを選択する方法を示すスクリーンショット":::

1. サインインするように求めるメッセージが表示されることがあります。 その場合は、アカウントでサインインMicrosoft 365します。
1. Teams へのアプリのインストールを促すメッセージが表示された場合は、**[追加]** を押してください。

バックエンドとフロントエンドの両方が、アプリケーション デバッガー Visual Studio Codeされます。  これにより、コード内の任意の場所にブレークポイントを設定し、状態を検査できます。  また、ブラウザー内でフロントエンド デバッグ ツール (開発者向けツールReactなど) を使用することもできます。  デバッグの詳細については、Visual Studio Codeを[参照してください](https://code.visualstudio.com/Docs/editor/debugging)。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

他のユーザーがアプリを使用する前に、アプリを開発者ポータルに発行して、他のユーザー Teams。

1. アプリを発行するには、アプリの [**Teams Toolkit] タブ** にVisual Studio Code。
1. [**発行] をTeams** セクションで **Project** します。

Azure ホスティングを使用する場合は、クラウドにプロビジョニングして展開している必要があります。 文書の公開プロセスの詳細については、SPFxチュートリアルを[SPFxしてください](../get-started/first-app-spfx.md)。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [発行済みアプリの保守とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

## <a name="see-also"></a>関連項目

* [アプリとアプリのTeams ToolkitをVisual Studio](~/toolkit/visual-studio-overview.md)
* [JavaScript クライアント SDK を使用してタブやその他のホストMicrosoft Teamsエクスペリエンスを構築する](~/tabs/how-to/using-teams-client-sdk.md)
