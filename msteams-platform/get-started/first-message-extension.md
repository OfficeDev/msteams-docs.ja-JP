---
title: 使用を開始する - 最初のメッセージング拡張機能のビルド
author: adrianhall
description: Teams ツールキットを使用して、Microsoft Teams のメッセージング拡張機能を作成します。
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: 3566bc55c9995a8407b1344fbdb7d1548e210046
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254289"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="213ed-103">Microsoft Teams 用の最初のメッセージング拡張機能のビルド及び実行</span><span class="sxs-lookup"><span data-stu-id="213ed-103">Build and run your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="213ed-104">このチュートリアルでは、外部データを検索して結果をメッセージに挿入する検索コマンドを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="213ed-104">In this tutorial, you will learn how to create a *search command* to search for external data and insert the results into a message.</span></span> 

<span data-ttu-id="213ed-105">Teams **メッセージング拡張機能** には、以下の 2 種類があります。</span><span class="sxs-lookup"><span data-stu-id="213ed-105">There are two types of Teams **messaging extensions**:</span></span>

- <span data-ttu-id="213ed-106">[検索コマンド](../messaging-extensions/how-to/search-commands/define-search-command.md)を使用すると、外部システムを検索し、その検索結果をカード形式でメッセージに挿入できます。</span><span class="sxs-lookup"><span data-stu-id="213ed-106">[Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) allow you to search external systems and insert the results of that search into a message in the form of a card.</span></span>
- <span data-ttu-id="213ed-107">[操作コマンド](../messaging-extensions/how-to/action-commands/define-action-command.md)を使用すると、情報を収集または表示するためのモーダル ポップアップをユーザーに表示し、対話を処理した後 Teams に情報を送り返すことができます。</span><span class="sxs-lookup"><span data-stu-id="213ed-107">[Action commands](../messaging-extensions/how-to/action-commands/define-action-command.md) allow you present your users with a modal popup to collect or display information, then process their interaction and send information back to Teams.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="213ed-108">はじめに</span><span class="sxs-lookup"><span data-stu-id="213ed-108">Before you begin</span></span>

<span data-ttu-id="213ed-109">前提条件をインストールして、開発環境がセットアップされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="213ed-109">Make sure your development environment is set up by installing the Prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="213ed-110">前提条件のインストール</span><span class="sxs-lookup"><span data-stu-id="213ed-110">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="213ed-111">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="213ed-111">Create your project</span></span>

<span data-ttu-id="213ed-112">Teams ツールキットを使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="213ed-112">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="213ed-113">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="213ed-113">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="213ed-114">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="213ed-114">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="213ed-115">サイドバーのTeamsアイコンを選択して、ウィンドウを開Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="213ed-115">Select the Teams icon in the sidebar to open the Teams Toolkit.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. <span data-ttu-id="213ed-117">**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="213ed-117">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. <span data-ttu-id="213ed-119">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="213ed-119">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. <span data-ttu-id="213ed-121">[機能 **の選択] セクションで**、[メッセージ拡張機能] を **選択し、[** タブ] の選択を **解除し\*\*\*\*、[OK] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="213ed-121">In the **Select capabilities** section, select **Message Extension**, deselect **Tab** and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="213ed-123">[ボット登録 **] セクションで** 、[新しい **ボット登録の作成] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="213ed-123">In the **Bot registration** section, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="新しいボット登録の作成を選択する":::

   > [!NOTE]
   > <span data-ttu-id="213ed-125">メッセージング拡張機能は、ユーザーとコードの間のダイアログを提供するボットに依存しています。</span><span class="sxs-lookup"><span data-stu-id="213ed-125">Messaging extensions rely on bots to provide a dialog between the user and your code.</span></span>

1. <span data-ttu-id="213ed-126">[プログラミング **言語] セクションで\*\*\*\*、[JavaScript] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="213ed-126">In the **Programming Language** section, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. <span data-ttu-id="213ed-128">ワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="213ed-128">Select a workspace folder.</span></span>  <span data-ttu-id="213ed-129">ワークスペース フォルダー内に、作成中のプロジェクト向けのフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="213ed-129">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="213ed-130">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="213ed-130">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="213ed-131">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="213ed-131">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="213ed-132">**Enter** キーを押して続行します。</span><span class="sxs-lookup"><span data-stu-id="213ed-132">Press **Enter** to continue.</span></span>

   <span data-ttu-id="213ed-133">数秒後に Teams アプリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="213ed-133">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="213ed-134">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="213ed-134">Command line</span></span>](#tab/cli)

<span data-ttu-id="213ed-135">`teamsfx` CLI を使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="213ed-135">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="213ed-136">プロジェクト フォルダーを作成するフォルダーから開始します。</span><span class="sxs-lookup"><span data-stu-id="213ed-136">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="213ed-137">CLI では、プロジェクトを作成するためのいくつかの質問を行います。</span><span class="sxs-lookup"><span data-stu-id="213ed-137">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="213ed-138">各質問には、回答方法 (矢印キーで選択肢を選択するなど) が記載されています。</span><span class="sxs-lookup"><span data-stu-id="213ed-138">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="213ed-139">質問に答えた後、**Enter** キーを押して選択を確認します。</span><span class="sxs-lookup"><span data-stu-id="213ed-139">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="213ed-140">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="213ed-140">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="213ed-141">[メッセージ拡張機能] **を選択し** 、[タブ] の選択を **解除します**。</span><span class="sxs-lookup"><span data-stu-id="213ed-141">Select the **Message Extension** and deselect **Tab**.</span></span>
1. <span data-ttu-id="213ed-142">**新しいボット登録の作成** を選択します。</span><span class="sxs-lookup"><span data-stu-id="213ed-142">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="213ed-143">プログラミング言語として **[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="213ed-143">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="213ed-144">**Enter** キーを押して、既定のワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="213ed-144">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="213ed-145">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="213ed-145">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="213ed-146">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="213ed-146">The name of the app must consist only of alphanumeric characters.</span></span>

   <span data-ttu-id="213ed-147">すべての質問に答えた後、プロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="213ed-147">After all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="213ed-148">ソース コードのツアーを開始する</span><span class="sxs-lookup"><span data-stu-id="213ed-148">Take a tour of the source code</span></span>

<span data-ttu-id="213ed-149">このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。</span><span class="sxs-lookup"><span data-stu-id="213ed-149">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="213ed-150">メッセージング拡張機能では、[[ボット フレームワーク]](https://docs.botframework.com) を使用して、ユーザーが会話を介してサービスと対話できるようにします。</span><span class="sxs-lookup"><span data-stu-id="213ed-150">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="213ed-151">足場を組むと、プロジェクトは以下のようになります。</span><span class="sxs-lookup"><span data-stu-id="213ed-151">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="ボット プロジェクトのファイル レイアウト":::。

<span data-ttu-id="213ed-153">ボット コードは `bot` ディレクトリに格納されています。</span><span class="sxs-lookup"><span data-stu-id="213ed-153">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="213ed-154">`bot/messageExtensionBot.js` は、メッセージング拡張機能の主な入力ポイントです。</span><span class="sxs-lookup"><span data-stu-id="213ed-154">The `bot/messageExtensionBot.js` is the main entry point for the messaging extension.</span></span>

> [!Tip]
> <span data-ttu-id="213ed-155">Teams 内で最初のボットを統合する前に、Teams 外のボットに慣れておきましょう。</span><span class="sxs-lookup"><span data-stu-id="213ed-155">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="213ed-156">ボットの詳細については、[[Azure Bot Service]](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) のチュートリアルをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="213ed-156">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="213ed-157">アプリをローカルで実行する</span><span class="sxs-lookup"><span data-stu-id="213ed-157">Run your app locally</span></span>

<span data-ttu-id="213ed-158">Teams ツールキットでは、アプリをローカルでホストすることができます。</span><span class="sxs-lookup"><span data-stu-id="213ed-158">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="213ed-159">これを行うには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="213ed-159">To do this:</span></span>

- <span data-ttu-id="213ed-160">M365 テナント内に Azure Active Directory アプリケーションが登録されています。</span><span class="sxs-lookup"><span data-stu-id="213ed-160">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="213ed-161">アプリのマニフェストをDeveloper Portal for Teams に送信します。</span><span class="sxs-lookup"><span data-stu-id="213ed-161">An app manifest is submitted to the Developer Portal for Teams.</span></span>
- <span data-ttu-id="213ed-162">API は Azure Functions Core Tools を使用してローカルで実行され、アプリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="213ed-162">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="213ed-163">[ngrok](https://ngrok.io) がインストールされ、Teams とメッセージング拡張機能の間のトンネルを指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="213ed-163">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your messaging extension.</span></span>

<span data-ttu-id="213ed-164">アプリをローカルに構築して実行するには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="213ed-164">To build and run your app locally:</span></span>

1. <span data-ttu-id="213ed-165">次Visual Studio Code **F5** キーを押して、アプリケーションをデバッグ モードで実行します。</span><span class="sxs-lookup"><span data-stu-id="213ed-165">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>

   > <span data-ttu-id="213ed-166">アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="213ed-166">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="213ed-167">ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="213ed-167">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="213ed-168">この作業には 3 ～ 5 分かかります。</span><span class="sxs-lookup"><span data-stu-id="213ed-168">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="213ed-169">Teams が Web ブラウザーに読み込まれ、サインインするようメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="213ed-169">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="213ed-170">Microsoft Teams を開くようメッセージが表示されたら、「キャンセル」を選択してブラウザーに残ります。</span><span class="sxs-lookup"><span data-stu-id="213ed-170">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="213ed-171">M365 アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="213ed-171">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="213ed-172">[ **追加] を** 選択して、アプリをアカウントに追加します。</span><span class="sxs-lookup"><span data-stu-id="213ed-172">Select **Add** to add the app to your account.</span></span>

   <span data-ttu-id="213ed-173">アプリが読み込まれた後、検索ダイアログに直接移動します。</span><span class="sxs-lookup"><span data-stu-id="213ed-173">After the app is loaded, you will be taken directly to a search dialog:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="検索ベースのメッセージング拡張機能の動作":::

   <span data-ttu-id="213ed-175">検索ボックスにテキストを入力し、オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="213ed-175">Type some text in the search box, then select one of the options.</span></span>  <span data-ttu-id="213ed-176">入力ボックスにアダプティブ カードが追加されます。</span><span class="sxs-lookup"><span data-stu-id="213ed-176">An adaptive card will be added to your input box.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="213ed-177">デバッガーでアプリをローカルに実行した場合に発生することを説明します。</span><span class="sxs-lookup"><span data-stu-id="213ed-177">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="213ed-178">**F5** キーを押すと、次のTeams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="213ed-178">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="213ed-179">アプリケーションをアプリケーションに登録Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="213ed-179">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="213ed-180">アプリケーションを"サイド ローディング" に登録Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="213ed-180">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="213ed-181">Azure Function Core Tools を使用してローカルで実行されている [アプリケーション バックエンドを開始します](/azure/azure-functions/functions-run-local?#start)。</span><span class="sxs-lookup"><span data-stu-id="213ed-181">Starts your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="213ed-182">アプリと通信Teams ngrok トンネルを開始します。</span><span class="sxs-lookup"><span data-stu-id="213ed-182">Starts an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="213ed-183">アプリケーションMicrosoft Teams読み込むようTeamsコマンドを使用して開始します。</span><span class="sxs-lookup"><span data-stu-id="213ed-183">Starts Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="213ed-184">アプリをローカルで実行する場合の一般的な問題のトラブルシューティングを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="213ed-184">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="213ed-185">Teams でアプリを正常に実行するには、アプリのサイドロードを許可する Microsoft 365 開発アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="213ed-185">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="213ed-186">アカウント開設の詳細については、「[前提条件](prerequisites.md#enable-sideloading)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="213ed-186">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="213ed-187">ツールキットに含まれる[アプリ認証ツール](https://dev.teams.microsoft.com/appvalidation.html)を使用して、アプリをサイドロードする前に問題がないか確認します。</span><span class="sxs-lookup"><span data-stu-id="213ed-187">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="213ed-188">エラーを修正して、アプリを正常にサイドロードします。</span><span class="sxs-lookup"><span data-stu-id="213ed-188">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="213ed-189">アプリを Azure に展開した場合に発生することを説明します</span><span class="sxs-lookup"><span data-stu-id="213ed-189">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="213ed-190">展開前は、このアプリケーションは以下のようにローカルで動作しています。</span><span class="sxs-lookup"><span data-stu-id="213ed-190">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="213ed-191">バックエンドは、_Azure Functions Core Tools_ を使用して実行します。</span><span class="sxs-lookup"><span data-stu-id="213ed-191">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="213ed-192">アプリケーションの HTTP エンドポイントは、Microsoft Teams がアプリケーションを読み込む場所でローカルに実行されます。</span><span class="sxs-lookup"><span data-stu-id="213ed-192">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="213ed-193">展開では、アクティブな Azure サブスクリプションにリソースをプロビジョニングし、アプリケーションのバックエンドとフロントエンドのコードを Azure に展開 (アップロード) します。</span><span class="sxs-lookup"><span data-stu-id="213ed-193">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="213ed-194">バックエンドには、Azure App Service や Azure Bot Service など、さまざまな Azure のサービスが使用されています。</span><span class="sxs-lookup"><span data-stu-id="213ed-194">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="add-a-configuration-page-to-your-messaging-extension"></a><span data-ttu-id="213ed-195">メッセージング拡張機能に構成ページを追加する</span><span class="sxs-lookup"><span data-stu-id="213ed-195">Add a configuration page to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="code-sample"></a><span data-ttu-id="213ed-196">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="213ed-196">Code sample</span></span>

<span data-ttu-id="213ed-197">Teams上GitHubサンプル プロジェクトの検索 Auth Config では、構成ページとボット サービス認証を含むメッセージング拡張機能を作成する方法[を示します](https://github.com/microsoft/BotBuilder-Samples#teams-samples)。</span><span class="sxs-lookup"><span data-stu-id="213ed-197">The Teams Search Auth Config for sample projects on GitHub, demonstrate how to create messaging extensions that include a configuration page and [Bot Service authentication](https://github.com/microsoft/BotBuilder-Samples#teams-samples).</span></span> <span data-ttu-id="213ed-198">このサンプルでは、ユーザーがサインインした後に、検索要求を受け入れ、結果を返すメッセージ拡張機能を作成する方法も示しています。</span><span class="sxs-lookup"><span data-stu-id="213ed-198">The samples also demonstrate how to create message extensions that accept search requests and return the results after the user has signed in.</span></span>

| <span data-ttu-id="213ed-199">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="213ed-199">**Sample name**</span></span> | <span data-ttu-id="213ed-200">**説明**</span><span class="sxs-lookup"><span data-stu-id="213ed-200">**Description**</span></span> | <span data-ttu-id="213ed-201">**.NET**</span><span class="sxs-lookup"><span data-stu-id="213ed-201">**.NET**</span></span> | <span data-ttu-id="213ed-202">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="213ed-202">**Node.js**</span></span> | <span data-ttu-id="213ed-203">**Python**</span><span class="sxs-lookup"><span data-stu-id="213ed-203">**Python**</span></span> |
|-----------------|-----------------|-------------|--------------|--------|
| <span data-ttu-id="213ed-204">ボット ビルダー</span><span class="sxs-lookup"><span data-stu-id="213ed-204">Bot builder</span></span> | <span data-ttu-id="213ed-205">メッセージング拡張機能を作成するには。</span><span class="sxs-lookup"><span data-stu-id="213ed-205">To create messaging extensions.</span></span> | [<span data-ttu-id="213ed-206">View</span><span class="sxs-lookup"><span data-stu-id="213ed-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="213ed-207">View</span><span class="sxs-lookup"><span data-stu-id="213ed-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) | [<span data-ttu-id="213ed-208">View</span><span class="sxs-lookup"><span data-stu-id="213ed-208">View</span></span>]( https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="additional-code-sample"></a><span data-ttu-id="213ed-209">追加のコード サンプル</span><span class="sxs-lookup"><span data-stu-id="213ed-209">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="213ed-210">ボット フレームワークのサンプルを表示する GitHub</span><span class="sxs-lookup"><span data-stu-id="213ed-210">View more Bot Framework Samples on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-samples#messaging-extensions-samples-using-the-v4-sdk)

## <a name="see-also"></a><span data-ttu-id="213ed-211">関連項目</span><span class="sxs-lookup"><span data-stu-id="213ed-211">See also</span></span>

* [<span data-ttu-id="213ed-212">チュートリアルの概要</span><span class="sxs-lookup"><span data-stu-id="213ed-212">Tutorials Overview</span></span>](code-samples.md) 
* [<span data-ttu-id="213ed-213">アプリを使用してアプリを作成React</span><span class="sxs-lookup"><span data-stu-id="213ed-213">Create an app using React</span></span>](first-app-react.md)
* [<span data-ttu-id="213ed-214">Blazor を使用してアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="213ed-214">Create an app using Blazor</span></span>](first-app-blazor.md)
* [<span data-ttu-id="213ed-215">アプリを使用してアプリを作成SPFx</span><span class="sxs-lookup"><span data-stu-id="213ed-215">Create an app using SPFx</span></span>](first-app-spfx.md)
* [<span data-ttu-id="213ed-216">C# を使用してアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="213ed-216">Create an app using C# or .NET</span></span>](get-started-dotnet-app-studio.md)
* [<span data-ttu-id="213ed-217">Node.js を使ってアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="213ed-217">Create an app using Node.js</span></span>](get-started-nodejs-app-studio.md)
* [<span data-ttu-id="213ed-218">Yeoman ジェネレーターを使用してアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="213ed-218">Create an app using Yeoman generator</span></span>](get-started-yeoman.md)
* [<span data-ttu-id="213ed-219">会話ボット アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="213ed-219">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="213ed-220">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="213ed-220">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)