---
title: 構成ページを作成する
author: laujan
description: 構成ページの作成方法
keywords: チーム タブ グループ チャネルの構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: aeab1cf96d1e875db79d9143fefd0e46348f585a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566685"
---
# <a name="create-a-configuration-page"></a>構成ページを作成する

構成ページは、特殊なタイプの [コンテンツ ページ です](content-page.md)。 ユーザーは、構成ページを使用してMicrosoft Teamsアプリのいくつかの側面を構成し、その構成を次の一部として使用します。

* チャンネルまたはグループチャットタブ: ユーザーから情報を収集し、 `contentUrl` 表示するコンテンツページの を設定します。
* [メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)。
* [Office 365 コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。

## <a name="configuring-a-channel-or-group-chat-tab"></a>チャネルまたはグループチャットタブの設定

アプリケーションは[、JavaScript クライアント SDK Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を参照し、 を呼び出す必要があります `microsoft.initialize()` 。 また、使用する URL は、セキュリティで保護された HTTPS エンドポイントで、クラウドから使用できる必要があります。 

### <a name="example"></a>例

構成ページの例を次の図に示します。 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

構成ページの対応するコードを次のセクションに示します。

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

設定ページで **[グレーを選択** ]または **[赤を選択** ]ボタンを選択して、タブの内容をグレーまたは赤のアイコンで表示します。 

次の図は、タブの内容を灰色のアイコンで表示します。

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

次の図は、タブの内容を赤いアイコンで表示します。

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

相対ボタンを選択すると、 `saveGray()` または `saveRed()` がトリガーされ、次が呼び出されます。

1. `settings.setValidityState(true)`は true に設定されます。
1. `microsoftTeams.settings.registerOnSaveHandler()`イベント ハンドラーがトリガーされます。
1. Teamsでアップロードされたアプリの構成ページの **[保存]** ボタンが有効になります。

構成ページ・コードは、構成要件が満たされ、インストールを続行できることをTeamsに通知します。 ユーザーが [ **保存**] を選択すると `settings.setSettings()` 、インターフェイスで定義されているとおりに のパラメータが設定されます `Settings` 。 詳細については[、「設定インターフェイス](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)」を参照してください。 最後の手順では、 `saveEvent.notifySuccess()` コンテンツ URL が正常に解決されたことを示すために呼び出されます。

>[!NOTE]
>
>* を使用して save ハンドラーを登録する場合 `microsoftTeams.settings.registerOnSaveHandler()` 、コールバックは、構成 `saveEvent.notifySuccess()` の結果を呼び出すか、または `saveEvent.notifyFailure()` その結果を示す必要があります。
>* 保存ハンドラを登録しない場合、 `saveEvent.notifySuccess()` ユーザーが **[ 保存**] を選択すると、呼び出しが自動的に行われます。

### <a name="get-context-data-for-your-tab-settings"></a>タブ設定のコンテキストデータを取得する

お使いのタブでは、関連するコンテンツを表示するためにコンテキスト情報が必要になる場合があります。 コンテキスト情報は、よりカスタマイズされたユーザーエクスペリエンスを提供することで、タブの魅力をさらに高めます。

タブ構成に使用されるプロパティの詳細については、「コンテキスト [インターフェイス](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)」を参照してください。 コンテキスト データ変数の値を次の 2 つの方法で収集します。

1. URL クエリ文字列プレースホルダーをマニフェストの `configurationURL` .

1. Teams [SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)メソッドを使用 `microsoftTeams.getContext((context) =>{})` します。

#### <a name="insert-placeholders-in-the-configurationurl"></a>プレースホルダを `configurationUrl`

コンテキスト インターフェイスのプレースホルダをベースに追加 `configurationUrl` します。 例:

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

ページがアップロードされると、Teamsはクエリ文字列のプレースホルダーを関連する値で更新します。 これらの値を取得して使用するロジックを構成ページに含めます。 URL クエリ文字列の操作の詳細については、「MDN Web ドキュメントの [URLSearchParams」](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) を参照してください。次の例では、プロパティから値を抽出する方法について説明 `configurationUrl` します。

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>関数を使用して `getContext()` コンテキストを取得する

`microsoftTeams.getContext((context) => {})`この関数は、呼び出されたときに[Context インターフェイス](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)を取得します。 コンテキスト値を取得するには、この関数を設定ページに追加します。

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

 ユーザーがアプリを構成できるようにする前に認証します。 それ以外の場合、コンテンツには、認証プロトコルを持つソースが含まれる可能性があります。 詳細については[、「Microsoft Teams タブでユーザーを認証する」を](~/tabs/how-to/authentication/auth-flow-tab.md)参照してください。コンテキスト情報を使用して、認証要求と承認ページ URL を作成します。
タブページで使用されているすべてのドメインが、 配列にリストされていることを確認します `manifest.json` `validDomains` 。

## <a name="modify-or-remove-a-tab"></a>タブを変更または削除する

サポートされている削除オプションは、ユーザー エクスペリエンスをさらに絞り込みます。 ユーザー `canUpdateConfiguration` `true` がグループまたはチャネル タブを変更、再構成、または名前変更できるように、マニフェストのプロパティを に設定します。また、アプリに削除オプション ページを含め、構成でプロパティの値を設定することで、タブが削除されたときにコンテンツに何が起こるか `removeUrl` を示  `setSettings()` します。 ユーザーは [個人] タブをアンインストールできますが、変更することはできません。 詳細については、「 [タブの削除ページを作成する](~/tabs/how-to/create-tab-pages/removal-page.md)」を参照してください。

Microsoft Teams削除ページの設定設定() 設定:

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

Teamsモバイル クライアントにチャンネルまたはグループ タブを表示する場合、 `setSettings()` 設定にはプロパティの値が必要 `websiteUrl` です。 詳細については、 [モバイルのタブのガイダンスを](~/tabs/design/tabs-mobile.md)参照してください。
