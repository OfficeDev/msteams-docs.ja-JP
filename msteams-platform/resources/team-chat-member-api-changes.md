---
title: チーム/チャットメンバーの Bot API の変更 (2020 更新)
author: ojasvichoudhary
description: Teams およびチャットのメンバーを取得するために使用される Bot Api に関する今後の変更点と進行中の変更点について説明します。
keywords: bot フレームワーク api チームメンバー名簿
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 926e4e39e4b5c3f1ba34a4458cf6f17612d86841
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2020
ms.locfileid: "44801292"
---
# <a name="changes-to-teams-bot-apis-for-fetching-teamchat-members"></a>チーム/チャットメンバーを取得するための Teams Bot Api に対する変更

現時点では、チャットまたはチームの1人または複数のメンバーの情報を取得することを希望する bot 開発者は、Microsoft Teams bot Api `TeamsInfo.GetMembersAsync` (C#) または `TeamsInfo.getMembers` (TypeScript/Node.js) api を使用します[(ここでは説明](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetching-the-roster-or-user-profile)しています)。 これらの Api には、現在いくつかの欠点があります。

* **大規模なチームでは、パフォーマンスが低下し、タイムアウトが発生する可能性が高くなります。** Microsoft Teams が2017初頭にリリースされて以来、チームの最大サイズは大幅に増加しました。 `GetMembersAsync` / `getMembers` メンバー一覧全体が返されるため、API 呼び出しが大規模なチームを返すのに長い時間がかかり、その呼び出しがタイムアウトになり、もう一度やり直す必要があります。
* **単一ユーザーのプロファイルの詳細を取得するのは煩雑です。** 単一のユーザーのプロファイル情報を取得するには、メンバーリスト全体を取得して、必要なものを検索する必要があります。 True の場合、ボット Framework SDK にはヘルパー関数がありますが、これを簡素化することができますが、それについては効率的ではありません。

個別に、組織全体のチームの導入によって、これらの Api を Office 365 のプライバシー制御に合わせた方がよいことがわかりました。大規模なチームで使用されている bot は、 `User.ReadBasic.All` Microsoft Graph のアクセス許可に似た基本的なプロファイル情報を取得することができます。 テナント管理者は、テナントで使用できるアプリとボットを多く制御できますが、これらの設定は Microsoft Graph を管理するものとは異なります。

ここでは、これらの Api によって返されるものの JSON 表記の例を示します。 ここでは、以下のフィールドについて説明します。

```json
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com"
}]
```

## <a name="api-changes"></a>API の変更点
今後の API の変更点は次のとおりです。

* [`TeamsInfo.GetPagedMembersAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetching-the-roster-or-user-profile)チャット/チームのメンバーのプロファイル情報を取得するための新しい API を作成しました。 この API は、ボット Framework 4.8 SDK で利用できるようになりました。 他のすべてのバージョンでの開発では、メソッドを使用し [`GetConversationPagedMembers`](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable) ます。 **注**: v3 または v4 のいずれかで、最新のポイントリリース (3.30.2 または4.8 それぞれ) にアップグレードすることをお勧めします。 
* [`TeamsInfo.GetMemberAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details)1 人のユーザーのプロファイル情報を取得するための新しい API を作成しました。 このメソッドは、チーム/チャットの ID と[UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) ( `userPrincipalName` 、*上記参照*)、Azure Active Directory オブジェクト id (、上記参照) `objectId` 、Teams ユーザー ID ( *see above* `id` 、*上記参照*) をパラメーターとして受け取り、そのユーザーのプロファイル情報を返します。 **注**: `objectId` `aadObjectId` `Activity` Bot フレームワークメッセージのオブジェクトで呼び出される内容と一致するようにに変更しています。 新しい API は、Bot Framework SDK のバージョン4.8 で利用できます。 まもなく、Teams SDK 拡張ボットフレームワーク 3. x で利用できるようになります。一方、 [REST](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details)エンドポイントを使用することもできます。
* `TeamsInfo.GetMembersAsync`(C#) と `TeamsInfo.getMembers` (TypeScript/Node.js) は正式に廃止され、2021後期に動作しなくなります。 開発者からのフィードバックに基づき、2020年5月に特定のタイムテーブルをアナウンスします。 新しいページ API が利用できるようになったら、開発者はそれらを使用するように bot を更新する必要があります。 (これは、これらの[api が使用する基礎となる REST API](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)にも適用されます)。
* 2021後期には、bot は `userPrincipalName` `email` チャット/チームのメンバーのまたはプロパティを積極的に取得できず、Microsoft Graph を使用してそれらを取得する必要があります。 具体的には、 `userPrincipalName` `email` 2021 の後期以降に新しい API からプロパティが返されることはありません `GetConversationPagedMembers` 。 Bot は、この情報を取得するために Microsoft Graph をアクセストークンと共に使用する必要があります。 これは明らかに大きな変更です。これは、ボットがアクセストークンを取得しやすくなるようにする必要があります。また、エンドユーザーの同意プロセスを簡素化し、簡素化する必要があります。

## <a name="feedback-and-more-information"></a>フィードバックと詳細情報
このページを使用して、これらの変更に関する最新情報を提供します。 ご質問がある場合は、下の**フィードバック**セクションの「フィードバック > をこのページに送信する」をご利用ください。 
