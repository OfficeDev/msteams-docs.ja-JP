---
title: SharePoint に [Teams] タブを追加する
author: surbhigupta
description: コード サンプルを使用して、既存の [Teams] タブSharePoint web パーツSharePoint Framework展開する方法について説明します。
keywords: teams タブ sharepoint framework 開発
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: ea5f5cc90e1451ab65a31205f4c83137163a36cc
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399227"
---
# <a name="add-teams-tab-to-sharepoint"></a>SharePoint に [Teams] タブを追加する

Microsoft Teams と SharePoint の間で、Microsoft Teams タブを SharePoint web パーツとしてSPFxできます。 このドキュメントでは、サンプル アプリからタブを取り出し、Microsoft Teamsで使用する方法についてSharePoint。

## <a name="rich-integration-between-teams-and-sharepoint"></a>ユーザーとユーザーの間のTeams統合SharePoint

11 月リリースの Teams v.1.7 SharePoint Framework開発者には、次の 2 つの強力な機能があります。

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
                        <h3>TeamsタブのSharePoint</h3>
                        <p>アプリを新しいアプリにSharePointして、TeamsエクスペリエンスSharePoint作成します (この記事)。</p>
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
                        <h3>SharePoint FrameworkのTeams</h3>
                        <p>Web パーツをSharePointして、TeamsをSharePoint管理できます。</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>TeamsのタブSharePoint

SharePoint Framework v.1.7 では、TeamsタブをホストSharePoint。 SharePointでホストされているタブは、Teams タブのすべての機能を公開しながら、SharePoint サイトのコンテキストとなじみを維持しながら、同様のフル ページ エクスペリエンスを取得します。

### <a name="sharepoint-framework-in-teams"></a>SharePoint FrameworkのTeams

このタブを使用して、Microsoft TeamsタブをSharePoint Framework。 SharePoint Framework Web パーツは、Azure SharePoint外部サービスを必要とせずにホストされます。 開発者SharePoint、これにより、タブの開発プロセスが大幅Teamsになります。 詳細については、SharePoint FrameworkのTeamsを使用する方法をSharePoint Framework[をTeams。](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>はじめに

ここで使用するタブは、必要な統合作業に焦点を当て、Azure で既にホストされています。

使用されているサンプル アプリは、Talent Management アプリケーションです。 チーム内のオープンポジションの候補者の採用プロセスを管理します。 アプリのサンプル をTeamsし、アプリに読み込Teams。 実際の人材管理アプリケーションを作成しない。

### <a name="benefits-of-this-approach"></a>このアプローチの利点

* 既存SharePointタブを使用して、ユーザーにTeamsします。
* アップロードマニフェストをアプリ カタログに直接SharePoint変更します。 [Teamsアプリケーション パッケージ](~/concepts/build-and-test/apps-package.md)は、現在、アプリケーション パッケージでSharePoint。
* ユーザーは、他の Web パーツと同様にページSharePoint構成します。
* タブは、[タブ内で](~/tabs/how-to/access-teams-context.md)実行する場合と同じコンテキストにTeams。

タブを TeamsするにはSharePointを実行して、次の手順を実行して、[Teams] タブを追加SharePoint。

## <a name="1-test-the-sample-app"></a>1. サンプル アプリをテストする

サンプル アプリ [マニフェストをダウンロードします](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)。

1. Microsoft Teams を開きます。
1. サイド タブ **の左下にある** [アプリストア] アイコンを選択します。
1. 左下 **アップロードカスタム アプリを選択** します。 次の図は、対応する画面を表示します。  

    ![カスタム アプリをアップロードする](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. アップロードするファイルは、[ダウンロード] フォルダー **にあります** 。 このメソッドは、TalentMgmt-Azure.zip。 次の図は、対応する画面を表示します。

    ![Azure の TalentMgmt](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. タレント管理アプリのインストール画面または同意画面が表示されます。 インストールするチームを選択します。
1. [インストール **] を** 選択し、アプリの実験を開始します。

## <a name="2-use-teams-tab-in-sharepoint"></a>2. [Teams] タブを使用SharePoint

1. アップロードにアクセスして、Teamsアプリ パッケージをアプリ カタログにSharePointして展開します`https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`。 たとえば、「 `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 」のように入力します。

1. メッセージが表示されたら、[ **このソリューションを組織内のすべてのサイトで使用できます] を有効にします**。
次の図は、対応する画面を表示します。

   ![Sharepoint ビューのタブ](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. サイトで、右上の歯車ボタンを選択して新しいページを作成し、[ページの追加 **] を選択します**。
次の図は、対応する画面を表示します。

   ![Sharepoint ビュー](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. このページの作成SharePoint確認できます。 ページに [マイ ページ] **タブTeamsします**。

1. ボタンを選択して Web パーツ ツールボックスを開`+`き、Contoso HR という名前Teamsタブを **選択します**。 Web パーツはアルファベット順に並べ替えされます。 長いリストの場合は、検索バーを使用して検索できます。 これにより、キャンバスに Web パーツが作成されます。このタブには、Teamsがあります。次の図は、タブ ビューを表示します。

   ![タブ ビュー](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. 編集が **完了したら** 、[発行] ボタンを選択します。

1. [ **ナビゲーションにページを追加する** ] を選択して、左側のナビゲーション バーでページを簡単に参照できます。
次の図は、Sharepoint のタブを表示します。

   ![Sharepoint イメージのタブ](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. アプリ ページの SharePoint詳細

ページが公開された後は、アプリをTeamsの中で、より完全なエクスペリエンス[に変SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages)。 これにより、現在のページがアプリ ページに変換されます。通常のページ レイアウトSharePointページ レイアウトを表示し、[ページ] タブのフル ページ エクスペリエンスTeamsします。

次の図は、[Sharepoint のタブのイメージ] TeamsアプリSharePointエクスペリエンス![全体を表示します。](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **SPFx** |
|-----------------|-----------------|----------|
| SPFx Web パーツ | SPFx、チャネル、およびグループの Web パーツサンプルを作成します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>関連項目

* [SharePoint Framework を使用した Microsoft Teams タブの作成: チュートリアル](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
* [SharePoint Online での Single Part App Pages の使用](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
* [Web アプリを統合する](~/samples/integrate-web-apps-overview.md)
