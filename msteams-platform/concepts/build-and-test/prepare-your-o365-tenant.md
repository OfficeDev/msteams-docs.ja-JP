---
title: Microsoft 365 テナントを準備する
description: Microsoft 365 の Teams の概要
ms.topic: how-to
ms.localizationpriority: medium
keywords: Microsoft 365 テナントTeams のアップロードの構成
ms.openlocfilehash: 83d45d567c11ff26b5c788371cd4a676f9c3ca2c
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156152"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Microsoft 365 テナントを準備する

Microsoft 365購読者は、次のいずれかの計画Microsoft Teamsアプリを開発できます。

* 基本
* 標準
* Enterprise E1、E3、E5
* 開発者
* 学歴, Education Plus, and Education E5

> [!NOTE]
> * サブスクリプションの詳細については、「Microsoft 365プラン」を[参照してください](https://products.office.com/business/compare-more-office-365-for-business-plans)。
> * Teamsは、退職前に E4 を購読しているお客様にも利用[できます](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)。

## <a name="create-your-development-environment"></a>開発環境の作成

ユーザーアカウントをお持ちMicrosoft 365場合は、開発者プログラムのサブスクリプションにMicrosoft 365[必要](https://developer.microsoft.com/microsoft-365/dev-program)があります。 サブスクリプションは 90 日間無料で、開発アクティビティに使用している限り更新を続行します。 ユーザーがサブスクリプションをVisual Studio EnterpriseまたはProfessional場合、両方のプログラムに無料の開発者サブスクリプションMicrosoft 365[含まれます](https://aka.ms/MyVisualStudioBenefits)。 サブスクリプションがアクティブである限りVisual Studioアクティブです。 詳細については、「開発者向けサブスクリプション[のセットアップ」Microsoft 365参照してください](/office/developer-program/office-365-developer-program-get-started)。

## <a name="enable-teams-for-your-organization"></a>組織Teamsを有効にする

組織のTeamsを有効にする、および詳細については、「組織のTeams[を有効にする」を参照してください](/microsoftteams/enable-features-office-365)。

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>カスタム Teams アプリを有効にして、カスタム アプリのアップロードを有効にする

**開発者テナントのカスタム アプリのアップロードまたはサイドローディングを有効にする**

1. 管理者資格情報を[使用Microsoft 365 管理センター](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)にサインインします。

2. [**すべての** > **Teams の表示**]を選択します。

    ![管理センター メニュー](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > このオプションを表示するには、最大で 24 **Teams** かかる場合があります。 カスタム アプリ[をテストおよび検証Teams環境](/microsoftteams/upload-custom-apps#validate)にアップロードできます。

3. [アプリの **セットアップ Teams**  >  **グローバル] に**  >  **移動します**。

   ![サイドロード ビューを有効にする](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. カスタム **アップロードを On** の位置に **切り替** える。

5. **[保存]** を選択します。 テスト テナントは、カスタム アプリのサイドローディングを許可できます。

    > [!Note]
    > サイドローディングがアクティブになるには、最大 24 時間かかる場合があります。 暫定的には、アップロードを **使用してアプリ \<your tenant>** をテストできます。 アプリのパッケージ .zipをアップロードするには、「カスタム アプリのアップロード [」を参照してください](/microsoftteams/upload-custom-apps#upload)。

    ![アップロードアプリ ビュー](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

これらの設定の操作方法の詳細については、「Teams[](/microsoftteams/teams-custom-app-policies-and-settings)のカスタム アプリ ポリシーと設定を管理する」および「Teams でアプリセットアップ ポリシー[を管理する」を参照してください](/microsoftteams/teams-app-setup-policies)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"] 
> [テスト セットアップの選択](~/concepts/build-and-test/debug.md)

