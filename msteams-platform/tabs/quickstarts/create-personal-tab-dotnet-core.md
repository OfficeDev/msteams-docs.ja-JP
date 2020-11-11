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
# <a name="create-a-personal-tab-with-aspnet-core"></a><span data-ttu-id="e87cc-103">ASP.NET Core を使用して [個人用] タブを作成する</span><span class="sxs-lookup"><span data-stu-id="e87cc-103">Create a personal tab with ASP.NET Core</span></span>

<span data-ttu-id="e87cc-104">このクイックスタートでは、C# と ASP.Net コアの Razor ページを使用して、カスタムの個人用タブを作成する手順を説明します。</span><span class="sxs-lookup"><span data-stu-id="e87cc-104">In this quickstart we'll walk-through creating a custom personal tab with C# and ASP.Net Core Razor pages.</span></span> <span data-ttu-id="e87cc-105">また、 [Microsoft teams 用のアプリ Studio](~/concepts/build-and-test/app-studio-overview.md) を使用して、アプリマニフェストを完成させ、タブを teams に展開します。</span><span class="sxs-lookup"><span data-stu-id="e87cc-105">We'll also use [App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) to finalize your app manifest and deploy your tab to Teams.</span></span>

[!INCLUDE [dotnet-core-prereq](~/includes/tabs/dotnet-core-prereq.md)]

## <a name="get-the-source-code"></a><span data-ttu-id="e87cc-106">ソースコードを取得する</span><span class="sxs-lookup"><span data-stu-id="e87cc-106">Get the source code</span></span>

<span data-ttu-id="e87cc-107">コマンドプロンプトを開き、タブプロジェクト用の新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="e87cc-107">Open a command prompt and create a new directory for your tab project.</span></span> <span data-ttu-id="e87cc-108">開始するための簡単なプロジェクトを提供しています。</span><span class="sxs-lookup"><span data-stu-id="e87cc-108">We have provided a simple project to get you started.</span></span> <span data-ttu-id="e87cc-109">ソースコードを取得するには、zip フォルダーをダウンロードして、ファイルを抽出するか、またはサンプルリポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="e87cc-109">To retrieve the source code you can download the zip folder and extract the files or clone the sample repository into your new directory:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="e87cc-110">ソースコードを取得したら、Visual Studio を開き、[ **プロジェクトまたはソリューションを開く** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e87cc-110">Once you have the source code, open Visual Studio and select **Open a project or solution**.</span></span> <span data-ttu-id="e87cc-111">Tab アプリケーションディレクトリに移動して、"独自のタブを開く" という名前の **.sln** を開きます。</span><span class="sxs-lookup"><span data-stu-id="e87cc-111">Navigate to the tab application directory and open **PersonalTab.sln**.</span></span>

<span data-ttu-id="e87cc-112">アプリケーションをビルドして実行するには、 **F5** キーを押すか、[ **デバッグ** ] メニューの [ **デバッグ開始** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e87cc-112">To build and run your application press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="e87cc-113">ブラウザーで以下の Url に移動し、アプリケーションが正しく読み込まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e87cc-113">In a browser navigate to the URLs below to verify the application loaded properly:</span></span>

- `http://localhost:44325/`
- `http://localhost:44325/personal`
- `http://localhost:44325/privacy`
- `http://localhost:44325/tou`

## <a name="review-the-source-code"></a><span data-ttu-id="e87cc-114">ソースコードを確認する</span><span class="sxs-lookup"><span data-stu-id="e87cc-114">Review the source code</span></span>

### <a name="startupcs"></a><span data-ttu-id="e87cc-115">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="e87cc-115">Startup.cs</span></span>

<span data-ttu-id="e87cc-116">このプロジェクトは、セットアップ時に選択されている *[HTTPS の詳細構成* ] チェックボックスがオンになっている ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成されました。</span><span class="sxs-lookup"><span data-stu-id="e87cc-116">This project was created from an ASP.NET Core 2.2 Web Application empty template with the *Advanced - Configure for HTTPS* check box selected at setup.</span></span> <span data-ttu-id="e87cc-117">MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録され `ConfigureServices()` ます。</span><span class="sxs-lookup"><span data-stu-id="e87cc-117">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="e87cc-118">また、空のテンプレートでは、既定で静的コンテンツの提供が有効になっていないため、このメソッドには静的ファイルミドルウェアが追加され `Configure()` ます。</span><span class="sxs-lookup"><span data-stu-id="e87cc-118">Additionally, the empty template doesn't enable serving static content by default, so the static files middleware is added to the `Configure()` method:</span></span>

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

### <a name="wwwroot-folder"></a><span data-ttu-id="e87cc-119">wwwroot フォルダー</span><span class="sxs-lookup"><span data-stu-id="e87cc-119">wwwroot folder</span></span>

<span data-ttu-id="e87cc-120">ASP.NET Core で、web ルートフォルダーはアプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="e87cc-120">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

### <a name="indexcshtml"></a><span data-ttu-id="e87cc-121">インデックス. cshtml</span><span class="sxs-lookup"><span data-stu-id="e87cc-121">Index.cshtml</span></span>

<span data-ttu-id="e87cc-122">ASP.NET Core は、 *Index* というファイルをサイトの既定またはホームページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="e87cc-122">ASP.NET Core treats files called *Index* as the default/home page for the site.</span></span> <span data-ttu-id="e87cc-123">ブラウザーの URL がサイトのルートを指している場合は、アプリケーションのホームページとして、 **cshtml** が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e87cc-123">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

### <a name="appmanifest-folder"></a><span data-ttu-id="e87cc-124">Appmanifest.xml フォルダー</span><span class="sxs-lookup"><span data-stu-id="e87cc-124">AppManifest folder</span></span>

<span data-ttu-id="e87cc-125">このフォルダーには、次の必要なアプリパッケージファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e87cc-125">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="e87cc-126">192 x 192 ピクセルを測定する **フルカラーアイコン** 。</span><span class="sxs-lookup"><span data-stu-id="e87cc-126">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="e87cc-127">32 x 32 ピクセルを測定する **透明のアウトラインアイコン** 。</span><span class="sxs-lookup"><span data-stu-id="e87cc-127">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="e87cc-128">アプリの属性を指定するファイルの **manifest.js** 。</span><span class="sxs-lookup"><span data-stu-id="e87cc-128">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="e87cc-129">これらのファイルは、タブを Teams にアップロードする際に使用するために、アプリパッケージに圧縮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e87cc-129">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="e87cc-130">Microsoft Teams は、 `contentUrl` マニフェストで指定されたを読み込み、それを IFrame に埋め込んで、それをタブに表示します。</span><span class="sxs-lookup"><span data-stu-id="e87cc-130">Microsoft Teams will load the `contentUrl` specified in your manifest, embed it in an IFrame, and render it in your tab.</span></span>

### <a name="csproj"></a><span data-ttu-id="e87cc-131">.csproj</span><span class="sxs-lookup"><span data-stu-id="e87cc-131">.csproj</span></span>

<span data-ttu-id="e87cc-132">Visual Studio の [ソリューションエクスプローラー] ウィンドウで、プロジェクトを右クリックし、[ **プロジェクトファイルの編集** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e87cc-132">In the Visual Studio Solution Explorer window right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="e87cc-133">ファイルの末尾に、アプリケーションのビルド時に zip フォルダーを作成して更新するコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e87cc-133">At the bottom of the file you'll see the code that creates and updates your zip folder when the application builds:</span></span>

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

- <span data-ttu-id="e87cc-134">プロジェクトディレクトリのルートでコマンドプロンプトを開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="e87cc-134">Open a command prompt in the root of your project directory and run the following command:</span></span>

```bash
ngrok http https://localhost:44325 -host-header="localhost:44325"
```

- <span data-ttu-id="e87cc-135">Ngrok は、インターネットからの要求をリッスンし、ポート44325上で実行されている場合にそれらをアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="e87cc-135">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44325.</span></span>  <span data-ttu-id="e87cc-136">`https://y8rPrT2b.ngrok.io/` *Y8rPrT2b* は、ngrok alpha の数字の HTTPS URL に置き換えられる場所に似ているはずです。</span><span class="sxs-lookup"><span data-stu-id="e87cc-136">It should resemble `https://y8rPrT2b.ngrok.io/` where *y8rPrT2b* is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="e87cc-137">コマンドプロンプトは ngrok を実行したままにしておき、後で必要になるように URL を書き留めておきます。</span><span class="sxs-lookup"><span data-stu-id="e87cc-137">Be sure to keep the command prompt with ngrok running, and to make a note of the URL—you'll need it later.</span></span>

- <span data-ttu-id="e87cc-138">ブラウザーを開き、コマンドプロンプトウィンドウで提供された ngrok HTTPS URL を使用してコンテンツページにアクセスすることにより、 *ngrok* が実行されて正常に動作していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e87cc-138">Verify that *ngrok* is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="e87cc-139">このクイックスタートを完了するには、Visual Studio と ngrok の両方のアプリケーションが実行されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="e87cc-139">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="e87cc-140">Visual Studio でのアプリケーションの実行を停止する必要がある場合は、 **ngrok の実行を継続** してください。</span><span class="sxs-lookup"><span data-stu-id="e87cc-140">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="e87cc-141">Visual Studio で再起動すると、アプリケーションの要求のルーティングが続行され、再開されます。</span><span class="sxs-lookup"><span data-stu-id="e87cc-141">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="e87cc-142">Ngrok サービスを再起動する必要がある場合は、新しい URL を返し、その URL を使用するすべての場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e87cc-142">If you have to restart the ngrok service it will return a new URL and you'll have to update every place that uses that URL.</span></span>

### <a name="run-your-application"></a><span data-ttu-id="e87cc-143">アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="e87cc-143">Run your application</span></span>

- <span data-ttu-id="e87cc-144">Visual Studio で **F5** キーを押すか、アプリケーションの **デバッグ** メニューから [ **デバッグ開始** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e87cc-144">In Visual Studio press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]
