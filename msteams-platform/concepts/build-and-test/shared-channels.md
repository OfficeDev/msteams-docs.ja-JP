---
title: Teams Connect共有チャネル
author: Rajeshwari-v
description: 共有チャネルをTeams Connectして、テナントを切り替えずに共有スペース内の内部および外部ユーザーと安全に共同作業する方法について説明します。
ms.author: surbhigupta
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: d1f2d212c33f80ce6a5d27e93bda0551d26542dd
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789927"
---
# <a name="microsoft-teams-connect-shared-channels"></a>共有チャネルをMicrosoft Teams Connectする

Microsoft Teams Connect共有チャネルを使用すると、チャネルのメンバーが他のチームや組織のユーザーと共同作業できるようになります。 共有チャネルは、次のように作成して共有できます。

* 同じ組織内の別のチームのメンバー。
* 同じ組織内の個人。
* 個人および他の組織の他のチーム。

Teams Connect共有チャネルは、安全なコラボレーションをシームレスに促進します。 組織外の外部ユーザーが、ユーザー コンテキストを変更せずに Teams の内部ユーザーと共同作業できるようにします。 たとえば、ゲスト アカウントの使用とは異なり、ユーザー エクスペリエンスを強化します。たとえば、メンバーは Teams からサインアウトし、ゲスト アカウントを使用して再びサインインする必要があります。 Teams アプリケーションは、強力なコラボレーション 領域を拡張します。

:::image type="content" source="~/assets/images/app-fundamentals/shared-channels-teams.png" alt-text="組織 A のチーム B と、チーム A として共有チャネルで共同作業している組織 B のチーム C を示す図。" border="true" :::

## <a name="enable-your-app-for-shared-channels"></a>共有チャネルに対してアプリを有効にする

SupportedChannelTypes は、標準以外のチャネルでアプリを有効にする省略可能なプロパティです。 アプリがチーム スコープをサポートし、プロパティが定義されている場合、Teams では、それに応じて各チャネルの種類でアプリが有効になります。 プライベート チャネルと共有チャネルは現在サポートされています。 詳細については、「 [supportedChannelTypes」を](../../resources/schema/manifest-schema.md#supportedchanneltypes)参照してください。

```JSON
"supportedChannelTypes": {
      "type": "array",
      "description": "List of ‘non-standard’ channel types that the app supports. Note: Channels of standard type are supported by default if the app supports team scope. ",
      "maxItems": 2,
      "items": { 
        "enum": [
          "sharedChannels",
          "privateChannels"
        ]
      }
    }
```

> [!NOTE]
>
> * アプリがチーム スコープをサポートしている場合、このプロパティで定義されている値に関係なく、アプリは標準チャネルで機能します。
> * アプリが適切に機能するためには、これらの各チャネルの種類の一意のプロパティを考慮する必要がある場合があります。

## <a name="get-context-for-shared-channels"></a>共有チャネルのコンテキストを取得する

コンテンツ UX が共有チャネルに読み込まれる場合は、共有チャネルの変更の呼び出しから `getContext` 受信したデータを使用します。 `getContext` 呼び出しでは、 `hostTeamGroupID` Microsoft Graph API を使用してチャネル メンバーシップを取得するために使用される 2 つの新しいプロパティと `hostTenantID`、 が発行されます。 `hostTeam` は、共有チャネルを作成するチームです。

タブを有効にする方法の詳細については、次を参照してください。

* [プライベート チャネルのタブのコンテキストを取得する](../../tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels)
* [共有チャネルでコンテキストを取得する](../../tabs/how-to/access-teams-context.md#get-context-in-shared-channels)

## <a name="apps-and-permissions-in-shared-channels"></a>共有チャネルのアプリとアクセス許可

共有チャネルを使用して、組織外の外部メンバーと共同作業を行うことができます。 共有チャネルのアプリのアクセス許可は、ホスト チームのアプリ名簿とホスト テナントのアプリ ポリシーに従います。

> [!NOTE]
> [アクティビティ フィード通知 API](/graph/teams-send-activityfeednotifications) では、共有チャネル内のアプリのテナント間通知はサポートされていません。

## <a name="get-shared-channel-membership"></a>共有チャネル メンバーシップを取得する

を使用し、次の手順に従って、直接共有チャネル メンバーシップを`hostTeamGroupID``getContext`取得できます。

1. [GET チャネル メンバー API API](/graph/api/channel-list-members?view=graph-rest-beta&tabs=http&preserve-view=true) を使用して直接メンバーを取得します。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. GET API を使用して各共有チームを取得 `sharedWithTeams` します。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams
    ```

3. GET API で各共有チーム (チーム X) の GET `sharedWithTeams` メンバーを使用します。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams/{teamX}/members
    ```

## <a name="classify-members-in-the-shared-channel-as-in-tenant-or-out-tenant"></a>共有チャネルのメンバーをテナント内またはテナント外として分類する

メンバーまたはチーム`hostTeamTenantID`を次のように比較することで、メンバーを`tenantID`テナント内またはテナント外として分類できます。

1. 比較するメンバーを取得します。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. を使用して `getContext`、メンバーの を `tenantID` プロパティと `hostTenantID` 比較します。

## <a name="azure-ad-native-identity"></a>Azure AD ネイティブ ID

アプリは、インストールと使用状況でテナント間で機能する必要があります。 次の表に、チャネルの種類とそれに対応するグループ ID を示します。

|チャネルの種類| groupId | hostTeamGroupId |
|----------|---------|-----------------|
|Regular | チーム Azure AD グループ ID | チーム Azure AD グループ ID |
|共有 | Empty | ホスト チーム Azure AD グループ ID |

## <a name="see-also"></a>関連項目

* [Teams の [ビルド] タブ](../../tabs/what-are-tabs.md)
* [Teams のアプリ マニフェストのスキーマ](../../resources/schema/manifest-schema.md)
* [Microsoft Teamsの共有チャネル](/MicrosoftTeams/shared-channels)
* [チャネル リソースの種類](/graph/api/resources/channel)
* [Teams の場所のアイテム保持ポリシー](/microsoft-365/compliance/create-retention-policies)
