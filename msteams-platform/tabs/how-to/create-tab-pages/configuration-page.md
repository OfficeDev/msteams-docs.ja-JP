---
title: 構成ページを作成する
author: surbhigupta
description: 構成ページの作成方法
keywords: teams タブ グループ チャネル構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 041ef78fcc6e3f5203842e808949e86e8dd3aae4
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069218"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="646ee-104">構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="646ee-104">Create a configuration page</span></span>

<span data-ttu-id="646ee-105">構成ページは、特殊な種類のコンテンツ [ページです](content-page.md)。</span><span class="sxs-lookup"><span data-stu-id="646ee-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="646ee-106">ユーザーは、構成ページを使用して Microsoft Teamsアプリのいくつかの側面を構成し、その構成を次の一部として使用します。</span><span class="sxs-lookup"><span data-stu-id="646ee-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="646ee-107">[チャネルまたはグループ チャット] タブ: ユーザーから情報を収集し、表示するコンテンツ ページ `contentUrl` の設定を行います。</span><span class="sxs-lookup"><span data-stu-id="646ee-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="646ee-108">メッセージング [拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="646ee-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="646ee-109">[Office 365[コネクタ]](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="646ee-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="646ee-110">チャネルまたはグループ チャット タブの構成</span><span class="sxs-lookup"><span data-stu-id="646ee-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="646ee-111">アプリケーションは JavaScript クライアント SDK Microsoft Teams[呼び出す](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)必要があります `microsoft.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="646ee-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="646ee-112">また、使用する URL はセキュリティで保護された HTTPS エンドポイントで、クラウドから利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="646ee-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> 

### <a name="example"></a><span data-ttu-id="646ee-113">例</span><span class="sxs-lookup"><span data-stu-id="646ee-113">Example</span></span>

<span data-ttu-id="646ee-114">構成ページの例を次の図に示します。</span><span class="sxs-lookup"><span data-stu-id="646ee-114">An example of a configuration page is shown in the following image:</span></span> 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="646ee-115">構成ページの対応するコードは、次のセクションに表示されます。</span><span class="sxs-lookup"><span data-stu-id="646ee-115">The corresponding code for configuration page is shown in the following section:</span></span>

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

<span data-ttu-id="646ee-116">構成ページ **で [灰色の選択\*\*\*\*]** または [赤の選択] ボタンを選択して、タブコンテンツを灰色または赤のアイコンで表示します。</span><span class="sxs-lookup"><span data-stu-id="646ee-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> 

<span data-ttu-id="646ee-117">次の図は、灰色のアイコンでタブ コンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="646ee-117">The following image displays the tab content with gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="646ee-118">次の図は、赤いアイコンでタブ コンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="646ee-118">The following image displays the tab content with red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="646ee-119">相対ボタンを選択すると、トリガーまたは `saveGray()` `saveRed()` 、 がトリガーされ、次のコマンドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="646ee-119">Choosing the relative button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="646ee-120">は `settings.setValidityState(true)` true に設定されます。</span><span class="sxs-lookup"><span data-stu-id="646ee-120">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="646ee-121">イベント `microsoftTeams.settings.registerOnSaveHandler()` ハンドラーがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="646ee-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="646ee-122">アプリ **の** 構成ページの [保存] ボタンが有効Teamsされます。</span><span class="sxs-lookup"><span data-stu-id="646ee-122">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="646ee-123">構成ページ コードは、構成Teams満たされ、インストールが続行可能な場合に、ユーザーに通知します。</span><span class="sxs-lookup"><span data-stu-id="646ee-123">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="646ee-124">ユーザーが [保存] を **選択** すると、インターフェイスで定義されているパラメーター `settings.setSettings()` が設定 `Settings` されます。</span><span class="sxs-lookup"><span data-stu-id="646ee-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="646ee-125">詳細については、「設定[インターフェイス」を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="646ee-125">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="646ee-126">最後の手順で、コンテンツ URL が正常に解決されたことを示 `saveEvent.notifySuccess()` すために呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="646ee-126">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="646ee-127">使用して保存ハンドラーを登録する場合は、コールバックを呼び出す必要があります。または構成の `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` 結果を示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="646ee-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="646ee-128">保存ハンドラーを登録しない場合、ユーザーが [保存] を選択すると、呼び `saveEvent.notifySuccess()` 出しが自動的に **行われます**。</span><span class="sxs-lookup"><span data-stu-id="646ee-128">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="646ee-129">タブ設定のコンテキスト データを取得する</span><span class="sxs-lookup"><span data-stu-id="646ee-129">Get context data for your tab settings</span></span>

<span data-ttu-id="646ee-130">お使いのタブでは、関連するコンテンツを表示するためにコンテキスト情報が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="646ee-130">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="646ee-131">コンテキスト情報は、よりカスタマイズされたユーザー エクスペリエンスを提供することで、タブの魅力をさらに強化します。</span><span class="sxs-lookup"><span data-stu-id="646ee-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="646ee-132">タブ構成に使用されるプロパティの詳細については、「Context [interface」を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="646ee-132">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="646ee-133">次の 2 つの方法でコンテキスト データ変数の値を収集します。</span><span class="sxs-lookup"><span data-stu-id="646ee-133">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="646ee-134">マニフェストに URL クエリ文字列プレースホルダーを挿入します `configurationURL` 。</span><span class="sxs-lookup"><span data-stu-id="646ee-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="646ee-135">SDK メソッド[Teams使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` します。</span><span class="sxs-lookup"><span data-stu-id="646ee-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="646ee-136">プレースホルダーを `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="646ee-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="646ee-137">コンテキスト インターフェイスのプレースホルダーを基本に追加します `configurationUrl` 。</span><span class="sxs-lookup"><span data-stu-id="646ee-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="646ee-138">例:</span><span class="sxs-lookup"><span data-stu-id="646ee-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="646ee-139">ベース URL</span><span class="sxs-lookup"><span data-stu-id="646ee-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="646ee-140">クエリ文字列を含む基本 URL</span><span class="sxs-lookup"><span data-stu-id="646ee-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="646ee-141">ページのアップロード後、クエリ文字列Teams適切な値で更新されます。</span><span class="sxs-lookup"><span data-stu-id="646ee-141">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="646ee-142">これらの値を取得して使用するロジックを構成ページに含める。</span><span class="sxs-lookup"><span data-stu-id="646ee-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="646ee-143">URL クエリ文字列の操作の詳細については、「MDN Web Docs の [URLSearchParams」](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) を参照してください。次の例では、プロパティから値を抽出する方法について説明 `configurationUrl` します。</span><span class="sxs-lookup"><span data-stu-id="646ee-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="646ee-144">関数を使用 `getContext()` してコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="646ee-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="646ee-145">この `microsoftTeams.getContext((context) => {})` 関数は、呼び出されると [コンテキスト インターフェイス](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) を取得します。</span><span class="sxs-lookup"><span data-stu-id="646ee-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="646ee-146">この関数を構成ページに追加して、コンテキスト値を取得します。</span><span class="sxs-lookup"><span data-stu-id="646ee-146">Add this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="646ee-147">コンテキストと認証</span><span class="sxs-lookup"><span data-stu-id="646ee-147">Context and authentication</span></span>

 <span data-ttu-id="646ee-148">ユーザーにアプリの構成を許可する前に認証を行います。</span><span class="sxs-lookup"><span data-stu-id="646ee-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="646ee-149">それ以外の場合、コンテンツに認証プロトコルを持つソースが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="646ee-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="646ee-150">詳細については、「[ユーザーの認証][タブでユーザーを認証するMicrosoft Teams参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。コンテキスト情報を使用して、認証要求と承認ページ URL を作成します。</span><span class="sxs-lookup"><span data-stu-id="646ee-150">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="646ee-151">タブ ページで使用されているドメインはすべて、and 配列に一覧表示 `manifest.json` されます `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="646ee-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="646ee-152">タブを変更または削除する</span><span class="sxs-lookup"><span data-stu-id="646ee-152">Modify or remove a tab</span></span>

<span data-ttu-id="646ee-153">サポートされている削除オプションは、ユーザー エクスペリエンスをさらに改善します。</span><span class="sxs-lookup"><span data-stu-id="646ee-153">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="646ee-154">ユーザーがグループまたはチャネル タブを変更、再構成、または名前変更できるマニフェストのプロパティを `canUpdateConfiguration` `true` に設定します。また、アプリに削除オプション ページを含め、構成でプロパティの値を設定して、タブが削除されるとコンテンツに何が起こるかを `removeUrl` 示  `setSettings()` します。</span><span class="sxs-lookup"><span data-stu-id="646ee-154">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="646ee-155">ユーザーは個人用タブをアンインストールできますが、変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="646ee-155">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="646ee-156">詳細については、「タブの [削除ページを作成する」を参照してください](~/tabs/how-to/create-tab-pages/removal-page.md)。</span><span class="sxs-lookup"><span data-stu-id="646ee-156">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="646ee-157">Microsoft Teamsの setSettings() 構成を次に示します。</span><span class="sxs-lookup"><span data-stu-id="646ee-157">Microsoft Teams setSettings() configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="646ee-158">モバイル クライアント</span><span class="sxs-lookup"><span data-stu-id="646ee-158">Mobile clients</span></span>

<span data-ttu-id="646ee-159">チャネルまたはグループ タブをモバイル クライアントのTeamsする場合は、構成の値が `setSettings()` 必要です `websiteUrl` 。</span><span class="sxs-lookup"><span data-stu-id="646ee-159">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for `websiteUrl`.</span></span> <span data-ttu-id="646ee-160">詳細については、「モバイルでの [タブのガイダンス」を参照してください](~/tabs/design/tabs-mobile.md)。</span><span class="sxs-lookup"><span data-stu-id="646ee-160">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>
