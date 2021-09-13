---
title: Microsoft Teams のボット
author: surbhigupta
description: このページのボットのMicrosoft Teams。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: a5702afcc4e87486d23f363e2e7ec0476f597a71
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156335"
---
# <a name="bots-in-microsoft-teams"></a>Microsoft Teams のボット

チャットボットまたは会話型ボットとも呼ばれるボットは、顧客サービスやサポート スタッフなど、ユーザーが実行する簡単で繰り返し自動化されたタスクを実行するアプリです。 日常的に使用されるボットの例としては、天気に関する情報を提供するボット、夕食の予約、旅行情報の提供などのボットがあります。 ボットの対話は、簡単な質問と回答、またはサービスへのアクセスを提供する複雑な会話です。

> [!IMPORTANT]
> 現在、ボットは Government Community Cloud (GCC) で使用できますが、GCC-High国防総省 (DOD) では使用できません。

> [!VIDEO https://www.youtube-nocookie.com/embed/zSIysk0yL0Q]

会話ボットを使用すると、ユーザーは、テキスト、対話型カード、タスク モジュールで Web サービスとのやり取りができるようになります。

![テキストを使用してボットを呼び出す](~/assets/images/invokebotwithtext.png)

![カードを使用してボットを呼び出す](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

会話型ボットは非常に柔軟性が高く、いくつかの簡単なコマンド、または複雑な人工知能による自然言語処理タスクを処理できます。 大きなアプリケーションの 1 つの側面、または完全にスタンドアロンの場合があります。

便利なボットを作成するには、カード、テキスト、タスク モジュールの適切な組み合わせを見つけることが重要です。 次の図は、テキスト カードと対話型カードの両方を使用して、1 対 1 のチャットでボットと会話するユーザーを示しています。

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="FAQ ボットのサンプル" border="true":::

ユーザーとボットの間のすべての操作は、アクティビティとして表されます。 ボットがアクティビティを受け取った場合、ボットはアクティビティ ハンドラーに渡します。 詳細については、「ボット アクティビティ [ハンドラー」を参照してください](~/bots/bot-basics.md)。 

さらに、ボットは会話型インターフェイスを持つアプリです。 テキスト、対話型カード、音声を使用してボットを操作できます。 ボットの動作は、会話がチャネルまたはグループ チャットの会話か、1 対 1 の会話かによって異なります。 会話はボット フレームワーク コネクタを介して処理されます。 詳細については、「会話の基本 [」を参照してください](~/bots/how-to/conversations/conversation-basics.md)。

ボットには、関連するコンテンツにアクセスしてボットエクスペリエンスを強化するために、ユーザー プロファイルの詳細などのコンテキスト情報が必要です。 詳細については、「get [Teams コンテキスト」を参照してください](~/bots/how-to/get-teams-context.md)。 

また、ボットを介して、API またはボット API を使用Graph受信Teamsできます。 詳細については、「ボットを介 [してファイルを送受信する」を参照してください](~/bots/how-to/bots-filesv4.md)。

さらに、レート制限は、アプリケーションで使用されるボットを最適化Teamsされます。 ボット API はMicrosoft Teamsユーザーを保護するために、受信要求のレート制限を提供します。 詳細については、「アプリのレート[制限を使用](~/bots/how-to/rate-limit.md)してボットを最適化する」を参照Teams。

Microsoft Graph通話やオンライン会議の API を使用すると、Microsoft Teamsアプリは音声とビデオを使用してユーザーとやり取りできます。 詳細については、「通話と [会議ボット」を参照してください](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。 

ボット API Teams使用して、チャットまたはチームの 1 つ以上のメンバーの情報を取得できます。 詳細については、「チームまたはチャット[メンバーをフェッチTeamsボット API に対する変更点」を参照してください](~/resources/team-chat-member-api-changes.md)。

## <a name="see-also"></a>関連項目

[Teams のボットを作成する](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ボットと SDK](~/bots/bot-features.md)
