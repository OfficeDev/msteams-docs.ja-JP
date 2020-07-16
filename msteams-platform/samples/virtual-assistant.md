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
# <a name="virtual-assistant-for-microsoft-teams"></a><span data-ttu-id="df2d5-104">Microsoft Teams の仮想アシスタント</span><span class="sxs-lookup"><span data-stu-id="df2d5-104">Virtual Assistant for Microsoft Teams</span></span>

<span data-ttu-id="df2d5-105">仮想アシスタントは、ユーザーの操作、組織のブランド化、必要なデータのフルコントロールを維持しながら、強力な会話ソリューションを作成できる、Microsoft のオープンソーステンプレートです。</span><span class="sxs-lookup"><span data-stu-id="df2d5-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="df2d5-106">[仮想アシスタントコアテンプレート](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template)は基本的なビルディングブロックであり、[ボット Framework SDK](https://github.com/microsoft/botframework-sdk)、[言語の理解 (LUIS)](https://www.luis.ai/)、 [qna](https://www.qnamaker.ai/)の開発者、スキルの登録、リンクされたアカウント、基本会話など、エンドユーザーにシームレスな対話とエクスペリエンスの範囲を提供する基本的な機能を含む、仮想アシスタントの構築に必要な Microsoft テクノロジを統合したものです。</span><span class="sxs-lookup"><span data-stu-id="df2d5-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), as well as essential capabilities including  skills registration, linked accounts, basic conversational intent to offer end users a range of seamless interactions and experiences.</span></span> <span data-ttu-id="df2d5-107">さらに、テンプレート機能には、再利用可能な会話[スキル](https://microsoft.github.io/botframework-solutions/overview/skills)の豊富な例も含まれています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-107">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="df2d5-108">個々のスキルを仮想アシスタントソリューションに統合して、複数のシナリオを有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-108">Individual skills can be integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="df2d5-109">Bot フレームワーク SDK を使用すると、スキルがソースコードの形式で表示され、必要に応じてカスタマイズおよび拡張することができます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-109">Using the Bot Framework SDK, Skills are presented in source code form enabling you to customize and extend as required.</span></span> <span data-ttu-id="df2d5-110">[Bot フレームワークのスキル](https://microsoft.github.io/botframework-solutions/overview/skills/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="df2d5-110">See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span>

![仮想アシスタントの概要図](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="df2d5-112">テキストメッセージアクティビティは、[ディスパッチ](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs)モデルを使用して仮想アシスタントコアによって関連付けられたスキルにルーティングされます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-112">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="df2d5-113">実装に関する考慮事項</span><span class="sxs-lookup"><span data-stu-id="df2d5-113">Implementation considerations</span></span>

<span data-ttu-id="df2d5-114">仮想アシスタントを追加するかどうかの決定には、組織ごとにさまざまな式を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-114">The decision to add a Virtual Assistant can include many determinants and differ for each organization.</span></span> <span data-ttu-id="df2d5-115">組織の仮想アシスタントの実装をサポートする要因を次に示します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-115">Here are the factors that support implementing a Virtual Assistant for your organization:</span></span>

- <span data-ttu-id="df2d5-116">中央チームは、すべての従業員エクスペリエンスを管理し、新しいスキルの追加など、中核となるエクスペリエンスの更新プログラムを管理する機能を備えています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-116">A central team manages all employee experiences and has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
- <span data-ttu-id="df2d5-117">複数のアプリケーションが複数のビジネス機能にわたって存在するか、または将来の増加が予想されます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-117">Multiple applications exist across business functions and/or the number is expected to grow in the future.</span></span>
- <span data-ttu-id="df2d5-118">既存のアプリケーションは、組織が所有するカスタマイズが可能であり、仮想アシスタントのスキルに変換することができます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-118">Existing applications are customizable, owned by the organization, and can be converted into skills for a Virtual Assistant.</span></span>
- <span data-ttu-id="df2d5-119">中央従業員エクスペリエンスチームは、既存のアプリにカスタマイズを反映して、既存のアプリケーションを仮想アシスタントエクスペリエンスのスキルとして統合するために必要なガイダンスを提供することができます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-119">The central employee-experiences team is able to influence customizations to existing apps and provide necessary guidance for integrating existing applications as skills in Virtual Assistant experience</span></span>

![中央チームがアシスタントを管理し、ビジネス機能チームがスキルを貢献](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="df2d5-121">Teams に特化した仮想アシスタントを作成する</span><span class="sxs-lookup"><span data-stu-id="df2d5-121">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="df2d5-122">Microsoft は、仮想アシスタントとスキルを構築するための[Visual Studio テンプレート](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate)を公開しています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-122">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="df2d5-123">Visual Studio テンプレートを使用すると、アクションを備えた限られたリッチカードのサポートを提供して、テキストベースの操作で提供される仮想アシスタントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-123">With the Visual Studio template, you can create a Virtual Assistant, powered by a text-based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="df2d5-124">Visual Studio の基本テンプレートが拡張され、Microsoft Teams のプラットフォーム機能と power Teams アプリのエクスペリエンスが追加されました。</span><span class="sxs-lookup"><span data-stu-id="df2d5-124">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="df2d5-125">豊富なアダプティブカード、タスクモジュール、teams/グループチャット、メッセージング拡張機能のサポートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-125">A few of the capabilities include support for rich adaptive cards, task modules, teams/group chats and messaging extensions.</span></span> <span data-ttu-id="df2d5-126">「[チュートリアル: 仮想アシスタントを Microsoft Teams に拡張する](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/) *」も参照して*ください。</span><span class="sxs-lookup"><span data-stu-id="df2d5-126">*See also*, [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>

![仮想アシスタントソリューションの高レベルの図](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="df2d5-128">仮想アシスタントに適応カードを追加する</span><span class="sxs-lookup"><span data-stu-id="df2d5-128">Add adaptive cards to your Virtual Assistant</span></span>

<span data-ttu-id="df2d5-129">要求を適切にディスパッチするには、仮想アシスタントが正しい LUIS モデルとそれに関連するスキルを特定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-129">To dispatch requests properly, your Virtual Assistant needs to identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="df2d5-130">ただし、これらは固定された定義済みのキーワードであり、ユーザーからの utterances ではないため、カードアクションの処理に対しては、そのスキルに関連付けられている LUIS モデルを使用することはできないため、ディスパッチメカニズムを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="df2d5-130">However, the dispatching mechanism cannot be used for card action activities since the LUIS model associated with a skill may not be trained for card action texts since these are fixed, pre-defined keywords, not utterances from a user.</span></span>

<span data-ttu-id="df2d5-131">このことは、スキル情報をカードアクションペイロードに埋め込むことによって解決されました。</span><span class="sxs-lookup"><span data-stu-id="df2d5-131">We have resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="df2d5-132">各スキルは `skillId` 、カードアクションのフィールドに埋め込む必要があり `value` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-132">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="df2d5-133">各カードアクションアクティビティに関連するスキル情報が確実に伝達され、仮想アシスタントがこの情報をディスパッチに利用できるようにするには、これが最善の方法です。</span><span class="sxs-lookup"><span data-stu-id="df2d5-133">This is the best way to ensure that each card action activity carries the relevant skill information and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="df2d5-134">カードアクションデータサンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-134">Below is a card action data sample.</span></span> <span data-ttu-id="df2d5-135">コンストラクターに提供することで、 `skillId` スキル情報がカードのアクションに常に表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-135">By providing `skillId` in the constructor we ensure that skill information is always present in card actions.</span></span>

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

<span data-ttu-id="df2d5-136">次に、 `SkillCardActionData` `skillId` カードアクションペイロードから抽出するために、仮想アシスタントテンプレートにクラスを導入します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-136">Next, we introduce `SkillCardActionData` class in the Virtual Assistant template to extract `skillId` from the card action payload.</span></span>

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

<span data-ttu-id="df2d5-137">カードアクションデータから抽出するコードスニペットを次に示し `skillId` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-137">Below is a code snippet to extract  `skillId` from card action data.</span></span> <span data-ttu-id="df2d5-138">[Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)クラスの拡張メソッドとして実装されています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-138">We implemented it as an  extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>

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

### <a name="handle-interruptions-gracefully"></a><span data-ttu-id="df2d5-139">正常に中断する処理</span><span class="sxs-lookup"><span data-stu-id="df2d5-139">Handle interruptions gracefully</span></span>

<span data-ttu-id="df2d5-140">仮想アシスタントは、ユーザーがスキルを呼び出そうとしているときに、別のスキルが現在アクティブな場合に、中断を処理できます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-140">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="df2d5-141">`TeamsSkillDialog`また `TeamsSwitchSkillDialog` 、Bot フレームワークのスキル[ダイアログ](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs)と [ [switchスキル] ダイアログ](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)に基づいて、ユーザーがカードアクションからスキル経験を切り替えることができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="df2d5-141">we have introduced `TeamsSkillDialog` and `TeamsSwitchSkillDialog`, based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), to enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="df2d5-142">この要求を処理するために、仮想アシスタントは、スキルを切り替えるための確認メッセージをユーザーに表示します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-142">To handle this request the Virtual Assistant prompts the user with a confirmation message to switch skills.</span></span>

![新しいスキルに切り替える際の確認メッセージ](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a><span data-ttu-id="df2d5-144">タスクモジュール要求の処理</span><span class="sxs-lookup"><span data-stu-id="df2d5-144">Handling task module requests</span></span>

<span data-ttu-id="df2d5-145">仮想アシスタントにタスクモジュールの機能を追加するには、仮想アシスタントアクティビティハンドラーに、という2つのメソッドが追加されてい `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-145">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="df2d5-146">これらのメソッドは、仮想アシスタントからタスクモジュールに関連するアクティビティをリッスンし、要求に関連付けられているスキルを特定し、要求を識別されたスキルに転送します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-146">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="df2d5-147">要求の転送は、[スキル Httpclient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable)、メソッドによって行われ `PostActivityAsync` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-147">Request forwarding is done via the  [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable), `PostActivityAsync` method.</span></span> <span data-ttu-id="df2d5-148">これ `InvokeResponse` は、解析され、に変換される応答を返し `TaskModuleResponse` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-148">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>

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

<span data-ttu-id="df2d5-149">同様の方法で、カードアクションのディスパッチとタスクモジュールの応答が続きます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-149">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="df2d5-150">タスクモジュールのフェッチと送信アクションのデータが更新され、を含むように `skillId` なります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-150">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="df2d5-151">アクティビティ拡張メソッド `GetSkillId` は `skillId` 、呼び出す必要があるスキルの詳細を提供するペイロードから抽出します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-151">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="df2d5-152">とメソッドのコードスニペットを次に示し `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-152">Below is a code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods.</span></span>

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

<span data-ttu-id="df2d5-153">さらに、 `validDomains` スキルを適切に使用してタスクモジュールが呼び出されるように、すべてのスキルドメインを仮想アシスタントのマニフェストファイルのセクションに含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-153">Additionally, all skill domains must be included in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked via a skill render properly.</span></span>

### <a name="handling-collaborative-app-scopes"></a><span data-ttu-id="df2d5-154">共同作業アプリのスコープを処理する</span><span class="sxs-lookup"><span data-stu-id="df2d5-154">Handling collaborative app scopes</span></span>

<span data-ttu-id="df2d5-155">Teams アプリは、1:1 のチャット、グループチャット、チャネルを含む複数のスコープ内に存在することができます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-155">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="df2d5-156">コア仮想アシスタントテンプレートは、1:1 のチャット用に設計されています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-156">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="df2d5-157">オンボードの機能の一部として、仮想アシスタントは、ユーザーに名前の入力を求め、ユーザーの状態を維持します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-157">As part of the onboarding experience Virtual Assistant  prompts users for name and maintains user state.</span></span> <span data-ttu-id="df2d5-158">その開始時の動作は、グループチャット/チャネルのスコープには適していないため、削除されました。</span><span class="sxs-lookup"><span data-stu-id="df2d5-158">Since that onboarding experience is not suited for group chat/channel scopes it has been removed.</span></span>

<span data-ttu-id="df2d5-159">スキルは、複数の範囲 (1:1 チャット、グループチャット、チャネル会話) でのアクティビティを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-159">Skills should handle activities in multiple scopes (1:1 chat, group chat, and channel conversation).</span></span> <span data-ttu-id="df2d5-160">これらのスコープのいずれかがサポートされていない場合、スキルは適切なメッセージで応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-160">If any of these scopes are not supported, skills should respond with an appropriate message.</span></span>

<span data-ttu-id="df2d5-161">次の処理関数が仮想アシスタントコアに追加されました。</span><span class="sxs-lookup"><span data-stu-id="df2d5-161">The following  processing functions have been added to Virtual Assistant core:</span></span>

- <span data-ttu-id="df2d5-162">仮想アシスタントは、グループチャットまたはチャネルからのテキストメッセージなしで呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-162">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
- <span data-ttu-id="df2d5-163">Articulations は、メッセージをディスパッチモジュールに送信する前に、(bot の必要な @mention を削除する) クリーンアップされます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-163">Articulations are cleaned (i.e.,  remove the necessary @mention of the bot) before sending the message to the dispatch module.</span></span>

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

### <a name="handling-messaging-extensions"></a><span data-ttu-id="df2d5-164">メッセージング拡張機能の処理</span><span class="sxs-lookup"><span data-stu-id="df2d5-164">Handling messaging extensions</span></span>

<span data-ttu-id="df2d5-165">メッセージング拡張機能のコマンドは、アプリマニフェストファイルで宣言されています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-165">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="df2d5-166">メッセージング拡張機能のユーザーインターフェイスは、これらのコマンドによって処理されます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-166">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="df2d5-167">メッセージング拡張コマンド (添付スキルとして) を電源にする仮想アシスタントの場合、仮想アシスタント自体のマニフェストにこれらのコマンドを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-167">For a Virtual Assistant to power a messaging extension command (as an attached skill), a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="df2d5-168">個々のスキルのマニフェストからのコマンドも、仮想アシスタントのマニフェストに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-168">The commands from an individual skill's manifest should be added to the Virtual Assistant's manifest as well.</span></span> <span data-ttu-id="df2d5-169">コマンド ID は、スキルのアプリ ID をセパレーター () で追加することによって、関連付けられたスキルに関する情報を提供し `:` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-169">The command ID provides information about an associated skill by appending the skill's app ID via a separator (`:`).</span></span>

<span data-ttu-id="df2d5-170">以下は、スキルのマニフェストファイルのスニペットです。</span><span class="sxs-lookup"><span data-stu-id="df2d5-170">Below is a snippet from a skill's manifest file.</span></span>

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

<span data-ttu-id="df2d5-171">次に、対応する仮想アシスタントマニフェストファイルのコードスニペットを示します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-171">And, below is the corresponding Virtual Assistant manifest file code snippet.</span></span>

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

<span data-ttu-id="df2d5-172">コマンドがユーザーによって起動されると、仮想アシスタントはコマンド ID を解析することによって関連付けられたスキルを特定し、コマンド ID から特別なサフィックス () を削除してアクティビティを更新し、それを対応するスキルに転送することができ `:<skill_id>` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-172">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix (`:<skill_id>`) from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="df2d5-173">スキルのコードでは、特別なサフィックスを処理する必要がないため、複数のスキルを使用したコマンド Id 間の競合は回避されます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-173">The code for a skill doesn't need to handle the extra suffix, thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="df2d5-174">この方法では、すべてのコンテキスト内のスキルのすべての検索およびアクションコマンド ("新規"、"commandBox"、"message") を仮想アシスタントで利用できます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-174">With this approach, all the search and action commands of a skill within all contexts ("compose", "commandBox" and "message") can be powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="df2d5-175">メッセージング拡張機能の中には、コマンド ID を含まないものがあります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-175">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="df2d5-176">たとえば、には、 `composeExtension/selectItem` invoke タップアクションの値のみが含まれています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-176">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="df2d5-177">関連付けられたスキルを識別するために、 `skillId` の応答を形成している間、各アイテムカードに接続されてい `OnTeamsMessagingExtensionQueryAsync` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-177">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="df2d5-178">(これは、[アダプティブカードを仮想アシスタントに追加](#add-adaptive-cards-to-your-virtual-assistant)する方法に似ています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-178">(This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a><span data-ttu-id="df2d5-179">例: ブック-a room アプリテンプレートを仮想アシスタントスキルに変換する</span><span class="sxs-lookup"><span data-stu-id="df2d5-179">Example: Convert the Book-a-room app template to a Virtual Assistant skill</span></span>

<span data-ttu-id="df2d5-180">[書籍-a room](app-templates.md#book-a-room)は[Microsoft Teams の bot](../bots/what-are-bots.md)で、現在の時刻から 30 (既定)、60、または90分間、ユーザーが会議室をすばやく検索して予約することができます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-180">[Book-a-room](app-templates.md#book-a-room) is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="df2d5-181">個人または1:1 の会話に対して、会議中の bot の範囲を示します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-181">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

![「Book a room」というスキルを持つ仮想アシスタント](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="df2d5-183">「」では、仮想アシスタントに接続できるスキルに変換するために導入されたデルタの変更について説明します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-183">Followings are the delta changes introduced to convert it to a skill which can be attached to a Virtual Assistant.</span></span> <span data-ttu-id="df2d5-184">同様のガイドラインに従って、既存の v4 bot をスキルに変換することができます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-184">Similar guidelines can be followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="df2d5-185">スキルマニフェスト</span><span class="sxs-lookup"><span data-stu-id="df2d5-185">Skill manifest</span></span>

<span data-ttu-id="df2d5-186">スキルマニフェストは、スキルのメッセージングエンドポイント、id、名前、およびその他の関連するメタデータを公開する JSON ファイルです (このマニフェストは、Microsoft Teams のアプリのサイドローディングに使用されるマニフェストとは異なります)。仮想アシスタントには、スキルを添付するための入力としてこのファイルへのパスが必要です。</span><span class="sxs-lookup"><span data-stu-id="df2d5-186">A skill manifest is a JSON file that exposes a skill's messaging endpoint, id, name, and other relevant metadata (this manifest is different than the manifest used for sideloading an app in Microsoft Teams) A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="df2d5-187">次のマニフェストが bot の wwwroot フォルダーに追加されました。</span><span class="sxs-lookup"><span data-stu-id="df2d5-187">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="df2d5-188">LUIS の統合</span><span class="sxs-lookup"><span data-stu-id="df2d5-188">LUIS Integration</span></span>

<span data-ttu-id="df2d5-189">仮想アシスタントのディスパッチモデルは、添付されたスキルの LUIS モデルに基づいて構築されています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-189">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="df2d5-190">ディスパッチモデルは、すべてのテキストアクティビティの目的を特定し、それに関連付けられているスキルを検出します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-190">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="df2d5-191">仮想アシスタント `.lu` は、スキルを付加する際に、入力としてスキルの LUIS モデル (形式) を必要とします。</span><span class="sxs-lookup"><span data-stu-id="df2d5-191">Virtual Assistant requires skill's LUIS model (in `.lu` format) as an input while attaching a skill.</span></span> <span data-ttu-id="df2d5-192">LUIS json は `.lu` 、botframework ツールを使用して形式に変換できます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-192">LUIS json can be converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="df2d5-193">本-room bot には、ユーザーに対して2つの主要なコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-193">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="df2d5-194">これら2つのコマンドについて理解している LUIS モデルを構築しました。</span><span class="sxs-lookup"><span data-stu-id="df2d5-194">We have built a LUIS model understanding these two commands.</span></span> <span data-ttu-id="df2d5-195">対応する機密情報を入力する必要があり `cognitivemodels.json` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-195">Corresponding secrets need to be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="df2d5-196">対応する LUIS JSON ファイルは[ここで](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json)見つけることができます。これは、対応するファイルがどのように見えるかを示してい `.lu` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-196">The corresponding LUIS JSON file can be found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) and this is how the corresponding `.lu` file looks like.</span></span>

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

<span data-ttu-id="df2d5-197">この方法では、ユーザーが、 `book room` `manage favorites` 会議室の bot に関連付けられている、またはこのスキルに転送されたコマンドとして識別されるため、ユーザーによる仮想アシスタントへのすべてのコマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-197">With this approach, any command issues by a user to Virtual Assistant related to `book room` or `manage favorites` can be identified as a command associated with Book-a-room bot and is forwarded to this skill.</span></span>
<span data-ttu-id="df2d5-198">一方、会議室の場合は、LUIS モデルを使用して、これらのコマンドが入力されていない場合 (例:) について理解しておく必要があり `I want to manage my favorite rooms` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-198">On the other hand, Book-a-room room bot needs to use LUIS model to understand these commands if they are not typed as is (for example: `I want to manage my favorite rooms`).</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="df2d5-199">複数言語のサポート</span><span class="sxs-lookup"><span data-stu-id="df2d5-199">Multi-Language support</span></span>

<span data-ttu-id="df2d5-200">この例では、英語のカルチャを持つ LUIS モデルのみが作成されています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-200">For this example, we have only created a LUIS model with English culture.</span></span> <span data-ttu-id="df2d5-201">他の言語に対応する LUIS モデルを作成し、にエントリを追加することができ `cognitivemodels.json` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-201">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="df2d5-202">パラレルで、対応する `.lu` ファイルを luisFolder パスに追加します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-202">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="df2d5-203">フォルダー構造は次のようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-203">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="df2d5-204">Botskills コマンドを次のように更新して、パラメーターを変更し `languages` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-204">Update botskills command as follows to modify `languages` parameter:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="df2d5-205">仮想アシスタントを使用し `SetLocaleMiddleware` て、現在のロケールを識別し、対応するディスパッチモデルを起動します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-205">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="df2d5-206">(Bot フレームワークアクティビティには、このミドルウェアで使用されるロケールフィールドがあります)。スキルにも同じを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="df2d5-206">(Bot framework activity has locale field which is used by this middleware.) We recommend to use the same for your skill as well.</span></span> <span data-ttu-id="df2d5-207">本-room bot はこのミドルウェアを使用せず、代わりに Bot フレームワークアクティビティの[Clientinfo エンティティ](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)からロケールを取得します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-207">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="df2d5-208">要求の検証</span><span class="sxs-lookup"><span data-stu-id="df2d5-208">Claim validation</span></span>

<span data-ttu-id="df2d5-209">発信者をスキルに制限する[claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs)が追加されました。</span><span class="sxs-lookup"><span data-stu-id="df2d5-209">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="df2d5-210">仮想アシスタントがこのスキルを呼び出せるようにするには、 `AllowedCallers` `appsettings` 特定の仮想アシスタントのアプリ ID を使用して配列を設定します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-210">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="df2d5-211">許可された発信者の配列は、スキルにアクセスできるスキルコンシューマーを制限できます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-211">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="df2d5-212">`*`任意のスキルコンシューマーからの呼び出しを受け入れるには、この配列に1つのエントリを追加します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-212">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```
<span data-ttu-id="df2d5-213">スキルにクレーム検証を追加するための詳細なドキュメントは、[こちら](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="df2d5-213">Detailed documentation for adding claims validation to a skill can be found [here](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator).</span></span>

### <a name="card-refresh-limitation"></a><span data-ttu-id="df2d5-214">カードの更新の制限</span><span class="sxs-lookup"><span data-stu-id="df2d5-214">Card refresh limitation</span></span>

<span data-ttu-id="df2d5-215">アクティビティの更新 (カードの更新) は、Virtual Assistant ([github の問題](https://github.com/microsoft/botbuilder-dotnet/issues/3686)) 経由ではまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="df2d5-215">Updating activity (card refresh) is not supported yet via Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="df2d5-216">そのため、すべてのカード更新呼び出し ( `UpdateActivityAsync` ) を新しいカード呼び出し () に置き換えました `SendActivityAsync` 。</span><span class="sxs-lookup"><span data-stu-id="df2d5-216">Hence, we have replaced all card refresh calls (`UpdateActivityAsync`) with posting new card calls(`SendActivityAsync`).</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="df2d5-217">カードアクションとタスクモジュールフロー</span><span class="sxs-lookup"><span data-stu-id="df2d5-217">Card actions and task module flows</span></span>

<span data-ttu-id="df2d5-218">関連付けられたスキルにカードアクションまたはタスクモジュールのアクティビティを転送するには、スキルをそのスキルに埋め込む必要があり `skillId` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-218">To forward card action or task module activities to an associated skill, the skill needs to embed `skillId` to it.</span></span>
<span data-ttu-id="df2d5-219">Book-a room ボットカードアクション、タスクモジュールのフェッチと送信アクションのペイロードは、パラメーターとして格納されるように変更され `skillId` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-219">Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="df2d5-220">詳細については、このドキュメント[のセクションを参照して](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards)ください。</span><span class="sxs-lookup"><span data-stu-id="df2d5-220">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="df2d5-221">グループチャットまたはチャネルスコープからのアクティビティを処理する</span><span class="sxs-lookup"><span data-stu-id="df2d5-221">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="df2d5-222">本-a room bot は、プライベートチャット (個人/1: 1 のスコープ) に対してのみ設計されています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-222">Book-a-room bot is designed for private chats (personal/1:1 scope) only.</span></span> <span data-ttu-id="df2d5-223">グループチャットとチャネルスコープをサポートするようにカスタマイズされた仮想アシスタントを使用しているため、これらのスコープから仮想アシスタントが呼び出される可能性があるので、このようにして、会議室 bot は同じ作業を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-223">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant might be invoked from these scopes and thus, Book-a-room bot might get activities for the same.</span></span> <span data-ttu-id="df2d5-224">そのため、このようなアクティビティを処理するために、ルーム bot がカスタマイズされています。</span><span class="sxs-lookup"><span data-stu-id="df2d5-224">Hence Book-a-room bot is customized to handle those activities.</span></span> <span data-ttu-id="df2d5-225">このチェックは、 `OnMessageActivityAsync` 会議室の bot アクティビティハンドラーのメソッドに追加されました。</span><span class="sxs-lookup"><span data-stu-id="df2d5-225">The check has been put in `OnMessageActivityAsync` methods of Book-a-room bot's activity handler.</span></span>

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

<span data-ttu-id="df2d5-226">[Bot フレームワークソリューションリポジトリ](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp)から既存のスキルを活用したり、新しいスキルを最初から作成したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-226">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="df2d5-227">[この記事](https://microsoft.github.io/botframework-solutions/overview/skills/)では、以降のチュートリアルをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="df2d5-227">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="df2d5-228">仮想アシスタントとスキルのアーキテクチャについては、[ドキュメント](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="df2d5-228">Please refer to [documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   for Virtual Assistant and skills architecture.</span></span>

## <a name="sample-code-to-get-started"></a><span data-ttu-id="df2d5-229">開始するためのサンプルコード</span><span class="sxs-lookup"><span data-stu-id="df2d5-229">Sample code to get started</span></span>

- [<span data-ttu-id="df2d5-230">更新された visual studio テンプレート</span><span class="sxs-lookup"><span data-stu-id="df2d5-230">Updated visual studio template</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [<span data-ttu-id="df2d5-231">書籍-a room bot スキルコード</span><span class="sxs-lookup"><span data-stu-id="df2d5-231">Book-a-room bot skill code</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a><span data-ttu-id="df2d5-232">仮想アシスタントの既知の制限</span><span class="sxs-lookup"><span data-stu-id="df2d5-232">Virtual Assistant known limitations</span></span>

- <span data-ttu-id="df2d5-233">**Endofconversation**。</span><span class="sxs-lookup"><span data-stu-id="df2d5-233">**EndOfConversation**.</span></span> <span data-ttu-id="df2d5-234">スキルは、会話が `endOfConversation` 終了したときにアクティビティを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-234">A skill should send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="df2d5-235">このアクティビティの基準として、仮想アシスタントは特定のスキルのコンテキストを終了し、仮想アシスタントの (ルート) コンテキストに戻ります。</span><span class="sxs-lookup"><span data-stu-id="df2d5-235">basis this activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's (root) context.</span></span> <span data-ttu-id="df2d5-236">冊子の bot の場合、会話を終了する明確な状態はありません。</span><span class="sxs-lookup"><span data-stu-id="df2d5-236">For Book-a-room bot, there is no clear state where conversation can be ended.</span></span> <span data-ttu-id="df2d5-237">そのため、ユーザーが `endOfConversation` ルートコンテキストに戻る必要がある場合は、単にコマンドを実行するだけで済み `start over` ます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-237">Hence we have not sent `endOfConversation` from Book-a-room bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>
- <span data-ttu-id="df2d5-238">**カードの更新**。</span><span class="sxs-lookup"><span data-stu-id="df2d5-238">**Card refresh**.</span></span> <span data-ttu-id="df2d5-239">仮想アシスタントでは、カードの更新はまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="df2d5-239">Card refreshes is not yet supported through Virtual Assistant.</span></span>
- <span data-ttu-id="df2d5-240">**メッセージング拡張機能**:</span><span class="sxs-lookup"><span data-stu-id="df2d5-240">**Messaging extensions**.:</span></span>
  - <span data-ttu-id="df2d5-241">現在、仮想アシスタントは、メッセージング拡張機能に対して最大10個のコマンドをサポートできます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-241">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  - <span data-ttu-id="df2d5-242">メッセージング拡張機能の構成は、個々のコマンドを対象としたものではありません。</span><span class="sxs-lookup"><span data-stu-id="df2d5-242">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="df2d5-243">これは、仮想アシスタントを通じて個々のスキルの構成を制限します。</span><span class="sxs-lookup"><span data-stu-id="df2d5-243">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  - <span data-ttu-id="df2d5-244">メッセージング拡張機能のコマンド Id の最大長は[64 文字](../resources/schema/manifest-schema.md#composeextensions)、37文字は、スキル情報を埋め込むために使用されます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-244">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters will be used for embedding skill information.</span></span> <span data-ttu-id="df2d5-245">このため、コマンド ID の更新された制約は27文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="df2d5-245">Thus, updated constraints for command ID are limited to 27 characters.</span></span>
>
>
