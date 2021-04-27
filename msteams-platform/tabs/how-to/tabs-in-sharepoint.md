---
title: '[Teams] タブを SharePoint に追加する'
author: laujan
description: SharePoint Framework Web パーツとして既存の Teams タブを SharePoint に展開する方法。
keywords: teams タブ sharepoint framework 開発
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 08a4aef329d0e5e1d063f05959f0a589581c9c03
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020331"
---
# <a name="add-teams-tab-to-sharepoint"></a>[Teams] タブを SharePoint に追加する 

SharePoint の [Microsoft Teams] タブを SPFx Web パーツとして追加すると、Microsoft Teams と SharePoint の豊富な統合エクスペリエンスを得られる可能性があります。 このドキュメントでは、Microsoft Teams サンプル アプリからタブを取り出し、SharePoint で使用する方法について説明します。 

## <a name="rich-integration-between-teams-and-sharepoint"></a>Teams と SharePoint の豊富な統合

Teams と SharePoint Framework v.1.7 の 11 月リリースでは、開発者には次の 2 つの強力な機能があります。

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
                        <h3>SharePoint の Teams タブ</h3>
                        <p>Teams アプリを Sharepoint に取り込み、SharePoint で豊富なアプリ エクスペリエンスを作成します (この記事)。</p>
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
                        <h3>Teams の SharePoint Framework</h3>
                        <p>SharePoint Web パーツを Teams に持ち込み、SharePoint でホスティングを管理できます。</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>SharePoint の Teams タブ

SharePoint Framework v.1.7 では、SharePoint で Teams タブをホストできます。 SharePoint でホストされているタブは、同様のフル ページ エクスペリエンスを取得し、SharePoint サイトのコンテキストとなじみを維持しながら Teams タブのすべての機能を公開します。

### <a name="sharepoint-framework-in-teams"></a>Teams の SharePoint Framework

SharePoint Framework を使用して Microsoft Teams タブを実装することもできます。 SharePoint Framework Web パーツは、Azure などの外部サービスを必要とせずに SharePoint 内でホストされます。 SharePoint 開発者の場合、Teams タブの開発プロセスが大幅に簡略化されます。 Teams の SharePoint Framework の詳細については、「Teams で SharePoint Framework を使用する方法 [」を参照してください。](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>概要

ここで使用するタブは、必要な統合作業に焦点を当て、Azure で既にホストされています。

使用されているサンプル アプリは、Talent Management アプリケーションです。 チーム内のオープンポジションの候補者の採用プロセスを管理します。 サンプルの Teams アプリをビルドし、Teams に読み込む。 実際の人材管理アプリケーションを作成しない。

### <a name="benefits-of-this-approach"></a>このアプローチの利点

* 既存の Teams タブを使用して SharePoint ユーザーにリーチします。
* アプリ マニフェストを SharePoint アプリ カタログに直接アップロードします。 [Teams アプリケーション パッケージ](~/concepts/build-and-test/apps-package.md) は SharePoint でサポートされています。
* ユーザーは、他の SharePoint Web パーツと同じ方法でページのタブを構成します。
* タブは、Teams 内で [実行](~/tabs/how-to/access-teams-context.md) する場合と同じように、そのコンテキストにアクセスできます。

**SharePoint に Teams タブを追加するには**

Teams タブを SharePoint に追加するには、次の手順を実行します。

## <a name="1-test-the-sample-app"></a>1. サンプル アプリをテストする

サンプル アプリ [マニフェストをダウンロードします](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)。

1. Microsoft Teams を開きます。
1. サイド タブ **の左下にある** [アプリストア] アイコンを選択します。
1. 左下 **の [カスタム アプリのアップロード** ] を選択します。 次の図は、対応する画面を表示します。  

    ![カスタム アプリをアップロードする](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. アップロードするファイルは、[ダウンロード] フォルダー **にあります** 。 このメソッドは、TalentMgmt-Azure.zip。 次の図は、対応する画面を表示します。
 
    ![Azure の TalentMgmt](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. タレント管理アプリのインストール画面または同意画面が表示されます。 インストールするチームを選択します。 
1. [インストール **] を** 選択し、アプリの実験を開始します。

## <a name="2-use-teams-tab-in-sharepoint"></a>2. SharePoint の [Teams] タブを使用する

1. アクセスして、Teams アプリ パッケージを SharePoint アプリ カタログにアップロードして展開します `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。 たとえば、`https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` などです。

1. メッセージが表示されたら、[ **このソリューションを組織内のすべてのサイトで使用できる] を有効にします**。
次の図は、対応する画面を表示します。

   ![Sharepoint ビューのタブ](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. サイトで、右上の歯車ボタンを選択して新しいページを作成し、[ページの追加 **] を選択します**。
次の図は、対応する画面を表示します。

   ![Sharepoint ビュー](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. SharePoint ページの作成エクスペリエンスを確認できます。 ページの名前を **[My Teams] タブに設定します**。

1. ボタンを押して Web パーツ ツールボックスを開 `+` き、Contoso HR という名前の Teams タブ **を選択します**。 Web パーツはアルファベット順に並べ替えされます。 長いリストの場合は、検索バーを使用して検索できます。 これにより、Teams タブを含む Web パーツがキャンバスに作成されます。次の図は、タブ ビューを表示します。

   ![タブ ビュー](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. 編集が **完了したら** 、[発行] ボタンを押します。

1. [ **ナビゲーションにページを追加する** ] を選択して、左側のナビゲーション バーでページを簡単に参照できます。 次の図は、Sharepoint のタブを表示します。 

   ![Sharepoint イメージのタブ](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. SharePoint でアプリ ページを確認する

ページが公開された後、Teams アプリを SharePoint 内のより完全 [なエクスペリエンスに変える方法について説明します](/sharepoint/dev/spfx/web-parts/single-part-app-pages)。 これにより、現在のページがアプリ ページに変換されます。通常の SharePoint ページ レイアウトと Teams タブの完全なページ エクスペリエンスが表示されます。 

次の図は、Sharepoint での Teams アプリの完全なエクスペリエンスを ![ 表示します。](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>コード サンプル
| **サンプル名** | **説明** | **SPFx** |
|-----------------|-----------------|----------|
| SPFx Web パーツ | SPFx Web パーツのタブ、チャネル、およびグループのサンプル。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [SharePoint Framework を使用した Microsoft Teams タブの作成: チュートリアル](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

> [!div class="nextstepaction"]
> [SharePoint Online での Single Part App Pages の使用](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

> [!div class="nextstepaction"]
> [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
