---
title: 会議チャット用の拡張可能な会話を構築する
author: v-sdhakshina
description: この記事では、ボット、カード、メッセージ拡張機能を使用して Microsoft Teams 会議チャットの拡張可能な会話を構築する方法について説明します。
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: 65fc91d51cd4c740f28d5f33a2ad578f214c20a8
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615447"
---
# <a name="build-extensible-conversation-for-meeting-chat"></a>会議チャット用の拡張可能な会話を構築する

Microsoft Teams 会議では、会話を拡張可能にすることができます。 ボット、メッセージ拡張機能、カード、タスク モジュールを組み合わせて、直感的なエクスペリエンスを提供できます。

## <a name="bots"></a>ボット

ボットは、チャットボットまたは会話ボットとも呼ばれます。 これは、カスタマー サービスやサポート スタッフなどのユーザーが単純で反復的なタスクを実行するアプリです。 ボットの日常的な使用には、天気に関する情報を提供するボット、ディナーの予約を行うボット、旅行情報を提供するボットなどがあります。 ボットとのやり取りは、質問や回答を素早く行ったり、複雑な会話になったりする場合があります。 チャネル会議のスコープと、他のすべての会議の種類のスコープで `team` ボットを `groupchat` 有効にする必要があります。 ボットを実装するには、まず [ボットのビルドから始めます](/microsoftteams/platform//sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode)。

### <a name="bot-apis"></a>ボット API

[Bot Framework](https://dev.botframework.com/) は、C#、Java、Python、JavaScript を使用してボットを作成するために使用される豊富な SDK です。 Bot Framework に基づくボットが既にある場合は、Teams で動作するようにボットを簡単に変更できます。 用意されている [SDK](/microsoftteams/platform/) を活用するため、C# か Node.js を使用してください。

### <a name="code-samples---bots"></a>コード サンプル - ボット

|サンプルの名前 | 説明 | .NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|
| Teams 会話ボット | メッセージングと会話イベントの処理 | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |
|ボット サンプル | ボット サンプルのセット  | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python) |

## <a name="message-extensions"></a>メッセージ拡張機能

メッセージ拡張機能を使用すると、ユーザーは Teams クライアントのボタンやフォームを使用して Web サービスを操作できます。 ユーザーは、メッセージ作成領域、コマンド ボックス、またはメッセージから直接、外部システムでアクションを検索または開始できます。 その操作の結果は、豊富な形式のカードの形式で Teams クライアントに返送できます。 会議チャットのメッセージ拡張機能の実装は、通常のチャットと変われません。 メッセージ拡張機能を実装するには、 [まずメッセージ拡張機能](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions?tabs=dotnet)から始めます。

## <a name="cards-and-task-modules"></a>カードとタスク モジュール

カードは、ユーザーにさまざまな視覚、音声、選択可能なメッセージを提供し、会話フローに役立ちます。 タスク モジュールを使用すると、Teams でモーダル ポップアップ エクスペリエンスを作成できます。 タスクの開始と完了、ビデオや Power Business Intelligence (BI) ダッシュボードなどの豊富な情報の表示に役立ちます。 詳細については、 [カードとタスク モジュールの構築に関](/microsoftteams/platform/task-modules-and-cards/cards-and-task-modules)するページを参照してください。

## <a name="feature-compatibility-by-user-types"></a>ユーザーの種類別の機能の互換性

次の表に、ユーザーの種類と、各ユーザーが会議でアクセスできる機能の一覧を示します。

| ユーザーの種類 | ボット | メッセージ拡張機能 | アダプティブ カード | タスク モジュール |
| :-- | :-- | :-- | :-- | :-- |
| テナント内ユーザー | 使用可能 | 使用可能 | 使用可能 | 使用可能 |
| テナント Azure AD の一部であるゲスト | 使用不可 | 使用不可 | 会議チャットでの対話は許可されます。 | アダプティブ カードからの会議チャットでの対話は許可されます。 |
| フェデレーション ユーザーの詳細については、 [非標準ユーザーを](/microsoftteams/non-standard-users)参照してください。 | 対話は許可されます。 取得、更新、削除は許可されません。 | 使用不可 | 会議チャットでの対話は許可されます。 | アダプティブ カードからの会議チャットでの対話は許可されます。 |
| 匿名ユーザー | 使用不可 | 使用不可 | 会議チャットでの対話は許可されます。 | 使用不可 |

## <a name="see-also"></a>関連項目

* [Microsoft Teams メッセージ拡張機能のデザイン](../messaging-extensions/design/messaging-extension-design.md)
* [Microsoft Teams のアプリのタスク モジュールの設計](../task-modules-and-cards/task-modules/design-teams-task-modules.md)
