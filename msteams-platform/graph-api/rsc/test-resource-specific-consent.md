---
title: リソース固有の同意のアクセス許可をテストTeams
description: コード サンプルを使用して Postman を使用Teamsリソース固有の同意をテストする詳細
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: teams 承認 OAuth SSO Microsoft Azure Active Directory (Azure AD) rsc Postman Graph
ms.openlocfilehash: 15a2a80a8f1ce280b462ed6e6e99242fb30f0dc3
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518122"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>リソース固有の同意のアクセス許可をテストTeams

> [!NOTE]
> チャット スコープに対するリソース固有の同意は、パブリック開発者 [プレビューでのみ利用](../../resources/dev-preview/developer-preview-intro.md) できます。

リソース固有の同意 (RSC) は、Microsoft Teams と Graph API の統合であり、アプリは API エンドポイントを使用して組織内の特定のリソース (チームまたはチャット) を管理できます。 詳細については、「リソース固有の[同意 (RSC) - Microsoft Teams Graph参照してください](resource-specific-consent.md)。

## <a name="prerequisites"></a>前提条件

テストする前に、リソース固有の同意のために次のアプリ マニフェストの変更を確認してください。

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.12 の RSC アクセス許可</b></summary>

次の [値を使用して、WebApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加します。

|名前| 種類 | 説明|
|---|---|---|
|`id` |String |ユーザー Microsoft Azure Active Directory (Azure AD) アプリ ID。 詳細については、「アプリを[アプリ (Microsoft Azure Active Directory)](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal) ポータルAzure ADしてください。|
|`resource`|String| このフィールドは RSC で操作を行う必要がありますが、エラー応答を回避するには、値を追加して値を指定する必要があります。任意の文字列が実行します。|

アプリに必要なアクセス許可を指定します。

|名前| 種類 | 説明|
|---|---|---|
|`authorization`|オブジェクト|アプリを実行する必要があるアクセス許可の一覧。 詳細については、「承認」を [参照してください](../../resources/schema/manifest-schema.md#authorization)。|

チームの RSC の例

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp"
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "TeamSettings.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamSettings.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "ChannelSettings.Read.Group",
                "type": "Application"
            },
            {
                "name": "ChannelSettings.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "Channel.Create.Group",
                "type": "Application"
            },
            {
                "name": "Channel.Delete.Group",
                "type": "Application"
            },
            {
                "name": "ChannelMessage.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsAppInstallation.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Create.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Delete.Group",
                "type": "Application"
            },
            {
                "name": "TeamMember.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsActivity.Send.Group",
                "type": "Application"
            }
        ]    
    }
}
```

チャット内の RSC の例

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp"
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "ChatSettings.Read.Chat",
                "type": "Application"
            },
            {
                "name": "ChatSettings.ReadWrite.Chat",
                "type": "Application"
            },
            {
                "name": "ChatMessage.Read.Chat",
                "type": "Application"
            },
            {
                "name": "ChatMember.Read.Chat",
                "type": "Application"
            },
            {
                "name": "Chat.Manage.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Read.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Create.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Delete.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.ReadWrite.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsAppInstallation.Read.Chat",
                "type": "Application"
            },
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            },
            {
                "name": "Calls.AccessMedia.Chat",
                "type": "Application"
            },
            {
                "name": "Calls.JoinGroupCalls.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsActivity.Send.Chat",
                "type": "Application"
            }
        ]    
    }
}
```
    
> [!NOTE]
> アプリがチームスコープとチャット スコープの両方でのインストールをサポートすることを意図している場合は、チームとチャットの両方のアクセス許可を同じマニフェストで指定できます `authorization`。

</details>

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.11 以前の RSC アクセス許可</b></summary>

次の [値を使用して、WebApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加します。

|名前| 種類 | 説明|
|---|---|---|
|`id` |String |ユーザー Microsoft Azure Active Directory (Azure AD) アプリ ID。 詳細については、「アプリを[アプリ (Microsoft Azure Active Directory)](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal) ポータルAzure ADしてください。|
|`resource`|String| このフィールドは RSC で操作を行う必要がありますが、エラー応答を回避するには、値を追加して値を指定する必要があります。任意の文字列が実行します。|
|`applicationPermissions`|文字列の配列|アプリの RSC アクセス許可。 詳細については、「リソース固有 [のアクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。|

チームの RSC の例

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
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

チャット内の RSC の例

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
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

<br>

> [!NOTE]
> アプリがチームスコープとチャット スコープの両方でのインストールをサポートすることを意図している場合は、チームとチャットの両方のアクセス許可を同じマニフェストで指定できます `applicationPermissions`。
    
</details>

> [!IMPORTANT]
> アプリ マニフェストには、アプリに付与する RSC アクセス許可のみを含める必要があります。

> [!NOTE]
> アプリが通話/メディア API `webApplicationInfo.Id` にアクセスすることを意図している場合は、[Azure Bot Service](/graph/cloud-communications-get-started#register-a-bot) の Microsoft Azure Active Directory (Azure AD) アプリ ID である必要があります。

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Postman アプリを使用してチームに追加された RSC アクセス許可をテストする

RSC アクセス許可が API 要求ペイロードによって付与されているかどうかを確認するには、チームの [RSC JSON](test-team-rsc-json-file.md) テスト コードをローカル環境にコピーし、次の値を更新する必要があります。

* `azureADAppId`: アプリのMicrosoft Azure Active Directory (Azure AD) アプリ ID。
* `azureADAppSecret`: アプリMicrosoft Azure Active Directory (Azure AD) のパスワード。
* `token_scope`: トークンを取得するには、スコープが必要です。 に値を設定します https://graph.microsoft.com/.default。
* `teamGroupId`: 次のように、チーム グループ ID をクライアントTeams取得できます。

    1. クライアントで、**Teamsバーから** [Teams] を選択します。
    2. ドロップダウン メニューからアプリがインストールされているチームを選択します。
    3. [その他 **のオプション]** アイコンを選択します (&#8943;)。
    4. [チーム **へのリンクを取得する] を選択します**。 
    5. 文字列から **groupId 値をコピー** して保存します。

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Postman アプリを使用してチャットに追加された RSC アクセス許可をテストする

RSC アクセス許可が API 要求ペイロードによって付与されているかどうかを確認するには、チャットの [RSC JSON](test-chat-rsc-json-file.md) テスト コードをローカル環境にコピーし、次の値を更新する必要があります。

* `azureADAppId`: アプリのMicrosoft Azure Active Directory (Azure AD) アプリ ID。
* `azureADAppSecret`: アプリMicrosoft Azure Active Directory (Azure AD) のパスワード。
* `token_scope`: トークンを取得するには、スコープが必要です。 に値を設定します https://graph.microsoft.com/.default。
* `tenantId`: テナントの名前Microsoft Azure Active Directory (Azure AD) オブジェクト ID。
* `chatId`: 次のように、Web クライアントからチャット スレッド id をTeams *取得* できます。

    1. Web クライアントTeams、左側 **のナビゲーション** バーから [チャット] を選択します。
    2. アプリがインストールされているチャットをドロップダウン メニューから選択します。
    3. Web URL をコピーし、文字列からチャット スレッド ID を保存します。
![Web URL からのチャット スレッド ID。](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>Postman の使用

1. Postman [アプリを開](https://www.postman.com) きます。
2. [**FileImportImport** >  >  **ファイル] を選択** して、更新された JSON ファイルを環境からアップロードします。  
3. [コレクション **] タブを選択** します。 
4. テスト **RSC** の横にある **>** シェブロンを選択して詳細ビューを展開し、API 要求を表示します。

API 呼び出しごとにアクセス許可コレクション全体を実行します。 アプリ マニフェストで指定したアクセス許可は成功する必要があります。指定されていないアクセス許可は HTTP 403 状態コードで失敗する必要があります。 すべての応答状態コードを確認して、アプリ内の RSC アクセス許可の動作が期待を満たしている状態を確認します。

> [!NOTE]
> 特定の DELETE および READ API 呼び出しをテストするには、それらのインスタンス シナリオを JSON ファイルに追加します。

## <a name="test-revoked-rsc-permissions-using-postman"></a>Postman を使用して取り消された RSC アクセス [許可をテストする](https://www.postman.com/)

1. 特定のリソースからアプリをアンインストールします。
2. チャットまたはチームの手順に従います。 
    1. [Postman を使用してチームに追加された RSC アクセス許可をテストします](#test-added-rsc-permissions-to-a-team-using-the-postman-app)。
    2. [Postman を使用して、チャットに追加された RSC アクセス許可をテストします](#test-added-rsc-permissions-to-a-chat-using-the-postman-app)。
3. すべての応答状態コードを確認して、HTTP 403 状態コードで特定の API 呼び出し **が失敗したと確認します**。

## <a name="see-also"></a>関連項目

* [Microsoft Graph API と Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)
* [リソース固有の同意](~/graph-api/rsc/resource-specific-consent.md)
