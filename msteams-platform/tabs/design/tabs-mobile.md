---
title: モバイルのタブ
description: モバイルで使用できるタブの設計ガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスフレームワーク個人用アプリモバイルタブ
ms.openlocfilehash: 928fb8586434eca9cc1577fd45c6b94594724d7f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674889"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="1aac7-104">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="1aac7-104">Tabs on mobile</span></span>

> [!Important]
> <span data-ttu-id="1aac7-105">モバイルクライアントでのタブの完全なサポートは、近日中に予定されています。</span><span class="sxs-lookup"><span data-stu-id="1aac7-105">Full support for tabs on mobile clients is coming soon.</span></span> <span data-ttu-id="1aac7-106">この変更を準備するには、タブを作成するときにこのガイダンスに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-106">To prepare for this change you should follow the this guidance when creating your tabs.</span></span> <span data-ttu-id="1aac7-107">個人用アプリ (静的タブ) は現在、[開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)で利用できます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-107">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span> <span data-ttu-id="1aac7-108">およびチャネル/グループチャットのタブは、タブ`...`の [オーバーフロー] メニューから使用できます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-108">and channel / group chat tabs are available in the `...` overflow menu for the tab.</span></span>
>
> <span data-ttu-id="1aac7-109">タブの完全なサポートがリリースされると、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-109">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="1aac7-110">すべてのタブがモバイルで常に使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-110">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="1aac7-111">`contentUrl` **は、モバイル Teams クライアントにロードされ**ます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-111">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="1aac7-112">[チャネル/グループ] タブでは、ユーザーは自分`websiteUrl`のを経由して別のブラウザーで`contentUrl`タブを開くことができます。ただし、は最初に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-112">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>
> * <span data-ttu-id="1aac7-113">タブで認証を使用している場合は、Teams の JavaScript SDK をバージョン1.4.1 以降にアップグレードする必要があります。認証は失敗します。</span><span class="sxs-lookup"><span data-stu-id="1aac7-113">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>

<span data-ttu-id="1aac7-114">カスタムタブは、チャネル、グループチャット、または個人アプリの一部にすることができます (静的タブを含むアプリ、または1対1の bot を含むアプリ)。</span><span class="sxs-lookup"><span data-stu-id="1aac7-114">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="1aac7-115">個人用アプリは、アプリケーションドロワーのモバイルクライアントで使用できます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-115">Personal apps are available on mobile clients in the App Drawer.</span></span> <span data-ttu-id="1aac7-116">アプリは、デスクトップまたは web クライアントからのみインストールでき、モバイルクライアントに表示されるまでに最大24時間かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-116">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="1aac7-117">[グループ] タブと [チャネル] タブは、モバイルクライアントでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-117">Group and channel tabs are available on mobile clients as well.</span></span> <span data-ttu-id="1aac7-118">既定の動作では、を使用`websiteUrl`して、ブラウザーウィンドウでタブを起動します。</span><span class="sxs-lookup"><span data-stu-id="1aac7-118">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="1aac7-119">ただし、[] タブの横にある`...`オーバーフローメニューをクリックし、[**開く**] を選択することによって、モバイル`contentUrl`クライアントに読み込むことができます。これは、を使用して、Teams モバイルクライアント内にタブをロードします。</span><span class="sxs-lookup"><span data-stu-id="1aac7-119">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

![モバイルアプリのドロアー](~/assets/images/app-drawer.png)

## <a name="developer-considerations-for-mobile-support"></a><span data-ttu-id="1aac7-121">モバイルサポートの開発に関する考慮事項</span><span class="sxs-lookup"><span data-stu-id="1aac7-121">Developer considerations for mobile support</span></span>

<span data-ttu-id="1aac7-122">タブを含むアプリを構築する場合は、Android と iOS の Microsoft Teams クライアントの両方でタブがどのように機能するかを考慮する必要があります (およびテストする必要があります)。</span><span class="sxs-lookup"><span data-stu-id="1aac7-122">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="1aac7-123">以下のセクションでは、考慮する必要がある主なシナリオのいくつかについて概説します。</span><span class="sxs-lookup"><span data-stu-id="1aac7-123">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="1aac7-124">モバイルクライアントでのテスト</span><span class="sxs-lookup"><span data-stu-id="1aac7-124">Testing on mobile clients</span></span>

<span data-ttu-id="1aac7-125">さまざまなサイズと品質のモバイルデバイスでタブが正しく機能することを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-125">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="1aac7-126">Android デバイスの場合、 [Devtools](~/tabs/how-to/developer-tools.md)を使用して、実行中にタブをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-126">For Android devices you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="1aac7-127">高および低パフォーマンスのデバイスに加えて、タブレット上でテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1aac7-127">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="1aac7-128">レスポンシブ デザイン</span><span class="sxs-lookup"><span data-stu-id="1aac7-128">Responsive design</span></span>

<span data-ttu-id="1aac7-129">タブはさまざまな画面サイズのデバイス上で開くことができるため、[応答性](https://www.w3schools.com/html/html_responsive.asp)の高い設計原則に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-129">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="1aac7-130">すべてのキーの構成はモバイルデバイスでアクセスできる必要があり、ビューがゆがんではないことが必要です。</span><span class="sxs-lookup"><span data-stu-id="1aac7-130">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="1aac7-131">タブがモバイルデバイスにロードされている場合、すべてのボタンとリンクは、finger ベースのナビゲーションを使用して簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-131">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="authentication"></a><span data-ttu-id="1aac7-132">認証</span><span class="sxs-lookup"><span data-stu-id="1aac7-132">Authentication</span></span>

<span data-ttu-id="1aac7-133">モバイルクライアントで認証を行うには、Teams JS SDK を少なくともバージョン1.4.1 にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-133">For authentication to work on mobile clients, you must upgrade you Teams JS SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth--intermittent-connections"></a><span data-ttu-id="1aac7-134">低帯域幅 & 断続的な接続</span><span class="sxs-lookup"><span data-stu-id="1aac7-134">Low bandwidth & intermittent connections</span></span>

<span data-ttu-id="1aac7-135">モバイルクライアントは、低帯域幅および断続的な接続で通常に機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-135">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="1aac7-136">アプリでは、ユーザーにコンテキストメッセージを提供することによって、すべてのタイムアウトを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-136">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="1aac7-137">また、長時間実行されているプロセスのユーザーにフィードバックを提供するために、ユーザーの進捗状況インジケーターを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-137">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

## <a name="design-considerations-for-mobile"></a><span data-ttu-id="1aac7-138">モバイルの設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="1aac7-138">Design considerations for mobile</span></span>

<span data-ttu-id="1aac7-139">弊社のモバイルプラットフォームを使用すると、アプリのコンテンツがメインの Teams ナビゲーションとは別にすべての画面を占有しているため、アプリをイマーシブ操作とすることができます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-139">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="1aac7-140">Microsoft Teams クライアントにシームレスに適合するイマーシブの機能を作成するには、以下のガイドラインに従ってください。</span><span class="sxs-lookup"><span data-stu-id="1aac7-140">To create an immersive experience that fits seamlessly within the Microsoft Teams client, follow the guidelines below.</span></span>

### <a name="layouts"></a><span data-ttu-id="1aac7-141">レイアウト</span><span class="sxs-lookup"><span data-stu-id="1aac7-141">Layouts</span></span>

<span data-ttu-id="1aac7-142">タブの正しいレイアウトを選択することは重要です。</span><span class="sxs-lookup"><span data-stu-id="1aac7-142">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="1aac7-143">表示する情報の種類を検討し、簡単に使用できるように整理されたレイアウトを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-143">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="1aac7-144">考えられるオプションには、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-144">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="1aac7-145">1つのキャンバス</span><span class="sxs-lookup"><span data-stu-id="1aac7-145">Single canvas</span></span>

<span data-ttu-id="1aac7-146">これは、作業が行われる大きな領域の1つです。</span><span class="sxs-lookup"><span data-stu-id="1aac7-146">This is one large area where work gets done.</span></span> <span data-ttu-id="1aac7-147">Wiki アプリは、このパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="1aac7-147">The Wiki app follows this pattern.</span></span> <span data-ttu-id="1aac7-148">コンテンツを小さなコンポーネントに分離しないアプリがある場合は、それに適しています。</span><span class="sxs-lookup"><span data-stu-id="1aac7-148">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

![単一キャンバスレイアウト](~/assets/images/mobile-single-canvas.png)

#### <a name="list"></a><span data-ttu-id="1aac7-150">リスト</span><span class="sxs-lookup"><span data-stu-id="1aac7-150">List</span></span>

<span data-ttu-id="1aac7-151">リストは大量のデータの並べ替えとフィルター処理を行うのに適しており、最も重要なものを最上位に保持するのに適しています。</span><span class="sxs-lookup"><span data-stu-id="1aac7-151">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="1aac7-152">並べ替え可能な列を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="1aac7-152">It is helpful to use sortable columns.</span></span> <span data-ttu-id="1aac7-153">アクションは、省略記号メニューの各リスト項目に追加できます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-153">Actions can be added to each list item under the ellipsis menu.</span></span>

![リストレイアウト](~/assets/images/mobile-list.png)

#### <a name="grid"></a><span data-ttu-id="1aac7-155">グリッド</span><span class="sxs-lookup"><span data-stu-id="1aac7-155">Grid</span></span>

<span data-ttu-id="1aac7-156">グリッドは、ビジュアルの高い要素を表示するのに便利です。</span><span class="sxs-lookup"><span data-stu-id="1aac7-156">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="1aac7-157">フィルターまたは検索コントロールを上部に含めることができます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-157">It helps to include a filter or search control at the top.</span></span>

![グリッドレイアウト](~/assets/images/mobile-grid.png)

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="1aac7-159">モバイルに bot があるタブ</span><span class="sxs-lookup"><span data-stu-id="1aac7-159">Tabs with bots on mobile</span></span>

<span data-ttu-id="1aac7-160">次に示すのは、2つの静的タブと bot を含む個人用アプリの例です。</span><span class="sxs-lookup"><span data-stu-id="1aac7-160">The below is an example personal app that contains two static tabs and a bot.</span></span>

![モバイルのタブとボット](~/assets/images/mobile-tab-with-bot.png)

### <a name="ui-components"></a><span data-ttu-id="1aac7-162">UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="1aac7-162">UI Components</span></span>

#### <a name="color-palettes"></a><span data-ttu-id="1aac7-163">カラー パレット</span><span class="sxs-lookup"><span data-stu-id="1aac7-163">Color palettes</span></span>

<span data-ttu-id="1aac7-164">背景、通知、テキスト、およびボタンに対して承認されたニュートラルパレットを使用すると、アプリが Teams での自宅をよりよく理解できるようになります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-164">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="1aac7-165">Teams mobile には2つの色のテーマ (軽いと濃) があるため、アプリが両方に適したものになるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1aac7-165">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

##### <a name="light-color"></a><span data-ttu-id="1aac7-166">明るい色</span><span class="sxs-lookup"><span data-stu-id="1aac7-166">Light color</span></span>

![ライトカラーパレット](~/assets/images/light-color.png)

##### <a name="dark-color"></a><span data-ttu-id="1aac7-168">暗い色</span><span class="sxs-lookup"><span data-stu-id="1aac7-168">Dark color</span></span>

![濃い色パレット](~/assets/images/dark-color.png)

#### <a name="buttons-and-controls"></a><span data-ttu-id="1aac7-170">ボタンとコントロール</span><span class="sxs-lookup"><span data-stu-id="1aac7-170">Buttons and controls</span></span>

<span data-ttu-id="1aac7-171">ボタンのスタイルを設定すると、どのような種類の動作が発生したかを伝えることができます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-171">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="1aac7-172">さまざまな強調レベルを表示するように書式設定されたさまざまなボタンを維持しています。</span><span class="sxs-lookup"><span data-stu-id="1aac7-172">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="1aac7-173">ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-173">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="1aac7-174">階層内のさまざまなレベルを通信するために、各カテゴリ内に主ボタンと副ボタンを設計しました。</span><span class="sxs-lookup"><span data-stu-id="1aac7-174">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

![リモコン](~/assets/images/buttons.png)

![選択コントロール](~/assets/images/selection-controls.png)

![chiclets および pills](~/assets/images/chiclets-and-pills.png)

#### <a name="typography"></a><span data-ttu-id="1aac7-178">文字体裁</span><span class="sxs-lookup"><span data-stu-id="1aac7-178">Typography</span></span>

<span data-ttu-id="1aac7-179">文字体裁はクリアで、意図的にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1aac7-179">Typography should be clear and purposeful.</span></span> <span data-ttu-id="1aac7-180">重要な情報を強調して、混乱を減らすために複数のフォントとサイズを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="1aac7-180">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="1aac7-181">ローカライズと読みやすくするために、文のケースを使用し、すべての cap の使用を回避することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1aac7-181">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![モバイル typograph](~/assets/images/mobile-typography.png)

#### <a name="fields-and-flyouts"></a><span data-ttu-id="1aac7-183">フィールドと Flyouts</span><span class="sxs-lookup"><span data-stu-id="1aac7-183">Fields and Flyouts</span></span>

<span data-ttu-id="1aac7-184">フィールドは、ユーザーがテキストを入力できる領域です。</span><span class="sxs-lookup"><span data-stu-id="1aac7-184">Fields are areas where users can input text.</span></span> <span data-ttu-id="1aac7-185">Flyouts はダイアログよりも軽量で、上部のウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="1aac7-185">Flyouts are more lightweight than dialogs, and appear from the top pane.</span></span>

##### <a name="list-controls"></a><span data-ttu-id="1aac7-186">コントロールを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="1aac7-186">List controls</span></span>

![モバイルリストコントロール](~/assets/images/mobile-list-controls.png)

##### <a name="field-controls"></a><span data-ttu-id="1aac7-188">フィールドコントロール</span><span class="sxs-lookup"><span data-stu-id="1aac7-188">Field controls</span></span>

![モバイルフィールドコントロール](~/assets/images/mobile-field-controls.png)
