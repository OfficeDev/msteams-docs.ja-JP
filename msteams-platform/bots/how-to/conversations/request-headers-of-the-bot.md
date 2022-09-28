---
title: ボットの要求ヘッダーにテナント ID と会話 ID を送信する
description: Teams のボットの要求ヘッダーに存在するテナント ID と会話 ID を使用して、ペイロード全体をアンパックせずにボット トラフィックをルーティングする方法について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 3132d91d4b3d0b290ee8e1fb35ebeea076217fe8
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100148"
---
# <a name="request-headers-of-the-bot"></a>ボットのヘッダーをリクエストする

ボットに対する現在の送信要求には、ペイロード全体をアンパックせずにボットがトラフィックをルーティングするのに役立つ情報がヘッダーまたは URL に含まれていません。 アクティビティは、https://<your_domain>/api/messages のような URL を通じてボットに送信されます。 ヘッダーに会話 ID とテナント ID を表示する要求を受信します。

## <a name="request-header-fields"></a>要求ヘッダー フィールド

非同期フローと同期フローの両方で、ボットに送信されるすべての要求に 2 つの非標準の要求ヘッダー フィールドが追加されます。 次の表に、要求ヘッダー フィールドとその値を示します。

| フィールド キー | 値 |
|----------------|-----------------|
| x-ms-conversation-id | 該当する場合は要求アクティビティに対応し、確認または検証された会話 ID。 |
| x-ms-tenant-id | 要求アクティビティの会話に対応するテナント ID。 |

テナントまたは会話 ID がアクティビティに存在しない場合、またはサービス側で検証されなかった場合、値は空です。

![要求ヘッダー フィールド](~/assets/images/bots/requestheaderfields.png)
