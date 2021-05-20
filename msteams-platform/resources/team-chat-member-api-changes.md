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
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a><span data-ttu-id="1179c-104">ボット API の変更をTeamsチームまたはチャットメンバーを取得する</span><span class="sxs-lookup"><span data-stu-id="1179c-104">Teams bot API changes to fetch team or chat members</span></span>

>[!NOTE]
> <span data-ttu-id="1179c-105">廃止プロセスと API `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` が開始されました。</span><span class="sxs-lookup"><span data-stu-id="1179c-105">The deprecation process for `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs have started.</span></span> <span data-ttu-id="1179c-106">最初は、1 分あたり 5 つの要求に大きく制限され、チームごとに最大 10K メンバーが返されます。</span><span class="sxs-lookup"><span data-stu-id="1179c-106">Initially, they are heavily throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="1179c-107">これにより、チームサイズが大きくなると完全な名簿が返されません。</span><span class="sxs-lookup"><span data-stu-id="1179c-107">This results in the full roster not being returned as team size increases.</span></span>
> <span data-ttu-id="1179c-108">バージョン 4.10 以降の Bot Framework SDK に更新し、ページ分割された API エンドポイントまたは単一ユーザー API に切り替える必要があります `TeamsInfo.GetMemberAsync` 。</span><span class="sxs-lookup"><span data-stu-id="1179c-108">You must update to version 4.10 or higher of the Bot Framework SDK and switch to the paginated API endpoints, or the `TeamsInfo.GetMemberAsync` single user API.</span></span> <span data-ttu-id="1179c-109">これは、これらの API を直接使用していない場合でも、古い SDK が [メンバーの](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) 追加イベント中にこれらの API を呼び出す場合にも適用されます。</span><span class="sxs-lookup"><span data-stu-id="1179c-109">This also applies to your bot even if you are not directly using these APIs, as older SDKs call these APIs during [membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) events.</span></span> <span data-ttu-id="1179c-110">今後の変更のリストを表示するには [、API](team-chat-member-api-changes.md#api-changes)の変更を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1179c-110">To view the list of upcoming changes, see [API changes](team-chat-member-api-changes.md#api-changes).</span></span> 

<span data-ttu-id="1179c-111">現在、チャットまたはチームの 1 人以上のメンバーの情報を取得するボット開発者は、c# または TypeScript API または Node.js API の Microsoft Teams ボット `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` API を使用します。</span><span class="sxs-lookup"><span data-stu-id="1179c-111">Currently, bot developers who want to retrieve information for one or more members of a chat or team use the Microsoft Teams bot APIs `TeamsInfo.GetMembersAsync` for C# or `TeamsInfo.getMembers` for TypeScript or Node.js APIs.</span></span> <span data-ttu-id="1179c-112">詳細については、「 [取得名簿またはユーザー プロファイル](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1179c-112">For more information, see [fetch roster or user profile](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile).</span></span> <span data-ttu-id="1179c-113">これらの API には、いくつかの欠点があります。</span><span class="sxs-lookup"><span data-stu-id="1179c-113">These APIs have several shortcomings.</span></span>

<span data-ttu-id="1179c-114">現在、チャットまたはチームの 1 人以上のメンバーの情報を取得する場合は[](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) `TeamsInfo.GetMembersAsync` 、c# または TypeScript または Node.js API の Microsoft Teams ボット API を使用できます `TeamsInfo.getMembers` 。</span><span class="sxs-lookup"><span data-stu-id="1179c-114">Currently, if you want to retrieve information for one or more members of a chat or team, you can use the [Microsoft Teams bot APIs](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) `TeamsInfo.GetMembersAsync` for C# or `TeamsInfo.getMembers` for TypeScript or Node.js APIs.</span></span> <span data-ttu-id="1179c-115">これらの API には、次の欠点があります。</span><span class="sxs-lookup"><span data-stu-id="1179c-115">These APIs have the following shortcomings:</span></span>

* <span data-ttu-id="1179c-116">大規模なチームの場合、パフォーマンスが低下し、タイムアウトが発生する可能性が高くなります: 2017 年初めにTeamsがリリースされて以来、最大チーム サイズが大幅に増加しています。</span><span class="sxs-lookup"><span data-stu-id="1179c-116">For large teams, performance is poor and timeouts are more likely: The maximum team size has grown considerably since Teams was released in early 2017.</span></span> <span data-ttu-id="1179c-117">`GetMembersAsync` `getMembers` メンバーリスト全体を返す場合、大きなチームの API 呼び出しが戻ってくるのに時間がかかり、呼び出しがタイムアウトする場合が一般的で、再試行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1179c-117">As `GetMembersAsync` or `getMembers` returns the entire member list, it takes a long time for the API call to return for large teams, and it is common for the call to time out and you have to try again.</span></span>
* <span data-ttu-id="1179c-118">1 人のユーザーのプロファイルの詳細を取得するのは難しい: 1 人のユーザーのプロファイル情報を取得するには、メンバー リスト全体を取得し、目的のユーザーを検索する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1179c-118">Getting profile details for a single user is difficult: To get the profile information for a single user, you have to retrieve the entire member list and then search for the one you want.</span></span> <span data-ttu-id="1179c-119">Bot Framework SDK には、それを簡単にするためのヘルパー関数がありますが、効率的ではありません。</span><span class="sxs-lookup"><span data-stu-id="1179c-119">There is a helper function in the Bot Framework SDK to make it simpler, but it is not efficient.</span></span>

<span data-ttu-id="1179c-120">組織全体のチームが導入されると、これらの API をOffice 365プライバシーコントロールと連携させる必要があります。</span><span class="sxs-lookup"><span data-stu-id="1179c-120">With the introduction of organization wide teams, there is a requirement to better align these APIs with Office 365 privacy controls.</span></span> <span data-ttu-id="1179c-121">大規模なチームで使用されるボットは、Microsoft Graph アクセス許可と同様の基本的なプロファイル情報を取得できます `User.ReadBasic.All` 。</span><span class="sxs-lookup"><span data-stu-id="1179c-121">Bots used in large teams are able to retrieve basic profile information similar to the `User.ReadBasic.All` Microsoft Graph permission.</span></span> <span data-ttu-id="1179c-122">テナント管理者は、テナントで使用できるアプリやボットを細かく制御できますが、これらの設定は Microsoft Graphとは異なります。</span><span class="sxs-lookup"><span data-stu-id="1179c-122">Tenant administrators have a great deal of control over which apps and bots can be used in their tenant, but these settings are different from Microsoft Graph.</span></span>

<span data-ttu-id="1179c-123">次のコードは、Teamsボット API によって返される内容の JSON 表現のサンプルを提供します。</span><span class="sxs-lookup"><span data-stu-id="1179c-123">The following code provides a sample JSON representation of what is returned by Teams bot APIs:</span></span>

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

## <a name="api-changes"></a><span data-ttu-id="1179c-124">API の変更点</span><span class="sxs-lookup"><span data-stu-id="1179c-124">API Changes</span></span>

<span data-ttu-id="1179c-125">今後の API の変更点を次に示します。</span><span class="sxs-lookup"><span data-stu-id="1179c-125">Following are the upcoming API changes:</span></span>

* <span data-ttu-id="1179c-126">[`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)チャットまたはチームのメンバーのプロファイル情報を取得するための新しい API が作成されます。</span><span class="sxs-lookup"><span data-stu-id="1179c-126">A new API is created [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) for retrieving profile information for members of a chat or team.</span></span> <span data-ttu-id="1179c-127">この API は、ボット フレームワーク バージョン 4.8 以降の SDK で使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="1179c-127">This API is now available with the Bot Framework version 4.8 or later SDK.</span></span> <span data-ttu-id="1179c-128">他のすべてのバージョンでの開発には、 [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="1179c-128">For development in all other versions, use the [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) method.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1179c-129">v3 または v4 では、3.30.2 または 4.8 以降の最新のポイント リリースにそれぞれアップグレードするのが最善の方法です。</span><span class="sxs-lookup"><span data-stu-id="1179c-129">In either v3 or v4, the best action is to upgrade to the latest point release that is 3.30.2 or 4.8 or later respectively.</span></span>

* <span data-ttu-id="1179c-130">[`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details)1 人のユーザーのプロファイル情報を取得するための新しい API が作成されます。</span><span class="sxs-lookup"><span data-stu-id="1179c-130">A new API is created [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) for retrieving the profile information for a single user.</span></span> <span data-ttu-id="1179c-131">チームまたはチャットの ID、および 、Azure Active Directory オブジェクト ID 、またはTeamsユーザー ID である[UPN](/windows/win32/ad/naming-properties#userprincipalname)をパラメーターとして受け取 `userPrincipalName` `objectId` `id` り、そのユーザーのプロファイル情報を返します。</span><span class="sxs-lookup"><span data-stu-id="1179c-131">It takes the ID of the team or chat and a [UPN](/windows/win32/ad/naming-properties#userprincipalname) that is `userPrincipalName`, Azure Active Directory Object ID `objectId`, or the Teams user ID `id` as parameters and returns the profile information for that user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1179c-132">`objectId` は `aadObjectId` 、Bot Framework メッセージのオブジェクトで呼び出される内容に一致するように変更 `Activity` されます。</span><span class="sxs-lookup"><span data-stu-id="1179c-132">`objectId` is changed to `aadObjectId` to match what is called in the `Activity` object of a Bot Framework message.</span></span> <span data-ttu-id="1179c-133">新しい API は、ボット フレームワーク SDK のバージョン 4.8 以降で使用できます。</span><span class="sxs-lookup"><span data-stu-id="1179c-133">The new API is available with version 4.8 or later of the Bot Framework SDK.</span></span> <span data-ttu-id="1179c-134">Teams SDK 拡張機能 Bot Framework 3.x でも使用できます。</span><span class="sxs-lookup"><span data-stu-id="1179c-134">It is also available in the Teams SDK extension Bot Framework 3.x.</span></span> <span data-ttu-id="1179c-135">一方 [、REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) エンドポイントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="1179c-135">Meanwhile, you can use the [REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) endpoint.</span></span>

* <span data-ttu-id="1179c-136">`TeamsInfo.GetMembersAsync` で、型スクリプト `TeamsInfo.getMembers` またはNode.jsは正式に廃止されました。</span><span class="sxs-lookup"><span data-stu-id="1179c-136">`TeamsInfo.GetMembersAsync` in C# and `TeamsInfo.getMembers` in TypeScript or Node.js is formally deprecated.</span></span> <span data-ttu-id="1179c-137">新しい API が利用可能になったら、それを使用するようにボットを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1179c-137">Once the new API is available, you must update your bots to use it.</span></span> <span data-ttu-id="1179c-138">これは、 [これらの API が使用する基盤となる REST API](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)にも適用されます。</span><span class="sxs-lookup"><span data-stu-id="1179c-138">This also applies to the [underlying REST API that these APIs use](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json).</span></span>
* <span data-ttu-id="1179c-139">2021 年後半までに、ボットは `userPrincipalName` `email` チャットまたはチームのメンバーの プロパティまたは プロパティを事前に取得できません。</span><span class="sxs-lookup"><span data-stu-id="1179c-139">By late 2021, bots cannot proactively retrieve the `userPrincipalName` or `email` properties for members of a chat or team.</span></span> <span data-ttu-id="1179c-140">ボットは、Graphを使用して取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1179c-140">Bots must use Graph to retrieve them.</span></span> <span data-ttu-id="1179c-141">`userPrincipalName`および `email` プロパティは `GetConversationPagedMembers` 、2021 年後半から新しい API から返されません。</span><span class="sxs-lookup"><span data-stu-id="1179c-141">The `userPrincipalName` and `email` properties are not returned from the new `GetConversationPagedMembers` API starting in late 2021.</span></span> <span data-ttu-id="1179c-142">ボットは、情報を取得するためにアクセス トークンを使用してGraphを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1179c-142">Bots have to use Graph with an access token to retrieve information.</span></span> <span data-ttu-id="1179c-143">ボットがアクセス トークンを取得し、エンド ユーザーの同意プロセスを簡素化し、簡素化しやすくする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1179c-143">It must be made easier for bots to get an access token and streamline and simplify the end-user consent process.</span></span>
