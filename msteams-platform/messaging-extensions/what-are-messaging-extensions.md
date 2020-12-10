---
title: メッセージング拡張機能について
author: clearab
description: Microsoft Teams プラットフォームでのメッセージング拡張機能の概要
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3ea9649a22ecc134e983037d1ef109be918a26b3
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587798"
---
# <a name="what-are-messaging-extensions"></a>メッセージング拡張機能について

メッセージング拡張機能では、ユーザーは、Microsoft Teams クライアントのボタンとフォームを使用して Web サービスを操作することができます。 ユーザーは、外部システムのメッセージ作成領域、コマンド ボックスから、またはメッセージから直接、操作を検索したり、開始したりできます。 その操作の結果を、通常はリッチに書式設定されたカードとして Microsoft Teams クライアントに送信できます。

次のスクリーンショットは、メッセージング拡張機能を呼び出すことができる場所を示しています。

![メッセージング拡張機能の呼び出し場所](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="what-kinds-of-tasks-are-they-good-for"></a>どんなタスクに向いていますか?

**シナリオ:** 何かを行うために外部システムが必要で、その操作の結果を自分の会話に送り返したい。\
**例:** リソースを予約して、何曜日/何時に予約したかをチャネルに知らせる。

**シナリオ:** 外部システムで何かを見つける必要があり、その結果を自分の会話と共有したい。\
**例:** Azure DevOps で作業項目を検索し、アダプティブ カードとしてグループと共有する。

**シナリオ:** 外部システムで複数の手順 (または多くの情報) を含む複雑なタスクを完了させる必要があり、その結果を会話で共有する必要がある。
**例:** Teams のメッセージに基づいてトラッキング システムにバグを作成し、そのバグを Bob に割り当て、そのバグの詳細情報が記載されたカードを会話スレッドに送信する。

## <a name="how-do-messaging-extensions-work"></a>メッセージング拡張機能の仕組み

メッセージング拡張機能は、ホストする Web サービスとアプリのマニフェストによって構成されています。このマニフェストによって、Microsoft Teams クライアントから Web サービスを呼び出せる場所を定義します。 これらは Bot Framework のメッセージング スキーマとセキュリティで保護された通信プロトコルを利用するので、Web サービスを Bot Framework でボットとして登録する必要もあります。 Web サービスを完全に手動で作成することもできますが、[Bot Framework SDK](https://github.com/microsoft/botframework) を活用してプロトコルをより簡単に操作できるようにすることをお勧めします。

Microsoft Teams アプリのアプリ マニフェストでは、最大 10 種類の異なるコマンドを使用して 1 つのメッセージング拡張機能を定義します。 それぞれのコマンドは、種類 (アクションや検索) と、それが呼び出されるクライアント内の場所 (メッセージ作成領域、コマンド バー、および/またはメッセージ) を定義します。 呼び出されると、Web サービスは、すべての関連情報を持つ JSON ペイロードを含む HTTPS メッセージを受信します。 JSON ペイロードを使用して応答し、次にどのような操作を有効にするかを Teams クライアントに知らせます。

## <a name="types-of-messaging-extension-commands"></a>メッセージング拡張機能のコマンドの種類

メッセージング拡張機能のコマンドの種類は、Web サービスで利用可能な UI 要素と操作フローを定義します。 認証や構成のような一部の操作は、どちらの種類のコマンドでも利用可能です。

### <a name="action-commands"></a>操作コマンド

操作コマンドでは、情報を収集または表示するためのモーダル ポップアップをユーザーに表示できます。 ユーザーがフォームを送信すると、Web サービスはメッセージを会話に直接挿入するか、またはメッセージ作成領域にメッセージを挿入し、ユーザーがメッセージを送信できるようにすることで応答します。 複数のフォームをチェーン化して、より複雑なワークフローを実現することもできます。

操作コマンドは、メッセージ作成領域、コマンド ボックス、またはメッセージからトリガーできます。 メッセージから呼び出す場合、ボットに送信される最初の JSON ペイロードには、呼び出されたメッセージ全体が含まれます。

![メッセージング拡張機能アクション コマンド タスク モジュール](~/assets/images/task-module.png)

### <a name="search-commands"></a>検索コマンド

検索コマンドを使用すると、ユーザーは (検索ボックスを使用して手動で、または監視対象ドメインへのリンクをメッセージ作成領域に貼り付けて) 外部システムの情報を検索し、検索結果をメッセージに挿入できます。 最も基本的な検索コマンドのフローでは、ユーザーが送信した検索文字列が最初の呼び出しメッセージに含まれています。 カードの一覧とカードのプレビューで応答します。 Teams クライアントは、カードのプレビューを一覧に表示して、エンド ユーザーが選択できるようにします。 ユーザーがカードを選択すると、フルサイズのカードがメッセージ作成領域に挿入されます。

検索コマンドは、メッセージ作成領域またはコマンド ボックスからトリガーできます。 アクション コマンドとは異なり、メッセージからトリガーすることはできません。

![メッセージング拡張機能の検索コマンド](~/assets/images/search-extension.png)

### <a name="link-unfurling"></a>リンク展開

また、メッセージ作成領域に URL が貼り付けられたときにサービスを呼び出すオプションもあります。 この機能は **リンク展開** として知られており、特定のドメインを含む URL がメッセージ作成領域に貼り付けられたときに、登録して呼び出しを受け取ることができます。 お客様の Web サービスは、URL を詳細情報が記載されたカードに "展開" することができ、そのカードでは標準的な Web サイトのプレビュー カードよりも多くの情報を提供できます。 また、ボタンを追加して、ユーザーが Microsoft Teams クライアントから離脱することなくすぐにアクションを起こせるようにすることもできます。

## <a name="get-started"></a>使用を開始する

作成を始める準備はできましたか? 次のクイックスタートのいずれかをお試しください。

* **C#**
  * [アクションベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [検索ベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* **JavaScript**
  * [アクションベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [検索ベースのコマンドを使用したメッセージング拡張機能](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

## <a name="learn-more"></a>詳細情報

メッセージング拡張機能を作成する:

* [メッセージング拡張機能を作成する](~/messaging-extensions/how-to/create-messaging-extension.md)
* [アクション メッセージング拡張機能のコマンドを定義する](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [検索メッセージング拡張機能のコマンドを定義する](~/messaging-extensions/how-to/search-commands/define-search-command.md)
