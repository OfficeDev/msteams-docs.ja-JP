---
title: Teams Toolkit を使用してクラウド リソースをプロビジョニングする
author: MuyangAmigo
description: クラウド リソースをプロビジョニングする
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 24b058957ab0db7ebd2ab9178ac95fe9473257e6
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104120"
---
# <a name="use-teams-toolkit-to-provision-cloud-resources"></a>Teams Toolkit を使用してクラウド リソースをプロビジョニングする

TeamsFx は Azure と Microsoft 365 クラウドと統合されています。これにより、アプリケーションを 1 つのコマンドで Azure に配置できます。 TeamsFx は Azure Resource Managerと統合されており、アプリケーションでコード アプローチに必要な Azure リソースをプロビジョニングできます。  

## <a name="prerequisites"></a>前提条件

* アカウントの前提条件 クラウド リソースをプロビジョニングするには、次のアカウントが必要です。

  * 有効なサブスクリプションを持つアカウントをMicrosoft 365する
  * 有効なサブスクリプションを持つ Azure 詳細については、[アプリを構築するためのアカウントを準備する方法Teams](accounts.md)参照してください。

* バージョン v3.0.0 以降[Teams Toolkitインストール](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)します。

> [!TIP]
> TEAMSアプリ プロジェクトが VS コードで開かれていることを確認します。

## <a name="provision-using-teams-toolkit"></a>Teams Toolkitを使用したプロビジョニング

プロビジョニングは、次のように、Visual Studio Code または TeamsFx CLI のTeams Toolkitで 1 つのコマンドで実行されます。

[Azure ベースのアプリをプロビジョニングする](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8)

## <a name="resource-creation"></a>リソースの作成

Teams Toolkitまたは TeamsFx CLI でプロビジョニング コマンドをトリガーすると、次のリソースを取得できます。

* Microsoft 365 テナントのMicrosoft Azure Active Directory (Azure AD) アプリケーション
* Microsoft 365 テナントのTeams プラットフォームでアプリの登録をTeamsする
* 選択した Azure サブスクリプションの Azure リソース

新しいプロジェクトを作成するときに、すべての Azure リソースを使用できます。 ARM テンプレートは、すべての Azure リソースを定義し、プロビジョニング中に必要な Azure リソースを作成するのに役立ちます。 既存のプロジェクトに [新しい機能リソースを追加](./add-resource.md) すると、更新された ARM テンプレートに最新の変更が反映されます。

> [!NOTE]
> Azure サービスでは、サブスクリプションにコストが発生します。コスト見積もりの詳細については、 [価格計算ツールを](https://azure.microsoft.com/pricing/calculator/)参照してください。

### <a name="resource-creation-for-teams-tab-application"></a>Teams タブ アプリケーションのリソース作成

|Resource|用途|説明 |
|----------|--------------------------------|-----|
| Azure Storage | タブ アプリをホストする | 静的 Web アプリ機能でタブ アプリをホストできるようにします |
| 簡単な認証の App Service プラン | Simple Auth の Web アプリをホストする |該当しない |
| 単純な認証用の Web アプリ | 単純な認証サーバーをホストして、単一ページ アプリケーション内の他のサービスにアクセスする | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します |
| ユーザー割り当て ID | Azure サービス間要求を認証する | さまざまな機能とリソース間で共有 |

### <a name="resource-creation-for-teams-bot-or-message-extension-application"></a>Teams ボットまたはメッセージ拡張機能アプリケーションのリソース作成

|Resource|用途| 説明 |
|----------|--------------------------------|-----|
| Azure ボット サービス | アプリをボット フレームワークにボットとして登録します | ボットをTeamsに接続する |
| ボットの App Service プラン | ボットの Web アプリをホストする |該当なし |
| ボット用 Web アプリ | ボット アプリをホストする | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。 <br /> [TeamsFx SDK](https://www.npmjs.com/package/@microsoft/teamsfx) で必要なアプリ設定を追加します |
| ユーザー割り当て ID | Azure サービス間要求を認証する | さまざまな機能とリソース間で共有 |

### <a name="resource-creation-for-azure-functions-in-the-project"></a>プロジェクト内のAzure Functionsのリソース作成

|Resource|用途| 説明|
|----------|--------------------------------|-----|
| 関数アプリの App Service プラン | 関数アプリをホストする |該当なし |
| 関数アプリ | Azure Functions API をホストする | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。 <br /> クロスオリジン リソース共有 (CORS) ルールを追加して、タブ アプリからの要求を許可する <br /> Teams アプリからの要求のみを許可する認証設定を追加します。 <br /> [TeamsFx SDK](https://www.npmjs.com/package/@microsoft/teamsfx) で必要なアプリ設定を追加します |
| 関数アプリ用の Azure Storage | 関数アプリの作成に必要 |該当しない|
| ユーザー割り当て ID | Azure サービス間要求を認証する | さまざまな機能とリソース間で共有 |

### <a name="resource-creation-for-azure-sql-in-the-project"></a>プロジェクト内のAzure SQLのリソース作成

|Resource|用途 | 説明 |
|----------|--------------------------------|-----|
| Azure SQL サーバー | Azure SQL データベース インスタンスをホストする | すべての Azure サービスがサーバーにアクセスできるようにします |
| Azure SQL データベース | アプリのデータを格納する | ユーザー割り当て ID、読み取りまたは書き込みアクセス許可をデータベースに付与します |
| ユーザー割り当て ID | Azure サービス間要求を認証する | さまざまな機能とリソース間で共有 |

### <a name="resource-creation-for-azure-api-management-in-the-project"></a>プロジェクト内の Azure API Managementのリソース作成

|Resource|用途|
|----------|--------------------------------|
| API 管理サービスのAzure AD アプリケーション | API 管理サービスによって管理される Microsoft Power Platform アクセス API を許可する |
| API 管理サービス | 関数アプリでホストされている API を管理する |
| API 管理製品 | API をグループ化し、使用条件とランタイム ポリシーを定義する |
| API Management OAuth サーバー | Microsoft Power Platform が関数アプリでホストされている API にアクセスできるようにします |
| ユーザー割り当て ID | Azure サービス間要求を認証する |

### <a name="resources-created-when-including-azure-key-vault-in-the-project"></a>Azure Key Vaultをプロジェクトに含めると作成されたリソース

|リソース|このリソースの目的|
|----------|--------------------------------|
| Azure Key Vault Service | 他の Azure Services で使用されるシークレット (Azure AD アプリ クライアント シークレットなど) を管理する |
| ユーザー割り当て ID | Azure サービス間要求を認証する |

## <a name="customize-resource-provision"></a>リソースのプロビジョニングをカスタマイズする

Teams Toolkitを使用すると、コード アプローチとしてインフラストラクチャを使用して、プロビジョニングする Azure リソースと構成方法を定義できます。 このツールでは、ARM テンプレートを使用して Azure リソースを定義します。 ARM テンプレートは、プロジェクトのインフラストラクチャと構成を定義する一連の Bicep ファイルです。 ARM テンプレートを変更することで、Azure リソースをカスタマイズできます。 詳細については、 [bicep ドキュメントを](/azure/azure-resource-manager/bicep)参照してください。

ARM を使用したプロビジョニングには、次のファイル、パラメーター、テンプレートのセットを変更する必要があります。

* テンプレートにパラメーターを渡すための ARM パラメーター ファイル (`azure.parameters.{your_env_name}.json`) はフォルダーにあります `.fx/configs` 。
* このフォルダーにある `templates/azure`ARM テンプレート ファイルには、次のファイルが含まれています。

| ファイル | 職務 | カスタマイズを許可する |
| --- | --- | --- |
| main.bicep | Azure リソースプロビジョニングのエントリ ポイントを指定する | はい |
| provision.bicep | Azure リソースを作成して構成する | はい |
| config.bicep | TeamsFx に必要な構成を Azure リソースに追加する | はい |
| provision/xxx.bicep | 使用される各 Azure リソースを作成して構成する `provision.bicep` | はい |
| teamsfx/xxx.bicep | によって使用される各 Azure リソースに TeamsFx の必要な構成を追加する `config.bicep`| なし |

> [!NOTE]
> リソースまたは機能をプロジェクトに追加すると再生成 `teamsfx/xxx.bicep` され、同じカスタマイズはできません。 Bicep ファイルを変更するには、Git を使用してファイルに対する `teamsfx/xxx.bicep` 変更を追跡できます。これにより、リソースや機能の追加中に変更が失われるのを抑えることができます。

### <a name="customize-arm-parameters-and-templates"></a>ARM パラメーターとテンプレートをカスタマイズする

パラメーター ファイルをカスタマイズし、bicep ファイルをカスタマイズすることで、Azure リソースをカスタマイズできます。

#### <a name="customize-arm-template-parameter-files"></a>ARM テンプレート パラメーター ファイルをカスタマイズする

ツールキットには、Azure リソースをカスタマイズするための定義済みパラメーターのセットが用意されています。 パラメーター ファイルが配置 `.fx/configs/azure.parameters.{env}.json` され、使用可能なすべてのパラメーターがプロパティで `provisionParameters` 定義されます。 定義済みのパラメーターが要件を満たす場合は、パラメーター ファイルをカスタマイズすることをお勧めします。

次の表に、使用可能な定義済みパラメーターの一覧を示します。

| パラメーター名 | 既定値 | パラメーターでカスタマイズできるもの | 値の制約 |
| --- | --- | --- | --- |
| resourceBaseName | 環境ごとに自動生成 | すべてのリソースの既定の名前 | 2 ~ 20 文字の小文字と数字 |
| simpleAuthServerFarmsName | ${resourceBaseName}simpleAuth | 単純な認証アプリ サービス プランの名前 | 1 ~ 40 文字の英数字とハイフン |
| simpleAuthWebAppName | ${resourceBaseName}simpleAuth | 単純な認証 Web アプリの名前 | 2 ~ 60 文字の英数字とハイフン <br /> ハイフンで開始または終了できない |
| simpleAuthSku | F1 | 単純な認証アプリ サービス プランの SKU | 該当しない |
| frontendHostingStorageName | ${resourceBaseName}タブ | フロントエンド ホスティング ストレージ アカウントの名前 | 3 ~ 24 文字の小文字と数字 |
| frontendHostingStorageSku | Standard_LRS | フロントエンド ホスティング ストレージ アカウントの SKU |[使用可能な SKU](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep)|
| functionServerfarmsName | ${resourceBaseName}api | 関数アプリサービス プランの名前 | 1 ~ 40 文字の英数字とハイフン |
| functionServerfarmsSku | Y1 | 関数アプリサービス プランの SKU | 該当なし|
| functionAppName | ${resourceBaseName}api | 関数アプリの名前 | 2 ~ 60 文字の英数字とハイフン <br /> ハイフンで開始または終了できない |
| functionStorageName | ${resourceBaseName}api | 関数アプリのストレージ アカウントの名前 | 3 ~ 24 文字の小文字と数字 |
| functionStorageSku | Standard_LRS | 関数アプリのストレージ アカウントの SKU | [使用可能な SKU](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep) |
| botServiceName | ${resourceBaseName} | Azure ボット サービスの名前 | 2 ~ 64 文字の英数字、アンダースコア、ピリオド、ハイフン <br /> 英数字から始める |
| botServiceSku | F0 | Azure ボット サービスの SKU | [使用可能な SKU](/azure/templates/microsoft.botservice/2021-05-01-preview/botservices?tabs=bicep) |
| botDisplayName | ${resourceBaseName} | ボットの表示名 | 1 ~ 42 文字 |
| botServerfarmsName | ${resourceBaseName}bot | ボットの App Service プランの名前 | 1 ~ 40 文字の英数字とハイフン |
| botWebAppName | ${resourceBaseName}bot | ボットの Web アプリの名前 | 2 ~ 60 文字の英数字とハイフン <br /> ハイフンで開始または終了できない |
| botWebAppSKU | F1 | ボット App Service プランの SKU | 該当しない |
| userAssignedIdentityName | ${resourceBaseName} | ユーザー割り当て ID の名前 | 3 ~ 128 文字の英数字、ハイフン、アンダースコア <br /> 文字または数字で始める |
| sqlServerName | ${resourceBaseName} | Azure SQL サーバーの名前 | 1 ~ 63 文字の小文字、数字、ハイフン <br /> ハイフンで開始または終了できない |
| sqlDatabaseName | ${resourceBaseName} | Azure SQL データベースの名前 | 1 から 128 文字、 <>*%&:\/? または制御文字 <br /> ピリオドまたはスペースで終了できない |
| sqlDatabaseSku | 基本 | Azure SQL データベースの SKU | 該当なし  |
| apimServiceName | ${resourceBaseName} | APIM サービスの名前 | 1 ~ 50 文字の英数字とハイフン <br /> 文字で始まり、英数字で終わる |
| apimServiceSku | 消費 | APIM サービスの SKU | [使用可能な SKU](/azure/templates/microsoft.apimanagement/service?tabs=bicep) |
| apimProductName | ${resourceBaseName} | APIM 製品の名前 | 1 ~ 80 文字の英数字とハイフン <br /> 文字で始まり、英数字で終わる |
| apimOauthServerName | ${resourceBaseName} | APIM OAuth サーバーの名前 | 1 ~ 80 文字の英数字とハイフン <br /> 文字で始まり、英数字で終わる |
| keyVaultSkuName | 標準 | Azure Key Vault Service の SKU 名| |

一方、プロビジョニング中に値が設定された次のパラメーターを使用できます。 これらのプレースホルダーの目的は、新しい環境で新しいリソースを作成できるようにすることです。 実際の値は `.fx/states/state.{env}.json`、 .

##### <a name="azure-ad-application-related-parameters"></a>Azure AD アプリケーション関連のパラメーター

| パラメーター名 | 既定値のプレース ホルダー | プレース ホルダーの意味 | カスタマイズする方法 |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | プロビジョニング中に作成されたアプリのAzure ADアプリ クライアント ID | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | プロビジョニング中に作成されたアプリのAzure AD アプリ クライアント シークレット | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | アプリのAzure AD アプリのテナント ID | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | アプリのAzure AD アプリの OAuth 機関ホスト | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | プロビジョニング中に作成されたボットのAzure AD アプリ クライアント ID | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | プロビジョニング中に作成されたボットのAzure AD アプリ クライアント シークレット | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-bot) |
| apimClientId | {{state.fx-resource-apim.apimClientAADClientId}} | プロビジョニング中に作成された APIM のAzure AD アプリ クライアント ID | プレースホルダーを削除し、実際の値を入力します |
| apimClientSecret | {{state.fx-resource-apim.apimClientAADClientSecret}} | プロビジョニング中に作成された APIM のAzure AD アプリ クライアント シークレット | プレースホルダーを削除し、実際の値を入力します |

##### <a name="azure-resource-related-parameters"></a>Azure リソース関連のパラメーター

| パラメーター名 | 既定値のプレース ホルダー | プレース ホルダーの意味 | カスタマイズする方法 |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | プロビジョニング中に指定したサーバー管理者アカウントをAzure SQLする | プレースホルダーを削除し、実際の値を入力します |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | プロビジョニング中に指定したサーバー管理者パスワードをAzure SQLする | プレースホルダーを削除し、実際の値を入力します |
| apimPublisherEmail | {{state.fx-resource-apim.publisherEmail}} | APIM の発行元の電子メール、既定値は Azure アカウントです | プレースホルダーを削除し、実際の値を入力します |
| apimPublisherName | {{state.fx-resource-apim.publisherName}} | APIM の発行元名、既定値は Azure アカウント | プレースホルダーを削除し、実際の値を入力します |

#### <a name="referencing-environment-variables-in-parameter-files"></a>パラメーター ファイル内の環境変数の参照

パラメーター ファイル内の値をハードコーディングしない場合 (たとえば、値がシークレットの場合など)。 パラメーター ファイルでは、環境変数からの値の参照がサポートされています。 ツールのパラメーター値の構文 `{{$env.YOUR_ENV_VARIABLE_NAME}}` を使用して、現在の環境変数から解決できます。

次の例では、環境変数`DB_CONNECTION_STRING`からパラメーターの値を`mySelfHostedDbConnectionString`読み取ります。

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>ARM テンプレート ファイルをカスタマイズする

定義済みのテンプレートがアプリケーション要件を満たしていない場合は、フォルダーの下 `templates/azure` にある ARM テンプレートをカスタマイズできます。 たとえば、ARM テンプレートをカスタマイズして、アプリ用に追加の Azure リソースを作成できます。 ARM テンプレートの作成に使用される Bicep 言語の基本的な知識が必要です。 Bicep の使用を開始するには、 [bicep のドキュメントを参照してください](/azure/azure-resource-manager/bicep/)。

> [!NOTE]
> ARM テンプレートは、すべての環境で共有されます。 プロビジョニング動作が環境によって異なる場合は、 [条件付きデプロイ](/azure/azure-resource-manager/bicep/conditional-resource-deployment) を使用できます。

TeamsFx ツールが正しく機能するようにするには、次の要件を満たす ARM テンプレートをカスタマイズしてください。 その他のツールを使用してさらなる開発を行う場合は、これらの要件を無視できます。

* フォルダー構造とファイル名は変更しません。 プロジェクトにリソースまたは機能を追加すると、既存のファイルに新しいコンテンツが追加される場合があります。
* 自動生成されたパラメーターの名前とプロパティ名は変更しません。 自動生成されたパラメーターは、プロジェクトにさらにリソースまたは機能を追加するときに使用できます。
* 自動生成された ARM テンプレートの出力は変更しません。 ARM テンプレートに追加の出力を追加できます。 出力は、 `.fx/states/state.{env}.json` 配置、マニフェスト ファイルの検証などの他の機能で使用できます。

### <a name="customization-scenarios"></a>カスタマイズ シナリオ

次のシナリオをカスタマイズできます。

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>ボットに既存のAzure AD アプリを使用する

次の構成スニペットをファイルに`.fx/configs/config.{env}.json`追加して、Teams アプリ用に自分で作成したAzure AD アプリを使用できます。 Azure AD アプリを作成するには、次を参照してください<https://aka.ms/teamsfx-existing-aad-doc>。

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

スニペットを追加した後、ツールがプロビジョニング中に実際のシークレットを解決できるように、関連する環境変数にシークレットを追加します。

> [!NOTE]
> 複数の環境で同じAzure AD アプリを共有しないようにしてください。 Azure AD アプリを更新する権限がない場合は、Azure AD アプリを手動で更新する方法に関する手順に関する警告を受け取ることができます。 手順に従って、プロビジョニング後にAzure AD アプリを更新します。

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Teams アプリに既存のAzure AD アプリを使用する

次の構成スニペットをファイルに`.fx/configs/config.{env}.json`追加して、ボット用に自分で作成したAzure AD アプリを使用できます。

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

前のスニペットを追加した後、プロビジョニング中に実際のシークレットを解決するために、ツールの関連する環境変数にシークレットを追加します。

#### <a name="skip-adding-user-for-sql-database"></a>SQL データベースのユーザーの追加をスキップする

ツールがデータベースにユーザーを追加しようとしたときにアクセス許可エラーが不十分SQL場合は、次の構成スニペットをファイルに`.fx/configs/config.{env}.json`追加して、データベース ユーザーの追加SQLスキップできます。

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>Function App インスタンスの名前を指定する

既定の名前を使用 `contosoteamsappapi` する代わりに、関数アプリ インスタンスに使用できます。

> [!NOTE]
> 環境を既にプロビジョニングしている場合は、名前を指定すると、前に作成したインスタンスの名前を変更する代わりに、新しい関数アプリ インスタンスを作成できます。

次の手順を実行します。

1. 現在の環境用に開きます `.fx/configs/azure.parameters.{env}.json` 。
2. パラメーターの値に新しいプロパティ `functionAppName` を追加します `provisionParameters`。
3. の値として入力します `contosoteamsappapi` 。 `functionAppName`
4. 最後のパラメーター ファイルは、次のスニペットに示されています。

    ```json
    {
        "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "provisionParameters": {
            "value": {
                "functionAppName": "contosoteamsappapi"
                ...
                }
            }
        }
    }
    ```

### <a name="scenerio"></a>シーリオ

他の Azure リソースまたはストレージをアプリケーションに追加するには、

このシナリオでは、Blob データを格納するために Azure 関数バックエンドに Azure ストレージを追加する必要があります。 Azure Storage サポートを使用して Bicep テンプレートを更新する自動フローはありません。 ただし、Bicep ファイルを編集してリソースを追加することはできます。 手順は次のとおりです。

1. タブ プロジェクトを作成します。
2. プロジェクトに関数を追加します。 詳細については、「リソースの [追加](./add-resource.md)」を参照してください。
3. ARM テンプレートで新しいストレージ アカウントを宣言します。 リソース `templates/azure/provision/function.bicep` は直接宣言できます。 他の場所でリソースを自由に宣言できます。

    `````````bicep
    var applicationStorageAccountName = 'myapp${uniqueString(resourceGroup().id)}'
    resource applicationStorageAccount 'Microsoft.Storage/storageAccounts@2021-06-01' = {
        name: applicationStorageAccountName
        location: resourceGroup().location
        kind: 'Storage'
        sku: {
            name: 'Standard_LRS'
        }
    }
    `````````

4. Azure ストレージ接続文字列を使用して Azure 関数アプリの `templates/azure/provision/function.bicep`設定を更新します。 次のスニペットをリソースの`appSettings`配列に`functionApp`追加します。

    ``````````````````bicep
    {
        name: 'MyAppStorageAccountConnectionString'
        value: 'DefaultEndpointsProtocol=https;AccountName=${applicationStorageAccount.name};AccountKey=${listKeys(applicationStorageAccount.id, '2021-06-01').keys[0].value}'
    }
    ```````````````````

5. Azure Storage の出力バインドを使用して関数を更新できます。

## <a name="faq"></a>よくあるご質問 (FAQ)

<br>

<details>

<summary><b>トラブルシューティングの方法</b></summary>

Visual Studio CodeでTeams Toolkitに関するエラーが発生した場合は、エラー通知で **問い合わせ** を選択して、関連するドキュメントに移動できます。 TeamsFx CLI を使用している場合は、ヘルプ ドキュメントを指すハイパーリンクがエラー メッセージの最後に表示されます。 [プロビジョニング ヘルプ ドキュメント](https://aka.ms/teamsfx-arm-help) を直接表示することもできます。

<br>

</details>

<details>

<summary><b>プロビジョニング中に別の Azure サブスクリプションに切り替えるにはどうすればよいですか。</b></summary>

1. 現在のアカウントでサブスクリプションを切り替えるか、ログアウトして新しいサブスクリプションを選択します。
2. 現在の環境を既にプロビジョニングしている場合は、ARM がリソースの移動をサポートしていないため、新しい環境を作成し、プロビジョニングを実行する必要があります。
3. 現在の環境をプロビジョニングしていない場合は、プロビジョニングを直接トリガーできます。

<br>

</details>

<details>

<summary><b>プロビジョニング中にリソース グループを変更するにはどうすればよいですか?</b></summary>

プロビジョニングの前に、ツールから新しいリソース グループを作成するか、既存のリソース グループを使用するかを確認するメッセージが表示されます。 新しいリソース グループ名を指定するか、この手順で既存のリソース グループ名を選択できます。

<br>

</details>

<details>

<summary><b>Sharepoint ベースのアプリをプロビジョニングするにはどうすればよいですか?</b></summary>

[プロビジョニングSharePointベースのアプリに](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4)従うことができます。

> [!NOTE]
> 現時点では、Teams Toolkitを使用した sharepoint フレームワークを使用したアプリのビルドTeams Azure との直接的な統合はありません。ドキュメント内のコンテンツは、SPFx ベースのアプリには適用されません。

<br>

</details>

## <a name="see-also"></a>関連項目

* [Teams アプリをクラウドに展開する](deploy.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
* [Teams プロジェクトで他の開発者と協力する](TeamsFx-collaboration.md)
