---
title: タブのコンテキストを取得する
description: タブにユーザーコンテキストを取得する方法について説明します。
keywords: teams タブのユーザーコンテキスト
ms.openlocfilehash: 01919999e38d6b659f014b0f05b76d3f332db9ab
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674634"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a><span data-ttu-id="8ead7-104">Microsoft Teams タブのコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="8ead7-104">Get context for your Microsoft Teams tab</span></span>

<span data-ttu-id="8ead7-105">タブには、関連するコンテンツを表示するためにコンテキスト情報が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="8ead7-105">Your tab might require contextual information to display relevant content.</span></span>

* <span data-ttu-id="8ead7-106">タブに、ユーザー、チーム、または会社に関する基本的な情報が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="8ead7-106">Your tab might need basic information about the user, team, or company.</span></span>
* <span data-ttu-id="8ead7-107">タブにロケールとテーマの情報が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="8ead7-107">Your tab might need locale and theme information.</span></span>
* <span data-ttu-id="8ead7-108">タブでは、 `entityId`またはこのタブ`subEntityId`の内容を識別するかどうかを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ead7-108">Your tab might need to read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="8ead7-109">ユーザーコンテキスト</span><span class="sxs-lookup"><span data-stu-id="8ead7-109">User context</span></span>

<span data-ttu-id="8ead7-110">ユーザー、チーム、または会社に関するコンテキストは、特に</span><span class="sxs-lookup"><span data-stu-id="8ead7-110">Context about the user, team or company can be especially useful when</span></span>

* <span data-ttu-id="8ead7-111">アプリ内のリソースを作成するか、指定したユーザーまたはチームと関連付ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ead7-111">You need to create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="8ead7-112">Azure Active Directory またはその他の id プロバイダーに対して認証フローを開始したいが、ユーザーが再度ユーザー名を入力する必要がない場合。</span><span class="sxs-lookup"><span data-stu-id="8ead7-112">You want to initiate an authentication flow against Azure Active Directory or other identity provider, and you don't want to require the user to enter their username again.</span></span> <span data-ttu-id="8ead7-113">(Microsoft Teams タブ内での認証の詳細については、「 [Microsoft teams タブでユーザーを認証する](~/concepts/authentication/authentication.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="8ead7-113">(For more information on authenticating within your Microsoft Teams tab, see [Authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ead7-114">このユーザー情報はスムーズなユーザー環境を提供するのに役立ちますが、id の証明としては使用*しない*でください。</span><span class="sxs-lookup"><span data-stu-id="8ead7-114">Although this user information can help provide a smooth user experience, you should *not* use it as proof of identity.</span></span> <span data-ttu-id="8ead7-115">たとえば、悪意のあるブラウザーにページを読み込み、必要な情報を提供することができます。</span><span class="sxs-lookup"><span data-stu-id="8ead7-115">For example, an attacker could you load your page in a "bad browser" and provide it with any information they want.</span></span>

## <a name="accessing-context"></a><span data-ttu-id="8ead7-116">コンテキストへのアクセス</span><span class="sxs-lookup"><span data-stu-id="8ead7-116">Accessing context</span></span>

<span data-ttu-id="8ead7-117">コンテキスト情報には、次の2つの方法でアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="8ead7-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="8ead7-118">URL プレースホルダーの値を挿入する</span><span class="sxs-lookup"><span data-stu-id="8ead7-118">Insert URL placeholder values</span></span>
* <span data-ttu-id="8ead7-119">[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)を使用する</span><span class="sxs-lookup"><span data-stu-id="8ead7-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client)</span></span>

### <a name="getting-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="8ead7-120">URL プレースホルダーの値を挿入してコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="8ead7-120">Getting context by inserting URL placeholder values</span></span>

<span data-ttu-id="8ead7-121">構成またはコンテンツの Url にプレースホルダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="8ead7-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="8ead7-122">Microsoft Teams は、移動先の実際の構成またはコンテンツ URL を決定するときに、プレースホルダーを関連する値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8ead7-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL to navigate to.</span></span> <span data-ttu-id="8ead7-123">使用可能なプレースホルダーには、 [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest)オブジェクトのすべてのフィールドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8ead7-123">The available placeholders include all fields on the [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) object.</span></span> <span data-ttu-id="8ead7-124">一般的なプレースホルダーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="8ead7-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="8ead7-125">{entityId}: 最初に[タブを構成](~/tabs/how-to/create-tab-pages/configuration-page.md)するときに、このタブのアイテムに対して指定した ID。</span><span class="sxs-lookup"><span data-stu-id="8ead7-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="8ead7-126">{subEntityId}: このタブ_内_の特定のアイテムに対して[詳細なリンク](~/concepts/build-and-test/deep-links.md)を生成するときに指定した ID。これは、エンティティ内の特定の状態に復元するために使用する必要があります。たとえば、特定のコンテンツをスクロールまたはアクティブ化します。</span><span class="sxs-lookup"><span data-stu-id="8ead7-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item _within_ this tab. This should be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="8ead7-127">{loginHint}: Azure AD のログインヒントとして適切な値。これは通常、ホームテナント内の現在のユーザーのログイン名です。</span><span class="sxs-lookup"><span data-stu-id="8ead7-127">{loginHint}: A value suitable as a login hint for Azure AD.This is usually the login name of the current user, in their home tenant.</span></span>
* <span data-ttu-id="8ead7-128">{userPrincipalName}: 現在のテナント内の現在のユーザーのユーザープリンシパル名。</span><span class="sxs-lookup"><span data-stu-id="8ead7-128">{userPrincipalName}: The User Principal Name of the current user, in the current tenant.</span></span>
* <span data-ttu-id="8ead7-129">{userObjectId}: 現在のテナント内の現在のユーザーの Azure AD オブジェクト ID。</span><span class="sxs-lookup"><span data-stu-id="8ead7-129">{userObjectId}: The Azure AD object ID of the current user, in the current tenant.</span></span>
* <span data-ttu-id="8ead7-130">{theme}:、、などの現在の`default`UI `dark`テーマ`contrast`。</span><span class="sxs-lookup"><span data-stu-id="8ead7-130">{theme}: The current UI theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="8ead7-131">{groupId}: タブが存在する Office 365 グループの ID。</span><span class="sxs-lookup"><span data-stu-id="8ead7-131">{groupId}: The ID of the Office 365 Group in which the tab resides.</span></span>
* <span data-ttu-id="8ead7-132">{tid}: 現在のユーザーの Azure AD テナント ID。</span><span class="sxs-lookup"><span data-stu-id="8ead7-132">{tid}: The Azure AD tenant ID of the current user.</span></span>
* <span data-ttu-id="8ead7-133">{locale}: ユーザーの現在のロケール (languageId) として書式設定されている countryId (例: en-us)。</span><span class="sxs-lookup"><span data-stu-id="8ead7-133">{locale}: The current locale of the user formatted as languageId-countryId (for example, en-us).</span></span>

>[!NOTE]
><span data-ttu-id="8ead7-134">以前`{upn}`のプレースホルダーは廃止されました。</span><span class="sxs-lookup"><span data-stu-id="8ead7-134">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="8ead7-135">下位互換性を維持するために、現在は`{loginHint}`にシノニムがあります。</span><span class="sxs-lookup"><span data-stu-id="8ead7-135">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="8ead7-136">たとえば、タブマニフェストで`configURL`属性をに設定したとします。</span><span class="sxs-lookup"><span data-stu-id="8ead7-136">For example, suppose in your tab manifest you set the `configURL` attribute to</span></span>

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

<span data-ttu-id="8ead7-137">サインインしているユーザーには、次の属性があります。</span><span class="sxs-lookup"><span data-stu-id="8ead7-137">And the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="8ead7-138">ユーザー名は ' user@example.com ' です</span><span class="sxs-lookup"><span data-stu-id="8ead7-138">Their username is 'user@example.com'</span></span>
* <span data-ttu-id="8ead7-139">会社のテナント ID は ' e2653c ' のようになっています。</span><span class="sxs-lookup"><span data-stu-id="8ead7-139">Their company tenant ID is 'e2653c-etc'</span></span>
* <span data-ttu-id="8ead7-140">Id が ' 00209384 ' の Office 365 グループのメンバーである</span><span class="sxs-lookup"><span data-stu-id="8ead7-140">They are a member of the Office 365 group with id '00209384-etc'</span></span>
* <span data-ttu-id="8ead7-141">ユーザーが Teams テーマを ' 暗 ' に設定しました</span><span class="sxs-lookup"><span data-stu-id="8ead7-141">The user has set their Teams theme to 'dark'</span></span>

<span data-ttu-id="8ead7-142">ユーザーがタブを構成すると、Teams は次の URL を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="8ead7-142">When they configure your tab, Teams calls this URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="8ead7-143">Microsoft Teams JavaScript ライブラリを使用してコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="8ead7-143">Getting context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="8ead7-144">また、 [Microsoft Teams の JavaScript クライアント SDK](/javascript/api/overview/msteams-client)を呼び出し`microsoftTeams.getContext(function(context) { /* ... */ })`て、上記の情報を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="8ead7-144">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="8ead7-145">コンテキスト変数は、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="8ead7-145">The context variable will look like the following example.</span></span>

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

## <a name="retrieving-context-in-private-channels"></a><span data-ttu-id="8ead7-146">プライベートチャネルでコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="8ead7-146">Retrieving context in private channels</span></span>

> [!Note]
> <span data-ttu-id="8ead7-147">プライベートチャネルは現在、プライベート開発者向けプレビューにあります。</span><span class="sxs-lookup"><span data-stu-id="8ead7-147">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="8ead7-148">コンテンツページがプライベートチャネルに読み込まれると、 `getContext`呼び出しから受け取ったデータは難読化され、チャネルのプライバシーを保護します。</span><span class="sxs-lookup"><span data-stu-id="8ead7-148">When your content page is loaded in a private channel, the data you receive from the `getContext` call will be obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="8ead7-149">コンテンツページがプライベートチャネルにある場合は、次のフィールドが変更されます。</span><span class="sxs-lookup"><span data-stu-id="8ead7-149">The following fields are changed when your content page is in a private channel.</span></span> <span data-ttu-id="8ead7-150">ページで以下の値のいずれかを使用する場合は、 `channelType`フィールドをチェックして、ページがプライベートチャネルに読み込まれているかどうかを確認し、適切に応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8ead7-150">If your page makes use of any of the values below, you'll need to check the `channelType` field to determine if your page is loaded in a private channel, and respond appropriately.</span></span>

* <span data-ttu-id="8ead7-151">`groupId`-プライベートチャネルの場合は未定義</span><span class="sxs-lookup"><span data-stu-id="8ead7-151">`groupId` - Undefined for private channels</span></span>
* <span data-ttu-id="8ead7-152">`teamId`-プライベートチャネルの threadId に設定します。</span><span class="sxs-lookup"><span data-stu-id="8ead7-152">`teamId` - Set to the threadId of the private channel</span></span>
* <span data-ttu-id="8ead7-153">`teamName`-プライベートチャネルの名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="8ead7-153">`teamName` - Set to the name of the private channel</span></span>
* <span data-ttu-id="8ead7-154">`teamSiteUrl`-プライベートチャネル用の一意の一意の SharePoint サイトの URL に設定します。</span><span class="sxs-lookup"><span data-stu-id="8ead7-154">`teamSiteUrl` - Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="8ead7-155">`teamSitePath`-プライベートチャネルの一意の一意の SharePoint サイトのパスに設定します。</span><span class="sxs-lookup"><span data-stu-id="8ead7-155">`teamSitePath` - Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="8ead7-156">`teamSiteDomain`-プライベートチャネルの一意の一意の SharePoint サイトドメインのドメインに設定します。</span><span class="sxs-lookup"><span data-stu-id="8ead7-156">`teamSiteDomain` - Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

## <a name="theme-change-handling"></a><span data-ttu-id="8ead7-157">テーマ変更の処理</span><span class="sxs-lookup"><span data-stu-id="8ead7-157">Theme change handling</span></span>

<span data-ttu-id="8ead7-158">アプリを登録`microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`して、テーマが変更された場合に通知されるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="8ead7-158">You can register your app to be told if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="8ead7-159">関数`theme`の引数は、 `default` `dark`の値、、または`contrast`の値を持つ文字列になります。</span><span class="sxs-lookup"><span data-stu-id="8ead7-159">The `theme` argument in the function will be a string with a value of `default`, `dark`, or `contrast`.</span></span>