---
title: ボットでタスク モジュールMicrosoft Teamsする
description: ボット フレームワーク カード、アダプティブ カード、ディープ Microsoft Teamsなど、ボットでタスク モジュールを使用する方法。
localization_priority: Normal
ms.topic: how-to
keywords: タスク モジュールのチーム ボット
ms.openlocfilehash: 5d9aa2b651a4c99cee75aada62a4d1176a589d79
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140308"
---
# <a name="use-task-modules-from-bots"></a><span data-ttu-id="f23eb-104">ボットからのタスク モジュールの使用</span><span class="sxs-lookup"><span data-stu-id="f23eb-104">Use task modules from bots</span></span>

<span data-ttu-id="f23eb-105">タスク モジュールは、ヒーロー、サムネイル、Microsoft Teams コネクタであるアダプティブ カードおよびボット フレームワーク カードのボタンを使用して、Office 365ボットから呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="f23eb-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive Cards and Bot Framework cards that is hero, thumbnail, and Office 365 Connector.</span></span> <span data-ttu-id="f23eb-106">タスク モジュールは、多くの場合、複数の会話手順よりも優れたユーザー エクスペリエンスです。</span><span class="sxs-lookup"><span data-stu-id="f23eb-106">Task modules are often a better user experience than multiple conversation steps.</span></span> <span data-ttu-id="f23eb-107">ボットの状態を追跡し、ユーザーがシーケンスを中断またはキャンセルできます。</span><span class="sxs-lookup"><span data-stu-id="f23eb-107">Keep track of bot state and allow the user to interrupt or cancel the sequence.</span></span>

<span data-ttu-id="f23eb-108">タスク モジュールを呼び出す方法は 2 通りあります。</span><span class="sxs-lookup"><span data-stu-id="f23eb-108">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="f23eb-109">新しい種類の呼び出しメッセージ : ボット フレームワーク カードのカード アクションを使用するか、アダプティブ カードのカード アクションを使用して、タスク モジュールが `task/fetch` `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` URL またはアダプティブ カードを使用して、ボットから動的にフェッチされます。</span><span class="sxs-lookup"><span data-stu-id="f23eb-109">A new kind of invoke message `task/fetch`: Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, task module either a URL or an Adaptive Card, is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="f23eb-110">ディープ リンク URL:[](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)タスク モジュールのディープ リンク構文を使用して、Bot Framework カードのカード アクションまたはアダプティブ カードのカード アクションをそれぞれ `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)使用できます。</span><span class="sxs-lookup"><span data-stu-id="f23eb-110">Deep link URLs: Using the [deep link syntax for task modules](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive Cards, respectively.</span></span> <span data-ttu-id="f23eb-111">ディープ リンク URL を使用すると、タスク モジュールの URL またはアダプティブ カード本文は、 を基準にしたサーバーのラウンドトリップを回避することが既に知られています `task/fetch` 。</span><span class="sxs-lookup"><span data-stu-id="f23eb-111">With deep link URLs, the task module URL or Adaptive Card body is already known to avoid a server round-trip relative to `task/fetch`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f23eb-112">それぞれ `url` `fallbackUrl` 、HTTPS 暗号化プロトコルを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f23eb-112">Each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

<span data-ttu-id="f23eb-113">次のセクションでは、 を使用してタスク モジュールを呼び出す方法の詳細について説明します `task/fetch` 。</span><span class="sxs-lookup"><span data-stu-id="f23eb-113">The next section provides details on invoking a task module using `task/fetch`.</span></span>

## <a name="invoke-a-task-module-using-taskfetch"></a><span data-ttu-id="f23eb-114">タスク/フェッチを使用してタスク モジュールを呼び出す</span><span class="sxs-lookup"><span data-stu-id="f23eb-114">Invoke a task module using task/fetch</span></span>

<span data-ttu-id="f23eb-115">カードアクションのオブジェクトが初期化されると、ユーザーがボタンを選択すると、ボットに `value` `invoke` `Action.Submit` `invoke` メッセージが送信されます。</span><span class="sxs-lookup"><span data-stu-id="f23eb-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized and when a user selects the button, an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="f23eb-116">メッセージに対する HTTP 応答には、ラッパー オブジェクトに TaskInfo オブジェクトが埋め込まれているので、Teamsモジュールの表示に `invoke` 使用されます。 [](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="f23eb-116">In the HTTP response to the `invoke` message, there is a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![task/fetch 要求または応答](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="f23eb-118">次の手順では、タスク/フェッチを使用してタスク モジュールを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-118">The following steps provides the invoke task module using task/fetch:</span></span>

1. <span data-ttu-id="f23eb-119">この画像は、カードの購入アクションを含む Bot Framework **ヒーロー カード** `invoke` [を示しています](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)。</span><span class="sxs-lookup"><span data-stu-id="f23eb-119">This image shows a Bot Framework hero card with a **Buy** `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke).</span></span> <span data-ttu-id="f23eb-120">プロパティの値 `type` は、オブジェクトの残りの部分 `task/fetch` `value` が選択できます。</span><span class="sxs-lookup"><span data-stu-id="f23eb-120">The value of the `type` property is `task/fetch` and the rest of the `value` object can be of your choice.</span></span>
1. <span data-ttu-id="f23eb-121">ボットは HTTP `invoke` POST メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-121">The bot receives the `invoke` HTTP POST message.</span></span>
1. <span data-ttu-id="f23eb-122">ボットは応答オブジェクトを作成し、HTTP 200 応答コードを使用して POST 応答の本文に返します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="f23eb-123">応答のスキーマの詳細については [、「task/submit」を参照してください](#the-flexibility-of-tasksubmit)。</span><span class="sxs-lookup"><span data-stu-id="f23eb-123">For more information on schema for responses, see [the discussion on task/submit](#the-flexibility-of-tasksubmit).</span></span> <span data-ttu-id="f23eb-124">次のコードは、ラッパー オブジェクトに埋め込まれた [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) オブジェクトを含む HTTP 応答の本文の例を示しています。</span><span class="sxs-lookup"><span data-stu-id="f23eb-124">The following code provides an example of body of the HTTP response that contains a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) embedded in a wrapper object:</span></span>

    ```json
    {
      "task": {
        "type": "continue",
        "value": {
          "title": "Task module title",
          "height": 500,
          "width": "medium",
          "url": "https://contoso.com/msteams/taskmodules/newcustomer",
          "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
        }
      }
    }
    ```

    <span data-ttu-id="f23eb-125">ボット `task/fetch` のイベントとその応答は、クライアント `microsoftTeams.tasks.startTask()` SDK の関数と似ています。</span><span class="sxs-lookup"><span data-stu-id="f23eb-125">The `task/fetch` event and its response for bots is similar to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>

1. <span data-ttu-id="f23eb-126">Microsoft Teamsタスク モジュールを表示します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-126">Microsoft Teams displays the task module.</span></span>

<span data-ttu-id="f23eb-127">次のセクションでは、タスク モジュールの結果の送信に関する詳細を説明します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-127">The next section provides details on submitting the result of a task module.</span></span>

## <a name="submit-the-result-of-a-task-module"></a><span data-ttu-id="f23eb-128">タスク モジュールの結果を送信する</span><span class="sxs-lookup"><span data-stu-id="f23eb-128">Submit the result of a task module</span></span>

<span data-ttu-id="f23eb-129">ユーザーがタスク モジュールを終了すると、結果をボットに送信し戻すのは、タブの動作と似ています。</span><span class="sxs-lookup"><span data-stu-id="f23eb-129">When the user is finished with the task module, submitting the result back to the bot is similar to the way it works with tabs.</span></span> <span data-ttu-id="f23eb-130">詳細については、タスク [モジュールの結果を送信する例を参照してください](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)。</span><span class="sxs-lookup"><span data-stu-id="f23eb-130">For more information, see [example of submitting the result of a task module](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module).</span></span> <span data-ttu-id="f23eb-131">次のようにいくつかの違いがあります。</span><span class="sxs-lookup"><span data-stu-id="f23eb-131">There are a few differences as follows:</span></span>

* <span data-ttu-id="f23eb-132">HTML または JavaScript : ユーザーが入力した値を検証したら、読みやすさを目的として、以下に示す SDK 関数 `TaskInfo.url` `microsoftTeams.tasks.submitTask()` `submitTask()` を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-132">HTML or JavaScript that is `TaskInfo.url`: Once you have validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function referred to hereafter as `submitTask()` for readability purposes.</span></span> <span data-ttu-id="f23eb-133">タスク モジュールを閉じTeamsパラメーターを指定せずに呼び出しできますが、オブジェクトまたは文字列を自分に `submitTask()` 渡す必要があります `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="f23eb-133">You can call `submitTask()` without any parameters if you want Teams to close the task module, but you must pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="f23eb-134">最初のパラメーターとして渡します `result` 。</span><span class="sxs-lookup"><span data-stu-id="f23eb-134">Pass it as the first parameter, `result`.</span></span> <span data-ttu-id="f23eb-135">Teams呼び `submitHandler` 出す `err` 、、、、に渡した `null` `result` オブジェクトまたは文字列です `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="f23eb-135">Teams invokes `submitHandler`, `err` is `null`, and `result` is the object or string you passed to `submitTask()`.</span></span> <span data-ttu-id="f23eb-136">パラメーターを使用 `submitTask()` して呼び出 `result` す場合は、文字列または文字列の `appId` 配列を渡す必要 `appId` があります。</span><span class="sxs-lookup"><span data-stu-id="f23eb-136">If you call `submitTask()` with a `result` parameter, you must pass an `appId` or an array of `appId` strings.</span></span> <span data-ttu-id="f23eb-137">これにより、Teams送信するアプリがタスク モジュールを呼び出したアプリと同じことを検証できます。</span><span class="sxs-lookup"><span data-stu-id="f23eb-137">This allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="f23eb-138">ボットは、 を含む `task/submit` メッセージを受信 `result` します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-138">Your bot receives a `task/submit` message including `result`.</span></span> <span data-ttu-id="f23eb-139">詳細については、「ペイロードと [メッセージ」 `task/fetch` を `task/submit` 参照してください](#payload-of-taskfetch-and-tasksubmit-messages)。</span><span class="sxs-lookup"><span data-stu-id="f23eb-139">For more information, see [payload of `task/fetch` and `task/submit` messages](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="f23eb-140">アダプティブ カード : ユーザーが入力したアダプティブ カード本文は、ユーザーがボタンを選択すると、メッセージを介してボット `TaskInfo.card` `task/submit` に送信 `Action.Submit` されます。</span><span class="sxs-lookup"><span data-stu-id="f23eb-140">Adaptive Card that is `TaskInfo.card`: The Adaptive Card body as filled in by the user is sent to the bot through a `task/submit` message when the user selects any `Action.Submit` button.</span></span>

<span data-ttu-id="f23eb-141">次のセクションでは、 の柔軟性に関する詳細を示します `task/submit` 。</span><span class="sxs-lookup"><span data-stu-id="f23eb-141">The next section provides details on the flexibility of `task/submit`.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="f23eb-142">タスク/送信の柔軟性</span><span class="sxs-lookup"><span data-stu-id="f23eb-142">The flexibility of task/submit</span></span>

<span data-ttu-id="f23eb-143">ユーザーがボットから呼び出されたタスク モジュールで終了すると、ボットは常にメッセージを受信 `task/submit invoke` します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-143">When the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="f23eb-144">次のようにメッセージに応答する場合、いくつかの `task/submit` オプションがあります。</span><span class="sxs-lookup"><span data-stu-id="f23eb-144">You have several options when responding to the `task/submit` message as follows:</span></span>

| <span data-ttu-id="f23eb-145">HTTP 本文の応答</span><span class="sxs-lookup"><span data-stu-id="f23eb-145">HTTP body response</span></span>                      | <span data-ttu-id="f23eb-146">シナリオ</span><span class="sxs-lookup"><span data-stu-id="f23eb-146">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="f23eb-147">メッセージを無視 `task/submit` しない</span><span class="sxs-lookup"><span data-stu-id="f23eb-147">None ignore the `task/submit` message</span></span> | <span data-ttu-id="f23eb-148">最も単純な応答は応答なしです。</span><span class="sxs-lookup"><span data-stu-id="f23eb-148">The simplest response is no response at all.</span></span> <span data-ttu-id="f23eb-149">ユーザーがタスク モジュールを使い終わったときにボットが応答する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f23eb-149">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="f23eb-150">Teamsポップアップ メッセージ ボックス `value` に値を表示します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-150">Teams displays the value of `value` in a pop-up message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="f23eb-151">アダプティブ カードのシーケンスを、ウィザードまたはマルチステップ エクスペリエンスで一緒にチェーンできます。</span><span class="sxs-lookup"><span data-stu-id="f23eb-151">Allows you to chain sequences of Adaptive Cards together in a wizard or multi-step experience.</span></span> |

> [!NOTE]
> <span data-ttu-id="f23eb-152">アダプティブ カードをシーケンスにチェーン化する方法は、高度なシナリオです。</span><span class="sxs-lookup"><span data-stu-id="f23eb-152">Chaining Adaptive Cards into a sequence is an advanced scenario.</span></span> <span data-ttu-id="f23eb-153">このNode.jsサンプル アプリがサポートしています。</span><span class="sxs-lookup"><span data-stu-id="f23eb-153">The Node.js sample app supports it.</span></span> <span data-ttu-id="f23eb-154">詳細については、「タスク モジュール[のMicrosoft Teams」を参照Node.js。 ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)</span><span class="sxs-lookup"><span data-stu-id="f23eb-154">For more information, see [Microsoft Teams task module Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).</span></span>

<span data-ttu-id="f23eb-155">次のセクションでは、ペイロードとメッセージの詳細 `task/fetch` について説明 `task/submit` します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-155">The next section provides details on payload of `task/fetch` and `task/submit` messages.</span></span>

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="f23eb-156">タスク/フェッチおよびタスク/送信メッセージのペイロード</span><span class="sxs-lookup"><span data-stu-id="f23eb-156">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="f23eb-157">このセクションでは、ボットがボットまたは Bot Framework オブジェクトを受信するときに受け取るスキーマ `task/fetch` `task/submit` を定義 `Activity` します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-157">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="f23eb-158">次の表に、ペイロードとメッセージのプロパティ `task/fetch` を示 `task/submit` します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-158">The following table provides the properties of payload of `task/fetch` and `task/submit` messages:</span></span>

| <span data-ttu-id="f23eb-159">プロパティ</span><span class="sxs-lookup"><span data-stu-id="f23eb-159">Property</span></span> | <span data-ttu-id="f23eb-160">説明</span><span class="sxs-lookup"><span data-stu-id="f23eb-160">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="f23eb-161">は常です `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="f23eb-161">Is always `invoke`.</span></span>           |
| `name`   | <span data-ttu-id="f23eb-162">は、 `task/fetch` または `task/submit` です。</span><span class="sxs-lookup"><span data-stu-id="f23eb-162">Is either `task/fetch` or `task/submit`.</span></span> |
| `value`  | <span data-ttu-id="f23eb-163">開発者定義のペイロードです。</span><span class="sxs-lookup"><span data-stu-id="f23eb-163">Is the developer-defined payload.</span></span> <span data-ttu-id="f23eb-164">オブジェクトの構造は、オブジェクトから送信される構造と `value` Teams。</span><span class="sxs-lookup"><span data-stu-id="f23eb-164">The structure of the `value` object is the same as what is sent from Teams.</span></span> <span data-ttu-id="f23eb-165">ただし、この場合は異なります。</span><span class="sxs-lookup"><span data-stu-id="f23eb-165">In this case, however, it is different.</span></span> <span data-ttu-id="f23eb-166">これは、Bot Framework (つまり) とアダプティブ カードアクションの両方からの動的フェッチのサポートが `task/fetch` `value` `Action.Submit` 必要です `data` 。</span><span class="sxs-lookup"><span data-stu-id="f23eb-166">It requires support for dynamic fetch that is `task/fetch` from both Bot Framework, which is `value` and Adaptive Card `Action.Submit` actions, which is `data`.</span></span> <span data-ttu-id="f23eb-167">ボットに含まれているTeamsに加えて、ボットにメッセージを伝達 `context` する方法が `value` 必要です `data` 。</span><span class="sxs-lookup"><span data-stu-id="f23eb-167">A way to communicate Teams `context` to the bot is required in addition to what is included in `value` or `data`.</span></span><br/><br/><span data-ttu-id="f23eb-168">'value' と 'data' を親オブジェクトに結合します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-168">Combine 'value' and 'data' into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

<span data-ttu-id="f23eb-169">次のセクションでは、メッセージの受信と応答、およびメッセージの呼び出しの例を示 `task/fetch` `task/submit` Node.js。</span><span class="sxs-lookup"><span data-stu-id="f23eb-169">The next section provides an example of receiving and responding to `task/fetch` and `task/submit` invoke messages in Node.js.</span></span>

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a><span data-ttu-id="f23eb-170">タスク/フェッチとタスク/サブミットの呼び出しメッセージの例 (Node.js C)#</span><span class="sxs-lookup"><span data-stu-id="f23eb-170">Example of task/fetch and task/submit invoke messages in Node.js and C#</span></span>

# <a name="nodejs"></a>[<span data-ttu-id="f23eb-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="f23eb-171">Node.js</span></span>](#tab/nodejs)

```typescript
handleTeamsTaskModuleFetch(context, taskModuleRequest) {
    // Called when the user selects an options from the displayed HeroCard or
    // AdaptiveCard.  The result is the action to perform.

    const cardTaskFetchValue = taskModuleRequest.data.data;
    var taskInfo = {}; // TaskModuleTaskInfo

    if (cardTaskFetchValue === TaskModuleIds.YouTube) {
        // Display the YouTube.html page
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.YouTube + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
    } else if (cardTaskFetchValue === TaskModuleIds.CustomForm) {
        // Display the CustomForm.html page, and post the form data back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.CustomForm + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
    } else if (cardTaskFetchValue === TaskModuleIds.AdaptiveCard) {
        // Display an AdaptiveCard to prompt user for text, and post it back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.card = this.createAdaptiveCardAttachment();
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
    }

    return TaskModuleResponseFactory.toTaskModuleResponse(taskInfo);
}

async handleTeamsTaskModuleSubmit(context, taskModuleRequest) {
    // Called when data is being returned from the selected option (see `handleTeamsTaskModuleFetch').

    // Echo the users input back.  In a production bot, this is where you'd add behavior in
    // response to the input.
    await context.sendActivity(MessageFactory.text('handleTeamsTaskModuleSubmit: ' + JSON.stringify(taskModuleRequest.data)));

    // Return TaskModuleResponse
    return {
        // TaskModuleMessageResponse
        task: {
            type: 'message',
            value: 'Thanks!'
        }
    };
}

setTaskInfo(taskInfo, uiSettings) {
    taskInfo.height = uiSettings.height;
    taskInfo.width = uiSettings.width;
    taskInfo.title = uiSettings.title;
}
```

# <a name="c"></a>[<span data-ttu-id="f23eb-172">C#</span><span class="sxs-lookup"><span data-stu-id="f23eb-172">C#</span></span>](#tab/csharp)

```csharp
protected override Task<TaskModuleResponse> OnTeamsTaskModuleFetchAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var asJobject = JObject.FromObject(taskModuleRequest.Data);
    var value = asJobject.ToObject<CardTaskFetchValue<string>>()?.Data;

    var taskInfo = new TaskModuleTaskInfo();
    switch (value)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = CreateAdaptiveCardAttachment();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }

    return Task.FromResult(taskInfo.ToTaskModuleResponse());
}

protected override async Task<TaskModuleResponse> OnTeamsTaskModuleSubmitAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var reply = MessageFactory.Text("OnTeamsTaskModuleSubmitAsync Value: " + JsonConvert.SerializeObject(taskModuleRequest));
    await turnContext.SendActivityAsync(reply, cancellationToken);

    return TaskModuleResponseFactory.CreateResponse("Thanks!");
}

private static void SetTaskInfo(TaskModuleTaskInfo taskInfo, UISettings uIConstants)
{
    taskInfo.Height = uIConstants.Height;
    taskInfo.Width = uIConstants.Width;
    taskInfo.Title = uIConstants.Title.ToString();
}
```

---

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="f23eb-173">Bot Framework カードアクションとアダプティブ カード アクション.Submit アクション</span><span class="sxs-lookup"><span data-stu-id="f23eb-173">Bot Framework card actions vs. Adaptive Card Action.Submit actions</span></span>

<span data-ttu-id="f23eb-174">Bot Framework カードアクションのスキーマはアダプティブ カード アクションとは異なります。また、タスク モジュールを呼び出す方法も `Action.Submit` 異なります。</span><span class="sxs-lookup"><span data-stu-id="f23eb-174">The schema for Bot Framework card actions is different from Adaptive Card `Action.Submit` actions and the way to invoke task modules is also different.</span></span> <span data-ttu-id="f23eb-175">オブジェクト `data` には `Action.Submit` オブジェクトが含まれているので、カード内の他の `msteams` プロパティに干渉しません。</span><span class="sxs-lookup"><span data-stu-id="f23eb-175">The `data` object in `Action.Submit` contains an `msteams` object so it does not interfere with other properties in the card.</span></span> <span data-ttu-id="f23eb-176">次の表に、各カード アクションの例を示します。</span><span class="sxs-lookup"><span data-stu-id="f23eb-176">The following table shows an example of each card action:</span></span>

| <span data-ttu-id="f23eb-177">Bot Framework カードアクション</span><span class="sxs-lookup"><span data-stu-id="f23eb-177">Bot Framework card action</span></span>                              | <span data-ttu-id="f23eb-178">アダプティブ カード アクション.Submit アクション</span><span class="sxs-lookup"><span data-stu-id="f23eb-178">Adaptive Card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a><span data-ttu-id="f23eb-179">コード サンプル</span><span class="sxs-lookup"><span data-stu-id="f23eb-179">Code sample</span></span>

|<span data-ttu-id="f23eb-180">サンプルの名前</span><span class="sxs-lookup"><span data-stu-id="f23eb-180">Sample name</span></span> | <span data-ttu-id="f23eb-181">説明</span><span class="sxs-lookup"><span data-stu-id="f23eb-181">Description</span></span> | <span data-ttu-id="f23eb-182">.NET</span><span class="sxs-lookup"><span data-stu-id="f23eb-182">.NET</span></span> | <span data-ttu-id="f23eb-183">Node.js</span><span class="sxs-lookup"><span data-stu-id="f23eb-183">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="f23eb-184">タスク モジュールのサンプル ボット-V4</span><span class="sxs-lookup"><span data-stu-id="f23eb-184">Task module sample bots-V4</span></span> | <span data-ttu-id="f23eb-185">タスク モジュールを作成するためのサンプル。</span><span class="sxs-lookup"><span data-stu-id="f23eb-185">Samples for creating task modules.</span></span> |[<span data-ttu-id="f23eb-186">View</span><span class="sxs-lookup"><span data-stu-id="f23eb-186">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[<span data-ttu-id="f23eb-187">View</span><span class="sxs-lookup"><span data-stu-id="f23eb-187">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a><span data-ttu-id="f23eb-188">関連項目</span><span class="sxs-lookup"><span data-stu-id="f23eb-188">See also</span></span>

* [<span data-ttu-id="f23eb-189">Microsoft Teamsタスク モジュールのサンプル コードをNode.js</span><span class="sxs-lookup"><span data-stu-id="f23eb-189">Microsoft Teams task module sample code in Node.js</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [<span data-ttu-id="f23eb-190">ボット フレームワークのサンプル</span><span class="sxs-lookup"><span data-stu-id="f23eb-190">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
