---
title: Microsoft Teams のボット
author: surbhigupta
description: このページのボットのMicrosoft Teams。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: a9f53654ba3240b973b77c05cd64a22c80237350
ms.sourcegitcommit: a6c39106ccc002d02a65e11627659e0c48981d8a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2022
ms.locfileid: "62014564"
---
# <a name="bots-in-microsoft-teams"></a>Microsoft Teams のボット

ボットは、チャットボットまたは会話型ボットとも呼ばれます。 顧客サービスやサポート スタッフなどのユーザーによる単純で繰り返しのタスクを実行するアプリです。 ボットの日常的な使用には、天気に関する情報を提供するボット、夕食の予約、旅行情報の提供を行うボットが含まれます。 ボットとのやり取りは、質問と回答を迅速に行う場合や、複雑な会話になる場合があります。

> [!IMPORTANT]
> 現在、ボットは Government Community Cloud (GCC) で利用できます。GCC-High国防総省 (DOD) では利用できません。

会話型ボットを使用すると、ユーザーはテキスト、対話型カード、タスク モジュールを使用して Web サービスを操作できます。

![テキストを使用してボットを呼び出す](~/assets/images/invokebotwithtext.png)

![カードを使用してボットを呼び出す](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

会話ボットは非常に柔軟です。 ボットは、人工知能と自然言語処理を含むいくつかの基本的なコマンドや複雑なタスクを処理できます。 ボットは、より大きなアプリケーションの一部にしたり、スタンドアロンにしたりできます。

カード、テキスト、タスク モジュールを適切に組み合わせ、便利なボットを作成します。 次の図は、テキスト カードと対話型カードを使用して 1 対 1 のチャットでボットと会話するユーザーを示しています。

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="FAQ ボットのサンプル" border="true":::

ユーザーとボットの間のすべての操作は、アクティビティとして表されます。 ボットがアクティビティを受け取った場合、ボットはアクティビティ ハンドラーに渡します。 「 [ボット アクティビティ ハンドラー」を参照してください](~/bots/bot-basics.md)。

ボットは、会話型インターフェイスを持つアプリです。 テキスト、対話型カード、音声を使用してボットを操作できます。 ボットの動作は、チャネルまたはグループ チャットの会話と 1 対 1 の会話で異なります。 会話はボット フレームワーク コネクタを介して処理されます。 「会話 [の基本」を参照してください](~/bots/how-to/conversations/conversation-basics.md)。

ボットには、関連するコンテンツにアクセスしてボットエクスペリエンスを強化するために、ユーザー プロファイルの詳細などのコンテキスト情報が必要です。 「get [Teams コンテキスト」を参照してください](~/bots/how-to/get-teams-context.md)。

ボットを介してファイルを送受信するには、api または Graphボット API をTeams使用します。 「ボット [を介したファイルの送受信」を参照してください](~/bots/how-to/bots-filesv4.md)。

レート制限は、アプリケーションで使用されるボットを最適化Teamsされます。 ボット API はMicrosoft Teamsユーザーを保護するために、受信要求のレート制限を提供します。 「[アプリのレート制限を使用してボットを最適化する」をTeams。](~/bots/how-to/rate-limit.md)

Microsoft Graph通話やオンライン会議の API を使用すると、Microsoft Teamsアプリは音声とビデオを使用してユーザーとやり取りできます。 「通話 [と会議のボット」を参照してください](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。

ボット API を使用Teams、チャットまたはチームのメンバーの情報を取得できます。 チーム[またはチャット メンバーをフェッチTeamsボット API の変更点を参照してください](~/resources/team-chat-member-api-changes.md)。

<!--- TBD: For quick scanning, see if the above information can be itemized as a list.
--->

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [ボットと SDK](~/bots/bot-features.md)

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| ボットの毎日のタスクリマインダー| 定期的なタスクをスケジュールし、スケジュールされた時刻にリマインダーを取得する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |

## <a name="see-also"></a>関連項目

* [Teams のボットを作成する](~/bots/how-to/create-a-bot-for-teams.md)
* [会議の通話と会議ボットを登録Microsoft Teams](~/bots/calls-and-meetings/registering-calling-bot.md)
* [認証をボットにTeamsする](~/bots/how-to/authentication/add-authentication.md)
* [ボットのアクティビティ ハンドラー](~/bots/bot-basics.md)
* [Teams ボットの会話イベント](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
