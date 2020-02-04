---
title: Web フックとコネクタとは
author: clearab
description: Webhook とコネクタが web サービスを Teams クライアントに接続する方法について説明します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2be6f82bba0efe05a22a8da9da0acc1e0ad6fa00
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674614"
---
# <a name="what-are-webhooks-and-connectors"></a><span data-ttu-id="cece4-103">Web フックとコネクタとは</span><span class="sxs-lookup"><span data-stu-id="cece4-103">What are webhooks and connectors?</span></span>

<span data-ttu-id="cece4-104">Webhooks とコネクタを使用すると、web サービスを、Microsoft Teams 内のチャネルやチームに簡単に接続することができます。</span><span class="sxs-lookup"><span data-stu-id="cece4-104">Webhooks and connectors are a simple way to connect your web services to channels and teams inside Microsoft Teams.</span></span> 

## <a name="outgoing-webhooks"></a><span data-ttu-id="cece4-105">送信 web フック</span><span class="sxs-lookup"><span data-stu-id="cece4-105">Outgoing webhooks</span></span>

<span data-ttu-id="cece4-106">送信 web フックを使用すると、ユーザーはチャネルから web サービスにテキストメッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="cece4-106">Outgoing webhooks allow your users to send text messages from a channel to your web services.</span></span> <span data-ttu-id="cece4-107">構成すると、ユーザーは、送信された webhook を @mention して、サービスにメッセージを送信できるようになります。</span><span class="sxs-lookup"><span data-stu-id="cece4-107">Once configured, your users will be able to @mention your outgoing webhook and send a message to your service.</span></span> <span data-ttu-id="cece4-108">サービスには、メッセージに応答を送信する5秒の時間があり、テキストまたはカードを含む可能性があります。</span><span class="sxs-lookup"><span data-stu-id="cece4-108">Your service will have five seconds to send a response to the message, potentially containing text or a card.</span></span>

<span data-ttu-id="cece4-109">送信 web フックはチームごとに構成され、通常の Teams アプリの一部として含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="cece4-109">Outgoing webhooks are configured on a per-team basis, cannot be included as part of a normal Teams app.</span></span> <span data-ttu-id="cece4-110">これらは、大量の情報を収集または交換する必要がないチーム固有のワークロードを完成させるのに最適です。</span><span class="sxs-lookup"><span data-stu-id="cece4-110">They are best suited for completing team-specific workloads that don't require large amounts of information to be collected or exchanged.</span></span>

<span data-ttu-id="cece4-111">「[送信 webhook を作成する](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cece4-111">See [Create an outgoing webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span></span>

## <a name="connectors"></a><span data-ttu-id="cece4-112">コネクタ</span><span class="sxs-lookup"><span data-stu-id="cece4-112">Connectors</span></span>

<span data-ttu-id="cece4-113">コネクタを使用すると、ユーザーは web サービスから通知やメッセージを受信することができます。</span><span class="sxs-lookup"><span data-stu-id="cece4-113">Connectors allow users to subscribe to receive notifications and messages from your web services.</span></span> <span data-ttu-id="cece4-114">これにより、サービスの HTTPS エンドポイントが公開され、通常はカード形式でメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="cece4-114">They expose an HTTPS endpoint for your service to post messages to - typically in the form of cards.</span></span>

### <a name="incoming-webhooks"></a><span data-ttu-id="cece4-115">受信 web フック</span><span class="sxs-lookup"><span data-stu-id="cece4-115">Incoming webhooks</span></span>

<span data-ttu-id="cece4-116">受信 web フックは、最も単純な種類のコネクタです。</span><span class="sxs-lookup"><span data-stu-id="cece4-116">Incoming webhooks are a the simplest type of connector.</span></span> <span data-ttu-id="cece4-117">Team のチャネル (そのチームに対して有効になっている場合) については、適切に書式設定された JSON を受け入れ、そのチャネルにメッセージを挿入する HTTPS エンドポイントを公開することを選択できます。</span><span class="sxs-lookup"><span data-stu-id="cece4-117">For any channel in team (if they are enabled for that team) you can choose to expose an HTTPS endpoint that will accept correctly formatted JSON and insert messages into that channel.</span></span> <span data-ttu-id="cece4-118">これは、サービスにチャネルをすばやく簡単に接続する方法であり、特定のチームに固有のシナリオで使用するのに最適です。</span><span class="sxs-lookup"><span data-stu-id="cece4-118">They are a quick and easy way to connect a channel to your service, and are best used for scenarios that are unique to a particular team.</span></span> <span data-ttu-id="cece4-119">たとえば、DevOps チャネルで受信 webhook を作成し、通知を送信するようにビルド、展開、および監視サービスを構成することができます。</span><span class="sxs-lookup"><span data-stu-id="cece4-119">For example, you could create an incoming webhook in your DevOps channel and configure your build, deployment and monitoring services to send alerts.</span></span>

<span data-ttu-id="cece4-120">「[受信 webhook を作成する](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cece4-120">See [Create an incoming webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span></span>

### <a name="office-365-connectors"></a><span data-ttu-id="cece4-121">Office 365 コネクタ</span><span class="sxs-lookup"><span data-stu-id="cece4-121">Office 365 Connectors</span></span>

<span data-ttu-id="cece4-122">Office 365 コネクタを使用すると、受信 webhook のカスタム構成ページを作成し、Teams アプリの一部としてパッケージ化することができます。</span><span class="sxs-lookup"><span data-stu-id="cece4-122">Office 365 Connectors allow you to create a custom configuration page for your incoming webhook, and package them as part of a Teams app.</span></span> <span data-ttu-id="cece4-123">その後で、そのアプリをより広い範囲で、またはアプリストアに配布できます。</span><span class="sxs-lookup"><span data-stu-id="cece4-123">You can then distribute that app more broadly, or even to our app store.</span></span> <span data-ttu-id="cece4-124">通常、Office 365 コネクタカードを使用してメッセージを送信し、そのメッセージにもカードアクションの制限セットを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="cece4-124">You send messages primarily using Office 365 Connector cards, and have the ability to add a limited set of card actions to them as well.</span></span> <span data-ttu-id="cece4-125">このような例として、ユーザーが明日の天気に関する更新を受信するための場所と時刻を選択できるようにする天気コネクタが挙げられます。</span><span class="sxs-lookup"><span data-stu-id="cece4-125">A good example of this is a weather connector that allows users to choose a location and time of day to receive updates about tomorrow's weather.</span></span> <span data-ttu-id="cece4-126">これらはチャネルレベルで構成されますが、チームレベルでインストールされます。</span><span class="sxs-lookup"><span data-stu-id="cece4-126">They are configured on a channel level, but are installed at a team level.</span></span>

<span data-ttu-id="cece4-127">「 [Office 365 Connector を作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cece4-127">See [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span></span>