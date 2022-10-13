---
title: 構成ページを作成する
author: surbhigupta
description: ユーザーから情報を収集する構成ページを作成します。 また、Microsoft Teams タブのコンテキスト データを取得し、認証について理解し、タブを変更または削除します。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 5db345ce0653407b750afa96e6f82fff949f98f6
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560660"
---
# <a name="create-a-configuration-page"></a>構成ページを作成する

構成ページは、特別な種類の [コンテンツ ページ](content-page.md)です。 ユーザーは、構成ページを使用して Microsoft Teams アプリのいくつかの側面を構成し、その構成を次の一部として使用します。

* [チャネルまたはグループ チャット] タブ: ユーザーから情報を収集し、表示するコンテンツ ページの `contentUrl` を設定します。
* [メッセージ拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)。
* [Office 365 コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="configure-a-channel-or-group-chat-tab"></a>チャネルまたはグループチャット タブを構成する

アプリケーションは、[ Microsoft Teams JavaScript クライアントSDK](/javascript/api/overview/msteams-client) を参照し、`app.initialize()` を呼び出す必要があります。 使用される URL は、セキュリティで保護された HTTPS エンドポイントである必要があり、クラウドから使用できます。

### <a name="example"></a>例

構成ページの例を次の図に示します。

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

次のコードは、構成ページに対応するコードの例です。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<head>
    <script src="https://res.cdn.office.net/teams-js/2.2.0/js/MicrosoftTeams.min.js" 
      integrity="sha384yBjE++eHeBPzIg+IKl9OHFqMbSdrzY2S/LW3qeitc5vqXewEYRWegByWzBN/chRh" 
      crossorigin="anonymous" >
    </script>
<body>
    <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
    <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
    <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

    <script>
        await microsoftTeams.app.initialize();
        let saveGray = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                const configPromise = pages.config.setConfig({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/gray",
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                configPromise.
                    then((result) => {saveEvent.notifySuccess()}).
                    catch((error) => {saveEvent.notifyFailure("failure message")});
            });
        }

        let saveRed = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                const configPromise = pages.config.setConfig({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/red",
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                configPromise.
                    then((result) => {saveEvent.notifySuccess();}).
                    catch((error) => {saveEvent.notifyFailure("failure message")});
            });
        }

        let gr = document.getElementById("gray").style;
        let rd = document.getElementById("red").style;

        const colorClickGray = () => {
            gr.display = "block";
            rd.display = "none";
            microsoftTeams.pages.config.setValidityState(true);
            saveGray()
        }

        const colorClickRed = () => {
            rd.display = "block";
            gr.display = "none";
            microsoftTeams.pages.config.setValidityState(true);
            saveRed();
        }
    </script>
    ...
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***
タブのコンテンツを灰色または赤色のアイコンで表示するには、構成ページで **[灰色を選択]** または **[赤色を選択]** ボタンを選択します。

次の図は、**[灰色]** のアイコンが選択されたタブコンテンツを表示します。

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

次の図は、**[赤]** のアイコンが選択されたタブコンテンツを表示します。

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

適切なボタンを選択すると、`saveGray()` または `saveRed()` のいずれかがトリガーされ、以下が呼び出されます。

* `pages.config.setValidityState(true)` を true に設定します。
* `pages.config.registerOnSaveHandler()`イベント ハンドラーがトリガーされます。
* アプリの構成ページで **[保存]** が有効になっています。

構成ページ コードは、構成要件が満たされ、インストールを続行できることを Teams に通知します。 ユーザーが **[保存]** を選択すると、`Config` インターフェースで定義されているように `pages.config.setConfig()` のパラメーターが設定されます。 詳細については、「 [構成インターフェイス」を](/javascript/api/@microsoft/teams-js/pages.config?)参照してください。 `saveEvent.notifySuccess()` は、コンテンツ URL が正常に解決されたことを示すために呼び出されます。

>[!NOTE]
>
>* タイムアウトまでに保存操作 (コールバック `registerOnSaveHandler`先) を完了するまでに 30 秒かかります。 タイムアウト後、一般的なエラー メッセージが表示されます。
>* `registerOnSaveHandler()` を使用して保存ハンドラーを登録する場合、コールバックは `saveEvent.notifySuccess()` または `saveEvent.notifyFailure()` を呼び出して、構成の結果を示す必要があります。
>* 保存ハンドラーを登録しない場合、ユーザーが **[保存]** を選択すると、`saveEvent.notifySuccess()` 呼び出しが自動的に行われます。
>* 一意 `entityId`であることを確認します。 タブの最初のインスタンスへのリダイレクトを複製 `entityId` します。

### <a name="get-context-data-for-your-tab-settings"></a>タブのコンテキストを取得する

お使いのタブでは、関連するコンテンツを表示するためにコンテキスト情報が必要になる場合があります。 コンテキスト情報は、よりカスタマイズされたユーザー エクスペリエンスを提供することで、タブの魅力をさらに高めます。

タブ構成に使用されるプロパティの詳細については、 [コンテキスト インターフェイス](/javascript/api/@microsoft/teams-js/app.context?view=msteams-client-js-latest&preserve-view=true)を参照してください。 コンテキスト データ変数の値を次の 2 つの方法で収集します。

* マニフェストの `configurationURL` に URL クエリ文字列プレースホルダーを挿入します。

* [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `app.getContext()` メソッドを使用します。

#### <a name="insert-placeholders-in-the-configurationurl"></a>`configurationUrl` にプレースホルダーを挿入します。

ベース `configurationUrl` にコンテキスト インターフェイス プレースホルダーを追加します。 次に例を示します。

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

ページのアップロード後、Teams クエリ文字列プレースホルダーが関連する値で更新されます。 これらの値を取得して使用するには、構成ページにロジックを含めます。 URL クエリ文字列の操作の詳細については、MDN Web Docs の [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) を参照してください。 次のコード例は、`configurationUrl` プロパティから値を抽出する方法を示しています。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<script>
   await microsoftTeams.app.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***

### <a name="use-the-getcontext-function-to-retrieve-context"></a>関数を `getContext()` 使用してコンテキストを取得する

この関数は `app.getContext()` 、 [コンテキスト インターフェイス](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest&preserve-view=true) オブジェクトを使用して解決する Promise を返します。

次のコードは、この関数を構成ページに追加してコンテキスト値を取得する例を示しています。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script type="module">
    import {app} from 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js';
    const contextPromise = app.getContext();
    contextPromise.
        then((context) => {
            let userId = document.getElementById('user');
            userId.innerHTML = context.user.userPrincipalName;
        }).
        catch((error) => {/*Unsuccessful operation*/});
</script>
...
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***

## <a name="context-and-authentication"></a>コンテキストと認証

ユーザーにアプリの構成を許可する前に認証します。 そうしないと、コンテンツに認証プロトコルを持つソースが含まれる可能性があります。 詳細については、「[Microsoft Teams タブでユーザーを認証する](~/tabs/how-to/authentication/auth-flow-tab.md)」を参照してください。コンテキスト情報を使用して、認証要求と承認ページ URL を作成します。 タブ ページで使用されているすべてのドメインが `manifest.json` および `validDomains` 配列にリストされていることを確認してください。

## <a name="modify-or-remove-a-tab"></a>タブを変更または削除する

マニフェストの `canUpdateConfiguration` プロパティ `true`を . これにより、ユーザーはチャネルまたはグループ タブを変更または再構成できます。タブの名前は、Teams ユーザー インターフェイスを使用してのみ行うことができます。 タブが削除されたときのコンテンツへの影響についてユーザーに通知します。 これを行うには、アプリに [削除オプション] ページを含め、(以前の) 構成でプロパティの`setConfig()`値`removeUrl`を`setSettings()`設定します。 ユーザーは個人用タブをアンインストールできますが、変更することはできません。 詳細については、「[タブの削除ページを作成する](~/tabs/how-to/create-tab-pages/removal-page.md)」を参照してください。

削除ページ用`setSettings()`の Microsoft Teams `setConfig()` (以前の) 構成:

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
import { pages } from "@microsoft/teams-js";
const configPromise = pages.config.setConfig({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
configPromise.
    then((result) => {/*Successful operation*/).
    catch((error) => {/*Unsuccessful operation*/});
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

***

## <a name="mobile-clients"></a>モバイル クライアント

Teams モバイル クライアントに、チャネルまたはグループ タブを表示するように選択した場合は、`setConfig()`の構成には`websiteUrl`の値を設定する必要があります。 詳細については、「[モバイル上のタブに関するガイダンス](~/tabs/design/tabs-mobile.md)」を参照してください。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [タブのコンテンツ ページを作成する](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="see-also"></a>関連項目

* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネル] または [グループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [コンテンツ ページを作成する](~/tabs/how-to/create-tab-pages/content-page.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
