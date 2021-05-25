---
title: 会話の基本
description: 会話の概要
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: conversations basics messages
ms.openlocfilehash: a0c00d093827221968714aad88c35efa00660d82
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630986"
---
# <a name="conversation-basics"></a>会話の基本

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

会話とは、ボットと 1 人または複数のユーザー Microsoft Teams送信される一連のメッセージです。 次の表に、次の 3 種類の会話 (スコープとも呼ばれる) を示Teams。

| 会話の種類 | 説明 |
| ------- | ----------- |
| `channel` | この会話の種類は、チャネルのすべてのメンバーに表示されます。 |
| `personal` | この会話の種類には、ボットと 1 人のユーザーとの会話が含まれます。 |
| `groupChat` | この会話の種類には、ボットと 2 人以上のユーザーの間のチャットが含まれます。 また、会議チャットでボットを有効にできます。 |

ボットの動作は、関連する会話に応じて異なります。

* チャネル内やグループ チャット内の会話の場合、ユーザーはボットを @メンションしてチャネルに呼び出す必要があります。

* 1 対 1 の会話のボットでは、1 対 1 の@mention。 ユーザーが送信したメッセージはすべてボットにルーティングされます。

> [!NOTE]
> ボットは、リソース固有の同意 (RSC) アクセス許可を使用@mentioned、チーム内のすべてのチャネル メッセージを受信できます。 この機能は現在、パブリック開発者 [プレビューでのみ利用](../../../resources/dev-preview/developer-preview-intro.md) できます。 詳細については [、「RSC を使用してすべてのチャネル メッセージを受信する」を参照してください](channel-messages-with-rsc.md)。

ボットが特定の会話またはスコープで動作するには、アプリ マニフェストのそのスコープにサポートを [追加します](~/resources/schema/manifest-schema.md)。

ボット会話の各メッセージは、 `Activity` 型のオブジェクトです `messageType: message` 。 ユーザーがメッセージを送信するとTeamsボットにメッセージが投稿され、ボットがメッセージを処理します。 さらに、ボットが応答するコア コマンドを定義するには、ボットのコマンドのドロップダウン リストを含むコマンド メニューを追加できます。 グループまたはチャネル内のボットは、グループまたはチャネルに関する情報が記載されている場合にのみ@botname。 Teamsボットがアクティブなスコープで発生する会話イベントの通知をボットに送信します。 これらのイベントをコードでキャプチャし、アクションを実行できます。

ボットは、ユーザーにプロアクティブ メッセージを送信することもできます。 プロアクティブ メッセージとは、ユーザーからの要求に応答しないボットから送信されるメッセージです。 ボタン、テキスト、画像、オーディオ、ビデオなどの対話型要素を含むリッチ カードをボット メッセージに書式設定できます。 ボットは、メッセージをデータの静的スナップショットとしてではなく、送信後に動的に更新できます。 ボット フレームワークのメソッドを使用してメッセージを削除 `DeleteActivity` することもできます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ボットの会話内のメッセージ](~/bots/how-to/conversations/conversation-messages.md)
