---
title: チームおよびチャット メンバーのボット API の変更
author: ojasvichoudhary
description: このモジュールでは、チームとチャットのメンバーを取得するために使用される Bot API に対する今後の変更と進行中の変更について説明します
ms.localizationpriority: medium
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 8160f59f1bb08cf205d057fa6c1e5df7a4e61240
ms.sourcegitcommit: 0e4fcbc5efff4bfa1dbfba1e5467bbfaa6638705
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2022
ms.locfileid: "68773486"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>チームまたはチャット メンバーをフェッチするための Teams ボット API の変更

>[!NOTE]
> API と `TeamsInfo.GetMembersAsync` API の`TeamsInfo.getMembers`非推奨プロセスが開始されました。 最初は、1 分あたり 5 つの要求に大幅に調整され、チームごとに最大 10,000 人のメンバーが返されます。 これにより、チーム サイズが大きくなると、完全な名簿が返されません。
> Bot Framework SDK のバージョン 4.10 以降に更新し、ページ分割された API エンドポイントまたはシングル ユーザー API に `TeamsInfo.GetMemberAsync` 切り替える必要があります。 これは、古い SDK が [メンバーの追加](../bots/how-to/conversations/subscribe-to-conversation-events.md#members-added) イベント中にこれらの API を呼び出すので、これらの API を直接使用していない場合でもボットにも適用されます。 今後の変更の一覧を表示するには、「 [API の変更](team-chat-member-api-changes.md#api-changes)」を参照してください。

現在、チャットまたはチームの 1 人以上のメンバーの情報を取得する場合は、C# 用または TypeScript API `TeamsInfo.GetMembersAsync` または `TeamsInfo.getMembers` Node.js API 用[の Microsoft Teams ボット](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) API を使用できます。 詳細については、「 [名簿またはユーザー プロファイルをフェッチ](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)する」を参照してください。

これらの API には、次の欠点があります。

* 大規模なチームの場合、パフォーマンスが低下し、タイムアウトが発生する可能性が高くなります。Teams が 2017 年初めにリリースされて以来、チームの最大サイズはかなり大きくなりました。 `GetMembersAsync`メンバー リスト全体を返す場合、`getMembers`大規模なチームに対して API 呼び出しが返されるまでに長い時間がかかり、呼び出しがタイムアウトになるのは一般的であり、もう一度やり直す必要があります。
* 1 人のユーザーのプロファイルの詳細を取得するのは困難です。1 人のユーザーのプロファイル情報を取得するには、メンバー リスト全体を取得し、目的のユーザーを検索する必要があります。 Bot Framework SDK には、よりシンプルにするためにヘルパー関数がありますが、効率的ではありません。

組織全体のチームの導入により、これらの API をOffice 365プライバシー制御とより適切に連携させる必要があります。 大規模なチームで使用されるボットは、Microsoft Graph のアクセス許可と同様の基本的なプロファイル情報を `User.ReadBasic.All` 取得できます。 テナント管理者は、テナントで使用できるアプリとボットを十分に制御できますが、これらの設定は Microsoft Graph とは異なります。

次のコードは、Teams ボット API によって返される内容のサンプル JSON 表現を提供します。

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

* チャットまたはチームのメンバーのプロファイル情報を取得するための新しい API が作成 [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) されます。 この API は、Bot Framework バージョン 4.8 以降の SDK で使用できるようになりました。 その他のすべてのバージョンで開発する場合は、 メソッドを使用します [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) 。

    > [!NOTE]
    > v3 または v4 では、それぞれ 3.30.2 または 4.8 以降の最新のポイント リリースにアップグレードすることをお勧めします。

* 1 人のユーザーのプロファイル情報を取得するための新しい API が作成 [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) されます。 チームまたはチャットの ID と[、](/windows/win32/ad/naming-properties#userprincipalname)`userPrincipalName`Microsoft Azure Active Directory (Azure AD) オブジェクト ID、または Teams ユーザー ID `objectId``id` をパラメーターとして取得し、そのユーザーのプロファイル情報を返します。

    > [!NOTE]
    > `objectId` が に `aadObjectId` 変更され、Bot Framework メッセージの `Activity` オブジェクトで呼び出される内容と一致します。 新しい API は、Bot Framework SDK のバージョン 4.8 以降で使用できます。 Teams SDK 拡張機能 Bot Framework 3.x でも使用できます。 一方、 [REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) エンドポイントを使用できます。

* `TeamsInfo.GetMembersAsync` C# と `TeamsInfo.getMembers` TypeScript または Node.js では正式に非推奨です。 新しい API が使用可能になったら、それを使用するようにボットを更新する必要があります。 これは、 [これらの API が使用する基になる REST API にも](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)適用されます。
* 2022 年後半までに、ボットはチャットまたはチームのメンバーの または `email` プロパティを事前に取得`userPrincipalName`できません。 ボットは、Graph API を使用して必要な情報を取得する必要があります。 新しい `GetConversationPagedMembers` API は、 プロパティと `email` プロパティを `userPrincipalName` 2022 年後半から返すことはできません。

    > [!NOTE]
    > [Graph API](/graph/api/user-get?view=graph-rest-1.0&tabs=http&preserve-view=true#examples)とアクセス トークンを使用して情報を取得することをお勧めします。
