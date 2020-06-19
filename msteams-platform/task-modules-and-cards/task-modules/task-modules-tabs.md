---
title: Microsoft Teams のタブでタスクモジュールを使用する
description: Microsoft Teams クライアント SDK を使用して Teams タブからタスクモジュールを呼び出す方法について説明します。
keywords: タスクモジュールチームタブクライアント sdk
ms.openlocfilehash: e10958195713f338a9b5e0a0672d8b6a29da9264
ms.sourcegitcommit: 2a84a3c8b10771e37ce51bf603a967633947a3e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2020
ms.locfileid: "44801199"
---
# <a name="using-task-modules-in-tabs"></a><span data-ttu-id="a3cde-104">タブでタスクモジュールを使用する</span><span class="sxs-lookup"><span data-stu-id="a3cde-104">Using task modules in tabs</span></span>

<span data-ttu-id="a3cde-105">タスクモジュールをタブに追加すると、データ入力を必要とするすべてのワークフローについて、ユーザーの操作が大幅に簡素化されます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-105">Adding a task module to your tab can greatly simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="a3cde-106">タスクモジュールを使用すると、チーム対応のポップアップで入力を収集できます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-106">Task modules allow you to gather their input in a Teams-aware popup.</span></span> <span data-ttu-id="a3cde-107">プランナーカードを編集することをよく例を示します。タスクモジュールを使用して、同様の操作を作成できます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-107">A good example of this is editing Planner cards; you can use task modules to create a similar experience.</span></span>

<span data-ttu-id="a3cde-108">タスクモジュール機能をサポートするために、 [Microsoft Teams クライアント SDK](/javascript/api/overview/msteams-client)に2つの新しい関数が追加されました。</span><span class="sxs-lookup"><span data-stu-id="a3cde-108">To support the task module feature, two new functions were added to the [Microsoft Teams client SDK](/javascript/api/overview/msteams-client):</span></span>

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

<span data-ttu-id="a3cde-109">それぞれがどのように機能するかを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="a3cde-109">Let's see how each of them work.</span></span>

## <a name="invoking-a-task-module-from-a-tab"></a><span data-ttu-id="a3cde-110">タブからタスクモジュールを呼び出す</span><span class="sxs-lookup"><span data-stu-id="a3cde-110">Invoking a task module from a tab</span></span>

<span data-ttu-id="a3cde-111">タスクモジュールをタブから呼び出し `microsoftTeams.tasks.startTask()` て、 [taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)とオプションの `submitHandler` コールバック関数を渡す方法。</span><span class="sxs-lookup"><span data-stu-id="a3cde-111">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="a3cde-112">前述したように、次の2つのケースを考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a3cde-112">As described earlier, there are two cases to consider:</span></span>

1. <span data-ttu-id="a3cde-113">の値 `TaskInfo.url` は、URL に設定されます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-113">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="a3cde-114">タスクモジュールウィンドウが表示され、 `TaskModule.url` そのウィンドウ内に読み込まれ `<iframe>` ます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-114">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="a3cde-115">そのページの JavaScript がを呼び出す必要があり `microsoftTeams.initialize()` ます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-115">JavaScript on that page should call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="a3cde-116">ページ上に関数があり、呼び出し時にエラーが発生した場合は、以下に示すように、エラーを `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` 示すエラー文字列に[below](#task-module-invocation-errors)set を指定して呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-116">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the error as described [below](#task-module-invocation-errors).</span></span>
1. <span data-ttu-id="a3cde-117">の値 `taskInfo.card` は、[アダプティブカードの JSON](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)です。</span><span class="sxs-lookup"><span data-stu-id="a3cde-117">The value of `taskInfo.card` is the [JSON for an Adaptive card](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="a3cde-118">この場合、 `submitHandler` ユーザーがアダプティブカード上でボタンを閉じたり押したりしたときに呼び出す JavaScript 関数は存在しません。ユーザーが入力した内容を受信するには、結果を bot に渡す以外に方法はありません。</span><span class="sxs-lookup"><span data-stu-id="a3cde-118">In this case there's obviously not any JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive card; the only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="a3cde-119">タブからアダプティブカードタスクモジュールを使用するには、アプリがユーザーから情報を取得する bot を含んでいる必要があります。</span><span class="sxs-lookup"><span data-stu-id="a3cde-119">To use an Adaptive card task module from a tab your app must include a bot to get any information back from the user.</span></span> <span data-ttu-id="a3cde-120">これについては、以下で説明します。</span><span class="sxs-lookup"><span data-stu-id="a3cde-120">This is explained below.</span></span>

## <a name="example-invoking-a-task-module"></a><span data-ttu-id="a3cde-121">例: タスクモジュールを呼び出す</span><span class="sxs-lookup"><span data-stu-id="a3cde-121">Example: Invoking a task module</span></span>

<span data-ttu-id="a3cde-122">次のコードは、[タスクモジュールサンプル](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples)から適用されます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-122">The code below is adapted from [the task module sample](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples).</span></span> <span data-ttu-id="a3cde-123">タスクモジュールは以下のようになります。</span><span class="sxs-lookup"><span data-stu-id="a3cde-123">Here's what the task module looks like:</span></span>

![タスクモジュール-ユーザー設定フォーム](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="a3cde-125">は `submitHandler` 非常に単純で、またはコンソールの値をエコーするだけです `err` `result` 。</span><span class="sxs-lookup"><span data-stu-id="a3cde-125">The `submitHandler` is very simple; it just echoes the value of `err` or `result` to the console:</span></span>

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

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="a3cde-126">タスクモジュールの結果を提出する</span><span class="sxs-lookup"><span data-stu-id="a3cde-126">Submitting the result of a task module</span></span>

<span data-ttu-id="a3cde-127">`submitHandler`関数は、で使用され `TaskInfo.url` ます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-127">The `submitHandler` function is used with `TaskInfo.url`.</span></span> <span data-ttu-id="a3cde-128">`submitHandler`関数は web ページに存在し `TaskInfo.url` ます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-128">The `submitHandler` function resides in the `TaskInfo.url` web page.</span></span> <span data-ttu-id="a3cde-129">タスクモジュールの呼び出し時にエラーが発生した場合は、 `submitHandler` `err` [エラーが発生した](#task-module-invocation-errors)ことを示す文字列を使用して、関数が直ちに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-129">If there's an error when invoking the task module your `submitHandler` function will be immediately invoked with an `err` string indicating which [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="a3cde-130">この `submitHandler` 関数は、 `err` ユーザーがタスクモジュールの右上にある X を押したときに、文字列を使用しても呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-130">The `submitHandler` function is also called with an `err` string when the user presses the X at the upper right of task module.</span></span>

<span data-ttu-id="a3cde-131">呼び出しエラーがなく、ユーザーが X を押してそれを破棄しなかった場合、ユーザーは終了時にボタンを押したことになります。</span><span class="sxs-lookup"><span data-stu-id="a3cde-131">If there's no invocation error and the user doesn't press X to dismiss it, the user presses a button when finished.</span></span> <span data-ttu-id="a3cde-132">タスクモジュールの URL であるか、アダプティブカードであるかによって、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="a3cde-132">Depending on whether it's a URL or an Adaptive card in the task module, here's what happens:</span></span>

### <a name="htmljavascript-taskinfourl"></a><span data-ttu-id="a3cde-133">HTML/JavaScript ( `TaskInfo.url` )</span><span class="sxs-lookup"><span data-stu-id="a3cde-133">HTML/JavaScript (`TaskInfo.url`)</span></span>

<span data-ttu-id="a3cde-134">ユーザーが入力したことを確認したら、 `microsoftTeams.tasks.submitTask()` SDK 関数を呼び出し `submitTask()` ます (読みやすさを目的として、以降を参照)。</span><span class="sxs-lookup"><span data-stu-id="a3cde-134">Once you've validated what the user has entered you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="a3cde-135">`submitTask()`タスクモジュールを閉じるだけの場合は、パラメーターを指定せずに呼び出すことができますが、ほとんどの場合、オブジェクトまたは文字列をに渡すことが必要になり `submitHandler` ます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-135">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="a3cde-136">結果を最初のパラメーターとして渡します。</span><span class="sxs-lookup"><span data-stu-id="a3cde-136">Pass your result as the first parameter.</span></span> <span data-ttu-id="a3cde-137">Teams は、を呼び出し、 `submitHandler` `err` 渡され `null` `result` たオブジェクト/文字列になり `submitTask()` ます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-137">Teams will invoke `submitHandler` where `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="a3cde-138">パラメーターを指定して呼び出しを行う場合 `submitTask()` `result` は、または文字列の配列を渡す**必要があり** `appId` `appId` ます。これにより、チームは、結果を送信しているアプリがタスクモジュールを呼び出したものと同じであることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-138">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="a3cde-139">アダプティブカード ( `TaskInfo.card` )</span><span class="sxs-lookup"><span data-stu-id="a3cde-139">Adaptive card (`TaskInfo.card`)</span></span>

<span data-ttu-id="a3cde-140">でタスクモジュールを呼び出した場合 `submitHandler` 、ユーザーがボタンを押すと、 `Action.Submit` カード内の値はの値として返され `result` ます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-140">If you invoked the task module with a `submitHandler`, when the user presses an `Action.Submit` button the values in the card will be returned as the value of `result`.</span></span> <span data-ttu-id="a3cde-141">ユーザーが Esc ボタンを押すか、X を押すと、 `err` 代わりにが返されます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-141">If the user presses the Esc button or presses the X, `err` will be returned instead.</span></span> <span data-ttu-id="a3cde-142">または、アプリにタブに加えて bot が含まれている場合は、その `appId` bot のをオブジェクト内のの値として簡単に含めることができ `completionBotId` `TaskInfo` ます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-142">Alternatively, if your app contains a bot in addition to a tab you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="a3cde-143">ユーザーがボタンを押したときに、ユーザーが入力したアダプティブカードの本文が、メッセージによって bot に送信され `task/submit invoke` `Action.Submit` ます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-143">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit invoke` message when the user presses an `Action.Submit` button.</span></span> <span data-ttu-id="a3cde-144">受け取るオブジェクトのスキーマは、[タスク/フェッチおよびタスク/送信メッセージのために受け取るスキーマ](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)によく似ています。唯一の違いは、JSON オブジェクトのスキーマは、インテリカードを[bot と組み合わせて使用する場合](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)と同様に、アダプティブカードオブジェクトを*格納*しているオブジェクトではなく、アダプティブカードオブジェクトであるということです。</span><span class="sxs-lookup"><span data-stu-id="a3cde-144">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); the only difference is that the schema of the JSON object is an Adaptive card object as opposed to an object *containing* an Adaptive card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

## <a name="example-submitting-the-result-of-a-task-module"></a><span data-ttu-id="a3cde-145">例: タスクモジュールの結果を提出する</span><span class="sxs-lookup"><span data-stu-id="a3cde-145">Example: submitting the result of a task module</span></span>

<span data-ttu-id="a3cde-146">前述の[タスクモジュールのフォーム](#example-invoking-a-task-module)を HTML フォームで取り消します。</span><span class="sxs-lookup"><span data-stu-id="a3cde-146">Recall the [form in the task module above](#example-invoking-a-task-module) with an HTML form.</span></span> <span data-ttu-id="a3cde-147">フォームが定義されている場所は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a3cde-147">Here's where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="a3cde-148">このフォームには5つのフィールドがありますが、この例では、、、およびの3つのフィールドの値のみを対象としています。 `name` `email` `favoriteBook`</span><span class="sxs-lookup"><span data-stu-id="a3cde-148">There are five fields on this form but we're only interested in the values of three of them for this example: `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="a3cde-149">を呼び出す関数を次に示し `validateForm()` `submitTask()` ます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-149">Here's the `validateForm()` function that calls `submitTask()`:</span></span>

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

## <a name="task-module-invocation-errors"></a><span data-ttu-id="a3cde-150">タスク モジュール呼び出しのエラー</span><span class="sxs-lookup"><span data-stu-id="a3cde-150">Task module invocation errors</span></span>

<span data-ttu-id="a3cde-151">で受信可能な値は次のとおりです `err` `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="a3cde-151">Here are the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="a3cde-152">問題</span><span class="sxs-lookup"><span data-stu-id="a3cde-152">Problem</span></span> | <span data-ttu-id="a3cde-153">エラーメッセージ (の値 `err` )</span><span class="sxs-lookup"><span data-stu-id="a3cde-153">Error message (value of `err`)</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="a3cde-154">との両方の値 `TaskInfo.url` `TaskInfo.card` が指定されました。</span><span class="sxs-lookup"><span data-stu-id="a3cde-154">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="a3cde-155">カードと url の両方の値が指定されています。</span><span class="sxs-lookup"><span data-stu-id="a3cde-155">"Values for both card and url were specified.</span></span> <span data-ttu-id="a3cde-156">どちらか一方のみが許可されます。</span><span class="sxs-lookup"><span data-stu-id="a3cde-156">One or the other, but not both, are allowed."</span></span> |
| <span data-ttu-id="a3cde-157">`TaskInfo.url`または `TaskInfo.card` 指定されません。</span><span class="sxs-lookup"><span data-stu-id="a3cde-157">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="a3cde-158">"カードまたは url のいずれかに値を指定する必要があります。"</span><span class="sxs-lookup"><span data-stu-id="a3cde-158">"You must specify a value for either card or url."</span></span> |
| <span data-ttu-id="a3cde-159">無効 `appId` です。</span><span class="sxs-lookup"><span data-stu-id="a3cde-159">Invalid `appId`.</span></span> | <span data-ttu-id="a3cde-160">"無効な appId"。</span><span class="sxs-lookup"><span data-stu-id="a3cde-160">"Invalid appId."</span></span> |
| <span data-ttu-id="a3cde-161">ユーザーが X ボタンを押して、それを閉じる。</span><span class="sxs-lookup"><span data-stu-id="a3cde-161">User pressed X button, closing it.</span></span> | <span data-ttu-id="a3cde-162">"ユーザーがタスクモジュールを取り消しまたは終了しました。"</span><span class="sxs-lookup"><span data-stu-id="a3cde-162">"User cancelled/closed the task module."</span></span> |
