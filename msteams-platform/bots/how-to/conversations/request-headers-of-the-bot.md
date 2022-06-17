---
title: ボットの要求ヘッダーにテナント ID と会話 ID を送信する
description: このモジュールでは、Teamsのボットの要求ヘッダーにテナント ID と会話 ID を送信する方法について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: dab795a65cf1c6d62bd899c9fa5a5948c44fcdfb
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144125"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>ボットの要求ヘッダーにテナント ID と会話 ID を送信する

ボットに対する現在の送信要求には、ペイロード全体をアンパックせずにボットがトラフィックをルーティングするのに役立つ情報がヘッダーまたは URL に含まれていません。 アクティビティは、https://<your_domain>/api/messages のような URL を通じてボットに送信されます。 ヘッダーに会話 ID とテナント ID を表示する要求を受信します。

## <a name="request-header-fields"></a>要求ヘッダー フィールド

非同期フローと同期フローの両方で、ボットに送信されるすべての要求に 2 つの非標準の要求ヘッダー フィールドが追加されます。 次の表に、要求ヘッダー フィールドとその値を示します。

| フィールド キー | 値 |
|----------------|-----------------|
| x-ms-conversation-id | 該当する場合は要求アクティビティに対応し、確認または検証された会話 ID。 |
| x-ms-tenant-id | 要求アクティビティの会話に対応するテナント ID。 |

テナントまたは会話 ID がアクティビティに存在しない場合、またはサービス側で検証されなかった場合、値は空です。

![要求ヘッダー フィールド](~/assets/images/bots/requestheaderfields.png)
