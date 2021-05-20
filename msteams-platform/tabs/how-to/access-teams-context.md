---
title: タブのコンテキストを取得する
description: タブにユーザー コンテクストを付与する方法を説明します。
localization_priority: Normal
ms.topic: how-to
keywords: チーム タブ ユーザー コンテキスト
ms.openlocfilehash: 0d9224a941ae4f6a5ad125c93d5877ec49b6df28
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566867"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a><span data-ttu-id="b9c71-104">Microsoft Teams タブのコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="b9c71-104">Get context for your Microsoft Teams tab</span></span>

<span data-ttu-id="b9c71-105">タブには、関連するコンテンツを表示するためにコンテキスト情報が必要です。</span><span class="sxs-lookup"><span data-stu-id="b9c71-105">Your tab must require contextual information to display relevant content:</span></span>

* <span data-ttu-id="b9c71-106">ユーザー、チーム、または会社に関する基本情報。</span><span class="sxs-lookup"><span data-stu-id="b9c71-106">Basic information about the user, team, or company.</span></span>
* <span data-ttu-id="b9c71-107">ロケールとテーマ情報。</span><span class="sxs-lookup"><span data-stu-id="b9c71-107">Locale and theme information.</span></span>
* <span data-ttu-id="b9c71-108">`entityId` `subEntityId` このタブの内容を示す、または を読んでください。</span><span class="sxs-lookup"><span data-stu-id="b9c71-108">Read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="b9c71-109">ユーザー コンテキスト</span><span class="sxs-lookup"><span data-stu-id="b9c71-109">User context</span></span>

<span data-ttu-id="b9c71-110">ユーザー、チーム、または会社に関するコンテキストは、特に次のような場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="b9c71-110">Context about the user, team or company can be especially useful when:</span></span>

* <span data-ttu-id="b9c71-111">アプリ内のリソースを作成または関連付けるには、指定したユーザーまたはチームを使用します。</span><span class="sxs-lookup"><span data-stu-id="b9c71-111">You create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="b9c71-112">Azure Active Directoryまたは他の ID プロバイダーに対して認証フローを開始し、ユーザーにユーザー名の再入力を要求しない。</span><span class="sxs-lookup"><span data-stu-id="b9c71-112">You initiate an authentication flow against Azure Active Directory or other identity provider, and you don't want to require the user to enter their username again.</span></span> <span data-ttu-id="b9c71-113">[Microsoft Teams] タブでの認証の詳細については[、「Microsoft Teams タブでユーザーを認証する」を](~/concepts/authentication/authentication.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="b9c71-113">For more information on authenticating within your Microsoft Teams tab, see [Authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9c71-114">このユーザー情報は、スムーズなユーザー エクスペリエンスを提供するのに役立ちますが、身分証明書として使用するべきでは *ありません*。</span><span class="sxs-lookup"><span data-stu-id="b9c71-114">Although this user information can help provide a smooth user experience, you should *not* use it as proof of identity.</span></span> <span data-ttu-id="b9c71-115">たとえば、攻撃者が “悪いブラウザー” であなたのページをロードし、有害な情報や要求をレンダリングする可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b9c71-115">For example, an attacker could load your page in a "bad browser" and render harmful information or requests.</span></span>

## <a name="accessing-context"></a><span data-ttu-id="b9c71-116">コンテキストにアクセスする</span><span class="sxs-lookup"><span data-stu-id="b9c71-116">Accessing context</span></span>

<span data-ttu-id="b9c71-117">コンテキスト情報には 2 つの方法でアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="b9c71-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="b9c71-118">URL プレースホルダ値を挿入します。</span><span class="sxs-lookup"><span data-stu-id="b9c71-118">Insert URL placeholder values.</span></span>
* <span data-ttu-id="b9c71-119">Microsoft Teams [JavaScript クライアント SDK](/javascript/api/overview/msteams-client)を使用します。</span><span class="sxs-lookup"><span data-stu-id="b9c71-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client).</span></span>

### <a name="getting-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="b9c71-120">URL プレースホルダー値を挿入してコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="b9c71-120">Getting context by inserting URL placeholder values</span></span>

<span data-ttu-id="b9c71-121">構成やコンテンツ URL では、プレースホルダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="b9c71-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="b9c71-122">Microsoft Teams では、実際の構成やコンテンツ URL を決定する際に、プレースホルダーを該当する値で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b9c71-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL.</span></span> <span data-ttu-id="b9c71-123">使用可能なプレースホルダーには、[コンテキスト](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) オブジェクトのすべてのフィールドが含まれます。</span><span class="sxs-lookup"><span data-stu-id="b9c71-123">The available placeholders include all fields on the [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) object.</span></span> <span data-ttu-id="b9c71-124">一般的なプレースホルダーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b9c71-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="b9c71-125">{entityId}: 最初の [タブの構成](~/tabs/how-to/create-tab-pages/configuration-page.md) 時に、このタブのアイテムに与えた ID。</span><span class="sxs-lookup"><span data-stu-id="b9c71-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="b9c71-126">{subEntityId}: このタブ _内部_ の特定のアイテム向けの [ディープ リンク](~/concepts/build-and-test/deep-links.md) を生成する場合に指定した ID。これは、エンティティ内の特定の状態に復元するために使用します。たとえば、特定のコンテンツにスクロールしたり、アクティブにしたりします。</span><span class="sxs-lookup"><span data-stu-id="b9c71-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item _within_ this tab. This should be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="b9c71-127">{loginHint}: Azure AD へのログインのヒントに適した値。これは通常、ホーム テナントでの現在のユーザーのログイン名。</span><span class="sxs-lookup"><span data-stu-id="b9c71-127">{loginHint}: A value suitable as a login hint for Azure AD.This is usually the login name of the current user, in their home tenant.</span></span>
* <span data-ttu-id="b9c71-128">{userPrincipalName}: 現在のテナントで、現在のユーザーのユーザー プリンシパル名。</span><span class="sxs-lookup"><span data-stu-id="b9c71-128">{userPrincipalName}: The User Principal Name of the current user, in the current tenant.</span></span>
* <span data-ttu-id="b9c71-129">{userObjectId}: 現在のテナント内の現在のユーザーの Azure AD オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="b9c71-129">{userObjectId}: The Azure AD object ID of the current user, in the current tenant.</span></span>
* <span data-ttu-id="b9c71-130">{theme}: `default`、`dark`、`contrast` などの現在の UI テーマ。</span><span class="sxs-lookup"><span data-stu-id="b9c71-130">{theme}: The current UI theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="b9c71-131">{groupId}: タブが存在する Office 365 グループの ID です。</span><span class="sxs-lookup"><span data-stu-id="b9c71-131">{groupId}: The ID of the Office 365 Group in which the tab resides.</span></span>
* <span data-ttu-id="b9c71-132">{tid}: 現在のユーザーの Azure AD テナント ID。</span><span class="sxs-lookup"><span data-stu-id="b9c71-132">{tid}: The Azure AD tenant ID of the current user.</span></span>
* <span data-ttu-id="b9c71-133">{ロケール}: 言語として書式設定されたユーザーの現在のロケールId-国Id。</span><span class="sxs-lookup"><span data-stu-id="b9c71-133">{locale}: The current locale of the user formatted as languageId-countryId.</span></span> <span data-ttu-id="b9c71-134">例えば、en-us。</span><span class="sxs-lookup"><span data-stu-id="b9c71-134">For example, en-us.</span></span>

>[!NOTE]
><span data-ttu-id="b9c71-135">以前の `{upn}` プレースホルダーは、現在では非推奨となっています。</span><span class="sxs-lookup"><span data-stu-id="b9c71-135">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="b9c71-136">後方互換性のため、現在は `{loginHint}` の同義語となっています。</span><span class="sxs-lookup"><span data-stu-id="b9c71-136">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="b9c71-137">たとえば、タブ マニフェストで `configURL` 、属性を に設定するとします `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` 。</span><span class="sxs-lookup"><span data-stu-id="b9c71-137">For example, suppose in your tab manifest you set the `configURL` attribute to `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`, the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="b9c71-138">ユーザー名は 「user@example.com」 です。</span><span class="sxs-lookup"><span data-stu-id="b9c71-138">Their username is 'user@example.com'.</span></span>
* <span data-ttu-id="b9c71-139">彼らの会社のテナントIDは'e2653c-etc'です。</span><span class="sxs-lookup"><span data-stu-id="b9c71-139">Their company tenant ID is 'e2653c-etc'.</span></span>
* <span data-ttu-id="b9c71-140">id '00209384-etc' のOffice 365グループのメンバーです。</span><span class="sxs-lookup"><span data-stu-id="b9c71-140">They are a member of the Office 365 group with id '00209384-etc'.</span></span>
* <span data-ttu-id="b9c71-141">ユーザーはテーマを「暗」にTeams設定しました。</span><span class="sxs-lookup"><span data-stu-id="b9c71-141">The user has set their Teams theme to 'dark'.</span></span>

<span data-ttu-id="b9c71-142">ユーザーがタブを構成すると、Teamsは次の URL を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b9c71-142">When they configure your tab, Teams calls the following URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="b9c71-143">Microsoft Teams のJavaScript ライブラリを使用したコンテキストの取得</span><span class="sxs-lookup"><span data-stu-id="b9c71-143">Getting context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="b9c71-144">[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) を使用して `microsoftTeams.getContext(function(context) { /* ... */ })` を呼び出す方法でも、上記の情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="b9c71-144">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="b9c71-145">コンテキスト変数は、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="b9c71-145">The context variable looks like the following example:</span></span>

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
    "defaultOneNoteSectionId": "The OneNote section ID that is linked to the channel"
}
```

## <a name="retrieving-context-in-private-channels"></a><span data-ttu-id="b9c71-146">プライベート チャネルでのコンテキストの取得</span><span class="sxs-lookup"><span data-stu-id="b9c71-146">Retrieving context in private channels</span></span>

> [!Note]
> <span data-ttu-id="b9c71-147">プライベート チャネルは、現在、開発者のプライベートなプレビューです。</span><span class="sxs-lookup"><span data-stu-id="b9c71-147">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="b9c71-148">プライベート チャネルでコンテンツ ページが読み込まれると、チャネルのプライバシーを保護するために、`getContext` 呼び出しから受信するデータは暗号化されます。</span><span class="sxs-lookup"><span data-stu-id="b9c71-148">When your content page is loaded in a private channel, the data you receive from the `getContext` call will be obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="b9c71-149">コンテンツ ページがプライベート チャネルにある場合、次のフィールドが変更されます。</span><span class="sxs-lookup"><span data-stu-id="b9c71-149">The following fields are changed when your content page is in a private channel.</span></span> <span data-ttu-id="b9c71-150">以下のいずれかの値を使用している場合は、`channelType` フィールドをチェックして、ページがプライベート チャネルでロードされているか判断し、適切に対応する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b9c71-150">If your page makes use of any of the values below, you'll need to check the `channelType` field to determine if your page is loaded in a private channel, and respond appropriately.</span></span>

* <span data-ttu-id="b9c71-151">`groupId`: プライベート チャネルの未定義</span><span class="sxs-lookup"><span data-stu-id="b9c71-151">`groupId`: Undefined for private channels</span></span>
* <span data-ttu-id="b9c71-152">`teamId`: プライベート チャネルのスレッド ID に設定します。</span><span class="sxs-lookup"><span data-stu-id="b9c71-152">`teamId`: Set to the threadId of the private channel</span></span>
* <span data-ttu-id="b9c71-153">`teamName`: プライベート チャネルの名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="b9c71-153">`teamName`: Set to the name of the private channel</span></span>
* <span data-ttu-id="b9c71-154">`teamSiteUrl`: プライベート チャネル用に、個別の一意のSharePoint サイトの URL に設定します。</span><span class="sxs-lookup"><span data-stu-id="b9c71-154">`teamSiteUrl`: Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="b9c71-155">`teamSitePath`: プライベート チャネル用の個別の一意のSharePoint サイトのパスに設定します。</span><span class="sxs-lookup"><span data-stu-id="b9c71-155">`teamSitePath`: Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="b9c71-156">`teamSiteDomain`: プライベート チャネルの個別の一意SharePointサイト ドメインのドメインに設定します。</span><span class="sxs-lookup"><span data-stu-id="b9c71-156">`teamSiteDomain`: Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

> [!Note]
>  <span data-ttu-id="b9c71-157">teamSiteUrl は、標準的なチャネルにも有効に機能します。</span><span class="sxs-lookup"><span data-stu-id="b9c71-157">teamSiteUrl works well for standard channels also.</span></span>

## <a name="theme-change-handling"></a><span data-ttu-id="b9c71-158">テーマ変更時の対応</span><span class="sxs-lookup"><span data-stu-id="b9c71-158">Theme change handling</span></span>

<span data-ttu-id="b9c71-159">`microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` の呼び出しにより、テーマが変更された場合に通知されるようにアプリを登録することができます。</span><span class="sxs-lookup"><span data-stu-id="b9c71-159">You can register your app to be told if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="b9c71-160">関数の `theme` 引数は、`default`、`dark`、`contrast` のいずれかの値を持つ文字列になります。</span><span class="sxs-lookup"><span data-stu-id="b9c71-160">The `theme` argument in the function will be a string with a value of `default`, `dark`, or `contrast`.</span></span>
