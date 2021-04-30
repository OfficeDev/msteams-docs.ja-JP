---
title: カードの紹介
description: カードと、ボット、コネクタ、メッセージング拡張機能でのカードの使い方について説明します。
localization_priority: Normal
ms.topic: conceptual
keywords: コネクタ ボット カード メッセージング
ms.openlocfilehash: 77dcbb7d0472b584623e878df956a6165296f4cf
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088753"
---
# <a name="cards"></a>カード

カード *は* 、短い情報や関連する情報のユーザー インターフェイス (UI) コンテナーです。 カードには複数のプロパティと添付ファイルを含めることができます。 カードには、カードアクションをトリガーできるボタン [を含めできます](~/task-modules-and-cards/cards/cards-actions.md)。

## <a name="adaptive-cards"></a>アダプティブ カード

[アダプティブ カードは](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)、Bots、Cortana、Outlook、および Windows などの Microsoft 製品のカードの新しいクロス製品仕様です。 これらは、新しいカード開発に推奨されるTeamsです。 アダプティブ カード チームの一般的な情報については、「アダプティブ カード [の概要」を参照してください](/adaptive-cards)。 アダプティブ カードは、既存のヒーロー カード、Office365 カード、およびサムネイル カードを使用できる任意の場所で使用できます。

アダプティブ カードに加えて、Teams 2 種類のカードがサポートされています。

* コネクタ カード(コネクタ コネクタの一Office 365されます。
* サムネイルカードやヒーロー カードなど、ボット フレームワークからの単純なカード。

これらのカードの種類については、「カードリファレンス」[で詳Teams説明します](~/task-modules-and-cards/cards/cards-reference.md)。

Teamsは、次の 3 つの異なる場所でカードを使用します。

* コネクタ
* ボット
* メッセージング拡張機能

## <a name="adaptive-cards-and-incoming-webhooks"></a>アダプティブ カードと受信 Webhooks

> [!NOTE]
>
> ✔ `Action.Submit` 以外のすべてのネイティブのアダプティブ カード スキーマ要素は、完全にサポートされます。
>
> ✔サポートされているアクションは[](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute)、Action.OpenURL、Action.ShowCard、Action.ToggleVisibility、およびAction.Exeです。 [](https://adaptivecards.io/explorer/Action.OpenUrl.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html) [](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)

## <a name="cards-in-connectors"></a>コネクタ内のカード

カードは最初に、OutlookおよびOffice 365の一部として定義され、Office 365コネクタの一部として使用されます。 多くのアプリケーションOffice 365同様に、Teamsコネクタもサポートしています。 コネクタの詳細については、「Office 365 コネクタ[](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)for Microsoft Teams」、および「Actionable message card reference」の「コネクタ内のカードの仕様」[を参照してください](/outlook/actionable-messages/card-reference)。

## <a name="cards-in-bots"></a>ボット内のカード

このMicrosoft Bot Frameworkボットがボット メッセージの一部として使用できる定義済みのカードのセットを追加することで、カードの仕様を拡張しました。 Teamsボットフレームワークを使用してボットをサポートしていますが、これらのカードの少し異なるセットをサポートしています。 Bot Framework のカードに関する一般的な情報については、「メッセージにリッチ カード [の添付ファイルを追加する」を参照してください](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。 これらのカードは、簡易 *カードと* 呼ばれるTeams。

ボットは、Teams、コネクタ、アダプティブなど、任意の種類のカードを使用できます。 このページのボットでサポートされているTeamsについては[、「Teams」を参照してください](~/task-modules-and-cards/cards/cards-reference.md)。  

## <a name="cards-in-messaging-extensions"></a>メッセージング拡張機能のカード

[メッセージング拡張機能は、](~/messaging-extensions/what-are-messaging-extensions.md) カードを返す場合があります。 メッセージング拡張機能では、シンプル、コネクタ、アダプティブなど、任意の種類のカードを使用できます。 これらのカードは、「カード リファレンス[」のTeamsに示されています](~/task-modules-and-cards/cards/cards-reference.md)。

## <a name="card-reference"></a>カード参照

ユーザーが使用するTeamsは、[カードリファレンス] にTeams[一覧表示されます](~/task-modules-and-cards/cards/cards-reference.md)。 このリファレンスでは、ボット フレームワーク カードとボット フレームワーク カードの違いについて説明Teams。
