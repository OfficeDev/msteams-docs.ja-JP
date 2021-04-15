---
title: Microsoft Teams ボットでのタスク モジュールの使用
description: ボット フレームワーク カード、アダプティブ カード、ディープ リンクなど、Microsoft Teams ボットでタスク モジュールを使用する方法。
ms.topic: how-to
keywords: タスク モジュールのチーム ボット
ms.openlocfilehash: d87b55bf202184f315abf69dfc34fc4db9125c4f
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696473"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Microsoft Teams ボットからのタスク モジュールの使用

タスク モジュールは、アダプティブ カードとボット フレームワーク カード (ヒーロー、サムネイル、および 365 コネクタ) のボタンを使用して、Microsoft Teams Office呼び出すことができます。 多くの場合、タスク モジュールは、開発者がボットの状態を追跡し、ユーザーがシーケンスを中断/取り消す必要がある複数の会話手順よりも優れたユーザー エクスペリエンスです。

タスク モジュールを呼び出す方法は 2 通りあります。

* **新しい種類の呼び出しメッセージ `task/fetch` 。** Bot Framework カードのカード アクション、またはアダプティブ カードのカード アクションを使用すると、タスク モジュール (URL またはアダプティブ カード) がボットから動的に `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` フェッチされます。
* **ディープ リンク URL。** タスク モジュール[のディープ リンク構文を](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)使用すると、Bot Framework カードのカード アクション、アダプティブ カードのカード アクションをそれぞれ `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)使用できます。 ディープ リンク URL では、タスク モジュールの URL またはアダプティブ カードの本文が事前に明らかに知られているので、サーバーのラウンドトリップは避けます `task/fetch` 。

>[!IMPORTANT]
>安全な通信を確保するには、HTTPS `url` `fallbackUrl` 暗号化プロトコルを実装する必要があります。

## <a name="invoking-a-task-module-via-taskfetch"></a>タスク/フェッチによるタスク モジュールの呼び出し

カードアクションのオブジェクトが適切な方法で初期化されている場合 (以下で詳しく説明します)、ユーザーがボタンを押すと、メッセージがボット `value` `invoke` `Action.Submit` `invoke` に送信されます。 メッセージに対する HTTP 応答には、ラッパー オブジェクトに TaskInfo オブジェクトが埋め込まれているので、Teams はタスク モジュールの表示 `invoke` に使用します。 [](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)

![task/fetch request/response](~/assets/images/task-module/task-module-invoke-request-response.png)

各手順についてもう少し詳しく見てみます。

1. 次の使用例は、"Buy" カードアクションを持つ Bot Framework Hero `invoke` [カードを示しています](~/task-modules-and-cards/cards/cards-actions.md#invoke)。 プロパティの値 `type` は、 `task/fetch` - オブジェクトの残りの `value` 部分は、好きなものは何でもできます。
2. ボットは HTTP `invoke` POST メッセージを受信します。
3. ボットは応答オブジェクトを作成し、HTTP 200 応答コードを使用して POST 応答の本文に返します。 応答のスキーマについては [、task/submit](#the-flexibility-of-tasksubmit)に関するディスカッションで以下に説明しますが、ここで覚えておく必要がある重要な点は、HTTP 応答の本文にラッパー オブジェクトに埋め込まれた [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) オブジェクトが含まれていることです。たとえば、次のようにします。

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

    ボット `task/fetch` のイベントとその応答は、概念的には、クライアント SDK `microsoftTeams.tasks.startTask()` の関数と似ています。
4. Microsoft Teams はタスク モジュールを表示します。

## <a name="submitting-the-result-of-a-task-module"></a>タスク モジュールの結果の送信

ユーザーがタスク モジュールを終了すると、ボットに結果を送信し戻すのは、タブ[](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)の動作と似ていますが、いくつかの違いがあります。ここではも説明します。

* **HTML/JavaScript ( `TaskInfo.url` ) 。** ユーザーが入力した情報を検証したら、SDK 関数を呼び出します (以下、読みやすさの目的 `microsoftTeams.tasks.submitTask()` `submitTask()` で呼び出します)。 Teams でタスク モジュールを閉じるだけで、ほとんどの場合、オブジェクトまたは文字列を自分のタスク モジュールに渡す必要がある場合は、パラメーターを指定せずに `submitTask()` 呼び出します `submitHandler` 。 単に最初のパラメーターとして渡します `result` 。 Teams は `submitHandler` 次のように呼 `err` び出し `null` 、 `result` 渡したオブジェクト/文字列になります `submitTask()` 。 パラメーターを使用して呼び出す場合は、文字列または文字列の配列を渡す必要があります。これにより、Teams は、結果を送信するアプリがタスク モジュールを呼び出したアプリと同じことを検証 `submitTask()` `result`  `appId` `appId` できます。 ボットは、以下の説明 `task/submit` を含む `result` メッセージを受信 [します](#payload-of-taskfetch-and-tasksubmit-messages)。
* **アダプティブ カード ( `TaskInfo.card` ) 。** アダプティブ カード本文 (ユーザーが入力した場合) は、ユーザーがボタンを押すと、メッセージを介してボット `task/submit` に送信 `Action.Submit` されます。

## <a name="the-flexibility-of-tasksubmit"></a>タスク/送信の柔軟性

前のセクションでは、ユーザーがボットから呼び出されたタスク モジュールを終了すると、ボットは常にメッセージを受信する方法について説明 `task/submit invoke` しました。 開発者は、メッセージに応答するときに *いくつかのオプション* があります `task/submit` 。

| HTTP 本文の応答                      | シナリオ                                |
| --------------------------------------- | --------------------------------------- |
| なし (メッセージを `task/submit` 無視する) | 最も単純な応答は応答なしです。 ユーザーがタスク モジュールを使い終わったときにボットが応答する必要はありません。 |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams はポップアップ メッセージ ボックスに `value` 値を表示します。 |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | ウィザード/マルチステップ エクスペリエンスでアダプティブ カードのシーケンスを一緒に "チェーン" できます。 _アダプティブ カードをシーケンスにチェーン化する方法は高度なシナリオであり、ここでは説明しません。ただしNode.jsサンプル アプリではサポートされ、その動作方法は、そのサンプル ファイルに [README.md されます](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)。_ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>タスク/フェッチおよびタスク/送信メッセージのペイロード

このセクションでは、ボットがボットまたは Bot Framework オブジェクトを受信するときに受け取るスキーマ `task/fetch` `task/submit` を定義 `Activity` します。 重要なトップ レベルは、以下に表示されます。

| プロパティ | 説明                          |
| -------- | ------------------------------------ |
| `type`   | 常に `invoke`              |
| `name`   | どちらか `task/fetch` または `task/submit` |
| `value`  | 開発者定義のペイロード。 通常、オブジェクトの構造 `value` は Teams から送信されたデータをミラー化します。 ただし、この場合は、ボット フレームワーク ( ) とアダプティブ カードアクション ( ) の両方から動的フェッチ ( ) をサポートする必要があります。また、 に含まれるものに加えて Teams をボットに通信する方法が必要なので、異なります。 `task/fetch` `value` `Action.Submit` `data` `context` `value` / `data`<br/><br/>これを行うには、2 つを親オブジェクトに結合します。<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>例: タスク/フェッチおよびタスク/送信の呼び出しメッセージの受信と応答 - Node.js

> [!NOTE]
> 次のサンプル コードは、テクニカル プレビューとこの機能の最終リリースの間で変更されました。要求のスキーマは、前のセクションで説明した手順に `task/fetch` [従って変更されました](#payload-of-taskfetch-and-tasksubmit-messages)。 つまり、ドキュメントは正しくありませんが、実装は正しくありません。 変更された変更 `// for Technical Preview [...]` については、以下のコメントを参照してください。

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

*「Microsoft* [Teams タスク モジュールのサンプル コード — nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) と Bot Framework の  [サンプル」も参照してください](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>例: タスク/フェッチおよびタスク/送信の呼び出しメッセージの受信と応答 - C#

ボットC#、メッセージは、メッセージ `invoke` を処理する `HttpResponseMessage()` コントローラーによって処理 `Activity` されます。 要求 `task/fetch` と `task/submit` 応答は JSON です。 このC#、Node.js のように生の JSON を扱うのは便利ではないので、JSON とのシリアル化を処理するにはラッパー クラスが必要です。 Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) では、これを直接サポートしていませんが、これらの単純なラッパー クラスが C# サンプル アプリでどのような外観を示すのかを示 [す例を確認できます](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)。

以下に、C# これらのラッパー クラス ( 、 、 ) を使用して処理およびメッセージを処理するコードの例を次に示します。サンプルから `task/fetch` `task/submit` `TaskInfo` `TaskEnvelope` 抜粋 [します](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)。

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

上記の例では示されていないのは、各ケースのオブジェクトの 、 、およびプロパティを設定する `SetTaskInfo()` `height` `width` `title` `TaskInfo` 関数です。 [SetTaskInfo() のソース コードを次に示します](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)。

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Bot Framework カードアクションとアダプティブ カード Action.Submit アクション

Bot Framework カード アクションのスキーマは、アダプティブ カードアクションとは少し異 `Action.Submit` なります。 その結果、タスク モジュールを呼び出す方法も少し異なります。オブジェクトにはオブジェクトが含まれているので、カード内の他のプロパティに干渉 `data` `Action.Submit` `msteams` しません。 次の表に、それぞれの例を示します。

| Bot Framework カードアクション                              | アダプティブ カード Action.Submit アクション                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
