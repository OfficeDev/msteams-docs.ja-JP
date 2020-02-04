---
title: タスクモジュールとは
author: clearab
description: Microsoft Teams アプリからユーザーに情報を収集または表示するためのモーダルポップアップエクスペリエンスを追加します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 22fdc7a9dab1ff6f27e2b0d144e54676b6cca50e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675060"
---
# <a name="what-are-task-modules"></a><span data-ttu-id="85730-103">タスクモジュールとは</span><span class="sxs-lookup"><span data-stu-id="85730-103">What are task modules?</span></span>

<span data-ttu-id="85730-104">タスクモジュールを使用すると、Teams アプリケーションでモーダルポップアップエクスペリエンスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="85730-104">Task modules allow you to create modal popup experiences in your Teams application.</span></span> <span data-ttu-id="85730-105">ポップアップの内部では、独自のカスタム HTML/JavaScript コードを実行し`<iframe>`たり、YouTube や Microsoft Stream ビデオなどのベースのウィジェットを表示したり、[アダプティブカード](/adaptive-cards/)を表示したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="85730-105">Inside the popup you can run your own custom HTML/JavaScript code, show an `<iframe>`-based widget such as a YouTube or Microsoft Stream video or display an [Adaptive card](/adaptive-cards/).</span></span> <span data-ttu-id="85730-106">これらは特に、タスクを開始および完了したり、ビデオや Power BI ダッシュボードのようなリッチ情報を表示したりするのに便利です。</span><span class="sxs-lookup"><span data-stu-id="85730-106">They are especially useful for initiating and completing tasks or displaying rich information like videos or Power BI dashboards.</span></span> <span data-ttu-id="85730-107">多くの場合、ポップアップは、タブや会話ベースのボットのようなタスクを開始および完了するユーザーのために、より自然に表示されます。</span><span class="sxs-lookup"><span data-stu-id="85730-107">A popup experience is often more natural for users initiating and completing tasks compared to a tab or a conversation-based bot experience.</span></span>

<span data-ttu-id="85730-108">タスクモジュールは、Microsoft Teams のタブの基礎に基づいて構築されています。これらは基本的にはポップアップウィンドウ内のタブです。</span><span class="sxs-lookup"><span data-stu-id="85730-108">Task modules build on the foundation of Microsoft Teams tabs; they are essentially a tab inside a popup window.</span></span> <span data-ttu-id="85730-109">これらは同じ SDK を使用します。そのため、タブを構築した場合は、タスクモジュールを作成する方法が既に90% になっています。</span><span class="sxs-lookup"><span data-stu-id="85730-109">They use the same SDK, so if you've built a tab you are already 90% of the way to being able to create a task module.</span></span>

<span data-ttu-id="85730-110">タスクモジュールは、次の3つの方法で呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="85730-110">Task modules can be invoked in three ways:</span></span>

* <span data-ttu-id="85730-111">**チャネルまたは個人用タブ。**</span><span class="sxs-lookup"><span data-stu-id="85730-111">**Channel or personal tabs.**</span></span> <span data-ttu-id="85730-112">Microsoft Teams のタブ SDK を使用すると、タブのボタン、リンク、またはメニューからタスクモジュールを呼び出すことができます。[これについては、ここで詳しく説明し](~/task-modules-and-cards/task-modules/task-modules-tabs.md)ます。</span><span class="sxs-lookup"><span data-stu-id="85730-112">Using the Microsoft Teams Tabs SDK you can invoke task modules from buttons, links or menus on your tab. [This is covered in detail here.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)</span></span>
* <span data-ttu-id="85730-113">**Bot.**</span><span class="sxs-lookup"><span data-stu-id="85730-113">**Bots.**</span></span> <span data-ttu-id="85730-114">Bot から送信された[カード](~/task-modules-and-cards/cards/cards-reference.md)のボタン。</span><span class="sxs-lookup"><span data-stu-id="85730-114">Buttons on [cards](~/task-modules-and-cards/cards/cards-reference.md) sent from your bot.</span></span> <span data-ttu-id="85730-115">これは、ユーザーが bot を使用していることを確認するためにチャネル内のすべてのユーザーが必要ない場合に特に便利です。</span><span class="sxs-lookup"><span data-stu-id="85730-115">This is particularly useful when you don't need everyone in a channel to see what you are doing with a bot.</span></span> <span data-ttu-id="85730-116">たとえば、ユーザーがチャネル内の投票に応答する場合、作成中の投票の記録を表示するのはそれほど便利ではありません。</span><span class="sxs-lookup"><span data-stu-id="85730-116">For example, when having users respond to a poll in a channel it's not terribly useful to see a record of that poll being created.</span></span> [<span data-ttu-id="85730-117">これについては、ここで詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="85730-117">This is covered in detail here.</span></span>](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* <span data-ttu-id="85730-118">**深いリンクから Teams の外側。**</span><span class="sxs-lookup"><span data-stu-id="85730-118">**Outside of Teams from a deep link.**</span></span> <span data-ttu-id="85730-119">任意の場所からタスクモジュールを呼び出すための Url を作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="85730-119">You can also create URLs to invoke a task module from anywhere.</span></span> [<span data-ttu-id="85730-120">これについては、ここで詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="85730-120">This is covered in detail here.</span></span>](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a><span data-ttu-id="85730-121">タスクモジュールの外観</span><span class="sxs-lookup"><span data-stu-id="85730-121">What a task module looks like</span></span>

<span data-ttu-id="85730-122">Bot から呼び出された場合のタスクモジュールは次のようになります (色の付いた長方形と番号付き円はありません)。</span><span class="sxs-lookup"><span data-stu-id="85730-122">Here's what a task module looks like when invoked from a bot (without the colored rectangles and numbered circles, of course):</span></span>

![タスクモジュールの例](~/assets/images/task-module/task-module-example.png)

<span data-ttu-id="85730-124">これについて説明します。</span><span class="sxs-lookup"><span data-stu-id="85730-124">Let's walk through it:</span></span>

1. <span data-ttu-id="85730-125">アプリの[ `color`アイコン](~/resources/schema/manifest-schema.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="85730-125">Your app's [`color` icon](~/resources/schema/manifest-schema.md#icons).</span></span>
2. <span data-ttu-id="85730-126">アプリの[ `short`名前](~/resources/schema/manifest-schema.md#name)。</span><span class="sxs-lookup"><span data-stu-id="85730-126">Your app's [`short` name](~/resources/schema/manifest-schema.md#name).</span></span>
3. <span data-ttu-id="85730-127">`title` [Taskinfo オブジェクト](#the-taskinfo-object)のプロパティで指定されたタスクモジュールのタイトル。</span><span class="sxs-lookup"><span data-stu-id="85730-127">The task module's title specified in the `title` property of the [TaskInfo object](#the-taskinfo-object).</span></span>
4. <span data-ttu-id="85730-128">タスクモジュールの [閉じる/キャンセル] ボタン。</span><span class="sxs-lookup"><span data-stu-id="85730-128">The task module's close/cancel button.</span></span> <span data-ttu-id="85730-129">ユーザーがこのコードを押すと、[ここで](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)説明`err`したように、アプリはイベントを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="85730-129">If the user presses this, your app will receive an `err` event as described [here](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module).</span></span> <span data-ttu-id="85730-130">(現時点では、タスクモジュールが bot から呼び出されたとき**に、この**イベントを検出することはできません)。</span><span class="sxs-lookup"><span data-stu-id="85730-130">(**Note:** It is currently not possible to detect this event when a task module is invoked from a bot.)</span></span>
5. <span data-ttu-id="85730-131">青い四角形は、 `url` [taskinfo オブジェクト](#the-taskinfo-object)のプロパティを使用して独自の web ページを読み込む場合に、web ページが表示される場所です。</span><span class="sxs-lookup"><span data-stu-id="85730-131">The blue rectangle is the where your web page appears if you are loading your own web page using the `url` property of the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="85730-132">詳細については、以下の「[タスクモジュールのサイズ変更](#task-module-sizing)」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="85730-132">More detail is in the [task module sizing](#task-module-sizing) section below.</span></span>
6. <span data-ttu-id="85730-133">`card` [Taskinfo オブジェクト](#the-taskinfo-object)のプロパティを使用してアダプティブカードを表示している場合は、スペースが自動的に追加されます。それ以外の場合は、[自分で処理](#task-module-css-for-htmljavascript-task-modules)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85730-133">If you are displaying an Adaptive card via the `card` property of the [TaskInfo object](#the-taskinfo-object) the padding is added for you, otherwise you'll need to [handle this yourself](#task-module-css-for-htmljavascript-task-modules).</span></span>
7. <span data-ttu-id="85730-134">アダプティブカードボタンがここに表示されます。</span><span class="sxs-lookup"><span data-stu-id="85730-134">Adaptive card buttons will render here.</span></span> <span data-ttu-id="85730-135">独自のページを使用している場合は、独自のボタンを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85730-135">If you're using your own page you must create your own buttons.</span></span>

## <a name="overview-of-invoking-and-dismissing-task-modules"></a><span data-ttu-id="85730-136">タスクモジュールの呼び出しと消去の概要</span><span class="sxs-lookup"><span data-stu-id="85730-136">Overview of invoking and dismissing task modules</span></span>

<span data-ttu-id="85730-137">タスクモジュールは、タブ、ボット、またはディープリンクから呼び出すことができ、一方で表示されるものは HTML またはアダプティブカードのどちらかになります。そのため、その呼び出し方法やユーザー操作の結果を処理する方法について、柔軟性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="85730-137">Task modules can be invoked from tabs, bots or deep links and what appears in one can be either HTML or an Adaptive card, so there's a lot of flexibility in terms of how they are invoked and how to deal with the result of a user's interaction.</span></span> <span data-ttu-id="85730-138">次の表は、この機能の概要を示しています。</span><span class="sxs-lookup"><span data-stu-id="85730-138">The table below summarizes how this works:</span></span>

| <span data-ttu-id="85730-139">**呼び出しを経由する...**</span><span class="sxs-lookup"><span data-stu-id="85730-139">**Invoked via...**</span></span> | <span data-ttu-id="85730-140">**タスクモジュールは HTML/JavaScript**</span><span class="sxs-lookup"><span data-stu-id="85730-140">**Task module is HTML/JavaScript**</span></span> | <span data-ttu-id="85730-141">**タスクモジュールはアダプティブカード**</span><span class="sxs-lookup"><span data-stu-id="85730-141">**Task module is Adaptive card**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85730-142">**タブ内の JavaScript**</span><span class="sxs-lookup"><span data-stu-id="85730-142">**JavaScript in a tab**</span></span> | <span data-ttu-id="85730-143">1. オプション`submitHandler(err, result)`のコールバック関数で`tasks.startTask()` Teams クライアント SDK 関数を使用する</span><span class="sxs-lookup"><span data-stu-id="85730-143">1. Use the Teams client SDK function `tasks.startTask()` with an optional `submitHandler(err, result)` callback function</span></span> <br/><br/> <span data-ttu-id="85730-144">2. タスクモジュールコードで、ユーザーが終了したら、 `tasks.submitTask()` `result`オブジェクトをパラメーターとして Teams SDK 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="85730-144">2. In the task module code, when the user is finished, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="85730-145">で`submitHandler` `tasks.startTask()`コールバックが指定されていた場合`result` 、Teams はそれをパラメーターとして呼び出します。</span><span class="sxs-lookup"><span data-stu-id="85730-145">If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with `result` as a parameter.</span></span><br/><br/> <span data-ttu-id="85730-146">3. 呼び出し`tasks.startTask()`時にエラーが発生した場合`submitHandler`は、代わりに`err`文字列で関数が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="85730-146">3. If there was an error when invoking `tasks.startTask()`, the `submitHandler` function is called with an `err` string instead.</span></span> <br/><br/> <span data-ttu-id="85730-147">4. そのケースを呼び出し`completionBotId` `teams.startTask()`たときに、そのケース`result`を bot に送信するように指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="85730-147">4. You can also specify a `completionBotId` when calling `teams.startTask()` - in that case `result` is sent to the bot instead.</span></span> | <span data-ttu-id="85730-148">1. [Taskinfo オブジェクト](#the-taskinfo-object)を使用し`tasks.startTask()`て Teams クライアント SDK 関数を`TaskInfo.card`呼び出し、[タスクモジュール] ポップアップに表示するアダプティブカードの JSON を格納します。</span><span class="sxs-lookup"><span data-stu-id="85730-148">1. Call the Teams client SDK function `tasks.startTask()` with a [TaskInfo object](#the-taskinfo-object) and `TaskInfo.card` containing the JSON for the Adaptive card to show in the task module popup.</span></span> <br/><br/> <span data-ttu-id="85730-149">2 `submitHandler` . で`tasks.startTask()`コールバックが指定されていた場合、 `err`を呼び出したときにエラーが発生`tasks.startTask()`した場合、またはユーザーが右上の X を使用してタスクモジュールのポップアップを閉じた場合、Teams は文字列を使用して呼び出します。</span><span class="sxs-lookup"><span data-stu-id="85730-149">2. If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with an `err` string if there was an error when invoking `tasks.startTask()` or if the user closes the task module popup using the X at the upper right.</span></span> <br/><br/> <span data-ttu-id="85730-150">3. ユーザーが [送信] ボタンを押すと、その`data`オブジェクトはの`result`値として返されます。</span><span class="sxs-lookup"><span data-stu-id="85730-150">3. If the user presses an Action.Submit button then its `data` object is returned as the value of `result`.</span></span> |
| <span data-ttu-id="85730-151">**[ボットカード] ボタン**</span><span class="sxs-lookup"><span data-stu-id="85730-151">**Bot card button**</span></span> | <span data-ttu-id="85730-152">1つのボットカードボタンは、ボタンの種類に応じて、ディープリンク URL、またはメッセージを`task/fetch`送信する2つの方法で、タスクモジュールを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="85730-152">1. Bot card buttons, depending on the type of button, can invoke task modules in two ways: a deep link URL or by sending a `task/fetch` message.</span></span> <span data-ttu-id="85730-153">深いリンク Url のしくみについては、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85730-153">See below for how deep link URLs work.</span></span> <br/><br/> <span data-ttu-id="85730-154">2. ボタンの`type`アクション`task/fetch` (`Action.Submit`アダプティブカード用のボタンの種類) がある場合`task/fetch invoke`は、bot にイベント (カバーの下の HTTP POST) が送信され、bot は http 200 を使用して post に応答し、ボットは[taskinfo オブジェクト](#the-taskinfo-object)のラッパーを含む応答本文に応答します。</span><span class="sxs-lookup"><span data-stu-id="85730-154">2. If the button's action `type` is `task/fetch` (`Action.Submit` button type for Adaptive cards), a `task/fetch invoke` event (an HTTP POST under the covers) is sent to the bot, and the bot responds to the POST with HTTP 200 and the response body containing a wrapper around the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="85730-155">これについては[、「task/fetch を使用してタスクモジュールを呼び出す](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch)」で詳しく説明されています。</span><span class="sxs-lookup"><span data-stu-id="85730-155">This is explained in detail in [invoking a task module via task/fetch](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch).</span></span><br/><br/> <span data-ttu-id="85730-156">3. Teams には、タスクモジュールが表示されます。ユーザーが終了したら、 `tasks.submitTask()` `result`オブジェクトをパラメーターとして Teams SDK 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="85730-156">3. Teams displays the task module; when the user is finished, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <br/><br/> <span data-ttu-id="85730-157">4. この bot は、 `task/submit invoke` `result`オブジェクトを含むメッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="85730-157">4. The bot receives a `task/submit invoke` message that contains the `result` object.</span></span> <span data-ttu-id="85730-158">`task/submit`メッセージに返信するには、次の3つの方法があります。そのためには、何もしない (タスクが正常に完了した) か、ユーザーにメッセージをポップアップウィンドウで表示するか、または別のタスクモジュールウィンドウ (つまりウィザードのような操作を作成する) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="85730-158">You have three different ways to respond to the `task/submit` message: by doing nothing (the task completed successfully), by displaying a message to the user in a popup window, or by invoking another task module window (i.e. creating a wizard-like experience).</span></span> <span data-ttu-id="85730-159">この3つのオプションについ[ては、「タスク/送信に関する詳細な説明」](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85730-159">These three options are discussed more [in the detailed discussion on task/submit](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> | <span data-ttu-id="85730-160">1. Bot フレームワークカードのボタンと同様に、アダプティブカード上のボタンは、タスクモジュールを呼び出すための`Action.openUrl` 2 つの方法`task/fetch`を`Action.Submit`サポートしています。ボタンを使用した深いリンク url とボタンを使用する方法です。</span><span class="sxs-lookup"><span data-stu-id="85730-160">1. Like buttons on Bot Framework cards, buttons on Adaptive cards support two ways of invoking task modules: deep link URLs with `Action.openUrl` buttons, and via `task/fetch` using `Action.Submit` buttons.</span></span> <br/><br/> <span data-ttu-id="85730-161">2. アダプティブカードを使用したタスクモジュールは、HTML/JavaScript のケースと同じように動作します (左を参照)。</span><span class="sxs-lookup"><span data-stu-id="85730-161">2. Task modules with Adaptive cards work very similarly to the HTML/JavaScript case (see left).</span></span> <span data-ttu-id="85730-162">主な違いは、アダプティブカードを使用しているときに JavaScript が存在しないため、を呼び`tasks.submitTask()`出すことができないということです。</span><span class="sxs-lookup"><span data-stu-id="85730-162">The major difference is that since there's no JavaScript when you're using Adaptive cards, there's no way to call `tasks.submitTask()`.</span></span> <span data-ttu-id="85730-163">代わりに、チームはから`data` `Action.Submit`オブジェクトを取得し、それを`task/submit`イベントのペイロードとして返します ([ここで](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)説明します)。</span><span class="sxs-lookup"><span data-stu-id="85730-163">Instead, Teams takes the `data` object from `Action.Submit` and returns it as the payload of in the `task/submit` event, as described [here](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> |
| <span data-ttu-id="85730-164">**ディープリンクの URL**</span><span class="sxs-lookup"><span data-stu-id="85730-164">**Deep link URL**</span></span> <br/>[<span data-ttu-id="85730-165">URL 構文</span><span class="sxs-lookup"><span data-stu-id="85730-165">URL syntax</span></span>](#task-module-deep-link-syntax) | <span data-ttu-id="85730-166">1. Teams がタスクモジュールを呼び出します。ディープリンクの`url`パラメーターで指定`<iframe>`されたの内部に表示される URL。</span><span class="sxs-lookup"><span data-stu-id="85730-166">1. Teams invokes the task module; the URL that appears inside the `<iframe>` specified in the `url` parameter of the deep link.</span></span> <span data-ttu-id="85730-167">コールバックは`submitHandler`ありません。</span><span class="sxs-lookup"><span data-stu-id="85730-167">There is no `submitHandler` callback.</span></span> <br/><br/> <span data-ttu-id="85730-168">2. タスクモジュールのページの JavaScript 内で、 `tasks.submitTask()` `result`オブジェクトをパラメーターとして閉じます。これは、タブまたはボットカードボタンから呼び出すときと同じです。</span><span class="sxs-lookup"><span data-stu-id="85730-168">2. Within the JavaScript of the page in the task module, call `tasks.submitTask()` to close it with a `result` object as a parameter, the same as when invoking it from a tab or a bot card button.</span></span> <span data-ttu-id="85730-169">ただし、完了ロジックは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="85730-169">Completion logic is slightly different, however.</span></span> <span data-ttu-id="85730-170">完了ロジックがクライアント上に存在する場合 (bot がない場合)、コールバックがない`submitHandler`ので、へ`tasks.submitTask()`の呼び出しの前のコードにすべての完了ロジックが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="85730-170">If your completion logic resides on the client (i.e. if there is no bot) there is no `submitHandler` callback, so any completion logic must be in the code preceding the call to `tasks.submitTask()`.</span></span> <span data-ttu-id="85730-171">呼び出しエラーはコンソールによってのみ報告されます。</span><span class="sxs-lookup"><span data-stu-id="85730-171">Invocation errors are only reported via the console.</span></span> <span data-ttu-id="85730-172">Bot がある場合は、deep link で`completionBotId`パラメーターを指定して、イベントを`result` `task/submit`使用してオブジェクトを送信できます。</span><span class="sxs-lookup"><span data-stu-id="85730-172">If you have a bot, then you can specify a `completionBotId` parameter in the deep link to send the `result` object via a `task/submit` event.</span></span> | <span data-ttu-id="85730-173">1. Teams がタスクモジュールを呼び出します。アダプティブカードの JSON カード本文は、ディープリンクの`card`パラメーターの URL エンコードされた値として指定されます。</span><span class="sxs-lookup"><span data-stu-id="85730-173">1. Teams invokes the task module; the JSON card body of the Adaptive card is specified as a URL-encoded value of the `card` parameter of the deep link.</span></span> <br/><br/> <span data-ttu-id="85730-174">2. ユーザーがタスクモジュールを閉じるには、タスクモジュールの右上にある [X `Action.Submit` ] をクリックするか、カードのボタンを押します。</span><span class="sxs-lookup"><span data-stu-id="85730-174">2. The user closes the task module by clicking on the X at the upper right of the task module or by pressing an `Action.Submit` button on the card.</span></span> <span data-ttu-id="85730-175">を呼び出すこと`submitHandler`はできないので、アダプティブカードフィールドの値をに送信する bot が必要です。</span><span class="sxs-lookup"><span data-stu-id="85730-175">Since there is no `submitHandler` to call, you must have a bot to send the value of the Adaptive card fields to.</span></span> <span data-ttu-id="85730-176">ディープリンクの`completionBotId`パラメーターを使用して、 `task/submit invoke`イベントを使用してデータを送信する bot を指定します。</span><span class="sxs-lookup"><span data-stu-id="85730-176">You use the `completionBotId` parameter in the deep link to specify the bot to send the data to via a `task/submit invoke` event.</span></span> |

> [!NOTE]
> <span data-ttu-id="85730-177">JavaScript からのタスクモジュールの呼び出しは、mobile ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="85730-177">Invoking a task module from JavaScript is not supported on mobile.</span></span>

## <a name="the-taskinfo-object"></a><span data-ttu-id="85730-178">TaskInfo オブジェクト</span><span class="sxs-lookup"><span data-stu-id="85730-178">The TaskInfo object</span></span>

<span data-ttu-id="85730-179">オブジェクト`TaskInfo`には、タスクモジュールのメタデータが含まれています。</span><span class="sxs-lookup"><span data-stu-id="85730-179">The `TaskInfo` object contains the metadata for a task module.</span></span> <span data-ttu-id="85730-180">オブジェクト定義は以下のとおりです。</span><span class="sxs-lookup"><span data-stu-id="85730-180">The object definition is below.</span></span> <span data-ttu-id="85730-181">(En 埋め込み`url` iFrame の場合) または`card` (アダプティブカードの場合) のいずれかを定義**する必要があり**ます。</span><span class="sxs-lookup"><span data-stu-id="85730-181">You **must** define either `url` (for en embedded iFrame) or `card` (for an Adaptive Card).</span></span>

| <span data-ttu-id="85730-182">属性</span><span class="sxs-lookup"><span data-stu-id="85730-182">Attribute</span></span> | <span data-ttu-id="85730-183">型</span><span class="sxs-lookup"><span data-stu-id="85730-183">Type</span></span> | <span data-ttu-id="85730-184">説明</span><span class="sxs-lookup"><span data-stu-id="85730-184">Description</span></span> |
| --- | --- | --- |
| `title` | <span data-ttu-id="85730-185">string</span><span class="sxs-lookup"><span data-stu-id="85730-185">string</span></span> | <span data-ttu-id="85730-186">アプリ名の下に表示され、アプリアイコンの右側に表示されます。</span><span class="sxs-lookup"><span data-stu-id="85730-186">Appears below the app name and to the right of the app icon</span></span> |
| `height` | <span data-ttu-id="85730-187">number または string</span><span class="sxs-lookup"><span data-stu-id="85730-187">number or string</span></span> | <span data-ttu-id="85730-188">タスクモジュールの高さを表す数値をピクセル、また`small` `medium`は、または`large`で指定できます。</span><span class="sxs-lookup"><span data-stu-id="85730-188">This can be a number representing the task module's height in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="85730-189">[高さと幅を処理する方法については、以下を参照して](#task-module-sizing)ください。</span><span class="sxs-lookup"><span data-stu-id="85730-189">[See below for how height and width are handled](#task-module-sizing).</span></span> |
| `width` | <span data-ttu-id="85730-190">number または string</span><span class="sxs-lookup"><span data-stu-id="85730-190">number or string</span></span> | <span data-ttu-id="85730-191">タスクモジュールの幅をピクセル、また`small` `medium`は、、または`large`の数値で指定できます。</span><span class="sxs-lookup"><span data-stu-id="85730-191">This can be a number representing the task module's width in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="85730-192">[高さと幅を処理する方法については、以下を参照して](#task-module-sizing)ください。</span><span class="sxs-lookup"><span data-stu-id="85730-192">[See below for how height and width are handled](#task-module-sizing).</span></span> |
| `url` | <span data-ttu-id="85730-193">string</span><span class="sxs-lookup"><span data-stu-id="85730-193">string</span></span> | <span data-ttu-id="85730-194">タスクモジュール内に`<iframe>`読み込まれたページの URL。</span><span class="sxs-lookup"><span data-stu-id="85730-194">The URL of the page loaded as an `<iframe>` inside the task module.</span></span> <span data-ttu-id="85730-195">URL のドメインは、アプリのマニフェストのアプリの[Validdomains 配列](~/resources/schema/manifest-schema.md#validdomains)内にある必要があります。</span><span class="sxs-lookup"><span data-stu-id="85730-195">The URL's domain must be in the app's [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in your app's manifest.</span></span> |
| `card` | <span data-ttu-id="85730-196">アダプティブカードまたはアダプティブカードのボットカード添付ファイル</span><span class="sxs-lookup"><span data-stu-id="85730-196">Adaptive card or an Adaptive card bot card attachment</span></span> | <span data-ttu-id="85730-197">タスクモジュールに表示されるアダプティブカードの JSON。</span><span class="sxs-lookup"><span data-stu-id="85730-197">The JSON for the Adaptive card to appear in the task module.</span></span> <span data-ttu-id="85730-198">Bot から呼び出している場合は、Bot フレームワーク`attachment`オブジェクトでアダプティブカード JSON を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85730-198">If you're invoking from a bot, you'll need to use the Adaptive card JSON in a Bot Framework `attachment` object.</span></span> <span data-ttu-id="85730-199">タブからは、アダプティブカードのみを使用します。</span><span class="sxs-lookup"><span data-stu-id="85730-199">From a tab you'll use just an Adaptive Card.</span></span> [<span data-ttu-id="85730-200">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="85730-200">Here's an example.</span></span>](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | <span data-ttu-id="85730-201">string</span><span class="sxs-lookup"><span data-stu-id="85730-201">string</span></span> | <span data-ttu-id="85730-202">クライアントがタスクモジュール機能をサポートしていない場合、この URL はブラウザタブで開かれます。</span><span class="sxs-lookup"><span data-stu-id="85730-202">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |
| `completionBotId` | <span data-ttu-id="85730-203">string</span><span class="sxs-lookup"><span data-stu-id="85730-203">string</span></span> | <span data-ttu-id="85730-204">ユーザーのタスクモジュールとの対話結果をに送信する bot アプリ ID を指定します。</span><span class="sxs-lookup"><span data-stu-id="85730-204">Specifies a bot App ID to send the result of the user's interaction with the task module to.</span></span> <span data-ttu-id="85730-205">指定した場合、bot は、 `task/submit invoke`イベントペイロードで JSON オブジェクトを含むイベントを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="85730-205">If specified, the bot will receive a `task/submit invoke` event with a JSON object in the event payload.</span></span> |

> [!NOTE]
> <span data-ttu-id="85730-206">タスクモジュール機能を使用するには、読み込む Url のドメインがアプリのマニフェストの`validDomains`配列に含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="85730-206">The task module feature requires that the domains of any URLs you want to load are included in the `validDomains` array in your app's manifest.</span></span>

## <a name="task-module-sizing"></a><span data-ttu-id="85730-207">タスクモジュールのサイズ変更</span><span class="sxs-lookup"><span data-stu-id="85730-207">Task module sizing</span></span>

<span data-ttu-id="85730-208">および`TaskInfo.width` `TaskInfo.height`の整数を使用して、高さと幅をピクセル単位で設定します。</span><span class="sxs-lookup"><span data-stu-id="85730-208">Using integers for `TaskInfo.width` and `TaskInfo.height` will set the height and width in pixels.</span></span> <span data-ttu-id="85730-209">ただし、チームのウィンドウと画面の解像度のサイズによっては、縦横比 (幅/高さ) を維持している場合に、比率が低くなります。</span><span class="sxs-lookup"><span data-stu-id="85730-209">However, depending on the size of the Team's window and screen resolution they will be reduced proportionally while maintaining the aspect ratio (width/height).</span></span>

<span data-ttu-id="85730-210">と`TaskInfo.width`の`TaskInfo.height`場合`"small"`、 `"medium"` `"large"`およびの場合、上の図の赤の四角形のサイズは、使用可能な領域の比率 (20%、50%、 `width` 60%、50%、66%(for `height`) です。</span><span class="sxs-lookup"><span data-stu-id="85730-210">If `TaskInfo.width` and `TaskInfo.height` are `"small"`, `"medium"` or `"large"` the size of the red rectangle in the picture above is a proportion of the available space: 20%, 50%, 60% for `width` and 20%, 50%, 66% for `height`.</span></span>

<span data-ttu-id="85730-211">タブから起動されたタスクモジュールは、動的にサイズ変更できます。</span><span class="sxs-lookup"><span data-stu-id="85730-211">Task modules invoked from a tab can be dynamically resized.</span></span> <span data-ttu-id="85730-212">呼び出し`tasks.startTask()`後に、newSize `tasks.updateTask(newSize)`オブジェクトの height プロパティと width プロパティの両方が taskinfo 仕様に準拠していることを呼び出します (例、</span><span class="sxs-lookup"><span data-stu-id="85730-212">After calling `tasks.startTask()` you can call `tasks.updateTask(newSize)` where height and width properties on the newSize object conform to the TaskInfo spec (ex.</span></span> <span data-ttu-id="85730-213">`{ height: 'medium', width: 'medium' }`).</span><span class="sxs-lookup"><span data-stu-id="85730-213">`{ height: 'medium', width: 'medium' }`).</span></span>

## <a name="task-module-css-for-htmljavascript-task-modules"></a><span data-ttu-id="85730-214">HTML/JavaScript タスクモジュール用のタスクモジュール CSS</span><span class="sxs-lookup"><span data-stu-id="85730-214">Task module CSS for HTML/JavaScript task modules</span></span>

<span data-ttu-id="85730-215">HTML/JavaScript ベースのタスクモジュールは、ヘッダーの下にあるタスクモジュールの領域全体にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="85730-215">HTML/JavaScript-based task modules have access to the entire area of the task module below the header.</span></span> <span data-ttu-id="85730-216">非常に高い柔軟性が提供されますが、ヘッダー要素に合わせてエッジの周囲にパディングを行い、不要なスクロールバーを使用しないようにするには、適切な CSS を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85730-216">While that offers a great deal of flexibility, if you want padding around the edges to align with the header elements and avoid unnecessary scrollbars you'll need to provide the right CSS.</span></span> <span data-ttu-id="85730-217">いくつかのユースケースの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="85730-217">Here are some examples for a few use cases.</span></span>

### <a name="example-1---youtube-video"></a><span data-ttu-id="85730-218">例 1-YouTube ビデオ</span><span class="sxs-lookup"><span data-stu-id="85730-218">Example 1 - YouTube video</span></span>

<span data-ttu-id="85730-219">YouTube は、web ページにビデオを埋め込む機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="85730-219">YouTube offers the ability to embed videos on web pages.</span></span> <span data-ttu-id="85730-220">簡単なスタブ web ページを使用すると、これをタスクモジュールに簡単に表示できます。</span><span class="sxs-lookup"><span data-stu-id="85730-220">Using a simple stub web page it's easy to show this in a task module:</span></span>

![YouTube ビデオ](~/assets/images/task-module/youtube-example.png)

<span data-ttu-id="85730-222">CSS を使用しないこのページの HTML を次に示します。</span><span class="sxs-lookup"><span data-stu-id="85730-222">Here's the HTML for this page, without the CSS:</span></span>

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

<span data-ttu-id="85730-223">CSS は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="85730-223">The CSS looks like this:</span></span>

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

### <a name="example-2---powerapp"></a><span data-ttu-id="85730-224">例 2-PowerApp</span><span class="sxs-lookup"><span data-stu-id="85730-224">Example 2 - PowerApp</span></span>

<span data-ttu-id="85730-225">同じ方法を使用して、PowerApp も埋め込むことができます。</span><span class="sxs-lookup"><span data-stu-id="85730-225">You can use the same approach to embed a PowerApp as well.</span></span> <span data-ttu-id="85730-226">個々の PowerApp の高さと幅はカスタマイズ可能なので、目的のプレゼンテーションを実現するには、高さと幅を調整しなければならない場合があります。</span><span class="sxs-lookup"><span data-stu-id="85730-226">As the height/width of any individual PowerApp is customizable, you may need to adjust the height and width to achieve your desired presentation.</span></span>

![Asset Management PowerApp](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

<span data-ttu-id="85730-228">そして、CSS は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="85730-228">And the CSS is:</span></span>

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a><span data-ttu-id="85730-229">アダプティブカードまたはアダプティブカードのボットカード添付ファイル</span><span class="sxs-lookup"><span data-stu-id="85730-229">Adaptive card or Adaptive card bot card attachment</span></span>

<span data-ttu-id="85730-230">前述したように、を呼び出す`card`方法によっては、アダプティブカードを使用するか、またはアダプティブカードのボットカードの添付ファイル (添付ファイルオブジェクトにラップされたアダプティブカードのみ) を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85730-230">As we noted above, depending on how you're invoking your `card` you'll need to use either an Adaptive card, or an Adaptive card bot card attachment (which is just an Adaptive card wrapped in an attachment object).</span></span>

<span data-ttu-id="85730-231">タブから呼び出している場合は、アダプティブカードを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85730-231">When you're invoking from a tab, you'll need to use an adaptive card.</span></span> <span data-ttu-id="85730-232">非常に簡単な例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="85730-232">Here's a very simple example:</span></span>

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

<span data-ttu-id="85730-233">Bot から呼び出している場合は、次の例に示すように、アダプティブカードのボットカード添付ファイルを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85730-233">When you're invoking from a bot you'll need to use an Adaptive card bot card attachment as in the example below:</span></span>

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

<span data-ttu-id="85730-234">Bot またはタブから、アダプティブカードを含むタスクモジュールを呼び出しているかどうかを覚えておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="85730-234">You'll need to remember whether you are invoking a task module containing an Adaptive card from a bot or a tab.</span></span>

## <a name="task-module-deep-link-syntax"></a><span data-ttu-id="85730-235">タスクモジュールの詳細なリンク構文</span><span class="sxs-lookup"><span data-stu-id="85730-235">Task module deep link syntax</span></span>

<span data-ttu-id="85730-236">タスクモジュールの深さのリンクは、他の2つの情報`APP_ID`を含む[taskinfo オブジェクト](#the-taskinfo-object)のシリアル化だけで`BOT_APP_ID`あり、必要に応じて次のようにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="85730-236">A task module deep link is just a serialization of the [TaskInfo object](#the-taskinfo-object) with two other pieces of information, `APP_ID` and optionally the `BOT_APP_ID`:</span></span>

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

<span data-ttu-id="85730-237">データ型については、「」、「」 `<TaskInfo.url>` `<TaskInfo.width>`、 `<TaskInfo.card>`および`<TaskInfo.height>` `<TaskInfo.title>`「」の値については、「 [taskinfo オブジェクト](#the-taskinfo-object)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="85730-237">See [TaskInfo object](#the-taskinfo-object) for the data types and allowable values for `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`, and `<TaskInfo.title>`.</span></span>

> [!TIP]
> <span data-ttu-id="85730-238">特に、 `card`パラメーター (JavaScript の[ `encodeURI()`関数](https://www.w3schools.com/jsref/jsref_encodeURI.asp)など) を使用する場合は、URL が深いリンクをエンコードしていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="85730-238">Be sure to URL encode the deep link, especially when using the `card` parameter (for example, JavaScript's [`encodeURI()` function](https://www.w3schools.com/jsref/jsref_encodeURI.asp)).</span></span>

<span data-ttu-id="85730-239">と`BOT_APP_ID`の情報を以下`APP_ID`に示します。</span><span class="sxs-lookup"><span data-stu-id="85730-239">Here's the information on `APP_ID` and `BOT_APP_ID`:</span></span>

| <span data-ttu-id="85730-240">値</span><span class="sxs-lookup"><span data-stu-id="85730-240">Value</span></span> | <span data-ttu-id="85730-241">型</span><span class="sxs-lookup"><span data-stu-id="85730-241">Type</span></span> | <span data-ttu-id="85730-242">必須</span><span class="sxs-lookup"><span data-stu-id="85730-242">Required?</span></span> | <span data-ttu-id="85730-243">説明</span><span class="sxs-lookup"><span data-stu-id="85730-243">Description</span></span> |
| --- | --- | --- | --- |
| `APP_ID` | <span data-ttu-id="85730-244">string</span><span class="sxs-lookup"><span data-stu-id="85730-244">string</span></span> | <span data-ttu-id="85730-245">はい</span><span class="sxs-lookup"><span data-stu-id="85730-245">Yes</span></span> | <span data-ttu-id="85730-246">タスクモジュールを呼び出すアプリの[id](~/resources/schema/manifest-schema.md#id) 。</span><span class="sxs-lookup"><span data-stu-id="85730-246">The [id](~/resources/schema/manifest-schema.md#id) of the app invoking the task module.</span></span> <span data-ttu-id="85730-247">マニフェスト内の[Validdomains 配列](~/resources/schema/manifest-schema.md#validdomains)には`APP_ID` 、が URL にある`url`場合`url`のドメインが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="85730-247">The [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in the manifest for `APP_ID` must contain the domain for `url` if `url` is in the URL.</span></span> <span data-ttu-id="85730-248">(アプリ ID は、タスクモジュールがタブまたは bot から呼び出されたときに既に知られています。これは`TaskInfo`、に含まれていないためです)。</span><span class="sxs-lookup"><span data-stu-id="85730-248">(The app ID is already known when a task module is invoked from a tab or a bot, which is why it's not included in `TaskInfo`.)</span></span> |
| `BOT_APP_ID` | <span data-ttu-id="85730-249">文字列</span><span class="sxs-lookup"><span data-stu-id="85730-249">string</span></span> | <span data-ttu-id="85730-250">いいえ</span><span class="sxs-lookup"><span data-stu-id="85730-250">No</span></span> | <span data-ttu-id="85730-251">の`completionBotId`値が指定されている`result`場合、オブジェクトは、指定`task/submit invoke`された bot へのメッセージによって送信されます。</span><span class="sxs-lookup"><span data-stu-id="85730-251">If a value for `completionBotId` is specified, the `result` object is sent via a a `task/submit invoke` message to the specified bot.</span></span> <span data-ttu-id="85730-252">`BOT_APP_ID`アプリのマニフェストでボットとして指定する必要があります。つまり、任意の bot に送信するだけではできません。</span><span class="sxs-lookup"><span data-stu-id="85730-252">`BOT_APP_ID` must be specified as a bot in the app's manifest, i.e. you can't just send it to any bot.</span></span> |

<span data-ttu-id="85730-253">これ`APP_ID`は同じであること`BOT_APP_ID`に注意してください。多くの場合、アプリの ID として使用することをお勧めするので、アプリに bot がある場合は、それを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="85730-253">Note that it's valid for `APP_ID` and `BOT_APP_ID` to be the same, and in many cases will be if an app has a bot since it's recommended to use that as an app's ID if there is one.</span></span>

## <a name="keyboard-and-accessibility-guidelines"></a><span data-ttu-id="85730-254">キーボードとユーザー補助ガイドライン</span><span class="sxs-lookup"><span data-stu-id="85730-254">Keyboard and accessibility guidelines</span></span>

<span data-ttu-id="85730-255">HTML/JavaScript ベースのタスクモジュールを使用すると、アプリのタスクモジュールをキーボードで使用できることを確認する責任があります。</span><span class="sxs-lookup"><span data-stu-id="85730-255">With HTML/JavaScript-based task modules it is your responsibility to ensure your app's task module can be used with a keyboard.</span></span> <span data-ttu-id="85730-256">スクリーンリーダープログラムは、キーボードを使用して移動する機能にも依存します。</span><span class="sxs-lookup"><span data-stu-id="85730-256">Screen reader programs also depend on the ability to navigate using the keyboard.</span></span> <span data-ttu-id="85730-257">実用上の問題として、次の2つのことがあります。</span><span class="sxs-lookup"><span data-stu-id="85730-257">As a practical matter this means two things:</span></span>

1. <span data-ttu-id="85730-258">HTML タグの[tabindex 属性](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex)を使用して、どの要素がフォーカスされているか、または (通常は<kbd>Tab</kbd>キーと Shift キーを<kbd>押しながら</kbd>tab キーを使用して) 連続したキーボードナビゲーションに参加するかどうかを制御します。</span><span class="sxs-lookup"><span data-stu-id="85730-258">Using the [tabindex attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) in your HTML tags to control which elements can be focused and if/where it participates in sequential keyboard navigation (usually with the <kbd>Tab</kbd> and <kbd>Shift-Tab</kbd> keys).</span></span>
2. <span data-ttu-id="85730-259">タスクモジュールの JavaScript で<kbd>Esc</kbd>キーを処理します。</span><span class="sxs-lookup"><span data-stu-id="85730-259">Handling the <kbd>Esc</kbd> key in the JavaScript for your task module.</span></span> <span data-ttu-id="85730-260">これを行う方法を示すコードサンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="85730-260">Here's a code sample showing how to do this:</span></span>

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

<span data-ttu-id="85730-261">Microsoft Teams では、キーボードナビゲーションがタスクモジュールヘッダーから HTML およびその逆に適切に動作することが保証されます。</span><span class="sxs-lookup"><span data-stu-id="85730-261">Microsoft Teams will ensure that keyboard navigation works properly from the task module header into your HTML and vice-versa.</span></span>

## <a name="task-module-samples"></a><span data-ttu-id="85730-262">タスクモジュールのサンプル</span><span class="sxs-lookup"><span data-stu-id="85730-262">Task module samples</span></span>

* [<span data-ttu-id="85730-263">Node.js/TypeScript サンプル</span><span class="sxs-lookup"><span data-stu-id="85730-263">Node.js/TypeScript sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs)
* [<span data-ttu-id="85730-264">C#/.NET サンプル</span><span class="sxs-lookup"><span data-stu-id="85730-264">C#/.NET sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp)
