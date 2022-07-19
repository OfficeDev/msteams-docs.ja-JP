---
title: Office 365 コネクタの作成
author: laujan
description: このモジュールでは、Office 365 コネクタの使用を開始し、Microsoft Teams の Teams アプリにコネクタを追加する方法について説明します
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: a0e135864fd7c7d9775731e6c46faf9f24242943
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841641"
---
# <a name="create-office-365-connectors"></a>Office 365 コネクタの作成

Microsoft Teams アプリを使用すると、Teams 内に既存の Office 365 コネクタを追加したり、新しい Office 365 コネクタを作成したりできます。詳細については、[自分でコネクタを開発する](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector)を参照してください。

Office 365 コネクタを作成する方法については、次のビデオを参照してください。
<br>

> [!VIDEO <https://www.microsoft.com/en-us/videoplayer/embed/RE4OIzv>]
<br>

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="add-a-connector-to-teams-app"></a>Teams アプリにコネクタを追加する

[パッケージ](~/concepts/build-and-test/apps-package.md)を作成し、AppSource への提出の一部としてコネクタを[公開](~/concepts/deploy-and-publish/apps-publish.md)できます。 登録済みのコネクタを Teams アプリ パッケージの一部として配布できます。 Teams アプリのエントリ ポイントに関する情報は、[機能](~/concepts/extensibility-points.md)を参照してください。 Teams 内でアップロードするために、パッケージをユーザーに直接提供することもできます。

コネクタを配布するには、[コネクタ開発者ダッシュボード](https://aka.ms/connectorsdashboard)にコネクタを登録します。

コネクタを Teams でのみ機能させるには、手順に従って、 [Microsoft Teams ストアの記事にアプリを公開する際にコネクタを](~/concepts/deploy-and-publish/appsource/publish.md) 送信します。 それ以外の場合、登録済みのコネクタは、Outlook や Teams など、アプリケーションをサポートするすべての Office 365 製品で機能します。

> [!IMPORTANT]
> コネクタは、コネクタ開発者ダッシュボードで **[保存]** を選択した後で登録されます。 AppSource でコネクタを発行する場合は、[Microsoft Teams アプリを AppSource に公開する](~/concepts/deploy-and-publish/apps-publish.md)の手順に従います。 AppSource でアプリを公開しない場合は、それを組織に直接配布します。 組織のコネクタを公開した後、コネクタ ダッシュボードでそれ以上のアクションは必要ありません。

### <a name="integrate-the-configuration-experience"></a>構成エクスペリエンスを統合する

ユーザーは、Teams クライアントから離れることなく、すべてのコネクタ構成エクスペリエンスを完了できます。 エクスペリエンスを得るために、Teams は iframe 内に直接構成ページを埋め込むことができます。 操作のシーケンスは以下のとおりです。

1. ユーザーが構成プロセスを開始するために、コネクタを選択します。
1. ユーザーは Web エクスペリエンスと対話し、構成を完了します。
1. ユーザーは、コードのコールバックをトリガーする **[保存]** を選択します。

    > [!NOTE]
    >
    > * このコードでは、Webhook 設定を取得して保存イベントを処理することができます。 コードには、後でイベントを投稿するための Webhook が格納されます。
    > * 構成エクスペリエンスは、Teams 内にインラインで読み込まれます。

既存の Web 構成エクスペリエンスを再利用することも、Teams 専用にホストされた別のバージョンを作成することもできます。 コードには Teams JavaScript SDK を含める必要があります。 これにより、コードから API にアクセスして、現在のユーザー、チャネル、またはチーム コンテキストの取得や認証フローの開始などの一般的な操作を実行できます。

構成エクスペリエンスを統合するには、以下の操作を行います。

> [!NOTE]
> Teams JavaScript クライアント SDK (TeamsJS) v.2.0.0 以降、 *設定* 名前空間内の API は非推奨となり、サブ名前空間内の *他* の API を含め `pages.getConfig()` 、ページ名前空間内 `pages.config` の同等の API が優先されました。 詳細については、「[TeamsJS バージョン 2.0 の新機能](../../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20)」を参照してください。

1. `app.initialize()` を呼び出して SDK を初期化します。
1. `pages.config.setValidityState(true)` を呼び出して **[保存]** を有効にします。

    > [!NOTE]
    > ユーザーの選択またはフィールドの更新に対する応答として `microsoftTeams.pages.config.setValidityState(true)` を呼び出す必要があります。

1. ユーザーが **[保存]** を選択した場合に呼び出される `microsoftTeams.pages.config.registerOnSaveHandler()` イベント ハンドラーを登録します。
1. `microsoftTeams.pages.config.setConfig()` を呼び出し、コネクタ設定を保存します。保存された設定は、ユーザーがコネクタの既存の構成を更新しようとした場合にも、構成ダイアログに表示されます。
1. `microsoftTeams.pages.getConfig()` を呼び出し、URL を含む Webhook プロパティを取得します。

    > [!NOTE]
    > 再設定する場合は、ページが最初にロードされたときに `microsoftTeams.pages.getConfig()` を呼び出す必要があります。

1. ユーザーがコネクタを削除した場合に呼び出される `microsoftTeams.pages.config.registerOnRemoveHandler()` イベント ハンドラーを登録します。

このイベントにより、サービスはクリーンアップ アクションを実行できます。

以下のコードは、カスタマー サービスやサポートなしでコネクタ設定ページを作成するためのサンプル HTML です。

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

<script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js" integrity="sha384-Q2Z9S56exI6Oz/ThvYaV0SUn8j4HwS8BveGPmuwLXe4CvCUEGlL80qSzHMnvGqee" crossorigin="anonymous"></script>
<script src="/Scripts/jquery-1.10.2.js"></script>

<script type="module">
        import {app, pages} from 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js';
        
        function onClick() {
            pages.config.setValidityState(true);
        }

        await app.initialize();
        pages.config.registerOnSaveHandler(function (saveEvent) {
            var radios = document.getElementsByName('notificationType');

            var eventType = '';
            if (radios[0].checked) {
                eventType = radios[0].value;
            } else {
                eventType = radios[1].value;
            }

            await pages.config.setConfig({
                entityId: eventType,
                contentUrl: "https://YourSite/Connector/Setup",
                removeUrl:"https://YourSite/Connector/Setup",
                configName: eventType
                });

            pages.getConfig().then(async (config) {
                // We get the Webhook URL from config.webhookUrl which needs to be saved. 
                // This can be used later to send notification.
            });

            saveEvent.notifySuccess();
        });

        pages.config.registerOnRemoveHandler(function (removeEvent) {
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

ページの読み込みの一部としてユーザーを認証するには、[タブの認証フロー](~/tabs/how-to/authentication/auth-flow-tab.md)を参照して、ページが埋め込まれたときにサインインを統合してください。

> [!NOTE]
> TeamsJS v.2.0.0 より前は、クライアント間の互換性上の理由から、コードを呼び出す `microsoftTeams.authentication.registerAuthenticationHandlers()` 前に URL と成功または失敗のコールバック メソッドを使用して呼び出す `authenticate()` 必要があります。 TeamsJS v.2.0.0 以降では、 *registerAuthenticationHandlers* は、必要な認証パラメーターを使用して [authentication()](/javascript/api/@microsoft/teams-js/authentication#@microsoft-teams-js-authentication-authenticate) を直接呼び出すのを優先して非推奨になりました。

#### <a name="getconfig-response-properties"></a>`getConfig` 件の応答のプロパティ

>[!NOTE]
>このメソッドを `getConfig` タブから呼び出すと、呼び出しによって返されるパラメーターは異なり、 [参照](/javascript/api/@microsoft/teams-js/pages#@microsoft-teams-js-pages-getconfig)に記載されているものとは異なります。

`getConfig` 件の応答のプロパティのパラメーターとその詳細についてはとおりです。

| パラメーター   | 詳細 |
|-------------|---------|
| `entityId`       | `setConfig()` を呼び出す場合にコードで設定されたエンティティ ID。 |
| `configName`  | `setConfig()` を呼び出す場合にコードで設定される構成名。 |
| `contentUrl` | `setConfig()` を呼び出す場合にコードによって設定される、構成ページの URL。 |
| `webhookUrl` | コネクタ用に作成された Webhook の URL。Webhook URL を使用して、構造化された JSON を投稿し、チャネルにカードを送信します。アプリケーションが正常にデータを返した場合のみ `webhookUrl` が返されます。 |
| `appType` | 返される`mail`値は、 `groups``teams` Office 365 メール、Office 365 グループ、または Teams にそれぞれ対応できます。 |
| `userObjectId` | コネクタの設定を開始した Office 365 ユーザに対応する一意の ID。セキュリティで保護されている必要があります。この値は、お客様のサービスで設定を行った Office 365 のユーザーを関連付けるために使用できます。 |

#### <a name="handle-edits"></a>編集の処理

コードは、既存のコネクタ構成を編集するために戻るユーザーを処理する必要があります。 これを行うには、初期構成時に以下のパラメーターを指定して `microsoftTeams.pages.config.setConfig()` を呼び出します。

* `entityId` は、ユーザーがサービスによって構成および理解されたことを表すカスタム ID です。
* `configName` は、構成コードで取得できる名前です。
* `contentUrl` は、ユーザーが既存のコネクタ構成を編集したときに読み込まれるカスタム URL です。

この呼び出しは、保存イベント ハンドラーの一部として行われます。 次に、`contentUrl` がロードされると、コードは `getConfig()` を呼び出して、構成ユーザー インターフェイスの設定やフォームを事前に入力する必要があります。

#### <a name="handle-removals"></a>削除の処理

ユーザーが既存のコネクタ構成を削除したときに、イベント ハンドラーを実行できます。 このハンドラーは、`microsoftTeams.pages.config.registerOnRemoveHandler()` メソッドを実装することで登録します。 このハンドラーは、データベースからエントリを削除するなどのクリーンアップ操作を実行するために使用されます。

### <a name="include-the-connector-in-your-manifest"></a>マニフェストにコネクタを含める

開発者ポータル ()<https://dev.teams.microsoft.com> から自動生成された *Teams アプリ マニフェスト* をダウンロードします。 アプリをテストまたは発行する前に、次の手順を実行します。

1. [アイコンを 2 つ含めます](../../concepts/build-and-test/apps-package.md#app-icons)。
1. マニフェストの `icons` 部分を、URL ではなくアイコンのファイル名に変更します。

次の *manifest.json* ファイルには、アプリのテストと送信に必要な要素が含まれています。

> [!NOTE]
> 次の例の `id` と `connectorId` を、コネクタの GUID に置き換えます。

#### <a name="example-of-manifestjson-with-connector"></a>コネクタを使用した manifest.json の例

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

## <a name="test-your-connector"></a>コネクタをテストする

コネクタをテストするには、他のアプリと同じ方法でコネクタをチームにアップロードします。「[マニフェストにコネクタを含める](#include-the-connector-in-your-manifest)」での指示どおりに修正した 2 つのアイコン ファイルとコネクタ開発者ダッシュボードからマニフェスト ファイルを使用して、.zip パッケージを作成できます。

アプリをアップロードしたら、任意のチャネルからコネクタ リストを開きます。 一番下までスクロールして、アプリが **[アップロード済み]** セクションに表示されていることを確認します。

![コネクタ ダイアログ ボックスの [アップロード済み] セクションのスクリーンショット](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> フローは、ホストされたエクスペリエンスとして Teams 内で完全に発生します。

`HttpPOST` アクションが正しく動作していることを確認するために、[お使いのコネクタにメッセージを送信します](~/webhooks-and-connectors/how-to/connectors-using.md)。

ステップ [バイ ステップ ガイド](../../sbs-teams-connectors.yml) に従って、Teams でコネクタを作成してテストします。

## <a name="distribute-webhook-and-connector"></a>Webhook とコネクタを配布する

1. チームに[受信 Webhook を直接セットアップ](~/webhooks-and-connectors/how-to/add-incoming-webhook.md#create-an-incoming-webhook)します。

1. [構成ページ](~/webhooks-and-connectors/how-to/connectors-creating.md?#integrate-the-configuration-experience)を追加し、受信 Webhook をOffice 365 コネクタに発行します。

1. [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) への提出の一部としてコネクタをパッケージ化して公開します。

## <a name="code-sample"></a>コード サンプル

次のテーブルに、サンプル名とその説明を示します。

|**サンプルの名前** | **説明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| コネクタ | Teams チャネルに通知を生成する Office 365 コネクタのサンプル。| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| 汎用コネクタのサンプル |Webhook をサポートするすべてのシステムに対して簡単にカスタマイズできる汎用コネクタのサンプル コード。| | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

[ステップバイステップ ガイド](../../sbs-teams-connectors.yml)に従って、Teams でコネクタを構築してテストします。

## <a name="see-also"></a>関連項目

* [メッセージを作成して送信する](~/webhooks-and-connectors/how-to/connectors-using.md)
* [受信 Webhook を作成する](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Office 365 コネクタを作成する](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [管理者がコネクタを有効または無効にする方法](/MicrosoftTeams/office-365-custom-connectors#enable-or-disable-connectors-in-teams)
* [管理者が組織内でカスタム コネクタを発行する方法](/MicrosoftTeams/office-365-custom-connectors)
