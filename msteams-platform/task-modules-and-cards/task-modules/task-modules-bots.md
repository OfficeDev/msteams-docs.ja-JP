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
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Microsoft Teams のボットからのタスクモジュールの使用

タスクモジュールは、アダプティブカードおよび Bot フレームワークカード (英雄、サムネイル、および Office 365 Connector) のボタンを使用して、Microsoft Teams の bot から呼び出すことができます。 タスクモジュールは、多くの場合、開発者が bot の状態を追跡し、ユーザーがシーケンスを中断または取り消しられるようにする必要がある、複数の会話手順よりも優れたユーザー環境を提供します。

タスクモジュールを呼び出すには、次の2つの方法があります。

* **新しい種類の invoke メッセージ `task/fetch` 。** `invoke`Bot フレームワークカードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#invoke)、または `Action.Submit` アダプティブカードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)を使用すると、 `task/fetch` タスクモジュール (URL またはアダプティブカード) が bot から動的に取り出されます。
* **ディープリンク Url。** [タスクモジュールのディープリンク構文](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)を使用すると、 `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl)ボットフレームワークカード、または `Action.OpenUrl` 適応カードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)をそれぞれ使用できます。 深いリンク Url を使用すると、タスクモジュールの URL またはアダプティブカードの本文は明らかによく知られており、に対するサーバーのラウンドトリップを回避 `task/fetch` します。

>[!IMPORTANT]
>セキュリティで保護された通信を確保するために、それぞれに `url` `fallbackUrl` HTTPS 暗号化プロトコルを実装する必要があります。

## <a name="invoking-a-task-module-via-taskfetch"></a>Task/fetch を使用してタスクモジュールを呼び出す

`value`カードアクションのオブジェクトの場合、 `invoke` または `Action.Submit` 適切な方法で初期化される場合 (以下を参照)、ユーザーがボタンを押すと、 `invoke` メッセージが bot に送信されます。 メッセージに対する HTTP 応答では `invoke` 、タスクモジュールを表示するために Teams で使用される [taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) がラッパーオブジェクトに埋め込まれています。

![タスク/フェッチ要求/応答](~/assets/images/task-module/task-module-invoke-request-response.png)

各手順について、さらに詳しく説明します。

1. この例では、"Buy" カードアクションを含む Bot フレームワークの英雄カードを示し `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke)ます。 プロパティの値 `type` は、 `task/fetch` オブジェクトの残りの部分を `value` 任意のものにすることができます。
2. Bot が `invoke` HTTP POST メッセージを受信します。
3. Bot は応答オブジェクトを作成し、それを HTTP 200 応答コードを使用して POST 応答の本文に返します。 応答のスキーマについては、次の「 [タスク/送信に](#the-flexibility-of-tasksubmit)ついて」を参照してください。ここで覚えておくべき重要な点は、HTTP 応答の本文に、次のように、ラッパーオブジェクトに埋め込まれた [taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) が含まれるということです。

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

    `task/fetch`Bot に対するイベントとその応答は、概念的には `microsoftTeams.tasks.startTask()` クライアント SDK の関数に似ています。
4. Microsoft Teams では、タスクモジュールが表示されます。

## <a name="submitting-the-result-of-a-task-module"></a>タスクモジュールの結果を提出する

ユーザーがタスクモジュールで作業を終了すると、検索結果は [タブを使用](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)した場合と同じようになりますが、いくつかの違いがあるので、ここでも説明します。

* **HTML/JavaScript ( `TaskInfo.url` )**。 ユーザーが入力したことを確認したら、 `microsoftTeams.tasks.submitTask()` SDK 関数を呼び出し `submitTask()` ます (読みやすさを目的として、以降を参照)。 `submitTask()`タスクモジュールを閉じるだけの場合は、パラメーターを指定せずに呼び出すことができますが、ほとんどの場合、オブジェクトまたは文字列をに渡すことが必要になり `submitHandler` ます。 単にこれを最初のパラメーターとして渡し `result` ます。 Teams が呼び出す `submitHandler` : はになり、 `err` 渡され `null` `result` たオブジェクト/文字列になり `submitTask()` ます。 パラメーターを指定して呼び出しを行う場合 `submitTask()` `result` は、または文字列の配列を渡す **必要があり** `appId` `appId` ます。これにより、チームは、結果を送信しているアプリがタスクモジュールを呼び出したものと同じであることを確認できます。 Bot は、次に `task/submit` 示すようなメッセージを受け取り `result` ます。 [below](#payload-of-taskfetch-and-tasksubmit-messages)
* **アダプティブカード ( `TaskInfo.card` )**。 ユーザーが任意のボタンを押したときに、ユーザーが入力したアダプティブカードの本文が、メッセージによって bot に送信され `task/submit` `Action.Submit` ます。

## <a name="the-flexibility-of-tasksubmit"></a>タスク/提出の柔軟性

前のセクションでは、ユーザーが bot から呼び出されたタスクモジュールで終了すると、bot は常にメッセージを受信することを学びました `task/submit invoke` 。 開発者は、メッセージに *応答* するときにいくつかのオプションを使用でき `task/submit` ます。

| HTTP 本文の応答                      | シナリオ                                |
| --------------------------------------- | --------------------------------------- |
| なし (メッセージを無視します `task/submit` ) | 最も単純な応答は、まったく応答がありません。 ユーザーがタスクモジュールで作業を終了すると、bot は応答する必要はありません。 |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | の値は、Teams によって `value` ポップアップメッセージボックスに表示されます。 |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | 1つのウィザード/複数ステップの画面で、アダプティブカードのシーケンスを "チェーン" することができます。 _アダプティブカードをシーケンスにチェーンすることは高度なシナリオで、ここでは文書化されていません。Node.js サンプルアプリはこれをサポートしていますが、その機能が [README.md ファイル](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)に記載されています。_ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>タスク/フェッチおよびタスク/送信メッセージのペイロード

このセクションでは、bot が、または bot フレームワークオブジェクトを受け取ったときに、bot が受け取る内容のスキーマを定義 `task/fetch` `task/submit` `Activity` します。 重要な最上位レベルは下に表示されます。

| プロパティ | 説明                          |
| -------- | ------------------------------------ |
| `type`   | は常に `invoke`              |
| `name`   | `task/fetch`あるいは`task/submit` |
| `value`  | 開発者が定義したペイロード。 通常、オブジェクトの構造は `value` Teams から送信されたものを反映します。 ただし、この場合は、 `task/fetch` Bot フレームワーク () とアダプティブカードアクション () の両方から動的な fetch () をサポートし、 `value` `Action.Submit` `data` `context` に含まれていたものに加えて Teams を bot に伝達する方法が必要になり `value` / `data` ます。<br/><br/>これを行うには、2つを親オブジェクトに結合します。<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>例: タスク/フェッチおよびタスク/送信呼び出しメッセージの受信と応答 Node.js

> [!NOTE]
> 次に示すサンプルコードは、この機能の Technical Preview と最終リリースの間で変更されました。要求のスキーマは、 `task/fetch` [前のセクションで説明](#payload-of-taskfetch-and-tasksubmit-messages)した内容に従って変更されました。 つまり、ドキュメントは修正されましたが、実装はできませんでした。 変更点については、次のコメントを参照してください `// for Technical Preview [...]` 。

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
## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>例: タスク/フェッチおよびタスク/送信呼び出しメッセージを受信して応答する-C#

C# bot では、メッセージ `invoke` はメッセージを処理するコントローラーによって処理され `HttpResponseMessage()` `Activity` ます。 `task/fetch`との `task/submit` 要求と応答は JSON です。 C# では、Node.js のように raw JSON を処理するのは便利ではありません。したがって、JSON とのシリアル化を処理するには、ラッパークラスが必要です。 このことは、Microsoft Teams の [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) で直接サポートされていませんが、これらの簡単なラッパークラスが [C# サンプルアプリ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)でどのように表示されるかの例を確認できます。

以下は、 `task/fetch` `task/submit` これらのラッパークラス (,) を使用して、次のようなコードを処理およびメッセージを処理するための C# のコード例です `TaskInfo` `TaskEnvelope` 。 excerpted [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)のコードは次のとおりです。

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
## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---python"></a>例: タスク/フェッチおよびタスク/送信呼び出しメッセージを受信して応答する-Python
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
### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Bot フレームワークカードアクションとアダプティブカードアクションの送信アクション

Bot フレームワークカードアクションのスキーマは、アダプティブカードアクションとは少し異なり `Action.Submit` ます。 そのため、タスクモジュールを呼び出す方法は少し異なります。オブジェクトが `data` 含まれているオブジェクトには、 `Action.Submit` `msteams` カード内の他のプロパティに干渉しないようにします。 次の表は、それぞれの例を示しています。

| Bot フレームワークカードアクション                              | アダプティブカードアクションの送信アクション                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
