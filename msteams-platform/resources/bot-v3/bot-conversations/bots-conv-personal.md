---
title: ボットとの 1 対 1 の会話
description: このモジュールでは、Microsoft Teamsでボットと 1 対 1 の会話を行うエンドツーエンドのシナリオについて説明します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: e973e335558a54187a11d5146b52c5774d3cf758
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144328"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Microsoft Teams ボットで個人 (1 対 1) の会話を行う

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teamsを使用すると、ユーザーは [Microsoft Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) に基づいて構築されたボットと直接会話できます。 ユーザーは、Discover Apps ギャラリーでボットを見つけて、個人的な会話用に Teams エクスペリエンスに追加できます。 適切なアクセス許可を持つチームの所有者とユーザーは、チーム メンバーとしてボットを追加することもできます。 詳細については、「[チーム チャネルでの対話](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)」を参照してください。これにより、チームのチャネルで利用できるだけでなく、個人用チャット ユーザーにも利用できるようになります。

個人用チャットは、ユーザーがボットを @mention する必要がないという点で、チャネル内のチャットとは異なります。 ボットが次のスコープなどの複数のコンテキストで使用されている場合:
* 個人
* グループ チャット
* チャネル

ボットがグループ チャットまたはチャネル内にあるかどうかを検出し、メッセージを少し異なる方法で処理する必要があります。 詳細については、「[チーム チャネルまたはグループ チャットでの対話](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」を参照してください。

## <a name="designing-a-great-personal-bot"></a>優れた個人用ボットの設計

Microsoft Teams の優れたボットは、ユーザーがTeams エクスペリエンスのコンテキスト内で必要な情報を取得するのに役立ちます。 ボットとの個人的な会話は、ボットとそのユーザー間のプライベートなやり取りです。これらは、個人的のコンテキストでそのユーザーに固有かつ関連性のある情報を提供する優れた方法です。 個人用チャットのボットは、サービスと個人の間のダイアログであり、グループ チャットまたはチャネル内のボットがすべてをユーザーのグループにブロードキャストします。

作成するエクスペリエンスによっては、ボットが複数のスコープ (個人用、グループ チャット、チーム) で作業する必要がある場合があります。 複数のスコープをサポートする作業は最小限になっています。 Teams では、ボットがすべてのスコープで機能することを期待していませんが、サポートするスコープが何であれ、ボットが意味を持ち、ユーザーに価値を提供することを確認する必要があります。

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>ベスト プラクティス: Teams でのウェルカム メッセージ

ボットは、ユーザーがボットとの個人用チャットを初めて開始する (初めての時のみ) パーソナル チャットにウェルカム メッセージを [プロアクティブに送信](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) する必要があります。 この推奨事項は、チャネル内の初めての連絡先には適用されません。
