---
title: Bot のコンテキストを取得する
description: Microsoft Teams でボットのコンテキストを取得する方法について説明します。
keywords: teams の bot コンテキスト
ms.date: 05/20/2019
ms.openlocfilehash: 2dea6fd51e7274fa899d9ae882441a21618d7e09
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675110"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="03df6-104">Microsoft Teams の bot のコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="03df6-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="03df6-105">Bot は、ユーザープロファイルなどのチームまたはチャットに関する追加のコンテキストにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="03df6-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="03df6-106">この情報は、ボットの機能を強化し、よりパーソナライズされた環境を提供するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="03df6-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
> <span data-ttu-id="03df6-107">これらの Microsoft&ndash;Teams 固有の bot api には、BOT ビルダー SDK の拡張機能を通じてアクセスすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="03df6-107">These Microsoft Teams&ndash;specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span> <span data-ttu-id="03df6-108">C#/.NET については、「 [Microsoft の Bot](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージをダウンロードしてください。</span><span class="sxs-lookup"><span data-stu-id="03df6-108">For C#/.NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span> <span data-ttu-id="03df6-109">Node.js を開発する場合は、 [botbuilder](https://www.npmjs.com/package/botbuilder-teams)の npm パッケージをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="03df6-109">For Node.js development, you can install the [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) npm package.</span></span> <span data-ttu-id="03df6-110">両方の Sdk がターゲットボットビルダー v3。</span><span class="sxs-lookup"><span data-stu-id="03df6-110">Both SDKs target Bot Builder v3.</span></span>

## <a name="fetching-the-team-roster"></a><span data-ttu-id="03df6-111">チーム名簿を取得する</span><span class="sxs-lookup"><span data-stu-id="03df6-111">Fetching the team roster</span></span>

<span data-ttu-id="03df6-112">Bot は、チームメンバーの一覧とその基本プロファイルを照会できます。これには、Teams のユーザー Id と、名前や objectId などの Azure Active Directory (Azure AD) の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="03df6-112">Your bot can query for the list of team members and their basic profiles, which includes Teams user IDs and Azure Active Directory (Azure AD) information such as name and objectId.</span></span> <span data-ttu-id="03df6-113">この情報を使用して、ユーザー id を関連付けることができます。たとえば、Azure AD 資格情報を介してタブにログインしているユーザーが、チームのメンバーであるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="03df6-113">You can use this information to correlate user identities; for example, to check whether a user logged into a tab through Azure AD credentials is a member of the team.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="03df6-114">REST API の例</span><span class="sxs-lookup"><span data-stu-id="03df6-114">REST API example</span></span>

<span data-ttu-id="03df6-115">エンドポイントとしての[`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) `serviceUrl`値を使用して、GET 要求を直接発行することができます。</span><span class="sxs-lookup"><span data-stu-id="03df6-115">You can directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the value of `serviceUrl` as the endpoint.</span></span>

<span data-ttu-id="03df6-116">は`teamId` 、次のシナリオで`channeldata` 、ボットが受け取るアクティビティペイロードのオブジェクトにあります。</span><span class="sxs-lookup"><span data-stu-id="03df6-116">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>
* <span data-ttu-id="03df6-117">ユーザーがチームコンテキストの bot との間でメッセージを送信したり、対話したりする場合 ([メッセージの受信](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)を参照)</span><span class="sxs-lookup"><span data-stu-id="03df6-117">When a user messages or interacts with your bot in a team context (see [Receiving Messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))</span></span>
* <span data-ttu-id="03df6-118">新しいユーザーまたは bot がチームに追加されたとき (「[チームに追加された bot またはユーザー」を](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)参照)</span><span class="sxs-lookup"><span data-stu-id="03df6-118">When a new user or bot is added to a team (see [Bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))</span></span>

> [!NOTE]
>* <span data-ttu-id="03df6-119">Api を呼び出すときにチーム id を必ず使用してください。</span><span class="sxs-lookup"><span data-stu-id="03df6-119">Make sure to use the team id when calling the api</span></span>
>* <span data-ttu-id="03df6-120">の`serviceUrl`値は安定していますが、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="03df6-120">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="03df6-121">新しいメッセージが到着すると、ボットはに格納されて`serviceUrl`いる値を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="03df6-121">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

```json
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members

Response body
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

### <a name="net-example"></a><span data-ttu-id="03df6-122">.NET の例</span><span class="sxs-lookup"><span data-stu-id="03df6-122">.NET example</span></span>

<span data-ttu-id="03df6-123">を`GetConversationMembersAsync`使用`Team.Id`して、ユーザー id のリストを返します。</span><span class="sxs-lookup"><span data-stu-id="03df6-123">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

```csharp
// Fetch the members in the current conversation
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));
var teamId = context.Activity.GetChannelData<TeamsChannelData>().Team.Id;
var members = await connector.Conversations.GetConversationMembersAsync(teamId);

// Concatenate information about all members into a string
var sb = new StringBuilder();
foreach (var member in members.AsTeamsChannelAccounts())
{
    sb.AppendFormat(
        "GivenName = {0}, TeamsMemberId = {1}",
        member.Name, member.Id);

    sb.AppendLine();
}

// Post the member info back into the conversation
await context.PostAsync($"People in this conversation: {sb.ToString()}");
```

### <a name="nodejstypescript-example"></a><span data-ttu-id="03df6-124">Node.js/TypeScript の例</span><span class="sxs-lookup"><span data-stu-id="03df6-124">Node.js/TypeScript example</span></span>

<span data-ttu-id="03df6-125">次の例では、 [node.js の Bot ビルダー SDK の Microsoft Teams 拡張機能](https://www.npmjs.com/package/botbuilder-teams)を使用しています。</span><span class="sxs-lookup"><span data-stu-id="03df6-125">The following example uses the [Microsoft Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams).</span></span>

```typescript

[...]
import * as builder from "botbuilder";
[...]

var teamId = session.message.sourceEvent.team.id;
connector.fetchMembers(
  (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is some error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```

## <a name="fetching-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="03df6-126">個人またはグループチャットでのユーザープロファイルまたは名簿の取得</span><span class="sxs-lookup"><span data-stu-id="03df6-126">Fetching user profile or roster in personal or group chat</span></span>

<span data-ttu-id="03df6-127">また、任意の個人チャットに対して同じ API 呼び出しを行うことにより、ユーザーが bot とチャットする際のプロファイル情報を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="03df6-127">You can also make the same API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="03df6-128">API call および SDK のメソッドは、応答オブジェクトと同様に、チーム名簿を取得するのと同じです。</span><span class="sxs-lookup"><span data-stu-id="03df6-128">The API call and SDK methods are identical to fetching the team roster, as is the response object.</span></span> <span data-ttu-id="03df6-129">唯一の違いは、では`conversationId`なくを渡し`teamId`ます。</span><span class="sxs-lookup"><span data-stu-id="03df6-129">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetching-the-list-of-channels-in-a-team"></a><span data-ttu-id="03df6-130">チーム内のチャネルのリストの取得</span><span class="sxs-lookup"><span data-stu-id="03df6-130">Fetching the list of channels in a team</span></span>

<span data-ttu-id="03df6-131">Bot は、チーム内のチャネルの一覧を照会できます。</span><span class="sxs-lookup"><span data-stu-id="03df6-131">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="03df6-132">既定の一般的なチャネルの名前は、ローカリゼーション`null`を許可するためにとして返されます。</span><span class="sxs-lookup"><span data-stu-id="03df6-132">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="03df6-133">一般チャネルのチャネル ID は、常にチーム ID と一致します。</span><span class="sxs-lookup"><span data-stu-id="03df6-133">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="03df6-134">REST API の例</span><span class="sxs-lookup"><span data-stu-id="03df6-134">REST API example</span></span>

<span data-ttu-id="03df6-135">エンドポイントとしての`/teams/{teamId}/conversations/` `serviceUrl`値を使用して、GET 要求を直接発行することができます。</span><span class="sxs-lookup"><span data-stu-id="03df6-135">You can directly issue a GET request on `/teams/{teamId}/conversations/`, using the value of `serviceUrl` as the endpoint.</span></span>

<span data-ttu-id="03df6-136">の唯一の`teamId`ソースは、チームコンテキストからのメッセージです。これは、ユーザーからのメッセージ、または、チームに追加されたときにボットが受信するメッセージのどちらかです (「[チームに追加されたボットまたはユーザー」を](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)参照)。</span><span class="sxs-lookup"><span data-stu-id="03df6-136">The only source for `teamId` is a message from the team context - either a message from a user or the message that your bot receives when it is added to a team (see [Bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).</span></span>

> [!NOTE]
> <span data-ttu-id="03df6-137">の`serviceUrl`値は安定していますが、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="03df6-137">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="03df6-138">新しいメッセージが到着すると、ボットはに格納されて`serviceUrl`いる値を確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="03df6-138">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

```json
GET /v3/teams/19%3A033451497ea84fcc83d17ed7fb08a1b6%40thread.skype/conversations

Response body
{
    "conversations": [{
        "id": "19:033451497ea84fcc83d17ed7fb08a1b6@thread.skype",
        "name": null
    }, {
        "id": "19:cc25e4aae50746ecbb11473bba24c70a@thread.skype",
        "name": "Materials"
    }, {
        "id": "19:b7b84cba410c406ba671dbbf5e0a3519@thread.skype",
        "name": "Design"
    }, {
        "id": "19:fc5db2aed489454e8f8c06829ed6c986@thread.skype",
        "name": "Marketing"
    }]
}
```

#### <a name="net-example"></a><span data-ttu-id="03df6-139">.NET の例</span><span class="sxs-lookup"><span data-stu-id="03df6-139">.NET example</span></span>

<span data-ttu-id="03df6-140">次の例では`FetchChannelList` 、[ボット Builder SDK For .Net の Microsoft Teams 拡張機能](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)からの呼び出しを使用しています。</span><span class="sxs-lookup"><span data-stu-id="03df6-140">The following example uses the `FetchChannelList` call from the [Microsoft Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="03df6-141">Node.js の例</span><span class="sxs-lookup"><span data-stu-id="03df6-141">Node.js example</span></span>

<span data-ttu-id="03df6-142">次の例で`fetchChannelList`は、 [Node.js の Bot ビルダー SDK の Microsoft Teams 拡張機能](https://www.npmjs.com/package/botbuilder-teams)からの呼び出しを使用しています。</span><span class="sxs-lookup"><span data-stu-id="03df6-142">The following example uses `fetchChannelList` call from the [Microsoft Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams).</span></span>

```javascript
var teamId = session.message.sourceEvent.team.id;
connector.fetchChannelList(
  (session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is an error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```
