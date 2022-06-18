---
title: Webhook とコネクタ
author: clearab
description: このモジュールでは、Webhook とコネクタによって Web サービスがどのように Teams クライアントに接続されるかについて説明します。
ms.localizationpriority: high
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 604f4bce563957afb477a58d47ef8235e4b5c30d
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142179"
---
# <a name="webhooks-and-connectors"></a>Webhook とコネクタ

Webhook とコネクタは、Microsoft Teams のチャネルとチームに Web サービスを接続するのに役立ちます。 Webhook は、Microsoft Teams チャネルで実行されたすべてのアクションについてユーザーに通知するユーザー定義の HTTP コールバックです。 これは、アプリがリアルタイム データを取得する方法です。 コネクタを使用すると、ユーザーは Web サービスから通知とメッセージをサブスクライブして受け取ることができます。 サービスの HTTPS エンドポイントを公開して、カード形式でメッセージを投稿します。

## <a name="outgoing-webhooks"></a>Webhookの送信

Webhook は、Teams を外部アプリと統合するのに役立ちます。 送信 Webhook を使用すると、チャネルから Web サービスにテキスト メッセージを送信できます。 送信 Webhook を構成すると、ユーザーは送信 Webhook を@mentionし、Web サービスにメッセージを送信できます。 サービスは、テキストまたはカードを使用してメッセージに 10 秒以内に応答します。

> [!NOTE]
> 送信 Webhook はチームごとに構成され、通常の Teams アプリの一部として含めることはできません。

## <a name="connectors"></a>コネクタ

コネクタを使用すると、ユーザーは Web サービスから通知とメッセージを受信するようにサブスクライブできます。 これにより、サービスの HTTPS エンドポイントが公開されるようになり、通常はカード形式でメッセージを投稿します。

### <a name="incoming-webhooks"></a>受信 Webhook

受信 Webhook は、アプリから Teams へのメッセージの投稿に役立ちます。 受信 Webhooks が任意のチャネルのチームで有効になっている場合、HTTPS エンドポイントが公開され、正しく書式設定された JSON を受け入れ、そのチャネルにメッセージが挿入されます。 たとえば、DevOps チャネルで受信 Webhook を作成し、ビルドを構成し、サービスを同時にデプロイおよび監視してアラートを送信することができます。

### <a name="office-365-connectors"></a>Office 365 コネクタ

Office 365 コネクタを使用すると、受信 Webhook のカスタム構成ページを作成し、Teams アプリの一部としてパッケージ化できます。 主に Office 365 コネクタ カードを使用してメッセージを送信し、それらに限られたカード アクションのセットを追加できます。 たとえば、ユーザーが場所と時刻を選択し、明日の天気に関する更新プログラムを受信できるようにする天気予報コネクタなどです。 チャネル レベルで構成されていますが、チーム レベルでインストールされます。

> [!NOTE]
> Office 365 Connector Teams アプリを AppStore に配布できます。

## <a name="create-and-send-messages"></a>メッセージを作成して送信する

アクション可能なメッセージを使用すると、ユーザーは電子メール クライアントから離れることなくアクションを実行できるため、ユーザーエンゲージメントが向上します。 Office 365 と受信 Webhook では、WEBhook URL に JSON ペイロードを投稿することでメッセージを送信できます。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [送信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="see-also"></a>関連項目

* [受信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Office 365 コネクタを作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [メッセージを作成して送信する](~/webhooks-and-connectors/how-to/connectors-using.md)
