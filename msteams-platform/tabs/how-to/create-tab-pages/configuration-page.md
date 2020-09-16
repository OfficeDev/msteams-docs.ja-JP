---
title: 構成ページを作成する
author: laujan
description: 構成ページを作成する方法
keywords: 構成可能な teams タブグループチャネル
ms.topic: conceptualF
ms.author: lajanuar
ms.openlocfilehash: 6288fc8c296ebf0aa85ffe8e08234e5faf22a1ef
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819026"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="2ca17-104">構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="2ca17-104">Create a configuration page</span></span>

<span data-ttu-id="2ca17-105">構成ページは、ユーザーが Teams アプリのいくつかの側面を構成できる特別な種類の [コンテンツページ](content-page.md) です。</span><span class="sxs-lookup"><span data-stu-id="2ca17-105">A configuration page is a special type of [content page](content-page.md) that allows your users to configure some aspect of your Teams app.</span></span> <span data-ttu-id="2ca17-106">通常は、次の一部として使用されます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-106">Typically these are used as part of:</span></span>

* <span data-ttu-id="2ca17-107">[チャネルまたはグループチャット] タブ-[構成] ページでは、ユーザーから情報を収集し、 `contentUrl` 表示するコンテンツページのを設定できます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-107">A channel or group chat tab - The configuration page allows you to collect information from your users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="2ca17-108">[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="2ca17-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="2ca17-109">[Office 365 コネクタ](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="2ca17-109">A [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="2ca17-110">チャネルまたはグループの [チャット] タブの構成</span><span class="sxs-lookup"><span data-stu-id="2ca17-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="2ca17-111">構成ページがコンテンツページに表示される方法を通知します。</span><span class="sxs-lookup"><span data-stu-id="2ca17-111">A configuration page informs the content page how it should render.</span></span> <span data-ttu-id="2ca17-112">アプリケーションは、 [Microsoft Teams の JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) および呼び出しを参照する必要があり `microsoft.initialize()` ます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-112">Your application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="2ca17-113">さらに、Url は、セキュリティで保護された HTTPS エンドポイントであり、クラウドから入手可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ca17-113">Additionally, your URLs must be secure HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="2ca17-114">構成ページの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="2ca17-114">Below is a configuration page example.</span></span>

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

<span data-ttu-id="2ca17-115">ここでは、ユーザーに2つのオプションボタンを表示し、[ **灰色** ] または **[赤** ] を選択してタブのコンテンツを赤または灰色のアイコンで表示します。</span><span class="sxs-lookup"><span data-stu-id="2ca17-115">Here, the user is presented with two option buttons, **Select Gray** or **Select Red** to display the tab content with either a red or gray icon.</span></span> <span data-ttu-id="2ca17-116">[相対] ボタンを選択する `saveGray()` `saveRed()` と、次のように起動されます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-116">Choosing the relative button fires `saveGray()` or `saveRed()` and invokes the following:</span></span>

1. <span data-ttu-id="2ca17-117">`settings.setValidityState(true)`は true に設定されています。</span><span class="sxs-lookup"><span data-stu-id="2ca17-117">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="2ca17-118">`microsoftTeams.settings.registerOnSaveHandler()`イベントハンドラーがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-118">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="2ca17-119">アプリの [構成] ページの [ **保存** ] ボタン (Teams にアップロードされたもの) は有効になっています。</span><span class="sxs-lookup"><span data-stu-id="2ca17-119">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="2ca17-120">このコードを使用すると、構成の要件が満たされており、インストールを続行できることがわかります。</span><span class="sxs-lookup"><span data-stu-id="2ca17-120">This code lets Teams know that the configuration requirements have been satisfied and the installation can proceed.</span></span> <span data-ttu-id="2ca17-121">**Save**では、のパラメーターは、 `settings.setSettings()` インターフェイスの定義に従って、現在のインスタンスに対して設定され `Settings` ます (「 [Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) 」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="2ca17-121">On **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface, for the current instance (See [Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ).</span></span> <span data-ttu-id="2ca17-122">最後に、 `saveEvent.notifySuccess()` は、コンテンツ URL が正常に解決されたことを示すためにを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="2ca17-122">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="2ca17-123">を使用して保存ハンドラーを登録した場合 `microsoftTeams.settings.registerOnSaveHandler()` は、コールバックが起動する `saveEvent.notifySuccess()` か、 `saveEvent.notifyFailure()` 構成の結果を示す必要があります。</span><span class="sxs-lookup"><span data-stu-id="2ca17-123">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="2ca17-124">保存ハンドラーが登録されていない場合は、 `saveEvent.notifySuccess()` ユーザーが [ **保存** ] ボタンを選択すると、その時点で通話が自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-124">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the **Save** button.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="2ca17-125">タブ設定のコンテキストデータを取得する</span><span class="sxs-lookup"><span data-stu-id="2ca17-125">Get context data for your tab settings</span></span>

<span data-ttu-id="2ca17-126">タブには、関連するコンテンツを表示するためにコンテキスト情報が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="2ca17-126">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="2ca17-127">コンテキスト情報を使用すると、よりカスタマイズされたユーザー環境を提供することにより、タブの外観をさらに向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-127">Contextual information can further enhance your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="2ca17-128">Teams [コンテキストインターフェイス](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) は、タブの構成に使用できるプロパティを定義します。</span><span class="sxs-lookup"><span data-stu-id="2ca17-128">The Teams [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) defines the properties that can be used for your tab configuration.</span></span> <span data-ttu-id="2ca17-129">コンテキストデータ変数の値は、次の2つの方法で収集できます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-129">You can collect the values of context data variables in two ways:</span></span>

1. <span data-ttu-id="2ca17-130">マニフェスト内に URL クエリ文字列プレースホルダーを挿入 `configurationURL` します。</span><span class="sxs-lookup"><span data-stu-id="2ca17-130">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="2ca17-131">[TEAMS SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest)メソッドを使用し `microsoftTeams.getContext((context) =>{}` ます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-131">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="2ca17-132">にプレースホルダーを挿入します。 `configurationURL`</span><span class="sxs-lookup"><span data-stu-id="2ca17-132">Insert placeholders in the `configurationURL`</span></span>

<span data-ttu-id="2ca17-133">コンテキストインターフェイスプレースホルダーは、ベースに追加でき `configurationUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-133">Context interface placeholders can be added to your base `configurationUrl`.</span></span> <span data-ttu-id="2ca17-134">以下に例を示します。</span><span class="sxs-lookup"><span data-stu-id="2ca17-134">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="2ca17-135">ベース Url</span><span class="sxs-lookup"><span data-stu-id="2ca17-135">Base Url</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="2ca17-136">クエリ文字列を含むベース URL</span><span class="sxs-lookup"><span data-stu-id="2ca17-136">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="2ca17-137">ページがアップロードされると、クエリ文字列のプレースホルダーが関連する値で Teams によって更新されます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-137">After your page has uploaded, the query string placeholders will be updated by Teams with the relevant values.</span></span> <span data-ttu-id="2ca17-138">構成ページにロジックを含めて、それらの値を取得して使用することができます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-138">You can include logic in your configuration page to retrieve and use those values.</span></span> <span data-ttu-id="2ca17-139">URL クエリ文字列の処理の詳細については、「MDN web ドキュメント」の「 [Urlsearchparams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) 」を参照してください。上記のプロパティから値を抽出する方法の例を次に示し `configurationURL` ます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-139">For more information on working with URL query strings see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN web docs. Here is an example of how to extract a value from the above `configurationURL` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="2ca17-140">関数を使用して `getContext()` コンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="2ca17-140">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="2ca17-141">呼び出されると、 `microsoftTeams.getContext((context) => {})` 関数は [コンテキストインターフェイス](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest)を取得します。</span><span class="sxs-lookup"><span data-stu-id="2ca17-141">When invoked, the `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest).</span></span> <span data-ttu-id="2ca17-142">この関数を構成ページに追加して、コンテキストの値を取得できます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-142">You can add this function to your configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="2ca17-143">コンテキストと認証</span><span class="sxs-lookup"><span data-stu-id="2ca17-143">Context and Authentication</span></span>

<span data-ttu-id="2ca17-144">ユーザーにアプリの構成を許可する前に認証が必要な場合や、独自の認証プロトコルを使用するソースがコンテンツに含まれている場合があります。</span><span class="sxs-lookup"><span data-stu-id="2ca17-144">You might require authentication before allowing a user to configure your app or your content might include sources that have their own authentication protocols.</span></span> <span data-ttu-id="2ca17-145">「 [Microsoft Teams でユーザーを認証する」タブ](~/tabs/how-to/authentication/auth-flow-tab.md) コンテキスト情報は、認証要求および承認ページの url を構築するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-145">See [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md) Context information can be used to help construct authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="2ca17-146">タブページで使用されているすべてのドメインが配列に含まれていることを確認してください `manifest.json` `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="2ca17-146">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="2ca17-147">タブを変更または削除する</span><span class="sxs-lookup"><span data-stu-id="2ca17-147">Modify or remove a tab</span></span>

<span data-ttu-id="2ca17-148">サポートされている削除オプションでは、ユーザーの作業をさらに絞り込むことができます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-148">Supported removal options can further refine the user experience.</span></span> <span data-ttu-id="2ca17-149">ユーザーがマニフェストのプロパティをに設定して、グループ/チャネルタブの変更、再構成、または名前の変更を行うことができるようになり `canUpdateConfiguration` `true` ます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-149">You can enable users to modify, reconfigure, or rename a group/channel tab by setting your manifest's `canUpdateConfiguration` property to `true`.</span></span>  <span data-ttu-id="2ca17-150">また、アプリに [削除オプション] ページを含め、構成内のプロパティの値を設定することによって、タブが削除されたときにコンテンツに何が起こるかを指定でき `removeUrl`  `setSettings()` ます (以下を参照)。</span><span class="sxs-lookup"><span data-stu-id="2ca17-150">In addition, you can designate what happens to the content when a tab is removed by including a removal options page in your app and setting a value for the `removeUrl` property in the  `setSettings()` configuration (see below).</span></span> <span data-ttu-id="2ca17-151">個人用タブは変更できませんが、ユーザーがアンインストールすることはできます。</span><span class="sxs-lookup"><span data-stu-id="2ca17-151">Personal tabs can't be modified but can be uninstalled by the user.</span></span> <span data-ttu-id="2ca17-152">詳細については、「 [タブの削除ページを作成する](~/tabs/how-to/create-tab-pages/removal-page.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2ca17-152">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="2ca17-153">モバイル クライアント</span><span class="sxs-lookup"><span data-stu-id="2ca17-153">Mobile clients</span></span>

<span data-ttu-id="2ca17-154">Teams モバイル クライアントに [チャネル/グループ] タブを表示するように選択した場合は、`setSettings()` 構成には `websiteUrl` プロパティの値を設定する必要があります (下記参照)。</span><span class="sxs-lookup"><span data-stu-id="2ca17-154">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span> <span data-ttu-id="2ca17-155">モバイル クライアントでのタブの完全なサポートは、間もなくリリースされる予定です。</span><span class="sxs-lookup"><span data-stu-id="2ca17-155">Full support for tabs on mobile clients will be released soon.</span></span> <span data-ttu-id="2ca17-156">更新プログラムの準備を行うには、タブの作成時に、[モバイルでのタブのガイダンス](~/tabs/design/tabs-mobile.md)に従ってください。</span><span class="sxs-lookup"><span data-stu-id="2ca17-156">To prepare for the update, you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span>

<span data-ttu-id="2ca17-157">削除ページまたはモバイルクライアントの Microsoft Teams setSettings () 構成:</span><span class="sxs-lookup"><span data-stu-id="2ca17-157">Microsoft Teams setSettings() configuration for removal page and/or mobile clients:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
