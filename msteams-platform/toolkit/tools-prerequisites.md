---
title: Visual Studio Code を使用して Teams アプリを作成するための前提条件
author: zyxiaoyuer
description: このモジュールでは、ツールと SDK に必要な前提条件について説明します
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: 412b7bfedb6ba39f1d38f42aac56cc793ea385b1
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617151"
---
# <a name="prerequisites-for-creating-your-teams-app"></a>Teams アプリを作成するための前提条件

Teams アプリの作成を開始する前に、次の前提条件が満たされていることを確認します。

* [Teams アプリを構築するための基本的な要件](#basic-requirements-to-build-your-teams-app)
* [アカウントを準備して Teams アプリを構築する](#accounts-to-build-your-teams-app)
* [サイドローディングアクセス許可](#sideloading-permission)

## <a name="basic-requirements-to-build-your-teams-app"></a>Teams アプリを構築するための基本的な要件

Teams アプリのビルドを開始する前に、次の要件が満たされていることを確認します。

| &nbsp; | 基本的な要件 | 使用する場合| 環境の種類の場合|
   | --- | --- | --- |
   | **必須** | &nbsp; | &nbsp; | &nbsp; |
   | &nbsp; | Teams ツールキット| アプリのプロジェクト スキャフォールディングを作成する Microsoft Visual Studio Code 拡張機能。 最新バージョンを使用します。 | JavaScript と SPFx|
   | &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | チャット、会議、通話のためのアプリを通じて作業するすべてのユーザーと共同作業を行います。すべて 1 か所で行うことができます。| JavaScript と SPFx|
   | &nbsp; | [Node.js](https://nodejs.org/en/download/) | バックエンド JavaScript ランタイム環境。 最新の v16 LTS リリースを使用します。| JavaScript と SPFx|
   | &nbsp; |[ノード パッケージ マネージャー (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx) | Node.jsアプリケーションと ASP.NET Core アプリケーションの両方で使用するパッケージをインストールして管理します。| JavaScript と SPFx|
   | &nbsp; | [Microsoft&nbsp;Edge](https://www.microsoft.com/edge) (推奨) または [Google Chrome](https://www.google.com/chrome/) | 開発者ツールを備えたブラウザー。 | JavaScript と SPFx|
   | &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | JavaScript、TypeScript、または SharePoint Framework (SPFx) ビルド環境。 バージョン 1.55 以降を使用してください。 | JavaScript と SPFx|
   | **Optional** | &nbsp; | &nbsp; | &nbsp; |
   | &nbsp; | [Azure Tools for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack) および [Azure CLI](/cli/azure/install-azure-cli) | 保存されたデータにアクセスするか、Azure で Teams アプリのクラウドベースのバックエンドをデプロイします。 | JavaScript|
   | &nbsp; | [React Developer Tools for Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) または [React Developer Tools for Microsoft&nbsp;Edge](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil) | オープン ソース React JavaScript ライブラリのブラウザー DevTools 拡張機能。 | JavaScript|
   | &nbsp; | [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) | Microsoft Graph データからクエリを実行できるブラウザー ベースのツール。 | JavaScript と SPFx|
   | &nbsp; | [Teams の開発者ポータル](https://dev.teams.microsoft.com/) | Teams アプリを構成、管理、組織や Teams ストアなどに配布するための Web ベースのポータル。| JavaScript と SPFx|

   > [!NOTE]
   >
   > * このドキュメントは、Teams Toolkit バージョン 4.0.0 および Nodejs バージョン 16 でテストされています。
   > * Microsoft Graph サービスの詳細については、Microsoft Graph エクスプローラーをブックマークします。 このブラウザー ベースのツールを使用すると、アプリの外部で Microsoft Graph にクエリを実行してアクセスできます。

## <a name="accounts-to-build-your-teams-app"></a>Teams アプリを構築するためのアカウント

Teams アプリのビルドを開始する前に、次のアカウントがあることを確認します。

| アカウント | 使用する場合| 環境の種類の場合|
| --- | --- |
|[有効なサブスクリプションのある Microsoft 365 アカウント](#microsoft-365-developer-program)|アプリの開発中に Teams 開発者アカウント。| JavaScript と SPFx|
|[Azure アカウント](accounts.md#azure-account-to-host-backend-resources)|Azure 上のバックエンド リソース。| JavaScript と SPFx|
|[SharePoint コレクション サイト管理者アカウント](#sharepoint-collection-site-administrator-account) |ホスティング用のデプロイ。| SPFx|

### <a name="microsoft-365-developer-program"></a>Microsoft 365 開発者プログラム

Microsoft 365 アカウントを作成するには、Microsoft 365 開発者プログラム サブスクリプションにサインアップします。 サブスクリプションは 90 日間無料で、開発アクティビティに使用している限り、引き続き更新されます。

Visual Studio Enterprise または Professional サブスクリプションをお持ちの場合は、両方のプログラムに無料の Microsoft 365 [開発者サブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。 Visual Studio サブスクリプションがアクティブである限り、アクティブです。 詳細については、「[Microsoft 365 開発者サブスクリプション](https://developer.microsoft.com/microsoft-365/dev-program)」を参照してください。

次のいずれかの種類のアカウントを使用して、開発者プログラムにサインアップできます。

* **個人使用の Microsoft アカウント**

  :::row:::

    :::column span="3":::

       このアカウントを使用すると、Outlook、Messenger、OneDrive、MSN、Xbox Live、Microsoft 365 などの Microsoft 製品とクラウド サービスにアクセスできます。 

       Outlook.com メールボックスにサインアップして、コンシューマー関連の Microsoft クラウド サービスまたは Azure にアクセスするために使用できる Microsoft アカウントを作成できます。

    :::column-end:::
    :::column span="1":::
             :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/personal-account-icon.png" alt-text="個人アカウント。":::
   :::column-end:::

  :::row-end:::

* **ビジネス向け Microsoft ワーク アカウント**

  :::row:::

    :::column span="3":::

       このアカウントでは、すべての小規模、中規模、エンタープライズのビジネス レベルの Microsoft クラウド サービスにアクセスできます。 サービスには、Azure、Microsoft Intune、または Microsoft 365 が含まれます。 

       組織としてこのいずれかのサービスにサインアップすると、組織を表すクラウド ベースのディレクトリが Azure AD に自動的にプロビジョニングされます。

    :::column-end:::
    :::column span="1":::
             :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/work-account-icon.png" alt-text="ワーク アカウント。":::
    :::column-end:::

  :::row-end:::

#### <a name="create-a-free-microsoft-365-developer-account"></a>無料の Microsoft 365 開発者アカウントを作成する

無料の Microsoft 365 開発者アカウントを作成するには、Microsoft 365 開発者プログラムに参加し、次のアカウントを実行します。

1. [Microsoft 365 開発者プログラム](https://developer.microsoft.com/microsoft-365/dev-program)に移動します。
1. [**今すぐ参加**] を選択します。
1. 管理者アカウントを設定します。

   サブスクリプションが完了すると、次の図が表示されます。

    :::image type="content" source="../assets/images/teams-toolkit-v2/m365-account.png" alt-text="M365 アカウント":::

### <a name="azure-account"></a>Azure アカウント

Visual Studio Code で Teams Toolkit を使用して Teams アプリまたは Teams アプリのバックエンド リソースをホストするには、Azure アカウントが必要です。 次のシナリオでは、Azure サブスクリプションが必要です。

* Azure 以外の別のクラウド プロバイダーに既に既存のアプリがあり、Teams プラットフォームでアプリを統合する場合は、Azure サブスクリプションが必要です。
* Azure サブスクリプションを選択して、別のクラウド プロバイダーを使用してバックエンド リソースをホストするか、パブリック ドメインから利用できる場合は独自のサーバーでホストできます。

> [!NOTE]
> 開始する前に [、無料アカウントを作成](https://azure.microsoft.com/free/) する必要があります。

### <a name="sharepoint-collection-site-administrator-account"></a>SharePoint コレクション サイト管理者アカウント

SPFx 環境を使用して Teams アプリを作成するときに、ホスト用の展開時に SharePoint コレクション サイト管理者アカウントが必要になります。 Microsoft 365 開発者プログラム テナントを使用している場合は、そのときに作成した管理者アカウントを使用することができます。

## <a name="sideloading-permission"></a>サイドローディングアクセス許可

アプリを作成したら、アプリを配布せずに Teams に読み込む必要があります。 このプロセスはサイドローディングと呼ばれます。 このオプションを表示するには、Microsoft 365 アカウントにサインインします。

Visual Studio Code または Teams クライアントを使用して、サイドローディングアクセス許可が有効になっているかどうかを確認できます。

<br>
<details>
<summary><b>Visual Studio Code を使用してサイドローディングアクセス許可を確認する</b></summary>

1. **Visual Studio Code** を開きます。
1. Teams Toolkit :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: ツール バーから Teams Toolkit アイコンを選択します。

   > [!NOTE]
   > このオプションが表示できない場合は、「 [Teams Toolkit をインストール](install-Teams-Toolkit.md) して Teams Toolkit 拡張機能を Visual Studio Code にインストールする」を参照してください。
1. [**ACCOUNTS**] **で [M365 に** サインイン] を選択し、Microsoft 365 アカウントにサインインします。

    :::image type="content" source="../assets/images/teams-toolkit-v2/accounts.png" alt-text="アカウントの詳細":::

1. 次の図に示すように、**サイドローディングが有効** なオプションを表示できるかどうかを確認します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="サイドローディングを有効にする":::

</details>
<br>
<details>
<summary><b>Teams クライアントを使用してサイドローディングのアクセス許可を確認する</b></summary>

1. Teams クライアントで、[アプリ] を選択 **します**。
1. [ **アプリの管理] を選択します**。
1. [ **アプリのアップロード] を選択します**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/upload-app.png" alt-text="アプリを発行します。":::

4. 次の図に示すように、[**カスタム アプリのアップロード**] オプションが表示されるかどうかを確認します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/upload-custom-app1.png" alt-text="カスタム アプリをアップロード":::

</details>

### <a name="enable-sideloading-using-admin-center"></a>管理センターを使用してサイドローディングを有効にする

[ **カスタム アプリのアップロード** ] オプションを表示できない場合は、サイドローディングに必要なアクセス許可がないことを示します。

* テナント管理者の場合は、Teams 管理センターでテナントまたは組織のサイドローディング設定を有効にします。
* テナント管理者でない場合は、テナント管理者に問い合わせ、サイドローディングを有効にする必要があります。

管理者権限がある場合は、次の手順に従って、管理センターを使用してカスタム アプリをアップロードします。

  1. 管理者の資格情報で [Microsoft 365 管理センター](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)にサインインします。

  1. Teams >アイコンを :::image type="icon" source="../assets/images/teams-toolkit-v2/showall icon.PNG"::: 選択 **します**。

       :::image type="content" source="../assets/images/teams-toolkit-v2/m365-admin-center.png" alt-text="Microsoft 365 管理センター":::

     > [!Note]
     > **Teams** オプションが表示されるまで、**最大 24 時間** かかる場合があります。 テストと検証のために、[カスタム アプリを Teams 環境にアップロード](/microsoftteams/upload-custom-apps)することができます。

  1. 管理者資格情報を使用して Microsoft Teams 管理センターにサインインします。
  1. **Teams アプリ** > の:::image type="icon" source="../assets/images/teams-toolkit-v2/showall icon.PNG":::**セットアップ ポリシー**>アイコンを選択します。

     :::image type="content" source="../assets/images/teams-toolkit-v2/m365-admin-center1.png" alt-text="Microsoft 365 管理 center1":::

  1. グローバルを選択 **する (組織全体の既定値)**

     :::image type="content" source="../assets/images/teams-toolkit-v2/select-manage-policies.png" alt-text="[ポリシーの管理] を選択する":::

  1. [**カスタム アプリのアップロード**] を "**オン**" に切り替えます。

     :::image type="content" source="../assets/images/teams-toolkit-v2/Upload-custom-apps.png" alt-text="カスタム アプリをアップロードする":::

  5. **[保存]** を選択します。

     > [!Note]
     > データが反映されるまでに最大 24 時間かかることがあります。 その間、[**テナントのアップロード**] を使用してアプリをテストできます。 アプリの .zip パッケージ ファイルをアップロードするには、「[カスタム アプリのアップロード](/microsoftteams/teams-app-setup-policies)」を参照してください。

     Visual Studio Code または Teams クライアントを使用してサイドローディングアクセス許可を確認する手順に記載されている手順[を使用してサイドローディングアクセス許可](#sideloading-permission)が付与されていることを確認します。

</details>

## <a name="see-also"></a>関連項目

* [Teams でカスタム アプリのポリシーと設定を管理する](/microsoftteams/teams-custom-app-policies-and-settings)
* [Teams でアプリのセットアップ ポリシーを管理する](/microsoftteams/teams-app-setup-policies)
* [カスタム アプリをアップロードする](/microsoftteams/teams-app-setup-policies)
* [Teams Toolkit を使用してクラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリをクラウドに展開する](deploy.md)
