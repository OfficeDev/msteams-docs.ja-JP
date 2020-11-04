---
title: 会議中のタブを設計する
author: heath-hamilton
description: Microsoft Teams の [会議中] タブを効果的に設計する方法について説明します。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 402d25e543494636af287bcc2e8a308765b4cea9
ms.sourcegitcommit: df9448681d2a81f1029aad5a5e1989cd438d1ae0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "48877030"
---
# <a name="design-an-in-meeting-tab"></a><span data-ttu-id="26ff8-103">会議中のタブを設計する</span><span class="sxs-lookup"><span data-stu-id="26ff8-103">Design an in-meeting tab</span></span>

<span data-ttu-id="26ff8-104">[会議中] タブは、会議中に共同作業を補強するためのキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="26ff8-104">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="26ff8-105">[チーム] タブの機能に基づいて、参加者は共有ビューまたはロールベースのビューを使用して、会議ステージ外の専用の領域でアプリコンテンツを表示したり操作したりできます。</span><span class="sxs-lookup"><span data-stu-id="26ff8-105">Based on the Teams tab capability, attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

## <a name="use-cases"></a><span data-ttu-id="26ff8-106">ユース ケース</span><span class="sxs-lookup"><span data-stu-id="26ff8-106">Use cases</span></span>

<span data-ttu-id="26ff8-107">[会議中] タブを使用して、次のことを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="26ff8-107">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="26ff8-108">詳細なフィードバックを提供する (たとえば、ジョブ候補を評価する)</span><span class="sxs-lookup"><span data-stu-id="26ff8-108">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="26ff8-109">会議の参加者用に投票、調査、または仕事アイテムをすばやく作成する</span><span class="sxs-lookup"><span data-stu-id="26ff8-109">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="26ff8-110">会議に関連するメモを表示する (たとえば、販売リードに関する情報)</span><span class="sxs-lookup"><span data-stu-id="26ff8-110">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

## <a name="example"></a><span data-ttu-id="26ff8-111">例</span><span class="sxs-lookup"><span data-stu-id="26ff8-111">Example</span></span>

<span data-ttu-id="26ff8-112">次の例は、アンケートのアプリコンテンツを表示する [会議中] タブを示しています。</span><span class="sxs-lookup"><span data-stu-id="26ff8-112">The following example shows the in-meeting tab displaying survey app content.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-organizer-view.png" alt-text="例では、会議の開催者からの会議タブは、会議の開催者の視点から見ることができるようになります。":::

<span data-ttu-id="26ff8-114"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">完全なシナリオを参照してください (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="26ff8-114"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See the full scenario (Figma)</a></span></span>

<span data-ttu-id="26ff8-115"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">その他の使用例 (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="26ff8-115"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See other example use cases (Figma)</a></span></span>

## <a name="anatomy"></a><span data-ttu-id="26ff8-116">構造</span><span class="sxs-lookup"><span data-stu-id="26ff8-116">Anatomy</span></span>

<span data-ttu-id="26ff8-117">[会議中] タブには、次のディメンションを使用してアプリのコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="26ff8-117">The in-meeting tab displays your app content using the following dimensions:</span></span>

* <span data-ttu-id="26ff8-118">**幅** : webview エリアの場合は280ピクセル。</span><span class="sxs-lookup"><span data-stu-id="26ff8-118">**Width** : 280 pixels for the webview area.</span></span> <span data-ttu-id="26ff8-119">Webview の左側と右側には、20ピクセルのパディングがあります。</span><span class="sxs-lookup"><span data-stu-id="26ff8-119">There are 20 pixels of padding on the left and right sides of the webview.</span></span>
* <span data-ttu-id="26ff8-120">**高さ** : タブの下端までの裁ち落とし。Webview エリアと tab ヘッダーの間には、20ピクセルのパディングがあります。</span><span class="sxs-lookup"><span data-stu-id="26ff8-120">**Height** : Full bleed to the bottom of the tab. There are 20 pixels of padding between the webview area and tab header.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-anatomy.png" alt-text="会議の拡張機能の UI を [会議] タブに示す図" border="false":::

1. <span data-ttu-id="26ff8-122">**アプリアイコン** : [会議中] タブへのエントリポイントです。</span><span class="sxs-lookup"><span data-stu-id="26ff8-122">**App icon** : The entry point to the in-meeting tab.</span></span>
1. <span data-ttu-id="26ff8-123">**ヘッダー** : タブ名を含みます。</span><span class="sxs-lookup"><span data-stu-id="26ff8-123">**Header** : Includes the tab name.</span></span>
1. <span data-ttu-id="26ff8-124">**Name** : tab インスタンスの名前。</span><span class="sxs-lookup"><span data-stu-id="26ff8-124">**Name** : The name of the tab instance.</span></span>
1. <span data-ttu-id="26ff8-125">[ **閉じる** ]: タブを閉じます。フッター内のアクションではなく、右上にある閉じるアイコンを常に使用します。</span><span class="sxs-lookup"><span data-stu-id="26ff8-125">**Dismiss** : Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>
1. <span data-ttu-id="26ff8-126">**Webview** : サードパーティアプリのすべてのコンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="26ff8-126">**Webview** : Displays all third-party app content.</span></span>

## <a name="behavior"></a><span data-ttu-id="26ff8-127">動作</span><span class="sxs-lookup"><span data-stu-id="26ff8-127">Behavior</span></span>

### <a name="scale"></a><span data-ttu-id="26ff8-128">倍率</span><span class="sxs-lookup"><span data-stu-id="26ff8-128">Scale</span></span>

<span data-ttu-id="26ff8-129">現在、[会議中] タブの幅は固定されています。</span><span class="sxs-lookup"><span data-stu-id="26ff8-129">Currently, the width of the in-meeting tab is fixed.</span></span>

### <a name="scrolling"></a><span data-ttu-id="26ff8-130">量</span><span class="sxs-lookup"><span data-stu-id="26ff8-130">Scrolling</span></span>

<span data-ttu-id="26ff8-131">[会議中] タブでスクロールすることについては、次の項目を参照してください。</span><span class="sxs-lookup"><span data-stu-id="26ff8-131">Here's what to know about scrolling in the in-meeting tab:</span></span>

* <span data-ttu-id="26ff8-132">垂直方向にスクロールできるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="26ff8-132">You should only be able to scroll vertically.</span></span>
* <span data-ttu-id="26ff8-133">スクロールした内容のみが表示されます (何も上または下にありません)。</span><span class="sxs-lookup"><span data-stu-id="26ff8-133">You can only see the content you've scrolled to (nothing above or below).</span></span>
* <span data-ttu-id="26ff8-134">Scrollbar は、webview コンテンツの一部です。</span><span class="sxs-lookup"><span data-stu-id="26ff8-134">The scrollbar is part of the webview content.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll.png" alt-text="[会議中] タブでの webview コンテンツのスクロール方法を示す図。" border="false":::

### <a name="navigation"></a><span data-ttu-id="26ff8-136">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="26ff8-136">Navigation</span></span>

<span data-ttu-id="26ff8-137">ナビゲーション層またはヘビーコンテンツがあるシナリオでは、ユーザーがセカンダリレイヤーに移動できるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="26ff8-137">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="26ff8-138">ユーザーは前のレイヤーに戻ることができる必要があります。</span><span class="sxs-lookup"><span data-stu-id="26ff8-138">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav.png" alt-text="[会議中] タブでのセカンダリレイヤーへの移動方法を示す図" border="false":::

## <a name="components"></a><span data-ttu-id="26ff8-140">コンポーネント</span><span class="sxs-lookup"><span data-stu-id="26ff8-140">Components</span></span>

<span data-ttu-id="26ff8-141">会議中のタブは、主に、 <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent デザインシステム</a>を基にした次の<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI コンポーネント (figma)</a>で構築されています。</span><span class="sxs-lookup"><span data-stu-id="26ff8-141">In-meeting tabs are built primarily with the following <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI components (Figma)</a>, which are based on the <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent Design System</a>.</span></span>

<span data-ttu-id="26ff8-142">コンポーネント</span><span class="sxs-lookup"><span data-stu-id="26ff8-142">Component</span></span> | <span data-ttu-id="26ff8-143">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="26ff8-143">Guidelines</span></span> | <span data-ttu-id="26ff8-144">例</span><span class="sxs-lookup"><span data-stu-id="26ff8-144">Example</span></span>
 - | - | -
<span data-ttu-id="26ff8-145">ボタン</span><span class="sxs-lookup"><span data-stu-id="26ff8-145">Button</span></span> | <span data-ttu-id="26ff8-146">プライマリボタンとセカンダリボタンは、中または small にすることができます。</span><span class="sxs-lookup"><span data-stu-id="26ff8-146">Primary and secondary buttons can be medium or small</span></span> | <span data-ttu-id="26ff8-147">応答を送信する</span><span class="sxs-lookup"><span data-stu-id="26ff8-147">Send a response</span></span>
<span data-ttu-id="26ff8-148">Input</span><span class="sxs-lookup"><span data-stu-id="26ff8-148">Input</span></span> | <span data-ttu-id="26ff8-149">簡単なユーザー入力のフィールド。</span><span class="sxs-lookup"><span data-stu-id="26ff8-149">Field for brief user input.</span></span> <span data-ttu-id="26ff8-150">ラベルのテキストにアイコンを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="26ff8-150">Label text can include an icon</span></span>  | <span data-ttu-id="26ff8-151">フィードバックの入力</span><span class="sxs-lookup"><span data-stu-id="26ff8-151">Enter feedback</span></span>
<span data-ttu-id="26ff8-152">Dropdown</span><span class="sxs-lookup"><span data-stu-id="26ff8-152">Dropdown</span></span> | <span data-ttu-id="26ff8-153">リストから1つ以上のオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="26ff8-153">Select one or more options from a list.</span></span> <span data-ttu-id="26ff8-154">検索機能と複数選択機能を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="26ff8-154">Can include search and multi-selection features</span></span> | <span data-ttu-id="26ff8-155">言語を選択する</span><span class="sxs-lookup"><span data-stu-id="26ff8-155">Choose a language</span></span>
<span data-ttu-id="26ff8-156">選択コントロール</span><span class="sxs-lookup"><span data-stu-id="26ff8-156">Selection controls</span></span> | <span data-ttu-id="26ff8-157">複数の選択肢またはラジオボタンのチェックボックスを使用して、1つの選択肢に対してトグルを行います。</span><span class="sxs-lookup"><span data-stu-id="26ff8-157">Use checkboxes for multiple choices or radio buttons and toggles for single choices.</span></span> <span data-ttu-id="26ff8-158">選択の詳細については、スライダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="26ff8-158">For more detailed selections, use a slider</span></span> | <span data-ttu-id="26ff8-159">投票の投票</span><span class="sxs-lookup"><span data-stu-id="26ff8-159">Vote in a poll</span></span>
<span data-ttu-id="26ff8-160">アラート</span><span class="sxs-lookup"><span data-stu-id="26ff8-160">Alerts</span></span> | <span data-ttu-id="26ff8-161">緊急メッセージ、エラー状態、または警告を表示するかどうかにかかわらず、メッセージは短くなければならず、ユーザーの現在のタスクが中断されることはありません。</span><span class="sxs-lookup"><span data-stu-id="26ff8-161">Whether displaying an urgent message, error state, or warning, the message should be short and won't interrupt the user's current task</span></span> | <span data-ttu-id="26ff8-162">応答を送信するときの表示の問題</span><span class="sxs-lookup"><span data-stu-id="26ff8-162">Display issue when submitting a response</span></span>

## <a name="theming"></a><span data-ttu-id="26ff8-163">テーマ</span><span class="sxs-lookup"><span data-stu-id="26ff8-163">Theming</span></span>

### <a name="colors"></a><span data-ttu-id="26ff8-164">色</span><span class="sxs-lookup"><span data-stu-id="26ff8-164">Colors</span></span>

<span data-ttu-id="26ff8-165">背景、foregrounds、および伝達の状態に推奨される <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">配色 (Figma)</a> を使用します。</span><span class="sxs-lookup"><span data-stu-id="26ff8-165">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended color scheme (Figma)</a> for backgrounds, foregrounds, and conveying states.</span></span>

### <a name="typography"></a><span data-ttu-id="26ff8-166">文字体裁</span><span class="sxs-lookup"><span data-stu-id="26ff8-166">Typography</span></span>

<span data-ttu-id="26ff8-167">タイトル、本文テキスト、およびメタデータテキストに推奨される <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">フォントサイズと太さ (Figma)</a> を使用します。</span><span class="sxs-lookup"><span data-stu-id="26ff8-167">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended font sizes and weights (Figma)</a> for titles, body text, and metadata text.</span></span>

## <a name="best-practices"></a><span data-ttu-id="26ff8-168">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="26ff8-168">Best practices</span></span>

### <a name="responsiveness"></a><span data-ttu-id="26ff8-169">性</span><span class="sxs-lookup"><span data-stu-id="26ff8-169">Responsiveness</span></span>

<span data-ttu-id="26ff8-170">会議中のタブレイアウトは、さまざまなサイズに拡張できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="26ff8-170">In-meeting tab layouts should be able to scale to various sizes.</span></span> <span data-ttu-id="26ff8-171">会議の後、実行中、および後に、タブの拡大/縮小と実行の方法を検討します。</span><span class="sxs-lookup"><span data-stu-id="26ff8-171">Consider how the tab will scale and take shape before, during, and after the meeting.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-before-meeting.png" alt-text="会議の前と後に、会議内のタブのコンテンツが全画面のタブのように表示されることを示す図。" border="false":::

#### <a name="before-the-meeting"></a><span data-ttu-id="26ff8-173">会議の前</span><span class="sxs-lookup"><span data-stu-id="26ff8-173">Before the meeting</span></span>

<span data-ttu-id="26ff8-174">タブレイアウトが異なる言語の右または左のレイアウトに適応し、コントロールが正しい位置に移動することを確認してください。</span><span class="sxs-lookup"><span data-stu-id="26ff8-174">Make sure your tab layout can adapt to a right or left layout for different languages and that controls move to the correct locations.</span></span> <span data-ttu-id="26ff8-175">(会議前レイアウトは、会議後のレイアウトにも適用されます)。</span><span class="sxs-lookup"><span data-stu-id="26ff8-175">(Pre-meeting layouts can also apply to post-meeting layouts.)</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-during-meeting.png" alt-text="会議中に [会議前] タブの内容が [会議中] タブにどのように縮小されるかを示す図。" border="false":::

#### <a name="during-the-meeting"></a><span data-ttu-id="26ff8-177">会議中</span><span class="sxs-lookup"><span data-stu-id="26ff8-177">During the meeting</span></span>

<span data-ttu-id="26ff8-178">タブのコンテンツは、[会議中] タブのレイアウトと場所に調整されます。</span><span class="sxs-lookup"><span data-stu-id="26ff8-178">Tab content adjusts to the in-meeting tab layout and location.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="26ff8-179">テーマ</span><span class="sxs-lookup"><span data-stu-id="26ff8-179">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-theming-do.png" alt-text="Teams 会議で使用される暗いテーマの [会議中] タブの設計方法を示す図。" border="false":::

#### <a name="do-design-for-a-dark-theme"></a><span data-ttu-id="26ff8-181">Do: 暗いテーマのデザイン</span><span class="sxs-lookup"><span data-stu-id="26ff8-181">Do: Design for a dark theme</span></span>

<span data-ttu-id="26ff8-182">Teams 会議は、ビジュアルおよび認知ノイズを軽減するために最適化されており、ユーザーがディスカッションと共有コンテンツに集中できるようにするために役立ちます。</span><span class="sxs-lookup"><span data-stu-id="26ff8-182">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-theming-dont.png" alt-text="この図は、Teams の暗いテーマに向いていない色を使用しないことを示しています。" border="false":::

#### <a name="dont-use-unfamiliar-colors"></a><span data-ttu-id="26ff8-184">いいえ: 見慣れない色を使用する</span><span class="sxs-lookup"><span data-stu-id="26ff8-184">Don't: Use unfamiliar colors</span></span>

<span data-ttu-id="26ff8-185">会議環境と競合している色は、煩雑で、Teams に対してネイティブに表示されないことがあります。</span><span class="sxs-lookup"><span data-stu-id="26ff8-185">Colors that clash with the meeting environment may be distracting and appear less native to Teams.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a><span data-ttu-id="26ff8-186">量</span><span class="sxs-lookup"><span data-stu-id="26ff8-186">Scrolling</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll-do.png" alt-text="[会議中] タブで垂直方向にスクロールできることを示す図" border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="26ff8-188">Do: 上下にスクロール</span><span class="sxs-lookup"><span data-stu-id="26ff8-188">Do: Scroll vertically</span></span>

<span data-ttu-id="26ff8-189">ユーザーは、Teams (およびその他の場所) で縦方向にスクロールすることが予想されます。</span><span class="sxs-lookup"><span data-stu-id="26ff8-189">Users anticipate vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll-dont.png" alt-text="[会議中] タブで水平スクロールを許可しないことを示す図" border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="26ff8-191">いいえ: 横方向にスクロール</span><span class="sxs-lookup"><span data-stu-id="26ff8-191">Don't: Scroll horizontally</span></span>

<span data-ttu-id="26ff8-192">水平方向のスクロールは、Teams では予期された動作ではありません。</span><span class="sxs-lookup"><span data-stu-id="26ff8-192">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="26ff8-193">会議環境でのその他のキャンバスは、垂直方向にスクロールします。</span><span class="sxs-lookup"><span data-stu-id="26ff8-193">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="26ff8-194">レイアウト</span><span class="sxs-lookup"><span data-stu-id="26ff8-194">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-layout-do.png" alt-text="[会議中] タブで推奨される単一列のレイアウトを示す図" border="false":::

#### <a name="do-single-columns"></a><span data-ttu-id="26ff8-196">Do: 単一列</span><span class="sxs-lookup"><span data-stu-id="26ff8-196">Do: Single columns</span></span>

<span data-ttu-id="26ff8-197">[会議中] タブの絞り込みの性質を考えると、コンテンツを1列で表示することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="26ff8-197">Given the in-meeting tab’s narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-layout-dont.png" alt-text="[会議中] タブの2列のレイアウトが最適でないことを示す図" border="false":::

#### <a name="dont-multiple-columns"></a><span data-ttu-id="26ff8-199">いいえ: 複数列</span><span class="sxs-lookup"><span data-stu-id="26ff8-199">Don't: Multiple columns</span></span>

<span data-ttu-id="26ff8-200">[会議中] タブの容量に制限があるため、複数の列を持つレイアウトは推奨されません。</span><span class="sxs-lookup"><span data-stu-id="26ff8-200">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="26ff8-201">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="26ff8-201">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-do.png" alt-text="会議中のタブアプリに複数のナビゲーション層がある場合は、常に [戻る] ボタンを表示する図を示します。" border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="26ff8-203">Do: [戻る] ボタンを用意する</span><span class="sxs-lookup"><span data-stu-id="26ff8-203">Do: Have a back button</span></span>

<span data-ttu-id="26ff8-204">複数のナビゲーション層がある場合は、ユーザーが前のビューに戻ることができる必要があります。</span><span class="sxs-lookup"><span data-stu-id="26ff8-204">If you have more than one layer of navigation, users must be able to go back to their previous view.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-dont.png" alt-text="ナビゲーション用に [会議中] タブにもう1つの [閉じる] ボタンを追加することによって、問題が発生する可能性があることを示す図。" border="false":::

#### <a name="dont-include-another-close-button"></a><span data-ttu-id="26ff8-206">[しない]: 別の [閉じる] ボタンを含める</span><span class="sxs-lookup"><span data-stu-id="26ff8-206">Don't: Include another close button</span></span>

<span data-ttu-id="26ff8-207">[会議中] タブのコンテンツを閉じるオプションを指定すると、ヘッダーに既に [閉じる] ボタンがあるために問題が発生し、会議中のタブ自体が閉じられることがあります。</span><span class="sxs-lookup"><span data-stu-id="26ff8-207">Providing an option to close in-meeting tab content may cause issues since there’s already a close button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-caution.png" alt-text="制限されたスペースがある場合に、[会議中] タブで modals (つまり、タスクモジュール) を使用するときに注意が必要なことを示す図" border="false":::

#### <a name="caution-using-dialogs-in-a-narrow-space"></a><span data-ttu-id="26ff8-209">注意: 狭いスペースでのダイアログの使用</span><span class="sxs-lookup"><span data-stu-id="26ff8-209">Caution: Using dialogs in a narrow space</span></span>

<span data-ttu-id="26ff8-210">すでに絞り込みが行われているタブの [タスクモジュール] などのダイアログは、コンテンツの折り返しや不明瞭になることがあります。</span><span class="sxs-lookup"><span data-stu-id="26ff8-210">Dialogs, such as task modules, in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a><span data-ttu-id="26ff8-211">アクセシビリティ</span><span class="sxs-lookup"><span data-stu-id="26ff8-211">Accessibility</span></span>

<span data-ttu-id="26ff8-212">アクセシビリティの詳細については、「 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="26ff8-212">For information on accessibility, see <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

## <a name="resources"></a><span data-ttu-id="26ff8-213">リソース</span><span class="sxs-lookup"><span data-stu-id="26ff8-213">Resources</span></span>

* <span data-ttu-id="26ff8-214"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams の会議拡張機能 Figma ファイル</a></span><span class="sxs-lookup"><span data-stu-id="26ff8-214"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams meeting extensions Figma file</a></span></span>
* [<span data-ttu-id="26ff8-215">タブデザインガイドライン</span><span class="sxs-lookup"><span data-stu-id="26ff8-215">Tabs design guidelines</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="26ff8-216">タブモバイルのデザインガイドライン</span><span class="sxs-lookup"><span data-stu-id="26ff8-216">Tabs design guidelines for mobile</span></span>](../../tabs/design/tabs-mobile.md)

## <a name="validate-your-design"></a><span data-ttu-id="26ff8-217">設計を検証する</span><span class="sxs-lookup"><span data-stu-id="26ff8-217">Validate your design</span></span>

<span data-ttu-id="26ff8-218">アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="26ff8-218">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="26ff8-219">設計検証ガイドラインの確認</span><span class="sxs-lookup"><span data-stu-id="26ff8-219">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
