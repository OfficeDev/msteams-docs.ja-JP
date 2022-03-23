---
title: 複数のTeamsアプリを拡張Microsoft 365 (プレビュー)
description: アプリ エクスペリエンスTeams他の高使用率領域に拡張Microsoft 365
ms.date: 02/11/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 1936e6a660d77855e53257f40925cf54b05de0de
ms.sourcegitcommit: 5e5d2d3fb621bcbd9d792a5b450f95167ec8548b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2022
ms.locfileid: "63727293"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Teams アプリを Microsoft 365 全体に拡張する

> [!NOTE]
> この初期の開発者プレビューは、Teams 開発者に既存のアプリケーションに新しい機能を試し、Microsoft 365 エコシステムの他の高使用率[](/microsoftteams/platform/feedback)領域への Teams 開発者プラットフォームの拡張に関するフィードバックを提供することを目的としています。

Microsoft Office および Outlook で実行されている Teams アプリをテストするには、新しい [Microsoft Teams JavaScript クライアント SDK v2](using-teams-client-sdk-preview.md) Preview および Microsoft Teams [Developer](../resources/schema/manifest-schema-dev-preview.md) プレビュー マニフェストを使用するコードを更新します。

このプレビューでは、次の機能を使用できます。

- 既存の個人用Teams[をデスクトップ](/microsoftteams/platform/tabs/how-to/create-personal-tab)Outlook Web 上のユーザーに拡張し、Office on the web (office.com)。
- 既存のTeams[ベース](/microsoftteams/platform/messaging-extensions/how-to/search-commands/define-search-command)のメッセージング拡張機能をデスクトップおよび web Outlookに拡張します。

フィードバックや問題については、開発者コミュニティ チャネルに関連するMicrosoft Teams[使用してください](/microsoftteams/platform/feedback)。

## <a name="teams-personal-tabs-in-office-and-outlook"></a>Teamsの個人用タブをOfficeおよびOutlook

このプレビューを使用すると、Teams 個人用タブ アプリケーションを拡張して、Outlook デスクトップと web の Outlook Windows と web の両方で実行し、Office on the web。

ユーザーにサイドローディングTeams、個人用タブが、インストールされているアプリの 1 つとして、OutlookおよびOffice。

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="[個人用] タブは、Outlook、Office、およびTeams":::

## <a name="teams-messaging-extensions-in-outlook"></a>Teams内のメッセージング拡張機能Outlook

このプレビューを使用すると、検索ベースの Teams メッセージング拡張機能を Outlook on the web および Windows デスクトップに拡張し、Microsoft Teams クライアントに加えて、Outlook のメッセージ作成領域を通じて結果を検索および共有できます。

メッセージをサイドローディングTeams、メッセージング拡張機能は、メッセージの作成領域内にインストールされているアプリOutlook表示されます。

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="メッセージング拡張機能は、OutlookおよびTeams":::

## <a name="next-steps"></a>次の手順

複数のアプリケーション間でアプリを拡張Teams環境をMicrosoft 365。

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)
