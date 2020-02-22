---
title: ASP.NET Core を使用して [チャネルとグループ] タブを作成する
author: laujan
description: ASP.NET コアを使用してカスタムチャネルおよびグループタブを作成するためのクイックスタートガイド。
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 47a0c98d630501944c7a5f4baf4620dbb70cdbcd
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228011"
---
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core"></a><span data-ttu-id="e8480-103">ASP.NET Core を使用してカスタムのチャネルとグループタブを作成する</span><span class="sxs-lookup"><span data-stu-id="e8480-103">Create a Custom Channel and Group Tab with ASP.NET Core</span></span>

<span data-ttu-id="e8480-104">このクイックスタートでは、C# および ASP.Net コアの Razor ページを使用して、カスタムのチャネル/グループタブを作成する手順を説明します。</span><span class="sxs-lookup"><span data-stu-id="e8480-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core Razor page.</span></span> <span data-ttu-id="e8480-105">また、 [Microsoft teams 用のアプリ Studio](~/concepts/build-and-test/app-studio-overview.md)を使用して、アプリマニフェストを完成させ、タブを teams に展開します。</span><span class="sxs-lookup"><span data-stu-id="e8480-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="e8480-106">ソースコードを取得する</span><span class="sxs-lookup"><span data-stu-id="e8480-106">Get the source code</span></span>

<span data-ttu-id="e8480-107">コマンドプロンプトを開き、タブプロジェクト用の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="e8480-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="e8480-108">開始するための簡単なプロジェクトを提供しています。</span><span class="sxs-lookup"><span data-stu-id="e8480-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="e8480-109">ソースコードを取得するには、zip フォルダーをダウンロードして、ファイルを抽出するか、またはサンプルリポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="e8480-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="e8480-110">ソースコードを取得したら、Visual Studio を開き、[**プロジェクトまたはソリューションを開く**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e8480-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="e8480-111">Tab アプリケーションディレクトリに移動し、[ **Channelgrouptab] .sln**を開きます。</span><span class="sxs-lookup"><span data-stu-id="e8480-111">Navigate to the tab application directory and open **ChannelGroupTab.sln**.</span></span>

<span data-ttu-id="e8480-112">アプリケーションをビルドして実行するには、 **F5**キーを押すか、[**デバッグ**] メニューの [**デバッグ開始**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e8480-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="e8480-113">ブラウザーで以下の Url に移動し、アプリケーションが正しく読み込まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e8480-113">In a browser navigate to the URLs below and verify the application loaded properly:</span></span>

- `http://localhost:44355`
- `http://localhost:44355/privacy`
- `http://localhost:44355/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="e8480-114">ソースコードを確認する</span><span class="sxs-lookup"><span data-stu-id="e8480-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="e8480-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="e8480-115">Startup.cs</span></span>

<span data-ttu-id="e8480-116">このプロジェクトは、セットアップ時に選択されている *[HTTPS の詳細構成*] チェックボックスがオンになっている ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成されました。</span><span class="sxs-lookup"><span data-stu-id="e8480-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="e8480-117">MVC サービスは、依存関係の挿入フレームワークの`ConfigureServices()`メソッドによって登録されます。</span><span class="sxs-lookup"><span data-stu-id="e8480-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="e8480-118">また、空のテンプレートでは、既定で静的コンテンツの提供が有効になっていないため`Configure()` 、このメソッドには静的ファイルミドルウェアが追加されます。</span><span class="sxs-lookup"><span data-stu-id="e8480-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="e8480-119">wwwroot フォルダー</span><span class="sxs-lookup"><span data-stu-id="e8480-119">wwwroot folder</span></span>

<span data-ttu-id="e8480-120">ASP.NET Core で、web ルートフォルダーはアプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="e8480-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="e8480-121">インデックス. cshtml</span><span class="sxs-lookup"><span data-stu-id="e8480-121">Index.cshtml</span></span>

<span data-ttu-id="e8480-122">ASP.NET Core は、 *Index*というファイルをサイトの既定またはホームページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="e8480-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="e8480-123">ブラウザーの URL がサイトのルートを指している場合は、アプリケーションのホームページとして、 **cshtml**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e8480-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="tabcs"></a><span data-ttu-id="e8480-124">Tab.cs</span><span class="sxs-lookup"><span data-stu-id="e8480-124">Tab.cs</span></span>

<span data-ttu-id="e8480-125">この C# ファイルには、構成中に Tab から呼び出されるメソッドが含まれてい**ます。**</span><span class="sxs-lookup"><span data-stu-id="e8480-125">This C# file contains a method that will be called from **Tab.cshtml** during configuration.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="e8480-126">Appmanifest.xml フォルダー</span><span class="sxs-lookup"><span data-stu-id="e8480-126">AppManifest folder</span></span>

<span data-ttu-id="e8480-127">このフォルダーには、次の必要なアプリパッケージファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e8480-127">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="e8480-128">192 x 192 ピクセルを測定する**フルカラーアイコン**。</span><span class="sxs-lookup"><span data-stu-id="e8480-128">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="e8480-129">32 x 32 ピクセルを測定する**透明のアウトラインアイコン**。</span><span class="sxs-lookup"><span data-stu-id="e8480-129">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="e8480-130">アプリの属性を指定する**manifest.xml**ファイル。</span><span class="sxs-lookup"><span data-stu-id="e8480-130">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="e8480-131">これらのファイルは、タブを Teams にアップロードする際に使用するために、アプリパッケージに圧縮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8480-131">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="e8480-132">ユーザーがタブを追加または更新することを選択すると、Microsoft `configurationUrl` Teams はマニフェストに指定されたを読み込み、それを IFrame に埋め込んで、それをタブに表示します。</span><span class="sxs-lookup"><span data-stu-id="e8480-132">When a user chooses to add or update your tab, Microsoft Teams will load the `configurationUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="e8480-133">.csproj</span><span class="sxs-lookup"><span data-stu-id="e8480-133">.csproj</span></span>

<span data-ttu-id="e8480-134">Visual Studio の [ソリューションエクスプローラー] ウィンドウで、プロジェクトを右クリックし、[**プロジェクトファイルの編集**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e8480-134">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="e8480-135">ファイルの末尾に、アプリケーションのビルド時に zip フォルダーを作成して更新するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e8480-135">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="e8480-136">プロジェクトディレクトリのルートでコマンドプロンプトを開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="e8480-136">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:44355 -host-header="localhost:44355"
```

- <span data-ttu-id="e8480-137">Ngrok は、インターネットからの要求をリッスンし、ポート44355上で実行されている場合にそれらをアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="e8480-137">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span> <span data-ttu-id="e8480-138">Y8rCgT2b は、 `https://y8rCgT2b.ngrok.io/` ngrok \*\* ALPHA の数字の HTTPS URL に置き換えられる場所に似ているはずです。</span><span class="sxs-lookup"><span data-stu-id="e8480-138">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="e8480-139">Ngrok を実行していることを確認し、URL をメモするためには、後で必要になるように、コマンドプロンプトを常に使用してください。</span><span class="sxs-lookup"><span data-stu-id="e8480-139">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="e8480-140">アプリケーションを更新する</span><span class="sxs-lookup"><span data-stu-id="e8480-140">Update your application</span></span>

<span data-ttu-id="e8480-141">*Tab. cshtml*アプリケーションは、赤いアイコンまたは灰色のアイコンでタブを表示するための2つのオプションボタンをユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="e8480-141">Within *Tab.cshtml* the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="e8480-142">**[灰色]** または **[赤**の選択`saveGray()` ] `saveRed()`ボタンを選択する`settings.setValidityState(true)`と、[構成] ページの [**保存**] ボタンが設定され、有効になります。</span><span class="sxs-lookup"><span data-stu-id="e8480-142">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="e8480-143">このコードを使用すると、構成の要件を満たしていることを Teams で認識し、インストールを続行することができます。</span><span class="sxs-lookup"><span data-stu-id="e8480-143">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="e8480-144">Save では、の`settings.setSettings`パラメーターが設定されます。</span><span class="sxs-lookup"><span data-stu-id="e8480-144">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="e8480-145">最後に`saveEvent.notifySuccess()` 、は、コンテンツ URL が正常に解決されたことを示すためにを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="e8480-145">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

