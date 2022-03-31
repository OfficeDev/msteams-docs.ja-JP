---
title: '[チャネルまたはグループ] タブを作成する'
author: laujan
description: コード例を使用したソース コードの確認など、Yeoman Generator Microsoft Teamsを使用してチャネルとグループ タブを作成するクイック スタート ガイド。
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 7d74a49ff85986b27ec30eeffbc15ca836a6a94b
ms.sourcegitcommit: 52af681132e496a57b18f468c5b73265a49a5f44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2022
ms.locfileid: "64590671"
---
# <a name="channel-or-group-tab"></a>[チャネルまたはグループ] タブ

チャネル/グループ タブは、コンテンツをチャネルやグループのチャットに配信します。また、専用の Web ベースのコンテンツまわりに関する共同作業スペースを作成するのに優れた方法です。

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>カスタム チャネルまたはグループ タブを作成するには、Node.js

1. コマンド プロンプトで、次のコマンドを入力して [Yeoman](https://yeoman.io/) パッケージと [gulp-cli](https://www.npmjs.com/package/gulp-cli) パッケージをインストールし、次のコマンドをインストール **Node.js。**

    ```cmd
    npm install yo gulp-cli --global
    ```

2. コマンド プロンプトで、次のコマンドMicrosoft Teamsしてアプリ ジェネレーターをインストールします。

    ```cmd
    npm install generator-teams --global
    ```

チャネルまたはグループ タブを作成する手順は次のとおりです。

* [チャネルまたはグループ タブを使用してアプリケーションを生成する](#generate-your-application-with-a-channel-or-group-tab)
* [アプリ パッケージを作成する](#create-your-app-package)
* [アプリケーションのビルドと実行](#build-and-run-your-application)
* [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab)
* [アップロードにアプリケーションをTeams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>チャネルまたはグループ タブを使用してアプリケーションを生成する

1. コマンド プロンプトで、チャネルまたはグループ タブの新しいディレクトリを作成します。

1. 新しいディレクトリに次のコマンドを入力して、アプリ ジェネレーター Microsoft Teams開始します。

    ```cmd
    yo teams
    ```

1. manifest.json ファイルを更新するようにアプリ ジェネレーターから求Microsoft Teams一連の質問に値 **を入力** します。

    ![ジェネレーターの開くスクリーンショット](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <details>
    <summary><b>manifest.json ファイルを更新する一連の質問</b></summary>

    * **ソリューション名は何ですか?**

        ソリューション名はプロジェクト名です。 [Enter] を選択すると、候補の名前を受け入 **れできます**。

    * **ファイルをどこに保存しますか?**

        現在、プロジェクト ディレクトリにいます。 [Enter] を **選択します**。

    * **アプリ プロジェクトMicrosoft Teamsタイトル**

        タイトルはアプリ パッケージ名で、アプリ マニフェストと説明で使用されます。 タイトルを入力するか、Enter **を選択して** 既定の名前を受け入れる。

    * **(会社) の名前(最大 32 文字)**

        会社名はアプリ マニフェストで使用されます。 会社名を入力するか、 **Enter を選択して** 既定の名前を受け入れる。

    * **どのマニフェスト バージョンを使用しますか?**

        既定のスキーマを選択します。

    * **クイック スキャフォールディング(Y/n)**

        既定値は yes です。 **n と入力** して Microsoft パートナー ID を入力します。

    * **Microsoft パートナー ID をお持ちの場合は、Microsoft パートナー ID を入力してください。(スキップする場合は空白のままにする)**

        このフィールドは必須ではなく、既に Microsoft パートナー ネットワークに参加している場合にのみ [使用する必要があります](https://partner.microsoft.com)。

    * **プロジェクトに何を追加しますか?**

        [ **( ) &ast; ] タブを選択します**。

    * **このソリューションをホストする URL**

        既定では、ジェネレーターは Azure Web サイトの URL を提案します。 アプリをローカルでテストしているだけなので、有効な URL は必要ありません。

    * **アプリ/タブの読み込み時に読み込みインジケーターを表示しますか?**

        アプリ **またはタブ** の読み込み時に読み込みインジケーターを含めないを選択します。 既定値は no で、 **n と入力します**。

    * **個人用アプリをタブ ヘッダーバーなしでレンダリングしますか?**

        タブ **ヘッダー** バーなしでレンダリングする個人用アプリを含めないを選択します。 既定値は no で、 **n と入力します**。

    * **テスト フレームワークと初期テストを含めるには?(y/N)**

        この **プロジェクトの** テスト フレームワークを含めないを選択します。 既定値は no で、 **n と入力します**。

    * **ESLint のサポートを含めませんか?(y/N)**

        ESLint サポートを含めないを選択します。 既定値は no で、 **n と入力します**。

    * **テレメトリに Azure Applications インサイト使用しますか?(y/N)**

        [**データを含**[めAzure アプリケーション インサイト](/azure/azure-monitor/app/app-insights-overview)。 既定値は no です。 **n と入力します**。

    * **既定のタブ名 (最大 16 文字)?**

        タブの名前を指定します。このタブ名は、ファイルまたは URL パス コンポーネントとしてプロジェクト全体で使用されます。

    * **作成するタブの種類**

        矢印キーを使用して、[構成可能] **タブを選択** します。

    * **Tab に使用するスコープは何ですか?**

        チームまたはグループ チャットを選択できます。

    * **タブに対Microsoft Azure Active Directory (Azure AD) シングル サインオンのサポートが必要ですか?**

        タブ **に** シングル サインオンMicrosoft Azure Active Directory (Azure AD) のサポートを含めないを選択します。既定値ははい、n と **入力します**。

    * **このタブをオンラインで使用SharePointしますか?(Y/n)**

        **n と入力します**。

    </details>

> [!IMPORTANT]
> パス コンポーネント **yourDefaultTabNameTab** は、[既定] タブ名のジェネレーターに入力した値に Tab という単語を加 **えた値です**。
>
> たとえば、DefaultTabName は **MyTab** で、 **次に /MyTabTab/**

### <a name="create-your-app-package"></a>アプリ パッケージを作成する

アプリケーションをビルドして実行するには、アプリ パッケージが必要Teams。 アプリ パッケージは、 **manifest.json** ファイルを検証し、./package ディレクトリに zip フォルダーを生成する gulp タスクを使用 **して作成** されます。 コマンド プロンプトで、次のコマンドを入力します。

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>アプリケーションのビルドと実行

#### <a name="build-your-application"></a>アプリケーションのビルド

コマンド プロンプトで次のコマンドを入力して、ソリューションを **./dist フォルダーに変換** します。

```cmd
gulp build
```

#### <a name="run-your-application"></a>アプリケーションを実行する

1. コマンド プロンプトで、次のコマンドを入力してローカル Web サーバーを起動します。

    ```bash
    gulp serve
    ```

1. ブラウザー `http://localhost:3007/<yourDefaultAppNameTab>/` に入力して、アプリケーションのホーム ページを表示します。

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="[既定] タブ" border="true":::

1. タブ構成ページを表示するには、 に移動します `https://localhost:3007/<yourDefaultAppNameTab>/config.html`。 次に示します。

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="タブ構成ページ" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

タブへのセキュリティで保護されたトンネルを確立するには、localhost を終了し、次のコマンドを入力します。

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> **タブが ngrok** をMicrosoft Teamsして正常に保存された後、トンネル セッションが終了するまで、Teamsで表示できます。 ngrok セッションを再起動する場合は、新しい URL でアプリを更新する必要があります。

### <a name="upload-your-application-to-teams"></a>アップロードにアプリケーションをTeams

1. [ストア] にMicrosoft Teamsし、[**ストア**&nbsp;] :::image type="content" source="~/assets/images/tab-images/store.png" alt-text="をTeamsします":::。
1. [アプリ **の管理] を選択します**。
1. [**アプリの発行] を** 選択 **しアップロードアプリを作成します**。

    :::image type="content" source="~/assets/images/tab-images/publish-app.png" alt-text="アップロードカスタム アプリ" border="true":::

1. プロジェクト ディレクトリに移動し、 **./package** フォルダーを参照し、アプリ パッケージの zip フォルダーを選択して、[開く] を選択 **します**。
    
    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="[アップロードされたチャネル] タブ" border="true":::

1. ポップアップ **ウィンドウで** [追加] を選択します。 タブがアップロードされ、Teams。
    
    > [!NOTE]
    > [  **追加]** がダイアログ ボックスに表示されない場合は、アップロードしたアプリ パッケージの zip フォルダーのマニフェストから次のコードを削除します。 もう一度フォルダーを圧縮し、フォルダーにTeams。
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. チームに戻り、タブ➕を追加するチャネルを選択し、タブ バーから選択し、リストからタブを選択します。
1. タブを追加するには、指示に従います。チャネルまたはグループ タブのカスタム構成ダイアログ ボックスがあります。
1. [ **保存] を** 選択すると、タブがチャネルのタブ バーに追加されます。

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="チャネル タブのアップロード" border="true":::

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>カスタム チャネルまたはグループ タブを作成し、ASP.NET Core

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. 次のコマンドを使用して、サンプル リポジトリを新しいディレクトリに複製するか、ソース コードをダウンロード [してファイルを](https://github.com/OfficeDev/Microsoft-Teams-Samples) 抽出できます。

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

チャネルまたはグループ タブを作成する手順は次のとおりです。

* [チャネルまたはグループ タブを使用してアプリケーションを生成する](#generate-your-application-with-a-channel-or-group-tab-1)
* [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab-1)
* [アプリケーションを更新する](#update-your-application)
* [アプリケーションのビルドと実行](#build-and-run-your-application-1)
* [開発者ポータルでアプリ パッケージを更新する](#update-your-app-package-with-developer-portal)
* [アプリをプレビュー Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>チャネルまたはグループ タブを使用してアプリケーションを生成する

1. [プロジェクトVisual Studio開き、[**プロジェクトまたはソリューションを開く] を選択します**。

1. Microsoft-Teams-Samplessamplestab-channel-grouprazor-csharp  >  >  >  フォルダーに移動し、**channelGroupTab.sln を開きます**。

1. このVisual Studio **F5** キーを押するか、アプリケーションの  [デバッグ] メニューから [デバッグの開始] を選択して、アプリケーションが正しく読み込まれたか確認します。 ブラウザーで、次の URL に移動します。

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>ソース コードを確認する</b></summary>

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは、ASP.NET Core 3.1 Web アプリケーションの空のテンプレートから作成され、セットアップ時に [**詳細設定 ] * [HTTPS** の構成] チェック ボックスがオンになっています。 MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。 さらに、空のテンプレートでは `Configure()` 既定では静的コンテンツの提供が有効ではないので、静的ファイル ミドルウェアは次のコードを使用してメソッドに追加されます。

```csharp
public void ConfigureServices(IServiceCollection services)
  {
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

#### <a name="wwwroot-folder"></a>wwwroot フォルダー

この ASP.NET Core Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core Index と呼ばれるファイルを **サイトの既定** またはホーム ページとして扱います。 ブラウザーの URL がサイトのルートをポイントすると、 **Index.cshtml** がアプリケーションのホーム ページとして表示されます。

#### <a name="tabcs"></a>Tab.cs

このC#ファイルには、構成時に **Tab.cshtml から呼び出されるメソッドが** 含まれる。

#### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

* 192 x 192 ピクセルのフル カラー アイコン。
* 32 x 32 ピクセルの透明なアウトライン アイコン。
* アプリ **の属性を指定する manifest.json** ファイル。

これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。 ユーザーがタブの`configurationUrl`追加または更新を選択すると、Microsoft Teamsがマニフェストに読み込み、IFrame に埋め込み、タブに表示されます。

#### <a name="csproj"></a>.csproj

[ファイル] ウィンドウVisual Studio ソリューション エクスプローラープロジェクトを右クリックし、[ファイルの編集] **Projectします**。 ファイルの最後に、アプリケーションのビルド時に zip フォルダーを作成および更新する次のコードが表示されます。

```xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行して、タブへのセキュリティで保護されたトンネルを確立します。

```cmd
ngrok http 3978 --host-header=localhost
```

ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。

### <a name="update-your-application"></a>アプリケーションを更新する

1. **PagesShared フォルダー** > **に移動** し、**_Layout.cshtml** を開き、次の項目を <head> タグ セクション:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > URL は最新バージョンを `<script src="...">` 表すので、このページの URL をコピーして貼り付けは行ないます。 SDK の最新バージョンを取得するには、常に [JavaScript API Microsoft Teams移動します](https://www.npmjs.com/package/@microsoft/teams-js)。
    
1. タグの上部に 、 `script` への呼び出しを挿入します `microsoftTeams.initialize();`。

1. Pages フォルダーに **移動し** 、 **Tab.cshtml を開きます。**

    **Tab.cshtml 内** では、アプリケーションは、赤または灰色のアイコンでタブを表示するための 2 つのオプション ボタンをユーザーに表示します。 [灰色の **選択] または**  **[赤の選択** `saveGray()` `saveRed()``settings.setValidityState(true)`] ボタンを選択すると、構成ページの [保存] ボタンがそれぞれトリガーまたは設定され、有効になります。 このコードをTeams構成要件を完了し、インストールを続行できます。 のパラメーターが `settings.setSettings` 設定されます。 最後に、 `saveEvent.notifySuccess()` コンテンツ URL が正常に解決されたことを示すために呼び出されます。

1. タブへの `websiteUrl` HTTPS `contentUrl` ngrok URL を使用して、各関数の値と値を更新します。

    これで、 **y8rCgT2b が ngrok** URL に置き換えられた次のコードを含める必要があります。

    ```javascript
        
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
        });
        }
    ```

1. 更新された **Tab.cshtml を保存します**。

### <a name="build-and-run-your-application"></a>アプリケーションのビルドと実行

1. このVisual Studio **F5 キーを押するか、[** デバッグ] メニューから [**デバッグ** の開始] **を選択** します。

1. ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を介してコンテンツ ページに移動して、 **ngrok** が正常に実行され、正常に動作されていることを確認します。

    > [!TIP]
    > この記事で示す手順を実行するには、Visual Studioと ngrok の両方でアプリケーションを実行する必要があります。 アプリケーションの実行を停止する必要がある場合Visual Studio **ngrok を実行し続ける必要があります**。 アプリケーションの要求がアプリケーションで再起動されると、アプリケーションの要求をリッスンしてVisual Studio。 ngrok サービスを再起動する必要がある場合は、新しい URL が返され、新しい URL でアプリケーションを更新する必要があります。

### <a name="update-your-app-package-with-developer-portal"></a>開発者ポータルでアプリ パッケージを更新する

1. [次へ] Microsoft Teams。 Web ベースの [バージョンを使用する](https://teams.microsoft.com)場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。

1. [開発者ポータル] **に移動** Teams。

1. [アプリ **] を開** き、[アプリの **インポート] を選択します**。

1. アプリ パッケージの名前は次 **tab.zip**。 これは、次のパスで使用できます。

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. [ **tab.zip** を選択し、開発者ポータルで開きます。

1. 既定の **アプリ ID が** 作成され、[基本情報] **セクションに設定** されます。

1. [説明] にアプリの短い説明と長い説明 **を追加します**。

1. [ **開発者情報]** で、必要な詳細を追加し、[Web サイト] (有効な **HTTPS URL** である必要があります) で ngrok HTTPS URL を指定します。

1. アプリ **の URL で、** プライバシー ポリシーを更新し `https://<yourngrokurl>/privacy` 、使用条件を更新して `https://<yourngrokurl>/tou` 保存します。

1. [ **アプリの機能] で**、[個人用アプリ] を選択し、[名前] を入力してコンテンツ **URL を更新** します `https://<yourngrokurl>/personalTab`。 [Web サイトの URL] フィールドは空白のままにします。 

1. **[保存]** を選択します。

1. [ドメイン] セクションでは、タブのドメインに HTTPS プレフィックスのない ngrok URL が含まれている必要があります `<yourngrokurl>.ngrok.io`。

### <a name="preview-your-app-in-teams"></a>アプリをプレビュー Teams

1. [開発者 **ポータル] ツール バー Teams**[プレビュー] を選択します。 開発者ポータルは、アプリが正常にサイドロードされたことを通知します。

1. [アプリ **の管理] を選択します**。 アプリがサイドロードされたアプリに表示されます。

1. 検索を使用してアプリを検索し、[アプリ] を &#x25CF;&#x25CF;&#x25CF;。

1. [詳細の **表示] オプションを** 選択します。 アプリの詳細ウィンドウがアプリに表示されます。

1. [アプリ&nbsp;:::image type="content" source="~/assets/images/tab-images/app-dropdown.png" alt-text="の詳細] ドロップダウン" border="true":::&nbsp; >  **[チームに追加] を選択** して、チームにタブを読み込む。 タブは、このタブでTeams。

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="[チャネル] タブの ASPNET がアップロードされました" border="true":::

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>MVC を使用してカスタム チャネルまたはグループ タブ ASP.NET Coreする

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. 次のコマンドを使用して、サンプル リポジトリを新しいディレクトリに複製するか、ソース コードをダウンロード [してファイルを](https://github.com/OfficeDev/Microsoft-Teams-Samples) 抽出できます。

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

チャネルまたはグループ タブを作成する手順は次のとおりです。

* [チャネルまたはグループ タブを使用してアプリケーションを生成する](#generate-your-application-with-a-channel-or-group-tab-2)
* [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab-2)
* [アプリケーションを更新する](#update-your-application-1)
* [アプリケーションのビルドと実行](#build-and-run-your-application-2)
* [開発者ポータルでアプリ パッケージを更新する](#update-your-app-package-with-developer-portal-1)
* [アプリをプレビュー Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>チャネルまたはグループ タブを使用してアプリケーションを生成する

1. [プロジェクトVisual Studio開き、[**プロジェクトまたはソリューションを開く] を選択します**。

1. Microsoft-Teams-Samplessamplestab-channel-groupmvc-csharp  >  >  >  フォルダーに移動し、**ChannelGroupTabMVC.sln を開きます**。

1. このVisual Studio **F5** キーを押するか、アプリケーションの  [デバッグ] メニューから [デバッグの開始] を選択して、アプリケーションが正しく読み込まれたか確認します。 ブラウザーで、次の URL に移動します。

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>ソース コードを確認する</b></summary>

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは、3.1 web アプリケーション ASP.NET Coreテンプレートから作成され、セットアップ時に [Advanced **- Configure for HTTPS**] チェック ボックスがオンになっています。 MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。 さらに、空のテンプレートでは `Configure()` 既定では静的コンテンツの提供が有効ではないので、静的ファイル ミドルウェアは次のコードを使用してメソッドに追加されます。

```csharp
public void ConfigureServices(IServiceCollection services)
  {
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

#### <a name="wwwroot-folder"></a>wwwroot フォルダー

この ASP.NET Core Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

#### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

* 192 x 192 ピクセルのフル カラー アイコン。
* 32 x 32 ピクセルの透明なアウトライン アイコン。
* アプリ **の属性を指定する manifest.json** ファイル。

これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。

#### <a name="csproj"></a>.csproj

[ファイル] ウィンドウVisual Studio ソリューション エクスプローラープロジェクトを右クリックし、[ファイルの編集] **Projectします**。 ファイルの最後に、アプリケーションのビルド時に zip フォルダーを作成および更新する次のコードが表示されます。

```xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

#### <a name="models"></a>モデル

**ChannelGroup.cs** は、構成中にコントローラーから呼び出される Message オブジェクトとメソッドを示します。

#### <a name="views"></a>ビュー

次に示すのは、MVC の ASP.NET Coreです。

* ホーム: ASP.NET Core Index と呼ばれるファイルをサイトの既定またはホーム ページとして扱います。 ブラウザーの URL がサイトのルートをポイントすると、 **Index.cshtml** がアプリケーションのホーム ページとして表示されます。

* 共有: 部分ビュー マークアップ **_Layout.cshtml** には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれます。 また、ライブラリのTeamsします。

#### <a name="controllers"></a>コントローラー

コントローラーは、プロパティを使用 `ViewBag` してビューに動的に値を転送します。

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行して、タブへのセキュリティで保護されたトンネルを確立します。

```cmd
ngrok http 3978 --host-header=localhost
```

ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。

### <a name="update-your-application"></a>アプリケーションを更新する

1. **ViewsShared フォルダー** > **に移動** し、**_Layout.cshtml** を開き、次の項目を <head> タグ セクション:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > URL は最新バージョンを `<script src="...">` 表すので、このページの URL をコピーして貼り付けは行ないます。 SDK の最新バージョンを取得するには、常に [JavaScript API Microsoft Teams移動します](https://www.npmjs.com/package/@microsoft/teams-js)。
    
1. タグの上部に 、 `script` への呼び出しを挿入します `microsoftTeams.initialize();`。

1. Tab フォルダーに **移動し** 、 **Tab.cshtml を開きます**

    **Tab.cshtml 内** では、アプリケーションは、赤または灰色のアイコンでタブを表示するための 2 つのオプション ボタンをユーザーに表示します。 [灰色の **選択] または**  **[赤の選択** `saveGray()` `saveRed()``settings.setValidityState(true)`] ボタンを選択すると、構成ページの [保存] ボタンがそれぞれトリガーまたは設定され、有効になります。 このコードをTeams構成要件を完了し、インストールを続行できます。 のパラメーターが `settings.setSettings` 設定されます。 最後に、 `saveEvent.notifySuccess()` コンテンツ URL が正常に解決されたことを示すために呼び出されます。 

1. タブへの `websiteUrl` HTTPS `contentUrl` ngrok URL を使用して、各関数の値と値を更新します。

    これで、 **y8rCgT2b が ngrok** URL に置き換えられた次のコードを含める必要があります。

    ```javascript

        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    
        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. 更新された **Tab.cshtml を保存してください**。

### <a name="build-and-run-your-application"></a>アプリケーションのビルドと実行

1. このVisual Studio **F5 キーを押するか、[** デバッグ] メニューから [**デバッグ** の開始] **を選択** します。

1. ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を介してコンテンツ ページに移動して、 **ngrok** が正常に実行され、正常に動作されていることを確認します。

    > [!TIP]
    > この記事で示す手順を実行するには、Visual Studioと ngrok の両方でアプリケーションを実行する必要があります。 アプリケーションの実行を停止する必要がある場合Visual Studio **ngrok を実行し続ける必要があります**。 アプリケーションの要求がアプリケーションで再起動されると、アプリケーションの要求をリッスンしてVisual Studio。 ngrok サービスを再起動する必要がある場合は、新しい URL が返され、新しい URL でアプリケーションを更新する必要があります。

### <a name="update-your-app-package-with-developer-portal"></a>開発者ポータルでアプリ パッケージを更新する

1. [次へ] Microsoft Teams。 Web ベースの [バージョンを使用する](https://teams.microsoft.com)場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。

1. [開発者ポータル **] に** 移動Teams。

1. [アプリ **] を開** き、[アプリの **インポート] を選択します**。

1. アプリ パッケージの名前は次 **tab.zip**。 これは、次のパスで使用できます。

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. [ **tab.zip** を選択し、開発者ポータルで開きます。

1. 既定の **アプリ ID が** 作成され、[基本情報] **セクションに設定** されます。

1. [説明] にアプリの短い説明と長い説明 **を追加します**。

1. [ **開発者情報]** で、必要な詳細を追加し、[Web サイト] (有効な **HTTPS URL** である必要があります) で ngrok HTTPS URL を指定します。

1. アプリ **の URL で、** プライバシー ポリシーを更新し `https://<yourngrokurl>/privacy` 、使用条件を更新して `https://<yourngrokurl>/tou` 保存します。

1. [ **アプリの機能] で**、[個人用アプリ] を選択し、[名前] を入力してコンテンツ **URL を更新** します `https://<yourngrokurl>/personalTab`。 [Web サイトの URL] フィールドは空白のままにします。

1. **[保存]** を選択します。

1. [ドメイン] セクションでは、タブのドメインに HTTPS プレフィックスのない ngrok URL が含まれている必要があります `<yourngrokurl>.ngrok.io`。

### <a name="preview-your-app-in-teams"></a>アプリをプレビュー Teams

1. [開発者 **ポータル] ツール バー Teams**[プレビュー] を選択します。 開発者ポータルは、アプリが正常にサイドロードされたことを通知します。

1. [アプリ **の管理] を選択します**。 アプリがサイドロードされたアプリに表示されます。

1. 検索を使用してアプリを検索し、[アプリ] を &#x25CF;&#x25CF;&#x25CF;。

1. [詳細の **表示] オプションを** 選択します。 アプリの詳細ウィンドウがアプリに表示されます。

1. [チャネル&nbsp;:::image type="content" source="~/assets/images/tab-images/app-dropdown.png" alt-text="] タブ [ASPNET のアップロード] [" border="true":::&nbsp; > **チームに追加] を選択して**、チームにタブを読みTeams。 タブは、このタブでTeams。

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="チャネル タブ ASPNET MVC アップロード" border="true":::

::: zone-end

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [コンテンツ ページを作成する](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
* [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)
* [削除ページを作成する](~/tabs/how-to/create-tab-pages/removal-page.md)
