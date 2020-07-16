---
title: Microsoft Teams の仮想アシスタント
description: Microsoft Teams で使用する仮想アシスタントのボットとスキルを作成する方法
keywords: teams 仮想アシスタントの bot
ms.openlocfilehash: 0bb1ad832fd33675e607874fcc50f20ffbb96943
ms.sourcegitcommit: 26b7404142706290810064f8216abaa1c262d1e5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "45146023"
---
# <a name="virtual-assistant-for-microsoft-teams"></a>Microsoft Teams の仮想アシスタント

仮想アシスタントは、ユーザーの操作、組織のブランド化、必要なデータのフルコントロールを維持しながら、強力な会話ソリューションを作成できる、Microsoft のオープンソーステンプレートです。 [仮想アシスタントコアテンプレート](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template)は基本的なビルディングブロックであり、[ボット Framework SDK](https://github.com/microsoft/botframework-sdk)、[言語の理解 (LUIS)](https://www.luis.ai/)、 [qna](https://www.qnamaker.ai/)の開発者、スキルの登録、リンクされたアカウント、基本会話など、エンドユーザーにシームレスな対話とエクスペリエンスの範囲を提供する基本的な機能を含む、仮想アシスタントの構築に必要な Microsoft テクノロジを統合したものです。 さらに、テンプレート機能には、再利用可能な会話[スキル](https://microsoft.github.io/botframework-solutions/overview/skills)の豊富な例も含まれています。  個々のスキルを仮想アシスタントソリューションに統合して、複数のシナリオを有効にすることができます。 Bot フレームワーク SDK を使用すると、スキルがソースコードの形式で表示され、必要に応じてカスタマイズおよび拡張することができます。 [Bot フレームワークのスキル](https://microsoft.github.io/botframework-solutions/overview/skills/)を参照してください。

![仮想アシスタントの概要図](../assets/images/bots/virtual-assistant/overview.png)

テキストメッセージアクティビティは、[ディスパッチ](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs)モデルを使用して仮想アシスタントコアによって関連付けられたスキルにルーティングされます。 

## <a name="implementation-considerations"></a>実装に関する考慮事項

仮想アシスタントを追加するかどうかの決定には、組織ごとにさまざまな式を含めることができます。 組織の仮想アシスタントの実装をサポートする要因を次に示します。

- 中央チームは、すべての従業員エクスペリエンスを管理し、新しいスキルの追加など、中核となるエクスペリエンスの更新プログラムを管理する機能を備えています。
- 複数のアプリケーションが複数のビジネス機能にわたって存在するか、または将来の増加が予想されます。
- 既存のアプリケーションは、組織が所有するカスタマイズが可能であり、仮想アシスタントのスキルに変換することができます。
- 中央従業員エクスペリエンスチームは、既存のアプリにカスタマイズを反映して、既存のアプリケーションを仮想アシスタントエクスペリエンスのスキルとして統合するために必要なガイダンスを提供することができます。

![中央チームがアシスタントを管理し、ビジネス機能チームがスキルを貢献](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Teams に特化した仮想アシスタントを作成する

Microsoft は、仮想アシスタントとスキルを構築するための[Visual Studio テンプレート](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate)を公開しています。 Visual Studio テンプレートを使用すると、アクションを備えた限られたリッチカードのサポートを提供して、テキストベースの操作で提供される仮想アシスタントを作成できます。 Visual Studio の基本テンプレートが拡張され、Microsoft Teams のプラットフォーム機能と power Teams アプリのエクスペリエンスが追加されました。 豊富なアダプティブカード、タスクモジュール、teams/グループチャット、メッセージング拡張機能のサポートが含まれています。 「[チュートリアル: 仮想アシスタントを Microsoft Teams に拡張する](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/) *」も参照して*ください。

![仮想アシスタントソリューションの高レベルの図](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>仮想アシスタントに適応カードを追加する

要求を適切にディスパッチするには、仮想アシスタントが正しい LUIS モデルとそれに関連するスキルを特定する必要があります。 ただし、これらは固定された定義済みのキーワードであり、ユーザーからの utterances ではないため、カードアクションの処理に対しては、そのスキルに関連付けられている LUIS モデルを使用することはできないため、ディスパッチメカニズムを使用することはできません。

このことは、スキル情報をカードアクションペイロードに埋め込むことによって解決されました。 各スキルは `skillId` 、カードアクションのフィールドに埋め込む必要があり `value` ます。 各カードアクションアクティビティに関連するスキル情報が確実に伝達され、仮想アシスタントがこの情報をディスパッチに利用できるようにするには、これが最善の方法です。

カードアクションデータサンプルを次に示します。 コンストラクターに提供することで、 `skillId` スキル情報がカードのアクションに常に表示されるようになります。

```csharp
    public class CardActionData
    {
        public CardActionData(string skillId)
        {
            this.SkillId = skillId;
        }

        [JsonProperty("skillId")]
        public string SkillId { get; set; }
    }

    ...
    var button = new CardAction
    {
        Type = ActionTypes.MessageBack,
        Title = "Card action button",
        Text = "card action button text",
        Value = new CardActionData(<SkillId>),
    };
```

次に、 `SkillCardActionData` `skillId` カードアクションペイロードから抽出するために、仮想アシスタントテンプレートにクラスを導入します。

```csharp
    // Skill Card action data should contain skillId parameter
    // This class is used to deserialize it and get skillId 
    public class SkillCardActionData
    {
        /// <summary>
        /// Gets the ID of the skil that should handle this card
        /// </summary>
        [JsonProperty("skillId")]
        public string SkillId { get; set; }
    }
```

カードアクションデータから抽出するコードスニペットを次に示し `skillId` ます。 [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)クラスの拡張メソッドとして実装されています。

```csharp
    public static class ActivityExtensions
    {
        // Fetches skillId from CardAction data if present
        public static string GetSkillId(this Activity activity)
        {
            string skillId = string.Empty;

            try
            {
                if (activity.Type.Equals(ActivityTypes.Message) && activity.Value != null)
                {
                    var data = JsonConvert.DeserializeObject<SkillCardActionData>(activity.Value.ToString());
                    skillId = data.SkillId;
                }
                else if (activity.Type.Equals(ActivityTypes.Invoke) && activity.Value != null)
                {
                    var data = JsonConvert.DeserializeObject<SkillCardActionData>(JObject.Parse(activity.Value.ToString()).SelectToken("data").ToString());
                    skillId = data.SkillId;
                }
            }
            catch
            {
                // If not able to retrive skillId, empty skillId should be returned
            }

            return skillId;
        }
    }
```

### <a name="handle-interruptions-gracefully"></a>正常に中断する処理

仮想アシスタントは、ユーザーがスキルを呼び出そうとしているときに、別のスキルが現在アクティブな場合に、中断を処理できます。 `TeamsSkillDialog`また `TeamsSwitchSkillDialog` 、Bot フレームワークのスキル[ダイアログ](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs)と [ [switchスキル] ダイアログ](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)に基づいて、ユーザーがカードアクションからスキル経験を切り替えることができるようになりました。 この要求を処理するために、仮想アシスタントは、スキルを切り替えるための確認メッセージをユーザーに表示します。

![新しいスキルに切り替える際の確認メッセージ](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a>タスクモジュール要求の処理

仮想アシスタントにタスクモジュールの機能を追加するには、仮想アシスタントアクティビティハンドラーに、という2つのメソッドが追加されてい `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` ます。 これらのメソッドは、仮想アシスタントからタスクモジュールに関連するアクティビティをリッスンし、要求に関連付けられているスキルを特定し、要求を識別されたスキルに転送します。 

要求の転送は、[スキル Httpclient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable)、メソッドによって行われ `PostActivityAsync` ます。 これ `InvokeResponse` は、解析され、に変換される応答を返し `TaskModuleResponse` ます。

```csharp
    public static TaskModuleResponse GetTaskModuleRespose(this InvokeResponse invokeResponse)
    {
        if (invokeResponse.Body != null)
        {
            return new TaskModuleResponse()
            {
                Task = GetTask(invokeResponse.Body),
            };
        }

        return null;
    }

    private static TaskModuleResponseBase GetTask(object invokeResponseBody)
        {
            JObject resposeBody = (JObject)JToken.FromObject(invokeResponseBody);
            var task = resposeBody.GetValue("task");
            var taskType = task.SelectToken("type").ToString();

            return taskType switch
            {
                "continue" => new TaskModuleContinueResponse()
                {
                    Type = taskType,
                    Value = task.SelectToken("value").ToObject<TaskModuleTaskInfo>(),
                },
                "message" => new TaskModuleMessageResponse()
                {
                    Type = taskType,
                    Value = task.SelectToken("value").ToString(),
                },
                _ => null,
            };
        }
```

同様の方法で、カードアクションのディスパッチとタスクモジュールの応答が続きます。 タスクモジュールのフェッチと送信アクションのデータが更新され、を含むように `skillId` なります。 アクティビティ拡張メソッド `GetSkillId` は `skillId` 、呼び出す必要があるスキルの詳細を提供するペイロードから抽出します。

とメソッドのコードスニペットを次に示し `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` ます。

```csharp
    // Invoked when a "task/fetch" event is received to invoke task module.
    protected override async Task<TaskModuleResponse> OnTeamsTaskModuleFetchAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
    {
        try
        {
            string skillId = (turnContext.Activity as Activity).GetSkillId();
            var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;

            // Forward request to correct skill
            var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken);

            return invokeResponse.GetTaskModuleRespose();
        }
        catch (Exception exception)
        {
            await turnContext.SendActivityAsync(_templateEngine.GenerateActivityForLocale("ErrorMessage"));
            _telemetryClient.TrackException(exception);

            return null;
        }
    }

    // Invoked when a 'task/submit' invoke activity is received for task module submit actions.
    protected override async Task<TaskModuleResponse> OnTeamsTaskModuleSubmitAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
    {
        try
        {
            string skillId = (turnContext.Activity as Activity).GetSkillId();
            var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;

            // Forward request to correct skill
            var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

            return invokeResponse.GetTaskModuleRespose();
        }
        catch (Exception exception)
        {
            await turnContext.SendActivityAsync(_templateEngine.GenerateActivityForLocale("ErrorMessage"));
            _telemetryClient.TrackException(exception);

            return null;
        }
    }
```

さらに、 `validDomains` スキルを適切に使用してタスクモジュールが呼び出されるように、すべてのスキルドメインを仮想アシスタントのマニフェストファイルのセクションに含める必要があります。

### <a name="handling-collaborative-app-scopes"></a>共同作業アプリのスコープを処理する

Teams アプリは、1:1 のチャット、グループチャット、チャネルを含む複数のスコープ内に存在することができます。 コア仮想アシスタントテンプレートは、1:1 のチャット用に設計されています。 オンボードの機能の一部として、仮想アシスタントは、ユーザーに名前の入力を求め、ユーザーの状態を維持します。 その開始時の動作は、グループチャット/チャネルのスコープには適していないため、削除されました。

スキルは、複数の範囲 (1:1 チャット、グループチャット、チャネル会話) でのアクティビティを処理する必要があります。 これらのスコープのいずれかがサポートされていない場合、スキルは適切なメッセージで応答する必要があります。

次の処理関数が仮想アシスタントコアに追加されました。

- 仮想アシスタントは、グループチャットまたはチャネルからのテキストメッセージなしで呼び出すことができます。
- Articulations は、メッセージをディスパッチモジュールに送信する前に、(bot の必要な @mention を削除する) クリーンアップされます。

```csharp
    if (innerDc.Context.Activity.Conversation?.IsGroup == true)
    {
        // Remove bot atmentions for teams/groupchat scope
        innerDc.Context.Activity.RemoveRecipientMention();

        // If bot is invoked without any text, reply with FirstPromptMessage
        if (string.IsNullOrWhiteSpace(innerDc.Context.Activity.Text))
        {
            await innerDc.Context.SendActivityAsync(_templateEngine.GenerateActivityForLocale("FirstPromptMessage"));
            return EndOfTurn;
        }
    }
```

### <a name="handling-messaging-extensions"></a>メッセージング拡張機能の処理

メッセージング拡張機能のコマンドは、アプリマニフェストファイルで宣言されています。 メッセージング拡張機能のユーザーインターフェイスは、これらのコマンドによって処理されます。 メッセージング拡張コマンド (添付スキルとして) を電源にする仮想アシスタントの場合、仮想アシスタント自体のマニフェストにこれらのコマンドを含める必要があります。 個々のスキルのマニフェストからのコマンドも、仮想アシスタントのマニフェストに追加する必要があります。 コマンド ID は、スキルのアプリ ID をセパレーター () で追加することによって、関連付けられたスキルに関する情報を提供し `:` ます。

以下は、スキルのマニフェストファイルのスニペットです。

```json
 "composeExtensions": [
    {
        "botId": "<Skil_App_Id>",
        "commands": [
            {
                "id": "searchQuery",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
    ....
```

次に、対応する仮想アシスタントマニフェストファイルのコードスニペットを示します。

```json
 "composeExtensions": [
    {
        "botId": "<VA_App_Id>",
        "commands": [
            {
                "id": "searchQuery:<skill_id>",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
    ....
```

コマンドがユーザーによって起動されると、仮想アシスタントはコマンド ID を解析することによって関連付けられたスキルを特定し、コマンド ID から特別なサフィックス () を削除してアクティビティを更新し、それを対応するスキルに転送することができ `:<skill_id>` ます。 スキルのコードでは、特別なサフィックスを処理する必要がないため、複数のスキルを使用したコマンド Id 間の競合は回避されます。 この方法では、すべてのコンテキスト内のスキルのすべての検索およびアクションコマンド ("新規"、"commandBox"、"message") を仮想アシスタントで利用できます。

```csharp
    const string MessagingExtensionCommandIdSeparator = ":";

    // Invoked when a 'composeExtension/submitAction' invoke activity is received for a messaging extension action command
    protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
    {
        return await ForwardMessagingExtensionActionCommandActivityToSkill(turnContext, action, cancellationToken);
    }

    // Forwards invoke activity to right skill for messaging extension action commands.
    private async Task<MessagingExtensionActionResponse> ForwardMessagingExtensionActionCommandActivityToSkill(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
    {
        var skillId = ExtractSkillIdFromMessagingExtensionActionCommand(turnContext, action);
        var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;
        var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

        return invokeResponse.GetMessagingExtensionActionResponse();
    }

    // Extracts skill Id from messaging extension command and updates activity value
    private string ExtractSkillIdFromMessagingExtensionActionCommand(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action)
    {
        var commandArray = action.CommandId.Split(MessagingExtensionCommandIdSeparator);
        var skillId = commandArray.Last();

        // Update activity value by removing skill id before forwarding to the skill.
        var activityValue = JsonConvert.DeserializeObject<MessagingExtensionAction>(turnContext.Activity.Value.ToString());
        activityValue.CommandId = string.Join(MessagingExtensionCommandIdSeparator, commandArray, 0 commandArray.Length - 1);
        turnContext.Activity.Value = activityValue;

        return skillId;
    }
```

メッセージング拡張機能の中には、コマンド ID を含まないものがあります。 たとえば、には、 `composeExtension/selectItem` invoke タップアクションの値のみが含まれています。 関連付けられたスキルを識別するために、 `skillId` の応答を形成している間、各アイテムカードに接続されてい `OnTeamsMessagingExtensionQueryAsync` ます。 (これは、[アダプティブカードを仮想アシスタントに追加](#add-adaptive-cards-to-your-virtual-assistant)する方法に似ています。

```csharp
    // Invoked when a 'composeExtension/selectItem' invoke activity is received for compose extension query command.
    protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionSelectItemAsync(ITurnContext<IInvokeActivity> turnContext, JObject query, CancellationToken cancellationToken)
    {
        var data = JsonConvert.DeserializeObject<SkillCardActionData>(query.ToString());
        var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == data.SkillId).First().Value;
        var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

        return invokeResponse.GetMessagingExtensionResponse();
    }
```

---

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a>例: ブック-a room アプリテンプレートを仮想アシスタントスキルに変換する

[書籍-a room](app-templates.md#book-a-room)は[Microsoft Teams の bot](../bots/what-are-bots.md)で、現在の時刻から 30 (既定)、60、または90分間、ユーザーが会議室をすばやく検索して予約することができます。 個人または1:1 の会話に対して、会議中の bot の範囲を示します。

![「Book a room」というスキルを持つ仮想アシスタント](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

「」では、仮想アシスタントに接続できるスキルに変換するために導入されたデルタの変更について説明します。 同様のガイドラインに従って、既存の v4 bot をスキルに変換することができます。

### <a name="skill-manifest"></a>スキルマニフェスト

スキルマニフェストは、スキルのメッセージングエンドポイント、id、名前、およびその他の関連するメタデータを公開する JSON ファイルです (このマニフェストは、Microsoft Teams のアプリのサイドローディングに使用されるマニフェストとは異なります)。仮想アシスタントには、スキルを添付するための入力としてこのファイルへのパスが必要です。 次のマニフェストが bot の wwwroot フォルダーに追加されました。

```bash
botskills connect --remoteManifest "<url to skill's manifest>" ..
```

```json
{
  "$schema": "https://schemas.botframework.com/schemas/skills/skill-manifest-2.1.preview-0.json",
  "$id": "microsoft_teams_apps_bookaroom",
  "name": "microsoft-teams-apps-bookaroom",
  "description": "microsoft-teams-apps-bookaroom description",
  "publisherName": "Your Company",
  "version": "1.1",
  "iconUrl": "<icon url>",
  "copyright": "Copyright (c) Microsoft Corporation. All rights reserved.",
  "license": "",
  "privacyUrl": "<privacy url>",
  "endpoints": [
    {
      "name": "production",
      "protocol": "BotFrameworkV3",
      "description": "Production endpoint for the skill",
      "endpointUrl": "<endpoint url>",
      "msAppId": "skill app id"
    }
  ],
  "dispatchModels": {
    "languages": {
      "en-us": [
        {
          "id": "microsoft-teams-apps-bookaroom-en",
          "name": "microsoft-teams-apps-bookaroom LU (English)",
          "contentType": "application/lu",
          "url": "file://book-a-meeting.lu",
          "description": "English language model for the skill"
        }
      ]
    }
  },
  "activities": {
    "message": {
      "type": "message",
      "description": "Receives the users utterance and attempts to resolve it using the skill's LU models"
    }
  }
}
```

### <a name="luis-integration"></a>LUIS の統合

仮想アシスタントのディスパッチモデルは、添付されたスキルの LUIS モデルに基づいて構築されています。 ディスパッチモデルは、すべてのテキストアクティビティの目的を特定し、それに関連付けられているスキルを検出します。

仮想アシスタント `.lu` は、スキルを付加する際に、入力としてスキルの LUIS モデル (形式) を必要とします。 LUIS json は `.lu` 、botframework ツールを使用して形式に変換できます。

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

本-room bot には、ユーザーに対して2つの主要なコマンドがあります。

- `Book room`
- `Manage Favorites`

これら2つのコマンドについて理解している LUIS モデルを構築しました。 対応する機密情報を入力する必要があり `cognitivemodels.json` ます。 対応する LUIS JSON ファイルは[ここで](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json)見つけることができます。これは、対応するファイルがどのように見えるかを示してい `.lu` ます。

```
> ! Automatically generated by [LUDown CLI](https://github.com/Microsoft/botbuilder-tools/tree/master/Ludown), Tue Mar 31 2020 17:30:32 GMT+0530 (India Standard Time)

> ! Source LUIS JSON file: book-a-meeting.json

> ! Source QnA TSV file: Not Specified

> ! Source QnA Alterations file: Not Specified


> # Intent definitions

## BOOK ROOM
- book a room
- book room
- please book a room
- reserve a room
- i want to book a room
- i want to book a room please
- get me a room please
- get me a room


## MANAGE FAVORITES
- manage favorites
- manage favorite
- please manage my favorite rooms
- manage my favorite rooms please
- manage my favorite rooms
- i want to manage my favorite rooms

## None


> # Entity definitions


> # PREBUILT Entity definitions


> # Phrase list definitions


> # List entities

> # RegEx entities
```

この方法では、ユーザーが、 `book room` `manage favorites` 会議室の bot に関連付けられている、またはこのスキルに転送されたコマンドとして識別されるため、ユーザーによる仮想アシスタントへのすべてのコマンドを実行できます。
一方、会議室の場合は、LUIS モデルを使用して、これらのコマンドが入力されていない場合 (例:) について理解しておく必要があり `I want to manage my favorite rooms` ます。

### <a name="multi-language-support"></a>複数言語のサポート

この例では、英語のカルチャを持つ LUIS モデルのみが作成されています。 他の言語に対応する LUIS モデルを作成し、にエントリを追加することができ `cognitivemodels.json` ます。

```json
{
  "defaultLocale": "en-us",
  "languageModels": {
    "en-us": {
      "luisAppId": "",
      "luisApiKey": "",
      "luisApiHost": ""
    },
    "<your_language_culture>": {
      "luisAppId": "",
      "luisApiKey": "",
      "luisApiHost": ""
    }
  }
}
```

パラレルで、対応する `.lu` ファイルを luisFolder パスに追加します。 フォルダー構造は次のようにする必要があります。

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

Botskills コマンドを次のように更新して、パラメーターを変更し `languages` ます。

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

仮想アシスタントを使用し `SetLocaleMiddleware` て、現在のロケールを識別し、対応するディスパッチモデルを起動します。 (Bot フレームワークアクティビティには、このミドルウェアで使用されるロケールフィールドがあります)。スキルにも同じを使用することをお勧めします。 本-room bot はこのミドルウェアを使用せず、代わりに Bot フレームワークアクティビティの[Clientinfo エンティティ](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)からロケールを取得します。

### <a name="claim-validation"></a>要求の検証

発信者をスキルに制限する[claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs)が追加されました。 仮想アシスタントがこのスキルを呼び出せるようにするには、 `AllowedCallers` `appsettings` 特定の仮想アシスタントのアプリ ID を使用して配列を設定します。

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

許可された発信者の配列は、スキルにアクセスできるスキルコンシューマーを制限できます。 `*`任意のスキルコンシューマーからの呼び出しを受け入れるには、この配列に1つのエントリを追加します。

```
"AllowedCallers": [ "*" ],
```
スキルにクレーム検証を追加するための詳細なドキュメントは、[こちら](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)を参照してください。

### <a name="card-refresh-limitation"></a>カードの更新の制限

アクティビティの更新 (カードの更新) は、Virtual Assistant ([github の問題](https://github.com/microsoft/botbuilder-dotnet/issues/3686)) 経由ではまだサポートされていません。 そのため、すべてのカード更新呼び出し ( `UpdateActivityAsync` ) を新しいカード呼び出し () に置き換えました `SendActivityAsync` 。

### <a name="card-actions-and-task-module-flows"></a>カードアクションとタスクモジュールフロー

関連付けられたスキルにカードアクションまたはタスクモジュールのアクティビティを転送するには、スキルをそのスキルに埋め込む必要があり `skillId` ます。
Book-a room ボットカードアクション、タスクモジュールのフェッチと送信アクションのペイロードは、パラメーターとして格納されるように変更され `skillId` ます。 

詳細については、このドキュメント[のセクションを参照して](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards)ください。

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>グループチャットまたはチャネルスコープからのアクティビティを処理する

本-a room bot は、プライベートチャット (個人/1: 1 のスコープ) に対してのみ設計されています。 グループチャットとチャネルスコープをサポートするようにカスタマイズされた仮想アシスタントを使用しているため、これらのスコープから仮想アシスタントが呼び出される可能性があるので、このようにして、会議室 bot は同じ作業を行うことができます。 そのため、このようなアクティビティを処理するために、ルーム bot がカスタマイズされています。 このチェックは、 `OnMessageActivityAsync` 会議室の bot アクティビティハンドラーのメソッドに追加されました。

```csharp
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        // Check if activities are from groupchat/ teams scope. This might happen when the bot is consumed by Virtual Assistant.
        if (turnContext.Activity.Conversation.IsGroup == true)
        {
            await ShowNotSupportedInGroupChatCardAsync(turnContext).ConfigureAwait(false);
        }
        else
        {
            ...
        }
    }
```

[Bot フレームワークソリューションリポジトリ](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp)から既存のスキルを活用したり、新しいスキルを最初から作成したりすることもできます。 [この記事](https://microsoft.github.io/botframework-solutions/overview/skills/)では、以降のチュートリアルをご覧ください。 仮想アシスタントとスキルのアーキテクチャについては、[ドキュメント](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)を参照してください。

## <a name="sample-code-to-get-started"></a>開始するためのサンプルコード

- [更新された visual studio テンプレート](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [書籍-a room bot スキルコード](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a>仮想アシスタントの既知の制限

- **Endofconversation**。 スキルは、会話が `endOfConversation` 終了したときにアクティビティを送信する必要があります。 このアクティビティの基準として、仮想アシスタントは特定のスキルのコンテキストを終了し、仮想アシスタントの (ルート) コンテキストに戻ります。 冊子の bot の場合、会話を終了する明確な状態はありません。 そのため、ユーザーが `endOfConversation` ルートコンテキストに戻る必要がある場合は、単にコマンドを実行するだけで済み `start over` ます。
- **カードの更新**。 仮想アシスタントでは、カードの更新はまだサポートされていません。
- **メッセージング拡張機能**:
  - 現在、仮想アシスタントは、メッセージング拡張機能に対して最大10個のコマンドをサポートできます。
  - メッセージング拡張機能の構成は、個々のコマンドを対象としたものではありません。 これは、仮想アシスタントを通じて個々のスキルの構成を制限します。
  - メッセージング拡張機能のコマンド Id の最大長は[64 文字](../resources/schema/manifest-schema.md#composeextensions)、37文字は、スキル情報を埋め込むために使用されます。 このため、コマンド ID の更新された制約は27文字に制限されます。
>
>
