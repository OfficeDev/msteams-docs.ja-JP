---
title: アダプティブ カードのユニバーサル アクションの操作
description: アダプティブ カードのユニバーサル アクションを操作します。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 4361f1c7774837b728c6382df4e62e00ea912e35
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649700"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a><span data-ttu-id="a997b-103">アダプティブ カードのユニバーサル アクションの操作</span><span class="sxs-lookup"><span data-stu-id="a997b-103">Work with Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="a997b-104">アダプティブ カードのユニバーサル アクションは、Teams と Outlook の両方にアダプティブ カード ベースのシナリオを実装する方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="a997b-104">Universal Actions for Adaptive Cards provides a way to implement Adaptive Card based scenarios for both, Teams and Outlook.</span></span> <span data-ttu-id="a997b-105">このドキュメントでは、次の手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="a997b-105">This document covers the following:</span></span>

* [<span data-ttu-id="a997b-106">アダプティブ カードのユニバーサル アクションを使用したスキーマ</span><span class="sxs-lookup"><span data-stu-id="a997b-106">Schema used for Universal Actions for Adaptive Cards</span></span>](#schema-for-universal-actions-for-adaptive-cards)
* [<span data-ttu-id="a997b-107">モデルのリフレッシュ</span><span class="sxs-lookup"><span data-stu-id="a997b-107">Refresh model</span></span>](#refresh-model)
* [<span data-ttu-id="a997b-108">`adaptiveCard/action` 起動アクティビティ</span><span class="sxs-lookup"><span data-stu-id="a997b-108">`adaptiveCard/action` invoke activity</span></span>](#adaptivecardaction-invoke-activity)
* [<span data-ttu-id="a997b-109">下位互換機能</span><span class="sxs-lookup"><span data-stu-id="a997b-109">Backward compatibility</span></span>](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a><span data-ttu-id="a997b-110">アダプティブ カードのユニバーサル アクションを Teams で活用するためのクイック スタート ガイド</span><span class="sxs-lookup"><span data-stu-id="a997b-110">Quick start guide to leverage Universal Actions for Adaptive Cards in Teams</span></span>

1. <span data-ttu-id="a997b-111">`Action.Submit` のすべてのインスタンスを `Action.Execute` に置き換えて、Teams の既存のシナリオを更新します。</span><span class="sxs-lookup"><span data-stu-id="a997b-111">Replace all instances of `Action.Submit` with `Action.Execute` to update an existing scenario on Teams.</span></span>
2. <span data-ttu-id="a997b-112">自動更新モデルを活用したい場合や、シナリオにユーザー固有のビューが必要な場合は、アダプティブ カードに `refresh` 句を追加します。</span><span class="sxs-lookup"><span data-stu-id="a997b-112">Add a `refresh` clause to your Adaptive Card, if you want to leverage the automatic refresh model or if your scenario requires User Specific Views.</span></span>

    >[!NOTE]
    > <span data-ttu-id="a997b-113">`userIds` プロパティを指定して、どのユーザーが自動更新を取得するかを特定します。</span><span class="sxs-lookup"><span data-stu-id="a997b-113">Specify the `userIds` property to identify, which users get automatic updates.</span></span>

3. <span data-ttu-id="a997b-114">ボットの中で `adaptiveCard/action` の起動要求を処理します。</span><span class="sxs-lookup"><span data-stu-id="a997b-114">Handle `adaptiveCard/action` invoke requests in your bot.</span></span>
4. <span data-ttu-id="a997b-115">起動要求のコンテキストを利用して、ユーザー向けに特別に作成されたカードを返信します。</span><span class="sxs-lookup"><span data-stu-id="a997b-115">Use the invoke request's context to respond back with cards that are specifically created for a user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a997b-116">ボットが `Action.Execute` を処理した結果、新しいカードを返す場合はいつでも、その応答は応答の形式に準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="a997b-116">Whenever your bot returns a new card as a result of processing an `Action.Execute`, the response must conform to the response format.</span></span>

## <a name="schema-for-universal-actions-for-adaptive-cards"></a><span data-ttu-id="a997b-117">アダプティブ カードのユニバーサル アクション向けスキーマ</span><span class="sxs-lookup"><span data-stu-id="a997b-117">Schema for Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="a997b-118">アダプティブ カードのユニバーサル アクションは、アダプティブ カード スキーマ バージョン 1.4 で導入されました。</span><span class="sxs-lookup"><span data-stu-id="a997b-118">Universal Actions for Adaptive Cards is introduced in the Adaptive Cards schema version 1.4.</span></span> <span data-ttu-id="a997b-119">アダプティブ カードを効果的に使用するには、アダプティブ カードの `version` プロパティが 1.4 に設定されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="a997b-119">To use Adaptive Card effectively, the `version` property of your Adaptive Card must be set to 1.4.</span></span>

> [!NOTE]
> <span data-ttu-id="a997b-120">`version` プロパティを 1.4 に設定すると、Outlook や Teams などのプラットフォームやアプリケーションの以前のバージョンのクライアントは、アダプティブ カードのユニバーサル アクションをサポートしていないため、アダプティブ カードとの互換性がありません。</span><span class="sxs-lookup"><span data-stu-id="a997b-120">Setting the `version` property to 1.4 makes your Adaptive Card incompatible with older clients of the platforms or applications, such as Outlook and Teams, as they do not support the Universal Actions for Adaptive Cards.</span></span>

<span data-ttu-id="a997b-121">カードのバージョンを 1.4 未満に設定し、`refresh` プロパティと `Action.Execute` のいずれかまたは両方を使用した場合は、以下のようになります。</span><span class="sxs-lookup"><span data-stu-id="a997b-121">If you set the card version to less than 1.4 and use either or both, `refresh` property and `Action.Execute`, the following happens:</span></span>

| <span data-ttu-id="a997b-122">クライアント</span><span class="sxs-lookup"><span data-stu-id="a997b-122">Client</span></span> | <span data-ttu-id="a997b-123">動作</span><span class="sxs-lookup"><span data-stu-id="a997b-123">Behavior</span></span> |
| :-- | :-- |
| <span data-ttu-id="a997b-124">Teams</span><span class="sxs-lookup"><span data-stu-id="a997b-124">Teams</span></span> | <span data-ttu-id="a997b-125">カードが作動しなくなります。</span><span class="sxs-lookup"><span data-stu-id="a997b-125">Your card stops working.</span></span> <span data-ttu-id="a997b-126">Teams クライアントのバージョンによっては、カードが更新されず、`Action.Execute` がレンダリングされない場合があります。</span><span class="sxs-lookup"><span data-stu-id="a997b-126">Card is not refreshed and `Action.Execute` does not render depending on the version of the Teams client.</span></span> <span data-ttu-id="a997b-127">Teams で最大限の互換性を確保するために、フォールバック プロパティに `Action.Submit` を含む `Action.Execute` を定義します。</span><span class="sxs-lookup"><span data-stu-id="a997b-127">To ensure maximum compatibility in Teams, define `Action.Execute` with an `Action.Submit` in the fallback property.</span></span> |

<span data-ttu-id="a997b-128">以前のバージョンのクライアントをサポートする方法の詳細については、「[下位換機能](#backward-compatibility)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a997b-128">For more information on how to support older clients, see [backward compatibility](#backward-compatibility).</span></span>

### <a name="actionexecute"></a><span data-ttu-id="a997b-129">Action.Execute</span><span class="sxs-lookup"><span data-stu-id="a997b-129">Action.Execute</span></span>

<span data-ttu-id="a997b-130">アダプティブ カードの作成では、`Action.Submit` と `Action.Http` を `Action.Execute` に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a997b-130">When authoring Adaptive Cards, replace `Action.Submit` and `Action.Http` with `Action.Execute`.</span></span> <span data-ttu-id="a997b-131">`Action.Execute` のスキーマは `Action.Submit` のスキーマと類似しています。</span><span class="sxs-lookup"><span data-stu-id="a997b-131">The schema for `Action.Execute` is similar to that of `Action.Submit`.</span></span>

<span data-ttu-id="a997b-132">詳細については、「[Action.Execute のスキーマとプロパティ](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a997b-132">For more information, see [Action.Execute schema and properties](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

<span data-ttu-id="a997b-133">モデルのリフレッシュを使用して、アダプティブ カードが自動的に更新されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="a997b-133">Now, you can use the refresh model to allow Adaptive Cards to update automatically.</span></span>

## <a name="refresh-model"></a><span data-ttu-id="a997b-134">モデルのリフレッシュ</span><span class="sxs-lookup"><span data-stu-id="a997b-134">Refresh model</span></span>

<span data-ttu-id="a997b-135">アダプティブ カードを自動的に更新するには、`refresh` プロパティを定義し、タイプ `Action.Execute` のアクションと `userIds` 配列を埋め込みます。</span><span class="sxs-lookup"><span data-stu-id="a997b-135">To automatically refresh your Adaptive Card, define its `refresh` property, which embeds an action of type `Action.Execute` and an `userIds` array.</span></span>

<span data-ttu-id="a997b-136">詳細については、「[スキーマとプロパティの更新](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a997b-136">For more information, see [refresh schema and properties](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).</span></span>

## <a name="user-ids-in-refresh"></a><span data-ttu-id="a997b-137">リフレッシュでのユーザー ID</span><span class="sxs-lookup"><span data-stu-id="a997b-137">User IDs in refresh</span></span>

<span data-ttu-id="a997b-138">リフレッシュでの UserIds の機能は以下のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a997b-138">The following are the features of UserIds in refresh:</span></span>

* <span data-ttu-id="a997b-139">UserIds は、アダプティブ カードの `refresh` プロパティの一部であるユーザー MRI の配列です。</span><span class="sxs-lookup"><span data-stu-id="a997b-139">UserIds is an array of user MRI's which is part of the `refresh` property in Adaptive Cards.</span></span>

* <span data-ttu-id="a997b-140">カードの更新セクションで `userIds` リスト プロパティを `userIds: []` として指定した場合、カードは自動的に更新されません。</span><span class="sxs-lookup"><span data-stu-id="a997b-140">If the `userIds` list property is specified as `userIds: []` in the refresh section of the card, the card is not automatically refreshed.</span></span> <span data-ttu-id="a997b-141">代わりに、Web やデスクトップではトリプル ドット メニューに、モバイル (Android や iOS) では長押しコンテキスト メニューに、カードを手動で更新するための **[カードの更新]** オプションがユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="a997b-141">Instead, a **Refresh Card** option is displayed to the user in the triple dot menu in web or desktop and in the long press context menu in mobile, that is, Android or iOS to manually refresh the card.</span></span>

* <span data-ttu-id="a997b-142">UserIds プロパティが追加されたのは、Teams チャネルには多数のメンバーが含まれる場合があるためです。</span><span class="sxs-lookup"><span data-stu-id="a997b-142">UserIds property is added because channels in Teams can include a large number of members.</span></span> <span data-ttu-id="a997b-143">すべてのメンバーが同時にチャネルを視聴している場合、無条件に自動更新を行うと、ボットへの同時呼び出しが多くなります。</span><span class="sxs-lookup"><span data-stu-id="a997b-143">If all members are viewing the channel at the same time, an unconditional automatic refresh results in many concurrent calls to the bot.</span></span> <span data-ttu-id="a997b-144">これを防止するには、`userIds` プロパティを常に含める必要があり、最大 *60 人のユーザー MRI* で自動更新を行うべきユーザーを特定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a997b-144">To avoid this, the `userIds` property must always be included to identify which users must get an automatic refresh with a maximum of *60 (sixty) user MRIs*.</span></span>

* <span data-ttu-id="a997b-145">アダプティブ カードの更新セクションの userIds リストに追加する Teams 会話メンバーのユーザー MRI を取得する方法については、「[参加者一覧またはユーザー プロファイルを取得する](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a997b-145">For more information on how you can fetch Teams conversation member's user MRIs to add in userIds list in refresh section of Adaptive Card, see [fetch roster or user profile](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).</span></span>

* <span data-ttu-id="a997b-146">サンプルの Teams ユーザー MRI は `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk` です</span><span class="sxs-lookup"><span data-stu-id="a997b-146">Sample Teams user MRI is `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span></span>

> [!NOTE]
> <span data-ttu-id="a997b-147">Outlook では `userIds` プロパティは無視され、`refresh` プロパティは常に自動的に有効化されます。</span><span class="sxs-lookup"><span data-stu-id="a997b-147">The `userIds` property is ignored in Outlook, and the `refresh` property is always automatically activated.</span></span> <span data-ttu-id="a997b-148">Outlook では、ユーザーがカードを表示する時間が異なるため、規模の問題はありません。</span><span class="sxs-lookup"><span data-stu-id="a997b-148">There is no scale issue in Outlook because users view the card at different times.</span></span>

<span data-ttu-id="a997b-149">次の手順では、`adaptiveCard/action` の起動アクティビティを使用して、`Action.Execute` が実行された後にどのような要求を行う必要があるか把握します。</span><span class="sxs-lookup"><span data-stu-id="a997b-149">Next step is to use the `adaptiveCard/action` invoke activity to understand what request must be made after `Action.Execute` is executed.</span></span>

## <a name="adaptivecardaction-invoke-activity"></a><span data-ttu-id="a997b-150">`adaptiveCard/action` 起動アクティビティ</span><span class="sxs-lookup"><span data-stu-id="a997b-150">`adaptiveCard/action` invoke activity</span></span>

<span data-ttu-id="a997b-151">クライアントで `Action.Execute` が実行されると、新しい種類の起動アクティビティ `adaptiveCard/action` がボットに作成されます。</span><span class="sxs-lookup"><span data-stu-id="a997b-151">When `Action.Execute` is executed in the client, a new type of Invoke activity `adaptiveCard/action` is made to your bot.</span></span>

<span data-ttu-id="a997b-152">詳細については、「[一般的な `adaptiveCard/action` 起動アクティビティの要求形式とプロパティ](/adaptive-cards/authoring-cards/universal-action-model#request-format)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a997b-152">For more information, see [request format and properties for a typical `adaptiveCard/action` invoke activity](/adaptive-cards/authoring-cards/universal-action-model#request-format).</span></span>

<span data-ttu-id="a997b-153">詳細については、「[サポートされた応答の種類を使用した一般的な `adaptiveCard/action` 起動アクティビティの応答形式とプロパティ](/adaptive-cards/authoring-cards/universal-action-model#response-format)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a997b-153">For more information, see [response format and properties for a typical `adaptiveCard/action` invoke activity with supported response types](/adaptive-cards/authoring-cards/universal-action-model#response-format).</span></span>

<span data-ttu-id="a997b-154">次に、異なるプラットフォームの以前のバージョンのクライアントに下位互換機能を適用し、アダプティブ カードの互換性を持たせることができます。</span><span class="sxs-lookup"><span data-stu-id="a997b-154">Next, you can apply backward compatibility to older clients across different platforms and make your Adaptive Card compatible.</span></span>

## <a name="backward-compatibility"></a><span data-ttu-id="a997b-155">下位互換機能</span><span class="sxs-lookup"><span data-stu-id="a997b-155">Backward compatibility</span></span>

<span data-ttu-id="a997b-156">アダプティブ カードのユニバーサル アクションでは、以前のバージョンの Outlook や Teams との下位互換機能を実現するためのプロパティを設定することができます。</span><span class="sxs-lookup"><span data-stu-id="a997b-156">Universal Actions for Adaptive Cards allows you to set properties that enable backward compatibility with older versions of Outlook and Teams.</span></span>

### <a name="teams"></a><span data-ttu-id="a997b-157">Teams</span><span class="sxs-lookup"><span data-stu-id="a997b-157">Teams</span></span>

<span data-ttu-id="a997b-158">アダプティブ カードの以前のバージョンの Teams との下位互換機能を確保するためには、`fallback` プロパティを含め、その値を `Action.Submit` に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a997b-158">To ensure backward compatibility of your Adaptive Cards with older versions of Teams, you must include the `fallback` property and set its value to `Action.Submit`.</span></span> <span data-ttu-id="a997b-159">また、ボット コードは、`Action.Execute` と `Action.Submit` の両方を処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a997b-159">Also, your bot code must process both `Action.Execute` and `Action.Submit`.</span></span>

<span data-ttu-id="a997b-160">詳細については、「[Teams での下位互換機能](/adaptive-cards/authoring-cards/universal-action-model#teams)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a997b-160">For more information, see [backward compatibility on Teams](/adaptive-cards/authoring-cards/universal-action-model#teams).</span></span>

## <a name="code-sample"></a><span data-ttu-id="a997b-161">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="a997b-161">Code sample</span></span>

|<span data-ttu-id="a997b-162">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="a997b-162">Sample name</span></span> | <span data-ttu-id="a997b-163">説明</span><span class="sxs-lookup"><span data-stu-id="a997b-163">Description</span></span> | <span data-ttu-id="a997b-164">.NETCore</span><span class="sxs-lookup"><span data-stu-id="a997b-164">.NETCore</span></span> |
|----------------|-----------------|--------------|
| <span data-ttu-id="a997b-165">Teams ケータリング ボット</span><span class="sxs-lookup"><span data-stu-id="a997b-165">Teams catering bot</span></span> | <span data-ttu-id="a997b-166">アダプティブ カードを使用して、料理の注文を受け付けるシンプルなボットを作成します。</span><span class="sxs-lookup"><span data-stu-id="a997b-166">Create a simple bot that accepts food order using Adaptive Cards.</span></span> |[<span data-ttu-id="a997b-167">表示</span><span class="sxs-lookup"><span data-stu-id="a997b-167">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)|

## <a name="see-also"></a><span data-ttu-id="a997b-168">関連項目</span><span class="sxs-lookup"><span data-stu-id="a997b-168">See also</span></span>

* [<span data-ttu-id="a997b-169">Teams でのアダプティブ カードのアクション</span><span class="sxs-lookup"><span data-stu-id="a997b-169">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="a997b-170">ボットの機能</span><span class="sxs-lookup"><span data-stu-id="a997b-170">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
