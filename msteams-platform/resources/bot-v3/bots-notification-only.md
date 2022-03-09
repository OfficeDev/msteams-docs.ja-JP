---
title: 通知のみのボット
description: 通知専用ボットの機能について説明Microsoft Teams
keywords: teams ボットの通知
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: d3ee5343ea159950859237f2a488557d9063eb6e
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355728"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>通知専用のボット (Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットの唯一の目的 `isNotificationOnly` がユーザーに通知を配信し、会話型ではない場合は、アプリ マニフェストでフィールドを有効にできます。 これにより、次の変更が行えます。

* ユーザーは通知専用ボットにメッセージを送信できません。
* ユーザーは@mentionを作成できません。

> [!NOTE]
> ボット専用アプリは、どちらの場合も個人用アプリ トレイに表示されます。 `isNotificationOnly: true` `isNotificationOnly: false`

## <a name="app-manifest"></a>アプリ マニフェスト

これを有効にするには、 に設定 `isNotificationOnly` します `true`。

> [!NOTE]
> 値はブール `isNotificationOnly` 型 (Boolean) で、文字列ではありません。

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
