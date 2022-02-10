---
title: アプリの収益化のためのアプリ内購入フロー
description: Teams アプリでアプリ内購入と試用版機能を実装するために必要な基本的なタスクと概念について説明します。
author: v-npaladugu
ms.author: surbhigupta
ms.topic: how-to
localization_priority: Normal
ms.openlocfilehash: 90b1bf713e898a0f61c540e76ee5dde77603e70b
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518241"
---
# <a name="in-app-purchases"></a>アプリ内購入

Microsoft Teams無料アプリから有料アプリへのアップグレードにアプリ内購入を実装するために使用できる API をTeamsします。 アプリ内購入では、アプリ内からユーザーを無料プランから有料プランに直接変換できます。

> [!NOTE]
> 現在、開発者向けアプリTeamsアプリ内購入は、開発者向けプレビュー [**でのみ利用できます**](/microsoftteams/platform/resources/dev-preview/developer-preview-intro)。

## <a name="implement-in-app-purchases"></a>アプリ内購入の実装

アプリ内購入エクスペリエンスをアプリのユーザーに提供するには、次の情報を確認します。

* アプリは、クライアント [SDK Teams基に構築されます](https://github.com/OfficeDev/microsoft-teams-library-js)。

* アプリは、トランザクション可能な [SaaS オファーで有効になっています](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)。

* アプリは [RSC アクセス許可で有効になっています](#update-manifest)。

* アプリは API で呼び[出`openPurchaseExperience`されます](#purchase-experience-api)。

アプリ内購入エクスペリエンスは、**manifest.json** ファイルを更新するか、開発者ポータルの [アクセス許可] セクションで [アプリ内購入オファーを表示する] を有効にすることで **有効にできます**。

### <a name="update-manifest"></a>マニフェストの更新

アプリ内購入エクスペリエンスを有効にするには、RSC Teamsを追加して、アプリ **manifest.json** ファイルを更新します。 これにより、アプリ ユーザーは有料バージョンのアプリにアップグレードし、新しい機能の使用を開始できます。 アプリ マニフェストの更新プログラムは次のとおりです。

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

次の例は、Contoso *Tasks* for Teamsという架空のアプリのサブスクリプション プランを購入Teams。

1. [アプリストアTeams **で**、アプリを見つけて選択します。

1. アプリの詳細ダイアログで、[サブスクリプションの **購入] または [自分用** に **追加] を選択します**。 

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplancontoso.png" alt-text="選択したアプリのサブスクリプションを購入する。" border="true":::

    
1. **Add for me** offers a free trial version of the app and **later Upgrade** it to a paid version.

    :::image type="content" source="~/assets/images/saas-offer/upgradeapp.png" alt-text="選択したアプリのサブスクリプションへのアップグレード。" border="true":::

1. [サブスクリプションプラン **の選択] ダイアログで** 、プランを選択し、[チェックアウト] を **選択します**。

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplancontoso.png" alt-text="適切なサブスクリプション プランを選択します。" border="true":::

1. トランザクションを完了し、[ **今すぐ構成] を選択** してサブスクリプションを設定します。

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-configure-now.png" alt-text="サブスクリプションのセットアップ。" border="true":::

    :::image type="content" source="~/assets/images/saas-offer/getstarted.png" alt-text="サブスクリプションのランディング ページ。" border="true":::

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [収益化されたアプリのテスト プレビュー](~/concepts/deploy-and-publish/appsource/prepare/Test-preview-for-monetized-apps.md)

## <a name="see-also"></a>関連項目

* [SaaS オファーをアプリにMicrosoft Teamsする](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
* [サービスとしてのソフトウェアの作成 (SaaS) オファー](include-saas-offer.md#create-your-saas-offer)
