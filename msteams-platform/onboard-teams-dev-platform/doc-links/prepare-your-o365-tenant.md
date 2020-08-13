---
title: Teams 開発環境の準備
description: 開発している Teams アプリを開発するための環境をセットアップする方法
keywords: Office 365 テナントチームを構成して環境の開発をアップロードする
ms.openlocfilehash: 701c6c110026007cf1670e783348bbdbe1aff498
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652079"
---
# <a name="prepare-your-development-environment"></a>開発環境を準備する

Office 365 サブスクライバーの場合は、次のいずれかの[プラン](https://products.office.com/business/compare-more-office-365-for-business-plans)を使用して Microsoft Teams 用アプリを開発できます。

* Business Essentials
* Business Premium
* Enterprise E1、E3、E5
* Developer
* 教育、教育プラス、教育の E5

また、[退職](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)前に、E4 をサブスクライブしたお客様も、Microsoft Teams を利用することができます。

## <a name="just-need-a-development-environment"></a>開発環境のみが必要ですか。

現在 Office 365 アカウントを持っていない場合は、 [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program)サブスクリプションにサインアップできます。 これは90日間*無料*で、開発アクティビティに使用している間は継続的に更新されます。 Visual Studio *Enterprise*または*Professional*サブスクリプションを所有している場合は、どちらのプログラムにも、visual studio サブスクリプションの有効期間中にアクティブな Microsoft 365[開発者向けサブスクリプション](https://aka.ms/MyVisualStudioBenefits)が組み込まれています。 *「* [Microsoft 365 developer サブスクリプションをセットアップする」を](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)参照してください。

## <a name="enable-microsoft-teams-for-your-organization"></a>組織に対して Microsoft Teams を有効にする

Microsoft Teams が組織に対して有効になっていない場合は、最初にその作業を行う必要があります。 [組織で Teams を有効](https://docs.microsoft.com/microsoftteams/enable-features-office-365)にするための詳細なガイダンスを参照してください。

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>カスタム Teams アプリを有効にし、カスタムアプリのアップロードをオンにする

開発者テナントのカスタムアプリのサイドロードを次のようにオンにします。

1. 管理者の資格情報を使用して[Microsoft 365 管理センター](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)にログインします。 

2. [**すべてのチームを表示**] を選択し  -->  **Teams**ます。 

![アプリのオーバーフローメニューのイメージ](~/assets/images/prepare-test-tenant/admin-center.png)

3. **Teams apps**  -->  **セットアップポリシー**  -->  **グローバル (組織全体の既定)** に移動する  

![アプリのオーバーフローメニューのイメージ](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. [**カスタムアプリのアップロード**を**オン**の位置に切り替える。

するだけです。 テストテナントは、カスタムアプリのサイドロードを許可するようになります。

> [!Note] 
> サイドローディングが有効になるまで最大24時間かかる場合があります。 中間時に、**の \<your tenant> upload**を使用してアプリをテストできます。

![アプリのオーバーフローメニューのイメージ](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

これらの設定がどのように影響するかの詳細については、「 [Microsoft teams のカスタムアプリポリシーと設定を管理](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)する」および「 [microsoft teams でアプリのセットアップポリシーを管理](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)する *」を参照してください*。