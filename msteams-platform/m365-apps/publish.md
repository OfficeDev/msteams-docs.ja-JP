---
title: Microsoft 365 用の Teams アプリを発行する
description: Microsoft 365 対応の Teams アプリを Teams、Outlook、Office のユーザーが検出できるようにする方法について説明します。 シングルテナント、マルチテナント分散について知る。
ms.date: 05/24/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 01806f5aa7e3a5b0cb79cb6a2562cbf104f031bb
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100939"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>Microsoft 365 用の Teams アプリを発行する

Microsoft Teams では、運用用の Microsoft 365 対応 Teams アプリがサポートされています。 これらのアプリは、 *対象リリース*  (開発プレビュー) バージョンの Outlook.com と Office.com、Windows デスクトップ用 Outlook の *ベータ チャネル* ビルド、Android 用 Office アプリの Office Current Channel (開発プレビュー) ビルドを使用する対象ユーザーに配布できます。 Microsoft 365 対応 Teams アプリの配布オプションとプロセスは、従来の Teams アプリと同じです。

発行後、アプリは、Teams ストアに加えて、Outlook および Office アプリ ストアからインストール可能なアプリとして検出できるようになります。 アプリでは、Outlook と Office 全体の Teams で定義されているアクセス許可が使用されます。 Teams 管理者は、組織内のユーザー [に対して Microsoft 365 全体の Teams アプリへのアクセスを管理](/MicrosoftTeams/manage-third-party-teams-apps) できます。

:::image type="content" source="images/outlook-office-app-store.png" alt-text="スクリーンショットは、Outlook と Office.com SurveyMonkey および SYMMETRIC Teams アプリのインストール画面を示す例です。":::

## <a name="single-tenant-distribution"></a>シングルテナント配布

Outlook 対応のメッセージ拡張機能は、いくつかの方法でテストテナントと運用テナントに配布できます。

### <a name="teams-client"></a>Teams クライアント

[**アプリ**] メニューの [**アプリ** > の管理] を選択 **し、アプリ** > を発行 **して組織にアプリを送信します**。これには、IT 管理者の承認が必要です。

### <a name="teams-developer-portal"></a>Teams 開発者ポータル

[Teams 開発者ポータル](https://dev.teams.microsoft.com/)を使用して、アプリをアップロードして組織に発行します。 これには、IT 管理者の承認が必要です。詳細については、「 [Microsoft Teams 用開発者ポータルでアプリを管理する」を参照してください](../concepts/build-and-test/teams-developer-portal.md)。

### <a name="microsoft-teams-admin-center"></a>‎Microsoft Teams 管理センター

Teams 管理者は、Teams [管理センター](https://admin.teams.microsoft.com/)から組織のテナントのアプリ パッケージをアップロードして事前インストールできます。 詳細については、「 [Microsoft Teams 管理センターでカスタム アプリをアップロードする」を参照してください](/MicrosoftTeams/upload-custom-apps)。

### <a name="microsoft-admin-center"></a>Microsoft Admin Center

グローバル管理者は、[Microsoft 管理者](https://admin.microsoft.com/)からアプリ パッケージをアップロードして事前インストールできます。詳細については、[統合アプリ ポータルの「パートナーによるMicrosoft 365 Appsのテストとデプロイ」を参照してください](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)。

## <a name="multitenant-distribution"></a>マルチテナント分布

Outlook と Office が有効になっている Teams アプリの [Microsoft AppSource](https://appsource.microsoft.com/) (Microsoft コマーシャル マーケットプレース) 提出プロセスは、従来の Teams アプリと同じです。 唯一の違いは、アプリ パッケージで Teams アプリ マニフェスト [バージョン 1.13](../tabs/how-to/using-teams-client-sdk.md) を使用する必要がある点です。これにより、Microsoft 365 全体で実行される Teams アプリのサポートが導入されます。

> [!TIP]
> Teams 開発者ポータルを使用して [、アプリ パッケージを検証](https://dev.teams.microsoft.com/validation) し、( [Microsoft パートナー ネットワーク](https://partner.microsoft.com/)経由で) Teams ストアに送信する前にエラーや警告を解決します。

作業を開始するには、「 [Microsoft Teams アプリを配布する」を参照してください](../concepts/deploy-and-publish/apps-publish-overview.md)。