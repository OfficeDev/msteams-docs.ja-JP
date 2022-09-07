---
title: クラウドにデプロイする
author: MuyangAmigo
description: このモジュールでは、クラウド、Azure、または SharePoint にアプリをデプロイし、Teams Toolkit を使用して Teams アプリをデプロイする方法について説明します。
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9ad2c9d16901990344ca521599b94b84b0e76217
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616927"
---
# <a name="deploy-teams-app-to-the-cloud"></a>Teams アプリをクラウドに展開する

Teams Toolkit を使用すると、アプリケーション内のフロントエンドコードとバックエンド コードを Azure でプロビジョニングされたクラウド リソースにデプロイまたはアップロードできます。 次をクラウドにデプロイできます。

* フロントエンド アプリケーションなどのタブは、Azure Storage にデプロイされ、静的 Web ホスティングまたは SharePoint サイト用に構成されます。
* バックエンド API は Azure 関数にデプロイされます。
* ボットまたはメッセージ拡張機能は、Azure アプリ サービスにデプロイされます。

  > [!NOTE]
  > Azure クラウドにアプリ コードをデプロイする前に、 [クラウド リソースのプロビジョニング](provision.md)を正常に完了する必要があります。

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Teams Toolkit を使用して Teams アプリを展開する

入門ガイドは、Teams Toolkit を使用して展開するのに役立ちます。 以下を使用して Teams アプリを展開できます。

* [アプリを Azure にデプロイする](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [アプリを SharePoint にデプロイする](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Teams アプリワークロードの詳細

| Teams アプリのワークロード | ソース コード | 成果物をビルドする| ターゲット リソース |
|-------------|----------|---------------|---------------|
|Reactを含むタブ </br> フロントエンド ワークロード| `yourProjectFolder/tabs`| `tabs/build` |Azure Storage |
|SharePoint を使用したタブ </br> フロントエンド ワークロード | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint アプリ カタログ |
|Azure 関数上の API </br> バックエンド ワークロード | `yourProjectFolder/api`| 対象外 |Azure Functions |
|ボットとメッセージ拡張機能 </br> バックエンド ワークロード | `yourProjectFolder/bot` | 対象外 | Azure アプリ サービス |

> [!NOTE]
> プロジェクトに Azure API 管理リソースを含め、デプロイをトリガーすると、Azure Functions で API を Azure API 管理サービスに発行できます。

## <a name="see-also"></a>関連項目

* [Azure クラウド サービスを作成してデプロイする](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [マルチ機能 Teams アプリを作成する](add-capability.md)
* [Microsoft Teams アプリにクラウド リソースを追加する](add-resource.md)
