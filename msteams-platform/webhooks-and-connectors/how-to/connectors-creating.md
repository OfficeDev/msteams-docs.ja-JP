---
title: Office 365 コネクタ
description: Microsoft TeamsでコネクタをOffice 365する方法について説明します。
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
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>Microsoft Teams用Office 365コネクタの作成

>Microsoft Teamsアプリを使用すると、既存のOffice 365コネクタを追加したり、Microsoft Teamsに含める新しいOffice 365を構築したりできます。 詳細については、「 [独自のコネクタを構築](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) する」を参照してください。

## <a name="adding-a-connector-to-your-teams-app"></a>Teams アプリへのコネクタの追加

登録済みのコネクタを Teams アプリ パッケージの一部として配布できます。 スタンドアロン ソリューションとして、またはTeamsでエクスペリエンスで有効にするいくつかの[機能](~/concepts/extensibility-points.md)の 1 つとして、[パッケージ化して](~/concepts/build-and-test/apps-package.md)、AppSource 申請の一部として、またはTeams内でアップロードするユーザーに直接提供することができます。 [](~/concepts/deploy-and-publish/apps-publish.md)

コネクタを配布するには、コネクタ [開発者ダッシュボード](https://outlook.office.com/connectors/home/login/#/publish)を使用して登録する必要があります。 既定では、コネクタが登録されると、コネクタは、OutlookやTeamsを含む、それらをサポートするすべてのOffice 365製品で動作することを前提としています。 そう _ではなく_、Microsoft Teamsでのみ動作するコネクタを作成する必要がある場合は [、Microsoft Teamsアプリの提出書類](mailto:teamsubm@microsoft.com)に直接お問い合わせください。

> [!IMPORTANT]
> コネクタ開発者ダッシュボードで **[保存]** を選択すると、コネクタが登録されます。 コネクタを AppSource で公開する場合は[、「Microsoft Teams アプリを AppSource に発行する](~/concepts/deploy-and-publish/apps-publish.md)」の手順に従います。 AppSource でアプリを公開せず、単に組織にのみ直接配布する場合は、 [組織 に公開](#publish-connectors-for-your-organization)します。 組織に公開するだけの場合は、コネクタ ダッシュボードでそれ以上の操作は必要ありません。

### <a name="integrating-the-configuration-experience"></a>構成エクスペリエンスの統合

ユーザーは、Teams クライアントから離れることなく、コネクタ構成エクスペリエンス全体を完了します。 このエクスペリエンスを実現するために、Teamsは iframe 内に直接構成ページを埋め込みます。 操作の順序は次のとおりです。

1. ユーザーがコネクタをクリックして、構成プロセスを開始します。
2. Teamsは、構成エクスペリエンスを一列に読み込みます。
3. ユーザーは Web エクスペリエンスを操作して構成を完了します。
4. ユーザーは "Save" を押すと、コード内のコールバックがトリガーされます。
5. コードは、webhook 設定を取得して保存イベントを処理します (以下に記載)。 その後、コードは Webhook を保存してイベントを後で投稿する必要があります。

既存の Web 構成エクスペリエンスを再利用したり、Teamsで特別にホストされる別のバージョンを作成したりできます。 コードは次のコードを実行する必要があります。

1. Microsoft Teams JavaScript SDK を含めます。 これにより、コードから API にアクセスして、現在のユーザ/チャネル/チーム コンテキストの取得や認証フローの実行などの一般的な操作を実行できます。 `microsoftTeams.initialize()` を呼び出して SDK を初期化します。
2. `microsoftTeams.settings.setValidityState(true)`[保存] ボタンを有効にするときに呼び出します。 これは、選択やフィールドの更新など、有効なユーザー入力に対する応答として行う必要があります。
3. `microsoftTeams.settings.registerOnSaveHandler()`ユーザーが [保存] をクリックしたときに呼び出されるイベント ハンドラーを登録します。
4. `microsoftTeams.settings.setSettings()`コネクタの設定を保存するために呼び出します。 ここに保存されているのは、ユーザーがコネクタの既存の構成を更新しようとした場合に、構成ダイアログに表示される内容です。
5. `microsoftTeams.settings.getSettings()`URL 自体を含む、webhook プロパティを取得する呼び出し。 これを呼び出す必要があります 保存イベント中に、再設定の場合にページが最初に読み込まれたときに、これを呼び出す必要もあります。
6. (オプション) `microsoftTeams.settings.registerOnRemoveHandler()` ユーザーがコネクタを削除したときに呼び出されるイベント ハンドラーを登録します。 このイベントは、サービスにクリーンアップ操作を実行する機会を与えます。

CSS を使用せずにコネクタ構成ページを作成する HTML の例を次に示します。

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

#### <a name="getsettings-response-properties"></a>`GetSettings()` 応答のプロパティ

>[!Note]
>`getSettings`ここでの呼び出しによって返されるパラメータは、このメソッドをタブから呼び出す場合とは異なり[、ここで](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)説明しているパラメータとは異なります。

| パラメーター   | 詳細 |
|-------------|---------|
| `entityId`       | を呼び出すときにコードによって設定されるエンティティ `setSettings()` ID。 |
| `configName`  | を呼び出すときにコードによって設定される構成名 `setSettings()` 。 |
| `contentUrl` | を呼び出すときにコードによって設定される構成ページの `setSettings()` URL。 |
| `webhookUrl` | このコネクタ用に作成された webhook URL。 ウェブフック URL を保持し、それを使用して、構造化 JSON を POST して、カードをチャネルに送信します。 は、アプリケーションが正常に返される場合にのみ返されます。 |
| `appType` | 返される値には、Office 365 メール、Office 365 グループ、Microsoft Teams のそれぞれに対応する `mail`、`groups`、`teams` を指定できます。 |
| `userObjectId` | これは、コネクタのセットアップを開始したOffice 365ユーザーに対応する一意の ID です。 セキュリティで保護する必要があります。 この値は、構成をセットアップした Office 365 内のユーザーをサービス内のユーザーに関連付けるために使用できます。 |

上記のステップ 2 でのページのロードの一部としてユーザーを認証する必要がある場合は、ページが埋め込まれているときにログインを統合する方法の詳細については、 [このリンク](~/tabs/how-to/authentication/auth-flow-tab.md) を参照してください。

> [!NOTE]
> クライアント間の互換性の理由から、コードは、 を呼び `microsoftTeams.authentication.registerAuthenticationHandlers()` 出す前に URL および成功/失敗コールバック メソッドを呼び出す必要があります `authenticate()` 。

#### <a name="handling-edits"></a>編集の処理

コードは、既存のコネクタ構成を編集するために戻るユーザーを処理する必要があります。 これを行うには、 `microsoftTeams.settings.setSettings()` 次のパラメータを使用して初期設定時に呼び出します。

- `entityId` は、サービスによって認識され、ユーザーが構成した内容を表すカスタム ID です。
- `configName` は、構成コードが取得できるフレンドリ名です
- `contentUrl` は、ユーザーが既存のコネクタ構成を編集するときに読み込まれるカスタム URL です。 この URL を使用すると、コードでの編集ケースの処理を容易にすることができます。

通常、この呼び出しは、保存イベント ハンドラーの一部として行われます。 次に、 `contentUrl` 上記のコードが読み込まれると、コードを呼び出 `getSettings()` して、構成 UI の設定やフォームを事前に設定する必要があります。

#### <a name="handling-removals"></a>削除の処理

ユーザーが既存のコネクタ構成を削除したときに、必要に応じてイベント ハンドラーを実行できます。 このハンドラを登録する `microsoftTeams.settings.registerOnRemoveHandler()` 場合は、 を呼び出します。 このハンドラーを使用して、データベースからエントリを削除するなどのクリーンアップ操作を実行できます。

### <a name="including-the-connector-in-your-manifest"></a>マニフェストにコネクタを含めます

自動生成されたTeamsアプリ マニフェストは、ポータルからダウンロードできます。 ただし、アプリをテストまたは公開するために使用する前に、次の操作を行う必要があります。

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

構成機能を起動できるようになりました。 このフローは、ホストされたエクスペリエンスとしてMicrosoft Teams内で発生します。

`HttpPOST`操作が正常に動作していることを確認するには、[コネクタ にメッセージを送信](~/webhooks-and-connectors/how-to/connectors-using.md)します。

## <a name="publish-connectors-for-your-organization"></a>組織のコネクタを公開する

コネクタ アプリをパブリック AppSource/Store に公開したくない場合がありますが、組織のユーザーのみが使用できるようにしたい場合があります。 このような場合は、組織の [App Catalog](~/concepts/deploy-and-publish/apps-publish.md)にカスタム コネクタ アプリをアップロードできます。 この方法では、コネクタ アプリはその組織でのみ使用でき、コネクタをパブリック ストアに発行する必要はありません。

アプリ パッケージをアップロードしたら、チームのコネクタを構成して使用するには、次の手順に従って組織のアプリ カタログからインストールできます。

1. 左端の垂直ナビゲーション バーからアプリ アイコンを選択します。
1. **[アプリ**] ウィンドウで [**コネクタ**] を選択します。
1. 追加するコネクタを選択すると、ポップアップ ダイアログ ウィンドウが表示されます。
1. [ **チームに追加** ] バーを選択します。
1. 次のダイアログ ウィンドウで、チーム名またはチャネル名を入力します。
1. ダイアログ ウィンドウの右下隅から[コネクタ バーを **設定]** を選択します。
1. コネクタは、そのチームのチームの [その他のオプション] &#9679;&#9679;&#9679; => [*その他のオプション*  =>  *コネクタ*  =>  *] セクション*  =>  で使用できます。 このセクションまでスクロールするか、コネクタ アプリを検索して移動できます。
1. コネクタを構成または変更するには、[ **構成** ] バーを選択します。

## <a name="code-sample"></a>コード サンプル
|**サンプル名** | **説明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| コネクタ    | サンプル Office 365 チームチャネルへの通知を生成するコネクタを示します。|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| 汎用コネクタのサンプル |webhook をサポートするシステムに合わせて簡単にカスタマイズできる汎用コネクタのサンプル コード。|  | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
