---
title: 会議中のダイアログを設計する
author: heath-hamilton
description: Microsoft Teams の会議中のダイアログを効果的に設計する方法について説明します。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: f2ac0df3ce28293d9e3f61f45dd2d460dc01f2e9
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452674"
---
# <a name="design-an-in-meeting-dialog"></a><span data-ttu-id="e9dfd-103">会議中のダイアログを設計する</span><span class="sxs-lookup"><span data-stu-id="e9dfd-103">Design an in-meeting dialog</span></span>

<span data-ttu-id="e9dfd-104">会議中のダイアログは Teams の会議のステージに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-104">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="e9dfd-105">ユーザーの注意、確認、または対話が必要ですが、それは微妙で、会議に割り込むことはありません。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-105">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span>

## <a name="use-cases"></a><span data-ttu-id="e9dfd-106">ユース ケース</span><span class="sxs-lookup"><span data-stu-id="e9dfd-106">Use cases</span></span>

<span data-ttu-id="e9dfd-107">会議中のダイアログは、参加者が必要になる可能性のあるユーザー (会議の開催者など) によってトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-107">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="e9dfd-108">簡単なフィードバックを提供する</span><span class="sxs-lookup"><span data-stu-id="e9dfd-108">Provide brief feedback</span></span>
* <span data-ttu-id="e9dfd-109">簡単なアンケートまたは投票を行う</span><span class="sxs-lookup"><span data-stu-id="e9dfd-109">Take a short survey or poll</span></span>
* <span data-ttu-id="e9dfd-110">承認の提出</span><span class="sxs-lookup"><span data-stu-id="e9dfd-110">Submit approvals</span></span>
* <span data-ttu-id="e9dfd-111">アラームを取得する</span><span class="sxs-lookup"><span data-stu-id="e9dfd-111">Get reminders</span></span>

## <a name="example"></a><span data-ttu-id="e9dfd-112">例</span><span class="sxs-lookup"><span data-stu-id="e9dfd-112">Example</span></span>

<span data-ttu-id="e9dfd-113">次の例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-113">The following example shows what the in-meeting dialog might look like from a meeting participant's perspective.</span></span> <span data-ttu-id="e9dfd-114">ご覧のように、コンテンツとタスクは軽量です。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-114">As you can see, the content and task are lightweight.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-participant-view.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。":::

<span data-ttu-id="e9dfd-116"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">完全なシナリオを参照してください (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="e9dfd-116"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See the full scenario (Figma)</a></span></span>

<span data-ttu-id="e9dfd-117"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">その他の使用例 (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="e9dfd-117"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See other example use cases (Figma)</a></span></span>

## <a name="anatomy"></a><span data-ttu-id="e9dfd-118">構造</span><span class="sxs-lookup"><span data-stu-id="e9dfd-118">Anatomy</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-anatomy.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

1. <span data-ttu-id="e9dfd-120">**アプリ アイコン**</span><span class="sxs-lookup"><span data-stu-id="e9dfd-120">**App icon**</span></span>
1. <span data-ttu-id="e9dfd-121">**アプリ名**</span><span class="sxs-lookup"><span data-stu-id="e9dfd-121">**App name**</span></span>
1. <span data-ttu-id="e9dfd-122">**アクション文字列**</span><span class="sxs-lookup"><span data-stu-id="e9dfd-122">**Action string**</span></span>
1. <span data-ttu-id="e9dfd-123">**消しアイコン:** 1つのダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-123">**Dismiss icon:** Closes a single dialog.</span></span> <span data-ttu-id="e9dfd-124">フッター内のアクションではなく、右上にある閉じるアイコンを常に使用します。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-124">Always use the upper-right close icon instead of an action in the footer.</span></span>
1. <span data-ttu-id="e9dfd-125">**Webview**: サードパーティのアプリのコンテンツとボタンをすべて表示します ([Teams の標準] ボタンを推奨)。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-125">**Webview**: Displays all third-party app content and buttons (standard Teams buttons recommended).</span></span>

### <a name="sizing"></a><span data-ttu-id="e9dfd-126">決定</span><span class="sxs-lookup"><span data-stu-id="e9dfd-126">Sizing</span></span>

<span data-ttu-id="e9dfd-127">会議中のダイアログのサイズはさまざまなユースケースに応じて異なる可能性がありますが、常にパディングとコンポーネントのサイズを維持する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-127">In-meeting dialogs can vary in size to account for different use cases, but you must always maintain padding and component sizes.</span></span>

* <span data-ttu-id="e9dfd-128">**高さ**: ダイアログの高さは、webview の内容によって決まります。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-128">**Height**: The height of the dialog is determined by the content in the webview.</span></span> <span data-ttu-id="e9dfd-129">指定した最大の高さを超えているコンテンツに対して垂直方向のスクロールが行われます。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-129">Vertical scroll takes over for content that exceeds the maximum height you specify.</span></span>
* <span data-ttu-id="e9dfd-130">**幅**: webview の幅は、指定した範囲内の絶対的な値です。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-130">**Width**: The width of the webview is an absolute value within the range you specify.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-sizing.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

## <a name="behavior"></a><span data-ttu-id="e9dfd-132">動作</span><span class="sxs-lookup"><span data-stu-id="e9dfd-132">Behavior</span></span>

<span data-ttu-id="e9dfd-133"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>では、rest、読み込みなど、会議中の一般的なダイアログの動作を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-133">See general in-meeting dialog behavior, such as rest, loading, and more, in <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

### <a name="position"></a><span data-ttu-id="e9dfd-134">Position</span><span class="sxs-lookup"><span data-stu-id="e9dfd-134">Position</span></span>

<span data-ttu-id="e9dfd-135">会議中のダイアログは、会議のステージの中央に配置されます。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-135">In-meeting dialogs are aligned in the center of the meeting stage.</span></span> <span data-ttu-id="e9dfd-136">チームのシステムレベル通知のフレームワーク内でドラッグして作業することはできません。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-136">They can’t be dragged and work within the framework of Teams system-level notifications.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-position.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

### <a name="aggregation"></a><span data-ttu-id="e9dfd-138">Aggregation</span><span class="sxs-lookup"><span data-stu-id="e9dfd-138">Aggregation</span></span>

<span data-ttu-id="e9dfd-139">一度に表示されるのは1つのダイアログのみで、最下部に最後に送信された時点からのスタックランキング。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-139">Only one dialog displays at a time, stack ranking from last to most recent sent to the bottom.</span></span> <span data-ttu-id="e9dfd-140">ダイアログが解決または消去されると、次のダイアログボックスに移動します。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-140">Once a dialog is resolved or dismissed, the next one take its place.</span></span>

<span data-ttu-id="e9dfd-141"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">例 (Figma) を参照してください。</a></span><span class="sxs-lookup"><span data-stu-id="e9dfd-141"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See an example (Figma)</a></span></span>

### <a name="scrolling"></a><span data-ttu-id="e9dfd-142">量</span><span class="sxs-lookup"><span data-stu-id="e9dfd-142">Scrolling</span></span>

<span data-ttu-id="e9dfd-143">スクロールは、会議中のダイアログの webview 部分で行われます。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-143">Scrolling occurs in the webview portion of an in-meeting dialog.</span></span> <span data-ttu-id="e9dfd-144">スクロールについて次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-144">Remember the following about scrolling:</span></span>

* <span data-ttu-id="e9dfd-145">垂直方向にスクロールできるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-145">You should only be able to scroll vertically.</span></span>
* <span data-ttu-id="e9dfd-146">スクロールした内容のみが表示されます (何も上または下にありません)。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-146">You can only see the content you've scrolled to (nothing above or below).</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-scroll.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

### <a name="buttons"></a><span data-ttu-id="e9dfd-148">ボタン</span><span class="sxs-lookup"><span data-stu-id="e9dfd-148">Buttons</span></span>

<span data-ttu-id="e9dfd-149">[会議中] ダイアログボタンは、webview の一部です ([いくつかの例を参照してください](#best-practices))。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-149">In-meeting dialog buttons are part of the webview ([see some examples](#best-practices)).</span></span>

<span data-ttu-id="e9dfd-150">類似のコンポーネントとは異なり、ユーザーがボタンを選択すると、会議中のダイアログは閉じられます。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-150">Unlike similar components, in-meeting dialogs are dismissed once a user selects a button.</span></span>

## <a name="components"></a><span data-ttu-id="e9dfd-151">コンポーネント</span><span class="sxs-lookup"><span data-stu-id="e9dfd-151">Components</span></span>

<span data-ttu-id="e9dfd-152">会議中のダイアログは、主に、 <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent デザインシステム</a>を基にした次の<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI コンポーネント (figma)</a>で構築されています。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-152">In-meeting dialogs are built primarily with the following <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI components (Figma)</a>, which are based on the <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent Design System</a>.</span></span>

<span data-ttu-id="e9dfd-153">コンポーネント</span><span class="sxs-lookup"><span data-stu-id="e9dfd-153">Component</span></span> | <span data-ttu-id="e9dfd-154">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="e9dfd-154">Guidelines</span></span> | <span data-ttu-id="e9dfd-155">例</span><span class="sxs-lookup"><span data-stu-id="e9dfd-155">Example</span></span>
 - | - | -
<span data-ttu-id="e9dfd-156">ボタン</span><span class="sxs-lookup"><span data-stu-id="e9dfd-156">Button</span></span> | <span data-ttu-id="e9dfd-157">プライマリボタンとセカンダリボタンは、中または small にすることができます。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-157">Primary and secondary buttons can be medium or small</span></span> | <span data-ttu-id="e9dfd-158">応答を送信する</span><span class="sxs-lookup"><span data-stu-id="e9dfd-158">Send a response</span></span>
<span data-ttu-id="e9dfd-159">Input</span><span class="sxs-lookup"><span data-stu-id="e9dfd-159">Input</span></span> | <span data-ttu-id="e9dfd-160">簡単なユーザー入力のフィールド。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-160">Field for brief user input.</span></span> <span data-ttu-id="e9dfd-161">ラベルのテキストにアイコンを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-161">Label text can include an icon</span></span>  | <span data-ttu-id="e9dfd-162">フィードバックの入力</span><span class="sxs-lookup"><span data-stu-id="e9dfd-162">Enter feedback</span></span>
<span data-ttu-id="e9dfd-163">Dropdown</span><span class="sxs-lookup"><span data-stu-id="e9dfd-163">Dropdown</span></span> | <span data-ttu-id="e9dfd-164">リストから1つ以上のオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-164">Select one or more options from a list.</span></span> <span data-ttu-id="e9dfd-165">検索機能と複数選択機能を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-165">Can include search and multi-selection features</span></span> | <span data-ttu-id="e9dfd-166">言語を選択する</span><span class="sxs-lookup"><span data-stu-id="e9dfd-166">Choose a language</span></span>
<span data-ttu-id="e9dfd-167">選択コントロール</span><span class="sxs-lookup"><span data-stu-id="e9dfd-167">Selection controls</span></span> | <span data-ttu-id="e9dfd-168">複数の選択肢またはラジオボタンのチェックボックスを使用して、1つの選択肢に対してトグルを行います。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-168">Use checkboxes for multiple choices or radio buttons and toggles for single choices.</span></span> <span data-ttu-id="e9dfd-169">選択の詳細については、スライダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-169">For more detailed selections, use a slider</span></span> | <span data-ttu-id="e9dfd-170">投票の投票</span><span class="sxs-lookup"><span data-stu-id="e9dfd-170">Vote in a poll</span></span>
<span data-ttu-id="e9dfd-171">アラート</span><span class="sxs-lookup"><span data-stu-id="e9dfd-171">Alerts</span></span> | <span data-ttu-id="e9dfd-172">緊急メッセージ、エラー状態、または警告を表示するかどうかにかかわらず、メッセージは短くなければならず、ユーザーの現在のタスクが中断されることはありません。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-172">Whether displaying an urgent message, error state, or warning, the message should be short and won't interrupt the user's current task</span></span> | <span data-ttu-id="e9dfd-173">応答を送信するときの表示の問題</span><span class="sxs-lookup"><span data-stu-id="e9dfd-173">Display issue when submitting a response</span></span>

## <a name="theming"></a><span data-ttu-id="e9dfd-174">テーマ</span><span class="sxs-lookup"><span data-stu-id="e9dfd-174">Theming</span></span>

### <a name="colors"></a><span data-ttu-id="e9dfd-175">色</span><span class="sxs-lookup"><span data-stu-id="e9dfd-175">Colors</span></span>

<span data-ttu-id="e9dfd-176">背景、foregrounds、および伝達の状態に推奨される <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">配色 (Figma)</a> を使用します。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-176">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended color scheme (Figma)</a> for backgrounds, foregrounds, and conveying states.</span></span>

### <a name="typography"></a><span data-ttu-id="e9dfd-177">文字体裁</span><span class="sxs-lookup"><span data-stu-id="e9dfd-177">Typography</span></span>

<span data-ttu-id="e9dfd-178">タイトル、本文テキスト、およびメタデータテキストに推奨される <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">フォントサイズと太さ (Figma)</a> を使用します。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-178">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended font sizes and weights (Figma)</a> for titles, body text, and metadata text.</span></span>

## <a name="best-practices"></a><span data-ttu-id="e9dfd-179">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="e9dfd-179">Best practices</span></span>

<span data-ttu-id="e9dfd-180">会議中のダイアログを使用すると通話がより効果的になることがありますが、obtrusive 過ぎると、着信呼び出しをすることもできます。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-180">While in-meeting dialogs can make calls more effective, they also can derail calls if too obtrusive.</span></span> <span data-ttu-id="e9dfd-181">一般的に、ダイアログは控えめに使用し、次のベストプラクティスに従ってください。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-181">In general, use the dialogs sparingly and follow these best practices.</span></span>

### <a name="navigation"></a><span data-ttu-id="e9dfd-182">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="e9dfd-182">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-do.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

#### <a name="do-keep-it-contained"></a><span data-ttu-id="e9dfd-184">Do: 格納されたまま保持する</span><span class="sxs-lookup"><span data-stu-id="e9dfd-184">Do: Keep it contained</span></span>

<span data-ttu-id="e9dfd-185">ユーザーが会議に集中できるように、会議ダイアログのコンテンツを1つの画面に制限します。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-185">Limit in-meeting dialog content to a single screen so users can focus on the meeting.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-dont.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

#### <a name="dont-include-multiple-steps"></a><span data-ttu-id="e9dfd-187">いいえ: 複数の手順を含めます</span><span class="sxs-lookup"><span data-stu-id="e9dfd-187">Don't: Include multiple steps</span></span>

<span data-ttu-id="e9dfd-188">会議中のダイアログでは、ユーザーがコンテンツを移動する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-188">In-meeting dialogs shouldn't require users to navigate through content.</span></span>

   :::column-end:::
:::row-end:::

### <a name="interactions"></a><span data-ttu-id="e9dfd-189">関係</span><span class="sxs-lookup"><span data-stu-id="e9dfd-189">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-interactions-do.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-interactions-dont.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-do.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

#### <a name="do-limit-number-of-interactions"></a><span data-ttu-id="e9dfd-193">Do: 操作の数を制限する</span><span class="sxs-lookup"><span data-stu-id="e9dfd-193">Do: Limit number of interactions</span></span>

<span data-ttu-id="e9dfd-194">不要なコンテンツを削除して、ユーザーがすばやく作業できないようにします。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-194">Remove unnecessary content that doesn't help users accomplish something quickly.</span></span> <span data-ttu-id="e9dfd-195">複雑な対話が必要な場合は、代わりに [会議中] タブで単一の列を使用してコンテンツを表示することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-195">If you need complex interactions, we strongly recommend displaying your content using a single column on the in-meeting tab instead.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-dont.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="e9dfd-197">いいえ: 不要な要素を紹介します。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-197">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="e9dfd-198">複数の対話を含む1つの会議中のダイアログを設計することもできますが、会議の参加者が多くなることがあります。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-198">You may be able to design a single in-meeting dialog with multiple interactions, but too many can distract from the meeting.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="e9dfd-199">レイアウト</span><span class="sxs-lookup"><span data-stu-id="e9dfd-199">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-do.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

#### <a name="do-use-single-column-layouts"></a><span data-ttu-id="e9dfd-201">手順: 単一列のレイアウトを使用する</span><span class="sxs-lookup"><span data-stu-id="e9dfd-201">Do: Use single-column layouts</span></span>

<span data-ttu-id="e9dfd-202">ダイアログは会議ステージの中央にあります。タスクの完了は、ユーザーの不満を回避するために、迅速かつシンプルにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-202">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-dont.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="e9dfd-204">[しない: スペースを整頓する」</span><span class="sxs-lookup"><span data-stu-id="e9dfd-204">Don't: Clutter the space</span></span>

<span data-ttu-id="e9dfd-205">高密度または過度に構造化されたコンテンツは、特に会議中に煩雑で圧倒的なものになる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-205">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

### <a name="size"></a><span data-ttu-id="e9dfd-206">Size</span><span class="sxs-lookup"><span data-stu-id="e9dfd-206">Size</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-do.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

#### <a name="do-keep-it-consistent"></a><span data-ttu-id="e9dfd-208">実行: 一貫性を保つ</span><span class="sxs-lookup"><span data-stu-id="e9dfd-208">Do: Keep it consistent</span></span>

<span data-ttu-id="e9dfd-209">会議ダイアログボックスは常に同じ場所に表示されるため、これは重要です。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-209">This is important because in-meeting dialogs always display in the same location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-dont.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

#### <a name="dont-always-fit-to-the-content"></a><span data-ttu-id="e9dfd-211">いいえ: 常にコンテンツに合わせる</span><span class="sxs-lookup"><span data-stu-id="e9dfd-211">Don't: Always fit to the content</span></span>

<span data-ttu-id="e9dfd-212">水平方向のスクロールを避けようとしていますが、同じアプリ内の複数の会議中のダイアログのサイズが一貫していない場合があります。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-212">You may be trying to avoid horizontal scrolling, but multiple in-meeting dialog sizes within the same app is an inconsistent experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="e9dfd-213">コントロール</span><span class="sxs-lookup"><span data-stu-id="e9dfd-213">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-do.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="e9dfd-215">Do: 右揃えで主な操作を行います。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-215">Do: Right align the primary action</span></span>

<span data-ttu-id="e9dfd-216">最も視覚的に大きなアクションは、右端の位置に配置することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-216">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-dont.png" alt-text="例は、会議の参加者の視点から、会議中のダイアログがどのようなものかを示しています。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="e9dfd-218">いいえ: 左揃えまたは中央揃えのアクション</span><span class="sxs-lookup"><span data-stu-id="e9dfd-218">Don't: Left or center align actions</span></span>

<span data-ttu-id="e9dfd-219">これは、ダイアログでのコントロールの配置に関する標準 Teams パターンとは異なり、一番上にあるダイアログと競合する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-219">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a><span data-ttu-id="e9dfd-220">アクセシビリティ</span><span class="sxs-lookup"><span data-stu-id="e9dfd-220">Accessibility</span></span>

<span data-ttu-id="e9dfd-221">アクセシビリティの詳細については、「 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-221">For information on accessibility, see <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

## <a name="resources"></a><span data-ttu-id="e9dfd-222">リソース</span><span class="sxs-lookup"><span data-stu-id="e9dfd-222">Resources</span></span>

* <span data-ttu-id="e9dfd-223"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams の会議拡張機能 Figma ファイル</a></span><span class="sxs-lookup"><span data-stu-id="e9dfd-223"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams meeting extensions Figma file</a></span></span>

## <a name="validate-your-design"></a><span data-ttu-id="e9dfd-224">設計を検証する</span><span class="sxs-lookup"><span data-stu-id="e9dfd-224">Validate your design</span></span>

<span data-ttu-id="e9dfd-225">アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9dfd-225">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e9dfd-226">設計検証ガイドラインの確認</span><span class="sxs-lookup"><span data-stu-id="e9dfd-226">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
