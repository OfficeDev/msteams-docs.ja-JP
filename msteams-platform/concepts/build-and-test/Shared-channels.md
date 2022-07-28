---
title: 共有チャネル
author: Rajeshwari-v
description: 共有チャネルとの共同作業。
ms.author: surbhigupta
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 96cd3014fa1cee38832724e1b50cf29db372d711
ms.sourcegitcommit: d40ea0d504db66d49bbe0955f7031db1cd210056
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2022
ms.locfileid: "67060042"
---
# <a name="shared-channels"></a>共有チャネル

Microsoft Teams の共有チャネルを使用すると、チャネルのメンバーは他の Teams や組織のユーザーと共同作業できます。 共有チャネルは、次のユーザーと作成して共有できます。

* 同じ組織内の別のチームのメンバー。
* 同じ組織内の個人。
* 個人と他の組織の他のチーム。

共有チャネルを使用すると、コラボレーションがシームレスに促進されます。 組織外の外部ユーザーが、ユーザー コンテキストを変更せずに Teams 内の内部ユーザーと共同作業できるようにします。 たとえば、メンバーはゲスト アカウントを使用する場合とは異なり、ユーザー エクスペリエンスを強化します。たとえば、メンバーは Teams からサインアウトし、ゲスト アカウントを使用してもう一度サインインする必要があります。 Teams アプリケーションは、強力なコラボレーション領域を拡張できるようになりました。

:::image type="content" source="~/assets/images/app-fundamentals/shared-channels-teams.png" alt-text="共有チャネル イメージ"border="true" :::

## <a name="manifest-update-in-shared-channels"></a>共有チャネルでのマニフェストの更新

コンテンツ UX が共有チャネルに読み込まれる場合は、共有チャネルの変更の呼び出しから `getContext` 受信したデータを使用します。 `getContext`call は 2 つの新しいプロパティを発行します`hostTenantID`。このプロパティは、 `hostTeamGroupID` Microsoft Graph API を使用してチャネル メンバーシップを取得するために使用されます。 `hostTeam` は、共有チャネルを作成するチームです。

SupportedChannelTypes は、非標準チャネルでアプリを有効にする省略可能なプロパティです。 アプリがチーム スコープをサポートし、プロパティが定義されている場合、Teams はそれに応じて各チャネルの種類でアプリを有効にします。 現在、プライベート チャネルと共有チャネルがサポートされています。 詳細については、「[supportedChannelTypes」を](../../resources/schema/manifest-schema.md#supportedchanneltypes)参照してください。

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
> * アプリがチーム スコープをサポートしている場合、このプロパティで定義されている値に関係なく、標準チャネルで機能します。
> * アプリが適切に機能するために、これらのチャネルの種類ごとに一意のプロパティを考慮する必要がある場合があります。

タブを有効にする方法の詳細については、次を参照してください。

* [プライベート チャネルのタブのコンテキストを取得する](../../tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels)
* [共有チャネルのタブのコンテキストを取得する](../../tabs/how-to/access-teams-context.md#retrieve-context-in-microsoft-teams-connect-shared-channels)

## <a name="apps-and-permissions-in-shared-channels"></a>共有チャネルのアプリとアクセス許可

共有チャネルを使用して、組織外の外部メンバーと共同作業できます。 共有チャネルのアプリのアクセス許可は、ホスト チームのアプリ名簿とホスト テナントのアプリ ポリシーに従います。

> [!NOTE]
> [アクティビティ フィード通知 API](/graph/teams-send-activityfeednotifications) では、共有チャネル内のアプリのテナント間通知はサポートされません。

## <a name="get-shared-channel-membership"></a>共有チャネル メンバーシップを取得する

次の手順を`getContext`使用して、直接共有チャネル メンバーシップを`hostTeamGroupID`取得できます。

1. [GET チャネル メンバー API API](/graph/api/channel-list-members?view=graph-rest-beta&tabs=http&preserve-view=true) を使用して直接メンバーを取得します。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. GET API を使用して各共有チームを取得 `sharedWithTeams` します。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams
    ```

3. GET API を使用して、各共有チーム (Team X) の GET メンバーを `sharedWithTeams` 使用します。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams/{teamX}/members
    ```

## <a name="classify-members-in-the-shared-channel-as-in-tenant-or-out-tenant"></a>共有チャネル内のメンバーをテナント内またはテナント外として分類する

メンバーまたはチーム`hostTeamTenantID`を次のように比較することで、メンバーを`tenantID`テナント内またはテナント外として分類できます。

1. 比較するメンバーを取得します。

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. を使用して `getContext`、 `tenantID` メンバーのプロパティを `hostTenantID` 比較します。

## <a name="azure-ad-native-identity"></a>Azure AD ネイティブ ID

アプリは、インストールと使用状況でテナント間で機能する必要があります。 次の表に、チャネルの種類と対応するグループ ID を示します。

|チャネルの種類| groupId | hostTeamGroupId |
|----------|---------|-----------------|
|Regular | Team Azure AD グループ ID | Team Azure AD グループ ID |
|共有 | Empty | Host Team Azure AD グループ ID |

## <a name="see-also"></a>関連項目

* [Teams の [ビルド] タブ](../../tabs/what-are-tabs.md)
* [Teams のアプリ マニフェストのスキーマ](../../resources/schema/manifest-schema.md)
