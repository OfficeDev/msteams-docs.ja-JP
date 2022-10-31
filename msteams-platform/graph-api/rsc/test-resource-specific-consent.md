---
title: Teams でリソース固有の同意アクセス許可をテストする
description: Postman とコード サンプルを使用した Teams でのリソース固有の同意のテストの詳細
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: teams 認証 OAuth SSO Microsoft Azure Active Directory (Azure AD) rsc Postman Graph
ms.openlocfilehash: ade66f40662140b86fcc9ae2e185fc10ea09d2f2
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791714"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Teams でリソース固有の同意アクセス許可をテストする

> [!NOTE]
> チャット スコープのリソース固有の同意は、[パブリック開発者向けプレビュー](../../resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

リソース固有の同意 (RSC) とは、アプリが API エンドポイントを使用して組織内の特定のリソース (チームまたはチャット) を管理できるようにする、Microsoft Teams と Graph API の統合です。 詳細については、「[リソース固有の同意 (RSC) — Microsoft Teams Graph API](resource-specific-consent.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

テストする前に、リソース固有の同意に対して次のアプリ マニフェストの変更を確認してください。

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.12 以降の RSC アクセス許可</b></summary>

次の値を使用して、アプリ マニフェストに [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーを追加します。

|名前| 型 | 説明|
|---|---|---|
|`id` |String |Azure ADアプリ ID。 詳細については、「[Azure AD ポータルでアプリを登録する](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)」を参照してください。|
|`resource`|String| このフィールドには RSC での操作はありませんが、エラー応答を回避するために値を追加し、値を指定する必要があります。任意の文字列が実行されます。|

アプリで必要なアクセス許可を指定します。

|名前| 型 | 説明|
|---|---|---|
|`authorization`|オブジェクト|アプリを実行する必要があるアクセス許可の一覧。 詳細については、「[承認](../../resources/schema/manifest-schema.md#authorization)」を参照してください。|

チーム内の RSC の例

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
> アプリがチーム スコープとチャット スコープの両方でのインストールをサポートすることを意図している場合は、チームとチャットの両方のアクセス許可を `authorization` の下の同じマニフェストで指定できます。

</details>

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.11 以前の RSC アクセス許可</b></summary>

次の値を使用して、アプリ マニフェストに [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーを追加します。

|名前| 型 | 説明|
|---|---|---|
|`id` |String |Azure ADアプリ ID。 詳細については、「[Azure AD ポータルでアプリを登録する](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)」を参照してください。|
|`resource`|String| このフィールドには RSC での操作はありませんが、エラー応答を回避するために値を追加し、値を指定する必要があります。任意の文字列が実行されます。|
|`applicationPermissions`|文字列の配列|アプリの RSC アクセス許可。 詳細については、「[リソース固有のアクセス許可](resource-specific-consent.md#resource-specific-permissions)」を参照してください。|

チーム内の RSC の例

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
> アプリがチーム スコープとチャット スコープの両方でのインストールをサポートすることを意図している場合は、チームとチャットの両方のアクセス許可を `applicationPermissions` の下の同じマニフェストで指定できます。

</details>

> [!IMPORTANT]
> アプリ マニフェストには、アプリに付与する RSC アクセス許可のみを含めます。

> [!NOTE]
> アプリが呼び出し元/メディア API にアクセスすることを目的としている場合、`webApplicationInfo.Id` は [Azure ボット サービス](/graph/cloud-communications-get-started#register-a-bot) の Azure AD アプリ IDである必要があります。

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Postman アプリを使用してチームに RSC アクセス許可を追加したテスト

RSC 権限が API リクエストペ イロードによって受け入れられているかどうかを確認するには、[チームの RSC JSON テスト コード](test-team-rsc-json-file.md)をローカル環境にコピーし、次の値を更新する必要があります。

* `azureADAppId`: アプリのAzure ADアプリ ID。
* `azureADAppSecret`: Azure AD アプリのパスワード。
* `token_scope`: トークンを取得するにはスコープが必要です。 値を に設定します `https://graph.microsoft.com/.default`。
* `teamGroupId`: 次のように、Teams クライアントからチーム グループ ID を取得できます。

    1. Teams クライアントで、左端のナビゲーション バーから **Teams** を選択します。
    2. ドロップダウン メニューから、アプリがインストールされているチームを選択します。
    3. **[その他のオプション]** アイコン (&#8943;) を選択します。
    4. **[チームへのリンクを取得する]** を選択します。
    5. 文字列から **groupId** 値をコピーして保存します。

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Postman アプリを使用してチャットに RSC アクセス許可を追加したテスト

API 要求ペイロードによって RSC アクセス許可が受け入れられているかどうかを確認するには、[[チャット用の RSC JSON テスト コード]](test-chat-rsc-json-file.md) をローカル環境にコピーし、次の値を更新する必要があります。

* `azureADAppId`: アプリのAzure ADアプリ ID。
* `azureADAppSecret`: Azure AD アプリのパスワード。
* `token_scope`: トークンを取得するにはスコープが必要です。 値を に設定します `https://graph.microsoft.com/.default`。
* `tenantId`: テナントの名前または Azure AD オブジェクト ID。
* `chatId`: 次のように、Teams *Web* クライアントからチャット スレッド ID を取得できます。

    1. Teams Web クライアントで、左端のナビゲーション バーから **[チャット]** を選択します。
    2. ドロップダウン メニューから、アプリがインストールされているチャットを選択します。
    3. Web URL をコピーし、文字列からチャット スレッド ID を保存します。
![Web URL からのチャット スレッド ID。](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>Postman の使用

1. [Postman](https://www.postman.com) アプリを開きます。
2. **[ファイル]** > **[インポート]** > **[ファイルのインポート]** の順に選択して、更新された JSON ファイルを環境からアップロードします。  
3. **[コレクション]** タブをクリックします。
4. **TestRSC** の横にあるシェブロン **>** を選択して、詳細ビューを展開し、API リクエストを確認します。

API 呼び出しごとにアクセス許可コレクション全体を実行します。 アプリ マニフェストで指定したアクセス許可は成功する必要がありますが、指定されていないアクセス許可は HTTP 403 状態コードで失敗する必要があります。 すべての応答状態コードを確認して、アプリ内の RSC アクセス許可の動作が期待を満たしていることを確認します。

> [!NOTE]
> 特定の DELETE および READ API 呼び出しをテストするには、これらのインスタンス シナリオを JSON ファイルに追加します。

## <a name="test-revoked-rsc-permissions-using-postman"></a>[Postman](https://www.postman.com/) を使用して失効した RSC アクセス許可をテストする

1. 特定のリソースからアプリをアンインストールします。
2. チャットまたはチームのいずれかの手順に従います。
    1. [Postman を使用してチームに RSC アクセス許可を追加しました](#test-added-rsc-permissions-to-a-team-using-the-postman-app)。
    2. [Postman を使用してチャットに RSC アクセス許可を追加しました](#test-added-rsc-permissions-to-a-chat-using-the-postman-app)。
3. **HTTP 403 状態コードで特定の API 呼び出しが失敗した** ことを確認するには、すべての応答状態コードを確認します。

## <a name="see-also"></a>関連項目

* [Microsoft Graph API と Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)
* [リソース固有の同意](~/graph-api/rsc/resource-specific-consent.md)
