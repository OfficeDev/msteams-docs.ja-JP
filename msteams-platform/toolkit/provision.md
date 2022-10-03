---
title: Teams Toolkit を使用してクラウド リソースをプロビジョニングする
author: MuyangAmigo
description: このモジュールでは、Teams Toolkit を使用してクラウド リソースをプロビジョニングする方法、リソースの作成、リソースのプロビジョニングのカスタマイズを行う方法について説明します。
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: a0174d113d441e2318f4f9f4165211f46df1876e
ms.sourcegitcommit: ea7b7b8ebb4b2acdd0b9a3411c59a9a91a06f409
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2022
ms.locfileid: "68350462"
---
# <a name="provision-cloud-resources"></a>クラウド リソースをプロビジョニングする

TeamsFx は Azure および Microsoft 365 クラウドと統合されており、1 つのコマンドでアプリケーションを Azure に配置できます。 TeamsFx は Azure Resource Managerと統合されており、アプリケーションでコード アプローチに必要な Azure リソースをプロビジョニングできます。

::: zone pivot="visual-studio-code"

## <a name="provision-using-teams-toolkit-in-visual-studio-code"></a>Visual Studio Code で Teams Toolkit を使用してプロビジョニングする

プロビジョニングは、Teams Toolkit for Visual Studio Code または TeamsFx CLI の 1 つのコマンドで実行されます。 詳細については、「[Azure ベースのアプリのプロビジョニング](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8)」を参照してください。

## <a name="create-resources"></a>リソースの作成

Teams Toolkit または TeamsFx CLI でプロビジョニング コマンドをトリガーすると、次のリソースを取得できます。

* Microsoft 365 テナントの Microsoft Azure Active Directory (Azure AD) アプリケーション。
* Microsoft 365 テナントの Teams プラットフォームの Teams アプリの登録。
* 選択した Azure サブスクリプションの Azure リソース。

新しいプロジェクトを作成するときに、すべての Azure リソースを使用できます。 ARM テンプレートは、すべての Azure リソースを定義し、プロビジョニング中に必要な Azure リソースを作成するのに役立ちます。 既存のプロジェクトに [新しい機能リソースを追加](./add-resource.md) すると、更新された ARM テンプレートに最新の変更が反映されます。

> [!NOTE]
> Azure サービスでは、サブスクリプションにコストが発生します。コスト見積もりの詳細については、 [価格計算ツールを](https://azure.microsoft.com/pricing/calculator/)参照してください。

次の一覧は、さまざまな種類のアプリと Azure リソースのリソース作成を示しています。
<br>

<details>
<summary><b>Teams タブ アプリケーションのリソース作成</b></summary>

|Resource|用途|説明 |
|----------|--------------------------------|-----|
| Azure Storage | タブ アプリをホストする | 静的 Web アプリ機能でタブ アプリをホストできるようにします |
| 簡単な認証の App Service プラン | Simple Auth の Web アプリをホストする |対象外 |
| 単純な認証用の Web アプリ | 単純な認証サーバーをホストして、単一ページ アプリケーション内の他のサービスにアクセスする | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します |
| ユーザー割り当て ID | Azure サービス間要求を認証する | さまざまな機能とリソース間で共有 |

</details>
<br>

<details>
<summary><b>Teams ボットまたはメッセージ拡張機能アプリケーションのリソース作成</b></summary>

|Resource|用途| 説明 |
|----------|--------------------------------|-----|
| Azure ボット サービス | アプリをボット フレームワークにボットとして登録します | ボットを Teams に接続する |
| ボットの App Service プラン | ボットの Web アプリをホストする |対象外 |
| ボット用 Web アプリ | ボット アプリをホストする | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。 <br /> [TeamsFx SDK](https://www.npmjs.com/package/@microsoft/teamsfx) で必要なアプリ設定を追加します |
| ユーザー割り当て ID | Azure サービス間要求を認証する | さまざまな機能とリソース間で共有 |

</details>
<br>

<details>
<summary><b>プロジェクト内のAzure Functionsのリソース作成</b></summary>

|Resource|用途| 説明|
|----------|--------------------------------|-----|
| 関数アプリの App Service プラン | 関数アプリをホストする |対象外 |
| 関数アプリ | Azure Functions API をホストする | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。 <br /> クロスオリジン リソース共有 (CORS) ルールを追加して、タブ アプリからの要求を許可する <br /> Teams アプリからの要求のみを許可する認証設定を追加します。 <br /> [TeamsFx SDK](https://www.npmjs.com/package/@microsoft/teamsfx) で必要なアプリ設定を追加します |
| 関数アプリ用の Azure Storage | 関数アプリの作成に必要 |対象外|
| ユーザー割り当て ID | Azure サービス間要求を認証する | さまざまな機能とリソース間で共有 |

</details>
<br>

<details>
<summary><b>プロジェクト内のAzure SQLのリソース作成</b></summary>

|Resource|用途 | 説明 |
|----------|--------------------------------|-----|
| Azure SQL サーバー | Azure SQL データベース インスタンスをホストする | すべての Azure サービスがサーバーにアクセスできるようにします |
| Azure SQL データベース | アプリのデータを格納する | ユーザー割り当て ID、読み取りまたは書き込みアクセス許可をデータベースに付与します |
| ユーザー割り当て ID | Azure サービス間要求を認証する | さまざまな機能とリソース間で共有 |

</details>
<br>

<details>
<summary><b>プロジェクト内の Azure API Managementのリソース作成</b></summary>

|Resource|用途|
|----------|--------------------------------|
| API 管理サービス用の Azure AD アプリケーション | API 管理サービスによって管理される Microsoft Power Platform アクセス API を許可する |
| API 管理サービス | 関数アプリでホストされている API を管理する |
| API 管理製品 | API をグループ化し、使用条件とランタイム ポリシーを定義する |
| API Management OAuth サーバー | Microsoft Power Platform が関数アプリでホストされている API にアクセスできるようにします |
| ユーザー割り当て ID | Azure サービス間要求を認証する |

</details>
<br>

<details>
<summary><b>Azure Key Vaultをプロジェクトに含めると作成されたリソース</b></summary>

|リソース|このリソースの目的|
|----------|--------------------------------|
| Azure Key Vault Service | 他の Azure Services で使用されるシークレット (Azure AD アプリ クライアント シークレットなど) を管理する |
| ユーザー割り当て ID | Azure サービス間要求を認証する |

</details>
<br>

## <a name="customize-resource-provision"></a>リソースのプロビジョニングをカスタマイズする

Teams Toolkit を使用すると、コードとしてのインフラストラクチャ アプローチを使用して、プロビジョニングする Azure リソースと構成方法を定義できます。 このツールでは、ARM テンプレートを使用して Azure リソースを定義します。 ARM テンプレートは、プロジェクトのインフラストラクチャと構成を定義する一連の Bicep ファイルです。 ARM テンプレートを変更することで、Azure リソースをカスタマイズできます。 詳細については、[Bicep に関するドキュメント](/azure/azure-resource-manager/bicep)を参照してください。

ARM を使用したプロビジョニングには、次のファイル、パラメーター、テンプレートのセットを変更する必要があります。

* テンプレートにパラメーターを渡すための ARM パラメーター ファイル (`azure.parameters.{your_env_name}.json`) はフォルダーにあります `.fx/configs` 。
* このフォルダーにある `templates/azure`ARM テンプレート ファイルには、次のファイルが含まれています。

| File | 職務 | カスタマイズを許可する |
| --- | --- | --- |
| main.bicep | Azure リソースプロビジョニングのエントリ ポイントを指定する | はい |
| provision.bicep | Azure リソースを作成して構成する | はい |
| config.bicep | TeamsFx に必要な構成を Azure リソースに追加する | はい |
| provision/xxx.bicep | 使用される各 Azure リソースを作成して構成する `provision.bicep` | はい |
| teamsfx/xxx.bicep | によって使用される各 Azure リソースに TeamsFx の必要な構成を追加する `config.bicep`| いいえ |

> [!NOTE]
> リソースまたは機能をプロジェクトに追加すると再生成 `teamsfx/xxx.bicep` され、同じカスタマイズはできません。 Bicep ファイルを変更するには、Git を使用してファイルに対する `teamsfx/xxx.bicep` 変更を追跡できます。これにより、リソースや機能の追加中に変更が失われるのを抑えることができます。

### <a name="azure-ad-parameters"></a>Azure AD パラメーター

ARM テンプレート ファイルでは、パラメーターにプレースホルダーが使用されます。 これらのプレースホルダーの目的は、新しい環境で新しいリソースを確実に作成することです。 実際の値は `.fx/states/state.{env}.json`、 .

Azure AD アプリケーション関連のパラメーターと Azure リソース関連のパラメーターなど、2 種類のパラメーターがあります。

##### <a name="azure-ad-application-related-parameters"></a>Azure AD アプリケーション関連のパラメーター

| パラメーター名 | 既定値のプレース ホルダー | プレース ホルダーの意味 | カスタマイズする方法 |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | プロビジョニング中に作成されたアプリの Azure AD アプリ クライアント ID | [ボットに既存の Azure AD アプリを使用する](#use-an-existing-azure-ad-app-for-your-bot) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | プロビジョニング中に作成されたアプリの Azure AD アプリ クライアント シークレット | [Teams アプリに既存の Azure AD アプリを使用する](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | アプリの Azure AD アプリのテナント ID | [Teams アプリに既存の Azure AD アプリを使用する](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | アプリの Azure AD アプリの OAuth 機関ホスト | [Teams アプリに既存の Azure AD アプリを使用する](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | プロビジョニング中に作成された Bot の Azure AD アプリ クライアント ID | [ボットに既存の Azure AD アプリを使用する](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | プロビジョニング中に作成された Bot の Azure AD アプリ クライアント シークレット | [ボットに既存の Azure AD アプリを使用する](#use-an-existing-azure-ad-app-for-your-bot) |

##### <a name="azure-resource-related-parameters"></a>Azure リソース関連のパラメーター

| パラメーター名 | 既定値のプレース ホルダー | プレース ホルダーの意味 | カスタマイズする方法 |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | プロビジョニング中に指定したサーバー管理者アカウントをAzure SQLする | プレースホルダーを削除し、実際の値を入力します |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | プロビジョニング中に指定したサーバー管理者パスワードをAzure SQLする | プレースホルダーを削除し、実際の値を入力します |

#### <a name="referencing-environment-variables-in-parameter-files"></a>パラメーター ファイル内の環境変数の参照

パラメーター ファイル内の値をハードコーディングしない場合 (たとえば、値がシークレットの場合など)。 パラメーター ファイルでは、環境変数からの値の参照がサポートされています。 ツールのパラメーター値の構文 `{{$env.YOUR_ENV_VARIABLE_NAME}}` を使用して、現在の環境変数から解決できます。

次の例では、環境変数 `DB_CONNECTION_STRING` からパラメーターの値 `mySelfHostedDbConnectionString` を読み取ります。

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
* 自動生成されたパラメーターの名前とプロパティ名は変更しません。 自動生成されたパラメーターは、プロジェクトにリソースまたは機能をさらに追加するときに使用できます。
* 自動生成された ARM テンプレートの出力は変更しません。 ARM テンプレートに追加の出力を追加できます。 出力は、 `.fx/states/state.{env}.json` 配置、マニフェスト ファイルの検証などの他の機能で使用できます。

### <a name="customization-scenarios"></a>カスタマイズ シナリオ

次のシナリオをカスタマイズできます。

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Teams アプリに既存の Azure AD アプリを使用する

次の構成スニペットをファイルに `.fx/configs/config.{env}.json` 追加して、Teams アプリ用に自分で作成した Azure AD アプリを使用できます。 Azure AD アプリを作成するには、次を参照してください <https://aka.ms/teamsfx-existing-aad-doc>。

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
> 複数の環境で同じ Azure AD アプリを共有しないようにしてください。 Azure AD アプリを更新するアクセス許可がない場合は、Azure AD アプリを手動で更新する方法に関する手順に関する警告を受け取ることができます。 手順に従って、プロビジョニング後に Azure AD アプリを更新します。

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>ボットに既存の Azure AD アプリを使用する

次の構成スニペットをファイルに `.fx/configs/config.{env}.json` 追加して、ボット用に自分で作成した Azure AD アプリを使用できます。

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

前のスニペットを追加した後、プロビジョニング中に実際のシークレットを解決するために、ツールの関連する環境変数にシークレットを追加します。

#### <a name="skip-adding-user-for-sql-database"></a>SQL データベースのユーザーの追加をスキップする

ツールが SQL データベースにユーザーを追加しようとしたときにアクセス許可エラーが不十分な場合は、次の構成スニペットをファイルに `.fx/configs/config.{env}.json` 追加して、SQL データベース ユーザーの追加をスキップできます。

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>Function App インスタンスの名前を指定する

既定の名前を使用 `contosoteamsappapi` する代わりに、関数アプリ インスタンスに使用できます。

> [!NOTE]
> 環境を既にプロビジョニングしている場合は、名前を指定すると、前に作成したインスタンスの名前を変更する代わりに、新しい関数アプリ インスタンスを作成できます。

次の手順を実行します。

1. 現在の環境用に開きます `.fx/configs/azure.parameters.{env}.json` 。
2. たとえば `functionAppName` 、セクションの下に新しいプロパティを `provisionParameters` 追加します。
3. たとえば`contosoteamsappapi`、次の`functionAppName`値を入力します。
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

他の Azure リソースまたはストレージをアプリケーションに追加するには、

次のような状況で問題が発生します。

Blob データを格納するために、Azure 関数バックエンドに Azure ストレージを追加する必要があります。 Azure Storage サポートを使用して Bicep テンプレートを更新する自動フローはありません。 ただし、Bicep ファイルを編集してリソースを追加することはできます。 手順は次のとおりです。

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

::: zone-end

::: zone pivot="visual-studio"

## <a name="provision-using-teams-toolkit-in-visual-studio"></a>Visual Studio で Teams Toolkit を使用してプロビジョニングする

次の手順は、Visual Studio を使用してクラウド リソースをプロビジョニングするのに役立ちます。

### <a name="sign-in-to-your-microsoft-365-account"></a>Microsoft 365 アカウントにサインインする

1. Visual Studio 2022 を開きます。
1. Microsoft Teams アプリ プロジェクトを開きます。
1. **[Project** > **Teams Toolkit Prepare** > **Teams アプリの依存関係] を選択します**。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare-app-dependencies1.png" alt-text="Teams アプリの依存関係を準備する":::

1. [ **サインイン** ] を選択して Azure アカウントにサインインします。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare1.png" alt-text="Microsoft 365 にサインインする":::

    > [!NOTE]
    > 既にログインしている場合、ユーザー名が表示されます。または、同じものを選択してアカウントを切り替えることができます。

1. 既定の Web ブラウザーが開き、アカウントに[サインイン](https://developer.microsoft.com/en-us/microsoft-365/dev-program)できます。

1. アカウントにサインインしたら **、[続行]** を選択します。

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-signin-M365.png" alt-text="[続行] を選択して確認する":::

### <a name="sign-in-to-your-azure-account"></a>Azure アカウントにサインインする

1. Visual Studio 2022 を開きます。
1. Teams アプリ プロジェクトを開きます。
1. クラウドで **Project** > **Teams Toolkit** > **のプロビジョニングを** 選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud2.png" alt-text="Azure アカウントにサインインする":::

1. **[サインイン...]** を選択して、Azure アカウントにサインインします。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-start.png" alt-text="Azure アカウントにサインインする":::

   > [!NOTE]
   > 既にログインしている場合、ユーザー名が表示されます。または、アカウントを切り替えることができます。

   資格情報を使用して Azure アカウントにサインインすると、ブラウザーは自動的に閉じます。

### <a name="to-provision-cloud-resources"></a>クラウド リソースをプロビジョニングする方法

Visual Studio でプロジェクトを開いた後:

1. クラウドで **Project** > **Teams Toolkit** > **のプロビジョニングを** 選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud2.png" alt-text="クラウドでのプロビジョニング":::

   [ **プロビジョニング]** ウィンドウが表示されます。

1. 次の詳細を入力してリソースをプロビジョニングします。

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-select-subscription1.png" alt-text="リソース グループの選択":::

   1. ドロップダウン リストから **サブスクリプション名** を選択します。
   1. ドロップダウン リストから **[リソース グループ]** を選択します。
   1. ドロップダウン リストから **リージョン** を選択します。

      > [!NOTE]
      > [新規 **] を選択** すると、新しいリソース グループを作成できます。

   1. **[プロビジョニング]** を選択します。

1. Azure の使用状況に従って料金が追加される可能性があることを示すダイアログが表示されます。 **[プロビジョニング]** を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-warning.png" alt-text="プロビジョニングの警告":::

   プロビジョニング プロセスにより、Azure クラウドにリソースが作成されます。 Teams Toolkit の出力ウィンドウを観察することで、進行状況を監視できます。

1. プロビジョニングが完了すると、メッセージが表示されます。 **[プロビジョニングされたリソースの表示]** を選択して、プロビジョニングされたすべてのリソースを表示します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-provision-success.png" alt-text="プロビジョニングされたリソースの表示":::

## <a name="create-resources"></a>リソースを作成する

Teams ツールキットまたは TeamsFx CLI でプロビジョニング コマンドをトリガーすると、次のリソースを作成できます。

* Microsoft 365 テナントの Microsoft Azure Active Directory (Azure AD) アプリケーション。
* Microsoft 365 テナントの Teams プラットフォームの Teams アプリの登録。
* 選択した Azure サブスクリプションの Azure リソース。

新しいプロジェクトを作成するときに、Azure リソースも作成する必要があります。 Azure Resource Manager (ARM) テンプレートは、すべての Azure リソースを定義し、プロビジョニング中に必要な Azure リソースを作成するのに役立ちます。

次の一覧は、さまざまな種類のアプリと Azure リソースのリソース作成を示しています。
<br>

<details>
<summary><b>Teams タブ アプリケーションのリソース作成</b></summary>

| Resource | 用途 | 説明 |
| --- | --- | --- |
| アプリ サービス プラン | タブの Web アプリをホストします。 | 対象外 |
| アプリ サービス | Blazor タブ アプリと、他のサービスへのアクセスに役立つシンプルな認証サーバーをホストします。 | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。 |
| ID を管理する | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有します。 |

</details>
<br>

<details>
<summary><b>Teams メッセージ拡張アプリケーションのリソース作成</b></summary>

| Resource | 用途 | 説明 |
| --- | --- | --- |
| Azure ボット | ボット フレームワークで、アプリをボットとして登録します。 | ボットを Teams に接続します。 |
| アプリ サービス プラン | Web ボット アプリをホストします。 | 対象外 |
| アプリ サービス | ボット アプリをホストします。 | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。 |
| ID を管理する | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有します。 |

</details>
<br>

<details>
<summary><b>Teams コマンド ボット アプリケーションのリソース作成</b></summary>

| Resource | 用途 | 説明 |
| --- | --- | --- |
| Azure ボット | ボット フレームワークで、アプリをボットとして登録します。 | ボットを Teams に接続します。 |
| アプリ サービス プラン | Web ボット アプリをホストします。 | 対象外 |
| アプリ サービス | ボット アプリをホストします。 | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。 |
| ID を管理する | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有します。 |

</details>
<br>

<details>
<summary><b>HTTP トリガー (Web API サーバー) アプリケーションを使用した Teams 通知ボットのリソース作成</b></summary>

| Resource | 用途 | 説明 |
| --- | --- | --- |
| Azure ボット | ボット フレームワークで、アプリをボットとして登録します。 | ボットを Teams に接続します。 |
| アプリ サービス プラン | Web ボット アプリをホストします。 | 対象外 |
| アプリ サービス | ボット アプリをホストします。 | 他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。 |
| マネージド ID | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有します。 |

</details>
<br>

<details>
<summary><b>HTTP トリガー (Azure 関数) アプリケーションを使用した Teams 通知ボットのリソース作成</b></summary>

| Resource | 用途 | 説明 |
| --- | --- | --- |
| Azure ボット | ボット フレームワークで、アプリをボットとして登録します。 | ボットを Teams に接続します。 |
| ID を管理する | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有されます。 |
| ストレージ アカウント | 関数アプリの作成に役立ちます。 | 対象外 |
| アプリ サービス プラン | 関数ボット アプリをホストします。 | 対象外 |
| 関数アプリ | ボット アプリをホストします。 | -他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。<br>-クロスオリジン リソース共有 (CORS) ルールを追加して、タブ アプリからの要求を許可します。<br>-Teams アプリからの要求のみを許可する認証設定を追加します。<br>-TeamsFx SDK で必要なアプリ設定を追加します。 |

</details>
<br>

<details>
<summary><b>タイマー トリガー (Azure 関数) アプリケーションを使用した Teams 通知ボットのリソース作成</b></summary>

| Resource | 用途 | 説明 |
| --- | --- | --- |
| Azure ボット | ボット フレームワークで、アプリをボットとして登録します。 | ボットを Teams に接続します。 |
| ID を管理する | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有します。 |
| ストレージ アカウント | 関数アプリの作成に役立ちます。 | 該当なし。 |
| アプリ サービス プラン | 関数ボット アプリをホストします。 | 対象外 |
| 関数アプリ | ボット アプリをホストします。 | -他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。<br>-クロスオリジン リソース共有 (CORS) ルールを追加して、タブ アプリからの要求を許可します。<br>-Teams アプリからの要求のみを許可する認証設定を追加します。<br>-TeamsFx SDK で必要なアプリ設定を追加します。 |

</details>
<br>

<details>
<summary><b>HTTP トリガー + タイマー トリガー (Azure 関数) アプリケーションを使用した Teams 通知ボットのリソース作成</b></summary>

| Resource | 用途 | 説明 |
| --- | --- | --- |
| Azure ボット | ボット フレームワークで、アプリをボットとして登録します。 | ボットを Teams に接続します。 |
| ID を管理する | Azure サービス間要求を認証します。 | さまざまな機能とリソース間で共有します。 |
| ストレージ アカウント | 関数アプリの作成に役立ちます。 | 対象外 |
| アプリ サービス プラン | 関数ボット アプリをホストします。 | 対象外 |
| 関数アプリ | ボット アプリをホストします。 | -他の Azure リソースにアクセスするためのユーザー割り当て ID を追加します。<br>-クロスオリジン リソース共有 (CORS) ルールを追加して、タブ アプリからの要求を許可します。<br>-Teams アプリからの要求のみを許可する認証設定を追加します。<br>-TeamsFx SDK で必要なアプリ設定を追加します。 |

</details>
<br>

### <a name="manage-your-resources"></a>リソースを管理する

[Azure ポータル](https://portal.azure.com/)にサインインし、Teams ツールキットによって作成されたすべてのリソースを管理できます。

* 既存の一覧のリソース グループまたは作成した新しいリソース グループを選択できます。
* 選択したリソース グループの詳細は、コンテンツ テーブルの概要セクションで確認できます。

## <a name="customize-resource-provision"></a>リソースのプロビジョニングをカスタマイズする

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
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | プロビジョニング中に作成されたアプリの Azure AD アプリ クライアント ID。 | [Teams アプリに既存の Azure AD アプリを使用する](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | プロビジョニング中に作成されたアプリの Azure AD アプリ クライアント シークレット。 | [Teams アプリに既存の Azure AD アプリを使用する](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | アプリの Azure AD アプリのテナント ID。 | [Teams アプリに既存の Azure AD アプリを使用する](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | アプリの Azure AD アプリの OAuth 機関ホスト。 | [Teams アプリに既存の Azure AD アプリを使用する](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | プロビジョニング中に作成されたボットの Azure AD アプリ クライアント ID。 | [ボットに既存の Azure AD アプリを使用する](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | プロビジョニング中に作成されたボットの Azure AD アプリ クライアント シークレット。 | [ボットに既存の Azure AD アプリを使用する](#use-an-existing-azure-ad-app-for-your-bot) |

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

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>Teams アプリに既存の Azure AD アプリを使用する

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

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>ボットに既存の Azure AD アプリを使用する

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

::: zone-end

## <a name="see-also"></a>関連項目

* [Teams アプリをクラウドに展開する](deploy.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
* [Teams プロジェクトで他の開発者と協力する](TeamsFx-collaboration.md)
* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy-teams-app.md)
* [Visual Studio を使用して Teams アプリ マニフェストを編集する](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [Visual Studio 用に Teams アプリをローカルでデバッグする](debug-teams-app-visual-studio.md)
