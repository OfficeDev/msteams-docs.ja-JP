---
title: チームおよびチャット メンバーのボット API の変更
author: ojasvichoudhary
description: チームやチャットのメンバーを取得するために使用される Bot API に対する今後の変更と進行中の変更について説明します。
keywords: ボット フレームワーク api チーム メンバー名簿
localization_priority: Normal
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 333a29664f0d60e89039f906fce77e71054d486f
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555438"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>ボット API の変更をTeamsチームまたはチャットメンバーを取得する

>[!NOTE]
> 廃止プロセスと API `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` が開始されました。 最初は、1 分あたり 5 つの要求に大きく制限され、チームごとに最大 10K メンバーが返されます。 これにより、チームサイズが大きくなると完全な名簿が返されません。
> バージョン 4.10 以降の Bot Framework SDK に更新し、ページ分割された API エンドポイントまたは単一ユーザー API に切り替える必要があります `TeamsInfo.GetMemberAsync` 。 これは、これらの API を直接使用していない場合でも、古い SDK が [メンバーの](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) 追加イベント中にこれらの API を呼び出す場合にも適用されます。 今後の変更のリストを表示するには [、API](team-chat-member-api-changes.md#api-changes)の変更を参照してください。 

現在、チャットまたはチームの 1 人以上のメンバーの情報を取得するボット開発者は、c# または TypeScript API または Node.js API の Microsoft Teams ボット `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` API を使用します。 詳細については、「 [取得名簿またはユーザー プロファイル](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)」を参照してください。 これらの API には、いくつかの欠点があります。

現在、チャットまたはチームの 1 人以上のメンバーの情報を取得する場合は[](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) `TeamsInfo.GetMembersAsync` 、c# または TypeScript または Node.js API の Microsoft Teams ボット API を使用できます `TeamsInfo.getMembers` 。 これらの API には、次の欠点があります。

* 大規模なチームの場合、パフォーマンスが低下し、タイムアウトが発生する可能性が高くなります: 2017 年初めにTeamsがリリースされて以来、最大チーム サイズが大幅に増加しています。 `GetMembersAsync` `getMembers` メンバーリスト全体を返す場合、大きなチームの API 呼び出しが戻ってくるのに時間がかかり、呼び出しがタイムアウトする場合が一般的で、再試行する必要があります。
* 1 人のユーザーのプロファイルの詳細を取得するのは難しい: 1 人のユーザーのプロファイル情報を取得するには、メンバー リスト全体を取得し、目的のユーザーを検索する必要があります。 Bot Framework SDK には、それを簡単にするためのヘルパー関数がありますが、効率的ではありません。

組織全体のチームが導入されると、これらの API をOffice 365プライバシーコントロールと連携させる必要があります。 大規模なチームで使用されるボットは、Microsoft Graph アクセス許可と同様の基本的なプロファイル情報を取得できます `User.ReadBasic.All` 。 テナント管理者は、テナントで使用できるアプリやボットを細かく制御できますが、これらの設定は Microsoft Graphとは異なります。

次のコードは、Teamsボット API によって返される内容の JSON 表現のサンプルを提供します。

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

## <a name="api-changes"></a>API の変更点

今後の API の変更点を次に示します。

* [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)チャットまたはチームのメンバーのプロファイル情報を取得するための新しい API が作成されます。 この API は、ボット フレームワーク バージョン 4.8 以降の SDK で使用できるようになりました。 他のすべてのバージョンでの開発には、 [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) メソッドを使用します。

    > [!NOTE]
    > v3 または v4 では、3.30.2 または 4.8 以降の最新のポイント リリースにそれぞれアップグレードするのが最善の方法です。

* [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details)1 人のユーザーのプロファイル情報を取得するための新しい API が作成されます。 チームまたはチャットの ID、および 、Azure Active Directory オブジェクト ID 、またはTeamsユーザー ID である[UPN](/windows/win32/ad/naming-properties#userprincipalname)をパラメーターとして受け取 `userPrincipalName` `objectId` `id` り、そのユーザーのプロファイル情報を返します。

    > [!NOTE]
    > `objectId` は `aadObjectId` 、Bot Framework メッセージのオブジェクトで呼び出される内容に一致するように変更 `Activity` されます。 新しい API は、ボット フレームワーク SDK のバージョン 4.8 以降で使用できます。 Teams SDK 拡張機能 Bot Framework 3.x でも使用できます。 一方 [、REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) エンドポイントを使用できます。

* `TeamsInfo.GetMembersAsync` で、型スクリプト `TeamsInfo.getMembers` またはNode.jsは正式に廃止されました。 新しい API が利用可能になったら、それを使用するようにボットを更新する必要があります。 これは、 [これらの API が使用する基盤となる REST API](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)にも適用されます。
* 2021 年後半までに、ボットは `userPrincipalName` `email` チャットまたはチームのメンバーの プロパティまたは プロパティを事前に取得できません。 ボットは、Graphを使用して取得する必要があります。 `userPrincipalName`および `email` プロパティは `GetConversationPagedMembers` 、2021 年後半から新しい API から返されません。 ボットは、情報を取得するためにアクセス トークンを使用してGraphを使用する必要があります。 ボットがアクセス トークンを取得し、エンド ユーザーの同意プロセスを簡素化し、簡素化しやすくする必要があります。
