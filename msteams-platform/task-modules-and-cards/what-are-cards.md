---
title: カードの紹介
description: カードについて説明し、ボット、コネクタ、メッセージング拡張機能でカードがどのように使用されるのかについて説明します。
keywords: コネクタボット カードメッセージング
ms.openlocfilehash: 00c649a1339f05b782e03a2c0db5cba2445f66bc
ms.sourcegitcommit: 23ceb25d07a76f03ffe92cf1ac578b7c50b0bafc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2021
ms.locfileid: "49777925"
---
# <a name="cards"></a>カード

カード *は* 、短い情報または関連する情報のユーザー インターフェイス (UI) コンテナーです。 カードには、複数のプロパティと添付ファイルを含めることができます。 カードには、カードアクションをトリガーできるボタン [を含めできます](~/task-modules-and-cards/cards/cards-actions.md)。

## <a name="adaptive-cards"></a>アダプティブ カード

[アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) は、ボット、Cortana、Outlook、Windows など、Microsoft 製品のカードの新しいクロス製品仕様です。 これらは、新しい Teams 開発に推奨されるカードの種類です。 アダプティブ カード チームからの一般的な情報については、「アダプティブ カード [の概要」を参照してください](/adaptive-cards)。 アダプティブ カードは、既存のヒーロー カード、Office365 カード、サムネイル カードを使用できる任意の場所で使用できます。

Teams では、アダプティブ カードに加えて、次の 2 種類のカードをサポートしています。

* 365 コネクタの一部としてOfficeカード。
* サムネイルやヒーロー カードなど、ボット フレームワークからの単純なカード。

これらのカードの種類については、「Teams カード リファレンス」で [詳しい説明があります](~/task-modules-and-cards/cards/cards-reference.md)。

Teams は、次の 3 つの異なる場所でカードを使用します。

* コネクタ
* ボット
* メッセージング拡張機能

## <a name="adaptive-cards-and-incoming-webhooks"></a>アダプティブ カードと受信 Webhook

> [!NOTE]
>
> ✔ `Action.Submit` 以外のすべてのネイティブのアダプティブ カード スキーマ要素は、完全にサポートされます。
>
> ✔サポートされているアクションは、Action.OpenURL、Action.ShowCard、Action.ToggleVisibility [**です**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)。 [](https://adaptivecards.io/explorer/Action.OpenUrl.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html)

## <a name="cards-in-connectors"></a>コネクタ内のカード

カードは最初に Outlook および Office 365 の一部として定義され、Office 365 コネクタの一部として使用されます。 365 Officeの多くのアプリケーションと同様に、Teams はコネクタをサポートしています。 Office [365 Connectors for Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)のコネクタの詳細を確認し、コネクタ内のカードの仕様については、「操作可能なメッセージ カード リファレンス」 [を参照してください](/outlook/actionable-messages/card-reference)。

## <a name="cards-in-bots"></a>ボット内のカード

Microsoft Bot Framework は、ボットがボット メッセージの一部として使用できる定義済みカードのセットを追加することで、カードの仕様を拡張しました。 Teams は Bot Framework を使用したボットをサポートしますが、これらのカードの少し異なるセットをサポートします。 Bot Framework のカードに関する一般的な情報については、「リッチ カードの添付ファイルをメッセージ [に追加する」を参照してください](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。 これらのカードは、Teams では *簡易カード* と呼ばれるカードです。

Teams のボットは、シンプル、コネクタ、アダプティブなど、任意の種類のカードを使用できます。 Teams のボットでサポートされているカードの詳細については、「Teams カード リファレンス」 [を参照してください](~/task-modules-and-cards/cards/cards-reference.md)。  

## <a name="cards-in-messaging-extensions"></a>メッセージング拡張機能のカード

[メッセージング拡張機能は、](~/messaging-extensions/what-are-messaging-extensions.md) カードを返す場合があります。 メッセージング拡張機能は、シンプル、コネクタ、アダプティブなど、任意の種類のカードを使用できます。 これらのカードは、Teams カード リファレンス [に含まれるものがあります](~/task-modules-and-cards/cards/cards-reference.md)。

## <a name="card-reference"></a>カード リファレンス

Teams で使用されるカードはすべて、Teams カード リファレンスに [記載されています](~/task-modules-and-cards/cards/cards-reference.md)。 このリファレンスでは、Teams での Bot Framework カードとカードの違いも説明します。
