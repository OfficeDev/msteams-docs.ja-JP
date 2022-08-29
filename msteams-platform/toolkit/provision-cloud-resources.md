---
title: Visual Studio 用 Teams ツールキットを使用して、Teams ツールキットでクラウド リソースをプロビジョニングする
author: surbhigupta
description: このモジュールでは、Teams ツールキットを使用してクラウド リソースをプロビジョニングする方法について説明します。 また、Visual Studio でリソースを作成し、リソースのプロビジョニングをカスタマイズする方法についても説明します。
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 7dfc5817fb8872a782b28c113c270a318e3d5078
ms.sourcegitcommit: 52a11f7614c43172bc2d57401a60d569db5310a9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2022
ms.locfileid: "67291698"
---
# <a name="provision-cloud-resources-using-visual-studio"></a>Visual Studio を使用してクラウド リソースをプロビジョニングする

TeamsFx は Azure および Microsoft 365 クラウドと統合されています。これにより、単一のコマンドでアプリケーションを Azure に配置できます。 TeamsFx は、Azure Resource Manager と統合されています。これにより、Azure リソースをプロビジョニングできます。 コード アプローチでは、アプリケーションにクラウド リソースが必要です。

## <a name="prerequisites"></a>前提条件

クラウド リソースのプロビジョニングに必要なツールの一覧を次に示します。

| &nbsp; | インストール | 使用するには... |
| --- | --- | --- |
| &nbsp; | **必須** | &nbsp; |
| &nbsp; | Visual Studio 2022 バージョン 17.3 | Visual Studio のエンタープライズ エディションをインストールし、"ASP.NET" ワークロードと Microsoft Teams 開発ツールをインストールできます。 |
| &nbsp; | [Microsoft 365 開発者アカウント](https://developer.microsoft.com/en-us/microsoft-365/dev-program) | アプリをインストールするための適切なアクセス許可を持つ Teams アカウントにアクセスします。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams を使用して、チャット、会議、通話用のアプリを通じて共同作業を行うすべてのユーザーと 1 か所で共同作業を行うことができます。 |
| &nbsp; | Teams ツールキット | アプリのプロジェクト スキャフォールディングを作成する Visual Studio 拡張機能。 最新バージョン​​を使用します。 |
| &nbsp; | [Azure アカウント](https://portal.azure.com/) | 有効なサブスクリプションのある Azure アカウント。 |

## <a name="steps-to-provision-cloud-resources"></a>クラウド リソースをプロビジョニングする手順

次の手順は、Visual Studio を使用してクラウド リソースをプロビジョニングするのに役立ちます。

### <a name="sign-in-to-your-microsoft-365-account"></a>Microsoft 365 アカウントにサインインする

1. Visual Studio 2022。
2. Microsoft Teams アプリ プロジェクトを開きます。
3. **[プロジェクト]** を選択します。
4. **[Teams ツールキット]** を選択します。
5. **[Teams アプリの依存関係を準備する]** を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare-app-dependencies.png" alt-text="Teams アプリの依存関係を準備する":::

7. **[サインイン...]** を選択して、Azure アカウントにサインインします。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare1.png" alt-text="Microsoft 365 にサインインする":::

    > [!NOTE]
    > 既にログインしている場合、ユーザー名が表示されます。または、同じものを選択してアカウントを切り替えることができます。

8. 既定の Web ブラウザーが開き、アカウントに[サインイン](https://developer.microsoft.com/en-us/microsoft-365/dev-program)できます。
9. アカウントにサインインしたら、**[続行]** を選択します。

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-signin-M365.png" alt-text="[続行] を選択して確認する":::

### <a name="sign-in-to-your-azure-account"></a>Azure アカウントにサインインする

1. Visual Studio 2022 を開きます。
2. Teams アプリ プロジェクトを開きます。
3. **[プロジェクト]** を選択します。
4. **[Teams ツールキット]** を選択します。
5. **[クラウドにプロビジョニング]** を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud.png" alt-text="Azure アカウントにサインインする":::

6. **[サインイン...]** を選択して、Azure アカウントにサインインします。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-start.png" alt-text="Azure アカウントにサインインする":::

   > [!NOTE]
   > 既にログインしている場合、ユーザー名が表示されます。または、アカウントを切り替えることができます。

7. 資格情報を使用して Azure アカウントにサインインします。 ブラウザーは自動的に閉じます。

### <a name="to-provision-cloud-resources"></a>クラウド リソースをプロビジョニングする方法

1. Visual Studio でプロジェクトを開いた後、**[プロジェクト]** を選択します。
2. **[Teams ツールキット]** を選択します
3. **[クラウドにプロビジョニング]** を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud1.png" alt-text="クラウドでのプロビジョニング":::

4. **[プロビジョニング]** ダイアログには、Azure アカウント内のすべてのサブスクリプションの一覧が表示されます。
5. **リソース グループ** を選択するか、新しく作成できます。
6. **[プロビジョニング]** を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-select-subscription.png" alt-text="リソース グループの選択":::

7. このダイアログでは、Azure の使用状況に従って料金が追加される可能性があることを警告します。 **[プロビジョニング]** を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-warning.png" alt-text="プロビジョニングの警告":::

   Azure クラウドでリソースを作成するプロビジョニング プロセスには、時間がかかる場合があります。

8. Teams ツールキットの出力ウィンドウを確認して、進行状況を監視します。
9. プロビジョニングが完了すると、メッセージが表示されます。 **[プロビジョニングされたリソースの表示]** を選択して、プロビジョニングされたすべてのリソースを表示します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-provision-success.png" alt-text="プロビジョニングされたリソースの表示":::

### <a name="create-resources"></a>リソースを作成する

Teams ツールキットまたは TeamsFx CLI でプロビジョニング コマンドをトリガーすると、次のリソースを作成できます。

* Microsoft 365 テナントの Microsoft Azure Active Directory (Azure AD) アプリケーション。
* Microsoft 365 テナントの Teams プラットフォームの Teams アプリの登録。
* 選択した Azure サブスクリプションの Azure リソース。

新しいプロジェクトを作成するときに、Azure リソースも作成する必要があります。 Azure Resource Manager (ARM) テンプレートは、すべての Azure リソースを定義し、プロビジョニング中に必要な Azure リソースを作成するのに役立ちます。

### <a name="create-resource-for-teams-tab-application"></a>Teams タブ アプリケーションのリソースを作成する

| Resource | 用途 | 説明 |
| --- | --- | --- |
| アプリ サービス プラン | タブの Web アプリをホストします。 | 対象外 |
| アプリ サービス | Blazor タブ アプリと、他のサービスへのアクセスに役立つシンプルな認証サーバーをホストします。 | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。 |
| ID を管理する | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有します。 |

### <a name="create-resources-for-teams-message-extension-application"></a>Teams メッセージ拡張機能アプリケーションのリソースを作成する

| Resource | 用途 | 説明 |
| --- | --- | --- |
| Azure ボット | ボット フレームワークで、アプリをボットとして登録します。 | ボットを Teams に接続します。 |
| アプリ サービス プラン | Web ボット アプリをホストします。 | 対象外 |
| アプリ サービス | ボット アプリをホストします。 | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。 |
| ID を管理する | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有します。 |

### <a name="create-resources-for-teams-command-bot-application"></a>Teams コマンド ボット アプリケーションのリソースを作成する

| Resource | 用途 | 説明 |
| --- | --- | --- |
| Azure ボット | ボット フレームワークで、アプリをボットとして登録します。 | ボットを Teams に接続します。 |
| アプリ サービス プラン | Web ボット アプリをホストします。 | 対象外 |
| アプリ サービス | ボット アプリをホストします。 | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。 |
| ID を管理する | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有します。 |

### <a name="create-resources-for-teams-notification-bot-with-http-trigger-web-api-server-application"></a>HTTP トリガー (Web API サーバー) アプリケーションを使用して Teams 通知ボットのリソースを作成する

| Resource | 用途 | 説明 |
| --- | --- | --- |
| Azure ボット | ボット フレームワークで、アプリをボットとして登録します。 | ボットを Teams に接続します。 |
| アプリ サービス プラン | Web ボット アプリをホストします。 | 対象外 |
| アプリ サービス | ボット アプリをホストします。 | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。 |
| マネージド ID | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有します。 |

### <a name="create-resource-for-teams-notification-bot-with-http-trigger-azure-function-application"></a>HTTP トリガー (Azure 関数) アプリケーションを使用して Teams 通知ボットのリソースを作成する

| Resource | 用途 | 説明 |
| --- | --- | --- |
| Azure ボット | ボット フレームワークで、アプリをボットとして登録します。 | ボットを Teams に接続します。 |
| ID を管理する | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有されます。 |
| ストレージ アカウント | 関数アプリの作成に役立ちます。 | 対象外 |
| アプリ サービス プラン | 関数ボット アプリをホストします。 | 対象外 |
| 関数アプリ | ボット アプリをホストします。 | -他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。<br>-クロスオリジン リソース共有 (CORS) ルールを追加して、タブ アプリからの要求を許可します。<br>-Teams アプリからの要求のみを許可する認証設定を追加します。<br>-TeamsFx SDK で必要なアプリ設定を追加します。 |

### <a name="create-resource-for-teams-notification-bot-with-timer-trigger-azure-function-application"></a>タイマー トリガー (Azure 関数) アプリケーションを使用して Teams 通知ボットのリソースを作成する

| Resource | 用途 | 説明 |
| --- | --- | --- |
| Azure ボット | ボット フレームワークで、アプリをボットとして登録します。 | ボットを Teams に接続します。 |
| ID を管理する | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有します。 |
| ストレージ アカウント | 関数アプリの作成に役立ちます。 | 該当なし。 |
| アプリ サービス プラン | 関数ボット アプリをホストします。 | 対象外 |
| 関数アプリ | ボット アプリをホストします。 | -他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。<br>-クロスオリジン リソース共有 (CORS) ルールを追加して、タブ アプリからの要求を許可します。<br>-Teams アプリからの要求のみを許可する認証設定を追加します。<br>-TeamsFx SDK で必要なアプリ設定を追加します。 |

### <a name="create-resources-for-teams-notification-bot-with-http-trigger--timer-trigger-azure-function-application"></a>HTTP トリガーとタイマー トリガー (Azure 関数) アプリケーションを使用して Teams 通知ボットのリソースを作成する

| Resource | 用途 | 説明 |
| --- | --- | --- |
| Azure ボット | ボット フレームワークで、アプリをボットとして登録します。 | ボットを Teams に接続します。 |
| ID を管理する | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有します。 |
| ストレージ アカウント | 関数アプリの作成に役立ちます。 | 対象外 |
| アプリ サービス プラン | 関数ボット アプリをホストします。 | 対象外 |
| 関数アプリ | ボット アプリをホストします。 | -他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。<br>-クロスオリジン リソース共有 (CORS) ルールを追加して、タブ アプリからの要求を許可します。<br>-Teams アプリからの要求のみを許可する認証設定を追加します。<br>-TeamsFx SDK で必要なアプリ設定を追加します。 |

### <a name="manage-your-resources"></a>リソースを管理する

[Azure ポータル](https://portal.azure.com/)にサインインし、Teams ツールキットによって作成されたすべてのリソースを管理できます。

* 既存の一覧のリソース グループまたは作成した新しいリソース グループを選択できます。
* 選択したリソース グループの詳細は、コンテンツ テーブルの概要セクションで確認できます。

### <a name="customize-resource-provision"></a>リソースのプロビジョニングをカスタマイズする

Teams ツールキットを使用すると、コード アプローチのインフラストラクチャを使用して、プロビジョニングする Azure リソースを定義できます。 Teams ツールキットの構成は、要件に従って変更できます。

Teams ツールキットでは、ARM テンプレートを使用して Azure リソースを定義します。 ARM テンプレートは、プロジェクトのインフラストラクチャと構成を定義する一連の Bicep ファイルです。 ARM テンプレートを変更することで、Azure リソースをカスタマイズできます。 詳細については、[Bicep に関するドキュメント](/azure/azure-resource-manager/bicep)を参照してください。

ARM を使用したプロビジョニングには、次のファイル、パラメーター、テンプレートのセットを変更する必要があります。

* パラメーターをテンプレートに渡すための `.fx/configs` フォルダーにある ARM パラメーター ファイル (`azure.parameters.{your_env_name}.json`)。
* `templates/azure` フォルダーにある ARM テンプレート ファイルには、次のファイルが含まれています。

| File | 職務 | カスタマイズを許可する |
| --- | --- | --- |
| main.bicep | Azure リソースのエントリ ポイントを指定します。 プロビジョニング | はい |
| provision.bicep | Azure リソースを作成して構成します。 | はい |
| config.bicep | TeamsFx に必要な構成を Azure リソースに追加します。 | はい |
| provision/xxx.bicep | `provision.bicep` によって使用される各 Azure リソースを作成して構成します。 | はい |
| teamsfx/xxx.bicep | `config.bicep` によって使用される各 Azure リソースに TeamsFx の必要な構成を 追加します。| 不要 |

> [!NOTE]
> リソースまたは機能をプロジェクトに追加すると、`teamsfx/xxx.bicep` が再生成されます。 Bicep ファイルを変更するには、Git を使用して `teamsfx/xxx.bicep` ファイルに対する変更を追跡できます。 これにより、プロジェクトにリソースや機能を追加するときに変更が失われることはありません。

ARM テンプレート ファイルでは、パラメーターにプレースホルダーが使用されます。 プレースホルダーの目的は、新しい環境で新しいリソースを作成できるようにすることです。 実際の値は `.fx/states/state.{env}.json` ファイルから解決されます。

### <a name="azure-ad-application-related-parameters"></a>Azure AD アプリケーション関連のパラメーター

| パラメーター名 | 既定値のプレース ホルダー | プレース ホルダーの意味 | カスタマイズする方法 |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | プロビジョニング中に作成されたアプリの Azure AD アプリ クライアント ID。 | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | プロビジョニング中に作成されたアプリの Azure AD アプリ クライアント シークレット。 | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | アプリの Azure AD アプリのテナント ID。 | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | アプリの Azure AD アプリの OAuth 機関ホスト。 | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | プロビジョニング中に作成されたボットの Azure AD アプリ クライアント ID。 | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | プロビジョニング中に作成されたボットの Azure AD アプリ クライアント シークレット。 | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-bot) |

### <a name="reference-environment-variables-in-parameter-files"></a>パラメーター ファイル内の参照環境変数

値がシークレットの場合、パラメーター ファイルにハードコーディングする必要はありません。 パラメーター ファイルでは、環境変数からの値の参照がサポートされています。 Teams ツールキットのパラメーター値で構文 `{{$env.YOUR_ENV_VARIABLE_NAME}}` を使用して、現在の環境変数から解決できます。

次の例では、環境変数 `DB_CONNECTION_STRING` からパラメーターの値 `mySelfHostedDbConnectionString` を読み取ります。

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

### <a name="customize-arm-template-files"></a>ARM テンプレート ファイルをカスタマイズする

定義済みのテンプレートがアプリケーション要件を満たしていない場合は、`templates/azure` フォルダーにある ARM テンプレートをカスタマイズできます。 たとえば、ARM テンプレートをカスタマイズして、アプリ用の追加の Azure リソースを作成できます。 ARM テンプレートの作成に使用される Bicep 言語の基本的な知識が必要です。

TeamsFx ツールが正しく機能することを確認するには、次の要件を満たす ARM テンプレートをカスタマイズします。

* フォルダー構造とファイル名が変更されていないことを確認します。 プロジェクトにリソースまたは機能をさらに追加すると、既存のファイルに新しいコンテンツが追加されることがあります。
* 自動生成されたパラメーターの名前とそのプロパティ名がハングしないようにします。 自動生成されたパラメーターは、プロジェクトにリソースまたは機能をさらに追加するときに使用できます。
* 自動生成された ARM テンプレートの出力も変更されていないことを確認します。 ARM テンプレートに出力をさらに追加できます。 出力は `.fx/states/state.{env}.json` で、マニフェスト ファイルの展開や検証などの他の機能で使用できます。

### <a name="customize-teams-app"></a>Teams アプリをカスタマイズする

自分で作成した Azure AD アプリを使用するように構成スニペットを追加することで、ボットまたは Teams アプリをカスタマイズできます。 これは、次の方法で実行できます。

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>ボットに既存の Azure AD アプリを使用する

次の構成スニペット `.fx/configs/config.{env}.json` を追加して、Teams アプリ用に作成した Azure AD アプリを使用できます。 Azure AD アプリを作成するには、リンク <https://aka.ms/teamsfx-existing-aad-doc> に移動します。

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

スニペットを追加した後、関連する環境変数にクライアント シークレットを追加します。これにより、Teams ツールキットがプロビジョニング中に実際のクライアント シークレットを解決できるようにします。

> [!NOTE]
> 複数の環境で同じ Azure AD アプリを共有しないようにしてください。 Azure AD アプリを更新するアクセス許可がない場合は、Azure AD アプリを手動で更新する手順を含む警告が表示されます。 プロビジョニング後に Azure AD アプリを更新するには、この手順に従います。

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Teams アプリに既存の Azure AD アプリを使用する

次の構成スニペット `.fx/configs/config.{env}.json` を追加して、ボット用に作成された Azure AD アプリを使用できます。

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

スニペットを追加した後、Teams ツールキットの関連する環境変数にクライアント シークレットを追加して、プロビジョニング中に実際のクライアント シークレットを解決します。

#### <a name="skip-adding-user-for-sql-database"></a>SQL データベースのユーザーの追加をスキップする

Teams ツールキットが SQL データベースにユーザーを追加しようとしたときに必要なアクセス許可がないというエラーが発生した場合、次の構成スニペットを `.fx/configs/config.{env}.json` に追加して、SQL データベース ユーザーの追加をスキップできます。

```json
"skipAddingSqlUser": true
```

## <a name="see-also"></a>関連項目

* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy-teams-app.md)
* [Visual Studio を使用して Teams アプリ マニフェストを編集する](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Visual Studio 用に Teams アプリをローカルでデバッグする](debug-teams-app-visual-studio.md)
