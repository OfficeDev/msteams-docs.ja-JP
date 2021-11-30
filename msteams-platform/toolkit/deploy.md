---
title: クラウドへの展開
author: MuyangAmigo
description: クラウドへの展開
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 3f7dc4b320bccfa8a6017f87045b27a37d8199f7
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227736"
---
# <a name="deploy-to-the-cloud"></a>クラウドへの展開

Teams Toolkit、アプリケーションのフロントエンドコードとバックエンド コードを Azure のプロビジョニングされたクラウド リソースに展開またはアップロードするのに役立ちます。

* フロントエンド アプリケーションなどの Tab は Azure ストレージに展開され、静的な Web ホスティングまたはサイトSharePointされます。
* バックエンド API は Azure Functions に展開されます。
* ボットまたはメッセージング拡張機能が Azure App Service に展開されます。

## <a name="prerequisite"></a>前提条件

* [バージョン Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) v3.0.0 以上をインストールします。

> [!TIP]
> VS コードで開Teamsアプリ プロジェクトを既に持っている必要があります。

> [!NOTE]
> プロジェクト コードをクラウドに展開する前に、最初にクラウド リソース [のプロビジョニング手順を](provision.md) 実行します。


## <a name="deploy-teams-apps-using-teams-toolkit"></a>アプリをTeamsしてアプリを展開Teams Toolkit

[スタートガイド] のチュートリアルでは、このチュートリアルを使用して展開する方法の手順Teams Toolkit。 次のコマンドを使用して、アプリをTeamsできます。

* [アプリを Azure に展開する](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [アプリをアプリに展開SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workloads"></a>アプリのワークロードTeams詳細

| Teamsアプリのワークロード| ソース コード | ビルド Artifacts| ターゲット リソース |
|-------------|----------|---------------|---------------|
|タブとReact </br> フロントエンド ワークロード| `yourProjectFolder/tabs`| `tabs/build` |Azure Storage |
|タブとSharePoint </br> フロントエンド ワークロード | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint アプリ カタログ |
|Azure 関数の API </br> バックエンド ワークロード | `yourProjectFolder/api`| N/A |Azure Functions |
|ボットとメッセージング拡張機能 </br> バックエンド ワークロード | `yourProjectFolder/bot` | N/A | Azure App Service |

> [!NOTE]
> Azure API 管理リソースをプロジェクトに含め、展開をトリガーする場合。 Azure Functions で API を Azure API 管理サービスに発行できます。

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [クラウド リソースの追加](add-resource.md)

> [!div class="nextstepaction"]
> [アプリの機能Teams追加する](add-capability.md)

> [!div class="nextstepaction"]
> [CI/CD パイプラインを使用してプロジェクト コードを展開する](use-CICD-template.md)

> [!div class="nextstepaction"]
> [複数の環境を管理する](TeamsFx-multi-env.md)

> [!div class="nextstepaction"]
> [プロジェクトで他の開発者とTeamsする](TeamsFx-collaboration.md)
