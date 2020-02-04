---
title: 'クイックスタート: node.js を使用してカスタムの個人用タブを作成し、Microsoft Teams 用の Outlook を使用します。'
author: laujan
description: Microsoft Teams 用のごみ箱のジェネレーターを使用して、個人用タブを作成するためのクイックスタートガイド。
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 2d1b17360b92a161179091c1f6ba06ffa194e958
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674618"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="22ef0-103">クイックスタート: node.js を使用してカスタムの個人用タブを作成し、Microsoft Teams 用の Outlook を使用します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-103">Quickstart: Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="22ef0-104">このクイックスタートは、「Microsoft OfficeDev GitHub リポジトリにある[最初の Microsoft Teams アプリ](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)Wiki を構築する」に記載されている手順に従います。</span><span class="sxs-lookup"><span data-stu-id="22ef0-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="22ef0-105">このクイックスタートでは、Teams の [[オマーン] ジェネレーター](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)を使用して、カスタムの個人用タブを作成する手順を順を追って説明します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="22ef0-106">また、アプリケーションをチームにアップロードします。</span><span class="sxs-lookup"><span data-stu-id="22ef0-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="22ef0-107">**構成可能なタブまたは静的タブを作成しますか?**</span><span class="sxs-lookup"><span data-stu-id="22ef0-107">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="22ef0-108">方向キーを使用して、[静的] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="22ef0-109">このクイックスタートで参照される path コンポーネントの*Defaulttabnametab*は、[*既定のタブ名*] と [word *] タブ*に入力した値です。</span><span class="sxs-lookup"><span data-stu-id="22ef0-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="22ef0-110">例: defaulttabname: *MyTab* => /*mytabtab/*</span><span class="sxs-lookup"><span data-stu-id="22ef0-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="22ef0-111">[個人用] タブを作成する</span><span class="sxs-lookup"><span data-stu-id="22ef0-111">Create your personal tab</span></span>

<span data-ttu-id="22ef0-112">このアプリケーションに個人用タブを追加するには、コンテンツページを作成し、既存のファイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="22ef0-113">コードエディター**で、新しい html ファイル (.html** ) を作成し、次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

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

- <span data-ttu-id="22ef0-114">アプリケーションの**web**フォルダーに**personal .html**を保存します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-114">Save **personal.html** in your application's **web** folder:</span></span>

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- <span data-ttu-id="22ef0-115">コードエディターで**マニフェスト**を開きます。</span><span class="sxs-lookup"><span data-stu-id="22ef0-115">Open **manifest.json** in your code editor:</span></span>

```bash
./src/manifest/manifest.json/
```

<span data-ttu-id="22ef0-116">次のものを空`staticTabs`の配列 (`staticTabs":[]`) に追加し、次の JSON オブジェクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="22ef0-117">「 **Defaulttabnametab** 」という実際のタブ名を使用して、 **「contenturl」** パスコンポーネントを必ず更新してください。</span><span class="sxs-lookup"><span data-stu-id="22ef0-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="22ef0-118">更新された**manifest**を保存します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="22ef0-119">コンテンツページは IFrame で提供される必要があります。</span><span class="sxs-lookup"><span data-stu-id="22ef0-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="22ef0-120">コードエディターで、次のように Tab を開きます **。**</span><span class="sxs-lookup"><span data-stu-id="22ef0-120">Open **Tab.ts** in your code editor:</span></span>

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- <span data-ttu-id="22ef0-121">次のものを IFrame decorators のリストに追加します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-121">Add the following to the list of IFrame decorators:</span></span>

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- <span data-ttu-id="22ef0-122">更新した**タブの ts**ファイルを保存してください。</span><span class="sxs-lookup"><span data-stu-id="22ef0-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="22ef0-123">タブコードが完成しました。</span><span class="sxs-lookup"><span data-stu-id="22ef0-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="22ef0-124">アプリケーションをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="22ef0-124">Build and Run Your Application</span></span>

<span data-ttu-id="22ef0-125">プロジェクトディレクトリでコマンドプロンプトを開いて、次のタスクを完了します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="22ef0-126">[個人用] タブを表示するには、`http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="22ef0-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![[個人用] タブのスクリーンショット](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="22ef0-128">タブへのセキュリティで保護されたトンネルの確立</span><span class="sxs-lookup"><span data-stu-id="22ef0-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="22ef0-129">Microsoft Teams は完全なクラウドベースの製品であり、HTTPS エンドポイントを使用してクラウドからタブのコンテンツを利用できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="22ef0-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="22ef0-130">Teams ではローカルホスティングが許可されていません。そのため、タブをパブリック URL に公開するか、またはプロキシを使用して、ローカルポートをインターネットに接続する URL に公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="22ef0-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="22ef0-131">タブ拡張機能をテストするには、このアプリケーションに組み込まれている[ngrok](https://ngrok.com/docs)を使用します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="22ef0-132">Ngrok はリバースプロキシソフトウェアツールであり、ローカルで実行されている web サーバーの公開された HTTPS エンドポイントへのトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="22ef0-133">サーバーの web エンドポイントは、ローカルコンピューターの現在のセッション中に使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="22ef0-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="22ef0-134">コンピューターがシャットダウンされるかスリープ状態になると、サービスは使用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="22ef0-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="22ef0-135">コマンドプロンプトで、localhost を終了し、次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="22ef0-136">タブが Microsoft teams にアップロードされ、 *ngrok*を介して正常に保存されると、トンネルセッションが終了するまで、teams でそのタブを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="22ef0-136">After your tab has been uploaded to Microsoft teams, via *ngrok*, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="22ef0-137">アプリケーションを Teams にアップロードする</span><span class="sxs-lookup"><span data-stu-id="22ef0-137">Upload your application to Teams</span></span>

- <span data-ttu-id="22ef0-138">Microsoft Teams クライアントを開きます。</span><span class="sxs-lookup"><span data-stu-id="22ef0-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="22ef0-139">[Web ベースのバージョン](https://teams.microsoft.com)を使用する場合は、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンドコードを調べることができます。</span><span class="sxs-lookup"><span data-stu-id="22ef0-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="22ef0-140">左側の [*チーム*] パネルで、使用して`...`いるチームの横のメニューを選択して、タブのテストを行い、[**チームの管理**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-140">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="22ef0-141">メインパネルで、タブバーから [**アプリ**] を選択し、ページの右下隅にある [**カスタムアプリのアップロード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="22ef0-142">プロジェクトディレクトリを開き、 **./パッケージ**フォルダーを参照し、zip フォルダーを選択して右クリックし、[**開く**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="22ef0-143">タブが Teams にアップロードされます。</span><span class="sxs-lookup"><span data-stu-id="22ef0-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="22ef0-144">個人用タブの表示</span><span class="sxs-lookup"><span data-stu-id="22ef0-144">View your personal tabs</span></span>

<span data-ttu-id="22ef0-145">Teams クライアントの左端にあるナビゲーションバーで、 `...`メニューを選択し、リストからアプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="22ef0-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>
