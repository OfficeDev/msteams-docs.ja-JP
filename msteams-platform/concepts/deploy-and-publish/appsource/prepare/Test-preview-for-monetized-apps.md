---
title: 収益化されたアプリのテスト プレビュー
author: v-ypalikila
description: オファーを公開する前に、Teams アプリの SaaS プレビュー オファーを作成してテストします。 プレビュー オファー ID を作成し、プレビュー オファー ID を使用してアプリを構成し、サイドロードします。
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: high
ms.openlocfilehash: 98b9876a93fe6040cf66a16475fe7fdacf98a520
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100792"
---
# <a name="test-preview-for-monetized-apps"></a>収益化されたアプリのテスト プレビュー

サービスとしてのソフトウェア (SaaS) オファーを作成し、Teams で収益化されたアプリのエンドツーエンドの購入エクスペリエンスをテストできます。 Teams アプリのプレビュー対象ユーザーとして追加されたユーザーは、公開する前に SaaS オファーを確認できます。

## <a name="create-a-preview-offer-id"></a>プレビュー オファー ID を作成する

プレビュー オファー ID は、パートナー センターの **AppSource プレビュー** リンクから生成できます。 SaaS オファーがプレビュー作成フェーズにあることを確認します。 プレビュー オファー ID を生成するには:

1. [パートナー センター](https://go.microsoft.com/fwlink/?linkid=2166002)に移動し、開発者の資格情報を使用してサインインします。
1. **マーケットプレイスのオファー** を選択します。
1. プレビューする SaaS オファーを選択します。
1. SaaS オファーの[プレビュー対象ユーザー](/azure/marketplace/create-new-saas-offer-preview)を追加します。
1. **[ライブに移動]** の下の **[AppSource プレビュー]** リンクを選択して、*publisherId.offerId-preview* 形式のブラウザー アドレス バーでプレビュー オファー ID を見つけます。

    :::image type="content" source="../../../../assets/images/apps-in-meetings/publish-status-publisher-signoff.png" alt-text="プレビュー オファー ID" :::

1. ブラウザーのアドレス バーからプレビュー オファー ID をコピーします。

      :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-monetized-apps-preview-offer-id.png" alt-text="プレビュー オファー ID" :::

    > [!NOTE]
    > Unlike a public offer ID, the Preview offer ID can be recognized with the *-preview* suffix. For example, **publisherId.offerId-preview**.

## <a name="configure-your-app-with-the-preview-offer-id"></a>プレビュー オファー ID を使用してアプリを構成する

開始する前に、ユーザーが Teams ストアでサブスクリプション プランを確認できるように、**プレビュー対象ユーザー** を備えた開発者アカウントを使用して **開発者ポータル** にサインインします。

After you've generated your Preview offer ID, link the offer ID to your Teams app. To link the offer ID:

1. [開発者ポータル](https://dev.teams.microsoft.com/)に移動し、開発者の資格情報を使用してサインインします。
1. 左側のウィンドウから **[アプリ]** を選択します。
1. SaaS オファーをリンクするアプリを選択します。
1. **[プランと価格]** を選択し、**発行元 ID** と **オファー ID** を入力します。  
  オファー ID に *-preview* サフィックスが含まれていることを確認してください。
1. **[表示]** を選択して、サブスクリプション プランをプレビューします。
1. **[アプリのサブスクリプション]** の下にリストされているプランを確認し、**[保存]** を選択します。

    :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-add-offer-id.png" alt-text="オファー ID の追加" :::

subscriptionOffer プロパティがアプリ マニフェストに追加されます。

```json
"subscriptionOffer": {
     "offerId": "publisherId.offerId-preview"  
     }
```

>[!NOTE]
> **[アプリのサブスクリプション]** の横にあるラベル *[プレビュー オファー]* をチェックして、オファーがプレビュー オファーであるかどうかを確認します。

## <a name="sideload-the-app-to-teams"></a>アプリを Teams にサイドロードする

プレビュー オファー ID を使用してアプリを構成した後、更新されたアプリ パッケージを作成し、それを Teams にアップロードして、エンドツーエンドの購入エクスペリエンスをテストします。 詳細については、「[Microsoft Teams でのアプリのアップロード](../../apps-upload.md)」を参照してください。 また、Teams の開発者ポータルの **[Teams のプレビュー]** を選択して、Teams クライアントでアプリをすばやく起動することもできます。

プレビュー オファーがアプリ マニフェストで指定され、プレビュー対象ユーザーがオファーのパートナー センターで定義されている場合、ユーザーには **[サブスクリプションの購入]** ボタンが表示されます。

:::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-buy-subscription.png" alt-text="サブスクリプションを購入する":::

### <a name="error-scenarios"></a>エラー シナリオ

* オファー ID が指定されているが、ユーザーがパートナー センターで定義された **プレビュー対象ユーザー** の一部ではない場合、**[サブスクリプションの購入]** ボタンは有効にならず、アプリはユーザーに次の警告メッセージを表示します。

  **-preview** でプランが見つかりません。 プレビュー対象ユーザーであることを確認してください。

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-audience.png" alt-text="プレビュー対象ユーザーなし" :::

* アプリ マニフェストで指定されたオファー ID がプレビュー オファーでない場合、アプリはユーザーに次の警告メッセージを表示し、サイドローディングは無効になります。
  
  これはプレビュー オファーではありません。 必ず **-preview** をオファー ID に追加してください。

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-offer-id.png" alt-text="-preview なし" :::

## <a name="see-also"></a>関連項目

* [Microsoft Teams アプリに SaaS オファーを含める](include-saas-offer.md)
* [サービスとしてのソフトウェア (SaaS) オファーを作成する](include-saas-offer.md#create-your-saas-offer)
* [SaaS オファーのプレビュー対象ユーザーを追加する](/azure/marketplace/create-new-saas-offer-preview)
* [プレビュー作成フェーズ](/azure/marketplace/review-publish-offer)
* [商用マーケットプレースへのオファーの確認と発行](/azure/marketplace/review-publish-offer#validation-and-publishing-steps)
