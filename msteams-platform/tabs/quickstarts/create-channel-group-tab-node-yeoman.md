---
title: Node.js を使用してカスタムのチャネルとグループタブを作成し、Microsoft Teams 用の Outlook を使用する
author: laujan
description: Microsoft Teams 用のごみ箱のジェネレーターを使用して、チャネルおよびグループタブを作成するためのクイックスタートガイド。
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: c5e028dcc117d729f2bf366923d03568b7f557a4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674833"
---
# <a name="create-a-custom-channel-and-group-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="2d9bd-103">Node.js を使用してカスタムのチャネルとグループタブを作成し、Microsoft Teams 用の Outlook を使用する</span><span class="sxs-lookup"><span data-stu-id="2d9bd-103">Create a custom channel and group tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="2d9bd-104">このクイックスタートは、「Microsoft OfficeDev GitHub リポジトリにある[最初の Microsoft Teams アプリ](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)Wiki を構築する」に記載されている手順に従います。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="2d9bd-105">このクイックスタートでは、Teams の [[オマーン] ジェネレーター](https://github.com/OfficeDev/generator-teams/)を使用して、カスタムのチャネルとグループタブを作成する手順を順を追って説明します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-105">In this quickstart we'll walk-through creating a custom channel and group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="2d9bd-106">**構成可能なタブまたは静的タブを作成しますか?**</span><span class="sxs-lookup"><span data-stu-id="2d9bd-106">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="2d9bd-107">方向キーを使用して、[構成可能なタブ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-107">Use the arrow keys to select configurable tab.</span></span>

<span data-ttu-id="2d9bd-108">**タブに使用するスコープを決定します。**</span><span class="sxs-lookup"><span data-stu-id="2d9bd-108">**What scopes do you intend to use for your Tab?**</span></span>

<span data-ttu-id="2d9bd-109">チームまたはグループチャット (あるいはその両方) を選択できます。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-109">You can select a Team and/or a group chat</span></span>

<span data-ttu-id="2d9bd-110">**このタブを SharePoint Online で使用できるようにしますか。(Y/n)**</span><span class="sxs-lookup"><span data-stu-id="2d9bd-110">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span> 

<span data-ttu-id="2d9bd-111">[ **N**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-111">Select **n**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="2d9bd-112">このクイックスタートで参照される path コンポーネントの**Defaulttabnametab**は、[**既定のタブ名**] と [word **] タブ**に入力した値です。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-112">The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
>
><span data-ttu-id="2d9bd-113">例: defaulttabname: **MyTab** => /**mytabtab/**</span><span class="sxs-lookup"><span data-stu-id="2d9bd-113">For example: DefaultTabName: **MyTab** => **/MyTabTab/**</span></span>

<span data-ttu-id="2d9bd-114">プロジェクトディレクトリで、次の場所に移動します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-114">In your project directory, navigate to the following:</span></span>

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

<span data-ttu-id="2d9bd-115">ここでは、タブロジックについて説明します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-115">That is where you'll find your tab logic.</span></span> <span data-ttu-id="2d9bd-116">`render()`メソッドを検索し、次`<div>`のタグとコンテンツを`<PanelBody>`コンテナーコードの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-116">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

<span data-ttu-id="2d9bd-117">更新したファイルを保存してください。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-117">Make sure to save the updated file.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="2d9bd-118">アプリケーションをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="2d9bd-118">Build and Run Your Application</span></span>

<span data-ttu-id="2d9bd-119">プロジェクトディレクトリでコマンドプロンプトを開いて、次のタスクを完了します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-119">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="2d9bd-120">[タブの構成] ページを表示`https://localhost:3007/<yourDefaultAppNameTab>/config.html`するには、に移動します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-120">To view your tab configuration page go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="2d9bd-121">以下のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-121">You should see the following:</span></span>

![構成ページのスクリーンショット](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="2d9bd-123">タブへのセキュリティで保護されたトンネルの確立</span><span class="sxs-lookup"><span data-stu-id="2d9bd-123">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="2d9bd-124">Microsoft Teams は完全なクラウドベースの製品であり、HTTPS エンドポイントを使用してクラウドからタブのコンテンツを利用できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-124">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="2d9bd-125">Teams ではローカルホスティングが許可されていません。そのため、タブをパブリック URL に公開するか、またはプロキシを使用して、ローカルポートをインターネットに接続する URL に公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-125">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="2d9bd-126">タブ拡張機能をテストするには、このアプリケーションに組み込まれている[ngrok](https://ngrok.com/docs)を使用します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-126">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="2d9bd-127">Ngrok はリバースプロキシソフトウェアツールであり、ローカルで実行されている web サーバーの公開された HTTPS エンドポイントへのトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-127">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="2d9bd-128">サーバーの web エンドポイントは、ローカルコンピューターの現在のセッション中に使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-128">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="2d9bd-129">コンピューターがシャットダウンされるかスリープ状態になると、サービスは使用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-129">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="2d9bd-130">コマンドプロンプトで、localhost を終了し、次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-130">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="2d9bd-131">タブが Microsoft teams にアップロードされて正常に保存されると、タブギャラリーで表示し、[タブ] バーに追加して、ngrok トンネルセッションが終了するまでそれを操作することができます。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-131">After your tab has been uploaded to Microsoft teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="2d9bd-132">Ngrok セッションを再起動する場合は、新しい URL を使用してアプリを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-132">If you restart your ngrok session, you'll need to update your app with the new URL.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="2d9bd-133">アプリケーションを Teams にアップロードする</span><span class="sxs-lookup"><span data-stu-id="2d9bd-133">Upload your application to Teams</span></span>

- <span data-ttu-id="2d9bd-134">Microsoft Teams クライアントを開きます。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-134">Open the Microsoft Teams client.</span></span> <span data-ttu-id="2d9bd-135">[Web ベースのバージョン](https://teams.microsoft.com)を使用する場合は、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンドコードを調べることができます。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-135">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="2d9bd-136">左側の [*チーム*] パネルで、使用して`...`いるチームの横のメニューを選択して、タブのテストを行い、[**チームの管理**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-136">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="2d9bd-137">メインパネルで、タブバーから [**アプリ**] を選択し、ページの右下隅にある [**カスタムアプリのアップロード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-137">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="2d9bd-138">プロジェクトディレクトリを開き、 **./パッケージ**フォルダーを参照して、アプリパッケージの zip フォルダーを選択し、[**開く**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-138">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="2d9bd-139">タブが Teams にアップロードされます。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-139">Your tab will upload into Teams.</span></span>
- <span data-ttu-id="2d9bd-140">チームに戻り、タブを表示するチャネルを選択し、タブバーから [➕] を選択して、ギャラリーからタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-140">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
- <span data-ttu-id="2d9bd-141">タブを追加する手順に従います。 [チャネル/グループ] タブには、カスタム構成ダイアログがあることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-141">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab.</span></span>
- <span data-ttu-id="2d9bd-142">[**保存**] を選択すると、タブがチャネルのタブバーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="2d9bd-142">Select **Save** and your tab will be added to the channel's tab bar.</span></span>
