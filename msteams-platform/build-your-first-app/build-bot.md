---
title: 開始する - ボットを作成する
author: heath-hamilton
description: Microsoft Teams ボットを使用して、Microsoft Teams ボットをすばやく作成Toolkit。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: fbabd5130f0b7eb648a980f5f143792cc4c17933
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911948"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="405ba-103">Microsoft Teams のボットを構築する</span><span class="sxs-lookup"><span data-stu-id="405ba-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="405ba-104">このチュートリアルでは、基本的な *ボット* アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="405ba-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="405ba-105">ボットは、Teams ユーザーと Web サービスの間の仲介者として機能します。</span><span class="sxs-lookup"><span data-stu-id="405ba-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="405ba-106">ユーザーはボットとチャットして、情報をすばやく取得したり、サービスによって実行されるワークフローやタスクを開始することができます。</span><span class="sxs-lookup"><span data-stu-id="405ba-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="405ba-107">割り当て</span><span class="sxs-lookup"><span data-stu-id="405ba-107">Your assignment</span></span>

<span data-ttu-id="405ba-108">職場で、タブを使用して重要 [な連絡先情報](../build-your-first-app/build-personal-tab.md) を表示する Teams アプリを作成しました。</span><span class="sxs-lookup"><span data-stu-id="405ba-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="405ba-109">たとえば、同僚はヘルプ デスクの電話番号にすばやくアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="405ba-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="405ba-110">しかし、ユーザーがチャットボットを使用してヘルプ デスクに問い合わせたらどうでしょうか。</span><span class="sxs-lookup"><span data-stu-id="405ba-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="405ba-111">上司から、Teams で基本的な会話ボットをどのくらいの速い時間で実行できるのか確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="405ba-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="405ba-112">学習する情報</span><span class="sxs-lookup"><span data-stu-id="405ba-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="405ba-113">Microsoft Teams Toolkit for Visual Studio コードを使用してアプリ プロジェクトとボットをVisual Studioする</span><span class="sxs-lookup"><span data-stu-id="405ba-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="405ba-114">ボットに関連するアプリ構成とスキャフォールディングの一部を特定する</span><span class="sxs-lookup"><span data-stu-id="405ba-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="405ba-115">アプリをローカルでホストする</span><span class="sxs-lookup"><span data-stu-id="405ba-115">Host an app locally</span></span>
> * <span data-ttu-id="405ba-116">Teams のボットを構成する</span><span class="sxs-lookup"><span data-stu-id="405ba-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="405ba-117">Teams でボットをサイドロードしてテストする</span><span class="sxs-lookup"><span data-stu-id="405ba-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="405ba-118">はじめに</span><span class="sxs-lookup"><span data-stu-id="405ba-118">Before you begin</span></span>

<span data-ttu-id="405ba-119">まだ理解していない場合は、Teams 開発の前提条件 [を理解してインストールしてください](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="405ba-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="405ba-120">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="405ba-120">1. Create your app project</span></span>

<span data-ttu-id="405ba-121">Microsoft Teams Toolkitは、アプリ用に次のコンポーネントを設定するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="405ba-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="405ba-122">**ボットに関連するアプリの** 構成とスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="405ba-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="405ba-123"> Microsoft Azure Bot Service に自動的に登録されるボット</span><span class="sxs-lookup"><span data-stu-id="405ba-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="405ba-124">Teams アプリ プロジェクトをまだ作成していない場合は、プロジェクトについて詳しく説明する次[](../build-your-first-app/build-and-run.md)の手順に従うのが役に立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="405ba-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. [Visual Studioコード] で、左側のアクティビティ バーで **Microsoft Teams** を選択し、[新しい Teams アプリの作成 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: ] **を選択します**。
1. <span data-ttu-id="405ba-126">ダイアログが表示されたら、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="405ba-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="405ba-127">[機能 **の追加] 画面で、[** ボット] **を選択** し、[次へ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="405ba-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="405ba-128">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="405ba-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="405ba-129">(これは、アプリの既定の名前と、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です)。</span><span class="sxs-lookup"><span data-stu-id="405ba-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="405ba-130">[ボットの **構成] に移動し** 、[新しい **ボットの作成] を** 選択し、[ **ボット登録の作成] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="405ba-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="405ba-131">成功した場合、新しいボットの状態は **登録済み** になります。</span><span class="sxs-lookup"><span data-stu-id="405ba-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="405ba-132">画面 **の** 下部にある [完了] を選択し、プロジェクトを作成する場所を選択します。</span><span class="sxs-lookup"><span data-stu-id="405ba-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="405ba-133">2. 関連するアプリ プロジェクト コンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="405ba-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="405ba-134">アプリの構成とスキャフォールディングの多くが、Teams アプリを使用してプロジェクトを作成するときに自動的に設定Toolkit。</span><span class="sxs-lookup"><span data-stu-id="405ba-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="405ba-135">ボットを構築する主なコンポーネントを見てみしましょう。</span><span class="sxs-lookup"><span data-stu-id="405ba-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="405ba-136">アプリの構成</span><span class="sxs-lookup"><span data-stu-id="405ba-136">App configurations</span></span>

<span data-ttu-id="405ba-137">ボットの構成を表示または更新するには、ツールキットで **App Studio** を選択し、[ボット] に **移動します**。</span><span class="sxs-lookup"><span data-stu-id="405ba-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="405ba-138">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="405ba-138">App scaffolding</span></span>

<span data-ttu-id="405ba-139">アプリのスキャフォールディングは、ボットが Teams でアクティビティを処理する方法 (たとえば、ボットが "Hello" などの特定のメッセージに応答する方法) を処理するために、プロジェクトのルート ディレクトリにあるファイルを提供します。 `botActivityHandler.js`</span><span class="sxs-lookup"><span data-stu-id="405ba-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="405ba-140">3. アプリへのセキュリティで保護されたトンネルを設定する</span><span class="sxs-lookup"><span data-stu-id="405ba-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="405ba-141">テストの目的で、ローカル Web サーバー (ポート 3978) でアプリをホストします。</span><span class="sxs-lookup"><span data-stu-id="405ba-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="405ba-142">まだインストールしていない場合は [、ngrok をインストールします](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="405ba-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="405ba-143">ターミナルで、次を実行します `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="405ba-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="405ba-144">Teams は HTTPS 接続を必要としますので、出力内の HTTPS URL (たとえば `https://468b9ab725e9.ngrok.io` ) をコピーします。</span><span class="sxs-lookup"><span data-stu-id="405ba-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="405ba-145">この URL を使用すると、Teams (HTTPS 接続が必要) は、アプリをホストしている場所 (ポート `localhost` 3978) にトンネリングできます。</span><span class="sxs-lookup"><span data-stu-id="405ba-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="405ba-146">4. ボットを構成する</span><span class="sxs-lookup"><span data-stu-id="405ba-146">4. Configure your bot</span></span>

<span data-ttu-id="405ba-147">Teams でボットを使用するには、Azure Bot Service にボットを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="405ba-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="405ba-148">Teams アプリを使用してアプリをセットアップすると、自動的にToolkit。</span><span class="sxs-lookup"><span data-stu-id="405ba-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="405ba-149">引き続き、ボットに送信されるユーザー メッセージ (要求) を受信および処理するエンドポイント アドレスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="405ba-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="405ba-150">通常、URL は次のように表示されます `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="405ba-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="405ba-151">この設定は、ツールキットですばやく構成できます。</span><span class="sxs-lookup"><span data-stu-id="405ba-151">You can configure this quickly in the toolkit.</span></span>

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Open Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Toolkit.**
1. <span data-ttu-id="405ba-153">既存の **ボット登録>ボットに移動し** 、セットアップ時に作成したボットを選択します。</span><span class="sxs-lookup"><span data-stu-id="405ba-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="405ba-154">[Bot **endpoint address]** フィールドに、ボットをホストしている ngrok URL (たとえば) を入力し、 `https://468b9ab725e9.ngrok.io` ボットに `/api/messages` 追加します。</span><span class="sxs-lookup"><span data-stu-id="405ba-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Teams アプリケーションでボット エンドポイント URL を構成できる場所を示すToolkit。":::

<span data-ttu-id="405ba-156">ボットは Teams のメッセージに応答できます。</span><span class="sxs-lookup"><span data-stu-id="405ba-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="405ba-157">5. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="405ba-157">5. Build and run your app</span></span>

<span data-ttu-id="405ba-158">ボットをホストする URL を設定し、メッセージを処理するようにボットを構成しました。</span><span class="sxs-lookup"><span data-stu-id="405ba-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="405ba-159">次に、アプリを起動して実行します。</span><span class="sxs-lookup"><span data-stu-id="405ba-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="405ba-160">ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、実行します `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="405ba-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="405ba-161">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="405ba-161">Run `npm start`.</span></span>

<span data-ttu-id="405ba-162">成功した場合、ボットが自分のアクティビティをリッスン中であることを示す次のメッセージが表示されます `localhost` 。</span><span class="sxs-lookup"><span data-stu-id="405ba-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="405ba-163">6. Teams でボットをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="405ba-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="405ba-164">ボットを実行すると、Teams にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="405ba-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="405ba-165">以前に Teams アプリをサイドローディングして問題が発生していない場合は、次の手順に [従います](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="405ba-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="405ba-166">コードVisual Studio **F5** キーを押して、Teams Web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="405ba-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="405ba-167">アプリのインストール ダイアログで、[追加] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="405ba-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="405ba-168">(ボットをチャネルまたはチャットに追加できますが、1 対 1 のチャットでボットをテストする方が、他のユーザーに対してはあまり邪魔ではありません)。</span><span class="sxs-lookup"><span data-stu-id="405ba-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="405ba-169">7. ボットをテストする</span><span class="sxs-lookup"><span data-stu-id="405ba-169">7. Test your bot</span></span>

<span data-ttu-id="405ba-170">ここで、楽しい部分について:ボットに "Hello" と言います。</span><span class="sxs-lookup"><span data-stu-id="405ba-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="405ba-171">作成ボックスで、メッセージを送信 `Hello` します。</span><span class="sxs-lookup"><span data-stu-id="405ba-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="405ba-172">ボットは次のようなメッセージで応答します。</span><span class="sxs-lookup"><span data-stu-id="405ba-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="ユーザーが Teams ボットに 「Hello」と言って応答を受け取るスクリーンショット。":::

## <a name="well-done"></a><span data-ttu-id="405ba-174">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="405ba-174">Well done</span></span>

<span data-ttu-id="405ba-175">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="405ba-175">Congratulations!</span></span> <span data-ttu-id="405ba-176">1 対 1 またはグループ設定 (チャネルとチャット) でユーザーと通信できる基本的な Teams ボットがあります。</span><span class="sxs-lookup"><span data-stu-id="405ba-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="405ba-177">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="405ba-177">Troubleshooting</span></span>

<span data-ttu-id="405ba-178">このチュートリアルを完了する上で問題が発生した場合は、次の情報が役立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="405ba-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="405ba-179">ボットが Teams に接続されていない</span><span class="sxs-lookup"><span data-stu-id="405ba-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="405ba-180">アプリをインストールしたがボットが機能しない場合は、ボットが Azure Bot Service の Teams チャネルに接続 [されていることを確認 *します*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="405ba-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="405ba-181">これは Teams のチャネルと同じではないという点を理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="405ba-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="405ba-182">この場合、チャネルは、Azure Bot Service がボットを Teams または別のサポートされている Microsoft またはサード パーティ通信アプリに接続 [する方法です](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="405ba-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="405ba-183">詳細情報</span><span class="sxs-lookup"><span data-stu-id="405ba-183">Learn more</span></span>

* [<span data-ttu-id="405ba-184">サンプルの 1 つで Teams ボットが実行できるその他の操作を参照する</span><span class="sxs-lookup"><span data-stu-id="405ba-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="405ba-185">ボット会話の基本</span><span class="sxs-lookup"><span data-stu-id="405ba-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* <span data-ttu-id="405ba-186">設計ガイドライン [に従い](../bots/design/bots.md) 、実稼働対応 [の UI](../concepts/design/design-teams-app-ui-templates.md) テンプレートを使用してビルドし、シームレスなエクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="405ba-186">Follow our [design guidelines](../bots/design/bots.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="405ba-187">Teams でのボット認証</span><span class="sxs-lookup"><span data-stu-id="405ba-187">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="405ba-188">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="405ba-188">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="405ba-189">ツールキットを使用せずにボットを作成する</span><span class="sxs-lookup"><span data-stu-id="405ba-189">Create a bot without the toolkit</span></span>](../bots/how-to/create-a-bot-for-teams.md)
