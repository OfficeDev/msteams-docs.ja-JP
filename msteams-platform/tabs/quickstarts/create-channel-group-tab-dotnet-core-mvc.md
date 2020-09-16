---
title: ASP.NET コア MVC を使用して [チャネルとグループ] タブを作成する
author: laujan
description: ASP.NET コア MVC を使用してカスタムチャネルおよびグループタブを作成するためのクイックスタートガイド。
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: cda91825ee37da94ee84747c5d2439c2940c728b
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818928"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a>ASP.NET コア MVC を使用してカスタムのチャネルとグループタブを作成する

このクイックスタートでは、C# および ASP.Net コア MVC を使用して、カスタムのチャネル/グループタブを作成する手順を説明します。 また、 [Microsoft teams 用のアプリ Studio](~/concepts/build-and-test/app-studio-overview.md) を使用して、アプリマニフェストを完成させ、タブを teams に展開します。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>ソースコードを取得する

コマンドプロンプトを開き、タブプロジェクト用の新しいディレクトリを作成します。 開始するための簡単な [チャネルグループタブ](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) プロジェクトを提供しています。 ソースコードを取得するには、zip フォルダーをダウンロードして、ファイルを抽出するか、またはサンプルリポジトリを新しいディレクトリに複製します。

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

ソースコードを取得したら、Visual Studio を開き、[ **プロジェクトまたはソリューションを開く**] を選択します。 Tab アプリケーションディレクトリに移動し、[ **Channelgrouptabmvc .sln**] を開きます。

アプリケーションをビルドして実行するには、 **F5**キーを押すか、[**デバッグ**] メニューの [**デバッグ開始**] を選択します。 ブラウザーで以下の Url に移動し、アプリケーションが正しく読み込まれていることを確認します。

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a>ソースコードを確認する

### <a name="startupcs"></a>Startup.cs

このプロジェクトは、セットアップ時に選択されている *[HTTPS の詳細構成* ] チェックボックスがオンになっている ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成されました。 MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録され `ConfigureServices()` ます。 また、空のテンプレートでは、既定で静的コンテンツの提供が有効になっていないため、このメソッドには静的ファイルミドルウェアが追加され `Configure()` ます。

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

ASP.NET Core で、web ルートフォルダーはアプリケーションが静的ファイルを検索する場所です。

### <a name="appmanifest-folder"></a>Appmanifest.xml フォルダー

このフォルダーには、次の必要なアプリパッケージファイルが含まれています。

- 192 x 192 ピクセルを測定する **フルカラーアイコン** 。
- 32 x 32 ピクセルを測定する **透明のアウトラインアイコン** 。
- アプリの属性を指定するファイルの **manifest.js** 。

これらのファイルは、タブを Teams にアップロードする際に使用するために、アプリパッケージに圧縮する必要があります。

### <a name="csproj"></a>.csproj

Visual Studio の [ソリューションエクスプローラー] ウィンドウで、プロジェクトを右クリックし、[ **プロジェクトファイルの編集**] を選択します。 ファイルの末尾に、アプリケーションのビルド時に zip フォルダーを作成して更新するコードが表示されます。

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

*ChannelGroup.cs* は、構成中にコントローラーから呼び出されるメッセージオブジェクトとメソッドを示しています。

### <a name="views"></a>ビュー

#### <a name="home"></a>Home

ASP.NET Core は、 *Index* というファイルをサイトの既定またはホームページとして扱います。 ブラウザーの URL がサイトのルートを指している場合は、アプリケーションのホームページとして、 **cshtml** が表示されます。

#### <a name="shared"></a>共有

部分的なビューのマークアップ *_Layout* には、アプリケーションの全体的なページ構造と共有のビジュアル要素が含まれています。 Teams ライブラリを参照することもできます。

### <a name="controllers"></a>コントローラー

コントローラーは、ViewBag プロパティを使用して、ビューに値を動的に転送します。

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- プロジェクトディレクトリのルートでコマンドプロンプトを開き、次のコマンドを実行します。

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- Ngrok は、インターネットからの要求をリッスンし、ポート44355上で実行されている場合にそれらをアプリケーションにルーティングします。  `https://y8rCgT2b.ngrok.io/` *Y8rCgT2b*は、ngrok alpha の数字の HTTPS URL に置き換えられる場所に似ているはずです。

- Ngrok を実行していることを確認し、URL をメモするためには、後で必要になるように、コマンドプロンプトを常に使用してください。

## <a name="update-your-application"></a>アプリケーションを更新する

**Tab. cshtml**アプリケーションは、赤いアイコンまたは灰色のアイコンでタブを表示するための2つのオプションボタンをユーザーに提供します。 **[灰色]** または **[赤の選択**] ボタンを選択する `saveGray()` と、[構成] ページの [ `saveRed()` `settings.setValidityState(true)` **保存**] ボタンが設定され、有効になります。 このコードを使用すると、構成の要件を満たしていることを Teams で認識し、インストールを続行することができます。 Save では、のパラメーター `settings.setSettings` が設定されます。 最後に、 `saveEvent.notifySuccess()` は、コンテンツ URL が正常に解決されたことを示すためにを呼び出します。

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
