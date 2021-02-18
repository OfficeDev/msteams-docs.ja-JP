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
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a>SharePoint の Microsoft Teams タブを SPFx Web パーツとして追加する

## <a name="rich-integration-between-teams-and-sharepoint"></a>Teams と SharePoint の豊富な統合

Teams と SharePoint Framework v の 11 月リリース 1.7、開発者には次の 2 つの強力な機能があります。

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
                        <p>Teams アプリを SharePoint に取り込み、SharePoint で豊富なアプリ エクスペリエンスを作成します (この記事)。</p>
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
                        <p>SharePoint Web パーツを Teams に持ち込み、SharePoint がホスティングを管理します。</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>SharePoint の Teams タブ

SharePoint Framework v.1.7 では、開発者が Teams タブを使用して SharePoint でホストする機能をサポートしています。 SharePoint でホストされているタブも同様の "ページ全体" エクスペリエンスを得て、SharePoint サイトのコンテキストと使い慣れたものにしながら Teams タブのすべての機能を公開します。

### <a name="sharepoint-framework-in-teams"></a>Teams の SharePoint Framework

SharePoint Framework を使用して Microsoft Teams タブを実装することもできます。 SharePoint 開発者の場合、SharePoint Framework Web パーツは Azure などの外部サービスを必要とせずに SharePoint 内でホストされるので、Teams タブの開発プロセスが大幅に簡素化されます。 [Teams での SharePoint Framework の使用の詳細について説明します。](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>はじめに

次の手順では、Microsoft Teams サンプル アプリからタブを取り、SharePoint で使用する方法について説明します。 必要な統合作業に集中するために、Azure で既にホストされているタブを使用します。

使用しているサンプル アプリは、Talent Management アプリケーションです。 チーム内のオープンポジションの候補の採用プロセスを管理します。 (アプリ自体は見栄えは良く見えますが、実際には何もしません。 実際の人材管理アプリケーションを作成するのではなく、Teams アプリの構築と Teams への読み込みに重点を置きたいと思っています。

### <a name="benefits-of-this-approach"></a>このアプローチの利点

- 既存の Teams タブを使用して SharePoint ユーザーにアクセスする
- アプリ マニフェストを SharePoint アプリ カタログに直接アップロードします。 [Teams アプリケーション パッケージ](~/concepts/build-and-test/apps-package.md) が SharePoint でサポートされる
- エンド ユーザーが他の SharePoint Web パーツと同様にページ上のタブを構成する
- タブは、Teams [内で](~/tabs/how-to/access-teams-context.md) 実行する場合と同じ方法でコンテキストにアクセスできます。

## <a name="step-1-testing-the-sample-app"></a>手順 1: サンプル アプリをテストする

サンプル アプリ マニフェストは、ここからダウンロード [**してください**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)。

Microsoft Teams で、左下の [ストア] アイコンをクリックし、左下の [カスタム アプリのアップロード] をクリックします。 アップロードするファイルは[ダウンロード] フォルダーにあります。このメソッドは、TalentMgmt-Azure.zip。 すべて問題ない場合は、人材管理アプリのインストール/同意画面が表示されます。 インストールするチームを選択し、[インストール] ボタンをクリックします。 これで、アプリを自由に試す必要があります。

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a>手順 2: SharePoint の [Teams] タブを使用する

Teams アプリ パッケージをアップロードし、SharePoint アプリ カタログに展開するには、次に例 `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` を示します `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。

メッセージが表示されたら、"このソリューションを組織内のすべてのサイトで使用可能にする" を有効にします。

![SharePoint ビューのタブ](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

サイトで、右上の歯車ボタンをクリックし、[ページの追加] をクリックして、新しいページを作成します。

![Sharepoint ビュー](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

SharePoint ページの作成エクスペリエンスが表示されます。 ページに「自分の Teams タブ」という名前を付け、

[+] ボタンを押して Web パーツ ツールボックスを開き、Teams タブ ("Contoso HR" という名前) を選択します。 Web パーツはアルファベット順に並べ替えされます。リストが長い場合は、検索バーを使用して検索できます。 これにより、Teams タブを含む Web パーツがキャンバスに作成されます。

![タブ ビュー](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

編集が完了したら、[発行] ボタンを押します。

左側のナビゲーション バーでページをクイック参照するには、[ナビゲーションにページを追加] をクリックします。

![Sharepoint イメージのタブ](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a>手順 3: SharePoint のアプリ ページを確認する

ページが公開された後は、Teams アプリを SharePoint 内のより完全な [エクスペリエンスに変える方法について説明します](/sharepoint/dev/spfx/web-parts/single-part-app-pages)。 これにより、現在のページがアプリ ページに変換されます。[Teams] タブでは、通常の SharePoint ページ レイアウトとページ全体のエクスペリエンスが表示されます。

![Sharepoint のタブの画像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>コード サンプル
| **サンプルの名前** | **説明** | **SPFx** |
|-----------------|-----------------|----------|
| SPFx Web パーツ | タブ、チャネル、およびグループ用の SPFx Web パーツのサンプル。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="more-information"></a>詳細情報

- [SharePoint Framework を使用した Microsoft Teams タブの作成: チュートリアル](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [SharePoint Online での Single Part App Pages の使用](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
