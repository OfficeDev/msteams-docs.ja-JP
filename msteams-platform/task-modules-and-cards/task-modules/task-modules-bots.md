---
title: ボットでのタスク モジュールMicrosoft Teamsする
description: ボット フレームワーク カード、アダプティブ カード、ディープ Microsoft Teamsなど、ボットでタスク モジュールを使用する方法
localization_priority: Normal
ms.topic: how-to
keywords: タスク モジュールのチーム ボット
ms.openlocfilehash: bfaf3dfe791c1736aeb418e2689e513908f04534
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566570"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="8b07b-104">ボットからのタスク モジュールMicrosoft Teamsする</span><span class="sxs-lookup"><span data-stu-id="8b07b-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="8b07b-105">タスク モジュールは、アダプティブ カードMicrosoft Teamsボット フレームワーク カード (Hero、Thumbnail、および Office 365 コネクタ) のボタンを使用して、ボットから呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="8b07b-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="8b07b-106">多くの場合、タスク モジュールは、開発者がボットの状態を追跡し、ユーザーがシーケンスを中断/取り消す必要がある複数の会話手順よりも優れたユーザー エクスペリエンスです。</span><span class="sxs-lookup"><span data-stu-id="8b07b-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="8b07b-107">タスク モジュールを呼び出す方法は 2 通りあります。</span><span class="sxs-lookup"><span data-stu-id="8b07b-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="8b07b-108">**新しい種類の呼び出しメッセージ `task/fetch` 。**</span><span class="sxs-lookup"><span data-stu-id="8b07b-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="8b07b-109">Bot Framework カードのカード アクション、またはアダプティブ カードのカード アクションを使用すると、タスク モジュール (URL またはアダプティブ カード) がボットから動的に `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` フェッチされます。</span><span class="sxs-lookup"><span data-stu-id="8b07b-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="8b07b-110">**ディープ リンク URL。**</span><span class="sxs-lookup"><span data-stu-id="8b07b-110">**Deep link URLs.**</span></span> <span data-ttu-id="8b07b-111">タスク モジュール[のディープ リンク構文を](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)使用すると、Bot Framework カードのカード アクション、アダプティブ カードのカード アクションをそれぞれ `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)使用できます。</span><span class="sxs-lookup"><span data-stu-id="8b07b-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="8b07b-112">ディープ リンク URL では、タスク モジュールの URL またはアダプティブ カードの本文が事前に明らかに知られているので、サーバーのラウンドトリップは避けます `task/fetch` 。</span><span class="sxs-lookup"><span data-stu-id="8b07b-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

>[!IMPORTANT]
><span data-ttu-id="8b07b-113">安全な通信を確保するには、HTTPS `url` `fallbackUrl` 暗号化プロトコルを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8b07b-113">To ensure secure communications, each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

## <a name="invoking-a-task-module-through-taskfetch"></a><span data-ttu-id="8b07b-114">タスク/フェッチによるタスク モジュールの呼び出し</span><span class="sxs-lookup"><span data-stu-id="8b07b-114">Invoking a task module through task/fetch</span></span>

<span data-ttu-id="8b07b-115">カードアクションのオブジェクトが適切な方法で初期化されている場合 (以下で詳しく説明します)、ユーザーがボタンを押すと、メッセージがボット `value` `invoke` `Action.Submit` `invoke` に送信されます。</span><span class="sxs-lookup"><span data-stu-id="8b07b-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="8b07b-116">メッセージに対する HTTP 応答には、ラッパー オブジェクトに TaskInfo オブジェクトが埋め込まれているので、Teamsモジュールの表示に `invoke` 使用されます。 [](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="8b07b-116">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![task/fetch request/response](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="8b07b-118">各手順についてもう少し詳しく見てみます。</span><span class="sxs-lookup"><span data-stu-id="8b07b-118">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="8b07b-119">次の使用例は、"Buy" カードアクションを持つ Bot Framework Hero `invoke` [カードを示しています](~/task-modules-and-cards/cards/cards-actions.md#invoke)。</span><span class="sxs-lookup"><span data-stu-id="8b07b-119">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="8b07b-120">プロパティの値 `type` は、 `task/fetch` - オブジェクトの残りの `value` 部分は、好きなものは何でもできます。</span><span class="sxs-lookup"><span data-stu-id="8b07b-120">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
1. <span data-ttu-id="8b07b-121">ボットは HTTP `invoke` POST メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="8b07b-121">The bot receives the `invoke` HTTP POST message.</span></span>
1. <span data-ttu-id="8b07b-122">ボットは応答オブジェクトを作成し、HTTP 200 応答コードを使用して POST 応答の本文に返します。</span><span class="sxs-lookup"><span data-stu-id="8b07b-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="8b07b-123">応答のスキーマについては、以下のタスク [/](#the-flexibility-of-tasksubmit)送信に関するディスカッションで説明しますが、今覚えておく必要がある重要な点は、HTTP 応答の本文にラッパー オブジェクトに埋め込まれた [TaskInfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) が含まれていることです。</span><span class="sxs-lookup"><span data-stu-id="8b07b-123">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object.</span></span> <span data-ttu-id="8b07b-124">例:</span><span class="sxs-lookup"><span data-stu-id="8b07b-124">For example:</span></span>

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

    <span data-ttu-id="8b07b-125">ボット `task/fetch` のイベントとその応答は、概念的には、クライアント SDK `microsoftTeams.tasks.startTask()` の関数と似ています。</span><span class="sxs-lookup"><span data-stu-id="8b07b-125">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
1. <span data-ttu-id="8b07b-126">Microsoft Teamsタスク モジュールを表示します。</span><span class="sxs-lookup"><span data-stu-id="8b07b-126">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="8b07b-127">タスク モジュールの結果の送信</span><span class="sxs-lookup"><span data-stu-id="8b07b-127">Submitting the result of a task module</span></span>

<span data-ttu-id="8b07b-128">ユーザーがタスク モジュールを終了すると、ボットに結果を送信し戻すのは、タブ[](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)の動作と似ていますが、いくつかの違いがあります。ここではも説明します。</span><span class="sxs-lookup"><span data-stu-id="8b07b-128">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="8b07b-129">**HTML/JavaScript ( `TaskInfo.url` ) 。**</span><span class="sxs-lookup"><span data-stu-id="8b07b-129">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="8b07b-130">ユーザーが入力した情報を検証したら、SDK 関数を呼び出します (以下、読みやすさの目的 `microsoftTeams.tasks.submitTask()` `submitTask()` で呼び出します)。</span><span class="sxs-lookup"><span data-stu-id="8b07b-130">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="8b07b-131">Teams がタスク モジュールを閉じるだけで、ほとんどの場合、オブジェクトまたは文字列を自分のタスク モジュールに渡す場合は、パラメーターを指定せずに呼び出 `submitTask()` します `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="8b07b-131">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="8b07b-132">単に最初のパラメーターとして渡します `result` 。</span><span class="sxs-lookup"><span data-stu-id="8b07b-132">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="8b07b-133">Teams呼び `submitHandler` 出す : `err` は、渡した `null` `result` オブジェクト/文字列になります `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="8b07b-133">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="8b07b-134">パラメーターを使用して呼び出す場合は、文字列の配列または配列を渡す必要があります `submitTask()` `result`  `appId` `appId` 。これにより、Teams は、結果を送信するアプリがタスク モジュールを呼び出したアプリと同じことを検証できます。</span><span class="sxs-lookup"><span data-stu-id="8b07b-134">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="8b07b-135">ボットは、以下の説明 `task/submit` を含む `result` メッセージを受信 [します](#payload-of-taskfetch-and-tasksubmit-messages)。</span><span class="sxs-lookup"><span data-stu-id="8b07b-135">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="8b07b-136">**アダプティブ カード ( `TaskInfo.card` ) 。**</span><span class="sxs-lookup"><span data-stu-id="8b07b-136">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="8b07b-137">アダプティブ カード本文 (ユーザーが入力した場合) は、ユーザーがボタンを押すと、メッセージを介してボット `task/submit` に送信 `Action.Submit` されます。</span><span class="sxs-lookup"><span data-stu-id="8b07b-137">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="8b07b-138">タスク/送信の柔軟性</span><span class="sxs-lookup"><span data-stu-id="8b07b-138">The flexibility of task/submit</span></span>

<span data-ttu-id="8b07b-139">前のセクションでは、ユーザーがボットから呼び出されたタスク モジュールを終了すると、ボットは常にメッセージを受信する方法について説明 `task/submit invoke` しました。</span><span class="sxs-lookup"><span data-stu-id="8b07b-139">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="8b07b-140">開発者は、メッセージに応答するときに *いくつかのオプション* があります `task/submit` 。</span><span class="sxs-lookup"><span data-stu-id="8b07b-140">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="8b07b-141">HTTP 本文の応答</span><span class="sxs-lookup"><span data-stu-id="8b07b-141">HTTP Body Response</span></span>                      | <span data-ttu-id="8b07b-142">シナリオ</span><span class="sxs-lookup"><span data-stu-id="8b07b-142">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="8b07b-143">なし (メッセージを `task/submit` 無視する)</span><span class="sxs-lookup"><span data-stu-id="8b07b-143">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="8b07b-144">最も単純な応答は応答なしです。</span><span class="sxs-lookup"><span data-stu-id="8b07b-144">The simplest response is no response at all.</span></span> <span data-ttu-id="8b07b-145">ユーザーがタスク モジュールを使い終わったときにボットが応答する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="8b07b-145">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="8b07b-146">Teamsポップアップ メッセージ ボックスに値 `value` が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8b07b-146">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="8b07b-147">ウィザード/マルチステップ エクスペリエンスでアダプティブ カードのシーケンスを一緒に "チェーン" できます。</span><span class="sxs-lookup"><span data-stu-id="8b07b-147">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="8b07b-148">_アダプティブ カードをシーケンスにチェーン化する方法は高度なシナリオであり、ここでは説明しません。ただしNode.jsサンプル アプリではサポートされ、その動作方法は、そのサンプル ファイルに [README.md されます](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)。_</span><span class="sxs-lookup"><span data-stu-id="8b07b-148">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="8b07b-149">タスク/フェッチおよびタスク/送信メッセージのペイロード</span><span class="sxs-lookup"><span data-stu-id="8b07b-149">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="8b07b-150">このセクションでは、ボットがボットまたは Bot Framework オブジェクトを受信するときに受け取るスキーマ `task/fetch` `task/submit` を定義 `Activity` します。</span><span class="sxs-lookup"><span data-stu-id="8b07b-150">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="8b07b-151">重要なトップ レベルは、以下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="8b07b-151">The important top-level appear below:</span></span>

| <span data-ttu-id="8b07b-152">プロパティ</span><span class="sxs-lookup"><span data-stu-id="8b07b-152">Property</span></span> | <span data-ttu-id="8b07b-153">説明</span><span class="sxs-lookup"><span data-stu-id="8b07b-153">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="8b07b-154">常に `invoke`</span><span class="sxs-lookup"><span data-stu-id="8b07b-154">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="8b07b-155">どちらか `task/fetch` または `task/submit`</span><span class="sxs-lookup"><span data-stu-id="8b07b-155">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="8b07b-156">開発者定義のペイロード。</span><span class="sxs-lookup"><span data-stu-id="8b07b-156">The developer-defined payload.</span></span> <span data-ttu-id="8b07b-157">通常、オブジェクトの構造 `value` は、オブジェクトから送信されたデータをTeams。</span><span class="sxs-lookup"><span data-stu-id="8b07b-157">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="8b07b-158">ただし、この場合は、ボット フレームワーク ( ) とアダプティブ カードアクション ( ) の両方から動的フェッチ ( ) をサポートする必要があります。また、Teams をボットと通信する方法が必要です。 `task/fetch` `value` `Action.Submit` `data` `context` `value` / `data`</span><span class="sxs-lookup"><span data-stu-id="8b07b-158">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="8b07b-159">これを行うには、2 つを親オブジェクトに結合します。</span><span class="sxs-lookup"><span data-stu-id="8b07b-159">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="8b07b-160">例: タスク/フェッチおよびタスク/送信の呼び出しメッセージの受信と応答 - Node.js</span><span class="sxs-lookup"><span data-stu-id="8b07b-160">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

> [!NOTE]
> <span data-ttu-id="8b07b-161">次のサンプル コードは、テクニカル プレビューとこの機能の最終リリースの間で変更されました。要求のスキーマは、前のセクションで説明した手順に `task/fetch` [従って変更されました](#payload-of-taskfetch-and-tasksubmit-messages)。</span><span class="sxs-lookup"><span data-stu-id="8b07b-161">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="8b07b-162">つまり、ドキュメントは正しくありませんが、実装は正しくありません。</span><span class="sxs-lookup"><span data-stu-id="8b07b-162">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="8b07b-163">変更された変更 `// for Technical Preview [...]` については、以下のコメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="8b07b-163">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

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

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="8b07b-164">例: タスク/フェッチおよびタスク/送信の呼び出しメッセージの受信と応答 - C#</span><span class="sxs-lookup"><span data-stu-id="8b07b-164">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="8b07b-165">ボットC#、メッセージは、メッセージ `invoke` を処理する `HttpResponseMessage()` コントローラーによって処理 `Activity` されます。</span><span class="sxs-lookup"><span data-stu-id="8b07b-165">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="8b07b-166">要求 `task/fetch` と `task/submit` 応答は JSON です。</span><span class="sxs-lookup"><span data-stu-id="8b07b-166">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="8b07b-167">このC#、Node.js のように生の JSON を扱うのは便利ではないので、JSON とのシリアル化を処理するにはラッパー クラスが必要です。</span><span class="sxs-lookup"><span data-stu-id="8b07b-167">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="8b07b-168">Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)ではこれを直接サポートしていませんが、C# サンプル アプリでこれらの単純なラッパー クラスの外観[の例を確認できます](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)。</span><span class="sxs-lookup"><span data-stu-id="8b07b-168">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="8b07b-169">以下に、C# これらのラッパー クラス ( 、 、 ) を使用して処理およびメッセージを処理するコードの例を次に示します。サンプルから `task/fetch` `task/submit` `TaskInfo` `TaskEnvelope` 抜粋 [します](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)。</span><span class="sxs-lookup"><span data-stu-id="8b07b-169">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

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

<span data-ttu-id="8b07b-170">上記の例では示されていないのは、各ケースのオブジェクトの 、 、およびプロパティを設定する `SetTaskInfo()` `height` `width` `title` `TaskInfo` 関数です。</span><span class="sxs-lookup"><span data-stu-id="8b07b-170">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="8b07b-171">[SetTaskInfo() のソース コードを次に示します](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)。</span><span class="sxs-lookup"><span data-stu-id="8b07b-171">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="8b07b-172">Bot Framework カードアクションとアダプティブ カード Action.Submit アクション</span><span class="sxs-lookup"><span data-stu-id="8b07b-172">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="8b07b-173">Bot Framework カード アクションのスキーマは、アダプティブ カードアクションとは少し異 `Action.Submit` なります。</span><span class="sxs-lookup"><span data-stu-id="8b07b-173">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="8b07b-174">その結果、タスク モジュールを呼び出す方法も少し異なります。オブジェクトにはオブジェクトが含まれているので、カード内の他のプロパティに干渉 `data` `Action.Submit` `msteams` しません。</span><span class="sxs-lookup"><span data-stu-id="8b07b-174">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="8b07b-175">次の表に、それぞれの例を示します。</span><span class="sxs-lookup"><span data-stu-id="8b07b-175">The following table shows an example of each:</span></span>

| <span data-ttu-id="8b07b-176">Bot Framework カードアクション</span><span class="sxs-lookup"><span data-stu-id="8b07b-176">Bot Framework card action</span></span>                              | <span data-ttu-id="8b07b-177">アダプティブ カード Action.Submit アクション</span><span class="sxs-lookup"><span data-stu-id="8b07b-177">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="see-also"></a><span data-ttu-id="8b07b-178">関連項目</span><span class="sxs-lookup"><span data-stu-id="8b07b-178">See also</span></span>

* [<span data-ttu-id="8b07b-179">Microsoft Teams モジュールのサンプル コード — nodejs</span><span class="sxs-lookup"><span data-stu-id="8b07b-179">Microsoft Teams task module sample code — nodejs</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* <span data-ttu-id="8b07b-180">[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="8b07b-180">[Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>