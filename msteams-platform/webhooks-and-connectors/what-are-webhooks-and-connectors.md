---
title: Webhook とコネクタ
author: clearab
description: Webhook とコネクタによって Web サービスがどのように Teams クライアントに接続されるかについて説明します。
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2cb763a6637abd3faa500de871119f0b829871bf
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140055"
---
# <a name="webhooks-and-connectors"></a><span data-ttu-id="95220-103">Webhook とコネクタ</span><span class="sxs-lookup"><span data-stu-id="95220-103">Webhooks and connectors</span></span>

<span data-ttu-id="95220-104">Webhooks とコネクタは、Web サービスをチャネルやチームに接続するのに役立Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="95220-104">Webhooks and connectors help to connect the web services to channels and teams in Microsoft Teams.</span></span> <span data-ttu-id="95220-105">Webhooks は、ユーザー定義の HTTP コールバックで、ユーザーチャネルで行ったアクションについてユーザーに通知Microsoft Teamsします。</span><span class="sxs-lookup"><span data-stu-id="95220-105">Webhooks are user defined HTTP callback that notifies users about any action that has taken place in the Microsoft Teams channel.</span></span> <span data-ttu-id="95220-106">これは、アプリがリアルタイム データを取得する方法です。</span><span class="sxs-lookup"><span data-stu-id="95220-106">It is a way for an app to get real time data.</span></span> <span data-ttu-id="95220-107">コネクタを使用すると、ユーザーは Web サービスから通知とメッセージをサブスクライブして受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="95220-107">Connectors allow users to subscribe to receive notifications and messages from your web services.</span></span> <span data-ttu-id="95220-108">サービスの HTTPS エンドポイントを公開して、カード形式でメッセージを投稿します。</span><span class="sxs-lookup"><span data-stu-id="95220-108">They expose an HTTPS endpoint for your service to post messages in the form of cards.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="95220-109">送信 Webhooks</span><span class="sxs-lookup"><span data-stu-id="95220-109">Outgoing Webhooks</span></span>

<span data-ttu-id="95220-110">Webhooks は、Teamsアプリとの統合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="95220-110">Webhooks help Teams to integrate with external apps.</span></span> <span data-ttu-id="95220-111">送信 Webhooks を使用すると、チャネルから Web サービスにテキスト メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="95220-111">With Outgoing Webhooks, you can send text messages from a channel to the web services.</span></span> <span data-ttu-id="95220-112">送信 Webhook を構成した後、ユーザーは送信 Webhook を@mention Web サービスにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="95220-112">After configuring the Outgoing Webhooks, users can @mention Outgoing Webhook and send a message to web services.</span></span> <span data-ttu-id="95220-113">サービスは、テキストまたはカードを使用してメッセージに 10 秒以内に応答します。</span><span class="sxs-lookup"><span data-stu-id="95220-113">The service responds within ten seconds to the message with a text or a card.</span></span>

> [!NOTE]
> <span data-ttu-id="95220-114">送信 Webhook はチーム単位で構成され、通常のアプリの一部Teamsできません。</span><span class="sxs-lookup"><span data-stu-id="95220-114">Outgoing Webhooks are configured on a per team basis and cannot be included as part of a normal Teams app.</span></span>

## <a name="connectors"></a><span data-ttu-id="95220-115">コネクタ</span><span class="sxs-lookup"><span data-stu-id="95220-115">Connectors</span></span>

<span data-ttu-id="95220-116">コネクタを使用すると、ユーザーは Web サービスから通知とメッセージを受信できます。</span><span class="sxs-lookup"><span data-stu-id="95220-116">Connectors allow users to subscribe to receive notifications and messages from the web services.</span></span> <span data-ttu-id="95220-117">サービスの HTTPS エンドポイントを公開して、通常はカードの形式Teamsチャネルにメッセージを投稿します。</span><span class="sxs-lookup"><span data-stu-id="95220-117">They expose the HTTPS endpoint for the service to post messages to Teams channels, typically in the form of cards.</span></span>

### <a name="incoming-webhooks"></a><span data-ttu-id="95220-118">受信 Webhooks</span><span class="sxs-lookup"><span data-stu-id="95220-118">Incoming Webhooks</span></span>

<span data-ttu-id="95220-119">受信 Webhooks は、アプリからアプリへのメッセージの投稿に役立Teams。</span><span class="sxs-lookup"><span data-stu-id="95220-119">Incoming Webhooks help in posting messages from apps to Teams.</span></span> <span data-ttu-id="95220-120">受信 Webhooks が任意のチャネルのチームで有効になっている場合、HTTPS エンドポイントが公開され、正しく書式設定された JSON を受け入れ、そのチャネルにメッセージが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="95220-120">If Incoming Webhooks are enabled for a team in any channel, it exposes the HTTPS endpoint, which accepts correctly formatted JSON and inserts the messages into that channel.</span></span> <span data-ttu-id="95220-121">たとえば、受信 Webhook を DevOpsチャネルに作成し、ビルドを構成し、アラートを送信するサービスを同時に展開および監視できます。</span><span class="sxs-lookup"><span data-stu-id="95220-121">For example, you can create an Incoming Webhook in your DevOps channel, configure your build, and simultaneously deploy and monitor services to send alerts.</span></span>

### <a name="office-365-connectors"></a><span data-ttu-id="95220-122">Office 365 コネクタ</span><span class="sxs-lookup"><span data-stu-id="95220-122">Office 365 Connectors</span></span>

<span data-ttu-id="95220-123">Office 365コネクタを使用すると、受信 Webhook 用のカスタム構成ページを作成し、アプリの一部としてパッケージ化Teamsできます。</span><span class="sxs-lookup"><span data-stu-id="95220-123">Office 365 Connectors allow you to create a custom configuration page for your Incoming Webhook and package them as part of a Teams app.</span></span> <span data-ttu-id="95220-124">主にコネクタ カードを使用Office 365メッセージを送信し、制限された一連のカード アクションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="95220-124">You send messages primarily using Office 365 Connector cards and have the ability to add a limited set of card actions to them.</span></span> <span data-ttu-id="95220-125">たとえば、ユーザーが場所と時刻を選択して、明日の天気に関する更新プログラムを受信できる天気予報コネクタです。</span><span class="sxs-lookup"><span data-stu-id="95220-125">For example, a weather connector that allows users to select a location and time of day, to receive updates about tomorrow's weather.</span></span> <span data-ttu-id="95220-126">これらはチャネル レベルで構成されますが、チーム レベルでインストールされます。</span><span class="sxs-lookup"><span data-stu-id="95220-126">They are configured on a channel level but are installed at a team level.</span></span>

> [!NOTE]
> <span data-ttu-id="95220-127">AppStore に Office 365 コネクタ Teams配布できます。</span><span class="sxs-lookup"><span data-stu-id="95220-127">You can distribute the Office 365 Connector Teams app to our AppStore.</span></span>

## <a name="create-and-send-messages"></a><span data-ttu-id="95220-128">メッセージを作成して送信する</span><span class="sxs-lookup"><span data-stu-id="95220-128">Create and send messages</span></span>

<span data-ttu-id="95220-129">アクション可能なメッセージを使用すると、ユーザーはメール クライアントを離れることなくアクションを実行できます。ユーザーエンゲージメントが向上します。</span><span class="sxs-lookup"><span data-stu-id="95220-129">Actionable messages allow users to take action without leaving their email client, increasing user engagement.</span></span> <span data-ttu-id="95220-130">Web Office 365受信 Webhook を使用すると、JSON ペイロードを Webhook URL に投稿することでメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="95220-130">With Office 365 and Incoming Webhooks, you can send messages by posting a JSON payload to the webhook URL.</span></span>

## <a name="see-also"></a><span data-ttu-id="95220-131">関連項目</span><span class="sxs-lookup"><span data-stu-id="95220-131">See also</span></span>

* [<span data-ttu-id="95220-132">受信 Webhook の作成</span><span class="sxs-lookup"><span data-stu-id="95220-132">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="95220-133">Office 365 コネクタを作成する</span><span class="sxs-lookup"><span data-stu-id="95220-133">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="95220-134">メッセージを作成して送信する</span><span class="sxs-lookup"><span data-stu-id="95220-134">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="next-step"></a><span data-ttu-id="95220-135">次の手順</span><span class="sxs-lookup"><span data-stu-id="95220-135">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="95220-136">送信 Webhook の作成</span><span class="sxs-lookup"><span data-stu-id="95220-136">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
