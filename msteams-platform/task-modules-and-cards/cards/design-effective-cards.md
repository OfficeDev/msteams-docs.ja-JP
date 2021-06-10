---
title: アプリのアダプティブ カードの設計
description: ユーザー向けアダプティブ カードを設計し、Teams UI キットMicrosoft Teamsする方法について学習します。
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b4d5f43268c7bd5afecb56d26eb0d49ed6c9002b
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630281"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>アプリのアダプティブ カードMicrosoft Teamsする

アダプティブ カードには、カード要素のフリーフォーム本文とオプションのアクション セットが含まれます。 アダプティブ カードは、ボットまたはメッセージング拡張機能を介して会話に追加できる、アクション可能なコンテンツのスニペットです。 テキスト、グラフィックス、およびボタンを使用して、これらのカードはユーザーに豊富なコミュニケーションを提供します。

アダプティブ カード フレームワークは、さまざまな Microsoft 製品で使用されます。このフレームワークは、Teams。 メッセージ内のカードは、ボットまたはメッセージング拡張機能を介してユーザーに送信できます。 ユーザーは、存在する場合にカードに対してアクションを実行できます。

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="アダプティブ カードの概要の例。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

アダプティブ カードのより包括的な設計ガイドラインについては、Teams の UI キットで、必要に応じて取得および変更できる要素を含む、Microsoft Teamsをご覧ください。 UI キットでは、テーマ、アクセシビリティ、応答性のサイジングなどの重要なトピックも扱います。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>アダプティブ カード デザイナー

アダプティブ カードの設計をブラウザーで直接開始することもできます。

> [!div class="nextstepaction"]
> [アダプティブ カード デザイナーを試す](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>アダプティブ カードの種類

### <a name="hero"></a>ヒーロー

最大のカード。 画像がほとんどのストーリーを伝える記事やシナリオを共有するために使用します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="アダプティブ カードのヒーロー カードの例を示します。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="例は、モバイルでのアダプティブ カードのヒーロー カードを示しています。" border="false":::

---

### <a name="thumbnail"></a>サムネイル

単純な操作可能なメッセージの送信に使用します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="アダプティブ カードのサムネイル カードの例を示します。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="例では、モバイルでアダプティブ カードのサムネイル カードを表示します。" border="false":::

---

### <a name="list"></a>List

ユーザーがリストからアイテムを選択するシナリオで使用しますが、項目に多くの説明は必要はありません。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="アダプティブ カードリスト カードの例を示します。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="例は、モバイル上のアダプティブ カード リスト カードを示しています。" border="false":::

---

### Digest

Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false":::

---

### <a name="media"></a>メディア

オーディオやビデオなど、テキストとメディアを組み合わせる場合に使用します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="アダプティブ カード メディア カードの例を示します。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="例は、モバイル上のアダプティブ カード メディア カードを示しています。" border="false":::

---

### <a name="people"></a>連絡先

タスクに関わるユーザーを効率的に伝える場合に最適です。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="アダプティブ カードのユーザー カードの例を示します。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="例は、モバイル上のアダプティブ カードのユーザー カードを示しています。" border="false":::

---

### <a name="request-ticket"></a>チケットの要求

タスクまたはチケットを自動的に作成するために、ユーザーからのクイック入力を取得するために使用します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="アダプティブ カード要求チケット カードの例を示します。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="例は、モバイル上のアダプティブ カード要求チケット カードを示しています。" border="false":::

---

### <a name="image-set"></a>イメージ セット

複数の画像サムネイルを送信する場合に使用します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="アダプティブ カードイメージ セット カードの例を示します。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="例は、モバイル上のアダプティブ カード イメージ セット カードを示しています。" border="false":::

---

### <a name="action-set"></a>アクション セット

ユーザーがボタンを選択し、追加ユーザー入力を同じカードから収集する場合に使用します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="アダプティブ カード アクション セット カードの例を示します。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="例は、モバイル上のアダプティブ カード アクション セット カードを示しています。" border="false":::

---

### <a name="choice-set"></a>選択肢セット

ユーザーから複数の入力を収集するために使用します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="アダプティブ カードの選択肢セット カードの例を示します。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="例は、モバイル上のアダプティブ カード選択セット カードを示しています。" border="false":::

---

## <a name="anatomy"></a>構造

アダプティブ カードには多くの柔軟性があります。 ただし、少なくとも、すべてのカードに次のコンポーネントを含め、強く提案します。

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="EExample はアダプティブ カードの構造を示します。" border="false":::

# <a name="mobile"></a>[モバイル](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="例は、モバイルでのアダプティブ カードの構造を示しています。" border="false":::

---

|カウンター|説明|
|----------|-----------|
|A|**ヘッダー**: ヘッダーを明確かつ簡潔にします。|
|B|**本文コピー**: ヘッダーに含めるほど長すぎるか、重要ではない詳細を伝える。|
|C|**主なアクション**: ベスト プラクティスとして、1 ~ 3 の主なアクションを含める。 最大 6 個まで使用できます。|

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="primary-and-secondary-actions"></a>プライマリアクションとセカンダリ アクション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="アダプティブ カードにアクションの小さなセットのみを含める方法に関するベスト プラクティス。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Do: 最大 6 つのプライマリ アクションを使用する

アダプティブ カードは 6 つの主なアクションをサポートすることができますが、ほとんどのカードでは必要とされていません。 アクションは明確で簡潔で、簡単に行う必要があります。 より少ない方が多い。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="アダプティブ カードのアクションが多すぎるとユーザーを圧倒しない方法に関するベスト プラクティス。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>[しない]: 6 つ以上の主なアクションを使用する

アダプティブ カードは、迅速で操作可能なコンテンツを提示する必要があります。 アクションが多すぎると、ユーザーが圧倒される可能性があります。

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Frequency

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="アダプティブ カードの頻度に関するベスト プラクティス。" border="false":::

#### <a name="do-be-concise"></a>Do: 簡潔に

複数のカードを会話に送信するのは簡単ですが、カードが表示から外にスクロールすると、あまり役に立たなくなります。 自分を必需品に限定してみてください。 これは、ユーザーが "ノイズ" と認識する値に対する許容度が低いチャネルでは特に当てはまる。
