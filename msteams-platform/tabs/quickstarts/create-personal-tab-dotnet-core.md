---
title: ASP.NET Core を使用して [個人用] タブを作成する
author: laujan
description: ASP.NET コアを使用してカスタムの個人用タブを作成するためのクイックスタートガイド。
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 3eb0c42bb81ec8b2d906863051bd551c88c35f57
ms.sourcegitcommit: fdb53284a20285f7e8a7daf25e85cb5d06c52b95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "48992632"
---
# <a name="create-a-personal-tab-with-aspnet-core"></a>ASP.NET Core を使用して [個人用] タブを作成する

このクイックスタートでは、C# と ASP.Net コアの Razor ページを使用して、カスタムの個人用タブを作成する手順を説明します。 また、 [Microsoft teams 用のアプリ Studio](~/concepts/build-and-test/app-studio-overview.md) を使用して、アプリマニフェストを完成させ、タブを teams に展開します。

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a>ソースコードを取得する

コマンドプロンプトを開き、タブプロジェクト用の新しいディレクトリを作成します。 開始するための簡単なプロジェクトを提供しています。 ソースコードを取得するには、zip フォルダーをダウンロードして、ファイルを抽出するか、またはサンプルリポジトリを新しいディレクトリに複製します。

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

ソースコードを取得したら、Visual Studio を開き、[ **プロジェクトまたはソリューションを開く** ] を選択します。 Tab アプリケーションディレクトリに移動して、"独自のタブを開く" という名前の **.sln** を開きます。

アプリケーションをビルドして実行するには、 **F5** キーを押すか、[ **デバッグ** ] メニューの [ **デバッグ開始** ] を選択します。 ブラウザーで以下の Url に移動し、アプリケーションが正しく読み込まれていることを確認します。

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

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

### <a name="indexcshtml"></a>インデックス. cshtml

ASP.NET Core は、 *Index* というファイルをサイトの既定またはホームページとして扱います。 ブラウザーの URL がサイトのルートを指している場合は、アプリケーションのホームページとして、 **cshtml** が表示されます。

### <a name="appmanifest-folder"></a>Appmanifest.xml フォルダー

このフォルダーには、次の必要なアプリパッケージファイルが含まれています。

- 192 x 192 ピクセルを測定する **フルカラーアイコン** 。
- 32 x 32 ピクセルを測定する **透明のアウトラインアイコン** 。
- アプリの属性を指定するファイルの **manifest.js** 。

これらのファイルは、タブを Teams にアップロードする際に使用するために、アプリパッケージに圧縮する必要があります。 Microsoft Teams は、 `contentUrl` マニフェストで指定されたを読み込み、それを IFrame に埋め込んで、それをタブに表示します。

### <a name="csproj"></a>.csproj

Visual Studio の [ソリューションエクスプローラー] ウィンドウで、プロジェクトを右クリックし、[ **プロジェクトファイルの編集** ] を選択します。 ファイルの末尾に、アプリケーションのビルド時に zip フォルダーを作成して更新するコードが表示されます。

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

- プロジェクトディレクトリのルートでコマンドプロンプトを開き、次のコマンドを実行します。

```bash
ngrok http https://localhost:44325 -host-header="localhost:44325"
```

- Ngrok は、インターネットからの要求をリッスンし、ポート44325上で実行されている場合にそれらをアプリケーションにルーティングします。  `https://y8rPrT2b.ngrok.io/` *Y8rPrT2b* は、ngrok alpha の数字の HTTPS URL に置き換えられる場所に似ているはずです。

- コマンドプロンプトは ngrok を実行したままにしておき、後で必要になるように URL を書き留めておきます。

- ブラウザーを開き、コマンドプロンプトウィンドウで提供された ngrok HTTPS URL を使用してコンテンツページにアクセスすることにより、 *ngrok* が実行されて正常に動作していることを確認します。

>[!TIP]
>このクイックスタートを完了するには、Visual Studio と ngrok の両方のアプリケーションが実行されている必要があります。 Visual Studio でのアプリケーションの実行を停止する必要がある場合は、 **ngrok の実行を継続** してください。 Visual Studio で再起動すると、アプリケーションの要求のルーティングが続行され、再開されます。 Ngrok サービスを再起動する必要がある場合は、新しい URL を返し、その URL を使用するすべての場所を更新する必要があります。

### <a name="run-your-application"></a>アプリケーションを実行する

- Visual Studio で **F5** キーを押すか、アプリケーションの **デバッグ** メニューから [ **デバッグ開始** ] を選択します。

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
