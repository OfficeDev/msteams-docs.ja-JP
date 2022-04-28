---
title: クラウドにデプロイする
author: MuyangAmigo
description: クラウド、Azure、またはSharePointにアプリをデプロイする
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 1d0ade9abed4be212abfb96068626172c4f0f03e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104148"
---
# <a name="deploy-to-the-cloud"></a>クラウドにデプロイする

Teams Toolkitは、アプリケーション内のフロントエンド コードとバックエンド コードを Azure でプロビジョニングされたクラウド リソースにデプロイまたはアップロードするのに役立ちます。

* フロントエンド アプリケーションなどのタブは、Azure Storage にデプロイされ、静的 Web ホスティングまたは SharePoint サイト用に構成されます。
* バックエンド API は Azure 関数にデプロイされます。
* ボットまたはメッセージ拡張機能は、Azure アプリ サービスにデプロイされます。

## <a name="prerequisite"></a>前提条件

* バージョン v3.0.0 以降[Teams Toolkitインストール](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)します。

> [!NOTE]
>
> * TEAMSアプリ プロジェクトが VS コードで開かれていることを確認します。
> * プロジェクト コードをクラウドにデプロイする前に、 [クラウド リソースをプロビジョニングします](provision.md)。

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Teams Toolkitを使用してTeams アプリをデプロイする

入門ガイドは、Teams Toolkitを使用したデプロイに役立ちます。 次を使用して、Teams アプリをデプロイできます。

* [アプリを Azure にデプロイする](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [アプリをSharePointにデプロイする](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Teams アプリワークロードの詳細

| Teams アプリワークロード | ソースコード | 成果物をビルドする| ターゲット リソース |
|-------------|----------|---------------|---------------|
|Reactを含むタブ </br> フロントエンド ワークロード| `yourProjectFolder/tabs`| `tabs/build` |Azure Storage |
|SharePointのタブ </br> フロントエンド ワークロード | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint アプリ カタログ |
|Azure 関数上の API </br> バックエンド ワークロード | `yourProjectFolder/api`| 該当しない |Azure 関数 |
|ボットとメッセージ拡張機能 </br> バックエンド ワークロード | `yourProjectFolder/bot` | 該当しない | Azure アプリ サービス |

> [!NOTE]
> プロジェクトに Azure API 管理リソースを含め、デプロイをトリガーする場合。 Azure 関数の API を Azure API 管理サービスに発行できます。

## <a name="see-also"></a>関連項目

* [クラウド リソースをさらに追加する](add-resource.md)
* [Azure クラウド サービスを作成してデプロイする](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [アプリの機能Teams追加する](add-capability.md)
* [CI/CD パイプラインを使用してプロジェクト コードをデプロイする](use-CICD-template.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
* [Teams プロジェクトで他の開発者と協力する](TeamsFx-collaboration.md)
