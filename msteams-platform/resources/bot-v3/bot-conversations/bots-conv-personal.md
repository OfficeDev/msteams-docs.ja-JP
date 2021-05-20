---
title: ボットとの 1 対 1 の会話
description: Microsoft Teamsでボットと 1 対 1 の会話を行うエンド ツー エンドのシナリオについて説明Microsoft Teams
keywords: チームシナリオ 1on1 1to1 会話ボット
localization_priority: Normal
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: dff65e919485eff0443032995b934b7ae93c64eb
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566503"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Microsoft Teamsボットとの個人的な (1 対 1) の会話をする

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams、ユーザーは[Microsoft Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true)上に構築されたボットと直接会話をすることができます。 ユーザーは、アプリの検出ギャラリーでボットを見つけ、個人的な会話のためにTeamsエクスペリエンスに追加できます。 チームの所有者と適切なアクセス許可を持つユーザーは、チーム メンバーとしてボットを追加することもできます。 詳細については、「チーム [チャネルで対話](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)する」を参照してください。

ユーザーがボットを@mentionする必要がなされないという点で、チャットとチャンネルのチャットが異なります。 ボットが個人、groupChat、チャンネルなどの複数のコンテキストで使用されている場合、ボットがグループチャットまたはチャンネル内にあるかどうかを検出し、メッセージの処理方法が少し異なる必要があります。 詳細については、「 [チーム チャネルまたはグループ チャットで対話](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)する 」を参照してください。

## <a name="designing-a-great-personal-bot"></a>優れたパーソナルボットの設計

Microsoft Teamsの優れたボットは、ユーザーがTeamsエクスペリエンスのコンテキスト内で必要な情報を取得するのに役立ちます。 ボットとの個人的な会話は、ボットとそのユーザーとの間のプライベートなやり取りです。個人コンテキストで、そのユーザーに固有で関連性のある情報を提供する優れた方法です。 パーソナルチャットのボットは、実際にはサービスと個人の間のダイアログで、グループチャットやチャンネルのボットがすべてをグループの人々にブロードキャストします。

作成するエクスペリエンスによっては、ボットが複数のスコープ (パーソナル、グループチャット、チーム) で作業する必要がある場合があります。 複数のスコープをサポートする作業は最小限です。 Teamsでは、すべてのスコープでボットが機能するとは期待できませんが、ボットが意味を持ち、サポートするスコープでユーザー価値を提供することを確認する必要があります。

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>ベスト プラクティス: 個人的な会話のウェルカム メッセージ

ボットは、ユーザーがボットとのパーソナル チャットを開始した場合に初めて (初めて) 個人用チャットにウェルカム メッセージを [積極的に送信](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) する必要があります。 この推奨事項は、チャネル内の初回の連絡先には適用されません。
