---
title: リソース固有の同意のアクセス許可をテストTeams
description: コード サンプルを使用して Postman を使用Teamsリソース固有の同意をテストする詳細
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: teams 承認 OAuth SSO Azure AD rsc Postman Graph
ms.openlocfilehash: fe3819b0da9783a6cf3aacac08a6045337e27600
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212483"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>リソース固有の同意のアクセス許可をテストTeams

> [!NOTE]
> チャット スコープに対するリソース固有の同意は、パブリック開発者 [プレビューでのみ利用](../../resources/dev-preview/developer-preview-intro.md) できます。

リソース固有の同意 (RSC) は、Microsoft Teams と Graph API の統合であり、アプリは API エンドポイントを使用して組織内の特定のリソース (チームまたはチャット) を管理できます。 詳細については、「リソース固有[の同意 (RSC) - Microsoft Teams Graph API 」を参照してください](resource-specific-consent.md)。

> [!NOTE]
> RSC アクセス許可をテストするには、Teamsアプリ マニフェスト ファイルに、次のフィールドが設定された **webApplicationInfo** キーを含める必要があります。
>
> - **id**: アプリ ID Azure AD、アプリをポータルに登録 [するをAzure ADしてください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。
> - **resource**: 任意の文字列は、「アプリ マニフェストの更新 [」のTeams参照してください](resource-specific-consent.md#update-your-teams-app-manifest)。
> - **アプリケーションのアクセス許可**: アプリの RSC アクセス許可については、「リソース固有の [アクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。

## <a name="example-for-a-team"></a>チームの例
```json
"webApplicationInfo":{
    "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource":"https://AnyString",
    "applicationPermissions":[
        "TeamSettings.Read.Group",
        "TeamSettings.ReadWrite.Group",
        "ChannelSettings.Read.Group",
        "ChannelSettings.ReadWrite.Group",
        "Channel.Create.Group",
        "Channel.Delete.Group",
        "ChannelMessage.Read.Group",
        "TeamsAppInstallation.Read.Group",
        "TeamsTab.Read.Group",
        "TeamsTab.Create.Group",
        "TeamsTab.ReadWrite.Group",
        "TeamsTab.Delete.Group",
        "TeamMember.Read.Group",
        "TeamsActivity.Send.Group"
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
        "OnlineMeeting.ReadBasic.Chat",
        "Calls.AccessMedia.Chat",
        "Calls.JoinGroupCalls.Chat",
        "TeamsActivity.Send.Chat"
    ]
   }
```

> [!IMPORTANT]
> アプリ マニフェストには、アプリに付与する RSC アクセス許可のみを含める必要があります。

>[!NOTE]
>アプリがチームスコープとチャット スコープの両方でのインストールをサポートすることを意図している場合は、チームとチャットの両方のアクセス許可を同じマニフェストで指定できます `applicationPermissions` 。

>アプリが通話/メディア API にアクセスすることを意図している場合は `webApplicationInfo.Id` 、Azure Bot Service のAzure ADアプリ ID[である必要があります](/graph/cloud-communications-get-started#register-a-bot)。

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Postman アプリを使用してチームに追加された RSC アクセス許可をテストする

RSC アクセス許可が API 要求ペイロードによって付与されているかどうかを確認するには、チームの [RSC JSON](test-team-rsc-json-file.md) テスト コードをローカル環境にコピーし、次の値を更新する必要があります。

* `azureADAppId`: アプリのAzure AD ID です。
* `azureADAppSecret`: アプリAzure ADパスワード。
* `token_scope`: トークンを取得するには、スコープが必要です。 に値を設定します https://graph.microsoft.com/.default 。
* `teamGroupId`: 次のように、チーム グループ ID をクライアントTeams取得できます。

    1. クライアントで、Teams **バーから**[Teams] を選択します。
    2. ドロップダウン メニューからアプリがインストールされているチームを選択します。
    3. [その他 **のオプション]** アイコンを選択します (&#8943;)。
    4. [チーム **へのリンクを取得する] を選択します**。 
    5. 文字列から **groupId 値をコピー** して保存します。

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Postman アプリを使用してチャットに追加された RSC アクセス許可をテストする

RSC アクセス許可が API 要求ペイロードによって付与されているかどうかを確認するには、チャットの [RSC JSON](test-chat-rsc-json-file.md) テスト コードをローカル環境にコピーし、次の値を更新する必要があります。

* `azureADAppId`: アプリのAzure AD ID です。
* `azureADAppSecret`: アプリAzure ADパスワード。
* `token_scope`: トークンを取得するには、スコープが必要です。 に値を設定します https://graph.microsoft.com/.default 。
* `tenantId`: テナントの名前Azure ADオブジェクト ID です。
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

* [Microsoft Graph API と Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)
* [リソース固有の同意](~/graph-api/rsc/resource-specific-consent.md)
