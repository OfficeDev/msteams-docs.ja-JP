---
title: メッセージング拡張機能とは
author: clearab
description: Microsoft Teams プラットフォームでのメッセージング拡張機能の概要
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 01a038d57368826345a55358b1d628447b21f772
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674933"
---
# <a name="what-are-messaging-extensions"></a>メッセージング拡張機能とは

メッセージング拡張機能により、ユーザーは Microsoft Teams クライアントのボタンとフォームを使用して web サービスを操作することができます。 作成メッセージ領域、コマンドボックス、またはメッセージから直接、外部システムでアクションを検索したり、開始したりできます。 その結果を Microsoft Teams クライアントに送り返すことができます (通常は、強力な形式のカードの形式)。

次のスクリーンショットは、メッセージング拡張機能を呼び出す場所を示しています。

![メッセージング拡張機能の呼び出し場所](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="what-kinds-of-tasks-are-they-good-for"></a>どのような種類のタスクが適しているか。

**シナリオ:** 何らかの操作を実行するために外部システムが必要で、アクションの結果が自分の会話に送り返されるようにしたいと考えています。
**例:** リソースを予約し、チャネルに予約した曜日と時間を知らせます。

**シナリオ:** 外部システムで何かを検索する必要があり、その結果を自分の会話と共有する。
**例:** Azure DevOps で作業項目を検索し、それをアダプティブカードとしてグループと共有します。

**シナリオ:** 外部システムに複数の手順 (または大量の情報) を含む複雑なタスクを完了し、結果を会話と共有する必要があります。
**例:** Teams メッセージに基づいて追跡システムにバグを作成し、そのバグを Bob に割り当ててから、バグの詳細を含むカードを会話スレッドに送信します。

## <a name="how-do-messaging-extensions-work"></a>メッセージング拡張機能のしくみ

メッセージング拡張機能は、ホストする web サービスとアプリのマニフェストで構成されています。これは、Microsoft Teams クライアントで web サービスを呼び出すことができる場所を定義します。 Bot フレームワークのメッセージングスキーマとセキュリティで保護された通信プロトコルを利用することにより、web サービスを bot フレームワークの bot として登録する必要があります。 Web サービスを完全に手動で作成することもできますが、このプロトコルをより簡単に動作させるために[Bot フレームワーク SDK](https://github.com/microsoft/botframework)を利用することをお勧めします。

Microsoft Teams アプリのアプリマニフェストには、最大10個の異なるコマンドを持つ1つのメッセージング拡張機能を定義します。 各コマンドは、種類 (操作または検索)、およびクライアント内の場所 (メッセージ領域の作成、コマンドバー、メッセージ) を定義します。 呼び出しが完了すると、web サービスは、関連するすべての情報を含む JSON ペイロードを含む HTTPS メッセージを受信します。 JSON ペイロードで応答し、Teams クライアントに、次に有効にする相互作用を知らせます。

## <a name="types-of-messaging-extension-commands"></a>メッセージング拡張コマンドの種類

メッセージ拡張コマンドの種類によって、web サービスで使用できる UI 要素と相互作用フローが定義されます。 認証や構成などの一部の操作は、両方の種類のコマンドで使用できます。

### <a name="action-commands"></a>アクションコマンド

アクションコマンドを使用すると、ユーザーにモーダルポップアップを表示して、情報を収集または表示することができます。 ユーザーがフォームを送信すると、web サービスは会話に直接メッセージを挿入するか、またはメッセージを作成メッセージ領域に挿入してメッセージを送信できるようにすることによって応答できます。 複数のフォームを結合して、より複雑なワークフローを作成することもできます。

これらのメッセージは、[メッセージの作成] 領域、[コマンド] ボックス、またはメッセージから起動できます。 メッセージから呼び出した場合、bot に送信される最初の JSON ペイロードには、から呼び出されたメッセージ全体が含まれます。

![メッセージング拡張機能のコマンドタスクモジュール](~/assets/images/task-module.png)

### <a name="search-commands"></a>検索コマンド

検索コマンドを使用すると、ユーザーは外部システムで情報を検索できます (検索ボックスを手動で検索するか、または監視対象ドメインへのリンクを作成メッセージ領域に貼り付けることにより)、検索の結果をメッセージに挿入できます。 最も基本的な検索コマンドフローでは、最初の呼び出しメッセージに、ユーザーが送信した検索文字列が含まれます。 カードとカードのプレビューの一覧を返信します。 Teams クライアントは、エンドユーザーが選択するカードのプレビューを一覧で表示します。 ユーザーがカードを選択すると、フルサイズのカードが [メッセージの作成] 領域に挿入されます。

これらは、[メッセージの作成] 領域またはコマンドボックスから起動できます。 アクションコマンドとは異なり、メッセージからトリガーすることはできません。

![メッセージング拡張機能検索コマンド](~/assets/images/search-extension.png)

### <a name="link-unfurling"></a>Link unfurling

また、[メッセージの作成] 領域に URL が貼り付けられたときに、サービスを呼び出すこともできます。 この機能 ( **link unfurling**と呼ばれる) を使用すると、特定のドメインを含む url が [メッセージの作成] 領域に貼り付けられたときに呼び出しを受信するようにサブスクライブできます。 Web サービスは、URL を詳細なカードに "アン url" して、標準の web サイトプレビューカードより多くの情報を提供することができます。 ボタンを追加して、ユーザーが Microsoft Teams クライアントを離れることなく、すぐにアクションを実行できるようにすることもできます。

## <a name="get-started"></a>作業の開始

構築を開始する準備ができましたか? クイックスタートのいずれかをお試しください。

* C のクイックスタート#
  * [アクションベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [検索ベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* JavaScript のクイックスタート
  * [アクションベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [検索ベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

## <a name="learn-more"></a>詳細情報

メッセージング拡張機能を構築します。

* [メッセージング拡張機能を作成する](~/messaging-extensions/how-to/create-messaging-extension.md)
* [アクションメッセージング拡張コマンドの定義](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [検索メッセージ拡張コマンドの定義](~/messaging-extensions/how-to/search-commands/define-search-command.md)
