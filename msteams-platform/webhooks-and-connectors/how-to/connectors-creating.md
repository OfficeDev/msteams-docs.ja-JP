---
title: Office 365 コネクタの作成
author: laujan
description: コネクタの使用を開始するOffice 365説明Microsoft Teams
keywords: Teams o365 コネクタ
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: ee9a00473a7d871e0c69f27a44ca6c7c23eadcbf
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345740"
---
# <a name="create-office-365-connectors"></a>Office 365 コネクタの作成

アプリMicrosoft Teams、既存のコネクタを追加するか、Office 365内に新しいコネクタをTeams。 詳細については、「独自のコネクタ [をビルドする」を参照してください](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector)。

## <a name="add-a-connector-to-teams-app"></a>コネクタをアプリにTeamsする

AppSource[申請の](~/concepts/build-and-test/apps-package.md)[一部](~/concepts/deploy-and-publish/apps-publish.md)としてコネクタをパッケージ化して発行できます。 登録されたコネクタは、アプリ パッケージの一部としてTeamsできます。 アプリのエントリ ポイントの詳細については、「Teams機能」[を参照してください](~/concepts/extensibility-points.md)。 また、パッケージをユーザーに直接提供して、アプリ内でアップロードTeams。

コネクタを配布するには、Connectors Developer [Dashboard を使用して登録する必要があります](https://outlook.office.com/connectors/home/login/#/publish)。 コネクタが登録されている場合は、アプリケーションをサポートしているすべての Office 365 製品で動作OutlookとTeams。 この問題が当てはめず、アプリ申請メールで動作するコネクタのみを作成するMicrosoft Teams:Microsoft Teams[に連絡してください](mailto:teamsubm@microsoft.com)。

> [!IMPORTANT]
> コネクタ開発者ダッシュボードで [保存] を **選択** すると、コネクタが登録されます。 AppSource でコネクタを発行する場合は、「アプリを AppSource に発行する」のMicrosoft Teams[に従います](~/concepts/deploy-and-publish/apps-publish.md)。 AppSource でアプリを発行しない場合は、組織に直接配布します。 組織 [のコネクタを発行した後](#publish-connectors-for-the-organization)、コネクタ ダッシュボードでそれ以上の操作は必要ありません。

### <a name="integrate-the-configuration-experience"></a>構成エクスペリエンスの統合

ユーザーは、クライアントから離れることなく、コネクタ構成Teamsできます。 このエクスペリエンスを得Teams、構成ページを iframe 内に直接埋め込む必要があります。 操作のシーケンスは次のとおりです。

1. ユーザーがコネクタを選択して構成プロセスを開始します。
1. ユーザーは Web エクスペリエンスを操作して構成を完了します。
1. ユーザーが [保存] **を選択** し、コード内のコールバックをトリガーします。

    > [!NOTE]
    > * コードは、Webhook 設定を取得して保存イベントを処理できます。 後でイベントを投稿する Webhook をコードに格納します。
    > * 構成エクスペリエンスは、構成エクスペリエンス内でインラインTeams。

既存の Web 構成エクスペリエンスを再利用したり、別のバージョンを作成して、特にホストTeams。 コードには JavaScript SDK Microsoft Teams含める必要があります。 これにより、現在のユーザー、チャネル、またはチーム のコンテキストを取得して認証フローを開始するなどの一般的な操作を実行するための API へのコード アクセスが可能になります。

**構成エクスペリエンスを統合するには**

1. `microsoftTeams.initialize()` を呼び出して SDK を初期化します。
1. [保存 `microsoftTeams.settings.setValidityState(true)` ] を有効にする **呼び出し**。

    > [!NOTE]
    > ユーザーの選択または `microsoftTeams.settings.setValidityState(true)` フィールドの更新に対する応答として呼び出す必要があります。

1. ユーザー  `microsoftTeams.settings.registerOnSaveHandler()` が [保存] を選択すると呼び出されるイベント ハンドラーを登録 **します**。
1. コネクタ `microsoftTeams.settings.setSettings()` の設定を保存するために呼び出します。 ユーザーがコネクタの既存の構成を更新しようとすると、保存された設定も構成ダイアログに表示されます。
1. `microsoftTeams.settings.getSettings()`URL を含む Webhook プロパティをフェッチする呼び出し。

    > [!NOTE]
    > 再構成の場合 `microsoftTeams.settings.getSettings()` は、ページが最初に読み込まれたときに呼び出す必要があります。

1. ユーザー `microsoftTeams.settings.registerOnRemoveHandler()` がコネクタを削除するときに呼び出されるイベント ハンドラーを登録します。

このイベントは、サービスにクリーンアップ アクションを実行する機会を提供します。

次のコードは、カスタマー サービスとサポートなしでコネクタ構成ページを作成するサンプル HTML を提供します。

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

ページの読み込みの一環としてユーザーを認証[](~/tabs/how-to/authentication/auth-flow-tab.md)するには、「ページが埋め込まれているときにサインインを統合するためのタブの認証フロー」を参照してください。

> [!NOTE]
> クライアント間の互換性上の理由から、コードは呼び出す前に URL と成功または失敗のコールバック メソッドで呼び `microsoftTeams.authentication.registerAuthenticationHandlers()` 出す必要があります `authenticate()` 。

#### <a name="getsettings-response-properties"></a>`GetSettings` 応答プロパティ

>[!NOTE]
>このメソッドをタブから呼び出すと、呼び出しによって返されるパラメーターは異なります。js 設定に記載されているパラメーター `getSettings` とは [異なります](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)。

次の表に、パラメーターと応答プロパティの詳細 `GetSetting` を示します。

| パラメーター   | 詳細 |
|-------------|---------|
| `entityId`       | 呼び出し時にコードによって設定されたエンティティ `setSettings()` ID。 |
| `configName`  | 呼び出し時にコードによって設定される構成名 `setSettings()` 。 |
| `contentUrl` | 呼び出し時にコードによって設定された構成ページの `setSettings()` URL。 |
| `webhookUrl` | コネクタ用に作成された Webhook URL。 Webhook URL を使用して構造化 JSON を POST し、チャネルにカードを送信します。 アプリケーション `webhookUrl` がデータを正常に返した場合にのみ返されます。 |
| `appType` | 返される値は、メール、グループ、Office 365、またはOffice 365 Office 365に対応Microsoft Teams `mail` `groups` `teams` できます。 |
| `userObjectId` | コネクタのセットアップを開始Office 365ユーザーに対応する一意の ID。 セキュリティで保護されている必要があります。 この値は、サービスで構成をOffice 365ユーザーを関連付ける場合に使用できます。 |

#### <a name="handle-edits"></a>編集の処理

コードは、既存のコネクタ構成の編集に戻るユーザーを処理する必要があります。 これを行うには、次の `microsoftTeams.settings.setSettings()` パラメーターを使用して初期構成中に呼び出します。

- `entityId` は、ユーザーがサービスで構成および理解した情報を表すカスタム ID です。
- `configName` は、構成コードが取得できる名前です。
- `contentUrl` は、ユーザーが既存のコネクタ構成を編集するときに読み込まれるカスタム URL です。

この呼び出しは、保存イベント ハンドラーの一部として行います。 次に、読み込まれると、構成ユーザー インターフェイスの設定やフォームを事前に設定するためにコードを呼び `contentUrl` `getSettings()` 出す必要があります。

#### <a name="handle-removals"></a>削除の処理

ユーザーが既存のコネクタ構成を削除すると、イベント ハンドラーを実行できます。 このハンドラーを登録するには、 を呼び出します `microsoftTeams.settings.registerOnRemoveHandler()` 。 このハンドラーは、データベースからエントリを削除するなどのクリーンアップ操作を実行するために使用されます。

### <a name="include-the-connector-in-your-manifest"></a>マニフェストにコネクタを含める

ポータルから自動生成 `Teams app manifest` をダウンロードします。 アプリをテストまたは発行する前に、次の手順を実行します。

1. [アイコンを 2 つ含めます](../../concepts/build-and-test/apps-package.md#app-icons)。
1. マニフェストの `icons` 部分を変更して、URL ではなくアイコンのファイル名を含める。

ファイルのmanifest.jsには、アプリのテストと送信に必要な要素が含まれています。

> [!NOTE]
> 次 `id` の `connectorId` 例では、コネクタの GUID に置き換え、使用します。

#### <a name="example-of-manifestjson-with-connector"></a>コネクタを使用manifest.jsの例

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
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="enable-or-disable-connectors-in-teams"></a>デバイスでコネクタを有効または無効Teams

PowerShell V2 Exchange Onlineモジュールは、モダン認証を使用し、多要素認証 (MFA と呼ばれる) を使用して、Exchange に関連する PowerShell 環境に接続Microsoft 365。 管理者は、Exchange Online PowerShell を使用して、テナント全体または特定のグループ メールボックスのコネクタを無効にし、そのテナントまたはメールボックス内のすべてのユーザーに影響を与える可能性があります。 一部のユーザーに対して無効にし、他のユーザーに対して無効にはできません。 また、コネクタは既定で、テナントと呼ばれるGovernment Community CloudにGCCされます。

テナント レベルの設定は、グループ レベルの設定より優先されます。 たとえば、管理者がグループのコネクタを有効にしてテナントで無効にした場合、グループのコネクタは無効になります。 クライアントでコネクタを有効にするにはTeams MFA のExchange Online[を使用して PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true)に接続します。

### <a name="commands-to-enable-or-disable-connectors"></a>コネクタを有効または無効にするコマンド

Exchange Online PowerShell で次のコマンドを実行します。

* テナントのコネクタを無効にするには、次のコマンドを実行します `Set-OrganizationConfig -ConnectorsEnabled:$false` 。
* テナントのアクション可能なメッセージを無効にするには、次の操作を行います `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false` 。
* コネクタを有効にするには、Teamsコマンドを実行します。
  * `Set-OrganizationConfig -ConnectorsEnabled:$true `
  * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
  * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

PowerShell モジュール交換の詳細については [、「Set-OrganizationConfig」を参照してください](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true)。 コネクタを有効または無効にするにはOutlookでアプリを[グループに接続Outlook。](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us)

## <a name="test-your-connector"></a>コネクタをテストする

コネクタをテストするには、他のアプリを使用してチームにアップロードします。 マニフェスト ファイルとコネクタ.zipマニフェスト ファイルを使用して、マニフェスト パッケージを作成できます。「マニフェストにコネクタを含める」の指示に基いて [変更されます](#include-the-connector-in-your-manifest)。

アプリをアップロードした後、任意のチャネルからコネクタリストを開きます。 下にスクロールして、[アップロード] セクションにアプリ **を表示** します。

![[コネクタ] ダイアログ ボックスでアップロードされたセクションのスクリーンショット](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> フローは、ホストされたエクスペリエンスとしてMicrosoft Teams内で完全に発生します。

アクションが正 `HttpPOST` しく動作しているのを確認するには [、コネクタにメッセージを送信します](~/webhooks-and-connectors/how-to/connectors-using.md)。

## <a name="publish-connectors-for-the-organization"></a>組織の発行コネクタ

コネクタを組織内のユーザーだけが使用できる場合は、カスタム コネクタ アプリを組織のアプリ カタログ [にアップロードできます](~/concepts/deploy-and-publish/apps-publish.md)。

チームでコネクタを構成して使用するためにアプリ パッケージをアップロードした後、組織のアプリ カタログからコネクタをインストールします。

**コネクタを設定するには**

1. 左側の **ナビゲーション** バーから [アプリ] を選択します。
1. [アプリ **] セクションで** 、[コネクタ] **を選択します**。
1. 追加するコネクタを選択します。 ポップアップ ダイアログ ウィンドウが表示されます。
1. ドロップダウン メニューから、[チームに **追加] を選択します**。
1. 検索ボックスに、チーム名またはチャネル名を入力します。
1. ダイアログ **ウィンドウの右下隅** にあるドロップダウン メニューから [コネクタのセットアップ] を選択します。

> [!IMPORTANT]
> 現在、カスタム コネクタは、Government Community Cloud (GCC)、GCC-High、および国防総省 (DOD) では使用できません。

コネクタは、「その他のオプション コネクタ &#9679;&#9679;&#9679; > チームのすべてのコネクタ」のセクション  >    >    >  で使用できます。 このセクションまでスクロールするか、コネクタ アプリを検索して移動できます。 コネクタを構成または変更するには、[構成] を **選択します**。

## <a name="distribute-webhook-and-connector"></a>Webhook とコネクタの配布

1. [チームに直接受信 Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) を設定します。
1. 構成ページ [を追加し](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) 、O365 コネクタで受信 [Webhook](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) を発行します。
1. AppSource 申請の一部としてコネクタをパッケージ化 [して発行](~/concepts/deploy-and-publish/office-store-guidance.md) します。

## <a name="code-sample"></a>コード サンプル

次の表に、サンプル名とその説明を示します。

|**サンプルの名前** | **説明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| コネクタ    | サンプル Office 365 チャネルへの通知を生成するコネクタTeamsします。|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| 汎用コネクタのサンプル |Webhook をサポートする任意のシステム用にカスタマイズしやすい汎用コネクタのサンプル コード。|  | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="see-also"></a>関連項目

* [メッセージを作成して送信する](~/webhooks-and-connectors/how-to/connectors-using.md)
* [受信 Webhook の作成](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Office 365 コネクタを作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)
