---
title: タブの設計ガイドライン
description: コンテンツとコラボレーションのタブを作成するためのガイドラインについて説明します。
keywords: teams 設計ガイドラインリファレンスフレームワークタブの構成
ms.openlocfilehash: adf86678a42e2267af00734e1ef85efced882488
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674603"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="0345a-104">すべてのタブを使用したコンテンツと会話</span><span class="sxs-lookup"><span data-stu-id="0345a-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="0345a-105">**モバイルクライアントのタブ**</span><span class="sxs-lookup"><span data-stu-id="0345a-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="0345a-106">タブを作成するときに、 [[モバイル] のタブのガイダンス](~/tabs/design/tabs-mobile.md)に従ってください。</span><span class="sxs-lookup"><span data-stu-id="0345a-106">Follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="0345a-107">タブで認証を使用している場合は、Teams の JavaScript SDK をバージョン1.4.1 以降にアップグレードする必要があります。認証は失敗します。</span><span class="sxs-lookup"><span data-stu-id="0345a-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="0345a-108">**モバイルの個人用 (静的) タブ:**</span><span class="sxs-lookup"><span data-stu-id="0345a-108">**Personal (static) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="0345a-109">静的タブ (個人用アプリ) は、[開発者向けプレビュー](~/resources/dev-preview/developer-preview-intro.md)で利用できます。</span><span class="sxs-lookup"><span data-stu-id="0345a-109">Static tabs (personal app) are available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
> * <span data-ttu-id="0345a-110">静的タブを作成する際には、「[モバイルのタブのガイダンス](~/tabs/design/tabs-mobile.md)」に従ってください。</span><span class="sxs-lookup"><span data-stu-id="0345a-110">While building your static tabs, ensure to follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md)</span></span>
>
> <span data-ttu-id="0345a-111">**モバイルのチャネル/グループ (構成可能) のタブ:**</span><span class="sxs-lookup"><span data-stu-id="0345a-111">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="0345a-112">モバイルクライアントは、の`websiteUrl`値があるタブのみを表示します。</span><span class="sxs-lookup"><span data-stu-id="0345a-112">Mobile clients only show tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="0345a-113">チームのモバイルクライアントにタブを表示する場合は、の`websiteUrl`値を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0345a-113">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="0345a-114">モバイルでの既定のオープン動作は、 `websiteUrl`を使用してブラウザーの外部で開くことができます。</span><span class="sxs-lookup"><span data-stu-id="0345a-114">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="0345a-115">公開アプリストアに発行されたアプリの場合、[チャネル] タブを既定でオンにするには、 [[モバイル] のタブのガイダンス](~/tabs/design/tabs-mobile.md)に従って、サポート担当者に連絡して、ホワイトリストを要求します。</span><span class="sxs-lookup"><span data-stu-id="0345a-115">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="0345a-116">タブは、チームの有機ワークフロー内でコンテンツを共有し、会話を保持し、サードパーティのサービスをホストするために使用できるキャンバスです。</span><span class="sxs-lookup"><span data-stu-id="0345a-116">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="0345a-117">Microsoft Teams でタブを作成すると、主要な会話から簡単にアクセスできるように、web アプリのフロントおよび中央が配置されます。</span><span class="sxs-lookup"><span data-stu-id="0345a-117">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="0345a-118">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="0345a-118">Guidelines</span></span>

<span data-ttu-id="0345a-119">適切なタブには、次の特性が表示されます。</span><span class="sxs-lookup"><span data-stu-id="0345a-119">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="0345a-120">フォーカスのある機能</span><span class="sxs-lookup"><span data-stu-id="0345a-120">Focused functionality</span></span>

<span data-ttu-id="0345a-121">タブは、特定のニーズに対応するように構築されている場合に最適に機能します。</span><span class="sxs-lookup"><span data-stu-id="0345a-121">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="0345a-122">タブがあるチャネルに関連する、少数のタスクまたはデータのサブセットにフォーカスします。</span><span class="sxs-lookup"><span data-stu-id="0345a-122">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="0345a-123">クロムが縮小される</span><span class="sxs-lookup"><span data-stu-id="0345a-123">Reduced chrome</span></span>

<span data-ttu-id="0345a-124">タブに複数のパネルを作成したり、ナビゲーションのレイヤーを追加したり、1つのタブで垂直方向および水平方向にスクロールするようにユーザーに要求したりすることは避けてください。つまり、タブにタブを設定しないようにします。</span><span class="sxs-lookup"><span data-stu-id="0345a-124">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

> [!TIP]
> <span data-ttu-id="0345a-125">タブに複数のパネルを作成したり、ナビゲーションのレイヤーを追加したり、1つのタブで垂直方向および水平方向にスクロールするようにユーザーに要求したりすることは避けてください。</span><span class="sxs-lookup"><span data-stu-id="0345a-125">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab.</span></span>

### <a name="integration"></a><span data-ttu-id="0345a-126">統合</span><span class="sxs-lookup"><span data-stu-id="0345a-126">Integration</span></span>

<span data-ttu-id="0345a-127">会話にカードを投稿することで、ユーザーにタブアクティビティについて通知する方法を検索します (例:)。</span><span class="sxs-lookup"><span data-stu-id="0345a-127">Find ways to notify users about tab activity by posting cards to a conversation, for example.</span></span>

### <a name="conversational"></a><span data-ttu-id="0345a-128">会話</span><span class="sxs-lookup"><span data-stu-id="0345a-128">Conversational</span></span>

<span data-ttu-id="0345a-129">タブを中心に会話を円滑にする方法を見つけます。これにより、会話センターがコンテンツ、データ、またはプロセスに対して実行されることが保証されます。</span><span class="sxs-lookup"><span data-stu-id="0345a-129">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="0345a-130">円滑なアクセス</span><span class="sxs-lookup"><span data-stu-id="0345a-130">Streamlined access</span></span>

<span data-ttu-id="0345a-131">適切なときに、適切なユーザーにアクセスを許可していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="0345a-131">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="0345a-132">サインインプロセスを簡単にすることで、投稿とコラボレーションへの障壁をなくすことができます。</span><span class="sxs-lookup"><span data-stu-id="0345a-132">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="personality"></a><span data-ttu-id="0345a-133">プラン</span><span class="sxs-lookup"><span data-stu-id="0345a-133">Personality</span></span>

<span data-ttu-id="0345a-134">タブキャンバスは、自分の環境をブランド化する良い機会を提供します。</span><span class="sxs-lookup"><span data-stu-id="0345a-134">Your tab canvas presents a good opportunity to brand your experience.</span></span> <span data-ttu-id="0345a-135">個性を伝えるために独自のロゴ、色、レイアウトを組み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="0345a-135">Incorporate your own logos, colors, and layouts to communicate personality.</span></span>

<span data-ttu-id="0345a-136">ロゴは、id の重要な部分であり、ユーザーとの接続にも使用されます。</span><span class="sxs-lookup"><span data-stu-id="0345a-136">Your logo is an important part of your identity and a connection with your users.</span></span> <span data-ttu-id="0345a-137">そのため、必ず含めてください。</span><span class="sxs-lookup"><span data-stu-id="0345a-137">So be sure to include it.</span></span>

* <span data-ttu-id="0345a-138">ロゴを左または右または下の端に配置する</span><span class="sxs-lookup"><span data-stu-id="0345a-138">Place your logo in the left or right corner or along the bottom edge</span></span>
* <span data-ttu-id="0345a-139">ロゴのサイズを小さくして、邪魔されないようにする</span><span class="sxs-lookup"><span data-stu-id="0345a-139">Keep your logo small and unobtrusive</span></span>

> [!TIP]
> <span data-ttu-id="0345a-140">Visual スタイルを使用して、サービスが Teams の一部として感じられるようにしてください。</span><span class="sxs-lookup"><span data-stu-id="0345a-140">Please work with our visual style so your service feels like a part of Teams.</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="0345a-141">タブレイアウト</span><span class="sxs-lookup"><span data-stu-id="0345a-141">Tab layouts</span></span>

[!include[Tab layouts](~/includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="0345a-142">タブの種類</span><span class="sxs-lookup"><span data-stu-id="0345a-142">Types of tabs</span></span>

[!include[Tab types](~/includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="0345a-143">構成ページの高さ</span><span class="sxs-lookup"><span data-stu-id="0345a-143">Configuration page height</span></span>

>[!NOTE]
><span data-ttu-id="0345a-144">2018年9月に、[タブの[構成] ページ](~/tabs/how-to/create-tab-pages/configuration-page.md)の高さが変更されましたが、幅は変更されませんでした。</span><span class="sxs-lookup"><span data-stu-id="0345a-144">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="0345a-145">アプリが古いサイズを対象として設計されている場合は、タブの構成ページに大きな縦方向の空白があります。</span><span class="sxs-lookup"><span data-stu-id="0345a-145">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="0345a-146">この変更によって除外された従来のストアアプリは、新しいディメンションに対応するために、更新後に Microsoft に連絡する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0345a-146">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="0345a-147">[タブの構成] ページのサイズ:</span><span class="sxs-lookup"><span data-stu-id="0345a-147">The dimensions of the tab configuration page:</span></span>

<img width="450px" title="構成タブのサイズ" src="~/assets/images/tabs/config-dialog-Contoso2.png" />

### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="0345a-149">タブ構成ページ形式に関するガイドライン</span><span class="sxs-lookup"><span data-stu-id="0345a-149">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="0345a-150">固定高高さのグラフィック要素で、タブの構成ページのコンテンツ領域の最小の高さを基準にします。</span><span class="sxs-lookup"><span data-stu-id="0345a-150">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="0345a-151">を使用して、使用可能な垂直方向の間隔 ([構成] ページ`window.innerHeight`のコンテンツ領域の高さ) を計算します。</span><span class="sxs-lookup"><span data-stu-id="0345a-151">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="0345a-152">これは、 `<iframe>`構成ページが存在するのサイズを返します。これは、今後のリリースで変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0345a-152">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="0345a-153">この値を使用すると、コンテンツは今後の変更に合わせて自動的に調整されます。</span><span class="sxs-lookup"><span data-stu-id="0345a-153">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="0345a-154">可変長要素に垂直方向のスペースを割り当て、固定された高さの要素に対して必要なものを減算します。</span><span class="sxs-lookup"><span data-stu-id="0345a-154">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="0345a-155">*ログイン*状態では、コンテンツを上下に中央揃えで配置します。</span><span class="sxs-lookup"><span data-stu-id="0345a-155">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="0345a-156">背景画像が必要な場合は、新しい画像、領域に合わせてサイズを変更する (推奨) か、同じ画像を保持して次のいずれかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="0345a-156">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="0345a-157">左上隅に合わせて配置します。</span><span class="sxs-lookup"><span data-stu-id="0345a-157">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="0345a-158">イメージのサイズを調整します。</span><span class="sxs-lookup"><span data-stu-id="0345a-158">scaling the image to fit.</span></span>

<span data-ttu-id="0345a-159">適切なサイズに設定すると、タブの構成ページは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="0345a-159">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title="[新しい構成] タブ" src="~/assets/images/tabs/config-dialog-Contoso.png" />

## <a name="best-practices"></a><span data-ttu-id="0345a-161">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="0345a-161">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="0345a-162">常に既定の状態を含める</span><span class="sxs-lookup"><span data-stu-id="0345a-162">Always include a default state</span></span>

<span data-ttu-id="0345a-163">タブを構成できる場合でも、タブを簡単に設定できるように、既定の状態を含めます。</span><span class="sxs-lookup"><span data-stu-id="0345a-163">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="0345a-164">ディープリンク</span><span class="sxs-lookup"><span data-stu-id="0345a-164">Deep linking</span></span>

<span data-ttu-id="0345a-165">可能な限り、カードやボットは、ホストされたタブで豊富なデータにリンクする必要があります。たとえば、カードにバグデータの要約が表示されている場合でも、それをクリックすると、バグ全体がタブに表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="0345a-165">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="0345a-166">規約</span><span class="sxs-lookup"><span data-stu-id="0345a-166">Naming</span></span>

<span data-ttu-id="0345a-167">多くの場合、アプリの名前を使用すると、便利なタブ名を作成できます。</span><span class="sxs-lookup"><span data-stu-id="0345a-167">In many cases, the name of your app may make a great tab name.</span></span> <span data-ttu-id="0345a-168">ただし、タブは、提供する機能に従って名前を付けることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="0345a-168">But consider naming your tabs according to the functionality they provide.</span></span>
