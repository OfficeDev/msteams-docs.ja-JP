---
title: SharePoint の Microsoft Teams タブを SPFx web パーツとして追加する
author: laujan
description: 既存の Teams タブを sharepoint Framework web パーツとして SharePoint に展開する方法について説明します。
keywords: teams のタブ sharepoint framework の開発
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2bdc7ab578be485eee33020b3b0c1a4099fd8ade
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818942"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a><span data-ttu-id="8280a-104">SharePoint の Microsoft Teams タブを SPFx web パーツとして追加する</span><span class="sxs-lookup"><span data-stu-id="8280a-104">Adding a Microsoft Teams tab in SharePoint as an SPFx web part</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8280a-105">この機能は現在プレビュー段階であり、変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8280a-105">This feature is currently in preview and is subject to change.</span></span> <span data-ttu-id="8280a-106">運用環境での使用はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="8280a-106">It is not supported for use in production environments.</span></span> <span data-ttu-id="8280a-107">[SharePoint 開発ドキュメントの問題リスト](https://github.com/SharePoint/sp-dev-docs/issues)を使用して、この機能に関するフィードバックやご意見をお寄せください。</span><span class="sxs-lookup"><span data-stu-id="8280a-107">Your feedback and input around this capability is welcome using the [SharePoint Dev Docs issue list](https://github.com/SharePoint/sp-dev-docs/issues).</span></span>

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="8280a-108">Teams と SharePoint の間の高度な統合</span><span class="sxs-lookup"><span data-stu-id="8280a-108">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="8280a-109">11月リリースの Teams と SharePoint Framework v を使用しています。</span><span class="sxs-lookup"><span data-stu-id="8280a-109">With the November release of Teams and SharePoint Framework v.</span></span> <span data-ttu-id="8280a-110">1.7 の開発者には、次の2つの強力な機能があります。</span><span class="sxs-lookup"><span data-stu-id="8280a-110">1.7, developers have two powerful capabilities:</span></span>

<ul  class="panelContent cardsC">
<li>
    <a href="#introduction">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/image084.png" alt="tab-in-sharepoint view"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="8280a-111">SharePoint の Teams タブ</span><span class="sxs-lookup"><span data-stu-id="8280a-111">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="8280a-112">Teams アプリを Sharepoint にすることで、SharePoint で豊富なアプリエクスペリエンスを作成します (この記事)。</span><span class="sxs-lookup"><span data-stu-id="8280a-112">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li>
    <a href="https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/SharePoint-web-part-exposed-as-a-Tab-in-Microsoft-Teams.png" alt="web-part-exposed-as-a-tab" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="8280a-113">Teams での SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="8280a-113">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="8280a-114">SharePoint web パーツを Teams に移行し、SharePoint でホスティングを管理できるようにします。</span><span class="sxs-lookup"><span data-stu-id="8280a-114">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="8280a-115">SharePoint の Teams タブ</span><span class="sxs-lookup"><span data-stu-id="8280a-115">Teams tabs in SharePoint</span></span>

<span data-ttu-id="8280a-116">SharePoint Framework v2.0 を使用すると、開発者は Teams タブを使用して SharePoint でホストすることができるようになります。</span><span class="sxs-lookup"><span data-stu-id="8280a-116">With SharePoint Framework v.1.7, we’re now supporting the ability for developers to take their Teams tabs and host it in SharePoint.</span></span> <span data-ttu-id="8280a-117">SharePoint でホストされているタブの場合と同様に、SharePoint サイトのコンテキストと理解を保ったまま、Teams タブのすべての機能が公開されています。</span><span class="sxs-lookup"><span data-stu-id="8280a-117">As Tabs hosted in SharePoint get a similar "full page" experience, exposing the all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="8280a-118">Teams での SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="8280a-118">SharePoint Framework in Teams</span></span>

<span data-ttu-id="8280a-119">SharePoint Framework を使用して Microsoft Teams のタブを実装することもできます。</span><span class="sxs-lookup"><span data-stu-id="8280a-119">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="8280a-120">Sharepoint 開発者にとって、sharepoint Framework web パーツは Azure などの外部サービスを必要とせずに SharePoint 内でホストされるため、これにより、Teams タブの開発プロセスが大幅に簡素化されます。</span><span class="sxs-lookup"><span data-stu-id="8280a-120">For SharePoint developers, this significantly simplifies the development process for Teams tabs because SharePoint Framework web parts are hosted within SharePoint without any need for external services such as Azure.</span></span> [<span data-ttu-id="8280a-121">Teams での SharePoint Framework の使用方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8280a-121">Learn more about using the SharePoint Framework in Teams.</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a><span data-ttu-id="8280a-122">概要</span><span class="sxs-lookup"><span data-stu-id="8280a-122">Introduction</span></span>

<span data-ttu-id="8280a-123">次の手順では、Microsoft Teams サンプルアプリからタブを取得し、それを SharePoint で使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8280a-123">These instructions will explain how you can take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> <span data-ttu-id="8280a-124">必要な統合作業に焦点を当てるために、Azure で既にホストされているタブを使用します。</span><span class="sxs-lookup"><span data-stu-id="8280a-124">We will be using a tab that's already hosted on Azure in order to focus on the required integration work.</span></span>

<span data-ttu-id="8280a-125">使用しているサンプルアプリは、人材管理アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="8280a-125">The sample app we're using is a Talent Management application.</span></span> <span data-ttu-id="8280a-126">これにより、チーム内のオープンポジションの採用候補の雇用プロセスが管理されます。</span><span class="sxs-lookup"><span data-stu-id="8280a-126">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="8280a-127">(アプリ自体は見栄えがよく見えますが、実際には何も実行しません。</span><span class="sxs-lookup"><span data-stu-id="8280a-127">(The app itself, while it looks nice, doesn't actually do anything.</span></span> <span data-ttu-id="8280a-128">Teams アプリを作成して Teams に読み込むことに重点を置いて、実際の人材管理アプリケーションを作成することはお勧めしません。</span><span class="sxs-lookup"><span data-stu-id="8280a-128">We want to focus on building a Teams app and loading it into Teams, not create a real talent management application.)</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="8280a-129">このアプローチの利点</span><span class="sxs-lookup"><span data-stu-id="8280a-129">Benefits of this approach</span></span>

- <span data-ttu-id="8280a-130">[既存のチーム] タブを使用して SharePoint ユーザーにアクセスする</span><span class="sxs-lookup"><span data-stu-id="8280a-130">Reach SharePoint users with your existing Teams tab</span></span>
- <span data-ttu-id="8280a-131">アプリのマニフェストを SharePoint アプリカタログに直接アップロードします。</span><span class="sxs-lookup"><span data-stu-id="8280a-131">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="8280a-132">[Teams アプリケーションパッケージ](~/concepts/build-and-test/apps-package.md) が SharePoint によってサポートされるようになりました</span><span class="sxs-lookup"><span data-stu-id="8280a-132">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint</span></span>
- <span data-ttu-id="8280a-133">エンドユーザーは、他の SharePoint web パーツと同じように、ページ上のタブを構成します。</span><span class="sxs-lookup"><span data-stu-id="8280a-133">End users configure the tab on a page just like any other SharePoint web part</span></span>
- <span data-ttu-id="8280a-134">タブは、Teams 内で実行する場合と同様に、 [コンテキスト](~/tabs/how-to/access-teams-context.md) にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="8280a-134">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) just as it can when running inside Teams</span></span>

## <a name="step-1-testing-the-sample-app"></a><span data-ttu-id="8280a-135">手順 1: サンプルアプリをテストする</span><span class="sxs-lookup"><span data-stu-id="8280a-135">Step 1: Testing the sample app</span></span>

<span data-ttu-id="8280a-136">サンプルアプリのマニフェストを [**ここ**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)からダウンロードしてください。</span><span class="sxs-lookup"><span data-stu-id="8280a-136">Download the sample app manifest from [**here**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

<span data-ttu-id="8280a-137">Microsoft Teams で、左下の [Store] アイコンをクリックしてから、左下の [カスタムアプリのアップロード] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8280a-137">In Microsoft Teams, click on the Store icon at the lower left and then "Upload a custom app" at the lower left.</span></span> <span data-ttu-id="8280a-138">アップロードするファイルは、[ダウンロード] フォルダーにあります。これは TalentMgmt-Azure.zip と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="8280a-138">The file to upload will be located in your Downloads folder; it's called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="8280a-139">すべてがうまくいくと、才能 management アプリのインストール/同意画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8280a-139">If all goes well, you'll see the install/consent screen for the talent management app.</span></span> <span data-ttu-id="8280a-140">インストール先のチームを選択し、[インストール] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8280a-140">Choose the team you want to install to and click the Install button.</span></span> <span data-ttu-id="8280a-141">アプリを自由に試すことができるようになりました。</span><span class="sxs-lookup"><span data-stu-id="8280a-141">You're now free to experiment with the app.</span></span>

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a><span data-ttu-id="8280a-142">手順 2: SharePoint で Teams タブを使用する</span><span class="sxs-lookup"><span data-stu-id="8280a-142">Step 2: Using the Teams tab in SharePoint</span></span>

<span data-ttu-id="8280a-143">にアクセスして、Teams アプリパッケージをアップロードし、SharePoint アプリカタログに展開し `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` ます (例:) `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。</span><span class="sxs-lookup"><span data-stu-id="8280a-143">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`, e.g. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

<span data-ttu-id="8280a-144">メッセージが表示されたら、[組織内のすべてのサイトでこのソリューションを使用できるようにする] を有効にします。</span><span class="sxs-lookup"><span data-stu-id="8280a-144">When prompted, enable "Make this solution available to all sites in the organization":</span></span>

![Sharepoint ビューのタブ](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

<span data-ttu-id="8280a-146">サイトで、右上隅にある歯車ボタンをクリックし、[ページの追加] をクリックして、新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="8280a-146">In your site, create a new page by clicking in the gear button at the upper right and then "Add a page":</span></span>

![Sharepoint ビュー](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

<span data-ttu-id="8280a-148">SharePoint ページの作成環境が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8280a-148">You'll see the SharePoint Pages authoring experience.</span></span> <span data-ttu-id="8280a-149">ページに「My Teams タブ」という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="8280a-149">Name your page "My Teams Tab".</span></span>

<span data-ttu-id="8280a-150">+ ボタンを押して web パーツツールボックスを開き、[Teams] タブ ("Contoso HR" という名前) を選択します。</span><span class="sxs-lookup"><span data-stu-id="8280a-150">Open the web part toolbox by pressing the + button, and select your Teams Tab (named "Contoso HR").</span></span> <span data-ttu-id="8280a-151">Web パーツはアルファベット順に並べ替えられます。リストが長い場合は、検索バーを使用して検索できます。</span><span class="sxs-lookup"><span data-stu-id="8280a-151">Web parts are sorted alphabetically; if it's a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="8280a-152">これにより、Teams タブを含むキャンバスに web パーツが作成されます。</span><span class="sxs-lookup"><span data-stu-id="8280a-152">This will create a web part in the canvas that contains your Teams tab:</span></span>

![タブビュー](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

<span data-ttu-id="8280a-154">編集が終了したら、[発行] ボタンを押します。</span><span class="sxs-lookup"><span data-stu-id="8280a-154">Press the "Publish" button when you are finished editing.</span></span>

<span data-ttu-id="8280a-155">左側のナビゲーションバーにページのクイックリファレンスを表示するには、[ページをナビゲーションに追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8280a-155">You may want to click "Add page to navigation" to have a quick reference to your page in the left navigation bar:</span></span>

![Sharepoint 画像のタブ](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="8280a-157">手順 3: SharePoint でアプリページを調べる</span><span class="sxs-lookup"><span data-stu-id="8280a-157">Step 3: Explore App Pages in SharePoint</span></span>

<span data-ttu-id="8280a-158">ページが発行されると、 [Teams アプリを SharePoint 内でより完全な体験に](/sharepoint/dev/spfx/web-parts/single-part-app-pages)することができます。</span><span class="sxs-lookup"><span data-stu-id="8280a-158">Once your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="8280a-159">これにより、現在のページがアプリページに変換され、[Teams] タブの完全なページ表示がある通常の SharePoint ページレイアウトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8280a-159">This converts the current page into an App Page, showing the normal SharePoint page layout with a full-page experience for the Teams tab:</span></span>

![Sharepoint のタブの画像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="more-information"></a><span data-ttu-id="8280a-161">詳細情報</span><span class="sxs-lookup"><span data-stu-id="8280a-161">More information</span></span>

- [<span data-ttu-id="8280a-162">SharePoint Framework を使用した Microsoft Teams タブの作成: チュートリアル</span><span class="sxs-lookup"><span data-stu-id="8280a-162">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [<span data-ttu-id="8280a-163">SharePoint Online での Single Part App Pages の使用</span><span class="sxs-lookup"><span data-stu-id="8280a-163">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
