---
title: タブ余白の変更
author: surbhigupta
description: このモジュールでは、タブの余白を削除すると、アプリの構築エクスペリエンスが向上する方法について説明します。
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: d99b58529cf15da4357d44d6bcfdcc9801b995ba
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558283"
---
# <a name="tab-margin-changes"></a>タブ余白の変更

このドキュメントでは、Microsoft Teams のすべてのタブの余白を削除すると、アプリのビルド エクスペリエンスが向上する方法について説明します。 これは、2021 年に Teams で導入された機能強化です。
すべてのタブの余白を削除することで、Teams に対してよりネイティブに見えるアプリを構築できます。 余白が削除されたタブは、Microsoft Teams の [UI キットのデザイン](~/tabs/design/tabs.md)と一致します。 ほとんどのアプリでは、余白のない強化された外観が得られます。

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="タブの wit と余白なし":::

> [!NOTE]
> モバイル クライアントで表示されるタブには余白がないため、この機能はモバイル クライアントには適用されません。

## <a name="guidelines"></a>ガイドライン

タブ余白の削除は、タブを使用する Teams アプリに影響します。 このような場合は、必要なタブ デザインの周囲に余白を追加できます。 運用環境のアプリデザインには、追加のパディング効果があります。つまり、Teams によって提供される余白とタブによって提供される余白です。ただし、余分なパディングは一時的なものであり、数週間後に消え、アプリが提供するパディングだけが残ります。

## <a name="faq"></a>FAQ

**ヘッダー バーやタスク バーなどのアプリ クロムがデザインの端に触れても問題ありませんか?**

はい、これは問題ありません。Teams ではこのような設計が推奨されます。 アプリがネイティブと感じるのに役立ちます。

**テキスト、ロゴ、画像などのアプリ コンテンツがデザインの左端と右端に触れても問題ありませんか?**

いいえ。UI の端に触れないよう、すべてのアプリ コンテンツの左右に独自のパディングまたは余白を指定する必要があります。 必要に応じて、タブの上部に余白を追加することもできます。

**Teams が以前に適用したタブ余白のサイズは何ですか?**

* 左右: 20 ピクセル
* Top: 16 px
* 下: 0 ピクセル

> [!IMPORTANT]
>
> * 個人用タブ、(グループ) チャット タブ、会議タブ、チャネル タブなど、すべてのタブの余白が削除されます。
> * タブの余白の削除の変更は、すべてのタブに適用されます。 変更をオプトインまたはオプトアウトする方法はありません。
> * タブ余白の変更は、MICROSOFT Teams に依存して UI を囲む余白を提供するタブに影響を与える可能性があります。

## <a name="see-also"></a>関連項目

* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネル] または [グループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
