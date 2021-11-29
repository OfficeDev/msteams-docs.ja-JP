---
title: 構成ページを作成する
author: surbhigupta
description: コンテキスト データの取得、プレースホルダーの挿入、コード例を使用した認証など、設定用のチャネルまたはグループ チャットを構成する構成ページを作成する方法について説明します。
keywords: teams タブ グループ チャネル構成可能
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6e182c305950188e316c290e2c3d3fd5732adcf4
ms.sourcegitcommit: 85d0584877db21e2d3e49d3ee940d22675617582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/29/2021
ms.locfileid: "61216217"
---
# <a name="create-a-configuration-page"></a>構成ページを作成する

構成ページは、特殊な種類のコンテンツ [ページです](content-page.md)。 ユーザーは、構成ページを使用して Microsoft Teamsアプリのいくつかの側面を構成し、その構成を次の一部として使用します。

* [チャネルまたはグループ チャット] タブ: ユーザーから情報を収集し、表示するコンテンツ ページ `contentUrl` を設定します。
* メッセージング [拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)。
* [Office 365[コネクタ]](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configure-a-channel-or-group-chat-tab"></a>チャネルまたはグループ チャット タブを構成する

アプリケーションは JavaScript クライアント SDK Microsoft Teams[呼び出す](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)必要があります `microsoft.initialize()` 。 使用する URL は、セキュリティで保護された HTTPS エンドポイントで、クラウドから利用できる必要があります。

### <a name="example"></a>例

構成ページの例を次の図に示します。

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

次のコードは、構成ページの対応するコードの例です。

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
    ...
</body>
```

構成ページ **で [灰色の選択****]** または [赤の選択] ボタンを選択して、タブコンテンツを灰色または赤のアイコンで表示します。

次の図は、灰色のアイコンが選択された **タブ コンテンツ** を表示します。

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

次の図は、赤いアイコンが選択された **タブ コンテンツ** を表示します。

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

適切なボタンを選択すると、トリガー `saveGray()` または `saveRed()` トリガーが実行され、次のコマンドが呼び出されます。

* true `settings.setValidityState(true)` に設定します。 
* イベント `microsoftTeams.settings.registerOnSaveHandler()` ハンドラーがトリガーされます。
* **アプリ** の構成ページで保存が有効です。

構成ページ コードは、Teams要件が満たされ、インストールを続行できると通知します。 ユーザーが [保存] を **選択** すると、インターフェイスで定義されているパラメーター `settings.setSettings()` が設定 `Settings` されます。 詳細については、「設定インターフェイス」 [を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)。 `saveEvent.notifySuccess()` が呼び出され、コンテンツ URL が正常に解決されたことを示します。

>[!NOTE]
>
>* タイムアウト前に保存操作 (RegisterOnSaveHandler へのコールバック) を完了するには、30 秒かかります。 タイムアウト後に、汎用的なエラー メッセージが表示されます。
>* 使用して保存ハンドラーを登録する場合は、コールバックを呼び出す必要があります。または構成の `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` 結果を示す必要があります。
>* 保存ハンドラーを登録しない場合、ユーザーが [保存] を選択すると、呼び `saveEvent.notifySuccess()` 出しが自動的に **行われます**。

### <a name="get-context-data-for-your-tab-settings"></a>タブ設定のコンテキスト データを取得する

関連するコンテンツを表示するには、コンテキスト情報が必要です。 コンテキスト情報は、よりカスタマイズされたユーザー エクスペリエンスを提供することで、タブの魅力をさらに強化します。

タブ構成に使用されるプロパティの詳細については、「コンテキスト インターフェイス」 [を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)。 次の 2 つの方法でコンテキスト データ変数の値を収集します。

* マニフェストに URL クエリ文字列プレースホルダーを挿入します `configurationURL` 。

* SDK メソッド[Teams使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` します。

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

ページのアップロード後、Teams値を使用してクエリ文字列プレースホルダーを更新します。 これらの値を取得して使用するロジックを構成ページに含める。 URL クエリ文字列の操作の詳細については、「MDN Web Docs の [URLSearchParams」](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) を参照してください。次のコード例では、プロパティから値を抽出する方法を示 `configurationUrl` します。

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

この `microsoftTeams.getContext((context) => {})` 関数は、呼び出されると [コンテキスト インターフェイス](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) を取得します。

次のコードでは、この関数を構成ページに追加してコンテキスト値を取得する例を示します。

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

ユーザーにアプリの構成を許可する前に認証を行います。 それ以外の場合、コンテンツに認証プロトコルを持つソースが含まれる場合があります。 詳細については、「ユーザー認証」[タブでユーザーを認証するMicrosoft Teams参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。コンテキスト情報を使用して、認証要求と承認ページ URL を作成します。 タブ ページで使用されているドメインはすべて、and 配列に一覧表示 `manifest.json` されます `validDomains` 。

## <a name="modify-or-remove-a-tab"></a>タブを変更または削除する

ユーザーがチャネルまたはグループ タブを変更、再構成、または名前を変更できるマニフェストのプロパティを `canUpdateConfiguration` `true` に設定します。また、アプリに削除オプション ページを含め、構成でプロパティの値を設定して、タブが削除されるとコンテンツに何が起こるかを `removeUrl` 示  `setSettings()` します。 ユーザーは個人用タブをアンインストールできますが、変更することはできません。 詳細については、「タブの [削除ページを作成する」を参照してください](~/tabs/how-to/create-tab-pages/removal-page.md)。

Microsoft Teams `setSettings()` の構成ページ:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a>モバイル クライアント

チャネルまたはグループ タブをモバイル クライアントのTeamsする場合は、構成の値が `setSettings()` 必要です `websiteUrl` 。 詳細については、「モバイルでの [タブのガイダンス」を参照してください](~/tabs/design/tabs-mobile.md)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブの削除ページを作成する](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [コンテンツ ページを作成する](~/tabs/how-to/create-tab-pages/content-page.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
