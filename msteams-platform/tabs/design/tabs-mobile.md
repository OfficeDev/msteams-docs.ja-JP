---
title: モバイルのタブ
description: モバイルで使用できるタブの設計ガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスフレームワーク個人用アプリモバイルタブ
ms.openlocfilehash: a1939465b04a1fe4b803efaf83402852ca536059
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279781"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="ebafc-104">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="ebafc-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="ebafc-105">Teams モバイル クライアントに [チャネル/グループ] タブを表示するように選択した場合は、`setSettings()` 構成には `websiteUrl` プロパティの値を設定する必要があります (下記参照)。</span><span class="sxs-lookup"><span data-stu-id="ebafc-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="ebafc-106">カスタムタブは、チャネル、グループチャット、または個人アプリの一部にすることができます (静的タブを含むアプリ、または1対1の bot を含むアプリ)。</span><span class="sxs-lookup"><span data-stu-id="ebafc-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="ebafc-107">個人用アプリは、アプリケーションドロワーのモバイルクライアントで使用できます。</span><span class="sxs-lookup"><span data-stu-id="ebafc-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="ebafc-108">アプリは、デスクトップまたは web クライアントからのみインストールでき、モバイルクライアントに表示されるまでに最大24時間かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="ebafc-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="ebafc-109">[チャネル] タブは、モバイルでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="ebafc-109">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="ebafc-110">既定の動作では、を使用して、 `websiteUrl` ブラウザーウィンドウでタブを起動します。</span><span class="sxs-lookup"><span data-stu-id="ebafc-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="ebafc-111">ただし、[] タブの横にあるオーバーフローメニューをクリックし、[開く] を選択することによって、モバイルクライアントに読み込むことができます `...` 。これは**Open**、を使用して、 `contentUrl` Teams モバイルクライアント内にタブをロードします。</span><span class="sxs-lookup"><span data-stu-id="ebafc-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="ebafc-112">個人用タブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="ebafc-112">Accessing personal tabs</span></span>

<span data-ttu-id="ebafc-113">次の図は、モバイルの [個人用] タブにアクセスする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="ebafc-113">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Teams モバイルアプリドロワーを示す図" border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="ebafc-115">チャネルタブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="ebafc-115">Accessing channel tabs</span></span>

<span data-ttu-id="ebafc-116">次の図は、モバイルの [チャネル] タブにアクセスする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="ebafc-116">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Teams の [モバイル] タブを示す図。" border="false":::

## <a name="design-considerations"></a><span data-ttu-id="ebafc-118">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="ebafc-118">Design considerations</span></span>

<span data-ttu-id="ebafc-119">弊社のモバイルプラットフォームを使用すると、アプリのコンテンツがメインの Teams ナビゲーションとは別にすべての画面を占有しているため、アプリをイマーシブ操作とすることができます。</span><span class="sxs-lookup"><span data-stu-id="ebafc-119">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="ebafc-120">Teams に適したイマーシブ環境を作成するには、次のガイドラインに従ってください。</span><span class="sxs-lookup"><span data-stu-id="ebafc-120">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="ebafc-121">レスポンシブ デザイン</span><span class="sxs-lookup"><span data-stu-id="ebafc-121">Responsive design</span></span>

<span data-ttu-id="ebafc-122">タブはさまざまな画面サイズのデバイス上で開くことができるため、 [応答性](https://www.w3schools.com/html/html_responsive.asp) の高い設計原則に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebafc-122">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="ebafc-123">すべてのキーの構成はモバイルデバイスでアクセスできる必要があり、ビューがゆがんではないことが必要です。</span><span class="sxs-lookup"><span data-stu-id="ebafc-123">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="ebafc-124">タブがモバイルデバイスにロードされている場合、すべてのボタンとリンクは、finger ベースのナビゲーションを使用して簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="ebafc-124">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="ebafc-125">レイアウト</span><span class="sxs-lookup"><span data-stu-id="ebafc-125">Layouts</span></span>

<span data-ttu-id="ebafc-126">タブの正しいレイアウトを選択することは重要です。</span><span class="sxs-lookup"><span data-stu-id="ebafc-126">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="ebafc-127">表示する情報の種類を検討し、簡単に使用できるように整理されたレイアウトを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebafc-127">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="ebafc-128">考えられるオプションには、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="ebafc-128">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="ebafc-129">1つのキャンバス</span><span class="sxs-lookup"><span data-stu-id="ebafc-129">Single canvas</span></span>

<span data-ttu-id="ebafc-130">これは、作業が行われる大きな領域の1つです。</span><span class="sxs-lookup"><span data-stu-id="ebafc-130">This is one large area where work gets done.</span></span> <span data-ttu-id="ebafc-131">Teams Wiki アプリは、このパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="ebafc-131">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="ebafc-132">コンテンツを小さなコンポーネントに分離しないアプリがある場合は、それに適しています。</span><span class="sxs-lookup"><span data-stu-id="ebafc-132">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Teams の [モバイルシングルキャンバス] タブを示す図" border="false":::

#### <a name="list"></a><span data-ttu-id="ebafc-134">リスト</span><span class="sxs-lookup"><span data-stu-id="ebafc-134">List</span></span>

<span data-ttu-id="ebafc-135">リストは大量のデータの並べ替えとフィルター処理を行うのに適しており、最も重要なものを最上位に保持するのに適しています。</span><span class="sxs-lookup"><span data-stu-id="ebafc-135">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="ebafc-136">並べ替え可能な列を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="ebafc-136">It is helpful to use sortable columns.</span></span> <span data-ttu-id="ebafc-137">アクションは、省略記号メニューの各リスト項目に追加できます。</span><span class="sxs-lookup"><span data-stu-id="ebafc-137">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Teams モバイルリストタブを示す図" border="false":::

#### <a name="grid"></a><span data-ttu-id="ebafc-139">グリッド</span><span class="sxs-lookup"><span data-stu-id="ebafc-139">Grid</span></span>

<span data-ttu-id="ebafc-140">グリッドは、ビジュアルの高い要素を表示するのに便利です。</span><span class="sxs-lookup"><span data-stu-id="ebafc-140">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="ebafc-141">フィルターまたは検索コントロールを上部に含めることができます。</span><span class="sxs-lookup"><span data-stu-id="ebafc-141">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="グリッドレイアウトを含む Teams mobile タブを示す図" border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="ebafc-143">モバイルに bot があるタブ</span><span class="sxs-lookup"><span data-stu-id="ebafc-143">Tabs with bots on mobile</span></span>

<span data-ttu-id="ebafc-144">次の例は、タブと bot を備えた個人のアプリです。</span><span class="sxs-lookup"><span data-stu-id="ebafc-144">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="タブと bot を備えたモバイル Teams アプリを示す図" border="false":::

## <a name="ui-components"></a><span data-ttu-id="ebafc-146">UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="ebafc-146">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="ebafc-147">カラー パレット</span><span class="sxs-lookup"><span data-stu-id="ebafc-147">Color palettes</span></span>

<span data-ttu-id="ebafc-148">背景、通知、テキスト、およびボタンに対して承認されたニュートラルパレットを使用すると、アプリが Teams での自宅をよりよく理解できるようになります。</span><span class="sxs-lookup"><span data-stu-id="ebafc-148">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="ebafc-149">Teams mobile には2つの色のテーマ (軽いと濃) があるため、アプリが両方に適したものになるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ebafc-149">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="ebafc-150">明るい色</span><span class="sxs-lookup"><span data-stu-id="ebafc-150">Light color</span></span>

![ライトカラーパレット](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="ebafc-152">暗い色</span><span class="sxs-lookup"><span data-stu-id="ebafc-152">Dark color</span></span>

![濃い色パレット](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="ebafc-154">ボタンとコントロール</span><span class="sxs-lookup"><span data-stu-id="ebafc-154">Buttons and controls</span></span>

<span data-ttu-id="ebafc-155">ボタンのスタイルを設定すると、どのような種類の動作が発生したかを伝えることができます。</span><span class="sxs-lookup"><span data-stu-id="ebafc-155">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="ebafc-156">さまざまな強調レベルを表示するように書式設定されたさまざまなボタンを維持しています。</span><span class="sxs-lookup"><span data-stu-id="ebafc-156">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="ebafc-157">ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="ebafc-157">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="ebafc-158">階層内のさまざまなレベルを通信するために、各カテゴリ内に主ボタンと副ボタンを設計しました。</span><span class="sxs-lookup"><span data-stu-id="ebafc-158">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="ebafc-159">ボタン</span><span class="sxs-lookup"><span data-stu-id="ebafc-159">Buttons</span></span>

<span data-ttu-id="ebafc-160">主ボタンとセカンダリボタン。</span><span class="sxs-lookup"><span data-stu-id="ebafc-160">Primary and secondary buttons.</span></span>

![ボタンの画像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="ebafc-162">選択コントロール</span><span class="sxs-lookup"><span data-stu-id="ebafc-162">Selection controls</span></span>

<span data-ttu-id="ebafc-163">ラジオボタン、チェックボックス、および切り替え。</span><span class="sxs-lookup"><span data-stu-id="ebafc-163">Radio buttons, checkboxes, and toggles.</span></span>

![選択コントロール](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="ebafc-165">Chiclets および pills</span><span class="sxs-lookup"><span data-stu-id="ebafc-165">Chiclets and pills</span></span>

![chiclets および pills](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="ebafc-167">文字体裁</span><span class="sxs-lookup"><span data-stu-id="ebafc-167">Typography</span></span>

<span data-ttu-id="ebafc-168">文字体裁はクリアで、意図的にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebafc-168">Typography should be clear and purposeful.</span></span> <span data-ttu-id="ebafc-169">重要な情報を強調して、混乱を減らすために複数のフォントとサイズを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="ebafc-169">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="ebafc-170">ローカライズと読みやすくするために、文のケースを使用し、すべての cap の使用を回避することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ebafc-170">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![モバイル typograph](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="ebafc-172">フィールドと flyouts</span><span class="sxs-lookup"><span data-stu-id="ebafc-172">Fields and flyouts</span></span>

<span data-ttu-id="ebafc-173">フィールドは、ユーザーがテキストを入力できる領域です。</span><span class="sxs-lookup"><span data-stu-id="ebafc-173">Fields are areas where users can input text.</span></span> <span data-ttu-id="ebafc-174">Flyouts はダイアログよりも軽量で、上部のウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="ebafc-174">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="ebafc-175">コントロールを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="ebafc-175">List controls</span></span>

![モバイルリストコントロール](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="ebafc-177">フィールドコントロール</span><span class="sxs-lookup"><span data-stu-id="ebafc-177">Field controls</span></span>

![モバイルフィールドコントロール](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="ebafc-179">開発者の考慮事項</span><span class="sxs-lookup"><span data-stu-id="ebafc-179">Developer considerations</span></span>

<span data-ttu-id="ebafc-180">タブを含むアプリを構築する場合は、Android と iOS の Microsoft Teams クライアントの両方でタブがどのように機能するかを考慮する必要があります (およびテストする必要があります)。</span><span class="sxs-lookup"><span data-stu-id="ebafc-180">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="ebafc-181">以下のセクションでは、考慮する必要がある主なシナリオのいくつかについて概説します。</span><span class="sxs-lookup"><span data-stu-id="ebafc-181">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="ebafc-182">モバイルクライアントでのテスト</span><span class="sxs-lookup"><span data-stu-id="ebafc-182">Testing on mobile clients</span></span>

<span data-ttu-id="ebafc-183">さまざまなサイズと品質のモバイルデバイスでタブが正しく機能することを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebafc-183">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="ebafc-184">Android デバイスの場合、 [Devtools](~/tabs/how-to/developer-tools.md) を使用して、実行中にタブをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="ebafc-184">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="ebafc-185">高および低パフォーマンスのデバイスに加えて、タブレット上でテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ebafc-185">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="ebafc-186">認証</span><span class="sxs-lookup"><span data-stu-id="ebafc-186">Authentication</span></span>

<span data-ttu-id="ebafc-187">モバイルクライアントで認証を行うには、Teams JavaScript SDK を少なくともバージョン1.4.1 にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebafc-187">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="ebafc-188">低帯域幅および断続的な接続</span><span class="sxs-lookup"><span data-stu-id="ebafc-188">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="ebafc-189">モバイルクライアントは、低帯域幅および断続的な接続で通常に機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebafc-189">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="ebafc-190">アプリでは、ユーザーにコンテキストメッセージを提供することによって、すべてのタイムアウトを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebafc-190">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="ebafc-191">また、長時間実行されているプロセスのユーザーにフィードバックを提供するために、ユーザーの進捗状況インジケーターを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ebafc-191">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>
