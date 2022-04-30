---
title: ボットの要求ヘッダーにテナント ID と会話 ID を送信する
description: テナント ID と会話 ID をボットの要求ヘッダーに送信する方法について説明します。
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 9b63dd81eeccbf78989a31a06baa5d678916acef
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111291"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>ボットの要求ヘッダーにテナント ID と会話 ID を送信する

ボットへの現在の送信要求には、ペイロード全体を解凍せずにボットがトラフィックをルーティングするのに役立つ情報がヘッダーまたは URL に含まれていません。 アクティビティは、https://<your_domain>/api/messages のような URL を通じてボットに送信されます。 ヘッダーに会話 ID とテナント ID を表示する要求を受信します。

## <a name="request-header-fields"></a>要求ヘッダー フィールド

非同期フローと同期フローの両方で、ボットに送信されるすべての要求に 2 つの非標準の要求ヘッダー フィールドが追加されます。 次の表に、要求ヘッダー フィールドとその値を示します。

| フィールド キー | 値 |
|----------------|-----------------|
| x-ms-conversation-id | 該当する場合は要求アクティビティに対応し、確認または検証された会話 ID。 |
| x-ms-tenant-id | 要求アクティビティの会話に対応するテナント ID。 |

テナントまたは会話 ID がアクティビティに存在しないか、サービス側で検証されていない場合、値は空です。

![要求ヘッダー フィールド](~/assets/images/bots/requestheaderfields.png)
