---
title: 使い始める - メッセージング拡張機能を作成する
author: girliemac
description: アプリケーションを使用してMicrosoft Teamsメッセージング拡張機能をすばやく作成Microsoft Teams Toolkit。
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: 91a5a15697163ee9103607511047a6411a5acf1a
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068760"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="3b5d8-103">ユーザー向け最初のメッセージング拡張機能をMicrosoft Teams</span><span class="sxs-lookup"><span data-stu-id="3b5d8-103">Build your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="3b5d8-104">メッセージング拡張機能には、検索Teams *アクション コマンド* の 2 [種類](../messaging-extensions/how-to/search-commands/define-search-command.md)[があります](../messaging-extensions/how-to/action-commands/define-action-command.md)。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="3b5d8-105">このチュートリアルでは、外部コンテンツを検索し、Teams で共有するショートカットである検索コマンド *(検索* ベースのメッセージング拡張機能とも呼ばれる) を作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-105">This tutorial teaches you to create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="3b5d8-106">ユーザーは、[新規作成] または [コマンド] ボックスからTeamsコマンドにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-106">Users can access search commands from the Teams compose or command box.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="3b5d8-107">学習する情報</span><span class="sxs-lookup"><span data-stu-id="3b5d8-107">What you'll learn</span></span>

* <span data-ttu-id="3b5d8-108">アプリ プロジェクトとメッセージング拡張機能ボットを作成するには、アプリ のMicrosoft Teams ToolkitをVisual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-108">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="3b5d8-109">アプリの構成とメッセージング拡張機能に関連するスキャフォールディングについて理解します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-109">Understand the app configurations and the scaffolding relevant to messaging extensions.</span></span>
* <span data-ttu-id="3b5d8-110">アプリをローカルでホストします。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-110">Host an app locally.</span></span>
* <span data-ttu-id="3b5d8-111">メッセージング拡張機能のボットを構成します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-111">Configure the bot for your messaging extension.</span></span>
* <span data-ttu-id="3b5d8-112">メッセージ拡張機能をサイドロードしてテストTeams。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-112">Sideload and test a messaging extension in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b5d8-113">前提条件</span><span class="sxs-lookup"><span data-stu-id="3b5d8-113">Prerequisites</span></span>

<span data-ttu-id="3b5d8-114">簡単なアプリをセットアップして構築する方法を理解Teamsしてください。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-114">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="3b5d8-115">詳細については[、「Hello, World!」アプリMicrosoft Teamsを作成するを参照してください](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-115">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="3b5d8-116">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="3b5d8-116">1. Create your app project</span></span>

<span data-ttu-id="3b5d8-117">このMicrosoft Teams Toolkitは、メッセージング拡張機能用に次のコンポーネントをセットアップするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-117">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="3b5d8-118">**メッセージング拡張機能に関連するアプリ** の構成とスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="3b5d8-118">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="3b5d8-119">**ボット** サービスに自動的に登録されるメッセージング拡張機能Microsoft Azureボット</span><span class="sxs-lookup"><span data-stu-id="3b5d8-119">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

<span data-ttu-id="3b5d8-120">**アプリ プロジェクトを作成するには**</span><span class="sxs-lookup"><span data-stu-id="3b5d8-120">**To create your app project**</span></span>

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。
1. <span data-ttu-id="3b5d8-122">メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-122">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="3b5d8-123">[プロジェクト **の選択]** 画面の [**メッセージング拡張機能** の検索]  >  **で、[JS** **(JavaScript) ] をクリックします**。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-123">On the **Select project** screen, at **Messaging Extensions** > **Search**, click **JS (JavaScript)**.</span></span> 
1. <span data-ttu-id="3b5d8-124">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-124">Enter a name for your Teams app.</span></span> <span data-ttu-id="3b5d8-125">これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-125">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="3b5d8-126">[新 **しいボットの作成] を選択し** 、[ **ボット登録の作成] ボタンをクリック** します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-126">Select **Create a new Bot** then click **Create Bot Registration** button.</span></span> <span data-ttu-id="3b5d8-127">成功した場合、新しいボットの状態は *[* 登録済み] になります。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-127">If successful, your new bot will have a *Registered* status.</span></span> <span data-ttu-id="3b5d8-128">これで、ボットは自動的にボット サービスMicrosoft Azure登録されます。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-128">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 
1. <span data-ttu-id="3b5d8-129">画面 **の下部** にある [完了] を選択してプロジェクトを構成し、プロジェクトをローカル コンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-129">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="3b5d8-130">2. アプリ プロジェクト コンポーネントについて</span><span class="sxs-lookup"><span data-stu-id="3b5d8-130">2. Understand your app project components</span></span>

<span data-ttu-id="3b5d8-131">アプリの構成とスキャフォールディングの多くが、プロジェクトを作成するときに自動的に設定Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-131">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

* <span data-ttu-id="3b5d8-132">アプリの構成: メッセージング拡張機能の構成を表示または更新するには、ツールキットで **[App Studio]** を選択し、[メッセージング拡張機能 **] に移動します**。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-132">App configurations: To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>
* <span data-ttu-id="3b5d8-133">アプリのスキャフォールディング: アプリのスキャフォールディングは、メッセージング拡張機能 (または技術的にはメッセージング拡張機能のボット) が Teams で検索クエリに応答する方法を処理するために、プロジェクトのルート ディレクトリにあるファイルを提供します。 `botActivityHandler.js` [](#4-configure-the-bot-for-your-messaging-extension)</span><span class="sxs-lookup"><span data-stu-id="3b5d8-133">App scaffolding: The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="3b5d8-134">3. アプリにセキュリティで保護されたトンネルを設定する</span><span class="sxs-lookup"><span data-stu-id="3b5d8-134">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="3b5d8-135">テストの目的で、メッセージング拡張機能をローカル Web サーバー (ポート 3978) でホストします。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-135">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span> <span data-ttu-id="3b5d8-136">[ngrok](https://ngrok.com/download)を使用して localhost へのセキュリティで保護されたトンネルを設定します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-136">You are going to use [ngrok](https://ngrok.com/download) to set up a secure tunnel to localhost.</span></span> <span data-ttu-id="3b5d8-137">詳細[については、「最初のボットをビルドMicrosoft Teams」](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-137">See [build your first bot for Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) for details.</span></span> 

1. <span data-ttu-id="3b5d8-138">まだインストールしていない場合は [、ngrok をインストールします](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-138">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="3b5d8-139">ターミナルで、 を実行します `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-139">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="3b5d8-140">HTTPS 接続が必要な場合は、出力内の HTTPS `https://468b9ab725e9.ngrok.io` URL (たとえば) Teamsコピーします。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-140">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

   <span data-ttu-id="3b5d8-141">この URL を使用Teams (HTTPS 接続が必要) は、アプリをホストしている場所 (ポート `localhost` 3978) にトンネルを接続できます。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-141">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="3b5d8-142">4. メッセージング拡張機能のボットを構成する</span><span class="sxs-lookup"><span data-stu-id="3b5d8-142">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="3b5d8-143">メッセージング拡張機能は、ボットを使用して、ホストされているサービスに対して、Teams要求を送信および処理します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-143">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="3b5d8-144">ボットは Azure Bot Service に登録されている必要があります。これは、アプリを使用してアプリをセットアップするときに実行Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-144">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="3b5d8-145">メッセージング拡張機能で検索クエリを受信および処理するには、ボット エンドポイント URL を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-145">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="3b5d8-146">通常、URL は次のように表示されます `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-146">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="3b5d8-147">この設定はツールキットですばやく構成できます。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-147">You can configure this quickly in the toolkit.</span></span>

1. [Visual Studio Code] で **Microsoft Teamsの**[アクティビティ バー] を選択し、[開く] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: Microsoft Teams Toolkit。 
1. <span data-ttu-id="3b5d8-149">[ボット] **>既存のボット登録に移動し、** セットアップ中に作成したボットを選択します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-149">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="3b5d8-150">[ **ボット エンドポイント アドレス** ] フィールドに、ボットをホストしている ngrok URL (たとえば) を入力し、 `https://468b9ab725e9.ngrok.io` ボットに `/api/messages` 追加します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-150">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

   <span data-ttu-id="3b5d8-151">ボットはメッセージング拡張機能でクエリを処理できます。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-151">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="3b5d8-152">5. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="3b5d8-152">5. Build and run your app</span></span>

<span data-ttu-id="3b5d8-153">メッセージング拡張機能をホストする URL を設定し、検索を処理するように構成しました。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-153">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="3b5d8-154">アプリを起動して実行する時間です。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-154">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="3b5d8-155">ターミナルを開き、アプリ プロジェクトのルート ディレクトリに移動する</span><span class="sxs-lookup"><span data-stu-id="3b5d8-155">Open terminal and go to the root directory of your app project</span></span>
1. <span data-ttu-id="3b5d8-156">`npm install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-156">Run `npm install`.</span></span>
1. <span data-ttu-id="3b5d8-157">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-157">Run `npm start`.</span></span>

   <span data-ttu-id="3b5d8-158">成功した場合は、メッセージング拡張機能サービスがアクティビティをリッスン中であることを示す次のメッセージが表示されます `localhost` 。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-158">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="3b5d8-159">6. メッセージング拡張機能をサイドロードTeams</span><span class="sxs-lookup"><span data-stu-id="3b5d8-159">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="3b5d8-160">メッセージング拡張機能を実行すると、メッセージング拡張機能をインストールTeams。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-160">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="3b5d8-161">以前にアプリをサイドロードTeams問題が発生していない場合は、次の手順に[従います](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-161">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="3b5d8-162">[Visual Studio Code **F5** キーを選択して、Web クライアントTeams起動します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-162">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="3b5d8-163">[アプリのインストール] ダイアログで、[追加] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-163">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="3b5d8-164">7. メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="3b5d8-164">7. Test your messaging extension</span></span>

<span data-ttu-id="3b5d8-165">メッセージング拡張機能がチャットでどのように機能Teamsします。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-165">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="3b5d8-166">新しいチャットを開始します。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-166">Start a new chat.</span></span> 作成ボックスで、[詳細] **を選択** し、サイドロードしたメッセージング :::image type="icon" source="../assets/icons/teams-client-more.png"::: 拡張機能アプリを選択します。
1. <span data-ttu-id="3b5d8-168">何かを検索してみてください (**チケットなど)。**</span><span class="sxs-lookup"><span data-stu-id="3b5d8-168">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="3b5d8-169">アプリが動作している場合は、サンプル検索結果が表示されます (後で独自の検索結果を追加できます)。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-169">If your app is working, you'll see sample search results (you can add your own later).</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="[メッセージ作成] ボックスで検索ベースのメッセージング拡張機能がどのように使用Teamsスクリーンショットです。":::

## <a name="troubleshooting"></a><span data-ttu-id="3b5d8-171">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="3b5d8-171">Troubleshooting</span></span>

<span data-ttu-id="3b5d8-172">このチュートリアルの完了に問題がある場合は、次の情報が役立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-172">The following information may help if you had issues completing this tutorial.</span></span>

<span data-ttu-id="3b5d8-173">**ボットがデバイスに接続Teams**</span><span class="sxs-lookup"><span data-stu-id="3b5d8-173">**Bot isn't connected to Teams**</span></span>

<span data-ttu-id="3b5d8-174">アプリをインストールしたが機能しない場合は、メッセージング拡張機能のボットが Azure Bot Service のサービス チャネルに接続されていることを [Teams *してください*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-174">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="3b5d8-175">これは、チャネルと同じではないと理解することが重要Teams。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-175">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="3b5d8-176">この場合、チャネルとは、Azure Bot Service がボットを他の microsoft またはサード パーティの通信アプリTeamsに接続する[方法です](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3b5d8-176">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="3b5d8-177">関連項目</span><span class="sxs-lookup"><span data-stu-id="3b5d8-177">See also</span></span>

* [<span data-ttu-id="3b5d8-178">Teams作成またはコマンド ボックス</span><span class="sxs-lookup"><span data-stu-id="3b5d8-178">Teams compose or command box</span></span>](../messaging-extensions/what-are-messaging-extensions.md) 
* [<span data-ttu-id="3b5d8-179">リンクのリンク解除機能を含める</span><span class="sxs-lookup"><span data-stu-id="3b5d8-179">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="3b5d8-180">デザインのガイドライン</span><span class="sxs-lookup"><span data-stu-id="3b5d8-180">Design guidelines</span></span>](../messaging-extensions/design/messaging-extension-design.md) 
* [<span data-ttu-id="3b5d8-181">実稼働対応の UI テンプレート</span><span class="sxs-lookup"><span data-stu-id="3b5d8-181">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="3b5d8-182">認証を追加する</span><span class="sxs-lookup"><span data-stu-id="3b5d8-182">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="3b5d8-183">アクション ベースのメッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="3b5d8-183">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="3b5d8-184">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b5d8-184">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)

## <a name="next-steps"></a><span data-ttu-id="3b5d8-185">次の手順</span><span class="sxs-lookup"><span data-stu-id="3b5d8-185">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b5d8-186">検索コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="3b5d8-186">Define search commands</span></span>](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b5d8-187">ユーザーの検索に応答する</span><span class="sxs-lookup"><span data-stu-id="3b5d8-187">Respond to users' searches</span></span>](../messaging-extensions/how-to/search-commands/respond-to-search.md)