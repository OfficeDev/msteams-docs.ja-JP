---
title: タブのコンテキストを取得する
description: タブにユーザー コンテクストを付与する方法を説明します。
keywords: チーム タブ ユーザー コンテキスト
ms.openlocfilehash: 18c8541e948f206fcdddc3a942325e2f5d6e3e5c
ms.sourcegitcommit: 309823e6911b4e8e307493cbd59880fe69a4dca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2020
ms.locfileid: "49727164"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a>Microsoft Teams タブのコンテキストを取得する

お使いのタブでは、関連するコンテンツを表示するためにコンテキスト情報が必要になる場合があります。

* ユーザー、チーム、会社に関する基本情報が必要な場合もあります。
* ロケール情報やテーマ情報が必要な場合もあります。
* お使いのタブは、このタブの中にあるものを識別する `entityId` または `subEntityId` を読む必要がある場合があります。

## <a name="user-context"></a>ユーザー コンテキスト

ユーザー、チーム、会社に関するコンテクストは、以下のような場合に特に役立ちます。

* アプリ内のリソースを作成したり、指定したユーザーやチームと関連付ける必要がある場合。
* Azure Active Directory やその他の ID プロバイダーに対する認証フローを開始したいが、ユーザーにユーザー名の再入力を要求したくない場合。 (Microsoft Teams タブでの認証に関する詳細については、「[Microsoft Teams タブでユーザーを認証する](~/concepts/authentication/authentication.md)」を参照してください)。

> [!IMPORTANT]
> このユーザー情報は、スムーズなユーザー エクスペリエンスを提供するのに役立ちますが、身分証明書として使用するべきでは *ありません*。 たとえば、攻撃者が “悪いブラウザー” であなたのページをロードし、有害な情報や要求をレンダリングする可能性があります。

## <a name="accessing-context"></a>コンテキストにアクセスする

コンテキスト情報には 2 つの方法でアクセスできます。

* URL プレースホルダー値を挿入する
* [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) を使用する

### <a name="getting-context-by-inserting-url-placeholder-values"></a>URL プレースホルダー値を挿入してコンテキストを取得する

構成やコンテンツ URL では、プレースホルダーを使用します。 Microsoft Teams では、実際の構成やコンテンツ URL を決定する際に、プレースホルダーを該当する値で置き換えます。 使用可能なプレースホルダーには、[コンテキスト](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) オブジェクトのすべてのフィールドが含まれます。 一般的なプレースホルダーは次のとおりです。

* {entityId}: 最初の [タブの構成](~/tabs/how-to/create-tab-pages/configuration-page.md) 時に、このタブのアイテムに与えた ID。
* {subEntityId}: このタブ _内部_ の特定のアイテム向けの [ディープ リンク](~/concepts/build-and-test/deep-links.md) を生成する場合に指定した ID。これは、エンティティ内の特定の状態に復元するために使用します。たとえば、特定のコンテンツにスクロールしたり、アクティブにしたりします。
* {loginHint}: Azure AD へのログインのヒントに適した値。これは通常、ホーム テナントでの現在のユーザーのログイン名。
* {userPrincipalName}: 現在のテナントで、現在のユーザーのユーザー プリンシパル名。
* {userObjectId}: 現在のテナント内の現在のユーザーの Azure AD オブジェクト ID。
* {theme}: `default`、`dark`、`contrast` などの現在の UI テーマ。
* {groupId}: タブが存在する Office 365 グループの ID です。
* {tid}: 現在のユーザーの Azure AD テナント ID。
* {locale}: ユーザーの現在のロケールを languageId-countryId として形式化したもの (例: en-us)。

>[!NOTE]
>以前の `{upn}` プレースホルダーは、現在では非推奨となっています。 後方互換性のため、現在は `{loginHint}` の同義語となっています。

たとえば、タブ マニフェストで `configURL` 属性を設定する場合を仮定

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

また、サインインしたユーザーには以下の属性があります。

* ユーザーネームは ‘user@example.com’。
* 会社のテナント ID は ‘e2653c-etc’。
* これらのユーザーは、ID ‘00209384-etc’ の Office 365 グループのメンバーです。
* ユーザーは Teams のテーマを ‘ダーク’ に設定しています。

タブを構成する場合、Teams はこの URL を呼び出します。

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a>Microsoft Teams のJavaScript ライブラリを使用したコンテキストの取得

[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) を使用して `microsoftTeams.getContext(function(context) { /* ... */ })` を呼び出す方法でも、上記の情報を取得できます。

このコンテキスト変数は、次の例のようになるはずです。

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
    "tenantSKU": "The license type for the current user tenant",
    "userLicenseType": "The license type for the current user",
    "parentMessageId": "The parent message ID from which this task module is launched",
    "ringId": "The current ring ID",
    "appSessionId": "The unique ID for the current session used for correlating telemetry data",
    "isCallingAllowed": "Indicates if calling is allowed for the current logged in user",
    "isPSTNCallingAllowed": "Indicates if PSTN calling is allowed for the current logged in user",
    "meetingId": "The meeting ID used by tab when running in meeting context",
    "defaultOneNoteSectionId": "The OneNote section ID that is linked to the channel"
}
```

## <a name="retrieving-context-in-private-channels"></a>プライベート チャネルでのコンテキストの取得

> [!Note]
> プライベート チャネルは、現在、開発者のプライベートなプレビューです。

プライベート チャネルでコンテンツ ページが読み込まれると、チャネルのプライバシーを保護するために、`getContext` 呼び出しから受信するデータは暗号化されます。 コンテンツ ページがプライベート チャネルにある場合、次のフィールドが変更されます。 以下のいずれかの値を使用している場合は、`channelType` フィールドをチェックして、ページがプライベート チャネルでロードされているか判断し、適切に対応する必要があります。

* `groupId` - プライベート チャンネルでは未定義
* `teamId` - プライベート チャネルの threadId に設定
* `teamName` - プライベート チャネルの名前に設定
* `teamSiteUrl` - プライベート チャネルに固有の SharePoint サイトの URL に設定
* `teamSitePath` - プライベート チャネルに固有の SharePoint サイトの特徴的なパスに設定
* `teamSiteDomain` - プライベート チャネルに固有の SharePoint サイト ドメインの特徴的なドメインに設定

> [!Note]
>  teamSiteUrl は、標準的なチャネルにも有効に機能します。

## <a name="theme-change-handling"></a>テーマ変更時の対応

`microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` の呼び出しにより、テーマが変更された場合に通知されるようにアプリを登録することができます。

関数の `theme` 引数は、`default`、`dark`、`contrast` のいずれかの値を持つ文字列になります。
