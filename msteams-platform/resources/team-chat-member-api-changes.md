---
title: チームおよびチャット メンバーのボット API の変更
author: ojasvichoudhary
description: チームとチャットのメンバーを取得するために使用されるボット API に対する今後の変更と進行中の変更について説明します。
keywords: bot framework apis チーム メンバー名簿
localization_priority: Normal
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: ad03d14ca1c38eb810d43027e901e01199858992
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019679"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a><span data-ttu-id="dd68d-104">チームまたはチャット メンバーをフェッチする Teams ボット API の変更</span><span class="sxs-lookup"><span data-stu-id="dd68d-104">Teams bot API changes to fetch team or chat members</span></span>

>[!NOTE]
> <span data-ttu-id="dd68d-105">API および API の `TeamsInfo.getMembers` 廃止 `TeamsInfo.GetMembersAsync` プロセスが開始されました。</span><span class="sxs-lookup"><span data-stu-id="dd68d-105">The deprecation process for `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs have started.</span></span> <span data-ttu-id="dd68d-106">最初は、1 分間に 5 回の要求に大きく調整され、チームごとに最大 10K のメンバーが返されます。</span><span class="sxs-lookup"><span data-stu-id="dd68d-106">Initially, they are heavily throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="dd68d-107">これにより、チームのサイズが大きくなって完全な名簿が返されません。</span><span class="sxs-lookup"><span data-stu-id="dd68d-107">This results in the full roster not being returned as team size increases.</span></span>
> <span data-ttu-id="dd68d-108">Bot Framework SDK のバージョン 4.10 以上に更新し、ページ分割された API エンドポイントまたは単一ユーザー `TeamsInfo.GetMemberAsync` API に切り替える必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd68d-108">You must update to version 4.10 or higher of the Bot Framework SDK and switch to the paginated API endpoints, or the `TeamsInfo.GetMemberAsync` single user API.</span></span> <span data-ttu-id="dd68d-109">これは、古い SDK がメンバーのAdded イベント中にこれらの API を呼び出すので、これらの API を直接使用していない場合でも、ボット [にも適用](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) されます。</span><span class="sxs-lookup"><span data-stu-id="dd68d-109">This also applies to your bot even if you are not directly using these APIs, as older SDKs call these APIs during [membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) events.</span></span> <span data-ttu-id="dd68d-110">今後の変更の一覧を表示するには、「API の変更」 [を参照してください](team-chat-member-api-changes.md#api-changes)。</span><span class="sxs-lookup"><span data-stu-id="dd68d-110">To view the list of upcoming changes, see [API changes](team-chat-member-api-changes.md#api-changes).</span></span> 

<span data-ttu-id="dd68d-111">現在、チャットまたはチームの 1 人または複数のメンバーの情報を取得するボット開発者は、C# または TypeScript または Node.js API の Microsoft Teams ボット `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` API を使用します。</span><span class="sxs-lookup"><span data-stu-id="dd68d-111">Currently, bot developers who want to retrieve information for one or more members of a chat or team use the Microsoft Teams bot APIs `TeamsInfo.GetMembersAsync` for C# or `TeamsInfo.getMembers` for TypeScript or Node.js APIs.</span></span> <span data-ttu-id="dd68d-112">詳細については、「フェッチ名 [簿またはユーザー プロファイル」を参照してください](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)。</span><span class="sxs-lookup"><span data-stu-id="dd68d-112">For more information, see [fetch roster or user profile](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile).</span></span> <span data-ttu-id="dd68d-113">これらの API にはいくつかの欠点があります。</span><span class="sxs-lookup"><span data-stu-id="dd68d-113">These APIs have several shortcomings.</span></span>

<span data-ttu-id="dd68d-114">現在、チャットまたはチームの 1 人または複数のメンバーの情報を取得する場合は [、microsoft Teams](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)ボット API を C# または TypeScript または Node.js `TeamsInfo.GetMembersAsync` API `TeamsInfo.getMembers` に使用できます。</span><span class="sxs-lookup"><span data-stu-id="dd68d-114">Currently, if you want to retrieve information for one or more members of a chat or team, you can use the [Microsoft Teams bot APIs](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) `TeamsInfo.GetMembersAsync` for C# or `TeamsInfo.getMembers` for TypeScript or Node.js APIs.</span></span> <span data-ttu-id="dd68d-115">これらの API には、次のような欠点があります。</span><span class="sxs-lookup"><span data-stu-id="dd68d-115">These APIs have the following shortcomings:</span></span>

* <span data-ttu-id="dd68d-116">大規模なチームの場合、パフォーマンスが低下し、タイムアウトが発生する可能性が高い。 Teams が 2017 年初めにリリースされた後、チームの最大サイズが大幅に大きくなった。</span><span class="sxs-lookup"><span data-stu-id="dd68d-116">For large teams, performance is poor and timeouts are more likely: The maximum team size has grown considerably since Teams was released in early 2017.</span></span> <span data-ttu-id="dd68d-117">メンバー リスト全体を返す場合、API 呼び出しが大規模なチームに戻るのに長い時間がかかるので、呼び出しが一般的にアウトし、もう一度やり直す必要 `GetMembersAsync` `getMembers` があります。</span><span class="sxs-lookup"><span data-stu-id="dd68d-117">As `GetMembersAsync` or `getMembers` returns the entire member list, it takes a long time for the API call to return for large teams, and it is common for the call to time out and you have to try again.</span></span>
* <span data-ttu-id="dd68d-118">1 人のユーザーのプロファイルの詳細を取得するのは困難です。1 人のユーザーのプロファイル情報を取得するには、メンバー リスト全体を取得してから、必要なプロファイルを検索する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd68d-118">Getting profile details for a single user is difficult: To get the profile information for a single user, you have to retrieve the entire member list and then search for the one you want.</span></span> <span data-ttu-id="dd68d-119">ボット フレームワーク SDK には、より簡単なヘルパー関数がありますが、効率的ではありません。</span><span class="sxs-lookup"><span data-stu-id="dd68d-119">There is a helper function in the Bot Framework SDK to make it simpler, but it is not efficient.</span></span>

<span data-ttu-id="dd68d-120">組織全体のチームが導入された場合、これらの API を 365 のプライバシー制御に合わせてOffice必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd68d-120">With the introduction of organization wide teams, there is a requirement to better align these APIs with Office 365 privacy controls.</span></span> <span data-ttu-id="dd68d-121">大規模なチームで使用されるボットは、Microsoft Graph アクセス許可と同様の基本的なプロファイル情報 `User.ReadBasic.All` を取得できます。</span><span class="sxs-lookup"><span data-stu-id="dd68d-121">Bots used in large teams are able to retrieve basic profile information similar to the `User.ReadBasic.All` Microsoft Graph permission.</span></span> <span data-ttu-id="dd68d-122">テナント管理者は、テナントで使用できるアプリとボットを大きな制御を持っていますが、これらの設定は Microsoft Graph とは異なります。</span><span class="sxs-lookup"><span data-stu-id="dd68d-122">Tenant administrators have a great deal of control over which apps and bots can be used in their tenant, but these settings are different from Microsoft Graph.</span></span>

<span data-ttu-id="dd68d-123">次のコードは、Teams ボット API によって返される処理のサンプル JSON 表現を提供します。</span><span class="sxs-lookup"><span data-stu-id="dd68d-123">The following code provides a sample JSON representation of what is returned by Teams bot APIs:</span></span>

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

## <a name="api-changes"></a><span data-ttu-id="dd68d-124">API の変更</span><span class="sxs-lookup"><span data-stu-id="dd68d-124">API Changes</span></span>

<span data-ttu-id="dd68d-125">今後の API の変更点を次に示します。</span><span class="sxs-lookup"><span data-stu-id="dd68d-125">Following are the upcoming API changes:</span></span>

* <span data-ttu-id="dd68d-126">チャットまたはチームのメンバー [`TeamsInfo.GetPagedMembersAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) のプロファイル情報を取得するための新しい API が作成されます。</span><span class="sxs-lookup"><span data-stu-id="dd68d-126">A new API is created [`TeamsInfo.GetPagedMembersAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) for retrieving profile information for members of a chat or team.</span></span> <span data-ttu-id="dd68d-127">この API は、ボット フレームワーク 4.8 SDK で利用できます。</span><span class="sxs-lookup"><span data-stu-id="dd68d-127">This API is now available with the Bot Framework 4.8 SDK.</span></span> <span data-ttu-id="dd68d-128">他のすべてのバージョンでの開発には、メソッドを使用 [`GetConversationPagedMembers`](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) します。</span><span class="sxs-lookup"><span data-stu-id="dd68d-128">For development in all other versions, use the [`GetConversationPagedMembers`](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) method.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dd68d-129">v3 または v4 では、それぞれ 3.30.2 または 4.8 の最新のポイント リリースにアップグレードする方法が最適です。</span><span class="sxs-lookup"><span data-stu-id="dd68d-129">In either v3 or v4, the best action is to upgrade to the latest point release that is 3.30.2 or 4.8 respectively.</span></span>

* <span data-ttu-id="dd68d-130">1 人のユーザーの [`TeamsInfo.GetMemberAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) プロファイル情報を取得するための新しい API が作成されます。</span><span class="sxs-lookup"><span data-stu-id="dd68d-130">A new API is created [`TeamsInfo.GetMemberAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) for retrieving the profile information for a single user.</span></span> <span data-ttu-id="dd68d-131">チームまたはチャットの ID と、パラメーターとして Azure Active Directory オブジェクト ID、または Teams ユーザー ID である [UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) を受け取り、そのユーザーのプロファイル情報 `userPrincipalName` `objectId` `id` を返します。</span><span class="sxs-lookup"><span data-stu-id="dd68d-131">It takes the ID of the team or chat and a [UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) that is `userPrincipalName`, Azure Active Directory Object ID `objectId`, or the Teams user ID `id` as parameters and returns the profile information for that user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dd68d-132">`objectId` は、Bot Framework メッセージのオブジェクトで呼び出されたオブジェクトに一 `aadObjectId` `Activity` 致するに変更されます。</span><span class="sxs-lookup"><span data-stu-id="dd68d-132">`objectId` is changed to `aadObjectId` to match what is called in the `Activity` object of a Bot Framework message.</span></span> <span data-ttu-id="dd68d-133">新しい API は、ボット フレームワーク SDK のバージョン 4.8 で使用できます。</span><span class="sxs-lookup"><span data-stu-id="dd68d-133">The new API is available with version 4.8 of the Bot Framework SDK.</span></span> <span data-ttu-id="dd68d-134">Teams SDK 拡張機能 Bot Framework 3.x でも利用できます。</span><span class="sxs-lookup"><span data-stu-id="dd68d-134">It is also available in the Teams SDK extension Bot Framework 3.x.</span></span> <span data-ttu-id="dd68d-135">一方 [、REST](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) エンドポイントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="dd68d-135">Meanwhile, you can use the [REST](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) endpoint.</span></span>

* <span data-ttu-id="dd68d-136">`TeamsInfo.GetMembersAsync` の `TeamsInfo.getMembers` C#、TypeScript または Node.jsは正式に非推奨です。</span><span class="sxs-lookup"><span data-stu-id="dd68d-136">`TeamsInfo.GetMembersAsync` in C# and `TeamsInfo.getMembers` in TypeScript or Node.js is formally deprecated.</span></span> <span data-ttu-id="dd68d-137">新しい API が利用可能な場合は、ボットを更新して使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd68d-137">Once the new API is available, you must update your bots to use it.</span></span> <span data-ttu-id="dd68d-138">これは、これらの API が使用する [基になる REST API にも適用されます](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)。</span><span class="sxs-lookup"><span data-stu-id="dd68d-138">This also applies to the [underlying REST API that these APIs use](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json).</span></span>
* <span data-ttu-id="dd68d-139">2021 年後半には、ボットはチャットまたはチームのメンバーのプロパティを事前 `userPrincipalName` `email` に取得できません。</span><span class="sxs-lookup"><span data-stu-id="dd68d-139">By late 2021, bots cannot proactively retrieve the `userPrincipalName` or `email` properties for members of a chat or team.</span></span> <span data-ttu-id="dd68d-140">ボットは Graph を使用して取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd68d-140">Bots must use Graph to retrieve them.</span></span> <span data-ttu-id="dd68d-141">プロパティ `userPrincipalName` と `email` プロパティは、2021 年後半から新しい API から `GetConversationPagedMembers` 返されません。</span><span class="sxs-lookup"><span data-stu-id="dd68d-141">The `userPrincipalName` and `email` properties are not returned from the new `GetConversationPagedMembers` API starting in late 2021.</span></span> <span data-ttu-id="dd68d-142">ボットは、情報を取得するためにアクセス トークンで Graph を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd68d-142">Bots have to use Graph with an access token to retrieve information.</span></span> <span data-ttu-id="dd68d-143">ボットがアクセス トークンを取得し、エンド ユーザーの同意プロセスを合理化し、簡素化しやすくする必要があります。</span><span class="sxs-lookup"><span data-stu-id="dd68d-143">It must be made easier for bots to get an access token and streamline and simplify the end-user consent process.</span></span>
