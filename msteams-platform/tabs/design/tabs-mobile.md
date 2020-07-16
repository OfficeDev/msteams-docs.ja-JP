---
title: モバイルのタブ
description: モバイルで使用できるタブの設計ガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスフレームワーク個人用アプリモバイルタブ
ms.openlocfilehash: ac547e74fd56e4f1da6c731959d8bb59dbe48213
ms.sourcegitcommit: 26b7404142706290810064f8216abaa1c262d1e5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "45145927"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="a61a9-104">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="a61a9-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="a61a9-105">Teams モバイル クライアントに [チャネル/グループ] タブを表示するように選択した場合は、`setSettings()` 構成には `websiteUrl` プロパティの値を設定する必要があります (下記参照)。</span><span class="sxs-lookup"><span data-stu-id="a61a9-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span> <span data-ttu-id="a61a9-106">[個人] タブは現在、[開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)で利用できます。</span><span class="sxs-lookup"><span data-stu-id="a61a9-106">Personal tabs are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span> <span data-ttu-id="a61a9-107">モバイル クライアントでのタブの完全なサポートは、間もなくリリースされる予定です。</span><span class="sxs-lookup"><span data-stu-id="a61a9-107">Full support for tabs on mobile clients will be released soon.</span></span> <span data-ttu-id="a61a9-108">更新プログラムの準備をするには、タブを作成するときに、ここに示す手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a61a9-108">To prepare for the update, you should follow the presented here when creating your tabs.</span></span>

<span data-ttu-id="a61a9-109">カスタムタブは、チャネル、グループチャット、または個人アプリの一部にすることができます (静的タブを含むアプリ、または1対1の bot を含むアプリ)。</span><span class="sxs-lookup"><span data-stu-id="a61a9-109">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="a61a9-110">個人用アプリは、アプリケーションドロワーのモバイルクライアントで使用できます。</span><span class="sxs-lookup"><span data-stu-id="a61a9-110">Personal apps are available on mobile clients in the App Drawer.</span></span> <span data-ttu-id="a61a9-111">アプリは、デスクトップまたは web クライアントからのみインストールでき、モバイルクライアントに表示されるまでに最大24時間かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="a61a9-111">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="a61a9-112">[グループ] タブと [チャネル] タブは、モバイルクライアントでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="a61a9-112">Group and channel tabs are available on mobile clients as well.</span></span> <span data-ttu-id="a61a9-113">既定の動作では、を使用して、 `websiteUrl` ブラウザーウィンドウでタブを起動します。</span><span class="sxs-lookup"><span data-stu-id="a61a9-113">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="a61a9-114">ただし、[] タブの横にあるオーバーフローメニューをクリックし、[開く] を選択することによって、モバイルクライアントに読み込むことができます `...` 。これは**Open**、を使用して、 `contentUrl` Teams モバイルクライアント内にタブをロードします。</span><span class="sxs-lookup"><span data-stu-id="a61a9-114">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

![モバイルアプリのドロアー](../../assets/images/personal-app-mobile.png)

## <a name="developer-considerations-for-mobile-support"></a><span data-ttu-id="a61a9-116">モバイルサポートの開発に関する考慮事項</span><span class="sxs-lookup"><span data-stu-id="a61a9-116">Developer considerations for mobile support</span></span>

<span data-ttu-id="a61a9-117">タブを含むアプリを構築する場合は、Android と iOS の Microsoft Teams クライアントの両方でタブがどのように機能するかを考慮する必要があります (およびテストする必要があります)。</span><span class="sxs-lookup"><span data-stu-id="a61a9-117">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="a61a9-118">以下のセクションでは、考慮する必要がある主なシナリオのいくつかについて概説します。</span><span class="sxs-lookup"><span data-stu-id="a61a9-118">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="a61a9-119">モバイルクライアントでのテスト</span><span class="sxs-lookup"><span data-stu-id="a61a9-119">Testing on mobile clients</span></span>

<span data-ttu-id="a61a9-120">さまざまなサイズと品質のモバイルデバイスでタブが正しく機能することを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a61a9-120">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="a61a9-121">Android デバイスの場合、 [Devtools](~/tabs/how-to/developer-tools.md)を使用して、実行中にタブをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="a61a9-121">For Android devices you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="a61a9-122">高および低パフォーマンスのデバイスに加えて、タブレット上でテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a61a9-122">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="a61a9-123">レスポンシブ デザイン</span><span class="sxs-lookup"><span data-stu-id="a61a9-123">Responsive design</span></span>

<span data-ttu-id="a61a9-124">タブはさまざまな画面サイズのデバイス上で開くことができるため、[応答性](https://www.w3schools.com/html/html_responsive.asp)の高い設計原則に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="a61a9-124">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="a61a9-125">すべてのキーの構成はモバイルデバイスでアクセスできる必要があり、ビューがゆがんではないことが必要です。</span><span class="sxs-lookup"><span data-stu-id="a61a9-125">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="a61a9-126">タブがモバイルデバイスにロードされている場合、すべてのボタンとリンクは、finger ベースのナビゲーションを使用して簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="a61a9-126">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="authentication"></a><span data-ttu-id="a61a9-127">認証</span><span class="sxs-lookup"><span data-stu-id="a61a9-127">Authentication</span></span>

<span data-ttu-id="a61a9-128">モバイルクライアントで認証を行うには、Teams JS SDK を少なくともバージョン1.4.1 にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a61a9-128">For authentication to work on mobile clients, you must upgrade you Teams JS SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth--intermittent-connections"></a><span data-ttu-id="a61a9-129">低帯域幅 & 断続的な接続</span><span class="sxs-lookup"><span data-stu-id="a61a9-129">Low bandwidth & intermittent connections</span></span>

<span data-ttu-id="a61a9-130">モバイルクライアントは、低帯域幅および断続的な接続で通常に機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a61a9-130">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="a61a9-131">アプリでは、ユーザーにコンテキストメッセージを提供することによって、すべてのタイムアウトを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a61a9-131">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="a61a9-132">また、長時間実行されているプロセスのユーザーにフィードバックを提供するために、ユーザーの進捗状況インジケーターを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a61a9-132">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

## <a name="design-considerations-for-mobile"></a><span data-ttu-id="a61a9-133">モバイルの設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="a61a9-133">Design considerations for mobile</span></span>

<span data-ttu-id="a61a9-134">弊社のモバイルプラットフォームを使用すると、アプリのコンテンツがメインの Teams ナビゲーションとは別にすべての画面を占有しているため、アプリをイマーシブ操作とすることができます。</span><span class="sxs-lookup"><span data-stu-id="a61a9-134">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="a61a9-135">Microsoft Teams クライアントにシームレスに適合するイマーシブの機能を作成するには、以下のガイドラインに従ってください。</span><span class="sxs-lookup"><span data-stu-id="a61a9-135">To create an immersive experience that fits seamlessly within the Microsoft Teams client, follow the guidelines below.</span></span>

### <a name="layouts"></a><span data-ttu-id="a61a9-136">レイアウト</span><span class="sxs-lookup"><span data-stu-id="a61a9-136">Layouts</span></span>

<span data-ttu-id="a61a9-137">タブの正しいレイアウトを選択することは重要です。</span><span class="sxs-lookup"><span data-stu-id="a61a9-137">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="a61a9-138">表示する情報の種類を検討し、簡単に使用できるように整理されたレイアウトを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a61a9-138">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="a61a9-139">考えられるオプションには、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="a61a9-139">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="a61a9-140">1つのキャンバス</span><span class="sxs-lookup"><span data-stu-id="a61a9-140">Single canvas</span></span>

<span data-ttu-id="a61a9-141">これは、作業が行われる大きな領域の1つです。</span><span class="sxs-lookup"><span data-stu-id="a61a9-141">This is one large area where work gets done.</span></span> <span data-ttu-id="a61a9-142">Wiki アプリは、このパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="a61a9-142">The Wiki app follows this pattern.</span></span> <span data-ttu-id="a61a9-143">コンテンツを小さなコンポーネントに分離しないアプリがある場合は、それに適しています。</span><span class="sxs-lookup"><span data-stu-id="a61a9-143">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

![単一キャンバスレイアウト](~/assets/images/mobile-single-canvas.png)

#### <a name="list"></a><span data-ttu-id="a61a9-145">リスト</span><span class="sxs-lookup"><span data-stu-id="a61a9-145">List</span></span>

<span data-ttu-id="a61a9-146">リストは大量のデータの並べ替えとフィルター処理を行うのに適しており、最も重要なものを最上位に保持するのに適しています。</span><span class="sxs-lookup"><span data-stu-id="a61a9-146">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="a61a9-147">並べ替え可能な列を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="a61a9-147">It is helpful to use sortable columns.</span></span> <span data-ttu-id="a61a9-148">アクションは、省略記号メニューの各リスト項目に追加できます。</span><span class="sxs-lookup"><span data-stu-id="a61a9-148">Actions can be added to each list item under the ellipsis menu.</span></span>

![リストレイアウト](~/assets/images/mobile-list.png)

#### <a name="grid"></a><span data-ttu-id="a61a9-150">グリッド</span><span class="sxs-lookup"><span data-stu-id="a61a9-150">Grid</span></span>

<span data-ttu-id="a61a9-151">グリッドは、ビジュアルの高い要素を表示するのに便利です。</span><span class="sxs-lookup"><span data-stu-id="a61a9-151">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="a61a9-152">フィルターまたは検索コントロールを上部に含めることができます。</span><span class="sxs-lookup"><span data-stu-id="a61a9-152">It helps to include a filter or search control at the top.</span></span>

![グリッドレイアウト](~/assets/images/mobile-grid.png)

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="a61a9-154">モバイルに bot があるタブ</span><span class="sxs-lookup"><span data-stu-id="a61a9-154">Tabs with bots on mobile</span></span>

<span data-ttu-id="a61a9-155">次に示すのは、2つの静的タブと bot を含む個人用アプリの例です。</span><span class="sxs-lookup"><span data-stu-id="a61a9-155">The below is an example personal app that contains two static tabs and a bot.</span></span>

![モバイルのタブとボット](~/assets/images/mobile-tab-with-bot.png)

### <a name="ui-components"></a><span data-ttu-id="a61a9-157">UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="a61a9-157">UI Components</span></span>

#### <a name="color-palettes"></a><span data-ttu-id="a61a9-158">カラー パレット</span><span class="sxs-lookup"><span data-stu-id="a61a9-158">Color palettes</span></span>

<span data-ttu-id="a61a9-159">背景、通知、テキスト、およびボタンに対して承認されたニュートラルパレットを使用すると、アプリが Teams での自宅をよりよく理解できるようになります。</span><span class="sxs-lookup"><span data-stu-id="a61a9-159">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="a61a9-160">Teams mobile には2つの色のテーマ (軽いと濃) があるため、アプリが両方に適したものになるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a61a9-160">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

##### <a name="light-color"></a><span data-ttu-id="a61a9-161">明るい色</span><span class="sxs-lookup"><span data-stu-id="a61a9-161">Light color</span></span>

![ライトカラーパレット](~/assets/images/light-color.png)

##### <a name="dark-color"></a><span data-ttu-id="a61a9-163">暗い色</span><span class="sxs-lookup"><span data-stu-id="a61a9-163">Dark color</span></span>

![濃い色パレット](~/assets/images/dark-color.png)

#### <a name="buttons-and-controls"></a><span data-ttu-id="a61a9-165">ボタンとコントロール</span><span class="sxs-lookup"><span data-stu-id="a61a9-165">Buttons and controls</span></span>

<span data-ttu-id="a61a9-166">ボタンのスタイルを設定すると、どのような種類の動作が発生したかを伝えることができます。</span><span class="sxs-lookup"><span data-stu-id="a61a9-166">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="a61a9-167">さまざまな強調レベルを表示するように書式設定されたさまざまなボタンを維持しています。</span><span class="sxs-lookup"><span data-stu-id="a61a9-167">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="a61a9-168">ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="a61a9-168">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="a61a9-169">階層内のさまざまなレベルを通信するために、各カテゴリ内に主ボタンと副ボタンを設計しました。</span><span class="sxs-lookup"><span data-stu-id="a61a9-169">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

![リモコン](~/assets/images/buttons.png)

![選択コントロール](~/assets/images/selection-controls.png)

![chiclets および pills](~/assets/images/chiclets-and-pills.png)

#### <a name="typography"></a><span data-ttu-id="a61a9-173">文字体裁</span><span class="sxs-lookup"><span data-stu-id="a61a9-173">Typography</span></span>

<span data-ttu-id="a61a9-174">文字体裁はクリアで、意図的にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a61a9-174">Typography should be clear and purposeful.</span></span> <span data-ttu-id="a61a9-175">重要な情報を強調して、混乱を減らすために複数のフォントとサイズを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="a61a9-175">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="a61a9-176">ローカライズと読みやすくするために、文のケースを使用し、すべての cap の使用を回避することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="a61a9-176">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![モバイル typograph](~/assets/images/mobile-typography.png)

#### <a name="fields-and-flyouts"></a><span data-ttu-id="a61a9-178">フィールドとポップアップ</span><span class="sxs-lookup"><span data-stu-id="a61a9-178">Fields and Flyouts</span></span>

<span data-ttu-id="a61a9-179">フィールドは、ユーザーがテキストを入力できる領域です。</span><span class="sxs-lookup"><span data-stu-id="a61a9-179">Fields are areas where users can input text.</span></span> <span data-ttu-id="a61a9-180">Flyouts はダイアログよりも軽量で、上部のウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="a61a9-180">Flyouts are more lightweight than dialogs, and appear from the top pane.</span></span>

##### <a name="list-controls"></a><span data-ttu-id="a61a9-181">コントロールを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="a61a9-181">List controls</span></span>

![モバイルリストコントロール](~/assets/images/mobile-list-controls.png)

##### <a name="field-controls"></a><span data-ttu-id="a61a9-183">フィールドコントロール</span><span class="sxs-lookup"><span data-stu-id="a61a9-183">Field controls</span></span>

![モバイルフィールドコントロール](~/assets/images/mobile-field-controls.png)
