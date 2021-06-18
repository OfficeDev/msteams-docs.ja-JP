---
title: Microsoft Teams のコードとコードを使用ToolkitアプリVisual Studioする
description: Microsoft Teams アプリケーションを使用して、コード内でVisual Studioカスタム アプリを直接構築Toolkit
keywords: teams visual studio コード ツールキット
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: b2cfab5cb2ea2d727608b6ea3bbfec3271b2b039
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994141"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Teams のコードとコードを使用ToolkitアプリVisual Studioする

Teams Toolkit for Visual Studio Code は、開発者エクスペリエンスに対する "ゼロ構成" アプローチを使用して、Azure および M365 の統合 ID、クラウド ストレージへのアクセス、Microsoft Graph からのデータ、その他のサービスを備えた Teams アプリを作成および展開するのに役立ちます。  

また、このツールキットは、Visual Studio CLI (と呼ばれる) として使用することもできます `teamsfx` 。

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>コードの Teams ToolkitをVisual Studioする

1. Visual Studio Code を開きます。
1. [拡張機能] ビューを選択します **(Ctrl + Shift +**  /   **>** X
1. 検索ボックスに _、「Teams」と入力Toolkit。_
1. Teams サーバーの横にある緑色のインストール ボタンをToolkit。

Teams ファイルは、コード マーケットプレースToolkitでVisual Studio [できます](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

次のツールは、必要に応Visual Studioコード拡張機能によってインストールされます。 既にインストールされている場合は、インストールされているバージョンが代わりに使用されます。 Linux (WSL を含む) を使用する場合は、次のツールをインストールしてから使用する必要があります。

- [Azure Functions コア ツール](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools は、Azure でサービスを実行するときに必要な認証ヘルパーを含む、ローカル デバッグ実行時にバックエンド コンポーネントをローカルで実行するために使用されます。 これは、npm を使用してプロジェクト ディレクトリ内にインストールされます `devDependencies` 。

- [.NET SDK](/dotnet/core/install/)

    .NET SDK は、ローカル デバッグと Azure Functions アプリの展開用にカスタマイズされたバインドをインストールするために使用されます。 .NET 3.1 以降の SDK をグローバルにインストールしていない場合は、ポータブル バージョンがインストールされます。

- [ngrok](https://ngrok.com/download)

    Teams アプリの一部の機能 (会話型ボット、メッセージング拡張機能、受信 Webhook) では、受信接続が必要です。  開発システムをトンネル経由で Teams に公開する必要があります。 タブのみを含むアプリでは、トンネルは必要ありません。  このパッケージは、(npm を使用して) プロジェクト ディレクトリ内にインストールされます `devDependencies` 。

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a>Teams コードを使用ToolkitコードVisual Studioする

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [アプリを構成する](#configure-your-app)
- [アプリをローカルで実行する](#install-and-run-your-app-locally)
- [アプリを公開する](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しい Teams プロジェクトをセットアップする

Teams Toolkit、M365 SharePoint 環境でホストされている Azure または SPFx Web パーツでホストされている React アプリを作成できます。 Azure でホストされる新しい React アプリを作成するには、次の方法を実行します。

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

1. 必要に応じて、[ **クラウド** リソース] ステップで、アプリケーションで使用するクラウド リソースを選択します。 CRUD (作成、読み取り、更新、および削除) を選択して、テーブルまたは API SQLアクセスできます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="新しいアプリにクラウド リソースを追加する方法を示すスクリーンショット":::。

1. [プログラミング **言語] ステップで****、JavaScript** または **TypeScript を選択できます**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. ワークスペース フォルダーを選択します。 作成するプロジェクトのワークスペース フォルダー内にフォルダーが作成されます。

1. `helloworld` のように、アプリに適した名前を入力します。 アプリの名前は、英数字のみで構成されている必要があります。  **Enter** キーを押して続行します。

Teams アプリは数秒で作成されます。 スキャフォールディング されたアプリには、Azure Active Directory でのシングル サインオンを処理し、Microsoft Graph にアクセスするコードが含まれます。  Azure リソースを選択した場合は、それらのリソースのコードも使用できます。

SPFx の作成および発行プロセスの詳細については [、SPFx チュートリアルを参照してください](../get-started/first-app-spfx.md)。

## <a name="configure-your-app"></a>アプリを構成する

Teams アプリの中核となるのは、次の 3 つのコンポーネントです。

  1. ユーザーがアプリを操作する Microsoft Teams クライアント (Web、デスクトップ、またはモバイル)。
  1. Teams に表示されるコンテンツの要求に応答するサーバー。 たとえば、HTML タブ コンテンツやボットアダプティブ カードなどです。
  1. Teams アプリ パッケージは、次の 3 つのファイルで構成されます。

      > [!div class="checklist"]
      >
      > - このmanifest.jsオンです。
      > - パブリック [または組織](../resources/schema/manifest-schema.md#icons) のアプリ カタログに表示するアプリの色アイコン。
      > - Teams [アクティビティ バー](../resources/schema/manifest-schema.md#icons) に表示するアウトライン アイコン。

マニフェストとアイコンは、Teams にアップロードされる前 `.fx` にプロジェクトのフォルダーに保存されます。 アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。

1. アプリを構成するには、[コード] の **[Teams Toolkit]** タブVisual Studio移動します。
1. [ **プロジェクト] セクションで [** マニフェスト エディター **] を** 選択します。

[アプリの詳細] ページでフィールドを編集すると、最終的にアプリ パッケージの一部としてmanifest.jsファイルのコンテンツが更新されます。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

アプリをローカルに構築して実行するには、以下のようにします。

1. Visual Studio Code で、**F5** を押して、アプリケーションをデバッグ モードで実行します。

   > アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。  ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。  この作業には 3 ～ 5 分かかります。

   必要に応じて、ローカル証明書をインストールするように求めるメッセージがツールキットに表示されます。 この証明書により、Teams は `https://localhost` からアプリケーションを読み込むことができます。 以下のダイアログが表示されたら、「はい」を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Teams がアプリケーションを localhost からロードできるようにするための SSL 証明書のインストールを求めるメッセージが表示される方法を示すスクリーンショット":::。

1. アプリケーションを実行するために Web ブラウザーが起動します。 Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。 また、他の時間に Teams アプリケーションに切り替えるメッセージが表示される場合があります。 このような場合は、Web アプリを選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="起動時に Web 版のチームを選択する方法を示すスクリーンショット":::

1. サインインするように求めるメッセージが表示されることがあります。 その場合は、M365 アカウントを使用してサインインします。
1. Teams へのアプリのインストールを促すメッセージが表示された場合は、**[追加]** を押してください。

バックエンドとフロントエンドの両方がコード デバッガーにVisual Studioされます。  これにより、コード内の任意の場所にブレークポイントを設定し、状態を検査できます。  また、ブラウザー内でフロントエンド デバッグ ツール (React Developer Tools など) を使用することもできます。  コードのデバッグの詳細については、Visual Studioドキュメントを [参照してください](https://code.visualstudio.com/Docs/editor/debugging)。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

他のユーザーが使用する前に、アプリを Teams の開発者ポータルに発行する必要があります。

1. アプリを発行するには、コードの **[Teams** Toolkit] タブVisual Studioします。
1. [**発行] をTeams** セクションで **Project** します。

Azure ホスティングを使用する場合は、クラウドにプロビジョニングして展開している必要があります。 文書の公開プロセスの詳細については、「SPFxチュートリアル」[をSPFxしてください](../get-started/first-app-spfx.md)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [発行済みアプリの保守とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
