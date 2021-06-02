---
title: 使用を開始する - 最初のメッセージング拡張機能のビルド
author: adrianhall
description: Teams ツールキットを使用して、Microsoft Teams のメッセージング拡張機能を作成します。
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: eaecb045993f8dfd21f4c2c4359a4a3388d659e6
ms.sourcegitcommit: e50cdeb6b7f481e12911b2bb74a8da22af0bffac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2021
ms.locfileid: "52710649"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="2cc77-103">Microsoft Teams 用の最初のメッセージング拡張機能のビルド及び実行</span><span class="sxs-lookup"><span data-stu-id="2cc77-103">Build and run your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="2cc77-104">Teams **メッセージング拡張機能** には、以下の 2 種類があります。</span><span class="sxs-lookup"><span data-stu-id="2cc77-104">There are two types of Teams **messaging extensions**:</span></span>

- <span data-ttu-id="2cc77-105">[検索コマンド](../messaging-extensions/how-to/search-commands/define-search-command.md)を使用すると、外部システムを検索し、その検索結果をカード形式でメッセージに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-105">[Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) allow you to search external systems and insert the results of that search into a message in the form of a card.</span></span>
- <span data-ttu-id="2cc77-106">[操作コマンド](../messaging-extensions/how-to/action-commands/define-action-command.md)を使用すると、情報を収集または表示するためのモーダル ポップアップをユーザーに表示し、対話を処理した後 Teams に情報を送り返すことができます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-106">[Action commands](../messaging-extensions/how-to/action-commands/define-action-command.md) allow you present your users with a modal popup to collect or display information, then process their interaction and send information back to Teams.</span></span>

<span data-ttu-id="2cc77-107">このチュートリアルでは、外部データを検索し、その結果をメッセージに挿入する *検索コマンド* を作成します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-107">In this tutorial, you will create a *search command* to search for external data and insert the results into a message.</span></span>  

## <a name="before-you-begin"></a><span data-ttu-id="2cc77-108">始める前に</span><span class="sxs-lookup"><span data-stu-id="2cc77-108">Before you begin</span></span>

<span data-ttu-id="2cc77-109">[前提条件](prerequisites.md)をインストールして、開発環境が整っていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-109">Make sure your development environment is set up by installing the [Prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2cc77-110">前提条件のインストール</span><span class="sxs-lookup"><span data-stu-id="2cc77-110">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="2cc77-111">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="2cc77-111">Create your project</span></span>

<span data-ttu-id="2cc77-112">Teams ツールキットを使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-112">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="2cc77-113">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2cc77-113">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="2cc77-114">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-114">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="2cc77-115">サイド バーの Teams アイコンを選択して、Teams ツールキットを開きます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-115">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. <span data-ttu-id="2cc77-117">**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-117">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. <span data-ttu-id="2cc77-119">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-119">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. <span data-ttu-id="2cc77-121">**[機能の選択]** 手順で、**[メッセージ拡張機能]** を選択し、**[タブ]** の選択を解除します。**[OK]** を押します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-121">On the **Select capabilities** step, select **Message Extension** and deselect **Tab**.  Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="2cc77-123">**[ボットの登録]** 手順で、**[新しいボットの登録を作成する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-123">On the **Bot registration** step, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="新しいボット登録の作成を選択する":::

   > [!NOTE]
   > <span data-ttu-id="2cc77-125">メッセージング拡張機能は、ユーザーとコードの間のダイアログを提供するボットに依存しています。</span><span class="sxs-lookup"><span data-stu-id="2cc77-125">Messaging extensions rely on bots to provide a dialog between the user and your code.</span></span>

1. <span data-ttu-id="2cc77-126">**プログラミング言語** の手順で、**[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-126">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. <span data-ttu-id="2cc77-128">ワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-128">Select a workspace folder.</span></span>  <span data-ttu-id="2cc77-129">ワークスペース フォルダー内に、作成中のプロジェクト向けのフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-129">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="2cc77-130">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-130">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="2cc77-131">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cc77-131">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="2cc77-132">**Enter** キーを押して続行します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-132">Press **Enter** to continue.</span></span>

<span data-ttu-id="2cc77-133">数秒後に Teams アプリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-133">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="2cc77-134">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="2cc77-134">Command line</span></span>](#tab/cli)

<span data-ttu-id="2cc77-135">`teamsfx` CLI を使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-135">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="2cc77-136">プロジェクト フォルダーを作成するフォルダーから開始します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-136">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="2cc77-137">CLI では、プロジェクトを作成するためのいくつかの質問を行います。</span><span class="sxs-lookup"><span data-stu-id="2cc77-137">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="2cc77-138">各質問には、回答方法 (矢印キーで選択肢を選択するなど) が記載されています。</span><span class="sxs-lookup"><span data-stu-id="2cc77-138">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="2cc77-139">質問に答えた後、**Enter** キーを押して選択を確認します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-139">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="2cc77-140">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-140">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="2cc77-141">**[メッセージング拡張機能]** 機能を選択し、**[タブ]** 機能の選択を解除します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-141">Select the **Message Extension** capability and deselect the **Tab** capability.</span></span>
1. <span data-ttu-id="2cc77-142">**新しいボット登録の作成** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-142">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="2cc77-143">プログラミング言語として **[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-143">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="2cc77-144">**Enter** キーを押して、既定のワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-144">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="2cc77-145">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-145">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="2cc77-146">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cc77-146">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="2cc77-147">すべての質問に答えると、プロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-147">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="2cc77-148">ソース コードのツアーを開始する</span><span class="sxs-lookup"><span data-stu-id="2cc77-148">Take a tour of the source code</span></span>

<span data-ttu-id="2cc77-149">このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-149">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="2cc77-150">メッセージング拡張機能では、[[ボット フレームワーク]](https://docs.botframework.com) を使用して、ユーザーが会話を介してサービスと対話できるようにします。</span><span class="sxs-lookup"><span data-stu-id="2cc77-150">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="2cc77-151">足場を組むと、プロジェクトは以下のようになります。</span><span class="sxs-lookup"><span data-stu-id="2cc77-151">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="ボット プロジェクトのファイル レイアウト":::。

<span data-ttu-id="2cc77-153">ボット コードは `bot` ディレクトリに格納されています。</span><span class="sxs-lookup"><span data-stu-id="2cc77-153">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="2cc77-154">`bots/messageExtensionBot.js` は、メッセージング拡張機能の主な入力ポイントです。</span><span class="sxs-lookup"><span data-stu-id="2cc77-154">The `bots/messageExtensionBot.js` is the main entry point for the messaging extension.</span></span>

> [!Tip]
> <span data-ttu-id="2cc77-155">Teams 内で最初のボットを統合する前に、Teams 外のボットに慣れておきましょう。</span><span class="sxs-lookup"><span data-stu-id="2cc77-155">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="2cc77-156">ボットの詳細については、[[Azure Bot Service]](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) のチュートリアルをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2cc77-156">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="2cc77-157">アプリをローカルで実行する</span><span class="sxs-lookup"><span data-stu-id="2cc77-157">Run your app locally</span></span>

<span data-ttu-id="2cc77-158">Teams ツールキットでは、アプリをローカルでホストすることができます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-158">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="2cc77-159">これを行うには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-159">To do this:</span></span>

- <span data-ttu-id="2cc77-160">M365 テナント内に Azure Active Directory アプリケーションが登録されています。</span><span class="sxs-lookup"><span data-stu-id="2cc77-160">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="2cc77-161">アプリのマニフェストをDeveloper Portal for Teams に送信します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-161">An app manifest is submitted to the Developer Portal for Teams.</span></span>
- <span data-ttu-id="2cc77-162">API は Azure Functions Core Tools を使用してローカルで実行され、アプリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="2cc77-162">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="2cc77-163">[ngrok](https://ngrok.io) がインストールされ、Teams とメッセージング拡張機能の間のトンネルを指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-163">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your messaging extension.</span></span>

<span data-ttu-id="2cc77-164">アプリをローカルに構築して実行するには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="2cc77-164">To build and run your app locally:</span></span>

1. <span data-ttu-id="2cc77-165">Visual Studio Code で、**F5** を押して、アプリケーションをデバッグ モードで実行します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-165">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="2cc77-166">アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-166">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="2cc77-167">ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-167">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="2cc77-168">この作業には 3 ～ 5 分かかります。</span><span class="sxs-lookup"><span data-stu-id="2cc77-168">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="2cc77-169">Teams が Web ブラウザーに読み込まれ、サインインするようメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-169">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="2cc77-170">Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。</span><span class="sxs-lookup"><span data-stu-id="2cc77-170">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="2cc77-171">M365 アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="2cc77-171">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="2cc77-172">**[追加]** を押して、アプリを自分のアカウントに追加します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-172">Press **Add** to add the app to your account.</span></span>

<span data-ttu-id="2cc77-173">アプリが読み込まれると、そのまま検索ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-173">Once the app is loaded, you will be taken directly to a search dialog:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="検索ベースのメッセージング拡張機能の動作":::

<span data-ttu-id="2cc77-175">検索ボックスにテキストを入力し、オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-175">Type some text in the search box, then select one of the options.</span></span>  <span data-ttu-id="2cc77-176">入力ボックスにアダプティブ カードが追加されます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-176">An adaptive card will be added to your input box.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="2cc77-177">デバッガーでアプリをローカルに実行した場合に発生することを説明します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-177">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="2cc77-178">F5 を押すと、以下のように Teams ツールキットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-178">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="2cc77-179">Azure Active Directory を使用してアプリケーションを登録しました。</span><span class="sxs-lookup"><span data-stu-id="2cc77-179">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="2cc77-180">Microsoft Teams で "サイド読み込み" 用にアプリケーションを登録しました。</span><span class="sxs-lookup"><span data-stu-id="2cc77-180">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="2cc77-181">[Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start) を使用して、アプリケーション バックエンドのローカルでの実行を開始しました。</span><span class="sxs-lookup"><span data-stu-id="2cc77-181">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="2cc77-182">Teams がアプリと通信できるように、ngrok トンネルを開始しました。</span><span class="sxs-lookup"><span data-stu-id="2cc77-182">Started an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="2cc77-183">アプリケーションのサイドロードを Teams に指示するコマンドで Microsoft Teams を開始します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-183">Started Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="2cc77-184">アプリをローカルで実行する場合の一般的な問題のトラブルシューティングを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-184">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="2cc77-185">Teams でアプリを正常に実行するには、アプリのサイドロードを許可する Microsoft 365 開発アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="2cc77-185">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="2cc77-186">アカウント開設の詳細については、「[前提条件](prerequisites.md#enable-sideloading)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2cc77-186">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="2cc77-187">ツールキットに含まれる[アプリ認証ツール](https://dev.teams.microsoft.com/appvalidation.html)を使用して、アプリをサイドロードする前に問題がないか確認します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-187">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="2cc77-188">エラーを修正して、アプリを正常にサイドロードします。</span><span class="sxs-lookup"><span data-stu-id="2cc77-188">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="2cc77-189">アプリを Azure に展開した場合に発生することを説明します</span><span class="sxs-lookup"><span data-stu-id="2cc77-189">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="2cc77-190">展開前は、このアプリケーションは以下のようにローカルで動作しています。</span><span class="sxs-lookup"><span data-stu-id="2cc77-190">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="2cc77-191">バックエンドは、_Azure Functions Core Tools_ を使用して実行します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-191">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="2cc77-192">アプリケーションの HTTP エンドポイントは、Microsoft Teams がアプリケーションを読み込む場所でローカルに実行されます。</span><span class="sxs-lookup"><span data-stu-id="2cc77-192">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="2cc77-193">展開では、アクティブな Azure サブスクリプションにリソースをプロビジョニングし、アプリケーションのバックエンドとフロントエンドのコードを Azure に展開 (アップロード) します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-193">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="2cc77-194">バックエンドには、Azure App Service や Azure Bot Service など、さまざまな Azure のサービスが使用されています。</span><span class="sxs-lookup"><span data-stu-id="2cc77-194">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="add-a-configuration-page-to-your-messaging-extension"></a><span data-ttu-id="2cc77-195">メッセージング拡張機能に構成ページを追加する</span><span class="sxs-lookup"><span data-stu-id="2cc77-195">Add a configuration page to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="code-sample"></a><span data-ttu-id="2cc77-196">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="2cc77-196">Code sample</span></span>

<span data-ttu-id="2cc77-197">Teams上GitHubサンプル プロジェクトの検索 Auth Config では、構成ページとボット サービス認証を含むメッセージング拡張機能を作成する方法[を示します](https://github.com/microsoft/BotBuilder-Samples#teams-samples)。</span><span class="sxs-lookup"><span data-stu-id="2cc77-197">The Teams Search Auth Config for sample projects on GitHub, demonstrate how to create messaging extensions that include a configuration page and [Bot Service authentication](https://github.com/microsoft/BotBuilder-Samples#teams-samples).</span></span> <span data-ttu-id="2cc77-198">このサンプルでは、ユーザーがサインインした後に、検索要求を受け入れ、結果を返すメッセージ拡張機能を作成する方法も示しています。</span><span class="sxs-lookup"><span data-stu-id="2cc77-198">The samples also demonstrate how to create message extensions that accept search requests and return the results after the user has signed in.</span></span>

| <span data-ttu-id="2cc77-199">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="2cc77-199">**Sample name**</span></span> | <span data-ttu-id="2cc77-200">**説明**</span><span class="sxs-lookup"><span data-stu-id="2cc77-200">**Description**</span></span> | <span data-ttu-id="2cc77-201">**.NET**</span><span class="sxs-lookup"><span data-stu-id="2cc77-201">**.NET**</span></span> | <span data-ttu-id="2cc77-202">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="2cc77-202">**Node.js**</span></span> | <span data-ttu-id="2cc77-203">**Python**</span><span class="sxs-lookup"><span data-stu-id="2cc77-203">**Python**</span></span> |
|-----------------|-----------------|-------------|--------------|--------|
| <span data-ttu-id="2cc77-204">ボット ビルダー</span><span class="sxs-lookup"><span data-stu-id="2cc77-204">Bot builder</span></span> | <span data-ttu-id="2cc77-205">メッセージング拡張機能を作成するには。</span><span class="sxs-lookup"><span data-stu-id="2cc77-205">To create messaging extensions.</span></span> | [<span data-ttu-id="2cc77-206">View</span><span class="sxs-lookup"><span data-stu-id="2cc77-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="2cc77-207">View</span><span class="sxs-lookup"><span data-stu-id="2cc77-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="2cc77-208">View</span><span class="sxs-lookup"><span data-stu-id="2cc77-208">View</span></span>]( https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="additional-code-sample"></a><span data-ttu-id="2cc77-209">追加のコード サンプル</span><span class="sxs-lookup"><span data-stu-id="2cc77-209">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2cc77-210">ボット フレームワークのサンプルを表示する GitHub</span><span class="sxs-lookup"><span data-stu-id="2cc77-210">View more Bot Framework Samples on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-samples#messaging-extensions-samples-using-the-v4-sdk)

## <a name="next-steps"></a><span data-ttu-id="2cc77-211">次の手順</span><span class="sxs-lookup"><span data-stu-id="2cc77-211">Next steps</span></span>

<span data-ttu-id="2cc77-212">Teams アプリを作成する他の方法についてご紹介します。</span><span class="sxs-lookup"><span data-stu-id="2cc77-212">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="2cc77-213">React を使用して Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="2cc77-213">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="2cc77-214">Blazor を使用して Teams アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="2cc77-214">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="2cc77-215">[SharePoint Web パーツとして Teams アプリを作成する](first-app-spfx.md) (Azure は必要なし)</span><span class="sxs-lookup"><span data-stu-id="2cc77-215">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="2cc77-216">会話ボットを作成する</span><span class="sxs-lookup"><span data-stu-id="2cc77-216">Create a conversation bot</span></span>](first-app-bot.md)
