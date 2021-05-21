---
title: Webhook とコネクタとは
author: clearab
description: Webhook とコネクタによって Web サービスがどのように Teams クライアントに接続されるかについて説明します。
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: e36b73c0eaed5068311dae6c1ef8fdc073432334
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566804"
---
# <a name="what-are-webhooks-and-connectors"></a><span data-ttu-id="2bda7-103">Webhook とコネクタとは</span><span class="sxs-lookup"><span data-stu-id="2bda7-103">What are webhooks and connectors?</span></span>

<span data-ttu-id="2bda7-104">Webhook とコネクタを使用すると、Web サービスを、Microsoft Teams 内のチャネルやチームに簡単に接続することができます。</span><span class="sxs-lookup"><span data-stu-id="2bda7-104">Webhooks and connectors are a simple way to connect your web services to channels and teams inside Microsoft Teams.</span></span> 

## <a name="outgoing-webhooks"></a><span data-ttu-id="2bda7-105">送信 Webhook</span><span class="sxs-lookup"><span data-stu-id="2bda7-105">Outgoing webhooks</span></span>

<span data-ttu-id="2bda7-106">送信 Webhook を使用すると、ユーザーはチャネルから Web サービスにテキスト メッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="2bda7-106">Outgoing webhooks allow your users to send text messages from a channel to your web services.</span></span> <span data-ttu-id="2bda7-107">構成が完了すると、ユーザーは、送信 Webhook を @メンションして、サービスにメッセージを送信できるようになります。</span><span class="sxs-lookup"><span data-stu-id="2bda7-107">Once configured, your users will be able to @mention your outgoing webhook and send a message to your service.</span></span> <span data-ttu-id="2bda7-108">サービスでメッセージに応答を送信するには 5 秒かかります。メッセージにはテキストやカードが含まれている場合があります。</span><span class="sxs-lookup"><span data-stu-id="2bda7-108">Your service will have five seconds to send a response to the message, potentially containing text or a card.</span></span>

<span data-ttu-id="2bda7-109">送信 Webhook はチーム単位で構成され、通常の Teams アプリの一部として扱うことはできません。</span><span class="sxs-lookup"><span data-stu-id="2bda7-109">Outgoing webhooks are configured on a per-team basis, cannot be included as part of a normal Teams app.</span></span> <span data-ttu-id="2bda7-110">送信 Webhook は、大量の情報収集または情報交換を必要としないチーム固有のワークロードを完成させるのに最も適しています。</span><span class="sxs-lookup"><span data-stu-id="2bda7-110">They are best suited for completing team-specific workloads that don't require large amounts of information to be collected or exchanged.</span></span>

<span data-ttu-id="2bda7-111">詳細については、「送信 [Webhook を作成する」を参照してください](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="2bda7-111">For more information, see [Create an outgoing webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span></span>

## <a name="connectors"></a><span data-ttu-id="2bda7-112">コネクタ</span><span class="sxs-lookup"><span data-stu-id="2bda7-112">Connectors</span></span>

<span data-ttu-id="2bda7-113">コネクタを使用すると、ユーザーは Web サービスから通知とメッセージを受信することができます。</span><span class="sxs-lookup"><span data-stu-id="2bda7-113">Connectors allow users to subscribe to receive notifications and messages from your web services.</span></span> <span data-ttu-id="2bda7-114">これにより、サービスの HTTPS エンドポイントが公開されるようになり、通常はカード形式でメッセージを投稿します。</span><span class="sxs-lookup"><span data-stu-id="2bda7-114">They expose an HTTPS endpoint for your service to post messages to - typically in the form of cards.</span></span>

### <a name="incoming-webhooks"></a><span data-ttu-id="2bda7-115">受信 Webhook</span><span class="sxs-lookup"><span data-stu-id="2bda7-115">Incoming webhooks</span></span>

<span data-ttu-id="2bda7-116">受信 Webhook は、最も簡単な種類のコネクタです。</span><span class="sxs-lookup"><span data-stu-id="2bda7-116">Incoming webhooks are the simplest type of connector.</span></span> <span data-ttu-id="2bda7-117">チームのどのチャネルにおいても (チームに対して有効になっている場合)、適切に書式設定された JSON に対応し、そのチャネルにメッセージを挿入する HTTPS エンドポイントを公開することができます。</span><span class="sxs-lookup"><span data-stu-id="2bda7-117">For any channel in team (if they are enabled for that team) you can choose to expose an HTTPS endpoint that will accept correctly formatted JSON and insert messages into that channel.</span></span> <span data-ttu-id="2bda7-118">これは、チャネルをサービスにすばやく簡単に接続する方法であり、特定のチームの固有のシナリオで使用するのに最適です。</span><span class="sxs-lookup"><span data-stu-id="2bda7-118">They are a quick and easy way to connect a channel to your service, and are best used for scenarios that are unique to a particular team.</span></span> <span data-ttu-id="2bda7-119">たとえば、アラート送信が行えるように、DevOps チャネルで受信 Webhook を作成し、ビルド、展開、監視サービスを構成することができます。</span><span class="sxs-lookup"><span data-stu-id="2bda7-119">For example, you could create an incoming webhook in your DevOps channel and configure your build, deployment and monitoring services to send alerts.</span></span>

<span data-ttu-id="2bda7-120">詳細については、「受信 [Webhook を作成する」を参照してください](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="2bda7-120">For more information, see [Create an incoming webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span></span>

### <a name="office-365-connectors"></a><span data-ttu-id="2bda7-121">Office 365 コネクタ</span><span class="sxs-lookup"><span data-stu-id="2bda7-121">Office 365 Connectors</span></span>

<span data-ttu-id="2bda7-122">Office 365 コネクタを使用すると、受信 Webhook のカスタム構成ページの作成ができ、Teams アプリの一部としてパッケージ化することができます。</span><span class="sxs-lookup"><span data-stu-id="2bda7-122">Office 365 Connectors allow you to create a custom configuration page for your incoming webhook, and package them as part of a Teams app.</span></span> <span data-ttu-id="2bda7-123">その後、そのアプリを App Store など、より広範囲に配布することができます。</span><span class="sxs-lookup"><span data-stu-id="2bda7-123">You can then distribute that app more broadly, or even to our app store.</span></span> <span data-ttu-id="2bda7-124">通常、Office 365 コネクタ カードを使用してメッセージを送信します。また、そのメッセージにカード アクションの制限一式を追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="2bda7-124">You send messages primarily using Office 365 Connector cards, and have the ability to add a limited set of card actions to them as well.</span></span> <span data-ttu-id="2bda7-125">たとえば、天気のコネクタを使用すると、ユーザーが翌日の天気に関する更新を受信する場所と時刻を選択できるようになります。</span><span class="sxs-lookup"><span data-stu-id="2bda7-125">A good example of this is a weather connector that allows users to choose a location and time of day to receive updates about tomorrow's weather.</span></span> <span data-ttu-id="2bda7-126">Office 365 コネクタの構成はチャネルのレベルで行われますが、インストールはチームのレベルで行われます。</span><span class="sxs-lookup"><span data-stu-id="2bda7-126">They are configured on a channel level, but are installed at a team level.</span></span>

<span data-ttu-id="2bda7-127">詳細については、「Create [an an Office 365 コネクタ」を参照してください](~/webhooks-and-connectors/how-to/connectors-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="2bda7-127">For more information, see [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span></span>
