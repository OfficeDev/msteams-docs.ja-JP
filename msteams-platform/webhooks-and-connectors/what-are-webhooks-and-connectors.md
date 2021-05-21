---
title: Webhook とコネクタとは
author: clearab
description: Webhook とコネクタによって Web サービスがどのように Teams クライアントに接続されるかについて説明します。
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: e36b73c0eaed5068311dae6c1ef8fdc073432334
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566804"
---
# <a name="what-are-webhooks-and-connectors"></a>Webhook とコネクタとは

Webhook とコネクタを使用すると、Web サービスを、Microsoft Teams 内のチャネルやチームに簡単に接続することができます。 

## <a name="outgoing-webhooks"></a>送信 Webhook

送信 Webhook を使用すると、ユーザーはチャネルから Web サービスにテキスト メッセージを送信することができます。 構成が完了すると、ユーザーは、送信 Webhook を @メンションして、サービスにメッセージを送信できるようになります。 サービスでメッセージに応答を送信するには 5 秒かかります。メッセージにはテキストやカードが含まれている場合があります。

送信 Webhook はチーム単位で構成され、通常の Teams アプリの一部として扱うことはできません。 送信 Webhook は、大量の情報収集または情報交換を必要としないチーム固有のワークロードを完成させるのに最も適しています。

詳細については、「送信 [Webhook を作成する」を参照してください](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)。

## <a name="connectors"></a>コネクタ

コネクタを使用すると、ユーザーは Web サービスから通知とメッセージを受信することができます。 これにより、サービスの HTTPS エンドポイントが公開されるようになり、通常はカード形式でメッセージを投稿します。

### <a name="incoming-webhooks"></a>受信 Webhook

受信 Webhook は、最も簡単な種類のコネクタです。 チームのどのチャネルにおいても (チームに対して有効になっている場合)、適切に書式設定された JSON に対応し、そのチャネルにメッセージを挿入する HTTPS エンドポイントを公開することができます。 これは、チャネルをサービスにすばやく簡単に接続する方法であり、特定のチームの固有のシナリオで使用するのに最適です。 たとえば、アラート送信が行えるように、DevOps チャネルで受信 Webhook を作成し、ビルド、展開、監視サービスを構成することができます。

詳細については、「受信 [Webhook を作成する」を参照してください](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)。

### <a name="office-365-connectors"></a>Office 365 コネクタ

Office 365 コネクタを使用すると、受信 Webhook のカスタム構成ページの作成ができ、Teams アプリの一部としてパッケージ化することができます。 その後、そのアプリを App Store など、より広範囲に配布することができます。 通常、Office 365 コネクタ カードを使用してメッセージを送信します。また、そのメッセージにカード アクションの制限一式を追加することもできます。 たとえば、天気のコネクタを使用すると、ユーザーが翌日の天気に関する更新を受信する場所と時刻を選択できるようになります。 Office 365 コネクタの構成はチャネルのレベルで行われますが、インストールはチームのレベルで行われます。

詳細については、「Create [an an Office 365 コネクタ」を参照してください](~/webhooks-and-connectors/how-to/connectors-creating.md)。
