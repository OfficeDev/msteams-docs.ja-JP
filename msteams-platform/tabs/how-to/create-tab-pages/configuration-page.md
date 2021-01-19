---
title: 構成ページを作成する
author: laujan
description: 構成ページを作成する方法
keywords: teams タブ グループ チャネルを構成可能
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2544454fd06348fa41269f3a8fd57cc71a07d140
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886738"
---
# <a name="create-a-configuration-page"></a>構成ページを作成する

構成ページは、特別な種類の [コンテンツ ページです](content-page.md)。 ユーザーは、構成ページを使用して Microsoft Teams アプリのいくつかの側面を構成し、次の一部としてその構成を使用します。

* チャネルまたはグループ チャット タブ - ユーザーから情報を収集し、表示するコンテンツ `contentUrl` ページの設定を行います。
* メッセージング [拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)
* Office [365 コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>チャネルまたはグループ チャット タブの構成

アプリケーションは [、Microsoft Teams JavaScript クライアント SDK と呼び出しを](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 参照する必要があります `microsoft.initialize()` 。 また、使用する URL はセキュリティで保護された HTTPS エンドポイントで、クラウドから利用できる必要があります。 次のコードは、構成ページの例です。

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

構成ページで **[灰色の選択]** または [ **赤** の選択] ボタンを選択して、タブのコンテンツを灰色または赤のアイコンで表示します。 相対ボタンを選択すると、次のどちらか `saveGray()` または `saveRed()` 実行され、次のコマンドが呼び出されます。

1. true `settings.setValidityState(true)` に設定されます。
1. イベント `microsoftTeams.settings.registerOnSaveHandler()` ハンドラーがトリガーされます。
1. Teams **に** アップロードされたアプリの構成ページの [保存] ボタンが有効になります。

構成ページのコードは、構成要件が満たされ、インストールを続行できると Teams に通知します。 ユーザーが [保存 **]** を選択すると、インターフェイスで定義されているパラメーター `settings.setSettings()` が設定 `Settings` されます。 詳細については、「設定インターフェイス」 [を参照してください](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)。 最後の手順では `saveEvent.notifySuccess()` 、コンテンツ URL が正常に解決されたことを示すために呼び出されます。

>[!NOTE]
>
>* 保存ハンドラーを使用して登録する場合は、コールバックが呼び出す必要があります。また、構成の `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` 結果を示す必要があります。
>* 保存ハンドラーを登録しない場合、ユーザーが [保存] を選択すると、呼び出 `saveEvent.notifySuccess()` しが自動的に行 **われます**。

### <a name="get-context-data-for-your-tab-settings"></a>タブ設定のコンテキスト データを取得する

タブには、関連するコンテンツを表示するためにコンテキスト情報が必要な場合があります。 コンテキスト情報は、よりカスタマイズされたユーザー エクスペリエンスを提供することで、タブの魅力をさらに高めるものになります。

タブ構成に使用されるプロパティの詳細については、「コンテキスト インターフェイス」を [参照してください](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)。 コンテキスト データ変数の値は、次の 2 つの方法で収集します。

1. マニフェストに URL クエリ文字列プレースホルダーを挿入します `configurationURL` 。

1. Teams [SDK メソッドを使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` します。

#### <a name="insert-placeholders-in-the-configurationurl"></a>プレースホルダーの挿入 `configurationUrl`

コンテキスト インターフェイスプレースホルダーをベースに追加します `configurationUrl` 。 以下に例を示します。

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

ページのアップロード後、Teams はクエリ文字列プレースホルダーを関連する値で更新します。 これらの値を取得して使用するロジックを構成ページに含める。 URL クエリ文字列の操作について詳しくは、MDN Web Docs の [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) に関するページをご覧ください。次の例では、プロパティから値を抽出する方法について説明 `configurationUrl` します。

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

 ユーザーにアプリの構成を許可する前に認証を行います。 そうしないと、コンテンツに認証プロトコルを持つソースが含まれる場合があります。 詳細については [、「Microsoft Teams タブでユーザーを認証する」を参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。コンテキスト情報を使用して、認証要求と承認ページの URL を作成します。
タブ ページで使用されているドメインすべてが、配列と一覧に表示 `manifest.json` されます `validDomains` 。

## <a name="modify-or-remove-a-tab"></a>タブを変更または削除する

サポートされている削除オプションは、ユーザー エクスペリエンスをさらに改良します。 ユーザーがグループまたはチャネル タブを変更、再構成、または名前変更できるマニフェストのプロパティを `canUpdateConfiguration` `true` 設定します。また、アプリに削除オプション ページを含め、構成内のプロパティの値を設定することで、タブが削除されるとコンテンツに何が起こるかを `removeUrl` 示  `setSettings()` します。 詳細については、「モバイル クライアント」 [を参照してください](#mobile-clients)。 ユーザーは [個人用] タブをアンインストールできますが、変更することはできません。 詳細については、「タブの削除 [ページを作成する」を参照してください](~/tabs/how-to/create-tab-pages/removal-page.md)。

## <a name="mobile-clients"></a>モバイル クライアント

Teams モバイル クライアントにチャネルまたはグループ タブを表示する場合、構成にはプロパティの値 `setSettings()` が必要 `websiteUrl` です。 詳細については、モバイルの [タブに関するガイダンスを参照してください](~/tabs/design/tabs-mobile.md)。

削除ページまたはモバイル クライアント用の Microsoft Teams setSettings() 構成:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
