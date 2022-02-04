---
title: アプリに SaaS オファーを含める
description: サブスクリプション プランを使用してアプリMicrosoft Teams収益化する方法について学習します。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: 0efaea87af8128086db3e0e6416014d97f0af5a2
ms.sourcegitcommit: 54f6690b559beedc330b971618e574d33d69e8a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2022
ms.locfileid: "62362775"
---
# <a name="include-a-saas-offer-with-your-microsoft-teams-app"></a>SaaS オファーをアプリにMicrosoft Teamsする

:::row:::
   :::column span="3":::

取引可能なサービスとしてのソフトウェア (SaaS) オファーを使用すると、Teams ストアの登録情報からサブスクリプション プランを直接販売することで、Teams Teams アプリを収益化できます。 たとえば、誰もがストアにアクセスできる無料アプリを持っているとします。 これで、より多くの機能が必要なユーザーに対して、プレミアムプランとエンタープライズ プランを提供できます。

アプリを収益化する方法の一般的な考え方を次に示します。

1.  [SaaS プランを計画します](#plan-your-saas-offer)。

1.  [SaaS フルフィルメント API と統合します](#integrate-with-the-saas-fulfillment-apis)。

1.  [サブスクリプション管理用のランディング ページを作成します](#build-a-landing-page-for-subscription-management)。

1.  [SaaS オファーを作成します](#create-your-saas-offer)。

1.  [SaaS オファー用にアプリを構成します](#configure-your-app-for-the-saas-offer)。

1.  [アプリをアプリ ストアTeamsします](#publish-your-app)。

   :::column-end:::
   :::column span="1":::
   
:::image type="content" source="~/assets/images/saas-offer/saas-offer-diagram.png" alt-text="SaaS オファーをアプリに含める方法を示すTeams図。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="plan-your-saas-offer"></a>SaaS プランを計画する

包括的なガイダンスについては、「 [Microsoft 商用市場向け SaaS プランを計画する方法」を参照してください](/azure/marketplace/plan-saas-offer)。

アプリで収益を上Teams計画する場合は、次の点を考慮してください。

* サブスクリプション モデルを決定します。 トランザクション可能な SaaS プランには、複数のサブスクリプション プランを含めできます。 誰でも利用できる公開サブスクリプション プランは最も一般的ですが、特定の顧客のみを対象にした場合もあります。 詳細については、「Microsoft 商用 [マーケットプレースのプライベート オファー」を参照してください](/azure/marketplace/private-offers)。
* ユーザーが[アプリのサブスクリプション](/azure/marketplace/plan-saas-offer#listing-options) プランをアプリのサブスクリプション プランを直接購入する場合は、SaaS プランの [Microsoft による販売] オプションについてTeamsしてください。
* シングル [サインオンAzure Active Directory (SSO)](/azure/marketplace/azure-ad-saas) を使用して、顧客がサブスクリプションを購入および管理する方法について学習します。 (saaS Azure ADアプリの場合はTeams SSO が必要です)。
* お客様の SaaS オファーの使用をサポートするために必要なインフラストラクチャの管理と支払いは、お客様の責任で行う必要があります。
* モバイルを計画する。 サードパーティのアプリ ストア ポリシーに違反しないようにするために、アプリには、ユーザーがモバイルでサブスクリプション プランを購入できるリンクを含めかねない。 ただし、アプリにサブスクリプション プランを必要とする機能が含けられているかどうかを示す場合は、引き続き指定できます。 詳細については、関連する商用マーケットプレース認定ポリシー [を参照してください](/legal/marketplace/certification-policies#114048-mobile-experience)。

## <a name="integrate-with-the-saas-fulfillment-apis"></a>SaaS フルフィルメント API との統合

SaaS フルフィルメント API との統合は、アプリの収益化にTeamsです。 これらの API は、ユーザーが購入したサブスクリプション プランのライフサイクルを管理するのに役立ちます。

詳細な手順と API リファレンスについては、 [SaaS フルフィルメント API のドキュメントを参照してください](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-apis)。 一般に、サブスクリプションの購入後に API を使用して次の手順を実装します。

1. ランディング ページ [*への URL を介*](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-life-cycle#purchased-but-not-yet-activated-pendingfulfillmentstart) して購入識別トークンを受け取ります。

1. トークンを使用してサブスクリプションの詳細を取得します。

1. サブスクリプションがアクティブ化されている商用マーケットプレースに通知します。

### <a name="best-practices-for-implementing-subscription-management"></a>サブスクリプション管理を実装するためのベスト プラクティス

* Teams アプリ向け取引可能な SaaS オファーでは、サブスクリプション プラン (ライセンス) は、グループまたは組織全体ではなく、個々のユーザーに割り当てる必要があります。
* ユーザーにサブスクリプション プランが割り当てられている場合は、ボットまたはTeamsを通じて通知します。 メッセージングで、アプリをアプリに追加して開始する方法Teams含める。
* 複数の管理者のアイデアをサポートします。 つまり、同じ組織の複数のユーザーが独自のサブスクリプションを購入および管理できます。

## <a name="build-a-landing-page-for-subscription-management"></a>サブスクリプション管理用のランディング ページを作成する 

Teams ストアでアプリのサブスクリプション プランの購入が完了すると、商用マーケットプレースからランディング ページに移動して、サブスクリプションを管理できます (組織の特定のユーザーにライセンスを割り当てるなど)。

詳細な手順については、「 [SaaS オファーのランディング ページを作成する」を参照してください](/azure/marketplace/azure-ad-transactable-saas-landing-page)。

### <a name="best-practices-for-landing-pages"></a>ランディング ページのベスト プラクティス

収益化するアプリのランディング ページを作成する際には、次Teams方法を検討してください。 エンド ユーザーの購入エクスペリエンスでランディング ページ [の例を参照してください](#end-user-purchasing-experience)。

* ユーザーは、サブスクリプションの購入に使用した資格情報と同Azure ADランディング ページにログインできる必要があります。 詳細については、「商用マーケットAzure AD SaaS の販売と取引可能な [SaaS オファー」を参照してください](/azure/marketplace/azure-ad-saas)。
* ユーザーがランディング ページで次の操作を実行できます。 ユーザーの役割とアクセス許可に適した機能を検討することを忘れないでください (たとえば、サブスクリプション管理者だけがユーザーを検索することを許可する場合があります)。
  * 電子メールまたは別の形式の ID を使用して、組織のユーザーを検索します。
  * リストでライセンスを割り当て可能なユーザーを確認します。
  * ライセンスを 1 人または複数のユーザーに同時に割り当てる。
  * 異なる種類のライセンスを割り当て、管理します (使用可能な場合)。
  * ライセンスが既に別のユーザーに割り当てられているか検証します。
  * サブスクリプションをキャンセルします。
* アプリの使い方の概要を説明します。
* FAQ、ナレッジ ベース、連絡先メールなど、サポートを受け取る方法を追加します。
* サブスクライバーがランディング ページに戻りやすくするリンクを提供します。 たとえば、アプリの [概要] タブにこのリンク **を含** める。

## <a name="create-your-saas-offer"></a>SaaS オファーを作成する

SaaS フルフィルメント API を統合し、ユーザーがサブスクリプションを管理できるランディング ページを構築したら、取引可能な SaaS プランを公式に作成、テスト、発行します。

> [!IMPORTANT]
> Teamsは、SaaS オファーの **ユーザー単位 (** ユーザー/月およびユーザー/年) の価格モデルのみをサポートしています。 詳細については、「 [SaaS 価格モデル」を参照してください](/azure/marketplace/plan-saas-offer#saas-pricing-models)。

### <a name="create-the-offer"></a>オファーを作成する

パートナー [センターでこれを行う方法の詳細については、「Create a SaaS offer](/azure/marketplace/create-new-saas-offer) 」を参照してください。 次の手順では、高レベルで実行する操作について説明します。

1.  パートナー センター [アカウントをお持](https://partner.microsoft.com/) ちでない場合は、パートナー センター アカウントを作成します。

1.  取引可能な SaaS プランのサブスクリプション プラン、価格の詳細などについて構成します。 特に、次の手順を実行してください。

    * [ **セットアップの詳細]** で、[ **は** い] オプションを選択して、Microsoft を通じてオファーを販売する場合に指定します。
     
    * [**Microsoft 365統合] で**、アプリの一覧に [AppSource] リンクを追加します。 この手順では、ユーザーが AppSource でサブスクリプション プランを購入できるだけでなく、サブスクリプション プランも購入Teams。

1. 発行元とオファーの ID を保存します。 (開発者ポータルでオファーをアプリにリンクするには、後で必要になります)。

1. オファーを商用マーケットプレースに発行します。

### <a name="test-the-offer"></a>オファーをテストする

SaaS オファーを発行する前に、エンドツーエンドの購入エクスペリエンスを確認することを強く推奨します。 これを行うには、テスト用に個別のオファーを作成します。 詳細については、「テスト オファーの [概要」、](/azure/marketplace/plan-saas-offer#test-offer)テスト [オファーの](/azure/marketplace/create-saas-dev-test-offer)作成、およびオファー [のプレビューを参照してください](/azure/marketplace/test-publish-saas-offer)。

> [!IMPORTANT]
> アプリがストアの検証を完了するまで、Teamsトランザクションをテストできます。 詳細については、「収益化された [アプリのプレビューをテストする」を参照してください](Test-preview-for-monetized-apps.md)。

これらのテストTeams、ユーザーが次の場合に、ライセンスと割り当ての数が管理センターにある数と一致Teams確認する必要があります。

* ランディング ページでサブスクリプション プランをアクティブ化して構成します。
* 自分自身または他のユーザーにライセンスを割り当て、削除、または再割り当てします。
* サブスクリプションをキャンセルまたは更新します。

### <a name="publish-the-offer"></a>オファーを発行する

テストが完了したら、オファー [をライブで公開します](/azure/marketplace/test-publish-saas-offer#publish-your-offer-live)。

## <a name="configure-your-app-for-the-saas-offer"></a>SaaS オファー用にアプリを構成する

SaaS プランは公開済みですが、ユーザーがサブスクリプション プランを Teams ストアに表示するには、そのプランを Teams アプリにリンクする必要があります。

1. 開発者ポータルに [移動し、[アプリ](https://dev.teams.microsoft.com/) ] を **選択します**。
1. [アプリ **] ページ** で、SaaS オファーをリンクするアプリを選択します。
1. [プランと価格 **] ページに移動** し、発行元とオファーの ID を指定します。 (これらの ID は、すぐに利用できない場合は、パートナー センターで確認できます)。
1. [ **表示] を** 選択して、SaaS プランのサブスクリプション プランをプレビューします。
1. すべてが適切な場合は、[保存] を **選択します**。

   プロパティ `subscriptionOffer` がアプリ マニフェストに [追加されます](~/resources/schema/manifest-schema-dev-preview.md#subscriptionoffer)。

   ```json
      "subscriptionOffer": {
        "offerId": "publisherId.offerId"  
        }
   ```

## <a name="publish-your-app"></a>アプリを公開する

SaaS オファーを作成し、Teams アプリにリンクしました。次に、アプリをアプリを Teams ストアに発行します。 詳細な手順については、「[アプリをアプリストアに発行する」をTeamsしてください](~/concepts/deploy-and-publish/appsource/publish.md)。

> [!IMPORTANT]
> アプリが既に Teams ストアに表示されている場合でも、SaaS オファーを含めるには、ストア検証プロセスを再度実行する必要があります。

公開すると、アプリをアプリに追加しようとするときに、[アプリの詳細] ダイアログに [サブスクリプションの購入] オプションが表示Teams。

## <a name="end-user-purchasing-experience"></a>エンドユーザーの購入エクスペリエンス

次の例は、ユーザーが Recloud と呼ばれる架空のアプリのサブスクリプション プランTeams *示しています*。

1. [アプリ] Teams、*Recloud アプリを見つけて選択* します。

1. アプリの詳細ダイアログで、[サブスクリプションの購入 **] を選択します**。

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplan.png" alt-text="選択したアプリのサブスクリプションを購入する。":::

1. お客様の国を選択すると、現在地のサブスクリプション プランが表示されます。

1. [サブスクリプション **プランの選択] ダイアログで** 、必要なプランを選択し、[チェックアウト] を **選択します**。 (注: プライベート プランは、オファーを提供する組織のユーザーにのみ表示されます。 これらのプランには、特別オファー アイコン **が表示**:::image type="icon" source="~/assets/icons/special-icon.png":::されます)。

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplan.png" alt-text="適切なサブスクリプション プランを選択します。":::

1. [チェックアウト **] ダイアログで** 、必要な情報を入力し、[注文の配置] **を選択します**。

    :::image type="content" source="~/assets/images/saas-offer/placesubscriptionorder.png" alt-text="サブスクリプションの注文を行う。":::

1. メッセージが表示されたら、[今 **すぐ設定] を選択して** サブスクリプションを設定します。

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-set-up.png" alt-text="サブスクリプションのセットアップ。":::

1. *Recloud* Web サイト (ランディング ページとも呼ばれる) を使用してサブスクリプション プランを [管理します](#build-a-landing-page-for-subscription-management)。

    :::image type="content" source="~/assets/images/saas-offer/subscriptionlicenses.png" alt-text="ユーザー ライセンスの構成。":::

## <a name="admin-purchasing-experience"></a>管理者の購入エクスペリエンス

管理者は、アプリのサブスクリプション プランを管理センター Teams[購入できます](/MicrosoftTeams/purchase-third-party-apps)。

## <a name="remove-a-saas-offer-from-your-app"></a>アプリから SaaS オファーを削除する

Teams ストアの登録情報に含まれる SaaS オファーのリンクを解除する場合は、アプリを再発行してストア内の変更を確認する必要があります。

1. 開発者ポータルに [移動し、[アプリ](https://dev.teams.microsoft.com/) ] を **選択します**。
1. [アプリ **] ページ** で、オファーを削除するアプリを選択します。
1. [プランと価格 **] ページに移動し、[** 元に戻す] を **選択します**。
1. オファーのリンクが解除された後、次の手順を実行してストアの登録情報を更新します。
   1. [**配布] >ストアに発行Teamsします**。
   1. [ **パートナー センターを開く** ] を選択して、オファーなしでアプリを再発行するプロセスを開始します。

## <a name="see-also"></a>関連項目

[発行済みアプリの保守とサポート](../post-publish/overview.md)
