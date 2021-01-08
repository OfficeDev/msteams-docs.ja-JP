---
title: Office 365 コネクタ
description: Microsoft Teams で Office 365 コネクタの使用を開始する方法について説明します
keywords: Teams o365 コネクタ
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 62a27e8f7b218491682ff0b9216e428f51264d0a
ms.sourcegitcommit: 5f1d6c12d80d48f403b73586f68bacf15785c855
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/30/2020
ms.locfileid: "49739050"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>Microsoft Teams Office 365 コネクタの作成

>Microsoft Teams アプリを使用すると、既存の Office 365 コネクタを追加したり、Microsoft Teams に含める新しいコネクタを作成することができます。 詳細 [については、「独自のコネクタを作成する](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) 」を参照してください。

## <a name="adding-a-connector-to-your-teams-app"></a>Teams アプリへのコネクタの追加

登録済みのコネクタを Teams アプリ パッケージの一部として配布できます。 スタンドアロン ソリューションとしても、Teams でエクスペリエンスが可能[](~/concepts/extensibility-points.md)ないくつかの機能の 1 つとしても、AppSource[](~/concepts/deploy-and-publish/apps-publish.md)提出の一部としてコネクタをパッケージ化して公開したり、Teams 内でアップロードするためにユーザーに直接提供することができます。 [](~/concepts/build-and-test/apps-package.md)

コネクタを配布するには、コネクタ開発者ダッシュボードを使用して [登録する必要があります](https://outlook.office.com/connectors/home/login/#/publish)。 既定では、コネクタを登録すると、Outlook や Teams を含む、コネクタをサポートする Office 365 製品すべてでコネクタが機能すると想定されます。 Microsoft Teams _でのみ動作_ するコネクタを作成する必要がある場合は、Microsoft Teams アプリの申請で直接 [お問い合わせください](mailto:teamsubm@microsoft.com)。

> [!IMPORTANT]
> コネクタ開発者ダッシュボード **で** [保存] を選択すると、コネクタが登録されます。 AppSource でコネクタを発行する場合は、「Microsoft Teams アプリを AppSource に発行する」の手順 [に従います](~/concepts/deploy-and-publish/apps-publish.md)。 AppSource でアプリを公開するのではなく、組織にのみ直接配布する場合は、組織に公開 [します](#publish-connectors-for-your-organization)。 組織にのみ発行する場合は、コネクタ ダッシュボードでこれ以上の操作は必要ありません。

### <a name="integrating-the-configuration-experience"></a>構成エクスペリエンスの統合

ユーザーは、Teams クライアントから離れることなく、コネクタの構成エクスペリエンス全体を完了します。 このエクスペリエンスを実現するために、Teams は構成ページを iframe 内に直接埋め込む必要があります。 操作の順序は次のとおりです。

1. ユーザーがコネクタをクリックして構成プロセスを開始します。
2. Teams は、構成エクスペリエンスをラインで読み込む。
3. ユーザーは Web エクスペリエンスを操作して構成を完了します。
4. ユーザーが "Save" を押すと、コード内でコールバックがトリガーされます。
5. コードは、webhook 設定を取得して保存イベントを処理します (以下に説明します)。 コードでは、後でイベントを投稿するために webhook を保存する必要があります。

既存の Web 構成エクスペリエンスを再利用したり、Teams で特にホストする別のバージョンを作成することができます。 コードは次の条件を実行する必要があります。

1. Microsoft Teams JavaScript SDK を含める。 これにより、現在のユーザー/チャネル/チーム コンテキストの取得や認証フローの開始など、一般的な操作を実行する API へのコード アクセスが可能になります。 `microsoftTeams.initialize()` を呼び出して SDK を初期化します。
2. [ `microsoftTeams.settings.setValidityState(true)` 保存] ボタンを有効にする場合に呼び出します。 これは、選択やフィールドの更新など、有効なユーザー入力への応答として行う必要があります。
3. ユーザーが `microsoftTeams.settings.registerOnSaveHandler()` [保存] をクリックすると呼び出されるイベント ハンドラーを登録します。
4. コネクタ `microsoftTeams.settings.setSettings()` の設定を保存するために呼び出します。 ここで保存される情報は、ユーザーがコネクタの既存の構成を更新しようとすると、構成ダイアログに表示されます。
5. `microsoftTeams.settings.getSettings()`URL 自体を含む webhook プロパティをフェッチする呼び出し。 保存イベント中にこのメソッドを呼び出す必要があります。また、再構成の場合にページが最初に読み込まれたときにも、このメソッドを呼び出す必要があります。
6. (省略可能)ユーザーが `microsoftTeams.settings.registerOnRemoveHandler()` コネクタを削除するときに呼び出されるイベント ハンドラーを登録します。 このイベントにより、サービスはクリーンアップ操作を実行できます。

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
            var removeCalled = true;
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

#### <a name="getsettings-response-properties"></a>`GetSettings()` 応答プロパティ

>[!Note]
>ここでの呼び出しによって返されるパラメーターは、タブからこのメソッドを呼び出す場合とは異なります。また、ここに記載されているパラメーター `getSettings` とは異 [なります](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)。

| パラメーター   | 詳細 |
|-------------|---------|
| `entityId`       | 呼び出し時にコードによって設定されるエンティティ `setSettings()` ID。 |
| `configName`  | 呼び出し時にコードによって設定される構成名 `setSettings()` 。 |
| `contentUrl` | 呼び出し時にコードによって設定される構成ページの URL `setSettings()` |
| `webhookUrl` | このコネクタ用に作成された webhook URL。 webhook URL を永続化し、POST 構造化 JSON に使用してカードをチャネルに送信します。 は、アプリケーションが正常に返される場合にのみ返されます。 |
| `appType` | 返される値には、Office 365 メール、Office 365 グループ、Microsoft Teams のそれぞれに対応する `mail`、`groups`、`teams` を指定できます。 |
| `userObjectId` | これは、コネクタのセットアップを開始した Office 365 ユーザーに対応する一意の ID です。 セキュリティで保護する必要があります。 この値は、構成をセットアップした Office 365 内のユーザーをサービス内のユーザーに関連付けるために使用できます。 |

上記の手順 2 でページを読み込む際にユーザーを認証する必要[](~/tabs/how-to/authentication/auth-flow-tab.md)がある場合は、ページが埋め込まれたときにログインを統合する方法の詳細については、このリンクを参照してください。

> [!NOTE]
> クライアント間の互換性上の理由から、コードは呼び出す前に URL と成功/失敗コールバック メソッドを使用して呼び `microsoftTeams.authentication.registerAuthenticationHandlers()` 出す必要があります `authenticate()` 。

#### <a name="handling-edits"></a>編集の処理

コードは、既存のコネクタ構成を編集するために戻るユーザーを処理する必要があります。 これを行うには、次の `microsoftTeams.settings.setSettings()` パラメーターを使用して初期構成中に呼び出します。

- `entityId` は、サービスによって理解されるカスタム ID であり、ユーザーが構成した構成を表します。
- `configName` は、構成コードで取得できる表示名です。
- `contentUrl` は、ユーザーが既存のコネクタ構成を編集するときに読み込まれるカスタム URL です。 この URL を使用すると、コードで編集ケースを簡単に処理できます。

通常、この呼び出しは保存イベント ハンドラーの一部として行います。 次に、上記が読み込まれたら、コードを呼び出して、構成 UI に設定または `contentUrl` `getSettings()` フォームを事前設定する必要があります。

#### <a name="handling-removals"></a>削除の処理

必要に応じて、ユーザーが既存のコネクタ構成を削除するときにイベント ハンドラーを実行できます。 このハンドラーは、呼び出して登録します `microsoftTeams.settings.registerOnRemoveHandler()` 。 このハンドラーを使用して、データベースからエントリを削除するなどのクリーンアップ操作を実行できます。

### <a name="including-the-connector-in-your-manifest"></a>マニフェストにコネクタを含む

自動生成された Teams アプリ マニフェストは、ポータルからダウンロードできます。 アプリをテストまたは公開する前に、次の操作を行う必要があります。

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

構成機能を起動できるようになりました。 このフローは、ホストされたエクスペリエンスとして Microsoft Teams 内で完全に発生します。

操作が正しく `HttpPOST` 動作を確認するには、 [コネクタにメッセージを送信します](~/webhooks-and-connectors/how-to/connectors-using.md)。

## <a name="publish-connectors-for-your-organization"></a>組織のコネクタを発行する

場合によっては、コネクタ アプリをパブリック AppSource/Store に公開したくないが、組織内のユーザーだけが利用できる場合があります。 このような場合は、カスタム コネクタ アプリを組織のアプリ カタログ [にアップロードできます](~/concepts/deploy-and-publish/apps-publish.md)。 これにより、コネクタ アプリは、その組織でのみ利用できます。また、コネクタをパブリック ストアに公開する必要が生じられません。

アプリ パッケージをアップロードしたら、チームでコネクタを構成して使用するために、次の手順に従って、組織のアプリ カタログからインストールできます。

1. 一方、一方のバーティカル ナビゲーション バーからアプリ アイコンを選択します。
1. [アプリ **] ウィンドウで** 、[コネクタ] **を選択します**。
1. 追加するコネクタを選択すると、ポップアップ ダイアログ ウィンドウが表示されます。
1. [チーム **に追加] バーを選択** します。
1. 次のダイアログ ウィンドウで、チーム名またはチャネル名を入力します。
1. ダイアログ ウィンドウ **の右下隅** から [コネクタ バーのセットアップ] を選択します。
1. コネクタは、そのチームのチームの &#9679;&#9679;&#9679; =>その他のオプションコネクタすべてのコネクタのセクション  =>    =>    =>  で使用できます。 このセクションをスクロールするか、コネクタ アプリを検索して移動できます。
1. コネクタを構成または変更するには、[構成] バー **を選択** します。
