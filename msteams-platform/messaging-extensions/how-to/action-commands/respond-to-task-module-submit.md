---
title: タスク モジュールの送信アクションに応答する
author: clearab
description: メッセージング拡張機能アクション コマンドからタスク モジュール送信アクションに応答する方法について説明します。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: fecc0ace5f767da3764529a9e8a590b37e547bb0
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827943"
---
# <a name="respond-to-the-task-module-submit-action"></a>タスク モジュールの送信アクションに応答する

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

ユーザーがタスク モジュールを送信すると、Web サービスはコマンド ID とパラメーター値を含む呼び出し `composeExtension/submitAction` メッセージを受信します。 アプリは呼び出しに応答するために **5** 秒を持っています。それ以外の場合、ユーザーはエラー メッセージを受け取りますアプリに到達できず、呼び出しに対する返信は Teams クライアントによって無視されます。

応答するオプションは次のとおりです。

* 応答なし - 送信アクションを使用して外部システムのプロセスをトリガーし、ユーザーにフィードバックを提供しない選択できます。 これは長時間実行されるプロセスに役立ちます。また、別の方法 (プロアクティブ メッセージなど) でフィードバックを [提供する場合があります](~/bots/how-to/conversations/send-proactive-messages.md)。
* [別のタスク モジュール](#respond-with-another-task-module) - 複数ステップの操作の一環として、追加のタスク モジュールで応答できます。
* [カードの](#respond-with-a-card-inserted-into-the-compose-message-area) 応答 - ユーザーがメッセージを操作したり、メッセージに挿入したりできるカードで応答できます。
* [ボットからのアダプティブ カード](#bot-response-with-adaptive-card) - アダプティブ カードを会話に直接挿入します。
* [ユーザーの認証を要求する](~/messaging-extensions/how-to/add-authentication.md)
* [ユーザーに追加の構成の提供を要求する](~/messaging-extensions/how-to/add-configuration-page.md)

認証または構成の場合、ユーザーがフローを完了すると、元の呼び出しが Web サービスに再送信されます。 次の表に、メッセージング拡張機能の呼び出し場所に基づいて使用できる応答 `commandContext` の種類を示します。 

|応答の種類 | compose | コマンド バー | message |
|--------------|:-------------:|:-------------:|:---------:|
|カードの応答 | x | x | x |
|別のタスク モジュール | x | x | x |
|アダプティブ カードを使用したボット | x |  | x |
| 応答なし | x | x | x |

> [!NOTE]
> * **[Action.Submit** through ME] カードを選択すると、その値が通常のペイロードと等しい名前 **の composeExtension** を持つ呼び出しアクティビティが送信されます。
> * **[Action.Submit** through conversation] を選択すると、onCardButtonClicked という名前のメッセージ アクティビティが表示され、値は通常のペイロードと等しくなります。 

## <a name="the-submitaction-invoke-event"></a>submitAction 呼び出しイベント

呼び出しメッセージを受信する例は次のとおりです。

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

これは、受信する JSON オブジェクトの例です。 パラメーター `commandContext` は、メッセージング拡張機能がトリガーされた場所を示します。 オブジェクト `data` には、パラメーターとしてフォームのフィールドと、ユーザーが送信した値が含まれます。 ここでの JSON オブジェクトは、最も関連性の高いフィールドを強調表示するために短縮されます。

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>作成メッセージ領域にカードを挿入して応答する

要求に応答する最も一般的な方法は、作成メッセージ領域にカード `composeExtension/submitAction` を挿入する方法です。 その後、ユーザーは会話にカードを送信できます。 カードの使用の詳細については、「カードと [カードのアクション」を参照してください](~/task-modules-and-cards/cards/cards-actions.md)。

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

追加のタスク モジュールを使用して `submitAction` イベントに応答できます。 これは、次の場合に役立ちます。

* 大量の情報を収集する必要があります。
* ユーザー入力に基づいて収集する情報を動的に変更する必要がある場合
* ユーザーが送信した情報を検証し、何か問題が発生した場合にエラー メッセージを表示してフォームを再送信する必要がある場合。 

応答のメソッドは、最初のイベント [に応答する方法と同 `fetchTask` じです](~/messaging-extensions/how-to/action-commands/create-task-module.md)。 Bot Framework SDK を使用している場合は、両方の送信アクションに対して同じイベント トリガーが発生します。 つまり、正しい応答を決定するロジックを追加する必要があります。

## <a name="bot-response-with-adaptive-card"></a>アダプティブ カードを使用したボットの応答

>[!Note]
>このフローでは、アプリ マニフェストにオブジェクトを追加し、ボットに必要なスコープを定義 `bot` する必要があります。 ボットのメッセージング拡張機能と同じ ID を使用します。

送信アクションに応答するには、アダプティブ カードを含むメッセージをボットを使用してチャネルに挿入します。 ユーザーは、メッセージを送信する前にプレビューし、メッセージを編集したり操作したりすることもできます。 これは、アダプティブ カード応答を作成する前にユーザーから情報を収集するシナリオや、ユーザーがカードを操作した後にカードを更新する場合に非常に役立ちます。 次のシナリオは、アプリ Polly がチャネル会話に構成手順を含めずに、このフローを使用してポーリングを構成する方法を示しています。

1. ユーザーがメッセージング拡張機能を選択して、タスク モジュールをトリガーします。
2. ユーザーは、タスク モジュールを使用してポーリングを構成します。
3. タスク モジュールを送信した後、アプリは提供された情報を使用して、アダプティブ カードとしてポーリングを構築し、それをクライアントに応答 `botMessagePreview` として送信します。
4. その後、ボットがチャネルに挿入する前に、アダプティブ カード メッセージをプレビューできます。 アプリがチャネルのメンバーではない場合は、選択すると追加 `Send` されます。
   1. ユーザーはメッセージを選択して、元のタスク モジュール `Edit` に返します。
5. アダプティブ カードを操作すると、メッセージを送信する前に変更されます。
6. ユーザーがボットを選択 `Send` すると、メッセージがチャネルに投稿されます。

### <a name="respond-to-initial-submit-action"></a>最初の送信アクションに応答する

このフローを有効にするには、ボットがチャネルに送信するカードのプレビューを使用して、タスク モジュールが最初のメッセージ `composeExtension/submitAction` に応答する必要があります。 これにより、ユーザーは送信する前にカードを確認し、ボットがインストールされていない場合は会話にボットをインストールする機会も与えます。

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

>[!Note]
>アダプティブ `activityPreview` カードの添付ファイル `message` が 1 つのアクティビティを含む必要があります。 この `<< Card Payload >>` 値は、送信するカードのプレースホルダーです。

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

### <a name="the-botmessagepreview-send-and-edit-events"></a>botMessagePreview 送信イベントと編集イベント

メッセージ拡張機能は、2 つの新しい種類の呼び出しに今すぐ応答する `composeExtension/submitAction` 必要があります。where と `value.botMessagePreviewAction = "send"` `value.botMessagePreviewAction = "edit"` .

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

### <a name="respond-to-botmessagepreview-edit"></a>botMessagePreview 編集に応答する

ユーザーが [編集] ボタンを選択して送信する前にカードを編集すると、で呼び出しを `composeExtension/submitAction` 受け取る `value.botMessagePreviewAction = edit` 。 通常、対話を開始した最初の呼び出しに応答して送信したタスク モジュール `composeExtension/fetchTask` を返して応答する必要があります。 これにより、ユーザーは元の情報を再入力してプロセスを開始できます。 使用可能な情報を使用して、ユーザーがすべての情報を最初から入力する必要が生じないので、タスク モジュールに事前入力します。

「 [初期イベントへの応答」を `fetchTask` 参照してください](~/messaging-extensions/how-to/action-commands/create-task-module.md)。

### <a name="respond-to-botmessagepreview-send"></a>botMessagePreview 送信に応答する

ユーザーが [送信] ボタンを **選択すると** 、呼び出しが `composeExtension/submitAction` 表示されます `value.botMessagePreviewAction = send` 。 Web サービスでは、アダプティブ カードを含むプロアクティブ メッセージを作成して会話に送信し、呼び出しに返信する必要があります。

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

次のような新しい `composeExtension/submitAction` メッセージが表示されます。

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

ボットがユーザーに代わってメッセージを送信するシナリオでは、メッセージをそのユーザーに帰属すると、エンゲージメントに役立ち、より自然な対話フローを紹介できます。 この機能を使用すると、ボットから送信されたユーザーにメッセージを属性付けできます。

次の図では、左側はユーザー属性なしでボットから送信されたカードメッセージで、右側はユーザー属性を持つボット *によって送信された* カードです。

![スクリーンショット](../../../assets/images/messaging-extension/user-attribution-bots.png)

Teams でユーザー属性を使用するには、Teams に送信されるペイロードにメンション `OnBehalfOf` `ChannelData` `Activity` エンティティを追加する必要があります。

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

次のセクションでは、Array のエンティティの `OnBehalfOf` 説明を示します。

#### <a name="details-of--onbehalfof-entity-schema"></a>エンティティ スキーマ  `OnBehalfOf` の詳細

|Field|種類|説明|
|:---|:---|:---|
|`itemId`|整数|0 である必要があります|
|`mentionType`|文字列|"人" である必要があります|
|`mri`|文字列|メッセージが送信されたユーザーのメッセージ リソース識別子 (MRI)。 メッセージ送信者名は "via" として \<user\> 表示 \<bot name\> されます。|
|`displayName`|文字列|ユーザーの名前。 名前解決が使用できない場合にフォールバックとして使用されます。|
  
## <a name="next-steps"></a>次の手順

検索コマンドの追加

* [検索コマンドを定義する](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
