---
title: Office 365 テナントの準備
description: Office 365 で Teams の使用を開始する方法
keywords: Office 365 テナントチームのアップロードを構成する
ms.openlocfilehash: 35f102223a5f8e6a8e12268e22aedca07a61b1fa
ms.sourcegitcommit: 058b7bbd817af5f513e0e018f2ef562dc3086a84
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2020
ms.locfileid: "43120270"
---
# <a name="prepare-your-office-365-tenant"></a>Office 365 テナントの準備

Office 365 サブスクライバーの場合は、次のいずれかの[プラン](https://products.office.com/business/compare-more-office-365-for-business-plans)を使用して Microsoft Teams 用アプリを開発できます。

* Business Essentials
* Business Premium
* Enterprise E1、E3、E5
* Developer
* 教育、教育プラス、教育の E5

また、[退職](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)前に、E4 をサブスクライブしたお客様も、Microsoft Teams を利用することができます。

## <a name="just-need-a-development-environment"></a>開発環境のみが必要ですか。

現在 Office 365 アカウントを持っていない場合は、 [office 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program)サブスクリプションにサインアップできます。 これは90日間*無料*で、開発アクティビティに使用している間は継続的に更新されます。 Visual Studio *Enterprise*または*Professional*サブスクリプションを所有している場合は、両方のプログラムに無料の Office 365[開発者サブスクリプション](https://aka.ms/MyVisualStudioBenefits)が含まれています。これは、visual studio サブスクリプションの有効期間中にアクティブになります。 *「* [Microsoft 365 developer サブスクリプションをセットアップする」を](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)参照してください。

## <a name="enable-microsoft-teams-for-your-organization"></a>組織に対して Microsoft Teams を有効にする

Microsoft Teams が組織に対して有効になっていない場合は、最初にその作業を行う必要があります。 [組織で Teams を有効](https://docs.microsoft.com/microsoftteams/enable-features-office-365)にするための詳細なガイダンスを参照してください。

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>カスタム Teams アプリを有効にし、カスタムアプリのアップロードをオンにする

> [!Note] 
> Office 365 developer platform を使用してアプリをビルドしている場合は、アプリのビルド、アップロード、およびテストができるように、これらの設定を構成しておく必要があります。

カスタムアプリとカスタムアプリのアップロードを有効にするには、次の3つの設定が関係します。

* **組織全体のカスタムアプリ設定** => **で**カスタム => **アプリを使用することができ**ます—この設定では、組織のカスタムアプリを有効または無効にできます。 これをオンにする必要があります。 
* **チームカスタムアプリ設定** => を使用すると、**メンバーがカスタムアプリ** => **のオン/オフ**をアップロードできるようになります。この設定は、Microsoft Teams 内の個々のチームに適用されます。 特定のチームに対してアプリをインストールする場合は、そのチームに対してこれをオンにする必要があります。
* **User custom app policy** => **user はカスタムアプリ** => **をオン/オフに**することができます。この設定により、個々のユーザーのアクセス許可が制御されます。 これは、カスタムアプリのアップロードが許可されている個人に対して有効にする必要があります。

これらの設定がどのように影響するかの詳細については、「 [Microsoft teams でカスタムアプリポリシーと設定を管理](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)する」および「 [microsoft teams でアプリのセットアップポリシーを管理](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)する *」を参照してください*。
