---
title: Microsoft Teams Toolkit と Visual Studio コードを使用してアプリをビルドする
description: Microsoft Teams ツールキットを使用して、Visual Studio Code 内で魅力的なカスタムアプリを直接作成する
keywords: teams visual studio code toolkit
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 350da030d15e72e2cad51c5967afab9b6f29fe9e
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604474"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Teams Toolkit と Visual Studio Code を使用してアプリをビルドする

Microsoft Teams ツールキットを使用すると、Visual Studio Code 環境内で直接カスタムの Teams アプリを構築できます。 ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。

## <a name="installing-the-teams-toolkit"></a>Teams ツールキットをインストールする

Microsoft Teams Toolkit for Visual studio code は、visual [Studio Marketplace](https://aka.ms/teams-toolkit) からダウンロードするか、Visual studio code 内の拡張機能として直接ダウンロードできます。

> [!TIP]
> インストール後に、Visual Studio Code アクティビティバーに Teams ツールキットが表示されます。 表示されていない場合は、アクティビティバー内を右クリックし、[ **Microsoft Teams** ] を選択して、簡単にアクセスできるようにツールキットを固定します。

## <a name="using-the-toolkit"></a>ツールキットの使用

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [既存のプロジェクトをインポートする](#import-an-existing-teams-app-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [アプリをローカルで、または Teams で実行する](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>新しい Teams プロジェクトをセットアップする

1. ローカル環境でプロジェクトのワークスペース/フォルダーを作成します。
1. Visual Studio Code で、Teams アイコンを選択します。 ![Teams アイコン](../assets/icons/favicon-16x16.png) ウィンドウの左側にあるアクティビティバーから。
1. [コマンド] メニューから [ **Microsoft Teams Toolkit** ] を選択します。
1. [コマンド] メニューから [ **新しい Teams アプリの作成** ] を選択します。
1. メッセージが表示されたら、ワークスペースの名前を入力します。 これは、プロジェクトが存在するフォルダーの名前と、アプリの既定の名前の両方として使用されます。
1. **Enter** キーを押すと、[**機能の追加**] 画面が表示され、新しいアプリのプロパティを構成します。
1. [ **完了** ] ボタンを選択して、構成プロセスを完了します。

## <a name="import-an-existing-teams-app-project"></a>既存の Teams アプリプロジェクトをインポートする

1. Visual Studio Code で、Teams アイコンを選択します。 ![Teams アイコン](../assets/icons/favicon-16x16.png) ウィンドウの左側にあるアクティビティバーから。
1. [コマンド] メニューから [ **アプリパッケージのインポート** ] を選択します。
1. 既存の [Teams アプリパッケージ](../concepts/build-and-test/apps-package.md) の zip ファイルを選択します。
1. **[発行パッケージの選択**] ボタンを選択します。 これで、ツールキットの [構成] タブにアプリの詳細が設定されます。
1. Visual studio code で、[**ファイル**] [  ->  **ワークスペースへのフォルダーの追加**] を選択して、ソースコードディレクトリを visual studio code Workspace に追加します。

## <a name="configure-your-app"></a>アプリを構成する

主に、Teams アプリは3つのコンポーネントをサポートしています。

  1. ユーザーがアプリを操作する Microsoft Teams クライアント (web、デスクトップ、またはモバイル)。
  1. Teams に表示されるコンテンツの要求に応答するサーバー。たとえば、HTML タブのコンテンツや bot のアダプティブカード。
  1. 3つのファイルで構成される Teams [アプリパッケージ](/concepts/build-and-test/apps-package.md) :

  > [!div class="checklist"]
  >
  > - manifest.js 
  > - パブリックまたは組織のアプリカタログに表示するための、アプリの[カラーアイコン](../resources/schema/manifest-schema.md#icons)
 > - Teams アクティビティバーに表示するための [アウトラインアイコン](../resources/schema/manifest-schema.md#icons) 。

アプリがインストールされると、Teams クライアントはマニフェストファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を特定します。

1. アプリを構成するには、Visual Studio Code の [ **Microsoft Teams Toolkit** ] タブに移動します。
1. [ **アプリパッケージの編集** ] を選択して、[ **アプリの詳細** ] ページを表示します。
1. [アプリの詳細] ページのフィールドを編集すると、最終的にアプリパッケージの一部として配布されるファイルの manifest.jsの内容が更新されます。 *「* [App Studio manifest Editor](https://aka.ms/teams-toolkit-manifest) 」を参照

## <a name="package-your-app"></a>アプリをパッケージ化する

アプリの **publish** フォルダーにある **アプリの詳細** ページ、**マニフェスト**、または **env** ファイルを変更すると、 **Development.zip** ファイルが自動的に生成されます。 同じフォルダーに [2 つのアイコン](../concepts/build-and-test/apps-package.md#app-icons) を含める必要があります。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

## <a name="run-your-app"></a>アプリを実行する

### <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

アプリをパッケージ化してテストする方法の詳細については、「プロジェクトホームページのコンテンツを *ビルドして実行* する」を参照してください。 一般に、アプリのサーバーをインストールし、実行して、トンネリングソリューションをセットアップして、Teams が localhost から実行されているコンテンツにアクセスできるようにする必要があります。

### <a name="enable-development-from-localhost"></a>Localhost からの開発を有効にする

HTTPS を使用して localhost でタブベースのアプリをデバッグする場合は、提供元のアプリが信頼されていることをブラウザーに通知する必要があり <https://localhost> ます。 <https://localhost:3000/tab> に移動します。 サイトが信頼されていないことを示す警告が表示された場合は、そのまま続行するオプションを選択します。 これで、アプリは Teams クライアントからアクセスできるようになります。

### <a name="run-your-app-in-teams"></a>Teams でアプリを実行する

前提条件: [Teams 開発者プレビューモードを有効にする](https://aka.ms/teams-toolkit-enable-devpreview)

1. Visual Studio の [コード] ウィンドウの左側にあるアクティビティバーに移動します。
1. [実行 **] アイコンを** 選択して、[ **実行] および [デバッグ** ] ビューを表示します。
1. キーボードショートカットを使用することもでき `Ctrl+Shift+D` ます。

> [!div class="nextstepaction"]
> [次のステップ: 公開アプリの管理とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
