---
title: Teams でのリソース固有の同意
description: Teams でのリソース固有の同意と、それを活用する方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: Teams 承認 OAuth SSO AAD rsc Graph
ms.openlocfilehash: 97f642b203a1f7fb4cd9332b61265c0b27788e2b
ms.sourcegitcommit: 6caf503de5544fb8b9c8c6bef8eff4ff5a46068c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/17/2021
ms.locfileid: "50270799"
---
# <a name="resource-specific-consent-rsc"></a>リソース固有の同意 (RSC)

リソース固有の同意 (RSC) は、アプリが API エンドポイントを使用して組織内の特定のチームを管理できる Microsoft Teams と Microsoft Graph API の統合です。 リソース固有の同意 (RSC) アクセス許可モデルを使用すると、チーム所有者は、アプリケーションがチームのデータにアクセスしたり変更したりするための同意を付与できます。 Teams 固有の RSC の詳細なアクセス許可は、アプリケーションが特定のチーム内で実行できる操作を定義します。

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
>リソース固有のアクセス許可は、Teams クライアントにインストールされている Teams アプリでのみ使用できます。現在、Azure Active Directory ポータルには含められません。

## <a name="enable-resource-specific-consent-in-your-application"></a>アプリケーションでリソース固有の同意を有効にする

アプリケーションで RSC を有効にする手順は次のとおりです。

1. [Azure Active Directory ポータルでグループ所有者の同意設定を構成します](#configure-group-owner-consent-settings-in-the-azure-ad-portal)。
1. [Azure AD ポータルを使用して、Microsoft](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)ID プラットフォームにアプリを登録します。
1. [Azure AD ポータルでアプリケーションのアクセス許可を確認します](#review-your-application-permissions-in-the-azure-ad-portal)。
1. [Microsoft Identity プラットフォームからアクセス トークンを取得します](#obtain-an-access-token-from-the-microsoft-identity-platform)。
1. [Teams アプリ マニフェストを更新します](#update-your-teams-app-manifest)。
1. [Teams に直接アプリをインストールします](#install-your-app-directly-in-teams)。
1. [RSC のアクセス許可が追加されていないかアプリを確認します](#check-your-app-for-added-rsc-permissions)。

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Azure AD ポータルでグループ所有者の同意設定を構成する

Azure Portal 内で直接 [グループ所有者の同意](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) を有効または無効にできます。

> [!div class="checklist"]
>
>- グローバル管理者/ [会社管理者として Azure Portal](https://portal.azure.com) [にサインインします](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)。  
 > - [[Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Active Directory Enterprise**  =>  **アプリケーションの同意とアクセス**  =>  **許可]** ユーザーの同意  =>  **設定を選択します**。
> - データにアクセスするアプリに対するグループ所有者の同意というラベルが付いたコントロールを使用して、ユーザーの同意を有効、無効、または制限します **(既定** では、すべてのグループ所有者に対するグループ所有者の同意 **を許可します**)。 チーム所有者が RSC を使用してアプリをインストールするには、そのユーザーに対してグループ所有者の同意を有効にする必要があります。

![azure rsc の構成](../../assets/images/azure-rsc-configuration.png)

PowerShell を使用してグループ所有者の同意を有効または無効にするには、「PowerShell を使用してグループ所有者の同意を構成する」で説明 [されている手順に従います](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Azure AD ポータルを使用してアプリを Microsoft ID プラットフォームに登録する

Azure Active Directory ポータルは、アプリを登録および構成する中心的なプラットフォームを提供します。 Microsoft ID プラットフォームと統合し、Microsoft Graph API を呼び出AD Azure AD ポータルにアプリを登録する必要があります。 *「Microsoft* [ID プラットフォームにアプリケーションを登録する」を参照してください](/graph/auth-register-app-v2)。

>[!WARNING]
>複数の Teams アプリを同じ Azure アプリ id AD登録しない。アプリ ID は、アプリごとに一意である必要があります。 同じアプリ ID に複数のアプリをインストールしようとすると失敗します。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Azure AD ポータルでアプリケーションのアクセス許可を確認する

[ホーム アプリ **の**  =>  **登録] ページに移動し**、RSC アプリを選択します。 左側 **のナビゲーション バーから API** のアクセス許可を選択し、アプリに対して構成されているアクセス許可の一覧を確認します。 アプリで RSC Graph API 呼び出しのみを行う場合は、そのページのすべてのアクセス許可を削除します。 アプリで RSC 以外の呼び出しも行う場合は、必要に応じてこれらのアクセス許可を保持します。

>[!IMPORTANT]
>Azure AD ポータルを使用して RSC アクセス許可を要求することはできません。 RSC アクセス許可は現在、Teams クライアントにインストールされている Teams アプリケーション専用であり、アプリ マニフェスト (JSON) ファイルで宣言されています。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Microsoft ID プラットフォームからアクセス トークンを取得する

Graph API 呼び出しを行う場合は、ID プラットフォームからアプリのアクセス トークンを取得する必要があります。 アプリが Microsoft ID プラットフォームからトークンを取得するには、その前に Azure AD ポータルに登録する必要があります。 アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。

ID プラットフォームからアクセス トークンを取得するには、Azure AD 登録プロセスから次の値を取得する必要があります。

- アプリ **登録ポータルによって** 割り当てられたアプリケーション ID。 アプリでシングル サインオン (SSO) がサポートされている場合は、アプリと SSO に同じアプリケーション ID を使用する必要があります。
- クライアント  **シークレット/パスワード、** または公開/秘密キーのペア (**証明書**)。 ネイティブ アプリの場合、これは必須ではありません。
- Azure AD からの応答をアプリが受信するリダイレクト **URI** (または応答 URL)。

 *「ユーザー*[の代わりにアクセスを取得する」と「ユーザー](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)なしで [アクセスを取得する」を参照](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Teams アプリ マニフェストを更新する

RSC アクセス許可は、アプリ マニフェスト (JSON) ファイルで宣言されます。  次の [値を使用して、webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加します。

> [!div class="checklist"]
>
> - **id** — Azure ADアプリ ID。Azure AD ポータルにアプリ [を登録するを参照してください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
> - **resource**  — 任意の文字列。 このフィールドは RSC では操作されませんが、エラー応答を回避するために値を追加する必要があります。任意の文字列で実行されます。
> - **アプリケーションのアクセス許可** — アプリの RSC アクセス許可。 *「リソース*[固有のアクセス許可」を参照してください](resource-specific-consent.md#resource-specific-permissions)。

>
>[!IMPORTANT]
> RSC 以外のアクセス許可は、Azure Portal に保存されます。 アプリ マニフェストに追加しません。
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

## <a name="install-your-app-directly-in-teams"></a>Teams に直接アプリをインストールする

アプリを作成したら、アプリ パッケージを特定の [チームに直接](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) アップロードできます。  これを行うには、カスタム アプリ **セットアップ** ポリシーの一部として [カスタム アプリのアップロード] ポリシー設定を有効にする必要があります。 *「カスタム*[アプリ ポリシー設定」をご覧ください](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)。

## <a name="check-your-app-for-added-rsc-permissions"></a>RSC のアクセス許可が追加されていないかアプリを確認する

>[!IMPORTANT]
>RSC アクセス許可はユーザーに属性付けされません。 呼び出しは、ユーザーによって委任されたアクセス許可ではなく、アプリのアクセス許可で行います。 したがって、チャネルの作成やタブの削除など、ユーザーが実行できない操作をアプリで実行できる場合があります。RSC API 呼び出しを行う前に、チーム所有者の使用事例の意図を確認する必要があります。 *Microsoft* [Teams API の概要を参照してください](/graph/teams-concept-overview)。

アプリがチームにインストールされた後 [、Graph エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)  を使用して、チーム内のアプリに付与されているアクセス許可を表示できます。

> [!div class="checklist"]
>
>- Teams クライアントからチーム **の groupId** を取得します。
> - Teams クライアントで、一 **方** の左側のナビゲーション バーから Teams を選択します。
> - アプリがインストールされているチームをドロップダウン メニューから選択します。
> - [その他 **のオプション]** アイコン (&#8943;)。
> - [チーム **へのリンクを取得する] を選択します**。
> - 文字列から **groupId 値をコピー** して保存します。
> - Graph エクスプローラー **にログインします**。
> - 次の **エンドポイントに対** して GET 呼び出しを行います `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` 。 応答の clientAppId フィールドは、Teams アプリ マニフェストで指定された appId にマップされます。
  ![GET 呼び出しに対する Graph エクスプローラーの応答。](../../assets/images/graph-permissions.png)

## <a name="code-sample"></a>コード サンプル
| **サンプルの名前** | **説明** | **C#** |
|-----------------|-----------------|----------------|
| リソース固有の同意 (RSC) | RSC を使用して Graph API を呼び出します。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|

## <a name="test-resource-specific-consent"></a>リソース固有の同意をテストする
 
> [!div class="nextstepaction"]
> [**Teams でリソース固有の同意のアクセス許可をテストする**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Teams 管理者向け関連トピック

> [!div class="nextstepaction"]
> [**管理者向け Microsoft Teams でのリソース固有の同意**](/MicrosoftTeams/resource-specific-consent)
> 

