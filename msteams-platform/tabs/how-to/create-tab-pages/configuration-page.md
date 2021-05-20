---
title: 構成ページを作成する
author: laujan
description: 構成ページの作成方法
keywords: チーム タブ グループ チャネルの構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: aeab1cf96d1e875db79d9143fefd0e46348f585a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566685"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="3479d-104">構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="3479d-104">Create a configuration page</span></span>

<span data-ttu-id="3479d-105">構成ページは、特殊なタイプの [コンテンツ ページ です](content-page.md)。</span><span class="sxs-lookup"><span data-stu-id="3479d-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="3479d-106">ユーザーは、構成ページを使用してMicrosoft Teamsアプリのいくつかの側面を構成し、その構成を次の一部として使用します。</span><span class="sxs-lookup"><span data-stu-id="3479d-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="3479d-107">チャンネルまたはグループチャットタブ: ユーザーから情報を収集し、 `contentUrl` 表示するコンテンツページの を設定します。</span><span class="sxs-lookup"><span data-stu-id="3479d-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="3479d-108">[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="3479d-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="3479d-109">[Office 365 コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="3479d-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="3479d-110">チャネルまたはグループチャットタブの設定</span><span class="sxs-lookup"><span data-stu-id="3479d-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="3479d-111">アプリケーションは[、JavaScript クライアント SDK Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を参照し、 を呼び出す必要があります `microsoft.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="3479d-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="3479d-112">また、使用する URL は、セキュリティで保護された HTTPS エンドポイントで、クラウドから使用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="3479d-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> 

### <a name="example"></a><span data-ttu-id="3479d-113">例</span><span class="sxs-lookup"><span data-stu-id="3479d-113">Example</span></span>

<span data-ttu-id="3479d-114">構成ページの例を次の図に示します。</span><span class="sxs-lookup"><span data-stu-id="3479d-114">An example of a configuration page is shown in the following image:</span></span> 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="3479d-115">構成ページの対応するコードを次のセクションに示します。</span><span class="sxs-lookup"><span data-stu-id="3479d-115">The corresponding code for configuration page is shown in the following section:</span></span>

```html
<head>
<script src='https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
</head>
    <body>
        <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
        <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
        <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

        <script>
            microsoftTeams.initialize();
            let saveGray = () => {
                microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                    microsoftTeams.settings.setSettings({
                        websiteUrl: "https://yourWebsite.com",
                        contentUrl: "https://yourWebsite.com/gray",
                        entityId: "grayIconTab",
                        suggestedDisplayName: "MyNewTab"
                    });
                    saveEvent.notifySuccess();
                });
            }
            let saveRed = () => {
                microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                    microsoftTeams.settings.setSettings({
                        websiteUrl: "https://yourWebsite.com",
                        contentUrl: "https://yourWebsite.com/red",
                        entityId: "redIconTab",
                        suggestedDisplayName: "MyNewTab"
                    });
                    saveEvent.notifySuccess();
                });
            }

            let gr = document.getElementById("gray").style;
            let rd = document.getElementById("red").style;

            const colorClickGray = () => {
                gr.display = "block";
                rd.display = "none";
                microsoftTeams.settings.setValidityState(true);
                saveGray()
            }

            const colorClickRed = () => {
                rd.display = "block";
                gr.display = "none";
                microsoftTeams.settings.setValidityState(true);
                saveRed();
            }
        </script>
    </body>
...
```

<span data-ttu-id="3479d-116">設定ページで **[グレーを選択** ]または **[赤を選択** ]ボタンを選択して、タブの内容をグレーまたは赤のアイコンで表示します。</span><span class="sxs-lookup"><span data-stu-id="3479d-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> 

<span data-ttu-id="3479d-117">次の図は、タブの内容を灰色のアイコンで表示します。</span><span class="sxs-lookup"><span data-stu-id="3479d-117">The following image displays the tab content with gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="3479d-118">次の図は、タブの内容を赤いアイコンで表示します。</span><span class="sxs-lookup"><span data-stu-id="3479d-118">The following image displays the tab content with red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="3479d-119">相対ボタンを選択すると、 `saveGray()` または `saveRed()` がトリガーされ、次が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="3479d-119">Choosing the relative button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="3479d-120">`settings.setValidityState(true)`は true に設定されます。</span><span class="sxs-lookup"><span data-stu-id="3479d-120">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="3479d-121">`microsoftTeams.settings.registerOnSaveHandler()`イベント ハンドラーがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="3479d-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="3479d-122">Teamsでアップロードされたアプリの構成ページの **[保存]** ボタンが有効になります。</span><span class="sxs-lookup"><span data-stu-id="3479d-122">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="3479d-123">構成ページ・コードは、構成要件が満たされ、インストールを続行できることをTeamsに通知します。</span><span class="sxs-lookup"><span data-stu-id="3479d-123">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="3479d-124">ユーザーが [ **保存**] を選択すると `settings.setSettings()` 、インターフェイスで定義されているとおりに のパラメータが設定されます `Settings` 。</span><span class="sxs-lookup"><span data-stu-id="3479d-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="3479d-125">詳細については[、「設定インターフェイス](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3479d-125">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="3479d-126">最後の手順では、 `saveEvent.notifySuccess()` コンテンツ URL が正常に解決されたことを示すために呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="3479d-126">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="3479d-127">を使用して save ハンドラーを登録する場合 `microsoftTeams.settings.registerOnSaveHandler()` 、コールバックは、構成 `saveEvent.notifySuccess()` の結果を呼び出すか、または `saveEvent.notifyFailure()` その結果を示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="3479d-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="3479d-128">保存ハンドラを登録しない場合、 `saveEvent.notifySuccess()` ユーザーが **[ 保存**] を選択すると、呼び出しが自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="3479d-128">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="3479d-129">タブ設定のコンテキストデータを取得する</span><span class="sxs-lookup"><span data-stu-id="3479d-129">Get context data for your tab settings</span></span>

<span data-ttu-id="3479d-130">お使いのタブでは、関連するコンテンツを表示するためにコンテキスト情報が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="3479d-130">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="3479d-131">コンテキスト情報は、よりカスタマイズされたユーザーエクスペリエンスを提供することで、タブの魅力をさらに高めます。</span><span class="sxs-lookup"><span data-stu-id="3479d-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="3479d-132">タブ構成に使用されるプロパティの詳細については、「コンテキスト [インターフェイス](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3479d-132">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="3479d-133">コンテキスト データ変数の値を次の 2 つの方法で収集します。</span><span class="sxs-lookup"><span data-stu-id="3479d-133">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="3479d-134">URL クエリ文字列プレースホルダーをマニフェストの `configurationURL` .</span><span class="sxs-lookup"><span data-stu-id="3479d-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="3479d-135">Teams [SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)メソッドを使用 `microsoftTeams.getContext((context) =>{})` します。</span><span class="sxs-lookup"><span data-stu-id="3479d-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="3479d-136">プレースホルダを `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="3479d-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="3479d-137">コンテキスト インターフェイスのプレースホルダをベースに追加 `configurationUrl` します。</span><span class="sxs-lookup"><span data-stu-id="3479d-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="3479d-138">例:</span><span class="sxs-lookup"><span data-stu-id="3479d-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="3479d-139">ベース URL</span><span class="sxs-lookup"><span data-stu-id="3479d-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="3479d-140">クエリ文字列を含むベース URL</span><span class="sxs-lookup"><span data-stu-id="3479d-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="3479d-141">ページがアップロードされると、Teamsはクエリ文字列のプレースホルダーを関連する値で更新します。</span><span class="sxs-lookup"><span data-stu-id="3479d-141">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="3479d-142">これらの値を取得して使用するロジックを構成ページに含めます。</span><span class="sxs-lookup"><span data-stu-id="3479d-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="3479d-143">URL クエリ文字列の操作の詳細については、「MDN Web ドキュメントの [URLSearchParams」](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) を参照してください。次の例では、プロパティから値を抽出する方法について説明 `configurationUrl` します。</span><span class="sxs-lookup"><span data-stu-id="3479d-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

```html
<script>
   microsoftTeams.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="3479d-144">関数を使用して `getContext()` コンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="3479d-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="3479d-145">`microsoftTeams.getContext((context) => {})`この関数は、呼び出されたときに[Context インターフェイス](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)を取得します。</span><span class="sxs-lookup"><span data-stu-id="3479d-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="3479d-146">コンテキスト値を取得するには、この関数を設定ページに追加します。</span><span class="sxs-lookup"><span data-stu-id="3479d-146">Add this function to the configuration page to retrieve context values:</span></span>

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script>
    microsoftTeams.getContext((context) =>{
        let userId = document.getElementById('user');
        userId.innerHTML = context.userPrincipalName;
    });
</script>
...
```

## <a name="context-and-authentication"></a><span data-ttu-id="3479d-147">コンテキストと認証</span><span class="sxs-lookup"><span data-stu-id="3479d-147">Context and authentication</span></span>

 <span data-ttu-id="3479d-148">ユーザーがアプリを構成できるようにする前に認証します。</span><span class="sxs-lookup"><span data-stu-id="3479d-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="3479d-149">それ以外の場合、コンテンツには、認証プロトコルを持つソースが含まれる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3479d-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="3479d-150">詳細については[、「Microsoft Teams タブでユーザーを認証する」を](~/tabs/how-to/authentication/auth-flow-tab.md)参照してください。コンテキスト情報を使用して、認証要求と承認ページ URL を作成します。</span><span class="sxs-lookup"><span data-stu-id="3479d-150">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="3479d-151">タブページで使用されているすべてのドメインが、 配列にリストされていることを確認します `manifest.json` `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="3479d-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="3479d-152">タブを変更または削除する</span><span class="sxs-lookup"><span data-stu-id="3479d-152">Modify or remove a tab</span></span>

<span data-ttu-id="3479d-153">サポートされている削除オプションは、ユーザー エクスペリエンスをさらに絞り込みます。</span><span class="sxs-lookup"><span data-stu-id="3479d-153">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="3479d-154">ユーザー `canUpdateConfiguration` `true` がグループまたはチャネル タブを変更、再構成、または名前変更できるように、マニフェストのプロパティを に設定します。また、アプリに削除オプション ページを含め、構成でプロパティの値を設定することで、タブが削除されたときにコンテンツに何が起こるか `removeUrl` を示  `setSettings()` します。</span><span class="sxs-lookup"><span data-stu-id="3479d-154">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="3479d-155">ユーザーは [個人] タブをアンインストールできますが、変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="3479d-155">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="3479d-156">詳細については、「 [タブの削除ページを作成する](~/tabs/how-to/create-tab-pages/removal-page.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3479d-156">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="3479d-157">Microsoft Teams削除ページの設定設定() 設定:</span><span class="sxs-lookup"><span data-stu-id="3479d-157">Microsoft Teams setSettings() configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="3479d-158">モバイル クライアント</span><span class="sxs-lookup"><span data-stu-id="3479d-158">Mobile clients</span></span>

<span data-ttu-id="3479d-159">Teamsモバイル クライアントにチャンネルまたはグループ タブを表示する場合、 `setSettings()` 設定にはプロパティの値が必要 `websiteUrl` です。</span><span class="sxs-lookup"><span data-stu-id="3479d-159">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span> <span data-ttu-id="3479d-160">詳細については、 [モバイルのタブのガイダンスを](~/tabs/design/tabs-mobile.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="3479d-160">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>
