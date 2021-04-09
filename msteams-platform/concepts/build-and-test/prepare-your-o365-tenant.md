---
title: Microsoft 365 テナントを準備する
description: Microsoft 365 の Teams の概要
ms.topic: how-to
keywords: Microsoft 365 テナントTeams のアップロードの構成
ms.openlocfilehash: aa7f994744f8b1c62aa32122a5006cfa0f22d391
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634757"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Microsoft 365 テナントを準備する

Microsoft 365 サブスクライバーは、次のいずれかの計画で Microsoft Teams 用のアプリを開発できます。

* 基本
* 標準
* Enterprise E1、E3、E5
* 開発者
* 学歴, Education Plus, and Education E5

> [!NOTE]
> Microsoft 365 サブスクリプションの詳細については、「プラン」を [参照してください](https://products.office.com/business/compare-more-office-365-for-business-plans)。
> 
> Microsoft Teams は、退職前に E4 を購読しているお客様にも利用 [できます](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)。

## <a name="create-your-development-environment"></a>開発環境の作成

Microsoft 365 アカウントをお持ちではない場合は [、Microsoft 365 Developer Program サブスクリプションにサインアップする必要](https://developer.microsoft.com/microsoft-365/dev-program) があります。 サブスクリプションは 90 日間無料で、開発アクティビティに使用している限り更新を続行します。 エンタープライズ サブスクリプションまたはプロフェッショナル サブスクリプションVisual Studio、両方のプログラムに無料の Microsoft 365 開発者サブスクリプションが [含まれます](https://aka.ms/MyVisualStudioBenefits)。 サブスクリプションがアクティブである限り、Visual Studioアクティブです。 詳細については [、「Microsoft 365 開発者サブスクリプションをセットアップする」を参照してください](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。

## <a name="enable-microsoft-teams-for-your-organization"></a>組織用に Microsoft Teams を有効にする

組織で Microsoft Teams を有効にし、組織で Teams を有効にするための詳細なガイダンス [を確認します](/microsoftteams/enable-features-office-365)。

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>カスタム Teams アプリを有効にして、カスタム アプリのアップロードを有効にする

**開発者テナントのカスタム アプリのアップロードまたはサイドローディングを有効にする**

1. 管理者資格情報を [使用して Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) 管理センターにサインインします。

2. [**すべての** > **Teams の表示**]を選択します。

    ![管理センター メニューの画像](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > Teams オプションが表示されるには、最大で 24 **時間かかる** 場合があります。 カスタム アプリ [を Teams 環境にアップロードして](/microsoftteams/upload-custom-apps#validate) 、その時間のテストと検証を行えます。

3. **[Teams アプリのセットアップ**  >  **ポリシー] グローバル に**  >  **移動します**。

   ![sideload ビューを有効にする](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. **カスタム アプリのアップロード** を切り替え **オン** の位置にします。

5. **[保存]** を選択します。
   テスト テナントは、カスタム アプリのサイドローディングを許可できます。

    > [!Note]
    > サイドローディングがアクティブになるには、最大 24 時間かかる場合があります。 その間、[**アップロード\<your tenant>**] を使用して、アプリをテストできます。

    ![updload アプリ ビュー](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

これらの設定の操作方法の詳細については、「Microsoft Teams でのカスタム アプリ ポリシーと設定の管理」および [「Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) でのアプリセットアップ ポリシーの管理」を [参照してください](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"] 
> [テストセットアップの選択](~/concepts/build-and-test/debug.md)
> 


