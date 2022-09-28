---
title: 会話イベント
author: WashingtonKayaker
description: サンプル (.NET、Node.js、Python) を使用して、Microsoft Teams ボットからの会話イベント、チャネル イベントの更新、チーム メンバー イベント、メッセージリアクション イベントを操作します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
keywords: イベント ボット チャネル メッセージの反応の会話
ms.openlocfilehash: 6bf1be094afc778317f2e4d5a7657514d35b9777
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100358"
---
# <a name="conversation-events-in-your-teams-bot"></a>Teams ボットの会話イベント

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Microsoft Teams 用の会話ボットを構築する場合は、会話イベントを操作できます。 Teams はボットがアクティブな範囲で発生する会話イベントの通知をボットに送ります。 コードでこれらのイベントをキャプチャして、以下のアクションを行うことができます。

* ボットがチームに追加されたときに、ウェルカム メッセージをトリガーする。
* 新しいチーム メンバーが追加または削除されたときにウェルカム メッセージをトリガーする。
* チャネルが作成、名前変更、削除されたときに通知をトリガーする。
* ボット メッセージがユーザーによって「いいね!」されたときに通知をトリガーする。
* インストール中に、ユーザー入力 (選択) からボットの既定のチャネルを特定します。

## <a name="conversation-update-events"></a>会話の更新イベント

会話更新イベントを使用すると、より良い通知と効果的なボット アクションを提供できます。

> [!IMPORTANT]
>
> * 新しいイベントはいつでも追加でき、ボットはその受信を開始します。
> * 予期しないイベントを受け取るようにボットを設計する必要があります。
> * Bot Framework SDK を使用している場合、ボットは、処理しないことを選択したイベントに対して `200 - OK` で自動的に応答します。

ボットは、次のいずれかの場合に `conversationUpdate` イベントを受け取ります。

* ボットが会話に追加された場合。
* 会話に他のメンバーが追加または削除されます。
* 会話メタデータが変更されました。

`conversationUpdate` イベントは、ボットが追加されているチームのメンバーシップの更新に関する情報を受信したときにボットに送信されます。 また、ボットが個人の会話に初めて追加されたときにも更新を受け取ります。

次の表は、Teams 会話更新イベントの一覧と詳細を示しています。

| 実行されたアクション        | EventType         | 呼び出されたメソッド              | 説明                | 範囲 |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| チャネルを作成しました     | channelCreated    | OnTeamsChannelCreatedAsync | [チャネルが作成される](#channel-created)。 | チーム |
| チャネルの名前が変更されました     | channelRenamed    | OnTeamsChannelRenamedAsync | [チャネルの名前が変更されます](#channel-renamed)。 | チーム |
| チャネルが削除されました     | channelDeleted    | OnTeamsChannelDeletedAsync | [チャネルが削除されます](#channel-deleted)。 | チーム |
| 復元されたチャネル    | channelRestored    | OnTeamsChannelRestoredAsync | [チャネルが復元されます](#channel-deleted)。 | チーム |
| メンバーが追加されました   | membersAdded   | OnTeamsMembersAddedAsync   | [メンバーが追加されます](#members-added)。 | すべて |
| 削除されたメンバー | membersRemoved | OnTeamsMembersRemovedAsync | [メンバーが削除されます](#members-removed)。 | すべて |
| チャットの名前が変更されました        | teamRenamed       | OnTeamsTeamRenamedAsync    | [チームの名前が変更されます](#team-renamed)。       | チーム |
| チームが削除されました        | teamDeleted       | OnTeamsTeamDeletedAsync    | [チームが削除されます](#team-deleted)。       | チーム |
| チームがアーカイブされました        | teamArchived       | OnTeamsTeamArchivedAsync    | [チームはアーカイブされます](#team-archived)。       | チーム |
| チームのアーカイブが解除されました        | teamUnarchived       | OnTeamsTeamUnarchivedAsync    | [チームのアーカイブが解除されます](#team-unarchived)。       | チーム |
| 復元されたチーム        | teamRestored      | OnTeamsTeamRestoredAsync    | [チームが復元される](#team-restored)       | チーム |

### <a name="channel-created"></a>チャネルを作成しました

イベントは `channelCreated` 、ボットがインストールされているチームで新しいチャネルが作成されるたびにボットに送信されます。

次のコードは、チャネル作成イベントの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelCreatedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Created', `${channelInfo.name} is the Channel created`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "FunDiscussions"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelCreated",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_channel_created(
 self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(
   f"The new channel is {channel_info.name}. The channel id is {channel_info.id}"
  )
 )
```

---

### <a name="channel-renamed"></a>チャネルの名前が変更されました

このイベントは `channelRenamed` 、ボットがインストールされているチームでチャネルの名前が変更されるたびにボットに送信されます。

次のコードは、チャネル名変更イベントの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRenamedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Renamed', `${channelInfo.name} is the new Channel name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "PhotographyUpdates"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelRenamed",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_channel_renamed(
 self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The new channel name is {channel_info.name}")
 )
```

---

### <a name="channel-deleted"></a>チャネルが削除されました

`channelDeleted`ボットがインストールされているチームでチャネルが削除されるたびに、イベントがボットに送信されます。

次のコードは、チャネル削除イベントの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelDeletedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Deleted', `${channelInfo.name} is the Channel deleted`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "PhotographyUpdates"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelDeleted",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_channel_deleted(
 self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The deleted channel is {channel_info.name}")
 )
```

---

### <a name="channel-restored"></a>復元されたチャネル

イベントは `channelRestored` 、ボットが既にインストールされているチームで以前に削除されたチャネルが復元されるたびに、ボットに送信されます。

次のコードは、チャネルが復元されたイベントの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRestoredEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Restored', `${channelInfo.name} is the Channel restored`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "FunDiscussions"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelRestored",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_channel_restored(
 self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(
   f"The restored channel is {channel_info.name}. The channel id is {channel_info.id}"
  )
 )
```

---

### <a name="members-added"></a>メンバーが追加されました

メンバーが追加したイベントは、次のシナリオでボットに送信されます。

1. ボット自体がインストールされ、会話に追加されると

   > チーム コンテキストでは、アクティビティの conversation.id は、アプリのインストール中に `id` ユーザーが選択したチャネル、またはボットがインストールされたチャネルに設定されます。

2. ボットがインストールされている会話にユーザーが追加されたとき

   > イベント ペイロードで受信されたユーザー ID はボットに固有であり、ユーザーを直接メッセージングするなど、将来の使用のためにキャッシュできます。

メンバーが追加したアクティビティ `eventType` は、イベントがチーム コンテキストから送信されたときに設定 `teamMemberAdded` されます。 追加された新しいメンバーがボット自体かユーザーかを確認するには、`Activity``turnContext`. リストにオブジェクトの`MembersAdded`フィールド`Recipient`と`id`同じオブジェクトが`id`含まれている場合、追加されたメンバーはボット、それ以外の場合はユーザーです。 ボットの `id` 形式 `28:<MicrosoftAppId>`は .

> [!TIP]
> [このイベントを`InstallationUpdate`](#installation-update-event)使用して、ボットがいつ会話に追加または削除されるかを判断します。

次のコードは、チーム メンバー追加イベントの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> teamsMembersAdded , TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in teamsMembersAdded)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // Send a message to introduce the bot to the team
            var heroCard = new HeroCard(text: $"The {member.Name} bot has joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersAddedEvent(async (membersAdded: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
                let newMembers: string = '';
                console.log(JSON.stringify(membersAdded));
                membersAdded.forEach((account) => {
                    newMembers += account.id + ' ';
                });
                const name = !teamInfo ? 'not in team' : teamInfo.name;
                const card = CardFactory.heroCard('Account Added', `${newMembers} joined ${name}.`);
                const message = MessageFactory.attachment(card);
                await turnContext.sendActivity(message);
                await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

ボットがチームに追加されたときにボットが受信するメッセージ。

> [!NOTE]
> このペイロードでは、 `conversation.id` `channelData.settings.selectedChannel.id` アプリのインストール中またはインストールのトリガー元としてユーザーが選択したチャネルの ID になります。

```json
{
    "type": "conversationUpdate",
    "membersAdded": [
        {
            "id": "28:608cacfd-1cea-40c9-b678-4b93e69bb72b"
        }
    ],
    "timestamp": "2021-12-07T22:34:56.534Z",
    "id": "f:0b9079f4-d4d3-3d8e-b883-798298053c7e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "29:1ljv6N86roXr5pjPrCJVIz6xHh5QxjI....",
        "aadObjectId": "eddfa9d4-346e-4cce-a18f-fa6261ad776b"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "tenantId": "b28fdbfd-2b78-4f93-b0f8-8881793f0f8f",
        "id": "19:0b7f32667e064dd9b25d7969801541f4@thread.tacv2",
        "name": "2021 Test Channel"
    },
    "recipient": {
        "id": "28:608cacfd-1cea-40c9-b678-4b93e69bb72b",
        "name": "Test Bot"
    },
    "channelData": {
        "settings": {
            "selectedChannel": {
                "id": "19:0b7f32667e064dd9b25d7969801541f4@thread.tacv2"
            }
        },
        "team": {
            "aadGroupId": "f3ec8cd2-e704-4344-8c47-9a3a21d683c0",
            "name": "TestTeam2022",
            "id": "19:zFLSDFWsesfzcmKArqKJ-65aOXJz@sgf462H2wz41@thread.tacv2"
        },
        "eventType": "teamMemberAdded",
        "tenant": {
            "id": "b28fdbfd-2b78-4f93-b0f8-8881793f0f8f"
        }
    }
}
```

ボットが 1 対 1 のチャットに追加されたときにボットが受信するメッセージ。

```json
{
  "membersAdded": [{
      "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
    },
    {
      "id": "29:<userID>",
      "aadObjectId": "***"
    }
  ],
  "type": "conversationUpdate",
  "timestamp": "2019-04-23T10:17:44.349Z",
  "id": "f:5f85c2ad",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:<USERID>",
    "aadObjectId": "***"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "***"
  },
  "recipient": {
    "id": "28:<BOT ID>",
    "name": "<BOT NAME>"
  },
  "channelData": {
    "tenant": {
      "id": "<TENANT ID>"
    }
  }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_members_added(
 self, teams_members_added: [TeamsChannelAccount], turn_context: TurnContext
):
 for member in teams_members_added:
  await turn_context.send_activity(
   MessageFactory.text(f"Welcome your new team member {member.id}")
  )
 return
```

---

### <a name="members-removed"></a>削除されたメンバー

メンバーが削除されたイベントは、次のシナリオでボットに送信されます。

1. ボット自体がアンインストールされ、会話から削除されるとします。
2. ボットがインストールされている会話からユーザーが削除されたとき。

メンバーが削除したアクティビティ `eventType` は、イベントがチーム コンテキストから送信されたときに設定 `teamMemberRemoved` されます。 新たに削除されたメンバーがボット自身なのかユーザーなのかを判断するには、`turnContext` のうちの `Activity` オブジェクトを確認します。 リストにオブジェクトの`MembersRemoved`フィールド`Recipient`と`id`同じオブジェクトが`id`含まれている場合、追加されたメンバーはボット、それ以外の場合はユーザーです。 ボットの ID は 、 `28:<MicrosoftAppId>`.

> [!NOTE]
> ユーザーがテナントから完全に削除されると、`membersRemoved conversationUpdate` イベントがトリガーされます。

次のコードは、チーム メンバー削除イベントの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersRemovedAsync(IList<ChannelAccount> membersRemoved, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in membersRemoved)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // The bot was removed
            // You should clear any cached data you have for this team
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} was removed from {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersRemovedEvent(async (membersRemoved: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            let removedMembers: string = '';
            console.log(JSON.stringify(membersRemoved));
            membersRemoved.forEach((account) => {
                removedMembers += account.id + ' ';
            });
            const name = !teamInfo ? 'not in team' : teamInfo.name;
            const card = CardFactory.heroCard('Account Removed', `${removedMembers} removed from ${teamInfo.name}.`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

次のペイロード例の `channelData` オブジェクトは、グループ チャットではなくチームへのメンバー追加、または新しい 1 対 1 の会話の開始に基づくものです。

```json
{
    "membersRemoved": [
        {
            "id": "29:1_LCi5Up14pAy65yZuaJzG1uIT7ujYhjjSTsUNqjORsZHjLHKiQIBJa4cX2XsAsRoaY7va2w6ZymA9-1VtSY_g"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:37:06.96Z",
    "localTimestamp": "2017-02-23T12:37:06.96-07:00",
    "id": "f:d8a6a4aa",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient":
    {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberRemoved",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_members_removed(
 self, teams_members_removed: [TeamsChannelAccount], turn_context: TurnContext
):
 for member in teams_members_removed:
  await turn_context.send_activity(
   MessageFactory.text(f"Say goodbye to {member.id}")
  )
 return
```

---

### <a name="team-renamed"></a>チャットの名前が変更されました

チームの名前が変更されると、そのボットは通知を受け取ります。 ボットは、`channelData` オブジェクト内に `eventType.teamRenamed` を含む `conversationUpdate` イベントを受信します。

次のコードは、チーム名変更イベントの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamRenamedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team Renamed', `${teamInfo.name} is the new Team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "New Team Name"
        },
        "eventType": "teamRenamed",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_renamed(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The new team name is {team_info.name}")
 )
```

---

### <a name="team-deleted"></a>チームが削除されました

チームが削除されると、ボットは通知を受け取ります。 ボットは、`channelData` オブジェクト内に `eventType.teamDeleted` を含む `conversationUpdate` イベントを受信します。

次のコードは、チーム削除イベントの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamDeletedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            //handle delete event
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "Team Name"
        },
        "eventType": "teamDeleted",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_deleted(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 //handle delete event
 )
```

---

### <a name="team-restored"></a>復元されたチーム

ボットは、チームが削除された後に復元されると通知を受け取ります。 ボットは、`channelData` オブジェクト内に `eventType.teamrestored` を含む `conversationUpdate` イベントを受信します。

次のコードは、チーム復元イベントの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamrestoredEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team restored', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "Team Name"
        },
        "eventType": "teamrestored",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_restored(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The team name is {team_info.name}")
 )
```

---

### <a name="team-archived"></a>チームがアーカイブされました

チームがインストールされてアーカイブされると、ボットは通知を受け取ります。 ボットは、`channelData` オブジェクト内に `eventType.teamarchived` を含む `conversationUpdate` イベントを受信します。

次のコードは、チーム アーカイブ イベントの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamArchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "Team Name"
        },
        "eventType": "teamArchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_archived(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The team name is {team_info.name}")
 )
```

---

### <a name="team-unarchived"></a>チームのアーカイブが解除されました

チームがインストールされてアーカイブが解除されると、ボットは通知を受け取ります。 ボットは、`channelData` オブジェクト内に `eventType.teamUnarchived` を含む `conversationUpdate` イベントを受信します。

次のコードは、チーム アーカイブ解除イベントの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamUnarchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "Team Name"
        },
        "eventType": "teamUnarchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_unarchived(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The team name is {team_info.name}")
 )
```

---

会話の更新イベントを操作したので、メッセージに対するさまざまな反応に対して発生するメッセージリアクション イベントを理解できます。

## <a name="message-reaction-events"></a>メッセージ リアクション イベント

このイベントは `messageReaction` 、ユーザーがボットによって送信されたメッセージに対する反応を追加または削除したときに送信されます。 `replyToId` にはメッセージの ID が、`Type` にはテキスト形式のリアクションの種類が含まれます。 リアクションの種類には、怒り、ハート、笑い、いいね!、悲しい、驚きなどがあります。 このイベントには、元のメッセージの内容は含まれません。 メッセージに対する処理のリアクションがボットにとって重要な場合は、メッセージを送信するときにメッセージを格納する必要があります。 次の表に、イベントの種類とペイロード オブジェクトの詳細を示します。

| EventType       | ペイロード オブジェクト   | 説明                                                             | 範囲 |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| messageReaction | reactionsAdded   | [ボット メッセージに追加されたリアクション](#reactions-added-to-bot-message)。           | すべて   |
| messageReaction | reactionsRemoved | [ボット メッセージからのリアクションの削除](#reactions-removed-from-bot-message)。 | すべて |

### <a name="reactions-added-to-bot-message"></a>ボット メッセージに追加されたリアクション

次のコードは、ボット メッセージに対するリアクションの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnReactionsAddedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You reacted with '{reaction.Type}' to the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

<!-- Verify -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsAdded(async (context, next) => {
           const reactionsAdded = context.activity.reactionsAdded;
            if (reactionsAdded && reactionsAdded.length > 0) {
                for (let i = 0; i < reactionsAdded.length; i++) {
                    const reaction = reactionsAdded[i];
                    const newReaction = `You reacted with '${reaction.type}' to the following message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "reactionsAdded": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_reactions_added(
 self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
 for reaction in message_reactions:
  activity = await self._log.find(turn_context.activity.reply_to_id)
  if not activity:
   await self._send_message_and_log_activity_id(
    turn_context,
    f"Activity {turn_context.activity.reply_to_id} not found in log",
   )
  else:
   await self._send_message_and_log_activity_id(
    turn_context,
    f"You added '{reaction.type}' regarding '{activity.text}'",
   )
 return
```

---

### <a name="reactions-removed-from-bot-message"></a>ボット メッセージからのリアクションの削除

次のコードは、ボット メッセージから削除されたリアクションの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnReactionsRemovedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You removed the reaction '{reaction.Type}' from the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

<!-- Verify -->

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsRemoved(async(context,next)=>{
            const reactionsRemoved = context.activity.reactionsRemoved;
            if (reactionsRemoved && reactionsRemoved.length > 0) {
                for (let i = 0; i < reactionsRemoved.length; i++) {
                    const reaction = reactionsRemoved[i];
                    const newReaction = `You removed the reaction '${reaction.type}' from the message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "reactionsRemoved": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_reactions_removed(
 self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
 for reaction in message_reactions:
  activity = await self._log.find(turn_context.activity.reply_to_id)
  if not activity:
   await self._send_message_and_log_activity_id(
    turn_context,
    f"Activity {turn_context.activity.reply_to_id} not found in log",
   )
  else:
   await self._send_message_and_log_activity_id(
    turn_context,
    f"You removed '{reaction.type}' regarding '{activity.text}'",
   )
 return
```

---

## <a name="installation-update-event"></a>インストール更新イベント

ボットを会話スレッドにインストールすると、ボットは `installationUpdate` イベントを受け取ります。 スレッドからボットをアンインストールすると、イベントもトリガーされます。 ボットをインストールすると、イベント内の **アクション** フィールドが *追加* に設定され、ボットがアンインストールされると、**アクション** フィールドが *削除* されるように設定されます。

> [!NOTE]
> アプリケーションをアップグレードしてからボットを追加または削除すると、アクションによって `installationUpdate` イベントもトリガーされます。 **アクション** フィールドは、ボットを追加する場合は *追加してアップグレード* に設定され、ボットを削除する場合は *削除してアップグレード* に設定されます。

### <a name="install-update-event"></a>更新イベントのインストール

`installationUpdate` イベントを使用して、インストールでボットから入門メッセージを送信します。 このイベントは、プライバシーとデータ保持の要件を満たすのに役立ちます。 ボットがアンインストールされたときに、ユーザーまたはスレッド データをクリーンアップして削除することもできます。

ボットが `conversationUpdate` チームに追加されたときに送信されるイベントと同様に、イベントの conversation.id は、アプリの `installationUpdate` インストール中にユーザーが選択したチャネルの ID またはインストールが発生したチャネルに設定されます。 ID は、ユーザーがボットを操作するチャネルを表し、ウェルカム メッセージを送信するときにボットが使用する必要があります。 For scenarios where the ID of the General channel is explicitly required, you can get it from `team.id` in `channelData`.

この例では、 `conversation.id` Daves Demo チームの `conversationUpdate` 応答チャネルの ID にアクティビティと `installationUpdate` アクティビティが設定されます。

![選択したチャネルを作成する](~/assets/videos/addteam.gif)

> [!NOTE]
> 選択したチャネル ID は、アプリがチームに `installationUpdate`インストールされたときに送信されるイベントの *追加* にのみ設定されます。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnInstallationUpdateActivityAsync(ITurnContext<IInstallationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var activity = turnContext.Activity;
    if (string.Equals(activity.Action, "Add", StringComparison.InvariantCultureIgnoreCase))
    {
        // TO:DO Installation workflow
    }
    else
    {
        // TO:DO Uninstallation workflow
    }
    return;
}
```

イベントをキャプチャするための代替方法として、シナリオを *追加* または *削除* するための専用ハンドラーを使用することもできます。

```csharp
protected override async Task OnInstallationUpdateAddAsync(ITurnContext<IInstallationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    // TO:DO Installation workflow return;
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
async onInstallationUpdateActivity(context: TurnContext) {
        var activity = context.activity.action;
        if(activity == "Add") {
            await context.sendActivity(MessageFactory.text("Added"));
        }
        else {
            await context.sendActivity(MessageFactory.text("Uninstalled"));
        }
    }
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    {
    "type": "installationUpdate",
    "id": "f:816eb23d-bfa1-afa3-dfeb-d2aa338e9541",
    "timestamp": "2021-11-09T04:47:30.91Z",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1ljv6N86roXr5pjPrCJVIz6xHh5QxjI....",
        "aadObjectId": "eddfa9d4-346e-4cce-a18f-fa6261ad776b"
    },
    "recipient": {
        "id": "28:608cacfd-1cea-40c9-b678-4b93e69bb72b",
        "name": "Test Bot"
    },
    "locale": "en-US",
    "entities": [
        {
            "type": "clientInfo",
            "locale": "en-US"
        }
    ],
    "conversation": {
        "isGroup": true,
        "id": "19:0b7f32667e064dd9b25d7969801541f4@thread.tacv2",
        "name": "2021 Test Channel",
        "conversationType": "channel",
        "tenantId": "b28fdbfd-2b78-4f93-b0f8-8881793f0f8f"
    },
    "channelData": {
        "settings": {
            "selectedChannel": {
                "id": "19:0b7f32667e064dd9b25d7969801541f4@thread.tacv2"
            }
        },
        "channel": {
            "id": "19:0b7f32667e064dd9b25d7969801541f4@thread.tacv2"
        },
        "team": {
            "aadGroupId": "da849743-4259-475f-ae7a-4f4b0fb49943",
            "name": "TestTeam2022",
            "id": "19:zFLSDFWsesfzcmKArqKJ-65aOXJz@sgf462H2wz41@thread.tacv2"
        },
        "tenant": {
            "id": "b28fdbfd-2b78-4f93-b0f8-8881793f0f8f"
        },
        "source": {
            "name": "message"
        }
    },
    "action": "add"
    }
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_installation_update(self, turn_context: TurnContext):
   if turn_context.activity.action == "add":   
       await turn_context.send_activity(MessageFactory.text("Added"))
   else:
       await turn_context.send_activity(MessageFactory.text("Uninstalled"))
```

---

## <a name="uninstall-behavior-for-personal-app-with-bot"></a>ボットを使用した個人用アプリのアンインストール動作

アプリをアンインストールすると、ボットもアンインストールされます。 ユーザーがアプリにメッセージを送信すると、403 応答コードが表示されます。 ボットによって投稿された新しいメッセージには、403 応答コードが表示されます。 個人用スコープ内のボットのアンインストール後の動作と、Teams スコープと groupChat スコープが揃いました。 アプリのアンインストール後にメッセージを送受信することはできません。

:::image type="content" source="../../../assets/images/bots/uninstallbot.png" alt-text="応答コードをアンインストールする"lightbox="../../../assets/images/bots/uninstallbot.png"border="true":::

## <a name="event-handling-for-install-and-uninstall-events"></a>インストールおよびアンインストール イベント向けのイベント ハンドリング

これらのインストール およびアンインストール イベントを使用すると、ボットが Teams から予期しないイベントを受信する際に例外が発生する場合があります。これは、次の場合に発生します。

* Microsoft Bot Framework SDK を使用せずにボットをビルドした結果、ボットが予期しないイベントを受信した場合に例外が発生します。
* Microsoft Bot Framework SDK を使用してボットをビルドし、基本イベント ハンドルをオーバーライドして既定のイベント動作を変更することを選択します。

今後いつでも新しいイベントを追加でき、ボットが受け取り始めるという点を理解しておくことが重要です。 そのため、予期しないイベントを受け取る可能性があることを想定して設計する必要があります。 Bot Framework SDK を使用している場合、ボットは 200 - OK で自動的に応答し、処理を選択しないイベントに対して OK を返します。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **.NET** | **Node.js** | **Python** |
|----------|-----------------|----------|
| 会話ボット | ボットの会話イベントのサンプル コード。 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)  | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [プロアクティブ メッセージを送信する](~/bots/how-to/conversations/send-proactive-messages.md)
