---
title: 受信 web フックを使用して Microsoft Teams に外部要求を投稿する
author: laujan
description: 受信 webhook を Teams アプリに追加する方法
keywords: Teams、タブ、送信 Webhook*
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 3aa795170af9695fc375043c94e794f814b38646
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819068"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a>受信 web フックを使用して Teams に外部要求を投稿する

## <a name="what-are-incoming-webhooks-in-teams"></a>Teams での受信 web フックとは

受信 web フックは、外部アプリがチームチャネル内のコンテンツを共有するための簡単な方法を提供し、多くの場合、追跡および通知ツールとして使用される、Teams の特別な種類のコネクタです。 Teams には、POST するメッセージで JSON ペイロードを送信するための一意の URL が用意されています (通常はカード形式)。 カードは、1つのトピックに関連するコンテンツとアクションを含むユーザーインターフェイス (UI) コンテナーで、一貫性のある方法でメッセージデータを表示する方法です。 Teams は3つの機能内でカードを使用します。

* ボット
* メッセージングの拡張機能
* コネクタ

## <a name="incoming-webhook-key-features"></a>受信 webhook キー機能

| 機能 | 説明 |
| ------- | ----------- |
|スコープ構成|受信 web フックは、チャネルレベルでスコープ設定および構成されます (たとえば、送信 web フックはチームレベルでスコープ設定および構成されます)。|
|リソース定義の保護|メッセージは JSON ペイロードとして書式設定されます。 この宣言型メッセージング構造では、クライアントでコードが実行されていないため、悪意のあるコードが挿入されることはありません。|
|アクション可能なメッセージングのサポート|カードを経由してメッセージを送信する場合は、操作可能な **メッセージカード** 形式を使用する必要があります。 操作可能なメッセージカードは、Teams を含むすべての Office 365 グループでサポートされています。 従来の操作可能な [メッセージカード参照](/outlook/actionable-messages/message-card-reference) と [メッセージカードプレイグラウンド](https://messagecardplayground.azurewebsites.net)へのリンクを以下に示します。|
|独立した HTTPS メッセージングのサポート| カードは、わかりやすく一貫した方法で情報を表示するための最適な方法です。 HTTPS POST 要求を送信できる任意のツールまたはフレームワークは、受信した webhook を介してチームにメッセージを送信できます。|
|Markdown のサポート|操作可能なメッセージングカードのすべてのテキストフィールドは、基本的な Markdown をサポートします。 **カードには、HTML マークアップを使用しないで**ください。 HTML は無視され、プレーン テキストとして扱われます。|

> [!Note]  
> Teams bot、メッセージング拡張機能、ボットフレームワークは、オープンなクロスカードプラットフォームフレームワークであるアダプティブカードをサポートしています。 Teams コネクタは現在、アダプティブカードをサポートしていません。 ただし、アダプティブカードを Teams チャネルにポストする [フロー](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) を作成することは可能です。

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a>受信 webhook を Teams チャネルに追加する

> [!Important]  
> チームの**設定**メンバーのアクセス許可で [  =>  **Member permissions**  =>  **メンバーによるコネクタの作成、更新、および削除を許可**する] が選択されている場合は、すべてのチームメンバーがコネクタを追加、変更、または削除できます。

1. Webhook を追加するチャネルに移動し、上部のナビゲーションバーから [ *その他のオプション* ] を選択します (&#8226;&#8226;&#8226;)。
1. ドロップダウンメニューから [ **コネクタ** ] を選択し、 **受信 Webhook**を検索します。
1. [ **構成** ] ボタンを選択し、名前を入力します。必要に応じて、webhook の画像アバターをアップロードします。
1. ダイアログウィンドウには、チャネルにマップされる一意の URL が表示されます。 **URL をコピーして保存**することを確認し、外部のサービスに提供する必要があります。
1. [ **完了** ] ボタンをクリックします。 Webhook はチームチャネルで利用可能になります。

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a>Teams チャネルから受信 webhook を削除する

1. Webhook が追加されたチャネルに移動し、トップナビゲーションバーから [(&#8226;&#8226;&#8226;)] *オプション* を選択します。
1. ドロップダウンメニューから [ **コネクタ** ] を選択します。
1. 左側の [ **管理**] で、[ **構成済み**] を選択します。
1. 構成した *番号* を選択して、現在のコネクタの一覧を表示します。
1. 削除するコネクタの横にある [ **管理** ] を選択します。
1. [ **削除** ] ボタンを選択すると、[ *構成の削除* ] ダイアログボックスが表示されます。
1. 必要に応じて、[ **削除** ] ボタンを選択する前に、ダイアログボックスのフィールドとチェックボックスを完了します。 Webhook はチームチャネルから削除されます。

## <a name="distribution"></a>分配

受信 webhook を配布するには、次の3つのオプションがあります。

* チームの受信 webhook を直接設定します。
* [構成] ページを追加し、 [O365 コネクタ](~/webhooks-and-connectors/how-to/connectors-creating.md)で受信 webhook をラップする
* [Appsource](~/concepts/deploy-and-publish/office-store-guidance.md)提出の一部として、コネクタをパッケージ化して発行します。

## <a name="learn-more"></a>詳細情報

* [コネクタと Web フックへのメッセージの送信](~/webhooks-and-connectors/how-to/connectors-using.md)
