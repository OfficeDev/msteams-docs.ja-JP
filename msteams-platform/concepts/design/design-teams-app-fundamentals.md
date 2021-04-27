---
title: アプリを設計する - 基本について
description: レイアウト、配色など、Microsoft Teams アプリの設計の基本について説明します。
author: heath-hamilton
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: c0edfe7ac538fc27b7f255cdd09d2853f6f4cebc
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020773"
---
# <a name="microsoft-teams-app-design-fundamentals"></a>Microsoft Teams アプリの設計の基本

Teams アプリの設計の基本について簡単に学ぶ。 包括的なガイダンスと例については <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">、「Microsoft Teams UI Kit (Figma)」を参照してください</a>。

## <a name="layout"></a>レイアウト

:::row:::

   :::column span="3":::

      Teams は、デザイン コンポーネント間の一貫したエレガントな関係を確保するために、グリッド レイアウトに依存しています。 グリッドの 4 ピクセルベースユニットを使用すると、コンポーネントは Teams のすべての表示サイズにわたって一貫して拡大縮小できます。

      <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なレイアウト ガイドライン (Figma) を参照してください。</a>

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-layout.png" alt-text="Microsoft Teams UI キットの概念イメージ。" border="false":::
   :::column-end:::

:::row-end:::

## <a name="avatars"></a>アバター

:::row:::

   :::column span="3":::

      アバターは、Teams の人物、チーム、ボット、またはエンティティのグラフィック表現です。 アバター グループは、多くの場合、垂直空間を保持する方法で、ライブ アクティビティまたは名簿を表す場合に使用されます。 

      <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なアバター ガイドライン (Figma) を参照してください。</a>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-avatars.png" alt-text="Teams UI キットの概念イメージ。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="colors"></a>色

:::row:::

   :::column span="3":::

      Teams Web とデスクトップは既定の (明るいテーマ、暗いテーマ、ハイコントラストテーマ) をサポートし、Teams モバイルは明るいテーマと暗いテーマをサポートします。 各テーマには独自の配色があります。

      <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">フル カラー ガイドラインと使用可能なカラー トークン (Figma) を参照してください。</a>

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-color.png" alt-text="Microsoft Teams UI キットの概念イメージ。" border="false":::
   :::column-end:::

:::row-end:::

## <a name="iconography"></a>アイコン

:::row:::

   :::column span="3":::

      Teams アプリは、Fluent UI によって提供されるアイコンを使用します。

### <a name="resources"></a>リソース

      * <a href="https://www.figma.com/community/file/836835755999342788" target="_blank">最新の Fluent アイコン (Figma) を参照してください。</a>
      * <a href="https://aka.ms/fluent-ui-icons" target="_blank">Fluent アイコンを試す (Fluent UI)</a>
      * <a href="https://github.com/microsoft/fluentui-system-icons" target="_blank">Fluent アイコン ライブラリを取得する (GitHub)</a>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-iconography.png" alt-text="Microsoft Teams UI Kit の概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="typography"></a>文字体裁

:::row:::

   :::column span="3":::

      Teams では、Segoe UI を使用して、その種類のランプとさまざまなフォント サイズと重みを使用して、階層を作成し、読みやすさを確保します。

      <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なタイポグラフィ ガイドライン (Figma) を参照してください。</a>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-typography.png" alt-text="Microsoft Teams UI キットの概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="copy-and-content"></a>コピーとコンテンツ

:::row:::

   :::column span="3":::

      Teams の一部を感じるには、アプリ コピー全般で、暖かくリラックスした、鮮明で明確で、手を貸す準備ができているという [Microsoft](https://docs.microsoft.com/style-guide/brand-voice-above-all-simple-human)音声の原則に従う必要があります。

      <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なコピーとコンテンツのガイドライン (ボット用の書き込みを含む) を参照してください (Figma)</a>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-copy-and-content.png" alt-text="Microsoft Teams UI キットの概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="brand-expression"></a>ブランド式

:::row:::

   :::column span="3":::

      アプリアイコンは、Teams ユーザーにブランドを伝えるのに長い道のりを行く可能性があります。 アプリを AppSource に発行する場合も、アイコン [の](../../concepts/build-and-test/apps-package.md) デザインを正しい方法で取得することが重要です。

      <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なブランド表現のガイドライン (Figma) を参照してください。</a>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-branding.png" alt-text="Microsoft Teams UI キットの概念フォーム。" border="false":::

   :::column-end:::
:::row-end:::
