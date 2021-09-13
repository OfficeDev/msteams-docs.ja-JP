---
title: アプリのアダプティブ カードのデザイン
description: Teams のアダプティブ カードをデザインして、Microsoft Teams UI Kit を取得するする方法を説明します。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 0a8964de024b01237632db1214ce24fdd5b6bd29
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156885"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Microsoft Teams のアプリのアダプティブ カードの設計

アダプティブ カードには、カード要素のフリーフォーム本体とオプションのアクション セットが含まれています。 アダプティブ カードは、ボットまたはメッセージングの拡張機能を介してスレッドに追加できる、アクション可能なコンテンツのスニペットです。 これらのカードは、テキスト、グラフィック、ボタンを使用して、対象ユーザーにリッチなコミュニケーションを提供します。

アダプティブ カード フレームワークは、Teams を含む多くの Microsoft 製品で使用されています。 メッセージ内のカードは、ボットまたはメッセージングの拡張機能を介してユーザーに送信できます。 ユーザーは、カードが存在する場合、カードに対してアクションを実行することもできます。

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="アダプティブ カードの概要の例。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI Kit には、必要に応じて変更できる要素を含む、Teams のアダプティブ カードに関するより包括的なデザイン ガイドラインが掲載されています。 UI キットには、テーマ、アクセシビリティ、応答性の高いサイズ設定などの重要なトピックも含まれています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>アダプティブ カード デザイナー。

ブラウザーで直接アダプティブ カードのデザインを開始することもできます。

> [!div class="nextstepaction"]
> [アダプティブ カード デザイナーを試す](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>アダプティブ カードの種類

### <a name="hero"></a>ヒーロー

私たちの最大のカードです。画像がストーリーのほぼ全容を伝える記事やシナリオの共有に使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="モバイルでのアダプティブ カード ヒーロー カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="アダプティブ カードのヒーロー カードの例を示します。" border="false":::

### <a name="thumbnail"></a>サムネイル

単純な、アクション可能なメッセージを送信するために使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="モバイルでのアダプティブ カードのサムネイル カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="アダプティブ カードのサムネイル カードの例を示します。" border="false":::

### <a name="list"></a>リスト

ユーザーにリストから項目を選択してもらいたいが、項目に多くの説明は必要ないシナリオで使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="モバイルでのアダプティブ カードのリスト カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="アダプティブ カードのリスト カードの例を示します。" border="false":::

### <a name="digest"></a>Digest

ニュース ダイジェストと切り上げ投稿に使用します。 注: 単一の更新またはニュース アイテムに使用するサムネイル カードをお勧めします。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="モバイルでのアダプティブ カードのダイジェスト カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="アダプティブ カードのダイジェスト カードの例を示します。" border="false":::

### <a name="media"></a>メディア

オーディオやビデオなどのテキストとメディアを組み合わせたい場合に使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="モバイルでのアダプティブ カードのメディア カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="アダプティブ カードのメディア カードの例を示します。" border="false":::

### <a name="people"></a>連絡先

タスクに関係するユーザーを効率的に伝える場合に最適です。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="モバイルでのアダプティブ カードの連絡先カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="アダプティブ カードの連絡先カードの例を示します。" border="false":::

### <a name="request-ticket"></a>要求チケット

ユーザーから簡単な入力を取得して、タスクまたはチケットを自動的に作成するために使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="モバイルでのアダプティブ カードの要求チケット カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="アダプティブ カードの要求チケット カードの例を示します。" border="false":::

### <a name="image-set"></a>イメージ

複数の画像サムネイルを送信するために使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="モバイルでのアダプティブ カードの画像セット カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="アダプティブ カードの画像セット カードの例を示します。" border="false":::

### <a name="action-set"></a>アクション セット

ユーザーにボタンを選択してもらい、同じカードから追加のユーザー入力を収集する場合に使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="モバイルでのアダプティブ カードのアクション セット カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="アダプティブ カードのアクション セット カードの例を示します。" border="false":::

### <a name="choice-set"></a>選択肢セット

ユーザーから複数の入力を収集するために使用します。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="モバイルでのアダプティブ カードの選択肢セット カードの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="アダプティブ カードの選択肢セット カードの例を示します。" border="false":::

## <a name="anatomy"></a>構造

アダプティブ カードの柔軟性は高いです。 ただし、少なくとも、すべてのカードに次のコンポーネントを含めることをお勧めします。

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="モバイルでのアダプティブ カードの構造の例を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**ヘッダー**: ヘッダーを明確かつ簡潔にします。|
|B|**本文のコピー**: ヘッダーに含めるには長すぎるか、ヘッダーに含めるほど重要ではない詳細を伝えます。|
|C|**プライマリ アクション**: ベスト プラクティスとして、1 ~ 3 個のプライマリ アクションを含めます。 グループには最大 6 個のコントロールを指定できます。|

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="アダプティブ カードの構造の例を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|A|**ヘッダー**: ヘッダーを明確かつ簡潔にします。|
|B|**本文のコピー**: ヘッダーに含めるには長すぎるか、ヘッダーに含めるほど重要ではない詳細を伝えます。|
|C|**プライマリ アクション**: ベスト プラクティスとして、1 ~ 3 個のプライマリ アクションを含めます。 グループには最大 6 個のコントロールを指定できます。|

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="primary-and-secondary-actions"></a>プライマリとセカンダリ

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="アダプティブ カードに少数のアクションのみを含める方法に関するベスト プラクティス。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Do: 最大 6 つの主要なアクションを使用します

アダプティブ カードは 6 つの主要なアクションをサポートできますが、ほとんどのカードではそれを必要としません。 アクションは明確で簡潔で率直なものである必要があります。 少なければ少ない方がいいです。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="アダプティブ カードに対するアクションが多すぎてユーザーに負荷をかけないようにする方法についてのベスト プラクティスです。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>Don't: 6 つ以上のプライマリ アクションを使用しないでください

アダプティブ カードは、迅速で実用的なコンテンツを提示する必要があります。 アクションが多すぎると、ユーザーの負担になる可能性があります。

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>頻度

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="アダプティブ カードの頻度に関するベスト プラクティス。" border="false":::

#### <a name="do-be-concise"></a>Do: 簡潔にしてください

スレッドに複数のカードを送信するのは簡単ですが、スクロールしてカードが見えなくなると、役に立たなくなります。 必須項目にのみ制限するようにしてください。 これは、ユーザーが "ノイズ" と認識する内容に対する許容度が低いチャネルでは特に当てはまります。
