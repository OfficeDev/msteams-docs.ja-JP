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
# <a name="notification-only-bots-in-microsoft-teams"></a>アプリ内の通知専用ボットMicrosoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットの唯一の目的がユーザーに通知を配信し、会話型ではない場合は、アプリ マニフェストでフィールド `isNotificationOnly` を有効にできます。 これにより、次の変更が行えます。

* ユーザーは通知専用ボットにメッセージを送信できません。
* ユーザーは@mentionを作成できません。

> [!NOTE]
> ボット専用アプリは、どちらの場合も個人用アプリ トレイに表示 `isNotificationOnly: true` されます。 `isNotificationOnly: false`

## <a name="app-manifest"></a>アプリ マニフェスト

これを有効にするには、 に `isNotificationOnly` 設定します `true` 。

> [!NOTE]
> 値がブール値であり `isNotificationOnly` 、文字列ではない点に注意してください。

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

## <a name="best-practices-and-limitations"></a>ベスト プラクティスと制限事項

* 通知専用ボットは、プロアクティブ メッセージングを使用してユーザーと通信します。 詳細については、「Proactive [Messaging for bots」を参照してください](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。
