---
title: 設計ガイドラインのリファレンス
description: アプリでフィールドと flyouts を使用するためのガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスコンポーネントフィールドおよび flyouts
ms.openlocfilehash: 0f62d38bf961ae79b05c599638cefb3c76f46ed4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675054"
---
# <a name="fields-and-flyouts"></a>フィールドと flyouts

---

## <a name="fields"></a>フィールド

フィールドは、ユーザーがテキストを入力できる領域です。

### <a name="padding-and-size"></a>スペースとサイズ

1行のテキストフィールドは、他のコンポーネントの高さと一致するように、固定の高さが間隔です。 Description フィールドなどの一部のテキストフィールドは、より多くのテキストが表示されるように垂直方向に縦に並んでいる場合があります。
[!include[Padding and size](~/includes/design/fields-image-padding.html)]

### <a name="states"></a>示し

テキストフィールドの状態を次に示します。 テキストフィールドはさまざまな状態で存在します。 次の9つのシナリオ (上から下) への専用の設計があります。たとえば、[テキストフィールド]、[フォーカスがあるキーボード]、フィールド内のカーソル、エラー処理が正常に完了した、エラー処理が失敗した、テキストがクリアされています。フィールド (X アイコンを含む)、検索フィールド (検索アイコンを含む)、読み込みフィールド、および無効なフィールド。
[!include[Field states](~/includes/design/fields-image-states.html)]

### <a name="formatting-help-text-and-labels"></a>ヘルプのテキストとラベルの書式設定

フィールドにプレースホルダーテキストを含めると、必要な情報の種類の例を得ることができます。 また、ユーザーにより多くのコンテキストを提供するラベルを保持することもできます。 フィールド内では、テキストを常に左寄せにする必要があります。 ここでは、文の大文字と小文字を使用しています。

Microsoft では、12 pt (caption) で Yu Gothic UI Regular を使用し、ラベルには $app グレー-02 を使用しています。 ヘルプテキストについては、14 pt (base) では MEIRUI レギュラーを使用し、グレースケールでは $app します。
[!include[Fields typography](~/includes/design/fields-image-typography.html)]

---

## <a name="flyouts"></a>Flyouts

Flyouts はダイアログよりも軽量で、すぐに消去することができます。 これらには、ボタン、フィールド、およびその他のコンポーネントを含めることができます。
[!include[Flyouts](~/includes/design/flyouts-image.html)]

### <a name="sizing-and-padding"></a>サイズとスペース

コンテンツの左側と右側には、16ピクセルのパディングをお勧めします。
[!include[Flyouts size and padding](~/includes/design/flyouts-image-sizepadding.html)]

### <a name="placement"></a>Placement

Flyouts はコンテキストであり、トリガーされた要素の上、下、または横に配置する必要があります。

### <a name="scrolling"></a>量

ヘッダーは、スクロールされるコンテンツのコンテキストを提供するために残されています。
[!include[Flyouts scrolling](~/includes/design/flyouts-image-scrolling.html)]

## <a name="mobile"></a>Mobile

フィールドは、ユーザーからの入力を受け付けるテキスト入力ボックスです。 ポップアップメニューは、上部のウィンドウに表示される水平のポップアップウィンドウで、アイテムの詳細を表示するために使用できます。

### <a name="field-controls"></a>フィールド コントロール

[!include[Mobile fields](~/includes/design/fields-mobile-image.html)]

### <a name="flyout-menu-list-controls"></a>ポップアップメニューリストコントロール

[!include[Mobile flyout menu controls](~/includes/design/flyout-menu-mobile-image.html)]
