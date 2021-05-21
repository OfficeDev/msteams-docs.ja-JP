---
title: Office 365 コネクタ
description: コネクタの使用を開始するOffice 365説明Microsoft Teams
keywords: Teams o365 コネクタ
localization_priority: Normal
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 9eaaedf88d907dd7a7422068ab5d20450345f0e7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566811"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>ユーザー Office 365コネクタのMicrosoft Teams

>アプリMicrosoft Teamsを使用すると、既存のコネクタコネクタをOffice 365したり、新しいコネクタをビルドして新しいコネクタにMicrosoft Teams。 詳細については [、「独自のコネクタをビルド](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) する」を参照してください。

## <a name="adding-a-connector-to-your-teams-app"></a>コネクタをアプリにTeamsする

登録済みのコネクタを Teams アプリ パッケージの一部として配布できます。 スタンドアロン ソリューションとしても、Teams でエクスペリエンスが有効にしている機能の 1 つでも、AppSource[](~/concepts/build-and-test/apps-package.md)申請[](~/concepts/deploy-and-publish/apps-publish.md)の一部としてコネクタをパッケージ化して発行したり、Teams 内でアップロードするためにユーザーに直接提供することもできます。 [](~/concepts/extensibility-points.md)

コネクタを配布するには、コネクタ開発者ダッシュボードを使用して [登録する必要があります](https://outlook.office.com/connectors/home/login/#/publish)。 既定では、コネクタが登録された後、コネクタは、コネクタとコネクタを含む、それらをサポートしているすべての Office 365 製品で動作OutlookとTeams。 そう _ではなく、コネクタ_ を作成する必要がある場合は、Microsoft Teams App Submissions で直接Microsoft Teams [問い合わせください](mailto:teamsubm@microsoft.com)。

> [!IMPORTANT]
> コネクタ開発者ダッシュボード **で [** 保存] を選択すると、コネクタが登録されます。 AppSource でコネクタを発行する場合は、「アプリを AppSource に発行する」[のMicrosoft Teamsに従います](~/concepts/deploy-and-publish/apps-publish.md)。 AppSource でアプリを発行するのではなく、組織にのみ直接配布する場合は、組織に発行[します。](#publish-connectors-for-your-organization) 組織にのみ発行する場合は、Connector ダッシュボードでそれ以上の操作は必要ありません。

### <a name="integrating-the-configuration-experience"></a>構成エクスペリエンスの統合

ユーザーは、クライアントから離れることなく、コネクタ構成Teamsします。 このエクスペリエンスを実現するために、Teamsページを iframe に直接埋め込む必要があります。 操作のシーケンスは次のとおりです。

1. ユーザーがコネクタをクリックして構成プロセスを開始します。
2. Teams構成エクスペリエンスを一行に読み込む必要があります。
3. ユーザーは Web エクスペリエンスと対話して構成を完了します。
4. ユーザーが "Save" を押すと、コード内のコールバックがトリガーされます。
5. コードは、Webhook 設定を取得して保存イベントを処理します (以下に説明します)。 その後、後でイベントを投稿するために Webhook を保存する必要があります。

既存の Web 構成エクスペリエンスを再利用したり、別のバージョンを作成して、特にホストTeams。 コードは次の必要があります。

1. JavaScript SDK Microsoft Teams含める。 これにより、現在のユーザー/チャネル/チーム コンテキストの取得や認証フローの開始など、一般的な操作を実行するための API へのコード アクセスが可能になります。 `microsoftTeams.initialize()` を呼び出して SDK を初期化します。
2. [ `microsoftTeams.settings.setValidityState(true)` 保存] ボタンを有効にする場合に呼び出します。 これは、選択やフィールドの更新など、有効なユーザー入力に対する応答として行う必要があります。
3. ユーザーが `microsoftTeams.settings.registerOnSaveHandler()` [保存] をクリックすると呼び出されるイベント ハンドラーを登録します。
4. コネクタ `microsoftTeams.settings.setSettings()` の設定を保存するために呼び出します。 ここに保存されているのは、ユーザーがコネクタの既存の構成を更新しようとすると、構成ダイアログに表示される操作です。
5. URL `microsoftTeams.settings.getSettings()` 自体を含む Webhook プロパティをフェッチする呼び出し。 これを呼び出す必要があります保存イベント中に加えて、再構成の場合にページが最初に読み込まれたときにも呼び出す必要があります。
6. (省略可能)ユーザーがコネクタを削除すると呼び出されるイベント `microsoftTeams.settings.registerOnRemoveHandler()` ハンドラーを登録します。 このイベントは、サービスにクリーンアップ アクションを実行する機会を提供します。

CSS を使用せずにコネクタ構成ページを作成するサンプル HTML を次に示します。

```html
<h2>Send notifications when tasks are:</h2>
<div class="col-md-8">
    <section id="configSection">
        <form id="configForm">
            <input type="radio" name="notificationType" value="Create" onclick="onClick()"> Created
            <br>
            <br>
            <input type="radio" name="notificationType" value="Update" onclick="onClick()"> Updated
        </form>
    </section>
</div>

<script src="https://statics.teams.microsoft.com/sdk/v1.5.2/js/MicrosoftTeams.min.js" crossorigin="anonymous"></script>
<script src="/Scripts/jquery-1.10.2.js"></script>

<script type="text/javascript">

        function onClick() {
            microsoftTeams.settings.setValidityState(true);
        }

        microsoftTeams.initialize();
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            var radios = document.getElementsByName('notificationType');

            var eventType = '';
            if (radios[0].checked) {
                eventType = radios[0].value;
            } else {
                eventType = radios[1].value;
            }

            microsoftTeams.settings.setSettings({
                 entityId: eventType,
                contentUrl: "https://YourSite/Connector/Setup",
                removeUrl:"https://YourSite/Connector/Setup",
                 configName: eventType
                });

            microsoftTeams.settings.getSettings(function (settings) {
                // We get the Webhook URL in settings.webhookUrl which needs to be saved. 
                // This can be used later to send notification.
            });

            saveEvent.notifySuccess();
        });

        microsoftTeams.settings.registerOnRemoveHandler(function (removeEvent) {
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

#### <a name="getsettings-response-properties"></a>`GetSettings()` 応答プロパティ

>[!Note]
>ここでの呼び出しによって返されるパラメーターは、タブからこのメソッドを呼び出す場合とは異なります。また、ここに記載されているパラメーター `getSettings` とは異 [なります](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)。

| パラメーター   | 詳細 |
|-------------|---------|
| `entityId`       | 呼び出し時にコードによって設定されたエンティティ `setSettings()` ID。 |
| `configName`  | 呼び出し時にコードによって設定される構成名 `setSettings()` 。 |
| `contentUrl` | 呼び出し時にコードによって設定された構成ページの `setSettings()` URL。 |
| `webhookUrl` | このコネクタ用に作成された Webhook URL。 Webhook URL を保持し、それを使用して構造化 JSON を POST してチャネルにカードを送信します。 は、アプリケーションが正常に返される場合にのみ返されます。 |
| `appType` | 返される値には、Office 365 メール、Office 365 グループ、Microsoft Teams のそれぞれに対応する `mail`、`groups`、`teams` を指定できます。 |
| `userObjectId` | これは、コネクタのセットアップを開始Office 365ユーザーに対応する一意の ID です。 セキュリティで保護する必要があります。 この値は、構成をセットアップした Office 365 内のユーザーをサービス内のユーザーに関連付けるために使用できます。 |

上記の手順 2 でページの読み込みの一部としてユーザーを認証する[](~/tabs/how-to/authentication/auth-flow-tab.md)必要がある場合は、ページを埋め込むときにログインを統合する方法の詳細については、このリンクを参照してください。

> [!NOTE]
> クライアント間の互換性上の理由から、コードを呼び出す前に URL と成功/失敗コールバック メソッドで呼び `microsoftTeams.authentication.registerAuthenticationHandlers()` 出す必要があります `authenticate()` 。

#### <a name="handling-edits"></a>編集の処理

コードは、既存のコネクタ構成を編集するために戻るユーザーを処理する必要があります。 これを行うには、次の `microsoftTeams.settings.setSettings()` パラメーターを使用して初期構成中に呼び出します。

- `entityId` は、サービスによって理解され、ユーザーが構成した構成を表すカスタム ID です。
- `configName` は、構成コードで取得できる表示名です。
- `contentUrl` は、ユーザーが既存のコネクタ構成を編集するときに読み込まれるカスタム URL です。 この URL を使用すると、コードで編集ケースを簡単に処理できます。

通常、この呼び出しは、保存イベント ハンドラーの一部として行います。 次に、上記が読み込まれると、コードを呼び出して、構成 UI の設定やフォーム `contentUrl` `getSettings()` を事前設定する必要があります。

#### <a name="handling-removals"></a>削除の処理

必要に応じて、ユーザーが既存のコネクタ構成を削除するときにイベント ハンドラーを実行できます。 このハンドラーを登録するには、 を呼び出します `microsoftTeams.settings.registerOnRemoveHandler()` 。 このハンドラーは、データベースからエントリを削除するなどのクリーンアップ操作を実行するために使用できます。

### <a name="including-the-connector-in-your-manifest"></a>マニフェストにコネクタを含む

自動生成されたアプリ マニフェストTeamsポータルからダウンロードできます。 アプリをテストまたは発行する前に、次の操作を行う必要があります。

- [アイコンを 2 つ含めます](../../concepts/build-and-test/apps-package.md#app-icons)。
- マニフェストの `icons` の部分を変更し、アイコンの URL ではなくアイコンのファイル名を参照するようにします。

次の manifest.json ファイルには、アプリをテストして送信するために必要な基本的な要素が含まれています。

> [!NOTE]
> 次の例の `id` と `connectorId` を、コネクタの GUID に置き換えます。

#### <a name="example-manifestjson-with-connector"></a>コネクタを使用した manifest.json の例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a sample manifest for an app with a connector with an inline configuration experience.",
    "short": "This is a sample manifest for an app with a connector."
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "configurationUrl": "https://teamstodoappconnectorwithinlineconfig.azurewebsites.net/Connector/Setup",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App Long Name"
  },
  "accentColor": "#FFFFFF"
}
```

## <a name="testing-your-connector"></a>コネクタのテスト

コネクタをテストするには、他のアプリと同じ方法でコネクタをチームにアップロードします。 (前のセクションの指示に従って変更された) コネクタ開発者ダッシュボードからのマニフェスト ファイルと 2 つのアイコン ファイルを使用して .zip パッケージを作成できます。

アプリをアップロードしたら、任意のチャネルからコネクタ リストを開きます。 一番下までスクロールして、アプリが [**アップロード済み**] セクションに表示されていることを確認します。

![コネクタ ダイアログ ボックスの [アップロード済み] セクションのスクリーンショット](~/assets/images/connectors/connector_dialog_uploaded.png)

構成機能を起動できるようになりました。 このフローは、ホストされたエクスペリエンスとして、Microsoft Teams内で発生します。

アクションが正しく `HttpPOST` 動作しているのを確認するには [、コネクタにメッセージを送信します](~/webhooks-and-connectors/how-to/connectors-using.md)。

## <a name="publish-connectors-for-your-organization"></a>組織のコネクタを発行する

場合によっては、コネクタ アプリをパブリック AppSource/Store に発行したくない場合がありますが、組織内のユーザーだけが使用できます。 このような場合は、カスタム コネクタ アプリを組織のアプリ カタログ [にアップロードできます](~/concepts/deploy-and-publish/apps-publish.md)。 これにより、コネクタ アプリは、その組織でのみ使用できます。また、コネクタをパブリック ストアに発行する必要が生じられません。

アプリ パッケージをアップロードしたら、チームでコネクタを構成して使用するには、次の手順に従って組織のアプリ カタログからインストールできます。

1. 左上の垂直ナビゲーション バーからアプリ アイコンを選択します。
1. [アプリ **] ウィンドウで** [ **コネクタ] を選択します**。
1. 追加するコネクタを選択すると、ポップアップ ダイアログ ウィンドウが表示されます。
1. [チームに **追加] バーを選択** します。
1. 次のダイアログ ウィンドウで、チーム名またはチャネル名を入力します。
1. ダイアログ ウィンドウ **の右下隅から** [コネクタ バーの設定] を選択します。
1. コネクタは、[その他のオプション] &#9679;&#9679;&#9679; =>チームの[すべてのコネクタ] セクション  =>    =>    =>  で使用できます。 このセクションまでスクロールするか、コネクタ アプリを検索して移動できます。
1. コネクタを構成または変更するには、[構成] バー **を選択** します。

## <a name="code-sample"></a>コード サンプル
|**サンプル名** | **説明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| コネクタ    | Teams チャネルOffice 365生成するコネクタのサンプル。|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| 汎用コネクタのサンプル |Webhook をサポートする任意のシステム用に簡単にカスタマイズできる汎用コネクタのサンプル コード。|  | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
