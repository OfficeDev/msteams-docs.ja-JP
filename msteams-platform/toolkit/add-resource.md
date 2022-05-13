---
title: Teams アプリにリソースを追加する
author: MuyangAmigo
description: Teams Toolkit のリソースの追加について説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 50cd3de693f70fd0c8414408bd6f4e6d3332d544
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2022
ms.locfileid: "65297206"
---
# <a name="add-cloud-resources-to-your-teams-app"></a>Teams アプリにクラウド リソースを追加する

TeamsFx は、アプリケーション ホスティング用にクラウド リソースをプロビジョニングするのに役立ちます。 必要に応じて、開発ニーズに合ったクラウド リソースを追加することもできます。

## <a name="prerequisite"></a>前提条件

[Teams ツールキット バージョン v3.0.0+ をインストール](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)します。

> [!TIP]
> Teams アプリ プロジェクトが Visual Studio Code にあることを確認します。

## <a name="add-cloud-resources-using-teams-toolkit"></a>Teams Toolkit を使用してクラウド リソースを追加する

> [!IMPORTANT]
> リソースを追加した後は、各環境をプロビジョニングする必要があります。

1. **Microsoft Visual Studio Code** を開きます。
1. 左側のウィンドウから **Teams Toolkit** を選択します。
1. Teams Toolkit サイド バー パネルで、[**クラウド リソースの追加**] を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add cloudresources.png" alt-text="リソースの追加":::

   コマンド パレットを開き、「**Teams: クラウド リソースを追加する**」と入力することもできます。

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addcloud.png" alt-text="クラウド リソースを追加する":::

1. ポップアップから、Teams アプリ プロジェクトに追加するクラウド リソースを選択します。

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addresources.png" alt-text="追加":::

1. **[OK]** を選択します。

選択したリソースがプロジェクトに正常に追加されます。

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>コマンド ウィンドウで TeamsFx CLI を使用してクラウド リソースを追加する

1. **プロジェクト ディレクトリ** をプロジェクト フォルダーに変更します。
1. 次のコマンドを実行して、プロジェクトに異なるリソースを追加します。

|クラウド リソース|コマンド|
|---------------|----------|
| Azure 関数|`teamsfx resource add azure-function --function-name your-func-name`|
| Azure SQL データベース|`teamsfx resource add --function-name your-func-name`|
| Azure API 管理|`teamsfx resource add azure-apim`|
| Azure Key Vault|`teamsfx resource add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>クラウド リソースの種類

TeamsFx は、次のシナリオで Azure サービスと統合されます:

- [Azure 関数](/azure/azure-functions/functions-overview): Teams アプリケーション バックエンド用の Web API の作成など、オンデマンド要件を満たすサーバーレス ソリューション。
- [Azure SQL Database](/azure/azure-sql/database/sql-database-paas-overview): Teams アプリケーション データ ストアとして機能するサービスとしてのプラットフォーム (PaaS) のデータベース エンジン。
- [Azure API Management](deploy.md): Teams アプリケーション用に作成された API を管理し、Power アプリなどの他のアプリケーションで使用するために公開するために使用できる API ゲートウェイ。
- [Azure Key Vault](/azure/key-vault/general/overview): クラウド アプリとサービスで使用される暗号化キーとその他のシークレットを保護します。

## <a name="add-cloud-resources"></a>クラウド リソースの追加

リソースを追加すると、プロジェクトの変更は次のようになります:

- プロビジョニングに必要な情報を提供するために新しいパラメータを azure.parameter.{env}.json に追加できます。
- 新しいコンテンツは、追加された Azure リソースを作成する `templates/azure/teamsfx` フォルダーの下のファイルを除き、`templates/azure` フォルダーの下の ARM テンプレートに追加されます。
- `templates/azure/teamsfx` フォルダー下のファイルは、追加された Azure リソースに対して TeamsFx に必要な構成が最新であることを確認するために再生成されるものです。
- `.fx/projectSettings.json` は、プロジェクトに存在するリソースを追跡するために更新されます。

リソースを追加した後、プロジェクト内での追加の変化は次のものです:

|リソース|変更内容|説明|
|---------------|---------------|-----------------------------|
|Azure Functions|Azure Functions テンプレート コードがパス `yourProjectFolder/api` を持つサブフォルダーに追加される</br></br>`launch.json` と `task.json` が `.visual studio code` フォルダーで更新されました。| hello world http トリガー テンプレートがプロジェクトに含まれます。</br></br> アプリケーションをローカルでデバッグするときに実行する Visual Studio コードに必要なスクリプトが含まれています。|
|Azure API 管理|パス `yourProjectFolder/openapi` を持つサブフォルダーに追加された開いている API 仕様ファイル|公開後に API を定義します。これは API 仕様ファイルです。|

## <a name="limitation"></a>制限

SPFx ベースのタブ プロジェクトを作成した場合は、リソースを追加できません。

## <a name="see-also"></a>関連項目

[クラウド リソースをプロビジョニングする](provision.md)
