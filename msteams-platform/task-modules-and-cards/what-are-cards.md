---
title: カード
description: カードと、それらがボット、コネクタ、メッセージング拡張機能でどのように使用されるかについて説明します
ms.localizationpriority: high
keywords: コネクタ ボット カード メッセージング
ms.topic: overview
ms.openlocfilehash: 077da748ec7dd594b5ba029e3e53b0642610f1ee
ms.sourcegitcommit: 98cde8ff08552da4ce36fb0463982366bed979e0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2022
ms.locfileid: "62062524"
---
# <a name="cards"></a>カード

カードは、短い情報や関連する情報のユーザー インターフェイス (UI) コンテナーです。 カードには複数のプロパティと添付ファイルを含めることができます。また、ボタンを含めることができます。このボタンは、[カードアクション](~/task-modules-and-cards/cards/cards-actions.md)をトリガーします。 カードを使用すると、情報をグループに整理し、ユーザーが情報の特定の部分を操作する機会を与えることができます。

Teams のボットでは、次の種類のカードがサポートされています。
 
- アダプティブ カード
- ヒーロー カード
- リスト カード
- Office 365 コネクタ カード
- レシート カード
- サインイン カード
- サムネイル カード
- カード コレクション

カードの種類に応じて、Markdown または HTML を使用して、カードにリッチ テキストの書式設定を追加できます。 Microsoft Teams のボットとメッセージング拡張機能で使用されるカードは、これらのカード アクション、 `openUrl`、 `messageBack`、 `imBack`、 `invoke`、および `signin`に追加して応答します。

Teams では、次の 3 つの異なる場所でカードが使用されます。

* コネクタ
* ボット
* メッセージング拡張機能

## <a name="cards-in-connectors"></a>コネクタ内のカード

カードは、最初に Outlook と Office 365 の一部として定義され、Office 365 コネクタの一部として使用されるようになりました。 多くの Office 365 アプリケーションと同様に、Teams はコネクタをサポートしています。 詳細については、「[Teams の Office 365 コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)」を参照してください。 コネクタ内のカードの仕様は、[アクション可能なメッセージ カードリファレンス ](/outlook/actionable-messages/card-reference)にあります。

## <a name="cards-in-bots"></a>ボット内のカード

このMicrosoft Bot Framework、ボットがボット メッセージの一部として使用できる定義済みのカードのセットを追加することで、カードの仕様を拡張します。 Teams ではBot Frameworkを使用するボットがサポートされていますが、これらのカードの異なるセットがサポートされています。 Bot Framework のカードに関する一般的な情報については、「[メッセージにリッチ カードの添付ファイルを追加](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)」を参照してください。 これらのカードは、Teams では単純なカードと呼ばれます。

Teams のボットでは、単純なカード、コネクタ カード、またはアダプティブ カードを使用できます。 [カードの種類](~/task-modules-and-cards/cards/cards-reference.md)は Teams のボットでサポートされているカードに関する情報を提供します。

## <a name="cards-in-messaging-extensions"></a>メッセージング拡張機能のカード

[メッセージング拡張機能は、](~/messaging-extensions/what-are-messaging-extensions.md) カードを返す場合もあります。 メッセージング拡張機能では、単純なカード、コネクタ カード、またはアダプティブ カードを使用できます。 これらのカードは、 [カードの種類](~/task-modules-and-cards/cards/cards-reference.md)の中にあります。

## <a name="types-of-cards"></a>カードの種類

Teams で使用されるすべてのカードは、 [カードの種類](~/task-modules-and-cards/cards/cards-reference.md)に一覧表示されます。 このリファレンスでは、Teams のBot Framework カードとカードの違いについても説明します。

## <a name="adaptive-cards"></a>アダプティブ カード

[アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) は、ボット、Cortana、Outlook、Windows など、Microsoft 製品のカードの新しいクロス製品仕様です。 これらは、新しい Teams 開発に推奨されるカードの種類です。 アダプティブ カード チームからの一般的な情報については、「 [アダプティブ カード概要](/adaptive-cards)」を参照してください。 アダプティブ カードは、既存のヒーロー カード、Office 365 カード、サムネイル カードを使用する任意の場所で使用できます。

Teams では、アダプティブ カードに加えて、他の 2 種類のカードもサポートされています。

* コネクタ カード: Office 365 コネクタの一部として使用されます。
* シンプル カード: サムネイルカードやヒーロー カードなど、Bot Frameworkから使用されます。

### <a name="people-picker-in-adaptive-cards"></a>アダプティブ カードでのユーザー ピッカー

[ユーザー ピッカー](cards/people-picker.md#people-picker-in-adaptive-cards) 入力コントロールとして追加アダプティブ カード、ユーザーの検索と選択を有効にします。 チャット、チャネル、タスク モジュール、タブで使用できます。 モバイル クライアントとデスクトップ クライアントは、インライン入力エクスペリエンスを提供するユーザー ピッカーをサポートします。 

### <a name="type-ahead-search-in-adaptive-cards"></a>アダプティブ カードでの先行入力検索  

入力コントロールとして追加された先行検索を入力アダプティブ カード、動的に読み込まれたデータセットから[動的検索](~/task-modules-and-cards/cards/dynamic-search.md)エクスペリエンスを可能にします。 また、ユーザーは選択肢の数が限られているリスト内で先行入力の静的検索を実行することもできます。 モバイル クライアントとデスクトップ クライアントでは、先行入力の動的検索エクスペリエンスがサポートされています。 

### <a name="adaptive-cards-and-incoming-webhooks"></a>アダプティブ カードと受信 Webhook

> [!NOTE]
> * `Action.Submit`を除くすべてのネイティブ アダプティブ カード スキーマ要素は、完全にサポートされています。
> * サポートされているアクションは [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、[**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)、[**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)、および [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)です。

受信 Webhook でアダプティブ カードすると、アダプティブ カードの豊富で柔軟な機能を使用できます。 Teams の受信 Webhook を使用して、Web サービスからデータを送信します。

## <a name="support-for-aad-object-id-and-upn-in-user-mention"></a>ユーザーメンションでの AAD オブジェクト ID と UPN のサポート 

アダプティブ カードを持つボットでは、既存の ID に加えて、AAD オブジェクト ID やユーザー プリンシパル名 (UPN) などのユーザーメンション ID がサポートされます。 受信 Webhook では、AAD オブジェクト ID と UPN を使用したアダプティブ カードでのユーザーメンションのサポートが開始されます。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [カードの種類](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="see-also"></a>関連項目

* [Teams でカードを書式設定する](~/task-modules-and-cards/cards/cards-format.md)
* [アダプティブ カードの設計](~/task-modules-and-cards/cards/design-effective-cards.md)
* [ボットのアダプティブ カード](../bots/how-to/conversations/conversation-messages.md#adaptive-cards)