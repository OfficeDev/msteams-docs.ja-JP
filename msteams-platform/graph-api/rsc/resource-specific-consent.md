---
title: リソース固有の同意 (Teams
description: リソース固有の同意について、Teams活用する方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: teams 承認 OAuth SSO AAD rsc Graph
ms.openlocfilehash: 39e5c1bb8375fb5b5a3bd3900cb6ad870a3ff677
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101794"
---
# <a name="resource-specific-consent-rsc"></a>リソース固有の同意 (RSC)

リソース固有の同意 (RSC) は、アプリが API エンドポイントを使用して組織内の特定のチームを管理できる Microsoft Teams API と Microsoft Graph API 統合です。 リソース固有の同意 (RSC) アクセス許可モデルを使用すると、チーム所有者は、アプリケーションがチームのデータにアクセスしたり変更したりするための同意を付与できます。 詳細で、Teams固有の RSC アクセス許可は、特定のチーム内でアプリケーションが実行できる操作を定義します。

## <a name="resource-specific-permissions"></a>リソース固有のアクセス許可

|アプリケーションのアクセス許可| Action |
| ----- | ----- |
|TeamSettings.Read.Group | このチームの設定を取得します。|
|TeamSettings.ReadWrite.Group|このチームの設定を更新します。|
|ChannelSettings.Read.Group|このチームのチャネル名、チャネルの説明、チャネル設定を取得します。|
|ChannelSettings.ReadWrite.Group|このチームのチャネル名、チャネルの説明、チャネル設定を更新します。|
|Channel.Create.Group|このチームのチャネルを作成します。|
|Channel.Delete.Group|このチームのチャネルを削除します。|
|ChannelMessage.Read.Group |このチームのチャネル メッセージを取得します。|
|TeamsAppInstallation.Read.Group|このチームのインストール済みアプリの一覧を取得します。|
|TeamsTab.Read.Group|このチームのタブの一覧を取得します。|
|TeamsTab.Create.Group|このチームのタブを作成します。|
|TeamsTab.ReadWrite.Group|このチームのタブを更新します。|
|TeamsTab.Delete.Group|このチームのタブを削除します。|
|TeamMember.Read.Group|このチームのメンバーを取得します。|

>[!NOTE]
>リソース固有のアクセス許可は、Teams クライアントにインストールTeamsアプリでのみ使用できます。現在は、Azure Active Directory ポータルの一部ではありません。

## <a name="enable-resource-specific-consent-in-your-application"></a>アプリケーションでリソース固有の同意を有効にする

アプリケーションで RSC を有効にする手順は次のとおりです。

1. [ポータルでグループ所有者の同意設定をAzure Active Directoryします](#configure-group-owner-consent-settings-in-the-azure-ad-portal)。
1. [Azure Microsoft ID プラットフォーム ポータルをADします](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
1. [Azure ADポータルでアプリケーションのアクセス許可を確認します](#review-your-application-permissions-in-the-azure-ad-portal)。
1. [Microsoft Identity プラットフォームからアクセス トークンを取得します](#obtain-an-access-token-from-the-microsoft-identity-platform)。
1. [アプリ マニフェストTeams更新します](#update-your-teams-app-manifest)。
1. [アプリをアプリに直接インストールTeams。](#sideload-your-app-in-teams)
1. [アプリで追加された RSC アクセス許可を確認します](#check-your-app-for-added-rsc-permissions)。

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Azure AD ポータルでグループ所有者の同意設定を構成する

Azure portal 内でグループ所有者 [の同意を直接](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) 有効または無効にできます。

> [!div class="checklist"]
>
>- グローバル管理者/ [会社管理者として Azure](https://portal.azure.com) portal [にサインインします](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)。  
 > - [[アプリケーション](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)  =>  **Azure Active Directory Enterpriseと** アクセス許可ユーザー  =>  **の同意設定**  =>  **] を選択します**。
> - データにアクセスするアプリに対するグループ所有者の同意というラベルが付いたコントロールを使用して、ユーザーの同意を有効、無効、または制限します **(既定** では、すべてのグループ所有者にグループ所有者の同意 **を許可します**)。 チームの所有者が RSC を使用してアプリをインストールするには、そのユーザーに対してグループ所有者の同意を有効にする必要があります。

![azure rsc 構成](../../assets/images/azure-rsc-configuration.png)

PowerShell を使用してグループ所有者の同意を有効または無効にするには、「PowerShell を使用してグループ所有者の同意を構成する」で説明 [されている手順に従います](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Azure Microsoft ID プラットフォーム ポータルを使用してアプリをADする

このAzure Active Directoryは、アプリを登録および構成する中心的なプラットフォームを提供します。 アプリを Azure ADポータルに登録して、アプリと統合し、Microsoft Microsoft ID プラットフォーム API Graphする必要があります。 *「*[アプリケーションをアプリケーションに登録する」を参照Microsoft ID プラットフォーム。](/graph/auth-register-app-v2)

>[!WARNING]
>複数のアプリを同Teams Azure アプリ ID に登録ADしない。アプリ ID は、アプリごとに一意である必要があります。 同じアプリ ID に複数のアプリをインストールしようとすると失敗します。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Azure AD ポータルでアプリケーションのアクセス許可を確認する

[ホーム アプリの **登録**  =>  **] ページに移動し**、RSC アプリを選択します。 左側 **のナビゲーション バーから API** アクセス許可を選択し、アプリに対して構成されているアクセス許可の一覧を確認します。 アプリが API 呼び出しでのみ RSC Graphする場合は、そのページのすべてのアクセス許可を削除します。 アプリで RSC 以外の呼び出しを行う場合は、必要に応じてこれらのアクセス許可を保持します。

>[!IMPORTANT]
>Azure ADポータルを使用して RSC アクセス許可を要求することはできません。 RSC アクセス許可は現在、Teams クライアントにインストールされているアプリケーションTeams専用であり、アプリ マニフェスト (JSON) ファイルで宣言されています。

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
> - **id**  — Azure ADアプリ *ID。「Azure* AD ポータルにアプリ [を登録する」を参照してください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
> - **resource**  — 任意の文字列。 このフィールドは RSC で操作を行う必要がありますが、エラー応答を回避するには、値を追加して値を指定する必要があります。任意の文字列が実行します。
> - **アプリケーションのアクセス許可** - アプリの RSC アクセス許可。 *「*[リソース固有のアクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。

>
>[!IMPORTANT]
> RSC 以外のアクセス許可は Azure portal に格納されます。 アプリ マニフェストに追加しません。
>

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

## <a name="sideload-your-app-in-teams"></a>アプリをサイドロードTeams

管理者がTeamsアプリのアップロードを許可している場合は、アプリを特定[](~/concepts/deploy-and-publish/apps-upload.md)のチームに直接サイドロードできます。

## <a name="check-your-app-for-added-rsc-permissions"></a>アプリで追加された RSC アクセス許可を確認する

>[!IMPORTANT]
>RSC アクセス許可は、ユーザーに属性付けされません。 呼び出しは、ユーザーが委任したアクセス許可ではなく、アプリのアクセス許可を使用して行います。 したがって、アプリは、チャネルの作成やタブの削除など、ユーザーが実行できない操作を実行できる場合があります。RSC API 呼び出しを行う前に、チーム所有者の使用例の意図を確認する必要があります。 *「API* [Microsoft Teams」を参照してください](/graph/teams-concept-overview)。

アプリをチームにインストールしたら、Graph[エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)を使用して、チーム内のアプリに付与されたアクセス許可を表示できます。

> [!div class="checklist"]
>
>- チームの **groupId** をクライアントから取得Teamsします。
> - クライアントで、Teams **ナビゲーション** バー Teamsを選択します。
> - ドロップダウン メニューからアプリがインストールされているチームを選択します。
> - [その他 **のオプション]** アイコンを選択します (&#8943;)。
> - [チーム **へのリンクを取得する] を選択します**。
> - 文字列から **groupId 値をコピー** して保存します。
> - エクスプローラーに **Graphします**。
> - 次の **エンドポイントに対** して GET 呼び出しを行います `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` 。 応答の clientAppId フィールドは、アプリ マニフェストで指定された appId にTeamsされます。
  ![Graphに対するエクスプローラーの応答を確認します。](../../assets/images/graph-permissions.png)

## <a name="code-sample"></a>コード サンプル
| **サンプル名** | **説明** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| リソース固有の同意 (RSC) | RSC を使用して API Graph呼び出します。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="test-resource-specific-consent"></a>リソース固有の同意をテストする
 
> [!div class="nextstepaction"]
> [**リソース固有の同意のアクセス許可をテストTeams**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>管理者向けTeamsトピック

> [!div class="nextstepaction"]
> [**管理者向けリソース固有Microsoft Teams同意**](/MicrosoftTeams/resource-specific-consent)
> 

