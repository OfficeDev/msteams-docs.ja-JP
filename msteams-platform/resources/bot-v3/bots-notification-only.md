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
# <a name="notification-only-bots-in-microsoft-teams"></a>Microsoft Teamsの通知専用ボット

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットの唯一の目的がユーザーに通知を配信する目的であり、会話型でない場合は、 `isNotificationOnly` アプリ マニフェストでフィールドを有効にすることができます。 これにより、次の変更が行われます。

* ユーザーは通知専用のボットにメッセージを送信できません。
* ユーザーはボットを@mentionできません。

> [!NOTE]
> ボットのみのアプリは、どちらの場合も個人用アプリ トレイに表示されます `isNotificationOnly: true` `isNotificationOnly: false` 。

## <a name="app-manifest"></a>アプリ マニフェスト

これを有効にするには、 `isNotificationOnly` に設定 `true` します。

> [!NOTE]
> の値 `isNotificationOnly` はブール値であり、文字列ではないことに注意してください。

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

* 通知専用ボットは、プロアクティブ メッセージングを使用してユーザーと通信します。 詳細については、「 [ボットのプロアクティブメッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」を参照してください。
