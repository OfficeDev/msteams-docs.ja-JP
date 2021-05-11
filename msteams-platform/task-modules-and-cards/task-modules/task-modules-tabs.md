---
title: '[タスク モジュール] タブでのタスク Microsoft Teams使用する'
description: クライアント SDK を使用してタスク モジュールTeamsタブからMicrosoft Teams説明します。
localization_priority: Normal
ms.topic: how-to
keywords: タスク モジュールチームがクライアント SDK をタブする
ms.openlocfilehash: 5e85fd0662b8a15d6b98d9c2d2dfa5137b05fa39
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019525"
---
# <a name="using-task-modules-in-tabs"></a><span data-ttu-id="21d06-104">タブでタスク モジュールを使用する</span><span class="sxs-lookup"><span data-stu-id="21d06-104">Using task modules in tabs</span></span>

<span data-ttu-id="21d06-105">タブにタスク モジュールを追加すると、データ入力が必要なワークフローに対するユーザー エクスペリエンスが大幅に簡素化されます。</span><span class="sxs-lookup"><span data-stu-id="21d06-105">Adding a task module to your tab can greatly simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="21d06-106">タスク モジュールを使用すると、ユーザーが認識できるポップアップTeamsを収集できます。</span><span class="sxs-lookup"><span data-stu-id="21d06-106">Task modules allow you to gather their input in a Teams-aware popup.</span></span> <span data-ttu-id="21d06-107">この例の良い例は、Planner カードの編集です。タスク モジュールを使用して同様のエクスペリエンスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="21d06-107">A good example of this is editing Planner cards; you can use task modules to create a similar experience.</span></span>

<span data-ttu-id="21d06-108">タスク モジュール機能をサポートするために、次の 2 つの新しい機能がクライアント[SDK Microsoft Teams追加されました](/javascript/api/overview/msteams-client)。</span><span class="sxs-lookup"><span data-stu-id="21d06-108">To support the task module feature, two new functions were added to the [Microsoft Teams client SDK](/javascript/api/overview/msteams-client):</span></span>

```typescript
microsoftTeams.tasks.startTask(
    taskInfo: TaskInfo,
    submitHandler?: (err: string, result: string | any) => void
): void;

microsoftTeams.tasks.submitTask(
    result?: string | any,
    appIds?: string | string[]
): void;
```

<span data-ttu-id="21d06-109">それぞれの動作を見てみよ。</span><span class="sxs-lookup"><span data-stu-id="21d06-109">Let's see how each of them work.</span></span>

## <a name="invoking-a-task-module-from-a-tab"></a><span data-ttu-id="21d06-110">タブからのタスク モジュールの呼び出し</span><span class="sxs-lookup"><span data-stu-id="21d06-110">Invoking a task module from a tab</span></span>

<span data-ttu-id="21d06-111">タブからタスク モジュールを呼び出す場合は `microsoftTeams.tasks.startTask()` [、TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) オブジェクトとオプションのコールバック関数を渡 `submitHandler` します。</span><span class="sxs-lookup"><span data-stu-id="21d06-111">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="21d06-112">前述したように、次の 2 つのケースを考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="21d06-112">As described earlier, there are two cases to consider:</span></span>

1. <span data-ttu-id="21d06-113">の値 `TaskInfo.url` は URL に設定されます。</span><span class="sxs-lookup"><span data-stu-id="21d06-113">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="21d06-114">タスク モジュール ウィンドウが表示され `TaskModule.url` 、内部として `<iframe>` 読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="21d06-114">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="21d06-115">そのページの JavaScript を呼び出す必要があります `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="21d06-115">JavaScript on that page should call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="21d06-116">ページに関数が存在し、呼び出し時にエラーが発生した場合は、次に説明するようにエラーを示すエラー文字列に設定して `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` 呼び出 [されます](#task-module-invocation-errors)。</span><span class="sxs-lookup"><span data-stu-id="21d06-116">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the error as described [below](#task-module-invocation-errors).</span></span>
1. <span data-ttu-id="21d06-117">値はアダプティブ `taskInfo.card` カード [の JSON です](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)。</span><span class="sxs-lookup"><span data-stu-id="21d06-117">The value of `taskInfo.card` is the [JSON for an Adaptive card](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="21d06-118">この場合、ユーザーがアダプティブ カードのボタンを閉じるか押した場合に呼び出す JavaScript 関数は明らかではありません。ユーザーが入力した値を受け取る唯一の方法は、結果をボットに渡す方法です。 `submitHandler`</span><span class="sxs-lookup"><span data-stu-id="21d06-118">In this case there's obviously not any JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive card; the only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="21d06-119">タブからアダプティブ カード タスク モジュールを使用するには、ユーザーから情報を取得するために、アプリにボットを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="21d06-119">To use an Adaptive card task module from a tab your app must include a bot to get any information back from the user.</span></span> <span data-ttu-id="21d06-120">これは以下で説明します。</span><span class="sxs-lookup"><span data-stu-id="21d06-120">This is explained below.</span></span>

## <a name="example-invoking-a-task-module"></a><span data-ttu-id="21d06-121">例: タスク モジュールの呼び出し</span><span class="sxs-lookup"><span data-stu-id="21d06-121">Example: Invoking a task module</span></span>

<span data-ttu-id="21d06-122">以下のコードは、タスク モジュールの [サンプルから適合しています](~/task-modules-and-cards/what-are-task-modules.md#code-sample)。</span><span class="sxs-lookup"><span data-stu-id="21d06-122">The code below is adapted from [the task module sample](~/task-modules-and-cards/what-are-task-modules.md#code-sample).</span></span> <span data-ttu-id="21d06-123">タスク モジュールの外観を次に示します。</span><span class="sxs-lookup"><span data-stu-id="21d06-123">Here's what the task module looks like:</span></span>

![タスク モジュール - カスタム フォーム](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="21d06-125">これは `submitHandler` 非常に単純です。コンソールの値またはコンソール `err` に `result` エコーします。</span><span class="sxs-lookup"><span data-stu-id="21d06-125">The `submitHandler` is very simple; it just echoes the value of `err` or `result` to the console:</span></span>

```javascript
let taskInfo = {
    title: null,
    height: null,
    width: null,
    url: null,
    card: null,
    fallbackUrl: null,
    completionBotId: null,
};

taskInfo.url = "https://contoso.com/teamsapp/customform";
taskInfo.title = "Custom Form";
taskInfo.height = 510;
taskInfo.width = 430;
submitHandler = (err, result) => {
    console.log(`Submit handler - err: ${err}`);
    console.log(`Submit handler - result\rName: ${result.name}\rEmail: ${result.email}\rFavorite book: ${result.favoriteBook}`);
};
microsoftTeams.tasks.startTask(taskInfo, submitHandler);
```

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="21d06-126">タスク モジュールの結果の送信</span><span class="sxs-lookup"><span data-stu-id="21d06-126">Submitting the result of a task module</span></span>

<span data-ttu-id="21d06-127">この `submitHandler` 関数は、 と一緒に使用されます `TaskInfo.url` 。</span><span class="sxs-lookup"><span data-stu-id="21d06-127">The `submitHandler` function is used with `TaskInfo.url`.</span></span> <span data-ttu-id="21d06-128">関数 `submitHandler` は Web ページに `TaskInfo.url` 存在します。</span><span class="sxs-lookup"><span data-stu-id="21d06-128">The `submitHandler` function resides in the `TaskInfo.url` web page.</span></span> <span data-ttu-id="21d06-129">タスク モジュールを呼び出す際にエラーが発生した場合、関数は直ちに呼び出され、どのエラーが発生したのかを `submitHandler` `err` 示す文字列 [が表示されます](#task-module-invocation-errors)。</span><span class="sxs-lookup"><span data-stu-id="21d06-129">If there's an error when invoking the task module your `submitHandler` function will be immediately invoked with an `err` string indicating which [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="21d06-130">この関数は、ユーザーがタスク モジュールの右上にある X を押すと、文字列 `submitHandler` `err` で呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="21d06-130">The `submitHandler` function is also called with an `err` string when the user presses the X at the upper right of task module.</span></span>

<span data-ttu-id="21d06-131">呼び出しエラーが発生し、ユーザーが X キーを押して閉じなかった場合、ユーザーは終了するとボタンを押します。</span><span class="sxs-lookup"><span data-stu-id="21d06-131">If there's no invocation error and the user doesn't press X to dismiss it, the user presses a button when finished.</span></span> <span data-ttu-id="21d06-132">タスク モジュールの URL かアダプティブ カードかによって、次の処理が実行されます。</span><span class="sxs-lookup"><span data-stu-id="21d06-132">Depending on whether it's a URL or an Adaptive card in the task module, here's what happens:</span></span>

### <a name="htmljavascript-taskinfourl"></a><span data-ttu-id="21d06-133">HTML/JavaScript ( `TaskInfo.url` )</span><span class="sxs-lookup"><span data-stu-id="21d06-133">HTML/JavaScript (`TaskInfo.url`)</span></span>

<span data-ttu-id="21d06-134">ユーザーが入力した情報を検証したら、SDK 関数を呼び出します (以下、読みやすさの目的 `microsoftTeams.tasks.submitTask()` `submitTask()` で呼び出します)。</span><span class="sxs-lookup"><span data-stu-id="21d06-134">Once you've validated what the user has entered you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="21d06-135">Teams がタスク モジュールを閉じるだけで、ほとんどの場合、オブジェクトまたは文字列を自分のタスク モジュールに渡す場合は、パラメーターを指定せずに呼び出 `submitTask()` します `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="21d06-135">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="21d06-136">結果を最初のパラメーターとして渡します。</span><span class="sxs-lookup"><span data-stu-id="21d06-136">Pass your result as the first parameter.</span></span> <span data-ttu-id="21d06-137">Teamsが呼 `submitHandler` び出 `err` され、渡 `null` された `result` オブジェクト/文字列になります `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="21d06-137">Teams will invoke `submitHandler` where `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="21d06-138">パラメーターを使用して呼び出す場合は、文字列の配列または配列を渡す必要があります `submitTask()` `result`  `appId` `appId` 。これにより、Teams は、結果を送信するアプリがタスク モジュールを呼び出したアプリと同じことを検証できます。</span><span class="sxs-lookup"><span data-stu-id="21d06-138">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="21d06-139">アダプティブ カード ( `TaskInfo.card` )</span><span class="sxs-lookup"><span data-stu-id="21d06-139">Adaptive card (`TaskInfo.card`)</span></span>

<span data-ttu-id="21d06-140">タスク モジュールを呼び出した場合、ユーザーがボタンを押すと、カード内の値がの値 `submitHandler` `Action.Submit` として返されます `result` 。</span><span class="sxs-lookup"><span data-stu-id="21d06-140">If you invoked the task module with a `submitHandler`, when the user presses an `Action.Submit` button the values in the card will be returned as the value of `result`.</span></span> <span data-ttu-id="21d06-141">ユーザーが Esc ボタンを押すか、X キーを押すと `err` 、代わりに返されます。</span><span class="sxs-lookup"><span data-stu-id="21d06-141">If the user presses the Esc button or presses the X, `err` will be returned instead.</span></span> <span data-ttu-id="21d06-142">または、タブに加えてアプリにボットが含まれている場合は、単にボットの値をオブジェクトに `appId` `completionBotId` 含 `TaskInfo` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="21d06-142">Alternatively, if your app contains a bot in addition to a tab you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="21d06-143">アダプティブ カード本文 (ユーザーが入力した場合) は、ユーザーがボタンを押すと、メッセージを介してボット `task/submit invoke` に送信 `Action.Submit` されます。</span><span class="sxs-lookup"><span data-stu-id="21d06-143">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit invoke` message when the user presses an `Action.Submit` button.</span></span> <span data-ttu-id="21d06-144">受信するオブジェクトのスキーマは、タスク/フェッチおよびタスク/送信メッセージで受け取る[スキーマと非常に似ています](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)。唯一の違いは、JSON オブジェクトのスキーマがアダプティブ カード オブジェクトで、アダプティブカード オブジェクトを含むオブジェクト[](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)ではなく、アダプティブ カード オブジェクトである点です。</span><span class="sxs-lookup"><span data-stu-id="21d06-144">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); the only difference is that the schema of the JSON object is an Adaptive card object as opposed to an object *containing* an Adaptive card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

## <a name="example-submitting-the-result-of-a-task-module"></a><span data-ttu-id="21d06-145">例: タスク モジュールの結果の送信</span><span class="sxs-lookup"><span data-stu-id="21d06-145">Example: submitting the result of a task module</span></span>

<span data-ttu-id="21d06-146">上記の [タスク モジュールのフォームを](#example-invoking-a-task-module) HTML フォームで呼び出します。</span><span class="sxs-lookup"><span data-stu-id="21d06-146">Recall the [form in the task module above](#example-invoking-a-task-module) with an HTML form.</span></span> <span data-ttu-id="21d06-147">フォームが定義されている場所を次に示します。</span><span class="sxs-lookup"><span data-stu-id="21d06-147">Here's where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="21d06-148">このフォームには 5 つのフィールドがありますが、この例では、3 つのフィールドの値にのみ関心 `name` があります。 `email` `favoriteBook`</span><span class="sxs-lookup"><span data-stu-id="21d06-148">There are five fields on this form but we're only interested in the values of three of them for this example: `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="21d06-149">呼び出す `validateForm()` 関数を次に示します `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="21d06-149">Here's the `validateForm()` function that calls `submitTask()`:</span></span>

```javascript
function validateForm() {
    var customerInfo = {
        name: document.forms["customerForm"]["name"].value,
        email: document.forms["customerForm"]["email"].value,
        favoriteBook: document.forms["customerForm"]["favoriteBook"].value
    }
    microsoftTeams.tasks.submitTask(customerInfo, "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx");
    return true;
}
```

## <a name="task-module-invocation-errors"></a><span data-ttu-id="21d06-150">タスク モジュール呼び出しのエラー</span><span class="sxs-lookup"><span data-stu-id="21d06-150">Task module invocation errors</span></span>

<span data-ttu-id="21d06-151">以下に、ユーザーが受 `err` け取る可能性の値を示します `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="21d06-151">Here are the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="21d06-152">問題</span><span class="sxs-lookup"><span data-stu-id="21d06-152">Problem</span></span> | <span data-ttu-id="21d06-153">エラー メッセージ (値 `err` )</span><span class="sxs-lookup"><span data-stu-id="21d06-153">Error message (value of `err`)</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="21d06-154">両方の値と `TaskInfo.url` 指定 `TaskInfo.card` された値。</span><span class="sxs-lookup"><span data-stu-id="21d06-154">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="21d06-155">"カードと URL の両方の値が指定されました。</span><span class="sxs-lookup"><span data-stu-id="21d06-155">"Values for both card and url were specified.</span></span> <span data-ttu-id="21d06-156">一方または他の両方は許可されません。</span><span class="sxs-lookup"><span data-stu-id="21d06-156">One or the other, but not both, are allowed."</span></span> |
| <span data-ttu-id="21d06-157">指定も `TaskInfo.url` `TaskInfo.card` 指定もされていません。</span><span class="sxs-lookup"><span data-stu-id="21d06-157">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="21d06-158">"カードまたは URL の値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="21d06-158">"You must specify a value for either card or url."</span></span> |
| <span data-ttu-id="21d06-159">無効 `appId` です。</span><span class="sxs-lookup"><span data-stu-id="21d06-159">Invalid `appId`.</span></span> | <span data-ttu-id="21d06-160">"無効な appId"</span><span class="sxs-lookup"><span data-stu-id="21d06-160">"Invalid appId."</span></span> |
| <span data-ttu-id="21d06-161">ユーザーが X ボタンを押し、閉じる。</span><span class="sxs-lookup"><span data-stu-id="21d06-161">User pressed X button, closing it.</span></span> | <span data-ttu-id="21d06-162">"ユーザーがタスク モジュールを取り消し/閉じた。</span><span class="sxs-lookup"><span data-stu-id="21d06-162">"User cancelled/closed the task module."</span></span> |
