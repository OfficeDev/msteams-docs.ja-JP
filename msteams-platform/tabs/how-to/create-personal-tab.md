---
title: プライベート タブを作成する
author: laujan
description: Yeoman Generator を使用して個人用タブを作成するクイック スタート Microsoft Teams。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 47ed3027f936366964871733e78c7a43851ffb99
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179870"
---
# <a name="create-a-personal-tab"></a>プライベート タブを作成する

## <a name="create-a-custom-personal-tab"></a>ユーザー設定の個人用タブを作成する

[個人用] タブは、MVC Node.js Yeoman Generator、ASP.NET Core、または ASP.NET Coreできます。

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

### <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator"></a>ユーザー設定と Yeoman Generator を使用Node.js個人用タブを作成する

> [!NOTE]
> この記事では、Microsoft OfficeDev Microsoft Teamsリポジトリにある最初のアプリ[Wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)のビルドにGitHubします。

Yeoman ジェネレーターを使用してカスタム[個人用Teams作成できます](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。 アプリケーションは、アプリケーションにもアップロードTeams。

### <a name="prerequisites-for-teams-apps"></a>アプリのTeams前提条件

次の前提条件について理解している必要があります。

- カスタム アプリのアップロードを許可Office 365を有効にしたテナントとチーム **が構成されている必要** があります。 詳細については、「prepare [your Office 365 テナント」を参照してください](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

    > [!NOTE]
    > ユーザーアカウントをお持ちOffice 365場合は、開発者プログラムから無料サブスクリプションOffice 365できます。 サブスクリプションは、継続的な開発に使用している限りアクティブなままです。 「[開発者プログラムへようこそOffice 365」を参照してください](/office/developer-program/microsoft-365-developer-program)。

さらに、このプロジェクトでは、次のコードが開発環境にインストールされている必要があります。

- 任意のテキスト エディターまたは IDE。 無料でインストール[して使用Visual Studio Code](https://code.visualstudio.com/download)できます。

- [Node.js/npm](https://nodejs.org/en/). 最新の LTS バージョンを使用します。 ノード ノード パッケージ マネージャー (npm) がシステムにインストールされ、システムにインストールNode.js。

- インストールが正常に完了したらNode.jsに次のコマンド プロンプトを入力して [、Yeoman](https://yeoman.io/) パッケージと [gulp-cli](https://www.npmjs.com/package/gulp-cli) パッケージをインストールします。

    ```bash
    npm install yo gulp-cli --global
    ```

- コマンド プロンプトにMicrosoft Teamsを入力して、アプリ ジェネレーターをインストールします。

    ```bash
    npm install generator-teams --global
    ```

### <a name="generate-your-project"></a>プロジェクトを生成する

**プロジェクトを生成するには**

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. ジェネレーターを起動するには、新しいディレクトリに移動し、次のコマンドを入力します。

    ```bash
    yo teams
    ```

1. 次に、アプリケーションのファイルファイルで使用される一連の値manifest.js **指定** します。

    ![ジェネレーターの開くスクリーンショット](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    **ソリューション名は何ですか?**

    これはプロジェクト名です。 Enter キーを選択すると、候補の名前を **受け入** れできます。

    **ファイルをどこに保存しますか?**

    現在、プロジェクト ディレクトリにいます。 **[Enter] を選択します**。

    **アプリ プロジェクトMicrosoft Teamsタイトル**

    これはアプリ パッケージ名であり、アプリ マニフェストと説明で使用されます。 タイトルを入力するか、Enter **を選択して** 既定の名前を受け入れる。

    **(会社) の名前(最大 32 文字)**

    会社名はアプリ マニフェストで使用されます。 会社名を入力するか **、Enter を選択して** 既定の名前を受け入れる。

    **どのマニフェスト バージョンを使用しますか?**

    既定のスキーマを選択します。

    **クイック スキャフォールディング(Y/n)**

    既定値は yes です。 **n と入力** して Microsoft パートナー ID を入力します。

    **Microsoft パートナー ID をお持ちの場合は、Microsoft パートナー ID を入力してください。(スキップする場合は空白のままにする)**

    このフィールドは必須ではなく、Microsoft パートナー ネットワークに既に参加している場合にのみ [使用する必要があります](https://partner.microsoft.com)。

    **プロジェクトに何を追加しますか?**

    [ **選択] &ast; ( ) [タブ] をクリックします**。

    **このソリューションをホストする URL**

    既定では、ジェネレーターは Azure Web サイトの URL を提案します。 アプリをローカルでテストしているだけなので、有効な URL は必要ありません。

    **アプリ/タブの読み込み時に読み込みインジケーターを表示しますか?**

    アプリ **またはタブ** の読み込み時に読み込みインジケーターを含めないを選択します。 既定値は no で、n と **入力します**。

    **個人用アプリをタブ ヘッダーバーなしでレンダリングしますか?**

    タブ **ヘッダー** バーなしでレンダリングする個人用アプリを含めないを選択します。 既定値はいいえ、n と **入力します**。

    **テスト フレームワークと初期テストを含めるには?(y/N)**

    この **プロジェクトの** テスト フレームワークを含めないを選択します。 既定値ははい、n と **入力します**。

    **テレメトリに Azure Applications インサイト使用しますか?(y/N)**

    [Azure **Application インサイト**[を含インサイト。](/azure/azure-monitor/app/app-insights-overview) 既定値は no です。 **n と入力します**。

    **既定のタブ名 (最大 16 文字)?**

    タブの名前を指定します。このタブ名は、ファイルまたは URL パス コンポーネントとしてプロジェクト全体で使用されます。

    **作成するタブの種類**

    矢印キーを使用して [個人用 ( **静的) ] を選択します**。

    **タブに Azure AD のシングルサインオン サポートが必要ですか?**

    タブ **に** Azure ADシングル サインオン のサポートを含めないを選択します。既定値ははい、n と **入力します**。

    > [!IMPORTANT]
    > パス コンポーネント **yourDefaultTabNameTab** は、ジェネレータで既定のタブ名にTab という単語を加えた値 **です**。
    >
    > 例: DefaultTabName: **MyTab**  >  **/MyTabTab/**

### <a name="add-a-personal-tab"></a>個人用タブの追加

**このアプリケーションに個人用タブを追加するには、コンテンツ ページを作成し、既存のファイルを更新します。**

1. コード エディターで、新しい HTML ファイルを作成し、lpersonal.htm **次** のマークアップを追加します。

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

1. 次 **personal.htmアプリケーション** の Web フォルダーに **l** を保存します。

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

1. コード **manifest.jsで、** 次の場所から [オン] を開きます。

    ```bash
    ./src/manifest/manifest.json/
    ```

1. 空の配列 ( ) に次を `staticTabs` 追加 `staticTabs":[]` し、次の JSON オブジェクトを追加します。

    ```json
    {
        "entityId": "personalTab",
        "name": "Personal Tab ",
        "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
        "websiteUrl": "https://{{HOSTNAME}}",
        "scopes": ["personal"]
    }
    ```

1. **contentURL パス コンポーネント** **yourDefaultTabNameTab を** 実際のタブ名で更新します。

1. ファイルに更新されたmanifest.js **を保存** します。

1. IFrame でコンテンツ ページを提供するには、コード エディターで次のパスから **Tab.ts** を開きます。

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. IFrame デコレータの一覧に次の項目を追加します。

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

1. 更新された **Tab.ts ファイルを保存** します。 タブ コードが完成しました。

### <a name="build-and-run-your-application"></a>アプリケーションのビルドと実行

コマンド プロンプトで、プロジェクト ディレクトリを開いて次のタスクを完了します。

#### <a name="create-the-app-package"></a>アプリ パッケージを作成する

タブをテストするには、アプリ パッケージが必要Teams。 これは、次の必須ファイルを含む zip フォルダーです。

- 192 x 192 ピクセルのフル カラー アイコン。 
- **32** x 32 ピクセルの透明なアウトライン アイコン。
- アプリ **manifest.js** を指定するファイルのプロパティです。

パッケージは、ファイル上のファイルのmanifest.jsを検証し、./package ディレクトリに zip フォルダーを生成する **gulp タスクを使用して作成されます**。 コマンド プロンプトで、次のコマンドを入力します。

```bash
gulp manifest
```

#### <a name="build-your-application"></a>アプリケーションのビルド

ビルド コマンドは、ソリューションを **./dist フォルダーに変換** します。 コマンド プロンプトで次のコマンドを入力します。

```bash
gulp build
```

#### <a name="run-your-application-in-localhost"></a>localhost でアプリケーションを実行する

1. コマンド プロンプトに次の情報を入力して、ローカル Web サーバーを起動します。

    ```bash
    gulp serve
    ```

1. 次の図に示すように、ブラウザーに入力し、タブ名に置き換え、アプリケーションのホーム ページ `http://localhost:3007/<yourDefaultAppNameTab>/` **<yourDefaultAppNameTab>** を表示します。

    ![ホーム ページのスクリーンショット](~/assets/images/tab-images/homePage.png)

1. 個人用タブを表示するには、 に移動します `http://localhost:3007/<yourDefaultAppNameTab>/personal.html` 。

    >![個人用タブのスクリーンショット](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

Microsoft Teamsはクラウドベースの製品であり、HTTPS エンドポイントを使用してタブ コンテンツをクラウドから利用できる必要があります。 Teamsはローカル ホスティングを許可しない。 タブをパブリック URL に発行するか、ローカル ポートをインターネットに接続する URL に公開するプロキシを使用する必要があります。

タブ拡張機能をテストするには、このアプリケーションに組み込まれる [ngrok](https://ngrok.com/docs)を使用できます。 Ngrok はリバース プロキシ ソフトウェア ツールで、ローカルで実行中の Web サーバーの一般公開 HTTPS エンドポイントへのトンネルを作成します。 サーバーの Web エンドポイントは、コンピューター上の現在のセッション中に使用できます。 コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。

コマンド プロンプトで localhost を終了し、次のコマンドを入力します。

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> タブが **ngrok** を介して Microsoft Teamsにアップロードされ、正常に保存された後、トンネル セッションが終了するまで、Teamsでタブを表示できます。

### <a name="upload-your-application-to-teams"></a>アップロードを使用してアプリケーションをTeams

**アプリケーションをアプリにアップロードTeams**

1. [次へ] にMicrosoft Teams。 Web ベースのバージョン [を使用する場合は](https://teams.microsoft.com) 、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。
1. 左下隅から、[アプリ] を **選択します**。
1. 左下隅から、カスタム アプリ **アップロードを選択します**。
1. プロジェクト ディレクトリに移動し **、./package** フォルダーを参照し、zip フォルダーを選択し、[開く] を選択 **します**。

    ![個人用タブの追加](../../assets/images/tab-images/addingpersonaltab.png)

1. ポップアップ **ダイアログ ボックスで** [追加] を選択します。 タブがアップロードされ、Teams。

    ![アップロードされた個人用タブ](../../assets/images/tab-images/personaltabuploaded.png)

### <a name="view-your-personal-tab"></a>個人用タブを表示する

[次のページ] の一Teams左側にあるナビゲーション バーで、省略記号 &#x25CF;&#x25CF;&#x25CF; 選択し、一覧からアプリを選択します。

# <a name="aspnet-core"></a>[ASP.NET コア](#tab/aspnetcore)

### <a name="create-a-custom-personal-tab-using-aspnet-core"></a>ユーザー設定を使用してカスタム個人用タブを ASP.NET Core

カスタム個人用タブは、Razor ページを使用してC#作成 ASP.NET Core作成できます。 [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)は、アプリ マニフェストを最終的に作成し、タブを展開してアプリ マニフェストに展開Teams。

### <a name="prerequisites-for-personal-tab"></a>[個人用] タブの前提条件

次の前提条件について理解している必要があります。

- カスタム アプリのアップロードを許可Office 365を有効にしたテナントとチーム **が構成されている必要** があります。 詳細については、「prepare [your Office 365 テナント」を参照してください](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

    > [!NOTE]
    > ユーザーアカウントをお持ちMicrosoft 365場合は、Microsoft Developer Program を通じて無料サブスクリプションに[サインアップできます](https://developer.microsoft.com/en-us/microsoft-365/dev-program)。 サブスクリプションは、継続的な開発に使用している限りアクティブなままです。

- App Studio を使用してアプリケーションをインポートし、Teams。 App Studio をインストールするには、アプリアプリの左下隅にある [アプリ ストア アプリ] を選択Teams App Studio を ![ ](~/assets/images/tab-images/storeApp.png) **検索します**。 タイルを見つけたら、タイルを選択し、ポップアップ ダイアログ ボックスで [追加] を選択してインストールします。

さらに、このプロジェクトでは、次のコードが開発環境にインストールされている必要があります。

- 現在のバージョンの IDE **Visual Studio.NET CORE** クロスプラットフォーム開発ワークロードがインストールされています。 まだインストールされていない場合はVisual Studio最新バージョンを無料でダウンロード[Microsoft Visual Studio Communityインストールできます](https://visualstudio.microsoft.com/downloads)。

- [ngrok](https://ngrok.com)リバース プロキシ ツール。 ngrok を使用して、ローカルで実行中の Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。 [ngrok をダウンロードできます](https://ngrok.com/download)。

### <a name="get-the-source-code"></a>ソース コードを取得する

コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。 簡単なプロジェクトが用意されています。 次のコマンドを使用して、サンプル リポジトリを新しいディレクトリに複製します。

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

または、zip フォルダーをダウンロードしてファイルを抽出して、ソース コードを取得することもできます。

**タブ プロジェクトをビルドして実行するには**

1. ソース コードを取得した後、[プロジェクト] に移動Visual Studio[プロジェクトまたはソリューションを開く **] を選択します**。
1. タブ アプリケーション ディレクトリに移動し **、PersonalTab.sln を開きます**。
1. アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。
1. ブラウザーで、次の URL に移動して、アプリケーションが正しく読み込まれたか確認します。

    - `http://localhost:44325/`
    - `http://localhost:44325/personal`
    - `http://localhost:44325/privacy`
    - `http://localhost:44325/tou`

### <a name="review-the-source-code"></a>ソース コードを確認する

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは、ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成され、セットアップ時に [詳細設定 **- HTTPS** 用に構成] チェック ボックスがオンになっています。 MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。 さらに、空のテンプレートでは既定では静的コンテンツの提供が有効ではないので、静的ファイル ミドルウェアは次のコードを使用してメソッド `Configure()` に追加されます。

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

ASP.NET Core Index と呼ばれるファイルをサイトの既定またはホーム ページとして扱います。 ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。

#### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

- 192 x 192 ピクセルのフル カラー アイコン。 
- **32** x 32 ピクセルの透明なアウトライン アイコン。
- アプリ **manifest.js** を指定するファイルのプロパティです。

これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。 Microsoft Teams指定したマニフェストを読み込み、それを iframe <埋め込み、それをタブ `contentUrl` \> に表示します。

#### <a name="csproj"></a>.csproj

[ソリューション エクスプローラー Visual Studioで、プロジェクトを右クリックし、[ファイルの編集] Project **します**。 ファイルの最後に、アプリケーションのビルド時に zip フォルダーを作成および更新する次のコードが表示されます。

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

### <a name="update-your-application-for-teams"></a>アプリケーションを更新Teams

#### <a name="_layoutcshtml"></a>_Layout.cshtml

タブを JavaScript クライアントにTeamsするには **、JavaScript** クライアント SDK をMicrosoft Teamsし、ページの読み込み後に呼び出 `microsoftTeams.initialize()` しを含める必要があります。 次に、タブとアプリのTeams方法を示します。

[共有] **フォルダーに移動** し **、_Layout.cshtml** を開き、[タグ] セクションに次の項目 `<head>` を追加します。

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

#### <a name="personaltabcshtml"></a>PersonalTab.cshtml

**PersonalTab.cshtml を開** き、呼び出して埋め込 `<script>` みタグを更新します `microsoftTeams.initialize()` 。

更新された **PersonalTab.cshtml を保存してください**。

### <a name="establish-a-secure-tunnel-to-your-tab-for-teams"></a>タブにセキュリティで保護されたトンネルを確立し、Teams

Microsoft Teamsはクラウドベースの製品であり、HTTPS エンドポイントを使用してタブ コンテンツをクラウドから利用できる必要があります。 Teamsはローカル ホスティングを許可しない。 タブをパブリック URL に発行するか、ローカル ポートをインターネットに接続する URL に公開するプロキシを使用する必要があります。

タブをテストするには [、ngrok を使用します](https://ngrok.com/docs)。 ngrok がコンピューターで実行されている間、サーバーの Web エンドポイントを使用できます。 ngrok の無料版では、ngrok を閉じると、次回起動する URL が異なります。

**タブへのセキュリティで保護されたトンネルを確立するには**

1. プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行します。

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

    Ngrok は、インターネットからの要求をリッスンし、ポート 44325 で実行されているアプリケーションにルーティングします。 `https://y8rPrT2b.ngrok.io/`**これは、y8rPrT2b** が ngrok の英数字 HTTPS URL に置き換えられる場所に似ています。

    ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。

2. ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を使用してコンテンツ ページに移動して **、ngrok** が正常に実行および動作されていることを確認します。

> [!TIP]
> この記事で示す手順を完了するには、Visual Studioと ngrok の両方でアプリケーションを実行する必要があります。 アプリケーションの実行を停止する必要がある場合Visual Studio **ngrok を実行し続ける必要があります**。 アプリケーションの要求がアプリケーションで再起動されると、アプリケーションの要求をリッスンしてVisual Studio。 ngrok サービスを再起動する必要がある場合は、新しい URL が返され、その URL を使用する場所を更新する必要があります。

#### <a name="run-your-application"></a>アプリケーションを実行する

このVisual Studio F5 キー **を押** するか、**アプリケーションの**[デバッグ] メニューから [デバッグの開始]**を選択** します。

### <a name="upload-your-tab-with-app-studio-for-teams"></a>アップロード App Studio を使用してタブを開Teams

> [!NOTE]
> **App Studio** を使用すると、ファイル上のmanifest.js **を編集** し、完成したパッケージをファイルにアップロードTeams。 また、手動で編集することもできます **manifest.jsをオンにしてください**。 その場合は、ソリューションを再度ビルドして、アップロードする **Tab.zip作成してください** 。

**App Studio でタブをアップロードするには**

1. [次へ] にMicrosoft Teams。 Web ベースのバージョン [を使用する](https://teams.microsoft.com)場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。

1. [App **Studio] に移動し** 、[マニフェスト エディター **] タブを選択** します。

1. [ **マニフェスト エディターで既存のアプリ** をインポートする] **を選択して** 、タブのアプリ パッケージの更新を開始します。ソース コードには、部分的に完全なマニフェストが付属しています。 アプリ パッケージの名前は次 **tab.zip。** これは、次のパスから使用できます。

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. アップロードtab.zipApp  **Studio にアクセスします**。

#### <a name="update-your-app-package-with-manifest-editor"></a>マニフェスト エディターを使用してアプリ パッケージを更新する

アプリ パッケージを App Studio にアップロードしたら、アプリ パッケージを構成する必要があります。

マニフェスト エディターのウェルカム ページの右側のウィンドウで、新しくインポートしたタブのタイルを選択します。

マニフェスト エディターの左側に手順の一覧が表示され、右側には、各手順の値が必要なプロパティの一覧が表示されます。 この情報の多くが、ユーザーのmanifest.js **によって** 提供されますが、更新する必要があるフィールドがあります。

##### <a name="details-app-details"></a>詳細: アプリの詳細

[アプリ **の詳細] セクションで、次の内容を実行** します。

1. **[Id] で**、[**生成] を** 選択して、アプリの新しいアプリ ID を生成します。

1. [**開発者情報] で****、ngrok** HTTPS URL を使用して Web **サイトを** 更新します。

    ![アプリの URL が更新されました](../../assets/images/tab-images/appurls.png)

1. [**アプリの URL] で**、[プライバシーに関する **声明] と**[使用条件] を更新して、>。 `https://<yourngrokurl>/privacy`  `https://<yourngrokurl>/tou`

##### <a name="capabilities-tabs"></a>機能: タブ

[タブ **] セクションで、次の設定を** 行います。

1. [個人用 **タブの追加] で、[** 追加] を **選択します**。 ポップアップ ダイアログ ボックスが表示されます。

1. [名前] に個人用タブの名前を **入力します**。

1. エンティティ **ID を入力します**。

1. で **コンテンツ URL を** 更新 `https://<yourngrokurl>/personalTab` します。

    [Web サイト **の URL] フィールドは** 空白のままにします。

    ![[個人用] タブの詳細](../../assets/images/tab-images/personaltabdetails.png)

1. **[保存]** を選択します。

##### <a name="finish-domains-and-permissions"></a>完了: ドメインとアクセス許可

[ドメイン **とアクセス許可**] セクションで、タブのドメインには、HTTPS プレフィックスのない ngrok URL が含まれている必要があります `<yourngrokurl>.ngrok.io/` 。

###### <a name="finish-test-and-distribute"></a>完了: テストと配布

> [!IMPORTANT]
> 右側の [説明] **で**、次の警告が表示されます。
>
> &#9888; **'validDomains' 配列にトンネリング サイトを含めすることはできません。..**
>
> この警告は、タブのテスト中に無視できます。

1. [テストと **配布] セクションで、[** インストール] を **選択します**。

1. ポップアップ ダイアログ ボックスで、[追加] を選択 **すると** 、タブが表示されます。

    ![[個人用] タブの ASPNET がアップロードされました](../../assets/images/tab-images/personaltabaspnetuploaded.png)

### <a name="view-your-personal-tab-in-teams"></a>[個人用] タブを [Teams

1. アプリの左上にあるナビゲーション バーで、Teamsを選択 &#x25CF;&#x25CF;&#x25CF;。 個人用アプリの一覧が表示されます。

1. リストからタブを選択して表示します。

# <a name="aspnet-core-mvc"></a>[ASP.NET CoreMVC](#tab/aspnetcoremvc)

### <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a>MVC を使用してカスタム個人用タブを ASP.NET Coreする

MVC を使用してカスタム個人用タブをC#し ASP.NET Coreできます。 [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)は、アプリ マニフェストを最終的に作成し、タブを展開してアプリ マニフェストに展開Teams。

### <a name="prerequisites-for-personal-tab-with-aspnet-core-mvc"></a>MVC を使用した個人用タブ ASP.NET Core前提条件

- カスタム アプリのアップロードを許可Microsoft 365を有効にしたチームとテナント **が必要** です。 詳細については、「prepare [your Office 365 テナント」を参照してください](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

    > [!NOTE]
    > ユーザーアカウントをお持ちMicrosoft 365場合は、Microsoft Developer Program を通じて無料サブスクリプションに[サインアップできます](https://developer.microsoft.com/en-us/microsoft-365/dev-program)。 サブスクリプションは、継続的な開発に使用している限りアクティブなままです。

- App Studio を使用してアプリケーションをインポートし、Teams。 App Studio をインストールするには、アプリアプリの左下隅にある [アプリ ストア アプリ] を選択Teams App Studio を ![ ](~/assets/images/tab-images/storeApp.png) **検索します**。 タイルを見つけたら、タイルを選択し、ポップアップ ダイアログ ボックスで [追加] を選択してインストールします。

さらに、このプロジェクトでは、次のコードが開発環境にインストールされている必要があります。

- 現在のバージョンの IDE **Visual Studio.NET CORE** クロスプラットフォーム開発ワークロードがインストールされています。 まだインストールされていない場合はVisual Studio最新バージョンを無料でダウンロード[Microsoft Visual Studio Communityインストールできます](https://visualstudio.microsoft.com/downloads)。

- [ngrok](https://ngrok.com)リバース プロキシ ツール。 ngrok を使用して、ローカルで実行中の Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。 [ngrok をダウンロードできます](https://ngrok.com/download)。

### <a name="get-the-source-code"></a>ソース コードを取得する

コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。 簡単なプロジェクトが用意されています。 次のコマンドを使用して、サンプル リポジトリを新しいディレクトリに複製します。

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

または、zip フォルダーをダウンロードしてファイルを抽出して、ソース コードを取得することもできます。

**タブ プロジェクトをビルドして実行するには**

1. ソース コードを取得した後、[プロジェクト] に移動Visual Studioプロジェクトまたはソリューションを開 **く] を選択します**。
1. タブ アプリケーション ディレクトリに移動し **、PersonalTabMVC.sln を開きます**。
1. アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。
1. ブラウザーで、次の URL に移動して、アプリケーションが正しく読み込まれたか確認します。

    * `http://localhost:44335`
    * `http://localhost:44335/privacy`
    * `http://localhost:44335/tou`

### <a name="review-the-source-code"></a>ソース コードを確認する

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは、ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成され、セットアップ時に [詳細設定 **- HTTPS** 用に構成] チェック ボックスがオンになっています。 MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。 さらに、空のテンプレートでは既定では静的コンテンツの提供が有効ではないので、静的ファイル ミドルウェアは次のコードを使用してメソッド `Configure()` に追加されます。

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
* **32** x 32 ピクセルの透明なアウトライン アイコン。
* アプリ **manifest.js** を指定するファイルのプロパティです。

これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。 Microsoft Teams指定したマニフェストを読み込み、IFrame に埋め込み、タブ `contentUrl` にレンダリングします。

#### <a name="csproj"></a>.csproj

[ソリューション エクスプローラー Visual Studioで、プロジェクトを右クリックし、[ファイルの編集] Project **します**。 ファイルの最後に、アプリケーションのビルド時に zip フォルダーを作成および更新する次のコードが表示されます。

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

**PersonalTab.cs** は、ユーザーが PersonalTab ビューでボタンを選択すると **、PersonalTabController** から呼び出される Message オブジェクトとメソッド **を表示** します。

#### <a name="views"></a>ビュー

次に示すのは、MVC の ASP.NET Coreです。

* ホーム: ASP.NET Core Index と呼ばれるファイルをサイトの既定またはホーム ページとして扱います。 ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。

* 共有: 部分ビュー マークアップ **_Layout.cshtml** には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれます。 また、ライブラリのTeamsします。

#### <a name="controllers"></a>コントローラー

コントローラーはプロパティを使用 `ViewBag` して、値を Views に動的に転送します。

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

**ngrok を実行してコンテンツ ページを確認するには**

1. プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行します。

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

    Ngrok は、インターネットからの要求をリッスンし、ポート 44325 で実行されているアプリケーションにルーティングします。 `https://y8rPrT2b.ngrok.io/`**これは、y8rPrT2b** が ngrok の英数字 HTTPS URL に置き換えられる場所に似ています。

    ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。

1. ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を使用してコンテンツ ページに移動して **、ngrok** が正常に実行および動作されていることを確認します。

> [!TIP]
> この記事で示す手順を完了するには、Visual Studioと ngrok の両方でアプリケーションを実行する必要があります。 アプリケーションの実行を停止する必要がある場合Visual Studio **ngrok を実行し続ける必要があります**。 アプリケーションの要求がアプリケーションで再起動されると、アプリケーションの要求をリッスンしてVisual Studio。 ngrok サービスを再起動する必要がある場合は、新しい URL が返され、その URL を使用する場所を更新する必要があります。

#### <a name="run-your-application"></a>アプリケーションを実行する

このVisual Studio F5 キー **を押** するか、**アプリケーションの**[デバッグ] メニューから [デバッグの開始]**を選択** します。

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

---

## <a name="reorder-static-personal-tabs"></a>静的な個人用タブの並べ替え

マニフェスト バージョン 1.7 から、開発者は個人用アプリ内のすべてのタブを再配置できます。 特に、開発者はボット チャットタブを移動できます。これは常に既定で最初の位置に、個人用アプリのタブ ヘッダー内の任意の場所に移動できます。 2 つの予約済みタブ `entityId` キーワードが宣言され、**会話と****についてです**。

個人用スコープを持つ **ボットを作成** すると、既定では個人用アプリの最初のタブ位置に表示されます。 別の位置に移動する場合は、予約キーワードである会話を使用して静的タブ オブジェクトをマニフェストに追加する必要 **があります**。 [ **会話** ] タブは、配列に会話タブを追加する場所に応 **じて、Web** またはデスクトップに表示 `staticTabs` されます。

```json
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

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
* [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)
* [会話タブを作成する](~/tabs/how-to/conversational-tabs.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
