---
title: Bot のコンテキストを取得する
description: Microsoft Teams でボットのコンテキストを取得する方法について説明します。
keywords: teams の bot コンテキスト
ms.date: 05/20/2019
ms.openlocfilehash: 8f054661664850ffb843714230e209c8e4737f0a
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796163"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="266dc-104">Microsoft Teams の bot のコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="266dc-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="266dc-105">Bot は、ユーザープロファイルなどのチームまたはチャットに関する追加のコンテキストにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="266dc-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="266dc-106">この情報は、ボットの機能を強化し、よりパーソナライズされた環境を提供するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="266dc-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
> <span data-ttu-id="266dc-107">これらの Microsoft Teams &ndash; 固有の Bot api には、Bot ビルダー SDK の拡張機能を通じてアクセスすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="266dc-107">These Microsoft Teams&ndash;specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span> <span data-ttu-id="266dc-108">C#/.NET については、「 [Microsoft の Bot](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージをダウンロードしてください。</span><span class="sxs-lookup"><span data-stu-id="266dc-108">For C#/.NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span> <span data-ttu-id="266dc-109">Node.js 開発では、BotBuilder for Microsoft Teams の機能が、v2.0 [FRAMEWORK SDK](https://github.com/microsoft/botframework-sdk) in v2.0 に組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="266dc-109">For Node.js development, the BotBuilder for Microsoft Teams functionality has been incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) as of v4.6.</span></span>

## <a name="fetching-the-team-roster"></a><span data-ttu-id="266dc-110">チーム名簿を取得する</span><span class="sxs-lookup"><span data-stu-id="266dc-110">Fetching the team roster</span></span>

<span data-ttu-id="266dc-111">Bot は、チームメンバーの一覧とその基本プロファイルを照会できます。これには、Teams のユーザー Id と、名前や objectId などの Azure Active Directory (Azure AD) の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="266dc-111">Your bot can query for the list of team members and their basic profiles, which includes Teams user IDs and Azure Active Directory (Azure AD) information such as name and objectId.</span></span> <span data-ttu-id="266dc-112">この情報を使用して、ユーザー id を関連付けることができます。たとえば、Azure AD 資格情報を介してタブにログインしているユーザーが、チームのメンバーであるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="266dc-112">You can use this information to correlate user identities; for example, to check whether a user logged into a tab through Azure AD credentials is a member of the team.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="266dc-113">REST API の例</span><span class="sxs-lookup"><span data-stu-id="266dc-113">REST API example</span></span>

<span data-ttu-id="266dc-114">[`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members)エンドポイントとしての値を使用して、GET 要求を直接発行することができ `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="266dc-114">You can directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the value of `serviceUrl` as the endpoint.</span></span>

<span data-ttu-id="266dc-115">は、 `teamId` `channeldata` 次のシナリオで、ボットが受け取るアクティビティペイロードのオブジェクトにあります。</span><span class="sxs-lookup"><span data-stu-id="266dc-115">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>
* <span data-ttu-id="266dc-116">ユーザーがチームコンテキストの bot との間でメッセージを送信したり、対話したりする場合 ( [メッセージの受信](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)を参照)</span><span class="sxs-lookup"><span data-stu-id="266dc-116">When a user messages or interacts with your bot in a team context (see [Receiving Messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))</span></span>
* <span data-ttu-id="266dc-117">新しいユーザーまたは bot がチームに追加されたとき (「 [チームに追加された bot またはユーザー」を](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)参照)</span><span class="sxs-lookup"><span data-stu-id="266dc-117">When a new user or bot is added to a team (see [Bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))</span></span>

> [!NOTE]
>* <span data-ttu-id="266dc-118">Api を呼び出すときにチーム id を必ず使用してください。</span><span class="sxs-lookup"><span data-stu-id="266dc-118">Make sure to use the team id when calling the api</span></span>
>* <span data-ttu-id="266dc-119">の値は `serviceUrl` 安定していますが、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="266dc-119">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="266dc-120">新しいメッセージが到着すると、ボットはに格納されている値を確認する必要があり `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="266dc-120">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

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

### <a name="net-example"></a><span data-ttu-id="266dc-121">.NET の例</span><span class="sxs-lookup"><span data-stu-id="266dc-121">.NET example</span></span>

<span data-ttu-id="266dc-122">を `GetConversationMembersAsync` 使用して `Team.Id` 、ユーザー id のリストを返します。</span><span class="sxs-lookup"><span data-stu-id="266dc-122">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

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

### <a name="nodejstypescript-example"></a><span data-ttu-id="266dc-123">Node.js/TypeScript の例</span><span class="sxs-lookup"><span data-stu-id="266dc-123">Node.js/TypeScript example</span></span>

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

<span data-ttu-id="266dc-124">[Bot フレームワークサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)*も参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="266dc-124">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="fetching-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="266dc-125">個人またはグループチャットでのユーザープロファイルまたは名簿の取得</span><span class="sxs-lookup"><span data-stu-id="266dc-125">Fetching user profile or roster in personal or group chat</span></span>

<span data-ttu-id="266dc-126">また、任意の個人チャットに対して同じ API 呼び出しを行うことにより、ユーザーが bot とチャットする際のプロファイル情報を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="266dc-126">You can also make the same API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="266dc-127">API call および SDK のメソッドは、応答オブジェクトと同様に、チーム名簿を取得するのと同じです。</span><span class="sxs-lookup"><span data-stu-id="266dc-127">The API call and SDK methods are identical to fetching the team roster, as is the response object.</span></span> <span data-ttu-id="266dc-128">唯一の違いは、では `conversationId` なくを渡し `teamId` ます。</span><span class="sxs-lookup"><span data-stu-id="266dc-128">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetching-the-list-of-channels-in-a-team"></a><span data-ttu-id="266dc-129">チーム内のチャネルのリストの取得</span><span class="sxs-lookup"><span data-stu-id="266dc-129">Fetching the list of channels in a team</span></span>

<span data-ttu-id="266dc-130">Bot は、チーム内のチャネルの一覧を照会できます。</span><span class="sxs-lookup"><span data-stu-id="266dc-130">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="266dc-131">既定の一般的なチャネルの名前は、 `null` ローカリゼーションを許可するためにとして返されます。</span><span class="sxs-lookup"><span data-stu-id="266dc-131">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="266dc-132">一般チャネルのチャネル ID は、常にチーム ID と一致します。</span><span class="sxs-lookup"><span data-stu-id="266dc-132">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="266dc-133">REST API の例</span><span class="sxs-lookup"><span data-stu-id="266dc-133">REST API example</span></span>

<span data-ttu-id="266dc-134">`/teams/{teamId}/conversations/`エンドポイントとしての値を使用して、GET 要求を直接発行することができ `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="266dc-134">You can directly issue a GET request on `/teams/{teamId}/conversations/`, using the value of `serviceUrl` as the endpoint.</span></span>

<span data-ttu-id="266dc-135">の唯一のソース `teamId` は、チームコンテキストからのメッセージです。これは、ユーザーからのメッセージ、または、チームに追加されたときにボットが受信するメッセージのどちらかです (「 [チームに追加されたボットまたはユーザー」を](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)参照)。</span><span class="sxs-lookup"><span data-stu-id="266dc-135">The only source for `teamId` is a message from the team context - either a message from a user or the message that your bot receives when it is added to a team (see [Bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).</span></span>

> [!NOTE]
> <span data-ttu-id="266dc-136">の値は `serviceUrl` 安定していますが、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="266dc-136">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="266dc-137">新しいメッセージが到着すると、ボットはに格納されている値を確認する必要があり `serviceUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="266dc-137">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

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

#### <a name="net-example"></a><span data-ttu-id="266dc-138">.NET の例</span><span class="sxs-lookup"><span data-stu-id="266dc-138">.NET example</span></span>

<span data-ttu-id="266dc-139">次の例では、 `FetchChannelList` [ボット Builder SDK for .Net の Microsoft Teams 拡張機能](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)からの呼び出しを使用しています。</span><span class="sxs-lookup"><span data-stu-id="266dc-139">The following example uses the `FetchChannelList` call from the [Microsoft Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="266dc-140">Node.js の例</span><span class="sxs-lookup"><span data-stu-id="266dc-140">Node.js example</span></span>

<span data-ttu-id="266dc-141">次の例では、 `fetchChannelList` [Node.jsの BOT ビルダー SDK の Microsoft Teams 拡張機能 ](https://www.npmjs.com/package/botbuilder-teams)からの呼び出しを使用しています。</span><span class="sxs-lookup"><span data-stu-id="266dc-141">The following example uses `fetchChannelList` call from the [Microsoft Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams).</span></span>

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
