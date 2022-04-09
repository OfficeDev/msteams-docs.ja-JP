---
title: '[チャネルまたはグループの作成] タブ'
author: laujan
description: コード例を使用してソース コードを確認するなど、Microsoft Teams用 Yeoman Generator を使用してチャネルとグループタブを作成するクイック スタート ガイド。
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: bc7cb1fceef586959be44ba680874914c4f07cc1
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2022
ms.locfileid: "64737044"
---
# <a name="channel-or-group-tab"></a>[チャネル] タブまたは [グループ] タブ

チャネル/グループ タブは、コンテンツをチャネルやグループのチャットに配信します。また、専用の Web ベースのコンテンツまわりに関する共同作業スペースを作成するのに優れた方法です。

::: zone pivot="node-java-script"

## <a name="create-a-custom-channel-or-group-tab-with-nodejs"></a>Node.jsを使用してカスタム チャネルまたはグループ タブを作成する

1. コマンド プロンプトで、Node.jsをインストールした後に次のコマンドを入力して [、Yeoman](https://yeoman.io/) パッケージと [gulp-cli](https://www.npmjs.com/package/gulp-cli) **パッケージをインストール** します。

    ```cmd
    npm install yo gulp-cli --global
    ```

2. コマンド プロンプトで、次のコマンドMicrosoft Teams入力して、アプリ ジェネレーターをインストールします。

    ```cmd
    npm install generator-teams --global
    ```

チャネルまたはグループ タブを作成する手順を次に示します。

* [チャネルまたはグループ タブを使用してアプリケーションを生成する](#generate-your-application-with-a-channel-or-group-tab)
* [アプリ パッケージを作成する](#create-your-app-package)
* [アプリケーションをビルドして実行する](#build-and-run-your-application)
* [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab)
* [アプリケーションをTeamsにアップロードする](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>チャネルまたはグループ タブを使用してアプリケーションを生成する

1. コマンド プロンプトで、チャネルまたはグループ タブの新しいディレクトリを作成します。

1. 新しいディレクトリに次のコマンドを入力して、Microsoft Teams アプリ ジェネレーターを起動します。

    ```cmd
    yo teams
    ```

1. Microsoft Teams アプリ ジェネレーターによってファイルを更新するように求められた一連の質問に値を`manifest.json`入力します。

    ![ジェネレーターを開くスクリーンショット](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <details>
    <summary><b>manifest.json ファイルを更新するための一連の質問</b></summary>

    * **ソリューション名は何ですか?**

        ソリューション名はプロジェクト名です。 **Enter** キーを押して、推奨される名前をそのまま使用できます。

    * **ファイルをどこに保存しますか?**

        現在、プロジェクト ディレクトリにいます。 Enter キーを **押します**。

    * **Microsoft Teams アプリ プロジェクトのタイトル**

        タイトルはアプリ パッケージ名であり、アプリ マニフェストと説明で使用されます。 タイトルを入力するか、 **Enter** キーを押して既定の名前をそのまま使用します。

    * **(会社名) の名前は?(最大 32 文字)**

        会社名はアプリ マニフェストで使用されます。 会社名を入力するか、 **Enter** を選択して既定の名前をそのまま使用します。

    * **どのマニフェスト バージョンを使用しますか?**

        既定のスキーマを選択します。

    * **クイック スキャフォールディング?(Y/n)**

        既定値は yes です。 **n と** 入力して、Microsoft パートナー ID を入力します。

    * **Microsoft パートナー ID をお持ちであれば、Microsoft パートナー ID を入力してください。(スキップするには空白のままにします)**

        このフィールドは必須ではなく、 [Microsoft パートナー ネットワーク](https://partner.microsoft.com)に既に参加している場合にのみ使用する必要があります。

    * **プロジェクトに何を追加しますか?**

        **タブを選択 ( &ast; ) します**。

    * **このソリューションをホストする URL は?**

        既定では、ジェネレーターは Azure Web サイト URL を提案します。 アプリをローカルでのみテストしているため、有効な URL は必要ありません。

    * **アプリ/タブの読み込み時に読み込みインジケーターを表示しますか?**

        アプリまたはタブの読み込み時に読み込みインジケーターを含 **めないように** 選択します。 既定値は no で、n と入力 **します**。

    * **個人用アプリをタブ ヘッダーバーなしでレンダリングしますか?**

        タブ ヘッダー バーなしでレンダリングする個人用アプリを含 **めないように** 選択します。 既定値は no で、 **n** と入力します。

    * **テスト フレームワークと初期テストを含めますか?(y/N)**

        このプロジェクトのテスト フレームワークを含 **めないことを** 選択します。 既定値は no で、n と入力 **します**。

    * **ESLint サポートを含めますか?(y/N)**

        ESLint サポートを含めないことを選択します。 既定値は no で、n と入力 **します**。

    * **テレメトリに Azure Applications インサイトを使用しますか?(y/N)**

        Azure アプリケーション インサイトを含 **めないように** 選択 [します](/azure/azure-monitor/app/app-insights-overview)。 既定値は no です。 **n と入力します**。

    * **既定のタブ名 (最大 16 文字)?**

        タブに名前を付けます。このタブ名は、ファイルまたは URL パス コンポーネントとしてプロジェクト全体で使用されます。

    * **どのような種類のタブを作成しますか?**

        方向キーを使用して、[ **構成可能** ] タブを選択します。

    * **タブに使用するスコープは何ですか?**

        チームまたはグループ チャットを選択できます。

    * **タブのMicrosoft Azure Active Directory (Azure AD) シングル サインオンのサポートが必要ですか?**

        タブのMicrosoft Azure Active Directory (Azure AD) シングル サインオンのサポートを含 **めないように** 選択します。既定値は yes で、n と入力 **します**。

    * **このタブをSharePoint Online で使用できるようにしますか?(Y/n)**

        **n と入力します**。

    </details>

> [!IMPORTANT]
> path コンポーネント **yourDefaultTabNameTab** は、 **既定のタブ名** と単語 **Tab** のジェネレーターに入力した値です。たとえば、 `DefaultTabName` **MyTab** は **/MyTabTab/** です。

<!--- TBD: this info seems removed from the main branch.
* A **full color icon** measuring 192 x 192 pixels.
* A **transparent outline icon** measuring 32 x 32 pixels.
* A `manifest.json` file that specifies the attributes of your app.
--->

### <a name="create-your-app-package"></a>アプリ パッケージを作成する

Teamsでアプリケーションをビルドして実行するためのアプリ パッケージが必要です。 アプリ パッケージは、ファイルを検証し、ディレクトリ内`./package`の zip フォルダーを`manifest.json`生成する gulp タスクを使用して作成されます。 コマンド プロンプトで、次のコマンドを入力します。

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>アプリケーションをビルドして実行する

#### <a name="build-your-application"></a>アプリケーションをビルドする

コマンド プロンプトで次のコマンドを入力して、ソリューションをフォルダーに `./dist` 挿入します。

```cmd
gulp build
```

#### <a name="run-your-application"></a>アプリケーションを実行する

1. コマンド プロンプトで次のコマンドを入力して、ローカル Web サーバーを起動します。

    ```bash
    gulp serve
    ```

1. ブラウザーに入力 `http://localhost:3007/<yourDefaultAppNameTab>/` して、アプリケーションのホーム ページを表示します。

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="既定のタブ" border="true":::

1. タブ構成ページを表示するには、 `http://localhost:3007/<yourDefaultAppNameTab>/config.html`. 次の図を示します。

    :::image type="content" source="~/assets/images/tab-images/configurationPage.png" alt-text="タブ構成ページ" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

タブへのセキュリティで保護されたトンネルを確立するには、localhost を終了し、次のコマンドを入力します。

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> タブが **ngrok** 経由でMicrosoft Teamsにアップロードされ、正常に保存されたら、トンネル セッションが終了するまでTeamsで表示できます。 ngrok セッションを再起動する場合は、新しい URL でアプリを更新する必要があります。

### <a name="upload-your-application-to-teams"></a>アプリケーションをTeamsにアップロードする

1. Microsoft Teamsに移動し、[**アプリ**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teamsストア":::] を選択します。
1. [**アプリの管理**] を選択し、**カスタム アプリをアップロードします**。
1. プロジェクト ディレクトリに移動し、 **./package** フォルダーに移動し、アプリ パッケージの zip フォルダーを選択して、[ **開く**] を選択します。

    :::image type="content" source="~/assets/images/tab-images/channeltabadded.png" alt-text="[アップロードされたチャネル] タブ" border="true":::

1. ダイアログで **[追加]** を選択します。 タブがTeamsにアップロードされます。

    > [!NOTE]
    > ダイアログ ボックスに  **[追加]** が表示されない場合は、アップロードされたアプリ パッケージ zip フォルダーのマニフェストから次のコードを削除します。 もう一度フォルダーを zip 形式で圧縮し、Teamsにアップロードします。
    >
    >```Json
    >"staticTabs": [],
    >"bots": [],
    >"connectors": [],
    >"composeExtensions": [],
    >```

1. タブを追加する手順に従います。チャネルまたはグループ タブのカスタム構成ダイアログがあります。
1. **[保存] を** 選択すると、タブがチャネルのタブ バーに追加されます。

    :::image type="content" source="~/assets/images/tab-images/channeltabuploaded.png" alt-text="[チャネル] タブがアップロードされました" border="true":::

    これで、Teamsでチャネルまたはグループ タブが正常に作成され、追加されました。

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a>ASP.NET Coreを使用してカスタム チャネルまたはグループ タブを作成する

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. 次のコマンドを使用してサンプル リポジトリを新しいディレクトリに複製するか、 [ソース コード](https://github.com/OfficeDev/Microsoft-Teams-Samples) をダウンロードしてファイルを抽出できます。

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

チャネルまたはグループ タブを作成する手順を次に示します。

* [チャネルまたはグループ タブを使用してアプリケーションを生成する](#generate-your-application-with-a-channel-or-group-tab-1)
* [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab-1)
* [アプリケーションを更新する](#update-your-application)
* [アプリケーションをビルドして実行する](#build-and-run-your-application-1)
* [開発者ポータルを使用してアプリ パッケージを更新する](#update-your-app-package-with-developer-portal)
* [Teamsでアプリをプレビューする](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>チャネルまたはグループ タブを使用してアプリケーションを生成する

1. Visual Studio開き、**プロジェクトまたはソリューションを開く** を選択します。

1. Microsoft-Teams-Samplessamplestab-channel-grouprazor-csharp  >  >  >  フォルダーに移動し、**channelGroupTab.sln** を開きます。

1. Visual Studioで **F5** を選択するか、アプリケーションの [**デバッグ]** メニューから [**デバッグ** の開始] を選択して、アプリケーションが正しく読み込まれたかどうかを確認します。 ブラウザーで、次の URL に移動します。

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>ソース コードを確認する</b></summary>

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは、ASP.NET Core 3.1 Web アプリケーションの空のテンプレートから作成され、セットアップ時に **[Advanced * Configure for HTTPS**] チェック ボックスがオンになっています。 MVC サービスは、依存関係挿入フレームワーク `ConfigureServices()` のメソッドによって登録されます。 また、空のテンプレートでは既定では静的コンテンツの提供が有効にされないため、次のコードを使用して静的ファイル ミドルウェアがメソッドに `Configure()` 追加されます。

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

ASP.NET Coreでは、Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core **は、Index** という名前のファイルをサイトの既定またはホーム ページとして扱います。 ブラウザー URL がサイトのルートを指すと、 **Index.cshtml** がアプリケーションのホーム ページとして表示されます。

#### <a name="tabcs"></a>Tab.cs

この C# ファイルには、構成中に **Tab.cshtml** から呼び出されるメソッドが含まれています。

#### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

* 192 x 192 ピクセルの **フル カラー アイコン** 。
* 32 x 32 ピクセルの **透明なアウトライン アイコン** 。
* `manifest.json`アプリの属性を指定するファイル。

タブをTeamsにアップロードする際に使用するには、これらのファイルをアプリ パッケージに圧縮する必要があります。 ユーザーがタブの追加または更新を選択すると、マニフェストで指定した内容を読み込み`configurationUrl`、IFrame に埋め込み、タブにレンダリングMicrosoft Teams。

#### <a name="csproj"></a>.csproj

Visual Studio ソリューション エクスプローラー ウィンドウで、プロジェクトを右クリックし、[ファイルの編集] Project選択 **します**。 ファイルの最後には、アプリケーションのビルド時に zip フォルダーを作成して更新する次のコードが表示されます。

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

ngrok を実行したままコマンド プロンプトを保持し、URL を書き留めておきます。

### <a name="update-your-application"></a>アプリケーションを更新する

1. Visual Studio ソリューション エクスプローラーを開いて **PagesShared**  >  フォルダーに移動し **、_Layout.cshtml** を開き、次を次のように追加します。 <head> tags セクション:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > このページの URL は最新バージョンを表していないため、コピーして貼り付け `<script src="...">` ないでください。 SDK の最新バージョンを取得するには、常に [JavaScript API Microsoft Teams](https://www.npmjs.com/package/@microsoft/teams-js)に移動します。
    
1. タグに呼び出しを`microsoftTeams.initialize();``script`挿入します。

1. Visual Studio ソリューション エクスプローラー **Pages** フォルダーに移動し、**Tab.cshtml を** 開きます

    **Tab.cshtml** 内では、アプリケーションによって、赤または灰色のアイコンでタブを表示するための 2 つのオプション ボタンがユーザーに表示されます。 **[灰色の選択**] ボタンまたは **[赤の選択]** ボタンを選択すると、それぞれトリガー`saveGray()`または`saveRed()`設定`settings.setValidityState(true)`が行われ、構成ページの **[保存]** ボタンが有効になります。 このコードTeams、構成要件を完了し、インストールを続行できることを確認できます。 のパラメーター `settings.setSettings` が設定されます。 最後に、 `saveEvent.notifySuccess()` コンテンツ URL が正常に解決されたことを示すために呼び出されます。

1. タブへの `websiteUrl` HTTPS ngrok URL を使用して、各関数の値と `contentUrl` 値を更新します。

    これで、次のコードを ngrok URL に置き換えて **y8rCgT2b** に含める必要があります。

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

1. 更新された **Tab.cshtml を** 保存します。

### <a name="build-and-run-your-application"></a>アプリケーションをビルドして実行する

1. Visual Studioで **F5** を選択するか、[**デバッグ**] メニューの [**デバッグの開始**] を選択します。

1. ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を使用してコンテンツ ページに移動して、 **ngrok** が正常に実行され、動作していることを確認します。

    > [!TIP]
    > この記事で説明する手順を完了するには、アプリケーションをVisual Studioと ngrok の両方で実行する必要があります。 Visual Studioでアプリケーションの実行を停止して作業する必要がある場合は、**ngrok を実行し続けます**。 アプリケーションがVisual Studioで再起動されると、アプリケーションの要求をリッスンしてルーティングを再開します。 ngrok サービスを再起動する必要がある場合は、新しい URL が返され、新しい URL でアプリケーションを更新する必要があります。

<!--- TBD: This note seems to be removed from main. Commenting it for now.
> [!NOTE]
> App Studio can be used to edit your `manifest.json` file and upload the completed package to Teams. You can also manually edit the `manifest.json` file. If you do, ensure that you build the solution again to create the `tab.zip` file to upload.
--->

### <a name="update-your-app-package-with-developer-portal"></a>開発者ポータルを使用してアプリ パッケージを更新する

1. Microsoft Teamsに移動します。 [Web ベースのバージョン](https://teams.microsoft.com)を使用している場合は、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンド コードを調べることができます。

1. [**開発者ポータル**](https://dev.teams.microsoft.com/home)に移動します。

1. **アプリを** 開き、[**アプリのインポート**] を選択します。

<!--- TBD: This steps seems to be removed from main now so commenting it for now.

1. Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest. The name of your app package is `tab.zip`. It is available from the following path:
--->

1. アプリ パッケージの名前は `tab.zip`. 次のパスで使用できます。

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. 開発者ポータルで選択 `tab.zip` して開きます。

1. 既定の **アプリ ID** が作成され、[ **基本情報** ] セクションに入力されます。

1. 説明にアプリの短い説明と長い説明を追加 **します**。

1. **開発者情報** で、必要な詳細を追加し、**Web サイトに (有効な HTTPS URL である必要があります)** ngrok HTTPS URL を指定します。

1. **アプリの URL で**、プライバシー ポリシーと使用条件を`https://<yourngrokurl>/privacy`更新して`https://<yourngrokurl>/tou`保存します。

1. **アプリの機能** で、[グループアプリとチャネル アプリ] を選択します。 **[構成 URL] を**`https://<yourngrokurl>/tab`更新し、[**スコープ**] タブを選択します。

1. **[保存]** を選択します。

1. [ドメイン] セクションでは、タブのドメインに HTTPS プレフィックス `<yourngrokurl>.ngrok.io`のない ngrok URL を含める必要があります。

### <a name="preview-your-app-in-teams"></a>Teamsでアプリをプレビューする

1. [開発者ポータル] ツール バーの **[Teamsでプレビュー** を選択すると、アプリが正常にサイドロードされたことを開発者ポータルから通知されます。 アプリの **[追加]** ページがTeamsに表示されます。

1. [ **チームに追加]** を選択して、チームのタブを設定します。 タブを構成し、[ **保存**] を選択します。 これで、タブがTeamsで使用できるようになりました。

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="アップロードされた [チャネル] タブの ASPNET" border="true":::
    
    これで、Teamsでチャネルまたはグループ タブが正常に作成され、追加されました。

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a>ASP.NET CORE MVC を使用してカスタム チャネルまたはグループ タブを作成する

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. 次のコマンドを使用してサンプル リポジトリを新しいディレクトリに複製するか、 [ソース コード](https://github.com/OfficeDev/Microsoft-Teams-Samples) をダウンロードしてファイルを抽出できます。

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

チャネルまたはグループ タブを作成する手順を次に示します。

* [チャネルまたはグループ タブを使用してアプリケーションを生成する](#generate-your-application-with-a-channel-or-group-tab-2)
* [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab-2)
* [アプリケーションを更新する](#update-your-application-1)
* [アプリケーションをビルドして実行する](#build-and-run-your-application-2)
* [開発者ポータルを使用してアプリ パッケージを更新する](#update-your-app-package-with-developer-portal-1)
* [Teamsでアプリをプレビューする](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-channel-or-group-tab"></a>チャネルまたはグループ タブを使用してアプリケーションを生成する

1. Visual Studio開き、**プロジェクトまたはソリューションを開く** を選択します。

1. Microsoft-Teams-Samplessamplestab-channel-groupmvc-csharp  >  >  >  フォルダーに移動し、**ChannelGroupTabMVC.sln** を開きます。

1. Visual Studioで **F5** を選択するか、アプリケーションの [**デバッグ]** メニューから [**デバッグ** の開始] を選択して、アプリケーションが正しく読み込まれたかどうかを確認します。 ブラウザーで、次の URL に移動します。

    * https://localhost:3978/
    * https://localhost:3978/privacy
    * https://localhost:3978/tou

<details>
<summary><b>ソース コードを確認する</b></summary>

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは、セットアップ時に [**Advanced - Configure for HTTPS**] チェック ボックスがオンの ASP.NET Core 3.1 Web アプリケーション空のテンプレートから作成されました。 MVC サービスは、依存関係挿入フレームワーク `ConfigureServices()` のメソッドによって登録されます。 また、空のテンプレートでは既定では静的コンテンツの提供が有効にされないため、次のコードを使用して静的ファイル ミドルウェアがメソッドに `Configure()` 追加されます。

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

ASP.NET Coreでは、Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

#### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

* 192 x 192 ピクセルの **フル カラー アイコン** 。
* 32 x 32 ピクセルの **透明なアウトライン アイコン** 。
* `manifest.json`アプリの属性を指定するファイル。

タブをTeamsにアップロードする際に使用するには、これらのファイルをアプリ パッケージに圧縮する必要があります。

#### <a name="csproj"></a>.csproj

Visual Studio ソリューション エクスプローラー ウィンドウで、プロジェクトを右クリックし、[ファイルの編集] Project選択 **します**。 ファイルの最後には、アプリケーションのビルド時に zip フォルダーを作成して更新する次のコードが表示されます。

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

これらは、ASP.NET Core MVC のさまざまなビューです。

* ホーム: ASP.NET Coreは **、Index** という名前のファイルをサイトの既定またはホーム ページとして扱います。 ブラウザー URL がサイトのルートを指すと、 **Index.cshtml** がアプリケーションのホーム ページとして表示されます。

* 共有: 部分ビュー マークアップ **_Layout.cshtml** には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれています。 また、Teams ライブラリも参照します。

#### <a name="controllers"></a>コント ローラー

コントローラーは、プロパティを `ViewBag` 使用して、値をビューに動的に転送します。

</details>

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行して、タブへのセキュリティで保護されたトンネルを確立します。

```cmd
ngrok http 3978 --host-header=localhost
```

ngrok を実行したままコマンド プロンプトを保持し、URL を書き留めておきます。

### <a name="update-your-application"></a>アプリケーションを更新する

1. Visual Studio ソリューション エクスプローラーを開き **、****ViewsShared** >  フォルダーに移動し **、_Layout.cshtml** を開き、次を次のように追加します。 <head> tags セクション:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```
    
    > [!IMPORTANT]
    > このページの URL は最新バージョンを表していないため、コピーして貼り付け `<script src="...">` ないでください。 SDK の最新バージョンを取得するには、常に [JavaScript API Microsoft Teams](https://www.npmjs.com/package/@microsoft/teams-js)に移動します。
    
1. タグに呼び出しを`microsoftTeams.initialize();``script`挿入します。

1. Visual Studio ソリューション エクスプローラー **Tab** フォルダーに移動し、**Tab.cshtml を** 開きます

    **Tab.cshtml** 内では、アプリケーションによって、赤または灰色のアイコンでタブを表示するための 2 つのオプション ボタンがユーザーに表示されます。 **[灰色の選択**] ボタンまたは **[赤の選択]** ボタンを選択すると、それぞれトリガー`saveGray()`または`saveRed()`設定`settings.setValidityState(true)`が行われ、構成ページの **[保存]** ボタンが有効になります。 このコードTeams、構成要件を完了し、インストールを続行できることを確認できます。 のパラメーター `settings.setSettings` が設定されます。 最後に、 `saveEvent.notifySuccess()` コンテンツ URL が正常に解決されたことを示すために呼び出されます。 

1. タブへの `websiteUrl` HTTPS ngrok URL を使用して、各関数の値と `contentUrl` 値を更新します。

    これで、次のコードを ngrok URL に置き換えて **y8rCgT2b** に含める必要があります。

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

1. 更新された **Tab.cshtml** を必ず保存してください。

### <a name="build-and-run-your-application"></a>アプリケーションをビルドして実行する

1. Visual Studioで **F5** を選択するか、[**デバッグ**] メニューの [**デバッグの開始**] を選択します。

1. ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を使用してコンテンツ ページに移動して、 **ngrok** が正常に実行され、動作していることを確認します。

    > [!TIP]
    > この記事で説明する手順を完了するには、アプリケーションをVisual Studioと ngrok の両方で実行する必要があります。 Visual Studioでアプリケーションの実行を停止して作業する必要がある場合は、**ngrok を実行し続けます**。 アプリケーションがVisual Studioで再起動されると、アプリケーションの要求をリッスンしてルーティングを再開します。 ngrok サービスを再起動する必要がある場合は、新しい URL が返され、新しい URL でアプリケーションを更新する必要があります。

### <a name="update-your-app-package-with-developer-portal"></a>開発者ポータルを使用してアプリ パッケージを更新する

1. Microsoft Teamsに移動します。 [Web ベースのバージョン](https://teams.microsoft.com)を使用している場合は、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンド コードを調べることができます。

1. [**開発者ポータル**](https://dev.teams.microsoft.com/home)に移動します。

1. **アプリを** 開き、[**アプリのインポート**] を選択します。

1. アプリ パッケージの名前は **tab.zip** です。 次のパスで使用できます。

    ```bash
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. **tab.zip** 選択し、開発者ポータルで開きます。

1. 既定の **アプリ ID** が作成され、[ **基本情報** ] セクションに入力されます。

1. 説明にアプリの短い説明と長い説明を追加 **します**。

1. **開発者情報** で、必要な詳細を追加し、**Web サイトに (有効な HTTPS URL である必要があります)** ngrok HTTPS URL を指定します。

1. **アプリの URL で**、プライバシー ポリシーと使用条件を`https://<yourngrokurl>/privacy`更新して`https://<yourngrokurl>/tou`保存します。

1. **アプリの機能** で、[グループアプリとチャネル アプリ] を選択します。 **[構成 URL] を**`https://<yourngrokurl>/tab`更新し、[**スコープ**] タブを選択します。

1. **[保存]** を選択します。

1. [ドメイン] セクションでは、タブのドメインに HTTPS プレフィックス `<yourngrokurl>.ngrok.io`のない ngrok URL を含める必要があります。

### <a name="preview-your-app-in-teams"></a>Teamsでアプリをプレビューする

1. [開発者ポータル] ツール バーの **[Teamsでプレビュー** を選択すると、アプリが正常にサイドロードされたことを開発者ポータルから通知されます。 アプリの **[追加]** ページがTeamsに表示されます。

1. [ **チームに追加]** を選択して、チームのタブを設定します。 タブを構成し、[ **保存**] を選択します。 これで、タブがTeamsで使用できるようになりました。

    :::image type="content" source="~/assets/images/tab-images/channeltabaspnetuploaded.png" alt-text="アップロードされた [チャネル] タブの ASPNET MVC" border="true":::
    
    これで、Teamsでチャネルまたはグループ タブが正常に作成され、追加されました。

::: zone-end

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [コンテンツ ページを作成する](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="see-also"></a>関連項目

* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
* [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)
* [削除ページを作成する](~/tabs/how-to/create-tab-pages/removal-page.md)
