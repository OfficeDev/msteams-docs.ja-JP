---
title: Webhook とコネクタとは
author: clearab
description: Webhook とコネクタによって Web サービスがどのように Teams クライアントに接続されるかについて説明します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 740806e43af94d5a5da876affec2070a5a461b11
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652059"
---
# <a name="what-are-webhooks-and-connectors"></a>Webhook とコネクタとは

Webhooks とコネクタは、外部のシステムやサービスを Microsoft Teams のチャネルとチャットと接続するための簡単な方法です。

たとえば、ユーザーは別のアプリからの通知を購読することができます (通常はカード形式)。

## <a name="incoming-webhooks"></a>受信 Webhook

受信 web フックは、最も単純な種類のコネクタで、チームチャネルを外部サービスにすばやく簡単に接続する方法を提供します。 任意のチャネル (そのチームに対して有効になっている場合) では、正しく書式設定された JSON を受け入れ、メッセージをチャネルに挿入する HTTPS エンドポイントを公開できます。

「[受信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)」を参照してください。

### <a name="user-scenarios"></a>ユーザーのシナリオ

受信 web フックは、特定のチームに固有のシナリオに最適です。 たとえば、DevOps チャネルで受信 webhook を作成し、通知を送信するようにビルド、展開、および監視サービスを構成することができます。

## <a name="office-365-connectors"></a>Office 365 コネクタ

Office 365 コネクタを使用すると、受信 webhook のカスタム構成ページを作成し、Teams アプリの一部としてパッケージ化することができます。 その後、アプリストアに対して、より広い範囲で、またはアプリを配布することができます。 メッセージを送信するのは、主に Office 365 コネクタカードを使用して、限られたセットのカードアクションを持つことができます。 これらはチャネルレベルで構成されていますが、チームレベルでインストールされます。

「[Office 365 コネクタを作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)」を参照してください。

### <a name="user-scenarios"></a>ユーザーのシナリオ

明日の予測に関する更新を受信する場所と時刻を選択できる天気コネクタ。

## <a name="outgoing-webhooks"></a>送信 Webhook

送信 Webhook を使用すると、ユーザーはチャネルから Web サービスにテキスト メッセージを送信することができます。 構成すると、ユーザーはアプリを @mention て、外部サービスにメッセージを送信できるようになります。 サービスは5秒でメッセージに応答を送信します。これは、テキストまたはカードを含んでいる可能性があります。

送信 web フックはチームごとに構成されており、通常の Teams アプリの一部として含めることはできません。

「[送信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)」を参照してください。

### <a name="user-scenarios"></a>ユーザーのシナリオ

送信 web フックは、大量の情報の収集や交換を必要としないチーム固有のワークフローを完成させるのに最適です。

## <a name="learn-more"></a>詳細情報

* [アプリを計画する](../../concepts/extensibility-points.md)
* [アプリのビルド](../../concepts/building-an-app.md)
* [アプリの発行](../../concepts/deploy-and-publish/overview.md)
