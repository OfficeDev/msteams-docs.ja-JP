---
title: チームおよびチャット メンバーのボット API の変更
author: ojasvichoudhary
description: チームとチャットのメンバーを取得するために使用されるボット API に対する今後の変更と進行中の変更について説明します。
keywords: bot framework apis チーム メンバー名簿
localization_priority: Normal
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: d2eb75a69100a6daaf3af3a021b9896c42abe5f1
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114246"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Teamsまたはチャット メンバーをフェッチするボット API の変更を確認する

>[!NOTE]
> API および API の `TeamsInfo.getMembers` 廃止 `TeamsInfo.GetMembersAsync` プロセスが開始されました。 最初は、1 分間に 5 回の要求に大きく調整され、チームごとに最大 10K のメンバーが返されます。 これにより、チームのサイズが大きくなって完全な名簿が返されません。
> Bot Framework SDK のバージョン 4.10 以上に更新し、ページ分割された API エンドポイントまたは単一ユーザー `TeamsInfo.GetMemberAsync` API に切り替える必要があります。 これは、古い SDK がメンバーのAdded イベント中にこれらの API を呼び出すので、これらの API を直接使用していない場合でも、ボット [にも適用](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) されます。 今後の変更の一覧を表示するには、「API の変更」 [を参照してください](team-chat-member-api-changes.md#api-changes)。 

現在、チャットまたはチームの 1 人または複数のメンバーの情報を取得するボット開発者は、C# または TypeScript または Node.js API の Microsoft Teams ボット `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` API を使用します。 詳細については、「フェッチ名 [簿またはユーザー プロファイル」を参照してください](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)。 これらの API にはいくつかの欠点があります。

現在、チャットまたはチームの 1 人または複数のメンバーの情報を取得する場合は[、C#](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)または TypeScript または Node.js API の Microsoft Teams ボット `TeamsInfo.GetMembersAsync` API `TeamsInfo.getMembers` を使用できます。 これらの API には、次のような欠点があります。

* 大規模なチームの場合、パフォーマンスが低下し、タイムアウトが発生する可能性が高く、2017 年初めにリリースされたチームの最大Teams大きくなった。 メンバー リスト全体を返す場合、API 呼び出しが大規模なチームに戻るのに長い時間がかかるので、呼び出しが一般的にアウトし、もう一度やり直す必要 `GetMembersAsync` `getMembers` があります。
* 1 人のユーザーのプロファイルの詳細を取得するのは困難です。1 人のユーザーのプロファイル情報を取得するには、メンバー リスト全体を取得してから、必要なプロファイルを検索する必要があります。 ボット フレームワーク SDK には、より簡単なヘルパー関数がありますが、効率的ではありません。

組織全体のチームが導入された場合、これらの API をプライバシー管理に合わせてOffice 365があります。 大規模なチームで使用されるボットは、Microsoft のアクセス許可と同様の基本的な `User.ReadBasic.All` プロファイル情報Graphできます。 テナント管理者は、テナントで使用できるアプリとボットを大きな制御を持っていますが、これらの設定は Microsoft と異Graph。

次のコードは、ボット API によって返される処理の JSON 表現Teams示しています。

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

今後の API の変更点を次に示します。

* チャットまたはチームのメンバー [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) のプロファイル情報を取得するための新しい API が作成されます。 この API は、ボット フレームワーク バージョン 4.8 以降の SDK で利用できます。 他のすべてのバージョンでの開発には、メソッドを使用 [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) します。

    > [!NOTE]
    > v3 または v4 では、それぞれ 3.30.2 または 4.8 以降の最新のポイント リリースにアップグレードする方法が最適です。

* 1 人のユーザーの [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) プロファイル情報を取得するための新しい API が作成されます。 チームまたはチャットの ID と[](/windows/win32/ad/naming-properties#userprincipalname) `userPrincipalName` 、Azure Active Directory オブジェクト ID、または Teams ユーザー ID をパラメーターとして取得し、そのユーザーのプロファイル情報を返します `objectId` `id` 。

    > [!NOTE]
    > `objectId` は、Bot Framework メッセージのオブジェクトで呼び出されたオブジェクトに一 `aadObjectId` `Activity` 致するに変更されます。 新しい API は、Bot Framework SDK のバージョン 4.8 以降で使用できます。 また、SDK 拡張機能 Bot Framework 3.x Teamsで使用することもできます。 一方 [、REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) エンドポイントを使用できます。

* `TeamsInfo.GetMembersAsync` の `TeamsInfo.getMembers` C#、TypeScript または Node.jsは正式に非推奨です。 新しい API が利用可能な場合は、ボットを更新して使用する必要があります。 これは、これらの API が使用する [基になる REST API にも適用されます](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)。
* 2022 年後半には、ボットはチャットまたはチームのメンバーのプロパティを事前 `userPrincipalName` `email` に取得できません。 ボットは、ボットを取得Graphを使用する必要があります。 プロパティ `userPrincipalName` と `email` プロパティは、2022 年後半から新しい API から `GetConversationPagedMembers` 返されません。 ボットは、アクセス トークンGraphを使用して情報を取得する必要があります。 ボットがアクセス トークンを取得し、エンド ユーザーの同意プロセスを合理化し、簡素化しやすくする必要があります。
