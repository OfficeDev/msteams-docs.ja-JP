---
title: アプリを設計し、基本事項を理解する
description: レイアウト、配色など、Microsoft Teams アプリの設計に関する基本事項について説明します。
author: heath-hamilton
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 91191f9d431fc45fae41c58e24fdf142e5af0b25
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606007"
---
# <a name="microsoft-teams-app-design-fundamentals"></a>Microsoft Teams アプリデザインの基礎

Teams アプリデザインの基礎について簡単に説明します。 総合的なガイダンスと例については、 <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">「Microsoft TEAMS UI Kit (Figma)</a>」を参照してください。

## <a name="layout"></a>レイアウト

:::row:::

   :::column span="3":::

      Teams は、デザインコンポーネント間の一貫性と洗練された関係を実現するためにグリッドレイアウトに依存します。 グリッドの4ピクセルの基本単位を使用すると、Teams のすべての表示サイズ間で、コンポーネントを一貫して拡大または縮小できます。

      <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なレイアウトガイドライン (Figma) を参照</a>

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-layout.png" alt-text="Microsoft Teams UI Kit の概念図。" border="false":::
   :::column-end:::

:::row-end:::

## <a name="avatars"></a>アバター

:::row:::

   :::column span="3":::

      アバターは、Teams の人物、チーム、ボット、またはエンティティをグラフィカルに表現したものです。 アバターグループは、多くの場合、ライブアクティビティを伝えるため、または、垂直スペースを保持する方法で名簿を表すために使用されます。 

      <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なアバターガイドライン (Figma) を参照してください。</a>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-avatars.png" alt-text="Microsoft Teams UI Kit の概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="colors"></a>色

:::row:::

   :::column span="3":::

      Teams web およびデスクトップは、既定の (淡色)、暗い、およびハイコントラストテーマをサポートしていますが、Teams mobile は明るいテーマと暗いテーマをサポートしています。 各テーマには独自の配色があります。

      <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">フルカラーガイドラインと使用可能なカラートークン (Figma) を参照してください。</a>

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-color.png" alt-text="Microsoft Teams UI Kit の概念図。" border="false":::
   :::column-end:::

:::row-end:::

## <a name="iconography"></a>図像

:::row:::

   :::column span="3":::

      Teams アプリは、Fluent UI で提供されるアイコンを使用します。

### <a name="resources"></a>リソース

      * <a href="https://www.figma.com/community/file/836835755999342788" target="_blank">最新の Fluent アイコン (Figma) を参照してください。</a>
      * <a href="https://aka.ms/fluent-ui-icons" target="_blank">Fluent アイコンを試す (Fluent UI)</a>
      * <a href="https://github.com/microsoft/fluentui-system-icons" target="_blank">Fluent アイコンライブラリ (GitHub) を取得する</a>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-iconography.png" alt-text="Microsoft Teams UI Kit の概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="typography"></a>文字体裁

:::row:::

   :::column span="3":::

      Teams では、タイプランプに対して Meirui を使用して、階層を作成し、読みやすくするために、さまざまなフォントサイズと重みを使用しています。

      <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全な文字体裁のガイドライン (Figma) を参照してください。</a>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-typography.png" alt-text="Microsoft Teams UI Kit の概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="copy-and-content"></a>コピーとコンテンツ

:::row:::

   :::column span="3":::

      Teams の一部としては、一般にアプリコピーが次の [Microsoft 音声原則](https://docs.microsoft.com/style-guide/brand-voice-above-all-simple-human)に従う必要があります。これには、ウォームと緩和された、明瞭で明瞭で、すぐに手を貸します。

      <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全コピーとコンテンツのガイドラインを参照してください (bot への書き込みを含む) (Figma)</a>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-copy-and-content.png" alt-text="Microsoft Teams UI Kit の概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="brand-expression"></a>ブランド式

:::row:::

   :::column span="3":::

      アプリアイコンは、自分のブランドを Teams ユーザーに伝えるのに長い時間がかかる場合があります。 また、アイコンデザインの権限を取得することも、アプリを AppSource に [発行](../../concepts/build-and-test/apps-package.md) するために重要です。

      <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なブランド式のガイドライン (Figma) を参照してください。</a>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-branding.png" alt-text="Microsoft Teams UI Kit の概念図。" border="false":::

   :::column-end:::
:::row-end:::
