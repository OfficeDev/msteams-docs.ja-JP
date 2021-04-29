---
title: '[スタート] - ボットを作成する'
author: girliemac
description: Microsoft Teams ボットを使用して Microsoft Teams ボットをすばやく作成Toolkit。
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: dbb6f0a2497a0914d8e14473f1dbd6b2b225fc96
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068631"
---
# <a name="create-your-first-bot-for-teams"></a><span data-ttu-id="9c333-103">Teams 用の最初のボットを作成する</span><span class="sxs-lookup"><span data-stu-id="9c333-103">Create your first bot for Teams</span></span>

<span data-ttu-id="9c333-104">このチュートリアルでは、基本的なボット アプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="9c333-104">This tutorial teaches you to build a basic bot app.</span></span> <span data-ttu-id="9c333-105">ボットは、Teams ユーザーと会話型インターフェイスを使用した Web アプリまたはサービス間の仲介として機能します。</span><span class="sxs-lookup"><span data-stu-id="9c333-105">A bot acts as an intermediary between Teams users and your web app or service with a conversational interface.</span></span> <span data-ttu-id="9c333-106">ユーザーはボットとチャットして、情報をすばやく取得したり、サービスによって実行されるワークフローやタスクを開始できます。</span><span class="sxs-lookup"><span data-stu-id="9c333-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="9c333-107">学習する情報</span><span class="sxs-lookup"><span data-stu-id="9c333-107">What you'll learn</span></span>

* <span data-ttu-id="9c333-108">Microsoft Teams を使用してアプリ プロジェクトとボットを作成し、ToolkitコードVisual Studioします。</span><span class="sxs-lookup"><span data-stu-id="9c333-108">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="9c333-109">ボットに関連する Teams アプリの構成について理解します。</span><span class="sxs-lookup"><span data-stu-id="9c333-109">Understand the Teams app configurations relevant to bots.</span></span>
* <span data-ttu-id="9c333-110">ローカル ホスト トンネリング ソリューションを使用してアプリをローカルでホストして実行します。</span><span class="sxs-lookup"><span data-stu-id="9c333-110">Host and run an app locally using a localhost tunneling solution.</span></span>
* <span data-ttu-id="9c333-111">Teams でボットをサイドロードしてテストします。</span><span class="sxs-lookup"><span data-stu-id="9c333-111">Sideload and test a bot in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c333-112">前提条件</span><span class="sxs-lookup"><span data-stu-id="9c333-112">Prerequisites</span></span>

<span data-ttu-id="9c333-113">簡単な Teams アプリをセットアップしてビルドする方法を理解してください。</span><span class="sxs-lookup"><span data-stu-id="9c333-113">Ensure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="9c333-114">詳細については、「Hello, World!」アプリの最初の Microsoft Teams の作成 [に関するページをご覧ください](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="9c333-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span> 

## <a name="1-create-your-app-project"></a><span data-ttu-id="9c333-115">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="9c333-115">1. Create your app project</span></span>

<span data-ttu-id="9c333-116">Microsoft Teams Toolkitは、アプリの次のコンポーネントをセットアップするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="9c333-116">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span> 

* <span data-ttu-id="9c333-117">**ボットに関連するアプリの構成** とスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="9c333-117">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="9c333-118"> Microsoft Azure Bot Service に自動的に登録されるボット</span><span class="sxs-lookup"><span data-stu-id="9c333-118">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

<span data-ttu-id="9c333-119">**アプリ プロジェクトを作成するには**</span><span class="sxs-lookup"><span data-stu-id="9c333-119">**To create your app project**</span></span>

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Teams アプリケーションでアプリを作成する方法を示すスクリーンショットToolkit。":::

1. <span data-ttu-id="9c333-122">メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="9c333-122">When prompted, sign in with your Microsoft 365 development account.</span></span> 
1. <span data-ttu-id="9c333-123">[プロジェクトの選択] 画面で、[会話ボット] を選択します。</span><span class="sxs-lookup"><span data-stu-id="9c333-123">On the Select project screen, select Conversation bots:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Teams サーバーで新しいボットを作成する方法を示すスクリーンショットToolkit。":::

1. <span data-ttu-id="9c333-125">[プロジェクトの **構成] 画面** で、ボットの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="9c333-125">On the **Configure project** screen, enter a name for your bot.</span></span> <span data-ttu-id="9c333-126">これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です。</span><span class="sxs-lookup"><span data-stu-id="9c333-126">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="9c333-127">次 **の図に示すように、[ボット**  >  **登録の** 作成] を選択します。</span><span class="sxs-lookup"><span data-stu-id="9c333-127">Select **Create a new Bot** > **Create Bot Registration** as shown in the following image:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Teams アプリケーションで新しいボットに名前を付けるToolkit。":::

    <span data-ttu-id="9c333-129">成功した場合、新しいボットの状態は **[** 登録済み] になります。</span><span class="sxs-lookup"><span data-stu-id="9c333-129">If successful, your new bot will have a **Registered** status.</span></span> <span data-ttu-id="9c333-130">これで、ボットが Microsoft Azure Bot Service に自動的に登録されます。</span><span class="sxs-lookup"><span data-stu-id="9c333-130">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Teams サーバーに新しいボットを登録するToolkit。":::

1. <span data-ttu-id="9c333-132">画面 **の下部** にある [完了] を選択し、プロジェクトをコンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="9c333-132">Select **Finish** at the bottom of the screen and save your project on your machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="9c333-133">2. アプリ プロジェクト コンポーネントについて</span><span class="sxs-lookup"><span data-stu-id="9c333-133">2. Understand your app project components</span></span>

<span data-ttu-id="9c333-134">Teams を使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的にToolkit。</span><span class="sxs-lookup"><span data-stu-id="9c333-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="9c333-135">ボットを構築する主なコンポーネントを見てみ取る:</span><span class="sxs-lookup"><span data-stu-id="9c333-135">Let's look at the main components for building a bot:</span></span>

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Teams のプロジェクト スキャフォールディングを示すスクリーンショットToolkit。":::

<span data-ttu-id="9c333-137">別のチュートリアルでタブを作成した場合、ボットのアプリスキャフォールディングは異なります。</span><span class="sxs-lookup"><span data-stu-id="9c333-137">If you created a tab in another tutorial, the app scaffolding for the bot is different.</span></span> <span data-ttu-id="9c333-138">タブとは異なり、ボットの開発では、フロントエンド Web コンポーネントをビルドしたり、Teams JavaScript クライアント SDK を使用する必要は一切ない。</span><span class="sxs-lookup"><span data-stu-id="9c333-138">Unlike tabs, bot development doesn't require you to build any front-end web components or use the Teams JavaScript client SDK.</span></span>  <span data-ttu-id="9c333-139">代わりに、スキャフォールディングは [Microsoft Bot Framework](https://dev.botframework.com/)を使用します。これは、Web、モバイル、およびもちろん Teams で動作するインテリジェントなエンタープライズ レベルのボットを構築するオープンソース SDK です。</span><span class="sxs-lookup"><span data-stu-id="9c333-139">Instead, the scaffolding uses the [Microsoft Bot Framework](https://dev.botframework.com/), which is an open-source SDK for building intelligent, enterprise-grade bots that can work on the web, mobile, and of course Teams!</span></span> 

<span data-ttu-id="9c333-140">プロジェクトのルート ディレクトリにあるファイルは、ボットが特定のメッセージに応答する方法など、ボットアクティビティを処理する Teams 固有の `botActivityHandler.js` ハンドラーです。</span><span class="sxs-lookup"><span data-stu-id="9c333-140">The `botActivityHandler.js` file, located in the root directory of your project, is the Teams-specific handler that handles bot activities, such as how the bot responds to specific messages.</span></span> <span data-ttu-id="9c333-141">アプリのスキャフォールディングは、プロジェクトのルート ディレクトリにあるファイルを提供し、ボットが特定のメッセージに応答する方法などのボット アクティビティを処理する Teams 固有のハンドラー `botActivityHandler.js` です。</span><span class="sxs-lookup"><span data-stu-id="9c333-141">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, is the Teams specific handler that handles bot activities such as how the bot responds to specific messages.</span></span>

## <a name="3-securely-expose-your-localhost-to-the-internet"></a><span data-ttu-id="9c333-142">3. localhost をインターネットに安全に公開する</span><span class="sxs-lookup"><span data-stu-id="9c333-142">3. Securely expose your localhost to the internet</span></span>

<span data-ttu-id="9c333-143">HTTP サーバーを作成し、ボットへの受信要求をリッスンするルーティングを処理するファイル `index.js` を確認します。</span><span class="sxs-lookup"><span data-stu-id="9c333-143">Take a look at the `index.js` file, which creates an HTTP server and handles routing to listen for incoming requests to your bot.</span></span> <span data-ttu-id="9c333-144">クライアント `/api/messages` 要求に応答するアプリのエンドポイント URL を次に示します。</span><span class="sxs-lookup"><span data-stu-id="9c333-144">The `/api/messages` is your app's endpoint URL to respond to client requests:</span></span> 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

<span data-ttu-id="9c333-145">ボットのロジックに要求を転送するには、. `https://example.com/api/messages` `https://localhost`</span><span class="sxs-lookup"><span data-stu-id="9c333-145">To forward the requests to your bot's logic, you must set up a publicly accessible URL, such as `https://example.com/api/messages`, instead of `https://localhost`.</span></span> <span data-ttu-id="9c333-146">アプリは現在 localhost から実行されているので、ネットワークを *トンネリングする* 必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c333-146">Because your app is running from your localhost currently, you must *tunnel* the network.</span></span>

<span data-ttu-id="9c333-147">トンネリングは、ネットワーク間でデータを転送できるプロトコルです。</span><span class="sxs-lookup"><span data-stu-id="9c333-147">Tunneling is a protocol that allows you to transport data across a network.</span></span> <span data-ttu-id="9c333-148">localhost トンネリングを使用すると、ローカル コンピューターとリモート接続間の接続が提供されます。</span><span class="sxs-lookup"><span data-stu-id="9c333-148">And localhost tunneling gives you a connection between your local machine and a remote connection.</span></span> <span data-ttu-id="9c333-149">localhost をインターネットに安全に公開するには **、ngrok** というサードパーティ製のツールを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9c333-149">To securely expose your localhost to the internet, we recommend you to use the 3rd party tool called, **ngrok**.</span></span> <span data-ttu-id="9c333-150">これにより、セキュリティで保護された URL が提供されます。</span><span class="sxs-lookup"><span data-stu-id="9c333-150">This will give you a secure URL.</span></span> 

1. <span data-ttu-id="9c333-151">サイトに移動 [ngrok.com](https://ngrok.com/download) 指示に従って、環境に ngrok をインストールしてセットアップします。</span><span class="sxs-lookup"><span data-stu-id="9c333-151">Go to the [ngrok.com](https://ngrok.com/download) site and follow the instruction to install and set up ngrok in your environment.</span></span> 
    
    <span data-ttu-id="9c333-152">システム PATH 環境変数にインストールngrok.exeファイルへの完全パスを追加します。</span><span class="sxs-lookup"><span data-stu-id="9c333-152">Add the full path to the ngrok.exe file that you installed to the system PATH environment variable.</span></span> <span data-ttu-id="9c333-153">正確な手順は、使用しているシェルに固有です。</span><span class="sxs-lookup"><span data-stu-id="9c333-153">The exact steps are specific to the shell that you are using.</span></span>

1.  <span data-ttu-id="9c333-154">セットアップが完了したら、ターミナルを開いて実行します `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="9c333-154">After you have finished setting it up, open a terminal and run `ngrok http -host-header=rewrite 3978`.</span></span> 

    <span data-ttu-id="9c333-155">次に、ngrok はポート 3978 でローカル ホストに転送するパブリックで安全な URL を提供します。Teams では HTTPS 接続が必要なので、次のスクリーンショットに示すように HTTPS URL をコピーします `https://287a4f4223bc.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="9c333-155">Now ngrok provides you a public, secure URL that forwards to your localhost at port 3978, so copy the HTTPS URL, for example, `https://287a4f4223bc.ngrok.io` as shown in the screenshot below, since Teams requires HTTPS connections:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="ngrok を使用した localhost のトンネリングを示すスクリーンショット。":::

1. <span data-ttu-id="9c333-157">アプリ マニフェストに URL を登録します。</span><span class="sxs-lookup"><span data-stu-id="9c333-157">Register the URL in your app manifest.</span></span> 

## <a name="4-register-your-bot-endpoint"></a><span data-ttu-id="9c333-158">4. ボット エンドポイントを登録する</span><span class="sxs-lookup"><span data-stu-id="9c333-158">4. Register your bot endpoint</span></span>

<span data-ttu-id="9c333-159">Teams でボットを使用するには、Azure Bot Service にボットを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c333-159">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="9c333-160">これは、Teams アプリケーションを使用してアプリをセットアップするときに自動的にToolkit。</span><span class="sxs-lookup"><span data-stu-id="9c333-160">This is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="9c333-161">引き続き、ボットに送信されるユーザー メッセージ (要求) を受信および処理するエンドポイント アドレスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9c333-161">You must still specify an endpoint address to receive and process user messages, or requests, sent to the bot.</span></span> <span data-ttu-id="9c333-162">通常、URL は次のように表示されます `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="9c333-162">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="9c333-163">この設定はツールキットですばやく構成できます。</span><span class="sxs-lookup"><span data-stu-id="9c333-163">You can configure this quickly in the toolkit.</span></span>

1. <span data-ttu-id="9c333-164">[Visual Studioコード] で **、[Microsoft Teams] を開Toolkit。**</span><span class="sxs-lookup"><span data-stu-id="9c333-164">In Visual Studio Code, open **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="9c333-165">[**ボット]**  >  **[既存のボット登録] を選択し**、セットアップ時に作成したボットを選択します。</span><span class="sxs-lookup"><span data-stu-id="9c333-165">Select **Bots** > **Existing bot registrations** and select the bot you created during setup.</span></span> 
1. <span data-ttu-id="9c333-166">[ **ボット エンドポイント アドレス** ] フィールドに、ボットをホストしている ngrok URL を入力し、その URL `https://287a4f4223bc.ngrok.io` に `/api/messages` 追加します。</span><span class="sxs-lookup"><span data-stu-id="9c333-166">In the **Bot endpoint address** field, enter the ngrok URL, for example, `https://287a4f4223bc.ngrok.io`, where you're hosting the bot and append `/api/messages` to it:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="ngrok を使用して localhost をトンネリングする方法を示すスクリーンショット。":::

    <span data-ttu-id="9c333-168">エンドポイントを正しくセットアップした後、ボットは Teams のメッセージに応答できます。</span><span class="sxs-lookup"><span data-stu-id="9c333-168">Your bot will be able to respond to messages in Teams, after you set up the endpoint correctly.</span></span> 

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="9c333-169">5. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="9c333-169">5. Build and run your app</span></span>

<span data-ttu-id="9c333-170">ボットをホストする URL を設定し、メッセージを処理するように構成しました。</span><span class="sxs-lookup"><span data-stu-id="9c333-170">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="9c333-171">アプリを起動して実行する時間です。</span><span class="sxs-lookup"><span data-stu-id="9c333-171">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="9c333-172">ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、`npm install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="9c333-172">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="9c333-173">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="9c333-173">Run `npm start`.</span></span>

   <span data-ttu-id="9c333-174">成功した場合は、ボットがアクティビティをリッスン中であることを示す次のメッセージが表示されます `localhost` 。</span><span class="sxs-lookup"><span data-stu-id="9c333-174">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="9c333-175">6. Teams でボットをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="9c333-175">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="9c333-176">ボットを実行すると、Teams にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="9c333-176">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="9c333-177">以前に Teams アプリをサイドロードし、問題が発生していない場合は、次の手順に [従います](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="9c333-177">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="9c333-178">[Visual Studioコード] で **、F5** キーを選択して Teams Web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="9c333-178">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="9c333-179">[アプリのインストール] ダイアログで、[追加] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="9c333-179">In the app install dialog, select **Add for me**.</span></span> 

   > [!Note]
   > <span data-ttu-id="9c333-180">既定では、アプリは 1:1 ダイレクト チャット メッセージに追加されます。ただし、[追加] の横にある小さな矢印をクリックして、チームまたはチャットにインストール **することもできます。**</span><span class="sxs-lookup"><span data-stu-id="9c333-180">By default, the app is added to your 1:1 direct chat message, however you can choose to install it to a team or chat by clicking the little arrow beside **Add for me**.</span></span> <span data-ttu-id="9c333-181">このチュートリアルでは、[追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="9c333-181">In this tutorial, let’s just click Add.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="ngrok を使用したローカル ホストのトンネリングを示すスクリーンショット。":::

## <a name="7-test-your-bot"></a><span data-ttu-id="9c333-183">7. ボットをテストする</span><span class="sxs-lookup"><span data-stu-id="9c333-183">7. Test your bot</span></span>

<span data-ttu-id="9c333-184">ボットに "Hello" と言います。</span><span class="sxs-lookup"><span data-stu-id="9c333-184">Let's say "Hello" to your bot.</span></span>

* <span data-ttu-id="9c333-185">作成ボックスで、メッセージを送信 `Hello` します。</span><span class="sxs-lookup"><span data-stu-id="9c333-185">In the compose box, send a `Hello` message.</span></span>
    <span data-ttu-id="9c333-186">ボットは次のようなメッセージで返信します。</span><span class="sxs-lookup"><span data-stu-id="9c333-186">Your bot replies with something like the following message:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="ユーザーが Teams ボットに 「Hello」 と答え、応答を取得するスクリーンショット。":::

    <span data-ttu-id="9c333-188">これで、ユーザーと 1 対 1 またはグループ設定 (チャネルとチャット) で通信できる基本的な Teams ボットを作成🎉</span><span class="sxs-lookup"><span data-stu-id="9c333-188">You have now created a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats) 🎉</span></span>

## <a name="troubleshoot-your-bot"></a><span data-ttu-id="9c333-189">ボットのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="9c333-189">Troubleshoot your bot</span></span>

<span data-ttu-id="9c333-190">このチュートリアルの完了に問題がある場合は、次の情報が役立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="9c333-190">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="9c333-191">ボットが Teams に接続されていない</span><span class="sxs-lookup"><span data-stu-id="9c333-191">Bot isn't connected to Teams</span></span>


<span data-ttu-id="9c333-192">アプリをインストールしたがボットが機能しない場合は、ボットが Azure Bot Service の Teams チャネルに接続 [されていることを確認 *します*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="9c333-192">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="9c333-193">これは Teams のチャネルと同じではないと理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="9c333-193">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="9c333-194">この場合、チャネルとは、Azure Bot Service がボットを Teams または別のサポートされている Microsoft またはサード パーティの通信アプリに接続 [する方法です](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="9c333-194">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="9c333-195">関連項目</span><span class="sxs-lookup"><span data-stu-id="9c333-195">See also</span></span>

* [<span data-ttu-id="9c333-196">ボットの基本</span><span class="sxs-lookup"><span data-stu-id="9c333-196">Bot basics</span></span>](../bots/bot-basics.md)
* [<span data-ttu-id="9c333-197">Microsoft Teams の個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="9c333-197">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
* [<span data-ttu-id="9c333-198">Teams ボットがサンプルの 1 つで実行できるその他の操作を参照する</span><span class="sxs-lookup"><span data-stu-id="9c333-198">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="9c333-199">ボット会話の基本</span><span class="sxs-lookup"><span data-stu-id="9c333-199">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="9c333-200">デザインのガイドライン</span><span class="sxs-lookup"><span data-stu-id="9c333-200">Design guidelines</span></span>](../bots/design/bots.md) 
* [<span data-ttu-id="9c333-201">実稼働対応の UI テンプレート</span><span class="sxs-lookup"><span data-stu-id="9c333-201">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md)
* [<span data-ttu-id="9c333-202">Teams でのボット認証</span><span class="sxs-lookup"><span data-stu-id="9c333-202">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="9c333-203">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="9c333-203">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="9c333-204">ツールキットなしでボットを作成する</span><span class="sxs-lookup"><span data-stu-id="9c333-204">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a><span data-ttu-id="9c333-205">次の手順</span><span class="sxs-lookup"><span data-stu-id="9c333-205">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9c333-206">メッセージングの拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="9c333-206">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
