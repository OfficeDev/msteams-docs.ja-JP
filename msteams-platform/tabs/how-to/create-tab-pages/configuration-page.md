---
title: 構成ページを作成する
author: surbhigupta
description: コンテキスト データの取得、プレースホルダーの挿入、コード例を使用した認証など、設定用のチャネルまたはグループ チャットを構成する構成ページを作成する方法について説明します。
keywords: teams タブ グループ チャネル構成可能
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: ed4f60e3071b882f73662c0b666f87c484b4e77b
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398730"
---
# <a name="create-a-configuration-page"></a>構成ページを作成する

構成ページは、特別な種類のコンテンツ [ページです](content-page.md)。 ユーザーは、構成ページを使用して Microsoft Teamsアプリのいくつかの側面を構成し、その構成を次の一部として使用します。

* [チャネルまたはグループ チャット] タブ: ユーザーから情報を収集 `contentUrl` し、表示するコンテンツ ページを設定します。
* メッセージング [拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)。
* [[Office 365コネクタ]](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configure-a-channel-or-group-chat-tab"></a>チャネルまたはグループ チャット タブを構成する

アプリケーションは、[JavaScript クライアント SDK Microsoft Teams呼び出しを](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)参照する必要があります`microsoft.initialize()`。 使用する URL は、セキュリティで保護された HTTPS エンドポイントで、クラウドから利用できる必要があります。

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

適切なボタンを選択すると、トリガーまたは`saveGray()``saveRed()`トリガーが実行され、次のコマンドが呼び出されます。

* true に `settings.setValidityState(true)` 設定します。
* イベント `microsoftTeams.settings.registerOnSaveHandler()` ハンドラーがトリガーされます。
* **アプリ** の構成ページで保存が有効です。

構成ページ コードは、構成Teamsが満たされ、インストールを続行できると通知します。 ユーザーが [保存] を **選択** すると、インターフェイスで `settings.setSettings()` 定義されているパラメーターが設定 `Settings` されます。 詳細については、「設定インターフェイス [」を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)。 `saveEvent.notifySuccess()` が呼び出され、コンテンツ URL が正常に解決されたことを示します。

>[!NOTE]
>
>* タイムアウト前に保存操作 (RegisterOnSaveHandler へのコールバック) を完了するには、30 秒かかります。 タイムアウト後に、汎用的なエラー メッセージが表示されます。
>* 使用して保存ハンドラーを登録する`microsoftTeams.settings.registerOnSaveHandler()`場合は、コールバックを`saveEvent.notifySuccess()``saveEvent.notifyFailure()`呼び出す必要があります。または構成の結果を示す必要があります。
>* 保存ハンドラーを登録しない場合、ユーザー `saveEvent.notifySuccess()` が [保存] を選択すると、呼び出しが自動的に行 **われます**。

### <a name="get-context-data-for-your-tab-settings"></a>タブ設定のコンテキスト データを取得する

関連するコンテンツを表示するには、コンテキスト情報が必要です。 コンテキスト情報は、よりカスタマイズされたユーザー エクスペリエンスを提供することで、タブの魅力をさらに強化します。

タブ構成に使用されるプロパティの詳細については、「コンテキスト インターフェイス」 [を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)。 次の 2 つの方法でコンテキスト データ変数の値を収集します。

* マニフェストに URL クエリ文字列プレースホルダーを挿入します `configurationURL`。

* SDK メソッド[Teams使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)`microsoftTeams.getContext((context) =>{})`します。

#### <a name="insert-placeholders-in-the-configurationurl"></a>プレースホルダーを `configurationUrl`

コンテキスト インターフェイスのプレースホルダーを基本に追加します `configurationUrl`。 次に例を示します。

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

ページのアップロード後、Teams値を使用してクエリ文字列プレースホルダーを更新します。 これらの値を取得して使用するロジックを構成ページに含める。 URL クエリ文字列の操作の詳細については、「MDN Web Docs の [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 」を参照してください。次のコード例では、プロパティから値を抽出する方法を示 `configurationUrl` します。

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

この関数 `microsoftTeams.getContext((context) => {})` は、呼び出されると [コンテキスト インターフェイス](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) を取得します。

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

ユーザーにアプリの構成を許可する前に認証を行います。 それ以外の場合、コンテンツに認証プロトコルを持つソースが含まれる場合があります。 詳細については、「ユーザー認証」[タブでユーザーを認証するMicrosoft Teamsしてください](~/tabs/how-to/authentication/auth-flow-tab.md)。コンテキスト情報を使用して、認証要求と承認ページ URL を作成します。 タブ ページで使用されているドメインはすべて、and 配列に一覧表示されます`manifest.json``validDomains`。

## <a name="modify-or-remove-a-tab"></a>タブを変更または削除する

ユーザーがチャネルまたはグループ タブ`canUpdateConfiguration``true`を変更、再構成、または名前を変更できるマニフェストのプロパティをに設定します。また、アプリに削除オプション `removeUrl` ページを含め、構成でプロパティの値を設定して、タブが削除されるとコンテンツに何が起こるかを示`setSettings()`します。 ユーザーは個人用タブをアンインストールできますが、変更することはできません。 詳細については、「タブの [削除ページを作成する」を参照してください](~/tabs/how-to/create-tab-pages/removal-page.md)。

`setSettings()` Microsoft Teamsの構成ページ:

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

チャネルまたはグループ タブをモバイル クライアント`setSettings()`のTeamsする場合は、構成の値が必要です`websiteUrl`。 詳細については、「モバイル上の [タブのガイダンス」を参照してください](~/tabs/design/tabs-mobile.md)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブの削除ページを作成する](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [コンテンツ ページを作成する](~/tabs/how-to/create-tab-pages/content-page.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
