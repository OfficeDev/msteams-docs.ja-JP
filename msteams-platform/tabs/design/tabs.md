---
title: タブの設計ガイドライン
description: コンテンツとコラボレーションのタブを作成するためのガイドラインについて説明します。
keywords: teams 設計ガイドラインリファレンスフレームワークタブ [構成チャネル] タブ [静的] タブ [シンプル] [デザインチーム] タブ
ms.openlocfilehash: 2d4e809e3ac11a5742113bf65125848a922c0207
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576863"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="be3af-104">すべてのタブを使用したコンテンツと会話</span><span class="sxs-lookup"><span data-stu-id="be3af-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="be3af-105">**モバイルクライアントのタブ**</span><span class="sxs-lookup"><span data-stu-id="be3af-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="be3af-106">タブを作成するときに、 [[モバイル] のタブのガイダンス](./tabs-mobile.md) に従ってください。</span><span class="sxs-lookup"><span data-stu-id="be3af-106">Follow the [guidance for tabs on mobile](./tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="be3af-107">タブで認証を使用している場合は、Teams の JavaScript SDK をバージョン1.4.1 以降にアップグレードする必要があります。認証は失敗します。</span><span class="sxs-lookup"><span data-stu-id="be3af-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="be3af-108">**モバイルのチャネル/グループ (構成可能) のタブ:**</span><span class="sxs-lookup"><span data-stu-id="be3af-108">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="be3af-109">モバイルクライアントは、の値を持つ構成可能なタブのみを表示 `websiteUrl` します。</span><span class="sxs-lookup"><span data-stu-id="be3af-109">Mobile clients only show configurable tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="be3af-110">チームのモバイルクライアントにタブを表示する場合は、の値を設定する必要があり `websiteUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="be3af-110">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="be3af-111">モバイルでの既定のオープン動作は、を使用してブラウザーの外部で開くことが `websiteUrl` できます。</span><span class="sxs-lookup"><span data-stu-id="be3af-111">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="be3af-112">公開アプリストアに発行されたアプリの場合、[チャネル] タブを既定でオンにするには、 [[モバイル] のタブのガイダンス](~/tabs/design/tabs-mobile.md)に従って、サポート担当者に連絡して、ホワイトリストを要求します。</span><span class="sxs-lookup"><span data-stu-id="be3af-112">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="be3af-113">タブは、チームの有機ワークフロー内でコンテンツを共有し、会話を保持し、サードパーティのサービスをホストするために使用できるキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="be3af-113">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="be3af-114">Microsoft Teams でタブを作成すると、主要な会話から簡単にアクセスできるように、web アプリのフロントおよび中央が配置されます。</span><span class="sxs-lookup"><span data-stu-id="be3af-114">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="be3af-115">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="be3af-115">Guidelines</span></span>

<span data-ttu-id="be3af-116">適切なタブには、次の特性が表示されます。</span><span class="sxs-lookup"><span data-stu-id="be3af-116">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="be3af-117">フォーカスのある機能</span><span class="sxs-lookup"><span data-stu-id="be3af-117">Focused functionality</span></span>

<span data-ttu-id="be3af-118">タブは、特定のニーズに対応するように構築されている場合に最適に機能します。</span><span class="sxs-lookup"><span data-stu-id="be3af-118">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="be3af-119">タブがあるチャネルに関連する、少数のタスクまたはデータのサブセットにフォーカスします。</span><span class="sxs-lookup"><span data-stu-id="be3af-119">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="be3af-120">クロムの削減</span><span class="sxs-lookup"><span data-stu-id="be3af-120">Reduced chrome</span></span>

<span data-ttu-id="be3af-121">タブ内に複数のパネルを作成したり、ナビゲーションの階層を増やしたり、同一のタブ内で垂直方向と水平方向の両方のスクロール操作をユーザーに求めたりしないようにします。つまり、タブ内に他のタブがあるような状態にしないようにします。</span><span class="sxs-lookup"><span data-stu-id="be3af-121">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

### <a name="integration"></a><span data-ttu-id="be3af-122">統合</span><span class="sxs-lookup"><span data-stu-id="be3af-122">Integration</span></span>

<span data-ttu-id="be3af-123">会話に [アダプティブカード](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) を投稿することで、ユーザーにタブアクティビティについて通知する方法を検索します。</span><span class="sxs-lookup"><span data-stu-id="be3af-123">Find ways to notify users about tab activity by posting [adaptive cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) to a conversation.</span></span>

### <a name="conversational"></a><span data-ttu-id="be3af-124">会話性</span><span class="sxs-lookup"><span data-stu-id="be3af-124">Conversational</span></span>

<span data-ttu-id="be3af-125">タブを中心に会話を円滑にする方法を見つけます。これにより、会話センターがコンテンツ、データ、またはプロセスに対して実行されることが保証されます。</span><span class="sxs-lookup"><span data-stu-id="be3af-125">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="be3af-126">アクセスの効率化</span><span class="sxs-lookup"><span data-stu-id="be3af-126">Streamlined access</span></span>

<span data-ttu-id="be3af-127">適切なときに、適切なユーザーにアクセスを許可していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="be3af-127">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="be3af-128">サインインプロセスを簡単にすることで、投稿とコラボレーションへの障壁をなくすことができます。</span><span class="sxs-lookup"><span data-stu-id="be3af-128">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="responsiveness-to-window-sizing"></a><span data-ttu-id="be3af-129">ウィンドウのサイズ変更への応答</span><span class="sxs-lookup"><span data-stu-id="be3af-129">Responsiveness to window sizing</span></span>

<span data-ttu-id="be3af-130">Teams は、ウィンドウのサイズが720ピクセルの場合に使用できるので、タブを小さなウィンドウで使用できることを確認することは、非常に高解像度の場合と同様に重要です。</span><span class="sxs-lookup"><span data-stu-id="be3af-130">Teams can be used in window sizes as small as 720px, so making sure that a tab is usable in a small window is just as important as usability at very high resolutions.</span></span>

### <a name="flat-navigation"></a><span data-ttu-id="be3af-131">フラットナビゲーション</span><span class="sxs-lookup"><span data-stu-id="be3af-131">Flat navigation</span></span>

<span data-ttu-id="be3af-132">開発者は、ポータル全体をタブに追加しないようにしてください。ナビゲーションを比較的フラットに維持すると、より単純な会話モデルが維持されます。</span><span class="sxs-lookup"><span data-stu-id="be3af-132">We ask developers not to add their entire portal to a tab. Keeping the navigation relatively flat helps maintain a simpler conversational model.</span></span> <span data-ttu-id="be3af-133">言い換えると、会話は、トリアージされた作業項目、または仕様のような1つの事柄の一覧についてのものです。</span><span class="sxs-lookup"><span data-stu-id="be3af-133">In other words, the conversation is about a list of things, such as triaged work items, or a single thing, like a spec.</span></span>

<span data-ttu-id="be3af-134">スレッド化された会話内に深いナビゲーション階層を使用して、固有のナビゲーションの課題があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-134">There are inherent navigational challenges with deep navigation hierarchy, within threaded conversations.</span></span> <span data-ttu-id="be3af-135">ユーザーにとって最適な操作を行うには、タブナビゲーションを最小限に抑え、次のように設計する必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-135">For the best user experience, your tab navigation should be kept to a minimum and be designed as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="be3af-136">**個別の作業項目またはエンティティなどのタスクモジュールを開き** ます。</span><span class="sxs-lookup"><span data-stu-id="be3af-136">**Opens a task module such as an individual work item or entity**.</span></span> <span data-ttu-id="be3af-137">これにより、チャットが完全には不可能になります。これは、サブエンティティや編集機能ではなく、特にタブについてのチャットを維持するための最適なオプションです。</span><span class="sxs-lookup"><span data-stu-id="be3af-137">This precludes chat entirely and is the best option to keep chat specifically about the tab and not the sub-entities or editing experiences.</span></span>
>* <span data-ttu-id="be3af-138">**Iframe で擬似ダイアログを開き** ます。</span><span class="sxs-lookup"><span data-stu-id="be3af-138">**Opens a pseudo dialog in an iframe**.</span></span> <span data-ttu-id="be3af-139">スクリーン背景を使用する場合は、暗色ではなく明るい色を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="be3af-139">If used with a screened background we recommend using the lighter color rather than the dark.</span></span> <span data-ttu-id="be3af-140">`app-gray-10 at 30%`透過性は適切に機能します。</span><span class="sxs-lookup"><span data-stu-id="be3af-140">The `app-gray-10 at 30%` transparency works well.</span></span>
>* <span data-ttu-id="be3af-141">**ブラウザーページを開き** ます。</span><span class="sxs-lookup"><span data-stu-id="be3af-141">**Opens a browser page**.</span></span>

### <a name="personality"></a><span data-ttu-id="be3af-142">プラン</span><span class="sxs-lookup"><span data-stu-id="be3af-142">Personality</span></span>

<span data-ttu-id="be3af-143">タブキャンバスは、自分の環境をブランド化する絶好の機会を提供します。</span><span class="sxs-lookup"><span data-stu-id="be3af-143">Your tab canvas presents a great opportunity to brand your experience.</span></span> <span data-ttu-id="be3af-144">ロゴは、ユーザーとの間で id と接続の重要な部分です。そのため、必ず含めてください。</span><span class="sxs-lookup"><span data-stu-id="be3af-144">Your logo is an important part of your identity and connection with your users., so be sure to include it:</span></span>

> [!div class="checklist"]
>
>* <span data-ttu-id="be3af-145">ロゴを左または右または下の端に配置する</span><span class="sxs-lookup"><span data-stu-id="be3af-145">Place your logo in the left or right corner or along the bottom edge</span></span>
> * <span data-ttu-id="be3af-146">ロゴのサイズを小さくして、邪魔されないようにする</span><span class="sxs-lookup"><span data-stu-id="be3af-146">Keep your logo small and unobtrusive</span></span>

<span data-ttu-id="be3af-147">独自の色とレイアウトを組み込むことは、個性を伝える上でも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="be3af-147">Incorporating your own colors and layouts twill also aid in communicating personality.</span></span>

> [!TIP]
> <span data-ttu-id="be3af-148">Visual スタイルを使用して、サービスが Teams の一部として感じられるようにしてください。</span><span class="sxs-lookup"><span data-stu-id="be3af-148">Please work with our visual style so your service feels like a part of Teams.</span></span> <span data-ttu-id="be3af-149">[Teams の色](../../concepts/design/components/color.md)などの例を *参照してください*。</span><span class="sxs-lookup"><span data-stu-id="be3af-149">*See*, for example [Teams Colors](../../concepts/design/components/color.md)</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="be3af-150">タブレイアウト</span><span class="sxs-lookup"><span data-stu-id="be3af-150">Tab layouts</span></span>

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="be3af-151">タブの種類</span><span class="sxs-lookup"><span data-stu-id="be3af-151">Types of tabs</span></span>

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="be3af-152">構成ページの高さ</span><span class="sxs-lookup"><span data-stu-id="be3af-152">Configuration page height</span></span>

>[!IMPORTANT]
><span data-ttu-id="be3af-153">2018年9月に、[タブの [構成] ページ](~/tabs/how-to/create-tab-pages/configuration-page.md) の高さが変更されましたが、幅は変更されませんでした。</span><span class="sxs-lookup"><span data-stu-id="be3af-153">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="be3af-154">アプリが古いサイズを対象として設計されている場合は、タブの構成ページに大きな縦方向の空白があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-154">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="be3af-155">この変更によって除外された従来のストアアプリは、新しいディメンションに対応するために、更新後に Microsoft に連絡する必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-155">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="be3af-156">[タブの構成] ページのサイズ:</span><span class="sxs-lookup"><span data-stu-id="be3af-156">The dimensions of the tab configuration page:</span></span>


<img width="450px" title="構成タブのサイズ" src="~/assets/images/tabs/config-dialog-Contoso2.png" alt="sizes for config tabs" />


### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="be3af-158">タブ構成ページ形式に関するガイドライン</span><span class="sxs-lookup"><span data-stu-id="be3af-158">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="be3af-159">固定高高さのグラフィック要素で、タブの構成ページのコンテンツ領域の最小の高さを基準にします。</span><span class="sxs-lookup"><span data-stu-id="be3af-159">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="be3af-160">を使用して、使用可能な垂直方向の間隔 ([構成] ページのコンテンツ領域の高さ) を計算し `window.innerHeight` ます。</span><span class="sxs-lookup"><span data-stu-id="be3af-160">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="be3af-161">これは、構成ページが存在するのサイズを返します。これは、 `<iframe>` 今後のリリースで変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-161">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="be3af-162">この値を使用すると、コンテンツは今後の変更に合わせて自動的に調整されます。</span><span class="sxs-lookup"><span data-stu-id="be3af-162">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="be3af-163">可変長要素に垂直方向のスペースを割り当て、固定された高さの要素に対して必要なものを減算します。</span><span class="sxs-lookup"><span data-stu-id="be3af-163">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="be3af-164">*ログイン* 状態では、コンテンツを上下に中央揃えで配置します。</span><span class="sxs-lookup"><span data-stu-id="be3af-164">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="be3af-165">背景画像が必要な場合は、新しい画像、領域に合わせてサイズを変更する (推奨) か、同じ画像を保持して次のいずれかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="be3af-165">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="be3af-166">左上隅に合わせて配置します。</span><span class="sxs-lookup"><span data-stu-id="be3af-166">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="be3af-167">イメージのサイズを調整します。</span><span class="sxs-lookup"><span data-stu-id="be3af-167">scaling the image to fit.</span></span>

<span data-ttu-id="be3af-168">適切なサイズに設定すると、タブの構成ページは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="be3af-168">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title="[新しい構成] タブ" src="~/assets/images/tabs/config-dialog-Contoso.png" alt="new config tab"/>

## <a name="best-practices"></a><span data-ttu-id="be3af-170">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="be3af-170">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="be3af-171">常に既定の状態を含める</span><span class="sxs-lookup"><span data-stu-id="be3af-171">Always include a default state</span></span>

<span data-ttu-id="be3af-172">タブを構成できる場合でも、タブを簡単に設定できるように、既定の状態を含めます。</span><span class="sxs-lookup"><span data-stu-id="be3af-172">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="be3af-173">ディープリンク</span><span class="sxs-lookup"><span data-stu-id="be3af-173">Deep linking</span></span>

<span data-ttu-id="be3af-174">可能な限り、カードやボットは、ホストされたタブで豊富なデータにリンクする必要があります。たとえば、カードにバグデータの要約が表示されている場合でも、それをクリックすると、バグ全体がタブに表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="be3af-174">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="be3af-175">規約</span><span class="sxs-lookup"><span data-stu-id="be3af-175">Naming</span></span>

<span data-ttu-id="be3af-176">多くの場合、アプリの名前を使用すると、便利なタブ名が作成されます。</span><span class="sxs-lookup"><span data-stu-id="be3af-176">In many cases, the name of your app will make a great tab name.</span></span> <span data-ttu-id="be3af-177">ただし、タブは、提供される機能に従って名前を付けることも検討してください。</span><span class="sxs-lookup"><span data-stu-id="be3af-177">But, also consider naming your tabs according to the functionality they provide.</span></span>

### <a name="multi-window"></a><span data-ttu-id="be3af-178">複数ウィンドウ</span><span class="sxs-lookup"><span data-stu-id="be3af-178">Multi-window</span></span>

<span data-ttu-id="be3af-179">複雑な編集機能があるチャネルタブでは、タブではなく複数のウィンドウでエディタービューを開く必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-179">Channel tabs that have complex editing capabilities must open the editor view in multi-window rather than a tab.</span></span>

### <a name="no-horizontal-scrolling"></a><span data-ttu-id="be3af-180">水平方向のスクロールなし</span><span class="sxs-lookup"><span data-stu-id="be3af-180">No horizontal scrolling</span></span>

<span data-ttu-id="be3af-181">Tab キーは水平スクロールできません。</span><span class="sxs-lookup"><span data-stu-id="be3af-181">Tab should not have horizontal scrolling.</span></span>

### <a name="easy-navigation"></a><span data-ttu-id="be3af-182">簡単なナビゲーション</span><span class="sxs-lookup"><span data-stu-id="be3af-182">Easy navigation</span></span>

<span data-ttu-id="be3af-183">タブアプリ内のナビゲーションは、簡単に実行できるようにする必要があります。または、必要/該当するページは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="be3af-183">Navigation inside a tab app must be easy to follow i.e. pages have the following where necessary/applicable:</span></span>
* <span data-ttu-id="be3af-184">戻るボタン</span><span class="sxs-lookup"><span data-stu-id="be3af-184">Back buttons</span></span>
* <span data-ttu-id="be3af-185">ページヘッダー</span><span class="sxs-lookup"><span data-stu-id="be3af-185">Page headers</span></span>
* <span data-ttu-id="be3af-186">クラム</span><span class="sxs-lookup"><span data-stu-id="be3af-186">Breadcrumbs</span></span>
* <span data-ttu-id="be3af-187">ハンバーガーメニュー</span><span class="sxs-lookup"><span data-stu-id="be3af-187">Hamburger menus</span></span>

### <a name="undo-last-action"></a><span data-ttu-id="be3af-188">直前の操作を元に戻す</span><span class="sxs-lookup"><span data-stu-id="be3af-188">Undo last action</span></span>

<span data-ttu-id="be3af-189">ユーザーは、アプリの最後の操作を元に戻すことができる必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-189">User must be able to undo their last action in the app.</span></span>

### <a name="share-content"></a><span data-ttu-id="be3af-190">コンテンツを共有する</span><span class="sxs-lookup"><span data-stu-id="be3af-190">Share content</span></span>

<span data-ttu-id="be3af-191">個人用アプリを使用すると、ユーザーが個人のアプリの作業環境から他のチームメンバーとコンテンツを共有できるようになります。</span><span class="sxs-lookup"><span data-stu-id="be3af-191">Personal apps should enable users to share content from a personal app experience with other team members.</span></span> <span data-ttu-id="be3af-192">[チャネル] タブでは、メインチームのナビゲーションを補完するナビゲーションを提供する必要があります (左側のレールのナビゲーションバーなど)。</span><span class="sxs-lookup"><span data-stu-id="be3af-192">Channel tab must provide navigation that complements the main Teams navigation, rather than conflicting with it (such as left rail nav-bars).</span></span>

### <a name="single-view"></a><span data-ttu-id="be3af-193">単一ビュー</span><span class="sxs-lookup"><span data-stu-id="be3af-193">Single view</span></span>

<span data-ttu-id="be3af-194">個人用アプリは、チームまたはグループのチャットを対象としたアプリのインスタンスのコンテンツを1つのビューに表示する必要があります。たとえば、Trello ユーザーは、個人のアプリでチームレベルで参加した Trello ボードのすべてのインスタンスを表示できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-194">Personal apps should present content from team or group chat scoped instances of that app in a single view, e.g., a Trello user should be able to see all instances of Trello boards they participate in at a team level in their personal app.</span></span>

### <a name="no-app-bar"></a><span data-ttu-id="be3af-195">アプリバーなし</span><span class="sxs-lookup"><span data-stu-id="be3af-195">No app bar</span></span>

<span data-ttu-id="be3af-196">タブは、メインの Teams ナビゲーションと競合するアイコンがあるアプリバーを左側のレールに表示しません。</span><span class="sxs-lookup"><span data-stu-id="be3af-196">Tabs should not provide an app bar with icons in the left rail that conflicts with the main Teams navigation.</span></span>

### <a name="navigation"></a><span data-ttu-id="be3af-197">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="be3af-197">Navigation</span></span>

<span data-ttu-id="be3af-198">タブには、アプリ内で3レベルを超えるナビゲーションを含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="be3af-198">Tabs should not have more than 3 levels of navigation within the app.</span></span>

### <a name="l2l3-view"></a><span data-ttu-id="be3af-199">L2/L3 ビュー</span><span class="sxs-lookup"><span data-stu-id="be3af-199">L2/L3 view</span></span>

<span data-ttu-id="be3af-200">タブ内のセカンダリページと3番目のページは、階層リンクを介して移動するメインタブ領域の L2/L3 ビューで開く必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-200">Secondary and tertiary pages in a tab should be opened in an L2/L3 view in the main tab area that is navigated via the breadcrumb.</span></span>

### <a name="no-link-to-external-browser"></a><span data-ttu-id="be3af-201">外部ブラウザーへのリンクはありません</span><span class="sxs-lookup"><span data-stu-id="be3af-201">No link to external browser</span></span>

<span data-ttu-id="be3af-202">タブ内のリンクターゲットは、外部ブラウザーにリンクするのではなく、Teams 内に含まれる div 要素にリンクする必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-202">Link targets in tabs should not link to an external browser but should link to div elements contained within Teams.</span></span> <span data-ttu-id="be3af-203">たとえば、タスクモジュール、タブなどに含まれます。</span><span class="sxs-lookup"><span data-stu-id="be3af-203">For example, inside task Modules, tabs, etc.</span></span>

## <a name="notifications-for-tabs"></a><span data-ttu-id="be3af-204">タブの通知</span><span class="sxs-lookup"><span data-stu-id="be3af-204">Notifications for tabs</span></span>

<span data-ttu-id="be3af-205">タブのコンテンツの変更については、次の2つのモードの通知があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-205">There are two modes of notification for tab content changes:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="be3af-206">**アプリ API を使用して、ユーザーに変更を通知** します。</span><span class="sxs-lookup"><span data-stu-id="be3af-206">**Use the app API to notify users of changes**.</span></span> <span data-ttu-id="be3af-207">このメッセージは、ユーザーのアクティビティフィードに表示され、タブに深くリンクします。「[Microsoft Teams のコンテンツと機能への詳細なリンクの作成](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true ) *」を参照してください*。  </span><span class="sxs-lookup"><span data-stu-id="be3af-207">This message will show up in the user’s activity feed and deep link to the tab. *See*  [Create deep links to content and features in Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true )</span></span>

> * <span data-ttu-id="be3af-208">**Bot を使用** します。</span><span class="sxs-lookup"><span data-stu-id="be3af-208">**Use a bot**.</span></span> <span data-ttu-id="be3af-209">このメソッドは、特に Tab スレッドが対象の場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="be3af-209">This method is preferred especially if the Tab thread is targeted.</span></span> <span data-ttu-id="be3af-210">その結果、タブのスレッド化されたスレッドは、最近アクティブな状態で表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="be3af-210">The result will be that the tab’s threaded conversation will be moved into view as recently active.</span></span> <span data-ttu-id="be3af-211">また、このメソッドを使用すると、通知の送信方法をいくらか洗練することができます。</span><span class="sxs-lookup"><span data-stu-id="be3af-211">This method also allows for some sophistication in how the notification is sent.</span></span>

<span data-ttu-id="be3af-212">Tab スレッドにメッセージを送信すると、すべてのユーザーに対して明示的に通知することなく、すべてのユーザーに対するアクティビティの認識が向上します。</span><span class="sxs-lookup"><span data-stu-id="be3af-212">Sending a message to a tab thread increases the awareness of activity to all users without explicitly notifying everyone.</span></span> <span data-ttu-id="be3af-213">これは、ノイズなしで認識されます。</span><span class="sxs-lookup"><span data-stu-id="be3af-213">This is awareness without noise.</span></span> <span data-ttu-id="be3af-214">さらに、特定の `@mention`  ユーザーがフィードに同じ通知を配置する場合は、それらをタブスレッドに直接リンクします。</span><span class="sxs-lookup"><span data-stu-id="be3af-214">In addition, when you `@mention`  specific users the same notification will be placed in their feed, deep linking them to the tab thread directly.</span></span>

### <a name="tab-design-best-practices"></a><span data-ttu-id="be3af-215">タブデザインのベストプラクティス</span><span class="sxs-lookup"><span data-stu-id="be3af-215">Tab design best practices</span></span>

* <span data-ttu-id="be3af-216">個人/静的タブを使用すると、ユーザーが個人のアプリの作業環境から別のチームメンバーとコンテンツを共有できるようになります。</span><span class="sxs-lookup"><span data-stu-id="be3af-216">Personal/Static tabs should enable users to share content from a personal app experience with another team members.</span></span>
* <span data-ttu-id="be3af-217">個人/静的タブでは、チームまたはグループのチャットを対象とするアプリのインスタンスのコンテンツが1つのビューに表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="be3af-217">Personal/Static tabs may present content from team or group chat scoped instances of that app in a single view.</span></span>
* <span data-ttu-id="be3af-218">タブ内のリンクターゲットは、外部ブラウザーにリンクするのではなく、Teams 内に含まれる div 要素 (例: in、task モジュール、タブなど) にリンクする必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-218">Link targets in tabs should not link to an external browser but should link to div elements contained within Teams (example-inside, task modules, tabs, etc).</span></span>
* <span data-ttu-id="be3af-219">タブは、チームのテーマに応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-219">Tabs should be responsive to Team’s themes.</span></span> <span data-ttu-id="be3af-220">Teams テーマが変更されると、アプリ内のテーマもそのテーマを反映するように変更されます。</span><span class="sxs-lookup"><span data-stu-id="be3af-220">When the Teams theme is changed, the theme within the app should also change to reflect that theme.</span></span>
* <span data-ttu-id="be3af-221">タブでは、可能な場合は Teams スタイルのコンポーネントを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-221">Tabs should use Teams-styled components where possible.</span></span> <span data-ttu-id="be3af-222">これは、Teams フォント、種類傾斜、カラーパレット、グリッドシステム、モーション、音声のトーンなどを採用していることを意味します。</span><span class="sxs-lookup"><span data-stu-id="be3af-222">It means adopting Teams fonts, type ramps, color palettes, grid system, motion, tone of voice, etc.</span></span>
* <span data-ttu-id="be3af-223">タブでは、ページ内のナビゲーション、位置、およびダイアログや情報階層の使用に Teams の対話動作を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-223">Tabs should use Teams interaction behaviors for in-page navigation, position, and use of dialogs, information hierarchies, etc.</span></span>
* <span data-ttu-id="be3af-224">タブでは、アプリ内ナビゲーション用に標準の Teams のハンバーガーメニューまたは階層リンクを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-224">Tabs should use the standard Teams hamburger menu and/or breadcrumb for in-app navigation.</span></span> <span data-ttu-id="be3af-225">タブは、メインの Teams ナビゲーションと競合するアイコンがあるアプリバーを左側のレールに表示しません。</span><span class="sxs-lookup"><span data-stu-id="be3af-225">Tabs should not provide an app bar with icons in the left rail that conflicts with the main Teams navigation.</span></span>
* <span data-ttu-id="be3af-226">タブには、アプリ内で3つ以上のレベルのナビゲーションを表示しないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-226">Tabs should not have more than three levels of navigation within the app.</span></span>
* <span data-ttu-id="be3af-227">タブ内のセカンダリページと3番目のページは、階層リンクを介して移動するメインタブ領域の L2/L3 ビューで開く必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-227">Secondary and tertiary pages in a tab should be opened in an L2/L3 view in the main tab area that is navigated via the breadcrumb.</span></span>
* <span data-ttu-id="be3af-228">アプリケーション内で複雑な編集機能があるタブでは、タブ (デスクトップおよび web) ではなく、複数ウィンドウでエディタービューを開く必要があります。</span><span class="sxs-lookup"><span data-stu-id="be3af-228">Tabs that have complex editing capabilities within the app should open the editor view in multi-window rather than a tab (for desktop and web).</span></span>
* <span data-ttu-id="be3af-229">ユーザーの操作性を向上させるために、最初の実行時にようこそメッセージをユーザーに送信し、 **hi**、 **help**、および **hello** コマンドに応答する個人 bot を追加します。</span><span class="sxs-lookup"><span data-stu-id="be3af-229">For improved user experience include a personal bot that sends a welcome message to the user on the first run and responds to the **hi**, **help**, and **hello** commands.</span></span> <span data-ttu-id="be3af-230">詳細については、「 [会話の bot](../../bots/what-are-bots.md#in-a-one-to-one-chat) 」のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="be3af-230">You can refer to the documentation on [conversational bots](../../bots/what-are-bots.md#in-a-one-to-one-chat) for further assistance.</span></span>
