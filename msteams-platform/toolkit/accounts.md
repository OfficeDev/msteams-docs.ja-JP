---
title: Teams アプリを構築するためのアカウントを準備する
author: zyxiaoyuer
description: Teams アプリを構築するためのアカウントを準備する
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: a7b830ef0aba9b7e46a10d67de128aa9f3076eeb
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2022
ms.locfileid: "66122916"
---
# <a name="prepare-accounts-to-build-teams-apps"></a>Teams アプリを構築するためのアカウントを準備する

Teams アプリを作成してアップロードするには、次のアカウントを準備する必要があります:

* [有効なサブスクリプションのある Microsoft 365 アカウント](accounts.md#microsoft-365-account)
* [Azure でバックエンド リソースをホストする Azure アカウント](accounts.md#azure-account-to-host-backend-resources)

## <a name="microsoft-365-account"></a>Microsoft 365 アカウント

Microsoft 365 アカウントを作成するには、Microsoft 365 開発者プログラム サブスクリプションにサインアップします。 サブスクリプションは 90 日間無料で、開発アクティビティに使用している限り、引き続き更新されます。

Visual Studio Enterprise または Professional サブスクリプションをお持ちの場合は、両方のプログラムに無料の Microsoft 365 [開発者サブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。 Visual Studio サブスクリプションがアクティブである限り、アクティブです。 詳細については、「[Microsoft 365 開発者サブスクリプション](https://developer.microsoft.com/microsoft-365/dev-program)」を参照してください。

### <a name="microsoft-365-developer-program"></a>Microsoft 365 開発者プログラム

無料の Teams 開発者アカウントを取得するには、Microsoft 365 開発者プログラムに参加し、次の手順に従います:

1. [Microsoft 365 開発者プログラム](https://developer.microsoft.com/microsoft-365/dev-program)に移動します。
2. [**今すぐ参加**] を選択します。
3. [**E5 サブスクリプションのセットアップ**] を選択します。
4. 管理者アカウントを設定します。

   サブスクリプションが完了すると、次の図が表示されます。

    :::image type="content" source="./images/m365-developer-program.png" alt-text="Microsoft 365プログラムを示す図":::

### <a name="microsoft-365-developer-account-types"></a>Microsoft 365 開発者アカウントの種類

次のいずれかの種類のアカウントを使用して、開発者プログラムにサインアップできます。

* **個人使用の Microsoft アカウント**

    このアカウントを使用すると、Outlook、Messenger、OneDrive、MSN、Xbox Live、Microsoft 365 などの Microsoft 製品とクラウド サービスにアクセスできます。 Outlook.com メールボックスにサインアップして、コンシューマー関連の Microsoft クラウド サービスまたは Azure にアクセスするために使用できる Microsoft アカウントを作成できます。

* **ビジネス向け Microsoft ワーク アカウント**

     このアカウントを使用すると、Azure、Microsoft Intune、Microsoft 365 など、すべての小規模、中規模、エンタープライズのビジネス レベルの Microsoft クラウド サービスにアクセスできます。 組織としてこのいずれかのサービスにサインアップすると、組織を表すクラウド ベースのディレクトリが Azure AD に自動的にプロビジョニングされます。

* **Visual Studio ユーザー ID**

    Visual Studio Professional または Enterprise サブスクリプションのユーザー ID を使用して、Visual Studio ギャラリー内の開発者プログラムに参加し、Visual Studio サブスクライバーとして完全な利点を利用できます。

## <a name="azure-account-to-host-backend-resources"></a>バックエンド リソースをホストする Azure アカウント

既存のアプリケーションが他のクラウド プロバイダーでホストされていて、Teams プラットフォームで既存のアプリケーションを統合する場合、Azure アカウントは省略可能です。

**Visual Studio ID**

アプリケーション関連のリソースをホストする場合、または Azure 内のリソースにアクセスする場合は、開始する前に[無料のアカウントを作成](https://azure.microsoft.com/free/)できます。 または、別のクラウド プロバイダーを使用してバックエンド リソースをホストするか、パブリック ドメインから使用できる場合は独自のサーバーでホストするかを選択できます。

## <a name="upload-custom-app"></a>カスタム アプリをアップロードする

> [!IMPORTANT]
> アプリを作成したら、アプリを配布せずに Teams に読み込む必要があります。このプロセスは **サイドローディング** と呼ばれます。

   Visual Studio Code または Teams クライアントを使用して、サイドローディングアクセス許可が有効になっているかどうかを確認できます。

* **Visual Studio Code を使用してサイドローディングアクセス許可を確認する**

    1. **Visual Studio Code** を開きます。
    2. 左側のウィンドウから [**Teams Toolkit**] を選択します。 オプションが表示できない場合は、Teams Toolkit 拡張機能がインストールされていることを確認します。
    3. [**アカウント**] 選択し、Microsoft 365 アカウントにログインします。
    4. 次の図に示すように、**サイドローディングが有効** なオプションを表示できるかどうかを確認します。

       :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="サイドローディングを有効にする" border="true":::

* **Teams クライアントを使用してサイドローディングのアクセス許可を確認する**

    1. **Microsoft Teams** を開きます。
    2. 左側のパネルで [**アプリ**] を選択します。
    3. [**アプリ の発行**] を選択します。

       :::image type="content" source="../assets/images/teams-toolkit-v2/publish2.png" alt-text="アプリを発行します。" border="true":::

    4. 次の図に示すように、[**カスタム アプリのアップロード**] オプションが表示されるかどうかを確認します。

       :::image type="content" source="../assets/images/teams-toolkit-v2/upload2.png" alt-text="カスタム アプリをアップロード" border="true":::

        **[カスタム アプリのアップロード]** オプションを表示できない場合は、サイドローディングに必要なアクセス許可がないということです。

        * テナント管理者の場合は、Teams 管理センターでテナントまたは組織のサイドローディング設定を有効にします。
        * テナント管理者でない場合は、テナント管理者に問い合わせ、サイドローディングを有効にする必要があります。

* **管理センターを使用してカスタム アプリをアップロードする**

  > [!IMPORTANT]
  > 開発者テナントのカスタム アプリのアップロードまたはサイドローディングを有効にするには、テナントの管理者である必要があります。

  カスタム アプリをアップロードするには、次の手順を実行します:

  1. 管理者の資格情報で [Microsoft 365 管理センター](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)にサインインします。

  2. [**すべての** > **Teams の表示**]を選択します。

     :::image type="content" source="../assets/images/teams-toolkit-v2/5.png" alt-text="すべて表示" border="true":::

     > [!Note]
     > **Teams** オプションが表示されるまで、**最大 24 時間** かかる場合があります。 テストと検証のために、[カスタム アプリを Teams 環境にアップロード](/microsoftteams/upload-custom-apps)することができます。

  3. [**Teams アプリ**]  >  [**セット アップ ポリシー**] に移動します。

     :::image type="content" source="../assets/images/teams-toolkit-v2/3.png" alt-text="ポリシーの設定":::

  4. [**カスタム アプリのアップロード**] を "**オン**" に切り替えます。

     :::image type="content" source="../assets/images/teams-toolkit-v2/4.png" alt-text="切り替え":::

  5. **[保存]** を選択します。

     > [!Note]
     > データが反映されるまでに最大 24 時間かかることがあります。 その間、[**テナントのアップロード**] を使用してアプリをテストできます。 アプリの .zip パッケージ ファイルをアップロードするには、「[カスタム アプリのアップロード](/microsoftteams/teams-app-setup-policies)」を参照してください。

詳細については、「[Teams でカスタム アプリ ポリシーと設定を管理する](/microsoftteams/teams-custom-app-policies-and-settings)」および「[Teams でアプリのセットアップ ポリシーを管理する](/microsoftteams/teams-app-setup-policies)」を参照してください。

## <a name="see-also"></a>関連項目

* [Teams Toolkit を使用して新しい Teams アプリを作成する](create-new-project.md)
* [クラウド リソースをプロビジョニングする](provision.md)
* [Teams アプリをクラウドに展開する](deploy.md)
* [Teams アプリの発行](../concepts/deploy-and-publish/appsource/publish.md)
* [複数の環境を管理する](TeamsFx-multi-env.md)
