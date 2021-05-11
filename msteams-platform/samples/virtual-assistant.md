---
title: 仮想アシスタントを作成する
description: 仮想アシスタント ボットとスキルを作成する方法をMicrosoft Teams
localization_priority: Normal
ms.topic: how-to
keywords: teams 仮想アシスタント ボット
ms.openlocfilehash: 80a308050317e8a211b8f7a9e2dd459c1572af18
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058678"
---
# <a name="create-virtual-assistant"></a>仮想アシスタントを作成する 

Virtual Assistant は、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話型ソリューションを作成できる Microsoft のオープン ソース テンプレートです。 Virtual [Assistant コア](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) テンプレートは、ボット フレームワーク [SDK](https://github.com/microsoft/botframework-sdk)、言語理解 [(LUIS)](https://www.luis.ai/) [、QnA Maker](https://www.qnamaker.ai/)など、仮想アシスタントの構築に必要な Microsoft テクノロジをまとめる基本的な構成ブロックです。 また、スキル登録、リンクされたアカウント、ユーザーにシームレスな対話とエクスペリエンスを提供する基本的な会話の意図を含む重要な機能をまとめます。 さらに、テンプレート機能には、再利用可能な会話スキルの豊富な例が含 [まれます](https://microsoft.github.io/botframework-solutions/overview/skills)。  個々のスキルは、仮想アシスタント ソリューションに統合され、複数のシナリオを有効にします。 Bot Framework SDK を使用すると、スキルがソース コード形式で提示され、必要に応じてカスタマイズおよび拡張できます。 ボット フレームワークのスキルの詳細については [、「What is a Bot Framework skill」を参照してください](https://microsoft.github.io/botframework-solutions/overview/skills/)。 このドキュメントでは、組織の仮想アシスタントの実装に関する考慮事項、Teams に焦点を当てた仮想アシスタントを作成する方法、関連する例、コード サンプル、および仮想アシスタントの制限事項について説明します。
次の図は、仮想アシスタントの概要を表示します。

![仮想アシスタントの概要図](../assets/images/bots/virtual-assistant/overview.png)

テキスト メッセージ アクティビティは、ディスパッチ モデルを使用して Virtual Assistant コアによって関連付けられたスキルに [ルーティング](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) されます。 

## <a name="implementation-considerations"></a>実装に関する考慮事項

仮想アシスタントを追加する決定には、多くの決定項目が含まれています。組織ごとに異なります。 組織の仮想アシスタント実装のサポート要素は次のとおりです。

* 中央チームがすべての従業員エクスペリエンスを管理します。 仮想アシスタント エクスペリエンスを構築し、新しいスキルの追加を含むコア エクスペリエンスの更新プログラムを管理する機能があります。
* ビジネス機能全体に複数のアプリケーションが存在し、その数は今後増加する見込みです。
* 既存のアプリケーションはカスタマイズ可能で、組織が所有し、仮想アシスタントのスキルに変換されます。
* 中央の従業員エクスペリエンス チームは、既存のアプリのカスタマイズに影響を与える可能性があります。 また、仮想アシスタント エクスペリエンスのスキルとして既存のアプリケーションを統合するために必要なガイダンスも提供します。   
次の図は、仮想アシスタントのビジネス機能を表示します。 

![中央チームはアシスタントを維持し、ビジネス機能チームはスキルを提供します](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>ユーザーにフォーカスTeams仮想アシスタントを作成する

Microsoft は、仮想アシスタント[Visual Studioスキルを構築](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate)する新しいテンプレートを公開しました。 このテンプレートVisual Studio、アクションを含む限られたリッチ カードをサポートするテキスト ベースのエクスペリエンスをベースにした仮想アシスタントを作成できます。 基本テンプレートを拡張Visual Studio、プラットフォームの機能Microsoft Teams、アプリ エクスペリエンスを向上Teams強化しました。 機能のいくつかには、豊富なアダプティブ カード、タスク モジュール、チームまたはグループ チャット、メッセージング拡張機能のサポートが含まれます。 仮想アシスタントを仮想アシスタントに拡張する方法のMicrosoft Teams、「チュートリアル: Extend your Virtual Assistant to [Microsoft Teams」 を参照してください](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)。    
次の図は、仮想アシスタント ソリューションの高レベル図を示しています。

![仮想アシスタント ソリューションの高レベルの図](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>仮想アシスタントにアダプティブ カードを追加する

要求を適切にディスパッチするには、仮想アシスタントが適切な LUIS モデルとそれに関連付けられている対応するスキルを識別する必要があります。 ただし、スキルに関連付けられた LUIS モデルがカード アクション テキスト用にトレーニングされている場合、ディスパッチ機構をカード アクション アクティビティに使用することはできません。 カード アクション のテキストは、固定された定義済みのキーワードであり、ユーザーからのコメントはありません。

この欠点は、カード アクション ペイロードにスキル情報を埋め込む方法によって解決されます。 すべてのスキルは、カード `skillId` アクションの  `value` フィールドに埋め込む必要があります。 各カード アクション アクティビティに関連するスキル情報が含まれる必要があります。仮想アシスタントは、この情報をディスパッチに利用できます。

スキル情報が常にカード アクションに表示されるのを確認するには、コンストラクター `skillId` で指定する必要があります。
カード アクション データのサンプル コードを次のセクションに示します。
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

次に `SkillCardActionData` 、仮想アシスタント テンプレートのクラスを導入して、カード `skillId` アクション ペイロードから抽出します。
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

実装は [、Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) クラスの拡張メソッドによって行われます。
カード アクション データから抽出  `skillId` するコード スニペットを次のセクションに示します。

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

### <a name="handle-interruptions"></a>中断の処理

仮想アシスタントは、別のスキルが現在アクティブな間にユーザーがスキルを呼び出そうとする場合に中断を処理できます。 `TeamsSkillDialog`、 `TeamsSwitchSkillDialog` ボット フレームワークの [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) と [SwitchSkillDialog に基づいて導入されます](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)。 ユーザーは、カード操作からスキル エクスペリエンスを切り替えできます。 この要求を処理するために、仮想アシスタントはスキルを切り替える確認メッセージをユーザーに求めるメッセージを表示します。

![新しいスキルに切り替える際の確認プロンプト](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>タスク モジュール要求の処理

タスク モジュールの機能を仮想アシスタントに追加するには、2 つの追加メソッドが Virtual Assistant アクティビティ ハンドラーに含 `OnTeamsTaskModuleFetchAsync` まれています。 `OnTeamsTaskModuleSubmitAsync` これらのメソッドは、仮想アシスタントからタスク モジュール関連のアクティビティをリッスンし、要求に関連付けられたスキルを特定し、特定されたスキルに要求を転送します。 

要求の転送は [、SkillHttpClient メソッドを介](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true)して行 `PostActivityAsync` われます。 これは、解析され、に変換 `InvokeResponse` される応答を返します `TaskModuleResponse` 。


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

カード アクションのディスパッチとタスク モジュールの応答にも同様の方法が実行されます。 タスク モジュールのフェッチと送信のアクション データが更新され、含まれます `skillId` 。 Activity Extension メソッド `GetSkillId` は、呼び出す必要があるスキルの詳細を提供するペイロード `skillId` から抽出します。

コード スニペットと `OnTeamsTaskModuleFetchAsync` メソッド `OnTeamsTaskModuleSubmitAsync` については、次のセクションで説明します。

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

さらに、スキルを介して呼び出されるタスク モジュールが適切にレンダリングされるので、仮想アシスタントのマニフェスト ファイルのセクションに、すべてのスキル ドメイン `validDomains` を含める必要があります。

### <a name="handle-collaborative-app-scopes"></a>共同アプリのスコープを処理する

Teamsは、1:1 チャット、グループ チャット、チャネルなど、複数のスコープに存在できます。 コア仮想アシスタント テンプレートは、1:1 チャット用に設計されています。 オンボーディング エクスペリエンスの一環として、仮想アシスタントはユーザーに名前を求め、ユーザーの状態を維持します。 オンボーディング エクスペリエンスはグループ チャットやチャネル スコープには適していないので、削除されています。

スキルは、1:1 チャット、グループ チャット、チャネル会話など、複数の範囲のアクティビティを処理する必要があります。 これらのスコープがサポートされていない場合、スキルは適切なメッセージで応答する必要があります。

仮想アシスタント コアには、次の処理機能が追加されています。

* 仮想アシスタントは、グループ チャットまたはチャネルからのテキスト メッセージなしで呼び出すことができます。
* メッセージをディスパッチ モジュールに送信する前に、アーティキュレーションがクリーンアップされます。 たとえば、ボットの必要な@mention削除します。

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

### <a name="handle-messaging-extensions"></a>メッセージング拡張機能の処理

メッセージング拡張機能のコマンドは、アプリ マニフェスト ファイルで宣言されます。 メッセージング拡張機能のユーザー インターフェイスには、これらのコマンドが搭載されています。 仮想アシスタントが添付スキルとしてメッセージング拡張機能コマンドに電力を供給するには、仮想アシスタント独自のマニフェストにこれらのコマンドが含まれている必要があります。 個々のスキルのマニフェストから仮想アシスタントのマニフェストにコマンドを追加する必要があります。 コマンド ID は、スキルのアプリ ID を区切り記号で追加することで、関連付けられたスキルに関する情報を提供します `:` 。

スキルのマニフェスト ファイルのスニペットを次のセクションに示します。

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

対応する Virtual Assistant マニフェスト ファイル コード スニペットを次のセクションに示します。

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

コマンドがユーザーによって呼び出されると、仮想アシスタントはコマンド ID を解析して関連スキルを識別し、コマンド ID から追加のサフィックスを削除してアクティビティを更新し、対応するスキルに転送できます。 `:<skill_id>` スキルのコードは、余分な接尾辞を処理する必要はありません。 したがって、スキル間のコマンドの ID 間の競合は回避されます。 この方法では、作成、commandBox、メッセージなど、すべてのコンテキスト内でスキルのすべての検索コマンドとアクションコマンドが仮想アシスタントによって実行されます。

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

メッセージング拡張機能のアクティビティの中には、コマンド ID が含まれるものがあります。 たとえば、呼 `composeExtension/selectItem` び出しタップ アクションの値だけが含まれるとします。 関連付けられたスキルを識別するには、に対する応答を形成している間、各 `skillId`  アイテム カードに添付されます `OnTeamsMessagingExtensionQueryAsync` 。 これは、仮想アシスタントにアダプティブ カードを [追加する方法と似ています](#add-adaptive-cards-to-your-virtual-assistant)。

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

次の例は、Book-a-room アプリ テンプレートを仮想アシスタント スキルに変換する方法を示しています。Book-a-room は Microsoft Teams であり、ユーザーは現在の時刻から 30 分、60 分、または 90 分の会議室をすばやく見つけて予約できます。 既定の時間は 30 分です。 Book-a-room ボットのスコープは、個人用の o**r 1:1 の会話に対応します。 次の図は、部屋のスキルを持つ仮想 **アシスタントを表示** します。

!["部屋を予約する" スキルを持つ仮想アシスタント](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

仮想アシスタントに関連付けられたスキルに変換するために導入されたデルタの変更点を次に示します。 同様のガイドラインに従って、既存の v4 ボットをスキルに変換します。

### <a name="skill-manifest"></a>スキル マニフェスト

スキル マニフェストは、スキルのメッセージング エンドポイント、ID、名前、その他の関連するメタデータを公開する JSON ファイルです。 このマニフェストは、アプリのサイドローディングに使用されるマニフェストとは異Microsoft Teams。 仮想アシスタントには、スキルを添付する入力としてこのファイルへのパスが必要です。 ボットの wwwroot フォルダーに次のマニフェストを追加しました。

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

仮想アシスタントのディスパッチ モデルは、付属のスキルの LUIS モデルの上に構築されています。 ディスパッチ モデルは、すべてのテキスト アクティビティの意図を識別し、関連付けられたスキルを見つける。

仮想アシスタントでは、スキルを添付する場合、入力形式でスキルの LUIS `.lu` モデルが必要です。 LUIS json は `.lu` 、botframework-cli ツールを使用して形式に変換されます。

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

Book-a-room ボットには、ユーザー用の 2 つの主なコマンドがあります。

- `Book room`
- `Manage Favorites`

これら 2 つのコマンドを理解して、LUIS モデルを構築しました。 対応するシークレットを入力する必要があります `cognitivemodels.json` 。 対応する LUIS JSON ファイルは次のページ [で確認できます](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json)。
対応する `.lu` ファイルは、次のセクションに表示されます。

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

この方法では、ユーザーが仮想アシスタントに対して発行したコマンドに関連するコマンド、またはボットに関連付けられたコマンドとして識別され、このスキル `book room` `manage favorites` `Book-a-room` に転送されます。
一方、ボットは、入力が完全ではない場合、これらのコマンドを理解するために LUIS モデル `Book-a-room room` を使用する必要があります。 例: `I want to manage my favorite rooms`。

### <a name="multi-language-support"></a>多言語サポート

たとえば、英語のカルチャのみを持つ LUIS モデルが作成されます。 他の言語に対応する LUIS モデルを作成し、にエントリを追加できます `cognitivemodels.json` 。

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

並行して、対応する `.lu` ファイルを luisFolder パスに追加します。 フォルダー構造は次のとおりです。

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

パラメーターを `languages` 変更するには、botskills コマンドを次のように更新します。

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

仮想アシスタントは、現在 `SetLocaleMiddleware` のロケールを識別し、対応するディスパッチ モデルを呼び出す場合に使用します。 ボット フレームワーク アクティビティには、このミドルウェアで使用されるロケール フィールドがあります。 スキルにも同じ機能を使用できます。 Book-a-room ボットは、このミドルウェアを使用しない代わりに、ボット フレームワーク アクティビティの clientInfo エンティティから [ロケールを取得します](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)。

### <a name="claim-validation"></a>クレーム検証

呼び出し [元をスキルに制限する claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) を追加しました。 仮想アシスタントがこのスキルを呼び出すのを許可するには、その特定の仮想アシスタントのアプリ ID から配列 `AllowedCallers` `appsettings` を設定します。

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

許可された発信者配列は、どのスキルコンシューマーがスキルにアクセスできるのか制限できます。 スキルコンシュー `*` マからの呼び出しを受け入れるには、この配列に 1 つのエントリを追加します。

```
"AllowedCallers": [ "*" ],
```

スキルにクレーム検証を追加する方法の詳細については、「スキルにクレーム検証を追加 [する」を参照してください](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)。

### <a name="limitation-of-card-refresh"></a>カードの更新の制限 

カードの更新などの更新アクティビティは、仮想アシスタント[(github](https://github.com/microsoft/botbuilder-dotnet/issues/3686)の問題) を通じてまだサポートされていません。 したがって、すべてのカード更新呼び出しを新しい `UpdateActivityAsync` カード呼び出しの投稿に置き換えました `SendActivityAsync` 。

### <a name="card-actions-and-task-module-flows"></a>カードアクションとタスク モジュールフロー

カード アクションまたはタスク モジュールアクティビティを関連付けられたスキルに転送するには、スキルを埋め込む `skillId` 必要があります。
`Book-a-room` ボット カードアクション、タスク モジュールのフェッチおよび送信アクション ペイロードは、パラメーターとして格納 `skillId` するために変更されます。 

詳細については、この [ドキュメントのこの](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) セクションを参照してください。

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>グループ チャットまたはチャネル スコープからのアクティビティの処理

`Book-a-room bot` 個人チャットや 1:1 スコープのみなど、プライベート チャット用に設計されています。 グループ チャットとチャネル スコープをサポートするために仮想アシスタントをカスタマイズしましたので、仮想アシスタントをチャネル スコープから呼び出す必要があります。したがって、ボットは同じスコープのアクティビティを `Book-a-room` 取得する必要があります。 したがって `Book-a-room` 、ボットは、これらのアクティビティを処理するためにカスタマイズされます。 ボットのアクティビティ ハンドラー `OnMessageActivityAsync` のチェックイン メソッド `Book-a-room` を確認できます。

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

ボット フレームワーク ソリューション リポジトリの既存の [スキルを活用](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) したり、新しいスキルを最初から完全に作成することもできます。 新しいスキルを作成するには、「 [チュートリアル」を参照して新しいスキルを作成します](https://microsoft.github.io/botframework-solutions/overview/skills/)。 仮想アシスタントとスキル アーキテクチャのドキュメントについては[、「Virtual Assistant and skills architecture」を参照してください](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)。  

## <a name="limitations-of-virtual-assistant"></a>仮想アシスタントの制限事項 

* **EndOfConversation**: スキルは、会話が終了したら `endOfConversation` アクティビティを送信する必要があります。 アクティビティに基づいて、仮想アシスタントは特定のスキルとのコンテキストを終了し、仮想アシスタントのルート コンテキストに戻ります。 Book-a-room ボットの場合、会話が終了する明確な状態はありません。 したがって、ボットから送信していないので、ユーザーがルート コンテキストに戻りたい場合は、コマンド `endOfConversation` `Book-a-room` で簡単に行 `start over` います。  
* **カードの更新**: 仮想アシスタントを通じてカードの更新がまだサポートされていません。  
* **メッセージング拡張機能**:
  * 現在、仮想アシスタントはメッセージング拡張機能に対して最大 10 個のコマンドをサポートできます。
  * メッセージング拡張機能の構成は、個々のコマンドではなく、拡張機能全体に対してスコープ設定されます。 これにより、仮想アシスタントを通じて個々のスキルの構成が制限されます。
  * メッセージング拡張機能コマンドの ID には最大 [64](../resources/schema/manifest-schema.md#composeextensions) 文字の長さ、スキル情報の埋め込みには 37 文字が使用されます。 したがって、コマンド ID の更新された制約は 27 文字に制限されます。

ボット フレームワーク ソリューション リポジトリの既存の [スキルを活用](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) したり、新しいスキルを最初から完全に作成することもできます。 以降のチュートリアルについては、こちらを参照 [してください](https://microsoft.github.io/botframework-solutions/overview/skills/)。 「Virtual Assistant [and skills](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) architecture」のドキュメントを参照してください。

## <a name="code-sample"></a>コード サンプル

| **サンプル名** | **説明** | **C#** | **.NET** |
|----------|-----------------|----------|------------------|
| 更新された visual studio テンプレート | チームの機能をサポートするカスタマイズされたテンプレート。 | [View](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| Book-a-room ボットのスキル コード | 移動中に会議室をすばやく見つけて予約できます。 |  | [View](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |


## <a name="see-also"></a>関連項目

- [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)

- [会議室予約](app-templates.md#book-a-room)

- [Microsoft Teamsボット](../bots/what-are-bots.md)