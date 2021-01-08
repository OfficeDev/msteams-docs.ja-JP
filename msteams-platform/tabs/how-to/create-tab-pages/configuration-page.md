---
title: 構成ページを作成する
author: laujan
description: 構成ページを作成する方法
keywords: teams タブ グループ チャネルを構成可能
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: c041c311245bb5bfc5e2655ef8d596b2839fdb70
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731966"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="c86ef-104">構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="c86ef-104">Create a configuration page</span></span>

<span data-ttu-id="c86ef-105">構成ページは、ユーザーが Teams[](content-page.md)アプリの一部の側面を構成できる特別な種類のコンテンツ ページです。</span><span class="sxs-lookup"><span data-stu-id="c86ef-105">A configuration page is a special type of [content page](content-page.md) that allows your users to configure some aspect of your Teams app.</span></span> <span data-ttu-id="c86ef-106">通常、これらは次の一部として使用されます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-106">Typically these are used as part of:</span></span>

* <span data-ttu-id="c86ef-107">チャネルまたはグループ チャット タブ - 構成ページでは、ユーザーから情報を収集し、表示するコンテンツ `contentUrl` ページの設定を行えます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-107">A channel or group chat tab - The configuration page allows you to collect information from your users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="c86ef-108">メッセージング [拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="c86ef-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="c86ef-109">Office [365 コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="c86ef-109">A [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="c86ef-110">チャネルまたはグループ チャット タブの構成</span><span class="sxs-lookup"><span data-stu-id="c86ef-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="c86ef-111">構成ページは、コンテンツ ページのレンダリング方法を通知します。</span><span class="sxs-lookup"><span data-stu-id="c86ef-111">A configuration page informs the content page how it should render.</span></span> <span data-ttu-id="c86ef-112">アプリケーションは、Microsoft Teams JavaScript クライアント SDK と呼 [び出しを](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 参照する必要があります `microsoft.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="c86ef-112">Your application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="c86ef-113">さらに、URL はセキュリティで保護された HTTPS エンドポイントで、クラウドから利用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="c86ef-113">Additionally, your URLs must be secure HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="c86ef-114">構成ページの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="c86ef-114">Below is a configuration page example.</span></span>

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

<span data-ttu-id="c86ef-115">ここでは、ユーザーに [灰色の選択] または[赤の選択] の 2 つのオプション ボタンが表示され、タブのコンテンツが赤または灰色のアイコンで表示されます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-115">Here, the user is presented with two option buttons, **Select Gray** or **Select Red** to display the tab content with either a red or gray icon.</span></span> <span data-ttu-id="c86ef-116">相対ボタンを選択すると、次のイベント `saveGray()` `saveRed()` が発生または起動します。</span><span class="sxs-lookup"><span data-stu-id="c86ef-116">Choosing the relative button fires `saveGray()` or `saveRed()` and invokes the following:</span></span>

1. <span data-ttu-id="c86ef-117">true `settings.setValidityState(true)` に設定されます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-117">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="c86ef-118">イベント `microsoftTeams.settings.registerOnSaveHandler()` ハンドラーがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-118">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="c86ef-119">Teams **に** アップロードされたアプリの構成ページの [保存] ボタンが有効になります。</span><span class="sxs-lookup"><span data-stu-id="c86ef-119">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="c86ef-120">このコードを使用すると、構成要件が満たされ、インストールを続行できると Teams に知らされます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-120">This code lets Teams know that the configuration requirements have been satisfied and the installation can proceed.</span></span> <span data-ttu-id="c86ef-121">[ **保存**] では、現在のインスタンスに対して、インターフェイスによって定義されたパラメーター `settings.setSettings()` `Settings` が設定されます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-121">On **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface, for the current instance.</span></span> <span data-ttu-id="c86ef-122">詳細については、「設定インターフェイス」 [を参照してください](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="c86ef-122">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="c86ef-123">最後に、 `saveEvent.notifySuccess()` コンテンツ URL が正常に解決されたことを示すために呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-123">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="c86ef-124">保存ハンドラーが使用して登録されている場合は、コールバックが呼び出す必要があります。または、構成の `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` 結果を示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="c86ef-124">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="c86ef-125">保存ハンドラーが登録されていない場合、ユーザーが [保存] ボタンを選択するとすぐに呼び出 `saveEvent.notifySuccess()` しが **自動的に行** われます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-125">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the **Save** button.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="c86ef-126">タブ設定のコンテキスト データを取得する</span><span class="sxs-lookup"><span data-stu-id="c86ef-126">Get context data for your tab settings</span></span>

<span data-ttu-id="c86ef-127">タブには、関連するコンテンツを表示するためにコンテキスト情報が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="c86ef-127">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="c86ef-128">コンテキスト情報は、よりカスタマイズされたユーザー エクスペリエンスを提供することで、タブの魅力をさらに高める可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c86ef-128">Contextual information can further enhance your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="c86ef-129">Teams コンテキスト [インターフェイスは](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 、タブ構成に使用できるプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="c86ef-129">The Teams [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) defines the properties that can be used for your tab configuration.</span></span> <span data-ttu-id="c86ef-130">コンテキスト データ変数の値は、次の 2 つの方法で収集できます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-130">You can collect the values of context data variables in two ways:</span></span>

1. <span data-ttu-id="c86ef-131">マニフェストに URL クエリ文字列プレースホルダーを挿入します `configurationURL` 。</span><span class="sxs-lookup"><span data-stu-id="c86ef-131">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="c86ef-132">Teams [SDK メソッドを使用](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{}` します。</span><span class="sxs-lookup"><span data-stu-id="c86ef-132">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{}` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="c86ef-133">プレースホルダーの挿入 `configurationURL`</span><span class="sxs-lookup"><span data-stu-id="c86ef-133">Insert placeholders in the `configurationURL`</span></span>

<span data-ttu-id="c86ef-134">コンテキスト インターフェイスのプレースホルダーをベースに追加できます `configurationUrl` 。</span><span class="sxs-lookup"><span data-stu-id="c86ef-134">Context interface placeholders can be added to your base `configurationUrl`.</span></span> <span data-ttu-id="c86ef-135">例:</span><span class="sxs-lookup"><span data-stu-id="c86ef-135">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="c86ef-136">ベース URL</span><span class="sxs-lookup"><span data-stu-id="c86ef-136">Base Url</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="c86ef-137">クエリ文字列を含むベース URL</span><span class="sxs-lookup"><span data-stu-id="c86ef-137">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="c86ef-138">ページがアップロードされると、クエリ文字列プレースホルダーが Teams によって関連する値で更新されます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-138">After your page has uploaded, the query string placeholders will be updated by Teams with the relevant values.</span></span> <span data-ttu-id="c86ef-139">これらの値を取得して使用するロジックを構成ページに含めることができます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-139">You can include logic in your configuration page to retrieve and use those values.</span></span> <span data-ttu-id="c86ef-140">URL クエリ文字列の操作について詳しくは、MDN Web ドキュメントの [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) をご覧ください。上記のプロパティから値を抽出する方法の例を次に示 `configurationURL` します。</span><span class="sxs-lookup"><span data-stu-id="c86ef-140">For more information on working with URL query strings see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN web docs. Here is an example of how to extract a value from the above `configurationURL` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="c86ef-141">関数を `getContext()` 使用してコンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="c86ef-141">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="c86ef-142">呼び出されると、 `microsoftTeams.getContext((context) => {})` この関数はコンテキスト インターフェイスを [取得します](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="c86ef-142">When invoked, the `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="c86ef-143">この関数を構成ページに追加して、コンテキスト値を取得できます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-143">You can add this function to your configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="c86ef-144">コンテキストと認証</span><span class="sxs-lookup"><span data-stu-id="c86ef-144">Context and Authentication</span></span>

<span data-ttu-id="c86ef-145">ユーザーにアプリの構成を許可する前に認証が必要になる場合や、コンテンツに独自の認証プロトコルを持つソースが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c86ef-145">You might require authentication before allowing a user to configure your app or your content might include sources that have their own authentication protocols.</span></span> <span data-ttu-id="c86ef-146">「Microsoft [Teams タブのコンテキスト情報でユーザー](~/tabs/how-to/authentication/auth-flow-tab.md) を認証する」を参照して、認証要求と承認ページの URL を作成できます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-146">See [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md) Context information can be used to help construct authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="c86ef-147">タブ ページで使用されているドメインすべてが配列に表示されます `manifest.json` `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="c86ef-147">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="c86ef-148">タブを変更または削除する</span><span class="sxs-lookup"><span data-stu-id="c86ef-148">Modify or remove a tab</span></span>

<span data-ttu-id="c86ef-149">サポートされている削除オプションにより、ユーザー エクスペリエンスをさらに調整できます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-149">Supported removal options can further refine the user experience.</span></span> <span data-ttu-id="c86ef-150">ユーザーがグループ/チャネル タブを変更、再構成、または名前変更するには、マニフェストのプロパティを設定 `canUpdateConfiguration` します `true` 。</span><span class="sxs-lookup"><span data-stu-id="c86ef-150">You can enable users to modify, reconfigure, or rename a group/channel tab by setting your manifest's `canUpdateConfiguration` property to `true`.</span></span>  <span data-ttu-id="c86ef-151">さらに、アプリに削除オプション ページを含め、構成でプロパティの値を設定することで、タブが削除された場合のコンテンツの処理 `removeUrl` を指定できます  `setSettings()` (下記を参照)。</span><span class="sxs-lookup"><span data-stu-id="c86ef-151">In addition, you can designate what happens to the content when a tab is removed by including a removal options page in your app and setting a value for the `removeUrl` property in the  `setSettings()` configuration (see below).</span></span> <span data-ttu-id="c86ef-152">[個人用] タブは変更できませんが、ユーザーはアンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="c86ef-152">Personal tabs can't be modified but can be uninstalled by the user.</span></span> <span data-ttu-id="c86ef-153">詳細については、「タブの削除 [ページを作成する」を参照してください](~/tabs/how-to/create-tab-pages/removal-page.md)。</span><span class="sxs-lookup"><span data-stu-id="c86ef-153">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="c86ef-154">モバイル クライアント</span><span class="sxs-lookup"><span data-stu-id="c86ef-154">Mobile clients</span></span>

<span data-ttu-id="c86ef-155">Teams モバイル クライアントに [チャネル/グループ] タブを表示するように選択した場合は、`setSettings()` 構成には `websiteUrl` プロパティの値を設定する必要があります (下記参照)。</span><span class="sxs-lookup"><span data-stu-id="c86ef-155">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span> <span data-ttu-id="c86ef-156">モバイルの [タブに関するガイダンスを参照してください](~/tabs/design/tabs-mobile.md)。</span><span class="sxs-lookup"><span data-stu-id="c86ef-156">See [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

<span data-ttu-id="c86ef-157">削除ページやモバイル クライアント用の Microsoft Teams setSettings() 構成:</span><span class="sxs-lookup"><span data-stu-id="c86ef-157">Microsoft Teams setSettings() configuration for removal page and/or mobile clients:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
