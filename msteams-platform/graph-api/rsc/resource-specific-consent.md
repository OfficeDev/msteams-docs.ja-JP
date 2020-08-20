---
title: Teams でのリソース固有の同意
description: Teams でのリソース固有の同意とその活用方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams 承認 OAuth SSO AAD rsc Graph
ms.openlocfilehash: 7e3fc3faa111f4ba982c1c79e6b5b873b8773aef
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819183"
---
# <a name="resource-specific-consent-rsc"></a>リソース固有の同意 (RSC)

>[!IMPORTANT]
> これらの API にはエンドポイントからアクセス https://graph.microsoft.com/beta できます。  ベ [ータ版](/graph/versioning-and-support#beta-version) のエンドポイントには、現在プレビュー段階であり、まだ一般公開されていない API が含まれます。 ベータ版のエンドポイントの API は変更されることがあります。運用アプリ内で使用することはお勧めしません。 

リソース固有の同意 (RSC) は、アプリで API エンドポイントを使用して組織内の特定のチームを管理できる Microsoft Teams と Graph API 統合です。 リソース固有の同意 (RSC) 許可モデルを *使用すると* 、アプリケーションに対する同意をチーム所有者がチームのデータにアクセスしたり、変更したりすることができます。 細かい Teams 固有の RSC アクセス許可によって、アプリケーションが特定のチーム内で実行できる操作が定義されます。

## <a name="resource-specific-permissions"></a>リソース固有のアクセス許可

|アプリケーションのアクセス許可| Action |
| ----- | ----- |
|TeamSettings.Read.Group | このチームの設定を取得します。|
|TeamSettings.Edit.Group|このチームの設定を更新します。|
|ChannelSettings.Read.Group|このチームのチャネル名、チャネルの説明、チャネルの設定を取得します。|
|ChannelSettings.ReadWrite.Group|このチームのチャネルの名前、チャネルの説明、チャネルの設定を更新します。|
|Channel.Create.Group|このチームのチャネルを作成します。|
|Channel.Delete.Group|このチームのチャネルを削除します。|
|ChannelMessage.Read.Group |このチームのチャネル メッセージを取得します。|
|TeamsApp.Read.Group|このチームがインストールしたアプリの一覧を取得します。|
|TeamsTab.Read.Group|このチームのタブの一覧を取得します。|
|TeamsTab.Create.Group|このチームのタブを作成します。|
|TeamsTab.ReadWrite.Group|このチームのタブを更新します。|
|TeamsTab.Delete.Group|このチームのタブを削除します。|
|Member.Read.Group|このチームのメンバーを取得します。|
|Owner.Read.Group|このチームの所有者を取得します。|

>[!NOTE]
>リソース固有のアクセス許可は、Teams クライアントにインストールされている Teams アプリのみで利用できます。現時点では、Azure Active Directory ポータルの一部には含ていません。

## <a name="enable-resource-specific-consent-in-your-application"></a>リソースに固有のアプリケーションの同意を有効にする

アプリケーションで RSC を有効にする手順は次のとおりです。

1. [Azure Active Directory ポータルでグループ所有者の同意設定を構成します](#configure-group-owner-consent-settings-in-the-azure-ad-portal)。
1. [Azure ポータルポータルから Microsoft ID プラットフォームにアプリを登録ADします](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
1. [Azure ポータルでアプリケーションのアクセス許可をADする](#review-your-application-permissions-in-the-azure-ad-portal)
1. [Microsoft ID プラットフォームからアクセス トークンを取得します](#obtain-an-access-token-from-the-microsoft-identity-platform)。
1. [Teams アプリ マニフェストを更新します](#update-your-teams-app-manifest)。
1. [アプリを Teams に直接インストールします](#install-your-app-directly-in-teams)。
1. [追加の RSC アクセス許可がアプリに付与されているか確認します](#check-your-app-for-added-rsc-permissions)。

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Azure ポータルでグループ所有者の同意設定ADする

グループ所有者の同意  [は、Azure ポータルで](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) 直接有効または無効にすることができます。

> [!div class="checklist"]
>
>- グローバル管理者または会社 [管理者として Azure](https://portal.azure.com) [portal にサインインします](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)。  
 > - **Azure Active Directory Enterprise アプリケーション**  => **のユーザー設定**  => **を選択します**。
> - ユーザーのラベルが付いた管理ラベルが付いたユーザーによる同意の許可 **に同意する、無効化、または制限を、所有グループの企業データにアクセスするアプリに同意することができます** (既定ではこの機能は有効です)。

![Azure Rsc の構成](../../assets/images/azure-rsc-configuration.svg)

| 値 | 説明|
|--- | --- |
|はい | グループ固有の同意をすべてのグループ所有者に対して有効にします。|
|いいえ |すべてのユーザーに対してグループ固有の同意を無効にします。| 
|制限付き | 選択したグループのメンバーに対してグループ固有の同意を有効にします。|

PowerShell を使用して Azure portal 内でグループ所有者の同意を有効または無効にするには、PowerShell を使用してグループ所有者 [の同意を構成する手順に従います](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell)。

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Azure AD ポータルから Microsoft ID プラットフォームにアプリを登録する

Azure Active Directory ポータルは、アプリを登録および構成するための中央プラットフォームを提供します。 Microsoft ID プラットフォームと統合し、Graph API を呼び出すには、アプリを Azure AD ポータルに登録する必要があります。 *「*[アプリケーションを Microsoft ID プラットフォームに登録する」を参照してください](/graph/auth-register-app-v2)。

>[!WARNING]
>複数の Teams アプリを同じ Azure アプリ ID にADしないようにします。アプリ ID は、アプリごとに一意にする必要があります。 同じアプリ ID に対して複数のアプリをインストールしようとすると失敗します。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Azure ポータルでアプリケーションのアクセス許可をADする

ホーム アプリの**登録ページ**  =>  **に移動し、RSC**アプリを選択します。 左側 **のナビゲーション バー** から API アクセス許可を選択し、アプリに構成されているアクセス許可の一覧を確認します。 アプリが RSC グラフ呼び出しのみを行う場合は、そのページですべてのアクセス許可を削除します。 アプリで RSC 以外の呼び出しを行う場合は、必要に応じてこれらのアクセス許可を保持します。

>[!IMPORTANT]
>Azure ADは RSC アクセス許可を要求するために使用できません。 RSC アクセス許可は、現在 Teams クライアントにインストールされている Teams アプリケーションに対してのみで、アプリ マニフェスト (JSON) ファイルで宣言されます。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Microsoft ID プラットフォームからアクセス トークンを取得する

Graph API を呼び出すには、ID プラットフォームからアプリのアクセス トークンを取得する必要があります。 アプリが Microsoft ID プラットフォームからトークンを取得するには、その前に Azure ポータルに登録しておくADがあります。 アクセス トークンには、アプリとアプリに付与されているアクセス許可に関する情報が含まれています。このアクセス許可は、Microsoft Graph を通じて利用できるリソースと API に対応するものです。

ID プラットフォームからアクセス トークンを取得するには、Azure AD の登録プロセスから次に示す値が必要になります。

- アプリ **登録ポータルによって** 割り当てられたアプリケーション ID。 アプリがシングル サインオン (SSO) をサポートする場合は、アプリと SSO で同じアプリケーション ID を使用する必要があります。
- クライアント  **シークレット/パスワード** 、または公開/秘密キーのペア (**証明書)** です。 ネイティブ アプリの場合、これは必須ではありません。
- Azure **アプリからの** 応答を受信するためのリダイレクト URI (またはAD。

 *ユーザー*[に代わって取得するアクセスと、ユーザーなし](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token)[の Get アクセスの表示](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Teams アプリ マニフェストを更新する

RSC アクセス許可はアプリ マニフェスト ファイル (JSON) で宣言されます。  次の [値を使用して](../../resources/schema/manifest-schema.md#webapplicationinfo) 、アプリ マニフェストに webApplicationInfo キーを追加します。

> [!div class="checklist"]
>
> - **id**  — Azure AD アプリ ID。 *Azure* [ポータルのアプリの登録AD覧ください](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
> - **resource**  — 任意の文字列。 このフィールドは RSC では操作を実行できませんが、追加されたものである必要があります。また、エラー応答を回避するためにはその値が設定されている必要があります。任意の文字列を使用します。
> - **アプリケーションのアクセス** 許可 — アプリ用の RSC 権限。 *リソース固有*[のアクセス許可を参照してください](resource-specific-consent.md#resource-specific-permissions)。

>
>[!IMPORTANT]
> RSC 以外のアクセス許可は Azure portal に格納されます。 アプリ マニフェストには追加しないでください。
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

## <a name="install-your-app-directly-in-teams"></a>アプリを Teams に直接インストールする

アプリを作成したら、アプリ パッケージ [を特定のチーム](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) に直接アップロードできます。  この操作を行うには、[ **カスタム アプリのアップロード]** ポリシーの一部として、カスタム アプリのアップロード ポリシー設定を有効にする必要があります。 *カスタム アプリ*[ポリシー設定をご覧ください](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)。

## <a name="check-your-app-for-added-rsc-permissions"></a>追加の RSC アクセス許可がアプリに付与されているか確認する

>[!IMPORTANT]
>RSC のアクセス許可はユーザーに属性が設定されません。 呼び出しは、ユーザーに委任されたアクセス許可で行われません。 そのため、アプリは、チャネルの作成やタブの削除など、ユーザーが操作できないアクションを実行できる場合があります。RSC API 呼び出しを行う前に、チーム所有者の使用目的を確認する必要があります。 *Microsoft* [Teams API の概要を参照してください](/graph/teams-concept-overview)。

アプリがチームにインストールされると [、Graph エクスプローラ](https://developer.microsoft.com/graph/graph-explorer)  ーを使用して、チーム内のアプリに付与されているアクセス許可を表示できます。

> [!div class="checklist"]
>
>- Teams クライアントからチーム **の groupId** を取得します。
> - Teams クライアントで、左のナビゲーション バーから **Teams** を選択します。
> - ドロップダウン メニューから、アプリがインストールされているチームを選択します。
> - [その他 **のオプション] アイコン** (タスク&#8943;)。
> - [ **チームへのリンクを取得] を選します**。
> - 文字列から **groupId 値をコピー** して保存します。
> - Graph エクスプローラ **ーにログインします**。
> - 次のエンド **ポイントに** 対して GET を呼び出します `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` : 。 応答の clientAppId フィールドは、Teams アプリ マニフェストで指定された appId にマップされます。
  ![Get 呼び出しに対する Graph エクスプローラーの応答。](../../assets/images/graph-permissions.png)
 
## <a name="test-resource-specific-consent"></a>リソース固有の同意をテストする
 
> [!div class="nextstepaction"]
> [**Teams でリソース固有の同意のアクセス許可をテストする**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Teams 管理者向けの関連トピック

> [!div class="nextstepaction"]
> [**管理者向けに Microsoft Teams でのリソース固有の同意**](/MicrosoftTeams/resource-specific-consent)
> 
