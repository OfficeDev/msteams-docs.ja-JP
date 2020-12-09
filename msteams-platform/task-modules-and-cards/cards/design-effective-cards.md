---
title: アプリに適応カードを設計する
description: Teams 用のアダプティブカードを設計し、Microsoft Teams UI キットを取得する方法について説明します。
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bd48846284620415cc8cadabc59f2ab7b61d5189
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604555"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Microsoft Teams アプリ用のアダプティブカードの設計

アダプティブカードには、フリーフォームのカード要素と任意のアクションセットが含まれています。 アダプティブカードは、ボットまたはメッセージング拡張機能を使用して会話に追加できる、実行可能なコンテンツのスニペットです。 これらのカードは、テキスト、グラフィックス、ボタンを使用して、対象ユーザーに豊富なコミュニケーションを提供します。

アダプティブカードフレームワークは、Teams を含む多くの Microsoft 製品で使用されています。 Bot またはメッセージング拡張機能を使用して、メッセージ内のカードをユーザーに送信することができます。 ユーザーは、表示されている場合は、カードに対してアクションを実行できます。

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI キットでは、必要に応じて取得して変更できる要素を含め、Teams のアダプティブカードについて、より包括的な設計ガイドラインを参照できます。 UI キットでは、テーマ、アクセシビリティ、応答性の高いサイズ設定など、重要なトピックについても説明しています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を取得する](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>アダプティブカードデザイナー

また、アダプティブカードのデザインをブラウザーで直接開始することもできます。

> [!div class="nextstepaction"]
> [アダプティブカードデザイナーを試す](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>アダプティブカードの種類

### <a name="hero"></a>ヒーロー

最大のカード 画像が最も多くの話を伝える記事やシナリオを共有するために使用します。

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="thumbnail"></a>Thumbnail

簡単な操作可能なメッセージを送信するために使用します。

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="list"></a>リスト

ユーザーがリストからアイテムを選択する必要があるが、アイテムには多くの説明は必要ない場合に使用します。

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="digest"></a>Digest

ニュースダイジェストおよび切り上げられた投稿に使用します。 注: 1 つの更新プログラムまたはニュースアイテムには、サムネイルカードをお勧めします。

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="media"></a>メディア

音声やビデオなどのテキストとメディアを結合する場合に使用します。

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="people"></a>People

タスクに関係する人物を効率的に伝える場合に最適です。

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="request-ticket"></a>要求チケット

ユーザーからすばやく入力を取得して、タスクまたはチケットを自動的に作成するために使用します。

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="imageset"></a>ImageSet

複数の画像のサムネイルを送信するために使用します。

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="actionset"></a>ActionSet

ユーザーにボタンを選択させ、そのカードから追加のユーザー入力を収集する場合に使用します。

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

### <a name="choiceset"></a>ChoiceSet

ユーザーから複数の入力を収集するために使用します。

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="例は、アダプティブカードを示しています。" border="false":::

## <a name="anatomy"></a>構造

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="アダプティブカードの UI の構造を示す図。" border="false":::

アダプティブカードには多くの柔軟性があります。 ただし、少なくとも、以下のコンポーネントをすべてのカードに含めることを強くお勧めします。

|カウンター|説明|
|----------|-----------|
|A|**ヘッダー**: ヘッダーを明瞭で簡潔なものにします。ただし、わかりやすくする。|
|B|**本文のコピー**: ヘッダーに含めるには、長すぎる、または重要ではない詳細情報を伝達するために使用します。|
|C|**主な処置**: ベストプラクティスとして、1-3 プライマリアクションを含めます。 最大6個が許可されます。|

## <a name="best-practices"></a>ベスト プラクティス

### <a name="primary-and-secondary-actions"></a>プライマリおよびセカンダリのアクション

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="アダプティブカードのベストプラクティスを示す例。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Do: 最大6つの主要なアクションを使用します。

アダプティブカードは6つの主要なアクションをサポートしていますが、ほとんどのカードはそれを必要としません。 アクションは、明瞭、簡潔、およびまっすぐに実行する必要があります。 これよりも少なくなります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="アダプティブカードのベストプラクティスを示す例。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>6つ以上の主なアクションを使用します。

アダプティブカードは、すぐに実行可能なコンテンツを表示する必要があります。 ユーザーが過負荷になる可能性があります。

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Frequency

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="アダプティブカードのベストプラクティスを示す例。" border="false":::

#### <a name="do-be-concise"></a>実行: 簡潔

複数のカードを1つの会話に簡単に送信できますが、カードが表示されなくなると、利便性が低下します。 Essentials に制限するようにしてください。 これは、ユーザーが "ノイズ" として認識される許容範囲を下回っているチャネルの場合に特に当てはまります。
