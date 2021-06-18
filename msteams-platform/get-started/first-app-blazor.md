---
title: まず始める - Blazor を使用してTeamsアプリをビルドする
author: adrianhall
description: "\"こんにちは!\" を表示する Microsoft Teams アプリを迅速に作成します。 と .NET Blazor をMicrosoft Teams Toolkitメッセージを表示します。"
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: c336c97d477e7038cc41a5e593d71b0e98dc4643
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994393"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a>Blazor で最初のアプリをMicrosoft Teams実行する

このチュートリアルでは、.NET/Blazor で新しい Microsoft Teams アプリを作成し、Microsoft クライアントから情報を取得するための簡単な個人用アプリを実装Graph。 (個人用 *アプリには、* 個々の使用を対象にした一連のタブが含まれます)。 チュートリアルでは、Teams アプリの構造、アプリをローカルで実行する方法、Azure にアプリを展開する方法について説明します。

ビルドされたアプリは、現在のユーザーの基本的なユーザー情報を表示します。  許可が付与された場合、アプリは現在のユーザーとして Microsoft Graph に接続し、完全なプロフィールを取得します。

## <a name="before-you-begin"></a>始める前に

[前提条件](prerequisites.md)をインストールして、開発環境が整っていることを確認する

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)

## <a name="create-your-project"></a>プロジェクトを作成する

Teams ツールキットを使用して、最初のプロジェクトを作成します。

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

1. 2019 Visual Studioを開きます。

1. [新 **しいプロジェクトを作成する] を選択します**。

1. [アプリ **Microsoft Teams選択し、[** 次へ] を **押します**。  テンプレートを見つけるのに役立つには、プロジェクトの種類 **を使用** Microsoft Teams。

1. プロジェクトとソリューションに良い名前を付け、[次へ] を **押します**。

1. アプリケーション名と会社名を入力し、[作成] を **押します**。  アプリケーション名と会社名がエンド ユーザーに表示されます。

1. 数秒後に Teams アプリが作成されます。  プロジェクトを作成したら、M365 でシングル サインオンを設定します。

   - [TeamsFx **Project**  >  **SSO 用**  >  **に構成する] を選択します**。
   - メッセージが表示されたら、M365 管理者アカウントにサインインします。

# <a name="command-line"></a>[コマンド ライン](#tab/cli)

1. ターミナルを開き、プロジェクトを作成するディレクトリを選択します。

1. 次 `dotnet new -i` のコマンドからテンプレートをインストールNuGet。

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   これを行う必要があるのは、初めて、またはテンプレートを更新する場合のみです。 この[NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/)の最新バージョンを確認します。

1. ディレクトリを作成します。

   ``` bash
   mkdir helloworld
   ```

1. 新 `dotnet new` しいプロジェクトを作成するには、次のコマンドを実行します。

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. スキャフォールディングが完了したら、プロジェクトを次の展開Teams構成します。

   ``` bash
   teamsfx init
   ```

これで、デバッグ用にソリューションをVisual Studio開く必要があります。

---

## <a name="take-a-tour-of-the-source-code"></a>ソース コードのツアーを開始する

このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。

Teams ツールキットでプロジェクトを構成すると、Teams 向けの基本的な個人用タブを構築するためのコンポーネントがあります。 プロジェクト のディレクトリとファイルは、2019 年 2019 年のソリューション エクスプローラー Visual Studio表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="2019 年に個人用アプリのアプリ プロジェクト ファイルをVisual Studioスクリーンショット。":::

- アプリ アイコンは PNG ファイルとして `color.png` と `outline.png` に格納されます。
- 開発者ポータルを通じて発行するアプリ マニフェストは、Teamsに格納されます `Properties/manifest.json` 。
- 認証を支援するためにバックエンド `Controllers/BackendController.cs` コントローラーが用意されています。

セットアップ中にタブ アプリを作成したTeams Toolkit、基本的なタブに必要なすべてのコードが[Blazor Server としてスキャフォールディングされます](/aspnet/core/blazor)。

- `Pages/Tab.razor` は、フロントエンド アプリケーションのエントリ ポイントです。
- `TeamsFx.cs`ホスト `JS/src/index.js` との通信を初期化するためにTeamsされます。

バックエンド機能を追加するには、アプリケーションに ASP.NET Coreを追加します。

## <a name="run-your-app-locally"></a>アプリをローカルで実行する

Teams ツールキットでは、アプリをローカルで実行することができます。  これは、Teams が予想する正しいインフラを提供するために必要ないくつかのパーツで構成されています。

- Azure Active Directory を使用してアプリケーションを登録しました。  このアプリケーションには、アプリケーションが読み込まれる場所や、アクセスするバックエンド リソースに関連するアクセス許可があります。
- Web API は 、認証タスクを支援するために (IIS Express 経由で) ホストされ、アプリとアプリ間のプロキシとして機能Azure Active Directory。  
- アプリのマニフェストは、Developer Portal for Teams で生成され存在します。  Teams はアプリ マニフェストを使用して、接続しているクライアントにアプリをロードする場所を伝達します。

この作業が完了すると、Teams クライアント内でアプリを読み込むことができます。  Teams の Web クライアントを使用することで、標準的な Web 開発環境で HTML、CSS、JavaScript のコードを確認することができます。

アプリをローカルに構築して実行するには、以下のようにします。

1. Visual Studio Code で、**F5** を押して、アプリケーションをデバッグ モードで実行します。

1. 要求された場合は、ローカル デバッグ用の自己署名証明書 SSL 証明書をインストールします。

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Teams がアプリケーションを localhost からロードできるようにするための SSL 証明書のインストールを求めるメッセージが表示される方法を示すスクリーンショット":::。

1. Teams が Web ブラウザーに読み込まれ、サインインするようメッセージが表示されます。 Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。 M365 アカウントでサインインします。
1. Teams へのアプリのインストールを促すメッセージが表示された場合は、**[追加]** を押してください。

これでご使用のアプリが表示されます。

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="完了したアプリのスクリーンショット":::

他の Web アプリケーションと同様に、通常のデバッグ作業を行うことができます (ブレークポイントの設定など)。 このアプリはホット リロードをサポートしています。  プロジェクト内のファイルを変更すると、ページが再読み込みされます。

<!-- markdownlint-disable MD033 -->
<details>
<summary>デバッガーでアプリをローカルに実行した場合に発生することを説明します。</summary>

F5 を押すと、以下のように Teams ツールキットが表示されます。

1. Azure Active Directory を使用してアプリケーションを登録しました。
1. Microsoft Teams で "サイド読み込み" 用にアプリケーションを登録しました。
1. ローカルで実行されているアプリケーション バックエンドを開始しました。
1. アプリケーションのフロント エンドがローカルでホストされるようになりました。
1. アプリケーションMicrosoft Teams読み込むようTeamsコマンドを使用して Web ブラウザーで開始します (URL はアプリケーション マニフェスト内に登録されます)。

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>アプリをローカルで実行する場合の一般的な問題のトラブルシューティングを行う方法について説明します。</summary>

アプリをアプリ側で正常にTeamsするには、アプリ側の読み込みをMicrosoft 365開発アカウントを持っている必要があります。 アカウント開設の詳細については、「[前提条件](prerequisites.md#enable-sideloading)」を参照してください。

</details>

## <a name="deploy-your-app-to-azure"></a>アプリを Azure に展開する

展開は 2 つの手順で構成されます。  まず、必要なクラウド リソース (プロビジョニングとも呼ばれる) が作成され、アプリを構成するコードが作成されたクラウド リソースにコピーされます。

> **プレビュー**
>
> Blazor アプリのサポートは、新しいTeams Toolkit。  プロビジョニングと展開は、2019 年と 2019 年Visual Studio開発者ポータルの組み合わせでTeams。

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a>アプリのプロビジョニングと Azure App Service への展開

1. ソリューション エクスプローラーで、プロジェクト ノードを右クリックし、[発行] を **選択します**(または、[ビルド発行 **] メニュー項目**  >  **を** 使用します)。

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="プロジェクトの発行操作を選択する":::

1. [発行]**ウィンドウで****、[Azure] を選択します**。  [次 **へ] を押します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="発行ターゲットとして Azure を選択する":::

1. [Azure **App Service] (Windows) を選択します**。  [次 **へ] を押します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="発行ターゲットとして Azure App Service を選択する":::

1. 新 **+** しい App Service インスタンスを作成する場合に選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="新しいインスタンスを作成します。":::

1. [アプリ **サービスの作成 (Windows)** ダイアログボックスに、[名前] 、[サブスクリプション名]  、[**リソース** グループ]、および [ホスティング プラン] エントリ フィールドが設定されます。 App Service が既に実行されている場合は、既存の設定が選択されます。  新しいリソース グループとホスティング プランを作成することを選択できます (推奨)。  準備ができたら、[作成] を **選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="ホスティング プランとサブスクリプションの選択":::

1. [発行 **] ダイアログ** で、新しく作成されたインスタンスが自動的に選択されています。  準備ができたら、[完了] を **選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="新しいインスタンスを選択します。":::

1. [展開モード **] の** 横にある [編集] (鉛筆) アイコン **を押** し、[自己格納 **型] を選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="[自己格納型展開モード] を選択します。":::

1. [**発行**] を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="アプリをアプリ サービスに発行する":::

Visual Studio Azure App Service にアプリを展開すると、Web アプリがブラウザーに読み込まれます。  URL `/tab` の末尾に追加して、ページを表示します。

プロジェクトのプロパティ [ **発行] ウィンドウ** には、サイトの URL などの詳細が表示されます。 サイト URL をメモします。

## <a name="create-an-environment-for-your-app"></a>アプリの環境を作成する

アプリのタブTeams環境を使用して読み込む場所を管理する開発者 **ポータル** です。  環境を作成するには、次の方法を実行します。

1. 開発者ポータル[を開Teams。](https://dev.teams.microsoft.com)  M365 管理アカウントでサインインします。

1. サイドバーで 、[アプリ] を **選択します**。

1. アプリが 1 つのみである場合は、自動的に選択されます。  表示されない場合は、一覧からアプリを選択します。

1. [環境 **] を選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="環境の選択":::

1. [最初 **の環境を作成する] を選択します**。

1. 環境の名前を入力し、[追加] を **押します**。たとえば、_実稼働 ._

1. 新しく作成した環境が選択されている場合は、[最初の **環境変数を作成する] を押します**。

1. [名前 `azure_app_url` ] に入力 **します**。  Azure サイトの URL (なし) を Value `https://` として入力 **します**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="環境変数の作成":::

   [追加 **] を押します**。

## <a name="update-the-app-manifest"></a>アプリ マニフェストを更新します。

アプリ マニフェストが URL からタブを読み込 `localhost` み中です。  このセクションでは、アプリ マニフェストを調整して、作成した環境内にリストされている URL からタブを読み込む。

1. サイドバーで、[基本情報] **を選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="基本情報の選択":::

1. マニフェスト内には、URL の一部としてリスト `locahost:XXXXX` される場所が複数あります。  すべてのオカレンスを `{{azure_app_url}}` (中かっこを含む) に置き換えてください。

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="環境の基本情報を調整する":::

1. 完了したら、[保存] **を押します**。

1. サイドバーで、[機能] **を選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="機能の選択":::

1. [個人用 **] タブを選択します**。
1. [個人用] タブ **の横で**、3 つのドットを選択し、[編集] を **選択します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="個人用タブ設定の編集":::

1. URL を [コンテンツ URL] フィールドと [Web サイト **URL]** フィールド内の **環境変数に置き換** えます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="個人用タブ URL の編集":::

1. [ **更新] を押します**。

1. **[保存]** を押します。

1. サイドバーで、[シングル サインオン **] を選択します**。

1. アプリケーション `localhost` ID URI 内の **値を . に置き** 換える `{{azure_app_url}}` 。

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="シングル サインオンアプリケーション ID URI の編集":::

1. **[保存]** を押します。

1. サイドバーで[ドメイン] **を押します**。

1. [ドメイン **の追加] を押します**。

1. 有効なドメインとしてリストされていない場合は、有効なドメインとして追加し、[追加] `{{azure_app_url}}` を **押します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="ドメインの追加":::

ページの上部にある **[プレビュー] Teams** ボタンを使用して、アプリをアプリ内で起動Teams。

## <a name="see-also"></a>関連項目

- [React を使用して Teams アプリを作成する](first-app-react.md)
- [Web パーツTeamsアプリをSharePointする](first-app-spfx.md)
- [会話ボット アプリを作成する](first-app-bot.md)
- [メッセージング拡張機能を作成する](first-message-extension.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Web パーツTeamsアプリをSharePointする](first-app-spfx.md)
