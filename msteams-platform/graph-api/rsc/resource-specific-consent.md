---
title: リソース固有の同意を有効Teams
description: リソース固有の同意について、Teams活用する方法について説明します。
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: reference
keywords: teams 承認 OAuth SSO Azure AD rsc Graph
ms.openlocfilehash: 613416c7363de8a9351e56f5cdb2a6a339b74392
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821690"
---
# <a name="resource-specific-consent"></a>リソース固有の同意

> [!NOTE]
> チャット スコープに対するリソース固有の同意は、パブリック開発者 [プレビューでのみ利用](../../resources/dev-preview/developer-preview-intro.md) できます。

リソース固有の同意 (RSC) は、Microsoft Teams と Microsoft Graph API の統合であり、アプリは API エンドポイントを使用して、組織内のチームまたはチャットのいずれかの特定のリソースを管理できます。 RSC アクセス許可モデルを使用すると、チームの所有者とチャットの所有者は、アプリケーションがチームのデータとチャットのデータにそれぞれアクセスおよび変更するための同意を付与できます。 

**注:** チャットに会議または通話が関連付けられている場合は、関連する RSC アクセス許可がそれらのリソースにも適用されます。

## <a name="resource-specific-permissions"></a>リソース固有のアクセス許可

詳細で、Teams固有の RSC アクセス許可は、アプリケーションが特定のリソース内で実行できる操作を定義します。

### <a name="resource-specific-permissions-for-a-team"></a>チームのリソース固有のアクセス許可

|アプリケーションのアクセス許可| アクション |
| ----- | ----- |
|TeamSettings.Read.Group | このチームの設定を取得します。|
|TeamSettings.ReadWrite.Group|このチームの設定を更新します。|
|ChannelSettings.Read.Group|このチームのチャネル名、チャネルの説明、チャネル設定を取得します。|
|ChannelSettings.ReadWrite.Group|このチームのチャネル名、チャネルの説明、チャネル設定を更新します。|
|Channel.Create.Group|このチームのチャネルを作成します。 |
|Channel.Delete.Group|このチームのチャネルを削除します。 |
|ChannelMessage.Read.Group |このチームのチャネル メッセージを取得します。 |
|TeamsAppInstallation.Read.Group|このチームのインストール済みアプリの一覧を取得します。|
|TeamsTab.Read.Group|このチームのタブの一覧を取得します。|
|TeamsTab.Create.Group|このチームのタブを作成します。 |
|TeamsTab.ReadWrite.Group|このチームのタブを更新します。 |
|TeamsTab.Delete.Group|このチームのタブを削除します。 |
|TeamMember.Read.Group|このチームのメンバーを取得します。 |
|TeamsActivity.Send.Group|このチームのユーザーのアクティビティ フィードに新しい通知を作成します。 |

詳細については、「チーム リソース固有 [の同意のアクセス許可」を参照してください](/graph/permissions-reference#teams-resource-specific-consent-permissions)。

### <a name="resource-specific-permissions-for-a-chat"></a>チャットのリソース固有のアクセス許可

次の表に、チャットのリソース固有のアクセス許可を示します。

|アプリケーションのアクセス許可| アクション |
| ----- | ----- |
| ChatSettings.Read.Chat         | このチャットの設定を取得します。                                    |
| ChatSettings.ReadWrite.Chat    | このチャットの設定を更新します。                          |
| ChatMessage.Read.Chat          | このチャットのメッセージを取得します。                                    |
| ChatMember.Read.Chat           | このチャットのメンバーを取得します。                                     |
| Chat.Manage.Chat               | このチャットを管理します。                                             |
| TeamsTab.Read.Chat             | このチャットのタブを取得します。                                        |
| TeamsTab.Create.Chat           | このチャットでタブを作成します。                                     |
| TeamsTab.Delete.Chat           | このチャットのタブを削除します。                                      |
| TeamsTab.ReadWrite.Chat        | このチャットのタブを管理します。                                      |
| TeamsAppInstallation.Read.Chat | このチャットにインストールされているアプリを取得します。                   |
| OnlineMeeting.ReadBasic.Chat   | このチャットに関連付けられた会議の名前、スケジュール、開催者、参加リンク、開始/終了通知などの基本的なプロパティを読み取る。 |
| Calls.AccessMedia.Chat         | このチャットまたは会議に関連付けられた通話でメディア ストリームにアクセスします。                                    |
| Calls.JoinGroupCalls.Chat         | このチャットまたは会議に関連付けられた通話に参加します。                                    |
| TeamsActivity.Send.Chat         | このチャットのユーザーのアクティビティ フィードに新しい通知を作成します。 |

詳細については、「チャット リソース [固有の同意のアクセス許可」を参照してください](/graph/permissions-reference#chat-resource-specific-consent-permissions)。

> [!NOTE]
> リソース固有のアクセス許可は、Teams クライアントにインストールされている Teams アプリでのみ使用できます。現在は Azure Active Directory (AAD) ポータルの一部ではありません。

## <a name="enable-rsc-in-your-application"></a>アプリケーションで RSC を有効にする

1. [ポータルで同意の設定をAzure ADします](#configure-consent-settings-in-the-azure-ad-portal)。
    1. [チーム内の RSC のグループ所有者の同意設定を構成します](#configure-group-owner-consent-settings-for-rsc-in-a-team)。
    1. [チャットで RSC のユーザー同意設定を構成します](#configure-user-consent-settings-for-rsc-in-a-chat)。
1. [ポータルを使用してアプリMicrosoft ID プラットフォームをAzure ADします](#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。
1. [ポータルでアプリケーションのアクセス許可Azure ADします](#review-your-application-permissions-in-the-azure-ad-portal)。
1. [ID プラットフォームからアクセス トークンを取得します](#obtain-an-access-token-from-the-microsoft-identity-platform)。
1. [アプリ マニフェストTeams更新します](#update-your-teams-app-manifest)。
1. [アプリをアプリに直接インストールTeams](#sideload-your-app-in-teams)。
1. [アプリで追加された RSC アクセス許可を確認します](#check-your-app-for-added-rsc-permissions)。
    1. [チームに追加された RSC アクセス許可をアプリで確認します](#check-your-app-for-added-rsc-permissions-in-a-team)。
    1. [チャットで追加された RSC アクセス許可をアプリで確認します](#check-your-app-for-added-rsc-permissions-in-a-chat)。

## <a name="configure-consent-settings-in-the-azure-ad-portal"></a>ポータルで同意の設定をAzure ADする

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a>チームで RSC のグループ所有者の同意設定を構成する

グループ所有者の同意は、[次の](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal)ポータルで直接有効またはMicrosoft Azureできます。

1. グローバル管理者または [会社](https://portal.azure.com) の管理者として Azure [portal にサインインします](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。
1. [**アプリケーションAzure Active Directory** >  **Enterprise Consent** >  **と permissionsUser** >  [**の同意設定] を選択します**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)。
1. データにアクセスするアプリに対するグループ所有者の同意というラベルの付いたコントロールを使用して、ユーザーの同意 **を有効、無効、または制限します**。 既定値は、[ **すべてのグループ所有者に対するグループ所有者の同意を許可する] です**。 チームの所有者が RSC を使用してアプリをインストールするには、そのユーザーに対してグループ所有者の同意を有効にする必要があります。

    ![Azure RSC チーム構成](../../assets/images/azure-rsc-team-configuration.png)

さらに、PowerShell を使用してグループ所有者の同意を有効または無効にできます。PowerShell を使用してグループ所有者の同意を構成するで説明されている手順 [に従います](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a>チャットで RSC のユーザー同意設定を構成する

Azure portal 内でユーザーの [同意を直接](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) 有効または無効にできます。

1. グローバル管理者または [会社](https://portal.azure.com) の管理者として Azure [portal にサインインします](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。
1. [**アプリケーションAzure Active Directory** >  **Enterprise Consent** >  **と permissionsUser** >  [**の同意設定] を選択します**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)。
1. [アプリケーションに対するユーザーの同意] というラベルの付いたコントロールを使用して、ユーザーの同意を有効 **、無効、または制限します**。 既定値は [ **アプリに対するユーザーの同意を許可する] です**。 チャット メンバーが RSC を使用してアプリをインストールするには、そのユーザーに対してユーザーの同意を有効にする必要があります。

    ![Azure RSC チャット構成](../../assets/images/azure-rsc-chat-configuration.png)

さらに、PowerShell を使用してユーザーの同意を有効または無効にしたり、PowerShell を使用してユーザーの同意を構成するで説明されている [手順に従います](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)。

## <a name="register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal"></a>ポータルを使用してアプリMicrosoft ID プラットフォームをAzure ADする

このAzure ADは、アプリを登録および構成する中心的なプラットフォームを提供します。 ID プラットフォームと統合し、Microsoft Azure AD API を呼び出すには、アプリを Graphする必要があります。 詳細については、「アプリケーションを [ID プラットフォームに登録する」を参照してください](/graph/auth-register-app-v2)。

> [!WARNING]
> 複数Azure ADアプリ間でアプリ ID を共有Teams必要があります。 1 つのアプリとアプリの間に 1:1 TeamsがAzure ADがあります。 同じアプリ ID にTeams複数のアプリをインストールしようとすると、Azure AD実行時にエラーが発生します。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>ポータルでアプリケーションのアクセス許可をAzure ADする

1. [HomeApp 登録 **] ページ** > **に移動し** 、RSC アプリを選択します。
1. 左側 **のウィンドウから [API の** アクセス許可] を選択し、アプリの [構成済み **アクセス許可]** の一覧を表示します。 アプリで RSC 呼び出しGraph場合は、そのページのすべてのアクセス許可を削除します。 アプリで RSC 以外の呼び出しを行う場合は、必要に応じてこれらのアクセス許可を保持します。

> [!IMPORTANT]
> このAzure ADを使用して RSC アクセス許可を要求することはできません。 RSC アクセス許可は現在、Teams クライアントにインストールされている Teams アプリケーション専用であり、Teams アプリ マニフェスト (JSON) ファイルで宣言されています。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>サーバーからアクセス トークンを取得Microsoft ID プラットフォーム

API 呼びGraphするには、ID プラットフォームからアプリのアクセス トークンを取得する必要があります。 アプリが ID プラットフォームからトークンを取得するには、そのトークンをポータルに登録Azure ADがあります。 アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。

ID プラットフォームからアクセス トークンを取得するには、Azure AD登録プロセスから次の値が必要です。

- アプリ **登録ポータルによって** 割り当てられたアプリケーション ID。 アプリがシングル サインオン (SSO) をサポートしている場合は、アプリと SSO に同じアプリケーション ID を使用する必要があります。
- クライアント **シークレット/パスワード、** または証明書である公開キーまたは秘密 **キーのペア**。 ネイティブ アプリの場合、これは必須ではありません。
- アプリ **のリダイレクト URI** または返信 URL で、アプリから応答を受信Azure AD。

詳細については、「ユーザーに [代わってアクセス権を取得](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) する」および「ユーザーなしで [アクセスを取得する」を参照してください](/graph/auth-v2-service)。

## <a name="update-your-teams-app-manifest"></a>アプリ マニフェストTeams更新する

RSC アクセス許可は、アプリ マニフェスト JSON ファイルで宣言されます。 

> [!IMPORTANT]
> RSC 以外のアクセス許可は Azure portal に格納されます。 アプリ マニフェストに追加しません。

### <a name="manifest-changes-for-resource-specific-consent"></a>リソース固有の同意のためのマニフェストの変更

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.12 の RSC アクセス許可</b></summary>

次の [値を使用して、WebApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加します。

|名前| 型 | 説明|
|---|---|---|
|`id` |String |ユーザー Azure ADアプリ ID。 詳細については、「アプリを[ポータルに登録する」をAzure ADしてください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。|
|`resource`|String| このフィールドは RSC で操作を行う必要がありますが、エラー応答を回避するには、値を追加して値を指定する必要があります。任意の文字列が実行します。|

アプリに必要なアクセス許可を指定します。

|名前| 型 | 説明|
|---|---|---|
|`authorization`|オブジェクト|アプリを実行する必要があるアクセス許可の一覧。 詳細については、「[マニフェストでのリンク承認のプレースホルダー] 」を参照してください。

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
    
<br>

</details>

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.11 以前の RSC アクセス許可</b></summary>

次の [値を使用して、WebApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加します。

|名前| 型 | 説明|
|---|---|---|
|`id` |String |ユーザー Azure ADアプリ ID。 詳細については、「アプリを[ポータルに登録する」をAzure ADしてください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。|
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

> [!NOTE]
> アプリがチームスコープとチャット スコープの両方でのインストールをサポートすることを意図している場合は、チームとチャットの両方のアクセス許可を同じマニフェストで指定できます `applicationPermissions`。
    
<br>

</details>

## <a name="sideload-your-app-in-teams"></a>Teams でアプリをサイドロード

管理者がTeamsアプリのアップロードを許可している場合は、アプリを特定[](~/concepts/deploy-and-publish/apps-upload.md)のチームまたはチャットに直接サイドロードできます。

## <a name="check-your-app-for-added-rsc-permissions"></a>アプリで追加された RSC アクセス許可を確認する

> [!IMPORTANT]
> RSC アクセス許可は、ユーザーに属性付けされません。 呼び出しは、ユーザーが委任したアクセス許可ではなく、アプリのアクセス許可を使用して行います。 アプリは、タブの削除など、ユーザーが実行できない操作を実行できます。RSC API 呼び出しを行う前に、チーム所有者またはチャット所有者の使用意図を確認する必要があります。 詳細については、「API の概要Microsoft Teams[参照してください](/graph/teams-concept-overview)。

アプリがリソースにインストールされた後、Graph [エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)を使用して、リソース内のアプリに付与されたアクセス許可を表示できます。

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>チームに追加された RSC アクセス許可をアプリで確認する

1. チームの **groupId を次** のTeams。
1. [Teams] で、左端 **Teams** ウィンドウから [プロパティ] を選択します。
1. アプリをインストールするチームを選択します。
1. そのチームの省略 &#x25CF;&#x25CF;&#x25CF; を選択します。
1. [チーム **] ドロップダウン メニューから [チームへの** リンクを取得する] を選択します。
1. [チームへのリンク **を取得する** ] ポップアップ ダイアログ ボックスから groupId **値をコピー** して保存します。
1. エクスプローラーにサインイン **Graphします**。
1. このエンドポイント **に GET** 呼び出しを行います。 `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` 応答`clientAppId`のフィールドは、アプリ マニフェストで`webApplicationInfo.id`指定されたTeamsマップされます。

    ![Graph RSC アクセス許可の GET 呼び出しに対するエクスプローラーの応答](../../assets/images/team-graph-permissions.png)

特定のチームにインストールされているアプリの詳細を取得する方法の詳細については、「指定したチームにインストールされているアプリの名前と他の詳細を取得する」 [を参照してください](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)。

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>チャットで追加された RSC アクセス許可をアプリで確認する

1. Web クライアントからチャット スレッド ID を *Teamsします。*
1. Web クライアントTeams、左端 **のウィンドウから** [チャット] を選択します。
1. アプリがインストールされているチャットをドロップダウン メニューから選択します。
1. Web URL をコピーし、文字列からチャット スレッド ID を保存します。

    ![Web URL からのチャット スレッド ID](../../assets/images/chat-thread-id.png)

1. エクスプローラーにサインイン **Graphします**。
1. 次の **エンドポイントに対して GET** 呼び出しを行います。 `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` 応答`clientAppId`のフィールドは、アプリ マニフェストで`webApplicationInfo.id`指定されたTeamsマップされます。

    ![Graph RSC アクセス許可の GET 呼び出しに対するエクスプローラーの応答](../../assets/images/chat-graph-permissions.png)

特定のチャットにインストールされているアプリの詳細を取得する方法の詳細については、「指定したチャットにインストールされているアプリの名前と他の詳細を取得する」 [を参照してください](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Resource-Specific同意 (RSC) | RSC を使用して API Graph呼び出します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a>関連項目
 
* [リソース固有の同意のアクセス許可をテストTeams](test-resource-specific-consent.md)
* [管理者向けリソース固有Microsoft Teams同意](/MicrosoftTeams/resource-specific-consent)
