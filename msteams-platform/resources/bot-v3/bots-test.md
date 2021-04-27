---
title: ボットのテストとデバッグ
description: Microsoft Teams でボットをテストする方法について説明します。
keywords: teams ボットのテスト
ms.topic: how-to
localization_priority: Normal
ms.date: 03/20/2019
ms.openlocfilehash: 0f44a88bcf054f4e0f4112ddc8bd3fbfdc18117d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020633"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a><span data-ttu-id="0dc7b-104">Microsoft Teams ボットのテストとデバッグ</span><span class="sxs-lookup"><span data-stu-id="0dc7b-104">Test and debug your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="0dc7b-105">ボットをテストする場合は、ボットを実行するコンテキストと、Microsoft Teams 固有のデータを必要とするボットに追加した可能性がある機能の両方を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-105">When testing your bot you need to take into consideration both the context(s) you want your bot to run in, as well as any functionality you may have added to your bot that requires data specific to Microsoft Teams.</span></span> <span data-ttu-id="0dc7b-106">ボットをテストするために選択したメソッドが、その機能と一致することを確認します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-106">Make sure that the method you chose to test your bot aligns with its functionality.</span></span>

## <a name="test-by-uploading-to-teams"></a><span data-ttu-id="0dc7b-107">Teams にアップロードしてテストする</span><span class="sxs-lookup"><span data-stu-id="0dc7b-107">Test by uploading to Teams</span></span>

<span data-ttu-id="0dc7b-108">ボットをテストする最も包括的な方法は、アプリ パッケージを作成して Teams にアップロードする方法です。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-108">The most comprehensive way to test your bot is by creating an app package and uploading it to Teams.</span></span> <span data-ttu-id="0dc7b-109">これは、すべてのスコープでボットで使用できる完全な機能をテストする唯一の方法です。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-109">This is the only method to test the full functionality available to your bot, across all scopes.</span></span>

<span data-ttu-id="0dc7b-110">アプリをアップロードするには、2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-110">There are two methods for uploading your app.</span></span> <span data-ttu-id="0dc7b-111">App Studio を使用[して支援することもできます](~/concepts/build-and-test/app-studio-overview.md)し、アプリ パッケージ[](~/concepts/build-and-test/apps-package.md)を手動で作成してアプリ[をアップロードすることもできます](~/concepts/deploy-and-publish/apps-upload.md)。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-111">You can either use [App Studio](~/concepts/build-and-test/app-studio-overview.md) to help you, or you can manually [create an app package](~/concepts/build-and-test/apps-package.md) and [upload your app](~/concepts/deploy-and-publish/apps-upload.md).</span></span> <span data-ttu-id="0dc7b-112">マニフェストを変更してアプリを再アップロードする必要がある場合は、変更された[](#deleting-a-bot-from-teams)アプリ パッケージをアップロードする前にボットを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-112">If you need to alter your manifest and re-upload your app, you should [delete your bot](#deleting-a-bot-from-teams) before uploading your altered app package.</span></span>

## <a name="debug-your-bot-locally"></a><span data-ttu-id="0dc7b-113">ボットをローカルでデバッグする</span><span class="sxs-lookup"><span data-stu-id="0dc7b-113">Debug your bot locally</span></span>

<span data-ttu-id="0dc7b-114">開発中にボットをローカルでホストしている場合は、ボットをテストするために [ngrok](https://ngrok.com/) のようなトンネリング サービスを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-114">If you are hosting your bot locally during development you'll need to use a tunneling service like [ngrok](https://ngrok.com/) in order to test your bot.</span></span> <span data-ttu-id="0dc7b-115">ngrok をダウンロードしてインストールしたら、次のコマンドを実行してトンネリング サービスを開始します (パスに ngrok を追加する必要がある場合があります)。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-115">Once you've downloaded and installed ngrok, run the below command to start the tunneling service (you may need to add ngrok to your path).</span></span>

```bash
ngrok http <port> -host-header=localhost:<port>
```

<span data-ttu-id="0dc7b-116">アプリ マニフェストで ngrok によって提供される https エンドポイントを使用します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-116">Use the https endpoint provided by ngrok in your app manifest.</span></span> <span data-ttu-id="0dc7b-117">コマンド ウィンドウを閉じて再起動すると、新しい URL が取得され、その URL も使用するにはボット エンドポイント アドレスを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-117">If you close your command window and restart you'll get a new URL, and you'll need to update your bot endpoint address to use that one as well.</span></span>

## <a name="testing-your-bot-without-uploading-to-teams"></a><span data-ttu-id="0dc7b-118">Teams にアップロードせずにボットをテストする</span><span class="sxs-lookup"><span data-stu-id="0dc7b-118">Testing your bot without uploading to Teams</span></span>

<span data-ttu-id="0dc7b-119">場合によっては、Teams にアプリとしてインストールせずにボットをテストする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-119">Occasionally it may be necessary to test your bot without installing it as an app in Teams.</span></span> <span data-ttu-id="0dc7b-120">これを行う 2 つの方法を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-120">We provide two methods for doing so below.</span></span> <span data-ttu-id="0dc7b-121">アプリとしてインストールせずにボットをテストすると、ボットが利用可能で応答を確実に行うのに役立ちますが、ボットに追加した Microsoft Teams の機能全体をテストできません。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-121">Testing your bot without installing it as an app can be useful to ensure your bot is available and responding, however it will not allow you to test the full breadth of Microsoft Teams functionality you may have added to your bot.</span></span> <span data-ttu-id="0dc7b-122">ボットを完全にテストする必要がある場合は、アップロードによるテストの手順 [に従ってください](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-122">If you need to fully test your bot, please follow the instructions for [testing by uploading](#test-by-uploading-to-teams).</span></span>

### <a name="use-the-bot-emulator"></a><span data-ttu-id="0dc7b-123">ボット エミュレーターの使用</span><span class="sxs-lookup"><span data-stu-id="0dc7b-123">Use the Bot Emulator</span></span>

<span data-ttu-id="0dc7b-124">ボット フレームワーク エミュレーターは、ボット開発者がボットをローカルまたはリモートでテストおよびデバッグできるデスクトップ アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-124">The Bot Framework Emulator is a desktop application that allows bot developers to test and debug their bots, either locally or remotely.</span></span> <span data-ttu-id="0dc7b-125">エミュレーターを使用すると、ボットとチャットし、ボットが送信および受信するメッセージを検査できます。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-125">Using the emulator, you can chat with your bot and inspect the messages that your bot sends and receives.</span></span> <span data-ttu-id="0dc7b-126">これは、ボットが使用可能で応答を確認する場合に役立ちますが、エミュレーターでは、ボットに追加した Teams 固有の機能をテストしたり、ボットからの応答を Teams でレンダリングする方法を正確に視覚的に表現したりできません。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-126">This can be useful for verifying that your bot is available and responding, however the emulator will not allow you to test any Teams-specific functionality you've added to your bot, nor will responses from your bot be an accurate visual representation of how they will be rendered in Teams.</span></span> <span data-ttu-id="0dc7b-127">これらのテストを行う必要がある場合は、ボットをアップロード [する方が最適です](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-127">If you need to test either of those things it is best to [upload your bot](#test-by-uploading-to-teams).</span></span>

<span data-ttu-id="0dc7b-128">Bot Framework エミュレーターの完全な手順については、こちらを参照 [してください](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-128">Complete instructions on the Bot Framework Emulator can be found [here](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).</span></span>

### <a name="talk-to-your-bot-directly-by-id"></a><span data-ttu-id="0dc7b-129">Id でボットに直接話す</span><span class="sxs-lookup"><span data-stu-id="0dc7b-129">Talk to your bot directly by Id</span></span>

>[!Important]
><span data-ttu-id="0dc7b-130">Id によってボットと話すのは、テスト目的のみを目的とします。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-130">Talking to your bot by Id is intended for testing purposes only.</span></span>

<span data-ttu-id="0dc7b-131">ボットの ID を使用して、ボットとの会話を開始できます。これを行う 2 つの方法を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-131">You can also initiate a conversation with your bot by using its Id. Two methods for doing so are given below.</span></span> <span data-ttu-id="0dc7b-132">これらの方法のいずれかを使用してボットが追加された場合、チャネル会話では対応できません。また、タブやメッセージング拡張機能などの他の Microsoft Teams アプリ機能を利用することはできません。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-132">When a bot has been added through one of these methods it will not be addressable in channel conversations, and you cannot take advantage of other Microsoft Teams app capabilities like tabs or messaging extensions.</span></span>

1. <span data-ttu-id="0dc7b-133">ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots)ページの [チャネル] で、[Microsoft Teams に **追加] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-133">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Channels**, select **Add to Microsoft Teams**.</span></span> <span data-ttu-id="0dc7b-134">Microsoft Teams は、ボットとの個人用チャットで起動します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-134">Microsoft Teams will launch with a personal chat with your bot.</span></span>
2. <span data-ttu-id="0dc7b-135">Microsoft Teams 内からボットのアプリ ID を直接参照します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-135">Directly reference your bot's app ID from within Microsoft Teams:</span></span>
   * <span data-ttu-id="0dc7b-136">ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots)ページの [詳細] で、ボットの **Microsoft App ID** をコピーします。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-136">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Details**, copy the **Microsoft App ID** for your bot.</span></span>
  
     ![ボットの AppID の取得](~/assets/images/bots_appid_botframework.png)
  
   * <span data-ttu-id="0dc7b-138">Microsoft Teams 内の [チャット] ウィンドウ **で** 、[チャットの追加] **アイコンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-138">From within Microsoft Teams, on the **Chat** pane, select the **Add chat** icon.</span></span> <span data-ttu-id="0dc7b-139">**[To:]** の場合は、ボットの Microsoft App ID を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-139">For **To:**, paste your bot's Microsoft App ID.</span></span>
  
     ![ボットの AppID のアップロード](~/assets/images/bots_uploading.png)

     <span data-ttu-id="0dc7b-141">アプリ ID はボット名に解決する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-141">The app ID should resolve to your bot name.</span></span>

   * <span data-ttu-id="0dc7b-142">ボットを選択し、メッセージを送信して会話を開始します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-142">Select your bot and send a message to initiate a conversation.</span></span>
   * <span data-ttu-id="0dc7b-143">または、Microsoft Teams の左上にある検索ボックスにボットのアプリ ID を貼り付けることができます。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-143">Alternatively, you can paste your bot's app ID in the search box in the top left in Microsoft Teams.</span></span> <span data-ttu-id="0dc7b-144">検索結果ページで、[ユーザー] タブに移動してボットを表示し、チャットを開始します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-144">In the search results page, navigate to the People tab to see your bot and to start chatting with it.</span></span>

<span data-ttu-id="0dc7b-145">ボットは、チームに追加されたボットと同様に、オブジェクト内のチーム情報なしでイベント `conversationUpdate` を受信 `channelData` します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-145">Your bot will receive the `conversationUpdate` event just like bots added to a team, but without the team information in the `channelData` object.</span></span>

## <a name="blocking-a-bot-in-personal-chat"></a><span data-ttu-id="0dc7b-146">個人用チャットでのボットのブロック</span><span class="sxs-lookup"><span data-stu-id="0dc7b-146">Blocking a bot in personal chat</span></span>

<span data-ttu-id="0dc7b-147">ユーザーは、ボットが個人のチャット メッセージを送信するのをブロックすることができます。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-147">Note that users can choose to block your bot from sending personal chat messages.</span></span> <span data-ttu-id="0dc7b-148">チャット チャネルでボットを右クリックし、[ボットの会話をブロックする] を選択することで、これを **切り替える場合があります**。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-148">They may toggle this by right-clicking your bot in the chat channel and choosing **Block bot conversation**.</span></span> <span data-ttu-id="0dc7b-149">つまり、ボットは引き続きメッセージを送信しますが、ユーザーはそれらのメッセージを受信しません。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-149">This means your bots will continue to send messages but the user will not receive those messages.</span></span>

![ボットのブロック](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a><span data-ttu-id="0dc7b-151">チームからボットを削除する</span><span class="sxs-lookup"><span data-stu-id="0dc7b-151">Removing a bot from a team</span></span>

<span data-ttu-id="0dc7b-152">ユーザーは、チーム ビューでボットリストのごみ箱アイコンを選択して、ボットを削除できます。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-152">Users can delete the bot by choosing the trash-can icon on the bots list in their teams view.</span></span> <span data-ttu-id="0dc7b-153">これは、そのチームの使用からボットを削除するだけである点に注意してください。個々のユーザーは引き続き個人のコンテキストで対話できます。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-153">Note that this only removes the bot from that team's use; individual users will still be able to interact in personal context.</span></span>

<span data-ttu-id="0dc7b-154">個人用コンテキストのボットを無効にしたり、ユーザーが削除したりすることはできません。Teams からボットを完全に削除することはできません。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-154">Bots in personal context cannot be disabled or removed by a user, short of completely removing the bot from Teams.</span></span>

## <a name="disabling-a-bot-in-teams"></a><span data-ttu-id="0dc7b-155">Teams でボットを無効にする</span><span class="sxs-lookup"><span data-stu-id="0dc7b-155">Disabling a bot in Teams</span></span>

<span data-ttu-id="0dc7b-156">ボットのメッセージ受信を停止するには、ボット ダッシュボードに移動し、Microsoft Teams チャネルを編集します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-156">To stop your bot receiving messages, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="0dc7b-157">[Microsoft **Teams で有効にする] オプションをオフ** にします。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-157">Clear the **Enable on Microsoft Teams** option.</span></span> <span data-ttu-id="0dc7b-158">これにより、ユーザーはボットを操作できませんが、検出可能であり、ユーザーは引き続きチームに追加できます。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-158">This prevents users from interacting with the bot, but it will still be discoverable and users will still be able to add it to teams.</span></span>

## <a name="deleting-a-bot-from-teams"></a><span data-ttu-id="0dc7b-159">Teams からボットを削除する</span><span class="sxs-lookup"><span data-stu-id="0dc7b-159">Deleting a bot from Teams</span></span>

<span data-ttu-id="0dc7b-160">Teams からボットを完全に削除するには、ボット ダッシュボードに移動し、Microsoft Teams チャネルを編集します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-160">To remove your bot completely from Teams, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="0dc7b-161">下部にある **[削除** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-161">Choose the **Delete** button at the bottom.</span></span> <span data-ttu-id="0dc7b-162">これにより、ユーザーはボットを検出、追加、または操作できます。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-162">This prevents users from discovering, adding, or interacting with your bot.</span></span> <span data-ttu-id="0dc7b-163">これは他のユーザーの Teams インスタンスからボットを削除しませんが、ボットの機能も停止します。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-163">Note that this does not remove the bot from other users' Teams instances, although it will cease functioning for them as well.</span></span>

## <a name="removing-your-bot-from-appsource"></a><span data-ttu-id="0dc7b-164">AppSource からボットを削除する</span><span class="sxs-lookup"><span data-stu-id="0dc7b-164">Removing your bot from AppSource</span></span>

<span data-ttu-id="0dc7b-165">AppSource (以前は Office ストア) の Teams アプリからボットを削除する場合は、アプリ マニフェストからボットを削除し、検証のためにアプリを再送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-165">If you want to remove your bot from your Teams app in AppSource (formerly Office Store), you must remove the bot from your app manifest and resubmit your app for validation.</span></span> <span data-ttu-id="0dc7b-166">詳細 [については、「Microsoft Teams アプリを AppSource に発行する](~/concepts/deploy-and-publish/apps-publish.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0dc7b-166">See [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md) for more information.</span></span>
