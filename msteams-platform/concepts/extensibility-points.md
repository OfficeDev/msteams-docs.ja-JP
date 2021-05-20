---
title: Teams アプリのエントリー ポイント
author: heath-hamilton
description: ユーザーが Teams でアプリを発見し、使用できる場所を説明します。
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: c26b938f56af6f09c0e4ba274b9b3f4da19d08ee
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566174"
---
# <a name="entry-points-for-teams-apps"></a>Teams アプリのエントリー ポイント

Teams プラットフォームは、チーム、チャネル、チャットなど、ユーザーがアプリを検出して使用できる、柔軟なエントリ ポイントセットを提供します。 アプリは、既存の Web コンテンツをタブに埋め込むようなシンプルなものから、ユーザーが複数のコンテキストで操作する多面的なものまであります。
最も成功したアプリはTeamsネイティブであるため、アプリのエントリ ポイントは慎重に選択してください。

## <a name="shared-app-experiences"></a>共有アプリ エクスペリエンス

チーム、チャネル、チャットはコラボレーションスペースです。 これらのコンテキストのアプリは、その領域のすべてのユーザーが利用できます。 コラボレーションスペースは、通常、追加のワークフローに焦点を当てたり、新しいソーシャルインタラクションのロックを解除したりします。

次の一覧は、Teamsアプリの機能がコラボレーション コンテキストで一般的に使用される方法を示しています。

* [**タブ**](~/tabs/what-are-tabs.md) には、チーム、チャネル、またはグループ チャットに合わせて構成される全画面の組み込み Web エクスペリエンスがあります。 すべてのメンバーが同じ Web ベースのコンテンツと対話するので、ステートレスな単一ページ アプリエクスペリエンスが一般的です。

* [**メッセージング拡張**](~/messaging-extensions/what-are-messaging-extensions.md) は、外部のコンテンツを会話に挿入したり、Teams を離れることなくメッセージにアクションを起こすためのショートカットです。 [リンクの展開は](~/messaging-extensions/how-to/link-unfurling.md) 、共通 URL からコンテンツを共有する際にリッチ コンテンツを提供します。

* [**ボットは、**](~/bots/what-are-bots.md) チャットを通じて会話のメンバーと対話し、新しいメンバーの追加やチャンネルの名前変更などのイベントに応答します。 
   > [!NOTE]
   > これらのコンテキストでボットとの会話はチーム、チャネル、またはグループのすべてのメンバーに表示されるため、ボットの会話は全員に関連している必要があります。

* [**Webhook とコネクタ**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) では、外部サービスが会話にメッセージを投稿したり、ユーザーがサービスにメッセージを送信することができます。

* [**Microsoft Graph REST API**](/graph/teams-concept-overview) では、チーム、チャネル、グループ チャットに関するデータを取得し、Teams プロセスの自動化や管理に役立てます。

## <a name="personal-app-experiences"></a>パーソナルアプリエクスペリエンス

[個人用アプリ](../concepts/design/personal-apps.md) は、1 人のユーザーとのやりとりに焦点を当てます。 このコンテキストでのエクスペリエンスは、それぞれのユーザーに固有のものです。

以下のリストは、Teams機能が個人的なコンテキストで一般的に使用される方法を示しています。

* [**ボット**](~/bots/what-are-bots.md) はユーザーと 1 対 1 で会話します。 複数回の会話が必要なものや、特定のユーザーにのみ関連する通知を提供するボットは、個人用アプリに最適です。

* [**タブ**](~/tabs/what-are-tabs.md) は、ユーザーが見る意味のある全画面表示の埋め込み Web エクスペリエンスを提供します。

## <a name="see-also"></a>関連項目

[アプリの設計ガイドラインTeams](../concepts/design/design-teams-app-overview.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ユース ケースの理解](../concepts/design/understand-use-cases.md)
