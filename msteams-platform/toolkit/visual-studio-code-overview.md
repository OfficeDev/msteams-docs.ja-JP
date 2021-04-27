---
title: Microsoft Teams のコードとコードを使用ToolkitアプリVisual Studioする
description: Microsoft Teams アプリケーションを使用して、コード内でVisual Studioカスタム アプリを直接構築Toolkit
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
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Teams のコードとコードを使用ToolkitアプリVisual Studioする

Microsoft Teams ツールキットを使用すると、Visual Studio Code 環境内で直接カスタムの Teams アプリを構築できます。 ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。

## <a name="installing-the-teams-toolkit"></a>Teams サーバーのインストールToolkit

Microsoft Teams Toolkit Visual Studioコードは、Visual Studio [Marketplace](https://aka.ms/teams-toolkit) から、または Visual Studio コード内の拡張機能としてVisual Studioできます。

> [!TIP]
> インストール後、[コード] アクティビティ バーに Teams ToolkitがVisual Studio表示されます。 設定されていない場合は、アクティビティ バー内を右クリックし **、[Microsoft Teams]** を選択してツールキットをピン留めして簡単にアクセスできます。

## <a name="using-the-toolkit"></a>ツールキットの使用

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [既存のプロジェクトをインポートする](#import-an-existing-teams-app-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [アプリをローカルまたは Teams で実行する](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>新しい Teams プロジェクトをセットアップする

1. ローカル環境でプロジェクトのワークスペース/フォルダーを作成します。
1. [Visual Studioコード] で、[Teams] アイコンを選択します。 ![Teams アイコン](../assets/icons/favicon-16x16.png) ウィンドウの左側のアクティビティ バーから。
1. コマンド **メニューから [Microsoft Teams Toolkit** 開く] を選択します。
1. コマンド メニュー **から [新しい Teams アプリの** 作成] を選択します。
1. プロンプトが表示されたら、ワークスペースの名前を入力します。 これは、プロジェクトが存在するフォルダーの名前と、アプリの既定の名前の両方として使用されます。
1. Enter **キーを** 押すと、[機能の追加 **] 画面が** 表示され、新しいアプリのプロパティが構成されます。
1. [完了] **ボタンを** 選択して構成プロセスを完了します。

## <a name="import-an-existing-teams-app-project"></a>既存の Teams アプリ プロジェクトをインポートする

1. [Visual Studioコード] で、[Teams] アイコンを選択します。 ![Teams アイコン](../assets/icons/favicon-16x16.png) ウィンドウの左側のアクティビティ バーから。
1. コマンド メニュー **から [アプリ パッケージの** インポート] を選択します。
1. 既存の Teams アプリ パッケージ [の zip ファイルを](../concepts/build-and-test/apps-package.md) 選択します。
1. [発行パッケージ **の選択] ボタンを選択** します。 これで、ツールキットの構成タブにアプリの詳細が表示されます。
1. [Visual Studio コード] で、[ワークスペースにフォルダーを追加する] を選択して、ソース コード ディレクトリを [コード]  ->  ワークスペースVisual Studio追加します。

## <a name="configure-your-app"></a>アプリを構成する

Teams アプリの中核となるのは、次の 3 つのコンポーネントです。

  1. ユーザーがアプリを操作する Microsoft Teams クライアント (Web、デスクトップ、またはモバイル)。
  1. Teams に表示されるコンテンツの要求 (HTML タブ コンテンツやボットアダプティブ カードなど) に応答するサーバー。
  1. 3 [つのファイルで構成](/concepts/build-and-test/apps-package.md) される Teams アプリ パッケージ。

  > [!div class="checklist"]
  >
  > - [manifest.js] 
  > - パブリック [または組織の](../resources/schema/manifest-schema.md#icons) アプリ カタログに表示するアプリの色アイコン
 > - Teams [アクティビティ バー](../resources/schema/manifest-schema.md#icons) に表示するアウトライン アイコン。

アプリがインストールされている場合、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL など、必要な情報を特定します。

1. アプリを構成するには、[コード] の **[Microsoft Teams Toolkit]** タブVisual Studioします。
1. [アプリ **パッケージの編集] を** 選択して、[ **アプリの詳細] ページを表示** します。
1. [アプリの詳細] ページでフィールドを編集すると、最終的にアプリ パッケージの一部としてmanifest.jsファイルのコンテンツが更新されます。 *「App* [Studio マニフェスト エディター」を参照してください。](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>アプリをパッケージ化する

アプリの .publish **フォルダー** でアプリの詳細ページ、マニフェスト、または **.env** ファイルを **変更** すると、アプリのファイルが自動的にDevelopment.zipされます。  同じフォルダーに 2 [つのアイコン](../concepts/build-and-test/apps-package.md#app-icons) を含める必要があります。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

## <a name="run-your-app"></a>アプリの実行

### <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

アプリをパッケージ化 *してテストする* 方法の詳細な手順については、プロジェクトのホームページの *Build and Run コンテンツを参照してください。 一般に、アプリのサーバーをインストールし、それを実行してから、Teams が localhost から実行されているコンテンツにアクセスできるよう、トンネリング ソリューションをセットアップする必要があります。

### <a name="enable-development-from-localhost"></a>localhost からの開発を有効にする

HTTPS を使用して localhost でタブ ベースのアプリをデバッグする場合は、ブラウザーに対して、サービスを提供するアプリを信頼するように伝える必要があります <https://localhost> 。 <https://localhost:3000/tab> に移動します。 サイトが信頼されていないという警告が表示される場合は、続行するオプションを選択します。 これで、Teams クライアントからアプリにアクセスできる必要があります。

### <a name="run-your-app-in-teams"></a>Teams でアプリを実行する

前提条件: [Teams 開発者プレビュー モードを有効にする](https://aka.ms/teams-toolkit-enable-devpreview)

1. [コード] ウィンドウの左側にあるアクティビティ バー Visual Studio移動します。
1. [実行] **アイコンを** 選択して、[実行] ビュー **と [デバッグ] ビューを表示** します。
1. キーボード ショートカットを使用することもできます `Ctrl+Shift+D` 。

> [!div class="nextstepaction"]
> [次の手順: 発行済みアプリの保守とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
