---
title: SharePoint に [Teams] タブを追加する
author: surbhigupta
description: コード サンプルを使用して、既存の [Teams] タブを SharePoint Framework Web パーツとして SharePoint に展開する方法について説明します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 076cf027e2696848319fc0beb7ae69c3633b8dc4
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499196"
---
# <a name="add-teams-tab-to-sharepoint"></a>SharePoint に [Teams] タブを追加する

SPFx Web パーツとして SharePoint に Microsoft Teams タブを追加することで、Microsoft Teams と SharePoint の間のリッチなインテグレーション エクスペリエンスを得ることができます。 このドキュメントでは、Microsoft Teams サンプル アプリからタブを取得し、SharePoint で使用する方法について説明します。

## <a name="rich-integration-between-teams-and-sharepoint"></a>Teams と SharePoint のリッチなインテグレーション

11 月リリース版の Teams と SharePoint Framework v.1.7 で、開発者は次の 2 つの強力な機能を備えます:

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
                        <h3>SharePoint における Teams Tabs</h3>
                        <p>Teams アプリを SharePoint に導入することで、SharePoint でリッチなアプリ エクスペリエンスを作成します (この記事)。</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li>
    <a href="/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/SharePoint-web-part-exposed-as-a-Tab-in-Microsoft-Teams.png" alt="web-part-exposed-as-a-tab" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>SharePoint Framework in Teams</h3>
                        <p>SharePoint Web パーツを Teams に導入し、SharePoint でホスティングを管理できるようにします。</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>SharePoint における Teams タブ

With SharePoint Framework v.1.7, you can host your Teams tabs in SharePoint. As tabs hosted in SharePoint get a similar **full page** experience, exposing all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework in Teams

SharePoint Frameworkを使用して Teams タブを実装することもできます。 SharePoint Framework Web パーツは、Azure などの外部サービスを必要とせずに、SharePoint 内でホストされます。 SharePoint 開発者の場合、これにより Teams タブの開発プロセスが大幅に簡素化されます。 SharePoint Framework in Teams の詳細情報については、「[Teams で SharePoint Framework を使用する方法](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)」を参照してください。

## <a name="introduction"></a>はじめに

ここで使用されるタブは、必要な統合作業に重点を置くために、Azure で既にホストされています。

使用されているサンプル アプリは Talent Management アプリケーションです。 チーム内のオープン ポジションの候補者の採用プロセスを管理します。 サンプル Teams アプリをビルドし、Teams に導入します。 実際のタレント管理アプリケーションを作成しないでください。

### <a name="benefits-of-this-approach"></a>このアプローチの利点

* 既存の Teams タブで SharePoint ユーザーにリーチします。
* アプリ マニフェストを SharePoint アプリ カタログに直接アップロードします。 [Teams アプリケーション パッケージ](~/concepts/build-and-test/apps-package.md)は、SharePoint でサポートされるようになりました。
* ユーザーは、他の SharePoint Web パーツと同様にページ上のタブを構成します。
* タブは、Teams 内で実行されている場合と同じ様に、その [context](~/tabs/how-to/access-teams-context.md) にアクセスできます。

Teams タブを SharePoint に追加するには、次の手順に従って、Teams タブを SharePoint に追加します:

## <a name="1-test-the-sample-app"></a>1. サンプル アプリをテストします。

[サンプル アプリ マニフェスト](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)をダウンロードします。

1. Microsoft Teams を開きます。
1. サイド タブの左下にある **Appstore** アイコンを選択します。
1. 左下にある **カスタム アプリのアップロード** を選択します。 次の図は、対応する画面を示しています:  

    ![カスタム アプリのアップロード](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. アップロードするファイルは、**ダウンロード** フォルダーにあります。 TalentMgmt-Azure.zipと呼ばれます。 次の図は、対応する画面を示しています:

    ![TalentMgmt in Azure](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. 人材管理アプリのインストール画面または同意画面を見ることができます。 インストールするチームを選択します。
1. **インストール** を選択し、アプリの実験を開始します。

## <a name="2-use-teams-tab-in-sharepoint"></a>2. SharePointの Teams タブを使用する

1. `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` にアクセスして、Teams アプリ パッケージを SharePoint アプリ カタログにアップロードしてデプロイします。 たとえば、「 `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 」のように入力します。

1. プロンプトで促されたら、**組織内のすべてのサイトでこのソリューションを使用できるようにする** を有効にします。
次の図は、対応する画面を示しています:

   ![SharePoint ビューのタブ](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. In your site, create a new page by selecting the gear button at the upper right and then  select **Add a page**.
The following image displays the corresponding screen:

   ![SharePoint ビュー](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. SharePoint ページ作成エクスペリエンスを確認できます。 ページに **My Teams タブ** という名前を付けます。

1. `+` ボタンを選択して Web パーツ ツールボックスを開き、**Contoso HR** という名前の Teams タブを選択します。 Web パーツはアルファベット順に並べ替えられます。 長いリストの場合は、検索バーを使用して検索できます。 これにより、Teams タブを含む Web パーツがキャンバスに作成されます。次の図は、タブ ビューを示します:

   ![タブ ビュー](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. 編集が完了したら、**Publish** ボタンを選択します。

1. 左側のナビゲーション バーでページを素早く参照するには、**ナビゲーションにページを追加** を選択します。
次の図は、SharePoint のタブを表示しています。

   ![SharePoint におけるタブを示す画像](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. SharePoint でアプリ ページを探索する

ページが公開されたら、[Teams アプリをSharePoint 内でより完全なエクスペリエンスに転換する](/sharepoint/dev/spfx/web-parts/single-part-app-pages) を探索できます。 これにより、Teams タブの全画面エクスペリエンスとともに通常の SharePoint ページ レイアウトを表示しながら、現在のページをアプリ ページに変換します。

次の図は、SharePoint の Teams アプリの完全なエクスペリエンスを示しています。![SharePoint の Tabs を示す画像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **SPFx** |
|-----------------|-----------------|----------|
| SPFx Web パーツ | タブ、チャンネル、グループの SPFx Web パーツ サンプル。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>関連項目

* [SharePoint Framework を使用した Microsoft Teams タブの作成: チュートリアル](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
* [SharePoint Online での Single Part App Pages の使用](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
