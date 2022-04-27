---
title: アダプティブ カードのユーザー ピッカー
description: アダプティブ カードで People Picker コントロールを使用する方法について説明します
localization_priority: Normal
keywords: アダプティブ カードのユーザー選択
ms.topic: reference
author: Rajeshwari-v
ms.author: surbhigupta
ms.openlocfilehash: 8a78be74d8142600ccc08093744491a19900e60b
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073433"
---
# <a name="people-picker-in-adaptive-cards"></a>アダプティブ カードのユーザー ピッカー

>[!NOTE]
> 現在、アダプティブ カードのユーザー選択ツールは、モバイル向けの [パブリック 開発者向けプレビュー](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) でのみ使用でき、デスクトップでは一般公開 (GA) されています。

ユーザー選択ウィンドウは、ユーザーがアダプティブ カードでユーザーを検索して選択するのに役立ちます。 チャット、チャネル、タスク モジュール、タブ間で機能するアダプティブ カードに、入力コントロールとして People Picker を追加できます。 People Picker では、次の機能がサポートされています。

* 1 人または複数のユーザーを検索します。
* 1 人または複数のユーザーを選択します。
* 1 人または複数のユーザーに再割り当てします。
* 選択したユーザーの名前を事前設定します。

## <a name="popular-scenarios"></a>一般的なシナリオ

次の表に、アダプティブ カードのユーザー選択ツールと対応するアクションの一般的なシナリオを示します。

|シナリオ|Actions|
|----------|-------------------------|
|承認ベースのシナリオ| 要件に基づいて、目的のユーザーに承認を要求、割り当て、再割り当てする。|
|インシデント管理| インシデントを追跡し、迅速なアクションのために目的のユーザーに通知、割り当て、再割り当てするため。|
|プロジェクト管理| 特定のユーザーにチケットまたはバグを割り当てるには。|
|ユーザー参照| 組織全体のユーザーを検索する。|

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

Web クライアントとデスクトップ クライアントは、アダプティブ カードでのユーザー選択をサポートします。 Web で検索するときに、ユーザー選択ウィンドウにはインライン入力エクスペリエンスが含まれます。

### <a name="reassignment-scenario-example"></a>再割り当てシナリオの例

ユーザー A (Robert) は、チャネル内のタスクのチケットを受け取り、不適切な担当者を認識します。 ユーザー A は、情報をボットに返送するタスクを再割り当てします。

タスクを再割り当てするには:

1. [ユーザー選択フィールドに名前が事前設定されている場所を **再** 割り当て] を選択して、タスクを目的のユーザーに再割り当てします。
1. 正しくないユーザーの名前を削除します。
1. イメージ シナリオに従って目的のユーザーを選択し、タスクのユーザー B (Pdb)、およびユーザー C (Robin) を選択します。
1. **[割り当て]** を選択します。 割り当て後、情報はボットに送信されます。
   ボットはアダプティブ カードを更新し、目的のユーザーに通知します。

次の図は、再割り当てのシナリオを示しています。

![デスクトップ上のユーザー選択ウィンドウ](../../assets/images/cards/desktoppp.gif)

# <a name="mobile"></a>[モバイル](#tab/mobile)

> [!NOTE]
> 現時点では、この機能は [パブリック開発者向けプレビュー](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) でのみ使用できます。

Android および iOS モバイル クライアントでは、アダプティブ カードでのユーザー選択がサポートされます。 モバイルでユーザー選択ウィンドウを使用して、ユーザーを検索および選択して、ユーザー エクスペリエンスを向上させることができます。 検索エクスペリエンスは、モバイルの他のユーザー選択エクスペリエンスと似ています。

### <a name="reassignment-scenario-example"></a>再割り当てシナリオの例

ユーザー A (Robert) は、チャネル内のタスクのチケットを受け取り、不適切な担当者を認識します。 ユーザー A は、情報をボットに返送するタスクを再割り当てします。

タスクを再割り当てするには:

1. [ユーザー選択フィールドに名前が事前設定されている場所を **再** 割り当て] を選択して、タスクを目的のユーザーに再割り当てします。
1. 正しくないユーザーの名前を削除します。
1. イメージ シナリオに従って目的のユーザーを選択し、タスクのユーザー B (Pdb)、およびユーザー C (Robin) を選択します。
1. [**完了**] を選択します。
1. **[割り当て]** を選択します。 割り当て後、情報はボットに送信されます。
   ボットはアダプティブ カードを更新し、目的のユーザーに通知します。

次の図は、再割り当てのシナリオを示しています。

![モバイル上のユーザー選択ウィンドウ](../../assets/images/cards/mobilepp.gif)

---

## <a name="implement-people-picker"></a>ユーザー選択ウィンドウを実装する

ユーザー選択ウィンドウは、 [Input.ChoiceSet](https://adaptivecards.io/explorer/Input.ChoiceSet.html) コントロールの拡張機能として実装されます。 入力コントロールには、次の選択項目が含まれます。

* 展開された選択などのドロップダウン。
* 1 つの選択など、ラジオ ボタン。
* 複数の選択など、チェック ボックス。  

> [!NOTE]
> コントロールは`Input.ChoiceSet`、プロパティと`isMultiSelect`プロパティに`style`基づいています。  

### <a name="update-schema"></a>スキーマの更新

次のプロパティは、カードで People Picker エクスペリエンスを `Input.ChoiceSet` 有効にするためのスキーマへの追加です。  

#### <a name="inputchoiceset-control"></a>Input.ChoiceSet コントロール

|プロパティ |型 |必須 |説明 |
|----|----|----|----|
|**choices.data** |**Data.Query** |いいえ |指定したデータセットから結果をフェッチすることで、さまざまなユーザーの種類に対して動的な自動完了を有効にします。 |

#### <a name="dataquery"></a>Data.Query

|プロパティ |型 |必須 |説明|
|--|--|--|--|
|**データセット** |String |はい |動的にフェッチする必要があるデータの種類。|

#### <a name="dataset"></a>データセット

次の表に、ユーザー選択の **データセット** として定義済みの値を示します。

|データセット|検索スコープ
|--|--|
|**graph.microsoft.com/users** |組織全体のすべてのメンバーを検索します。|
|**graph.microsoft.com/users?scope=currentContext** |特定のカードが送信されるチャットやチャネルなど、現在の会話のメンバー内で検索します。|

### <a name="example"></a>例

組織検索を使用して People Picker を作成するコード例は次のとおりです。

```json
{
 "type": "AdaptiveCard",
 "body": [
  {
   "type": "TextBlock",
   "size": "Medium",
   "weight": "Bolder",
   "text": "People Picker with Org search enabled"
  },
  {
   "type": "Input.ChoiceSet",
   "choices": [],
   "choices.data": {
    "type": "Data.Query",
    "dataset": "graph.microsoft.com/users"
   },
   "id": "people-picker",
   "isMultiSelect": true
  }
 ],
 "actions": [
  {
   "type": "Action.Submit",
   "title": "Submit"
  }
 ],
 "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
 "version": "1.2"
}
```  

次の図は、組織検索を使用したアダプティブ カードのユーザー選択ウィンドウを示しています。

:::image type="content" source="../../assets/images/Cards/peoplepicker-org-search.png" alt-text="ユーザー選択組織の検索":::

会話メンバーの一覧内で検索を有効にするには、データセット テーブルで定義されている適切な [データセット](#dataset) を使用します。 `isMultiSelect` プロパティは、コントロール内の複数のユーザーの選択を有効にするために使用されます。 既定では false に設定されており、この設定では 1 人のユーザーのみを選択できます。

### <a name="data-submission"></a>データの送信

選択したデータを使用 `Action.Submit` したり、ボットに送信したりできます `Action.Execute` 。 ボットで受信されるペイロードは`invoke`、Microsoft Azure Active Directory (Azure AD) ID または静的リストで提供される ID の一覧です。
ユーザー選択ウィンドウで、コントロールでユーザーが選択されている場合、 `Azure AD ID` ユーザーの値が返されます。 は `Azure AD ID` 文字列であり、ディレクトリ内のユーザーを一意に識別します。

ボットに送信される値の形式は、プロパティの `isMultiSelect` 値によって異なります。

|の値 `isMultiSelect`|フォーマット|
|--|--|
|false _(単一選択)_|<selected_Azure_AD_ID>|
|true _(複数選択)_|<selected_Azure_AD_ID_1>、<selected_Azure_AD_ID_2>、<selected_Azure_AD_ID_3>|  

`Azure AD ID`[ユーザー 選択] を使用すると、対応するユーザーが事前に選択されます。

## <a name="preselection-of-user"></a>ユーザーの事前選択

ユーザー選択ウィンドウは、アダプティブ カードを作成して送信するときに、コントロール内のユーザーの事前選択をサポートします。 `Input.ChoiceSet` は、ユーザーの `value` 事前選択に使用されるプロパティをサポートします。 この `value` プロパティの形式は、 [データ](#data-submission)送信で送信された値の形式と同じです。  
次の一覧では、ユーザーを事前選択するための情報を示します。

* コントロール内の 1 人のユーザーの場合は、ユーザー`value`の名前を `Azure AD ID` .
* 複数のユーザー (次のように `isMultiSelect` ) の場合は `true`、コンマ区切りの文字列 `Azure AD ID`s を指定します。  

次の例では、1 人のユーザーの事前選択について説明します。

```json
{
 "type": "AdaptiveCard",
 "body": [
  {
   "type": "TextBlock",
   "size": "Medium",
   "weight": "Bolder",
   "text": "People Picker with Org search enabled"
  },
  {
   "type": "Input.ChoiceSet",
   "choices": [],
   "choices.data": {
    "type": "Data.Query",
    "dataset": "graph.microsoft.com/users"
   },
   "id": "people-picker",
   "value": "<Azure AD ID 1>"
  }
 ],
 "actions": [
  {
   "type": "Action.Submit",
   "title": "Submit"
  }
 ],
 "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
 "version": "1.2"
}
```  

次の例では、複数のユーザーの事前選択について説明します。

```json
{
 "type": "AdaptiveCard",
 "body": [
  {
   "type": "TextBlock",
   "size": "Medium",
   "weight": "Bolder",
   "text": "People Picker with Org search enabled"
  },
  {
   "type": "Input.ChoiceSet",
   "choices": [],
   "choices.data": {
    "type": "Data.Query",
    "dataset": "graph.microsoft.com/users"
   },
   "id": "people-picker",
   "isMultiSelect": true,
   "value": "<Azure AD ID 1>,<Azure AD ID 2>,<Azure AD ID 3>"
  }
 ],
 "actions": [
  {
   "type": "Action.Submit",
   "title": "Submit"
  }
 ],
 "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
 "version": "1.2"
}
```

## <a name="static-choices"></a>静的な選択肢

静的な選択肢では、定義済みのデータセットにカスタム プロファイルを挿入する必要があるシナリオがサポートされています。 `Input.ChoiceSet` は json で静的に指定することを `choices` サポートしています。 静的な選択肢は、ユーザーが選択できる選択肢を作成するために使用されます。

> [!NOTE]
> 静的 `choices` は、動的データセットと共に使用されます。

選択は、次の `title` 要素で `value`構成されます。 ユーザー選択ウィンドウと共に使用すると、これらの選択肢は、名前と識別子を持つ `title` ユーザー プロファイルに `value` 変換されます。 これらのカスタム プロファイルは、検索クエリが特定のクエリと一致する場合にも、検索結果の一部です `title`。
次の例では、静的な選択肢について説明します。

```json
{
 "type": "AdaptiveCard",
 "body": [
  {
   "type": "TextBlock",
   "size": "Medium",
   "weight": "Bolder",
   "text": "People Picker with Org search enabled"
  },
  {
   "type": "Input.ChoiceSet",
   "choices": [
    {
     "title": "Custom Profile 1",
     "value": "Profile1"
    },
    {
     "title": "Custom Profile 2",
     "value": "Profile2"
    }
   ],
   "choices.data": {
    "type": "Data.Query",
    "dataset": "graph.microsoft.com/users"
   },
   "id": "people-picker",
   "isMultiSelect": true
  }
 ],
 "actions": [
  {
   "type": "Action.Submit",
   "title": "Submit"
  }
 ],
 "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
 "version": "1.2"
}
```

次の図は、組織検索で静的な選択肢を持つアダプティブ カードの People Picker を示しています。

:::image type="content" source="../../assets/images/Cards/peoplepicker-static-choice.png" alt-text="people-picker-static-choice":::

さまざまなシナリオで効率的なタスク管理を行うための People Picker を実装できます。  

## <a name="code-sample"></a>コード サンプル

| サンプルの名前           | 説明 | C#    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|アダプティブ カードのユーザー 選択コントロール| このサンプルでは、アダプティブ カードでユーザー選択コントロールを使用する方法を示します。|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-people-picker-adaptive-card/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-people-picker-adaptive-card/nodejs) |

## <a name="see-also"></a>関連項目

[カード リファレンス](cards-reference.md)
