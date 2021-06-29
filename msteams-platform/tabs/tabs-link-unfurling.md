---
title: タブのリンクの展開とステージ ビュー
author: Rajeshwari-v
description: リンクのリンクを解除し、ステージ ビューを開き、アプリでタブをピン留Microsoft Teamsします。
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: b54eb5942d19749b39bb9bb504dd8645f5655ef3
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179945"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>タブのリンクの展開とステージ ビュー

> [!NOTE]
> この機能は、パブリック開発者 [プレビューでのみ使用](../resources/dev-preview/developer-preview-intro.md) できます。

ステージ ビューは、新しいユーザー インターフェイス (UI) コンポーネントで、Teams で開き、タブとしてピン留めされたコンテンツをレンダリングできます。
 
> [!NOTE]
> 現時点では、Teamsクライアントはサポート タブリンクを開き、ステージ ビューをリンクしません。 モバイル クライアントは、 `websiteUrl` 開発者が提供する属性を使用して、デバイスの Web ブラウザーでページを開きます。

## <a name="stage-view"></a>ステージ ビュー

ステージ ビューは、Web コンテンツを表示するために呼び出すフルスクリーン UI コンポーネントです。 既存のリンク解除サービスが更新され、アダプティブ カードとチャット サービスを使用して URL をタブに変換するために使用されます。 ユーザーがチャットまたはチャネルで URL を送信すると、その URL はアダプティブ カードにリンク解除されます。 ユーザーは、カード **で [表示]** を選択し、ステージ ビューから直接タブとしてコンテンツをピン留めできます。

## <a name="advantage-of-stage-view"></a>ステージ ビューの利点

ステージ ビューを使用すると、コンテンツを表示するエクスペリエンスをシームレスにTeams。 ユーザーは、コンテキストを離れることなくアプリが提供するコンテンツを開いて表示し、コンテンツをチャットまたはチャネルにピン留めして、将来の迅速なアクセスを可能にできます。 これにより、アプリとのユーザーエンゲージメントが向上します。

## <a name="stage-view-vs-task-module"></a>ステージ ビューとタスク モジュール

|ステージ ビュー|タスク モジュール|
|:-----------|:-----------|
|ステージ ビューは、ページ、ダッシュボード、ファイルなど、ユーザーに表示するリッチ コンテンツがある場合に便利です。 コンテンツをフルスクリーン キャンバスでレンダリングするのに役立つ豊富な機能を提供します。|[タスク モジュールは](../task-modules-and-cards/task-modules/task-modules-tabs.md) 、ユーザーの注意が必要なメッセージを表示したり、次の手順に進むのに必要な情報を収集したりするために特に便利です。|
  
## <a name="invoke-stage-view"></a>ステージ ビューの呼び出し

ステージ ビューは、次の方法で呼び出します。

* [アダプティブ カードからステージ ビューを呼び出す](#invoke-stage-view-from-adaptive-card)
* [深いリンクを介してステージ ビューを呼び出す](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>アダプティブ カードからステージ ビューを呼び出す

ユーザーが Teams デスクトップ クライアントで URL を入力すると、ボットが呼び出され、ステージ[](../task-modules-and-cards/cards/cards-actions.md)内で URL を開くオプションを持つアダプティブ カードが返されます。 ステージを起動して指定した後、ステージをタブとしてピン留めする機能 `tabInfo` を追加できます。  

次の画像は、アダプティブ カードから開いたステージを表示します。

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card1.png" alt="Open a stage from Adaptive Card" width="700"/>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card2.png" alt="Open a stage" width="700"/>

### <a name="example"></a>例

アダプティブ カードからステージを開くコードを次に示します。

```json
{
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
} 
```

要求 `invoke` の種類は、 である必要があります `composeExtension/queryLink` 。

> [!NOTE]
> * `invoke` ワークフローは、現在のワークフローと似 `appLinking` ています。 
> * 一貫性を保つには、 という名前を付けをお `Action.Submit` 勧めします `View` 。
> * `websiteUrl` は、オブジェクトに渡す必要があるプロパティ `TabInfo` です。

ステージ ビューを呼び出すプロセスを次に示します。

* ユーザーが [表示] を **選択すると**、ボットは要求を受け取 `invoke` ります。 要求の種類はです `composeExtension/queryLink` 。
* `invoke` ボットからの応答には、型が含まれるアダプティブ カード `tab/tabInfoAction` が含まれる。
* ボットはコードで応答 `200` します。

> [!NOTE]
> 現在、Teamsクライアントはステージ ビュー機能をサポートしません。 ユーザーがモバイル クライアント **で [表示** ] を選択すると、ユーザーはデバイスのブラウザーに移動されます。 ブラウザーは、オブジェクトのパラメーターで指定 `websiteUrl` された URL を開 `TabInfo` きます。

## <a name="invoke-stage-view-through-deep-link"></a>深いリンクを介してステージ ビューを呼び出す

タブからディープ リンクを介してステージ ビューを呼び出す場合は、API でディープ リンク URL をラップする必要 `microsoftTeams.executeDeeplink(url)` があります。 ディープ リンクは、カード内の `OpenURL` アクションを介して渡される場合があります。

次の図は、ディープ リンクを介して呼び出されるステージ ビューを表示します。

<img src="~/assets/images/tab-images/invoke-stage-view-through-deep-link.png" alt="Invoke a Stage View through a deep link" width="400"/>

### <a name="syntax"></a>構文

ディープリンク構文を次に示します。  
 
https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":""[contentUrl]","websiteUrl":"[websiteUrl]","name":"[name]"}

### <a name="examples"></a>例

ユーザーが URL を入力すると、アダプティブ カードにリンク解除されます。

ステージ ビューを呼び出すディープ リンクの例を次に示します。

**例 1**

https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","websiteUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name":"Contoso"}

**例 2**

https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","websiteUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name":"Contoso"}

> [!NOTE]
> * ディープ `name` リンクではオプションです。 含まれていない場合は、アプリ名が置き換わります。
> * ディープ リンクは、アクションを介して渡 `OpenURL` される場合があります。
> * 現在、Teamsクライアントはステージ ビュー機能をサポートしません。 ユーザーがステージ ビューへのディープ リンクを選択すると、デバイスの Web ブラウザーにアクセスします。 Web ブラウザーは、ディープ リンクのパラメーターで指定された URL `websiteUrl` を開きます。
> * 特定のコンテキストからステージを起動する場合は、そのコンテキストでアプリが動作します。 たとえば、個人用アプリからステージ ビューを起動する場合は、アプリに個人用スコープが設定されている必要があります。

## <a name="tab-information-property"></a>タブ情報プロパティ

| プロパティ名 | 種類 | 文字数 | 説明 |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | String | 64 | このプロパティは、タブが表示されるエンティティの一意の識別子です。 これは必須フィールドです。|
| `name` | String | 128 | このプロパティは、チャネル インターフェイスのタブの表示名です。 この入力フィールドは省略できます。|
| `contentUrl` | String | 2048 | このプロパティは、https:// キャンバスに表示するエンティティ UI をポイントするTeamsです。 これは必須フィールドです。|
| `websiteUrl?` | String | 2048 | ユーザーがブラウザーで表示 https:// 場合、このプロパティは参照先の URL です。 これは必須フィールドです。|
| `removeUrl?` | String | 2048 | このプロパティは、https:// を削除するときに表示される UI を示す URL です。これはオプションのフィールドです。|

## <a name="see-also"></a>関連項目

* [メッセージング拡張機能リンクの分岐解除](~/messaging-extensions/how-to/link-unfurling.md)
* [Teamsタブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [会話タブを作成する](~/tabs/how-to/conversational-tabs.md)