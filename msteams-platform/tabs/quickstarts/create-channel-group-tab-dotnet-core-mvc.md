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
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="04e1d-103">ASP.NET コア MVC を使用してカスタムのチャネルとグループタブを作成する</span><span class="sxs-lookup"><span data-stu-id="04e1d-103">Create a Custom Channel and Group Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="04e1d-104">このクイックスタートでは、C# および ASP.Net コア MVC を使用して、カスタムのチャネル/グループタブを作成する手順を説明します。</span><span class="sxs-lookup"><span data-stu-id="04e1d-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="04e1d-105">また、 [Microsoft teams 用のアプリ Studio](~/concepts/build-and-test/app-studio-overview.md) を使用して、アプリマニフェストを完成させ、タブを teams に展開します。</span><span class="sxs-lookup"><span data-stu-id="04e1d-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="04e1d-106">ソースコードを取得する</span><span class="sxs-lookup"><span data-stu-id="04e1d-106">Get the source code</span></span>

<span data-ttu-id="04e1d-107">コマンドプロンプトを開き、タブプロジェクト用の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="04e1d-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="04e1d-108">開始するための簡単な [チャネルグループタブ](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) プロジェクトを提供しています。</span><span class="sxs-lookup"><span data-stu-id="04e1d-108">We have provided a simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) project to get you started.</span></span> <span data-ttu-id="04e1d-109">ソースコードを取得するには、zip フォルダーをダウンロードして、ファイルを抽出するか、またはサンプルリポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="04e1d-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="04e1d-110">ソースコードを取得したら、Visual Studio を開き、[ **プロジェクトまたはソリューションを開く**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="04e1d-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="04e1d-111">Tab アプリケーションディレクトリに移動し、[ **Channelgrouptabmvc .sln**] を開きます。</span><span class="sxs-lookup"><span data-stu-id="04e1d-111">Navigate to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>

<span data-ttu-id="04e1d-112">アプリケーションをビルドして実行するには、 **F5**キーを押すか、[**デバッグ**] メニューの [**デバッグ開始**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="04e1d-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="04e1d-113">ブラウザーで以下の Url に移動し、アプリケーションが正しく読み込まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="04e1d-113">In a browser, navigate to the URLs below and verify that the application loaded properly:</span></span>

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="04e1d-114">ソースコードを確認する</span><span class="sxs-lookup"><span data-stu-id="04e1d-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="04e1d-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="04e1d-115">Startup.cs</span></span>

<span data-ttu-id="04e1d-116">このプロジェクトは、セットアップ時に選択されている *[HTTPS の詳細構成* ] チェックボックスがオンになっている ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成されました。</span><span class="sxs-lookup"><span data-stu-id="04e1d-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="04e1d-117">MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録され `ConfigureServices()` ます。</span><span class="sxs-lookup"><span data-stu-id="04e1d-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="04e1d-118">また、空のテンプレートでは、既定で静的コンテンツの提供が有効になっていないため、このメソッドには静的ファイルミドルウェアが追加され `Configure()` ます。</span><span class="sxs-lookup"><span data-stu-id="04e1d-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="04e1d-119">wwwroot フォルダー</span><span class="sxs-lookup"><span data-stu-id="04e1d-119">wwwroot folder</span></span>

<span data-ttu-id="04e1d-120">ASP.NET Core で、web ルートフォルダーはアプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="04e1d-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="04e1d-121">Appmanifest.xml フォルダー</span><span class="sxs-lookup"><span data-stu-id="04e1d-121">AppManifest folder</span></span>

<span data-ttu-id="04e1d-122">このフォルダーには、次の必要なアプリパッケージファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="04e1d-122">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="04e1d-123">192 x 192 ピクセルを測定する **フルカラーアイコン** 。</span><span class="sxs-lookup"><span data-stu-id="04e1d-123">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="04e1d-124">32 x 32 ピクセルを測定する **透明のアウトラインアイコン** 。</span><span class="sxs-lookup"><span data-stu-id="04e1d-124">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="04e1d-125">アプリの属性を指定するファイルの **manifest.js** 。</span><span class="sxs-lookup"><span data-stu-id="04e1d-125">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="04e1d-126">これらのファイルは、タブを Teams にアップロードする際に使用するために、アプリパッケージに圧縮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="04e1d-126">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

### <a name="csproj"></a><span data-ttu-id="04e1d-127">.csproj</span><span class="sxs-lookup"><span data-stu-id="04e1d-127">.csproj</span></span>

<span data-ttu-id="04e1d-128">Visual Studio の [ソリューションエクスプローラー] ウィンドウで、プロジェクトを右クリックし、[ **プロジェクトファイルの編集**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="04e1d-128">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="04e1d-129">ファイルの末尾に、アプリケーションのビルド時に zip フォルダーを作成して更新するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="04e1d-129">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="04e1d-130">モデル</span><span class="sxs-lookup"><span data-stu-id="04e1d-130">Models</span></span>

<span data-ttu-id="04e1d-131">*ChannelGroup.cs* は、構成中にコントローラーから呼び出されるメッセージオブジェクトとメソッドを示しています。</span><span class="sxs-lookup"><span data-stu-id="04e1d-131">*ChannelGroup.cs* presents a Message object and methods that will be called from the Controllers during configuration.</span></span>

### <a name="views"></a><span data-ttu-id="04e1d-132">ビュー</span><span class="sxs-lookup"><span data-stu-id="04e1d-132">Views</span></span>

#### <a name="home"></a><span data-ttu-id="04e1d-133">Home</span><span class="sxs-lookup"><span data-stu-id="04e1d-133">Home</span></span>

<span data-ttu-id="04e1d-134">ASP.NET Core は、 *Index* というファイルをサイトの既定またはホームページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="04e1d-134">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="04e1d-135">ブラウザーの URL がサイトのルートを指している場合は、アプリケーションのホームページとして、 **cshtml** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="04e1d-135">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="04e1d-136">共有</span><span class="sxs-lookup"><span data-stu-id="04e1d-136">Shared</span></span>

<span data-ttu-id="04e1d-137">部分的なビューのマークアップ *_Layout* には、アプリケーションの全体的なページ構造と共有のビジュアル要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="04e1d-137">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="04e1d-138">Teams ライブラリを参照することもできます。</span><span class="sxs-lookup"><span data-stu-id="04e1d-138">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="04e1d-139">コントローラー</span><span class="sxs-lookup"><span data-stu-id="04e1d-139">Controllers</span></span>

<span data-ttu-id="04e1d-140">コントローラーは、ViewBag プロパティを使用して、ビューに値を動的に転送します。</span><span class="sxs-lookup"><span data-stu-id="04e1d-140">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="04e1d-141">プロジェクトディレクトリのルートでコマンドプロンプトを開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="04e1d-141">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- <span data-ttu-id="04e1d-142">Ngrok は、インターネットからの要求をリッスンし、ポート44355上で実行されている場合にそれらをアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="04e1d-142">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span>  <span data-ttu-id="04e1d-143">`https://y8rCgT2b.ngrok.io/` *Y8rCgT2b*は、ngrok alpha の数字の HTTPS URL に置き換えられる場所に似ているはずです。</span><span class="sxs-lookup"><span data-stu-id="04e1d-143">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="04e1d-144">Ngrok を実行していることを確認し、URL をメモするためには、後で必要になるように、コマンドプロンプトを常に使用してください。</span><span class="sxs-lookup"><span data-stu-id="04e1d-144">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="04e1d-145">アプリケーションを更新する</span><span class="sxs-lookup"><span data-stu-id="04e1d-145">Update your application</span></span>

<span data-ttu-id="04e1d-146">**Tab. cshtml**アプリケーションは、赤いアイコンまたは灰色のアイコンでタブを表示するための2つのオプションボタンをユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="04e1d-146">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="04e1d-147">**[灰色]** または **[赤の選択**] ボタンを選択する `saveGray()` と、[構成] ページの [ `saveRed()` `settings.setValidityState(true)` **保存**] ボタンが設定され、有効になります。</span><span class="sxs-lookup"><span data-stu-id="04e1d-147">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="04e1d-148">このコードを使用すると、構成の要件を満たしていることを Teams で認識し、インストールを続行することができます。</span><span class="sxs-lookup"><span data-stu-id="04e1d-148">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="04e1d-149">Save では、のパラメーター `settings.setSettings` が設定されます。</span><span class="sxs-lookup"><span data-stu-id="04e1d-149">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="04e1d-150">最後に、 `saveEvent.notifySuccess()` は、コンテンツ URL が正常に解決されたことを示すためにを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="04e1d-150">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
