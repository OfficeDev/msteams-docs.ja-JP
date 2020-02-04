---
title: Office 365 テナントの準備
description: Office 365 で Teams の使用を開始する方法
keywords: Office 365 テナントチームのアップロードを構成する
ms.openlocfilehash: 62cd640196631f50c72762253ff1bd75a143337d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674988"
---
# <a name="prepare-your-office-365-tenant"></a>Office 365 テナントの準備

Microsoft Teams 用のアプリを開発するには、[次のいずれかのプランを使用して Office 365 お客様](https://products.office.com/business/compare-more-office-365-for-business-plans)になる必要があります。

* Business Essentials
* Business Premium
* Enterprise E1、E3、E5
* Developer
* 教育、教育プラス、教育の E5

また、廃棄の前に E4 を購入したお客様も、Microsoft Teams を利用することができます。

## <a name="just-need-a-development-environment"></a>開発環境のみが必要ですか。

現在 Office 365 アカウントを持っていない場合は、office [365 開発者プログラム](https://dev.office.com/devprogram)にサインアップして、*無料*の90日間を取得できます (開発アクティビティに使用している間は更新できます) office 365 developer テナント。 このアカウントは、テスト目的にのみ使用できます。 [テストアカウントの](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US)セットアップの詳細については、「」を参照してください。

## <a name="enable-microsoft-teams-for-your-organization"></a>組織に対して Microsoft Teams を有効にする

Microsoft Teams が組織でまだ有効になっていない場合は、最初にその作業を行う必要があります。 [組織で Teams を有効](/microsoftteams/how-to-roll-out-teams)にするための詳細なガイダンスを参照してください。

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>カスタム Teams アプリを有効にし、カスタムアプリのアップロードをオンにする

> 注: O365 開発者組織を使用してアプリを構築している場合は、アプリのビルド、アップロード、およびテストができるように、これらの設定を構成しておく必要があります。

カスタムアプリとカスタムアプリのアップロードを有効にするには、次の3つの設定が関係します。

* 組織**全体のカスタムアプリ設定**-この設定は、組織のカスタムアプリを有効または無効にします。 これをオンにする必要があります。 
* [ **Team custom app setting** ]-この設定は、Microsoft Teams 内の個々のチームに対して使用されます。 特定のチームに対してアプリをインストールする場合は、そのチームに対してこれをオンにする必要があります。
* **User custom app policy** -この設定セットは、個々のユーザーのアクセス許可を制御します。 カスタムアプリをアップロードする個人に対して、これを有効にする必要があります。

これらの設定の相互関係の詳細については[、「Microsoft Teams でカスタムアプリポリシーと設定を管理](/MicrosoftTeams/teams-custom-app-policies-and-settings)する」を参照してください。
