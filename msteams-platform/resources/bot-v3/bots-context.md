---
title: Microsoft Teams ボットのコンテキストを取得する
description: Microsoft Teams でボットのコンテキストを取得する方法について説明します。
keywords: チーム ボットのコンテキスト
ms.date: 05/20/2019
ms.openlocfilehash: 1465e6624b4eaadd73e2d4d9cf87fccedc002e52
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231553"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="2d017-104">Microsoft Teams ボットのコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="2d017-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="2d017-105">ボットは、ユーザー プロファイルなど、チームまたはチャットに関する追加のコンテキストにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="2d017-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="2d017-106">この情報は、ボットの機能を強化し、よりカスタマイズされたエクスペリエンスを提供するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="2d017-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="2d017-107">Microsoft Teams 固有のボット API は、Bot Builder SDK の拡張機能を通じて最適にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="2d017-107">Microsoft Teams-specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span>
> * <span data-ttu-id="2d017-108">C# または .NET の場合は [、Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="2d017-108">For C# or .NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>
> * <span data-ttu-id="2d017-109">開発Node.js、Teams のボット ビルダー機能は [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6 に組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="2d017-109">For Node.js development, the Bot Builder for Teams functionality is incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6.</span></span>

## <a name="fetch-the-team-roster"></a><span data-ttu-id="2d017-110">チーム名簿を取得する</span><span class="sxs-lookup"><span data-stu-id="2d017-110">Fetch the team roster</span></span>

<span data-ttu-id="2d017-111">ボットは、チーム メンバーのリストとその基本的なプロファイルを照会できます。</span><span class="sxs-lookup"><span data-stu-id="2d017-111">Your bot can query for the list of team members and their basic profiles.</span></span> <span data-ttu-id="2d017-112">基本的なプロファイルには、Teams ユーザー ID と、名前やオブジェクト ID などの Azure Active Directory (AAD) 情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2d017-112">The basic profiles include Teams user IDs and Azure Active Directory (AAD) information such as name and object ID.</span></span> <span data-ttu-id="2d017-113">この情報を使用して、ユーザー ID を関連付けできます。</span><span class="sxs-lookup"><span data-stu-id="2d017-113">You can use this information to correlate user identities.</span></span> <span data-ttu-id="2d017-114">たとえば、AAD 資格情報を使用してタブにログインしたユーザーがチーム メンバーである場合を確認します。</span><span class="sxs-lookup"><span data-stu-id="2d017-114">For example, check if a user logged into a tab through AAD credentials is a team member.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="2d017-115">REST API の例</span><span class="sxs-lookup"><span data-stu-id="2d017-115">REST API example</span></span>

<span data-ttu-id="2d017-116">値をエンドポイントとして使用して、GET [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) `serviceUrl` 要求を直接発行します。</span><span class="sxs-lookup"><span data-stu-id="2d017-116">Directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="2d017-117">次 `teamId` のシナリオでは、ボットが受け取るアクティビティ ペイロード `channeldata` のオブジェクト内で確認できます。</span><span class="sxs-lookup"><span data-stu-id="2d017-117">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>

* <span data-ttu-id="2d017-118">ユーザーがチーム コンテキストでボットにメッセージを送信または操作する場合。</span><span class="sxs-lookup"><span data-stu-id="2d017-118">When a user messages or interacts with your bot in a team context.</span></span> <span data-ttu-id="2d017-119">詳細については、「メッセージの受信 [」を参照してください](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)。</span><span class="sxs-lookup"><span data-stu-id="2d017-119">For more information, see [receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).</span></span>
* <span data-ttu-id="2d017-120">新しいユーザーまたはボットがチームに追加された場合。</span><span class="sxs-lookup"><span data-stu-id="2d017-120">When a new user or bot is added to a team.</span></span> <span data-ttu-id="2d017-121">詳細については、チームに [追加されたボットまたはユーザーを参照してください](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)。</span><span class="sxs-lookup"><span data-stu-id="2d017-121">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).</span></span>

> [!NOTE]
>
>* <span data-ttu-id="2d017-122">API を呼び出す場合は、常にチーム ID を使用します。</span><span class="sxs-lookup"><span data-stu-id="2d017-122">Always use the team ID when calling the API.</span></span>
>* <span data-ttu-id="2d017-123">値 `serviceUrl` は安定する傾向がありますが、変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2d017-123">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="2d017-124">新しいメッセージが到着したら、ボットは保存された値を確認する必要 `serviceUrl` があります。</span><span class="sxs-lookup"><span data-stu-id="2d017-124">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

### <a name="net-example"></a><span data-ttu-id="2d017-125">.NET の例</span><span class="sxs-lookup"><span data-stu-id="2d017-125">.NET example</span></span>

<span data-ttu-id="2d017-126">ユーザー `GetConversationMembersAsync` ID `Team.Id` の一覧を返す呼び出し</span><span class="sxs-lookup"><span data-stu-id="2d017-126">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

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

### <a name="nodejs-or-typescript-example"></a><span data-ttu-id="2d017-127">Node.jsまたは TypeScript の例</span><span class="sxs-lookup"><span data-stu-id="2d017-127">Node.js or TypeScript example</span></span>

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

<span data-ttu-id="2d017-128">また [、Bot Framework のサンプルも参照してください](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="2d017-128">Also, see [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="2d017-129">個人チャットまたはグループ チャットでユーザー プロファイルまたは名簿を取得する</span><span class="sxs-lookup"><span data-stu-id="2d017-129">Fetch user profile or roster in personal or group chat</span></span>

<span data-ttu-id="2d017-130">任意の個人チャットの API 呼び出しを行って、ボットとチャットしているユーザーのプロファイル情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="2d017-130">You can make the API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="2d017-131">API 呼び出し、SDK メソッド、および応答オブジェクトは、チーム名簿の取得と同じです。</span><span class="sxs-lookup"><span data-stu-id="2d017-131">The API call, SDK methods, and the response object are identical to fetching the team roster.</span></span> <span data-ttu-id="2d017-132">唯一の違いは、 `conversationId` `teamId` .</span><span class="sxs-lookup"><span data-stu-id="2d017-132">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetch-the-list-of-channels-in-a-team"></a><span data-ttu-id="2d017-133">チーム内のチャネルの一覧を取得する</span><span class="sxs-lookup"><span data-stu-id="2d017-133">Fetch the list of channels in a team</span></span>

<span data-ttu-id="2d017-134">ボットは、チーム内のチャネルの一覧を照会できます。</span><span class="sxs-lookup"><span data-stu-id="2d017-134">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="2d017-135">ローカライズを許可するために、既定の全般チャネル `null` の名前が返されます。</span><span class="sxs-lookup"><span data-stu-id="2d017-135">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="2d017-136">一般チャネルのチャネル ID は、常にチーム ID と一致します。</span><span class="sxs-lookup"><span data-stu-id="2d017-136">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="2d017-137">REST API の例</span><span class="sxs-lookup"><span data-stu-id="2d017-137">REST API example</span></span>

<span data-ttu-id="2d017-138">値をエンドポイントとして使用して、GET `/teams/{teamId}/conversations/` `serviceUrl` 要求を直接発行します。</span><span class="sxs-lookup"><span data-stu-id="2d017-138">Directly issue a GET request on `/teams/{teamId}/conversations/`, using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="2d017-139">唯一のソース `teamId` は、チーム コンテキストからのメッセージです。</span><span class="sxs-lookup"><span data-stu-id="2d017-139">The only source for `teamId` is a message from the team context.</span></span> <span data-ttu-id="2d017-140">メッセージは、ユーザーからのメッセージか、ボットがチームに追加された際に受信するメッセージのいずれかです。</span><span class="sxs-lookup"><span data-stu-id="2d017-140">The message is either a message from a user or the message that your bot receives when it is added to a team.</span></span> <span data-ttu-id="2d017-141">詳細については、チームに [追加されたボットまたはユーザーを参照してください](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)。</span><span class="sxs-lookup"><span data-stu-id="2d017-141">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).</span></span>

> [!NOTE]
> <span data-ttu-id="2d017-142">値 `serviceUrl` は安定する傾向がありますが、変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2d017-142">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="2d017-143">新しいメッセージが到着したら、ボットは保存された値を確認する必要 `serviceUrl` があります。</span><span class="sxs-lookup"><span data-stu-id="2d017-143">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

#### <a name="net-example"></a><span data-ttu-id="2d017-144">.NET の例</span><span class="sxs-lookup"><span data-stu-id="2d017-144">.NET example</span></span>

<span data-ttu-id="2d017-145">次の例では、.NET 用 Bot Builder SDK の Teams 拡張機能からの呼び `FetchChannelList` [出しを使用します](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)。</span><span class="sxs-lookup"><span data-stu-id="2d017-145">The following example uses the `FetchChannelList` call from the [Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="2d017-146">Node.js例</span><span class="sxs-lookup"><span data-stu-id="2d017-146">Node.js example</span></span>

<span data-ttu-id="2d017-147">次の例では、Bot Builder SDK for Node.jsの Teams 拡張機能からの呼び出 `fetchChannelList` [しを使用します ](https://www.npmjs.com/package/botbuilder-teams)。</span><span class="sxs-lookup"><span data-stu-id="2d017-147">The following example uses `fetchChannelList` call from the [Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams):</span></span>

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

## <a name="get-clientinfo-in-your-bot-context"></a><span data-ttu-id="2d017-148">ボット コンテキストで clientInfo を取得する</span><span class="sxs-lookup"><span data-stu-id="2d017-148">Get clientInfo in your bot context</span></span>

<span data-ttu-id="2d017-149">ボットのアクティビティ内で clientInfo をフェッチできます。</span><span class="sxs-lookup"><span data-stu-id="2d017-149">You can fetch the clientInfo within your bot's activity.</span></span> <span data-ttu-id="2d017-150">clientInfo には、次のプロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2d017-150">The clientInfo contains the following properties:</span></span>

* <span data-ttu-id="2d017-151">Locale</span><span class="sxs-lookup"><span data-stu-id="2d017-151">Locale</span></span>
* <span data-ttu-id="2d017-152">国</span><span class="sxs-lookup"><span data-stu-id="2d017-152">Country</span></span>
* <span data-ttu-id="2d017-153">プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="2d017-153">Platform</span></span>
* <span data-ttu-id="2d017-154">タイムゾーン</span><span class="sxs-lookup"><span data-stu-id="2d017-154">Timezone</span></span>

### <a name="json-example"></a><span data-ttu-id="2d017-155">JSON の例</span><span class="sxs-lookup"><span data-stu-id="2d017-155">JSON example</span></span>

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

### <a name="c-example"></a><span data-ttu-id="2d017-156">C# の例</span><span class="sxs-lookup"><span data-stu-id="2d017-156">C# example</span></span>

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```