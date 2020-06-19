---
title: タスク モジュールとは
author: clearab
description: Microsoft Teams アプリからユーザーに情報を収集または表示するためのモーダルポップアップエクスペリエンスを追加します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 22fdc7a9dab1ff6f27e2b0d144e54676b6cca50e
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801259"
---
# <a name="what-are-task-modules"></a><span data-ttu-id="ed8de-103">タスク モジュールとは</span><span class="sxs-lookup"><span data-stu-id="ed8de-103">What are task modules?</span></span>

<span data-ttu-id="ed8de-104">タスク モジュールを使用すると、Teams アプリケーションでモーダル ポップアップ エクスペリエンスを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-104">Task modules allow you to create modal popup experiences in your Teams application.</span></span> <span data-ttu-id="ed8de-105">ポップアップの内部では、独自のカスタム HTML/JavaScript コードを実行したり、 `<iframe>` YouTube や Microsoft Stream ビデオなどのベースのウィジェットを表示したり、[アダプティブカード](/adaptive-cards/)を表示したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-105">Inside the popup you can run your own custom HTML/JavaScript code, show an `<iframe>`-based widget such as a YouTube or Microsoft Stream video or display an [Adaptive card](/adaptive-cards/).</span></span> <span data-ttu-id="ed8de-106">これらは特に、タスクの開始や完了、ビデオや Power BI ダッシュボードなどのリッチな情報の表示に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-106">They are especially useful for initiating and completing tasks or displaying rich information like videos or Power BI dashboards.</span></span> <span data-ttu-id="ed8de-107">一般的にポップアップ エクスペリエンスは、タブや会話ベースのボット エクスペリエンスに比べて、より自然にユーザーがタスクを開始したり完了したりすることができるようになっています。</span><span class="sxs-lookup"><span data-stu-id="ed8de-107">A popup experience is often more natural for users initiating and completing tasks compared to a tab or a conversation-based bot experience.</span></span>

<span data-ttu-id="ed8de-108">タスクモジュールは、Microsoft Teams のタブの基礎に基づいて構築されています。これらは基本的にはポップアップウィンドウ内のタブです。</span><span class="sxs-lookup"><span data-stu-id="ed8de-108">Task modules build on the foundation of Microsoft Teams tabs; they are essentially a tab inside a popup window.</span></span> <span data-ttu-id="ed8de-109">これらは同じ SDK を使用します。そのため、タブを構築した場合は、タスクモジュールを作成する方法が既に90% になっています。</span><span class="sxs-lookup"><span data-stu-id="ed8de-109">They use the same SDK, so if you've built a tab you are already 90% of the way to being able to create a task module.</span></span>

<span data-ttu-id="ed8de-110">タスク モジュールは次の 3 つの方法で呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-110">Task modules can be invoked in three ways:</span></span>

* <span data-ttu-id="ed8de-111">**チャネルまたは個人用タブ。**</span><span class="sxs-lookup"><span data-stu-id="ed8de-111">**Channel or personal tabs.**</span></span> <span data-ttu-id="ed8de-112">Microsoft Teams のタブ SDK を使用すると、タブのボタン、リンク、またはメニューからタスクモジュールを呼び出すことができます。[これについては、ここで詳しく説明し](~/task-modules-and-cards/task-modules/task-modules-tabs.md)ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-112">Using the Microsoft Teams Tabs SDK you can invoke task modules from buttons, links or menus on your tab. [This is covered in detail here.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)</span></span>
* <span data-ttu-id="ed8de-113">**Bot.**</span><span class="sxs-lookup"><span data-stu-id="ed8de-113">**Bots.**</span></span> <span data-ttu-id="ed8de-114">Bot から送信された[カード](~/task-modules-and-cards/cards/cards-reference.md)のボタン。</span><span class="sxs-lookup"><span data-stu-id="ed8de-114">Buttons on [cards](~/task-modules-and-cards/cards/cards-reference.md) sent from your bot.</span></span> <span data-ttu-id="ed8de-115">これは、ユーザーが bot を使用していることを確認するためにチャネル内のすべてのユーザーが必要ない場合に特に便利です。</span><span class="sxs-lookup"><span data-stu-id="ed8de-115">This is particularly useful when you don't need everyone in a channel to see what you are doing with a bot.</span></span> <span data-ttu-id="ed8de-116">たとえば、チャネル内のユーザーに投票してもらう場合、投票中の記録が見えるのは好ましくありません。</span><span class="sxs-lookup"><span data-stu-id="ed8de-116">For example, when having users respond to a poll in a channel it's not terribly useful to see a record of that poll being created.</span></span> [<span data-ttu-id="ed8de-117">これについては、ここで詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-117">This is covered in detail here.</span></span>](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* <span data-ttu-id="ed8de-118">**深いリンクから Teams の外側。**</span><span class="sxs-lookup"><span data-stu-id="ed8de-118">**Outside of Teams from a deep link.**</span></span> <span data-ttu-id="ed8de-119">任意の場所からタスクモジュールを呼び出すための Url を作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-119">You can also create URLs to invoke a task module from anywhere.</span></span> [<span data-ttu-id="ed8de-120">これについては、ここで詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-120">This is covered in detail here.</span></span>](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a><span data-ttu-id="ed8de-121">タスクモジュールの外観</span><span class="sxs-lookup"><span data-stu-id="ed8de-121">What a task module looks like</span></span>

<span data-ttu-id="ed8de-122">Bot から呼び出された場合のタスクモジュールは次のようになります (色の付いた長方形と番号付き円はありません)。</span><span class="sxs-lookup"><span data-stu-id="ed8de-122">Here's what a task module looks like when invoked from a bot (without the colored rectangles and numbered circles, of course):</span></span>

![タスクモジュールの例](~/assets/images/task-module/task-module-example.png)

<span data-ttu-id="ed8de-124">これについて説明します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-124">Let's walk through it:</span></span>

1. <span data-ttu-id="ed8de-125">アプリの[ `color` アイコン](~/resources/schema/manifest-schema.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="ed8de-125">Your app's [`color` icon](~/resources/schema/manifest-schema.md#icons).</span></span>
2. <span data-ttu-id="ed8de-126">アプリの[ `short` 名前](~/resources/schema/manifest-schema.md#name)。</span><span class="sxs-lookup"><span data-stu-id="ed8de-126">Your app's [`short` name](~/resources/schema/manifest-schema.md#name).</span></span>
3. <span data-ttu-id="ed8de-127">`title` [Taskinfo オブジェクト](#the-taskinfo-object)のプロパティで指定されたタスクモジュールのタイトル。</span><span class="sxs-lookup"><span data-stu-id="ed8de-127">The task module's title specified in the `title` property of the [TaskInfo object](#the-taskinfo-object).</span></span>
4. <span data-ttu-id="ed8de-128">タスクモジュールの [閉じる/キャンセル] ボタン。</span><span class="sxs-lookup"><span data-stu-id="ed8de-128">The task module's close/cancel button.</span></span> <span data-ttu-id="ed8de-129">ユーザーがこのコードを押す `err` と、[ここで](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)説明したように、アプリはイベントを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-129">If the user presses this, your app will receive an `err` event as described [here](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module).</span></span> <span data-ttu-id="ed8de-130">(現時点では、タスクモジュールが bot から呼び出されたとき**に、この**イベントを検出することはできません)。</span><span class="sxs-lookup"><span data-stu-id="ed8de-130">(**Note:** It is currently not possible to detect this event when a task module is invoked from a bot.)</span></span>
5. <span data-ttu-id="ed8de-131">青い四角形は、 `url` [taskinfo オブジェクト](#the-taskinfo-object)のプロパティを使用して独自の web ページを読み込む場合に、web ページが表示される場所です。</span><span class="sxs-lookup"><span data-stu-id="ed8de-131">The blue rectangle is the where your web page appears if you are loading your own web page using the `url` property of the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="ed8de-132">詳細については、以下の「[タスクモジュールのサイズ変更](#task-module-sizing)」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed8de-132">More detail is in the [task module sizing](#task-module-sizing) section below.</span></span>
6. <span data-ttu-id="ed8de-133">Taskinfo オブジェクトのプロパティを使用してアダプティブカードを表示している場合は、 `card` スペースが自動的に追加されます。それ以外の場合は、[自分で処理](#task-module-css-for-htmljavascript-task-modules)する必要があります。 [TaskInfo object](#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="ed8de-133">If you are displaying an Adaptive card via the `card` property of the [TaskInfo object](#the-taskinfo-object) the padding is added for you, otherwise you'll need to [handle this yourself](#task-module-css-for-htmljavascript-task-modules).</span></span>
7. <span data-ttu-id="ed8de-134">アダプティブカードボタンがここに表示されます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-134">Adaptive card buttons will render here.</span></span> <span data-ttu-id="ed8de-135">独自のページを使用している場合は、独自のボタンを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-135">If you're using your own page you must create your own buttons.</span></span>

## <a name="overview-of-invoking-and-dismissing-task-modules"></a><span data-ttu-id="ed8de-136">タスクモジュールの呼び出しと消去の概要</span><span class="sxs-lookup"><span data-stu-id="ed8de-136">Overview of invoking and dismissing task modules</span></span>

<span data-ttu-id="ed8de-137">タスクモジュールは、タブ、ボット、またはディープリンクから呼び出すことができ、一方で表示されるものは HTML またはアダプティブカードのどちらかになります。そのため、その呼び出し方法やユーザー操作の結果を処理する方法について、柔軟性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-137">Task modules can be invoked from tabs, bots or deep links and what appears in one can be either HTML or an Adaptive card, so there's a lot of flexibility in terms of how they are invoked and how to deal with the result of a user's interaction.</span></span> <span data-ttu-id="ed8de-138">次の表は、この機能の概要を示しています。</span><span class="sxs-lookup"><span data-stu-id="ed8de-138">The table below summarizes how this works:</span></span>

| <span data-ttu-id="ed8de-139">**呼び出しを経由する...**</span><span class="sxs-lookup"><span data-stu-id="ed8de-139">**Invoked via...**</span></span> | <span data-ttu-id="ed8de-140">**タスクモジュールは HTML/JavaScript**</span><span class="sxs-lookup"><span data-stu-id="ed8de-140">**Task module is HTML/JavaScript**</span></span> | <span data-ttu-id="ed8de-141">**タスクモジュールはアダプティブカード**</span><span class="sxs-lookup"><span data-stu-id="ed8de-141">**Task module is Adaptive card**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed8de-142">**タブ内の JavaScript**</span><span class="sxs-lookup"><span data-stu-id="ed8de-142">**JavaScript in a tab**</span></span> | <span data-ttu-id="ed8de-143">1. `tasks.startTask()` オプションの `submitHandler(err, result)` コールバック関数で TEAMS クライアント SDK 関数を使用する</span><span class="sxs-lookup"><span data-stu-id="ed8de-143">1. Use the Teams client SDK function `tasks.startTask()` with an optional `submitHandler(err, result)` callback function</span></span> <br/><br/> <span data-ttu-id="ed8de-144">2. タスクモジュールコードで、ユーザーが終了したら、 `tasks.submitTask()` `result` オブジェクトをパラメーターとして Teams SDK 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-144">2. In the task module code, when the user is finished, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="ed8de-145">`submitHandler`でコールバックが指定されていた場合 `tasks.startTask()` 、Teams はそれを `result` パラメーターとして呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-145">If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with `result` as a parameter.</span></span><br/><br/> <span data-ttu-id="ed8de-146">3. 呼び出し時にエラーが発生した場合は、 `tasks.startTask()` `submitHandler` 代わりに文字列で関数が呼び出され `err` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-146">3. If there was an error when invoking `tasks.startTask()`, the `submitHandler` function is called with an `err` string instead.</span></span> <br/><br/> <span data-ttu-id="ed8de-147">4. `completionBotId` そのケースを呼び出したときに、 `teams.startTask()` そのケースを `result` bot に送信するように指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-147">4. You can also specify a `completionBotId` when calling `teams.startTask()` - in that case `result` is sent to the bot instead.</span></span> | <span data-ttu-id="ed8de-148">1. Taskinfo オブジェクトを使用して Teams クライアント SDK 関数を呼び出し、[ `tasks.startTask()` [TaskInfo object](#the-taskinfo-object) `TaskInfo.card` タスクモジュール] ポップアップに表示するアダプティブカードの JSON を格納します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-148">1. Call the Teams client SDK function `tasks.startTask()` with a [TaskInfo object](#the-taskinfo-object) and `TaskInfo.card` containing the JSON for the Adaptive card to show in the task module popup.</span></span> <br/><br/> <span data-ttu-id="ed8de-149">2. `submitHandler` でコールバックが指定されていた場合、を呼び出したときにエラーが発生した場合 `tasks.startTask()` 、 `err` `tasks.startTask()` またはユーザーが右上の X を使用してタスクモジュールのポップアップを閉じた場合、Teams は文字列を使用して呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-149">2. If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with an `err` string if there was an error when invoking `tasks.startTask()` or if the user closes the task module popup using the X at the upper right.</span></span> <br/><br/> <span data-ttu-id="ed8de-150">3. ユーザーが [送信] ボタンを押すと、その `data` オブジェクトはの値として返さ `result` れます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-150">3. If the user presses an Action.Submit button then its `data` object is returned as the value of `result`.</span></span> |
| <span data-ttu-id="ed8de-151">**[ボットカード] ボタン**</span><span class="sxs-lookup"><span data-stu-id="ed8de-151">**Bot card button**</span></span> | <span data-ttu-id="ed8de-152">1つのボットカードボタンは、ボタンの種類に応じて、ディープリンク URL、またはメッセージを送信する2つの方法で、タスクモジュールを呼び出すことができます。 `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="ed8de-152">1. Bot card buttons, depending on the type of button, can invoke task modules in two ways: a deep link URL or by sending a `task/fetch` message.</span></span> <span data-ttu-id="ed8de-153">深いリンク Url のしくみについては、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed8de-153">See below for how deep link URLs work.</span></span> <br/><br/> <span data-ttu-id="ed8de-154">2. ボタンのアクション `type` `task/fetch` ( `Action.Submit` アダプティブカード用のボタンの種類) がある場合 `task/fetch invoke` は、bot にイベント (カバーの下の HTTP POST) が送信され、bot は http 200 を使用して post に応答し、ボットは[taskinfo オブジェクト](#the-taskinfo-object)のラッパーを含む応答本文に応答します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-154">2. If the button's action `type` is `task/fetch` (`Action.Submit` button type for Adaptive cards), a `task/fetch invoke` event (an HTTP POST under the covers) is sent to the bot, and the bot responds to the POST with HTTP 200 and the response body containing a wrapper around the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="ed8de-155">これについては[、「task/fetch を使用してタスクモジュールを呼び出す](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch)」で詳しく説明されています。</span><span class="sxs-lookup"><span data-stu-id="ed8de-155">This is explained in detail in [invoking a task module via task/fetch](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch).</span></span><br/><br/> <span data-ttu-id="ed8de-156">3. Teams には、タスクモジュールが表示されます。ユーザーが終了したら、 `tasks.submitTask()` オブジェクトをパラメーターとして TEAMS SDK 関数を呼び出し `result` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-156">3. Teams displays the task module; when the user is finished, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <br/><br/> <span data-ttu-id="ed8de-157">4. この bot は、 `task/submit invoke` オブジェクトを含むメッセージを受信します。 `result`</span><span class="sxs-lookup"><span data-stu-id="ed8de-157">4. The bot receives a `task/submit invoke` message that contains the `result` object.</span></span> <span data-ttu-id="ed8de-158">メッセージに返信するには、次の3つの方法があります。そのために `task/submit` は、何もしない (タスクが正常に完了した) か、ユーザーにメッセージをポップアップウィンドウで表示するか、または別のタスクモジュールウィンドウ (つまりウィザードのような操作を作成する) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-158">You have three different ways to respond to the `task/submit` message: by doing nothing (the task completed successfully), by displaying a message to the user in a popup window, or by invoking another task module window (i.e. creating a wizard-like experience).</span></span> <span data-ttu-id="ed8de-159">この3つのオプションについ[ては、「タスク/送信に関する詳細な説明」](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed8de-159">These three options are discussed more [in the detailed discussion on task/submit](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> | <span data-ttu-id="ed8de-160">1. Bot フレームワークカードのボタンと同様に、アダプティブカード上のボタンは、タスクモジュールを呼び出すための2つの方法をサポートしています。ボタンを使用した深いリンク Url とボタンを `Action.openUrl` `task/fetch` 使用する方法 `Action.Submit` です。</span><span class="sxs-lookup"><span data-stu-id="ed8de-160">1. Like buttons on Bot Framework cards, buttons on Adaptive cards support two ways of invoking task modules: deep link URLs with `Action.openUrl` buttons, and via `task/fetch` using `Action.Submit` buttons.</span></span> <br/><br/> <span data-ttu-id="ed8de-161">2. アダプティブカードを使用したタスクモジュールは、HTML/JavaScript のケースと同じように動作します (左を参照)。</span><span class="sxs-lookup"><span data-stu-id="ed8de-161">2. Task modules with Adaptive cards work very similarly to the HTML/JavaScript case (see left).</span></span> <span data-ttu-id="ed8de-162">主な違いは、アダプティブカードを使用しているときに JavaScript が存在しないため、を呼び出すことができないということです `tasks.submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="ed8de-162">The major difference is that since there's no JavaScript when you're using Adaptive cards, there's no way to call `tasks.submitTask()`.</span></span> <span data-ttu-id="ed8de-163">代わりに、チームは `data` からオブジェクトを取得し、それを `Action.Submit` イベントのペイロードとして返し `task/submit` ます ([ここで](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)説明します)。</span><span class="sxs-lookup"><span data-stu-id="ed8de-163">Instead, Teams takes the `data` object from `Action.Submit` and returns it as the payload of in the `task/submit` event, as described [here](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> |
| <span data-ttu-id="ed8de-164">**ディープリンクの URL**</span><span class="sxs-lookup"><span data-stu-id="ed8de-164">**Deep link URL**</span></span> <br/>[<span data-ttu-id="ed8de-165">URL 構文</span><span class="sxs-lookup"><span data-stu-id="ed8de-165">URL syntax</span></span>](#task-module-deep-link-syntax) | <span data-ttu-id="ed8de-166">1. Teams がタスクモジュールを呼び出します。`<iframe>`ディープリンクのパラメーターで指定されたの内部に表示される URL `url` 。</span><span class="sxs-lookup"><span data-stu-id="ed8de-166">1. Teams invokes the task module; the URL that appears inside the `<iframe>` specified in the `url` parameter of the deep link.</span></span> <span data-ttu-id="ed8de-167">コールバックはありません `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="ed8de-167">There is no `submitHandler` callback.</span></span> <br/><br/> <span data-ttu-id="ed8de-168">2. タスクモジュールのページの JavaScript 内で、 `tasks.submitTask()` オブジェクトをパラメーターとして閉じます。これは、 `result` タブまたはボットカードボタンから呼び出すときと同じです。</span><span class="sxs-lookup"><span data-stu-id="ed8de-168">2. Within the JavaScript of the page in the task module, call `tasks.submitTask()` to close it with a `result` object as a parameter, the same as when invoking it from a tab or a bot card button.</span></span> <span data-ttu-id="ed8de-169">ただし、完了ロジックは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-169">Completion logic is slightly different, however.</span></span> <span data-ttu-id="ed8de-170">完了ロジックがクライアント上に存在する場合 (bot がない場合)、コールバックがないので、 `submitHandler` への呼び出しの前のコードにすべての完了ロジックが含まれている必要があり `tasks.submitTask()` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-170">If your completion logic resides on the client (i.e. if there is no bot) there is no `submitHandler` callback, so any completion logic must be in the code preceding the call to `tasks.submitTask()`.</span></span> <span data-ttu-id="ed8de-171">呼び出しエラーはコンソールによってのみ報告されます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-171">Invocation errors are only reported via the console.</span></span> <span data-ttu-id="ed8de-172">Bot がある場合は、deep link でパラメーターを指定して、 `completionBotId` イベントを使用してオブジェクトを送信でき `result` `task/submit` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-172">If you have a bot, then you can specify a `completionBotId` parameter in the deep link to send the `result` object via a `task/submit` event.</span></span> | <span data-ttu-id="ed8de-173">1. Teams がタスクモジュールを呼び出します。アダプティブカードの JSON カード本文は、ディープリンクのパラメーターの URL エンコードされた値として指定され `card` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-173">1. Teams invokes the task module; the JSON card body of the Adaptive card is specified as a URL-encoded value of the `card` parameter of the deep link.</span></span> <br/><br/> <span data-ttu-id="ed8de-174">2. ユーザーがタスクモジュールを閉じるには、タスクモジュールの右上にある [X] をクリックするか、カードのボタンを押し `Action.Submit` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-174">2. The user closes the task module by clicking on the X at the upper right of the task module or by pressing an `Action.Submit` button on the card.</span></span> <span data-ttu-id="ed8de-175">を呼び出すことはできないの `submitHandler` で、アダプティブカードフィールドの値をに送信する bot が必要です。</span><span class="sxs-lookup"><span data-stu-id="ed8de-175">Since there is no `submitHandler` to call, you must have a bot to send the value of the Adaptive card fields to.</span></span> <span data-ttu-id="ed8de-176">ディープリンクのパラメーターを使用して、 `completionBotId` イベントを使用してデータを送信する bot を指定し `task/submit invoke` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-176">You use the `completionBotId` parameter in the deep link to specify the bot to send the data to via a `task/submit invoke` event.</span></span> |

> [!NOTE]
> <span data-ttu-id="ed8de-177">JavaScript からのタスクモジュールの呼び出しは、mobile ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="ed8de-177">Invoking a task module from JavaScript is not supported on mobile.</span></span>

## <a name="the-taskinfo-object"></a><span data-ttu-id="ed8de-178">TaskInfo オブジェクト</span><span class="sxs-lookup"><span data-stu-id="ed8de-178">The TaskInfo object</span></span>

<span data-ttu-id="ed8de-179">オブジェクトには、 `TaskInfo` タスクモジュールのメタデータが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ed8de-179">The `TaskInfo` object contains the metadata for a task module.</span></span> <span data-ttu-id="ed8de-180">オブジェクト定義は以下のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ed8de-180">The object definition is below.</span></span> <span data-ttu-id="ed8de-181">**must** `url` (En 埋め込み iFrame の場合) または `card` (アダプティブカードの場合) のいずれかを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-181">You **must** define either `url` (for en embedded iFrame) or `card` (for an Adaptive Card).</span></span>

| <span data-ttu-id="ed8de-182">属性</span><span class="sxs-lookup"><span data-stu-id="ed8de-182">Attribute</span></span> | <span data-ttu-id="ed8de-183">型</span><span class="sxs-lookup"><span data-stu-id="ed8de-183">Type</span></span> | <span data-ttu-id="ed8de-184">説明</span><span class="sxs-lookup"><span data-stu-id="ed8de-184">Description</span></span> |
| --- | --- | --- |
| `title` | <span data-ttu-id="ed8de-185">string</span><span class="sxs-lookup"><span data-stu-id="ed8de-185">string</span></span> | <span data-ttu-id="ed8de-186">アプリ名の下に表示され、アプリアイコンの右側に表示されます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-186">Appears below the app name and to the right of the app icon</span></span> |
| `height` | <span data-ttu-id="ed8de-187">number または string</span><span class="sxs-lookup"><span data-stu-id="ed8de-187">number or string</span></span> | <span data-ttu-id="ed8de-188">タスクモジュールの高さを表す数値をピクセル、または、またはで指定でき `small` `medium` `large` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-188">This can be a number representing the task module's height in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="ed8de-189">[高さと幅を処理する方法については、以下を参照して](#task-module-sizing)ください。</span><span class="sxs-lookup"><span data-stu-id="ed8de-189">[See below for how height and width are handled](#task-module-sizing).</span></span> |
| `width` | <span data-ttu-id="ed8de-190">number または string</span><span class="sxs-lookup"><span data-stu-id="ed8de-190">number or string</span></span> | <span data-ttu-id="ed8de-191">タスクモジュールの幅をピクセル、または、、またはの数値で指定でき `small` `medium` `large` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-191">This can be a number representing the task module's width in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="ed8de-192">[高さと幅を処理する方法については、以下を参照して](#task-module-sizing)ください。</span><span class="sxs-lookup"><span data-stu-id="ed8de-192">[See below for how height and width are handled](#task-module-sizing).</span></span> |
| `url` | <span data-ttu-id="ed8de-193">string</span><span class="sxs-lookup"><span data-stu-id="ed8de-193">string</span></span> | <span data-ttu-id="ed8de-194">タスクモジュール内に読み込まれたページの URL `<iframe>` 。</span><span class="sxs-lookup"><span data-stu-id="ed8de-194">The URL of the page loaded as an `<iframe>` inside the task module.</span></span> <span data-ttu-id="ed8de-195">URL のドメインは、アプリのマニフェストのアプリの[Validdomains 配列](~/resources/schema/manifest-schema.md#validdomains)内にある必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-195">The URL's domain must be in the app's [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in your app's manifest.</span></span> |
| `card` | <span data-ttu-id="ed8de-196">アダプティブカードまたはアダプティブカードのボットカード添付ファイル</span><span class="sxs-lookup"><span data-stu-id="ed8de-196">Adaptive card or an Adaptive card bot card attachment</span></span> | <span data-ttu-id="ed8de-197">タスクモジュールに表示されるアダプティブカードの JSON。</span><span class="sxs-lookup"><span data-stu-id="ed8de-197">The JSON for the Adaptive card to appear in the task module.</span></span> <span data-ttu-id="ed8de-198">Bot から呼び出している場合は、Bot フレームワークオブジェクトでアダプティブカード JSON を使用する必要があり `attachment` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-198">If you're invoking from a bot, you'll need to use the Adaptive card JSON in a Bot Framework `attachment` object.</span></span> <span data-ttu-id="ed8de-199">タブからは、アダプティブカードのみを使用します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-199">From a tab you'll use just an Adaptive Card.</span></span> [<span data-ttu-id="ed8de-200">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-200">Here's an example.</span></span>](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | <span data-ttu-id="ed8de-201">string</span><span class="sxs-lookup"><span data-stu-id="ed8de-201">string</span></span> | <span data-ttu-id="ed8de-202">クライアントがタスクモジュール機能をサポートしていない場合、この URL はブラウザタブで開かれます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-202">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |
| `completionBotId` | <span data-ttu-id="ed8de-203">string</span><span class="sxs-lookup"><span data-stu-id="ed8de-203">string</span></span> | <span data-ttu-id="ed8de-204">ユーザーのタスクモジュールとの対話結果をに送信する bot アプリ ID を指定します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-204">Specifies a bot App ID to send the result of the user's interaction with the task module to.</span></span> <span data-ttu-id="ed8de-205">指定した場合、bot は、 `task/submit invoke` イベントペイロードで JSON オブジェクトを含むイベントを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-205">If specified, the bot will receive a `task/submit invoke` event with a JSON object in the event payload.</span></span> |

> [!NOTE]
> <span data-ttu-id="ed8de-206">タスクモジュール機能を使用するには、読み込む Url のドメインが `validDomains` アプリのマニフェストの配列に含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-206">The task module feature requires that the domains of any URLs you want to load are included in the `validDomains` array in your app's manifest.</span></span>

## <a name="task-module-sizing"></a><span data-ttu-id="ed8de-207">タスクモジュールのサイズ変更</span><span class="sxs-lookup"><span data-stu-id="ed8de-207">Task module sizing</span></span>

<span data-ttu-id="ed8de-208">およびの整数を使用して `TaskInfo.width` `TaskInfo.height` 、高さと幅をピクセル単位で設定します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-208">Using integers for `TaskInfo.width` and `TaskInfo.height` will set the height and width in pixels.</span></span> <span data-ttu-id="ed8de-209">ただし、チームのウィンドウと画面の解像度のサイズによっては、縦横比 (幅/高さ) を維持している場合に、比率が低くなります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-209">However, depending on the size of the Team's window and screen resolution they will be reduced proportionally while maintaining the aspect ratio (width/height).</span></span>

<span data-ttu-id="ed8de-210">との場合、およびの場合、 `TaskInfo.width` `TaskInfo.height` 上の図の赤の `"small"` `"medium"` `"large"` 四角形のサイズは、使用可能な領域の比率 (20%、50%、60%、 `width` 50%、66%(for `height` ) です。</span><span class="sxs-lookup"><span data-stu-id="ed8de-210">If `TaskInfo.width` and `TaskInfo.height` are `"small"`, `"medium"` or `"large"` the size of the red rectangle in the picture above is a proportion of the available space: 20%, 50%, 60% for `width` and 20%, 50%, 66% for `height`.</span></span>

<span data-ttu-id="ed8de-211">タブから起動されたタスクモジュールは、動的にサイズ変更できます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-211">Task modules invoked from a tab can be dynamically resized.</span></span> <span data-ttu-id="ed8de-212">呼び出し後に、 `tasks.startTask()` `tasks.updateTask(newSize)` newSize オブジェクトの height プロパティと width プロパティの両方が taskinfo 仕様に準拠していることを呼び出します (例、</span><span class="sxs-lookup"><span data-stu-id="ed8de-212">After calling `tasks.startTask()` you can call `tasks.updateTask(newSize)` where height and width properties on the newSize object conform to the TaskInfo spec (ex.</span></span> <span data-ttu-id="ed8de-213">`{ height: 'medium', width: 'medium' }`).</span><span class="sxs-lookup"><span data-stu-id="ed8de-213">`{ height: 'medium', width: 'medium' }`).</span></span>

## <a name="task-module-css-for-htmljavascript-task-modules"></a><span data-ttu-id="ed8de-214">HTML/JavaScript タスクモジュール用のタスクモジュール CSS</span><span class="sxs-lookup"><span data-stu-id="ed8de-214">Task module CSS for HTML/JavaScript task modules</span></span>

<span data-ttu-id="ed8de-215">HTML/JavaScript ベースのタスクモジュールは、ヘッダーの下にあるタスクモジュールの領域全体にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-215">HTML/JavaScript-based task modules have access to the entire area of the task module below the header.</span></span> <span data-ttu-id="ed8de-216">非常に高い柔軟性が提供されますが、ヘッダー要素に合わせてエッジの周囲にパディングを行い、不要なスクロールバーを使用しないようにするには、適切な CSS を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-216">While that offers a great deal of flexibility, if you want padding around the edges to align with the header elements and avoid unnecessary scrollbars you'll need to provide the right CSS.</span></span> <span data-ttu-id="ed8de-217">いくつかのユースケースの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-217">Here are some examples for a few use cases.</span></span>

### <a name="example-1---youtube-video"></a><span data-ttu-id="ed8de-218">例 1-YouTube ビデオ</span><span class="sxs-lookup"><span data-stu-id="ed8de-218">Example 1 - YouTube video</span></span>

<span data-ttu-id="ed8de-219">YouTube は、web ページにビデオを埋め込む機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-219">YouTube offers the ability to embed videos on web pages.</span></span> <span data-ttu-id="ed8de-220">簡単なスタブ web ページを使用すると、これをタスクモジュールに簡単に表示できます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-220">Using a simple stub web page it's easy to show this in a task module:</span></span>

![YouTube ビデオ](~/assets/images/task-module/youtube-example.png)

<span data-ttu-id="ed8de-222">CSS を使用しないこのページの HTML を次に示します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-222">Here's the HTML for this page, without the CSS:</span></span>

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

<span data-ttu-id="ed8de-223">CSS は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-223">The CSS looks like this:</span></span>

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

### <a name="example-2---powerapp"></a><span data-ttu-id="ed8de-224">例 2-PowerApp</span><span class="sxs-lookup"><span data-stu-id="ed8de-224">Example 2 - PowerApp</span></span>

<span data-ttu-id="ed8de-225">同じ方法を使用して、PowerApp も埋め込むことができます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-225">You can use the same approach to embed a PowerApp as well.</span></span> <span data-ttu-id="ed8de-226">個々の PowerApp の高さと幅はカスタマイズ可能なので、目的のプレゼンテーションを実現するには、高さと幅を調整しなければならない場合があります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-226">As the height/width of any individual PowerApp is customizable, you may need to adjust the height and width to achieve your desired presentation.</span></span>

![Asset Management PowerApp](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

<span data-ttu-id="ed8de-228">そして、CSS は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ed8de-228">And the CSS is:</span></span>

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a><span data-ttu-id="ed8de-229">アダプティブカードまたはアダプティブカードのボットカード添付ファイル</span><span class="sxs-lookup"><span data-stu-id="ed8de-229">Adaptive card or Adaptive card bot card attachment</span></span>

<span data-ttu-id="ed8de-230">前述したように、を呼び出す方法によって `card` は、アダプティブカードを使用するか、またはアダプティブカードのボットカードの添付ファイル (添付ファイルオブジェクトにラップされたアダプティブカードのみ) を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-230">As we noted above, depending on how you're invoking your `card` you'll need to use either an Adaptive card, or an Adaptive card bot card attachment (which is just an Adaptive card wrapped in an attachment object).</span></span>

<span data-ttu-id="ed8de-231">タブから呼び出している場合は、アダプティブカードを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-231">When you're invoking from a tab, you'll need to use an adaptive card.</span></span> <span data-ttu-id="ed8de-232">非常に簡単な例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-232">Here's a very simple example:</span></span>

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

<span data-ttu-id="ed8de-233">Bot から呼び出している場合は、次の例に示すように、アダプティブカードのボットカード添付ファイルを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-233">When you're invoking from a bot you'll need to use an Adaptive card bot card attachment as in the example below:</span></span>

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

<span data-ttu-id="ed8de-234">Bot またはタブから、アダプティブカードを含むタスクモジュールを呼び出しているかどうかを覚えておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-234">You'll need to remember whether you are invoking a task module containing an Adaptive card from a bot or a tab.</span></span>

## <a name="task-module-deep-link-syntax"></a><span data-ttu-id="ed8de-235">タスクモジュールの詳細なリンク構文</span><span class="sxs-lookup"><span data-stu-id="ed8de-235">Task module deep link syntax</span></span>

<span data-ttu-id="ed8de-236">タスクモジュールの深さのリンクは、他の2つの情報を含む[Taskinfo オブジェクト](#the-taskinfo-object)のシリアル化だけで `APP_ID` あり、必要に応じて次のようにすることもでき `BOT_APP_ID` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-236">A task module deep link is just a serialization of the [TaskInfo object](#the-taskinfo-object) with two other pieces of information, `APP_ID` and optionally the `BOT_APP_ID`:</span></span>

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

<span data-ttu-id="ed8de-237">データ[TaskInfo object](#the-taskinfo-object)型については、「」、「」 `<TaskInfo.url>` `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` 、および `<TaskInfo.title>` 「」の値については、「taskinfo オブジェクト」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ed8de-237">See [TaskInfo object](#the-taskinfo-object) for the data types and allowable values for `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`, and `<TaskInfo.title>`.</span></span>

> [!TIP]
> <span data-ttu-id="ed8de-238">特に、 `card` パラメーター (JavaScript の[ `encodeURI()` 関数](https://www.w3schools.com/jsref/jsref_encodeURI.asp)など) を使用する場合は、URL が深いリンクをエンコードしていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="ed8de-238">Be sure to URL encode the deep link, especially when using the `card` parameter (for example, JavaScript's [`encodeURI()` function](https://www.w3schools.com/jsref/jsref_encodeURI.asp)).</span></span>

<span data-ttu-id="ed8de-239">との情報を以下に示し `APP_ID` `BOT_APP_ID` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-239">Here's the information on `APP_ID` and `BOT_APP_ID`:</span></span>

| <span data-ttu-id="ed8de-240">値</span><span class="sxs-lookup"><span data-stu-id="ed8de-240">Value</span></span> | <span data-ttu-id="ed8de-241">型</span><span class="sxs-lookup"><span data-stu-id="ed8de-241">Type</span></span> | <span data-ttu-id="ed8de-242">必須</span><span class="sxs-lookup"><span data-stu-id="ed8de-242">Required?</span></span> | <span data-ttu-id="ed8de-243">説明</span><span class="sxs-lookup"><span data-stu-id="ed8de-243">Description</span></span> |
| --- | --- | --- | --- |
| `APP_ID` | <span data-ttu-id="ed8de-244">string</span><span class="sxs-lookup"><span data-stu-id="ed8de-244">string</span></span> | <span data-ttu-id="ed8de-245">はい</span><span class="sxs-lookup"><span data-stu-id="ed8de-245">Yes</span></span> | <span data-ttu-id="ed8de-246">タスクモジュールを呼び出すアプリの[id](~/resources/schema/manifest-schema.md#id) 。</span><span class="sxs-lookup"><span data-stu-id="ed8de-246">The [id](~/resources/schema/manifest-schema.md#id) of the app invoking the task module.</span></span> <span data-ttu-id="ed8de-247">マニフェスト内の[Validdomains 配列](~/resources/schema/manifest-schema.md#validdomains)に `APP_ID` は、 `url` が URL にある場合のドメインが含まれている必要があり `url` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-247">The [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in the manifest for `APP_ID` must contain the domain for `url` if `url` is in the URL.</span></span> <span data-ttu-id="ed8de-248">(アプリ ID は、タスクモジュールがタブまたは bot から呼び出されたときに既に知られています。これは、に含まれていないため `TaskInfo` です)。</span><span class="sxs-lookup"><span data-stu-id="ed8de-248">(The app ID is already known when a task module is invoked from a tab or a bot, which is why it's not included in `TaskInfo`.)</span></span> |
| `BOT_APP_ID` | <span data-ttu-id="ed8de-249">文字列</span><span class="sxs-lookup"><span data-stu-id="ed8de-249">string</span></span> | <span data-ttu-id="ed8de-250">いいえ</span><span class="sxs-lookup"><span data-stu-id="ed8de-250">No</span></span> | <span data-ttu-id="ed8de-251">の値が指定されている場合、 `completionBotId` `result` オブジェクトは、指定された bot へのメッセージによって送信され `task/submit invoke` ます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-251">If a value for `completionBotId` is specified, the `result` object is sent via a a `task/submit invoke` message to the specified bot.</span></span> <span data-ttu-id="ed8de-252">`BOT_APP_ID`アプリのマニフェストでボットとして指定する必要があります。つまり、任意の bot に送信するだけではできません。</span><span class="sxs-lookup"><span data-stu-id="ed8de-252">`BOT_APP_ID` must be specified as a bot in the app's manifest, i.e. you can't just send it to any bot.</span></span> |

<span data-ttu-id="ed8de-253">これは同じであること `APP_ID` `BOT_APP_ID` に注意してください。多くの場合、アプリの ID として使用することをお勧めするので、アプリに bot がある場合は、それを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ed8de-253">Note that it's valid for `APP_ID` and `BOT_APP_ID` to be the same, and in many cases will be if an app has a bot since it's recommended to use that as an app's ID if there is one.</span></span>

## <a name="keyboard-and-accessibility-guidelines"></a><span data-ttu-id="ed8de-254">キーボードとユーザー補助ガイドライン</span><span class="sxs-lookup"><span data-stu-id="ed8de-254">Keyboard and accessibility guidelines</span></span>

<span data-ttu-id="ed8de-255">HTML/JavaScript ベースのタスクモジュールを使用すると、アプリのタスクモジュールをキーボードで使用できることを確認する責任があります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-255">With HTML/JavaScript-based task modules it is your responsibility to ensure your app's task module can be used with a keyboard.</span></span> <span data-ttu-id="ed8de-256">スクリーンリーダープログラムは、キーボードを使用して移動する機能にも依存します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-256">Screen reader programs also depend on the ability to navigate using the keyboard.</span></span> <span data-ttu-id="ed8de-257">実用上の問題として、次の2つのことがあります。</span><span class="sxs-lookup"><span data-stu-id="ed8de-257">As a practical matter this means two things:</span></span>

1. <span data-ttu-id="ed8de-258">HTML タグの[tabindex 属性](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex)を使用して、どの要素がフォーカスされているか、または (通常は<kbd>Tab</kbd>キーと Shift キーを<kbd>押しながら</kbd>tab キーを使用して) 連続したキーボードナビゲーションに参加するかどうかを制御します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-258">Using the [tabindex attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) in your HTML tags to control which elements can be focused and if/where it participates in sequential keyboard navigation (usually with the <kbd>Tab</kbd> and <kbd>Shift-Tab</kbd> keys).</span></span>
2. <span data-ttu-id="ed8de-259">タスクモジュールの JavaScript で<kbd>Esc</kbd>キーを処理します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-259">Handling the <kbd>Esc</kbd> key in the JavaScript for your task module.</span></span> <span data-ttu-id="ed8de-260">これを行う方法を示すコードサンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="ed8de-260">Here's a code sample showing how to do this:</span></span>

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

<span data-ttu-id="ed8de-261">Microsoft Teams では、キーボードナビゲーションがタスクモジュールヘッダーから HTML およびその逆に適切に動作することが保証されます。</span><span class="sxs-lookup"><span data-stu-id="ed8de-261">Microsoft Teams will ensure that keyboard navigation works properly from the task module header into your HTML and vice-versa.</span></span>

## <a name="task-module-samples"></a><span data-ttu-id="ed8de-262">タスクモジュールのサンプル</span><span class="sxs-lookup"><span data-stu-id="ed8de-262">Task module samples</span></span>

* [<span data-ttu-id="ed8de-263">Node.js/TypeScript サンプル</span><span class="sxs-lookup"><span data-stu-id="ed8de-263">Node.js/TypeScript sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs)
* [<span data-ttu-id="ed8de-264">C#/.NET サンプル</span><span class="sxs-lookup"><span data-stu-id="ed8de-264">C#/.NET sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp)
