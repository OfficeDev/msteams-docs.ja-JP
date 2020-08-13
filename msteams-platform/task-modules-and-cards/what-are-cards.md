---
title: カードの紹介
description: カードと、ボット、コネクタ、およびメッセージング拡張機能での使用方法について説明します。
keywords: コネクタボットカードメッセージ
ms.openlocfilehash: 6d850f83183f12fa0c228a7a89b23e58f523e15b
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651657"
---
# <a name="cards"></a>カード

*カード*は、短いまたは関連する情報のユーザーインターフェイス (UI) コンテナーです。 カードは複数のプロパティと添付ファイルを持つことができます。 カードには、 [カードアクション](~/task-modules-and-cards/cards/cards-actions.md)をトリガーできるボタンを含めることができます。

## <a name="adaptive-cards"></a>アダプティブカード

[アダプティブカード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) は、ボット、Cortana、Outlook、Windows など、Microsoft 製品のカードの新しいクロスプロダクト仕様です。 新しいチーム開発に推奨されるカードの種類です。 アダプティブカードチームからの一般的な情報については、「 [アダプティブカードの概要](/adaptive-cards)」を参照してください。 既存のヒーローカード、Office365 カード、およびサムネイルカードを使用できる場所であれば、アダプティブカードを使用することができます。

アダプティブカードに加えて、Teams は次の2種類のカードをサポートしています。

* コネクタカード。 Office 365 コネクタの一部として使用されます。
* Bot フレームワークからのシンプルなカード (サムネイルカード、英雄カードなど)。

これらのカードの種類については、 [Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)でさらに詳しく説明されています。

Teams では、次の3つの異なる場所にカードを使用します。

* コネクタ
* ボット
* メッセージングの拡張機能

## <a name="adaptive-cards-and-incoming-webhooks"></a>アダプティブカードと受信 web フック

> [!NOTE]
> アダプティブカードは、 [一般開発者向けプレビュープログラム](../resources/dev-preview/developer-preview-intro.md)の一部として受信 web フックでサポートされています。 パブリックプレビューは、早期アクセスおよびフィードバックに使用できます。 リリースは安定しており、広範なテストを行っていますが、運用環境での使用は想定されていません。
>
> ✔開発者向けプレビューでは、を除くすべてのネイティブアダプティブカードスキーマ要素 `Action.Submit` が完全にサポートされています。
>
> サポートされているアクションは✔ [**OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、 [**showcard**](https://adaptivecards.io/explorer/Action.ShowCard.html)、および [**action.togglevisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)です。

## <a name="cards-in-connectors"></a>コネクタ内のカード

カードは、最初は Outlook および Office 365 の一部として定義されており、Office 365 コネクタの一部として使用されています。 多くの Office 365 アプリケーションと同様に、Teams はコネクタをサポートしています。 [Microsoft Teams の Office 365 コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)のコネクタの詳細については、「操作可能な[メッセージカードリファレンス](/outlook/actionable-messages/card-reference)」の「コネクタ内のカードの仕様」を参照してください。

## <a name="cards-in-bots"></a>Bot のカード

Microsoft Bot フレームワークは、ボットメッセージの一部として使用できる定義済みのカードのセットを追加することによって、カードの仕様を拡張しました。 Teams は Bot フレームワークを使用してサポートされていますが、これらのカードの少し異なるセットをサポートしています。 Bot フレームワークのカードに関する一般的な情報については、「 [メッセージへのリッチカードの添付ファイルの追加](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)」を参照してください。 これらのカードは Teams で *シンプルカード* と呼ばれています。

Teams のボットは、任意の種類のカードを使用できます: simple、connector、またはアダプティブ。 Teams の bot がサポートするカードについては、 [Teams カードリファレンスを参照](~/task-modules-and-cards/cards/cards-reference.md)してください。  

## <a name="cards-in-messaging-extensions"></a>メッセージング拡張機能のカード

[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md) もカードを返すことができます。 メッセージング拡張機能では、シンプル、コネクタ、またはアダプティブのいずれの種類のカードでも使用できます。 これらのカードは [Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)に掲載されています。

## <a name="card-reference"></a>カードリファレンス

Teams で使用されるすべてのカードは [Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)に記載されています。 このリファレンスでは、Teams の Bot フレームワークカードとカードの相違点についても説明します。
