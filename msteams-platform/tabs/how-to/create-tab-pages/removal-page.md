---
title: タブ削除のページを作成する
author: laujan
description: タブ削除ページを作成する方法
keywords: チーム タブ グループ の構成可能な削除削除
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: e1a1f38a2bcb3b5bc4bc54f469c8727e44d8695e
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566671"
---
# <a name="modify-or-remove-a-channel-group-tab"></a><span data-ttu-id="abc35-104">チャネル グループ タブを変更または削除する</span><span class="sxs-lookup"><span data-stu-id="abc35-104">Modify or remove a channel group tab</span></span>

<span data-ttu-id="abc35-105">アプリの削除および変更オプションをサポートすることで、ユーザー エクスペリエンスを拡張および強化できます。</span><span class="sxs-lookup"><span data-stu-id="abc35-105">You can extend and enhance the user experience by supporting removal and modification options in your app.</span></span> <span data-ttu-id="abc35-106">Teams、ユーザーはチャンネル/グループタブの名前を変更したり削除したりすることができ、インストール後にユーザーがタブを再構成することを許可することができます。</span><span class="sxs-lookup"><span data-stu-id="abc35-106">Teams enables users to rename or remove a channel/group tab and you can permit users to reconfigure your tab after installation.</span></span> <span data-ttu-id="abc35-107">また、タブの削除には、タブが削除されたときにコンテンツに何が起こるかを指定したり、コンテンツの削除やアーカイブなどの削除後のオプションをユーザーに提供したりすることが含まれます。</span><span class="sxs-lookup"><span data-stu-id="abc35-107">Additionally, your tab removal experience can include designating what happens to the content when your tab is removed or giving users post-removal options such as deleting or archiving the content.</span></span>

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a><span data-ttu-id="abc35-108">インストール後にタブを再構成できるようにする</span><span class="sxs-lookup"><span data-stu-id="abc35-108">Enable your tab to be reconfigured after installation</span></span>

<span data-ttu-id="abc35-109">上 **のmanifest.js** は、タブの機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="abc35-109">Your **manifest.json** defines your tab's features and capabilities.</span></span> <span data-ttu-id="abc35-110">タブインスタンス `canUpdateConfiguration` プロパティは、ユーザーがタブの作成後にタブを変更または再構成できるかどうかを示すブール値を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="abc35-110">The tab instance `canUpdateConfiguration` property takes a Boolean value that indicates whether a user can modify or reconfigure the tab after it is created:</span></span>

|<span data-ttu-id="abc35-111">名前</span><span class="sxs-lookup"><span data-stu-id="abc35-111">Name</span></span>| <span data-ttu-id="abc35-112">型</span><span class="sxs-lookup"><span data-stu-id="abc35-112">Type</span></span>| <span data-ttu-id="abc35-113">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="abc35-113">Maximum size</span></span> | <span data-ttu-id="abc35-114">必須</span><span class="sxs-lookup"><span data-stu-id="abc35-114">Required</span></span> | <span data-ttu-id="abc35-115">説明</span><span class="sxs-lookup"><span data-stu-id="abc35-115">Description</span></span>|
|---|---|---|---|---|
|`canUpdateConfiguration`|<span data-ttu-id="abc35-116">Boolean</span><span class="sxs-lookup"><span data-stu-id="abc35-116">Boolean</span></span>|||<span data-ttu-id="abc35-117">タブの構成のインスタンスを作成後にユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="abc35-117">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="abc35-118">デフォルト： `true`</span><span class="sxs-lookup"><span data-stu-id="abc35-118">Default: `true`</span></span>|

<span data-ttu-id="abc35-119">タブがチャンネルまたはグループチャットにアップロードされると、Teamsタブの右クリックドロップダウンメニューが追加されます。使用可能なオプションは、設定によって決まります `canUpdateConfiguration` 。</span><span class="sxs-lookup"><span data-stu-id="abc35-119">When your tab is uploaded to a channel or group chat, Teams will add a right-click drop-down menu for your tab. The available options are determined by the `canUpdateConfiguration` setting:</span></span>

| `canUpdateConfiguration`| <span data-ttu-id="abc35-120">true</span><span class="sxs-lookup"><span data-stu-id="abc35-120">true</span></span>   | <span data-ttu-id="abc35-121">false</span><span class="sxs-lookup"><span data-stu-id="abc35-121">false</span></span> | <span data-ttu-id="abc35-122">説明</span><span class="sxs-lookup"><span data-stu-id="abc35-122">description</span></span> |
| ----------------------- | :----: | ----- | ----------- |
|     <span data-ttu-id="abc35-123">設定</span><span class="sxs-lookup"><span data-stu-id="abc35-123">Settings</span></span>            |   <span data-ttu-id="abc35-124">√</span><span class="sxs-lookup"><span data-stu-id="abc35-124">√</span></span>    |       |<span data-ttu-id="abc35-125">`configurationUrl`ページが IFrame に再読み込みされ、ユーザーはタブを再構成できます。</span><span class="sxs-lookup"><span data-stu-id="abc35-125">The `configurationUrl` page is reloaded in an IFrame allowing the user to reconfigure the tab.</span></span>  |
|     <span data-ttu-id="abc35-126">名前の変更</span><span class="sxs-lookup"><span data-stu-id="abc35-126">Rename</span></span>              |   <span data-ttu-id="abc35-127">√</span><span class="sxs-lookup"><span data-stu-id="abc35-127">√</span></span>    |   <span data-ttu-id="abc35-128">√</span><span class="sxs-lookup"><span data-stu-id="abc35-128">√</span></span>   | <span data-ttu-id="abc35-129">ユーザーは、タブバーに表示されるタブ名を変更できます。</span><span class="sxs-lookup"><span data-stu-id="abc35-129">The user can change the tab name as it appears in the tab bar.</span></span>          |
|     <span data-ttu-id="abc35-130">削除</span><span class="sxs-lookup"><span data-stu-id="abc35-130">Remove</span></span>              |   <span data-ttu-id="abc35-131">√</span><span class="sxs-lookup"><span data-stu-id="abc35-131">√</span></span>    |   <span data-ttu-id="abc35-132">√</span><span class="sxs-lookup"><span data-stu-id="abc35-132">√</span></span>   |  <span data-ttu-id="abc35-133">`removeURL`プロパティと値が **構成ページ** に含まれている場合、**削除ページ** は IFrame に読み込まれ、ユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="abc35-133">If the  `removeURL` property and value are included in the **configuration page**, the **removal page** is loaded into an IFrame and presented to the user.</span></span> <span data-ttu-id="abc35-134">削除ページが含まれていない場合、ユーザーには確認ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="abc35-134">If a removal page is not included the user is presented with a confirm dialog box.</span></span>          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a><span data-ttu-id="abc35-135">アプリケーションのタブ削除ページを作成する</span><span class="sxs-lookup"><span data-stu-id="abc35-135">Create a tab removal page for your application</span></span>

<span data-ttu-id="abc35-136">省略可能な削除ページは、ホストする HTML ページで、タブが削除されると表示されます。</span><span class="sxs-lookup"><span data-stu-id="abc35-136">The optional removal page is an HTML page that you host and is displayed when the tab is removed.</span></span> <span data-ttu-id="abc35-137">削除ページの URL は、 `setSettings()` 構成ページ内のメソッドによって指定されます。</span><span class="sxs-lookup"><span data-stu-id="abc35-137">The removal page URL is designated by the `setSettings()` method within your configuration page.</span></span> <span data-ttu-id="abc35-138">アプリのすべてのページと同様に、削除ページは[Teams タブの要件](../../../tabs/how-to/tab-requirements.md)に準拠している必要があります。</span><span class="sxs-lookup"><span data-stu-id="abc35-138">As with all pages in your app, the removal page must comply with [Teams tab requirements](../../../tabs/how-to/tab-requirements.md).</span></span>

### <a name="register-a-remove-handler"></a><span data-ttu-id="abc35-139">削除ハンドラーを登録する</span><span class="sxs-lookup"><span data-stu-id="abc35-139">Register a remove handler</span></span>

<span data-ttu-id="abc35-140">必要に応じて、削除ページロジック内で、 `registerOnRemoveHandler((RemoveEvent) => {}` ユーザーが既存のタブ構成を削除したときにイベントハンドラーを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="abc35-140">Optionally, within your removal page logic, you can  invoke the `registerOnRemoveHandler((RemoveEvent) => {}` event handler when the user removes an existing tab configuration.</span></span> <span data-ttu-id="abc35-141">このメソッドは [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) 、ユーザーがコンテンツを削除しようとしたときに、インターフェイスを取得してハンドラー内のコードを実行します。</span><span class="sxs-lookup"><span data-stu-id="abc35-141">The  method takes in the [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) interface and executes the code in the handler when a user attempts to remove content.</span></span> <span data-ttu-id="abc35-142">これは、タブの内容に電力を供給する基になるリソースを削除するなどのクリーンアップ操作を実行するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="abc35-142">It is used to perform cleanup operations such as removing the underlying resource powering the tab content.</span></span> <span data-ttu-id="abc35-143">一度に登録できる削除ハンドラは 1 つだけです。</span><span class="sxs-lookup"><span data-stu-id="abc35-143">Only one remove handler can be registered at a time.</span></span>

<span data-ttu-id="abc35-144">`RemoveEvent`このインターフェイスは、2 つのメソッドを持つオブジェクトを記述します。</span><span class="sxs-lookup"><span data-stu-id="abc35-144">The `RemoveEvent` interface describes an object with two methods:</span></span>

* <span data-ttu-id="abc35-145">`notifySuccess()`関数は必須です。</span><span class="sxs-lookup"><span data-stu-id="abc35-145">The `notifySuccess()` function is required.</span></span> <span data-ttu-id="abc35-146">基になるリソースの削除が成功し、その内容を削除できることを示します。</span><span class="sxs-lookup"><span data-stu-id="abc35-146">It indicates that the removal of the underlying resource succeeded and its content can be removed.</span></span>

* <span data-ttu-id="abc35-147">`notifyFailure(string)`この関数はオプションです。</span><span class="sxs-lookup"><span data-stu-id="abc35-147">The `notifyFailure(string)` function is optional.</span></span> <span data-ttu-id="abc35-148">基になるリソースの削除が失敗し、その内容を削除できないことを示します。</span><span class="sxs-lookup"><span data-stu-id="abc35-148">It indicates that removal of the underlying resource failed and its content cannot be removed.</span></span> <span data-ttu-id="abc35-149">省略可能な文字列パラメーターは、失敗の理由を指定します。</span><span class="sxs-lookup"><span data-stu-id="abc35-149">The optional string parameter specifies a reason for the failure.</span></span> <span data-ttu-id="abc35-150">指定した場合、この文字列はユーザーに表示されます。それ以外の場合は、一般的なエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="abc35-150">If provided, this string is displayed to the user; otherwise a generic error is displayed.</span></span>

#### <a name="use-the-getsettings-function"></a><span data-ttu-id="abc35-151">関数を使用する `getSettings()`</span><span class="sxs-lookup"><span data-stu-id="abc35-151">Use the `getSettings()` function</span></span>

<span data-ttu-id="abc35-152">を使用 `getSettings()` して、削除するタブコンテンツを指定できます。</span><span class="sxs-lookup"><span data-stu-id="abc35-152">You can use `getSettings()`to designate the tab content to be removed.</span></span> <span data-ttu-id="abc35-153">関数は `getSettings((Settings) =>{})` を取 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) り込み、取得できる有効な設定プロパティ値を提供します。</span><span class="sxs-lookup"><span data-stu-id="abc35-153">The `getSettings((Settings) =>{})` function takes in the [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) and provides the valid settings property values that can be retrieved.</span></span>

#### <a name="use-the-getcontext-function"></a><span data-ttu-id="abc35-154">関数を使用する `getContext()`</span><span class="sxs-lookup"><span data-stu-id="abc35-154">Use the `getContext()` function</span></span>

<span data-ttu-id="abc35-155">を使用 `getContext()` して、フレームが実行されている現在のコンテキストを取得できます。</span><span class="sxs-lookup"><span data-stu-id="abc35-155">You can use `getContext()` to retrieves the current context in which the frame is running.</span></span> <span data-ttu-id="abc35-156">`getContext((Context) =>{})`この関数は、 [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) を使用して有効な `Context` プロパティ値を提供し、削除ページのロジックで使用して削除ページに表示するコンテンツを決定します。</span><span class="sxs-lookup"><span data-stu-id="abc35-156">The `getContext((Context) =>{})` function takes in the [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) and provides valid `Context` property values that you can use in your removal page logic to determine the content to display in the removal page.</span></span>

#### <a name="include-authentication"></a><span data-ttu-id="abc35-157">認証を含める</span><span class="sxs-lookup"><span data-stu-id="abc35-157">Include authentication</span></span>

<span data-ttu-id="abc35-158">ユーザーがタブの内容を削除できるようにする前に、認証が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="abc35-158">You might require authentication before allowing a user to delete the tab content.</span></span> <span data-ttu-id="abc35-159">コンテキスト情報は、認証要求と承認ページ URL の構築に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="abc35-159">Context information can be used to help construct authentication requests and authorization page URLs.</span></span> <span data-ttu-id="abc35-160">[タブMicrosoft Teams認証フローを](~/tabs/how-to/authentication/auth-flow-tab.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="abc35-160">See [Microsoft Teams authentication flow for tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="abc35-161">タブページで使用されているすべてのドメインがアレイにリストされていることを確認します `manifest.json` `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="abc35-161">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

<span data-ttu-id="abc35-162">以下は、タブ削除コードブロックの例です。</span><span class="sxs-lookup"><span data-stu-id="abc35-162">Below is a sample tab removal code block:</span></span>

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

<span data-ttu-id="abc35-163">ユーザーがタブのドロップダウン メニューから **[削除]** を選択すると、Teamsはオプション ページ `removeUrl` (**構成ページ** で指定) を IFrame に読み込みます。</span><span class="sxs-lookup"><span data-stu-id="abc35-163">When a user selects **Remove** from the tab's drop-down menu, Teams will load the optional `removeUrl` page (designated in your **configuration page**) into an IFrame.</span></span> <span data-ttu-id="abc35-164">ここでは、削除 `onClick()` `microsoftTeams.settings.setValidityState(true)` ページ IFrame の下部にある **[削除** ] ボタンを呼び出して有効にする関数を読み込んだボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="abc35-164">Here, the user is presented with a button loaded with the `onClick()` function that calls `microsoftTeams.settings.setValidityState(true)` and enables the **Remove** button located near the bottom of the removal page IFrame.</span></span>

<span data-ttu-id="abc35-165">削除ハンドラの実行後、 `removeEvent.notifySuccess()` または `removeEvent.notifyFailure()` コンテンツ削除の結果をTeamsに通知します。</span><span class="sxs-lookup"><span data-stu-id="abc35-165">Following the execution of the remove handler, `removeEvent.notifySuccess()` or `removeEvent.notifyFailure()` notifies Teams of the content removal outcome.</span></span>

>[!NOTE]
> * <span data-ttu-id="abc35-166">承認されたユーザーによるタブの制御が禁止されないようにするには、Teams成功と失敗の両方のケースでタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="abc35-166">To ensure that an authorized user's control over a tab is not inhibited, Teams will remove the tab in both success and failure cases.\</span></span>
> * <span data-ttu-id="abc35-167">Teamsタブが .\ を呼び出していない場合でも、5 秒後に **[削除**] ボタンを有効 `setValidityState()` にします。</span><span class="sxs-lookup"><span data-stu-id="abc35-167">Teams enables the **Remove** button after 5 seconds, even if your tab hasn't called `setValidityState()`.\</span></span>
> * <span data-ttu-id="abc35-168">ユーザーが **[削除**] を選択すると、Teamsは、操作が完了したかどうかに関係なく、30 秒後にタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="abc35-168">When the user selects **Remove** Teams removes the tab after 30 seconds regardless of whether your actions have completed.</span></span>
