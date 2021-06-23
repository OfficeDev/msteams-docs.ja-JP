---
title: リソース固有の同意 (Teams
description: リソース固有の同意について、Teams活用する方法について説明します。
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: reference
keywords: teams 承認 OAuth SSO AAD rsc Graph
ms.openlocfilehash: f364371f7763235e64da71b91db9b16b41ddf389
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068551"
---
# <a name="resource-specific-consent-rsc"></a>リソース固有の同意 (RSC)

> [!NOTE]
> チャット スコープに対するリソース固有の同意は、パブリック開発者 [プレビューでのみ利用](../../resources/dev-preview/developer-preview-intro.md) できます。

リソース固有の同意 (RSC) は、Microsoft Teams API と Microsoft Graph API の統合であり、アプリは API エンドポイントを使用して、組織内の特定のリソース (チームまたはチャット) を管理できます。 リソース固有の同意 (RSC) アクセス許可モデルを使用すると、チームの所有者とチャット所有者は、アプリケーションがチームのデータとチャットのデータにそれぞれアクセスしたり、変更したりするための同意を付与できます。 詳細な RSC アクセス許可は、アプリケーションが特定のリソース内で実行できる操作を定義します。

## <a name="resource-specific-permissions"></a>リソース固有のアクセス許可

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

詳細については、「チーム リソース固有の [同意のアクセス許可」を参照してください](/graph/permissions-reference#team-resource-specific-consent-permissions)。

### <a name="resource-specific-permissions-for-a-chat"></a>チャットのリソース固有のアクセス許可
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
| OnlineMeeting.ReadBasic.Chat   | このチャットに関連付けられた会議の基本的なプロパティ (名前、スケジュール、開催者、参加リンクなど) を取得します。 |

詳細については、「Chat リソース固有の [同意のアクセス許可」を参照してください](/graph/permissions-reference#chat-resource-specific-consent-permissions)。

>[!NOTE]
>リソース固有のアクセス許可は、Teams クライアントにインストールTeamsアプリでのみ使用できます。現在は、Azure Active Directory ポータルの一部ではありません。

## <a name="enable-resource-specific-consent-in-your-application"></a>アプリケーションでリソース固有の同意を有効にする

アプリケーションで RSC を有効にする手順は次のとおりです。

1. [ポータルで同意の設定をAzure Active Directoryします](#configure-consent-settings-in-the-azure-ad-portal)。
    1. [チーム内の RSC のグループ所有者の同意設定を構成します](#configure-group-owner-consent-settings-for-rsc-in-a-team)。
    1. [チャットで RSC のユーザー同意設定を構成します](#configure-user-consent-settings-for-rsc-in-a-chat)。
1. [Azure Microsoft ID プラットフォーム ポータルをADします](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
1. [Azure ADポータルでアプリケーションのアクセス許可を確認します](#review-your-application-permissions-in-the-azure-ad-portal)。
1. [Microsoft Identity プラットフォームからアクセス トークンを取得します](#obtain-an-access-token-from-the-microsoft-identity-platform)。
1. [アプリ マニフェストTeams更新します](#update-your-teams-app-manifest)。
1. [アプリをアプリに直接インストールTeams。](#sideload-your-app-in-teams)
1. [アプリで追加された RSC アクセス許可を確認します](#check-your-app-for-added-rsc-permissions)。
    1. [チームに追加された RSC アクセス許可をアプリで確認します](#check-your-app-for-added-rsc-permissions-in-a-team)。
    1. [チャットで追加された RSC アクセス許可をアプリで確認します](#check-your-app-for-added-rsc-permissions-in-a-chat)。

## <a name="configure-consent-settings-in-the-azure-ad-portal"></a>Azure AD ポータルで同意の設定を構成する

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a>チームで RSC のグループ所有者の同意設定を構成する

Azure portal 内でグループ所有者 [の同意を直接](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) 有効または無効にできます。

> [!div class="checklist"]
>
>- グローバル管理者/ [会社管理者として Azure](https://portal.azure.com) portal [にサインインします](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。  
 > - [[アプリケーション](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)  =>  **Azure Active Directory Enterpriseと** アクセス許可ユーザー  =>  **の同意設定**  =>  **] を選択します**。
> - データにアクセスするアプリに対するグループ所有者の同意というラベルが付いたコントロールを使用して、ユーザーの同意を有効、無効、または制限します **(既定** では、すべてのグループ所有者にグループ所有者の同意 **を許可します**)。 チームの所有者が RSC を使用してアプリをインストールするには、そのユーザーに対してグループ所有者の同意を有効にする必要があります。

![azure rsc チーム構成](../../assets/images/azure-rsc-team-configuration.png)

PowerShell を使用してグループ所有者の同意を有効または無効にするには、「PowerShell を使用してグループ所有者の同意を構成する」で説明 [されている手順に従います](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a>チャットで RSC のユーザー同意設定を構成する

Azure portal 内でユーザーの [同意を直接](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) 有効または無効にできます。

> [!div class="checklist"]
>
>- グローバル管理者/ [会社管理者として Azure](https://portal.azure.com) portal [にサインインします](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。  
 > - [[アプリケーション](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)  =>  **Azure Active Directory Enterpriseと** アクセス許可ユーザー  =>  **の同意設定**  =>  **] を選択します**。
> - [アプリケーションに対するユーザーの同意] というラベルの付いたコントロールを使用して、ユーザーの同意を有効、無効、または制限します **(既定値** は [アプリの **ユーザーの同意を** 許可する] です)。 チャット メンバーが RSC を使用してアプリをインストールするには、そのユーザーに対してユーザーの同意を有効にする必要があります。

![azure rsc チャット構成](../../assets/images/azure-rsc-chat-configuration.png)

PowerShell を使用してユーザーの同意を有効または無効にするには、「PowerShell を使用してユーザーの同意を構成する」で説明 [されている手順に従います](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)。


## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Azure Microsoft ID プラットフォーム ポータルを使用してアプリをADする

このAzure Active Directoryは、アプリを登録および構成する中心的なプラットフォームを提供します。 アプリを Azure ADポータルに登録して、アプリと統合し、Microsoft Microsoft ID プラットフォーム API Graphする必要があります。 詳細については、「アプリケーションを[アプリケーションに登録する」を参照Microsoft ID プラットフォーム。](/graph/auth-register-app-v2)

>[!WARNING]
>Azure アプリ ID AD複数のアプリ間で共有Teamsする必要があります。 1 つのアプリと Azure アプリの間に 1:1 TeamsマッピングがADがあります。 同じ Azure TEAMSに関連付けられている複数のアプリをインストールしようとすると、AD/ランタイムエラーが発生します。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Azure AD ポータルでアプリケーションのアクセス許可を確認する

[ホーム アプリの **登録**  =>  **] ページに移動し**、RSC アプリを選択します。 左側 **のナビゲーション バーから API** アクセス許可を選択し、アプリに対して構成されているアクセス許可の一覧を確認します。 アプリが API 呼び出しでのみ RSC Graphする場合は、そのページのすべてのアクセス許可を削除します。 アプリで RSC 以外の呼び出しを行う場合は、必要に応じてこれらのアクセス許可を保持します。

>[!IMPORTANT]
>Azure ADポータルを使用して RSC アクセス許可を要求することはできません。 RSC アクセス許可は現在、Teams クライアントにインストールされている Teams アプリケーション専用であり、Teams アプリ マニフェスト (JSON) ファイルで宣言されています。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>サーバーからアクセス トークンを取得Microsoft ID プラットフォーム

API 呼びGraphするには、ID プラットフォームからアプリのアクセス トークンを取得する必要があります。 アプリがアプリからトークンを取得するには、Microsoft ID プラットフォーム Azure ポータルに登録するADがあります。 アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。

ID プラットフォームからアクセス トークンを取得するには、Azure AD登録プロセスから次の値を取得する必要があります。

- アプリ **登録ポータルによって** 割り当てられたアプリケーション ID。 アプリがシングル サインオン (SSO) をサポートしている場合は、アプリと SSO に同じアプリケーション ID を使用する必要があります。
- クライアント  **シークレット/パスワード、** または公開/秘密キーのペア (**証明書**)。 ネイティブ アプリの場合、これは必須ではありません。
- Azure **サーバーから応答** を受信するアプリのリダイレクト URI (または返信 URL) AD。

 *「*[ユーザーに代わってアクセスを取得する」および](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)「[ユーザーなしでアクセスを取得する」を参照してください。](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>アプリ マニフェストTeams更新する

RSC アクセス許可は、アプリ マニフェスト (JSON) ファイルで宣言されます。  次の [値を使用して、WebApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加します。

> [!div class="checklist"]
>
> - **id**  — Azure ADアプリ ID。 詳細については、「Azure AD ポータルにアプリを [登録する」を参照してください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
> - **resource**  — 任意の文字列。 このフィールドは RSC で操作を行う必要がありますが、エラー応答を回避するには、値を追加して値を指定する必要があります。任意の文字列が実行します。
> - **アプリケーションのアクセス許可** - アプリの RSC アクセス許可。 詳細については、「リソース固有 [のアクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。

>
>[!IMPORTANT]
> RSC 以外のアクセス許可は Azure portal に格納されます。 アプリ マニフェストに追加しません。
>

### <a name="example-for-rsc-in-a-team"></a>チームの RSC の例
```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.ReadWrite.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.ReadWrite.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

### <a name="example-for-rsc-in-a-chat"></a>チャット内の RSC の例
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
      "OnlineMeeting.ReadBasic.Chat"
    ]
  }
```

>[!NOTE]
>アプリがチームスコープとチャット スコープの両方でのインストールをサポートすることを意図している場合は、チームとチャットの両方のアクセス許可を同じマニフェストで指定できます `applicationPermissions` 。

## <a name="sideload-your-app-in-teams"></a>アプリをサイドロードTeams

管理者がTeamsアプリのアップロードを許可している場合は、アプリを特定[](~/concepts/deploy-and-publish/apps-upload.md)のチームまたはチャットに直接サイドロードできます。

## <a name="check-your-app-for-added-rsc-permissions"></a>アプリで追加された RSC アクセス許可を確認する

>[!IMPORTANT]
>RSC アクセス許可は、ユーザーに属性付けされません。 呼び出しは、ユーザーが委任したアクセス許可ではなく、アプリのアクセス許可を使用して行います。 したがって、アプリは、タブの削除など、ユーザーが実行できない操作を実行できる場合があります。RSC API 呼び出しを行う前に、チーム所有者またはチャット所有者の使用例の意図を確認する必要があります。 詳細については、「API の概要[Microsoft Teamsを参照してください](/graph/teams-concept-overview)。

アプリがリソースにインストールされた後、Graph[エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)を使用して、リソース内のアプリに付与されたアクセス許可を表示できます。

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>チームに追加された RSC アクセス許可をアプリで確認する

> [!div class="checklist"]
>
>- チームの **groupId** をクライアントから取得Teamsします。
> - クライアントで、Teams **ナビゲーション** バー Teamsを選択します。
> - ドロップダウン メニューからアプリがインストールされているチームを選択します。
> - [その他 **のオプション]** アイコンを選択します (&#8943;)。
> - [チーム **へのリンクを取得する] を選択します**。
> - 文字列から **groupId 値をコピー** して保存します。
> - エクスプローラーに **Graphします**。
> - 次の **エンドポイントに対** して GET 呼び出しを行います `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` 。 応答 `clientAppId` のフィールドは、アプリ マニフェスト `webApplicationInfo.id` で指定されたTeamsマップされます。
  ![Graph RSC アクセス許可の GET 呼び出しに対するエクスプローラーの応答を確認します。](../../assets/images/team-graph-permissions.png)

特定のチームにインストールされているアプリの詳細を取得する方法については、「指定したチームにインストールされているアプリの名前と他の詳細を取得する」 [を参照してください](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)。

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>チャットで追加された RSC アクセス許可をアプリで確認する

> [!div class="checklist"]
>
>- Web クライアントからチャット スレッド ID を *Teamsします。*
> - Web クライアントTeams、左側 **のナビゲーション** バーから [チャット] を選択します。
> - アプリがインストールされているチャットをドロップダウン メニューから選択します。
> - Web URL をコピーし、文字列からチャット スレッド ID を保存します。
![Web URL からのチャット スレッド ID。](../../assets/images/chat-thread-id.png)
> - エクスプローラーに **Graphします**。
> - 次の **エンドポイントに対** して GET 呼び出しを行います `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` 。 応答 `clientAppId` のフィールドは、アプリ マニフェスト `webApplicationInfo.id` で指定されたTeamsマップされます。
  ![Graph RSC アクセス許可の GET 呼び出しに対するエクスプローラーの応答を確認します。](../../assets/images/chat-graph-permissions.png)

特定のチャットにインストールされているアプリの詳細を取得する方法については、「指定したチャットにインストールされているアプリの名前と他の詳細を取得する」 [を参照してください](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)。

## <a name="code-sample"></a>コード サンプル
| **サンプル名** | **説明** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| リソース固有の同意 (RSC) | RSC を使用して API Graph呼び出します。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="see-also"></a>関連項目
 
* [リソース固有の同意のアクセス許可をテストTeams](test-resource-specific-consent.md)
* [管理者向けリソース固有Microsoft Teams同意](/MicrosoftTeams/resource-specific-consent)


