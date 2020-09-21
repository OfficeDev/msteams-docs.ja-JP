---
title: Teams のボットを作成する
author: heath-hamilton
description: 最初の Microsoft Teams アプリで bot をビルドする方法について説明します。
ms.author: lajanuar
ms.date: 08/31/2020
ms.topic: tutorial
ms.openlocfilehash: f1307bcc7bb864ddfa97b9297f34fa4f7d5fcb0d
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964723"
---
# <a name="create-a-bot-for-teams"></a><span data-ttu-id="04b6a-103">Teams のボットを作成する</span><span class="sxs-lookup"><span data-stu-id="04b6a-103">Create a bot for Teams</span></span>

<span data-ttu-id="04b6a-104">このチュートリアルでは、基本的な *bot* アプリを構築します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="04b6a-105">Bot は Teams ユーザーと web サービス間の仲介者として機能します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="04b6a-106">ユーザーは bot とチャットして、サービスによって実行された情報をすばやく取得したり、ワークフローやタスクを開始したりできます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="04b6a-107">自分の割り当て</span><span class="sxs-lookup"><span data-stu-id="04b6a-107">Your assignment</span></span>

<span data-ttu-id="04b6a-108">職場では、チーム内で重要な連絡先情報を表示するための [タブ](../build-your-first-app/add-personal-tab.md) を使用しています。</span><span class="sxs-lookup"><span data-stu-id="04b6a-108">Your workplace has been using [tabs](../build-your-first-app/add-personal-tab.md) to surface important contact information in Teams.</span></span> <span data-ttu-id="04b6a-109">たとえば、仕事仲間は、ヘルプデスクの電話番号にすばやくアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="04b6a-110">しかし、通話の代わりに、ユーザーが chatbot を使用してヘルプデスクに連絡することができた場合はどうなりますか。</span><span class="sxs-lookup"><span data-stu-id="04b6a-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="04b6a-111">上司からは、Teams での基本的な会話をすばやく実行する方法を確認するように求められています。</span><span class="sxs-lookup"><span data-stu-id="04b6a-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="04b6a-112">学習内容</span><span class="sxs-lookup"><span data-stu-id="04b6a-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="04b6a-113">Microsoft Teams Toolkit for Visual Studio Code を使用してアプリプロジェクトとボットを作成する</span><span class="sxs-lookup"><span data-stu-id="04b6a-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="04b6a-114">アプリマニフェストのプロパティと bot に関連するいくつかのスキャフォールディングを特定する</span><span class="sxs-lookup"><span data-stu-id="04b6a-114">Identify the app manifest properties and some of the scaffolding relevant to bots</span></span>
> * <span data-ttu-id="04b6a-115">Bot をローカルでホストする</span><span class="sxs-lookup"><span data-stu-id="04b6a-115">Host a bot locally</span></span>
> * <span data-ttu-id="04b6a-116">Teams の bot を構成する</span><span class="sxs-lookup"><span data-stu-id="04b6a-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="04b6a-117">Teams でボットをサイドロードおよびテストする</span><span class="sxs-lookup"><span data-stu-id="04b6a-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="04b6a-118">はじめに</span><span class="sxs-lookup"><span data-stu-id="04b6a-118">Before you begin</span></span>

<span data-ttu-id="04b6a-119">まだお持ちでない場合は、Microsoft 365 開発 [アカウント](building-real-world-app.md#set-up-your-development-account) および [Teams アプリツール](building-real-world-app.md#install-your-development-tools)を設定してください。</span><span class="sxs-lookup"><span data-stu-id="04b6a-119">If you haven't yet, set up your Microsoft 365 development [account](building-real-world-app.md#set-up-your-development-account) and [Teams app tools](building-real-world-app.md#install-your-development-tools).</span></span>

## <a name="create-your-app-project-and-bot"></a><span data-ttu-id="04b6a-120">アプリプロジェクトと bot を作成する</span><span class="sxs-lookup"><span data-stu-id="04b6a-120">Create your app project and bot</span></span>

<span data-ttu-id="04b6a-121">Microsoft Teams Toolkit は、アプリ用に次のコンポーネントをセットアップするのに役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="04b6a-122">**アプリプロジェクト**: bot に関連するアプリマニフェストとスキャフォールディングを含みます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-122">**App project**: Includes the app manifest and scaffolding relevant to bots</span></span>
* <span data-ttu-id="04b6a-123">**Bot**: 新しい Bot を構成し、それを Microsoft Azure Bot サービスに登録します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-123">**Bot**: Configures a new bot and registers it with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="04b6a-124">以前に Teams アプリプロジェクトを作成していない場合は、 [以下の手順](../build-your-first-app/build-and-run.md) に従って、プロジェクトについて詳しく説明することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="04b6a-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
1. <span data-ttu-id="04b6a-126">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-126">Enter a name for your Teams app.</span></span> <span data-ttu-id="04b6a-127">(これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)</span><span class="sxs-lookup"><span data-stu-id="04b6a-127">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="04b6a-128">[ **機能の追加** ] 画面で、[ **Bot** ] を選択し、[ **次へ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-128">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="04b6a-129">[ **新しい Bot を作成** し、 **ログイン** する] を選択して、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="04b6a-129">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span><br/>
:::image type="content" source="../doc-links/images/vsc-create-bot.png" alt-text="Teams ツールキットで、Microsoft 365 アカウントにログインして新しい bot を作成する方法を示す図。":::
1. <span data-ttu-id="04b6a-131">オプションBot のカスタム名を入力し、[ **作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-131">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="04b6a-132">(これは bot の名前であり、既に指定した Teams アプリの名前ではないことに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="04b6a-132">(Remember, this is the name for your bot and not the name of the Teams app you already specified.)</span></span>
1. <span data-ttu-id="04b6a-133">画面の下部にある [ **完了** ] を選択して、プロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-133">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="identify-relevant-app-project-components"></a><span data-ttu-id="04b6a-134">関連するアプリプロジェクトコンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="04b6a-134">Identify relevant app project components</span></span>

<span data-ttu-id="04b6a-135">Teams ツールキットを使用してプロジェクトを作成すると、アプリマニフェストとスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-135">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="04b6a-136">Bot を構築するための主なコンポーネントを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="04b6a-136">Let's look at the main components for building a bot.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="04b6a-137">アプリマニフェスト</span><span class="sxs-lookup"><span data-stu-id="04b6a-137">App manifest</span></span>

<span data-ttu-id="04b6a-138">アプリマニフェスト ( `manifest.json` プロジェクトのディレクトリ内のファイル) の次のスニペットは、 `.publish` bot に関連するプロパティと既定値を示しています。</span><span class="sxs-lookup"><span data-stu-id="04b6a-138">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to bots.</span></span>

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

<span data-ttu-id="04b6a-139">ここでは、次の必須プロパティに焦点を絞って説明します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-139">For now, let's just focus on the following required properties.</span></span> <span data-ttu-id="04b6a-140">(サポートされているプロパティの完全な一覧を参照してください [`bots`](../../resources/schema/manifest-schema.md#bots) )。</span><span class="sxs-lookup"><span data-stu-id="04b6a-140">(See the full list of supported [`bots`](../../resources/schema/manifest-schema.md#bots) properties.)</span></span>

* <span data-ttu-id="04b6a-141">`botId`: 作成した bot の ID。プロジェクトを設定します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-141">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="04b6a-142">(に保存されている場合は、の `{botId0}` 実際の ID を検索でき `Development.env` ます)。</span><span class="sxs-lookup"><span data-stu-id="04b6a-142">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="04b6a-143">`scopes`: Bot が `personal` 、、 `groupchat` または `team` (つまりチャネル) コンテキストで使用可能かどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-143">`scopes`: Specifies if your bot is available in `personal`, `groupchat`, or `team` (i.e., channel) contexts.</span></span>
* <span data-ttu-id="04b6a-144">`commands`: 使用可能なコマンドは、ユーザーが bot に送信できます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-144">`commands`: Available commands users can send to your bot.</span></span>
* <span data-ttu-id="04b6a-145">`title`: Teams クライアントに bot コマンド名ユーザーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-145">`title`: A bot command name users see in the Teams client.</span></span>
* <span data-ttu-id="04b6a-146">`description`: ユーザーが bot コマンドの機能を理解するのに役立つ構文および引数の簡単な説明または例。</span><span class="sxs-lookup"><span data-stu-id="04b6a-146">`description`: A short description or example of the syntax and arguments to help users understand what a bot command does.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="04b6a-147">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="04b6a-147">App scaffolding</span></span>

<span data-ttu-id="04b6a-148">アプリのスキャフォールディングは、 `botActivityHandler.js` ボットが Teams でのアクティビティを処理する方法について、プロジェクトのルートディレクトリにあるファイルを提供します (たとえば、"Hello" のような特定のメッセージに bot が応答する方法)。</span><span class="sxs-lookup"><span data-stu-id="04b6a-148">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="04b6a-149">アプリへのセキュリティで保護されたトンネルの設定</span><span class="sxs-lookup"><span data-stu-id="04b6a-149">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="04b6a-150">テストを目的として、ボットをローカル web サーバー (ポート 3978) にホストしてみましょう。</span><span class="sxs-lookup"><span data-stu-id="04b6a-150">For testing purposes, let's host your bot on a local web server (port 3978).</span></span>

1. <span data-ttu-id="04b6a-151">ターミナルで、を実行 `ngrok http -host-header=rewrite 3978` します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-151">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="04b6a-152">Teams で HTTPS 接続が必要なため、出力に HTTPS URL をコピーします。</span><span class="sxs-lookup"><span data-stu-id="04b6a-152">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="04b6a-153">ディレクトリで `.publish` 、を開き `Development.env` ます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-153">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="04b6a-154">値を `baseUrl0` コピーした URL に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-154">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="04b6a-155">(たとえば、 `baseUrl0=http://localhost:3000` をに変更 `baseUrl0=https://85528b2b3ca5.ngrok.io` します)。</span><span class="sxs-lookup"><span data-stu-id="04b6a-155">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="04b6a-156">アプリのマニフェストが bot をホストしている場所を指しています。</span><span class="sxs-lookup"><span data-stu-id="04b6a-156">Your app manifest is pointing to where you're hosting the bot.</span></span>

## <a name="configuring-your-bot"></a><span data-ttu-id="04b6a-157">Bot を構成する</span><span class="sxs-lookup"><span data-stu-id="04b6a-157">Configuring your bot</span></span>

<span data-ttu-id="04b6a-158">Teams でボットを使用するには、その bot を Azure Bot サービスに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="04b6a-158">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="04b6a-159">さいわい、Teams ツールキットを使用してアプリをセットアップすると、これは自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-159">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="04b6a-160">Bot エンドポイントアドレスを追加する</span><span class="sxs-lookup"><span data-stu-id="04b6a-160">Add the bot endpoint address</span></span>

<span data-ttu-id="04b6a-161">Bot に送信されるユーザーメッセージ (つまり、要求) を受信して処理するためのエンドポイント URL を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="04b6a-161">You must specify an endpoint URL to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="04b6a-162">通常、URL はのように `https://HOST_URL/api/messages` なります。</span><span class="sxs-lookup"><span data-stu-id="04b6a-162">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="04b6a-163">これは Teams ツールキットですばやく構成できます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-163">You can configure this quickly in the Teams Toolkit.</span></span>

1. Visual Studio Code で、左側のアクティビティバーで [ **Microsoft teams** ] を選択し、 :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: [ **microsoft Teams ツールキットを開く**] を選択します。
1. <span data-ttu-id="04b6a-165">[ **ボット management > 既存の bot 登録** ] に移動し、セットアップ時に作成した bot を選択します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-165">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="04b6a-166">**Bot エンドポイントアドレス**フィールドに、bot をホストしているローカル web サーバーを入力して、そのサーバーに追加し `/api/messages` ます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-166">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot and append `/api/messages` to it.</span></span>

    :::image type="content" source="../doc-links/images/bot-config-endpoint-url.png" alt-text="Teams ツールキットで bot エンドポイント URL を構成できる場所を示す図。":::

<span data-ttu-id="04b6a-168">Bot は Teams のメッセージに応答できるようになります。</span><span class="sxs-lookup"><span data-stu-id="04b6a-168">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="04b6a-169">アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="04b6a-169">Run your app</span></span>

<span data-ttu-id="04b6a-170">Bot をホストする URL を設定し、メッセージを処理するように構成します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-170">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="04b6a-171">その後、自分の bot を起動して実行します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-171">It's time to get your bot up and running.</span></span>

1. <span data-ttu-id="04b6a-172">ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-172">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="04b6a-173">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-173">Run `npm start`.</span></span>

<span data-ttu-id="04b6a-174">成功した場合、ボットが自分のアクティビティをリッスンしていることを示す次のようなメッセージが表示され `localhost` ます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-174">If successful, you see something like the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="sideload-your-bot-in-teams"></a><span data-ttu-id="04b6a-175">Teams でボットをサイドロード</span><span class="sxs-lookup"><span data-stu-id="04b6a-175">Sideload your bot in Teams</span></span>

<span data-ttu-id="04b6a-176">Bot を実行している場合は、Teams にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-176">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="04b6a-177">以前に Teams アプリをサイドロードしていない場合は、以下の [手順](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams)を実行します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-177">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="04b6a-178">アプリのサイドロードを許可するアカウントを使用して、Teams クライアントにログインします。</span><span class="sxs-lookup"><span data-stu-id="04b6a-178">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="04b6a-179">[ **アプリ**] を選択し、[ **カスタムアプリのアップロード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-179">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="04b6a-180">アプリプロジェクトフォルダーに移動し `.publish` 、を選択し `Development.zip` ます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-180">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="04b6a-181">[モーダルのインストール] で、[ **追加** ] を選択してアプリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="04b6a-181">In the install modal, select **Add** to install your app.</span></span>

## <a name="test-your-bot"></a><span data-ttu-id="04b6a-182">Bot をテストする</span><span class="sxs-lookup"><span data-stu-id="04b6a-182">Test your bot</span></span>

<span data-ttu-id="04b6a-183">おもしろい部分のために、1対1のチャットで bot に "Hello" と言うことができます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-183">Now for the fun part: Let's say "Hello" to your bot in a one-on-one chat.</span></span>

1. Teams で、左側にある [ **その他**] を選択し :::image type="icon" source="../doc-links/images/teams-client-more.png"::: ます。
1. <span data-ttu-id="04b6a-185">サイドロードの bot を見つけて選択します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-185">Locate and select the bot you just sideloaded.</span></span><br/>
   :::image type="content" source="../doc-links/images/bot-teams-access.png" alt-text="Teams で bot にアクセスする場所を示す図。":::
1. <span data-ttu-id="04b6a-187">[新規作成] ボックスで、 `Hello` メッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-187">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="04b6a-188">Bot は次のようなメッセージに返信します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-188">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../doc-links/images/contoso-chatbot.png" alt-text="ユーザーが Teams の bot に "Hello" と言って、応答を返すことを示すスクリーンショット。":::

> [!NOTE]
> <span data-ttu-id="04b6a-190">Bot をテストした後でコードを変更した場合 (更新など)、 `botActivityHandler.js` その変更が Teams に反映されたことを確認するために、アプリをもう一度実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="04b6a-190">If you make code changes after testing your bot—for example, you update `botActivityHandler.js`—you must run your app again to see those changes reflected in Teams.</span></span>

## <a name="well-done"></a><span data-ttu-id="04b6a-191">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="04b6a-191">Well done</span></span>

<span data-ttu-id="04b6a-192">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="04b6a-192">Congratulations!</span></span> <span data-ttu-id="04b6a-193">ユーザーが1対1で、またはグループ設定 (チャネルとチャット) で通信できる基本的な Teams bot があります。</span><span class="sxs-lookup"><span data-stu-id="04b6a-193">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="04b6a-194">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="04b6a-194">Troubleshooting</span></span>

<span data-ttu-id="04b6a-195">このチュートリアルを完了する際に問題が発生した場合は、次の情報が役立ちます。</span><span class="sxs-lookup"><span data-stu-id="04b6a-195">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="04b6a-196">ツールキットのセットアップが失敗する</span><span class="sxs-lookup"><span data-stu-id="04b6a-196">Toolkit setup fails</span></span>

<span data-ttu-id="04b6a-197">Teams ツールキットを使用してアプリプロジェクトをセットアップするときに、[ **新しい Bot を作成** する] オプションを選択し、Microsoft 365 開発アカウントでログインすると、エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-197">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="04b6a-198">これは認証の問題である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="04b6a-198">This could be an authentication issue.</span></span> <span data-ttu-id="04b6a-199">プロジェクトの設定を完了するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-199">Follow these steps to finish setting up your project.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft Teams** ] を選択 :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: し、[ **サインアウト**] を選択します。
1. <span data-ttu-id="04b6a-201">同じアカウントを使用してログインし、新しい bot を作成することにより、セットアッププロセスを再度実行します。</span><span class="sxs-lookup"><span data-stu-id="04b6a-201">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="04b6a-202">Bot が Teams に接続されていない</span><span class="sxs-lookup"><span data-stu-id="04b6a-202">Bot isn't connected to Teams</span></span>

<span data-ttu-id="04b6a-203">アプリをインストールしたが、bot が動作していない場合は、ボットが[Azure Bot サービスの Teams*チャネル*に接続](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="04b6a-203">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="04b6a-204">これは Teams のチャネルと同じではないことを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="04b6a-204">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="04b6a-205">この場合、チャネルは、Azure Bot サービスが Bot を Teams または他の [サポートされている Microsoft またはサードパーティの通信アプリ](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)に接続する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="04b6a-205">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="04b6a-206">詳細情報</span><span class="sxs-lookup"><span data-stu-id="04b6a-206">Learn more</span></span>

* [<span data-ttu-id="04b6a-207">このサンプルの1つで、他の Teams の bot ができることを確認する (GitHub)</span><span class="sxs-lookup"><span data-stu-id="04b6a-207">See what else Teams bots can do with one of our samples (GitHub)</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="04b6a-208">ボット会話の基本</span><span class="sxs-lookup"><span data-stu-id="04b6a-208">Bot conversation basics</span></span>](../../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="04b6a-209">Teams での Bot 認証</span><span class="sxs-lookup"><span data-stu-id="04b6a-209">Bot authentication in Teams</span></span>](../../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="04b6a-210">Microsoft Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="04b6a-210">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
