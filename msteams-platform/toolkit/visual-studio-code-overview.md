---
title: アプリとアプリのMicrosoft Teams ToolkitをVisual Studio Code
description: アプリを使用して、アプリ内で直接素晴らしいカスタム Visual Studio Codeを構築Microsoft Teams Toolkit
keywords: teams visual studio コード ツールキット
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 59f2943f37856c42346b2ffad4e01d88910679ae
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020262"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>アプリとアプリのTeams ToolkitをVisual Studio Code

Microsoft Teams ツールキットを使用すると、Visual Studio Code 環境内で直接カスタムの Teams アプリを構築できます。 ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。

## <a name="installing-the-teams-toolkit"></a>アプリケーションのインストールTeams Toolkit

このMicrosoft Teams ToolkitはVisual Studio Code[マーケット](https://aka.ms/teams-toolkit)プレースから、またはVisual Studio内の拡張機能として直接ダウンロードVisual Studio Code。

> [!TIP]
> インストール後、アクティビティ バーにTeams ToolkitがVisual Studio Code表示されます。 表示されない場合は、アクティビティ バー内を右クリックし、[Microsoft Teams]を選択してツールキットをピン留めして簡単にアクセスできます。

## <a name="using-the-toolkit"></a>ツールキットの使用

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [既存のプロジェクトをインポートする](#import-an-existing-teams-app-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [アプリをローカルまたはローカルで実行Teams](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>新しいプロジェクトをTeamsする

1. ローカル環境でプロジェクトのワークスペース/フォルダーを作成します。
1. [Visual Studio Code] アイコンをTeamsします。 ![Teams アイコン](../assets/icons/favicon-16x16.png) ウィンドウの左側のアクティビティ バーから。
1. [**コマンド メニューからMicrosoft Teams Toolkit** を開く] を選択します。
1. コマンド **メニューから [新Teamsアプリ** を作成する] を選択します。
1. プロンプトが表示されたら、ワークスペースの名前を入力します。 これは、プロジェクトが存在するフォルダーの名前と、アプリの既定の名前の両方として使用されます。
1. Enter **キーを** 押すと、[機能の追加 **] 画面が** 表示され、新しいアプリのプロパティが構成されます。
1. [完了] **ボタンを** 選択して構成プロセスを完了します。

## <a name="import-an-existing-teams-app-project"></a>既存のアプリ プロジェクトTeamsインポートする

1. [Visual Studio Code] アイコンをTeamsします。 ![Teams アイコン](../assets/icons/favicon-16x16.png) ウィンドウの左側のアクティビティ バーから。
1. コマンド メニュー **から [アプリ パッケージの** インポート] を選択します。
1. アプリ パッケージの zip[ファイルTeams既存のファイルを](../concepts/build-and-test/apps-package.md)選択します。
1. [発行パッケージ **の選択] ボタンを選択** します。 これで、ツールキットの構成タブにアプリの詳細が表示されます。
1. [Visual Studio Code] で[ワークスペースにフォルダーを追加] を選択して、ソース コード ディレクトリをワークスペースに  ->  Visual Studio Codeします。

## <a name="configure-your-app"></a>アプリを構成する

このアプリの中核となるのは、Teams 3 つのコンポーネントです。

  1. ユーザー Microsoft Teamsアプリを操作するクライアント (Web、デスクトップ、モバイル) を指定します。
  1. HTML タブ コンテンツやボットアダプティブ カードなど、Teamsに表示されるコンテンツの要求に応答するサーバー。
  1. 次Teams [3 つのファイルで](/concepts/build-and-test/apps-package.md)構成されるアプリ パッケージです。

  > [!div class="checklist"]
  >
  > - [manifest.js] 
  > - パブリック [または組織の](../resources/schema/manifest-schema.md#icons) アプリ カタログに表示するアプリの色アイコン
 > - アクティビティ[バーに](../resources/schema/manifest-schema.md#icons)表示するアウトライン Teamsアイコン。

アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。

1. アプリを構成するには、アプリの **[Microsoft Teams Toolkit]** タブにVisual Studio Code。
1. [アプリ **パッケージの編集] を** 選択して、[ **アプリの詳細] ページを表示** します。
1. [アプリの詳細] ページでフィールドを編集すると、最終的にアプリ パッケージの一部としてmanifest.jsファイルのコンテンツが更新されます。 *「App* [Studio マニフェスト エディター」を参照してください。](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>アプリをパッケージ化する

アプリの .publish **フォルダー** でアプリの詳細ページ、マニフェスト、または **.env** ファイルを **変更** すると、アプリのファイルが自動的にDevelopment.zipされます。  同じフォルダーに 2 [つのアイコン](../concepts/build-and-test/apps-package.md#app-icons) を含める必要があります。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

## <a name="run-your-app"></a>アプリの実行

### <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

アプリをパッケージ化 *してテストする* 方法の詳細な手順については、プロジェクトのホームページの *Build and Run コンテンツを参照してください。 一般に、アプリのサーバーをインストールし、実行してからトンネリング ソリューションをセットアップし、Teams localhost から実行されているコンテンツにアクセスする必要があります。

### <a name="enable-development-from-localhost"></a>localhost からの開発を有効にする

HTTPS を使用して localhost でタブ ベースのアプリをデバッグする場合は、ブラウザーに対して、サービスを提供するアプリを信頼するように伝える必要があります <https://localhost> 。 <https://localhost:3000/tab> に移動します。 サイトが信頼されていないという警告が表示される場合は、続行するオプションを選択します。 これで、アプリはクライアントからアクセスTeams必要があります。

### <a name="run-your-app-in-teams"></a>アプリをアプリで実行Teams

前提条件:[開発者Teamsモードを有効にする](https://aka.ms/teams-toolkit-enable-devpreview)

1. ウィンドウの左側にあるアクティビティ バーにVisual Studio Codeします。
1. [実行] **アイコンを** 選択して、[実行] ビュー **と [デバッグ] ビューを表示** します。
1. キーボード ショートカットを使用することもできます `Ctrl+Shift+D` 。

> [!div class="nextstepaction"]
> [次の手順: 発行済みアプリの保守とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
