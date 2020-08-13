---
title: Webhook とコネクタとは
author: clearab
description: Webhook とコネクタによって Web サービスがどのように Teams クライアントに接続されるかについて説明します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 740806e43af94d5a5da876affec2070a5a461b11
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652059"
---
# <a name="what-are-webhooks-and-connectors"></a><span data-ttu-id="ccc0e-103">Webhook とコネクタとは</span><span class="sxs-lookup"><span data-stu-id="ccc0e-103">What are webhooks and connectors?</span></span>

<span data-ttu-id="ccc0e-104">Webhooks とコネクタは、外部のシステムやサービスを Microsoft Teams のチャネルとチャットと接続するための簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-104">Webhooks and connectors are straightforward ways to connect external systems and services with Microsoft Teams channels and chats.</span></span>

<span data-ttu-id="ccc0e-105">たとえば、ユーザーは別のアプリからの通知を購読することができます (通常はカード形式)。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-105">Users can, for example, subscribe to notifications from another app (typically in the form of cards).</span></span>

## <a name="incoming-webhooks"></a><span data-ttu-id="ccc0e-106">受信 Webhook</span><span class="sxs-lookup"><span data-stu-id="ccc0e-106">Incoming webhooks</span></span>

<span data-ttu-id="ccc0e-107">受信 web フックは、最も単純な種類のコネクタで、チームチャネルを外部サービスにすばやく簡単に接続する方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-107">Incoming webhooks are the simplest type of connector and a quick and easy way to connect a team's channel to an external service.</span></span> <span data-ttu-id="ccc0e-108">任意のチャネル (そのチームに対して有効になっている場合) では、正しく書式設定された JSON を受け入れ、メッセージをチャネルに挿入する HTTPS エンドポイントを公開できます。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-108">For any channel (if enabled for that team), you can expose an HTTPS endpoint that accepts correctly formatted JSON and insert messages into the channel.</span></span>

<span data-ttu-id="ccc0e-109">「[受信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-109">See [Create an incoming webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="ccc0e-110">ユーザーのシナリオ</span><span class="sxs-lookup"><span data-stu-id="ccc0e-110">User scenarios</span></span>

<span data-ttu-id="ccc0e-111">受信 web フックは、特定のチームに固有のシナリオに最適です。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-111">Incoming webhooks are best for scenarios unique to a particular team.</span></span> <span data-ttu-id="ccc0e-112">たとえば、DevOps チャネルで受信 webhook を作成し、通知を送信するようにビルド、展開、および監視サービスを構成することができます。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-112">For example, you could create an incoming webhook in your DevOps channel and configure your build, deployment, and monitoring services to send alerts.</span></span>

## <a name="office-365-connectors"></a><span data-ttu-id="ccc0e-113">Office 365 コネクタ</span><span class="sxs-lookup"><span data-stu-id="ccc0e-113">Office 365 Connectors</span></span>

<span data-ttu-id="ccc0e-114">Office 365 コネクタを使用すると、受信 webhook のカスタム構成ページを作成し、Teams アプリの一部としてパッケージ化することができます。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-114">An Office 365 Connector allows you to create a custom configuration page for your incoming webhook and package it as part of a Teams app.</span></span> <span data-ttu-id="ccc0e-115">その後、アプリストアに対して、より広い範囲で、またはアプリを配布することができます。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-115">You can then distribute that app more broadly or even to our app store.</span></span> <span data-ttu-id="ccc0e-116">メッセージを送信するのは、主に Office 365 コネクタカードを使用して、限られたセットのカードアクションを持つことができます。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-116">You send messages primarily using Office 365 Connector cards that can also have a limited set of card actions.</span></span> <span data-ttu-id="ccc0e-117">これらはチャネルレベルで構成されていますが、チームレベルでインストールされます。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-117">They are configured on the channel level but installed at the team level.</span></span>

<span data-ttu-id="ccc0e-118">「[Office 365 コネクタを作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-118">See [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="ccc0e-119">ユーザーのシナリオ</span><span class="sxs-lookup"><span data-stu-id="ccc0e-119">User scenarios</span></span>

<span data-ttu-id="ccc0e-120">明日の予測に関する更新を受信する場所と時刻を選択できる天気コネクタ。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-120">A weather connector that lets you choose a location and time of day to receive updates about tomorrow's forecast.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="ccc0e-121">送信 Webhook</span><span class="sxs-lookup"><span data-stu-id="ccc0e-121">Outgoing webhooks</span></span>

<span data-ttu-id="ccc0e-122">送信 Webhook を使用すると、ユーザーはチャネルから Web サービスにテキスト メッセージを送信することができます。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-122">Outgoing webhooks allow your users to send text messages from a channel to your web services.</span></span> <span data-ttu-id="ccc0e-123">構成すると、ユーザーはアプリを @mention て、外部サービスにメッセージを送信できるようになります。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-123">Once configured, users can @mention your app and send a message to your external service.</span></span> <span data-ttu-id="ccc0e-124">サービスは5秒でメッセージに応答を送信します。これは、テキストまたはカードを含んでいる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-124">Your service has five seconds to send a response to the message, potentially containing text or a card.</span></span>

<span data-ttu-id="ccc0e-125">送信 web フックはチームごとに構成されており、通常の Teams アプリの一部として含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-125">Outgoing webhooks are configured on a per-team basis and can't be included as part of a normal Teams app.</span></span>

<span data-ttu-id="ccc0e-126">「[送信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-126">See [Create an outgoing webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="ccc0e-127">ユーザーのシナリオ</span><span class="sxs-lookup"><span data-stu-id="ccc0e-127">User scenarios</span></span>

<span data-ttu-id="ccc0e-128">送信 web フックは、大量の情報の収集や交換を必要としないチーム固有のワークフローを完成させるのに最適です。</span><span class="sxs-lookup"><span data-stu-id="ccc0e-128">Outgoing webhooks are best suited for completing team-specific workflows that don't require collecting or exchanging large amounts of information.</span></span>

## <a name="learn-more"></a><span data-ttu-id="ccc0e-129">詳細情報</span><span class="sxs-lookup"><span data-stu-id="ccc0e-129">Learn more</span></span>

* [<span data-ttu-id="ccc0e-130">アプリを計画する</span><span class="sxs-lookup"><span data-stu-id="ccc0e-130">Planning your app</span></span>](../../concepts/extensibility-points.md)
* [<span data-ttu-id="ccc0e-131">アプリのビルド</span><span class="sxs-lookup"><span data-stu-id="ccc0e-131">Building your app</span></span>](../../concepts/building-an-app.md)
* [<span data-ttu-id="ccc0e-132">アプリの発行</span><span class="sxs-lookup"><span data-stu-id="ccc0e-132">Publishing your app</span></span>](../../concepts/deploy-and-publish/overview.md)
