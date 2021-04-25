---
title: 会話の基本
description: 会話の概要
ms.topic: overview
ms.author: anclear
keyword: conversations basics messages
ms.openlocfilehash: eff1c6fe18f7b2ba082b5075b6c1806f41b68a6b
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2021
ms.locfileid: "51996038"
---
# <a name="conversation-basics"></a>会話の基本

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

会話とは、Microsoft Teams ボットと 1 人または複数のユーザーの間で送信される一連のメッセージです。 次の表に、Teams のスコープとも呼ばれる 3 種類の会話を示します。

| 会話の種類 | 説明 |
| ------- | ----------- |
| `channel` | この会話の種類は、チャネルのすべてのメンバーに表示されます。 |
| `personal` | この会話の種類には、ボットと 1 人のユーザーとの会話が含まれます。 |
| `groupChat` | この会話の種類には、ボットと 2 人以上のユーザーの間のチャットが含まれます。 また、会議チャットでボットを有効にできます。 |

ボットの動作は、関連する会話に応じて異なります。

* チャネルチャットとグループ チャット会話のボットでは、チャネルでボットを呼び出す場合は、ユーザーがボットに @メンションする必要があります。
* 1 対 1 の会話のボットでは@メンションは必要ない。 ユーザーが送信したメッセージはすべてボットにルーティングされます。

ボットが特定の会話またはスコープで動作するには、アプリ マニフェストのそのスコープにサポートを [追加します](~/resources/schema/manifest-schema.md)。

ボット会話の各メッセージは、 `Activity` 型のオブジェクトです `messageType: message` 。 ユーザーがメッセージを送信すると、Teams はメッセージをボットに投稿し、ボットはメッセージを処理します。 さらに、ボットが応答するコア コマンドを定義するには、ボットのコマンドのドロップダウン リストを含むコマンド メニューを追加できます。 グループまたはチャネル内のボットは、グループまたはチャネルに関する情報が記載されている場合にのみ@botname。 Teams は、ボットがアクティブなスコープで発生する会話イベントの通知をボットに送信します。 これらのイベントをコードでキャプチャし、アクションを実行できます。 

ボットは、ユーザーにプロアクティブ メッセージを送信することもできます。 プロアクティブ メッセージとは、ユーザーからの要求に応答しないボットから送信されるメッセージです。 ボタン、テキスト、画像、オーディオ、ビデオなどの対話型要素を含むリッチ カードをボット メッセージに書式設定できます。 ボットは、メッセージをデータの静的スナップショットとしてではなく、送信後に動的に更新できます。 ボット フレームワークのメソッドを使用してメッセージを削除 `DeleteActivity` することもできます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ボットの会話内のメッセージ](~/bots/how-to/conversations/conversation-messages.md)
