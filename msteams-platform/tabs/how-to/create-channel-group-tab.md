---
title: '[チャネルまたはグループ] タブを作成する'
author: laujan
description: Yeoman Generator を使用してチャネルとグループ タブを作成するクイック スタート Microsoft Teams。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: fedaf3ec639917110e16c666734fa3eedbcda18e
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179996"
---
# <a name="create-a-channel-or-group-tab"></a><span data-ttu-id="31b8f-103">[チャネルまたはグループ] タブを作成する</span><span class="sxs-lookup"><span data-stu-id="31b8f-103">Create a channel or group tab</span></span>

## <a name="create-a-custom-channel-or-group-tab"></a><span data-ttu-id="31b8f-104">カスタム チャネルまたはグループ タブの作成</span><span class="sxs-lookup"><span data-stu-id="31b8f-104">Create a custom channel or group tab</span></span>

<span data-ttu-id="31b8f-105">チャネルまたはグループ タブは、Node.js Yeoman Generator、ASP.NETCore、または ASP.NETCore MVC を使用して作成できます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-105">You can create a channel or group tab using Node.js and the Yeoman Generator, ASP.NETCore, or ASP.NETCore MVC.</span></span>

# <a name="nodejs"></a>[<span data-ttu-id="31b8f-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="31b8f-106">Node.js</span></span>](#tab/nodejs)

### <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator"></a><span data-ttu-id="31b8f-107">カスタム チャネルとグループ タブを作成するには、Node.js Yeoman Generator を使用します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-107">Create a custom channel and group tab using Node.js and the Yeoman Generator</span></span>

> [!NOTE]
> <span data-ttu-id="31b8f-108">この記事では、Microsoft OfficeDev Microsoft Teamsリポジトリにあるアプリ[Wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)のビルドにGitHubします。</span><span class="sxs-lookup"><span data-stu-id="31b8f-108">This article follows the steps outlined in the [build Your first Microsoft Teams app](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="31b8f-109">You can create a custom channel or group tab using the you can create a custom channel or group tab using [the Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span><span class="sxs-lookup"><span data-stu-id="31b8f-109">You can create a custom channel or group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

### <a name="prerequisites-for-apps"></a><span data-ttu-id="31b8f-110">アプリの前提条件</span><span class="sxs-lookup"><span data-stu-id="31b8f-110">Prerequisites for apps</span></span>

<span data-ttu-id="31b8f-111">次の前提条件について理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-111">You must have an understanding of the following prerequisites:</span></span>

- <span data-ttu-id="31b8f-112">カスタム アプリのアップロードを許可Office 365を有効にしたテナントとチーム **が構成されている必要** があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-112">You must have an Office 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="31b8f-113">詳細については、「prepare [your Office 365 テナント」を参照してください](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-113">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="31b8f-114">現在アカウントをお持ちOffice 365場合は、開発者プログラムから無料サブスクリプションOffice 365できます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-114">If you do not currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="31b8f-115">サブスクリプションは、継続的な開発に使用している限りアクティブなままです。</span><span class="sxs-lookup"><span data-stu-id="31b8f-115">The subscription remains active as long as you are using it for ongoing development.</span></span> <span data-ttu-id="31b8f-116">「[開発者プログラムへようこそOffice 365」を参照してください](/office/developer-program/microsoft-365-developer-program)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-116">See [welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="31b8f-117">さらに、このプロジェクトでは、次のコードが開発環境にインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-117">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="31b8f-118">任意のテキスト エディターまたは IDE。</span><span class="sxs-lookup"><span data-stu-id="31b8f-118">Any text editor or IDE.</span></span> <span data-ttu-id="31b8f-119">無料でインストール[して使用Visual Studio Code](https://code.visualstudio.com/download)できます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-119">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="31b8f-120">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="31b8f-120">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="31b8f-121">最新の LTS バージョンを使用します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-121">Use the latest LTS version.</span></span> <span data-ttu-id="31b8f-122">Node パッケージ マネージャー (npm) は、システムにインストールされたシステムにインストールNode.js。</span><span class="sxs-lookup"><span data-stu-id="31b8f-122">The Node Package Manager (npm) installs in your system with the installation of Node.js.</span></span>

- <span data-ttu-id="31b8f-123">インストールが正常に完了したらNode.jsに次のコマンド プロンプトを入力して [、Yeoman](https://yeoman.io/) パッケージと [gulp-cli](https://www.npmjs.com/package/gulp-cli) パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="31b8f-123">After you have successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by entering the following in your command prompt:</span></span>

    ```bash
    npm install yo gulp-cli --global
    ```

- <span data-ttu-id="31b8f-124">コマンド プロンプトにMicrosoft Teamsを入力して、アプリ ジェネレーターをインストールします。</span><span class="sxs-lookup"><span data-stu-id="31b8f-124">Install the Microsoft Teams Apps generator by entering the following in your command prompt:</span></span>

    ```bash
    npm install generator-teams --global
    ```

### <a name="generate-your-project"></a><span data-ttu-id="31b8f-125">プロジェクトを生成する</span><span class="sxs-lookup"><span data-stu-id="31b8f-125">Generate your project</span></span>

<span data-ttu-id="31b8f-126">**プロジェクトを生成するには**</span><span class="sxs-lookup"><span data-stu-id="31b8f-126">**To generate your project**</span></span>

1. <span data-ttu-id="31b8f-127">コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-127">At a command prompt, create a new directory for your tab project.</span></span>

1. <span data-ttu-id="31b8f-128">ジェネレーターを起動するには、新しいディレクトリに移動し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-128">To start the generator, go to your new directory and type the following command:</span></span>

    ```bash
    yo teams
    ```

1. <span data-ttu-id="31b8f-129">次に、アプリケーションのファイルファイルで使用される一連の値manifest.js **指定** します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-129">Next, provide a series of values that are used in your application's **manifest.json** file:</span></span>

    ![ジェネレーターの開くスクリーンショット](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <span data-ttu-id="31b8f-131">**ソリューション名は何ですか?**</span><span class="sxs-lookup"><span data-stu-id="31b8f-131">**What is your solution name?**</span></span>

    <span data-ttu-id="31b8f-132">これはプロジェクト名です。</span><span class="sxs-lookup"><span data-stu-id="31b8f-132">This is your project name.</span></span> <span data-ttu-id="31b8f-133">Enter キーを選択すると、候補の名前を **受け入** れできます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-133">You can accept the suggested name by selecting the **Enter** key.</span></span>

    <span data-ttu-id="31b8f-134">**ファイルをどこに保存しますか?**</span><span class="sxs-lookup"><span data-stu-id="31b8f-134">**Where do you want to place the files?**</span></span>

    <span data-ttu-id="31b8f-135">現在、プロジェクト ディレクトリにいます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-135">You are currently in your project directory.</span></span> <span data-ttu-id="31b8f-136">**[Enter] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-136">Select **Enter**.</span></span>

    <span data-ttu-id="31b8f-137">**アプリ プロジェクトMicrosoft Teamsタイトル**</span><span class="sxs-lookup"><span data-stu-id="31b8f-137">**Title of your Microsoft Teams app project?**</span></span>

    <span data-ttu-id="31b8f-138">これはアプリ パッケージ名であり、アプリ マニフェストと説明で使用されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-138">This is your app package name and will be used in the app manifest and description.</span></span> <span data-ttu-id="31b8f-139">タイトルを入力するか、Enter **を選択して** 既定の名前を受け入れる。</span><span class="sxs-lookup"><span data-stu-id="31b8f-139">Enter a title or select **Enter** to accept the default name.</span></span>

    <span data-ttu-id="31b8f-140">**(会社) の名前(最大 32 文字)**</span><span class="sxs-lookup"><span data-stu-id="31b8f-140">**Your (company) name? (max 32 characters)**</span></span>

    <span data-ttu-id="31b8f-141">会社名はアプリ マニフェストで使用されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-141">Your company name will be used in the app manifest.</span></span> <span data-ttu-id="31b8f-142">会社名を入力するか **、Enter を選択して** 既定の名前を受け入れる。</span><span class="sxs-lookup"><span data-stu-id="31b8f-142">Enter a company name or select **Enter** to accept the default name.</span></span>

    <span data-ttu-id="31b8f-143">**どのマニフェスト バージョンを使用しますか?**</span><span class="sxs-lookup"><span data-stu-id="31b8f-143">**Which manifest version would you like to use?**</span></span>

    <span data-ttu-id="31b8f-144">既定のスキーマを選択します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-144">Select the default schema.</span></span>

    <span data-ttu-id="31b8f-145">**クイック スキャフォールディング(Y/n)**</span><span class="sxs-lookup"><span data-stu-id="31b8f-145">**Quick scaffolding? (Y/n)**</span></span>

    <span data-ttu-id="31b8f-146">既定値は yes です。 **n と入力** して Microsoft パートナー ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-146">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

    <span data-ttu-id="31b8f-147">**Microsoft パートナー ID をお持ちの場合は、Microsoft パートナー ID を入力してください。(スキップする場合は空白のままにする)**</span><span class="sxs-lookup"><span data-stu-id="31b8f-147">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

    <span data-ttu-id="31b8f-148">このフィールドは必須ではなく、Microsoft パートナー ネットワークに既に参加している場合にのみ [使用する必要があります](https://partner.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-148">This field is not required and should only be used if you are already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

    <span data-ttu-id="31b8f-149">**プロジェクトに何を追加しますか?**</span><span class="sxs-lookup"><span data-stu-id="31b8f-149">**What do you want to add to your project?**</span></span>

    <span data-ttu-id="31b8f-150">[ **選択] &ast; ( ) [タブ] をクリックします**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-150">Select **( &ast; ) A Tab**.</span></span>

    <span data-ttu-id="31b8f-151">**このソリューションをホストする URL**</span><span class="sxs-lookup"><span data-stu-id="31b8f-151">**The URL where you will host this solution?**</span></span>

    <span data-ttu-id="31b8f-152">既定では、ジェネレーターは Azure Web サイトの URL を提案します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-152">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="31b8f-153">アプリをローカルでテストしているだけなので、有効な URL は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="31b8f-153">You are only testing your app locally, therefore, a valid URL is not necessary.</span></span>

    <span data-ttu-id="31b8f-154">**アプリ/タブの読み込み時に読み込みインジケーターを表示しますか?**</span><span class="sxs-lookup"><span data-stu-id="31b8f-154">**Would you like show a loading indicator when your app/tab loads?**</span></span>

    <span data-ttu-id="31b8f-155">アプリ **またはタブ** の読み込み時に読み込みインジケーターを含めないを選択します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-155">Choose **not** to include a loading indicator when your app or tab loads.</span></span> <span data-ttu-id="31b8f-156">既定値は no で、n と **入力します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-156">The default is no, enter **n**.</span></span>

   <span data-ttu-id="31b8f-157">**個人用アプリをタブ ヘッダーバーなしでレンダリングしますか?**</span><span class="sxs-lookup"><span data-stu-id="31b8f-157">**Would you like personal apps to be rendered without a tab header-bar?**</span></span>

    <span data-ttu-id="31b8f-158">タブ **ヘッダー** バーなしでレンダリングする個人用アプリを含めないを選択します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-158">Choose **not** to include personal apps to be rendered without a tab header-bar.</span></span> <span data-ttu-id="31b8f-159">既定値はいいえ、n と **入力します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-159">Default is no, enter **n**.</span></span>

    <span data-ttu-id="31b8f-160">**テスト フレームワークと初期テストを含めるには?(y/N)**</span><span class="sxs-lookup"><span data-stu-id="31b8f-160">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

    <span data-ttu-id="31b8f-161">この **プロジェクトの** テスト フレームワークを含めないを選択します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-161">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="31b8f-162">既定値は yes です。 **n と入力します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-162">The default is yes; enter **n**.</span></span>

    <span data-ttu-id="31b8f-163">**テレメトリに Azure Applications インサイト使用しますか?(y/N)**</span><span class="sxs-lookup"><span data-stu-id="31b8f-163">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

    <span data-ttu-id="31b8f-164">[Azure **Application インサイト**[を含インサイト。](/azure/azure-monitor/app/app-insights-overview)</span><span class="sxs-lookup"><span data-stu-id="31b8f-164">Choose **not** to include [Azure Application Insights](/azure/azure-monitor/app/app-insights-overview).</span></span> <span data-ttu-id="31b8f-165">既定値は no です。 **n と入力します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-165">The default is no; enter **n**.</span></span>

    <span data-ttu-id="31b8f-166">**既定のタブ名 (最大 16 文字)?**</span><span class="sxs-lookup"><span data-stu-id="31b8f-166">**Default Tab Name (max 16 characters)?**</span></span>

    <span data-ttu-id="31b8f-167">タブの名前を指定します。このタブ名は、ファイルまたは URL パス コンポーネントとしてプロジェクト全体で使用されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-167">Name your tab. This tab name will be used throughout your project as a file or URL path component.</span></span>

    <span data-ttu-id="31b8f-168">**作成するタブの種類**</span><span class="sxs-lookup"><span data-stu-id="31b8f-168">**What kind of Tab would you like to create?**</span></span>

    <span data-ttu-id="31b8f-169">矢印キーを使用して、[構成可能] **タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-169">Use the arrow keys to select **Configurable** tab.</span></span>

    <span data-ttu-id="31b8f-170">**Tab に使用するスコープは何ですか?**</span><span class="sxs-lookup"><span data-stu-id="31b8f-170">**What scopes do you intend to use for your Tab?**</span></span>

    <span data-ttu-id="31b8f-171">チームまたはグループ チャットを選択できます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-171">You can select a team or a group chat.</span></span>

    <span data-ttu-id="31b8f-172">**タブに Azure AD のシングルサインオン サポートが必要ですか?**</span><span class="sxs-lookup"><span data-stu-id="31b8f-172">**Do you require Azure AD Single-Sign-On support for the tab?**</span></span>

    <span data-ttu-id="31b8f-173">タブ **に** Azure ADシングル サインオン のサポートを含めないを選択します。既定値ははい、n と **入力します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-173">Choose **not** to include Azure AD Single-Sign-On support for the tab. The default is yes, enter **n**.</span></span>

    <span data-ttu-id="31b8f-174">**このタブをオンラインで使用SharePointしますか?(Y/n)**</span><span class="sxs-lookup"><span data-stu-id="31b8f-174">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span>

    <span data-ttu-id="31b8f-175">**n と入力します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-175">Enter **n**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="31b8f-176">パス コンポーネント **yourDefaultTabNameTab**, is you entered the value in the generator for **Default Tab Name** plus the word **Tab**.</span><span class="sxs-lookup"><span data-stu-id="31b8f-176">The path component **yourDefaultTabNameTab**, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
    >
    > <span data-ttu-id="31b8f-177">例: DefaultTabName: **MyTab**  >  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="31b8f-177">For example: DefaultTabName: **MyTab** > **/MyTabTab/**</span></span>

1. <span data-ttu-id="31b8f-178">[Visual Studio Codeまたはコード エディターで、プロジェクト ディレクトリに移動し、次のファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-178">In Visual Studio Code or any code editor, go to your project directory and open the following file:</span></span>

    ```bash
    ./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
    ```

1. <span data-ttu-id="31b8f-179">メソッドを `render()` 見つけて、コンテナー コードの上部に `<div>` 次のタグとコンテンツを `<PanelBody>` 追加します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-179">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

    ```html
        <PanelBody>
            <div style={styles.section}>
                Hello World! Yo Teams rocks!
            </div>
        </PanelBody>
    ```

1. <span data-ttu-id="31b8f-180">更新されたファイルを保存してください。</span><span class="sxs-lookup"><span data-stu-id="31b8f-180">Make sure to save the updated file.</span></span>

### <a name="build-and-run-your-application"></a><span data-ttu-id="31b8f-181">アプリケーションのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="31b8f-181">Build and run your application</span></span>

<span data-ttu-id="31b8f-182">コマンド プロンプトで、プロジェクト ディレクトリを開いて次のタスクを完了します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-182">At a command prompt, open your project directory to complete the next tasks.</span></span>

#### <a name="create-the-app-package"></a><span data-ttu-id="31b8f-183">アプリ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="31b8f-183">Create the app package</span></span>

<span data-ttu-id="31b8f-184">タブをテストするには、アプリ パッケージが必要Teams。</span><span class="sxs-lookup"><span data-stu-id="31b8f-184">You must have an app package to test your tab in Teams.</span></span> <span data-ttu-id="31b8f-185">これは、次の必須ファイルを含む zip フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="31b8f-185">It is a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="31b8f-186">192 x 192 ピクセルのフル カラー アイコン。 </span><span class="sxs-lookup"><span data-stu-id="31b8f-186">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="31b8f-187">**32** x 32 ピクセルの透明なアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="31b8f-187">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="31b8f-188">アプリ **manifest.js** を指定するファイルのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="31b8f-188">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="31b8f-189">パッケージは、ファイル上のファイルのmanifest.jsを検証し、./package ディレクトリに zip フォルダーを生成する **gulp タスクを使用して作成されます**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-189">The package is created through a gulp task that validates the manifest.json file and generates the zip folder in the **./package directory**.</span></span> <span data-ttu-id="31b8f-190">コマンド プロンプトで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-190">In the command prompt, enter the following command:</span></span>

```bash
gulp manifest
```

#### <a name="build-your-application"></a><span data-ttu-id="31b8f-191">アプリケーションのビルド</span><span class="sxs-lookup"><span data-stu-id="31b8f-191">Build your application</span></span>

<span data-ttu-id="31b8f-192">ビルド コマンドは、ソリューションを **./dist フォルダーに変換** します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-192">The build command transpiles your solution into the **./dist** folder.</span></span> <span data-ttu-id="31b8f-193">コマンド プロンプトで次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-193">Enter the following command in the command prompt:</span></span>

```bash
gulp build
```

#### <a name="run-your-application-in-localhost"></a><span data-ttu-id="31b8f-194">localhost でアプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="31b8f-194">Run your application in localhost</span></span>

1. <span data-ttu-id="31b8f-195">コマンド プロンプトに次の情報を入力して、ローカル Web サーバーを起動します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-195">Start a local web server by entering the following in the command prompt:</span></span>

    ```bash
    gulp serve
    ```

1. <span data-ttu-id="31b8f-196">次の図に示すように、ブラウザーに入力し、タブ名に置き換え、アプリケーションのホーム ページ `http://localhost:3007/<yourDefaultAppNameTab>/` **<yourDefaultAppNameTab>** を表示します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-196">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser, replace **<yourDefaultAppNameTab>** with your tab name, and view your application's home page as shown in the following image:</span></span>

    ![ホーム ページのスクリーンショット](~/assets/images/tab-images/homePage.png)

1. <span data-ttu-id="31b8f-198">タブ構成ページを表示するには、 に移動します `https://localhost:3007/<yourDefaultAppNameTab>/config.html` 。</span><span class="sxs-lookup"><span data-stu-id="31b8f-198">To view your tab configuration page, go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="31b8f-199">次に示します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-199">The following is shown:</span></span>

    ![構成ページのスクリーンショット](~/assets/images/tab-images/configurationPage.png)

### <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="31b8f-201">タブへのセキュリティで保護されたトンネルを確立する</span><span class="sxs-lookup"><span data-stu-id="31b8f-201">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="31b8f-202">Microsoft Teamsはクラウドベースの製品であり、HTTPS エンドポイントを使用してタブ コンテンツをクラウドから利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-202">Microsoft Teams is a cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="31b8f-203">Teamsはローカル ホスティングを許可しない。</span><span class="sxs-lookup"><span data-stu-id="31b8f-203">Teams does not allow local hosting.</span></span> <span data-ttu-id="31b8f-204">タブをパブリック URL に発行するか、ローカル ポートをインターネットに接続する URL に公開するプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-204">You must either publish your tab to a public URL or use a proxy that exposes your local port to an internet-facing URL.</span></span>

<span data-ttu-id="31b8f-205">タブ拡張機能をテストするには、 [このアプリケーションに組み込まれる ngrok](https://ngrok.com/docs)を使用します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-205">To test your tab extension, use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="31b8f-206">Ngrok はリバース プロキシ ソフトウェア ツールで、ローカルで実行中の Web サーバーの一般公開 HTTPS エンドポイントへのトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-206">Ngrok is a reverse proxy software tool that creates a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="31b8f-207">サーバーの Web エンドポイントは、コンピューター上の現在のセッション中に使用できます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-207">Your server's web endpoints are available during the current session on your computer.</span></span> <span data-ttu-id="31b8f-208">コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="31b8f-208">When the computer is shut down or goes to sleep the service is no longer available.</span></span>

<span data-ttu-id="31b8f-209">コマンド プロンプトで localhost を終了し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-209">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="31b8f-210">タブが Microsoft Teams にアップロードされ、正常に保存された後は、タブ ギャラリーでタブを表示し、タブ バーに追加し、ngrok トンネル セッションが終了するまで操作できます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-210">After your tab has been uploaded to Microsoft Teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="31b8f-211">ngrok セッションを再起動する場合は、新しい URL でアプリを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-211">If you restart your ngrok session, you must update your app with the new URL.</span></span>

### <a name="upload-your-application-to-teams"></a><span data-ttu-id="31b8f-212">アップロードを使用してアプリケーションをTeams</span><span class="sxs-lookup"><span data-stu-id="31b8f-212">Upload your application to Teams</span></span>

<span data-ttu-id="31b8f-213">**アプリケーションをアプリにアップロードTeams**</span><span class="sxs-lookup"><span data-stu-id="31b8f-213">**To upload your application to Teams**</span></span>

1. <span data-ttu-id="31b8f-214">[次へ] にMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="31b8f-214">Go to Microsoft Teams.</span></span> <span data-ttu-id="31b8f-215">Web ベースのバージョン [を使用する場合は](https://teams.microsoft.com) 、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-215">If you use the [web-based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
1. <span data-ttu-id="31b8f-216">左側のウィンドウのチームから、タブのテストに使用 &#x25CF;&#x25CF;&#x25CF; の横にある省略記号を選択し、[チームの管理] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-216">From your teams on the left pane, select the ellipses &#x25CF;&#x25CF;&#x25CF; next to the team that you are using to test your tab and choose **Manage team**.</span></span>
1. <span data-ttu-id="31b8f-217">メイン ウィンドウで、タブ **バーから**[アプリ]を選択し、アップロード右下隅にあるカスタム アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-217">In the main pane, select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right corner of the page.</span></span>
1. <span data-ttu-id="31b8f-218">プロジェクト ディレクトリを移動し **、./package** フォルダーを参照し、アプリ パッケージの zip フォルダーを選択し、[開く] を選択 **します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-218">Go your project directory, browse to the **./package** folder, select the app package zip folder, and choose **Open**.</span></span>

    ![[チャネル] タブが追加されました](../../assets/images/tab-images/channeltabadded.png)

1. <span data-ttu-id="31b8f-220">ポップアップ **ダイアログ ボックスで** [追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-220">Select **Add** in the pop-up dialog box.</span></span> <span data-ttu-id="31b8f-221">タブがサイトにTeams。</span><span class="sxs-lookup"><span data-stu-id="31b8f-221">Your tab uploads into Teams.</span></span>
1. <span data-ttu-id="31b8f-222">チームに戻り、タブを表示するチャネルを選択し、タブ バーから [➕] を選択し、ギャラリーからタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-222">Return to your team, choose the channel where you want to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
1. <span data-ttu-id="31b8f-223">タブを追加するには、指示に従います。チャネルまたはグループ タブのカスタム構成ダイアログ ボックスがあります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-223">Follow the directions for adding a tab. There is a custom configuration dialog box for your channel or group tab.</span></span>
1. <span data-ttu-id="31b8f-224">[ **保存] を** 選択すると、タブがチャネルのタブ バーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-224">Select **Save** and your tab is added to the channel's tab bar.</span></span>

    ![チャネル タブのアップロード](../../assets/images/tab-images/channeltabuploaded.png)

# <a name="aspnet-core"></a>[<span data-ttu-id="31b8f-226">ASP.NET コア</span><span class="sxs-lookup"><span data-stu-id="31b8f-226">ASP.NET Core</span></span>](#tab/aspnetcore)

### <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a><span data-ttu-id="31b8f-227">カスタム チャネルまたはグループ タブを作成し、ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="31b8f-227">Create a custom channel or group tab with ASP.NET Core</span></span>

<span data-ttu-id="31b8f-228">カスタム チャネルまたはグループ タブを作成するには、[コア C#] ASP.Net を使用します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-228">You can create a custom channel or group tab using C# and ASP.Net Core Razor page.</span></span> <span data-ttu-id="31b8f-229">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)は、アプリ マニフェストを最終的に作成し、タブを展開してアプリ マニフェストに展開Teams。</span><span class="sxs-lookup"><span data-stu-id="31b8f-229">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) is also used to finalize your app manifest and deploy your tab to Teams.</span></span>

### <a name="prerequisites-for-teams-apps"></a><span data-ttu-id="31b8f-230">アプリのTeams前提条件</span><span class="sxs-lookup"><span data-stu-id="31b8f-230">Prerequisites for Teams apps</span></span>

<span data-ttu-id="31b8f-231">次の前提条件について理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-231">You must have an understanding of the following prerequisites:</span></span>

- <span data-ttu-id="31b8f-232">カスタム アプリのアップロードを許可Office 365を有効にしたテナントとチーム **が構成されている必要** があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-232">You must have an Office 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="31b8f-233">詳細については、「prepare [your Office 365 テナント」を参照してください](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-233">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="31b8f-234">現在アカウントを持Microsoft 365場合は、Microsoft Developer Program を通じて無料サブスクリプションに[サインアップできます](https://developer.microsoft.com/en-us/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-234">If you do not currently have a Microsoft 365 account, you can sign up for a free subscription through the [Microsoft Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program).</span></span> <span data-ttu-id="31b8f-235">サブスクリプションは、継続的な開発に使用している限りアクティブなままです。</span><span class="sxs-lookup"><span data-stu-id="31b8f-235">The subscription remains active as long as you are using it for ongoing development.</span></span>

- <span data-ttu-id="31b8f-236">App Studio を使用してアプリケーションをインポートし、Teams。</span><span class="sxs-lookup"><span data-stu-id="31b8f-236">Use App Studio to import your application to Teams.</span></span> <span data-ttu-id="31b8f-237">App Studio をインストールするには、アプリアプリの左下隅にある [アプリ ストア アプリ] を選択Teams App Studio を ![ ](~/assets/images/tab-images/storeApp.png) **検索します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-237">To install App Studio, select **Apps** ![Store App](~/assets/images/tab-images/storeApp.png) at the lower left corner of the Teams app, and search for **App Studio**.</span></span> <span data-ttu-id="31b8f-238">タイルを見つけたら、タイルを選択し、ポップアップ ダイアログ ボックスで [追加] を選択してインストールします。</span><span class="sxs-lookup"><span data-stu-id="31b8f-238">After you find the tile, select it and choose **Add** in the pop-up dialog box to install it.</span></span>

<span data-ttu-id="31b8f-239">さらに、このプロジェクトでは、次のコードが開発環境にインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-239">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="31b8f-240">現在のバージョンの IDE **Visual Studio.NET CORE** クロスプラットフォーム開発ワークロードがインストールされています。</span><span class="sxs-lookup"><span data-stu-id="31b8f-240">The current version of the Visual Studio IDE with the **.NET CORE cross-platform development** workload installed.</span></span> <span data-ttu-id="31b8f-241">まだインストールされていない場合はVisual Studio最新バージョンを無料でダウンロード[Microsoft Visual Studio Communityインストールできます](https://visualstudio.microsoft.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-241">If you do not already have Visual Studio, you can download and install the latest [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) version for free.</span></span>

- <span data-ttu-id="31b8f-242">[ngrok](https://ngrok.com)リバース プロキシ ツール。</span><span class="sxs-lookup"><span data-stu-id="31b8f-242">The [ngrok](https://ngrok.com) reverse proxy tool.</span></span> <span data-ttu-id="31b8f-243">ngrok を使用して、ローカルで実行中の Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-243">Use ngrok to create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="31b8f-244">[ngrok をダウンロードできます](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-244">You can [download ngrok](https://ngrok.com/download).</span></span>

### <a name="get-the-source-code"></a><span data-ttu-id="31b8f-245">ソース コードを取得する</span><span class="sxs-lookup"><span data-stu-id="31b8f-245">Get the source code</span></span>

<span data-ttu-id="31b8f-246">コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-246">At a command prompt, create a new directory for your tab project.</span></span> <span data-ttu-id="31b8f-247">簡単なプロジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="31b8f-247">A simple project is provided to get you started.</span></span> <span data-ttu-id="31b8f-248">次のコマンドを使用して、サンプル リポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-248">Clone the sample repository into your new directory using the following command:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="31b8f-249">または、zip フォルダーをダウンロードしてファイルを抽出して、ソース コードを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-249">Alternately, you can retrieve the source code by downloading the zip folder and extracting the files.</span></span>

<span data-ttu-id="31b8f-250">**タブ プロジェクトをビルドして実行するには**</span><span class="sxs-lookup"><span data-stu-id="31b8f-250">**To build and run the tab project**</span></span>

1. <span data-ttu-id="31b8f-251">ソース コードを取得した後、[プロジェクト] に移動Visual Studioプロジェクトまたはソリューションを開 **く] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-251">After you have the source code, go to Visual Studio and select **Open a project or solution**.</span></span>
1. <span data-ttu-id="31b8f-252">タブ アプリケーション ディレクトリに移動し **、ChannelGroupTab.sln を開きます**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-252">Go to the tab application directory and open **ChannelGroupTab.sln**.</span></span>
1. <span data-ttu-id="31b8f-253">アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-253">To build and run your application, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="31b8f-254">ブラウザーで、次の URL に移動し、アプリケーションが正しく読み込まれているか確認します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-254">In a browser, go to the following URLs and verify the application loaded properly:</span></span>

    - `http://localhost:44355`
    - `http://localhost:44355/privacy`
    - `http://localhost:44355/tou`

### <a name="review-the-source-code"></a><span data-ttu-id="31b8f-255">ソース コードを確認する</span><span class="sxs-lookup"><span data-stu-id="31b8f-255">Review the source code</span></span>

#### <a name="startupcs"></a><span data-ttu-id="31b8f-256">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="31b8f-256">Startup.cs</span></span>

<span data-ttu-id="31b8f-257">このプロジェクトは、ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成され、セットアップ時に [詳細設定 **- HTTPS** 用に構成] チェック ボックスがオンになっています。</span><span class="sxs-lookup"><span data-stu-id="31b8f-257">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="31b8f-258">MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-258">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="31b8f-259">さらに、空のテンプレートでは既定では静的コンテンツの提供が有効ではないので、静的ファイル ミドルウェアは次のコードを使用してメソッド `Configure()` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-259">Additionally, the empty template does not enable serving static content by default, so the static files middleware is added to the `Configure()` method using the following code:</span></span>

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

#### <a name="wwwroot-folder"></a><span data-ttu-id="31b8f-260">wwwroot フォルダー</span><span class="sxs-lookup"><span data-stu-id="31b8f-260">wwwroot folder</span></span>

<span data-ttu-id="31b8f-261">この ASP.NET Core Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="31b8f-261">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

#### <a name="indexcshtml"></a><span data-ttu-id="31b8f-262">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="31b8f-262">Index.cshtml</span></span>

<span data-ttu-id="31b8f-263">ASP.NET Core Index と呼ばれるファイルをサイトの既定またはホーム ページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="31b8f-263">ASP.NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="31b8f-264">ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-264">When your browser URL points to the root of the site, **Index.cshtml** is displayed as the home page for your application.</span></span>

#### <a name="tabcs"></a><span data-ttu-id="31b8f-265">Tab.cs</span><span class="sxs-lookup"><span data-stu-id="31b8f-265">Tab.cs</span></span>

<span data-ttu-id="31b8f-266">このC#には、構成時に **Tab.cshtml** から呼び出されるメソッドが含まれる。</span><span class="sxs-lookup"><span data-stu-id="31b8f-266">This C# file contains a method that is called from **Tab.cshtml** during configuration.</span></span>

#### <a name="appmanifest-folder"></a><span data-ttu-id="31b8f-267">AppManifest フォルダー</span><span class="sxs-lookup"><span data-stu-id="31b8f-267">AppManifest folder</span></span>

<span data-ttu-id="31b8f-268">このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="31b8f-268">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="31b8f-269">192 x 192 ピクセルのフル カラー アイコン。 </span><span class="sxs-lookup"><span data-stu-id="31b8f-269">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="31b8f-270">**32** x 32 ピクセルの透明なアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="31b8f-270">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="31b8f-271">アプリ **manifest.js** を指定するファイルのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="31b8f-271">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="31b8f-272">これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。</span><span class="sxs-lookup"><span data-stu-id="31b8f-272">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="31b8f-273">ユーザーがタブの追加または更新を選択すると、Microsoft Teamsがマニフェストに読み込み、IFrame に埋め込み、タブに `configurationUrl` 表示されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-273">When a user chooses to add or update your tab, Microsoft Teams loads the `configurationUrl` specified in your manifest, embeds it in an IFrame, and renders it in your tab.</span></span>

#### <a name="csproj"></a><span data-ttu-id="31b8f-274">.csproj</span><span class="sxs-lookup"><span data-stu-id="31b8f-274">.csproj</span></span>

<span data-ttu-id="31b8f-275">[ソリューション エクスプローラー Visual Studioで、プロジェクトを右クリックし、[ファイルの編集] Project **します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-275">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="31b8f-276">ファイルの最後に、アプリケーションのビルド時に zip フォルダーを作成および更新する次のコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-276">At the end of the file, you see the following code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="establish-a-secure-tunnel-to-your-tab-for-teams"></a><span data-ttu-id="31b8f-277">タブにセキュリティで保護されたトンネルを確立し、Teams</span><span class="sxs-lookup"><span data-stu-id="31b8f-277">Establish a secure tunnel to your tab for Teams</span></span>

<span data-ttu-id="31b8f-278">Microsoft Teamsはクラウドベースの製品であり、HTTPS エンドポイントを使用してタブ コンテンツをクラウドから利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-278">Microsoft Teams is a cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="31b8f-279">Teamsはローカル ホスティングを許可しない。</span><span class="sxs-lookup"><span data-stu-id="31b8f-279">Teams does not allow local hosting.</span></span> <span data-ttu-id="31b8f-280">タブをパブリック URL に発行するか、ローカル ポートをインターネットに接続する URL に公開するプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-280">You must either publish your tab to a public URL, or use a proxy that exposes your local port to an internet-facing URL.</span></span>

<span data-ttu-id="31b8f-281">タブをテストするには [、ngrok を使用します](https://ngrok.com/docs)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-281">To test your tab, use [ngrok](https://ngrok.com/docs).</span></span> <span data-ttu-id="31b8f-282">ngrok がコンピューターで実行されている間、サーバーの Web エンドポイントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-282">Your server's web endpoints are available while ngrok is running on your computer.</span></span> <span data-ttu-id="31b8f-283">ngrok の無料版では、ngrok を閉じると、次回起動する URL が異なります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-283">In the free version of ngrok, if you close ngrok, the URLs are different the next time you start it.</span></span>

- <span data-ttu-id="31b8f-284">プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-284">At a command prompt in the root of your project directory, run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44355 -host-header="localhost:44355"
    ```

- <span data-ttu-id="31b8f-285">Ngrok は、インターネットからの要求をリッスンし、ポート 44355 で実行されているアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="31b8f-285">Ngrok listens to requests from the internet and routes them to your application when it is running on port 44355.</span></span> <span data-ttu-id="31b8f-286">`https://y8rCgT2b.ngrok.io/` **y8rCgT2b** が ngrok の英数字 HTTPS URL に置き換えられる場所に似ている必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-286">It should resemble `https://y8rCgT2b.ngrok.io/` where **y8rCgT2b** is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="31b8f-287">ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。</span><span class="sxs-lookup"><span data-stu-id="31b8f-287">Ensure that you keep the command prompt with ngrok running and make a note of the URL.</span></span>

### <a name="update-your-application"></a><span data-ttu-id="31b8f-288">アプリケーションを更新する</span><span class="sxs-lookup"><span data-stu-id="31b8f-288">Update your application</span></span>

<span data-ttu-id="31b8f-289">**Tab.cshtml 内** では、アプリケーションは、赤または灰色のアイコンでタブを表示するための 2 つのオプション ボタンをユーザーに表示します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-289">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="31b8f-290">[灰色の **選択] または** **[赤の選択**] ボタンを選択すると、構成ページの [保存] ボタンがそれぞれトリガーまたは設定され、 `saveGray()` `saveRed()` `settings.setValidityState(true)` 有効になります。 </span><span class="sxs-lookup"><span data-stu-id="31b8f-290">Choosing the **Select Gray** or **Select Red** button triggers `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="31b8f-291">このコードをTeams構成要件を完了し、インストールを続行できます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-291">This code lets Teams know that you have completed the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="31b8f-292">のパラメーター `settings.setSettings` が設定されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-292">The parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="31b8f-293">最後に、コンテンツ URL が正常に解決されたことを示 `saveEvent.notifySuccess()` すために呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-293">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has been successfully resolved.</span></span>

#### <a name="_layoutcshtml"></a><span data-ttu-id="31b8f-294">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="31b8f-294">_Layout.cshtml</span></span>

<span data-ttu-id="31b8f-295">タブを JavaScript クライアントにTeamsするには **、JavaScript** クライアント SDK をMicrosoft Teamsし、ページの読み込み後に呼び出 `microsoftTeams.initialize()` しを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-295">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="31b8f-296">次に、タブとクライアントがTeams方法を示します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-296">This is how your tab and the Teams client communicate:</span></span>

<span data-ttu-id="31b8f-297">[共有] **フォルダーに移動** し **、_Layout.cshtml** を開き、次の項目をタグに追加 `<head>` します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-297">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

> [!IMPORTANT]
> <span data-ttu-id="31b8f-298">URL は最新バージョンを表すので、このページの URL をコピーして `<script src="...">` 貼り付けは行ないます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-298">Do not copy and paste the `<script src="...">` URLs from this page, as they do not represent the latest version.</span></span> <span data-ttu-id="31b8f-299">SDK の最新バージョンを取得するには、常に[JavaScript API Microsoft Teams移動します](https://www.npmjs.com/package/@microsoft/teams-js)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-299">To get the latest version of the SDK, always go to [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

#### <a name="tabcshtml"></a><span data-ttu-id="31b8f-300">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="31b8f-300">Tab.cshtml</span></span>

<span data-ttu-id="31b8f-301">**Tab.cshtml を更新するには**</span><span class="sxs-lookup"><span data-stu-id="31b8f-301">**To update Tab.cshtml**</span></span>

1. <span data-ttu-id="31b8f-302">**[Tab.cshtml] を** 開Visual Studio埋め込みファイルを更新します `<script>` 。</span><span class="sxs-lookup"><span data-stu-id="31b8f-302">Open **Tab.cshtml** in Visual Studio and update the embedded `<script>`.</span></span>

1. <span data-ttu-id="31b8f-303">スクリプトの上部で、 を呼び出します `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="31b8f-303">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

1. <span data-ttu-id="31b8f-304">タブへの HTTPS ngrok URL を使用して、各関数の値 `websiteUrl` `contentUrl` と値を更新します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-304">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

    <span data-ttu-id="31b8f-305">これで **、y8rCgT2b** が ngrok URL に置き換えられた次のコードを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-305">Your code should now include the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

    ```javascript
        microsoftTeams.initialize();

        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
        });
        }
    ```

1. <span data-ttu-id="31b8f-306">更新された **Tab.cshtml を保存します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-306">Save the updated **Tab.cshtml**.</span></span>

### <a name="build-and-run-your-application-for-teams"></a><span data-ttu-id="31b8f-307">アプリケーションをビルドして実行Teams</span><span class="sxs-lookup"><span data-stu-id="31b8f-307">Build and run your application for Teams</span></span>

<span data-ttu-id="31b8f-308">**アプリケーションをビルドして実行するには**</span><span class="sxs-lookup"><span data-stu-id="31b8f-308">**To build and run your application**</span></span>

1. <span data-ttu-id="31b8f-309">このVisual Studio F5 キー **を押するか、[** デバッグ] メニューから [**デバッグ** の開始]**を選択** します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-309">In Visual Studio, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="31b8f-310">ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を介してコンテンツ ページに移動して **、ngrok** が正常に実行され、正常に動作されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-310">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="31b8f-311">この記事で示す手順を完了するには、Visual Studioと ngrok の両方でアプリケーションを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-311">You need to have both your application in Visual Studio and ngrok running to complete the steps provided in this article.</span></span> <span data-ttu-id="31b8f-312">アプリケーションの実行を停止する必要がある場合Visual Studio **ngrok を実行し続ける必要があります**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-312">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="31b8f-313">アプリケーションの要求がアプリケーションで再起動されると、アプリケーションの要求をリッスンしてVisual Studio。</span><span class="sxs-lookup"><span data-stu-id="31b8f-313">It listens and resumes routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="31b8f-314">ngrok サービスを再起動する必要がある場合は、新しい URL が返され、新しい URL でアプリケーションを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-314">If you have to restart the ngrok service it returns a new URL and you have to update your application with the new URL.</span></span>

### <a name="upload-your-tab-for-teams"></a><span data-ttu-id="31b8f-315">アップロードのタブを開Teams</span><span class="sxs-lookup"><span data-stu-id="31b8f-315">Upload your tab for Teams</span></span>

> [!NOTE]
> <span data-ttu-id="31b8f-316">App Studio を使用すると、ファイル上のmanifest.js **を編集** し、完成したパッケージをファイルにアップロードTeams。</span><span class="sxs-lookup"><span data-stu-id="31b8f-316">App Studio can be used to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="31b8f-317">また、手動でファイルのmanifest.js **編集** することもできます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-317">You can also manually edit the **manifest.json** file.</span></span> <span data-ttu-id="31b8f-318">その場合は、ソリューションを再度ビルドして、アップロードする **tab.zip作成してください** 。</span><span class="sxs-lookup"><span data-stu-id="31b8f-318">If you do, ensure that you build the solution again to create the **tab.zip** file to upload.</span></span>

<span data-ttu-id="31b8f-319">**App Studio でタブをアップロードするには**</span><span class="sxs-lookup"><span data-stu-id="31b8f-319">**To upload your tab with App Studio**</span></span>

1. <span data-ttu-id="31b8f-320">[次へ] にMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="31b8f-320">Go to Microsoft Teams.</span></span> <span data-ttu-id="31b8f-321">Web ベースのバージョン [を使用する](https://teams.microsoft.com)場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-321">If you use the [web-based version](https://teams.microsoft.com), you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="31b8f-322">[App **Studio] に移動し** 、[マニフェスト エディター **] タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-322">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="31b8f-323">[ **マニフェスト エディターで既存のアプリ** をインポートする] **を選択して** 、タブのアプリ パッケージの更新を開始します。ソース コードには、部分的に完全なマニフェストが付属しています。</span><span class="sxs-lookup"><span data-stu-id="31b8f-323">Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="31b8f-324">アプリ パッケージの名前は次 **tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="31b8f-324">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="31b8f-325">これは、次のパスから使用できます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-325">It is available from the following path:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="31b8f-326">アップロードtab.zipApp  Studio にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="31b8f-326">Upload **tab.zip** to App Studio.</span></span>

#### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="31b8f-327">マニフェスト エディターを使用してアプリ パッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="31b8f-327">Update your app package with Manifest editor</span></span>

<span data-ttu-id="31b8f-328">アプリ パッケージを App Studio にアップロードしたら、アプリ パッケージを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-328">After you have uploaded your app package into App Studio, you must configure it.</span></span>

<span data-ttu-id="31b8f-329">マニフェスト エディターのウェルカム ページの右側のパネルで、新しくインポートしたタブのタイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-329">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="31b8f-330">マニフェスト エディターの左側に手順の一覧が表示され、右側には、各手順の値が必要なプロパティの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-330">There is a list of steps on the left side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="31b8f-331">この情報の多くが、ユーザーのmanifest.js **によって** 提供されますが、更新する必要があるフィールドがあります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-331">Much of the information has been provided by your **manifest.json** but there are fields that you must update.</span></span>

##### <a name="details-app-details"></a><span data-ttu-id="31b8f-332">詳細: アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="31b8f-332">Details: App details</span></span>

<span data-ttu-id="31b8f-333">[アプリ **の詳細] セクションで、次の内容を実行** します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-333">In the **App details** section:</span></span>

1. <span data-ttu-id="31b8f-334">**[Id]** で、[**生成] を** 選択して、プレースホルダー ID をタブに必要な GUID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-334">Under **Identification**, select **Generate** to replace the placeholder ID with the required GUID for your tab.</span></span>

1. <span data-ttu-id="31b8f-335">[**開発者情報] で\*\*\*\*、ngrok** HTTPS URL を使用して Web **サイトを** 更新します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-335">Under **Developer information**, update **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="31b8f-336">[**アプリの URL] で**、[プライバシーに関する **声明] と**[使用条件] を更新して、>。 `https://<yourngrokurl>/privacy`  `https://<yourngrokurl>/tou`</span><span class="sxs-lookup"><span data-stu-id="31b8f-336">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

##### <a name="capabilities-tabs"></a><span data-ttu-id="31b8f-337">機能: タブ</span><span class="sxs-lookup"><span data-stu-id="31b8f-337">Capabilities: Tabs</span></span>

<span data-ttu-id="31b8f-338">[タブ **] セクションで、次の設定を** 行います。</span><span class="sxs-lookup"><span data-stu-id="31b8f-338">In the **Tabs** section:</span></span>

1. <span data-ttu-id="31b8f-339">[チーム **] タブで、[** 追加] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-339">Under **Team tab**, select **Add**.</span></span>

1. <span data-ttu-id="31b8f-340">[チーム **] タブの** ポップアップ ウィンドウで、構成 **URL をに更新** します `https://<yourngrokurl>/tab` 。</span><span class="sxs-lookup"><span data-stu-id="31b8f-340">In the **Team tab** pop-up window, update the **Configuration URL** to `https://<yourngrokurl>/tab`.</span></span>

1. <span data-ttu-id="31b8f-341">[構成を **更新できますか] 、[\*\*\*\*チーム]**、および [グループ **チャット]** チェック ボックスがオンになっていることを確認し、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-341">Ensure the **Can update configuration?**, **Team**, and **Group chat** checkboxes are selected and select **Save**.</span></span>

##### <a name="finish-domains-and-permissions"></a><span data-ttu-id="31b8f-342">完了: ドメインとアクセス許可</span><span class="sxs-lookup"><span data-stu-id="31b8f-342">Finish: Domains and permissions</span></span>

<span data-ttu-id="31b8f-343">[ドメイン **とアクセス許可**] セクションで、タブのドメインには、HTTPS プレフィックスのない ngrok URL が含まれている必要があります `<yourngrokurl>.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="31b8f-343">In the **Domains and permissions** section, **Domains from your tabs** must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="31b8f-344">完了: テストと配布</span><span class="sxs-lookup"><span data-stu-id="31b8f-344">Finish: Test and distribute</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31b8f-345">右側の [説明] **で**、次の警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-345">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="31b8f-346">&#9888; "**'validDomains' 配列にはトンネリング サイトを含めできません。..**</span><span class="sxs-lookup"><span data-stu-id="31b8f-346">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
> <span data-ttu-id="31b8f-347">この警告は、タブのテスト中に無視できます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-347">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="31b8f-348">[テストと **配布] セクションで、[** インストール] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-348">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="31b8f-349">ポップアップ ダイアログ ボックスで、[チームに追加] を選択するか、ドロップダウンから [チャットに追加 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-349">In the pop-up dialog box, select **Add to a team** or from the drop-down, select **Add to a chat**.</span></span>

1. <span data-ttu-id="31b8f-350">タブを表示するチームまたはチャットを選択し、[タブの設定 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-350">Choose the team or chat where you want the tab to be displayed and select **Set up a tab**.</span></span>

1. <span data-ttu-id="31b8f-351">次のポップアップ ダイアログ ボックスで、[灰色の選択]または [赤の選択] を選択し、[保存] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-351">In the next pop-up dialog box, choose either **Select Gray** or **Select Red**, and select **Save**.</span></span>

1. <span data-ttu-id="31b8f-352">タブを表示するには、タブをインストールしたチームまたはチャットに移動し、タブ バーから選択します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-352">To view your tab, go to the team or chat where you installed the tab, and select it from the tab bar.</span></span> <span data-ttu-id="31b8f-353">構成時に選択したページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-353">The page that you chose during configuration is displayed.</span></span>

    ![[チャネル] タブの ASPNET がアップロードされました](../../assets/images/tab-images/channeltabaspnetuploaded.png)

# <a name="aspnet-core-mvc"></a>[<span data-ttu-id="31b8f-355">ASP.NET CoreMVC</span><span class="sxs-lookup"><span data-stu-id="31b8f-355">ASP.NET Core MVC</span></span>](#tab/aspnetcoremvc)

### <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="31b8f-356">MVC を使用してカスタム チャネルまたはグループ タブ ASP.NET Coreする</span><span class="sxs-lookup"><span data-stu-id="31b8f-356">Create a custom channel or group tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="31b8f-357">Core MVC を使用して、カスタム チャネルまたはグループ タブC#作成 ASP.Net 作成できます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-357">You can create a custom channel or group tab using C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="31b8f-358">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)は、アプリ マニフェストを最終的に作成し、タブを展開してアプリ マニフェストに展開Teams。</span><span class="sxs-lookup"><span data-stu-id="31b8f-358">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) is also used to finalize your app manifest and deploy your tab to Teams.</span></span>

### <a name="prerequisites-for-custom-channel-or-group-tab"></a><span data-ttu-id="31b8f-359">カスタム チャネルまたはグループ タブの前提条件</span><span class="sxs-lookup"><span data-stu-id="31b8f-359">Prerequisites for custom channel or group tab</span></span>

- <span data-ttu-id="31b8f-360">カスタム アプリのアップロードを許可Microsoft 365を有効にしたチームとテナント **が必要** です。</span><span class="sxs-lookup"><span data-stu-id="31b8f-360">You must have a Microsoft 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="31b8f-361">詳細については、「prepare [your Office 365 テナント」を参照してください](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-361">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="31b8f-362">現在アカウントを持Microsoft 365場合は、Microsoft Developer Program を通じて無料サブスクリプションに[サインアップできます](https://developer.microsoft.com/en-us/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-362">If you do not currently have a Microsoft 365 account, you can sign up for a free subscription through the [Microsoft Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program).</span></span> <span data-ttu-id="31b8f-363">サブスクリプションは、継続的な開発に使用している限りアクティブなままです。</span><span class="sxs-lookup"><span data-stu-id="31b8f-363">The subscription remains active as long as you are using it for ongoing development.</span></span>

- <span data-ttu-id="31b8f-364">App Studio を使用してアプリケーションをインポートし、Teams。</span><span class="sxs-lookup"><span data-stu-id="31b8f-364">Use App Studio to import your application to Teams.</span></span> <span data-ttu-id="31b8f-365">App Studio をインストールするには、アプリアプリの左下隅にある [アプリ ストア アプリ] を選択Teams App Studio を ![ ](~/assets/images/tab-images/storeApp.png) **検索します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-365">To install App Studio, select **Apps** ![Store App](~/assets/images/tab-images/storeApp.png) at the lower left corner of the Teams app, and search for **App Studio**.</span></span> <span data-ttu-id="31b8f-366">タイルを見つけたら、タイルを選択し、ポップアップ ダイアログ ボックスで [追加] を選択してインストールします。</span><span class="sxs-lookup"><span data-stu-id="31b8f-366">After you find the tile, select it and choose **Add** in the pop-up dialog box to install it.</span></span>

<span data-ttu-id="31b8f-367">さらに、このプロジェクトでは、次のコードが開発環境にインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-367">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="31b8f-368">現在のバージョンの IDE **Visual Studio.NET CORE** クロスプラットフォーム開発ワークロードがインストールされています。</span><span class="sxs-lookup"><span data-stu-id="31b8f-368">The current version of the Visual Studio IDE with the **.NET CORE cross-platform development** workload installed.</span></span> <span data-ttu-id="31b8f-369">まだインストールされていない場合はVisual Studio最新バージョンを無料でダウンロード[Microsoft Visual Studio Communityインストールできます](https://visualstudio.microsoft.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-369">If you do not already have Visual Studio, you can download and install the latest [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) version for free.</span></span>

- <span data-ttu-id="31b8f-370">[ngrok](https://ngrok.com)リバース プロキシ ツール。</span><span class="sxs-lookup"><span data-stu-id="31b8f-370">The [ngrok](https://ngrok.com) reverse proxy tool.</span></span> <span data-ttu-id="31b8f-371">ngrok を使用して、ローカルで実行中の Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-371">Use ngrok to create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="31b8f-372">[ngrok をダウンロードできます](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="31b8f-372">You can [download ngrok](https://ngrok.com/download).</span></span>

### <a name="get-the-source-code"></a><span data-ttu-id="31b8f-373">ソース コードを取得する</span><span class="sxs-lookup"><span data-stu-id="31b8f-373">Get the source code</span></span>

<span data-ttu-id="31b8f-374">コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-374">At a command prompt, create a new directory for your tab project.</span></span> <span data-ttu-id="31b8f-375">簡単な [チャネル グループ タブ](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) プロジェクトは、開始するために提供されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-375">A simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) project is provided to get you started.</span></span> <span data-ttu-id="31b8f-376">次のコマンドを使用して、サンプル リポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-376">Clone the sample repository into your new directory using the following command:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="31b8f-377">または、zip フォルダーをダウンロードしてファイルを抽出して、ソース コードを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-377">Alternately, you can retrieve the source code by downloading the zip folder and extracting the files.</span></span>

<span data-ttu-id="31b8f-378">**タブ プロジェクトをビルドして実行するには**</span><span class="sxs-lookup"><span data-stu-id="31b8f-378">**To build and run the tab project**</span></span>

1. <span data-ttu-id="31b8f-379">ソース コードを取得した後、[プロジェクト] に移動Visual Studioプロジェクトまたはソリューションを開 **く] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-379">After you have the source code, go to Visual Studio and select **Open a project or solution**.</span></span>
1. <span data-ttu-id="31b8f-380">タブ アプリケーション ディレクトリに移動し **、ChannelGroupTabMVC.sln を開きます**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-380">Go to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>
1. <span data-ttu-id="31b8f-381">アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-381">To build and run your application, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="31b8f-382">ブラウザーで、次の URL に移動し、アプリケーションが正しく読み込まれたか確認します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-382">In a browser, navigate to the following URLs and verify that the application loaded properly:</span></span>

    - `http://localhost:44360`
    - `http://localhost:44360/privacy`
    - `http://localhost:44360/tou`

### <a name="review-the-source-code"></a><span data-ttu-id="31b8f-383">ソース コードを確認する</span><span class="sxs-lookup"><span data-stu-id="31b8f-383">Review the source code</span></span>

#### <a name="startupcs"></a><span data-ttu-id="31b8f-384">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="31b8f-384">Startup.cs</span></span>

<span data-ttu-id="31b8f-385">このプロジェクトは、ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成され、セットアップ時に [詳細設定 **- HTTPS** 用に構成] チェック ボックスがオンになっています。</span><span class="sxs-lookup"><span data-stu-id="31b8f-385">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="31b8f-386">MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-386">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="31b8f-387">さらに、空のテンプレートでは既定では静的コンテンツの提供が有効ではないので、静的ファイル ミドルウェアは次のコードを使用してメソッド `Configure()` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-387">Additionally, the empty template does not enable serving static content by default, so the static files middleware is added to the `Configure()` method using the following code:</span></span>

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

#### <a name="wwwroot-folder"></a><span data-ttu-id="31b8f-388">wwwroot フォルダー</span><span class="sxs-lookup"><span data-stu-id="31b8f-388">wwwroot folder</span></span>

<span data-ttu-id="31b8f-389">この ASP.NET Core Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="31b8f-389">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

#### <a name="appmanifest-folder"></a><span data-ttu-id="31b8f-390">AppManifest フォルダー</span><span class="sxs-lookup"><span data-stu-id="31b8f-390">AppManifest folder</span></span>

<span data-ttu-id="31b8f-391">このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="31b8f-391">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="31b8f-392">192 x 192 ピクセルのフル カラー アイコン。 </span><span class="sxs-lookup"><span data-stu-id="31b8f-392">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="31b8f-393">**32** x 32 ピクセルの透明なアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="31b8f-393">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="31b8f-394">アプリ **manifest.js** を指定するファイルのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="31b8f-394">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="31b8f-395">これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。</span><span class="sxs-lookup"><span data-stu-id="31b8f-395">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

#### <a name="csproj"></a><span data-ttu-id="31b8f-396">.csproj</span><span class="sxs-lookup"><span data-stu-id="31b8f-396">.csproj</span></span>

<span data-ttu-id="31b8f-397">[ソリューション エクスプローラー Visual Studioで、プロジェクトを右クリックし、[ファイルの編集] Project **します**。</span><span class="sxs-lookup"><span data-stu-id="31b8f-397">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="31b8f-398">ファイルの最後に、アプリケーションのビルド時に zip フォルダーを作成および更新する次のコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-398">At the end of the file you see the following code that creates and updates your zip folder when the application builds:</span></span>

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

#### <a name="models"></a><span data-ttu-id="31b8f-399">モデル</span><span class="sxs-lookup"><span data-stu-id="31b8f-399">Models</span></span>

<span data-ttu-id="31b8f-400">**ChannelGroup.cs** は、構成中にコントローラーから呼び出される Message オブジェクトとメソッドを示します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-400">**ChannelGroup.cs** presents a Message object and methods that will be called from the controllers during configuration.</span></span>

#### <a name="views"></a><span data-ttu-id="31b8f-401">ビュー</span><span class="sxs-lookup"><span data-stu-id="31b8f-401">Views</span></span>

<span data-ttu-id="31b8f-402">次に示すのは、MVC の ASP.NET Coreです。</span><span class="sxs-lookup"><span data-stu-id="31b8f-402">These are the different views in ASP.NET Core MVC:</span></span>

* <span data-ttu-id="31b8f-403">ホーム: ASP.NET Core Index と呼ばれるファイルをサイトの既定またはホーム ページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="31b8f-403">Home: ASP.NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="31b8f-404">ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-404">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

* <span data-ttu-id="31b8f-405">共有: 部分ビュー マークアップ **_Layout.cshtml** には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-405">Shared: The partial view markup **_Layout.cshtml** contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="31b8f-406">また、ライブラリのTeamsします。</span><span class="sxs-lookup"><span data-stu-id="31b8f-406">It will also reference the Teams Library.</span></span>

#### <a name="controllers"></a><span data-ttu-id="31b8f-407">コントローラー</span><span class="sxs-lookup"><span data-stu-id="31b8f-407">Controllers</span></span>

<span data-ttu-id="31b8f-408">コントローラーは、プロパティを `ViewBag` 使用してビューに動的に値を転送します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-408">The controllers use the `ViewBag` property to transfer values dynamically to the views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="31b8f-409">プロジェクト ディレクトリのルートでコマンド プロンプトを開き、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-409">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:443560 -host-header="localhost:44360"
    ```

* <span data-ttu-id="31b8f-410">Ngrok はインターネットからの要求をリッスンし、ポート 44355 で実行されているアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="31b8f-410">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span> <span data-ttu-id="31b8f-411">`https://y8rCgT2b.ngrok.io/` **y8rCgT2b** が ngrok の英数字 HTTPS URL に置き換えられる場所に似ている必要があります。</span><span class="sxs-lookup"><span data-stu-id="31b8f-411">It should resemble `https://y8rCgT2b.ngrok.io/` where **y8rCgT2b** is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="31b8f-412">ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。</span><span class="sxs-lookup"><span data-stu-id="31b8f-412">Ensure that you keep the command prompt with ngrok running and make a note of the URL.</span></span>

### <a name="update-your-application"></a><span data-ttu-id="31b8f-413">アプリケーションを更新する</span><span class="sxs-lookup"><span data-stu-id="31b8f-413">Update your application</span></span>

<span data-ttu-id="31b8f-414">**Tab.cshtml 内** では、アプリケーションは、赤または灰色のアイコンでタブを表示するための 2 つのオプション ボタンをユーザーに表示します。</span><span class="sxs-lookup"><span data-stu-id="31b8f-414">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="31b8f-415">[灰色の **選択] または** **[赤の選択**] ボタンを選択すると、構成ページで [保存] ボタンが設定され、有効になります `saveGray()` `saveRed()` `settings.setValidityState(true)` 。 </span><span class="sxs-lookup"><span data-stu-id="31b8f-415">Choosing the **Select Gray** or **Select Red** button, triggers `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="31b8f-416">このコードをTeams構成要件を完了し、インストールを続行できます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-416">This code lets Teams know that you have completed the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="31b8f-417">保存時に、のパラメーターが `settings.setSettings` 設定されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-417">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="31b8f-418">最後に、コンテンツ URL が正常に解決されたことを示 `saveEvent.notifySuccess()` すために呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="31b8f-418">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has been successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

---

## <a name="see-also"></a><span data-ttu-id="31b8f-419">関連項目</span><span class="sxs-lookup"><span data-stu-id="31b8f-419">See also</span></span>

* [<span data-ttu-id="31b8f-420">Teamsタブ</span><span class="sxs-lookup"><span data-stu-id="31b8f-420">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="31b8f-421">プライベート タブを作成する</span><span class="sxs-lookup"><span data-stu-id="31b8f-421">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="31b8f-422">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="31b8f-422">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="31b8f-423">アダプティブ カードを使用してタブをビルドする</span><span class="sxs-lookup"><span data-stu-id="31b8f-423">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="next-step"></a><span data-ttu-id="31b8f-424">次の手順</span><span class="sxs-lookup"><span data-stu-id="31b8f-424">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="31b8f-425">コンテンツ ページを作成する</span><span class="sxs-lookup"><span data-stu-id="31b8f-425">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
