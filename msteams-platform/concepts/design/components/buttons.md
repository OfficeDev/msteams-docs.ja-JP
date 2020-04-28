---
title: 設計ガイドラインのリファレンス
description: アプリでボタン、リンク、コントロールを使用するためのガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスコンポーネントボタンリンクの色
ms.openlocfilehash: b9325980c38048ee250ace6b00f1ed29c6cbea8d
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914589"
---
# <a name="buttons-links-and-controls"></a>ボタン、リンク、コントロール

---

## <a name="button-types"></a>ボタンの種類

ボタンのスタイルを設定すると、どのような種類の動作が発生したかを伝えることができます。 さまざまな強調レベルを表示するように書式設定されたさまざまなボタンを維持しています。

ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを含めることができます。 階層内のさまざまなレベルを通信するために、各カテゴリ内に主ボタンと副ボタンを設計しました。

### <a name="fluent-design-system"></a>Fluent デザインシステム

Fluent UI は、web およびデスクトップコンポーネントの状態、スタイル設定、およびアクセシビリティに関するガイダンスを提供します。 Teams プラットフォームのボタンは、さまざまな強調レベルを表示するように書式設定できます。 HTML および CSS の16進カラー値については、「[FLUENT UI ボタンの色](https://fluentsite.z22.web.core.windows.net/components/button/definition?showCode=false&showRtl=false&showTransparent=false&showVariables=true#types-emphasis) *」を参照してください*。  

### <a name="text-buttons"></a>テキストボタン

ダイアログボックスでは、右の主なアクションから始めて、右にボタンを配置する必要があります。 カードでは、ボタンは左揃えに配置されます。

Teams のボタンスタイル

デスクトップクライアント[!include[Button states](~/includes/design/buttons-image-states.html)]

モバイルクライアント[!include[Mobile button states](~/includes/design/buttons-mobile-image-states.html)]

ダイアログボタン[!include[Dialog buttons](~/includes/design/buttons-image-dialog.html)]

カードボタンの状態[!include[Card button states](~/includes/design/buttons-image-cardstates.html)]

カードボタン[!include[Card buttons](~/includes/design/buttons-image-card.html)]

### <a name="icon-buttons"></a>アイコンボタン

アイコンボタンは、アクションを呼び出すことができます。また、オンとオフを切り替えることもできます。
[!include[Icon buttons](~/includes/design/buttons-image-icon.html)]

場合によっては、アイコンとテキストをペアにして強調を増やすことができます。
[!include[Icon text buttons](~/includes/design/buttons-image-icontext.html)]

### <a name="miscellaneous-buttons"></a>[その他] ボタン

#### <a name="desktop-clients"></a>デスクトップクライアント
ラジアルボタン、チェックボックス、およびトグルスイッチ。<br/>
[!include[Other buttons](~/includes/design/buttons-image-others.html)]

#### <a name="mobile-clients"></a>モバイルクライアント
ラジアルボタン、チェックボックス、およびトグルスイッチ。<br/>
[!include[Other buttons](~/includes/design/buttons-image-mobile-others.html)]

---

## <a name="links"></a>リンク

インラインテキストリンクの承認されたスタイルを次に示します。
[!include[Approved link styles](~/includes/design/links-image-text.html)]

---

## <a name="style"></a>Style

## <a name="size-and-padding"></a>サイズとスペース

テキストボタン、アイコン、およびコントロールは、すべてのコントロールを視覚的に配置し、一貫性を持たせるために、間隔レベルのコンテナー内に含まれています。
[!include[Size and padding](~/includes/design/style-image-size.html)]

### <a name="rounded-corners"></a>角の丸み

テキストボタンの角の半径は3px です。
[!include[Rounded corners](~/includes/design/style-image-corners.html)]

### <a name="button-text"></a>ボタンテキスト

ボタンのテキストには、ローカライズと読みやすくするために、文の大文字を使用します。 (つまり、語句または文の最初の単語の最初の文字のみを大文字にします)。
