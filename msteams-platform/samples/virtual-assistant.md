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
# <a name="virtual-assistant-for-microsoft-teams"></a><span data-ttu-id="5337a-104">Microsoft Teams の仮想アシスタント</span><span class="sxs-lookup"><span data-stu-id="5337a-104">Virtual Assistant for Microsoft Teams</span></span>

<span data-ttu-id="5337a-105">仮想アシスタントは、ユーザー エクスペリエンス、組織のブランド化、および必要なデータのフル コントロールを維持しながら、堅牢な会話ソリューションを作成できる Microsoft オープン ソース テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="5337a-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="5337a-106">仮想[](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template)アシスタントコア テンプレートは[、Bot Framework SDK、Language](https://github.com/microsoft/botframework-sdk) [Understanding (FRAMEWORK)](https://www.luis.ai/) [、QnA Maker](https://www.qnamaker.ai/)など、仮想アシスタントの構築に必要な Microsoft テクノロジと、スキルの登録、リンクされたアカウント、さまざまなシームレスな対話とエクスペリエンスをエンド ユーザーに提供するための基本的な会話の意図など、重要な機能をまとめる基本の構成ブロックです。</span><span class="sxs-lookup"><span data-stu-id="5337a-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), as well as essential capabilities including  skills registration, linked accounts, basic conversational intent to offer end users a range of seamless interactions and experiences.</span></span> <span data-ttu-id="5337a-107">さらに、テンプレート機能には、再利用可能な会話スキルの豊富な例が含 [まれます](https://microsoft.github.io/botframework-solutions/overview/skills)。</span><span class="sxs-lookup"><span data-stu-id="5337a-107">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="5337a-108">個々のスキルを仮想アシスタント ソリューションに統合して、複数のシナリオを有効にできます。</span><span class="sxs-lookup"><span data-stu-id="5337a-108">Individual skills can be integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="5337a-109">Bot Framework SDK を使用すると、必要に応じてカスタマイズおよび拡張できるソース コード形式でスキルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5337a-109">Using the Bot Framework SDK, Skills are presented in source code form enabling you to customize and extend as required.</span></span> <span data-ttu-id="5337a-110">「Bot [Framework のスキルとは」を参照してください](https://microsoft.github.io/botframework-solutions/overview/skills/)。</span><span class="sxs-lookup"><span data-stu-id="5337a-110">See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span>

![仮想アシスタントの概要図](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="5337a-112">テキスト メッセージ アクティビティは、ディスパッチ モデルを使用して仮想アシスタント コアによって関連付けられたスキルに [ルーティング](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) されます。</span><span class="sxs-lookup"><span data-stu-id="5337a-112">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="5337a-113">実装に関する考慮事項</span><span class="sxs-lookup"><span data-stu-id="5337a-113">Implementation considerations</span></span>

<span data-ttu-id="5337a-114">仮想アシスタントを追加する決定には、多くの決定性を含め、組織ごとに異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-114">The decision to add a Virtual Assistant can include many determinants and differ for each organization.</span></span> <span data-ttu-id="5337a-115">組織の仮想アシスタントの実装をサポートする要因を次に示します。</span><span class="sxs-lookup"><span data-stu-id="5337a-115">Here are the factors that support implementing a Virtual Assistant for your organization:</span></span>

- <span data-ttu-id="5337a-116">中央チームは、すべての従業員のエクスペリエンスを管理し、仮想アシスタント エクスペリエンスを構築し、新しいスキルの追加を含むコア エクスペリエンスの更新を管理する機能を備えています。</span><span class="sxs-lookup"><span data-stu-id="5337a-116">A central team manages all employee experiences and has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
- <span data-ttu-id="5337a-117">複数のアプリケーションが複数のビジネス機能に存在したり、その数が将来増える見込みです。</span><span class="sxs-lookup"><span data-stu-id="5337a-117">Multiple applications exist across business functions and/or the number is expected to grow in the future.</span></span>
- <span data-ttu-id="5337a-118">既存のアプリケーションはカスタマイズ可能で、組織が所有し、仮想アシスタントのスキルに変換できます。</span><span class="sxs-lookup"><span data-stu-id="5337a-118">Existing applications are customizable, owned by the organization, and can be converted into skills for a Virtual Assistant.</span></span>
- <span data-ttu-id="5337a-119">中央の従業員エクスペリエンス チームは、既存のアプリのカスタマイズに影響を与え、既存のアプリケーションを仮想アシスタントエクスペリエンスのスキルとして統合するために必要なガイダンスを提供できます。</span><span class="sxs-lookup"><span data-stu-id="5337a-119">The central employee-experiences team is able to influence customizations to existing apps and provide necessary guidance for integrating existing applications as skills in Virtual Assistant experience</span></span>

![中央チームがアシスタントを管理し、ビジネス機能チームがスキルを貢献する](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="5337a-121">Teams に重点を置く仮想アシスタントを作成する</span><span class="sxs-lookup"><span data-stu-id="5337a-121">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="5337a-122">Microsoft は、仮想アシスタント [Visual Studio構築のための](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) 新しいテンプレートを公開しました。</span><span class="sxs-lookup"><span data-stu-id="5337a-122">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="5337a-123">新しいVisual Studioテンプレートを使用すると、アクションを含む限られたリッチ カードをサポートするテキスト ベースのエクスペリエンスを利用した仮想アシスタントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="5337a-123">With the Visual Studio template, you can create a Virtual Assistant, powered by a text-based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="5337a-124">Microsoft Teams プラットフォーム機能をVisual Studio Teams アプリエクスペリエンスを強化するために、新しい基本テンプレートが強化されました。</span><span class="sxs-lookup"><span data-stu-id="5337a-124">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="5337a-125">機能のいくつかには、豊富なアダプティブ カード、タスク モジュール、チーム/グループ チャット、メッセージング拡張機能のサポートが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5337a-125">A few of the capabilities include support for rich adaptive cards, task modules, teams/group chats and messaging extensions.</span></span> <span data-ttu-id="5337a-126">*「チュートリアル:* 仮想 [アシスタントを Microsoft Teams に拡張する」も参照してください](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)。</span><span class="sxs-lookup"><span data-stu-id="5337a-126">*See also*, [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>

![仮想アシスタント ソリューションの大きな図](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="5337a-128">アダプティブ カードを仮想アシスタントに追加する</span><span class="sxs-lookup"><span data-stu-id="5337a-128">Add adaptive cards to your Virtual Assistant</span></span>

<span data-ttu-id="5337a-129">要求を適切にディスパッチするには、仮想アシスタントが適切な THEIS モデルとそれに関連付けられているスキルを識別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-129">To dispatch requests properly, your Virtual Assistant needs to identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="5337a-130">ただし、ユーザーからの発声ではなく、定義済みの固定キーワードで、スキルに関連付けられたカード アクション テキストに対してトレーニングを受けできない可能性があります。このため、ディスパッチメカニズムはカード アクション アクティビティには使用できません。</span><span class="sxs-lookup"><span data-stu-id="5337a-130">However, the dispatching mechanism cannot be used for card action activities since the LUIS model associated with a skill may not be trained for card action texts since these are fixed, pre-defined keywords, not utterances from a user.</span></span>

<span data-ttu-id="5337a-131">この問題を解決するには、スキル情報をカードアクションペイロードに埋め込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-131">We have resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="5337a-132">すべてのスキルはカード `skillId` アクションの  `value` フィールドに埋め込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-132">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="5337a-133">これは、各カード アクション アクティビティが関連するスキル情報を持ち、仮想アシスタントがディスパッチにこの情報を利用できる最善の方法です。</span><span class="sxs-lookup"><span data-stu-id="5337a-133">This is the best way to ensure that each card action activity carries the relevant skill information and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="5337a-134">カード アクション データのサンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="5337a-134">Below is a card action data sample.</span></span> <span data-ttu-id="5337a-135">コンストラクターを `skillId` 指定することで、スキル情報が常にカード アクションに存在する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-135">By providing `skillId` in the constructor we ensure that skill information is always present in card actions.</span></span>

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

<span data-ttu-id="5337a-136">次に、仮想アシスタント `SkillCardActionData` テンプレートのクラスを導入して、カード `skillId` アクションペイロードから抽出します。</span><span class="sxs-lookup"><span data-stu-id="5337a-136">Next, we introduce `SkillCardActionData` class in the Virtual Assistant template to extract `skillId` from the card action payload.</span></span>

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

<span data-ttu-id="5337a-137">カードのアクション データから抽出するコード  `skillId` スニペットを次に示します。</span><span class="sxs-lookup"><span data-stu-id="5337a-137">Below is a code snippet to extract  `skillId` from card action data.</span></span> <span data-ttu-id="5337a-138">Activity クラスに拡張メソッドとして [実装](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) しました。</span><span class="sxs-lookup"><span data-stu-id="5337a-138">We implemented it as an  extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>

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

### <a name="handle-interruptions-gracefully"></a><span data-ttu-id="5337a-139">中断を適切に処理する</span><span class="sxs-lookup"><span data-stu-id="5337a-139">Handle interruptions gracefully</span></span>

<span data-ttu-id="5337a-140">仮想アシスタントは、別のスキルが現在アクティブな間にユーザーがスキルを呼び出そうとする場合に、中断を処理できます。</span><span class="sxs-lookup"><span data-stu-id="5337a-140">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="5337a-141">Bot Framework の `TeamsSkillDialog` `TeamsSwitchSkillDialog` [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) と [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)に基づいて、ユーザーがカードアクションからスキル エクスペリエンスを切り替え可能にしました。</span><span class="sxs-lookup"><span data-stu-id="5337a-141">we have introduced `TeamsSkillDialog` and `TeamsSwitchSkillDialog`, based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), to enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="5337a-142">この要求を処理するために、仮想アシスタントは、スキルを切り替える確認メッセージをユーザーに表示します。</span><span class="sxs-lookup"><span data-stu-id="5337a-142">To handle this request the Virtual Assistant prompts the user with a confirmation message to switch skills.</span></span>

![新しいスキルに切り替える際の確認プロンプト](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a><span data-ttu-id="5337a-144">タスク モジュール要求の処理</span><span class="sxs-lookup"><span data-stu-id="5337a-144">Handling task module requests</span></span>

<span data-ttu-id="5337a-145">仮想アシスタントにタスク モジュール機能を追加するには、仮想アシスタント アクティビティ ハンドラーに次の 2 つの追加メソッドが含 `OnTeamsTaskModuleFetchAsync` まれています `OnTeamsTaskModuleSubmitAsync` 。</span><span class="sxs-lookup"><span data-stu-id="5337a-145">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="5337a-146">これらのメソッドは、仮想アシスタントからタスク モジュール関連のアクティビティをリッスンし、要求に関連付けられているスキルを特定し、識別されたスキルに要求を転送します。</span><span class="sxs-lookup"><span data-stu-id="5337a-146">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="5337a-147">要求の転送は  [、SkillHttpClient メソッドを使用](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable)して行 `PostActivityAsync` われます。</span><span class="sxs-lookup"><span data-stu-id="5337a-147">Request forwarding is done via the  [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable), `PostActivityAsync` method.</span></span> <span data-ttu-id="5337a-148">これは、解析され、 `InvokeResponse` 変換された応答を返します `TaskModuleResponse` 。</span><span class="sxs-lookup"><span data-stu-id="5337a-148">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>

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

<span data-ttu-id="5337a-149">カード アクションのディスパッチとタスク モジュールの応答にも同様のアプローチが使用されます。</span><span class="sxs-lookup"><span data-stu-id="5337a-149">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="5337a-150">タスク モジュールのフェッチと送信のアクション データが更新され、含まれます `skillId` 。</span><span class="sxs-lookup"><span data-stu-id="5337a-150">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="5337a-151">Activity Extension メソッド `GetSkillId` は、呼び出す必要があるスキルに関する詳細を提供するペイロード `skillId` から抽出します。</span><span class="sxs-lookup"><span data-stu-id="5337a-151">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="5337a-152">次のコード スニペットと `OnTeamsTaskModuleFetchAsync` メソッドを `OnTeamsTaskModuleSubmitAsync` 示します。</span><span class="sxs-lookup"><span data-stu-id="5337a-152">Below is a code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods.</span></span>

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

<span data-ttu-id="5337a-153">さらに、スキルによって呼び出されるタスク モジュールが適切にレンダリングされるには、すべてのスキル ドメインを仮想アシスタントのマニフェスト ファイルのセクション `validDomains` に含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-153">Additionally, all skill domains must be included in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked via a skill render properly.</span></span>

### <a name="handling-collaborative-app-scopes"></a><span data-ttu-id="5337a-154">共同作業アプリのスコープの処理</span><span class="sxs-lookup"><span data-stu-id="5337a-154">Handling collaborative app scopes</span></span>

<span data-ttu-id="5337a-155">Teams アプリは、1 対 1 のチャット、グループ チャット、チャネルなど、複数のスコープで存在できます。</span><span class="sxs-lookup"><span data-stu-id="5337a-155">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="5337a-156">コア仮想アシスタント テンプレートは、1 対 1 のチャット用に設計されています。</span><span class="sxs-lookup"><span data-stu-id="5337a-156">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="5337a-157">オンボーディング エクスペリエンスの一環として、仮想アシスタントはユーザーに名前の入力を求め、ユーザーの状態を維持します。</span><span class="sxs-lookup"><span data-stu-id="5337a-157">As part of the onboarding experience Virtual Assistant  prompts users for name and maintains user state.</span></span> <span data-ttu-id="5337a-158">オンボーディング エクスペリエンスはグループ チャット/チャネル スコープには適していないので、削除されています。</span><span class="sxs-lookup"><span data-stu-id="5337a-158">Since that onboarding experience is not suited for group chat/channel scopes it has been removed.</span></span>

<span data-ttu-id="5337a-159">スキルは、複数の範囲 (1 対 1 のチャット、グループ チャット、チャネル会話) のアクティビティを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-159">Skills should handle activities in multiple scopes (1:1 chat, group chat, and channel conversation).</span></span> <span data-ttu-id="5337a-160">これらのスコープがサポートされていない場合、スキルは適切なメッセージで応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-160">If any of these scopes are not supported, skills should respond with an appropriate message.</span></span>

<span data-ttu-id="5337a-161">次の処理機能が仮想アシスタント コアに追加されました。</span><span class="sxs-lookup"><span data-stu-id="5337a-161">The following  processing functions have been added to Virtual Assistant core:</span></span>

- <span data-ttu-id="5337a-162">仮想アシスタントは、グループ チャットまたはチャネルからのテキスト メッセージなしで呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="5337a-162">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
- <span data-ttu-id="5337a-163">メッセージをディスパッチ モジュールに送信する前に、明確化がクリーンアップされます (つまり、ボットの@mentionを削除します)。</span><span class="sxs-lookup"><span data-stu-id="5337a-163">Articulations are cleaned (i.e.,  remove the necessary @mention of the bot) before sending the message to the dispatch module.</span></span>

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

### <a name="handling-messaging-extensions"></a><span data-ttu-id="5337a-164">メッセージング拡張機能の処理</span><span class="sxs-lookup"><span data-stu-id="5337a-164">Handling messaging extensions</span></span>

<span data-ttu-id="5337a-165">メッセージング拡張機能のコマンドは、アプリ マニフェスト ファイルで宣言されています。</span><span class="sxs-lookup"><span data-stu-id="5337a-165">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="5337a-166">メッセージング拡張機能のユーザー インターフェイスには、これらのコマンドが搭載されています。</span><span class="sxs-lookup"><span data-stu-id="5337a-166">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="5337a-167">仮想アシスタントがメッセージング拡張機能コマンドの電源を入れるには (付属のスキルとして)、仮想アシスタント独自のマニフェストにこれらのコマンドが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-167">For a Virtual Assistant to power a messaging extension command (as an attached skill), a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="5337a-168">個々のスキルのマニフェストのコマンドも仮想アシスタントのマニフェストに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-168">The commands from an individual skill's manifest should be added to the Virtual Assistant's manifest as well.</span></span> <span data-ttu-id="5337a-169">コマンド ID は、スキルのアプリ ID を区切り記号 ( ) を介して追加することで、関連付けられたスキルに関する情報を提供します `:` 。</span><span class="sxs-lookup"><span data-stu-id="5337a-169">The command ID provides information about an associated skill by appending the skill's app ID via a separator (`:`).</span></span>

<span data-ttu-id="5337a-170">スキルのマニフェスト ファイルのスニペットを次に示します。</span><span class="sxs-lookup"><span data-stu-id="5337a-170">Below is a snippet from a skill's manifest file.</span></span>

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

<span data-ttu-id="5337a-171">対応する仮想アシスタント マニフェスト ファイル コード スニペットを次に示します。</span><span class="sxs-lookup"><span data-stu-id="5337a-171">And, below is the corresponding Virtual Assistant manifest file code snippet.</span></span>

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

<span data-ttu-id="5337a-172">ユーザーによってコマンドが呼び出されると、仮想アシスタントは、コマンド ID を解析して関連付けられたスキルを識別し、コマンド ID から余分なサフィックス ( ) を削除してアクティビティを更新し、対応するスキルに転送できます。 `:<skill_id>`</span><span class="sxs-lookup"><span data-stu-id="5337a-172">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix (`:<skill_id>`) from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="5337a-173">スキルのコードは余分なサフィックスを処理する必要はありません。したがって、スキル間のコマンドの ID 間の競合は回避されます。</span><span class="sxs-lookup"><span data-stu-id="5337a-173">The code for a skill doesn't need to handle the extra suffix, thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="5337a-174">この方法では、すべてのコンテキスト内のスキルのすべての検索コマンドとアクション コマンド ("compose"、"commandBox"、および "message") を仮想アシスタントが利用できます。</span><span class="sxs-lookup"><span data-stu-id="5337a-174">With this approach, all the search and action commands of a skill within all contexts ("compose", "commandBox" and "message") can be powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="5337a-175">メッセージング拡張機能のアクティビティの中には、コマンド ID が含まれるものがあります。</span><span class="sxs-lookup"><span data-stu-id="5337a-175">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="5337a-176">たとえば、呼 `composeExtension/selectItem` び出しタップ アクションの値だけが含まれているとします。</span><span class="sxs-lookup"><span data-stu-id="5337a-176">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="5337a-177">関連するスキルを識別するために、応答を形成している間に各アイテム `skillId`  カードに添付されます `OnTeamsMessagingExtensionQueryAsync` 。</span><span class="sxs-lookup"><span data-stu-id="5337a-177">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="5337a-178">(これは、アダプティブ カードを仮想アシスタント [に追加する方法に似ています](#add-adaptive-cards-to-your-virtual-assistant)。</span><span class="sxs-lookup"><span data-stu-id="5337a-178">(This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a><span data-ttu-id="5337a-179">例: ブック ルーム アプリ テンプレートを仮想アシスタントのスキルに変換する</span><span class="sxs-lookup"><span data-stu-id="5337a-179">Example: Convert the Book-a-room app template to a Virtual Assistant skill</span></span>

<span data-ttu-id="5337a-180">[会議室](app-templates.md#book-a-room) の予約は [、ユーザー](../bots/what-are-bots.md) が現在の時刻から 30 分 (既定)、60 分、または 90 分間の会議室をすばやく見つけて予約できる Microsoft Teams ボットです。</span><span class="sxs-lookup"><span data-stu-id="5337a-180">[Book-a-room](app-templates.md#book-a-room) is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="5337a-181">会議室予約ボットは、個人の会話または一対一の会話を対象としています。</span><span class="sxs-lookup"><span data-stu-id="5337a-181">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

!["部屋を予約する" スキルを持つ仮想アシスタント](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="5337a-183">仮想アシスタントにアタッチできるスキルに変換するために導入された差分の変更を次に示します。</span><span class="sxs-lookup"><span data-stu-id="5337a-183">Followings are the delta changes introduced to convert it to a skill which can be attached to a Virtual Assistant.</span></span> <span data-ttu-id="5337a-184">同様のガイドラインに従って、既存の v4 ボットをスキルに変換できます。</span><span class="sxs-lookup"><span data-stu-id="5337a-184">Similar guidelines can be followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="5337a-185">スキル マニフェスト</span><span class="sxs-lookup"><span data-stu-id="5337a-185">Skill manifest</span></span>

<span data-ttu-id="5337a-186">スキル マニフェストは、スキルのメッセージング エンドポイント、ID、名前、その他の関連するメタデータを公開する JSON ファイルです (このマニフェストは、Microsoft Teams でアプリをサイドロードするために使用されるマニフェストとは異なります)。仮想アシスタントは、スキルを添付する入力としてこのファイルへのパスを必要とします。</span><span class="sxs-lookup"><span data-stu-id="5337a-186">A skill manifest is a JSON file that exposes a skill's messaging endpoint, id, name, and other relevant metadata (this manifest is different than the manifest used for sideloading an app in Microsoft Teams) A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="5337a-187">ボットの wwwroot フォルダーに次のマニフェストを追加しました。</span><span class="sxs-lookup"><span data-stu-id="5337a-187">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="5337a-188">[!!--]--</span><span class="sxs-lookup"><span data-stu-id="5337a-188">LUIS Integration</span></span>

<span data-ttu-id="5337a-189">仮想アシスタントのディスパッチ モデルは、アタッチされたスキルの数を持つ OF モデルを基に構築されています。</span><span class="sxs-lookup"><span data-stu-id="5337a-189">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="5337a-190">ディスパッチ モデルは、すべてのテキスト アクティビティの意図を識別し、関連付けられているスキルを見つけ出します。</span><span class="sxs-lookup"><span data-stu-id="5337a-190">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="5337a-191">仮想アシスタントでは、スキルを追加する一方で、入力としてスキルの (形式で) スキルの種類 `.lu` (形式) が必要です。</span><span class="sxs-lookup"><span data-stu-id="5337a-191">Virtual Assistant requires skill's LUIS model (in `.lu` format) as an input while attaching a skill.</span></span> <span data-ttu-id="5337a-192">BOTframework-cli ツールを使用して、JSON を形式 `.lu` に変換できます。</span><span class="sxs-lookup"><span data-stu-id="5337a-192">LUIS json can be converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="5337a-193">Book-a-room ボットには、ユーザーに対して次の 2 つの主なコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="5337a-193">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="5337a-194">これら 2 つのコマンドを理解する、1 つの大きなモデルを構築しました。</span><span class="sxs-lookup"><span data-stu-id="5337a-194">We have built a LUIS model understanding these two commands.</span></span> <span data-ttu-id="5337a-195">対応するシークレットを設定する必要があります `cognitivemodels.json` 。</span><span class="sxs-lookup"><span data-stu-id="5337a-195">Corresponding secrets need to be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="5337a-196">対応する JSON ファイルはここに [見つか](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) り、対応するファイルは `.lu` 次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="5337a-196">The corresponding LUIS JSON file can be found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) and this is how the corresponding `.lu` file looks like.</span></span>

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

<span data-ttu-id="5337a-197">この方法では、仮想アシスタントに関連するユーザーによるコマンドの問題、または `book room` Book-a-room ボットに関連付けられたコマンドとして識別されるコマンドは、このスキルに転送 `manage favorites` されます。</span><span class="sxs-lookup"><span data-stu-id="5337a-197">With this approach, any command issues by a user to Virtual Assistant related to `book room` or `manage favorites` can be identified as a command associated with Book-a-room bot and is forwarded to this skill.</span></span>
<span data-ttu-id="5337a-198">一方、BOOK-a-room room bot は、これらのコマンドが入力されていない場合は、このモデルを使用してこれらのコマンドを理解する必要があります (次に例を示します `I want to manage my favorite rooms` )。</span><span class="sxs-lookup"><span data-stu-id="5337a-198">On the other hand, Book-a-room room bot needs to use LUIS model to understand these commands if they are not typed as is (for example: `I want to manage my favorite rooms`).</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="5337a-199">複数言語のサポート</span><span class="sxs-lookup"><span data-stu-id="5337a-199">Multi-Language support</span></span>

<span data-ttu-id="5337a-200">この例では、英語のカルチャを持つ、唯一の種類のオブジェクト モデルを作成しました。</span><span class="sxs-lookup"><span data-stu-id="5337a-200">For this example, we have only created a LUIS model with English culture.</span></span> <span data-ttu-id="5337a-201">他の言語に対応する数型 (-) のモデルを作成し、エントリを追加できます `cognitivemodels.json` 。</span><span class="sxs-lookup"><span data-stu-id="5337a-201">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="5337a-202">並行して、対応する `.lu` ファイルをfolder パスに追加します。</span><span class="sxs-lookup"><span data-stu-id="5337a-202">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="5337a-203">フォルダーの構造は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5337a-203">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="5337a-204">botskills コマンドを次のように更新してパラメーターを変更 `languages` します。</span><span class="sxs-lookup"><span data-stu-id="5337a-204">Update botskills command as follows to modify `languages` parameter:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="5337a-205">仮想アシスタントは、 `SetLocaleMiddleware` 現在のロケールを識別し、対応するディスパッチ モデルを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5337a-205">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="5337a-206">(Bot フレームワーク アクティビティには、このミドルウェアで使用されるロケール フィールドがあります)。スキルにも同じ機能を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5337a-206">(Bot framework activity has locale field which is used by this middleware.) We recommend to use the same for your skill as well.</span></span> <span data-ttu-id="5337a-207">Book-a-room bot は、このミドルウェアを使用しません。代わりに、Bot フレームワーク アクティビティの clientInfo エンティティから [ロケールを取得します](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)。</span><span class="sxs-lookup"><span data-stu-id="5337a-207">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="5337a-208">要求の検証</span><span class="sxs-lookup"><span data-stu-id="5337a-208">Claim validation</span></span>

<span data-ttu-id="5337a-209">呼び出し [元をスキルに制限するために claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) が追加されました。</span><span class="sxs-lookup"><span data-stu-id="5337a-209">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="5337a-210">仮想アシスタントがこのスキルを呼び出すのを許可するには、その特定の仮想アシスタントのアプリ ID から `AllowedCallers` `appsettings` 配列を設定します。</span><span class="sxs-lookup"><span data-stu-id="5337a-210">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="5337a-211">許可された呼び出し元の配列では、ユーザーがスキルにアクセスできるスキルを制限できます。</span><span class="sxs-lookup"><span data-stu-id="5337a-211">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="5337a-212">任意のスキル コンシューマー `*` からの呼び出しを受け入れるには、この配列に単一のエントリを追加します。</span><span class="sxs-lookup"><span data-stu-id="5337a-212">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```
<span data-ttu-id="5337a-213">スキルにクレーム検証を追加する詳細なドキュメントについては、こちらを参照 [してください](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)。</span><span class="sxs-lookup"><span data-stu-id="5337a-213">Detailed documentation for adding claims validation to a skill can be found [here](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator).</span></span>

### <a name="card-refresh-limitation"></a><span data-ttu-id="5337a-214">カードの更新の制限</span><span class="sxs-lookup"><span data-stu-id="5337a-214">Card refresh limitation</span></span>

<span data-ttu-id="5337a-215">アクティビティの更新 (カードの更新) は、仮想アシスタント[(github](https://github.com/microsoft/botbuilder-dotnet/issues/3686)の問題) ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="5337a-215">Updating activity (card refresh) is not supported yet via Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="5337a-216">そのため、すべてのカード更新呼び出し ( ) を新しいカード呼び出し ( ) の投稿 `UpdateActivityAsync` に置き換えました `SendActivityAsync` 。</span><span class="sxs-lookup"><span data-stu-id="5337a-216">Hence, we have replaced all card refresh calls (`UpdateActivityAsync`) with posting new card calls(`SendActivityAsync`).</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="5337a-217">カード アクションとタスク モジュール フロー</span><span class="sxs-lookup"><span data-stu-id="5337a-217">Card actions and task module flows</span></span>

<span data-ttu-id="5337a-218">カードアクションまたはタスク モジュールアクティビティを関連付けられたスキルに転送するには、スキルをそのスキルに埋め込む `skillId` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-218">To forward card action or task module activities to an associated skill, the skill needs to embed `skillId` to it.</span></span>
<span data-ttu-id="5337a-219">Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span><span class="sxs-lookup"><span data-stu-id="5337a-219">Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="5337a-220">詳細については、このドキュメント [のこの](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5337a-220">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="5337a-221">グループ チャットまたはチャネル スコープからのアクティビティの処理</span><span class="sxs-lookup"><span data-stu-id="5337a-221">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="5337a-222">Book-a-room ボットは、プライベート チャット (個人用/1:1 スコープ) 専用に設計されています。</span><span class="sxs-lookup"><span data-stu-id="5337a-222">Book-a-room bot is designed for private chats (personal/1:1 scope) only.</span></span> <span data-ttu-id="5337a-223">グループ チャットとチャネルスコープをサポートするために仮想アシスタントをカスタマイズしたので、仮想アシスタントがこれらのスコープから呼び出される可能性があります。したがって、Book-a-room ボットは同じアクティビティを取得する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-223">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant might be invoked from these scopes and thus, Book-a-room bot might get activities for the same.</span></span> <span data-ttu-id="5337a-224">したがって、ブック ルーム ボットは、これらのアクティビティを処理するためにカスタマイズされます。</span><span class="sxs-lookup"><span data-stu-id="5337a-224">Hence Book-a-room bot is customized to handle those activities.</span></span> <span data-ttu-id="5337a-225">チェックは `OnMessageActivityAsync` 、Book-a-room ボットのアクティビティ ハンドラーのメソッドに入れらされています。</span><span class="sxs-lookup"><span data-stu-id="5337a-225">The check has been put in `OnMessageActivityAsync` methods of Book-a-room bot's activity handler.</span></span>

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

<span data-ttu-id="5337a-226">[Bot Framework](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp)ソリューション リポジトリの既存のスキルを活用したり、新しいスキルを最初から完全に作成したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="5337a-226">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="5337a-227">以降のチュートリアルについては、こちらを参照 [してください](https://microsoft.github.io/botframework-solutions/overview/skills/)。</span><span class="sxs-lookup"><span data-stu-id="5337a-227">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="5337a-228">仮想アシスタントと [スキル アーキテクチャ](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5337a-228">Please refer to [documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   for Virtual Assistant and skills architecture.</span></span>

## <a name="sample-code-to-get-started"></a><span data-ttu-id="5337a-229">開始するサンプル コード</span><span class="sxs-lookup"><span data-stu-id="5337a-229">Sample code to get started</span></span>

- [<span data-ttu-id="5337a-230">Visual Studio テンプレートの更新</span><span class="sxs-lookup"><span data-stu-id="5337a-230">Updated visual studio template</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [<span data-ttu-id="5337a-231">Book-a-room ボットのスキル コード</span><span class="sxs-lookup"><span data-stu-id="5337a-231">Book-a-room bot skill code</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a><span data-ttu-id="5337a-232">仮想アシスタントの既知の制限事項</span><span class="sxs-lookup"><span data-stu-id="5337a-232">Virtual Assistant known limitations</span></span>

- <span data-ttu-id="5337a-233">**EndOfConversation**.</span><span class="sxs-lookup"><span data-stu-id="5337a-233">**EndOfConversation**.</span></span> <span data-ttu-id="5337a-234">スキルは会話を終了 `endOfConversation` するときにアクティビティを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5337a-234">A skill should send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="5337a-235">このアクティビティに基づいて、仮想アシスタントは特定のスキルを持つコンテキストを終了し、仮想アシスタント (ルート) コンテキストに戻ります。</span><span class="sxs-lookup"><span data-stu-id="5337a-235">basis this activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's (root) context.</span></span> <span data-ttu-id="5337a-236">Book-a-room ボットの場合、会話を終了できる明確な状態はありません。</span><span class="sxs-lookup"><span data-stu-id="5337a-236">For Book-a-room bot, there is no clear state where conversation can be ended.</span></span> <span data-ttu-id="5337a-237">そのため、Book-a-room ボットから送信したのではなく、ユーザーがルート コンテキストに戻る必要がある場合は、コマンドを使用するだけで `endOfConversation` 行 `start over` えるのです。</span><span class="sxs-lookup"><span data-stu-id="5337a-237">Hence we have not sent `endOfConversation` from Book-a-room bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>
- <span data-ttu-id="5337a-238">**カードの更新**。</span><span class="sxs-lookup"><span data-stu-id="5337a-238">**Card refresh**.</span></span> <span data-ttu-id="5337a-239">カードの更新は、仮想アシスタントを通じてまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="5337a-239">Card refreshes is not yet supported through Virtual Assistant.</span></span>
- <span data-ttu-id="5337a-240">**メッセージング拡張機能**。:</span><span class="sxs-lookup"><span data-stu-id="5337a-240">**Messaging extensions**.:</span></span>
  - <span data-ttu-id="5337a-241">現在、仮想アシスタントはメッセージング拡張機能に対して最大 10 個のコマンドをサポートできます。</span><span class="sxs-lookup"><span data-stu-id="5337a-241">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  - <span data-ttu-id="5337a-242">メッセージング拡張機能の構成は、個々のコマンドではなく、拡張機能全体を対象とします。</span><span class="sxs-lookup"><span data-stu-id="5337a-242">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="5337a-243">これにより、仮想アシスタントを通じて個々のスキルの構成が制限されます。</span><span class="sxs-lookup"><span data-stu-id="5337a-243">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  - <span data-ttu-id="5337a-244">メッセージング拡張機能コマンドの ID の長さは最大 [64](../resources/schema/manifest-schema.md#composeextensions) 文字で、スキル情報の埋め込みには 37 文字が使用されます。</span><span class="sxs-lookup"><span data-stu-id="5337a-244">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters will be used for embedding skill information.</span></span> <span data-ttu-id="5337a-245">したがって、コマンド ID の更新された制約は 27 文字に制限されています。</span><span class="sxs-lookup"><span data-stu-id="5337a-245">Thus, updated constraints for command ID are limited to 27 characters.</span></span>
>
>
