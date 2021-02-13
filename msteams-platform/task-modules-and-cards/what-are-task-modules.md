---
title: タスク モジュールとは
author: clearab
description: モーダル ポップアップ エクスペリエンスを追加して、Microsoft Teams アプリからユーザーに情報を収集または表示します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d92da7e6def6d66efd2f94600b7b8f8847553701
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231660"
---
# <a name="what-are-task-modules"></a><span data-ttu-id="53805-103">タスク モジュールとは</span><span class="sxs-lookup"><span data-stu-id="53805-103">What are task modules?</span></span>

<span data-ttu-id="53805-104">タスク モジュールを使用すると、Teams のアプリケーションでモーダル ポップアップ エクスペリエンスを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="53805-104">Task modules allow you to create modal popup experiences in your Teams application.</span></span> <span data-ttu-id="53805-105">ポップアップ内では、独自のカスタム HTML/JavaScript コードを実行したり、YouTube や Microsoft Stream ビデオなどの -based ウィジェットを表示したり、アダプティブ カード `<iframe>` [を表示することができます](/adaptive-cards/)。</span><span class="sxs-lookup"><span data-stu-id="53805-105">Inside the popup you can run your own custom HTML/JavaScript code, show an `<iframe>`-based widget such as a YouTube or Microsoft Stream video or display an [Adaptive card](/adaptive-cards/).</span></span> <span data-ttu-id="53805-106">これらは特に、タスクの開始や完了、ビデオや Power BI ダッシュボードなどのリッチな情報の表示に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="53805-106">They are especially useful for initiating and completing tasks or displaying rich information like videos or Power BI dashboards.</span></span> <span data-ttu-id="53805-107">一般的にポップアップ エクスペリエンスは、タブや会話ベースのボット エクスペリエンスに比べて、より自然にユーザーがタスクを開始したり完了したりすることができるようになっています。</span><span class="sxs-lookup"><span data-stu-id="53805-107">A popup experience is often more natural for users initiating and completing tasks compared to a tab or a conversation-based bot experience.</span></span>

<span data-ttu-id="53805-108">タスク モジュールは、Microsoft Teams のタブの基礎に構築されます。基本的には、ポップアップ ウィンドウ内のタブです。</span><span class="sxs-lookup"><span data-stu-id="53805-108">Task modules build on the foundation of Microsoft Teams tabs; they are essentially a tab inside a popup window.</span></span> <span data-ttu-id="53805-109">これらは同じ SDK を使用します。そのため、タブを作成している場合は、タスク モジュールを作成する方法の 90% が既に存在します。</span><span class="sxs-lookup"><span data-stu-id="53805-109">They use the same SDK, so if you've built a tab you are already 90% of the way to being able to create a task module.</span></span>

<span data-ttu-id="53805-110">タスク モジュールは次の 3 つの方法で呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="53805-110">Task modules can be invoked in three ways:</span></span>

* <span data-ttu-id="53805-111">**[チャネル] タブまたは [個人用] タブ。**</span><span class="sxs-lookup"><span data-stu-id="53805-111">**Channel or personal tabs.**</span></span> <span data-ttu-id="53805-112">Microsoft Teams Tabs SDK を使用すると、タブのボタン、リンク、またはメニューからタスク モジュールを呼び出す方法について説明します。詳しくは、こちらを [参照してください。](~/task-modules-and-cards/task-modules/task-modules-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="53805-112">Using the Microsoft Teams Tabs SDK you can invoke task modules from buttons, links or menus on your tab. [This is covered in detail here.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)</span></span>
* <span data-ttu-id="53805-113">**ボット。**</span><span class="sxs-lookup"><span data-stu-id="53805-113">**Bots.**</span></span> <span data-ttu-id="53805-114">ボットから送信 [されたカード](~/task-modules-and-cards/cards/cards-reference.md) のボタン。</span><span class="sxs-lookup"><span data-stu-id="53805-114">Buttons on [cards](~/task-modules-and-cards/cards/cards-reference.md) sent from your bot.</span></span> <span data-ttu-id="53805-115">これは、チャネル内のすべてのユーザーがボットで何を行っているのかを確認する必要が生じない場合に特に便利です。</span><span class="sxs-lookup"><span data-stu-id="53805-115">This is particularly useful when you don't need everyone in a channel to see what you are doing with a bot.</span></span> <span data-ttu-id="53805-116">たとえば、チャネル内のユーザーに投票してもらう場合、投票中の記録が見えるのは好ましくありません。</span><span class="sxs-lookup"><span data-stu-id="53805-116">For example, when having users respond to a poll in a channel it's not terribly useful to see a record of that poll being created.</span></span> [<span data-ttu-id="53805-117">詳しくは、ここをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="53805-117">This is covered in detail here.</span></span>](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* <span data-ttu-id="53805-118">**ディープ リンクからの Teams の外部。**</span><span class="sxs-lookup"><span data-stu-id="53805-118">**Outside of Teams from a deep link.**</span></span> <span data-ttu-id="53805-119">どこからでもタスク モジュールを呼び出す URL を作成できます。</span><span class="sxs-lookup"><span data-stu-id="53805-119">You can also create URLs to invoke a task module from anywhere.</span></span> [<span data-ttu-id="53805-120">詳しくは、ここをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="53805-120">This is covered in detail here.</span></span>](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a><span data-ttu-id="53805-121">タスク モジュールの外観</span><span class="sxs-lookup"><span data-stu-id="53805-121">What a task module looks like</span></span>

<span data-ttu-id="53805-122">ボットから呼び出された場合のタスク モジュールの外観を次に示します (もちろん、色付き四角形と番号付き円はありません)。</span><span class="sxs-lookup"><span data-stu-id="53805-122">Here's what a task module looks like when invoked from a bot (without the colored rectangles and numbered circles, of course):</span></span>

![タスク モジュールの例](~/assets/images/task-module/task-module-example.png)

<span data-ttu-id="53805-124">それでは、次の方法を見てみいます。</span><span class="sxs-lookup"><span data-stu-id="53805-124">Let's walk through it:</span></span>

1. <span data-ttu-id="53805-125">アプリの[ `color` アイコン。](~/resources/schema/manifest-schema.md#icons)</span><span class="sxs-lookup"><span data-stu-id="53805-125">Your app's [`color` icon](~/resources/schema/manifest-schema.md#icons).</span></span>
2. <span data-ttu-id="53805-126">アプリの[ `short` 名前です](~/resources/schema/manifest-schema.md#name)。</span><span class="sxs-lookup"><span data-stu-id="53805-126">Your app's [`short` name](~/resources/schema/manifest-schema.md#name).</span></span>
3. <span data-ttu-id="53805-127">TaskInfo オブジェクトのプロパティで指定されたタスク `title` モジュール [のタイトルです](#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="53805-127">The task module's title specified in the `title` property of the [TaskInfo object](#the-taskinfo-object).</span></span>
4. <span data-ttu-id="53805-128">タスク モジュールの [閉じる]/[キャンセル] ボタン。</span><span class="sxs-lookup"><span data-stu-id="53805-128">The task module's close/cancel button.</span></span> <span data-ttu-id="53805-129">ユーザーがこれを押すと、アプリはここで説明する `err` イベントを受信 [します](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)。</span><span class="sxs-lookup"><span data-stu-id="53805-129">If the user presses this, your app will receive an `err` event as described [here](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module).</span></span> <span data-ttu-id="53805-130">(**注:** 現在、タスク モジュールがボットから呼び出された場合、このイベントを検出する機能は使用されません)。</span><span class="sxs-lookup"><span data-stu-id="53805-130">(**Note:** It is currently not possible to detect this event when a task module is invoked from a bot.)</span></span>
5. <span data-ttu-id="53805-131">青色の四角形は、TaskInfo オブジェクトのプロパティを使用して独自の Web ページを読み込む場合に Web ページが `url` [表示される場所です](#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="53805-131">The blue rectangle is the where your web page appears if you are loading your own web page using the `url` property of the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="53805-132">詳細については、後の「 [タスク モジュールのサイズ変更」](#task-module-sizing) セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="53805-132">More detail is in the [task module sizing](#task-module-sizing) section below.</span></span>
6. <span data-ttu-id="53805-133">TaskInfo オブジェクトのプロパティを介してアダプティブ カードを表示している場合は、パディングが追加されます。それ以外の場合は、これを自分 `card` [で処理する必要があります](#task-module-css-for-htmljavascript-task-modules)。 [](#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="53805-133">If you are displaying an Adaptive card via the `card` property of the [TaskInfo object](#the-taskinfo-object) the padding is added for you, otherwise you'll need to [handle this yourself](#task-module-css-for-htmljavascript-task-modules).</span></span>
7. <span data-ttu-id="53805-134">アダプティブ カード ボタンがここに表示されます。</span><span class="sxs-lookup"><span data-stu-id="53805-134">Adaptive card buttons will render here.</span></span> <span data-ttu-id="53805-135">独自のページを使用している場合は、独自のボタンを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="53805-135">If you're using your own page you must create your own buttons.</span></span>

## <a name="overview-of-invoking-and-dismissing-task-modules"></a><span data-ttu-id="53805-136">タスク モジュールの呼び出しと閉じの概要</span><span class="sxs-lookup"><span data-stu-id="53805-136">Overview of invoking and dismissing task modules</span></span>

<span data-ttu-id="53805-137">タスク モジュールは、タブ、ボット、またはディープ リンクから呼び出すことができます。また、1 つに表示される機能は HTML またはアダプティブ カードのいずれかなので、起動方法とユーザーの対話の結果に対処する方法の点で柔軟性が高い。</span><span class="sxs-lookup"><span data-stu-id="53805-137">Task modules can be invoked from tabs, bots or deep links and what appears in one can be either HTML or an Adaptive card, so there's a lot of flexibility in terms of how they are invoked and how to deal with the result of a user's interaction.</span></span> <span data-ttu-id="53805-138">次の表は、この動作の概要を示しています。</span><span class="sxs-lookup"><span data-stu-id="53805-138">The table below summarizes how this works:</span></span>

| <span data-ttu-id="53805-139">**呼び出し方法**</span><span class="sxs-lookup"><span data-stu-id="53805-139">**Invoked via...**</span></span> | <span data-ttu-id="53805-140">**タスク モジュールは HTML/JavaScript です**</span><span class="sxs-lookup"><span data-stu-id="53805-140">**Task module is HTML/JavaScript**</span></span> | <span data-ttu-id="53805-141">**タスク モジュールがアダプティブ カードである**</span><span class="sxs-lookup"><span data-stu-id="53805-141">**Task module is Adaptive card**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="53805-142">**タブ内の JavaScript**</span><span class="sxs-lookup"><span data-stu-id="53805-142">**JavaScript in a tab**</span></span> | <span data-ttu-id="53805-143">1. オプションのコールバック関数で Teams クライアント SDK `tasks.startTask()` 関数を `submitHandler(err, result)` 使用する</span><span class="sxs-lookup"><span data-stu-id="53805-143">1. Use the Teams client SDK function `tasks.startTask()` with an optional `submitHandler(err, result)` callback function</span></span> <br/><br/> <span data-ttu-id="53805-144">2. タスク モジュールのコードで、ユーザーが終了したら、オブジェクトをパラメーターとして Teams SDK `tasks.submitTask()` `result` 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="53805-144">2. In the task module code, when the user is finished, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="53805-145">コールバックが `submitHandler` 指定されている場合 `tasks.startTask()` 、Teams はそれをパラメーターとして `result` 呼び出します。</span><span class="sxs-lookup"><span data-stu-id="53805-145">If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with `result` as a parameter.</span></span><br/><br/> <span data-ttu-id="53805-146">3. 呼び出し中にエラーが発生した場合は、代わりに文字列を使用 `tasks.startTask()` `submitHandler` `err` して関数が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="53805-146">3. If there was an error when invoking `tasks.startTask()`, the `submitHandler` function is called with an `err` string instead.</span></span> <br/><br/> <span data-ttu-id="53805-147">4. 呼び出し時に指定することもできます。その場合は、代わりにボット `completionBotId` `teams.startTask()` `result` に送信されます。</span><span class="sxs-lookup"><span data-stu-id="53805-147">4. You can also specify a `completionBotId` when calling `teams.startTask()` - in that case `result` is sent to the bot instead.</span></span> | <span data-ttu-id="53805-148">1. TaskInfo オブジェクトを使用して Teams クライアント SDK 関数を呼び出し、タスク モジュール ポップアップに表示するアダプティブ カードの `tasks.startTask()` JSON[](#the-taskinfo-object) `TaskInfo.card` を含む。</span><span class="sxs-lookup"><span data-stu-id="53805-148">1. Call the Teams client SDK function `tasks.startTask()` with a [TaskInfo object](#the-taskinfo-object) and `TaskInfo.card` containing the JSON for the Adaptive card to show in the task module popup.</span></span> <br/><br/> <span data-ttu-id="53805-149">2. コールバックが指定されている場合、呼び出し時にエラーが発生した場合、またはユーザーが右上の X を使用してタスク モジュールポップアップを閉じる場合 `submitHandler` `tasks.startTask()` 、Teams は `err` 文字列を使用してコールバックを呼び出します。 `tasks.startTask()`</span><span class="sxs-lookup"><span data-stu-id="53805-149">2. If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with an `err` string if there was an error when invoking `tasks.startTask()` or if the user closes the task module popup using the X at the upper right.</span></span> <br/><br/> <span data-ttu-id="53805-150">3. ユーザーが Action.Submit ボタンを押すと、そのオブジェクトが値 `data` として返されます `result` 。</span><span class="sxs-lookup"><span data-stu-id="53805-150">3. If the user presses an Action.Submit button then its `data` object is returned as the value of `result`.</span></span> |
| <span data-ttu-id="53805-151">**ボット カード ボタン**</span><span class="sxs-lookup"><span data-stu-id="53805-151">**Bot card button**</span></span> | <span data-ttu-id="53805-152">1. ボット カードボタンは、ボタンの種類に応じて、ディープ リンク URL またはメッセージの送信という 2 つの方法でタスク モジュールを呼び出 `task/fetch` します。</span><span class="sxs-lookup"><span data-stu-id="53805-152">1. Bot card buttons, depending on the type of button, can invoke task modules in two ways: a deep link URL or by sending a `task/fetch` message.</span></span> <span data-ttu-id="53805-153">ディープ リンク URL の動作については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="53805-153">See below for how deep link URLs work.</span></span> <br/><br/> <span data-ttu-id="53805-154">2. ボタンのアクションが ( アダプティブ カードのボタンの種類) の場合、イベント (表の下の HTTP POST) がボットに送信され、ボットは `type` `task/fetch` HTTP `Action.Submit` `task/fetch invoke` 200 で POST に応答し [、TaskInfo](#the-taskinfo-object)オブジェクトのラッパーを含む応答本文に応答します。</span><span class="sxs-lookup"><span data-stu-id="53805-154">2. If the button's action `type` is `task/fetch` (`Action.Submit` button type for Adaptive cards), a `task/fetch invoke` event (an HTTP POST under the covers) is sent to the bot, and the bot responds to the POST with HTTP 200 and the response body containing a wrapper around the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="53805-155">これは、タスク/フェッチを介 [してタスク モジュールを呼び出す方法で詳細に説明されています](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch)。</span><span class="sxs-lookup"><span data-stu-id="53805-155">This is explained in detail in [invoking a task module via task/fetch](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch).</span></span><br/><br/> <span data-ttu-id="53805-156">3. Teams はタスク モジュールを表示します。ユーザーが終了したら、オブジェクトをパラメーターとして Teams SDK `tasks.submitTask()` `result` 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="53805-156">3. Teams displays the task module; when the user is finished, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <br/><br/> <span data-ttu-id="53805-157">4. ボットは、オブジェクト `task/submit invoke` を含むメッセージを受信 `result` します。</span><span class="sxs-lookup"><span data-stu-id="53805-157">4. The bot receives a `task/submit invoke` message that contains the `result` object.</span></span> <span data-ttu-id="53805-158">メッセージに応答するには、何もしない (タスクが正常に完了した) 方法、ポップアップ ウィンドウにユーザーにメッセージを表示する方法、または別のタスク モジュール ウィンドウを呼び出す方法 (ウィザードのようなエクスペリエンスの作成) の 3 つの方法があります。 `task/submit`</span><span class="sxs-lookup"><span data-stu-id="53805-158">You have three different ways to respond to the `task/submit` message: by doing nothing (the task completed successfully), by displaying a message to the user in a popup window, or by invoking another task module window (i.e. creating a wizard-like experience).</span></span> <span data-ttu-id="53805-159">これら 3 つのオプションについては、タスク/提出 [に関する詳細な説明で詳しく説明します](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。</span><span class="sxs-lookup"><span data-stu-id="53805-159">These three options are discussed more [in the detailed discussion on task/submit](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> | <span data-ttu-id="53805-160">1. Bot Framework カードのボタンと同様に、アダプティブ カード上のボタンは、タスク モジュールを呼び出す 2 つの方法 (ボタンを含むディープ リンク URL とボタンの使用) をサポートしています `Action.openUrl` `task/fetch` `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="53805-160">1. Like buttons on Bot Framework cards, buttons on Adaptive cards support two ways of invoking task modules: deep link URLs with `Action.openUrl` buttons, and via `task/fetch` using `Action.Submit` buttons.</span></span> <br/><br/> <span data-ttu-id="53805-161">2. アダプティブ カードを含むタスク モジュールは、HTML/JavaScript のケースと非常に似た動作をします (左を参照)。</span><span class="sxs-lookup"><span data-stu-id="53805-161">2. Task modules with Adaptive cards work very similarly to the HTML/JavaScript case (see left).</span></span> <span data-ttu-id="53805-162">主な違いは、アダプティブ カードを使用している場合は JavaScript がないので、呼び出す方法がない点です `tasks.submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="53805-162">The major difference is that since there's no JavaScript when you're using Adaptive cards, there's no way to call `tasks.submitTask()`.</span></span> <span data-ttu-id="53805-163">代わりに、Teams はオブジェクトを取得し、ここで説明するようにイベントの `data` `Action.Submit` `task/submit` ペイロードとして返 [します](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。</span><span class="sxs-lookup"><span data-stu-id="53805-163">Instead, Teams takes the `data` object from `Action.Submit` and returns it as the payload of in the `task/submit` event, as described [here](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> |
| <span data-ttu-id="53805-164">**ディープ リンク URL**</span><span class="sxs-lookup"><span data-stu-id="53805-164">**Deep link URL**</span></span> <br/>[<span data-ttu-id="53805-165">URL 構文</span><span class="sxs-lookup"><span data-stu-id="53805-165">URL syntax</span></span>](#task-module-deep-link-syntax) | <span data-ttu-id="53805-166">1. Teams はタスク モジュールを呼び出します。ディープ リンクのパラメーターで `<iframe>` 指定された内部に表示 `url` される URL。</span><span class="sxs-lookup"><span data-stu-id="53805-166">1. Teams invokes the task module; the URL that appears inside the `<iframe>` specified in the `url` parameter of the deep link.</span></span> <span data-ttu-id="53805-167">コールバック `submitHandler` はありません。</span><span class="sxs-lookup"><span data-stu-id="53805-167">There is no `submitHandler` callback.</span></span> <br/><br/> <span data-ttu-id="53805-168">2. タスク モジュールのページの JavaScript 内で、タブまたはボット カード ボタンから呼び出す場合と同じように、オブジェクトをパラメーターとして呼び出して閉じます。 `tasks.submitTask()` `result`</span><span class="sxs-lookup"><span data-stu-id="53805-168">2. Within the JavaScript of the page in the task module, call `tasks.submitTask()` to close it with a `result` object as a parameter, the same as when invoking it from a tab or a bot card button.</span></span> <span data-ttu-id="53805-169">ただし、完了ロジックは若干異なります。</span><span class="sxs-lookup"><span data-stu-id="53805-169">Completion logic is slightly different, however.</span></span> <span data-ttu-id="53805-170">完了ロジックがクライアント上にある場合 (つまり、ボットがない場合) にはコールバックが存在しないので、呼び出しの前のコードに完了ロジックを含む `submitHandler` 必要があります `tasks.submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="53805-170">If your completion logic resides on the client (i.e. if there is no bot) there is no `submitHandler` callback, so any completion logic must be in the code preceding the call to `tasks.submitTask()`.</span></span> <span data-ttu-id="53805-171">呼び出しエラーは、コンソール経由でのみ報告されます。</span><span class="sxs-lookup"><span data-stu-id="53805-171">Invocation errors are only reported via the console.</span></span> <span data-ttu-id="53805-172">ボットがある場合は、ディープ リンクにパラメーターを指定して、イベントを介して `completionBotId` `result` オブジェクトを送信 `task/submit` できます。</span><span class="sxs-lookup"><span data-stu-id="53805-172">If you have a bot, then you can specify a `completionBotId` parameter in the deep link to send the `result` object via a `task/submit` event.</span></span> | <span data-ttu-id="53805-173">1. Teams はタスク モジュールを呼び出します。アダプティブ カードの JSON カード本文は、ディープ リンクのパラメーターの URL エンコード `card` 値として指定されます。</span><span class="sxs-lookup"><span data-stu-id="53805-173">1. Teams invokes the task module; the JSON card body of the Adaptive card is specified as a URL-encoded value of the `card` parameter of the deep link.</span></span> <br/><br/> <span data-ttu-id="53805-174">2. ユーザーがタスク モジュールを閉じるには、タスク モジュールの右上にある [X] をクリックするか、カードのボタン `Action.Submit` を押します。</span><span class="sxs-lookup"><span data-stu-id="53805-174">2. The user closes the task module by clicking on the X at the upper right of the task module or by pressing an `Action.Submit` button on the card.</span></span> <span data-ttu-id="53805-175">呼び出す必要は何もなから、アダプティブ カード フィールドの値を送信するボット `submitHandler` が必要です。</span><span class="sxs-lookup"><span data-stu-id="53805-175">Since there is no `submitHandler` to call, you must have a bot to send the value of the Adaptive card fields to.</span></span> <span data-ttu-id="53805-176">ディープ リンクの `completionBotId` パラメーターを使用して、イベント経由でデータを送信するボットを指定 `task/submit invoke` します。</span><span class="sxs-lookup"><span data-stu-id="53805-176">You use the `completionBotId` parameter in the deep link to specify the bot to send the data to via a `task/submit invoke` event.</span></span> |

> [!NOTE]
> <span data-ttu-id="53805-177">JavaScript からのタスク モジュールの呼び出しは、モバイルではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="53805-177">Invoking a task module from JavaScript is not supported on mobile.</span></span>

## <a name="the-taskinfo-object"></a><span data-ttu-id="53805-178">TaskInfo オブジェクト</span><span class="sxs-lookup"><span data-stu-id="53805-178">The TaskInfo object</span></span>

<span data-ttu-id="53805-179">オブジェクト `TaskInfo` には、タスク モジュールのメタデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="53805-179">The `TaskInfo` object contains the metadata for a task module.</span></span> <span data-ttu-id="53805-180">オブジェクトの定義を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="53805-180">The object definition is below.</span></span> <span data-ttu-id="53805-181">( **埋** め込み iFrame の場合) または (アダプティブ カード `url` の場合) `card` を定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="53805-181">You **must** define either `url` (for an embedded iFrame) or `card` (for an Adaptive Card).</span></span>

| <span data-ttu-id="53805-182">属性</span><span class="sxs-lookup"><span data-stu-id="53805-182">Attribute</span></span> | <span data-ttu-id="53805-183">種類</span><span class="sxs-lookup"><span data-stu-id="53805-183">Type</span></span> | <span data-ttu-id="53805-184">説明</span><span class="sxs-lookup"><span data-stu-id="53805-184">Description</span></span> |
| --- | --- | --- |
| `title` | <span data-ttu-id="53805-185">string</span><span class="sxs-lookup"><span data-stu-id="53805-185">string</span></span> | <span data-ttu-id="53805-186">アプリ名の下とアプリ アイコンの右側に表示されます。</span><span class="sxs-lookup"><span data-stu-id="53805-186">Appears below the app name and to the right of the app icon</span></span> |
| `height` | <span data-ttu-id="53805-187">number または string</span><span class="sxs-lookup"><span data-stu-id="53805-187">number or string</span></span> | <span data-ttu-id="53805-188">タスク モジュールの高さをピクセル単位で表す数値、または 、または `small` `medium` `large` .</span><span class="sxs-lookup"><span data-stu-id="53805-188">This can be a number representing the task module's height in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="53805-189">[高さと幅の処理方法については、以下を参照してください](#task-module-sizing)。</span><span class="sxs-lookup"><span data-stu-id="53805-189">[See below for how height and width are handled](#task-module-sizing).</span></span> |
| `width` | <span data-ttu-id="53805-190">number または string</span><span class="sxs-lookup"><span data-stu-id="53805-190">number or string</span></span> | <span data-ttu-id="53805-191">タスク モジュールの幅をピクセル単位で表す数値、または 、または `small` `medium` `large` .</span><span class="sxs-lookup"><span data-stu-id="53805-191">This can be a number representing the task module's width in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="53805-192">[高さと幅の処理方法については、以下を参照してください](#task-module-sizing)。</span><span class="sxs-lookup"><span data-stu-id="53805-192">[See below for how height and width are handled](#task-module-sizing).</span></span> |
| `url` | <span data-ttu-id="53805-193">string</span><span class="sxs-lookup"><span data-stu-id="53805-193">string</span></span> | <span data-ttu-id="53805-194">タスク モジュール内に読み込 `<iframe>` まれるページの URL。</span><span class="sxs-lookup"><span data-stu-id="53805-194">The URL of the page loaded as an `<iframe>` inside the task module.</span></span> <span data-ttu-id="53805-195">URL のドメインは、アプリのマニフェスト内の [アプリの validDomains](~/resources/schema/manifest-schema.md#validdomains) 配列に含む必要があります。</span><span class="sxs-lookup"><span data-stu-id="53805-195">The URL's domain must be in the app's [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in your app's manifest.</span></span> |
| `card` | <span data-ttu-id="53805-196">アダプティブ カードまたはアダプティブ カードボット カードの添付ファイル</span><span class="sxs-lookup"><span data-stu-id="53805-196">Adaptive card or an Adaptive card bot card attachment</span></span> | <span data-ttu-id="53805-197">タスク モジュールに表示されるアダプティブ カードの JSON。</span><span class="sxs-lookup"><span data-stu-id="53805-197">The JSON for the Adaptive card to appear in the task module.</span></span> <span data-ttu-id="53805-198">ボットから呼び出す場合は、Bot Framework オブジェクトでアダプティブ カード JSON を使用する必要 `attachment` があります。</span><span class="sxs-lookup"><span data-stu-id="53805-198">If you're invoking from a bot, you'll need to use the Adaptive card JSON in a Bot Framework `attachment` object.</span></span> <span data-ttu-id="53805-199">タブからアダプティブ カードを使用します。</span><span class="sxs-lookup"><span data-stu-id="53805-199">From a tab you'll use just an Adaptive Card.</span></span> [<span data-ttu-id="53805-200">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="53805-200">Here's an example.</span></span>](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | <span data-ttu-id="53805-201">string</span><span class="sxs-lookup"><span data-stu-id="53805-201">string</span></span> | <span data-ttu-id="53805-202">クライアントがタスク モジュール機能をサポートしていない場合、この URL はブラウザー タブで開きます。</span><span class="sxs-lookup"><span data-stu-id="53805-202">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |
| `completionBotId` | <span data-ttu-id="53805-203">string</span><span class="sxs-lookup"><span data-stu-id="53805-203">string</span></span> | <span data-ttu-id="53805-204">タスク モジュールとのユーザーの対話の結果を送信するボット アプリ ID を指定します。</span><span class="sxs-lookup"><span data-stu-id="53805-204">Specifies a bot App ID to send the result of the user's interaction with the task module to.</span></span> <span data-ttu-id="53805-205">指定した場合、ボットはイベント ペイロードに `task/submit invoke` JSON オブジェクトを含むイベントを受信します。</span><span class="sxs-lookup"><span data-stu-id="53805-205">If specified, the bot will receive a `task/submit invoke` event with a JSON object in the event payload.</span></span> |

> [!NOTE]
> <span data-ttu-id="53805-206">タスク モジュール機能では、読み込む URL のドメインがアプリのマニフェストの配列 `validDomains` に含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="53805-206">The task module feature requires that the domains of any URLs you want to load are included in the `validDomains` array in your app's manifest.</span></span>

## <a name="task-module-sizing"></a><span data-ttu-id="53805-207">タスク モジュールのサイズ変更</span><span class="sxs-lookup"><span data-stu-id="53805-207">Task module sizing</span></span>

<span data-ttu-id="53805-208">高さと幅を `TaskInfo.width` `TaskInfo.height` ピクセル単位で設定する整数を使用します。</span><span class="sxs-lookup"><span data-stu-id="53805-208">Using integers for `TaskInfo.width` and `TaskInfo.height` will set the height and width in pixels.</span></span> <span data-ttu-id="53805-209">ただし、チームのウィンドウのサイズと画面解像度に応じて、縦横比 (幅/高さ) を維持しながら、比例して縮小されます。</span><span class="sxs-lookup"><span data-stu-id="53805-209">However, depending on the size of the Team's window and screen resolution they will be reduced proportionally while maintaining the aspect ratio (width/height).</span></span>

<span data-ttu-id="53805-210">If `TaskInfo.width` and are, or the size of the red rectangle in the picture above is a proportion of the available `TaskInfo.height` `"small"` `"medium"` `"large"` space: 20%, 50%, 60% `width` for and 20%, 50%, 66% for `height` .</span><span class="sxs-lookup"><span data-stu-id="53805-210">If `TaskInfo.width` and `TaskInfo.height` are `"small"`, `"medium"` or `"large"` the size of the red rectangle in the picture above is a proportion of the available space: 20%, 50%, 60% for `width` and 20%, 50%, 66% for `height`.</span></span>

<span data-ttu-id="53805-211">タブから呼び出されるタスク モジュールは、動的にサイズ変更できます。</span><span class="sxs-lookup"><span data-stu-id="53805-211">Task modules invoked from a tab can be dynamically resized.</span></span> <span data-ttu-id="53805-212">呼び `tasks.startTask()` 出した後、newSize オブジェクトの高さと幅のプロパティが TaskInfo 仕様 `tasks.updateTask(newSize)` (例:</span><span class="sxs-lookup"><span data-stu-id="53805-212">After calling `tasks.startTask()` you can call `tasks.updateTask(newSize)` where height and width properties on the newSize object conform to the TaskInfo spec (ex.</span></span> <span data-ttu-id="53805-213">`{ height: 'medium', width: 'medium' }`).</span><span class="sxs-lookup"><span data-stu-id="53805-213">`{ height: 'medium', width: 'medium' }`).</span></span>

## <a name="task-module-css-for-htmljavascript-task-modules"></a><span data-ttu-id="53805-214">HTML/JavaScript タスク モジュール用のタスク モジュール CSS</span><span class="sxs-lookup"><span data-stu-id="53805-214">Task module CSS for HTML/JavaScript task modules</span></span>

<span data-ttu-id="53805-215">HTML/JavaScript ベースのタスク モジュールは、ヘッダーの下のタスク モジュールの領域全体にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="53805-215">HTML/JavaScript-based task modules have access to the entire area of the task module below the header.</span></span> <span data-ttu-id="53805-216">これは大きな柔軟性を提供しますが、ヘッダー要素に合わせてエッジの周囲のパディングを使用し、不要なスクロール バーを回避する場合は、適切な CSS を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="53805-216">While that offers a great deal of flexibility, if you want padding around the edges to align with the header elements and avoid unnecessary scrollbars you'll need to provide the right CSS.</span></span> <span data-ttu-id="53805-217">いくつかの使用例の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="53805-217">Here are some examples for a few use cases.</span></span>

### <a name="example-1---youtube-video"></a><span data-ttu-id="53805-218">例 1 - YouTube ビデオ</span><span class="sxs-lookup"><span data-stu-id="53805-218">Example 1 - YouTube video</span></span>

<span data-ttu-id="53805-219">YouTube には、Web ページにビデオを埋め込む機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="53805-219">YouTube offers the ability to embed videos on web pages.</span></span> <span data-ttu-id="53805-220">単純なスタブ Web ページを使用すると、タスク モジュールで簡単に表示できます。</span><span class="sxs-lookup"><span data-stu-id="53805-220">Using a simple stub web page it's easy to show this in a task module:</span></span>

![YouTube ビデオ](~/assets/images/task-module/youtube-example.png)

<span data-ttu-id="53805-222">CSS を含めずに、このページの HTML を次に示します。</span><span class="sxs-lookup"><span data-stu-id="53805-222">Here's the HTML for this page, without the CSS:</span></span>

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

<span data-ttu-id="53805-223">CSS は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="53805-223">The CSS looks like this:</span></span>

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

### <a name="example-2---powerapp"></a><span data-ttu-id="53805-224">例 2 - PowerApp</span><span class="sxs-lookup"><span data-stu-id="53805-224">Example 2 - PowerApp</span></span>

<span data-ttu-id="53805-225">PowerApp を埋め込む場合も、同じ方法を使用できます。</span><span class="sxs-lookup"><span data-stu-id="53805-225">You can use the same approach to embed a PowerApp as well.</span></span> <span data-ttu-id="53805-226">個々の PowerApp の高さ/幅はカスタマイズ可能であり、目的のプレゼンテーションを実現するために高さと幅を調整する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="53805-226">As the height/width of any individual PowerApp is customizable, you may need to adjust the height and width to achieve your desired presentation.</span></span>

![Asset Management PowerApp](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

<span data-ttu-id="53805-228">CSS は次の要素です。</span><span class="sxs-lookup"><span data-stu-id="53805-228">And the CSS is:</span></span>

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a><span data-ttu-id="53805-229">アダプティブ カードまたはアダプティブ カードボット カードの添付ファイル</span><span class="sxs-lookup"><span data-stu-id="53805-229">Adaptive card or Adaptive card bot card attachment</span></span>

<span data-ttu-id="53805-230">前に説明したように、呼び出し方法に応じて、アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル (添付ファイル オブジェクトにラップされたアダプティブ カード) を使用する必要があります `card` 。</span><span class="sxs-lookup"><span data-stu-id="53805-230">As we noted above, depending on how you're invoking your `card` you'll need to use either an Adaptive card, or an Adaptive card bot card attachment (which is just an Adaptive card wrapped in an attachment object).</span></span>

<span data-ttu-id="53805-231">タブから呼び出す場合は、アダプティブ カードを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="53805-231">When you're invoking from a tab, you'll need to use an adaptive card.</span></span> <span data-ttu-id="53805-232">次に、非常に簡単な例を示します。</span><span class="sxs-lookup"><span data-stu-id="53805-232">Here's a very simple example:</span></span>

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

<span data-ttu-id="53805-233">ボットから呼び出す場合は、次の例に示すアダプティブ カード ボット カードの添付ファイルを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="53805-233">When you're invoking from a bot you'll need to use an Adaptive card bot card attachment as in the example below:</span></span>

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

<span data-ttu-id="53805-234">アダプティブ カードを含むタスク モジュールをボットから呼び出すのか、タブから呼び出すのかを覚えておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="53805-234">You'll need to remember whether you are invoking a task module containing an Adaptive card from a bot or a tab.</span></span>

## <a name="task-module-deep-link-syntax"></a><span data-ttu-id="53805-235">タスク モジュールのディープ リンク構文</span><span class="sxs-lookup"><span data-stu-id="53805-235">Task module deep link syntax</span></span>

<span data-ttu-id="53805-236">タスク モジュールのディープ リンクは、他の 2 つの情報と、オプションで次の 2 つの情報を持つ [TaskInfo](#the-taskinfo-object) オブジェクトのシリアル化 `APP_ID` です `BOT_APP_ID` 。</span><span class="sxs-lookup"><span data-stu-id="53805-236">A task module deep link is just a serialization of the [TaskInfo object](#the-taskinfo-object) with two other pieces of information, `APP_ID` and optionally the `BOT_APP_ID`:</span></span>

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

<span data-ttu-id="53805-237">データ [型、および使用可能な値については、TaskInfo](#the-taskinfo-object) オブジェクトを参照してください `<TaskInfo.url>` `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` 。</span><span class="sxs-lookup"><span data-stu-id="53805-237">See [TaskInfo object](#the-taskinfo-object) for the data types and allowable values for `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`, and `<TaskInfo.title>`.</span></span>

> [!TIP]
> <span data-ttu-id="53805-238">特にパラメーター (JavaScript の関数など) を使用する場合は、必ず URL でディープ リンク `card` をエンコード[ `encodeURI()` してください](https://www.w3schools.com/jsref/jsref_encodeURI.asp)。</span><span class="sxs-lookup"><span data-stu-id="53805-238">Be sure to URL encode the deep link, especially when using the `card` parameter (for example, JavaScript's [`encodeURI()` function](https://www.w3schools.com/jsref/jsref_encodeURI.asp)).</span></span>

<span data-ttu-id="53805-239">以下に情報を示 `APP_ID` します `BOT_APP_ID` 。</span><span class="sxs-lookup"><span data-stu-id="53805-239">Here's the information on `APP_ID` and `BOT_APP_ID`:</span></span>

| <span data-ttu-id="53805-240">値</span><span class="sxs-lookup"><span data-stu-id="53805-240">Value</span></span> | <span data-ttu-id="53805-241">型</span><span class="sxs-lookup"><span data-stu-id="53805-241">Type</span></span> | <span data-ttu-id="53805-242">必須</span><span class="sxs-lookup"><span data-stu-id="53805-242">Required?</span></span> | <span data-ttu-id="53805-243">説明</span><span class="sxs-lookup"><span data-stu-id="53805-243">Description</span></span> |
| --- | --- | --- | --- |
| `APP_ID` | <span data-ttu-id="53805-244">string</span><span class="sxs-lookup"><span data-stu-id="53805-244">string</span></span> | <span data-ttu-id="53805-245">はい</span><span class="sxs-lookup"><span data-stu-id="53805-245">Yes</span></span> | <span data-ttu-id="53805-246">タスク モジュールを呼び出すアプリの[ID。](~/resources/schema/manifest-schema.md#id)</span><span class="sxs-lookup"><span data-stu-id="53805-246">The [id](~/resources/schema/manifest-schema.md#id) of the app invoking the task module.</span></span> <span data-ttu-id="53805-247">マニフェスト [の validDomains 配列](~/resources/schema/manifest-schema.md#validdomains) には、URL に if のドメイン `APP_ID` `url` `url` が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="53805-247">The [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in the manifest for `APP_ID` must contain the domain for `url` if `url` is in the URL.</span></span> <span data-ttu-id="53805-248">(アプリ ID は、タスク モジュールがタブまたはボットから呼び出された場合に既に知られています。これは、それが含まれていない理由 `TaskInfo` です)。</span><span class="sxs-lookup"><span data-stu-id="53805-248">(The app ID is already known when a task module is invoked from a tab or a bot, which is why it's not included in `TaskInfo`.)</span></span> |
| `BOT_APP_ID` | <span data-ttu-id="53805-249">文字列</span><span class="sxs-lookup"><span data-stu-id="53805-249">string</span></span> | <span data-ttu-id="53805-250">いいえ</span><span class="sxs-lookup"><span data-stu-id="53805-250">No</span></span> | <span data-ttu-id="53805-251">値が指定 `completionBotId` されている場合、オブジェクトはメッセージを介して指定 `result` `task/submit invoke` されたボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="53805-251">If a value for `completionBotId` is specified, the `result` object is sent via a a `task/submit invoke` message to the specified bot.</span></span> <span data-ttu-id="53805-252">`BOT_APP_ID` は、アプリのマニフェストでボットとして指定する必要があります。つまり、ボットに送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="53805-252">`BOT_APP_ID` must be specified as a bot in the app's manifest, i.e. you can't just send it to any bot.</span></span> |

<span data-ttu-id="53805-253">これは有効であり、同じであり、多くの場合、アプリがボットを持っている場合は、ボットがある場合はアプリの ID として使用する必要があります。 `APP_ID` `BOT_APP_ID`</span><span class="sxs-lookup"><span data-stu-id="53805-253">Note that it's valid for `APP_ID` and `BOT_APP_ID` to be the same, and in many cases will be if an app has a bot since it's recommended to use that as an app's ID if there is one.</span></span>

## <a name="keyboard-and-accessibility-guidelines"></a><span data-ttu-id="53805-254">キーボードとアクセシビリティのガイドライン</span><span class="sxs-lookup"><span data-stu-id="53805-254">Keyboard and accessibility guidelines</span></span>

<span data-ttu-id="53805-255">HTML/JavaScript ベースのタスク モジュールでは、アプリのタスク モジュールをキーボードで使用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="53805-255">With HTML/JavaScript-based task modules it is your responsibility to ensure your app's task module can be used with a keyboard.</span></span> <span data-ttu-id="53805-256">スクリーン リーダー プログラムは、キーボードを使用して移動する機能にも依存します。</span><span class="sxs-lookup"><span data-stu-id="53805-256">Screen reader programs also depend on the ability to navigate using the keyboard.</span></span> <span data-ttu-id="53805-257">実際には、これは次の 2 つのことを意味します。</span><span class="sxs-lookup"><span data-stu-id="53805-257">As a practical matter this means two things:</span></span>

1. <span data-ttu-id="53805-258">HTML タグ [で tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) 属性を使用して、フォーカスできる要素と、シーケンシャル キーボード ナビゲーションに参加する場合/参加する場所を制御します (通常 <kbd>、Tab</kbd> キーと <kbd>Shift キー</kbd> を使用)。</span><span class="sxs-lookup"><span data-stu-id="53805-258">Using the [tabindex attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) in your HTML tags to control which elements can be focused and if/where it participates in sequential keyboard navigation (usually with the <kbd>Tab</kbd> and <kbd>Shift-Tab</kbd> keys).</span></span>
2. <span data-ttu-id="53805-259">タスク モジュール <kbd>の JavaScript</kbd> で Esc キーを処理します。</span><span class="sxs-lookup"><span data-stu-id="53805-259">Handling the <kbd>Esc</kbd> key in the JavaScript for your task module.</span></span> <span data-ttu-id="53805-260">これを行う方法を示すコード サンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="53805-260">Here's a code sample showing how to do this:</span></span>

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

<span data-ttu-id="53805-261">Microsoft Teams は、タスク モジュール ヘッダーから HTML へのキーボード ナビゲーションが正しく機能し、その逆も正しく動作します。</span><span class="sxs-lookup"><span data-stu-id="53805-261">Microsoft Teams will ensure that keyboard navigation works properly from the task module header into your HTML and vice-versa.</span></span>

## <a name="task-module-samples"></a><span data-ttu-id="53805-262">タスク モジュールのサンプル</span><span class="sxs-lookup"><span data-stu-id="53805-262">Task module samples</span></span>

* [<span data-ttu-id="53805-263">Node.js/TypeScript サンプル</span><span class="sxs-lookup"><span data-stu-id="53805-263">Node.js/TypeScript sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs)
* [<span data-ttu-id="53805-264">C#/.NET サンプル</span><span class="sxs-lookup"><span data-stu-id="53805-264">C#/.NET sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp)

> [!div class="nextstepaction"]
> [<span data-ttu-id="53805-265">詳細については、デバイスのアクセス許可の要求を参照してください</span><span class="sxs-lookup"><span data-stu-id="53805-265">Learn  more: Request device permissions</span></span>](../concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="53805-266">詳細: メディア機能の統合</span><span class="sxs-lookup"><span data-stu-id="53805-266">Learn more: Integrate media capabilities</span></span>](../concepts/device-capabilities/mobile-camera-image-permissions.md)
