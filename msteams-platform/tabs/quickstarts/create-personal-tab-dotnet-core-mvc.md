---
title: ASP を使用して個人用タブを作成します。 NET Core MVC
author: surbhigupta
description: ASP を使用してカスタム個人用タブを作成するクイック スタート ガイド。 NET Core MVC。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: ac01ae64f44ccf3e06476d4412b16ac9a4730f6c
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069150"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a><span data-ttu-id="ef4ae-105">MVC を使用してカスタム個人用タブを ASP.NET Coreする</span><span class="sxs-lookup"><span data-stu-id="ef4ae-105">Create a Custom Personal Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="ef4ae-106">このクイック スタートでは、コア MVC を使用してカスタム個人用タブを作成C#を ASP.Net します。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-106">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="ef4ae-107">また、アプリ マニフェストをMicrosoft Teams、アプリ マニフェストにタブを展開するために App [Studio](~/concepts/build-and-test/app-studio-overview.md)をTeams。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-107">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="ef4ae-108">ソース コードを取得する</span><span class="sxs-lookup"><span data-stu-id="ef4ae-108">Get the source code</span></span>

<span data-ttu-id="ef4ae-109">コマンド プロンプトを開き、タブ プロジェクトの新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-109">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="ef4ae-110">開始する簡単なプロジェクトを提供しました。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-110">We have provided a simple project to get you started.</span></span> <span data-ttu-id="ef4ae-111">ソース コードを取得するには、zip フォルダーをダウンロードしてファイルを抽出するか、サンプル リポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-111">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="ef4ae-112">ソース コードを取得したら、[プロジェクト] を開Visual Studioプロジェクトまたはソリューションを開 **く] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-112">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="ef4ae-113">タブ アプリケーション ディレクトリに移動し **、PersonalTabMVC.sln を開きます**。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-113">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="ef4ae-114">アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-114">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="ef4ae-115">ブラウザーで、以下の URL に移動して、アプリケーションが正しく読み込まれたか確認します。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-115">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="ef4ae-116">ソース コードを確認する</span><span class="sxs-lookup"><span data-stu-id="ef4ae-116">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="ef4ae-117">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="ef4ae-117">Startup.cs</span></span>

<span data-ttu-id="ef4ae-118">このプロジェクトは ASP から作成されました。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-118">This project was created from an ASP.</span></span> <span data-ttu-id="ef4ae-119">NET Core 2.2 Web Application 空のテンプレートで、セットアップ時に *[Advanced - Configure for HTTPS]* チェック ボックスがオンになっています。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-119">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="ef4ae-120">MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-120">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="ef4ae-121">さらに、空のテンプレートでは既定では静的コンテンツの配信が有効ではないので、静的ファイル ミドルウェアがメソッドに追加 `Configure()` されます。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-121">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="ef4ae-122">wwwroot フォルダー</span><span class="sxs-lookup"><span data-stu-id="ef4ae-122">wwwroot folder</span></span>

<span data-ttu-id="ef4ae-123">ASP で。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-123">In ASP.</span></span> <span data-ttu-id="ef4ae-124">NET Core、Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-124">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="ef4ae-125">AppManifest フォルダー</span><span class="sxs-lookup"><span data-stu-id="ef4ae-125">AppManifest folder</span></span>

<span data-ttu-id="ef4ae-126">このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-126">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="ef4ae-127">192 x 192 ピクセルのフル カラー アイコン。 </span><span class="sxs-lookup"><span data-stu-id="ef4ae-127">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="ef4ae-128">**32** x 32 ピクセルの透明なアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-128">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="ef4ae-129">アプリ **manifest.js** を指定するファイルのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-129">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="ef4ae-130">これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-130">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="ef4ae-131">Microsoft Teams指定されたマニフェストを読み込み、IFrame に埋め込み、それをタブ `contentUrl` にレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-131">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="ef4ae-132">.csproj</span><span class="sxs-lookup"><span data-stu-id="ef4ae-132">.csproj</span></span>

<span data-ttu-id="ef4ae-133">[ソリューション エクスプローラー Visual Studio] ウィンドウでプロジェクトを右クリックし、[ファイルの編集] Project **します**。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-133">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="ef4ae-134">ファイルの下部には、アプリケーションのビルド時に zip フォルダーを作成および更新するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-134">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="ef4ae-135">モデル</span><span class="sxs-lookup"><span data-stu-id="ef4ae-135">Models</span></span>

<span data-ttu-id="ef4ae-136">**PersonalTab.cs** は、ユーザーが PersonalTab ビューでボタンを選択すると *、PersonalTabController* から呼び出される Message オブジェクトとメソッド **を示** します。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-136">**PersonalTab.cs** presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the **PersonalTab** View.</span></span>

### <a name="views"></a><span data-ttu-id="ef4ae-137">ビュー</span><span class="sxs-lookup"><span data-stu-id="ef4ae-137">Views</span></span>

#### <a name="home"></a><span data-ttu-id="ef4ae-138">ホーム</span><span class="sxs-lookup"><span data-stu-id="ef4ae-138">Home</span></span>

<span data-ttu-id="ef4ae-139">ASP。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-139">ASP.</span></span> <span data-ttu-id="ef4ae-140">NET Core は **、Index** と呼ばれるファイルをサイトの既定またはホーム ページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-140">NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="ef4ae-141">ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-141">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="ef4ae-142">共有</span><span class="sxs-lookup"><span data-stu-id="ef4ae-142">Shared</span></span>

<span data-ttu-id="ef4ae-143">部分ビュー マークアップ *_Layout.cshtml* には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-143">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="ef4ae-144">また、ライブラリのTeamsします。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-144">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="ef4ae-145">コントローラー</span><span class="sxs-lookup"><span data-stu-id="ef4ae-145">Controllers</span></span>

<span data-ttu-id="ef4ae-146">コントローラーは ViewBag プロパティを使用して、値を Views に動的に転送します。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-146">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="ef4ae-147">プロジェクト ディレクトリのルートでコマンド プロンプトを開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-147">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

* <span data-ttu-id="ef4ae-148">Ngrok はインターネットからの要求をリッスンし、ポート 44325 で実行されているアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-148">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="ef4ae-149">`https://y8rPrT2b.ngrok.io/` *y8rPrT2b* が ngrok の英数字 HTTPS URL に置き換えられる場所に似ている必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-149">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="ef4ae-150">ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。後で必要になります。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-150">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="ef4ae-151">ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を介してコンテンツ ページに移動して **、ngrok** が正常に実行され、正常に動作されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-151">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="ef4ae-152">このクイック スタートを完了するには、アプリケーションVisual Studio ngrok の両方を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-152">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="ef4ae-153">アプリケーションの実行を停止する必要がある場合Visual Studio **ngrok を実行し続ける必要があります**。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-153">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="ef4ae-154">引き続きリッスンし、アプリケーションの要求がサーバーで再起動されると、アプリケーションの要求のルーティングVisual Studio。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-154">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="ef4ae-155">ngrok サービスを再起動する必要がある場合は、新しい URL が返され、その URL を使用する場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-155">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="ef4ae-156">アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="ef4ae-156">Run your application</span></span>

* <span data-ttu-id="ef4ae-157">[Visual Studio **F5 キーを押するか、\*\*\*\*アプリケーションの**[デバッグ] メニューから [デバッグの開始]**を選択** します。</span><span class="sxs-lookup"><span data-stu-id="ef4ae-157">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="ef4ae-158">次の手順</span><span class="sxs-lookup"><span data-stu-id="ef4ae-158">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ef4ae-159">カスタム チャネルとグループ タブを作成するには、Node.js と Yeoman Generator を使用Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ef4ae-159">Create a custom channel and group tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>](~/tabs/quickstarts/create-channel-group-tab-node-yeoman.md)
