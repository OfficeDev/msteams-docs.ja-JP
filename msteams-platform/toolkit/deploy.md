---
title: クラウドにデプロイする
author: MuyangAmigo
description: アプリをクラウド、Azure、またはクラウドに展開SharePoint
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 35a60e718bb97cdcc24de66729e3929b2d21a59f
ms.sourcegitcommit: 2236204ff710f4eca606ceffb233572981f6edbe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2022
ms.locfileid: "64614531"
---
# <a name="deploy-to-the-cloud"></a>クラウドにデプロイする

Teams Toolkitアプリケーションのフロントエンドコードとバックエンド コードを Azure でプロビジョニングされたクラウド リソースに展開またはアップロードするのに役立ちます。

* フロントエンド アプリケーションなどのタブは Azure ストレージに展開され、静的 Web ホスティングまたは sharepoint サイト用に構成されます。
* バックエンド API は Azure 関数に展開されます。
* ボットまたはメッセージング拡張機能が Azure アプリ サービスに展開されます。

## <a name="prerequisite"></a>前提条件

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!NOTE]
>
> * VS コードでTeamsアプリ プロジェクトが開いているか確認します。
> * プロジェクト コードをクラウドに展開する前に、 [クラウド リソースを準備します](provision.md)。

## <a name="deploy-teams-apps-using-teams-toolkit"></a>アプリをTeamsしてアプリを展開Teams Toolkit

スタートガイドは、ユーザーがユーザーの情報を使用して展開Teams Toolkit。 次のコマンドを使用して、アプリをTeamsできます。

* [アプリを Azure に展開する](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [アプリをアプリに展開SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>アプリのワークロードTeams詳細

| Teamsのワークロード | ソース コード | ビルド成果物| ターゲット リソース |
|-------------|----------|---------------|---------------|
|タブとReact </br> フロントエンド ワークロード| `yourProjectFolder/tabs`| `tabs/build` |Azure ストレージ |
|タブとSharePoint </br> フロントエンド ワークロード | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint アプリ カタログ |
|Azure 関数の API </br> バックエンド ワークロード | `yourProjectFolder/api`| 該当なし |Azure 関数 |
|ボットとメッセージング拡張機能 </br> バックエンド ワークロード | `yourProjectFolder/bot` | 該当なし | Azure アプリ サービス |

> [!NOTE]
> Azure API 管理リソースをプロジェクトに含め、展開をトリガーする場合。 Azure 関数で API を Azure API 管理サービスに発行できます。

## <a name="see-also"></a>関連項目

* [クラウド リソースの追加](add-resource.md)
* [Azure クラウド サービスの作成と展開](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [アプリの機能Teams追加する](add-capability.md)
* [CI/CD パイプラインを使用してプロジェクト コードを展開する](use-CICD-template.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
* [Teams プロジェクトで他の開発者と協力する](TeamsFx-collaboration.md)
