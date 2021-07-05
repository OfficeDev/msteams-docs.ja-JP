---
title: 使用を開始する - 最初の会話型ボットのビルド
author: adrianhall
description: Teams ツールキットを使用して、Microsoft Teams の会話ボットを作成します。
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: 96bbddd99b6901a4b92e1e2f2dc98482c755dc66
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254252"
---
# <a name="build-your-first-conversational-bot-for-microsoft-teams"></a><span data-ttu-id="7674c-103">Microsoft Teams 用の会話型ボットをビルドする</span><span class="sxs-lookup"><span data-stu-id="7674c-103">Build your first conversational bot for Microsoft Teams</span></span>

<span data-ttu-id="7674c-104">このチュートリアルでは、Teams ボット アプリを構築し、実行し、展開する方法を学びます。</span><span class="sxs-lookup"><span data-stu-id="7674c-104">In this tutorial, you will learn how to build, run, and deploy a Teams bot app.</span></span> <span data-ttu-id="7674c-105">ボットは、Teams ユーザーと Web サービスの間を仲介する役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="7674c-105">A bot acts as an intermediary between a Teams user and a web service.</span></span>  <span data-ttu-id="7674c-106">ユーザーは、ボットとチャットすることで、情報を素早く入手したり、ワークフローを開始したり、Web サービスに可能なすべてのことができます。</span><span class="sxs-lookup"><span data-stu-id="7674c-106">Users can chat with a bot to quickly get information, initiate workflows, or anything else your web service can do.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="7674c-107">はじめに</span><span class="sxs-lookup"><span data-stu-id="7674c-107">Before you begin</span></span>

<span data-ttu-id="7674c-108">前提条件をインストールして、開発環境がセットアップされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="7674c-108">Make sure your development environment is set up by installing the Prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7674c-109">前提条件のインストール</span><span class="sxs-lookup"><span data-stu-id="7674c-109">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="7674c-110">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="7674c-110">Create your project</span></span>

<span data-ttu-id="7674c-111">Teams ツールキットを使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="7674c-111">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="7674c-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7674c-112">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="7674c-113">Visual Studio Code を開きます。</span><span class="sxs-lookup"><span data-stu-id="7674c-113">Open Visual Studio code.</span></span>
1. <span data-ttu-id="7674c-114">サイドバーのTeamsアイコンを選択して、ウィンドウを開Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="7674c-114">Select the Teams icon in the sidebar to open the Teams Toolkit.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code サイド バーの Teams アイコン":::。

1. <span data-ttu-id="7674c-116">**[新しいプロジェクトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7674c-116">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams ツールキットのサイド バーにある [新しいプロジェクトの作成] リンクの位置":::。

1. <span data-ttu-id="7674c-118">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7674c-118">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="[新しいプロジェクトの作成] のウィザードの開始":::。

1. <span data-ttu-id="7674c-120">[機能の **選択] セクションで**、[ボット] を選択 **し、[タブ**] の選択を **解除し\*\*\*\*、[OK] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="7674c-120">In the **Select capabilities** section, select **Bot**, deselect **Tab** and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="新しいアプリに機能を追加する方法を示すスクリーンショット":::。

1. <span data-ttu-id="7674c-122">[ボット登録 **] セクションで** 、[新しい **ボット登録の作成] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="7674c-122">In the **Bot registration** section, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="新しいボット登録の作成を選択する":::

1. <span data-ttu-id="7674c-124">[プログラミング **言語] セクションで\*\*\*\*、[JavaScript] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="7674c-124">In the **Programming Language** section, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="プログラミング言語を選択する方法のスクリーンショット":::

1. <span data-ttu-id="7674c-126">ワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="7674c-126">Select a workspace folder.</span></span>  <span data-ttu-id="7674c-127">ワークスペース フォルダー内に、作成中のプロジェクト向けのフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="7674c-127">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="7674c-128">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="7674c-128">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="7674c-129">アプリの名前には、英数字のみを含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="7674c-129">The name of the app must contain only alphanumeric characters.</span></span>  <span data-ttu-id="7674c-130">**Enter** キーを押して続行します。</span><span class="sxs-lookup"><span data-stu-id="7674c-130">Press **Enter** to continue.</span></span>

<span data-ttu-id="7674c-131">数秒後に Teams アプリが作成されます。</span><span class="sxs-lookup"><span data-stu-id="7674c-131">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="7674c-132">コマンド ライン</span><span class="sxs-lookup"><span data-stu-id="7674c-132">Command line</span></span>](#tab/cli)

<span data-ttu-id="7674c-133">`teamsfx` CLI を使用して、最初のプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="7674c-133">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="7674c-134">プロジェクト フォルダーを作成するフォルダーから開始します。</span><span class="sxs-lookup"><span data-stu-id="7674c-134">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="7674c-135">CLI では、プロジェクトを作成するためのいくつかの質問を行います。</span><span class="sxs-lookup"><span data-stu-id="7674c-135">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="7674c-136">各質問には、回答方法 (矢印キーで選択肢を選択するなど) が記載されています。</span><span class="sxs-lookup"><span data-stu-id="7674c-136">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="7674c-137">質問に答えた後、**Enter** キーを押して選択を確認します。</span><span class="sxs-lookup"><span data-stu-id="7674c-137">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="7674c-138">**[新しい Teams アプリを作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7674c-138">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="7674c-139">[ボット **] を選択し** 、[タブ] の **選択を解除します**。</span><span class="sxs-lookup"><span data-stu-id="7674c-139">Select **Bot** and deselect **Tab**.</span></span>
1. <span data-ttu-id="7674c-140">**新しいボット登録の作成** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7674c-140">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="7674c-141">プログラミング言語として **[JavaScript]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7674c-141">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="7674c-142">**Enter** キーを押して、既定のワークスペース フォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="7674c-142">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="7674c-143">`helloworld` のように、アプリに適した名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="7674c-143">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="7674c-144">アプリの名前は、英数字のみで構成されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="7674c-144">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="7674c-145">すべての質問に答えた後、プロジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="7674c-145">After all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="7674c-146">ソース コードのツアーを開始する</span><span class="sxs-lookup"><span data-stu-id="7674c-146">Take a tour of the source code</span></span>

<span data-ttu-id="7674c-147">このセクションをスキップしたい場合は、[アプリをローカルで実行する](#run-your-app-locally)ことができます。</span><span class="sxs-lookup"><span data-stu-id="7674c-147">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="7674c-148">メッセージング拡張機能では、[[ボット フレームワーク]](https://docs.botframework.com) を使用して、ユーザーが会話を介してサービスと対話できるようにします。</span><span class="sxs-lookup"><span data-stu-id="7674c-148">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="7674c-149">足場を組むと、プロジェクトは以下のようになります。</span><span class="sxs-lookup"><span data-stu-id="7674c-149">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="ボット プロジェクトのファイル レイアウト":::。

<span data-ttu-id="7674c-151">ボット コードは `bot` ディレクトリに格納されています。</span><span class="sxs-lookup"><span data-stu-id="7674c-151">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="7674c-152">`bot/teamsBot.js` はボットの主な入力ポイントで、ダイアログは `dialogs` ディレクトリに格納されます。</span><span class="sxs-lookup"><span data-stu-id="7674c-152">The `bot/teamsBot.js` is the main entry point for the bot, and the dialogs are stored in the `dialogs` directory.</span></span>

> [!Tip]
> <span data-ttu-id="7674c-153">Teams 内で最初のボットを統合する前に、Teams 外のボットに慣れておきましょう。</span><span class="sxs-lookup"><span data-stu-id="7674c-153">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="7674c-154">ボットの詳細については、[[Azure Bot Service]](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) のチュートリアルをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="7674c-154">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="7674c-155">アプリをローカルで実行する</span><span class="sxs-lookup"><span data-stu-id="7674c-155">Run your app locally</span></span>

<span data-ttu-id="7674c-156">Teams ツールキットでは、アプリをローカルでホストすることができます。</span><span class="sxs-lookup"><span data-stu-id="7674c-156">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="7674c-157">これを行うには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="7674c-157">To do this:</span></span>

- <span data-ttu-id="7674c-158">M365 テナント内に Azure Active Directory アプリケーションが登録されています。</span><span class="sxs-lookup"><span data-stu-id="7674c-158">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="7674c-159">アプリのマニフェストを Teams の開発者センターに送信します。</span><span class="sxs-lookup"><span data-stu-id="7674c-159">An app manifest is submitted to the Developer Center for Teams.</span></span>
- <span data-ttu-id="7674c-160">API は Azure Functions Core Tools を使用してローカルで実行され、アプリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="7674c-160">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="7674c-161">[ngrok](https://ngrok.io) がインストールされ、Teams とボット コードの間のトンネルを指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="7674c-161">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your bot code.</span></span>

<span data-ttu-id="7674c-162">アプリをローカルに構築して実行するには、以下のようにします。</span><span class="sxs-lookup"><span data-stu-id="7674c-162">To build and run your app locally:</span></span>

1. <span data-ttu-id="7674c-163">次Visual Studio Code **F5** キーを押して、アプリケーションをデバッグ モードで実行します。</span><span class="sxs-lookup"><span data-stu-id="7674c-163">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>

   > <span data-ttu-id="7674c-164">アプリを初めて実行すると、すべての依存関係がダウンロードされ、アプリがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="7674c-164">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="7674c-165">ビルドが完了すると、自動的にブラウザー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="7674c-165">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="7674c-166">この作業には 3 ～ 5 分かかります。</span><span class="sxs-lookup"><span data-stu-id="7674c-166">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="7674c-167">Web ブラウザーがアプリの実行を開始します。</span><span class="sxs-lookup"><span data-stu-id="7674c-167">Your web browser starts to run the app.</span></span> <span data-ttu-id="7674c-168">デスクトップを開くTeams場合は、[キャンセル] を **選択して** ブラウザーに残ります。</span><span class="sxs-lookup"><span data-stu-id="7674c-168">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="7674c-169">また、他の場合はデスクトップに切り替Teams表示される場合があります。この場合Teams Web アプリを選択します。</span><span class="sxs-lookup"><span data-stu-id="7674c-169">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="起動時に Web 版のチームを選択する方法を示すスクリーンショット":::

1. <span data-ttu-id="7674c-171">サインインするように求めるメッセージが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="7674c-171">You may be prompted to sign in.</span></span>  <span data-ttu-id="7674c-172">その場合は、M365 アカウントを使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="7674c-172">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="7674c-173">アプリをインストールするように求めるメッセージが表示されたら、[Teams] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="7674c-173">When prompted to install the app onto Teams, select **Add**.</span></span>

   <span data-ttu-id="7674c-174">アプリが読み込まれた後、ボットとのチャット セッションに直接アクセスします。</span><span class="sxs-lookup"><span data-stu-id="7674c-174">After the app is loaded, you will be taken directly to a chat session with the bot.</span></span>  <span data-ttu-id="7674c-175">`intro` を入力すると紹介カードが表示され、`show` を入力すると Microsoft Graph からユーザーの詳細情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7674c-175">You can type `intro` to show an introduction card, and `show` to show your details from Microsoft Graph.</span></span>  <span data-ttu-id="7674c-176">(これには追加で許可の承認が必要です)。</span><span class="sxs-lookup"><span data-stu-id="7674c-176">(This will require an additional permissions approval).</span></span>

   <span data-ttu-id="7674c-177">デバッグは通常通りに動作します。実際にお試しください。</span><span class="sxs-lookup"><span data-stu-id="7674c-177">Debugging works as you normally would expect - try it yourself!</span></span> <span data-ttu-id="7674c-178">`bot/dialogs/rootDialog.js` ファイルを開き、`triggerCommand(...)` メソッドを探します。</span><span class="sxs-lookup"><span data-stu-id="7674c-178">Open the `bot/dialogs/rootDialog.js` file and locate the `triggerCommand(...)` method.</span></span>  <span data-ttu-id="7674c-179">既定のケースにブレークポイントを設定します。</span><span class="sxs-lookup"><span data-stu-id="7674c-179">Set a breakpoint on the default case.</span></span>  <span data-ttu-id="7674c-180">次に、テキストを入力します。</span><span class="sxs-lookup"><span data-stu-id="7674c-180">Then type some text.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="7674c-181">デバッガーでアプリをローカルに実行した場合に発生することを説明します。</span><span class="sxs-lookup"><span data-stu-id="7674c-181">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="7674c-182">**F5** キーを押すと、次のTeams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="7674c-182">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="7674c-183">アプリケーションをアプリケーションに登録Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="7674c-183">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="7674c-184">アプリケーションを"サイド ローディング" に登録Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="7674c-184">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="7674c-185">Azure Function Core Tools を使用してローカルで実行されている [アプリケーション バックエンドを開始します](/azure/azure-functions/functions-run-local?#start)。</span><span class="sxs-lookup"><span data-stu-id="7674c-185">Starts your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="7674c-186">アプリと通信Teams ngrok トンネルを開始します。</span><span class="sxs-lookup"><span data-stu-id="7674c-186">Starts an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="7674c-187">アプリケーションMicrosoft Teams読み込むようTeamsコマンドを使用して開始します。</span><span class="sxs-lookup"><span data-stu-id="7674c-187">Starts Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="7674c-188">アプリをローカルで実行する場合の一般的な問題のトラブルシューティングを行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7674c-188">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="7674c-189">Teams でアプリを正常に実行するには、アプリのサイドロードを許可する Microsoft 365 開発アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="7674c-189">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="7674c-190">アカウント開設の詳細については、「[前提条件](prerequisites.md#enable-sideloading)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7674c-190">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="7674c-191">ツールキットに含まれる[アプリ認証ツール](https://dev.teams.microsoft.com/appvalidation.html)を使用して、アプリをサイドロードする前に問題がないか確認します。</span><span class="sxs-lookup"><span data-stu-id="7674c-191">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="7674c-192">エラーを修正して、アプリを正常にサイドロードします。</span><span class="sxs-lookup"><span data-stu-id="7674c-192">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="7674c-193">アプリを Azure に展開した場合に発生することを説明します</span><span class="sxs-lookup"><span data-stu-id="7674c-193">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="7674c-194">展開前は、このアプリケーションは以下のようにローカルで動作しています。</span><span class="sxs-lookup"><span data-stu-id="7674c-194">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="7674c-195">バックエンドは、_Azure Functions Core Tools_ を使用して実行します。</span><span class="sxs-lookup"><span data-stu-id="7674c-195">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="7674c-196">アプリケーションの HTTP エンドポイントは、Microsoft Teams がアプリケーションを読み込む場所でローカルに実行されます。</span><span class="sxs-lookup"><span data-stu-id="7674c-196">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

   <span data-ttu-id="7674c-197">展開では、アクティブな Azure サブスクリプションにリソースをプロビジョニングし、アプリケーションのバックエンドとフロントエンドのコードを Azure に展開 (アップロード) します。</span><span class="sxs-lookup"><span data-stu-id="7674c-197">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="7674c-198">バックエンドには、Azure App Service や Azure Bot Service など、さまざまな Azure のサービスが使用されています。</span><span class="sxs-lookup"><span data-stu-id="7674c-198">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="7674c-199">関連項目</span><span class="sxs-lookup"><span data-stu-id="7674c-199">See also</span></span>

* [<span data-ttu-id="7674c-200">チュートリアルの概要</span><span class="sxs-lookup"><span data-stu-id="7674c-200">Tutorials Overview</span></span>](code-samples.md) 
* [<span data-ttu-id="7674c-201">アプリを使用してアプリを作成React</span><span class="sxs-lookup"><span data-stu-id="7674c-201">Create an app using React</span></span>](first-app-react.md)
* [<span data-ttu-id="7674c-202">Blazor を使用してアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="7674c-202">Create an app using Blazor</span></span>](first-app-blazor.md)
* [<span data-ttu-id="7674c-203">アプリを使用してアプリを作成SPFx</span><span class="sxs-lookup"><span data-stu-id="7674c-203">Create an app using SPFx</span></span>](first-app-spfx.md)
* [<span data-ttu-id="7674c-204">C# を使用してアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="7674c-204">Create an app using C# or .NET</span></span>](get-started-dotnet-app-studio.md)
* [<span data-ttu-id="7674c-205">Node.js を使ってアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="7674c-205">Create an app using Node.js</span></span>](get-started-nodejs-app-studio.md)
* [<span data-ttu-id="7674c-206">Yeoman ジェネレーターを使用してアプリを作成する</span><span class="sxs-lookup"><span data-stu-id="7674c-206">Create an app using Yeoman generator</span></span>](get-started-yeoman.md)
* [<span data-ttu-id="7674c-207">メッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="7674c-207">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="7674c-208">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="7674c-208">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)