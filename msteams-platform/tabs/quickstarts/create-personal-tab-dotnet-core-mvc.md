---
title: ASP を使用して個人用タブを作成します。 NET Core MVC
author: surbhigupta
description: ASP を使用してカスタム個人用タブを作成するクイック スタート ガイド。 NET Core MVC。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: ac01ae64f44ccf3e06476d4412b16ac9a4730f6c
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069150"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a>MVC を使用してカスタム個人用タブを ASP.NET Coreする

このクイック スタートでは、コア MVC を使用してカスタム個人用タブを作成C#を ASP.Net します。 また、アプリ マニフェストをMicrosoft Teams、アプリ マニフェストにタブを展開するために App [Studio](~/concepts/build-and-test/app-studio-overview.md)をTeams。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>ソース コードを取得する

コマンド プロンプトを開き、タブ プロジェクトの新しいディレクトリを作成します。 開始する簡単なプロジェクトを提供しました。 ソース コードを取得するには、zip フォルダーをダウンロードしてファイルを抽出するか、サンプル リポジトリを新しいディレクトリに複製します。

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

ソース コードを取得したら、[プロジェクト] を開Visual Studioプロジェクトまたはソリューションを開 **く] を選択します**。 タブ アプリケーション ディレクトリに移動し **、PersonalTabMVC.sln を開きます**。

アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。 ブラウザーで、以下の URL に移動して、アプリケーションが正しく読み込まれたか確認します。

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a>ソース コードを確認する

### <a name="startupcs"></a>Startup.cs

このプロジェクトは ASP から作成されました。 NET Core 2.2 Web Application 空のテンプレートで、セットアップ時に *[Advanced - Configure for HTTPS]* チェック ボックスがオンになっています。 MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。 さらに、空のテンプレートでは既定では静的コンテンツの配信が有効ではないので、静的ファイル ミドルウェアがメソッドに追加 `Configure()` されます。

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

### <a name="wwwroot-folder"></a>wwwroot フォルダー

ASP で。 NET Core、Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

* 192 x 192 ピクセルのフル カラー アイコン。 
* **32** x 32 ピクセルの透明なアウトライン アイコン。
* アプリ **manifest.js** を指定するファイルのプロパティです。

これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。 Microsoft Teams指定されたマニフェストを読み込み、IFrame に埋め込み、それをタブ `contentUrl` にレンダリングします。

### <a name="csproj"></a>.csproj

[ソリューション エクスプローラー Visual Studio] ウィンドウでプロジェクトを右クリックし、[ファイルの編集] Project **します**。 ファイルの下部には、アプリケーションのビルド時に zip フォルダーを作成および更新するコードが表示されます。

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

### <a name="models"></a>モデル

**PersonalTab.cs** は、ユーザーが PersonalTab ビューでボタンを選択すると *、PersonalTabController* から呼び出される Message オブジェクトとメソッド **を示** します。

### <a name="views"></a>ビュー

#### <a name="home"></a>ホーム

ASP。 NET Core は **、Index** と呼ばれるファイルをサイトの既定またはホーム ページとして扱います。 ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。

#### <a name="shared"></a>共有

部分ビュー マークアップ *_Layout.cshtml* には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれます。 また、ライブラリのTeamsします。

### <a name="controllers"></a>コントローラー

コントローラーは ViewBag プロパティを使用して、値を Views に動的に転送します。

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* プロジェクト ディレクトリのルートでコマンド プロンプトを開き、次のコマンドを実行します。

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

* Ngrok はインターネットからの要求をリッスンし、ポート 44325 で実行されているアプリケーションにルーティングします。  `https://y8rPrT2b.ngrok.io/` *y8rPrT2b* が ngrok の英数字 HTTPS URL に置き換えられる場所に似ている必要があります。

* ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。後で必要になります。

* ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を介してコンテンツ ページに移動して **、ngrok** が正常に実行され、正常に動作されていることを確認します。

> [!TIP]
> このクイック スタートを完了するには、アプリケーションVisual Studio ngrok の両方を実行する必要があります。 アプリケーションの実行を停止する必要がある場合Visual Studio **ngrok を実行し続ける必要があります**。 引き続きリッスンし、アプリケーションの要求がサーバーで再起動されると、アプリケーションの要求のルーティングVisual Studio。 ngrok サービスを再起動する必要がある場合は、新しい URL が返され、その URL を使用する場所を更新する必要があります。

### <a name="run-your-application"></a>アプリケーションを実行する

* [Visual Studio **F5 キーを押するか、****アプリケーションの**[デバッグ] メニューから [デバッグの開始]**を選択** します。

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [カスタム チャネルとグループ タブを作成するには、Node.js と Yeoman Generator を使用Microsoft Teams](~/tabs/quickstarts/create-channel-group-tab-node-yeoman.md)
