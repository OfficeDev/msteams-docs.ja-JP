---
title: アダプティブ カードのユニバーサル アクションの操作
description: アダプティブ カードのユニバーサル アクション (アダプティブ カードの UniversalActions のスキーマ、モデルの更新、下位互換性など) を操作する方法について説明します
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: d723b565cadfacc550cd4fd9c8648149e9d164e2
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833010"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>アダプティブ カードのユニバーサル アクションの操作

Universal Actions for Adaptive Cards provide a way to implement Adaptive Card based scenarios for both, Teams and Outlook. This document covers the following topics:

* [アダプティブ カードのユニバーサル アクションを使用したスキーマ](#schema-for-universal-actions-for-adaptive-cards)
* [モデルのリフレッシュ](#refresh-model)
* [`adaptiveCard/action` 起動アクティビティ](#adaptivecardaction-invoke-activity)
* [下位互換機能](#backward-compatibility)

## <a name="quick-start-guide-to-use-universal-actions-for-adaptive-cards-in-teams"></a>アダプティブ カードのユニバーサル アクションを Teams で活用するためのクイック スタート ガイド

1. `Action.Submit` のすべてのインスタンスを `Action.Execute` に置き換えて、Teams の既存のシナリオを更新します。
2. 自動更新モデルを活用したい場合や、シナリオにユーザー固有のビューが必要な場合は、アダプティブ カードに `refresh` 句を追加します。

    >[!NOTE]
    > 自動更新を `userIds` 取得するユーザーを識別するプロパティを指定します。

3. ボットの中で `adaptiveCard/action` の起動要求を処理します。
4. 起動要求のコンテキストを利用して、ユーザー向けに作成されたカードを返信します。

    > [!NOTE]
    > ボットが `Action.Execute` を処理した結果、新しいカードを返す場合はいつでも、その応答は応答の形式に準拠している必要があります。

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>アダプティブ カードのユニバーサル アクション向けスキーマ

アダプティブ カードのユニバーサル アクションは、アダプティブ カード スキーマ バージョン 1.4 で導入されました。 アダプティブ カードを効果的に使用するには、アダプティブ カードの `version` プロパティが 1.4 に設定されている必要があります。

> [!NOTE]
> `version` プロパティを 1.4 に設定すると、Outlook や Teams などのプラットフォームやアプリケーションの以前のバージョンのクライアントは、アダプティブ カードのユニバーサル アクションをサポートしていないため、アダプティブ カードとの互換性がありません。

カードのバージョンを 1.4 未満に設定し、`refresh` プロパティと `Action.Execute` のいずれかまたは両方を使用した場合は、以下のようになります。

| クライアント | 動作 |
| :-- | :-- |
| Teams | カードが作動しなくなります。 カードは更新されず、 `Action.Execute` Teams クライアントのバージョンによってはレンダリングされません。 Teams で最大限の互換性を確保するために、フォールバック プロパティに `Action.Submit` を含む `Action.Execute` を定義します。 |

以前のバージョンのクライアントをサポートする方法の詳細については、「[下位換機能](#backward-compatibility)」を参照してください。

### <a name="actionexecute"></a>Action.Execute

アダプティブ カードの作成では、`Action.Submit` と `Action.Http` を `Action.Execute` に置き換えます。 `Action.Execute` のスキーマは `Action.Submit` のスキーマと類似しています。

詳細については、「[Action.Execute のスキーマとプロパティ](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)」を参照してください。

モデルのリフレッシュを使用して、アダプティブ カードが自動的に更新されるようになりました。

## <a name="refresh-model"></a>モデルのリフレッシュ

アダプティブ カードを自動的に更新するには、`refresh` プロパティを定義し、タイプ `Action.Execute` のアクションと `userIds` 配列を埋め込みます。

詳細については、「[スキーマとプロパティの更新](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism)」を参照してください。

## <a name="user-ids-in-refresh"></a>リフレッシュでのユーザー ID

リフレッシュでの UserIds の機能は以下のとおりです。

* UserIds は、アダプティブ カードの `refresh` プロパティの一部であるユーザー MRI の配列です。

* list プロパティがカードの `userIds` 更新セクションのように `userIds: []` 指定されている場合、カードは自動的に更新されません。 代わりに、Teams Web クライアントまたはデスクトップのトリプル ドット メニューと、Teams モバイルの長押しコンテキスト メニュー (Android または iOS) でカードを手動で更新するための [カードの更新 **] オプションが** ユーザーに表示されます。 または、シナリオが Teams グループ チャットまたはチャネルで<=60 人のメンバーを含む場合に備えて、refresh プロパティを完全にスキップ `userIds` することもできます。 Teams クライアントは、グループまたはチャネルに <=60 ユーザーがある場合、すべてのユーザーに対して更新呼び出しを自動的に呼び出します。

* UserIds プロパティが追加されたのは、Teams チャネルには多数のメンバーが含まれる場合があるためです。 すべてのメンバーが同時にチャネルを視聴している場合、無条件に自動更新を行うと、ボットへの同時呼び出しが多くなります。 `userIds` プロパティを常に含める必要があり、最大 *60 人のユーザー MRI* で自動更新を行うべきユーザーを特定する必要があります。

* You can fetch Teams conversation member's user MRIs. For more information on how to add in userIds list in refresh section of Adaptive Card, see [fetch roster or user profile](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).

 次の例を使用して、チャネル、グループ チャット、または 1:1 チャットのユーザーの MRI を取得できます。

 1. TurnContext の使用  

     `userMRI= turnContext.Activity.From.Id`

 1. GetMemberAsync メソッドの使用
  
     `var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);var userMRI = member.Id;`

* サンプルの Teams ユーザー MRI は `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk` です

> [!NOTE]
> Outlook では `userIds` プロパティは無視され、`refresh` プロパティは常に自動的に有効化されます。 Outlook では、ユーザーがカードを表示する時間が異なるため、規模の問題はありません。

次の手順では、`adaptiveCard/action` の起動アクティビティを使用して、`Action.Execute` が実行された後にどのような要求を行う必要があるか把握します。

## <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` 起動アクティビティ

クライアントで `Action.Execute` が実行されると、新しい種類の起動アクティビティ `adaptiveCard/action` がボットに作成されます。

詳細については、「[一般的な `adaptiveCard/action` 起動アクティビティの要求形式とプロパティ](/adaptive-cards/authoring-cards/universal-action-model#request-format)」を参照してください。

詳細については、「[サポートされた応答の種類を使用した一般的な `adaptiveCard/action` 起動アクティビティの応答形式とプロパティ](/adaptive-cards/authoring-cards/universal-action-model#response-format)」を参照してください。

次に、異なるプラットフォームの以前のバージョンのクライアントに下位互換機能を適用し、アダプティブ カードの互換性を持たせることができます。

## <a name="backward-compatibility"></a>下位互換機能

アダプティブ カードのユニバーサル アクションでは、以前のバージョンの Outlook や Teams との下位互換機能を実現するためのプロパティを設定することができます。

### <a name="teams"></a>Teams

To ensure backward compatibility of your Adaptive Cards with older versions of Teams, you must include the `fallback` property and set its value to `Action.Submit`. Also, your bot code must process both `Action.Execute` and `Action.Submit`.

詳細については、「[Teams での下位互換機能](/adaptive-cards/authoring-cards/universal-action-model#teams)」を参照してください。

## <a name="code-samples"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Teams ケータリング ボット | アダプティブ カードを使用して、料理の注文を受け付けるボットを作成します。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| 該当なし |
| シーケンシャル ワークフロー アダプティブ カード | シーケンシャル ワークフロー、ユーザー固有のビュー、最新のアダプティブ カードをボットに実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>関連項目

* [Teams でのアダプティブ カードのアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [ボットの機能](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [シーケンシャル ワークフロー](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/sequential-workflows.md)
* [最新のカード](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/up-to-date-views.md)
* [フォームの完了に関するフィードバック](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
