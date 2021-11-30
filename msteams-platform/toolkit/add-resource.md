---
title: リソースを自分のアプリTeamsする
author: MuyangAmigo
description: '[リソースの追加] Teams Toolkit'
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: dcaa4475db62be2cebbbe2b1b74e0bbbd7fb5398
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227757"
---
# <a name="add-cloud-resources-to-your-teams-app"></a>クラウド リソースをアプリにTeamsする

TeamsFx は、アプリケーション ホスティング用にクラウド リソースをプロビジョニングするのに役立ちます。 必要に応じて、開発ニーズに合ったクラウド リソースを追加することもできます。

## <a name="prerequisite"></a>前提条件

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> アプリ プロジェクトは既にTeams必要があります。

## <a name="add-cloud-resources-using-teams-toolkit"></a>クラウド リソースを使用してクラウド リソースをTeams Toolkit

> [!IMPORTANT]
> リソースを追加した後、各環境をプロビジョニングする必要があります。

1. [ファイル **Visual Studio Code] を開きます**。
1. 左側 **のTeams Toolkit** を選択します。

    ![ライセンス認証Teams Toolkit](./images/activate-teams-toolkit.png)

1. [サイド バー Teams Toolkitで、[クラウド リソースの **追加] を選択します**。

    ![クラウド リソースの追加](./images/add-cloud-resources.png)

    コマンド パレットを開き、[クラウド リソースの追加] Teams **入力することもできます**。
    
    > [!NOTE]
    > ツリー ビューからトリガーされるのと同じプロセスに従います。

    ![代替クラウド リソース](./images/alternate-cloud-resources.png)

1. ポップアップから、アプリ プロジェクトに追加するクラウド リソースTeams選択します。

     ![クラウド リソースの選択](./images/select-cloud-resources.png)

1. **[OK]** を選択します。

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>コマンド ウィンドウで TeamsFx CLI を使用してクラウド リソースを追加する

1. ディレクトリをプロジェクト ディレクトリ **に変更します**。
1. コマンドを実行して、さまざまな機能を追加します。

次の表に、クラウド リソースとそれらを追加する対応するコマンドについて説明します。

|クラウド リソース|コマンド|
|---------------|----------|
| Azure 関数|`teamsfx resource add azure-function --function-name your-func-name`|
| Azure SQL データベース|`teamsfx resource add --function-name your-func-name`|
| Azure API 管理|`teamsfx resource add azure-apim`|

## <a name="what-cloud-resources-can-be-added"></a>追加できるクラウド リソース

TeamsFx は、次のアプリケーション シナリオで一般的な Azure サービスとのシームレスな統合を提供します。

- [Azure 関数](/azure/azure-functions/functions-overview): アプリケーション バックエンド用の Web API の作成など、オンデマンド要件を満たすサーバーレス ソリューションTeamsです。
- [Azure SQL データベース](/azure/azure-sql/database/sql-database-paas-overview): サービスとしての完全に管理されたプラットフォーム (PaaS) データベース エンジンで、アプリケーション データ ストアTeams機能します。
- [Azure API 管理](/azure/azure-sql/database/sql-database-paas-overview): Teams アプリケーション用に作成された API を管理し、Power Apps などの他のアプリケーションで使用するように発行するために使用できる API ゲートウェイ。

## <a name="what-happens-when-you-add-resources"></a>リソースを追加するとどうなるか

リソースを追加すると、プロジェクトに対して次の変更が行います。

- azure.parameter に新しいパラメーターを追加できます。プロビジョニングに必要な情報を提供する {env}.json。
- 新しいコンテンツは、追加された Azure ARM作成するために、フォルダー (フォルダーの下のファイルを除く) の下のテンプレート `templates/azure` `templates/azure/teamsfx` に追加されます。
- フォルダーの `templates/azure/teamsfx` 下のファイルが再生成され、TeamsFx に必要な構成が Azure リソースの追加に関して最新の情報に更新されます。
- `.fx/projectSettings.json` は、プロジェクトに存在するリソースを追跡するために更新されます。

一方、リソースの種類ごとにいくつかの追加の変更があります。

|追加されたリソース|変更された変更|これらの変更が行われた理由|
|---------------|---------------|-----------------------------|
|Azure Functions|Azure Functions テンプレート コードがパスを持つサブフォルダーに追加される `yourProjectFolder/api`</br></br>`launch.json` フォルダー `task.json` の下で `.vscode` 更新されます。| hello world http トリガー テンプレートをプロジェクトに含める。</br></br> アプリケーションをローカルでデバッグするVisual Studio Code実行されるスクリプトを含めるには、次の操作を行います。|
|Azure API の管理|パスを持つサブフォルダーに追加された Open API 仕様ファイル `yourProjectFolder/openapi`|これは、発行後に API を定義する API 仕様ファイルです。|

## <a name="limitations"></a>制限事項

- 1 つの Function App / Azure SQL Database / APIM Service のみをプロジェクトに追加できます。
- プロジェクトにタブ アプリが含まれている場合は、リソースを追加できません。

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [クラウド リソースのプロビジョニング](provision.md)
