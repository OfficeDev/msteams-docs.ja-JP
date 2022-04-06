---
title: プライベート タブを作成する
author: laujan
description: Node.jsを使用してアプリ マニフェストを更新するための Yeoman Generator、ASP.NET Core、ASP.NET Core MVC を使用した個人用タブの作成に Microsoft Teams関するクイック スタート ガイド。
ms.localizationpriority: medium
ms.topic: quickstart
ms.author: lajanuar
keywords: yeoman ASP.NET MVC パッケージ appmanifest conversation domain permission store
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 91099b1acdea7b89305db9aad894c94019de4695
ms.sourcegitcommit: b2f6599e44a418b4cce92f28843b7e013fd6e86d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2022
ms.locfileid: "64686684"
---
# <a name="create-a-personal-tab"></a>プライベート タブを作成する

[個人] タブは、個人を対象としたボットと共に、個人用アプリの一部であり、1 人のユーザーを対象としています。 左側のウィンドウにピン留めして簡単にアクセスできます。 個人用タブの API を[並べ替えて](#reorder-static-personal-tabs)追加[`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps)することもできます。

個人用タブを作成するための [前提条件](~/tabs/how-to/tab-requirements.md) がすべて揃っていることを確認します。

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>Node.jsを使用して個人用タブを作成する

1. コマンド プロンプトで、Node.jsのインストール後に次のコマンドを入力して [、Yeoman](https://yeoman.io/) パッケージと [gulp-cli](https://www.npmjs.com/package/gulp-cli) パッケージをインストールします。

    ```cmd
    npm install yo gulp-cli --global
    ```

1. コマンド プロンプトで、次のコマンドMicrosoft Teams入力して、アプリ ジェネレーターをインストールします。

    ```cmd
    npm install generator-teams --global
    ```

個人用タブを作成する手順を次に示します。

1. [個人用タブを使用してアプリケーションを生成する](#generate-your-application-with-a-personal-tab)
1. [個人用タブにコンテンツ ページを追加する](#add-a-content-page-to-the-personal-tab)
1. [アプリ パッケージを作成する](#create-your-app-package)
1. [アプリケーションをビルドして実行する](#build-and-run-your-application)
1. [個人用タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab)
1. [アプリケーションをTeamsにアップロードする](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>個人用タブを使用してアプリケーションを生成する

1. コマンド プロンプトで、個人用タブの新しいディレクトリを作成します。

1. 新しいディレクトリに次のコマンドを入力して、Microsoft Teams アプリ ジェネレーターを起動します。

    ```cmd
    yo teams
    ```

1. **マニフェスト.json** ファイルを更新するためにアプリ ジェネレーター Microsoft Teams求められる一連の質問に値を入力します。

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text="Teams ジェネレーター" border="true":::

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

      方向キーを使用して、[ **個人用 (静的)]** を選択します。

    * **タブのMicrosoft Azure Active Directory (Azure AD) シングル サインオンのサポートが必要ですか?**

      タブのシングル サインオンのサポートAzure AD含 **めないように** 選択します。既定値は yes で、n と入力 **します**。

    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>個人用タブにコンテンツ ページを追加する

コンテンツ ページを作成し、個人用タブ アプリケーションの既存のファイルを更新します。

1. 次のマークアップを **使用して**、Visual Studio Codeに新しいpersonal.htmlファイルを作成します。

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

1. アプリケーション **の** **パブリック** フォルダーにpersonal.htmlを次の場所に保存します。

    ```
    ./src/public/<yourDefaultTabNameTab>/personal.html
    ```

1. Visual Studio Code内の次の場所から **manifest.json を** 開きます。

    ```
     ./src/manifest/manifest.json
    ```

1. 空 `staticTabs` の配列 (`staticTabs":[]`) に次を追加し、次の JSON オブジェクトを追加します。

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
    > path コンポーネント **yourDefaultTabNameTab** は、 **既定のタブ名** と単語 **Tab** のジェネレーターに入力した値です。
    >
    > たとえば、DefaultTabName は **MyTab**、**次に /MyTabTab/** です。

1. **contentURL** パス コンポーネント **yourDefaultTabNameTab** を実際のタブ名で更新します。

1. 更新された **manifest.json** ファイルを保存します。

1. 次のパスからVisual Studio Codeで **Tab.ts** を開き、IFrame でコンテンツ ページを提供します。

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. IFrame デコレーターの一覧に次を追加します。

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. 更新されたファイルを保存します。 タブ コードは完了です。

### <a name="create-your-app-package"></a>アプリ パッケージを作成する

Teamsでアプリケーションをビルドして実行するためのアプリ パッケージが必要です。 アプリ パッケージは、 **manifest.json** ファイルを検証し、 **./package** ディレクトリに zip フォルダーを生成する gulp タスクを使用して作成されます。 コマンド プロンプトで、次のコマンドを入力します。

```cmd
gulp manifest
```

### <a name="build-and-run-your-application"></a>アプリケーションをビルドして実行する

#### <a name="build-your-application"></a>アプリケーションをビルドする

コマンド プロンプトで次のコマンドを入力して、 **ソリューションを ./dist** フォルダーに移します。

```cmd
gulp build
```

#### <a name="run-your-application"></a>アプリケーションを実行する

1. コマンド プロンプトで次のコマンドを入力して、ローカル Web サーバーを起動します。

    ```cmd
    gulp serve
    ```

1. ブラウザーに入力 `http://localhost:3007/<yourDefaultAppNameTab>/` して、アプリケーションのホーム ページを表示します。

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="既定のタブ" border="true":::

1. [参照] `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`をクリックして、個人用タブを表示します。

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text="既定の html タブ" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

コマンド プロンプトで localhost を終了し、次のコマンドを入力して、タブへのセキュリティで保護されたトンネルを確立します。

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> タブが **ngrok** 経由でMicrosoft Teamsにアップロードされ、正常に保存されたら、トンネル セッションが終了するまでTeamsで表示できます。

### <a name="upload-your-application-to-teams"></a>アプリケーションをTeamsにアップロードする

1. Microsoft Teamsに移動し、[**アプリ**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="Teamsストア":::] を選択します。
1. [**アプリの管理**] を選択し、**カスタム アプリをアップロードします**。
1. プロジェクト ディレクトリに移動し、 **./package** フォルダーに移動し、zip フォルダーを選択して **[開く**] を選択します。

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text="個人用タブの追加" border="true":::

1. ダイアログで **[追加]** を選択します。 タブがTeamsにアップロードされます。

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text="個人用タブがアップロードされました" border="true":::

1. Teamsの左側のウィンドウで省略記号 &#x25CF;&#x25CF;&#x25CF; を選択し、アップロードしたアプリを選択して個人用タブを表示します。

   これで、Teamsに個人用タブが正常に作成され、追加されました。
  
   Teamsに個人用タブがあるため、個人用タブの API [を並べ替えて](#reorder-static-personal-tabs)追加[`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps)することもできます。

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-personal-tab-with-aspnet-core"></a>ASP.NET Coreを使用して個人用タブを作成する

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. 次のコマンドを使用してサンプル リポジトリを新しいディレクトリに複製するか、 [ソース コード](https://github.com/OfficeDev/Microsoft-Teams-Samples) をダウンロードしてファイルを抽出できます。

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

個人用タブを作成する手順を次に示します。

1. [個人用タブを使用してアプリケーションを生成する](#generate-your-application-with-a-personal-tab-1)
1. [アプリケーションを更新して実行する](#update-and-run-your-application)
1. [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab-1)
1. [開発者ポータルを使用してアプリ パッケージを更新する](#update-your-app-package-with-developer-portal)
1. [Teamsでアプリをプレビューする](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>個人用タブを使用してアプリケーションを生成する

1. Visual Studio開き、**プロジェクトまたはソリューションを開く** を選択します。

1. Microsoft-Teams-Samplessamplestab-personalrazor-csharp  >  >  >  フォルダーに移動し、**PersonalTab.sln** を開きます。

1. Visual Studioで **F5** を選択するか、アプリケーションの [**デバッグ]** メニューから [**デバッグ** の開始] を選択して、アプリケーションが正しく読み込まれたかどうかを確認します。 ブラウザーで、次の URL に移動します。

    * <http://localhost:3978/>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

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

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core **は、Index** という名前のファイルをサイトの既定またはホーム ページとして扱います。 ブラウザー URL がサイトのルートを指すと、 **Index.cshtml** がアプリケーションのホーム ページとして表示されます。

#### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

* 192 x 192 ピクセルの **フル カラー アイコン** 。
* 32 x 32 ピクセルの **透明なアウトライン アイコン** 。
* アプリの属性を指定する **manifest.json** ファイル。

タブをTeamsにアップロードする際に使用するには、これらのファイルをアプリ パッケージに圧縮する必要があります。 指定したマニフェストを`contentUrl`読み込み、<iframe\> に埋め込み、タブにレンダリングMicrosoft Teams。

#### <a name="csproj"></a>.csproj

Visual Studio ソリューション エクスプローラーで、プロジェクトを右クリックし、[**ファイルの編集] Project選択します**。 ファイルの最後には、アプリケーションのビルド時に zip フォルダーを作成して更新する次のコードが表示されます。

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

1. Visual Studio ソリューション エクスプローラー開いて **PagesShared**  >  フォルダーに移動し **、_Layout.cshtml** を開き、次をタグ セクションに`<head>`追加します。

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. Visual Studio ソリューション エクスプローラー **Pages** フォルダーから **PersonalTab.cshtml** を開き、タグを`<script>`追加`microsoftTeams.initialize()`して保存します。

1. Visual Studioで **F5** を選択するか、アプリケーションの **[デバッグ**] メニューから [デバッグの開始 **]** を選択します。

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行して、タブへのセキュリティで保護されたトンネルを確立します。

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>開発者ポータルを使用してアプリ パッケージを更新する

1. [**開発者ポータル**](https://dev.teams.microsoft.com/home)に移動します。

1. **アプリを** 開き、[**アプリのインポート**] を選択します。

1. アプリ パッケージの名前は **tab.zip** です。 次のパスで使用できます。

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. **tab.zip** 選択し、開発者ポータルで開きます。

1. 既定の **アプリ ID** が作成され、[ **基本情報** ] セクションに入力されます。

1. 説明にアプリの短い説明と長い説明を追加 **します**。

1. **開発者情報** で、必要な詳細を追加し、**Web サイトに (有効な HTTPS URL である必要があります)** ngrok HTTPS URL を指定します。

1. **アプリの URL で**、プライバシー ポリシーと使用条件を`https://<yourngrokurl>/privacy`更新して`https://<yourngrokurl>/tou`保存します。

1. **アプリの機能** で、[**個人用 appCreate** >  **your first personal app] タブを** 選択し、名前を入力して **コンテンツ URL を**`https://<yourngrokurl>/personalTab`更新します。 [Web サイト URL] フィールドを空白のままにし、ドロップダウン リストと **[追加**] から [**Context** as personalTab] を選択します。

1. [**保存**] を選択します。

1. [ドメイン] セクションでは、タブのドメインに HTTPS プレフィックス `<yourngrokurl>.ngrok.io`のない ngrok URL を含める必要があります。

### <a name="preview-your-app-in-teams"></a>Teamsでアプリをプレビューする

1. [開発者ポータル] ツール バーの **[Teamsでプレビュー** を選択すると、アプリが正常にサイドロードされたことを開発者ポータルから通知されます。 アプリの **[追加]** ページがTeamsに表示されます。

1. [**追加]** を選択して、Teamsでタブを読み込みます。 これで、タブがTeamsで使用できるようになりました。

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text="既定のタブ" border="true":::

   これで、Teamsに個人用タブが正常に作成され、追加されました。
  
   Teamsに個人用タブがあるため、個人用タブの API [を並べ替えて](#reorder-static-personal-tabs)追加[`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps)することもできます。

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-personal-tab-with-aspnet-core-mvc"></a>ASP.NET Core MVC を使用して個人用タブを作成する

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. 次のコマンドを使用してサンプル リポジトリを新しいディレクトリに複製するか、 [ソース コード](https://github.com/OfficeDev/Microsoft-Teams-Samples) をダウンロードしてファイルを抽出できます。

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

個人用タブを作成する手順を次に示します。

1. [個人用タブを使用してアプリケーションを生成する](#generate-your-application-with-a-personal-tab-2)
1. [アプリケーションを更新して実行する](#update-and-run-your-application-1)
1. [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab-2)
1. [開発者ポータルを使用してアプリ パッケージを更新する](#update-your-app-package-with-developer-portal-1)
1. [Teamsでアプリをプレビューする](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>個人用タブを使用してアプリケーションを生成する

1. Visual Studio開き、**プロジェクトまたはソリューションを開く** を選択します。

1. Microsoft-Teams-Samplessamplestab-personalmvc-csharp  >  >  >  フォルダーに移動し、Visual Studioで **PersonalTabMVC.sln** を開きます。

1. Visual Studioで **F5** を選択するか、アプリケーションの [**デバッグ]** メニューから [**デバッグ** の開始] を選択して、アプリケーションが正しく読み込まれたかどうかを確認します。 ブラウザーで、次の URL に移動します。

    * <http://localhost:3978>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>ソース コードを確認する</b></summary>

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは、セットアップ時に [**Advanced - Configure for HTTPS**] チェック ボックスがオンの ASP.NET Core 3.1 Web アプリケーション空のテンプレートから作成されました。 MVC サービスは、依存関係挿入フレームワーク `ConfigureServices()` のメソッドによって登録されます。 また、空のテンプレートでは既定では静的コンテンツの提供が有効にされないため、次のコードを使用して静的ファイル ミドルウェアがメソッドに `Configure()` 追加されます。

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

ASP.NET Coreでは、Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

#### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

* 192 x 192 ピクセルの **フル カラー アイコン** 。
* 32 x 32 ピクセルの **透明なアウトライン アイコン** 。
* アプリの属性を指定する **manifest.json** ファイル。

タブをTeamsにアップロードする際に使用するには、これらのファイルをアプリ パッケージに圧縮する必要があります。 指定したマニフェストを`contentUrl`読み込み、IFrame に埋め込み、タブにレンダリングMicrosoft Teams。

#### <a name="csproj"></a>.csproj

Visual Studio ソリューション エクスプローラーで、プロジェクトを右クリックし、[ファイルの編集] Project選択 **します**。 ファイルの最後には、アプリケーションのビルド時に zip フォルダーを作成して更新する次のコードが表示されます。

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

**PersonalTab.cs** は、ユーザーが **PersonalTab** ビューでボタンを選択したときに **PersonalTabController** から呼び出されるメッセージ オブジェクトとメソッドを表示します。

#### <a name="views"></a>ビュー

これらのビューは、ASP.NET Core MVC のさまざまなビューです。

* ホーム: ASP.NET Coreは **、Index** という名前のファイルをサイトの既定またはホーム ページとして扱います。 ブラウザー URL がサイトのルートを指すと、 **Index.cshtml** がアプリケーションのホーム ページとして表示されます。

* 共有: 部分ビュー マークアップ **_Layout.cshtml** には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれています。 また、Teams ライブラリも参照します。

#### <a name="controllers"></a>コント ローラー

コントローラーは、プロパティを `ViewBag` 使用して、値を Views に動的に転送します。

</details>

### <a name="update-and-run-your-application"></a>アプリケーションを更新して実行する

1. Visual Studio ソリューション エクスプローラー開いて **ViewsShared**  >  フォルダーに移動し **、_Layout.cshtml** を開き、次をタグ セクションに`<head>`追加します。

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

1. Visual Studio ソリューション エクスプローラー **ViewsPersonalTab**  >  フォルダーから **PersonalTab.cshtml** を開き、タグ内に`<script>`追加`microsoftTeams.initialize()`して保存します。

1. Visual Studioで **F5** を選択するか、アプリケーションの **[デバッグ**] メニューから [デバッグの開始 **]** を選択します。

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行して、タブへのセキュリティで保護されたトンネルを確立します。

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>開発者ポータルを使用してアプリ パッケージを更新する

1. [**開発者ポータル**](https://dev.teams.microsoft.com/home)に移動します。

1. **アプリを** 開き、[**アプリのインポート**] を選択します。

1. アプリ パッケージの名前は **tab.zip** です。 次のパスで使用できます。

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. **tab.zip** 選択し、開発者ポータルで開きます。

1. 既定の **アプリ ID** が作成され、[ **基本情報** ] セクションに入力されます。

1. 説明にアプリの短い説明と長い説明を追加 **します**。

1. **開発者情報** で、必要な詳細を追加し、**Web サイトに (有効な HTTPS URL である必要があります)** ngrok HTTPS URL を指定します。

1. **アプリの URL で**、プライバシー ポリシーと使用条件を`https://<yourngrokurl>/privacy`更新して`https://<yourngrokurl>/tou`保存します。

1. **アプリの機能** で、[**個人用 appCreate** >  **your first personal app] タブを** 選択し、名前を入力して **コンテンツ URL を**`https://<yourngrokurl>/personalTab`更新します。 [Web サイト URL] フィールドを空白のままにし、ドロップダウン リストと **[追加**] から [**Context** as personalTab] を選択します。

1. [**保存**] を選択します。

1. [ドメイン] セクションでは、タブのドメインに HTTPS プレフィックス `<yourngrokurl>.ngrok.io`のない ngrok URL を含める必要があります。

### <a name="preview-your-app-in-teams"></a>Teamsでアプリをプレビューする

1. [開発者ポータル] ツール バーの **[Teamsでプレビュー** を選択すると、アプリが正常にサイドロードされたことを開発者ポータルから通知されます。 アプリの **[追加]** ページがTeamsに表示されます。

1. [**追加]** を選択して、Teamsのタブを読み込みます。 これで、タブがTeamsで使用できるようになりました。

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="個人タブ" border="true":::
  
   これで、Teamsに個人用タブが正常に作成され、追加されました。

   Teamsに個人用タブがあるため、個人用タブの API [を並べ替えて](#reorder-static-personal-tabs)追加[`registerOnFocused`](#add-registeronfocused-api-for-tabs-or-personal-apps)することもできます。

::: zone-end

## <a name="reorder-static-personal-tabs"></a>静的個人用タブの順序を変更する

マニフェスト バージョン 1.7 以降、開発者は個人用アプリ内のすべてのタブを再配置できます。 特に、開発者は **ボット チャット** タブを移動できます。このタブは、常に既定で最初の位置 (個人用アプリ タブ ヘッダー内の任意の場所) に移動できます。 2 つの予約済みタブ `entityId` キーワードが宣言され、**会話と****会話が行われます**。

**個人用** スコープを使用してボットを作成すると、既定では個人用アプリの最初のタブ位置に表示されます。 別の位置に移動する場合は、予約済みのキーワードである会話を使用して静的タブ オブジェクトをマニフェストに追加 **する** 必要があります。 **会話** タブは、配列内の **会話** タブを追加する場所に応じて、Web またはデスクトップに`staticTabs`表示されます。

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

## <a name="add-registeronfocused-api-for-tabs-or-personal-apps"></a>タブまたは個人用アプリ用の API を追加 `registerOnFocused` する

`registerOnFocused` SDK API を使用すると、Teamsでキーボードを使用できます。 Ctrl キー、Shift キー、F6 キーを使用して、個人用アプリに戻り、タブまたは個人用アプリにフォーカスを維持できます。 たとえば、個人用アプリから離れて何かを検索し、個人用アプリに戻ったり、Ctrl + F6 キーを押して必要な場所を移動したりできます。

次のコードは、フォーカスをタブまたは個人用アプリに `registerFocusEnterHandler` 返す必要がある場合の SDK のハンドラー定義の例を示しています。

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

ハンドラーがキーワード `focusEnter`を使用してトリガーされると、ハンドラー `registerFocusEnterHandler` は 、.. という名前のパラメーターを受け取るコールバック関数 `focusEnterHandler` を使用して呼び `navigateForward`出されます。 `navigateForward`値によって、イベントの種類が決まります。 これは `focusEnterHandler` Ctrl + F6 によってのみ呼び出され、タブ キーでは呼び出されません。
Teams内の移動イベントに役立つキーは次のとおりです。

* 転送イベント: Ctrl + F6 キー
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

:::image type="content" source="../../assets/images/personal-apps/registerfocus.png" alt-text="registerOnFocussed API を追加するためのオプションを示す例" border="true":::

#### <a name="personal-app-forward-event"></a>個人用アプリ: 転送イベント

:::image type="content" source="../../assets/images/personal-apps/registerfocus-forward-event.png" alt-text="registerOnFocussed API の前方移動を追加するためのオプションを示す例" border="true":::

#### <a name="personal-app-backward-event"></a>個人用アプリ: バックワード イベント

:::image type="content" source="../../assets/images/personal-apps/registerfocus-backward-event.png" alt-text="例は、registerOnFocussed API の後方移動を追加するためのオプションを示しています" border="true":::

### <a name="tab"></a>Tab

:::image type="content" source="../../assets/images/personal-apps/registerfocus-tab.png" alt-text="例は、タブに registerOnFocussed API を追加するためのオプションを示しています" border="true":::

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [[チャネルまたはグループの作成] タブ](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>関連項目

* [Teams タブ](~/tabs/what-are-tabs.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
* [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)
* [会話タブを作成する](~/tabs/how-to/conversational-tabs.md)
* [個人用アプリまたはタブからTeamsに共有する](~/concepts/build-and-test/share-to-teams-from-personal-app-or-tab.md)
