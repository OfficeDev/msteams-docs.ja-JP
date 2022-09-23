---
title: Webhook とコネクタ
author: clearab
description: このモジュールでは、Webhook とコネクタによって Web サービスがどのように Teams クライアントに接続されるかについて説明します。
ms.localizationpriority: high
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: bb453367eb0d8f4c2c1a54681d67dc38fb3e0358
ms.sourcegitcommit: ef545fac5c0dbe970d81f53b1631930e9196eba3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2022
ms.locfileid: "67991650"
---
# <a name="webhooks-and-connectors"></a>Webhook とコネクタ

Webhook とコネクタは、Microsoft Teams のチャネルとチームに Web サービスを接続するのに役立ちます。 Webhook は、Teams チャネルで実行されたすべてのアクションについてユーザーに通知するユーザー定義の HTTP コールバックです。 これは、アプリがリアルタイム データを取得する方法です。 コネクタを使用すると、ユーザーは Web サービスから通知とメッセージをサブスクライブして受け取ることができます。 サービスの HTTPS エンドポイントを公開して、カード形式でメッセージを投稿します。

> [!IMPORTANT]
> 受信 Webhook 以外の通知ボット Teams アプリを作成することもできます。 同様に実行されますが、通知ボットにはより多くの機能があります。 詳細については、「JavaScript または[受信 Webhook 通知サンプル](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/incoming-webhook-notification)[を使用した通知ボットのビルド](../sbs-gs-notificationbot.yml)」を参照してください。 作業を開始するには、 [Teams Toolkit を](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) 今すぐダウンロードし、調査します。 詳細については、「 [Teams Toolkit ドキュメント」を](../toolkit/teams-toolkit-fundamentals.md)参照してください。

## <a name="outgoing-webhooks"></a>Webhookの送信

Webhook は、Teams を外部アプリと統合するのに役立ちます。 送信 Webhook を使用すると、チャネルから Web サービスにテキスト メッセージを送信できます。 送信 Webhook を構成すると、ユーザーは送信 Webhook を@mentionし、Web サービスにメッセージを送信できます。 サービスは、テキストまたはカードを使用してメッセージに 10 秒以内に応答します。

> [!NOTE]
> 送信 Webhook はチームごとに構成され、通常の Teams アプリの一部として含めることはできません。

## <a name="connectors"></a>コネクタ

コネクタを使用すると、ユーザーは Web サービスから通知とメッセージを受信するようにサブスクライブできます。 これにより、サービスの HTTPS エンドポイントが公開されるようになり、通常はカード形式でメッセージを投稿します。

### <a name="incoming-webhooks"></a>受信 Webhook

受信 Webhook は、アプリから Teams へのメッセージの投稿に役立ちます。 受信 Webhooks が任意のチャネルのチームで有効になっている場合、HTTPS エンドポイントが公開され、正しく書式設定された JSON を受け入れ、そのチャネルにメッセージが挿入されます。 たとえば、DevOps チャネルで受信 Webhook を作成し、ビルドを構成し、サービスを同時にデプロイおよび監視してアラートを送信することができます。

#### <a name="notification-bot-or-incoming-webhook---choose-the-right-one"></a>通知ボットまたは受信 Webhook - 適切なものを選択する

受信 Webhook をビルドする方法を学習する前に、Teams Toolkit を使用して Notification Bot をビルドできることも知りたい場合があります。 Notification Bots を使用すると、さまざまなビジネス シナリオを満たすために、よりカスタマイズ可能なエクスペリエンスを実現できます。

シナリオに適したソリューションを選択できるように、Notification Bot と着信 Webhook の違いについて詳しく説明します。

| &nbsp; | 通知ボット |  着信 Webhook |
| --- | --- | --- |
| 暗号化オプションの説明 | Teams アプリ | Teams 機能 |
| インストールが必要 | はい | いいえ |
| 適切なシナリオ | • 定期的な通知とメッセージを定期的に受け取ります。たとえば、チーム タスクの毎日の通知を受け取ります。 <br>  • 実際のイベントに基づいて通知とメッセージを受信します。 たとえば、チームメイトがファイルをアップロードすると、通知を受け取ります。 | 外部アプリと通信し、他のアプリから通知やメッセージを受信します。 |
| スコープの構成 | • Teams チャネル <br> • グループ チャット <br> • 個人用チャット | Teams チャネル |
| メッセージ プロセス | 通知ボットは Teams アプリケーションとして機能します。 ビジネス ロジックを定義して、データを処理し、カスタマイズされた形式でデータを表示できます。 | Webhook は Teams アプリケーションではなく Teams 機能であるため、処理せずにデータを受信して表示するだけです。 |
| Teams コンテキストを取得する | 通知ボットは、チャネルやユーザー情報、メッセージなどの Teams コンテキストを取得できます。 | いいえ |
| アダプティブ カードを送信する | はい | はい |
| ウェルカム メッセージを送信する | ウェルカム メッセージを送信できます | ウェルカム メッセージなし |
| トリガーがサポートされています | サポートされているすべてのトリガー。 Teams Toolkit を使用している場合は、次のトリガーを使用してテンプレート プロジェクトをすばやく取得できます。 <br> • Azure 関数でホストされる時間トリガー。 <br> • Azure App Service でホストされている HTTP トリガーを Restify する <br> • Azure Functionsでホストされる HTTP トリガー | サポートされているすべてのトリガー |
| ツールの構築 | • [Teams Toolkit の Visual Studio Code の概要](../toolkit/teams-toolkit-fundamentals.md) <br> • [Visual Studio 用 Teams Toolkit の概要](../toolkit/teams-toolkit-fundamentals.md) <br> • [TeamsFx ライブラリ](../toolkit/TeamsFx-CLI.md) <br> • [TeamsFx SDK](../toolkit/TeamsFx-SDK.md) | ツールは必要ありません |
| クラウド リソースが必要 | Azure Bot Framework | リソースは必要ありません |
| チュートリアル | [JavaScript を使用した通知ボットのビルド](../sbs-gs-notificationbot.yml) | [受信 Webhook 通知のサンプル](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/incoming-webhook-notification) |

### <a name="office-365-connectors"></a>Office 365 コネクタ

Office 365 コネクタを使用すると、受信 Webhook のカスタム構成ページを作成し、Teams アプリの一部としてパッケージ化できます。 主に Office 365 コネクタ カードを使用してメッセージを送信し、それらに限られたカード アクションのセットを追加できます。 たとえば、ユーザーが場所と任意の時刻を選択し、明日の天気に関する更新プログラムを受信できるようにする天気予報コネクタなどです。 チャネル レベルで構成されますが、チーム レベルでインストールされます。

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
* [JavaScript を使用した通知ボットのビルド](../sbs-gs-notificationbot.yml)
* [JavaScript を使用して初めてのボット アプリを構築する](../sbs-gs-bot.yml)
