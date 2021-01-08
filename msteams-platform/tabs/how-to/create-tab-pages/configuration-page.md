---
title: 構成ページを作成する
author: laujan
description: 構成ページを作成する方法
keywords: teams タブ グループ チャネルを構成可能
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: c041c311245bb5bfc5e2655ef8d596b2839fdb70
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731966"
---
# <a name="create-a-configuration-page"></a>構成ページを作成する

構成ページは、ユーザーが Teams[](content-page.md)アプリの一部の側面を構成できる特別な種類のコンテンツ ページです。 通常、これらは次の一部として使用されます。

* チャネルまたはグループ チャット タブ - 構成ページでは、ユーザーから情報を収集し、表示するコンテンツ `contentUrl` ページの設定を行えます。
* メッセージング [拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)
* Office [365 コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>チャネルまたはグループ チャット タブの構成

構成ページは、コンテンツ ページのレンダリング方法を通知します。 アプリケーションは、Microsoft Teams JavaScript クライアント SDK と呼 [び出しを](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 参照する必要があります `microsoft.initialize()` 。 さらに、URL はセキュリティで保護された HTTPS エンドポイントで、クラウドから利用できる必要があります。 構成ページの例を次に示します。

```html
<head>
<script src='https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
</head>
    <body>
        <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
        <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
        <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

        <script>
            microsoftTeams.initialize();
            let saveGray = () => {
                microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                    microsoftTeams.settings.setSettings({
                        websiteUrl: "https://yourWebsite.com",
                        contentUrl: "https://yourWebsite.com/gray",
                        entityId: "grayIconTab",
                        suggestedDisplayName: "MyNewTab"
                    });
                    saveEvent.notifySuccess();
                });
            }
            let saveRed = () => {
                microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                    microsoftTeams.settings.setSettings({
                        websiteUrl: "https://yourWebsite.com",
                        contentUrl: "https://yourWebsite.com/red",
                        entityId: "redIconTab",
                        suggestedDisplayName: "MyNewTab"
                    });
                    saveEvent.notifySuccess();
                });
            }

            let gr = document.getElementById("gray").style;
            let rd = document.getElementById("red").style;

            const colorClickGray = () => {
                gr.display = "block";
                rd.display = "none";
                microsoftTeams.settings.setValidityState(true);
                saveGray()
            }

            const colorClickRed = () => {
                rd.display = "block";
                gr.display = "none";
                microsoftTeams.settings.setValidityState(true);
                saveRed();
            }
        </script>
    </body>
...
```

ここでは、ユーザーに [灰色の選択] または[赤の選択] の 2 つのオプション ボタンが表示され、タブのコンテンツが赤または灰色のアイコンで表示されます。 相対ボタンを選択すると、次のイベント `saveGray()` `saveRed()` が発生または起動します。

1. true `settings.setValidityState(true)` に設定されます。
1. イベント `microsoftTeams.settings.registerOnSaveHandler()` ハンドラーがトリガーされます。
1. Teams **に** アップロードされたアプリの構成ページの [保存] ボタンが有効になります。

このコードを使用すると、構成要件が満たされ、インストールを続行できると Teams に知らされます。 [ **保存**] では、現在のインスタンスに対して、インターフェイスによって定義されたパラメーター `settings.setSettings()` `Settings` が設定されます。 詳細については、「設定インターフェイス」 [を参照してください](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)。 最後に、 `saveEvent.notifySuccess()` コンテンツ URL が正常に解決されたことを示すために呼び出されます。

>[!NOTE]
>
>* 保存ハンドラーが使用して登録されている場合は、コールバックが呼び出す必要があります。または、構成の `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` 結果を示す必要があります。
>* 保存ハンドラーが登録されていない場合、ユーザーが [保存] ボタンを選択するとすぐに呼び出 `saveEvent.notifySuccess()` しが **自動的に行** われます。

### <a name="get-context-data-for-your-tab-settings"></a>タブ設定のコンテキスト データを取得する

タブには、関連するコンテンツを表示するためにコンテキスト情報が必要な場合があります。 コンテキスト情報は、よりカスタマイズされたユーザー エクスペリエンスを提供することで、タブの魅力をさらに高める可能性があります。

Teams コンテキスト [インターフェイスは](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 、タブ構成に使用できるプロパティを定義します。 コンテキスト データ変数の値は、次の 2 つの方法で収集できます。

1. マニフェストに URL クエリ文字列プレースホルダーを挿入します `configurationURL` 。

1. Teams [SDK メソッドを使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{}` します。

#### <a name="insert-placeholders-in-the-configurationurl"></a>プレースホルダーの挿入 `configurationURL`

コンテキスト インターフェイスのプレースホルダーをベースに追加できます `configurationUrl` 。 例:

##### <a name="base-url"></a>ベース URL

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>クエリ文字列を含むベース URL

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

ページがアップロードされると、クエリ文字列プレースホルダーが Teams によって関連する値で更新されます。 これらの値を取得して使用するロジックを構成ページに含めることができます。 URL クエリ文字列の操作について詳しくは、MDN Web ドキュメントの [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) をご覧ください。上記のプロパティから値を抽出する方法の例を次に示 `configurationURL` します。

```html
<script>
   microsoftTeams.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

### <a name="use-the-getcontext-function-to-retrieve-context"></a>関数を `getContext()` 使用してコンテキストを取得する

呼び出されると、 `microsoftTeams.getContext((context) => {})` この関数はコンテキスト インターフェイスを [取得します](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)。 この関数を構成ページに追加して、コンテキスト値を取得できます。

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script>
    microsoftTeams.getContext((context) =>{
        let userId = document.getElementById('user');
        userId.innerHTML = context.userPrincipalName;
    });
</script>
...
```

## <a name="context-and-authentication"></a>コンテキストと認証

ユーザーにアプリの構成を許可する前に認証が必要になる場合や、コンテンツに独自の認証プロトコルを持つソースが含まれる場合があります。 「Microsoft [Teams タブのコンテキスト情報でユーザー](~/tabs/how-to/authentication/auth-flow-tab.md) を認証する」を参照して、認証要求と承認ページの URL を作成できます。
タブ ページで使用されているドメインすべてが配列に表示されます `manifest.json` `validDomains` 。

## <a name="modify-or-remove-a-tab"></a>タブを変更または削除する

サポートされている削除オプションにより、ユーザー エクスペリエンスをさらに調整できます。 ユーザーがグループ/チャネル タブを変更、再構成、または名前変更するには、マニフェストのプロパティを設定 `canUpdateConfiguration` します `true` 。  さらに、アプリに削除オプション ページを含め、構成でプロパティの値を設定することで、タブが削除された場合のコンテンツの処理 `removeUrl` を指定できます  `setSettings()` (下記を参照)。 [個人用] タブは変更できませんが、ユーザーはアンインストールできます。 詳細については、「タブの削除 [ページを作成する」を参照してください](~/tabs/how-to/create-tab-pages/removal-page.md)。

## <a name="mobile-clients"></a>モバイル クライアント

Teams モバイル クライアントに [チャネル/グループ] タブを表示するように選択した場合は、`setSettings()` 構成には `websiteUrl` プロパティの値を設定する必要があります (下記参照)。 モバイルの [タブに関するガイダンスを参照してください](~/tabs/design/tabs-mobile.md)。

削除ページやモバイル クライアント用の Microsoft Teams setSettings() 構成:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
