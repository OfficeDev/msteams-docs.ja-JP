---
title: ボットの要求ヘッダーにテナント ID と会話 ID を送信する
description: ボットの要求ヘッダーにテナント ID と会話 ID を送信する方法について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 054b5bed99b1569a74ba4f69b144bd1edd60fd3d
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889280"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>ボットの要求ヘッダーにテナント ID と会話 ID を送信する

ボットに対する現在の送信要求には、ペイロード全体を解凍せずにボットがトラフィックをルーティングするのに役立つ情報がヘッダーまたは URL に含まれている必要はありません。 アクティビティは、https://<your_domain>/api/messages に似た URL を介してボットに送信されます。 ヘッダーに会話 ID とテナント ID を表示する要求が受信されます。

## <a name="request-header-fields"></a>要求ヘッダー フィールド

非同期フローと同期フローの両方で、ボットに送信されるすべての要求に、標準以外の 2 つの要求ヘッダー フィールドが追加されます。 次の表に、要求ヘッダー フィールドとその値を示します。

| フィールド キー | 値 |
|----------------|-----------------|
| x-ms-conversation-id | 要求アクティビティに対応する会話 ID (該当する場合は確認済みまたは確認済み)。 |
| x-ms-tenant-id | 要求アクティビティ内の会話に対応するテナント ID。 |

テナントまたは会話 ID がアクティビティに存在しない場合、またはサービス側で検証されていない場合、値は空です。

![要求ヘッダー フィールド](~/assets/images/bots/requestheaderfields.png)
