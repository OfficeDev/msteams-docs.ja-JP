---
title: ASP を使用して個人用タブを作成します。 ネットコアMVC
author: laujan
description: ASP を使用したカスタム 個人用タブの作成に関するクイック スタート ガイドです。 ネット コア MVC。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 01418adb32335660bb20f74ecfaa0e7e27230c93
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566631"
---
# <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a><span data-ttu-id="e3287-105">ASP.NET Core MVC を使用してカスタム パーソナル タブを作成する</span><span class="sxs-lookup"><span data-stu-id="e3287-105">Create a Custom Personal Tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="e3287-106">このクイック スタートでは、C# と ASP.Net Core MVC を使用してカスタム 個人用タブを作成する手順を説明します。</span><span class="sxs-lookup"><span data-stu-id="e3287-106">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="e3287-107">アプリ マニフェストを完成させ、タブをTeamsするために展開する[Microsoft Teams用にアプリ スタジオ](~/concepts/build-and-test/app-studio-overview.md)も使用します。</span><span class="sxs-lookup"><span data-stu-id="e3287-107">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="e3287-108">ソース コードを取得する</span><span class="sxs-lookup"><span data-stu-id="e3287-108">Get the source code</span></span>

<span data-ttu-id="e3287-109">コマンド プロンプトを開き、タブ プロジェクト用の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="e3287-109">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="e3287-110">私たちは、あなたが始めるために簡単なプロジェクトを提供しました。</span><span class="sxs-lookup"><span data-stu-id="e3287-110">We have provided a simple project to get you started.</span></span> <span data-ttu-id="e3287-111">ソースコードを取得するには、zipフォルダをダウンロードしてファイルを抽出するか、サンプルリポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="e3287-111">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="e3287-112">ソース コードを作成したら、Visual Studio開いて **[プロジェクトまたはソリューションを開く**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e3287-112">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="e3287-113">タブ アプリケーション ディレクトリに移動し、 **パーソナルタブMVC.sln** を開きます。</span><span class="sxs-lookup"><span data-stu-id="e3287-113">Navigate to the tab application directory and open **PersonalTabMVC.sln**.</span></span>

<span data-ttu-id="e3287-114">アプリケーションをビルドして実行するには **、F5 キー** を押すか、[**デバッグ**] メニューから **[デバッグの開始**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e3287-114">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="e3287-115">ブラウザで、以下の URL に移動して、アプリケーションが正しく読み込まれたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="e3287-115">In a browser navigate to the URLs below to verify that the application loaded properly:</span></span>

* `http://localhost:44335`
* `http://localhost:44335/privacy`
* `http://localhost:44335/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="e3287-116">ソース コードを確認する</span><span class="sxs-lookup"><span data-stu-id="e3287-116">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="e3287-117">スタートアップ.cs</span><span class="sxs-lookup"><span data-stu-id="e3287-117">Startup.cs</span></span>

<span data-ttu-id="e3287-118">このプロジェクトは ASP から作成されました。</span><span class="sxs-lookup"><span data-stu-id="e3287-118">This project was created from an ASP.</span></span> <span data-ttu-id="e3287-119">セットアップ時に *[詳細設定 - HTTPS の構成]* チェック ボックスがオンになっている NET Core 2.2 Web アプリケーションの空のテンプレート。</span><span class="sxs-lookup"><span data-stu-id="e3287-119">NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="e3287-120">MVC サービスは、依存関係挿入フレームワークのメソッドによって登録されます `ConfigureServices()` 。</span><span class="sxs-lookup"><span data-stu-id="e3287-120">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="e3287-121">さらに、空のテンプレートでは、静的コンテンツの提供がデフォルトで有効になっていないため、静的ファイルミドルウェアがメソッドに追加 `Configure()` されます。</span><span class="sxs-lookup"><span data-stu-id="e3287-121">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="e3287-122">フォルダ</span><span class="sxs-lookup"><span data-stu-id="e3287-122">wwwroot folder</span></span>

<span data-ttu-id="e3287-123">ASP で。</span><span class="sxs-lookup"><span data-stu-id="e3287-123">In ASP.</span></span> <span data-ttu-id="e3287-124">NET Core は、アプリケーションが静的ファイルを検索する場所である Web ルート フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="e3287-124">NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="e3287-125">アプリ マニフェスト フォルダー</span><span class="sxs-lookup"><span data-stu-id="e3287-125">AppManifest folder</span></span>

<span data-ttu-id="e3287-126">このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e3287-126">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="e3287-127">192 x 192 ピクセルの **フルカラーアイコン** です。</span><span class="sxs-lookup"><span data-stu-id="e3287-127">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="e3287-128">32 x 32 ピクセルの **透明なアウトライン アイコン** 。</span><span class="sxs-lookup"><span data-stu-id="e3287-128">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="e3287-129">アプリ **の属性を指定するファイルのmanifest.js。**</span><span class="sxs-lookup"><span data-stu-id="e3287-129">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="e3287-130">これらのファイルは、Teamsにタブをアップロードする際に使用するために、アプリ パッケージに圧縮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3287-130">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="e3287-131">Microsoft Teams、マニフェストに指定された値を読み込 `contentUrl` み、IFrame に埋め込んでタブに表示します。</span><span class="sxs-lookup"><span data-stu-id="e3287-131">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="e3287-132">csproj</span><span class="sxs-lookup"><span data-stu-id="e3287-132">.csproj</span></span>

<span data-ttu-id="e3287-133">[Visual Studio ソリューション エクスプローラ] ウィンドウで、プロジェクトを右クリックし **、[Project ファイルの編集**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e3287-133">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="e3287-134">ファイルの下部に、アプリケーションのビルド時に zip フォルダーを作成および更新するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3287-134">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="models"></a><span data-ttu-id="e3287-135">モデル</span><span class="sxs-lookup"><span data-stu-id="e3287-135">Models</span></span>

<span data-ttu-id="e3287-136">**パーソナルタブ.cs** は、ユーザーがパーソナルタブ **ビューで** ボタンを選択したときに *パーソナルタブコントローラ* から呼び出されるメッセージオブジェクトとメソッドを提示します。</span><span class="sxs-lookup"><span data-stu-id="e3287-136">**PersonalTab.cs** presents a Message object and methods that will be called from *PersonalTabController* when a user selects a button in the **PersonalTab** View.</span></span>

### <a name="views"></a><span data-ttu-id="e3287-137">ビュー</span><span class="sxs-lookup"><span data-stu-id="e3287-137">Views</span></span>

#### <a name="home"></a><span data-ttu-id="e3287-138">ホーム</span><span class="sxs-lookup"><span data-stu-id="e3287-138">Home</span></span>

<span data-ttu-id="e3287-139">ASP.</span><span class="sxs-lookup"><span data-stu-id="e3287-139">ASP.</span></span> <span data-ttu-id="e3287-140">NET Core では **、Index** という名前のファイルがサイトの既定のページまたはホーム ページとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="e3287-140">NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="e3287-141">ブラウザの URL がサイトのルートを指している場合 **、Index.cshtml** はアプリケーションのホーム ページとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3287-141">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

#### <a name="shared"></a><span data-ttu-id="e3287-142">共有</span><span class="sxs-lookup"><span data-stu-id="e3287-142">Shared</span></span>

<span data-ttu-id="e3287-143">部分ビュー マークアップ *_Layout.cshtml* には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="e3287-143">The partial view markup *_Layout.cshtml* contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="e3287-144">また、Teams ライブラリも参照します。</span><span class="sxs-lookup"><span data-stu-id="e3287-144">It will also reference the Teams Library.</span></span>

### <a name="controllers"></a><span data-ttu-id="e3287-145">コント ローラー</span><span class="sxs-lookup"><span data-stu-id="e3287-145">Controllers</span></span>

<span data-ttu-id="e3287-146">コントローラは ViewBag プロパティを使用して、値を動的にビューに転送します。</span><span class="sxs-lookup"><span data-stu-id="e3287-146">The controllers use the ViewBag property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="e3287-147">プロジェクト ディレクトリのルートでコマンド プロンプトを開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="e3287-147">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

* <span data-ttu-id="e3287-148">Ngrokはインターネットからのリクエストを聞き、ポート44325で実行されているときにアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="e3287-148">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="e3287-149">`https://y8rPrT2b.ngrok.io/`*これは、y8rPrT2b* が ngrok の英数字 HTTPS URL に置き換えられる場所に似ているはずです。</span><span class="sxs-lookup"><span data-stu-id="e3287-149">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="e3287-150">必ず、コマンド プロンプトを ngrok で実行し、URL をメモしてください。</span><span class="sxs-lookup"><span data-stu-id="e3287-150">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

* <span data-ttu-id="e3287-151">**ngrok** が動作していることを確認するには、ブラウザを開き、コマンド プロンプト ウィンドウで指定された ngrok HTTPS URL を使用してコンテンツ ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="e3287-151">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="e3287-152">このクイック スタートを完了するには、Visual Studioと ngrok の両方のアプリケーションを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3287-152">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="e3287-153">アプリケーションを操作するためにVisual Studioでアプリケーションの実行を停止する必要がある場合は、 **ngrok を実行したまま** にします。</span><span class="sxs-lookup"><span data-stu-id="e3287-153">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="e3287-154">引き続きリッスンし、Visual Studioで再起動すると、アプリケーションの要求のルーティングを再開します。</span><span class="sxs-lookup"><span data-stu-id="e3287-154">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="e3287-155">ngrokサービスを再起動する必要がある場合は、新しいURLを返し、そのURLを使用するすべての場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e3287-155">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="e3287-156">アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="e3287-156">Run your application</span></span>

* <span data-ttu-id="e3287-157">**Visual Studio F5** キーを押すか、アプリケーションの **[デバッグ**] メニューから **[デバッグの開始**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e3287-157">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="e3287-158">次の手順</span><span class="sxs-lookup"><span data-stu-id="e3287-158">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3287-159">Node.jsとYeoman ジェネレータを使用して、カスタムチャネルとグループタブを作成Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e3287-159">Create a custom channel and group tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>](~/tabs/quickstarts/create-channel-group-tab-node-yeoman.md)
