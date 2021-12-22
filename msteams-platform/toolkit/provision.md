---
title: クラウド Teams Toolkitプロビジョニングに使用する
author: MuyangAmigo
description: クラウド リソースのプロビジョニング
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: c8899131876533fdd64913fb6790cff9f258e8f5
ms.sourcegitcommit: aede47694894d281f6b725083bc0b46ab0e4846d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2021
ms.locfileid: "61591786"
---
# <a name="use-teams-toolkit-to-provision-cloud-resources"></a>クラウド Teams Toolkitプロビジョニングに使用する

TeamsFx は、Azure と Microsoft 365クラウドとのシームレスな統合を提供し、1 つのコマンドでアプリケーションを Azure に配置できます。 TeamsFx は Azure Resource Manager と統合し、インフラストラクチャをコード アプローチとして使用して、アプリケーションが必要とする Azure リソースを宣言的にプロビジョニングできます。  

## <a name="prerequisites"></a>前提条件

* アカウントの前提条件

    クラウド リソースをプロビジョニングするには、適切なアクセス許可を持つ次のアカウントが必要です。 詳細については、「アプリをビルド[するためのアカウントの準備」をTeamsしてください](accounts.md)。
    * Microsoft 365
    * 有効なサブスクリプションを持つ Azure

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> VS コードで開Teamsアプリ プロジェクトを既に持っている必要があります。

## <a name="provision-using-teams-toolkit"></a>サーバーを使用したプロビジョニングTeams Toolkit

プロビジョニングは、次のように、Teams Toolkitまたは TeamsFx CLI Visual Studio Codeコマンドを使用して実行されます。

[Azure ベースのアプリをプロビジョニングする](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)

## <a name="resource-creation"></a>リソースの作成

このコマンドまたは TeamsFx CLI でTeams Toolkitコマンドをトリガーすると、次のリソースを取得できます。

* AADテナントの下Microsoft 365アプリケーション
* TeamsテナントのプラットフォームMicrosoft 365アプリの登録Teamsする
* 選択した Azure サブスクリプションの Azure リソース

新しいプロジェクトを作成すると、すべての Azure リソースが作成されます。 生成されたARMテンプレートは、すべての Azure リソースを定義し、プロビジョニング中に必要な Azure リソースを作成するのに役立ちます。 既存の [プロジェクトに新しい機能/リソース](./add-resource.md) を追加すると、更新された ARMは最新の変更を反映します。

> [!NOTE]
> Azure サービスでは、サブスクリプションにコストが発生します。見積もりを理解するには、価格 [計算ツールを](https://azure.microsoft.com/pricing/calculator/) 参照してください。

### <a name="resource-creation-for-teams-tab-application"></a>タブ アプリケーションのリソースTeams作成

|リソース|このリソースの目的| メモ |
|----------|--------------------------------|-----|
| Azure Storage | タブ アプリをホストする | 静的 Web アプリ機能でタブ アプリをホストできます |
| 簡易認証の App Service プラン | 簡易認証の Web アプリをホストする | |
| 簡易認証用 Web アプリ | 単一ページ アプリケーションで他のサービスにアクセスするのに役立つ簡単な認証サーバーをホストする | ユーザー割り当て ID を追加して、他の Azure リソースに簡単にアクセスできます |
| ユーザー割り当て ID | Azure サービス間要求の認証 | さまざまな機能とリソース間で共有 |

### <a name="resources-created-for-teams-bot-or-messaging-extension-application"></a>ボットまたはメッセージングTeamsアプリケーション用に作成されたリソース

|リソース|このリソースの目的| メモ |
|----------|--------------------------------|-----|
| Azure Bot Service | ボット フレームワークにアプリをボットとして登録する | ボットをデバイスに接続Teams |
| ボットの App Service プラン | ボットの Web アプリをホストする | |
| ボット用 Web アプリ | ボット アプリをホストする | ユーザー割り当て ID を追加して、他の Azure リソースに簡単にアクセスできます。 <br /> TeamsFx SDK で必要な [アプリ設定を追加する](https://www.npmjs.com/package/@microsoft/teamsfx) |
| ユーザー割り当て ID | Azure サービス間要求の認証 | さまざまな機能とリソース間で共有 |

### <a name="resources-created-when-including-azure-functions-in-the-project"></a>Azure Functions をプロジェクトに含めたときに作成されるリソース

|リソース|このリソースの目的| メモ |
|----------|--------------------------------|-----|
| 関数アプリの App Service プラン | 関数アプリをホストする | |
| 関数アプリ | Azure Functions API をホストする | ユーザー割り当て ID を追加して、他の Azure リソースに簡単にアクセスできます。 <br /> CORS ルールを追加してタブ アプリからの要求を許可する <br /> アプリからの要求のみを許可する認証設定をTeamsします。 <br /> TeamsFx SDK で必要な [アプリ設定を追加する](https://www.npmjs.com/package/@microsoft/teamsfx) |
| Azure Storage関数アプリの詳細 | 関数アプリの作成時に必須 | |
| ユーザー割り当て ID | Azure サービス間要求の認証 | さまざまな機能とリソース間で共有 |

### <a name="resources-created-when-including-azure-sql-in-the-project"></a>Azure リソースをプロジェクトに含SQLリソース

|リソース|このリソースの目的| メモ |
|----------|--------------------------------|-----|
| Azure SQL Server | インスタンスのホストAzure SQL Databaseする | すべての Azure サービスがサーバーにアクセスできます |
| Azure SQL データベース | アプリのデータを保存する | ユーザーに割り当てられた ID の読み取り/書き込みアクセス許可をデータベースに付与する |
| ユーザー割り当て ID | Azure サービス間要求の認証 | さまざまな機能とリソース間で共有 |

### <a name="resources-created-when-including-azure-api-management-in-the-project"></a>Azure API Management をプロジェクトに含めたときに作成されるリソース

|リソース|このリソースの目的|
|----------|--------------------------------|
| Azure Active Directory API 管理サービス用のアプリケーション | API 管理サービスによって管理される Microsoft Power Platform アクセス API を許可する |
| API 管理サービス | 関数アプリでホストされている API を管理する |
| API 管理製品 | API をグループ化し、使用条件とランタイム ポリシーを定義する |
| API 管理 OAuth サーバー | Microsoft Power Platform が関数アプリでホストされている API にアクセスできます |
| ユーザー割り当て ID | Azure サービス間要求の認証 |

## <a name="customize-resource-provision"></a>リソースのプロビジョニングをカスタマイズする

Teams Toolkitでは、インフラストラクチャをコード アプローチとして使用して、プロビジョニングする Azure リソースと、それらを構成する方法を定義できます。 このツールは、ARMを使用して Azure リソースを定義します。 このARMテンプレートは、プロジェクトのインフラストラクチャと構成を定義する一連のバイセップ ファイルです。 カスタム テンプレートを変更して作成された Azure リソースARMできます。 詳細については [、「bicep ドキュメント」を参照してください](/azure/azure-resource-manager/bicep.md)。 アプリケーションを使用ARM、次の 2 セットのファイル、パラメーター、およびテンプレートを変更します。

* ARMパラメーター ファイル ( ) は、テンプレートにパラメーターを渡すフォルダー `azure.parameters.{your_env_name}.json` `.fx/configs` にあります。
* ARMにあるテンプレート ファイルには、 `templates/azure` 次のファイルが含まれます。

| File | 何を行う | カスタマイズを許可する |
| --- | --- | --- |
| main.bicep | Azure リソースプロビジョニングのエントリ ポイントを提供する | 必要 |
| provision.bicep | Azure リソースの作成と構成 | はい |
| config.bicep | TeamsFx に必要な構成を Azure リソースに追加する | はい |
| provision/xxx.bicep | によって使用される各 Azure リソースを作成および構成する `provision.bicep` | 必要 |
| teamsfx/xxx.bicep | 使用する各 Azure リソースに TeamsFx 必要な構成を追加する `config.bicep`| いいえ |

> [!NOTE]
> リソースまたは機能をプロジェクトに追加すると、 `teamsfx/xxx.bicep` 再生成されます。 そのため、カスタマイズ不可としてマークされています。 これらのバイセップ ファイルを実際に変更する必要がある場合は、Git を使用してファイルに対する変更を追跡し、リソースや機能の追加中に変更を失わないので、お勧 `teamsfx/xxx.bicep` めします。

### <a name="customize-arm-parameters-and-templates"></a>パラメーター ARMテンプレートをカスタマイズする

パラメーター ファイルをカスタマイズし、二頭上のファイルをカスタマイズすることで、Azure リソースをカスタマイズできます。

#### <a name="customize-arm-template-parameter-files"></a>テンプレート ARM ファイルをカスタマイズする

このツールキットには、Azure リソースをカスタマイズするための一連の定義済みパラメーターが含まれています。 パラメーター ファイルは場所にあり `.fx/configs/azure.parameters.{env}.json` 、使用可能なすべてのパラメーターはプロパティで定義 `provisionParameters` されます。 定義済みのパラメーターが要件を満たす場合は、パラメーター ファイルをカスタマイズしてください。

使用可能な定義済みのパラメーターの一覧を次に示します。

| パラメーター名 | 既定値 | パラメーターでカスタマイズできる機能 | 値の制約 |
| --- | --- | --- | --- |
| resourceBaseName | 環境ごとに自動生成 | すべてのリソースの既定の名前 | 2 ~ 20 文字の小文字と数字 |
| simpleAuthServerFarmsName | ${resourceBaseName}simpleAuth | 簡易認証アプリ サービス プランの名前 | 1 ~ 40 文字の英数字とハイフン |
| simpleAuthWebAppName | ${resourceBaseName}simpleAuth | 簡易認証 Web アプリの名前 | 2 ~ 60 文字の英数字とハイフン <br /> ハイフンで開始または終了できない |
| simpleAuthSku | F1 | 簡易認証 App Service プランの SKU |  |
| frontendHostingStorageName | ${resourceBaseName}タブ | Frontend Hosting Storage アカウントの名前 | 3 ~ 24 文字の小文字と数字 |
| frontendHostingStorageSku | Standard_LRS | Frontend Hosting Storage アカウントの SKU | 使用可能な SKU [については、](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep&branch) このページを参照してください。 |
| functionServerfarmsName | ${resourceBaseName}api | 関数アプリの App Service プランの名前 | 1 ~ 40 文字の英数字とハイフン |
| functionServerfarmsSku | Y1 | FUnction アプリの App Service プランの SKU |
| functionAppName | ${resourceBaseName}api | 関数アプリの名前 | 2 ~ 60 文字の英数字とハイフン <br /> ハイフンで開始または終了できない |
| functionStorageName | ${resourceBaseName}api | 関数アプリのアカウントStorage名 | 3 ~ 24 文字の小文字と数字 |
| functionStorageSku | Standard_LRS | 関数アプリのアカウントStorage SKU | 使用可能な SKU [については、](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep&branch=pr-en-us-4713)このページを参照してください。 |
| botServiceName | ${resourceBaseName} | Azure Bot サービスの名前 | 2 ~ 64 文字の英数字、アンダースコア、ピリオド、ハイフン <br /> 英数字で始める |
| botServiceSku | F0 | Azure Bot サービスの SKU | 使用可能な SKU [については、](/azure/templates/microsoft.botservice/2021-05-01-preview/botservices?tabs=bicep&branch) このページを参照してください。 |
| botDisplayName | ${resourceBaseName} | ボットの表示名 | 1 ~ 42 文字 |
| botServerfarmsName | ${resourceBaseName}bot | ボットの App Service プランの名前 | 1 ~ 40 文字の英数字とハイフン |
| botWebAppName | ${resourceBaseName}bot | ボットの Web アプリの名前 | 2 ~ 60 文字の英数字とハイフン <br /> ハイフンで開始または終了できない |
| botWebAppSKU | F1 | ボット アプリ サービス プランの SKU |  |
| userAssignedIdentityName | ${resourceBaseName} | ユーザー割り当て ID の名前 | 3 ~ 128 文字の英数字、ハイフン、アンダースコア <br /> 文字または数字で始める |
| sqlServerName | ${resourceBaseName} | Azure の名前SQL Server | 1 ~ 63 の小文字、数字、ハイフン <br /> ハイフンで開始または終了できない |
| sqlDatabaseName | ${resourceBaseName} | [名前] Azure SQL Database | 1 ~ 128 文字、次の <>*%を \/ &。 またはコントロール文字 <br /> ピリオドまたはスペースで終了できない |
| sqlDatabaseSku | 基本 | SKU のAzure SQL Database |  |
| apimServiceName | ${resourceBaseName} | APIM サービスの名前 | 1 ~ 50 文字の英数字とハイフン <br /> 文字で始め、英数字で終わる |
| apimServiceSku | 消費 | APIM サービスの SKU | 使用可能な SKU [については、](/azure/templates/microsoft.apimanagement/service?tabs=bicep&branch)このページを参照してください。 |
| apimProductName | ${resourceBaseName} | APIM 製品の名前 | 1 ~ 80 文字の英数字とハイフン <br /> 文字で始め、英数字で終わる |
| apimOauthServerName | ${resourceBaseName} | APIM OAuth Server の名前 | 1 ~ 80 文字の英数字とハイフン <br /> 文字で始め、英数字で終わる |

一方、次のパラメーターは、プロビジョニング中に値が設定された場合に使用できます。 これらのプレースホルダーの目的は、新しい環境を作成するときに、新しいリソースを作成できます。 実際の値はから解決されます `.fx/states/state.{env}.json` 。

##### <a name="aad-application-related-parameters"></a>AAD関連のパラメーター

| パラメーター名 | 既定値の場所の所有者 | 場所所有者の意味 | カスタマイズする方法 |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | プロビジョニング中に作成AADアプリのクライアント ID | 値 [をカスタマイズするには](#use-an-existing-aad-app-for-your-teams-app) 、このセクションを参照してください。 |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | プロビジョニング中に作成AADアプリのクライアント シークレット | 値 [をカスタマイズするには](#use-an-existing-aad-app-for-your-teams-app) 、このセクションを参照してください。 |
| Microsoft 365TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | アプリのアプリのテナント id AADします。 | 値 [をカスタマイズするには](#use-an-existing-aad-app-for-your-teams-app) 、このセクションを参照してください。 |
| Microsoft 365 OauthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | アプリのアプリの OAuth AADホスト | 値 [をカスタマイズするには](#use-an-existing-aad-app-for-your-teams-app) 、このセクションを参照してください。 |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | プロビジョニング中にAADボットのアプリ クライアント ID | 値 [をカスタマイズするには](#use-an-existing-aad-app-for-your-bot) 、このセクションを参照してください。 |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | プロビジョニング中に作成AADボットのアプリ クライアント シークレット | 値 [をカスタマイズするには](#use-an-existing-aad-app-for-your-bot) 、このセクションを参照してください。 |
| apimClientId | {{state.fx-resource-apim.apimClientAADClientId}} | プロビジョニング中に作成AAD APIM のアプリ クライアント ID | プレースホルダーを削除し、実際の値を入力する |
| apimClientSecret | {{state.fx-resource-apim.apimClientAADClientSecret}} | プロビジョニング中に作成AAD APIM のアプリ クライアント シークレット | プレースホルダーを削除し、実際の値を入力する |

##### <a name="azure-resource-related-parameters"></a>Azure リソース関連のパラメーター

| パラメーター名 | 既定値の場所の所有者 | 場所所有者の意味 | カスタマイズする方法 |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | プロビジョニングSQL Serverした Azure 管理者アカウント | プレースホルダーを削除し、実際の値を入力する |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | プロビジョニングSQL Server指定した Azure 管理者パスワード | プレースホルダーを削除し、実際の値を入力する |
| apimPublisherEmail | {{state.fx-resource-apim.publisherEmail}} | APIM の発行元メール、既定値は Azure アカウント | プレースホルダーを削除し、実際の値を入力する |
| apimPublisherName | {{state.fx-resource-apim.publisherName}} | APIM の発行元名、既定値は Azure アカウント | プレースホルダーを削除し、実際の値を入力する |

#### <a name="referencing-environment-variables-in-parameter-files"></a>パラメーター ファイルでの環境変数の参照

パラメーター ファイル内の値をハードコードしない場合があります。 たとえば、値がシークレットの場合です。 パラメーター ファイルは、環境変数からの値の参照をサポートします。 パラメーター値の構文を使用して、現在の環境変数から値を解決する必要があることをツール `{{$env.YOUR_ENV_VARIABLE_NAME}}` に伝えます。

次の例では、環境変数から `mySelfHostedDbConnectionString` パラメーターの値を読み取ります `DB_CONNECTION_STRING` 。

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>テンプレート ARMをカスタマイズする

定義済みのテンプレートがアプリケーション要件を満たしていない場合は、フォルダーのARMカスタマイズ `templates/azure` できます。 たとえば、アプリ用の追加の Azure ARM作成するテンプレートをカスタマイズできます。 これは事前のシナリオであり、テンプレートの作成に使用される二頭上言語の基本的なARMです。 バイセップの使用を開始するには、 [バイセップのドキュメントを参照してください](/azure/azure-resource-manager/bicep/?branch)。
> [!NOTE]
> このARMは、すべての環境で共有されます。 環境間のさまざまな [プロビジョニング動作の](/azure/azure-resource-manager/bicep/conditional-resource-deployment?branch) 場合は、条件付き展開を使用できます。

TeamsFx ツールが正しく機能していることを確認するには、カスタマイズしたテンプレートがARM要件を満たしていることを確認してください。 他のツールを使用してさらなる開発を行う場合は、これらの要件を無視できます。

* フォルダー構造とファイル名は変更しないでください。 プロジェクトにリソース/機能を追加すると、ツールによって既存のファイルに新しいコンテンツが追加される場合があります。
* 自動生成されたパラメーターの名前とプロパティ名は変更しないでください。 自動生成されたパラメーターは、プロジェクトにリソース/機能を追加するときに使用できます。
* 自動生成されたテンプレートの出力は変更ARMしてください。 テンプレートに出力を追加ARMできます。 出力は、展開、マニフェスト ファイルの検証などの他の機能に保持され `.fx/states/state.{env}.json` 、使用されます。

### <a name="customization-scenarios"></a>カスタマイズ シナリオ

これらは、プロビジョニング動作をカスタマイズできる一般的なシナリオです。

#### <a name="use-an-existing-aad-app-for-your-teams-app"></a>既存のアプリをAADアプリにTeamsする

次の構成スニペットをファイルに追加して、AADアプリ用にTeams `.fx/configs/config.{env}.json` できます。 アプリを作成するにはAADを参照してください <https://aka.ms/teamsfx-existing-aad-doc> 。

```json
"auth": {
    "clientId": "<your AAD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your AAD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

上記のスニペットを追加した後、関連する環境変数にシークレットを追加して、プロビジョニング中にツールが実際のシークレットを解決できます。

> [!NOTE]
> 複数の環境で 1 つのアプリAAD共有しないでください。 アプリを更新する権限を持AAD場合は、アプリを手動で更新する方法に関するAADされます。 プロビジョニング後にアプリを更新するには、AAD手順に従ってください。

#### <a name="use-an-existing-aad-app-for-your-bot"></a>ボットに既存のAADアプリを使用する

次の構成スニペットをファイルに追加 `.fx/configs/config.{env}.json` して、ボットAADアプリを使用できます。

```json
"bot": {
    "appId": "<your AAD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

上記のスニペットを追加した後、関連する環境変数にシークレットを追加して、プロビジョニング中にツールが実際のシークレットを解決できます。

> [!NOTE]
> 複数の環境で 1 つのアプリAAD共有しないでください。

#### <a name="skip-adding-user-for-sql-database"></a>データベースのユーザーの追加SQLスキップする

ツールがデータベースにユーザーを追加しようとすると、アクセス許可エラーがSQL場合があります。 次の構成スニペットをファイルに追加 `.fx/configs/config.{env}.json` して、データベース ユーザーへの追加SQLスキップできます。

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>Function App インスタンスの名前を指定する

この例では、既定の名前を `contosoteamsappapi` 使用する代わりに、Function App インスタンスに別の名前を指定します。

> [!NOTE]
> 既に環境をプロビジョニングしている場合、名前を指定すると、以前に作成したインスタンスの名前を変更する代わりに、新しい Function App インスタンスが作成されます。

次の手順を実行します。

1. 現在 `.fx/configs/azure.parameters.{env}.json` の環境で開きます。
2. パラメーターの値に `functionAppName` 新しいプロパティを追加します `provisionParameters` 。
3. "contosoteamsappapi" を値として入力する `functionAppName`
4. 最後のパラメーター ファイルは、次のように表示されます。

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

**他の Azure リソース (Azure ストレージ) をアプリケーションに追加するには**

このシナリオでは、いくつかの BLOB データを格納Azure Storage Azure Function バックエンドにデータを追加する場合を考えます。 サポートを使用してバイセップ テンプレートを更新する自動フロー Azure Storageはありません。 ただし、バイセップ ファイルを編集してリソースを追加できます。 手順は次のとおりです。

1. タブ プロジェクトを作成する
2. プロジェクトに関数を追加します。 リソースの追加の [詳細については、「リソース](./add-resource.md) の追加」をご覧ください。
3. 新しいアカウントをStorageテンプレートARMします。 簡略化するために、リソースを直接宣言 `templates/azure/provision/function.bicep` します。 他の場所でリソースを宣言できます。

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

4. 手順 3 の同設定でAzure Storage接続文字列を使用して Azure Function App を `templates/azure/provision/function.bicep` 更新します。 リソースの配列に `functionApp` 次のスニペットを追加 `appSettings` します。

    ``````````````````bicep
    {
        name: 'MyAppStorageAccountConnectionString'
        value: 'DefaultEndpointsProtocol=https;AccountName=${applicationStorageAccount.name};AccountKey=${listKeys(applicationStorageAccount.id, '2021-06-01').keys[0].value}'
    }
    ```````````````````

5. これで、出力バインドを使用してAzure Storage更新できます。

## <a name="faq"></a>よくあるご質問 (FAQ)

<br>

<details>

<summary><b>トラブルシューティングの方法</b></summary>

エラーが発生したTeams ToolkitがVisual Studio Code、エラー通知のボタンをクリックして、関連するヘルプ `Get Help` ドキュメントに移動できます。TeamsFx CLI を使用している場合は、ヘルプ ドキュメントを示すハイパー リンクがエラー メッセージの最後に表示されます。プロビジョニング ヘルプ ドキュメントを[直接表示](https://aka.ms/teamsfx-arm-help)することもできます。

<br>

</details>

<details>

<summary><b>プロビジョニング中に別の Azure サブスクリプションに切り替える方法</b></summary>

1. 現在のアカウントでサブスクリプションを切り替えるか、ログアウトして新しいサブスクリプションを選択します。
2. 現在の環境を既にプロビジョニングしている場合は、リソースの移動をサポートしていないので、新しい環境を作成し、ARMを実行する必要があります。
3. 現在の環境をプロビジョニングしなかった場合は、プロビジョニングを直接トリガーできます。

<br>

</details>

<details>

<summary><b>プロビジョニング中にリソース グループを変更する方法</b></summary>

プロビジョニングの前に、新しいリソース グループを作成するか、既存のリソース グループを使用するかが確認されます。 この手順では、新しいリソース グループ名を指定するか、既存のリソース グループ名を選択できます。

<br>

</details>

<details>

<summary><b>アプリをプロビジョニングSharePointする方法</b></summary>

[プロビジョニング] SharePoint[ベース のアプリに従](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)って、SharePointアプリをプロビジョニングできます。

> [!NOTE]
> 現在 Teams、Teams Toolkit を使用した SharePoint Framework を使用したアプリの構築には Azure との直接統合は行いません。このドキュメントのコンテンツは、SPFx ベースのアプリには適用されません。


<br>

</details>

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [クラウドTeamsアプリを展開する](deploy.md)

> [!div class="nextstepaction"]
> [複数の環境を管理する](TeamsFx-multi-env.md)

> [!div class="nextstepaction"]
> [プロジェクトで他の開発者とTeamsする](TeamsFx-collaboration.md)
