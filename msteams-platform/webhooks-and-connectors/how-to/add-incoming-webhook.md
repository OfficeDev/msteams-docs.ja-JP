---
title: 受信 Webhook を使用して外部リクエストを Microsoft Teams に投稿する
author: laujan
description: Teams アプリに受信 Webhook を追加する方法
keywords: Teams タブ 送信 Webhook*
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a05f9ec448a722f3d662a8323a40ebe6b2de1e27
ms.sourcegitcommit: 23ceb25d07a76f03ffe92cf1ac578b7c50b0bafc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2021
ms.locfileid: "49777918"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a>受信 Webhook を使用して外部リクエストを Teams に投稿する

## <a name="what-are-incoming-webhooks-in-teams"></a>Teams での受信 Webhook とは

受信 Webhook は Teams の特別な種類のコネクタで、外部アプリがチーム チャネルでコンテンツを共有するためのシンプルな方法を提供し、時にはトラッキングや通知ツールとしても使用されます。 Teams は、投稿するメッセージと JSON ペイロードを通常カード形式で送信するための一意の URL を提供します。 カードは、ある 1 つのトピックに関連するコンテンツとアクションを含んだユーザー インターフェース (UI) コンテナであり、メッセージ データを一貫した方法で表示するための方法です。 Teams は、次の 3 つの機能でカードを使用します。

* ボット
* メッセージング拡張機能
* コネクタ

## <a name="incoming-webhook-key-features"></a>受信 Webhook の主な機能

| 機能 | 説明 |
| ------- | ----------- |
|スコープ構成|受信 Webhook にはスコープが設定されており、チャネル レベルで構成されます (例: 送信 Webhook はチーム レベルで構成されます)。|
|セキュリティで保護されたリソース定義|メッセージは JSON ペイロードとして書式設定されます。 この宣言メッセージング構造により、クライアントでコードが実行されることはないため、悪意のあるコードの挿入が防止されます。|
|アクション可能なメッセージングのサポート|カード経由でメッセージを送信する場合は、**アクション可能なメッセージ カード** 形式を使用する必要があります。 アクション可能なメッセージ カードは、Teams を含むすべての Office 365 グループでサポートされています。 こちらは、「[従来の操作可能なメッセージ カード リファレンス](/outlook/actionable-messages/message-card-reference)」と「[メッセージ カードのプレイグラウンド](https://messagecardplayground.azurewebsites.net)」へのリンクです。|
|独立した HTTPS メッセージングのサポート| カードは、明瞭で一貫した方法で情報を表示する優れた方法です。 HTTPS POST 要求を送信できるツールやフレームワークは、受信 Webhook を介して Teams にメッセージを送信できます。|
|Markdown のサポート|アクション可能なメッセージング カードのすべてのテキスト フィールドで、基本的な Markdown がサポートされています。 **カードには HTML マークアップを使用しないでください**。 HTML は無視され、プレーン テキストとして扱われます。|

> [!Note]
> Teams ボット、メッセージング拡張機能、受信 Webhook、Bot Framework は、オープンなクロスカード プラットフォーム フレームワークであるアダプティブ カードをサポートします。 [Teams コネクタは現在](../../webhooks-and-connectors/how-to/connectors-creating.md) 、アダプティブ カードをサポートしていない。 ただし、Teams チャネルにアダプティブ カード [を](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) 投稿するフローを作成することもできます。

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a>Teams チャネルに受信 Webhook を追加する

> [!Important]  
> チームの **[設定]** => **[メンバーのアクセス許可]** => **[Allow members to create, update, and remove connectors]** (メンバーがコネクタを作成、更新、削除することを許可する) が選択されている場合、すべてのチーム メンバーがコネクタの追加、変更、削除を行うことができます。

1. Webhook を追加するチャネルに移動し、上部のナビゲーション バーから (&#8226;&#8226;&#8226;) *[その他のオプション]* を選択します。
1. ドロップダウン メニューから **[コネクタ]** を選択し、**受信 Webhook** を検索します。
1. **[構成]** ボタンを選択し、名前を入力し、オプションで Webhook 用の画像アバターをアップロードします。
1. ダイアログ ウィンドウに、チャネルにマッピングされる一意の URL が表示されます。 **URL をコピーして保存した** ことをご確認ください (URL は外部サービスに提供する必要があります)。
1. **[完了]** ボタンを選択します。 Webhook が、チーム チャネルで利用できるようになります。

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a>Teams チャネルから受信 Webhook を削除する

1. Webhook が追加されたチャネルに移動し、上部のナビゲーション バーから (&#8226;&#8226;&#8226;) *[その他のオプション]* を選択します。
1. ドロップダウン メニューから **[コネクタ]** を選択します。
1. 左側にある **[管理]** で、**[構成]** を選択します。
1. *[number Configured]* (構成されている数) を選択すると、現在のコネクタの一覧が表示されます。
1. 削除するコネクタの横にある **[管理]** を選択します。
1. **[削除]** ボタンを選択すると、*[構成の削除]* ダイアログ ボックスが表示されます。
1. 必要に応じて、**[削除]** ボタンを選択する前に、ダイアログ ボックスのフィールドとチェックボックスに入力を行います。 Webhook が、チーム チャネルから削除されます。

## <a name="distribution"></a>配布

受信 Webhook の配布には、次の 3 つのオプションがあります。

* チームに受信 Webhook を直接セットアップする。
* 構成ページを追加して、受信 Webhook を [O365 コネクタ](~/webhooks-and-connectors/how-to/connectors-creating.md)でラップする。
* [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) への提出の一部としてコネクタをパッケージ化して公開する。

## <a name="learn-more"></a>詳細情報

* [コネクタと Webhook へのメッセージの送信](~/webhooks-and-connectors/how-to/connectors-using.md)
