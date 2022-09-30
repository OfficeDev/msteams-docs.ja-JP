---
title: Microsoft 365 テナントを準備する
description: このモジュールでは、Microsoft 365 で Teams を使用し、開発環境を作成する方法について説明します
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: c5ebc7d36f73978e1cd954c7be8d7ac3595ba68e
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243585"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Microsoft 365 テナントを準備する

Microsoft 365 のサブスクライバーは、次のいずれかのプランを使用して、Microsoft Teams のアプリを開発できます。

* 基本
* 標準
* Enterprise E1、E3、E5
* 開発者
* 学歴, Education Plus, and Education E5

> [!NOTE]
>
> * Microsoft 365 サブスクリプションの詳細については、「[プラン](https://products.office.com/business/compare-more-office-365-for-business-plans)」を参照してください。
> * Teams は、[廃止](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)前に E4 以前を購読していたお客様も利用できます。

## <a name="create-your-development-environment"></a>開発環境を作成する

現在 Microsoft 365 アカウントを使用していない場合は、[Microsoft 365 開発者プログラム](https://developer.microsoft.com/microsoft-365/dev-program) サブスクリプションにサインアップする必要があります。 サブスクリプションは 90 日間無料で、開発アクティビティに使用している限り、引き続き更新されます。 Visual Studio Enterprise または Professional サブスクリプションをお持ちの場合は、両方のプログラムに無料の Microsoft 365 [開発者サブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。 Visual Studio サブスクリプションがアクティブである限り、アクティブです。 詳細については、[Microsoft 365 開発者サブスクリプションを設定する](/office/developer-program/office-365-developer-program-get-started)をご覧ください。

## <a name="enable-teams-for-your-organization"></a>組織用に Teams を有効にする

組織用に Teams を有効し、詳細については、「[組織用に Teams を有効にする](/microsoftteams/enable-features-office-365)」を参照してください。

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>カスタム Teams アプリを有効にして、カスタム アプリのアップロードを有効にする

開発者テナントのカスタム アプリのアップロードまたはサイドローディングを有効にするには:

1. 管理者の資格情報で [Microsoft 365 管理センター](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)にサインインします。

2. [**すべての** > **Teams の表示**]を選択します。

    ![管理センター メニュー](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > Teams オプションが表示されるまで、**最大 24 時間** かかる場合があります。 その時点でのテストと検証のために、[カスタム アプリを Teams 環境にアップロード](/microsoftteams/upload-custom-apps#validate)することができます。

3. **Teams アプリ** > **のセットアップ ポリシー** > **グローバル** に移動します。

   ![サイドロード ビューを有効にする](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. [**カスタム アプリをアップロード**] を [**オン**] に切り替えます。

5. **[保存]** を選択します。 テスト テナントで、カスタムアプリのサイドローディングができるようになりました。

    > [!Note]
    > サイドローディングがアクティブになるまでに最大 24 時間かかる場合があります。 その間、[**\<your tenant> にアップロード**] を使用して、アプリをテストできます。 アプリの .zip パッケージ ファイルをアップロードするには、「[カスタム アプリのアップロード](/microsoftteams/upload-custom-apps#upload)」を参照してください。

    ![アップロード アプリ ビュー](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

これらの設定がどのように機能するかの詳細については、「[Teams のカスタム アプリ ポリシーと設定の管理](/microsoftteams/teams-custom-app-policies-and-settings)」 および「[Teams のアプリ セットアップ ポリシーの管理](/microsoftteams/teams-app-setup-policies)」を参照してください。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [テスト セットアップの選択](~/concepts/build-and-test/debug.md)

## <a name="see-also"></a>関連項目

* [Microsoft 365 テスト テナントにテスト データを追加する](~/concepts/build-and-test/test-data.md)
* [Microsoft 365 Multi-Geo](/microsoft-365/enterprise/microsoft-365-multi-geo?view=o365-worldwide&preserve-view=true)
