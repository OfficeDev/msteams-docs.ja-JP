---
title: 開始する - アプリを使用して最初のTeamsアプリをSPFx
author: zhenyasav
description: カスタム タブを作成する方法については、SharePoint Framework
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.localizationpriority: none
ms.openlocfilehash: 36aa779db0c45ab3724673cb0030a97cceef6a78
ms.sourcegitcommit: 72de146d11e81fd9777374dd3915ad290fd07d82
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2021
ms.locfileid: "59360814"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a>アプリで最初のアプリをビルドMicrosoft Teams実行する (SharePoint Framework) (SPFx)

このチュートリアルでは、単純な個人用アプリを実装する新Microsoft TeamsアプリSharePoint Framework SPFx作成する方法について説明します。 たとえば、個人用アプリ *には、* 個別に使用するタブのセットが含まれます。 チュートリアルでは、Teams アプリの構造、アプリをローカルで実行する方法、アプリを SharePoint に展開する方法について説明します。

## <a name="before-you-begin"></a>はじめに

前提条件をインストールして、開発環境がセットアップされていることを確認します。

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="get-organized"></a>すっきり整理しましょう。

前提条件に加えて、サイト コレクションの管理者SharePoint必要があります。  ここで、ホスティング用にアプリを展開します。  M365 開発者プログラム テナントを使用している場合は、プログラムに登録するときに設定した管理者アカウントを使用します。  

## <a name="create-your-project"></a>プロジェクトを作成する

Teams ツールキットを使用して、最初のプロジェクトを作成します。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Visual Studio Code を開きます。
1. サイドバーのTeamsアイコンを選択して、ウィンドウを開Teams Toolkit。

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. **[新しいプロジェクトの作成]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. **[新しい Teams アプリを作成]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. [機能の **選択] セクションで** 、[タブ] を選択 **し、[OK]** を **選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. **[Frontend ホスティングの種類] セクション** で、[SharePoint Framework **] (SPFx) を選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="新規アプリのホスティングを選択する方法を示すスクリーンショット":::。

1. [フレームワーク **] セクションで**、[フレームワーク]**をReact。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="Select Framework":::

1. Web パーツ名を求める **メッセージが表示された場合** は **、Enter キーを押** して既定値を受け入れる。

1. Web パーツの説明を求める **メッセージが表示された** 場合は **、Enter キーを押** して既定値を受け入れる。

1. プログラミング言語の入力を求 **めるメッセージが表示された場合は、Enter****キーを押** して既定値を受け入れる。

1. ワークスペース フォルダーを選択します。  ワークスペース フォルダー内に、作成中のプロジェクト向けのフォルダーが作成されます。

1. `helloworld` のように、アプリに適した名前を入力します。  アプリの名前は、英数字のみで構成されている必要があります。  **Enter** キーを押して続行します。

   数秒後に Teams アプリが作成されます。

# <a name="command-line"></a>[コマンド ライン](#tab/cli)

`teamsfx` CLI を使用して、最初のプロジェクトを作成します。  プロジェクト フォルダーを作成するフォルダーから開始します。

``` bash
teamsfx new
```

CLI では、プロジェクトを作成するためのいくつかの質問を行います。  各質問には、回答方法 (矢印キーで選択肢を選択するなど) が記載されています。  質問に答えた後、**Enter** キーを押して選択を確認します。

1. **[新しい Teams アプリを作成]** を選択します。
1. [タブ **] を選択します**。
1. [SharePoint Framework **(SPFx)** フロントエンド ホスティング] を選択します。
1. [フレームワーク **React** 選択します。
1. Web **パーツ名の Enter** **キーを押します**。
1. Web **パーツの説明** に **対して Enter キーを押します**。
1. プログラミング **言語の Enter** **キーを押します**。
1. **Enter** キーを押して、既定のワークスペース フォルダーを選択します。
1. `helloworld` のように、アプリに適した名前を入力します。  アプリの名前は、英数字のみで構成されている必要があります。

   すべての質問に回答すると、プロジェクトが作成されます。

---

- [ユーザー向け開発の詳細については、SharePoint Framework](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a>ソース コードのツアーを開始する

このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。

プロジェクトをTeams Toolkitした後、プロジェクト内でホストされている Teamsの基本的な個人用アプリを構築するコンポーネントがSharePoint Framework。  プロジェクトのディレクトリとファイルには、Visual Studio Code の [エクスプローラー] 領域に表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="Visual Studio Code で個人用アプリ向けのアプリのプロジェクト ファイルを表示したスクリーンショット。":::

ツールキットは、セットアップ時に追加した機能に基づいて、プロジェクト ディレクトリにスキャフォールディングを自動的に作成します。 Teams ツールキットは、`.fx` ディレクトリにアプリの状態を保持します。 

- プロジェクト作成時に選択した設定が `.fx/settings.json` に保存されます。
- プロジェクトの状態はに格納されます `.fx/env.*.json` 。

また、Teams情報がディレクトリに格納 `appPackage` されます。

- アプリ アイコンは PNG ファイルとして `appPackage/color.png` と `appPackage/outline.png` に格納されます。
- 開発者ポータルに発行するアプリ マニフェストは、Teamsに格納されます `appPackage/manifest.source.json` 。


Webpart プロジェクトでSPFxしたので、次のファイルは UI に関連します。

- フォルダーには `SPFx/src/webparts/{webpart}` 、webpart のSPFxされます。
- このファイル `.vscode/launch.json` には、デバッグ パレットで使用できるデバッグ構成が記述されています。

Webparts for SharePointのTeamsについては、次の[ドキュメントをSharePointしてください](/sharepoint/dev/spfx/build-for-teams-overview)。

## <a name="run-your-app-locally"></a>アプリをローカルで実行する

Teams Toolkitを使用すると、アプリをローカルでホストし、ワークベンチから実行SharePoint Framework[できます](/sharepoint/dev/spfx/debug-in-vscode)。

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a>Visual Studio Code でアプリをローカルにビルドして実行する

アプリをローカルに構築して実行するには、以下のようにします。

1. [Visual Studio Code F5 キー **を押** します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="ローカル ワークベンチでアプリをSPFxする方法を示すスクリーンショット。":::

   > [!NOTE]
   > アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。  ビルドが完了すると、ブラウザー ウィンドウが自動的に開SharePointワークベンチが読み込まれます。  この作業には 3 ～ 5 分かかります。

   ワークベンチのSharePointが読み込まれます。

   >[!NOTE]
   > ツールキットでは、必要に応じてローカル証明書をインストールするようメッセージが表示されます。 この証明書により、Teams は `https://localhost` からアプリケーションを読み込むことができます。 以下のダイアログが表示されたら、「はい」を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Teams がアプリケーションを localhost からロードできるようにするための SSL 証明書のインストールを求めるメッセージが表示される方法を示すスクリーンショット":::。

1. [Web **パーツとアイコンの追加] を** 選択して Web パーツを追加します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="ポップアップで実行されているSPFxを示すスクリーンショットを示し、Web パーツを表示します。":::

1. メニューから Web パーツを選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="ポップアップと一緒にSPFxワークベンチで Web パーツの選択を追加する方法を示すスクリーンショット。":::

   アプリが実行されている必要があります。  通常のデバッグ アクティビティは、他の web パーツ (ブレークポイントの設定など) と同様SPFx実行できます。

   > [!TIP]
   > ブラウザー ウィンドウの render メソッドにブレークポイントを配置し `SPFx/src/webparts/{webpart}/{webpart}.ts` 、再読み込みしてみてください。 VS Codeコード内のブレークポイントで停止します。

## <a name="deploy-your-app-to-sharepoint"></a>アプリをアプリに展開SharePoint

展開にSharePointアプリ カタログが存在することを確認します。  存在しない場合は、作成 [します](/sharepoint/use-app-catalog)。  アプリ カタログを完全に作成するには、最大で 15 分かかる場合があります。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Visual Studio Code を開きます。
1. サイドバーからTeams Toolkitアイコンを選択してTeamsします。
1. [クラウド **でプロビジョニング] を選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="プロビジョニング コマンドを示すスクリーンショット":::

   右下隅のダイアログを見て、進行状況を監視できます。  数秒後に、次の通知が表示されます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="プロビジョニング完了ダイアログを示すスクリーンショット。":::

1. プロビジョニングが完了したら、[クラウドに **展開する] を選択します**。

1. 現在、自動展開は使用できません。  手動でビルドして展開するように求めるダイアログが表示されます。 [**ビルド とパッケージSharePoint選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="[Sharepoint パッケージのビルド] ダイアログのスクリーンショット":::

# <a name="command-line"></a>[コマンド ライン](#tab/cli)

ターミナル ウィンドウで次の設定を行います。

1. `teamsfx provision` を実行します。

   ``` bash
   teamsfx provision
   ```

   Azure サブスクリプションにログインするように求めるメッセージが表示される場合があります。  必要に応じて、Azure リソースに使用する Azure サブスクリプションを選択するように求めるメッセージが表示されます。

   > [!NOTE]
   > アプリのホスティングに使用される Azure リソースは常にいくつかある。

1. `teamsfx deploy` を実行します。

   ``` bash
   teamsfx deploy
   ```

1. メッセージが表示されたら、[パッケージの **ビルドSharePoint選択します**。

---

パッケージSharePointプロジェクト内 `SPFx/sharepoint/solution` に保存されます。  アップロードを次の方法でSharePoint。

1. M365 管理コンソールにログインし、アプリ カタログSharePoint移動します。

   1. を `https://admin.microsoft.com/AdminPortal/Home` 開きます。
   1. [**管理センター] で**、**管理センター** SharePoint選択します。
   1. サイドバー メニュー **から [その他の** 機能] を選択します。
   1. [アプリ **] で [開く** ] **を押します**。
   1. [アプリ **カタログ] を選択します**。

1. [アプリ **の配布] を選択SharePoint。**

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="アプリを配布SharePoint。":::

1. [アップロード]**を選択します**。

1. [ファイル **の選択] を選択します**。

1. プロジェクト内 `{project}.sppkg` のフォルダー内 `SPFx/sharepoint/solution` のファイルを見つける。 [**開く**]を選択します。

1. **[OK]** をクリックします。

1. 展開SharePoint自動的に開始されます。 [この **ソリューションを組織内のすべてのサイト** で使用できる] が選択されているのを確認します。 次に、[展開] **を選択します**。

1. [ファイル] **タブを選択** します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="[アプリ カタログ] の [ファイル] タブSharePoint選択します。":::

1. 展開したパッケージを選択し、右上隅から [同期 **Teamsを選択** します。

    > [!Note]
    > 同期プロセスTeams数分かかる場合があります。  ブラウザーの右側に、アプリが正常に同期されたことを示すメッセージが表示Teams。

   アプリケーションを開Teams (またはサインイン時 `https://teams.microsoft.com` )。  サイドバーのトリプルドットを押し、[すべてのアプリ] **を選択します**。  アプリは、組織カテゴリ用 **に構築されたアプリに配置** されます。  そこからアプリを追加できます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="アプリ内のアプリを示すスクリーンショットTeams":::

## <a name="see-also"></a>関連項目

* [チュートリアルの概要](code-samples.md)
* [会話ボット アプリを作成する](first-app-bot.md)
* [メッセージング拡張機能を作成する](first-message-extension.md)
* [コード サンプル](https://github.com/OfficeDev/Microsoft-Teams-Samples)
