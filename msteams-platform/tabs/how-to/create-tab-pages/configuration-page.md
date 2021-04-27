---
title: 構成ページを作成する
author: laujan
description: 構成ページの作成方法
keywords: teams タブ グループ チャネル構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 0866d11442f79cee33d4454dbd4ed4d6b4b1a840
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019595"
---
# <a name="create-a-configuration-page"></a>構成ページを作成する

構成ページは、特殊な種類のコンテンツ [ページです](content-page.md)。 ユーザーは、構成ページを使用して Microsoft Teams アプリのいくつかの側面を構成し、その構成を次の一部として使用します。

* [チャネルまたはグループ チャット] タブ - ユーザーから情報を収集し、表示するコンテンツ ページ `contentUrl` の設定を行います。
* メッセージング [拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)
* [365 Officeコネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>チャネルまたはグループ チャット タブの構成

アプリケーションは [、Microsoft Teams JavaScript クライアント SDK を参照して呼び](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 出す必要があります `microsoft.initialize()` 。 また、使用する URL はセキュリティで保護された HTTPS エンドポイントで、クラウドから利用できる必要があります。 

### <a name="example"></a>例

構成ページの例を次の図に示します。 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

構成ページの対応するコードは、次のセクションに表示されます。

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

構成ページ **で [灰色の選択****]** または [赤の選択] ボタンを選択して、タブコンテンツを灰色または赤のアイコンで表示します。 

次の図は、灰色のアイコンでタブ コンテンツを表示します。

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

次の図は、赤いアイコンでタブ コンテンツを表示します。

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

相対ボタンを選択すると、トリガーまたは `saveGray()` `saveRed()` 、 がトリガーされ、次のコマンドが呼び出されます。

1. は `settings.setValidityState(true)` true に設定されます。
1. イベント `microsoftTeams.settings.registerOnSaveHandler()` ハンドラーがトリガーされます。
1. Teams **で** アップロードされたアプリの構成ページの [保存] ボタンが有効になります。

構成ページ コードは、構成要件が満たされ、インストールを続行できると Teams に通知します。 ユーザーが [保存] を **選択** すると、インターフェイスで定義されているパラメーター `settings.setSettings()` が設定 `Settings` されます。 詳細については、「設定インターフェイス」 [を参照してください](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)。 最後の手順で、コンテンツ URL が正常に解決されたことを示 `saveEvent.notifySuccess()` すために呼び出されます。

>[!NOTE]
>
>* 使用して保存ハンドラーを登録する場合は、コールバックを呼び出す必要があります。または構成の `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` 結果を示す必要があります。
>* 保存ハンドラーを登録しない場合、ユーザーが [保存] を選択すると、呼び `saveEvent.notifySuccess()` 出しが自動的に **行われます**。

### <a name="get-context-data-for-your-tab-settings"></a>タブ設定のコンテキスト データを取得する

お使いのタブでは、関連するコンテンツを表示するためにコンテキスト情報が必要になる場合があります。 コンテキスト情報は、よりカスタマイズされたユーザー エクスペリエンスを提供することで、タブの魅力をさらに強化します。

タブ構成に使用されるプロパティの詳細については、「Context [interface」を参照してください](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)。 次の 2 つの方法でコンテキスト データ変数の値を収集します。

1. マニフェストに URL クエリ文字列プレースホルダーを挿入します `configurationURL` 。

1. Teams [SDK メソッドを使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` します。

#### <a name="insert-placeholders-in-the-configurationurl"></a>プレースホルダーを `configurationUrl`

コンテキスト インターフェイスのプレースホルダーを基本に追加します `configurationUrl` 。 例:

##### <a name="base-url"></a>ベース URL

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>クエリ文字列を含む基本 URL

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

ページのアップロード後、Teams はクエリ文字列プレースホルダーを関連する値で更新します。 これらの値を取得して使用するロジックを構成ページに含める。 URL クエリ文字列の操作の詳細については、「MDN Web Docs の [URLSearchParams」](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) を参照してください。次の例では、プロパティから値を抽出する方法について説明 `configurationUrl` します。

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>関数を使用 `getContext()` してコンテキストを取得する

この `microsoftTeams.getContext((context) => {})` 関数は、呼び出されると [コンテキスト インターフェイス](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) を取得します。 この関数を構成ページに追加して、コンテキスト値を取得します。

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

 ユーザーにアプリの構成を許可する前に認証を行います。 それ以外の場合、コンテンツに認証プロトコルを持つソースが含まれる場合があります。 詳細については [、「Microsoft Teams タブでユーザーを認証する」を参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。コンテキスト情報を使用して、認証要求と承認ページ URL を作成します。
タブ ページで使用されているドメインはすべて、and 配列に一覧表示 `manifest.json` されます `validDomains` 。

## <a name="modify-or-remove-a-tab"></a>タブを変更または削除する

サポートされている削除オプションは、ユーザー エクスペリエンスをさらに改善します。 ユーザーがグループまたはチャネル タブを変更、再構成、または名前変更できるマニフェストのプロパティを `canUpdateConfiguration` `true` に設定します。また、アプリに削除オプション ページを含め、構成でプロパティの値を設定して、タブが削除されるとコンテンツに何が起こるかを `removeUrl` 示  `setSettings()` します。 ユーザーは個人用タブをアンインストールできますが、変更することはできません。 詳細については、「タブの [削除ページを作成する」を参照してください](~/tabs/how-to/create-tab-pages/removal-page.md)。

Microsoft Teams setSettings() の削除ページの構成:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a>モバイル クライアント

チャネルまたはグループ タブを Teams モバイル クライアントに表示する場合、構成にはプロパティの `setSettings()` 値が必要 `websiteUrl` です。 詳細については、「モバイルでの [タブのガイダンス」を参照してください](~/tabs/design/tabs-mobile.md)。
