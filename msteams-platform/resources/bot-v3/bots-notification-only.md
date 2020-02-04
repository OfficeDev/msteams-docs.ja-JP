---
title: 通知のみのボット
description: Microsoft Teams での通知のみの bot の機能について説明します。
keywords: teams の bot 通知
ms.date: 05/20/2019
ms.openlocfilehash: 37652bc2d6171191c81be4e5a2875f47c79574f9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674661"
---
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="d3e51-104">Microsoft Teams での通知のみ</span><span class="sxs-lookup"><span data-stu-id="d3e51-104">Notification only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="d3e51-105">Bot がユーザーに通知を配信し、会話ではないことを目的としている場合`isNotificationOnly`は、アプリマニフェストでフィールドを有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="d3e51-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="d3e51-106">これにより、次の変更が生じます。</span><span class="sxs-lookup"><span data-stu-id="d3e51-106">This produces the following changes:</span></span>

* <span data-ttu-id="d3e51-107">ユーザーは、通知のみの bot にメッセージを表示できません。</span><span class="sxs-lookup"><span data-stu-id="d3e51-107">Users cannot message your notification only bot.</span></span>
* <span data-ttu-id="d3e51-108">ユーザーが bot を @mention ことはできません。</span><span class="sxs-lookup"><span data-stu-id="d3e51-108">Users cannot @mention the bot.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="d3e51-109">アプリマニフェスト</span><span class="sxs-lookup"><span data-stu-id="d3e51-109">App manifest</span></span>

<span data-ttu-id="d3e51-110">これを有効にする`isNotificationOnly`に`true`は、をに設定します。</span><span class="sxs-lookup"><span data-stu-id="d3e51-110">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="d3e51-111">の`isNotificationOnly`値は、文字列ではなく boolean であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d3e51-111">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="d3e51-112">ベストプラクティスと制限事項</span><span class="sxs-lookup"><span data-stu-id="d3e51-112">Best practices and limitations</span></span>

* <span data-ttu-id="d3e51-113">ユーザーは個人チャット`personal`でのみ通知を受け取ることができないため、スコープ付きの通知のみを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="d3e51-113">You cannot create a `personal` scoped notification only bot, as the user cannot message your notification only bot in a personal chat.</span></span> <span data-ttu-id="d3e51-114">これは、通知を送信する`conversationUpdate`ために必要な詳細情報を提供するイベントを受信できないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="d3e51-114">This means that you can't receive a `conversationUpdate` event that would provide you with the necessary details to send a notification.</span></span> <span data-ttu-id="d3e51-115">通知のみの bot は、 `team`スコープをサポートしており、チームに追加されている場合にのみ正しく機能します。</span><span class="sxs-lookup"><span data-stu-id="d3e51-115">Your notification only bot will only function correctly if it supports the `team` scope and is added to a team.</span></span> <span data-ttu-id="d3e51-116">チームの設定では、ユーザーに通知をチャネルに送信するか、またはプライベートに送信するために必要な情報に、bot がアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="d3e51-116">In the team setting, your bot will have access to the necessary information to either send a notification to a channel or privately to a user.</span></span>
* <span data-ttu-id="d3e51-117">通知のみのボットは、ユーザーとの通信に事前メッセージを使用します。</span><span class="sxs-lookup"><span data-stu-id="d3e51-117">Notification only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="d3e51-118">詳細については、「[ボット向けの事前メッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d3e51-118">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>
