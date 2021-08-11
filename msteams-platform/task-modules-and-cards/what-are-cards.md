---
title: カード
description: カードと、ボット、コネクタ、メッセージング拡張機能でのカードの使い方について説明します。
localization_priority: Normal
keywords: コネクタ ボット カード メッセージング
ms.topic: overview
ms.openlocfilehash: 5fce5983e5197bfde37d2c92d427e8135b294d422eb019ef207eeb7f0e5be9f3
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57706633"
---
# <a name="cards"></a>カード

カードは、短い情報や関連する情報のユーザー インターフェイス (UI) コンテナーです。 カードには複数のプロパティと添付ファイルを含め、ボタンを含め、カードアクション [をトリガーできます](~/task-modules-and-cards/cards/cards-actions.md)。 カードを使用して、情報をグループに整理し、ユーザーに情報の特定の部分を操作する機会を与える。

Teams のボットは、アダプティブ カード、ヒーロー カード、リスト カード、Office 365 コネクタ カード、レシート カード、サインイン カード、サムネイル カード、カード コレクションの種類をサポートします。 カードの種類に応じて、Markdown または HTML を使用してリッチ テキスト書式をカードに追加できます。 ボットとメッセージング拡張機能で使用されるカードは、Microsoft Teams、 で、これらのカードアクションに追加して `openUrl` `messageBack` `imBack` `invoke` 応答します `signin` 。

Teamsは、次の 3 つの異なる場所でカードを使用します。

* コネクタ
* ボット
* メッセージング拡張機能

## <a name="cards-in-connectors"></a>コネクタ内のカード

カードは、最初に、OutlookおよびOffice 365の一部として定義され、現在はコネクタコネクタのOffice 365されています。 多くのアプリケーションOffice 365同様に、Teamsをサポートしています。 詳細については、「Office 365[コネクタ」を参照Teams。](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) コネクタ内のカードの仕様は、アクション可能なメッセージ カード [リファレンスで確認できます](/outlook/actionable-messages/card-reference)。

## <a name="cards-in-bots"></a>ボット内のカード

このMicrosoft Bot Framework、ボットがボット メッセージの一部として使用できる定義済みのカードのセットを追加することで、カードの仕様を拡張します。 Teamsボット フレームワークを使用してボットをサポートしていますが、これらのカードの異なるセットをサポートしています。 Bot Framework のカードに関する一般的な情報は、メッセージにリッチ カード [添付ファイルを追加するで確認できます](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。 これらのカードは、簡易カードと呼ばれるTeams。

ボットはTeamsカード、コネクタ カード、アダプティブ カードを使用できます。 [カードの種類は](~/task-modules-and-cards/cards/cards-reference.md)、カードに関する情報を提供します。Teams。

## <a name="cards-in-messaging-extensions"></a>メッセージング拡張機能のカード

[メッセージング拡張機能は、](~/messaging-extensions/what-are-messaging-extensions.md) カードを返す場合があります。 メッセージング拡張機能では、単純なカード、コネクタ カード、アダプティブ カードを使用できます。 これらのカードは、カード [の種類で見つかりました](~/task-modules-and-cards/cards/cards-reference.md)。

## <a name="types-of-cards"></a>カードの種類

ユーザーが使用するTeamsカードの種類[に一覧表示されます](~/task-modules-and-cards/cards/cards-reference.md)。 このリファレンスでは、ボット フレームワーク カードとボット フレームワーク カードの違いについて説明Teams。

## <a name="adaptive-cards"></a>アダプティブ カード

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

[アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)は、ボット、Cortana、Outlook、および Windows を含む Microsoft 製品の新しいクロス製品仕様です。 これらは、新しいカード開発に推奨されるTeamsです。 アダプティブ カード チームの一般的な情報については、「アダプティブ カード [の概要」を参照してください](/adaptive-cards)。 アダプティブ カードは、既存のヒーロー カード、Office 365カードを使用する任意の場所で使用できます。

アダプティブ カードに加えて、Teams 2 種類のカードがサポートされています。

* コネクタ カード: コネクタ コネクタの一Office 365されます。
* 単純なカード: サムネイルカードやヒーロー カードなど、ボット フレームワークから使用されます。

### <a name="adaptive-cards-and-incoming-webhooks"></a>アダプティブ カードと受信 Webhooks

> [!VIDEO https://www.youtube-nocookie.com/embed/y5pbJI43Zvg]

> [!NOTE]
> * ネイティブのアダプティブ カード スキーマ要素 (ただし `Action.Submit` 、 を除く) はすべて完全にサポートされています。
> * サポートされているアクションは [**、Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**、Action.ShowCard、Action.ToggleVisibility、**](https://adaptivecards.io/explorer/Action.ShowCard.html)およびAction.Exe [**です**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。 [](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)

受信 Webhook を使用したアダプティブ カードを使用すると、アダプティブ カードの豊富で柔軟な機能を使用できます。 Web サービスから受信 Webhooks を使用Teamsデータを送信します。

## <a name="see-also"></a>関連項目

* [カードの書式を設定Teams](~/task-modules-and-cards/cards/cards-format.md)
* [アダプティブ カードの設計](~/task-modules-and-cards/cards/design-effective-cards.md)

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [カードの種類](~/task-modules-and-cards/cards/cards-reference.md)