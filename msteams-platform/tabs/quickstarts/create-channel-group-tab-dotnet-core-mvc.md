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
# <a name="create-a-custom-channel-and-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="dae54-103">コア MVC を使用してカスタム チャネルとグループ ASP.NET を作成する</span><span class="sxs-lookup"><span data-stu-id="dae54-103">Create a Custom Channel and Group Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="dae54-104">このクイック スタートでは、コア MVC を使用してカスタム チャネル/グループ タブを作成C#を ASP.Net します。</span><span class="sxs-lookup"><span data-stu-id="dae54-104">In this quickstart we'll walk-through creating a custom channel/group tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="dae54-105">また、App [Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) を使用してアプリ マニフェストを最終決定し、タブを Teams に展開します。</span><span class="sxs-lookup"><span data-stu-id="dae54-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="dae54-106">ソース コードを取得する</span><span class="sxs-lookup"><span data-stu-id="dae54-106">Get the source code</span></span>

<span data-ttu-id="dae54-107">コマンド プロンプトを開き、タブ プロジェクトの新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="dae54-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="dae54-108">開始する簡単な [チャネル グループ タブ](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) プロジェクトを提供しました。</span><span class="sxs-lookup"><span data-stu-id="dae54-108">We have provided a simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/ChannelGroupTabMVC) project to get you started.</span></span> <span data-ttu-id="dae54-109">ソース コードを取得するには、zip フォルダーをダウンロードしてファイルを抽出するか、サンプル リポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="dae54-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="dae54-110">ソース コードを取得したら、[プロジェクト] を開Visual Studioプロジェクトまたはソリューションを **開く] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="dae54-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="dae54-111">タブ アプリケーション ディレクトリに移動し **、ChannelGroupTabMVC.sln を開きます**。</span><span class="sxs-lookup"><span data-stu-id="dae54-111">Navigate to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>

<span data-ttu-id="dae54-112">アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="dae54-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="dae54-113">ブラウザーで、以下の URL に移動し、アプリケーションが正しく読み込まれたか確認します。</span><span class="sxs-lookup"><span data-stu-id="dae54-113">In a browser, navigate to the URLs below and verify that the application loaded properly:</span></span>

- `http://localhost:44360`
- `http://localhost:44360/privacy`
- `http://localhost:44360/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="dae54-114">ソース コードを確認する</span><span class="sxs-lookup"><span data-stu-id="dae54-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="dae54-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="dae54-115">Startup.cs</span></span>

<span data-ttu-id="dae54-116">このプロジェクトは、コア 2.2 Web アプリケーション ASP.NET テンプレートから作成され、セットアップ時に [ *詳細設定 - HTTPS* の構成] チェック ボックスがオンになっています。</span><span class="sxs-lookup"><span data-stu-id="dae54-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="dae54-117">MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。</span><span class="sxs-lookup"><span data-stu-id="dae54-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="dae54-118">さらに、空のテンプレートでは既定では静的コンテンツの配信が有効ではないので、静的ファイル ミドルウェアがメソッドに追加 `Configure()` されます。</span><span class="sxs-lookup"><span data-stu-id="dae54-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="dae54-119">wwwroot フォルダー</span><span class="sxs-lookup"><span data-stu-id="dae54-119">wwwroot folder</span></span>

<span data-ttu-id="dae54-120">コア ASP.NET Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="dae54-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="dae54-121">AppManifest フォルダー</span><span class="sxs-lookup"><span data-stu-id="dae54-121">AppManifest folder</span></span>

<span data-ttu-id="dae54-122">このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="dae54-122">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="dae54-123">192 x 192 ピクセルのフル カラー アイコン。 </span><span class="sxs-lookup"><span data-stu-id="dae54-123">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="dae54-124">**32** x 32 ピクセルの透明なアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="dae54-124">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="dae54-125">アプリ **manifest.js** を指定するファイルのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="dae54-125">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="dae54-126">これらのファイルは、Teams にタブをアップロードする場合に使用するアプリ パッケージに圧縮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dae54-126">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

### <a name="csproj"></a><span data-ttu-id="dae54-127">.csproj</span><span class="sxs-lookup"><span data-stu-id="dae54-127">.csproj</span></span>

<span data-ttu-id="dae54-128">[ソリューション エクスプローラー Visual Studioでプロジェクトを右クリックし、[プロジェクト ファイルの編集] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="dae54-128">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="dae54-129">ファイルの下部には、アプリケーションのビルド時に zip フォルダーを作成および更新するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="dae54-129">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="dae54-130">モデル</span><span class="sxs-lookup"><span data-stu-id="dae54-130">Models</span></span>

<span data-ttu-id="dae54-131">*ChannelGroup.cs* は、構成中にコントローラーから呼び出される Message オブジェクトとメソッドを示します。</span><span class="sxs-lookup"><span data-stu-id="dae54-131">*ChannelGroup.cs* presents a Message object and methods that will be called from the Controllers during configuration.</span></span>

### <a name="views"></a><span data-ttu-id="dae54-132">ビュー</span><span class="sxs-lookup"><span data-stu-id="dae54-132">Views</span></span>

#### <a name="home"></a><span data-ttu-id="dae54-133">ホーム</span><span class="sxs-lookup"><span data-stu-id="dae54-133">Home</span></span>

<span data-ttu-id="dae54-134">ASP.NET Core は *、Index* と呼ばれるファイルをサイトの既定/ホーム ページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="dae54-134">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="dae54-135">ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="dae54-135">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="dae54-136">共有</span><span class="sxs-lookup"><span data-stu-id="dae54-136">Shared</span></span>

<span data-ttu-id="dae54-137">部分ビュー マークアップ *_Layout.cshtml* には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="dae54-137">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="dae54-138">また、Teams ライブラリも参照します。</span><span class="sxs-lookup"><span data-stu-id="dae54-138">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="dae54-139">コントローラー</span><span class="sxs-lookup"><span data-stu-id="dae54-139">Controllers</span></span>

<span data-ttu-id="dae54-140">コントローラーは ViewBag プロパティを使用して、値を Views に動的に転送します。</span><span class="sxs-lookup"><span data-stu-id="dae54-140">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

- <span data-ttu-id="dae54-141">プロジェクト ディレクトリのルートでコマンド プロンプトを開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="dae54-141">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:443560 -host-header="localhost:44360"
```

- <span data-ttu-id="dae54-142">Ngrok はインターネットからの要求をリッスンし、ポート 44355 で実行されているアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="dae54-142">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span>  <span data-ttu-id="dae54-143">`https://y8rCgT2b.ngrok.io/` *y8rCgT2b* が ngrok の英数字 HTTPS URL に置き換えられる場所に似ている必要があります。</span><span class="sxs-lookup"><span data-stu-id="dae54-143">It should resemble `https://y8rCgT2b.ngrok.io/` where *y8rCgT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="dae54-144">ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。後で必要になります。</span><span class="sxs-lookup"><span data-stu-id="dae54-144">Be sure to keep the command prompt with ngrok running and to make note of the URL — you'll need it later.</span></span>

## <a name="update-your-application"></a><span data-ttu-id="dae54-145">アプリケーションを更新する</span><span class="sxs-lookup"><span data-stu-id="dae54-145">Update your application</span></span>

<span data-ttu-id="dae54-146">**Tab.cshtml 内** では、アプリケーションは、赤または灰色のアイコンでタブを表示するための 2 つのオプション ボタンをユーザーに表示します。</span><span class="sxs-lookup"><span data-stu-id="dae54-146">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="dae54-147">[灰色の **選択] または** **[** 赤の選択] ボタンを選択すると、構成ページの [保存] ボタンが設定され、 `saveGray()` `saveRed()` `settings.setValidityState(true)` 有効になります。 </span><span class="sxs-lookup"><span data-stu-id="dae54-147">Choosing the **Select Gray** or **Select Red** button fires `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="dae54-148">このコードを使用すると、構成要件を満たしていることを Teams に知らされ、インストールを続行できます。</span><span class="sxs-lookup"><span data-stu-id="dae54-148">This code lets Teams know that you have satisfied the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="dae54-149">保存時に、のパラメーターが `settings.setSettings` 設定されます。</span><span class="sxs-lookup"><span data-stu-id="dae54-149">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="dae54-150">最後に、 `saveEvent.notifySuccess()` コンテンツ URL が正常に解決されたことを示すために呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="dae54-150">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

[!INCLUDE [dotnet-upload-to-teams](~/includes/tabs/dotnet-upload-to-teams.md)]
