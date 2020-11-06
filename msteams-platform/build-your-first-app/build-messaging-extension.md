---
title: まず、メッセージング拡張機能を構築する
author: heath-hamilton
description: Microsoft Teams ツールキットを使用して、Microsoft Teams メッセージング拡張機能をすばやく作成できます。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 160878d92969d57680e6fa25eb6fc13e82bf2a82
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931751"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="3ac87-103">Microsoft Teams のメッセージング拡張機能を構築する</span><span class="sxs-lookup"><span data-stu-id="3ac87-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="3ac87-104">Teams アプリケーション *メッセージング拡張機能* には、 [検索コマンド](../messaging-extensions/how-to/search-commands/define-search-command.md) と [アクションコマンド](../messaging-extensions/how-to/action-commands/define-action-command.md)の2種類があります。</span><span class="sxs-lookup"><span data-stu-id="3ac87-104">There are two types of Teams app *messaging extensions* : [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="3ac87-105">このレッスンでは、 *検索コマンド* ( *検索ベースのメッセージング拡張機能* とも呼ばれます) を作成します。これは、外部コンテンツを検索して Teams で共有するためのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="3ac87-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension* ), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="3ac87-106">ユーザーは、[ [Teams の作成] または [コマンド] ボックス](../messaging-extensions/what-are-messaging-extensions.md)から検索コマンドにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="3ac87-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="3ac87-107">自分の割り当て</span><span class="sxs-lookup"><span data-stu-id="3ac87-107">Your assignment</span></span>

<span data-ttu-id="3ac87-108">組織のヘルプデスクは Teams を通じてユーザーと通信しますが、チケットは別のシステムに存在します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="3ac87-109">これは、サポートスタッフが常にアプリ間を行き来する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="3ac87-110">Teams の簡単な検索ベースのメッセージング拡張機能を作成することによって、この大幅な切り替えを減らす方法を調査します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="3ac87-111">学習内容</span><span class="sxs-lookup"><span data-stu-id="3ac87-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="3ac87-112">Microsoft Teams Toolkit for Visual Studio Code を使用して、アプリプロジェクトとメッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="3ac87-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="3ac87-113">メッセージング拡張機能に関連するアプリ構成と一部のスキャフォールディングを特定する</span><span class="sxs-lookup"><span data-stu-id="3ac87-113">Identify the app configurations and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="3ac87-114">アプリをローカルでホストする</span><span class="sxs-lookup"><span data-stu-id="3ac87-114">Host an app locally</span></span>
> * <span data-ttu-id="3ac87-115">メッセージング拡張機能の bot を構成する</span><span class="sxs-lookup"><span data-stu-id="3ac87-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="3ac87-116">Teams でメッセージング拡張機能をサイドロードおよびテストする</span><span class="sxs-lookup"><span data-stu-id="3ac87-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3ac87-117">はじめに</span><span class="sxs-lookup"><span data-stu-id="3ac87-117">Before you begin</span></span>

<span data-ttu-id="3ac87-118">まだお持ちでない場合は、 [Teams 開発の前提条件を理解し、インストール](build-first-app-overview.md#get-prerequisites)してください。</span><span class="sxs-lookup"><span data-stu-id="3ac87-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="3ac87-119">1. アプリプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-119">1. Create your app project</span></span>

<span data-ttu-id="3ac87-120">Microsoft Teams Toolkit は、メッセージング拡張機能に次のコンポーネントをセットアップするのに役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="3ac87-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="3ac87-121">メッセージング拡張機能に関連する **アプリの構成とスキャフォールディング**</span><span class="sxs-lookup"><span data-stu-id="3ac87-121">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="3ac87-122">Microsoft Azure Bot サービスに自動的に登録されるメッセージング拡張機能の **Bot**</span><span class="sxs-lookup"><span data-stu-id="3ac87-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="3ac87-123">以前に Teams アプリプロジェクトを作成していない場合は、 [以下の手順](../build-your-first-app/build-and-run.md) に従って、プロジェクトについて詳しく説明することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="3ac87-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成** ] を選択します。
1. <span data-ttu-id="3ac87-125">メッセージが表示されたら、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="3ac87-125">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="3ac87-126">[ **機能の追加** ] 画面で、[ **メッセージング内線番号** ] を選択し、[ **次へ** ] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3ac87-126">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="3ac87-127">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-127">Enter a name for your Teams app.</span></span> <span data-ttu-id="3ac87-128">(これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)</span><span class="sxs-lookup"><span data-stu-id="3ac87-128">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="3ac87-129">[ **メッセージング拡張機能の構成** ] 画面で、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="3ac87-129">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="3ac87-130">メッセージング拡張機能の種類に対して **検索ベース** のオプションのみを選択します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-130">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="3ac87-131">[ **新しい bot を作成し、** **ボット登録を作成** する] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-131">Select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="3ac87-132">成功した場合、新しい bot は **登録済み** の状態になります。</span><span class="sxs-lookup"><span data-stu-id="3ac87-132">If successful, your new bot will have a **Registered** status.</span></span>
    1. <span data-ttu-id="3ac87-133">ここでは、リンク unfurling オプションに [ **いいえ** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-133">For now, select **No** for the link unfurling option.</span></span>
1. <span data-ttu-id="3ac87-134">画面の下部にある [ **完了** ] を選択して、プロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="3ac87-135">2. 関連するアプリプロジェクトコンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="3ac87-135">2. Identify relevant app project components</span></span>

<span data-ttu-id="3ac87-136">Teams ツールキットを使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="3ac87-136">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="3ac87-137">アプリの構成</span><span class="sxs-lookup"><span data-stu-id="3ac87-137">App configurations</span></span>

<span data-ttu-id="3ac87-138">メッセージング拡張機能の構成を表示または更新するには、ツールキットで [ **App Studio** ] を選択し、[ **メッセージング拡張** ] に移動します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-138">To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="3ac87-139">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="3ac87-139">App scaffolding</span></span>

<span data-ttu-id="3ac87-140">アプリのスキャフォールディングは、 `botActivityHandler.js` メッセージング拡張機能 (または、技術的には [メッセージング拡張機能](#4-configure-the-bot-for-your-messaging-extension)) が Teams の検索クエリにどのように応答するかを処理するために、プロジェクトのルートディレクトリにあるファイルを提供します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-140">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="3ac87-141">3. アプリへのセキュリティで保護されたトンネルをセットアップする</span><span class="sxs-lookup"><span data-stu-id="3ac87-141">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="3ac87-142">テストを目的として、ローカル web サーバーでメッセージング拡張機能をホストします (ポート 3978)。</span><span class="sxs-lookup"><span data-stu-id="3ac87-142">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="3ac87-143">まだインストールしていない場合は、 [ngrok](https://ngrok.com/download)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="3ac87-143">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="3ac87-144">ターミナルで、を実行 `ngrok http -host-header=rewrite 3978` します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-144">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="3ac87-145">Teams で HTTPS 接続が必要になったため、出力に HTTPS URL (たとえば、) をコピーし `https://468b9ab725e9.ngrok.io` ます。</span><span class="sxs-lookup"><span data-stu-id="3ac87-145">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="3ac87-146">この URL を使用すると、Teams (HTTPS 接続を必要とする) は、アプリをホストしている場所にトンネルでき `localhost` ます (ポート 3978)。</span><span class="sxs-lookup"><span data-stu-id="3ac87-146">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="3ac87-147">4. メッセージング拡張機能の bot を構成する</span><span class="sxs-lookup"><span data-stu-id="3ac87-147">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="3ac87-148">メッセージング拡張機能は、ボットに依存して、チームからのユーザー要求をホストされたサービスに送信して処理します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-148">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="3ac87-149">ボットは、Teams ツールキットを使用してアプリをセットアップするときに実行された Azure Bot サービスに登録されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ac87-149">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="3ac87-150">メッセージング拡張機能で検索クエリを受信して処理するには、ボットエンドポイント URL を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ac87-150">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="3ac87-151">通常、URL はのように `https://HOST_URL/api/messages` なります。</span><span class="sxs-lookup"><span data-stu-id="3ac87-151">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="3ac87-152">これは、ツールキットですばやく構成できます。</span><span class="sxs-lookup"><span data-stu-id="3ac87-152">You can configure this quickly in the toolkit.</span></span>

1. Visual Studio Code で、左側のアクティビティバーで [ **Microsoft teams** ] を選択し、 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: [ **microsoft Teams ツールキットを開く** ] を選択します。
1. <span data-ttu-id="3ac87-154">[ **ボット > 既存の bot 登録** ] に移動し、セットアップ時に作成した bot を選択します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-154">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="3ac87-155">**Bot エンドポイントアドレス** フィールドに、bot をホストしている ngrok URL (たとえば、) を入力 `https://468b9ab725e9.ngrok.io` し `/api/messages` ます。</span><span class="sxs-lookup"><span data-stu-id="3ac87-155">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

<span data-ttu-id="3ac87-156">Bot は、メッセージング拡張機能でクエリを処理できるようになります。</span><span class="sxs-lookup"><span data-stu-id="3ac87-156">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="3ac87-157">5. アプリをビルドして実行する</span><span class="sxs-lookup"><span data-stu-id="3ac87-157">5. Build and run your app</span></span>

<span data-ttu-id="3ac87-158">メッセージング拡張機能をホストする URL を設定し、検索を処理するように構成します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-158">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="3ac87-159">アプリを起動して実行します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="3ac87-160">ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="3ac87-161">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-161">Run `npm start`.</span></span>

<span data-ttu-id="3ac87-162">成功した場合、次のメッセージが表示されます。メッセージング拡張サービスが自分のアクティビティをリッスンしていることを示し `localhost` ます。</span><span class="sxs-lookup"><span data-stu-id="3ac87-162">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="3ac87-163">サイドロード Teams でのメッセージング拡張機能の作成</span><span class="sxs-lookup"><span data-stu-id="3ac87-163">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="3ac87-164">メッセージング拡張機能が実行されている状態で、Teams にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="3ac87-164">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="3ac87-165">以前に Teams アプリをサイドロードしていない場合は、以下の [手順](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)を実行します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="3ac87-166">Visual Studio Code で、 **F5** キーを押して Teams web クライアントを起動します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="3ac87-167">[アプリのインストール] ダイアログで、[ **追加** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-167">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="3ac87-168">7. メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="3ac87-168">7. Test your messaging extension</span></span>

<span data-ttu-id="3ac87-169">Teams チャットでのメッセージング拡張機能のしくみについて説明します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-169">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="3ac87-170">新しいチャットを開始します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-170">Start a new chat.</span></span> [新規作成] ボックスで、[ **詳細** ] を選択 :::image type="icon" source="../assets/icons/teams-client-more.png"::: し、サイドロードしたばかりのメッセージング拡張アプリを選択します。
1. <span data-ttu-id="3ac87-172">何らかの検索を試みます (たとえば、[ **チケット** ])。</span><span class="sxs-lookup"><span data-stu-id="3ac87-172">Try searching for something (for example, **Tickets** ).</span></span> <span data-ttu-id="3ac87-173">アプリが動作している場合は、サンプルの検索結果が表示されます (後で自分で追加することができます)。</span><span class="sxs-lookup"><span data-stu-id="3ac87-173">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="検索ベースのメッセージング拡張が Teams の新規作成ボックスでどのように使用されるかを示すスクリーンショット。":::

## <a name="well-done"></a><span data-ttu-id="3ac87-175">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="3ac87-175">Well done</span></span>

<span data-ttu-id="3ac87-176">おめでとうございます。</span><span class="sxs-lookup"><span data-stu-id="3ac87-176">Congratulations!</span></span> <span data-ttu-id="3ac87-177">[作成] または [コマンド] ボックスで外部コンテンツを検索するように設定されている基本的な Teams メッセージング拡張機能があります。</span><span class="sxs-lookup"><span data-stu-id="3ac87-177">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ac87-178">次のステップ</span><span class="sxs-lookup"><span data-stu-id="3ac87-178">Next steps</span></span>

<span data-ttu-id="3ac87-179">次のページを参照して続行し、完全な機能を備えたメッセージング拡張機能を構築します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-179">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="3ac87-180">サービスに関連する[検索コマンドを定義](../messaging-extensions/how-to/search-commands/define-search-command.md)します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-180">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="3ac87-181">[ユーザーの検索に応答](../messaging-extensions/how-to/search-commands/respond-to-search.md)するようにサービスを構成します。</span><span class="sxs-lookup"><span data-stu-id="3ac87-181">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3ac87-182">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="3ac87-182">Troubleshooting</span></span>

<span data-ttu-id="3ac87-183">このチュートリアルを完了する際に問題が発生した場合は、次の情報が役立ちます。</span><span class="sxs-lookup"><span data-stu-id="3ac87-183">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="3ac87-184">Bot が Teams に接続されていない</span><span class="sxs-lookup"><span data-stu-id="3ac87-184">Bot isn't connected to Teams</span></span>

<span data-ttu-id="3ac87-185">アプリをインストールしたが動作していない場合は、メッセージング拡張機能の bot が [Azure Bot サービスの Teams *チャネル* に接続](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="3ac87-185">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="3ac87-186">これは Teams のチャネルと同じではないことを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="3ac87-186">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="3ac87-187">この場合、チャネルは、Azure Bot サービスが Bot を Teams または他の [サポートされている Microsoft またはサードパーティの通信アプリ](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)に接続する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3ac87-187">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="3ac87-188">詳細情報</span><span class="sxs-lookup"><span data-stu-id="3ac87-188">Learn more</span></span>

* [<span data-ttu-id="3ac87-189">Link unfurling フィーチャーを含める</span><span class="sxs-lookup"><span data-stu-id="3ac87-189">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="3ac87-190">認証を追加する</span><span class="sxs-lookup"><span data-stu-id="3ac87-190">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="3ac87-191">アクションベースのメッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="3ac87-191">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="3ac87-192">Microsoft Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="3ac87-192">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
