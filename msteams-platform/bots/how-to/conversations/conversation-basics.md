---
title: 会話の基本
description: このモジュールでは、Teamsのチャネル、個人用チャット、およびグループ チャット環境でのボットの会話について説明します。
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 682555cadaeca5f50a942de98b2dcdd85ce0f6b2
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142921"
---
# <a name="conversation-basics"></a>会話の基本

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

会話は、Microsoft Teams ボットと 1 人以上のユーザーの間で送信される一連のメッセージです。 次の表に、Teamsのスコープとも呼ばれる 3 種類の会話を示します。

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

ボット会話内の各メッセージは、型`messageType: message`の`Activity`オブジェクトです。 ユーザーがメッセージを送信すると、Teamsメッセージがボットに投稿され、ボットによってメッセージが処理されます。 さらに、ボットが応答するコア コマンドを定義するために、ボットのコマンドのドロップダウン リストを含むコマンド メニューを追加できます。 グループまたはチャネル内のボットは、@botnameに言及された場合にのみメッセージを受信します。 Teams はボットがアクティブな範囲で発生する会話イベントの通知をボットに送ります。 これらのイベントは、コード内でキャプチャし、それらに対してアクションを実行できます。

ボットは、プロアクティブ メッセージをユーザーに送信することもできます。 プロアクティブ メッセージとは、ユーザーからの要求に応答していないボットから送信されたメッセージのことです。 ボット メッセージを書式設定して、ボタン、テキスト、画像、オーディオ、ビデオなどの対話型要素を含むリッチ カードを含めることができます。 ボットは、メッセージをデータの静的スナップショットとして保持するのではなく、メッセージを送信した後に動的に更新できます。 メッセージは、Bot Framework の `DeleteActivity` メソッドを使用して削除することもできます。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [ボットの会話内のメッセージ](~/bots/how-to/conversations/conversation-messages.md)
