---
title: コアを使用して個人用タブを ASP.NET する
author: laujan
description: コアを使用してカスタム個人用タブを作成するクイック スタート ガイド ASP.NET です。
ms.topic: quickstart
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 858175c5afa742d7f2d818204fe1a6f09f6e2245
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020297"
---
# <a name="create-a-personal-tab-with-aspnet-core"></a>コアを使用して個人用タブを ASP.NET する

このクイック スタートでは、Core Razor ページを使用してカスタムの個人用タブC#作成 ASP.Net 説明します。 また、App [Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) を使用してアプリ マニフェストを最終決定し、タブを Teams に展開します。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>ソース コードを取得する

コマンド プロンプトを開き、タブ プロジェクトの新しいディレクトリを作成します。 開始する簡単なプロジェクトを提供しました。 ソース コードを取得するには、zip フォルダーをダウンロードしてファイルを抽出するか、サンプル リポジトリを新しいディレクトリに複製します。

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

ソース コードを取得したら、[プロジェクト] を開Visual Studioプロジェクトまたはソリューションを **開く] を選択します**。 タブ アプリケーション ディレクトリに移動し **、PersonalTab.sln を開きます**。

アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。 ブラウザーで、以下の URL に移動して、アプリケーションが正しく読み込まれているか確認します。

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

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

### <a name="indexcshtml"></a>Index.cshtml

ASP.NET Core は *、Index* と呼ばれるファイルをサイトの既定/ホーム ページとして扱います。 ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。

### <a name="appmanifest-folder"></a>AppManifest フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

- 192 x 192 ピクセルのフル カラー アイコン。 
- **32** x 32 ピクセルの透明なアウトライン アイコン。
- アプリ **manifest.js** を指定するファイルのプロパティです。

これらのファイルは、Teams にタブをアップロードする場合に使用するアプリ パッケージに圧縮する必要があります。 Microsoft Teams は、指定したマニフェストを読み込み、それを iframe <埋め込み、タブ `contentUrl` \> に表示します。

### <a name="csproj"></a>.csproj

[ソリューション エクスプローラー Visual Studioで、プロジェクトを右クリックし、[プロジェクト ファイルの編集] **を選択します**。 ファイルの下部には、アプリケーションのビルド時に zip フォルダーを作成および更新するコードが表示されます。

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

[!INCLUDE  [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- プロジェクト ディレクトリのルートでコマンド プロンプトを開き、次のコマンドを実行します。

```bash
ngrok http https://localhost:44325 -host-header="localhost:44325"
```

- Ngrok はインターネットからの要求をリッスンし、ポート 44325 で実行されているアプリケーションにルーティングします。  `https://y8rPrT2b.ngrok.io/` *y8rPrT2b* が ngrok の英数字 HTTPS URL に置き換えられる場所に似ている必要があります。

- ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。後で必要になります。

- ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を介してコンテンツ ページに移動して *、ngrok* が正常に実行され、正常に動作されていることを確認します。

>[!TIP]
>このクイック スタートを完了するには、アプリケーションVisual Studio ngrok の両方を実行する必要があります。 アプリケーションの実行を停止する必要がある場合は、Visual Studio **ngrok を実行し続ける必要があります**。 引き続きリッスンし、アプリケーションの要求がアプリケーションで再起動されると、アプリケーションの要求のルーティングが再開Visual Studio。 ngrok サービスを再起動する必要がある場合は、新しい URL が返され、その URL を使用する場所を更新する必要があります。

### <a name="run-your-application"></a>アプリケーションを実行する

- [Visual Studio **F5 キーを押** するか **、アプリケーションの** [デバッグ] メニューから [デバッグの開始] **を選択** します。

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
