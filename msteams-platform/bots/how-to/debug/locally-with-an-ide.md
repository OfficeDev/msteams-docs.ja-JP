---
title: ボットをローカルでテストおよびデバッグする
author: surbhigupta
description: IDE を使用してボットをローカルでテストおよびデバッグする
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 0c34d46069c52dfb51f828ed89298f50362ea021
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068989"
---
# <a name="test-and-debug-your-bot-locally"></a><span data-ttu-id="148ab-103">ボットをローカルでテストおよびデバッグする</span><span class="sxs-lookup"><span data-stu-id="148ab-103">Test and debug your bot locally</span></span>

<span data-ttu-id="148ab-104">ボットをテストする場合は、ボットで実行するコンテキストと、Microsoft Teams に固有のデータを必要とするボットに追加した可能性があるすべての機能の両方を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="148ab-104">When testing your bot you need to take into consideration both the contexts you want your bot to run in, and any functionality you may have added to your bot that requires data specific to Microsoft Teams.</span></span> <span data-ttu-id="148ab-105">ボットをテストするために選択したメソッドが、その機能と一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="148ab-105">Make sure that the method you choose to test your bot aligns with its functionality.</span></span>

## <a name="test-by-uploading-to-teams"></a><span data-ttu-id="148ab-106">アプリにアップロードしてテストTeams</span><span class="sxs-lookup"><span data-stu-id="148ab-106">Test by uploading to Teams</span></span>

<span data-ttu-id="148ab-107">ボットをテストする最も包括的な方法は、アプリ パッケージを作成し、アプリ パッケージをアプリ パッケージにアップロードTeams。</span><span class="sxs-lookup"><span data-stu-id="148ab-107">The most comprehensive way to test your bot is by creating an app package and uploading it to Teams.</span></span> <span data-ttu-id="148ab-108">これは、すべてのスコープでボットで使用できる完全な機能をテストする唯一の方法です。</span><span class="sxs-lookup"><span data-stu-id="148ab-108">This is the only method to test the full functionality available to your bot, across all scopes.</span></span>

<span data-ttu-id="148ab-109">アプリをアップロードするには、次の 2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="148ab-109">There are two methods for uploading your app:</span></span>
* <span data-ttu-id="148ab-110">[App Studio を使用します](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="148ab-110">Use [App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>
* <span data-ttu-id="148ab-111">[アプリ パッケージを手動で作成](~/concepts/build-and-test/apps-package.md) し、アプリ [をアップロードします](~/concepts/deploy-and-publish/apps-upload.md)。</span><span class="sxs-lookup"><span data-stu-id="148ab-111">[Create an app package](~/concepts/build-and-test/apps-package.md) manually, and then [upload your app](~/concepts/deploy-and-publish/apps-upload.md).</span></span>

> [!NOTE]
> <span data-ttu-id="148ab-112">マニフェストを変更してアプリを再アップロードする必要がある場合は、変更された[](#delete-a-bot-from-teams)アプリ パッケージをアップロードする前にボットを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="148ab-112">If you need to alter your manifest and re-upload your app, you must [delete your bot](#delete-a-bot-from-teams) before uploading your altered app package.</span></span>

## <a name="debug-your-bot-locally"></a><span data-ttu-id="148ab-113">ボットをローカルでデバッグする</span><span class="sxs-lookup"><span data-stu-id="148ab-113">Debug your bot locally</span></span>

<span data-ttu-id="148ab-114">開発中にボットをローカルでホストしている場合は、ボットをテストするために [ngrok](https://ngrok.com/) のようなトンネリング サービスを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="148ab-114">If you are hosting your bot locally during development, you need to use a tunneling service like [ngrok](https://ngrok.com/) in order to test your bot.</span></span> <span data-ttu-id="148ab-115">ngrok をダウンロードしてインストールした後、パスに追加し、次のコマンドを実行してトンネ `ngrok` リング サービスを開始します。</span><span class="sxs-lookup"><span data-stu-id="148ab-115">After you download and install ngrok, add `ngrok` to your path, and run the following command to start the tunneling service:</span></span>

```bash
ngrok http <port> -host-header=localhost:<port>
```

<span data-ttu-id="148ab-116">アプリ マニフェストで ngrok によって提供される https エンドポイントを使用します。</span><span class="sxs-lookup"><span data-stu-id="148ab-116">Use the https endpoint provided by ngrok in your app manifest.</span></span> 

> [!NOTE]
> <span data-ttu-id="148ab-117">コマンド ウィンドウを閉じて再起動すると、新しい URL が生成され、ボット エンドポイント のアドレスを更新して使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="148ab-117">If you close your command window and restart, a new URL is generated and you need to update your bot endpoint address to use it.</span></span>

## <a name="test-your-bot-without-uploading-to-teams"></a><span data-ttu-id="148ab-118">ボットにアップロードせずにボットをテストTeams</span><span class="sxs-lookup"><span data-stu-id="148ab-118">Test your bot without uploading to Teams</span></span>

<span data-ttu-id="148ab-119">場合によっては、ボットをアプリとしてインストールせずにボットをテストする必要Teams。</span><span class="sxs-lookup"><span data-stu-id="148ab-119">Occasionally, it may be necessary to test your bot without installing it as an app in Teams.</span></span> <span data-ttu-id="148ab-120">ボットをテストする 2 つの方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="148ab-120">We provide two methods for testing the bot.</span></span> <span data-ttu-id="148ab-121">アプリとしてインストールせずにボットをテストすると、ボットが利用可能で応答を確実に行うのに役立ちますが、ボットに追加した Microsoft Teams 機能の全幅をテストできません。</span><span class="sxs-lookup"><span data-stu-id="148ab-121">Testing your bot without installing it as an app can be useful to ensure your bot is available and responding, however it won't allow you to test the full breadth of Microsoft Teams functionality you may have added to your bot.</span></span> <span data-ttu-id="148ab-122">ボットを完全にテストする必要がある場合は、「アップロード [によるテスト」を参照してください](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="148ab-122">If you need to fully test your bot, see [testing by uploading](#test-by-uploading-to-teams).</span></span>

### <a name="use-the-bot-emulator"></a><span data-ttu-id="148ab-123">ボット を使用Emulator</span><span class="sxs-lookup"><span data-stu-id="148ab-123">Use the Bot Emulator</span></span>

<span data-ttu-id="148ab-124">このBot Framework Emulatorは、ボット開発者がボットをローカルまたはリモートでテストおよびデバッグできるデスクトップ アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="148ab-124">The Bot Framework Emulator is a desktop application that permits bot developers to test and debug their bots locally or remotely.</span></span> <span data-ttu-id="148ab-125">エミュレーターは、ボットとチャットし、ボットが送信および受信するメッセージを調べするのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="148ab-125">The emulator helps you to chat with your bot and inspect the messages that your bot sends and receives.</span></span> <span data-ttu-id="148ab-126">これは、ボットが使用可能で応答を確認する場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="148ab-126">This can be useful for verifying that your bot is available and responding.</span></span> <span data-ttu-id="148ab-127">ただし、エミュレーターでは、ボットに追加した Teams 固有の機能をテストできません。また、ボットからの応答は、Teams でのレンダリング方法の正確な視覚的表現です。</span><span class="sxs-lookup"><span data-stu-id="148ab-127">However, the emulator does not permit you to test any Teams-specific functionality you have added to the bot, nor the responses from your bot are an accurate visual representation of how they are rendered in Teams.</span></span> <span data-ttu-id="148ab-128">これらのテストを行う必要がある場合は、ボットをアップロード [する方が最適です](#test-by-uploading-to-teams)。</span><span class="sxs-lookup"><span data-stu-id="148ab-128">If you need to test either of those things it is best to [upload your bot](#test-by-uploading-to-teams).</span></span>

<span data-ttu-id="148ab-129">詳細については、「詳細な手順[」を参照Bot Framework Emulator。](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="148ab-129">For more information, see [complete instructions on the Bot Framework Emulator](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).</span></span>

### <a name="talk-to-your-bot-directly-by-id"></a><span data-ttu-id="148ab-130">ボットと ID で直接話す</span><span class="sxs-lookup"><span data-stu-id="148ab-130">Talk to your bot directly by ID</span></span>

> [!Important]
> <span data-ttu-id="148ab-131">ID でボットと話すのは、基本的なテストのみを目的とします。</span><span class="sxs-lookup"><span data-stu-id="148ab-131">Talking to your bot by ID is intended for basic testing purposes only.</span></span> <span data-ttu-id="148ab-132">ボットTeams特定の機能が機能しません。</span><span class="sxs-lookup"><span data-stu-id="148ab-132">Any Teams-specific functionality you have added to your bot fails to work.</span></span>

<span data-ttu-id="148ab-133">ボットとの会話を開始するには、その ID を使用します。</span><span class="sxs-lookup"><span data-stu-id="148ab-133">You can also initiate a conversation with your bot by using its ID.</span></span> <span data-ttu-id="148ab-134">これらの方法のいずれかを使用してボットを追加した場合、チャネル会話では対応できません。また、タブやメッセージング拡張機能などの他の Microsoft Teams アプリ機能を利用することはできません。</span><span class="sxs-lookup"><span data-stu-id="148ab-134">When a bot has been added through one of these methods it is not addressable in channel conversations and you cannot take advantage of other Microsoft Teams app capabilities like tabs or messaging extensions.</span></span> <span data-ttu-id="148ab-135">次のいずれかの方法で会話を開始できます。</span><span class="sxs-lookup"><span data-stu-id="148ab-135">You can initiate a conversation in one of the following ways:</span></span>

* <span data-ttu-id="148ab-136">ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots)ページの [チャネル]**で、[ボット** に追加] を選択 **Microsoft Teams。**</span><span class="sxs-lookup"><span data-stu-id="148ab-136">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Channels**, select **Add to Microsoft Teams**.</span></span> <span data-ttu-id="148ab-137">Microsoft Teamsボットとの個人用チャットを起動します。</span><span class="sxs-lookup"><span data-stu-id="148ab-137">Microsoft Teams launches a personal chat with your bot.</span></span>

* <span data-ttu-id="148ab-138">ボットのアプリ ID を次の場所から直接参照Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="148ab-138">Directly reference your bot's app ID from within Microsoft Teams:</span></span>
   1. <span data-ttu-id="148ab-139">ボットの [[ボット ダッシュボード]](https://dev.botframework.com/bots)ページの [詳細] で、ボットの **Microsoft App ID** をコピーします。</span><span class="sxs-lookup"><span data-stu-id="148ab-139">On the [Bot Dashboard](https://dev.botframework.com/bots) page for your bot, under **Details**, copy the **Microsoft App ID** for your bot.</span></span>
  
      ![ボットの AppID の取得](~/assets/images/bots_appid_botframework.png)
  
   2. <span data-ttu-id="148ab-141">[チャットMicrosoft Teamsを開き、[チャットの追加]**アイコンを選択** します。</span><span class="sxs-lookup"><span data-stu-id="148ab-141">Open Microsoft Teams, on the **Chat** pane, select the **Add chat** icon.</span></span> <span data-ttu-id="148ab-142">**[To:]** で、ボットの Microsoft App ID を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="148ab-142">In **To:**, paste your bot's Microsoft App ID.</span></span>
  
      ![ボットのアップロード](~/assets/images/bots_uploading.png)

      <span data-ttu-id="148ab-144">アプリ ID はボット名に解決する必要があります。</span><span class="sxs-lookup"><span data-stu-id="148ab-144">The app ID must resolve to your bot name.</span></span>

   3. <span data-ttu-id="148ab-145">ボットを選択し、メッセージを送信して会話を開始します。</span><span class="sxs-lookup"><span data-stu-id="148ab-145">Select your bot and send a message to initiate a conversation.</span></span>
      <span data-ttu-id="148ab-146">または、ボットのアプリ ID をアプリの左上の検索ボックスに貼り付Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="148ab-146">Alternatively, you can paste your bot's app ID in the search box in the top left in Microsoft Teams.</span></span> <span data-ttu-id="148ab-147">検索結果ページで、[ユーザー] タブに移動してボットを表示し、チャットを開始します。</span><span class="sxs-lookup"><span data-stu-id="148ab-147">In the search results page, navigate to the **People** tab to see your bot and to start chatting with it.</span></span>

<span data-ttu-id="148ab-148">ボットは、オブジェクト内のチーム情報なしで、ボットをチームに追加すると `conversationUpdate` イベントを受け取 `channelData` ります。</span><span class="sxs-lookup"><span data-stu-id="148ab-148">Your bot receives the `conversationUpdate` event as you add the bots to a team, without the team information in the `channelData` object.</span></span>

## <a name="block-a-bot-in-personal-chat"></a><span data-ttu-id="148ab-149">個人用チャットでボットをブロックする</span><span class="sxs-lookup"><span data-stu-id="148ab-149">Block a bot in personal chat</span></span>

<span data-ttu-id="148ab-150">ユーザーは、ボットが個人のチャット メッセージを送信するのをブロックできます。</span><span class="sxs-lookup"><span data-stu-id="148ab-150">Users can choose to block your bot from sending personal chat messages.</span></span> <span data-ttu-id="148ab-151">チャット チャネルでボットを右クリックし、[ボットの会話をブロックする] を選択することで、これを **切り替える場合があります**。</span><span class="sxs-lookup"><span data-stu-id="148ab-151">They may toggle this by right-clicking your bot in the chat channel and choosing **Block bot conversation**.</span></span> <span data-ttu-id="148ab-152">つまり、ボットは引き続きメッセージを送信しますが、ユーザーはメッセージを受信しません。</span><span class="sxs-lookup"><span data-stu-id="148ab-152">This means, your bots continues to send messages, however, the user does not receive the messages.</span></span>

![ボットのブロック](~/assets/images/bots/botdisable.png)

## <a name="remove-a-bot-from-a-team"></a><span data-ttu-id="148ab-154">チームからボットを削除する</span><span class="sxs-lookup"><span data-stu-id="148ab-154">Remove a bot from a team</span></span>

<span data-ttu-id="148ab-155">ユーザーは、チームのビューでボットリストのごみ箱アイコンを選択して、ボットを削除できます。</span><span class="sxs-lookup"><span data-stu-id="148ab-155">Users can delete the bot by choosing the trash-can icon on the bots list in their team's view.</span></span> <span data-ttu-id="148ab-156">これにより、そのチームの使用からボットが削除されるだけで、個々のユーザーは個人のコンテキストで操作できます。</span><span class="sxs-lookup"><span data-stu-id="148ab-156">This only removes the bot from that team's use, individual users can still interact in personal context.</span></span> <span data-ttu-id="148ab-157">個人用コンテキストのボットは、ユーザーが無効にしたり削除したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="148ab-157">Bots in personal context cannot be disabled or removed by users.</span></span>

## <a name="disable-a-bot-in-teams"></a><span data-ttu-id="148ab-158">アプリでボットを無効Teams</span><span class="sxs-lookup"><span data-stu-id="148ab-158">Disable a bot in Teams</span></span>

<span data-ttu-id="148ab-159">ボットがメッセージを受け取るのを停止するには、ボット ダッシュボードに移動し、ボット チャネルMicrosoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="148ab-159">To stop your bot from receiving messages, go to your **Bot Dashboard** and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="148ab-160">[有効にする **] オプションをMicrosoft Teams** します。</span><span class="sxs-lookup"><span data-stu-id="148ab-160">Clear the **Enable on Microsoft Teams** option.</span></span> <span data-ttu-id="148ab-161">これにより、ユーザーはボットを操作できませんが、検出可能であり、ユーザーは引き続きボットに追加Teams。</span><span class="sxs-lookup"><span data-stu-id="148ab-161">This prevents users from interacting with the bot, however, it will still be discoverable and users will still be able to add it to Teams.</span></span>

## <a name="delete-a-bot-from-teams"></a><span data-ttu-id="148ab-162">ボットを削除Teams</span><span class="sxs-lookup"><span data-stu-id="148ab-162">Delete a bot from Teams</span></span>

<span data-ttu-id="148ab-163">ボットを完全に削除するにはTeamsボット ダッシュボードに移動し、ボット チャネルMicrosoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="148ab-163">To remove your bot completely from Teams, go to your **Bot Dashboard** and edit the Microsoft Teams channel.</span></span> <span data-ttu-id="148ab-164">下部にある **[削除** ] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="148ab-164">Choose the **Delete** button at the bottom.</span></span> <span data-ttu-id="148ab-165">これにより、ユーザーはボットを検出、追加、操作できます。</span><span class="sxs-lookup"><span data-stu-id="148ab-165">This prevents users from discovering, adding, and interacting with your bot.</span></span> <span data-ttu-id="148ab-166">これにより、他のユーザーのインスタンスからボットTeams削除されるわけではありませんが、ボットの機能も停止します。</span><span class="sxs-lookup"><span data-stu-id="148ab-166">This does not remove the bot from other user's Teams instances, however, it stops functioning for them as well.</span></span>

## <a name="see-also"></a><span data-ttu-id="148ab-167">関連項目</span><span class="sxs-lookup"><span data-stu-id="148ab-167">See also</span></span>

* [<span data-ttu-id="148ab-168">検査ミドルウェアでボットのデバッグを行う</span><span class="sxs-lookup"><span data-stu-id="148ab-168">Debug your bot with inspection middleware</span></span>](/azure/bot-service/bot-service-debug-inspection-middleware)
* [<span data-ttu-id="148ab-169">ローカルで呼び出しや会議用ボットのデバッグを行う</span><span class="sxs-lookup"><span data-stu-id="148ab-169">Debug your calling and meeting bot locally</span></span>](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
