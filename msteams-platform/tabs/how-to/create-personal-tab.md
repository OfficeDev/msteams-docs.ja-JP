---
title: プライベート タブを作成する
author: laujan
description: Node.js を使用して Yeoman Generator、ASP.NET Core、または ASP.NET Core MVC を使用して個人用タブを作成し、Node.js を使用して Microsoft Teams を更新するクイック スタート ガイド。
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
keywords: yeoman ASP.NET MVC パッケージ appmanifest 会話ドメインのアクセス許可ストア
zone_pivot_groups: teams-app-environment
---

# <a name="create-a-personal-tab"></a>プライベート タブを作成する

[個人] タブは、個人を対象としたボットと共に、個人用アプリの一部であり、1 人のユーザーを対象としています。 左ウィンドウにピン留めして、簡単にアクセスできます。 個人用タブの [API の順序](#reorder-static-personal-tabs)を[変更`registerOnFocused`して](#add-registeronfocused-api-for-tabs-or-personal-apps)追加することもできます。

個人用タブを作成するために [、すべてのプリrequsites](~/tabs/how-to/tab-requirements.md) が必要です。

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>ユーザー設定で個人用タブを作成Node.js

1. コマンド プロンプトで、次のコマンドを入力して [Yeoman](https://yeoman.io/) パッケージと [gulp-cli](https://www.npmjs.com/package/gulp-cli) パッケージをインストールし、次のコマンドをインストールNode.js。

    ```cmd
    npm install yo gulp-cli --global
    ```

1. コマンド プロンプトで、次のコマンドMicrosoft Teamsしてアプリ ジェネレーターをインストールします。

    ```cmd
    npm install generator-teams --global
    ```

個人用タブを作成する手順は次のとおりです。

1. [個人用タブを使用してアプリケーションを生成する](#generate-your-application-with-a-personal-tab)
1. [個人用タブにコンテンツ ページを追加する](#add-a-content-page-to-the-personal-tab)
1. [アプリ パッケージを作成する](#create-your-app-package)
1. [アプリケーションのビルドと実行](#build-and-run-your-application)
1. [個人用タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab)
1. [アップロードにアプリケーションをTeams](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>個人用タブを使用してアプリケーションを生成する

1. コマンド プロンプトで、個人用タブ用の新しいディレクトリを作成します。

1. 新しいディレクトリに次のコマンドを入力して、アプリ ジェネレーター Microsoft Teams開始します。

    ```cmd
    yo teams
    ```

1. manifest.json ファイルを更新するようにアプリ ジェネレーターから求Microsoft Teams一連の質問に値 **を入力** します。

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text="Teamsジェネレーター" border="true":::

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

      矢印キーを使用して [個人用 **(静的) ] を選択します**。

    * **タブに対Microsoft Azure Active Directory (Azure AD) シングル サインオンのサポートが必要ですか?**

      [**シングル** サインオンのサポートAzure AD含めない] を選択します。既定値ははい、n と **入力します**。

    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>個人用タブにコンテンツ ページを追加する

コンテンツ ページを作成し、個人用タブ アプリケーションの既存のファイルを更新します。

1. 次のマークアップを **使用personal.html** 新しいVisual Studio Codeファイルを作成します。

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

1. アプリケーション **personal.html** のパブリック フォルダーに次 **の** 場所に保存します。

    ```
    ./src/public/<yourDefaultTabNameTab>/personal.html
    ```

1. マニフェスト **.json を、** 次の場所から開Visual Studio Code。

    ```
     ./src/manifest/manifest.json
    ```

1. 空の配列 () に次の `staticTabs` 値を追加`staticTabs":[]`し、次の JSON オブジェクトを追加します。

    ```json
    {
        "entityId": "personalTab",
        "name": "Personal Tab ",
        "contentUrl": "https://{{PUBLIC_HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
        "websiteUrl": "https://{{PUBLIC_HOSTNAME}}",
        "scopes": ["personal"]
    }
    ```

    > [!IMPORTANT]
    > パス コンポーネント **yourDefaultTabNameTab** は、[既定] タブ名のジェネレーターに入力した値に Tab という単語を加 **えた値です**。
    >
    > たとえば、DefaultTabName は **MyTab** で、 **次に /MyTabTab/**

1. **contentURL パス コンポーネント** **yourDefaultTabNameTab を** 実際のタブ名で更新します。

1. 更新された **manifest.json ファイルを保存** します。

1. IFrame でコンテンツ ページを提供Visual Studio Codeパスからタブ.**ts** を開きます。

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. IFrame デコレータの一覧に次の項目を追加します。

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. 更新されたファイルを保存します。 タブ コードが完成しました。

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

    ```cmd
    gulp serve
    ```

1. ブラウザー `http://localhost:3007/<yourDefaultAppNameTab>/` に入力して、アプリケーションのホーム ページを表示します。

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="[既定] タブ" border="true":::

1. [参照 `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`] をクリックして、個人用タブを表示します。

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text="既定の html タブ" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

コマンド プロンプトで localhost を終了し、次のコマンドを入力して、タブへのセキュリティで保護されたトンネルを確立します。

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> **タブが ngrok** をMicrosoft Teamsして正常に保存された後、トンネル セッションが終了するまで、Teamsで表示できます。

### <a name="upload-your-application-to-teams"></a>アップロードにアプリケーションをTeams

1. [ストア] にMicrosoft Teamsし、[**ストア**&nbsp;] :::image type="content" source="~/assets/images/tab-images/store.png" alt-text="をTeamsします":::。
1. [アプリ **の管理] を選択します。**
1. [**アプリの発行] を** 選択 **しアップロードアプリを作成します**。

    :::image type="content" source="~/assets/images/tab-images/publish-app.png" alt-text="アップロードカスタム アプリ" border="true":::

1. プロジェクト ディレクトリに移動し、 **./package** フォルダーを参照し、zip フォルダーを選択して、[開く] を選択 **します**。

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text="個人用タブの追加" border="true":::

1. ダイアログで **[追加** ] を選択します。 タブがアップロードされ、Teams。

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text="アップロードされた個人用タブ" border="true":::

1. アプリの左側のウィンドウでTeams省略記号を選択 &#x25CF;&#x25CF;&#x25CF; 、アップロードしたアプリを選択して個人用タブを表示します。

   これで、自分の個人用タブを完全に作成し、追加Teams。
  
   [個人用] タブが表示Teams、[](#reorder-static-personal-tabs)[`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps)個人タブの API の順序を変更して追加することもできます。

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-personal-tab-with-aspnet-core"></a>ユーザー設定で個人用タブを作成 ASP.NET Core

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. 次のコマンドを使用して、サンプル リポジトリを新しいディレクトリに複製するか、ソース コードをダウンロード [してファイルを](https://github.com/OfficeDev/Microsoft-Teams-Samples) 抽出できます。

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

個人用タブを作成する手順は次のとおりです。

1. [個人用タブを使用してアプリケーションを生成する](#generate-your-application-with-a-personal-tab-1)
1. [アプリケーションを更新して実行する](#update-and-run-your-application)
1. [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab-1)
1. [開発者ポータルでアプリ パッケージを更新する](#update-your-app-package-with-developer-portal)
1. [アプリをプレビュー Teams](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>個人用タブを使用してアプリケーションを生成する

1. [プロジェクトVisual Studio開き、[**プロジェクトまたはソリューションを開く] を選択します**。

1. Microsoft-Teams-Samplessamplestab-personalrazor-csharp >  >  >  フォルダーに移動し、**PersonalTab.sln を開きます**。

1. [Visual Studio **F5**] を選択するか、アプリケーションの  [デバッグ] メニューから [デバッグの開始] を選択して、アプリケーションが正しく読み込まれているか確認します。 ブラウザーで、次の URL に移動します。

    * <http://localhost:3978/>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>ソース コードを確認する</b></summary>

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは、3.1 web アプリケーション ASP.NET Coreテンプレートから作成され、セットアップ時に [Advanced **- Configure for HTTPS**] チェック ボックスがオンになっています。 MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。 さらに、空のテンプレート `Configure()` では既定では静的コンテンツの配信が有効ではないので、静的ファイル ミドルウェアは次のコードを使用してメソッドに追加されます。

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

#### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

* 192 x 192 ピクセルのフル カラー アイコン。
* 32 x 32 ピクセルの透明なアウトライン アイコン。
* アプリ **の属性を指定する manifest.json** ファイル。

これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。 Microsoft Teams指定した`contentUrl`マニフェストを読み込み、それを iframe\> <に埋め込み、それをタブにレンダリングします。

#### <a name="csproj"></a>.csproj

[Visual Studio ソリューション エクスプローラー] で、プロジェクトを右クリックし、[ファイルの編集 **] Projectします**。 ファイルの最後に、アプリケーションのビルド時に zip フォルダーを作成および更新する次のコードを確認できます。

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

### <a name="update-and-run-your-application"></a>アプリケーションを更新して実行する

1. [Visual Studio ソリューション エクスプローラー開き、**PagesShared**  >  フォルダーに移動し、**_Layout.cshtml** を開き、[タグ] セクションに次の項目を`<head>`追加します。

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. このVisual Studio ソリューション エクスプローラー **Pages フォルダーから PersonalTab.cshtml** を **開** き、タグ`microsoftTeams.initialize()`を追加して`<script>`保存します。

1. [Visual Studio **F5] を選択するか****、アプリケーションの** [デバッグ] メニューから [デバッグの開始] **を選択** します。

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行して、タブへのセキュリティで保護されたトンネルを確立します。

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>開発者ポータルでアプリ パッケージを更新する

1. [開発者ポータル [**] に移動します**](https://dev.teams.microsoft.com/home)。

1. [アプリ **] を開** き、[アプリの **インポート] を選択します**。

1. アプリ パッケージの名前は次 **tab.zip**。 これは、次のパスで使用できます。

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. [ **tab.zip** を選択し、開発者ポータルで開きます。

1. 既定の **アプリ ID が** 作成され、[基本情報] **セクションに設定** されます。

1. [説明] にアプリの短い説明と長い説明 **を追加します**。

1. [ **開発者情報]** で、必要な詳細を追加し、[Web サイト] (有効な **HTTPS URL** である必要があります) で ngrok HTTPS URL を指定します。

1. アプリ **の URL で、** プライバシー ポリシーを更新し `https://<yourngrokurl>/privacy` 、使用条件を更新して `https://<yourngrokurl>/tou` 保存します。

1. [ **アプリの機能]** で、[ **個人用アプリ** > **を** 作成する] タブを選択し、[名前] を入力してコンテンツ **URL を更新** します `https://<yourngrokurl>/personalTab`。 [Web サイトの URL] フィールドを空白のままにし **、ドロップダウン リスト** から [Context as personalTab] を選択し、[追加] を **選択します**。

1. [**保存**] を選択します。

1. [ドメイン] セクションでは、タブのドメインに HTTPS プレフィックスのない ngrok URL が含まれている必要があります `<yourngrokurl>.ngrok.io`。

### <a name="preview-your-app-in-teams"></a>アプリをプレビュー Teams

1. [**開発者ポータル] Teams** [プレビュー] を選択すると、アプリが正常にサイドロードされたことを開発者ポータルから通知されます。 アプリ **の [** 追加] ページが [アプリ] Teams。

1. [追加 **] を** 選択してタブを読み込Teams。 タブは、このタブでTeams。

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text="[既定] タブ" border="true":::

   これで、自分の個人用タブを完全に作成し、追加Teams。
  
   [個人用] タブが表示Teams、[](#reorder-static-personal-tabs)[`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps)個人タブの API の順序を変更して追加することもできます。

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-personal-tab-with-aspnet-core-mvc"></a>MVC を使用して個人用タブ ASP.NET Coreする

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. 次のコマンドを使用して、サンプル リポジトリを新しいディレクトリに複製するか、ソース コードをダウンロード [してファイルを](https://github.com/OfficeDev/Microsoft-Teams-Samples) 抽出できます。

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

個人用タブを作成する手順は次のとおりです。

1. [個人用タブを使用してアプリケーションを生成する](#generate-your-application-with-a-personal-tab-2)
1. [アプリケーションの更新と実行](#update-and-run-your-application-1)
1. [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab-2)
1. [開発者ポータルでアプリ パッケージを更新する](#update-your-app-package-with-developer-portal-1)
1. [アプリをプレビュー Teams](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>個人用タブを使用してアプリケーションを生成する

1. [プロジェクトVisual Studio開き、[**プロジェクトまたはソリューションを開く] を選択します**。

1. **Microsoft-Teams-Samplessamplestab-personalmvc-csharp** >  >  >  フォルダーに移動し、このフォルダーで **PersonalTabMVC.sln** を開Visual Studio。

1. [Visual Studio **F5**] を選択するか、アプリケーションの  [デバッグ] メニューから [デバッグの開始] を選択して、アプリケーションが正しく読み込まれているか確認します。 ブラウザーで、次の URL に移動します。

    * <http://localhost:3978>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>ソース コードを確認する</b></summary>

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは、3.1 web アプリケーション ASP.NET Coreテンプレートから作成され、セットアップ時に [Advanced **- Configure for HTTPS**] チェック ボックスがオンになっています。 MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。 さらに、空のテンプレート `Configure()` では既定では静的コンテンツの配信が有効ではないので、静的ファイル ミドルウェアは次のコードを使用してメソッドに追加されます。

``` csharp
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

これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。 Microsoft Teams指定した`contentUrl`マニフェストを読み込み、IFrame に埋め込み、それをタブにレンダリングします。

#### <a name="csproj"></a>.csproj

[ファイル] Visual Studio ソリューション エクスプローラープロジェクトを右クリックし、[ファイルの編集] Project **します**。 ファイルの最後に、アプリケーションのビルド時に zip フォルダーを作成および更新する次のコードが表示されます。

``` xml
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

**PersonalTab.cs** は、ユーザーが PersonalTab ビューでボタンを選択すると **、PersonalTabController** から呼び出されるメッセージ オブジェクトとメソッド **を表示** します。

#### <a name="views"></a>ビュー

これらのビューは、MVC の異なる ASP.NET Coreです。

* ホーム: ASP.NET Core Index と呼ばれるファイルをサイトの既定またはホーム ページとして扱います。 ブラウザーの URL がサイトのルートをポイントすると、 **Index.cshtml** がアプリケーションのホーム ページとして表示されます。

* 共有: 部分ビュー マークアップ **_Layout.cshtml** には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれます。 また、ライブラリのTeamsします。

#### <a name="controllers"></a>コントローラー

コントローラーはプロパティを使用して `ViewBag` 、値を Views に動的に転送します。

</details>

### <a name="update-and-run-your-application"></a>アプリケーションを更新して実行する

1. [Visual Studio ソリューション エクスプローラーを開き、**ViewsShared**  >  フォルダーに移動し、**_Layout.cshtml** を開き、次の項目を [タグ] セクションに`<head>`追加します。

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. このVisual Studio ソリューション エクスプローラー **ViewsPersonalTab** フォルダーから **PersonalTab.cshtml**  >  を開き、タグ`microsoftTeams.initialize()`内に追加して`<script>`保存します。

1. [Visual Studio **F5] を選択するか****、アプリケーションの** [デバッグ] メニューから [デバッグの開始] **を選択** します。

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行して、タブへのセキュリティで保護されたトンネルを確立します。

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>開発者ポータルでアプリ パッケージを更新する

1. [開発者ポータル [**] に移動します**](https://dev.teams.microsoft.com/home)。

1. [アプリ **] を開** き、[アプリの **インポート] を選択します**。

1. アプリ パッケージの名前は次 **tab.zip**。 これは、次のパスで使用できます。

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. [ **tab.zip** を選択し、開発者ポータルで開きます。

1. 既定の **アプリ ID が** 作成され、[基本情報] **セクションに設定** されます。

1. [説明] にアプリの短い説明と長い説明 **を追加します**。

1. [ **開発者情報]** で、必要な詳細を追加し、[Web サイト] (有効な **HTTPS URL** である必要があります) で ngrok HTTPS URL を指定します。

1. アプリ **の URL で、** プライバシー ポリシーを更新し `https://<yourngrokurl>/privacy` 、使用条件を更新して `https://<yourngrokurl>/tou` 保存します。

1. [ **アプリの機能]** で、[ **個人用アプリ** > **を** 作成する] タブを選択し、[名前] を入力してコンテンツ **URL を更新** します `https://<yourngrokurl>/personalTab`。 [Web サイトの URL] フィールドを空白のままにし **、ドロップダウン リスト** から [Context as personalTab] を選択し、[追加] を **選択します**。

1. [**保存**] を選択します。

1. [ドメイン] セクションで、タブのドメインには、HTTPS プレフィックスのない ngrok URL が含まれている必要があります `<yourngrokurl>.ngrok.io`。

### <a name="preview-your-app-in-teams"></a>アプリをプレビュー Teams

1. [**開発者ポータル] Teams** [プレビュー] を選択すると、アプリが正常にサイドロードされたことを開発者ポータルから通知されます。 アプリ **の [** 追加] ページが [アプリ] Teams。

1. [追加 **] を** 選択して、タブを [Teams] に読み込Teams。 タブは、このタブでTeams。

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="個人タブ" border="true":::
  
   これで、自分の個人用タブを完全に作成し、追加Teams。

   [個人用] タブが表示Teams、[](#reorder-static-personal-tabs)[`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps)個人タブの API の順序を変更して追加することもできます。

::: zone-end

## <a name="reorder-static-personal-tabs"></a>静的な個人用タブの並べ替え

マニフェスト バージョン 1.7 から、開発者は個人用アプリ内のすべてのタブを再配置できます。 特に、開発者はボット チャット タブを移動できます。これは常に既定で最初の位置に、個人用アプリのタブ ヘッダー内の任意の場所に移動できます。 2 つの予約済 `entityId` みタブ キーワードが宣言され、 **会話が** 行 **えます**。

個人用スコープを持つ **ボットを作成** すると、既定では個人用アプリの最初のタブ位置に表示されます。 別の位置に移動する場合は、予約キーワードである会話を使用して静的タブ オブジェクトをマニフェストに追加する必要 **があります**。 [ **会話** ] タブは、配列に会話タブを追加する場所に応 **じて、Web** またはデスクトップに表示 `staticTabs` されます。

``` JSON

{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}

```

## <a name="add-registeronfocused-api-for-tabs-or-personal-apps"></a>タブまたは `registerOnFocused` 個人用アプリの API を追加する

SDK `registerOnFocused` API を使用すると、ユーザーがキーボードを使用Teams。 Ctrl キー、Shift キー、F6 キーを使用して、個人用アプリに戻り、タブまたは個人用アプリにフォーカスを維持できます。 たとえば、個人用アプリから移動して何かを検索し、個人用アプリに戻すか、Ctrl + F6 を使用して必要な場所を移動できます。

次のコードは、フォーカスをタブ `registerFocusEnterHandler` または個人用アプリに返す必要がある場合の SDK のハンドラー定義の例を示しています。

``` C#

export function registerFocusEnterHandler(handler: (navigateForward: boolean) => void): 
void {
  HandlersPrivate.focusEnterHandler = handler;
  handler && sendMessageToParent('registerHandler', ['focusEnter']);
}
function handleFocusEnter(navigateForward: boolean): void
 {
  if (HandlersPrivate.focusEnterHandler)
   {
    HandlersPrivate.focusEnterHandler(navigateForward);
  }
}

```

ハンドラーがキーワードでトリガーされると`focusEnter``registerFocusEnterHandler``focusEnterHandler`、ハンドラーはというパラメーターを受け取るコールバック関数で呼び出されます。`navigateForward` 値は、 `navigateForward` イベントの種類を決定します。 これは `focusEnterHandler` Ctrl + F6 によってのみ呼び出され、タブ キーでは呼び出されません。
次に示すキーは、Teams内の移動イベントに役立ちます。

* Forward イベント: Ctrl + F6 キー
* 後方イベント: Ctrl + Shift + F6 キー

``` C#

case 'focusEnter':     
this.registerFocusEnterHandler((navigateForward: boolean = true) => {
this.sdkWindowMessageHandler.sendRequestMessage(this.frame, this.constants.SdkMessageTypes.focusEnter, [navigateForward]);
// Set focus on iframe or webview
if (this.frame && this.frame.sourceElem) {
  this.frame.sourceElem.focus();
}
return true;
});
}

// callback function to be passed to the handler
private focusEnterHandler: (navigateForward: boolean) => boolean;

// function that gets invoked after handler is registered.
private registerFocusEnterHandler(focusEnterHandler: (navigateForward: boolean) => boolean): void {
this.focusEnterHandler = focusEnterHandler;
this.layoutService.registerAppFocusEnterCallback(this.focusEnterHandler);
}

```

### <a name="personal-app"></a>個人用アプリ

:::image type="content" source="../../assets/images/personal-apps/registerfocus.png" alt-text="例は、registerOnFocussed API を追加するためのオプションを示しています" border="true":::

#### <a name="personal-app-forward-event"></a>個人用アプリ: 転送イベント

:::image type="content" source="../../assets/images/personal-apps/registerfocus-forward-event.png" alt-text="例は、registerOnFocussed API の前方移動を追加するためのオプションを示しています" border="true":::

#### <a name="personal-app-backward-event"></a>個人用アプリ: 下位イベント

:::image type="content" source="../../assets/images/personal-apps/registerfocus-backward-event.png" alt-text="例では、registerOnFocussed API の後方移動を追加するためのオプションを示しています" border="true":::

### <a name="tab"></a>Tab

:::image type="content" source="../../assets/images/personal-apps/registerfocus-tab.png" alt-text="例は、tab に registerOnFocussed API を追加するためのオプションを示しています" border="true":::

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
* [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)
* [会話タブを作成する](~/tabs/how-to/conversational-tabs.md)
