---
title: Microsoft Teams のボット
author: surbhigupta
description: この記事では、Microsoft Teams の会話ボットを使用して、ファイルの共有、プロアクティブ通知の送信、対話型カードの送信、通話、ボット コマンドの呼び出し、IVR を行います。
ms.topic: overview
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 4f421c5bcc8251976a54bf5f94b7dafbcc50c64c
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791581"
---
# <a name="build-bots-for-teams"></a>Teams 用のボットを構築する

ボットは、チャットボットまたは会話ボットとも呼ばれます。 これは、カスタマー サービスやサポート スタッフなどのユーザーが単純で反復的なタスクを実行するアプリです。 ボットの日常的な使用には、天気に関する情報を提供するボット、ディナーの予約を行うボット、旅行情報を提供するボットなどがあります。 ボットとのやり取りは、質問や回答を素早く行ったり、複雑な会話になったりする場合があります。

> [!NOTE]
> まず、 [JavaScript を使用して最初のボット アプリをビルド](../sbs-gs-bot.yml) するか、新しい世代の Teams 開発ツールを使用して [JavaScript を使用して通知ボットをビルド](../sbs-gs-notificationbot.yml) することをお勧めします。 詳細については、「 [Teams Toolkit の概要](../toolkit/teams-toolkit-fundamentals.md)」を参照してください。

> [!IMPORTANT]
>
> * 現在、ボットは Government Community Cloud (GCC) と GCC-High で利用できますが、国防総省 (DOD) では利用できません。
>
> * Microsoft Teams 内のボット アプリケーションは、[Azure ボット サービス](/azure/bot-service/how-to-deploy-gov-cloud-high)を通じて GCC-High で利用でき、ボット チャネルの登録は Azure Government ポータルで行う必要があります。
>
> * GCCH のアプリケーションは、マニフェスト バージョン v1.10 までしかサポートしていません。 アダプティブ カードの画像 URL は、GCCH 環境ではサポートされていません。 画像 URL を Base64 でエンコードされた DataUri に置き換えることができます。

会話ボットを使用すると、ユーザーはテキスト、対話型カード、タスク モジュールを使用して Web サービスと対話できます。

:::image type="content" source="../assets/images/invokebotwithtext.png" alt-text="スクリーンショットは、テキストを使用した Web サービスを示す例です。"lightbox="../assets/images/invokebotwithtext.png":::

:::image type="content" source="../assets/images/invokebotwithcard.png" alt-text="スクリーンショットは、対話型カードを使用した Web サービスを示す例です。"lightbox="../assets/images/invokebotwithcard.png"border="true":::

:::image type="content" source="../assets/images/task-module-example.png" alt-text="スクリーンショットは、タスク モジュールを使用する Web サービスを示す例です。" lightbox="../assets/images/task-module-example-expanded.png":::

会話ボットは非常に柔軟です。 ボットは、人工知能と自然言語処理を含むいくつかの基本的なコマンドまたは複雑なタスクを処理できます。 ボットは、大規模なアプリケーションの一部にすることも、スタンドアロンにすることもできます。

カード、テキスト、タスク モジュールの適切な組み合わせを使用して、便利なボットを作成します。 次の図は、テキストカードと対話型カードを使用して、1 対 1 のチャットでボットと会話するユーザーを示しています。

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="スクリーンショットは、サンプルの FAQ ボットを示す例です。":::

ユーザーとボットの間のすべての対話は、アクティビティとして表されます。 ボットは、アクティビティを受け取ると、そのアクティビティ ハンドラーに渡します。 [ボット アクティビティ ハンドラー](~/bots/bot-basics.md)を参照してください。

ボットは、会話インターフェイスを持つアプリです。 テキスト、対話型カード、音声を使用してボットと対話できます。 ボットの動作は、チャネルまたはグループ チャットの会話と 1 対 1 の会話で異なります。 会話は、Bot Framework コネクタを介して処理されます。 [会話の基本](~/bots/how-to/conversations/conversation-basics.md)を参照してください。

ボットには、関連するコンテンツにアクセスし、ボットのエクスペリエンスを向上させるために、ユーザー プロファイルの詳細などのコンテキスト情報が必要です。 [Teams コンテキストを取得](~/bots/how-to/get-teams-context.md)を参照してください。

Graph API または Teams ボット API を使用して、ボットを介してファイルを送受信できます。 ボット[を介してファイルを送受信する方法](~/bots/how-to/bots-filesv4.md)を参照してください。

レート制限は、Teams アプリケーションに使用されるボットを最適化するために使用されます。 Teams とそのユーザーを保護するために、ボット API は受信要求のレート制限を提供します。 [Teamsでレート制限を使用してボットを最適化](~/bots/how-to/rate-limit.md)を参照してください。

通話やオンライン会議用の Microsoft Graph API により、Microsoft Teams アプリは音声とビデオを使用してユーザーと対話できるようになりました。 [通話と会議のボット](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)を参照してください。

Teams ボット API を使用して、チャットまたはチームのメンバーの情報を取得できます。 [チームまたはチャット メンバーをフェッチするための Teams ボット API に対する変更](~/resources/team-chat-member-api-changes.md)を参照してください。

<!--- TBD: For quick scanning, see if the above information can be itemized as a list.
--->

## <a name="code-samples"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| ボットの毎日のタスクリマインダー| 定期的なタスクをスケジュールし、スケジュールされた時刻にリマインダーを受け取る方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |
| Hello World ボット | これは、Bot と Message の両方の拡張機能を備えたシンプルな hello world アプリケーションです。 | 該当なし | [表示](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/hello-world-bot) |
| アダプティブ カード通知 | これは、ボットを使用してさまざまなアダプティブ カードで通知を送信する方法を示すサンプルです。 | 該当なし | [表示](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/adaptive-card-notification) |
| 受信 Webhook 通知 | これは、Microsoft Teams チャネルで受信 Webhook 経由で通知を送信する方法を示すサンプルです。 | 該当なし | [表示](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/incoming-webhook-notification) |

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [ボットと SDK](~/bots/bot-features.md)

## <a name="see-also"></a>関連項目

* [Teams のボットを作成する](../resources/bot-v3/bots-create.md)
* [Microsoft Teams ボットの仕組み](/azure/bot-service/bot-builder-basics-teams)
* [Microsoft Teams の通話と会議ボットを登録する](~/bots/calls-and-meetings/registering-calling-bot.md)
* [Teams ボットに認証を追加する](~/bots/how-to/authentication/add-authentication.md)
* [ボットのアクティビティ ハンドラー](~/bots/bot-basics.md)
* [Teams ボットの会話イベント](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [JavaScript を使用して初めてのボット アプリを構築する](../sbs-gs-bot.yml)
* [JavaScript を使用した通知ボットのビルド](../sbs-gs-notificationbot.yml)
