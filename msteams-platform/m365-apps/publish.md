---
title: Microsoft 365 用の Teams アプリを発行する
description: シングル テナントとマルチテナント配布を使用して、Microsoft 365 対応の Teams アプリを Teams、Outlook、Office のユーザーが検出できるようにする方法について説明します。
ms.date: 10/10/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: cfe650e676252a16c1665f078938adbff0d4c7d7
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789885"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>Microsoft 365 用の Teams アプリを発行する

Microsoft Teams では、運用環境向けの Microsoft 365 対応 Teams アプリがサポートされています。 これらのアプリは、 *ターゲット リリース*  (開発プレビュー) バージョンの Outlook.com と Office.com、Outlook for Windows デスクトップの *ベータ チャネル* ビルド、Android 用 Office アプリの Office Current Channel (開発プレビュー) ビルドを使用するユーザーに配布できます。 Microsoft 365 対応 Teams アプリの配布オプションとプロセスは、従来の Teams アプリの場合と同じです。

発行後、アプリは、Teams ストアに加えて、Outlook および Office アプリ ストアからインストール可能なアプリとして検出されます。 アプリでは、Outlook と Office 全体で Teams で定義されているアクセス許可が使用されます。 Teams 管理者は、組織内のユーザーに対 [する Microsoft 365 全体の Teams アプリへのアクセスを管理](/MicrosoftTeams/manage-third-party-teams-apps) できます。

:::image type="content" source="images/outlook-office-app-store.png" alt-text="スクリーンショットは、SurveyMonkey アプリと MURAL Teams アプリの Outlook と Office.com インストール画面を示す例です。":::

## <a name="single-tenant-distribution"></a>シングルテナント配布

Outlook 対応メッセージ拡張機能は、いくつかの方法でテストテナントと運用テナントに配布できます。

### <a name="teams-client"></a>Teams クライアント

[ **アプリ** ] メニューの [ **アプリの管理] [アプリ** > **の発行] [アプリ** > **を組織に送信する] の順に選択します**。アプリを送信するには、IT 管理者からの承認が必要です。

### <a name="teams-developer-portal"></a>Teams 開発者ポータル

[Teams 開発者ポータル](https://dev.teams.microsoft.com/)を使用して、組織のアプリをアップロードして発行します。 アプリをアップロードして発行するには、IT 管理者からの承認が必要です。詳細については、「 [Microsoft Teams 用開発者ポータルを使用してアプリを管理する](../concepts/build-and-test/teams-developer-portal.md)」を参照してください。

### <a name="microsoft-teams-admin-center"></a>‎Microsoft Teams 管理センター

Teams 管理者は、Teams [管理センター](https://admin.teams.microsoft.com/)から組織のテナントのアプリ パッケージをアップロードして事前インストールできます。 詳細については、「 [Microsoft Teams 管理センターでカスタム アプリをアップロードする](/MicrosoftTeams/upload-custom-apps)」を参照してください。

### <a name="microsoft-admin-center"></a>Microsoft Admin Center

グローバル管理者は、[Microsoft 管理者](https://admin.microsoft.com/)からアプリ パッケージをアップロードして事前インストールできます。詳細については、「[統合アプリ ポータルでパートナーがMicrosoft 365 Appsをテストしてデプロイする」を](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)参照してください。

## <a name="multitenant-distribution"></a>マルチテナント分布

Outlook および Office で有効になっている Teams アプリの [Microsoft AppSource](https://appsource.microsoft.com/) (Microsoft コマーシャル マーケットプレース) 申請プロセスは、従来の Teams アプリの場合と同じです。 唯一の違いは、アプリ パッケージで Teams アプリ マニフェスト [バージョン 1.13](../tabs/how-to/using-teams-client-sdk.md) を使用する必要がある点です。これにより、Microsoft 365 全体で実行される Teams アプリのサポートが導入されます。

> [!TIP]
> Teams 開発者ポータルを使用して [アプリ パッケージを検証](https://dev.teams.microsoft.com/validation) し、( [Microsoft Partner Network](https://partner.microsoft.com/) 経由で) Teams ストアに送信する前にエラーや警告を解決します。

開始するには、「 [Microsoft Teams アプリを配布](../concepts/deploy-and-publish/apps-publish-overview.md)する」を参照してください。
