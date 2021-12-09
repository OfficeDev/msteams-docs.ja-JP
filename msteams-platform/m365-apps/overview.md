---
title: 複数のTeamsアプリを拡張Microsoft 365 (プレビュー)
description: アプリ エクスペリエンスTeams他の使用率の高い領域に拡張Microsoft 365
ms.date: 11/15/2021
ms.topic: overview
ms.custom: m365apps
ms.openlocfilehash: 23251d06c38df847a98d27bbc7010b76681a4ea9
ms.sourcegitcommit: 239807b74aa222452559509d49c4f2808cd9c9ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2021
ms.locfileid: "61391333"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>複数のTeamsアプリを拡張Microsoft 365

> [!NOTE]
> この初期の開発者向けプレビューは、Teams 開発者に既存のアプリケーションに新しい機能を試し、Teams 開発者向[](/microsoftteams/platform/feedback)けプラットフォームを Microsoft 365 エコシステムの他の高利用分野に拡大するフィードバックを提供することを目的としています。

Microsoft Office および Outlook で実行されている Teams アプリをテストするには、新しい Microsoft Teams JavaScript クライアント[SDK v2](using-teams-client-sdk-preview.md) Preview および Microsoft Teams Developer プレビュー マニフェストを使用するコードを更新[します](../resources/schema/manifest-schema-dev-preview.md)。

このプレビューでは、次の機能を使用できます。

- 既存の個人用Teams[をデスクトップ](/microsoftteams/platform/tabs/how-to/create-personal-tab)Outlook Web 上のユーザーに拡張し、Office on the web (office.com)。
- 既存のTeams[ベース](/microsoftteams/platform/messaging-extensions/how-to/search-commands/define-search-command)のメッセージング拡張機能をデスクトップおよび web Outlookに拡張します。

フィードバックや問題については、開発者コミュニティ チャネルに関連するMicrosoft Teams[を使用します](/microsoftteams/platform/feedback)。

## <a name="teams-personal-tabs-in-office-and-outlook"></a>Teamsの個人用タブをOfficeおよびOutlook

このプレビューを使用すると、Teams 個人用タブ アプリケーションを拡張して、Outlook Windows デスクトップと web の Outlook と web の両方で実行し、Office on the web。

ユーザーにサイドローディングTeams、個人用タブは、インストールされているアプリの 1 つとして、OutlookおよびOffice。

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="[個人用] タブは、outlook.com":::

## <a name="teams-messaging-extensions-in-outlook"></a>Teams内のメッセージング拡張機能Outlook

このプレビューを使用すると、検索ベースの Teams メッセージング拡張機能を Outlook on the web および Windows デスクトップに拡張し、Microsoft Teams クライアントに加えて、Outlook のメッセージ作成領域を通じて結果を検索および共有できます。

メッセージをサイドローディングTeams、メッセージの作成領域にインストールされているアプリの 1 Outlook表示されます。

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="[個人用] タブは、outlook.com":::

## <a name="next-step"></a>次の手順

複数のアプリを拡張するために、Teams環境をMicrosoft 365。

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)
