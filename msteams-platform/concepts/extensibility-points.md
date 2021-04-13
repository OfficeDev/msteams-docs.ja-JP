---
title: Teams アプリのエントリー ポイント
author: heath-hamilton
description: ユーザーが Teams でアプリを発見し、使用できる場所を説明します。
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f61e5b5c05855c0a3a766920095cf46f699f08a6
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654357"
---
# <a name="entry-points-for-teams-apps"></a>Teams アプリのエントリー ポイント

Teams プラットフォームは、チーム、チャネル、チャットなどの柔軟なエントリ ポイントセットを提供し、ユーザーがアプリを検出して使用できます。 アプリは、既存の Web コンテンツをタブに埋め込むようなシンプルなものから、ユーザーが複数のコンテキストで操作する多面的なものまであります。
最も成功したアプリは Teams にネイティブなので、アプリのエントリ ポイントを慎重に選択します。

## <a name="shared-app-experiences"></a>共有アプリ エクスペリエンス

チーム、チャネル、チャットはコラボレーション スペースです。 これらのコンテキストのアプリは、その領域内のすべてのユーザーが利用できます。 通常、コラボレーション スペースは、追加のワークフローに焦点を当てたり、新しいソーシャル操作のロックを解除したりします。

次の一覧は、Teams アプリの機能が共同作業コンテキストで一般的に使用される方法を示しています。

* [**タブ**](~/tabs/what-are-tabs.md) には、チーム、チャネル、またはグループ チャットに合わせて構成される全画面の組み込み Web エクスペリエンスがあります。 すべてのメンバーが同じ Web ベースのコンテンツを操作します。そのため、ステートレスな単一ページ アプリ エクスペリエンスが一般的です。

* [**メッセージング拡張**](~/messaging-extensions/what-are-messaging-extensions.md) は、外部のコンテンツを会話に挿入したり、Teams を離れることなくメッセージにアクションを起こすためのショートカットです。 [リンク解除は、共通](~/messaging-extensions/how-to/link-unfurling.md) の URL からコンテンツを共有するときにリッチ コンテンツを提供します。

* [**ボットは**](~/bots/what-are-bots.md) 、チャットを通じて会話のメンバーと対話し、新しいメンバーの追加やチャネルの名前の変更などのイベントに応答します。 
   > [!NOTE]
   > これらのコンテキストでのボットとの会話は、チーム、チャネル、またはグループのすべてのメンバーに表示されます。そのため、ボットの会話は全員に関連している必要があります。

* [**Webhook とコネクタ**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) では、外部サービスが会話にメッセージを投稿したり、ユーザーがサービスにメッセージを送信することができます。

* [**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) では、チーム、チャネル、グループ チャットに関するデータを取得し、Teams プロセスの自動化や管理に役立てます。

## <a name="personal-app-experiences"></a>個人用アプリエクスペリエンス

[個人用アプリ](../concepts/design/personal-apps.md) は、1 人のユーザーとのやりとりに焦点を当てます。 このコンテキストでのエクスペリエンスは、それぞれのユーザーに固有のものです。

次の一覧は、Teams の機能が個人のコンテキストで一般的に使用される方法を示しています。

* [**ボット**](~/bots/what-are-bots.md) はユーザーと 1 対 1 で会話します。 複数回の会話が必要なものや、特定のユーザーにのみ関連する通知を提供するボットは、個人用アプリに最適です。

* [**タブ**](~/tabs/what-are-tabs.md) は、それを見ているユーザーにとって意味のある、フルスクリーンの埋め込み Web エクスペリエンスを提供します。

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [Teams アプリの設計ガイドライン](../concepts/design/design-teams-app-overview.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [使用例を理解する](../concepts/design/understand-use-cases.md)
