---
title: 'クイック スタート: Microsoft Teams 用のユーザー設定Node.js Yeoman Generator を使用してカスタム個人用タブを作成する'
author: laujan
description: Microsoft Teams 用 Yeoman Generator を使用して個人用タブを作成するクイック スタート ガイド。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 30143fa3c84a68ae6c34176b252badaa4cef9613
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019553"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="d31e5-103">クイック スタート: Microsoft Teams 用のユーザー設定Node.js Yeoman Generator を使用してカスタム個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="d31e5-103">Quickstart: Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="d31e5-104">このクイック スタートは、Microsoft OfficeDev GitHub リポジトリにある最初の Microsoft [Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki のビルドで説明されている手順に従います。</span><span class="sxs-lookup"><span data-stu-id="d31e5-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="d31e5-105">このクイック スタートでは、Teams Yeoman ジェネレーターを使用してカスタム個人用タブを作成 [する方法について説明します](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。</span><span class="sxs-lookup"><span data-stu-id="d31e5-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="d31e5-106">また、アプリケーションをチームにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="d31e5-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="d31e5-107">**構成可能なタブまたは静的タブを作成しますか?**</span><span class="sxs-lookup"><span data-stu-id="d31e5-107">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="d31e5-108">矢印キーを使用して静的タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="d31e5-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d31e5-109">このクイック スタートで参照されるパス コンポーネント *yourDefaultTabNameTab* は、[既定のタブ名] のジェネレーターに入力した値に Tab という単語を加 *えた値です*。</span><span class="sxs-lookup"><span data-stu-id="d31e5-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="d31e5-110">例: DefaultTabName: *MyTab*  =>  */MyTabTab/*</span><span class="sxs-lookup"><span data-stu-id="d31e5-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="d31e5-111">個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="d31e5-111">Create your personal tab</span></span>

<span data-ttu-id="d31e5-112">このアプリケーションに個人用タブを追加するには、コンテンツ ページを作成し、既存のファイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="d31e5-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="d31e5-113">コード エディターで、新しい HTML ファイルを作成し、lpersonal.htm **次** のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="d31e5-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

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

- <span data-ttu-id="d31e5-114">アプリケーション **personal.htmの Web** フォルダーに l を **保存** します。</span><span class="sxs-lookup"><span data-stu-id="d31e5-114">Save **personal.html** in your application's **web** folder:</span></span>

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- <span data-ttu-id="d31e5-115">コード **manifest.jsで[** オン] を開きます。</span><span class="sxs-lookup"><span data-stu-id="d31e5-115">Open **manifest.json** in your code editor:</span></span>

```bash
./src/manifest/manifest.json/
```

<span data-ttu-id="d31e5-116">空の配列 ( ) に次を `staticTabs` 追加 `staticTabs":[]` し、次の JSON オブジェクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="d31e5-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="d31e5-117">**"contentURL" パス コンポーネント** **yourDefaultTabNameTab** を実際のタブ名で更新してください。</span><span class="sxs-lookup"><span data-stu-id="d31e5-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="d31e5-118">更新されたファイルを **manifest.jsします**。</span><span class="sxs-lookup"><span data-stu-id="d31e5-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="d31e5-119">コンテンツ ページは IFrame で提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d31e5-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="d31e5-120">コード **エディターで Tab.ts** を開きます。</span><span class="sxs-lookup"><span data-stu-id="d31e5-120">Open **Tab.ts** in your code editor:</span></span>

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- <span data-ttu-id="d31e5-121">IFrame デコレータの一覧に次の項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="d31e5-121">Add the following to the list of IFrame decorators:</span></span>

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- <span data-ttu-id="d31e5-122">更新された **Tab.ts ファイルを保存してください** 。</span><span class="sxs-lookup"><span data-stu-id="d31e5-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="d31e5-123">タブ コードが完成しました。</span><span class="sxs-lookup"><span data-stu-id="d31e5-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="d31e5-124">アプリケーションのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="d31e5-124">Build and Run Your Application</span></span>

<span data-ttu-id="d31e5-125">プロジェクト ディレクトリでコマンド プロンプトを開き、次のタスクを完了します。</span><span class="sxs-lookup"><span data-stu-id="d31e5-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="d31e5-126">個人用タブを表示するには、 `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="d31e5-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![個人用タブのスクリーンショット](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="d31e5-128">タブへのセキュリティで保護されたトンネルを確立する</span><span class="sxs-lookup"><span data-stu-id="d31e5-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="d31e5-129">Microsoft Teams は完全にクラウドベースの製品であり、HTTPS エンドポイントを使用してタブ コンテンツをクラウドから利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="d31e5-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="d31e5-130">Teams ではローカル ホスティングが許可されていないので、タブをパブリック URL に発行するか、ローカル ポートをインターネットに接続する URL に公開するプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d31e5-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="d31e5-131">タブ拡張機能をテストするには、このアプリケーションに組み込まれる [ngrok](https://ngrok.com/docs)を使用します。</span><span class="sxs-lookup"><span data-stu-id="d31e5-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="d31e5-132">Ngrok はリバース プロキシ ソフトウェア ツールで、ローカルで実行中の Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="d31e5-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="d31e5-133">サーバーの Web エンドポイントは、ローカル コンピューター上の現在のセッション中に利用できます。</span><span class="sxs-lookup"><span data-stu-id="d31e5-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="d31e5-134">コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="d31e5-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="d31e5-135">コマンド プロンプトで localhost を終了し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="d31e5-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="d31e5-136">タブが *ngrok* 経由で Microsoft チームにアップロードされ、正常に保存されると、トンネル セッションが終了するまで Teams で表示できます。</span><span class="sxs-lookup"><span data-stu-id="d31e5-136">After your tab has been uploaded to Microsoft teams, via *ngrok*, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="d31e5-137">アプリケーションを Teams にアップロードする</span><span class="sxs-lookup"><span data-stu-id="d31e5-137">Upload your application to Teams</span></span>

- <span data-ttu-id="d31e5-138">Microsoft Teams クライアントを開きます。</span><span class="sxs-lookup"><span data-stu-id="d31e5-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="d31e5-139">Web ベースのバージョン [を使用する](https://teams.microsoft.com) 場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="d31e5-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="d31e5-140">左側の *[YourTeams]* パネルで、タブのテストに使用するチームの横にあるメニューを選択し、[チームの管理 `...` ] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="d31e5-140">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="d31e5-141">メイン パネルでタブ バーから **[アプリ**]を選択し、ページの右下隅にある [カスタム アプリのアップロード] を選択します。</span><span class="sxs-lookup"><span data-stu-id="d31e5-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="d31e5-142">プロジェクト ディレクトリを開き **、./package** フォルダーを参照し、zip フォルダーを選択して右クリックし、[開く] を選択 **します**。</span><span class="sxs-lookup"><span data-stu-id="d31e5-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="d31e5-143">タブが Teams にアップロードされます。</span><span class="sxs-lookup"><span data-stu-id="d31e5-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="d31e5-144">個人用タブを表示する</span><span class="sxs-lookup"><span data-stu-id="d31e5-144">View your personal tabs</span></span>

<span data-ttu-id="d31e5-145">Teams クライアントの左上にあるナビゲーション バーで、メニューを選択し、一覧から `...` アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="d31e5-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>
