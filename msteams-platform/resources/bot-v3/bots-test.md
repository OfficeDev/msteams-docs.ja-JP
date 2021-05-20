---
title: ボットのテストとデバッグ
description: Microsoft Teamsでボットをテストする方法について説明します。
keywords: チームボットテスト
ms.topic: how-to
localization_priority: Normal
ms.date: 03/20/2019
ms.openlocfilehash: 269b0680e45d764cf4cb0269c40d3d202145edb8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566461"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a><span data-ttu-id="e9641-104">Microsoft Teamsボットのテストとデバッグ</span><span class="sxs-lookup"><span data-stu-id="e9641-104">Test and debug your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="e9641-105">ボットをテストする場合は、ボットを実行するコンテキストと、Microsoft Teamsに固有のデータを必要とするボットに追加した機能の両方を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9641-105">When testing your bot you need to take into consideration both the context(s) you want your bot to run in, as well as any functionality you may have added to your bot that requires data specific to Microsoft Teams.</span></span> <span data-ttu-id="e9641-106">ボットのテストに選択したメソッドが、その機能に合っていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e9641-106">Make sure that the method you chose to test your bot aligns with its functionality.</span></span>

## <a name="test-by-uploading-to-teams"></a><span data-ttu-id="e9641-107">Teamsにアップロードしてテストする</span><span class="sxs-lookup"><span data-stu-id="e9641-107">Test by uploading to Teams</span></span>

<span data-ttu-id="e9641-108">ボットをテストする最も包括的な方法は、アプリ パッケージを作成してTeamsにアップロードすることです。</span><span class="sxs-lookup"><span data-stu-id="e9641-108">The most comprehensive way to test your bot is by creating an app package and uploading it to Teams.</span></span> <span data-ttu-id="e9641-109">これは、すべてのスコープでボットが利用できる機能をすべてテストする唯一の方法です。</span><span class="sxs-lookup"><span data-stu-id="e9641-109">This is the only method to test the full functionality available to your bot, across all scopes.</span></span>

<span data-ttu-id="e9641-110">アプリをアップロードするには、2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="e9641-110">There are two methods for uploading your app.</span></span> <span data-ttu-id="e9641-111">[App Studio](~/concepts/build-and-test/app-studio-overview.md)を使用して支援するか、[またはアプリ パッケージを](~/concepts/build-and-test/apps-package.md)手動で作成して[アプリをアップロード](~/concepts/deploy-and-publish/apps-upload.md)することができます。</span><span class="sxs-lookup"><span data-stu-id="e9641-111">You can either use [App Studio](~/concepts/build-and-test/app-studio-overview.md) to help you, or you can manually [create an app package](~/concepts/build-and-test/apps-package.md) and [upload your app](~/concepts/deploy-and-publish/apps-upload.md).</span></span> <span data-ttu-id="e9641-112">マニフェストを変更してアプリを再アップロードする必要がある場合は、変更したアプリ パッケージをアップロードする前に [ボットを削除](#deleting-a-bot-from-teams) する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9641-112">If you need to alter your manifest and re-upload your app, you should [delete your bot](#deleting-a-bot-from-teams) before uploading your altered app package.</span></span>

## <a name="debug-your-bot-locally"></a><span data-ttu-id="e9641-113">ボットをローカルでデバッグする</span><span class="sxs-lookup"><span data-stu-id="e9641-113">Debug your bot locally</span></span>

<span data-ttu-id="e9641-114">開発中にボットをローカルでホストしている場合は、ボットをテストするために [ngrok](https://ngrok.com/) のようなトンネリング サービスを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9641-114">If you are hosting your bot locally during development you'll need to use a tunneling service like [ngrok](https://ngrok.com/) in order to test your bot.</span></span> <span data-ttu-id="e9641-115">ngrok をダウンロードしてインストールしたら、以下のコマンドを実行してトンネリング サービスを開始します。</span><span class="sxs-lookup"><span data-stu-id="e9641-115">Once you've downloaded and installed ngrok, run the below command to start the tunneling service.</span></span> <span data-ttu-id="e9641-116">パスに ngrok を追加する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="e9641-116">You may need to add ngrok to your path.</span></span>

```bash
ngrok http <port> -host-header=localhost:<port>
```

<span data-ttu-id="e9641-117">ngrok が提供する https エンドポイントをアプリ マニフェストで使用します。</span><span class="sxs-lookup"><span data-stu-id="e9641-117">Use the https endpoint provided by ngrok in your app manifest.</span></span> <span data-ttu-id="e9641-118">コマンド ウィンドウを閉じて再起動すると、新しい URL が取得され、ボット エンドポイントのアドレスも更新してその URL を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9641-118">If you close your command window and restart you'll get a new URL, and you'll need to update your bot endpoint address to use that one as well.</span></span>

## <a name="testing-your-bot-without-uploading-to-teams"></a><span data-ttu-id="e9641-119">Teamsにアップロードせずにボットをテストする</span><span class="sxs-lookup"><span data-stu-id="e9641-119">Testing your bot without uploading to Teams</span></span>

<span data-ttu-id="e9641-120">場合によっては、Teamsでアプリとしてインストールせずにボットをテストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9641-120">Occasionally it may be necessary to test your bot without installing it as an app in Teams.</span></span> <span data-ttu-id="e9641-121">以下に、2 つの方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="e9641-121">We provide two methods for doing so below.</span></span> <span data-ttu-id="e9641-122">ボットをアプリとしてインストールせずにボットをテストすると、ボットが利用可能で応答できることを確認できますが、ボットに追加した可能性のあるMicrosoft Teams機能の幅を完全にテストすることはできません。</span><span class="sxs-lookup"><span data-stu-id="e9641-122">Testing your bot without installing it as an app can be useful to ensure your bot is available and responding, however it will not allow you to test the full breadth of Microsoft Teams functionality you may have added to your bot.</span></span> <span data-ttu-id="e9641-123">ボットを完全にテストする必要がある場合は、 [をアップロードしてテスト](#test-by-uploading-to-teams)の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="e9641-123">If you need to fully test your bot, please follow the instructions for [testing by uploading](#test-by-uploading-to-teams).</span></span>

### <a name="use-the-bot-emulator"></a><span data-ttu-id="e9641-124">ボット エミュレーターを使用する</span><span class="sxs-lookup"><span data-stu-id="e9641-124">Use the Bot Emulator</span></span>

<span data-ttu-id="e9641-125">Bot Framework Emulatorは、ボット開発者が、ローカルまたはリモートでボットをテストおよびデバッグできるようにするデスクトップ アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="e9641-125">The Bot Framework Emulator is a desktop application that allows bot developers to test and debug their bots, either locally or remotely.</span></span> <span data-ttu-id="e9641-126">エミュレーターを使用して、ボットとチャットしたり、ボットが送受信するメッセージを調べることができます。</span><span class="sxs-lookup"><span data-stu-id="e9641-126">Using the emulator, you can chat with your bot and inspect the messages that your bot sends and receives.</span></span> <span data-ttu-id="e9641-127">これは、ボットが利用可能で応答していることを確認するのに便利ですが、エミュレーターでは、ボットに追加したTeams固有の機能をテストしたり、ボットからの応答をTeamsでどのようにレンダリングするかを正確に視覚的に表現することはできません。</span><span class="sxs-lookup"><span data-stu-id="e9641-127">This can be useful for verifying that your bot is available and responding, however the emulator will not allow you to test any Teams-specific functionality you've added to your bot, nor will responses from your bot be an accurate visual representation of how they will be rendered in Teams.</span></span> <span data-ttu-id="e9641-128">これらのいずれかのことをテストする必要がある場合は、 [ボットをアップロードすることをお勧めします](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="e9641-128">If you need to test either of those things it is best to [upload your bot](#test-by-uploading-to-teams).</span></span>

<span data-ttu-id="e9641-129">Bot Framework Emulatorの詳細な手順はこちらからご[覧いただけます](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="e9641-129">Complete instructions on the Bot Framework Emulator can be found [here](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).</span></span>

### <a name="talk-to-your-bot-directly-by-id"></a><span data-ttu-id="e9641-130">ID で直接ボットに問い合わせてください</span><span class="sxs-lookup"><span data-stu-id="e9641-130">Talk to your bot directly by Id</span></span>

>[!Important]
><span data-ttu-id="e9641-131">Id によってボットとの会話は、テスト目的でのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="e9641-131">Talking to your bot by Id is intended for testing purposes only.</span></span>

<span data-ttu-id="e9641-132">また、Id を使用してボットとの会話を開始することもできます。これを行うための2つの方法を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="e9641-132">You can also initiate a conversation with your bot by using its Id. Two methods for doing so are given below.</span></span> <span data-ttu-id="e9641-133">これらの方法のいずれかを通じてボットが追加された場合、チャネルの会話ではアドレス指定が可能ではなく、タブやメッセージング拡張機能などの他のMicrosoft Teamsアプリ機能を利用することはできません。</span><span class="sxs-lookup"><span data-stu-id="e9641-133">When a bot has been added through one of these methods it will not be addressable in channel conversations, and you cannot take advantage of other Microsoft Teams app capabilities like tabs or messaging extensions.</span></span>

1. <span data-ttu-id="e9641-134">ボットの [[Bot ダッシュボード](https://dev.botframework.com/bots)] ページの **[チャネル**] で **、[Microsoft Teamsに追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e9641-134">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Channels**, select **Add to Microsoft Teams**.</span></span> <span data-ttu-id="e9641-135">Microsoft Teamsは、あなたのボットとの個人的なチャットで起動します。</span><span class="sxs-lookup"><span data-stu-id="e9641-135">Microsoft Teams will launch with a personal chat with your bot.</span></span>
2. <span data-ttu-id="e9641-136">Microsoft Teams内からボットのアプリ ID を直接参照します。</span><span class="sxs-lookup"><span data-stu-id="e9641-136">Directly reference your bot's app ID from within Microsoft Teams:</span></span>
   * <span data-ttu-id="e9641-137">ボットの [ [ボット ダッシュボード](https://dev.botframework.com/bots) ] ページの **[詳細]** で、ボットの **Microsoft アプリ ID** をコピーします。</span><span class="sxs-lookup"><span data-stu-id="e9641-137">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Details**, copy the **Microsoft App ID** for your bot.</span></span>
  
     ![ボットの AppID を取得する](~/assets/images/bots_appid_botframework.png)
  
   * <span data-ttu-id="e9641-139">Microsoft Teamsの [**チャット**] ウィンドウで、[**チャットの追加**] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="e9641-139">From within Microsoft Teams, on the **Chat** pane, select the **Add chat** icon.</span></span> <span data-ttu-id="e9641-140">**[対象] の場合:** に、ボットの Microsoft アプリ ID を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="e9641-140">For **To:**, paste your bot's Microsoft App ID.</span></span>
  
     ![ボットの AppID のアップロード](~/assets/images/bots_uploading.png)

     <span data-ttu-id="e9641-142">アプリ ID は、ボット名に解決する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9641-142">The app ID should resolve to your bot name.</span></span>

   * <span data-ttu-id="e9641-143">ボットを選択し、メッセージを送信して会話を開始します。</span><span class="sxs-lookup"><span data-stu-id="e9641-143">Select your bot and send a message to initiate a conversation.</span></span>
   * <span data-ttu-id="e9641-144">または、Microsoft Teamsの左上の検索ボックスにボットのアプリ ID を貼り付けることもできます。</span><span class="sxs-lookup"><span data-stu-id="e9641-144">Alternatively, you can paste your bot's app ID in the search box in the top left in Microsoft Teams.</span></span> <span data-ttu-id="e9641-145">検索結果ページで[人]タブに移動してボットを表示し、チャットを開始します。</span><span class="sxs-lookup"><span data-stu-id="e9641-145">In the search results page, navigate to the People tab to see your bot and to start chatting with it.</span></span>

<span data-ttu-id="e9641-146">ボットは `conversationUpdate` 、チームに追加されたボットと同じようにイベントを受け取りますが、オブジェクト内のチーム情報は表示 `channelData` しません。</span><span class="sxs-lookup"><span data-stu-id="e9641-146">Your bot will receive the `conversationUpdate` event just like bots added to a team, but without the team information in the `channelData` object.</span></span>

## <a name="blocking-a-bot-in-personal-chat"></a><span data-ttu-id="e9641-147">パーソナルチャットでボットをブロックする</span><span class="sxs-lookup"><span data-stu-id="e9641-147">Blocking a bot in personal chat</span></span>

<span data-ttu-id="e9641-148">ユーザーは、ボットが個人用チャット メッセージを送信するのをブロックできます。</span><span class="sxs-lookup"><span data-stu-id="e9641-148">Note that users can choose to block your bot from sending personal chat messages.</span></span> <span data-ttu-id="e9641-149">チャットチャンネルでボットを右クリックし、[ **ボットの会話をブロック**] を選択して、この設定を切り替えることができます。</span><span class="sxs-lookup"><span data-stu-id="e9641-149">They may toggle this by right-clicking your bot in the chat channel and choosing **Block bot conversation**.</span></span> <span data-ttu-id="e9641-150">つまり、ボットはメッセージを送信し続けますが、ユーザーはこれらのメッセージを受信しません。</span><span class="sxs-lookup"><span data-stu-id="e9641-150">This means your bots will continue to send messages but the user will not receive those messages.</span></span>

![ボットのブロック](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a><span data-ttu-id="e9641-152">チームからのボットの削除</span><span class="sxs-lookup"><span data-stu-id="e9641-152">Removing a bot from a team</span></span>

<span data-ttu-id="e9641-153">ユーザーは、チーム ビューのボット リストでごみ箱アイコンを選択して、ボットを削除できます。</span><span class="sxs-lookup"><span data-stu-id="e9641-153">Users can delete the bot by choosing the trash-can icon on the bots list in their teams view.</span></span> <span data-ttu-id="e9641-154">これは、そのチームの使用からボットを削除するだけです。個々のユーザーは、個人的なコンテキストで対話することができます。</span><span class="sxs-lookup"><span data-stu-id="e9641-154">Note that this only removes the bot from that team's use; individual users will still be able to interact in personal context.</span></span>

<span data-ttu-id="e9641-155">個人的なコンテキストのボットは Teams、ユーザーが無効にしたり削除したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="e9641-155">Bots in personal context cannot be disabled or removed by a user, short of completely removing the bot from Teams.</span></span>

## <a name="disabling-a-bot-in-teams"></a><span data-ttu-id="e9641-156">Teamsでボットを無効にする</span><span class="sxs-lookup"><span data-stu-id="e9641-156">Disabling a bot in Teams</span></span>

<span data-ttu-id="e9641-157">ボットがメッセージを受信するのを停止するには、Bot ダッシュボードに移動して、Microsoft Teamsチャネルを編集します。</span><span class="sxs-lookup"><span data-stu-id="e9641-157">To stop your bot receiving messages, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="e9641-158">[Microsoft Teams **で有効にする]** オプションをオフにします。</span><span class="sxs-lookup"><span data-stu-id="e9641-158">Clear the **Enable on Microsoft Teams** option.</span></span> <span data-ttu-id="e9641-159">これにより、ユーザーはボットとやり取りできなくなりますが、引き続き検出可能であり、ユーザーは引き続きボットをチームに追加できます。</span><span class="sxs-lookup"><span data-stu-id="e9641-159">This prevents users from interacting with the bot, but it will still be discoverable and users will still be able to add it to teams.</span></span>

## <a name="deleting-a-bot-from-teams"></a><span data-ttu-id="e9641-160">Teamsからボットを削除する</span><span class="sxs-lookup"><span data-stu-id="e9641-160">Deleting a bot from Teams</span></span>

<span data-ttu-id="e9641-161">Teamsからボットを完全に削除するには、Bot ダッシュボードに移動してMicrosoft Teamsチャネルを編集します。</span><span class="sxs-lookup"><span data-stu-id="e9641-161">To remove your bot completely from Teams, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="e9641-162">下部にある **[削除]** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="e9641-162">Choose the **Delete** button at the bottom.</span></span> <span data-ttu-id="e9641-163">これにより、ユーザーがボットを検出、追加、または操作できなくなります。</span><span class="sxs-lookup"><span data-stu-id="e9641-163">This prevents users from discovering, adding, or interacting with your bot.</span></span> <span data-ttu-id="e9641-164">他のユーザーのTeamsインスタンスからボットが削除されることはありませんが、ボットの機能も停止します。</span><span class="sxs-lookup"><span data-stu-id="e9641-164">Note that this does not remove the bot from other users' Teams instances, although it will cease functioning for them as well.</span></span>

## <a name="removing-your-bot-from-appsource"></a><span data-ttu-id="e9641-165">アプリソースからボットを削除する</span><span class="sxs-lookup"><span data-stu-id="e9641-165">Removing your bot from AppSource</span></span>

<span data-ttu-id="e9641-166">AppSource (以前はストアOffice) で Teams アプリからボットを削除する場合は、アプリ マニフェストからボットを削除し、検証のためにアプリを再送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9641-166">If you want to remove your bot from your Teams app in AppSource (previously Office Store), you must remove the bot from your app manifest and resubmit your app for validation.</span></span> <span data-ttu-id="e9641-167">詳細については、「 [Microsoft Teams アプリを AppSource に発行する](~/concepts/deploy-and-publish/apps-publish.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e9641-167">For more information, see [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span>
