---
title: '[スタート] - ボットを作成する'
author: heath-hamilton
description: Microsoft Teams ボットを使用して Microsoft Teams ボットをすばやく作成Toolkit。
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 5dfbfa05d2f1e36bbc14bd929cb2592303081522
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020001"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="3b5a5-103">Microsoft Teams 用のボットを作成する</span><span class="sxs-lookup"><span data-stu-id="3b5a5-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="3b5a5-104">このチュートリアルでは、基本的 *なボット アプリ* を作成します。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="3b5a5-105">ボットは、Teams ユーザーと Web サービスの間の仲介者として機能します。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="3b5a5-106">ユーザーはボットとチャットして、情報をすばやく取得したり、サービスによって実行されるワークフローやタスクを開始できます。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="3b5a5-107">割り当て</span><span class="sxs-lookup"><span data-stu-id="3b5a5-107">Your assignment</span></span>

<span data-ttu-id="3b5a5-108">職場では、タブを使用して重要 [な連絡先情報を](../build-your-first-app/build-personal-tab.md) 表示する Teams アプリを作成しました。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="3b5a5-109">たとえば、同僚はヘルプ デスクの電話番号にすばやくアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="3b5a5-110">しかし、通話の代わりに、チャットボットを使用してヘルプ デスクに問い合わせたらどうしますか?</span><span class="sxs-lookup"><span data-stu-id="3b5a5-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="3b5a5-111">上司から、Teams で基本的な会話ボットを立ち上げ、実行できる時間を確認するメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="3b5a5-112">学習する情報</span><span class="sxs-lookup"><span data-stu-id="3b5a5-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="3b5a5-113">Microsoft Teams を使用してアプリ プロジェクトとボットを作成ToolkitコードVisual Studioする</span><span class="sxs-lookup"><span data-stu-id="3b5a5-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="3b5a5-114">ボットに関連するアプリ構成とスキャフォールディングの一部を特定する</span><span class="sxs-lookup"><span data-stu-id="3b5a5-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="3b5a5-115">アプリをローカルでホストする</span><span class="sxs-lookup"><span data-stu-id="3b5a5-115">Host an app locally</span></span>
> * <span data-ttu-id="3b5a5-116">Teams のボットを構成する</span><span class="sxs-lookup"><span data-stu-id="3b5a5-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="3b5a5-117">Teams でボットをサイドロードしてテストする</span><span class="sxs-lookup"><span data-stu-id="3b5a5-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3b5a5-118">はじめに</span><span class="sxs-lookup"><span data-stu-id="3b5a5-118">Before you begin</span></span>

<span data-ttu-id="3b5a5-119">まだインストールしていない場合は、Teams 開発の [前提条件を理解してインストールしてください](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="3b5a5-120">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="3b5a5-120">1. Create your app project</span></span>

<span data-ttu-id="3b5a5-121">Microsoft Teams Toolkitは、アプリの次のコンポーネントをセットアップするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="3b5a5-122">**ボットに関連するアプリの構成** とスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="3b5a5-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="3b5a5-123"> Microsoft Azure Bot Service に自動的に登録されるボット</span><span class="sxs-lookup"><span data-stu-id="3b5a5-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="3b5a5-124">以前に Teams アプリ プロジェクトを作成したことがない場合は、プロジェクトの詳細を[](../build-your-first-app/build-and-run.md)説明する手順に従うのが役に立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。
1. <span data-ttu-id="3b5a5-126">メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="3b5a5-127">[機能の **追加] 画面で、[** ボット] 、[ **次へ] の順** に **選択します**。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="3b5a5-128">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="3b5a5-129">(これは、アプリの既定の名前であり、ローカル コンピューター上のアプリのプロジェクト ディレクトリの名前でもあります)。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="3b5a5-130">[ボットの **構成] に移動し**、[**新しいボットの作成] を選択し、[\*\*\*\*ボット登録の作成] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="3b5a5-131">成功した場合、新しいボットの状態は **[** 登録済み] になります。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="3b5a5-132">画面 **の下部** にある [完了] を選択し、プロジェクトを作成する場所を選択します。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="3b5a5-133">2. 関連するアプリ プロジェクト コンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="3b5a5-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="3b5a5-134">Teams を使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的にToolkit。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="3b5a5-135">ボットを構築する主要なコンポーネントについて説明します。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="3b5a5-136">アプリの構成</span><span class="sxs-lookup"><span data-stu-id="3b5a5-136">App configurations</span></span>

<span data-ttu-id="3b5a5-137">ボットの構成を表示または更新するには、ツールキットで **[App Studio]** を選択し、[ボット] **に移動します**。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="3b5a5-138">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="3b5a5-138">App scaffolding</span></span>

<span data-ttu-id="3b5a5-139">アプリのスキャフォールディングは、プロジェクトのルート ディレクトリにあるファイルを提供し、ボットが Teams でアクティビティを処理する方法 (たとえば、ボットが "Hello" などの特定のメッセージに応答する方法など) を処理します `botActivityHandler.js` 。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="3b5a5-140">3. アプリにセキュリティで保護されたトンネルを設定する</span><span class="sxs-lookup"><span data-stu-id="3b5a5-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="3b5a5-141">テストの目的で、アプリをローカル Web サーバー (ポート 3978) でホストします。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="3b5a5-142">まだインストールしていない場合は [、ngrok をインストールします](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="3b5a5-143">ターミナルで、 を実行します `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="3b5a5-144">Teams が HTTPS 接続を必要としますので、出力内の HTTPS URL (たとえば `https://468b9ab725e9.ngrok.io` ) をコピーします。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="3b5a5-145">この URL を使用すると、Teams (HTTPS 接続が必要) は、アプリをホストしている場所 (ポート `localhost` 3978) にトンネルを接続できます。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="3b5a5-146">4. ボットを構成する</span><span class="sxs-lookup"><span data-stu-id="3b5a5-146">4. Configure your bot</span></span>

<span data-ttu-id="3b5a5-147">Teams でボットを使用するには、Azure Bot Service にボットを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="3b5a5-148">幸運なことに、Teams アプリケーションを使用してアプリをセットアップすると、自動的にToolkit。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="3b5a5-149">引き続き、ボットに送信されるユーザー メッセージ (要求) を受信および処理するエンドポイント アドレスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="3b5a5-150">通常、URL は次のように表示されます `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="3b5a5-151">この設定はツールキットですばやく構成できます。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-151">You can configure this quickly in the toolkit.</span></span>

1. [Visual Studioコード] で、左側の [アクティビティ バー] で **[Microsoft Teams]** を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し **、[Microsoft Teams** を開く] Toolkit。
1. <span data-ttu-id="3b5a5-153">[ボット] **>既存のボット登録に移動し、** セットアップ中に作成したボットを選択します。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="3b5a5-154">[ **ボット エンドポイント アドレス** ] フィールドに、ボットをホストしている ngrok URL (たとえば) を入力し、 `https://468b9ab725e9.ngrok.io` ボットに `/api/messages` 追加します。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Teams サーバーでボット エンドポイント URL を構成できる場所を示すToolkit。":::

<span data-ttu-id="3b5a5-156">ボットは Teams のメッセージに応答できます。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="3b5a5-157">5. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="3b5a5-157">5. Build and run your app</span></span>

<span data-ttu-id="3b5a5-158">ボットをホストする URL を設定し、メッセージを処理するように構成しました。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="3b5a5-159">アプリを起動して実行する時間です。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="3b5a5-160">ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、`npm install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="3b5a5-161">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-161">Run `npm start`.</span></span>

<span data-ttu-id="3b5a5-162">成功した場合は、ボットがアクティビティをリッスン中であることを示す次のメッセージが表示されます `localhost` 。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="3b5a5-163">6. Teams でボットをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="3b5a5-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="3b5a5-164">ボットを実行すると、Teams にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="3b5a5-165">以前に Teams アプリをサイドロードし、問題が発生していない場合は、次の手順に [従います](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="3b5a5-166">[Visual Studioコード] で **、F5** キーを押して Teams Web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="3b5a5-167">[アプリのインストール] ダイアログで、[追加] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="3b5a5-168">(ボットをチャネルまたはチャットに追加できますが、1 対 1 のチャットでボットをテストする場合は、他のユーザーにはあまり邪魔ではありません)。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="3b5a5-169">7. ボットをテストする</span><span class="sxs-lookup"><span data-stu-id="3b5a5-169">7. Test your bot</span></span>

<span data-ttu-id="3b5a5-170">ここでは、ボットに "Hello" と言います。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="3b5a5-171">作成ボックスで、メッセージを送信 `Hello` します。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="3b5a5-172">ボットは次のようなメッセージで返信します。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="ユーザーが Teams ボットに 「Hello」 と答え、応答を取得するスクリーンショット。":::

## <a name="well-done"></a><span data-ttu-id="3b5a5-174">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="3b5a5-174">Well done</span></span>

<span data-ttu-id="3b5a5-175">お疲れさまでした。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-175">Congratulations!</span></span> <span data-ttu-id="3b5a5-176">ユーザーと 1 対 1 またはグループ設定 (チャネルとチャット) で通信できる基本的な Teams ボットがあります。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3b5a5-177">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="3b5a5-177">Troubleshooting</span></span>

<span data-ttu-id="3b5a5-178">このチュートリアルの完了に問題がある場合は、次の情報が役立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="3b5a5-179">ボットが Teams に接続されていない</span><span class="sxs-lookup"><span data-stu-id="3b5a5-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="3b5a5-180">アプリをインストールしたがボットが機能しない場合は、ボットが Azure Bot Service の Teams チャネルに接続 [されていることを確認 *します*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="3b5a5-181">これは Teams のチャネルと同じではないと理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="3b5a5-182">この場合、チャネルとは、Azure Bot Service がボットを Teams または別のサポートされている Microsoft またはサード パーティの通信アプリに接続 [する方法です](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="3b5a5-183">詳細情報</span><span class="sxs-lookup"><span data-stu-id="3b5a5-183">Learn more</span></span>

* [<span data-ttu-id="3b5a5-184">Teams ボットがサンプルの 1 つで実行できるその他の操作を参照する</span><span class="sxs-lookup"><span data-stu-id="3b5a5-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="3b5a5-185">ボット会話の基本</span><span class="sxs-lookup"><span data-stu-id="3b5a5-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* <span data-ttu-id="3b5a5-186">シームレスな [エクスペリエンスを作成するには、](../bots/design/bots.md) 設計ガイドラインに従い、実稼働対応 [の UI](../concepts/design/design-teams-app-ui-templates.md) テンプレートを使用してビルドします。</span><span class="sxs-lookup"><span data-stu-id="3b5a5-186">Follow our [design guidelines](../bots/design/bots.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="3b5a5-187">Teams でのボット認証</span><span class="sxs-lookup"><span data-stu-id="3b5a5-187">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="3b5a5-188">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="3b5a5-188">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="3b5a5-189">ツールキットなしでボットを作成する</span><span class="sxs-lookup"><span data-stu-id="3b5a5-189">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)
