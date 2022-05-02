---
title: Teams アプリを Microsoft 365 全体に拡張する (プレビュー)
description: Teams アプリ エクスペリエンスを、使用頻度の高い Microsoft 365 の他の領域に拡張します
ms.date: 02/11/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 66ba17a638fc57b47febef34bea769e39cdea7e3
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111949"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Teams アプリを Microsoft 365 全体に拡張する

> [!NOTE]
> 初期段階のこの開発者向けプレビューは、既存のアプリケーションの Teams 開発者に対して、新しい機能を試し、Teams 開発者プラットフォームを使用頻度の高い Microsoft 365 エコシステムの他の領域に拡張することに関する[フィードバックを提供](/microsoftteams/platform/feedback)していただく機会を提供することを目的としています。

Microsoft Office および Outlook で実行されている Teams アプリは、新しい[Microsoft Teams JavaScript クライアント SDK v2 プレビュー](using-teams-client-sdk-preview.md)と Microsoft Teams [開発者プレビュー マニフェスト](../resources/schema/manifest-schema-dev-preview.md)を使用するようにコードを更新することによってテストできるようになります。

このプレビューでは、次のことができます。

- 既存の Teams [個人用タブ](/microsoftteams/platform/tabs/how-to/create-personal-tab)をデスクトップ用 Outlook、Outlook on the web、Office on the web (office.com) に拡張する。
- 既存の Teams [検索ベースのメッセージ拡張機能](/microsoftteams/platform/messaging-extensions/how-to/search-commands/define-search-command)を、デスクトップ用 Outlook と Outlook on the web に拡張する。

フィードバックと問題については、関連する [Microsoft Teams 開発者コミュニティ チャネル](/microsoftteams/platform/feedback)を引き続きご利用ください。

## <a name="teams-personal-tabs-in-office-and-outlook"></a>Office と Outlook での Teams 個人用タブ

このプレビューを使用すると、Teams 個人用タブ アプリケーションを拡張して、Windows デスクトップ版の Outlook と Outlook on the web、および Office on the web でも実行できるようになります。

Teams にサイドロードすると、個人用タブが Outlook と Office にインストールされているアプリの 1 つとして表示されます。

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Outlook、Office、Teams で実行されている個人用タブ":::

## <a name="teams-message-extensions-in-outlook"></a>Outlook での Teams メッセージ拡張機能

このプレビューを使用すると、検索ベースの Teams メッセージ拡張機能を Outlook on the web および Windows デスクトップに拡張して、Microsoft Teams クライアントだけでなく Outlook のメッセージ作成領域でも顧客が結果を検索および共有できるようにすることができます。

Teams にサイドロードすると、メッセージ拡張機能は、Outlook のメッセージ作成領域にインストールされているアプリの 1 つとして表示されます。

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="Outlook と Teams で実行されているメッセージ拡張機能":::

## <a name="next-steps"></a>次の手順

Teams アプリを Microsoft 365 全体に拡張するための開発環境を設定します。

> [!div class="nextstepaction"]
> [前提条件のインストール](prerequisites.md)
