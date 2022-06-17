---
title: 通知のみのボット
description: このモジュールでは、Microsoft Teams、アプリ マニフェスト、およびそのベスト プラクティスと制限事項に含まれる通知専用ボットについて説明します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: 547ef73cfd036efe566afe15e4f50701a275c2cd
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144300"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Microsoft Teams の通知専用ボット

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

ボットの唯一の目的がユーザーに通知を配信することであり、会話ではない場合は、アプリ マニフェストのフィールドを `isNotificationOnly` 有効にすることができます。 これにより、次の変更が生成されます。

* ユーザーは通知専用ボットにメッセージを送信できません。
* ユーザーはボットを@mentionできません。

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
