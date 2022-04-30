---
title: Teams でリソース固有の同意を有効にする
description: Teams におけるリソース固有の同意と、それを利用する方法について説明します。
ms.localizationpriority: high
author: akjo
ms.author: lajanuar
ms.topic: reference
keywords: teams authorization OAuth SSO Azure AD rsc Graph
ms.openlocfilehash: 8a90d1280f94de099543d879028a84d538c588ac
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111508"
---
# <a name="resource-specific-consent"></a>リソース固有の同意

> [!NOTE]
> チャット スコープのリソース固有の同意は、[パブリック開発者向けプレビュー](../../resources/dev-preview/developer-preview-intro.md)でのみ使用できます。

リソース固有の同意 (RSC) とは、アプリが API エンドポイントを使用して組織内の特定のリソース (チームまたはチャット) を管理できるようにする、Microsoft Teams と Microsoft Graph API の統合です。 RSC アクセス許可モデルを使用すると、*チーム所有者* と *チャット所有者* は、アプリケーションがチームのデータとチャットのデータにアクセスして変更することに同意できます。

**メモ：** チャットに会議または通話が関連付けられている場合は、関連する RSC アクセス許可もそれらのリソースに適用されます。

## <a name="resource-specific-permissions"></a>リソース固有の委任されたアクセス許可

きめ細かく、Teams 固有の RSC アクセス許可は、特定のリソース内でアプリケーションが実行できる操作を定義します。

### <a name="resource-specific-permissions-for-a-team"></a>チームのリソース固有のアクセス許可

|アプリケーションのアクセス許可| Action |
| ----- | ----- |
|TeamSettings.Read.Group | このチームの設定を取得します。|
|TeamSettings.ReadWrite.Group|このチームの設定を更新します。|
|ChannelSettings.Read.Group|このチームのチャネル名、チャネルの説明、チャネル設定を取得します。|
|ChannelSettings.ReadWrite.Group|ユーザーがサインインしていない状態で、このチームのチャネル名、チャネルの説明、チャネルの設定を更新します。|
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

詳細については、「[チーム リソース固有の同意アクセス許可](/graph/permissions-reference#teams-resource-specific-consent-permissions)」参照してください。

### <a name="resource-specific-permissions-for-a-chat"></a>チャットのリソース固有のアクセス許可

次の表に、チャットに対するリソース固有のアクセス許可を示します:

|アプリケーションのアクセス許可| Action |
| ----- | ----- |
| ChatSettings.Read.Chat         | このチャットの設定を取得します。                                    |
| ChatSettings.ReadWrite.Chat    | このチャットの設定を読み取ります。                          |
| ChatMessage.Read.Chat          | このチャットのメッセージを取得します。                                    |
| ChatMember.Read.Chat           | このチャットのメンバーを取得します。                                     |
| Chat.Manage.Chat               | このチャットを管理します。                                             |
| TeamsTab.Read.Chat             | このチャットのタブを取得します。                                        |
| TeamsTab.Create.Chat           | このチャットでタブを作成します。                                     |
| TeamsTab.Delete.Chat           | このチャットのタブを削除します。                                      |
| TeamsTab.ReadWrite.Chat        | このチャットのタブを管理します。                                      |
| TeamsAppInstallation.Read.Chat | このチャットにインストールされているアプリを読み取ります。                   |
| OnlineMeeting.ReadBasic.Chat   | このチャットに関連付けられている会議の名前、スケジュール、開催者、参加リンク、開始/終了通知などの基本的なプロパティを読み取ります。 |
| Calls.AccessMedia.Chat         | このチャットまたは会議に関連付けられた通話でメディア ストリームにアクセスします。                                    |
| Calls.JoinGroupCalls.Chat         | このチャットまたは会議に関連付けられた通話に参加します。                                    |
| TeamsActivity.Send.Chat         | このチャットのユーザーのアクティビティ フィードに新しい通知を作成します。 |

詳細については、「[チャット リソース固有の同意アクセス許可](/graph/permissions-reference#chat-resource-specific-consent-permissions)」ページを参照してください。

> [!NOTE]
> リソース固有のアクセス許可は、Teams クライアントにインストールされている Teams アプリでのみ使用でき、現在は Azure Active Directory (AAD) ポータルに含まれていません。

## <a name="enable-rsc-in-your-application"></a>アプリケーションで RSC を有効にする

1. [Azure AD ポータルで同意設定を構成します](#configure-consent-settings-in-the-azure-ad-portal)。
    1. [チーム内の RSC のグループ所有者の同意設定を構成します](#configure-group-owner-consent-settings-for-rsc-in-a-team)。
    1. [チャットで RSC のユーザー同意設定を構成します](#configure-user-consent-settings-for-rsc-in-a-chat)。
1. [Azure AD ポータルを使用して、アプリを Microsoft ID プラットフォームに登録します](#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。
1. [Azure AD ポータルでアプリケーションのアクセス許可を確認します](#review-your-application-permissions-in-the-azure-ad-portal)。
1. [ID プラットフォームからアクセス トークンを取得します](#obtain-an-access-token-from-the-microsoft-identity-platform)。
1. [アプリ マニフェストを更新する](#update-your-teams-app-manifest)。
1. [Teams にアプリを直接インストールします](#sideload-your-app-in-teams)。
1. [追加された RSC アクセス許可をアプリで確認します](#check-your-app-for-added-rsc-permissions)。
    1. [チームで追加された RSC アクセス許可がないかアプリを確認します](#check-your-app-for-added-rsc-permissions-in-a-team)。
    1. [チャットで RSC アクセス許可が追加されたかどうかをアプリで確認します](#check-your-app-for-added-rsc-permissions-in-a-chat)。

## <a name="configure-consent-settings-in-the-azure-ad-portal"></a>Azure AD ポータルで同意設定を構成する

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a>チーム内の RSC のグループ所有者の同意設定を構成する

[グループ所有者の同意](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal)は、Microsoft Azure ポータル内で直接有効または無効にすることができます。

1. [グローバル管理者または会社の管理者](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)として [Azure portal](https://portal.azure.com) にサインインします。
1. [**Azure Active Directory**]  >  [**エンタープライズ アプリケーション**]  >  [**同意とアクセス許可**]  > [ [**ユーザー同意設定**]](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) を選択します。
1. [**データにアクセスするアプリのグループ所有者の同意**] とラベル付けされたコントロールを使ってユーザーの同意を有効、無効、または制限します。 既定では、"**すべてのグループ所有者に対するグループ所有者の同意を許可**" に設定されています。 チーム所有者が RSC を使用してアプリをインストールするには、そのユーザーに対してグループ所有者の同意を有効にする必要があります。

    ![Azure RSC チームの構成](../../assets/images/azure-rsc-team-configuration.png)

さらに、PowerShell を使用してグループ所有者の同意を有効または無効にすることができます。｢[PowerShell を使用してグループ所有者の同意を構成する](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)」で説明されている手順に従います。

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a>チャットで RSC のユーザー同意設定を構成する

[ユーザーの同意](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal)は、Azure portal内で直接有効または無効にすることができます。

1. [グローバル管理者または会社の管理者](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)として [Azure portal](https://portal.azure.com) にサインインします。
1. [**Azure Active Directory**]  >  [**エンタープライズ アプリケーション**]  >  [**同意とアクセス許可**]  > [ [**ユーザー同意設定**]](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) を選択します。
1. [**アプリケーションに対するユーザー同意**] とラベル付けられたコントロールを使って、ユーザー同意を有効化、無効化、または制限します。 既定値は、[**アプリに対するユーザーの同意を許可する] です**。 チャット メンバーが RSC を使用してアプリをインストールするには、そのユーザーに対してユーザーの同意を有効にする必要があります。

    ![Azure RSC チャットの構成](../../assets/images/azure-rsc-chat-configuration.png)

さらに、PowerShell を使用してユーザーの同意を有効または無効にすることができます。「[PowerShell を 使用したユーザーの同意の構成](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)」に関するページで説明されている手順に従います。

## <a name="register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal"></a>Azure AD ポータルを使用してアプリを Microsoft ID プラットフォームに登録する

Azure AD ポータルには、アプリを登録および構成するための中央プラットフォームが用意されています。 ID プラットフォームと統合し、Microsoft Graph API を呼び出すには、アプリを Azure AD ポータルに登録する必要があります。 詳細については、「[ID プラットフォームにアプリケーションを登録する](/graph/auth-register-app-v2)」を参照してください。

> [!WARNING]
> Azure AD アプリ ID は、複数の Teams アプリ間で共有することはできません。 Teams アプリと Azure AD アプリの間には 1 対 1 のマッピングが必要です。 同じ Azure AD アプリ ID に関連付けられている複数の Teams アプリをインストールしようとすると、インストールまたはランタイム エラーが発生します。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Azure AD ポータルでアプリケーションのアクセス許可を確認する

1. [**ホーム**]  >  [**アプリの登録**] ページに移動し、RSC アプリを選択します。
1. 左側のウィンドウで [**API アクセス許可**] を選択し、アプリの [**構成済みアクセス許可** のリストに移動します。 アプリが RSC Graph API呼び出しのみを行う場合は、そのページのすべてのアクセス許可を削除します。 アプリで RSC 以外の呼び出しも行う場合は、必要に応じてそれらのアクセス許可を保持します。

> [!IMPORTANT]
> Azure AD ポータルを使用して RSC アクセス許可を要求することはできません。 RSC アクセス許可は、現在、Teams クライアントにインストールされているTeams アプリケーション専用であり、Teams アプリ マニフェスト (JSON) ファイルで宣言されています。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Microsoft ID プラットフォームからアクセス トークンを取得する

Graph API 呼び出しを行うには、ID プラットフォームからアプリのアクセス トークンを取得する必要があります。 アプリが Microsoft ID プラットフォームからトークンを取得する前に、Azure AD ポータルに登録する必要があります。 アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。

ID プラットフォームからアクセス トークンを取得するには、Azure AD 登録プロセスから次の値が必要です。

* アプリ登録ポータルによって割り当てられた **アプリケーション ID**。 アプリでシングル サインオン (SSO) がサポートされている場合は、アプリと SSO に同じアプリケーション ID を使用する必要があります。
* **クライアントシークレット/パスワード**、または **証明書** である公開キーまたは秘密キーのペア。 ネイティブ アプリの場合、これは必須ではありません。
* Azure AD からの応答を受信するための **リダイレクト URI**、または応答 URL。

詳細については、「[ユーザーに代わってアクセスを取得する](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)」および「[ユーザーなしでアクセス権を取得する](/graph/auth-v2-service)」を参照してください。

## <a name="update-your-teams-app-manifest"></a>アプリ マニフェストを更新する

RSC アクセス許可は、アプリ マニフェスト JSON ファイルで宣言されます。

> [!IMPORTANT]
> RSC 以外のアクセス許可は、Azure portal に格納されます。 アプリ マニフェストに追加しないでください。

### <a name="manifest-changes-for-resource-specific-consent"></a>リソース固有の同意に対するマニフェストの変更

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.12 の RSC アクセス許可</b></summary>

次の値を使用して、アプリ マニフェストに [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーを追加します。

|名前| 種類 | 説明|
|---|---|---|
|`id` |String |Azure ADアプリ ID。 詳細については、「[Azure AD ポータルでアプリを登録する](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)」を参照してください。|
|`resource`|String| このフィールドには RSC での操作はありませんが、エラー応答を回避するために値を追加し、値を指定する必要があります。任意の文字列が実行されます。|

アプリで必要なアクセス許可を指定します。

|名前| 種類 | 説明|
|---|---|---|
|`authorization`|オブジェクト|アプリを実行する必要があるアクセス許可の一覧。 詳細については、[マニフェストでのリンク認可のプレースホルダー] を参照してください。

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

<br>

</details>

<br>

<details>

<summary><b>アプリ マニフェスト バージョン 1.11 以前の RSC アクセス許可</b></summary>

次の値を使用して、アプリ マニフェストに [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーを追加します。

|名前| 種類 | 説明|
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

> [!NOTE]
> アプリがチーム スコープとチャット スコープの両方でのインストールをサポートすることを意図している場合は、チームとチャットの両方のアクセス許可を `applicationPermissions` の下の同じマニフェストで指定できます。

<br>

</details>

## <a name="sideload-your-app-in-teams"></a>Teams でアプリをサイドロード

Teams 管理者がカスタム アプリのアップロードを許可している場合は、特定のチームまたはチャットに直接[アプリをサイドロード](~/concepts/deploy-and-publish/apps-upload.md)できます。

## <a name="check-your-app-for-added-rsc-permissions"></a>追加された RSC アクセス許可をアプリで確認する

> [!IMPORTANT]
> RSC のアクセス許可は、ユーザーに帰属しません。 呼び出しは、ユーザーが委任したアクセス許可ではなく、アプリのアクセス許可を使用して行われます。 アプリでは、タブの削除など、ユーザーが実行できない操作を実行できます。RSC API 呼び出しを行う前に、チーム所有者またはチャット所有者の使用目的を確認する必要があります。 詳細については、「[Microsoft Teams API の概要](/graph/teams-concept-overview)」を参照してください。

アプリがリソースにインストールされたら、[Graph エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)を使用して、リソース内のアプリに付与されたアクセス許可を表示できます。

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>チームで追加された RSC アクセス許可をアプリで確認する

1. Teams からチームの **groupId** を取得します。
1. Teams で、左端のウィンドウから **Teams** を選択します。
1. アプリをインストールするチームを選択します。
1. そのチームの省略記号 &#x25CF;&#x25CF;&#x25CF; を選択します。
1. チームのドロップダウン メニューから [**チームへのリンクを取得する**] を選択します。
1. [**チームへのリンクを取得する**] ポップアップ ダイアログ ボックスから **groupId** 値をコピーして保存します。
1. **Microsoft Graph** エクスプローラーにサインインする。
1. このエンドポイントへの **GET** 呼び出しを行います: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`。 応答のフィールドの `clientAppId` は、Teams アプリ マニフェストで指定された `webApplicationInfo.id` にマップされます。

    ![チーム RSC アクセス許可の GET 呼び出しに対するGraph エクスプローラー応答](../../assets/images/team-graph-permissions.png)

特定のチームにインストールされているアプリの詳細を取得する方法の詳細については、「[指定したチームにインストールされているアプリの名前とその他の詳細を取得する](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)」を参照してください。

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>チャットで追加された RSC アクセス許可をアプリで確認する

1. Teams *Web* クライアントからチャット スレッド ID を取得します。
1. Teams Web クライアントで、左端のウィンドウで [**チャット**] を選択します。
1. ドロップダウン メニューから、アプリがインストールされているチャットを選択します。
1. Web URL をコピーし、文字列からチャット スレッド ID を保存します。

    ![Web URL からのチャット スレッド ID](../../assets/images/chat-thread-id.png)

1. **Microsoft Graph** エクスプローラーにサインインする。
1. 次のエンドポイントへの **GET** 呼び出しを行います: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`。 応答のフィールドの `clientAppId` は、Teams アプリ マニフェストで指定された `webApplicationInfo.id` にマップされます。

    ![チャット RSC アクセス許可の GET 呼び出しに対する Graph エクスプローラー応答](../../assets/images/chat-graph-permissions.png)

特定のチャットにインストールされているアプリの詳細を取得する方法の詳細については、「[指定したチャットにインストールされているアプリの名前とその他の詳細を取得する](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)」を参照してください。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| リソース固有の同意 (RSC) | RSC を使用して Graph API を呼び出します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a>関連項目

* [Teams でリソース固有の同意アクセス許可をテストする](test-resource-specific-consent.md)
* [管理者向けの Microsoft Teams でのリソース固有の同意](/MicrosoftTeams/resource-specific-consent)
