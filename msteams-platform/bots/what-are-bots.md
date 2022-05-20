---
title: Microsoft Teams のボット
author: surbhigupta
description: Microsoft Teams のボットの概要。
ms.topic: overview
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 81fa44730a26f3d7bcafdc9f37ec15b4eb7b1951
ms.sourcegitcommit: aa95313cdab4fbf0a9f62a047ebbe6a5f1fbbf5d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2022
ms.locfileid: "65602293"
---
# <a name="bots-in-microsoft-teams"></a>Microsoft Teams のボット

ボットは、チャットボットまたは会話ボットとも呼ばれます。 これは、カスタマー サービスやサポート スタッフなどのユーザーが単純で反復的なタスクを実行するアプリです。 ボットの日常的な使用には、天気に関する情報を提供するボット、ディナーの予約を行うボット、旅行情報を提供するボットなどがあります。 ボットとのやり取りは、質問や回答を素早く行ったり、複雑な会話になったりする場合があります。

> [!IMPORTANT]
> 現在、ボットは Government Community Cloud (GCC) と GCC-High で利用できますが、国防総省 (DOD) では利用できません。
> 
> Microsoft Teams 内のボット アプリケーションは、 [Azure Bot Service](/azure/bot-service/channel-connect-teams) を介して GCC-High で利用できます。

会話ボットを使用すると、ユーザーはテキスト、対話型カード、タスク モジュールを使用して Web サービスと対話できます。

:::image type="content" source="../assets/images/invokebotwithtext.png" alt-text="テキストを使用した Web サービス"lightbox="../assets/images/invokebotwithtext.png":::

:::image type="content" source="../assets/images/invokebotwithcard.png" alt-text="対話型カードを使用した Web サービス"lightbox="../assets/images/invokebotwithcard.png"border="true":::

:::image type="content" source="../assets/images/task-module-example.png" alt-text="タスク モジュールを使用した Web サービス"lightbox="../assets/images/task-module-example.png"border="true":::

会話ボットは非常に柔軟です。 ボットは、人工知能と自然言語処理を含むいくつかの基本的なコマンドまたは複雑なタスクを処理できます。 ボットは、大規模なアプリケーションの一部にすることも、スタンドアロンにすることもできます。

カード、テキスト、タスク モジュールの適切な組み合わせを使用して、便利なボットを作成します。 次の図は、テキストカードと対話型カードを使用して、1 対 1 のチャットでボットと会話するユーザーを示しています。

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="サンプル FAQ ボット" border="true":::

ユーザーとボットの間のすべての対話は、アクティビティとして表されます。 ボットは、アクティビティを受け取ると、そのアクティビティ ハンドラーに渡します。 [ボット アクティビティ ハンドラー](~/bots/bot-basics.md)を参照してください。

ボットは、会話インターフェイスを持つアプリです。 テキスト、対話型カード、音声を使用してボットと対話できます。 ボットの動作は、チャネルまたはグループ チャットの会話と 1 対 1 の会話で異なります。 会話は、Bot Framework コネクタを介して処理されます。 [会話の基本](~/bots/how-to/conversations/conversation-basics.md)を参照してください。

ボットには、関連するコンテンツにアクセスし、ボットのエクスペリエンスを向上させるために、ユーザー プロファイルの詳細などのコンテキスト情報が必要です。「[Teams コンテキストを取得](~/bots/how-to/get-teams-context.md)」を参照してください。

Graph API または Teams ボット API を使用して、ボットを介してファイルを送受信できます。 ボット[を介してファイルを送受信する方法](~/bots/how-to/bots-filesv4.md)を参照してください。

レート制限は、Teams アプリケーションに使用されるボットを最適化するために使用されます。 Microsoft Teams とそのユーザーを保護するために、ボット API は受信要求のレート制限を提供します。 [Teamsでレート制限を使用してボットを最適化](~/bots/how-to/rate-limit.md)を参照してください。

通話やオンライン会議用のMicrosoft Graph API により、Microsoft Teams アプリで音声とビデオを使用してユーザーと対話できるようになりました。「[通話と会議のボット](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)」を参照してください。

Teams ボット API を使用して、チャットまたはチームのメンバーの情報を取得できます。 [チームまたはチャット メンバーをフェッチするための Teams ボット API に対する変更](~/resources/team-chat-member-api-changes.md)を参照してください。

<!--- TBD: For quick scanning, see if the above information can be itemized as a list.
--->

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [ボットと SDK](~/bots/bot-features.md)

## <a name="code-samples"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| ボットの毎日のタスクリマインダー| 定期的なタスクをスケジュールし、スケジュールされた時刻にリマインダーを受け取る方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |

## <a name="see-also"></a>関連項目

* [Teams のボットを作成する](../resources/bot-v3/bots-create.md)
* [Microsoft Teams ボットの仕組み](/azure/bot-service/bot-builder-basics-teams)
* [Microsoft Teams の通話と会議ボットを登録する](~/bots/calls-and-meetings/registering-calling-bot.md)
* [Teams ボットに認証を追加する](~/bots/how-to/authentication/add-authentication.md)
* [ボットのアクティビティ ハンドラー](~/bots/bot-basics.md)
* [Teams ボットの会話イベント](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
