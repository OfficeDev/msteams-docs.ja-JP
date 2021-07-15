---
title: 仮想アシスタントを作成する
description: アプリで使用Virtual Assistantボットとスキルを作成するMicrosoft Teams
localization_priority: Normal
ms.topic: how-to
keywords: teams 仮想アシスタント ボット
ms.openlocfilehash: 976dacbd8b0bef7a3158d5ff35c5c38d97707c63
ms.sourcegitcommit: e327c9766dfa05abb468cdc71319e3cba7c6c79f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2021
ms.locfileid: "53428724"
---
# <a name="create-virtual-assistant"></a><span data-ttu-id="e22d9-104">仮想アシスタントを作成する</span><span class="sxs-lookup"><span data-stu-id="e22d9-104">Create Virtual Assistant</span></span> 

<span data-ttu-id="e22d9-105">Virtual Assistantは、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話型ソリューションを作成できる Microsoft のオープン ソース テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="e22d9-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="e22d9-106">Virtual Assistant [](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template)コア テンプレートは、ボット[フレームワーク SDK、](https://github.com/microsoft/botframework-sdk)言語理解[(LUIS)、QnA](https://www.luis.ai/)Maker など、Virtual Assistant を構築するために必要な Microsoft テクノロジをまとめる基本的なビルド ブロック[です](https://www.qnamaker.ai/)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), and [QnA Maker](https://www.qnamaker.ai/).</span></span> <span data-ttu-id="e22d9-107">また、スキル登録、リンクされたアカウント、ユーザーにシームレスな対話とエクスペリエンスを提供する基本的な会話の意図を含む重要な機能をまとめます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-107">It also brings together the essential capabilities including  skills registration, linked accounts, basic conversational intent to offer a range of seamless interactions and experiences to users.</span></span> <span data-ttu-id="e22d9-108">さらに、テンプレート機能には、再利用可能な会話スキルの豊富な例が含 [まれます](https://microsoft.github.io/botframework-solutions/overview/skills)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-108">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="e22d9-109">個々のスキルは、複数のシナリオを有効Virtual Assistantソリューションに統合されています。</span><span class="sxs-lookup"><span data-stu-id="e22d9-109">Individual skills are integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="e22d9-110">Bot Framework SDK を使用すると、スキルがソース コード形式で提示され、必要に応じてカスタマイズおよび拡張できます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-110">Using the Bot Framework SDK, skills are presented in source code form, enabling you to customize and extend as required.</span></span> <span data-ttu-id="e22d9-111">ボット フレームワークのスキルの詳細については [、「What is a Bot Framework skill」を参照してください](https://microsoft.github.io/botframework-solutions/overview/skills/)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-111">For more information on skills of Bot Framework, see [What is a Bot Framework skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="e22d9-112">このドキュメントでは、Virtual Assistant 実装に関する考慮事項、Teams に焦点を当てた Virtual Assistant の作成方法、関連する例、コード サンプル、および Virtual Assistant の制限事項について説明します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-112">This document guides you on Virtual Assistant implementation considerations for organizations, how to create a Teams focused Virtual Assistant, related example, code sample, and limitations of Virtual Assistant.</span></span>
<span data-ttu-id="e22d9-113">次の図は、仮想アシスタントの概要を表示します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-113">The following image displays the overview of virtual assistant:</span></span>

![Virtual Assistant概要図](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="e22d9-115">テキスト メッセージアクティビティは、ディスパッチ モデルを使用して、Virtual Assistantによって関連付けられたスキル[にルーティング](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true)されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-115">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="e22d9-116">実装に関する考慮事項</span><span class="sxs-lookup"><span data-stu-id="e22d9-116">Implementation considerations</span></span>

<span data-ttu-id="e22d9-117">グループを追加する決定にはVirtual Assistant決定者が多数含まれるので、組織ごとに異なります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-117">The decision to add a Virtual Assistant includes many determinants and differs for each organization.</span></span> <span data-ttu-id="e22d9-118">組織のVirtual Assistantのサポート要素は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="e22d9-118">The supporting factors of a Virtual Assistant implementation for your organization are as follows:</span></span>

* <span data-ttu-id="e22d9-119">中央チームがすべての従業員エクスペリエンスを管理します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-119">A central team manages all employee experiences.</span></span> <span data-ttu-id="e22d9-120">新しいスキルの追加など、Virtual Assistantエクスペリエンスを構築し、更新プログラムを管理する機能があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-120">It has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
* <span data-ttu-id="e22d9-121">ビジネス機能全体に複数のアプリケーションが存在し、その数は今後増加する見込みです。</span><span class="sxs-lookup"><span data-stu-id="e22d9-121">Multiple applications exist across business functions and the number is expected to grow in the future.</span></span>
* <span data-ttu-id="e22d9-122">既存のアプリケーションはカスタマイズ可能で、組織が所有し、組織のスキルにVirtual Assistant。</span><span class="sxs-lookup"><span data-stu-id="e22d9-122">Existing applications are customizable, owned by the organization, and are converted into skills for a Virtual Assistant.</span></span>
* <span data-ttu-id="e22d9-123">中央の従業員エクスペリエンス チームは、既存のアプリのカスタマイズに影響を与える可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-123">The central employee experiences team is able to influence customizations to existing apps.</span></span> <span data-ttu-id="e22d9-124">また、既存のアプリケーションをエクスペリエンスのスキルとして統合するために必要Virtual Assistant提供します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-124">It also provides necessary guidance for integrating existing applications as skills in Virtual Assistant experience.</span></span>

<span data-ttu-id="e22d9-125">次の図は、ユーザーのビジネス機能をVirtual Assistant。</span><span class="sxs-lookup"><span data-stu-id="e22d9-125">The following image displays the business functions of Virtual Assistant:</span></span> 

![中央チームはアシスタントを維持し、ビジネス機能チームはスキルを提供します](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="e22d9-127">フォーカスにTeamsを作成Virtual Assistant</span><span class="sxs-lookup"><span data-stu-id="e22d9-127">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="e22d9-128">Microsoft は、仮想アシスタント[Visual Studioスキルを構築](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate)する新しいテンプレートを公開しました。</span><span class="sxs-lookup"><span data-stu-id="e22d9-128">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="e22d9-129">このテンプレートVisual Studioを使用すると、アクションVirtual Assistantリッチ カードをサポートするテキスト ベースのエクスペリエンスを利用して、新しいカードを作成できます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-129">With the Visual Studio template, you can create a Virtual Assistant, powered by a text based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="e22d9-130">基本テンプレートを拡張Visual Studio、プラットフォームの機能Microsoft Teams、アプリ エクスペリエンスを向上Teams強化しました。</span><span class="sxs-lookup"><span data-stu-id="e22d9-130">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="e22d9-131">機能のいくつかには、豊富なアダプティブ カード、タスク モジュール、チームまたはグループ チャット、メッセージング拡張機能のサポートが含まれます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-131">A few of the capabilities include support for rich Adaptive Cards, task modules, teams or group chats, and messaging extensions.</span></span> <span data-ttu-id="e22d9-132">[チュートリアル] から [Virtual Assistant] Microsoft Teamsの詳細については、「チュートリアル[: Extend your Virtual Assistant to Microsoft Teams」 を参照してください](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-132">For more information on extending Virtual Assistant to Microsoft Teams, see [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>    
<span data-ttu-id="e22d9-133">次の図は、ソリューションの高レベル図Virtual Assistantします。</span><span class="sxs-lookup"><span data-stu-id="e22d9-133">The following image displays the high level diagram of a Virtual Assistant solution:</span></span>

![ソリューションの高レベルVirtual Assistant図](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="e22d9-135">アダプティブ カードをアプリに追加Virtual Assistant</span><span class="sxs-lookup"><span data-stu-id="e22d9-135">Add Adaptive Cards to your Virtual Assistant</span></span>

<span data-ttu-id="e22d9-136">要求を適切にディスパッチするには、Virtual Assistant適切な LUIS モデルとそれに関連付けられている対応するスキルを識別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-136">To dispatch requests properly, your Virtual Assistant must identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="e22d9-137">ただし、スキルに関連付けられた LUIS モデルがカード アクション テキスト用にトレーニングされている場合、ディスパッチ機構をカード アクション アクティビティに使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="e22d9-137">However, the dispatching mechanism cannot be used for card action activities as the LUIS model associated with a skill, is trained for card action texts.</span></span> <span data-ttu-id="e22d9-138">カード アクション のテキストは、固定された定義済みのキーワードであり、ユーザーからのコメントはありません。</span><span class="sxs-lookup"><span data-stu-id="e22d9-138">The card action texts are fixed, pre-defined keywords, and not commented from a user.</span></span>

<span data-ttu-id="e22d9-139">この欠点は、カード アクション ペイロードにスキル情報を埋め込む方法によって解決されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-139">This drawback is resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="e22d9-140">すべてのスキルは、カード `skillId` アクションの  `value` フィールドに埋め込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-140">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="e22d9-141">各カード アクション アクティビティに関連するスキル情報が含まれるか確認し、Virtual Assistant情報をディスパッチに利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-141">You must ensure that each card action activity carries the relevant skill information, and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="e22d9-142">スキル情報が常にカード アクションに表示されるのを確認するには、コンストラクター `skillId` で指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-142">You must provide `skillId` in the constructor to ensure that the skill information is always present in card actions.</span></span>
<span data-ttu-id="e22d9-143">カード アクション データのサンプル コードを次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-143">A card action data sample code is shown in the following section:</span></span>
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

<span data-ttu-id="e22d9-144">次に `SkillCardActionData` 、カード アクション ペイロードからVirtual Assistantテンプレートのクラス `skillId` を紹介します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-144">Next, `SkillCardActionData` class in the Virtual Assistant template is introduces to extract `skillId` from the card action payload.</span></span>
<span data-ttu-id="e22d9-145">カード アクション ペイロードから抽出  `skillId` するコード スニペットを次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-145">A code snippet to extract  `skillId` from card action payload is shown in the following section:</span></span>

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

<span data-ttu-id="e22d9-146">実装は [、Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) クラスの拡張メソッドによって行われます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-146">The implementation is done by an extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>
<span data-ttu-id="e22d9-147">カード アクション データから抽出  `skillId` するコード スニペットを次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-147">A code snippet to extract  `skillId` from card action data is shown in the following section:</span></span>

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

### <a name="handle-interruptions"></a><span data-ttu-id="e22d9-148">中断の処理</span><span class="sxs-lookup"><span data-stu-id="e22d9-148">Handle interruptions</span></span>

<span data-ttu-id="e22d9-149">Virtual Assistant別のスキルが現在アクティブな間にユーザーがスキルを呼び出そうとした場合の中断を処理できます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-149">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="e22d9-150">`TeamsSkillDialog`、 `TeamsSwitchSkillDialog` ボット フレームワークの [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) と [SwitchSkillDialog に基づいて導入されます](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-150">`TeamsSkillDialog`, and `TeamsSwitchSkillDialog`are introduced based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs).</span></span> <span data-ttu-id="e22d9-151">ユーザーは、カード操作からスキル エクスペリエンスを切り替えできます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-151">They enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="e22d9-152">この要求を処理するために、Virtual Assistant確認メッセージをユーザーに求め、スキルを切り替えます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-152">To handle this request, the Virtual Assistant prompts the user with a confirmation message to switch skills:</span></span>

![新しいスキルに切り替える際の確認プロンプト](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a><span data-ttu-id="e22d9-154">タスク モジュール要求の処理</span><span class="sxs-lookup"><span data-stu-id="e22d9-154">Handle task module requests</span></span>

<span data-ttu-id="e22d9-155">タスク モジュールの機能を Virtual Assistantに追加するには、2 つの追加のメソッドが Virtual Assistant アクティビティ ハンドラーに `OnTeamsTaskModuleFetchAsync` 含まれています。 `OnTeamsTaskModuleSubmitAsync`</span><span class="sxs-lookup"><span data-stu-id="e22d9-155">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="e22d9-156">これらのメソッドは、Virtual Assistant からタスク モジュール関連のアクティビティをリッスンし、要求に関連付けられたスキルを識別し、特定のスキルに要求を転送します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-156">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="e22d9-157">要求の転送は [、SkillHttpClient メソッドを介](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true)して行 `PostActivityAsync` われます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-157">Request forwarding is done through the [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` method.</span></span> <span data-ttu-id="e22d9-158">これは、解析され、に変換 `InvokeResponse` される応答を返します `TaskModuleResponse` 。</span><span class="sxs-lookup"><span data-stu-id="e22d9-158">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>


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

<span data-ttu-id="e22d9-159">カード アクションのディスパッチとタスク モジュールの応答にも同様の方法が実行されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-159">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="e22d9-160">タスク モジュールのフェッチと送信のアクション データが更新され、含まれます `skillId` 。</span><span class="sxs-lookup"><span data-stu-id="e22d9-160">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="e22d9-161">Activity Extension メソッド `GetSkillId` は、呼び出す必要があるスキルの詳細を提供するペイロード `skillId` から抽出します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-161">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="e22d9-162">コード スニペットと `OnTeamsTaskModuleFetchAsync` メソッド `OnTeamsTaskModuleSubmitAsync` については、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-162">The code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods are given in the following section:</span></span>

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

<span data-ttu-id="e22d9-163">さらに、スキルを介して呼び出されるタスク モジュールが適切にレンダリングVirtual Assistantマニフェスト ファイルのセクションに、すべてのスキル ドメイン `validDomains` を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-163">Additionally, you must include all skill domains in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked through a skill render properly.</span></span>

### <a name="handle-collaborative-app-scopes"></a><span data-ttu-id="e22d9-164">共同アプリのスコープを処理する</span><span class="sxs-lookup"><span data-stu-id="e22d9-164">Handle collaborative app scopes</span></span>

<span data-ttu-id="e22d9-165">Teamsは、1:1 チャット、グループ チャット、チャネルなど、複数のスコープに存在できます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-165">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="e22d9-166">コア Virtual Assistantは、1:1 チャット用に設計されています。</span><span class="sxs-lookup"><span data-stu-id="e22d9-166">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="e22d9-167">オンボーディング エクスペリエンスの一環として、Virtual Assistantを求め、ユーザーの状態を維持します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-167">As part of the onboarding experience Virtual Assistant prompts users for name and maintains user state.</span></span> <span data-ttu-id="e22d9-168">オンボーディング エクスペリエンスはグループ チャットやチャネル スコープには適していないので、削除されています。</span><span class="sxs-lookup"><span data-stu-id="e22d9-168">Since that onboarding experience is not suited for group chat or channel scopes it has been removed.</span></span>

<span data-ttu-id="e22d9-169">スキルは、1:1 チャット、グループ チャット、チャネル会話など、複数の範囲のアクティビティを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-169">Skills should handle activities in multiple scopes, such as 1:1 chat, group chat, and channel conversation.</span></span> <span data-ttu-id="e22d9-170">これらのスコープがサポートされていない場合、スキルは適切なメッセージで応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-170">If any of these scopes are not supported, skills must respond with an appropriate message.</span></span>

<span data-ttu-id="e22d9-171">次の処理関数がコアにVirtual Assistantされています。</span><span class="sxs-lookup"><span data-stu-id="e22d9-171">The following  processing functions have been added to Virtual Assistant core:</span></span>

* <span data-ttu-id="e22d9-172">Virtual Assistantグループ チャットまたはチャネルからのテキスト メッセージなしで呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-172">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
* <span data-ttu-id="e22d9-173">メッセージをディスパッチ モジュールに送信する前に、アーティキュレーションがクリーンアップされます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-173">Articulations are cleaned before sending the message to the dispatch module.</span></span> <span data-ttu-id="e22d9-174">たとえば、ボットの必要な@mention削除します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-174">For example, remove the necessary @mention of the bot.</span></span>

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

### <a name="handle-messaging-extensions"></a><span data-ttu-id="e22d9-175">メッセージング拡張機能の処理</span><span class="sxs-lookup"><span data-stu-id="e22d9-175">Handle messaging extensions</span></span>

<span data-ttu-id="e22d9-176">メッセージング拡張機能のコマンドは、アプリ マニフェスト ファイルで宣言されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-176">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="e22d9-177">メッセージング拡張機能のユーザー インターフェイスには、これらのコマンドが搭載されています。</span><span class="sxs-lookup"><span data-stu-id="e22d9-177">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="e22d9-178">メッセージング拡張機能Virtual Assistant接続スキルとして電源を供給するには、Virtual Assistant独自のマニフェストにこれらのコマンドが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-178">For a Virtual Assistant to power a messaging extension command as an attached skill, a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="e22d9-179">個々のスキルのマニフェストからユーザーのマニフェストにコマンドを追加Virtual Assistant必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-179">You must add the commands from an individual skill's manifest to the Virtual Assistant's manifest.</span></span> <span data-ttu-id="e22d9-180">コマンド ID は、スキルのアプリ ID を区切り記号で追加することで、関連付けられたスキルに関する情報を提供します `:` 。</span><span class="sxs-lookup"><span data-stu-id="e22d9-180">The command ID provides information about an associated skill by appending the skill's app ID through a separator `:`.</span></span>

<span data-ttu-id="e22d9-181">スキルのマニフェスト ファイルのスニペットを次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-181">The snippet from a skill's manifest file is shown in the following section:</span></span>

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

<span data-ttu-id="e22d9-182">対応するVirtual Assistantマニフェスト ファイル コード スニペットを次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-182">The corresponding Virtual Assistant manifest file code snippet is shown in the following section:</span></span>

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

<span data-ttu-id="e22d9-183">コマンドがユーザーによって呼び出されると、Virtual Assistant はコマンド ID を解析して関連付けられたスキルを識別し、コマンド ID から余分な接尾辞を削除してアクティビティを更新し、対応するスキルに転送できます。 `:<skill_id>`</span><span class="sxs-lookup"><span data-stu-id="e22d9-183">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix `:<skill_id>` from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="e22d9-184">スキルのコードは、余分な接尾辞を処理する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="e22d9-184">The code for a skill doesnot need to handle the extra suffix.</span></span> <span data-ttu-id="e22d9-185">したがって、スキル間のコマンドの ID 間の競合は回避されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-185">Thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="e22d9-186">この方法では、作成 **、commandBox、** メッセージなど、すべてのコンテキスト内のすべてのスキルの検索コマンドとアクション コマンドは、Virtual Assistant。 </span><span class="sxs-lookup"><span data-stu-id="e22d9-186">With this approach, all the search and action commands of a skill within all contexts, such as **compose**, **commandBox**, and **message** are powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="e22d9-187">メッセージング拡張機能のアクティビティの中には、コマンド ID が含まれるものがあります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-187">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="e22d9-188">たとえば、呼 `composeExtension/selectItem` び出しタップ アクションの値だけが含まれるとします。</span><span class="sxs-lookup"><span data-stu-id="e22d9-188">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="e22d9-189">関連付けられたスキルを識別するには、に対する応答を形成している間、各 `skillId`  アイテム カードに添付されます `OnTeamsMessagingExtensionQueryAsync` 。</span><span class="sxs-lookup"><span data-stu-id="e22d9-189">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="e22d9-190">これは、アダプティブ カードをアプリに追加する方法と[似Virtual Assistant。](#add-adaptive-cards-to-your-virtual-assistant)</span><span class="sxs-lookup"><span data-stu-id="e22d9-190">This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example"></a><span data-ttu-id="e22d9-191">例</span><span class="sxs-lookup"><span data-stu-id="e22d9-191">Example</span></span>

<span data-ttu-id="e22d9-192">次の使用例は、Book-a-room アプリ テンプレートを Virtual Assistant スキルに変換する方法を示しています。Book-a-room は Microsoft Teams であり、ユーザーは現在の時刻から 30 分、60 分、または 90 分の会議室をすばやく検索して予約できます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-192">The following example shows how to convert the Book-a-room app template to a Virtual Assistant skill: Book-a-room is a Microsoft Teams that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="e22d9-193">既定の時間は 30 分です。</span><span class="sxs-lookup"><span data-stu-id="e22d9-193">The default time is 30 minutes.</span></span> <span data-ttu-id="e22d9-194">会議室予約ボットは、個人の会話または一対一の会話を対象としています。</span><span class="sxs-lookup"><span data-stu-id="e22d9-194">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="e22d9-195">次の図は、Virtual Assistantスキルを含 **むビューを表示** します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-195">The following image displays a Virtual Assistant with a **book a room** skill:</span></span>

![Virtual Assistant「部屋を予約する」スキルを使用する](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="e22d9-197">以下に、デルタをスキルに変換するために導入された変更点を示します。この変更は、Virtual Assistant。</span><span class="sxs-lookup"><span data-stu-id="e22d9-197">Followings are the delta changes introduced to convert it to a skill which is attached to a Virtual Assistant.</span></span> <span data-ttu-id="e22d9-198">同様のガイドラインに従って、既存の v4 ボットをスキルに変換します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-198">Similar guidelines are followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="e22d9-199">スキル マニフェスト</span><span class="sxs-lookup"><span data-stu-id="e22d9-199">Skill manifest</span></span>

<span data-ttu-id="e22d9-200">スキル マニフェストは、スキルのメッセージング エンドポイント、ID、名前、その他の関連するメタデータを公開する JSON ファイルです。</span><span class="sxs-lookup"><span data-stu-id="e22d9-200">A skill manifest is a JSON file that exposes a skill's messaging endpoint, ID, name, and other relevant metadata.</span></span> <span data-ttu-id="e22d9-201">このマニフェストは、アプリのサイドローディングに使用されるマニフェストとは異Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="e22d9-201">This manifest is different than the manifest used for sideloading an app in Microsoft Teams.</span></span> <span data-ttu-id="e22d9-202">スキルVirtual Assistant接続するには、入力としてこのファイルへのパスが必要です。</span><span class="sxs-lookup"><span data-stu-id="e22d9-202">A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="e22d9-203">ボットの wwwroot フォルダーに次のマニフェストを追加しました。</span><span class="sxs-lookup"><span data-stu-id="e22d9-203">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="e22d9-204">LUIS 統合</span><span class="sxs-lookup"><span data-stu-id="e22d9-204">LUIS Integration</span></span>

<span data-ttu-id="e22d9-205">Virtual Assistantのディスパッチ モデルは、添付されたスキルの LUIS モデルの上に構築されています。</span><span class="sxs-lookup"><span data-stu-id="e22d9-205">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="e22d9-206">ディスパッチ モデルは、すべてのテキスト アクティビティの意図を識別し、関連付けられたスキルを見つける。</span><span class="sxs-lookup"><span data-stu-id="e22d9-206">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="e22d9-207">Virtual Assistantを添付する場合は、入力形式でスキルの LUIS `.lu` モデルが必要です。</span><span class="sxs-lookup"><span data-stu-id="e22d9-207">Virtual Assistant requires skill's LUIS model in `.lu` format as an input while attaching a skill.</span></span> <span data-ttu-id="e22d9-208">LUIS json は `.lu` 、botframework-cli ツールを使用して形式に変換されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-208">LUIS json is converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="e22d9-209">Book-a-room ボットには、ユーザー用の 2 つの主なコマンドがあります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-209">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="e22d9-210">これら 2 つのコマンドを理解して、LUIS モデルを構築しました。</span><span class="sxs-lookup"><span data-stu-id="e22d9-210">We have built a LUIS model by understanding these two commands.</span></span> <span data-ttu-id="e22d9-211">対応するシークレットを入力する必要があります `cognitivemodels.json` 。</span><span class="sxs-lookup"><span data-stu-id="e22d9-211">Corresponding secrets must be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="e22d9-212">対応する LUIS JSON ファイルは次のページ [で確認できます](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-212">The corresponding LUIS JSON file is found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json).</span></span>
<span data-ttu-id="e22d9-213">対応する `.lu` ファイルは、次のセクションに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-213">The corresponding `.lu` file is shown in the following section:</span></span>

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

<span data-ttu-id="e22d9-214">この方法では、ボットに関連付けられたコマンドVirtual Assistant、またはボットに関連付けられたコマンドとして識別されるユーザーが発行したコマンドは、このスキル `book room` `manage favorites` `Book-a-room` に転送されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-214">With this approach, any command issued by a user to Virtual Assistant related to `book room` or `manage favorites` are identified as a command associated with `Book-a-room` bot and is forwarded to this skill.</span></span>
<span data-ttu-id="e22d9-215">一方、ボットは、入力が完全ではない場合、これらのコマンドを理解するために LUIS モデル `Book-a-room room` を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-215">On the other hand, `Book-a-room room` bot needs to use LUIS model to understand these commands if they are not typed full.</span></span> <span data-ttu-id="e22d9-216">例: `I want to manage my favorite rooms`。</span><span class="sxs-lookup"><span data-stu-id="e22d9-216">For example: `I want to manage my favorite rooms`.</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="e22d9-217">多言語サポート</span><span class="sxs-lookup"><span data-stu-id="e22d9-217">Multi-Language support</span></span>

<span data-ttu-id="e22d9-218">たとえば、英語のカルチャのみを持つ LUIS モデルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-218">As an example, a LUIS model with only English culture is created.</span></span> <span data-ttu-id="e22d9-219">他の言語に対応する LUIS モデルを作成し、にエントリを追加できます `cognitivemodels.json` 。</span><span class="sxs-lookup"><span data-stu-id="e22d9-219">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="e22d9-220">並行して、対応する `.lu` ファイルを luisFolder パスに追加します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-220">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="e22d9-221">フォルダー構造は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="e22d9-221">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="e22d9-222">パラメーターを `languages` 変更するには、botskills コマンドを次のように更新します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-222">To modify `languages` parameter, update botskills command as follows:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="e22d9-223">Virtual Assistantロケールを `SetLocaleMiddleware` 識別し、対応するディスパッチ モデルを呼び出す場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-223">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="e22d9-224">ボット フレームワーク アクティビティには、このミドルウェアで使用されるロケール フィールドがあります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-224">Bot framework activity has locale field which is used by this middleware.</span></span> <span data-ttu-id="e22d9-225">スキルにも同じ機能を使用できます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-225">You can use the same for your skill as well.</span></span> <span data-ttu-id="e22d9-226">Book-a-room ボットは、このミドルウェアを使用しない代わりに、ボット フレームワーク アクティビティの clientInfo エンティティから [ロケールを取得します](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-226">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="e22d9-227">クレーム検証</span><span class="sxs-lookup"><span data-stu-id="e22d9-227">Claim validation</span></span>

<span data-ttu-id="e22d9-228">呼び出し [元をスキルに制限する claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) を追加しました。</span><span class="sxs-lookup"><span data-stu-id="e22d9-228">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="e22d9-229">ユーザーがこのVirtual Assistant呼び出しを許可するには、その特定のユーザーのアプリ ID Virtual Assistant `AllowedCallers` `appsettings` 配列を設定します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-229">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="e22d9-230">許可された発信者配列は、どのスキルコンシューマーがスキルにアクセスできるのか制限できます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-230">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="e22d9-231">スキルコンシュー `*` マからの呼び出しを受け入れるには、この配列に 1 つのエントリを追加します。</span><span class="sxs-lookup"><span data-stu-id="e22d9-231">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```

<span data-ttu-id="e22d9-232">スキルにクレーム検証を追加する方法の詳細については、「スキルにクレーム検証を追加 [する」を参照してください](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-232">For more information on adding claims validation to a skill, see [add claims validation to skill](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span></span>

### <a name="limitation-of-card-refresh"></a><span data-ttu-id="e22d9-233">カードの更新の制限</span><span class="sxs-lookup"><span data-stu-id="e22d9-233">Limitation of card refresh</span></span> 

<span data-ttu-id="e22d9-234">カードの更新などのアクティビティの更新は、Virtual Assistant[(github の](https://github.com/microsoft/botbuilder-dotnet/issues/3686)問題) ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="e22d9-234">Updating activity, such as card refresh is not supported yet through Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="e22d9-235">したがって、すべてのカード更新呼び出しを新しい `UpdateActivityAsync` カード呼び出しの投稿に置き換えました `SendActivityAsync` 。</span><span class="sxs-lookup"><span data-stu-id="e22d9-235">Hence, we have replaced all card refresh calls `UpdateActivityAsync` with posting new card calls `SendActivityAsync`.</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="e22d9-236">カードアクションとタスク モジュールフロー</span><span class="sxs-lookup"><span data-stu-id="e22d9-236">Card actions and task module flows</span></span>

<span data-ttu-id="e22d9-237">カード アクションまたはタスク モジュールアクティビティを関連付けられたスキルに転送するには、スキルを埋め込む `skillId` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-237">To forward card action or task module activities to an associated skill, the skill must embed `skillId` to it.</span></span>
<span data-ttu-id="e22d9-238">`Book-a-room` ボット カードアクション、タスク モジュールのフェッチおよび送信アクション ペイロードは、パラメーターとして格納 `skillId` するために変更されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-238">`Book-a-room` bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="e22d9-239">詳細については、この [ドキュメントのこの](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="e22d9-239">For more information refer [this](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="e22d9-240">グループ チャットまたはチャネル スコープからのアクティビティの処理</span><span class="sxs-lookup"><span data-stu-id="e22d9-240">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="e22d9-241">`Book-a-room bot` 個人チャットや 1:1 スコープのみなど、プライベート チャット用に設計されています。</span><span class="sxs-lookup"><span data-stu-id="e22d9-241">`Book-a-room bot` is designed for private chats, such as personal or 1:1 scope only.</span></span> <span data-ttu-id="e22d9-242">グループ チャットとチャネル スコープをサポートするために Virtual Assistant をカスタマイズしましたので、Virtual Assistant をチャネル スコープから呼び出す必要があります。そのため、ボットは同じスコープのアクティビティを取得 `Book-a-room` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-242">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant must be invoked from the channel scopes and thus, `Book-a-room` bot must get activities for the same scope.</span></span> <span data-ttu-id="e22d9-243">したがって `Book-a-room` 、ボットは、これらのアクティビティを処理するためにカスタマイズされます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-243">Hence `Book-a-room`bot is customized to handle those activities.</span></span> <span data-ttu-id="e22d9-244">ボットのアクティビティ ハンドラー `OnMessageActivityAsync` のチェックイン メソッド `Book-a-room` を確認できます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-244">You can find the check in `OnMessageActivityAsync` methods of `Book-a-room` bot's activity handler.</span></span>

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

<span data-ttu-id="e22d9-245">ボット フレームワーク ソリューション リポジトリの既存の [スキルを活用](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) したり、新しいスキルを最初から完全に作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-245">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="e22d9-246">新しいスキルを作成するには、「 [チュートリアル」を参照して新しいスキルを作成します](https://microsoft.github.io/botframework-solutions/overview/skills/)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-246">For creating a new skill, see [tutorials to create a new skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="e22d9-247">詳細Virtual Assistantスキル アーキテクチャのドキュメントについては、「Virtual Assistant[スキル アーキテクチャ」を参照してください](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-247">For Virtual Assistant and skills architecture documentation, see[Virtual Assistant and skills architecture](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).</span></span>  

## <a name="limitations-of-virtual-assistant"></a><span data-ttu-id="e22d9-248">制限のVirtual Assistant</span><span class="sxs-lookup"><span data-stu-id="e22d9-248">Limitations of Virtual Assistant</span></span> 

* <span data-ttu-id="e22d9-249">**EndOfConversation**: スキルは、会話が終了したら `endOfConversation` アクティビティを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-249">**EndOfConversation**: A skill must send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="e22d9-250">アクティビティに基づいて、Virtual Assistant特定のスキルとのコンテキストを終了し、Virtual Assistantのルート コンテキストに戻ります。</span><span class="sxs-lookup"><span data-stu-id="e22d9-250">Based on the activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's root context.</span></span> <span data-ttu-id="e22d9-251">Book-a-room ボットの場合、会話が終了する明確な状態はありません。</span><span class="sxs-lookup"><span data-stu-id="e22d9-251">For Book-a-room bot, there is no clear state where conversation is ended.</span></span> <span data-ttu-id="e22d9-252">したがって、ボットから送信していないので、ユーザーがルート コンテキストに戻りたい場合は、コマンド `endOfConversation` `Book-a-room` で簡単に行 `start over` います。</span><span class="sxs-lookup"><span data-stu-id="e22d9-252">Hence we have not sent `endOfConversation` from `Book-a-room` bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>  
* <span data-ttu-id="e22d9-253">**カードの更新**: カードの更新は、カード更新プログラムを通じてVirtual Assistant。</span><span class="sxs-lookup"><span data-stu-id="e22d9-253">**Card refresh**: Card refresh is not yet supported through Virtual Assistant.</span></span>  
* <span data-ttu-id="e22d9-254">**メッセージング拡張機能**:</span><span class="sxs-lookup"><span data-stu-id="e22d9-254">**Messaging extensions**:</span></span>
  * <span data-ttu-id="e22d9-255">現時点では、Virtual Assistant拡張機能の最大 10 個のコマンドをサポートできます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-255">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  * <span data-ttu-id="e22d9-256">メッセージング拡張機能の構成は、個々のコマンドではなく、拡張機能全体に対してスコープ設定されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-256">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="e22d9-257">これにより、個々のスキルの構成が制限されます。Virtual Assistant。</span><span class="sxs-lookup"><span data-stu-id="e22d9-257">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  * <span data-ttu-id="e22d9-258">メッセージング拡張機能コマンドの ID には最大 [64](../resources/schema/manifest-schema.md#composeextensions) 文字の長さ、スキル情報の埋め込みには 37 文字が使用されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-258">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters are used for embedding skill information.</span></span> <span data-ttu-id="e22d9-259">したがって、コマンド ID の更新された制約は 27 文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-259">Thus, updated constraints for command ID are limited to 27 characters.</span></span>

<span data-ttu-id="e22d9-260">ボット フレームワーク ソリューション リポジトリの既存の [スキルを活用](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) したり、新しいスキルを最初から完全に作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-260">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="e22d9-261">以降のチュートリアルについては、こちらを参照 [してください](https://microsoft.github.io/botframework-solutions/overview/skills/)。</span><span class="sxs-lookup"><span data-stu-id="e22d9-261">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="e22d9-262">詳細とスキル[のアーキテクチャ](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)については、Virtual Assistantを参照してください。</span><span class="sxs-lookup"><span data-stu-id="e22d9-262">Please refer to [documentation](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) for Virtual Assistant and skills architecture.</span></span>

## <a name="code-sample"></a><span data-ttu-id="e22d9-263">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="e22d9-263">Code sample</span></span>

| <span data-ttu-id="e22d9-264">**サンプルの名前**</span><span class="sxs-lookup"><span data-stu-id="e22d9-264">**Sample name**</span></span> | <span data-ttu-id="e22d9-265">**説明**</span><span class="sxs-lookup"><span data-stu-id="e22d9-265">**Description**</span></span> | <span data-ttu-id="e22d9-266">**C#**  **.NET**</span><span class="sxs-lookup"><span data-stu-id="e22d9-266">**C#**  **.NET**</span></span> |
|----------|-----------------|---------------------------|
| <span data-ttu-id="e22d9-267">更新された visual studio テンプレート</span><span class="sxs-lookup"><span data-stu-id="e22d9-267">Updated visual studio template</span></span> | <span data-ttu-id="e22d9-268">チームの機能をサポートするカスタマイズされたテンプレート。</span><span class="sxs-lookup"><span data-stu-id="e22d9-268">Customized template to support teams capabilities.</span></span> | [<span data-ttu-id="e22d9-269">表示</span><span class="sxs-lookup"><span data-stu-id="e22d9-269">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| <span data-ttu-id="e22d9-270">Book-a-room ボットのスキル コード</span><span class="sxs-lookup"><span data-stu-id="e22d9-270">Book-a-room bot skill code</span></span> | <span data-ttu-id="e22d9-271">移動中に会議室をすばやく見つけて予約できます。</span><span class="sxs-lookup"><span data-stu-id="e22d9-271">Lets you quickly find and book a meeting room on the go.</span></span> | [<span data-ttu-id="e22d9-272">表示</span><span class="sxs-lookup"><span data-stu-id="e22d9-272">View</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |


## <a name="see-also"></a><span data-ttu-id="e22d9-273">関連項目</span><span class="sxs-lookup"><span data-stu-id="e22d9-273">See also</span></span>

* [<span data-ttu-id="e22d9-274">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="e22d9-274">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
* [<span data-ttu-id="e22d9-275">会議室予約</span><span class="sxs-lookup"><span data-stu-id="e22d9-275">Book-a-room</span></span>](app-templates.md#book-a-room)
* [<span data-ttu-id="e22d9-276">Microsoft Teamsボット</span><span class="sxs-lookup"><span data-stu-id="e22d9-276">Microsoft Teams bot</span></span>](../bots/what-are-bots.md)
