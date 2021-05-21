---
title: 'クイック スタート: カスタム 個人用タブを作成し、Node.js Yeoman Generator を使用Microsoft Teams'
author: laujan
description: Yeoman Generator を使用して個人用タブを作成するクイック スタート Microsoft Teams。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 88ad05aacaed69d695bc918e3e8a44ec18e560ae
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566609"
---
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="988ae-103">カスタム 個人用タブを作成するには、Node.js と Yeoman Generator を使用Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="988ae-103">Create a custom personal tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="988ae-104">このクイック スタートは、Microsoft OfficeDev Microsoft Teams リポジトリにあるビルド Your First [Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) App Wiki で説明されている手順にGitHubします。</span><span class="sxs-lookup"><span data-stu-id="988ae-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="988ae-105">このクイック スタートでは[、Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)ジェネレーターを使用してカスタム個人用タブを作成Teams説明します。</span><span class="sxs-lookup"><span data-stu-id="988ae-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="988ae-106">また、アプリケーションをチームにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="988ae-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="988ae-107">**構成可能なタブまたは静的タブを作成する**</span><span class="sxs-lookup"><span data-stu-id="988ae-107">**Create a configurable or static tab**</span></span>

<span data-ttu-id="988ae-108">矢印キーを使用して静的タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="988ae-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="988ae-109">このクイック スタートで参照されるパス コンポーネント *yourDefaultTabNameTab* は、[既定のタブ名] のジェネレーターに入力した値に Tab という単語を加 *えた値です*。</span><span class="sxs-lookup"><span data-stu-id="988ae-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="988ae-110">例: DefaultTabName: *MyTab*  =>  */MyTabTab/*</span><span class="sxs-lookup"><span data-stu-id="988ae-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="988ae-111">個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="988ae-111">Create your personal tab</span></span>

<span data-ttu-id="988ae-112">このアプリケーションに個人用タブを追加するには、コンテンツ ページを作成し、既存のファイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="988ae-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="988ae-113">コード エディターで、新しい HTML ファイルを作成し、lpersonal.htm **次** のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="988ae-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

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

- <span data-ttu-id="988ae-114">アプリケーション **personal.htmの Web** フォルダーに l を **保存** します。</span><span class="sxs-lookup"><span data-stu-id="988ae-114">Save **personal.html** in your application's **web** folder:</span></span>

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- <span data-ttu-id="988ae-115">コード **manifest.jsで[** オン] を開きます。</span><span class="sxs-lookup"><span data-stu-id="988ae-115">Open **manifest.json** in your code editor:</span></span>

    ```bash
    ./src/manifest/manifest.json/
    ```

<span data-ttu-id="988ae-116">空の配列 ( ) に次を `staticTabs` 追加 `staticTabs":[]` し、次の JSON オブジェクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="988ae-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="988ae-117">**"contentURL" パス コンポーネント** **yourDefaultTabNameTab** を実際のタブ名で更新してください。</span><span class="sxs-lookup"><span data-stu-id="988ae-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="988ae-118">更新されたファイルを **manifest.jsします**。</span><span class="sxs-lookup"><span data-stu-id="988ae-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="988ae-119">コンテンツ ページは IFrame で提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="988ae-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="988ae-120">コード **エディターで Tab.ts** を開きます。</span><span class="sxs-lookup"><span data-stu-id="988ae-120">Open **Tab.ts** in your code editor:</span></span>

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- <span data-ttu-id="988ae-121">IFrame デコレータの一覧に次の項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="988ae-121">Add the following to the list of IFrame decorators:</span></span>

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- <span data-ttu-id="988ae-122">更新された **Tab.ts ファイルを保存してください** 。</span><span class="sxs-lookup"><span data-stu-id="988ae-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="988ae-123">タブ コードが完成しました。</span><span class="sxs-lookup"><span data-stu-id="988ae-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="988ae-124">アプリケーションのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="988ae-124">Build and Run Your Application</span></span>

<span data-ttu-id="988ae-125">プロジェクト ディレクトリでコマンド プロンプトを開き、次のタスクを完了します。</span><span class="sxs-lookup"><span data-stu-id="988ae-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="988ae-126">個人用タブを表示するには、 `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="988ae-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![個人用タブのスクリーンショット](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="988ae-128">タブへのセキュリティで保護されたトンネルを確立する</span><span class="sxs-lookup"><span data-stu-id="988ae-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="988ae-129">Microsoft Teams完全にクラウドベースの製品であり、HTTPS エンドポイントを使用してタブ コンテンツをクラウドから利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="988ae-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="988ae-130">Teamsローカル ホスティングは許可されていないので、タブをパブリック URL に発行するか、ローカル ポートをインターネットに接続する URL に公開するプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="988ae-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="988ae-131">タブ拡張機能をテストするには、このアプリケーションに組み込まれる [ngrok](https://ngrok.com/docs)を使用します。</span><span class="sxs-lookup"><span data-stu-id="988ae-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="988ae-132">Ngrok はリバース プロキシ ソフトウェア ツールで、ローカルで実行中の Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="988ae-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="988ae-133">サーバーの Web エンドポイントは、ローカル コンピューター上の現在のセッション中に利用できます。</span><span class="sxs-lookup"><span data-stu-id="988ae-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="988ae-134">コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="988ae-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="988ae-135">コマンド プロンプトで localhost を終了し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="988ae-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="988ae-136">タブが **ngrok** 経由で Microsoft チームにアップロードされ、正常に保存された後、トンネル セッションが終了するまで、Teamsで表示できます。</span><span class="sxs-lookup"><span data-stu-id="988ae-136">After your tab has been uploaded to Microsoft teams, via **ngrok**, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="988ae-137">アップロードを使用してアプリケーションをTeams</span><span class="sxs-lookup"><span data-stu-id="988ae-137">Upload your application to Teams</span></span>

- <span data-ttu-id="988ae-138">クライアントを開Microsoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="988ae-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="988ae-139">Web ベースのバージョン [を使用する](https://teams.microsoft.com) 場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="988ae-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="988ae-140">左側の **[YourTeams]** パネルで、タブのテストに使用するチームの横にあるメニューを選択し、[チームの管理 `...` ] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="988ae-140">In the **YourTeams** panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="988ae-141">メイン パネルでタブ バーから **[** アプリ]を選択しアップロードの右下隅にあるカスタム アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="988ae-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="988ae-142">プロジェクト ディレクトリを開き **、./package** フォルダーを参照し、zip フォルダーを選択して右クリックし、[開く] を選択 **します**。</span><span class="sxs-lookup"><span data-stu-id="988ae-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="988ae-143">タブがアプリにアップロードTeams。</span><span class="sxs-lookup"><span data-stu-id="988ae-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="988ae-144">個人用タブを表示する</span><span class="sxs-lookup"><span data-stu-id="988ae-144">View your personal tabs</span></span>

<span data-ttu-id="988ae-145">クライアントの左上にあるナビゲーション バーでTeamsメニューを選択し、一覧から `...` アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="988ae-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>

## <a name="next-step"></a><span data-ttu-id="988ae-146">次の手順</span><span class="sxs-lookup"><span data-stu-id="988ae-146">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="988ae-147">ASP.NETCore を使用して個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="988ae-147">Create a personal tab using ASP.NETCore</span></span>](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
