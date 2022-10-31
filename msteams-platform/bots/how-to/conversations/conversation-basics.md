---
title: 会話の基本
description: このモジュールでは、Microsoft Teams のチャネル、個人用チャット、グループ チャット スコープのボット会話の種類について説明します。
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: ab27bc6000712cd046d92d9e020bfbe8fa65daa0
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791819"
---
# <a name="conversation-basics"></a>会話の基本

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

会話とは、Microsoft Teams ボットと 1 人以上のユーザーの間で送信される一連のメッセージです。 次の表に、Teams のスコープとも呼ばれる 3 種類の会話を示します。

| 会話の種類 | 説明 |
| ------- | ----------- |
| `channel` | この会話の種類は、チャネルのすべてのメンバーに表示されます。 |
| `personal` | この会話の種類には、ボットと 1 人のユーザー間の会話が含まれます。 |
| `groupChat` | この会話の種類には、ボットと 2 人以上のユーザー間のチャットが含まれます。 また、会議チャットでボットを有効にすることもできます。 |

ボットは、関係する会話に応じて動作が異なります。

* チャネル内やグループ チャット内の会話の場合、ユーザーはボットを @メンションしてチャネルに呼び出す必要があります。

* 1 対 1 の会話の場合、ボットを @メンションする必要はありません。 ユーザーによって送信されたすべてのメッセージは、ボットにルーティングされます。

> [!NOTE]
> ボットを有効にすると、リソース固有の同意 (RSC) アクセス許可を使用して@mentionedされることなく、チーム内のすべてのチャネル メッセージを受信できます。 この機能は現在、 [パブリック開発者プレビュー](../../../resources/dev-preview/developer-preview-intro.md) でのみ使用できます。 詳細については、「 [RSC を使用してすべてのチャネル メッセージを受信する](channel-messages-with-rsc.md)」を参照してください。

ボットが特定の会話またはスコープで動作するには、 [アプリ マニフェスト](~/resources/schema/manifest-schema.md)でそのスコープにサポートを追加します。

ボット会話内の各メッセージは、 `Activity` 型 `messageType: message`のオブジェクトです。 ユーザーがメッセージを送信すると、Teams によってボットにメッセージが投稿され、ボットによってメッセージが処理されます。 さらに、ボットが応答するコア コマンドを定義するには、ボットのコマンドのドロップダウン リストを含むコマンド メニューを追加できます。 グループまたはチャネル内のボットは、@botnameメンションされたときにのみメッセージを受信します。 Teams はボットがアクティブな範囲で発生する会話イベントの通知をボットに送ります。 コードでこれらのイベントをキャプチャし、それらに対してアクションを実行できます。

ボットは、プロアクティブ メッセージをユーザーに送信することもできます。 プロアクティブ メッセージとは、ユーザーからのリクエストに応答しないボットによって送信されるメッセージのことです。 ボット メッセージを書式設定して、ボタン、テキスト、画像、オーディオ、ビデオなどの対話型要素を含むリッチ カードを含めることができます。 ボットは、メッセージをデータの静的スナップショットとして使用するのではなく、送信後にメッセージを動的に更新できます。 メッセージは、Bot Framework の `DeleteActivity` メソッドを使用して削除することもできます。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [ボットの会話内のメッセージ](~/bots/how-to/conversations/conversation-messages.md)
