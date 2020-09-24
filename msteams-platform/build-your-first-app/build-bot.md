---
title: Teams bot を構築する
author: heath-hamilton
description: 最初の Microsoft Teams アプリの bot を構築する方法について説明します。
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: cc004bd0d86eca1e4e63c2a96a72f9c11d2269db
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237826"
---
# <a name="build-a-teams-bot"></a><span data-ttu-id="72258-103">Teams bot を構築する</span><span class="sxs-lookup"><span data-stu-id="72258-103">Build a Teams bot</span></span>

<span data-ttu-id="72258-104">このチュートリアルでは、基本的な *bot* アプリを構築します。</span><span class="sxs-lookup"><span data-stu-id="72258-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="72258-105">Bot は Teams ユーザーと web サービス間の仲介者として機能します。</span><span class="sxs-lookup"><span data-stu-id="72258-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="72258-106">ユーザーは bot とチャットして、サービスによって実行された情報をすばやく取得したり、ワークフローやタスクを開始したりできます。</span><span class="sxs-lookup"><span data-stu-id="72258-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="72258-107">自分の割り当て</span><span class="sxs-lookup"><span data-stu-id="72258-107">Your assignment</span></span>

<span data-ttu-id="72258-108">職場では、チーム内で重要な連絡先情報を表示するための [タブ](../build-your-first-app/build-personal-tab.md) を使用しています。</span><span class="sxs-lookup"><span data-stu-id="72258-108">Your workplace has been using [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information in Teams.</span></span> <span data-ttu-id="72258-109">たとえば、仕事仲間は、ヘルプデスクの電話番号にすばやくアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="72258-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="72258-110">しかし、通話の代わりに、ユーザーが chatbot を使用してヘルプデスクに連絡することができた場合はどうなりますか。</span><span class="sxs-lookup"><span data-stu-id="72258-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="72258-111">上司からは、Teams での基本的な会話をすばやく実行する方法を確認するように求められています。</span><span class="sxs-lookup"><span data-stu-id="72258-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="72258-112">学習内容</span><span class="sxs-lookup"><span data-stu-id="72258-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="72258-113">Microsoft Teams Toolkit for Visual Studio Code を使用してアプリプロジェクトとボットを作成する</span><span class="sxs-lookup"><span data-stu-id="72258-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="72258-114">Bot に関連するアプリマニフェストのプロパティとスキャフォールディングの一部を特定する</span><span class="sxs-lookup"><span data-stu-id="72258-114">Identify some of the app manifest properties and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="72258-115">アプリをローカルでホストする</span><span class="sxs-lookup"><span data-stu-id="72258-115">Host an app locally</span></span>
> * <span data-ttu-id="72258-116">Teams の bot を構成する</span><span class="sxs-lookup"><span data-stu-id="72258-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="72258-117">Teams でボットをサイドロードおよびテストする</span><span class="sxs-lookup"><span data-stu-id="72258-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="72258-118">はじめに</span><span class="sxs-lookup"><span data-stu-id="72258-118">Before you begin</span></span>

<span data-ttu-id="72258-119">まだお持ちでない場合は、 [Teams 開発の前提条件を理解し、インストール](build-first-app-overview.md#get-prerequisites)してください。</span><span class="sxs-lookup"><span data-stu-id="72258-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="72258-120">1. アプリプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="72258-120">1. Create your app project</span></span>

<span data-ttu-id="72258-121">Microsoft Teams Toolkit は、アプリ用に次のコンポーネントをセットアップするのに役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="72258-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="72258-122">**アプリケーションマニフェストと** bot に関連するスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="72258-122">**App manifest and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="72258-123">Microsoft Azure Bot サービスに自動的に登録された**Bot**</span><span class="sxs-lookup"><span data-stu-id="72258-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="72258-124">以前に Teams アプリプロジェクトを作成していない場合は、 [以下の手順](../build-your-first-app/build-and-run.md) に従って、プロジェクトについて詳しく説明することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="72258-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
1. <span data-ttu-id="72258-126">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="72258-126">Enter a name for your Teams app.</span></span> <span data-ttu-id="72258-127">(これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)</span><span class="sxs-lookup"><span data-stu-id="72258-127">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="72258-128">[ **機能の追加** ] 画面で、[ **Bot** ] を選択し、[ **次へ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="72258-128">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="72258-129">[ **新しい Bot を作成** し、 **ログイン** する] を選択して、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="72258-129">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span><br/>
:::image type="content" source="../assets/images/build-your-first-app/vsc-create-bot.png" alt-text="Teams ツールキットで、Microsoft 365 アカウントにログインして新しい bot を作成する方法を示す図。":::
1. <span data-ttu-id="72258-131">Bot ID とパスワードを保存します (これは後で必要になります)。</span><span class="sxs-lookup"><span data-stu-id="72258-131">Store your bot ID and password (you need this a little later).</span></span>
1. <span data-ttu-id="72258-132">オプションBot のカスタム名を入力し、[ **作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="72258-132">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="72258-133">(これは bot の名前であり、既に指定した Teams アプリの名前ではないことに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="72258-133">(Remember, this is the name for your bot and not the name of the Teams app you already specified.)</span></span>
1. <span data-ttu-id="72258-134">画面の下部にある [ **完了** ] を選択して、プロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="72258-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="72258-135">2. 関連するアプリプロジェクトコンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="72258-135">2. Identify relevant app project components</span></span>

<span data-ttu-id="72258-136">Teams ツールキットを使用してプロジェクトを作成すると、アプリマニフェストとスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="72258-136">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="72258-137">Bot を構築するための主なコンポーネントを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="72258-137">Let's look at the main components for building a bot.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="72258-138">アプリマニフェスト</span><span class="sxs-lookup"><span data-stu-id="72258-138">App manifest</span></span>

<span data-ttu-id="72258-139">アプリマニフェスト ( `manifest.json` プロジェクトのディレクトリ内のファイル) の次のスニペットは、 `.publish` bot に関連するプロパティと既定値を示しています。</span><span class="sxs-lookup"><span data-stu-id="72258-139">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to bots.</span></span>

```JSON
"bots": [
    {
        "botId": "{botId0}",
        "scopes": [
            "personal",
            "groupchat",
            "team"
        ],
        "supportsFiles": false,
        "isNotificationOnly": false,
        "commandLists": [
            {
                "scopes": [
                    "personal",
                    "groupchat",
                    "team"
                ],
                "commands": [
                    {
                        "title": "Hello",
                        "description": "Sends a hello message and @mention the sender"
                    }
                ]
            }
        ]
    }
],
```

<span data-ttu-id="72258-140">ここでは、次の必須プロパティに焦点を絞って説明します。</span><span class="sxs-lookup"><span data-stu-id="72258-140">For now, let's just focus on the following required properties.</span></span> <span data-ttu-id="72258-141">(サポートされているプロパティの完全な一覧を参照してください [`bots`](../resources/schema/manifest-schema.md#bots) )。</span><span class="sxs-lookup"><span data-stu-id="72258-141">(See the full list of supported [`bots`](../resources/schema/manifest-schema.md#bots) properties.)</span></span>

* <span data-ttu-id="72258-142">`botId`: 作成した bot の ID。プロジェクトを設定します。</span><span class="sxs-lookup"><span data-stu-id="72258-142">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="72258-143">(に保存されている場合は、の `{botId0}` 実際の ID を検索でき `Development.env` ます)。</span><span class="sxs-lookup"><span data-stu-id="72258-143">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="72258-144">`scopes`: Bot が `personal` 、、 `groupchat` または `team` (つまりチャネル) コンテキストで使用可能かどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="72258-144">`scopes`: Specifies if your bot is available in `personal`, `groupchat`, or `team` (i.e., channel) contexts.</span></span>
* <span data-ttu-id="72258-145">`commands`: 使用可能なコマンドは、ユーザーが bot に送信できます。</span><span class="sxs-lookup"><span data-stu-id="72258-145">`commands`: Available commands users can send to your bot.</span></span>
* <span data-ttu-id="72258-146">`title`: Teams クライアントに表示される Bot コマンド名。</span><span class="sxs-lookup"><span data-stu-id="72258-146">`title`: Bot command name that displays in the Teams client.</span></span>
* <span data-ttu-id="72258-147">`description`: ユーザーが bot コマンドの機能を理解するのに役立つ構文および引数の簡単な説明または例。</span><span class="sxs-lookup"><span data-stu-id="72258-147">`description`: A short description or example of the syntax and arguments to help users understand what a bot command does.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="72258-148">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="72258-148">App scaffolding</span></span>

<span data-ttu-id="72258-149">アプリのスキャフォールディングは、 `botActivityHandler.js` ボットが Teams でのアクティビティを処理する方法について、プロジェクトのルートディレクトリにあるファイルを提供します (たとえば、"Hello" のような特定のメッセージに bot が応答する方法)。</span><span class="sxs-lookup"><span data-stu-id="72258-149">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

<span data-ttu-id="72258-150">このファイルには、 `.env` ルートディレクトリにも BOT ID とパスワードが保存されます。</span><span class="sxs-lookup"><span data-stu-id="72258-150">The `.env` file, also in the root directory, stores your bot ID and password.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="72258-151">3. アプリへのセキュリティで保護されたトンネルをセットアップする</span><span class="sxs-lookup"><span data-stu-id="72258-151">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="72258-152">テストを目的として、ボットをローカル web サーバー (ポート 3978) にホストしてみましょう。</span><span class="sxs-lookup"><span data-stu-id="72258-152">For testing purposes, let's host your bot on a local web server (port 3978).</span></span>

1. <span data-ttu-id="72258-153">ターミナルで、を実行 `ngrok http -host-header=rewrite 3978` します。</span><span class="sxs-lookup"><span data-stu-id="72258-153">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="72258-154">Teams で HTTPS 接続が必要なため、出力に HTTPS URL をコピーします。</span><span class="sxs-lookup"><span data-stu-id="72258-154">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="72258-155">ディレクトリで `.publish` 、を開き `Development.env` ます。</span><span class="sxs-lookup"><span data-stu-id="72258-155">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="72258-156">値を `baseUrl0` コピーした URL に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="72258-156">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="72258-157">(たとえば、 `baseUrl0=http://localhost:3000` をに変更 `baseUrl0=https://85528b2b3ca5.ngrok.io` します)。</span><span class="sxs-lookup"><span data-stu-id="72258-157">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="72258-158">アプリのマニフェストが bot をホストしている場所を指しています。</span><span class="sxs-lookup"><span data-stu-id="72258-158">Your app manifest is pointing to where you're hosting the bot.</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="72258-159">4. bot を構成する</span><span class="sxs-lookup"><span data-stu-id="72258-159">4. Configure your bot</span></span>

<span data-ttu-id="72258-160">Teams でボットを使用するには、その bot を Azure Bot サービスに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="72258-160">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="72258-161">さいわい、Teams ツールキットを使用してアプリをセットアップすると、これは自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="72258-161">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

### <a name="specify-your-bot-id-and-password"></a><span data-ttu-id="72258-162">Bot ID とパスワードを指定する</span><span class="sxs-lookup"><span data-stu-id="72258-162">Specify your bot ID and password</span></span>

<span data-ttu-id="72258-163">Bot が Azure Bot サービスに登録されると、Teams アプリが知っておく必要がある ID とパスワードが割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="72258-163">When your bot is registered with the Azure Bot Service, it's assigned an ID and password that your Teams app must know about.</span></span>

1. <span data-ttu-id="72258-164">ツールキットのセットアップ時に保存した bot ID とパスワードを見つけます。</span><span class="sxs-lookup"><span data-stu-id="72258-164">Locate the bot ID and password you stored during toolkit setup.</span></span>
1. <span data-ttu-id="72258-165">ルートディレクトリで、ファイルを開き `.env` ます。</span><span class="sxs-lookup"><span data-stu-id="72258-165">In your root directory, open the `.env` file.</span></span>
1. <span data-ttu-id="72258-166">Bot ID とパスワードをそれぞれにに追加し `BotId` `BotPassword` ます。</span><span class="sxs-lookup"><span data-stu-id="72258-166">Add your bot ID and password to `BotId` and `BotPassword`, respectively.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="72258-167">Bot エンドポイントアドレスを追加する</span><span class="sxs-lookup"><span data-stu-id="72258-167">Add the bot endpoint address</span></span>

<span data-ttu-id="72258-168">Bot に送信されるユーザーメッセージ (つまり、要求) を受信して処理するためのエンドポイント URL を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="72258-168">You must specify an endpoint URL to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="72258-169">通常、URL はのように `https://HOST_URL/api/messages` なります。</span><span class="sxs-lookup"><span data-stu-id="72258-169">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="72258-170">これは Teams ツールキットですばやく構成できます。</span><span class="sxs-lookup"><span data-stu-id="72258-170">You can configure this quickly in the Teams Toolkit.</span></span>

1. Visual Studio Code で、左側のアクティビティバーで [ **Microsoft teams** ] を選択し、 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: [ **microsoft Teams ツールキットを開く**] を選択します。
1. <span data-ttu-id="72258-172">[ **ボット management > 既存の bot 登録** ] に移動し、セットアップ時に作成した bot を選択します。</span><span class="sxs-lookup"><span data-stu-id="72258-172">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="72258-173">**Bot エンドポイントアドレス**フィールドに、bot (値) をホストしているローカル web サーバーを入力 `baseUrl10` し、 `/api/messages` それに追加します。</span><span class="sxs-lookup"><span data-stu-id="72258-173">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot (`baseUrl10` value) and append `/api/messages` to it.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Teams ツールキットで bot エンドポイント URL を構成できる場所を示す図。":::

<span data-ttu-id="72258-175">Bot は Teams のメッセージに応答できるようになります。</span><span class="sxs-lookup"><span data-stu-id="72258-175">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-run-your-app"></a><span data-ttu-id="72258-176">5. アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="72258-176">5. Run your app</span></span>

<span data-ttu-id="72258-177">Bot をホストする URL を設定し、メッセージを処理するように構成します。</span><span class="sxs-lookup"><span data-stu-id="72258-177">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="72258-178">その後、自分の bot を起動して実行します。</span><span class="sxs-lookup"><span data-stu-id="72258-178">It's time to get your bot up and running.</span></span>

1. <span data-ttu-id="72258-179">ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。</span><span class="sxs-lookup"><span data-stu-id="72258-179">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="72258-180">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="72258-180">Run `npm start`.</span></span>

<span data-ttu-id="72258-181">成功した場合、ボットが自分のアクティビティをリッスンしていることを示す次のようなメッセージが表示され `localhost` ます。</span><span class="sxs-lookup"><span data-stu-id="72258-181">If successful, you see something like the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="72258-182">6 Teams での bot のサイドロード</span><span class="sxs-lookup"><span data-stu-id="72258-182">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="72258-183">Bot を実行している場合は、Teams にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="72258-183">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="72258-184">以前に Teams アプリをサイドロードしていない場合は、以下の [手順](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams)を実行します。</span><span class="sxs-lookup"><span data-stu-id="72258-184">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="72258-185">アプリのサイドロードを許可するアカウントを使用して、Teams クライアントにログインします。</span><span class="sxs-lookup"><span data-stu-id="72258-185">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="72258-186">[ **アプリ**] を選択し、[ **カスタムアプリのアップロード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="72258-186">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="72258-187">アプリプロジェクトフォルダーに移動し `.publish` 、を選択し `Development.zip` ます。</span><span class="sxs-lookup"><span data-stu-id="72258-187">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="72258-188">[モーダルのインストール] で、[ **追加** ] を選択してアプリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="72258-188">In the install modal, select **Add** to install your app.</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="72258-189">7. bot をテストする</span><span class="sxs-lookup"><span data-stu-id="72258-189">7. Test your bot</span></span>

<span data-ttu-id="72258-190">おもしろい部分のために、1対1のチャットで bot に "Hello" と言うことができます。</span><span class="sxs-lookup"><span data-stu-id="72258-190">Now for the fun part: Let's say "Hello" to your bot in a one-on-one chat.</span></span>

1. Teams で、左側にある [ **その他**] を選択し :::image type="icon" source="../assets/icons/teams-client-more.png"::: ます。
1. <span data-ttu-id="72258-192">サイドロードの bot を見つけて選択します。</span><span class="sxs-lookup"><span data-stu-id="72258-192">Locate and choose the bot you just sideloaded.</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/bot-teams-access.png" alt-text="Teams で bot にアクセスする場所を示す図。":::
1. <span data-ttu-id="72258-194">[新規作成] ボックスで、 `Hello` メッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="72258-194">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="72258-195">Bot は次のようなメッセージに返信します。</span><span class="sxs-lookup"><span data-stu-id="72258-195">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="ユーザーが Teams の bot に "Hello" と言って、応答を取得することを示すスクリーンショット。":::

## <a name="well-done"></a><span data-ttu-id="72258-197">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="72258-197">Well done</span></span>

<span data-ttu-id="72258-198">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="72258-198">Congratulations!</span></span> <span data-ttu-id="72258-199">ユーザーが1対1で、またはグループ設定 (チャネルとチャット) で通信できる基本的な Teams bot があります。</span><span class="sxs-lookup"><span data-stu-id="72258-199">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="72258-200">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="72258-200">Troubleshooting</span></span>

<span data-ttu-id="72258-201">このチュートリアルを完了する際に問題が発生した場合は、次の情報が役立ちます。</span><span class="sxs-lookup"><span data-stu-id="72258-201">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="72258-202">ツールキットのセットアップが失敗する</span><span class="sxs-lookup"><span data-stu-id="72258-202">Toolkit setup fails</span></span>

<span data-ttu-id="72258-203">Teams ツールキットを使用してアプリプロジェクトをセットアップするときに、[ **新しい Bot を作成** する] オプションを選択し、Microsoft 365 開発アカウントでログインすると、エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="72258-203">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="72258-204">これは認証の問題である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="72258-204">This could be an authentication issue.</span></span> <span data-ttu-id="72258-205">プロジェクトの設定を完了するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="72258-205">Follow these steps to finish setting up your project.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft Teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **サインアウト**] を選択します。
1. <span data-ttu-id="72258-207">同じアカウントを使用してログインし、新しい bot を作成することにより、セットアッププロセスを再度実行します。</span><span class="sxs-lookup"><span data-stu-id="72258-207">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="72258-208">Bot が Teams に接続されていない</span><span class="sxs-lookup"><span data-stu-id="72258-208">Bot isn't connected to Teams</span></span>

<span data-ttu-id="72258-209">アプリをインストールしたが、bot が動作していない場合は、ボットが[Azure Bot サービスの Teams*チャネル*に接続](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="72258-209">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="72258-210">これは Teams のチャネルと同じではないことを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="72258-210">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="72258-211">この場合、チャネルは、Azure Bot サービスが Bot を Teams または他の [サポートされている Microsoft またはサードパーティの通信アプリ](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)に接続する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="72258-211">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="72258-212">詳細情報</span><span class="sxs-lookup"><span data-stu-id="72258-212">Learn more</span></span>

* [<span data-ttu-id="72258-213">サンプルのいずれかで、他の Teams のボットができることを確認する</span><span class="sxs-lookup"><span data-stu-id="72258-213">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="72258-214">ボット会話の基本</span><span class="sxs-lookup"><span data-stu-id="72258-214">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="72258-215">Teams での Bot 認証</span><span class="sxs-lookup"><span data-stu-id="72258-215">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="72258-216">Microsoft Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="72258-216">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="72258-217">ツールキットなしでボットを作成する</span><span class="sxs-lookup"><span data-stu-id="72258-217">Create a bot without the toolkit</span></span>](../bots/how-to/create-a-bot-for-teams.md)
