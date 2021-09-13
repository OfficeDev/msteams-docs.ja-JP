---
title: ボットとの 1 対 1 の会話
description: ボットと 1 対 1 の会話を行うというエンドツーエンドのシナリオについて説明Microsoft Teams
keywords: teams シナリオ 1on1 1to1 会話ボット
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: 2fd76b8bc5fa4cd260b70e15b92bef2dec2de683
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156110"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>ユーザーボットと個人的な (1 対 1 の) 会話Microsoft Teamsする

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teamsを使用すると、ユーザーは、アプリに基[Microsoft Bot Framework。](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) ユーザーは、[アプリの検出] ギャラリーでボットを見つけて、Teamsのエクスペリエンスに追加できます。 適切なアクセス許可を持つチーム所有者とユーザーは、チーム メンバーとしてボットを追加できます。 詳細については、「チーム チャネルの [Interact」](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)を参照してください。これは、チームのチャネルで利用できるだけでなく、すべてのユーザーに対する個人用チャットにも使用できます。

個人用チャットは、ユーザーがボットにアクセスする必要が@mention異なります。 ボットが個人用、groupChat、チャネルなどの複数のコンテキストで使用されている場合は、ボットがグループ チャットまたはチャネル内にあるか検出し、メッセージを少し異なる方法で処理する必要があります。 詳細については、「チーム チャネルまたは [グループ チャットでの Interact」を参照してください](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。

## <a name="designing-a-great-personal-bot"></a>偉大な個人ボットの設計

ユーザーが必要なMicrosoft Teams、ユーザーエクスペリエンスのコンテキスト内で、ユーザーが必要な情報をTeamsできます。 ボットとの個人的な会話は、ボットとそのユーザー間のプライベートなやり取りです。個人のコンテキストで、そのユーザーに固有で関連性の高い情報を提供する最適な方法です。 個人用チャット内のボットは、実際にはサービスと個人の間のダイアログであり、グループ チャットまたはチャネル内のボットがグループのユーザーにすべてをブロードキャストします。

作成するエクスペリエンスによっては、ボットが複数のスコープ (個人用、グループチャット、チーム) で作業する必要がある場合があります。 複数のスコープをサポートする作業は最小限です。 Teams では、ボットがすべてのスコープで機能するとは思ってはいありませんが、ボットが意味を持ち、サポートするスコープでユーザー値を提供する必要があります。

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>ベスト プラクティス: 個人的な会話でのウェルカム メッセージ

ボットは、 [ユーザー](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) がボットとの個人用チャットを初めて (初めて) 開始する場合にのみ、事前にウェルカム メッセージを個人チャットに送信する必要があります。 この推奨事項は、チャネルの初回連絡先には適用されません。
