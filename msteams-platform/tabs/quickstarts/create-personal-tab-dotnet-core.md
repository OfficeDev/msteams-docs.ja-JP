---
title: ASP.NET Coreを含む個人用タブを作成する
author: laujan
description: ASP.NET Coreを使用したカスタム 個人用タブの作成に関するクイック スタート ガイドです。
ms.topic: quickstart
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 41aa916f4c69d50e48254d0f4934109429dab83c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566895"
---
# <a name="create-a-personal-tab-using-aspnetcore"></a><span data-ttu-id="2143b-103">ASP.NETCore を使用して個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="2143b-103">Create a personal tab using ASP.NETCore</span></span>

<span data-ttu-id="2143b-104">このクイック スタートでは、C# とコア Razor ページを ASP.Net カスタム 個人用タブを作成する手順を説明します。</span><span class="sxs-lookup"><span data-stu-id="2143b-104">In this quickstart, we'll walk-through creating a custom personal tab with C# and ASP.Net Core Razor pages.</span></span> <span data-ttu-id="2143b-105">アプリ マニフェストを完成させ、タブをTeamsするために展開する[Microsoft Teams用にアプリ スタジオ](~/concepts/build-and-test/app-studio-overview.md)も使用します。</span><span class="sxs-lookup"><span data-stu-id="2143b-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="2143b-106">ソース コードを取得する</span><span class="sxs-lookup"><span data-stu-id="2143b-106">Get the source code</span></span>

<span data-ttu-id="2143b-107">コマンド プロンプトを開き、タブ プロジェクト用の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="2143b-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="2143b-108">私たちは、あなたが始めるために簡単なプロジェクトを提供しました。</span><span class="sxs-lookup"><span data-stu-id="2143b-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="2143b-109">ソースコードを取得するには、zipフォルダをダウンロードしてファイルを抽出するか、サンプルリポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="2143b-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="2143b-110">ソース コードを作成したら、Visual Studio開いて **[プロジェクトまたはソリューションを開く**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2143b-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="2143b-111">タブアプリケーションディレクトリに移動し、 **パーソナルタブ.sln** を開きます。</span><span class="sxs-lookup"><span data-stu-id="2143b-111">Navigate to the tab application directory and open **PersonalTab.sln**.</span></span>

<span data-ttu-id="2143b-112">アプリケーションをビルドして実行するには **、F5 キー** を押すか、[**デバッグ**] メニューから **[デバッグの開始**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2143b-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="2143b-113">ブラウザで、以下の URL に移動して、アプリケーションが正しくロードされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="2143b-113">In a browser navigate to the URLs below to verify the application loaded properly:</span></span>

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="2143b-114">ソース コードを確認する</span><span class="sxs-lookup"><span data-stu-id="2143b-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="2143b-115">スタートアップ.cs</span><span class="sxs-lookup"><span data-stu-id="2143b-115">Startup.cs</span></span>

<span data-ttu-id="2143b-116">このプロジェクトは、セットアップ時に **[詳細設定 - HTTPS の構成]** チェック ボックスがオンになっている ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成されました。</span><span class="sxs-lookup"><span data-stu-id="2143b-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="2143b-117">MVC サービスは、依存関係挿入フレームワークのメソッドによって登録されます `ConfigureServices()` 。</span><span class="sxs-lookup"><span data-stu-id="2143b-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="2143b-118">さらに、空のテンプレートでは、静的コンテンツの提供がデフォルトで有効になっていないため、静的ファイルミドルウェアがメソッドに追加 `Configure()` されます。</span><span class="sxs-lookup"><span data-stu-id="2143b-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="2143b-119">フォルダ</span><span class="sxs-lookup"><span data-stu-id="2143b-119">wwwroot folder</span></span>

<span data-ttu-id="2143b-120">ASP.NET Coreでは、Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="2143b-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="2143b-121">インデックス.cshtml</span><span class="sxs-lookup"><span data-stu-id="2143b-121">Index.cshtml</span></span>

<span data-ttu-id="2143b-122">ASP.NET Coreは *、Index* という名前のファイルをサイトの既定のホーム ページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="2143b-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="2143b-123">ブラウザの URL がサイトのルートを指している場合 **、Index.cshtml** はアプリケーションのホーム ページとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="2143b-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="2143b-124">アプリ マニフェスト フォルダー</span><span class="sxs-lookup"><span data-stu-id="2143b-124">AppManifest folder</span></span>

<span data-ttu-id="2143b-125">このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="2143b-125">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="2143b-126">192 x 192 ピクセルの **フルカラーアイコン** です。</span><span class="sxs-lookup"><span data-stu-id="2143b-126">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="2143b-127">32 x 32 ピクセルの **透明なアウトライン アイコン** 。</span><span class="sxs-lookup"><span data-stu-id="2143b-127">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="2143b-128">アプリ **の属性を指定するファイルのmanifest.js。**</span><span class="sxs-lookup"><span data-stu-id="2143b-128">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="2143b-129">これらのファイルは、Teamsにタブをアップロードする際に使用するために、アプリ パッケージに圧縮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2143b-129">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="2143b-130">Microsoft Teams、マニフェストに指定した値を読み込 `contentUrl` み、それを <iframe に埋め込んで \> 、タブに表示します。</span><span class="sxs-lookup"><span data-stu-id="2143b-130">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an <iframe\>, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="2143b-131">csproj</span><span class="sxs-lookup"><span data-stu-id="2143b-131">.csproj</span></span>

<span data-ttu-id="2143b-132">[ソリューション エクスプローラVisual Studio] ウィンドウで、プロジェクトを右クリックし **、[Project ファイルの編集**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2143b-132">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="2143b-133">ファイルの下部に、アプリケーションのビルド時に zip フォルダーを作成および更新するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2143b-133">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="2143b-134">プロジェクト ディレクトリのルートでコマンド プロンプトを開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="2143b-134">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

- <span data-ttu-id="2143b-135">Ngrokはインターネットからのリクエストを聞き、ポート44325で実行されているときにアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="2143b-135">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="2143b-136">`https://y8rPrT2b.ngrok.io/`*これは、y8rPrT2b* が ngrok の英数字 HTTPS URL に置き換えられる場所に似ているはずです。</span><span class="sxs-lookup"><span data-stu-id="2143b-136">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="2143b-137">必ず、コマンド プロンプトを ngrok で実行し、URL をメモしてください。</span><span class="sxs-lookup"><span data-stu-id="2143b-137">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

- <span data-ttu-id="2143b-138">**ngrok** が動作していることを確認するには、ブラウザを開き、コマンド プロンプト ウィンドウで指定された ngrok HTTPS URL を使用してコンテンツ ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="2143b-138">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="2143b-139">このクイック スタートを完了するには、Visual Studioと ngrok の両方のアプリケーションを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2143b-139">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="2143b-140">アプリケーションを操作するためにVisual Studioでアプリケーションの実行を停止する必要がある場合は、 **ngrok を実行したまま** にします。</span><span class="sxs-lookup"><span data-stu-id="2143b-140">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="2143b-141">引き続きリッスンし、Visual Studioで再起動すると、アプリケーションの要求のルーティングを再開します。</span><span class="sxs-lookup"><span data-stu-id="2143b-141">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="2143b-142">ngrokサービスを再起動する必要がある場合は、新しいURLを返し、そのURLを使用するすべての場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2143b-142">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="2143b-143">アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="2143b-143">Run your application</span></span>

- <span data-ttu-id="2143b-144">**Visual Studio F5** キーを押すか、アプリケーションの **[デバッグ**] メニューから **[デバッグの開始**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2143b-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="2143b-145">次の手順</span><span class="sxs-lookup"><span data-stu-id="2143b-145">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2143b-146">ASP.NETCore MVC を使用してカスタム 個人用タブを作成します。</span><span class="sxs-lookup"><span data-stu-id="2143b-146">Create a Custom Personal Tab with ASP.NETCore MVC</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core-mvc.md)
