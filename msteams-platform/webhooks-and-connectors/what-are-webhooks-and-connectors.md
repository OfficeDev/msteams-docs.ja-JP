---
title: Webhook とコネクタ
author: clearab
description: Webhook とコネクタによって Web サービスがどのように Teams クライアントに接続されるかについて説明します。
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2cb763a6637abd3faa500de871119f0b829871bf
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140055"
---
# <a name="webhooks-and-connectors"></a>Webhook とコネクタ

Webhooks とコネクタは、Web サービスをチャネルやチームに接続するのに役立Microsoft Teams。 Webhooks は、ユーザー定義の HTTP コールバックで、ユーザーチャネルで行ったアクションについてユーザーに通知Microsoft Teamsします。 これは、アプリがリアルタイム データを取得する方法です。 コネクタを使用すると、ユーザーは Web サービスから通知とメッセージをサブスクライブして受け取ることができます。 サービスの HTTPS エンドポイントを公開して、カード形式でメッセージを投稿します。

## <a name="outgoing-webhooks"></a>送信 Webhooks

Webhooks は、Teamsアプリとの統合に役立ちます。 送信 Webhooks を使用すると、チャネルから Web サービスにテキスト メッセージを送信できます。 送信 Webhook を構成した後、ユーザーは送信 Webhook を@mention Web サービスにメッセージを送信できます。 サービスは、テキストまたはカードを使用してメッセージに 10 秒以内に応答します。

> [!NOTE]
> 送信 Webhook はチーム単位で構成され、通常のアプリの一部Teamsできません。

## <a name="connectors"></a>コネクタ

コネクタを使用すると、ユーザーは Web サービスから通知とメッセージを受信できます。 サービスの HTTPS エンドポイントを公開して、通常はカードの形式Teamsチャネルにメッセージを投稿します。

### <a name="incoming-webhooks"></a>受信 Webhooks

受信 Webhooks は、アプリからアプリへのメッセージの投稿に役立Teams。 受信 Webhooks が任意のチャネルのチームで有効になっている場合、HTTPS エンドポイントが公開され、正しく書式設定された JSON を受け入れ、そのチャネルにメッセージが挿入されます。 たとえば、受信 Webhook を DevOpsチャネルに作成し、ビルドを構成し、アラートを送信するサービスを同時に展開および監視できます。

### <a name="office-365-connectors"></a>Office 365 コネクタ

Office 365コネクタを使用すると、受信 Webhook 用のカスタム構成ページを作成し、アプリの一部としてパッケージ化Teamsできます。 主にコネクタ カードを使用Office 365メッセージを送信し、制限された一連のカード アクションを追加できます。 たとえば、ユーザーが場所と時刻を選択して、明日の天気に関する更新プログラムを受信できる天気予報コネクタです。 これらはチャネル レベルで構成されますが、チーム レベルでインストールされます。

> [!NOTE]
> AppStore に Office 365 コネクタ Teams配布できます。

## <a name="create-and-send-messages"></a>メッセージを作成して送信する

アクション可能なメッセージを使用すると、ユーザーはメール クライアントを離れることなくアクションを実行できます。ユーザーエンゲージメントが向上します。 Web Office 365受信 Webhook を使用すると、JSON ペイロードを Webhook URL に投稿することでメッセージを送信できます。

## <a name="see-also"></a>関連項目

* [受信 Webhook の作成](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Office 365 コネクタを作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [メッセージを作成して送信する](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [送信 Webhook の作成](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
