---
title: ボットのテストとデバッグ
description: ボットをテストする方法について説明Microsoft Teams
keywords: teams ボットのテスト
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
# <a name="test-and-debug-your-microsoft-teams-bot"></a><span data-ttu-id="3f992-104">ボットのテストとデバッグMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="3f992-104">Test and debug your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="3f992-105">ボットをテストする場合は、ボットで実行するコンテキストと、Microsoft Teams 固有のデータを必要とするボットに追加した可能性がある機能の両方を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3f992-105">When testing your bot you need to take into consideration both the context(s) you want your bot to run in, as well as any functionality you may have added to your bot that requires data specific to Microsoft Teams.</span></span> <span data-ttu-id="3f992-106">ボットをテストするために選択したメソッドが、その機能と一致することを確認します。</span><span class="sxs-lookup"><span data-stu-id="3f992-106">Make sure that the method you chose to test your bot aligns with its functionality.</span></span>

## <a name="test-by-uploading-to-teams"></a><span data-ttu-id="3f992-107">アプリにアップロードしてテストTeams</span><span class="sxs-lookup"><span data-stu-id="3f992-107">Test by uploading to Teams</span></span>

<span data-ttu-id="3f992-108">ボットをテストする最も包括的な方法は、アプリ パッケージを作成し、アプリ パッケージをアプリ パッケージにアップロードTeams。</span><span class="sxs-lookup"><span data-stu-id="3f992-108">The most comprehensive way to test your bot is by creating an app package and uploading it to Teams.</span></span> <span data-ttu-id="3f992-109">これは、すべてのスコープでボットで使用できる完全な機能をテストする唯一の方法です。</span><span class="sxs-lookup"><span data-stu-id="3f992-109">This is the only method to test the full functionality available to your bot, across all scopes.</span></span>

<span data-ttu-id="3f992-110">アプリをアップロードするには、2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="3f992-110">There are two methods for uploading your app.</span></span> <span data-ttu-id="3f992-111">App Studio を使用[して支援することもできます](~/concepts/build-and-test/app-studio-overview.md)し、アプリ パッケージ[](~/concepts/build-and-test/apps-package.md)を手動で作成してアプリ[をアップロードすることもできます](~/concepts/deploy-and-publish/apps-upload.md)。</span><span class="sxs-lookup"><span data-stu-id="3f992-111">You can either use [App Studio](~/concepts/build-and-test/app-studio-overview.md) to help you, or you can manually [create an app package](~/concepts/build-and-test/apps-package.md) and [upload your app](~/concepts/deploy-and-publish/apps-upload.md).</span></span> <span data-ttu-id="3f992-112">マニフェストを変更してアプリを再アップロードする必要がある場合は、変更された[](#deleting-a-bot-from-teams)アプリ パッケージをアップロードする前にボットを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3f992-112">If you need to alter your manifest and re-upload your app, you should [delete your bot](#deleting-a-bot-from-teams) before uploading your altered app package.</span></span>

## <a name="debug-your-bot-locally"></a><span data-ttu-id="3f992-113">ボットをローカルでデバッグする</span><span class="sxs-lookup"><span data-stu-id="3f992-113">Debug your bot locally</span></span>

<span data-ttu-id="3f992-114">開発中にボットをローカルでホストしている場合は、ボットをテストするために [ngrok](https://ngrok.com/) のようなトンネリング サービスを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3f992-114">If you are hosting your bot locally during development you'll need to use a tunneling service like [ngrok](https://ngrok.com/) in order to test your bot.</span></span> <span data-ttu-id="3f992-115">ngrok をダウンロードしてインストールしたら、次のコマンドを実行してトンネリング サービスを開始します。</span><span class="sxs-lookup"><span data-stu-id="3f992-115">Once you've downloaded and installed ngrok, run the below command to start the tunneling service.</span></span> <span data-ttu-id="3f992-116">パスに ngrok を追加する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="3f992-116">You may need to add ngrok to your path.</span></span>

```bash
ngrok http <port> -host-header=localhost:<port>
```

<span data-ttu-id="3f992-117">アプリ マニフェストで ngrok によって提供される https エンドポイントを使用します。</span><span class="sxs-lookup"><span data-stu-id="3f992-117">Use the https endpoint provided by ngrok in your app manifest.</span></span> <span data-ttu-id="3f992-118">コマンド ウィンドウを閉じて再起動すると、新しい URL が取得され、その URL も使用するにはボット エンドポイント アドレスを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3f992-118">If you close your command window and restart you'll get a new URL, and you'll need to update your bot endpoint address to use that one as well.</span></span>

## <a name="testing-your-bot-without-uploading-to-teams"></a><span data-ttu-id="3f992-119">ボットにアップロードせずにボットをテストTeams</span><span class="sxs-lookup"><span data-stu-id="3f992-119">Testing your bot without uploading to Teams</span></span>

<span data-ttu-id="3f992-120">場合によっては、ボットをアプリとしてインストールせずにボットをテストする必要Teams。</span><span class="sxs-lookup"><span data-stu-id="3f992-120">Occasionally it may be necessary to test your bot without installing it as an app in Teams.</span></span> <span data-ttu-id="3f992-121">これを行う 2 つの方法を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="3f992-121">We provide two methods for doing so below.</span></span> <span data-ttu-id="3f992-122">アプリとしてインストールせずにボットをテストすると、ボットが利用可能で応答を確実に行うのに役立ちますが、ボットに追加した Microsoft Teams 機能の全幅をテストできません。</span><span class="sxs-lookup"><span data-stu-id="3f992-122">Testing your bot without installing it as an app can be useful to ensure your bot is available and responding, however it will not allow you to test the full breadth of Microsoft Teams functionality you may have added to your bot.</span></span> <span data-ttu-id="3f992-123">ボットを完全にテストする必要がある場合は、アップロードによるテストの手順 [に従ってください](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="3f992-123">If you need to fully test your bot, please follow the instructions for [testing by uploading](#test-by-uploading-to-teams).</span></span>

### <a name="use-the-bot-emulator"></a><span data-ttu-id="3f992-124">ボット エミュレーターの使用</span><span class="sxs-lookup"><span data-stu-id="3f992-124">Use the Bot Emulator</span></span>

<span data-ttu-id="3f992-125">このBot Framework Emulatorは、ボット開発者がボットをローカルまたはリモートでテストおよびデバッグできるデスクトップ アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="3f992-125">The Bot Framework Emulator is a desktop application that allows bot developers to test and debug their bots, either locally or remotely.</span></span> <span data-ttu-id="3f992-126">エミュレーターを使用すると、ボットとチャットし、ボットが送信および受信するメッセージを検査できます。</span><span class="sxs-lookup"><span data-stu-id="3f992-126">Using the emulator, you can chat with your bot and inspect the messages that your bot sends and receives.</span></span> <span data-ttu-id="3f992-127">これは、ボットが使用可能で応答を確認する場合に役立ちますが、エミュレーターでは、ボットに追加した Teams 固有の機能をテストしたり、ボットからの応答を Teams で表示する方法を正確に視覚的に表現したりできません。</span><span class="sxs-lookup"><span data-stu-id="3f992-127">This can be useful for verifying that your bot is available and responding, however the emulator will not allow you to test any Teams-specific functionality you've added to your bot, nor will responses from your bot be an accurate visual representation of how they will be rendered in Teams.</span></span> <span data-ttu-id="3f992-128">これらのテストを行う必要がある場合は、ボットをアップロード [する方が最適です](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="3f992-128">If you need to test either of those things it is best to [upload your bot](#test-by-uploading-to-teams).</span></span>

<span data-ttu-id="3f992-129">詳細については、Bot Framework Emulatorを参照[してください](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3f992-129">Complete instructions on the Bot Framework Emulator can be found [here](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).</span></span>

### <a name="talk-to-your-bot-directly-by-id"></a><span data-ttu-id="3f992-130">Id でボットに直接話す</span><span class="sxs-lookup"><span data-stu-id="3f992-130">Talk to your bot directly by Id</span></span>

>[!Important]
><span data-ttu-id="3f992-131">Id によってボットと話すのは、テスト目的のみを目的とします。</span><span class="sxs-lookup"><span data-stu-id="3f992-131">Talking to your bot by Id is intended for testing purposes only.</span></span>

<span data-ttu-id="3f992-132">ボットの ID を使用して、ボットとの会話を開始できます。これを行う 2 つの方法を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="3f992-132">You can also initiate a conversation with your bot by using its Id. Two methods for doing so are given below.</span></span> <span data-ttu-id="3f992-133">これらの方法のいずれかを使用してボットを追加した場合、チャネル会話では対応できません。また、タブやメッセージング拡張機能などの他の Microsoft Teams アプリ機能を利用することはできません。</span><span class="sxs-lookup"><span data-stu-id="3f992-133">When a bot has been added through one of these methods it will not be addressable in channel conversations, and you cannot take advantage of other Microsoft Teams app capabilities like tabs or messaging extensions.</span></span>

1. <span data-ttu-id="3f992-134">ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots)ページの [チャネル]**で、[ボット** に追加] を選択 **Microsoft Teams。**</span><span class="sxs-lookup"><span data-stu-id="3f992-134">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Channels**, select **Add to Microsoft Teams**.</span></span> <span data-ttu-id="3f992-135">Microsoft Teamsボットとの個人用チャットで起動します。</span><span class="sxs-lookup"><span data-stu-id="3f992-135">Microsoft Teams will launch with a personal chat with your bot.</span></span>
2. <span data-ttu-id="3f992-136">ボットのアプリ ID を次の場所から直接参照Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="3f992-136">Directly reference your bot's app ID from within Microsoft Teams:</span></span>
   * <span data-ttu-id="3f992-137">ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots)ページの [詳細] で、ボットの **Microsoft App ID** をコピーします。</span><span class="sxs-lookup"><span data-stu-id="3f992-137">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Details**, copy the **Microsoft App ID** for your bot.</span></span>
  
     ![ボットの AppID の取得](~/assets/images/bots_appid_botframework.png)
  
   * <span data-ttu-id="3f992-139">[チャット] Microsoft Teamsで、[チャットの追加]**アイコンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="3f992-139">From within Microsoft Teams, on the **Chat** pane, select the **Add chat** icon.</span></span> <span data-ttu-id="3f992-140">**[To:]** の場合は、ボットの Microsoft App ID を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="3f992-140">For **To:**, paste your bot's Microsoft App ID.</span></span>
  
     ![ボットの AppID のアップロード](~/assets/images/bots_uploading.png)

     <span data-ttu-id="3f992-142">アプリ ID はボット名に解決する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3f992-142">The app ID should resolve to your bot name.</span></span>

   * <span data-ttu-id="3f992-143">ボットを選択し、メッセージを送信して会話を開始します。</span><span class="sxs-lookup"><span data-stu-id="3f992-143">Select your bot and send a message to initiate a conversation.</span></span>
   * <span data-ttu-id="3f992-144">または、ボットのアプリ ID をアプリの左上の検索ボックスに貼り付Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="3f992-144">Alternatively, you can paste your bot's app ID in the search box in the top left in Microsoft Teams.</span></span> <span data-ttu-id="3f992-145">検索結果ページで、[ユーザー] タブに移動してボットを表示し、チャットを開始します。</span><span class="sxs-lookup"><span data-stu-id="3f992-145">In the search results page, navigate to the People tab to see your bot and to start chatting with it.</span></span>

<span data-ttu-id="3f992-146">ボットは、チームに追加されたボットと同様に、オブジェクト内のチーム情報なしでイベント `conversationUpdate` を受信 `channelData` します。</span><span class="sxs-lookup"><span data-stu-id="3f992-146">Your bot will receive the `conversationUpdate` event just like bots added to a team, but without the team information in the `channelData` object.</span></span>

## <a name="blocking-a-bot-in-personal-chat"></a><span data-ttu-id="3f992-147">個人用チャットでのボットのブロック</span><span class="sxs-lookup"><span data-stu-id="3f992-147">Blocking a bot in personal chat</span></span>

<span data-ttu-id="3f992-148">ユーザーは、ボットが個人のチャット メッセージを送信するのをブロックすることができます。</span><span class="sxs-lookup"><span data-stu-id="3f992-148">Note that users can choose to block your bot from sending personal chat messages.</span></span> <span data-ttu-id="3f992-149">チャット チャネルでボットを右クリックし、[ボットの会話をブロックする] を選択することで、これを **切り替える場合があります**。</span><span class="sxs-lookup"><span data-stu-id="3f992-149">They may toggle this by right-clicking your bot in the chat channel and choosing **Block bot conversation**.</span></span> <span data-ttu-id="3f992-150">つまり、ボットは引き続きメッセージを送信しますが、ユーザーはそれらのメッセージを受信しません。</span><span class="sxs-lookup"><span data-stu-id="3f992-150">This means your bots will continue to send messages but the user will not receive those messages.</span></span>

![ボットのブロック](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a><span data-ttu-id="3f992-152">チームからボットを削除する</span><span class="sxs-lookup"><span data-stu-id="3f992-152">Removing a bot from a team</span></span>

<span data-ttu-id="3f992-153">ユーザーは、チーム ビューでボットリストのごみ箱アイコンを選択して、ボットを削除できます。</span><span class="sxs-lookup"><span data-stu-id="3f992-153">Users can delete the bot by choosing the trash-can icon on the bots list in their teams view.</span></span> <span data-ttu-id="3f992-154">これは、そのチームの使用からボットを削除するだけである点に注意してください。個々のユーザーは引き続き個人のコンテキストで対話できます。</span><span class="sxs-lookup"><span data-stu-id="3f992-154">Note that this only removes the bot from that team's use; individual users will still be able to interact in personal context.</span></span>

<span data-ttu-id="3f992-155">個人用コンテキストのボットを無効にしたり、ユーザーが削除したりすることはできません。ユーザーがボットを完全に削除Teams。</span><span class="sxs-lookup"><span data-stu-id="3f992-155">Bots in personal context cannot be disabled or removed by a user, short of completely removing the bot from Teams.</span></span>

## <a name="disabling-a-bot-in-teams"></a><span data-ttu-id="3f992-156">アプリでボットを無効Teams</span><span class="sxs-lookup"><span data-stu-id="3f992-156">Disabling a bot in Teams</span></span>

<span data-ttu-id="3f992-157">ボットのメッセージ受信を停止するには、ボット ダッシュボードに移動し、ボット チャネルMicrosoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="3f992-157">To stop your bot receiving messages, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="3f992-158">[有効にする **] オプションをMicrosoft Teams** します。</span><span class="sxs-lookup"><span data-stu-id="3f992-158">Clear the **Enable on Microsoft Teams** option.</span></span> <span data-ttu-id="3f992-159">これにより、ユーザーはボットを操作できませんが、検出可能であり、ユーザーは引き続きチームに追加できます。</span><span class="sxs-lookup"><span data-stu-id="3f992-159">This prevents users from interacting with the bot, but it will still be discoverable and users will still be able to add it to teams.</span></span>

## <a name="deleting-a-bot-from-teams"></a><span data-ttu-id="3f992-160">ボットをユーザーから削除Teams</span><span class="sxs-lookup"><span data-stu-id="3f992-160">Deleting a bot from Teams</span></span>

<span data-ttu-id="3f992-161">ボットを完全に削除するには、Teamsダッシュボードに移動し、ボット チャネルMicrosoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="3f992-161">To remove your bot completely from Teams, go to your Bot Dashboard and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="3f992-162">下部にある **[削除** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="3f992-162">Choose the **Delete** button at the bottom.</span></span> <span data-ttu-id="3f992-163">これにより、ユーザーはボットを検出、追加、または操作できます。</span><span class="sxs-lookup"><span data-stu-id="3f992-163">This prevents users from discovering, adding, or interacting with your bot.</span></span> <span data-ttu-id="3f992-164">これは、他のユーザーのインスタンスからボットを削除Teams、ボットの機能も停止します。</span><span class="sxs-lookup"><span data-stu-id="3f992-164">Note that this does not remove the bot from other users' Teams instances, although it will cease functioning for them as well.</span></span>

## <a name="removing-your-bot-from-appsource"></a><span data-ttu-id="3f992-165">AppSource からボットを削除する</span><span class="sxs-lookup"><span data-stu-id="3f992-165">Removing your bot from AppSource</span></span>

<span data-ttu-id="3f992-166">AppSource (以前の Office ストア) の Teams アプリからボットを削除する場合は、アプリ マニフェストからボットを削除し、検証のためにアプリを再送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3f992-166">If you want to remove your bot from your Teams app in AppSource (previously Office Store), you must remove the bot from your app manifest and resubmit your app for validation.</span></span> <span data-ttu-id="3f992-167">詳細については、「アプリを[AppSource にMicrosoft Teamsする」を参照してください](~/concepts/deploy-and-publish/apps-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="3f992-167">For more information, see [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span>
