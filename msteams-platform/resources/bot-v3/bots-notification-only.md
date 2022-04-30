---
title: 通知のみのボット
description: Microsoft Teams 内の通知専用ボットについて説明します
keywords: teams ボット通知
ms.topic: conceptual
ms.localizationpriority: high
ms.date: 01/29/2020
ms.openlocfilehash: 1ee009fb76a52bcebdd3fe24c7a672f1ed455b42
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111480"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Microsoft Teams の通知専用ボット

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットの唯一の目的がユーザーに通知を配信することであり、会話ではない場合は、アプリ マニフェストのフィールドを `isNotificationOnly` 有効にすることができます。 これにより、次の変更が生成されます。

* ユーザーは通知専用ボットにメッセージを送信できません。
* ユーザーはボットを @メンションできません。

> [!NOTE]
> ボットのみのアプリは、`isNotificationOnly: true` または `isNotificationOnly: false` の両方の場合にパーソナル アプリ トレイに表示されます。

## <a name="app-manifest"></a>アプリ マニフェスト

これを有効にするには、`isNotificationOnly` を `true` に設定します。

> [!NOTE]
> `isNotificationOnly` の値はブール値であり、文字列ではありません。

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

* 通知専用ボットでは、プロアクティブ メッセージングを使用してユーザーと通信します。 詳細については、「[ボット用のプロアクティブ メッセージング](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」を参照してください。
