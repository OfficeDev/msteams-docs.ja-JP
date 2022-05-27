---
title: プライベート タブを作成する
author: laujan
description: Node.js を使用して、Microsoft Teams 用の Yeoman Generator、ASP.NET Core、ASP.NET Core MVC を使用した個人用タブを作成し、アプリ マニフェストを更新するためのクイック スタート ガイド。
ms.localizationpriority: high
ms.topic: quickstart
ms.author: lajanuar
keywords: yeoman ASP.NET MVC パッケージ appmanifest 会話ドメイン アクセス許可ストア
zone_pivot_groups: teams-app-environment
ms.openlocfilehash: 9da0078813d43584d415ccb9425a529decdc78bd
ms.sourcegitcommit: 929391b6c04d53ea84a93145e2f29d6b96a64d37
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2022
ms.locfileid: "65673021"
---
# <a name="create-a-personal-tab"></a>プライベート タブを作成する

[個人] タブは、個人を対象としたボットと共に、個人用アプリの一部であり、1 人のユーザーを対象としています。 簡単にアクセスできるように、左側のナビゲーション バーにピン留めすることができます。 個人用タブの[順序を変更](#reorder-static-personal-tabs)することもできます。

個人用タブを作成するための[前提条件](~/tabs/how-to/tab-requirements.md)がすべて揃っていることを確認します。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

::: zone pivot="node-java-script"

## <a name="create-a-personal-tab-with-nodejs"></a>Node.js を使用して個人用タブを作成する

1. コマンド プロンプトで、Node.js のインストール後に次のコマンドを入力して [Yeoman](https://yeoman.io/) パッケージと [gulp-cli](https://www.npmjs.com/package/gulp-cli) パッケージをインストールします。

    ```cmd
    npm install yo gulp-cli --global
    ```

1. コマンド プロンプトで、次のコマンドを入力して、Microsoft Teams アプリ ジェネレーターをインストールします。

    ```cmd
    npm install generator-teams --global
    ```

個人用タブを作成する手順を次に示します。

1. [個人用タブを使用してアプリケーションを生成する](#generate-your-application-with-a-personal-tab)
1. [個人用タブにコンテンツ ページを追加する](#add-a-content-page-to-the-personal-tab)
1. [アプリ パッケージを作成する](#create-your-app-package)
1. [デーモン アプリケーションをビルドして実行する](#build-and-run-your-application)
1. [個人用タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab)
1. [Microsoft Teams にアプリ パッケージをアップロードする](#upload-your-application-to-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>個人用タブを使用してアプリケーションを生成する

1. コマンド プロンプトで、個人用タブの新しいディレクトリを作成します。

1. 新しいディレクトリに次のコマンドを入力して、Microsoft Teams アプリ ジェネレーターを起動します。

    ```cmd
    yo teams
    ```

1. Microsoft Teams アプリ ジェネレーターによって `manifest.json` ファイルを更新するように求められる、一連の質問に値を指定します。

    :::image type="content" source="~/assets/images/tab-images/teamsTabScreenshot.PNG" alt-text="Teams ジェネレーター" border="true":::

    <details>
    <summary><b>manifest.json ファイルを更新するための一連の質問</b></summary>

    * **ソリューション名は何ですか?**

      ソリューション名はプロジェクト名です。 候補の名前をそのまま使用するには、**Enter** キーを押します。

    * **ファイルをどこに保存しますか?**

      現在、プロジェクト ディレクトリにいます。 **Enter** キーを押します。

    * **Microsoft Teams アプリ プロジェクトのタイトル**

      タイトルはアプリ パッケージ名であり、アプリ マニフェストと説明で使用されます。 タイトルを入力するか、**Enter** キーを押して既定の名前をそのまま使用します。

    * **(会社) 名 (最大 32 文字)**

      会社名はアプリ マニフェストで使用されます。 会社名を入力するか、**Enter** キーを押して既定の名前をそのまま使用します。

    * **使用するマニフェスト バージョン**

      既定のスキーマを選択します。

    * **クイック スキャフォールディング (Y/n)**

      既定値は [はい] です。Microsoft パートナー ID を入力するには、**[n]** を入力します。

    * **Microsoft パートナー ID (お持ちの場合): (空白のままにする)**

      このフィールドは必須ではなく、既に [Microsoft Partner Network](https://partner.microsoft.com) に参加している場合にのみ使用する必要があります。

    * **プロジェクトに何を追加しますか?**

      **( &ast; ) A タブ** を選択します。

    * **このソリューションをホストする URL**

      既定では、ジェネレーターは Azure Web サイトの URL を提案します。 アプリをローカルでのみテストしているため、有効な URL は必要ありません。

    * **アプリ/タブが読み込まれたときに、読み込みインジケーターを表示しますか?**

      アプリまたはタブの読み込み時に読み込みインジケーターを含め **ない** ことを選択します。 既定値は [いいえ] です。**[n]** を入力します。

    * **個人用アプリをタブ ヘッダーバーなしでレンダリングしますか?**

      タブのヘッダーバーなしで表示される個人用アプリを含め **ない** ことを選択します。 既定値は [いいえ] です。**[n]** を入力します。

    * **Test フレームワークと初期テストを含めますか? (y/N)**

      このプロジェクトのテスト フレームワークを含め **ない** ことを選択します。 既定値は [いいえ] です。**[n]** を入力します。

    * **ESLint のサポートを含めますか? (y/N)**

      ESLint サポートを含めないことを選択します。 既定値は [いいえ] です。**[n]** を入力します。

    * **テレメトリに Azure Application Insights を使用しますか? (y/N)**

      [Azure Application Insights](/azure/azure-monitor/app/app-insights-overview) を含め **ない** ことを選択します。 既定値は [いいえ] です。**[n]** を入力します。

    * **既定のタブ名 (最大 16 文字)**

      タブに名前を付けます。このタブ名は、ファイルまたは URL パス コンポーネントとしてプロジェクト全体で使用されます。

    * **作成するタブの種類を選択してください。**

      方向キーを使用して、[**個人用**] を選択します。

    * **タブのMicrosoft Azure Active Directory (Azure AD) シングル サインオンのサポートが必要ですか?**

      タブの Azure AD シングル サインオンを含め **ない** ことを選択します。既定値は yes で、**n** と入力します。

    </details>

### <a name="add-a-content-page-to-the-personal-tab"></a>個人用タブにコンテンツ ページを追加する

コンテンツ ページを作成し、個人用タブ アプリケーションの既存のファイルを更新します:

1. 次のマークアップを使用して、Visual Studio Code に新しい **personal.html** ファイルを作成します。

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

1. 次の場所にあるアプリケーションの **パブリック** フォルダーに **personal.html** を保存します。

    ```
    ./src/public/<yourDefaultTabNameTab>/personal.html
    ```

1. Visual Studio Code 内の次の場所から `manifest.json` を開きます。

    ```
     ./src/manifest/manifest.json
    ```

1. 空の `staticTabs` 配列 (`staticTabs":[]`) に次を追加し、次の JSON オブジェクトを追加します:

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
    > path コンポーネント **yourDefaultTabNameTab** は、**既定のタブ名** のジェネレーターに入力した値プラス単語 **Tab** になります。
    >
    > たとえば、DefaultTabName は **MyTab**、次に **/MyTabTab/** です。

1. **contentURL** パス コンポーネント **yourDefaultTabNameTab** を実際のタブ名で更新します。

1. 更新された `manifest.json` ファイルを保存します。

1. 次のパスから Visual Studio Code で **Tab.ts** を開き、IFrame でコンテンツ ページを提供します:

    ```bash
    ./src/server/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. IFrame デコレーターの一覧に次を追加します。

    ```typescript
     @PreventIframe("/<yourDefaultTabName Tab>/personal.html")
    ```

1. 更新されたファイルを保存します。 コードはこれで完了です。

### <a name="create-your-app-package"></a>アプリ パッケージを作成する

Teams でアプリケーションをビルドして実行するには、アプリ パッケージが必要です。 アプリ パッケージは、`manifest.json` ファイルを検証し、`./package` ディレクトリに zip フォルダーを生成する gulp タスクを使用して作成されます。 コマンド プロンプトで、コマンド `gulp manifest` を実行します。

### <a name="build-and-run-your-application"></a>アプリケーションをビルドして実行する

#### <a name="build-your-application"></a>アプリケーションをビルドする

コマンド プロンプトで次のコマンドを入力して、**ソリューションを ./dist** フォルダーに移します:

```cmd
gulp build
```

#### <a name="run-your-application"></a>アプリケーションを実行する

1. コマンド プロンプトで次のコマンドを入力して、ローカル Web サーバーを起動します。

    ```cmd
    gulp serve
    ```

1. ブラウザーで `http://localhost:3007/<yourDefaultAppNameTab>/` を入力して、アプリケーションのホーム ページを表示します。

    :::image type="content" source="~/assets/images/tab-images/homePage.png" alt-text="既定のタブ" border="true":::

1. `http://localhost:3007/<yourDefaultAppNameTab>/personal.html` を参照して、個人用タブを表示します。

    :::image type="content" source="~/assets/images/tab-images/personalTab.PNG" alt-text="既定の html タブ" border="true":::

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

コマンド プロンプトでローカルホストを終了し、次のコマンドを入力して、タブへのセキュリティで保護されたトンネルを確立します:

```cmd
gulp ngrok-serve
```

> [!IMPORTANT]
> タブが **ngrok** 経由で Microsoft Teams にアップロードされ、正常に保存されたら、トンネル セッションが終了するまで Teams で表示できます。

### <a name="upload-your-application-to-teams"></a>Microsoft Teams にアプリ パッケージをアップロードする

1. Microsoft Teams に移動し、**[アプリ]**&nbsp;:::image type="content" source="~/assets/images/tab-images/store.png" alt-text="[Teamsストア]"::: を選択します。
1. [**アプリの管理**] を選択し、[**カスタム アプリをアップロード**] します。
1. プロジェクト ディレクトリに移動し、 **./package** フォルダーに移動し、zip フォルダーを選択して [**開く**] を選択します。

    :::image type="content" source="~/assets/images/tab-images/addingpersonaltab.png" alt-text="個人用タブの追加" border="true":::

1. ダイアログで **[追加]** を選択します。 タブが Teams にアップロードされます。

    :::image type="content" source="~/assets/images/tab-images/personaltabuploaded.png" alt-text="個人用タブがアップロードされました" border="true":::

1. Teams の左側のウィンドウで省略記号 &#x25CF;&#x25CF;&#x25CF; を選択し、アップロードしたアプリを選択して個人用タブを表示します。

   これで、Teams に個人用タブが正常に作成され、追加されました。
  
   Teams に個人用タブがあるため、個人用タブを[並べ替える](#reorder-static-personal-tabs)こともできます。

::: zone-end

::: zone pivot="razor-csharp"

## <a name="create-a-personal-tab-with-aspnet-core"></a>ASP.NET Coreを使用して個人用タブを作成する

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. 次のコマンドを使用してサンプル リポジトリを新しいディレクトリに複製するか、[ソース コード](https://github.com/OfficeDev/Microsoft-Teams-Samples) をダウンロードしてファイルを抽出できます:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

個人用タブを作成する手順を次に示します。

1. [個人用タブを使用してアプリケーションを生成する](#generate-your-application-with-a-personal-tab-1)
1. [アプリケーションを更新して実行する](#update-and-run-your-application)
1. [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab-1)
1. [開発者ポータルを使用してアプリ パッケージを更新する](#update-your-app-package-with-developer-portal)
1. [Teams でアプリをプレビューする](#preview-your-app-in-teams)

### <a name="generate-your-application-with-a-personal-tab"></a>個人用タブを使用してアプリケーションを生成する

1. Visual Studio を開き、[**プロジェクトまたはソリューションを開く**] を選択します。

1. [**Microsoft-Teams-Samples**]  >  [**samples**]  >  [**tab-personal**]  >  [**razor-csharp**] フォルダーに移動し、**PersonalTab.sln** を開きます。

1. Visual Studioで **F5** を選択するか、アプリケーションの [**デバッグ**] メニューから [**デバッグの開始**] を選択して、アプリケーションが正しく読み込まれたかどうかを確認します。 ブラウザーで、次の URL に移動します。

    * <http://localhost:3978/>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>ソース コードを確認する</b></summary>

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは ASP.NET Core 3.1 Web アプリケーションの空のテンプレートから作成され、セットアップ時に **[Advanced - Configure for HTTPS]** チェック ボックスがオンになっています。 MVC サービスは、依存関係挿入フレームワーク `ConfigureServices()` のメソッドによって登録されます。 また、空のテンプレートでは、既定では静的コンテンツの提供が有効にされないため、次のコードを使用して静的ファイル ミドルウェアがメソッド `Configure()` に追加されます。

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

ASP.NET Core では、Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

#### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core は、**Index** という名前のファイルをサイトの既定またはホーム ページとして扱います。 ブラウザー URL がサイトのルートを指すと、**Index.cshtml** がアプリケーションのホーム ページとして表示されます。

#### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています:

* 192 x 192 ピクセルのフル カラー アイコン。
* 32 x 32 ピクセルの透明なアウトライン アイコン。
* アプリの属性を指定する `manifest.json` ファイル。

これらのファイルは、Teams へのタブのアップロードに使用するために、アプリ パッケージで zip 形式にする必要があります。 Microsoft Teams は、マニフェストで指定された `contentUrl` を読み込み、<iframe\> に埋め込み、タブにレンダリングします。

#### <a name="csproj"></a>.csproj

Visual Studio ソリューション エクスプローラーで、プロジェクトを右クリックし、[**プロジェクト ファイルの編集**] を選択します。 ファイルの最後には、アプリケーションのビルド時に zip フォルダーを作成して更新する次のコードが表示されます。

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

1. Visual Studio ソリューション エクスプローラーを開き、[**ページ**]  >  [**共有**] フォルダーに移動し、**_Layout.cshtml** を開き、`<head>` タグ セクションに次を追加します:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v2.0.0/js/MicrosoftTeams.min.js"></script>
    ```

1. Visual Studio ソリューション エクスプローラー [**Pages**] フォルダーから **PersonalTab.cshtml** を開き、`app.initialize()` を `<script>` タグに追加して保存します。

1. Visual Studioで **F5** を選択するか、アプリケーションの [**デバッグ**] メニューから [**デバッグの開始**] を選択します。

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行して、タブへのセキュリティで保護されたトンネルを確立します:

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>開発者ポータルを使用してアプリ パッケージを更新する

1. [**開発者ポータル**](https://dev.teams.microsoft.com/home)に移動します。

1. **アプリ** を開き、[**アプリのインポート**] を選択します。

1. アプリ パッケージファイル名は `tab.zip` で、`/bin/Debug/netcoreapp3.1/tab.zip` パスで使用できます。

1. 開発者ポータルで `tab.zip` を選択して開きます。

1. 既定の **アプリ ID** が作成され、**[基本情報]** セクションに入力されます。

1. **[説明]** にアプリの短い説明と長い説明を追加します。

1. **[開発者情報]** で、必要な詳細を追加し、**Web サイト (有効な HTTPS URL である必要があります)** に ngrok HTTPS URL を指定します。

1. **アプリの URL** で、プライバシー ポリシーを `https://<yourngrokurl>/privacy` に、利用規約を `https://<yourngrokurl>/tou` に更新して保存します。

1. **アプリの機能** で、[**個人用アプリ**]  >  [**初めての個人用アプリ タブを作成**] を選択し、[名前] を入力して、[**コンテンツ URL**] を `https://<yourngrokurl>/personalTab` で更新します。 [Web サイト URL] フィールドを空白のままにし、ドロップダウン リストと [**追加**] から personalTab として [**コンテキスト**] を選択します。

1. **[保存]** を選択します。

1. [ドメイン] セクションでは、タブのドメインに HTTPS プレフィックス `<yourngrokurl>.ngrok.io` のない ngrok URL を含める必要があります。

### <a name="preview-your-app-in-teams"></a>Teams でアプリをプレビューする

1. [開発者ポータル] ツール バーの **[Teamsでプレビュー]** を選択すると、アプリが正常にサイドロードされたことを開発者ポータルから通知されます。 アプリの [**追加**] ページが表示されます。

1. [**追加**] を選択して、Teams にアプリを読み込みます。 タブが Teams で利用できるようになりました。

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetuploaded.png" alt-text="既定のタブ" border="true":::

   これで、Teams に個人用タブが正常に作成され、追加されました。
  
   Teams に個人用タブがあるため、個人用タブを[並べ替える](#reorder-static-personal-tabs)こともできます。

::: zone-end

::: zone pivot="mvc-csharp"

## <a name="create-a-personal-tab-with-aspnet-core-mvc"></a>ASP.NET Core MVC を使用して個人用タブを作成する

1. コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。

1. 次のコマンドを使用してサンプル リポジトリを新しいディレクトリに複製するか、[ソース コード](https://github.com/OfficeDev/Microsoft-Teams-Samples) をダウンロードしてファイルを抽出できます:

    ```cmd
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

個人用タブを作成する手順を次に示します。

1. [個人用タブを使用してアプリケーションを生成する](#generate-your-application-with-a-personal-tab-2)
1. [アプリケーションを更新して実行する](#update-and-run-your-application-1)
1. [タブへのセキュリティで保護されたトンネルを確立する](#establish-a-secure-tunnel-to-your-tab-2)
1. [開発者ポータルを使用してアプリ パッケージを更新する](#update-your-app-package-with-developer-portal-1)
1. [Teams でアプリをプレビューする](#preview-your-app-in-teams-1)

### <a name="generate-your-application-with-a-personal-tab"></a>個人用タブを使用してアプリケーションを生成する

1. Visual Studio を開き、[**プロジェクトまたはソリューションを開く**] を選択します。

1. [**Microsoft-Teams-Samples**]  >  [**samples**]  >  [**tab-personal**]  >  [**mvc-csharp**] フォルダーに移動し、Visual Studio で **PersonalTabMVC.sln** を開きます。

1. Visual Studio で **F5** を選択するか、アプリケーションの [**デバッグ**] メニューから [**デバッグの開始**] を選択して、アプリケーションが正しく読み込まれたかどうかを確認します。 ブラウザーで、次の URL に移動します。

    * <http://localhost:3978>
    * <http://localhost:3978/personalTab>
    * <http://localhost:3978/privacy>
    * <http://localhost:3978/tou>

<details>
<summary><b>ソース コードを確認する</b></summary>

#### <a name="startupcs"></a>Startup.cs

このプロジェクトは ASP.NET Core 3.1 Web アプリケーションの空のテンプレートから作成され、セットアップ時に **[Advanced - Configure for HTTPS]** チェック ボックスがオンになっています。 MVC サービスは、依存関係挿入フレームワーク `ConfigureServices()` のメソッドによって登録されます。 また、空のテンプレートでは、既定では静的コンテンツの提供が有効にされないため、次のコードを使用して静的ファイル ミドルウェアがメソッド `Configure()` に追加されます。

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

ASP.NET Core では、Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

#### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています:

* 192 x 192 ピクセルの **フル カラー アイコン**。
* 32 x 32 ピクセルの **透明なアウトライン アイコン**。
* アプリの属性を指定する `manifest.json` ファイル。

これらのファイルは、Teams へのタブのアップロードに使用するために、アプリ パッケージで zip 形式にする必要があります。 Microsoft Teams は、マニフェストで指定された `contentUrl` を読み込み、IFrame に埋め込み、タブにレンダリングします。

#### <a name="csproj"></a>.csproj

Visual Studio ソリューション エクスプローラーで、プロジェクトを右クリックし、[**プロジェクト ファイルの編集**] を選択します。 ファイルの最後には、アプリケーションのビルド時に zip フォルダーを作成して更新する次のコードが表示されます:

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

**PersonalTab.cs** は、ユーザーが [**PersonalTab**] ビューでボタンを選択したときに **PersonalTabController** から呼び出されるメッセージ オブジェクトとメソッドを表示します。

#### <a name="views"></a>ビュー

これらのビューは、ASP.NET Core MVC のさまざまなビューです。

* ホーム: ASP.NET Core は、**Index** という名前のファイルをサイトの既定またはホーム ページとして扱います。 ブラウザー URL がサイトのルートを指すと、**Index.cshtml** がアプリケーションのホーム ページとして表示されます。

* 共有: 部分ビュー マークアップ **_Layout.cshtml** には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれています。 また、Teams ライブラリも参照します。

#### <a name="controllers"></a>コントローラー

コントローラーは、`ViewBag` プロパティを使用して、値を Views に動的に転送します。

</details>

### <a name="update-and-run-your-application"></a>アプリケーションを更新して実行する

1. Visual Studio ソリューション エクスプローラーを開き、[**ビュー**]  >  [**[共有**] フォルダーに移動し、**_Layout.cshtml** を開き、`<head>` タグ セクションに次を追加します:

    ```HTML
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v2.0.0/js/MicrosoftTeams.min.js"></script>
    ```

1. Visual Studio ソリューション エクスプローラーで、[**ビュー**]  >  [**PersonalTab**] フォルダーから **PersonalTab.cshtml** を開き、`<script>` タグ内で `app.initialize()` を追加して保存します。

1. Visual Studioで **F5** を選択するか、アプリケーションの [**デバッグ**] メニューから [**デバッグの開始**] を選択します。

### <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行して、タブへのセキュリティで保護されたトンネルを確立します:

```cmd
ngrok http 3978 --host-header=localhost
```

### <a name="update-your-app-package-with-developer-portal"></a>開発者ポータルを使用してアプリ パッケージを更新する

1. [**開発者ポータル**](https://dev.teams.microsoft.com/home)に移動します。

1. **[アプリ]** を開き、**[アプリのインポート]** を選択します。

1. アプリ パッケージの名前は **tab.zip** です。 次のパスで使用できます:

    ```
    /bin/Debug/netcoreapp3.1/tab.zip
    ```

1. **tab.zip** を選択し、開発者ポータルで開きます。

1. 既定の **アプリ ID** が作成され、**[基本情報]** セクションに入力されます。

1. **[説明]** にアプリの短い説明と長い説明を追加します。

1. **[開発者情報]** で、必要な詳細を追加し、**Web サイト (有効な HTTPS URL である必要があります)** に ngrok HTTPS URL を指定します。

1. **アプリの URL** で、プライバシー ポリシーを `https://<yourngrokurl>/privacy` に、利用規約を `https://<yourngrokurl>/tou` に更新して保存します。

1. **アプリの機能** で、[**個人用アプリ**]  >  [**初めての個人用アプリ タブを作成**] を選択し、[名前] を入力して、[**コンテンツ URL**] を `https://<yourngrokurl>/personalTab` で更新します。 [Web サイト URL] フィールドを空白のままにし、ドロップダウン リストと [**追加**] から personalTab として [**コンテキスト**] を選択します。

1. **[保存]** を選択します。

1. [ドメイン] セクションでは、タブのドメインに HTTPS プレフィックス `<yourngrokurl>.ngrok.io` のない ngrok URL を含める必要があります。

### <a name="preview-your-app-in-teams"></a>Teams でアプリをプレビューする

1. [開発者ポータル] ツール バーの **[Teamsでプレビュー]** を選択すると、アプリが正常にサイドロードされたことを開発者ポータルから通知されます。 アプリの [**追加**] ページが表示されます。

1. [**追加**] を選択して、Teams にアプリを読み込みます。 タブが Teams で利用できるようになりました。

    :::image type="content" source="~/assets/images/tab-images/personaltabaspnetmvccoreuploaded.png" alt-text="個人タブ" border="true":::
  
   これで、Teams に個人用タブが正常に作成され、追加されました。

   Teams に個人用タブがあるため、個人用タブを[並べ替える](#reorder-static-personal-tabs)こともできます。

::: zone-end

## <a name="reorder-static-personal-tabs"></a>静的な個人用タブの並べ替え

マニフェスト バージョン 1.7 以降では、開発者が個人用アプリ内のすべてのタブを再配置できます。 特に、開発者は [**ボット チャット**] タブを移動できます。このタブは、常に既定で最初の位置 (個人用アプリ タブ ヘッダー内の任意の場所) に移動できます。 2 つの予約済みタブ `entityId` キーワードが宣言されます:**会話** と **プロフィール**。

**個人用** スコープを使用してボットを作成すると、既定では個人用アプリの最初のタブ位置に表示されます。 別の位置に移動する場合は、予約済みのキーワードである "**会話**" を使用して静的タブ オブジェクトをマニフェストに追加する必要があります。 [**会話**] タブは、`staticTabs` 配列内の [**会話**] タブを追加する場所に応じて、Web またはデスクトップに表示されます。

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

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [チャネルまたはグループ タブの作成](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>関連項目

* [Teams タブ](~/tabs/what-are-tabs.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
* [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)
* [会話タブを作成する](~/tabs/how-to/conversational-tabs.md)
* [個人用アプリまたはタブから Teams に共有する](~/concepts/build-and-test/share-to-teams-from-personal-app-or-tab.md)
