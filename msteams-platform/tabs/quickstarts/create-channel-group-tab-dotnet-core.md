---
title: '[チャネルとグループ] タブを作成 ASP.NET Coreする'
author: laujan
description: カスタム チャネルとグループ タブを作成するクイック スタート ガイドとグループ ASP.NET Core。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 8271e2d225d5ae3f6458b17b9595c4d23c3ca6c9
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019574"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core"></a>カスタム チャネルとグループ タブを作成するには、ASP.NET Core

このクイック スタートでは、カスタム チャネル/グループ タブを作成し、[コア C#] ページ ASP.Net 作成します。 また、アプリ マニフェストをMicrosoft Teams、アプリ マニフェストにタブを展開するために App [Studio](~/concepts/build-and-test/app-studio-overview.md)をTeams。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>ソース コードを取得する

コマンド プロンプトを開き、タブ プロジェクトの新しいディレクトリを作成します。 開始する簡単なプロジェクトを提供しました。 ソース コードを取得するには、zip フォルダーをダウンロードしてファイルを抽出するか、サンプル リポジトリを新しいディレクトリに複製します。

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

ソース コードを取得したら、[プロジェクト] を開Visual Studioプロジェクトまたはソリューションを開 **く] を選択します**。 タブ アプリケーション ディレクトリに移動し **、ChannelGroupTab.sln を開きます**。

アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。 ブラウザーで、以下の URL に移動し、アプリケーションが正しく読み込まれているか確認します。

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a>ソース コードを確認する

### <a name="startupcs"></a>Startup.cs

このプロジェクトは、ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成され、セットアップ時に [詳細設定 *- HTTPS* 用に構成] チェック ボックスがオンになっています。 MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。 さらに、空のテンプレートでは既定では静的コンテンツの配信が有効ではないので、静的ファイル ミドルウェアがメソッドに追加 `Configure()` されます。

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

この ASP.NET Core Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core Index と呼ばれるファイルをサイトの既定/ホーム ページとして扱います。 ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。

### <a name="tabcs"></a>Tab.cs

このC#ファイルには、構成時に **Tab.cshtml** から呼び出されるメソッドが含まれる。

### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

- 192 x 192 ピクセルのフル カラー アイコン。 
- **32** x 32 ピクセルの透明なアウトライン アイコン。
- アプリ **manifest.js** を指定するファイルのプロパティです。

これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。 ユーザーがタブの追加または更新を選択すると、Microsoft Teams は指定したマニフェストを読み込み、IFrame に埋め込み、タブに `configurationUrl` 表示します。

### <a name="csproj"></a>.csproj

[ソリューション エクスプローラー Visual Studio] ウィンドウでプロジェクトを右クリックし、[ファイルの編集] Project **します**。 ファイルの下部には、アプリケーションのビルド時に zip フォルダーを作成および更新するコードが表示されます。

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

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- プロジェクト ディレクトリのルートでコマンド プロンプトを開き、次のコマンドを実行します。

```bash
ngrok http https://localhost:44355 -host-header="localhost:44355"
```

- Ngrok はインターネットからの要求をリッスンし、ポート 44355 で実行されているアプリケーションにルーティングします。 `https://y8rCgT2b.ngrok.io/` *y8rCgT2b* が ngrok の英数字 HTTPS URL に置き換えられる場所に似ている必要があります。

- ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。後で必要になります。

## <a name="update-your-application"></a>アプリケーションを更新する

*Tab.cshtml 内* では、アプリケーションは、赤または灰色のアイコンでタブを表示するための 2 つのオプション ボタンをユーザーに表示します。 [灰色の **選択] または** **[** 赤の選択] ボタンを選択すると、構成ページの [保存] ボタンが設定され、 `saveGray()` `saveRed()` `settings.setValidityState(true)` 有効になります。  このコードではTeams要件を満たしていることを確認し、インストールを続行できます。 保存時に、のパラメーターが `settings.setSettings` 設定されます。 最後に、 `saveEvent.notifySuccess()` コンテンツ URL が正常に解決されたことを示すために呼び出されます。

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

