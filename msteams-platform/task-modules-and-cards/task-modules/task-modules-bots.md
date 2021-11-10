---
title: ボットでタスク モジュールMicrosoft Teamsする
description: ボット フレームワーク カード、アダプティブ カード、ディープ Microsoft Teamsなど、ボットでタスク モジュールを使用する方法。
ms.localizationpriority: medium
ms.topic: how-to
keywords: タスク モジュール チームボット ディープ リンクアダプティブ カード
ms.openlocfilehash: c46b647ca9fa446db6ae51ae6d33dbabdef18296
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888308"
---
# <a name="use-task-modules-from-bots"></a>ボットでタスク モジュールを使用する
 
タスク モジュールは、ヒーロー、サムネイル、Microsoft Teams コネクタであるアダプティブ カードおよびボット フレームワーク カードのボタンを使用して、Office 365ボットから呼び出すことができます。 タスク モジュールは、多くの場合、複数の会話手順よりも優れたユーザー エクスペリエンスです。 ボットの状態を追跡し、ユーザーがシーケンスを中断またはキャンセルできます。

タスク モジュールを呼び出す方法は 2 通りあります。

* 新しい種類の呼び出しメッセージ : ボット フレームワーク カードのカード アクションを使用するか、アダプティブ カードのカード アクションを使用して、タスク モジュールが `task/fetch` `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` URL またはアダプティブ カードを使用して、ボットから動的にフェッチされます。
* ディープ リンク URL:[](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)タスク モジュールのディープ リンク構文を使用して、Bot Framework カードのカード アクションまたはアダプティブ カードのカード アクションをそれぞれ `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)使用できます。 ディープ リンク URL を使用すると、タスク モジュールの URL またはアダプティブ カード本文は、 を基準にしたサーバーのラウンドトリップを回避することが既に知られています `task/fetch` 。

> [!IMPORTANT]
> それぞれ `url` `fallbackUrl` 、HTTPS 暗号化プロトコルを実装する必要があります。

次のセクションでは、 を使用してタスク モジュールを呼び出す方法の詳細について説明します `task/fetch` 。

## <a name="invoke-a-task-module-using-taskfetch"></a>タスク/フェッチを使用してタスク モジュールを呼び出す

カードアクションのオブジェクトが初期化されると、ユーザーがボタンを選択すると、ボットに `value` `invoke` `Action.Submit` `invoke` メッセージが送信されます。 メッセージに対する HTTP 応答には、ラッパー オブジェクトに TaskInfo オブジェクトが埋め込まれているので、Teamsモジュールの表示に `invoke` 使用されます。 [](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)

![task/fetch 要求または応答](~/assets/images/task-module/task-module-invoke-request-response.png)

次の手順では、タスク/フェッチを使用してタスク モジュールを呼び出します。

1. この画像は、カードの購入アクションを含む Bot Framework **ヒーロー カード** `invoke` [を示しています](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)。 プロパティの値 `type` は、オブジェクトの残りの部分 `task/fetch` `value` が選択できます。
1. ボットは HTTP `invoke` POST メッセージを受信します。
1. ボットは応答オブジェクトを作成し、HTTP 200 応答コードを使用して POST 応答の本文に返します。 応答のスキーマの詳細については [、「task/submit」を参照してください](#the-flexibility-of-tasksubmit)。 次のコードは、ラッパー オブジェクトに埋め込まれた [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) オブジェクトを含む HTTP 応答の本文の例を示しています。

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

    ボット `task/fetch` のイベントとその応答は、クライアント `microsoftTeams.tasks.startTask()` SDK の関数と似ています。

1. Microsoft Teamsタスク モジュールを表示します。

次のセクションでは、タスク モジュールの結果の送信に関する詳細を説明します。

## <a name="submit-the-result-of-a-task-module"></a>タスク モジュールの結果を送信する

ユーザーがタスク モジュールを終了すると、結果をボットに送信し戻すのは、タブの動作と似ています。 詳細については、タスク [モジュールの結果を送信する例を参照してください](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)。 次のようにいくつかの違いがあります。

* HTML または JavaScript : ユーザーが入力した値を検証したら、読みやすさを目的として、以下に示す SDK 関数 `TaskInfo.url` `microsoftTeams.tasks.submitTask()` `submitTask()` を呼び出します。 タスク モジュールを閉じTeamsパラメーターを指定せずに呼び出しできますが、オブジェクトまたは文字列を自分に `submitTask()` 渡す必要があります `submitHandler` 。 最初のパラメーターとして渡します `result` 。 Teams呼び `submitHandler` 出す `err` 、、、、に渡した `null` `result` オブジェクトまたは文字列です `submitTask()` 。 パラメーターを使用 `submitTask()` して呼び出 `result` す場合は、文字列または文字列の `appId` 配列を渡す必要 `appId` があります。 これにより、Teams送信するアプリがタスク モジュールを呼び出したアプリと同じことを検証できます。 ボットは、 を含む `task/submit` メッセージを受信 `result` します。 詳細については、「ペイロードと [メッセージ」 `task/fetch` を `task/submit` 参照してください](#payload-of-taskfetch-and-tasksubmit-messages)。
* アダプティブ カード : ユーザーが入力したアダプティブ カード本文は、ユーザーがボタンを選択すると、メッセージを介してボット `TaskInfo.card` `task/submit` に送信 `Action.Submit` されます。

次のセクションでは、 の柔軟性に関する詳細を示します `task/submit` 。

## <a name="the-flexibility-of-tasksubmit"></a>タスク/送信の柔軟性

ユーザーがボットから呼び出されたタスク モジュールで終了すると、ボットは常にメッセージを受信 `task/submit invoke` します。 次のようにメッセージに応答する場合、いくつかの `task/submit` オプションがあります。

| HTTP 本文の応答                      | シナリオ                                |
| --------------------------------------- | --------------------------------------- |
| メッセージを無視 `task/submit` しない | 最も単純な応答は応答なしです。 ユーザーがタスク モジュールを使い終わったときにボットが応答する必要はありません。 |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teamsポップアップ メッセージ ボックス `value` に値を表示します。 |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | アダプティブ カードのシーケンスを、ウィザードまたはマルチステップ エクスペリエンスで一緒にチェーンできます。 |

> [!NOTE]
> アダプティブ カードをシーケンスにチェーン化する方法は、高度なシナリオです。 このNode.jsサンプル アプリがサポートしています。 詳細については、「タスク モジュール[のMicrosoft Teams」を参照Node.js。 ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)

次のセクションでは、ペイロードとメッセージの詳細 `task/fetch` について説明 `task/submit` します。

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>タスク/フェッチおよびタスク/送信メッセージのペイロード

このセクションでは、ボットがボットまたは Bot Framework オブジェクトを受信するときに受け取るスキーマ `task/fetch` `task/submit` を定義 `Activity` します。 次の表に、ペイロードとメッセージのプロパティ `task/fetch` を示 `task/submit` します。

| プロパティ | 説明                          |
| -------- | ------------------------------------ |
| `type`   | は常です `invoke` 。           |
| `name`   | は、 `task/fetch` または `task/submit` です。 |
| `value`  | 開発者定義のペイロードです。 オブジェクトの構造は、オブジェクトから送信される構造と `value` Teams。 ただし、この場合は異なります。 これは、Bot Framework (つまり) とアダプティブ カードアクションの両方からの動的フェッチのサポートが `task/fetch` `value` `Action.Submit` 必要です `data` 。 ボットに含まれているTeamsに加えて、ボットにメッセージを伝達 `context` する方法が `value` 必要です `data` 。<br/><br/>'value' と 'data' を親オブジェクトに結合します。<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

次のセクションでは、メッセージの受信と応答、およびメッセージの呼び出しの例を示 `task/fetch` `task/submit` Node.js。

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>タスク/フェッチとタスク/サブミットの呼び出しメッセージの例 (Node.js C)#

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

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

# <a name="c"></a>[C#](#tab/csharp)

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

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Bot Framework カードアクションとアダプティブ カード アクション.Submit アクション

Bot Framework カードアクションのスキーマはアダプティブ カード アクションとは異なります。また、タスク モジュールを呼び出す方法も `Action.Submit` 異なります。 オブジェクト `data` には `Action.Submit` オブジェクトが含まれているので、カード内の他の `msteams` プロパティに干渉しません。 次の表に、各カード アクションの例を示します。

| Bot Framework カードアクション                              | アダプティブ カード アクション.Submit アクション                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|タスク モジュールのサンプル ボット-V4 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a>関連項目

* [Microsoft Teamsタスク モジュールのサンプル コードをNode.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
