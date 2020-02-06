---
title: 通知専用ボット
description: Microsoft Teams で通知のみのボットがあることを説明します。
keywords: teams の bot 通知
ms.date: 01/29/2020
ms.openlocfilehash: d312f9cd4558d35fc2492b5cf0b4f77b65660833
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783907"
---
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="96f36-104">Microsoft Teams での通知のみのボット</span><span class="sxs-lookup"><span data-stu-id="96f36-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="96f36-105">Bot がユーザーに通知を配信し、会話ではないことを目的としている場合`isNotificationOnly`は、アプリマニフェストでフィールドを有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="96f36-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="96f36-106">これにより、次の変更が生じます。</span><span class="sxs-lookup"><span data-stu-id="96f36-106">This produces the following changes:</span></span>

* <span data-ttu-id="96f36-107">ユーザーが通知のみの bot にメッセージを表示することはできません。</span><span class="sxs-lookup"><span data-stu-id="96f36-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="96f36-108">ユーザーが bot を @mention ことはできません。</span><span class="sxs-lookup"><span data-stu-id="96f36-108">Users cannot @mention the bot.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="96f36-109">アプリマニフェスト</span><span class="sxs-lookup"><span data-stu-id="96f36-109">App manifest</span></span>

<span data-ttu-id="96f36-110">これを有効にする`isNotificationOnly`に`true`は、をに設定します。</span><span class="sxs-lookup"><span data-stu-id="96f36-110">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="96f36-111">の`isNotificationOnly`値は、文字列ではなく boolean であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="96f36-111">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "isNotificationOnly": true,
      "scopes": [
        "personal",
        "team"
      ],
    }
  ],
  ...
}
```

## <a name="best-practices-and-limitations"></a><span data-ttu-id="96f36-112">ベストプラクティスと制限事項</span><span class="sxs-lookup"><span data-stu-id="96f36-112">Best practices and limitations</span></span>

* <span data-ttu-id="96f36-113">通知専用ボットは、ユーザーとの通信に事前メッセージを使用します。</span><span class="sxs-lookup"><span data-stu-id="96f36-113">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="96f36-114">詳細については、「[ボット向けの事前メッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="96f36-114">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>
