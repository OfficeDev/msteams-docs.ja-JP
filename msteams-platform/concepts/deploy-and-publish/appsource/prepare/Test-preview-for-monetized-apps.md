---
title: 収益化されたアプリのテスト プレビュー
author: v-ypalikila
description: オファーをライブにプッシュする前に、Teams SaaS Preview オファーを作成してテストします。
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
keywords: Teams アプリ SaaS がプレビュー を提供するテスト プレビューの収益化された Saas
ms.openlocfilehash: 849dd2ecd79a4b43d6feb6ceaca599f371df1de1
ms.sourcegitcommit: 54f6690b559beedc330b971618e574d33d69e8a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2022
ms.locfileid: "62363480"
---
# <a name="test-preview-for-monetized-apps"></a>収益化されたアプリのテスト プレビュー

> [!NOTE]
> 収益化されたアプリのテスト プレビューは、現在開発者向けプレビュー [**でのみ利用できます**](/microsoftteams/platform/resources/dev-preview/developer-preview-intro)。

サービスとしてのソフトウェア (SaaS) オファーを作成し、収益化されたアプリのエンドツーエンドの購入エクスペリエンスをテストTeams。 アプリのプレビュー 対象ユーザーとして追加されたユーザーはTeams前に SaaS オファーを確認できます。

## <a name="create-a-preview-offer-id"></a>プレビュー オファー ID の作成

パートナー センターの [ **AppSource** プレビュー] リンクからプレビュー オファー ID を生成できます。 SaaS オファーがプレビュー作成フェーズにあるか確認します。 プレビュー オファー ID を生成するには、次の方法を実行します。

1. パートナー センター [に移動し](https://go.microsoft.com/fwlink/?linkid=2166002) 、開発者資格情報を使用してサインインします。
1. [Marketplace **のオファー] を選択します**。
1. プレビューする SaaS オファーを選択します。
1. SaaS [オファーのプレビュー](/azure/marketplace/create-new-saas-offer-preview) 対象ユーザーを追加します。
1. [ **Go Live] の [AppSource** プレビュー] リンク **を** 選択して、 *publisherId.offerId-preview* 形式のブラウザー アドレス バーでプレビュー オファー ID を検索します。

    :::image type="content" source="../../../../assets/images/apps-in-meetings/publish-status-publisher-signoff.png" alt-text="プレビュー オファー ID" border="true" :::

1. ブラウザーのアドレス バーからプレビュー オファー ID をコピーします。

      :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-monetized-apps-preview-offer-id.png" alt-text="プレビュー オファー ID" border="true" :::

    > [!NOTE]
    > パブリック オファー ID とは異なり、プレビュー オファー ID は *-preview サフィックスで認識* できます。 たとえば、**publisherId.offerId-preview。**

## <a name="configure-your-app-with-the-preview-offer-id"></a>プレビュー オファー ID を使用してアプリを構成する

開始する前に、開発者アカウントを使用して開発者向けポータルにサインインし、ユーザーがサブスクリプション プランをアプリ ストアTeamsします。

プレビュー オファー ID を生成した後、オファー ID をアプリにリンクTeamsします。 オファー ID をリンクするには、次の方法を使用します。

1. 開発者ポータル [に移動し](https://dev.teams.microsoft.com/) 、開発者資格情報を使用してサインインします。
1. 左側 **のウィンドウから** [アプリ] を選択します。
1. SaaS オファーをリンクするアプリを選択します。
1. [**プランと価格] を** 選択し、[プラン ID **Publisherプラン ID**] **を入力します**。  
  オファー ID に -preview サフィックス *が含まれているか確認* します。
1. [表示 **] を** 選択してサブスクリプション プランをプレビューします。
1. [アプリのサブスクリプション] の下に表示されている **プランを確認し、[** 保存] を **選択します**。

    :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-add-offer-id.png" alt-text="オファー ID の追加" :::

subscriptionOffer プロパティがアプリ マニフェストに追加されます。

```json
"subscriptionOffer": {
     "offerId": "publisherId.offerId-preview"  
     }
```

>[!NOTE]
> [アプリ] サブスクリプションの *横にある [プレビュー* プラン] というラベル **を** 確認して、オファーがプレビュー オファーか確認します。

## <a name="sideload-the-app-to-teams"></a>アプリをサイドロードしてTeams

プレビュー オファー ID を使用してアプリを構成した後、更新されたアプリ パッケージを作成し、Teams にアップロードして、エンドツーエンドの購入エクスペリエンスをテストします。 詳細については、「アプリのアップロード[」を参照Microsoft Teams](../../apps-upload.md)。 開発者ポータルで [**プレビュー] Teams** を選択して、Teamsクライアントでアプリをすばやく起動Teamsすることもできます。

プレビュー オファーがアプリ マニフェストで指定され、プレビュー対象ユーザーがプランのパートナー センターで定義されている場合、ユーザーは [サブスクリプションの購入] ボタン **を表示** できます。

:::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-buy-subscription.png" alt-text="サブスクリプションを購入する" border="true":::

### <a name="error-scenarios"></a>エラーシナリオ

* プラン ID が指定されているが、ユーザーがパートナー センターで定義されているプレビュー対象ユーザーの一部ではない場合、[サブスクリプションの購入] ボタンは有効ではなく、アプリはユーザーに次の警告メッセージを表示します。

  -preview でプラン **が見つかりません**。 プレビュー対象ユーザーに確認してください。

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-audience.png" alt-text="プレブ対象ユーザーなし" border="true" :::

* アプリ マニフェストで指定されたオファー ID がプレビュー オファーではない場合、アプリはユーザーに対して次の警告メッセージを表示し、サイドローディングは無効になります。
  
  これはプレビュー オファーではない。 必ず - **preview をオファー** ID に追加してください。

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-offer-id.png" alt-text="no -preview" border="true" :::

## <a name="see-also"></a>関連項目

* [SaaS オファーをアプリにMicrosoft Teamsする](include-saas-offer.md)
* [サービスとしてのソフトウェアの作成 (SaaS) オファー](include-saas-offer.md#create-your-saas-offer)
* [SaaS オファーのプレビュー対象ユーザーを追加する](/azure/marketplace/create-new-saas-offer-preview)
* [プレビュー作成フェーズ](/azure/marketplace/review-publish-offer)
* [商用マーケットプレースへのオファーの確認と発行](/azure/marketplace/review-publish-offer#validation-and-publishing-steps)
