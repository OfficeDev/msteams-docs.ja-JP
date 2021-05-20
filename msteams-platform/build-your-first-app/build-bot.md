---
title: はじめに - ボットを構築する
author: girliemac
description: Microsoft Teams Toolkitを使用して、Microsoft Teamsボットをすばやく作成します。
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: 2cbd90b293e8ac8343febc7b3d23278d5bb5bf82
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565887"
---
# <a name="create-your-first-bot-for-teams"></a><span data-ttu-id="2fbca-103">Teams用の最初のボットを作成する</span><span class="sxs-lookup"><span data-stu-id="2fbca-103">Create your first bot for Teams</span></span>

<span data-ttu-id="2fbca-104">このチュートリアルでは、基本的なボット アプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-104">This tutorial teaches you to build a basic bot app.</span></span> <span data-ttu-id="2fbca-105">ボットは、Teamsユーザーと、会話型インターフェイスを使用して Web アプリまたはサービスの間の仲介役を果たし、</span><span class="sxs-lookup"><span data-stu-id="2fbca-105">A bot acts as an intermediary between Teams users and your web app or service with a conversational interface.</span></span> <span data-ttu-id="2fbca-106">ボットとチャットすることで、サービスで実行される情報をすばやく取得したり、ワークフローやタスクを開始したりできます。</span><span class="sxs-lookup"><span data-stu-id="2fbca-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="2fbca-107">あなたが学ぶこと</span><span class="sxs-lookup"><span data-stu-id="2fbca-107">What you'll learn</span></span>

* <span data-ttu-id="2fbca-108">Visual Studio CodeのMicrosoft Teams Toolkitを使用して、アプリ プロジェクトとボットを作成します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-108">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="2fbca-109">ボットに関連するTeamsアプリの構成を理解する。</span><span class="sxs-lookup"><span data-stu-id="2fbca-109">Understand the Teams app configurations relevant to bots.</span></span>
* <span data-ttu-id="2fbca-110">ローカル ホスト トンネリング ソリューションを使用して、ローカルでアプリをホストして実行します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-110">Host and run an app locally using a localhost tunneling solution.</span></span>
* <span data-ttu-id="2fbca-111">Teamsでボットをサイドロードしてテストします。</span><span class="sxs-lookup"><span data-stu-id="2fbca-111">Sideload and test a bot in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fbca-112">前提条件</span><span class="sxs-lookup"><span data-stu-id="2fbca-112">Prerequisites</span></span>

<span data-ttu-id="2fbca-113">簡単なTeams アプリを設定して構築する方法を理解していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-113">Ensure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="2fbca-114">詳細については、[最初のMicrosoft Teams "Hello, World!" アプリを作成する](../build-your-first-app/build-and-run.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2fbca-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span> 

## <a name="1-create-your-app-project"></a><span data-ttu-id="2fbca-115">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="2fbca-115">1. Create your app project</span></span>

<span data-ttu-id="2fbca-116">Microsoft Teams Toolkitは、アプリの次のコンポーネントを設定するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2fbca-116">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span> 

* <span data-ttu-id="2fbca-117">ボット **に関連するアプリの構成とスキャフォールディング**。</span><span class="sxs-lookup"><span data-stu-id="2fbca-117">**App configurations and scaffolding** relevant to bots.</span></span>
* <span data-ttu-id="2fbca-118">**Microsoft Azure ボット** サービスに自動的に登録されるボット。</span><span class="sxs-lookup"><span data-stu-id="2fbca-118">**Bot** that's automatically registered with the Microsoft Azure Bot Service.</span></span>

<span data-ttu-id="2fbca-119">**アプリ プロジェクトを作成するには**</span><span class="sxs-lookup"><span data-stu-id="2fbca-119">**To create your app project**</span></span>

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="Teams Toolkitでアプリを作成する方法を示すスクリーンショット。":::

1. <span data-ttu-id="2fbca-122">メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="2fbca-122">When prompted, sign in with your Microsoft 365 development account.</span></span> 
1. <span data-ttu-id="2fbca-123">[プロジェクトの選択] 画面で、[会話ボット] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-123">On the Select project screen, select Conversation bots:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Teams Toolkitで新しいボットを作成する方法を示すスクリーンショット。":::

1. <span data-ttu-id="2fbca-125">[ **プロジェクトの構成]** 画面で、ボットの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-125">On the **Configure project** screen, enter a name for your bot.</span></span> <span data-ttu-id="2fbca-126">これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前でもあります。</span><span class="sxs-lookup"><span data-stu-id="2fbca-126">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="2fbca-127">次の図に示すように、[**新しい**  >  **ボット作成ボット登録の作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-127">Select **Create a new Bot** > **Create Bot Registration** as shown in the following image:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Teams Toolkitで新しいボットの名前を付けるスクリーンショット。":::

    <span data-ttu-id="2fbca-129">成功した場合、新しいボットは **登録済み** ステータスになります。</span><span class="sxs-lookup"><span data-stu-id="2fbca-129">If successful, your new bot will have a **Registered** status.</span></span> <span data-ttu-id="2fbca-130">これで、ボットが Microsoft Azure Bot サービスに自動的に登録されます。</span><span class="sxs-lookup"><span data-stu-id="2fbca-130">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Teams Toolkitでの新しいボットの登録を示すスクリーンショット。":::

1. <span data-ttu-id="2fbca-132">画面の下部にある **[完了] を** 選択し、プロジェクトをコンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-132">Select **Finish** at the bottom of the screen and save your project on your machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="2fbca-133">2. アプリ プロジェクト コンポーネントを理解する</span><span class="sxs-lookup"><span data-stu-id="2fbca-133">2. Understand your app project components</span></span>

<span data-ttu-id="2fbca-134">アプリの構成とスキャフォールディングの多くは、Teams Toolkitを使用してプロジェクトを作成するときに自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="2fbca-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="2fbca-135">ボットを構築するための主なコンポーネントを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="2fbca-135">Let's look at the main components for building a bot:</span></span>

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Teams Toolkit内のプロジェクト スキャフォールディングを示すスクリーンショット。":::

<span data-ttu-id="2fbca-137">別のチュートリアルでタブを作成した場合、ボットのアプリスキャフォールディングは異なります。</span><span class="sxs-lookup"><span data-stu-id="2fbca-137">If you created a tab in another tutorial, the app scaffolding for the bot is different.</span></span> <span data-ttu-id="2fbca-138">タブとは異なり、ボット開発では、フロントエンド Web コンポーネントを構築したり、JavaScript クライアント SDK Teamsを使用したりする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="2fbca-138">Unlike tabs, bot development doesn't require you to build any front-end web components or use the Teams JavaScript client SDK.</span></span>  <span data-ttu-id="2fbca-139">代わりに、スキャフォールディングは、ウェブ、モバイル、そしてもちろんTeamsで動作できるインテリジェントなエンタープライズグレードのボットを構築するためのオープンソースSDKである[Microsoft Bot Framework](https://dev.botframework.com/)を使用します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-139">Instead, the scaffolding uses the [Microsoft Bot Framework](https://dev.botframework.com/), which is an open-source SDK for building intelligent, enterprise-grade bots that can work on the web, mobile, and of course Teams!</span></span> 

<span data-ttu-id="2fbca-140">`botActivityHandler.js`プロジェクトのルート ディレクトリにあるファイルは、特定のメッセージに対するボットの応答など、ボットアクティビティを処理するTeams固有のハンドラーです。</span><span class="sxs-lookup"><span data-stu-id="2fbca-140">The `botActivityHandler.js` file, located in the root directory of your project, is the Teams-specific handler that handles bot activities, such as how the bot responds to specific messages.</span></span> <span data-ttu-id="2fbca-141">アプリのスキャフォールディングは `botActivityHandler.js` 、プロジェクトのルート ディレクトリにあるファイルを提供する、特定のメッセージに対するボットの応答などのボット アクティビティを処理するTeams固有のハンドラーです。</span><span class="sxs-lookup"><span data-stu-id="2fbca-141">The app scaffolding provides a `botActivityHandler.js` file located in the root directory of your project, is the Teams specific handler that handles bot activities such as how the bot responds to specific messages.</span></span>

## <a name="3-securely-expose-your-localhost-to-the-internet"></a><span data-ttu-id="2fbca-142">3. ローカルホストをインターネットに安全に公開する</span><span class="sxs-lookup"><span data-stu-id="2fbca-142">3. Securely expose your localhost to the internet</span></span>

<span data-ttu-id="2fbca-143">`index.js`HTTP サーバーを作成し、ボットへの着信要求をリッスンするルーティングを処理するファイルを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="2fbca-143">Take a look at the `index.js` file, which creates an HTTP server and handles routing to listen for incoming requests to your bot.</span></span> <span data-ttu-id="2fbca-144">`/api/messages`は、クライアント要求に応答するためのアプリのエンドポイント URL です。</span><span class="sxs-lookup"><span data-stu-id="2fbca-144">The `/api/messages` is your app's endpoint URL to respond to client requests:</span></span> 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

<span data-ttu-id="2fbca-145">リクエストをボットのロジックに転送するには、 の代わりに、 など、パブリックにアクセスできる URL を設定する必要があります `https://example.com/api/messages` `https://localhost` 。</span><span class="sxs-lookup"><span data-stu-id="2fbca-145">To forward the requests to your bot's logic, you must set up a publicly accessible URL, such as `https://example.com/api/messages`, instead of `https://localhost`.</span></span> <span data-ttu-id="2fbca-146">アプリは現在ローカルホストから実行されているため、ネットワークを *トンネル* する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fbca-146">Because your app is running from your localhost currently, you must *tunnel* the network.</span></span>

<span data-ttu-id="2fbca-147">トンネリングは、ネットワークを介してデータを転送できるようにするプロトコルです。</span><span class="sxs-lookup"><span data-stu-id="2fbca-147">Tunneling is a protocol that allows you to transport data across a network.</span></span> <span data-ttu-id="2fbca-148">ローカルホストトンネリングを使用すると、ローカルマシンとリモート接続の間の接続が提供されます。</span><span class="sxs-lookup"><span data-stu-id="2fbca-148">And localhost tunneling gives you a connection between your local machine and a remote connection.</span></span> <span data-ttu-id="2fbca-149">ローカルホストをインターネットに安全に公開するには **、ngrok** というサードパーティ製ツールを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2fbca-149">To securely expose your localhost to the internet, we recommend you to use the 3rd party tool called, **ngrok**.</span></span> <span data-ttu-id="2fbca-150">これにより、安全な URL が提供されます。</span><span class="sxs-lookup"><span data-stu-id="2fbca-150">This will give you a secure URL.</span></span> 

1. <span data-ttu-id="2fbca-151">[ngrok.com](https://ngrok.com/download)サイトにアクセスし、指示に従って、ご使用の環境にngrokをインストールして設定します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-151">Go to the [ngrok.com](https://ngrok.com/download) site and follow the instruction to install and set up ngrok in your environment.</span></span> 
    
    <span data-ttu-id="2fbca-152">システム PATH 環境変数にインストールしたngrok.exe ファイルへの完全パスを追加します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-152">Add the full path to the ngrok.exe file that you installed to the system PATH environment variable.</span></span> <span data-ttu-id="2fbca-153">正確な手順は、使用しているシェルに固有のものです。</span><span class="sxs-lookup"><span data-stu-id="2fbca-153">The exact steps are specific to the shell that you are using.</span></span>

1.  <span data-ttu-id="2fbca-154">設定が完了したら、ターミナルを開いて `ngrok http -host-header=rewrite 3978` を実行します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-154">After you have finished setting it up, open a terminal and run `ngrok http -host-header=rewrite 3978`.</span></span> 

    <span data-ttu-id="2fbca-155">ngrok は、ポート 3978 でローカルホストに転送するパブリックで安全な URL を提供します `https://287a4f4223bc.ngrok.io` Teams。</span><span class="sxs-lookup"><span data-stu-id="2fbca-155">Now ngrok provides you a public, secure URL that forwards to your localhost at port 3978, so copy the HTTPS URL, for example, `https://287a4f4223bc.ngrok.io` as shown in the screenshot below, since Teams requires HTTPS connections:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="ngrok を使用したローカルホストのトンネリングを示すスクリーンショット。":::

1. <span data-ttu-id="2fbca-157">アプリ マニフェストに URL を登録します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-157">Register the URL in your app manifest.</span></span> 

## <a name="4-register-your-bot-endpoint"></a><span data-ttu-id="2fbca-158">4. ボットエンドポイントを登録する</span><span class="sxs-lookup"><span data-stu-id="2fbca-158">4. Register your bot endpoint</span></span>

<span data-ttu-id="2fbca-159">Teamsでボットを使用するには、Azure Bot サービスに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fbca-159">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="2fbca-160">これは、Teams Toolkitを使用してアプリを設定すると自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="2fbca-160">This is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="2fbca-161">ユーザー メッセージ、またはボットに送信される要求を受信および処理するエンドポイント アドレスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2fbca-161">You must still specify an endpoint address to receive and process user messages, or requests sent to the bot.</span></span> <span data-ttu-id="2fbca-162">通常、URL は `https://HOST_URL/api/messages` のようになります。</span><span class="sxs-lookup"><span data-stu-id="2fbca-162">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="2fbca-163">これは、ツールキットで構成できます。</span><span class="sxs-lookup"><span data-stu-id="2fbca-163">You can configure this in the toolkit.</span></span>

1. <span data-ttu-id="2fbca-164">Visual Studio Codeで、 **Microsoft Teams Toolkit** を開きます。</span><span class="sxs-lookup"><span data-stu-id="2fbca-164">In Visual Studio Code, open **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="2fbca-165">[**ボット**  >  **] 既存のボット登録を** 選択し、セットアップ中に作成したボットを選択します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-165">Select **Bots** > **Existing bot registrations** and select the bot you created during setup.</span></span> 
1. <span data-ttu-id="2fbca-166">[ **ボット エンドポイント アドレス]** フィールドに、たとえば、ボットをホストしている ngrok URL `https://287a4f4223bc.ngrok.io` を入力し、その URL に追加 `/api/messages` します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-166">In the **Bot endpoint address** field, enter the ngrok URL, for example, `https://287a4f4223bc.ngrok.io`, where you're hosting the bot and append `/api/messages` to it:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="ngrok でローカルホストをトンネルする方法を示すスクリーンショット。":::

    <span data-ttu-id="2fbca-168">エンドポイントを正しく設定すると、ボットはTeamsのメッセージに応答できるようになります。</span><span class="sxs-lookup"><span data-stu-id="2fbca-168">Your bot will be able to respond to messages in Teams, after you set up the endpoint correctly.</span></span> 

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="2fbca-169">5. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="2fbca-169">5. Build and run your app</span></span>

<span data-ttu-id="2fbca-170">ボットをホストする URL を設定し、メッセージを処理するように設定しました。</span><span class="sxs-lookup"><span data-stu-id="2fbca-170">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="2fbca-171">アプリを起動して実行する時間です。</span><span class="sxs-lookup"><span data-stu-id="2fbca-171">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="2fbca-172">ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、`npm install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-172">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="2fbca-173">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-173">Run `npm start`.</span></span>

   <span data-ttu-id="2fbca-174">成功した場合は、ボットがでアクティビティをリッスンしている、という次のメッセージが表示されます `localhost` 。</span><span class="sxs-lookup"><span data-stu-id="2fbca-174">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="2fbca-175">6. Teamsでボットをサイドロードする</span><span class="sxs-lookup"><span data-stu-id="2fbca-175">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="2fbca-176">ボットを実行すると、Teamsにインストールできます。</span><span class="sxs-lookup"><span data-stu-id="2fbca-176">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="2fbca-177">Teamsアプリを以前にサイドロードし、問題が発生していない場合は、次の[手順](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)に従ってください。</span><span class="sxs-lookup"><span data-stu-id="2fbca-177">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="2fbca-178">Visual Studio Codeで **、F5** キーを選択して、Teams Web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-178">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="2fbca-179">[アプリのインストール] ダイアログで、[ **追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-179">In the app install dialog, select **Add for me**.</span></span> 

   > [!Note]
   > <span data-ttu-id="2fbca-180">既定では、アプリは 1:1 のダイレクト チャット メッセージに追加されていますが、チームにインストールするか、または [ **自分のために追加**] の横にある小さな矢印をクリックしてチャットをインストールするかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="2fbca-180">By default, the app is added to your 1:1 direct chat message, however you can choose to install it to a team or chat by clicking the little arrow beside **Add for me**.</span></span> <span data-ttu-id="2fbca-181">このチュートリアルでは、[追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2fbca-181">In this tutorial, let’s just click Add.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="ngrok でローカル ホストをトンネリングするスクリーンショット。":::

## <a name="7-test-your-bot"></a><span data-ttu-id="2fbca-183">7. ボットをテストする</span><span class="sxs-lookup"><span data-stu-id="2fbca-183">7. Test your bot</span></span>

<span data-ttu-id="2fbca-184">ボットに「こんにちは」と言いましょう。</span><span class="sxs-lookup"><span data-stu-id="2fbca-184">Let's say "Hello" to your bot.</span></span>

* <span data-ttu-id="2fbca-185">作成ボックスで、メッセージを送信 `Hello` します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-185">In the compose box, send a `Hello` message.</span></span>
    <span data-ttu-id="2fbca-186">ボットは次のようなメッセージで返信します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-186">Your bot replies with something like the following message:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="ユーザーがボットに「こんにちは」と答えてTeamsを示すスクリーンショット。":::

    <span data-ttu-id="2fbca-188">これで、ユーザーと 1 対 1 またはグループ設定 (チャネルとチャット) 🎉と通信できる基本的なTeamsボットが作成されました。</span><span class="sxs-lookup"><span data-stu-id="2fbca-188">You have now created a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats) 🎉.</span></span>

## <a name="troubleshoot-your-bot"></a><span data-ttu-id="2fbca-189">ボットのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="2fbca-189">Troubleshoot your bot</span></span>

<span data-ttu-id="2fbca-190">このチュートリアルを完了する際に問題が発生した場合は、次の情報が役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2fbca-190">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="2fbca-191">ボットがTeamsに接続されていない</span><span class="sxs-lookup"><span data-stu-id="2fbca-191">Bot isn't connected to Teams</span></span>


<span data-ttu-id="2fbca-192">アプリをインストールしてもボットが機能していない場合は、ボットが Azure Bot [サービスのTeams *チャネル* に接続](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="2fbca-192">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="2fbca-193">これはTeamsのチャンネルと同じではないことを理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="2fbca-193">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="2fbca-194">この場合、チャネルとは、Azure Bot サービスがボットをTeamsまたは[サポートされている別の Microsoft またはサードパーティの通信アプリ](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)に接続する方法です。</span><span class="sxs-lookup"><span data-stu-id="2fbca-194">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="2fbca-195">関連項目</span><span class="sxs-lookup"><span data-stu-id="2fbca-195">See also</span></span>

* [<span data-ttu-id="2fbca-196">ボットの基本</span><span class="sxs-lookup"><span data-stu-id="2fbca-196">Bot basics</span></span>](../bots/bot-basics.md)
* [<span data-ttu-id="2fbca-197">Microsoft Teams用の個人用タブを作成する</span><span class="sxs-lookup"><span data-stu-id="2fbca-197">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
* [<span data-ttu-id="2fbca-198">Teamsのサンプルで他に何ができるのかを確認する</span><span class="sxs-lookup"><span data-stu-id="2fbca-198">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="2fbca-199">ボット会話の基本</span><span class="sxs-lookup"><span data-stu-id="2fbca-199">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="2fbca-200">デザインのガイドライン</span><span class="sxs-lookup"><span data-stu-id="2fbca-200">Design guidelines</span></span>](../bots/design/bots.md) 
* [<span data-ttu-id="2fbca-201">プロダクション対応の UI テンプレート</span><span class="sxs-lookup"><span data-stu-id="2fbca-201">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md)
* [<span data-ttu-id="2fbca-202">Teamsでのボット認証</span><span class="sxs-lookup"><span data-stu-id="2fbca-202">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="2fbca-203">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="2fbca-203">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="2fbca-204">ツールキットを使用せずにボットを作成する</span><span class="sxs-lookup"><span data-stu-id="2fbca-204">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a><span data-ttu-id="2fbca-205">次の手順</span><span class="sxs-lookup"><span data-stu-id="2fbca-205">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2fbca-206">メッセージングの拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="2fbca-206">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
