---
title: タブのコンテキストを取得する
description: タブにユーザー コンテクストを付与する方法を説明します。
ms.localizationpriority: medium
ms.topic: how-to
keywords: チーム タブ ユーザー コンテキスト
ms.openlocfilehash: 319aea79c38466969f84e1e00d44b127a77ef92f
ms.sourcegitcommit: 929391b6c04d53ea84a93145e2f29d6b96a64d37
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2022
ms.locfileid: "65672921"
---
# <a name="get-context-for-your-tab"></a>タブのコンテキストを取得する

タブには、関連するコンテンツを表示するためのコンテキスト情報が必要です。

* ユーザー、チーム、または会社に関する基本情報。
* ロケールとテーマの情報。
* このタブの `entityId` 内容を識別する情報を `subEntityId` 読み取ります。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="user-context"></a>ユーザー コンテキスト

ユーザー、チーム、または会社に関するコンテキストは、次の場合に特に役立ちます。

* アプリ内のリソースを作成するか、指定したユーザーまたはチームに関連付けます。
* Microsoft Azure Active Directory (Azure AD) またはその他の ID プロバイダーから認証フローを開始すると、ユーザーがユーザー名を再度入力する必要はありません。

詳細については、「[Microsoft Teamsでユーザーを認証する」を参照してください](~/concepts/authentication/authentication.md)。

> [!IMPORTANT]
> このユーザー情報はスムーズなユーザー エクスペリエンスを提供するのに役立ちますが、ID の証明として使用しないでください。  たとえば、攻撃者はブラウザーにページを読み込み、有害な情報や要求をレンダリングできます。

## <a name="access-context-information"></a>コンテキスト情報にアクセスする

コンテキスト情報には 2 つの方法でアクセスできます。

* URL プレースホルダー値を挿入します。
* [Microsoft Teams JavaScript クライアント SDK を使用します](/javascript/api/overview/msteams-client)。

### <a name="get-context-by-inserting-url-placeholder-values"></a>URL プレースホルダー値を挿入してコンテキストを取得する

構成やコンテンツ URL では、プレースホルダーを使用します。 Microsoft Teams では、実際の構成やコンテンツ URL を決定する際に、プレースホルダーを該当する値で置き換えます。 使用可能なプレースホルダーには、 [コンテキスト](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-1.12.1&preserve-view=true) オブジェクト上のすべてのフィールドが含まれます。 一般的なプレースホルダーは次のとおりです。

* {entityId}: 最初の [タブの構成](~/tabs/how-to/create-tab-pages/configuration-page.md) 時に、このタブのアイテムに与えた ID。
* {subEntityId}: このタブ内の特定のアイテムの [ディープ リンク](~/concepts/build-and-test/deep-links.md) を生成するときに指定した ID。これは、エンティティ内の特定の状態に復元するために使用する必要があります。たとえば、特定のコンテンツへのスクロールやアクティブ化などです。
* {loginHint}: Azure AD のログイン ヒントとして適した値。 これは通常、ホーム テナント内の現在のユーザーのログイン名です。
* {userPrincipalName}: 現在のテナント内の現在のユーザーのユーザー プリンシパル名。
* {userObjectId}: 現在のテナント内の現在のユーザーの Azure AD オブジェクト ID。
* {theme}: 現在のユーザー インターフェイス (UI) テーマ (例: `default`、 `dark`、または `contrast`.
* {groupId}: タブが存在するOffice 365 グループの ID。
* {tid}: 現在のユーザーの Azure AD テナント ID。
* {locale}: languageId-countryId(en-us) として書式設定されたユーザーの現在のロケール。

> [!NOTE]
> 以前の `{upn}` プレースホルダーは、現在では非推奨となっています。 後方互換性のため、現在は `{loginHint}` の同義語となっています。

たとえば、タブ マニフェストで属性`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`を`configURL`設定すると、サインインしているユーザーには次の属性があります。

* ユーザー名は **user@example.com**。
* 会社のテナント ID は **e2653c-etc** です。
* id **00209384-etc** を持つOffice 365 グループのメンバーです。
* ユーザーがTeamsテーマを **ダーク** に設定しました。

タブを構成すると、Teamsは次の URL を呼び出します。

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Microsoft Teams JavaScript ライブラリを使用してコンテキストを取得する

また、関数を呼び出して[、Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) を使用して、上記の情報を`app.getContext()`取得することもできます。 詳細については、 [Context インターフェイス](/javascript/api/@microsoft/teams-js/app.context?view=msteams-client-js-latest&preserve-view=true)のプロパティを参照してください。

## <a name="retrieve-context-in-private-channels"></a>プライベート チャネルでコンテキストを取得する

コンテンツ ページがプライベート チャネルに読み込まれると、チャネルのプライバシーを `getContext` 保護するために、通話から受信したデータが難読化されます。

コンテンツ ページがプライベート チャネルにある場合、次のフィールドが変更されます。

* `groupId`: プライベート チャネルの場合は未定義
* `teamId`: プライベート チャネルの threadId に設定します
* `teamName`: プライベート チャネルの名前に設定します
* `teamSiteUrl`: プライベート チャネルの個別の一意のSharePoint サイトの URL に設定します。
* `teamSitePath`: プライベート チャネルの個別の一意のSharePoint サイトのパスに設定します
* `teamSiteDomain`: プライベート チャネルの個別の一意のSharePoint サイト ドメインのドメインに設定します

ページでこれらの値のいずれかを使用する場合、フィールドの `channelType` 値は `Private` 、ページがプライベート チャネルに読み込まれ、適切に応答できるかどうかを判断する必要があります。

## <a name="retrieve-context-in-microsoft-teams-connect-shared-channels"></a>Microsoft Teams Connect共有チャネルでコンテキストを取得する

> [!NOTE]
> 現在、Microsoft Teams Connect共有チャネルは[開発者向けプレビュー](../../resources/dev-preview/developer-preview-intro.md)版のみです。

コンテンツ ページがMicrosoft Teams Connect共有チャネルに読み込まれると、共有チャネル内の一意の`getContext`ユーザー名簿が原因で、通話から受信したデータが変更されます。

コンテンツ ページが共有チャネル内にある場合、次のフィールドが変更されます。

* `groupId`: 共有チャネルの場合は未定義です。
* `teamId`: チームの `threadId` ユーザーに設定すると、チャネルは現在のユーザーに対して共有されます。 ユーザーが複数のチームにアクセスできる場合は、 `teamId` 共有チャネルをホスト (作成) するチームに設定されます。
* `teamName`: チームの名前に設定すると、現在のユーザーのチャネルが共有されます。 ユーザーが複数のチームにアクセスできる場合は、 `teamName` 共有チャネルをホスト (作成) するチームに設定されます。
* `teamSiteUrl`: 共有チャネルの個別の一意のSharePoint サイトの URL に設定します。
* `teamSitePath`: 共有チャネルの個別の一意のSharePoint サイトのパスに設定します。
* `teamSiteDomain`: 共有チャネルの個別の一意のSharePoint サイト ドメインのドメインに設定します。

これらのフィールドの変更に加えて、共有チャネルで使用できる新しいフィールドは 2 つあります。

* `hostTeamGroupId`: ホスティング チームに `groupId` 関連付けられているか、共有チャネルを作成したチームに設定します。 このプロパティを使用すると、Microsoft Graph API呼び出しで共有チャネルのメンバーシップを取得できます。
* `hostTeamTenantId`: ホスティング チームに `tenantId` 関連付けられているか、共有チャネルを作成したチームに設定します。 このプロパティは、現在のユーザーのテナント ID `tid` と相互参照して、ユーザーがホスティング チームの `getContext` テナントの内部か外部かを判断できます。

ページでこれらの値のいずれかを使用する場合、フィールドの `channelType` 値は `Shared` 、ページが共有チャネルに読み込まれ、適切に応答できるかどうかを判断する必要があります。

## <a name="handle-theme-change"></a>テーマの変更を処理する

テーマが変更された場合は、アプリを登録して通知を受け取 `app.registerOnThemeChangeHandler(function(theme) { /* ... */ })`ることができます。

`theme`関数内の引数は、値`default`が 、 、 または `dark``contrast`.

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>関連項目

* [タブデザインのガイドライン](../../tabs/design/tabs.md)
* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネル] または [グループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [タブでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
