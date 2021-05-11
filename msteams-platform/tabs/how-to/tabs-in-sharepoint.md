---
title: SharePoint に [Teams] タブを追加する
author: laujan
description: 既存の [web パーツ] タブTeams、SharePoint Web パーツSharePoint Framework展開する方法。
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
# <a name="add-teams-tab-to-sharepoint"></a><span data-ttu-id="42685-104">SharePoint に [Teams] タブを追加する</span><span class="sxs-lookup"><span data-stu-id="42685-104">Add Teams tab to SharePoint</span></span> 

<span data-ttu-id="42685-105">Microsoft Teams と SharePoint の間の豊富な統合エクスペリエンスを得るには、Microsoft Teams タブを SharePoint web パーツSPFx追加します。</span><span class="sxs-lookup"><span data-stu-id="42685-105">You can get a rich integration experience between Microsoft Teams and SharePoint by adding a Microsoft Teams tab in SharePoint as an SPFx web part.</span></span> <span data-ttu-id="42685-106">このドキュメントでは、サンプル アプリからタブを取り出し、Microsoft Teamsで使用する方法SharePoint。</span><span class="sxs-lookup"><span data-stu-id="42685-106">This document guides you on how you to take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> 

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="42685-107">ユーザーとユーザーの間Teams統合SharePoint</span><span class="sxs-lookup"><span data-stu-id="42685-107">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="42685-108">11 月リリースの Teams v.1.7 SharePoint Framework開発者には、次の 2 つの強力な機能があります。</span><span class="sxs-lookup"><span data-stu-id="42685-108">With the November release of Teams and SharePoint Framework v.1.7, developers have two powerful capabilities:</span></span>

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
                        <h3><span data-ttu-id="42685-109">Teams[タブ] SharePoint</span><span class="sxs-lookup"><span data-stu-id="42685-109">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="42685-110">アプリを Sharepoint にSharePointして、Teams豊富なアプリ エクスペリエンスを作成します (この記事)。</span><span class="sxs-lookup"><span data-stu-id="42685-110">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
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
                        <h3><span data-ttu-id="42685-111">SharePoint FrameworkのTeams</span><span class="sxs-lookup"><span data-stu-id="42685-111">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="42685-112">Web パーツをSharePointして、TeamsをSharePoint管理できます。</span><span class="sxs-lookup"><span data-stu-id="42685-112">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="42685-113">TeamsタブのSharePoint</span><span class="sxs-lookup"><span data-stu-id="42685-113">Teams tabs in SharePoint</span></span>

<span data-ttu-id="42685-114">SharePoint Framework v.1.7 では、TeamsタブをホストSharePoint。</span><span class="sxs-lookup"><span data-stu-id="42685-114">With SharePoint Framework v.1.7, you can host your Teams tabs in SharePoint.</span></span> <span data-ttu-id="42685-115">SharePointでホストされているタブと同様のフル ページエクスペリエンスが得られているので、Teams タブのすべての機能が公開され、SharePoint サイトのコンテキストと親しみSharePointされます。</span><span class="sxs-lookup"><span data-stu-id="42685-115">As tabs hosted in SharePoint get a similar **full page** experience, exposing all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="42685-116">SharePoint FrameworkのTeams</span><span class="sxs-lookup"><span data-stu-id="42685-116">SharePoint Framework in Teams</span></span>

<span data-ttu-id="42685-117">また、タブを使用してMicrosoft Teamsを実装SharePoint Framework。</span><span class="sxs-lookup"><span data-stu-id="42685-117">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="42685-118">SharePoint Framework Web パーツは、Azure などのSharePointサービスを必要とせずに、Web パーツ内でホストされます。</span><span class="sxs-lookup"><span data-stu-id="42685-118">SharePoint Framework web parts are hosted within SharePoint without any need for external services, such as Azure.</span></span> <span data-ttu-id="42685-119">開発者SharePoint、これにより、タブの開発プロセスが大幅にTeamsされます。</span><span class="sxs-lookup"><span data-stu-id="42685-119">For SharePoint developers, this significantly simplifies the development process for Teams tabs.</span></span> <span data-ttu-id="42685-120">詳細については、SharePoint FrameworkのTeamsを使用する方法をSharePoint Framework[をTeams。](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span><span class="sxs-lookup"><span data-stu-id="42685-120">For more information on SharePoint Framework in Teams, see [how to use the SharePoint Framework in Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span></span>

## <a name="introduction"></a><span data-ttu-id="42685-121">はじめに</span><span class="sxs-lookup"><span data-stu-id="42685-121">Introduction</span></span>

<span data-ttu-id="42685-122">ここで使用するタブは、必要な統合作業に焦点を当て、Azure で既にホストされています。</span><span class="sxs-lookup"><span data-stu-id="42685-122">The tab used here is already hosted on Azure, to focus on the required integration work.</span></span>

<span data-ttu-id="42685-123">使用されているサンプル アプリは、Talent Management アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="42685-123">The sample app that is being used is a Talent Management application.</span></span> <span data-ttu-id="42685-124">チーム内のオープンポジションの候補者の採用プロセスを管理します。</span><span class="sxs-lookup"><span data-stu-id="42685-124">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="42685-125">アプリのサンプル をTeamsし、アプリに読み込Teams。</span><span class="sxs-lookup"><span data-stu-id="42685-125">Build a sample Teams app and load it into Teams.</span></span> <span data-ttu-id="42685-126">実際の人材管理アプリケーションを作成しない。</span><span class="sxs-lookup"><span data-stu-id="42685-126">Do not create a real talent management application.</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="42685-127">このアプローチの利点</span><span class="sxs-lookup"><span data-stu-id="42685-127">Benefits of this approach</span></span>

* <span data-ttu-id="42685-128">既存SharePointタブを使用して、ユーザーにTeamsします。</span><span class="sxs-lookup"><span data-stu-id="42685-128">Reach SharePoint users with your existing Teams tab.</span></span>
* <span data-ttu-id="42685-129">アップロードマニフェストをアプリ カタログに直接SharePointする。</span><span class="sxs-lookup"><span data-stu-id="42685-129">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="42685-130">[Teamsアプリケーション パッケージ](~/concepts/build-and-test/apps-package.md)は、現在、アプリケーション パッケージでSharePoint。</span><span class="sxs-lookup"><span data-stu-id="42685-130">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint.</span></span>
* <span data-ttu-id="42685-131">ユーザーは、他の Web パーツと同様にページSharePoint構成します。</span><span class="sxs-lookup"><span data-stu-id="42685-131">The users configure the tab on a page just like any other SharePoint web part.</span></span>
* <span data-ttu-id="42685-132">タブは、[タブ内で](~/tabs/how-to/access-teams-context.md)実行する場合と同じように、そのコンテキストにTeams。</span><span class="sxs-lookup"><span data-stu-id="42685-132">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) sameas it can, when running inside Teams.</span></span>

<span data-ttu-id="42685-133">**タブをTeamsするには、次SharePoint**</span><span class="sxs-lookup"><span data-stu-id="42685-133">**To add Teams tab to SharePoint**</span></span>

<span data-ttu-id="42685-134">次の手順を実行して、[Teams] タブを追加SharePoint。</span><span class="sxs-lookup"><span data-stu-id="42685-134">Perform the following steps to add Teams tab to SharePoint:</span></span>

## <a name="1-test-the-sample-app"></a><span data-ttu-id="42685-135">1. サンプル アプリをテストする</span><span class="sxs-lookup"><span data-stu-id="42685-135">1. Test the sample app</span></span>

<span data-ttu-id="42685-136">サンプル アプリ [マニフェストをダウンロードします](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)。</span><span class="sxs-lookup"><span data-stu-id="42685-136">Download the [sample app manifest](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

1. <span data-ttu-id="42685-137">Microsoft Teams を開きます。</span><span class="sxs-lookup"><span data-stu-id="42685-137">Open Microsoft Teams.</span></span>
1. <span data-ttu-id="42685-138">サイド タブ **の左下にある** [アプリストア] アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="42685-138">Select the **Appstore** icon at the lower left of side tab.</span></span>
1. <span data-ttu-id="42685-139">左下 **アップロードカスタム アプリを選択** します。</span><span class="sxs-lookup"><span data-stu-id="42685-139">Select **Upload a custom app** at the lower left.</span></span> <span data-ttu-id="42685-140">次の図は、対応する画面を表示します。</span><span class="sxs-lookup"><span data-stu-id="42685-140">The following image displays the corresponding screen:</span></span>  

    ![カスタム アプリをアップロードする](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. <span data-ttu-id="42685-142">アップロードするファイルは、[ダウンロード] フォルダー **にあります** 。</span><span class="sxs-lookup"><span data-stu-id="42685-142">The file to upload is located in your **Downloads** folder.</span></span> <span data-ttu-id="42685-143">このメソッドは、TalentMgmt-Azure.zip。</span><span class="sxs-lookup"><span data-stu-id="42685-143">It is called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="42685-144">次の図は、対応する画面を表示します。</span><span class="sxs-lookup"><span data-stu-id="42685-144">The following image displays the corresponding screen:</span></span>
 
    ![Azure の TalentMgmt](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. <span data-ttu-id="42685-146">タレント管理アプリのインストール画面または同意画面が表示されます。</span><span class="sxs-lookup"><span data-stu-id="42685-146">You can see the install or consent screen for the talent management app.</span></span> <span data-ttu-id="42685-147">インストールするチームを選択します。</span><span class="sxs-lookup"><span data-stu-id="42685-147">Select the team you want to install.</span></span> 
1. <span data-ttu-id="42685-148">[インストール **] を** 選択し、アプリの実験を開始します。</span><span class="sxs-lookup"><span data-stu-id="42685-148">Select the **Install** and start experimenting with the app.</span></span>

## <a name="2-use-teams-tab-in-sharepoint"></a><span data-ttu-id="42685-149">2. [Teams] タブを使用SharePoint</span><span class="sxs-lookup"><span data-stu-id="42685-149">2. Use Teams tab in SharePoint</span></span>

1. <span data-ttu-id="42685-150">アップロードアクセスして、Teamsアプリ パッケージをアプリ SharePointに展開します `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。</span><span class="sxs-lookup"><span data-stu-id="42685-150">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span> <span data-ttu-id="42685-151">たとえば、`https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` などです。</span><span class="sxs-lookup"><span data-stu-id="42685-151">For example, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

1. <span data-ttu-id="42685-152">メッセージが表示されたら、[ **このソリューションを組織内のすべてのサイトで使用できる] を有効にします**。</span><span class="sxs-lookup"><span data-stu-id="42685-152">When prompted, enable **Make this solution available to all sites in the organization**.</span></span>
<span data-ttu-id="42685-153">次の図は、対応する画面を表示します。</span><span class="sxs-lookup"><span data-stu-id="42685-153">The following image displays the corresponding screen:</span></span>

   ![Sharepoint ビューのタブ](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. <span data-ttu-id="42685-155">サイトで、右上の歯車ボタンを選択して新しいページを作成し、[ページの追加 **] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="42685-155">In your site, create a new page by selecting the gear button at the upper right and then  select **Add a page**.</span></span>
<span data-ttu-id="42685-156">次の図は、対応する画面を表示します。</span><span class="sxs-lookup"><span data-stu-id="42685-156">The following image displays the corresponding screen:</span></span>

   ![Sharepoint ビュー](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. <span data-ttu-id="42685-158">このページの作成SharePoint確認できます。</span><span class="sxs-lookup"><span data-stu-id="42685-158">You can see the SharePoint pages authoring experience.</span></span> <span data-ttu-id="42685-159">ページに [マイ ページ]**タブTeamsします**。</span><span class="sxs-lookup"><span data-stu-id="42685-159">Name your page as **My Teams Tab**.</span></span>

1. <span data-ttu-id="42685-160">ボタンを押して Web パーツ ツールボックスを開き、Contoso HR という名前Teams `+` タブを **選択します**。</span><span class="sxs-lookup"><span data-stu-id="42685-160">Open the web part toolbox by pressing the `+` button, and select your Teams Tab, named **Contoso HR**.</span></span> <span data-ttu-id="42685-161">Web パーツはアルファベット順に並べ替えされます。</span><span class="sxs-lookup"><span data-stu-id="42685-161">Web parts are sorted alphabetically.</span></span> <span data-ttu-id="42685-162">長いリストの場合は、検索バーを使用して検索できます。</span><span class="sxs-lookup"><span data-stu-id="42685-162">If it is a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="42685-163">これにより、キャンバスに Web パーツが作成されます。このタブには、Teamsがあります。次の図は、タブ ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="42685-163">This creates a web part in the canvas that contains your Teams tab. The following image displays the tab view:</span></span>

   ![タブ ビュー](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. <span data-ttu-id="42685-165">編集が **完了したら** 、[発行] ボタンを押します。</span><span class="sxs-lookup"><span data-stu-id="42685-165">Press the **Publish** button after you finish  editing.</span></span>

1. <span data-ttu-id="42685-166">[ **ナビゲーションにページを追加する** ] を選択して、左側のナビゲーション バーでページを簡単に参照できます。</span><span class="sxs-lookup"><span data-stu-id="42685-166">Select **Add page to navigation** to have a quick reference to your page in the left navigation bar.</span></span> <span data-ttu-id="42685-167">次の図は、Sharepoint のタブを表示します。</span><span class="sxs-lookup"><span data-stu-id="42685-167">The following image displays the tab in Sharepoint:</span></span> 

   ![Sharepoint イメージのタブ](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="42685-169">3. アプリ ページの SharePoint詳細</span><span class="sxs-lookup"><span data-stu-id="42685-169">3. Explore App Pages in SharePoint</span></span>

<span data-ttu-id="42685-170">ページが公開された後、アプリをアプリ内でTeams完全なエクスペリエンスに変える[方法をSharePoint。](/sharepoint/dev/spfx/web-parts/single-part-app-pages)</span><span class="sxs-lookup"><span data-stu-id="42685-170">After your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="42685-171">これにより、現在のページがアプリ ページに変換されます。通常のページ レイアウトSharePointページ レイアウトを表示し、[ページ] タブのフル ページ エクスペリエンスTeamsします。</span><span class="sxs-lookup"><span data-stu-id="42685-171">This converts the current page into an App Page, showing the normal SharePoint page layout with a full page experience for the Teams tab.</span></span> 

<span data-ttu-id="42685-172">次の図は、Sharepoint でのアプリのTeamsエクスペリエンスを表示します。 ![](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span><span class="sxs-lookup"><span data-stu-id="42685-172">The following image displays the complete experience of Teams app in Sharepoint: ![Image of Tabs in Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="42685-173">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="42685-173">Code sample</span></span>
| <span data-ttu-id="42685-174">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="42685-174">**Sample name**</span></span> | <span data-ttu-id="42685-175">**説明**</span><span class="sxs-lookup"><span data-stu-id="42685-175">**Description**</span></span> | <span data-ttu-id="42685-176">**SPFx**</span><span class="sxs-lookup"><span data-stu-id="42685-176">**SPFx**</span></span> |
|-----------------|-----------------|----------|
| <span data-ttu-id="42685-177">SPFx Web パーツ</span><span class="sxs-lookup"><span data-stu-id="42685-177">SPFx web part</span></span> | <span data-ttu-id="42685-178">SPFx、チャネル、およびグループの Web パーツサンプルを作成します。</span><span class="sxs-lookup"><span data-stu-id="42685-178">SPFx web part samples for tabs, channels, and groups.</span></span> | [<span data-ttu-id="42685-179">View</span><span class="sxs-lookup"><span data-stu-id="42685-179">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a><span data-ttu-id="42685-180">関連項目</span><span class="sxs-lookup"><span data-stu-id="42685-180">See also</span></span>

- [<span data-ttu-id="42685-181">SharePoint Framework を使用した Microsoft Teams タブの作成: チュートリアル</span><span class="sxs-lookup"><span data-stu-id="42685-181">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

- [<span data-ttu-id="42685-182">SharePoint Online での Single Part App Pages の使用</span><span class="sxs-lookup"><span data-stu-id="42685-182">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

- [<span data-ttu-id="42685-183">Web アプリを統合する</span><span class="sxs-lookup"><span data-stu-id="42685-183">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
