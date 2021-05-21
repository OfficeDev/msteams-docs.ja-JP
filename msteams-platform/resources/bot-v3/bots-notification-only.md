---
title: 通知のみのボット
description: 通知専用ボットの機能について説明Microsoft Teams
keywords: teams ボットの通知
ms.topic: conceptual
localization_priority: Normal
ms.date: 01/29/2020
ms.openlocfilehash: 3de462f73733f5f7cf223444ffe6deeb53faaaaa
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566762"
---
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="1a0d8-104">アプリ内の通知専用ボットMicrosoft Teams</span><span class="sxs-lookup"><span data-stu-id="1a0d8-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="1a0d8-105">ボットの唯一の目的がユーザーに通知を配信し、会話型ではない場合は、アプリ マニフェストでフィールド `isNotificationOnly` を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="1a0d8-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="1a0d8-106">これにより、次の変更が行えます。</span><span class="sxs-lookup"><span data-stu-id="1a0d8-106">This produces the following changes:</span></span>

* <span data-ttu-id="1a0d8-107">ユーザーは通知専用ボットにメッセージを送信できません。</span><span class="sxs-lookup"><span data-stu-id="1a0d8-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="1a0d8-108">ユーザーは@mentionを作成できません。</span><span class="sxs-lookup"><span data-stu-id="1a0d8-108">Users cannot @mention the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="1a0d8-109">ボット専用アプリは、どちらの場合も個人用アプリ トレイに表示 `isNotificationOnly: true` されます。 `isNotificationOnly: false`</span><span class="sxs-lookup"><span data-stu-id="1a0d8-109">The bot-only apps will surface in the personal app tray in both cases: `isNotificationOnly: true` or `isNotificationOnly: false`.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="1a0d8-110">アプリ マニフェスト</span><span class="sxs-lookup"><span data-stu-id="1a0d8-110">App manifest</span></span>

<span data-ttu-id="1a0d8-111">これを有効にするには、 に `isNotificationOnly` 設定します `true` 。</span><span class="sxs-lookup"><span data-stu-id="1a0d8-111">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="1a0d8-112">値がブール値であり `isNotificationOnly` 、文字列ではない点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="1a0d8-112">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="1a0d8-113">ベスト プラクティスと制限事項</span><span class="sxs-lookup"><span data-stu-id="1a0d8-113">Best practices and limitations</span></span>

* <span data-ttu-id="1a0d8-114">通知専用ボットは、プロアクティブ メッセージングを使用してユーザーと通信します。</span><span class="sxs-lookup"><span data-stu-id="1a0d8-114">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="1a0d8-115">詳細については、「Proactive [Messaging for bots」を参照してください](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。</span><span class="sxs-lookup"><span data-stu-id="1a0d8-115">For more information, see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>
