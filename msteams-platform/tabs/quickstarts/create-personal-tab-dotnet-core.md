---
title: ASP.NET Coreを含む個人用タブを作成する
author: laujan
description: ASP.NET Coreを使用したカスタム 個人用タブの作成に関するクイック スタート ガイドです。
ms.topic: quickstart
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 41aa916f4c69d50e48254d0f4934109429dab83c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566895"
---
# <a name="create-a-personal-tab-using-aspnetcore"></a>ASP.NETCore を使用して個人用タブを作成する

このクイック スタートでは、C# とコア Razor ページを ASP.Net カスタム 個人用タブを作成する手順を説明します。 アプリ マニフェストを完成させ、タブをTeamsするために展開する[Microsoft Teams用にアプリ スタジオ](~/concepts/build-and-test/app-studio-overview.md)も使用します。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>ソース コードを取得する

コマンド プロンプトを開き、タブ プロジェクト用の新しいディレクトリを作成します。 私たちは、あなたが始めるために簡単なプロジェクトを提供しました。 ソースコードを取得するには、zipフォルダをダウンロードしてファイルを抽出するか、サンプルリポジトリを新しいディレクトリに複製します。

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

ソース コードを作成したら、Visual Studio開いて **[プロジェクトまたはソリューションを開く**] を選択します。 タブアプリケーションディレクトリに移動し、 **パーソナルタブ.sln** を開きます。

アプリケーションをビルドして実行するには **、F5 キー** を押すか、[**デバッグ**] メニューから **[デバッグの開始**] を選択します。 ブラウザで、以下の URL に移動して、アプリケーションが正しくロードされていることを確認します。

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a>ソース コードを確認する

### <a name="startupcs"></a>スタートアップ.cs

このプロジェクトは、セットアップ時に **[詳細設定 - HTTPS の構成]** チェック ボックスがオンになっている ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成されました。 MVC サービスは、依存関係挿入フレームワークのメソッドによって登録されます `ConfigureServices()` 。 さらに、空のテンプレートでは、静的コンテンツの提供がデフォルトで有効になっていないため、静的ファイルミドルウェアがメソッドに追加 `Configure()` されます。

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

### <a name="wwwroot-folder"></a>フォルダ

ASP.NET Coreでは、Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。

### <a name="indexcshtml"></a>インデックス.cshtml

ASP.NET Coreは *、Index* という名前のファイルをサイトの既定のホーム ページとして扱います。 ブラウザの URL がサイトのルートを指している場合 **、Index.cshtml** はアプリケーションのホーム ページとして表示されます。

### <a name="appmanifest-folder"></a>アプリ マニフェスト フォルダー

このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。

- 192 x 192 ピクセルの **フルカラーアイコン** です。
- 32 x 32 ピクセルの **透明なアウトライン アイコン** 。
- アプリ **の属性を指定するファイルのmanifest.js。**

これらのファイルは、Teamsにタブをアップロードする際に使用するために、アプリ パッケージに圧縮する必要があります。 Microsoft Teams、マニフェストに指定した値を読み込 `contentUrl` み、それを <iframe に埋め込んで \> 、タブに表示します。

### <a name="csproj"></a>csproj

[ソリューション エクスプローラVisual Studio] ウィンドウで、プロジェクトを右クリックし **、[Project ファイルの編集**] を選択します。 ファイルの下部に、アプリケーションのビルド時に zip フォルダーを作成および更新するコードが表示されます。

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

- Ngrokはインターネットからのリクエストを聞き、ポート44325で実行されているときにアプリケーションにルーティングします。  `https://y8rPrT2b.ngrok.io/`*これは、y8rPrT2b* が ngrok の英数字 HTTPS URL に置き換えられる場所に似ているはずです。

- 必ず、コマンド プロンプトを ngrok で実行し、URL をメモしてください。

- **ngrok** が動作していることを確認するには、ブラウザを開き、コマンド プロンプト ウィンドウで指定された ngrok HTTPS URL を使用してコンテンツ ページに移動します。

>[!TIP]
>このクイック スタートを完了するには、Visual Studioと ngrok の両方のアプリケーションを実行する必要があります。 アプリケーションを操作するためにVisual Studioでアプリケーションの実行を停止する必要がある場合は、 **ngrok を実行したまま** にします。 引き続きリッスンし、Visual Studioで再起動すると、アプリケーションの要求のルーティングを再開します。 ngrokサービスを再起動する必要がある場合は、新しいURLを返し、そのURLを使用するすべての場所を更新する必要があります。

### <a name="run-your-application"></a>アプリケーションを実行する

- **Visual Studio F5** キーを押すか、アプリケーションの **[デバッグ**] メニューから **[デバッグの開始**] を選択します。

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ASP.NETCore MVC を使用してカスタム 個人用タブを作成します。](~/tabs/quickstarts/create-personal-tab-dotnet-core-mvc.md)
