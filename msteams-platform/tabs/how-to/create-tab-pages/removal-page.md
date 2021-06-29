---
title: タブ削除のページを作成する
author: surbhigupta
description: タブの削除ページを作成する方法
keywords: teams タブ グループ チャネル構成可能 削除
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 97f5dfdd8cd9e5e19ec26c345ac960a04a108ab3
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179714"
---
# <a name="create-a-removal-page"></a><span data-ttu-id="58c1f-104">削除ページを作成する</span><span class="sxs-lookup"><span data-stu-id="58c1f-104">Create a removal page</span></span>

<span data-ttu-id="58c1f-105">アプリで削除と変更のオプションをサポートすることで、ユーザー エクスペリエンスを拡張および強化できます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-105">You can extend and enhance the user experience by supporting removal and modification options in your app.</span></span> <span data-ttu-id="58c1f-106">Teamsを使用すると、チャネルまたはグループ タブの名前の変更や削除が可能で、インストール後にユーザーがタブを再構成できます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-106">Teams enables users to rename or remove a channel or group tab and you can permit users to reconfigure your tab after installation.</span></span> <span data-ttu-id="58c1f-107">さらに、タブの削除エクスペリエンスでは、削除後のオプションをユーザーに提供して、コンテンツを削除またはアーカイブできます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-107">Additionally, the tab removal experience provides the users with post-removal options to delete or archive content.</span></span>

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a><span data-ttu-id="58c1f-108">インストール後にタブを再構成する</span><span class="sxs-lookup"><span data-stu-id="58c1f-108">Enable your tab to be reconfigured after installation</span></span>

<span data-ttu-id="58c1f-109">この **manifest.jsタブ** の機能を定義します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-109">Your **manifest.json** defines your tab's features and capabilities.</span></span> <span data-ttu-id="58c1f-110">tab instance プロパティは、ユーザーが作成後にタブを変更または再構成できるかどうかを示すブール値 `canUpdateConfiguration` を取得します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-110">The tab instance `canUpdateConfiguration` property takes a Boolean value that indicates whether a user can modify or reconfigure the tab after it is created.</span></span> <span data-ttu-id="58c1f-111">次の表に、プロパティの詳細を示します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-111">The following table provides the property details:</span></span>

|<span data-ttu-id="58c1f-112">名前</span><span class="sxs-lookup"><span data-stu-id="58c1f-112">Name</span></span>| <span data-ttu-id="58c1f-113">型</span><span class="sxs-lookup"><span data-stu-id="58c1f-113">Type</span></span>| <span data-ttu-id="58c1f-114">最大サイズ</span><span class="sxs-lookup"><span data-stu-id="58c1f-114">Maximum size</span></span> | <span data-ttu-id="58c1f-115">必須</span><span class="sxs-lookup"><span data-stu-id="58c1f-115">Required</span></span> | <span data-ttu-id="58c1f-116">説明</span><span class="sxs-lookup"><span data-stu-id="58c1f-116">Description</span></span>|
|---|---|---|---|---|
|`canUpdateConfiguration`|<span data-ttu-id="58c1f-117">Boolean</span><span class="sxs-lookup"><span data-stu-id="58c1f-117">Boolean</span></span>|||<span data-ttu-id="58c1f-118">作成後に、タブの構成のインスタンスをユーザーが更新できるかどうかを示す値。</span><span class="sxs-lookup"><span data-stu-id="58c1f-118">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="58c1f-119">既定値は `true` です。</span><span class="sxs-lookup"><span data-stu-id="58c1f-119">Default is `true`.</span></span> |

<span data-ttu-id="58c1f-120">タブがチャネルまたはグループ チャットにアップロードされると、Teamsの右クリック ドロップダウン メニューが追加されます。使用可能なオプションは、設定によって決 `canUpdateConfiguration` まります。</span><span class="sxs-lookup"><span data-stu-id="58c1f-120">When your tab is uploaded to a channel or group chat, Teams adds a right-click drop-down menu for your tab. The available options are determined by the `canUpdateConfiguration` setting.</span></span> <span data-ttu-id="58c1f-121">次の表に、設定の詳細を示します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-121">The following table provides the setting details:</span></span>

| `canUpdateConfiguration`| <span data-ttu-id="58c1f-122">true</span><span class="sxs-lookup"><span data-stu-id="58c1f-122">true</span></span>   | <span data-ttu-id="58c1f-123">false</span><span class="sxs-lookup"><span data-stu-id="58c1f-123">false</span></span> | <span data-ttu-id="58c1f-124">description</span><span class="sxs-lookup"><span data-stu-id="58c1f-124">description</span></span> |
| ----------------------- | :----: | ----- | ----------- |
|     <span data-ttu-id="58c1f-125">設定</span><span class="sxs-lookup"><span data-stu-id="58c1f-125">Settings</span></span>            |   <span data-ttu-id="58c1f-126">√</span><span class="sxs-lookup"><span data-stu-id="58c1f-126">√</span></span>    |       |<span data-ttu-id="58c1f-127">ページ `configurationUrl` が IFrame に再読み込みされ、ユーザーはタブを再構成できます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-127">The `configurationUrl` page is reloaded in an IFrame allowing the user to reconfigure the tab.</span></span> |
|     <span data-ttu-id="58c1f-128">名前の変更</span><span class="sxs-lookup"><span data-stu-id="58c1f-128">Rename</span></span>              |   <span data-ttu-id="58c1f-129">√</span><span class="sxs-lookup"><span data-stu-id="58c1f-129">√</span></span>    |   <span data-ttu-id="58c1f-130">√</span><span class="sxs-lookup"><span data-stu-id="58c1f-130">√</span></span>   | <span data-ttu-id="58c1f-131">ユーザーは、タブ バーに表示されるタブ名を変更できます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-131">The user can change the tab name as it appears in the tab bar.</span></span>          |
|     <span data-ttu-id="58c1f-132">削除</span><span class="sxs-lookup"><span data-stu-id="58c1f-132">Remove</span></span>              |   <span data-ttu-id="58c1f-133">√</span><span class="sxs-lookup"><span data-stu-id="58c1f-133">√</span></span>    |   <span data-ttu-id="58c1f-134">√</span><span class="sxs-lookup"><span data-stu-id="58c1f-134">√</span></span>   |  <span data-ttu-id="58c1f-135">プロパティと値が構成ページに含まれている場合は、削除ページが IFrame に読み込まれ `removeURL` 、ユーザーに表示されます。  </span><span class="sxs-lookup"><span data-stu-id="58c1f-135">If the  `removeURL` property and value are included in the **configuration page**, the **removal page** is loaded into an IFrame and presented to the user.</span></span> <span data-ttu-id="58c1f-136">削除ページが含まれていない場合は、ユーザーに確認ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-136">If a removal page is not included, the user is presented with a confirm dialog box.</span></span>          |

## <a name="create-a-tab-removal-page-for-your-application"></a><span data-ttu-id="58c1f-137">アプリケーションのタブ削除ページを作成する</span><span class="sxs-lookup"><span data-stu-id="58c1f-137">Create a tab removal page for your application</span></span>

<span data-ttu-id="58c1f-138">オプションの削除ページは、ホストする HTML ページであり、タブが削除されると表示されます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-138">The optional removal page is an HTML page that you host and is displayed when the tab is removed.</span></span> <span data-ttu-id="58c1f-139">削除ページの URL は、構成ページ `setSettings()` 内のメソッドによって指定されます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-139">The removal page URL is designated by the `setSettings()` method within your configuration page.</span></span> <span data-ttu-id="58c1f-140">アプリのすべてのページと同様に、削除ページはタブの前提条件に準拠[Teams必要があります](../../../tabs/how-to/tab-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="58c1f-140">As with all pages in your app, the removal page must comply with [Teams tab prerequisites](../../../tabs/how-to/tab-requirements.md).</span></span>

### <a name="register-a-remove-handler"></a><span data-ttu-id="58c1f-141">削除ハンドラーを登録する</span><span class="sxs-lookup"><span data-stu-id="58c1f-141">Register a remove handler</span></span>

<span data-ttu-id="58c1f-142">必要に応じて、削除ページ ロジック内で、ユーザーが既存のタブ構成を削除するときにイベント ハンドラー `registerOnRemoveHandler((RemoveEvent) => {}` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-142">Optionally, within your removal page logic, you can  invoke the `registerOnRemoveHandler((RemoveEvent) => {}` event handler when the user removes an existing tab configuration.</span></span> <span data-ttu-id="58c1f-143">ユーザーがコンテンツを削除しようとすると、メソッドはインターフェイスを取り込み、ハンドラーで [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) コードを実行します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-143">The method takes in the [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) interface and executes the code in the handler when a user attempts to remove content.</span></span> <span data-ttu-id="58c1f-144">このメソッドは、基になるリソースを削除してタブ コンテンツに電力を供給するなどのクリーンアップ操作を実行するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-144">The method is used to perform cleanup operations such as removing the underlying resource powering the tab content.</span></span> <span data-ttu-id="58c1f-145">一度に登録できる削除ハンドラーは 1 つのみです。</span><span class="sxs-lookup"><span data-stu-id="58c1f-145">At a time only one remove handler can be registered.</span></span>

<span data-ttu-id="58c1f-146">インターフェイス `RemoveEvent` は、2 つのメソッドを持つオブジェクトについて説明します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-146">The `RemoveEvent` interface describes an object with two methods:</span></span>

* <span data-ttu-id="58c1f-147">この `notifySuccess()` 関数は必須です。</span><span class="sxs-lookup"><span data-stu-id="58c1f-147">The `notifySuccess()` function is required.</span></span> <span data-ttu-id="58c1f-148">基になるリソースの削除が成功し、そのコンテンツを削除できると示します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-148">It indicates that the removal of the underlying resource succeeded and its content can be removed.</span></span>

* <span data-ttu-id="58c1f-149">この `notifyFailure(string)` 関数はオプションです。</span><span class="sxs-lookup"><span data-stu-id="58c1f-149">The `notifyFailure(string)` function is optional.</span></span> <span data-ttu-id="58c1f-150">基になるリソースの削除が失敗し、そのコンテンツを削除できないことを示します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-150">It indicates that removal of the underlying resource failed and its content cannot be removed.</span></span> <span data-ttu-id="58c1f-151">省略可能な文字列パラメーターは、エラーの理由を指定します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-151">The optional string parameter specifies a reason for the failure.</span></span> <span data-ttu-id="58c1f-152">指定されている場合、この文字列はユーザーに表示されます。それ以外の場合は、汎用エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-152">If provided, this string is displayed to the user; else a generic error is displayed.</span></span>

#### <a name="use-the-getsettings-function"></a><span data-ttu-id="58c1f-153">関数を使用 `getSettings()` する</span><span class="sxs-lookup"><span data-stu-id="58c1f-153">Use the `getSettings()` function</span></span>

<span data-ttu-id="58c1f-154">削除するタブ `getSettings()` コンテンツを割り当てる場合に使用できます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-154">You can use `getSettings()`to assign the tab content to be removed.</span></span> <span data-ttu-id="58c1f-155">この `getSettings((Settings) =>{})` 関数は、取得できる [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 有効な settings プロパティ値を取り込み、提供します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-155">The `getSettings((Settings) =>{})` function takes in the [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) and provides the valid settings property values that can be retrieved.</span></span>

#### <a name="use-the-getcontext-function"></a><span data-ttu-id="58c1f-156">関数を使用 `getContext()` する</span><span class="sxs-lookup"><span data-stu-id="58c1f-156">Use the `getContext()` function</span></span>

<span data-ttu-id="58c1f-157">フレームが実行 `getContext()` されている現在のコンテキストを取得するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-157">You can use `getContext()` to get the current context in which the frame is running.</span></span> <span data-ttu-id="58c1f-158">この `getContext((Context) =>{})` 関数は、 を取り込 [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) む。</span><span class="sxs-lookup"><span data-stu-id="58c1f-158">The `getContext((Context) =>{})` function takes in the [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="58c1f-159">この関数は、削除ページ ロジックで使用できる有効なプロパティ値を提供し、削除ページに表示するコンテンツ `Context` を決定します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-159">The function provides valid `Context` property values that you can use in your removal page logic to determine the content to display in the removal page.</span></span>

#### <a name="include-authentication"></a><span data-ttu-id="58c1f-160">認証を含める</span><span class="sxs-lookup"><span data-stu-id="58c1f-160">Include authentication</span></span>

<span data-ttu-id="58c1f-161">ユーザーがタブ コンテンツを削除するには、認証が必要です。</span><span class="sxs-lookup"><span data-stu-id="58c1f-161">Authentication is required before allowing a user to delete the tab content.</span></span> <span data-ttu-id="58c1f-162">コンテキスト情報は、認証要求と承認ページ URL の作成に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-162">Context information can be used to help construct authentication requests and authorization page URLs.</span></span> <span data-ttu-id="58c1f-163">タブについては[Microsoft Teamsの認証フローを参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="58c1f-163">See [Microsoft Teams authentication flow for tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="58c1f-164">タブ ページで使用されているドメインすべてが配列に一覧表示されます `manifest.json` `validDomains` 。</span><span class="sxs-lookup"><span data-stu-id="58c1f-164">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

<span data-ttu-id="58c1f-165">次に、タブの削除コード ブロックの例を示します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-165">The following is a sample tab removal code block:</span></span>

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

<span data-ttu-id="58c1f-166">ユーザーがタブのドロップダウン **メニューから**[削除] を選択すると、Teamsページに割り当てられている省略可能なページが `removeUrl` IFrame に読み込まれます。 </span><span class="sxs-lookup"><span data-stu-id="58c1f-166">When a user selects **Remove** from the tab's drop-down menu, Teams loads the optional `removeUrl` page assigned in your **configuration page**, into an IFrame.</span></span> <span data-ttu-id="58c1f-167">ユーザーには、削除ページ IFrame の下部に表示される [削除] ボタンを呼び出して有効にする関数が読み込まれたボタン `onClick()` `microsoftTeams.settings.setValidityState(true)` が表示されます。 </span><span class="sxs-lookup"><span data-stu-id="58c1f-167">The user is shown a button loaded with the `onClick()` function that calls `microsoftTeams.settings.setValidityState(true)` and enables the **Remove** button shown at the bottom of the removal page IFrame.</span></span>

<span data-ttu-id="58c1f-168">削除ハンドラーが実行された後、またはコンテンツのTeams `removeEvent.notifySuccess()` `removeEvent.notifyFailure()` 結果を通知します。</span><span class="sxs-lookup"><span data-stu-id="58c1f-168">After the remove handler is executed, `removeEvent.notifySuccess()` or `removeEvent.notifyFailure()` notifies Teams of the content removal outcome.</span></span>

>[!NOTE]
> * <span data-ttu-id="58c1f-169">承認されたユーザーによるタブの制御が禁止されなかTeams、成功と失敗の両方の場合にタブが削除されます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-169">To ensure that an authorized user's control over a tab is not inhibited, Teams removes the tab in both success and failure cases.</span></span>
> * <span data-ttu-id="58c1f-170">Teamsが呼び **出** されていない場合でも、5 秒後に [削除] ボタンを有効にします `setValidityState()` 。</span><span class="sxs-lookup"><span data-stu-id="58c1f-170">Teams enables the **Remove** button after five seconds, even if your tab has not called `setValidityState()`.</span></span>
> * <span data-ttu-id="58c1f-171">ユーザーが [削除] を選択するとTeamsが完了したかどうかに関係なく、30 秒後にタブが削除されます。</span><span class="sxs-lookup"><span data-stu-id="58c1f-171">When the user selects **Remove**, Teams removes the tab after 30 seconds regardless of whether the actions have been completed or not.</span></span>

## <a name="see-also"></a><span data-ttu-id="58c1f-172">関連項目</span><span class="sxs-lookup"><span data-stu-id="58c1f-172">See also</span></span>

* [<span data-ttu-id="58c1f-173">Teamsタブ</span><span class="sxs-lookup"><span data-stu-id="58c1f-173">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="58c1f-174">プライベート タブを作成する</span><span class="sxs-lookup"><span data-stu-id="58c1f-174">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* <span data-ttu-id="58c1f-175">[[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)</span><span class="sxs-lookup"><span data-stu-id="58c1f-175">[Create a channel or group tab](~/tabs/how-to/create-channel-group-tab.md)</span></span>
* [<span data-ttu-id="58c1f-176">構成ページを作成する</span><span class="sxs-lookup"><span data-stu-id="58c1f-176">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)

## <a name="next-step"></a><span data-ttu-id="58c1f-177">次の手順</span><span class="sxs-lookup"><span data-stu-id="58c1f-177">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="58c1f-178">モバイルのタブ</span><span class="sxs-lookup"><span data-stu-id="58c1f-178">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)