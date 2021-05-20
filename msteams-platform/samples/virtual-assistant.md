---
title: 仮想アシスタントを作成する
description: Microsoft Teamsで使用するバーチャル アシスタント ボットとスキルを作成する方法
localization_priority: Normal
ms.topic: how-to
keywords: チーム仮想アシスタントボット
ms.openlocfilehash: 072d9cb5742cd39101587cad32e3048bd36cc1d8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566874"
---
# <a name="create-virtual-assistant"></a><span data-ttu-id="92bb7-104">仮想アシスタントを作成する</span><span class="sxs-lookup"><span data-stu-id="92bb7-104">Create Virtual Assistant</span></span> 

<span data-ttu-id="92bb7-105">Virtual Assistant は、ユーザー エクスペリエンス、組織のブランド化、および必要なデータを完全に制御しながら、堅牢な会話ソリューションを作成できる Microsoft オープンソース テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="92bb7-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="92bb7-106">[バーチャル アシスタント コア テンプレート](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template)は、[仮想](https://github.com/microsoft/botframework-sdk)アシスタントを構築するために必要なマイクロソフトのテクノロジをまとめて使用する基本的な構成要素[です。](https://www.qnamaker.ai/) [](https://www.luis.ai/)</span><span class="sxs-lookup"><span data-stu-id="92bb7-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), and [QnA Maker](https://www.qnamaker.ai/).</span></span> <span data-ttu-id="92bb7-107">また、スキル登録、リンクされたアカウント、基本的な会話の意図など、ユーザーにシームレスなインタラクションやエクスペリエンスの範囲を提供する必要不可欠な機能を一緒に提供します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-107">It also brings together the essential capabilities including  skills registration, linked accounts, basic conversational intent to offer a range of seamless interactions and experiences to users.</span></span> <span data-ttu-id="92bb7-108">また、テンプレート機能には、再利用可能な会話スキルの豊富な例が含 [まれています](https://microsoft.github.io/botframework-solutions/overview/skills)。</span><span class="sxs-lookup"><span data-stu-id="92bb7-108">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="92bb7-109">個々のスキルは、仮想アシスタントソリューションに統合され、複数のシナリオを可能にします。</span><span class="sxs-lookup"><span data-stu-id="92bb7-109">Individual skills are integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="92bb7-110">Bot Framework SDK を使用すると、スキルがソース コード形式で表示され、必要に応じてカスタマイズおよび拡張できます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-110">Using the Bot Framework SDK, skills are presented in source code form, enabling you to customize and extend as required.</span></span> <span data-ttu-id="92bb7-111">Bot Framework のスキルの詳細については、「 [Bot Framework スキルとは 」](https://microsoft.github.io/botframework-solutions/overview/skills/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="92bb7-111">For more information on skills of Bot Framework, see [What is a Bot Framework skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="92bb7-112">このドキュメントでは、組織の仮想アシスタントの実装に関する考慮事項、Teamsに焦点を当てた仮想アシスタントの作成方法、関連する例、コード サンプル、および Virtual Assistant の制限事項について説明します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-112">This document guides you on Virtual Assistant implementation considerations for organizations, how to create a Teams focused Virtual Assistant, related example, code sample, and limitations of Virtual Assistant.</span></span>
<span data-ttu-id="92bb7-113">次の図は、仮想アシスタントの概要を示しています。</span><span class="sxs-lookup"><span data-stu-id="92bb7-113">The following image displays the overview of virtual assistant:</span></span>

![仮想アシスタントの概要図](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="92bb7-115">テキストメッセージアクティビティは、 [ディスパッチ](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) モデルを使用して仮想アシスタントコアによって関連するスキルにルーティングされます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-115">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="92bb7-116">実装に関する考慮事項</span><span class="sxs-lookup"><span data-stu-id="92bb7-116">Implementation considerations</span></span>

<span data-ttu-id="92bb7-117">バーチャル アシスタントの追加決定には、多くの決定要因が含まれ、組織ごとに異なります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-117">The decision to add a Virtual Assistant includes many determinants and differs for each organization.</span></span> <span data-ttu-id="92bb7-118">組織の仮想アシスタント実装のサポート要因は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="92bb7-118">The supporting factors of a Virtual Assistant implementation for your organization are as follows:</span></span>

* <span data-ttu-id="92bb7-119">中央のチームは、すべての従業員の経験を管理します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-119">A central team manages all employee experiences.</span></span> <span data-ttu-id="92bb7-120">バーチャル アシスタント エクスペリエンスを構築し、新しいスキルの追加を含むコア エクスペリエンスの更新を管理する機能があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-120">It has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
* <span data-ttu-id="92bb7-121">ビジネス機能間で複数のアプリケーションが存在し、その数は今後増加することが予想されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-121">Multiple applications exist across business functions and the number is expected to grow in the future.</span></span>
* <span data-ttu-id="92bb7-122">既存のアプリケーションは、カスタマイズ可能で、組織が所有し、バーチャルアシスタントのスキルに変換されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-122">Existing applications are customizable, owned by the organization, and are converted into skills for a Virtual Assistant.</span></span>
* <span data-ttu-id="92bb7-123">中央の従業員エクスペリエンス チームは、既存のアプリのカスタマイズに影響を与えます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-123">The central employee experiences team is able to influence customizations to existing apps.</span></span> <span data-ttu-id="92bb7-124">また、既存のアプリケーションをバーチャル アシスタント エクスペリエンスのスキルとして統合するために必要なガイダンスも提供します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-124">It also provides necessary guidance for integrating existing applications as skills in Virtual Assistant experience.</span></span>

<span data-ttu-id="92bb7-125">次の図は、バーチャルアシスタントのビジネス機能を示しています。</span><span class="sxs-lookup"><span data-stu-id="92bb7-125">The following image displays the business functions of Virtual Assistant:</span></span> 

![中央チームはアシスタントを維持し、ビジネス・ファンクション・チームがスキルを提供](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="92bb7-127">Teamsに焦点を当てたバーチャル アシスタントを作成する</span><span class="sxs-lookup"><span data-stu-id="92bb7-127">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="92bb7-128">マイクロソフトは、バーチャル アシスタントとスキルを構築するための[Visual Studio テンプレート](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate)を公開しました。</span><span class="sxs-lookup"><span data-stu-id="92bb7-128">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="92bb7-129">Visual Studioテンプレートを使用すると、アクションを持つ限られたリッチカードをサポートするテキストベースのエクスペリエンスを備えたバーチャルアシスタントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-129">With the Visual Studio template, you can create a Virtual Assistant, powered by a text based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="92bb7-130">Visual Studioベーステンプレートを拡張して、Microsoft Teamsプラットフォーム機能と優れたTeamsアプリエクスペリエンスを含めています。</span><span class="sxs-lookup"><span data-stu-id="92bb7-130">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="92bb7-131">機能の中には、豊富なアダプティブ カード、タスク モジュール、チームまたはグループ チャット、メッセージング拡張機能のサポートなどがあります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-131">A few of the capabilities include support for rich Adaptive Cards, task modules, teams or group chats, and messaging extensions.</span></span> <span data-ttu-id="92bb7-132">バーチャル アシスタントをMicrosoft Teamsに拡張する方法の詳細については、「[チュートリアル: バーチャル アシスタントをMicrosoft Teamsに拡張する](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="92bb7-132">For more information on extending Virtual Assistant to Microsoft Teams, see [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>    
<span data-ttu-id="92bb7-133">次の図は、仮想アシスタント ソリューションの高レベルの図を示しています。</span><span class="sxs-lookup"><span data-stu-id="92bb7-133">The following image displays the high level diagram of a Virtual Assistant solution:</span></span>

![仮想アシスタント ソリューションの概要図](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="92bb7-135">バーチャル アシスタントにアダプティブ カードを追加する</span><span class="sxs-lookup"><span data-stu-id="92bb7-135">Add Adaptive Cards to your Virtual Assistant</span></span>

<span data-ttu-id="92bb7-136">要求を適切にディスパッチするには、仮想アシスタントが正しい LUIS モデルとそれに関連付けられた対応するスキルを識別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-136">To dispatch requests properly, your Virtual Assistant must identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="92bb7-137">ただし、スキルに関連付けられた LUIS モデルはカード アクション テキストのトレーニングを受けているため、ディスパッチメカニズムをカード アクション アクティビティに使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="92bb7-137">However, the dispatching mechanism cannot be used for card action activities as the LUIS model associated with a skill, is trained for card action texts.</span></span> <span data-ttu-id="92bb7-138">カードアクションテキストは固定された定義済みキーワードであり、ユーザーからのコメントはされません。</span><span class="sxs-lookup"><span data-stu-id="92bb7-138">The card action texts are fixed, pre-defined keywords, and not commented from a user.</span></span>

<span data-ttu-id="92bb7-139">この欠点は、スキル情報をカードアクションペイロードに埋め込むことによって解決されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-139">This drawback is resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="92bb7-140">すべてのスキルは `skillId`  `value` 、カードアクションのフィールドに埋め込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-140">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="92bb7-141">各カードアクションアクティビティに関連するスキル情報が含まれ、バーチャルアシスタントがこの情報をディスパッチに利用できることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-141">You must ensure that each card action activity carries the relevant skill information, and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="92bb7-142">`skillId`スキル情報がカードアクションに常に存在するように、コンストラクタで指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-142">You must provide `skillId` in the constructor to ensure that the skill information is always present in card actions.</span></span>
<span data-ttu-id="92bb7-143">カード アクション データのサンプル コードは、次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-143">A card action data sample code is shown in the following section:</span></span>
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

<span data-ttu-id="92bb7-144">次 `SkillCardActionData` に、バーチャル アシスタント テンプレートのクラスを導入して `skillId` 、カード アクション ペイロードから抽出します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-144">Next, `SkillCardActionData` class in the Virtual Assistant template is introduces to extract `skillId` from the card action payload.</span></span>
<span data-ttu-id="92bb7-145">カード アクション ペイロードから抽出するコード スニペット  `skillId` を次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-145">A code snippet to extract  `skillId` from card action payload is shown in the following section:</span></span>

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

<span data-ttu-id="92bb7-146">実装は [、Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) クラスの拡張メソッドによって行われます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-146">The implementation is done by an extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>
<span data-ttu-id="92bb7-147">カード アクション データから抽出するコード スニペット  `skillId` を次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-147">A code snippet to extract  `skillId` from card action data is shown in the following section:</span></span>

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

### <a name="handle-interruptions"></a><span data-ttu-id="92bb7-148">中断の処理</span><span class="sxs-lookup"><span data-stu-id="92bb7-148">Handle interruptions</span></span>

<span data-ttu-id="92bb7-149">バーチャルアシスタントは、別のスキルが現在アクティブな状態でユーザがスキルを呼び出そうとする場合の中断を処理できます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-149">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="92bb7-150">`TeamsSkillDialog`を使用し、 `TeamsSwitchSkillDialog` ボット フレームワークのスキル[ダイアログ と](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs)[スイッチスキル ダイアログ に](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)基づいて導入されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-150">`TeamsSkillDialog`, and `TeamsSwitchSkillDialog`are introduced based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs).</span></span> <span data-ttu-id="92bb7-151">ユーザーは、スキルの経験をカードアクションから切り替えることができます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-151">They enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="92bb7-152">この要求を処理するために、バーチャル アシスタントは、スキルを切り替える確認メッセージをユーザーに求めます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-152">To handle this request, the Virtual Assistant prompts the user with a confirmation message to switch skills:</span></span>

![新しいスキルに切り替えたときに確認プロンプトを表示する](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a><span data-ttu-id="92bb7-154">タスク モジュール要求の処理</span><span class="sxs-lookup"><span data-stu-id="92bb7-154">Handle task module requests</span></span>

<span data-ttu-id="92bb7-155">仮想アシスタントにタスク モジュール機能を追加するには、仮想アシスタント アクティビティ ハンドラに 2 つのメソッド `OnTeamsTaskModuleFetchAsync` が追加されています `OnTeamsTaskModuleSubmitAsync` 。</span><span class="sxs-lookup"><span data-stu-id="92bb7-155">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="92bb7-156">これらのメソッドは、仮想アシスタントからタスクモジュール関連のアクティビティをリッスンし、要求に関連付けられたスキルを識別し、指定されたスキルに要求を転送します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-156">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="92bb7-157">要求の転送は [、skillHttp クライアント](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true)メソッドを使用して行 `PostActivityAsync` われます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-157">Request forwarding is done through the [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` method.</span></span> <span data-ttu-id="92bb7-158">`InvokeResponse`解析されて に変換された応答が返されます `TaskModuleResponse` 。</span><span class="sxs-lookup"><span data-stu-id="92bb7-158">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>


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

<span data-ttu-id="92bb7-159">カード アクションディスパッチとタスク モジュールの応答にも同様のアプローチが実行されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-159">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="92bb7-160">タスク モジュールのフェッチと送信のアクション データが更新され、 が含まれます `skillId` 。</span><span class="sxs-lookup"><span data-stu-id="92bb7-160">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="92bb7-161">アクティビティ拡張メソッド `GetSkillId` は `skillId` 、呼び出す必要があるスキルに関する詳細を提供するペイロードから抽出します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-161">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="92bb7-162">メソッドのコード `OnTeamsTaskModuleFetchAsync` スニペット `OnTeamsTaskModuleSubmitAsync` は、次のセクションで示します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-162">The code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods are given in the following section:</span></span>

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

<span data-ttu-id="92bb7-163">さらに、 `validDomains` スキルを通じて呼び出されるタスクモジュールが適切にレンダリングされるように、Virtual Assistantのマニフェストファイルのセクションにすべてのスキルドメインを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-163">Additionally, you must include all skill domains in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked through a skill render properly.</span></span>

### <a name="handle-collaborative-app-scopes"></a><span data-ttu-id="92bb7-164">共同アプリのスコープを処理する</span><span class="sxs-lookup"><span data-stu-id="92bb7-164">Handle collaborative app scopes</span></span>

<span data-ttu-id="92bb7-165">Teamsアプリは、1:1 チャット、グループ チャット、チャネルなど、複数のスコープに存在できます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-165">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="92bb7-166">コア仮想アシスタントテンプレートは、1:1チャット用に設計されています。</span><span class="sxs-lookup"><span data-stu-id="92bb7-166">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="92bb7-167">オンボーディング エクスペリエンスの一環として、バーチャル アシスタントはユーザーに名前を求め、ユーザー状態を維持します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-167">As part of the onboarding experience Virtual Assistant prompts users for name and maintains user state.</span></span> <span data-ttu-id="92bb7-168">そのオンボーディングの経験は、グループ チャットやチャネル のスコープには適していないので、削除されました。</span><span class="sxs-lookup"><span data-stu-id="92bb7-168">Since that onboarding experience is not suited for group chat or channel scopes it has been removed.</span></span>

<span data-ttu-id="92bb7-169">スキルは、1:1 チャット、グループ チャット、チャネル会話など、複数のスコープでアクティビティを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-169">Skills should handle activities in multiple scopes, such as 1:1 chat, group chat, and channel conversation.</span></span> <span data-ttu-id="92bb7-170">これらのスコープのいずれかがサポートされていない場合、スキルは適切なメッセージで応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-170">If any of these scopes are not supported, skills must respond with an appropriate message.</span></span>

<span data-ttu-id="92bb7-171">バーチャルアシスタントコアには、以下の処理機能が追加されました。</span><span class="sxs-lookup"><span data-stu-id="92bb7-171">The following  processing functions have been added to Virtual Assistant core:</span></span>

* <span data-ttu-id="92bb7-172">バーチャルアシスタントは、グループチャットやチャンネルからテキストメッセージなしで起動できます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-172">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
* <span data-ttu-id="92bb7-173">アーティキュレーションは、ディスパッチ モジュールにメッセージを送信する前にクリーンアップされます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-173">Articulations are cleaned before sending the message to the dispatch module.</span></span> <span data-ttu-id="92bb7-174">たとえば、ボットの必要な@mentionを削除します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-174">For example, remove the necessary @mention of the bot.</span></span>

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

### <a name="handle-messaging-extensions"></a><span data-ttu-id="92bb7-175">メッセージング拡張機能の処理</span><span class="sxs-lookup"><span data-stu-id="92bb7-175">Handle messaging extensions</span></span>

<span data-ttu-id="92bb7-176">メッセージング拡張機能のコマンドは、アプリ マニフェスト ファイルで宣言されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-176">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="92bb7-177">メッセージング拡張機能のユーザー インターフェイスは、これらのコマンドによって供給されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-177">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="92bb7-178">バーチャル アシスタントが添付されたスキルとしてメッセージング拡張機能コマンドを実行するには、バーチャル アシスタントのマニフェストにそれらのコマンドが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-178">For a Virtual Assistant to power a messaging extension command as an attached skill, a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="92bb7-179">個々のスキルのマニフェストから仮想アシスタントのマニフェストにコマンドを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-179">You must add the commands from an individual skill's manifest to the Virtual Assistant's manifest.</span></span> <span data-ttu-id="92bb7-180">コマンド ID は、区分線 を通してスキルのアプリ ID を追加することによって、関連付けられたスキルに関する情報を提供 `:` します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-180">The command ID provides information about an associated skill by appending the skill's app ID through a separator `:`.</span></span>

<span data-ttu-id="92bb7-181">スキルのマニフェスト ファイルのスニペットは、次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-181">The snippet from a skill's manifest file is shown in the following section:</span></span>

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

<span data-ttu-id="92bb7-182">対応する仮想アシスタント マニフェスト ファイルのコード スニペットを次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-182">The corresponding Virtual Assistant manifest file code snippet is shown in the following section:</span></span>

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

<span data-ttu-id="92bb7-183">ユーザーがコマンドを呼び出すと、仮想アシスタントは、コマンド ID を解析して関連付けられたスキルを識別し、コマンド ID から余分なサフィックスを削除してアクティビティ `:<skill_id>` を更新し、対応するスキルに転送できます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-183">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix `:<skill_id>` from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="92bb7-184">スキルのコードは、余分な接尾辞を処理する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="92bb7-184">The code for a skill doesnot need to handle the extra suffix.</span></span> <span data-ttu-id="92bb7-185">したがって、スキル間でのコマンド ID 間の競合は回避されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-185">Thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="92bb7-186">この方法では、**作成\*\*\*\*、commandBox、\*\*\*\*メッセージ** など、すべてのコンテキスト内のスキルのすべての検索コマンドとアクションコマンドは、仮想アシスタントによって供給されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-186">With this approach, all the search and action commands of a skill within all contexts, such as **compose**, **commandBox**, and **message** are powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="92bb7-187">メッセージング拡張アクティビティーの中には、コマンド ID が含まれていないものがあります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-187">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="92bb7-188">たとえば、 `composeExtension/selectItem` 呼び出しタップアクションの値のみが含まれます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-188">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="92bb7-189">関連付けられたスキルを識別するには、 `skillId`  の応答を形成しながら、各項目カードに添付されます `OnTeamsMessagingExtensionQueryAsync` 。</span><span class="sxs-lookup"><span data-stu-id="92bb7-189">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="92bb7-190">これは、 [仮想アシスタントにアダプティブ カードを追加する方法と](#add-adaptive-cards-to-your-virtual-assistant)似ています。</span><span class="sxs-lookup"><span data-stu-id="92bb7-190">This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example"></a><span data-ttu-id="92bb7-191">例</span><span class="sxs-lookup"><span data-stu-id="92bb7-191">Example</span></span>

<span data-ttu-id="92bb7-192">次の例は、Book-a-room アプリ テンプレートをバーチャル アシスタント スキルに変換する方法を示しています: Book-a-room は、ユーザーが現在の時刻から 30 分、60 分、または 90 分の会議室をすばやく見つけて予約できるようにするMicrosoft Teamsです。</span><span class="sxs-lookup"><span data-stu-id="92bb7-192">The following example shows how to convert the Book-a-room app template to a Virtual Assistant skill: Book-a-room is a Microsoft Teams that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="92bb7-193">デフォルトの時間は 30 分です。</span><span class="sxs-lookup"><span data-stu-id="92bb7-193">The default time is 30 minutes.</span></span> <span data-ttu-id="92bb7-194">会議室予約ボットは、個人の会話または一対一の会話を対象としています。</span><span class="sxs-lookup"><span data-stu-id="92bb7-194">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="92bb7-195">次の図は、 **ブックのルーム** スキルを持つバーチャルアシスタントを示しています。</span><span class="sxs-lookup"><span data-stu-id="92bb7-195">The following image displays a Virtual Assistant with a **book a room** skill:</span></span>

![「部屋を予約する」スキルを持つバーチャルアシスタント](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="92bb7-197">以下は、バーチャルアシスタントに添付されたスキルに変換するために導入されたデルタ変更です。</span><span class="sxs-lookup"><span data-stu-id="92bb7-197">Followings are the delta changes introduced to convert it to a skill which is attached to a Virtual Assistant.</span></span> <span data-ttu-id="92bb7-198">同様のガイドラインに従って、既存の v4 ボットをスキルに変換します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-198">Similar guidelines are followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="92bb7-199">スキルマニフェスト</span><span class="sxs-lookup"><span data-stu-id="92bb7-199">Skill manifest</span></span>

<span data-ttu-id="92bb7-200">スキル マニフェストは、スキルのメッセージング エンドポイント、ID、名前、およびその他の関連メタデータを公開する JSON ファイルです。</span><span class="sxs-lookup"><span data-stu-id="92bb7-200">A skill manifest is a JSON file that exposes a skill's messaging endpoint, ID, name, and other relevant metadata.</span></span> <span data-ttu-id="92bb7-201">このマニフェストは、Microsoft Teamsでアプリをサイドローディングするために使用されるマニフェストとは異なります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-201">This manifest is different than the manifest used for sideloading an app in Microsoft Teams.</span></span> <span data-ttu-id="92bb7-202">バーチャルアシスタントは、スキルを添付するための入力として、このファイルへのパスを必要とします。</span><span class="sxs-lookup"><span data-stu-id="92bb7-202">A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="92bb7-203">ボットの wwwroot フォルダーに次のマニフェストを追加しました。</span><span class="sxs-lookup"><span data-stu-id="92bb7-203">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="92bb7-204">LUIS 統合</span><span class="sxs-lookup"><span data-stu-id="92bb7-204">LUIS Integration</span></span>

<span data-ttu-id="92bb7-205">バーチャル アシスタントのディスパッチ モデルは、添付スキルの LUIS モデルの上に構築されています。</span><span class="sxs-lookup"><span data-stu-id="92bb7-205">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="92bb7-206">ディスパッチ モデルは、すべてのテキスト アクティビティの意図を識別し、それに関連付けられたスキルを見つけます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-206">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="92bb7-207">バーチャル アシスタントでは、スキルを `.lu` アタッチする際に入力として、スキルの LUIS モデルの形式が必要です。</span><span class="sxs-lookup"><span data-stu-id="92bb7-207">Virtual Assistant requires skill's LUIS model in `.lu` format as an input while attaching a skill.</span></span> <span data-ttu-id="92bb7-208">LUIS json は `.lu` 、ボットフレームワーク cli ツールを使用して形式に変換されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-208">LUIS json is converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="92bb7-209">ブックルームボットには、ユーザー向けの主なコマンドが2つ用意されています。</span><span class="sxs-lookup"><span data-stu-id="92bb7-209">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="92bb7-210">LUIS モデルは、これら 2 つのコマンドを理解して構築しました。</span><span class="sxs-lookup"><span data-stu-id="92bb7-210">We have built a LUIS model by understanding these two commands.</span></span> <span data-ttu-id="92bb7-211">対応するシークレットは、 に入力する必要があります `cognitivemodels.json` 。</span><span class="sxs-lookup"><span data-stu-id="92bb7-211">Corresponding secrets must be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="92bb7-212">対応する LUIS JSON ファイルは [、ここにあります](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json)。</span><span class="sxs-lookup"><span data-stu-id="92bb7-212">The corresponding LUIS JSON file is found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json).</span></span>
<span data-ttu-id="92bb7-213">対応する `.lu` ファイルは、次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-213">The corresponding `.lu` file is shown in the following section:</span></span>

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

<span data-ttu-id="92bb7-214">この方法では、ユーザーが仮想アシスタントに対して発行したコマンド `book room` は、 `manage favorites` ボットに関連付けられているコマンドとして識別され `Book-a-room` 、このスキルに転送されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-214">With this approach, any command issued by a user to Virtual Assistant related to `book room` or `manage favorites` are identified as a command associated with `Book-a-room` bot and is forwarded to this skill.</span></span>
<span data-ttu-id="92bb7-215">一方、ボットは、 `Book-a-room room` これらのコマンドがフル入力されていない場合、LUIS モデルを使用してこれらのコマンドを理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-215">On the other hand, `Book-a-room room` bot needs to use LUIS model to understand these commands if they are not typed full.</span></span> <span data-ttu-id="92bb7-216">例: `I want to manage my favorite rooms`。</span><span class="sxs-lookup"><span data-stu-id="92bb7-216">For example: `I want to manage my favorite rooms`.</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="92bb7-217">多言語サポート</span><span class="sxs-lookup"><span data-stu-id="92bb7-217">Multi-Language support</span></span>

<span data-ttu-id="92bb7-218">例として、英語のカルチャのみを持つ LUIS モデルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-218">As an example, a LUIS model with only English culture is created.</span></span> <span data-ttu-id="92bb7-219">他の言語に対応する LUIS モデルを作成し、 にエントリを追加できます `cognitivemodels.json` 。</span><span class="sxs-lookup"><span data-stu-id="92bb7-219">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="92bb7-220">対応するファイルを `.lu` luisFolder パスに並行して追加します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-220">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="92bb7-221">フォルダ構造は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-221">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="92bb7-222">パラメータを変更するには `languages` 、botskills コマンドを次のように更新します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-222">To modify `languages` parameter, update botskills command as follows:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="92bb7-223">バーチャルアシスタントは `SetLocaleMiddleware` 、現在のロケールを識別し、対応するディスパッチモデルを呼び出すために使用します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-223">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="92bb7-224">ボット フレームワークのアクティビティには、このミドルウェアで使用されるロケール フィールドがあります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-224">Bot framework activity has locale field which is used by this middleware.</span></span> <span data-ttu-id="92bb7-225">スキルにも同じものを使うことができます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-225">You can use the same for your skill as well.</span></span> <span data-ttu-id="92bb7-226">ブックルームボットはこのミドルウェアを使用せず、代わりに Bot フレームワークアクティビティの [clientInfo エンティティ](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)からロケールを取得します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-226">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="92bb7-227">クレーム検証</span><span class="sxs-lookup"><span data-stu-id="92bb7-227">Claim validation</span></span>

<span data-ttu-id="92bb7-228">呼び出し元をスキルに制限する [要求検証ツール](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) を追加しました。</span><span class="sxs-lookup"><span data-stu-id="92bb7-228">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="92bb7-229">バーチャル アシスタントがこのスキルを呼び出すことを許可するには、 `AllowedCallers` `appsettings` その特定のバーチャル アシスタントのアプリ ID を配列に入力します。</span><span class="sxs-lookup"><span data-stu-id="92bb7-229">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="92bb7-230">許可された発信者配列は、どのスキル消費者がスキルにアクセスできるかを制限できます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-230">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="92bb7-231">この配列に単一のエントリ `*` を追加して、スキルコンシューマからの呼び出しを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-231">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```

<span data-ttu-id="92bb7-232">スキルに要求検証を追加する方法の詳細については、「スキルへの [要求検証の追加」を](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)参照してください。</span><span class="sxs-lookup"><span data-stu-id="92bb7-232">For more information on adding claims validation to a skill, see [add claims validation to skill](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span></span>

### <a name="limitation-of-card-refresh"></a><span data-ttu-id="92bb7-233">カード更新の制限</span><span class="sxs-lookup"><span data-stu-id="92bb7-233">Limitation of card refresh</span></span> 

<span data-ttu-id="92bb7-234">カードの更新などの更新アクティビティは、バーチャルアシスタント[(githubの問題](https://github.com/microsoft/botbuilder-dotnet/issues/3686))を通じてまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="92bb7-234">Updating activity, such as card refresh is not supported yet through Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="92bb7-235">したがって、すべてのカード更新呼び出しを `UpdateActivityAsync` 新しいカードコールの投稿に置き換えました `SendActivityAsync` 。</span><span class="sxs-lookup"><span data-stu-id="92bb7-235">Hence, we have replaced all card refresh calls `UpdateActivityAsync` with posting new card calls `SendActivityAsync`.</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="92bb7-236">カードアクションとタスクモジュールフロー</span><span class="sxs-lookup"><span data-stu-id="92bb7-236">Card actions and task module flows</span></span>

<span data-ttu-id="92bb7-237">カードアクションまたはタスクモジュールの活動を関連するスキルに転送するには、スキルをそのスキルに埋め込む必要があります `skillId` 。</span><span class="sxs-lookup"><span data-stu-id="92bb7-237">To forward card action or task module activities to an associated skill, the skill must embed `skillId` to it.</span></span>
<span data-ttu-id="92bb7-238">`Book-a-room` ボットカードアクション、タスクモジュールのフェッチと送信アクションのペイロードは、パラメータとして含まれるように変更されます `skillId` 。</span><span class="sxs-lookup"><span data-stu-id="92bb7-238">`Book-a-room` bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="92bb7-239">詳細については、このドキュメントの [この](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="92bb7-239">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="92bb7-240">グループチャットまたはチャネルスコープからのアクティビティの処理</span><span class="sxs-lookup"><span data-stu-id="92bb7-240">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="92bb7-241">`Book-a-room bot` は、個人チャットや 1:1 スコープなどのプライベート チャット用に設計されています。</span><span class="sxs-lookup"><span data-stu-id="92bb7-241">`Book-a-room bot` is designed for private chats, such as personal or 1:1 scope only.</span></span> <span data-ttu-id="92bb7-242">グループチャットとチャンネルスコープをサポートするようにバーチャルアシスタントをカスタマイズしたので、バーチャルアシスタントはチャンネルスコープから呼び出す必要があるため、 `Book-a-room` ボットは同じスコープのアクティビティを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-242">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant must be invoked from the channel scopes and thus, `Book-a-room` bot must get activities for the same scope.</span></span> <span data-ttu-id="92bb7-243">したがって `Book-a-room` 、ボットは、これらのアクティビティを処理するようにカスタマイズされます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-243">Hence `Book-a-room`bot is customized to handle those activities.</span></span> <span data-ttu-id="92bb7-244">`OnMessageActivityAsync`ボットのアクティビティ ハンドラのチェックイン メソッドを見つけることができます `Book-a-room` 。</span><span class="sxs-lookup"><span data-stu-id="92bb7-244">You can find the check in `OnMessageActivityAsync` methods of `Book-a-room` bot's activity handler.</span></span>

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

<span data-ttu-id="92bb7-245">また [、Bot Framework ソリューション リポジトリ](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) から既存のスキルを活用したり、新しいスキルをゼロから作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-245">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="92bb7-246">新しいスキルを作成するには、 [新しいスキルを作成するためのチュートリアルを](https://microsoft.github.io/botframework-solutions/overview/skills/)参照してください。</span><span class="sxs-lookup"><span data-stu-id="92bb7-246">For creating a new skill, see [tutorials to create a new skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="92bb7-247">バーチャル アシスタントとスキル アーキテクチャのドキュメントについては、[バーチャル アシスタントとスキル アーキテクチャ](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="92bb7-247">For Virtual Assistant and skills architecture documentation, see[Virtual Assistant and skills architecture](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).</span></span>  

## <a name="limitations-of-virtual-assistant"></a><span data-ttu-id="92bb7-248">バーチャル アシスタントの制限事項</span><span class="sxs-lookup"><span data-stu-id="92bb7-248">Limitations of Virtual Assistant</span></span> 

* <span data-ttu-id="92bb7-249">**会話の終了**: スキルは `endOfConversation` 、会話が終了したときにアクティビティを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-249">**EndOfConversation**: A skill must send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="92bb7-250">アクティビティに基づいて、仮想アシスタントはその特定のスキルでコンテキストを終了し、仮想アシスタントのルートコンテキストに戻ります。</span><span class="sxs-lookup"><span data-stu-id="92bb7-250">Based on the activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's root context.</span></span> <span data-ttu-id="92bb7-251">ブックルームボットの場合、会話が終了する明確な状態はありません。</span><span class="sxs-lookup"><span data-stu-id="92bb7-251">For Book-a-room bot, there is no clear state where conversation is ended.</span></span> <span data-ttu-id="92bb7-252">したがって、ボットからは送信されておらず `endOfConversation` `Book-a-room` 、ユーザーがルートコンテキストに戻りたいときは、コマンドで簡単に行うことができます `start over` 。</span><span class="sxs-lookup"><span data-stu-id="92bb7-252">Hence we have not sent `endOfConversation` from `Book-a-room` bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>  
* <span data-ttu-id="92bb7-253">**カードの更新**: カードの更新は、バーチャル アシスタントを通じてまだサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="92bb7-253">**Card refresh**: Card refresh is not yet supported through Virtual Assistant.</span></span>  
* <span data-ttu-id="92bb7-254">**メッセージング拡張機能**:</span><span class="sxs-lookup"><span data-stu-id="92bb7-254">**Messaging extensions**:</span></span>
  * <span data-ttu-id="92bb7-255">現在、バーチャル アシスタントは、メッセージング拡張機能に対して最大 10 個のコマンドをサポートできます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-255">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  * <span data-ttu-id="92bb7-256">メッセージング拡張機能の構成は、個々のコマンドではなく、拡張機能全体に適用されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-256">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="92bb7-257">これにより、バーチャル アシスタントを使用して個々のスキルの設定が制限されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-257">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  * <span data-ttu-id="92bb7-258">メッセージング拡張機能コマンド ID の最大長は [64 文字](../resources/schema/manifest-schema.md#composeextensions) で、スキル情報の埋め込みに 37 文字が使用されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-258">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters are used for embedding skill information.</span></span> <span data-ttu-id="92bb7-259">したがって、コマンド ID の更新制約は 27 文字に制限されます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-259">Thus, updated constraints for command ID are limited to 27 characters.</span></span>

<span data-ttu-id="92bb7-260">また [、Bot Framework ソリューション リポジトリ](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) から既存のスキルを活用したり、新しいスキルをゼロから作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-260">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="92bb7-261">後でのチュートリアルは [、ここで](https://microsoft.github.io/botframework-solutions/overview/skills/)見つけることができます.</span><span class="sxs-lookup"><span data-stu-id="92bb7-261">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="92bb7-262">バーチャルアシスタントとスキルアーキテクチャの [ドキュメント](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="92bb7-262">Please refer to [documentation](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) for Virtual Assistant and skills architecture.</span></span>

## <a name="code-sample"></a><span data-ttu-id="92bb7-263">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="92bb7-263">Code sample</span></span>

| <span data-ttu-id="92bb7-264">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="92bb7-264">**Sample name**</span></span> | <span data-ttu-id="92bb7-265">**説明**</span><span class="sxs-lookup"><span data-stu-id="92bb7-265">**Description**</span></span> | <span data-ttu-id="92bb7-266">**C#**</span><span class="sxs-lookup"><span data-stu-id="92bb7-266">**C#**</span></span> | <span data-ttu-id="92bb7-267">**.NET**</span><span class="sxs-lookup"><span data-stu-id="92bb7-267">**.NET**</span></span> |
|----------|-----------------|----------|------------------|
| <span data-ttu-id="92bb7-268">ビジュアルスタジオテンプレートを更新</span><span class="sxs-lookup"><span data-stu-id="92bb7-268">Updated visual studio template</span></span> | <span data-ttu-id="92bb7-269">チームの機能をサポートするテンプレートをカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="92bb7-269">Customized template to support teams capabilities.</span></span> | [<span data-ttu-id="92bb7-270">View</span><span class="sxs-lookup"><span data-stu-id="92bb7-270">View</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| <span data-ttu-id="92bb7-271">ブック・ア・ルーム・ボット・スキル・コード</span><span class="sxs-lookup"><span data-stu-id="92bb7-271">Book-a-room bot skill code</span></span> | <span data-ttu-id="92bb7-272">外出先で会議室を素早く見つけて予約できます。</span><span class="sxs-lookup"><span data-stu-id="92bb7-272">Lets you quickly find and book a meeting room on the go.</span></span> |  | [<span data-ttu-id="92bb7-273">View</span><span class="sxs-lookup"><span data-stu-id="92bb7-273">View</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |


## <a name="see-also"></a><span data-ttu-id="92bb7-274">関連項目</span><span class="sxs-lookup"><span data-stu-id="92bb7-274">See also</span></span>

- [<span data-ttu-id="92bb7-275">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="92bb7-275">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

- [<span data-ttu-id="92bb7-276">会議室予約</span><span class="sxs-lookup"><span data-stu-id="92bb7-276">Book-a-room</span></span>](app-templates.md#book-a-room)

- [<span data-ttu-id="92bb7-277">Microsoft Teamsボット</span><span class="sxs-lookup"><span data-stu-id="92bb7-277">Microsoft Teams bot</span></span>](../bots/what-are-bots.md)