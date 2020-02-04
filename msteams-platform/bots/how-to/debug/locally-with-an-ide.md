---
title: Bot をローカルでテストおよびデバッグする
author: clearab
description: IDE でボットをローカルにテストおよびデバッグする
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 8494302b41e33910cb33f8c6889d82505b703577
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674758"
---
# <a name="test-and-debug-your-bot-locally"></a><span data-ttu-id="0f8d1-103">Bot をローカルでテストおよびデバッグする</span><span class="sxs-lookup"><span data-stu-id="0f8d1-103">Test and debug your bot locally</span></span>

<span data-ttu-id="0f8d1-104">Bot をテストする際には、bot が実行するコンテキストと、Microsoft Teams に固有のデータが必要なすべての機能について考慮することが必要になります。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-104">When testing your bot you need to take into consideration both the context(s) you want your bot to run in, as well as any functionality you may have added to your bot that requires data specific to Microsoft Teams.</span></span> <span data-ttu-id="0f8d1-105">Bot をテストするために選択した方法が、その機能に合っていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-105">Make sure that the method you chose to test your bot aligns with its functionality.</span></span>

## <a name="test-by-uploading-to-teams"></a><span data-ttu-id="0f8d1-106">Teams にアップロードしてテストする</span><span class="sxs-lookup"><span data-stu-id="0f8d1-106">Test by uploading to Teams</span></span>

<span data-ttu-id="0f8d1-107">Bot をテストする最も包括的な方法は、アプリパッケージを作成し、それを Teams にアップロードすることです。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-107">The most comprehensive way to test your bot is by creating an app package and uploading it to Teams.</span></span> <span data-ttu-id="0f8d1-108">これは、すべてのスコープで bot が使用できる完全な機能をテストする唯一の方法です。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-108">This is the only method to test the full functionality available to your bot, across all scopes.</span></span>

<span data-ttu-id="0f8d1-109">アプリをアップロードするには、2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-109">There are two methods for uploading your app.</span></span> <span data-ttu-id="0f8d1-110">アプリ[Studio](~/concepts/build-and-test/app-studio-overview.md)を使用して支援するか、アプリ[パッケージ](~/concepts/build-and-test/apps-package.md)を手動で作成し[てアプリをアップロード](~/concepts/deploy-and-publish/apps-upload.md)することができます。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-110">You can either use [App Studio](~/concepts/build-and-test/app-studio-overview.md) to help you, or you can manually [create an app package](~/concepts/build-and-test/apps-package.md) and [upload your app](~/concepts/deploy-and-publish/apps-upload.md).</span></span> <span data-ttu-id="0f8d1-111">マニフェストを変更してアプリを再アップロードする必要がある場合は、変更したアプリパッケージをアップロードする前に[bot を削除](#deleting-a-bot-from-teams)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-111">If you need to alter your manifest and re-upload your app, you should [delete your bot](#deleting-a-bot-from-teams) before uploading your altered app package.</span></span>

## <a name="debug-your-bot-locally"></a><span data-ttu-id="0f8d1-112">Bot をローカルでデバッグする</span><span class="sxs-lookup"><span data-stu-id="0f8d1-112">Debug your bot locally</span></span>

<span data-ttu-id="0f8d1-113">開発時にボットをローカルにホストしている場合は、bot をテストするために、 [ngrok](https://ngrok.com/)のようなトンネリングサービスを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-113">If you are hosting your bot locally during development you'll need to use a tunneling service like [ngrok](https://ngrok.com/) in order to test your bot.</span></span> <span data-ttu-id="0f8d1-114">Ngrok をダウンロードしてインストールしたら、次のコマンドを実行してトンネリングサービスを開始します (パスに ngrok を追加する必要がある場合があります)。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-114">Once you've downloaded and installed ngrok, run the below command to start the tunneling service (you may need to add ngrok to your path).</span></span>

```bash
ngrok http <port> -host-header=localhost:<port>
```

<span data-ttu-id="0f8d1-115">アプリのマニフェストで ngrok によって提供される https エンドポイントを使用します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-115">Use the https endpoint provided by ngrok in your app manifest.</span></span> <span data-ttu-id="0f8d1-116">コマンドウィンドウを閉じて再起動すると、新しい URL が表示されます。また、そのいずれかを使用するには、bot エンドポイントのアドレスも更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-116">If you close your command window and restart you'll get a new URL, and you'll need to update your bot endpoint address to use that one as well.</span></span>

## <a name="testing-your-bot-without-uploading-to-teams"></a><span data-ttu-id="0f8d1-117">Teams にアップロードせずに bot をテストする</span><span class="sxs-lookup"><span data-stu-id="0f8d1-117">Testing your bot without uploading to Teams</span></span>

<span data-ttu-id="0f8d1-118">場合によっては、ボットをアプリとして Teams にインストールせずにテストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-118">Occasionally it may be necessary to test your bot without installing it as an app in Teams.</span></span> <span data-ttu-id="0f8d1-119">これを行うには、次の2つの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-119">We provide two methods for doing so below.</span></span> <span data-ttu-id="0f8d1-120">Bot がアプリとしてインストールされていない状態でテストすると、bot が利用可能で応答していることを確認するのに役立ちます。ただし、bot に追加した広範な Microsoft Teams 機能をテストすることはできません。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-120">Testing your bot without installing it as an app can be useful to ensure your bot is available and responding, however it will not allow you to test the full breadth of Microsoft Teams functionality you may have added to your bot.</span></span> <span data-ttu-id="0f8d1-121">Bot を完全にテストする必要がある場合は、「」の手順に従って、をアップロードして[テスト](#test-by-uploading-to-teams)してください。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-121">If you need to fully test your bot, please follow the instructions for [testing by uploading](#test-by-uploading-to-teams).</span></span>

### <a name="use-the-bot-emulator"></a><span data-ttu-id="0f8d1-122">Bot エミュレーターを使用する</span><span class="sxs-lookup"><span data-stu-id="0f8d1-122">Use the Bot Emulator</span></span>

<span data-ttu-id="0f8d1-123">Bot フレームワークエミュレーターは、ボット開発者がローカルまたはリモートでボットをテストしてデバッグできるようにするデスクトップアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-123">The Bot Framework Emulator is a desktop application that allows bot developers to test and debug their bots, either locally or remotely.</span></span> <span data-ttu-id="0f8d1-124">エミュレーターを使用すると、ボットとチャットし、ボットが送受信するメッセージを検査できます。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-124">Using the emulator, you can chat with your bot and inspect the messages that your bot sends and receives.</span></span> <span data-ttu-id="0f8d1-125">これは、ボットが利用可能で応答していることを確認するのに便利ですが、お客様が bot に追加した Teams 固有の機能をテストすることはできません。また、お客様が bot からの応答を正確にビジュアルに表示することはできません。Teams でレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-125">This can be useful for verifying that your bot is available and responding, however the emulator will not allow you to test any Teams-specific functionality you've added to your bot, nor will responses from your bot be an accurate visual representation of how they will be rendered in Teams.</span></span> <span data-ttu-id="0f8d1-126">これらのいずれかをテストする必要がある場合は[、bot をアップロード](#test-by-uploading-to-teams)することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-126">If you need to test either of those things it is best to [upload your bot](#test-by-uploading-to-teams).</span></span>

<span data-ttu-id="0f8d1-127">Bot フレームワークエミュレーターの完全な手順については、[こちら](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-127">Complete instructions on the Bot Framework Emulator can be found [here](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0).</span></span>

### <a name="talk-to-your-bot-directly-by-id"></a><span data-ttu-id="0f8d1-128">Id で自分の bot と直接会話する</span><span class="sxs-lookup"><span data-stu-id="0f8d1-128">Talk to your bot directly by Id</span></span>

>[!Important]
><span data-ttu-id="0f8d1-129">Id で bot と会話することは、基本的なテストのみを目的としています。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-129">Talking to your bot by Id is intended for basic testing purposes only.</span></span> <span data-ttu-id="0f8d1-130">Bot に追加した Teams 固有の機能は機能しません。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-130">Any Teams-specific functionality you've added to your bot will not work.</span></span>

<span data-ttu-id="0f8d1-131">Id を使用して、bot との会話を開始することもできます。そのためには、次の2つのメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-131">You can also initiate a conversation with your bot by using its Id. Two methods for doing so are given below.</span></span> <span data-ttu-id="0f8d1-132">これらのいずれかの方法で bot が追加されている場合は、チャネル会話ではアドレス指定できないため、タブやメッセージング拡張機能などの他の Microsoft Teams アプリ機能を利用することはできません。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-132">When a bot has been added through one of these methods it will not be addressable in channel conversations, and you cannot take advantage of other Microsoft Teams app capabilities like tabs or messaging extensions.</span></span>

1. <span data-ttu-id="0f8d1-133">Bot の[Bot ダッシュボード](https://dev.botframework.com/bots)ページの [**チャネル**] で、[ **Microsoft Teams に追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-133">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Channels**, select **Add to Microsoft Teams**.</span></span> <span data-ttu-id="0f8d1-134">Microsoft Teams は、お客様の bot との個人チャットを使用して起動します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-134">Microsoft Teams will launch with a personal chat with your bot.</span></span>
2. <span data-ttu-id="0f8d1-135">Microsoft Teams 内から bot のアプリ ID を直接参照します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-135">Directly reference your bot's app ID from within Microsoft Teams:</span></span>
   * <span data-ttu-id="0f8d1-136">Bot の[Bot ダッシュボード](https://dev.botframework.com/bots)ページで、[**詳細**] の下にある BOT の**Microsoft アプリ ID**をコピーします。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-136">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Details**, copy the **Microsoft App ID** for your bot.</span></span>
  
     ![Bot の AppID を取得する](~/assets/images/bots_appid_botframework.png)
  
   * <span data-ttu-id="0f8d1-138">Microsoft Teams で、**チャット**ウィンドウから [**チャットの追加**] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-138">From within Microsoft Teams, on the **Chat** pane, select the **Add chat** icon.</span></span> <span data-ttu-id="0f8d1-139">[**宛先**] に、ボットの MICROSOFT アプリ ID を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-139">For **To:**, paste your bot's Microsoft App ID.</span></span>
  
     ![Bot の AppID を取得する](~/assets/images/bots_uploading.png)

     <span data-ttu-id="0f8d1-141">アプリ ID は、bot 名に解決される必要があります。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-141">The app ID should resolve to your bot name.</span></span>

   * <span data-ttu-id="0f8d1-142">Bot を選択し、メッセージを送信して会話を開始します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-142">Select your bot and send a message to initiate a conversation.</span></span>
   * <span data-ttu-id="0f8d1-143">または、ボットのアプリ ID を Microsoft Teams の左上にある検索ボックスに貼り付けることもできます。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-143">Alternatively, you can paste your bot's app ID in the search box in the top left in Microsoft Teams.</span></span> <span data-ttu-id="0f8d1-144">検索結果ページで、[人] タブに移動して bot を表示し、それとのチャットを開始します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-144">In the search results page, navigate to the People tab to see your bot and to start chatting with it.</span></span>

<span data-ttu-id="0f8d1-145">Bot はチームに追加`conversationUpdate`された bot と同じようにイベントを受け取りますが、チーム情報`channelData`はオブジェクトに含めません。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-145">Your bot will receive the `conversationUpdate` event just like bots added to a team, but without the team information in the `channelData` object.</span></span>

## <a name="blocking-a-bot-in-personal-chat"></a><span data-ttu-id="0f8d1-146">個人チャットでボットをブロックする</span><span class="sxs-lookup"><span data-stu-id="0f8d1-146">Blocking a bot in personal chat</span></span>

<span data-ttu-id="0f8d1-147">ユーザーが個人のチャットメッセージを送信しないようにすることを選択できることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-147">Note that users can choose to block your bot from sending personal chat messages.</span></span> <span data-ttu-id="0f8d1-148">チャットチャネルでボットを右クリックして、[**ブロックボット会話**] を選択すると、これを切り替えることができます。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-148">They may toggle this by right-clicking your bot in the chat channel and choosing **Block bot conversation**.</span></span> <span data-ttu-id="0f8d1-149">これは、ボットが引き続きメッセージを送信するのに対し、ユーザーはメッセージを受信できないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-149">This means your bots will continue to send messages but the user will not receive those messages.</span></span>

![Bot をブロックする](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a><span data-ttu-id="0f8d1-151">チームから bot を削除する</span><span class="sxs-lookup"><span data-stu-id="0f8d1-151">Removing a bot from a team</span></span>

<span data-ttu-id="0f8d1-152">ユーザーは、teams ビューのボットリストで [ごみ箱] アイコンを選択することによって、bot を削除できます。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-152">Users can delete the bot by choosing the trash-can icon on the bots list in their teams view.</span></span> <span data-ttu-id="0f8d1-153">これにより、チームの使用から bot が削除されるだけであることに注意してください。個々のユーザーは、引き続き個人コンテキストで操作できます。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-153">Note that this only removes the bot from that team's use; individual users will still be able to interact in personal context.</span></span>

<span data-ttu-id="0f8d1-154">個人コンテキストのボットは、ユーザーが無効にすることや削除することはできません。 Teams から bot を完全に削除するのは簡単です。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-154">Bots in personal context cannot be disabled or removed by a user, short of completely removing the bot from Teams.</span></span>

## <a name="disabling-a-bot-in-teams"></a><span data-ttu-id="0f8d1-155">Teams でボットを無効にする</span><span class="sxs-lookup"><span data-stu-id="0f8d1-155">Disabling a bot in Teams</span></span>

<span data-ttu-id="0f8d1-156">Bot がメッセージを受信しないようにするには、Bot ダッシュボードに移動して、Microsoft Teams チャネルを編集します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-156">To stop your bot receiving messages, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="0f8d1-157">**[Microsoft Teams で有効にする**] オプションをオフにします。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-157">Clear the **Enable on Microsoft Teams** option.</span></span> <span data-ttu-id="0f8d1-158">これにより、ユーザーは bot と対話することができなくなりますが、引き続き検出可能で、ユーザーは引き続き teams に追加することができます。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-158">This prevents users from interacting with the bot, but it will still be discoverable and users will still be able to add it to teams.</span></span>

## <a name="deleting-a-bot-from-teams"></a><span data-ttu-id="0f8d1-159">Teams から bot を削除する</span><span class="sxs-lookup"><span data-stu-id="0f8d1-159">Deleting a bot from Teams</span></span>

<span data-ttu-id="0f8d1-160">Bot を Teams から完全に削除するには、Bot ダッシュボードに移動して、Microsoft Teams チャネルを編集します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-160">To remove your bot completely from Teams, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="0f8d1-161">下部にある [**削除**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-161">Choose the **Delete** button at the bottom.</span></span> <span data-ttu-id="0f8d1-162">これにより、ユーザーは bot を検出、追加、または操作することができなくなります。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-162">This prevents users from discovering, adding, or interacting with your bot.</span></span> <span data-ttu-id="0f8d1-163">これにより、他のユーザーの Teams インスタンスから bot が削除されることはありませんが、機能も停止します。</span><span class="sxs-lookup"><span data-stu-id="0f8d1-163">Note that this does not remove the bot from other users' Teams instances, although it will cease functioning for them as well.</span></span>
