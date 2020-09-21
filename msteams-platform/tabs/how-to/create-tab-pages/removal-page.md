---
title: タブ削除のページを作成する
author: laujan
description: '[方法] タブ削除ページを作成する'
keywords: teams タブグループチャネルの構成可能な削除削除
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4ee060b8ef1f439ed4f8e4007e63606ce34c3d24
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964593"
---
# <a name="modify-or-remove-a-channel-group-tab"></a><span data-ttu-id="42052-104">チャネルグループタブの変更または削除</span><span class="sxs-lookup"><span data-stu-id="42052-104">Modify or remove a channel group tab</span></span>

<span data-ttu-id="42052-105">アプリでの削除および変更オプションをサポートすることで、ユーザーの作業を拡張し、強化することができます。</span><span class="sxs-lookup"><span data-stu-id="42052-105">You can extend and enhance the user experience by supporting removal and modification options in your app.</span></span> <span data-ttu-id="42052-106">Teams を使用すると、ユーザーは [チャネル/グループ] タブの名前を変更または削除することができ、インストール後にタブを再構成することができます。</span><span class="sxs-lookup"><span data-stu-id="42052-106">Teams enables users to rename or remove a channel/group tab and you can permit users to reconfigure your tab after installation.</span></span> <span data-ttu-id="42052-107">また、タブ削除の操作では、タブが削除されたときにコンテンツに何が起きるかを指定したり、コンテンツの削除やアーカイブなどの削除後のオプションをユーザーに提供したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="42052-107">Additionally, your tab removal experience can include designating what happens to the content when your tab is removed or giving users post-removal options such as deleting or archiving the content.</span></span>

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a><span data-ttu-id="42052-108">インストール後にタブを再構成できるようにする</span><span class="sxs-lookup"><span data-stu-id="42052-108">Enable your tab to be reconfigured after installation</span></span>

<span data-ttu-id="42052-109">**manifest.jsで**は、タブの機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="42052-109">Your **manifest.json** defines your tab's features and capabilities.</span></span> <span data-ttu-id="42052-110">Tab インスタンスプロパティは、 `canUpdateConfiguration` 作成後にユーザーがタブを変更または再構成できるかどうかを示すブール値を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="42052-110">The tab instance `canUpdateConfiguration` property takes a Boolean value that indicates whether a user can modify or reconfigure the tab after it is created:</span></span>

|<span data-ttu-id="42052-111">Name</span><span class="sxs-lookup"><span data-stu-id="42052-111">Name</span></span>| <span data-ttu-id="42052-112">型</span><span class="sxs-lookup"><span data-stu-id="42052-112">Type</span></span>| <span data-ttu-id="42052-113">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="42052-113">Maximum size</span></span> | <span data-ttu-id="42052-114">必須</span><span class="sxs-lookup"><span data-stu-id="42052-114">Required</span></span> | <span data-ttu-id="42052-115">説明</span><span class="sxs-lookup"><span data-stu-id="42052-115">Description</span></span>|
|---|---|---|---|---|
|`canUpdateConfiguration`|<span data-ttu-id="42052-116">ブール型</span><span class="sxs-lookup"><span data-stu-id="42052-116">Boolean</span></span>|||<span data-ttu-id="42052-117">作成後にタブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="42052-117">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="42052-118">限り `true`</span><span class="sxs-lookup"><span data-stu-id="42052-118">Default: `true`</span></span>|

<span data-ttu-id="42052-119">タブがチャネルまたはグループチャットにアップロードされると、チームはタブに右クリックされたドロップダウンメニューを追加します。使用可能なオプションは、次の設定によって決まり `canUpdateConfiguration` ます。</span><span class="sxs-lookup"><span data-stu-id="42052-119">When your tab is uploaded to a channel or group chat, Teams will add a right-click drop-down menu for your tab. The available options are determined by the `canUpdateConfiguration` setting:</span></span>

| `canUpdateConfiguration`| <span data-ttu-id="42052-120">true</span><span class="sxs-lookup"><span data-stu-id="42052-120">true</span></span>   | <span data-ttu-id="42052-121">false</span><span class="sxs-lookup"><span data-stu-id="42052-121">false</span></span> | <span data-ttu-id="42052-122">説明</span><span class="sxs-lookup"><span data-stu-id="42052-122">description</span></span> |
| ----------------------- | :----: | ----- | ----------- |
|     <span data-ttu-id="42052-123">設定</span><span class="sxs-lookup"><span data-stu-id="42052-123">Settings</span></span>            |   <span data-ttu-id="42052-124">√</span><span class="sxs-lookup"><span data-stu-id="42052-124">√</span></span>    |       |<span data-ttu-id="42052-125">`configurationUrl`ページが IFrame に再読み込みされ、ユーザーがタブを再設定できるようになります。</span><span class="sxs-lookup"><span data-stu-id="42052-125">The `configurationUrl` page is reloaded in an IFrame allowing the user to reconfigure the tab.</span></span>  |
|     <span data-ttu-id="42052-126">名前の変更</span><span class="sxs-lookup"><span data-stu-id="42052-126">Rename</span></span>              |   <span data-ttu-id="42052-127">√</span><span class="sxs-lookup"><span data-stu-id="42052-127">√</span></span>    |   <span data-ttu-id="42052-128">√</span><span class="sxs-lookup"><span data-stu-id="42052-128">√</span></span>   | <span data-ttu-id="42052-129">ユーザーは、タブバーに表示されるタブ名を変更できます。</span><span class="sxs-lookup"><span data-stu-id="42052-129">The user can change the tab name as it appears in the tab bar.</span></span>          |
|     <span data-ttu-id="42052-130">削除</span><span class="sxs-lookup"><span data-stu-id="42052-130">Remove</span></span>              |   <span data-ttu-id="42052-131">√</span><span class="sxs-lookup"><span data-stu-id="42052-131">√</span></span>    |   <span data-ttu-id="42052-132">√</span><span class="sxs-lookup"><span data-stu-id="42052-132">√</span></span>   |  <span data-ttu-id="42052-133">`removeURL`プロパティと値が [**構成] ページ**に含まれている場合は、**削除ページ**が IFrame に読み込まれ、ユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="42052-133">If the  `removeURL` property and value are included in the **configuration page**, the **removal page** is loaded into an IFrame and presented to the user.</span></span> <span data-ttu-id="42052-134">削除ページが含まれていない場合は、ユーザーに確認のダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="42052-134">If a removal page is not included the user is presented with a confirm dialog box.</span></span>          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a><span data-ttu-id="42052-135">アプリケーションのタブ削除ページを作成する</span><span class="sxs-lookup"><span data-stu-id="42052-135">Create a tab removal page for your application</span></span>

<span data-ttu-id="42052-136">オプションの削除ページは、ホストする HTML ページで、タブが削除されるときに表示されます。</span><span class="sxs-lookup"><span data-stu-id="42052-136">The optional removal page is an HTML page that you host and is displayed when the tab is removed.</span></span> <span data-ttu-id="42052-137">削除ページの URL は、構成ページ内のメソッドによって指定され `setSettings()` ます。</span><span class="sxs-lookup"><span data-stu-id="42052-137">The removal page URL is designated by the `setSettings()` method within your configuration page.</span></span> <span data-ttu-id="42052-138">アプリ内のすべてのページと同様に、削除ページは [Teams のタブ要件](~/tabs/how-to/add-tab.md)に準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="42052-138">As with all pages in your app, the removal page must comply with [Teams tab requirements](~/tabs/how-to/add-tab.md).</span></span>

### <a name="register-a-remove-handler"></a><span data-ttu-id="42052-139">削除ハンドラーを登録する</span><span class="sxs-lookup"><span data-stu-id="42052-139">Register a remove handler</span></span>

<span data-ttu-id="42052-140">必要に応じて、削除ページロジック内で、 `registerOnRemoveHandler((RemoveEvent) => {}` ユーザーが既存のタブ構成を削除したときに、イベントハンドラーを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="42052-140">Optionally, within your removal page logic, you can  invoke the `registerOnRemoveHandler((RemoveEvent) => {}` event handler when the user removes an existing tab configuration.</span></span> <span data-ttu-id="42052-141">メソッドはインターフェイスを取得 [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) し、ユーザーがコンテンツを削除しようとしたときにハンドラー内のコードを実行します。</span><span class="sxs-lookup"><span data-stu-id="42052-141">The  method takes in the [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) interface and executes the code in the handler when a user attempts to remove content.</span></span> <span data-ttu-id="42052-142">これを使用して、基になるリソースを削除するなどのクリーンアップ操作を実行して、タブのコンテンツを電源にします。</span><span class="sxs-lookup"><span data-stu-id="42052-142">It is used to perform cleanup operations such as removing the underlying resource powering the tab content.</span></span> <span data-ttu-id="42052-143">一度に登録できる削除ハンドラーは1つだけです。</span><span class="sxs-lookup"><span data-stu-id="42052-143">Only one remove handler can be registered at a time.</span></span>

<span data-ttu-id="42052-144">この `RemoveEvent` インターフェイスは、次の2つのメソッドを使用してオブジェクトを記述します。</span><span class="sxs-lookup"><span data-stu-id="42052-144">The `RemoveEvent` interface describes an object with two methods:</span></span>

* <span data-ttu-id="42052-145">`notifySuccess()`関数が必要です。</span><span class="sxs-lookup"><span data-stu-id="42052-145">The `notifySuccess()` function is required.</span></span> <span data-ttu-id="42052-146">これは、基になるリソースの削除が正常に終了し、そのコンテンツを削除できることを示します。</span><span class="sxs-lookup"><span data-stu-id="42052-146">It indicates that the removal of the underlying resource succeeded and its content can be removed.</span></span>

* <span data-ttu-id="42052-147">`notifyFailure(string)`関数はオプションです。</span><span class="sxs-lookup"><span data-stu-id="42052-147">The `notifyFailure(string)` function is optional.</span></span> <span data-ttu-id="42052-148">基になるリソースの削除が失敗し、そのコンテンツを削除できないことを示します。</span><span class="sxs-lookup"><span data-stu-id="42052-148">It indicates that removal of the underlying resource failed and its content cannot be removed.</span></span> <span data-ttu-id="42052-149">オプションの文字列パラメーターは、失敗の理由を指定します。</span><span class="sxs-lookup"><span data-stu-id="42052-149">The optional string parameter specifies a reason for the failure.</span></span> <span data-ttu-id="42052-150">指定した場合、この文字列がユーザーに表示されます。それ以外の場合は、一般的なエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="42052-150">If provided, this string is displayed to the user; otherwise a generic error is displayed.</span></span>

#### <a name="use-the-getsettings-function"></a><span data-ttu-id="42052-151">関数を使用する `getSettings()`</span><span class="sxs-lookup"><span data-stu-id="42052-151">Use the `getSettings()` function</span></span>

<span data-ttu-id="42052-152">を使用し `getSettings()` て、削除するタブの内容を指定できます。</span><span class="sxs-lookup"><span data-stu-id="42052-152">You can use `getSettings()`to designate the tab content to be removed.</span></span> <span data-ttu-id="42052-153">`getSettings((Settings) =>{})`関数は、を使用して、 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 取得できる有効な設定プロパティ値を提供します。</span><span class="sxs-lookup"><span data-stu-id="42052-153">The `getSettings((Settings) =>{})` function takes in the [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) and provides the valid settings property values that can be retrieved.</span></span>

#### <a name="use-the-getcontext-function"></a><span data-ttu-id="42052-154">関数を使用する `getContext()`</span><span class="sxs-lookup"><span data-stu-id="42052-154">Use the `getContext()` function</span></span>

<span data-ttu-id="42052-155">を使用して、 `getContext()` フレームが実行されている現在のコンテキストを取得できます。</span><span class="sxs-lookup"><span data-stu-id="42052-155">You can use `getContext()` to retrieves the current context in which the frame is running.</span></span> <span data-ttu-id="42052-156">関数は、を使用して、削除ページ `getContext((Context) =>{})` [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) `Context` に表示するコンテンツを決定するために削除ページロジックで使用できる有効なプロパティ値を提供します。</span><span class="sxs-lookup"><span data-stu-id="42052-156">The `getContext((Context) =>{})` function takes in the [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) and provides valid `Context` property values that you can use in your removal page logic to determine the content to display in the removal page.</span></span>

#### <a name="include-authentication"></a><span data-ttu-id="42052-157">認証を含める</span><span class="sxs-lookup"><span data-stu-id="42052-157">Include authentication</span></span>

<span data-ttu-id="42052-158">ユーザーがタブの内容を削除できるようにするには、認証が必要な場合があります。</span><span class="sxs-lookup"><span data-stu-id="42052-158">You might require authentication before allowing a user to delete the tab content.</span></span> <span data-ttu-id="42052-159">コンテキスト情報を使用して、認証要求および認証ページの Url を作成することができます。</span><span class="sxs-lookup"><span data-stu-id="42052-159">Context information can be used to help construct authentication requests and authorization page URLs.</span></span> <span data-ttu-id="42052-160">[タブについては、「Microsoft Teams の認証フロー」を](~/tabs/how-to/authentication/auth-flow-tab.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="42052-160">See [Microsoft Teams authentication flow for tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="42052-161">タブページで使用されているすべてのドメインが配列に含まれていることを確認してください `manifest.json` `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="42052-161">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

<span data-ttu-id="42052-162">タブ削除コードブロックの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="42052-162">Below is a sample tab removal code block:</span></span>

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    microsoftTeams.initialize();
    microsoftTeams.settings.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        microsoftTeams.settings.getSettings((settings) => {
        settings.contentUrl = "..."
        });
        removeEvent.notifySuccess();
    });

    const onClick() => {
        microsoftTeams.settings.setValidityState(true);
    }
  </script>
</body>

```

<span data-ttu-id="42052-163">ユーザーがタブのドロップダウンメニューから [ **削除** ] を選択すると、Teams は、 `removeUrl` ( **構成ページ**で指定されている) 省略可能なページを IFrame に読み込みます。</span><span class="sxs-lookup"><span data-stu-id="42052-163">When a user selects **Remove** from the tab's drop-down menu, Teams will load the optional `removeUrl` page (designated in your **configuration page**) into an IFrame.</span></span> <span data-ttu-id="42052-164">ここでは、削除 `onClick()` `microsoftTeams.settings.setValidityState(true)` ページの IFrame の下部にある [ **削除** ] ボタンを呼び出して有効にする関数と共に、ユーザーにボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="42052-164">Here, the user is presented with a button loaded with the `onClick()` function that calls `microsoftTeams.settings.setValidityState(true)` and enables the **Remove** button located near the bottom of the removal page IFrame.</span></span>

<span data-ttu-id="42052-165">削除ハンドラーの実行後、 `removeEvent.notifySuccess()` または `removeEvent.notifyFailure()` チームにコンテンツ削除の結果が通知されます。</span><span class="sxs-lookup"><span data-stu-id="42052-165">Following the execution of the remove handler, `removeEvent.notifySuccess()` or `removeEvent.notifyFailure()` notifies Teams of the content removal outcome.</span></span>

>[!NOTE]
><span data-ttu-id="42052-166">承認されたユーザーのコントロールがタブで禁止されないようにするために、Teams は成功とエラーの両方の場合にタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="42052-166">To ensure that an authorized user's control over a tab is not inhibited, Teams will remove the tab in both success and failure cases.\</span></span>
><span data-ttu-id="42052-167">Teams では、タブが呼び出されていない場合でも、5秒後に [ **削除** ] ボタンが有効になり `setValidityState()` ます。</span><span class="sxs-lookup"><span data-stu-id="42052-167">Teams enables the **Remove** button after 5 seconds, even if your tab hasn't called `setValidityState()`.\</span></span>
><span data-ttu-id="42052-168">ユーザーが [チームの **削除** ] を選択すると、操作が完了したかどうかにかかわらず、30秒後にタブが削除されます。</span><span class="sxs-lookup"><span data-stu-id="42052-168">When the user selects **Remove** Teams removes the tab after 30 seconds regardless of whether your actions have completed.</span></span>
