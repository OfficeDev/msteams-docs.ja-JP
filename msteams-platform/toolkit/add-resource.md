---
title: Teams アプリにリソースを追加する
author: MuyangAmigo
description: このモジュールでは、Teams Toolkit のリソース、利点、制限事項、および機能を追加する方法について説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: fc58610802a51af19efc32e579566fbf5e36feca
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616535"
---
# <a name="add-cloud-resources-to-microsoft-teams-app"></a>Microsoft Teams アプリにクラウド リソースを追加する

Teams Toolkit を使用すると、アプリケーション ホスティング用にクラウド リソースをプロビジョニングできます。 必要に応じて、開発ニーズに合わせてクラウド リソースを追加できます。 TeamsFx にクラウド リソースを追加する利点は、Teams Toolkit を使用してすべての構成ファイルを自動生成し、Teams アプリに接続できることです。

> [!NOTE]
> SPFx ベースのタブ プロジェクトを作成した場合、Azure クラウド リソースを追加することはできません。

## <a name="add-cloud-resources"></a>Teams アプリにクラウド リソースを追加する

クラウド リソースは、次の方法で追加できます。

### <a name="to-add-cloud-resources-by-using-teams-toolkit-in-visual-studio-code"></a>Visual Studio Code で Teams Toolkit を使用してクラウド リソースを追加するには

   1. **Visual Studio Code** を開きます。
   1. アクティビティ バーから **Teams Toolkit** を選択します。
   1. **[開発**] で [**機能の追加]** を選択します。

        :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/select-feature-updated.png" alt-text="Teams Toolkit から機能を追加する":::

### <a name="to-add-cloud-resources-by-using-command-palette"></a>コマンド パレットを使用してクラウド リソースを追加するには

   1. **[コマンド** パレットの表示 > **] を** 選択します。または **Ctrl + Shift + P** キーを押します。

      :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/Teams-add-features.png" alt-text="コマンド パレットから機能を追加する":::

   1. **Teams に入る: 機能を追加** します。
   1. **[Enter]** キーを押します。

      :::image type="content" source="../assets/images/teams-toolkit-v2/manual/cloud/Teams-add-features1.png" alt-text="機能の追加と入力":::

   1. ポップアップから、プロジェクトに追加する **クラウド リソース** を選択します。

      :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/updated-final-cloud.png" alt-text="最終的な":::

  > [!NOTE]
  > Teams アプリでリソースを正常に追加した後は、環境ごとにプロビジョニングする必要があります。

### <a name="add-cloud-resources-using-teamsfx-cli"></a>TeamsFx CLI を使用してクラウド リソースを追加する

* **プロジェクト ディレクトリ** をプロジェクト フォルダーに変更します。
* 次の表に、機能と必要なコマンドの一覧を示します。

  |クラウド リソース|コマンド|
  |---------------|----------|
  | Azure 関数|`teamsfx add azure-function`|
  | Azure SQL データベース|`teamsfx add azure-sql`|
  | Azure API 管理|`teamsfx add azure-apim`|
  | Azure Key Vault|`teamsfx add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>クラウド リソースの種類

次のシナリオでは、TeamsFx は Azure サービスと統合されます。

* [Azure 関数](/azure/azure-functions/functions-overview): Teams アプリケーション バックエンド用の Web API の作成など、オンデマンド要件を満たすサーバーレス ソリューション。
* [Azure SQL Database](/azure/azure-sql/database/sql-database-paas-overview): Teams アプリケーション データ ストアとして機能するサービスとしてのプラットフォーム (PaaS) のデータベース エンジン。
* [Azure API Management](deploy.md): API ゲートウェイを使用して、Teams アプリケーション用に作成された API を管理し、Power アプリなどの他のアプリケーションで使用するように公開できます。
* [Azure Key Vault](/azure/key-vault/general/overview): クラウド アプリとサービスで使用される暗号化キーとその他のシークレットを保護します。

## <a name="changes-after-adding-cloud-resources"></a>クラウド リソースを追加した後の変更

プロジェクトにリソースを追加すると、次の変更が表示されます。

* azure.parameter に追加された新しいパラメーター。プロビジョニングに必要な情報を提供する {env}.json。
* 新しいコンテンツは ARM テンプレートの下 `templates/azure`に含まれます。ただし、ファイルは Azure リソースを追加するためのフォルダーにあります `templates/azure/teamsfx` 。
* `templates/azure/teamsfx` フォルダー下のファイルは、追加された Azure リソースに対して TeamsFx に必要な構成が最新であることを確認するために再生成されるものです。
* `.fx/projectSettings.json` は、プロジェクトで使用可能なリソースを追跡するために更新されます。

プロジェクトにリソースを追加すると、次の追加の変更が表示されます。

|リソース|変更内容|説明|
|---------------|---------------|-----------------------------|
|Azure Functions|Azure Functions テンプレート コードがパス `yourProjectFolder/api` を持つサブフォルダーに追加される</br></br>`launch.json` と `task.json` が `.visual studio code` フォルダーで更新されました。| hello world http トリガー テンプレートがプロジェクトに含まれます。</br></br> アプリケーションをローカルでデバッグするときに実行する Visual Studio コードに必要なスクリプトが含まれています。|
|Azure API 管理|パス `yourProjectFolder/openapi` を持つサブフォルダーに追加された開いている API 仕様ファイル|公開後に API を定義します。これは API 仕様ファイルです。|

## <a name="see-also"></a>関連項目

* [クラウド リソースをプロビジョニングする](provision.md)
* [[新しい Teams アプリを作成]](create-new-project.md)
* [Teams アプリに機能を追加する](add-capability.md)
* [クラウドにデプロイする](deploy.md)
