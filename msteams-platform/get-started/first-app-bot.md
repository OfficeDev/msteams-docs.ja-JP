---
title: 使用を開始する - 最初の会話型ボットのビルド
author: adrianhall
description: Teams ツールキットを使用して、Microsoft Teams の会話ボットを作成します。
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: 3084020000cf53fbb33ffc25d141b41ffff83160
ms.sourcegitcommit: 2c8b35899dd845acd66f1f927e40d99523c29a91
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2021
ms.locfileid: "52697976"
---
# <a name="build-your-first-conversational-bot-for-microsoft-teams"></a><span data-ttu-id="487f2-103">Microsoft Teams 用の会話型ボットをビルドする</span><span class="sxs-lookup"><span data-stu-id="487f2-103">Build your first conversational bot for Microsoft Teams</span></span>

<span data-ttu-id="487f2-104">ボットは、Teams ユーザーと Web サービスの間を仲介する役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="487f2-104">A bot acts as an intermediary between a Teams user and a web service.</span></span>  <span data-ttu-id="487f2-105">ユーザーは、ボットとチャットすることで、情報を素早く入手したり、ワークフローを開始したり、Web サービスに可能なすべてのことができます。</span><span class="sxs-lookup"><span data-stu-id="487f2-105">Users can chat with a bot to quickly get information, initiate workflows, or anything else your web service can do.</span></span>  <span data-ttu-id="487f2-106">このチュートリアルでは、Teams ボット アプリを構築し、実行し、展開する方法を学びます。</span><span class="sxs-lookup"><span data-stu-id="487f2-106">In this tutorial, you will learn how to build, run, and deploy a Teams bot app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="487f2-107">始める前に</span><span class="sxs-lookup"><span data-stu-id="487f2-107">Before you begin</span></span>

<span data-ttu-id="487f2-108">[前提条件](prerequisites.md)をインストールして、開発環境が整っていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="487f2-108">Make sure your development environment is set up by installing the [Prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="487f2-109">前提条件のインストール</span><span class="sxs-lookup"><span data-stu-id="487f2-109">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="487f2-110">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="487f2-110">Create your project</span></span>

<span data-ttu-id="487f2-111">Teams ツールキットを使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="487f2-111">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="487f2-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="487f2-112">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="487f2-113">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="487f2-113">Open Visual Studio code.</span></span>
1. <span data-ttu-id="487f2-114">サイド バーの Teams アイコンを選択して、Teams ツールキットを開きます。</span><span class="sxs-lookup"><span data-stu-id="487f2-114">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. <span data-ttu-id="487f2-116">**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="487f2-116">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. <span data-ttu-id="487f2-118">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="487f2-118">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. <span data-ttu-id="487f2-120">**[機能の選択]** 手順で、**[ボット]** を選択し、**[タブ]** の選択を解除します。**[OK]** を押します。</span><span class="sxs-lookup"><span data-stu-id="487f2-120">On the **Select capabilities** step, select **Bot** and deselect **Tab**.  Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="487f2-122">**[ボットの登録]** 手順で、**[新しいボットの登録を作成する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="487f2-122">On the **Bot registration** step, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="新しいボット登録の作成を選択する":::

1. <span data-ttu-id="487f2-124">**プログラミング言語** の手順で、**[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="487f2-124">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. <span data-ttu-id="487f2-126">ワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="487f2-126">Select a workspace folder.</span></span>  <span data-ttu-id="487f2-127">ワークスペース フォルダー内に、作成中のプロジェクト向けのフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="487f2-127">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="487f2-128">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="487f2-128">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="487f2-129">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="487f2-129">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="487f2-130">**Enter** キーを押して続行します。</span><span class="sxs-lookup"><span data-stu-id="487f2-130">Press **Enter** to continue.</span></span>

<span data-ttu-id="487f2-131">数秒後に Teams アプリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="487f2-131">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="487f2-132">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="487f2-132">Command line</span></span>](#tab/cli)

<span data-ttu-id="487f2-133">`teamsfx` CLI を使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="487f2-133">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="487f2-134">プロジェクト フォルダーを作成するフォルダーから開始します。</span><span class="sxs-lookup"><span data-stu-id="487f2-134">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="487f2-135">CLI では、プロジェクトを作成するためのいくつかの質問を行います。</span><span class="sxs-lookup"><span data-stu-id="487f2-135">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="487f2-136">各質問には、回答方法 (矢印キーで選択肢を選択するなど) が記載されています。</span><span class="sxs-lookup"><span data-stu-id="487f2-136">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="487f2-137">質問に答えた後、**Enter** キーを押して選択を確認します。</span><span class="sxs-lookup"><span data-stu-id="487f2-137">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="487f2-138">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="487f2-138">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="487f2-139">**[ボット]** 機能を選択し、**[タブ]** 機能の選択を解除します。</span><span class="sxs-lookup"><span data-stu-id="487f2-139">Select the **Bot** capability and deselect the **Tab** capability.</span></span>
1. <span data-ttu-id="487f2-140">**新しいボット登録の作成** を選択します。</span><span class="sxs-lookup"><span data-stu-id="487f2-140">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="487f2-141">プログラミング言語として **[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="487f2-141">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="487f2-142">**Enter** キーを押して、既定のワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="487f2-142">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="487f2-143">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="487f2-143">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="487f2-144">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="487f2-144">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="487f2-145">すべての質問に答えると、プロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="487f2-145">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="487f2-146">ソース コードのツアーを開始する</span><span class="sxs-lookup"><span data-stu-id="487f2-146">Take a tour of the source code</span></span>

<span data-ttu-id="487f2-147">このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。</span><span class="sxs-lookup"><span data-stu-id="487f2-147">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="487f2-148">メッセージング拡張機能では、[[ボット フレームワーク]](https://docs.botframework.com) を使用して、ユーザーが会話を介してサービスと対話できるようにします。</span><span class="sxs-lookup"><span data-stu-id="487f2-148">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="487f2-149">足場を組むと、プロジェクトは以下のようになります。</span><span class="sxs-lookup"><span data-stu-id="487f2-149">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="ボット プロジェクトのファイル レイアウト":::。

<span data-ttu-id="487f2-151">ボット コードは `bot` ディレクトリに格納されています。</span><span class="sxs-lookup"><span data-stu-id="487f2-151">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="487f2-152">`bots/teamsBot.js` はボットの主な入力ポイントで、ダイアログは `dialogs` ディレクトリに格納されます。</span><span class="sxs-lookup"><span data-stu-id="487f2-152">The `bots/teamsBot.js` is the main entry point for the bot, and the dialogs are stored in the `dialogs` directory.</span></span>

> [!Tip]
> <span data-ttu-id="487f2-153">Teams 内で最初のボットを統合する前に、Teams 外のボットに慣れておきましょう。</span><span class="sxs-lookup"><span data-stu-id="487f2-153">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="487f2-154">ボットの詳細については、[[Azure Bot Service]](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) のチュートリアルをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="487f2-154">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="487f2-155">アプリをローカルで実行する</span><span class="sxs-lookup"><span data-stu-id="487f2-155">Run your app locally</span></span>

<span data-ttu-id="487f2-156">Teams ツールキットでは、アプリをローカルでホストすることができます。</span><span class="sxs-lookup"><span data-stu-id="487f2-156">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="487f2-157">これを行うには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="487f2-157">To do this:</span></span>

- <span data-ttu-id="487f2-158">M365 テナント内に Azure Active Directory アプリケーションが登録されています。</span><span class="sxs-lookup"><span data-stu-id="487f2-158">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="487f2-159">アプリのマニフェストを Teams の開発者センターに送信します。</span><span class="sxs-lookup"><span data-stu-id="487f2-159">An app manifest is submitted to the Developer Center for Teams.</span></span>
- <span data-ttu-id="487f2-160">API は Azure Functions Core Tools を使用してローカルで実行され、アプリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="487f2-160">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="487f2-161">[ngrok](https://ngrok.io) がインストールされ、Teams とボット コードの間のトンネルを指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="487f2-161">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your bot code.</span></span>

<span data-ttu-id="487f2-162">アプリをローカルに構築して実行するには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="487f2-162">To build and run your app locally:</span></span>

1. <span data-ttu-id="487f2-163">Visual Studio Code で、**F5** を押して、アプリケーションをデバッグ モードで実行します。</span><span class="sxs-lookup"><span data-stu-id="487f2-163">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="487f2-164">アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="487f2-164">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="487f2-165">ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="487f2-165">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="487f2-166">この作業には 3 ～ 5 分かかります。</span><span class="sxs-lookup"><span data-stu-id="487f2-166">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="487f2-167">アプリケーションを実行するために Web ブラウザーが起動します。</span><span class="sxs-lookup"><span data-stu-id="487f2-167">Your web browser is started to run the application.</span></span> <span data-ttu-id="487f2-168">Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。</span><span class="sxs-lookup"><span data-stu-id="487f2-168">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="487f2-169">メッセージが表示されたら、**[代わりに Web アプリケーションを使用する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="487f2-169">When prompted, select **Use the web app instead**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="起動時に Web 版のチームを選択する方法を示すスクリーンショット":::

1. <span data-ttu-id="487f2-171">サインインするように求めるメッセージが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="487f2-171">You may be prompted to sign in.</span></span>  <span data-ttu-id="487f2-172">その場合は、M365 アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="487f2-172">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="487f2-173">Teams へのアプリのインストールを促すメッセージが表示された場合は、**[追加]** を押してください。</span><span class="sxs-lookup"><span data-stu-id="487f2-173">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="487f2-174">アプリが読み込まれると、そのままボットを使用したチャット セッションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="487f2-174">Once the app is loaded, you will be taken directly to a chat session with the bot.</span></span>  <span data-ttu-id="487f2-175">`intro` を入力すると紹介カードが表示され、`show` を入力すると Microsoft Graph からユーザーの詳細情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="487f2-175">You can type `intro` to show an introduction card, and `show` to show your details from Microsoft Graph.</span></span>  <span data-ttu-id="487f2-176">(これには追加で許可の承認が必要です)。</span><span class="sxs-lookup"><span data-stu-id="487f2-176">(This will require an additional permissions approval).</span></span>

<span data-ttu-id="487f2-177">デバッグは通常通りに動作します。実際にお試しください。</span><span class="sxs-lookup"><span data-stu-id="487f2-177">Debugging works as you normally would expect - try it yourself!</span></span> <span data-ttu-id="487f2-178">`bot/dialogs/rootDialog.js` ファイルを開き、`triggerCommand(...)` メソッドを探します。</span><span class="sxs-lookup"><span data-stu-id="487f2-178">Open the `bot/dialogs/rootDialog.js` file and locate the `triggerCommand(...)` method.</span></span>  <span data-ttu-id="487f2-179">既定のケースにブレークポイントを設定します。</span><span class="sxs-lookup"><span data-stu-id="487f2-179">Set a breakpoint on the default case.</span></span>  <span data-ttu-id="487f2-180">次に、テキストを入力します。</span><span class="sxs-lookup"><span data-stu-id="487f2-180">Then type some text.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="487f2-181">デバッガーでアプリをローカルに実行した場合に発生することを説明します。</span><span class="sxs-lookup"><span data-stu-id="487f2-181">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="487f2-182">F5 を押すと、以下のように Teams ツールキットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="487f2-182">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="487f2-183">Azure Active Directory を使用してアプリケーションを登録しました。</span><span class="sxs-lookup"><span data-stu-id="487f2-183">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="487f2-184">Microsoft Teams で "サイド読み込み" 用にアプリケーションを登録しました。</span><span class="sxs-lookup"><span data-stu-id="487f2-184">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="487f2-185">[Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start) を使用して、アプリケーション バックエンドのローカルでの実行を開始しました。</span><span class="sxs-lookup"><span data-stu-id="487f2-185">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="487f2-186">Teams がアプリと通信できるように、ngrok トンネルを開始しました。</span><span class="sxs-lookup"><span data-stu-id="487f2-186">Started an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="487f2-187">アプリケーションのサイドロードを Teams に指示するコマンドで Microsoft Teams を開始します。</span><span class="sxs-lookup"><span data-stu-id="487f2-187">Started Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="487f2-188">アプリをローカルで実行する場合の一般的な問題のトラブルシューティングを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="487f2-188">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="487f2-189">Teams でアプリを正常に実行するには、アプリのサイドロードを許可する Microsoft 365 開発アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="487f2-189">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="487f2-190">アカウント開設の詳細については、「[前提条件](prerequisites.md#enable-sideloading)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="487f2-190">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="487f2-191">ツールキットに含まれる[アプリ認証ツール](https://dev.teams.microsoft.com/appvalidation.html)を使用して、アプリをサイドロードする前に問題がないか確認します。</span><span class="sxs-lookup"><span data-stu-id="487f2-191">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="487f2-192">エラーを修正して、アプリを正常にサイドロードします。</span><span class="sxs-lookup"><span data-stu-id="487f2-192">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="487f2-193">アプリを Azure に展開した場合に発生することを説明します</span><span class="sxs-lookup"><span data-stu-id="487f2-193">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="487f2-194">展開前は、このアプリケーションは以下のようにローカルで動作しています。</span><span class="sxs-lookup"><span data-stu-id="487f2-194">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="487f2-195">バックエンドは、_Azure Functions Core Tools_ を使用して実行します。</span><span class="sxs-lookup"><span data-stu-id="487f2-195">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="487f2-196">アプリケーションの HTTP エンドポイントは、Microsoft Teams がアプリケーションを読み込む場所でローカルに実行されます。</span><span class="sxs-lookup"><span data-stu-id="487f2-196">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="487f2-197">展開では、アクティブな Azure サブスクリプションにリソースをプロビジョニングし、アプリケーションのバックエンドとフロントエンドのコードを Azure に展開 (アップロード) します。</span><span class="sxs-lookup"><span data-stu-id="487f2-197">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="487f2-198">バックエンドには、Azure App Service や Azure Bot Service など、さまざまな Azure のサービスが使用されています。</span><span class="sxs-lookup"><span data-stu-id="487f2-198">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="next-steps"></a><span data-ttu-id="487f2-199">次の手順</span><span class="sxs-lookup"><span data-stu-id="487f2-199">Next steps</span></span>

<span data-ttu-id="487f2-200">Teams アプリを作成する他の方法についてご紹介します。</span><span class="sxs-lookup"><span data-stu-id="487f2-200">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="487f2-201">React を使用して Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="487f2-201">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="487f2-202">Blazor を使用して Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="487f2-202">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="487f2-203">[SharePoint Web パーツとして Teams アプリを作成する](first-app-spfx.md) (Azure は必要なし)</span><span class="sxs-lookup"><span data-stu-id="487f2-203">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="487f2-204">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="487f2-204">Create a messaging extension</span></span>](first-message-extension.md)
