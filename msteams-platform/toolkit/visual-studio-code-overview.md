---
title: Microsoft Teams ツールキットと Visual Studio Code を使用してアプリを構築する
description: Microsoft Teams Toolkit を使用して Visual Studio Code 内で直接優れたカスタム アプリの構築を開始する
keywords: teams Visual Studio コード ツールキット
ms.localizationpriority: medium
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 841dddfd515fd202a36f4c8a6b490faccff7b537
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2022
ms.locfileid: "65887605"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Teams Toolkit と Visual Studio Code を使用してアプリをビルドする

Teams Toolkit for Visual Studio Code を使用すると、開発者は、統合 ID、クラウド ストレージへのアクセス、Microsoft Graph からのデータ、および Azure および Microsoft 365 のその他のサービスへのアクセスを備えた Teams アプリを、開発者エクスペリエンスに対する "ゼロ構成" アプローチで作成および展開できます。  

また、Visual Studio または CLI (呼び出し) `teamsfx`としてツールキットを使用することもできます。

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>Teams Toolkit for Visual Studio Code をインストールする

1. Visual Studio Code を開きます。
1. 拡張機能ビュー (**Ctrl + Shift + X** / **⌘⇧-X** または **ビュー > Extensions**) を選択します。
1. 検索ボックスに、「_Teams Toolkit_」と入力します。
1. Teams Toolkit の横にある緑色のインストール ボタンを選択します。

Teams Toolkit は、[Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) でも見つけることができます。

次のツールは、必要に応じて Visual Studio Code 拡張機能によってインストールされます。 既にインストールされている場合は、代わりにインストールされているバージョンが使用されます。 Linux (WSL を含む) を使用している場合は、次のツールを使用する前にインストールする必要があります。

- [Azure Functions Core Tools](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools は、Azure でサービスを実行するときに必要な認証ヘルパーを含め、ローカル デバッグの実行中にバックエンド コンポーネントをローカルで実行するために使用されます。 npm `devDependencies`を使用してプロジェクト ディレクトリ内にインストールされます。

- [.NET SDK](/dotnet/core/install/)

    .NET SDK は、ローカル デバッグと Azure Functions アプリのデプロイ用にカスタマイズされたバインドをインストールするために使用されます。 .NET 3.1 以降の SDK をグローバルにインストールしていない場合は、ポータブル バージョンがインストールされます。

- [ngrok](https://ngrok.com/download)

    Teams アプリの一部の機能 (会話ボット、メッセージング拡張機能、受信 Webhook) には受信接続が必要です。  トンネルを介して開発システムを Teams に公開する必要があります。 タブのみを含むアプリにはトンネルは必要ありません。  このパッケージはプロジェクト ディレクトリ内にインストールされます (npm `devDependencies` を使用)。

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a>Teams Toolkit for Visual Studio Code を使用する

- [新しいプロジェクトを設定する](#set-up-a-new-teams-project)
- [アプリを構成する](#configure-your-app)
- [アプリをローカルで実行する](#install-and-run-your-app-locally)
- [アプリを公開する](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しい Teams プロジェクトを設定する

Teams Toolkit では、Microsoft 365 SharePoint 環境でホストされている Azure または SPFx Web パーツでホストされている React アプリを作成できます。 Azure でホストされる新しい React アプリを作成するには、

1. Visual Studio Code を開きます。
1. サイド バーの Teams アイコンを選択して、Teams ツールキットを開きます。

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. **[新しいプロジェクトの作成]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. **[新しい Teams アプリを作成]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. [ **機能の選択] ステップで** 、[ **タブ]** 機能が既に選択されています。 必要に応じて、[ **ボット** と **メッセージング拡張機能**] を選択することもできます。  **[OK]** を押します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. **[フロントエンド ホストの種類]** 手順で、**[Azure]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="新規アプリのホスティングを選択する方法を示すスクリーンショット":::。

1. 必要に応じて、[ **クラウド リソース** ] ステップで、アプリケーションで使用するクラウド リソースを選択します。 SQL テーブルまたは API への CRUD (作成、読み取り、更新、削除) アクセスを選択できます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="新しいアプリにクラウド リソースを追加する方法を示すスクリーンショット":::。

1. **[プログラミング言語**] ステップでは、**JavaScript または TypeScript** を選択できます。

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. ワークスペース フォルダーを選択します。 作成するプロジェクトのワークスペース フォルダー内にフォルダーが作成されます。

1. `helloworld` のように、アプリに適した名前を入力します。 アプリの名前は、英数字のみで構成されている必要があります。  **Enter** キーを押して続行します。

Teams アプリは数秒以内に作成されます。 スキャフォールディングされたアプリには、Azure Active Directory でのシングル サインオンと Microsoft Graph へのアクセスを処理するコードが含まれています。  Azure リソースを選択した場合は、それらのリソースのコードも使用できます。

SPFx の作成と発行プロセスの詳細については、 [SPFx のチュートリアル](../get-started/first-app-spfx.md)を参照してください。

## <a name="configure-your-app"></a>アプリを構成する

その中核となる Teams アプリは、次の 3 つのコンポーネントを採用しています。

  1. ユーザーがアプリを操作する Microsoft Teams クライアント (Web、デスクトップ、モバイル)。
  1. Teams に表示されるコンテンツの要求に応答するサーバー。 たとえば、HTML タブのコンテンツやボットのアダプティブ カードなどです。
  1. Teams アプリ パッケージは、次の 3 つのファイルで構成されます。

      > [!div class="checklist"]
      >
      > - manifest.json。
      > - パブリックまたは組織のアプリ カタログに表示するアプリの [色アイコン](../resources/schema/manifest-schema.md#icons) 。
      > - Teams アクティビティ バーに表示する [アウトライン アイコン](../resources/schema/manifest-schema.md#icons) 。

マニフェストとアイコンは、Teams にアップロードされる `.fx` 前に、プロジェクトのフォルダーに保存されます。 アプリがインストールされると、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を判断します。

1. アプリを構成するには、Visual Studio Code の **[Teams Toolkit** ] タブに移動します。
1. **[プロジェクト**] セクションで [**マニフェスト エディター]** を選択します。

[アプリの詳細] ページのフィールドを編集すると、最終的にアプリ パッケージの一部として出荷される manifest.json ファイルの内容が更新されます。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

アプリをローカルに構築して実行するには、以下のようにします。

1. Visual Studio Code で、**F5** を押して、アプリケーションをデバッグ モードで実行します。

   > アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。  ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。  この作業には 3 ～ 5 分かかります。

   必要に応じて、ローカル証明書のインストールを求めるメッセージがツールキットに表示されます。 この証明書により、Teams は `https://localhost` からアプリケーションを読み込むことができます。 以下のダイアログが表示されたら、「はい」を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Teams がアプリケーションを localhost からロードできるようにするための SSL 証明書のインストールを求めるメッセージが表示される方法を示すスクリーンショット":::。

1. アプリケーションを実行するために Web ブラウザーが起動します。 Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。 また、Teams アプリケーションへの切り替えを求めるメッセージが表示される場合もあります。 この場合は、Web アプリを選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="起動時に Web 版のチームを選択する方法を示すスクリーンショット":::

1. サインインするように求めるメッセージが表示されることがあります。 その場合は、Microsoft 365 アカウントでサインインします。
1. Teams へのアプリのインストールを促すメッセージが表示された場合は、**[追加]** を押してください。

バックエンドとフロントエンドの両方が Visual Studio Code デバッガーにフックされます。  これにより、コード内の任意の場所にブレークポイントを設定し、状態を検査できます。  ブラウザー内でフロントエンド デバッグ ツール (React Developer Tools など) を使用することもできます。  Visual Studio Code でのデバッグの詳細については、 [ドキュメントを参照してください](https://code.visualstudio.com/Docs/editor/debugging)。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

他のユーザーが使用できるようにするには、Teams 用開発者ポータルにアプリを発行する必要があります。

1. アプリを発行するには、Visual Studio Code の **[Teams Toolkit** ] タブに移動します。
1. [**プロジェクト**] セクションで [**Teams に発行**] を選択します。

Azure ホスティングを使用している場合は、クラウドにプロビジョニングしてデプロイする必要があります。 SPFx パブリケーション プロセスの詳細については、 [SPFx のチュートリアル](../get-started/first-app-spfx.md)を参照してください。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [公開したアプリの管理とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

## <a name="see-also"></a>関連項目

* [Teams Toolkit と Visual Studio を使用してアプリを構築する](~/toolkit/visual-studio-overview.md)
* [Microsoft Teams JavaScript クライアント SDK を使用してタブやその他のホストされたエクスペリエンスを構築する](~/tabs/how-to/using-teams-client-sdk.md)
