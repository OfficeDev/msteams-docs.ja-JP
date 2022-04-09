---
title: アプリの収益化のためのアプリ内購入フロー
description: チームアプリでアプリ内購入と試用機能を実装するために必要な基本的なタスクと概念について説明します。
author: v-npaladugu
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 4f606363b62126731afcbc8b7f065951d8cd1a13
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2022
ms.locfileid: "64736878"
---
# <a name="in-app-purchases"></a>アプリ内購入

Microsoft Teams は、アプリ内購入を実装して無料から有料の Teams アプリにアップグレードするために使用できる API を提供します。 アプリ内購入では、アプリ内から直接ユーザーを無料プランから有料プランに変換できます。

> [!NOTE]
> Teamsアプリのアプリ内購入は、現在、[**開発者プレビュー**](/microsoftteams/platform/resources/dev-preview/developer-preview-intro)でのみ利用可能です。

## <a name="implement-in-app-purchases"></a>アプリ内購入の実装

アプリ内購入エクスペリエンスをアプリのユーザーに提供するには、次の情報を確認します。

* アプリは [Teams クライアント SDK ライブラリ](https://github.com/OfficeDev/microsoft-teams-library-js)に基づいて構築されています。

* アプリは、トランザクション可能な [SaaS オファー](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)で有効になっています。

* アプリは [RSC アクセス許可](#update-manifest)で有効になっています。

* アプリは [`openPurchaseExperience`API](#purchase-experience-api) で呼び出されます。

アプリ内購入エクスペリエンスは、`manifest.json` ファイルを更新するか、**[開発者ポータル]** の **[アクセス許可]** セクションから **[アプリ内購入オファーを表示]** を有効にすることで有効にできます。

### <a name="update-manifest"></a>マニフェストを更新する

アプリ内購入エクスペリエンスを有効にするには、開発者ポータルの [アクセス許可] セクションから RSC の permissions.se オファーを追加して、Teams アプリの `manifest.json` ファイルを更新します。 これにより、アプリユーザーはアプリの有料バージョンにアップグレードして、新しい機能の使用を開始できます。 アプリ マニフェストの更新プログラムは次のとおりです。

```json

"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "InAppPurchase.Allow.User",
                "type": "Delegated"
            }
        ]
    }
}
```

### <a name="purchase-experience-api"></a>購入エクスペリエンス API

アプリのアプリ内購入をトリガーするには、Web アプリから `openPurchaseExperience` API を呼び出します。

アプリから API を呼び出す例を次に示します。

```json
<body> 
<div> 
<div class="sectionTitle">openPurchaseExperience</div> 
<button onclick="openPurchaseExperience()">openPurchaseExperience</button> 
</div> 
</body> 
<script> 
   function openPurchaseExperience() {
      microsoftTeams.initialize();
      let callbackcalled = false;
      microsoftTeams.monetization.openPurchaseExperience((e) => {
      console.log("callback is being called");
      callbackcalled = true;  
      if (!!e && typeof e !== "string") {
            e = JSON.stringify(e);
            alert(e);
        }
        return;
      });
      console.log("after callback: ",callbackcalled);
    } 
</script> 
```

## <a name="end-user-in-app-purchasing-experience"></a>エンド ユーザーのアプリ内購入エクスペリエンス

次の例は、*Contoso Tasks for Teams* と呼ばれる架空の Teams アプリのサブスクリプション プランを購入するユーザーを示しています。

1. Teams **ストア** で、アプリを見つけて選択します。

1. アプリの詳細ダイアログで、**[サブスクリプションの購入]** または **[自分用に追加]** を選択します。

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplancontoso.png" alt-text="選択したアプリのサブスクリプションを購入します。" border="true":::

1. **[自分用に追加]** は、アプリの無料試用版を提供し、後で有料版に **アップグレード** します。

    :::image type="content" source="~/assets/images/saas-offer/upgradeapp.png" alt-text="選択したアプリのサブスクリプションへのアップグレード。" lightbox="../../../../assets/images/saas-offer/upgradeapp.png" border="true":::

1. **[サブスクリプション プランを選ぶ]** ダイアログでプランを選択し、**[チェックアウト]** を選択します。

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplancontoso.png" alt-text="適切なサブスクリプション プランを選択する。" lightbox="../../../../assets/images/saas-offer/choosingsubscriptionplancontoso.png" border="true":::

1. トランザクションを完了し、**[今すぐ構成]** を選択してサブスクリプションを設定します。

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-configure-now.png" alt-text="サブスクリプションを設定する。" lightbox="../../../../assets/images/saas-offer/saas-offer-configure-now.png" border="true":::

    :::image type="content" source="~/assets/images/saas-offer/getstarted.png" alt-text="サブスクリプションのランディング ページ。" lightbox="../../../../assets/images/saas-offer/getstarted.png" border="true":::

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [収益化されたアプリのテスト プレビュー](~/concepts/deploy-and-publish/appsource/prepare/Test-preview-for-monetized-apps.md)

## <a name="see-also"></a>関連項目

* [Microsoft Teams アプリに SaaS オファーを含める](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
* [サービスとしてのソフトウェア (SaaS) オファーを作成する](include-saas-offer.md#create-your-saas-offer)
