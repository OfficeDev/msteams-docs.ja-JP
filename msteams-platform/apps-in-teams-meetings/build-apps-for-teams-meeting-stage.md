---
title: Teams 会議ステージ用のアプリを構築する
author: v-sdhakshina
description: Teams 会議ステージ用のアプリを構築し、API をステージに共有し、会議のステージにコンテンツを共有するためのディープ リンクを生成する方法について説明します。
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: ea5d7b57b9ee6344d34fcc6ed560936ac6109304
ms.sourcegitcommit: 4e355e22ddcd10ba9a8f37965c4f5c8fa04f5776
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/26/2022
ms.locfileid: "68701035"
---
# <a name="build-apps-for-teams-meeting-stage"></a>Teams 会議ステージ用のアプリを構築する

[ステージに共有] を使用すると、ユーザーは進行中の会議の会議側パネルから会議ステージにアプリを共有できます。 この共有は、パッシブ画面共有と比較して対話型で共同作業が可能です。

共有をステージに呼び出すために、ユーザーは会議側パネルの右上にある [ **Share to Stage]\(ステージに共有** \) アイコンを選択できます。 **[ステージに共有** ] アイコンは Teams クライアントにネイティブであり、アプリ全体を会議ステージに共有することを選択します。

## <a name="app-manifest-settings-for-apps-in-meeting-stage"></a>会議ステージのアプリのアプリ マニフェスト設定

アプリを会議ステージと共有するには、アプリ マニフェストの プロパティを `context` 次のように更新します。

```json
"context":[ 
    "meetingSidePanel", 
    "meetingStage" 
     ] 
```

## <a name="advanced-share-to-stage-apis"></a>高度な共有からステージング API

アプリ全体を会議ステージに共有すると、アプリの特定の部分を共有するほど役に立たないシナリオは多数あります。  

1. ブレーンストーミング アプリまたはホワイトボード アプリの場合、ユーザーは会議で特定のボードを共有し、アプリ全体をすべてのボードと共有したい場合があります。  

1. 医療アプリの場合、医師は画面上の X 線だけを患者と共有し、アプリ全体をすべての患者の記録や結果と共有したい場合があります。

1. ユーザーは、一度に 1 つのコンテンツ プロバイダー (YouTube など) のコンテンツを共有する場合と、ビデオ カタログ全体をステージに共有する場合があります。

このようなシナリオでユーザーを支援するために、Teams クライアント SDK 内の API をリリースしました。これにより、プログラムを使用して、会議側パネルのボタンからアプリの特定の部分の共有をステージに呼び出すことができます。

:::image type="content" source="../assets/images/apps-in-meetings/shared-meeting-stage-edit-review-component.png" alt-text="スクリーンショットは、会議ステージ ビューへの共有を示しています。":::

アプリの特定の部分を共有するには、次の API を使用します。

|メソッド| 説明| ソース|
|---|---|----|
|[**アプリ コンテンツをステージに共有する**](#share-app-content-to-stage-api)| 会議の会議側パネルから、アプリの特定の部分を会議ステージに共有します。 | [Microsoft Teams JavaScript ライブラリ SDK](/javascript/api/@microsoft/teams-js/meeting) |
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
|**callback**| String | はい | コールバックには、エラーと結果という 2 つのパラメーターが含まれています。 *エラー* には、エラーの種類 *SdkError* が含まれるか、共有が成功した場合は null が含まれます。 *結果* には、成功した共有がある場合は true 値、共有が失敗した場合は null を含めることができます。 |
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
| **501** | API は、現在のコンテキストではサポートされていません。|
| **1000** | アプリには、共有のステージングを許可するための適切なアクセス許可がありません。|

## <a name="get-app-content-stage-sharing-state-api"></a>アプリ コンテンツ ステージの共有状態を取得する API

`getAppContentStageSharingState` API を使用すると、会議ステージでアプリの共有に関する情報を取得できます。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、エラーと結果の 2 つのパラメーターが含まれています。 *エラー* には、エラーの場合はエラーの種類 *SdkError* が含まれ、共有が成功した場合は null が含まれます。 *結果* には、共有が成功した場合はオブジェクト、エラーの場合は null を含`IAppContentStageSharingState`めることができます。|

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
| **501** | API は、現在のコンテキストではサポートされていません。|
| **1000** | アプリには、共有のステージングを許可するための適切なアクセス許可がありません。|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>アプリ コンテンツ ステージの共有機能を取得する API

`getAppContentStageSharingCapabilities` API を使用すると、会議ステージに対して共有するためのアプリの機能を取得できます。

### <a name="query-parameter"></a>クエリ パラメーター

次の表に、クエリ パラメーターを示します。

|値|型|必須|説明|
|---|---|----|---|
|**callback**| String | はい | コールバックには、エラーと結果の 2 つのパラメーターが含まれています。 *エラー* には、エラーの種類 *SdkError* が含まれるか、共有が成功した場合は null が含まれます。 結果には、共有が成功した場合はオブジェクト、エラーの場合は null を含 `IAppContentStageSharingCapabilities` めることができます。|

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
| **501** | API は、現在のコンテキストではサポートされていません。|
| **1000** | アプリには、共有のステージングを許可するアクセス許可がありません。|

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>会議のステージにコンテンツを共有するためのディープ リンクを生成する

また、ディープ リンクを生成して、アプリを共有して、会議のステージングと開始または参加を行うこともできます。

> [!NOTE]
>
> * 現在、会議でコンテンツをステージに共有するためのディープ リンクは UX の機能強化を行っており、 [パブリック開発者プレビュー](~/resources/dev-preview/developer-preview-intro.md)でのみ使用できます。
> * 会議のステージにコンテンツを共有するためのディープ リンクは、Teams デスクトップ クライアントでのみサポートされています。

進行中の会議に参加しているユーザーがアプリでディープ リンクを選択すると、アプリがステージと共有され、アクセス許可のポップアップ ウィンドウが表示されます。 ユーザーは、参加者にアクセス権を付与してアプリと共同作業できます。

:::image type="content" source="../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="スクリーンショットは、アクセス許可のポップアップ ウィンドウを示す例です。":::

ユーザーが会議に参加していない場合、ユーザーは Teams 予定表にリダイレクトされ、会議に参加したり、インスタント会議を開始したりできます (今すぐ会議)。

:::image type="content" source="../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="スクリーンショットは、進行中の会議がない場合のポップアップ ウィンドウを示す例です。":::

ユーザーがインスタント会議 (今すぐ会議) を開始すると、参加者を追加してアプリと対話できます。

:::image type="content" source="../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="スクリーンショットは、参加者を追加するオプションとアプリと対話する方法を示す例です。":::

ステージでコンテンツを共有するためのディープ リンクを追加するには、アプリ コンテキストが必要です。 アプリ コンテキストを使用すると、Teams クライアントはアプリ マニフェストをフェッチし、ステージでの共有が可能かどうかを確認できます。 アプリ コンテキストの例を次に示します。

`{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

アプリ コンテキストのクエリ パラメーターは次のとおりです。

* `appID`: これは、アプリ マニフェストから取得できる ID です。
* `appSharingUrl`: ステージで共有する必要がある URL は、アプリ マニフェストで定義されている有効なドメインである必要があります。 URL が有効なドメインでない場合は、エラーの説明をユーザーに提供するエラー ダイアログが表示されます。
* `useMeetNow`: これには、true または false を指定できるブール値パラメーターが含まれます。
  * **True**: 値が `UseMeetNow` true の場合、進行中の会議がない場合は、新しい会議が開始されます。 会議が進行中の場合、この値は無視されます。

  * **False**: の既定値 `UseMeetNow` は false です。つまり、ディープ リンクがステージに共有され、会議が進行中でなければ、予定表のポップアップが表示されます。 ただし、会議中に直接共有できます。

すべてのクエリ パラメーターが適切に URI エンコードされ、アプリ コンテキストが最終的な URL で 2 回エンコードされている必要があることを確認します。 以下に例を示します。

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
    |アプリを共有して Teams 予定表を開くには、UseMeeetNow が **false の** 場合は既定です。|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |UseMeeetNow が true の場合に、アプリを共有してインスタント会議を開始 **します**。|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **チーム デスクトップ クライアント**: 次の形式を使用して、Teams デスクトップ クライアントからディープ リンクを起動し、ステージ上でコンテンツを共有します。

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    例: `msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |ディープ リンク|フォーマット|例|
    |---------|---------|---------|
    |アプリを共有して Teams 予定表を開くには、UseMeeetNow が **false の** 場合は既定です。|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |UseMeeetNow が true の場合に、アプリを共有してインスタント会議を開始 **します**。|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

クエリ パラメーターは次のとおりです。

* `deepLinkId`: テレメトリの関連付けに使用される任意の識別子。
* `fqdn`: `fqdn` は省略可能なパラメーターで、ステージ上でアプリを共有するための会議の適切な環境に切り替えるために使用できます。 特定の環境で特定のアプリ共有が発生するシナリオをサポートします。 の `fqdn` 既定値はエンタープライズ URL で、使用可能な値は `Teams.live.com` Teams for Life、、 `teams.microsoft.com`または `teams.microsoft.us`です。

アプリ全体をステージに共有するには、アプリ マニフェストで、フレーム コンテキストとして を構成 `meetingStage` する `meetingSidePanel` 必要があります。 [アプリ マニフェスト](../resources/schema/manifest-schema.md)に関するページを参照してください。 そうしないと、会議の出席者がステージ上のコンテンツを表示できない場合があります。

> [!NOTE]
> アプリが検証に合格するには、Web サイト、Web アプリ、アダプティブ カードからディープ リンクを作成するときに、文字列またはコピーとして **会議で共有** を使用します。

## <a name="build-an-in-meeting-document-signing-app"></a>会議内ドキュメント署名アプリを構築する

会議参加者がリアルタイムでドキュメントに署名できるようにするための会議内アプリを構築できます。 1 つのセッションでドキュメントのレビューと署名を容易にします。 参加者は、現在のテナント ID を使用してドキュメントに署名できます。

会議内署名アプリを使用すると、次のことができます。

- 会議中に確認するドキュメントを追加する
- メイン ステージにレビューするドキュメントを共有する
- 署名者の ID を使用してドキュメントに署名する

参加者は、購買契約や発注書などのドキュメントを確認して署名できます。

:::image type="content" source="../assets/images/sbs-inmeeting-doc-signing/final-output.png" alt-text="会議内ドキュメント署名アプリ":::

会議中に、次の参加者ロールが関与する場合があります。

- **ドキュメント作成者**: このロールは、レビューおよび署名する独自のドキュメントを追加できます。
- **署名者**: このロールは、レビューされたドキュメントに署名できます。
- **閲覧者**: このロールは、会議に追加されたドキュメントを表示できます。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|----------------|
|会議ステージのサンプル | 共同作業のために会議ステージでタブを表示するサンプル アプリ | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| 会議中の通知 | ボットを使用して会議内通知を実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| 会議内ドキュメントの署名 | Teams アプリに署名するドキュメントを実装する方法を示します。 特定のアプリ コンテンツをステージに共有する、Teams SSO、ユーザー固有のステージ ビューが含まれます。 | [表示](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | 該当なし |

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

詳細 [なガイド](../sbs-inmeeting-document-signing.yml) に従って、会議内ドキュメント署名アプリを作成します。

## <a name="see-also"></a>関連項目

* [タブの Teams 認証フロー](../tabs/how-to/authentication/auth-flow-tab.md)
* [Teams 会議用アプリ](teams-apps-in-meetings.md)
* [会議用のビルド タブ](build-tabs-for-meeting.md)
* [会議チャット用の拡張可能な会話を構築する](build-extensible-conversation-for-meeting-chat.md)
* [匿名ユーザー向けのアプリを構築する](build-apps-for-anonymous-user.md)
* [高度な会議 API](meeting-apps-apis.md)
* [カスタム Together モード シーン](~/apps-in-teams-meetings/teams-together-mode.md)
* [Live Share SDK](teams-live-share-overview.md)
