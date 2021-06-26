---
title: タスク モジュールの呼び出しと終了
description: タスク モジュールを呼び出して閉じる。
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: a23d5cee3f13967772a4b58ed973bf08906e36a6
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140779"
---
# <a name="invoke-and-dismiss-task-modules"></a><span data-ttu-id="5a0f1-103">タスク モジュールの呼び出しと終了</span><span class="sxs-lookup"><span data-stu-id="5a0f1-103">Invoke and dismiss task modules</span></span>

<span data-ttu-id="5a0f1-104">タスク モジュールは、タブ、ボット、またはディープ リンクから呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-104">Task modules can be invoked from tabs, bots, or deep links.</span></span> <span data-ttu-id="5a0f1-105">応答は、HTML、JavaScript、またはアダプティブ カードのいずれかです。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-105">The response can be either in HTML, JavaScript, or as an Adaptive Card.</span></span> <span data-ttu-id="5a0f1-106">タスク モジュールの呼び出し方法と、ユーザーの操作の応答に対処する方法に関して、多くの柔軟性があります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-106">There is a lot of flexibility in terms of how task modules are invoked and how to deal with the response of the user's interaction.</span></span> <span data-ttu-id="5a0f1-107">次の表に、この動作の概要を示します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-107">The following table summarizes how this works:</span></span>

| <span data-ttu-id="5a0f1-108">using を使用して呼び出される</span><span class="sxs-lookup"><span data-stu-id="5a0f1-108">Invoked using</span></span> | <span data-ttu-id="5a0f1-109">HTML または JavaScript のタスク モジュール</span><span class="sxs-lookup"><span data-stu-id="5a0f1-109">Task module with HTML or JavaScript</span></span> | <span data-ttu-id="5a0f1-110">アダプティブ カード付きタスク モジュール</span><span class="sxs-lookup"><span data-stu-id="5a0f1-110">Task module with Adaptive Card</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a0f1-111">タブ内の JavaScript</span><span class="sxs-lookup"><span data-stu-id="5a0f1-111">JavaScript in a tab</span></span> | <span data-ttu-id="5a0f1-112">1. オプションのコールバック関数Teamsクライアント SDK `tasks.startTask()` 関数を `submitHandler(err, result)` 使用します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-112">1. Use the Teams client SDK function `tasks.startTask()` with an optional `submitHandler(err, result)` callback function.</span></span> <br/><br/> <span data-ttu-id="5a0f1-113">2. タスク モジュール コードで、ユーザーがアクションを実行した場合、Teams SDK 関数をパラメーターとして `tasks.submitTask()` `result` 呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-113">2. In the task module code, when the user has performed the actions, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="5a0f1-114">でコールバック `submitHandler` を指定した `tasks.startTask()` 場合、Teamsパラメーターとして `result` 呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-114">If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with `result` as a parameter.</span></span> <span data-ttu-id="5a0f1-115">呼び出し時にエラーが発生した場合は、代わりに文字列 `tasks.startTask()` `submitHandler` で関数 `err` が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-115">If there was an error when invoking `tasks.startTask()`, the `submitHandler` function is called with an `err` string instead.</span></span> <br/><br/> <span data-ttu-id="5a0f1-116">3. 呼び出し時に a `completionBotId` を指定できます `teams.startTask()` 。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-116">3. You can also specify a `completionBotId` when calling `teams.startTask()`.</span></span> <span data-ttu-id="5a0f1-117">その後 `result` 、代わりにボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-117">Then the `result` is sent to the bot instead.</span></span> | <span data-ttu-id="5a0f1-118">1. TaskInfo オブジェクトTeams、タスク モジュールポップアップに表示するアダプティブ カードの JSON を含むクライアント SDK 関数を呼び `tasks.startTask()` [](#the-taskinfo-object) `TaskInfo.card` 出します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-118">1. Call the Teams client SDK function `tasks.startTask()` with a [TaskInfo object](#the-taskinfo-object) and `TaskInfo.card` containing the JSON for the Adaptive Card to show in the task module pop-up.</span></span> <br/><br/> <span data-ttu-id="5a0f1-119">2. でコールバックを指定した場合、Teams は、呼び出し時にエラーが発生した場合、または右上の `submitHandler` `tasks.startTask()` `err` `tasks.startTask()` X を使用してタスク モジュールポップアップを閉じる場合に、文字列で呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-119">2. If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with an `err` string, if there was an error when invoking `tasks.startTask()` or if the user closes the task module pop-up using the X at the upper right.</span></span> <br/><br/> <span data-ttu-id="5a0f1-120">3. ユーザーがボタンを押すと、オブジェクトがの値 `Action.Submit` `data` として返されます `result` 。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-120">3. If the user presses an `Action.Submit` button then its `data` object is returned as the value of `result`.</span></span> |
| <span data-ttu-id="5a0f1-121">ボット カード ボタン</span><span class="sxs-lookup"><span data-stu-id="5a0f1-121">Bot card button</span></span> | <span data-ttu-id="5a0f1-122">1. ボット カード ボタンは、ボタンの種類に応じて、ディープ リンク URL またはメッセージを送信する 2 つの方法でタスク モジュールを呼び出 `task/fetch` します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-122">1. Bot card buttons, depending on the type of button, can invoke task modules in two ways, a deep link URL or by sending a `task/fetch` message.</span></span> <br/><br/> <span data-ttu-id="5a0f1-123">2. ボタンのアクションがアダプティブ カードのボタンの種類である場合、HTTP POST であるイベント `type` `task/fetch` `Action.Submit` `task/fetch invoke` がボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-123">2. If the button's action `type` is `task/fetch` that is `Action.Submit` button type for Adaptive Cards, a `task/fetch invoke` event that is an HTTP POST is sent to the bot.</span></span> <span data-ttu-id="5a0f1-124">ボットは、HTTP 200 で POST に応答し、TaskInfo オブジェクトのラッパーを含む [応答本文に応答します](#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-124">The bot responds to the POST with HTTP 200 and the response body containing a wrapper around the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="5a0f1-125">詳細については、「を使用して[タスク モジュールを呼 `task/fetch` び出す」を参照してください](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch)。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-125">For more information, see [invoking a task module using `task/fetch`](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch).</span></span> <span data-ttu-id="5a0f1-126">Teamsタスク モジュールを表示します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-126">Teams displays the task module.</span></span> <br/><br/> <span data-ttu-id="5a0f1-127">3. ユーザーがアクションを実行した後、オブジェクトをパラメーター Teams SDK `tasks.submitTask()` `result` 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-127">3. After the user has performed the actions, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="5a0f1-128">ボットは、オブジェクト `task/submit invoke` を含むメッセージを受信 `result` します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-128">The bot receives a `task/submit invoke` message that contains the `result` object.</span></span> <br/><br/> <span data-ttu-id="5a0f1-129">4. メッセージに応答するには、タスクが正常に完了した何もしないか、ポップアップ ウィンドウでユーザーにメッセージを表示するか、別のタスク モジュール ウィンドウを呼び出して、メッセージに応答する 3 つの異なる方法 `task/submit` があります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-129">4. You have three different ways to respond to the `task/submit` message, by doing nothing that is the task completed successfully, by displaying a message to the user in a pop-up window, or by invoking another task module window.</span></span> <span data-ttu-id="5a0f1-130">詳細については、「に関[する詳細な説明 `task/submit` 」を参照してください](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-130">For more information, see [detailed discussion on `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> | <ul><li> <span data-ttu-id="5a0f1-131">Bot Framework カードのボタンと同様に、アダプティブ カードのボタンは、タスク モジュールの呼び出し、ボタンによるディープ リンク URL、およびボタンの使用の 2 つの方法を `Action.openUrl` `task/fetch` `Action.Submit` サポートします。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-131">Like buttons on Bot Framework cards, buttons on Adaptive Cards support two ways of invoking task modules, deep link URLs with `Action.openUrl` buttons, and `task/fetch` using `Action.Submit` buttons.</span></span> </li></ul> <br/><br/> <ul><li> <span data-ttu-id="5a0f1-132">アダプティブ カードを使用するタスク モジュールは、HTML または JavaScript の場合と非常に似て動作します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-132">Task modules with Adaptive Cards work very similarly to the HTML or JavaScript case.</span></span> <span data-ttu-id="5a0f1-133">主な違いは、アダプティブ カードを使用している場合は JavaScript が無いから、呼び出す方法がない点です `tasks.submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-133">The major difference is that since there is no JavaScript when you are using Adaptive Cards, there is no way to call `tasks.submitTask()`.</span></span> <span data-ttu-id="5a0f1-134">代わりに、Teamsオブジェクトを取得し、 `data` `Action.Submit` イベントのペイロードとして返 `task/submit` します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-134">Instead, Teams takes the `data` object from `Action.Submit` and returns it as the payload of the `task/submit` event.</span></span> <span data-ttu-id="5a0f1-135">詳細については、「の柔軟性[」を参照 `task/submit` してください](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-135">For more information, see [flexibility of `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> </li></ul> |
| <span data-ttu-id="5a0f1-136">ディープ リンク URL</span><span class="sxs-lookup"><span data-stu-id="5a0f1-136">Deep link URL</span></span> <br/>[<span data-ttu-id="5a0f1-137">URL 構文</span><span class="sxs-lookup"><span data-stu-id="5a0f1-137">URL syntax</span></span>](#task-module-deep-link-syntax) | <span data-ttu-id="5a0f1-138">1. Teams、ディープ リンクのパラメーターで指定された内部に表示される URL であるタスク モジュール `<iframe>` `url` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-138">1. Teams invokes the task module that is the URL that appears inside the `<iframe>` specified in the `url` parameter of the deep link.</span></span> <span data-ttu-id="5a0f1-139">コールバック `submitHandler` はありません。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-139">There is no `submitHandler` callback.</span></span> <br/><br/> <span data-ttu-id="5a0f1-140">2. タスク モジュール内のページの JavaScript 内で、タブまたはボット カード ボタンから呼び出す場合と同じように、オブジェクトをパラメーターとして呼び出して閉じます `tasks.submitTask()` `result` 。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-140">2. Within the JavaScript of the page in the task module, call `tasks.submitTask()` to close it with a `result` object as a parameter, the same as when invoking it from a tab or a bot card button.</span></span> <span data-ttu-id="5a0f1-141">ただし、完了ロジックは若干異なります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-141">However, completion logic is slightly different.</span></span> <span data-ttu-id="5a0f1-142">完了ロジックがボットがない場合は、クライアントに存在する場合、コールバックは存在しないので、完了ロジックは呼び出しの前のコードに `submitHandler` 存在する必要があります `tasks.submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-142">If your completion logic resides on the client that is if there is no bot, there is no `submitHandler` callback, so any completion logic must be in the code preceding the call to `tasks.submitTask()`.</span></span> <span data-ttu-id="5a0f1-143">呼び出しエラーは、コンソールを通じてのみ報告されます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-143">Invocation errors are only reported through the console.</span></span> <span data-ttu-id="5a0f1-144">ボットがある場合は、ディープ リンクでパラメーターを指定して、イベントを介して `completionBotId` `result` オブジェクトを送信 `task/submit` できます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-144">If you have a bot, then you can specify a `completionBotId` parameter in the deep link to send the `result` object through a `task/submit` event.</span></span> | <span data-ttu-id="5a0f1-145">1. Teams、ディープ リンクのパラメーターの URL エンコード値として指定されたアダプティブ カードの JSON カード本文であるタスク モジュールを `card` 呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-145">1. Teams invokes the task module that is the JSON card body of the Adaptive Card that is specified as a URL-encoded value of the `card` parameter of the deep link.</span></span> <br/><br/> <span data-ttu-id="5a0f1-146">2. ユーザーは、タスク モジュールの右上にある X を選択するか、カードのボタンを押してタスク モジュール `Action.Submit` を閉じます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-146">2. The user closes the task module by selecting the X at the upper right of the task module or by pressing an `Action.Submit` button on the card.</span></span> <span data-ttu-id="5a0f1-147">呼び出す必要が無い場合、ユーザーはアダプティブ カード フィールドの値を送信するボット `submitHandler` を持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-147">Since there is no `submitHandler` to call, the user must have a bot to send the value of the Adaptive Card fields.</span></span> <span data-ttu-id="5a0f1-148">ユーザーはディープ リンクのパラメーターを使用して、イベントを使用してデータを送信するボット `completionBotId` を指定する必要 `task/submit invoke` があります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-148">The user must use the `completionBotId` parameter in the deep link to specify the bot to send the data to using a `task/submit invoke` event.</span></span> |

> [!NOTE]
> <span data-ttu-id="5a0f1-149">JavaScript からタスク モジュールを呼び出す操作は、モバイルではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-149">Invoking a task module from JavaScript is not supported on mobile.</span></span>

<span data-ttu-id="5a0f1-150">次のセクションでは、タスク `TaskInfo` モジュールの特定の属性を定義するオブジェクトを指定します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-150">The next section specifies the `TaskInfo` object that defines certain attributes for a task module.</span></span>

## <a name="the-taskinfo-object"></a><span data-ttu-id="5a0f1-151">TaskInfo オブジェクト</span><span class="sxs-lookup"><span data-stu-id="5a0f1-151">The TaskInfo object</span></span>

<span data-ttu-id="5a0f1-152">オブジェクト `TaskInfo` には、タスク モジュールのメタデータが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-152">The `TaskInfo` object contains the metadata for a task module.</span></span> <span data-ttu-id="5a0f1-153">埋め `url` 込み iFrame 用またはアダプティブ `card` カード用に定義します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-153">Define the `url` for an embedded iFrame or `card` for an Adaptive Card.</span></span> <span data-ttu-id="5a0f1-154">次の表に、オブジェクト定義を示します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-154">The following table provides the object definition:</span></span>

| <span data-ttu-id="5a0f1-155">属性</span><span class="sxs-lookup"><span data-stu-id="5a0f1-155">Attribute</span></span> | <span data-ttu-id="5a0f1-156">種類</span><span class="sxs-lookup"><span data-stu-id="5a0f1-156">Type</span></span> | <span data-ttu-id="5a0f1-157">説明</span><span class="sxs-lookup"><span data-stu-id="5a0f1-157">Description</span></span> |
| --- | --- | --- |
| `title` | <span data-ttu-id="5a0f1-158">string</span><span class="sxs-lookup"><span data-stu-id="5a0f1-158">string</span></span> | <span data-ttu-id="5a0f1-159">この属性は、アプリ名の下とアプリ アイコンの右側に表示されます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-159">This attribute appears below the app name and to the right of the app icon.</span></span> |
| `height` | <span data-ttu-id="5a0f1-160">number または string</span><span class="sxs-lookup"><span data-stu-id="5a0f1-160">number or string</span></span> | <span data-ttu-id="5a0f1-161">この属性には、タスク モジュールの高さをピクセル単位で表す数値、または `small` 、 `medium` 、 を指定できます `large` 。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-161">This attribute can be a number representing the task module's height in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="5a0f1-162">詳細については、「タスク モジュールの [サイズ変更」を参照してください](#task-module-sizing)。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-162">For more information, see [task module sizing](#task-module-sizing).</span></span> |
| `width` | <span data-ttu-id="5a0f1-163">number または string</span><span class="sxs-lookup"><span data-stu-id="5a0f1-163">number or string</span></span> | <span data-ttu-id="5a0f1-164">この属性には、タスク モジュールの幅をピクセル単位で表す数値、または `small` 、 `medium` 、 を指定できます `large` 。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-164">This attribute can be a number representing the task module's width in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="5a0f1-165">詳細については、「タスク モジュールの [サイズ変更」を参照してください](#task-module-sizing)。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-165">For more information, see [task module sizing](#task-module-sizing).</span></span> |
| `url` | <span data-ttu-id="5a0f1-166">string</span><span class="sxs-lookup"><span data-stu-id="5a0f1-166">string</span></span> | <span data-ttu-id="5a0f1-167">この属性は、タスク モジュール内に読み込まれるページ `<iframe>` の URL です。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-167">This attribute is the URL of the page loaded as an `<iframe>` inside the task module.</span></span> <span data-ttu-id="5a0f1-168">URL のドメインは、アプリのマニフェスト内の [アプリの validDomains](~/resources/schema/manifest-schema.md#validdomains) 配列内にある必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-168">The URL's domain must be in the app's [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in your app's manifest.</span></span> |
| `card` | <span data-ttu-id="5a0f1-169">アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル</span><span class="sxs-lookup"><span data-stu-id="5a0f1-169">Adaptive Card or Adaptive Card bot card attachment</span></span> | <span data-ttu-id="5a0f1-170">この属性は、アダプティブ カードがタスク モジュールに表示される JSON です。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-170">This attribute is the JSON for the Adaptive Card to appear in the task module.</span></span> <span data-ttu-id="5a0f1-171">ユーザーがボットから呼び出す場合は、Bot Framework オブジェクトでアダプティブ カード JSON を使用 `attachment` します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-171">If the user is invoking from a bot, use the Adaptive Card JSON in a Bot Framework `attachment` object.</span></span> <span data-ttu-id="5a0f1-172">タブから、ユーザーはアダプティブ カードを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-172">From a tab, the user must use an Adaptive Card.</span></span> <span data-ttu-id="5a0f1-173">詳細については、「アダプティブ カード [またはアダプティブ カード ボット カードの添付ファイル」を参照してください。](#adaptive-card-or-adaptive-card-bot-card-attachment)</span><span class="sxs-lookup"><span data-stu-id="5a0f1-173">For more information, see [Adaptive Card or Adaptive Card bot card attachment](#adaptive-card-or-adaptive-card-bot-card-attachment)</span></span> |
| `fallbackUrl` | <span data-ttu-id="5a0f1-174">string</span><span class="sxs-lookup"><span data-stu-id="5a0f1-174">string</span></span> | <span data-ttu-id="5a0f1-175">この属性は、クライアントがタスク モジュール機能をサポートしていない場合、ブラウザー タブで URL を開きます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-175">This attribute opens the URL in a browser tab, if a client does not support the task module feature.</span></span> |
| `completionBotId` | <span data-ttu-id="5a0f1-176">string</span><span class="sxs-lookup"><span data-stu-id="5a0f1-176">string</span></span> | <span data-ttu-id="5a0f1-177">この属性は、ユーザーがタスク モジュールとやり取りした結果を送信するボット アプリ ID を指定します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-177">This attribute specifies a bot App ID to send the result of the user's interaction with the task module.</span></span> <span data-ttu-id="5a0f1-178">指定した場合、ボットはイベント ペイロード `task/submit invoke` に JSON オブジェクトを含むイベントを受信します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-178">If specified, the bot receives a `task/submit invoke` event with a JSON object in the event payload.</span></span> |

> [!NOTE]
> <span data-ttu-id="5a0f1-179">タスク モジュール機能では、読み込む URL のドメインがアプリのマニフェストの配列 `validDomains` に含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-179">The task module feature requires that the domains of any URLs you want to load are included in the `validDomains` array in your app's manifest.</span></span>

<span data-ttu-id="5a0f1-180">次のセクションでは、ユーザーがタスク モジュールの高さと幅を設定できるタスク モジュールのサイズ変更を指定します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-180">The next section specifies task module sizing that enables the user to set the height and width of the task module.</span></span>

## <a name="task-module-sizing"></a><span data-ttu-id="5a0f1-181">タスク モジュールのサイズ変更</span><span class="sxs-lookup"><span data-stu-id="5a0f1-181">Task module sizing</span></span>

<span data-ttu-id="5a0f1-182">の整数を使用 `TaskInfo.width` `TaskInfo.height` して、タスク モジュールの高さと幅をピクセル単位で設定します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-182">Using integers for `TaskInfo.width` and `TaskInfo.height`, sets the height and width of the task module in pixels.</span></span> <span data-ttu-id="5a0f1-183">ただし、チームのウィンドウのサイズと画面の解像度に応じて、縦横比 (幅または高さ) を維持しながら、比例して縮小されます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-183">However, depending on the size of the Team's window and screen resolution they are reduced proportionally while maintaining the aspect ratio that is width or height.</span></span>

<span data-ttu-id="5a0f1-184">次の図の赤い四角形のサイズは、次の画像の場合 `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` 、20%、50%、および 60% の使用可能な領域と `width` 20%、50%、および 66% `height` の比率です。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-184">If `TaskInfo.width` and `TaskInfo.height` are `"small"`, `"medium"`, or `"large"`, the size of the red rectangle in the following image is a proportion of the available space, 20%, 50%, and 60% for `width` and 20%, 50%, and 66% for `height`:</span></span>

![タスク モジュールの例](~/assets/images/task-module/task-module-example.png)

<span data-ttu-id="5a0f1-186">タブから呼び出されるタスク モジュールは、動的にサイズを変更できます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-186">Task modules invoked from a tab can be dynamically resized.</span></span> <span data-ttu-id="5a0f1-187">呼び出し後、newSize オブジェクトの高さと幅のプロパティが TaskInfo の仕様に準拠している場所 `tasks.startTask()` `tasks.updateTask(newSize)` を呼び出します `{ height: 'medium', width: 'medium' }` 。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-187">After calling `tasks.startTask()` you can call `tasks.updateTask(newSize)` where height and width properties on the newSize object conform to the TaskInfo specification, for example `{ height: 'medium', width: 'medium' }`.</span></span>

<span data-ttu-id="5a0f1-188">次のセクションでは、YouTube ビデオと PowerApp にタスク モジュールを埋め込む例を示します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-188">The next section provides examples of embedding task modules in a YouTube video and a PowerApp.</span></span>

## <a name="task-module-css-for-html-or-javascript-task-modules"></a><span data-ttu-id="5a0f1-189">HTML または JavaScript タスク モジュールのタスク モジュール CSS</span><span class="sxs-lookup"><span data-stu-id="5a0f1-189">Task module CSS for HTML or JavaScript task modules</span></span>

<span data-ttu-id="5a0f1-190">HTML または JavaScript ベースのタスク モジュールは、ヘッダーの下のタスク モジュールの領域全体にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-190">HTML or JavaScript-based task modules have access to the entire area of the task module below the header.</span></span> <span data-ttu-id="5a0f1-191">多くの柔軟性を提供しますが、ヘッダー要素に合わせてエッジをパディングし、不要なスクロール バーを回避する場合は、適切な CSS を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-191">While that offers a great deal of flexibility, if you want padding around the edges to align with the header elements and avoid unnecessary scroll bars, the user must provide the right CSS.</span></span> <span data-ttu-id="5a0f1-192">次のセクションでは、いくつかの使用例の例を示します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-192">The next sections provide some examples for a few use cases.</span></span>

<span data-ttu-id="5a0f1-193">**例 1: YouTube ビデオ**</span><span class="sxs-lookup"><span data-stu-id="5a0f1-193">**Example 1: YouTube video**</span></span>

<span data-ttu-id="5a0f1-194">YouTube では、Web ページにビデオを埋め込む機能が提供されています。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-194">YouTube offers the ability to embed videos on web pages.</span></span> <span data-ttu-id="5a0f1-195">簡単なスタブ Web ページを使用して、タスク モジュール内の Web ページにビデオを埋め込むのは簡単です。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-195">It is easy to embed videos on web pages in a task module using a simple stub web page.</span></span>

![YouTube ビデオ](~/assets/images/task-module/youtube-example.png)

<span data-ttu-id="5a0f1-197">次のコードは、CSS のない Web ページの HTML の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-197">The following code provides an example of the HTML for the web page without the CSS:</span></span>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  ⋮
</head>
<body>
  <div id="embed-container">
    <iframe width="1000" height="700" src="https://www.youtube.com/embed/rd0Rd8w3FZ0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen=""></iframe>
  </div>
</body>
</html>
```

<span data-ttu-id="5a0f1-198">次のコードは、CSS の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-198">The following code provides an example of the CSS:</span></span>

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 95%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

<span data-ttu-id="5a0f1-199">**例 2: PowerApp**</span><span class="sxs-lookup"><span data-stu-id="5a0f1-199">**Example 2: PowerApp**</span></span>

<span data-ttu-id="5a0f1-200">ユーザーは、PowerApp を埋め込む場合にも同じ方法を使用できます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-200">The user can use the same approach to embed a PowerApp as well.</span></span> <span data-ttu-id="5a0f1-201">個々の PowerApp の高さまたは幅をカスタマイズできるので、ユーザーは高さと幅を調整して、目的のプレゼンテーションを実現できます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-201">As the height or width of any individual PowerApp is customizable, the user can adjust the height and width to achieve the desired presentation.</span></span>

![アセット管理 PowerApp](~/assets/images/task-module/powerapp-example.png)

<span data-ttu-id="5a0f1-203">次のコードは、PowerApp の HTML の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-203">The following code provides an example of the HTML for PowerApp:</span></span>

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

<span data-ttu-id="5a0f1-204">次のコードは、CSS の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-204">The following code provides an example of the CSS:</span></span>

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 94%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

<span data-ttu-id="5a0f1-205">次のセクションでは、アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイルを使用してカードを呼び出す方法の詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-205">The next section provides details on invoking your card using Adaptive Card or Adaptive Card bot card attachment.</span></span>

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a><span data-ttu-id="5a0f1-206">アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル</span><span class="sxs-lookup"><span data-stu-id="5a0f1-206">Adaptive Card or Adaptive Card bot card attachment</span></span>

<span data-ttu-id="5a0f1-207">呼び出し方法に応じて、アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル (添付ファイル オブジェクトにラップされたアダプティブ カード) を使用する `card` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-207">Depending on how you are invoking your `card`, you must use either an Adaptive Card or an Adaptive Card bot card attachment, which is an Adaptive Card wrapped in an attachment object.</span></span>

<span data-ttu-id="5a0f1-208">タブから呼び出す場合、ユーザーはアダプティブ カードを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-208">When you are invoking from a tab, the user must use an Adaptive Card.</span></span>

<span data-ttu-id="5a0f1-209">次のコードは、アダプティブ カードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-209">The following code provides an example of an Adaptive Card:</span></span>

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "text": "Here is a ninja cat:"
        },
        {
            "type": "Image",
            "url": "http://adaptivecards.io/content/cats/1.png",
            "size": "Medium"
        }
    ],
    "version": "1.0"
}
```

<span data-ttu-id="5a0f1-210">次のコードは、ボットから呼び出す際のアダプティブ カード ボット カードの添付ファイルの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-210">The following code provides an example of an Adaptive Card bot card attachment when you are invoking from a bot:</span></span>

```json
{
    "contentType": "application/vnd.microsoft.card.adaptive",
    "content": {
        "type": "AdaptiveCard",
        "body": [
            {
                "type": "TextBlock",
                "text": "Here is a ninja cat:"
            },
            {
                "type": "Image",
                "url": "http://adaptivecards.io/content/cats/1.png",
                "size": "Medium"
            }
        ],
        "version": "1.0"
    }
}
```

<span data-ttu-id="5a0f1-211">次のセクションでは、オブジェクトと . を含むタスク モジュールのディープ リンク `TaskInfo` 構文の詳細について `APP_ID` 説明します `BOT_APP_ID` 。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-211">The next section provides details on task module deep link syntax including the `TaskInfo` object and `APP_ID` and `BOT_APP_ID`.</span></span>

## <a name="task-module-deep-link-syntax"></a><span data-ttu-id="5a0f1-212">タスク モジュールのディープ リンク構文</span><span class="sxs-lookup"><span data-stu-id="5a0f1-212">Task module deep link syntax</span></span>

<span data-ttu-id="5a0f1-213">タスク モジュールのディープ リンクは、TaskInfo オブジェクトのシリアル化であり、他の 2 つの詳細と、必要に応じて `APP_ID` 、 `BOT_APP_ID`</span><span class="sxs-lookup"><span data-stu-id="5a0f1-213">A task module deep link is a serialization of the TaskInfo object with the following two other details, `APP_ID` and optionally the `BOT_APP_ID`:</span></span>

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

<span data-ttu-id="5a0f1-214">、、、のデータ型と許容値については `<TaskInfo.url>` `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` [、TaskInfo オブジェクトを参照してください](#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-214">For the data types and allowable values for `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`, and `<TaskInfo.title>`, see [TaskInfo object](#the-taskinfo-object).</span></span>

> [!TIP]
> <span data-ttu-id="5a0f1-215">URL は、JavaScript の関数など、パラメーターを使用する場合にディープ リンク `card` をエンコード[ `encodeURI()` します](https://www.w3schools.com/jsref/jsref_encodeURI.asp)。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-215">URL encode the deep link when using the `card` parameter, for example, JavaScript's [`encodeURI()` function](https://www.w3schools.com/jsref/jsref_encodeURI.asp).</span></span>

<span data-ttu-id="5a0f1-216">次の表に、以下の情報を `APP_ID` 示します `BOT_APP_ID` 。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-216">The following table provides information on `APP_ID` and `BOT_APP_ID`:</span></span>

| <span data-ttu-id="5a0f1-217">値</span><span class="sxs-lookup"><span data-stu-id="5a0f1-217">Value</span></span> | <span data-ttu-id="5a0f1-218">型</span><span class="sxs-lookup"><span data-stu-id="5a0f1-218">Type</span></span> | <span data-ttu-id="5a0f1-219">必須</span><span class="sxs-lookup"><span data-stu-id="5a0f1-219">Required</span></span> | <span data-ttu-id="5a0f1-220">説明</span><span class="sxs-lookup"><span data-stu-id="5a0f1-220">Description</span></span> |
| --- | --- | --- | --- |
| `APP_ID` | <span data-ttu-id="5a0f1-221">string</span><span class="sxs-lookup"><span data-stu-id="5a0f1-221">string</span></span> | <span data-ttu-id="5a0f1-222">はい</span><span class="sxs-lookup"><span data-stu-id="5a0f1-222">Yes</span></span> | <span data-ttu-id="5a0f1-223">タスク [モジュール](~/resources/schema/manifest-schema.md#id) を呼び出すアプリの ID。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-223">The [ID](~/resources/schema/manifest-schema.md#id) of the app invoking the task module.</span></span> <span data-ttu-id="5a0f1-224">マニフェスト [の validDomains 配列](~/resources/schema/manifest-schema.md#validdomains) には、URL に if の `APP_ID` `url` ドメイン `url` が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-224">The [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in the manifest for `APP_ID` must contain the domain for `url` if `url` is in the URL.</span></span> <span data-ttu-id="5a0f1-225">アプリ ID は、タブまたはボットからタスク モジュールを呼び出す際に既に知られているので、 に含まれません `TaskInfo` 。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-225">The app ID is already known when a task module is invoked from a tab or a bot, which is why it is not included in `TaskInfo`.</span></span> |
| `BOT_APP_ID` | <span data-ttu-id="5a0f1-226">文字列</span><span class="sxs-lookup"><span data-stu-id="5a0f1-226">string</span></span> | <span data-ttu-id="5a0f1-227">いいえ</span><span class="sxs-lookup"><span data-stu-id="5a0f1-227">No</span></span> | <span data-ttu-id="5a0f1-228">for の値を `completionBotId` 指定すると、指定したボットにメッセージ `result` を使用 `task/submit invoke` してオブジェクトが送信されます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-228">If a value for `completionBotId` is specified, the `result` object is sent using a `task/submit invoke` message to the specified bot.</span></span> <span data-ttu-id="5a0f1-229">`BOT_APP_ID` アプリのマニフェストでボットとして指定する必要があります。つまり、ボットに送信することはできません。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-229">`BOT_APP_ID` must be specified as a bot in the app's manifest, that is you cannot send it to any bot.</span></span> |

> [!NOTE]
> <span data-ttu-id="5a0f1-230">`APP_ID` 多くの場合、アプリにアプリの ID として使用する推奨ボットがある場合は、同じ値 `BOT_APP_ID` を指定できます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-230">`APP_ID` and `BOT_APP_ID` can be the same in many cases, if an app has a recommended bot to use as an app's ID if there is one.</span></span>

<span data-ttu-id="5a0f1-231">次のセクションでは、アプリのタスク モジュールでキーボードを使用する方法の詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-231">The next section provides details on using a keyboard with your app's task module.</span></span>

## <a name="keyboard-and-accessibility-guidelines"></a><span data-ttu-id="5a0f1-232">キーボードとアクセシビリティのガイドライン</span><span class="sxs-lookup"><span data-stu-id="5a0f1-232">Keyboard and accessibility guidelines</span></span>

<span data-ttu-id="5a0f1-233">HTML または JavaScript ベースのタスク モジュールでは、アプリのタスク モジュールをキーボードで使用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-233">With HTML or JavaScript-based task modules, you must ensure your app's task module can be used with a keyboard.</span></span> <span data-ttu-id="5a0f1-234">スクリーン リーダー プログラムは、キーボードを使用して移動する機能にも依存します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-234">Screen reader programs also depend on the ability to navigate using the keyboard.</span></span> <span data-ttu-id="5a0f1-235">これには、次の 2 つのことが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-235">This includes the following two things:</span></span>

* <span data-ttu-id="5a0f1-236">HTML タグ [で tabindex 属性](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) を使用して、フォーカスできる要素を制御します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-236">Using the [tabindex attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) in your HTML tags to control which elements can be focused.</span></span> <span data-ttu-id="5a0f1-237">また、tabindex 属性を使用して、通常は Tab キーと <kbd>Shift-Tab</kbd> キーを使用して、シーケンシャル キーボード ナビゲーションに参加する場所 <kbd>を特定</kbd> します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-237">Also, use tabindex attribute to identify where it participates in sequential keyboard navigation usually with the <kbd>Tab</kbd> and <kbd>Shift-Tab</kbd> keys.</span></span>
* <span data-ttu-id="5a0f1-238">タスク モジュール <kbd>の JavaScript</kbd> の Esc キーを処理します。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-238">Handling the <kbd>Esc</kbd> key in the JavaScript for your task module.</span></span> <span data-ttu-id="5a0f1-239">次のコードは、Esc キーを処理する方法の例 <kbd>を示</kbd> しています。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-239">The following code provides an example of how to handle the <kbd>Esc</kbd> key:</span></span>

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

<span data-ttu-id="5a0f1-240">Microsoft Teamsタスク モジュール ヘッダーから HTML へのキーボード ナビゲーションが正しく機能し、その逆も同様です。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-240">Microsoft Teams ensures that keyboard navigation works properly from the task module header into your HTML and vice-versa.</span></span>

## <a name="code-sample"></a><span data-ttu-id="5a0f1-241">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="5a0f1-241">Code sample</span></span>

|<span data-ttu-id="5a0f1-242">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="5a0f1-242">Sample name</span></span> | <span data-ttu-id="5a0f1-243">説明</span><span class="sxs-lookup"><span data-stu-id="5a0f1-243">Description</span></span> | <span data-ttu-id="5a0f1-244">.NET</span><span class="sxs-lookup"><span data-stu-id="5a0f1-244">.NET</span></span> | <span data-ttu-id="5a0f1-245">Node.js</span><span class="sxs-lookup"><span data-stu-id="5a0f1-245">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="5a0f1-246">タスク モジュールのサンプル ボット-V4</span><span class="sxs-lookup"><span data-stu-id="5a0f1-246">Task module sample bots-V4</span></span> | <span data-ttu-id="5a0f1-247">タスク モジュールを作成するためのサンプル。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-247">Samples for creating task modules.</span></span> |[<span data-ttu-id="5a0f1-248">View</span><span class="sxs-lookup"><span data-stu-id="5a0f1-248">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[<span data-ttu-id="5a0f1-249">View</span><span class="sxs-lookup"><span data-stu-id="5a0f1-249">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|<span data-ttu-id="5a0f1-250">タスク モジュールのサンプル タブとボット-V3</span><span class="sxs-lookup"><span data-stu-id="5a0f1-250">Task module sample tabs and bots-V3</span></span> | <span data-ttu-id="5a0f1-251">タスク モジュールを作成するためのサンプル。</span><span class="sxs-lookup"><span data-stu-id="5a0f1-251">Samples for creating task modules.</span></span> |[<span data-ttu-id="5a0f1-252">View</span><span class="sxs-lookup"><span data-stu-id="5a0f1-252">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[<span data-ttu-id="5a0f1-253">View</span><span class="sxs-lookup"><span data-stu-id="5a0f1-253">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a><span data-ttu-id="5a0f1-254">関連項目</span><span class="sxs-lookup"><span data-stu-id="5a0f1-254">See also</span></span>

* [<span data-ttu-id="5a0f1-255">デバイスのアクセス許可を要求する</span><span class="sxs-lookup"><span data-stu-id="5a0f1-255">Request device permissions</span></span>](~/concepts/device-capabilities/native-device-permissions.md)
* [<span data-ttu-id="5a0f1-256">メディア機能を統合する</span><span class="sxs-lookup"><span data-stu-id="5a0f1-256">Integrate media capabilities</span></span>](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [<span data-ttu-id="5a0f1-257">QR スキャナーまたはバーコード スキャナー機能をアプリに統合Teams</span><span class="sxs-lookup"><span data-stu-id="5a0f1-257">Integrate QR or barcode scanner capability in Teams</span></span>](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [<span data-ttu-id="5a0f1-258">場所の機能を統合Teams</span><span class="sxs-lookup"><span data-stu-id="5a0f1-258">Integrate location capabilities in Teams</span></span>](~/concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a><span data-ttu-id="5a0f1-259">次の手順</span><span class="sxs-lookup"><span data-stu-id="5a0f1-259">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5a0f1-260">タブでタスク モジュールを使用する</span><span class="sxs-lookup"><span data-stu-id="5a0f1-260">Use task modules in tabs</span></span>](~/task-modules-and-cards/task-modules/task-modules-tabs.md)