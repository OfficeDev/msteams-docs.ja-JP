---
title: タスク モジュールの送信アクションに応答する
author: surbhigupta
description: プロアクティブ メッセージを使用してメッセージ拡張アクション コマンドからタスク モジュールの送信アクションに応答する方法について説明します。 検索コマンドを定義し、検索に応答します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 472bde652e60a8029bd54c7a1360412ab9710ada
ms.sourcegitcommit: bb15ce26cd65bec90991b703069424ab4b4e1a61
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2022
ms.locfileid: "68772308"
---
# <a name="respond-to-the-task-module-submit-action"></a>タスク モジュールの送信アクションに応答する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

このドキュメントでは、ユーザーのタスク モジュール送信アクションなどのアクション コマンドに対するアプリの応答について説明します。
ユーザーがタスク モジュールを送信すると、Web サービスはコマンド ID とパラメーター値を含む `composeExtension/submitAction` 呼び出しメッセージを受信します。 アプリには、呼び出しに応答する 5 秒があります。  

対応には、以下のオプションがあります。

* 応答なし: 送信アクションを使用して、外部システムでプロセスをトリガーし、ユーザーにはフィードバックを提供しません。 これは、実行時間の長いプロセスに役立ち、フィードバックを代替的に提供します。 たとえば、[プロアクティブ メッセージ](~/bots/how-to/conversations/send-proactive-messages.md)を使用してフィードバックを送信できます。
* [別のタスク モジュール](#respond-with-another-task-module): 複数のステップがある操作の一部として、追加のタスク モジュールで応答します。
* [カードによる応答](#respond-with-a-card-inserted-into-the-compose-message-area): ユーザーが操作したり、メッセージに挿入したりできるカードで応答できます。
* [ボットからのアダプティブ カード](#bot-response-with-adaptive-card): アダプティブ カードを会話に直接挿入します。
* [ユーザーに認証を要求します](~/messaging-extensions/how-to/add-authentication.md)。
* [追加の構成をユーザーに要求します](~/get-started/first-message-extension.md)。

アプリが 5 秒以内に応答しない場合、Teams クライアントは要求を 2 回再試行してから、 **アプリに到達できません** というエラー メッセージを送信します。 タイムアウト後にボットが応答した場合、応答は無視されます。

> [!NOTE]
> ボットが呼び出し要求に応答した後、アプリは実行時間の長いアクションを延期する必要があります。 実行時間の長いアクションの結果は、メッセージとして配信できます。

認証または構成の場合、ユーザーがプロセスを完了すると、元の呼び出しが Web サービスに再送信されます。 次の表は、メッセージ拡張機能の呼び出し場所 `commandContext` に基づいて、使用可能な応答の種類を示しています。

|応答の種類 | 作成 | コマンド バー | メッセージ |
|--------------|:-------------:|:-------------:|:---------:|
|カードの応答 | ✔️ | ✔️ | ✔️ |
|別のタスク モジュール | ✔️ | ✔️ | ✔️ |
|アダプティブ カードを使用したボット | ✔️ | ❌ | ✔️ |
| 応答なし | ✔️ | ✔️ | ✔️ |

> [!NOTE]
>
> * ME カードを通して **Action.Submit** を選択すると、値は通常のペイロードと等しくなる **composeExtension** という名前の呼び出しアクティビティが送信されます。
> * 会話を通して **Action.Submit** を選択すると、値は通常のペイロードと等しくなる **onCardButtonClicked** という名前のメッセージ アクティビティを受け取ります。

アプリに会話ボットが含まれている場合は、会話にボットをインストールし、タスク モジュールを読み込みます。 ボットは、タスク モジュールの追加のコンテキストを取得するのに役立ちます。 会話型ボットをインストールするには、「[会話型ボットのインストールを要求する](create-task-module.md#request-to-install-your-conversational-bot)」を参照してください。

## <a name="the-submitaction-invoke-event"></a>submitAction 呼び出しイベント

呼び出しメッセージを受信する例を次に示します。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

これは、受信する JSON オブジェクトの例です。 この `commandContext` パラメーターは、メッセージ拡張機能がトリガーされた場所を示します。 `data` オブジェクトには、パラメーターとしてフォーム上のフィールドと、ユーザーが送信した値が含まれます。 JSON オブジェクトは、最も関連性の高いフィールドを強調表示します。

```json
{
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith",
  "serviceUrl": "https://smba.trafficmanager.net/amer/",
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "id": "submitButton",
      "formField1": "formField1_value",
      "formField2": "formField2_value",
      "formField3": "formField3_value"
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  }
}
```

* * *

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>メッセージ作成領域にカードを挿入して応答する

`composeExtension/submitAction` の要求に応答する最も一般的な方法は、作成メッセージ領域にカードを挿入することです。 ユーザーは、カードを会話に送信します。 カードの使用に関する詳細については、「[カードとカード アクション](~/task-modules-and-cards/cards/cards-actions.md)」を参照してください。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var createCardData = ((JObject)action.Data).ToObject<CreateCardData>();
var card = new HeroCard
{
     Title = createCardData.Title,
     Subtitle = createCardData.Subtitle,
     Text = createCardData.Text,
};
    var attachments = new List<MessagingExtensionAttachment>();
    attachments.Add(new MessagingExtensionAttachment
    {
        Content = card,
        ContentType = HeroCard.ContentType,
        Preview = card.ToAttachment(),
    });
    response.ComposeExtension.Attachments = attachments;
    return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const data = action.data;
    const heroCard = CardFactory.heroCard(data.title, data.text);
    heroCard.content.subtitle = data.subTitle;
    const attachment = { contentType: heroCard.contentType, content: heroCard.content, preview: heroCard };

    return {
      composeExtension: {
        type: 'result',
        attachmentLayout: 'list',
        attachments: [
          attachment
        ]
      }
    }
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "composeExtension": {
    "attachmentLayout": "list",
    "type": "result",
    "attachments": [
      {
        "preview": {
          "contentType": "application/vnd.microsoft.card.hero",
          "content": {
            "title": "formField1_value",
            "subtitle": "formField2_value",
            "text": "formField3_value"
          }
        },
        "contentType": "application/vnd.microsoft.card.hero",
        "content": {
          "title": "formField1_value",
          "subtitle": "formField2_value",
          "text": "formField3_value"
        }
      }
    ]
  }
}
```

* * *

## <a name="respond-with-another-task-module"></a>別のタスク モジュールで応答する

追加のタスク モジュールを使用して `submitAction` イベントに応答するように選択できます。 これは、次のことを行う必要がある場合に便利です。

* 大量の情報を収集する。
* ユーザー入力に基づいて情報コレクションを動的に変更する。
* ユーザーが送信した情報を検証し、問題が発生した場合は、エラー メッセージでフォームを再送信します。

対応方法は、[ としての最初の`fetchTask`イベント](~/messaging-extensions/how-to/action-commands/create-task-module.md)への対応と同じです。 Bot Framework SDK を使用している場合は、両方の送信アクションに対して同じイベント トリガーが発生します。 これを機能させるには、正しい応答を決定するロジックを追加する必要があります。

## <a name="bot-response-with-adaptive-card"></a>アダプティブ カードを使用したボットの応答

> [!NOTE]
> アダプティブ カードを使用してボットの応答を取得する前提条件は、`bot` オブジェクトをアプリ マニフェストに追加し、ボットに必要なスコープを定義する必要があるということです。 ボットのメッセージ拡張機能と同じ ID を使用します。

また、ボットを使用してアダプティブ カードを含むメッセージをチャネルに挿入することで、`submitAction` に応答することもできます。 ユーザーは、メッセージを送信する前にプレビューできます。 これは、アダプティブ カード応答を作成する前にユーザーから情報を収集するシナリオや、他のユーザーが対話した後にカードを更新する場合に便利です。

次のシナリオは、アプリ Polly がチャネル会話に構成手順を含めずに投票を構成する方法を示しています。

投票を構成するには、以下の操作を行います。

1. ユーザーは、タスク モジュールを呼び出すメッセージ拡張機能を選択します。
1. ユーザーは、タスク モジュールを使用して投票を構成します。
1. タスク モジュールを送信した後、アプリは提供された情報を使用してアダプティブ カードとして投票を構築し、クライアントに `botMessagePreview` 応答として送信します。
1. その後、ユーザーは、ボットがチャネルに挿入する前に、アダプティブ カード メッセージをプレビューできます。 アプリがチャネルのメンバーでない場合は、 を選択 `Send` して追加します。

    > [!NOTE]
    >
    > * ユーザーは `Edit` にメッセージを選択して、元のタスク モジュールに返すこともできます。
    > * アダプティブ カードとの対話では、メッセージの送信前に変更されます。
    >
1. ユーザーが を選択 `Send`すると、ボットはチャネルにメッセージを投稿します。

## <a name="respond-to-initial-submit-action"></a>最初の送信アクションに応答する

タスク モジュールは、ボットがチャネルに送信するカードのプレビューを使用して、最初の `composeExtension/submitAction` メッセージに応答する必要があります。 ユーザーは送信前にカードを確認し、ボットが既にインストールされている場合は、会話にボットをインストールしてみてください。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic createCardData = ((JObject) action.Data).ToObject(typeof(JObject));
  var response = new MessagingExtensionActionResponse
  {
    ComposeExtension = new MessagingExtensionResult
    {
      Type = "botMessagePreview",
      ActivityPreview = MessageFactory.Attachment(new Attachment
      {
        Content = new AdaptiveCard("1.0")
        {
          Body = new List<AdaptiveElement>()
          {
            new AdaptiveTextBlock() { Text = "FormField1 value was:", Size = AdaptiveTextSize.Large },
            new AdaptiveTextBlock() { Text = Data["FormField1"] as string }
          },
          Height = AdaptiveHeight.Auto,
          Actions = new List<AdaptiveAction>()
          {
            new AdaptiveSubmitAction
            {
              Type = AdaptiveSubmitAction.TypeName,
              Title = "Submit",
              Data = new JObject { { "submitLocation", "messagingExtensionFetchTask" } },
            },
          }
        },
        ContentType = AdaptiveCard.ContentType
      }) as Activity
    }
  };

  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const submittedData = action.data;
    const adaptiveCard = CardFactory.adaptiveCard({
      actions: [
        { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
      ],
      body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submittedData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
        {
          choices: [
            { title: submittedData.Option1, value: submittedData.Option1 },
            { title: submittedData.Option2, value: submittedData.Option2 },
            { title: submittedData.Option3, value: submittedData.Option3 }
          ],
          id: 'Choices',
          isMultiSelect: submittedData.MultiSelect,
          style: 'expanded',
          type: 'Input.ChoiceSet'
        }
      ],
      type: 'AdaptiveCard',
      version: '1.0'
    });
    return {
      composeExtension: {
        activityPreview: MessageFactory.attachment(adaptiveCard, null, null, InputHints.ExpectingInput),
        type: 'botMessagePreview'
      }
    };
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

> [!NOTE]
>
> * `activityPreview` には、1 つのアダプティブ カード添付ファイルを含む `message` アクティビティが含まれている必要があります。 `<< Card Payload >>` の値は、送信するカードのプレースホルダーです。

```json
{
  "composeExtension": {
    "type": "botMessagePreview",
    "activityPreview": {
      "type": "message",
      "attachments":  [
        {
          "contentType": "application/vnd.microsoft.card.adaptive",
          "content": << Card Payload >>
        }
      ]
    }
  }
}
```

* * *

### <a name="the-botmessagepreview-send-and-edit-events"></a>botMessagePreview によるイベントの送信と編集

メッセージ拡張機能は、`composeExtension/submitAction` 呼び出しの 2 つの新しい種類である `value.botMessagePreviewAction = "send"` と `value.botMessagePreviewAction = "edit"` に応答する必要があります。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewEditAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionBotMessagePreviewEdit(context, action) {

    //handle the event
  }
  
  handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {

    //handle the event
  }
}

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "edit | send",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

* * *

### <a name="respond-to-botmessagepreview-edit"></a>botMessagePreview の編集に応答する

**[編集]** を選択してユーザーが送信する前にカードを編集した場合は、`value.botMessagePreviewAction = edit` を含む `composeExtension/submitAction` の呼び出しを受信します。 対話を開始した最初の `composeExtension/fetchTask` 呼び出しに応答して、送信したタスク モジュールを返すことで応答します。 これにより、ユーザーは元の情報を再入力してプロセスを開始できます。 ユーザーが最初からすべての情報を入力する必要がないように、使用可能な情報を使用してタスク モジュールを更新します。
最初の `fetchTask` イベントへの応答に関する詳細については、「[最初の `fetchTask` イベントに応答する](~/messaging-extensions/how-to/action-commands/create-task-module.md)」を参照してください。

### <a name="respond-to-botmessagepreview-send"></a>botMessagePreview 送信に応答する

ユーザーが **[送信]** を選択すると、`value.botMessagePreviewAction = send` を含む `composeExtension/submitAction` の呼び出しを受信します。 Web サービスは、アダプティブ カードを使用したプロアクティブ メッセージを作成して会話に送信し、呼び出しに返信する必要があります。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var activityPreview = action.BotActivityPreview[0];
  var attachmentContent = activityPreview.Attachments[0].Content;
  var previewedCard = JsonConvert.DeserializeObject<AdaptiveCard>(attachmentContent.ToString(),
          new JsonSerializerSettings { NullValueHandling = NullValueHandling.Ignore });
  
  previewedCard.Version = "1.0";

  var responseActivity = Activity.CreateMessageActivity();
  Attachment attachment = new Attachment()
  {
    ContentType = AdaptiveCard.ContentType,
    Content = previewedCard
  };
  responseActivity.Attachments.Add(attachment);
  
  // Attribute the message to the user on whose behalf the bot is posting
  responseActivity.ChannelData = new {
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }
  };
  
  await turnContext.SendActivityAsync(responseActivity);

  return new MessagingExtensionActionResponse();
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {
      // The data has been returned to the bot in the action structure.
      const activityPreview = action.botActivityPreview[0];
      const attachmentContent = activityPreview.attachments[0].content;
      const userText = attachmentContent.body[1].text;
      const choiceSet = attachmentContent.body[3];

      const submitData = {
        MultiSelect: choiceSet.isMultiSelect ? 'true' : 'false',
        Option1: choiceSet.choices[0].title,
        Option2: choiceSet.choices[1].title,
        Option3: choiceSet.choices[2].title,
        Question: userText
      };

      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [
          { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
        ],
        body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submitData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
          {
            choices: [
                { title: submitData.Option1, value: submitData.Option1 },
                { title: submitData.Option2, value: submitData.Option2 },
                { title: submitData.Option3, value: submitData.Option3 }
            ],
            id: 'Choices',
            isMultiSelect: submitData.MultiSelect,
            style: 'expanded',
            type: 'Input.ChoiceSet'
          }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });
      const responseActivity = { type: 'message', attachments: [adaptiveCard], channelData: {
          onBehalfOf: [
              { itemId: 0, mentionType: 'person', mri: context.activity.from.id, displayname: context.activity.from.name }
          ]
      }};

      await context.sendActivity(responseActivity);
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

次のような新しい `composeExtension/submitAction` メッセージを受信します。

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

* * *

### <a name="user-attribution-for-bots-messages"></a>ボット メッセージのユーザー属性

ボットがユーザーに代わってメッセージを送信するシナリオでは、メッセージをそのユーザーに帰属させることでエンゲージメントを高め、より自然な対話フローを示すのに役立ちます。 この機能を使用すると、ボットから送信されたメッセージを、送信先のユーザーに属性付けできます。

次の画像では、左側はユーザー属性のないボットによって送信されたカード メッセージ、右側はユーザー属性のあるボットによって送信されたカードです。

:::image type="content" source="../../../assets/images/messaging-extension/user-attribution-bots.png" alt-text="ユーザー属性ボット":::

チームでユーザー属性を使用するには、Teams に送信される `Activity` ペイロードで `ChannelData` に `OnBehalfOf` メンション エンティティを追加する必要があります。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-1)

```csharp
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }

```

# <a name="json"></a>[JSON](#tab/json-1)

```json
{
    "text": "Hello World!",
    "ChannelData": {
        "OnBehalfOf": [{
            "itemid": 0,
            "mentionType": "person",
            "mri": "29:orgid:89e6508d-6c0f-4ffe-9f6a-b58416d965ae",
            "displayName": "Sowrabh N R S"
        }]
    }
}
```

* * *

#### <a name="details-of--onbehalfof-entity-schema"></a>`OnBehalfOf` エンティティ スキーマの詳細

次のセクションは、`OnBehalfOf` 配列内のエンティティの説明です。

|フィールド|種類|説明|
|:---|:---|:---|
|`itemId`|整数|アイテムの識別について説明します。 その値は `0` にする必要があります。|
|`mentionType`|String|"ユーザー" のメンションについて説明します。|
|`mri`|String|メッセージが送信された代理ユーザーのメッセージ リソース識別子 (MRI)。 メッセージの送信者名は"\<bot name\> 経由の \<user\>" として表示されます。|
|`displayName`|String|ユーザーの名前。 ケース名の解決が利用できない場合にフォールバックとして使用されます。|
  
## <a name="code-sample"></a>コード サンプル

| サンプルの名前           | 説明 | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams メッセージ拡張機能アクション| アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Teams メッセージ拡張機能検索   |  検索コマンドを定義し、検索に応答する方法について説明します。        |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [検索コマンドを定義する](~/messaging-extensions/how-to/search-commands/define-search-command.md)

## <a name="see-also"></a>関連項目

[検索コマンドに応答する](~/messaging-extensions/how-to/search-commands/respond-to-search.md)
