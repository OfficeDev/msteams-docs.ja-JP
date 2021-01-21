---
title: 開始する - メッセージング拡張機能を構築する
author: heath-hamilton
description: Microsoft Teams を使用して、Microsoft Teams メッセージング拡張機能をすばやく作成Toolkit。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 86d44740feaa2cd33aff0e1dde14d757420d90d6
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911920"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="36e82-103">Microsoft Teams のメッセージング拡張機能を構築する</span><span class="sxs-lookup"><span data-stu-id="36e82-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="36e82-104">Teams アプリのメッセージング拡張機能には、検索コマンド *と* アクション コマンドの 2 [種類](../messaging-extensions/how-to/search-commands/define-search-command.md)[があります](../messaging-extensions/how-to/action-commands/define-action-command.md)。</span><span class="sxs-lookup"><span data-stu-id="36e82-104">There are two types of Teams app *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="36e82-105">このレッスンでは、外部コンテンツを検索して Teams で共有するショートカットである検索コマンド *(検索* ベースのメッセージング拡張機能とも呼ばれる) を作成します。</span><span class="sxs-lookup"><span data-stu-id="36e82-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="36e82-106">ユーザーは、Teams の作成またはコマンド ボックス [から検索コマンドにアクセスできます](../messaging-extensions/what-are-messaging-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="36e82-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="36e82-107">割り当て</span><span class="sxs-lookup"><span data-stu-id="36e82-107">Your assignment</span></span>

<span data-ttu-id="36e82-108">組織のヘルプ デスクは Teams を通じてユーザーと通信しますが、チケットは別のシステムに存在します。</span><span class="sxs-lookup"><span data-stu-id="36e82-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="36e82-109">つまり、サポート スタッフは常にアプリ間を行き来する必要があります。</span><span class="sxs-lookup"><span data-stu-id="36e82-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="36e82-110">Teams の単純な検索ベースのメッセージング拡張機能を作成することで、このようなコンテキスト切り替えの量を減らす方法を調査します。</span><span class="sxs-lookup"><span data-stu-id="36e82-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="36e82-111">学習する情報</span><span class="sxs-lookup"><span data-stu-id="36e82-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="36e82-112">Microsoft Teams Toolkit for Visual Studio Code を使用してアプリ プロジェクトとメッセージング拡張機能ボットを作成する</span><span class="sxs-lookup"><span data-stu-id="36e82-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="36e82-113">アプリの構成とメッセージング拡張機能に関連するスキャフォールディングの一部を特定する</span><span class="sxs-lookup"><span data-stu-id="36e82-113">Identify the app configurations and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="36e82-114">アプリをローカルでホストする</span><span class="sxs-lookup"><span data-stu-id="36e82-114">Host an app locally</span></span>
> * <span data-ttu-id="36e82-115">メッセージング拡張機能用にボットを構成する</span><span class="sxs-lookup"><span data-stu-id="36e82-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="36e82-116">Teams でメッセージング拡張機能をサイドロードしてテストする</span><span class="sxs-lookup"><span data-stu-id="36e82-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="36e82-117">はじめに</span><span class="sxs-lookup"><span data-stu-id="36e82-117">Before you begin</span></span>

<span data-ttu-id="36e82-118">まだ理解していない場合は、Teams 開発の前提条件 [を理解してインストールしてください](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="36e82-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="36e82-119">1. アプリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="36e82-119">1. Create your app project</span></span>

<span data-ttu-id="36e82-120">Microsoft Teams Toolkitは、メッセージング拡張機能用に次のコンポーネントを設定するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="36e82-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="36e82-121">**メッセージング拡張機能に関連するアプリ** の構成とスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="36e82-121">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="36e82-122"> Microsoft Azure Bot Service に自動的に登録されるメッセージング拡張機能のボット</span><span class="sxs-lookup"><span data-stu-id="36e82-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="36e82-123">Teams アプリ プロジェクトをまだ作成していない場合は、プロジェクトについて詳しく説明する次[](../build-your-first-app/build-and-run.md)の手順に従うのが役に立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="36e82-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. [Visual Studioコード] で、左側のアクティビティ バーで **Microsoft Teams** を選択し、[新しい Teams アプリの作成 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: ] **を選択します**。
1. <span data-ttu-id="36e82-125">ダイアログが表示されたら、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="36e82-125">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="36e82-126">[機能 **の追加] 画面で、[\*\*\*\*メッセージング拡張機能]** を選択し、[次へ] を **選択します**。</span><span class="sxs-lookup"><span data-stu-id="36e82-126">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="36e82-127">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="36e82-127">Enter a name for your Teams app.</span></span> <span data-ttu-id="36e82-128">(これは、アプリの既定の名前と、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です)。</span><span class="sxs-lookup"><span data-stu-id="36e82-128">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="36e82-129">[メッセージング **拡張機能の構成] 画面で** 、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="36e82-129">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="36e82-130">メッセージング拡張機能 **の種類に対して** 検索ベースのオプションのみを選択します。</span><span class="sxs-lookup"><span data-stu-id="36e82-130">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="36e82-131">[新 **しいボットの作成] を選択し、[\*\*\*\*ボット登録の作成] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="36e82-131">Select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="36e82-132">成功した場合、新しいボットの状態は **登録済み** になります。</span><span class="sxs-lookup"><span data-stu-id="36e82-132">If successful, your new bot will have a **Registered** status.</span></span>
    1. <span data-ttu-id="36e82-133">ここで、リンクの **分岐オプション** として [いいえ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="36e82-133">For now, select **No** for the link unfurling option.</span></span>
1. <span data-ttu-id="36e82-134">画面 **の** 下部にある [完了] を選択して、プロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="36e82-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="36e82-135">2. 関連するアプリ プロジェクト コンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="36e82-135">2. Identify relevant app project components</span></span>

<span data-ttu-id="36e82-136">アプリの構成とスキャフォールディングの多くが、Teams アプリを使用してプロジェクトを作成するときに自動的に設定Toolkit。</span><span class="sxs-lookup"><span data-stu-id="36e82-136">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="36e82-137">アプリの構成</span><span class="sxs-lookup"><span data-stu-id="36e82-137">App configurations</span></span>

<span data-ttu-id="36e82-138">メッセージング拡張機能の構成を表示または更新するには、ツールキットで **App Studio** を選択し、 **メッセージング拡張機能に移動します**。</span><span class="sxs-lookup"><span data-stu-id="36e82-138">To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="36e82-139">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="36e82-139">App scaffolding</span></span>

<span data-ttu-id="36e82-140">アプリのスキャフォールディングは、メッセージング拡張機能 (または技術的にはメッセージング拡張機能のボット) が Teams の検索クエリに応答する方法を処理するために、プロジェクトのルート ディレクトリにあるファイルを提供します。 `botActivityHandler.js` [](#4-configure-the-bot-for-your-messaging-extension)</span><span class="sxs-lookup"><span data-stu-id="36e82-140">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="36e82-141">3. アプリへのセキュリティで保護されたトンネルを設定する</span><span class="sxs-lookup"><span data-stu-id="36e82-141">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="36e82-142">テストの目的で、メッセージング拡張機能をローカル Web サーバー (ポート 3978) でホストします。</span><span class="sxs-lookup"><span data-stu-id="36e82-142">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="36e82-143">まだインストールしていない場合は [、ngrok をインストールします](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="36e82-143">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="36e82-144">ターミナルで、次を実行します `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="36e82-144">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="36e82-145">Teams は HTTPS 接続を必要としますので、出力内の HTTPS URL (たとえば `https://468b9ab725e9.ngrok.io` ) をコピーします。</span><span class="sxs-lookup"><span data-stu-id="36e82-145">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="36e82-146">この URL を使用すると、Teams (HTTPS 接続が必要) は、アプリをホストしている場所 (ポート `localhost` 3978) にトンネリングできます。</span><span class="sxs-lookup"><span data-stu-id="36e82-146">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="36e82-147">4. メッセージング拡張機能用にボットを構成する</span><span class="sxs-lookup"><span data-stu-id="36e82-147">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="36e82-148">メッセージング拡張機能はボットに依存して、Teams からホストされたサービスにユーザー要求を送信および処理します。</span><span class="sxs-lookup"><span data-stu-id="36e82-148">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="36e82-149">ボットは Azure Bot Service に登録する必要があります。このサービスは、Teams サービスを使用してアプリをセットアップToolkit。</span><span class="sxs-lookup"><span data-stu-id="36e82-149">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="36e82-150">メッセージング拡張機能で検索クエリを受信および処理するには、ボット エンドポイント URL を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="36e82-150">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="36e82-151">通常、URL は次のように表示されます `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="36e82-151">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="36e82-152">この設定は、ツールキットですばやく構成できます。</span><span class="sxs-lookup"><span data-stu-id="36e82-152">You can configure this quickly in the toolkit.</span></span>

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Open Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **Toolkit.**
1. <span data-ttu-id="36e82-154">既存の **ボット登録>ボットに移動し** 、セットアップ時に作成したボットを選択します。</span><span class="sxs-lookup"><span data-stu-id="36e82-154">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="36e82-155">[Bot **endpoint address]** フィールドに、ボットをホストしている ngrok URL (たとえば) を入力し、 `https://468b9ab725e9.ngrok.io` ボットに `/api/messages` 追加します。</span><span class="sxs-lookup"><span data-stu-id="36e82-155">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

<span data-ttu-id="36e82-156">ボットはメッセージング拡張機能でクエリを処理できます。</span><span class="sxs-lookup"><span data-stu-id="36e82-156">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="36e82-157">5. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="36e82-157">5. Build and run your app</span></span>

<span data-ttu-id="36e82-158">メッセージング拡張機能をホストする URL を設定し、検索を処理するように構成しました。</span><span class="sxs-lookup"><span data-stu-id="36e82-158">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="36e82-159">次に、アプリを起動して実行します。</span><span class="sxs-lookup"><span data-stu-id="36e82-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="36e82-160">ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、実行します `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="36e82-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="36e82-161">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="36e82-161">Run `npm start`.</span></span>

<span data-ttu-id="36e82-162">成功した場合は、メッセージング拡張機能サービスが自分のアクティビティをリッスン中であることを示す次のメッセージが表示されます `localhost` 。</span><span class="sxs-lookup"><span data-stu-id="36e82-162">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="36e82-163">6. Teams でメッセージング拡張機能をサイドロードする</span><span class="sxs-lookup"><span data-stu-id="36e82-163">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="36e82-164">メッセージング拡張機能を実行すると、Teams にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="36e82-164">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="36e82-165">以前に Teams アプリをサイドローディングして問題が発生していない場合は、次の手順に [従います](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="36e82-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="36e82-166">コードVisual Studio **F5** キーを押して、Teams Web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="36e82-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="36e82-167">アプリのインストール ダイアログで、[追加] **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="36e82-167">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="36e82-168">7. メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="36e82-168">7. Test your messaging extension</span></span>

<span data-ttu-id="36e82-169">Teams チャットでのメッセージング拡張機能の動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="36e82-169">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="36e82-170">新しいチャットを開始します。</span><span class="sxs-lookup"><span data-stu-id="36e82-170">Start a new chat.</span></span> 作成ボックスで [その他] **を** 選択し、サイドローディングした :::image type="icon" source="../assets/icons/teams-client-more.png"::: メッセージング拡張機能アプリを選択します。
1. <span data-ttu-id="36e82-172">何か (チケットなど) を **検索してみてください**。</span><span class="sxs-lookup"><span data-stu-id="36e82-172">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="36e82-173">アプリが動作している場合は、サンプルの検索結果が表示されます (後で独自の検索結果を追加できます)。</span><span class="sxs-lookup"><span data-stu-id="36e82-173">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Teams の作成ボックスで検索ベースのメッセージング拡張機能がどのように使用されるのか示すスクリーンショット。":::

## <a name="well-done"></a><span data-ttu-id="36e82-175">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="36e82-175">Well done</span></span>

<span data-ttu-id="36e82-176">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="36e82-176">Congratulations!</span></span> <span data-ttu-id="36e82-177">作成ボックスまたはコマンド ボックスで外部コンテンツを検索するように設定されている基本的な Teams メッセージング拡張機能があります。</span><span class="sxs-lookup"><span data-stu-id="36e82-177">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36e82-178">次の手順</span><span class="sxs-lookup"><span data-stu-id="36e82-178">Next steps</span></span>

<span data-ttu-id="36e82-179">すべての機能を備ったメッセージング拡張機能を続行して構築するには、次のページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="36e82-179">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="36e82-180">[サービスに関連する](../messaging-extensions/how-to/search-commands/define-search-command.md) 検索コマンドを定義します。</span><span class="sxs-lookup"><span data-stu-id="36e82-180">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="36e82-181">ユーザーの検索に [応答するサービスを構成します](../messaging-extensions/how-to/search-commands/respond-to-search.md)。</span><span class="sxs-lookup"><span data-stu-id="36e82-181">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="36e82-182">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="36e82-182">Troubleshooting</span></span>

<span data-ttu-id="36e82-183">このチュートリアルを完了する上で問題が発生した場合は、次の情報が役立つ場合があります。</span><span class="sxs-lookup"><span data-stu-id="36e82-183">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="36e82-184">ボットが Teams に接続されていない</span><span class="sxs-lookup"><span data-stu-id="36e82-184">Bot isn't connected to Teams</span></span>

<span data-ttu-id="36e82-185">アプリをインストールしたが動作しない場合は、メッセージング拡張機能のボットが Azure Bot Service の Teams チャネルに接続 [されていることを確認 *します*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="36e82-185">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="36e82-186">これは Teams のチャネルと同じではないという点を理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="36e82-186">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="36e82-187">この場合、チャネルは、Azure Bot Service がボットを Teams または別のサポートされている Microsoft またはサード パーティ通信アプリに接続 [する方法です](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="36e82-187">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="36e82-188">詳細情報</span><span class="sxs-lookup"><span data-stu-id="36e82-188">Learn more</span></span>

* [<span data-ttu-id="36e82-189">リンクの分岐機能を含める</span><span class="sxs-lookup"><span data-stu-id="36e82-189">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* <span data-ttu-id="36e82-190">設計ガイドライン [に従い](../messaging-extensions/design/messaging-extension-design.md) 、実稼働対応 [の UI](../concepts/design/design-teams-app-ui-templates.md) テンプレートを使用してビルドし、シームレスなエクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="36e82-190">Follow our [design guidelines](../messaging-extensions/design/messaging-extension-design.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="36e82-191">認証を追加する</span><span class="sxs-lookup"><span data-stu-id="36e82-191">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="36e82-192">アクション ベースのメッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="36e82-192">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="36e82-193">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="36e82-193">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
