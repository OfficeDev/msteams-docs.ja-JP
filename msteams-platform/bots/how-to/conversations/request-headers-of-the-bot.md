---
title: ボットの要求ヘッダーにテナント ID と会話 ID を送信する
description: は、ボットの要求ヘッダーにテナント ID と会話 ID を送信する方法を示します。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 76f667453114ab202d43217b9a4c01a6d14cc1a8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565894"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>ボットの要求ヘッダーにテナント ID と会話 ID を送信する

ボットへの現在の送信要求は、ペイロード全体をアンパックせずにボットがトラフィックをルーティングするのに役立つ情報をヘッダーまたは URL に含みはありません。 アクティビティは、https://<your_domain>/api/messages に似た URL を介してボットに送信されます。 ヘッダーに会話 ID とテナント ID を示す要求を受信します。

## <a name="request-header-fields"></a>要求ヘッダー フィールド

非同期フローと同期フローの両方について、ボットに送信されるすべての要求に、標準以外の 2 つの要求ヘッダー フィールドが追加されます。 次の表に、要求ヘッダー フィールドとその値を示します。

| フィールドキー | 値 |
|----------------|-----------------|
| 会話 ID | 該当し、確認または検証された場合、要求アクティビティに対応する会話 ID。 |
| x-ms テナント ID | 要求アクティビティ内の会話に対応するテナント ID。 |

テナントまたは会話 ID がアクティビティに存在しない場合、またはサービス側で検証されなかった場合、値は空です。

![要求ヘッダー フィールド](~/assets/images/bots/requestheaderfields.png)
