---
title: まず、メッセージング拡張機能を構築する
author: heath-hamilton
description: Microsoft Teams ツールキットを使用して、Microsoft Teams メッセージング拡張機能をすばやく作成できます。
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: b19856eacee866ebbc89f21ac12575f1392918b3
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452835"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="eb427-103">Microsoft Teams のメッセージング拡張機能を構築する</span><span class="sxs-lookup"><span data-stu-id="eb427-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="eb427-104">Teams *メッセージング拡張機能*には、 [検索コマンド](../messaging-extensions/how-to/search-commands/define-search-command.md) と [アクションコマンド](../messaging-extensions/how-to/action-commands/define-action-command.md)の2種類があります。</span><span class="sxs-lookup"><span data-stu-id="eb427-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="eb427-105">このレッスンでは、 *検索コマンド* ( *検索ベースのメッセージング拡張機能*とも呼ばれます) を作成します。これは、外部コンテンツを検索して Teams で共有するためのショートカットです。</span><span class="sxs-lookup"><span data-stu-id="eb427-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="eb427-106">ユーザーは、[ [Teams の作成] または [コマンド] ボックス](../messaging-extensions/what-are-messaging-extensions.md)から検索コマンドにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="eb427-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="eb427-107">自分の割り当て</span><span class="sxs-lookup"><span data-stu-id="eb427-107">Your assignment</span></span>

<span data-ttu-id="eb427-108">組織のヘルプデスクは Teams を通じてユーザーと通信しますが、チケットは別のシステムに存在します。</span><span class="sxs-lookup"><span data-stu-id="eb427-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="eb427-109">これは、サポートスタッフが常にアプリ間を行き来する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="eb427-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="eb427-110">Teams の簡単な検索ベースのメッセージング拡張機能を作成することによって、この大幅な切り替えを減らす方法を調査します。</span><span class="sxs-lookup"><span data-stu-id="eb427-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="eb427-111">学習内容</span><span class="sxs-lookup"><span data-stu-id="eb427-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="eb427-112">Microsoft Teams Toolkit for Visual Studio Code を使用して、アプリプロジェクトとメッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="eb427-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="eb427-113">メッセージング拡張機能に関連するアプリマニフェストのプロパティと一部のスキャフォールディングを特定する</span><span class="sxs-lookup"><span data-stu-id="eb427-113">Identify the app manifest properties and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="eb427-114">アプリをローカルでホストする</span><span class="sxs-lookup"><span data-stu-id="eb427-114">Host an app locally</span></span>
> * <span data-ttu-id="eb427-115">メッセージング拡張機能の bot を構成する</span><span class="sxs-lookup"><span data-stu-id="eb427-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="eb427-116">Teams でメッセージング拡張機能をサイドロードおよびテストする</span><span class="sxs-lookup"><span data-stu-id="eb427-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eb427-117">はじめに</span><span class="sxs-lookup"><span data-stu-id="eb427-117">Before you begin</span></span>

<span data-ttu-id="eb427-118">まだお持ちでない場合は、 [Teams 開発の前提条件を理解し、インストール](build-first-app-overview.md#get-prerequisites)してください。</span><span class="sxs-lookup"><span data-stu-id="eb427-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="eb427-119">1. アプリプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="eb427-119">1. Create your app project</span></span>

<span data-ttu-id="eb427-120">Microsoft Teams Toolkit は、メッセージング拡張機能に次のコンポーネントをセットアップするのに役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="eb427-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="eb427-121">メッセージング拡張機能に関連する**アプリマニフェストとスキャフォールディング**</span><span class="sxs-lookup"><span data-stu-id="eb427-121">**App manifest and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="eb427-122">Microsoft Azure Bot サービスに自動的に登録されるメッセージング拡張機能の**Bot**</span><span class="sxs-lookup"><span data-stu-id="eb427-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="eb427-123">以前に Teams アプリプロジェクトを作成していない場合は、 [以下の手順](../build-your-first-app/build-and-run.md) に従って、プロジェクトについて詳しく説明することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="eb427-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
1. <span data-ttu-id="eb427-125">Teams アプリの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="eb427-125">Enter a name for your Teams app.</span></span> <span data-ttu-id="eb427-126">(これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)</span><span class="sxs-lookup"><span data-stu-id="eb427-126">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="eb427-127">[ **機能の追加** ] 画面で、[ **メッセージング内線番号** ] を選択し、[ **次へ**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="eb427-127">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="eb427-128">[ **メッセージング拡張機能の構成** ] 画面で、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="eb427-128">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="eb427-129">メッセージング拡張機能の種類に対して **検索ベース** のオプションのみを選択します。</span><span class="sxs-lookup"><span data-stu-id="eb427-129">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="eb427-130">[ **新しい Bot を作成** し、 **ログイン** する] を選択して、Microsoft 365 開発アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="eb427-130">Select **Create a new Bot** and **Login** to sign in with your Microsoft 365 development account.</span></span>
    1. <span data-ttu-id="eb427-131">Bot ID とパスワードを保存します (これは後で必要になります)。</span><span class="sxs-lookup"><span data-stu-id="eb427-131">Store your bot ID and password (you need this a little later).</span></span>
    1. <span data-ttu-id="eb427-132">オプションBot のカスタム名を入力し、[ **作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="eb427-132">(Optional) Enter a custom name for your bot and select **Create**.</span></span> <span data-ttu-id="eb427-133">(これは、既に指定した Teams アプリの名前ではありません)。</span><span class="sxs-lookup"><span data-stu-id="eb427-133">(This is not the name of the Teams app you already specified.)</span></span>
    1. <span data-ttu-id="eb427-134">ここでは、リンク unfurling オプションに [ **いいえ** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="eb427-134">For now, select **No** for the link unfurling option.</span></span></br>
:::image type="content" source="../assets/images/build-your-first-app/choose-me-search.png" alt-text="Teams ツールキットで、メッセージング拡張機能のために新しい bot を作成するために Microsoft 365 アカウントにログインする方法を示す図。":::
1. <span data-ttu-id="eb427-136">画面の下部にある [ **完了** ] を選択して、プロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="eb427-136">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="eb427-137">2. 関連するアプリプロジェクトコンポーネントを特定する</span><span class="sxs-lookup"><span data-stu-id="eb427-137">2. Identify relevant app project components</span></span>

<span data-ttu-id="eb427-138">Teams ツールキットを使用してプロジェクトを作成すると、アプリマニフェストとスキャフォールディングの多くが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="eb427-138">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="eb427-139">アプリマニフェスト</span><span class="sxs-lookup"><span data-stu-id="eb427-139">App manifest</span></span>

<span data-ttu-id="eb427-140">アプリケーションマニフェスト ( `manifest.json` プロジェクトのディレクトリ内のファイル) の次のスニペットは、 `.publish` メッセージング拡張機能に関連するプロパティと既定値を示しています。</span><span class="sxs-lookup"><span data-stu-id="eb427-140">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows the properties and default values relevant to messaging extensions.</span></span>

```JSON
"composeExtensions": [
    {
        "botId": "{botId0}",
        "canUpdateConfiguration": true,
        "commands": [
            {
                "id": "searchQuery",
                "context": [
                    "compose",
                    "commandBox"
                ],
                "description": "Test command to run query",
                "title": "Search",
                "type": "query",
                "parameters": [
                    {
                        "name": "searchQuery",
                        "title": "Search Query",
                        "description": "Your search query",
                        "inputType": "text"
                    }
                ]
            }
        ]
    }
],
```

<span data-ttu-id="eb427-141">ツールキットによって作成されたプロパティのいくつかを理解してみましょう。</span><span class="sxs-lookup"><span data-stu-id="eb427-141">Let's understand some of the properties the toolkit created for you.</span></span> <span data-ttu-id="eb427-142">(サポートされているプロパティの完全な一覧を参照してください [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) )。</span><span class="sxs-lookup"><span data-stu-id="eb427-142">(See the full list of supported [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) properties.)</span></span>

* <span data-ttu-id="eb427-143">`botId`: 作成した bot の ID。プロジェクトを設定します。</span><span class="sxs-lookup"><span data-stu-id="eb427-143">`botId`: The ID of the bot you created setting up your project.</span></span> <span data-ttu-id="eb427-144">(に保存されている場合は、の `{botId0}` 実際の ID を検索でき `Development.env` ます)。</span><span class="sxs-lookup"><span data-stu-id="eb427-144">(Stored in `{botId0}`, you can find the actual ID in `Development.env`.)</span></span>
* <span data-ttu-id="eb427-145">`commands`: メッセージング拡張機能で使用可能なコマンド。</span><span class="sxs-lookup"><span data-stu-id="eb427-145">`commands`: Available commands for the messaging extension.</span></span> <span data-ttu-id="eb427-146">ツールキットには、検索コマンドのためのスキャフォールディングが用意されていました。</span><span class="sxs-lookup"><span data-stu-id="eb427-146">The toolkit provided you scaffolding for a search command.</span></span>
* <span data-ttu-id="eb427-147">`context`: ユーザーがメッセージング拡張機能を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="eb427-147">`context`: Where users can invoke the messaging extension.</span></span> <span data-ttu-id="eb427-148">この場合は、Teams の作成またはコマンドボックスからメッセージング拡張機能を起動できます。</span><span class="sxs-lookup"><span data-stu-id="eb427-148">In this case, you can launch the messaging extension from the Teams compose or command box.</span></span>
* <span data-ttu-id="eb427-149">`description`: UI ヘルプテキストコマンドの機能または使用方法を示します。</span><span class="sxs-lookup"><span data-stu-id="eb427-149">`description`: UI help text indicating what the command does or how to use it.</span></span>
* <span data-ttu-id="eb427-150">`parameters`: コマンドが受け付けるすべてのパラメーターが含まれています (少なくとも1つは必要です。最大5個を持つことができます)。</span><span class="sxs-lookup"><span data-stu-id="eb427-150">`parameters`: Includes all parameters a command accepts (you must have at least one and can have up to five).</span></span>
* <span data-ttu-id="eb427-151">`parameters.description`: パラメーターの目的または入力例を説明する UI ヘルプテキスト。</span><span class="sxs-lookup"><span data-stu-id="eb427-151">`parameters.description`: UI help text describing the parameter's purpose or example input.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="eb427-152">アプリのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="eb427-152">App scaffolding</span></span>

<span data-ttu-id="eb427-153">アプリのスキャフォールディングには、 `.env` プロジェクトのルートディレクトリにあるファイルが含まれています。このファイルには、メッセージング拡張機能の bot の ID とパスワードが格納されています。</span><span class="sxs-lookup"><span data-stu-id="eb427-153">The app scaffolding includes a `.env` file, located in the root directory of your project, which stores the ID and password of your messaging extension's bot.</span></span>

<span data-ttu-id="eb427-154">また、ルートディレクトリには、 `botActivityHandler.js` メッセージング拡張機能 (または、技術的には [メッセージング拡張機能](#4-configure-the-bot-for-your-messaging-extension)) が Teams の検索クエリに応答する方法を処理するためのファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="eb427-154">Also in the root directory, there's a `botActivityHandler.js` file for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="eb427-155">3. アプリへのセキュリティで保護されたトンネルをセットアップする</span><span class="sxs-lookup"><span data-stu-id="eb427-155">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="eb427-156">テストを目的として、ローカル web サーバーでメッセージング拡張機能をホストします (ポート 3978)。</span><span class="sxs-lookup"><span data-stu-id="eb427-156">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="eb427-157">ターミナルで、を実行 `ngrok http -host-header=rewrite 3978` します。</span><span class="sxs-lookup"><span data-stu-id="eb427-157">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="eb427-158">Teams で HTTPS 接続が必要なため、出力に HTTPS URL をコピーします。</span><span class="sxs-lookup"><span data-stu-id="eb427-158">Copy the HTTPS URL in the output since Teams requires HTTPS connections.</span></span>
1. <span data-ttu-id="eb427-159">ディレクトリで `.publish` 、を開き `Development.env` ます。</span><span class="sxs-lookup"><span data-stu-id="eb427-159">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="eb427-160">値を `baseUrl0` コピーした URL に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="eb427-160">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="eb427-161">(たとえば、 `baseUrl0=http://localhost:3000` をに変更 `baseUrl0=https://85528b2b3ca5.ngrok.io` します)。</span><span class="sxs-lookup"><span data-stu-id="eb427-161">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="eb427-162">アプリのマニフェストは、メッセージング拡張機能によって使用される bot をホストしている場所を指しています。</span><span class="sxs-lookup"><span data-stu-id="eb427-162">Your app manifest is pointing to where you're hosting the bot used by the messaging extension.</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="eb427-163">4. メッセージング拡張機能の bot を構成する</span><span class="sxs-lookup"><span data-stu-id="eb427-163">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="eb427-164">メッセージング拡張機能は、ボットに依存して、チームからのユーザー要求をホストされたサービスに送信して処理します。</span><span class="sxs-lookup"><span data-stu-id="eb427-164">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span>

<span data-ttu-id="eb427-165">ボットは、Teams ツールキットを使用してアプリをセットアップするときに実行された Azure Bot サービスに登録されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="eb427-165">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

### <a name="specify-your-bot-id-and-password"></a><span data-ttu-id="eb427-166">Bot ID とパスワードを指定する</span><span class="sxs-lookup"><span data-stu-id="eb427-166">Specify your bot ID and password</span></span>

<span data-ttu-id="eb427-167">Bot が Azure Bot サービスに登録されると、Teams アプリが知っておく必要がある ID とパスワードが割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="eb427-167">When your bot is registered with the Azure Bot Service, it's assigned an ID and password that your Teams app must know about.</span></span>

1. <span data-ttu-id="eb427-168">ツールキットのセットアップ時に保存した bot ID とパスワードを見つけます。</span><span class="sxs-lookup"><span data-stu-id="eb427-168">Locate the bot ID and password you stored during toolkit setup.</span></span>
1. <span data-ttu-id="eb427-169">ルートディレクトリで、ファイルを開き `.env` ます。</span><span class="sxs-lookup"><span data-stu-id="eb427-169">In your root directory, open the `.env` file.</span></span>
1. <span data-ttu-id="eb427-170">Bot ID とパスワードを `BotId` それぞれおよびプロパティに設定し `BotPassword` ます。</span><span class="sxs-lookup"><span data-stu-id="eb427-170">Set your bot ID and password to the `BotId` and `BotPassword` properties, respectively.</span></span>

### <a name="add-the-bot-endpoint-address"></a><span data-ttu-id="eb427-171">Bot エンドポイントアドレスを追加する</span><span class="sxs-lookup"><span data-stu-id="eb427-171">Add the bot endpoint address</span></span>

<span data-ttu-id="eb427-172">メッセージング拡張機能で検索クエリを受信して処理するには、ボットエンドポイントの URL を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="eb427-172">You must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="eb427-173">通常、URL はのように `https://HOST_URL/api/messages` なります。</span><span class="sxs-lookup"><span data-stu-id="eb427-173">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="eb427-174">これは Teams ツールキットですばやく構成できます。</span><span class="sxs-lookup"><span data-stu-id="eb427-174">You can configure this quickly in the Teams Toolkit.</span></span>

1. Visual Studio Code で、左側のアクティビティバーで [ **Microsoft teams** ] を選択し、 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: [ **microsoft Teams ツールキットを開く**] を選択します。
1. <span data-ttu-id="eb427-176">[ **ボット management > 既存の bot 登録** ] に移動し、セットアップ時に作成した bot を選択します。</span><span class="sxs-lookup"><span data-stu-id="eb427-176">Go to **Bot management > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="eb427-177">**Bot エンドポイントアドレス**フィールドに、bot (値) をホストしているローカル web サーバーを入力 `baseUrl10` し、 `/api/messages` それに追加します。</span><span class="sxs-lookup"><span data-stu-id="eb427-177">In the **Bot endpoint address** field, enter the local web server where you're hosting the bot (`baseUrl10` value) and append `/api/messages` to it.</span></span>

<span data-ttu-id="eb427-178">Bot は、メッセージング拡張機能でクエリを処理できるようになります。</span><span class="sxs-lookup"><span data-stu-id="eb427-178">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-run-your-app"></a><span data-ttu-id="eb427-179">5. アプリを実行する</span><span class="sxs-lookup"><span data-stu-id="eb427-179">5. Run your app</span></span>

<span data-ttu-id="eb427-180">メッセージング拡張機能をホストする URL を設定し、検索を処理するように構成します。</span><span class="sxs-lookup"><span data-stu-id="eb427-180">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="eb427-181">アプリを起動して実行します。</span><span class="sxs-lookup"><span data-stu-id="eb427-181">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="eb427-182">ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。</span><span class="sxs-lookup"><span data-stu-id="eb427-182">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="eb427-183">`npm start` を実行します。</span><span class="sxs-lookup"><span data-stu-id="eb427-183">Run `npm start`.</span></span>

<span data-ttu-id="eb427-184">成功した場合、次のメッセージが表示されます。メッセージング拡張サービスが自分のアクティビティをリッスンしていることを示し `localhost` ます。</span><span class="sxs-lookup"><span data-stu-id="eb427-184">If successful, you see something like the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="eb427-185">サイドロード Teams でのメッセージング拡張機能の作成</span><span class="sxs-lookup"><span data-stu-id="eb427-185">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="eb427-186">メッセージング拡張機能が実行されている状態で、Teams にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="eb427-186">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="eb427-187">以前に Teams アプリをサイドロードしていない場合は、以下の [手順](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams)を実行します。</span><span class="sxs-lookup"><span data-stu-id="eb427-187">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="eb427-188">アプリのサイドロードを許可するアカウントを使用して、Teams クライアントにログインします。</span><span class="sxs-lookup"><span data-stu-id="eb427-188">Log in to the Teams client with your account that allows app sideloading.</span></span>
1. <span data-ttu-id="eb427-189">[ **アプリ**] を選択し、[ **カスタムアプリのアップロード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="eb427-189">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="eb427-190">アプリプロジェクトフォルダーに移動し `.publish` 、を選択し `Development.zip` ます。</span><span class="sxs-lookup"><span data-stu-id="eb427-190">Go to your app project `.publish` folder and select `Development.zip`.</span></span>
1. <span data-ttu-id="eb427-191">[モーダルのインストール] で、[ **追加** ] を選択してアプリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="eb427-191">In the install modal, select **Add** to install your app.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="eb427-192">7. メッセージング拡張機能をテストする</span><span class="sxs-lookup"><span data-stu-id="eb427-192">7. Test your messaging extension</span></span>

<span data-ttu-id="eb427-193">Teams チャットでのメッセージング拡張機能のしくみについて説明します。</span><span class="sxs-lookup"><span data-stu-id="eb427-193">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="eb427-194">新しいチャットを開始します。</span><span class="sxs-lookup"><span data-stu-id="eb427-194">Start a new chat.</span></span> [新規作成] ボックスで、[ **その他**] を選択し、 :::image type="icon" source="../assets/icons/teams-client-more.png"::: サイドロードしたばかりのメッセージング拡張アプリを選択します。<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-access.png" alt-text="Teams ツールキットで、メッセージング拡張機能のために新しい bot を作成するために Microsoft 365 アカウントにログインする方法を示す図。":::
1. <span data-ttu-id="eb427-197">何らかの検索を試してみてください (たとえば、「チケット」)。</span><span class="sxs-lookup"><span data-stu-id="eb427-197">Try searching for something (for example, "Tickets").</span></span> <span data-ttu-id="eb427-198">アプリが動作している場合は、サンプルの検索結果が表示されます (後で自分で追加することができます)。</span><span class="sxs-lookup"><span data-stu-id="eb427-198">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Teams ツールキットで、メッセージング拡張機能のために新しい bot を作成するために Microsoft 365 アカウントにログインする方法を示す図。":::

## <a name="well-done"></a><span data-ttu-id="eb427-200">よくやりましたね</span><span class="sxs-lookup"><span data-stu-id="eb427-200">Well done</span></span>

<span data-ttu-id="eb427-201">おめでとうございます!</span><span class="sxs-lookup"><span data-stu-id="eb427-201">Congratulations!</span></span> <span data-ttu-id="eb427-202">[作成] または [コマンド] ボックスで外部コンテンツを検索するように設定されている基本的な Teams メッセージング拡張機能があります。</span><span class="sxs-lookup"><span data-stu-id="eb427-202">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb427-203">次の手順</span><span class="sxs-lookup"><span data-stu-id="eb427-203">Next steps</span></span>

<span data-ttu-id="eb427-204">次のページを参照して続行し、完全な機能を備えたメッセージング拡張機能を構築します。</span><span class="sxs-lookup"><span data-stu-id="eb427-204">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="eb427-205">サービスに関連する[検索コマンドを定義](../messaging-extensions/how-to/search-commands/define-search-command.md)します。</span><span class="sxs-lookup"><span data-stu-id="eb427-205">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="eb427-206">[ユーザーの検索に応答](../messaging-extensions/how-to/search-commands/respond-to-search.md)するようにサービスを構成します。</span><span class="sxs-lookup"><span data-stu-id="eb427-206">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="eb427-207">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="eb427-207">Troubleshooting</span></span>

<span data-ttu-id="eb427-208">このチュートリアルを完了する際に問題が発生した場合は、次の情報が役立ちます。</span><span class="sxs-lookup"><span data-stu-id="eb427-208">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="toolkit-setup-fails"></a><span data-ttu-id="eb427-209">ツールキットのセットアップが失敗する</span><span class="sxs-lookup"><span data-stu-id="eb427-209">Toolkit setup fails</span></span>

<span data-ttu-id="eb427-210">Teams ツールキットを使用してアプリプロジェクトをセットアップするときに、[ **新しい Bot を作成** する] オプションを選択し、Microsoft 365 開発アカウントでログインすると、エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="eb427-210">While setting up your app project with the Teams Toolkit, you get an error after selecting the **Create a new Bot** option and logging in with your Microsoft 365 development account.</span></span>

<span data-ttu-id="eb427-211">これは認証の問題である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="eb427-211">This could be an authentication issue.</span></span> <span data-ttu-id="eb427-212">プロジェクトの設定を完了するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="eb427-212">Follow these steps to finish setting up your project.</span></span>

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft Teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **サインアウト**] を選択します。
1. <span data-ttu-id="eb427-214">同じアカウントを使用してログインし、新しい bot を作成することにより、セットアッププロセスを再度実行します。</span><span class="sxs-lookup"><span data-stu-id="eb427-214">Go through the setup process again by logging in with the same account and creating a new bot.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="eb427-215">Bot が Teams に接続されていない</span><span class="sxs-lookup"><span data-stu-id="eb427-215">Bot isn't connected to Teams</span></span>

<span data-ttu-id="eb427-216">アプリをインストールしたが動作していない場合は、メッセージング拡張機能の bot が[Azure Bot サービスの Teams*チャネル*に接続](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="eb427-216">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="eb427-217">これは Teams のチャネルと同じではないことを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="eb427-217">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="eb427-218">この場合、チャネルは、Azure Bot サービスが Bot を Teams または他の [サポートされている Microsoft またはサードパーティの通信アプリ](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)に接続する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="eb427-218">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="eb427-219">詳細情報</span><span class="sxs-lookup"><span data-stu-id="eb427-219">Learn more</span></span>

* [<span data-ttu-id="eb427-220">Link unfurling フィーチャーを含める</span><span class="sxs-lookup"><span data-stu-id="eb427-220">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="eb427-221">認証を追加する</span><span class="sxs-lookup"><span data-stu-id="eb427-221">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="eb427-222">アクションベースのメッセージング拡張機能を作成する</span><span class="sxs-lookup"><span data-stu-id="eb427-222">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="eb427-223">Microsoft Bot フレームワーク</span><span class="sxs-lookup"><span data-stu-id="eb427-223">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
