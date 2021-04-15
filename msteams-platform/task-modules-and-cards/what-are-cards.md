---
title: カードの紹介
description: カードと、ボット、コネクタ、メッセージング拡張機能でのカードの使い方について説明します。
ms.topic: conceptual
keywords: コネクタ ボット カード メッセージング
ms.openlocfilehash: c2fe0aea142a96643e33e16acc08bcfd8c33e92e
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696459"
---
# <a name="cards"></a>カード

カード *は* 、短い情報や関連する情報のユーザー インターフェイス (UI) コンテナーです。 カードには複数のプロパティと添付ファイルを含めることができます。 カードには、カードアクションをトリガーできるボタン [を含めできます](~/task-modules-and-cards/cards/cards-actions.md)。

## <a name="adaptive-cards"></a>アダプティブ カード

[アダプティブ カードは](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) 、ボット、Cortana、Outlook、Windows などの Microsoft 製品のカードの新しいクロス製品仕様です。 これらは、新しい Teams 開発に推奨されるカードの種類です。 アダプティブ カード チームの一般的な情報については、「アダプティブ カード [の概要」を参照してください](/adaptive-cards)。 アダプティブ カードは、既存のヒーロー カード、Office365 カード、およびサムネイル カードを使用できる任意の場所で使用できます。

アダプティブ カードに加えて、Teams は次の 2 種類のカードをサポートしています。

* 365 コネクタの一部としてOfficeカード。
* サムネイルカードやヒーロー カードなど、ボット フレームワークからの単純なカード。

これらのカードの種類については、「Teams カードリファレンス」 [を参照してください](~/task-modules-and-cards/cards/cards-reference.md)。

Teams は、次の 3 つの異なる場所でカードを使用します。

* コネクタ
* ボット
* メッセージング拡張機能

## <a name="adaptive-cards-and-incoming-webhooks"></a>アダプティブ カードと受信 Webhooks

> [!NOTE]
>
> ✔ `Action.Submit` 以外のすべてのネイティブのアダプティブ カード スキーマ要素は、完全にサポートされます。
>
> ✔サポートされているアクションは [**、Action.OpenURL、Action.ShowCard、**](https://adaptivecards.io/explorer/Action.OpenUrl.html)[**および Action.ToggleVisibility です**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)。 [](https://adaptivecards.io/explorer/Action.ShowCard.html)

## <a name="cards-in-connectors"></a>コネクタ内のカード

カードは、最初に Outlook および Office 365 の一部として定義され、365 コネクタOffice使用されます。 365 Officeの多くのアプリケーションと同様に、Teams はコネクタをサポートしています。 Microsoft Teams 用 Office [365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)コネクタのコネクタの詳細については、「アクション可能なメッセージ カードリファレンス」の「コネクタ内のカードの仕様」 [を参照してください](/outlook/actionable-messages/card-reference)。

## <a name="cards-in-bots"></a>ボット内のカード

Microsoft Bot Framework は、ボットがボット メッセージの一部として使用できる定義済みのカードのセットを追加することで、カードの仕様を拡張しました。 Teams はボット フレームワークを使用してボットをサポートしますが、これらのカードの少し異なるセットをサポートしています。 Bot Framework のカードに関する一般的な情報については、「メッセージにリッチ カード [の添付ファイルを追加する」を参照してください](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。 これらのカードは Teams の簡易 *カードと* 呼ばれる。

Teams のボットは、シンプル、コネクタ、アダプティブなど、任意の種類のカードを使用できます。 Teams のボットでサポートされているカードについては、「Teams カードリファレンス [」を参照してください](~/task-modules-and-cards/cards/cards-reference.md)。  

## <a name="cards-in-messaging-extensions"></a>メッセージング拡張機能のカード

[メッセージング拡張機能は、](~/messaging-extensions/what-are-messaging-extensions.md) カードを返す場合があります。 メッセージング拡張機能では、シンプル、コネクタ、アダプティブなど、任意の種類のカードを使用できます。 これらのカードは[、Teams カードリファレンスに含まれる。](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="card-reference"></a>カード参照

Teams で使用されるカードはすべて、Teams カードリファレンス [に一覧表示されます](~/task-modules-and-cards/cards/cards-reference.md)。 このリファレンスでは、Teams の Bot Framework カードとカードの違いについて説明します。
