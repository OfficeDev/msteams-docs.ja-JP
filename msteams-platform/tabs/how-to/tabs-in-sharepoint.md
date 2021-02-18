---
title: SharePoint の Microsoft Teams タブを SPFx Web パーツとして追加する
author: laujan
description: 既存の Teams タブを SharePoint Framework Web パーツとして SharePoint に展開する方法。
keywords: teams タブの sharepoint フレームワーク開発
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2e5d1b01aa5f7566e25c7720d6a0539386226576
ms.sourcegitcommit: 6caf503de5544fb8b9c8c6bef8eff4ff5a46068c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/17/2021
ms.locfileid: "50270792"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a><span data-ttu-id="2bfcf-104">SharePoint の Microsoft Teams タブを SPFx Web パーツとして追加する</span><span class="sxs-lookup"><span data-stu-id="2bfcf-104">Adding a Microsoft Teams tab in SharePoint as an SPFx web part</span></span>

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="2bfcf-105">Teams と SharePoint の豊富な統合</span><span class="sxs-lookup"><span data-stu-id="2bfcf-105">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="2bfcf-106">Teams と SharePoint Framework v の 11 月リリース</span><span class="sxs-lookup"><span data-stu-id="2bfcf-106">With the November release of Teams and SharePoint Framework v.</span></span> <span data-ttu-id="2bfcf-107">1.7、開発者には次の 2 つの強力な機能があります。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-107">1.7, developers have two powerful capabilities:</span></span>

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
                        <h3><span data-ttu-id="2bfcf-108">SharePoint の Teams タブ</span><span class="sxs-lookup"><span data-stu-id="2bfcf-108">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="2bfcf-109">Teams アプリを SharePoint に取り込み、SharePoint で豊富なアプリ エクスペリエンスを作成します (この記事)。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-109">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
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
                        <h3><span data-ttu-id="2bfcf-110">Teams の SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="2bfcf-110">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="2bfcf-111">SharePoint Web パーツを Teams に持ち込み、SharePoint がホスティングを管理します。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-111">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="2bfcf-112">SharePoint の Teams タブ</span><span class="sxs-lookup"><span data-stu-id="2bfcf-112">Teams tabs in SharePoint</span></span>

<span data-ttu-id="2bfcf-113">SharePoint Framework v.1.7 では、開発者が Teams タブを使用して SharePoint でホストする機能をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-113">With SharePoint Framework v.1.7, we’re now supporting the ability for developers to take their Teams tabs and host it in SharePoint.</span></span> <span data-ttu-id="2bfcf-114">SharePoint でホストされているタブも同様の "ページ全体" エクスペリエンスを得て、SharePoint サイトのコンテキストと使い慣れたものにしながら Teams タブのすべての機能を公開します。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-114">As Tabs hosted in SharePoint get a similar "full page" experience, exposing the all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="2bfcf-115">Teams の SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="2bfcf-115">SharePoint Framework in Teams</span></span>

<span data-ttu-id="2bfcf-116">SharePoint Framework を使用して Microsoft Teams タブを実装することもできます。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-116">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="2bfcf-117">SharePoint 開発者の場合、SharePoint Framework Web パーツは Azure などの外部サービスを必要とせずに SharePoint 内でホストされるので、Teams タブの開発プロセスが大幅に簡素化されます。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-117">For SharePoint developers, this significantly simplifies the development process for Teams tabs because SharePoint Framework web parts are hosted within SharePoint without any need for external services such as Azure.</span></span> [<span data-ttu-id="2bfcf-118">Teams での SharePoint Framework の使用の詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-118">Learn more about using the SharePoint Framework in Teams.</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a><span data-ttu-id="2bfcf-119">はじめに</span><span class="sxs-lookup"><span data-stu-id="2bfcf-119">Introduction</span></span>

<span data-ttu-id="2bfcf-120">次の手順では、Microsoft Teams サンプル アプリからタブを取り、SharePoint で使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-120">These instructions will explain how you can take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> <span data-ttu-id="2bfcf-121">必要な統合作業に集中するために、Azure で既にホストされているタブを使用します。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-121">We will be using a tab that's already hosted on Azure in order to focus on the required integration work.</span></span>

<span data-ttu-id="2bfcf-122">使用しているサンプル アプリは、Talent Management アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-122">The sample app we're using is a Talent Management application.</span></span> <span data-ttu-id="2bfcf-123">チーム内のオープンポジションの候補の採用プロセスを管理します。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-123">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="2bfcf-124">(アプリ自体は見栄えは良く見えますが、実際には何もしません。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-124">(The app itself, while it looks nice, doesn't actually do anything.</span></span> <span data-ttu-id="2bfcf-125">実際の人材管理アプリケーションを作成するのではなく、Teams アプリの構築と Teams への読み込みに重点を置きたいと思っています。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-125">We want to focus on building a Teams app and loading it into Teams, not create a real talent management application.)</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="2bfcf-126">このアプローチの利点</span><span class="sxs-lookup"><span data-stu-id="2bfcf-126">Benefits of this approach</span></span>

- <span data-ttu-id="2bfcf-127">既存の Teams タブを使用して SharePoint ユーザーにアクセスする</span><span class="sxs-lookup"><span data-stu-id="2bfcf-127">Reach SharePoint users with your existing Teams tab</span></span>
- <span data-ttu-id="2bfcf-128">アプリ マニフェストを SharePoint アプリ カタログに直接アップロードします。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-128">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="2bfcf-129">[Teams アプリケーション パッケージ](~/concepts/build-and-test/apps-package.md) が SharePoint でサポートされる</span><span class="sxs-lookup"><span data-stu-id="2bfcf-129">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint</span></span>
- <span data-ttu-id="2bfcf-130">エンド ユーザーが他の SharePoint Web パーツと同様にページ上のタブを構成する</span><span class="sxs-lookup"><span data-stu-id="2bfcf-130">End users configure the tab on a page just like any other SharePoint web part</span></span>
- <span data-ttu-id="2bfcf-131">タブは、Teams [内で](~/tabs/how-to/access-teams-context.md) 実行する場合と同じ方法でコンテキストにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-131">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) just as it can when running inside Teams</span></span>

## <a name="step-1-testing-the-sample-app"></a><span data-ttu-id="2bfcf-132">手順 1: サンプル アプリをテストする</span><span class="sxs-lookup"><span data-stu-id="2bfcf-132">Step 1: Testing the sample app</span></span>

<span data-ttu-id="2bfcf-133">サンプル アプリ マニフェストは、ここからダウンロード [**してください**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-133">Download the sample app manifest from [**here**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

<span data-ttu-id="2bfcf-134">Microsoft Teams で、左下の [ストア] アイコンをクリックし、左下の [カスタム アプリのアップロード] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-134">In Microsoft Teams, click on the Store icon at the lower left and then "Upload a custom app" at the lower left.</span></span> <span data-ttu-id="2bfcf-135">アップロードするファイルは[ダウンロード] フォルダーにあります。このメソッドは、TalentMgmt-Azure.zip。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-135">The file to upload will be located in your Downloads folder; it's called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="2bfcf-136">すべて問題ない場合は、人材管理アプリのインストール/同意画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-136">If all goes well, you'll see the install/consent screen for the talent management app.</span></span> <span data-ttu-id="2bfcf-137">インストールするチームを選択し、[インストール] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-137">Choose the team you want to install to and click the Install button.</span></span> <span data-ttu-id="2bfcf-138">これで、アプリを自由に試す必要があります。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-138">You're now free to experiment with the app.</span></span>

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a><span data-ttu-id="2bfcf-139">手順 2: SharePoint の [Teams] タブを使用する</span><span class="sxs-lookup"><span data-stu-id="2bfcf-139">Step 2: Using the Teams tab in SharePoint</span></span>

<span data-ttu-id="2bfcf-140">Teams アプリ パッケージをアップロードし、SharePoint アプリ カタログに展開するには、次に例 `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` を示します `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-140">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`, e.g. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

<span data-ttu-id="2bfcf-141">メッセージが表示されたら、"このソリューションを組織内のすべてのサイトで使用可能にする" を有効にします。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-141">When prompted, enable "Make this solution available to all sites in the organization":</span></span>

![SharePoint ビューのタブ](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

<span data-ttu-id="2bfcf-143">サイトで、右上の歯車ボタンをクリックし、[ページの追加] をクリックして、新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-143">In your site, create a new page by clicking in the gear button at the upper right and then "Add a page":</span></span>

![Sharepoint ビュー](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

<span data-ttu-id="2bfcf-145">SharePoint ページの作成エクスペリエンスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-145">You'll see the SharePoint Pages authoring experience.</span></span> <span data-ttu-id="2bfcf-146">ページに「自分の Teams タブ」という名前を付け、</span><span class="sxs-lookup"><span data-stu-id="2bfcf-146">Name your page "My Teams Tab".</span></span>

<span data-ttu-id="2bfcf-147">[+] ボタンを押して Web パーツ ツールボックスを開き、Teams タブ ("Contoso HR" という名前) を選択します。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-147">Open the web part toolbox by pressing the + button, and select your Teams Tab (named "Contoso HR").</span></span> <span data-ttu-id="2bfcf-148">Web パーツはアルファベット順に並べ替えされます。リストが長い場合は、検索バーを使用して検索できます。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-148">Web parts are sorted alphabetically; if it's a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="2bfcf-149">これにより、Teams タブを含む Web パーツがキャンバスに作成されます。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-149">This will create a web part in the canvas that contains your Teams tab:</span></span>

![タブ ビュー](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

<span data-ttu-id="2bfcf-151">編集が完了したら、[発行] ボタンを押します。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-151">Press the "Publish" button when you are finished editing.</span></span>

<span data-ttu-id="2bfcf-152">左側のナビゲーション バーでページをクイック参照するには、[ナビゲーションにページを追加] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-152">You may want to click "Add page to navigation" to have a quick reference to your page in the left navigation bar:</span></span>

![Sharepoint イメージのタブ](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="2bfcf-154">手順 3: SharePoint のアプリ ページを確認する</span><span class="sxs-lookup"><span data-stu-id="2bfcf-154">Step 3: Explore App Pages in SharePoint</span></span>

<span data-ttu-id="2bfcf-155">ページが公開された後は、Teams アプリを SharePoint 内のより完全な [エクスペリエンスに変える方法について説明します](/sharepoint/dev/spfx/web-parts/single-part-app-pages)。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-155">Once your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="2bfcf-156">これにより、現在のページがアプリ ページに変換されます。[Teams] タブでは、通常の SharePoint ページ レイアウトとページ全体のエクスペリエンスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-156">This converts the current page into an App Page, showing the normal SharePoint page layout with a full-page experience for the Teams tab:</span></span>

![Sharepoint のタブの画像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a><span data-ttu-id="2bfcf-158">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="2bfcf-158">Code sample</span></span>
| <span data-ttu-id="2bfcf-159">**サンプルの名前**</span><span class="sxs-lookup"><span data-stu-id="2bfcf-159">**Sample name**</span></span> | <span data-ttu-id="2bfcf-160">**説明**</span><span class="sxs-lookup"><span data-stu-id="2bfcf-160">**Description**</span></span> | <span data-ttu-id="2bfcf-161">**SPFx**</span><span class="sxs-lookup"><span data-stu-id="2bfcf-161">**SPFx**</span></span> |
|-----------------|-----------------|----------|
| <span data-ttu-id="2bfcf-162">SPFx Web パーツ</span><span class="sxs-lookup"><span data-stu-id="2bfcf-162">SPFx web part</span></span> | <span data-ttu-id="2bfcf-163">タブ、チャネル、およびグループ用の SPFx Web パーツのサンプル。</span><span class="sxs-lookup"><span data-stu-id="2bfcf-163">SPFx web part samples for tabs, channels, and groups.</span></span> | [<span data-ttu-id="2bfcf-164">View</span><span class="sxs-lookup"><span data-stu-id="2bfcf-164">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="more-information"></a><span data-ttu-id="2bfcf-165">詳細情報</span><span class="sxs-lookup"><span data-stu-id="2bfcf-165">More information</span></span>

- [<span data-ttu-id="2bfcf-166">SharePoint Framework を使用した Microsoft Teams タブの作成: チュートリアル</span><span class="sxs-lookup"><span data-stu-id="2bfcf-166">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [<span data-ttu-id="2bfcf-167">SharePoint Online での Single Part App Pages の使用</span><span class="sxs-lookup"><span data-stu-id="2bfcf-167">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
