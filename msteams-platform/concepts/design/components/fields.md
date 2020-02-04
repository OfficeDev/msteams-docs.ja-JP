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
# <a name="fields-and-flyouts"></a><span data-ttu-id="33736-104">フィールドと flyouts</span><span class="sxs-lookup"><span data-stu-id="33736-104">Fields and flyouts</span></span>

---

## <a name="fields"></a><span data-ttu-id="33736-105">フィールド</span><span class="sxs-lookup"><span data-stu-id="33736-105">Fields</span></span>

<span data-ttu-id="33736-106">フィールドは、ユーザーがテキストを入力できる領域です。</span><span class="sxs-lookup"><span data-stu-id="33736-106">Fields are areas where users can input text.</span></span>

### <a name="padding-and-size"></a><span data-ttu-id="33736-107">スペースとサイズ</span><span class="sxs-lookup"><span data-stu-id="33736-107">Padding and size</span></span>

<span data-ttu-id="33736-108">1行のテキストフィールドは、他のコンポーネントの高さと一致するように、固定の高さが間隔です。</span><span class="sxs-lookup"><span data-stu-id="33736-108">Single-line text fields are a fixed height of 32px to match the height of other components.</span></span> <span data-ttu-id="33736-109">Description フィールドなどの一部のテキストフィールドは、より多くのテキストが表示されるように垂直方向に縦に並んでいる場合があります。</span><span class="sxs-lookup"><span data-stu-id="33736-109">Some text fields such as description fields may be taller vertically to allow more text.</span></span>
[!include[Padding and size](~/includes/design/fields-image-padding.html)]

### <a name="states"></a><span data-ttu-id="33736-110">示し</span><span class="sxs-lookup"><span data-stu-id="33736-110">States</span></span>

<span data-ttu-id="33736-111">テキストフィールドの状態を次に示します。</span><span class="sxs-lookup"><span data-stu-id="33736-111">These are the states of our text fields.</span></span> <span data-ttu-id="33736-112">テキストフィールドはさまざまな状態で存在します。</span><span class="sxs-lookup"><span data-stu-id="33736-112">Text fields exist in different states.</span></span> <span data-ttu-id="33736-113">次の9つのシナリオ (上から下) への専用の設計があります。たとえば、[テキストフィールド]、[フォーカスがあるキーボード]、フィールド内のカーソル、エラー処理が正常に完了した、エラー処理が失敗した、テキストがクリアされています。フィールド (X アイコンを含む)、検索フィールド (検索アイコンを含む)、読み込みフィールド、および無効なフィールド。</span><span class="sxs-lookup"><span data-stu-id="33736-113">We have specific designs dedicated to nine possible scenarios, including (top to bottom): Resting text field, Keyboard in focus and cursor inside the field, Keyboard in focus with text entered, Error handling has succeeded, Error handling has failed, Clear text field (including an X icon), Search field (including a Search icon), Loading field, and a Disabled field.</span></span>
[!include[Field states](~/includes/design/fields-image-states.html)]

### <a name="formatting-help-text-and-labels"></a><span data-ttu-id="33736-114">ヘルプのテキストとラベルの書式設定</span><span class="sxs-lookup"><span data-stu-id="33736-114">Formatting help text and labels</span></span>

<span data-ttu-id="33736-115">フィールドにプレースホルダーテキストを含めると、必要な情報の種類の例を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="33736-115">Fields can contain placeholder text to give an example of the kind of information that is required.</span></span> <span data-ttu-id="33736-116">また、ユーザーにより多くのコンテキストを提供するラベルを保持することもできます。</span><span class="sxs-lookup"><span data-stu-id="33736-116">They can also hold labels that give the user more context.</span></span> <span data-ttu-id="33736-117">フィールド内では、テキストを常に左寄せにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="33736-117">Within a field, your text should always be justified left.</span></span> <span data-ttu-id="33736-118">ここでは、文の大文字と小文字を使用しています。</span><span class="sxs-lookup"><span data-stu-id="33736-118">We use sentence casing throughout here, as well.</span></span>

<span data-ttu-id="33736-119">Microsoft では、12 pt (caption) で Yu Gothic UI Regular を使用し、ラベルには $app グレー-02 を使用しています。</span><span class="sxs-lookup"><span data-stu-id="33736-119">We use Segoe UI Regular at 12 pt (caption) and $app-gray-02 for labels.</span></span> <span data-ttu-id="33736-120">ヘルプテキストについては、14 pt (base) では MEIRUI レギュラーを使用し、グレースケールでは $app します。</span><span class="sxs-lookup"><span data-stu-id="33736-120">For help text, we use Segoe UI Regular at 14 pt (base) and $app-gray-02.</span></span>
[!include[Fields typography](~/includes/design/fields-image-typography.html)]

---

## <a name="flyouts"></a><span data-ttu-id="33736-121">Flyouts</span><span class="sxs-lookup"><span data-stu-id="33736-121">Flyouts</span></span>

<span data-ttu-id="33736-122">Flyouts はダイアログよりも軽量で、すぐに消去することができます。</span><span class="sxs-lookup"><span data-stu-id="33736-122">Flyouts are more lightweight than dialogs and can be dismissed quickly.</span></span> <span data-ttu-id="33736-123">これらには、ボタン、フィールド、およびその他のコンポーネントを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="33736-123">They can contain buttons, fields, and other components.</span></span>
[!include[Flyouts](~/includes/design/flyouts-image.html)]

### <a name="sizing-and-padding"></a><span data-ttu-id="33736-124">サイズとスペース</span><span class="sxs-lookup"><span data-stu-id="33736-124">Sizing and padding</span></span>

<span data-ttu-id="33736-125">コンテンツの左側と右側には、16ピクセルのパディングをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="33736-125">We recommend a 16px padding to the left and right of the content.</span></span>
[!include[Flyouts size and padding](~/includes/design/flyouts-image-sizepadding.html)]

### <a name="placement"></a><span data-ttu-id="33736-126">Placement</span><span class="sxs-lookup"><span data-stu-id="33736-126">Placement</span></span>

<span data-ttu-id="33736-127">Flyouts はコンテキストであり、トリガーされた要素の上、下、または横に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="33736-127">Flyouts are contextual and should be placed above, below, or beside the element that triggered it.</span></span>

### <a name="scrolling"></a><span data-ttu-id="33736-128">量</span><span class="sxs-lookup"><span data-stu-id="33736-128">Scrolling</span></span>

<span data-ttu-id="33736-129">ヘッダーは、スクロールされるコンテンツのコンテキストを提供するために残されています。</span><span class="sxs-lookup"><span data-stu-id="33736-129">The header remains in place to give context to the content being scrolled.</span></span>
[!include[Flyouts scrolling](~/includes/design/flyouts-image-scrolling.html)]

## <a name="mobile"></a><span data-ttu-id="33736-130">Mobile</span><span class="sxs-lookup"><span data-stu-id="33736-130">Mobile</span></span>

<span data-ttu-id="33736-131">フィールドは、ユーザーからの入力を受け付けるテキスト入力ボックスです。</span><span class="sxs-lookup"><span data-stu-id="33736-131">Fields are text-entry boxes that accept input from users.</span></span> <span data-ttu-id="33736-132">ポップアップメニューは、上部のウィンドウに表示される水平のポップアップウィンドウで、アイテムの詳細を表示するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="33736-132">Flyout menus are horizontal pop-up windows that appear from the top pane and can be used to show more detail about an item.</span></span>

### <a name="field-controls"></a><span data-ttu-id="33736-133">フィールド コントロール</span><span class="sxs-lookup"><span data-stu-id="33736-133">Field Controls</span></span>

[!include[Mobile fields](~/includes/design/fields-mobile-image.html)]

### <a name="flyout-menu-list-controls"></a><span data-ttu-id="33736-134">ポップアップメニューリストコントロール</span><span class="sxs-lookup"><span data-stu-id="33736-134">Flyout menu list controls</span></span>

[!include[Mobile flyout menu controls](~/includes/design/flyout-menu-mobile-image.html)]
