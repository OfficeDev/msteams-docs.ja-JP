---
title: 設計ガイドラインのリファレンス
description: アプリでダイアログを使用するためのガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスコンポーネントダイアログ
ms.openlocfilehash: d244eedde66085d41b1f356176a7775de304aaf4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674702"
---
# <a name="dialogs"></a><span data-ttu-id="61275-104">Dialogs</span><span class="sxs-lookup"><span data-stu-id="61275-104">Dialogs</span></span>

<span data-ttu-id="61275-105">ユーザーが中断する可能性があるため、ダイアログは慎重に使用する必要があります。ユーザーが終了する方法を明確にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="61275-105">Dialogs should be used sparingly since they can be disruptive, and should have a clear way for the user to exit.</span></span>

---

## <a name="sizes"></a><span data-ttu-id="61275-106">フェース</span><span class="sxs-lookup"><span data-stu-id="61275-106">Sizes</span></span>

<span data-ttu-id="61275-107">3つのダイアログサイズから選択できます。</span><span class="sxs-lookup"><span data-stu-id="61275-107">We have 3 dialog sizes to choose from.</span></span> <span data-ttu-id="61275-108">使用しているコンテンツに適したサイズを選択します。</span><span class="sxs-lookup"><span data-stu-id="61275-108">Choose the size that is appropriate for the content you have.</span></span>
[!include[Dialog sizes](~/includes/design/dialogs-image-sizes.html)]

---

## <a name="buttons"></a><span data-ttu-id="61275-109">ボタン</span><span class="sxs-lookup"><span data-stu-id="61275-109">Buttons</span></span>

<span data-ttu-id="61275-110">ボタンは右揃えで配置されます。</span><span class="sxs-lookup"><span data-stu-id="61275-110">Buttons are right-justified.</span></span>
<span data-ttu-id="61275-111">他のすべての要素 (チェックボックス、ヘルプテキストなど) は左揃えにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="61275-111">All other elements (checkboxes, help text, etc.) should be left-justified.</span></span>
<span data-ttu-id="61275-112">負のアクションを重複させないでください (' X ' と ' Cancel ' ボタンは同時に指定しないでください)。</span><span class="sxs-lookup"><span data-stu-id="61275-112">Don’t duplicate negative actions (Never provide an ‘X’ and a ‘Cancel’ button at the same time.).</span></span>
<span data-ttu-id="61275-113">' Apply ' ボタンは ' Cancel ' ボタンとペアにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="61275-113">‘Apply’ buttons should be paired with ‘Cancel’ buttons.</span></span>
[!include[Dialog buttons](~/includes/design/dialogs-image-buttons.html)]

---

## <a name="scrolling"></a><span data-ttu-id="61275-114">量</span><span class="sxs-lookup"><span data-stu-id="61275-114">Scrolling</span></span>

<span data-ttu-id="61275-115">場合によっては、コンテンツがスクロールされることがあります。</span><span class="sxs-lookup"><span data-stu-id="61275-115">In some cases, content will scroll.</span></span> <span data-ttu-id="61275-116">ダイアログのタイトルとその他の重要な情報はそのまま残ります。</span><span class="sxs-lookup"><span data-stu-id="61275-116">The dialog title and other important information remains in place.</span></span>
[!include[Dialog scrolling](~/includes/design/dialogs-image-scrolling.html)]

---

## <a name="padding"></a><span data-ttu-id="61275-117">Padding</span><span class="sxs-lookup"><span data-stu-id="61275-117">Padding</span></span>

<span data-ttu-id="61275-118">ダイアログの4つの辺の間のパディングは32px にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="61275-118">The padding around all four sides of the dialog should be 32px.</span></span>
[!include[Dialog padding](~/includes/design/dialogs-image-padding.html)]

---

## <a name="typography"></a><span data-ttu-id="61275-119">文字体裁</span><span class="sxs-lookup"><span data-stu-id="61275-119">Typography</span></span>

<span data-ttu-id="61275-120">Yu Gothic UI SemiBold in 18pt (title2) および $app-ブラック (dialog titles) を使用します。</span><span class="sxs-lookup"><span data-stu-id="61275-120">We use Segoe UI SemiBold at 18pt (title2) and $app-black for dialog titles.</span></span> <span data-ttu-id="61275-121">本文テキストの場合は、14pt (base) で Yu Gothic UI Regular を使用し、-黒を $app します。</span><span class="sxs-lookup"><span data-stu-id="61275-121">For body text, we use Segoe UI Regular at 14pt (base) and $app-black.</span></span>
[!include[Dialog typography](~/includes/design/dialogs-image-typography.html)]