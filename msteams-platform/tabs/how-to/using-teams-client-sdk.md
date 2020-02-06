---
title: Teams クライアント SDK の使用
author: laujan
description: Teams クライアント SDK を使用して、ユーザー設定のタブに Teams 対応機能を追加する方法
keywords: teams タブグループチャネルの構成可能な静的 SDK JavaScript personal
ms.topic: conceptual
ms.openlocfilehash: eac5a8ec03ba12d926346afb40ca9bc6e9dda8d6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675104"
---
# <a name="using-the-teams-client-sdk"></a><span data-ttu-id="04a03-104">Teams クライアント SDK の使用</span><span class="sxs-lookup"><span data-stu-id="04a03-104">Using the Teams client SDK</span></span>

<span data-ttu-id="04a03-105">**Teams javascript クライアント SDK**および**teams javascript ライブラリ**は、 [Microsoft teams 開発者プラットフォーム](https://msdn.microsoft.com/microsoft-teams)の一部であり、teams アプリケーションの作成を容易にするツールとプロセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="04a03-105">The **Teams JavaScript client SDK**  and **Teams JavaScript Library** are part of the [Microsoft Teams developer platform](https://msdn.microsoft.com/microsoft-teams) and provide tools and processes to facilitate Teams application creation.</span></span> <span data-ttu-id="04a03-106">Teams クライアント SDK は、npm パッケージとして配布されます。</span><span class="sxs-lookup"><span data-stu-id="04a03-106">The Teams client SDK is distributed as an npm package.</span></span> <span data-ttu-id="04a03-107">最新バージョンについては、「 <https://www.npmjs.com/package/@microsoft/teams-js>」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="04a03-107">The latest version can be found here: <https://www.npmjs.com/package/@microsoft/teams-js>.</span></span> <span data-ttu-id="04a03-108">Teams ライブラリは、に<https://github.com/OfficeDev/microsoft-teams-library-js>あります。</span><span class="sxs-lookup"><span data-stu-id="04a03-108">The Teams Library is located at <https://github.com/OfficeDev/microsoft-teams-library-js>.</span></span>

<span data-ttu-id="04a03-109">次の表に、タブ開発で一般的に使用される Teams ライブラリ関数の概要を示します。</span><span class="sxs-lookup"><span data-stu-id="04a03-109">The following table outlines the Teams Library functions typically used in tabs development:</span></span>

## <a name="teams-sdk-public-api"></a><span data-ttu-id="04a03-110">Teams SDK パブリック API</span><span class="sxs-lookup"><span data-stu-id="04a03-110">Teams SDK public API</span></span> 

| <span data-ttu-id="04a03-111">関数</span><span class="sxs-lookup"><span data-stu-id="04a03-111">Function</span></span>  | <span data-ttu-id="04a03-112">説明</span><span class="sxs-lookup"><span data-stu-id="04a03-112">Description</span></span>          | <span data-ttu-id="04a03-113">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="04a03-113">Documentation</span></span>|
| -----     | -----     | -----    | -----        |
| `microsoftTeams.initialize()` | <span data-ttu-id="04a03-114">Teams ライブラリを初期化します。</span><span class="sxs-lookup"><span data-stu-id="04a03-114">Initializes the Teams library.</span></span> <span data-ttu-id="04a03-115">この関数は、他の SDK 呼び出しの前に呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="04a03-115">This function must be called before any other SDK calls.</span></span>|[<span data-ttu-id="04a03-116">function</span><span class="sxs-lookup"><span data-stu-id="04a03-116">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-)|
|`microsoftTeams.getContext(callback: (context: Context)`| <span data-ttu-id="04a03-117">ページが実行されている現在の状態を取得します。</span><span class="sxs-lookup"><span data-stu-id="04a03-117">Gets the current state in which the page is running.</span></span> <span data-ttu-id="04a03-118">コールバックは、**コンテキスト**オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="04a03-118">The callback retrieves the **Context** object.</span></span>|[<span data-ttu-id="04a03-119">function</span><span class="sxs-lookup"><span data-stu-id="04a03-119">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-)<br/>[<span data-ttu-id="04a03-120">context obj</span><span class="sxs-lookup"><span data-stu-id="04a03-120">context obj</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |<span data-ttu-id="04a03-121">ユーザーがタブの全画面表示/ウィンドウ表示を切り替えたときに登録されるハンドラー。</span><span class="sxs-lookup"><span data-stu-id="04a03-121">The handler that is registered when the user toggles a tab's full-screen/windowed view.</span></span>|[<span data-ttu-id="04a03-122">function</span><span class="sxs-lookup"><span data-stu-id="04a03-122">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-)<br/>[<span data-ttu-id="04a03-123">boolean</span><span class="sxs-lookup"><span data-stu-id="04a03-123">boolean</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest#isfullscreen)|
|`microsoftTeams.registerChangeSettingsHandler()` |<span data-ttu-id="04a03-124">ユーザーがタブを再構成するために [有効な**設定**] ボタンを選択したときに登録されるハンドラー。</span><span class="sxs-lookup"><span data-stu-id="04a03-124">The handler that is registered when the user selects the enabled **Settings** button to reconfigure a tab.</span></span>|[<span data-ttu-id="04a03-125">function</span><span class="sxs-lookup"><span data-stu-id="04a03-125">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |<span data-ttu-id="04a03-126">アプリによって所有されているタブを取得します。</span><span class="sxs-lookup"><span data-stu-id="04a03-126">Gets the tabs owned by the app.</span></span> <span data-ttu-id="04a03-127">コールバックは、 **Tabinformation**オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="04a03-127">The callback retrieves the **TabInformation** object.</span></span> <span data-ttu-id="04a03-128">**Tabinstanceparameters**オブジェクトは、省略可能なパラメーターです。</span><span class="sxs-lookup"><span data-stu-id="04a03-128">The **TabInstanceParameters** object is an optional parameter.</span></span>|[<span data-ttu-id="04a03-129">function</span><span class="sxs-lookup"><span data-stu-id="04a03-129">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-)<br/>[<span data-ttu-id="04a03-130">tabInfo obj</span><span class="sxs-lookup"><span data-stu-id="04a03-130">tabInfo obj</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|<span data-ttu-id="04a03-131">ユーザーに対して最後に使用されたタブを取得します。</span><span class="sxs-lookup"><span data-stu-id="04a03-131">Gets the most recently used tabs for the user.</span></span> <span data-ttu-id="04a03-132">コールバックは、 **Tabinformation**オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="04a03-132">The callback retrieves the **TabInformation** object.</span></span> <span data-ttu-id="04a03-133">**Tabinstanceparameters**オブジェクトは、省略可能なパラメーターです。</span><span class="sxs-lookup"><span data-stu-id="04a03-133">The **TabInstanceParameters** object is an optional parameter.</span></span>|[<span data-ttu-id="04a03-134">function</span><span class="sxs-lookup"><span data-stu-id="04a03-134">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-)<br/>[<span data-ttu-id="04a03-135">tabInfo obj</span><span class="sxs-lookup"><span data-stu-id="04a03-135">tabInfo obj</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.teaminformation?view=msteams-client-js-latest)<br/>[<span data-ttu-id="04a03-136">tabInstance obj</span><span class="sxs-lookup"><span data-stu-id="04a03-136">tabInstance obj</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|<span data-ttu-id="04a03-137">**DeepLinkParameters**オブジェクトを入力として受け取り、ユーザーが*タブ内の*コンテンツに移動するために使用できるディープリンクダイアログボックスを共有します。</span><span class="sxs-lookup"><span data-stu-id="04a03-137">Takes the **DeepLinkParameters** object as input and shares a deep link dialog box that a user can use to navigate to content *within the tab*.</span></span>|[<span data-ttu-id="04a03-138">function</span><span class="sxs-lookup"><span data-stu-id="04a03-138">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-)<br/>[<span data-ttu-id="04a03-139">ディープリンク obj</span><span class="sxs-lookup"><span data-stu-id="04a03-139">deepLink obj</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|<span data-ttu-id="04a03-140">必要な**ディープリンク**を入力として受け取り、ユーザーを URL に移動するか、または*チーム内の*アプリを開く、インストールするなどのクライアントアクションをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="04a03-140">Takes a required **deepLink** as input and navigates user to a URL or triggers a client action—such as opening or installing—an app *within Teams*.</span></span>|[<span data-ttu-id="04a03-141">function</span><span class="sxs-lookup"><span data-stu-id="04a03-141">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|<span data-ttu-id="04a03-142">**Tabinstance**オブジェクトを入力として受け取り、指定された tab インスタンスに移動します。</span><span class="sxs-lookup"><span data-stu-id="04a03-142">Takes the **TabInstance** object as input and navigates to a specified tab instance.</span></span>|[<span data-ttu-id="04a03-143">function</span><span class="sxs-lookup"><span data-stu-id="04a03-143">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-)<br/>[<span data-ttu-id="04a03-144">tabInstance obj</span><span class="sxs-lookup"><span data-stu-id="04a03-144">tabInstance obj</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest)|

## <a name="authentication-namespace"></a><span data-ttu-id="04a03-145">認証名前空間</span><span class="sxs-lookup"><span data-stu-id="04a03-145">Authentication namespace</span></span>

| <span data-ttu-id="04a03-146">関数</span><span class="sxs-lookup"><span data-stu-id="04a03-146">Function</span></span>  | <span data-ttu-id="04a03-147">説明</span><span class="sxs-lookup"><span data-stu-id="04a03-147">Description</span></span>          | <span data-ttu-id="04a03-148">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="04a03-148">Documentation</span></span>|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|<span data-ttu-id="04a03-149">呼び出し元によって提供されたパラメーターを使用して新しいウィンドウを開く認証要求を開始します。</span><span class="sxs-lookup"><span data-stu-id="04a03-149">Initiates an authentication request that opens a new window with the parameters provided by the caller.</span></span> <span data-ttu-id="04a03-150">オプションの入力値は、 **AuthenticateParameters**オブジェクトによって定義されます。</span><span class="sxs-lookup"><span data-stu-id="04a03-150">Optional input values are defined by the **AuthenticateParameters** object.</span></span>|[<span data-ttu-id="04a03-151">function</span><span class="sxs-lookup"><span data-stu-id="04a03-151">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#authenticate-authenticateparameters-)<br/>[<span data-ttu-id="04a03-152">auth obj</span><span class="sxs-lookup"><span data-stu-id="04a03-152">auth obj</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|<span data-ttu-id="04a03-153">認証要求を開始したフレームに、要求が成功したことを通知し、[認証] ウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="04a03-153">Notifies the frame that initiated the authentication request that the request was successful and closes the authentication window</span></span>|[<span data-ttu-id="04a03-154">function</span><span class="sxs-lookup"><span data-stu-id="04a03-154">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#notifysuccess-string--string-)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|<span data-ttu-id="04a03-155">認証要求を開始したフレームに、要求が失敗したことを通知し、認証ウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="04a03-155">Notifies the frame that initiated the authentication request that the request failed and closes the authentication window.</span></span>|[<span data-ttu-id="04a03-156">function</span><span class="sxs-lookup"><span data-stu-id="04a03-156">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#notifyfailure-string--string-)|

## <a name="settings-namespace"></a><span data-ttu-id="04a03-157">Settings 名前空間</span><span class="sxs-lookup"><span data-stu-id="04a03-157">Settings namespace</span></span>

| <span data-ttu-id="04a03-158">関数</span><span class="sxs-lookup"><span data-stu-id="04a03-158">Function</span></span>  | <span data-ttu-id="04a03-159">説明</span><span class="sxs-lookup"><span data-stu-id="04a03-159">Description</span></span>          | <span data-ttu-id="04a03-160">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="04a03-160">Documentation</span></span>|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|<span data-ttu-id="04a03-161">初期値は false です。</span><span class="sxs-lookup"><span data-stu-id="04a03-161">The initial value is false.</span></span> <span data-ttu-id="04a03-162">有効状態が true の場合、[**保存**] または [**削除**] ボタンをアクティブにします。</span><span class="sxs-lookup"><span data-stu-id="04a03-162">Activates the **Save** or **Remove** button when the validity state is true.</span></span>|[<span data-ttu-id="04a03-163">function</span><span class="sxs-lookup"><span data-stu-id="04a03-163">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#setvaliditystate-boolean-)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|<span data-ttu-id="04a03-164">現在のインスタンスの設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="04a03-164">Gets the settings for the current instance.</span></span> <span data-ttu-id="04a03-165">コールバックは、 **Settings**オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="04a03-165">The callback retrieves the **Settings** object.</span></span>|[<span data-ttu-id="04a03-166">function</span><span class="sxs-lookup"><span data-stu-id="04a03-166">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#getsettings--instancesettings--settings-----void-)<br/>[<span data-ttu-id="04a03-167">settings obj</span><span class="sxs-lookup"><span data-stu-id="04a03-167">settings obj</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|<span data-ttu-id="04a03-168">現在のインスタンスの設定を構成します。</span><span class="sxs-lookup"><span data-stu-id="04a03-168">Configures the settings for the current instance.</span></span> <span data-ttu-id="04a03-169">有効な設定は、 **settings**オブジェクトによって定義されます。</span><span class="sxs-lookup"><span data-stu-id="04a03-169">Valid settings are defined by the **Settings** object.</span></span>|[<span data-ttu-id="04a03-170">function</span><span class="sxs-lookup"><span data-stu-id="04a03-170">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#setsettings-settings-)<br/>[<span data-ttu-id="04a03-171">settings obj</span><span class="sxs-lookup"><span data-stu-id="04a03-171">settings obj</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|<span data-ttu-id="04a03-172">ユーザーが [**保存**] ボタンを選択したときに登録されるハンドラー。</span><span class="sxs-lookup"><span data-stu-id="04a03-172">The handler that is registered when the user selects the **Save** button.</span></span> <span data-ttu-id="04a03-173">このハンドラーは、コンテンツを電源にする基礎となるリソースを作成または更新するために使用します。</span><span class="sxs-lookup"><span data-stu-id="04a03-173">This handler should be used to create or update the underlying resource powering the content.</span></span>|[<span data-ttu-id="04a03-174">function</span><span class="sxs-lookup"><span data-stu-id="04a03-174">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#registeronsavehandler--evt--saveevent-----void-)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|<span data-ttu-id="04a03-175">ユーザーが [**削除**] ボタンを選択したときに登録されるハンドラー。</span><span class="sxs-lookup"><span data-stu-id="04a03-175">The handler that is registered when the user selects the **Remove** button.</span></span> <span data-ttu-id="04a03-176">このハンドラーを使用して、コンテンツを電源にしている基になっているリソースを削除します。</span><span class="sxs-lookup"><span data-stu-id="04a03-176">This handler should be used to remove the underlying resource powering the content.</span></span>|[<span data-ttu-id="04a03-177">function</span><span class="sxs-lookup"><span data-stu-id="04a03-177">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#registeronremovehandler--evt--removeevent-----void-)|

## <a name="tasks-namespace"></a><span data-ttu-id="04a03-178">Tasks 名前空間</span><span class="sxs-lookup"><span data-stu-id="04a03-178">Tasks namespace</span></span>

| <span data-ttu-id="04a03-179">関数</span><span class="sxs-lookup"><span data-stu-id="04a03-179">Function</span></span>  | <span data-ttu-id="04a03-180">説明</span><span class="sxs-lookup"><span data-stu-id="04a03-180">Description</span></span>          | <span data-ttu-id="04a03-181">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="04a03-181">Documentation</span></span>|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|<span data-ttu-id="04a03-182">**Taskinfo**オブジェクトを入力として受け取り、アプリでタスクモジュールを開くことができるようにします。</span><span class="sxs-lookup"><span data-stu-id="04a03-182">Takes the **TaskInfo** object as input and allows an app to open the task module.</span></span> <span data-ttu-id="04a03-183">オプションの**Submithandler**は、タスクモジュールが完了するときに登録されます。</span><span class="sxs-lookup"><span data-stu-id="04a03-183">The optional **submitHandler** is registered when the task module is completed.</span></span> |[<span data-ttu-id="04a03-184">function</span><span class="sxs-lookup"><span data-stu-id="04a03-184">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#starttask-taskinfo---err--string--result--string-----void-)<br/>[<span data-ttu-id="04a03-185">taskInfo obj</span><span class="sxs-lookup"><span data-stu-id="04a03-185">taskInfo obj</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|<span data-ttu-id="04a03-186">タスクモジュールを送信します。</span><span class="sxs-lookup"><span data-stu-id="04a03-186">Submits the task module.</span></span> <span data-ttu-id="04a03-187">省略可能な**result** string パラメーターは、ボットまたはアプリに送信される結果で、通常は JSON オブジェクトまたはシリアル化です。省略可能な**Appids**文字列または文字列配列パラメーターは、呼び出しがタスクモジュールを起動したものと同じ appId から発信されたことを検証するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="04a03-187">The optional **result** string parameter is the result sent to the bot or the app and is typically a JSON object or serialization; The optional **appIds** string or string array parameter aids in validating that the call originated from the same appId as the one that invoked the task module.</span></span>|[<span data-ttu-id="04a03-188">function</span><span class="sxs-lookup"><span data-stu-id="04a03-188">function</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---)|