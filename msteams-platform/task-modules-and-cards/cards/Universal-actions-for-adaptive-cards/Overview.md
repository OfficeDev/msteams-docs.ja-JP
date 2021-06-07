---
title: アダプティブ カードのユニバーサル アクションの概要
description: アダプティブ カードのユニバーサル アクションの概要を簡単に説明します。
ms.topic: overview
localization_priority: Normal
ms.openlocfilehash: f8980743954c4dff2ced464bc599439c7519cefe
ms.sourcegitcommit: d1d1143e285cac5f23590ccba5389616d08f94b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2021
ms.locfileid: "52781619"
---
# <a name="universal-actions-for-adaptive-cards"></a><span data-ttu-id="4809f-103">アダプティブ カードのユニバーサル アクション</span><span class="sxs-lookup"><span data-stu-id="4809f-103">Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="4809f-104">アダプティブ カードのユニバーサル アクションは、アダプティブ カードのレイアウトとレンダリングがユニバーサルであるにもかかわらず、アクション処理が行えなくても、開発者からのフィードバックから進化しました。</span><span class="sxs-lookup"><span data-stu-id="4809f-104">Universal Actions for Adaptive Cards evolved from developer feedback that even though layout and rendering for Adaptive Cards was universal, action handling was not.</span></span> <span data-ttu-id="4809f-105">開発者が同じカードを別の場所に送信する場合でも、異なる方法でアクションを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4809f-105">Even if a developer wanted to send the same card to different places, they have to handle actions differently.</span></span>

<span data-ttu-id="4809f-106">アダプティブ カードのユニバーサル アクションは、アクションを処理する一般的なバックエンドとしてボットを提供し、Teams や Outlook などのアプリ間で動作する新しいアクションの種類 `Action.Execute` を導入します。</span><span class="sxs-lookup"><span data-stu-id="4809f-106">Universal Actions for Adaptive Cards brings the bot as the common backend for handling actions and introduces a new action type, `Action.Execute`, which works across apps, such as Teams and Outlook.</span></span>

<span data-ttu-id="4809f-107">このドキュメントでは、ユニバーサル アクション モデルを使用して、プラットフォームやアプリケーション間でアダプティブ カードを操作するユーザー エクスペリエンスを強化する方法を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="4809f-107">This document helps you to understand how you can use Universal Actions model to enhance user experience of interacting with Adaptive Cards across platforms and applications.</span></span>

> [!NOTE]
> <span data-ttu-id="4809f-108">アダプティブ カードのユニバーサル アクションのサポートは、ボットから送信されたカードでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="4809f-108">Support for Universal Actions for Adaptive Cards is only available for cards sent by bot.</span></span> <span data-ttu-id="4809f-109">新規作成ボックスとリンク解除カードを介して送信されるカードのサポートは、近日公開予定です。</span><span class="sxs-lookup"><span data-stu-id="4809f-109">Support for cards sent through compose box and link unfurling cards is coming soon.</span></span>

## <a name="enhance-user-experiences-with-universal-actions-for-adaptive-cards"></a><span data-ttu-id="4809f-110">アダプティブ カードのユニバーサル アクションを使用してユーザー エクスペリエンスを強化する</span><span class="sxs-lookup"><span data-stu-id="4809f-110">Enhance user experiences with Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="4809f-111">アダプティブ カードのユニバーサル アクションは、次のシナリオを有効にすることでユーザー エクスペリエンスを強化します。</span><span class="sxs-lookup"><span data-stu-id="4809f-111">Universal Actions for Adaptive Cards enhances user experience by enabling the following scenarios:</span></span>

* [<span data-ttu-id="4809f-112">ユニバーサル アクション</span><span class="sxs-lookup"><span data-stu-id="4809f-112">Universal Actions</span></span>](#universal-actions)
* [<span data-ttu-id="4809f-113">ユーザー固有のビュー</span><span class="sxs-lookup"><span data-stu-id="4809f-113">User Specific Views</span></span>](#user-specific-views)
* [<span data-ttu-id="4809f-114">シーケンシャル ワークフローのサポート</span><span class="sxs-lookup"><span data-stu-id="4809f-114">Sequential Workflow support</span></span>](#sequential-workflow-support)
* [<span data-ttu-id="4809f-115">最新のビュー</span><span class="sxs-lookup"><span data-stu-id="4809f-115">Up to date views</span></span>](#up-to-date-views)

### <a name="universal-actions"></a><span data-ttu-id="4809f-116">ユニバーサル アクション</span><span class="sxs-lookup"><span data-stu-id="4809f-116">Universal Actions</span></span>

<span data-ttu-id="4809f-117">アダプティブ カードのユニバーサル アクションの前に、次のように異なるホストが異なるアクション モデルを提供しました。</span><span class="sxs-lookup"><span data-stu-id="4809f-117">Before the Universal Actions for Adaptive Cards, different hosts provided different action models as follows:</span></span>

* <span data-ttu-id="4809f-118">Teamsボットを使用する場合、実際の通信モデルを基になるチャネル `Action.Submit` に延期するアプローチ。</span><span class="sxs-lookup"><span data-stu-id="4809f-118">Teams or bots used `Action.Submit`, an approach which defers the actual communication model to the underlying channel.</span></span>
* <span data-ttu-id="4809f-119">Outlookアダプティブ カード `Action.Http` ペイロードで明示的に指定されたバックエンド サービスとの通信に使用されます。</span><span class="sxs-lookup"><span data-stu-id="4809f-119">Outlook used `Action.Http` to communicate with the backend service explicitly specified in the Adaptive Card payload.</span></span>

<span data-ttu-id="4809f-120">次の図は、現在の一貫性のないアクション モデルを示しています。</span><span class="sxs-lookup"><span data-stu-id="4809f-120">The following image shows the current inconsistent action model:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/current-teams-outlook-action-model.png" alt-text="一貫性のないアクション モデル":::

<span data-ttu-id="4809f-122">アダプティブ カードのユニバーサル アクションを使用すると、さまざまな `Action.Execute` プラットフォーム間でのアクション処理に使用できます。</span><span class="sxs-lookup"><span data-stu-id="4809f-122">With the Universal Actions for Adaptive Cards, you can use `Action.Execute` for action handling across different platforms.</span></span> <span data-ttu-id="4809f-123">`Action.Execute`を含むハブ間Teams動作Outlook。</span><span class="sxs-lookup"><span data-stu-id="4809f-123">`Action.Execute` works across hubs including Teams and Outlook.</span></span> <span data-ttu-id="4809f-124">さらに、アダプティブ カードは、トリガーされた呼び出し要求に対する `Action.Execute` 応答として返されます。</span><span class="sxs-lookup"><span data-stu-id="4809f-124">In addition, an Adaptive Card can be returned as response for an `Action.Execute` triggered invoke request.</span></span>

<span data-ttu-id="4809f-125">次の図は、新しいユニバーサル アクション モデルを示しています。</span><span class="sxs-lookup"><span data-stu-id="4809f-125">The following image shows the new Universal Action model:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-action-model.png" alt-text="アダプティブ カードの新しいユニバーサル アクション":::

<span data-ttu-id="4809f-127">これで、同じカードを両方、Teams、Outlookに送信し、基になるボットを使用して互いに同期することができます。</span><span class="sxs-lookup"><span data-stu-id="4809f-127">You can now send the same card to both, Teams and Outlook, and keep them in sync with each other using the underlying bot.</span></span> <span data-ttu-id="4809f-128">いずれかのプラットフォームで実行されるアクションは、このビルドで一度だけ他のプラットフォームに反映され、任意の場所 *(アダプティブ* カード用ユニバーサル アクション) モデルを展開します。</span><span class="sxs-lookup"><span data-stu-id="4809f-128">Any action taken on either platform is reflected to the other with this *build once, deploy anywhere* (Universal Actions for Adaptive Cards) model.</span></span>

<span data-ttu-id="4809f-129">次の図は、アダプティブ カードのユニバーサル アクションを表TeamsとOutlook。</span><span class="sxs-lookup"><span data-stu-id="4809f-129">The following image depicts the Universal Actions for Adaptive Cards for both Teams and Outlook:</span></span>

# <a name="mobile"></a>[<span data-ttu-id="4809f-130">モバイル</span><span class="sxs-lookup"><span data-stu-id="4809f-130">Mobile</span></span>](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-teams-outlook.jpg" alt-text="モバイルで同じカードをTeamsとOutlook":::

# <a name="desktop"></a>[<span data-ttu-id="4809f-132">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="4809f-132">Desktop</span></span>](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-teams-outlook.png" alt-text="同じカードをTeamsとOutlook":::

* * *

### <a name="user-specific-views"></a><span data-ttu-id="4809f-134">ユーザー固有のビュー</span><span class="sxs-lookup"><span data-stu-id="4809f-134">User Specific Views</span></span>

<span data-ttu-id="4809f-135">現在、チャットまたはチャネルTeamsユーザーは、アダプティブ カードでまったく同じビューアクションとボタン アクションを表示します。</span><span class="sxs-lookup"><span data-stu-id="4809f-135">Today every user in the Teams chat or channel sees the exact same view and button actions on the Adaptive Card.</span></span> <span data-ttu-id="4809f-136">ただし、特定のシナリオでは、特定のユーザーが異なる方法で行動し、同じチャットまたはチャネル内の異なる情報にアクセスする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4809f-136">However, in certain scenarios there is a requirement for certain users to act differently and have access to different information within the same chat or channel.</span></span>

<span data-ttu-id="4809f-137">たとえば、チャットまたはチャネルでインシデント レポート カードを送信する場合、インシデントが割り当てられているユーザーだけが [解決] ボタンを表示 **する必要** があります。</span><span class="sxs-lookup"><span data-stu-id="4809f-137">For example, if you send an incident reporting card in a chat or channel, only the user who is assigned the incident must see a **Resolve** button.</span></span> <span data-ttu-id="4809f-138">一方、インシデント作成者には [編集]ボタンが表示され、他のすべてのユーザーはインシデントの詳細のみを表示できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="4809f-138">On the other hand, the incident creator must see an **Edit** button and all other users must only be able to view details of the incident.</span></span> <span data-ttu-id="4809f-139">これは、プロパティによって有効になっているユーザー固有のビューによって可能 `refresh` になります。</span><span class="sxs-lookup"><span data-stu-id="4809f-139">This is made possible by User Specific Views that is enabled by the `refresh` property.</span></span>

<span data-ttu-id="4809f-140">次の図は、チャット内の異なるユーザーが要件に基づいて異なるアクションを表示するチケット メッセージング拡張機能 (ME) の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="4809f-140">The following image shows an example of a ticketing messaging extension (ME) where different users in the chat are shown different actions based on the requirement:</span></span>

# <a name="mobile"></a>[<span data-ttu-id="4809f-141">モバイル</span><span class="sxs-lookup"><span data-stu-id="4809f-141">Mobile</span></span>](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="モバイル ユーザー固有のビュー":::

# <a name="desktop"></a>[<span data-ttu-id="4809f-143">デスクトップ</span><span class="sxs-lookup"><span data-stu-id="4809f-143">Desktop</span></span>](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="ユーザー固有のビュー":::

* * *

<span data-ttu-id="4809f-145">詳細については、「ユーザー固有の [ビューのサンプル」を参照してください](User-Specific-Views.md)。</span><span class="sxs-lookup"><span data-stu-id="4809f-145">For more information, see [sample for User Specific Views](User-Specific-Views.md).</span></span>

### <a name="sequential-workflow-support"></a><span data-ttu-id="4809f-146">シーケンシャル ワークフローのサポート</span><span class="sxs-lookup"><span data-stu-id="4809f-146">Sequential Workflow support</span></span>

<span data-ttu-id="4809f-147">シーケンシャル ワークフローのサポートにより、ユーザーは別のカードを個別に送信することなく、一連のワークフローを進めできます。</span><span class="sxs-lookup"><span data-stu-id="4809f-147">With Sequential Workflow support, users can progress through a series of workflows without sending different cards separately.</span></span> <span data-ttu-id="4809f-148">これは、アクションに応答してアダプティブ カード `Action.Execute` を返す機能によって可能になります。</span><span class="sxs-lookup"><span data-stu-id="4809f-148">This is made possible by the ability of `Action.Execute` to return an Adaptive Card in response to an action.</span></span> <span data-ttu-id="4809f-149">また、チャットまたはチャネル内のすべてのユーザーは、チャット内の他のユーザーのカードを変更せずにワークフローを進めできます。</span><span class="sxs-lookup"><span data-stu-id="4809f-149">Also, any user in the chat or channel can progress through their workflow without modifying the card for other users in the chat.</span></span>

<span data-ttu-id="4809f-150">次の図は、食品の注文ボットの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="4809f-150">The following image illustrates a food ordering bot example:</span></span> <br/>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="4809f-151">次の図は、チャットまたはチャネル内のユーザーごとにさまざまな状態を示しています。</span><span class="sxs-lookup"><span data-stu-id="4809f-151">The following image shows the various states for different users in the chat or channel:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="ケータリング ボットの状態":::

<span data-ttu-id="4809f-153">詳細については、「シーケンシャル ワークフロー [のサンプル」を参照してください](Sequential-Workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="4809f-153">For more information, see [sample for Sequential Workflow](Sequential-Workflows.md).</span></span>

### <a name="up-to-date-views"></a><span data-ttu-id="4809f-154">最新のビュー</span><span class="sxs-lookup"><span data-stu-id="4809f-154">Up to date views</span></span>

<span data-ttu-id="4809f-155">自動的に更新されるアダプティブ カードを作成できます。</span><span class="sxs-lookup"><span data-stu-id="4809f-155">You can create Adaptive Cards that update automatically.</span></span> <span data-ttu-id="4809f-156">たとえば、ユーザーが送信した承認要求を指定できます。</span><span class="sxs-lookup"><span data-stu-id="4809f-156">For example, it can be an approval request sent by a user.</span></span> <span data-ttu-id="4809f-157">承認後、カードは要求の承認時間と要求を承認したユーザーに関する詳細を自動的に表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4809f-157">After approval, the card must automatically display details about the request approval time and who approved the request.</span></span> <span data-ttu-id="4809f-158">更新モデルを使用すると、このような最新のビューを提供できます。</span><span class="sxs-lookup"><span data-stu-id="4809f-158">The refresh model enables you to provide such up to date views.</span></span> <span data-ttu-id="4809f-159">次の図は、複数ステップの承認フローと、さまざまなユーザーのビューの表示方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="4809f-159">The following image shows a multi-step approval flow and how the views for different users is shown.</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views.png" alt-text="最新のユーザー固有のビュー":::

<span data-ttu-id="4809f-161">詳細については、「最新のビュー [のサンプル」を参照してください](Up-To-Date-Views.md)。</span><span class="sxs-lookup"><span data-stu-id="4809f-161">For more information, see [sample for up to date views](Up-To-Date-Views.md).</span></span>

<span data-ttu-id="4809f-162">これで、アダプティブ カードを新しいユニバーサル アクション モデルで変換して、独自の強化されたユーザー エクスペリエンスを提供する方法を理解できます。</span><span class="sxs-lookup"><span data-stu-id="4809f-162">Now, you can understand how Adaptive Cards can be transformed with the new Universal Actions model to provide a unique and enhanced user experience.</span></span>

## <a name="adaptive-cards-and-the-new-universal-actions-model"></a><span data-ttu-id="4809f-163">アダプティブ カードと新しいユニバーサル アクション モデル</span><span class="sxs-lookup"><span data-stu-id="4809f-163">Adaptive Cards and the new Universal Actions model</span></span>

<span data-ttu-id="4809f-164">アダプティブ カードは、テキストやグラフィックスなどのコンテンツと、ユーザーが実行できるアクションの組み合わせです。</span><span class="sxs-lookup"><span data-stu-id="4809f-164">Adaptive Cards are a combination of content, such as text and graphics, and actions that can be performed by a user.</span></span> <span data-ttu-id="4809f-165">詳細については、「アダプティブ カード」 [を参照してください](http://adaptivecards.io/)。</span><span class="sxs-lookup"><span data-stu-id="4809f-165">For more information, see [Adaptive Cards](http://adaptivecards.io/).</span></span> <span data-ttu-id="4809f-166">アダプティブ カード用の新しいユニバーサル アクションを使用すると、プラットフォームやアプリケーション間でアダプティブ カードアクションを一般的に処理できます。</span><span class="sxs-lookup"><span data-stu-id="4809f-166">The new Universal Actions for Adaptive Cards enables a common handling of the Adaptive Card actions across platforms and applications.</span></span> <span data-ttu-id="4809f-167">詳細については、「ユニバーサル アクション [モデル」を参照してください](/adaptive-cards/authoring-cards/universal-action-model)。</span><span class="sxs-lookup"><span data-stu-id="4809f-167">For more information, see [Universal Action Model](/adaptive-cards/authoring-cards/universal-action-model).</span></span>

<span data-ttu-id="4809f-168">まず、クイック スタート ガイドを使用してシナリオを更新し [、ユニバーサル](Work-with-universal-actions-for-adaptive-cards.md) アクションを活用します。</span><span class="sxs-lookup"><span data-stu-id="4809f-168">You can get started by updating scenarios using the [quick start guide](Work-with-universal-actions-for-adaptive-cards.md) and leverage Universal Actions.</span></span>

## <a name="see-also"></a><span data-ttu-id="4809f-169">関連項目</span><span class="sxs-lookup"><span data-stu-id="4809f-169">See also</span></span>

* [<span data-ttu-id="4809f-170">ボットについて</span><span class="sxs-lookup"><span data-stu-id="4809f-170">What are bots</span></span>](~/bots/what-are-bots.md)
* [<span data-ttu-id="4809f-171">アダプティブ カードの概要</span><span class="sxs-lookup"><span data-stu-id="4809f-171">Adaptive Cards overview</span></span>](~/task-modules-and-cards/what-are-cards.md)
* [<span data-ttu-id="4809f-172">アダプティブ カード @ Microsoft ビルド 2020</span><span class="sxs-lookup"><span data-stu-id="4809f-172">Adaptive Cards @ Microsoft Build 2020</span></span>](https://youtu.be/hEBhwB72Qn4?t=1393)
* [<span data-ttu-id="4809f-173">アダプティブ カード @ Ignite 2020</span><span class="sxs-lookup"><span data-stu-id="4809f-173">Adaptive Cards @ Ignite 2020</span></span>](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)

## <a name="next-step"></a><span data-ttu-id="4809f-174">次の手順</span><span class="sxs-lookup"><span data-stu-id="4809f-174">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4809f-175">アダプティブ カードのユニバーサル アクションの操作</span><span class="sxs-lookup"><span data-stu-id="4809f-175">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
