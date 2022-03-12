---
title: タブのコンテキストを取得する
description: タブにユーザー コンテクストを付与する方法を説明します。
ms.localizationpriority: medium
ms.topic: how-to
keywords: チーム タブ ユーザー コンテキスト
ms.openlocfilehash: b991a9703faedd3b849287abd5aef2d42e1baf9e
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453685"
---
# <a name="get-context-for-your-tab"></a>タブのコンテキストを取得する

関連するコンテンツを表示するには、コンテキスト情報が必要です。

* ユーザー、チーム、または会社に関する基本情報。
* ロケールとテーマの情報。
* 読み取 `entityId` り、 `subEntityId` またはこのタブ内の何を識別します。

## <a name="user-context"></a>ユーザー コンテキスト

ユーザー、チーム、または会社に関するコンテキストは、次の場合に特に役立ちます。

* アプリ内のリソースを作成または指定したユーザーまたはチームに関連付ける。
* 認証フローは、Microsoft Azure Active Directory (Azure AD) または他の ID プロバイダーから開始し、ユーザーがユーザー名を再入力する必要はありません。

詳細については、「ユーザーを認証[する」](~/concepts/authentication/authentication.md)を参照Microsoft Teams。

> [!IMPORTANT]
> このユーザー情報は、スムーズなユーザー エクスペリエンスを提供するのに役立ちますが、ID の証明として使用することはできません。  たとえば、攻撃者はブラウザーにページを読み込み、有害な情報や要求を表示する可能性があります。

## <a name="access-context-information"></a>コンテキスト情報にアクセスする

コンテキスト情報には 2 つの方法でアクセスできます。

* URL プレースホルダーの値を挿入します。
* [JavaScript クライアント SDK Microsoft Teams使用します](/javascript/api/overview/msteams-client)。

### <a name="get-context-by-inserting-url-placeholder-values"></a>URL プレースホルダー値を挿入してコンテキストを取得する

構成やコンテンツ URL では、プレースホルダーを使用します。 Microsoft Teams では、実際の構成やコンテンツ URL を決定する際に、プレースホルダーを該当する値で置き換えます。 使用可能なプレースホルダーには、コンテキスト オブジェクトのすべてのフィールド [が含](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) まれます。 一般的なプレースホルダーは次のとおりです。

* {entityId}: 最初の [タブの構成](~/tabs/how-to/create-tab-pages/configuration-page.md) 時に、このタブのアイテムに与えた ID。
* {subEntityId}: このタブ内の特定のアイテムのディープ [](~/concepts/build-and-test/deep-links.md) リンクを生成するときに指定した ID。これは、エンティティ内の特定の状態に復元するために使用する必要があります。たとえば、特定のコンテンツにスクロールしたり、アクティブ化したりします。
* {loginHint}: ユーザーのログイン ヒントとして適したAzure AD。 これは通常、ホーム テナントの現在のユーザーのログイン名です。
* {userPrincipalName}: 現在のテナント内の現在のユーザーのユーザー プリンシパル名。
* {userObjectId}: 現在Azure AD現在のユーザーのオブジェクト ID を指定します。
* {theme}: 現在のユーザー インターフェイス (UI) テーマ `default`(例: 、 `dark`、 `contrast`または )
* {groupId}: タブがOffice 365グループの ID。
* {tid}: 現在のユーザーの Azure AD テナント ID。
* {locale}: languageId-countryId(ja-us) として書式設定されたユーザーの現在のロケール。

> [!NOTE]
> 以前の `{upn}` プレースホルダーは、現在では非推奨となっています。 後方互換性のため、現在は `{loginHint}` の同義語となっています。

たとえば、タブ マニフェストで属性`configURL``"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`を設定すると、サインインしているユーザーには次の属性があります。

* ユーザー **名は user@example.com**。
* 会社のテナント ID **は e2653c-などです**。
* id **00209384-などOffice 365グループのメンバーです**。
* ユーザーが自分のテーマをTeamsに設定 **しました**。

タブを構成すると、次Teams URL が呼び出されます。

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>JavaScript ライブラリを使用してコンテキストMicrosoft Teams取得する

[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) を使用して `microsoftTeams.getContext(function(context) { /* ... */ })` を呼び出す方法でも、上記の情報を取得できます。

次のコードは、コンテキスト変数の例を示しています。

```json
{
    "teamId": "The Microsoft Teams ID in the format 19:[id]@thread.skype",
    "teamName": "The name of the current team",
    "channelId": "The channel ID in the format 19:[id]@thread.skype",
    "channelName": "The name of the current channel",
    "chatId": "The chat ID in the format 19:[id]@thread.skype",
    "locale": "The current locale of the user formatted as languageId-countryId (for example, en-us)",
    "entityId": "The developer-defined unique ID for the entity this content points to",
    "subEntityId": "The developer-defined unique ID for the sub-entity this content points to",
    "loginHint": "A value suitable as a login hint for Azure AD. This is usually the login name of the current user, in their home tenant",
    "userPrincipalName": "The principal name of the current user, in the current tenant",
    "userObjectId": "The Azure AD object id of the current user, in the current tenant",
    "tid": "The Azure AD tenant ID of the current user",
    "groupId": "Guid identifying the current Office 365 Group ID",
    "theme": "The current UI theme: default | dark | contrast",
    "isFullScreen": "Indicates if the tab is in full-screen",
    "teamType": "The type of team",
    "teamSiteUrl": "The root SharePoint site associated with the team",
    "teamSiteDomain": "The domain of the root SharePoint site associated with the team",
    "teamSitePath": "The relative path to the SharePoint site associated with the team",
    "channelRelativeUrl": "The relative path to the SharePoint folder associated with the channel",
    "sessionId": "The unique ID for the current Teams session for use in correlating telemetry data",
    "userTeamRole": "The user's role in the team",
    "isTeamArchived": "Indicates if team is archived",
    "hostClientType": "The type of host client. Possible values are android, ios, web, desktop, surfaceHub, teamsRoomsAndroid, teamsPhones, teamsDisplays rigel (deprecated, use teamsRoomsWindows instead)",
    "frameContext": "The context where tab URL is loaded (for example, content, task, setting, remove, sidePanel)",
    "sharepoint": "The SharePoint context is available only when hosted in SharePoint",
    "tenantSKU": "The license type for the current user tenant. Possible values are enterprise, free, edu, unknown",
    "userLicenseType": "The license type for the current user",
    "parentMessageId": "The parent message ID from which this task module is launched",
    "ringId": "The current ring ID",
    "appSessionId": "The unique ID for the current session used for correlating telemetry data",
    "isCallingAllowed": "Indicates if calling is allowed for the current logged in user",
    "isPSTNCallingAllowed": "Indicates if PSTN calling is allowed for the current logged in user",
    "meetingId": "The meeting ID used by tab when running in meeting context",
    "defaultOneNoteSectionId": "The OneNote section ID that is linked to the channel",
    "isMultiWindow": "The indication whether the tab is in a pop out window"
}
```

## <a name="retrieve-context-in-private-channels"></a>プライベート チャネルでのコンテキストの取得

コンテンツ ページがプライベート `getContext` チャネルに読み込まれると、通話から受け取ったデータは、チャネルのプライバシーを保護するために難読化されます。

コンテンツ ページがプライベート チャネルにある場合、次のフィールドが変更されます。

* `groupId`: プライベート チャネルの場合は未定義
* `teamId`: プライベート チャネルの threadId に設定します。
* `teamName`: プライベート チャネルの名前に設定する
* `teamSiteUrl`: プライベート チャネル用の個別の一意のSharePointサイトの URL に設定します。
* `teamSitePath`: プライベート チャネル用の個別の一意のSharePointパスに設定します。
* `teamSiteDomain`: プライベート チャネルの個別の一意のSharePointドメインに設定します。

ページでこれらの値を`channelType``Private`使用する場合、フィールドの値は、ページがプライベート チャネルに読み込まれ、適切に応答できるかどうかを判断する必要があります。

## <a name="retrieve-context-in-microsoft-teams-connect-shared-channels"></a>共有チャネルのコンテキストMicrosoft Teams Connect取得する

> [!NOTE]
> 現時点では、Microsoft Teams Connect共有チャネルは[開発者向けプレビューでのみ行](../../resources/dev-preview/developer-preview-intro.md)っています。

コンテンツ ページが Microsoft Teams Connect共有チャネルに`getContext`読み込まれると、通話から受信したデータは、共有チャネル内のユーザーの一意の名簿によって変更されます。

コンテンツ ページが共有チャネルにある場合、次のフィールドが変更されます。

* `groupId`: 共有チャネルに対して未定義。
* `teamId`: チームに設定 `threadId` すると、チャネルは現在のユーザーに対して共有されます。 ユーザーが複数のチームにアクセスできる場合、共有 `teamId` チャネルをホスト (作成) するチームに設定されます。
* `teamName`: チームの名前に設定すると、チャネルは現在のユーザーに対して共有されます。 ユーザーが複数のチームにアクセスできる場合、共有 `teamName` チャネルをホスト (作成) するチームに設定されます。
* `teamSiteUrl`: 共有チャネルの個別の一意のSharePointサイトの URL に設定します。
* `teamSitePath`: 共有チャネルの個別の一意のSharePointパスに設定します。
* `teamSiteDomain`: 共有チャネルの個別の一意のSharePointドメインに設定します。

これらのフィールドの変更に加えて、共有チャネルで使用できる 2 つの新しいフィールドがあります。

* `hostTeamGroupId`: ホスティング チーム、 `groupId` または共有チャネルを作成したチームに関連付けられているチームに設定します。 このプロパティを使用すると、Microsoft Graph呼び出しで共有チャネルのメンバーシップを取得できます。
* `hostTeamTenantId`: ホスティング チーム、 `tenantId` または共有チャネルを作成したチームに関連付けられているチームに設定します。 プロパティは、フィールド内にある現在のユーザーのテナント ID `tid` `getContext` と相互参照して、ユーザーがホスティング チームのテナントの内部または外部かどうかを判断できます。

ページでこれらの値を`channelType``Shared`使用する場合、フィールドの値は、ページが共有チャネルに読み込まれ、適切に応答できるかどうかを判断する必要があります。

## <a name="handle-theme-change"></a>テーマの変更を処理する

呼び出してテーマが変更された場合に通知するアプリを登録できます `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`。

関数`theme`の引数は、、 、または `default``dark`の値を持つ文字列です`contrast`。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>関連項目

* [タブデザインのガイドライン](../../tabs/design/tabs.md)
* [Teamsタブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [タブでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
