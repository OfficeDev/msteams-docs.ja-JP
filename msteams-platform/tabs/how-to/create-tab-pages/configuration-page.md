---
title: 構成ページを作成する
author: laujan
description: 構成ページを作成する方法
keywords: teams タブ グループ チャネルを構成可能
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2544454fd06348fa41269f3a8fd57cc71a07d140
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886738"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="ff9ab-104">構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="ff9ab-104">Create a configuration page</span></span>

<span data-ttu-id="ff9ab-105">構成ページは、特別な種類の [コンテンツ ページです](content-page.md)。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="ff9ab-106">ユーザーは、構成ページを使用して Microsoft Teams アプリのいくつかの側面を構成し、次の一部としてその構成を使用します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="ff9ab-107">チャネルまたはグループ チャット タブ - ユーザーから情報を収集し、表示するコンテンツ `contentUrl` ページの設定を行います。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-107">A channel or group chat tab - Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="ff9ab-108">メッセージング [拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="ff9ab-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="ff9ab-109">Office [365 コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="ff9ab-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="ff9ab-110">チャネルまたはグループ チャット タブの構成</span><span class="sxs-lookup"><span data-stu-id="ff9ab-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="ff9ab-111">アプリケーションは [、Microsoft Teams JavaScript クライアント SDK と呼び出しを](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 参照する必要があります `microsoft.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="ff9ab-112">また、使用する URL はセキュリティで保護された HTTPS エンドポイントで、クラウドから利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="ff9ab-113">次のコードは、構成ページの例です。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-113">The following code is an example of a configuration page:</span></span>

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

<span data-ttu-id="ff9ab-114">構成ページで **[灰色の選択]** または [ **赤** の選択] ボタンを選択して、タブのコンテンツを灰色または赤のアイコンで表示します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-114">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> <span data-ttu-id="ff9ab-115">相対ボタンを選択すると、次のどちらか `saveGray()` または `saveRed()` 実行され、次のコマンドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-115">Choosing the relative button fires either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="ff9ab-116">true `settings.setValidityState(true)` に設定されます。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-116">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="ff9ab-117">イベント `microsoftTeams.settings.registerOnSaveHandler()` ハンドラーがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-117">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="ff9ab-118">Teams **に** アップロードされたアプリの構成ページの [保存] ボタンが有効になります。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-118">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="ff9ab-119">構成ページのコードは、構成要件が満たされ、インストールを続行できると Teams に通知します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-119">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="ff9ab-120">ユーザーが [保存 **]** を選択すると、インターフェイスで定義されているパラメーター `settings.setSettings()` が設定 `Settings` されます。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-120">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="ff9ab-121">詳細については、「設定インターフェイス」 [を参照してください](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-121">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="ff9ab-122">最後の手順では `saveEvent.notifySuccess()` 、コンテンツ URL が正常に解決されたことを示すために呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-122">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="ff9ab-123">保存ハンドラーを使用して登録する場合は、コールバックが呼び出す必要があります。また、構成の `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` 結果を示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-123">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="ff9ab-124">保存ハンドラーを登録しない場合、ユーザーが [保存] を選択すると、呼び出 `saveEvent.notifySuccess()` しが自動的に行 **われます**。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-124">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="ff9ab-125">タブ設定のコンテキスト データを取得する</span><span class="sxs-lookup"><span data-stu-id="ff9ab-125">Get context data for your tab settings</span></span>

<span data-ttu-id="ff9ab-126">タブには、関連するコンテンツを表示するためにコンテキスト情報が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-126">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="ff9ab-127">コンテキスト情報は、よりカスタマイズされたユーザー エクスペリエンスを提供することで、タブの魅力をさらに高めるものになります。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-127">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="ff9ab-128">タブ構成に使用されるプロパティの詳細については、「コンテキスト インターフェイス」を [参照してください](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-128">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="ff9ab-129">コンテキスト データ変数の値は、次の 2 つの方法で収集します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-129">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="ff9ab-130">マニフェストに URL クエリ文字列プレースホルダーを挿入します `configurationURL` 。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-130">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="ff9ab-131">Teams [SDK メソッドを使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-131">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="ff9ab-132">プレースホルダーの挿入 `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="ff9ab-132">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="ff9ab-133">コンテキスト インターフェイスプレースホルダーをベースに追加します `configurationUrl` 。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-133">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="ff9ab-134">以下に例を示します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-134">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="ff9ab-135">ベース URL</span><span class="sxs-lookup"><span data-stu-id="ff9ab-135">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="ff9ab-136">クエリ文字列を含むベース URL</span><span class="sxs-lookup"><span data-stu-id="ff9ab-136">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="ff9ab-137">ページのアップロード後、Teams はクエリ文字列プレースホルダーを関連する値で更新します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-137">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="ff9ab-138">これらの値を取得して使用するロジックを構成ページに含める。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-138">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="ff9ab-139">URL クエリ文字列の操作について詳しくは、MDN Web Docs の [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) に関するページをご覧ください。次の例では、プロパティから値を抽出する方法について説明 `configurationUrl` します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-139">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="ff9ab-140">関数を `getContext()` 使用してコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="ff9ab-140">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="ff9ab-141">この `microsoftTeams.getContext((context) => {})` 関数は、呼び出されると [コンテキスト インターフェイス](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) を取得します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-141">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="ff9ab-142">この関数を構成ページに追加して、コンテキスト値を取得します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-142">Add this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="ff9ab-143">コンテキストと認証</span><span class="sxs-lookup"><span data-stu-id="ff9ab-143">Context and authentication</span></span>

 <span data-ttu-id="ff9ab-144">ユーザーにアプリの構成を許可する前に認証を行います。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-144">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="ff9ab-145">そうしないと、コンテンツに認証プロトコルを持つソースが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-145">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="ff9ab-146">詳細については [、「Microsoft Teams タブでユーザーを認証する」を参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。コンテキスト情報を使用して、認証要求と承認ページの URL を作成します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-146">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="ff9ab-147">タブ ページで使用されているドメインすべてが、配列と一覧に表示 `manifest.json` されます `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-147">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="ff9ab-148">タブを変更または削除する</span><span class="sxs-lookup"><span data-stu-id="ff9ab-148">Modify or remove a tab</span></span>

<span data-ttu-id="ff9ab-149">サポートされている削除オプションは、ユーザー エクスペリエンスをさらに改良します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-149">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="ff9ab-150">ユーザーがグループまたはチャネル タブを変更、再構成、または名前変更できるマニフェストのプロパティを `canUpdateConfiguration` `true` 設定します。また、アプリに削除オプション ページを含め、構成内のプロパティの値を設定することで、タブが削除されるとコンテンツに何が起こるかを `removeUrl` 示  `setSettings()` します。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-150">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="ff9ab-151">詳細については、「モバイル クライアント」 [を参照してください](#mobile-clients)。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-151">For more information, see [Mobile clients](#mobile-clients).</span></span> <span data-ttu-id="ff9ab-152">ユーザーは [個人用] タブをアンインストールできますが、変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-152">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="ff9ab-153">詳細については、「タブの削除 [ページを作成する」を参照してください](~/tabs/how-to/create-tab-pages/removal-page.md)。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-153">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="ff9ab-154">モバイル クライアント</span><span class="sxs-lookup"><span data-stu-id="ff9ab-154">Mobile clients</span></span>

<span data-ttu-id="ff9ab-155">Teams モバイル クライアントにチャネルまたはグループ タブを表示する場合、構成にはプロパティの値 `setSettings()` が必要 `websiteUrl` です。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-155">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span> <span data-ttu-id="ff9ab-156">詳細については、モバイルの [タブに関するガイダンスを参照してください](~/tabs/design/tabs-mobile.md)。</span><span class="sxs-lookup"><span data-stu-id="ff9ab-156">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

<span data-ttu-id="ff9ab-157">削除ページまたはモバイル クライアント用の Microsoft Teams setSettings() 構成:</span><span class="sxs-lookup"><span data-stu-id="ff9ab-157">Microsoft Teams setSettings() configuration for removal page or mobile clients:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
