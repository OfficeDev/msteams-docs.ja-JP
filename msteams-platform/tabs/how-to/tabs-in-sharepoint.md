---
title: SharePoint に [Teams] タブを追加する
author: laujan
description: SharePoint Framework Web パーツとして既存の Teams タブを SharePoint に展開する方法。
keywords: teams タブ sharepoint framework 開発
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a2ea6c470f094a9d7b8617a210559e911f5f81c9
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058482"
---
# <a name="add-teams-tab-to-sharepoint"></a><span data-ttu-id="3de9c-104">SharePoint に [Teams] タブを追加する</span><span class="sxs-lookup"><span data-stu-id="3de9c-104">Add Teams tab to SharePoint</span></span> 

<span data-ttu-id="3de9c-105">SharePoint の [Microsoft Teams] タブを SPFx Web パーツとして追加すると、Microsoft Teams と SharePoint の豊富な統合エクスペリエンスを得られる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3de9c-105">You can get a rich integration experience between Microsoft Teams and SharePoint by adding a Microsoft Teams tab in SharePoint as an SPFx web part.</span></span> <span data-ttu-id="3de9c-106">このドキュメントでは、Microsoft Teams サンプル アプリからタブを取り出し、SharePoint で使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-106">This document guides you on how you to take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> 

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="3de9c-107">Teams と SharePoint の豊富な統合</span><span class="sxs-lookup"><span data-stu-id="3de9c-107">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="3de9c-108">Teams と SharePoint Framework v.1.7 の 11 月リリースでは、開発者には次の 2 つの強力な機能があります。</span><span class="sxs-lookup"><span data-stu-id="3de9c-108">With the November release of Teams and SharePoint Framework v.1.7, developers have two powerful capabilities:</span></span>

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
                        <h3><span data-ttu-id="3de9c-109">SharePoint の Teams タブ</span><span class="sxs-lookup"><span data-stu-id="3de9c-109">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="3de9c-110">Teams アプリを Sharepoint に取り込み、SharePoint で豊富なアプリ エクスペリエンスを作成します (この記事)。</span><span class="sxs-lookup"><span data-stu-id="3de9c-110">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
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
                        <h3><span data-ttu-id="3de9c-111">Teams の SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="3de9c-111">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="3de9c-112">SharePoint Web パーツを Teams に持ち込み、SharePoint でホスティングを管理できます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-112">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="3de9c-113">SharePoint の Teams タブ</span><span class="sxs-lookup"><span data-stu-id="3de9c-113">Teams tabs in SharePoint</span></span>

<span data-ttu-id="3de9c-114">SharePoint Framework v.1.7 では、SharePoint で Teams タブをホストできます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-114">With SharePoint Framework v.1.7, you can host your Teams tabs in SharePoint.</span></span> <span data-ttu-id="3de9c-115">SharePoint でホストされているタブは、同様のフル ページ エクスペリエンスを取得し、SharePoint サイトのコンテキストとなじみを維持しながら Teams タブのすべての機能を公開します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-115">As tabs hosted in SharePoint get a similar **full page** experience, exposing all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="3de9c-116">Teams の SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="3de9c-116">SharePoint Framework in Teams</span></span>

<span data-ttu-id="3de9c-117">SharePoint Framework を使用して Microsoft Teams タブを実装することもできます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-117">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="3de9c-118">SharePoint Framework Web パーツは、Azure などの外部サービスを必要とせずに SharePoint 内でホストされます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-118">SharePoint Framework web parts are hosted within SharePoint without any need for external services, such as Azure.</span></span> <span data-ttu-id="3de9c-119">SharePoint 開発者の場合、Teams タブの開発プロセスが大幅に簡略化されます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-119">For SharePoint developers, this significantly simplifies the development process for Teams tabs.</span></span> <span data-ttu-id="3de9c-120">Teams の SharePoint Framework の詳細については、「Teams で SharePoint Framework を使用する方法 [」を参照してください。](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span><span class="sxs-lookup"><span data-stu-id="3de9c-120">For more information on SharePoint Framework in Teams, see [how to use the SharePoint Framework in Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span></span>

## <a name="introduction"></a><span data-ttu-id="3de9c-121">概要</span><span class="sxs-lookup"><span data-stu-id="3de9c-121">Introduction</span></span>

<span data-ttu-id="3de9c-122">ここで使用するタブは、必要な統合作業に焦点を当て、Azure で既にホストされています。</span><span class="sxs-lookup"><span data-stu-id="3de9c-122">The tab used here is already hosted on Azure, to focus on the required integration work.</span></span>

<span data-ttu-id="3de9c-123">使用されているサンプル アプリは、Talent Management アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="3de9c-123">The sample app that is being used is a Talent Management application.</span></span> <span data-ttu-id="3de9c-124">チーム内のオープンポジションの候補者の採用プロセスを管理します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-124">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="3de9c-125">サンプルの Teams アプリをビルドし、Teams に読み込む。</span><span class="sxs-lookup"><span data-stu-id="3de9c-125">Build a sample Teams app and load it into Teams.</span></span> <span data-ttu-id="3de9c-126">実際の人材管理アプリケーションを作成しない。</span><span class="sxs-lookup"><span data-stu-id="3de9c-126">Do not create a real talent management application.</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="3de9c-127">このアプローチの利点</span><span class="sxs-lookup"><span data-stu-id="3de9c-127">Benefits of this approach</span></span>

* <span data-ttu-id="3de9c-128">既存の Teams タブを使用して SharePoint ユーザーにリーチします。</span><span class="sxs-lookup"><span data-stu-id="3de9c-128">Reach SharePoint users with your existing Teams tab.</span></span>
* <span data-ttu-id="3de9c-129">アプリ マニフェストを SharePoint アプリ カタログに直接アップロードします。</span><span class="sxs-lookup"><span data-stu-id="3de9c-129">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="3de9c-130">[Teams アプリケーション パッケージ](~/concepts/build-and-test/apps-package.md) は SharePoint でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3de9c-130">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint.</span></span>
* <span data-ttu-id="3de9c-131">ユーザーは、他の SharePoint Web パーツと同じ方法でページのタブを構成します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-131">The users configure the tab on a page just like any other SharePoint web part.</span></span>
* <span data-ttu-id="3de9c-132">タブは、Teams 内で [実行](~/tabs/how-to/access-teams-context.md) する場合と同じように、そのコンテキストにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-132">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) sameas it can, when running inside Teams.</span></span>

<span data-ttu-id="3de9c-133">**SharePoint に Teams タブを追加するには**</span><span class="sxs-lookup"><span data-stu-id="3de9c-133">**To add Teams tab to SharePoint**</span></span>

<span data-ttu-id="3de9c-134">Teams タブを SharePoint に追加するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-134">Perform the following steps to add Teams tab to SharePoint:</span></span>

## <a name="1-test-the-sample-app"></a><span data-ttu-id="3de9c-135">1. サンプル アプリをテストする</span><span class="sxs-lookup"><span data-stu-id="3de9c-135">1. Test the sample app</span></span>

<span data-ttu-id="3de9c-136">サンプル アプリ [マニフェストをダウンロードします](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)。</span><span class="sxs-lookup"><span data-stu-id="3de9c-136">Download the [sample app manifest](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

1. <span data-ttu-id="3de9c-137">Microsoft Teams を開きます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-137">Open Microsoft Teams.</span></span>
1. <span data-ttu-id="3de9c-138">サイド タブ **の左下にある** [アプリストア] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-138">Select the **Appstore** icon at the lower left of side tab.</span></span>
1. <span data-ttu-id="3de9c-139">左下 **の [カスタム アプリのアップロード** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-139">Select **Upload a custom app** at the lower left.</span></span> <span data-ttu-id="3de9c-140">次の図は、対応する画面を表示します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-140">The following image displays the corresponding screen:</span></span>  

    ![カスタム アプリをアップロードする](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. <span data-ttu-id="3de9c-142">アップロードするファイルは、[ダウンロード] フォルダー **にあります** 。</span><span class="sxs-lookup"><span data-stu-id="3de9c-142">The file to upload is located in your **Downloads** folder.</span></span> <span data-ttu-id="3de9c-143">このメソッドは、TalentMgmt-Azure.zip。</span><span class="sxs-lookup"><span data-stu-id="3de9c-143">It is called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="3de9c-144">次の図は、対応する画面を表示します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-144">The following image displays the corresponding screen:</span></span>
 
    ![Azure の TalentMgmt](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. <span data-ttu-id="3de9c-146">タレント管理アプリのインストール画面または同意画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-146">You can see the install or consent screen for the talent management app.</span></span> <span data-ttu-id="3de9c-147">インストールするチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-147">Select the team you want to install.</span></span> 
1. <span data-ttu-id="3de9c-148">[インストール **] を** 選択し、アプリの実験を開始します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-148">Select the **Install** and start experimenting with the app.</span></span>

## <a name="2-use-teams-tab-in-sharepoint"></a><span data-ttu-id="3de9c-149">2. SharePoint の [Teams] タブを使用する</span><span class="sxs-lookup"><span data-stu-id="3de9c-149">2. Use Teams tab in SharePoint</span></span>

1. <span data-ttu-id="3de9c-150">アクセスして、Teams アプリ パッケージを SharePoint アプリ カタログにアップロードして展開します `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。</span><span class="sxs-lookup"><span data-stu-id="3de9c-150">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span> <span data-ttu-id="3de9c-151">たとえば、`https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` などです。</span><span class="sxs-lookup"><span data-stu-id="3de9c-151">For example, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

1. <span data-ttu-id="3de9c-152">メッセージが表示されたら、[ **このソリューションを組織内のすべてのサイトで使用できる] を有効にします**。</span><span class="sxs-lookup"><span data-stu-id="3de9c-152">When prompted, enable **Make this solution available to all sites in the organization**.</span></span>
<span data-ttu-id="3de9c-153">次の図は、対応する画面を表示します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-153">The following image displays the corresponding screen:</span></span>

   ![Sharepoint ビューのタブ](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. <span data-ttu-id="3de9c-155">サイトで、右上の歯車ボタンを選択して新しいページを作成し、[ページの追加 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3de9c-155">In your site, create a new page by selecting the gear button at the upper right and then  select **Add a page**.</span></span>
<span data-ttu-id="3de9c-156">次の図は、対応する画面を表示します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-156">The following image displays the corresponding screen:</span></span>

   ![Sharepoint ビュー](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. <span data-ttu-id="3de9c-158">SharePoint ページの作成エクスペリエンスを確認できます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-158">You can see the SharePoint pages authoring experience.</span></span> <span data-ttu-id="3de9c-159">ページの名前を **[My Teams] タブに設定します**。</span><span class="sxs-lookup"><span data-stu-id="3de9c-159">Name your page as **My Teams Tab**.</span></span>

1. <span data-ttu-id="3de9c-160">ボタンを押して Web パーツ ツールボックスを開 `+` き、Contoso HR という名前の Teams タブ **を選択します**。</span><span class="sxs-lookup"><span data-stu-id="3de9c-160">Open the web part toolbox by pressing the `+` button, and select your Teams Tab, named **Contoso HR**.</span></span> <span data-ttu-id="3de9c-161">Web パーツはアルファベット順に並べ替えされます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-161">Web parts are sorted alphabetically.</span></span> <span data-ttu-id="3de9c-162">長いリストの場合は、検索バーを使用して検索できます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-162">If it is a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="3de9c-163">これにより、Teams タブを含む Web パーツがキャンバスに作成されます。次の図は、タブ ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-163">This creates a web part in the canvas that contains your Teams tab. The following image displays the tab view:</span></span>

   ![タブ ビュー](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. <span data-ttu-id="3de9c-165">編集が **完了したら** 、[発行] ボタンを押します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-165">Press the **Publish** button after you finish  editing.</span></span>

1. <span data-ttu-id="3de9c-166">[ **ナビゲーションにページを追加する** ] を選択して、左側のナビゲーション バーでページを簡単に参照できます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-166">Select **Add page to navigation** to have a quick reference to your page in the left navigation bar.</span></span> <span data-ttu-id="3de9c-167">次の図は、Sharepoint のタブを表示します。</span><span class="sxs-lookup"><span data-stu-id="3de9c-167">The following image displays the tab in Sharepoint:</span></span> 

   ![Sharepoint イメージのタブ](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="3de9c-169">3. SharePoint でアプリ ページを確認する</span><span class="sxs-lookup"><span data-stu-id="3de9c-169">3. Explore App Pages in SharePoint</span></span>

<span data-ttu-id="3de9c-170">ページが公開された後、Teams アプリを SharePoint 内のより完全 [なエクスペリエンスに変える方法について説明します](/sharepoint/dev/spfx/web-parts/single-part-app-pages)。</span><span class="sxs-lookup"><span data-stu-id="3de9c-170">After your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="3de9c-171">これにより、現在のページがアプリ ページに変換されます。通常の SharePoint ページ レイアウトと Teams タブの完全なページ エクスペリエンスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3de9c-171">This converts the current page into an App Page, showing the normal SharePoint page layout with a full page experience for the Teams tab.</span></span> 

<span data-ttu-id="3de9c-172">次の図は、Sharepoint での Teams アプリの完全なエクスペリエンスを ![ 表示します。](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span><span class="sxs-lookup"><span data-stu-id="3de9c-172">The following image displays the complete experience of Teams app in Sharepoint: ![Image of Tabs in Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="3de9c-173">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="3de9c-173">Code sample</span></span>
| <span data-ttu-id="3de9c-174">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="3de9c-174">**Sample name**</span></span> | <span data-ttu-id="3de9c-175">**説明**</span><span class="sxs-lookup"><span data-stu-id="3de9c-175">**Description**</span></span> | <span data-ttu-id="3de9c-176">**SPFx**</span><span class="sxs-lookup"><span data-stu-id="3de9c-176">**SPFx**</span></span> |
|-----------------|-----------------|----------|
| <span data-ttu-id="3de9c-177">SPFx Web パーツ</span><span class="sxs-lookup"><span data-stu-id="3de9c-177">SPFx web part</span></span> | <span data-ttu-id="3de9c-178">SPFx Web パーツのタブ、チャネル、およびグループのサンプル。</span><span class="sxs-lookup"><span data-stu-id="3de9c-178">SPFx web part samples for tabs, channels, and groups.</span></span> | [<span data-ttu-id="3de9c-179">View</span><span class="sxs-lookup"><span data-stu-id="3de9c-179">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a><span data-ttu-id="3de9c-180">関連項目</span><span class="sxs-lookup"><span data-stu-id="3de9c-180">See also</span></span>

- [<span data-ttu-id="3de9c-181">SharePoint Framework を使用した Microsoft Teams タブの作成: チュートリアル</span><span class="sxs-lookup"><span data-stu-id="3de9c-181">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

- [<span data-ttu-id="3de9c-182">SharePoint Online での Single Part App Pages の使用</span><span class="sxs-lookup"><span data-stu-id="3de9c-182">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

- [<span data-ttu-id="3de9c-183">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="3de9c-183">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
