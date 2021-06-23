---
title: ユーザー設定で個人用タブを作成 ASP.NET Core
author: surbhigupta
description: ユーザー設定の個人用タブを作成するクイック スタート ASP.NET Core。
ms.topic: quickstart
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: a839ae126a2cfdb137b22108038dd15a4b47b95a
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069046"
---
# <a name="create-a-personal-tab-using-aspnetcore"></a><span data-ttu-id="c47ee-103">ASP.NETCore を使用して個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="c47ee-103">Create a personal tab using ASP.NETCore</span></span>

<span data-ttu-id="c47ee-104">このクイック スタートでは、Core Razor ページを使用してカスタムの個人用タブC#作成 ASP.Net 説明します。</span><span class="sxs-lookup"><span data-stu-id="c47ee-104">In this quickstart, we'll walk-through creating a custom personal tab with C# and ASP.Net Core Razor pages.</span></span> <span data-ttu-id="c47ee-105">また、アプリ マニフェストをMicrosoft Teams、アプリ マニフェストにタブを展開するために App [Studio](~/concepts/build-and-test/app-studio-overview.md)をTeams。</span><span class="sxs-lookup"><span data-stu-id="c47ee-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="c47ee-106">ソース コードを取得する</span><span class="sxs-lookup"><span data-stu-id="c47ee-106">Get the source code</span></span>

<span data-ttu-id="c47ee-107">コマンド プロンプトを開き、タブ プロジェクトの新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="c47ee-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="c47ee-108">開始する簡単なプロジェクトを提供しました。</span><span class="sxs-lookup"><span data-stu-id="c47ee-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="c47ee-109">ソース コードを取得するには、zip フォルダーをダウンロードしてファイルを抽出するか、サンプル リポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="c47ee-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="c47ee-110">ソース コードを取得したら、[プロジェクト] を開Visual Studioプロジェクトまたはソリューションを開 **く] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="c47ee-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="c47ee-111">タブ アプリケーション ディレクトリに移動し **、PersonalTab.sln を開きます**。</span><span class="sxs-lookup"><span data-stu-id="c47ee-111">Navigate to the tab application directory and open **PersonalTab.sln**.</span></span>

<span data-ttu-id="c47ee-112">アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="c47ee-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="c47ee-113">ブラウザーで、以下の URL に移動して、アプリケーションが正しく読み込まれているか確認します。</span><span class="sxs-lookup"><span data-stu-id="c47ee-113">In a browser navigate to the URLs below to verify the application loaded properly:</span></span>

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="c47ee-114">ソース コードを確認する</span><span class="sxs-lookup"><span data-stu-id="c47ee-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="c47ee-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="c47ee-115">Startup.cs</span></span>

<span data-ttu-id="c47ee-116">このプロジェクトは、ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成され、セットアップ時に [詳細設定 **- HTTPS** 用に構成] チェック ボックスがオンになっています。</span><span class="sxs-lookup"><span data-stu-id="c47ee-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="c47ee-117">MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。</span><span class="sxs-lookup"><span data-stu-id="c47ee-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="c47ee-118">さらに、空のテンプレートでは既定では静的コンテンツの配信が有効ではないので、静的ファイル ミドルウェアがメソッドに追加 `Configure()` されます。</span><span class="sxs-lookup"><span data-stu-id="c47ee-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="c47ee-119">wwwroot フォルダー</span><span class="sxs-lookup"><span data-stu-id="c47ee-119">wwwroot folder</span></span>

<span data-ttu-id="c47ee-120">この ASP.NET Core Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="c47ee-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="c47ee-121">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="c47ee-121">Index.cshtml</span></span>

<span data-ttu-id="c47ee-122">ASP.NET Core Index と呼ばれるファイルをサイトの既定/ホーム ページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="c47ee-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="c47ee-123">ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="c47ee-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="c47ee-124">AppManifest フォルダー</span><span class="sxs-lookup"><span data-stu-id="c47ee-124">AppManifest folder</span></span>

<span data-ttu-id="c47ee-125">このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c47ee-125">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="c47ee-126">192 x 192 ピクセルのフル カラー アイコン。 </span><span class="sxs-lookup"><span data-stu-id="c47ee-126">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="c47ee-127">**32** x 32 ピクセルの透明なアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="c47ee-127">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="c47ee-128">アプリ **manifest.js** を指定するファイルのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="c47ee-128">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="c47ee-129">これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。</span><span class="sxs-lookup"><span data-stu-id="c47ee-129">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="c47ee-130">Microsoft Teams指定したマニフェストを読み込み、それを iframe <に埋め込み、タブ `contentUrl` \> に表示します。</span><span class="sxs-lookup"><span data-stu-id="c47ee-130">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an <iframe\>, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="c47ee-131">.csproj</span><span class="sxs-lookup"><span data-stu-id="c47ee-131">.csproj</span></span>

<span data-ttu-id="c47ee-132">[ソリューション エクスプローラー Visual Studioで、プロジェクトを右クリックし、[ファイルの編集] Project **します**。</span><span class="sxs-lookup"><span data-stu-id="c47ee-132">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="c47ee-133">ファイルの下部には、アプリケーションのビルド時に zip フォルダーを作成および更新するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c47ee-133">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="c47ee-134">プロジェクト ディレクトリのルートでコマンド プロンプトを開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="c47ee-134">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

- <span data-ttu-id="c47ee-135">Ngrok はインターネットからの要求をリッスンし、ポート 44325 で実行されているアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="c47ee-135">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="c47ee-136">`https://y8rPrT2b.ngrok.io/` *y8rPrT2b* が ngrok の英数字 HTTPS URL に置き換えられる場所に似ている必要があります。</span><span class="sxs-lookup"><span data-stu-id="c47ee-136">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="c47ee-137">ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。後で必要になります。</span><span class="sxs-lookup"><span data-stu-id="c47ee-137">Be sure to keep the command prompt with ngrok running, and to make a note of the URL — you'll need it later.</span></span>

- <span data-ttu-id="c47ee-138">ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を介してコンテンツ ページに移動して **、ngrok** が正常に実行され、正常に動作されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c47ee-138">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="c47ee-139">このクイック スタートを完了するには、アプリケーションVisual Studio ngrok の両方を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c47ee-139">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="c47ee-140">アプリケーションの実行を停止する必要がある場合Visual Studio **ngrok を実行し続ける必要があります**。</span><span class="sxs-lookup"><span data-stu-id="c47ee-140">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="c47ee-141">引き続きリッスンし、アプリケーションの要求がサーバーで再起動されると、アプリケーションの要求のルーティングVisual Studio。</span><span class="sxs-lookup"><span data-stu-id="c47ee-141">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="c47ee-142">ngrok サービスを再起動する必要がある場合は、新しい URL が返され、その URL を使用する場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c47ee-142">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="c47ee-143">アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="c47ee-143">Run your application</span></span>

- <span data-ttu-id="c47ee-144">[Visual Studio **F5 キーを押するか、\*\*\*\*アプリケーションの**[デバッグ] メニューから [デバッグの開始]**を選択** します。</span><span class="sxs-lookup"><span data-stu-id="c47ee-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

## <a name="next-step"></a><span data-ttu-id="c47ee-145">次の手順</span><span class="sxs-lookup"><span data-stu-id="c47ee-145">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c47ee-146">ASP.NETCore MVC を使用してカスタム個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="c47ee-146">Create a Custom Personal Tab with ASP.NETCore MVC</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core-mvc.md)
