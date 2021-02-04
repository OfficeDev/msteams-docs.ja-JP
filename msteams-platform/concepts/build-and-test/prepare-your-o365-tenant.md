---
title: Microsoft 365 テナントを準備する
description: Microsoft 365 の Teams の概要
ms.topic: how-to
keywords: Microsoft 365 テナントTeams のアップロードの構成
ms.openlocfilehash: 50765271b93edd380d1c23672289b618baf1d346
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093944"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Microsoft 365 テナントを準備する

Microsoft 365 のサブスクライバーである場合は、 次のいずれかの[プラン](https://products.office.com/business/compare-more-office-365-for-business-plans) を使用して、Microsoft Teams のアプリを開発できます。

* 基本
* 標準
* Enterprise E1、E3、E5
* 開発者
* 学歴, Education Plus, and Education E5

またMicrosoft Teamsは、 [廃止](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)前に E4 以前を購読していた客様も利用できます。

## <a name="just-need-a-development-environment"></a>開発環境が必要ですか?

現在 Microsoft 365 アカウントを使用していない場合は、 [Microsoft 365 開発者プログラム](https://developer.microsoft.com/microsoft-365/dev-program) サブスクリプションにサイン アップできます。 これは 90 日間 *無料* で開発活動に使用する限り継続的に更新されます。 Visual Studio *Enterprise* または *Professional* サブスクリプションをお持ちの場合、両方のプログラムには、無料の Microsoft 365 [開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、Visual Studio サブスクリプションの有効期間中はアクティブです。 「*Microsoft 365 開発者サブスクリプションを設定する*」[を参照してください](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。

## <a name="enable-microsoft-teams-for-your-organization"></a>組織用に Microsoft Teams を有効にする 

組織に対して Microsoft Teams が有効になっていない場合は、最初に行う必要があります。 詳しい説明は、「[組織での Teams を有効にする](/microsoftteams/enable-features-office-365)」を参照してください。

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>カスタム Teams アプリを有効にして、カスタム アプリのアップロードを有効にする

開発者テナントのカスタムアプリのサイドローディングを次のようにオンにします。

1. 管理者の資格情報を使用して[ Microsoft 365 管理センター](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)にサイン インします。 

2. [**すべての** --> **Teams の表示**]を選択します。 

![管理センター メニューの画像](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> "Teams" オプションが表示されるまで、最大で24時間かかります。 その間、テストおよび検証用に[カスタムアプリをTeams 環境にアップロード](/microsoftteams/upload-custom-apps#validate) することができます。

3. **Teams アプリ** --> **セット アップ ポリシー** --> **グローバル (組織全体の既定)** に移動する  

![sideload ビューを有効にする](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. **カスタム アプリのアップロード** を切り替え **オン** の位置にします。

5. [保存 **] を** 選択して変更を保存します。

手順は以上です。 テスト テナントで、カスタムアプリのサイドローディングができるようになりました。

> [!Note] 
> サイドローディングが有効になるまでに 24 時間かかることがあります。 その間、[**アップロード\<your tenant>**] を使用して、アプリをテストできます。

![updload アプリ ビュー](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

これらの設定がどのように機能するかの詳細については、「[Microsoft Teams のカスタム アプリ ポリシーと設定の管理](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)」 および「[Microsoft Teams のアプリ セットアップ ポリシーの管理](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)」を *参照してください*。
