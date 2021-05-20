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
# <a name="using-task-modules-from-microsoft-teams-bots"></a>Microsoft Teamsボットのタスクモジュールの使用

タスク モジュールは、アダプティブ カードと Bot フレームワーク カード (ヒーロー、サムネイル、およびOffice 365 コネクタ) のボタンを使用して、Microsoft Teams ボットから呼び出すことができます。 タスクモジュールは、多くの場合、開発者がボットの状態を追跡し、ユーザーがシーケンスを中断/キャンセルできるようにする複数の会話ステップよりも優れたユーザーエクスペリエンスです。

タスクモジュールを呼び出す方法は2つあります。

* **新しい種類の呼び出しメッセージ `task/fetch` 。** Bot `invoke` Framework [カードのカード アクション](~/task-modules-and-cards/cards/cards-actions.md#invoke) 、または `Action.Submit` アダプティブ カードの [カード アクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) を使用して、タスク `task/fetch` モジュール (URL またはアダプティブ カード) を使用すると、ボットから動的に取得されます。
* **ディープ リンク URL。** タスク [モジュールのディープ リンク構文](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)を使用して `openUrl` 、Bot Framework [カードのカード アクション](~/task-modules-and-cards/cards/cards-actions.md#openurl) 、または `Action.OpenUrl` アダプティブ カードの [カード アクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) をそれぞれ使用できます。 ディープ リンク URL を使用すると、タスク モジュール URL またはアダプティブ カード本文は明らかに事前に知られており、サーバーの往復を回避 `task/fetch` します。

>[!IMPORTANT]
>通信のセキュリティを確保するために、各プロトコル `url` は `fallbackUrl` HTTPS 暗号化プロトコルを実装する必要があります。

## <a name="invoking-a-task-module-through-taskfetch"></a>タスク/フェッチを使用したタスク・モジュールの呼び出し

`value` `invoke` カードアクションのオブジェクトまたは `Action.Submit` 適切な方法で初期化されると(詳細は後述)、ユーザーがボタンを押すと `invoke` 、ボットにメッセージが送信されます。 メッセージに対する HTTP 応答には `invoke` 、タスク モジュールの表示に使用Teamsラッパー オブジェクトに[TaskInfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)が埋め込まれています。

![タスク/フェッチ要求/応答](~/assets/images/task-module/task-module-invoke-request-response.png)

各ステップをもう少し詳しく見てみましょう。

1. この例では、"購入" カード アクションを持つボット フレームワーク ヒーロー `invoke` [カード](~/task-modules-and-cards/cards/cards-actions.md#invoke)を示します。 プロパティの値 `type` は `task/fetch` - オブジェクトの残りの部分 `value` は、あなたが好きなものにすることができます。
1. ボットは HTTP `invoke` POST メッセージを受信します。
1. ボットは応答オブジェクトを作成し、HTTP 200 応答コードを使用して POST 応答の本文に返します。 応答のスキーマは [、タスク/送信に関する説明で後述](#the-flexibility-of-tasksubmit)しますが、ここで覚えておくべきことは、HTTP 応答の本文にラッパー オブジェクトに埋め込まれた [TaskInfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) が含まれていることです。 例:

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

    `task/fetch`ボットのイベントとその応答は、概念的には `microsoftTeams.tasks.startTask()` 、クライアント SDK の関数と似ています。
1. Microsoft Teamsタスク モジュールが表示されます。

## <a name="submitting-the-result-of-a-task-module"></a>タスク モジュールの結果の送信

ユーザーがタスク モジュールを終了すると、ボットに結果を戻す方法はタブ との [動作に](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)似ていますが、いくつかの違いがあるので、ここでも説明します。

* **HTML/JavaScript ( `TaskInfo.url` )** ユーザーが入力した内容を検証したら、SDK 関数を呼び出します `microsoftTeams.tasks.submitTask()` (ここでは `submitTask()` 読みやすさを目的として参照)。 `submitTask()`タスク モジュールを閉じるTeams場合はパラメータなしで呼び出すことができますが、ほとんどの場合はオブジェクトまたは文字列をに渡します `submitHandler` 。 最初のパラメータとして渡すだけです `result` 。 Teamsは `submitHandler` 、 に `err` `null` `result` 渡したオブジェクト/文字列になります `submitTask()` 。 パラメーターを指定して呼び出す場合 `submitTask()` `result` は、 または文字列の配列を渡す **必要があります** `appId` `appId` Teams。 ボットには、以下の `task/submit` 説明を含むメッセージ `result` が表示 [されます](#payload-of-taskfetch-and-tasksubmit-messages)。
* **アダプティブ カード ( `TaskInfo.card` )**。 ユーザーがボタンを押すと、アダプティブ カード本体 (ユーザーが入力した状態) がメッセージを介してボットに送信されます `task/submit` `Action.Submit` 。

## <a name="the-flexibility-of-tasksubmit"></a>タスク/提出の柔軟性

前のセクションでは、ボットから呼び出されたタスク モジュールでユーザーが終了すると、ボットは常にメッセージを受信することを学習しました `task/submit invoke` 。 開発者は、メッセージに *応答* する際に、いくつかのオプションがあります `task/submit` 。

| HTTP 本文応答                      | シナリオ                                |
| --------------------------------------- | --------------------------------------- |
| なし (メッセージを無視 `task/submit` ) | 最も簡単な応答は、まったく応答しません。 ユーザーがタスク モジュールを使い終えたら、ボットが応答する必要はありません。 |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teamsポップアップ メッセージ ボックスに の値 `value` が表示されます。 |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | ウィザード/マルチステップエクスペリエンスでアダプティブカードのシーケンスを一緒に"連鎖"することができます。 _Adaptive カードをシーケンスにチェーンすることは高度なシナリオであり、ここでは文書化されていない点に注意してください。ただし、Node.jsサンプルアプリはそれをサポートしており、その動作方法は README.md [ファイルに記載されています](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)。_ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>タスク/フェッチおよびタスク/送信メッセージのペイロード

このセクションでは、ボットがまたは Bot Framework オブジェクトを受け取ったときに、ボットが受け取る内容のスキーマを定義 `task/fetch` `task/submit` `Activity` します。 重要なトップレベルは以下に示されます。

| プロパティ | 説明                          |
| -------- | ------------------------------------ |
| `type`   | 常に `invoke`              |
| `name`   | `task/fetch`または`task/submit` |
| `value`  | 開発者が定義したペイロード。 通常、オブジェクトの構造 `value` は、Teamsから送信されたものをミラー化します。 しかし、この場合は、Bot Framework ( ) と Adaptive カード アクション ( ) の両方からの動的フェッチ ( ) をサポートする必要 `task/fetch` `value` `Action.Submit` `data` Teamsがあるため、この方法は異なります `context` `value` / `data` 。<br/><br/>これを行うには、2 つを親オブジェクトに結合します。<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>例: タスク/フェッチおよびタスク/送信の呼び出しメッセージの受信と応答 - Node.js

> [!NOTE]
> 以下のサンプル コードは、テクニカル プレビューとこの機能の最終リリースの間に変更されました: 要求のスキーマ `task/fetch` は [、前のセクションで説明](#payload-of-taskfetch-and-tasksubmit-messages)した内容に従うように変更されました。 つまり、ドキュメントは正しかったが、実装は正しくなかった。 変更された `// for Technical Preview [...]` 内容については、以下のコメントを参照してください。

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

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>例: タスク/フェッチおよびタスク/送信呼び出しメッセージの受信と応答 - C#

C# ボットでは、 `invoke` メッセージはメッセージを処理するコント ローラーによって処理されます `HttpResponseMessage()` `Activity` 。 `task/fetch`および `task/submit` 要求と応答は JSON です。 C# では、Node.jsのように生の JSON を扱うのも便利ではないので、JSON との間でシリアル化を処理するラッパー クラスが必要です。 Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)では、この機能に対する直接的なサポートはまだありませんが[、C# サンプル アプリ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)でこれらの単純なラッパー クラスの例を示します。

次に、C# での処理用のコード例 `task/fetch` と `task/submit` 、サンプルから抜粋したこれらのラッパー クラス ( `TaskInfo` , `TaskEnvelope` )を使用したメッセージの [処理例を示](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)します。

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

上の例では示されていない関数は `SetTaskInfo()` 、 `height` `width` `title` 各ケースのオブジェクトの 、、、、およびプロパティを設定 `TaskInfo` します。 次に [、SetTaskInfo() のソース コードを](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)示します。

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>ボット フレームワーク カード アクションとアダプティブ カード アクションの対

Bot Framework カード アクションのスキーマは、アダプティブ カード アクションとは少し異なります `Action.Submit` 。 その結果、タスクモジュールを呼び出す方法も少し異なります: `data` オブジェクト `Action.Submit` が含まれているので `msteams` 、カード内の他のプロパティに干渉しません。 次の表に、それぞれの例を示します。

| ボット フレームワーク カード アクション                              | アダプティブ カード アクション.Submit アクション                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="see-also"></a>関連項目

* [Microsoft Teamsタスク モジュールサンプル コード — nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)