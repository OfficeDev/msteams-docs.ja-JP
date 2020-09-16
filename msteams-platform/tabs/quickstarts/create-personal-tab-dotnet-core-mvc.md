---
title: ASP を使用して、[個人] タブを作成します。 NET Core MVC
author: laujan
description: ASP を使用してカスタムの個人用タブを作成するためのクイックスタートガイド。 NET Core MVC。
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 7fcb0862647dec15bc93eecf9ce637d52892825c
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818914"
---
# <a name="create-a-custom-personal-tab-with-asp-net-core-mvc"></a>ASP を使用して、カスタムの個人用タブを作成します。 NET Core MVC

このクイックスタートでは、C# と ASP を使用して、カスタムの個人用タブを作成する手順を順を追って説明します。 Net Core MVC。 また、 [Microsoft teams 用のアプリ Studio](~/concepts/build-and-test/app-studio-overview.md) を使用して、アプリマニフェストを完成させ、タブを teams に展開します。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>ソースコードを取得する

コマンドプロンプトを開き、タブプロジェクト用の新しいディレクトリを作成します。 開始するための簡単なプロジェクトを提供しています。 ソースコードを取得するには、zip フォルダーをダウンロードして、ファイルを抽出するか、またはサンプルリポジトリを新しいディレクトリに複製します。

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

ソースコードを取得したら、Visual Studio を開き、[ **プロジェクトまたはソリューションを開く**] を選択します。 Tab アプリケーションディレクトリに移動し **、[参照] を開きます**。

アプリケーションをビルドして実行するには、 **F5**キーを押すか、[**デバッグ**] メニューの [**デバッグ開始**] を選択します。 ブラウザーで以下の Url に移動し、アプリケーションが正しく読み込まれたことを確認します。

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a>ソースコードを確認する

### <a name="startupcs"></a>Startup.cs

このプロジェクトは ASP から作成されました。 NET Core 2.2 Web Application の空のテンプレート (セットアップ時に *[HTTPS 用に構成する* ] チェックボックスがオン)。 MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録され `ConfigureServices()` ます。 また、空のテンプレートでは、既定で静的コンテンツの提供が有効になっていないため、このメソッドには静的ファイルミドルウェアが追加され `Configure()` ます。

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

ASP で。 NET Core、web ルートフォルダーはアプリケーションが静的ファイルを検索する場所です。

### <a name="appmanifest-folder"></a>Appmanifest.xml フォルダー

このフォルダーには、次の必要なアプリパッケージファイルが含まれています。

* 192 x 192 ピクセルを測定する **フルカラーアイコン** 。
* 32 x 32 ピクセルを測定する **透明のアウトラインアイコン** 。
* アプリの属性を指定するファイルの **manifest.js** 。

これらのファイルは、タブを Teams にアップロードする際に使用するために、アプリパッケージに圧縮する必要があります。 Microsoft Teams は、 `contentUrl` マニフェストで指定されたを読み込み、それを IFrame に埋め込んで、それをタブに表示します。

### <a name="csproj"></a>.csproj

Visual Studio の [ソリューションエクスプローラー] ウィンドウで、プロジェクトを右クリックし、[ **プロジェクトファイルの編集**] を選択します。 ファイルの末尾に、アプリケーションのビルド時に zip フォルダーを作成して更新するコードが表示されます。

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

*PersonalTab.cs*は、ユーザーが [*パーソナル] タブ*ビューでボタンを選択したときに、そのユーザーを*指定すると*、そのメッセージオブジェクトとメソッドを提供します。

### <a name="views"></a>ビュー

#### <a name="home"></a>Home

.ASP. NET Core は、 *Index* というファイルをサイトの既定のホームページとして扱います。 ブラウザーの URL がサイトのルートを指している場合は、アプリケーションのホームページとして、 *cshtml* が表示されます。

#### <a name="shared"></a>共有

部分的なビューのマークアップ *_Layout* には、アプリケーションの全体的なページ構造と共有のビジュアル要素が含まれています。 Teams ライブラリを参照することもできます。

### <a name="controllers"></a>コントローラー

コントローラーは、ViewBag プロパティを使用して、ビューに値を動的に転送します。

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* プロジェクトディレクトリのルートでコマンドプロンプトを開き、次のコマンドを実行します。

``` bash
ngrok http https://localhost:44345 -host-header="localhost:44345"
```

* Ngrok は、インターネットからの要求をリッスンし、ポート44325上で実行されている場合にそれらをアプリケーションにルーティングします。  `https://y8rPrT2b.ngrok.io/` *Y8rPrT2b*は、ngrok alpha の数字の HTTPS URL に置き換えられる場所に似ているはずです。

* コマンドプロンプトは ngrok を実行したままにしておき、後で必要になるように URL を書き留めておきます。

* ブラウザーを開き、コマンドプロンプトウィンドウで提供された ngrok HTTPS URL を使用してコンテンツページにアクセスすることにより、 *ngrok* が実行されて正常に動作していることを確認します。

> [! ヒントこのクイックスタートを完了するには、Visual Studio と ngrok の両方のアプリケーションを実行している必要があります。 Visual Studio でのアプリケーションの実行を停止する必要がある場合は、 **ngrok の実行を継続**してください。 Visual Studio で再起動すると、アプリケーションの要求のルーティングが続行され、再開されます。 Ngrok サービスを再起動する必要がある場合は、新しい URL を返し、その URL を使用するすべての場所を更新する必要があります。

### <a name="run-your-application"></a>アプリケーションを実行する

* Visual Studio で**F5**キーを押すか、アプリケーションの**デバッグ**メニューから [**デバッグ開始**] を選択します。

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
