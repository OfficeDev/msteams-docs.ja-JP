---
title: モバイルのタブ
description: モバイルで使用できるタブの設計ガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスフレームワーク個人用アプリモバイルタブ
ms.openlocfilehash: d47039c245b8e262af6e1f60bc0c644dc7e65bd6
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819047"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="7df9b-104">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="7df9b-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="7df9b-105">Teams モバイル クライアントに [チャネル/グループ] タブを表示するように選択した場合は、`setSettings()` 構成には `websiteUrl` プロパティの値を設定する必要があります (下記参照)。</span><span class="sxs-lookup"><span data-stu-id="7df9b-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="7df9b-106">カスタムタブは、チャネル、グループチャット、または個人アプリの一部にすることができます (静的タブを含むアプリ、または1対1の bot を含むアプリ)。</span><span class="sxs-lookup"><span data-stu-id="7df9b-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="7df9b-107">個人用アプリは、アプリケーションドロワーのモバイルクライアントで使用できます。</span><span class="sxs-lookup"><span data-stu-id="7df9b-107">Personal apps are available on mobile clients in the App Drawer.</span></span> <span data-ttu-id="7df9b-108">アプリは、デスクトップまたは web クライアントからのみインストールでき、モバイルクライアントに表示されるまでに最大24時間かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="7df9b-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="7df9b-109">[グループ] タブと [チャネル] タブは、モバイルクライアントでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="7df9b-109">Group and channel tabs are available on mobile clients as well.</span></span> <span data-ttu-id="7df9b-110">既定の動作では、を使用して、 `websiteUrl` ブラウザーウィンドウでタブを起動します。</span><span class="sxs-lookup"><span data-stu-id="7df9b-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="7df9b-111">ただし、[] タブの横にあるオーバーフローメニューをクリックし、[開く] を選択することによって、モバイルクライアントに読み込むことができます `...` 。これは**Open**、を使用して、 `contentUrl` Teams モバイルクライアント内にタブをロードします。</span><span class="sxs-lookup"><span data-stu-id="7df9b-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

![モバイルアプリのドロアー](../../assets/images/personal-app-mobile.png)

## <a name="developer-considerations-for-mobile-support"></a><span data-ttu-id="7df9b-113">モバイルサポートの開発に関する考慮事項</span><span class="sxs-lookup"><span data-stu-id="7df9b-113">Developer considerations for mobile support</span></span>

<span data-ttu-id="7df9b-114">タブを含むアプリを構築する場合は、Android と iOS の Microsoft Teams クライアントの両方でタブがどのように機能するかを考慮する必要があります (およびテストする必要があります)。</span><span class="sxs-lookup"><span data-stu-id="7df9b-114">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="7df9b-115">以下のセクションでは、考慮する必要がある主なシナリオのいくつかについて概説します。</span><span class="sxs-lookup"><span data-stu-id="7df9b-115">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="7df9b-116">モバイルクライアントでのテスト</span><span class="sxs-lookup"><span data-stu-id="7df9b-116">Testing on mobile clients</span></span>

<span data-ttu-id="7df9b-117">さまざまなサイズと品質のモバイルデバイスでタブが正しく機能することを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7df9b-117">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="7df9b-118">Android デバイスの場合、 [Devtools](~/tabs/how-to/developer-tools.md) を使用して、実行中にタブをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="7df9b-118">For Android devices you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="7df9b-119">高および低パフォーマンスのデバイスに加えて、タブレット上でテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7df9b-119">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="7df9b-120">レスポンシブ デザイン</span><span class="sxs-lookup"><span data-stu-id="7df9b-120">Responsive design</span></span>

<span data-ttu-id="7df9b-121">タブはさまざまな画面サイズのデバイス上で開くことができるため、 [応答性](https://www.w3schools.com/html/html_responsive.asp) の高い設計原則に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="7df9b-121">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="7df9b-122">すべてのキーの構成はモバイルデバイスでアクセスできる必要があり、ビューがゆがんではないことが必要です。</span><span class="sxs-lookup"><span data-stu-id="7df9b-122">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="7df9b-123">タブがモバイルデバイスにロードされている場合、すべてのボタンとリンクは、finger ベースのナビゲーションを使用して簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="7df9b-123">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="authentication"></a><span data-ttu-id="7df9b-124">認証</span><span class="sxs-lookup"><span data-stu-id="7df9b-124">Authentication</span></span>

<span data-ttu-id="7df9b-125">モバイルクライアントで認証を行うには、Teams JS SDK を少なくともバージョン1.4.1 にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7df9b-125">For authentication to work on mobile clients, you must upgrade you Teams JS SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth--intermittent-connections"></a><span data-ttu-id="7df9b-126">低帯域幅 & 断続的な接続</span><span class="sxs-lookup"><span data-stu-id="7df9b-126">Low bandwidth & intermittent connections</span></span>

<span data-ttu-id="7df9b-127">モバイルクライアントは、低帯域幅および断続的な接続で通常に機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7df9b-127">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="7df9b-128">アプリでは、ユーザーにコンテキストメッセージを提供することによって、すべてのタイムアウトを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7df9b-128">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="7df9b-129">また、長時間実行されているプロセスのユーザーにフィードバックを提供するために、ユーザーの進捗状況インジケーターを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7df9b-129">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

## <a name="design-considerations-for-mobile"></a><span data-ttu-id="7df9b-130">モバイルの設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="7df9b-130">Design considerations for mobile</span></span>

<span data-ttu-id="7df9b-131">弊社のモバイルプラットフォームを使用すると、アプリのコンテンツがメインの Teams ナビゲーションとは別にすべての画面を占有しているため、アプリをイマーシブ操作とすることができます。</span><span class="sxs-lookup"><span data-stu-id="7df9b-131">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="7df9b-132">Microsoft Teams クライアントにシームレスに適合するイマーシブの機能を作成するには、以下のガイドラインに従ってください。</span><span class="sxs-lookup"><span data-stu-id="7df9b-132">To create an immersive experience that fits seamlessly within the Microsoft Teams client, follow the guidelines below.</span></span>

### <a name="layouts"></a><span data-ttu-id="7df9b-133">レイアウト</span><span class="sxs-lookup"><span data-stu-id="7df9b-133">Layouts</span></span>

<span data-ttu-id="7df9b-134">タブの正しいレイアウトを選択することは重要です。</span><span class="sxs-lookup"><span data-stu-id="7df9b-134">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="7df9b-135">表示する情報の種類を検討し、簡単に使用できるように整理されたレイアウトを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7df9b-135">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="7df9b-136">考えられるオプションには、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="7df9b-136">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="7df9b-137">1つのキャンバス</span><span class="sxs-lookup"><span data-stu-id="7df9b-137">Single canvas</span></span>

<span data-ttu-id="7df9b-138">これは、作業が行われる大きな領域の1つです。</span><span class="sxs-lookup"><span data-stu-id="7df9b-138">This is one large area where work gets done.</span></span> <span data-ttu-id="7df9b-139">Wiki アプリは、このパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="7df9b-139">The Wiki app follows this pattern.</span></span> <span data-ttu-id="7df9b-140">コンテンツを小さなコンポーネントに分離しないアプリがある場合は、それに適しています。</span><span class="sxs-lookup"><span data-stu-id="7df9b-140">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

![単一キャンバスレイアウト](~/assets/images/mobile-single-canvas.png)

#### <a name="list"></a><span data-ttu-id="7df9b-142">リスト</span><span class="sxs-lookup"><span data-stu-id="7df9b-142">List</span></span>

<span data-ttu-id="7df9b-143">リストは大量のデータの並べ替えとフィルター処理を行うのに適しており、最も重要なものを最上位に保持するのに適しています。</span><span class="sxs-lookup"><span data-stu-id="7df9b-143">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="7df9b-144">並べ替え可能な列を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="7df9b-144">It is helpful to use sortable columns.</span></span> <span data-ttu-id="7df9b-145">アクションは、省略記号メニューの各リスト項目に追加できます。</span><span class="sxs-lookup"><span data-stu-id="7df9b-145">Actions can be added to each list item under the ellipsis menu.</span></span>

![リストレイアウト](~/assets/images/mobile-list.png)

#### <a name="grid"></a><span data-ttu-id="7df9b-147">グリッド</span><span class="sxs-lookup"><span data-stu-id="7df9b-147">Grid</span></span>

<span data-ttu-id="7df9b-148">グリッドは、ビジュアルの高い要素を表示するのに便利です。</span><span class="sxs-lookup"><span data-stu-id="7df9b-148">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="7df9b-149">フィルターまたは検索コントロールを上部に含めることができます。</span><span class="sxs-lookup"><span data-stu-id="7df9b-149">It helps to include a filter or search control at the top.</span></span>

![グリッドレイアウト](~/assets/images/mobile-grid.png)

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="7df9b-151">モバイルに bot があるタブ</span><span class="sxs-lookup"><span data-stu-id="7df9b-151">Tabs with bots on mobile</span></span>

<span data-ttu-id="7df9b-152">次に示すのは、2つの静的タブと bot を含む個人用アプリの例です。</span><span class="sxs-lookup"><span data-stu-id="7df9b-152">The below is an example personal app that contains two static tabs and a bot.</span></span>

![モバイルのタブとボット](~/assets/images/mobile-tab-with-bot.png)

### <a name="ui-components"></a><span data-ttu-id="7df9b-154">UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="7df9b-154">UI Components</span></span>

#### <a name="color-palettes"></a><span data-ttu-id="7df9b-155">カラー パレット</span><span class="sxs-lookup"><span data-stu-id="7df9b-155">Color palettes</span></span>

<span data-ttu-id="7df9b-156">背景、通知、テキスト、およびボタンに対して承認されたニュートラルパレットを使用すると、アプリが Teams での自宅をよりよく理解できるようになります。</span><span class="sxs-lookup"><span data-stu-id="7df9b-156">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="7df9b-157">Teams mobile には2つの色のテーマ (軽いと濃) があるため、アプリが両方に適したものになるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7df9b-157">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

##### <a name="light-color"></a><span data-ttu-id="7df9b-158">明るい色</span><span class="sxs-lookup"><span data-stu-id="7df9b-158">Light color</span></span>

![ライトカラーパレット](~/assets/images/light-color.png)

##### <a name="dark-color"></a><span data-ttu-id="7df9b-160">暗い色</span><span class="sxs-lookup"><span data-stu-id="7df9b-160">Dark color</span></span>

![濃い色パレット](~/assets/images/dark-color.png)

#### <a name="buttons-and-controls"></a><span data-ttu-id="7df9b-162">ボタンとコントロール</span><span class="sxs-lookup"><span data-stu-id="7df9b-162">Buttons and controls</span></span>

<span data-ttu-id="7df9b-163">ボタンのスタイルを設定すると、どのような種類の動作が発生したかを伝えることができます。</span><span class="sxs-lookup"><span data-stu-id="7df9b-163">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="7df9b-164">さまざまな強調レベルを表示するように書式設定されたさまざまなボタンを維持しています。</span><span class="sxs-lookup"><span data-stu-id="7df9b-164">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="7df9b-165">ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="7df9b-165">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="7df9b-166">階層内のさまざまなレベルを通信するために、各カテゴリ内に主ボタンと副ボタンを設計しました。</span><span class="sxs-lookup"><span data-stu-id="7df9b-166">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

![ボタンの画像](~/assets/images/buttons.png)

![選択コントロール](~/assets/images/selection-controls.png)

![chiclets および pills](~/assets/images/chiclets-and-pills.png)

#### <a name="typography"></a><span data-ttu-id="7df9b-170">文字体裁</span><span class="sxs-lookup"><span data-stu-id="7df9b-170">Typography</span></span>

<span data-ttu-id="7df9b-171">文字体裁はクリアで、意図的にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7df9b-171">Typography should be clear and purposeful.</span></span> <span data-ttu-id="7df9b-172">重要な情報を強調して、混乱を減らすために複数のフォントとサイズを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="7df9b-172">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="7df9b-173">ローカライズと読みやすくするために、文のケースを使用し、すべての cap の使用を回避することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7df9b-173">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![モバイル typograph](~/assets/images/mobile-typography.png)

#### <a name="fields-and-flyouts"></a><span data-ttu-id="7df9b-175">フィールドとポップアップ</span><span class="sxs-lookup"><span data-stu-id="7df9b-175">Fields and Flyouts</span></span>

<span data-ttu-id="7df9b-176">フィールドは、ユーザーがテキストを入力できる領域です。</span><span class="sxs-lookup"><span data-stu-id="7df9b-176">Fields are areas where users can input text.</span></span> <span data-ttu-id="7df9b-177">Flyouts はダイアログよりも軽量で、上部のウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="7df9b-177">Flyouts are more lightweight than dialogs, and appear from the top pane.</span></span>

##### <a name="list-controls"></a><span data-ttu-id="7df9b-178">コントロールを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="7df9b-178">List controls</span></span>

![モバイルリストコントロール](~/assets/images/mobile-list-controls.png)

##### <a name="field-controls"></a><span data-ttu-id="7df9b-180">フィールドコントロール</span><span class="sxs-lookup"><span data-stu-id="7df9b-180">Field controls</span></span>

![モバイルフィールドコントロール](~/assets/images/mobile-field-controls.png)
