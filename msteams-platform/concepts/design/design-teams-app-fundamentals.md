---
title: アプリを設計する - デザイン システムを理解する
description: アバター、レイアウト、アイコン、配色など、Microsoft Teams アプリの設計の基本について説明します。
author: heath-hamilton
ms.localizationpriority: high
ms.author: lajanuar
ms.topic: overview
keywords: レイアウト グリッド アバター アイコン segoe ui タイポグラフィ
ms.openlocfilehash: d4b8d610de0575024db5d7140c0452b00655ef91
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111298"
---
# <a name="microsoft-teams-app-design-system"></a>Microsoft Teams アプリ設計システム

Teams アプリ設計の基礎について簡単に説明します。 包括的なガイダンスと例については、「<a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI キット (Figma)</a>」 を参照してください。

## <a name="layout"></a>レイアウト

:::row:::

   :::column span="3":::

      Teams は、デザイン コンポーネント間の一貫性と洗練された関係を確保するためにグリッド レイアウトに依存しています。 グリッドの 4 ピクセル ベース ユニットを使用すると、コンポーネントは Teams のすべてのディスプレイ サイズにわたって一貫してスケーリングできます。

      * [完全なレイアウト ガイドライン (Figma) を参照してください](https://www.figma.com/community/file/916836509871353159)
      * [レイアウト (Fluent UI) の実装](https://developer.microsoft.com/fluentui#/styles/web/layout)

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-layout.png" alt-text="Teams レイアウトの概念図。" border="false":::
   :::column-end:::

:::row-end:::

## <a name="avatars"></a>アバター

:::row:::

   :::column span="3":::

      アバターは、Teams 内の人物、チーム、ボット、またはエンティティをグラフィカルに表したものです。 アバター グループは、多くの場合、ライブ アクティビティを伝達したり、縦のスペースを保持する方法で名簿を表すために使用されます。 

      * <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なアバター ガイドライン (Figma) を参照する</a>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-avatars.png" alt-text="Teams アバターの概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="icons"></a>アイコン

:::row:::

   :::column span="3":::

      アプリのプライマリ アイコンは、ブランドを Teams ユーザーに伝達するのに長い道のりを行くことができます。 アイコン デザインを適切に取得することも、Teams ストアに[アプリを発行する](../../concepts/build-and-test/apps-package.md)場合に重要です。

      アプリ全体で Fluent UI アイコンを使用することもできます。

      * <a href="https://www.figma.com/community/file/836835755999342788" target="_blank">最新の Fluent アイコン セット (Figma) を取得する</a>
      * [アイコン (Fluent UI) を実装する](https://developer.microsoft.com/fluentui#/styles/web/icons)

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-iconography.png" alt-text="Teams アイコンの概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="type"></a>種類

:::row:::

   :::column span="3":::

      Teams は、タイプ ランプとさまざまなフォント サイズやウェイトに Segoe UI を使用することで、階層を作成し、読みやすさを確保しています。

      * <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なガイドライン (Figma) を参照してください</a>
      * [文字体裁 (Fluent UI) を実装する](https://developer.microsoft.com/fluentui#/styles/web/typography)

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-typography.png" alt-text="Teams 文字体裁の概念図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="colors"></a>色

:::row:::

   :::column span="3":::

      Teams Web とデスクトップでは既定のテーマ (明るいテーマ)、ダーク テーマ、ハイコントラスト テーマがサポートされていますが、Teams モバイルでは明るいテーマとダーク テーマがサポートされています。 各テーマには独自の配色があります。

      * <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">フル カラー ガイドラインと使用可能なカラー トークンを参照してください (Figma)</a>
      * [色を実装する (Fluent UI)](https://fluentsite.z22.web.core.windows.net/0.51.7/colors)

   :::column-end:::
   :::column span="1":::
      :::image type="content" source="../../assets/images/design-guidelines/teams-color.png" alt-text="Teams 色の概念図。" border="false":::
   :::column-end:::

:::row-end:::

## <a name="shape-and-elevation"></a>図形と昇格

:::row:::

   :::column span="3":::

      図形と昇格を使用して、アプリに追加の階層を作成できます。 

      * <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全な図形と昇格のガイドラインを参照してください (Figma)</a>
      * [図形と昇格を実装する (Fluent UI)](https://developer.microsoft.com/fluentui#/styles/web/elevation)

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/shape-and-elevation.png" alt-text="図形と昇格の概念。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="copy-and-content"></a>コピーとコンテンツ

:::row:::

   :::column span="3":::

      Teams の一部であると感じるには、一般に、アプリのコピーは次の [ [Microsoft 音声原則]](/style-guide/brand-voice-above-all-simple-human) に従う必要があります。暖かくリラックスし、鮮明でクリアで、すぐに使用できます。

      * <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">完全なコピーとコンテンツのガイドライン (ボットの作成を含む) (Figma) を参照してください</a>

   :::column-end:::
   :::column span="1":::

      :::image type="content" source="../../assets/images/design-guidelines/teams-copy-and-content.png" alt-text="コピーとコンテンツの概念イメージ。" border="false":::

   :::column-end:::
:::row-end:::
