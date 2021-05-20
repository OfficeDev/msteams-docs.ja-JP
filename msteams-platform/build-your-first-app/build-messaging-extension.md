---
title: はじめに - メッセージング拡張機能を構築する
author: girliemac
description: Microsoft Teams Toolkitを使用して、Microsoft Teamsメッセージング拡張機能をすばやく作成します。
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: c120a5b5d878c549cde008c3e1ccc71743a4e24f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566062"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="fb6fb-103">Microsoft Teamsの最初のメッセージング拡張機能を構築する</span><span class="sxs-lookup"><span data-stu-id="fb6fb-103">Build your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="fb6fb-104">*Teamsメッセージング拡張機能* には、[検索コマンド](../messaging-extensions/how-to/search-commands/define-search-command.md)と [アクションコマンド](../messaging-extensions/how-to/action-commands/define-action-command.md)の 2 種類があります。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="fb6fb-105">このチュートリアルでは、外部コンテンツを検索してTeamsで共有するためのショートカットである *検索コマンド*(*検索ベースのメッセージング拡張機能* とも呼ばれます) を作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-105">This tutorial teaches you to create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="fb6fb-106">ユーザーは、Teams作成またはコマンド ボックスから検索コマンドにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-106">Users can access search commands from the Teams compose or command box.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="fb6fb-107">あなたが学ぶこと</span><span class="sxs-lookup"><span data-stu-id="fb6fb-107">What you'll learn</span></span>

* <span data-ttu-id="fb6fb-108">Visual Studio CodeのMicrosoft Teams Toolkitを使用して、アプリ プロジェクトとメッセージング拡張機能のボットを作成します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-108">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="fb6fb-109">アプリの構成と、メッセージング拡張機能に関連するスキャフォールディングについて理解する。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-109">Understand the app configurations and the scaffolding relevant to messaging extensions.</span></span>
* <span data-ttu-id="fb6fb-110">アプリをローカルでホストします。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-110">Host an app locally.</span></span>
* <span data-ttu-id="fb6fb-111">メッセージング拡張機能のボットを構成します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-111">Configure the bot for your messaging extension.</span></span>
* <span data-ttu-id="fb6fb-112">Teamsでメッセージング拡張機能をサイドロードしてテストします。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-112">Sideload and test a messaging extension in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb6fb-113">前提条件</span><span class="sxs-lookup"><span data-stu-id="fb6fb-113">Prerequisites</span></span>

<span data-ttu-id="fb6fb-114">簡単なTeams アプリを設定して構築する方法を理解していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-114">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="fb6fb-115">詳細については、[最初のMicrosoft Teams "Hello, World!" アプリを作成する](../build-your-first-app/build-and-run.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-115">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="fb6fb-116">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="fb6fb-116">1. Create your app project</span></span>

<span data-ttu-id="fb6fb-117">Microsoft Teams Toolkitは、メッセージング拡張機能の次のコンポーネントを設定するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-117">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="fb6fb-118">メッセージング拡張機能に関連 **するアプリの構成とスキャフォールディング**。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-118">**App configurations and scaffolding** relevant to messaging extensions.</span></span>
* <span data-ttu-id="fb6fb-119">**Microsoft Azure Bot** サービスに自動的に登録されるメッセージング拡張機能のボット。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-119">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service.</span></span>

<span data-ttu-id="fb6fb-120">**アプリ プロジェクトを作成するには**</span><span class="sxs-lookup"><span data-stu-id="fb6fb-120">**To create your app project**</span></span>

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。
1. <span data-ttu-id="fb6fb-122">メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-122">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="fb6fb-123">[**プロジェクトの選択**] 画面 **の [メッセージング拡張機能**  >  **検索**] で **、[JS (JavaScript)]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-123">On the **Select project** screen, at **Messaging Extensions** > **Search**, click **JS (JavaScript)**.</span></span> 
1. <span data-ttu-id="fb6fb-124">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-124">Enter a name for your Teams app.</span></span> <span data-ttu-id="fb6fb-125">これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前でもあります。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-125">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="fb6fb-126">[ **新しいボットを作成する** ] を選択し、[ **ボット登録の作成** ] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-126">Select **Create a new Bot** then click **Create Bot Registration** button.</span></span> <span data-ttu-id="fb6fb-127">成功した場合、新しいボットは *登録済み* ステータスになります。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-127">If successful, your new bot will have a *Registered* status.</span></span> <span data-ttu-id="fb6fb-128">これで、ボットが Microsoft Azure Bot サービスに自動的に登録されます。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-128">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 
1. <span data-ttu-id="fb6fb-129">画面の下部にある **[完了] を** 選択してプロジェクトを構成し、プロジェクトをローカル コンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-129">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="fb6fb-130">2. アプリ プロジェクト コンポーネントを理解する</span><span class="sxs-lookup"><span data-stu-id="fb6fb-130">2. Understand your app project components</span></span>

<span data-ttu-id="fb6fb-131">アプリの構成とスキャフォールディングの多くは、Teams Toolkitを使用してプロジェクトを作成するときに自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-131">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

* <span data-ttu-id="fb6fb-132">アプリの構成: メッセージング拡張機能の構成を表示または更新するには、ツールキットで **[App Studio]** を選択し、[ **メッセージング拡張機能**] に移動します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-132">App configurations: To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>
* <span data-ttu-id="fb6fb-133">アプリのスキャフォールディング: アプリのスキャフォールディングは `botActivityHandler.js` 、メッセージング拡張機能 (または技術的にはメッセージング拡張機能[のボット](#4-configure-the-bot-for-your-messaging-extension)) がTeamsの検索クエリにどのように応答するかを処理するために、プロジェクトのルート ディレクトリにあるファイルを提供します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-133">App scaffolding: The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="fb6fb-134">3. アプリへの安全なトンネルを設定する</span><span class="sxs-lookup"><span data-stu-id="fb6fb-134">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="fb6fb-135">テスト目的で、ローカル Web サーバー (ポート 3978) でメッセージング拡張機能をホストしましょう。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-135">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span> <span data-ttu-id="fb6fb-136">ローカルホストへのセキュアなトンネルを設定するために [ngrok](https://ngrok.com/download) を使用します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-136">You are going to use [ngrok](https://ngrok.com/download) to set up a secure tunnel to localhost.</span></span> <span data-ttu-id="fb6fb-137">詳細については[、最初のボットの構築Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet)参照してください。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-137">See [build your first bot for Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) for details.</span></span> 

1. <span data-ttu-id="fb6fb-138">まだインストールしていない場合は [、ngrok](https://ngrok.com/download)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-138">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="fb6fb-139">ターミナルで、 `ngrok http -host-header=rewrite 3978` を実行します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-139">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="fb6fb-140">Teamsには HTTPS 接続が必要なので、出力内の HTTPS URL をコピーします (例: `https://468b9ab725e9.ngrok.io` ) 。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-140">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

   <span data-ttu-id="fb6fb-141">この URL を使用すると、Teams (HTTPS 接続が必要) は、(ポート 3978 上の) アプリをホストしている場所にトンネルを作成できます `localhost` 。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-141">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="fb6fb-142">4. メッセージング拡張機能のボットを構成する</span><span class="sxs-lookup"><span data-stu-id="fb6fb-142">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="fb6fb-143">メッセージング拡張機能は、ボットに依存して、Teamsからホストされたサービスへのユーザー要求を送信および処理します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-143">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="fb6fb-144">ボットは、Teams Toolkitを使用してアプリを設定するときに実行された Azure Bot サービスに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-144">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="fb6fb-145">メッセージング拡張機能で検索クエリを受信および処理するには、ボット エンドポイント URL を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-145">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="fb6fb-146">通常、URL は `https://HOST_URL/api/messages` のようになります。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-146">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="fb6fb-147">この設定は、ツールキットですばやく構成できます。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-147">You can configure this quickly in the toolkit.</span></span>

1. Visual Studio Codeで、 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 左側のアクティビティ バーのMicrosoft Teamsを選択し **、[Microsoft Teams Toolkitを開く**] を選択します。
1. <span data-ttu-id="fb6fb-149">**[ボット>既存のボットの登録]** に移動し、セットアップ中に作成したボットを選択します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-149">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="fb6fb-150">[ **ボット エンドポイント アドレス]** フィールドに、ボットをホストしている ngrok URL (たとえば) を入力し、その URL `https://468b9ab725e9.ngrok.io` `/api/messages` に追加します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-150">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

   <span data-ttu-id="fb6fb-151">ボットは、メッセージング拡張機能でクエリを処理できるようになります。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-151">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="fb6fb-152">5. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="fb6fb-152">5. Build and run your app</span></span>

<span data-ttu-id="fb6fb-153">メッセージング拡張機能をホストする URL を設定し、検索を処理するように構成しました。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-153">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="fb6fb-154">アプリを起動して実行する時間です。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-154">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="fb6fb-155">ターミナルを開き、アプリ プロジェクトのルート ディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-155">Open terminal and go to the root directory of your app project.</span></span>
1. <span data-ttu-id="fb6fb-156">`npm install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-156">Run `npm install`.</span></span>
1. <span data-ttu-id="fb6fb-157">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-157">Run `npm start`.</span></span>

   <span data-ttu-id="fb6fb-158">正常に実行された場合、メッセージング拡張サービスが でのアクティビティをリッスンしていることを示す次のメッセージが表示されます `localhost` 。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-158">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="fb6fb-159">6. Teamsでメッセージング拡張機能をサイドロードする</span><span class="sxs-lookup"><span data-stu-id="fb6fb-159">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="fb6fb-160">メッセージング拡張機能を実行すると、Teamsでインストールできます。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-160">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="fb6fb-161">Teamsアプリを以前にサイドロードし、問題が発生していない場合は、次の[手順](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)に従ってください。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-161">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="fb6fb-162">Visual Studio Codeで **、F5** キーを選択して、Teams Web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-162">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="fb6fb-163">[アプリのインストール] ダイアログで、[ **追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-163">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="fb6fb-164">7. メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="fb6fb-164">7. Test your messaging extension</span></span>

<span data-ttu-id="fb6fb-165">Teams チャットでメッセージング拡張機能がどのように機能するかを説明します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-165">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="fb6fb-166">新しいチャットを開始します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-166">Start a new chat.</span></span> [新規作成] ボックスで [ **詳細**] を選択 :::image type="icon" source="../assets/icons/teams-client-more.png"::: し、サイドロードしたメッセージング拡張機能アプリを選択します。
1. <span data-ttu-id="fb6fb-168">何か (たとえば、 **チケット**) を検索してみてください。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-168">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="fb6fb-169">アプリが動作している場合は、サンプル検索結果が表示されます (後で独自に追加できます)。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-169">If your app is working, you'll see sample search results (you can add your own later).</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Teams作成ボックスで検索ベースのメッセージング拡張機能を使用する方法を示すスクリーンショット。":::

## <a name="troubleshooting"></a><span data-ttu-id="fb6fb-171">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="fb6fb-171">Troubleshooting</span></span>

<span data-ttu-id="fb6fb-172">このチュートリアルを完了する際に問題が発生した場合は、次の情報が役立ちます。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-172">The following information may help if you had issues completing this tutorial.</span></span>

<span data-ttu-id="fb6fb-173">**ボットがTeamsに接続されていない**</span><span class="sxs-lookup"><span data-stu-id="fb6fb-173">**Bot isn't connected to Teams**</span></span>

<span data-ttu-id="fb6fb-174">アプリをインストールしても動作しない場合は、メッセージング拡張機能のボットが Azure Bot Service の [Teams *チャネル* に接続](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-174">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="fb6fb-175">これはTeamsのチャンネルと同じではないことを理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-175">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="fb6fb-176">この場合、チャネルとは、Azure Bot サービスがボットをTeamsまたは[サポートされている別の Microsoft またはサードパーティの通信アプリ](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)に接続する方法です。</span><span class="sxs-lookup"><span data-stu-id="fb6fb-176">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="fb6fb-177">関連項目</span><span class="sxs-lookup"><span data-stu-id="fb6fb-177">See also</span></span>

* [<span data-ttu-id="fb6fb-178">Teams作成またはコマンド ボックス</span><span class="sxs-lookup"><span data-stu-id="fb6fb-178">Teams compose or command box</span></span>](../messaging-extensions/what-are-messaging-extensions.md) 
* [<span data-ttu-id="fb6fb-179">リンクを展開する機能を含める</span><span class="sxs-lookup"><span data-stu-id="fb6fb-179">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="fb6fb-180">デザインのガイドライン</span><span class="sxs-lookup"><span data-stu-id="fb6fb-180">Design guidelines</span></span>](../messaging-extensions/design/messaging-extension-design.md) 
* [<span data-ttu-id="fb6fb-181">プロダクション対応の UI テンプレート</span><span class="sxs-lookup"><span data-stu-id="fb6fb-181">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="fb6fb-182">認証を追加する</span><span class="sxs-lookup"><span data-stu-id="fb6fb-182">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="fb6fb-183">アクションベースのメッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="fb6fb-183">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="fb6fb-184">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="fb6fb-184">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)

## <a name="next-steps"></a><span data-ttu-id="fb6fb-185">次の手順</span><span class="sxs-lookup"><span data-stu-id="fb6fb-185">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fb6fb-186">検索コマンドを定義する</span><span class="sxs-lookup"><span data-stu-id="fb6fb-186">Define search commands</span></span>](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="fb6fb-187">ユーザーの検索に応答する</span><span class="sxs-lookup"><span data-stu-id="fb6fb-187">Respond to users' searches</span></span>](../messaging-extensions/how-to/search-commands/respond-to-search.md)
