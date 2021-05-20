---
title: Teamsにおけるリソース固有の同意
description: Teamsでのリソース固有の同意と、その利点を活かす方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: チーム承認 OAuth SSO AAD rsc Graph
ms.openlocfilehash: dabe0c33013fbb398eee7bf00ac2881cd86e6bc5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566133"
---
# <a name="resource-specific-consent-rsc"></a>リソース固有の同意 (RSC)

リソース固有の同意 (RSC) は、アプリが API エンドポイントを使用して組織内の特定のチームを管理できるようにするMicrosoft Teamsと Microsoft Graph API 統合です。 リソース固有の同意 (RSC) のアクセス許可モデルを使用すると、 *チームの所有者* は、チームのデータにアクセスしたり、チームのデータを変更したりするための同意を付与できます。 詳細なTeams固有の RSC アクセス許可は、アプリケーションが特定のチーム内で実行できる操作を定義します。

## <a name="resource-specific-permissions"></a>リソース固有のアクセス許可

|アプリケーションのアクセス許可| Action |
| ----- | ----- |
|TeamSettings.Read.Group | このチームの設定を取得します。|
|TeamSettings.ReadWrite.Group|このチームの設定を更新します。|
|ChannelSettings.Read.Group|このチームのチャネル名、チャネルの説明、およびチャネル設定を取得します。|
|ChannelSettings.ReadWrite.Group|このチームのチャネル名、チャネルの説明、およびチャネル設定を更新します。|
|Channel.Create.Group|このチームのチャネルを作成します。|
|Channel.Delete.Group|このチームのチャンネルを削除します。|
|ChannelMessage.Read.Group |このチームのチャンネルメッセージを取得します。|
|TeamsAppInstallation.Read.Group|このチームがインストールしたアプリの一覧を取得します。|
|TeamsTab.Read.Group|このチームのタブのリストを取得します。|
|TeamsTab.Create.Group|このチームのタブを作成します。|
|TeamsTab.ReadWrite.Group|このチームのタブを更新します。|
|TeamsTab.Delete.Group|このチームのタブを削除します。|
|TeamMember.Read.Group|このチームのメンバーを取得します。|

>[!NOTE]
>リソース固有のアクセス許可は、Teams クライアントにインストールされているTeamsアプリでのみ使用でき、現在はAzure Active Directory ポータルには含まれていません。

## <a name="enable-resource-specific-consent-in-your-application"></a>アプリケーションでリソース固有の同意を有効にする

アプリケーションで RSC を有効にする手順は次のとおりです。

1. [Azure Active Directory ポータル でグループ所有者の同意設定を構成](#configure-group-owner-consent-settings-in-the-azure-ad-portal)する 。
1. [Azure AD ポータル を介して Microsoft ID プラットフォーム にアプリを登録](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)します。
1. [Azure AD ポータル でアプリケーションのアクセス許可を確認](#review-your-application-permissions-in-the-azure-ad-portal)します。
1. [Microsoft ID プラットフォームからアクセス トークンを取得](#obtain-an-access-token-from-the-microsoft-identity-platform)する 。
1. [Teams アプリ マニフェストを更新](#update-your-teams-app-manifest)する 。
1. [アプリを Teams に直接インストールします](#sideload-your-app-in-teams)。
1. [追加された RSC 権限のアプリを確認](#check-your-app-for-added-rsc-permissions)します。

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Azure AD ポータルでグループ所有者の同意の設定を構成する

[グループ所有者の同意](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal)を Azure ポータル内で直接有効または無効にすることができます。

> [!div class="checklist"]
>
>- [グローバル管理者または会社管理者](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)として[Azure ポータル](https://portal.azure.com)にサインインします。  
 > - [[](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)**アプリケーション Azure Active Directory Enterprise同意**  =>    =>  **とアクセス許可**  =>  **] [ユーザーの同意の設定]** を選択します。
> - [グループ所有者の同意] というラベルの付いたコントロールで、 **データにアクセスするアプリのユーザーの同意を** 有効、無効、または制限します (既定では **、すべてのグループ所有者に対するグループ所有者の同意を許可** します)。 チーム所有者が RSC を使用してアプリをインストールするには、そのユーザーのグループ所有者の同意を有効にする必要があります。

![azure rsc 構成](../../assets/images/azure-rsc-configuration.png)

PowerShell を使用してグループ所有者の同意を有効または無効にするには [、「PowerShell を使用してグループ所有者の同意を構成する](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)」で説明されている手順に従います。

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Azure AD ポータル経由でアプリをMicrosoft ID プラットフォームに登録する

Azure Active Directory ポータルは、アプリを登録および構成するための中央プラットフォームを提供します。 アプリを Azure AD ポータルに登録して、Microsoft ID プラットフォームと統合し、Microsoft Graph API を呼び出す必要があります。 詳細については、「[アプリケーションの Microsoft ID プラットフォーム への登録](/graph/auth-register-app-v2)」を参照してください。

>[!WARNING]
>同じ Azure AD アプリ ID に複数のTeamsアプリを登録しないでください。アプリ ID は、アプリごとに一意である必要があります。 同じアプリ ID に複数のアプリをインストールしようとすると失敗します。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Azure AD ポータルでアプリケーションのアクセス許可を確認する

**[ホーム**  =>  **アプリの登録**] ページに移動し、RSC アプリを選択します。 左側のナビゲーション バーから **[API のアクセス許可** ] を選択し、アプリに構成されているアクセス許可の一覧を確認します。 アプリが RSC Graph API 呼び出しのみを行う場合は、そのページのすべてのアクセス許可を削除します。 アプリが RSC 以外の呼び出しを行う場合は、必要に応じてアクセス許可を保持します。

>[!IMPORTANT]
>Azure AD ポータルを使用して RSC アクセス許可を要求することはできません。 RSC のアクセス許可は、現在、Teams クライアントにインストールされているアプリケーションTeams排他的であり、アプリ マニフェスト (JSON) ファイルで宣言されています。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Microsoft ID プラットフォームからアクセス トークンを取得する

API 呼び出しGraphするには、ID プラットフォームからアプリのアクセス トークンを取得する必要があります。 アプリがMicrosoft ID プラットフォームからトークンを取得するには、Azure AD ポータルに登録する必要があります。 アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。

ID プラットフォームからアクセス トークンを取得するには、Azure AD 登録プロセスから次の値を取得する必要があります。

- アプリ登録ポータルによって割り当てられたアプリケーション **ID。** アプリがシングル サインオン (SSO) をサポートしている場合は、アプリと SSO に同じアプリケーション ID を使用する必要があります。
- **クライアント シークレットとパスワード**、または公開キーと秘密キーのペア (**証明書**) ネイティブ アプリの場合、これは必須ではありません。
- Azure AD からの応答を受信するアプリの **リダイレクト URI** (または応答 URL)。

 [「ユーザーの代わりにアクセスを取得する](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)」および「[ユーザーなしでアクセスを取得する」を](/graph/auth-v2-service)*参照してください*。

## <a name="update-your-teams-app-manifest"></a>Teams アプリ マニフェストを更新する

RSC のアクセス許可は、アプリ マニフェスト (JSON) ファイルで宣言されます。  次の値を使用して、アプリ マニフェストに [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーを追加します。

> [!div class="checklist"]
>
> - **id**  — Azure AD アプリ ID。詳細については [、「Azure AD ポータルでのアプリの登録](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)」を参照してください。
> - **リソース**  — 任意の文字列。 このフィールドには RSC に操作はありませんが、エラー応答を避けるために値を追加し、値を指定する必要があります。任意の文字列が実行されます。
> - **アプリケーションのアクセス許可** — アプリの RSC アクセス許可。 詳細については、「 [リソース固有のアクセス許可](resource-specific-consent.md#resource-specific-permissions)」を参照してください。

>
>[!IMPORTANT]
> RSC 以外のアクセス許可は、Azure ポータルに格納されます。 アプリ マニフェストに追加しないでください。
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

## <a name="sideload-your-app-in-teams"></a>Teamsでアプリをサイドロードする

管理者Teamsカスタム アプリのアップロードを許可している場合は、特定のチームに直接[アプリをサイドロード](~/concepts/deploy-and-publish/apps-upload.md)できます。

## <a name="check-your-app-for-added-rsc-permissions"></a>追加された RSC 権限のアプリを確認する

>[!IMPORTANT]
>RSC 権限はユーザーに帰属しません。 呼び出しは、ユーザーが委任したアクセス許可ではなく、アプリのアクセス許可を使用して行われます。 したがって、アプリでは、チャネルの作成やタブの削除など、ユーザーが実行できないアクションを実行できる場合があります。RSC API 呼び出しを行う前に、ユース ケースに対するチーム所有者の意図を確認する必要があります。 詳細については[、「API の概要Microsoft Teams」](/graph/teams-concept-overview)を参照してください。

アプリをチームにインストールしたら[、Graph エクスプローラーを](https://developer.microsoft.com/graph/graph-explorer)使用して、チーム内のアプリに付与されているアクセス許可を表示できます。

> [!div class="checklist"]
>
>- Teamsクライアントからチームの **groupId** を取得します。
> - Teamsクライアントで、左端のナビゲーション バーから **Teams** を選択します。
> - ドロップダウン メニューからアプリがインストールされているチームを選択します。
> - [ **その他のオプション]** アイコン(&#8943;)を選択します。
> - [ **チームへのリンクを取得]** を選択します。
> - 文字列から **groupId** 値をコピーして保存します。
> - **エクスプローラにログインGraph。**
> - 次のエンドポイントに **GET** 呼び出しを行います `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` 。 応答の clientAppId フィールドは、Teams アプリ マニフェストで指定された appId にマップされます。
  ![GET 呼び出しに対するGraphの応答。](../../assets/images/graph-permissions.png)

## <a name="code-sample"></a>コード サンプル
| **サンプル名** | **説明** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| リソース固有の同意 (RSC) | RSC を使用して api を呼び出Graph。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="see-also"></a>関連項目
 
* [Teamsでリソース固有の同意アクセス許可をテストする](test-resource-specific-consent.md)
* [管理者のMicrosoft Teamsでのリソース固有の同意](/MicrosoftTeams/resource-specific-consent)


