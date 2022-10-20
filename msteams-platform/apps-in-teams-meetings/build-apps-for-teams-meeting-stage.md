---
title: Teams 会議ステージ用のアプリをビルドする
author: v-sdhakshina
description: Teams 会議ステージ用のアプリを構築し、API をステージングするために共有し、会議のステージにコンテンツを共有するためのディープ リンクを生成する方法について説明します。
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: 440e48d370d18564f5bba869d95c63bc25b11e4e
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615435"
---
# <a name="build-apps-for-teams-meeting-stage"></a>Teams 会議ステージ用のアプリをビルドする

ステージに共有すると、ユーザーは進行中の会議の会議のサイド パネルから会議ステージにアプリを共有できます。 この共有は、パッシブ画面共有と比較して、対話型で協調的です。

ステージへの共有を呼び出すには、ユーザーは会議のサイド パネルの右上にある **[ステージに共有** ] アイコンを選択できます。 **[ステージに共有]** アイコンは Teams クライアントにネイティブであり、選択するとアプリ全体が会議ステージに共有されます。

## <a name="app-manifest-settings-for-apps-in-meeting-stage"></a>会議ステージのアプリのアプリ マニフェスト設定

会議ステージにアプリを共有するには、アプリ マニフェストのプロパティを `context` 次のように更新します。

```json
"context":[ 
    "meetingSidePanel", 
    "meetingStage" 
     ] 
```

## <a name="advanced-share-to-stage-apis"></a>API をステージングするための高度な共有

アプリ全体を会議ステージに共有しても、アプリの特定の部分を共有する場合ほど役に立たないシナリオは多数あります。  

1. ブレーンストーミング アプリまたはホワイトボード アプリの場合、ユーザーは会議内の特定のボードと、すべてのボードとアプリ全体を共有したい場合があります。  

1. 医療アプリの場合、医師は画面上の X 線のみを患者と共有する場合と、すべての患者レコードや結果などとアプリ全体を共有する場合があります。

1. ユーザーは、一度に 1 つのコンテンツ プロバイダー (YouTube など) からコンテンツを共有する場合と、ビデオ カタログ全体をステージ上で共有する場合があります。

このようなシナリオのユーザーを支援するために、Teams クライアント SDK 内で API をリリースしました。これにより、会議のサイド パネルのボタンからアプリの特定の部分の共有をプログラムで呼び出してステージできます。

:::image type="content" source="../assets/images/apps-in-meetings/shared-meeting-stage-edit-review-component.png" alt-text="スクリーンショットは、会議ステージ ビューへの共有を示しています。":::

次の API を使用して、アプリの特定の部分を共有します。

|メソッド| 説明| ソース|
|---|---|----|
|[**アプリ コンテンツをステージに共有する**](#share-app-content-to-stage-api)| 会議の会議サイド パネルから、アプリの特定の部分を会議ステージに共有します。 | [Microsoft Teams JavaScript ライブラリ SDK](/javascript/api/@microsoft/teams-js/meeting) |
|[**アプリ コンテンツ ステージの共有状態を取得する**](#get-app-content-stage-sharing-state-api)| 会議ステージでアプリの共有状態に関する情報を取得します。 | [Microsoft Teams JavaScript ライブラリ SDK](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingstate) |
|[**アプリ コンテンツ ステージの共有機能を取得する**](#get-app-content-stage-sharing-capabilities-api)| 共有のためのアプリの機能を会議ステージに取得します。 | [Microsoft Teams JavaScript ライブラリ SDK](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingcapabilities) |

## <a name="share-app-content-to-stage-api"></a>アプリ コンテンツをステージに共有する API

`shareAppContentToStage` API を使用すると、アプリの特定の部分を会議ステージに対して共有できます。 この API は、Teams クライアント SDK を通して使用できます。

### <a name="prerequisite"></a>前提条件

* `shareAppContentToStage` API を使用するには、RSC アクセス許可を取得する必要があります。 アプリ マニフェストで、`authorization` プロパティと、`resourceSpecific` フィールドの `name` および `type` を構成します。 次に例を示します。

    ```json
    "authorization": {
        "permissions": { 
        "resourceSpecific": [
        { 
         "name": "MeetingStage.Write.Chat",
         "type": "Delegated"
        }
        ]
    }
    }
    ```

* `appContentUrl` manifest.json 内の配列で `validDomains` 許可する必要があります。それ以外の場合、API は 501 エラーを返します。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、エラーと結果という 2 つのパラメーターが含まれています。 *エラー* には、エラーの種類 *SdkError* が含まれるか、共有が成功した場合は null が含まれます。 *結果* には、成功した共有がある場合は true の値を格納するか、共有が失敗したときに null を含めることができます。 |
|**appContentURL**| String | はい | ステージ上で共有される URL。 |

### <a name="example"></a>例

```javascript
const appContentUrl = "https://www.bing.com/";

microsoftTeams.meeting.shareAppContentToStage((err, result) => {
    if (result) {
        // handle success
    }
    if (err) {
        // handle error
    }
}, appContentUrl);
```

### <a name="response-codes"></a>応答コード

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **500** | 内部エラー。 |
| **501** | API は現在のコンテキストではサポートされていません。|
| **1000** | アプリには、共有のステージングを許可するための適切なアクセス許可がありません。|

## <a name="get-app-content-stage-sharing-state-api"></a>アプリ コンテンツ ステージの共有状態を取得する API

API `getAppContentStageSharingState` を使用すると、会議ステージでのアプリ共有に関する情報を取得できます。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、エラーと結果という 2 つのパラメーターが含まれています。 *エラー* には、エラーの場合はエラーの種類 *SdkError* が含まれ、共有が成功した場合は null が含まれます。 *結果* には、共有が成功した場合はオブジェクトを`IAppContentStageSharingState`含めるか、エラーが発生した場合は null を含めることができます。|

### <a name="example"></a>例

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates if app is sharing content on the meeting stage.
    }
});
```

`getAppContentStageSharingState` API の JSON 応答本文は次のとおりです。

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>応答コード

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **500** | 内部エラー。 |
| **501** | API は現在のコンテキストではサポートされていません。|
| **1000** | アプリには、共有のステージングを許可するための適切なアクセス許可がありません。|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>アプリ コンテンツ ステージの共有機能を取得する API

`getAppContentStageSharingCapabilities` API を使用すると、会議ステージに対して共有するためのアプリの機能を取得できます。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、エラーと結果という 2 つのパラメーターが含まれています。 *エラー* には、エラーの種類 *SdkError* が含まれるか、共有が成功した場合は null が含まれます。 結果には、共有が成功した場合はオブジェクトを `IAppContentStageSharingCapabilities` 含めるか、エラーが発生した場合は null を含めることができます。|

### <a name="example"></a>例

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

`getAppContentStageSharingCapabilities` API の JSON 応答本文は次のとおりです。

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>応答コード

次の表に、応答コードを示します。

|応答コード|説明|
|---|---|
| **500** | 内部エラー。 |
| **501** | API は現在のコンテキストではサポートされていません。|
| **1000** | アプリには、共有のステージングを許可するアクセス許可がありません。|

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>会議のステージにコンテンツを共有するためのディープ リンクを生成する

また、ディープ リンクを生成してアプリを共有し、会議をステージングして開始または参加することもできます。

> [!NOTE]
>
> * 現在、会議のステージにコンテンツを共有するためのディープ リンクは UX の改善が行われ、 [パブリック開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ利用できます。
> * 会議のステージにコンテンツを共有するためのディープ リンクは、Teams デスクトップ クライアントでのみサポートされています。

進行中の会議の一部であるユーザーがアプリでディープ リンクを選択すると、アプリがステージに共有され、アクセス許可ポップアップ ウィンドウが表示されます。 ユーザーは、アプリと共同作業するための参加者へのアクセス権を付与できます。

:::image type="content" source="../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="スクリーンショットは、アクセス許可ポップアップ ウィンドウを示す例です。":::

ユーザーが会議に参加していない場合、ユーザーは Teams カレンダーにリダイレクトされ、会議に参加したり、インスタント会議を開始したりできます (今すぐ会議を開く)。

:::image type="content" source="../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="スクリーンショットは、進行中の会議がない場合のポップアップ ウィンドウを示す例です。":::

ユーザーがインスタント会議 (今すぐ会議) を開始すると、参加者を追加してアプリを操作できます。

:::image type="content" source="../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="スクリーンショットは、参加者を追加するオプションと、アプリを操作する方法を示す例です。":::

ステージでコンテンツを共有するためのディープ リンクを追加するには、アプリ コンテキストが必要です。 アプリ コンテキストを使用すると、Teams クライアントはアプリ マニフェストをフェッチし、ステージでの共有が可能かどうかを確認できます。 アプリ コンテキストの例を次に示します。

`{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

アプリ コンテキストのクエリ パラメーターは次のとおりです。

* `appID`: これは、アプリ マニフェストから取得できる ID です。
* `appSharingUrl`: ステージで共有する必要がある URL は、アプリ マニフェストで定義された有効なドメインである必要があります。 URL が有効なドメインでない場合は、エラーの説明をユーザーに提供するエラー ダイアログが表示されます。
* `useMeetNow`: これには、true または false のブール型パラメーターが含まれます。
  * **True**: 値が `UseMeetNow` true で、進行中の会議がない場合は、新しい会議が開始されます。 進行中の会議がある場合、この値は無視されます。

  * **False**: 既定値 `UseMeetNow` は false です。つまり、ディープ リンクがステージに共有され、進行中の会議がない場合、予定表のポップアップが表示されます。 ただし、会議中は直接共有できます。

すべてのクエリ パラメーターが適切に URI エンコードされ、アプリ コンテキストを最終 URL で 2 回エンコードする必要があることを確認します。 以下に例を示します。

```json
var appContext= JSON.stringify({ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9cc80a93-1d41-4bcb-8170-4b9ec9e29fbb", "useMeetNow":false })
var encodedContext = encodeURIComponent(appcontext).replace(/'/g,"%27").replace(/"/g,"%22")
var encodedAppContext = encodeURIComponent(encodedContext).replace(/'/g,"%27").replace(/"/g,"%22")
```

ディープ リンクは、Teams Web または Teams デスクトップ クライアントから起動できます。

* **Teams Web**: 次の形式を使用して、Teams Web からディープ リンクを起動し、ステージ上でコンテンツを共有します。

    `https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`

    例: `https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |ディープ リンク|フォーマット|例|
    |---------|---------|---------|
    |アプリを共有して Teams カレンダーを開くには、UseMeeetNow が **false** の場合は既定です。|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |UseMeeetNow が **true** の場合、アプリを共有してインスタント会議を開始します。|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **チーム デスクトップ クライアント**: 次の形式を使用して、Teams デスクトップ クライアントからディープ リンクを起動し、ステージでコンテンツを共有します。

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    例: `msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |ディープ リンク|フォーマット|例|
    |---------|---------|---------|
    |アプリを共有して Teams カレンダーを開くには、UseMeeetNow が **false** の場合は既定です。|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |UseMeeetNow が **true** の場合、アプリを共有してインスタント会議を開始します。|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

クエリ パラメーターは次のとおりです。

* `deepLinkId`: テレメトリの関連付けに使用される任意の識別子。
* `fqdn`: `fqdn` は省略可能なパラメーターで、会議の適切な環境に切り替えて、ステージ上でアプリを共有するために使用できます。 特定の環境で特定のアプリ共有が発生するシナリオをサポートします。 既定値 `fqdn` はエンタープライズ URL で、可能な値は `Teams.live.com` Teams for Life、 `teams.microsoft.com`または `teams.microsoft.us`.

ステージにアプリ全体を共有するには、アプリ マニフェストで構成し`meetingSidePanel`、フレーム コンテキストとして[アプリ マニフェストを](../resources/schema/manifest-schema.md)参照する必要があります`meetingStage`。 それ以外の場合、会議の出席者はステージ上でコンテンツを表示できない可能性があります。

> [!NOTE]
> アプリが検証に合格するには、Web サイト、Web アプリ、またはアダプティブ カードからディープ リンクを作成するときに、 **会議で共有** を文字列またはコピーとして使用します。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|----------------|
|会議ステージのサンプル | 共同作業のために会議ステージでタブを表示するサンプル アプリ | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| 会議中の通知 | ボットを使用して会議内通知を実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| 会議中のドキュメント署名 | ドキュメント署名 Teams アプリを実装する方法を示します。 ステージ、Teams SSO、ユーザー固有のステージ ビューへの特定のアプリ コンテンツの共有が含まれます。 | [表示](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | 該当なし |

## <a name="see-also"></a>関連項目

* [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [Teams 会議用アプリ](teams-apps-in-meetings.md)
* [会議のタブを作成する](build-tabs-for-meeting.md)
* [会議チャット用の拡張可能な会話を構築する](build-extensible-conversation-for-meeting-chat.md)
* [匿名ユーザー用のアプリを作成する](build-apps-for-anonymous-user.md)
* [高度な会議 API](meeting-apps-apis.md)
* [カスタム Together モード シーン](~/apps-in-teams-meetings/teams-together-mode.md)
* [Live Share SDK](teams-live-share-overview.md)
