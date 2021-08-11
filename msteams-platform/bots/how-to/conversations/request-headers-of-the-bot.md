---
title: ボットの要求ヘッダーにテナント ID と会話 ID を送信する
description: ボットの要求ヘッダーにテナント ID と会話 ID を送信する方法について説明します。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: a775c09589f59a6d487bf403544afccd5b59f797ac12cf60a9deb1fc2de16644
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57706672"
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
