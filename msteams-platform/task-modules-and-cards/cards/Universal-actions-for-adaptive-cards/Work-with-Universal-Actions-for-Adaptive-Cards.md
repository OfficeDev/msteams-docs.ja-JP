---
title: アダプティブ カードのユニバーサル アクションを操作する
description: アダプティブ カードのユニバーサル アクションを操作します。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 8c260a4893d38ad365cbb3bdd5a7613a1b42654f
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088873"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a><span data-ttu-id="642bf-103">アダプティブ カードのユニバーサル アクションを操作する</span><span class="sxs-lookup"><span data-stu-id="642bf-103">Work with Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="642bf-104">アダプティブ カードのユニバーサル アクションは、アダプティブ カード ベースのシナリオを、アダプティブ カードとアダプティブ カードの両方Teams実装Outlook。</span><span class="sxs-lookup"><span data-stu-id="642bf-104">Universal Actions for Adaptive Cards provides a way to implement Adaptive Card based scenarios for both, Teams and Outlook.</span></span> <span data-ttu-id="642bf-105">このドキュメントでは、次の内容について説明します。</span><span class="sxs-lookup"><span data-stu-id="642bf-105">This document covers the following:</span></span>

* [<span data-ttu-id="642bf-106">アダプティブ カードのユニバーサル アクションに使用されるスキーマ</span><span class="sxs-lookup"><span data-stu-id="642bf-106">Schema used for Universal Actions for Adaptive Cards</span></span>](#schema-for-universal-actions-for-adaptive-cards)
* [<span data-ttu-id="642bf-107">モデルの更新</span><span class="sxs-lookup"><span data-stu-id="642bf-107">Refresh model</span></span>](#refresh-model)
* [<span data-ttu-id="642bf-108">`adaptiveCard/action` アクティビティの呼び出し</span><span class="sxs-lookup"><span data-stu-id="642bf-108">`adaptiveCard/action` invoke activity</span></span>](#adaptivecardaction-invoke-activity)
* [<span data-ttu-id="642bf-109">下位互換機能</span><span class="sxs-lookup"><span data-stu-id="642bf-109">Backward compatibility</span></span>](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a><span data-ttu-id="642bf-110">ユニバーサル アクション for アダプティブ カードを活用するクイック スタート ガイド (Teams</span><span class="sxs-lookup"><span data-stu-id="642bf-110">Quick start guide to leverage Universal Actions for Adaptive Cards in Teams</span></span>

1. <span data-ttu-id="642bf-111">すべてのインスタンスを置き換 `Action.Submit` え `Action.Execute` 、既存のシナリオを更新Teams。</span><span class="sxs-lookup"><span data-stu-id="642bf-111">Replace all instances of `Action.Submit` with `Action.Execute` to update an existing scenario on Teams.</span></span>
2. <span data-ttu-id="642bf-112">自動更新モデルを利用する場合、またはシナリオでユーザー固有のビューが必要な場合は、アダプティブ カードに句 `refresh` を追加します。</span><span class="sxs-lookup"><span data-stu-id="642bf-112">Add a `refresh` clause to your Adaptive Card, if you want to leverage the automatic refresh model or if your scenario requires User Specific Views.</span></span>

    >[!NOTE]
    > <span data-ttu-id="642bf-113">識別する `userIds` プロパティ、自動更新を取得するユーザーを指定します。</span><span class="sxs-lookup"><span data-stu-id="642bf-113">Specify the `userIds` property to identify, which users get automatic updates.</span></span>

3. <span data-ttu-id="642bf-114">ボット `adaptiveCard/action` で呼び出し要求を処理します。</span><span class="sxs-lookup"><span data-stu-id="642bf-114">Handle `adaptiveCard/action` invoke requests in your bot.</span></span>
4. <span data-ttu-id="642bf-115">呼び出し要求のコンテキストを使用して、ユーザー用に特別に作成されたカードで応答します。</span><span class="sxs-lookup"><span data-stu-id="642bf-115">Use the invoke request's context to respond back with cards that are specifically created for a user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="642bf-116">ボットが処理の結果として新しいカードを返すたびに、応答 `Action.Execute` は応答形式に準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="642bf-116">Whenever your bot returns a new card as a result of processing an `Action.Execute`, the response must conform to the response format.</span></span>

## <a name="schema-for-universal-actions-for-adaptive-cards"></a><span data-ttu-id="642bf-117">アダプティブ カードのユニバーサル アクションのスキーマ</span><span class="sxs-lookup"><span data-stu-id="642bf-117">Schema for Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="642bf-118">アダプティブ カードのユニバーサル アクションは、アダプティブ カード スキーマ バージョン 1.4 で導入されています。</span><span class="sxs-lookup"><span data-stu-id="642bf-118">Universal Actions for Adaptive Cards is introduced in the Adaptive Cards schema version 1.4.</span></span> <span data-ttu-id="642bf-119">アダプティブ カードを効果的に使用するには、アダプティブ カードのプロパティを `version` 1.4 に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642bf-119">To use Adaptive Card effectively, the `version` property of your Adaptive Card must be set to 1.4.</span></span>

> [!NOTE]
> <span data-ttu-id="642bf-120">プロパティを 1.4 に設定すると、アダプティブ カードはアダプティブ カードのユニバーサル アクションをサポートしていないので、Outlook や Teams などのプラットフォームやアプリケーションの古いクライアントと互換性がありません。 `version`</span><span class="sxs-lookup"><span data-stu-id="642bf-120">Setting the `version` property to 1.4 makes your Adaptive Card incompatible with older clients of the platforms or applications, such as Outlook and Teams, as they do not support the Universal Actions for Adaptive Cards.</span></span>

<span data-ttu-id="642bf-121">カードのバージョンを 1.4 未満に設定し、プロパティとプロパティのどちらかまたは両方を使用すると、次 `refresh` `Action.Execute` のことが発生します。</span><span class="sxs-lookup"><span data-stu-id="642bf-121">If you set the card version to less than 1.4 and use either or both, `refresh` property and `Action.Execute`, the following happens:</span></span>

| <span data-ttu-id="642bf-122">クライアント</span><span class="sxs-lookup"><span data-stu-id="642bf-122">Client</span></span> | <span data-ttu-id="642bf-123">動作</span><span class="sxs-lookup"><span data-stu-id="642bf-123">Behavior</span></span> |
| :-- | :-- |
| <span data-ttu-id="642bf-124">Teams</span><span class="sxs-lookup"><span data-stu-id="642bf-124">Teams</span></span> | <span data-ttu-id="642bf-125">カードの動作が停止します。</span><span class="sxs-lookup"><span data-stu-id="642bf-125">Your card stops working.</span></span> <span data-ttu-id="642bf-126">カードは更新されないので `Action.Execute` 、クライアントのバージョンによってはレンダリングTeamsされません。</span><span class="sxs-lookup"><span data-stu-id="642bf-126">Card is not refreshed and `Action.Execute` does not render depending on the version of the Teams client.</span></span> <span data-ttu-id="642bf-127">アプリケーションの互換性を最大限に高Teams、フォールバック `Action.Execute` プロパティで `Action.Submit` 定義します。</span><span class="sxs-lookup"><span data-stu-id="642bf-127">To ensure maximum compatibility in Teams, define `Action.Execute` with an `Action.Submit` in the fallback property.</span></span> |

<span data-ttu-id="642bf-128">古いクライアントをサポートする方法の詳細については、「下位互換性 [」を参照してください](#backward-compatibility)。</span><span class="sxs-lookup"><span data-stu-id="642bf-128">For more information on how to support older clients, see [backward compatibility](#backward-compatibility).</span></span>

### <a name="actionexecute"></a><span data-ttu-id="642bf-129">Action.Exeかわいい</span><span class="sxs-lookup"><span data-stu-id="642bf-129">Action.Execute</span></span>

<span data-ttu-id="642bf-130">アダプティブ カードを作成する場合は、 に置 `Action.Submit` き換 `Action.Http` え、 に置き換える `Action.Execute` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="642bf-130">When authoring Adaptive Cards, replace `Action.Submit` and `Action.Http` with `Action.Execute`.</span></span> <span data-ttu-id="642bf-131">のスキーマ `Action.Execute` は、 のスキーマと似ています `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="642bf-131">The schema for `Action.Execute` is similar to that of `Action.Submit`.</span></span>

<span data-ttu-id="642bf-132">詳細については、「かわいいスキーマ [ とAction.Exeを参照してください](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。</span><span class="sxs-lookup"><span data-stu-id="642bf-132">For more information, see [Action.Execute schema and properties](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

<span data-ttu-id="642bf-133">これで、更新モデルを使用してアダプティブ カードを自動的に更新できます。</span><span class="sxs-lookup"><span data-stu-id="642bf-133">Now, you can use the refresh model to allow Adaptive Cards to update automatically.</span></span>

## <a name="refresh-model"></a><span data-ttu-id="642bf-134">モデルの更新</span><span class="sxs-lookup"><span data-stu-id="642bf-134">Refresh model</span></span>

<span data-ttu-id="642bf-135">アダプティブ カードを自動的に更新するには、型と配列のアクションを埋め込 `refresh` むプロパティ `Action.Execute` を定義 `userIds` します。</span><span class="sxs-lookup"><span data-stu-id="642bf-135">To automatically refresh your Adaptive Card, define its `refresh` property, which embeds an action of type `Action.Execute` and an `userIds` array.</span></span>

<span data-ttu-id="642bf-136">詳細については、「スキーマと [プロパティの更新」を参照してください](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism)。</span><span class="sxs-lookup"><span data-stu-id="642bf-136">For more information, see [refresh schema and properties](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).</span></span>

## <a name="user-ids-in-refresh"></a><span data-ttu-id="642bf-137">更新中のユーザー ID</span><span class="sxs-lookup"><span data-stu-id="642bf-137">User IDs in refresh</span></span>

<span data-ttu-id="642bf-138">更新時の UserId の機能を次に示します。</span><span class="sxs-lookup"><span data-stu-id="642bf-138">The following are the features of UserIds in refresh:</span></span>

* <span data-ttu-id="642bf-139">UserIds は、アダプティブ カードのプロパティの一部であるユーザーの MRI `refresh` の配列です。</span><span class="sxs-lookup"><span data-stu-id="642bf-139">UserIds is an array of user MRI's which is part of the `refresh` property in Adaptive Cards.</span></span>

* <span data-ttu-id="642bf-140">list プロパティがカードの更新セクションのように指定されている場合、カード `userIds` `userIds: []` は自動的に更新されません。</span><span class="sxs-lookup"><span data-stu-id="642bf-140">If the `userIds` list property is specified as `userIds: []` in the refresh section of the card, the card is not automatically refreshed.</span></span> <span data-ttu-id="642bf-141">代わりに、Webまたはデスクトップのトリプル ドット メニューおよびモバイルの長押しコンテキスト メニュー (Android または iOS で手動でカードを更新する) で、ユーザーに [カードの更新] オプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="642bf-141">Instead, a **Refresh Card** option is displayed to the user in the triple dot menu in web or desktop and in the long press context menu in mobile, that is, Android or iOS to manually refresh the card.</span></span>

* <span data-ttu-id="642bf-142">UserIds プロパティが追加される理由は、Teamsのチャネルに多数のメンバーが含まれる可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="642bf-142">UserIds property is added because channels in Teams can include a large number of members.</span></span> <span data-ttu-id="642bf-143">すべてのメンバーが同時にチャネルを表示している場合、無条件の自動更新により、ボットへの同時呼び出しが多数発生します。</span><span class="sxs-lookup"><span data-stu-id="642bf-143">If all members are viewing the channel at the same time, an unconditional automatic refresh results in many concurrent calls to the bot.</span></span> <span data-ttu-id="642bf-144">これを回避するには、プロパティを常に含め、最大 `userIds` *60 (60)* のユーザー MRIs で自動更新を取得する必要があるユーザーを識別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642bf-144">To avoid this, the `userIds` property must always be included to identify which users must get an automatic refresh with a maximum of *60 (sixty) user MRIs*.</span></span>

* <span data-ttu-id="642bf-145">アダプティブ カードの更新セクションの userId リストに追加する Teams 会話メンバーのユーザー MRIs をフェッチする方法の詳細については、「fetch roster or user [profile」を参照してください](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)。</span><span class="sxs-lookup"><span data-stu-id="642bf-145">For more information on how you can fetch Teams conversation member's user MRIs to add in userIds list in refresh section of Adaptive Card, see [fetch roster or user profile](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).</span></span>

* <span data-ttu-id="642bf-146">ユーザーのTEAMSのサンプルは、`29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span><span class="sxs-lookup"><span data-stu-id="642bf-146">Sample Teams user MRI is `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span></span>

> [!NOTE]
> <span data-ttu-id="642bf-147">この `userIds` プロパティは、Outlookで無視され、 `refresh` プロパティは常に自動的にアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="642bf-147">The `userIds` property is ignored in Outlook, and the `refresh` property is always automatically activated.</span></span> <span data-ttu-id="642bf-148">ユーザーが異なる時間にカードOutlookにスケールの問題はありません。</span><span class="sxs-lookup"><span data-stu-id="642bf-148">There is no scale issue in Outlook because users view the card at different times.</span></span>

<span data-ttu-id="642bf-149">次の手順では、呼び出し `adaptiveCard/action` アクティビティを使用して、実行後に行う必要がある要求 `Action.Execute` を理解します。</span><span class="sxs-lookup"><span data-stu-id="642bf-149">Next step is to use the `adaptiveCard/action` invoke activity to understand what request must be made after `Action.Execute` is executed.</span></span>

## <a name="adaptivecardaction-invoke-activity"></a><span data-ttu-id="642bf-150">`adaptiveCard/action` アクティビティの呼び出し</span><span class="sxs-lookup"><span data-stu-id="642bf-150">`adaptiveCard/action` invoke activity</span></span>

<span data-ttu-id="642bf-151">クライアント `Action.Execute` で実行されると、ボットに対して新しい種類の Invoke アクティビティ `adaptiveCard/action` が作成されます。</span><span class="sxs-lookup"><span data-stu-id="642bf-151">When `Action.Execute` is executed in the client, a new type of Invoke activity `adaptiveCard/action` is made to your bot.</span></span>

<span data-ttu-id="642bf-152">詳細については、「一般的な呼 [び出しアクティビティの要求の形式とプロパティ」 `adaptiveCard/action` を参照してください](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#request-format)。</span><span class="sxs-lookup"><span data-stu-id="642bf-152">For more information, see [request format and properties for a typical `adaptiveCard/action` invoke activity](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#request-format).</span></span>

<span data-ttu-id="642bf-153">詳細については、「サポートされている応答の種類を持つ一般的な呼び出しアクティビティの [ `adaptiveCard/action` 応答の形式とプロパティ」を参照してください](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#response-format)。</span><span class="sxs-lookup"><span data-stu-id="642bf-153">For more information, see [response format and properties for a typical `adaptiveCard/action` invoke activity with supported response types](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#response-format).</span></span>

<span data-ttu-id="642bf-154">次に、異なるプラットフォーム間で古いクライアントに下位互換性を適用し、アダプティブ カードを互換性のあるものにできます。</span><span class="sxs-lookup"><span data-stu-id="642bf-154">Next, you can apply backward compatibility to older clients across different platforms and make your Adaptive Card compatible.</span></span>

## <a name="backward-compatibility"></a><span data-ttu-id="642bf-155">下位互換機能</span><span class="sxs-lookup"><span data-stu-id="642bf-155">Backward compatibility</span></span>

<span data-ttu-id="642bf-156">アダプティブ カードのユニバーサル アクションを使用すると、以前のバージョンと下位互換性を有効にするプロパティをOutlookおよびTeams。</span><span class="sxs-lookup"><span data-stu-id="642bf-156">Universal Actions for Adaptive Cards allows you to set properties that enable backward compatibility with older versions of Outlook and Teams.</span></span>

### <a name="teams"></a><span data-ttu-id="642bf-157">Teams</span><span class="sxs-lookup"><span data-stu-id="642bf-157">Teams</span></span>

<span data-ttu-id="642bf-158">アダプティブ カードと以前のバージョンの Teamsとの下位互換性を確保するには、プロパティを含め、その値を `fallback` に設定する必要があります `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="642bf-158">To ensure backward compatibility of your Adaptive Cards with older versions of Teams, you must include the `fallback` property and set its value to `Action.Submit`.</span></span> <span data-ttu-id="642bf-159">また、ボット コードは、 と の両方を処理する `Action.Execute` 必要があります `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="642bf-159">Also, your bot code must process both `Action.Execute` and `Action.Submit`.</span></span>

<span data-ttu-id="642bf-160">詳細については、「下位互換性[」を参照Teams。](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#teams)</span><span class="sxs-lookup"><span data-stu-id="642bf-160">For more information, see [backward compatibility on Teams](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#teams).</span></span>

## <a name="see-also"></a><span data-ttu-id="642bf-161">関連項目</span><span class="sxs-lookup"><span data-stu-id="642bf-161">See also</span></span>

* [<span data-ttu-id="642bf-162">アダプティブ カードのアクション (Teams</span><span class="sxs-lookup"><span data-stu-id="642bf-162">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="642bf-163">ボットの機能</span><span class="sxs-lookup"><span data-stu-id="642bf-163">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
