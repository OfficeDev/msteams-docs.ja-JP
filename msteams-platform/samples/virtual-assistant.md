---
title: 仮想アシスタントを作成する
description: コードの例やスニペットを使用して、コードの例やスニペットを使用してMicrosoft Teams用のVirtual Assistant ボットを作成する方法について説明します。アダプティブ カード、中断の処理、タスク モジュール要求、コラボレーション アプリスコープ、メッセージ拡張機能の処理、スキル マニフェストを使用します。複数の言語、要求の検証、LUIS 統合、モードのサポート。
ms.localizationpriority: medium
ms.topic: how-to
keywords: teams 仮想アシスタント ボット
ms.openlocfilehash: e473fd8166be6285ec90d78401b1df028d81b5b0
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104106"
---
# <a name="create-virtual-assistant"></a>仮想アシスタントを作成する

Virtual Assistantは、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話型ソリューションを作成できる Microsoft オープンソース テンプレートです。 [Virtual Assistantコア テンプレート](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template)は、[Bot Framework SDK](https://github.com/microsoft/botframework-sdk)、[Language Understanding (LUIS)](https://www.luis.ai/)、[QnA Maker](https://www.qnamaker.ai/) など、Virtual Assistantを構築するために必要な Microsoft テクノロジをまとめた基本的な構成要素です。 また、スキル登録、リンクされたアカウント、基本的な会話意図など、さまざまなシームレスな対話とエクスペリエンスをユーザーに提供するための重要な機能も組み合わせています。 さらに、テンプレート機能には、再利用可能な会話 [スキル](https://microsoft.github.io/botframework-solutions/overview/skills)の豊富な例が含まれています。  個々のスキルは、複数のシナリオを有効にするために、Virtual Assistant ソリューションに統合されています。 Bot Framework SDK を使用すると、ソース コード形式でスキルが表示され、必要に応じてカスタマイズおよび拡張できます。 Bot Framework のスキルの詳細については、「Bot Framework [スキルとは」](https://microsoft.github.io/botframework-solutions/overview/skills/)を参照してください。 このドキュメントでは、組織の実装に関する考慮事項Virtual Assistant、Teamsに重点を置いたVirtual Assistantを作成する方法、関連する例、コード サンプル、Virtual Assistantの制限事項について説明します。
次の図は、仮想アシスタントの概要を示しています。

![Virtual Assistant概要図](../assets/images/bots/virtual-assistant/overview.png)

テキスト メッセージ アクティビティは、[ディスパッチ](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) モデルを使用して、Virtual Assistant コアによって関連付けられたスキルにルーティングされます。

## <a name="implementation-considerations"></a>実装に関する考慮事項

Virtual Assistantを追加する決定には、多くの決定要因が含まれており、組織ごとに異なります。 組織のVirtual Assistant実装のサポート要因は次のとおりです。

* 中央チームは、すべての従業員エクスペリエンスを管理します。 新しいスキルの追加など、Virtual Assistant エクスペリエンスを構築し、コア エクスペリエンスの更新を管理する機能があります。
* 複数のアプリケーションがビジネス機能にまたがって存在し、その数は今後増加することが予想されます。
* 既存のアプリケーションはカスタマイズ可能であり、組織が所有し、Virtual Assistantのスキルに変換されます。
* 中央従業員エクスペリエンス チームは、既存のアプリのカスタマイズに影響を与えることができるようになります。 また、既存のアプリケーションをVirtual Assistantエクスペリエンスのスキルとして統合するために必要なガイダンスも提供されます。

次の図は、Virtual Assistantのビジネス関数を示しています。

![中央チームはアシスタントを維持し、ビジネス機能チームはスキルを提供します](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>Teamsに焦点を当てたVirtual Assistantを作成する

Microsoft は、Virtual Assistants とスキルを構築するための[Microsoft Visual Studio テンプレート](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate)を公開しました。 Visual Studio テンプレートを使用すると、アクションを含む限られたリッチ カードをサポートするテキスト ベースのエクスペリエンスを利用して、Virtual Assistantを作成できます。 Microsoft Teams プラットフォーム機能を含め、優れたTeamsアプリ エクスペリエンスを強化するために、Visual Studio基本テンプレートを強化しました。 いくつかの機能には、豊富なアダプティブ カード、タスク モジュール、チームまたはグループ チャット、メッセージ拡張機能のサポートが含まれます。 Virtual AssistantをMicrosoft Teamsに拡張する方法の詳細については、「[チュートリアル: Virtual AssistantをMicrosoft Teamsに拡張する」を参照してください](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)。
次の図は、Virtual Assistant ソリューションの概要図を示しています。

![Virtual Assistant ソリューションの概要図](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>Virtual Assistantにアダプティブ カードを追加する

要求を適切にディスパッチするには、Virtual Assistantが適切な LUIS モデルとそれに関連付けられている対応するスキルを識別する必要があります。 ただし、スキルに関連付けられている LUIS モデルはカード アクション テキスト用にトレーニングされるため、カード アクション アクティビティにはディスパッチ メカニズムを使用できません。 カード アクション テキストは固定で定義済みのキーワードであり、ユーザーからコメントされません。

この欠点は、カード アクション ペイロードにスキル情報を埋め込むことによって解決されます。 すべてのスキルは、カード アクションのフィールドに`value`埋め込む`skillId`必要があります。 各カード アクション アクティビティが関連するスキル情報を保持し、Virtual Assistantこの情報をディスパッチに利用できることを確認する必要があります。

スキル情報が常にカード アクションに存在することを確認するには、コンストラクターで指定 `skillId` する必要があります。
カード アクション データのサンプル コードは、次のセクションに示されています。

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

次に、 `SkillCardActionData` Virtual Assistant テンプレートのクラスが導入され、カード アクション ペイロードから抽出`skillId`されます。
カード アクション ペイロードから抽出  `skillId` するコード スニペットを次のセクションに示します。

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

実装は、 [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) クラスの拡張メソッドによって行われます。
次のセクションでは、カード アクション データから抽出  `skillId` するコード スニペットを示します。

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

### <a name="handle-interruptions"></a>中断を処理する

Virtual Assistantは、ユーザーが別のスキルが現在アクティブな間にスキルを呼び出そうとした場合に中断を処理できます。 `TeamsSkillDialog``TeamsSwitchSkillDialog`は、Bot Framework の [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) と [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs) に基づいて導入されます。 ユーザーは、カード アクションからスキル エクスペリエンスを切り替えることができます。 この要求を処理するために、Virtual Assistantは、スキルを切り替える確認メッセージをユーザーに求めます。

![新しいスキルに切り替えるときの確認プロンプト](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>タスク モジュール要求を処理する

タスク モジュール機能をVirtual Assistantに追加するには、Virtual Assistant アクティビティ ハンドラーに 2 つの追加メソッドが含まれています。 `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` これらのメソッドは、Virtual Assistantからタスク モジュール関連のアクティビティをリッスンし、要求に関連付けられているスキルを特定し、特定されたスキルに要求を転送します。

要求の転送は [、SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true) メソッド `PostActivityAsync` を使用して行われます。 これは、解析および変換`TaskModuleResponse`される応答`InvokeResponse`を返します。

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

同様の方法で、カード アクションのディスパッチとタスク モジュールの応答が行われます。 タスク モジュールは、アクション データをフェッチして送信し、含めるために `skillId`更新されます。
アクティビティ拡張メソッド `GetSkillId` は、 `skillId` 呼び出す必要があるスキルの詳細を提供するペイロードから抽出します。

次のセクションでは、コード スニペット `OnTeamsTaskModuleFetchAsync` と `OnTeamsTaskModuleSubmitAsync` メソッドについて説明します。

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

            return invokeResponse.GetTaskModuleResponse();
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

さらに、スキルを介して呼び出されたタスク モジュールが`validDomains`適切にレンダリングされるように、Virtual Assistantのマニフェスト ファイルのセクションにすべてのスキル ドメインを含める必要があります。

### <a name="handle-collaborative-app-scopes"></a>コラボレーション アプリのスコープを処理する

Teams アプリは、1 対 1 のチャット、グループ チャット、チャネルを含む複数のスコープに存在できます。 コア Virtual Assistant テンプレートは、1 対 1 のチャット用に設計されています。 オンボード エクスペリエンスの一環として、Virtual Assistantはユーザーに名前の入力を求め、ユーザーの状態を維持します。 オンボーディング エクスペリエンスはグループ チャットやチャネル スコープには適していないため、削除されました。

スキルは、1:1 チャット、グループ チャット、チャネル会話など、複数のスコープのアクティビティを処理する必要があります。 これらのスコープのいずれかがサポートされていない場合、スキルは適切なメッセージで応答する必要があります。

コアに次の処理関数が追加Virtual Assistant。

* Virtual Assistantは、グループ チャットまたはチャネルからのテキスト メッセージなしで呼び出すことができます。
* アーティキュレーションは、ディスパッチ モジュールにメッセージを送信する前にクリーニングされます。 たとえば、ボットの必要な@mentionを削除します。

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

### <a name="handle-message-extensions"></a>メッセージ拡張機能を処理する

メッセージ拡張機能のコマンドは、アプリ マニフェスト ファイルで宣言されます。 メッセージ拡張機能のユーザー インターフェイスには、これらのコマンドが使用されます。 Virtual Assistantが添付スキルとしてメッセージ拡張コマンドを実行するには、Virtual Assistant独自のマニフェストにこれらのコマンドを含める必要があります。 個々のスキルのマニフェストからVirtual Assistantのマニフェストにコマンドを追加する必要があります。 コマンド ID は、区切り記号を使用してスキルのアプリ ID を追加することで、関連するスキルに関する情報を提供します `:`。

スキルのマニフェスト ファイルのスニペットは、次のセクションに示されています。

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

対応するVirtual Assistant マニフェスト ファイルのコード スニペットは、次のセクションに示されています。

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

コマンドがユーザーによって呼び出されると、Virtual Assistantは、コマンド ID を解析し、コマンド ID から追加のサフィックス`:<skill_id>`を削除してアクティビティを更新し、対応するスキルに転送することで、関連するスキルを識別できます。 スキルのコードでは、追加のサフィックスを処理する必要はありません。 そのため、スキル間でのコマンド ID 間の競合は回避されます。 この方法では、**作成**、**commandBox**、**メッセージ** など、すべてのコンテキスト内のスキルのすべての検索コマンドとアクション コマンドに、Virtual Assistantが使用されます。

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

一部のメッセージ拡張アクティビティには、コマンド ID が含まれていません。 たとえば、 `composeExtension/selectItem` 呼び出しタップ アクションの値のみが含まれます。 関連するスキルを識別するために、各項目カードに添付され、`skillId`.`OnTeamsMessagingExtensionQueryAsync` これは、[アダプティブ カードをVirtual Assistantに追加する方法と](#add-adaptive-cards-to-your-virtual-assistant)似ています。

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

## <a name="example"></a>例

次の例は、Book-a-room アプリ テンプレートをVirtual Assistantスキルに変換する方法を示しています。Book-a-room は、ユーザーが現在の時刻から 30 分、60 分、または 90 分間会議室をすばやく見つけて予約できるMicrosoft Teamsです。 既定は 30 分間です。 会議室予約ボットは、個人の会話または一対一の会話を対象としています。
次の図は、会議室のスキルを持つVirtual Assistant **を** 示しています。

!["部屋を予約する" スキルでVirtual Assistantする](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

Virtual Assistantにアタッチされているスキルに変換するために導入された差分の変更を次に示します。 同様のガイドラインに従って、既存の v4 ボットをスキルに変換します。

### <a name="skill-manifest"></a>スキル マニフェスト

スキル マニフェストは、スキルのメッセージング エンドポイント、ID、名前、およびその他の関連メタデータを公開する JSON ファイルです。 このマニフェストは、Microsoft Teamsでアプリをサイドローディングするために使用されるマニフェストとは異なります。 Virtual Assistantでは、スキルをアタッチするための入力としてこのファイルへのパスが必要です。 ボットの wwwroot フォルダーに次のマニフェストを追加しました。

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

### <a name="luis-integration"></a>LUIS 統合

Virtual Assistantのディスパッチ モデルは、アタッチされたスキルの LUIS モデルの上に構築されます。 ディスパッチ モデルは、すべてのテキスト アクティビティの意図を識別し、それに関連付けられているスキルを見つけます。

Virtual Assistantスキルをアタッチするときに、入力としてスキルの LUIS モデル`.lu`が形式で必要です。 LUIS json は、botframework-cli ツールを使用して書式設定に `.lu` 変換されます。

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Book-a-room ボットには、ユーザーに対して主に次の 2 つのコマンドがあります。

* `Book room`
* `Manage Favorites`

これら 2 つのコマンドを理解して、LUIS モデルを構築しました。 対応するシークレットは 、.`cognitivemodels.json` 対応する LUIS JSON ファイルは [、こちらにあります](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json)。
対応する `.lu` ファイルは、次のセクションに示されています。

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

この方法では、ユーザーがVirtual Assistantに対して発行したコマンドは、ボットに`book room``manage favorites`関連付けられている`Book-a-room`コマンドとして識別され、このスキルに転送されます。
一方、ボットは LUIS モデルを使用して、 `Book-a-room room` これらのコマンドが完全に入力されていない場合は理解する必要があります。 例: `I want to manage my favorite rooms`。

### <a name="multi-language-support"></a>多言語サポート

たとえば、英語のカルチャのみを持つ LUIS モデルが作成されます。 他の言語に対応する LUIS モデルを作成し、.`cognitivemodels.json`

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

並列で、luisFolder パスに対応する `.lu` ファイルを追加します。 フォルダー構造は次のようになります。

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

パラメーターを変更 `languages` するには、botskills コマンドを次のように更新します。

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

Virtual Assistantは、現在のロケールを識別し、対応するディスパッチ モデルを呼び出すために使用`SetLocaleMiddleware`します。 ボット フレームワーク アクティビティには、このミドルウェアで使用されるロケール フィールドがあります。 スキルにも同じものを使用できます。 Book-a-room ボットはこのミドルウェアを使用せず、代わりに Bot Framework アクティビティの [clientInfo エンティティ](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)からロケールを取得します。

### <a name="claim-validation"></a>要求の検証

呼び出し元をスキルに制限するために [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) を追加しました。 このスキルを呼び出すVirtual Assistantを許可するには、その特定のVirtual Assistantのアプリ ID から配列`appsettings`を設定`AllowedCallers`します。

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

許可された呼び出し元配列は、スキルコンシューマーがスキルにアクセスできるスキルを制限できます。 この配列に 1 つのエントリ `*` を追加して、任意のスキル コンシューマーからの呼び出しを受け入れます。

```
"AllowedCallers": [ "*" ],
```

スキルに要求の検証を追加する方法の詳細については、「スキルに [要求の検証を追加する」を](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)参照してください。

### <a name="limitation-of-card-refresh"></a>カードの更新の制限

カードの更新などのアクティビティの更新は、Virtual Assistant ([github の問題](https://github.com/microsoft/botbuilder-dotnet/issues/3686)) を通じてはまだサポートされていません。 そのため、すべてのカード更新呼び出しを新しいカード`SendActivityAsync`通話`UpdateActivityAsync`の投稿に置き換えました。

### <a name="card-actions-and-task-module-flows"></a>カード アクションとタスク モジュール フロー

カード アクションまたはタスク モジュールアクティビティを関連するスキルに転送するには、スキルをそのスキルに埋め込む `skillId` 必要があります。
`Book-a-room` ボット カード アクション、タスク モジュールのフェッチおよび送信アクション ペイロードは、パラメーターとして含 `skillId` まれるように変更されます。

詳細については、このドキュメントの [この](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) セクションを参照してください。

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>グループ チャットまたはチャネル スコープからのアクティビティを処理する

`Book-a-room bot` は、個人用または 1:1 のスコープのみなど、プライベート チャット用に設計されています。 グループ チャットとチャネル スコープをサポートするようにVirtual Assistantをカスタマイズしたので、チャネル スコープからVirtual Assistantを呼び出す必要があるため、`Book-a-room`ボットは同じスコープのアクティビティを取得する必要があります。 そのため、 `Book-a-room`ボットは、これらのアクティビティを処理するようにカスタマイズされます。 ボットのアクティビティ ハンドラーの`Book-a-room`チェックイン `OnMessageActivityAsync` 方法を確認できます。

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

[Bot Framework Solutions リポジトリ](https://github.com/microsoft/botframework-components/tree/main/skills/csharp)から既存のスキルを活用したり、新しいスキルを完全にゼロから作成したりすることもできます。 新しいスキルを作成する方法については、 [新しいスキルを作成するためのチュートリアルを](https://microsoft.github.io/botframework-solutions/overview/skills/)参照してください。 Virtual Assistantおよびスキル アーキテクチャのドキュメントについては、[Virtual Assistantとスキル アーキテクチャ](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)に関するドキュメントを参照してください。  

## <a name="limitations-of-virtual-assistant"></a>Virtual Assistantの制限事項

* **EndOfConversation**: スキルは、会話が完了したときにアクティビティを `endOfConversation` 送信する必要があります。 アクティビティに基づいて、Virtual Assistantはその特定のスキルでコンテキストを終了し、Virtual Assistantのルート コンテキストに戻ります。 Book-a-room ボットの場合、会話が終了した明確な状態はありません。 そのため、ボットから`Book-a-room`送信`endOfConversation`されておらず、ユーザーがルート コンテキストに戻りたい場合は、コマンドで`start over`簡単に行うことができます。  
* **カードの更新**: Virtual Assistantでは、カードの更新はまだサポートされていません。  
* **メッセージ拡張機能**:
  * 現在、Virtual Assistantでは、メッセージ拡張機能に対して最大 10 個のコマンドをサポートできます。
  * メッセージ拡張機能の構成は、個々のコマンドではなく、拡張機能自体全体に対してスコープが設定されます。 これにより、Virtual Assistantを通じて個々のスキルの構成が制限されます。
  * メッセージ拡張コマンド ID の最大長は [64 文字](../resources/schema/manifest-schema.md#composeextensions) で、スキル情報の埋め込みには 37 文字が使用されます。 したがって、コマンド ID の更新された制約は 27 文字に制限されます。

[Bot Framework Solutions リポジトリ](https://github.com/microsoft/botframework-components/tree/main/skills/csharp)から既存のスキルを活用したり、新しいスキルを完全にゼロから作成したりすることもできます。 後のチュートリアルについては、 [こちらを参照してください](https://microsoft.github.io/botframework-solutions/overview/skills/)。 Virtual Assistantとスキルのアーキテクチャについては[、ドキュメント](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)を参照してください。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **C#**  **.NET** |
|----------|-----------------|---------------------------|
| Visual Studio テンプレートを更新しました | チームの機能をサポートするためのカスタマイズされたテンプレート。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| Book-a-room ボットのスキル コード | 外出先で会議室をすばやく見つけて予約できます。 | [表示](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |

## <a name="see-also"></a>関連項目

* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
* [会議室予約](app-templates.md#app-template-code-samples)
* [Microsoft Teams ボット](../bots/what-are-bots.md)
