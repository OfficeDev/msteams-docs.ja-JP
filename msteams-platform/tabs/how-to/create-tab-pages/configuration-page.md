---
title: 構成ページを作成する
author: surbhigupta
description: 構成ページの作成方法
keywords: teams タブ グループ チャネル構成可能
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6f79480fb3ec6eb50de622e0b67b70e021d8cce7
ms.sourcegitcommit: a6253e89cb8c8c34d45b06e08c9668daeebc30a3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2021
ms.locfileid: "53300313"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="2c998-104">構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="2c998-104">Create a configuration page</span></span>

<span data-ttu-id="2c998-105">構成ページは、特殊な種類のコンテンツ [ページです](content-page.md)。</span><span class="sxs-lookup"><span data-stu-id="2c998-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="2c998-106">ユーザーは、構成ページを使用して Microsoft Teamsアプリのいくつかの側面を構成し、その構成を次の一部として使用します。</span><span class="sxs-lookup"><span data-stu-id="2c998-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="2c998-107">[チャネルまたはグループ チャット] タブ: ユーザーから情報を収集し、表示するコンテンツ ページ `contentUrl` を設定します。</span><span class="sxs-lookup"><span data-stu-id="2c998-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to be displayed.</span></span>
* <span data-ttu-id="2c998-108">メッセージング [拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="2c998-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="2c998-109">[Office 365[コネクタ]](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="2c998-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configure-a-channel-or-group-chat-tab"></a><span data-ttu-id="2c998-110">チャネルまたはグループ チャット タブを構成する</span><span class="sxs-lookup"><span data-stu-id="2c998-110">Configure a channel or group chat tab</span></span>

<span data-ttu-id="2c998-111">アプリケーションは JavaScript クライアント SDK Microsoft Teams[呼び出す](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)必要があります `microsoft.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="2c998-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="2c998-112">使用する URL は、セキュリティで保護された HTTPS エンドポイントで、クラウドから利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c998-112">The URLs used must be secured HTTPS endpoints and available from the cloud.</span></span>

### <a name="example"></a><span data-ttu-id="2c998-113">例</span><span class="sxs-lookup"><span data-stu-id="2c998-113">Example</span></span>

<span data-ttu-id="2c998-114">構成ページの例を次の図に示します。</span><span class="sxs-lookup"><span data-stu-id="2c998-114">An example of a configuration page is shown in the following image:</span></span>

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="2c998-115">次のコードは、構成ページの対応するコードの例です。</span><span class="sxs-lookup"><span data-stu-id="2c998-115">The following code is an example of corresponding code for the configuration page:</span></span>

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
    ...
</body>
```

<span data-ttu-id="2c998-116">構成ページ **で [灰色の選択\*\*\*\*]** または [赤の選択] ボタンを選択して、タブコンテンツを灰色または赤のアイコンで表示します。</span><span class="sxs-lookup"><span data-stu-id="2c998-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span>

<span data-ttu-id="2c998-117">次の図は、灰色のアイコンでタブ コンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="2c998-117">The following image displays the tab content with a gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="2c998-118">次の図は、赤いアイコンでタブ コンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="2c998-118">The following image displays the tab content with a red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="2c998-119">適切なボタンを選択すると、トリガー `saveGray()` または `saveRed()` トリガーが実行され、次のコマンドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="2c998-119">Choosing the appropriate button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

* <span data-ttu-id="2c998-120">true `settings.setValidityState(true)` に設定します。</span><span class="sxs-lookup"><span data-stu-id="2c998-120">Set `settings.setValidityState(true)` to true.</span></span> 
* <span data-ttu-id="2c998-121">イベント `microsoftTeams.settings.registerOnSaveHandler()` ハンドラーがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="2c998-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
* <span data-ttu-id="2c998-122">**アプリ** の構成ページで保存が有効です。</span><span class="sxs-lookup"><span data-stu-id="2c998-122">**Save** on the app's configuration page, is enabled.</span></span>

<span data-ttu-id="2c998-123">構成ページ コードは、Teams要件が満たされ、インストールを続行できると通知します。</span><span class="sxs-lookup"><span data-stu-id="2c998-123">The configuration page code informs Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="2c998-124">ユーザーが [保存] を **選択** すると、インターフェイスで定義されているパラメーター `settings.setSettings()` が設定 `Settings` されます。</span><span class="sxs-lookup"><span data-stu-id="2c998-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="2c998-125">詳細については、「設定インターフェイス」 [を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="2c998-125">For more information, see [settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="2c998-126">`saveEvent.notifySuccess()` が呼び出され、コンテンツ URL が正常に解決されたことを示します。</span><span class="sxs-lookup"><span data-stu-id="2c998-126">`saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="2c998-127">使用して保存ハンドラーを登録する場合は、コールバックを呼び出す必要があります。または構成の `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` 結果を示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c998-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="2c998-128">保存ハンドラーを登録しない場合、ユーザーが [保存] を選択すると、呼び `saveEvent.notifySuccess()` 出しが自動的に **行われます**。</span><span class="sxs-lookup"><span data-stu-id="2c998-128">If you do not register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="2c998-129">タブ設定のコンテキスト データを取得する</span><span class="sxs-lookup"><span data-stu-id="2c998-129">Get context data for your tab settings</span></span>

<span data-ttu-id="2c998-130">関連するコンテンツを表示するには、コンテキスト情報が必要です。</span><span class="sxs-lookup"><span data-stu-id="2c998-130">Your tab requires contextual information to display relevant content.</span></span> <span data-ttu-id="2c998-131">コンテキスト情報は、よりカスタマイズされたユーザー エクスペリエンスを提供することで、タブの魅力をさらに強化します。</span><span class="sxs-lookup"><span data-stu-id="2c998-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="2c998-132">タブ構成に使用されるプロパティの詳細については、「コンテキスト インターフェイス」 [を参照してください](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="2c998-132">For more information on the properties used for tab configuration, see [context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="2c998-133">次の 2 つの方法でコンテキスト データ変数の値を収集します。</span><span class="sxs-lookup"><span data-stu-id="2c998-133">Collect the values of context data variables in the following two ways:</span></span>

* <span data-ttu-id="2c998-134">マニフェストに URL クエリ文字列プレースホルダーを挿入します `configurationURL` 。</span><span class="sxs-lookup"><span data-stu-id="2c998-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

* <span data-ttu-id="2c998-135">SDK メソッド[Teams使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` します。</span><span class="sxs-lookup"><span data-stu-id="2c998-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="2c998-136">プレースホルダーを `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="2c998-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="2c998-137">コンテキスト インターフェイスのプレースホルダーを基本に追加します `configurationUrl` 。</span><span class="sxs-lookup"><span data-stu-id="2c998-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="2c998-138">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="2c998-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="2c998-139">ベース URL</span><span class="sxs-lookup"><span data-stu-id="2c998-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="2c998-140">クエリ文字列を含む基本 URL</span><span class="sxs-lookup"><span data-stu-id="2c998-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="2c998-141">ページのアップロード後、Teams値を使用してクエリ文字列プレースホルダーを更新します。</span><span class="sxs-lookup"><span data-stu-id="2c998-141">After your page uploads, Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="2c998-142">これらの値を取得して使用するロジックを構成ページに含める。</span><span class="sxs-lookup"><span data-stu-id="2c998-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="2c998-143">URL クエリ文字列の操作の詳細については、「MDN Web Docs の [URLSearchParams」](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) を参照してください。次のコード例では、プロパティから値を抽出する方法を示 `configurationUrl` します。</span><span class="sxs-lookup"><span data-stu-id="2c998-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following code example provides the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="2c998-144">関数を使用 `getContext()` してコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="2c998-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="2c998-145">この `microsoftTeams.getContext((context) => {})` 関数は、呼び出されると [コンテキスト インターフェイス](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) を取得します。</span><span class="sxs-lookup"><span data-stu-id="2c998-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span>

<span data-ttu-id="2c998-146">次のコードでは、この関数を構成ページに追加してコンテキスト値を取得する例を示します。</span><span class="sxs-lookup"><span data-stu-id="2c998-146">The following code provides an example of adding this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="2c998-147">コンテキストと認証</span><span class="sxs-lookup"><span data-stu-id="2c998-147">Context and authentication</span></span>

<span data-ttu-id="2c998-148">ユーザーにアプリの構成を許可する前に認証を行います。</span><span class="sxs-lookup"><span data-stu-id="2c998-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="2c998-149">それ以外の場合、コンテンツに認証プロトコルを持つソースが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="2c998-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="2c998-150">詳細については、「ユーザー認証」[タブでユーザーを認証するMicrosoft Teams参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。コンテキスト情報を使用して、認証要求と承認ページ URL を作成します。</span><span class="sxs-lookup"><span data-stu-id="2c998-150">For more information, see [authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span> <span data-ttu-id="2c998-151">タブ ページで使用されているドメインはすべて、and 配列に一覧表示 `manifest.json` されます `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="2c998-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="2c998-152">タブを変更または削除する</span><span class="sxs-lookup"><span data-stu-id="2c998-152">Modify or remove a tab</span></span>

<span data-ttu-id="2c998-153">ユーザーがチャネルまたはグループ タブを変更、再構成、または名前を変更できるマニフェストのプロパティを `canUpdateConfiguration` `true` に設定します。また、アプリに削除オプション ページを含め、構成でプロパティの値を設定して、タブが削除されるとコンテンツに何が起こるかを `removeUrl` 示  `setSettings()` します。</span><span class="sxs-lookup"><span data-stu-id="2c998-153">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a channel or group tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="2c998-154">ユーザーは個人用タブをアンインストールできますが、変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="2c998-154">The user can uninstall personal tabs but cannot modify them.</span></span> <span data-ttu-id="2c998-155">詳細については、「タブの [削除ページを作成する」を参照してください](~/tabs/how-to/create-tab-pages/removal-page.md)。</span><span class="sxs-lookup"><span data-stu-id="2c998-155">For more information, see [create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="2c998-156">`setSettings()`Microsoft Teams削除ページの構成:</span><span class="sxs-lookup"><span data-stu-id="2c998-156">Microsoft Teams `setSettings()` configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="2c998-157">モバイル クライアント</span><span class="sxs-lookup"><span data-stu-id="2c998-157">Mobile clients</span></span>

<span data-ttu-id="2c998-158">チャネルまたはグループ タブをモバイル クライアントのTeamsする場合は、構成の値が `setSettings()` 必要です `websiteUrl` 。</span><span class="sxs-lookup"><span data-stu-id="2c998-158">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for `websiteUrl`.</span></span> <span data-ttu-id="2c998-159">詳細については、「モバイルでの [タブのガイダンス」を参照してください](~/tabs/design/tabs-mobile.md)。</span><span class="sxs-lookup"><span data-stu-id="2c998-159">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2c998-160">関連項目</span><span class="sxs-lookup"><span data-stu-id="2c998-160">See also</span></span>

* [<span data-ttu-id="2c998-161">Teamsタブ</span><span class="sxs-lookup"><span data-stu-id="2c998-161">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="2c998-162">プライベート タブを作成する</span><span class="sxs-lookup"><span data-stu-id="2c998-162">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* <span data-ttu-id="2c998-163">[[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)</span><span class="sxs-lookup"><span data-stu-id="2c998-163">[Create a channel or group tab](~/tabs/how-to/create-channel-group-tab.md)</span></span>
* [<span data-ttu-id="2c998-164">コンテンツ ページを作成する</span><span class="sxs-lookup"><span data-stu-id="2c998-164">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="2c998-165">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="2c998-165">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a><span data-ttu-id="2c998-166">次の手順</span><span class="sxs-lookup"><span data-stu-id="2c998-166">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2c998-167">タブの削除ページを作成する</span><span class="sxs-lookup"><span data-stu-id="2c998-167">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
