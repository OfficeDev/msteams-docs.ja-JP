---
title: Teams アプリをMicrosoft 365全体に拡張する (プレビュー)
description: Teams アプリ エクスペリエンスを、Microsoft 365の他の高使用率領域に拡張する
ms.date: 02/11/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 013bb773897965d51daaa485459eec78478292b3
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104344"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Teams アプリを Microsoft 365 全体に拡張する

> [!NOTE]
> この初期の開発者向けプレビューは、Teams開発者に既存のアプリケーションに新しい機能を試す機会を提供し、Teams開発者プラットフォームをMicrosoft 365 エコシステムの他の高使用率領域に拡張することに関する[フィードバックを提供](/microsoftteams/platform/feedback)することを目的としています。

Microsoft OfficeおよびOutlookで実行されているTeams アプリをテストするには、新しい[Microsoft Teams JavaScript クライアント SDK v2 プレビュー](using-teams-client-sdk-preview.md) マニフェストと開発者[プレビュー マニフェスト](../resources/schema/manifest-schema-dev-preview.md)Microsoft Teams使用するようにコードを更新します。

このプレビューでは、次のことができます。

- 既存のTeams[個人用タブ](/microsoftteams/platform/tabs/how-to/create-personal-tab)をデスクトップと Web のOutlookに拡張し、Office on the web (office.com) することもできます。
- 既存のTeams[検索ベースのメッセージ拡張機能](/microsoftteams/platform/messaging-extensions/how-to/search-commands/define-search-command)を、デスクトップと Web のOutlookに拡張します。

フィードバックと問題については、関連する[Microsoft Teams開発者コミュニティ チャネル](/microsoftteams/platform/feedback)を引き続き使用してください。

## <a name="teams-personal-tabs-in-office-and-outlook"></a>OfficeとOutlookで個人用タブをTeamsする

このプレビューでは、Teams個人用タブ アプリケーションを拡張して、デスクトップと Web の両方のOutlookで実行Windowsし、Office on the webすることもできます。

Teamsにサイドロードすると、個人用タブがOutlookとOfficeにインストールされているアプリの 1 つとして表示されます。

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Outlook、Office、Teamsで実行されている個人用タブ":::

## <a name="teams-message-extensions-in-outlook"></a>Outlookでメッセージ拡張機能をTeamsする

このプレビューでは、検索ベースのTeamsメッセージ拡張機能をOutlook on the webおよびWindows デスクトップに拡張し、Microsoft Teams クライアントだけでなく、Outlookの作成メッセージ領域で結果を検索および共有できます。

Teamsにサイドロードすると、メッセージ拡張機能は、Outlook作成メッセージ領域にインストールされているアプリの 1 つとして表示されます。

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="OutlookとTeamsで実行されているメッセージ拡張機能":::

## <a name="next-steps"></a>次の手順

Microsoft 365間でTeams アプリを拡張するための開発環境を設定します。

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)
