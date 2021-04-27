---
title: Microsoft Teams のカスタム チャネルとグループ タブNode.js Yeoman Generator を作成する
author: laujan
description: Microsoft Teams 用 Yeoman Generator を使用してチャネルとグループ タブを作成するクイック スタート ガイド。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 962a558014a3bc84010860082df6891bb48c7715
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020304"
---
# <a name="create-a-custom-channel-and-group-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="baaa1-103">Microsoft Teams 用のカスタム チャネルとグループ Node.js Yeoman Generator を使用して作成する</span><span class="sxs-lookup"><span data-stu-id="baaa1-103">Create a custom channel and group tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="baaa1-104">このクイック スタートは、Microsoft OfficeDev GitHub リポジトリにある最初の Microsoft [Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki のビルドで説明されている手順に従います。</span><span class="sxs-lookup"><span data-stu-id="baaa1-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="baaa1-105">このクイック スタートでは、Teams Yeoman ジェネレーターを使用してカスタム チャネルとグループ タブを作成 [する方法について説明します](https://github.com/OfficeDev/generator-teams/)。</span><span class="sxs-lookup"><span data-stu-id="baaa1-105">In this quickstart we'll walk-through creating a custom channel and group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="baaa1-106">**構成可能なタブまたは静的タブを作成しますか?**</span><span class="sxs-lookup"><span data-stu-id="baaa1-106">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="baaa1-107">矢印キーを使用して、構成可能なタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="baaa1-107">Use the arrow keys to select configurable tab.</span></span>

<span data-ttu-id="baaa1-108">**Tab に使用するスコープは何ですか?**</span><span class="sxs-lookup"><span data-stu-id="baaa1-108">**What scopes do you intend to use for your Tab?**</span></span>

<span data-ttu-id="baaa1-109">チームチャットまたはグループ チャットを選択できます</span><span class="sxs-lookup"><span data-stu-id="baaa1-109">You can select a Team and/or a group chat</span></span>

<span data-ttu-id="baaa1-110">**このタブを SharePoint Online で使用できますか?(Y/n)**</span><span class="sxs-lookup"><span data-stu-id="baaa1-110">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span> 

<span data-ttu-id="baaa1-111">**[n] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="baaa1-111">Select **n**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="baaa1-112">このクイック スタートで参照されるパス コンポーネント **yourDefaultTabNameTab** は、[既定のタブ名] のジェネレーターに入力した値に Tab という単語を加 **えた値です**。</span><span class="sxs-lookup"><span data-stu-id="baaa1-112">The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
>
><span data-ttu-id="baaa1-113">例: DefaultTabName: **MyTab**  =>  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="baaa1-113">For example: DefaultTabName: **MyTab** => **/MyTabTab/**</span></span>

<span data-ttu-id="baaa1-114">プロジェクト ディレクトリで、次の場所に移動します。</span><span class="sxs-lookup"><span data-stu-id="baaa1-114">In your project directory, navigate to the following:</span></span>

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

<span data-ttu-id="baaa1-115">そこで、タブ ロジックを見つける必要があります。</span><span class="sxs-lookup"><span data-stu-id="baaa1-115">That is where you'll find your tab logic.</span></span> <span data-ttu-id="baaa1-116">メソッドを `render()` 見つけて、コンテナー コードの上部に `<div>` 次のタグとコンテンツを `<PanelBody>` 追加します。</span><span class="sxs-lookup"><span data-stu-id="baaa1-116">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

<span data-ttu-id="baaa1-117">更新されたファイルを保存してください。</span><span class="sxs-lookup"><span data-stu-id="baaa1-117">Make sure to save the updated file.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="baaa1-118">アプリケーションのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="baaa1-118">Build and Run Your Application</span></span>

<span data-ttu-id="baaa1-119">プロジェクト ディレクトリでコマンド プロンプトを開き、次のタスクを完了します。</span><span class="sxs-lookup"><span data-stu-id="baaa1-119">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="baaa1-120">タブ構成ページを表示するには、 に移動します `https://localhost:3007/<yourDefaultAppNameTab>/config.html` 。</span><span class="sxs-lookup"><span data-stu-id="baaa1-120">To view your tab configuration page go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="baaa1-121">以下のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="baaa1-121">You should see the following:</span></span>

![構成ページのスクリーンショット](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="baaa1-123">タブへのセキュリティで保護されたトンネルを確立する</span><span class="sxs-lookup"><span data-stu-id="baaa1-123">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="baaa1-124">Microsoft Teams は完全にクラウドベースの製品であり、HTTPS エンドポイントを使用してタブ コンテンツをクラウドから利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="baaa1-124">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="baaa1-125">Teams ではローカル ホスティングが許可されていないので、タブをパブリック URL に発行するか、ローカル ポートをインターネットに接続する URL に公開するプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="baaa1-125">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="baaa1-126">タブ拡張機能をテストするには、このアプリケーションに組み込まれる [ngrok](https://ngrok.com/docs)を使用します。</span><span class="sxs-lookup"><span data-stu-id="baaa1-126">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="baaa1-127">Ngrok はリバース プロキシ ソフトウェア ツールで、ローカルで実行中の Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="baaa1-127">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="baaa1-128">サーバーの Web エンドポイントは、ローカル コンピューター上の現在のセッション中に利用できます。</span><span class="sxs-lookup"><span data-stu-id="baaa1-128">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="baaa1-129">コンピューターがシャットダウンまたはスリープ状態になった場合、サービスは使用できなくなりました。</span><span class="sxs-lookup"><span data-stu-id="baaa1-129">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="baaa1-130">コマンド プロンプトで localhost を終了し、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="baaa1-130">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="baaa1-131">タブが Microsoft チームにアップロードされ、正常に保存された後は、タブ ギャラリーでタブを表示し、タブ バーに追加し、ngrok トンネル セッションが終了するまで操作できます。</span><span class="sxs-lookup"><span data-stu-id="baaa1-131">After your tab has been uploaded to Microsoft teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="baaa1-132">ngrok セッションを再起動する場合は、新しい URL でアプリを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="baaa1-132">If you restart your ngrok session, you'll need to update your app with the new URL.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="baaa1-133">アプリケーションを Teams にアップロードする</span><span class="sxs-lookup"><span data-stu-id="baaa1-133">Upload your application to Teams</span></span>

- <span data-ttu-id="baaa1-134">Microsoft Teams クライアントを開きます。</span><span class="sxs-lookup"><span data-stu-id="baaa1-134">Open the Microsoft Teams client.</span></span> <span data-ttu-id="baaa1-135">Web ベースのバージョン [を使用する](https://teams.microsoft.com) 場合は、ブラウザーの開発者ツールを使用してフロントエンド コードを [検査できます](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="baaa1-135">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="baaa1-136">左側の *[YourTeams]* パネルで、タブのテストに使用するチームの横にあるメニューを選択し、[チームの管理 `...` ] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="baaa1-136">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="baaa1-137">メイン パネルでタブ バーから **[アプリ**]を選択し、ページの右下隅にある [カスタム アプリのアップロード] を選択します。</span><span class="sxs-lookup"><span data-stu-id="baaa1-137">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="baaa1-138">プロジェクト ディレクトリを開き **、./package** フォルダーを参照し、アプリ パッケージの zip フォルダーを選択し、[開く] を選択 **します**。</span><span class="sxs-lookup"><span data-stu-id="baaa1-138">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="baaa1-139">タブが Teams にアップロードされます。</span><span class="sxs-lookup"><span data-stu-id="baaa1-139">Your tab will upload into Teams.</span></span>
- <span data-ttu-id="baaa1-140">チームに戻り、タブを表示するチャネルを選択し、タブ バーから [➕] を選択し、ギャラリーからタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="baaa1-140">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
- <span data-ttu-id="baaa1-141">タブを追加するには、指示に従います。チャネル/グループ タブのカスタム構成ダイアログがあります。</span><span class="sxs-lookup"><span data-stu-id="baaa1-141">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab.</span></span>
- <span data-ttu-id="baaa1-142">[ **保存]** を選択すると、タブがチャネルのタブ バーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="baaa1-142">Select **Save** and your tab will be added to the channel's tab bar.</span></span>
