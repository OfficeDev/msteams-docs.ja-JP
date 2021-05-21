---
title: ボットのコンテキストをMicrosoft Teamsする
description: ボットのコンテキストを取得する方法について説明Microsoft Teams
keywords: teams ボットのコンテキスト
ms.topic: conceptual
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: cda2e24816330964342b097f52bb955c8846c54a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566489"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="191c1-104">ボットのコンテキストをMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="191c1-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="191c1-105">ボットは、チームまたはチャットに関する追加のコンテキスト (ユーザー プロファイルなど) にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="191c1-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="191c1-106">この情報は、ボットの機能を強化し、よりパーソナライズされたエクスペリエンスを提供するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="191c1-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="191c1-107">Microsoft Teams固有のボット API は、ボット ビルダー SDK の拡張機能を通じて最適にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="191c1-107">Microsoft Teams-specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span>
> * <span data-ttu-id="191c1-108">Microsoft.bot.Connector.C#または .NET については[、Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)してください。</span><span class="sxs-lookup"><span data-stu-id="191c1-108">For C# or .NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>
> * <span data-ttu-id="191c1-109">開発Node.js、ボット フレームワーク SDK v4.6 Teams機能の[ボット ビルダーが](https://github.com/microsoft/botframework-sdk)組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="191c1-109">For Node.js development, the Bot Builder for Teams functionality is incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6.</span></span>

## <a name="fetch-the-team-roster"></a><span data-ttu-id="191c1-110">チーム名簿を取得する</span><span class="sxs-lookup"><span data-stu-id="191c1-110">Fetch the team roster</span></span>

<span data-ttu-id="191c1-111">ボットは、チーム メンバーとその基本的なプロファイルの一覧を照会できます。</span><span class="sxs-lookup"><span data-stu-id="191c1-111">Your bot can query for the list of team members and their basic profiles.</span></span> <span data-ttu-id="191c1-112">基本的なプロファイルには、Teams ID、Azure Active Directory ID などの AAD (AAD) 情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="191c1-112">The basic profiles include Teams user IDs and Azure Active Directory (AAD) information such as name and object ID.</span></span> <span data-ttu-id="191c1-113">この情報を使用して、ユーザー ID を関連付けできます。</span><span class="sxs-lookup"><span data-stu-id="191c1-113">You can use this information to correlate user identities.</span></span> <span data-ttu-id="191c1-114">たとえば、AAD 資格情報を使用してタブにログインしたユーザーがチーム メンバーである場合に確認します。</span><span class="sxs-lookup"><span data-stu-id="191c1-114">For example, check if a user logged into a tab through AAD credentials is a team member.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="191c1-115">REST API の例</span><span class="sxs-lookup"><span data-stu-id="191c1-115">REST API example</span></span>

<span data-ttu-id="191c1-116">値をエンドポイントとして使用して、GET 要求 [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) `serviceUrl` を直接発行します。</span><span class="sxs-lookup"><span data-stu-id="191c1-116">Directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="191c1-117">ボットが受け取るアクティビティ ペイロードのオブジェクトは、次の `teamId` `channeldata` シナリオで確認できます。</span><span class="sxs-lookup"><span data-stu-id="191c1-117">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>

* <span data-ttu-id="191c1-118">ユーザーがチーム コンテキストでボットにメッセージを送信または操作する場合。</span><span class="sxs-lookup"><span data-stu-id="191c1-118">When a user messages or interacts with your bot in a team context.</span></span> <span data-ttu-id="191c1-119">詳細については、「メッセージの受信 [」を参照してください](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)。</span><span class="sxs-lookup"><span data-stu-id="191c1-119">For more information, see [receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).</span></span>
* <span data-ttu-id="191c1-120">新しいユーザーまたはボットがチームに追加された場合。</span><span class="sxs-lookup"><span data-stu-id="191c1-120">When a new user or bot is added to a team.</span></span> <span data-ttu-id="191c1-121">詳細については、「チームに [追加されたボットまたはユーザー」を参照してください](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)。</span><span class="sxs-lookup"><span data-stu-id="191c1-121">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).</span></span>

> [!NOTE]
>
>* <span data-ttu-id="191c1-122">API を呼び出す場合は、必ずチーム ID を使用してください。</span><span class="sxs-lookup"><span data-stu-id="191c1-122">Always use the team ID when calling the API.</span></span>
>* <span data-ttu-id="191c1-123">値 `serviceUrl` は安定している傾向がありますが、変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="191c1-123">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="191c1-124">新しいメッセージが届いた場合、ボットは保存されている値を確認する必要 `serviceUrl` があります。</span><span class="sxs-lookup"><span data-stu-id="191c1-124">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

### <a name="net-example"></a><span data-ttu-id="191c1-125">.NET の例</span><span class="sxs-lookup"><span data-stu-id="191c1-125">.NET example</span></span>

<span data-ttu-id="191c1-126">ユーザー `GetConversationMembersAsync` ID `Team.Id` の一覧を取得するために using を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="191c1-126">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

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

### <a name="nodejs-or-typescript-example"></a><span data-ttu-id="191c1-127">Node.jsまたは TypeScript の例</span><span class="sxs-lookup"><span data-stu-id="191c1-127">Node.js or TypeScript example</span></span>

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="191c1-128">個人チャットまたはグループ チャットでユーザー プロファイルまたは名簿を取得する</span><span class="sxs-lookup"><span data-stu-id="191c1-128">Fetch user profile or roster in personal or group chat</span></span>

<span data-ttu-id="191c1-129">任意の個人チャットの API 呼び出しを行って、ボットとチャットしているユーザーのプロファイル情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="191c1-129">You can make the API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="191c1-130">API 呼び出し、SDK メソッド、および応答オブジェクトは、チーム名簿のフェッチと同じです。</span><span class="sxs-lookup"><span data-stu-id="191c1-130">The API call, SDK methods, and the response object are identical to fetching the team roster.</span></span> <span data-ttu-id="191c1-131">唯一の違いは `conversationId` 、. `teamId`</span><span class="sxs-lookup"><span data-stu-id="191c1-131">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetch-the-list-of-channels-in-a-team"></a><span data-ttu-id="191c1-132">チーム内のチャネルの一覧を取得する</span><span class="sxs-lookup"><span data-stu-id="191c1-132">Fetch the list of channels in a team</span></span>

<span data-ttu-id="191c1-133">ボットは、チーム内のチャネルの一覧を照会できます。</span><span class="sxs-lookup"><span data-stu-id="191c1-133">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="191c1-134">ローカライズを許可するために、既定の一般チャネル `null` の名前が返されます。</span><span class="sxs-lookup"><span data-stu-id="191c1-134">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="191c1-135">General チャネルのチャネル ID は、常にチーム ID と一致します。</span><span class="sxs-lookup"><span data-stu-id="191c1-135">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="191c1-136">REST API の例</span><span class="sxs-lookup"><span data-stu-id="191c1-136">REST API example</span></span>

<span data-ttu-id="191c1-137">値をエンドポイントとして使用して、GET 要求 `/teams/{teamId}/conversations/` `serviceUrl` を直接発行します。</span><span class="sxs-lookup"><span data-stu-id="191c1-137">Directly issue a GET request on `/teams/{teamId}/conversations/`, using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="191c1-138">唯一のソース `teamId` は、チーム コンテキストからのメッセージです。</span><span class="sxs-lookup"><span data-stu-id="191c1-138">The only source for `teamId` is a message from the team context.</span></span> <span data-ttu-id="191c1-139">メッセージは、ユーザーからのメッセージか、ボットがチームに追加するときに受信するメッセージのいずれかです。</span><span class="sxs-lookup"><span data-stu-id="191c1-139">The message is either a message from a user or the message that your bot receives when it is added to a team.</span></span> <span data-ttu-id="191c1-140">詳細については、「チームに [追加されたボットまたはユーザー」を参照してください](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)。</span><span class="sxs-lookup"><span data-stu-id="191c1-140">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).</span></span>

> [!NOTE]
> <span data-ttu-id="191c1-141">値 `serviceUrl` は安定している傾向がありますが、変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="191c1-141">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="191c1-142">新しいメッセージが届いた場合、ボットは保存されている値を確認する必要 `serviceUrl` があります。</span><span class="sxs-lookup"><span data-stu-id="191c1-142">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

#### <a name="net-example"></a><span data-ttu-id="191c1-143">.NET の例</span><span class="sxs-lookup"><span data-stu-id="191c1-143">.NET example</span></span>

<span data-ttu-id="191c1-144">次の例では、ボット ビルダー SDK for .NET Teams拡張機能からの呼び `FetchChannelList` [出しを使用します](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)。</span><span class="sxs-lookup"><span data-stu-id="191c1-144">The following example uses the `FetchChannelList` call from the [Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="191c1-145">Node.js例</span><span class="sxs-lookup"><span data-stu-id="191c1-145">Node.js example</span></span>

<span data-ttu-id="191c1-146">次の例では、ボット ビルダー SDK Teams `fetchChannelList` [拡張機能からの呼び出しを使用Node.js。 ](https://www.npmjs.com/package/botbuilder-teams)</span><span class="sxs-lookup"><span data-stu-id="191c1-146">The following example uses `fetchChannelList` call from the [Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams):</span></span>

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

## <a name="get-clientinfo-in-your-bot-context"></a><span data-ttu-id="191c1-147">ボット コンテキストで clientInfo を取得する</span><span class="sxs-lookup"><span data-stu-id="191c1-147">Get clientInfo in your bot context</span></span>

<span data-ttu-id="191c1-148">ボットのアクティビティ内で clientInfo をフェッチできます。</span><span class="sxs-lookup"><span data-stu-id="191c1-148">You can fetch the clientInfo within your bot's activity.</span></span> <span data-ttu-id="191c1-149">clientInfo には、次のプロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="191c1-149">The clientInfo contains the following properties:</span></span>

* <span data-ttu-id="191c1-150">Locale</span><span class="sxs-lookup"><span data-stu-id="191c1-150">Locale</span></span>
* <span data-ttu-id="191c1-151">国</span><span class="sxs-lookup"><span data-stu-id="191c1-151">Country</span></span>
* <span data-ttu-id="191c1-152">プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="191c1-152">Platform</span></span>
* <span data-ttu-id="191c1-153">タイムゾーン</span><span class="sxs-lookup"><span data-stu-id="191c1-153">Timezone</span></span>

### <a name="json-example"></a><span data-ttu-id="191c1-154">JSON の例</span><span class="sxs-lookup"><span data-stu-id="191c1-154">JSON example</span></span>

```json
[
    {
        "type": "clientInfo",
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "Asia/Calcutta"
    }
]
```

### <a name="c-example"></a><span data-ttu-id="191c1-155">C#例</span><span class="sxs-lookup"><span data-stu-id="191c1-155">C# example</span></span>

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```

## <a name="see-also"></a><span data-ttu-id="191c1-156">関連項目</span><span class="sxs-lookup"><span data-stu-id="191c1-156">See also</span></span>

<span data-ttu-id="191c1-157">[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="191c1-157">[Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>