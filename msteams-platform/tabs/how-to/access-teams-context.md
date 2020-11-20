---
title: タブのコンテキストを取得する
description: タブにユーザーコンテキストを取得する方法について説明します。
keywords: teams タブのユーザーコンテキスト
ms.openlocfilehash: 8c94c4fd895896186ddda20bfaafd1d6ccdc1e73
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346799"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a>Microsoft Teams タブのコンテキストを取得する

タブには、関連するコンテンツを表示するためにコンテキスト情報が必要な場合があります。

* タブに、ユーザー、チーム、または会社に関する基本的な情報が必要な場合があります。
* タブにロケールとテーマの情報が必要な場合があります。
* タブ `entityId` では、または `subEntityId` このタブの内容を識別するかどうかを確認する必要があります。

## <a name="user-context"></a>ユーザーコンテキスト

ユーザー、チーム、または会社に関するコンテキストは、特に

* アプリ内のリソースを作成するか、指定したユーザーまたはチームと関連付ける必要があります。
* Azure Active Directory またはその他の id プロバイダーに対して認証フローを開始したいが、ユーザーが再度ユーザー名を入力する必要がない場合。 (Microsoft Teams タブ内での認証の詳細については、「 [Microsoft teams タブでユーザーを認証する](~/concepts/authentication/authentication.md)」を参照してください)。

> [!IMPORTANT]
> このユーザー情報はスムーズなユーザー環境を提供するのに役立ちますが、id の証明としては使用 *しない* でください。 たとえば、悪意のあるブラウザーにページを読み込み、必要な情報を提供することができます。

## <a name="accessing-context"></a>コンテキストへのアクセス

コンテキスト情報には、次の2つの方法でアクセスできます。

* URL プレースホルダーの値を挿入する
* [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)を使用する

### <a name="getting-context-by-inserting-url-placeholder-values"></a>URL プレースホルダーの値を挿入してコンテキストを取得する

構成やコンテンツ URL では、プレースホルダーを使用します。 Microsoft Teams は、移動先の実際の構成またはコンテンツ URL を決定するときに、プレースホルダーを関連する値に置き換えます。 使用可能なプレースホルダーには、 [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) オブジェクトのすべてのフィールドが含まれています。 一般的なプレースホルダーは次のとおりです。

* {entityId}: 最初に [タブを構成](~/tabs/how-to/create-tab-pages/configuration-page.md)するときに、このタブのアイテムに対して指定した ID。
* {subEntityId}: このタブ _内_ の特定のアイテムに対して [詳細なリンク](~/concepts/build-and-test/deep-links.md)を生成するときに指定した ID。これは、エンティティ内の特定の状態に復元するために使用する必要があります。たとえば、特定のコンテンツをスクロールまたはアクティブ化します。
* {loginHint}: Azure AD のログインヒントとして適切な値。これは通常、ホームテナント内の現在のユーザーのログイン名です。
* {userPrincipalName}: 現在のテナント内の現在のユーザーのユーザープリンシパル名。
* {userObjectId}: 現在のテナント内の現在のユーザーの Azure AD オブジェクト ID。
* {theme}:、、などの現在の `default` UI `dark` テーマ。 `contrast`
* {groupId}: タブが存在する Office 365 グループの ID。
* {tid}: 現在のユーザーの Azure AD テナント ID。
* {locale}: ユーザーの現在のロケール (languageId) として書式設定されている countryId (例: en-us)。
* {osLocaleInfo}: ユーザーの OS からの詳細なロケール情報 (使用可能な場合)。 は、次のように組み合わせて使用できます。
    * @microsoft/地球儀 NPM パッケージを使用して、アプリがユーザーの OS の日付を尊重し、
    * 時刻の形式の構成。
* {sessionId}: テレメトリデータの関連付けで使用するための、現在の Teams セッションの一意の ID。
* {channelId}: コンテンツが関連付けられているチャネルの Microsoft Teams ID。
* {channelName}: コンテンツが関連付けられているチャネルの名前。
* {chatId}: コンテンツが関連付けられているチャットの Microsoft Teams ID。
* {url}: このタブのコンテンツ URL。
* {websiteUrl}: このタブの Web サイトの URL。
* {favoriteChannelsOnly}: フラグがお気に入りのチャネルのみを選択できるようにします。
* {お気に入りのチームのみ}: フラグがお気に入りのチームのみを選択できるようにします。
* {userTeamRole}: チーム内の現在のユーザーの役割。
* {teamType}: チームの種類。
* {isTeamLocked}: チームのロック状態。
* {isTeamArchived}: チームのアーカイブされた状態。
* {isFullScreen スクリーン}: タブが全画面表示モードであるかどうかを示します。
* {teamSiteUrl}: チームに関連付けられているルート SharePoint サイト。
* {teamSiteDomain}: チームに関連付けられているルート SharePoint サイトのドメイン。
* {teamSitePath}: チームに関連付けられている SharePoint サイトへの相対パス。
* {channelRelativeUrl}: チャネルに関連付けられている SharePoint フォルダーへの相対パスです。
* {tenantSKU}: 現在のユーザーのテナントのライセンスの種類。
* {ringId}: 現在の呼び出し ID。
* {appSessionId}: テレメトリデータの関連付けで使用する、現在のセッションの一意の ID。
* {[標準]: タスクモジュールを使用してユーザーの操作の結果を送信する bot ID を指定します。
* {conversationId}: スレッドの Id。
* {hostClientType}: ホストクライアントの種類。(可能な値は、android、ios、web、デスクトップ、および rigel です。)
* {frameContext}: タブの url が読み込まれるコンテキスト (コンテンツ、タスク、設定、削除、sidePanel)。
* {sharepoint}: これは、SharePoint でホストされている場合にのみ使用できます。
* {会議 Id}: 会議のコンテキストで実行されている場合は、タブで使用されます。
* {userLicenseType}現在のユーザーのライセンスの種類。

>[!NOTE]
>以前の `{upn}` プレースホルダーは廃止されました。 下位互換性を維持するために、現在はにシノニムが `{loginHint}` あります。

たとえば、タブマニフェストで `configURL` 属性をに設定したとします。

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

サインインしているユーザーには、次の属性があります。

* ユーザー名は ' user@example.com ' です
* 会社のテナント ID は ' e2653c ' のようになっています。
* Id が ' 00209384 ' の Office 365 グループのメンバーである
* ユーザーが Teams テーマを ' 暗 ' に設定しました

ユーザーがタブを構成すると、Teams は次の URL を呼び出します。

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a>Microsoft Teams JavaScript ライブラリを使用してコンテキストを取得する

また、 [Microsoft Teams の JavaScript クライアント SDK](/javascript/api/overview/msteams-client) を呼び出して、上記の情報を取得することもでき `microsoftTeams.getContext(function(context) { /* ... */ })` ます。

コンテキスト変数は、次の例のようになります。

```json
{
    "teamId": "The Microsoft Teams ID in the format 19:[id]@thread.skype",
    "teamName": "The name of the current team",
    "channelId": "The channel ID in the format 19:[id]@thread.skype",
    "channelName": "The name of the current channel",
    "chatId": "The chat ID in the in the format 19:[id]@thread.skype",
    "locale": "The current locale of the user formatted as languageId-countryId (for example, en-us)",
    "entityId": "The developer-defined unique ID for the entity this content points to",
    "subEntityId": "The developer-defined unique ID for the sub-entity this content points to",
    "loginHint": "A value suitable as a login hint for Azure AD. This is usually the login name of the current user, in their home tenant",
    "userPrincipalName": "The User Principal Name of the current user, in the current tenant",
    "userObjectId": "The Azure AD object id of the current user, in the current tenant",
    "tid": "The Azure AD tenant ID of the current user",
    "groupId": "Guid identifying the current O365 Group ID",
    "theme": "The current UI theme: default | dark | contrast",
    "isFullScreen": "Indicates whether the tab is in full-screen mode",
    "userLicenseType": "Indicates the user licence type in the given SKU (for example, student or teacher)",
    "tenantSKU": "Indicates the SKU category of the tenant (for example, EDU)",
    "channelType": "microsoftTeams.ChannelType.Private | microsoftTeams.ChannelType.Regular"
}
```

## <a name="retrieving-context-in-private-channels"></a>プライベートチャネルでコンテキストを取得する

> [!Note]
> プライベートチャネルは現在、プライベート開発者向けプレビューにあります。

コンテンツページがプライベートチャネルに読み込まれると、呼び出しから受け取ったデータは `getContext` 難読化され、チャネルのプライバシーを保護します。 コンテンツページがプライベートチャネルにある場合は、次のフィールドが変更されます。 ページで以下の値のいずれかを使用する場合は、フィールドをチェックして、 `channelType` ページがプライベートチャネルに読み込まれているかどうかを確認し、適切に応答する必要があります。

* `groupId` -プライベートチャネルの場合は未定義
* `teamId` -プライベートチャネルの threadId に設定します。
* `teamName` -プライベートチャネルの名前に設定します。
* `teamSiteUrl` -プライベートチャネル用の一意の一意の SharePoint サイトの URL に設定します。
* `teamSitePath` -プライベートチャネルの一意の一意の SharePoint サイトのパスに設定します。
* `teamSiteDomain` -プライベートチャネルの一意の一意の SharePoint サイトドメインのドメインに設定します。

## <a name="theme-change-handling"></a>テーマ変更の処理

アプリを登録して、テーマが変更された場合に通知されるようにすることができ `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` ます。

`theme`関数の引数は、の値、 `default` 、またはの値を持つ文字列になり `dark` `contrast` ます。
