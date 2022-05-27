---
title: カードとタスク モジュール
description: アダプティブ カード、ヒーロー カード、サムネイル カードなど、Teams用のボットでサポートされているカードの種類について説明します。 カード アクションと、チャネル、ボット、またはディープ リンクでのタスク モジュールの呼び出しについて説明します。
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: d68e45608d445e30a4d6b5ea8f5b662cfc22b116
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756577"
---
# <a name="cards-and-task-modules"></a>カードとタスク モジュール

カードは、ユーザーにさまざまな視覚、音声、選択可能なメッセージを提供し、会話フローに役立ちます。

タスク モジュールを使用すると、Microsoft Teamsでモーダル ポップアップ エクスペリエンスを作成できます。 タスクの開始と完了、ビデオや Power Business Intelligence (BI) ダッシュボードなどの豊富な情報の表示に役立ちます。

Teamsのボットでは、次の種類のカードがサポートされています。

* アダプティブ カード
* ヒーロー カード
* リスト カード
* Office 365 コネクタ カード
* レシート カード
* サインイン カード
* サムネイル カード
* カード コレクション

カードの種類に応じて、XML または HTML の書式設定または Markdown のサブセットを使用して、カード テキストを書式設定できます。

アダプティブ [カードのアダプティブ カードのユーザー選択ツール](cards/people-picker.md)は、チャットまたはチャネル内のユーザーを検索、選択、再割り当て、事前選択するのに役立ちます。

次のカード アクションを追加して応答できます。

* URL を開く
* メッセージとペイロードをボットに送信する
* OAuth フローを開始する

アダプティブ カードの先行入力コントロールを使用して大規模なデータセット内で [動的な検索](~/task-modules-and-cards/cards/dynamic-search.md) エクスペリエンスを提供し、選択肢の数に制限がある範囲内で先行型静的検索を実行できます。 チャネルまたは個人用タブ、ボット、またはディープ リンクでタスク モジュールを呼び出します。 ユーザーのタブにタスク モジュールを追加することで、データ入力を必要とするワークフローに対するユーザーエクスペリエンスを向上させることができます。アダプティブ カードと Bot Framework カードのボタンを使用して、Teams ボットからタスク モジュールを呼び出すことができます。

## <a name="see-also"></a>関連項目

* [カード](~/task-modules-and-cards/what-are-cards.md)
* [タスク モジュール](~/task-modules-and-cards/what-are-task-modules.md)
