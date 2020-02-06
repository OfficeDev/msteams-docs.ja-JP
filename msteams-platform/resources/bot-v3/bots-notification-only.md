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
# <a name="notification-only-bots-in-microsoft-teams"></a>Microsoft Teams での通知のみのボット

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Bot がユーザーに通知を配信し、会話ではないことを目的としている場合`isNotificationOnly`は、アプリマニフェストでフィールドを有効にすることができます。 これにより、次の変更が生じます。

* ユーザーが通知のみの bot にメッセージを表示することはできません。
* ユーザーが bot を @mention ことはできません。

## <a name="app-manifest"></a>アプリマニフェスト

これを有効にする`isNotificationOnly`に`true`は、をに設定します。

> [!NOTE]
> の`isNotificationOnly`値は、文字列ではなく boolean であることに注意してください。

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

## <a name="best-practices-and-limitations"></a>ベストプラクティスと制限事項

* 通知専用ボットは、ユーザーとの通信に事前メッセージを使用します。 詳細については、「[ボット向けの事前メッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」を参照してください。
