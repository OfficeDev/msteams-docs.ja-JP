---
title: リソース固有の同意のアクセス許可をテストTeams
description: Postman を使用したリソース固有の同意Teamsテストする詳細
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: teams 承認 OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 92c6d5d96c103fb5e0da6afd91357b5887b2ba10
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069083"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>リソース固有の同意のアクセス許可をテストTeams

> [!NOTE]
> チャット スコープに対するリソース固有の同意は、パブリック開発者 [プレビューでのみ利用](../../resources/dev-preview/developer-preview-intro.md) できます。

リソース固有の同意 (RSC) は、Microsoft Teams と Graph API の統合であり、アプリは API エンドポイントを使用して組織内の特定のリソース (チームまたはチャット) を管理できます。 詳細については、「リソース固有[の同意 (RSC) - Microsoft Teams Graph API 」を参照してください](resource-specific-consent.md)。

> [!NOTE]
> RSC アクセス許可をテストするには、Teamsアプリ マニフェスト ファイルに、次のフィールドが設定された **webApplicationInfo** キーを含める必要があります。
>
> - **id**: Azure ADアプリ ID については、「Azure アプリ ポータルにアプリを登録する [」をADしてください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
> - **resource**: 任意の文字列は、「アプリ マニフェストの更新 [」のTeams参照してください](resource-specific-consent.md#update-your-teams-app-manifest)。
> - **アプリケーションのアクセス許可**: アプリの RSC アクセス許可については、「リソース固有の [アクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。

## <a name="example-for-a-team"></a>チームの例
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

## <a name="example-for-a-chat"></a>チャットの例
```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
          "ChatSettings.Read.Chat",
          "ChatSettings.ReadWrite.Chat",
          "ChatMessage.Read.Chat",
          "ChatMember.Read.Chat",
          "Chat.Manage.Chat",
          "TeamsTab.Read.Chat",
          "TeamsTab.Create.Chat",
          "TeamsTab.Delete.Chat",
          "TeamsTab.ReadWrite.Chat",
          "TeamsAppInstallation.Read.Chat",
          "OnlineMeeting.ReadBasic.Chat"
      ]
   }
```

> [!IMPORTANT]
> アプリ マニフェストには、アプリに付与する RSC アクセス許可のみを含める必要があります。

>[!NOTE]
>アプリがチームスコープとチャット スコープの両方でのインストールをサポートすることを意図している場合は、チームとチャットの両方のアクセス許可を同じマニフェストで指定できます `applicationPermissions` 。

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Postman アプリを使用してチームに追加された RSC アクセス許可をテストする

RSC アクセス許可が API 要求ペイロードによって付与されているかどうかを確認するには、チームの [RSC JSON](test-team-rsc-json-file.md) テスト コードをローカル環境にコピーし、次の値を更新する必要があります。

* `azureADAppId`: アプリの Azure AD ID。
* `azureADAppSecret`: Azure ADパスワード。
* `token_scope`: トークンを取得するには、スコープが必要です。 に値を設定します https://graph.microsoft.com/.default 。
* `teamGroupId`: 次のように、チーム グループ ID をクライアントTeams取得できます。

    1. クライアントで、Teams **バーから**[Teams] を選択します。
    2. ドロップダウン メニューからアプリがインストールされているチームを選択します。
    3. [その他 **のオプション]** アイコンを選択します (&#8943;)。
    4. [チーム **へのリンクを取得する] を選択します**。 
    5. 文字列から **groupId 値をコピー** して保存します。

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Postman アプリを使用してチャットに追加された RSC アクセス許可をテストする

RSC アクセス許可が API 要求ペイロードによって付与されているかどうかを確認するには、チャットの [RSC JSON](test-chat-rsc-json-file.md) テスト コードをローカル環境にコピーし、次の値を更新する必要があります。

* `azureADAppId`: アプリの Azure AD ID。
* `azureADAppSecret`: Azure ADパスワード。
* `token_scope`: トークンを取得するには、スコープが必要です。 に値を設定します https://graph.microsoft.com/.default 。
* `tenantId`: テナントの名前または AAD オブジェクト ID。
* `chatId`: 次のように、Web クライアントからチャット スレッド id をTeams *取得* できます。

    1. Web クライアントTeams、左側 **のナビゲーション** バーから [チャット] を選択します。
    2. アプリがインストールされているチャットをドロップダウン メニューから選択します。
    3. Web URL をコピーし、文字列からチャット スレッド ID を保存します。
![Web URL からのチャット スレッド ID。](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>Postman の使用

1. Postman [アプリを開](https://www.postman.com) きます。
2. [**ファイル**  >  **インポート ファイル**  >  **] を選択** して、更新された JSON ファイルを環境からアップロードします。  
3. [コレクション **] タブを選択** します。 
4. テスト RSC の横にあるシェブロンを選択して詳細ビューを **>** 展開し、API 要求を表示します。

API 呼び出しごとにアクセス許可コレクション全体を実行します。 アプリ マニフェストで指定したアクセス許可は成功する必要があります。指定されていないアクセス許可は HTTP 403 状態コードで失敗する必要があります。 すべての応答状態コードを確認して、アプリ内の RSC アクセス許可の動作が期待を満たしている状態を確認します。

> [!NOTE]
> 特定の DELETE および READ API 呼び出しをテストするには、それらのインスタンス シナリオを JSON ファイルに追加します。

## <a name="test-revoked-rsc-permissions-using-postman"></a>Postman を使用して取り消された RSC アクセス [許可をテストする](https://www.postman.com/)

1. 特定のリソースからアプリをアンインストールします。
2. チャットまたはチームの手順に従います。 
    1. [Postman を使用してチームに追加された RSC アクセス許可をテストします](#test-added-rsc-permissions-to-a-team-using-the-postman-app)。
    2. [Postman を使用してチャットに追加された RSC アクセス許可をテストします](#test-added-rsc-permissions-to-a-chat-using-the-postman-app)。
3. すべての応答状態コードを確認して、HTTP 403 状態コードで特定の API 呼び出し **が失敗したと確認します**。

## <a name="see-also"></a>関連項目

[Microsoft Graph API と Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

