---
title: Microsoft 365 用の Teams アプリを発行する
description: Teams、Outlook、OfficeのユーザーがMicrosoft 365対応のTeams アプリを検出できるようにします
ms.date: 05/24/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: b256eb75f871425d855c0f12359015134870efc0
ms.sourcegitcommit: 1e77573e47fad51a19545949fdac1241b13052e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656081"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>Microsoft 365 用の Teams アプリを発行する

Microsoft Teamsでの運用環境での使用では、Microsoft 365対応のTeams アプリがサポートされています。 これらのアプリを配布して、*対象となるリリース* バージョンの outlook.com と office.com を使用する対象ユーザーと、デスクトップ用の *ベータ チャネル* ビルドのOutlook Windows配布できます。 Microsoft 365対応のTeams アプリの配布オプションとプロセスは、従来のTeams アプリの場合と同じです。

発行されたアプリは、Teams ストアに加えて、Outlook ストアとOffice アプリ ストアからインストール可能なアプリとして検出できるようになります。 アプリでは、OutlookとOfficeのTeamsで定義されているアクセス許可が使用されます。 Teams管理者は、組織内のユーザー[のMicrosoft 365全体でTeams アプリへのアクセスを管理](/MicrosoftTeams/manage-third-party-teams-apps)できます。

:::image type="content" source="images/outlook-office-app-store.png" alt-text="SurveyMonkey および SYMMETRIC Teams アプリのOutlookとOffice.com のインストール画面":::

## <a name="single-tenant-distribution"></a>シングルテナント配布

Outlookが有効なメッセージ拡張機能は、いくつかの方法でテストテナントと運用テナントに配布できます。

### <a name="teams-client"></a>Teams クライアント

[*アプリ*] メニューの [*アプリ* > の管理] を選択します *。appSubmit* >  **an app を組織に** 公開します。これには、IT 管理者の承認が必要です。

### <a name="teams-developer-portal"></a>Teams 開発者ポータル

[Teams開発者ポータル](https://dev.teams.microsoft.com/)を使用して、アプリをアップロードして組織に発行します。 これには、IT 管理者の承認が必要です。詳細については、「[Microsoft Teams用開発者ポータルでアプリを管理する」を参照してください](../concepts/build-and-test/teams-developer-portal.md)。

### <a name="microsoft-teams-admin-center"></a>‎Microsoft Teams 管理センター

Teams管理者は、管理センターから組織のテナントのアプリ パッケージ[をアップロードして事前インストールTeams](https://admin.teams.microsoft.com/)できます。 詳細については、[Microsoft Teams管理センターでカスタム アプリをアップロードする](/MicrosoftTeams/upload-custom-apps)方法に関するMicrosoft Teamsを参照してください。

### <a name="microsoft-admin-center"></a>Microsoft Admin Center

グローバル管理者は、[Microsoft 管理者](https://admin.microsoft.com/)からアプリ パッケージをアップロードして事前インストールできます。詳細については、[統合アプリ ポータルの「パートナーによるMicrosoft 365 Appsのテストとデプロイ」を参照してください](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)。

## <a name="multitenant-distribution"></a>マルチテナント分布

OutlookとOfficeに対して有効になっているTeams アプリの [Microsoft AppSource](https://appsource.microsoft.com/) (Microsoft コマーシャル マーケットプレース) 申請プロセスは、従来のTeams アプリと同じです。 唯一の違いは、アプリ パッケージTeamsアプリ マニフェスト [バージョン 1.13](../tabs/how-to/using-teams-client-sdk.md) を使用する必要がある点です。これにより、Microsoft 365全体で実行されるTeams アプリのサポートが導入されます。

> [!TIP]
> Teams開発者ポータルを使用して[、アプリ パッケージを検証](https://dev.teams.microsoft.com/validation)し、([Microsoft パートナー ネットワーク](https://partner.microsoft.com/)経由で) Teams ストアに送信する前に、エラーや警告を解決します。

開始するには、「[Microsoft Teams アプリを配布する](../concepts/deploy-and-publish/apps-publish-overview.md)」を参照してください。
