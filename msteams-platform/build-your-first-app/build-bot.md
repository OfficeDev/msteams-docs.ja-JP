---
title: 作業の開始-bot をビルドする
author: heath-hamilton
description: Microsoft Teams ツールキットを使用して、Microsoft Teams bot をすばやく作成できます。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 1229064ac6b7aab73c50048f0764c6a2353ab54a
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931741"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="dbbac-103">Microsoft Teams の bot を構築する</span><span class="sxs-lookup"><span data-stu-id="dbbac-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="dbbac-104">このチュートリアルでは、基本的な *bot* アプリを構築します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="dbbac-105">Bot は Teams ユーザーと web サービス間の仲介者として機能します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="dbbac-106">ユーザーは bot とチャットして、サービスによって実行された情報をすばやく取得したり、ワークフローやタスクを開始したりできます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="dbbac-107">自分の割り当て</span><span class="sxs-lookup"><span data-stu-id="dbbac-107">Your assignment</span></span>

<span data-ttu-id="dbbac-108">Workplace は、 [タブ](../build-your-first-app/build-personal-tab.md) を使用して重要な連絡先情報を表示する Teams アプリを作成しました。</span><span class="sxs-lookup"><span data-stu-id="dbbac-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="dbbac-109">たとえば、仕事仲間は、ヘルプデスクの電話番号にすばやくアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="dbbac-110">しかし、通話の代わりに、ユーザーが chatbot を使用してヘルプデスクに連絡することができた場合はどうなりますか。</span><span class="sxs-lookup"><span data-stu-id="dbbac-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="dbbac-111">上司からは、Teams での基本的な会話をすばやく実行する方法を確認するように求められています。</span><span class="sxs-lookup"><span data-stu-id="dbbac-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="dbbac-112">学習内容</span><span class="sxs-lookup"><span data-stu-id="dbbac-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="dbbac-113">Microsoft Teams Toolkit for Visual Studio Code を使用してアプリプロジェクトとボットを作成する</span><span class="sxs-lookup"><span data-stu-id="dbbac-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="dbbac-114">Bot に関連するアプリの構成とスキャフォールディングの一部を特定する</span><span class="sxs-lookup"><span data-stu-id="dbbac-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="dbbac-115">アプリをローカルでホストする</span><span class="sxs-lookup"><span data-stu-id="dbbac-115">Host an app locally</span></span>
> * <span data-ttu-id="dbbac-116">Teams の bot を構成する</span><span class="sxs-lookup"><span data-stu-id="dbbac-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="dbbac-117">Teams でボットをサイドロードおよびテストする</span><span class="sxs-lookup"><span data-stu-id="dbbac-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dbbac-118">はじめに</span><span class="sxs-lookup"><span data-stu-id="dbbac-118">Before you begin</span></span>

<span data-ttu-id="dbbac-119">まだお持ちでない場合は、 [Teams 開発の前提条件を理解し、インストール](build-first-app-overview.md#get-prerequisites)してください。</span><span class="sxs-lookup"><span data-stu-id="dbbac-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="dbbac-120">1. アプリプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-120">1. Create your app project</span></span>

<span data-ttu-id="dbbac-121">Microsoft Teams Toolkit は、アプリ用に次のコンポーネントをセットアップするのに役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="dbbac-122">**アプリの構成と** ボットに関連するスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="dbbac-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="dbbac-123">Microsoft Azure Bot サービスに自動的に登録された **Bot**</span><span class="sxs-lookup"><span data-stu-id="dbbac-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="dbbac-124">以前に Teams アプリプロジェクトを作成していない場合は、 [以下の手順](../build-your-first-app/build-and-run.md) に従って、プロジェクトについて詳しく説明することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="dbbac-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成** ] を選択します。
1. <span data-ttu-id="dbbac-126">メッセージが表示されたら、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="dbbac-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="dbbac-127">[ **機能の追加** ] 画面で、[ **Bot** ] を選択し、[ **次へ** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="dbbac-128">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="dbbac-129">(これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)</span><span class="sxs-lookup"><span data-stu-id="dbbac-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="dbbac-130">[ **Bot を構成** する] に移動して、[ **新しい bot を作成し、** **ボット登録を作成** する] を選択します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="dbbac-131">成功した場合、新しい bot は **登録済み** の状態になります。</span><span class="sxs-lookup"><span data-stu-id="dbbac-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="dbbac-132">画面の下部にある [ **完了** ] を選択し、プロジェクトを作成する場所を選択します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="dbbac-133">2. 関連するアプリプロジェクトコンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="dbbac-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="dbbac-134">Teams ツールキットを使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="dbbac-135">Bot を構築するための主なコンポーネントを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="dbbac-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="dbbac-136">アプリの構成</span><span class="sxs-lookup"><span data-stu-id="dbbac-136">App configurations</span></span>

<span data-ttu-id="dbbac-137">Bot の構成を表示または更新するには、ツールキットで [ **App Studio** ] を選択し、[ **bot** ] に移動します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="dbbac-138">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="dbbac-138">App scaffolding</span></span>

<span data-ttu-id="dbbac-139">アプリのスキャフォールディングは、 `botActivityHandler.js` ボットが Teams でのアクティビティを処理する方法について、プロジェクトのルートディレクトリにあるファイルを提供します (たとえば、"Hello" のような特定のメッセージに bot が応答する方法)。</span><span class="sxs-lookup"><span data-stu-id="dbbac-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="dbbac-140">3. アプリへのセキュリティで保護されたトンネルをセットアップする</span><span class="sxs-lookup"><span data-stu-id="dbbac-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="dbbac-141">テストのために、アプリケーションをローカル web サーバーでホストします (ポート 3978)。</span><span class="sxs-lookup"><span data-stu-id="dbbac-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="dbbac-142">まだインストールしていない場合は、 [ngrok](https://ngrok.com/download)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="dbbac-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="dbbac-143">ターミナルで、を実行 `ngrok http -host-header=rewrite 3978` します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="dbbac-144">Teams で HTTPS 接続が必要になったため、出力に HTTPS URL (たとえば、) をコピーし `https://468b9ab725e9.ngrok.io` ます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="dbbac-145">この URL を使用すると、Teams (HTTPS 接続を必要とする) は、アプリをホストしている場所にトンネルでき `localhost` ます (ポート 3978)。</span><span class="sxs-lookup"><span data-stu-id="dbbac-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="dbbac-146">4. bot を構成する</span><span class="sxs-lookup"><span data-stu-id="dbbac-146">4. Configure your bot</span></span>

<span data-ttu-id="dbbac-147">Teams でボットを使用するには、その bot を Azure Bot サービスに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dbbac-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="dbbac-148">さいわい、Teams ツールキットを使用してアプリをセットアップすると、これは自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="dbbac-149">その場合でも、bot に送信されるユーザーメッセージ (つまり、要求) を受信して処理するために、エンドポイントアドレスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dbbac-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="dbbac-150">通常、URL はのように `https://HOST_URL/api/messages` なります。</span><span class="sxs-lookup"><span data-stu-id="dbbac-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="dbbac-151">これは、ツールキットですばやく構成できます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-151">You can configure this quickly in the toolkit.</span></span>

1. Visual Studio Code で、左側のアクティビティバーで [ **Microsoft teams** ] を選択し、 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: [ **microsoft Teams ツールキットを開く** ] を選択します。
1. <span data-ttu-id="dbbac-153">[ **ボット > 既存の bot 登録** ] に移動し、セットアップ時に作成した bot を選択します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="dbbac-154">**Bot エンドポイントアドレス** フィールドに、bot をホストしている ngrok URL (たとえば、) を入力 `https://468b9ab725e9.ngrok.io` し `/api/messages` ます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Teams ツールキットで bot エンドポイント URL を構成できる場所を示す図。":::

<span data-ttu-id="dbbac-156">Bot は Teams のメッセージに応答できるようになります。</span><span class="sxs-lookup"><span data-stu-id="dbbac-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="dbbac-157">5. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="dbbac-157">5. Build and run your app</span></span>

<span data-ttu-id="dbbac-158">Bot をホストする URL を設定し、メッセージを処理するように構成します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="dbbac-159">アプリを起動して実行します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="dbbac-160">ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="dbbac-161">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-161">Run `npm start`.</span></span>

<span data-ttu-id="dbbac-162">成功した場合、ボットが自分のアクティビティをリッスンしていることを示す次のメッセージが表示され `localhost` ます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="dbbac-163">6 Teams での bot のサイドロード</span><span class="sxs-lookup"><span data-stu-id="dbbac-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="dbbac-164">Bot を実行している場合は、Teams にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="dbbac-165">以前に Teams アプリをサイドロードしていない場合は、以下の [手順](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)を実行します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="dbbac-166">Visual Studio Code で、 **F5** キーを押して Teams web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="dbbac-167">[アプリのインストール] ダイアログで、[ **追加** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="dbbac-168">(Bot をチャネルやチャットに追加することはできますが、1対1のチャットで bot をテストするには他の人には邪魔されません)。</span><span class="sxs-lookup"><span data-stu-id="dbbac-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="dbbac-169">7. bot をテストする</span><span class="sxs-lookup"><span data-stu-id="dbbac-169">7. Test your bot</span></span>

<span data-ttu-id="dbbac-170">おもしろい部分は、次のようにしてください。 bot に "Hello" と言うことができます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="dbbac-171">[新規作成] ボックスで、 `Hello` メッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="dbbac-172">Bot は次のようなメッセージに返信します。</span><span class="sxs-lookup"><span data-stu-id="dbbac-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="ユーザーが Teams の bot に _OL_QUOTE_PLACEHOLDER_Hello_OL_QUOTE_PLACEHOLDER_ と言って、応答を取得することを示すスクリーンショット。":::

## <a name="well-done"></a><span data-ttu-id="dbbac-174">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="dbbac-174">Well done</span></span>

<span data-ttu-id="dbbac-175">おめでとうございます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-175">Congratulations!</span></span> <span data-ttu-id="dbbac-176">ユーザーが1対1で、またはグループ設定 (チャネルとチャット) で通信できる基本的な Teams bot があります。</span><span class="sxs-lookup"><span data-stu-id="dbbac-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="dbbac-177">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="dbbac-177">Troubleshooting</span></span>

<span data-ttu-id="dbbac-178">このチュートリアルを完了する際に問題が発生した場合は、次の情報が役立ちます。</span><span class="sxs-lookup"><span data-stu-id="dbbac-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="dbbac-179">Bot が Teams に接続されていない</span><span class="sxs-lookup"><span data-stu-id="dbbac-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="dbbac-180">アプリをインストールしたが、bot が動作していない場合は、ボットが [Azure Bot サービスの Teams *チャネル* に接続](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="dbbac-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="dbbac-181">これは Teams のチャネルと同じではないことを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="dbbac-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="dbbac-182">この場合、チャネルは、Azure Bot サービスが Bot を Teams または他の [サポートされている Microsoft またはサードパーティの通信アプリ](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)に接続する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="dbbac-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="dbbac-183">詳細情報</span><span class="sxs-lookup"><span data-stu-id="dbbac-183">Learn more</span></span>

* [<span data-ttu-id="dbbac-184">サンプルのいずれかで、他の Teams のボットができることを確認する</span><span class="sxs-lookup"><span data-stu-id="dbbac-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="dbbac-185">ボット会話の基本</span><span class="sxs-lookup"><span data-stu-id="dbbac-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="dbbac-186">Teams での Bot 認証</span><span class="sxs-lookup"><span data-stu-id="dbbac-186">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="dbbac-187">Microsoft Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="dbbac-187">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="dbbac-188">ツールキットなしでボットを作成する</span><span class="sxs-lookup"><span data-stu-id="dbbac-188">Create a bot without the toolkit</span></span>](../bots/how-to/create-a-bot-for-teams.md)
