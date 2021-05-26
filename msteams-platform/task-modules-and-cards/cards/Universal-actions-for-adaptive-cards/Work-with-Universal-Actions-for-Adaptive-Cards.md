---
title: アダプティブ カードのユニバーサル アクションの操作
description: アダプティブ カードのユニバーサル アクションを操作します。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 4361f1c7774837b728c6382df4e62e00ea912e35
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649700"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>アダプティブ カードのユニバーサル アクションの操作

アダプティブ カードのユニバーサル アクションは、アダプティブ カード ベースのシナリオを、アダプティブ カードとアダプティブ カードの両方Teams実装Outlook。 このドキュメントでは、次の内容について説明します。

* [アダプティブ カードのユニバーサル アクションに使用されるスキーマ](#schema-for-universal-actions-for-adaptive-cards)
* [モデルの更新](#refresh-model)
* [`adaptiveCard/action` アクティビティの呼び出し](#adaptivecardaction-invoke-activity)
* [下位互換機能](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a>ユニバーサル アクション for アダプティブ カードを活用するクイック スタート ガイド (Teams

1. すべてのインスタンスを置き換 `Action.Submit` え `Action.Execute` 、既存のシナリオを更新Teams。
2. 自動更新モデルを利用する場合、またはシナリオでユーザー固有のビューが必要な場合は、アダプティブ カードに句 `refresh` を追加します。

    >[!NOTE]
    > 識別する `userIds` プロパティ、自動更新を取得するユーザーを指定します。

3. ボット `adaptiveCard/action` で呼び出し要求を処理します。
4. 呼び出し要求のコンテキストを使用して、ユーザー用に特別に作成されたカードで応答します。

    > [!NOTE]
    > ボットが処理の結果として新しいカードを返すたびに、応答 `Action.Execute` は応答形式に準拠している必要があります。

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>アダプティブ カードのユニバーサル アクションのスキーマ

アダプティブ カードのユニバーサル アクションは、アダプティブ カード スキーマ バージョン 1.4 で導入されています。 アダプティブ カードを効果的に使用するには、アダプティブ カードのプロパティを `version` 1.4 に設定する必要があります。

> [!NOTE]
> プロパティを 1.4 に設定すると、アダプティブ カードはアダプティブ カードのユニバーサル アクションをサポートしていないので、Outlook や Teams などのプラットフォームやアプリケーションの古いクライアントと互換性がありません。 `version`

カードのバージョンを 1.4 未満に設定し、プロパティとプロパティのどちらかまたは両方を使用すると、次 `refresh` `Action.Execute` のことが発生します。

| クライアント | 動作 |
| :-- | :-- |
| Teams | カードの動作が停止します。 カードは更新されないので `Action.Execute` 、クライアントのバージョンによってはレンダリングTeamsされません。 アプリケーションの互換性を最大限に高Teams、フォールバック `Action.Execute` プロパティで `Action.Submit` 定義します。 |

古いクライアントをサポートする方法の詳細については、「下位互換性 [」を参照してください](#backward-compatibility)。

### <a name="actionexecute"></a>Action.Exeかわいい

アダプティブ カードを作成する場合は、 に置 `Action.Submit` き換 `Action.Http` え、 に置き換える `Action.Execute` 必要があります。 のスキーマ `Action.Execute` は、 のスキーマと似ています `Action.Submit` 。

詳細については、「かわいいスキーマ [ とAction.Exeを参照してください](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。

これで、更新モデルを使用してアダプティブ カードを自動的に更新できます。

## <a name="refresh-model"></a>モデルの更新

アダプティブ カードを自動的に更新するには、型と配列のアクションを埋め込 `refresh` むプロパティ `Action.Execute` を定義 `userIds` します。

詳細については、「スキーマと [プロパティの更新」を参照してください](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism)。

## <a name="user-ids-in-refresh"></a>更新中のユーザー ID

更新時の UserId の機能を次に示します。

* UserIds は、アダプティブ カードのプロパティの一部であるユーザーの MRI `refresh` の配列です。

* list プロパティがカードの更新セクションのように指定されている場合、カード `userIds` `userIds: []` は自動的に更新されません。 代わりに、Webまたはデスクトップのトリプル ドット メニューおよびモバイルの長押しコンテキスト メニュー (Android または iOS で手動でカードを更新する) で、ユーザーに [カードの更新] オプションが表示されます。

* UserIds プロパティが追加される理由は、Teamsのチャネルに多数のメンバーが含まれる可能性があるためです。 すべてのメンバーが同時にチャネルを表示している場合、無条件の自動更新により、ボットへの同時呼び出しが多数発生します。 これを回避するには、プロパティを常に含め、最大 `userIds` *60 (60)* のユーザー MRIs で自動更新を取得する必要があるユーザーを識別する必要があります。

* アダプティブ カードの更新セクションの userId リストに追加する Teams 会話メンバーのユーザー MRIs をフェッチする方法の詳細については、「fetch roster or user [profile」を参照してください](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)。

* ユーザーのTEAMSのサンプルは、`29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`

> [!NOTE]
> この `userIds` プロパティは、Outlookで無視され、 `refresh` プロパティは常に自動的にアクティブ化されます。 ユーザーが異なる時間にカードOutlookにスケールの問題はありません。

次の手順では、呼び出し `adaptiveCard/action` アクティビティを使用して、実行後に行う必要がある要求 `Action.Execute` を理解します。

## <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` アクティビティの呼び出し

クライアント `Action.Execute` で実行されると、ボットに対して新しい種類の Invoke アクティビティ `adaptiveCard/action` が作成されます。

詳細については、「一般的な呼 [び出しアクティビティの要求の形式とプロパティ」 `adaptiveCard/action` を参照してください](/adaptive-cards/authoring-cards/universal-action-model#request-format)。

詳細については、「サポートされている応答の種類を持つ一般的な呼び出しアクティビティの [ `adaptiveCard/action` 応答の形式とプロパティ」を参照してください](/adaptive-cards/authoring-cards/universal-action-model#response-format)。

次に、異なるプラットフォーム間で古いクライアントに下位互換性を適用し、アダプティブ カードを互換性のあるものにできます。

## <a name="backward-compatibility"></a>下位互換機能

アダプティブ カードのユニバーサル アクションを使用すると、以前のバージョンと下位互換性を有効にするプロパティをOutlookおよびTeams。

### <a name="teams"></a>Teams

アダプティブ カードと以前のバージョンの Teamsとの下位互換性を確保するには、プロパティを含め、その値を `fallback` に設定する必要があります `Action.Submit` 。 また、ボット コードは、 と の両方を処理する `Action.Execute` 必要があります `Action.Submit` 。

詳細については、「下位互換性[」を参照Teams。](/adaptive-cards/authoring-cards/universal-action-model#teams)

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore |
|----------------|-----------------|--------------|
| Teamsボット | アダプティブ カードを使用して食品の注文を受け入れる簡単なボットを作成します。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)|

## <a name="see-also"></a>関連項目

* [アダプティブ カードのアクション (Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [ボットの機能](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
