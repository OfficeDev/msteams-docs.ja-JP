---
title: タスク モジュールとは
author: clearab
description: Microsoft Teamsアプリからユーザーに情報を収集または表示するためのモーダル ポップアップ エクスペリエンスを追加する
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 23157e30ce25c2dfa1c21e7f5c4ddd4f735b660f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566843"
---
# <a name="task-modules"></a><span data-ttu-id="3e29a-103">タスク モジュール</span><span class="sxs-lookup"><span data-stu-id="3e29a-103">Task modules</span></span>

<span data-ttu-id="3e29a-104">タスク モジュールを使用すると、Teams アプリケーションでモーダル ポップアップ エクスペリエンスを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-104">Task modules allow you to create modal popup experiences in your Teams application.</span></span> <span data-ttu-id="3e29a-105">ポップアップの内部では、独自のカスタム HTML/JavaScript コードを実行 `<iframe>` したり、YouTube や Microsoft Stream のビデオなどのベースのウィジェットを表示したり、 [アダプティブ カード](/adaptive-cards/)を表示したりできます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-105">Inside the popup you can run your own custom HTML/JavaScript code, show an `<iframe>`-based widget such as a YouTube or Microsoft Stream video or display an [Adaptive card](/adaptive-cards/).</span></span> <span data-ttu-id="3e29a-106">これらは特に、タスクの開始や完了、ビデオや Power BI ダッシュボードなどのリッチな情報の表示に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-106">They are especially useful for initiating and completing tasks or displaying rich information like videos or Power BI dashboards.</span></span> <span data-ttu-id="3e29a-107">一般的にポップアップ エクスペリエンスは、タブや会話ベースのボット エクスペリエンスに比べて、より自然にユーザーがタスクを開始したり完了したりすることができるようになっています。</span><span class="sxs-lookup"><span data-stu-id="3e29a-107">A popup experience is often more natural for users initiating and completing tasks compared to a tab or a conversation-based bot experience.</span></span>

<span data-ttu-id="3e29a-108">タスクモジュールは、Microsoft Teamsタブの基礎に基づいて構築されます。これらは、基本的にポップアップウィンドウ内のタブです。</span><span class="sxs-lookup"><span data-stu-id="3e29a-108">Task modules build on the foundation of Microsoft Teams tabs; they are essentially a tab inside a popup window.</span></span> <span data-ttu-id="3e29a-109">これらは同じ SDK を使用するため、タブを作成した場合は、タスク モジュールを作成する方法の 90% が既に存在します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-109">They use the same SDK, so if you've built a tab you are already 90% of the way to being able to create a task module.</span></span>

<span data-ttu-id="3e29a-110">タスク モジュールは次の 3 つの方法で呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-110">Task modules can be invoked in three ways:</span></span>

* <span data-ttu-id="3e29a-111">**チャンネルタブまたは個人用タブ**: Microsoft TeamsタブSDKを使用すると、タブ上のボタン、リンク、メニューからタスクモジュールを呼び出すことができます [。](~/task-modules-and-cards/task-modules/task-modules-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="3e29a-111">**Channel or personal tabs**: Using the Microsoft Teams Tabs SDK you can invoke task modules from buttons, links or menus on your tab. [This is covered in detail here.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)</span></span>
* <span data-ttu-id="3e29a-112">**ボット**: ボットから送信された [カード](~/task-modules-and-cards/cards/cards-reference.md) のボタン。</span><span class="sxs-lookup"><span data-stu-id="3e29a-112">**Bots**: Buttons on [cards](~/task-modules-and-cards/cards/cards-reference.md) sent from your bot.</span></span> <span data-ttu-id="3e29a-113">これは、ボットで何をしているかを確認するためにチャネル内のすべてのユーザーが必要ない場合に特に便利です。</span><span class="sxs-lookup"><span data-stu-id="3e29a-113">This is particularly useful when you don't need everyone in a channel to see what you are doing with a bot.</span></span> <span data-ttu-id="3e29a-114">たとえば、チャネル内のユーザーに投票してもらう場合、投票中の記録が見えるのは好ましくありません。</span><span class="sxs-lookup"><span data-stu-id="3e29a-114">For example, when having users respond to a poll in a channel it's not terribly useful to see a record of that poll being created.</span></span> [<span data-ttu-id="3e29a-115">これについては、ここで詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-115">This is covered in detail here.</span></span>](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* <span data-ttu-id="3e29a-116">**ディープリンクからTeamsの外**: どこからでもタスクモジュールを呼び出す URL を作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-116">**Outside of Teams from a deep link**: You can also create URLs to invoke a task module from anywhere.</span></span> [<span data-ttu-id="3e29a-117">これについては、ここで詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-117">This is covered in detail here.</span></span>](#task-module-deep-link-syntax)

## <a name="task-module-looks-like"></a><span data-ttu-id="3e29a-118">タスクモジュールは次のようになります</span><span class="sxs-lookup"><span data-stu-id="3e29a-118">Task module looks like</span></span>

<span data-ttu-id="3e29a-119">ボットから呼び出されたときのタスク モジュールは次のようになります (色付きの四角形と番号付きの円は除く)。</span><span class="sxs-lookup"><span data-stu-id="3e29a-119">Here's what a task module looks like when invoked from a bot (without the colored rectangles and numbered circles, of course):</span></span>

![タスク モジュールの例](~/assets/images/task-module/task-module-example.png)

<span data-ttu-id="3e29a-121">それを見てみましょう:</span><span class="sxs-lookup"><span data-stu-id="3e29a-121">Let's walk through it:</span></span>

1. <span data-ttu-id="3e29a-122">アプリの[ `color` アイコン](~/resources/schema/manifest-schema.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="3e29a-122">Your app's [`color` icon](~/resources/schema/manifest-schema.md#icons).</span></span>
1. <span data-ttu-id="3e29a-123">アプリの[ `short` 名前](~/resources/schema/manifest-schema.md#name)。</span><span class="sxs-lookup"><span data-stu-id="3e29a-123">Your app's [`short` name](~/resources/schema/manifest-schema.md#name).</span></span>
1. <span data-ttu-id="3e29a-124">TaskInfo オブジェクトのプロパティで指定された `title` [タスク](#the-taskinfo-object)モジュールのタイトル。</span><span class="sxs-lookup"><span data-stu-id="3e29a-124">The task module's title specified in the `title` property of the [TaskInfo object](#the-taskinfo-object).</span></span>
1. <span data-ttu-id="3e29a-125">タスク モジュールの閉じる/キャンセル ボタン。</span><span class="sxs-lookup"><span data-stu-id="3e29a-125">The task module's close/cancel button.</span></span> <span data-ttu-id="3e29a-126">ユーザーがこれを押すと、ここで説明するイベントがアプリに表示されます `err` 。 [](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)</span><span class="sxs-lookup"><span data-stu-id="3e29a-126">If the user presses this, your app will receive an `err` event as described [here](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module).</span></span>
    > [!Note]
    > <span data-ttu-id="3e29a-127">現在、タスク モジュールがボットから呼び出されたときに、このイベントを検出することはできません。</span><span class="sxs-lookup"><span data-stu-id="3e29a-127">It is currently not possible to detect this event when a task module is invoked from a bot.</span></span>
1. <span data-ttu-id="3e29a-128">青い四角形は、 TaskInfo オブジェクトのプロパティを使用して独自の Web ページを読み込む場合に Web ページが表示される場所 `url` です。 [](#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="3e29a-128">The blue rectangle is the where your web page appears if you are loading your own web page using the `url` property of the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="3e29a-129">詳細については、以下の [タスク モジュールのサイズ設定](#task-module-sizing) に関するセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="3e29a-129">More detail is in the [task module sizing](#task-module-sizing) section below.</span></span>
1. <span data-ttu-id="3e29a-130">TaskInfo オブジェクトのプロパティを使用して Adaptive カードを表示する場合 `card` は、埋め込みが追加されます。 [](#the-taskinfo-object) [](#task-module-css-for-htmljavascript-task-modules)</span><span class="sxs-lookup"><span data-stu-id="3e29a-130">If you are displaying an Adaptive card via the `card` property of the [TaskInfo object](#the-taskinfo-object) the padding is added for you, otherwise you'll need to [handle this yourself](#task-module-css-for-htmljavascript-task-modules).</span></span>
1. <span data-ttu-id="3e29a-131">アダプティブ カード ボタンは、ここに表示されます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-131">Adaptive card buttons will render here.</span></span> <span data-ttu-id="3e29a-132">独自のページを使用している場合は、独自のボタンを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-132">If you're using your own page you must create your own buttons.</span></span>

## <a name="overview-of-invoking-and-dismissing-task-modules"></a><span data-ttu-id="3e29a-133">タスク モジュールの呼び出しと消去の概要</span><span class="sxs-lookup"><span data-stu-id="3e29a-133">Overview of invoking and dismissing task modules</span></span>

<span data-ttu-id="3e29a-134">タスクモジュールはタブ、ボット、ディープリンクから呼び出し、HTMLまたはアダプティブカードのいずれかで表示されるため、どのように呼び出されるか、そしてユーザーの操作の結果にどのように対処するかという点で多くの柔軟性があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-134">Task modules can be invoked from tabs, bots or deep links and what appears in one can be either HTML or an Adaptive card, so there's a lot of flexibility in terms of how they are invoked and how to deal with the result of a user's interaction.</span></span> <span data-ttu-id="3e29a-135">次の表は、このしくみを要約したものです。</span><span class="sxs-lookup"><span data-stu-id="3e29a-135">The table below summarizes how this works:</span></span>

| <span data-ttu-id="3e29a-136">**を介して呼び出されます。**</span><span class="sxs-lookup"><span data-stu-id="3e29a-136">**Invoked via...**</span></span> | <span data-ttu-id="3e29a-137">**タスクモジュールはHTML/Javaスクリプトです**</span><span class="sxs-lookup"><span data-stu-id="3e29a-137">**Task module is HTML/JavaScript**</span></span> | <span data-ttu-id="3e29a-138">**タスクモジュールはアダプティブカードです**</span><span class="sxs-lookup"><span data-stu-id="3e29a-138">**Task module is Adaptive card**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e29a-139">**タブ内の JavaScript**</span><span class="sxs-lookup"><span data-stu-id="3e29a-139">**JavaScript in a tab**</span></span> | <span data-ttu-id="3e29a-140">1. オプションのコールバック関数でTeamsクライアント SDK `tasks.startTask()` 関数を使用 `submitHandler(err, result)` します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-140">1. Use the Teams client SDK function `tasks.startTask()` with an optional `submitHandler(err, result)` callback function.</span></span> <br/><br/> <span data-ttu-id="3e29a-141">2. タスク モジュール コードで、ユーザーが終了したら、 `tasks.submitTask()` パラメーターとしてオブジェクトを使用して Teams SDK 関数を呼び出 `result` します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-141">2. In the task module code, when the user is finished, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="3e29a-142">`submitHandler`コールバックが で指定されている場合 `tasks.startTask()` 、Teamsはパラメーターとして呼び出 `result` します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-142">If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with `result` as a parameter.</span></span><br/><br/> <span data-ttu-id="3e29a-143">3. 呼び出し時にエラーが発生した場合 `tasks.startTask()` `submitHandler` 、関数は `err` 代わりに文字列で呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-143">3. If there was an error when invoking `tasks.startTask()`, the `submitHandler` function is called with an `err` string instead.</span></span> <br/><br/> <span data-ttu-id="3e29a-144">4. `completionBotId` 呼び出し時にを指定することもできます `teams.startTask()` 。 `result`</span><span class="sxs-lookup"><span data-stu-id="3e29a-144">4. You can also specify a `completionBotId` when calling `teams.startTask()` - in that case `result` is sent to the bot instead.</span></span> | <span data-ttu-id="3e29a-145">1. TaskInfo オブジェクトを使用してTeamsクライアント SDK 関数を呼び出 `tasks.startTask()` し、タスク[](#the-taskinfo-object) `TaskInfo.card` モジュールポップアップに表示する Adaptive カードの JSON を含めます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-145">1. Call the Teams client SDK function `tasks.startTask()` with a [TaskInfo object](#the-taskinfo-object) and `TaskInfo.card` containing the JSON for the Adaptive card to show in the task module popup.</span></span> <br/><br/> <span data-ttu-id="3e29a-146">2. `submitHandler` コールバックが で指定されている場合 `tasks.startTask()` 、Teams呼 `err` び出し時にエラーがあった `tasks.startTask()` 場合、またはユーザーが右上の X を使用してタスク モジュール ポップアップを閉じた場合に、文字列を使用してコールバックを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-146">2. If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with an `err` string if there was an error when invoking `tasks.startTask()` or if the user closes the task module popup using the X at the upper right.</span></span> <br/><br/> <span data-ttu-id="3e29a-147">3. ユーザーが Action.Submit ボタンを押すと、その `data` オブジェクトがの値として返されます `result` 。</span><span class="sxs-lookup"><span data-stu-id="3e29a-147">3. If the user presses an Action.Submit button then its `data` object is returned as the value of `result`.</span></span> |
| <span data-ttu-id="3e29a-148">**ボット カード ボタン**</span><span class="sxs-lookup"><span data-stu-id="3e29a-148">**Bot card button**</span></span> | <span data-ttu-id="3e29a-149">1. ボットカードボタンは、ボタンの種類に応じて、ディープリンクURLまたはメッセージ送信の2つの方法でタスクモジュールを呼び出すことができます `task/fetch` 。</span><span class="sxs-lookup"><span data-stu-id="3e29a-149">1. Bot card buttons, depending on the type of button, can invoke task modules in two ways: a deep link URL or by sending a `task/fetch` message.</span></span> <span data-ttu-id="3e29a-150">リンク URL の動作の詳細については、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3e29a-150">See below for how deep link URLs work.</span></span> <br/><br/> <span data-ttu-id="3e29a-151">2. ボタンのアクションが `type` `task/fetch` ( `Action.Submit` アダプティブ カードのボタンの種類) の場合 `task/fetch invoke` 、イベント (カバーの下の HTTP POST) がボットに送信され、ボットは HTTP 200 で POST に応答し、応答本文に [TaskInfo オブジェクト](#the-taskinfo-object)のラッパーを含む。</span><span class="sxs-lookup"><span data-stu-id="3e29a-151">2. If the button's action `type` is `task/fetch` (`Action.Submit` button type for Adaptive cards), a `task/fetch invoke` event (an HTTP POST under the covers) is sent to the bot, and the bot responds to the POST with HTTP 200 and the response body containing a wrapper around the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="3e29a-152">これは、 [タスク/フェッチを介してタスクモジュールを呼び出す方法](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-through-taskfetch)で詳しく説明されています。</span><span class="sxs-lookup"><span data-stu-id="3e29a-152">This is explained in detail in [invoking a task module via task/fetch](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-through-taskfetch).</span></span><br/><br/> <span data-ttu-id="3e29a-153">3. Teamsタスクモジュールを表示します。ユーザーが終了したら、Teams SDK 関数を `tasks.submitTask()` パラメーターとしてオブジェクトを使用して呼び出 `result` します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-153">3. Teams displays the task module; when the user is finished, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <br/><br/> <span data-ttu-id="3e29a-154">4. ボットは `task/submit invoke` 、オブジェクトを含むメッセージを受信 `result` します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-154">4. The bot receives a `task/submit invoke` message that contains the `result` object.</span></span> <span data-ttu-id="3e29a-155">メッセージに応答するには、 `task/submit` 何もしない (タスクが正常に完了した) 、ポップアップ ウィンドウでユーザーにメッセージを表示する方法、または別のタスク モジュール ウィンドウを呼び出す (つまり、ウィザードのようなエクスペリエンスを作成する) という 3 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-155">You have three different ways to respond to the `task/submit` message: by doing nothing (the task completed successfully), by displaying a message to the user in a popup window, or by invoking another task module window (i.e. creating a wizard-like experience).</span></span> <span data-ttu-id="3e29a-156">これら 3 つのオプションについては、 [タスク/送信に関する詳細な説明](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)で詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-156">These three options are discussed more [in the detailed discussion on task/submit](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> | <span data-ttu-id="3e29a-157">1. Bot Framework カードのボタンと同様に、Adaptive カードのボタンはタスク モジュールを呼び出す 2 つの方法をサポートします: ボタン付きディープ リンク URL `Action.openUrl` と `task/fetch` ボタンを使用して `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="3e29a-157">1. Like buttons on Bot Framework cards, buttons on Adaptive cards support two ways of invoking task modules: deep link URLs with `Action.openUrl` buttons, and via `task/fetch` using `Action.Submit` buttons.</span></span> <br/><br/> <span data-ttu-id="3e29a-158">2. アダプティブカードを使用したタスクモジュールは、HTML/JavaScriptの場合と非常に似ています(左を参照)。</span><span class="sxs-lookup"><span data-stu-id="3e29a-158">2. Task modules with Adaptive cards work very similarly to the HTML/JavaScript case (see left).</span></span> <span data-ttu-id="3e29a-159">主な違いは、アダプティブカードを使用しているときにJavaScriptが存在しないため、呼び出す方法がなさ `tasks.submitTask()`</span><span class="sxs-lookup"><span data-stu-id="3e29a-159">The major difference is that since there's no JavaScript when you're using Adaptive cards, there's no way to call `tasks.submitTask()`.</span></span> <span data-ttu-id="3e29a-160">代わりに、Teamsは `data` 、ここで説明しているように、オブジェクトをから取得 `Action.Submit` し、イベントのペイロードとして返 `task/submit` [します](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。</span><span class="sxs-lookup"><span data-stu-id="3e29a-160">Instead, Teams takes the `data` object from `Action.Submit` and returns it as the payload of in the `task/submit` event, as described [here](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> |
| <span data-ttu-id="3e29a-161">**ディープリンクURL**</span><span class="sxs-lookup"><span data-stu-id="3e29a-161">**Deep link URL**</span></span> <br/>[<span data-ttu-id="3e29a-162">URL 構文</span><span class="sxs-lookup"><span data-stu-id="3e29a-162">URL syntax</span></span>](#task-module-deep-link-syntax) | <span data-ttu-id="3e29a-163">1. Teamsタスクモジュールを呼び出します。`<iframe>`ディープリンクのパラメータで指定された内部 `url` に表示されるURL。</span><span class="sxs-lookup"><span data-stu-id="3e29a-163">1. Teams invokes the task module; the URL that appears inside the `<iframe>` specified in the `url` parameter of the deep link.</span></span> <span data-ttu-id="3e29a-164">`submitHandler`コールバックはありません。</span><span class="sxs-lookup"><span data-stu-id="3e29a-164">There is no `submitHandler` callback.</span></span> <br/><br/> <span data-ttu-id="3e29a-165">2. タスクモジュールのページの JavaScript 内で、 `tasks.submitTask()` `result` タブやボットカードボタンから呼び出す場合と同じように、オブジェクトをパラメータとして閉じるように呼び出します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-165">2. Within the JavaScript of the page in the task module, call `tasks.submitTask()` to close it with a `result` object as a parameter, the same as when invoking it from a tab or a bot card button.</span></span> <span data-ttu-id="3e29a-166">ただし、完了ロジックは若干異なります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-166">Completion logic is slightly different, however.</span></span> <span data-ttu-id="3e29a-167">完了ロジックがクライアント上にある場合 (つまり、ボットがない場合)、コールバックは存在 `submitHandler` しません `tasks.submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="3e29a-167">If your completion logic resides on the client (i.e. if there is no bot) there is no `submitHandler` callback, so any completion logic must be in the code preceding the call to `tasks.submitTask()`.</span></span> <span data-ttu-id="3e29a-168">呼び出しエラーはコンソールを介してのみ報告されます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-168">Invocation errors are only reported via the console.</span></span> <span data-ttu-id="3e29a-169">ボットがある場合は、 `completionBotId` ディープリンクでパラメータを指定して `result` 、イベントを介してオブジェクトを送信できます `task/submit` 。</span><span class="sxs-lookup"><span data-stu-id="3e29a-169">If you have a bot, then you can specify a `completionBotId` parameter in the deep link to send the `result` object via a `task/submit` event.</span></span> | <span data-ttu-id="3e29a-170">1. Teamsタスクモジュールを呼び出します。アダプティブ カードの JSON カード本体は、ディープ リンクのパラメーターの URL エンコード値として指定 `card` されます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-170">1. Teams invokes the task module; the JSON card body of the Adaptive card is specified as a URL-encoded value of the `card` parameter of the deep link.</span></span> <br/><br/> <span data-ttu-id="3e29a-171">2. タスクモジュールの右上にあるXをクリックするか、カードのボタンを押して、タスクモジュールを閉じます `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="3e29a-171">2. The user closes the task module by clicking on the X at the upper right of the task module or by pressing an `Action.Submit` button on the card.</span></span> <span data-ttu-id="3e29a-172">`submitHandler`呼び出しが行ないため、Adaptive カード フィールドの値を送信するボットが必要です。</span><span class="sxs-lookup"><span data-stu-id="3e29a-172">Since there is no `submitHandler` to call, you must have a bot to send the value of the Adaptive card fields to.</span></span> <span data-ttu-id="3e29a-173">`completionBotId`ディープリンクのパラメータを使用して、イベントを介してデータを送信するボットを指定 `task/submit invoke` します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-173">You use the `completionBotId` parameter in the deep link to specify the bot to send the data to via a `task/submit invoke` event.</span></span> |

## <a name="the-taskinfo-object"></a><span data-ttu-id="3e29a-174">オブジェクト</span><span class="sxs-lookup"><span data-stu-id="3e29a-174">The TaskInfo object</span></span>

<span data-ttu-id="3e29a-175">`TaskInfo`オブジェクトには、タスク モジュールのメタデータが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3e29a-175">The `TaskInfo` object contains the metadata for a task module.</span></span> <span data-ttu-id="3e29a-176">オブジェクト定義は以下の通りです。</span><span class="sxs-lookup"><span data-stu-id="3e29a-176">The object definition is below.</span></span> <span data-ttu-id="3e29a-177"> `url` 埋め込み iFrame または `card` アダプティブ カードのどちらかを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-177">You **must** define either `url` for an embedded iFrame or `card` for an Adaptive Card.</span></span>

| <span data-ttu-id="3e29a-178">属性</span><span class="sxs-lookup"><span data-stu-id="3e29a-178">Attribute</span></span> | <span data-ttu-id="3e29a-179">種類</span><span class="sxs-lookup"><span data-stu-id="3e29a-179">Type</span></span> | <span data-ttu-id="3e29a-180">説明</span><span class="sxs-lookup"><span data-stu-id="3e29a-180">Description</span></span> |
| --- | --- | --- |
| `title` | <span data-ttu-id="3e29a-181">string</span><span class="sxs-lookup"><span data-stu-id="3e29a-181">string</span></span> | <span data-ttu-id="3e29a-182">アプリ名の下、アプリアイコンの右側に表示されます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-182">Appears below the app name and to the right of the app icon.</span></span> |
| `height` | <span data-ttu-id="3e29a-183">number または string</span><span class="sxs-lookup"><span data-stu-id="3e29a-183">number or string</span></span> | <span data-ttu-id="3e29a-184">これは、タスク モジュールの高さをピクセル単位で表す数値、または `small` `medium` 、、または を表す数値です `large` 。</span><span class="sxs-lookup"><span data-stu-id="3e29a-184">This can be a number representing the task module's height in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="3e29a-185">[高さと幅の取り扱いについては、以下を参照](#task-module-sizing)してください。</span><span class="sxs-lookup"><span data-stu-id="3e29a-185">[See below for how height and width are handled](#task-module-sizing).</span></span> |
| `width` | <span data-ttu-id="3e29a-186">number または string</span><span class="sxs-lookup"><span data-stu-id="3e29a-186">number or string</span></span> | <span data-ttu-id="3e29a-187">これは、タスク モジュールの幅をピクセル単位で表す数値、または `small` `medium` 、、または を表す数値です `large` 。</span><span class="sxs-lookup"><span data-stu-id="3e29a-187">This can be a number representing the task module's width in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="3e29a-188">[高さと幅の取り扱いについては、以下を参照](#task-module-sizing)してください。</span><span class="sxs-lookup"><span data-stu-id="3e29a-188">[See below for how height and width are handled](#task-module-sizing).</span></span> |
| `url` | <span data-ttu-id="3e29a-189">string</span><span class="sxs-lookup"><span data-stu-id="3e29a-189">string</span></span> | <span data-ttu-id="3e29a-190">タスク モジュール内に読み込まれたページ `<iframe>` の URL。</span><span class="sxs-lookup"><span data-stu-id="3e29a-190">The URL of the page loaded as an `<iframe>` inside the task module.</span></span> <span data-ttu-id="3e29a-191">URL のドメインは、アプリのマニフェストのアプリの [validDomains 配列](~/resources/schema/manifest-schema.md#validdomains) に含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-191">The URL's domain must be in the app's [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in your app's manifest.</span></span> |
| `card` | <span data-ttu-id="3e29a-192">アダプティブ カードまたはアダプティブ カード ボット カードアタッチメント</span><span class="sxs-lookup"><span data-stu-id="3e29a-192">Adaptive card or an Adaptive card bot card attachment</span></span> | <span data-ttu-id="3e29a-193">タスク モジュールに表示されるアダプティブ カードの JSON。</span><span class="sxs-lookup"><span data-stu-id="3e29a-193">The JSON for the Adaptive card to appear in the task module.</span></span> <span data-ttu-id="3e29a-194">ボットから呼び出す場合は、Bot Framework オブジェクトでアダプティブ カード JSON を使用する必要があります `attachment` 。</span><span class="sxs-lookup"><span data-stu-id="3e29a-194">If you're invoking from a bot, you'll need to use the Adaptive card JSON in a Bot Framework `attachment` object.</span></span> <span data-ttu-id="3e29a-195">タブからは、アダプティブカードだけを使用します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-195">From a tab you'll use just an Adaptive Card.</span></span> [<span data-ttu-id="3e29a-196">例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-196">Here's an example.</span></span>](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | <span data-ttu-id="3e29a-197">string</span><span class="sxs-lookup"><span data-stu-id="3e29a-197">string</span></span> | <span data-ttu-id="3e29a-198">クライアントがタスク モジュール機能をサポートしていない場合、この URL はブラウザー タブで開かれます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-198">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |
| `completionBotId` | <span data-ttu-id="3e29a-199">string</span><span class="sxs-lookup"><span data-stu-id="3e29a-199">string</span></span> | <span data-ttu-id="3e29a-200">ユーザーがタスク モジュールと対話した結果を送信するボット アプリ ID を指定します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-200">Specifies a bot App ID to send the result of the user's interaction with the task module to.</span></span> <span data-ttu-id="3e29a-201">指定した場合、ボットは `task/submit invoke` イベントペイロード内の JSON オブジェクトを含むイベントを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-201">If specified, the bot will receive a `task/submit invoke` event with a JSON object in the event payload.</span></span> |

> [!NOTE]
> <span data-ttu-id="3e29a-202">タスク モジュール機能では、読み込む URL のドメインが `validDomains` アプリのマニフェストの配列に含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-202">The task module feature requires that the domains of any URLs you want to load are included in the `validDomains` array in your app's manifest.</span></span>

## <a name="task-module-sizing"></a><span data-ttu-id="3e29a-203">タスク モジュールのサイズ変更</span><span class="sxs-lookup"><span data-stu-id="3e29a-203">Task module sizing</span></span>

<span data-ttu-id="3e29a-204">整数を使用 `TaskInfo.width` し、 `TaskInfo.height` 高さと幅をピクセル単位で設定します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-204">Using integers for `TaskInfo.width` and `TaskInfo.height` will set the height and width in pixels.</span></span> <span data-ttu-id="3e29a-205">ただし、チームのウィンドウのサイズと画面の解像度によっては、縦横比 (幅/高さ) を維持しながら、比例して縮小されます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-205">However, depending on the size of the Team's window and screen resolution they will be reduced proportionally while maintaining the aspect ratio (width/height).</span></span>

<span data-ttu-id="3e29a-206">`TaskInfo.width`と `TaskInfo.height` である場合 `"small"` 、 `"medium"` または `"large"` 上の図の赤い長方形のサイズは、利用可能なスペースの割合です:20%、50%、60% `width` と20%、50%、66%。 `height`</span><span class="sxs-lookup"><span data-stu-id="3e29a-206">If `TaskInfo.width` and `TaskInfo.height` are `"small"`, `"medium"` or `"large"` the size of the red rectangle in the picture above is a proportion of the available space: 20%, 50%, 60% for `width` and 20%, 50%, 66% for `height`.</span></span>

<span data-ttu-id="3e29a-207">タブから呼び出されたタスク モジュールのサイズを動的に変更できます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-207">Task modules invoked from a tab can be dynamically resized.</span></span> <span data-ttu-id="3e29a-208">呼び出し後 `tasks.startTask()` に `tasks.updateTask(newSize)` newSize オブジェクトの高さと幅のプロパティが TaskInfo 仕様 (例.</span><span class="sxs-lookup"><span data-stu-id="3e29a-208">After calling `tasks.startTask()` you can call `tasks.updateTask(newSize)` where height and width properties on the newSize object conform to the TaskInfo spec (ex.</span></span> <span data-ttu-id="3e29a-209">`{ height: 'medium', width: 'medium' }`).</span><span class="sxs-lookup"><span data-stu-id="3e29a-209">`{ height: 'medium', width: 'medium' }`).</span></span>

## <a name="task-module-css-for-htmljavascript-task-modules"></a><span data-ttu-id="3e29a-210">HTML/JavaScript タスクモジュールのタスクモジュール CSS</span><span class="sxs-lookup"><span data-stu-id="3e29a-210">Task module CSS for HTML/JavaScript task modules</span></span>

<span data-ttu-id="3e29a-211">HTML/JavaScript ベースのタスクモジュールは、ヘッダーの下にあるタスクモジュールの領域全体にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-211">HTML/JavaScript-based task modules have access to the entire area of the task module below the header.</span></span> <span data-ttu-id="3e29a-212">これは非常に柔軟性がありますが、ヘッダー要素に合わせてエッジの周りにパディングを行い、不要なスクロールバーを避ける場合は、適切なCSSを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-212">While that offers a great deal of flexibility, if you want padding around the edges to align with the header elements and avoid unnecessary scrollbars you'll need to provide the right CSS.</span></span> <span data-ttu-id="3e29a-213">いくつかの使用例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-213">Here are some examples for a few use cases.</span></span>

### <a name="example-1---youtube-video"></a><span data-ttu-id="3e29a-214">例 1 - YouTube 動画</span><span class="sxs-lookup"><span data-stu-id="3e29a-214">Example 1 - YouTube video</span></span>

<span data-ttu-id="3e29a-215">YouTube では、Web ページに動画を埋め込むことができます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-215">YouTube offers the ability to embed videos on web pages.</span></span> <span data-ttu-id="3e29a-216">単純なスタブ Web ページを使用すると、タスク モジュールでこれを簡単に表示できます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-216">Using a simple stub web page it's easy to show this in a task module:</span></span>

![ユーチューブ動画](~/assets/images/task-module/youtube-example.png)

<span data-ttu-id="3e29a-218">CSS を使用しないこのページの HTML は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="3e29a-218">Here's the HTML for this page, without the CSS:</span></span>

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

<span data-ttu-id="3e29a-219">CSS は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-219">The CSS looks like this:</span></span>

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

### <a name="example-2---powerapp"></a><span data-ttu-id="3e29a-220">例 2 - パワーアプリ</span><span class="sxs-lookup"><span data-stu-id="3e29a-220">Example 2 - PowerApp</span></span>

<span data-ttu-id="3e29a-221">PowerApp を埋め込むのと同じアプローチを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-221">You can use the same approach to embed a PowerApp as well.</span></span> <span data-ttu-id="3e29a-222">個々のPowerAppの高さ/幅はカスタマイズ可能であるため、必要なプレゼンテーションを実現するために高さと幅を調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-222">As the height/width of any individual PowerApp is customizable, you may need to adjust the height and width to achieve your desired presentation.</span></span>

![資産管理パワーアプリ](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

<span data-ttu-id="3e29a-224">そして、CSSは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="3e29a-224">And the CSS is:</span></span>

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a><span data-ttu-id="3e29a-225">アダプティブ カードまたはアダプティブ カード ボット カードアタッチメント</span><span class="sxs-lookup"><span data-stu-id="3e29a-225">Adaptive card or Adaptive card bot card attachment</span></span>

<span data-ttu-id="3e29a-226">上記で説明したように、どのように呼び出すかに応じて `card` 、アダプティブ カードまたはアダプティブ カード ボット カードアタッチメント (添付オブジェクトにラップされたアダプティブ カード) を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-226">As we noted above, depending on how you're invoking your `card` you'll need to use either an Adaptive card, or an Adaptive card bot card attachment (which is just an Adaptive card wrapped in an attachment object).</span></span>

<span data-ttu-id="3e29a-227">タブから呼び出す場合は、アダプティブ カードを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-227">When you're invoking from a tab, you'll need to use an adaptive card.</span></span> <span data-ttu-id="3e29a-228">次に、非常に簡単な例を示します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-228">Here's a very simple example:</span></span>

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

<span data-ttu-id="3e29a-229">ボットから呼び出す場合は、次の例のようにアダプティブ カード のボット カードアタッチメントを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-229">When you're invoking from a bot you'll need to use an Adaptive card bot card attachment as in the example below:</span></span>

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

<span data-ttu-id="3e29a-230">ボットまたはタブから Adaptive カードを含むタスク モジュールを呼び出すかどうかを覚えておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-230">You'll need to remember whether you are invoking a task module containing an Adaptive card from a bot or a tab.</span></span>

## <a name="task-module-deep-link-syntax"></a><span data-ttu-id="3e29a-231">タスク モジュールのディープ リンク構文</span><span class="sxs-lookup"><span data-stu-id="3e29a-231">Task module deep link syntax</span></span>

<span data-ttu-id="3e29a-232">タスク モジュールのディープ リンクは、他の 2 つの情報を含む [TaskInfo オブジェクト](#the-taskinfo-object) のシリアル化 `APP_ID` であり、オプションで `BOT_APP_ID` :</span><span class="sxs-lookup"><span data-stu-id="3e29a-232">A task module deep link is just a serialization of the [TaskInfo object](#the-taskinfo-object) with two other pieces of information, `APP_ID` and optionally the `BOT_APP_ID`:</span></span>

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

<span data-ttu-id="3e29a-233">データ型および 、 、 、および の許容値については、 [TaskInfo オブジェクト](#the-taskinfo-object) `<TaskInfo.url>` を参照 `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` してください。</span><span class="sxs-lookup"><span data-stu-id="3e29a-233">See [TaskInfo object](#the-taskinfo-object) for the data types and allowable values for `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`, and `<TaskInfo.title>`.</span></span>

> [!TIP]
> <span data-ttu-id="3e29a-234">特にパラメータを使用する場合は、ディープリンクをURLエンコードしてください `card` (例えば、JavaScriptの[ `encodeURI()` 関数](https://www.w3schools.com/jsref/jsref_encodeURI.asp))。</span><span class="sxs-lookup"><span data-stu-id="3e29a-234">Be sure to URL encode the deep link, especially when using the `card` parameter (for example, JavaScript's [`encodeURI()` function](https://www.w3schools.com/jsref/jsref_encodeURI.asp)).</span></span>

<span data-ttu-id="3e29a-235">以下に記載の情報 `APP_ID` を示 `BOT_APP_ID` します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-235">Here's the information on `APP_ID` and `BOT_APP_ID`:</span></span>

| <span data-ttu-id="3e29a-236">値</span><span class="sxs-lookup"><span data-stu-id="3e29a-236">Value</span></span> | <span data-ttu-id="3e29a-237">型</span><span class="sxs-lookup"><span data-stu-id="3e29a-237">Type</span></span> | <span data-ttu-id="3e29a-238">必須</span><span class="sxs-lookup"><span data-stu-id="3e29a-238">Required?</span></span> | <span data-ttu-id="3e29a-239">説明</span><span class="sxs-lookup"><span data-stu-id="3e29a-239">Description</span></span> |
| --- | --- | --- | --- |
| `APP_ID` | <span data-ttu-id="3e29a-240">string</span><span class="sxs-lookup"><span data-stu-id="3e29a-240">string</span></span> | <span data-ttu-id="3e29a-241">はい</span><span class="sxs-lookup"><span data-stu-id="3e29a-241">Yes</span></span> | <span data-ttu-id="3e29a-242">タスク モジュールを呼び出すアプリの[ID。](~/resources/schema/manifest-schema.md#id)</span><span class="sxs-lookup"><span data-stu-id="3e29a-242">The [id](~/resources/schema/manifest-schema.md#id) of the app invoking the task module.</span></span> <span data-ttu-id="3e29a-243">マニフェスト内の [validDomains 配列](~/resources/schema/manifest-schema.md#validdomains) には `APP_ID` `url` 、URL に存在する場合のドメインが含まれている必要があります `url` 。</span><span class="sxs-lookup"><span data-stu-id="3e29a-243">The [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in the manifest for `APP_ID` must contain the domain for `url` if `url` is in the URL.</span></span> <span data-ttu-id="3e29a-244">(このアプリ ID は、タブまたはボットからタスク モジュールが呼び出されたときに既に認識されています `TaskInfo` 。</span><span class="sxs-lookup"><span data-stu-id="3e29a-244">(The app ID is already known when a task module is invoked from a tab or a bot, which is why it's not included in `TaskInfo`.)</span></span> |
| `BOT_APP_ID` | <span data-ttu-id="3e29a-245">文字列</span><span class="sxs-lookup"><span data-stu-id="3e29a-245">string</span></span> | <span data-ttu-id="3e29a-246">いいえ</span><span class="sxs-lookup"><span data-stu-id="3e29a-246">No</span></span> | <span data-ttu-id="3e29a-247">の値 `completionBotId` が指定されている場合、 `result` オブジェクトはメッセージを介して `task/submit invoke` 指定されたボットに送信されます。</span><span class="sxs-lookup"><span data-stu-id="3e29a-247">If a value for `completionBotId` is specified, the `result` object is sent via a a `task/submit invoke` message to the specified bot.</span></span> <span data-ttu-id="3e29a-248">`BOT_APP_ID` アプリのマニフェストでボットとして指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-248">`BOT_APP_ID` must be specified as a bot in the app's manifest, i.e. you can't just send it to any bot.</span></span> |

<span data-ttu-id="3e29a-249">それは有効であり `APP_ID` `BOT_APP_ID` 、同じであることに注意してください、そして多くの場合、アプリがボットを持っている場合、それをアプリのIDとして使用することをお勧めします(もしある場合)。</span><span class="sxs-lookup"><span data-stu-id="3e29a-249">Note that it's valid for `APP_ID` and `BOT_APP_ID` to be the same, and in many cases will be if an app has a bot since it's recommended to use that as an app's ID if there is one.</span></span>

## <a name="keyboard-and-accessibility-guidelines"></a><span data-ttu-id="3e29a-250">キーボードとユーザー補助のガイドライン</span><span class="sxs-lookup"><span data-stu-id="3e29a-250">Keyboard and accessibility guidelines</span></span>

<span data-ttu-id="3e29a-251">HTML/JavaScript ベースのタスクモジュールでは、アプリのタスクモジュールをキーボードで使用できるようにする責任があります。</span><span class="sxs-lookup"><span data-stu-id="3e29a-251">With HTML/JavaScript-based task modules it is your responsibility to ensure your app's task module can be used with a keyboard.</span></span> <span data-ttu-id="3e29a-252">スクリーン リーダー プログラムは、キーボードを使用して移動する機能にも依存します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-252">Screen reader programs also depend on the ability to navigate using the keyboard.</span></span> <span data-ttu-id="3e29a-253">現実的な問題として、これは2つのことを意味します:</span><span class="sxs-lookup"><span data-stu-id="3e29a-253">As a practical matter this means two things:</span></span>

1. <span data-ttu-id="3e29a-254">HTML タグの [tabindex 属性](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) を使用して、フォーカスを設定できる要素と、その要素が連続したキーボード ナビゲーションに参加するかどうか(通常は <kbd>Tab</kbd> キーと Shift キーを押しながら <kbd>Tab キーを</kbd> 押す)を制御します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-254">Using the [tabindex attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) in your HTML tags to control which elements can be focused and if/where it participates in sequential keyboard navigation (usually with the <kbd>Tab</kbd> and <kbd>Shift-Tab</kbd> keys).</span></span>
2. <span data-ttu-id="3e29a-255">タスク モジュールの JavaScript で <kbd>Esc</kbd> キーを処理します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-255">Handling the <kbd>Esc</kbd> key in the JavaScript for your task module.</span></span> <span data-ttu-id="3e29a-256">これを行う方法を示すコード サンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-256">Here's a code sample showing how to do this:</span></span>

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

<span data-ttu-id="3e29a-257">Microsoft Teams、タスク モジュール ヘッダーから HTML にキーボード ナビゲーションが正しく動作し、その逆が正しく機能することを保証します。</span><span class="sxs-lookup"><span data-stu-id="3e29a-257">Microsoft Teams will ensure that keyboard navigation works properly from the task module header into your HTML and vice-versa.</span></span>

## <a name="code-sample"></a><span data-ttu-id="3e29a-258">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="3e29a-258">Code sample</span></span>
|<span data-ttu-id="3e29a-259">**サンプル名**</span><span class="sxs-lookup"><span data-stu-id="3e29a-259">**Sample name**</span></span> | <span data-ttu-id="3e29a-260">**説明**</span><span class="sxs-lookup"><span data-stu-id="3e29a-260">**Description**</span></span> | <span data-ttu-id="3e29a-261">**.NET**</span><span class="sxs-lookup"><span data-stu-id="3e29a-261">**.NET**</span></span> | <span data-ttu-id="3e29a-262">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="3e29a-262">**Node.js**</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="3e29a-263">タスクモジュールのサンプル(Bots-V4)</span><span class="sxs-lookup"><span data-stu-id="3e29a-263">Task module sample (Bots-V4)</span></span> | <span data-ttu-id="3e29a-264">タスクモジュールを作成するためのサンプルです。</span><span class="sxs-lookup"><span data-stu-id="3e29a-264">Samples for creating task modules.</span></span> |[<span data-ttu-id="3e29a-265">View</span><span class="sxs-lookup"><span data-stu-id="3e29a-265">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[<span data-ttu-id="3e29a-266">View</span><span class="sxs-lookup"><span data-stu-id="3e29a-266">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 
|<span data-ttu-id="3e29a-267">タスク モジュールのサンプル (タブ + ボット V3)</span><span class="sxs-lookup"><span data-stu-id="3e29a-267">Task module sample (Tabs + Bots-V3)</span></span> | <span data-ttu-id="3e29a-268">タスクモジュールを作成するためのサンプルです。</span><span class="sxs-lookup"><span data-stu-id="3e29a-268">Samples for creating task modules.</span></span> |[<span data-ttu-id="3e29a-269">View</span><span class="sxs-lookup"><span data-stu-id="3e29a-269">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[<span data-ttu-id="3e29a-270">View</span><span class="sxs-lookup"><span data-stu-id="3e29a-270">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a><span data-ttu-id="3e29a-271">関連項目</span><span class="sxs-lookup"><span data-stu-id="3e29a-271">See also</span></span>

* [<span data-ttu-id="3e29a-272">デバイスのアクセス許可を要求する</span><span class="sxs-lookup"><span data-stu-id="3e29a-272">Request device permissions</span></span>](../concepts/device-capabilities/native-device-permissions.md)
* [<span data-ttu-id="3e29a-273">メディア機能を統合する</span><span class="sxs-lookup"><span data-stu-id="3e29a-273">Integrate media capabilities</span></span>](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [<span data-ttu-id="3e29a-274">TeamsでQRまたはバーコードスキャナ機能を統合</span><span class="sxs-lookup"><span data-stu-id="3e29a-274">Integrate QR or barcode scanner capability in Teams</span></span>](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [<span data-ttu-id="3e29a-275">Teamsでの位置情報機能の統合</span><span class="sxs-lookup"><span data-stu-id="3e29a-275">Integrate location capabilities in Teams</span></span>](../concepts/device-capabilities/location-capability.md)
