---
title: Microsoft Teams の bot のタスクモジュールを使用する
description: Bot フレームワークカード、アダプティブカード、ディープリンクなど、Microsoft Teams の bot でタスクモジュールを使用する方法について説明します。
keywords: タスクモジュール teams の bot
ms.openlocfilehash: 3a0e4591dbb26ff4afa8cc06edc0a03365da0eca
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674825"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="b8463-104">Microsoft Teams のボットからのタスクモジュールの使用</span><span class="sxs-lookup"><span data-stu-id="b8463-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="b8463-105">タスクモジュールは、アダプティブカードおよび Bot フレームワークカード (英雄、サムネイル、および Office 365 Connector) のボタンを使用して、Microsoft Teams の bot から呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="b8463-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="b8463-106">タスクモジュールは、多くの場合、開発者が bot の状態を追跡し、ユーザーがシーケンスを中断または取り消しられるようにする必要がある、複数の会話手順よりも優れたユーザー環境を提供します。</span><span class="sxs-lookup"><span data-stu-id="b8463-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="b8463-107">タスクモジュールを呼び出すには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="b8463-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="b8463-108">**新しい種類の invoke メッセージ`task/fetch`。**</span><span class="sxs-lookup"><span data-stu-id="b8463-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="b8463-109">`invoke` Bot フレームワークカードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#invoke)、または`Action.Submit`アダプティブカードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)を使用すると`task/fetch`、タスクモジュール (URL またはアダプティブカード) が bot から動的に取り出されます。</span><span class="sxs-lookup"><span data-stu-id="b8463-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="b8463-110">**ディープリンク Url。**</span><span class="sxs-lookup"><span data-stu-id="b8463-110">**Deep link URLs.**</span></span> <span data-ttu-id="b8463-111">[タスクモジュールのディープリンク構文](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)を使用すると、ボットフレームワーク`openUrl`カード、また`Action.OpenUrl`は適応カードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)[をそれぞれ](~/task-modules-and-cards/cards/cards-actions.md#openurl)使用できます。</span><span class="sxs-lookup"><span data-stu-id="b8463-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="b8463-112">深いリンク Url を使用すると、タスクモジュールの URL またはアダプティブカードの本文は明らかによく知られており、 `task/fetch`に対するサーバーのラウンドトリップを回避します。</span><span class="sxs-lookup"><span data-stu-id="b8463-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

## <a name="invoking-a-task-module-via-taskfetch"></a><span data-ttu-id="b8463-113">Task/fetch を使用してタスクモジュールを呼び出す</span><span class="sxs-lookup"><span data-stu-id="b8463-113">Invoking a task module via task/fetch</span></span>

<span data-ttu-id="b8463-114">カードアクション`value`のオブジェクトの場合、また`Action.Submit`は適切な方法で初期化される場合 (以下を参照)、ユーザーがボタンを押すと`invoke` 、メッセージが bot に送信されます。 `invoke`</span><span class="sxs-lookup"><span data-stu-id="b8463-114">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="b8463-115">`invoke`メッセージに対する HTTP 応答では、タスクモジュールを表示するために Teams で使用される[taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)がラッパーオブジェクトに埋め込まれています。</span><span class="sxs-lookup"><span data-stu-id="b8463-115">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![タスク/フェッチ要求/応答](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="b8463-117">各手順について、さらに詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="b8463-117">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="b8463-118">この例では、"Buy" `invoke` [カードアクション](~/task-modules-and-cards/cards/cards-actions.md#invoke)を含む Bot フレームワークの英雄カードを示します。</span><span class="sxs-lookup"><span data-stu-id="b8463-118">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="b8463-119">`type`プロパティの値は`task/fetch` 、 `value`オブジェクトの残りの部分を任意のものにすることができます。</span><span class="sxs-lookup"><span data-stu-id="b8463-119">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
2. <span data-ttu-id="b8463-120">Bot が HTTP POST `invoke`メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="b8463-120">The bot receives the `invoke` HTTP POST message.</span></span>
3. <span data-ttu-id="b8463-121">Bot は応答オブジェクトを作成し、それを HTTP 200 応答コードを使用して POST 応答の本文に返します。</span><span class="sxs-lookup"><span data-stu-id="b8463-121">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="b8463-122">応答のスキーマについては、次の「[タスク/送信に](#the-flexibility-of-tasksubmit)ついて」を参照してください。ここで覚えておくべき重要な点は、HTTP 応答の本文に、次のように、ラッパーオブジェクトに埋め込まれた[taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)が含まれるということです。</span><span class="sxs-lookup"><span data-stu-id="b8463-122">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, e.g.:</span></span>

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
    
    <span data-ttu-id="b8463-123">Bot `task/fetch`に対するイベントとその応答は、概念的にはクライアント SDK `microsoftTeams.tasks.startTask()`の関数に似ています。</span><span class="sxs-lookup"><span data-stu-id="b8463-123">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
4. <span data-ttu-id="b8463-124">Microsoft Teams では、タスクモジュールが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b8463-124">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="b8463-125">タスクモジュールの結果を提出する</span><span class="sxs-lookup"><span data-stu-id="b8463-125">Submitting the result of a task module</span></span>

<span data-ttu-id="b8463-126">ユーザーがタスクモジュールで作業を終了すると、検索結果は[タブを使用](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)した場合と同じようになりますが、いくつかの違いがあるので、ここでも説明します。</span><span class="sxs-lookup"><span data-stu-id="b8463-126">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="b8463-127">**HTML/JavaScript (`TaskInfo.url`)**。</span><span class="sxs-lookup"><span data-stu-id="b8463-127">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="b8463-128">ユーザーが入力したことを確認したら、 `microsoftTeams.tasks.submitTask()` SDK 関数を呼び出します (読みやすさを`submitTask()`目的として、以降を参照)。</span><span class="sxs-lookup"><span data-stu-id="b8463-128">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="b8463-129">タスクモジュールを`submitTask()`閉じるだけの場合は、パラメーターを指定せずに呼び出すことができ`submitHandler`ますが、ほとんどの場合、オブジェクトまたは文字列をに渡すことが必要になります。</span><span class="sxs-lookup"><span data-stu-id="b8463-129">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="b8463-130">単にこれを`result`最初のパラメーターとして渡します。</span><span class="sxs-lookup"><span data-stu-id="b8463-130">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="b8463-131">Teams が呼び出す`submitHandler`: `err` `null` `result`はに`submitTask()`なり、渡されたオブジェクト/文字列になります。</span><span class="sxs-lookup"><span data-stu-id="b8463-131">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="b8463-132">`result`パラメーターを指定し`submitTask()`て呼び出しを行う場合`appId`は、または文字列の`appId`配列を渡す**必要があり**ます。これにより、チームは、結果を送信しているアプリがタスクモジュールを呼び出したものと同じであることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="b8463-132">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="b8463-133">Bot は、[次](#payload-of-taskfetch-and-tasksubmit-messages)に`task/submit`示す`result`ようなメッセージを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="b8463-133">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="b8463-134">**アダプティブカード (`TaskInfo.card`)**。</span><span class="sxs-lookup"><span data-stu-id="b8463-134">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="b8463-135">ユーザーが任意`Action.Submit`のボタンを押したときに、ユーザーが入力したアダプティブカードの本文`task/submit`が、メッセージによって bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="b8463-135">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="b8463-136">タスク/提出の柔軟性</span><span class="sxs-lookup"><span data-stu-id="b8463-136">The flexibility of task/submit</span></span>

<span data-ttu-id="b8463-137">前のセクションでは、ユーザーが bot から呼び出されたタスクモジュールで終了すると、bot は常にメッセージを`task/submit invoke`受信することを学びました。</span><span class="sxs-lookup"><span data-stu-id="b8463-137">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="b8463-138">開発者は、 `task/submit`メッセージに*応答*するときにいくつかのオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="b8463-138">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="b8463-139">HTTP 本文の応答</span><span class="sxs-lookup"><span data-stu-id="b8463-139">HTTP Body Response</span></span>                      | <span data-ttu-id="b8463-140">シナリオ</span><span class="sxs-lookup"><span data-stu-id="b8463-140">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="b8463-141">なし (メッセージを`task/submit`無視します)</span><span class="sxs-lookup"><span data-stu-id="b8463-141">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="b8463-142">最も単純な応答は、まったく応答がありません。</span><span class="sxs-lookup"><span data-stu-id="b8463-142">The simplest response is no response at all.</span></span> <span data-ttu-id="b8463-143">ユーザーがタスクモジュールで作業を終了すると、bot は応答する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="b8463-143">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="b8463-144">の`value`値は、Teams によってポップアップメッセージボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="b8463-144">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="b8463-145">1つのウィザード/複数ステップの画面で、アダプティブカードのシーケンスを "チェーン" することができます。</span><span class="sxs-lookup"><span data-stu-id="b8463-145">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="b8463-146">_アダプティブカードをシーケンスにチェーンすることは高度なシナリオで、ここでは文書化されていません。Node.js サンプルアプリは、これをサポートしていますが、その機能が[README.md ファイル](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)に記載されているかどうかについて説明します。_</span><span class="sxs-lookup"><span data-stu-id="b8463-146">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="b8463-147">タスク/フェッチおよびタスク/送信メッセージのペイロード</span><span class="sxs-lookup"><span data-stu-id="b8463-147">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="b8463-148">このセクションでは、bot が、または`task/fetch` `task/submit` bot フレームワーク`Activity`オブジェクトを受け取ったときに、bot が受け取る内容のスキーマを定義します。</span><span class="sxs-lookup"><span data-stu-id="b8463-148">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="b8463-149">重要な最上位レベルは下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="b8463-149">The important top-level appear below:</span></span>

| <span data-ttu-id="b8463-150">プロパティ</span><span class="sxs-lookup"><span data-stu-id="b8463-150">Property</span></span> | <span data-ttu-id="b8463-151">説明</span><span class="sxs-lookup"><span data-stu-id="b8463-151">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="b8463-152">は常に`invoke`</span><span class="sxs-lookup"><span data-stu-id="b8463-152">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="b8463-153">`task/fetch`あるいは`task/submit`</span><span class="sxs-lookup"><span data-stu-id="b8463-153">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="b8463-154">開発者が定義したペイロード。</span><span class="sxs-lookup"><span data-stu-id="b8463-154">The developer-defined payload.</span></span> <span data-ttu-id="b8463-155">通常、 `value`オブジェクトの構造は Teams から送信されたものを反映します。</span><span class="sxs-lookup"><span data-stu-id="b8463-155">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="b8463-156">ただし`task/fetch`、この場合は、bot フレームワーク (`value`) とアダプティブカード`Action.Submit`アクション (`data`) の両方から動的な fetch () をサポートし、に`context` `value` / `data`含まれていたものに加えて Teams を bot に伝達する方法が必要になります。</span><span class="sxs-lookup"><span data-stu-id="b8463-156">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="b8463-157">これを行うには、2つを親オブジェクトに結合します。</span><span class="sxs-lookup"><span data-stu-id="b8463-157">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="b8463-158">例: タスク/フェッチおよびタスク/送信呼び出しメッセージの受信と応答-node.js</span><span class="sxs-lookup"><span data-stu-id="b8463-158">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

<span data-ttu-id="b8463-159">Bot フレームワーク`invoke`でのメッセージの処理は、BOT フレームワーク SDK では正式にサポートされていないため、少し厄介になることがあります。</span><span class="sxs-lookup"><span data-stu-id="b8463-159">Dealing with `invoke` messages in Bot Framework can be a little tricky because there's no formal support for them in the Bot Framework SDK.</span></span> <span data-ttu-id="b8463-160">これを簡単にするために、 `onInvoke()`チームは botbuilder npm パッケージでヘルパー関数を作成しました[(node.js の場合)](https://www.npmjs.com/package/botbuilder-teams)。</span><span class="sxs-lookup"><span data-stu-id="b8463-160">To make it easier, Teams has created `onInvoke()` helper functions in the [botbuilder-teams npm package (for Node.js)](https://www.npmjs.com/package/botbuilder-teams).</span></span> <span data-ttu-id="b8463-161">次の例は、その方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="b8463-161">This example below shows how to do it:</span></span>

> [!NOTE]
> <span data-ttu-id="b8463-162">次に示すサンプルコードは、この機能の Technical Preview と最終リリースの間で変更さ`task/fetch`れました。要求のスキーマは、[前のセクションで説明](#payload-of-taskfetch-and-tasksubmit-messages)した内容に従って変更されました。</span><span class="sxs-lookup"><span data-stu-id="b8463-162">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="b8463-163">つまり、ドキュメントは修正されましたが、実装はできませんでした。</span><span class="sxs-lookup"><span data-stu-id="b8463-163">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="b8463-164">変更点`// for Technical Preview [...]`については、次のコメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b8463-164">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

```typescript
// Handle requests and responses for a "Custom Form" and an "Adaptive card" task module.
// Assumes request is coming from an Adaptive card Action.Submit button that has a "taskModule" property indicating what to invoke
private async onInvoke(event: builder.IEvent, cb: (err: Error, body: any, status?: number) => void): Promise<void> {
    let invokeType = (event as any).name;
    let invokeValue = (event as any).value;
    if (invokeType === undefined) {
        invokeType = null;
    }
    switch (invokeType) {
        case "task/fetch": {
            if (invokeValue !== undefined && invokeValue.data.taskModule === "customform") { // for Technical Preview, was invokeValue.taskModule
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Custom Form",
                            "height": 510,
                            "width": 430,
                            "fallbackUrl": "https://contoso.com/teamsapp/customform",
                            "url": "https://contoso.com/teamsapp/customform",
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            if (invokeValue !== undefined && invokeValue.data.taskModule === "adaptivecard") { // for Technical Preview, was invokeValue.taskModule
                let adaptiveCard = {
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
                };
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Ninja Cat",
                            "height": "small",
                            "width": "small",
                            "card": {
                                contentType: "application/vnd.microsoft.card.adaptive",
                                content: adaptiveCard,
                            }
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            break;
        }
        case "task/submit": {
            if (invokeValue.data !== undefined) {
                // It's a valid task module response
                let submitResponse: any = {
                    "task": {
                        "type": "message",
                        "value": "Task complete!",
                    }
                };
                cb(null, fetchTemplates.submitMessageResponse, 200)
            }
        }
    }
}
```

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="b8463-165">例: タスク/フェッチおよびタスク/送信呼び出しメッセージを受信して応答する-C#</span><span class="sxs-lookup"><span data-stu-id="b8463-165">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="b8463-166">C# bot では`invoke` 、メッセージは`Activity`メッセージを`HttpResponseMessage()`処理するコントローラーによって処理されます。</span><span class="sxs-lookup"><span data-stu-id="b8463-166">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="b8463-167">と`task/fetch` `task/submit`の要求と応答は JSON です。</span><span class="sxs-lookup"><span data-stu-id="b8463-167">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="b8463-168">C# では、JSON の場合と同様に、生の JSON を処理することはできません。そのため、JSON とのシリアル化を処理するラッパークラスが必要です。</span><span class="sxs-lookup"><span data-stu-id="b8463-168">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="b8463-169">このことは、Microsoft Teams の[C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)で直接サポートされていませんが、これらの簡単なラッパークラスが[C# サンプルアプリ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)でどのように表示されるかの例を確認できます。</span><span class="sxs-lookup"><span data-stu-id="b8463-169">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="b8463-170">以下は、これらのラッパークラス ( `task/fetch` `task/submit` `TaskInfo`, `TaskEnvelope`) を使用して、次のようなコードを処理およびメッセージを処理するための C# のコード例です。 excerpted のコード[は次の](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)とおりです。</span><span class="sxs-lookup"><span data-stu-id="b8463-170">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

```csharp
private HttpResponseMessage HandleInvokeMessages(Activity activity)
{
    var activityValue = activity.Value.ToString();
    if (activity.Name == "task/fetch")
    {
        var action = Newtonsoft.Json.JsonConvert.DeserializeObject<Models.BotFrameworkCardValue<string>>(activityValue);

        Models.TaskInfo taskInfo = GetTaskInfo(action.Data);
        Models.TaskEnvelope taskEnvelope = new Models.TaskEnvelope
        {
            Task = new Models.Task()
            {
                Type = Models.TaskType.Continue,
                TaskInfo = taskInfo
            }
        };
        return Request.CreateResponse(HttpStatusCode.OK, taskEnvelope);
    }
    else if (activity.Name == "task/submit")
    {
        ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
        Activity reply = activity.CreateReply("Received = " + activity.Value.ToString());
        connector.Conversations.ReplyToActivity(reply);
    }
    return new HttpResponseMessage(HttpStatusCode.Accepted);
}

// Helper function for building the TaskInfo object based on the incoming request
private static Models.TaskInfo GetTaskInfo(string actionInfo)
{
    Models.TaskInfo taskInfo = new Models.TaskInfo();
    switch (actionInfo)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.PowerApp:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.PowerApp;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.PowerApp);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = AdaptiveCardHelper.GetAdaptiveCard();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }
    return taskInfo;
}
```

<span data-ttu-id="b8463-171">上記の例に示されてい`SetTaskInfo()`ない関数は、各`height`case `width`の`TaskInfo`オブジェクト`title`の、、およびプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="b8463-171">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="b8463-172">[SetTaskInfo () のソースコード](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)を次に示します。</span><span class="sxs-lookup"><span data-stu-id="b8463-172">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="b8463-173">Bot フレームワークカードアクションとアダプティブカードアクションの送信アクション</span><span class="sxs-lookup"><span data-stu-id="b8463-173">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="b8463-174">Bot フレームワークカードアクションのスキーマは、アダプティブカード`Action.Submit`アクションとは少し異なります。</span><span class="sxs-lookup"><span data-stu-id="b8463-174">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="b8463-175">そのため、タスクモジュールを呼び出す方法は少し異なります。オブジェクトが`data`含まれ`Action.Submit` `msteams`ているオブジェクトには、カード内の他のプロパティに干渉しないようにします。</span><span class="sxs-lookup"><span data-stu-id="b8463-175">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="b8463-176">次の表は、それぞれの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="b8463-176">The following table shows an example of each:</span></span>

| <span data-ttu-id="b8463-177">Bot フレームワークカードアクション</span><span class="sxs-lookup"><span data-stu-id="b8463-177">Bot Framework card action</span></span>                              | <span data-ttu-id="b8463-178">アダプティブカードアクションの送信アクション</span><span class="sxs-lookup"><span data-stu-id="b8463-178">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
