---
title: Visual Studio 用 Teams ツールキットの概要
author: surbhigupta
description: このモジュールでは、Visual Studio 用 Teams ツールキットの概要について説明します
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
ms.openlocfilehash: 0f51d2c44eef3ec09d48581a797c63d501be8644
ms.sourcegitcommit: f192d7685ee3ddf4a55dc9787d56744403c3f8f9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2022
ms.locfileid: "67302452"
---
# <a name="teams-toolkit-overview-for-visual-studio"></a>Visual Studio 用 Teams ツールキットの概要

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

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png" alt-text="Teams ツールキットのユーザー体験":::

この体験の主なマイルストーンは次のとおりです。

1. まず、新しいプロジェクトを作成するか、サンプルの Teams アプリをビルドしてみてください。
1. その後、必要に応じてコードまたはマニフェスト ファイルを編集できます。
1. Teams アプリのビルドとデバッグには、Microsoft 365 アカウントを使用できます。
1. アプリをプロビジョニングしてクラウドに展開するには、Azure アカウントを使用できます。
1. 最後にアプリを Teams に発行できます。

## <a name="install-teams-toolkit-for-visual-studio"></a>Visual Studio 用 Teams ツールキットのインストール

最新の Visual Studio インストーラーは、[Visual Studio のダウンロード ページ](https://visualstudio.microsoft.com/vs/preview/)からダウンロードできます。

> [!NOTE]
> Visual Studio をインストールする前に、最初に Visual Studio インストーラーをインストールする必要があります。

Visual Studio インストーラーを開いたら、ポップアップ の [ワークロード] ウィンドウで次の操作を実行します。

1. **[ASP.NET と Web 開発]** のワークロードを選択します。
1. インストールの詳細パネルで、**[Microsoft Teams 開発ツール]** のボックスを選択します。
1. [**インストール**] を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install1.png" alt-text="Visual Studio のインストール":::

1. **[起動]** を選択して Visual Studio を開きます。

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch.png" alt-text="Visual Studio を起動する":::

   > [!IMPORTANT]
   > Visual Studio 用 Teams ツールキットは Visual Studio 2022 バージョン 17.3.0 の GA であるため、このバージョンをダウンロードすることをお勧めします。 この記事は、Visual Studio 2022 バージョン 17.3.0 を対象としています。 Teams ツールキット バージョン 17.3.* 以降。

## <a name="take-a-tour-of-teams-toolkit"></a>Teams Toolkit のツアーに参加する

Teams ツールキットをインストールした後、Teams ツールキットのさまざまなメニュー オプションを簡単に確認できます。

1. **[プロジェクト]** を選択します。
1. **[Teams ツールキット]** を選択します。
1. これで、**[Teams ツールキットのメニュー]** オプションにアクセスできます。

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu.png" alt-text="Teams ツールキットの操作メニュー":::

   ソリューション エクスプローラーから Teams ツールキットのメニューにアクセスすることもできます。

4. **プロジェクト** を右クリックします。
5. **[Teams ツールキット]** > **[Teams ツールキットのメニュー]** オプションの順に選択します。

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu1.png" alt-text="プロジェクトからの Teams ツールキットの操作":::

   > [!NOTE]
   > このシナリオでは、プロジェクト名は **MyTeamsApp1** です。

Visual Studio 用 Teams ツールキットでは、次の関数を実行できます。

|関数  |説明  |
|---------|---------|
|Teams プロジェクトを作成する     |Visual Studio で Teams テンプレートを使用して Teams プロジェクトを作成する         |
|Teams アプリの依存関係を準備する     |ローカル デバッグを実行する前に、この手順を実行します。これにより、ローカル デバッグの依存関係を設定し、Teams プラットフォームに Teams アプリを登録するのに役立ちます。 Microsoft 365 アカウントが必要です。 詳細については、「[Visual Studio を使用して Teams アプリをローカルでデバッグする](debug-teams-app-visual-studio.md)」を参照してください。         |
|マニフェスト ファイルを開く     |Teams マニフェスト ファイルを開くには、パラメーターにカーソルを合わせて値をプレビューします。 詳細については、「[Visual Studio を使用して Teams アプリ マニフェストを編集する](VS-TeamsFx-preview-and-customize-app-manifest.md)」を参照してください。         |
|Teams 開発者ポータルでマニフェストを更新する     |マニフェスト ファイルを更新した後でなければ、プロジェクト全体を再度展開することなくマニフェスト ファイルを Azure に再展開することはできません。 このコマンドを使用して、変更をリモートに更新します。 詳細については、「[Visual Studio を使用して Teams アプリ マニフェストを編集する](VS-TeamsFx-preview-and-customize-app-manifest.md)」を参照してください。       |
|クラウドへのプロビジョニング     |このオプションは、Teams アプリをホストする Azure リソースを作成するのに役立ちます。 詳細については、「[Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)」を参照してください。        |
|クラウドに展開する     |このオプションを使用すると、"クラウドへのプロビジョニング" を行ったときに作成された Azure リソースにコードをコピーできます。 詳細については、「[Visual Studio を使用して Teams アプリをクラウドに展開する](deploy-teams-app.md)」を参照してください。        |
|Teams でプレビュー     |このオプションを選択すると、Teams Web クライアントが起動し、ブラウザーで Teams アプリをプレビューできます。         |
|Zip アプリ パッケージ     |このオプションでは、プロジェクトの下の `Build` フォルダーに Teams アプリ パッケージを生成します。 パッケージを Teams クライアントにアップロードし、Teams アプリを実行できます。         |

Visual Studio Code 用 Teams ツールキットとは異なり、Visual Studio 用 Teams ツールキットでは、次の操作はまだサポートされていません。ただし、今後の製品ロードマップにおいて計画されています。

* Teams アプリに Teams 機能をさらに追加します。
* Teams アプリに Azure リソースをさらに追加する
* Teams アプリにシングル サインオンを追加します。
* Teams アプリに API 接続を追加します。
* Azure AD マニフェストをカスタマイズします。
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

## <a name="see-also"></a>関連項目

* [Visual Studio で新しい Teams アプリを作成する](create-new-teams-app-for-Visual-Studio.md)
* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy-teams-app.md)
