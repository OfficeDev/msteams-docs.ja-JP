---
title: アプリに SaaS オファーを含める
description: Teams ストアの登録情報からサブスクリプション プランを直接販売することで、Microsoft Teams アプリを収益化する方法について説明します。 発行アプリ、エンド ユーザー、管理者の購入エクスペリエンスについて説明します。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 3fe41b635f9789e7f96eeb41f17526205924dadf
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100638"
---
# <a name="include-a-saas-offer-with-your-teams-app"></a>Teams アプリに SaaS オファーを含める

:::row:::
   :::column span="3":::

取引可能なサービスとしてのソフトウェア (SaaS) オファーを使用すると、Teams ストア登録情報からサブスクリプション プランを直接販売し、Teams アプリを収益化できます。 たとえば、ストアで誰でも入手できる無料アプリを持っているとします。 より多くの機能が必要なユーザーに対して、プレミアム プランとエンタープライズ プランを提供できます。

アプリを収益化する方法の一般的な概念を次に示します。

1. [SaaS オファーを計画します](#plan-your-saas-offer)。

1. [SaaS フルフィルメント API と統合します](#integrate-with-the-saas-fulfillment-apis)。

1. [サブスクリプション管理のためのランディング ページを作成します](#build-a-landing-page-for-subscription-management)。

1. [SaaS オファーを作成します](#create-your-saas-offer)。

1. [SaaS オファー用にアプリを構成します](#configure-your-app-for-the-saas-offer)。

1. [アプリを Teams ストアに公開します](#publish-your-app)。

   :::column-end:::
   :::column span="1":::

:::image type="content" source="~/assets/images/saas-offer/saas-offer-diagram.png" alt-text="Teams アプリに SaaS オファーを含める方法のプロセスを示す図。":::

   :::column-end:::
:::row-end:::

## <a name="plan-your-saas-offer"></a>SaaS オファーの計画

包括的なガイダンスについては、「[コマーシャル マーケットプレース向けの SaaS オファーを計画する方法](/azure/marketplace/plan-saas-offer)」を参照してください。

Teams アプリを収益化する方法を計画するとき、次の点を考慮します。

* サブスクリプション モデルを決定します。 取引可能な SaaS プランには、複数のサブスクリプション プランを含めることができます。 誰でも利用できるパブリック サブスクリプション プランが最も一般的ですが、特定の顧客のみを対象に特典を用意する必要がある場合もあります。 詳細については、「[Microsoft コマーシャル マーケットプレースでのプライベート プラン](/azure/marketplace/private-plans)」を参照してください。
* SaaS オファーの「[*Microsoft を通じた販売*」リスト オプション](/azure/marketplace/plan-saas-offer#listing-options)についてお読みください。これは、ユーザーが Teams ストアを通して直接サブスクリプション プランを購入するようにする場合に必要です。
* [Azure Active Directory シングル サインオン (SSO)](/azure/marketplace/azure-ad-saas) がユーザーのサブスクリプションの購入と管理に役立つ方法を参照します。 (Microsoft Azure Active Directory (Azure AD) SSO は、SaaS オファーを含む Teamsアプリに必要です。)
* 顧客による SaaS オファーの使用をサポートするために必要なインフラストラクチャを管理し、支払う責任があることを理解します。
* モバイル向けに計画します。 サードパーティのアプリ ストア ポリシーの違反を回避するため、ユーザーがモバイルでサブスクリプション プランを購入できるリンクをアプリに含めることはできません。 ただし、アプリにサブスクリプション プランを必要とする機能が含まれているかどうかを引き続き示すことはできます。 詳細については、「[コマーシャル マーケットプレース認定ポリシー](/legal/marketplace/certification-policies#114048-mobile-experience)」を参照してください。

## <a name="integrate-with-the-saas-fulfillment-apis"></a>SaaS フルフィルメント API との統合

Teams アプリを収益化するには、SaaS フルフィルメント API との統合が必要です。 これらの API は、ユーザーが購入したサブスクリプション プランのライフサイクルを管理するのに役立ちます。

詳細な手順と API リファレンスについては、「[SaaS フルフィルメント API のドキュメント](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-apis)」を参照してください。 一般に、サブスクリプションが購入されたら、API を使用して次の手順を実装します。

1. ランディング ページへの URL を介して [*購入 ID トークンを受け取ります*](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-life-cycle#purchased-but-not-yet-activated-pendingfulfillmentstart)。

1. トークンを使用してサブスクリプションの詳細を取得します。

1. サブスクリプションがアクティブ化されたことをコマーシャル マーケットプレースに通知します。

### <a name="best-practices-for-implementing-subscription-management"></a>サブスクリプション管理を実装するためのベスト プラクティス

* Teams アプリの取引可能な SaaS オファーでは、サブスクリプション プラン (ライセンス) は、グループまたは組織全体ではなく、個々のユーザーに割り当てられる必要があります。
* ユーザーにサブスクリプション プランが割り当てられたら、Teams ボットまたはメールで通知します。 メッセージには、Teams にアプリを追加して開始する方法を含めます。
* 複数の管理者という概念をサポートします。 つまり、同じ組織の複数のユーザーが自分のサブスクリプションを購入および管理できます。

## <a name="build-a-landing-page-for-subscription-management"></a>サブスクリプション管理のためのランディング ページを作成する

Teams ストアでアプリのサブスクリプション プランの購入を完了すると、ユーザーはコマーシャル マーケットプレースからランディング ページに移動します。ここでは、サブスクリプションを管理できます (組織の特定のユーザーにライセンスを割り当てるなど)。

詳細な手順については、「[SaaS オファーのランディング ページを作成する](/azure/marketplace/azure-ad-transactable-saas-landing-page)」を参照してください。

### <a name="best-practices-for-landing-pages"></a>ランディング ページのベスト プラクティス

収益化する Teams アプリのランディング ページを作成するとき、次の方法を検討してください。 「[エンドユーザーの購入エクスペリエンス](#end-user-purchasing-experience)」でランディング ページの例を参照してください。

* ユーザーは、サブスクリプションの購入に使用したのと同じ Azure AD 資格情報を使用してランディング ページにサインインできる必要があります。 詳細については、「[コマーシャル マーケットプレースにおける Azure AD と取引可能な SaaS オファー](/azure/marketplace/azure-ad-saas)」を参照してください。
* ユーザーがランディング ページで次の操作を実行できるようにします。 ユーザーのロールとアクセス許可に適したものを忘れないでください。 たとえば、サブスクリプション管理者のみがユーザーを検索できるようにすることができます):
  * メールまたは別の形式の ID を使用して、組織のユーザーを検索する。
  * ライセンスを割り当てることのできるユーザーをリストで確認する。
  * ライセンスを 1 人または複数のユーザーに同時に割り当てる。
  * 異なる種類のライセンスを割り当て、管理する (使用可能な場合)。
  * ライセンスが既に別のユーザーに割り当てられているかどうかを検証する。
  * サブスクリプションをキャンセルする。
* アプリの使い方の概要を説明します。
* FAQ、ナレッジ ベース、連絡先のメール アドレスなど、サポートを受ける方法を追加します。
* サブスクライバーがランディング ページに簡単に戻ることができるようにするリンクを提供します。 たとえば、アプリの **[情報]** タブにこのリンクを含めます。

## <a name="create-your-saas-offer"></a>SaaS オファーを作成する

SaaS フルフィルメント API を統合し、ユーザーがサブスクリプションを管理できるランディング ページを作成したら、いよいよ取引可能な SaaS オファーを作成し、テストして公開します。

### <a name="create-the-offer"></a>オファーを作成する

パートナー センターでこれを行う方法の詳細な手順については、「[SaaS オファーを作成する](/azure/marketplace/create-new-saas-offer)」を参照してください。 次の手順では、実行する操作を大まかに説明します。

1. パートナー センター アカウントをお持ちでない場合は、[パートナー センター](https://partner.microsoft.com/) アカウントを作成します。

1. 取引可能な SaaS プランのサブスクリプション プラン、価格の詳細などを構成します。 特に、次の手順を必ず実行してください。

    * **[セットアップの詳細]** で、**[はい]** オプションを選択して、Microsoft を通してオファーを販売するように指定します。

    * **[Microsoft 365 の統合]** で、アプリの登録情報に AppSource リンクを追加します。 この手順により、ユーザーが Teams に加えて AppSource でもサブスクリプション プランを購入できます。

1. 発行元 ID とオファー ID を保存します。 (開発者ポータルでオファーをアプリにリンクするために後で必要になります)。

1. オファーをコマーシャル マーケットプレースに公開します。

### <a name="test-the-offer"></a>オファーをテストする

SaaS オファーを公開する前に、エンドツーエンドの購入エクスペリエンスを確認することをお勧めします。 テスト専用の別のオファーを作成することで確認できます。 詳細については、「[オファーのテスト](/azure/marketplace/plan-saas-offer#test-offer)」、「[テスト オファーを作成する](/azure/marketplace/create-saas-dev-test-offer)」、「[オファーをプレビューする](/azure/marketplace/test-publish-saas-offer)」を参照してください。

> [!IMPORTANT]
> [収益化されたアプリのテスト プレビュー](Test-preview-for-monetized-apps.md)機能を使用して、Teams でエンド ツー エンドのトランザクションをテストできます。 ライブ オファーの場合は、アプリ ストアの検証プロセスを完了する必要があります。

Teams の観点から、これらのテストで、ユーザーが次の操作を実行するときにライセンスと割り当ての数が Teams 管理センターでの数と一致することを検証する必要があります。

* ランディング ページでサブスクリプション プランをアクティブ化して構成する。
* 自分または他のユーザーにライセンスを割り当て、削除、または再割り当てする。
* サブスクリプションをキャンセルまたは更新する。

### <a name="publish-the-offer"></a>オファーを公開する

テストが完了したら、[オファーをライブ公開します](/azure/marketplace/test-publish-saas-offer#publish-your-offer-live)。

## <a name="configure-your-app-for-the-saas-offer"></a>SaaS オファー用にアプリを構成する

SaaS オファーを公開しましたが、Teams ストアでサブスクリプション プランをユーザーに表示するには、オファーを Teams アプリにリンクする必要があります。

1. [開発者ポータル](https://dev.teams.microsoft.com/)に移動し、**[アプリ]** を選択します。
1. **[アプリ]** ページで、SaaS オファーをリンクするアプリを選択します。
1. **[プランと価格]** ページに移動し、発行元 ID とオファー ID を指定します。 (これらの ID がすぐにわからない場合は、パートナー センターで確認できます。)
1. **[表示]** を選択して、SaaS オファーのサブスクリプション プランをプレビューします。
1. 問題がない場合は、**[保存]** を選択します。

   `subscriptionOffer` プロパティが[アプリ マニフェスト](~/resources/schema/manifest-schema-dev-preview.md#subscriptionoffer)に追加されます。

   ```json
      "subscriptionOffer": {
        "offerId": "publisherId.offerId"  
        }
   ```

## <a name="publish-your-app"></a>アプリを公開する

SaaS オファーを作成し、Teams アプリにリンクしました。次に、アプリを Teams ストアに公開します。 詳細な手順については、「[Teams ストアにアプリを公開する](~/concepts/deploy-and-publish/appsource/publish.md)」を参照してください。

> [!IMPORTANT]
>
> * アプリが既に Teams ストアに表示されている場合でも、SaaS オファーを含めるには、ストア検証プロセスを再度実行する必要があります。
> * アプリ マニフェストでオファー ID と発行元 ID なしで作成された定額プランは、検証のために更新して再送信する必要があります。

アプリを公開すると、ユーザーがアプリを Teams に追加しようとするときに [アプリの詳細] ダイアログに **[サブスクリプションの購入]** オプションが表示されます。

## <a name="end-user-purchasing-experience"></a>エンドユーザーの購入エクスペリエンス

次の例は、ユーザーが *Recloud* という架空の Teams アプリでサブスクリプション プランを購入する方法を示しています。

1. Teams ストアで、*Recloud* アプリを見つけて選択します。

1. [アプリの詳細] ダイアログで、**[サブスクリプションの購入]** を選択します。

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplan.png" alt-text="選択したアプリのサブスクリプションを購入する。":::

1. 国を選択すると、自分の地域のサブスクリプション プランが表示されます。

1. **[サブスクリプション プランを選ぶ]** ダイアログで目的のプランを選択し、**[チェックアウト]** を選択します。 (注: プライベート プランは、オファーを提供する組織のユーザーにのみ表示されます。 これらのプランには **特別オファー** :::image type="icon" source="~/assets/icons/special-icon.png"::: アイコンが表示されます。)

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplan.png" alt-text="適切なサブスクリプション プランを選択する。":::

1. **[チェックアウト]** ダイアログで必要な情報を入力し、**[注文]** を選択します。

    :::image type="content" source="~/assets/images/saas-offer/placesubscriptionorder.png" alt-text="サブスクリプションの注文を行う。":::

1. メッセージが表示されたら、**[今すぐ設定]** を選択してサブスクリプションを設定します。

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-set-up.png" alt-text="サブスクリプションを設定する。":::

1. *Recloud* Web サイト ([ランディング ページ](#build-a-landing-page-for-subscription-management)とも呼ばれる) を使用してサブスクリプション プランを管理します。

    :::image type="content" source="~/assets/images/saas-offer/subscriptionlicenses.png" alt-text="ユーザー ライセンスを構成する。":::

## <a name="admin-purchasing-experience"></a>管理者の購入エクスペリエンス

管理者は、[Teams 管理センター](/MicrosoftTeams/purchase-third-party-apps)でアプリのサブスクリプション プランを購入できます。

## <a name="remove-a-saas-offer-from-your-app"></a>アプリから SaaS オファーを削除する

Teams ストア登録情報に含まれる SaaS オファーのリンクを解除する場合、変更をストアに表示するにはアプリを再公開する必要があります。

1. [開発者ポータル](https://dev.teams.microsoft.com/)に移動し、**[アプリ]** を選択します。
1. **[アプリ]** ページで、オファーを削除するアプリを選択します。
1. **[プランと価格]** ページに移動し、**[元に戻す]** を選択します。
1. オファーのリンクが解除されたら、次の手順を実行してストア登録情報を更新します。
   1. **[配布] > [Teams ストアに公開する]** の順に選択します。
   1. **[パートナー センターを開く]** を選択して、オファーなしでアプリを再発行する手順を開始します。

## <a name="see-also"></a>関連項目

* [公開したアプリの管理とサポート](../post-publish/overview.md)
* [SaaS オファーに関連付けられたアプリの検証ガイドライン](teams-store-validation-guidelines.md#apps-linked-to-saas-offer)
