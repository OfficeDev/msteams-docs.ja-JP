---
title: リソースを自分のアプリTeamsする
author: MuyangAmigo
description: '[リソースの追加] Teams Toolkit'
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# <a name="add-cloud-resources-to-your-teams-app"></a>クラウド リソースをアプリにTeamsする

TeamsFx は、アプリケーション ホスティング用にクラウド リソースをプロビジョニングするのに役立ちます。 必要に応じて、開発ニーズに合ったクラウド リソースを追加することもできます。

## <a name="prerequisite"></a>前提条件

[バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> アプリ プロジェクトをTeamsする必要VS Code。

## <a name="add-cloud-resources-using-teams-toolkit"></a>クラウド リソースを使用してクラウド リソースをTeams Toolkit

> [!IMPORTANT]
> リソースを追加した後、各環境をプロビジョニングする必要があります。

1. [ファイル **Visual Studio Code] を開きます**。
1. 左側 **のTeams Toolkit** を選択します。
1. [サイド バー Teams Toolkitで、[クラウド リソースの追加 **] を選択します**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add cloudresources.png" alt-text="リソースの追加":::

   コマンド パレットを開き、[クラウド リソースの追加] Teams **入力することもできます**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addcloud.png" alt-text="クラウド リソースの追加":::

1. ポップアップから、アプリ プロジェクトに追加するクラウド リソースをTeamsします。

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addresources.png" alt-text="add":::

1. [**OK**] を選択します。

選択したリソースは、プロジェクトに完全に追加されます。

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>コマンド ウィンドウで TeamsFx CLI を使用してクラウド リソースを追加する

1. ディレクトリをプロジェクト ディレクトリ **に変更します**。
1. 次のコマンドを実行して、プロジェクトに別のリソースを追加します。

|クラウド リソース|コマンド|
|---------------|----------|
| Azure 関数|`teamsfx resource add azure-function --function-name your-func-name`|
| Azure SQL データベース|`teamsfx resource add --function-name your-func-name`|
| Azure API 管理|`teamsfx resource add azure-apim`|
| Azure Key Vault|`teamsfx resource add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>クラウド リソースの種類

TeamsFx は、次のシナリオで Azure サービスと統合されます。

- [Azure 関数](/azure/azure-functions/functions-overview): アプリケーション バックエンド用の Web API の作成など、オンデマンド要件を満たすサーバーレス ソリューションTeamsです。
- [Azure SQL データベース](/azure/azure-sql/database/sql-database-paas-overview): サービスとしてのプラットフォーム (PaaS) データベース エンジンで、アプリケーション データ ストアTeams機能します。
- [Azure API 管理](/azure/azure-sql/database/sql-database-paas-overview): Teams アプリケーション用に作成された API を管理し、それらを発行して Power アプリなどの他のアプリケーションで使用するために使用できる API ゲートウェイ。
- [Azure Key Vault](/azure/key-vault/general/overview): クラウド アプリとサービスで使用される暗号化キーおよび他のシークレットを保護します。

## <a name="add-cloud-resources"></a>クラウド リソースの追加

リソースを追加した後、プロジェクトの変更点は次のとおりです。

- azure.parameter に新しいパラメーターを追加できます。プロビジョニングに必要な情報を提供する {env}.json。
- 新しいコンテンツは、追加 `templates/azure` `templates/azure/teamsfx` ARM Azure リソースを作成するフォルダーの下のファイルを除き、フォルダーの下のテンプレートに追加されます。
- フォルダーの下のファイル `templates/azure/teamsfx` が再生成され、TeamsFx に必要な構成が Azure リソースの追加に関して最新の情報に更新されます。
- `.fx/projectSettings.json` は、プロジェクトに存在するリソースを追跡するために更新されます。

resouces を追加した後、プロジェクトの追加の変更点は次のとおりです。

|リソース|変更内容|説明|
|---------------|---------------|-----------------------------|
|Azure 関数|Azure 関数テンプレート コードがパスを持つサブフォルダーに追加される `yourProjectFolder/api`</br></br>`launch.json` フォルダー `task.json` の下で更新 `.vscode` されます。| プロジェクトに hello world http トリガー テンプレートを含む。</br></br> アプリケーションをローカルでデバッグVisual Studio Code実行するために必要なスクリプトが含まれています。|
|Azure API 管理|パスを持つサブフォルダーに追加された開いている API 仕様ファイル `yourProjectFolder/openapi`|発行後に API を定義します。API 仕様ファイルです。|

## <a name="limitation"></a>制限

ベースのタブ プロジェクトを作成した場合はSPFx追加できません。

## <a name="see-also"></a>関連項目

[クラウド リソースをプロビジョニングする](provision.md)
