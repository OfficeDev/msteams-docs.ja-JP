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
# <a name="create-a-custom-personal-tab-with-asp-net-core-mvc"></a><span data-ttu-id="8a514-105">ASP を使用して、カスタムの個人用タブを作成します。</span><span class="sxs-lookup"><span data-stu-id="8a514-105">Create a Custom Personal Tab with ASP.</span></span> <span data-ttu-id="8a514-106">NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="8a514-106">NET Core MVC</span></span>

<span data-ttu-id="8a514-107">このクイックスタートでは、C# と ASP を使用して、カスタムの個人用タブを作成する手順を順を追って説明します。</span><span class="sxs-lookup"><span data-stu-id="8a514-107">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.</span></span> <span data-ttu-id="8a514-108">Net Core MVC。</span><span class="sxs-lookup"><span data-stu-id="8a514-108">Net Core MVC.</span></span> <span data-ttu-id="8a514-109">また、 [Microsoft teams 用のアプリ Studio](~/concepts/build-and-test/app-studio-overview.md) を使用して、アプリマニフェストを完成させ、タブを teams に展開します。</span><span class="sxs-lookup"><span data-stu-id="8a514-109">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="8a514-110">ソースコードを取得する</span><span class="sxs-lookup"><span data-stu-id="8a514-110">Get the source code</span></span>

<span data-ttu-id="8a514-111">コマンドプロンプトを開き、タブプロジェクト用の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="8a514-111">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="8a514-112">開始するための簡単なプロジェクトを提供しています。</span><span class="sxs-lookup"><span data-stu-id="8a514-112">We have provided a simple project to get you started.</span></span> <span data-ttu-id="8a514-113">ソースコードを取得するには、zip フォルダーをダウンロードして、ファイルを抽出するか、またはサンプルリポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="8a514-113">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="8a514-114">ソースコードを取得したら、Visual Studio を開き、[ **プロジェクトまたはソリューションを開く**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8a514-114">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="8a514-115">Tab アプリケーションディレクトリに移動し **、[参照] を開きます**。</span><span class="sxs-lookup"><span data-stu-id="8a514-115">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="8a514-116">アプリケーションをビルドして実行するには、 **F5**キーを押すか、[**デバッグ**] メニューの [**デバッグ開始**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8a514-116">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="8a514-117">ブラウザーで以下の Url に移動し、アプリケーションが正しく読み込まれたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="8a514-117">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="8a514-118">ソースコードを確認する</span><span class="sxs-lookup"><span data-stu-id="8a514-118">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="8a514-119">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="8a514-119">Startup.cs</span></span>

<span data-ttu-id="8a514-120">このプロジェクトは ASP から作成されました。</span><span class="sxs-lookup"><span data-stu-id="8a514-120">This project was created from an ASP.</span></span> <span data-ttu-id="8a514-121">NET Core 2.2 Web Application の空のテンプレート (セットアップ時に *[HTTPS 用に構成する* ] チェックボックスがオン)。</span><span class="sxs-lookup"><span data-stu-id="8a514-121">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="8a514-122">MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録され `ConfigureServices()` ます。</span><span class="sxs-lookup"><span data-stu-id="8a514-122">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="8a514-123">また、空のテンプレートでは、既定で静的コンテンツの提供が有効になっていないため、このメソッドには静的ファイルミドルウェアが追加され `Configure()` ます。</span><span class="sxs-lookup"><span data-stu-id="8a514-123">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="8a514-124">wwwroot フォルダー</span><span class="sxs-lookup"><span data-stu-id="8a514-124">wwwroot folder</span></span>

<span data-ttu-id="8a514-125">ASP で。</span><span class="sxs-lookup"><span data-stu-id="8a514-125">In ASP.</span></span> <span data-ttu-id="8a514-126">NET Core、web ルートフォルダーはアプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="8a514-126">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="8a514-127">Appmanifest.xml フォルダー</span><span class="sxs-lookup"><span data-stu-id="8a514-127">AppManifest folder</span></span>

<span data-ttu-id="8a514-128">このフォルダーには、次の必要なアプリパッケージファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8a514-128">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="8a514-129">192 x 192 ピクセルを測定する **フルカラーアイコン** 。</span><span class="sxs-lookup"><span data-stu-id="8a514-129">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="8a514-130">32 x 32 ピクセルを測定する **透明のアウトラインアイコン** 。</span><span class="sxs-lookup"><span data-stu-id="8a514-130">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="8a514-131">アプリの属性を指定するファイルの **manifest.js** 。</span><span class="sxs-lookup"><span data-stu-id="8a514-131">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="8a514-132">これらのファイルは、タブを Teams にアップロードする際に使用するために、アプリパッケージに圧縮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8a514-132">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="8a514-133">Microsoft Teams は、 `contentUrl` マニフェストで指定されたを読み込み、それを IFrame に埋め込んで、それをタブに表示します。</span><span class="sxs-lookup"><span data-stu-id="8a514-133">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="8a514-134">.csproj</span><span class="sxs-lookup"><span data-stu-id="8a514-134">.csproj</span></span>

<span data-ttu-id="8a514-135">Visual Studio の [ソリューションエクスプローラー] ウィンドウで、プロジェクトを右クリックし、[ **プロジェクトファイルの編集**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8a514-135">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="8a514-136">ファイルの末尾に、アプリケーションのビルド時に zip フォルダーを作成して更新するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8a514-136">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="8a514-137">モデル</span><span class="sxs-lookup"><span data-stu-id="8a514-137">Models</span></span>

<span data-ttu-id="8a514-138">*PersonalTab.cs*は、ユーザーが [*パーソナル] タブ*ビューでボタンを選択したときに、そのユーザーを*指定すると*、そのメッセージオブジェクトとメソッドを提供します。</span><span class="sxs-lookup"><span data-stu-id="8a514-138">*PersonalTab.cs* presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the *PersonalTab* View.</span></span>

### <a name="views"></a><span data-ttu-id="8a514-139">ビュー</span><span class="sxs-lookup"><span data-stu-id="8a514-139">Views</span></span>

#### <a name="home"></a><span data-ttu-id="8a514-140">Home</span><span class="sxs-lookup"><span data-stu-id="8a514-140">Home</span></span>

<span data-ttu-id="8a514-141">.ASP.</span><span class="sxs-lookup"><span data-stu-id="8a514-141">ASP.</span></span> <span data-ttu-id="8a514-142">NET Core は、 *Index* というファイルをサイトの既定のホームページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="8a514-142">NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="8a514-143">ブラウザーの URL がサイトのルートを指している場合は、アプリケーションのホームページとして、 *cshtml* が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8a514-143">When your browser URL points to the root of the site, *Index.cshtml* will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="8a514-144">共有</span><span class="sxs-lookup"><span data-stu-id="8a514-144">Shared</span></span>

<span data-ttu-id="8a514-145">部分的なビューのマークアップ *_Layout* には、アプリケーションの全体的なページ構造と共有のビジュアル要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8a514-145">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="8a514-146">Teams ライブラリを参照することもできます。</span><span class="sxs-lookup"><span data-stu-id="8a514-146">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="8a514-147">コントローラー</span><span class="sxs-lookup"><span data-stu-id="8a514-147">Controllers</span></span>

<span data-ttu-id="8a514-148">コントローラーは、ViewBag プロパティを使用して、ビューに値を動的に転送します。</span><span class="sxs-lookup"><span data-stu-id="8a514-148">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="8a514-149">プロジェクトディレクトリのルートでコマンドプロンプトを開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="8a514-149">Open a command prompt in the root of your project directory and run the following command:</span></span>

``` bash
ngrok http https://localhost:44345 -host-header="localhost:44345"
```

* <span data-ttu-id="8a514-150">Ngrok は、インターネットからの要求をリッスンし、ポート44325上で実行されている場合にそれらをアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="8a514-150">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="8a514-151">`https://y8rPrT2b.ngrok.io/` *Y8rPrT2b*は、ngrok alpha の数字の HTTPS URL に置き換えられる場所に似ているはずです。</span><span class="sxs-lookup"><span data-stu-id="8a514-151">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="8a514-152">コマンドプロンプトは ngrok を実行したままにしておき、後で必要になるように URL を書き留めておきます。</span><span class="sxs-lookup"><span data-stu-id="8a514-152">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="8a514-153">ブラウザーを開き、コマンドプロンプトウィンドウで提供された ngrok HTTPS URL を使用してコンテンツページにアクセスすることにより、 *ngrok* が実行されて正常に動作していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8a514-153">Verify that *ngrok* is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> <span data-ttu-id="8a514-154">[!</span><span class="sxs-lookup"><span data-stu-id="8a514-154">[!</span></span> <span data-ttu-id="8a514-155">ヒントこのクイックスタートを完了するには、Visual Studio と ngrok の両方のアプリケーションを実行している必要があります。</span><span class="sxs-lookup"><span data-stu-id="8a514-155">TIP] You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="8a514-156">Visual Studio でのアプリケーションの実行を停止する必要がある場合は、 **ngrok の実行を継続**してください。</span><span class="sxs-lookup"><span data-stu-id="8a514-156">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="8a514-157">Visual Studio で再起動すると、アプリケーションの要求のルーティングが続行され、再開されます。</span><span class="sxs-lookup"><span data-stu-id="8a514-157">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="8a514-158">Ngrok サービスを再起動する必要がある場合は、新しい URL を返し、その URL を使用するすべての場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8a514-158">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="8a514-159">アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="8a514-159">Run your application</span></span>

* <span data-ttu-id="8a514-160">Visual Studio で**F5**キーを押すか、アプリケーションの**デバッグ**メニューから [**デバッグ開始**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8a514-160">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
