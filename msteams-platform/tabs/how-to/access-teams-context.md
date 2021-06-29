---
title: タブのコンテキストを取得する
description: タブにユーザー コンテクストを付与する方法を説明します。
localization_priority: Normal
ms.topic: how-to
keywords: チーム タブ ユーザー コンテキスト
ms.openlocfilehash: 8c91cf5a65f13d9f58f6ae8aa2678266c37338c8
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179728"
---
# <a name="get-context-for-your-tab"></a><span data-ttu-id="51a5b-104">タブのコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="51a5b-104">Get context for your tab</span></span>

<span data-ttu-id="51a5b-105">関連するコンテンツを表示するには、コンテキスト情報が必要です。</span><span class="sxs-lookup"><span data-stu-id="51a5b-105">Your tab requires contextual information to display relevant content:</span></span>

* <span data-ttu-id="51a5b-106">ユーザー、チーム、または会社に関する基本情報。</span><span class="sxs-lookup"><span data-stu-id="51a5b-106">Basic information about the user, team, or company.</span></span>
* <span data-ttu-id="51a5b-107">ロケールとテーマの情報。</span><span class="sxs-lookup"><span data-stu-id="51a5b-107">Locale and theme information.</span></span>
* <span data-ttu-id="51a5b-108">読み `entityId` 取 `subEntityId` り、またはこのタブ内の何を識別します。</span><span class="sxs-lookup"><span data-stu-id="51a5b-108">Read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="51a5b-109">ユーザー コンテキスト</span><span class="sxs-lookup"><span data-stu-id="51a5b-109">User context</span></span>

<span data-ttu-id="51a5b-110">ユーザー、チーム、または会社に関するコンテキストは、次の場合に特に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="51a5b-110">Context about the user, team, or company can be especially useful when:</span></span>

* <span data-ttu-id="51a5b-111">アプリ内のリソースを作成または指定したユーザーまたはチームに関連付ける。</span><span class="sxs-lookup"><span data-stu-id="51a5b-111">You create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="51a5b-112">認証フローは、Azure Active Directory (AAD) または他の ID プロバイダーから開始し、ユーザーがユーザー名を再入力する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="51a5b-112">You initiate an authentication flow from Azure Active Directory (AAD) or other identity provider, and you do not require the user to enter their username again.</span></span> <span data-ttu-id="51a5b-113">詳細については、「ユーザー認証」[タブでユーザーを認証するMicrosoft Teams参照してください](~/concepts/authentication/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="51a5b-113">For more information, see [authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51a5b-114">このユーザー情報は、スムーズなユーザー エクスペリエンスを提供するのに役立ちますが、ID の証明として使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="51a5b-114">Although this user information can help provide a smooth user experience, you must not use it as proof of identity.</span></span> <span data-ttu-id="51a5b-115">たとえば、攻撃者はブラウザーにページを読み込み、有害な情報や要求を表示する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="51a5b-115">For example, an attacker can load your page in a browser and render harmful information or requests.</span></span>

## <a name="access-context-information"></a><span data-ttu-id="51a5b-116">コンテキスト情報にアクセスする</span><span class="sxs-lookup"><span data-stu-id="51a5b-116">Access context information</span></span>

<span data-ttu-id="51a5b-117">コンテキスト情報には 2 つの方法でアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="51a5b-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="51a5b-118">URL プレースホルダーの値を挿入します。</span><span class="sxs-lookup"><span data-stu-id="51a5b-118">Insert URL placeholder values.</span></span>
* <span data-ttu-id="51a5b-119">JavaScript クライアント[SDK Microsoft Teams使用します](/javascript/api/overview/msteams-client)。</span><span class="sxs-lookup"><span data-stu-id="51a5b-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client).</span></span>

### <a name="get-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="51a5b-120">URL プレースホルダー値を挿入してコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="51a5b-120">Get context by inserting URL placeholder values</span></span>

<span data-ttu-id="51a5b-121">構成やコンテンツ URL では、プレースホルダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="51a5b-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="51a5b-122">Microsoft Teams では、実際の構成やコンテンツ URL を決定する際に、プレースホルダーを該当する値で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="51a5b-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL.</span></span> <span data-ttu-id="51a5b-123">使用可能なプレースホルダーには、コンテキスト オブジェクトのすべてのフィールド [が含](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) まれます。</span><span class="sxs-lookup"><span data-stu-id="51a5b-123">The available placeholders include all fields on the [context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) object.</span></span> <span data-ttu-id="51a5b-124">一般的なプレースホルダーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="51a5b-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="51a5b-125">{entityId}: 最初の [タブの構成](~/tabs/how-to/create-tab-pages/configuration-page.md) 時に、このタブのアイテムに与えた ID。</span><span class="sxs-lookup"><span data-stu-id="51a5b-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="51a5b-126">{subEntityId}: このタブ内の特定のアイテムの[](~/concepts/build-and-test/deep-links.md)ディープ リンクを生成するときに指定した ID。これは、エンティティ内の特定の状態に復元するために使用する必要があります。たとえば、特定のコンテンツにスクロールしたり、アクティブ化したりします。</span><span class="sxs-lookup"><span data-stu-id="51a5b-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item within this tab. This must be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="51a5b-127">{loginHint}: AAD のログイン ヒントとして適した値。</span><span class="sxs-lookup"><span data-stu-id="51a5b-127">{loginHint}: A value suitable as a login hint for AAD.</span></span> <span data-ttu-id="51a5b-128">これは通常、ホーム テナントの現在のユーザーのログイン名です。</span><span class="sxs-lookup"><span data-stu-id="51a5b-128">This is usually the login name of the current user in their home tenant.</span></span>
* <span data-ttu-id="51a5b-129">{userPrincipalName}: 現在のテナント内の現在のユーザーのユーザー プリンシパル名。</span><span class="sxs-lookup"><span data-stu-id="51a5b-129">{userPrincipalName}: The User Principal Name of the current user in the current tenant.</span></span>
* <span data-ttu-id="51a5b-130">{userObjectId}: 現在のテナント内の現在のユーザーの AAD オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="51a5b-130">{userObjectId}: The AAD object ID of the current user in the current tenant.</span></span>
* <span data-ttu-id="51a5b-131">{theme}: 現在のユーザー インターフェイス (UI) テーマ (例: `default` `dark` 、 、 または `contrast` )</span><span class="sxs-lookup"><span data-stu-id="51a5b-131">{theme}: The current user interface (UI) theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="51a5b-132">{groupId}: タブがOffice 365グループの ID。</span><span class="sxs-lookup"><span data-stu-id="51a5b-132">{groupId}: The ID of the Office 365 group in which the tab resides.</span></span>
* <span data-ttu-id="51a5b-133">{tid}: 現在のユーザーの AAD テナント ID。</span><span class="sxs-lookup"><span data-stu-id="51a5b-133">{tid}: The AAD tenant ID of the current user.</span></span>
* <span data-ttu-id="51a5b-134">{locale}: languageId-countryId として書式設定されたユーザーの現在のロケール。</span><span class="sxs-lookup"><span data-stu-id="51a5b-134">{locale}: The current locale of the user formatted as languageId-countryId.</span></span> <span data-ttu-id="51a5b-135">たとえば、ja-us。</span><span class="sxs-lookup"><span data-stu-id="51a5b-135">For example, en-us.</span></span>

> [!NOTE]
> <span data-ttu-id="51a5b-136">以前の `{upn}` プレースホルダーは、現在では非推奨となっています。</span><span class="sxs-lookup"><span data-stu-id="51a5b-136">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="51a5b-137">後方互換性のため、現在は `{loginHint}` の同義語となっています。</span><span class="sxs-lookup"><span data-stu-id="51a5b-137">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="51a5b-138">たとえば、タブ マニフェストで属性を設定すると、サインインしているユーザー `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` には次の属性があります。</span><span class="sxs-lookup"><span data-stu-id="51a5b-138">For example, in your tab manifest you set the `configURL` attribute to `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`, the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="51a5b-139">ユーザー名は user@example.com **です**。</span><span class="sxs-lookup"><span data-stu-id="51a5b-139">Their username is **user@example.com**.</span></span>
* <span data-ttu-id="51a5b-140">会社のテナント ID は **e2653c-etc です**。</span><span class="sxs-lookup"><span data-stu-id="51a5b-140">Their company tenant ID is **e2653c-etc**.</span></span>
* <span data-ttu-id="51a5b-141">これらは id **00209384-etc Office 365グループのメンバーです**。</span><span class="sxs-lookup"><span data-stu-id="51a5b-141">They are a member of the Office 365 group with id **00209384-etc**.</span></span>
* <span data-ttu-id="51a5b-142">ユーザーがテーマを暗Teams設定 **しました**。</span><span class="sxs-lookup"><span data-stu-id="51a5b-142">The user has set their Teams theme to **dark**.</span></span>

<span data-ttu-id="51a5b-143">タブを構成すると、次Teams URL が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="51a5b-143">When they configure the tab, Teams calls the following URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="51a5b-144">JavaScript ライブラリを使用してコンテキストMicrosoft Teams取得する</span><span class="sxs-lookup"><span data-stu-id="51a5b-144">Get context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="51a5b-145">[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) を使用して `microsoftTeams.getContext(function(context) { /* ... */ })` を呼び出す方法でも、上記の情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="51a5b-145">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="51a5b-146">次のコードは、コンテキスト変数の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="51a5b-146">The following code provides an example of context variable:</span></span>

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

## <a name="retrieve-context-in-private-channels"></a><span data-ttu-id="51a5b-147">プライベート チャネルでのコンテキストの取得</span><span class="sxs-lookup"><span data-stu-id="51a5b-147">Retrieve context in private channels</span></span>

> [!Note]
> <span data-ttu-id="51a5b-148">プライベート チャネルは、現在、開発者のプライベートなプレビューです。</span><span class="sxs-lookup"><span data-stu-id="51a5b-148">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="51a5b-149">コンテンツ ページがプライベート チャネルに読み込まれると、通話から受け取ったデータは、チャネルのプライバシーを保護するために難読 `getContext` 化されます。</span><span class="sxs-lookup"><span data-stu-id="51a5b-149">When your content page is loaded in a private channel, the data you receive from the `getContext` call is obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="51a5b-150">コンテンツ ページがプライベート チャネルにある場合、次のフィールドが変更されます。</span><span class="sxs-lookup"><span data-stu-id="51a5b-150">The following fields are changed when your content page is in a private channel:</span></span>

* <span data-ttu-id="51a5b-151">`groupId`: プライベート チャネルの場合は未定義</span><span class="sxs-lookup"><span data-stu-id="51a5b-151">`groupId`: Undefined for private channels</span></span>
* <span data-ttu-id="51a5b-152">`teamId`: プライベート チャネルの threadId に設定します。</span><span class="sxs-lookup"><span data-stu-id="51a5b-152">`teamId`: Set to the threadId of the private channel</span></span>
* <span data-ttu-id="51a5b-153">`teamName`: プライベート チャネルの名前に設定する</span><span class="sxs-lookup"><span data-stu-id="51a5b-153">`teamName`: Set to the name of the private channel</span></span>
* <span data-ttu-id="51a5b-154">`teamSiteUrl`: プライベート チャネル用の個別の一意のSharePointサイトの URL に設定します。</span><span class="sxs-lookup"><span data-stu-id="51a5b-154">`teamSiteUrl`: Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="51a5b-155">`teamSitePath`: プライベート チャネル用の個別の一意のSharePointパスに設定します。</span><span class="sxs-lookup"><span data-stu-id="51a5b-155">`teamSitePath`: Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="51a5b-156">`teamSiteDomain`: プライベート チャネル用の個別の一意のSharePointドメインに設定します。</span><span class="sxs-lookup"><span data-stu-id="51a5b-156">`teamSiteDomain`: Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

<span data-ttu-id="51a5b-157">ページでこれらの値を使用する場合は、フィールドをチェックして、ページがプライベート チャネルに読み込まれているかどうかを判断し、適切に `channelType` 対応する必要があります。</span><span class="sxs-lookup"><span data-stu-id="51a5b-157">If your page makes use of any of these values, you must check the `channelType` field to determine if your page is loaded in a private channel and respond appropriately.</span></span>

> [!Note]
> <span data-ttu-id="51a5b-158">`teamSiteUrl` 標準チャネルでも動作します。</span><span class="sxs-lookup"><span data-stu-id="51a5b-158">`teamSiteUrl` also works well for standard channels.</span></span>

## <a name="handle-theme-change"></a><span data-ttu-id="51a5b-159">テーマの変更を処理する</span><span class="sxs-lookup"><span data-stu-id="51a5b-159">Handle theme change</span></span>

<span data-ttu-id="51a5b-160">呼び出してテーマが変更された場合に通知するアプリを登録できます `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` 。</span><span class="sxs-lookup"><span data-stu-id="51a5b-160">You can register your app to be informed if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="51a5b-161">関数 `theme` の引数は、、 、または の値を持つ `default` `dark` 文字列です `contrast` 。</span><span class="sxs-lookup"><span data-stu-id="51a5b-161">The `theme` argument in the function is a string with a value of `default`, `dark`, or `contrast`.</span></span>

## <a name="see-also"></a><span data-ttu-id="51a5b-162">関連項目</span><span class="sxs-lookup"><span data-stu-id="51a5b-162">See also</span></span>

* [<span data-ttu-id="51a5b-163">タブデザインのガイドライン</span><span class="sxs-lookup"><span data-stu-id="51a5b-163">Tab design guidelines</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="51a5b-164">Teamsタブ</span><span class="sxs-lookup"><span data-stu-id="51a5b-164">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="51a5b-165">プライベート タブを作成する</span><span class="sxs-lookup"><span data-stu-id="51a5b-165">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* <span data-ttu-id="51a5b-166">[[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)</span><span class="sxs-lookup"><span data-stu-id="51a5b-166">[Create a channel or group tab](~/tabs/how-to/create-channel-group-tab.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="51a5b-167">次の手順</span><span class="sxs-lookup"><span data-stu-id="51a5b-167">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="51a5b-168">アダプティブ カードを使用してタブをビルドする</span><span class="sxs-lookup"><span data-stu-id="51a5b-168">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)