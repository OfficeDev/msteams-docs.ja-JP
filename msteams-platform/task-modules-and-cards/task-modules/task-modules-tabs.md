---
title: '[タスク モジュール] タブでタスク Microsoft Teams使用する'
description: クライアント SDK を使用して、Teamsタブからタスク モジュールMicrosoft Teams説明します。
localization_priority: Normal
ms.topic: how-to
keywords: タスク モジュールチームがクライアント SDK をタブする
ms.openlocfilehash: 8afd2c93261f28aa7ced4c98d29be27dca35f8b1
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140553"
---
# <a name="use-task-modules-in-tabs"></a><span data-ttu-id="4c173-104">タブでタスク モジュールを使用する</span><span class="sxs-lookup"><span data-stu-id="4c173-104">Use task modules in tabs</span></span>

<span data-ttu-id="4c173-105">タブにタスク モジュールを追加して、データ入力を必要とするワークフローに対するユーザー エクスペリエンスを簡略化します。</span><span class="sxs-lookup"><span data-stu-id="4c173-105">Add a task module to your tab to simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="4c173-106">タスク モジュールを使用すると、Microsoft のポップアップで入力をTeams-Awareできます。</span><span class="sxs-lookup"><span data-stu-id="4c173-106">Task modules allow you to gather their input in a Microsoft Teams-Aware pop-up.</span></span> <span data-ttu-id="4c173-107">この例の良い例は、Planner カードの編集です。</span><span class="sxs-lookup"><span data-stu-id="4c173-107">A good example of this is editing Planner cards.</span></span> <span data-ttu-id="4c173-108">タスク モジュールを使用して、同様のエクスペリエンスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="4c173-108">You can use task modules to create a similar experience.</span></span>

<span data-ttu-id="4c173-109">タスク モジュール機能をサポートするために、クライアント SDK に 2 つの[Teams追加されます](/javascript/api/overview/msteams-client)。</span><span class="sxs-lookup"><span data-stu-id="4c173-109">To support the task module feature, two new functions are added to the [Teams client SDK](/javascript/api/overview/msteams-client).</span></span> <span data-ttu-id="4c173-110">次のコードは、これら 2 つの関数の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="4c173-110">The following code shows an example of these two functions:</span></span>

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

<span data-ttu-id="4c173-111">タブからタスク モジュールを呼び出し、タスク モジュールの結果を送信する方法を確認できます。</span><span class="sxs-lookup"><span data-stu-id="4c173-111">You can see how invoking a task module from a tab and submitting the result of a task module works.</span></span>

## <a name="invoke-a-task-module-from-a-tab"></a><span data-ttu-id="4c173-112">タブからタスク モジュールを呼び出す</span><span class="sxs-lookup"><span data-stu-id="4c173-112">Invoke a task module from a tab</span></span>

<span data-ttu-id="4c173-113">タブからタスク モジュールを呼び出す場合は `microsoftTeams.tasks.startTask()` [、TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) オブジェクトとオプションのコールバック関数を渡 `submitHandler` します。</span><span class="sxs-lookup"><span data-stu-id="4c173-113">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="4c173-114">次の 2 つのケースを考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c173-114">There are two cases to consider:</span></span>

* <span data-ttu-id="4c173-115">の値 `TaskInfo.url` は URL に設定されます。</span><span class="sxs-lookup"><span data-stu-id="4c173-115">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="4c173-116">タスク モジュール ウィンドウが表示され `TaskModule.url` 、内部として `<iframe>` 読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="4c173-116">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="4c173-117">そのページ呼び出しの JavaScript `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="4c173-117">JavaScript on that page calls `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="4c173-118">ページに関数が存在し、呼び出し時にエラーが発生した場合は、同じことを示すエラー文字列に設定して `submitHandler` `microsoftTeams.tasks.startTask()` 呼び `submitHandler` `err` 出されます。</span><span class="sxs-lookup"><span data-stu-id="4c173-118">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the same.</span></span> <span data-ttu-id="4c173-119">詳細については、「タスク モジュールの呼び [出しエラー」を参照してください](#task-module-invocation-errors)。</span><span class="sxs-lookup"><span data-stu-id="4c173-119">For more information, see [task module invocation errors](#task-module-invocation-errors).</span></span>
* <span data-ttu-id="4c173-120">値はアダプティブ `taskInfo.card` カード [の JSON です](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)。</span><span class="sxs-lookup"><span data-stu-id="4c173-120">The value of `taskInfo.card` is the [JSON for an Adaptive Card](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="4c173-121">ユーザーがアダプティブ カードのボタンを閉じるか押すと、呼び出す JavaScript `submitHandler` 関数はありません。</span><span class="sxs-lookup"><span data-stu-id="4c173-121">There is no JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive Card.</span></span> <span data-ttu-id="4c173-122">ユーザーが入力した情報を受け取る唯一の方法は、結果をボットに渡す方法です。</span><span class="sxs-lookup"><span data-stu-id="4c173-122">The only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="4c173-123">タブからアダプティブ カード タスク モジュールを使用するには、アプリにボットを含め、ユーザーからの応答を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c173-123">To use an Adaptive Card task module from a tab, your app must include a bot to get any response from the user.</span></span>

<span data-ttu-id="4c173-124">次のセクションでは、タスク モジュールを呼び出す例を示します。</span><span class="sxs-lookup"><span data-stu-id="4c173-124">The next section gives an example of invoking a task module.</span></span>

## <a name="example-of-invoking-a-task-module"></a><span data-ttu-id="4c173-125">タスク モジュールの呼び出しの例</span><span class="sxs-lookup"><span data-stu-id="4c173-125">Example of invoking a task module</span></span>

<span data-ttu-id="4c173-126">次の図は、タスク モジュールを表示します。</span><span class="sxs-lookup"><span data-stu-id="4c173-126">The following image displays the task module:</span></span>

![タスク モジュール - カスタム フォーム](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="4c173-128">次のコードは、タスク モジュール [のサンプルから適合しています](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample)。</span><span class="sxs-lookup"><span data-stu-id="4c173-128">The following code is adapted from [the task module sample](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample):</span></span>

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

<span data-ttu-id="4c173-129">これは `submitHandler` 非常に単純で、コンソールの値またはコンソール `err` `result` にエコーされます。</span><span class="sxs-lookup"><span data-stu-id="4c173-129">The `submitHandler` is very simple and it echoes the value of `err` or `result` to the console.</span></span>

## <a name="submit-the-result-of-a-task-module"></a><span data-ttu-id="4c173-130">タスク モジュールの結果を送信する</span><span class="sxs-lookup"><span data-stu-id="4c173-130">Submit the result of a task module</span></span>

<span data-ttu-id="4c173-131">この `submitHandler` 関数は Web ページに `TaskInfo.url` 存在し、で使用されます `TaskInfo.url` 。</span><span class="sxs-lookup"><span data-stu-id="4c173-131">The `submitHandler` function resides in the `TaskInfo.url` web page and is used with `TaskInfo.url`.</span></span> <span data-ttu-id="4c173-132">タスク モジュールを呼び出す際にエラーが発生した場合、関数は直ちに呼び出され、発生したエラーを示す `submitHandler` `err` 文字列 [が表示されます](#task-module-invocation-errors)。</span><span class="sxs-lookup"><span data-stu-id="4c173-132">If there is an error when invoking the task module, your `submitHandler` function is immediately invoked with an `err` string indicating what [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="4c173-133">この関数は、ユーザーがタスク モジュールの右上にある X を選択して閉じるときに、文字列を使用して `submitHandler` `err` 呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="4c173-133">The `submitHandler` function is also called with an `err` string when the user selects X at the upper right of the task module to close it.</span></span>

<span data-ttu-id="4c173-134">呼び出しエラーが発生し、ユーザーが X を選択して閉じない場合、ユーザーは終了するとボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="4c173-134">If there is no invocation error and the user does not select X to dismiss it, the user chooses a button when finished.</span></span> <span data-ttu-id="4c173-135">タスク モジュール内の URL かアダプティブ カードかによって、次のセクションでは、発生する内容の詳細を示します。</span><span class="sxs-lookup"><span data-stu-id="4c173-135">Depending on whether it is a URL or an Adaptive Card in the task module, the next sections provide details on what occurs.</span></span>

### <a name="html-or-javascript-taskinfourl"></a><span data-ttu-id="4c173-136">HTML または JavaScript `TaskInfo.url`</span><span class="sxs-lookup"><span data-stu-id="4c173-136">HTML or JavaScript `TaskInfo.url`</span></span>

<span data-ttu-id="4c173-137">ユーザーの入力を検証した後、と呼ばれる `microsoftTeams.tasks.submitTask()` SDK 関数を呼び出します `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="4c173-137">After validating the user's inputs, call the `microsoftTeams.tasks.submitTask()` SDK function referred to as `submitTask()`.</span></span> <span data-ttu-id="4c173-138">タスク `submitTask()` モジュールを閉じる必要がある場合Teamsパラメーターなしで呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4c173-138">Call `submitTask()` without any parameters if you just want Teams to close the task module.</span></span> <span data-ttu-id="4c173-139">オブジェクトまたは文字列を自分のオブジェクトに渡します `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="4c173-139">You can pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="4c173-140">結果を最初のパラメーターとして渡します。</span><span class="sxs-lookup"><span data-stu-id="4c173-140">Pass your result as the first parameter.</span></span> <span data-ttu-id="4c173-141">Teams、渡したオブジェクトまたは文字列が where で `submitHandler` `err` `null` `result` 呼び出されます `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="4c173-141">Teams invokes `submitHandler` where `err` is `null` and `result` is the object or string you passed to `submitTask()`.</span></span> <span data-ttu-id="4c173-142">パラメーターを使用 `submitTask()` して呼び出 `result` す場合は、文字列または文字列の `appId` 配列を渡す必要 `appId` があります。</span><span class="sxs-lookup"><span data-stu-id="4c173-142">If you call `submitTask()` with a `result` parameter, you must pass an `appId` or an array of `appId` strings.</span></span> <span data-ttu-id="4c173-143">これにより、Teams送信するアプリが呼び出されたタスク モジュールと同じことを検証できます。</span><span class="sxs-lookup"><span data-stu-id="4c173-143">This permits Teams to validate that the app sending the result is same as the invoked task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="4c173-144">アダプティブ カード `TaskInfo.card`</span><span class="sxs-lookup"><span data-stu-id="4c173-144">Adaptive Card `TaskInfo.card`</span></span>

<span data-ttu-id="4c173-145">タスク モジュールを a で呼び出し、ユーザーがボタンを選択すると、カード内の値がの値 `submitHandler` `Action.Submit` として返されます `result` 。</span><span class="sxs-lookup"><span data-stu-id="4c173-145">When you invoke the task module with a `submitHandler` and the user selects an `Action.Submit` button, the values in the card are returned as the value of `result`.</span></span> <span data-ttu-id="4c173-146">ユーザーが上部右側の Esc キーまたは X キーを選択すると `err` 、代わりに返されます。</span><span class="sxs-lookup"><span data-stu-id="4c173-146">If the user selects the Esc key or X at the top right, `err` is returned instead.</span></span> <span data-ttu-id="4c173-147">アプリにタブに加えてボットが含まれている場合は、ボットの値をオブジェクトに含 `appId` `completionBotId` `TaskInfo` める必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c173-147">If your app contains a bot in addition to a tab, you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="4c173-148">ユーザーが入力したアダプティブ カード本文は、ユーザーがボタンを選択すると、メッセージを使用してボット `task/submit invoke` に送信 `Action.Submit` されます。</span><span class="sxs-lookup"><span data-stu-id="4c173-148">The Adaptive Card body as filled in by the user is sent to the bot using a `task/submit invoke` message when the user selects an `Action.Submit` button.</span></span> <span data-ttu-id="4c173-149">受信するオブジェクトのスキーマは、タスク/フェッチおよびタスク/送信メッセージで受け取る [スキーマと非常に似ています](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)。</span><span class="sxs-lookup"><span data-stu-id="4c173-149">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="4c173-150">唯一の違いは、JSON オブジェクトのスキーマがアダプティブ カード オブジェクトで、アダプティブ カード オブジェクトを含むオブジェクト[](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)ではなく、アダプティブ カード オブジェクトである点です。</span><span class="sxs-lookup"><span data-stu-id="4c173-150">The only difference is that the schema of the JSON object is an Adaptive Card object as opposed to an object containing an Adaptive Card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

<span data-ttu-id="4c173-151">次のセクションでは、タスク モジュールの結果を送信する例を示します。</span><span class="sxs-lookup"><span data-stu-id="4c173-151">The next section gives an example of submitting the result of a task module.</span></span>

## <a name="example-of-submitting-the-result-of-a-task-module"></a><span data-ttu-id="4c173-152">タスク モジュールの結果を送信する例</span><span class="sxs-lookup"><span data-stu-id="4c173-152">Example of submitting the result of a task module</span></span>

<span data-ttu-id="4c173-153">詳細については、タスク モジュールの [HTML フォームを参照してください](#example-of-invoking-a-task-module)。</span><span class="sxs-lookup"><span data-stu-id="4c173-153">For more information, see the [HTML form in the task module](#example-of-invoking-a-task-module).</span></span> <span data-ttu-id="4c173-154">次のコードは、フォームが定義されている場所の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="4c173-154">The following code gives an example of where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="4c173-155">このフォームには 5 つのフィールドがありますが、この例では、3 つの値だけが必要 `name` です。 `email` `favoriteBook`</span><span class="sxs-lookup"><span data-stu-id="4c173-155">There are five fields on this form but for this example only three values are required, `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="4c173-156">次のコードは、呼び出す関数 `validateForm()` の例を示しています `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="4c173-156">The following code gives an example of the `validateForm()` function that calls `submitTask()`:</span></span>

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

<span data-ttu-id="4c173-157">次のセクションでは、タスク モジュールの呼び出しの問題とそのエラー メッセージを示します。</span><span class="sxs-lookup"><span data-stu-id="4c173-157">The next section provides task module invocation problems and their error messages.</span></span>

## <a name="task-module-invocation-errors"></a><span data-ttu-id="4c173-158">タスク モジュール呼び出しのエラー</span><span class="sxs-lookup"><span data-stu-id="4c173-158">Task module invocation errors</span></span>

<span data-ttu-id="4c173-159">次の表に、次の値を使用 `err` して受信できる値を示します `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="4c173-159">The following table provides the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="4c173-160">問題</span><span class="sxs-lookup"><span data-stu-id="4c173-160">Problem</span></span> | <span data-ttu-id="4c173-161">エラー メッセージの値 `err`</span><span class="sxs-lookup"><span data-stu-id="4c173-161">Error message that is value of `err`</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="4c173-162">両方の値と `TaskInfo.url` 指定 `TaskInfo.card` された値。</span><span class="sxs-lookup"><span data-stu-id="4c173-162">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="4c173-163">カードと URL の両方の値が指定されました。</span><span class="sxs-lookup"><span data-stu-id="4c173-163">Values for both card and URL were specified.</span></span> <span data-ttu-id="4c173-164">一方または他の両方を使用できますが、両方は許可されません。</span><span class="sxs-lookup"><span data-stu-id="4c173-164">One or the other, but not both, are allowed.</span></span> |
| <span data-ttu-id="4c173-165">指定も `TaskInfo.url` `TaskInfo.card` 指定もされていません。</span><span class="sxs-lookup"><span data-stu-id="4c173-165">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="4c173-166">カードまたは URL の値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4c173-166">You must specify a value for either card or URL.</span></span> |
| <span data-ttu-id="4c173-167">無効 `appId` です。</span><span class="sxs-lookup"><span data-stu-id="4c173-167">Invalid `appId`.</span></span> | <span data-ttu-id="4c173-168">アプリ ID が無効です。</span><span class="sxs-lookup"><span data-stu-id="4c173-168">Invalid app ID.</span></span> |
| <span data-ttu-id="4c173-169">ユーザーが X ボタンを選択し、閉じる。</span><span class="sxs-lookup"><span data-stu-id="4c173-169">User selected X button, closing it.</span></span> | <span data-ttu-id="4c173-170">ユーザーがタスク モジュールを取り消したり閉じたりしました。</span><span class="sxs-lookup"><span data-stu-id="4c173-170">User cancelled or closed the task module.</span></span> |

## <a name="code-sample"></a><span data-ttu-id="4c173-171">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="4c173-171">Code sample</span></span>

|<span data-ttu-id="4c173-172">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="4c173-172">Sample name</span></span> | <span data-ttu-id="4c173-173">説明</span><span class="sxs-lookup"><span data-stu-id="4c173-173">Description</span></span> | <span data-ttu-id="4c173-174">.NET</span><span class="sxs-lookup"><span data-stu-id="4c173-174">.NET</span></span> | <span data-ttu-id="4c173-175">Node.js</span><span class="sxs-lookup"><span data-stu-id="4c173-175">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="4c173-176">タスク モジュールのサンプル タブとボット-V3</span><span class="sxs-lookup"><span data-stu-id="4c173-176">Task module sample tabs and bots-V3</span></span> | <span data-ttu-id="4c173-177">タスク モジュールを作成するためのサンプル。</span><span class="sxs-lookup"><span data-stu-id="4c173-177">Samples for creating task modules.</span></span> |[<span data-ttu-id="4c173-178">View</span><span class="sxs-lookup"><span data-stu-id="4c173-178">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[<span data-ttu-id="4c173-179">View</span><span class="sxs-lookup"><span data-stu-id="4c173-179">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a><span data-ttu-id="4c173-180">関連項目</span><span class="sxs-lookup"><span data-stu-id="4c173-180">See also</span></span>

[<span data-ttu-id="4c173-181">タスク モジュールの呼び出しと終了</span><span class="sxs-lookup"><span data-stu-id="4c173-181">Invoke and dismiss task modules</span></span>](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="next-step"></a><span data-ttu-id="4c173-182">次の手順</span><span class="sxs-lookup"><span data-stu-id="4c173-182">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4c173-183">ボットからのタスク モジュールの使用</span><span class="sxs-lookup"><span data-stu-id="4c173-183">Using task modules from bots</span></span>](~/task-modules-and-cards/task-modules/task-modules-bots.md)
