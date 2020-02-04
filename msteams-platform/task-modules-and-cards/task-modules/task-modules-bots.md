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
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Microsoft Teams のボットからのタスクモジュールの使用

タスクモジュールは、アダプティブカードおよび Bot フレームワークカード (英雄、サムネイル、および Office 365 Connector) のボタンを使用して、Microsoft Teams の bot から呼び出すことができます。 タスクモジュールは、多くの場合、開発者が bot の状態を追跡し、ユーザーがシーケンスを中断または取り消しられるようにする必要がある、複数の会話手順よりも優れたユーザー環境を提供します。

タスクモジュールを呼び出すには、次の2つの方法があります。

* **新しい種類の invoke メッセージ`task/fetch`。** `invoke` Bot フレームワークカードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#invoke)、または`Action.Submit`アダプティブカードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)を使用すると`task/fetch`、タスクモジュール (URL またはアダプティブカード) が bot から動的に取り出されます。
* **ディープリンク Url。** [タスクモジュールのディープリンク構文](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)を使用すると、ボットフレームワーク`openUrl`カード、また`Action.OpenUrl`は適応カードの[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)[をそれぞれ](~/task-modules-and-cards/cards/cards-actions.md#openurl)使用できます。 深いリンク Url を使用すると、タスクモジュールの URL またはアダプティブカードの本文は明らかによく知られており、 `task/fetch`に対するサーバーのラウンドトリップを回避します。

## <a name="invoking-a-task-module-via-taskfetch"></a>Task/fetch を使用してタスクモジュールを呼び出す

カードアクション`value`のオブジェクトの場合、また`Action.Submit`は適切な方法で初期化される場合 (以下を参照)、ユーザーがボタンを押すと`invoke` 、メッセージが bot に送信されます。 `invoke` `invoke`メッセージに対する HTTP 応答では、タスクモジュールを表示するために Teams で使用される[taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)がラッパーオブジェクトに埋め込まれています。

![タスク/フェッチ要求/応答](~/assets/images/task-module/task-module-invoke-request-response.png)

各手順について、さらに詳しく説明します。

1. この例では、"Buy" `invoke` [カードアクション](~/task-modules-and-cards/cards/cards-actions.md#invoke)を含む Bot フレームワークの英雄カードを示します。 `type`プロパティの値は`task/fetch` 、 `value`オブジェクトの残りの部分を任意のものにすることができます。
2. Bot が HTTP POST `invoke`メッセージを受信します。
3. Bot は応答オブジェクトを作成し、それを HTTP 200 応答コードを使用して POST 応答の本文に返します。 応答のスキーマについては、次の「[タスク/送信に](#the-flexibility-of-tasksubmit)ついて」を参照してください。ここで覚えておくべき重要な点は、HTTP 応答の本文に、次のように、ラッパーオブジェクトに埋め込まれた[taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)が含まれるということです。

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
    
    Bot `task/fetch`に対するイベントとその応答は、概念的にはクライアント SDK `microsoftTeams.tasks.startTask()`の関数に似ています。
4. Microsoft Teams では、タスクモジュールが表示されます。

## <a name="submitting-the-result-of-a-task-module"></a>タスクモジュールの結果を提出する

ユーザーがタスクモジュールで作業を終了すると、検索結果は[タブを使用](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)した場合と同じようになりますが、いくつかの違いがあるので、ここでも説明します。

* **HTML/JavaScript (`TaskInfo.url`)**。 ユーザーが入力したことを確認したら、 `microsoftTeams.tasks.submitTask()` SDK 関数を呼び出します (読みやすさを`submitTask()`目的として、以降を参照)。 タスクモジュールを`submitTask()`閉じるだけの場合は、パラメーターを指定せずに呼び出すことができ`submitHandler`ますが、ほとんどの場合、オブジェクトまたは文字列をに渡すことが必要になります。 単にこれを`result`最初のパラメーターとして渡します。 Teams が呼び出す`submitHandler`: `err` `null` `result`はに`submitTask()`なり、渡されたオブジェクト/文字列になります。 `result`パラメーターを指定し`submitTask()`て呼び出しを行う場合`appId`は、または文字列の`appId`配列を渡す**必要があり**ます。これにより、チームは、結果を送信しているアプリがタスクモジュールを呼び出したものと同じであることを確認できます。 Bot は、[次](#payload-of-taskfetch-and-tasksubmit-messages)に`task/submit`示す`result`ようなメッセージを受け取ります。
* **アダプティブカード (`TaskInfo.card`)**。 ユーザーが任意`Action.Submit`のボタンを押したときに、ユーザーが入力したアダプティブカードの本文`task/submit`が、メッセージによって bot に送信されます。

## <a name="the-flexibility-of-tasksubmit"></a>タスク/提出の柔軟性

前のセクションでは、ユーザーが bot から呼び出されたタスクモジュールで終了すると、bot は常にメッセージを`task/submit invoke`受信することを学びました。 開発者は、 `task/submit`メッセージに*応答*するときにいくつかのオプションを使用できます。

| HTTP 本文の応答                      | シナリオ                                |
| --------------------------------------- | --------------------------------------- |
| なし (メッセージを`task/submit`無視します) | 最も単純な応答は、まったく応答がありません。 ユーザーがタスクモジュールで作業を終了すると、bot は応答する必要はありません。 |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | の`value`値は、Teams によってポップアップメッセージボックスに表示されます。 |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | 1つのウィザード/複数ステップの画面で、アダプティブカードのシーケンスを "チェーン" することができます。 _アダプティブカードをシーケンスにチェーンすることは高度なシナリオで、ここでは文書化されていません。Node.js サンプルアプリは、これをサポートしていますが、その機能が[README.md ファイル](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)に記載されているかどうかについて説明します。_ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>タスク/フェッチおよびタスク/送信メッセージのペイロード

このセクションでは、bot が、または`task/fetch` `task/submit` bot フレームワーク`Activity`オブジェクトを受け取ったときに、bot が受け取る内容のスキーマを定義します。 重要な最上位レベルは下に表示されます。

| プロパティ | 説明                          |
| -------- | ------------------------------------ |
| `type`   | は常に`invoke`              |
| `name`   | `task/fetch`あるいは`task/submit` |
| `value`  | 開発者が定義したペイロード。 通常、 `value`オブジェクトの構造は Teams から送信されたものを反映します。 ただし`task/fetch`、この場合は、bot フレームワーク (`value`) とアダプティブカード`Action.Submit`アクション (`data`) の両方から動的な fetch () をサポートし、に`context` `value` / `data`含まれていたものに加えて Teams を bot に伝達する方法が必要になります。<br/><br/>これを行うには、2つを親オブジェクトに結合します。<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>例: タスク/フェッチおよびタスク/送信呼び出しメッセージの受信と応答-node.js

Bot フレームワーク`invoke`でのメッセージの処理は、BOT フレームワーク SDK では正式にサポートされていないため、少し厄介になることがあります。 これを簡単にするために、 `onInvoke()`チームは botbuilder npm パッケージでヘルパー関数を作成しました[(node.js の場合)](https://www.npmjs.com/package/botbuilder-teams)。 次の例は、その方法を示しています。

> [!NOTE]
> 次に示すサンプルコードは、この機能の Technical Preview と最終リリースの間で変更さ`task/fetch`れました。要求のスキーマは、[前のセクションで説明](#payload-of-taskfetch-and-tasksubmit-messages)した内容に従って変更されました。 つまり、ドキュメントは修正されましたが、実装はできませんでした。 変更点`// for Technical Preview [...]`については、次のコメントを参照してください。

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

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>例: タスク/フェッチおよびタスク/送信呼び出しメッセージを受信して応答する-C#

C# bot では`invoke` 、メッセージは`Activity`メッセージを`HttpResponseMessage()`処理するコントローラーによって処理されます。 と`task/fetch` `task/submit`の要求と応答は JSON です。 C# では、JSON の場合と同様に、生の JSON を処理することはできません。そのため、JSON とのシリアル化を処理するラッパークラスが必要です。 このことは、Microsoft Teams の[C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)で直接サポートされていませんが、これらの簡単なラッパークラスが[C# サンプルアプリ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)でどのように表示されるかの例を確認できます。

以下は、これらのラッパークラス ( `task/fetch` `task/submit` `TaskInfo`, `TaskEnvelope`) を使用して、次のようなコードを処理およびメッセージを処理するための C# のコード例です。 excerpted のコード[は次の](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)とおりです。

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

上記の例に示されてい`SetTaskInfo()`ない関数は、各`height`case `width`の`TaskInfo`オブジェクト`title`の、、およびプロパティを設定します。 [SetTaskInfo () のソースコード](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)を次に示します。

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Bot フレームワークカードアクションとアダプティブカードアクションの送信アクション

Bot フレームワークカードアクションのスキーマは、アダプティブカード`Action.Submit`アクションとは少し異なります。 そのため、タスクモジュールを呼び出す方法は少し異なります。オブジェクトが`data`含まれ`Action.Submit` `msteams`ているオブジェクトには、カード内の他のプロパティに干渉しないようにします。 次の表は、それぞれの例を示しています。

| Bot フレームワークカードアクション                              | アダプティブカードアクションの送信アクション                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
