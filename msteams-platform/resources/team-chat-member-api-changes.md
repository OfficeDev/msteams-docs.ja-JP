---
title: チームおよびチャット メンバーのボット API の変更
author: ojasvichoudhary
description: チームとチャットのメンバーを取得するために使用される Bot API の今後および進行中の変更について説明します
keywords: bot Framework APIs チーム メンバー名簿
ms.localizationpriority: medium
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: dfa85832fe8225b58e4566ba889c23d2696807e4
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2022
ms.locfileid: "64737204"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>チームまたはチャット メンバーをフェッチするためのボット API の変更をTeamsする

>[!NOTE]
> API と API の`TeamsInfo.getMembers``TeamsInfo.GetMembersAsync`非推奨プロセスが開始されました。 最初は、1 分間に 5 つの要求に大きく調整され、チームあたり最大 10,000 人のメンバーが返されます。 これにより、チーム のサイズが大きくなると、完全な名簿は返されません。
> バージョン 4.10 以降の Bot Framework SDK に更新し、ページ分割された API エンドポイントまたは `TeamsInfo.GetMemberAsync` 単一ユーザー API に切り替える必要があります。 これは、古い SDK が [membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) イベント中にこれらの API を呼び出すので、これらの API を直接使用していない場合でも、ボットにも適用されます。 今後の変更の一覧を表示するには、「 [API の変更](team-chat-member-api-changes.md#api-changes)」を参照してください。

現在、チャットまたはチームの 1 人以上のメンバーの情報を取得する場合は、C# または TypeScript または `TeamsInfo.getMembers` [Node.js API のMicrosoft Teams ボット API を](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)`TeamsInfo.GetMembersAsync`使用できます。 詳細については、 [フェッチ名簿またはユーザー プロファイル](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)に関するトピックを参照してください。

これらの API には、次の欠点があります。

* 大規模なチームでは、パフォーマンスが低下し、タイムアウトが発生する可能性が高くなります。Teamsが 2017 年初頭にリリースされて以降、最大チーム サイズは大幅に増加しています。 `GetMembersAsync`メンバー リスト全体を返すか`getMembers`、API 呼び出しが大規模なチームに戻るまでに時間がかかり、呼び出しがタイムアウトし、もう一度やり直す必要があるのが一般的です。
* 1 人のユーザーのプロファイルの詳細を取得するのは困難です。1 人のユーザーのプロファイル情報を取得するには、メンバー リスト全体を取得し、目的のユーザーを検索する必要があります。 Bot Framework SDK には、よりシンプルにするためのヘルパー関数がありますが、効率的ではありません。

組織全体のチームの導入により、これらの API をOffice 365プライバシー制御とより適切に連携させる必要があります。 大規模なチームで使用されるボットは、Microsoft Graphアクセス許可に似た基本的なプロファイル情報を`User.ReadBasic.All`取得できます。 テナント管理者は、テナントで使用できるアプリとボットを大きく制御できますが、これらの設定は Microsoft Graphとは異なります。

次のコードは、Teams ボット API によって返される内容の JSON 表現のサンプルを提供します。

```json
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "Anon1 (Guest)",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
 "userRole": "anonymous"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
 "userRole": "user"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
 "userRole": "user"
}]
```

## <a name="api-changes"></a>API の変更

今後の API の変更を次に示します。

* チャットまたはチームのメンバーのプロファイル情報を取得するための新しい API が作成 [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) されます。 この API は、Bot Framework バージョン 4.8 以降の SDK で使用できるようになりました。 他のすべてのバージョンで開発する場合は、このメソッドを使用します [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) 。

    > [!NOTE]
    > v3 または v4 では、それぞれ 3.30.2 または 4.8 以降の最新のポイント リリースにアップグレードすることをお勧めします。

* 1 人のユーザーのプロファイル情報を取得するための新しい API が作成 [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) されます。 チームまたはチャットの ID と [UPN](/windows/win32/ad/naming-properties#userprincipalname) `userPrincipalName`(Microsoft Azure Active Directory (Azure AD) オブジェクト ID`objectId`、またはTeamsユーザー ID を`id`パラメーターとして受け取り、そのユーザーのプロファイル情報を返します。

    > [!NOTE]
    > `objectId`は、Bot Framework メッセージのオブジェクトで呼び出されたものと`Activity`一致するように`aadObjectId`変更されます。 新しい API は、Bot Framework SDK のバージョン 4.8 以降で使用できます。 また、Teams SDK 拡張機能 Bot Framework 3.x でも使用できます。 一方、 [REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) エンドポイントを使用できます。

* `TeamsInfo.GetMembersAsync` C# および `TeamsInfo.getMembers` TypeScript またはNode.jsでは正式に非推奨です。 新しい API が使用可能になったら、ボットを更新して使用する必要があります。 これは、 [これらの API が使用する基になる REST API](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json) にも適用されます。
* 2022 年後半までに、ボットはチャットまたはチームのメンバーのプロパティを`email`事前に取得`userPrincipalName`できません。 ボットは、Graph API を使用して、必要な情報を取得する必要があります。 新しい `GetConversationPagedMembers` API では、2022 年後半からプロパティと`email`プロパティを返`userPrincipalName`すことはできません。 ボットは、アクセス トークンと共にGraph APIを使用して情報を取得する必要があります。 
