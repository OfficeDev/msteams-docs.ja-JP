---
title: Microsoft Teams の仮想アシスタント
description: Microsoft Teams で使用する仮想アシスタントボットとスキルを作成する方法
ms.topic: how-to
keywords: Teams 仮想アシスタント ボット
ms.openlocfilehash: d72b1afbf975707d694d4aaef31263a3ce467629
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014615"
---
# <a name="virtual-assistant-for-microsoft-teams"></a>Microsoft Teams の仮想アシスタント

仮想アシスタントは、ユーザー エクスペリエンス、組織のブランド化、および必要なデータのフル コントロールを維持しながら、堅牢な会話ソリューションを作成できる Microsoft オープン ソース テンプレートです。 仮想[](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template)アシスタントコア テンプレートは[、Bot Framework SDK、Language](https://github.com/microsoft/botframework-sdk) [Understanding (FRAMEWORK)](https://www.luis.ai/) [、QnA Maker](https://www.qnamaker.ai/)など、仮想アシスタントの構築に必要な Microsoft テクノロジと、スキルの登録、リンクされたアカウント、さまざまなシームレスな対話とエクスペリエンスをエンド ユーザーに提供するための基本的な会話の意図など、重要な機能をまとめる基本の構成ブロックです。 さらに、テンプレート機能には、再利用可能な会話スキルの豊富な例が含 [まれます](https://microsoft.github.io/botframework-solutions/overview/skills)。  個々のスキルを仮想アシスタント ソリューションに統合して、複数のシナリオを有効にできます。 Bot Framework SDK を使用すると、必要に応じてカスタマイズおよび拡張できるソース コード形式でスキルが表示されます。 「Bot [Framework のスキルとは」を参照してください](https://microsoft.github.io/botframework-solutions/overview/skills/)。

![仮想アシスタントの概要図](../assets/images/bots/virtual-assistant/overview.png)

テキスト メッセージ アクティビティは、ディスパッチ モデルを使用して仮想アシスタント コアによって関連付けられたスキルに [ルーティング](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) されます。 

## <a name="implementation-considerations"></a>実装に関する考慮事項

仮想アシスタントを追加する決定には、多くの決定性を含め、組織ごとに異なる場合があります。 組織の仮想アシスタントの実装をサポートする要因を次に示します。

- 中央チームは、すべての従業員のエクスペリエンスを管理し、仮想アシスタント エクスペリエンスを構築し、新しいスキルの追加を含むコア エクスペリエンスの更新を管理する機能を備えています。
- 複数のアプリケーションが複数のビジネス機能に存在したり、その数が将来増える見込みです。
- 既存のアプリケーションはカスタマイズ可能で、組織が所有し、仮想アシスタントのスキルに変換できます。
- 中央の従業員エクスペリエンス チームは、既存のアプリのカスタマイズに影響を与え、既存のアプリケーションを仮想アシスタントエクスペリエンスのスキルとして統合するために必要なガイダンスを提供できます。

![中央チームがアシスタントを管理し、ビジネス機能チームがスキルを貢献する](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Teams に重点を置く仮想アシスタントを作成する

Microsoft は、仮想アシスタント [Visual Studio構築のための](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) 新しいテンプレートを公開しました。 新しいVisual Studioテンプレートを使用すると、アクションを含む限られたリッチ カードをサポートするテキスト ベースのエクスペリエンスを利用した仮想アシスタントを作成できます。 Microsoft Teams プラットフォーム機能をVisual Studio Teams アプリエクスペリエンスを強化するために、新しい基本テンプレートが強化されました。 機能のいくつかには、豊富なアダプティブ カード、タスク モジュール、チーム/グループ チャット、メッセージング拡張機能のサポートが含まれます。 *「チュートリアル:* 仮想 [アシスタントを Microsoft Teams に拡張する」も参照してください](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)。

![仮想アシスタント ソリューションの大きな図](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>アダプティブ カードを仮想アシスタントに追加する

要求を適切にディスパッチするには、仮想アシスタントが適切な THEIS モデルとそれに関連付けられているスキルを識別する必要があります。 ただし、ユーザーからの発声ではなく、定義済みの固定キーワードで、スキルに関連付けられたカード アクション テキストに対してトレーニングを受けできない可能性があります。このため、ディスパッチメカニズムはカード アクション アクティビティには使用できません。

この問題を解決するには、スキル情報をカードアクションペイロードに埋め込む必要があります。 すべてのスキルはカード `skillId` アクションの  `value` フィールドに埋め込む必要があります。 これは、各カード アクション アクティビティが関連するスキル情報を持ち、仮想アシスタントがディスパッチにこの情報を利用できる最善の方法です。

カード アクション データのサンプルを次に示します。 コンストラクターを `skillId` 指定することで、スキル情報が常にカード アクションに存在する必要があります。

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

次に、仮想アシスタント `SkillCardActionData` テンプレートのクラスを導入して、カード `skillId` アクションペイロードから抽出します。

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

カードのアクション データから抽出するコード  `skillId` スニペットを次に示します。 Activity クラスに拡張メソッドとして [実装](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) しました。

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

### <a name="handle-interruptions-gracefully"></a>中断を適切に処理する

仮想アシスタントは、別のスキルが現在アクティブな間にユーザーがスキルを呼び出そうとする場合に、中断を処理できます。 Bot Framework の `TeamsSkillDialog` `TeamsSwitchSkillDialog` [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) と [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)に基づいて、ユーザーがカードアクションからスキル エクスペリエンスを切り替え可能にしました。 この要求を処理するために、仮想アシスタントは、スキルを切り替える確認メッセージをユーザーに表示します。

![新しいスキルに切り替える際の確認プロンプト](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a>タスク モジュール要求の処理

仮想アシスタントにタスク モジュール機能を追加するには、仮想アシスタント アクティビティ ハンドラーに次の 2 つの追加メソッドが含 `OnTeamsTaskModuleFetchAsync` まれています `OnTeamsTaskModuleSubmitAsync` 。 これらのメソッドは、仮想アシスタントからタスク モジュール関連のアクティビティをリッスンし、要求に関連付けられているスキルを特定し、識別されたスキルに要求を転送します。 

要求の転送は  [、SkillHttpClient メソッドを使用](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable)して行 `PostActivityAsync` われます。 これは、解析され、 `InvokeResponse` 変換された応答を返します `TaskModuleResponse` 。

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

カード アクションのディスパッチとタスク モジュールの応答にも同様のアプローチが使用されます。 タスク モジュールのフェッチと送信のアクション データが更新され、含まれます `skillId` 。 Activity Extension メソッド `GetSkillId` は、呼び出す必要があるスキルに関する詳細を提供するペイロード `skillId` から抽出します。

次のコード スニペットと `OnTeamsTaskModuleFetchAsync` メソッドを `OnTeamsTaskModuleSubmitAsync` 示します。

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

さらに、スキルによって呼び出されるタスク モジュールが適切にレンダリングされるには、すべてのスキル ドメインを仮想アシスタントのマニフェスト ファイルのセクション `validDomains` に含める必要があります。

### <a name="handling-collaborative-app-scopes"></a>共同作業アプリのスコープの処理

Teams アプリは、1 対 1 のチャット、グループ チャット、チャネルなど、複数のスコープで存在できます。 コア仮想アシスタント テンプレートは、1 対 1 のチャット用に設計されています。 オンボーディング エクスペリエンスの一環として、仮想アシスタントはユーザーに名前の入力を求め、ユーザーの状態を維持します。 オンボーディング エクスペリエンスはグループ チャット/チャネル スコープには適していないので、削除されています。

スキルは、複数の範囲 (1 対 1 のチャット、グループ チャット、チャネル会話) のアクティビティを処理する必要があります。 これらのスコープがサポートされていない場合、スキルは適切なメッセージで応答する必要があります。

次の処理機能が仮想アシスタント コアに追加されました。

- 仮想アシスタントは、グループ チャットまたはチャネルからのテキスト メッセージなしで呼び出すことができます。
- メッセージをディスパッチ モジュールに送信する前に、明確化がクリーンアップされます (つまり、ボットの@mentionを削除します)。

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

メッセージング拡張機能のコマンドは、アプリ マニフェスト ファイルで宣言されています。 メッセージング拡張機能のユーザー インターフェイスには、これらのコマンドが搭載されています。 仮想アシスタントがメッセージング拡張機能コマンドの電源を入れるには (付属のスキルとして)、仮想アシスタント独自のマニフェストにこれらのコマンドが含まれている必要があります。 個々のスキルのマニフェストのコマンドも仮想アシスタントのマニフェストに追加する必要があります。 コマンド ID は、スキルのアプリ ID を区切り記号 ( ) を介して追加することで、関連付けられたスキルに関する情報を提供します `:` 。

スキルのマニフェスト ファイルのスニペットを次に示します。

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

対応する仮想アシスタント マニフェスト ファイル コード スニペットを次に示します。

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

ユーザーによってコマンドが呼び出されると、仮想アシスタントは、コマンド ID を解析して関連付けられたスキルを識別し、コマンド ID から余分なサフィックス ( ) を削除してアクティビティを更新し、対応するスキルに転送できます。 `:<skill_id>` スキルのコードは余分なサフィックスを処理する必要はありません。したがって、スキル間のコマンドの ID 間の競合は回避されます。 この方法では、すべてのコンテキスト内のスキルのすべての検索コマンドとアクション コマンド ("compose"、"commandBox"、および "message") を仮想アシスタントが利用できます。

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

メッセージング拡張機能のアクティビティの中には、コマンド ID が含まれるものがあります。 たとえば、呼 `composeExtension/selectItem` び出しタップ アクションの値だけが含まれているとします。 関連するスキルを識別するために、応答を形成している間に各アイテム `skillId`  カードに添付されます `OnTeamsMessagingExtensionQueryAsync` 。 (これは、アダプティブ カードを仮想アシスタント [に追加する方法に似ています](#add-adaptive-cards-to-your-virtual-assistant)。

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a>例: ブック ルーム アプリ テンプレートを仮想アシスタントのスキルに変換する

[会議室](app-templates.md#book-a-room) の予約は [、ユーザー](../bots/what-are-bots.md) が現在の時刻から 30 分 (既定)、60 分、または 90 分間の会議室をすばやく見つけて予約できる Microsoft Teams ボットです。 会議室予約ボットは、個人の会話または一対一の会話を対象としています。

!["部屋を予約する" スキルを持つ仮想アシスタント](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

仮想アシスタントにアタッチできるスキルに変換するために導入された差分の変更を次に示します。 同様のガイドラインに従って、既存の v4 ボットをスキルに変換できます。

### <a name="skill-manifest"></a>スキル マニフェスト

スキル マニフェストは、スキルのメッセージング エンドポイント、ID、名前、その他の関連するメタデータを公開する JSON ファイルです (このマニフェストは、Microsoft Teams でアプリをサイドロードするために使用されるマニフェストとは異なります)。仮想アシスタントは、スキルを添付する入力としてこのファイルへのパスを必要とします。 ボットの wwwroot フォルダーに次のマニフェストを追加しました。

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

### <a name="luis-integration"></a>[!!--]--

仮想アシスタントのディスパッチ モデルは、アタッチされたスキルの数を持つ OF モデルを基に構築されています。 ディスパッチ モデルは、すべてのテキスト アクティビティの意図を識別し、関連付けられているスキルを見つけ出します。

仮想アシスタントでは、スキルを追加する一方で、入力としてスキルの (形式で) スキルの種類 `.lu` (形式) が必要です。 BOTframework-cli ツールを使用して、JSON を形式 `.lu` に変換できます。

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Book-a-room ボットには、ユーザーに対して次の 2 つの主なコマンドがあります。

- `Book room`
- `Manage Favorites`

これら 2 つのコマンドを理解する、1 つの大きなモデルを構築しました。 対応するシークレットを設定する必要があります `cognitivemodels.json` 。 対応する JSON ファイルはここに [見つか](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) り、対応するファイルは `.lu` 次のように表示されます。

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

この方法では、仮想アシスタントに関連するユーザーによるコマンドの問題、または `book room` Book-a-room ボットに関連付けられたコマンドとして識別されるコマンドは、このスキルに転送 `manage favorites` されます。
一方、BOOK-a-room room bot は、これらのコマンドが入力されていない場合は、このモデルを使用してこれらのコマンドを理解する必要があります (次に例を示します `I want to manage my favorite rooms` )。

### <a name="multi-language-support"></a>複数言語のサポート

この例では、英語のカルチャを持つ、唯一の種類のオブジェクト モデルを作成しました。 他の言語に対応する数型 (-) のモデルを作成し、エントリを追加できます `cognitivemodels.json` 。

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

並行して、対応する `.lu` ファイルをfolder パスに追加します。 フォルダーの構造は次のようになります。

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

botskills コマンドを次のように更新してパラメーターを変更 `languages` します。

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

仮想アシスタントは、 `SetLocaleMiddleware` 現在のロケールを識別し、対応するディスパッチ モデルを呼び出します。 (Bot フレームワーク アクティビティには、このミドルウェアで使用されるロケール フィールドがあります)。スキルにも同じ機能を使用することをお勧めします。 Book-a-room bot は、このミドルウェアを使用しません。代わりに、Bot フレームワーク アクティビティの clientInfo エンティティから [ロケールを取得します](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)。

### <a name="claim-validation"></a>要求の検証

呼び出し [元をスキルに制限するために claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) が追加されました。 仮想アシスタントがこのスキルを呼び出すのを許可するには、その特定の仮想アシスタントのアプリ ID から `AllowedCallers` `appsettings` 配列を設定します。

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

許可された呼び出し元の配列では、ユーザーがスキルにアクセスできるスキルを制限できます。 任意のスキル コンシューマー `*` からの呼び出しを受け入れるには、この配列に単一のエントリを追加します。

```
"AllowedCallers": [ "*" ],
```
スキルにクレーム検証を追加する詳細なドキュメントについては、こちらを参照 [してください](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)。

### <a name="card-refresh-limitation"></a>カードの更新の制限

アクティビティの更新 (カードの更新) は、仮想アシスタント[(github](https://github.com/microsoft/botbuilder-dotnet/issues/3686)の問題) ではサポートされていません。 そのため、すべてのカード更新呼び出し ( ) を新しいカード呼び出し ( ) の投稿 `UpdateActivityAsync` に置き換えました `SendActivityAsync` 。

### <a name="card-actions-and-task-module-flows"></a>カード アクションとタスク モジュール フロー

カードアクションまたはタスク モジュールアクティビティを関連付けられたスキルに転送するには、スキルをそのスキルに埋め込む `skillId` 必要があります。
Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter. 

詳細については、このドキュメント [のこの](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) セクションを参照してください。

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>グループ チャットまたはチャネル スコープからのアクティビティの処理

Book-a-room ボットは、プライベート チャット (個人用/1:1 スコープ) 専用に設計されています。 グループ チャットとチャネルスコープをサポートするために仮想アシスタントをカスタマイズしたので、仮想アシスタントがこれらのスコープから呼び出される可能性があります。したがって、Book-a-room ボットは同じアクティビティを取得する可能性があります。 したがって、ブック ルーム ボットは、これらのアクティビティを処理するためにカスタマイズされます。 チェックは `OnMessageActivityAsync` 、Book-a-room ボットのアクティビティ ハンドラーのメソッドに入れらされています。

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

[Bot Framework](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp)ソリューション リポジトリの既存のスキルを活用したり、新しいスキルを最初から完全に作成したりすることもできます。 以降のチュートリアルについては、こちらを参照 [してください](https://microsoft.github.io/botframework-solutions/overview/skills/)。 仮想アシスタントと [スキル アーキテクチャ](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   のドキュメントを参照してください。

## <a name="sample-code-to-get-started"></a>開始するサンプル コード

- [Visual Studio テンプレートの更新](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [Book-a-room ボットのスキル コード](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a>仮想アシスタントの既知の制限事項

- **EndOfConversation**. スキルは会話を終了 `endOfConversation` するときにアクティビティを送信する必要があります。 このアクティビティに基づいて、仮想アシスタントは特定のスキルを持つコンテキストを終了し、仮想アシスタント (ルート) コンテキストに戻ります。 Book-a-room ボットの場合、会話を終了できる明確な状態はありません。 そのため、Book-a-room ボットから送信したのではなく、ユーザーがルート コンテキストに戻る必要がある場合は、コマンドを使用するだけで `endOfConversation` 行 `start over` えるのです。
- **カードの更新**。 カードの更新は、仮想アシスタントを通じてまだサポートされていません。
- **メッセージング拡張機能**。:
  - 現在、仮想アシスタントはメッセージング拡張機能に対して最大 10 個のコマンドをサポートできます。
  - メッセージング拡張機能の構成は、個々のコマンドではなく、拡張機能全体を対象とします。 これにより、仮想アシスタントを通じて個々のスキルの構成が制限されます。
  - メッセージング拡張機能コマンドの ID の長さは最大 [64](../resources/schema/manifest-schema.md#composeextensions) 文字で、スキル情報の埋め込みには 37 文字が使用されます。 したがって、コマンド ID の更新された制約は 27 文字に制限されています。
>
>
