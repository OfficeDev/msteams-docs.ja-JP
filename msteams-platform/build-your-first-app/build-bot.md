---
title: '[スタート] - ボットを作成する'
author: girliemac
description: アプリを使用してMicrosoft Teamsボットをすばやく作成Microsoft Teams Toolkit。
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: d54766d739ceaf585ab4a1e026f4a6e1150e3a2e
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630979"
---
# <a name="create-your-first-bot-for-teams"></a><span data-ttu-id="57166-103">ユーザーの最初のボットを作成Teams</span><span class="sxs-lookup"><span data-stu-id="57166-103">Create your first bot for Teams</span></span>

<span data-ttu-id="57166-104">このチュートリアルでは、基本的なボット アプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="57166-104">This tutorial teaches you to build a basic bot app.</span></span> <span data-ttu-id="57166-105">ボットは、会話型インターフェイスを使用Teamsユーザーと Web アプリまたはサービスの間の仲介者として機能します。</span><span class="sxs-lookup"><span data-stu-id="57166-105">A bot acts as an intermediary between Teams users and your web app or service with a conversational interface.</span></span> <span data-ttu-id="57166-106">ユーザーはボットとチャットして、情報をすばやく取得したり、サービスによって実行されるワークフローやタスクを開始できます。</span><span class="sxs-lookup"><span data-stu-id="57166-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="57166-107">学習する情報</span><span class="sxs-lookup"><span data-stu-id="57166-107">What you'll learn</span></span>

* <span data-ttu-id="57166-108">アプリ プロジェクトとボットを作成するには、アプリ のMicrosoft Teams ToolkitをVisual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="57166-108">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="57166-109">ボットにTeamsするアプリ構成の説明について説明します。</span><span class="sxs-lookup"><span data-stu-id="57166-109">Understand the Teams app configurations relevant to bots.</span></span>
* <span data-ttu-id="57166-110">ローカル ホスト トンネリング ソリューションを使用してアプリをローカルでホストして実行します。</span><span class="sxs-lookup"><span data-stu-id="57166-110">Host and run an app locally using a localhost tunneling solution.</span></span>
* <span data-ttu-id="57166-111">アプリでボットをサイドロードしてテストTeams。</span><span class="sxs-lookup"><span data-stu-id="57166-111">Sideload and test a bot in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57166-112">前提条件</span><span class="sxs-lookup"><span data-stu-id="57166-112">Prerequisites</span></span>

<span data-ttu-id="57166-113">簡単なアプリをセットアップしてビルドする方法を理解Teamsしてください。</span><span class="sxs-lookup"><span data-stu-id="57166-113">Ensure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="57166-114">詳細については[、「Hello, World!」アプリMicrosoft Teamsを作成するを参照してください](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="57166-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span> 

## <a name="1-create-your-app-project"></a><span data-ttu-id="57166-115">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="57166-115">1. Create your app project</span></span>

<span data-ttu-id="57166-116">このMicrosoft Teams Toolkitは、アプリに対して次のコンポーネントをセットアップするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="57166-116">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span> 

* <span data-ttu-id="57166-117">**ボットに関連するアプリの構成** とスキャフォールディング。</span><span class="sxs-lookup"><span data-stu-id="57166-117">**App configurations and scaffolding** relevant to bots.</span></span>
* <span data-ttu-id="57166-118">**ボット** サービスに自動的に登録Microsoft Azureボット。</span><span class="sxs-lookup"><span data-stu-id="57166-118">**Bot** that's automatically registered with the Microsoft Azure Bot Service.</span></span>

<span data-ttu-id="57166-119">**アプリ プロジェクトを作成するには**</span><span class="sxs-lookup"><span data-stu-id="57166-119">**To create your app project**</span></span>

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="アプリをアプリで作成する方法を示すTeams Toolkit。":::

1. <span data-ttu-id="57166-122">メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="57166-122">When prompted, sign in with your Microsoft 365 development account.</span></span> 
1. <span data-ttu-id="57166-123">[プロジェクトの選択] 画面で、[会話ボット] を選択します。</span><span class="sxs-lookup"><span data-stu-id="57166-123">On the Select project screen, select Conversation bots:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="新しいボットを作成する方法を示すスクリーンショットをTeams Toolkit。":::

1. <span data-ttu-id="57166-125">[プロジェクトの **構成] 画面** で、ボットの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="57166-125">On the **Configure project** screen, enter a name for your bot.</span></span> <span data-ttu-id="57166-126">これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です。</span><span class="sxs-lookup"><span data-stu-id="57166-126">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="57166-127">次 **の図に示すように、[ボット**  >  **登録の** 作成] を選択します。</span><span class="sxs-lookup"><span data-stu-id="57166-127">Select **Create a new Bot** > **Create Bot Registration** as shown in the following image:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="新しいボットに名前を付ける方法を示すスクリーンショットをTeams Toolkit。":::

    <span data-ttu-id="57166-129">成功した場合、新しいボットの状態は **[** 登録済み] になります。</span><span class="sxs-lookup"><span data-stu-id="57166-129">If successful, your new bot will have a **Registered** status.</span></span> <span data-ttu-id="57166-130">これで、ボットは自動的にボット サービスMicrosoft Azure登録されます。</span><span class="sxs-lookup"><span data-stu-id="57166-130">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="新しいボットの登録を示すスクリーンショットをTeams Toolkit。":::

1. <span data-ttu-id="57166-132">画面 **の下部** にある [完了] を選択し、プロジェクトをコンピューターに保存します。</span><span class="sxs-lookup"><span data-stu-id="57166-132">Select **Finish** at the bottom of the screen and save your project on your machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="57166-133">2. アプリ プロジェクト コンポーネントについて</span><span class="sxs-lookup"><span data-stu-id="57166-133">2. Understand your app project components</span></span>

<span data-ttu-id="57166-134">アプリの構成とスキャフォールディングの多くが、プロジェクトを作成するときに自動的に設定Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="57166-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="57166-135">ボットを構築する主なコンポーネントを見てみ取る:</span><span class="sxs-lookup"><span data-stu-id="57166-135">Let's look at the main components for building a bot:</span></span>

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="プロジェクトのスキャフォールディングを示すスクリーンショットをTeams Toolkit。":::

<span data-ttu-id="57166-137">別のチュートリアルでタブを作成した場合、ボットのアプリスキャフォールディングは異なります。</span><span class="sxs-lookup"><span data-stu-id="57166-137">If you created a tab in another tutorial, the app scaffolding for the bot is different.</span></span> <span data-ttu-id="57166-138">タブとは異なり、ボットの開発では、フロントエンド Web コンポーネントをビルドしたり、JavaScript クライアント SDK のTeams必要としたりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="57166-138">Unlike tabs, bot development doesn't require you to build any front-end web components or use the Teams JavaScript client SDK.</span></span>  <span data-ttu-id="57166-139">代わりに、スキャフォールディングは[Microsoft Bot Framework](https://dev.botframework.com/)を使用します。これは、Web、モバイル、およびもちろんモバイルで動作するインテリジェントなエンタープライズ レベルのボットを構築するオープンソース SDK Teams です。</span><span class="sxs-lookup"><span data-stu-id="57166-139">Instead, the scaffolding uses the [Microsoft Bot Framework](https://dev.botframework.com/), which is an open-source SDK for building intelligent, enterprise-grade bots that can work on the web, mobile, and of course Teams!</span></span> 

<span data-ttu-id="57166-140">アプリのスキャフォールディングは、プロジェクトのルート ディレクトリにあるファイルを提供し、ボットが特定のメッセージに応答する方法などのボット アクティビティを処理する Teams 固有のハンドラーです `botActivityHandler.js` 。</span><span class="sxs-lookup"><span data-stu-id="57166-140">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, is the Teams-specific handler that handles bot activities such as, how the bot responds to specific messages.</span></span>

## <a name="3-securely-expose-your-localhost-to-the-internet"></a><span data-ttu-id="57166-141">3. localhost をインターネットに安全に公開する</span><span class="sxs-lookup"><span data-stu-id="57166-141">3. Securely expose your localhost to the internet</span></span>

<span data-ttu-id="57166-142">HTTP サーバーを作成し、ボットへの受信要求をリッスンするルーティングを処理するファイル `index.js` を確認します。</span><span class="sxs-lookup"><span data-stu-id="57166-142">Take a look at the `index.js` file, which creates an HTTP server and handles routing to listen for incoming requests to your bot.</span></span> <span data-ttu-id="57166-143">クライアント `/api/messages` 要求に応答するアプリのエンドポイント URL を次に示します。</span><span class="sxs-lookup"><span data-stu-id="57166-143">The `/api/messages` is your app's endpoint URL to respond to client requests:</span></span> 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

<span data-ttu-id="57166-144">ボットのロジックに要求を転送するには、. `https://example.com/api/messages` `https://localhost`</span><span class="sxs-lookup"><span data-stu-id="57166-144">To forward the requests to your bot's logic, you must set up a publicly accessible URL, such as `https://example.com/api/messages`, instead of `https://localhost`.</span></span> <span data-ttu-id="57166-145">アプリは現在 localhost から実行されているので、ネットワークを *トンネリングする* 必要があります。</span><span class="sxs-lookup"><span data-stu-id="57166-145">Because your app is running from your localhost currently, you must *tunnel* the network.</span></span>

<span data-ttu-id="57166-146">トンネリングは、ネットワーク間でデータを転送できるプロトコルです。</span><span class="sxs-lookup"><span data-stu-id="57166-146">Tunneling is a protocol that allows you to transport data across a network.</span></span> <span data-ttu-id="57166-147">localhost トンネリングを使用すると、ローカル コンピューターとリモート接続間の接続が提供されます。</span><span class="sxs-lookup"><span data-stu-id="57166-147">And localhost tunneling gives you a connection between your local machine and a remote connection.</span></span> <span data-ttu-id="57166-148">localhost をインターネットに安全に公開するには **、ngrok** というサードパーティ製のツールを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="57166-148">To securely expose your localhost to the internet, we recommend you to use the 3rd party tool called, **ngrok**.</span></span> <span data-ttu-id="57166-149">これにより、セキュリティで保護された URL が提供されます。</span><span class="sxs-lookup"><span data-stu-id="57166-149">This will give you a secure URL.</span></span> 

1. <span data-ttu-id="57166-150">サイトに移動 [ngrok.com](https://ngrok.com/download) 指示に従って、環境に ngrok をインストールしてセットアップします。</span><span class="sxs-lookup"><span data-stu-id="57166-150">Go to the [ngrok.com](https://ngrok.com/download) site and follow the instruction to install and set up ngrok in your environment.</span></span> 
    
    <span data-ttu-id="57166-151">システム PATH 環境変数にインストールngrok.exeファイルへの完全パスを追加します。</span><span class="sxs-lookup"><span data-stu-id="57166-151">Add the full path to the ngrok.exe file that you installed to the system PATH environment variable.</span></span> <span data-ttu-id="57166-152">正確な手順は、使用しているシェルに固有です。</span><span class="sxs-lookup"><span data-stu-id="57166-152">The exact steps are specific to the shell that you are using.</span></span>

1.  <span data-ttu-id="57166-153">セットアップが完了したら、ターミナルを開いて実行します `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="57166-153">After you have finished setting it up, open a terminal and run `ngrok http -host-header=rewrite 3978`.</span></span> 

    <span data-ttu-id="57166-154">ngrok は、ポート 3978 でローカル ホストに転送するパブリックで安全な URL を提供します。そのため、次のスクリーンショットに示すように、https URL をコピーします。Teams では HTTPS 接続が必要です `https://287a4f4223bc.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="57166-154">Now ngrok provides you a public, secure URL that forwards to your localhost at port 3978, so copy the HTTPS URL, for example, `https://287a4f4223bc.ngrok.io` as shown in the screenshot below, since Teams requires HTTPS connections:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="ngrok を使用した localhost のトンネリングを示すスクリーンショット。":::

1. <span data-ttu-id="57166-156">アプリ マニフェストに URL を登録します。</span><span class="sxs-lookup"><span data-stu-id="57166-156">Register the URL in your app manifest.</span></span> 

## <a name="4-register-your-bot-endpoint"></a><span data-ttu-id="57166-157">4. ボット エンドポイントを登録する</span><span class="sxs-lookup"><span data-stu-id="57166-157">4. Register your bot endpoint</span></span>

<span data-ttu-id="57166-158">ボットを使用するには、Teams Azure Bot Service に登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="57166-158">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="57166-159">これは、アプリを使用してアプリをセットアップするときに自動的にTeams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="57166-159">This is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="57166-160">引き続き、ユーザー メッセージまたはボットに送信される要求を受信および処理するエンドポイント アドレスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="57166-160">You must still specify an endpoint address to receive and process user messages, or requests sent to the bot.</span></span> <span data-ttu-id="57166-161">通常、URL は次のように表示されます `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="57166-161">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="57166-162">これをツールキットで構成できます。</span><span class="sxs-lookup"><span data-stu-id="57166-162">You can configure this in the toolkit.</span></span>

1. <span data-ttu-id="57166-163">[Visual Studio Code]**を開** Microsoft Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="57166-163">In Visual Studio Code, open **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="57166-164">[**ボット]**  >  **[既存のボット登録] を選択し**、セットアップ時に作成したボットを選択します。</span><span class="sxs-lookup"><span data-stu-id="57166-164">Select **Bots** > **Existing bot registrations** and select the bot you created during setup.</span></span> 
1. <span data-ttu-id="57166-165">[ **ボット エンドポイント アドレス** ] フィールドに、ボットをホストしている ngrok URL を入力し、その URL `https://287a4f4223bc.ngrok.io` に `/api/messages` 追加します。</span><span class="sxs-lookup"><span data-stu-id="57166-165">In the **Bot endpoint address** field, enter the ngrok URL, for example, `https://287a4f4223bc.ngrok.io`, where you're hosting the bot and append `/api/messages` to it:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="ngrok を使用して localhost をトンネリングする方法を示すスクリーンショット。":::

    <span data-ttu-id="57166-167">エンドポイントを正しく設定した後、ボットは Teamsメッセージに応答できます。</span><span class="sxs-lookup"><span data-stu-id="57166-167">Your bot will be able to respond to messages in Teams, after you set up the endpoint correctly.</span></span> 

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="57166-168">5. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="57166-168">5. Build and run your app</span></span>

<span data-ttu-id="57166-169">ボットをホストする URL を設定し、メッセージを処理するように構成しました。</span><span class="sxs-lookup"><span data-stu-id="57166-169">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="57166-170">アプリを起動して実行する時間です。</span><span class="sxs-lookup"><span data-stu-id="57166-170">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="57166-171">ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、`npm install` を実行します。</span><span class="sxs-lookup"><span data-stu-id="57166-171">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="57166-172">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="57166-172">Run `npm start`.</span></span>

   <span data-ttu-id="57166-173">成功した場合は、ボットがアクティビティをリッスン中であることを示す次のメッセージが表示されます `localhost` 。</span><span class="sxs-lookup"><span data-stu-id="57166-173">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="57166-174">6. ボットをサイドロードTeams</span><span class="sxs-lookup"><span data-stu-id="57166-174">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="57166-175">ボットを実行している場合は、ボットをインストールTeams。</span><span class="sxs-lookup"><span data-stu-id="57166-175">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="57166-176">以前にアプリをサイドロードTeams問題が発生していない場合は、次の手順に[従います](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="57166-176">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="57166-177">[Visual Studio Code **F5** キーを選択して、Web クライアントTeams起動します。</span><span class="sxs-lookup"><span data-stu-id="57166-177">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="57166-178">[アプリのインストール] ダイアログで、[追加] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="57166-178">In the app install dialog, select **Add for me**.</span></span> 

   > [!Note]
   > <span data-ttu-id="57166-179">既定では、アプリは 1:1 ダイレクト チャット メッセージに追加されます。ただし、[追加] の横にある小さな矢印をクリックして、チームまたはチャットにインストール **することもできます。**</span><span class="sxs-lookup"><span data-stu-id="57166-179">By default, the app is added to your 1:1 direct chat message, however you can choose to install it to a team or chat by clicking the little arrow beside **Add for me**.</span></span> <span data-ttu-id="57166-180">このチュートリアルでは、[追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="57166-180">In this tutorial, let’s just click Add.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="ngrok を使用したローカル ホストのトンネリングを示すスクリーンショット。":::

## <a name="7-test-your-bot"></a><span data-ttu-id="57166-182">7. ボットをテストする</span><span class="sxs-lookup"><span data-stu-id="57166-182">7. Test your bot</span></span>

<span data-ttu-id="57166-183">ボットに "Hello" と言います。</span><span class="sxs-lookup"><span data-stu-id="57166-183">Let's say "Hello" to your bot.</span></span>

* <span data-ttu-id="57166-184">作成ボックスで、メッセージを送信 `Hello` します。</span><span class="sxs-lookup"><span data-stu-id="57166-184">In the compose box, send a `Hello` message.</span></span>
    <span data-ttu-id="57166-185">ボットは次のようなメッセージで返信します。</span><span class="sxs-lookup"><span data-stu-id="57166-185">Your bot replies with something like the following message:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="ユーザーがボットに 「Hello」 と答え、応答Teams示すスクリーンショット。":::

    <span data-ttu-id="57166-187">これで、ユーザーと 1 対 1 Teamsまたはグループ設定 (チャネルとチャット) で通信できる基本的なボットを作成🎉。</span><span class="sxs-lookup"><span data-stu-id="57166-187">You have now created a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats) 🎉.</span></span>

## <a name="troubleshoot-your-bot"></a><span data-ttu-id="57166-188">ボットのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="57166-188">Troubleshoot your bot</span></span>

<span data-ttu-id="57166-189">このチュートリアルの完了に問題がある場合は、次の情報が役立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="57166-189">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="57166-190">ボットがデバイスに接続Teams</span><span class="sxs-lookup"><span data-stu-id="57166-190">Bot isn't connected to Teams</span></span>


<span data-ttu-id="57166-191">アプリをインストールしたがボットが機能しない場合は、ボットが Azure Bot Service のサービス チャネルに接続されていることを [Teams *してください*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="57166-191">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="57166-192">これは、チャネルと同じではないと理解することが重要Teams。</span><span class="sxs-lookup"><span data-stu-id="57166-192">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="57166-193">この場合、チャネルとは、Azure Bot Service がボットを他の microsoft またはサード パーティの通信アプリTeamsに接続する[方法です](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="57166-193">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="57166-194">関連項目</span><span class="sxs-lookup"><span data-stu-id="57166-194">See also</span></span>

* [<span data-ttu-id="57166-195">ボットの基本</span><span class="sxs-lookup"><span data-stu-id="57166-195">Bot basics</span></span>](../bots/bot-basics.md)
* [<span data-ttu-id="57166-196">ユーザーの個人用タブを作成Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="57166-196">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
* [<span data-ttu-id="57166-197">1 つのサンプルTeamsボットが実行できる他の操作を参照する</span><span class="sxs-lookup"><span data-stu-id="57166-197">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="57166-198">ボット会話の基本</span><span class="sxs-lookup"><span data-stu-id="57166-198">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="57166-199">デザインのガイドライン</span><span class="sxs-lookup"><span data-stu-id="57166-199">Design guidelines</span></span>](../bots/design/bots.md) 
* [<span data-ttu-id="57166-200">実稼働対応の UI テンプレート</span><span class="sxs-lookup"><span data-stu-id="57166-200">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md)
* [<span data-ttu-id="57166-201">ボット認証 (Teams</span><span class="sxs-lookup"><span data-stu-id="57166-201">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="57166-202">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="57166-202">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="57166-203">ツールキットなしでボットを作成する</span><span class="sxs-lookup"><span data-stu-id="57166-203">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a><span data-ttu-id="57166-204">次の手順</span><span class="sxs-lookup"><span data-stu-id="57166-204">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="57166-205">メッセージングの拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="57166-205">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
