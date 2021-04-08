---
title: Teams アプリのエントリー ポイント
author: heath-hamilton
description: ユーザーが Teams でアプリを発見し、使用できる場所を説明します。
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 72ce2620160f854bbe458821db01e91d2d9f62cd
ms.sourcegitcommit: 098d38dd947e87e69d289b99e807bea2d95c42f9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/18/2020
ms.locfileid: "49713628"
---
# <a name="entry-points-for-teams-apps"></a>Teams アプリのエントリー ポイント

Teams プラットフォームには、ユーザーがアプリを発見して使用することができる柔軟なエントリー ポイントがあります。 アプリは、既存の Web コンテンツをタブに埋め込むようなシンプルなものから、ユーザーが複数のコンテキストで操作する多面的なものまであります。

最もうまくいっているアプリは、Teams にネイティブな感覚なので、アプリのエントリー ポイントを慎重に計画することが重要です。

## <a name="teams-channels-and-chats"></a>Teams、チャネル、チャット

Teams、チャネル、およびチャットは共同作業スペースです。 このようなコンテキストでのアプリは、その空間内のすべてのユーザーが使用でき、一般的には、ワークフローの追加や新しい社会的対話の実現に重点が置かれます。

ここでは、Teams アプリの機能が共同作業の場でどのように使われているかをご紹介します。

* [**タブ**](~/tabs/what-are-tabs.md) には、チーム、チャネル、またはグループ チャットに合わせて構成される全画面の組み込み Web エクスペリエンスがあります。 すべてのメンバーは同じ Web ベースのコンテンツで会話するため、ステートレスなシングル ページ アプリ エクスペリエンスが一般的です。

* [**メッセージング拡張**](~/messaging-extensions/what-are-messaging-extensions.md) は、外部のコンテンツを会話に挿入したり、Teams を離れることなくメッセージにアクションを起こすためのショートカットです。 リンクの広がりは、共通の URL からコンテンツを共有する場合に、リッチ コンテンツを提供します。

* [**ボット**](~/bots/what-are-bots.md) は、チャットを通じて会話のメンバーと会話したり、イベント (新しいメンバーの追加や、チャネル名の変更など) に対応したりします。 このコンテキストでのボットとの会話は、チーム、チャネル、グループのすべてのメンバーに表示されるので、会話がすべてのユーザーに関連性のあるものであることを確認する必要があります。

* [**Webhook とコネクタ**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) では、外部サービスが会話にメッセージを投稿したり、ユーザーがサービスにメッセージを送信することができます。

* [**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) では、チーム、チャネル、グループ チャットに関するデータを取得し、Teams プロセスの自動化や管理に役立てます。

## <a name="personal-apps"></a>個人用アプリ

[個人用アプリ](~/concepts/design/personal-apps.md) は、1 人のユーザーとのやりとりに焦点を当てます。 このコンテキストでのエクスペリエンスは、それぞれのユーザーに固有のものです。

ここでは、Teams の機能が個人的なコンテキストでどのように使われているかをご紹介します。

* [**ボット**](~/bots/what-are-bots.md) はユーザーと 1 対 1 で会話します。 複数回の会話が必要なものや、特定のユーザーにのみ関連する通知を提供するボットは、個人用アプリに最適です。

* [**タブ**](~/tabs/what-are-tabs.md) は、閲覧するユーザーにとって意味のある全画面の埋め込み Web エクスペリエンスを提供します。

## <a name="examples"></a>例

Teams アプリのデザイン ガイドラインでは、ユーザーがどこで Teams アプリを検出し、使用するかを示す詳細を視覚的に提供します。

> [!div class="nextstepaction"]
> [Teams アプリのデザイン ガイドラインを表示する](../concepts/design/design-teams-app-overview.md)
