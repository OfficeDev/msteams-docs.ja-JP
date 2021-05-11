---
title: ASP を使用して個人用タブを作成します。 NET Core MVC
author: laujan
description: ASP を使用してカスタム個人用タブを作成するクイック スタート ガイド。 NET Core MVC。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 3ec6b5c054384653e30e46cbffed4a2af6662c33
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019567"
---
# <a name="create-a-custom-personal-tab-with-asp-net-core-mvc"></a><span data-ttu-id="acb63-105">ASP を使用してカスタム個人用タブを作成します。</span><span class="sxs-lookup"><span data-stu-id="acb63-105">Create a Custom Personal Tab with ASP.</span></span> <span data-ttu-id="acb63-106">NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="acb63-106">NET Core MVC</span></span>

<span data-ttu-id="acb63-107">このクイック スタートでは、ユーザー設定と ASP を使用してカスタム個人用タブを作成C#説明します。</span><span class="sxs-lookup"><span data-stu-id="acb63-107">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.</span></span> <span data-ttu-id="acb63-108">Net Core MVC。</span><span class="sxs-lookup"><span data-stu-id="acb63-108">Net Core MVC.</span></span> <span data-ttu-id="acb63-109">また、アプリ マニフェストをMicrosoft Teams、アプリ マニフェストにタブを展開するために App [Studio](~/concepts/build-and-test/app-studio-overview.md)をTeams。</span><span class="sxs-lookup"><span data-stu-id="acb63-109">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="acb63-110">ソース コードを取得する</span><span class="sxs-lookup"><span data-stu-id="acb63-110">Get the source code</span></span>

<span data-ttu-id="acb63-111">コマンド プロンプトを開き、タブ プロジェクトの新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="acb63-111">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="acb63-112">開始する簡単なプロジェクトを提供しました。</span><span class="sxs-lookup"><span data-stu-id="acb63-112">We have provided a simple project to get you started.</span></span> <span data-ttu-id="acb63-113">ソース コードを取得するには、zip フォルダーをダウンロードしてファイルを抽出するか、サンプル リポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="acb63-113">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="acb63-114">ソース コードを取得したら、[プロジェクト] を開Visual Studioプロジェクトまたはソリューションを開 **く] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="acb63-114">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="acb63-115">タブ アプリケーション ディレクトリに移動し **、PersonalTabMVC.sln を開きます**。</span><span class="sxs-lookup"><span data-stu-id="acb63-115">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="acb63-116">アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="acb63-116">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="acb63-117">ブラウザーで、以下の URL に移動して、アプリケーションが正しく読み込まれたか確認します。</span><span class="sxs-lookup"><span data-stu-id="acb63-117">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="acb63-118">ソース コードを確認する</span><span class="sxs-lookup"><span data-stu-id="acb63-118">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="acb63-119">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="acb63-119">Startup.cs</span></span>

<span data-ttu-id="acb63-120">このプロジェクトは ASP から作成されました。</span><span class="sxs-lookup"><span data-stu-id="acb63-120">This project was created from an ASP.</span></span> <span data-ttu-id="acb63-121">NET Core 2.2 Web Application 空のテンプレートで、セットアップ時に *[Advanced - Configure for HTTPS]* チェック ボックスがオンになっています。</span><span class="sxs-lookup"><span data-stu-id="acb63-121">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="acb63-122">MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。</span><span class="sxs-lookup"><span data-stu-id="acb63-122">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="acb63-123">さらに、空のテンプレートでは既定では静的コンテンツの配信が有効ではないので、静的ファイル ミドルウェアがメソッドに追加 `Configure()` されます。</span><span class="sxs-lookup"><span data-stu-id="acb63-123">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="acb63-124">wwwroot フォルダー</span><span class="sxs-lookup"><span data-stu-id="acb63-124">wwwroot folder</span></span>

<span data-ttu-id="acb63-125">ASP で。</span><span class="sxs-lookup"><span data-stu-id="acb63-125">In ASP.</span></span> <span data-ttu-id="acb63-126">NET Core、Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="acb63-126">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="acb63-127">AppManifest フォルダー</span><span class="sxs-lookup"><span data-stu-id="acb63-127">AppManifest folder</span></span>

<span data-ttu-id="acb63-128">このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="acb63-128">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="acb63-129">192 x 192 ピクセルのフル カラー アイコン。 </span><span class="sxs-lookup"><span data-stu-id="acb63-129">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="acb63-130">**32** x 32 ピクセルの透明なアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="acb63-130">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="acb63-131">アプリ **manifest.js** を指定するファイルのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="acb63-131">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="acb63-132">これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。</span><span class="sxs-lookup"><span data-stu-id="acb63-132">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="acb63-133">Microsoft Teams指定されたマニフェストを読み込み、IFrame に埋め込み、それをタブ `contentUrl` にレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="acb63-133">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="acb63-134">.csproj</span><span class="sxs-lookup"><span data-stu-id="acb63-134">.csproj</span></span>

<span data-ttu-id="acb63-135">[ソリューション エクスプローラー Visual Studio] ウィンドウでプロジェクトを右クリックし、[ファイルの編集] Project **します**。</span><span class="sxs-lookup"><span data-stu-id="acb63-135">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="acb63-136">ファイルの下部には、アプリケーションのビルド時に zip フォルダーを作成および更新するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="acb63-136">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="acb63-137">モデル</span><span class="sxs-lookup"><span data-stu-id="acb63-137">Models</span></span>

<span data-ttu-id="acb63-138">*PersonalTab.cs* は、ユーザーが PersonalTab ビューでボタンを選択すると *、PersonalTabController* から呼び出される Message オブジェクトとメソッド *を示* します。</span><span class="sxs-lookup"><span data-stu-id="acb63-138">*PersonalTab.cs* presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the *PersonalTab* View.</span></span>

### <a name="views"></a><span data-ttu-id="acb63-139">ビュー</span><span class="sxs-lookup"><span data-stu-id="acb63-139">Views</span></span>

#### <a name="home"></a><span data-ttu-id="acb63-140">ホーム</span><span class="sxs-lookup"><span data-stu-id="acb63-140">Home</span></span>

<span data-ttu-id="acb63-141">ASP。</span><span class="sxs-lookup"><span data-stu-id="acb63-141">ASP.</span></span> <span data-ttu-id="acb63-142">NET Core は *、Index* と呼ばれるファイルをサイトの既定/ホーム ページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="acb63-142">NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="acb63-143">ブラウザーの URL がサイトのルートをポイントすると *、Index.cshtml* がアプリケーションのホーム ページとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="acb63-143">When your browser URL points to the root of the site, *Index.cshtml* will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="acb63-144">共有</span><span class="sxs-lookup"><span data-stu-id="acb63-144">Shared</span></span>

<span data-ttu-id="acb63-145">部分ビュー マークアップ *_Layout.cshtml* には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="acb63-145">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="acb63-146">また、ライブラリのTeamsします。</span><span class="sxs-lookup"><span data-stu-id="acb63-146">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="acb63-147">コントローラー</span><span class="sxs-lookup"><span data-stu-id="acb63-147">Controllers</span></span>

<span data-ttu-id="acb63-148">コントローラーは ViewBag プロパティを使用して、値を Views に動的に転送します。</span><span class="sxs-lookup"><span data-stu-id="acb63-148">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="acb63-149">プロジェクト ディレクトリのルートでコマンド プロンプトを開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="acb63-149">Open a command prompt in the root of your project directory and run the following command:</span></span>

``` bash
ngrok http https://localhost:44345 -host-header="localhost:44345"
```

* <span data-ttu-id="acb63-150">Ngrok はインターネットからの要求をリッスンし、ポート 44325 で実行されているアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="acb63-150">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="acb63-151">`https://y8rPrT2b.ngrok.io/` *y8rPrT2b* が ngrok の英数字 HTTPS URL に置き換えられる場所に似ている必要があります。</span><span class="sxs-lookup"><span data-stu-id="acb63-151">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="acb63-152">ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。後で必要になります。</span><span class="sxs-lookup"><span data-stu-id="acb63-152">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="acb63-153">ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を介してコンテンツ ページに移動して *、ngrok* が正常に実行され、正常に動作されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="acb63-153">Verify that *ngrok* is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> <span data-ttu-id="acb63-154">[!</span><span class="sxs-lookup"><span data-stu-id="acb63-154">[!</span></span> <span data-ttu-id="acb63-155">ヒント] このクイック スタートを完了するには、アプリケーションVisual Studio ngrok の両方を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="acb63-155">TIP] You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="acb63-156">アプリケーションの実行を停止する必要がある場合Visual Studio **ngrok を実行し続ける必要があります**。</span><span class="sxs-lookup"><span data-stu-id="acb63-156">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="acb63-157">引き続きリッスンし、アプリケーションの要求がサーバーで再起動されると、アプリケーションの要求のルーティングVisual Studio。</span><span class="sxs-lookup"><span data-stu-id="acb63-157">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="acb63-158">ngrok サービスを再起動する必要がある場合は、新しい URL が返され、その URL を使用する場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="acb63-158">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="acb63-159">アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="acb63-159">Run your application</span></span>

* <span data-ttu-id="acb63-160">[Visual Studio **F5 キーを押するか、\*\*\*\*アプリケーションの**[デバッグ] メニューから [デバッグの開始]**を選択** します。</span><span class="sxs-lookup"><span data-stu-id="acb63-160">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
