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
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a>SharePoint の Microsoft Teams タブを SPFx web パーツとして追加する

> [!IMPORTANT]
> この機能は現在プレビュー段階であり、変更される可能性があります。 運用環境での使用はサポートされていません。 [SharePoint 開発ドキュメントの問題リスト](https://github.com/SharePoint/sp-dev-docs/issues)を使用して、この機能に関するフィードバックやご意見をお寄せください。

## <a name="rich-integration-between-teams-and-sharepoint"></a>Teams と SharePoint の間の高度な統合

11月リリースの Teams と SharePoint Framework v を使用しています。 1.7 の開発者には、次の2つの強力な機能があります。

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
                        <p>Teams アプリを Sharepoint にすることで、SharePoint で豊富なアプリエクスペリエンスを作成します (この記事)。</p>
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
                        <h3>Teams での SharePoint Framework</h3>
                        <p>SharePoint web パーツを Teams に移行し、SharePoint でホスティングを管理できるようにします。</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>SharePoint の Teams タブ

SharePoint Framework v2.0 を使用すると、開発者は Teams タブを使用して SharePoint でホストすることができるようになります。 SharePoint でホストされているタブの場合と同様に、SharePoint サイトのコンテキストと理解を保ったまま、Teams タブのすべての機能が公開されています。

### <a name="sharepoint-framework-in-teams"></a>Teams での SharePoint Framework

SharePoint Framework を使用して Microsoft Teams のタブを実装することもできます。 Sharepoint 開発者にとって、sharepoint Framework web パーツは Azure などの外部サービスを必要とせずに SharePoint 内でホストされるため、これにより、Teams タブの開発プロセスが大幅に簡素化されます。 [Teams での SharePoint Framework の使用方法について説明します。](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>概要

次の手順では、Microsoft Teams サンプルアプリからタブを取得し、それを SharePoint で使用する方法について説明します。 必要な統合作業に焦点を当てるために、Azure で既にホストされているタブを使用します。

使用しているサンプルアプリは、人材管理アプリケーションです。 これにより、チーム内のオープンポジションの採用候補の雇用プロセスが管理されます。 (アプリ自体は見栄えがよく見えますが、実際には何も実行しません。 Teams アプリを作成して Teams に読み込むことに重点を置いて、実際の人材管理アプリケーションを作成することはお勧めしません。

### <a name="benefits-of-this-approach"></a>このアプローチの利点

- [既存のチーム] タブを使用して SharePoint ユーザーにアクセスする
- アプリのマニフェストを SharePoint アプリカタログに直接アップロードします。 [Teams アプリケーションパッケージ](~/concepts/build-and-test/apps-package.md) が SharePoint によってサポートされるようになりました
- エンドユーザーは、他の SharePoint web パーツと同じように、ページ上のタブを構成します。
- タブは、Teams 内で実行する場合と同様に、 [コンテキスト](~/tabs/how-to/access-teams-context.md) にアクセスできます。

## <a name="step-1-testing-the-sample-app"></a>手順 1: サンプルアプリをテストする

サンプルアプリのマニフェストを [**ここ**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)からダウンロードしてください。

Microsoft Teams で、左下の [Store] アイコンをクリックしてから、左下の [カスタムアプリのアップロード] をクリックします。 アップロードするファイルは、[ダウンロード] フォルダーにあります。これは TalentMgmt-Azure.zip と呼ばれます。 すべてがうまくいくと、才能 management アプリのインストール/同意画面が表示されます。 インストール先のチームを選択し、[インストール] ボタンをクリックします。 アプリを自由に試すことができるようになりました。

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a>手順 2: SharePoint で Teams タブを使用する

にアクセスして、Teams アプリパッケージをアップロードし、SharePoint アプリカタログに展開し `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` ます (例:) `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。

メッセージが表示されたら、[組織内のすべてのサイトでこのソリューションを使用できるようにする] を有効にします。

![Sharepoint ビューのタブ](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

サイトで、右上隅にある歯車ボタンをクリックし、[ページの追加] をクリックして、新しいページを作成します。

![Sharepoint ビュー](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

SharePoint ページの作成環境が表示されます。 ページに「My Teams タブ」という名前を指定します。

+ ボタンを押して web パーツツールボックスを開き、[Teams] タブ ("Contoso HR" という名前) を選択します。 Web パーツはアルファベット順に並べ替えられます。リストが長い場合は、検索バーを使用して検索できます。 これにより、Teams タブを含むキャンバスに web パーツが作成されます。

![タブビュー](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

編集が終了したら、[発行] ボタンを押します。

左側のナビゲーションバーにページのクイックリファレンスを表示するには、[ページをナビゲーションに追加] をクリックします。

![Sharepoint 画像のタブ](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a>手順 3: SharePoint でアプリページを調べる

ページが発行されると、 [Teams アプリを SharePoint 内でより完全な体験に](/sharepoint/dev/spfx/web-parts/single-part-app-pages)することができます。 これにより、現在のページがアプリページに変換され、[Teams] タブの完全なページ表示がある通常の SharePoint ページレイアウトが表示されます。

![Sharepoint のタブの画像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="more-information"></a>詳細情報

- [SharePoint Framework を使用した Microsoft Teams タブの作成: チュートリアル](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [SharePoint Online での Single Part App Pages の使用](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
