---
title: Microsoft Teams の bot のタスクモジュールを使用する
description: Bot フレームワークカード、アダプティブカード、ディープリンクなど、Microsoft Teams の bot でタスクモジュールを使用する方法について説明します。
keywords: タスクモジュール teams の bot
ms.openlocfilehash: 32fb6a4aa0a8bf2297a4f60331dc5c6c6aceb4e2
ms.sourcegitcommit: 214eccbadb7f3a67236b79a041ef487b7bf6dfbd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "44801329"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="05ef2-104">Microsoft Teams のボットからのタスクモジュールの使用</span><span class="sxs-lookup"><span data-stu-id="05ef2-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="05ef2-105">タスクモジュールは、アダプティブカードおよび Bot フレームワークカード (英雄、サムネイル、および Office 365 Connector) のボタンを使用して、Microsoft Teams の bot から呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="05ef2-106">タスクモジュールは、多くの場合、開発者が bot の状態を追跡し、ユーザーがシーケンスを中断または取り消しられるようにする必要がある、複数の会話手順よりも優れたユーザー環境を提供します。</span><span class="sxs-lookup"><span data-stu-id="05ef2-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="05ef2-107">タスクモジュールを呼び出すには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="05ef2-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="05ef2-108">**新しい種類の invoke メッセージ `task/fetch` 。**</span><span class="sxs-lookup"><span data-stu-id="05ef2-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="05ef2-109">`invoke`Bot フレームワークカードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#invoke)、または `Action.Submit` アダプティブカードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)を使用すると、 `task/fetch` タスクモジュール (URL またはアダプティブカード) が bot から動的に取り出されます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="05ef2-110">**ディープリンク Url。**</span><span class="sxs-lookup"><span data-stu-id="05ef2-110">**Deep link URLs.**</span></span> <span data-ttu-id="05ef2-111">[タスクモジュールのディープリンク構文](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)を使用すると、 `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl)ボットフレームワークカード、または `Action.OpenUrl` 適応カードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)をそれぞれ使用できます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="05ef2-112">深いリンク Url を使用すると、タスクモジュールの URL またはアダプティブカードの本文は明らかによく知られており、に対するサーバーのラウンドトリップを回避 `task/fetch` します。</span><span class="sxs-lookup"><span data-stu-id="05ef2-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

>[!IMPORTANT]
><span data-ttu-id="05ef2-113">セキュリティで保護された通信を確保するために、それぞれに `url` `fallbackUrl` HTTPS 暗号化プロトコルを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="05ef2-113">To ensure secure communications, each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

## <a name="invoking-a-task-module-via-taskfetch"></a><span data-ttu-id="05ef2-114">Task/fetch を使用してタスクモジュールを呼び出す</span><span class="sxs-lookup"><span data-stu-id="05ef2-114">Invoking a task module via task/fetch</span></span>

<span data-ttu-id="05ef2-115">`value`カードアクションのオブジェクトの場合、 `invoke` または `Action.Submit` 適切な方法で初期化される場合 (以下を参照)、ユーザーがボタンを押すと、 `invoke` メッセージが bot に送信されます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="05ef2-116">メッセージに対する HTTP 応答では `invoke` 、タスクモジュールを表示するために Teams で使用される[taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)がラッパーオブジェクトに埋め込まれています。</span><span class="sxs-lookup"><span data-stu-id="05ef2-116">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![タスク/フェッチ要求/応答](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="05ef2-118">各手順について、さらに詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="05ef2-118">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="05ef2-119">この例では、"Buy" カードアクションを含む Bot フレームワークの英雄カードを示し `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke)ます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-119">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="05ef2-120">プロパティの値 `type` は、 `task/fetch` オブジェクトの残りの部分を `value` 任意のものにすることができます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-120">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
2. <span data-ttu-id="05ef2-121">Bot が `invoke` HTTP POST メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="05ef2-121">The bot receives the `invoke` HTTP POST message.</span></span>
3. <span data-ttu-id="05ef2-122">Bot は応答オブジェクトを作成し、それを HTTP 200 応答コードを使用して POST 応答の本文に返します。</span><span class="sxs-lookup"><span data-stu-id="05ef2-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="05ef2-123">応答のスキーマについては、次の「[タスク/送信に](#the-flexibility-of-tasksubmit)ついて」を参照してください。ここで覚えておくべき重要な点は、HTTP 応答の本文に、次のように、ラッパーオブジェクトに埋め込まれた[taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)が含まれるということです。</span><span class="sxs-lookup"><span data-stu-id="05ef2-123">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, e.g.:</span></span>

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

    <span data-ttu-id="05ef2-124">`task/fetch`Bot に対するイベントとその応答は、概念的には `microsoftTeams.tasks.startTask()` クライアント SDK の関数に似ています。</span><span class="sxs-lookup"><span data-stu-id="05ef2-124">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
4. <span data-ttu-id="05ef2-125">Microsoft Teams では、タスクモジュールが表示されます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-125">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="05ef2-126">タスクモジュールの結果を提出する</span><span class="sxs-lookup"><span data-stu-id="05ef2-126">Submitting the result of a task module</span></span>

<span data-ttu-id="05ef2-127">ユーザーがタスクモジュールで作業を終了すると、検索結果は[タブを使用](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)した場合と同じようになりますが、いくつかの違いがあるので、ここでも説明します。</span><span class="sxs-lookup"><span data-stu-id="05ef2-127">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="05ef2-128">**HTML/JavaScript ( `TaskInfo.url` )**。</span><span class="sxs-lookup"><span data-stu-id="05ef2-128">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="05ef2-129">ユーザーが入力したことを確認したら、 `microsoftTeams.tasks.submitTask()` SDK 関数を呼び出し `submitTask()` ます (読みやすさを目的として、以降を参照)。</span><span class="sxs-lookup"><span data-stu-id="05ef2-129">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="05ef2-130">`submitTask()`タスクモジュールを閉じるだけの場合は、パラメーターを指定せずに呼び出すことができますが、ほとんどの場合、オブジェクトまたは文字列をに渡すことが必要になり `submitHandler` ます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-130">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="05ef2-131">単にこれを最初のパラメーターとして渡し `result` ます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-131">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="05ef2-132">Teams が呼び出す `submitHandler` : はになり、 `err` 渡され `null` `result` たオブジェクト/文字列になり `submitTask()` ます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-132">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="05ef2-133">パラメーターを指定して呼び出しを行う場合 `submitTask()` `result` は、または文字列の配列を渡す**必要があり** `appId` `appId` ます。これにより、チームは、結果を送信しているアプリがタスクモジュールを呼び出したものと同じであることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-133">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="05ef2-134">Bot は、次に `task/submit` 示すようなメッセージを受け取り `result` ます。 [below](#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="05ef2-134">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="05ef2-135">**アダプティブカード ( `TaskInfo.card` )**。</span><span class="sxs-lookup"><span data-stu-id="05ef2-135">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="05ef2-136">ユーザーが任意のボタンを押したときに、ユーザーが入力したアダプティブカードの本文が、メッセージによって bot に送信され `task/submit` `Action.Submit` ます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-136">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="05ef2-137">タスク/提出の柔軟性</span><span class="sxs-lookup"><span data-stu-id="05ef2-137">The flexibility of task/submit</span></span>

<span data-ttu-id="05ef2-138">前のセクションでは、ユーザーが bot から呼び出されたタスクモジュールで終了すると、bot は常にメッセージを受信することを学びました `task/submit invoke` 。</span><span class="sxs-lookup"><span data-stu-id="05ef2-138">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="05ef2-139">開発者は、メッセージに*応答*するときにいくつかのオプションを使用でき `task/submit` ます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-139">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="05ef2-140">HTTP 本文の応答</span><span class="sxs-lookup"><span data-stu-id="05ef2-140">HTTP Body Response</span></span>                      | <span data-ttu-id="05ef2-141">シナリオ</span><span class="sxs-lookup"><span data-stu-id="05ef2-141">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="05ef2-142">なし (メッセージを無視します `task/submit` )</span><span class="sxs-lookup"><span data-stu-id="05ef2-142">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="05ef2-143">最も単純な応答は、まったく応答がありません。</span><span class="sxs-lookup"><span data-stu-id="05ef2-143">The simplest response is no response at all.</span></span> <span data-ttu-id="05ef2-144">ユーザーがタスクモジュールで作業を終了すると、bot は応答する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="05ef2-144">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="05ef2-145">の値は、Teams によって `value` ポップアップメッセージボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-145">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="05ef2-146">1つのウィザード/複数ステップの画面で、アダプティブカードのシーケンスを "チェーン" することができます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-146">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="05ef2-147">_アダプティブカードをシーケンスにチェーンすることは高度なシナリオで、ここでは文書化されていません。Node.js サンプルアプリはこれをサポートしていますが、その機能が[README.md ファイル](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)に記載されています。_</span><span class="sxs-lookup"><span data-stu-id="05ef2-147">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="05ef2-148">タスク/フェッチおよびタスク/送信メッセージのペイロード</span><span class="sxs-lookup"><span data-stu-id="05ef2-148">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="05ef2-149">このセクションでは、bot が、または bot フレームワークオブジェクトを受け取ったときに、bot が受け取る内容のスキーマを定義 `task/fetch` `task/submit` `Activity` します。</span><span class="sxs-lookup"><span data-stu-id="05ef2-149">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="05ef2-150">重要な最上位レベルは下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-150">The important top-level appear below:</span></span>

| <span data-ttu-id="05ef2-151">プロパティ</span><span class="sxs-lookup"><span data-stu-id="05ef2-151">Property</span></span> | <span data-ttu-id="05ef2-152">説明</span><span class="sxs-lookup"><span data-stu-id="05ef2-152">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="05ef2-153">は常に`invoke`</span><span class="sxs-lookup"><span data-stu-id="05ef2-153">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="05ef2-154">`task/fetch`あるいは`task/submit`</span><span class="sxs-lookup"><span data-stu-id="05ef2-154">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="05ef2-155">開発者が定義したペイロード。</span><span class="sxs-lookup"><span data-stu-id="05ef2-155">The developer-defined payload.</span></span> <span data-ttu-id="05ef2-156">通常、オブジェクトの構造は `value` Teams から送信されたものを反映します。</span><span class="sxs-lookup"><span data-stu-id="05ef2-156">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="05ef2-157">ただし、この場合は、 `task/fetch` Bot フレームワーク () とアダプティブカードアクション () の両方から動的な fetch () をサポートし、 `value` `Action.Submit` `data` `context` に含まれていたものに加えて Teams を bot に伝達する方法が必要になり `value` / `data` ます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-157">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="05ef2-158">これを行うには、2つを親オブジェクトに結合します。</span><span class="sxs-lookup"><span data-stu-id="05ef2-158">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="05ef2-159">例: タスク/フェッチおよびタスク/送信呼び出しメッセージの受信と応答 Node.js</span><span class="sxs-lookup"><span data-stu-id="05ef2-159">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

> [!NOTE]
> <span data-ttu-id="05ef2-160">次に示すサンプルコードは、この機能の Technical Preview と最終リリースの間で変更されました。要求のスキーマは、 `task/fetch` [前のセクションで説明](#payload-of-taskfetch-and-tasksubmit-messages)した内容に従って変更されました。</span><span class="sxs-lookup"><span data-stu-id="05ef2-160">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="05ef2-161">つまり、ドキュメントは修正されましたが、実装はできませんでした。</span><span class="sxs-lookup"><span data-stu-id="05ef2-161">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="05ef2-162">変更点については、次のコメントを参照してください `// for Technical Preview [...]` 。</span><span class="sxs-lookup"><span data-stu-id="05ef2-162">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

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

<span data-ttu-id="05ef2-163">*詳細について*は、「 [Microsoft Teams のタスクモジュールサンプルコード」、「nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) 」および「 [Bot フレームワークサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="05ef2-163">*See also*, [Microsoft Teams task module sample code — nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) and  [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="05ef2-164">例: タスク/フェッチおよびタスク/送信呼び出しメッセージを受信して応答する-C#</span><span class="sxs-lookup"><span data-stu-id="05ef2-164">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="05ef2-165">C# bot では、メッセージ `invoke` はメッセージを処理するコントローラーによって処理され `HttpResponseMessage()` `Activity` ます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-165">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="05ef2-166">`task/fetch`との `task/submit` 要求と応答は JSON です。</span><span class="sxs-lookup"><span data-stu-id="05ef2-166">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="05ef2-167">C# では、Node.js のように raw JSON を処理するのは便利ではありません。したがって、JSON とのシリアル化を処理するには、ラッパークラスが必要です。</span><span class="sxs-lookup"><span data-stu-id="05ef2-167">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="05ef2-168">このことは、Microsoft Teams の[C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)で直接サポートされていませんが、これらの簡単なラッパークラスが[C# サンプルアプリ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)でどのように表示されるかの例を確認できます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-168">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="05ef2-169">以下は、 `task/fetch` `task/submit` これらのラッパークラス (,) を使用して、次のようなコードを処理およびメッセージを処理するための C# のコード例です `TaskInfo` `TaskEnvelope` 。 excerpted [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)のコードは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="05ef2-169">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

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

<span data-ttu-id="05ef2-170">上記の例に示されていない関数は、 `SetTaskInfo()` `height` `width` `title` 各 case のオブジェクトの、、およびプロパティを設定し `TaskInfo` ます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-170">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="05ef2-171">[SetTaskInfo () のソースコード](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)を次に示します。</span><span class="sxs-lookup"><span data-stu-id="05ef2-171">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="05ef2-172">Bot フレームワークカードアクションとアダプティブカードアクションの送信アクション</span><span class="sxs-lookup"><span data-stu-id="05ef2-172">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="05ef2-173">Bot フレームワークカードアクションのスキーマは、アダプティブカードアクションとは少し異なり `Action.Submit` ます。</span><span class="sxs-lookup"><span data-stu-id="05ef2-173">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="05ef2-174">そのため、タスクモジュールを呼び出す方法は少し異なります。オブジェクトが `data` 含まれているオブジェクトには、 `Action.Submit` `msteams` カード内の他のプロパティに干渉しないようにします。</span><span class="sxs-lookup"><span data-stu-id="05ef2-174">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="05ef2-175">次の表は、それぞれの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="05ef2-175">The following table shows an example of each:</span></span>

| <span data-ttu-id="05ef2-176">Bot フレームワークカードアクション</span><span class="sxs-lookup"><span data-stu-id="05ef2-176">Bot Framework card action</span></span>                              | <span data-ttu-id="05ef2-177">アダプティブカードアクションの送信アクション</span><span class="sxs-lookup"><span data-stu-id="05ef2-177">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
