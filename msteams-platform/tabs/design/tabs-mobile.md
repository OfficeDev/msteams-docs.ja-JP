---
title: モバイルのタブ
description: モバイルで機能するタブをデザインするためのガイドラインについて説明します。
ms.topic: conceptual
localization_priority: Normal
keywords: チーム設計ガイドライン 参照フレームワーク個人用アプリ モバイル タブ
ms.openlocfilehash: 853ab2c52edd1f4faedcc92e6f0e8d0821b580c7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566699"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="c4caf-104">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="c4caf-104">Tabs on mobile</span></span>

<span data-ttu-id="c4caf-105">モバイルチャンネル、チャット、個人用アプリTeamsタブを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="c4caf-105">You can include tabs in Teams mobile channels, chats, and personal apps.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="c4caf-106">個人用タブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="c4caf-106">Accessing personal tabs</span></span>

<span data-ttu-id="c4caf-107">アプリの引き出しにある個人用タブにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="c4caf-107">You can access personal tabs in the app drawer.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Teamsモバイル アプリの引き出しを示す図。" border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="c4caf-109">チャンネルタブへのアクセス</span><span class="sxs-lookup"><span data-stu-id="c4caf-109">Accessing channel tabs</span></span>

<span data-ttu-id="c4caf-110">チャンネルタブやグループタブにアクセスするには、チャンネルまたはチャットで追加したチャンネルまたはチャットの[ **その他** ]ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="c4caf-110">You can access channel and group tabs by selecting the **More** button in the channel or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Teamsモバイル タブを示す図。" border="false":::

## <a name="design-considerations"></a><span data-ttu-id="c4caf-112">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="c4caf-112">Design considerations</span></span>

<span data-ttu-id="c4caf-113">当社のモバイルプラットフォームでは、アプリがメインTeamsナビゲーションとは別に、すべての画面を占めるアプリコンテンツで没入型体験をすることができます。</span><span class="sxs-lookup"><span data-stu-id="c4caf-113">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="c4caf-114">Teamsに合った没入型エクスペリエンスを作成するには、次のガイドラインに従います。</span><span class="sxs-lookup"><span data-stu-id="c4caf-114">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="c4caf-115">レスポンシブ デザイン</span><span class="sxs-lookup"><span data-stu-id="c4caf-115">Responsive design</span></span>

<span data-ttu-id="c4caf-116">幅広い画面サイズのデバイスでタブを開くことができるため、 [レスポンシブデザイン](https://www.w3schools.com/html/html_responsive.asp) の原則に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4caf-116">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="c4caf-117">すべてのキーコンストラクトはモバイルデバイス上でアクセス可能であり、ビューは歪んではなりません。</span><span class="sxs-lookup"><span data-stu-id="c4caf-117">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="c4caf-118">タブがモバイル デバイスに読み込まれるときに、すべてのボタンとリンクに指ベースのナビゲーションを使用して簡単にアクセスできることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c4caf-118">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="c4caf-119">レイアウト</span><span class="sxs-lookup"><span data-stu-id="c4caf-119">Layouts</span></span>

<span data-ttu-id="c4caf-120">タブに適したレイアウトを選択することが重要です。</span><span class="sxs-lookup"><span data-stu-id="c4caf-120">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="c4caf-121">表示する情報の種類を考慮し、使いやすいレイアウトを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4caf-121">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="c4caf-122">いくつかの潜在的なオプションは以下に概説されています。</span><span class="sxs-lookup"><span data-stu-id="c4caf-122">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="c4caf-123">シングルキャンバス</span><span class="sxs-lookup"><span data-stu-id="c4caf-123">Single canvas</span></span>

<span data-ttu-id="c4caf-124">これは作業が行われる1つの広い領域です。</span><span class="sxs-lookup"><span data-stu-id="c4caf-124">This is one large area where work gets done.</span></span> <span data-ttu-id="c4caf-125">Teams Wiki アプリは、このパターンに従います。</span><span class="sxs-lookup"><span data-stu-id="c4caf-125">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="c4caf-126">コンテンツを小さなコンポーネントに分割しないアプリがある場合は、この機能が適しています。</span><span class="sxs-lookup"><span data-stu-id="c4caf-126">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="モバイルシングルキャンバスタブTeamsを示す図。" border="false":::

#### <a name="list"></a><span data-ttu-id="c4caf-128">List</span><span class="sxs-lookup"><span data-stu-id="c4caf-128">List</span></span>

<span data-ttu-id="c4caf-129">リストは大量のデータを並べ替えたりフィルタリングする場合に最適であり、最も重要なデータを一番上に保持することに最適です。</span><span class="sxs-lookup"><span data-stu-id="c4caf-129">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="c4caf-130">並べ替え可能な列を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="c4caf-130">It is helpful to use sortable columns.</span></span> <span data-ttu-id="c4caf-131">アクションは、省略記号メニューの各リスト項目に追加できます。</span><span class="sxs-lookup"><span data-stu-id="c4caf-131">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Teamsモバイル リスト タブを示す図。" border="false":::

#### <a name="grid"></a><span data-ttu-id="c4caf-133">グリッド</span><span class="sxs-lookup"><span data-stu-id="c4caf-133">Grid</span></span>

<span data-ttu-id="c4caf-134">グリッドは、視覚的に優れた要素を表示する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="c4caf-134">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="c4caf-135">これは、上部にフィルターまたは検索コントロールを含めるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c4caf-135">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="グリッド レイアウトを使用したTeamsモバイル タブを示す図。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="c4caf-137">モバイルでボットを持つタブ</span><span class="sxs-lookup"><span data-stu-id="c4caf-137">Tabs with bots on mobile</span></span>

<span data-ttu-id="c4caf-138">次の例は、タブとボットを持つ個人用アプリです。</span><span class="sxs-lookup"><span data-stu-id="c4caf-138">The following example is a personal app that has tabs and a bot:</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="タブとボットを備えたモバイル Teams アプリの様子を示す図。" border="false":::

## <a name="ui-components"></a><span data-ttu-id="c4caf-140">UI コンポーネント</span><span class="sxs-lookup"><span data-stu-id="c4caf-140">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="c4caf-141">カラー パレット</span><span class="sxs-lookup"><span data-stu-id="c4caf-141">Color palettes</span></span>

<span data-ttu-id="c4caf-142">バックグラウンド、通知、テキスト、ボタンに対して承認されたニュートラルパレットを使用すると、アプリがTeamsにくつろぐのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c4caf-142">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="c4caf-143">モバイルTeams 2 つの色テーマ (明るいテーマと暗色テーマ) があるため、アプリが両方とも見栄えが良いことを確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c4caf-143">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="c4caf-144">明るい色</span><span class="sxs-lookup"><span data-stu-id="c4caf-144">Light color</span></span>

![淡色パレット](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="c4caf-146">暗い色</span><span class="sxs-lookup"><span data-stu-id="c4caf-146">Dark color</span></span>

![暗色パレット](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="c4caf-148">ボタンとコントロール</span><span class="sxs-lookup"><span data-stu-id="c4caf-148">Buttons and controls</span></span>

<span data-ttu-id="c4caf-149">ボタンのスタイル設定は、どのようなアクションがトリガーされるのかを伝えるのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c4caf-149">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="c4caf-150">私たちは、強調の異なるレベルを示すようにフォーマットされているボタンの広い範囲を維持します。</span><span class="sxs-lookup"><span data-stu-id="c4caf-150">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="c4caf-151">ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="c4caf-151">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="c4caf-152">階層内のさまざまなレベルを伝達するために、各カテゴリ内のプライマリ ボタンとセカンダリ ボタンを設計しました。</span><span class="sxs-lookup"><span data-stu-id="c4caf-152">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="c4caf-153">ボタン</span><span class="sxs-lookup"><span data-stu-id="c4caf-153">Buttons</span></span>

<span data-ttu-id="c4caf-154">プライマリ ボタンとセカンダリ ボタン。</span><span class="sxs-lookup"><span data-stu-id="c4caf-154">Primary and secondary buttons.</span></span>

![ボタンイメージ](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="c4caf-156">選択コントロール</span><span class="sxs-lookup"><span data-stu-id="c4caf-156">Selection controls</span></span>

<span data-ttu-id="c4caf-157">ラジオ ボタン、チェック ボックス、およびトグル。</span><span class="sxs-lookup"><span data-stu-id="c4caf-157">Radio buttons, checkboxes, and toggles.</span></span>

![選択コントロール](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="c4caf-159">チクレットと丸薬</span><span class="sxs-lookup"><span data-stu-id="c4caf-159">Chiclets and pills</span></span>

![チクレットと丸薬](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="c4caf-161">文字体裁</span><span class="sxs-lookup"><span data-stu-id="c4caf-161">Typography</span></span>

<span data-ttu-id="c4caf-162">タイポグラフィは明確かつ意図的であるべきです。</span><span class="sxs-lookup"><span data-stu-id="c4caf-162">Typography should be clear and purposeful.</span></span> <span data-ttu-id="c4caf-163">重要な情報を強調し、複数のフォントやサイズを使用して混乱を避けてください。</span><span class="sxs-lookup"><span data-stu-id="c4caf-163">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="c4caf-164">文章の大文字小文字を使用し、ローカライズと読みやすさを目的としてすべてのキャップを使用しないようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c4caf-164">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![モバイルタイポグラフ](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="c4caf-166">フィールドとポップアップ</span><span class="sxs-lookup"><span data-stu-id="c4caf-166">Fields and flyouts</span></span>

<span data-ttu-id="c4caf-167">フィールドは、ユーザーがテキストを入力できる領域です。</span><span class="sxs-lookup"><span data-stu-id="c4caf-167">Fields are areas where users can input text.</span></span> <span data-ttu-id="c4caf-168">ポップアップはダイアログよりも軽量で、上部のペインから表示されます。</span><span class="sxs-lookup"><span data-stu-id="c4caf-168">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="c4caf-169">コントロールを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="c4caf-169">List controls</span></span>

![モバイル リスト コントロール](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="c4caf-171">フィールド コントロール</span><span class="sxs-lookup"><span data-stu-id="c4caf-171">Field controls</span></span>

![モバイル フィールド コントロール](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="c4caf-173">開発者の考慮事項</span><span class="sxs-lookup"><span data-stu-id="c4caf-173">Developer considerations</span></span>

<span data-ttu-id="c4caf-174">タブを含むアプリを構築する場合は、Android と iOS の両方のクライアントでタブがどのように機能するかを検討 (およびテスト) Microsoft Teams必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4caf-174">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="c4caf-175">以下のセクションでは、考慮する必要があるいくつかの主要なシナリオについて説明します。</span><span class="sxs-lookup"><span data-stu-id="c4caf-175">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="authentication"></a><span data-ttu-id="c4caf-176">認証</span><span class="sxs-lookup"><span data-stu-id="c4caf-176">Authentication</span></span>

<span data-ttu-id="c4caf-177">モバイル クライアントで認証を実行するには、JavaScript SDK Teams少なくともバージョン 1.4.1 にアップグレードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4caf-177">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="c4caf-178">低帯域幅と断続的な接続</span><span class="sxs-lookup"><span data-stu-id="c4caf-178">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="c4caf-179">モバイル クライアントは、帯域幅が低く、断続的な接続で定期的に機能する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4caf-179">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="c4caf-180">アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4caf-180">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="c4caf-181">また、実行時間の長いプロセスについてユーザーにフィードバックを提供するために、ユーザーの進行状況インジケータを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4caf-181">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="c4caf-182">モバイルでタブが有効になるのは、承認チームの入力に基づいて、アプリケーションが許可リストに追加された後のみです。</span><span class="sxs-lookup"><span data-stu-id="c4caf-182">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="c4caf-183">モバイルの応答性を確認するには、teamsubm@microsoft.com に連絡します。</span><span class="sxs-lookup"><span data-stu-id="c4caf-183">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="c4caf-184">モバイル クライアントでのテスト</span><span class="sxs-lookup"><span data-stu-id="c4caf-184">Testing on mobile clients</span></span>

<span data-ttu-id="c4caf-185">さまざまなサイズと品質のモバイル デバイスでタブが正しく機能することを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4caf-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="c4caf-186">Android デバイスの場合、実行中に [DevTools を](~/tabs/how-to/developer-tools.md) 使用してタブをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="c4caf-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="c4caf-187">タブレットを含む高パフォーマンスと低パフォーマンスの両方のデバイスでテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c4caf-187">We recommend that you test on both high- and low-performance devices, including a tablet.</span></span>

### <a name="distribution"></a><span data-ttu-id="c4caf-188">配布</span><span class="sxs-lookup"><span data-stu-id="c4caf-188">Distribution</span></span>

<span data-ttu-id="c4caf-189">Teamsストアに登録されているアプリは、モバイルクライアントでモバイルが正常に機能するために承認Teams必要があります。</span><span class="sxs-lookup"><span data-stu-id="c4caf-189">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="c4caf-190">タブの可用性と動作は、アプリが承認されているかどうかによって異なります。</span><span class="sxs-lookup"><span data-stu-id="c4caf-190">Tab availability and behavior depends on whether your app is approved.</span></span>

#### <a name="apps-on-teams-store-approved-for-mobile"></a><span data-ttu-id="c4caf-191">モバイル向けに承認Teamsストア上のアプリ</span><span class="sxs-lookup"><span data-stu-id="c4caf-191">Apps on Teams store approved for mobile</span></span>

<span data-ttu-id="c4caf-192">次の表は、アプリがTeams ストアに表示され、モバイルでの使用が承認されたときのタブの可用性と動作を示しています。</span><span class="sxs-lookup"><span data-stu-id="c4caf-192">The following table describes tab availability and behavior when the app is listed on the Teams store and approved for mobile use:</span></span>

|<span data-ttu-id="c4caf-193">機能</span><span class="sxs-lookup"><span data-stu-id="c4caf-193">Capability</span></span>   |<span data-ttu-id="c4caf-194">モバイルの可用性?</span><span class="sxs-lookup"><span data-stu-id="c4caf-194">Mobile availability?</span></span>   |<span data-ttu-id="c4caf-195">モバイル動作</span><span class="sxs-lookup"><span data-stu-id="c4caf-195">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="c4caf-196">チャネル</span><span class="sxs-lookup"><span data-stu-id="c4caf-196">Channel</span></span> <br /> <span data-ttu-id="c4caf-197">およびグループ タブ</span><span class="sxs-lookup"><span data-stu-id="c4caf-197">and group tab</span></span>|<span data-ttu-id="c4caf-198">はい</span><span class="sxs-lookup"><span data-stu-id="c4caf-198">Yes</span></span>|<span data-ttu-id="c4caf-199">タブは、アプリの構成を使用してTeamsモバイルクライアントで開きます `contentUrl` 。</span><span class="sxs-lookup"><span data-stu-id="c4caf-199">Tab opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>|
|<span data-ttu-id="c4caf-200">パーソナルアプリ</span><span class="sxs-lookup"><span data-stu-id="c4caf-200">Personal app</span></span>|<span data-ttu-id="c4caf-201">はい</span><span class="sxs-lookup"><span data-stu-id="c4caf-201">Yes</span></span>|<span data-ttu-id="c4caf-202">[個人用アプリ] タブの各タブは、それぞれの構成を使用してTeamsモバイル クライアントに表示されます `contentUrl` 。</span><span class="sxs-lookup"><span data-stu-id="c4caf-202">Each tab in the personal app tab opens in the Teams mobile client using its respective `contentUrl` configuration.</span></span>|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a><span data-ttu-id="c4caf-203">Teamsストアのアプリがモバイルで承認されていません</span><span class="sxs-lookup"><span data-stu-id="c4caf-203">Apps on Teams store not approved for mobile</span></span>

<span data-ttu-id="c4caf-204">次の表は、アプリがTeams ストアに表示されているが、モバイルでの使用が承認されていない場合のタブの可用性と動作を示しています。</span><span class="sxs-lookup"><span data-stu-id="c4caf-204">The following table describes tab availability and behavior when the app is listed on the Teams store but not approved for mobile use:</span></span>

| <span data-ttu-id="c4caf-205">機能</span><span class="sxs-lookup"><span data-stu-id="c4caf-205">Capability</span></span> | <span data-ttu-id="c4caf-206">モバイルの可用性?</span><span class="sxs-lookup"><span data-stu-id="c4caf-206">Mobile availability?</span></span> | <span data-ttu-id="c4caf-207">モバイル動作</span><span class="sxs-lookup"><span data-stu-id="c4caf-207">Mobile behavior</span></span> |
|----------|-----------|------------|
|<span data-ttu-id="c4caf-208">[チャンネルとグループ] タブ</span><span class="sxs-lookup"><span data-stu-id="c4caf-208">Channel and group tab</span></span>|<span data-ttu-id="c4caf-209">はい</span><span class="sxs-lookup"><span data-stu-id="c4caf-209">Yes</span></span>|<span data-ttu-id="c4caf-210">アプリの構成を使用するモバイル クライアントの Teams代わりに、デバイスの既定のブラウザー `websiteUrl` でタブが開きます `setSettings()` [](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="c4caf-210">Tab opens in the device's default browser instead of the Teams mobile client using your app's `websiteUrl` configuration, which also must be included in your source code's `setSettings()` [function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true).</span></span> <span data-ttu-id="c4caf-211">ただし、ユーザーは、アプリの横にある **[その他]** を選択し、アプリの構成をトリガーする [**開く**] を選択することで、Teamsモバイル クライアントのタブを表示できます `contentUrl` 。</span><span class="sxs-lookup"><span data-stu-id="c4caf-211">However, users can still view the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>|
|<span data-ttu-id="c4caf-212">パーソナルアプリ</span><span class="sxs-lookup"><span data-stu-id="c4caf-212">Personal app</span></span>|<span data-ttu-id="c4caf-213">なし</span><span class="sxs-lookup"><span data-stu-id="c4caf-213">No</span></span>|<span data-ttu-id="c4caf-214">該当なし</span><span class="sxs-lookup"><span data-stu-id="c4caf-214">Not applicable</span></span>|

#### <a name="apps-not-on-teams-store"></a><span data-ttu-id="c4caf-215">ストアにないアプリTeams</span><span class="sxs-lookup"><span data-stu-id="c4caf-215">Apps not on Teams store</span></span>

<span data-ttu-id="c4caf-216">アプリをサイドローディングしたり、組織のアプリカタログに公開したりする場合、タブの動作は、モバイル向けに Microsoft が承認したストアアプリTeamsと同じになります。</span><span class="sxs-lookup"><span data-stu-id="c4caf-216">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>
