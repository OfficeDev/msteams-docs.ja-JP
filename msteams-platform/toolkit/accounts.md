---
title: アプリをビルドするためのアカウントTeamsする
author: zyxiaoyuer
description: アプリをビルドするためのアカウントTeamsする
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ff46e951122a74860e4518634e274ec4afdb1d21
ms.sourcegitcommit: c66da76fb766df6270095265e1da8c49a3afd195
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2022
ms.locfileid: "62435685"
---
# <a name="prepare-accounts-to-build-teams-apps"></a>アプリをビルドするためのアカウントTeamsする

アプリをTeamsするには、有効なサブスクリプションを持つアカウントMicrosoft 365少なくとも 1 つ必要です。 Azure でバックエンド リソースをホストする場合は、Azure アカウントが必要です。 Azure アカウントは、既存のアプリケーションが他のクラウド プロバイダーでホストされ、既存のアプリケーションを新しいプラットフォームに統合Teamsです。

## <a name="microsoft-365-account"></a>Microsoft 365 アカウント

有効なサブスクリプションを持つ既存Microsoft 365アカウントがない場合は、開発者プログラムに参加Microsoft 365[作成できます](https://developer.microsoft.com/microsoft-365/dev-program)。 開発者Microsoft 365には、Microsoft 365 E5サンドボックスを作成し、実稼働環境に依存しないソリューションを開発するために使用できる、開発者向けサブスクリプションが含まれています。

## <a name="azure-account"></a>Azure アカウント

アプリ関連のリソースをホストする場合、または Azure 内のリソースにアクセスする場合は、Azure サブスクリプションが必要です。 開始する [前に無料アカウント](https://azure.microsoft.com/free/) を作成できます。

## <a name="join-microsoft-365-developer-program"></a>開発者Microsoft 365に参加する 

ユーザーアカウントをお持ちMicrosoft 365場合は、開発者プログラムのサブスクリプションMicrosoft 365[する必要](https://developer.microsoft.com/microsoft-365/dev-program)があります。 サブスクリプションは 90 日間無料で、開発アクティビティに使用している限り更新を続行します。 ユーザーがサブスクリプションをVisual Studio EnterpriseまたはProfessional場合、両方のプログラムに無料の開発者サブスクリプションMicrosoft 365[含まれます](https://aka.ms/MyVisualStudioBenefits)。 サブスクリプションがアクティブである限りVisual Studioアクティブです。 詳細については、「開発者向けサブスクリプション[のMicrosoft 365参照してください](https://developer.microsoft.com/microsoft-365/dev-program)。

1. 開発者プログラムの[Microsoft 365に移動します](https://developer.microsoft.com/microsoft-365/dev-program)。
2. [今 **すぐ参加] を選択します**。
3. [ **E5 サブスクリプションの設定] を選択します**。
4. 管理者アカウントを設定します。 完了すると、次の画面が表示されます。

:::image type="content" source="./images/m365-developer-program.png" alt-text="プログラムを示Microsoft 365図":::

## <a name="accounts-for-microsoft-365-developer-program"></a>開発者プログラムMicrosoft 365アカウント

次のいずれかの種類のアカウントを使用して、開発者プログラムにサインアップできます。

- **個人用の Microsoft アカウント** 

  Outlook、Messenger、OneDrive、MSN、Xbox Live、クラウド サービスなど、すべてのコンシューマー向け Microsoft 製品とクラウド サービスMicrosoft 365。 Outlook.com メールボックスにサインアップすると、Microsoft アカウントが自動的に作成されます。 作成された Microsoft アカウントを使用して、コンシューマー関連の Microsoft クラウド サービスまたは Azure にアクセスできます。

- **業務用の仕事用アカウント**

  Azure、azure、Microsoft Intune、またはエンタープライズ のすべてのビジネス レベルの Microsoft クラウド サービスにアクセスMicrosoft 365。 組織としてこのいずれかのサービスにサインアップすると、組織を表すクラウド ベースのディレクトリが Azure Active Directory に自動的にプロビジョニングされます。

- **Visual Studio ID**

  Visual Studio Professional サブスクリプションまたは Enterprise サブスクリプション用に作成できます。 Visual Studio ギャラリー内から開発者プログラムに参加して、Visual Studio サブスクライバーとして完全なメリットを得る場合は、このオプションを使用することをお勧めします。

## <a name="teams-customer-app-upload-or-sideload-permission"></a>Teamsアプリのアップロードまたはサイドロードのアクセス許可

> [!IMPORTANT]
> 開発中は、アプリを配布せずにアプリをTeamsする必要があります。 これはサイドローディング **と呼ばれる。**

次の一覧では、サイドローディング アプリのアクセス許可が有効かどうかを確認する手順を示します。 2 つの異なる方法は次のとおりです。

* **Microsoft Visual studio コードを使用するには**

    1. [ファイル **Visual Studio Code] を開きます**。
    1. 左側 **のTeams Toolkit** を選択します。
    1. [**アカウント] を** 選択し、自分のアカウントMicrosoft 365します。
    1. イメージに示すように、サイドローディングが有効 **になっている** オプションが表示されるかどうかを確認します。

       :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="サイドローディングを有効にする":::

* **アカウントをTeamsするには**

    1. [ファイル **Microsoft Teams] を開きます**。
    2. 左側の **バーで [** アプリ] を選択します。
    3. [アプリ **の発行] を選択します**。

       :::image type="content" source="../assets/images/teams-toolkit-v2/publish.png" alt-text="アプリを発行します。":::

    4. イメージに示すように、カスタム アプリアップロード **オプションが表示** されるかどうかを確認します。

       :::image type="content" source="../assets/images/teams-toolkit-v2/upload.png" alt-text="アップロードアプリを作成する":::

カスタム アプリ オプション **にアップロード表示** できない場合は、サイドローディングのアクセス許可を持たなかった場合に表示されます。 サイドローディングのアクセス許可がない場合は、ローカルまたはリモートのデバッグを実行することはできません。 そのため、アプリのデバッグを行う前に、アカウントのサイドローディング権限を取得することがTeamsです。 テナントの管理者である場合は、テナントまたは組織のサイドローディング設定を開きます。 管理者ではない場合は、テナント管理者にアクセス許可を問い合わせください。

## <a name="enable-custom-app-uploading-for-your-organization"></a>組織のカスタム アプリのアップロードを有効にする

> [!IMPORTANT]
> 開発者テナントのカスタム アプリのアップロードまたはサイドローディングを有効にするには、テナントの管理者である必要があります。

1. 管理者資格情報を[使用Microsoft 365 管理センター](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)サインインします。

2. [**すべての** > **Teams の表示**]を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/5.png" alt-text="すべて表示する":::

> [!NOTE]
> このオプション **が表示される場合、Teams 24** **時間かかる** 場合があります。 カスタム アプリ[をテストおよび検証Teams環境](/microsoftteams/upload-custom-apps)にアップロードできます。

3. [アプリ **のTeams** >  **Setup PoliciesGlobal** > **] に移動します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/3.png" alt-text="olicies を設定する":::

4. カスタム アップロードを On の位置に **切り替** える。

   :::image type="content" source="../assets/images/teams-toolkit-v2/4.png" alt-text="トグル":::

5. **[保存]** を選択します。 

> [!Note]
> サイドローディングがアクティブになるには、最大 24 時間かかる場合があります。 その間、テナントの **アップロードを使用して** アプリをテストできます。 アプリのパッケージ .zipをアップロードするには、「カスタム アプリの [アップロード」を参照してください](/microsoftteams/teams-app-setup-policies)。

詳細については、「カスタム アプリ ポリシーと設定[を](/microsoftteams/teams-custom-app-policies-and-settings)管理する」を参照し、Teamsでアプリセットアップ ポリシー[を](/microsoftteams/teams-app-setup-policies)管理Teams。

## <a name="see-also"></a>関連項目

* [新しいプロジェクトTeamsする](create-new-project.md)
* [クラウド リソースをプロビジョニングする](provision.md)
