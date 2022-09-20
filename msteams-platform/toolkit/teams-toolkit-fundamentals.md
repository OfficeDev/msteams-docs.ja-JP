---
title: Teams ツールキットの概要
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit、Teams Toolkit のインストール、Teams Toolkit のユーザー体験について説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: bdcf92b52956eee6db21eb03d115a494c0f063e9
ms.sourcegitcommit: dccb48902e08484692ab927415bcd3d61dc50db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2022
ms.locfileid: "67806774"
---
# <a name="teams-toolkit-overview"></a>Teams ツールキットの概要

Teams Toolkit は、Microsoft Visual Studio Code と Visual Studio の両方で多機能を実行できる機能です。 Teams Toolkit の助けを借りて、アプリの作成からデプロイ、カスタマイズまでのプロセスを自動化できます。 Teams Toolkit のさまざまな機能と利点については、選択した環境に関するそれぞれのドキュメントで説明されています。

::: zone pivot="visual-studio-code"

## <a name="teams-toolkit-overview-for--visual-studio-code"></a>Teams Toolkit の Visual Studio Code の概要

Teams Toolkit を使用すると、Visual Studio Code.App 開発から直接 Teams アプリを作成、デバッグ、デプロイできます。ツールキットを使用すると、次の利点があります。

* 統合 ID
* クラウド ストレージへのアクセス
* Microsoft Graph からユーザー データにアクセスする
* ゼロ構成アプローチの Azure および Microsoft 365 サービス。

Teamsアプリ開発では、Visual Studio の Teams Toolkit と同様に、Toolkit `teamsfx` で構成される [CLI ツール](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)を使用できます。

## <a name="user-journey-of-teams-toolkit"></a>Teams Toolkit のユーザー体験

Teams Toolkit は手動作業を自動化し、Teams と Azure リソースの優れた統合を提供します。 次の画像は、Teams Toolkit のユーザー体験を示しています。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Teams Toolkit のユーザー体験" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

この体験の主なマイルストーンは次のとおりです。

1. まず、新しいプロジェクトを作成するか、サンプル Teams アプリを試します。
1. 必要に応じて、機能を追加するか、マニフェスト ファイルを編集します。
1. Microsoft 365 アカウントを使用して、Teams アプリをビルドしてデバッグします。
1. Azure アカウントを使用して、アプリをプロビジョニングしてクラウドにデプロイします。
1. アプリを Teams に公開する

次の表は、Visual Studio Code で Teams Toolkit の概要を取得するのに役立ちます。

| プロセス | 説明 |
| ---- | ---- |
| Teams Toolkit のインストール | Teams Toolkit は、次の 2 つの方法でインストールできます。 <br> - Visual Studio Code の使用 <br> - Visual Studio Code Marketplace の使用|
| ビルド環境のサポート | 環境には次の 2 種類があります。 <br> - Javascript または Typescript <br> - SPFx |
| アプリの種類と Azure 関数のサポート | アプリには次の 2 種類があります。 <br> - タブ、ボット、メッセージ拡張機能などの機能ベースのアプリ  <br> - シナリオベースの Teams アプリ (通知ボット、コマンド ボット、SSO が有効な個人用タブなど) |
| Teams アプリを開発する | 次のものが含まれます。 <br> - 環境の追加と管理 <br> - マルチ機能アプリを作成する <br> - 機能ベースのクラウド リソースを作成する <br> - サード パーティ API を統合する <br> - マニフェスト ファイルをカスタマイズする <br> - TeamsFx SDK |
| Teams アプリをデバッグする | 次のものが含まれます。 <br> - Teams アプリをローカルでデバッグする <br> - バックグラウンド プロセスをデバッグする|
| Teams アプリをホストする | 次のものが含まれます。 <br> - クラウドにリソースをプロビジョニングする <br> - クラウドにデプロイする|
| Teams アプリをテストする | 次のものが含まれます。 <br> - 統合と併置 <br> - Zip Teams メタデータ パッケージ <br> - Teams 環境でアプリをサイドロードしてテストする <br> - 異なる環境でアプリの動作をテストする|
| Teams アプリの発行 | 次のものが含まれます。 <br> - アプリを発行する <br> - 管理者の承認を管理する <br> - 公開して保存する <br> - 開発者ポータルと統合する |

### <a name="entities-integrated-with-teams-toolkit"></a>Teams Toolkit と統合されたエンティティ

Teams Toolkit は Visual Studio Code の拡張機能です。 Azure AD や Microsoft 365、開発者ポータル、Microsoft グラフなど、Teams Toolkit 内の次のエンティティと統合されています。 すべてのエンティティは Teams Toolkit 内に統合されており、ユーザーがアプリを作成するのに役立ちます。

| Entities | 説明 |
| ---- | ---- |
| Azure AD  | Azure Active Directory (Azure AD) は、クラウドベースの ID とアクセス管理サービスです。 このサービスは、従業員が Microsoft 365、Azure portal、その他数千の SaaS アプリケーションなどの外部リソースにアクセスするのに役立ちます。 |
| Microsoft 365  | アプリの開発中に Teams 開発者アカウント。|
| 開発者ポータル | Teams 用開発者ポータルは、Microsoft Teams アプリを構成、配布、管理するための主要なツールです。 開発者ポータルを使用すると、アプリで同僚と共同作業したり、ランタイム環境を設定したりできます。 |
| Microsoft Graph | Microsoft Graph は、Microsoft 365 のデータとインテリジェンスへの入り口です。 Microsoft Graph は、Microsoft 365、Windows、および Enterprise Mobility + Security の膨大な量のデータにアクセスする際に使用できる統合型プログラミング モデルを提供します。 |

Teams Toolkit は、Teams アプリのビルドに必要なすべてのツールを 1 か所にまとめています。

## <a name="manage-your-apps-using-developer-portal"></a>開発者ポータルを使用してアプリを管理する

Teams Toolkit は開発者ポータルと統合されているため、アプリを作成した後、デプロイの下で Teams   [用の開発者ポータル](../concepts/build-and-test/teams-developer-portal.md)を使用してアプリを構成、配布、管理できます。 詳細については、 [開発者ポータルを使用した Teams アプリの管理に](../concepts/build-and-test/manage-your-apps-in-developer-portal.md)関するページを参照してください。

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="開発者ポータル":::

::: zone-end

::: zone pivot="visual-studio"

## <a name="teams-toolkit-overview-for-visual-studio"></a>Visual Studio 用 Teams ツールキットの概要

Visual Studio 用 Teams ツールキットは、Microsoft Teams アプリの作成、デバッグ、展開に役立ちます。 Visual Studio 用 Teams ツールキットは、Visual Studio 2022 バージョン 17.3 の GA です。 Teams ツールキットを使用したアプリ開発には、次の利点があります。

* 統合 ID
* クラウド ストレージへのアクセス
* Microsoft Graph からユーザー データにアクセスする
* ゼロ構成アプローチを使用した Azure サービスとMicrosoft 365 サービス

Teams アプリ開発には、[CLI ツール](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)を使用することもできます。これは、ツールキットを含む Microsoft Visual Studio Code 用 Teams ツールキット `teamsfx` に似ています。

Teams ツールキットは、Teams アプリのビルドに必要なすべてのツールを 1 か所にまとめています。

> [!NOTE]
> Teams ツールキットは、他のバージョンでは使用できません。

## <a name="user-journey-of-teams-toolkit"></a>Teams ツールキットのユーザー体験

Teams ツールキットは手動作業を自動化し、Teams と Azure リソースの優れた統合を提供します。 次の画像は、ユーザー体験を示しています。

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png" alt-text="Teams ツールキットのユーザー体験" lightbox="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png":::

この体験の主なマイルストーンは次のとおりです。

1. まず、新しいプロジェクトを作成するか、サンプルの Teams アプリをビルドしてみてください。
1. その後、必要に応じてコードまたはマニフェスト ファイルを編集できます。
1. Teams アプリのビルドとデバッグには、Microsoft 365 アカウントを使用できます。
1. アプリをプロビジョニングしてクラウドに展開するには、Azure アカウントを使用できます。
1. 最後にアプリを Teams に発行できます。

Teams Toolkit for Visual Studio では、Microsoft Visual Studio Code の Teams Toolkit と比較しても、次の操作はサポートされていませんが、今後の製品ロードマップで計画されています。

* Teams アプリに Teams 機能をさらに追加します。
* Teams アプリに Azure リソースをさらに追加する
* Teams アプリにシングル サインオン (SSO) を追加します。
* Teams アプリに API 接続を追加します。
* Microsoft Azure Active Directory (Azure AD) マニフェストをカスタマイズします。
* CI/CD パイプラインを追加します。
* 複数のクラウド環境を管理します。
* Teams プロジェクトで共同作業を行います。
* Teams アプリを公開します。

### <a name="teamsfx-net-sdk-reference-docs"></a>TeamsFx .NET SDK リファレンス ドキュメント

* [Microsoft.Extensions.DependencyInjection 名前空間](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Microsoft.TeamsFx 名前空間](/../dotnet/api/Microsoft.TeamsFx)
* [Microsoft.TeamsFx.Configuration 名前空間](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Microsoft.TeamsFx.Conversation 名前空間](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Microsoft.TeamsFx.Helper 名前空間](/../dotnet/api/Microsoft.TeamsFx.Helper)

::: zone-end

## <a name="see-also"></a>関連項目

* [Visual Studio で新しい Teams アプリを作成する](create-new-teams-app-for-Visual-Studio.md)
* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy-teams-app.md)

