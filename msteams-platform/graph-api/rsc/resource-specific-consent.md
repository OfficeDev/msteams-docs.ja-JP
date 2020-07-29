---
title: Teams でのリソース固有の同意
description: Teams でのリソース固有の同意と、その利点を活用する方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams authorization OAuth SSO AAD rsc Graph
ms.openlocfilehash: bf449b338e8c0f42dfef776e533fb6b5ff591529
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434504"
---
# <a name="resource-specific-consent-rsc--developer-preview"></a>リソース固有の同意 (RSC)-開発者プレビュー

>[!NOTE]

>開発者プレビューが有効になっている場合、リソース固有の同意アクセス許可は、デスクトップおよび web クライアントで使用できます。 詳細については、「[開発者プレビューを有効にする方法](../../resources/dev-preview/developer-preview-intro.md)」を参照してください。

リソース固有の同意 (RSC) は Microsoft Teams と Graph API の統合で、アプリが API エンドポイントを使用して組織内の特定のチームを管理できるようにします。 リソース固有の同意 (RSC) アクセス許可モデルを使用すると、チームの*所有者*は、チームのデータにアクセスしたり、変更したりするアプリケーションに同意を与えることができます。 きめ細かい、Teams 固有、RSC の各アクセス許可によって、アプリケーションが特定のチーム内で実行できる処理を定義します。

## <a name="resource-specific-permissions"></a>リソース固有のアクセス許可

|アプリケーションのアクセス許可| アクション |
| ----- | ----- |
|TeamSettings.Read.Group | このチームの設定を取得します。|
|TeamSettings. グループ|このチームの設定を更新します。|
|ChannelSettings.Read.Group|このチームのチャネル名、チャネルの説明、およびチャネルの設定を取得します。|
|ChannelSettings.Edit.Group|このチームのチャネル名、チャネルの説明、およびチャネルの設定を更新します。|
|Channel.Create.Group|このチームのチャネルを作成します。|
|Channel.Delete.Group|このチームのチャネルを削除します。|
|ChannelMessage.Read.Group |このチームのチャネルメッセージを取得します。|
|TeamsApp.Read.Group|このチームのインストール済みアプリのリストを取得します。|
|TeamsTab.Read.Group|このチームのタブのリストを取得します。|
|TeamsTab.Create.Group|このチームのタブを作成します。|
|TeamsTab.Edit.Group|このチームのタブを更新します。|
|TeamsTab.Delete.Group|このチームのタブを削除します。|
|Member.Read.Group|このチームのメンバーを取得します。|
|Owner.Read.Group|このチームの所有者を取得します。|

>[!NOTE]
>リソース固有のアクセス許可は、Teams クライアントにインストールされている Teams アプリに対してのみ使用できます。現在、Azure Active Directory ポータルには含まれていません。

## <a name="enable-resource-specific-consent-in-your-application"></a>アプリケーションでリソース固有の同意を有効にする

アプリケーションで RSC を有効にする手順は次のとおりです。

1. [Azure Active Directory ポータルでグループ所有者の同意設定を構成](#configure-group-owner-consent-settings-in-the-azure-ad-portal)します。
1. Azure AD ポータルを使用して、[アプリを Microsoft identity platform に登録](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)します。
1. [Azure AD ポータルでアプリケーションのアクセス許可を確認する](#review-your-application-permissions-in-the-azure-ad-portal)
1. [Microsoft Identity platform からアクセストークンを取得](#obtain-an-access-token-from-the-microsoft-identity-platform)します。
1. [Teams アプリマニフェストを更新](#update-your-teams-app-manifest)します。
1. [Teams にアプリを直接インストール](#install-your-app-directly-in-teams)します。
1. [アプリで RSC 権限が追加されているかどうかを確認](#check-your-app-for-added-rsc-permissions)します。

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Azure AD ポータルでグループ所有者の同意設定を構成する

Azure portal で直接[グループ所有者の同意](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data)を有効または無効にすることができます。

> [!div class="checklist"]
>
>- [グローバル管理者または会社の管理者](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)として、 [Azure portal](https://portal.azure.com)にサインインします。  
 > - [ **Azure Active Directory**  => **エンタープライズアプリケーション**  => **ユーザー設定**] を選択します。
> - ユーザー**が所有するグループ**(この機能は既定で有効になっています) というラベルの付いたコントロールでユーザーの同意を有効化、無効化、または制限します。

![azure rsc 構成](../../assets/images/azure-rsc-configuration.svg)

| 値 | 説明|
|--- | --- |
|はい | すべてのグループ所有者に対してグループ固有の同意を有効にします。|
|いいえ |すべてのユーザーのグループ固有の同意を無効にします。| 
|いう | 選択したグループのメンバーのグループ固有の同意を有効にします。|

PowerShell を使用して Azure portal でグループ所有者の同意を有効または無効にするには、「 [powershell を使用してグループ所有者の同意を構成](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell)する」に記載されている手順に従います。

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Azure AD ポータルを使用してアプリを Microsoft identity platform に登録する

Azure Active Directory ポータルには、アプリを登録して構成するための一元的なプラットフォームが用意されています。 アプリは、Microsoft identity platform および call Graph Api と統合するために、Azure AD ポータルに登録されている必要があります。 「 [Microsoft identity platform を使用してアプリケーションを登録する」を](/graph/auth-register-app-v2)*参照してください*。

>[!WARNING]
>複数の Teams アプリを同じ Azure AD アプリ id に登録しないでください。アプリ id は、アプリごとに一意である必要があります。 同じアプリ id に複数のアプリをインストールしようとすると失敗します。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Azure AD ポータルでアプリケーションのアクセス許可を確認する

[**ホーム**  =>  **アプリの登録**] ページに移動して、RSC アプリを選択します。 左側のナビゲーションバーから [ **API アクセス許可**] を選択し、アプリに対して構成されているアクセス許可の一覧を確認します。 アプリケーションが RSC Graph 呼び出しのみを行う場合は、そのページに対するすべてのアクセス許可を削除します。 アプリが非 RSC 呼び出しを行う場合は、必要に応じてそれらのアクセス許可を維持します。

>[!IMPORTANT]
>Azure AD portal は、RSC のアクセス許可を要求するために使用することはできません。 RSC のアクセス許可は、現在、Teams クライアントにインストールされ、アプリマニフェスト (JSON) ファイルで宣言されている Teams アプリケーションに対して排他的です。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Microsoft identity platform からアクセストークンを取得する

Graph API の呼び出しを行うには、id プラットフォームからアプリのアクセストークンを取得する必要があります。 アプリが Microsoft identity platform からトークンを取得する前に、Azure AD ポータルに登録されている必要があります。 アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。

Id プラットフォームからアクセストークンを取得するには、Azure AD 登録プロセスの次の値を持っている必要があります。

- アプリ登録ポータルによって割り当てられた**アプリケーション ID** 。 アプリでシングルサインオン (SSO) がサポートされている場合は、アプリと SSO に対して同じアプリケーション ID を使用する必要があります。
- **クライアントシークレット/パスワード**、または公開/秘密キーペア (**証明書**)。 ネイティブ アプリの場合、これは必須ではありません。
- Azure AD からの応答を受信するための、アプリの**リダイレクト URI** (または応答 URL)。

 ユーザー[の代理](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token)としてアクセスを取得し、[ユーザーなしでアクセスを取得する](/graph/auth-v2-service)を*参照してください*。

## <a name="update-your-teams-app-manifest"></a>Teams アプリマニフェストを更新する

RSC アクセス許可は、アプリマニフェスト (JSON) ファイルで宣言されています。  次の値を使用して、 [Webapplicationinfo](../../resources/schema/manifest-schema.md#webapplicationinfo)キーをアプリのマニフェストに追加します。

> [!div class="checklist"]
>
> - **id** : Azure AD アプリ id。*「* [Azure AD ポータルでアプリを登録](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)する」を参照してください。
> - **resource** -任意の文字列。 このフィールドは、RSC では操作を行いませんが、追加して、エラー応答が発生しないように値を設定する必要があります。任意の文字列が実行されます。
> - **アプリケーションのアクセス許可**-アプリの RSC アクセス許可。 [リソース固有の権限](resource-specific-consent.md#resource-specific-permissions)を*参照してください*。

>
>[!IMPORTANT]
> 非 RSC アクセス許可は、Azure portal に格納されます。 アプリマニフェストに追加しないでください。
>

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

## <a name="install-your-app-directly-in-teams"></a>Teams にアプリを直接インストールする

アプリを作成したら、[アプリパッケージ](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab)を特定のチームに直接アップロードすることができます。  そのためには、カスタムアプリのセットアップポリシーの一部として、[**カスタムアプリのアップロード**] ポリシー設定を有効にする必要があります。 *「* [Custom App policy Settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)」を参照してください。

## <a name="check-your-app-for-added-rsc-permissions"></a>アプリで RSC 権限が追加されていることを確認する

>[!IMPORTANT]
>RSC のアクセス許可は、ユーザーには含まれません。 呼び出しは、ユーザーが委任したアクセス許可ではなく、アプリのアクセス許可で行われます。 そのため、アプリは、チャネルの作成やタブの削除など、ユーザーができない操作を実行できる場合があります。RSC API 呼び出しを行う前に、ユースケースに対するチーム所有者の意図を確認する必要があります。 *「* [Microsoft Teams API の概要](/graph/teams-concept-overview)」を参照してください。

アプリがチームにインストールされたら、 [Graph エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)を使用して、チーム内のアプリに付与されているアクセス許可を表示できます。

> [!div class="checklist"]
>
>- Teams クライアントからチームの**groupId**を取得します。
> - Teams クライアントで、左端のナビゲーションバーにある [ **teams** ] を選択します。
> - アプリがインストールされているチームを、ドロップダウンメニューから選択します。
> - [**その他のオプション**] アイコン (&#8943;) を選択します。
> - [**チームへのリンクの取得**] を選択します。
> - 文字列から**groupId**値をコピーして保存します。
> - **Graph エクスプローラー**にログインします。
> - 次のエンドポイントに対して**GET**を `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` 呼び出します。 応答の clientAppId フィールドは、Teams アプリマニフェストで指定されている appId にマップされます。

 ![通話を取得するための Graph エクスプローラーの応答。](../../assets/images/graph-permissions.png)
 
## <a name="test-resource-specific-consent"></a>リソース固有の同意をテストする
 
> [!div class="nextstepaction"]
> [**Teams でのリソース固有の同意権限をテストする**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Teams 管理者向けの関連トピック

> [!div class="nextstepaction"]
> [**管理者のための Microsoft Teams でのリソース固有の同意**](/MicrosoftTeams/resource-specific-consent)
> 
