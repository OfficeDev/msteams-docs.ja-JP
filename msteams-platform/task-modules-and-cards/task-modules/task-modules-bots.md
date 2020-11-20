---
title: Microsoft Teams の bot のタスクモジュールを使用する
description: Bot フレームワークカード、アダプティブカード、ディープリンクなど、Microsoft Teams の bot でタスクモジュールを使用する方法について説明します。
keywords: タスクモジュール teams の bot
ms.openlocfilehash: 1400fec0ef86448f8632018c7675999b6b1881a0
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346722"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="0e355-104">Microsoft Teams のボットからのタスクモジュールの使用</span><span class="sxs-lookup"><span data-stu-id="0e355-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="0e355-105">タスクモジュールは、アダプティブカードおよび Bot フレームワークカード (英雄、サムネイル、および Office 365 Connector) のボタンを使用して、Microsoft Teams の bot から呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="0e355-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="0e355-106">タスクモジュールは、多くの場合、開発者が bot の状態を追跡し、ユーザーがシーケンスを中断または取り消しられるようにする必要がある、複数の会話手順よりも優れたユーザー環境を提供します。</span><span class="sxs-lookup"><span data-stu-id="0e355-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="0e355-107">タスクモジュールを呼び出すには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="0e355-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="0e355-108">**新しい種類の invoke メッセージ `task/fetch` 。**</span><span class="sxs-lookup"><span data-stu-id="0e355-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="0e355-109">`invoke`Bot フレームワークカードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#invoke)、または `Action.Submit` アダプティブカードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)を使用すると、 `task/fetch` タスクモジュール (URL またはアダプティブカード) が bot から動的に取り出されます。</span><span class="sxs-lookup"><span data-stu-id="0e355-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="0e355-110">**ディープリンク Url。**</span><span class="sxs-lookup"><span data-stu-id="0e355-110">**Deep link URLs.**</span></span> <span data-ttu-id="0e355-111">[タスクモジュールのディープリンク構文](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)を使用すると、 `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl)ボットフレームワークカード、または `Action.OpenUrl` 適応カードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)をそれぞれ使用できます。</span><span class="sxs-lookup"><span data-stu-id="0e355-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="0e355-112">深いリンク Url を使用すると、タスクモジュールの URL またはアダプティブカードの本文は明らかによく知られており、に対するサーバーのラウンドトリップを回避 `task/fetch` します。</span><span class="sxs-lookup"><span data-stu-id="0e355-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0e355-113">セキュリティで保護された通信を確保するために、それぞれに `url` `fallbackUrl` HTTPS 暗号化プロトコルを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0e355-113">To ensure secure communications, each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

## <a name="invoking-a-task-module-via-taskfetch"></a><span data-ttu-id="0e355-114">Task/fetch を使用してタスクモジュールを呼び出す</span><span class="sxs-lookup"><span data-stu-id="0e355-114">Invoking a task module via task/fetch</span></span>

<span data-ttu-id="0e355-115">`value`カードアクションのオブジェクトの場合、 `invoke` または `Action.Submit` 適切な方法で初期化される場合 (以下を参照)、ユーザーがボタンを押すと、 `invoke` メッセージが bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="0e355-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="0e355-116">メッセージに対する HTTP 応答では `invoke` 、タスクモジュールを表示するために Teams で使用される [taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) がラッパーオブジェクトに埋め込まれています。</span><span class="sxs-lookup"><span data-stu-id="0e355-116">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![タスク/フェッチ要求/応答](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="0e355-118">各手順について、さらに詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="0e355-118">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="0e355-119">この例では、"Buy" カードアクションを含む Bot フレームワークの英雄カードを示し `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke)ます。</span><span class="sxs-lookup"><span data-stu-id="0e355-119">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="0e355-120">プロパティの値 `type` は、 `task/fetch` オブジェクトの残りの部分を `value` 任意のものにすることができます。</span><span class="sxs-lookup"><span data-stu-id="0e355-120">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
2. <span data-ttu-id="0e355-121">Bot が `invoke` HTTP POST メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="0e355-121">The bot receives the `invoke` HTTP POST message.</span></span>
3. <span data-ttu-id="0e355-122">Bot は応答オブジェクトを作成し、それを HTTP 200 応答コードを使用して POST 応答の本文に返します。</span><span class="sxs-lookup"><span data-stu-id="0e355-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="0e355-123">応答のスキーマについては、次の「 [タスク/送信に](#the-flexibility-of-tasksubmit)ついて」を参照してください。ここで覚えておくべき重要な点は、HTTP 応答の本文に、次のように、ラッパーオブジェクトに埋め込まれた [taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) が含まれるということです。</span><span class="sxs-lookup"><span data-stu-id="0e355-123">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, e.g.:</span></span>

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

    <span data-ttu-id="0e355-124">`task/fetch`Bot に対するイベントとその応答は、概念的には `microsoftTeams.tasks.startTask()` クライアント SDK の関数に似ています。</span><span class="sxs-lookup"><span data-stu-id="0e355-124">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
4. <span data-ttu-id="0e355-125">Microsoft Teams では、タスクモジュールが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0e355-125">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="0e355-126">タスクモジュールの結果を提出する</span><span class="sxs-lookup"><span data-stu-id="0e355-126">Submitting the result of a task module</span></span>

<span data-ttu-id="0e355-127">ユーザーがタスクモジュールで作業を終了すると、検索結果は [タブを使用](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)した場合と同じようになりますが、いくつかの違いがあるので、ここでも説明します。</span><span class="sxs-lookup"><span data-stu-id="0e355-127">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="0e355-128">**HTML/JavaScript ( `TaskInfo.url` )**。</span><span class="sxs-lookup"><span data-stu-id="0e355-128">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="0e355-129">ユーザーが入力したことを確認したら、 `microsoftTeams.tasks.submitTask()` SDK 関数を呼び出し `submitTask()` ます (読みやすさを目的として、以降を参照)。</span><span class="sxs-lookup"><span data-stu-id="0e355-129">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="0e355-130">`submitTask()`タスクモジュールを閉じるだけの場合は、パラメーターを指定せずに呼び出すことができますが、ほとんどの場合、オブジェクトまたは文字列をに渡すことが必要になり `submitHandler` ます。</span><span class="sxs-lookup"><span data-stu-id="0e355-130">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="0e355-131">単にこれを最初のパラメーターとして渡し `result` ます。</span><span class="sxs-lookup"><span data-stu-id="0e355-131">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="0e355-132">Teams が呼び出す `submitHandler` : はになり、 `err` 渡され `null` `result` たオブジェクト/文字列になり `submitTask()` ます。</span><span class="sxs-lookup"><span data-stu-id="0e355-132">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="0e355-133">パラメーターを指定して呼び出しを行う場合 `submitTask()` `result` は、または文字列の配列を渡す **必要があり** `appId` `appId` ます。これにより、チームは、結果を送信しているアプリがタスクモジュールを呼び出したものと同じであることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="0e355-133">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="0e355-134">Bot は、次に `task/submit` 示すようなメッセージを受け取り `result` ます。 [below](#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="0e355-134">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="0e355-135">**アダプティブカード ( `TaskInfo.card` )**。</span><span class="sxs-lookup"><span data-stu-id="0e355-135">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="0e355-136">ユーザーが任意のボタンを押したときに、ユーザーが入力したアダプティブカードの本文が、メッセージによって bot に送信され `task/submit` `Action.Submit` ます。</span><span class="sxs-lookup"><span data-stu-id="0e355-136">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="0e355-137">タスク/提出の柔軟性</span><span class="sxs-lookup"><span data-stu-id="0e355-137">The flexibility of task/submit</span></span>

<span data-ttu-id="0e355-138">前のセクションでは、ユーザーが bot から呼び出されたタスクモジュールで終了すると、bot は常にメッセージを受信することを学びました `task/submit invoke` 。</span><span class="sxs-lookup"><span data-stu-id="0e355-138">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="0e355-139">開発者は、メッセージに *応答* するときにいくつかのオプションを使用でき `task/submit` ます。</span><span class="sxs-lookup"><span data-stu-id="0e355-139">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="0e355-140">HTTP 本文の応答</span><span class="sxs-lookup"><span data-stu-id="0e355-140">HTTP Body Response</span></span>                      | <span data-ttu-id="0e355-141">シナリオ</span><span class="sxs-lookup"><span data-stu-id="0e355-141">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="0e355-142">なし (メッセージを無視します `task/submit` )</span><span class="sxs-lookup"><span data-stu-id="0e355-142">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="0e355-143">最も単純な応答は、まったく応答がありません。</span><span class="sxs-lookup"><span data-stu-id="0e355-143">The simplest response is no response at all.</span></span> <span data-ttu-id="0e355-144">ユーザーがタスクモジュールで作業を終了すると、bot は応答する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="0e355-144">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="0e355-145">の値は、Teams によって `value` ポップアップメッセージボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="0e355-145">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="0e355-146">1つのウィザード/複数ステップの画面で、アダプティブカードのシーケンスを "チェーン" することができます。</span><span class="sxs-lookup"><span data-stu-id="0e355-146">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="0e355-147">_アダプティブカードをシーケンスにチェーンすることは高度なシナリオで、ここでは文書化されていません。Node.js サンプルアプリはこれをサポートしていますが、その機能が [README.md ファイル](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)に記載されています。_</span><span class="sxs-lookup"><span data-stu-id="0e355-147">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="0e355-148">タスク/フェッチおよびタスク/送信メッセージのペイロード</span><span class="sxs-lookup"><span data-stu-id="0e355-148">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="0e355-149">このセクションでは、bot が、または bot フレームワークオブジェクトを受け取ったときに、bot が受け取る内容のスキーマを定義 `task/fetch` `task/submit` `Activity` します。</span><span class="sxs-lookup"><span data-stu-id="0e355-149">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="0e355-150">重要な最上位レベルは下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="0e355-150">The important top-level appear below:</span></span>

| <span data-ttu-id="0e355-151">プロパティ</span><span class="sxs-lookup"><span data-stu-id="0e355-151">Property</span></span> | <span data-ttu-id="0e355-152">説明</span><span class="sxs-lookup"><span data-stu-id="0e355-152">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="0e355-153">は常に `invoke`</span><span class="sxs-lookup"><span data-stu-id="0e355-153">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="0e355-154">`task/fetch`あるいは`task/submit`</span><span class="sxs-lookup"><span data-stu-id="0e355-154">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="0e355-155">開発者が定義したペイロード。</span><span class="sxs-lookup"><span data-stu-id="0e355-155">The developer-defined payload.</span></span> <span data-ttu-id="0e355-156">通常、オブジェクトの構造は `value` Teams から送信されたものを反映します。</span><span class="sxs-lookup"><span data-stu-id="0e355-156">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="0e355-157">ただし、この場合は、 `task/fetch` Bot フレームワーク () とアダプティブカードアクション () の両方から動的な fetch () をサポートし、 `value` `Action.Submit` `data` `context` に含まれていたものに加えて Teams を bot に伝達する方法が必要になり `value` / `data` ます。</span><span class="sxs-lookup"><span data-stu-id="0e355-157">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="0e355-158">これを行うには、2つを親オブジェクトに結合します。</span><span class="sxs-lookup"><span data-stu-id="0e355-158">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="0e355-159">例: タスク/フェッチおよびタスク/送信呼び出しメッセージの受信と応答 Node.js</span><span class="sxs-lookup"><span data-stu-id="0e355-159">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

> [!NOTE]
> <span data-ttu-id="0e355-160">次に示すサンプルコードは、この機能の Technical Preview と最終リリースの間で変更されました。要求のスキーマは、 `task/fetch` [前のセクションで説明](#payload-of-taskfetch-and-tasksubmit-messages)した内容に従って変更されました。</span><span class="sxs-lookup"><span data-stu-id="0e355-160">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="0e355-161">つまり、ドキュメントは修正されましたが、実装はできませんでした。</span><span class="sxs-lookup"><span data-stu-id="0e355-161">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="0e355-162">変更点については、次のコメントを参照してください `// for Technical Preview [...]` 。</span><span class="sxs-lookup"><span data-stu-id="0e355-162">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

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

*See also*, [Microsoft Teams task module sample code — nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) and  [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
```
## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="0e355-163">例: タスク/フェッチおよびタスク/送信呼び出しメッセージを受信して応答する-C#</span><span class="sxs-lookup"><span data-stu-id="0e355-163">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="0e355-164">C# bot では、メッセージ `invoke` はメッセージを処理するコントローラーによって処理され `HttpResponseMessage()` `Activity` ます。</span><span class="sxs-lookup"><span data-stu-id="0e355-164">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="0e355-165">`task/fetch`との `task/submit` 要求と応答は JSON です。</span><span class="sxs-lookup"><span data-stu-id="0e355-165">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="0e355-166">C# では、Node.js のように raw JSON を処理するのは便利ではありません。したがって、JSON とのシリアル化を処理するには、ラッパークラスが必要です。</span><span class="sxs-lookup"><span data-stu-id="0e355-166">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="0e355-167">このことは、Microsoft Teams の [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) で直接サポートされていませんが、これらの簡単なラッパークラスが [C# サンプルアプリ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)でどのように表示されるかの例を確認できます。</span><span class="sxs-lookup"><span data-stu-id="0e355-167">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="0e355-168">以下は、 `task/fetch` `task/submit` これらのラッパークラス (,) を使用して、次のようなコードを処理およびメッセージを処理するための C# のコード例です `TaskInfo` `TaskEnvelope` 。 excerpted [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)のコードは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="0e355-168">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

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
```
## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---python"></a><span data-ttu-id="0e355-169">例: タスク/フェッチおよびタスク/送信呼び出しメッセージを受信して応答する-Python</span><span class="sxs-lookup"><span data-stu-id="0e355-169">Example: Receiving and responding to task/fetch and task/submit invoke messages - Python</span></span>
```
async def on_teams_task_module_fetch(
        self, turn_context: TurnContext, task_module_request: TaskModuleRequest
    ) -> TaskModuleResponse:
        """
        Called when the user selects an options from the displayed HeroCard or
        AdaptiveCard.  The result is the action to perform.
        """

        card_task_fetch_value = task_module_request.data["data"]

        task_info = TaskModuleTaskInfo()
        if card_task_fetch_value == TaskModuleIds.YOUTUBE:
            # Display the YouTube.html page
            task_info.url = task_info.fallback_url = (
                self.__base_url + "/" + TaskModuleIds.YOUTUBE + ".html"
            )
            TeamsTaskModuleBot.__set_task_info(task_info, TaskModuleUIConstants.YOUTUBE)
        elif card_task_fetch_value == TaskModuleIds.CUSTOM_FORM:
            # Display the CustomForm.html page, and post the form data back via
            # on_teams_task_module_submit.
            task_info.url = task_info.fallback_url = (
                self.__base_url + "/" + TaskModuleIds.CUSTOM_FORM + ".html"
            )
            TeamsTaskModuleBot.__set_task_info(
                task_info, TaskModuleUIConstants.CUSTOM_FORM
            )
        elif card_task_fetch_value == TaskModuleIds.ADAPTIVE_CARD:
            # Display an AdaptiveCard to prompt user for text, and post it back via
            # on_teams_task_module_submit.
            task_info.card = TeamsTaskModuleBot.__create_adaptive_card_attachment()
            TeamsTaskModuleBot.__set_task_info(
                task_info, TaskModuleUIConstants.ADAPTIVE_CARD
            )

        return TaskModuleResponseFactory.to_task_module_response(task_info)

    async def on_teams_task_module_submit(
        self, turn_context: TurnContext, task_module_request: TaskModuleRequest
    ) -> TaskModuleResponse:
        """
        Called when data is being returned from the selected option (see `on_teams_task_module_fetch').
        """

        # Echo the users input back.  In a production bot, this is where you'd add behavior in
        # response to the input.
        await turn_context.send_activity(
            MessageFactory.text(
                f"on_teams_task_module_submit: {json.dumps(task_module_request.data)}"
            )
        )

        message_response = TaskModuleMessageResponse(value="Thanks!")
        return TaskModuleResponse(task=message_response)

Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case. Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).
```
### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="0e355-170">Bot フレームワークカードアクションとアダプティブカードアクションの送信アクション</span><span class="sxs-lookup"><span data-stu-id="0e355-170">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="0e355-171">Bot フレームワークカードアクションのスキーマは、アダプティブカードアクションとは少し異なり `Action.Submit` ます。</span><span class="sxs-lookup"><span data-stu-id="0e355-171">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="0e355-172">そのため、タスクモジュールを呼び出す方法は少し異なります。オブジェクトが `data` 含まれているオブジェクトには、 `Action.Submit` `msteams` カード内の他のプロパティに干渉しないようにします。</span><span class="sxs-lookup"><span data-stu-id="0e355-172">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="0e355-173">次の表は、それぞれの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="0e355-173">The following table shows an example of each:</span></span>

| <span data-ttu-id="0e355-174">Bot フレームワークカードアクション</span><span class="sxs-lookup"><span data-stu-id="0e355-174">Bot Framework card action</span></span>                              | <span data-ttu-id="0e355-175">アダプティブカードアクションの送信アクション</span><span class="sxs-lookup"><span data-stu-id="0e355-175">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
