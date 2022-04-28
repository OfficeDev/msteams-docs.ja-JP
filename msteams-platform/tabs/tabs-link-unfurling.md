---
title: タブのリンクの展開とステージ ビュー
author: Rajeshwari-v
description: リンクの展開を解除し、ステージ ビューを開き、アプリでタブMicrosoft Teamsピン留めする方法について説明します。 コード例とサンプルを使用して、アダプティブ カードを使用してステージ ビューと呼び出しについて説明します。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: 043129d6a81543ac00acf8b64da49f75282823a2
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104085"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>タブのリンクの展開とステージ ビュー

ステージ ビューは新しいユーザー インターフェイス (UI) コンポーネントです。これにより、Teamsで全画面表示で開き、タブとしてピン留めされたコンテンツをレンダリングできます。

## <a name="stage-view"></a>ステージ ビュー

ステージ ビューは、Web コンテンツを表示するために呼び出すことができる全画面表示 UI コンポーネントです。 既存のリンク展開サービスは、アダプティブ カードとチャット サービスを使用して URL をタブに変換するために使用されるように更新されます。 ユーザーがチャットまたはチャネルで URL を送信すると、その URL はアダプティブ カードに割り当て解除されます。 ユーザーはカードで **[表示** ] を選択し、ステージ ビューから直接コンテンツをタブとしてピン留めできます。

## <a name="advantage-of-stage-view"></a>ステージ ビューの利点

ステージ ビューは、Teamsでコンテンツを表示するよりシームレスなエクスペリエンスを提供するのに役立ちます。 ユーザーは、コンテキストを離れることなくアプリから提供されたコンテンツを開いて表示でき、今後のクイック アクセスのためにコンテンツをチャットまたはチャネルにピン留めして、アプリに対するユーザー エンゲージメントを高めることができます。

## <a name="stage-view-vs-task-module"></a>ステージ ビューとタスク モジュール

|ステージ ビュー|タスク モジュール|
|:-----------|:-----------|
|ステージ ビューは、ページ、ダッシュボード、ファイルなど、ユーザーに表示する豊富なコンテンツがある場合に便利です。 全画面表示キャンバスでコンテンツをレンダリングするのに役立つ豊富な機能が提供されます。|[タスク モジュール](../task-modules-and-cards/task-modules/task-modules-tabs.md) は、ユーザーの注意を必要とするメッセージを表示したり、次の手順に進むのに必要な情報を収集したりするのに特に便利です。|
  
## <a name="invoke-stage-view"></a>ステージ ビューを呼び出す

ステージ ビューは、次の方法で呼び出すことができます。

* [アダプティブ カードからステージ ビューを呼び出す](#invoke-stage-view-from-adaptive-card)
* [ディープ リンクを使用してステージ ビューを呼び出す](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>アダプティブ カードからステージ ビューを呼び出す

ユーザーがTeams デスクトップ クライアントで URL を入力すると、ボットが呼び出され、ステージで URL を開くオプションを含む[アダプティブ カード](../task-modules-and-cards/cards/cards-actions.md)が返されます。 ステージが起動され、 `tabInfo` 提供されたら、ステージをタブとしてピン留めする機能を追加できます。  

次の画像は、アダプティブ カードから開かれたステージを示しています。

[![アダプティブ カードからステージを開く](~/assets/images/tab-images/open-stage-from-adaptive-card1.png)](~/assets/images/tab-images/open-stage-from-adaptive-card1.png#lightbox)

[![ステージを開く](~/assets/images/tab-images/open-stage-from-adaptive-card2.png)](~/assets/images/tab-images/open-stage-from-adaptive-card2.png#lightbox)

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

要求の種類は `invoke` .`composeExtension/queryLink`

> [!NOTE]
>
> * `invoke` ワークフローは現在 `appLinking` のワークフローに似ています。
> * 一貫性を維持するために、名前を `Action.Submit` `View`.
> * `websiteUrl` は、オブジェクト内で `TabInfo` 渡す必要があるプロパティです。

ステージ ビューを呼び出すプロセスを次に示します。

* ユーザーが **[表示**] を選択すると、ボットは要求を `invoke` 受け取ります。 要求の種類は .`composeExtension/queryLink`
* `invoke` ボットからの応答には、型 `tab/tabInfoAction` が含まれるアダプティブ カードが含まれています。
* ボットはコードで `200` 応答します。

> [!NOTE]
> モバイル クライアントTeams、[Teams ストア](/platform/concepts/deploy-and-publish/apps-publish-overview.md)を通じて配布されたアプリのステージ ビューを呼び出し、moblie 最適化エクスペリエンスがない場合は、デバイスの既定の Web ブラウザーが開きます。 ブラウザーは、オブジェクトのパラメーター`TabInfo`で`websiteUrl`指定された URL を開きます。

## <a name="invoke-stage-view-through-deep-link"></a>ディープ リンクを使用してステージ ビューを呼び出す

タブからディープ リンクを介してステージ ビューを呼び出すには、ディープ リンク URL を API でラップする `microsoftTeams.executeDeeplink(url)` 必要があります。 ディープ リンクは、カード内のアクションを `OpenURL` 介して渡すこともできます。

### <a name="syntax"></a>構文

ディープリンク構文を次に示します。

https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}
 
### <a name="examples"></a>例

ユーザーが URL を入力すると、アダプティブ カードに割り当て解除されます。

ステージ ビューを呼び出すディープ リンクの例を次に示します。

**例 1: threadId を使用した URL**

エンコードされていない URL:

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191,"websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true,"title":"Quotes:その他","threadId":"19:9UryYW9rjwpfx-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}

エンコードされた URL:

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D

**例 2: threadId のない URL**

エンコードされていない URL:

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context={"contentUrl":""https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191,"websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true,"title":"Quotes:その他"}

エンコード

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D

> [!NOTE]
> URL を貼り付ける前に、すべてのディープリンクをエンコードする必要があります。 エンコードされていない URL はサポートされていません。
>
> * ディープ リンクでは `name` 省略可能です。 含まれていない場合は、アプリ名に置き換えられます。
> * ディープ リンクは、アクションを介して `OpenURL` 渡すこともできます。
> * 特定のコンテキストからステージを起動するときは、そのコンテキストでアプリが動作することを確認します。 たとえば、個人用アプリからステージ ビューを起動する場合は、アプリに個人用スコープがあることを確認する必要があります。

## <a name="tab-information-property"></a>Tab information プロパティ

| プロパティ名 | 種類 | 文字数 | 説明 |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | String | 64 | このプロパティは、タブに表示されるエンティティの一意の識別子です。 これは必須フィールドです。|
| `name` | String | 128 | このプロパティは、チャネル インターフェイスのタブの表示名です。 この入力フィールドは省略できます。|
| `contentUrl` | String | 2048 | このプロパティは、Teams キャンバスに表示されるエンティティ UI を指す https:// URL です。 これは必須フィールドです。|
| `websiteUrl?` | String | 2048 | このプロパティは、ユーザーがブラウザーで表示することを選択した場合にポイントする https:// URL です。 これは必須フィールドです。|
| `removeUrl?` | String | 2048 | このプロパティは、ユーザーがタブを削除したときに表示される UI を指す https:// URL です。これは省略可能なフィールドです。|

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | C# |Node.js|
|-------------|-------------|------|----|
|ステージ ビューのタブ |ステージ ビューでタブをデモンストレーションするためのタブ サンプル アプリをMicrosoft Teamsします。|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [会話タブを作成する](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>関連項目

* [メッセージ拡張機能のリンクの展開解除](~/messaging-extensions/how-to/link-unfurling.md)
* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループの作成] タブ](~/tabs/how-to/create-channel-group-tab.md)
