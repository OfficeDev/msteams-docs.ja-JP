---
title: 使用を開始する - 最初のメッセージング拡張機能のビルド
author: adrianhall
description: Teams ツールキットを使用して、Microsoft Teams のメッセージング拡張機能を作成します。
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: ad341c386cc9e1bf03cf6e25c0d8be8add0880c6
ms.sourcegitcommit: 2c8b35899dd845acd66f1f927e40d99523c29a91
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2021
ms.locfileid: "52698112"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="ac592-103">Microsoft Teams 用の最初のメッセージング拡張機能のビルド及び実行</span><span class="sxs-lookup"><span data-stu-id="ac592-103">Build and run your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="ac592-104">Teams **メッセージング拡張機能** には、以下の 2 種類があります。</span><span class="sxs-lookup"><span data-stu-id="ac592-104">There are two types of Teams **messaging extensions**:</span></span>

- <span data-ttu-id="ac592-105">[検索コマンド](../messaging-extensions/how-to/search-commands/define-search-command.md)を使用すると、外部システムを検索し、その検索結果をカード形式でメッセージに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="ac592-105">[Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) allow you to search external systems and insert the results of that search into a message in the form of a card.</span></span>
- <span data-ttu-id="ac592-106">[操作コマンド](../messaging-extensions/how-to/action-commands/define-action-command.md)を使用すると、情報を収集または表示するためのモーダル ポップアップをユーザーに表示し、対話を処理した後 Teams に情報を送り返すことができます。</span><span class="sxs-lookup"><span data-stu-id="ac592-106">[Action commands](../messaging-extensions/how-to/action-commands/define-action-command.md) allow you present your users with a modal popup to collect or display information, then process their interaction and send information back to Teams.</span></span>

<span data-ttu-id="ac592-107">このチュートリアルでは、外部データを検索し、その結果をメッセージに挿入する *検索コマンド* を作成します。</span><span class="sxs-lookup"><span data-stu-id="ac592-107">In this tutorial, you will create a *search command* to search for external data and insert the results into a message.</span></span>  

## <a name="before-you-begin"></a><span data-ttu-id="ac592-108">始める前に</span><span class="sxs-lookup"><span data-stu-id="ac592-108">Before you begin</span></span>

<span data-ttu-id="ac592-109">[前提条件](prerequisites.md)をインストールして、開発環境が整っていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ac592-109">Make sure your development environment is set up by installing the [Prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac592-110">前提条件のインストール</span><span class="sxs-lookup"><span data-stu-id="ac592-110">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="ac592-111">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="ac592-111">Create your project</span></span>

<span data-ttu-id="ac592-112">Teams ツールキットを使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="ac592-112">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="ac592-113">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ac592-113">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="ac592-114">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="ac592-114">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="ac592-115">サイド バーの Teams アイコンを選択して、Teams ツールキットを開きます。</span><span class="sxs-lookup"><span data-stu-id="ac592-115">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. <span data-ttu-id="ac592-117">**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ac592-117">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. <span data-ttu-id="ac592-119">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ac592-119">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. <span data-ttu-id="ac592-121">**[機能の選択]** 手順で、**[メッセージ拡張機能]** を選択し、**[タブ]** の選択を解除します。**[OK]** を押します。</span><span class="sxs-lookup"><span data-stu-id="ac592-121">On the **Select capabilities** step, select **Message Extension** and deselect **Tab**.  Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="ac592-123">**[ボットの登録]** 手順で、**[新しいボットの登録を作成する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ac592-123">On the **Bot registration** step, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="新しいボット登録の作成を選択する":::

   > [!NOTE]
   > <span data-ttu-id="ac592-125">メッセージング拡張機能は、ユーザーとコードの間のダイアログを提供するボットに依存しています。</span><span class="sxs-lookup"><span data-stu-id="ac592-125">Messaging extensions rely on bots to provide a dialog between the user and your code.</span></span>

1. <span data-ttu-id="ac592-126">**プログラミング言語** の手順で、**[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ac592-126">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. <span data-ttu-id="ac592-128">ワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="ac592-128">Select a workspace folder.</span></span>  <span data-ttu-id="ac592-129">ワークスペース フォルダー内に、作成中のプロジェクト向けのフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="ac592-129">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="ac592-130">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="ac592-130">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="ac592-131">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="ac592-131">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="ac592-132">**Enter** キーを押して続行します。</span><span class="sxs-lookup"><span data-stu-id="ac592-132">Press **Enter** to continue.</span></span>

<span data-ttu-id="ac592-133">数秒後に Teams アプリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="ac592-133">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="ac592-134">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="ac592-134">Command line</span></span>](#tab/cli)

<span data-ttu-id="ac592-135">`teamsfx` CLI を使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="ac592-135">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="ac592-136">プロジェクト フォルダーを作成するフォルダーから開始します。</span><span class="sxs-lookup"><span data-stu-id="ac592-136">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="ac592-137">CLI では、プロジェクトを作成するためのいくつかの質問を行います。</span><span class="sxs-lookup"><span data-stu-id="ac592-137">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="ac592-138">各質問には、回答方法 (矢印キーで選択肢を選択するなど) が記載されています。</span><span class="sxs-lookup"><span data-stu-id="ac592-138">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="ac592-139">質問に答えた後、**Enter** キーを押して選択を確認します。</span><span class="sxs-lookup"><span data-stu-id="ac592-139">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="ac592-140">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ac592-140">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="ac592-141">**[メッセージング拡張機能]** 機能を選択し、**[タブ]** 機能の選択を解除します。</span><span class="sxs-lookup"><span data-stu-id="ac592-141">Select the **Message Extension** capability and deselect the **Tab** capability.</span></span>
1. <span data-ttu-id="ac592-142">**新しいボット登録の作成** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ac592-142">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="ac592-143">プログラミング言語として **[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ac592-143">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="ac592-144">**Enter** キーを押して、既定のワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="ac592-144">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="ac592-145">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="ac592-145">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="ac592-146">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="ac592-146">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="ac592-147">すべての質問に答えると、プロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="ac592-147">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="ac592-148">ソース コードのツアーを開始する</span><span class="sxs-lookup"><span data-stu-id="ac592-148">Take a tour of the source code</span></span>

<span data-ttu-id="ac592-149">このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。</span><span class="sxs-lookup"><span data-stu-id="ac592-149">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="ac592-150">メッセージング拡張機能では、[[ボット フレームワーク]](https://docs.botframework.com) を使用して、ユーザーが会話を介してサービスと対話できるようにします。</span><span class="sxs-lookup"><span data-stu-id="ac592-150">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="ac592-151">足場を組むと、プロジェクトは以下のようになります。</span><span class="sxs-lookup"><span data-stu-id="ac592-151">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="ボット プロジェクトのファイル レイアウト":::。

<span data-ttu-id="ac592-153">ボット コードは `bot` ディレクトリに格納されています。</span><span class="sxs-lookup"><span data-stu-id="ac592-153">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="ac592-154">`bots/messageExtensionBot.js` は、メッセージング拡張機能の主な入力ポイントです。</span><span class="sxs-lookup"><span data-stu-id="ac592-154">The `bots/messageExtensionBot.js` is the main entry point for the messaging extension.</span></span>

> [!Tip]
> <span data-ttu-id="ac592-155">Teams 内で最初のボットを統合する前に、Teams 外のボットに慣れておきましょう。</span><span class="sxs-lookup"><span data-stu-id="ac592-155">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="ac592-156">ボットの詳細については、[[Azure Bot Service]](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) のチュートリアルをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="ac592-156">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="ac592-157">アプリをローカルで実行する</span><span class="sxs-lookup"><span data-stu-id="ac592-157">Run your app locally</span></span>

<span data-ttu-id="ac592-158">Teams ツールキットでは、アプリをローカルでホストすることができます。</span><span class="sxs-lookup"><span data-stu-id="ac592-158">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="ac592-159">これを行うには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="ac592-159">To do this:</span></span>

- <span data-ttu-id="ac592-160">M365 テナント内に Azure Active Directory アプリケーションが登録されています。</span><span class="sxs-lookup"><span data-stu-id="ac592-160">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="ac592-161">アプリのマニフェストをDeveloper Portal for Teams に送信します。</span><span class="sxs-lookup"><span data-stu-id="ac592-161">An app manifest is submitted to the Developer Portal for Teams.</span></span>
- <span data-ttu-id="ac592-162">API は Azure Functions Core Tools を使用してローカルで実行され、アプリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="ac592-162">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="ac592-163">[ngrok](https://ngrok.io) がインストールされ、Teams とメッセージング拡張機能の間のトンネルを指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="ac592-163">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your messaging extension.</span></span>

<span data-ttu-id="ac592-164">アプリをローカルに構築して実行するには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="ac592-164">To build and run your app locally:</span></span>

1. <span data-ttu-id="ac592-165">Visual Studio Code で、**F5** を押して、アプリケーションをデバッグ モードで実行します。</span><span class="sxs-lookup"><span data-stu-id="ac592-165">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="ac592-166">アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="ac592-166">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="ac592-167">ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="ac592-167">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="ac592-168">この作業には 3 ～ 5 分かかります。</span><span class="sxs-lookup"><span data-stu-id="ac592-168">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="ac592-169">Teams が Web ブラウザーに読み込まれ、サインインするようメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ac592-169">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="ac592-170">Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。</span><span class="sxs-lookup"><span data-stu-id="ac592-170">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="ac592-171">M365 アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="ac592-171">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="ac592-172">**[追加]** を押して、アプリを自分のアカウントに追加します。</span><span class="sxs-lookup"><span data-stu-id="ac592-172">Press **Add** to add the app to your account.</span></span>

<span data-ttu-id="ac592-173">アプリが読み込まれると、そのまま検索ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ac592-173">Once the app is loaded, you will be taken directly to a search dialog:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="検索ベースのメッセージング拡張機能の動作":::

<span data-ttu-id="ac592-175">検索ボックスにテキストを入力し、オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="ac592-175">Type some text in the search box, then select one of the options.</span></span>  <span data-ttu-id="ac592-176">入力ボックスにアダプティブ カードが追加されます。</span><span class="sxs-lookup"><span data-stu-id="ac592-176">An adaptive card will be added to your input box.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="ac592-177">デバッガーでアプリをローカルに実行した場合に発生することを説明します。</span><span class="sxs-lookup"><span data-stu-id="ac592-177">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="ac592-178">F5 を押すと、以下のように Teams ツールキットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ac592-178">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="ac592-179">Azure Active Directory を使用してアプリケーションを登録しました。</span><span class="sxs-lookup"><span data-stu-id="ac592-179">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="ac592-180">Microsoft Teams で "サイド読み込み" 用にアプリケーションを登録しました。</span><span class="sxs-lookup"><span data-stu-id="ac592-180">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="ac592-181">[Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start) を使用して、アプリケーション バックエンドのローカルでの実行を開始しました。</span><span class="sxs-lookup"><span data-stu-id="ac592-181">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="ac592-182">Teams がアプリと通信できるように、ngrok トンネルを開始しました。</span><span class="sxs-lookup"><span data-stu-id="ac592-182">Started an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="ac592-183">アプリケーションのサイドロードを Teams に指示するコマンドで Microsoft Teams を開始します。</span><span class="sxs-lookup"><span data-stu-id="ac592-183">Started Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="ac592-184">アプリをローカルで実行する場合の一般的な問題のトラブルシューティングを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ac592-184">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="ac592-185">Teams でアプリを正常に実行するには、アプリのサイドロードを許可する Microsoft 365 開発アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="ac592-185">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="ac592-186">アカウント開設の詳細については、「[前提条件](prerequisites.md#enable-sideloading)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ac592-186">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="ac592-187">ツールキットに含まれる[アプリ認証ツール](https://dev.teams.microsoft.com/appvalidation.html)を使用して、アプリをサイドロードする前に問題がないか確認します。</span><span class="sxs-lookup"><span data-stu-id="ac592-187">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="ac592-188">エラーを修正して、アプリを正常にサイドロードします。</span><span class="sxs-lookup"><span data-stu-id="ac592-188">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="ac592-189">アプリを Azure に展開した場合に発生することを説明します</span><span class="sxs-lookup"><span data-stu-id="ac592-189">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="ac592-190">展開前は、このアプリケーションは以下のようにローカルで動作しています。</span><span class="sxs-lookup"><span data-stu-id="ac592-190">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="ac592-191">バックエンドは、_Azure Functions Core Tools_ を使用して実行します。</span><span class="sxs-lookup"><span data-stu-id="ac592-191">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="ac592-192">アプリケーションの HTTP エンドポイントは、Microsoft Teams がアプリケーションを読み込む場所でローカルに実行されます。</span><span class="sxs-lookup"><span data-stu-id="ac592-192">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="ac592-193">展開では、アクティブな Azure サブスクリプションにリソースをプロビジョニングし、アプリケーションのバックエンドとフロントエンドのコードを Azure に展開 (アップロード) します。</span><span class="sxs-lookup"><span data-stu-id="ac592-193">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="ac592-194">バックエンドには、Azure App Service や Azure Bot Service など、さまざまな Azure のサービスが使用されています。</span><span class="sxs-lookup"><span data-stu-id="ac592-194">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="next-steps"></a><span data-ttu-id="ac592-195">次の手順</span><span class="sxs-lookup"><span data-stu-id="ac592-195">Next steps</span></span>

<span data-ttu-id="ac592-196">Teams アプリを作成する他の方法についてご紹介します。</span><span class="sxs-lookup"><span data-stu-id="ac592-196">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="ac592-197">React を使用して Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="ac592-197">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="ac592-198">Blazor を使用して Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="ac592-198">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="ac592-199">[SharePoint Web パーツとして Teams アプリを作成する](first-app-spfx.md) (Azure は必要なし)</span><span class="sxs-lookup"><span data-stu-id="ac592-199">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="ac592-200">会話ボットを作成する</span><span class="sxs-lookup"><span data-stu-id="ac592-200">Create a conversation bot</span></span>](first-app-bot.md)
