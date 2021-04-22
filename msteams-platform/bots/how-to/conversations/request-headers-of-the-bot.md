---
title: ボットの要求ヘッダーにテナント ID と会話 ID を送信する
description: ボットの要求ヘッダーにテナント ID と会話 ID を送信する方法について説明します。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: b3938b3011e09016f8594b2b17ba627d4922947b
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922529"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a><span data-ttu-id="c9421-103">ボットの要求ヘッダーにテナント ID と会話 ID を送信する</span><span class="sxs-lookup"><span data-stu-id="c9421-103">Send tenant ID and conversation ID to the request headers of the bot</span></span>

<span data-ttu-id="c9421-104">ボットに対する現在の送信要求には、ペイロード全体を解凍せずにボットがトラフィックをルーティングするのに役立つ情報がヘッダーまたは URL に含まれている必要はありません。</span><span class="sxs-lookup"><span data-stu-id="c9421-104">The current outgoing requests to the bot do not contain in the header or URL any information that helps bots route the traffic without unpacking the entire payload.</span></span> <span data-ttu-id="c9421-105">アクティビティは、https://<your_domain>/api/messages に似た URL を介してボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="c9421-105">The activities are sent to the bot through a URL similar to https://<your_domain>/api/messages.</span></span> <span data-ttu-id="c9421-106">ヘッダーに会話 ID とテナント ID を表示する要求が受信されます。</span><span class="sxs-lookup"><span data-stu-id="c9421-106">Requests are received to show the conversation ID and tenant ID in the headers.</span></span>

## <a name="request-header-fields"></a><span data-ttu-id="c9421-107">要求ヘッダー フィールド</span><span class="sxs-lookup"><span data-stu-id="c9421-107">Request header fields</span></span>

<span data-ttu-id="c9421-108">非同期フローと同期フローの両方で、ボットに送信されるすべての要求に、標準以外の 2 つの要求ヘッダー フィールドが追加されます。</span><span class="sxs-lookup"><span data-stu-id="c9421-108">Two non-standard request header fields are added to all the requests sent to bots, for both asynchronous flow and synchronous flow.</span></span> <span data-ttu-id="c9421-109">次の表に、要求ヘッダー フィールドとその値を示します。</span><span class="sxs-lookup"><span data-stu-id="c9421-109">The following table provides the request header fields and their values.</span></span>

| <span data-ttu-id="c9421-110">フィールド キー</span><span class="sxs-lookup"><span data-stu-id="c9421-110">Field key</span></span> | <span data-ttu-id="c9421-111">値</span><span class="sxs-lookup"><span data-stu-id="c9421-111">Value</span></span> |
|----------------|-----------------|
| <span data-ttu-id="c9421-112">x-ms-conversation-id</span><span class="sxs-lookup"><span data-stu-id="c9421-112">x-ms-conversation-id</span></span> | <span data-ttu-id="c9421-113">要求アクティビティに対応する会話 ID (該当する場合は確認済みまたは確認済み)。</span><span class="sxs-lookup"><span data-stu-id="c9421-113">The conversation ID corresponding to the request activity if applicable and confirmed or verified.</span></span> |
| <span data-ttu-id="c9421-114">x-ms-tenant-id</span><span class="sxs-lookup"><span data-stu-id="c9421-114">x-ms-tenant-id</span></span> | <span data-ttu-id="c9421-115">要求アクティビティ内の会話に対応するテナント ID。</span><span class="sxs-lookup"><span data-stu-id="c9421-115">The tenant ID corresponding to the conversation in the request activity.</span></span> |

<span data-ttu-id="c9421-116">テナントまたは会話 ID がアクティビティに存在しない場合、またはサービス側で検証されていない場合、値は空です。</span><span class="sxs-lookup"><span data-stu-id="c9421-116">If the tenant or conversation ID is not present in the activity or was not validated on the service side, the value is empty.</span></span>

![要求ヘッダー フィールド](~/assets/images/bots/requestheaderfields.png)
