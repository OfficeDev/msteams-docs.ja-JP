---
title: モバイルのタブ
description: モバイルで動作するタブを設計する際のガイドラインについて説明します。
ms.topic: conceptual
localization_priority: Normal
keywords: teams デザイン ガイドライン リファレンス フレームワーク 個人用アプリ モバイル タブ
ms.openlocfilehash: b9f09ce2603ee2617b8b93ba2132b900c61f2c31
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088760"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="a4887-104">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="a4887-104">Tabs on mobile</span></span>

<span data-ttu-id="a4887-105">モバイル チャネル、チャット、個人用Teamsにタブを含めできます。</span><span class="sxs-lookup"><span data-stu-id="a4887-105">You can include tabs in Teams mobile channels, chats, and personal apps.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="a4887-106">個人用タブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="a4887-106">Accessing personal tabs</span></span>

<span data-ttu-id="a4887-107">アプリドロワーの個人用タブにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="a4887-107">You can access personal tabs in the app drawer.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="モバイル アプリの引き出Teamsを示す図。" border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="a4887-109">チャネル タブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="a4887-109">Accessing channel tabs</span></span>

<span data-ttu-id="a4887-110">チャネルタブとグループ タブにアクセスするには、追加されたチャネルまたはチャットで [その他] ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="a4887-110">You can access channel and group tabs by selecting the **More** button in the channel or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="モバイル タブのTeams図。" border="false":::

## <a name="design-considerations"></a><span data-ttu-id="a4887-112">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="a4887-112">Design considerations</span></span>

<span data-ttu-id="a4887-113">モバイル プラットフォームを使用すると、アプリのコンテンツがメインのナビゲーションとは別に、すべての画面を取り上げ、アプリの臨場感Teamsできます。</span><span class="sxs-lookup"><span data-stu-id="a4887-113">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="a4887-114">ユーザーに合った臨場感のあるエクスペリエンスをTeamsガイドラインに従います。</span><span class="sxs-lookup"><span data-stu-id="a4887-114">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="a4887-115">レスポンシブ デザイン</span><span class="sxs-lookup"><span data-stu-id="a4887-115">Responsive design</span></span>

<span data-ttu-id="a4887-116">タブはさまざまな画面サイズのデバイスで開くことができるため、応答性の高い設計原則に従 [う必要](https://www.w3schools.com/html/html_responsive.asp) があります。</span><span class="sxs-lookup"><span data-stu-id="a4887-116">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="a4887-117">すべての主要な構成は、モバイル デバイスでアクセス可能で、ビューを歪めずに行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4887-117">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="a4887-118">タブがモバイル デバイスに読み込まれると、指ベースのナビゲーションを使用してすべてのボタンとリンクに簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="a4887-118">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="a4887-119">レイアウト</span><span class="sxs-lookup"><span data-stu-id="a4887-119">Layouts</span></span>

<span data-ttu-id="a4887-120">タブの適切なレイアウトを選択することが重要です。</span><span class="sxs-lookup"><span data-stu-id="a4887-120">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="a4887-121">提示する情報の種類を検討し、簡単に使用するためにそれを整理するレイアウトを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4887-121">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="a4887-122">いくつかの潜在的なオプションの概要を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="a4887-122">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="a4887-123">単一のキャンバス</span><span class="sxs-lookup"><span data-stu-id="a4887-123">Single canvas</span></span>

<span data-ttu-id="a4887-124">これは、作業が行われる 1 つの大きな領域です。</span><span class="sxs-lookup"><span data-stu-id="a4887-124">This is one large area where work gets done.</span></span> <span data-ttu-id="a4887-125">Wiki Teamsは、このパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="a4887-125">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="a4887-126">コンテンツを小さなコンポーネントに分けないアプリがある場合は、これは適しています。</span><span class="sxs-lookup"><span data-stu-id="a4887-126">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="モバイル単一のTeamsタブを示す図。" border="false":::

#### <a name="list"></a><span data-ttu-id="a4887-128">一覧表示</span><span class="sxs-lookup"><span data-stu-id="a4887-128">List</span></span>

<span data-ttu-id="a4887-129">リストは、大量のデータを並べ替え、フィルター処理する場合に最適で、最も重要な情報を一番上に保つことに最適です。</span><span class="sxs-lookup"><span data-stu-id="a4887-129">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="a4887-130">並べ替え可能な列を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="a4887-130">It is helpful to use sortable columns.</span></span> <span data-ttu-id="a4887-131">省略記号メニューの下の各リスト アイテムにアクションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="a4887-131">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="[モバイル リスト] タブTeamsを示す図。" border="false":::

#### <a name="grid"></a><span data-ttu-id="a4887-133">グリッド</span><span class="sxs-lookup"><span data-stu-id="a4887-133">Grid</span></span>

<span data-ttu-id="a4887-134">グリッドは、視覚的な要素を表示する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="a4887-134">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="a4887-135">上部にフィルターまたは検索コントロールを含めるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a4887-135">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="グリッド レイアウトがTeamsモバイル タブを示す図。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="a4887-137">モバイル上のボットを含むタブ</span><span class="sxs-lookup"><span data-stu-id="a4887-137">Tabs with bots on mobile</span></span>

<span data-ttu-id="a4887-138">次の例は、タブとボットを持つ個人用アプリです。</span><span class="sxs-lookup"><span data-stu-id="a4887-138">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="タブとボットを持つTeamsモバイル アプリの表示方法を示す図。" border="false":::

## <a name="ui-components"></a><span data-ttu-id="a4887-140">UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="a4887-140">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="a4887-141">カラー パレット</span><span class="sxs-lookup"><span data-stu-id="a4887-141">Color palettes</span></span>

<span data-ttu-id="a4887-142">承認済みのニュートラル パレットを背景、通知、テキスト、およびボタンに使用すると、アプリがユーザーの自宅で使いTeams。</span><span class="sxs-lookup"><span data-stu-id="a4887-142">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="a4887-143">モバイルTeams色のテーマが 2 つ (明るいと暗い) ので、両方でアプリが優れた外観を示すのは良い考えです。</span><span class="sxs-lookup"><span data-stu-id="a4887-143">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="a4887-144">明るい色</span><span class="sxs-lookup"><span data-stu-id="a4887-144">Light color</span></span>

![明るいカラー パレット](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="a4887-146">濃い色</span><span class="sxs-lookup"><span data-stu-id="a4887-146">Dark color</span></span>

![濃色パレット](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="a4887-148">ボタンとコントロール</span><span class="sxs-lookup"><span data-stu-id="a4887-148">Buttons and controls</span></span>

<span data-ttu-id="a4887-149">ボタンのスタイルを設定する方法は、トリガーするアクションの種類を伝えるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="a4887-149">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="a4887-150">さまざまなレベルの強調を表示するために書式設定されたボタンの広い範囲を維持します。</span><span class="sxs-lookup"><span data-stu-id="a4887-150">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="a4887-151">ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを指定できます。</span><span class="sxs-lookup"><span data-stu-id="a4887-151">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="a4887-152">階層内の異なるレベルを伝える目的で、各カテゴリ内のプライマリ ボタンとセカンダリ ボタンを設計しました。</span><span class="sxs-lookup"><span data-stu-id="a4887-152">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="a4887-153">ボタン</span><span class="sxs-lookup"><span data-stu-id="a4887-153">Buttons</span></span>

<span data-ttu-id="a4887-154">プライマリ ボタンとセカンダリ ボタン。</span><span class="sxs-lookup"><span data-stu-id="a4887-154">Primary and secondary buttons.</span></span>

![ボタンの画像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="a4887-156">選択コントロール</span><span class="sxs-lookup"><span data-stu-id="a4887-156">Selection controls</span></span>

<span data-ttu-id="a4887-157">ラジオ ボタン、チェック ボックス、およびトグル。</span><span class="sxs-lookup"><span data-stu-id="a4887-157">Radio buttons, checkboxes, and toggles.</span></span>

![選択コントロール](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="a4887-159">シックレットと丸薬</span><span class="sxs-lookup"><span data-stu-id="a4887-159">Chiclets and pills</span></span>

![シックレットと丸薬](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="a4887-161">文字体裁</span><span class="sxs-lookup"><span data-stu-id="a4887-161">Typography</span></span>

<span data-ttu-id="a4887-162">タイポグラフィは明確で目的に合ったものにしてください。</span><span class="sxs-lookup"><span data-stu-id="a4887-162">Typography should be clear and purposeful.</span></span> <span data-ttu-id="a4887-163">重要な情報を強調し、複数のフォントとサイズを使用して混乱を軽減しないようにします。</span><span class="sxs-lookup"><span data-stu-id="a4887-163">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="a4887-164">文の大文字と小文字を使用し、ローカライズと読み取り可能性のためにすべての大文字を使用しないようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a4887-164">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![モバイルタイポグラフ](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="a4887-166">フィールドとフライアウト</span><span class="sxs-lookup"><span data-stu-id="a4887-166">Fields and flyouts</span></span>

<span data-ttu-id="a4887-167">フィールドは、ユーザーがテキストを入力できる領域です。</span><span class="sxs-lookup"><span data-stu-id="a4887-167">Fields are areas where users can input text.</span></span> <span data-ttu-id="a4887-168">フライアウトはダイアログよりも軽量で、上部ウィンドウから表示されます。</span><span class="sxs-lookup"><span data-stu-id="a4887-168">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="a4887-169">コントロールを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="a4887-169">List controls</span></span>

![モバイル リスト コントロール](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="a4887-171">フィールド コントロール</span><span class="sxs-lookup"><span data-stu-id="a4887-171">Field controls</span></span>

![モバイル フィールド コントロール](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="a4887-173">開発者の考慮事項</span><span class="sxs-lookup"><span data-stu-id="a4887-173">Developer considerations</span></span>

<span data-ttu-id="a4887-174">タブを含むアプリを構築する場合は、Android クライアントと iOS クライアントの両方でタブがどのように機能Microsoft Teamsがあります。</span><span class="sxs-lookup"><span data-stu-id="a4887-174">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="a4887-175">以下のセクションでは、考慮する必要がある主要なシナリオの一部について説明します。</span><span class="sxs-lookup"><span data-stu-id="a4887-175">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="authentication"></a><span data-ttu-id="a4887-176">認証</span><span class="sxs-lookup"><span data-stu-id="a4887-176">Authentication</span></span>

<span data-ttu-id="a4887-177">モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4887-177">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="a4887-178">低帯域幅と断続的な接続</span><span class="sxs-lookup"><span data-stu-id="a4887-178">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="a4887-179">モバイル クライアントは、低帯域幅と断続的な接続で定期的に機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4887-179">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="a4887-180">アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4887-180">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="a4887-181">また、長時間実行されるプロセスに対してユーザーにフィードバックを提供するユーザー進行状況インジケーターも必要です。</span><span class="sxs-lookup"><span data-stu-id="a4887-181">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="a4887-182">タブは、承認チームの入力に基づいて、アプリケーションが許可リストに追加された後にのみ、モバイルで有効になります。</span><span class="sxs-lookup"><span data-stu-id="a4887-182">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="a4887-183">モバイルの応答性を確認するには、ユーザーに teamsubm@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="a4887-183">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="a4887-184">モバイル クライアントでのテスト</span><span class="sxs-lookup"><span data-stu-id="a4887-184">Testing on mobile clients</span></span>

<span data-ttu-id="a4887-185">さまざまなサイズと品質のモバイル デバイスでタブが適切に機能するを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4887-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="a4887-186">Android デバイスの場合 [、DevTools](~/tabs/how-to/developer-tools.md) を使用して、実行中にタブをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="a4887-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="a4887-187">タブレットを含む、高パフォーマンスデバイスと低パフォーマンスデバイスの両方でテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a4887-187">We recommend that you test on both high- and low-performance devices, including a tablet.</span></span>

### <a name="distribution"></a><span data-ttu-id="a4887-188">配布</span><span class="sxs-lookup"><span data-stu-id="a4887-188">Distribution</span></span>

<span data-ttu-id="a4887-189">モバイル クライアントで適切にTeams機能するには、モバイル ストアに一覧表示されているアプリTeams必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4887-189">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="a4887-190">タブの可用性と動作は、アプリが承認されたかどうかによって異なります。</span><span class="sxs-lookup"><span data-stu-id="a4887-190">Tab availability and behavior depends on whether your app is approved.</span></span>

#### <a name="apps-on-teams-store-approved-for-mobile"></a><span data-ttu-id="a4887-191">モバイル用にTeamsストア上のアプリ</span><span class="sxs-lookup"><span data-stu-id="a4887-191">Apps on Teams store approved for mobile</span></span>

<span data-ttu-id="a4887-192">次の表では、アプリがモバイル ストアに表示され、モバイルTeams承認された場合のタブの可用性と動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="a4887-192">The following table describes tab availability and behavior when the app is listed on the Teams store and approved for mobile use.</span></span>

|<span data-ttu-id="a4887-193">機能</span><span class="sxs-lookup"><span data-stu-id="a4887-193">Capability</span></span>   |<span data-ttu-id="a4887-194">モバイルの可用性</span><span class="sxs-lookup"><span data-stu-id="a4887-194">Mobile availability?</span></span>   |<span data-ttu-id="a4887-195">モバイル動作</span><span class="sxs-lookup"><span data-stu-id="a4887-195">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="a4887-196">チャネル</span><span class="sxs-lookup"><span data-stu-id="a4887-196">Channel</span></span> <br /> <span data-ttu-id="a4887-197">[グループ] タブ</span><span class="sxs-lookup"><span data-stu-id="a4887-197">and group tab</span></span>|<span data-ttu-id="a4887-198">はい</span><span class="sxs-lookup"><span data-stu-id="a4887-198">Yes</span></span>|<span data-ttu-id="a4887-199">アプリの構成を使用Teamsモバイル クライアントのタブが開 `contentUrl` きます。</span><span class="sxs-lookup"><span data-stu-id="a4887-199">Tab opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>|
|<span data-ttu-id="a4887-200">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="a4887-200">Personal app</span></span>|<span data-ttu-id="a4887-201">はい</span><span class="sxs-lookup"><span data-stu-id="a4887-201">Yes</span></span>|<span data-ttu-id="a4887-202">[個人用アプリ] タブの各タブが、Teamsを使用してモバイル クライアントに表示 `contentUrl` されます。</span><span class="sxs-lookup"><span data-stu-id="a4887-202">Each tab in the personal app tab opens in the Teams mobile client using its respective `contentUrl` configuration.</span></span>|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a><span data-ttu-id="a4887-203">モバイルで承認Teamsアプリストアのアプリ</span><span class="sxs-lookup"><span data-stu-id="a4887-203">Apps on Teams store not approved for mobile</span></span>

<span data-ttu-id="a4887-204">次の表では、アプリがモバイル ストアに表示されますが、モバイルでの使用がTeamsタブの可用性と動作について説明します。</span><span class="sxs-lookup"><span data-stu-id="a4887-204">The following table describes tab availability and behavior when the app is listed on the Teams store but not approved for mobile use.</span></span>

|<span data-ttu-id="a4887-205">機能</span><span class="sxs-lookup"><span data-stu-id="a4887-205">Capability</span></span>   |<span data-ttu-id="a4887-206">モバイルの可用性</span><span class="sxs-lookup"><span data-stu-id="a4887-206">Mobile availability?</span></span>|<span data-ttu-id="a4887-207">モバイル動作</span><span class="sxs-lookup"><span data-stu-id="a4887-207">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="a4887-208">[チャネルとグループ] タブ</span><span class="sxs-lookup"><span data-stu-id="a4887-208">Channel and group tab</span></span>|<span data-ttu-id="a4887-209">はい</span><span class="sxs-lookup"><span data-stu-id="a4887-209">Yes</span></span>|<span data-ttu-id="a4887-210">タブは、アプリの構成を使用して Teams モバイル クライアントではなく、デバイスの既定のブラウザーで開きます (ソース コードの関数にも含める `websiteUrl` 必要 `setSettings()` [があります](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions))。</span><span class="sxs-lookup"><span data-stu-id="a4887-210">Tab opens in the device's default browser instead of the Teams mobile client using your app's `websiteUrl` configuration (which also must be included in your source code's `setSettings()` [function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions)).</span></span> <span data-ttu-id="a4887-211">ただし、アプリの横にある [詳細] を選択し、[開く]を選択すると、Teams モバイルクライアントのタブが表示され、アプリの構成がトリガー `contentUrl` されます。</span><span class="sxs-lookup"><span data-stu-id="a4887-211">However, users can still view the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>|
|<span data-ttu-id="a4887-212">個人用アプリ</span><span class="sxs-lookup"><span data-stu-id="a4887-212">Personal app</span></span>|<span data-ttu-id="a4887-213">なし</span><span class="sxs-lookup"><span data-stu-id="a4887-213">No</span></span>|<span data-ttu-id="a4887-214">該当なし</span><span class="sxs-lookup"><span data-stu-id="a4887-214">Not applicable</span></span>|

#### <a name="apps-not-on-teams-store"></a><span data-ttu-id="a4887-215">アプリがストアTeamsしない</span><span class="sxs-lookup"><span data-stu-id="a4887-215">Apps not on Teams store</span></span>

<span data-ttu-id="a4887-216">アプリをサイドロードする場合や、組織のアプリ カタログに発行する場合、タブの動作は、モバイル向け Microsoft によって承認された Teams ストア アプリと同じです。</span><span class="sxs-lookup"><span data-stu-id="a4887-216">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>
