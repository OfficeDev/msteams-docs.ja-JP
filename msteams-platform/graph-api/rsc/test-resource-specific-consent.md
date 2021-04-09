---
title: Teams でリソース固有の同意のアクセス許可をテストする
description: Postman を使用して Teams でリソース固有の同意をテストする詳細
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: teams 承認 OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 0d3d1c895c77bb417a9fdd84e319103485aa8944
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634709"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Teams でリソース固有の同意のアクセス許可をテストする

リソース固有の同意 (RSC) は、Microsoft Teams と Graph API の統合であり、アプリで API エンドポイントを使用して組織内の特定のチームを管理できます。 詳細については、「リソース固有の [同意 (RSC) - Microsoft Teams Graph API」を参照してください](resource-specific-consent.md)。

> [!NOTE]
> RSC アクセス許可をテストするには、Teams アプリ マニフェスト ファイルに、次のフィールドが設定された **webApplicationInfo** キーを含める必要があります。
>
> - **id**: Azure ADアプリ ID については、「Azure アプリ ポータルにアプリを登録する [」をADしてください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
> - **resource**: 任意の文字列は、「Teams アプリ マニフェストの更新  [」のノートを参照してください。](resource-specific-consent.md#update-your-teams-app-manifest)
> - **アプリケーションのアクセス許可**: アプリの RSC アクセス許可については、「リソース固有の [アクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。

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

> [!IMPORTANT]
> アプリ マニフェストには、アプリに付与する RSC アクセス許可のみを含める必要があります。

## <a name="test-added-rsc-permissions-using-the-postman-app"></a>Postman アプリを使用して追加された RSC アクセス許可をテストする

RSC アクセス許可が API 要求ペイロードによって付与されているかどうかを確認するには [、RSC JSON](test-rsc-json-file.md) テスト コードをローカル環境にコピーし、次の値を更新する必要があります。

* `azureADAppId`: アプリの Azure AD ID
* `azureADAppSecret`: Azure AD アプリ シークレット (パスワード)
* `token_scope`: トークンを取得するにはスコープが必要です。 https://graph.microsoft.com/.default
* `teamGroupId`: 次のように Teams クライアントからチーム グループ ID を取得できます。

  > [!div class="checklist"]
  >
  > * Teams クライアントで、左上のナビゲーション バーから **[Teams]** を選択します。
  > * ドロップダウン メニューからアプリがインストールされているチームを選択します。
  > * [その他 **のオプション]** アイコンを選択します (&#8943;)
  > * [チーム **へのリンクを取得する] を選択します。** 
  > * 文字列から **groupId 値をコピー** して保存します。

### <a name="use-postman"></a>Postman の使用

1. Postman [アプリを開](https://www.postman.com) きます。
2. [**ファイル**  >  **インポート ファイル**  >  **] を選択** して、更新された JSON ファイルを環境からアップロードします。  
3. [コレクション **] タブを選択** します。 
4. テスト RSC の横にあるシェブロンを選択して詳細ビューを **>** 展開し、API 要求を表示します。

API 呼び出しごとにアクセス許可コレクション全体を実行します。 アプリ マニフェストで指定したアクセス許可は成功する必要があります。指定されていないアクセス許可は HTTP 403 状態コードで失敗する必要があります。 すべての応答状態コードを確認して、アプリ内の RSC アクセス許可の動作が期待を満たしている状態を確認します。

> [!NOTE]
> 特定の DELETE および READ API 呼び出しをテストするには、それらのインスタンス シナリオを JSON ファイルに追加します。

## <a name="test-revoked-rsc-permissions-using-postman"></a>Postman を使用して取り消された RSC アクセス [許可をテストする](https://www.postman.com/)

1. 特定のチームからアプリをアンインストールします。
2. Postman を使用して [RSC アクセス許可を追加したテストの手順に従います](#test-added-rsc-permissions-using-the-postman-app)。
3. すべての応答状態コードを確認して、特定の API 呼び出しが成功し **、HTTP 403** 状態コードで失敗したと確認します。

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [Microsoft Graph API と Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

