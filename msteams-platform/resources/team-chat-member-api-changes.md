---
title: チームおよびチャット メンバーのボット API の変更
author: ojasvichoudhary
description: チームとチャットのメンバーを取得するために使用されるボット API に対する今後の変更と進行中の変更について説明します。
keywords: bot framework apis チーム メンバー名簿
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: ee90c9c324f11e191cf596bcf8e27cd2bef41240
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596183"
---
# <a name="changes-to-teams-bot-apis-for-fetching-team-and-chat-members"></a>チームメンバーとチャット メンバーをフェッチする Teams ボット API の変更点

>[!NOTE]
> 廃止プロセスと API の使用を `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` 開始しました。 最初は、1 分間に 5 回の要求に大きく調整され、チームごとに最大 10K のメンバーが返されます。 これにより、チーム のサイズが大きくなって完全な名簿が返されません。 
> 
> **Bot Framework SDK のバージョン 4.10** 以上に更新し、ページ分割された API エンドポイントまたは単一ユーザー `TeamsInfo.GetMemberAsync` API に切り替える必要があります。 これは、古い SDK がメンバーの間にこれらの API を呼び出すので、これらの API を直接使用していない場合でも、ボットにも [適用されますAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) イベント。 今後の変更の一覧を表示するには、「API の変更」 [を参照してください](team-chat-member-api-changes.md#api-changes)。 

現在、チャットまたはチームの 1 つ以上のメンバーの情報を取得するボット開発者は、Microsoft Teams ボット API (C# 用) または `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` (TypeScript/Node.js) API [(](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile)ここに記載) を使用しています。 これらの API には、今日いくつかの欠点があります。

* **大規模なチームでは、パフォーマンスが低下し、タイムアウトが発生する可能性が高いです。** Microsoft Teams が 2017 年初めにリリースされた後、チームの最大サイズは大幅に増加しています。 メンバー `GetMembersAsync` / リスト全体を返すので、API 呼び出しが大規模なチームに戻るのに時間がかかるので、呼び出しがタイム アウトし、もう一度やり直す必要があります `getMembers` 。
* **1 人のユーザーのプロファイルの詳細を取得する作業は面倒です。** 1 人のユーザーのプロファイル情報を取得するには、メンバー リスト全体を取得し、必要なユーザーを検索する必要があります。 True、 Bot Framework SDK には、より簡単なヘルパー関数がありますが、カバーの下では効率的ではありません。

これとは別に、組織全体のチームの導入により、これらの API を Office 365 のプライバシー制御に合わせ、大規模なチームで使用されるボットは基本的なプロファイル情報を取得できます。これは Microsoft Graph のアクセス許可に似ています。 `User.ReadBasic.All` テナント管理者は、テナントで使用できるアプリとボットを大きな制御を持っていますが、これらの設定は Microsoft Graph を管理するアプリとは異なります。

今日、これらの API によって返される処理の JSON 表現の例を次に示します。 以下のフィールドの一部を参照します。

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

* チャット/チームのメンバーのプロファイル情報を取得するための新しい [`TeamsInfo.GetPagedMembersAsync`](~/bots/how-to/get-teams-context.md?tabs=dotnet#fetching-the-roster-or-user-profile) API が作成されました。 この API は、ボット フレームワーク 4.10 SDK で利用できます。 他のすべてのバージョンでの開発では、このメソッドを使用 [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) します。
  > [!NOTE]
  > v3 または v4 では、ベスト アクションは、最新のポイント リリースにアップグレードする方法です。
* 1 人のユーザーのプロファイル情報を取得するための新しい API [`TeamsInfo.GetMemberAsync`](~/bots/how-to/get-teams-context.md?tabs=dotnet#get-single-member-details) が作成されました。 チーム/チャットの ID と[UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) (上記を参照 `userPrincipalName` )、Azure Active Directory オブジェクト ID (、上記参照)、または Teams ユーザー ID (上記を参照 `objectId`  `id` )をパラメーターとして受け取り、そのユーザーのプロファイル情報を返します。
  > [!NOTE]
  > ボット フレームワーク メッセージのオブジェクトで呼び出された名前に合 `objectId` `aadObjectId` `Activity` わせて変更しています。 新しい API は、ボット フレームワーク SDK のバージョン 4.10 で使用できます。 Teams SDK 拡張機能 Bot Framework 3.x でもすぐに利用できます。一方 [、REST](~/bots/how-to/get-teams-context.md?tabs=json#get-single-member-details) エンドポイントを使用できます。
* `TeamsInfo.GetMembersAsync` (C#) および `TeamsInfo.getMembers` (TypeScript/Node.js) は正式に廃止され、2021 年後半に動作を停止します。 ページ API を使用するボットを更新してください。 (これは、これらの API が使用する [基になる REST API にも適用されます](~/bots/how-to/get-teams-context.md?tabs=json)。)
* 2021 年後半には、ボットはチャット/チームのメンバーのプロパティを事前に取得する機能を使用し、Microsoft Graph を使用して取得する `userPrincipalName` `email` 必要があります。 具体的には、 `userPrincipalName` プロパティ `email` は 2021 年後半から新しい API から `GetConversationPagedMembers` 返されません。 ボットは、この情報を取得するためにアクセス トークンと Microsoft Graph を使用する必要があります。 これは明らかに大きな変更です。ボットがアクセス トークンを取得しやすくする必要があります。また、エンドユーザーの同意プロセスを合理化して簡素化する必要があります。

## <a name="feedback-and-more-information"></a>フィードバックと詳細

これらの変更に関する最新の情報を提供するために、このページを使用します。 ご質問がある場合は、以下の 「フィードバック」セクション>「このページでフィードバックを送信 **する」を** 使用してください。
