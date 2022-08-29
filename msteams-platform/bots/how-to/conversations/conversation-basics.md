---
title: 会話の基本
description: このモジュールでは、Microsoft Teams のチャネル、個人用チャット、およびグループ チャット スコープのボット会話の種類について説明します。
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 23a72486ffb76d207eeabbef23b5ec5238234dc4
ms.sourcegitcommit: b918181217995a47be34632e1051d0f4d4d481b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2022
ms.locfileid: "67321216"
---
# <a name="conversation-basics"></a>会話の基本

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

会話とは、Microsoft Teams ボットと 1 人以上のユーザーの間で送信される一連のメッセージです。 次の表に、Teams のスコープとも呼ばれる 3 種類の会話を示します。

| 会話の種類 | 説明 |
| ------- | ----------- |
| `channel` | この会話の種類は、チャネルのすべてのメンバーに表示されます。 |
| `personal` | この会話の種類には、ボットと 1 人のユーザー間の会話が含まれます。 |
| `groupChat` | この会話の種類には、ボットと 2 人以上のユーザー間のチャットが含まれます。 また、会議チャットでもボットを有効にします。 |

ボットの動作は、ボットが関係する会話によって異なります。

* チャネル内やグループ チャット内の会話の場合、ユーザーはボットを @メンションしてチャネルに呼び出す必要があります。

* 1 対 1 の会話のボットには、@mentionは必要ありません。 ユーザーによって送信されたすべてのメッセージは、ボットにルーティングされます。

> [!NOTE]
> ボットを有効にすると、リソース固有の同意 (RSC) アクセス許可を使用して@mentionedすることなく、チーム内のすべてのチャネル メッセージを受信できます。 この機能は現在、 [パブリック開発者向けプレビュー](../../../resources/dev-preview/developer-preview-intro.md) でのみ使用できます。 詳細については、「 [RSC を使用してすべてのチャネル メッセージを受信する](channel-messages-with-rsc.md)」を参照してください。

ボットが特定の会話またはスコープで動作するには、 [アプリ マニフェスト](~/resources/schema/manifest-schema.md)でそのスコープにサポートを追加します。

ボット会話内の各メッセージは、型`messageType: message`の`Activity`オブジェクトです。 ユーザーがメッセージを送信すると、Teams はメッセージをボットに投稿し、ボットはメッセージを処理します。 さらに、ボットが応答するコア コマンドを定義するために、ボットのコマンドのドロップダウン リストを含むコマンド メニューを追加できます。 グループまたはチャネル内のボットは、@botnameに言及された場合にのみメッセージを受信します。 Teams はボットがアクティブな範囲で発生する会話イベントの通知をボットに送ります。 これらのイベントは、コード内でキャプチャし、それらに対してアクションを実行できます。

ボットは、プロアクティブ メッセージをユーザーに送信することもできます。 プロアクティブ メッセージとは、ユーザーからの要求に応答していないボットから送信されたメッセージのことです。 ボット メッセージを書式設定して、ボタン、テキスト、画像、オーディオ、ビデオなどの対話型要素を含むリッチ カードを含めることができます。 ボットは、メッセージをデータの静的スナップショットとして保持するのではなく、メッセージを送信した後に動的に更新できます。 メッセージは、Bot Framework の `DeleteActivity` メソッドを使用して削除することもできます。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [ボットの会話内のメッセージ](~/bots/how-to/conversations/conversation-messages.md)
