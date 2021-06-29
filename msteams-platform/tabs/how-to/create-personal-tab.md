---
title: プライベート タブを作成する
author: laujan
description: Yeoman Generator を使用して個人用タブを作成するクイック スタート Microsoft Teams。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 47ed3027f936366964871733e78c7a43851ffb99
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179870"
---
# <a name="create-a-personal-tab"></a><span data-ttu-id="ef5da-103">プライベート タブを作成する</span><span class="sxs-lookup"><span data-stu-id="ef5da-103">Create a personal tab</span></span>

## <a name="create-a-custom-personal-tab"></a><span data-ttu-id="ef5da-104">ユーザー設定の個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="ef5da-104">Create a custom personal tab</span></span>

<span data-ttu-id="ef5da-105">[個人用] タブは、MVC Node.js Yeoman Generator、ASP.NET Core、または ASP.NET Coreできます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-105">You can create a personal tab using Node.js and the Yeoman Generator, ASP.NET Core, or ASP.NET Core MVC.</span></span>

# <a name="nodejs"></a>[<span data-ttu-id="ef5da-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="ef5da-106">Node.js</span></span>](#tab/nodejs)

### <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator"></a><span data-ttu-id="ef5da-107">ユーザー設定と Yeoman Generator を使用Node.js個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="ef5da-107">Create a custom personal tab using Node.js and the Yeoman Generator</span></span>

> [!NOTE]
> <span data-ttu-id="ef5da-108">この記事では、Microsoft OfficeDev Microsoft Teamsリポジトリにある最初のアプリ[Wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)のビルドにGitHubします。</span><span class="sxs-lookup"><span data-stu-id="ef5da-108">This article follows the steps outlined in the [build your first Microsoft Teams app](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="ef5da-109">Yeoman ジェネレーターを使用してカスタム[個人用Teams作成できます](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-109">You can create a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="ef5da-110">アプリケーションは、アプリケーションにもアップロードTeams。</span><span class="sxs-lookup"><span data-stu-id="ef5da-110">The application is also uploaded to Teams.</span></span>

### <a name="prerequisites-for-teams-apps"></a><span data-ttu-id="ef5da-111">アプリのTeams前提条件</span><span class="sxs-lookup"><span data-stu-id="ef5da-111">Prerequisites for Teams apps</span></span>

<span data-ttu-id="ef5da-112">次の前提条件について理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-112">You must have an understanding of the following prerequisites:</span></span>

- <span data-ttu-id="ef5da-113">カスタム アプリのアップロードを許可Office 365を有効にしたテナントとチーム **が構成されている必要** があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-113">You must have an Office 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="ef5da-114">詳細については、「prepare [your Office 365 テナント」を参照してください](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-114">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ef5da-115">ユーザーアカウントをお持ちOffice 365場合は、開発者プログラムから無料サブスクリプションOffice 365できます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-115">If you do not have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="ef5da-116">サブスクリプションは、継続的な開発に使用している限りアクティブなままです。</span><span class="sxs-lookup"><span data-stu-id="ef5da-116">The subscription remains active as long as you are using it for ongoing development.</span></span> <span data-ttu-id="ef5da-117">「[開発者プログラムへようこそOffice 365」を参照してください](/office/developer-program/microsoft-365-developer-program)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-117">See [welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="ef5da-118">さらに、このプロジェクトでは、次のコードが開発環境にインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-118">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="ef5da-119">任意のテキスト エディターまたは IDE。</span><span class="sxs-lookup"><span data-stu-id="ef5da-119">Any text editor or IDE.</span></span> <span data-ttu-id="ef5da-120">無料でインストール[して使用Visual Studio Code](https://code.visualstudio.com/download)できます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-120">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="ef5da-121">[Node.js/npm](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="ef5da-121">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="ef5da-122">最新の LTS バージョンを使用します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-122">Use the latest LTS version.</span></span> <span data-ttu-id="ef5da-123">ノード ノード パッケージ マネージャー (npm) がシステムにインストールされ、システムにインストールNode.js。</span><span class="sxs-lookup"><span data-stu-id="ef5da-123">The Node Package Manager (npm) is installed in your system with the installation of Node.js.</span></span>

- <span data-ttu-id="ef5da-124">インストールが正常に完了したらNode.jsに次のコマンド プロンプトを入力して [、Yeoman](https://yeoman.io/) パッケージと [gulp-cli](https://www.npmjs.com/package/gulp-cli) パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="ef5da-124">After you have successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by entering the following in your command prompt:</span></span>

    ```bash
    npm install yo gulp-cli --global
    ```

- <span data-ttu-id="ef5da-125">コマンド プロンプトにMicrosoft Teamsを入力して、アプリ ジェネレーターをインストールします。</span><span class="sxs-lookup"><span data-stu-id="ef5da-125">Install the Microsoft Teams Apps generator by entering the following in your command prompt:</span></span>

    ```bash
    npm install generator-teams --global
    ```

### <a name="generate-your-project"></a><span data-ttu-id="ef5da-126">プロジェクトを生成する</span><span class="sxs-lookup"><span data-stu-id="ef5da-126">Generate your project</span></span>

<span data-ttu-id="ef5da-127">**プロジェクトを生成するには**</span><span class="sxs-lookup"><span data-stu-id="ef5da-127">**To generate your project**</span></span>

1. <span data-ttu-id="ef5da-128">コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-128">At a command prompt, create a new directory for your tab project.</span></span>

1. <span data-ttu-id="ef5da-129">ジェネレーターを起動するには、新しいディレクトリに移動し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-129">To start the generator, go to your new directory and enter the following command:</span></span>

    ```bash
    yo teams
    ```

1. <span data-ttu-id="ef5da-130">次に、アプリケーションのファイルファイルで使用される一連の値manifest.js **指定** します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-130">Next, provide a series of values that are used in your application's **manifest.json** file:</span></span>

    ![ジェネレーターの開くスクリーンショット](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <span data-ttu-id="ef5da-132">**ソリューション名は何ですか?**</span><span class="sxs-lookup"><span data-stu-id="ef5da-132">**What is your solution name?**</span></span>

    <span data-ttu-id="ef5da-133">これはプロジェクト名です。</span><span class="sxs-lookup"><span data-stu-id="ef5da-133">This is your project name.</span></span> <span data-ttu-id="ef5da-134">Enter キーを選択すると、候補の名前を **受け入** れできます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-134">You can accept the suggested name by selecting the **Enter** key.</span></span>

    <span data-ttu-id="ef5da-135">**ファイルをどこに保存しますか?**</span><span class="sxs-lookup"><span data-stu-id="ef5da-135">**Where do you want to place the files?**</span></span>

    <span data-ttu-id="ef5da-136">現在、プロジェクト ディレクトリにいます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-136">You are currently in your project directory.</span></span> <span data-ttu-id="ef5da-137">**[Enter] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-137">Select **Enter**.</span></span>

    <span data-ttu-id="ef5da-138">**アプリ プロジェクトMicrosoft Teamsタイトル**</span><span class="sxs-lookup"><span data-stu-id="ef5da-138">**Title of your Microsoft Teams app project?**</span></span>

    <span data-ttu-id="ef5da-139">これはアプリ パッケージ名であり、アプリ マニフェストと説明で使用されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-139">This is your app package name and will be used in the app manifest and description.</span></span> <span data-ttu-id="ef5da-140">タイトルを入力するか、Enter **を選択して** 既定の名前を受け入れる。</span><span class="sxs-lookup"><span data-stu-id="ef5da-140">Enter a title or select **Enter** to accept the default name.</span></span>

    <span data-ttu-id="ef5da-141">**(会社) の名前(最大 32 文字)**</span><span class="sxs-lookup"><span data-stu-id="ef5da-141">**Your (company) name? (max 32 characters)**</span></span>

    <span data-ttu-id="ef5da-142">会社名はアプリ マニフェストで使用されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-142">Your company name will be used in the app manifest.</span></span> <span data-ttu-id="ef5da-143">会社名を入力するか **、Enter を選択して** 既定の名前を受け入れる。</span><span class="sxs-lookup"><span data-stu-id="ef5da-143">Enter a company name or select **Enter** to accept the default name.</span></span>

    <span data-ttu-id="ef5da-144">**どのマニフェスト バージョンを使用しますか?**</span><span class="sxs-lookup"><span data-stu-id="ef5da-144">**Which manifest version would you like to use?**</span></span>

    <span data-ttu-id="ef5da-145">既定のスキーマを選択します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-145">Select the default schema.</span></span>

    <span data-ttu-id="ef5da-146">**クイック スキャフォールディング(Y/n)**</span><span class="sxs-lookup"><span data-stu-id="ef5da-146">**Quick scaffolding? (Y/n)**</span></span>

    <span data-ttu-id="ef5da-147">既定値は yes です。 **n と入力** して Microsoft パートナー ID を入力します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-147">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

    <span data-ttu-id="ef5da-148">**Microsoft パートナー ID をお持ちの場合は、Microsoft パートナー ID を入力してください。(スキップする場合は空白のままにする)**</span><span class="sxs-lookup"><span data-stu-id="ef5da-148">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

    <span data-ttu-id="ef5da-149">このフィールドは必須ではなく、Microsoft パートナー ネットワークに既に参加している場合にのみ [使用する必要があります](https://partner.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-149">This field is not required and should only be used if you are already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

    <span data-ttu-id="ef5da-150">**プロジェクトに何を追加しますか?**</span><span class="sxs-lookup"><span data-stu-id="ef5da-150">**What do you want to add to your project?**</span></span>

    <span data-ttu-id="ef5da-151">[ **選択] &ast; ( ) [タブ] をクリックします**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-151">Select **( &ast; ) A Tab**.</span></span>

    <span data-ttu-id="ef5da-152">**このソリューションをホストする URL**</span><span class="sxs-lookup"><span data-stu-id="ef5da-152">**The URL where you will host this solution?**</span></span>

    <span data-ttu-id="ef5da-153">既定では、ジェネレーターは Azure Web サイトの URL を提案します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-153">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="ef5da-154">アプリをローカルでテストしているだけなので、有効な URL は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="ef5da-154">You are only testing your app locally, therefore, a valid URL is not necessary.</span></span>

    <span data-ttu-id="ef5da-155">**アプリ/タブの読み込み時に読み込みインジケーターを表示しますか?**</span><span class="sxs-lookup"><span data-stu-id="ef5da-155">**Would you like show a loading indicator when your app/tab loads?**</span></span>

    <span data-ttu-id="ef5da-156">アプリ **またはタブ** の読み込み時に読み込みインジケーターを含めないを選択します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-156">Choose **not** to include a loading indicator when your app or tab loads.</span></span> <span data-ttu-id="ef5da-157">既定値は no で、n と **入力します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-157">The default is no, enter **n**.</span></span>

    <span data-ttu-id="ef5da-158">**個人用アプリをタブ ヘッダーバーなしでレンダリングしますか?**</span><span class="sxs-lookup"><span data-stu-id="ef5da-158">**Would you like personal apps to be rendered without a tab header-bar?**</span></span>

    <span data-ttu-id="ef5da-159">タブ **ヘッダー** バーなしでレンダリングする個人用アプリを含めないを選択します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-159">Choose **not** to include personal apps to be rendered without a tab header-bar.</span></span> <span data-ttu-id="ef5da-160">既定値はいいえ、n と **入力します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-160">Default is no, enter **n**.</span></span>

    <span data-ttu-id="ef5da-161">**テスト フレームワークと初期テストを含めるには?(y/N)**</span><span class="sxs-lookup"><span data-stu-id="ef5da-161">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

    <span data-ttu-id="ef5da-162">この **プロジェクトの** テスト フレームワークを含めないを選択します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-162">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="ef5da-163">既定値ははい、n と **入力します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-163">The default is yes, enter **n**.</span></span>

    <span data-ttu-id="ef5da-164">**テレメトリに Azure Applications インサイト使用しますか?(y/N)**</span><span class="sxs-lookup"><span data-stu-id="ef5da-164">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

    <span data-ttu-id="ef5da-165">[Azure **Application インサイト**[を含インサイト。](/azure/azure-monitor/app/app-insights-overview)</span><span class="sxs-lookup"><span data-stu-id="ef5da-165">Choose **not** to include [Azure Application Insights](/azure/azure-monitor/app/app-insights-overview).</span></span> <span data-ttu-id="ef5da-166">既定値は no です。 **n と入力します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-166">The default is no; enter **n**.</span></span>

    <span data-ttu-id="ef5da-167">**既定のタブ名 (最大 16 文字)?**</span><span class="sxs-lookup"><span data-stu-id="ef5da-167">**Default Tab Name (max 16 characters)?**</span></span>

    <span data-ttu-id="ef5da-168">タブの名前を指定します。このタブ名は、ファイルまたは URL パス コンポーネントとしてプロジェクト全体で使用されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-168">Name your tab. This tab name is used throughout your project as a file or URL path component.</span></span>

    <span data-ttu-id="ef5da-169">**作成するタブの種類**</span><span class="sxs-lookup"><span data-stu-id="ef5da-169">**What kind of Tab would you like to create?**</span></span>

    <span data-ttu-id="ef5da-170">矢印キーを使用して [個人用 ( **静的) ] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-170">Use the arrow keys to select **Personal (static)**.</span></span>

    <span data-ttu-id="ef5da-171">**タブに Azure AD のシングルサインオン サポートが必要ですか?**</span><span class="sxs-lookup"><span data-stu-id="ef5da-171">**Do you require Azure AD Single-Sign-On support for the tab?**</span></span>

    <span data-ttu-id="ef5da-172">タブ **に** Azure ADシングル サインオン のサポートを含めないを選択します。既定値ははい、n と **入力します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-172">Choose **not** to include Azure AD Single-Sign-On support for the tab. The default is yes, enter **n**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ef5da-173">パス コンポーネント **yourDefaultTabNameTab** は、ジェネレータで既定のタブ名にTab という単語を加えた値 **です**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-173">The path component **yourDefaultTabNameTab** is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
    >
    > <span data-ttu-id="ef5da-174">例: DefaultTabName: **MyTab**  >  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="ef5da-174">For example: DefaultTabName: **MyTab** > **/MyTabTab/**</span></span>

### <a name="add-a-personal-tab"></a><span data-ttu-id="ef5da-175">個人用タブの追加</span><span class="sxs-lookup"><span data-stu-id="ef5da-175">Add a personal tab</span></span>

<span data-ttu-id="ef5da-176">**このアプリケーションに個人用タブを追加するには、コンテンツ ページを作成し、既存のファイルを更新します。**</span><span class="sxs-lookup"><span data-stu-id="ef5da-176">**To add a personal tab to this application, create a content page, and update existing files**</span></span>

1. <span data-ttu-id="ef5da-177">コード エディターで、新しい HTML ファイルを作成し、lpersonal.htm **次** のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-177">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

1. <span data-ttu-id="ef5da-178">次 **personal.htmアプリケーション** の Web フォルダーに **l** を保存します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-178">Save **personal.html** in your application's **web** folder in the following location:</span></span>

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

1. <span data-ttu-id="ef5da-179">コード **manifest.jsで、** 次の場所から [オン] を開きます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-179">Open **manifest.json** from the following location in your code editor:</span></span>

    ```bash
    ./src/manifest/manifest.json/
    ```

1. <span data-ttu-id="ef5da-180">空の配列 ( ) に次を `staticTabs` 追加 `staticTabs":[]` し、次の JSON オブジェクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-180">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

    ```json
    {
        "entityId": "personalTab",
        "name": "Personal Tab ",
        "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
        "websiteUrl": "https://{{HOSTNAME}}",
        "scopes": ["personal"]
    }
    ```

1. <span data-ttu-id="ef5da-181">**contentURL パス コンポーネント** **yourDefaultTabNameTab を** 実際のタブ名で更新します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-181">Update the **contentURL** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

1. <span data-ttu-id="ef5da-182">ファイルに更新されたmanifest.js **を保存** します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-182">Save the updated **manifest.json** file.</span></span>

1. <span data-ttu-id="ef5da-183">IFrame でコンテンツ ページを提供するには、コード エディターで次のパスから **Tab.ts** を開きます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-183">To provide your content page in an IFrame, open **Tab.ts** in your code editor from the following path:</span></span>

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

1. <span data-ttu-id="ef5da-184">IFrame デコレータの一覧に次の項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-184">Add the following to the list of IFrame decorators:</span></span>

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

1. <span data-ttu-id="ef5da-185">更新された **Tab.ts ファイルを保存** します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-185">Save the updated **Tab.ts** file.</span></span> <span data-ttu-id="ef5da-186">タブ コードが完成しました。</span><span class="sxs-lookup"><span data-stu-id="ef5da-186">Your tab code is complete.</span></span>

### <a name="build-and-run-your-application"></a><span data-ttu-id="ef5da-187">アプリケーションのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="ef5da-187">Build and run your application</span></span>

<span data-ttu-id="ef5da-188">コマンド プロンプトで、プロジェクト ディレクトリを開いて次のタスクを完了します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-188">At a command prompt, open your project directory to complete the next tasks.</span></span>

#### <a name="create-the-app-package"></a><span data-ttu-id="ef5da-189">アプリ パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="ef5da-189">Create the app package</span></span>

<span data-ttu-id="ef5da-190">タブをテストするには、アプリ パッケージが必要Teams。</span><span class="sxs-lookup"><span data-stu-id="ef5da-190">You must have an app package to test your tab in Teams.</span></span> <span data-ttu-id="ef5da-191">これは、次の必須ファイルを含む zip フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="ef5da-191">It is a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="ef5da-192">192 x 192 ピクセルのフル カラー アイコン。 </span><span class="sxs-lookup"><span data-stu-id="ef5da-192">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="ef5da-193">**32** x 32 ピクセルの透明なアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="ef5da-193">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="ef5da-194">アプリ **manifest.js** を指定するファイルのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="ef5da-194">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="ef5da-195">パッケージは、ファイル上のファイルのmanifest.jsを検証し、./package ディレクトリに zip フォルダーを生成する **gulp タスクを使用して作成されます**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-195">The package is created through a gulp task that validates the manifest.json file and generates the zip folder in the **./package directory**.</span></span> <span data-ttu-id="ef5da-196">コマンド プロンプトで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-196">In the command prompt, enter the following command:</span></span>

```bash
gulp manifest
```

#### <a name="build-your-application"></a><span data-ttu-id="ef5da-197">アプリケーションのビルド</span><span class="sxs-lookup"><span data-stu-id="ef5da-197">Build your application</span></span>

<span data-ttu-id="ef5da-198">ビルド コマンドは、ソリューションを **./dist フォルダーに変換** します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-198">The build command transpiles your solution into the **./dist** folder.</span></span> <span data-ttu-id="ef5da-199">コマンド プロンプトで次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-199">Enter the following command in the command prompt:</span></span>

```bash
gulp build
```

#### <a name="run-your-application-in-localhost"></a><span data-ttu-id="ef5da-200">localhost でアプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="ef5da-200">Run your application in localhost</span></span>

1. <span data-ttu-id="ef5da-201">コマンド プロンプトに次の情報を入力して、ローカル Web サーバーを起動します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-201">Start a local web server by entering the following in the command prompt:</span></span>

    ```bash
    gulp serve
    ```

1. <span data-ttu-id="ef5da-202">次の図に示すように、ブラウザーに入力し、タブ名に置き換え、アプリケーションのホーム ページ `http://localhost:3007/<yourDefaultAppNameTab>/` **<yourDefaultAppNameTab>** を表示します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-202">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser, replace **<yourDefaultAppNameTab>** with your tab name, and view your application's home page as shown in the following image:</span></span>

    ![ホーム ページのスクリーンショット](~/assets/images/tab-images/homePage.png)

1. <span data-ttu-id="ef5da-204">個人用タブを表示するには、 に移動します `http://localhost:3007/<yourDefaultAppNameTab>/personal.html` 。</span><span class="sxs-lookup"><span data-stu-id="ef5da-204">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`.</span></span>

    >![個人用タブのスクリーンショット](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

### <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="ef5da-206">タブへのセキュリティで保護されたトンネルを確立する</span><span class="sxs-lookup"><span data-stu-id="ef5da-206">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="ef5da-207">Microsoft Teamsはクラウドベースの製品であり、HTTPS エンドポイントを使用してタブ コンテンツをクラウドから利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-207">Microsoft Teams is a cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="ef5da-208">Teamsはローカル ホスティングを許可しない。</span><span class="sxs-lookup"><span data-stu-id="ef5da-208">Teams does not allow local hosting.</span></span> <span data-ttu-id="ef5da-209">タブをパブリック URL に発行するか、ローカル ポートをインターネットに接続する URL に公開するプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-209">You must either publish your tab to a public URL or use a proxy that exposes your local port to an internet-facing URL.</span></span>

<span data-ttu-id="ef5da-210">タブ拡張機能をテストするには、このアプリケーションに組み込まれる [ngrok](https://ngrok.com/docs)を使用できます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-210">To test your tab extension, you can use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="ef5da-211">Ngrok はリバース プロキシ ソフトウェア ツールで、ローカルで実行中の Web サーバーの一般公開 HTTPS エンドポイントへのトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-211">Ngrok is a reverse proxy software tool that creates a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="ef5da-212">サーバーの Web エンドポイントは、コンピューター上の現在のセッション中に使用できます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-212">Your server's web endpoints are available during the current session on your computer.</span></span> <span data-ttu-id="ef5da-213">コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="ef5da-213">When the computer is shut down or goes to sleep, the service is no longer available.</span></span>

<span data-ttu-id="ef5da-214">コマンド プロンプトで localhost を終了し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-214">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="ef5da-215">タブが **ngrok** を介して Microsoft Teamsにアップロードされ、正常に保存された後、トンネル セッションが終了するまで、Teamsでタブを表示できます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-215">After your tab has been uploaded to Microsoft Teams through **ngrok**, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

### <a name="upload-your-application-to-teams"></a><span data-ttu-id="ef5da-216">アップロードを使用してアプリケーションをTeams</span><span class="sxs-lookup"><span data-stu-id="ef5da-216">Upload your application to Teams</span></span>

<span data-ttu-id="ef5da-217">**アプリケーションをアプリにアップロードTeams**</span><span class="sxs-lookup"><span data-stu-id="ef5da-217">**To upload your application to Teams**</span></span>

1. <span data-ttu-id="ef5da-218">[次へ] にMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="ef5da-218">Go to Microsoft Teams.</span></span> <span data-ttu-id="ef5da-219">Web ベースのバージョン [を使用する場合は](https://teams.microsoft.com) 、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-219">If you use the [web-based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
1. <span data-ttu-id="ef5da-220">左下隅から、[アプリ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-220">From the lower left corner, select **Apps**.</span></span>
1. <span data-ttu-id="ef5da-221">左下隅から、カスタム アプリ **アップロードを選択します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-221">From the lower left corner, choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="ef5da-222">プロジェクト ディレクトリに移動し **、./package** フォルダーを参照し、zip フォルダーを選択し、[開く] を選択 **します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-222">Go to your project directory, browse to the **./package** folder, select the zip folder, and choose **Open**.</span></span>

    ![個人用タブの追加](../../assets/images/tab-images/addingpersonaltab.png)

1. <span data-ttu-id="ef5da-224">ポップアップ **ダイアログ ボックスで** [追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-224">Select **Add** in the pop-up dialog box.</span></span> <span data-ttu-id="ef5da-225">タブがアップロードされ、Teams。</span><span class="sxs-lookup"><span data-stu-id="ef5da-225">Your tab is uploaded to Teams.</span></span>

    ![アップロードされた個人用タブ](../../assets/images/tab-images/personaltabuploaded.png)

### <a name="view-your-personal-tab"></a><span data-ttu-id="ef5da-227">個人用タブを表示する</span><span class="sxs-lookup"><span data-stu-id="ef5da-227">View your personal tab</span></span>

<span data-ttu-id="ef5da-228">[次のページ] の一Teams左側にあるナビゲーション バーで、省略記号 &#x25CF;&#x25CF;&#x25CF; 選択し、一覧からアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-228">In the navigation bar located at the far left in Teams, select the ellipses &#x25CF;&#x25CF;&#x25CF; and choose your app from the list.</span></span>

# <a name="aspnet-core"></a>[<span data-ttu-id="ef5da-229">ASP.NET コア</span><span class="sxs-lookup"><span data-stu-id="ef5da-229">ASP.NET Core</span></span>](#tab/aspnetcore)

### <a name="create-a-custom-personal-tab-using-aspnet-core"></a><span data-ttu-id="ef5da-230">ユーザー設定を使用してカスタム個人用タブを ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ef5da-230">Create a custom personal tab using ASP.NET Core</span></span>

<span data-ttu-id="ef5da-231">カスタム個人用タブは、Razor ページを使用してC#作成 ASP.NET Core作成できます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-231">You can create a custom personal tab using C# and ASP.NET Core Razor pages.</span></span> <span data-ttu-id="ef5da-232">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)は、アプリ マニフェストを最終的に作成し、タブを展開してアプリ マニフェストに展開Teams。</span><span class="sxs-lookup"><span data-stu-id="ef5da-232">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) is also used to finalize your app manifest and deploy your tab to Teams.</span></span>

### <a name="prerequisites-for-personal-tab"></a><span data-ttu-id="ef5da-233">[個人用] タブの前提条件</span><span class="sxs-lookup"><span data-stu-id="ef5da-233">Prerequisites for personal tab</span></span>

<span data-ttu-id="ef5da-234">次の前提条件について理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-234">You must have an understanding of the following prerequisites:</span></span>

- <span data-ttu-id="ef5da-235">カスタム アプリのアップロードを許可Office 365を有効にしたテナントとチーム **が構成されている必要** があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-235">You must have an Office 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="ef5da-236">詳細については、「prepare [your Office 365 テナント」を参照してください](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-236">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ef5da-237">ユーザーアカウントをお持ちMicrosoft 365場合は、Microsoft Developer Program を通じて無料サブスクリプションに[サインアップできます](https://developer.microsoft.com/en-us/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-237">If you do not have a Microsoft 365 account, you can sign up for a free subscription through the [Microsoft Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program).</span></span> <span data-ttu-id="ef5da-238">サブスクリプションは、継続的な開発に使用している限りアクティブなままです。</span><span class="sxs-lookup"><span data-stu-id="ef5da-238">The subscription remains active as long as you are using it for ongoing development.</span></span>

- <span data-ttu-id="ef5da-239">App Studio を使用してアプリケーションをインポートし、Teams。</span><span class="sxs-lookup"><span data-stu-id="ef5da-239">Use App Studio to import your application to Teams.</span></span> <span data-ttu-id="ef5da-240">App Studio をインストールするには、アプリアプリの左下隅にある [アプリ ストア アプリ] を選択Teams App Studio を ![ ](~/assets/images/tab-images/storeApp.png) **検索します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-240">To install App Studio, select **Apps** ![Store App](~/assets/images/tab-images/storeApp.png) at the lower left corner of the Teams app, and search for **App Studio**.</span></span> <span data-ttu-id="ef5da-241">タイルを見つけたら、タイルを選択し、ポップアップ ダイアログ ボックスで [追加] を選択してインストールします。</span><span class="sxs-lookup"><span data-stu-id="ef5da-241">After you find the tile, select it and choose **Add** in the pop-up dialog box to install it.</span></span>

<span data-ttu-id="ef5da-242">さらに、このプロジェクトでは、次のコードが開発環境にインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-242">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="ef5da-243">現在のバージョンの IDE **Visual Studio.NET CORE** クロスプラットフォーム開発ワークロードがインストールされています。</span><span class="sxs-lookup"><span data-stu-id="ef5da-243">The current version of the Visual Studio IDE with the **.NET CORE cross-platform development** workload installed.</span></span> <span data-ttu-id="ef5da-244">まだインストールされていない場合はVisual Studio最新バージョンを無料でダウンロード[Microsoft Visual Studio Communityインストールできます](https://visualstudio.microsoft.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-244">If you do not already have Visual Studio, you can download and install the latest [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) version for free.</span></span>

- <span data-ttu-id="ef5da-245">[ngrok](https://ngrok.com)リバース プロキシ ツール。</span><span class="sxs-lookup"><span data-stu-id="ef5da-245">The [ngrok](https://ngrok.com) reverse proxy tool.</span></span> <span data-ttu-id="ef5da-246">ngrok を使用して、ローカルで実行中の Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-246">Use ngrok to create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="ef5da-247">[ngrok をダウンロードできます](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-247">You can [download ngrok](https://ngrok.com/download).</span></span>

### <a name="get-the-source-code"></a><span data-ttu-id="ef5da-248">ソース コードを取得する</span><span class="sxs-lookup"><span data-stu-id="ef5da-248">Get the source code</span></span>

<span data-ttu-id="ef5da-249">コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-249">At a command prompt, create a new directory for your tab project.</span></span> <span data-ttu-id="ef5da-250">簡単なプロジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="ef5da-250">A simple project is provided to get you started.</span></span> <span data-ttu-id="ef5da-251">次のコマンドを使用して、サンプル リポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-251">Clone the sample repository into your new directory using the following command:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="ef5da-252">または、zip フォルダーをダウンロードしてファイルを抽出して、ソース コードを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-252">Alternately, you can retrieve the source code by downloading the zip folder and extracting the files.</span></span>

<span data-ttu-id="ef5da-253">**タブ プロジェクトをビルドして実行するには**</span><span class="sxs-lookup"><span data-stu-id="ef5da-253">**To build and run the tab project**</span></span>

1. <span data-ttu-id="ef5da-254">ソース コードを取得した後、[プロジェクト] に移動Visual Studio[プロジェクトまたはソリューションを開く **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-254">After you get the source code, go to Visual Studio and select **Open a project or solution**.</span></span>
1. <span data-ttu-id="ef5da-255">タブ アプリケーション ディレクトリに移動し **、PersonalTab.sln を開きます**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-255">Go to the tab application directory and open **PersonalTab.sln**.</span></span>
1. <span data-ttu-id="ef5da-256">アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-256">To build and run your application, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="ef5da-257">ブラウザーで、次の URL に移動して、アプリケーションが正しく読み込まれたか確認します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-257">In a browser, go to the following URLs to verify the application loaded properly:</span></span>

    - `http://localhost:44325/`
    - `http://localhost:44325/personal`
    - `http://localhost:44325/privacy`
    - `http://localhost:44325/tou`

### <a name="review-the-source-code"></a><span data-ttu-id="ef5da-258">ソース コードを確認する</span><span class="sxs-lookup"><span data-stu-id="ef5da-258">Review the source code</span></span>

#### <a name="startupcs"></a><span data-ttu-id="ef5da-259">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="ef5da-259">Startup.cs</span></span>

<span data-ttu-id="ef5da-260">このプロジェクトは、ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成され、セットアップ時に [詳細設定 **- HTTPS** 用に構成] チェック ボックスがオンになっています。</span><span class="sxs-lookup"><span data-stu-id="ef5da-260">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="ef5da-261">MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-261">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="ef5da-262">さらに、空のテンプレートでは既定では静的コンテンツの提供が有効ではないので、静的ファイル ミドルウェアは次のコードを使用してメソッド `Configure()` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-262">Additionally, the empty template does not enable serving static content by default, so the static files middleware is added to the `Configure()` method using the following code:</span></span>

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

#### <a name="wwwroot-folder"></a><span data-ttu-id="ef5da-263">wwwroot フォルダー</span><span class="sxs-lookup"><span data-stu-id="ef5da-263">wwwroot folder</span></span>

<span data-ttu-id="ef5da-264">この ASP.NET Core Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="ef5da-264">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

#### <a name="indexcshtml"></a><span data-ttu-id="ef5da-265">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="ef5da-265">Index.cshtml</span></span>

<span data-ttu-id="ef5da-266">ASP.NET Core Index と呼ばれるファイルをサイトの既定またはホーム ページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="ef5da-266">ASP.NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="ef5da-267">ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-267">When your browser URL points to the root of the site, **Index.cshtml** is displayed as the home page for your application.</span></span>

#### <a name="appmanifest-folder"></a><span data-ttu-id="ef5da-268">AppManifest フォルダー</span><span class="sxs-lookup"><span data-stu-id="ef5da-268">AppManifest folder</span></span>

<span data-ttu-id="ef5da-269">このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ef5da-269">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="ef5da-270">192 x 192 ピクセルのフル カラー アイコン。 </span><span class="sxs-lookup"><span data-stu-id="ef5da-270">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="ef5da-271">**32** x 32 ピクセルの透明なアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="ef5da-271">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="ef5da-272">アプリ **manifest.js** を指定するファイルのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="ef5da-272">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="ef5da-273">これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。</span><span class="sxs-lookup"><span data-stu-id="ef5da-273">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="ef5da-274">Microsoft Teams指定したマニフェストを読み込み、それを iframe <埋め込み、それをタブ `contentUrl` \> に表示します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-274">Microsoft Teams loads the `contentUrl` specified in your manifest, embeds it in an <iframe\>, and renders it in your tab.</span></span>

#### <a name="csproj"></a><span data-ttu-id="ef5da-275">.csproj</span><span class="sxs-lookup"><span data-stu-id="ef5da-275">.csproj</span></span>

<span data-ttu-id="ef5da-276">[ソリューション エクスプローラー Visual Studioで、プロジェクトを右クリックし、[ファイルの編集] Project **します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-276">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="ef5da-277">ファイルの最後に、アプリケーションのビルド時に zip フォルダーを作成および更新する次のコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-277">At the end of the file, you see the following code that creates and updates your zip folder when the application builds:</span></span>

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

### <a name="update-your-application-for-teams"></a><span data-ttu-id="ef5da-278">アプリケーションを更新Teams</span><span class="sxs-lookup"><span data-stu-id="ef5da-278">Update your application for Teams</span></span>

#### <a name="_layoutcshtml"></a><span data-ttu-id="ef5da-279">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="ef5da-279">_Layout.cshtml</span></span>

<span data-ttu-id="ef5da-280">タブを JavaScript クライアントにTeamsするには **、JavaScript** クライアント SDK をMicrosoft Teamsし、ページの読み込み後に呼び出 `microsoftTeams.initialize()` しを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-280">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="ef5da-281">次に、タブとアプリのTeams方法を示します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-281">This is how your tab and the Teams app communicate:</span></span>

<span data-ttu-id="ef5da-282">[共有] **フォルダーに移動** し **、_Layout.cshtml** を開き、[タグ] セクションに次の項目 `<head>` を追加します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-282">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

#### <a name="personaltabcshtml"></a><span data-ttu-id="ef5da-283">PersonalTab.cshtml</span><span class="sxs-lookup"><span data-stu-id="ef5da-283">PersonalTab.cshtml</span></span>

<span data-ttu-id="ef5da-284">**PersonalTab.cshtml を開** き、呼び出して埋め込 `<script>` みタグを更新します `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="ef5da-284">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="ef5da-285">更新された **PersonalTab.cshtml を保存してください**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-285">Ensure you save your updated **PersonalTab.cshtml**.</span></span>

### <a name="establish-a-secure-tunnel-to-your-tab-for-teams"></a><span data-ttu-id="ef5da-286">タブにセキュリティで保護されたトンネルを確立し、Teams</span><span class="sxs-lookup"><span data-stu-id="ef5da-286">Establish a secure tunnel to your tab for Teams</span></span>

<span data-ttu-id="ef5da-287">Microsoft Teamsはクラウドベースの製品であり、HTTPS エンドポイントを使用してタブ コンテンツをクラウドから利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-287">Microsoft Teams is a cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="ef5da-288">Teamsはローカル ホスティングを許可しない。</span><span class="sxs-lookup"><span data-stu-id="ef5da-288">Teams does not allow local hosting.</span></span> <span data-ttu-id="ef5da-289">タブをパブリック URL に発行するか、ローカル ポートをインターネットに接続する URL に公開するプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-289">You must either publish your tab to a public URL, or use a proxy that exposes your local port to an internet-facing URL.</span></span>

<span data-ttu-id="ef5da-290">タブをテストするには [、ngrok を使用します](https://ngrok.com/docs)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-290">To test your tab, use [ngrok](https://ngrok.com/docs).</span></span> <span data-ttu-id="ef5da-291">ngrok がコンピューターで実行されている間、サーバーの Web エンドポイントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-291">Your server's web endpoints are available while ngrok is running on your computer.</span></span> <span data-ttu-id="ef5da-292">ngrok の無料版では、ngrok を閉じると、次回起動する URL が異なります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-292">In the free version of ngrok, if you close ngrok, the URLs are different the next time you start it.</span></span>

<span data-ttu-id="ef5da-293">**タブへのセキュリティで保護されたトンネルを確立するには**</span><span class="sxs-lookup"><span data-stu-id="ef5da-293">**To establish a secure tunnel to your tab**</span></span>

1. <span data-ttu-id="ef5da-294">プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-294">At a command prompt in the root of your project directory, run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44325 -host-header="localhost:44325"
    ```

    <span data-ttu-id="ef5da-295">Ngrok は、インターネットからの要求をリッスンし、ポート 44325 で実行されているアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="ef5da-295">Ngrok listens to requests from the internet and routes them to your application when it is running on port 44325.</span></span> <span data-ttu-id="ef5da-296">`https://y8rPrT2b.ngrok.io/`**これは、y8rPrT2b** が ngrok の英数字 HTTPS URL に置き換えられる場所に似ています。</span><span class="sxs-lookup"><span data-stu-id="ef5da-296">It resembles `https://y8rPrT2b.ngrok.io/` where **y8rPrT2b** is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

    <span data-ttu-id="ef5da-297">ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。</span><span class="sxs-lookup"><span data-stu-id="ef5da-297">Ensure that you keep the command prompt with ngrok running, and make a note of the URL.</span></span>

2. <span data-ttu-id="ef5da-298">ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を使用してコンテンツ ページに移動して **、ngrok** が正常に実行および動作されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-298">Verify that **ngrok** is running and working properly by opening your browser and going to your content page through the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="ef5da-299">この記事で示す手順を完了するには、Visual Studioと ngrok の両方でアプリケーションを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-299">You need to have both your application in Visual Studio and ngrok running to complete the steps provided in this article.</span></span> <span data-ttu-id="ef5da-300">アプリケーションの実行を停止する必要がある場合Visual Studio **ngrok を実行し続ける必要があります**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-300">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="ef5da-301">アプリケーションの要求がアプリケーションで再起動されると、アプリケーションの要求をリッスンしてVisual Studio。</span><span class="sxs-lookup"><span data-stu-id="ef5da-301">It listens and resumes routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="ef5da-302">ngrok サービスを再起動する必要がある場合は、新しい URL が返され、その URL を使用する場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-302">If you have to restart the ngrok service, it returns a new URL and you have to update every place that uses that URL.</span></span>

#### <a name="run-your-application"></a><span data-ttu-id="ef5da-303">アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="ef5da-303">Run your application</span></span>

<span data-ttu-id="ef5da-304">このVisual Studio F5 キー **を押** するか、**アプリケーションの**[デバッグ] メニューから [デバッグの開始]**を選択** します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-304">In Visual Studio, press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

### <a name="upload-your-tab-with-app-studio-for-teams"></a><span data-ttu-id="ef5da-305">アップロード App Studio を使用してタブを開Teams</span><span class="sxs-lookup"><span data-stu-id="ef5da-305">Upload your tab with App Studio for Teams</span></span>

> [!NOTE]
> <span data-ttu-id="ef5da-306">**App Studio** を使用すると、ファイル上のmanifest.js **を編集** し、完成したパッケージをファイルにアップロードTeams。</span><span class="sxs-lookup"><span data-stu-id="ef5da-306">**App Studio** can be used to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="ef5da-307">また、手動で編集することもできます **manifest.jsをオンにしてください**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-307">You can also manually edit **manifest.json**.</span></span> <span data-ttu-id="ef5da-308">その場合は、ソリューションを再度ビルドして、アップロードする **Tab.zip作成してください** 。</span><span class="sxs-lookup"><span data-stu-id="ef5da-308">If you do, ensure that you build the solution again to create the **Tab.zip** file to upload.</span></span>

<span data-ttu-id="ef5da-309">**App Studio でタブをアップロードするには**</span><span class="sxs-lookup"><span data-stu-id="ef5da-309">**To upload your tab with App Studio**</span></span>

1. <span data-ttu-id="ef5da-310">[次へ] にMicrosoft Teams。</span><span class="sxs-lookup"><span data-stu-id="ef5da-310">Go to Microsoft Teams.</span></span> <span data-ttu-id="ef5da-311">Web ベースのバージョン [を使用する](https://teams.microsoft.com)場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-311">If you use the [web-based version](https://teams.microsoft.com), you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="ef5da-312">[App **Studio] に移動し** 、[マニフェスト エディター **] タブを選択** します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-312">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="ef5da-313">[ **マニフェスト エディターで既存のアプリ** をインポートする] **を選択して** 、タブのアプリ パッケージの更新を開始します。ソース コードには、部分的に完全なマニフェストが付属しています。</span><span class="sxs-lookup"><span data-stu-id="ef5da-313">Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="ef5da-314">アプリ パッケージの名前は次 **tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="ef5da-314">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="ef5da-315">これは、次のパスから使用できます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-315">It is available from the following path:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="ef5da-316">アップロードtab.zipApp  **Studio にアクセスします**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-316">Upload **tab.zip** to **App Studio**.</span></span>

#### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="ef5da-317">マニフェスト エディターを使用してアプリ パッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="ef5da-317">Update your app package with Manifest editor</span></span>

<span data-ttu-id="ef5da-318">アプリ パッケージを App Studio にアップロードしたら、アプリ パッケージを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-318">After you have uploaded your app package into App Studio, you must configure it.</span></span>

<span data-ttu-id="ef5da-319">マニフェスト エディターのウェルカム ページの右側のウィンドウで、新しくインポートしたタブのタイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-319">Select the tile for your newly imported tab in the right pane of the Manifest editor welcome page.</span></span>

<span data-ttu-id="ef5da-320">マニフェスト エディターの左側に手順の一覧が表示され、右側には、各手順の値が必要なプロパティの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-320">There is a list of steps on the left side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="ef5da-321">この情報の多くが、ユーザーのmanifest.js **によって** 提供されますが、更新する必要があるフィールドがあります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-321">Much of the information has been provided by your **manifest.json** but there are fields that you must update.</span></span>

##### <a name="details-app-details"></a><span data-ttu-id="ef5da-322">詳細: アプリの詳細</span><span class="sxs-lookup"><span data-stu-id="ef5da-322">Details: App details</span></span>

<span data-ttu-id="ef5da-323">[アプリ **の詳細] セクションで、次の内容を実行** します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-323">In the **App details** section:</span></span>

1. <span data-ttu-id="ef5da-324">**[Id] で**、[**生成] を** 選択して、アプリの新しいアプリ ID を生成します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-324">Under **Identification**, select **Generate** to generate a new App ID for your app.</span></span>

1. <span data-ttu-id="ef5da-325">[**開発者情報] で\*\*\*\*、ngrok** HTTPS URL を使用して Web **サイトを** 更新します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-325">Under **Developer information**, update **Website** with your **ngrok** HTTPS URL.</span></span>

    ![アプリの URL が更新されました](../../assets/images/tab-images/appurls.png)

1. <span data-ttu-id="ef5da-327">[**アプリの URL] で**、[プライバシーに関する **声明] と**[使用条件] を更新して、>。 `https://<yourngrokurl>/privacy`  `https://<yourngrokurl>/tou`</span><span class="sxs-lookup"><span data-stu-id="ef5da-327">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

##### <a name="capabilities-tabs"></a><span data-ttu-id="ef5da-328">機能: タブ</span><span class="sxs-lookup"><span data-stu-id="ef5da-328">Capabilities: Tabs</span></span>

<span data-ttu-id="ef5da-329">[タブ **] セクションで、次の設定を** 行います。</span><span class="sxs-lookup"><span data-stu-id="ef5da-329">In the **Tabs** section:</span></span>

1. <span data-ttu-id="ef5da-330">[個人用 **タブの追加] で、[** 追加] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-330">Under **Add a personal tab**, select **Add**.</span></span> <span data-ttu-id="ef5da-331">ポップアップ ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-331">A pop-up dialog box appears.</span></span>

1. <span data-ttu-id="ef5da-332">[名前] に個人用タブの名前を **入力します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-332">Enter a name for the personal tab in **Name**.</span></span>

1. <span data-ttu-id="ef5da-333">エンティティ **ID を入力します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-333">Enter the **Entity ID**.</span></span>

1. <span data-ttu-id="ef5da-334">で **コンテンツ URL を** 更新 `https://<yourngrokurl>/personalTab` します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-334">Update **Content URL** with `https://<yourngrokurl>/personalTab`.</span></span>

    <span data-ttu-id="ef5da-335">[Web サイト **の URL] フィールドは** 空白のままにします。</span><span class="sxs-lookup"><span data-stu-id="ef5da-335">Leave the **Website URL** field blank.</span></span>

    ![[個人用] タブの詳細](../../assets/images/tab-images/personaltabdetails.png)

1. <span data-ttu-id="ef5da-337">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-337">Select **Save**.</span></span>

##### <a name="finish-domains-and-permissions"></a><span data-ttu-id="ef5da-338">完了: ドメインとアクセス許可</span><span class="sxs-lookup"><span data-stu-id="ef5da-338">Finish: Domains and permissions</span></span>

<span data-ttu-id="ef5da-339">[ドメイン **とアクセス許可**] セクションで、タブのドメインには、HTTPS プレフィックスのない ngrok URL が含まれている必要があります `<yourngrokurl>.ngrok.io/` 。</span><span class="sxs-lookup"><span data-stu-id="ef5da-339">In the **Domains and permissions** section, **Domains from your tabs** must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

###### <a name="finish-test-and-distribute"></a><span data-ttu-id="ef5da-340">完了: テストと配布</span><span class="sxs-lookup"><span data-stu-id="ef5da-340">Finish: Test and distribute</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef5da-341">右側の [説明] **で**、次の警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-341">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="ef5da-342">&#9888; **'validDomains' 配列にトンネリング サイトを含めすることはできません。..**</span><span class="sxs-lookup"><span data-stu-id="ef5da-342">&#9888; **The 'validDomains' array cannot contain a tunneling site...**</span></span>
>
> <span data-ttu-id="ef5da-343">この警告は、タブのテスト中に無視できます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-343">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="ef5da-344">[テストと **配布] セクションで、[** インストール] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-344">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="ef5da-345">ポップアップ ダイアログ ボックスで、[追加] を選択 **すると** 、タブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-345">In the pop-up dialog box, select **Add** and your tab is displayed.</span></span>

    ![[個人用] タブの ASPNET がアップロードされました](../../assets/images/tab-images/personaltabaspnetuploaded.png)

### <a name="view-your-personal-tab-in-teams"></a><span data-ttu-id="ef5da-347">[個人用] タブを [Teams</span><span class="sxs-lookup"><span data-stu-id="ef5da-347">View your personal tab in Teams</span></span>

1. <span data-ttu-id="ef5da-348">アプリの左上にあるナビゲーション バーで、Teamsを選択 &#x25CF;&#x25CF;&#x25CF;。</span><span class="sxs-lookup"><span data-stu-id="ef5da-348">In the navigation bar located at the far left of the Teams app, select the ellipses &#x25CF;&#x25CF;&#x25CF;.</span></span> <span data-ttu-id="ef5da-349">個人用アプリの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-349">A list of personal apps is shown.</span></span>

1. <span data-ttu-id="ef5da-350">リストからタブを選択して表示します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-350">Select your tab from the list to view it.</span></span>

# <a name="aspnet-core-mvc"></a>[<span data-ttu-id="ef5da-351">ASP.NET CoreMVC</span><span class="sxs-lookup"><span data-stu-id="ef5da-351">ASP.NET Core MVC</span></span>](#tab/aspnetcoremvc)

### <a name="create-a-custom-personal-tab-with-aspnet-core-mvc"></a><span data-ttu-id="ef5da-352">MVC を使用してカスタム個人用タブを ASP.NET Coreする</span><span class="sxs-lookup"><span data-stu-id="ef5da-352">Create a custom personal tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="ef5da-353">MVC を使用してカスタム個人用タブをC#し ASP.NET Coreできます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-353">You can create a custom personal tab using C# and ASP.NET Core MVC.</span></span> <span data-ttu-id="ef5da-354">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)は、アプリ マニフェストを最終的に作成し、タブを展開してアプリ マニフェストに展開Teams。</span><span class="sxs-lookup"><span data-stu-id="ef5da-354">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) is also used to finalize your app manifest and deploy your tab to Teams.</span></span>

### <a name="prerequisites-for-personal-tab-with-aspnet-core-mvc"></a><span data-ttu-id="ef5da-355">MVC を使用した個人用タブ ASP.NET Core前提条件</span><span class="sxs-lookup"><span data-stu-id="ef5da-355">Prerequisites for personal tab with ASP.NET Core MVC</span></span>

- <span data-ttu-id="ef5da-356">カスタム アプリのアップロードを許可Microsoft 365を有効にしたチームとテナント **が必要** です。</span><span class="sxs-lookup"><span data-stu-id="ef5da-356">You must have a Microsoft 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="ef5da-357">詳細については、「prepare [your Office 365 テナント」を参照してください](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-357">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ef5da-358">ユーザーアカウントをお持ちMicrosoft 365場合は、Microsoft Developer Program を通じて無料サブスクリプションに[サインアップできます](https://developer.microsoft.com/en-us/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-358">If you do not have a Microsoft 365 account, you can sign up for a free subscription through the [Microsoft Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program).</span></span> <span data-ttu-id="ef5da-359">サブスクリプションは、継続的な開発に使用している限りアクティブなままです。</span><span class="sxs-lookup"><span data-stu-id="ef5da-359">The subscription remains active as long as you are using it for ongoing development.</span></span>

- <span data-ttu-id="ef5da-360">App Studio を使用してアプリケーションをインポートし、Teams。</span><span class="sxs-lookup"><span data-stu-id="ef5da-360">Use App Studio to import your application to Teams.</span></span> <span data-ttu-id="ef5da-361">App Studio をインストールするには、アプリアプリの左下隅にある [アプリ ストア アプリ] を選択Teams App Studio を ![ ](~/assets/images/tab-images/storeApp.png) **検索します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-361">To install App Studio, select **Apps** ![Store App](~/assets/images/tab-images/storeApp.png) at the lower left corner of the Teams app, and search for **App Studio**.</span></span> <span data-ttu-id="ef5da-362">タイルを見つけたら、タイルを選択し、ポップアップ ダイアログ ボックスで [追加] を選択してインストールします。</span><span class="sxs-lookup"><span data-stu-id="ef5da-362">After you find the tile, select it and choose **Add** in the pop-up dialog box to install it.</span></span>

<span data-ttu-id="ef5da-363">さらに、このプロジェクトでは、次のコードが開発環境にインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-363">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="ef5da-364">現在のバージョンの IDE **Visual Studio.NET CORE** クロスプラットフォーム開発ワークロードがインストールされています。</span><span class="sxs-lookup"><span data-stu-id="ef5da-364">The current version of the Visual Studio IDE with the **.NET CORE cross-platform development** workload installed.</span></span> <span data-ttu-id="ef5da-365">まだインストールされていない場合はVisual Studio最新バージョンを無料でダウンロード[Microsoft Visual Studio Communityインストールできます](https://visualstudio.microsoft.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-365">If you do not already have Visual Studio, you can download and install the latest [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) version for free.</span></span>

- <span data-ttu-id="ef5da-366">[ngrok](https://ngrok.com)リバース プロキシ ツール。</span><span class="sxs-lookup"><span data-stu-id="ef5da-366">The [ngrok](https://ngrok.com) reverse proxy tool.</span></span> <span data-ttu-id="ef5da-367">ngrok を使用して、ローカルで実行中の Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-367">Use ngrok to create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="ef5da-368">[ngrok をダウンロードできます](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="ef5da-368">You can [download ngrok](https://ngrok.com/download).</span></span>

### <a name="get-the-source-code"></a><span data-ttu-id="ef5da-369">ソース コードを取得する</span><span class="sxs-lookup"><span data-stu-id="ef5da-369">Get the source code</span></span>

<span data-ttu-id="ef5da-370">コマンド プロンプトで、タブ プロジェクトの新しいディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-370">At a command prompt, create a new directory for your tab project.</span></span> <span data-ttu-id="ef5da-371">簡単なプロジェクトが用意されています。</span><span class="sxs-lookup"><span data-stu-id="ef5da-371">A simple project is provided to get you started.</span></span> <span data-ttu-id="ef5da-372">次のコマンドを使用して、サンプル リポジトリを新しいディレクトリに複製します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-372">Clone the sample repository into your new directory using the following command:</span></span>

``` bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="ef5da-373">または、zip フォルダーをダウンロードしてファイルを抽出して、ソース コードを取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-373">Alternately, you can retrieve the source code by downloading the zip folder and extracting the files.</span></span>

<span data-ttu-id="ef5da-374">**タブ プロジェクトをビルドして実行するには**</span><span class="sxs-lookup"><span data-stu-id="ef5da-374">**To build and run the tab project**</span></span>

1. <span data-ttu-id="ef5da-375">ソース コードを取得した後、[プロジェクト] に移動Visual Studioプロジェクトまたはソリューションを開 **く] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-375">After you have the source code, go to Visual Studio and select **Open a project or solution**.</span></span>
1. <span data-ttu-id="ef5da-376">タブ アプリケーション ディレクトリに移動し **、PersonalTabMVC.sln を開きます**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-376">Go to the tab application directory and open **PersonalTabMVC.sln**.</span></span>
1. <span data-ttu-id="ef5da-377">アプリケーションをビルドして実行するには **、F5** キーを押するか、[デバッグ] メニューから [ **デバッグ** の開始] **を選択** します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-377">To build and run your application, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="ef5da-378">ブラウザーで、次の URL に移動して、アプリケーションが正しく読み込まれたか確認します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-378">In a browser, go to the following URLs to verify that the application loaded properly:</span></span>

    * `http://localhost:44335`
    * `http://localhost:44335/privacy`
    * `http://localhost:44335/tou`

### <a name="review-the-source-code"></a><span data-ttu-id="ef5da-379">ソース コードを確認する</span><span class="sxs-lookup"><span data-stu-id="ef5da-379">Review the source code</span></span>

#### <a name="startupcs"></a><span data-ttu-id="ef5da-380">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="ef5da-380">Startup.cs</span></span>

<span data-ttu-id="ef5da-381">このプロジェクトは、ASP.NET Core 2.2 Web アプリケーションの空のテンプレートから作成され、セットアップ時に [詳細設定 **- HTTPS** 用に構成] チェック ボックスがオンになっています。</span><span class="sxs-lookup"><span data-stu-id="ef5da-381">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="ef5da-382">MVC サービスは、依存関係の挿入フレームワークのメソッドによって登録 `ConfigureServices()` されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-382">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="ef5da-383">さらに、空のテンプレートでは既定では静的コンテンツの提供が有効ではないので、静的ファイル ミドルウェアは次のコードを使用してメソッド `Configure()` に追加されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-383">Additionally, the empty template does not enable serving static content by default, so the static files middleware is added to the `Configure()` method using the following code:</span></span>

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

#### <a name="wwwroot-folder"></a><span data-ttu-id="ef5da-384">wwwroot フォルダー</span><span class="sxs-lookup"><span data-stu-id="ef5da-384">wwwroot folder</span></span>

<span data-ttu-id="ef5da-385">この ASP.NET Core Web ルート フォルダーは、アプリケーションが静的ファイルを検索する場所です。</span><span class="sxs-lookup"><span data-stu-id="ef5da-385">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

#### <a name="appmanifest-folder"></a><span data-ttu-id="ef5da-386">AppManifest フォルダー</span><span class="sxs-lookup"><span data-stu-id="ef5da-386">AppManifest folder</span></span>

<span data-ttu-id="ef5da-387">このフォルダーには、次の必須アプリ パッケージ ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ef5da-387">This folder contains the following required app package files:</span></span>

* <span data-ttu-id="ef5da-388">192 x 192 ピクセルのフル カラー アイコン。 </span><span class="sxs-lookup"><span data-stu-id="ef5da-388">A **full color icon** measuring 192 x 192 pixels.</span></span>
* <span data-ttu-id="ef5da-389">**32** x 32 ピクセルの透明なアウトライン アイコン。</span><span class="sxs-lookup"><span data-stu-id="ef5da-389">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
* <span data-ttu-id="ef5da-390">アプリ **manifest.js** を指定するファイルのプロパティです。</span><span class="sxs-lookup"><span data-stu-id="ef5da-390">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="ef5da-391">これらのファイルは、タブをアプリ パッケージにアップロードする場合に使用するアプリ パッケージに圧縮するTeams。</span><span class="sxs-lookup"><span data-stu-id="ef5da-391">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="ef5da-392">Microsoft Teams指定したマニフェストを読み込み、IFrame に埋め込み、タブ `contentUrl` にレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="ef5da-392">Microsoft Teams loads the `contentUrl` specified in your manifest, embeds it in an IFrame, and renders it in your tab.</span></span>

#### <a name="csproj"></a><span data-ttu-id="ef5da-393">.csproj</span><span class="sxs-lookup"><span data-stu-id="ef5da-393">.csproj</span></span>

<span data-ttu-id="ef5da-394">[ソリューション エクスプローラー Visual Studioで、プロジェクトを右クリックし、[ファイルの編集] Project **します**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-394">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="ef5da-395">ファイルの最後に、アプリケーションのビルド時に zip フォルダーを作成および更新する次のコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-395">At the end of the file, you see the following code that creates and updates your zip folder when the application builds:</span></span>

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

#### <a name="models"></a><span data-ttu-id="ef5da-396">モデル</span><span class="sxs-lookup"><span data-stu-id="ef5da-396">Models</span></span>

<span data-ttu-id="ef5da-397">**PersonalTab.cs** は、ユーザーが PersonalTab ビューでボタンを選択すると **、PersonalTabController** から呼び出される Message オブジェクトとメソッド **を表示** します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-397">**PersonalTab.cs** presents a Message object and methods that are called from **PersonalTabController** when a user selects a button in the **PersonalTab** View.</span></span>

#### <a name="views"></a><span data-ttu-id="ef5da-398">ビュー</span><span class="sxs-lookup"><span data-stu-id="ef5da-398">Views</span></span>

<span data-ttu-id="ef5da-399">次に示すのは、MVC の ASP.NET Coreです。</span><span class="sxs-lookup"><span data-stu-id="ef5da-399">These are the different views in ASP.NET Core MVC:</span></span>

* <span data-ttu-id="ef5da-400">ホーム: ASP.NET Core Index と呼ばれるファイルをサイトの既定またはホーム ページとして扱います。</span><span class="sxs-lookup"><span data-stu-id="ef5da-400">Home: ASP.NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="ef5da-401">ブラウザーの URL がサイトのルートをポイントすると **、Index.cshtml** がアプリケーションのホーム ページとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-401">When your browser URL points to the root of the site, **Index.cshtml** is displayed as the home page for your application.</span></span>

* <span data-ttu-id="ef5da-402">共有: 部分ビュー マークアップ **_Layout.cshtml** には、アプリケーションの全体的なページ構造と共有ビジュアル要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-402">Shared: The partial view markup **_Layout.cshtml** contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="ef5da-403">また、ライブラリのTeamsします。</span><span class="sxs-lookup"><span data-stu-id="ef5da-403">It also references the Teams Library.</span></span>

#### <a name="controllers"></a><span data-ttu-id="ef5da-404">コントローラー</span><span class="sxs-lookup"><span data-stu-id="ef5da-404">Controllers</span></span>

<span data-ttu-id="ef5da-405">コントローラーはプロパティを使用 `ViewBag` して、値を Views に動的に転送します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-405">The controllers use the `ViewBag` property to transfer values dynamically to the Views.</span></span>

[!INCLUDE [dotnet-update-personal-app](~/includes/tabs/dotnet-update-personal-app.md)]

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

<span data-ttu-id="ef5da-406">**ngrok を実行してコンテンツ ページを確認するには**</span><span class="sxs-lookup"><span data-stu-id="ef5da-406">**To run ngrok and verify the content page**</span></span>

1. <span data-ttu-id="ef5da-407">プロジェクト ディレクトリのルートにあるコマンド プロンプトで、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-407">At a command prompt in the root of your project directory, run the following command:</span></span>

    ``` bash
    ngrok http https://localhost:44345 -host-header="localhost:44345"
    ```

    <span data-ttu-id="ef5da-408">Ngrok は、インターネットからの要求をリッスンし、ポート 44325 で実行されているアプリケーションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="ef5da-408">Ngrok listens to requests from the internet and routes them to your application when it is running on port 44325.</span></span> <span data-ttu-id="ef5da-409">`https://y8rPrT2b.ngrok.io/`**これは、y8rPrT2b** が ngrok の英数字 HTTPS URL に置き換えられる場所に似ています。</span><span class="sxs-lookup"><span data-stu-id="ef5da-409">It resembles `https://y8rPrT2b.ngrok.io/` where **y8rPrT2b** is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

    <span data-ttu-id="ef5da-410">ngrok を実行してコマンド プロンプトを保持し、URL をメモしてください。</span><span class="sxs-lookup"><span data-stu-id="ef5da-410">Ensure you keep the command prompt with ngrok running, and make a note of the URL.</span></span>

1. <span data-ttu-id="ef5da-411">ブラウザーを開き、コマンド プロンプト ウィンドウで提供された ngrok HTTPS URL を使用してコンテンツ ページに移動して **、ngrok** が正常に実行および動作されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-411">Verify that **ngrok** is running and working properly by opening your browser and going to your content page through the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="ef5da-412">この記事で示す手順を完了するには、Visual Studioと ngrok の両方でアプリケーションを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-412">You need to have both your application in Visual Studio and ngrok running to complete the steps provided in this article.</span></span> <span data-ttu-id="ef5da-413">アプリケーションの実行を停止する必要がある場合Visual Studio **ngrok を実行し続ける必要があります**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-413">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="ef5da-414">アプリケーションの要求がアプリケーションで再起動されると、アプリケーションの要求をリッスンしてVisual Studio。</span><span class="sxs-lookup"><span data-stu-id="ef5da-414">It listens and resumes routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="ef5da-415">ngrok サービスを再起動する必要がある場合は、新しい URL が返され、その URL を使用する場所を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ef5da-415">If you have to restart the ngrok service it returns a new URL and you have to update every place that uses that URL.</span></span>

#### <a name="run-your-application"></a><span data-ttu-id="ef5da-416">アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="ef5da-416">Run your application</span></span>

<span data-ttu-id="ef5da-417">このVisual Studio F5 キー **を押** するか、**アプリケーションの**[デバッグ] メニューから [デバッグの開始]**を選択** します。</span><span class="sxs-lookup"><span data-stu-id="ef5da-417">In Visual Studio, press **F5** or choose **Start Debugging** from your application's **Debug** menu.</span></span>

[!INCLUDE [dotnet-personal-use-appstudio](~/includes/tabs/dotnet-personal-use-appstudio.md)]

---

## <a name="reorder-static-personal-tabs"></a><span data-ttu-id="ef5da-418">静的な個人用タブの並べ替え</span><span class="sxs-lookup"><span data-stu-id="ef5da-418">Reorder static personal tabs</span></span>

<span data-ttu-id="ef5da-419">マニフェスト バージョン 1.7 から、開発者は個人用アプリ内のすべてのタブを再配置できます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-419">Starting with manifest version 1.7, developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="ef5da-420">特に、開発者はボット チャットタブを移動できます。これは常に既定で最初の位置に、個人用アプリのタブ ヘッダー内の任意の場所に移動できます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-420">In particular, a developer can move the **bot chat** tab, which always defaults to the first position, anywhere in the personal app tab header.</span></span> <span data-ttu-id="ef5da-421">2 つの予約済みタブ `entityId` キーワードが宣言され、**会話と\*\*\*\*についてです**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-421">Two reserved tab `entityId` keywords are declared, **conversations** and **about**.</span></span>

<span data-ttu-id="ef5da-422">個人用スコープを持つ **ボットを作成** すると、既定では個人用アプリの最初のタブ位置に表示されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-422">If you create a bot with a **personal** scope, it appears in the first tab position in a personal app by default.</span></span> <span data-ttu-id="ef5da-423">別の位置に移動する場合は、予約キーワードである会話を使用して静的タブ オブジェクトをマニフェストに追加する必要 **があります**。</span><span class="sxs-lookup"><span data-stu-id="ef5da-423">If you want to move it to another position, you must add a static tab object to your manifest with the reserved keyword, **conversations**.</span></span> <span data-ttu-id="ef5da-424">[ **会話** ] タブは、配列に会話タブを追加する場所に応 **じて、Web** またはデスクトップに表示 `staticTabs` されます。</span><span class="sxs-lookup"><span data-stu-id="ef5da-424">The **conversation** tab appears on web or desktop depending on where you add the **conversation** tab in the `staticTabs` array.</span></span>

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

## <a name="see-also"></a><span data-ttu-id="ef5da-425">関連項目</span><span class="sxs-lookup"><span data-stu-id="ef5da-425">See also</span></span>

* [<span data-ttu-id="ef5da-426">Teamsタブ</span><span class="sxs-lookup"><span data-stu-id="ef5da-426">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="ef5da-427">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="ef5da-427">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="ef5da-428">アダプティブ カードを使用してタブをビルドする</span><span class="sxs-lookup"><span data-stu-id="ef5da-428">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="ef5da-429">会話タブを作成する</span><span class="sxs-lookup"><span data-stu-id="ef5da-429">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)

## <a name="next-step"></a><span data-ttu-id="ef5da-430">次の手順</span><span class="sxs-lookup"><span data-stu-id="ef5da-430">Next step</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="ef5da-431">[[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)</span><span class="sxs-lookup"><span data-stu-id="ef5da-431">[Create a channel or group tab](~/tabs/how-to/create-channel-group-tab.md)</span></span>
