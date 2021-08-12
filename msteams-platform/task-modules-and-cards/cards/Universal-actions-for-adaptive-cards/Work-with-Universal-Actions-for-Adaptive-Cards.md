---
title: アダプティブ カードのユニバーサル アクションの操作
description: アダプティブ カードのユニバーサル アクションを操作します。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 0c3b07d630452abe945e43e7a9dfdced00e22f35324b2e9c7768b6bca5a0d065
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57701967"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>アダプティブ カードのユニバーサル アクションの操作

アダプティブ カードのユニバーサル アクションは、アダプティブ カード ベースのシナリオを、アダプティブ カードとアダプティブ カードの両方Teams実装Outlook。 このドキュメントでは、次のトピックについて説明します。

* [アダプティブ カードのユニバーサル アクションを使用したスキーマ](#schema-for-universal-actions-for-adaptive-cards)
* [モデルのリフレッシュ](#refresh-model)
* [`adaptiveCard/action` 起動アクティビティ](#adaptivecardaction-invoke-activity)
* [下位互換機能](#backward-compatibility)

## <a name="quick-start-guide-to-use-universal-actions-for-adaptive-cards-in-teams"></a>アダプティブ カードのユニバーサル アクションを使用するクイック スタート Teams

1. `Action.Submit` のすべてのインスタンスを `Action.Execute` に置き換えて、Teams の既存のシナリオを更新します。
2. 自動更新モデルを使用する場合、またはシナリオでユーザー固有のビューが必要な場合は、アダプティブ カードに句 `refresh` を追加します。

    >[!NOTE]
    > `userIds` プロパティを指定して、どのユーザーが自動更新を取得するかを特定します。

3. ボットの中で `adaptiveCard/action` の起動要求を処理します。
4. 呼び出し要求のコンテキストを使用して、ユーザー用に作成されたカードで応答します。

    > [!NOTE]
    > ボットが `Action.Execute` を処理した結果、新しいカードを返す場合はいつでも、その応答は応答の形式に準拠している必要があります。

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>アダプティブ カードのユニバーサル アクション向けスキーマ

アダプティブ カードのユニバーサル アクションは、アダプティブ カード スキーマ バージョン 1.4 で導入されています。 アダプティブ カードを効果的に使用するには、アダプティブ カードの `version` プロパティが 1.4 に設定されている必要があります。

> [!NOTE]
> `version` プロパティを 1.4 に設定すると、Outlook や Teams などのプラットフォームやアプリケーションの以前のバージョンのクライアントは、アダプティブ カードのユニバーサル アクションをサポートしていないため、アダプティブ カードとの互換性がありません。

カードのバージョンを 1.4 未満に設定し、`refresh` プロパティと `Action.Execute` のいずれかまたは両方を使用した場合は、以下のようになります。

| クライアント | 動作 |
| :-- | :-- |
| Teams | カードが作動しなくなります。 Teams クライアントのバージョンによっては、カードが更新されず、`Action.Execute` がレンダリングされない場合があります。 Teams で最大限の互換性を確保するために、フォールバック プロパティに `Action.Submit` を含む `Action.Execute` を定義します。 |

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

* UserIds は、アダプティブ カードのプロパティの一部であるユーザー MRIs `refresh` の配列です。

* カードの更新セクションで `userIds` リスト プロパティを `userIds: []` として指定した場合、カードは自動的に更新されません。 代わりに、Web やデスクトップではトリプル ドット メニューに、モバイル (Android や iOS) では長押しコンテキスト メニューに、カードを手動で更新するための **[カードの更新]** オプションがユーザーに表示されます。

* UserIds プロパティが追加されたのは、Teams チャネルには多数のメンバーが含まれる場合があるためです。 すべてのメンバーが同時にチャネルを視聴している場合、無条件に自動更新を行うと、ボットへの同時呼び出しが多くなります。 最大 `userIds` *60 (60)* のユーザー MRIs で自動更新を取得する必要があるユーザーを識別するには、常にプロパティを含める必要があります。

* 会話メンバーのTeams MRIs をフェッチできます。 アダプティブ カードの更新セクションで userIds リストに追加する方法の詳細については、「fetch roster or [user profile」を参照してください](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)。

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

アダプティブ カード用のユニバーサル アクションを使用すると、以前のバージョンのバージョンのカードと互換性のあるOutlook設定Teams。

### <a name="teams"></a>Teams

アダプティブ カードの以前のバージョンの Teams との下位互換機能を確保するためには、`fallback` プロパティを含め、その値を `Action.Submit` に設定する必要があります。 また、ボット コードは、`Action.Execute` と `Action.Submit` の両方を処理する必要があります。

詳細については、「[Teams での下位互換機能](/adaptive-cards/authoring-cards/universal-action-model#teams)」を参照してください。

## <a name="code-samples"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Teams ケータリング ボット | アダプティブ カードを使用して、食品の注文を受け入れるボットを作成します。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| まだ利用できません。 |
| シーケンシャル ワークフローアダプティブ カード | シーケンシャル ワークフロー、ユーザー固有のビュー、最新のアダプティブ カードをボットに実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>関連項目

* [Teams でのアダプティブ カードのアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [ボットの機能](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
