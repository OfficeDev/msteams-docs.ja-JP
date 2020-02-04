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
# <a name="notification-only-bots-in-microsoft-teams"></a>Microsoft Teams での通知のみ

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Bot がユーザーに通知を配信し、会話ではないことを目的としている場合`isNotificationOnly`は、アプリマニフェストでフィールドを有効にすることができます。 これにより、次の変更が生じます。

* ユーザーは、通知のみの bot にメッセージを表示できません。
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

* ユーザーは個人チャット`personal`でのみ通知を受け取ることができないため、スコープ付きの通知のみを作成することはできません。 これは、通知を送信する`conversationUpdate`ために必要な詳細情報を提供するイベントを受信できないことを意味します。 通知のみの bot は、 `team`スコープをサポートしており、チームに追加されている場合にのみ正しく機能します。 チームの設定では、ユーザーに通知をチャネルに送信するか、またはプライベートに送信するために必要な情報に、bot がアクセスできるようになります。
* 通知のみのボットは、ユーザーとの通信に事前メッセージを使用します。 詳細については、「[ボット向けの事前メッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」を参照してください。
