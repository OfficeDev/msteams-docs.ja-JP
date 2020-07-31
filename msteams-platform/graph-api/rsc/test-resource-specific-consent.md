---
title: Teams でのリソース固有の同意のテスト
description: Postman を使用する Teams でのリソース固有の同意のテストの詳細
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: How-to
keywords: teams authorization OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: a7384222e5e4cba164f918186ce53b4c1b702016
ms.sourcegitcommit: 3e94edba28e9e1252b6a6ba35d4df32710dfc5d4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "46531267"
---
# <a name="test-resource-specific-consent-permissions--in-teams"></a>Teams でのリソース固有の同意権限をテストする

リソース固有の同意 (RSC) は Microsoft Teams と Graph API の統合で、アプリが API エンドポイントを使用して組織内の特定のチームを管理できるようにします。 [リソース固有の同意 (RSC) — Microsoft Teams GRAPH API](resource-specific-consent.md)を*参照*してください。  

> [!NOTE]
>RSC のアクセス許可をテストするには、Teams アプリのマニフェストファイルに、次のフィールドで設定された**Webapplicationinfo**キーが含まれている必要があります。
>
> - **id** : azure ad アプリ id については、「 [azure ad ポータルでアプリを登録](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)する *」を参照してください*。
> - **resource** : 任意の文字列。「 [Teams アプリのマニフェストを更新する](resource-specific-consent.md#update-your-teams-app-manifest)」のメモを参照して*ください*。
> - **アプリケーションのアクセス許可**-アプリの RSC アクセス許可については、「[リソース固有のアクセス許可](resource-specific-consent.md#resource-specific-permissions) *」を参照してください*。

```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
         "Channel.Create.Group",
         "Channel.Delete.Group",
         "ChannelMessage.Read.Group",
         "ChannelSettings.Read.Group",
         "ChannelSettings.Edit.Group",
         "Member.Read.Group",
         "Owner.Read.Group",
         "TeamsApp.Read.Group",
         "TeamsTab.Read.Group",
         "TeamsTab.Create.Group",
         "TeamsTab.Edit.Group",
         "TeamsTab.Delete.Group",
         "TeamSettings.Read.Group",
         "TeamSettings.Edit.Group"
      ]
   }
```

>[!IMPORTANT]
>アプリのマニフェストには、アプリに必要な RSC アクセス許可のみが含まれています。

## <a name="test-added-rsc-permissions-using-the-postman-app"></a>Postman アプリを使用して、追加された RSC アクセス許可をテストする

RSC アクセス許可が API 要求ペイロードによって受け入れられているかどうかを確認するには、 [RSC JSON テストコード](test-rsc-json-file.md)をローカル環境にコピーし、次の値を更新する必要があります。

1. `azureADAppId`-アプリの Azure AD アプリ id。
1. `azureADAppSecret`-Azure AD アプリシークレット (パスワード)
1. `token_scope`-トークンに値を設定するには、スコープが必要です。https://graph.microsoft.com/.default
1. `teamGroupId`— Teams クライアントからチームグループ id を取得するには、次のようにします。

> [!div class="checklist"]
>
> * Teams クライアントで、左端のナビゲーションバーにある [ **teams** ] を選択します。
> * アプリがインストールされているチームをドロップダウンメニューから選択します。
> * [**その他のオプション**] アイコン (&#8943;) を選択します。
> * [**チームへのリンクの取得**] を選択する 
> * 文字列から**groupId**値をコピーして保存します。

### <a name="using-postman"></a>Postman を使用する

> [!div class="checklist"]
>
> * [Postman](https://www.postman.com)アプリを開きます。
> * [**ファイル**  =>  の**インポート**] [  =>  **インポートファイル**] を選択して、更新された JSON ファイルを環境からアップロードします。  
> * [**コレクション**] タブを選択します。 
> * **テスト RSC**の横にある山形 (>) を選択して、詳細ビューを展開し、API 要求を表示します。

API 呼び出しごとに、アクセス許可のコレクション全体を実行します。 アプリのマニフェストで指定したアクセス許可は成功するはずですが、指定されていない場合は、HTTP 403 状態コードで失敗する必要があります。 すべての応答状態コードを確認して、アプリの RSC アクセス許可の動作が期待どおりかどうかを確認します。

>[!NOTE]
>特定の削除および読み取り API 呼び出しをテストするには、これらのインスタンスシナリオを JSON ファイルに追加します。

## <a name="test--revoked-rsc-permissions-using-postman"></a>[Postman](https://www.postman.com/)を使用して失効した RSC アクセス許可をテストする

> [!div class="checklist"]
>
> * 特定のチームからアプリをアンインストールします。
> * [Postman を使用して、追加された RSC のアクセス許可をテスト](#test-added-rsc-permissions-using-the-postman-app)するには、上記の手順に従います。
> * すべての応答状態コードを調べて、成功した特定の API 呼び出しが HTTP 403 状態コードで失敗したことを確認します。

> [!div class="nextstepaction"]
>
> [Graph API と Teams の詳細情報](/graph/api/resources/teams-api-overview?view=graph-rest-1.0)
