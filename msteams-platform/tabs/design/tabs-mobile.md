---
title: モバイルのタブ
description: モバイルで動作するタブを設計する際のガイドラインについて説明します。
ms.topic: conceptual
keywords: Teams の設計ガイドラインリファレンス フレームワーク個人用アプリのモバイル タブ
ms.openlocfilehash: 462228daa2179482110e2deb42f0f16ab2f5d5ec
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014174"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="26bbd-104">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="26bbd-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="26bbd-105">Teams モバイル クライアントに [チャネル/グループ] タブを表示するように選択した場合は、`setSettings()` 構成には `websiteUrl` プロパティの値を設定する必要があります (下記参照)。</span><span class="sxs-lookup"><span data-stu-id="26bbd-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="26bbd-106">カスタム タブは、チャネル、グループ チャット、または個人用アプリ (静的なタブや 1 対 1 のボットを含むアプリ) の一部にできます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="26bbd-107">個人用アプリは、アプリ ドロワーのモバイル クライアントで利用できます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="26bbd-108">アプリはデスクトップまたは Web クライアントからのみインストールできます。モバイル クライアントに表示するには最大 24 時間かかります。</span><span class="sxs-lookup"><span data-stu-id="26bbd-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="26bbd-109">チャネル タブはモバイルでも利用できます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-109">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="26bbd-110">既定の動作では、現在、ブラウザー ウィンドウ `websiteUrl` でタブを起動します。</span><span class="sxs-lookup"><span data-stu-id="26bbd-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="26bbd-111">ただし、タブの横にあるオーバーフロー メニューをクリックして [開く] を選択すると、モバイル クライアントに読み込まれます。このメニューを使用して、Teams モバイル クライアント内にタブが読み込 `...`  `contentUrl` まれます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="26bbd-112">個人用タブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="26bbd-112">Accessing personal tabs</span></span>

<span data-ttu-id="26bbd-113">次の図は、モバイルで個人用タブにアクセスする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="26bbd-113">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Teams モバイル アプリのドロワーを示す図。" border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="26bbd-115">チャネル タブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="26bbd-115">Accessing channel tabs</span></span>

<span data-ttu-id="26bbd-116">次の図は、モバイルでチャネル タブにアクセスする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="26bbd-116">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Teams のモバイル タブを示す図。" border="false":::

## <a name="design-considerations"></a><span data-ttu-id="26bbd-118">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="26bbd-118">Design considerations</span></span>

<span data-ttu-id="26bbd-119">このモバイル プラットフォームを使用すると、アプリのコンテンツが Teams のメイン ナビゲーションとは別に、すべての画面を使いこなすイマーシブ エクスペリエンスをアプリに提供できます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-119">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="26bbd-120">Teams に適合するイマーシブ エクスペリエンスを作成するには、次のガイドラインに従います。</span><span class="sxs-lookup"><span data-stu-id="26bbd-120">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="26bbd-121">レスポンシブ デザイン</span><span class="sxs-lookup"><span data-stu-id="26bbd-121">Responsive design</span></span>

<span data-ttu-id="26bbd-122">タブはさまざまな画面サイズのデバイスで開くことができるため、レスポンシブ デザインの原則に従 [う](https://www.w3schools.com/html/html_responsive.asp) 必要があります。</span><span class="sxs-lookup"><span data-stu-id="26bbd-122">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="26bbd-123">すべての主要なコンストラクトにモバイル デバイスでアクセスできる必要があります。また、ビューがゆがんでも表示されません。</span><span class="sxs-lookup"><span data-stu-id="26bbd-123">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="26bbd-124">タブがモバイル デバイスに読み込まれると、指ベースのナビゲーションを使用してすべてのボタンとリンクに簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-124">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="26bbd-125">レイアウト</span><span class="sxs-lookup"><span data-stu-id="26bbd-125">Layouts</span></span>

<span data-ttu-id="26bbd-126">タブの適切なレイアウトを選択することが重要です。</span><span class="sxs-lookup"><span data-stu-id="26bbd-126">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="26bbd-127">表示する情報の種類を検討し、簡単に使用するために整理するレイアウトを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="26bbd-127">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="26bbd-128">次に、考え得るオプションの一部を示します。</span><span class="sxs-lookup"><span data-stu-id="26bbd-128">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="26bbd-129">単一キャンバス</span><span class="sxs-lookup"><span data-stu-id="26bbd-129">Single canvas</span></span>

<span data-ttu-id="26bbd-130">これは、作業が完了する 1 つの大きな領域です。</span><span class="sxs-lookup"><span data-stu-id="26bbd-130">This is one large area where work gets done.</span></span> <span data-ttu-id="26bbd-131">Teams Wiki アプリは、このパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="26bbd-131">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="26bbd-132">コンテンツを小さなコンポーネントに分離しないアプリがある場合は、この方法が適しています。</span><span class="sxs-lookup"><span data-stu-id="26bbd-132">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Teams モバイルの単一キャンバス タブを示す図。" border="false":::

#### <a name="list"></a><span data-ttu-id="26bbd-134">リスト</span><span class="sxs-lookup"><span data-stu-id="26bbd-134">List</span></span>

<span data-ttu-id="26bbd-135">リストは、大量のデータを並べ替え、フィルター処理する場合に最適で、最も重要な情報を一番上に維持するのに最適です。</span><span class="sxs-lookup"><span data-stu-id="26bbd-135">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="26bbd-136">並べ替え可能な列を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="26bbd-136">It is helpful to use sortable columns.</span></span> <span data-ttu-id="26bbd-137">アクションは、省略記号メニューの下の各リスト アイテムに追加できます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-137">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Teams のモバイル リスト タブを示す図。" border="false":::

#### <a name="grid"></a><span data-ttu-id="26bbd-139">グリッド</span><span class="sxs-lookup"><span data-stu-id="26bbd-139">Grid</span></span>

<span data-ttu-id="26bbd-140">グリッドは、視覚的な要素を表示する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="26bbd-140">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="26bbd-141">上部にフィルター コントロールまたは検索コントロールを含めるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-141">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="グリッド レイアウトが表示された Teams モバイル タブを示す図。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="26bbd-143">モバイル上のボットを含むタブ</span><span class="sxs-lookup"><span data-stu-id="26bbd-143">Tabs with bots on mobile</span></span>

<span data-ttu-id="26bbd-144">次の例は、タブとボットを含む個人用アプリです。</span><span class="sxs-lookup"><span data-stu-id="26bbd-144">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="タブとボットを含むモバイル Teams アプリを示す図。" border="false":::

## <a name="ui-components"></a><span data-ttu-id="26bbd-146">UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="26bbd-146">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="26bbd-147">カラー パレット</span><span class="sxs-lookup"><span data-stu-id="26bbd-147">Color palettes</span></span>

<span data-ttu-id="26bbd-148">承認されたニュートラル パレットを背景、通知、テキスト、ボタンに使用すると、アプリの Teams での使用感を高めることができます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-148">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="26bbd-149">Teams モバイルには 2 つのテーマ (淡色と濃色) が用意されているので、両方でアプリが見栄え良く表示されるのを確認する方が良い方法です。</span><span class="sxs-lookup"><span data-stu-id="26bbd-149">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="26bbd-150">明るい色</span><span class="sxs-lookup"><span data-stu-id="26bbd-150">Light color</span></span>

![淡色パレット](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="26bbd-152">濃色</span><span class="sxs-lookup"><span data-stu-id="26bbd-152">Dark color</span></span>

![濃色パレット](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="26bbd-154">ボタンとコントロール</span><span class="sxs-lookup"><span data-stu-id="26bbd-154">Buttons and controls</span></span>

<span data-ttu-id="26bbd-155">ボタンのスタイルを設定する方法は、トリガーするアクションの種類を伝えるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-155">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="26bbd-156">さまざまなレベルの強調を表示するために書式設定された幅広いボタンを維持しています。</span><span class="sxs-lookup"><span data-stu-id="26bbd-156">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="26bbd-157">ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを設定できます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-157">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="26bbd-158">階層内の異なるレベルを伝える目的で、各カテゴリ内のプライマリ ボタンとセカンダリ ボタンを設計しました。</span><span class="sxs-lookup"><span data-stu-id="26bbd-158">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="26bbd-159">ボタン</span><span class="sxs-lookup"><span data-stu-id="26bbd-159">Buttons</span></span>

<span data-ttu-id="26bbd-160">プライマリ ボタンとセカンダリ ボタン。</span><span class="sxs-lookup"><span data-stu-id="26bbd-160">Primary and secondary buttons.</span></span>

![ボタンの画像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="26bbd-162">選択コントロール</span><span class="sxs-lookup"><span data-stu-id="26bbd-162">Selection controls</span></span>

<span data-ttu-id="26bbd-163">ラジオ ボタン、チェック ボックス、トグル。</span><span class="sxs-lookup"><span data-stu-id="26bbd-163">Radio buttons, checkboxes, and toggles.</span></span>

![選択コントロール](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="26bbd-165">小冊子とくし</span><span class="sxs-lookup"><span data-stu-id="26bbd-165">Chiclets and pills</span></span>

![のり子とくじ](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="26bbd-167">文字体裁</span><span class="sxs-lookup"><span data-stu-id="26bbd-167">Typography</span></span>

<span data-ttu-id="26bbd-168">文字体裁は明確で、目的に合ったものにしてください。</span><span class="sxs-lookup"><span data-stu-id="26bbd-168">Typography should be clear and purposeful.</span></span> <span data-ttu-id="26bbd-169">重要な情報を強調し、混乱を減らすために複数のフォントとサイズを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="26bbd-169">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="26bbd-170">文の大文字と小文字を使用し、ローカライズと読み読みのためにすべての大文字の使用を避けることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="26bbd-170">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![モバイル入力ミス](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="26bbd-172">フィールドとフライアウト</span><span class="sxs-lookup"><span data-stu-id="26bbd-172">Fields and flyouts</span></span>

<span data-ttu-id="26bbd-173">フィールドは、ユーザーがテキストを入力できる領域です。</span><span class="sxs-lookup"><span data-stu-id="26bbd-173">Fields are areas where users can input text.</span></span> <span data-ttu-id="26bbd-174">フライアウトはダイアログよりも軽量で、上部のウィンドウから表示されます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-174">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="26bbd-175">コントロールを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="26bbd-175">List controls</span></span>

![モバイル リスト コントロール](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="26bbd-177">フィールド コントロール</span><span class="sxs-lookup"><span data-stu-id="26bbd-177">Field controls</span></span>

![モバイル フィールド コントロール](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="26bbd-179">開発者の考慮事項</span><span class="sxs-lookup"><span data-stu-id="26bbd-179">Developer considerations</span></span>

<span data-ttu-id="26bbd-180">タブを含むアプリを作成する場合は、Android と iOS の両方の Microsoft Teams クライアントでタブがどのように機能するのか検討 (およびテスト) する必要があります。</span><span class="sxs-lookup"><span data-stu-id="26bbd-180">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="26bbd-181">以下のセクションでは、考慮する必要がある重要なシナリオの一部について説明します。</span><span class="sxs-lookup"><span data-stu-id="26bbd-181">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="26bbd-182">モバイル クライアントでのテスト</span><span class="sxs-lookup"><span data-stu-id="26bbd-182">Testing on mobile clients</span></span>

<span data-ttu-id="26bbd-183">さまざまなサイズと特性を持つモバイル デバイスでタブが正しく機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="26bbd-183">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="26bbd-184">Android デバイスでは [、DevTools を使用して](~/tabs/how-to/developer-tools.md) 、実行中にタブをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="26bbd-184">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="26bbd-185">パフォーマンスの高いデバイスと低パフォーマンスデバイスの両方で、タブレットでテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="26bbd-185">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="26bbd-186">認証</span><span class="sxs-lookup"><span data-stu-id="26bbd-186">Authentication</span></span>

<span data-ttu-id="26bbd-187">モバイル クライアントで認証を機能するには、Teams JavaScript SDK をバージョン 1.4.1 以上にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="26bbd-187">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="26bbd-188">低帯域幅および断続的な接続</span><span class="sxs-lookup"><span data-stu-id="26bbd-188">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="26bbd-189">モバイル クライアントは、低帯域幅および断続的な接続で定期的に機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="26bbd-189">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="26bbd-190">アプリでは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="26bbd-190">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="26bbd-191">また、長時間実行されるプロセスに関するフィードバックをユーザーに提供する進行状況インジケーターも必要です。</span><span class="sxs-lookup"><span data-stu-id="26bbd-191">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>
