---
title: 設計ガイドラインのリファレンス
description: アプリで色を使用するためのガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスコンポーネントの色
ms.openlocfilehash: dab223891e88615b52386d3692d4a98607d6d449
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409065"
---
# <a name="color"></a>色

背景、通知、テキスト、およびボタンに対して承認されたニュートラルパレットを使用すると、アプリが Teams での自宅をよりよく理解できるようになります。 Teams には2つの色のテーマ (明るい色と濃) があるため、アプリが両方のテーマで快適に見えるようにすることをお勧めします。

### <a name="app-black-252423"></a>$app-黒 (#252423)

最も一般的に使用されるテキストの色です。 テキストには5つの不透明度レベルで使用します。 テキストは、主に100%、74%、64% の不透明度で使用する必要があります。これはアクセス可能なためです。 52% と36% のテキストは、アクセスできないため、慎重に使用する必要があります。

[!include[Appblack color and text](~/includes/design/color-image-appblack-text.html)]

1. 100%-ヘッダーとベーステキスト
2. 74%-ラベル、小見出し、attributions、アイコンの各ボタン
3. 64%-メッセージプレビュー、ヘルプテキスト (表示されません)
4. 52%-タイムスタンプ
5. 36%-無効なテキスト

また、 `$app-black` UI 要素によっては、他の opacities でも使用されます。

[!include[Appblack color and text](~/includes/design/color-image-appblack-ui.html)]

1. 14%-バナーの背景
2. 5%-無効にされたボタンとカードの罫線

### <a name="default-theme-color-ramp"></a>既定のテーマの色のランプ

「Pen [Microsoft Teams デザインガイドライン-CodePen の既定のテーマカラーランプ](https://codepen.io/msteams/pen/KyPmqL/) 」を参照してください。

<iframe height='620' scrolling='no' title='Microsoft Teams 設計ガイドライン-既定のテーマの色のランプ' src='//codepen.io/msteams/embed/KyPmqL/?height=682&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><a href='https://codepen.io'>CodePen</a>の microsoft teams (<a href='https://codepen.io/msteams'>@msteams</a>) による、microsoft teams の既定のテーマの色のランプについては、「Pen <a href='https://codepen.io/msteams/pen/KyPmqL/'>microsoft teams 設計ガイドライン</a>」を参照してください。
</iframe>

### <a name="other-default-theme-colors"></a>その他の既定のテーマの色

「Pen [Microsoft Teams の設計ガイドライン-CodePen 上のその他の既定のテーマの色](https://codepen.io/msteams/pen/zPOdYJ/) 」を参照してください。

<iframe height='392' scrolling='no' title='Microsoft Teams の設計ガイドライン-その他の既定のテーマの色' src='//codepen.io/msteams/embed/zPOdYJ/?height=442&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><a href='https://codepen.io'>CodePen</a>の microsoft teams (<a href='https://codepen.io/msteams'>@msteams</a>) 別<a href='https://codepen.io/msteams/pen/zPOdYJ/'>の既定のテーマの色</a>については、「Pen microsoft teams の設計ガイドライン」を参照してください。
</iframe>

### <a name="dark-theme-color-ramp"></a>暗いテーマの色のランプ

CodePen の Pen [Microsoft Teams デザインガイドライン-濃いテーマの色ランプ](https://codepen.io/msteams/pen/BmBwjx/) を参照してください。

<iframe height='798' scrolling='no' title='Microsoft Teams の設計ガイドライン-濃いテーマの色のランプ' src='//codepen.io/msteams/embed/BmBwjx/?height=846&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><a href='https://codepen.io'>CodePen</a>の microsoft teams (<a href='https://codepen.io/msteams'>@msteams</a>) ごとに、「Pen <a href='https://codepen.io/msteams/pen/BmBwjx/'>microsoft teams design ガイドライン-濃いテーマのカラーランプ</a>」を参照してください。
</iframe>

> **注:** Msteams ui のコアライブラリには、変数としてコード化された実際の値があります。 これらの変数は、色が更新された場合に役立ちます。


### <a name="other-dark-theme-colors"></a>その他の暗いテーマの色

「Pen [Microsoft Teams の設計ガイドライン-CodePen 上の暗いテーマの色](https://codepen.io/msteams/pen/zPOEXN/) 」を参照してください。

<iframe height='390' scrolling='no' title='Microsoft Teams の設計ガイドライン-その他の暗いテーマの色' src='//codepen.io/msteams/embed/zPOEXN/?height=442&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><a href='https://codepen.io'>CodePen</a>の microsoft teams (<a href='https://codepen.io/msteams'>@msteams</a>) による<a href='https://codepen.io/msteams/pen/zPOEXN/'>その他の暗いテーマの色</a>については、「Pen microsoft teams の設計ガイドライン」を参照してください。
</iframe>
