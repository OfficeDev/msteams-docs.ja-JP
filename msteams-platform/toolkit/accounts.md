---
title: アプリをビルドするためのアカウントTeamsする
author: zyxiaoyuer
description: アプリをビルドするためのアカウントTeamsする
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 6a215922ff4b89c4afdce187be9b03479e6a54e6
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2021
ms.locfileid: "61228046"
---
# <a name="prepare-accounts-to-build-teams-apps"></a>アプリをビルドするためのアカウントTeamsする

アプリを開発Teams、有効なサブスクリプションMicrosoft 365少なくとも 1 つのアカウントが必要です。 Azure でバックエンド リソースをホストする場合は、Azure アカウントも必要です。 Azure アカウントは、既存のアプリケーションが他のクラウド プロバイダーでホストされ、既存のアプリケーションを新しいプラットフォームに統合Teamsです。

## <a name="microsoft-365-account"></a>Microsoft 365アカウント

有効なサブスクリプションを持つ既存Microsoft 365アカウントがない場合は、開発者プログラムに参加Microsoft 365[作成できます](https://developer.microsoft.com/microsoft-365/dev-program)。 Microsoft 365 開発者プログラムには、運用環境から独立した独自のサンドボックスの作成およびソリューションの開発に使用できる Microsoft 365 E5 開発者 サブスクリプションが含まれます。

## <a name="azure-account"></a>Azure アカウント

アプリ関連のリソースをホストするか、Azure 内のリソースにアクセスする場合は **、Azure** サブスクリプションが必要です。 開始する [前に無料アカウント](https://azure.microsoft.com/free/) を作成できます。

## <a name="join-microsoft-365-developer-program"></a>開発者Microsoft 365に参加する 

ユーザーアカウントをお持ちMicrosoft 365場合は、開発者プログラムのサブスクリプションMicrosoft 365[する必要](https://developer.microsoft.com/microsoft-365/dev-program)があります。 サブスクリプションは 90 日間無料で、開発アクティビティに使用している限り更新を続行します。 ユーザーがサブスクリプションをVisual Studio EnterpriseまたはProfessional場合、両方のプログラムに無料の開発者サブスクリプションMicrosoft 365[含まれます](https://aka.ms/MyVisualStudioBenefits)。 サブスクリプションがアクティブである限りVisual Studioアクティブです。 詳細については、「開発者向けサブスクリプション[のセットアップ」Microsoft 365参照してください](https://developer.microsoft.com/microsoft-365/dev-program)。

1. 開発者プログラムの[Microsoft 365に移動します](https://developer.microsoft.com/microsoft-365/dev-program)。
2. [今 **すぐ参加] を** 選択し、画面の指示に従います。
3. ようこそ画面で **、[E5 サブスクリプションの設定] を選択します**。
4. 管理者アカウントを設定します。 完了すると、次の画面が表示されます。

:::image type="content" source="./images/m365-developer-program.png" alt-text="microsoft m365 プログラムを示す図":::

## <a name="accounts-for-microsoft-365-developer-program"></a>開発者プログラムMicrosoft 365アカウント

次のいずれかの種類のアカウントを使用して、開発者プログラムにサインアップできます。

- **Microsoft アカウント** 

個人用に作成できます - Outlook、Messenger、OneDrive、MSN、Xbox Live、Microsoft 365 など、すべてのコンシューマー向け Microsoft 製品とクラウド サービスへのアクセスを提供します。 Outlook.com メールボックスにサインアップすると、Microsoft アカウントが自動的に作成されます。 作成された Microsoft アカウントを使用して、コンシューマー関連の Microsoft クラウド サービスまたは Azure にアクセスできます。

- **仕事用アカウント**

 管理者は、ビジネス上の使用に問題を生じ得る - Azure、Microsoft Intune、Microsoft 365 など、すべての小規模、中規模、およびエンタープライズのビジネス レベルの Microsoft クラウド サービスにアクセスできます。 組織としてこのいずれかのサービスにサインアップすると、組織を表すクラウド ベースのディレクトリが Azure Active Directory に自動的にプロビジョニングされます。

- **Visual Studio ID**

Visual Studio Professional サブスクリプションまたは Enterprise サブスクリプション用に作成できます。 Visual Studio ギャラリー内から開発者プログラムに参加して、Visual Studio サブスクライバーとして完全なメリットを得る場合は、このオプションを使用することをお勧めします。

## <a name="teams-customer-app-uploading-sideloading-permission-check"></a>Teamsアプリのアップロード (サイドローディングのアクセス許可) チェック

> [!IMPORTANT]
> 開発中は、アプリを配布せずにアプリをTeamsする必要があります。 これはサイドローディング **と呼ばれる.**

ユーザーアカウントを持っている場合は、TeamsアプリをサイドロードできるTeams。

1. クライアントで、Teamsバーの **[アプリ]** を選択します。
2. [アプリ **の管理] を選択します**。
3. イメージに示すように、カスタム アプリアップロード **オプションが表示** されるかどうかを確認します。

:::image type="content" source="./images/sideload-check.png" alt-text="カスタム アプリのアップロードを示す図":::

カスタム アプリ **オプションにアップロード** 表示できない場合は、サイドローディングのアクセス許可が付与できないことを示します。 サイドローディングのアクセス許可がない場合は、ローカル/リモート デバッグを実行することはできません。 そのため、アプリのデバッグを行う前に、アカウントのサイドローディング権限を取得することがTeamsです。 テナントの管理者である場合は、テナント/組織のサイドローディング設定を開き、管理者ではない場合は、アクセス許可をテナント管理者に問い合わせください。

## <a name="enable-custom-app-uploading-sideloading--for-your-organization"></a>組織のカスタム アプリアップロード (サイドローディング) を有効にする

> [!IMPORTANT]
> 開発者テナントのカスタム アプリのアップロードまたはサイドローディングを有効にするには、テナントの管理者である必要があります。

1. 管理者資格情報を[使用Microsoft 365 管理センター](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)にサインインします。

2. [**すべての** > **Teams の表示**]を選択します。

:::image type="content" source="./images/admin-center-teams.png" alt-text="管理センターのTeams図":::

> [!NOTE]
> このオプション **を表示するには、最大で 24** **Teams** かかる場合があります。 カスタム アプリ[をテストおよび検証Teams環境](/microsoftteams/upload-custom-apps)にアップロードできます。

3. [アプリの **セットアップ Teams**  >  **グローバル] に**  >  **移動します**。

:::image type="content" source="./images/teams-setup-policy.png" alt-text="アプリケーションのセットアップ ポリシーを示すTeams":::

4. カスタム アップロードを On の位置に **切り替** える。

:::image type="content" source="./images/turn-on-sideload.png" alt-text="サイドロードを有効にする図":::

5. **[保存]** を選択します。 テスト テナントは、カスタム アプリのサイドローディングを許可できます。

:::image type="content" source="./images/save-sideload.png" alt-text="保存オプションを示す図":::

> [!Note]
> サイドローディングがアクティブになるには、最大 24 時間かかる場合があります。 その間、[テナントのアップロード]を使用してアプリをテストできます。 アプリのパッケージ .zipをアップロードするには、「カスタム アプリのアップロード [」を参照してください](/microsoftteams/teams-app-setup-policies)。

詳細については、「カスタム アプリ[ポリシーと](/microsoftteams/teams-custom-app-policies-and-settings)設定を管理する」を参照し、Teams でアプリセットアップ ポリシー[を](/microsoftteams/teams-app-setup-policies)管理Teams。

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [新しいプロジェクトTeamsする](create-new-project.md)

> [!div class="nextstepaction"]
> [クラウド リソースのプロビジョニング](provision.md)
