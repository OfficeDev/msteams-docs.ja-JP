---
author: surbhigupta
title: Visual Studio 用の Teams アプリをデバッグする
description: このモジュールでは、Teams ツールキットを使用して Teams アプリを Visual Studio でローカルでデバッグする方法について説明します
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: cff0b3e18f63bc7943a7fc16875294f41257a37c
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027447"
---
# <a name="debug-your-teams-app-locally-using-visual-studio"></a>Visual Studio を使用して Teams アプリをローカルでデバッグする

Teams ツールキットは、Microsoft Teams アプリをローカルでデバッグおよびプレビューするのに役立ちます。 デバッグとは、アプリ内の問題やバグを構築、確認、検出、修正するプロセスです。 デバッグにより、プログラムが正常に実行されることを確認します。 Visual Studio では、タブ、ボット、およびメッセージ拡張機能をデバッグできます。 Teams Toolkit では、次のデバッグ機能がサポートされています:

* Teams アプリの依存関係を準備する
* デバッグの開始
* ブレークポイントの切り替え
* ホット リロード
* デバッグの停止

デバッグ プロセス中に、Teams ツールキットは自動的にアプリ サービスを開始し、デバッグを開始し、Teams アプリをサイド ロードします。 デバッグ後、Teams Web クライアントで Teams アプリをプレビューできます。 また、ボット エンドポイントを使用するようにデバッグ設定をカスタマイズしたり、構成済みアプリを読み込むように環境変数をカスタマイズしたりできます。

## <a name="prerequisites"></a>前提条件

| &nbsp; | インストール | 使用するには... |
| --- | --- | --- |
| &nbsp; | **必須** | &nbsp; |
| &nbsp; | Visual Studio 2022 バージョン 17.3 | Visual Studio のエンタープライズ エディションをインストールし、"ASP.NET" ワークロードと Microsoft Teams 開発ツールをインストールできます。 |
| &nbsp; | Teams ツールキット | アプリのプロジェクト スキャフォールディングを作成する Visual Studio 拡張機能。 最新バージョン​​を使用します。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams を使用して、チャット、会議、通話用のアプリを通じて共同作業を行うすべてのユーザーと 1 か所で共同作業を行うことができます。 |
| &nbsp; | [Microsoft 365 テナントを準備する](../concepts/build-and-test/prepare-your-o365-tenant.md) | アプリをインストールするための適切なアクセス許可を持つ Teams アカウントにアクセスします。 |
| &nbsp; | [Microsoft 365 開発者アカウント](/../concepts/build-and-test/prepare-your-o365-tenant) | アプリをインストールするための適切なアクセス許可を持つ Teams アカウントにアクセスします。 |
| &nbsp; | Azure Tools と [Microsoft Azure CLI](/cli/azure/install-azure-cli) | 保存されたデータにアクセスしたり、Azure で Teams アプリ用のクラウドベースのバックエンドをデプロイしたりするための Azure ツール。 |
|&nbsp;  | **Optional** | &nbsp; |
|&nbsp; |[Ngrok](https://ngrok.com/) | Ngrok は、Azure Bot Framework からローカル コンピューターに外部メッセージを転送するために使用されます。|

## <a name="debug-your-app-locally"></a>アプリをローカルでデバッグする

Teams ツールキットを使用して、Visual Studio でアプリをローカルにデバッグできます。これを行うには、次の操作を実行します。

### <a name="set-up-ngrok-only-for-bot-and-message-extension-app"></a>Ngrok を設定する (ボットとメッセージ拡張機能アプリの場合のみ)

コマンド プロンプトを使用して、次のコマンドを実行します。

```
ngrok http 5130
```

### <a name="set-up-your-teams-toolkit"></a>Teams Toolkit を設定する

プロジェクトを作成した後、Teams ツールキットを使用して次の手順を実行して、アプリをデバッグします。

1. **プロジェクト** を右クリックします。
1. **[Teams ツールキット]** を選択します。
1. **[Teams アプリの依存関係を準備する]** を選択します。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="ローカル デバッグ用の Teams アプリの依存関係":::

   > [!NOTE]
   > このシナリオでは、プロジェクト名は MyTeamsApp1 です

   サインインする前に、Microsoft 365 アカウントにサイド ローディングのアクセス許可が必要です。  Teams アプリをテナントにアップロードできることを確認します。これを行わないと、Teams アプリが Teams クライアントで実行できない場合があります。

1. **Microsoft 365 アカウント** にサインインします。
1. **[続行]**
   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="[Microsoft 365 アカウントにサインインする]"::: の順に選択します。

   > [!Note]
   > サイドローディングのアクセス許可の詳細については、<https://aka.ms/teamsfx-sideloading-option> にアクセスしてください。

1. **[デバッグ]** を選択します。
1. **[デバッグの開始]** を選択するか、**F5** キーを直接選択します。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Startdebug.png" alt-text="デバッグの開始":::

   Visual Studio がブラウザーの Microsoft Teams クライアント内で Teams アプリを起動します。

   > [!Note]
   > 詳細については、<https://aka.ms/teamsfx-vs-debug> にアクセスしてください。

1. Microsoft Teams が読み込まれたら、**[追加]** を選択して Teams にアプリをインストールします。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-add-loadapp.png" alt-text="[追加] を選択してアプリを読み込む":::

   > [!TIP]
   > デバッグ中に Visual Studio のホット リロード機能を使用することもできます。 詳細については、<https://aka.ms/teamsfx-vs-hotreload> にアクセスしてください。

   > [!NOTE]
   > 通知ボット アプリをデバッグするときは、通知をトリガーするために必ず HTTP 要求を '<http://localhost:5130/api/notification>' に投稿してください。 プロジェクトの作成時に HTTP トリガーを選択した場合、curl (Windows コマンド プロンプト)、Postman などの任意の API ツールを使用できます。

   > [!TIP]
   > Teams アプリ マニフェスト ファイル (/templates/appPackage/manifest.template.json) に変更を加える場合、Teams アプリの依存関係を準備するコマンドを必ず実行してください。 Teams アプリをローカルで再度実行する前に実行します。

## <a name="key-features-of-teams-toolkit"></a>Teams Toolkit の主な機能

Teams ツールキットの次の主な機能を確認できます。これらは、Teams アプリのローカル デバッグ プロセスを自動化します。

### <a name="prepare-teams-app-dependencies"></a>Teams アプリの依存関係を準備する

Teams ツールキットは、ローカル デバッグの依存関係を準備し、アカウント内のテナントに Teams アプリを登録します。 ボット アプリとメッセージ拡張機能アプリの場合、Teams ツールキットはボットを登録して構成します。

### <a name="start-debugging"></a>デバッグの開始

デバッグは 1 回の操作で実行できます。**F5** キーを押してデバッグを開始します。 Teams ツールキットは、コードをビルドし、サービスを開始し、ブラウザーでアプリを起動します。

### <a name="toggle-breakpoints"></a>ブレークポイントの切り替え

タブ、ボット、メッセージ拡張機能、および Azure 関数のソース コードのブレークポイントを切り替えることができます。 ブレークポイントは、Web ブラウザーで Teams アプリを操作すると実行されます。
次の図は、ブレークポイントの切り替えを示しています。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png" alt-text="ローカル デバッグのブレークポイントの切り替え":::

### <a name="hot-reload"></a>ホット リロード

デバッグ中にソース コードの更新と保存を同時に実行するには、**[ホット リロード]** を選択して Teams アプリに変更を適用します。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload.png" alt-text="[ホット リロード] アイコンを選択する":::

ドロップダウンから **[ファイルの保存時にホット リロード]** オプションを選択して、自動ホット リロードを有効にします。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload-filesave.png" alt-text="[ファイルの保存時にホット リロード] を選択する":::
  
   > [!Tip]
   > デバッグ中の Visual Studio のホット リロード機能の詳細については、<https://aka.ms/teamsfx-vs-hotreload> にアクセスしてください。

### <a name="stop-debugging"></a>デバッグの停止

ローカル デバッグが完了したら、**[デバッグの停止]** を選択します。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Stopdebug.png" alt-text="[デバッグの停止] アイコンを選択する":::

## <a name="customize-debug-settings"></a>デバッグ設定をカスタマイズする

Teams アプリのデバッグ設定で、ボット エンドポイントを使用するようにカスタマイズして、環境変数を追加できます。

### <a name="use-your-bot-endpoint"></a>ボット エンドポイントを使用する

**.fx/configs/config.local.json** で siteEndpoint 構成をエンドポイントに設定できます。

```
"bot": {
    "siteEndpoint": "https://baidu.com"
}
```

### <a name="add-environment-variables"></a>環境変数の追加

**launchSettings.json** ファイルに **environmentVariables** を追加できます。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-environment-variables.png" alt-text="環境変数の追加":::

### <a name="launch-teams-app-as-a-web-app"></a>Teams アプリを Web アプリとして起動する

Teams クライアントで実行する代わりに、Teams アプリを Web アプリとして起動できます。

1. プロジェクトのソリューション エクスプローラー パネルで **[プロパティ]** > **[launchSettings.json]** を選択します。
1. ファイルから **'launchUrl'** を削除します。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png" alt-text="launchurl を削除してチームを Web アプリとして起動する":::

1. **[ソリューション]** を右クリックします。
1. [**プロパティ**] をクリックします。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png" alt-text="[ソリューション] を右クリックし、[プロパティ] を選択する":::

1. ダイアログで **[構成プロパティ]** > **[構成]** の順に選択します。
1. **[展開]** プロセス ボックスをオフにします。
1. **[OK]** をクリックします。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png" alt-text="構成プロパティで展開をオフにする ":::

## <a name="see-also"></a>関連項目

* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy-teams-app.md)
* [Visual Studio を使用して Teams アプリ マニフェストを編集する](VS-TeamsFx-preview-and-customize-app-manifest.md)
