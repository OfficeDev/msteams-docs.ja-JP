---
title: Office 365 コネクタ
description: Microsoft Teams で Office 365 コネクタを使い始める方法について説明します。
keywords: Teams o365 コネクタ
ms.date: 04/19/2019
ms.openlocfilehash: 9c18a4c0dfda449c1507b26e78889cfab56ffd5f
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "44590852"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>Microsoft Teams 用 Office 365 コネクタの作成

>Microsoft Teams アプリを使用すると、既存の Office 365 コネクタを追加したり、Microsoft Teams に含める新しい Office コネクタを作成したりできます。 詳細については[、「独自のコネクタを作成](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector)する」を参照してください。

## <a name="adding-a-connector-to-your-teams-app"></a>Teams アプリにコネクタを追加する

登録済みのコネクタを Teams アプリ パッケージの一部として配布できます。 スタンドアロンソリューションとして、または Teams で利用できるいくつかの[機能](~/concepts/extensibility-points.md)の1つとして、appsource の提出の一環として、コネクタを[パッケージ化](~/concepts/build-and-test/apps-package.md)して[発行](~/concepts/deploy-and-publish/apps-publish.md)することができます。また、teams 内でアップロードするために直接ユーザーに提供することもできます。

コネクタを配布するには、[コネクタ開発者ダッシュボード](https://outlook.office.com/connectors/home/login/#/publish)を使用して登録する必要があります。 既定では、コネクタが登録されると、そのコネクタは、それらをサポートするすべての Office 365 製品 (Outlook と Teams を含む) で動作していると見なされます。 そのようになって_いない_場合に、Microsoft teams でのみ動作するコネクタを作成する必要がある場合は、 [Teams ストアの提出のサポート](mailto:TeamsSubSupport@microsoft.com)を直接ご連絡ください。

> [!IMPORTANT]
> コネクタ開発者ダッシュボードで [**保存**] を選択すると、コネクタが登録されます。 AppSource でコネクタを公開する場合は、「 [Microsoft Teams アプリを AppSource に発行](~/concepts/deploy-and-publish/apps-publish.md)する」の手順に従ってください。 アプリを AppSource で公開せず、組織に直接配布するだけではなく、[組織に公開](#publish-connectors-for-your-organization)することもできます。 組織への発行のみを希望する場合は、コネクタのダッシュボードで、これ以上の操作は必要ありません。

### <a name="integrating-the-configuration-experience"></a>構成作業の統合

ユーザーは、Teams クライアントを離れることなく、コネクタ構成作業全体を完了します。 この操作を実現するために、Teams は構成ページを iframe 内に直接埋め込みます。 操作の順序は次のとおりです。

1. ユーザーがコネクタをクリックして、構成プロセスを開始します。
2. Teams は、構成の操作を行に読み込みます。
3. ユーザーは、web experience と対話して構成を完了します。
4. ユーザーが [保存] を押すと、コード内でコールバックがトリガーされます。
5. コードでは、webhook 設定 (以下に記載) を取得することによって、save イベントを処理します。 コードでは、後でイベントを post するために webhook を格納する必要があります。

既存の web 構成機能を再利用するか、Teams で特別にホストされる個別のバージョンを作成することができます。 コードは次のようにする必要があります。

1. Microsoft Teams JavaScript SDK を含めます。 これにより、コードは、現在のユーザー/チャネル/チームコンテキストを取得し、認証フローを開始するなどの一般的な操作を実行するための Api にアクセスできます。 `microsoftTeams.initialize()` を呼び出して SDK を初期化します。
2. `microsoftTeams.settings.setValidityState(true)`[保存] ボタンを有効にする場合に呼び出されます。 これは、選択範囲またはフィールドの更新など、有効なユーザー入力に対する応答として実行する必要があります。
3. `microsoftTeams.settings.registerOnSaveHandler()`ユーザーが [保存] をクリックしたときに呼び出されるイベントハンドラーを登録します。
4. `microsoftTeams.settings.setSettings()`を呼び出して、コネクタの設定を保存します。 ここに保存される内容は、ユーザーがコネクタの既存の構成を更新しようとした場合に、[構成] ダイアログに表示される内容にもなります。
5. `microsoftTeams.settings.getSettings()`URL 自体を含む webhook プロパティをフェッチする呼び出し。 Save イベントの実行時に加えて、この関数は、ページが最初に読み込まれたときに再構成したときにも呼び出す必要があります。
6. オプション`microsoftTeams.settings.registerOnRemoveHandler()`ユーザーがコネクタを削除したときに呼び出されるイベントハンドラーを登録します。 このイベントは、サービスにクリーンアップアクションを実行する機会を提供します。

#### <a name="getsettings-response-properties"></a>`GetSettings()`応答のプロパティ

>[!Note]
>この呼び出しによって返されるパラメーター `getSettings` は、このメソッドをタブから呼び出した場合とは異なり、[ここ](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest)に記載されているものとは異なります。

| パラメーター   | 詳細 |
|-------------|---------|
| `entityId`       | 呼び出し時にコードによって設定されたエンティティ ID `setSettings()` 。 |
| `configName`  | 呼び出し時にコードによって設定された構成名 `setSettings()` 。 |
| `contentUrl` | 呼び出し時にコードによって設定された、構成ページの URL`setSettings()` |
| `webhookUrl` | このコネクタ用に作成された webhook URL。 Webhook URL を保持し、それを使用して、カードをチャネルに送信するように構造化された JSON をポストします。 は、アプリケーションが正常に返される場合にのみ返されます。 |
| `appType` | 返される値には、Office 365 メール、Office 365 グループ、Microsoft Teams のそれぞれに対応する `mail`、`groups`、`teams` を指定できます。 |
| `userObjectId` | これは、コネクタのセットアップを開始した Office 365 ユーザーに対応する一意の id です。 セキュリティで保護する必要があります。 この値は、構成をセットアップした Office 365 内のユーザーをサービス内のユーザーに関連付けるために使用できます。 |

ページの読み込みの一環としてユーザーを認証する必要がある場合は、ページが埋め込まれているときにログインを統合する方法の詳細については、[このリンク](~/tabs/how-to/authentication/auth-flow-tab.md)を参照してください。

> [!NOTE]
> クライアント間の互換性に関する理由から、コードは、 `microsoftTeams.authentication.registerAuthenticationHandlers()` URL と、成功/失敗のコールバックメソッドを呼び出してから呼び出す必要があり `authenticate()` ます。

#### <a name="handling-edits"></a>編集の処理

コードは、既存のコネクタ構成を編集するために戻るユーザーを処理する必要があります。 これを行うには、 `microsoftTeams.settings.setSettings()` 次のパラメーターを使用して、初期構成中にを呼び出します。

- `entityId`は、サービスによって認識されるカスタム ID であり、ユーザーが構成した内容を表します。
- `configName`は、構成コードが取得できるフレンドリ名です。
- `contentUrl`は、ユーザーが既存のコネクタ構成を編集したときに読み込まれるカスタム URL です。 この URL を使用して、コードが編集ケースを簡単に処理できるようにすることができます。

通常、この呼び出しは、save イベントハンドラーの一部として行われます。 次に、 `contentUrl` 上記のコードが読み込まれたときに、 `getSettings()` 設定またはフォームを構成 UI に事前に設定するためのコードを呼び出す必要があります。

#### <a name="handling-removals"></a>削除の処理

ユーザーが既存のコネクタ構成を削除したときに、必要に応じてイベントハンドラーを実行することができます。 このハンドラーは、を呼び出して登録し `microsoftTeams.settings.registerOnRemoveHandler()` ます。 このハンドラーは、データベースからエントリを削除するなど、クリーンアップ操作を実行するために使用できます。

### <a name="including-the-connector-in-your-manifest"></a>マニフェストにコネクタを含める

自動生成された Teams アプリのマニフェストは、ポータルからダウンロードできます。 ただし、これを使用してアプリをテストまたは発行するには、次の操作を実行する必要があります。

- 「[アイコン](~/concepts/build-and-test/apps-package.md#icons)」の説明に従い、アイコンを 2 つ含めます。
- マニフェストの `icons` の部分を変更し、アイコンの URL ではなくアイコンのファイル名を参照するようにします。

次の manifest.json ファイルには、アプリをテストして送信するために必要な基本的な要素が含まれています。

> [!NOTE]
> 次の例の `id` と `connectorId` を、コネクタの GUID に置き換えます。

#### <a name="example-manifestjson-with-connector"></a>コネクタを使用した manifest.json の例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

構成機能を起動できるようになりました。 このフローは、Microsoft Teams 内でホストされる環境として全面的に発生することに注意してください。

アクションが正常に動作していることを確認するには `HttpPOST` 、[コネクタにメッセージを送信](~/webhooks-and-connectors/how-to/connectors-using.md)します。

## <a name="publish-connectors-for-your-organization"></a>組織の公開コネクタ

場合によっては、コネクタアプリを公開する AppSource/Store に公開する必要はありませんが、組織内のユーザーのみが使用できるようにする必要があります。 そのような場合は、カスタムコネクタアプリを[組織のアプリカタログ](~/concepts/deploy-and-publish/apps-publish.md)にアップロードすることができます。 このようにすると、コネクタアプリはその組織のみが使用できるようになり、パブリックストアにコネクタを公開する必要はありません。

アプリパッケージをアップロードした後、チーム内でコネクタを構成して使用するには、次の手順を実行して組織のアプリカタログからインストールできます。

1. 左端の垂直ナビゲーションバーから [アプリ] アイコンを選択します。
1. [**アプリ**] ウィンドウで、[**コネクタ**] を選択します。
1. 追加するコネクタを選択すると、ポップアップダイアログウィンドウが表示されます。
1. [**チームバーに追加] を**選択します。
1. 次のダイアログウィンドウで、チームまたはチャネルの名前を入力します。
1. ダイアログウィンドウの右下隅にあるコネクタバーの**設定**を選択します。
1. このコネクタは、「 &#9679;&#9679;&#9679; =」の「> その*他のオプション*コネクタのすべてのコネクタ」のセクションで使用でき  =>  *Connectors*  =>  *All*  =>  *Connectors for you team*ます。 このセクションまでスクロールするか、コネクタアプリを検索することによって移動できます。
1. コネクタを構成または変更するには、[**構成**] バーを選択します。
