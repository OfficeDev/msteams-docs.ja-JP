---
title: タブ削除のページを作成する
author: laujan
description: タブ削除ページを作成する方法
keywords: Teams タブ グループ チャネルの構成可能な削除の削除
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 49e2df47095999e9f9eea76ea341a44215bfacb3
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797884"
---
# <a name="modify-or-remove-a-channel-group-tab"></a><span data-ttu-id="40494-104">チャネル グループ タブを変更または削除する</span><span class="sxs-lookup"><span data-stu-id="40494-104">Modify or remove a channel group tab</span></span>

<span data-ttu-id="40494-105">アプリで削除と変更のオプションをサポートすることで、ユーザー エクスペリエンスを拡張および強化できます。</span><span class="sxs-lookup"><span data-stu-id="40494-105">You can extend and enhance the user experience by supporting removal and modification options in your app.</span></span> <span data-ttu-id="40494-106">Teams を使用すると、ユーザーはチャネル/グループ タブの名前を変更または削除できます。また、インストール後にユーザーがタブを再構成することもできます。</span><span class="sxs-lookup"><span data-stu-id="40494-106">Teams enables users to rename or remove a channel/group tab and you can permit users to reconfigure your tab after installation.</span></span> <span data-ttu-id="40494-107">さらに、タブ削除エクスペリエンスには、タブが削除された場合のコンテンツに対する処理の指定や、コンテンツの削除やアーカイブなどの削除後のオプションをユーザーに提供する操作も含まれます。</span><span class="sxs-lookup"><span data-stu-id="40494-107">Additionally, your tab removal experience can include designating what happens to the content when your tab is removed or giving users post-removal options such as deleting or archiving the content.</span></span>

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a><span data-ttu-id="40494-108">インストール後にタブを再構成する</span><span class="sxs-lookup"><span data-stu-id="40494-108">Enable your tab to be reconfigured after installation</span></span>

<span data-ttu-id="40494-109">ユーザー **manifest.jsタブ** の機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="40494-109">Your **manifest.json** defines your tab's features and capabilities.</span></span> <span data-ttu-id="40494-110">タブ インスタンス プロパティは、ユーザーがタブの作成後に変更または再構成できるかどうかを示すブール `canUpdateConfiguration` 値を受け取います。</span><span class="sxs-lookup"><span data-stu-id="40494-110">The tab instance `canUpdateConfiguration` property takes a Boolean value that indicates whether a user can modify or reconfigure the tab after it is created:</span></span>

|<span data-ttu-id="40494-111">名前</span><span class="sxs-lookup"><span data-stu-id="40494-111">Name</span></span>| <span data-ttu-id="40494-112">型</span><span class="sxs-lookup"><span data-stu-id="40494-112">Type</span></span>| <span data-ttu-id="40494-113">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="40494-113">Maximum size</span></span> | <span data-ttu-id="40494-114">必須</span><span class="sxs-lookup"><span data-stu-id="40494-114">Required</span></span> | <span data-ttu-id="40494-115">説明</span><span class="sxs-lookup"><span data-stu-id="40494-115">Description</span></span>|
|---|---|---|---|---|
|`canUpdateConfiguration`|<span data-ttu-id="40494-116">Boolean</span><span class="sxs-lookup"><span data-stu-id="40494-116">Boolean</span></span>|||<span data-ttu-id="40494-117">タブの構成のインスタンスを作成後にユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="40494-117">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="40494-118">既定値: `true`</span><span class="sxs-lookup"><span data-stu-id="40494-118">Default: `true`</span></span>|

<span data-ttu-id="40494-119">タブがチャネルまたはグループ チャットにアップロードされると、Teams はタブの右クリック ドロップダウン メニューを追加します。使用可能なオプションは、設定によって決 `canUpdateConfiguration` まります。</span><span class="sxs-lookup"><span data-stu-id="40494-119">When your tab is uploaded to a channel or group chat, Teams will add a right-click drop-down menu for your tab. The available options are determined by the `canUpdateConfiguration` setting:</span></span>

| `canUpdateConfiguration`| <span data-ttu-id="40494-120">true</span><span class="sxs-lookup"><span data-stu-id="40494-120">true</span></span>   | <span data-ttu-id="40494-121">false</span><span class="sxs-lookup"><span data-stu-id="40494-121">false</span></span> | <span data-ttu-id="40494-122">説明</span><span class="sxs-lookup"><span data-stu-id="40494-122">description</span></span> |
| ----------------------- | :----: | ----- | ----------- |
|     <span data-ttu-id="40494-123">設定</span><span class="sxs-lookup"><span data-stu-id="40494-123">Settings</span></span>            |   <span data-ttu-id="40494-124">√</span><span class="sxs-lookup"><span data-stu-id="40494-124">√</span></span>    |       |<span data-ttu-id="40494-125">ページ `configurationUrl` が IFrame に再読み込みされ、ユーザーはタブを再構成できます。</span><span class="sxs-lookup"><span data-stu-id="40494-125">The `configurationUrl` page is reloaded in an IFrame allowing the user to reconfigure the tab.</span></span>  |
|     <span data-ttu-id="40494-126">名前の変更</span><span class="sxs-lookup"><span data-stu-id="40494-126">Rename</span></span>              |   <span data-ttu-id="40494-127">√</span><span class="sxs-lookup"><span data-stu-id="40494-127">√</span></span>    |   <span data-ttu-id="40494-128">√</span><span class="sxs-lookup"><span data-stu-id="40494-128">√</span></span>   | <span data-ttu-id="40494-129">ユーザーは、タブ バーに表示されるタブ名を変更できます。</span><span class="sxs-lookup"><span data-stu-id="40494-129">The user can change the tab name as it appears in the tab bar.</span></span>          |
|     <span data-ttu-id="40494-130">削除</span><span class="sxs-lookup"><span data-stu-id="40494-130">Remove</span></span>              |   <span data-ttu-id="40494-131">√</span><span class="sxs-lookup"><span data-stu-id="40494-131">√</span></span>    |   <span data-ttu-id="40494-132">√</span><span class="sxs-lookup"><span data-stu-id="40494-132">√</span></span>   |  <span data-ttu-id="40494-133">プロパティと値が構成ページに含まれている場合、削除ページは IFrame に読み込まれ `removeURL` 、ユーザーに表示されます。  </span><span class="sxs-lookup"><span data-stu-id="40494-133">If the  `removeURL` property and value are included in the **configuration page**, the **removal page** is loaded into an IFrame and presented to the user.</span></span> <span data-ttu-id="40494-134">削除ページが含まれていない場合は、ユーザーに確認ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="40494-134">If a removal page is not included the user is presented with a confirm dialog box.</span></span>          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a><span data-ttu-id="40494-135">アプリケーションのタブ削除ページを作成する</span><span class="sxs-lookup"><span data-stu-id="40494-135">Create a tab removal page for your application</span></span>

<span data-ttu-id="40494-136">オプションの削除ページは、ホストする HTML ページであり、タブが削除されると表示されます。</span><span class="sxs-lookup"><span data-stu-id="40494-136">The optional removal page is an HTML page that you host and is displayed when the tab is removed.</span></span> <span data-ttu-id="40494-137">削除ページの URL は、構成ページ `setSettings()` 内のメソッドによって指定されます。</span><span class="sxs-lookup"><span data-stu-id="40494-137">The removal page URL is designated by the `setSettings()` method within your configuration page.</span></span> <span data-ttu-id="40494-138">アプリ内のすべてのページと同様に、削除ページは Teams タブの要件 [に準拠している必要があります](../../../tabs/how-to/tab-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="40494-138">As with all pages in your app, the removal page must comply with [Teams tab requirements](../../../tabs/how-to/tab-requirements.md).</span></span>

### <a name="register-a-remove-handler"></a><span data-ttu-id="40494-139">削除ハンドラーを登録する</span><span class="sxs-lookup"><span data-stu-id="40494-139">Register a remove handler</span></span>

<span data-ttu-id="40494-140">必要に応じて、削除ページ ロジック内で、ユーザーが既存のタブ構成を削除するときにイベント ハンドラー `registerOnRemoveHandler((RemoveEvent) => {}` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="40494-140">Optionally, within your removal page logic, you can  invoke the `registerOnRemoveHandler((RemoveEvent) => {}` event handler when the user removes an existing tab configuration.</span></span> <span data-ttu-id="40494-141">このメソッドはインターフェイスを取り込み、ユーザーがコンテンツを削除しようとするときにハンドラーで [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) コードを実行します。</span><span class="sxs-lookup"><span data-stu-id="40494-141">The  method takes in the [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) interface and executes the code in the handler when a user attempts to remove content.</span></span> <span data-ttu-id="40494-142">このプロパティは、基になるリソースを削除してタブ コンテンツを作成するなどのクリーンアップ操作を実行するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="40494-142">It is used to perform cleanup operations such as removing the underlying resource powering the tab content.</span></span> <span data-ttu-id="40494-143">一度に登録できる削除ハンドラーは 1 つのみです。</span><span class="sxs-lookup"><span data-stu-id="40494-143">Only one remove handler can be registered at a time.</span></span>

<span data-ttu-id="40494-144">インターフェイス `RemoveEvent` は、2 つのメソッドを持つオブジェクトを記述します。</span><span class="sxs-lookup"><span data-stu-id="40494-144">The `RemoveEvent` interface describes an object with two methods:</span></span>

* <span data-ttu-id="40494-145">この `notifySuccess()` 関数は必須です。</span><span class="sxs-lookup"><span data-stu-id="40494-145">The `notifySuccess()` function is required.</span></span> <span data-ttu-id="40494-146">基になるリソースの削除が成功し、そのコンテンツを削除できる状態を示します。</span><span class="sxs-lookup"><span data-stu-id="40494-146">It indicates that the removal of the underlying resource succeeded and its content can be removed.</span></span>

* <span data-ttu-id="40494-147">この `notifyFailure(string)` 関数は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="40494-147">The `notifyFailure(string)` function is optional.</span></span> <span data-ttu-id="40494-148">基になるリソースの削除が失敗し、そのコンテンツを削除できないことを示します。</span><span class="sxs-lookup"><span data-stu-id="40494-148">It indicates that removal of the underlying resource failed and its content cannot be removed.</span></span> <span data-ttu-id="40494-149">オプションの文字列パラメーターは、失敗の理由を指定します。</span><span class="sxs-lookup"><span data-stu-id="40494-149">The optional string parameter specifies a reason for the failure.</span></span> <span data-ttu-id="40494-150">指定した場合、この文字列はユーザーに表示されます。それ以外の場合は、汎用エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="40494-150">If provided, this string is displayed to the user; otherwise a generic error is displayed.</span></span>

#### <a name="use-the-getsettings-function"></a><span data-ttu-id="40494-151">関数を使用 `getSettings()` する</span><span class="sxs-lookup"><span data-stu-id="40494-151">Use the `getSettings()` function</span></span>

<span data-ttu-id="40494-152">削除する `getSettings()` タブ コンテンツを指定するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="40494-152">You can use `getSettings()`to designate the tab content to be removed.</span></span> <span data-ttu-id="40494-153">この `getSettings((Settings) =>{})` 関数は、取得 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 可能な有効な設定プロパティ値を取り込み、提供します。</span><span class="sxs-lookup"><span data-stu-id="40494-153">The `getSettings((Settings) =>{})` function takes in the [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) and provides the valid settings property values that can be retrieved.</span></span>

#### <a name="use-the-getcontext-function"></a><span data-ttu-id="40494-154">関数を使用 `getContext()` する</span><span class="sxs-lookup"><span data-stu-id="40494-154">Use the `getContext()` function</span></span>

<span data-ttu-id="40494-155">フレームが `getContext()` 実行されている現在のコンテキストを取得するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="40494-155">You can use `getContext()` to retrieves the current context in which the frame is running.</span></span> <span data-ttu-id="40494-156">関数は、削除ページのロジックで使用できる有効なプロパティ値を取り込み、削除ページに表示するコンテンツ `getContext((Context) =>{})` [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) `Context` を決定します。</span><span class="sxs-lookup"><span data-stu-id="40494-156">The `getContext((Context) =>{})` function takes in the [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) and provides valid `Context` property values that you can use in your removal page logic to determine the content to display in the removal page.</span></span>

#### <a name="include-authentication"></a><span data-ttu-id="40494-157">認証を含める</span><span class="sxs-lookup"><span data-stu-id="40494-157">Include authentication</span></span>

<span data-ttu-id="40494-158">ユーザーにタブ コンテンツの削除を許可する前に認証が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="40494-158">You might require authentication before allowing a user to delete the tab content.</span></span> <span data-ttu-id="40494-159">コンテキスト情報は、認証要求と承認ページ URL の構築に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="40494-159">Context information can be used to help construct authentication requests and authorization page URLs.</span></span> <span data-ttu-id="40494-160">タブについては [、Microsoft Teams の認証フローを参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="40494-160">See [Microsoft Teams authentication flow for tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="40494-161">タブ ページで使用されているドメインすべてが配列に表示されます `manifest.json` `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="40494-161">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

<span data-ttu-id="40494-162">次に、タブ削除コード ブロックのサンプルを示します。</span><span class="sxs-lookup"><span data-stu-id="40494-162">Below is a sample tab removal code block:</span></span>

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

<span data-ttu-id="40494-163">ユーザーがタブのドロップダウンメニューから [削除] を選択すると、Teams はオプションのページ (構成ページで指定) を IFrame に読み込 `removeUrl` む必要があります。 </span><span class="sxs-lookup"><span data-stu-id="40494-163">When a user selects **Remove** from the tab's drop-down menu, Teams will load the optional `removeUrl` page (designated in your **configuration page**) into an IFrame.</span></span> <span data-ttu-id="40494-164">ここでは、ユーザーには、削除ページ IFrame の下部付近にある [削除] ボタンを呼び出す関数が読み込まれたボタン `onClick()` `microsoftTeams.settings.setValidityState(true)` が表示されます。 </span><span class="sxs-lookup"><span data-stu-id="40494-164">Here, the user is presented with a button loaded with the `onClick()` function that calls `microsoftTeams.settings.setValidityState(true)` and enables the **Remove** button located near the bottom of the removal page IFrame.</span></span>

<span data-ttu-id="40494-165">削除ハンドラーの実行に従って、 `removeEvent.notifySuccess()` または `removeEvent.notifyFailure()` コンテンツ削除の結果を Teams に通知します。</span><span class="sxs-lookup"><span data-stu-id="40494-165">Following the execution of the remove handler, `removeEvent.notifySuccess()` or `removeEvent.notifyFailure()` notifies Teams of the content removal outcome.</span></span>

>[!NOTE]
><span data-ttu-id="40494-166">承認されたユーザーによるタブに対する制御が禁止されない場合、Teams は成功と失敗の両方の場合にタブを削除します。</span><span class="sxs-lookup"><span data-stu-id="40494-166">To ensure that an authorized user's control over a tab is not inhibited, Teams will remove the tab in both success and failure cases.</span></span>\
><span data-ttu-id="40494-167">Teams は、 **タブが呼** び出されていない場合でも、5 秒後に [削除] ボタンを `setValidityState()` 有効にします。</span><span class="sxs-lookup"><span data-stu-id="40494-167">Teams enables the **Remove** button after 5 seconds, even if your tab hasn't called `setValidityState()`.\</span></span>
><span data-ttu-id="40494-168">ユーザーが **[Teams** の削除] を選択すると、操作が完了したかどうかに関係なく、30 秒後にタブが削除されます。</span><span class="sxs-lookup"><span data-stu-id="40494-168">When the user selects **Remove** Teams removes the tab after 30 seconds regardless of whether your actions have completed.</span></span>
