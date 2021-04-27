---
title: アプリのアダプティブ カードの設計
description: Teams 用アダプティブ カードを設計し、Microsoft Teams UI キットを取得する方法について説明します。
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 67a2882a0a687d5ccb48759419ecefcdf9396fc3
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020283"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Microsoft Teams アプリのアダプティブ カードの設計

アダプティブ カードには、カード要素のフリーフォーム本文とオプションのアクション セットが含まれます。 アダプティブ カードは、ボットまたはメッセージング拡張機能を介して会話に追加できる、アクション可能なコンテンツのスニペットです。 テキスト、グラフィックス、およびボタンを使用して、これらのカードはユーザーに豊富なコミュニケーションを提供します。

アダプティブ カード フレームワークは、Teams を含む多くの Microsoft 製品で使用されます。 メッセージ内のカードは、ボットまたはメッセージング拡張機能を介してユーザーに送信できます。 ユーザーは、存在する場合にカードに対してアクションを実行できます。

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="アダプティブ カードの例を示します。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

必要に応じて取得および変更できる要素を含む、Teams のアダプティブ カードのより包括的な設計ガイドラインについては、「Microsoft Teams UI Kit」を参照してください。 UI キットでは、テーマ、アクセシビリティ、応答性のサイジングなどの重要なトピックも扱います。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>アダプティブ カード デザイナー

アダプティブ カードの設計をブラウザーで直接開始することもできます。

> [!div class="nextstepaction"]
> [アダプティブ カード デザイナーを試す](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>アダプティブ カードの種類

### <a name="hero"></a>ヒーロー

最大のカード。 画像がほとんどのストーリーを伝える記事やシナリオを共有するために使用します。

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="アダプティブ カードの例を示します。" border="false":::

### <a name="thumbnail"></a>サムネイル

単純な操作可能なメッセージの送信に使用します。

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="アダプティブ カードの例。" border="false":::

### <a name="list"></a>一覧表示

ユーザーがリストからアイテムを選択するシナリオで使用しますが、項目に多くの説明は必要はありません。

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="アダプティブ カードの例。" border="false":::

### <a name="digest"></a>ダイジェスト

ニュース ダイジェストと丸め投稿に使用します。 注: 1 つの更新またはニュース アイテムのサムネイル カードをお勧めします。

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="図はアダプティブ カードを示しています。" border="false":::

### <a name="media"></a>メディア

オーディオやビデオなど、テキストとメディアを組み合わせる場合に使用します。

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="図はアダプティブ カードを示しています。" border="false":::

### <a name="people"></a>連絡先

タスクに関わるユーザーを効率的に伝える場合に最適です。

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="アダプティブ カードの図。" border="false":::

### <a name="request-ticket"></a>チケットの要求

タスクまたはチケットを自動的に作成するために、ユーザーからのクイック入力を取得するために使用します。

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="アダプティブ カードの図。" border="false":::

### <a name="imageset"></a>ImageSet

複数の画像サムネイルを送信する場合に使用します。

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="アダプティブ カードのサンプル。" border="false":::

### <a name="actionset"></a>ActionSet

ユーザーがボタンを選択し、追加ユーザー入力を同じカードから収集する場合に使用します。

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="サンプルはアダプティブ カードを示しています。" border="false":::

### <a name="choiceset"></a>ChoiceSet

ユーザーから複数の入力を収集するために使用します。

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="アダプティブ カードを表示する例。" border="false":::

## <a name="anatomy"></a>構造

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="アダプティブ カードの UI 構造を示す図。" border="false":::

アダプティブ カードには多くの柔軟性があります。 ただし、少なくとも、すべてのカードに次のコンポーネントを含め、強く推奨します。

|カウンター|説明|
|----------|-----------|
|A|**ヘッダー**: ヘッダーを明確かつ簡潔にし、説明的にします。|
|B|**本文コピー**: ヘッダーに含めるほど長すぎるか、重要ではない詳細を伝えるために使用します。|
|C|**主なアクション**: ベスト プラクティスとして、1 ~ 3 の主なアクションを含める。 最大 6 個まで使用できます。|

## <a name="best-practices"></a>ベスト プラクティス

### <a name="primary-and-secondary-actions"></a>プライマリアクションとセカンダリ アクション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="アダプティブ カードのベスト プラクティスを示す例。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Do: 最大 6 つのプライマリ アクションを使用する

アダプティブ カードは 6 つの主なアクションをサポートすることができますが、ほとんどのカードでは必要とされていません。 アクションは明確で簡潔で、簡単に行う必要があります。 より少ない方が多い。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="アダプティブ カードのベスト プラクティスの例を示します。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>[しない]: 6 つ以上の主なアクションを使用する

アダプティブ カードは、迅速で操作可能なコンテンツを提示する必要があります。 アクションが多すぎると、ユーザーが圧倒される可能性があります。

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Frequency

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="アダプティブ カードのベスト プラクティスを表示する図。" border="false":::

#### <a name="do-be-concise"></a>Do: 簡潔に

複数のカードを会話に送信するのは簡単ですが、カードが表示から外にスクロールすると、あまり役に立たなくなります。 自分を必需品に限定してみてください。 これは、ユーザーが "ノイズ" と認識する値に対する許容度が低いチャネルでは特に当てはまる。
