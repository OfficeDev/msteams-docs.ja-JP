---
title: モバイルのタブ
description: モバイルで動作するタブを設計する際のガイドラインについて説明します。
ms.topic: conceptual
keywords: teams デザイン ガイドライン リファレンス フレームワーク 個人用アプリ モバイル タブ
ms.openlocfilehash: 72d1cf4623a9f4c1b5c993f1477f755b51d9fe64
ms.sourcegitcommit: 0e252159f53ff9b4452e0574b759bfe73cbf6c84
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "51762026"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="08d46-104">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="08d46-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="08d46-105">Teams モバイル クライアントに [チャネル/グループ] タブを表示するように選択した場合は、`setSettings()` 構成には `websiteUrl` プロパティの値を設定する必要があります (下記参照)。</span><span class="sxs-lookup"><span data-stu-id="08d46-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="08d46-106">カスタム タブは、チャネル、グループ チャット、または個人用アプリ (静的タブや 1 対 1 ボットを含むアプリ) に含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="08d46-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="08d46-107">個人用アプリは、アプリ ドロワー内のモバイル クライアントで利用できます。</span><span class="sxs-lookup"><span data-stu-id="08d46-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="08d46-108">アプリはデスクトップまたは Web クライアントからのみインストールできます。モバイル クライアントに表示するには最大 24 時間かかります。</span><span class="sxs-lookup"><span data-stu-id="08d46-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span> <span data-ttu-id="08d46-109">または、サインアウトしてサインインすることで、モバイル クライアントに再読み込みを適用できます。</span><span class="sxs-lookup"><span data-stu-id="08d46-109">Alternatively, you can enforce a reload on the mobile client by signing out and in.</span></span> <span data-ttu-id="08d46-110">これにより、モバイル アプリがすぐ利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="08d46-110">This should make the mobile app available right away.</span></span>

<span data-ttu-id="08d46-111">チャネル タブは、モバイルでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="08d46-111">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="08d46-112">既定の動作は現在、ブラウザー ウィンドウ `websiteUrl` でタブを起動するために使用します。</span><span class="sxs-lookup"><span data-stu-id="08d46-112">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="08d46-113">ただし、タブの横にあるオーバーフロー メニューをクリックし、[開く] を選択すると、モバイル クライアントに読み込まれ、Teams モバイル クライアント内にタブが読み込 `...`  `contentUrl` まれます。</span><span class="sxs-lookup"><span data-stu-id="08d46-113">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="08d46-114">個人用タブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="08d46-114">Accessing personal tabs</span></span>

<span data-ttu-id="08d46-115">次の図は、モバイルで個人用タブにアクセスする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="08d46-115">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Teams モバイル アプリの引き出しを示す図。" border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="08d46-117">チャネル タブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="08d46-117">Accessing channel tabs</span></span>

<span data-ttu-id="08d46-118">次の図は、モバイルでチャネル タブにアクセスする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="08d46-118">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Teams モバイル タブを示す図。" border="false":::

## <a name="design-considerations"></a><span data-ttu-id="08d46-120">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="08d46-120">Design considerations</span></span>

<span data-ttu-id="08d46-121">モバイル プラットフォームを使用すると、アプリのコンテンツが主要な Teams ナビゲーションとは別に、すべての画面を取り上げ、アプリを臨場感のあるエクスペリエンスにできます。</span><span class="sxs-lookup"><span data-stu-id="08d46-121">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="08d46-122">Teams に合った臨場感のあるエクスペリエンスを作成するには、次のガイドラインに従います。</span><span class="sxs-lookup"><span data-stu-id="08d46-122">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="08d46-123">レスポンシブ デザイン</span><span class="sxs-lookup"><span data-stu-id="08d46-123">Responsive design</span></span>

<span data-ttu-id="08d46-124">タブはさまざまな画面サイズのデバイスで開くことができるため、応答性の高い設計原則に従 [う必要](https://www.w3schools.com/html/html_responsive.asp) があります。</span><span class="sxs-lookup"><span data-stu-id="08d46-124">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="08d46-125">すべての主要な構成は、モバイル デバイスでアクセス可能で、ビューを歪めずに行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="08d46-125">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="08d46-126">タブがモバイル デバイスに読み込まれると、指ベースのナビゲーションを使用してすべてのボタンとリンクに簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="08d46-126">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="08d46-127">レイアウト</span><span class="sxs-lookup"><span data-stu-id="08d46-127">Layouts</span></span>

<span data-ttu-id="08d46-128">タブの適切なレイアウトを選択することが重要です。</span><span class="sxs-lookup"><span data-stu-id="08d46-128">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="08d46-129">提示する情報の種類を検討し、簡単に使用するためにそれを整理するレイアウトを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="08d46-129">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="08d46-130">いくつかの潜在的なオプションの概要を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="08d46-130">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="08d46-131">単一のキャンバス</span><span class="sxs-lookup"><span data-stu-id="08d46-131">Single canvas</span></span>

<span data-ttu-id="08d46-132">これは、作業が行われる 1 つの大きな領域です。</span><span class="sxs-lookup"><span data-stu-id="08d46-132">This is one large area where work gets done.</span></span> <span data-ttu-id="08d46-133">Teams Wiki アプリは、このパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="08d46-133">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="08d46-134">コンテンツを小さなコンポーネントに分けないアプリがある場合は、これは適しています。</span><span class="sxs-lookup"><span data-stu-id="08d46-134">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Teams モバイル単一キャンバス タブを示す図。" border="false":::

#### <a name="list"></a><span data-ttu-id="08d46-136">一覧表示</span><span class="sxs-lookup"><span data-stu-id="08d46-136">List</span></span>

<span data-ttu-id="08d46-137">リストは、大量のデータを並べ替え、フィルター処理する場合に最適で、最も重要な情報を一番上に保つことに最適です。</span><span class="sxs-lookup"><span data-stu-id="08d46-137">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="08d46-138">並べ替え可能な列を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="08d46-138">It is helpful to use sortable columns.</span></span> <span data-ttu-id="08d46-139">省略記号メニューの下の各リスト アイテムにアクションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="08d46-139">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Teams モバイル リスト タブを示す図。" border="false":::

#### <a name="grid"></a><span data-ttu-id="08d46-141">グリッド</span><span class="sxs-lookup"><span data-stu-id="08d46-141">Grid</span></span>

<span data-ttu-id="08d46-142">グリッドは、視覚的な要素を表示する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="08d46-142">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="08d46-143">上部にフィルターまたは検索コントロールを含めるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="08d46-143">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="グリッド レイアウトの Teams モバイル タブを示す図。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="08d46-145">モバイル上のボットを含むタブ</span><span class="sxs-lookup"><span data-stu-id="08d46-145">Tabs with bots on mobile</span></span>

<span data-ttu-id="08d46-146">次の例は、タブとボットを持つ個人用アプリです。</span><span class="sxs-lookup"><span data-stu-id="08d46-146">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="タブとボットを持つモバイル Teams アプリの方法を示す図。" border="false":::

## <a name="ui-components"></a><span data-ttu-id="08d46-148">UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="08d46-148">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="08d46-149">カラー パレット</span><span class="sxs-lookup"><span data-stu-id="08d46-149">Color palettes</span></span>

<span data-ttu-id="08d46-150">承認済みのニュートラル パレットを背景、通知、テキスト、ボタンに使用すると、アプリが Teams で自宅で使い分けるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="08d46-150">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="08d46-151">Teams モバイルには 2 つの色のテーマ (明るいテーマと暗いテーマ) が用意されていますので、両方でアプリが優れたものに見えるのを確認すると良い考えです。</span><span class="sxs-lookup"><span data-stu-id="08d46-151">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="08d46-152">明るい色</span><span class="sxs-lookup"><span data-stu-id="08d46-152">Light color</span></span>

![明るいカラー パレット](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="08d46-154">濃い色</span><span class="sxs-lookup"><span data-stu-id="08d46-154">Dark color</span></span>

![濃色パレット](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="08d46-156">ボタンとコントロール</span><span class="sxs-lookup"><span data-stu-id="08d46-156">Buttons and controls</span></span>

<span data-ttu-id="08d46-157">ボタンのスタイルを設定する方法は、トリガーするアクションの種類を伝えるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="08d46-157">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="08d46-158">さまざまなレベルの強調を表示するために書式設定されたボタンの広い範囲を維持します。</span><span class="sxs-lookup"><span data-stu-id="08d46-158">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="08d46-159">ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを指定できます。</span><span class="sxs-lookup"><span data-stu-id="08d46-159">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="08d46-160">階層内の異なるレベルを伝える目的で、各カテゴリ内のプライマリ ボタンとセカンダリ ボタンを設計しました。</span><span class="sxs-lookup"><span data-stu-id="08d46-160">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="08d46-161">ボタン</span><span class="sxs-lookup"><span data-stu-id="08d46-161">Buttons</span></span>

<span data-ttu-id="08d46-162">プライマリ ボタンとセカンダリ ボタン。</span><span class="sxs-lookup"><span data-stu-id="08d46-162">Primary and secondary buttons.</span></span>

![ボタンの画像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="08d46-164">選択コントロール</span><span class="sxs-lookup"><span data-stu-id="08d46-164">Selection controls</span></span>

<span data-ttu-id="08d46-165">ラジオ ボタン、チェック ボックス、およびトグル。</span><span class="sxs-lookup"><span data-stu-id="08d46-165">Radio buttons, checkboxes, and toggles.</span></span>

![選択コントロール](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="08d46-167">シックレットと丸薬</span><span class="sxs-lookup"><span data-stu-id="08d46-167">Chiclets and pills</span></span>

![シックレットと丸薬](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="08d46-169">文字体裁</span><span class="sxs-lookup"><span data-stu-id="08d46-169">Typography</span></span>

<span data-ttu-id="08d46-170">タイポグラフィは明確で目的に合ったものにしてください。</span><span class="sxs-lookup"><span data-stu-id="08d46-170">Typography should be clear and purposeful.</span></span> <span data-ttu-id="08d46-171">重要な情報を強調し、複数のフォントとサイズを使用して混乱を軽減しないようにします。</span><span class="sxs-lookup"><span data-stu-id="08d46-171">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="08d46-172">文の大文字と小文字を使用し、ローカライズと読み取り可能性のためにすべての大文字を使用しないようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="08d46-172">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![モバイルタイポグラフ](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="08d46-174">フィールドとフライアウト</span><span class="sxs-lookup"><span data-stu-id="08d46-174">Fields and flyouts</span></span>

<span data-ttu-id="08d46-175">フィールドは、ユーザーがテキストを入力できる領域です。</span><span class="sxs-lookup"><span data-stu-id="08d46-175">Fields are areas where users can input text.</span></span> <span data-ttu-id="08d46-176">フライアウトはダイアログよりも軽量で、上部ウィンドウから表示されます。</span><span class="sxs-lookup"><span data-stu-id="08d46-176">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="08d46-177">コントロールを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="08d46-177">List controls</span></span>

![モバイル リスト コントロール](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="08d46-179">フィールド コントロール</span><span class="sxs-lookup"><span data-stu-id="08d46-179">Field controls</span></span>

![モバイル フィールド コントロール](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="08d46-181">開発者の考慮事項</span><span class="sxs-lookup"><span data-stu-id="08d46-181">Developer considerations</span></span>

<span data-ttu-id="08d46-182">タブを含むアプリを構築する場合は、Android クライアントと iOS Microsoft Teams クライアントの両方でタブがどのように機能するのか検討 (およびテスト) する必要があります。</span><span class="sxs-lookup"><span data-stu-id="08d46-182">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="08d46-183">以下のセクションでは、考慮する必要がある主要なシナリオの一部について説明します。</span><span class="sxs-lookup"><span data-stu-id="08d46-183">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="08d46-184">モバイル クライアントでのテスト</span><span class="sxs-lookup"><span data-stu-id="08d46-184">Testing on mobile clients</span></span>

<span data-ttu-id="08d46-185">さまざまなサイズと品質のモバイル デバイスでタブが適切に機能するを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="08d46-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="08d46-186">Android デバイスの場合 [、DevTools](~/tabs/how-to/developer-tools.md) を使用して、実行中にタブをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="08d46-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="08d46-187">パフォーマンスの高いデバイスと低パフォーマンスデバイスの両方とタブレットでテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="08d46-187">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="08d46-188">認証</span><span class="sxs-lookup"><span data-stu-id="08d46-188">Authentication</span></span>

<span data-ttu-id="08d46-189">モバイル クライアントで認証を機能するには、Teams JavaScript SDK を少なくともバージョン 1.4.1 にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="08d46-189">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="08d46-190">低帯域幅と断続的な接続</span><span class="sxs-lookup"><span data-stu-id="08d46-190">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="08d46-191">モバイル クライアントは、低帯域幅と断続的な接続で定期的に機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="08d46-191">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="08d46-192">アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="08d46-192">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="08d46-193">また、長時間実行されるプロセスに対してユーザーにフィードバックを提供するユーザー進行状況インジケーターも必要です。</span><span class="sxs-lookup"><span data-stu-id="08d46-193">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="08d46-194">タブは、承認チームの入力に基づいて、アプリケーションが許可リストに追加された後にのみ、モバイルで有効になります。</span><span class="sxs-lookup"><span data-stu-id="08d46-194">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="08d46-195">モバイルの応答性を確認するには、ユーザーに teamsubm@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="08d46-195">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span> 
