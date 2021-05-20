---
title: 通知のみのボット
description: 通知専用のボットがMicrosoft Teamsに含まれているものについて説明します。
keywords: チームボット通知
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
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="3056d-104">Microsoft Teamsの通知専用ボット</span><span class="sxs-lookup"><span data-stu-id="3056d-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="3056d-105">ボットの唯一の目的がユーザーに通知を配信する目的であり、会話型でない場合は、 `isNotificationOnly` アプリ マニフェストでフィールドを有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="3056d-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="3056d-106">これにより、次の変更が行われます。</span><span class="sxs-lookup"><span data-stu-id="3056d-106">This produces the following changes:</span></span>

* <span data-ttu-id="3056d-107">ユーザーは通知専用のボットにメッセージを送信できません。</span><span class="sxs-lookup"><span data-stu-id="3056d-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="3056d-108">ユーザーはボットを@mentionできません。</span><span class="sxs-lookup"><span data-stu-id="3056d-108">Users cannot @mention the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="3056d-109">ボットのみのアプリは、どちらの場合も個人用アプリ トレイに表示されます `isNotificationOnly: true` `isNotificationOnly: false` 。</span><span class="sxs-lookup"><span data-stu-id="3056d-109">The bot-only apps will surface in the personal app tray in both cases: `isNotificationOnly: true` or `isNotificationOnly: false`.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="3056d-110">アプリ マニフェスト</span><span class="sxs-lookup"><span data-stu-id="3056d-110">App manifest</span></span>

<span data-ttu-id="3056d-111">これを有効にするには、 `isNotificationOnly` に設定 `true` します。</span><span class="sxs-lookup"><span data-stu-id="3056d-111">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="3056d-112">の値 `isNotificationOnly` はブール値であり、文字列ではないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3056d-112">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="3056d-113">ベスト プラクティスと制限事項</span><span class="sxs-lookup"><span data-stu-id="3056d-113">Best practices and limitations</span></span>

* <span data-ttu-id="3056d-114">通知専用ボットは、プロアクティブ メッセージングを使用してユーザーと通信します。</span><span class="sxs-lookup"><span data-stu-id="3056d-114">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="3056d-115">詳細については、「 [ボットのプロアクティブメッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3056d-115">For more information, see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>
