---
title: Microsoft Teamsボットでのタスクモジュールの使用
description: ボット フレームワーク カード、アダプティブ カード、ディープ リンクなど、Microsoft Teams ボットでタスク モジュールを使用する方法
localization_priority: Normal
ms.topic: how-to
keywords: タスク モジュール チーム ボット
ms.openlocfilehash: bfaf3dfe791c1736aeb418e2689e513908f04534
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566570"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="09fcc-104">Microsoft Teamsボットのタスクモジュールの使用</span><span class="sxs-lookup"><span data-stu-id="09fcc-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="09fcc-105">タスク モジュールは、アダプティブ カードと Bot フレームワーク カード (ヒーロー、サムネイル、およびOffice 365 コネクタ) のボタンを使用して、Microsoft Teams ボットから呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="09fcc-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="09fcc-106">タスクモジュールは、多くの場合、開発者がボットの状態を追跡し、ユーザーがシーケンスを中断/キャンセルできるようにする複数の会話ステップよりも優れたユーザーエクスペリエンスです。</span><span class="sxs-lookup"><span data-stu-id="09fcc-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="09fcc-107">タスクモジュールを呼び出す方法は2つあります。</span><span class="sxs-lookup"><span data-stu-id="09fcc-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="09fcc-108">**新しい種類の呼び出しメッセージ `task/fetch` 。**</span><span class="sxs-lookup"><span data-stu-id="09fcc-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="09fcc-109">Bot `invoke` Framework [カードのカード アクション](~/task-modules-and-cards/cards/cards-actions.md#invoke) 、または `Action.Submit` アダプティブ カードの [カード アクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) を使用して、タスク `task/fetch` モジュール (URL またはアダプティブ カード) を使用すると、ボットから動的に取得されます。</span><span class="sxs-lookup"><span data-stu-id="09fcc-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="09fcc-110">**ディープ リンク URL。**</span><span class="sxs-lookup"><span data-stu-id="09fcc-110">**Deep link URLs.**</span></span> <span data-ttu-id="09fcc-111">タスク [モジュールのディープ リンク構文](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)を使用して `openUrl` 、Bot Framework [カードのカード アクション](~/task-modules-and-cards/cards/cards-actions.md#openurl) 、または `Action.OpenUrl` アダプティブ カードの [カード アクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) をそれぞれ使用できます。</span><span class="sxs-lookup"><span data-stu-id="09fcc-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="09fcc-112">ディープ リンク URL を使用すると、タスク モジュール URL またはアダプティブ カード本文は明らかに事前に知られており、サーバーの往復を回避 `task/fetch` します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

>[!IMPORTANT]
><span data-ttu-id="09fcc-113">通信のセキュリティを確保するために、各プロトコル `url` は `fallbackUrl` HTTPS 暗号化プロトコルを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="09fcc-113">To ensure secure communications, each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

## <a name="invoking-a-task-module-through-taskfetch"></a><span data-ttu-id="09fcc-114">タスク/フェッチを使用したタスク・モジュールの呼び出し</span><span class="sxs-lookup"><span data-stu-id="09fcc-114">Invoking a task module through task/fetch</span></span>

<span data-ttu-id="09fcc-115">`value` `invoke` カードアクションのオブジェクトまたは `Action.Submit` 適切な方法で初期化されると(詳細は後述)、ユーザーがボタンを押すと `invoke` 、ボットにメッセージが送信されます。</span><span class="sxs-lookup"><span data-stu-id="09fcc-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="09fcc-116">メッセージに対する HTTP 応答には `invoke` 、タスク モジュールの表示に使用Teamsラッパー オブジェクトに[TaskInfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)が埋め込まれています。</span><span class="sxs-lookup"><span data-stu-id="09fcc-116">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![タスク/フェッチ要求/応答](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="09fcc-118">各ステップをもう少し詳しく見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="09fcc-118">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="09fcc-119">この例では、"購入" カード アクションを持つボット フレームワーク ヒーロー `invoke` [カード](~/task-modules-and-cards/cards/cards-actions.md#invoke)を示します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-119">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="09fcc-120">プロパティの値 `type` は `task/fetch` - オブジェクトの残りの部分 `value` は、あなたが好きなものにすることができます。</span><span class="sxs-lookup"><span data-stu-id="09fcc-120">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
1. <span data-ttu-id="09fcc-121">ボットは HTTP `invoke` POST メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-121">The bot receives the `invoke` HTTP POST message.</span></span>
1. <span data-ttu-id="09fcc-122">ボットは応答オブジェクトを作成し、HTTP 200 応答コードを使用して POST 応答の本文に返します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="09fcc-123">応答のスキーマは [、タスク/送信に関する説明で後述](#the-flexibility-of-tasksubmit)しますが、ここで覚えておくべきことは、HTTP 応答の本文にラッパー オブジェクトに埋め込まれた [TaskInfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) が含まれていることです。</span><span class="sxs-lookup"><span data-stu-id="09fcc-123">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object.</span></span> <span data-ttu-id="09fcc-124">例:</span><span class="sxs-lookup"><span data-stu-id="09fcc-124">For example:</span></span>

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

    <span data-ttu-id="09fcc-125">`task/fetch`ボットのイベントとその応答は、概念的には `microsoftTeams.tasks.startTask()` 、クライアント SDK の関数と似ています。</span><span class="sxs-lookup"><span data-stu-id="09fcc-125">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
1. <span data-ttu-id="09fcc-126">Microsoft Teamsタスク モジュールが表示されます。</span><span class="sxs-lookup"><span data-stu-id="09fcc-126">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="09fcc-127">タスク モジュールの結果の送信</span><span class="sxs-lookup"><span data-stu-id="09fcc-127">Submitting the result of a task module</span></span>

<span data-ttu-id="09fcc-128">ユーザーがタスク モジュールを終了すると、ボットに結果を戻す方法はタブ との [動作に](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)似ていますが、いくつかの違いがあるので、ここでも説明します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-128">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="09fcc-129">**HTML/JavaScript ( `TaskInfo.url` )**</span><span class="sxs-lookup"><span data-stu-id="09fcc-129">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="09fcc-130">ユーザーが入力した内容を検証したら、SDK 関数を呼び出します `microsoftTeams.tasks.submitTask()` (ここでは `submitTask()` 読みやすさを目的として参照)。</span><span class="sxs-lookup"><span data-stu-id="09fcc-130">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="09fcc-131">`submitTask()`タスク モジュールを閉じるTeams場合はパラメータなしで呼び出すことができますが、ほとんどの場合はオブジェクトまたは文字列をに渡します `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="09fcc-131">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="09fcc-132">最初のパラメータとして渡すだけです `result` 。</span><span class="sxs-lookup"><span data-stu-id="09fcc-132">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="09fcc-133">Teamsは `submitHandler` 、 に `err` `null` `result` 渡したオブジェクト/文字列になります `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="09fcc-133">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="09fcc-134">パラメーターを指定して呼び出す場合 `submitTask()` `result` は、 または文字列の配列を渡す **必要があります** `appId` `appId` Teams。</span><span class="sxs-lookup"><span data-stu-id="09fcc-134">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="09fcc-135">ボットには、以下の `task/submit` 説明を含むメッセージ `result` が表示 [されます](#payload-of-taskfetch-and-tasksubmit-messages)。</span><span class="sxs-lookup"><span data-stu-id="09fcc-135">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="09fcc-136">**アダプティブ カード ( `TaskInfo.card` )**。</span><span class="sxs-lookup"><span data-stu-id="09fcc-136">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="09fcc-137">ユーザーがボタンを押すと、アダプティブ カード本体 (ユーザーが入力した状態) がメッセージを介してボットに送信されます `task/submit` `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="09fcc-137">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="09fcc-138">タスク/提出の柔軟性</span><span class="sxs-lookup"><span data-stu-id="09fcc-138">The flexibility of task/submit</span></span>

<span data-ttu-id="09fcc-139">前のセクションでは、ボットから呼び出されたタスク モジュールでユーザーが終了すると、ボットは常にメッセージを受信することを学習しました `task/submit invoke` 。</span><span class="sxs-lookup"><span data-stu-id="09fcc-139">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="09fcc-140">開発者は、メッセージに *応答* する際に、いくつかのオプションがあります `task/submit` 。</span><span class="sxs-lookup"><span data-stu-id="09fcc-140">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="09fcc-141">HTTP 本文応答</span><span class="sxs-lookup"><span data-stu-id="09fcc-141">HTTP Body Response</span></span>                      | <span data-ttu-id="09fcc-142">シナリオ</span><span class="sxs-lookup"><span data-stu-id="09fcc-142">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="09fcc-143">なし (メッセージを無視 `task/submit` )</span><span class="sxs-lookup"><span data-stu-id="09fcc-143">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="09fcc-144">最も簡単な応答は、まったく応答しません。</span><span class="sxs-lookup"><span data-stu-id="09fcc-144">The simplest response is no response at all.</span></span> <span data-ttu-id="09fcc-145">ユーザーがタスク モジュールを使い終えたら、ボットが応答する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="09fcc-145">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="09fcc-146">Teamsポップアップ メッセージ ボックスに の値 `value` が表示されます。</span><span class="sxs-lookup"><span data-stu-id="09fcc-146">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="09fcc-147">ウィザード/マルチステップエクスペリエンスでアダプティブカードのシーケンスを一緒に"連鎖"することができます。</span><span class="sxs-lookup"><span data-stu-id="09fcc-147">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="09fcc-148">_Adaptive カードをシーケンスにチェーンすることは高度なシナリオであり、ここでは文書化されていない点に注意してください。ただし、Node.jsサンプルアプリはそれをサポートしており、その動作方法は README.md [ファイルに記載されています](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)。_</span><span class="sxs-lookup"><span data-stu-id="09fcc-148">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="09fcc-149">タスク/フェッチおよびタスク/送信メッセージのペイロード</span><span class="sxs-lookup"><span data-stu-id="09fcc-149">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="09fcc-150">このセクションでは、ボットがまたは Bot Framework オブジェクトを受け取ったときに、ボットが受け取る内容のスキーマを定義 `task/fetch` `task/submit` `Activity` します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-150">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="09fcc-151">重要なトップレベルは以下に示されます。</span><span class="sxs-lookup"><span data-stu-id="09fcc-151">The important top-level appear below:</span></span>

| <span data-ttu-id="09fcc-152">プロパティ</span><span class="sxs-lookup"><span data-stu-id="09fcc-152">Property</span></span> | <span data-ttu-id="09fcc-153">説明</span><span class="sxs-lookup"><span data-stu-id="09fcc-153">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="09fcc-154">常に `invoke`</span><span class="sxs-lookup"><span data-stu-id="09fcc-154">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="09fcc-155">`task/fetch`または`task/submit`</span><span class="sxs-lookup"><span data-stu-id="09fcc-155">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="09fcc-156">開発者が定義したペイロード。</span><span class="sxs-lookup"><span data-stu-id="09fcc-156">The developer-defined payload.</span></span> <span data-ttu-id="09fcc-157">通常、オブジェクトの構造 `value` は、Teamsから送信されたものをミラー化します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-157">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="09fcc-158">しかし、この場合は、Bot Framework ( ) と Adaptive カード アクション ( ) の両方からの動的フェッチ ( ) をサポートする必要 `task/fetch` `value` `Action.Submit` `data` Teamsがあるため、この方法は異なります `context` `value` / `data` 。</span><span class="sxs-lookup"><span data-stu-id="09fcc-158">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="09fcc-159">これを行うには、2 つを親オブジェクトに結合します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-159">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="09fcc-160">例: タスク/フェッチおよびタスク/送信の呼び出しメッセージの受信と応答 - Node.js</span><span class="sxs-lookup"><span data-stu-id="09fcc-160">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

> [!NOTE]
> <span data-ttu-id="09fcc-161">以下のサンプル コードは、テクニカル プレビューとこの機能の最終リリースの間に変更されました: 要求のスキーマ `task/fetch` は [、前のセクションで説明](#payload-of-taskfetch-and-tasksubmit-messages)した内容に従うように変更されました。</span><span class="sxs-lookup"><span data-stu-id="09fcc-161">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="09fcc-162">つまり、ドキュメントは正しかったが、実装は正しくなかった。</span><span class="sxs-lookup"><span data-stu-id="09fcc-162">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="09fcc-163">変更された `// for Technical Preview [...]` 内容については、以下のコメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="09fcc-163">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

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

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="09fcc-164">例: タスク/フェッチおよびタスク/送信呼び出しメッセージの受信と応答 - C#</span><span class="sxs-lookup"><span data-stu-id="09fcc-164">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="09fcc-165">C# ボットでは、 `invoke` メッセージはメッセージを処理するコント ローラーによって処理されます `HttpResponseMessage()` `Activity` 。</span><span class="sxs-lookup"><span data-stu-id="09fcc-165">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="09fcc-166">`task/fetch`および `task/submit` 要求と応答は JSON です。</span><span class="sxs-lookup"><span data-stu-id="09fcc-166">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="09fcc-167">C# では、Node.jsのように生の JSON を扱うのも便利ではないので、JSON との間でシリアル化を処理するラッパー クラスが必要です。</span><span class="sxs-lookup"><span data-stu-id="09fcc-167">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="09fcc-168">Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)では、この機能に対する直接的なサポートはまだありませんが[、C# サンプル アプリ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)でこれらの単純なラッパー クラスの例を示します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-168">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="09fcc-169">次に、C# での処理用のコード例 `task/fetch` と `task/submit` 、サンプルから抜粋したこれらのラッパー クラス ( `TaskInfo` , `TaskEnvelope` )を使用したメッセージの [処理例を示](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-169">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

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

<span data-ttu-id="09fcc-170">上の例では示されていない関数は `SetTaskInfo()` 、 `height` `width` `title` 各ケースのオブジェクトの 、、、、およびプロパティを設定 `TaskInfo` します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-170">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="09fcc-171">次に [、SetTaskInfo() のソース コードを](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)示します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-171">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="09fcc-172">ボット フレームワーク カード アクションとアダプティブ カード アクションの対</span><span class="sxs-lookup"><span data-stu-id="09fcc-172">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="09fcc-173">Bot Framework カード アクションのスキーマは、アダプティブ カード アクションとは少し異なります `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="09fcc-173">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="09fcc-174">その結果、タスクモジュールを呼び出す方法も少し異なります: `data` オブジェクト `Action.Submit` が含まれているので `msteams` 、カード内の他のプロパティに干渉しません。</span><span class="sxs-lookup"><span data-stu-id="09fcc-174">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="09fcc-175">次の表に、それぞれの例を示します。</span><span class="sxs-lookup"><span data-stu-id="09fcc-175">The following table shows an example of each:</span></span>

| <span data-ttu-id="09fcc-176">ボット フレームワーク カード アクション</span><span class="sxs-lookup"><span data-stu-id="09fcc-176">Bot Framework card action</span></span>                              | <span data-ttu-id="09fcc-177">アダプティブ カード アクション.Submit アクション</span><span class="sxs-lookup"><span data-stu-id="09fcc-177">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="see-also"></a><span data-ttu-id="09fcc-178">関連項目</span><span class="sxs-lookup"><span data-stu-id="09fcc-178">See also</span></span>

* [<span data-ttu-id="09fcc-179">Microsoft Teamsタスク モジュールサンプル コード — nodejs</span><span class="sxs-lookup"><span data-stu-id="09fcc-179">Microsoft Teams task module sample code — nodejs</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* <span data-ttu-id="09fcc-180">[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="09fcc-180">[Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>