---
title: タブのコンテキストを取得する
description: タブにユーザー コンテクストを付与する方法を説明します。
ms.localizationpriority: medium
ms.topic: how-to
keywords: チーム タブ ユーザー コンテキスト
ms.openlocfilehash: 8ff93018bd23aad5742c876efddca72edcd67b30
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212420"
---
# <a name="get-context-for-your-tab"></a>タブのコンテキストを取得する

関連するコンテンツを表示するには、コンテキスト情報が必要です。

* ユーザー、チーム、または会社に関する基本情報。
* ロケールとテーマの情報。
* 読み `entityId` 取 `subEntityId` り、またはこのタブ内の何を識別します。

## <a name="user-context"></a>ユーザー コンテキスト

ユーザー、チーム、または会社に関するコンテキストは、次の場合に特に役立ちます。

* アプリ内のリソースを作成または指定したユーザーまたはチームに関連付ける。
* ユーザーまたは他の id プロバイダー Azure Active Directory認証フローを開始し、ユーザーがユーザー名を再入力する必要はありません。 

詳細については、「ユーザーを認証[する」を参照Microsoft Teams。](~/concepts/authentication/authentication.md)

> [!IMPORTANT]
> このユーザー情報は、スムーズなユーザー エクスペリエンスを提供するのに役立ちますが、ID の証明として使用することはできません。  たとえば、攻撃者はブラウザーにページを読み込み、有害な情報や要求を表示する可能性があります。

## <a name="access-context-information"></a>コンテキスト情報にアクセスする

コンテキスト情報には 2 つの方法でアクセスできます。

* URL プレースホルダーの値を挿入します。
* JavaScript クライアント[SDK Microsoft Teams使用します](/javascript/api/overview/msteams-client)。

### <a name="get-context-by-inserting-url-placeholder-values"></a>URL プレースホルダー値を挿入してコンテキストを取得する

構成やコンテンツ URL では、プレースホルダーを使用します。 Microsoft Teams では、実際の構成やコンテンツ URL を決定する際に、プレースホルダーを該当する値で置き換えます。 使用可能なプレースホルダーには、コンテキスト オブジェクトのすべてのフィールド [が含](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) まれます。 一般的なプレースホルダーは次のとおりです。

* {entityId}: 最初の [タブの構成](~/tabs/how-to/create-tab-pages/configuration-page.md) 時に、このタブのアイテムに与えた ID。
* {subEntityId}: このタブ内の特定のアイテムの[](~/concepts/build-and-test/deep-links.md)ディープ リンクを生成するときに指定した ID。これは、エンティティ内の特定の状態に復元するために使用する必要があります。たとえば、特定のコンテンツにスクロールしたり、アクティブ化したりします。
* {loginHint}: ユーザーのログイン ヒントとして適したAzure AD。 これは通常、ホーム テナントの現在のユーザーのログイン名です。
* {userPrincipalName}: 現在のテナント内の現在のユーザーのユーザー プリンシパル名。
* {userObjectId}: 現在Azure AD現在のユーザーのオブジェクト ID を指定します。
* {theme}: 現在のユーザー インターフェイス (UI) テーマ (例: `default` `dark` 、 、 または `contrast` )
* {groupId}: タブがOffice 365グループの ID。
* {tid}: 現在のユーザーの Azure AD テナント ID。
* {locale}: languageId-countryId(ja-us) として書式設定されたユーザーの現在のロケール。

> [!NOTE]
> 以前の `{upn}` プレースホルダーは、現在では非推奨となっています。 後方互換性のため、現在は `{loginHint}` の同義語となっています。

たとえば、タブ マニフェストで属性を設定すると、サインインしているユーザー `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` には次の属性があります。

* ユーザー名は user@example.com **です**。
* 会社のテナント ID は **e2653c-etc です**。
* これらは id **00209384-etc Office 365グループのメンバーです**。
* ユーザーがテーマを暗Teams設定 **しました**。

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
    "groupId": "Guid identifying the current O365 Group ID",
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
    "hostClientType": "The type of host client. Possible values are android, ios, web, desktop, rigel",
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

> [!Note]
> プライベート チャネルは、現在、開発者のプライベートなプレビューです。

コンテンツ ページがプライベート チャネルに読み込まれると、通話から受け取ったデータは、チャネルのプライバシーを保護するために難読 `getContext` 化されます。 

コンテンツ ページがプライベート チャネルにある場合、次のフィールドが変更されます。

* `groupId`: プライベート チャネルの場合は未定義
* `teamId`: プライベート チャネルの threadId に設定します。
* `teamName`: プライベート チャネルの名前に設定する
* `teamSiteUrl`: プライベート チャネル用の個別の一意のSharePointサイトの URL に設定します。
* `teamSitePath`: プライベート チャネル用の個別の一意のSharePointパスに設定します。
* `teamSiteDomain`: プライベート チャネル用の個別の一意のSharePointドメインに設定します。

ページでこれらの値を使用する場合は、フィールドをチェックして、ページがプライベート チャネルに読み込まれているかどうかを判断し、適切に `channelType` 対応する必要があります。

> [!Note]
> `teamSiteUrl` 標準チャネルでも動作します。

## <a name="handle-theme-change"></a>テーマの変更を処理する

呼び出してテーマが変更された場合に通知するアプリを登録できます `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` 。

関数 `theme` の引数は、、 、または の値を持つ `default` `dark` 文字列です `contrast` 。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>関連項目

* [タブデザインのガイドライン](../../tabs/design/tabs.md)
* [Teamsタブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [タブでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-tabs.md)