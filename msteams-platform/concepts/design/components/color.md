---
title: 設計ガイドラインのリファレンス
description: アプリで色を使用するためのガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスコンポーネントの色
ms.openlocfilehash: c6c0a421abbfc23959c7873d95aa89ca7cc685f2
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674733"
---
# <a name="color"></a><span data-ttu-id="85a57-104">色</span><span class="sxs-lookup"><span data-stu-id="85a57-104">Color</span></span>

<span data-ttu-id="85a57-105">背景、通知、テキスト、およびボタンに対して承認されたニュートラルパレットを使用すると、アプリが Teams での自宅をよりよく理解できるようになります。</span><span class="sxs-lookup"><span data-stu-id="85a57-105">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="85a57-106">Teams には2つの色のテーマ (明るい色と濃) があるため、アプリが両方のテーマで快適に見えるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="85a57-106">Since Teams has two color themes (light and dark), it’s a good idea to make sure your app looks great in both themes.</span></span>

### <a name="app-black-252423"></a><span data-ttu-id="85a57-107">$app-黒 (#252423)</span><span class="sxs-lookup"><span data-stu-id="85a57-107">$app-black (#252423)</span></span>

<span data-ttu-id="85a57-108">最も一般的に使用されるテキストの色です。</span><span class="sxs-lookup"><span data-stu-id="85a57-108">Our most commonly-used text color.</span></span> <span data-ttu-id="85a57-109">テキストには5つの不透明度レベルで使用します。</span><span class="sxs-lookup"><span data-stu-id="85a57-109">We use it at five levels of opacity for text.</span></span> <span data-ttu-id="85a57-110">テキストは、主に100%、74%、64% の不透明度で使用する必要があります。これはアクセス可能なためです。</span><span class="sxs-lookup"><span data-stu-id="85a57-110">Text should mainly be used at 100%, 74%, 64% opacity since it is accessible.</span></span> <span data-ttu-id="85a57-111">52% と36% のテキストは、アクセスできないため、慎重に使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85a57-111">Text at 52% and 36% should be used sparingly since it is not accessible.</span></span>

[!include[Appblack color and text](~/includes/design/color-image-appblack-text.html)]

1. <span data-ttu-id="85a57-112">100%-ヘッダーとベーステキスト</span><span class="sxs-lookup"><span data-stu-id="85a57-112">100% - Headers and base text</span></span>
2. <span data-ttu-id="85a57-113">74%-ラベル、小見出し、attributions、アイコンの各ボタン</span><span class="sxs-lookup"><span data-stu-id="85a57-113">74% - Labels, subheads, attributions, and icon buttons</span></span>
3. <span data-ttu-id="85a57-114">64%-メッセージプレビュー、ヘルプテキスト (表示されません)</span><span class="sxs-lookup"><span data-stu-id="85a57-114">64% - Message previews, help text (not shown)</span></span>
4. <span data-ttu-id="85a57-115">52%-タイムスタンプ</span><span class="sxs-lookup"><span data-stu-id="85a57-115">52% - Timestamps</span></span>
5. <span data-ttu-id="85a57-116">36%-無効なテキスト</span><span class="sxs-lookup"><span data-stu-id="85a57-116">36% - Disabled text</span></span>

<span data-ttu-id="85a57-117">また、UI `$app-black`要素によっては、他の opacities でも使用されます。</span><span class="sxs-lookup"><span data-stu-id="85a57-117">We also use `$app-black` at other opacities for some UI elements:</span></span>

[!include[Appblack color and text](~/includes/design/color-image-appblack-ui.html)]

1. <span data-ttu-id="85a57-118">14%-バナーの背景</span><span class="sxs-lookup"><span data-stu-id="85a57-118">14% - Banner backgrounds</span></span>
2. <span data-ttu-id="85a57-119">5%-無効にされたボタンとカードの罫線</span><span class="sxs-lookup"><span data-stu-id="85a57-119">5% - Disabled button and card borders</span></span>

### <a name="default-theme-color-ramp"></a><span data-ttu-id="85a57-120">既定のテーマの色のランプ</span><span class="sxs-lookup"><span data-stu-id="85a57-120">Default theme color ramp</span></span>

<span data-ttu-id="85a57-121">「Pen [Microsoft Teams デザインガイドライン-CodePen の既定のテーマカラーランプ](https://codepen.io/msteams/pen/KyPmqL/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85a57-121">See the Pen [Microsoft Teams design guidelines - default theme color ramp](https://codepen.io/msteams/pen/KyPmqL/) on CodePen.</span></span>

<iframe height='620' scrolling='no' title='<span data-ttu-id="85a57-122">Microsoft Teams 設計ガイドライン-既定のテーマの色のランプ</span><span class="sxs-lookup"><span data-stu-id="85a57-122">Microsoft Teams design guidelines - default theme color ramp</span></span>' src='//codepen.io/msteams/embed/KyPmqL/?height=682&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="85a57-123"><a href='https://codepen.io'>CodePen</a>の microsoft teams (<a href='https://codepen.io/msteams'>@msteams</a>) による、microsoft teams の既定のテーマの色のランプについては、「Pen <a href='https://codepen.io/msteams/pen/KyPmqL/'>microsoft teams 設計ガイドライン</a>」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85a57-123">See the Pen <a href='https://codepen.io/msteams/pen/KyPmqL/'>Microsoft Teams design guidelines - default theme color ramp</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

### <a name="other-default-theme-colors"></a><span data-ttu-id="85a57-124">その他の既定のテーマの色</span><span class="sxs-lookup"><span data-stu-id="85a57-124">Other default theme colors</span></span>

<span data-ttu-id="85a57-125">「Pen [Microsoft Teams の設計ガイドライン-CodePen 上のその他の既定のテーマの色](https://codepen.io/msteams/pen/zPOdYJ/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85a57-125">See the Pen [Microsoft Teams design guidelines - other default theme colors](https://codepen.io/msteams/pen/zPOdYJ/) on CodePen.</span></span>

<iframe height='392' scrolling='no' title='<span data-ttu-id="85a57-126">Microsoft Teams の設計ガイドライン-その他の既定のテーマの色</span><span class="sxs-lookup"><span data-stu-id="85a57-126">Microsoft Teams design guidelines - other default theme colors</span></span>' src='//codepen.io/msteams/embed/zPOdYJ/?height=442&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="85a57-127"><a href='https://codepen.io'>CodePen</a>の microsoft teams (<a href='https://codepen.io/msteams'>@msteams</a>) 別<a href='https://codepen.io/msteams/pen/zPOdYJ/'>の既定のテーマの色</a>については、「Pen microsoft teams の設計ガイドライン」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85a57-127">See the Pen <a href='https://codepen.io/msteams/pen/zPOdYJ/'>Microsoft Teams design guidelines - other default theme colors</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

### <a name="dark-theme-color-ramp"></a><span data-ttu-id="85a57-128">暗いテーマの色のランプ</span><span class="sxs-lookup"><span data-stu-id="85a57-128">Dark theme color ramp</span></span>

<span data-ttu-id="85a57-129">CodePen の Pen [Microsoft Teams デザインガイドライン-濃いテーマの色ランプ](https://codepen.io/msteams/pen/BmBwjx/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85a57-129">See the Pen [Microsoft Teams design guidelines - dark theme color ramp](https://codepen.io/msteams/pen/BmBwjx/) on CodePen.</span></span>

<iframe height='798' scrolling='no' title='<span data-ttu-id="85a57-130">Microsoft Teams の設計ガイドライン-濃いテーマの色のランプ</span><span class="sxs-lookup"><span data-stu-id="85a57-130">Microsoft Teams design guidelines - dark theme color ramp</span></span>' src='//codepen.io/msteams/embed/BmBwjx/?height=846&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="85a57-131"><a href='https://codepen.io'>CodePen</a>の microsoft teams (<a href='https://codepen.io/msteams'>@msteams</a>) ごとに、「Pen <a href='https://codepen.io/msteams/pen/BmBwjx/'>microsoft teams design ガイドライン-濃いテーマのカラーランプ</a>」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85a57-131">See the Pen <a href='https://codepen.io/msteams/pen/BmBwjx/'>Microsoft Teams design guidelines - dark theme color ramp</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

### <a name="other-dark-theme-colors"></a><span data-ttu-id="85a57-132">その他の暗いテーマの色</span><span class="sxs-lookup"><span data-stu-id="85a57-132">Other dark theme colors</span></span>

<span data-ttu-id="85a57-133">「Pen [Microsoft Teams の設計ガイドライン-CodePen 上の暗いテーマの色](https://codepen.io/msteams/pen/zPOEXN/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85a57-133">See the Pen [Microsoft Teams design guidelines - other dark theme colors](https://codepen.io/msteams/pen/zPOEXN/) on CodePen.</span></span>

<iframe height='390' scrolling='no' title='<span data-ttu-id="85a57-134">Microsoft Teams の設計ガイドライン-その他の暗いテーマの色</span><span class="sxs-lookup"><span data-stu-id="85a57-134">Microsoft Teams design guidelines - other dark theme colors</span></span>' src='//codepen.io/msteams/embed/zPOEXN/?height=442&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="85a57-135"><a href='https://codepen.io'>CodePen</a>の microsoft teams (<a href='https://codepen.io/msteams'>@msteams</a>) による<a href='https://codepen.io/msteams/pen/zPOEXN/'>その他の暗いテーマの色</a>については、「Pen microsoft teams の設計ガイドライン」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85a57-135">See the Pen <a href='https://codepen.io/msteams/pen/zPOEXN/'>Microsoft Teams design guidelines - other dark theme colors</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>