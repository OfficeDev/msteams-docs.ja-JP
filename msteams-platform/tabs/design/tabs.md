---
title: タブの設計ガイドライン
description: コンテンツとコラボレーションのタブを作成するためのガイドラインについて説明します。
keywords: teams 設計ガイドラインリファレンスフレームワークタブ [構成チャネル] タブ [静的] タブ [シンプル] [デザインチーム] タブ
ms.openlocfilehash: 7636159e26a4000efb1d89dd8e9921a91cb5aa39
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796212"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="1e7e0-104">すべてのタブを使用したコンテンツと会話</span><span class="sxs-lookup"><span data-stu-id="1e7e0-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="1e7e0-105">**モバイルクライアントのタブ**</span><span class="sxs-lookup"><span data-stu-id="1e7e0-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="1e7e0-106">タブを作成するときに、 [[モバイル] のタブのガイダンス](./tabs-mobile.md) に従ってください。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-106">Follow the [guidance for tabs on mobile](./tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="1e7e0-107">タブで認証を使用している場合は、Teams の JavaScript SDK をバージョン1.4.1 以降にアップグレードする必要があります。認証は失敗します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="1e7e0-108">**モバイルのチャネル/グループ (構成可能) のタブ:**</span><span class="sxs-lookup"><span data-stu-id="1e7e0-108">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="1e7e0-109">モバイルクライアントは、の値を持つ構成可能なタブのみを表示 `websiteUrl` します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-109">Mobile clients only show configurable tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="1e7e0-110">チームのモバイルクライアントにタブを表示する場合は、の値を設定する必要があり `websiteUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-110">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="1e7e0-111">モバイルでの既定のオープン動作は、を使用してブラウザーの外部で開くことが `websiteUrl` できます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-111">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="1e7e0-112">公開アプリストアに発行されたアプリの場合、[チャネル] タブを既定でオンにするには、 [[モバイル] のタブのガイダンス](~/tabs/design/tabs-mobile.md)に従って、サポート担当者に連絡して、ホワイトリストを要求します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-112">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="1e7e0-113">タブは、チームの有機ワークフロー内でコンテンツを共有し、会話を保持し、サードパーティのサービスをホストするために使用できるキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-113">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="1e7e0-114">Microsoft Teams でタブを作成すると、主要な会話から簡単にアクセスできるように、web アプリのフロントおよび中央が配置されます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-114">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="1e7e0-115">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="1e7e0-115">Guidelines</span></span>

<span data-ttu-id="1e7e0-116">適切なタブには、次の特性が表示されます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-116">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="1e7e0-117">フォーカスのある機能</span><span class="sxs-lookup"><span data-stu-id="1e7e0-117">Focused functionality</span></span>

<span data-ttu-id="1e7e0-118">タブは、特定のニーズに対応するように構築されている場合に最適に機能します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-118">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="1e7e0-119">タブがあるチャネルに関連する、少数のタスクまたはデータのサブセットにフォーカスします。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-119">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="1e7e0-120">クロムの削減</span><span class="sxs-lookup"><span data-stu-id="1e7e0-120">Reduced chrome</span></span>

<span data-ttu-id="1e7e0-121">タブ内に複数のパネルを作成したり、ナビゲーションの階層を増やしたり、同一のタブ内で垂直方向と水平方向の両方のスクロール操作をユーザーに求めたりしないようにします。つまり、タブ内に他のタブがあるような状態にしないようにします。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-121">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

### <a name="integration"></a><span data-ttu-id="1e7e0-122">統合</span><span class="sxs-lookup"><span data-stu-id="1e7e0-122">Integration</span></span>

<span data-ttu-id="1e7e0-123">会話に [アダプティブカード](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) を投稿することで、ユーザーにタブアクティビティについて通知する方法を検索します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-123">Find ways to notify users about tab activity by posting [adaptive cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) to a conversation.</span></span>

### <a name="conversational"></a><span data-ttu-id="1e7e0-124">会話性</span><span class="sxs-lookup"><span data-stu-id="1e7e0-124">Conversational</span></span>

<span data-ttu-id="1e7e0-125">タブを中心に会話を円滑にする方法を見つけます。これにより、会話センターがコンテンツ、データ、またはプロセスに対して実行されることが保証されます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-125">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="1e7e0-126">アクセスの効率化</span><span class="sxs-lookup"><span data-stu-id="1e7e0-126">Streamlined access</span></span>

<span data-ttu-id="1e7e0-127">適切なときに、適切なユーザーにアクセスを許可していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-127">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="1e7e0-128">サインインプロセスを簡単にすることで、投稿とコラボレーションへの障壁をなくすことができます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-128">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="responsiveness-to-window-sizing"></a><span data-ttu-id="1e7e0-129">ウィンドウのサイズ変更への応答</span><span class="sxs-lookup"><span data-stu-id="1e7e0-129">Responsiveness to window sizing</span></span>

<span data-ttu-id="1e7e0-130">Teams は、ウィンドウのサイズが720ピクセルの場合に使用できるので、タブを小さなウィンドウで使用できることを確認することは、非常に高解像度の場合と同様に重要です。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-130">Teams can be used in window sizes as small as 720px, so making sure that a tab is usable in a small window is just as important as usability at very high resolutions.</span></span>

### <a name="flat-navigation"></a><span data-ttu-id="1e7e0-131">フラットナビゲーション</span><span class="sxs-lookup"><span data-stu-id="1e7e0-131">Flat navigation</span></span>

<span data-ttu-id="1e7e0-132">開発者は、ポータル全体をタブに追加しないようにしてください。ナビゲーションを比較的フラットに維持すると、より単純な会話モデルが維持されます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-132">We ask developers not to add their entire portal to a tab. Keeping the navigation relatively flat helps maintain a simpler conversational model.</span></span> <span data-ttu-id="1e7e0-133">言い換えると、会話は、トリアージされた作業項目、または仕様のような1つの事柄の一覧についてのものです。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-133">In other words, the conversation is about a list of things, such as triaged work items, or a single thing, like a spec.</span></span>

<span data-ttu-id="1e7e0-134">スレッド化された会話内に深いナビゲーション階層を使用して、固有のナビゲーションの課題があります。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-134">There are inherent navigational challenges with deep navigation hierarchy, within threaded conversations.</span></span> <span data-ttu-id="1e7e0-135">ユーザーにとって最適な操作を行うには、タブナビゲーションを最小限に抑え、次のように設計する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-135">For the best user experience, your tab navigation should be kept to a minimum and be designed as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="1e7e0-136">**個別の作業項目またはエンティティなどのタスクモジュールを開き** ます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-136">**Opens a task module such as an individual work item or entity** .</span></span> <span data-ttu-id="1e7e0-137">これにより、チャットが完全には不可能になります。これは、サブエンティティや編集機能ではなく、特にタブについてのチャットを維持するための最適なオプションです。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-137">This precludes chat entirely and is the best option to keep chat specifically about the tab and not the sub-entities or editing experiences.</span></span>
>* <span data-ttu-id="1e7e0-138">**Iframe で擬似ダイアログを開き** ます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-138">**Opens a pseudo dialog in an iframe** .</span></span> <span data-ttu-id="1e7e0-139">スクリーン背景を使用する場合は、暗色ではなく明るい色を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-139">If used with a screened background we recommend using the lighter color rather than the dark.</span></span> <span data-ttu-id="1e7e0-140">`app-gray-10 at 30%`透過性は適切に機能します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-140">The `app-gray-10 at 30%` transparency works well.</span></span>
>* <span data-ttu-id="1e7e0-141">**ブラウザーページを開き** ます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-141">**Opens a browser page** .</span></span>

### <a name="personality"></a><span data-ttu-id="1e7e0-142">プラン</span><span class="sxs-lookup"><span data-stu-id="1e7e0-142">Personality</span></span>

<span data-ttu-id="1e7e0-143">タブキャンバスは、自分の環境をブランド化する絶好の機会を提供します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-143">Your tab canvas presents a great opportunity to brand your experience.</span></span> <span data-ttu-id="1e7e0-144">ロゴは、ユーザーとの間で id と接続の重要な部分です。そのため、必ず含めてください。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-144">Your logo is an important part of your identity and connection with your users., so be sure to include it:</span></span>

> [!div class="checklist"]
>
>* <span data-ttu-id="1e7e0-145">ロゴを左または右または下の端に配置する</span><span class="sxs-lookup"><span data-stu-id="1e7e0-145">Place your logo in the left or right corner or along the bottom edge</span></span>
> * <span data-ttu-id="1e7e0-146">ロゴのサイズを小さくして、邪魔されないようにする</span><span class="sxs-lookup"><span data-stu-id="1e7e0-146">Keep your logo small and unobtrusive</span></span>

<span data-ttu-id="1e7e0-147">独自の色とレイアウトを組み込むことは、個性を伝える上でも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-147">Incorporating your own colors and layouts twill also aid in communicating personality.</span></span>

> [!TIP]
> <span data-ttu-id="1e7e0-148">Visual スタイルを使用して、サービスが Teams の一部として感じられるようにしてください。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-148">Please work with our visual style so your service feels like a part of Teams.</span></span> <span data-ttu-id="1e7e0-149">[Teams の色](../../concepts/design/components/color.md)などの例を *参照してください* 。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-149">*See* , for example [Teams Colors](../../concepts/design/components/color.md)</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="1e7e0-150">タブレイアウト</span><span class="sxs-lookup"><span data-stu-id="1e7e0-150">Tab layouts</span></span>

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="1e7e0-151">タブの種類</span><span class="sxs-lookup"><span data-stu-id="1e7e0-151">Types of tabs</span></span>

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="1e7e0-152">構成ページの高さ</span><span class="sxs-lookup"><span data-stu-id="1e7e0-152">Configuration page height</span></span>

>[!IMPORTANT]
><span data-ttu-id="1e7e0-153">2018年9月に、[タブの [構成] ページ](~/tabs/how-to/create-tab-pages/configuration-page.md) の高さが変更されましたが、幅は変更されませんでした。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-153">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="1e7e0-154">アプリが古いサイズを対象として設計されている場合は、タブの構成ページに大きな縦方向の空白があります。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-154">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="1e7e0-155">この変更によって除外された従来のストアアプリは、新しいディメンションに対応するために、更新後に Microsoft に連絡する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-155">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="1e7e0-156">[タブの構成] ページのサイズ:</span><span class="sxs-lookup"><span data-stu-id="1e7e0-156">The dimensions of the tab configuration page:</span></span>


<img width="450px" title="構成タブのサイズ" src="~/assets/images/tabs/config-dialog-Contoso2.png" alt="sizes for config tabs" />


### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="1e7e0-158">タブ構成ページ形式に関するガイドライン</span><span class="sxs-lookup"><span data-stu-id="1e7e0-158">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="1e7e0-159">固定高高さのグラフィック要素で、タブの構成ページのコンテンツ領域の最小の高さを基準にします。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-159">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="1e7e0-160">を使用して、使用可能な垂直方向の間隔 ([構成] ページのコンテンツ領域の高さ) を計算し `window.innerHeight` ます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-160">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="1e7e0-161">これは、構成ページが存在するのサイズを返します。これは、 `<iframe>` 今後のリリースで変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-161">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="1e7e0-162">この値を使用すると、コンテンツは今後の変更に合わせて自動的に調整されます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-162">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="1e7e0-163">可変長要素に垂直方向のスペースを割り当て、固定された高さの要素に対して必要なものを減算します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-163">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="1e7e0-164">*ログイン* 状態では、コンテンツを上下に中央揃えで配置します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-164">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="1e7e0-165">背景画像が必要な場合は、新しい画像、領域に合わせてサイズを変更する (推奨) か、同じ画像を保持して次のいずれかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-165">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="1e7e0-166">左上隅に合わせて配置します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-166">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="1e7e0-167">イメージのサイズを調整します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-167">scaling the image to fit.</span></span>

<span data-ttu-id="1e7e0-168">適切なサイズに設定すると、タブの構成ページは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-168">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title="[新しい構成] タブ" src="~/assets/images/tabs/config-dialog-Contoso.png" alt="new config tab"/>

## <a name="best-practices"></a><span data-ttu-id="1e7e0-170">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="1e7e0-170">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="1e7e0-171">常に既定の状態を含める</span><span class="sxs-lookup"><span data-stu-id="1e7e0-171">Always include a default state</span></span>

<span data-ttu-id="1e7e0-172">タブを構成できる場合でも、タブを簡単に設定できるように、既定の状態を含めます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-172">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="1e7e0-173">ディープリンク</span><span class="sxs-lookup"><span data-stu-id="1e7e0-173">Deep linking</span></span>

<span data-ttu-id="1e7e0-174">可能な限り、カードやボットは、ホストされたタブで豊富なデータにリンクする必要があります。たとえば、カードにバグデータの要約が表示されている場合でも、それをクリックすると、バグ全体がタブに表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-174">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="1e7e0-175">規約</span><span class="sxs-lookup"><span data-stu-id="1e7e0-175">Naming</span></span>

<span data-ttu-id="1e7e0-176">多くの場合、アプリの名前を使用すると、便利なタブ名が作成されます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-176">In many cases, the name of your app will make a great tab name.</span></span> <span data-ttu-id="1e7e0-177">ただし、タブは、提供される機能に従って名前を付けることも検討してください。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-177">But, also consider naming your tabs according to the functionality they provide.</span></span>

## <a name="notifications-for-tabs"></a><span data-ttu-id="1e7e0-178">タブの通知</span><span class="sxs-lookup"><span data-stu-id="1e7e0-178">Notifications for tabs</span></span>

<span data-ttu-id="1e7e0-179">タブのコンテンツの変更については、次の2つのモードの通知があります。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-179">There are two modes of notification for tab content changes:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="1e7e0-180">**アプリ api を使用して、ユーザーに変更を通知** します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-180">**Use the app api to notify users of changes** .</span></span> <span data-ttu-id="1e7e0-181">このメッセージは、ユーザーのアクティビティフィードに表示され、タブに深くリンクします。「 [Microsoft Teams のコンテンツと機能への詳細なリンクの作成](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true ) *」を参照してください* 。  </span><span class="sxs-lookup"><span data-stu-id="1e7e0-181">This message will show up in the user’s activity feed and deep link to the tab. *See*  [Create deep links to content and features in Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true )</span></span>
> * <span data-ttu-id="1e7e0-182">**Bot を使用** します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-182">**Use a bot** .</span></span> <span data-ttu-id="1e7e0-183">このメソッドは、特に Tab スレッドが対象の場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-183">This method is preferred especially if the Tab thread is targeted.</span></span> <span data-ttu-id="1e7e0-184">その結果、タブのスレッド化されたスレッドは、最近アクティブな状態で表示されるようになります。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-184">The result will be that the tab’s threaded conversation will be moved into view as recently active.</span></span> <span data-ttu-id="1e7e0-185">また、このメソッドを使用すると、通知の送信方法をいくらか洗練することができます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-185">This method also allows for some sophistication in how the notification is sent.</span></span>

  <span data-ttu-id="1e7e0-186">Tab スレッドにメッセージを送信すると、すべてのユーザーに対して明示的に通知することなく、すべてのユーザーに対するアクティビティの認識が向上します。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-186">Sending a message to a tab thread increases the awareness of activity to all users without explicitly notifying everyone.</span></span> <span data-ttu-id="1e7e0-187">これは、ノイズなしで認識されます。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-187">This is awareness without noise.</span></span> <span data-ttu-id="1e7e0-188">さらに、特定の `@mention`  ユーザーがフィードに同じ通知を配置する場合は、それらをタブスレッドに直接リンクします。</span><span class="sxs-lookup"><span data-stu-id="1e7e0-188">In addition, when you `@mention`  specific users the same notification will be placed in their feed, deep linking them to the tab thread directly.</span></span>
