---
title: モバイルのタブ
description: モバイルで動作するタブを設計する際のガイドラインについて説明します。
ms.topic: conceptual
localization_priority: Normal
keywords: teams デザイン ガイドライン リファレンス フレームワーク 個人用アプリ モバイル タブ
ms.openlocfilehash: cdcaddf5ba0fb18537e87daa4b459c7377225f76
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075697"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="a4bf1-104">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="a4bf1-104">Tabs on mobile</span></span>

<span data-ttu-id="a4bf1-105">Teams モバイル チャネル、チャット、個人用アプリにタブを含めできます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-105">You can include tabs in Teams mobile channels, chats, and personal apps.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="a4bf1-106">個人用タブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="a4bf1-106">Accessing personal tabs</span></span>

<span data-ttu-id="a4bf1-107">アプリドロワーの個人用タブにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-107">You can access personal tabs in the app drawer.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Teams モバイル アプリの引き出しを示す図。" border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="a4bf1-109">チャネル タブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="a4bf1-109">Accessing channel tabs</span></span>

<span data-ttu-id="a4bf1-110">チャネルタブとグループ タブにアクセスするには、追加されたチャネルまたはチャットで [その他] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-110">You can access channel and group tabs by selecting the **More** button in the channel or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Teams モバイル タブを示す図。" border="false":::

## <a name="design-considerations"></a><span data-ttu-id="a4bf1-112">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="a4bf1-112">Design considerations</span></span>

<span data-ttu-id="a4bf1-113">モバイル プラットフォームを使用すると、アプリのコンテンツが主要な Teams ナビゲーションとは別に、すべての画面を取り上げ、アプリを臨場感のあるエクスペリエンスにできます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-113">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="a4bf1-114">Teams に合った臨場感のあるエクスペリエンスを作成するには、次のガイドラインに従います。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-114">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="a4bf1-115">レスポンシブ デザイン</span><span class="sxs-lookup"><span data-stu-id="a4bf1-115">Responsive design</span></span>

<span data-ttu-id="a4bf1-116">タブはさまざまな画面サイズのデバイスで開くことができるため、応答性の高い設計原則に従 [う必要](https://www.w3schools.com/html/html_responsive.asp) があります。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-116">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="a4bf1-117">すべての主要な構成は、モバイル デバイスでアクセス可能で、ビューを歪めずに行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-117">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="a4bf1-118">タブがモバイル デバイスに読み込まれると、指ベースのナビゲーションを使用してすべてのボタンとリンクに簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-118">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="a4bf1-119">レイアウト</span><span class="sxs-lookup"><span data-stu-id="a4bf1-119">Layouts</span></span>

<span data-ttu-id="a4bf1-120">タブの適切なレイアウトを選択することが重要です。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-120">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="a4bf1-121">提示する情報の種類を検討し、簡単に使用するためにそれを整理するレイアウトを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-121">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="a4bf1-122">いくつかの潜在的なオプションの概要を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-122">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="a4bf1-123">単一のキャンバス</span><span class="sxs-lookup"><span data-stu-id="a4bf1-123">Single canvas</span></span>

<span data-ttu-id="a4bf1-124">これは、作業が行われる 1 つの大きな領域です。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-124">This is one large area where work gets done.</span></span> <span data-ttu-id="a4bf1-125">Teams Wiki アプリは、このパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-125">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="a4bf1-126">コンテンツを小さなコンポーネントに分けないアプリがある場合は、これは適しています。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-126">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Teams モバイル単一キャンバス タブを示す図。" border="false":::

#### <a name="list"></a><span data-ttu-id="a4bf1-128">一覧表示</span><span class="sxs-lookup"><span data-stu-id="a4bf1-128">List</span></span>

<span data-ttu-id="a4bf1-129">リストは、大量のデータを並べ替え、フィルター処理する場合に最適で、最も重要な情報を一番上に保つことに最適です。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-129">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="a4bf1-130">並べ替え可能な列を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-130">It is helpful to use sortable columns.</span></span> <span data-ttu-id="a4bf1-131">省略記号メニューの下の各リスト アイテムにアクションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-131">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Teams モバイル リスト タブを示す図。" border="false":::

#### <a name="grid"></a><span data-ttu-id="a4bf1-133">グリッド</span><span class="sxs-lookup"><span data-stu-id="a4bf1-133">Grid</span></span>

<span data-ttu-id="a4bf1-134">グリッドは、視覚的な要素を表示する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-134">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="a4bf1-135">上部にフィルターまたは検索コントロールを含めるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-135">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="グリッド レイアウトの Teams モバイル タブを示す図。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="a4bf1-137">モバイル上のボットを含むタブ</span><span class="sxs-lookup"><span data-stu-id="a4bf1-137">Tabs with bots on mobile</span></span>

<span data-ttu-id="a4bf1-138">次の例は、タブとボットを持つ個人用アプリです。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-138">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="タブとボットを持つモバイル Teams アプリの方法を示す図。" border="false":::

## <a name="ui-components"></a><span data-ttu-id="a4bf1-140">UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="a4bf1-140">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="a4bf1-141">カラー パレット</span><span class="sxs-lookup"><span data-stu-id="a4bf1-141">Color palettes</span></span>

<span data-ttu-id="a4bf1-142">承認済みのニュートラル パレットを背景、通知、テキスト、ボタンに使用すると、アプリが Teams で自宅で使い分けるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-142">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="a4bf1-143">Teams モバイルには 2 つの色のテーマ (明るいテーマと暗いテーマ) が用意されていますので、両方でアプリが優れたものに見えるのを確認すると良い考えです。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-143">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="a4bf1-144">明るい色</span><span class="sxs-lookup"><span data-stu-id="a4bf1-144">Light color</span></span>

![明るいカラー パレット](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="a4bf1-146">濃い色</span><span class="sxs-lookup"><span data-stu-id="a4bf1-146">Dark color</span></span>

![濃色パレット](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="a4bf1-148">ボタンとコントロール</span><span class="sxs-lookup"><span data-stu-id="a4bf1-148">Buttons and controls</span></span>

<span data-ttu-id="a4bf1-149">ボタンのスタイルを設定する方法は、トリガーするアクションの種類を伝えるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-149">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="a4bf1-150">さまざまなレベルの強調を表示するために書式設定されたボタンの広い範囲を維持します。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-150">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="a4bf1-151">ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを指定できます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-151">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="a4bf1-152">階層内の異なるレベルを伝える目的で、各カテゴリ内のプライマリ ボタンとセカンダリ ボタンを設計しました。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-152">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="a4bf1-153">ボタン</span><span class="sxs-lookup"><span data-stu-id="a4bf1-153">Buttons</span></span>

<span data-ttu-id="a4bf1-154">プライマリ ボタンとセカンダリ ボタン。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-154">Primary and secondary buttons.</span></span>

![ボタンの画像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="a4bf1-156">選択コントロール</span><span class="sxs-lookup"><span data-stu-id="a4bf1-156">Selection controls</span></span>

<span data-ttu-id="a4bf1-157">ラジオ ボタン、チェック ボックス、およびトグル。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-157">Radio buttons, checkboxes, and toggles.</span></span>

![選択コントロール](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="a4bf1-159">シックレットと丸薬</span><span class="sxs-lookup"><span data-stu-id="a4bf1-159">Chiclets and pills</span></span>

![シックレットと丸薬](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="a4bf1-161">文字体裁</span><span class="sxs-lookup"><span data-stu-id="a4bf1-161">Typography</span></span>

<span data-ttu-id="a4bf1-162">タイポグラフィは明確で目的に合ったものにしてください。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-162">Typography should be clear and purposeful.</span></span> <span data-ttu-id="a4bf1-163">重要な情報を強調し、複数のフォントとサイズを使用して混乱を軽減しないようにします。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-163">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="a4bf1-164">文の大文字と小文字を使用し、ローカライズと読み取り可能性のためにすべての大文字を使用しないようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-164">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![モバイルタイポグラフ](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="a4bf1-166">フィールドとフライアウト</span><span class="sxs-lookup"><span data-stu-id="a4bf1-166">Fields and flyouts</span></span>

<span data-ttu-id="a4bf1-167">フィールドは、ユーザーがテキストを入力できる領域です。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-167">Fields are areas where users can input text.</span></span> <span data-ttu-id="a4bf1-168">フライアウトはダイアログよりも軽量で、上部ウィンドウから表示されます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-168">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="a4bf1-169">コントロールを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="a4bf1-169">List controls</span></span>

![モバイル リスト コントロール](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="a4bf1-171">フィールド コントロール</span><span class="sxs-lookup"><span data-stu-id="a4bf1-171">Field controls</span></span>

![モバイル フィールド コントロール](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="a4bf1-173">開発者の考慮事項</span><span class="sxs-lookup"><span data-stu-id="a4bf1-173">Developer considerations</span></span>

<span data-ttu-id="a4bf1-174">タブを含むアプリを構築する場合は、Android クライアントと iOS Microsoft Teams クライアントの両方でタブがどのように機能するのか検討 (およびテスト) する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-174">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="a4bf1-175">以下のセクションでは、考慮する必要がある主要なシナリオの一部について説明します。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-175">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="authentication"></a><span data-ttu-id="a4bf1-176">認証</span><span class="sxs-lookup"><span data-stu-id="a4bf1-176">Authentication</span></span>

<span data-ttu-id="a4bf1-177">モバイル クライアントで認証を機能するには、Teams JavaScript SDK を少なくともバージョン 1.4.1 にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-177">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="a4bf1-178">低帯域幅と断続的な接続</span><span class="sxs-lookup"><span data-stu-id="a4bf1-178">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="a4bf1-179">モバイル クライアントは、低帯域幅と断続的な接続で定期的に機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-179">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="a4bf1-180">アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-180">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="a4bf1-181">また、長時間実行されるプロセスに対してユーザーにフィードバックを提供するユーザー進行状況インジケーターも必要です。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-181">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="a4bf1-182">タブは、承認チームの入力に基づいて、アプリケーションが許可リストに追加された後にのみ、モバイルで有効になります。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-182">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="a4bf1-183">モバイルの応答性を確認するには、ユーザーに teamsubm@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-183">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="a4bf1-184">モバイル クライアントでのテスト</span><span class="sxs-lookup"><span data-stu-id="a4bf1-184">Testing on mobile clients</span></span>

<span data-ttu-id="a4bf1-185">さまざまなサイズと品質のモバイル デバイスでタブが適切に機能するを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="a4bf1-186">Android デバイスの場合 [、DevTools](~/tabs/how-to/developer-tools.md) を使用して、実行中にタブをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="a4bf1-187">パフォーマンスの高いデバイスと低パフォーマンスデバイスの両方とタブレットでテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-187">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="distribution"></a><span data-ttu-id="a4bf1-188">配布</span><span class="sxs-lookup"><span data-stu-id="a4bf1-188">Distribution</span></span>

<span data-ttu-id="a4bf1-189">Teams モバイル クライアントで適切に機能するには、Teams ストアに記載されているアプリがモバイルでの使用を承認されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-189">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="a4bf1-190">タブの動作は、アプリが承認されるかどうかによって異なります。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-190">How tabs behave depends on whether your app is approved.</span></span>

#### <a name="channel-and-group-tab-behavior"></a><span data-ttu-id="a4bf1-191">チャネルとグループタブの動作</span><span class="sxs-lookup"><span data-stu-id="a4bf1-191">Channel and group tab behavior</span></span>

* <span data-ttu-id="a4bf1-192">**承認時の動作**: アプリの構成を使用して Teams モバイル クライアントで開 `contentUrl` きます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-192">**Behavior when approved**: Opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>
* <span data-ttu-id="a4bf1-193">**承認されていない場合の動作**: アプリの構成を使用してデバイスの既定のブラウザーで開きます (ソース コードの関数にも含める `websiteUrl` 必要 `setSettings()` があります)。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-193">**Behavior when not approved**: Opens in the device’s default browser using your app's `websiteUrl` configuration (which also must be included in your source code's `setSettings()` function).</span></span> <span data-ttu-id="a4bf1-194">ただし、ユーザーは、アプリの横にある [詳細] を選択し、[開く] を選択してアプリの構成をトリガーすることで、Teams モバイル クライアントでタブを読み込 `contentUrl` み続けることができます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-194">However, users can still load the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>

#### <a name="personal-app-behavior"></a><span data-ttu-id="a4bf1-195">個人用アプリの動作</span><span class="sxs-lookup"><span data-stu-id="a4bf1-195">Personal app behavior</span></span>

* <span data-ttu-id="a4bf1-196">**承認時の動作**: 個人用アプリの各タブは、それぞれの構成を使用して Teams モバイル クライアントに表示 `contentUrl` されます。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-196">**Behavior when approved**: Each tab in the personal app displays in the Teams mobile client using their respective `contentUrl` configuration.</span></span>
* <span data-ttu-id="a4bf1-197">**承認されていない場合の動作**: 個人用アプリは Teams モバイル クライアントで使用できません。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-197">**Behavior when not approved**: The personal app is unavailable in the Teams mobile client.</span></span>

#### <a name="non-teams-store-app-behavior"></a><span data-ttu-id="a4bf1-198">Teams 以外のストア アプリの動作</span><span class="sxs-lookup"><span data-stu-id="a4bf1-198">Non-Teams store app behavior</span></span>

<span data-ttu-id="a4bf1-199">アプリをサイドロードする場合や、組織のアプリ カタログに発行する場合、タブの動作は、モバイル向け Microsoft によって承認された Teams ストア アプリと同じです。</span><span class="sxs-lookup"><span data-stu-id="a4bf1-199">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>
