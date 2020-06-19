---
title: ボットを使用した1対1の会話
description: Microsoft Teams で bot との1対1の会話を行うエンドツーエンドのシナリオについて説明します。
keywords: teams シナリオ1on1to1 会話 bot
ms.date: 05/20/2019
ms.openlocfilehash: e23bb98160125d7fdbb4521467e2f522d6b6ce40
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801241"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Microsoft Teams bot との個人的な (1 対 1) 会話がある

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams を使用すると、ユーザーは、 [Microsoft Bot フレームワーク](/azure/bot-service/?view=azure-bot-service-3.0)上に構築された bot と直接会話することができます。 ユーザーは、[アプリの検索] ギャラリーでボットを検索して、個人の会話に備えて Teams の機能に追加することができます。 チームの所有者と適切なアクセス許可を持つユーザーは、チームのメンバーとして bot を追加することもできます (「[チームチャネルでの対話](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)」を参照)。これは、チームのチャネルで利用できるようにするだけでなく、すべてのユーザーに対して個人用チャットを行うためにも使用できます。

個人チャットは、ユーザーが bot を @mention する必要がないという点で、チャネルでのチャットとは異なります。 Bot が複数のコンテキスト (personal、groupChat または channel) で使用されている場合は、bot がグループチャットまたはチャネル内にあるかどうかを検出し、メッセージを少し異なる方法で処理する必要があります。 詳細について[は、「チームチャネルまたはグループチャットで対話する](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)」を参照してください。

## <a name="designing-a-great-personal-bot"></a>大個人 bot の設計

Microsoft Teams の大部分では、ユーザーが必要とする情報を Teams の環境のコンテキスト内で取得することができます。 Bot との個人的な会話は、ボットとそのユーザーの間のプライベートなやりとりです。個人のコンテキストでそのユーザーに固有で、関連する情報を提供するための最適な方法です。 個人チャットのボットは、実際にはサービスと個人の間でのダイアログです。グループチャットまたはチャネル内の bot は、すべてをユーザーのグループにブロードキャストします。

作成する操作によっては、bot が複数のスコープで作業する必要があります-personal、groupChat、または teams。 複数のスコープをサポートする作業は最小限に抑えられます。 Teams では、すべてのスコープにおいて bot が機能するとは想定されていませんが、ボットが意味を持ち、サポートする任意の範囲でユーザー値を提供するようにしてください。

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>ベストプラクティス: 個人の会話でのウェルカムメッセージ

Bot は、初めて、ユーザーが自分の bot との個人チャットを開始するために、最初に開始メッセージを個人チャットに[事前に送信](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)する必要があります。 (この推奨事項は、チャネルの最初の時点の連絡先には適用されません)。
