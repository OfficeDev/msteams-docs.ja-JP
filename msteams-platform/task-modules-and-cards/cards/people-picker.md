---
title: アダプティブ カードでのユーザー ピッカー
description: アダプティブ カードで People Picker コントロールを使用する方法について説明します。
localization_priority: Normal
keywords: アダプティブ カード ユーザー選択
ms.topic: reference
author: Rajeshwari-v
ms.author: surbhigupta
ms.openlocfilehash: 4fda2916c6eaeb3cc0878911c21eb20e276844f3
ms.sourcegitcommit: 20b84e13b5cb6899f4eb54ca90a13b6da7a3e3d1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/16/2022
ms.locfileid: "62855894"
---
# <a name="people-picker-in-adaptive-cards"></a>アダプティブ カードでのユーザー ピッカー

>[!NOTE]
> 現在、アダプティブ カードの People Picker は、モバイル[](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams)向けのパブリック開発者プレビューでのみ利用可能で、デスクトップ用に一般公開 (GA) で利用できます。

ユーザー選択機能は、アダプティブ カードでユーザーを検索して選択するのに役立ちます。 ユーザー選択ウィンドウを入力コントロールとしてアダプティブ カードに追加できます。これは、チャット、チャネル、タスク モジュール、タブ間で機能します。 People Picker は、次の機能をサポートしています。        

* 1 人または複数のユーザーを検索します。
* 1 人または複数のユーザーを選択します。 
* 1 人または複数のユーザーに再割り当てします。 
* 選択したユーザーの名前を事前設定します。

## <a name="popular-scenarios"></a>一般的なシナリオ 

次の表に、アダプティブ カードのユーザー選択ウィンドウの一般的なシナリオと、対応するアクションを示します。

|シナリオ|Actions|
|----------|-------------------------|
|承認ベースのシナリオ| 要求、割り当て、および要件に基づいて、目的のユーザーに承認を再割り当てします。|
|インシデント管理| インシデントを追跡し、通知、割り当て、および即時のアクションを目的のユーザーに再割り当てします。| 
|プロジェクト管理| 特定のユーザーにチケットまたはバグを割り当てる。|
|ユーザー参照| 組織全体のユーザーを検索します。|

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

Web クライアントとデスクトップ クライアントは、アダプティブ カードのユーザー 選択ウィンドウをサポートします。 Web 上で検索する場合、ユーザー選択にはインライン入力エクスペリエンスが含まれる。

### <a name="reassignment-scenario-example"></a>再割り当てシナリオの例

ユーザー A (Robert) は、チャネル内のタスクのチケットを受け取り、不適切な割り当て先を認識します。 ユーザー A は、ボットに情報を送信するタスクを再割り当てします。 

**タスクを再割り当てするには**

1. [ **ユーザー選択** ] フィールドに名前が事前入力されている場所を再割り当てするを選択して、タスクを目的のユーザーに再割り当てします。
1. 正しくないユーザーの名前を削除します。 
1. イメージ シナリオ、ユーザー B (Mona)、およびタスクのユーザー C (ロビン) に基いて、目的のユーザーを選択します。 
1. **[割り当て]** を選択します。 割り当て後、情報はボットに送信されます。 
   ボットはアダプティブ カードを更新し、目的のユーザーに通知します。 
 
次の図は、再割り当てシナリオを示しています。    

![デスクトップ上のユーザー選択ウィンドウ](../../assets/images/cards/desktoppp.gif)

# <a name="mobile"></a>[モバイル](#tab/mobile)

> [!NOTE]
> 現時点では、この機能はパブリック開発者 [プレビューでのみ利用](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) できます。

Android および iOS モバイル クライアントは、アダプティブ カードで People Picker をサポートします。 モバイルでユーザー選択ツールを使用すると、ユーザーを検索および選択してユーザー エクスペリエンスを向上できます。 検索エクスペリエンスは、モバイルでの他のユーザー選択エクスペリエンスと似ています。

### <a name="reassignment-scenario-example"></a>再割り当てシナリオの例

ユーザー A (Robert) は、チャネル内のタスクのチケットを受け取り、不適切な割り当て先を認識します。 ユーザー A は、ボットに情報を送信するタスクを再割り当てします。 

**タスクを再割り当てするには**

1. [ **ユーザー選択** ] フィールドに名前が事前入力されている場所を再割り当てするを選択して、タスクを目的のユーザーに再割り当てします。
1. 正しくないユーザーの名前を削除します。
1. イメージ シナリオ、ユーザー B (Mona)、およびタスクのユーザー C (ロビン) に基いて、目的のユーザーを選択します。
1. **[完了]** を選択します。
1. **[割り当て]** を選択します。 割り当て後、情報はボットに送信されます。 
   ボットはアダプティブ カードを更新し、目的のユーザーに通知します。 

次の図は、再割り当てシナリオを示しています。 

![モバイルでのユーザー選択](../../assets/images/cards/mobilepp.gif)

---

## <a name="implement-people-picker"></a>ユーザー選択の実装

People Picker は、 [Input.ChoiceSet コントロールの拡張機能として実装](https://adaptivecards.io/explorer/Input.ChoiceSet.html) されます。 入力コントロールには、次の選択が含まれます。   

* 展開された選択範囲などのドロップダウン。
* ラジオ ボタン (1 つの選択範囲など)。
* 複数の選択範囲などのチェック ボックスをオンにします。  

> [!NOTE]
> コントロール `Input.ChoiceSet` は、プロパティとに `style` 基 `isMultiSelect` づいて行います。  

### <a name="update-schema"></a>スキーマの更新

次のプロパティは、カードで `Input.ChoiceSet` ユーザー選択ウィンドウのエクスペリエンスを有効にするスキーマの追加です。  

#### <a name="inputchoiceset-control"></a>Input.ChoiceSet コントロール

|プロパティ |型 |必須 |説明 |
|----|----|----|----|
|**choices.data** |**Data.Query** |いいえ |指定したデータセットから結果を取得することにより、さまざまなユーザーの種類に対して動的自動完了を有効にできます。 |

#### <a name="dataquery"></a>Data.Query

|プロパティ |型 |必須 |説明|
|--|--|--|--|
|**データセット** |String |はい |動的にフェッチする必要があるデータの種類。|   

#### <a name="dataset"></a>データセット
次の表に、ユーザー選択ツールの **データセットとして定義済** みの値を示します。   

|データセット|検索範囲
|--|--|
|**graph.microsoft.com/users** |組織全体のすべてのメンバーを検索します。|
|**graph.microsoft.com/users?scope=currentContext** |チャットや特定のカードが送信されるチャネルなど、現在の会話のメンバー内で検索します。|        

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

次の図は、組織検索を使用したアダプティブ カードのユーザー選択機能を示しています。

![People Picker Org Search](../../assets/images/cards/peoplepicker-org-search.png)

会話メンバーのリスト内で検索を有効にするには、データセット テーブルで定義されている適切なデータセットを [使用](#dataset) します。 `isMultiSelect` プロパティは、コントロール内の複数のユーザーの選択を有効にするために使用されます。 既定では false に設定され、この設定では 1 人のユーザーのみを選択できます。

### <a name="data-submission"></a>データ提出

選択したデータを`Action.Submit``Action.Execute`ボットに使用または送信できます。 ボット`invoke`で受け取ったペイロードは、Microsoft Azure Active Directory (Azure AD) の一覧または静的リストで提供される ID です。
[ユーザー選択] で、コントロールでユーザーを `Azure AD ID` 選択すると、ユーザーの値が返されます。 は `Azure AD ID` 文字列であり、ディレクトリ内のユーザーを一意に識別します。

ボットに送信される値の形式は、プロパティの値によって異 `isMultiSelect` なります。

|の値 `isMultiSelect`|フォーマット|
|--|--|
|false _(単一の選択)_|<_Azure_AD_ID>|
|true _(複数選択)_|<_Azure_AD_ID_1>,<selected_Azure_AD_ID_2>,<selected_Azure_AD_ID_3>|  

[ユーザー選択 `Azure AD ID`] を使用すると、対応するユーザーが事前に選択されます。 

## <a name="preselection-of-user"></a>ユーザーの事前選択

People Picker は、アダプティブ カードを作成して送信するときに、コントロール内のユーザーの事前選択をサポートします。 `Input.ChoiceSet` は、 `value` ユーザーの事前選択に使用されるプロパティをサポートします。 このプロパティの形式 `value` は、データ送信で送信された値の形式 [と同じです](#data-submission)。  
次の一覧は、ユーザーを事前に選択する情報を提供します。

* コントロール内の単一ユーザーの場合は、ユーザーのユーザー`Azure AD ID`を .`value` 
* 複数のユーザー (is `isMultiSelect` など) の場合 `true`は、s のコンマ区切り文字列を指定 `Azure AD ID`します。  

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

静的な選択肢は、定義済みのデータセットにカスタム プロファイルを挿入する必要があるシナリオをサポートします。 `Input.ChoiceSet` json で静的 `choices` に指定できます。 静的な選択肢は、ユーザーが選択できる選択肢を作成するために使用されます。

> [!NOTE]
> 静的 `choices` は動的データセットと一緒に使用されます。 

選択肢は、 で構成されます`title``value`。 ユーザー選択と共`title``value`に使用すると、これらの選択肢は、名前と識別子を持つユーザー プロファイルに変換されます。 これらのカスタム プロファイルは、検索クエリが指定したクエリと一致する場合にも検索結果の一部です `title`。    
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

次の図は、組織検索で静的な選択肢を持つアダプティブ カードのユーザー選択を示しています。

![ユーザー選択の静的な選択](../../assets/images/cards/peoplepicker-static-choice.png)


さまざまなシナリオで効率的なタスク管理を行うユーザー選択ウィンドウを実装できます。  

## <a name="code-sample"></a>コード サンプル

| サンプルの名前           | 説明 | C#    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|アダプティブ カードのユーザーピッカー コントロール| このサンプルでは、アダプティブ カードでユーザー選択コントロールを使用する方法を示します。|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-people-picker-adaptive-card/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-people-picker-adaptive-card/nodejs) | 


## <a name="see-also"></a>関連項目

[カード リファレンス](cards-reference.md)

