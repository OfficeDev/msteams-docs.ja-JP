---
title: Microsoft Teams ToolkitとVisual Studio Codeを使用してアプリを構築する
description: Microsoft Teams Toolkitを使用して、Visual Studio Code内で優れたカスタム アプリを直接構築し始める
keywords: チームビジュアルスタジオコードツールキット
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: efd0962e9c4c0d64dbac47caf29b2e56907937b3
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566559"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>Teams ToolkitとVisual Studio Codeを使用してアプリを構築する

Microsoft Teams ツールキットを使用すると、Visual Studio Code 環境内で直接カスタムの Teams アプリを構築できます。 ツールキットはプロセスをガイドし、Teams アプリの構築、デバッグ、起動に必要なすべてを提供します。

## <a name="installing-the-teams-toolkit"></a>Teams Toolkitのインストール

Visual Studio CodeのMicrosoft Teams Toolkitは[、Visual Studioマーケットプレイス](https://aka.ms/teams-toolkit)からダウンロードするか、Visual Studio Code内の拡張機能として直接ダウンロードできます。

> [!TIP]
> インストール後、Visual Studio CodeアクティビティバーにTeams Toolkitが表示されます。 アクセスできない場合は、アクティビティバー内を右クリックし **、Microsoft Teams** 選択してツールキットをピン留めして簡単にアクセスできます。

## <a name="using-the-toolkit"></a>ツールキットの使用

- [新しいプロジェクトを設定する](#set-up-a-new-teams-project)
- [既存のプロジェクトをインポートする](#import-an-existing-teams-app-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [アプリをローカルまたはTeamsで実行する](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>新しいTeams プロジェクトを設定する

1. ローカル環境でプロジェクトのワークスペースまたはフォルダを作成します。
1. Visual Studio Codeで、Teams アイコンを選択します。 ![Teams アイコン](../assets/icons/favicon-16x16.png) ウィンドウの左側のアクティビティ バーから移動します。
1. コマンド メニュー **から [Microsoft Teams Toolkitを開く**] を選択します。
1. コマンド メニューから **[新しいTeams アプリの作成**] を選択します。
1. プロンプトが表示されたら、ワークスペースの名前を入力します。 これは、プロジェクトが存在するフォルダーの名前と、アプリの既定の名前の両方として使用されます。
1. **Enter キー** を押すと、[**機能の追加]** 画面に表示され、新しいアプリのプロパティを構成します。
1. [ **完了** ] ボタンを選択して、構成プロセスを完了します。

## <a name="import-an-existing-teams-app-project"></a>既存のTeams アプリ プロジェクトをインポートする

1. Visual Studio Codeで、Teams アイコンを選択します。 ![Teams アイコン](../assets/icons/favicon-16x16.png) ウィンドウの左側のアクティビティ バーから移動します。
1. コマンド メニューから **[アプリ パッケージのインポート** ] を選択します。
1. 既存の[Teams アプリ パッケージ](../concepts/build-and-test/apps-package.md)の zip ファイルを選択します。
1. [ **発行パッケージの選択** ] ボタンをクリックします。 ツールキットの構成タブに、アプリの詳細が表示されます。
1. Visual Studio Codeで、[  ->  **ファイル] [フォルダをワークスペースに追加**] を選択して、ソース コード ディレクトリをVisual Studio Code ワークスペースに追加します。

## <a name="configure-your-app"></a>アプリを構成する

その中核となるTeamsアプリには、次の 3 つのコンポーネントが含まれます。

  1. ユーザーがアプリを操作するクライアント (web、デスクトップ、モバイル) をMicrosoft Teams。
  1. Teamsに表示されるコンテンツの要求に応答するサーバー。 たとえば、HTML タブコンテンツやボットアダプティブカードなどです。
  1. 3 つのファイルで構成されるTeams[アプリ パッケージ](/concepts/build-and-test/apps-package.md)。

      > [!div class="checklist"]
      >
      > - manifest.js。 
      > - アプリがパブリックまたは組織のアプリ カタログに表示する [色のアイコン](../resources/schema/manifest-schema.md#icons) 。
      > - Teamsアクティビティ バーに表示する[アウトライン アイコン](../resources/schema/manifest-schema.md#icons)。

アプリがインストールされると、Teams クライアントはマニフェスト ファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を判断します。

1. アプリを構成するには、Visual Studio Codeの **[Microsoft Teams Toolkit]** タブに移動します。
1. [ **アプリ パッケージの編集]** を選択して、[ **アプリの詳細** ] ページを表示します。
1. [アプリの詳細] ページのフィールドを編集すると、最終的にアプリ パッケージの一部として出荷されるファイル上のmanifest.jsの内容が更新されます。 詳細については[、「App Studio マニフェスト エディター](https://aka.ms/teams-toolkit-manifest) 」を参照してください。

## <a name="package-your-app"></a>アプリをパッケージ化する

アプリの **.publish** フォルダー内の **アプリの詳細** ページ、**マニフェスト**、または **.env** ファイルを変更すると **、Development.zip** ファイルが自動的に生成されます。 同じフォルダに [2 つのアイコン](../concepts/build-and-test/apps-package.md#app-icons) を含める必要があります。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

## <a name="run-your-app"></a>アプリの実行

### <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

アプリをパッケージ化してテストする方法の詳細については、「プロジェクトホームページの **コンテンツのビルドと実行** 」を参照してください。 一般的に、アプリのサーバーをインストールして実行し、次に、Teamsが localhost から実行されているコンテンツにアクセスできるようにトンネリング ソリューションをセットアップする必要があります。

### <a name="enable-development-from-localhost"></a>ローカルホストからの開発を可能にする

HTTPS を使用して localhost でタブベースのアプリをデバッグする場合は、ブラウザーに、 から提供されているアプリを信頼するように指示する必要があります <https://localhost> 。 <https://localhost:3000/tab> に移動します。 サイトが信頼されていないことを示す警告が表示された場合は、続行するオプションを選択します。 これで、アプリがTeams クライアントからアクセスできるようになります。

### <a name="run-your-app-in-teams"></a>Teamsでアプリを実行する

必要条件:[開発者プレビュー モードTeams有効にする](https://aka.ms/teams-toolkit-enable-devpreview)

1. Visual Studio Code ウィンドウの左側にあるアクティビティ バーに移動します。
1. [ **実行** ] アイコンを選択して、[ **実行] ビューと [デバッグ** ] ビューを表示します。
1. また、キーボード ショートカット を使用することもできます `Ctrl+Shift+D` 。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [公開済みアプリの保守とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
