---
title: Node.jsとヨーマンジェネレータを使用したカスタムチャンネルとグループタブを作成Microsoft Teams
author: laujan
description: Microsoft Teams用の Yeoman ジェネレータを使用してチャネルとグループ タブを作成するクイック スタート ガイドです。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 559393884e3b8a4aad1787ea4ca8f9f4de54d151
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566647"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="cc752-103">Node.jsとYeoman ジェネレータを使用して、カスタムチャネルとグループタブを作成Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="cc752-103">Create a custom channel and group tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="cc752-104">このクイック スタートは、Microsoft OfficeDev GitHub リポジトリにある[最初のMicrosoft Teams アプリ](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)Wiki で説明されている手順に従います。</span><span class="sxs-lookup"><span data-stu-id="cc752-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="cc752-105">このクイック スタートでは、 [Yeoman ジェネレーター を](https://github.com/OfficeDev/generator-teams/)使用してカスタム チャネルとグループ タブを作成する方法Teamsします。</span><span class="sxs-lookup"><span data-stu-id="cc752-105">In this quickstart we'll walk-through creating a custom channel and group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="cc752-106">**構成可能なタブまたは静的タブを作成しますか?**</span><span class="sxs-lookup"><span data-stu-id="cc752-106">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="cc752-107">矢印キーを使用して、構成可能なタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="cc752-107">Use the arrow keys to select configurable tab.</span></span>

<span data-ttu-id="cc752-108">**Tab に使用するスコープを指定してください。**</span><span class="sxs-lookup"><span data-stu-id="cc752-108">**What scopes do you intend to use for your Tab?**</span></span>

<span data-ttu-id="cc752-109">チームチャットやグループチャットを選択できます。</span><span class="sxs-lookup"><span data-stu-id="cc752-109">You can select a Team and/or a group chat</span></span>

<span data-ttu-id="cc752-110">**このタブをオンラインで使用できるようにしますSharePoint?(Y/n)**</span><span class="sxs-lookup"><span data-stu-id="cc752-110">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span> 

<span data-ttu-id="cc752-111">n を選択します。</span><span class="sxs-lookup"><span data-stu-id="cc752-111">Select **n**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="cc752-112">このクイック スタートで参照されているパス コンポーネント **の DefaultTabNameTab** は、ジェネレータで **[既定のタブ名]** に入力した値 **と、Tab** という語を使用して入力した値です。</span><span class="sxs-lookup"><span data-stu-id="cc752-112">The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
>
><span data-ttu-id="cc752-113">たとえば、デフォルトタブ名:**マイタブ**  =>  **/マイタブタブ/**</span><span class="sxs-lookup"><span data-stu-id="cc752-113">For example: DefaultTabName: **MyTab** => **/MyTabTab/**</span></span>

<span data-ttu-id="cc752-114">プロジェクト ディレクトリで、次のディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="cc752-114">In your project directory, navigate to the following:</span></span>

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

<span data-ttu-id="cc752-115">そこでタブロジックを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="cc752-115">That is where you'll find your tab logic.</span></span> <span data-ttu-id="cc752-116">メソッドを探 `render()` し、次の `<div>` タグとコンテンツをコンテナー コードの先頭に追加 `<PanelBody>` します。</span><span class="sxs-lookup"><span data-stu-id="cc752-116">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

<span data-ttu-id="cc752-117">更新されたファイルを保存してください。</span><span class="sxs-lookup"><span data-stu-id="cc752-117">Make sure to save the updated file.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="cc752-118">アプリケーションのビルドと実行</span><span class="sxs-lookup"><span data-stu-id="cc752-118">Build and Run Your Application</span></span>

<span data-ttu-id="cc752-119">プロジェクト ディレクトリでコマンド プロンプトを開き、次のタスクを完了します。</span><span class="sxs-lookup"><span data-stu-id="cc752-119">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="cc752-120">タブの構成ページを表示するには、 に移動 `https://localhost:3007/<yourDefaultAppNameTab>/config.html` します。</span><span class="sxs-lookup"><span data-stu-id="cc752-120">To view your tab configuration page go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="cc752-121">以下のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="cc752-121">You should see the following:</span></span>

![構成ページのスクリーンショット](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="cc752-123">タブへの安全なトンネルを確立する</span><span class="sxs-lookup"><span data-stu-id="cc752-123">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="cc752-124">Microsoft Teamsは完全にクラウドベースの製品であり、HTTPS エンドポイントを使用してクラウドからタブ コンテンツを利用できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="cc752-124">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="cc752-125">Teamsローカル ホスティングを許可しないため、タブをパブリック URL に公開するか、インターネットに接続する URL にローカル ポートを公開するプロキシを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cc752-125">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="cc752-126">タブ拡張をテストするには、このアプリケーションに組み込まれている [ngrok](https://ngrok.com/docs)を使用します。</span><span class="sxs-lookup"><span data-stu-id="cc752-126">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="cc752-127">Ngrok はリバース プロキシ ソフトウェア ツールで、ローカルで実行されている Web サーバーの一般に公開されている HTTPS エンドポイントへのトンネルを作成します。</span><span class="sxs-lookup"><span data-stu-id="cc752-127">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="cc752-128">サーバーの Web エンドポイントは、ローカル コンピューター上の現在のセッション中に使用できます。</span><span class="sxs-lookup"><span data-stu-id="cc752-128">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="cc752-129">マシンがシャットダウンまたはスリープ状態になると、サービスは利用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="cc752-129">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="cc752-130">コマンド プロンプトで localhost を終了し、次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="cc752-130">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="cc752-131">タブが Microsoft チームにアップロードされ、正常に保存された後、タブ ギャラリーで表示し、タブ バーに追加して、ngrok トンネル セッションが終了するまで操作できます。</span><span class="sxs-lookup"><span data-stu-id="cc752-131">After your tab has been uploaded to Microsoft teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="cc752-132">ngrok セッションを再開する場合は、新しい URL でアプリを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cc752-132">If you restart your ngrok session, you'll need to update your app with the new URL.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="cc752-133">アプリケーションをTeamsにアップロードする</span><span class="sxs-lookup"><span data-stu-id="cc752-133">Upload your application to Teams</span></span>

- <span data-ttu-id="cc752-134">Microsoft Teams クライアントを開きます。</span><span class="sxs-lookup"><span data-stu-id="cc752-134">Open the Microsoft Teams client.</span></span> <span data-ttu-id="cc752-135">Web ベースの [バージョン](https://teams.microsoft.com) を使用する場合は、ブラウザーの [開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンド コードを検査できます。</span><span class="sxs-lookup"><span data-stu-id="cc752-135">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="cc752-136">左側の *[YourTeams]* パネルで、 `...` タブのテストに使用しているチームの横にあるメニューを選択し、[ **チームの管理**]を選択します。</span><span class="sxs-lookup"><span data-stu-id="cc752-136">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="cc752-137">メインパネルでタブバーから **「アプリ**」を選択し、ページの右下隅にある **カスタムアプリアップロード** 選択します。</span><span class="sxs-lookup"><span data-stu-id="cc752-137">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="cc752-138">プロジェクト ディレクトリを開き **、./package** フォルダを参照し、アプリ パッケージの zip フォルダーを選択して 、[ **開く**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="cc752-138">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="cc752-139">タブがTeamsにアップロードされます。</span><span class="sxs-lookup"><span data-stu-id="cc752-139">Your tab will upload into Teams.</span></span>
- <span data-ttu-id="cc752-140">チームに戻り、タブを表示するチャンネルを選択し、タブバーから➕選択して、ギャラリーからタブを選択します。</span><span class="sxs-lookup"><span data-stu-id="cc752-140">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
- <span data-ttu-id="cc752-141">タブを追加する手順に従います。チャンネル/グループタブにはカスタム設定ダイアログがあります。</span><span class="sxs-lookup"><span data-stu-id="cc752-141">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab.</span></span>
- <span data-ttu-id="cc752-142">[ **保存]** を選択すると、チャンネルのタブバーにタブが追加されます。</span><span class="sxs-lookup"><span data-stu-id="cc752-142">Select **Save** and your tab will be added to the channel's tab bar.</span></span>

## <a name="next-step"></a><span data-ttu-id="cc752-143">次の手順</span><span class="sxs-lookup"><span data-stu-id="cc752-143">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cc752-144">ASP.NETCore を使用してカスタム チャネルとグループ タブを作成する</span><span class="sxs-lookup"><span data-stu-id="cc752-144">Create a Custom Channel and Group Tab with ASP.NETCore</span></span>](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)