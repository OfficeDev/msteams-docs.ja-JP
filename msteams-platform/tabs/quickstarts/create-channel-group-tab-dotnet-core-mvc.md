---
title: Core MVC を使用してチャネルとグループ タブ ASP.NET 作成する
author: laujan
description: コア MVC を使用してカスタム チャネルとグループ タブを作成するクイック ASP.NET ガイド
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 9d89fd98bae9732a8f9e2d34b82d7fc0e6985e01
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020311"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a>コア MVC を使用してカスタム チャネルとグループ ASP.NET を作成する

このクイック スタートでは、コア MVC を使用してカスタム チャネル/グループ タブを作成C#を ASP.Net します。 また、App [Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) を使用してアプリ マニフェストを最終決定し、タブを Teams に展開します。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>ソース コードを取得する

コマンド プロンプトを開き、タブ プロジェクトの新しいディレクトリを作成します。 開始する簡単な [チャネル グループ タブ](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) プロジェクトを提供しました。 ソース コードを取得するには、zip フォルダーをダウンロードしてファイルを抽出するか、サンプル リポジトリを新しいディレクトリに複製します。

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

ソース コードを取得したら、[プロジェクト] を開Visual Studioプロジェクトまたはソリューションを **開く] を選択します**。 タブ アプリケーション ディレクトリに移動し **、ChannelGroupTabMVC.sln を開きます**。

アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。 ブラウザーで、以下の URL に移動し、アプリケーションが正しく読み込まれたか確認します。

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a>ソース コードを確認する

### <a name="startupcs"></a>Startup.cs

このプロジェクトは、コア 2.2 Web アプリケーション ASP.NET テンプレートから作成され、セットアップ時に [ *詳細設定 - HTTPS* の構成] チェック ボックスがオンになっています。 MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。 さらに、空のテンプレートでは既定では静的コンテンツの配信が有効ではないので、静的ファイル ミドルウェアがメソッドに追加 `Configure()` されます。

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

### <a name="wwwroot-folder"></a>wwwroot フォルダー

コア ASP.NET Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

- 192 x 192 ピクセルのフル カラー アイコン。 
- **32** x 32 ピクセルの透明なアウトライン アイコン。
- アプリ **manifest.js** を指定するファイルのプロパティです。

これらのファイルは、Teams にタブをアップロードする場合に使用するアプリ パッケージに圧縮する必要があります。

### <a name="csproj"></a>.csproj

[ソリューション エクスプローラー Visual Studioでプロジェクトを右クリックし、[プロジェクト ファイルの編集] **を選択します**。 ファイルの下部には、アプリケーションのビルド時に zip フォルダーを作成および更新するコードが表示されます。

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

### <a name="models"></a>モデル

*ChannelGroup.cs* は、構成中にコントローラーから呼び出される Message オブジェクトとメソッドを示します。

### <a name="views"></a>ビュー

#### <a name="home"></a>ホーム

ASP.NET Core は *、Index* と呼ばれるファイルをサイトの既定/ホーム ページとして扱います。 ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。

#### <a name="shared"></a>共有

部分ビュー マークアップ *_Layout.cshtml* には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれます。 また、Teams ライブラリも参照します。

### <a name="controllers"></a>コントローラー

コントローラーは ViewBag プロパティを使用して、値を Views に動的に転送します。

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- プロジェクト ディレクトリのルートでコマンド プロンプトを開き、次のコマンドを実行します。

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- Ngrok はインターネットからの要求をリッスンし、ポート 44355 で実行されているアプリケーションにルーティングします。  `https://y8rCgT2b.ngrok.io/` *y8rCgT2b* が ngrok の英数字 HTTPS URL に置き換えられる場所に似ている必要があります。

- ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。後で必要になります。

## <a name="update-your-application"></a>アプリケーションを更新する

**Tab.cshtml 内** では、アプリケーションは、赤または灰色のアイコンでタブを表示するための 2 つのオプション ボタンをユーザーに表示します。 [灰色の **選択] または** **[** 赤の選択] ボタンを選択すると、構成ページの [保存] ボタンが設定され、 `saveGray()` `saveRed()` `settings.setValidityState(true)` 有効になります。  このコードを使用すると、構成要件を満たしていることを Teams に知らされ、インストールを続行できます。 保存時に、のパラメーターが `settings.setSettings` 設定されます。 最後に、 `saveEvent.notifySuccess()` コンテンツ URL が正常に解決されたことを示すために呼び出されます。

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
