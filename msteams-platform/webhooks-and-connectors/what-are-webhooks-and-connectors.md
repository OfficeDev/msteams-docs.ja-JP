---
title: Web フックとコネクタとは
author: clearab
description: Webhook とコネクタが web サービスを Teams クライアントに接続する方法について説明します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2be6f82bba0efe05a22a8da9da0acc1e0ad6fa00
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674614"
---
# <a name="what-are-webhooks-and-connectors"></a>Web フックとコネクタとは

Webhooks とコネクタを使用すると、web サービスを、Microsoft Teams 内のチャネルやチームに簡単に接続することができます。 

## <a name="outgoing-webhooks"></a>送信 web フック

送信 web フックを使用すると、ユーザーはチャネルから web サービスにテキストメッセージを送信することができます。 構成すると、ユーザーは、送信された webhook を @mention して、サービスにメッセージを送信できるようになります。 サービスには、メッセージに応答を送信する5秒の時間があり、テキストまたはカードを含む可能性があります。

送信 web フックはチームごとに構成され、通常の Teams アプリの一部として含めることはできません。 これらは、大量の情報を収集または交換する必要がないチーム固有のワークロードを完成させるのに最適です。

「[送信 webhook を作成する](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)」を参照してください。

## <a name="connectors"></a>コネクタ

コネクタを使用すると、ユーザーは web サービスから通知やメッセージを受信することができます。 これにより、サービスの HTTPS エンドポイントが公開され、通常はカード形式でメッセージを送信します。

### <a name="incoming-webhooks"></a>受信 web フック

受信 web フックは、最も単純な種類のコネクタです。 Team のチャネル (そのチームに対して有効になっている場合) については、適切に書式設定された JSON を受け入れ、そのチャネルにメッセージを挿入する HTTPS エンドポイントを公開することを選択できます。 これは、サービスにチャネルをすばやく簡単に接続する方法であり、特定のチームに固有のシナリオで使用するのに最適です。 たとえば、DevOps チャネルで受信 webhook を作成し、通知を送信するようにビルド、展開、および監視サービスを構成することができます。

「[受信 webhook を作成する](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)」を参照してください。

### <a name="office-365-connectors"></a>Office 365 コネクタ

Office 365 コネクタを使用すると、受信 webhook のカスタム構成ページを作成し、Teams アプリの一部としてパッケージ化することができます。 その後で、そのアプリをより広い範囲で、またはアプリストアに配布できます。 通常、Office 365 コネクタカードを使用してメッセージを送信し、そのメッセージにもカードアクションの制限セットを追加することができます。 このような例として、ユーザーが明日の天気に関する更新を受信するための場所と時刻を選択できるようにする天気コネクタが挙げられます。 これらはチャネルレベルで構成されますが、チームレベルでインストールされます。

「 [Office 365 Connector を作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)」を参照してください。