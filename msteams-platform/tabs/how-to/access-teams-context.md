---
title: タブのコンテキストを取得する
description: タブのコンテキスト、ユーザー、チーム、または会社のコンテキスト、情報へのアクセス、プライベートまたは共有チャネルでのコンテキストの取得、テーマの変更の処理について説明します。
ms.localizationpriority: high
ms.topic: how-to
ms.openlocfilehash: f0a54dc749d1132918e3ec47ac614aff3ce8aab8
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791546"
---
# <a name="get-context-for-your-tab"></a>タブのコンテキストを取得する

関連するコンテンツを表示するには、タブにコンテキスト情報が必要です。

* ユーザー、チーム、または会社に関する基本情報。
* ロケールとテーマの情報。
* `page.id`このタブの内容を識別する と `page.subPageId` (TeamsJS v.2.0.0 以前と`subEntityId`呼ばれます`entityId`)。

## <a name="user-context"></a>ユーザー コンテキスト

ユーザー、チーム、または会社に関するコンテキストは、次の場合に特に役立ちます。

* アプリでリソースを作成するか、指定したユーザーまたはチームに関連付けます。
* Microsoft Azure Active Directory (Azure AD) またはその他の ID プロバイダーから認証フローを開始し、ユーザーが再度ユーザー名を入力する必要はありません。

詳細については、「 [Microsoft Teams でユーザーを認証する](~/concepts/authentication/authentication.md)」を参照してください。

> [!IMPORTANT]
> このユーザー情報はスムーズなユーザー エクスペリエンスを提供するのに役立ちますが、ID 証明として使用しないでください。  たとえば、攻撃者はブラウザーにページを読み込み、有害な情報や要求をレンダリングすることができます。

## <a name="access-context-information"></a>アクセス コンテキスト情報

コンテキスト情報には 2 つの方法でアクセスできます。

* [URL プレースホルダー値](#get-context-by-inserting-url-placeholder-values)の使用。
* Microsoft Teams JavaScript クライアント SDK [コンテキスト](/javascript/api/@microsoft/teams-js/app.context) オブジェクトから。

### <a name="get-context-by-inserting-url-placeholder-values"></a>URL プレースホルダー値を挿入してコンテキストを取得する

構成やコンテンツ URL では、プレースホルダーを使用します。 Microsoft Teams では、実際の構成やコンテンツ URL を決定する際に、プレースホルダーを該当する値で置き換えます。 使用可能なプレースホルダーには、 [コンテキスト](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) オブジェクトのすべてのフィールドが含まれます。 一般的なプレースホルダーには、次のプロパティがあります。

* [{page.id}](/javascript/api/@microsoft/teams-js/app.pageinfo#@microsoft-teams-js-app-pageinfo-id): 最初にページを構成するときに定義されたページの開発者が定義した一意 [の](~/tabs/how-to/create-tab-pages/configuration-page.md) ID。 (TeamsJS v.2.0.0 より前と `{entityId}` 呼ばれます)。
* [{page.subPageId}](/javascript/api/@microsoft/teams-js/app.pageinfo#@microsoft-teams-js-app-pageinfo-subpageid): ページ内の特定のアイテムの [ディープ リンク](~/concepts/build-and-test/deep-links.md) を生成するときに定義された、このコンテンツ ポイントのサブページの開発者が定義した一意の ID。 (TeamsJS v.2.0.0 より前と `{subEntityId}` 呼ばれます)。
* [{user.loginHint}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-loginhint): Azure AD のサインイン ヒントとして適した値。 これは通常、ホーム テナント内の現在のユーザーのログイン名です。 (TeamsJS v.2.0.0 より前と `{loginHint}` 呼ばれます)。
* [{user.userPrincipalName}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-userprincipalname): 現在のテナント内の現在のユーザーのユーザー プリンシパル名。 (TeamsJS v.2.0.0 より前と `{userPrincipalName}` 呼ばれます)。
* [{user.id}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-id): 現在のテナント内の現在のユーザーの Azure AD オブジェクト ID。 (TeamsJS v.2.0.0 より前と `{userObjectId}` 呼ばれます)。
* [{app.theme}](/javascript/api/@microsoft/teams-js/app.appinfo#@microsoft-teams-js-app-appinfo-theme): 、 などの`default``dark``contrast`現在のユーザー インターフェイス (UI) テーマ。 (TeamsJS v.2.0.0 より前と `{theme}` 呼ばれます)。
* [{team.groupId}](/javascript/api/@microsoft/teams-js/app.teaminfo#@microsoft-teams-js-app-teaminfo-groupid): タブが存在するOffice 365 グループの ID。 (TeamsJS v.2.0.0 より前と `{groupId}` 呼ばれます)
* [{user.tenant.id}](/javascript/api/@microsoft/teams-js/app.tenantinfo#@microsoft-teams-js-app-tenantinfo-id): 現在のユーザーの Azure AD テナント ID。 (TeamsJS v.2.0.0 より前と `{tid}` 呼ばれます)。
* [{app.locale}](/javascript/api/@microsoft/teams-js/app.appinfo#@microsoft-teams-js-app-appinfo-locale): *languageId-countryId*`en-us` などの形式のユーザーの現在のロケール。 (TeamsJS v.2.0.0 より前と `{locale}` 呼ばれます)。

> [!NOTE]
> 以前の `{upn}` プレースホルダーは、現在では非推奨となっています。 後方互換性のため、現在は `{user.loginHint}` の同義語となっています。

たとえば、アプリ マニフェストで Tab *configurationUrl* 属性を に `"https://www.contoso.com/config?name={user.loginHint}&tenant={user.tenant.id}&group={team.groupId}&theme={app.theme}"` 設定し、サインインしているユーザーに次の属性がある場合です。

* ユーザー名は **user@example.com**。
* 会社のテナント ID は **e2653c-etc です**。
* ID **00209384-etc** を持つOffice 365 グループのメンバーです。
* ユーザーが Teams テーマを **ダーク** に設定しました。

. . . 次に、Teams はタブを構成するときに次の URL を呼び出します。

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Microsoft Teams JavaScript ライブラリを使用してコンテキストを取得する

[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) を使用して `microsoftTeams.getContext(function(context) { /* ... */ })` を呼び出す方法でも、上記の情報を取得できます。

次のコードでは、コンテキスト変数の例を示します。

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

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

## <a name="typescript"></a>TypeScript

```TypeScript
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

同等の `async/await` パターン:

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

## <a name="javascript"></a>JavaScript

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context) => {
    /*...*/
});
```

同等の `async/await` パターン:

```js
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context = await app.getContext();
  /*...*/
}
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

## <a name="typescript"></a>TypeScript

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context: microsoftTeams.Context) => {
  /* ... */
});
```

## <a name="javascript"></a>JavaScript

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => {
  /* ... */ 
});
```

---

次の表は、コンテキスト オブジェクトの一般的に使用される *コンテキスト* プロパティの一覧です。

| TeamsJS v2 名 | TeamsJS v1 名 | 説明 |
|-----------------|-----------------|-------------|
| team.internalId | teamId | コンテンツが関連付けられているチームの Microsoft Teams ID。 |
| team.displayName | teamName | コンテンツが関連付けられているチームの名前。 |
| channel.id | channelId | コンテンツが関連付けられているチャネルの Microsoft Teams ID。 |
| channel.displayName | channelName | コンテンツが関連付けられているチャネルの名前。 |
| chat.id | chatId | コンテンツが関連付けられているチャットの Microsoft Teams ID。 |
| app.locale | ロケール | languageId-countryId (en-us など) として書式設定されたアプリに対してユーザーが構成した現在のロケール。 |
| page.id | entityId | このコンテンツが指すページの開発者が定義した一意の ID。 |
| page.subPageId | subEntityId | このコンテンツが指すサブページの開発者が定義した一意の ID。 このフィールドは、ページ内の特定の状態 (特定のコンテンツへのスクロールやアクティブ化など) に復元するために使用する必要があります。 |
| user.loginHint | loginHint | Azure AD で認証するときにlogin_hintとして使用するのに適した値。 悪意のあるユーザーはブラウザーでコンテンツを実行できるため、この値は、ユーザーが誰であるかについてのヒントとしてのみ使用し、ID の証明として使用しないでください。 このフィールドは、マニフェストで ID アクセス許可が要求された場合にのみ使用できます。 |
| user.userPrincipalName | Upn | 現在のユーザーの UPN。 これは、外部で認証された UPN (ゲスト ユーザーなど) である可能性があります。 悪意のあるパーティがブラウザーでコンテンツを実行するため、この値は、ユーザーが誰であるかについてのヒントとしてのみ使用し、ID の証明として使用しないでください。 このフィールドは、マニフェストで ID アクセス許可が要求された場合にのみ使用できます。 |
| user.id | userObjectId | 現在のユーザーの Azure AD オブジェクト ID。 悪意のあるパーティがブラウザーでコンテンツを実行するため、この値は、ユーザーが誰であるかについてのヒントとしてのみ使用し、ID の証明として使用しないでください。 このフィールドは、マニフェストで ID アクセス許可が要求された場合にのみ使用できます。 |
| user.tenant.id | Tid | 現在のユーザーの Azure AD テナント ID。 悪意のあるユーザーはブラウザーでコンテンツを実行できるため、この値は、ユーザーが誰であるかについてのヒントとしてのみ使用し、ID の証明として使用しないでください。 このフィールドは、マニフェストで ID アクセス許可が要求された場合にのみ使用できます。 |
| team.groupId | groupId | コンテンツが関連付けられているチームのOffice 365 グループ ID。 このフィールドは、マニフェストで ID アクセス許可が要求された場合にのみ使用できます。 |
| app.theme  | theme | 現在の UI テーマ: 既定、濃色、コントラスト |
| page.isFullScreen | IsFullScreen | ページが全画面表示モードであるかどうかを示します。 |
| team.type | teamType | チームの種類。 |
| sharepointSite.teamSiteUrl | teamSiteUrl | チームに関連付けられているルート SharePoint サイト。 |
| sharepointSite.teamSiteDomain | teamSiteDomain | チームに関連付けられているルート SharePoint サイトのドメイン。 |
| sharepointSite.teamSitePath | teamSitePath | チームに関連付けられている SharePoint サイトへの相対パス。 |
| channel.relativeUrl | channelRelativeUrl | チャネルに関連付けられている SharePoint フォルダーへの相対パス。 |
| app.host.sessionId | Sessionid | テレメトリ データの関連付けに使用する現在のホスト セッションの一意の ID。 |
| team.userRole | userTeamRole | チーム内のユーザーのロール。 悪意のあるユーザーはブラウザーでコンテンツを実行できるため、この値はユーザーのロールに関するヒントとしてのみ使用し、ロールの証明として使用しないでください。 |
| team.isArchived | isTeamArchived | チームがアーカイブされているかどうかを示します。 アプリでは、アーカイブされたチームに関連付けられているコンテンツに対する変更を防ぐためのシグナルとしてこれを使用する必要があります。 |
| app.host.clientType | hostClientType | ホスト クライアントの種類。 使用可能な値は、android、ios、Web、デスクトップ、rigel です |
| page.frameContext | frameContext | ページ URL が読み込まれるコンテキスト (コンテンツ、タスク、設定、削除、sidePanel) |
| sharepoint | sharepoint | SharePoint コンテキスト。 これは、SharePoint でホストされている場合にのみ使用できます。 |
| user.tenant.teamsSku | tenantSKU | 現在のユーザー テナントのライセンスの種類。 使用可能な値は、エンタープライズ、無料、edu、不明です |
| user.licenseType | userLicenseType | 現在のユーザーのライセンスの種類。 使用可能な値は、E1、E3、E5 エンタープライズ プランです |
| app.parentMessageId | parentMessageId | このタスク モジュールが起動された親メッセージの ID。 これは、ボット カードから起動されたタスク モジュールでのみ使用できます。 |
| app.host.ringId | ringId | 現在のリング ID。 |
| app.sessionId | appSessionId | テレメトリ データの関連付けに使用する現在のホスト セッションの一意の ID。 |
| user.isCallingAllowed | isCallingAllowed | 現在ログインしているユーザーに対して呼び出しが許可されるかどうかを表します。 |
| user.isPSTNCallingAllowed | isPSTNCallingAllowed | 現在のユーザーに対して PSTN 通話が許可されているかどうかを示します |
| meeting.id | meetingId | 会議コンテキストで実行するときにタブで使用される会議 ID。 |
| channel.defaultOneNoteSectionId | defaultOneNoteSectionId | チャネルにリンクされている OneNote セクション ID。 |
| page.isMultiWindow | isMultiWindow | タブがポップアップ ウィンドウ内にあるかどうかを示します。 |

詳細については、「[コンテキスト インターフェイスへの更新」と *「コンテキスト* インターフェイス](using-teams-client-sdk.md#updates-to-the-context-interface) API リファレンス [](/javascript/api/@microsoft/teams-js/app.context)」を参照してください。

## <a name="retrieve-context-in-private-channels"></a>プライベート チャネルでコンテキストを取得する

> [!NOTE]
> プライベート チャネルは現在、プライベート開発者プレビューのみです。

コンテンツ ページがプライベート チャネルに読み込まれると、呼び出しから `getContext` 受信したデータは難読化され、チャネルのプライバシーが保護されます。

コンテンツ ページがプライベート チャネルにある場合、次のフィールドが変更されます。

* `team.groupId`: プライベート チャネルの場合は未定義
* `team.internalId`: プライベート チャネルの threadId に設定します
* `team.displayName`: プライベート チャネルの名前に設定します
* `sharepointSite.url`: プライベート チャネルの個別の一意の SharePoint サイトの URL に設定します
* `sharepointSite.path`: プライベート チャネルの個別の一意の SharePoint サイトのパスに設定します
* `sharepointSite.domain`: プライベート チャネルの個別の一意の SharePoint サイト ドメインのドメインに設定します

ページでこれらの値のいずれかを使用する場合、フィールドの `channel.membershipType` 値は `Private` 、ページがプライベート チャネルに読み込まれ、適切に応答できるかどうかを判断する必要があります。

> [!NOTE]
>`teamSiteUrl` 標準チャネルにも適しています。 ページでこれらの値のいずれかを使用する場合、ページが共有チャネルに読み込まれ、適切に応答できるかどうかを判断するには、フィールドの `channelType` 値を にする必要があります `Shared` 。

## <a name="get-context-in-shared-channels"></a>共有チャネルでコンテキストを取得する

コンテンツ UX が共有チャネルに読み込まれる場合は、共有チャネルの変更の呼び出しから `getContext` 受信したデータを使用します。 タブで次のいずれかの値を使用する場合は、フィールドを設定 `channelType` して、タブが共有チャネルに読み込まれているかどうかを判断し、適切に応答する必要があります。
共有チャネルの `groupId` 場合、ホスト チームの groupId は共有チャネルの真のメンバーシップを正確に反映しないため、値は `null`です。 これに対処するために、 プロパティと `hostTenantID` プロパティが新しく追加され、`hostTeamGroupID`メンバーシップを取得するための Microsoft Graph API呼び出しを行う場合に便利です。 `hostTeam` は、共有チャネルを作成したチームを指します。 `currentTeam` は、現在のユーザーが共有チャネルにアクセスしている Team を指します。

これらの概念の詳細については、「 [共有チャネル](~/concepts/build-and-test/shared-channels.md)」を参照してください。

共有チャネルでは、次 `getContext` のプロパティを使用します。

| プロパティ | 説明 |
|----------|--------------|
|`channelId`| プロパティは、共有チャネル スレッド ID に設定されます。|
|`channelType`| プロパティは、共有チャネルに対して に `sharedChannel` 設定されます。|
|`groupId`|プロパティは共有チャネル用です `null` 。|
|`hostTenantId`| プロパティが新しく追加され、ホストのテナント ID が記述され、現在のユーザーの `tid` テナント ID プロパティと比較するのに役立ちます。 |
|`hostTeamGroupId`| プロパティが新しく追加され、ホスト チームの Azure AD グループ ID が記述され、Microsoft Graph API呼び出しを行って共有チャネル メンバーシップを取得するのに役立ちます。 |
|`teamId`|プロパティが新しく追加され、現在の共有チームのスレッド ID に設定されます。 |
|`teamName`|プロパティは、現在の共有チームの `teamName`に設定されます。 |
|`teamType`|プロパティは、現在の共有チームの `teamType`に設定されます。|
|`teamSiteUrl`|プロパティは、共有チャネル `channelSiteUrl`の について説明します。|
|`teamSitePath`| プロパティは、共有チャネル `channelSitePath`の について説明します。|
|`teamSiteDomain`| プロパティは、共有チャネル `channelSiteDomain`の について説明します。|
|`tenantSKU`| プロパティは、ホスト チームの `tenantSKU`について説明します。|
|`tid`|  プロパティは、現在のユーザーのテナント ID を記述します。|
|`userObjectId`|  プロパティは、現在のユーザーの ID を記述します。|
|`userPrincipalName`| プロパティは、現在のユーザーの UPN について説明します。|

共有チャネルの詳細については、「共有 [チャネル」を](~/concepts/build-and-test/shared-channels.md)参照してください。

## <a name="handle-theme-change"></a>テーマの変更を処理する

を呼び出 `microsoftTeams.app.registerOnThemeChangeHandler(function(theme) { /* ... */ })`すことで、テーマが変更された場合に通知されるようにアプリを登録できます。

関数の引数は`theme`、または `contrast`の`default``dark`値を持つ文字列です。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>関連項目

* [タブデザインガイドライン](../../tabs/design/tabs.md)
* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネル] または [グループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [タブでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
