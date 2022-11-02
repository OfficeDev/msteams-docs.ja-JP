---
title: タブのリンクの展開とステージ ビュー
author: Rajeshwari-v
description: Web コンテンツを表示するために呼び出される全画面表示 UI コンポーネントであるステージ ビューについて説明します。 リンクの展開は、アダプティブ カードを使用して URL をタブに変換するために使用されます。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 2563cfd266b967bd8c55c24491165c9979bad145
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820088"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>タブのリンクの展開とステージ ビュー

ステージ ビューは、新しいユーザー インターフェイス (UI) コンポーネントです。 これにより、Teams で全画面表示で開き、タブとしてピン留めされたコンテンツをレンダリングできます。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="stage-view"></a>ステージ ビュー

ステージ ビューは、Web コンテンツを表示するために呼び出すことができる全画面表示 UI コンポーネントです。 既存のリンク展開サービスが更新され、アダプティブ カードとチャット サービスを使用して URL をタブに変換するために使用されます。 ユーザーがチャットまたはチャネルで URLを送信すると、その URL はアダプティブ カードに展開されます。 ユーザーはカードで **[表示]** を選択し、ステージ ビューから直接コンテンツをタブとしてピン留めできます。

## <a name="advantage-of-stage-view"></a>ステージ ビューの利点

Stage View helps provide a more seamless experience of viewing content in Teams. Users can open and view the content provided by your app without leaving the context, and they can pin the content to the chat or channel for future quick access leading to a higher user engagement with your app.

## <a name="stage-view-vs-task-module"></a>ステージ ビューとタスク モジュール

|ステージ ビュー|タスク モジュール|
|:-----------|:-----------|
|ステージ ビューは、ページ、ダッシュボード、ファイルなど、ユーザーに表示する豊富なコンテンツがある場合に便利です。 これは、全画面表示キャンバスでコンテンツをレンダリングするのに役立つ豊富な機能を提供します。|[タスク モジュール](../task-modules-and-cards/task-modules/task-modules-tabs.md) は、ユーザーの注意を必要とするメッセージを表示したり、次の手順に進むのに必要な情報を収集したりするのに特に便利です。|
  
## <a name="invoke-stage-view"></a>ステージ ビューを呼び出す

ステージ ビューは、次の方法で呼び出すことができます。

* [アダプティブ カードからステージ ビューを呼び出す](#invoke-stage-view-from-adaptive-card)
* [ディープ リンクを使用してステージ ビューを呼び出す](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>アダプティブ カードからステージ ビューを呼び出す

ユーザーが Teams デスクトップ クライアントで URL を入力すると、ボットが呼び出され、ステージで URL を開くオプションを含む[アダプティブ カード](../task-modules-and-cards/cards/cards-actions.md)が返されます。 ステージが起動され、`tabInfo` が提供されたら、ステージをタブとしてピン留めする機能を追加できます。  

次の画像は、アダプティブ カードから開かれたステージを示しています。

:::image type="content" source="../assets/images/tab-images/open-stage-from-adaptive-card1.png" alt-text="アダプティブ カードからのオープン ステージを示すスクリーンショット。"lightbox="~/assets/images/tab-images/open-stage-from-adaptive-card1.png":::

:::image type="content" source="../assets/images/tab-images/open-stage-from-adaptive-card2.png" alt-text="カードから開いているステージを示すスクリーンショット。"lightbox="~/assets/images/tab-images/open-stage-from-adaptive-card2.png":::

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

`invoke` 要求の種類は `composeExtension/queryLink` である必要があります。

> [!NOTE]
>
> * `invoke` ワークフローは現在の `appLinking` ワークフローに似ています。
> * 一貫性を維持するために、`Action.Submit` に `View` という名前を付けることをお勧めします。
> * `websiteUrl` は、`TabInfo` オブジェクトで渡される必須のプロパティです。

ステージ ビューを呼び出すプロセスを次に示します。

* When the user selects **View**, the bot receives an `invoke` request. The request type is `composeExtension/queryLink`.
* `invoke` ボットからの応答には、型 `tab/tabInfoAction` が含まれるアダプティブ カードが含まれています。
* ボットは `200` コードで応答します。

> [!NOTE]
>
> Teams モバイル クライアントでは、 [Teams ストア](~/concepts/deploy-and-publish/apps-publish-overview.md) を介して配布され、モバイル最適化エクスペリエンスを持たないアプリのステージ ビューを呼び出すと、デバイスの既定の Web ブラウザーが開きます。 ブラウザは、`TabInfo` オブジェクトの `websiteUrl` パラメータで指定された URL を開きます。

## <a name="invoke-stage-view-through-deep-link"></a>ディープ リンクを使用してステージ ビューを呼び出す

タブからディープ リンクを介してステージ ビューを呼び出すには、ディープ リンク URL を `app.openLink(url)` API でラップする必要があります。 ディープ リンクは、カード内の `OpenURL` アクションを介して渡すこともできます。

### <a name="syntax"></a>構文

ディープ リンク構文を次に示します。

`<https://teams.microsoft.com/l/stage/{appId}/0?context>={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}`

### <a name="examples"></a>例

ユーザーが URL を入力すると、アダプティブ カードに展開されます。

ステージ ビューを呼び出すディープ リンクの例を次に示します。

**例 1: threadId を使用した URL**

エンコードされていない URL:

`<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context>={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191","websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous","threadId":"19:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}`

エンコードされた URL:

`<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D>`

**例 2: threadId のない URL**

エンコードされていない URL:

`<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context>={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191","websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous"}`

エンコード済み

`<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D>`

> [!NOTE]
> URL を貼り付ける前に、すべてのディープ リンクをエンコードする必要があります。 エンコードされていない URL はサポートされていません。
>
> * `name` はディープ リンクで省略可能です。 含まれていない場合は、アプリ名に置き換えられます。
> * ディープ リンクは、`OpenURL` アクションを介して渡すこともできます。
> * 特定のコンテキストからステージを起動するときは、そのコンテキストでアプリが動作することを確認します。 たとえば、個人用アプリからステージ ビューを起動する場合は、アプリに個人用スコープがあることを確認する必要があります。

## <a name="tab-information-property"></a>Tab 情報プロパティ

| プロパティ名 | 種類 | 文字数 | 説明 |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | String | 64 | このプロパティは、タブに表示されるエンティティの固有の識別子です。 これは必須フィールドです。|
| `name` | String | 128 | このプロパティは、チャネル インターフェイスのタブの表示名です。 この入力フィールドは省略できます。|
| `contentUrl` | String | 2048 | This property is the https:// URL that points to the entity UI to be displayed in the Teams canvas. This is a required field.|
| `websiteUrl?` | String | 2048 | This property is the https:// URL to point at, if a user selects to view in a browser. This is a required field.|
| `removeUrl?` | String | 2048 | このプロパティは、ユーザーがタブを削除したときに表示される UI を指す https:// URL です。これは省略可能なフィールドです。|

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | C# |Node.js|
|-------------|-------------|------|----|
|ステージ ビューのタブ |ステージ ビューでタブをデモンストレーションするための Microsoft Teams タブ サンプル アプリ。|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [会話タブを作成する](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>関連項目

* [Teams の [ビルド] タブ](what-are-tabs.md)
* [リンク展開を追加する](../messaging-extensions/how-to/link-unfurling.md)
* [composeExtensions](../resources/schema/manifest-schema.md#composeextensions)
* [アダプティブ カードを使用してタブをビルドする](how-to/build-adaptive-card-tabs.md)
* [ディープ リンクの作成](../concepts/build-and-test/deep-links.md)
