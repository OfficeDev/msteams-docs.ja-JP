---
title: クラウドにデプロイする
author: MuyangAmigo
description: このモジュールでは、クラウド、Azure、またはSharePointにアプリをデプロイし、Teams Toolkitを使用してTeamsアプリをデプロイする方法について説明します。
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: f7870a81c221182c98a0619d99c7cce255fcc170
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142053"
---
# <a name="deploy-to-the-cloud"></a>クラウドにデプロイする

Teams Toolkitは、アプリケーション内のフロントエンド コードとバックエンド コードを Azure でプロビジョニングされたクラウド リソースにデプロイまたはアップロードするのに役立ちます。

* フロントエンド アプリケーションなどのタブは、Azure Storage にデプロイされ、静的 Web ホスティングまたは SharePoint サイト用に構成されます。
* バックエンド API は Azure 関数にデプロイされます。
* ボットまたはメッセージ拡張機能は、Azure アプリ サービスにデプロイされます。

## <a name="prerequisite"></a>前提条件

* [Teams ツールキット バージョン v3.0.0+ をインストール](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)します。

> [!NOTE]
>
> * TEAMSアプリ プロジェクトが VS コードで開かれていることを確認します。
> * プロジェクト コードをクラウドにデプロイする前に、 [クラウド リソースをプロビジョニングします](provision.md)。

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Teams Toolkitを使用してTeams アプリをデプロイする

入門ガイドは、Teams Toolkitを使用したデプロイに役立ちます。 次を使用して、Teams アプリをデプロイできます。

* [アプリを Azure にデプロイする](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [アプリを SharePoint にデプロイする](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Teams アプリワークロードの詳細

| Teams アプリワークロード | ソース コード | 成果物をビルドする| ターゲット リソース |
|-------------|----------|---------------|---------------|
|Reactを含むタブ </br> フロントエンド ワークロード| `yourProjectFolder/tabs`| `tabs/build` |Azure Storage |
|SharePointのタブ </br> フロントエンド ワークロード | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint アプリ カタログ |
|Azure 関数上の API </br> バックエンド ワークロード | `yourProjectFolder/api`| 該当なし |Azure Functions |
|ボットとメッセージ拡張機能 </br> バックエンド ワークロード | `yourProjectFolder/bot` | 該当なし | Azure アプリ サービス |

> [!NOTE]
> プロジェクトに Azure API 管理リソースを含め、デプロイをトリガーする場合。 Azure 関数の API を Azure API 管理サービスに発行できます。

## <a name="see-also"></a>関連項目

* [クラウド リソースをさらに追加する](add-resource.md)
* [Azure クラウド サービスを作成してデプロイする](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [アプリの機能Teams追加する](add-capability.md)
* [CI/CD パイプラインを使用してプロジェクト コードをデプロイする](use-CICD-template.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
* [Teams プロジェクトで他の開発者と協力する](TeamsFx-collaboration.md)
