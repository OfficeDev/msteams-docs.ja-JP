---
title: Teams Toolkit を使用してクラウド リソースをプロビジョニングする
author: MuyangAmigo
description: クラウド リソースをプロビジョニングする
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 0528654b2867552af802fb95e3a6e47ca3228414
ms.sourcegitcommit: 52af681132e496a57b18f468c5b73265a49a5f44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2022
ms.locfileid: "64590648"
---
# <a name="use-teams-toolkit-to-provision-cloud-resources"></a>Teams Toolkit を使用してクラウド リソースをプロビジョニングする

TeamsFx は Azure および Microsoft 365クラウドと統合され、1 つのコマンドでアプリケーションを Azure に配置できます。 TeamsFx は Azure Resource Manager統合され、アプリケーションでコードアプローチに必要な Azure リソースをプロビジョニングできます。  

## <a name="prerequisites"></a>前提条件

* アカウントの前提条件 クラウド リソースをプロビジョニングするには、次のアカウントが必要です。

  * Microsoft 365有効なサブスクリプションを持つアカウント
  * 有効なサブスクリプションを持つ Azure の詳細については、「アプリを作成するアカウントを準備[するTeamsしてください](accounts.md)。

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> VS コードでTeamsアプリ プロジェクトが開いているか確認します。

## <a name="provision-using-teams-toolkit"></a>サーバーを使用したプロビジョニングTeams Toolkit

プロビジョニングは、次のように、Teams Toolkitまたは TeamsFx CLI Visual Studio Code単一のコマンドで実行されます。

[Azure ベースのアプリをプロビジョニングする](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8)

## <a name="resource-creation"></a>リソースの作成

このコマンドまたは TeamsFx CLI でTeams Toolkitコマンドをトリガーすると、次のリソースを取得できます。

* Microsoft Azure Active DirectoryテナントAzure AD (Microsoft 365) アプリケーション
* TeamsテナントのプラットフォームでアプリMicrosoft 365登録をTeamsする
* 選択した Azure サブスクリプションの Azure リソース

新しいプロジェクトを作成するときに、すべての Azure リソースを使用できます。 このARMテンプレートは、すべての Azure リソースを定義し、プロビジョニング中に必要な Azure リソースを作成するのに役立ちます。 既存の [プロジェクトに新しい機能リソース](./add-resource.md) を追加すると、更新された ARMは最新の変更を反映します。

> [!NOTE]
> Azure サービスでは、サブスクリプションにコストが発生します。コストの見積もりについては、「価格計算 [ツール」を参照してください](https://azure.microsoft.com/pricing/calculator/)。

### <a name="resource-creation-for-teams-tab-application"></a>タブ アプリケーションのリソースTeams作成

|Resource|用途|説明 |
|----------|--------------------------------|-----|
| Azure ストレージ | タブ アプリをホストする | 静的 Web アプリ機能でタブ アプリをホストできます |
| 簡単な認証のためのアプリ サービスプラン | 簡易認証の Web アプリをホストする |該当なし |
| 簡単な認証のための Web アプリ | 単純な認証サーバーをホストして、単一ページ アプリケーション内の他のサービスにアクセスする | 他の Azure リソースにアクセスするユーザー割り当て ID を追加する |
| ユーザー割り当て ID | Azure サービス間要求の認証 | さまざまな機能とリソース間で共有 |

### <a name="resource-creation-for-teams-bot-or-messaging-extension-application"></a>ボットまたはメッセージングTeamsアプリケーションのリソースの作成

|Resource|用途| 説明 |
|----------|--------------------------------|-----|
| Azure ボット サービス | ボット フレームワークにアプリをボットとして登録する | ボットをデバイスに接続Teams |
| ボットのアプリ サービス プラン | ボットの Web アプリをホストする |該当なし |
| ボット用 Web アプリ | ボット アプリをホストする | 他の Azure リソースにアクセスするユーザー割り当て ID を追加します。 <br /> [TeamsFx SDK で必要なアプリ設定を追加する](https://www.npmjs.com/package/@microsoft/teamsfx) |
| ユーザー割り当て ID | Azure サービス間要求の認証 | さまざまな機能とリソース間で共有 |

### <a name="resource-creation-for-azure-functions-in-the-project"></a>プロジェクト内のAzure Functionsリソースの作成

|Resource|用途| 説明|
|----------|--------------------------------|-----|
| 関数アプリのアプリ サービス プラン | 関数アプリをホストする |該当なし |
| 関数アプリ | Azure 関数 API をホストする | 他の Azure リソースにアクセスするユーザー割り当て ID を追加します。 <br /> クロスオリジン リソース共有 (CORS) ルールを追加して、タブ アプリからの要求を許可する <br /> アプリからの要求のみを許可する認証設定をTeamsします。 <br /> [TeamsFx SDK で必要なアプリ設定を追加する](https://www.npmjs.com/package/@microsoft/teamsfx) |
| 関数アプリ用の Azure ストレージ | 関数アプリの作成に必要 |該当なし|
| ユーザー割り当て ID | Azure サービス間要求の認証 | さまざまな機能とリソース間で共有 |

### <a name="resource-creation-for-azure-sql-in-the-project"></a>プロジェクト内のAzure SQLリソースの作成

|Resource|用途 | 説明 |
|----------|--------------------------------|-----|
| Azure SQL サーバー | データベース インスタンスAzure SQLホストする | すべての Azure サービスがサーバーにアクセスできます |
| Azure SQL データベース | アプリのデータを保存する | ユーザーに割り当てられた ID、読み取り、またはデータベースへの書き込みアクセス許可を付与する |
| ユーザー割り当て ID | Azure サービス間要求の認証 | さまざまな機能とリソース間で共有 |

### <a name="resource-creation-for-azure-api-management-in-the-project"></a>プロジェクト内の Azure API Managementリソースの作成

|Resource|用途|
|----------|--------------------------------|
| Azure AD API 管理サービス用のアプリケーション | API 管理サービスによって管理される Microsoft Power Platform アクセス API を許可する |
| API 管理サービス | 関数アプリでホストされる API を管理する |
| API 管理製品 | API をグループ化し、使用条件とランタイム ポリシーを定義する |
| API 管理 OAuth サーバー | Microsoft Power Platform が関数アプリでホストされている API にアクセスできます |
| ユーザー割り当て ID | Azure サービス間要求の認証 |

### <a name="resources-created-when-including-azure-key-vault-in-the-project"></a>Azure リソースをプロジェクトに含Key Vaultリソース

|リソース|このリソースの目的|
|----------|--------------------------------|
| Azure Key Vault サービス | 他の Azure Services で使用されるAzure AD (アプリ クライアント シークレットなど) を管理する |
| ユーザー割り当て ID | Azure サービス間要求の認証 |

## <a name="customize-resource-provision"></a>リソースのプロビジョニングをカスタマイズする

Teams Toolkit、インフラストラクチャをコード アプローチとして使用して、プロビジョニングする Azure リソースと構成方法を定義できます。 このツールは、ARMテンプレートを使用して Azure リソースを定義します。 このARMテンプレートは、プロジェクトのインフラストラクチャと構成を定義する一連のバイセップ ファイルです。 Azure リソースは、テンプレートを変更してARMできます。 詳細については、「バイセ [ップ ドキュメント」を参照してください](/azure/azure-resource-manager/bicep)。

ファイル、パラメーター ARMテンプレートのセットを変更する必要があります。

* ARMテンプレートにパラメーターを渡す場合は、フォルダーにあるパラメーター ファイル (`azure.parameters.{your_env_name}.json`) `.fx/configs` を指定します。
* ARMにあるテンプレート ファイル `templates/azure`には、次のファイルが含まれます。

| ファイル | 職務 | カスタマイズを許可する |
| --- | --- | --- |
| main.bicep | Azure リソースプロビジョニングのエントリ ポイントを提供する | はい |
| provision.bicep | Azure リソースの作成と構成 | はい |
| config.bicep | TeamsFx に必要な構成を Azure リソースに追加する | はい |
| provision/xxx.bicep | 使用する各 Azure リソースを作成および構成する `provision.bicep` | はい |
| teamsfx/xxx.bicep | 使用する各 Azure リソースに TeamsFx 必要な構成を追加する `config.bicep`| 不要 |

> [!NOTE]
> プロジェクトにリソースまたは機能を `teamsfx/xxx.bicep` 追加すると、再生成されます。同じ機能をカスタマイズできない。 バイセップ ファイルを変更するには、Git `teamsfx/xxx.bicep` を使用してファイルに対する変更を追跡できます。これにより、リソースや機能の追加中に変更を失わないのに役立ちます。

### <a name="customize-arm-parameters-and-templates"></a>パラメーター ARMテンプレートをカスタマイズする

パラメーター ファイルをカスタマイズし、二頭上のファイルをカスタマイズすることで、Azure リソースをカスタマイズできます。

#### <a name="customize-arm-template-parameter-files"></a>テンプレート ARM ファイルをカスタマイズする

このツールキットには、Azure リソースをカスタマイズするための一連の定義済みパラメーターが含まれています。 パラメーター ファイルは場所にあり `.fx/configs/azure.parameters.{env}.json` 、使用可能なすべてのパラメーターはプロパティで定義 `provisionParameters` されます。 定義済みのパラメーターが要件を満たす場合は、パラメーター ファイルをカスタマイズしてください。

次の表に、使用可能な定義済みパラメーターの一覧を示します。

| パラメーター名 | 既定値 | パラメーターでカスタマイズできる機能 | 値の制約 |
| --- | --- | --- | --- |
| resourceBaseName | 環境ごとに自動生成 | すべてのリソースの既定の名前 | 2 ~ 20 文字の小文字と数字 |
| simpleAuthServerFarmsName | ${resourceBaseName}simpleAuth | 簡易認証アプリ サービス プランの名前 | 1 ~ 40 文字の英数字とハイフン |
| simpleAuthWebAppName | ${resourceBaseName}simpleAuth | 単純な認証 Web アプリの名前 | 2 ~ 60 文字の英数字とハイフン <br /> ハイフンで開始または終了できない |
| simpleAuthSku | F1 | 簡易認証アプリ サービスプランの SKU | 該当なし |
| frontendHostingStorageName | ${resourceBaseName}タブ | フロントエンド ホスティング ストレージ アカウントの名前 | 3 ~ 24 文字の小文字と数字 |
| frontendHostingStorageSku | Standard_LRS | フロントエンド ホスティング ストレージ アカウントの SKU |[使用可能な SKU](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep)|
| functionServerfarmsName | ${resourceBaseName}api | 関数アプリのサービス プランの名前 | 1 ~ 40 文字の英数字とハイフン |
| functionServerfarmsSku | Y1 | 関数アプリサービスプランの SKU | 該当なし|
| functionAppName | ${resourceBaseName}api | 関数アプリの名前 | 2 ~ 60 文字の英数字とハイフン <br /> ハイフンで開始または終了できない |
| functionStorageName | ${resourceBaseName}api | 関数アプリのストレージ アカウントの名前 | 3 ~ 24 文字の小文字と数字 |
| functionStorageSku | Standard_LRS | 関数アプリのストレージ アカウントの SKU | [使用可能な SKU](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep) |
| botServiceName | ${resourceBaseName} | Azure ボット サービスの名前 | 2 ~ 64 文字の英数字、アンダースコア、ピリオド、ハイフン <br /> 英数字で始める |
| botServiceSku | F0 | Azure ボット サービスの SKU | [使用可能な SKU](/azure/templates/microsoft.botservice/2021-05-01-preview/botservices?tabs=bicep) |
| botDisplayName | ${resourceBaseName} | ボットの表示名 | 1 ~ 42 文字 |
| botServerfarmsName | ${resourceBaseName}bot | ボットのアプリ サービス プランの名前 | 1 ~ 40 文字の英数字とハイフン |
| botWebAppName | ${resourceBaseName}bot | ボットの Web アプリの名前 | 2 ~ 60 文字の英数字とハイフン <br /> ハイフンで開始または終了できない |
| botWebAppSKU | F1 | ボットの SKU App Serviceプラン | 該当なし |
| userAssignedIdentityName | ${resourceBaseName} | ユーザー割り当て ID の名前 | 3 ~ 128 文字の英数字、ハイフン、アンダースコア <br /> 文字または数字で始める |
| sqlServerName | ${resourceBaseName} | サーバー Azure SQL名 | 1 ~ 63 の小文字、数字、ハイフン <br /> ハイフンで開始または終了できない |
| sqlDatabaseName | ${resourceBaseName} | データベースのAzure SQL名 | 1 ~ 128 文字、 <>*%&:\/? またはコントロール文字 <br /> ピリオドまたはスペースで終了できない |
| sqlDatabaseSku | 基本 | データベースの SKU Azure SQL | 該当なし  |
| apimServiceName | ${resourceBaseName} | APIM サービスの名前 | 1 ~ 50 文字の英数字とハイフン <br /> 文字で始め、英数字で終わる |
| apimServiceSku | 消費 | APIM サービスの SKU | [使用可能な SKU](/azure/templates/microsoft.apimanagement/service?tabs=bicep) |
| apimProductName | ${resourceBaseName} | APIM 製品の名前 | 1 ~ 80 文字の英数字とハイフン <br /> 文字で始め、英数字で終わる |
| apimOauthServerName | ${resourceBaseName} | APIM OAuth サーバーの名前 | 1 ~ 80 文字の英数字とハイフン <br /> 文字で始め、英数字で終わる |
| keyVaultSkuName | 標準 | Azure Key Vault サービスの SKU 名| |

一方、次のパラメーターは、プロビジョニング中に値が設定された場合に使用できます。 これらのプレースホルダーの目的は、新しい環境で新しいリソースを作成できます。 実際の値はから解決されます `.fx/states/state.{env}.json`。

##### <a name="azure-ad-application-related-parameters"></a>Azure AD関連のパラメーター

| パラメーター名 | 既定値の場所の所有者 | 場所所有者の意味 | カスタマイズする方法 |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | プロビジョニング中に作成Azure ADアプリのクライアント ID | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | プロビジョニング中に作成Azure ADアプリのクライアント シークレット | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | アプリのアプリのテナント id Azure ADします。 | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | アプリのアプリの OAuth Azure ADホスト | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | プロビジョニング中にAzure ADボットのアプリ クライアント ID | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | プロビジョニング中に作成Azure ADボットのアプリ クライアント シークレット | [値をカスタマイズする](#use-an-existing-azure-ad-app-for-your-bot) |
| apimClientId | {{state.fx-resource-apim.apimClientAADClientId}} | プロビジョニング中にAzure AD APIM のアプリ クライアント ID | プレースホルダーを削除し、実際の値を入力する |
| apimClientSecret | {{state.fx-resource-apim.apimClientAADClientSecret}} | プロビジョニング中にAzure AD APIM のアプリ クライアント シークレット | プレースホルダーを削除し、実際の値を入力する |

##### <a name="azure-resource-related-parameters"></a>Azure リソース関連のパラメーター

| パラメーター名 | 既定値の場所の所有者 | 場所所有者の意味 | カスタマイズする方法 |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | Azure SQL中に指定したサーバー管理者アカウント | プレースホルダーを削除し、実際の値を入力する |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | Azure SQL中に指定したサーバー管理者パスワード | プレースホルダーを削除し、実際の値を入力する |
| apimPublisherEmail | {{state.fx-resource-apim.publisherEmail}} | APIM の発行元メール、既定値は Azure アカウント | プレースホルダーを削除し、実際の値を入力する |
| apimPublisherName | {{state.fx-resource-apim.publisherName}} | APIM の発行元名、既定値は Azure アカウント | プレースホルダーを削除し、実際の値を入力する |

#### <a name="referencing-environment-variables-in-parameter-files"></a>パラメーター ファイルでの環境変数の参照

パラメーター ファイル内の値をハードコードしない場合 (たとえば、値がシークレットの場合)。 パラメーター ファイルは、環境変数からの値の参照をサポートします。 ツールのパラメーター値の `{{$env.YOUR_ENV_VARIABLE_NAME}}` 構文を使用して、現在の環境変数から解決できます。

次の使用例は、環境変数からパラメーターの `mySelfHostedDbConnectionString` 値を読み取ります `DB_CONNECTION_STRING`。

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>テンプレート ARMをカスタマイズする

定義済みのテンプレートがアプリケーション要件を満たしない場合は、フォルダーのARMカスタマイズ `templates/azure` できます。 たとえば、アプリ用の追加の Azure ARM作成するテンプレートをカスタマイズできます。 テンプレートの作成に使用する二頭上言語の基本的な知識ARMがあります。 バイセップの使用を開始するには、バイセップ [のドキュメントを参照してください](/azure/azure-resource-manager/bicep/)。

> [!NOTE]
> このARMは、すべての環境で共有されます。 プロビジョニングの動作 [が環境によって](/azure/azure-resource-manager/bicep/conditional-resource-deployment) 異なる場合は、条件付き展開を使用できます。

TeamsFx ツールが正しく機能していることを確認するには、次の要件をARMテンプレートをカスタマイズしてください。 他のツールを使用してさらなる開発を行う場合は、これらの要件を無視できます。

* フォルダー構造とファイル名は変更しないでください。 プロジェクトにリソースや機能を追加すると、ツールによって既存のファイルに新しいコンテンツが追加される場合があります。
* 自動生成されたパラメーターの名前とプロパティ名は変更しないでください。 自動生成されたパラメーターは、プロジェクトにリソースや機能を追加するときに使用できます。
* 自動生成されたテンプレートの出力を変更ARMしてください。 テンプレートに出力を追加ARMできます。 出力は、 `.fx/states/state.{env}.json` マニフェスト ファイルの展開、検証などの他の機能で使用できます。

### <a name="customization-scenarios"></a>カスタマイズ シナリオ

次のシナリオをカスタマイズできます。

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>ボットに既存のAzure ADアプリを使用する

次の構成スニペットをファイル`.fx/configs/config.{env}.json`に追加して、自分で作成Azure ADアプリを使用Teamsできます。 アプリを作成するにはAzure ADを参照してください<https://aka.ms/teamsfx-existing-aad-doc>。

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

スニペットを追加した後、関連する環境変数にシークレットを追加して、プロビジョニング中に実際のシークレットを解決できます。

> [!NOTE]
> 複数の環境で同じアプリAzure AD共有しないでください。 アプリを更新する権限を持Azure AD場合は、アプリを手動で更新する方法に関するAzure ADできます。 手順に従って、プロビジョニング後Azure ADアプリを更新します。

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>既存のアプリをAzure ADアプリTeamsする

次の構成スニペットをファイルに追加`.fx/configs/config.{env}.json`して、ボットAzure ADアプリを使用できます。

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

前のスニペットを追加した後、ツールの関連する環境変数にシークレットを追加して、プロビジョニング中に実際のシークレットを解決します。

#### <a name="skip-adding-user-for-sql-database"></a>データベースのユーザーの追加SQLスキップする

ツールがユーザーを SQL `.fx/configs/config.{env}.json` データベースに追加しようとするときにアクセス許可エラーが不足している場合は、次の構成スニペットをファイルに追加して、データベース ユーザーへの追加SQLできます。

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>Function App インスタンスの名前を指定する

既定の名前を `contosoteamsappapi` 使用する代わりに、関数アプリ インスタンスに使用できます。

> [!NOTE]
> 既に環境をプロビジョニングしている場合は、名前を指定すると、以前に作成したインスタンスの名前を変更する代わりに、新しい関数アプリ インスタンスを作成できます。

次の手順を実行します。

1. 現在の `.fx/configs/azure.parameters.{env}.json` 環境で開きます。
2. パラメーターの値に新 `functionAppName` しいプロパティを追加します `provisionParameters`。
3. の `contosoteamsappapi` 値として入力します。 `functionAppName`
4. 最終的なパラメーター ファイルは、次のスニペットに表示されます。

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

### <a name="scenerio"></a>Scenerio

他の Azure リソースまたはストレージをアプリケーションに追加するには、次の手順を実行します。

Blob データを格納するために Azure 関数バックエンドに Azure ストレージを追加するシナリオについて考えます。 Azure ストレージ サポートを使用してバイセップ テンプレートを更新する自動フローはありません。 ただし、バイセップ ファイルを編集してリソースを追加できます。 手順は次のとおりです。

1. タブ プロジェクトを作成します。
2. プロジェクトに関数を追加します。 詳細については、「リソースの追加 [」を参照してください](./add-resource.md)。
3. 新しいストレージ アカウントをテンプレートでARMします。 リソースは直接宣言 `templates/azure/provision/function.bicep` できます。 他の場所でリソースを宣言できます。

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

4. で Azure ストレージ接続文字列を使用して Azure 関数アプリの設定を更新します `templates/azure/provision/function.bicep`。 リソースの配列に次のスニペット `functionApp` を追加 `appSettings` します。

    ``````````````````bicep
    {
        name: 'MyAppStorageAccountConnectionString'
        value: 'DefaultEndpointsProtocol=https;AccountName=${applicationStorageAccount.name};AccountKey=${listKeys(applicationStorageAccount.id, '2021-06-01').keys[0].value}'
    }
    ```````````````````

5. Azure ストレージ出力バインドを使用して関数を更新できます。

## <a name="faq"></a>よくあるご質問 (FAQ)

<br>

<details>

<summary><b>トラブルシューティングの方法</b></summary>

エラーが発生したTeams ToolkitがVisual Studio Code場合は、エラー通知問い合わせを選択して、関連するドキュメントに移動できます。 TeamsFx CLI を使用している場合は、ヘルプ ドキュメントを示すハイパーリンクがエラー メッセージの最後に表示されます。プロビジョニング ヘルプ ドキュメントを [直接表示](https://aka.ms/teamsfx-arm-help) することもできます。

<br>

</details>

<details>

<summary><b>プロビジョニング中に別の Azure サブスクリプションに切り替える方法</b></summary>

1. 現在のアカウントでサブスクリプションを切り替えるか、ログアウトして新しいサブスクリプションを選択します。
2. 現在の環境を既に準備している場合は、リソースの移動をサポートしていないARM新しい環境を作成し、プロビジョニングを実行する必要があります。
3. 現在の環境をプロビジョニングしなかった場合は、プロビジョニングを直接トリガーできます。

<br>

</details>

<details>

<summary><b>プロビジョニング中にリソース グループを変更する方法</b></summary>

プロビジョニングの前に、新しいリソース グループを作成するか、既存のリソース グループを使用するかが確認されます。 この手順では、新しいリソース グループ名を指定するか、既存のリソース グループ名を選択できます。

<br>

</details>

<details>

<summary><b>Sharepoint ベースのアプリをプロビジョニングする方法</b></summary>

プロビジョニング の手順[に従って、SharePointアプリを実行できます](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4)。

> [!NOTE]
> 現在、Teams Toolkit を使用した sharepoint フレームワークを使用した Teams アプリの構築には Azure との直接統合は行いませんが、ドキュメント内のコンテンツは SPFx ベースのアプリには適用されません。

<br>

</details>

## <a name="see-also"></a>関連項目

* [Teams アプリをクラウドに展開する](deploy.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
* [Teams プロジェクトで他の開発者と協力する](TeamsFx-collaboration.md)
