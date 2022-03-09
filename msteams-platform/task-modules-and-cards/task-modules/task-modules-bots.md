---
title: ボットでタスク モジュールをMicrosoft Teamsする
description: ボット フレームワーク カード、アダプティブ カード、ディープ リンクなど、Microsoft Teamsボットでタスク モジュールを使用する方法。
ms.localizationpriority: medium
ms.topic: how-to
keywords: タスク モジュール チームボット ディープ リンクアダプティブ カード
ms.openlocfilehash: 39df7f3845cc11e6e15da03c72b0c792a795af35
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355721"
---
# <a name="use-task-modules-from-bots"></a>ボットでタスク モジュールを使用する
 
タスク モジュールは、ヒーロー、サムネイル、Microsoft Teams コネクタであるアダプティブ カードとボット フレームワーク カードのボタンを使用して、Office 365できます。 タスク モジュールは、多くの場合、複数の会話手順よりも優れたユーザー エクスペリエンスです。 ボットの状態を追跡し、ユーザーがシーケンスを中断またはキャンセルできます。

タスク モジュールを呼び出す方法は 2 通りあります。

* 新しい種類の呼び出しメッセージ : [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) [](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) `invoke` ボット フレームワーク `task/fetch``Action.Submit` カードのカード アクションを使用するか、アダプティブ カードのカード アクションを使用して、タスク モジュールが URL またはアダプティブ カードを使用して、ボットから動的にフェッチされます。`task/fetch`
* [](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)ディープ リンク URL: タスク `openUrl` モジュールのディープ リンク構文を使用して、Bot Framework [](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) `Action.OpenUrl` カードのカード アクションまたはアダプティブ カードのカード アクションをそれぞれ使用できます。[](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) ディープ リンク URL を使用すると、タスク モジュールの URL またはアダプティブ カード本文は、 を基準にしたサーバーのラウンドトリップを回避することが既に知られています `task/fetch`。

> [!IMPORTANT]
> それぞれ、 `url` HTTPS `fallbackUrl` 暗号化プロトコルを実装する必要があります。

次のセクションでは、 を使用してタスク モジュールを呼び出す方法の詳細について説明します `task/fetch`。

## <a name="invoke-a-task-module-using-taskfetch"></a>タスク/フェッチを使用してタスク モジュールを呼び出す

カードアクション`value`のオブジェクトが`invoke`初期化`Action.Submit``invoke`されると、ユーザーがボタンを選択すると、ボットにメッセージが送信されます。 メッセージに対する `invoke` HTTP 応答には、ラッパー オブジェクトに [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) オブジェクトが埋め込まれているTeamsモジュールを表示するために使用されます。

![task/fetch 要求または応答](~/assets/images/task-module/task-module-invoke-request-response.png)

次の手順では、タスク/フェッチを使用してタスク モジュールを呼び出します。

1. 次の図は、カードの購入アクションを含む **Bot Framework ヒーロー カードを** `invoke` [示しています](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)。 プロパティの値は `type` 、オブジェクト `task/fetch` の `value` 残りの部分が選択できます。
1. ボットは HTTP POST メッセージ `invoke` を受信します。
1. ボットは応答オブジェクトを作成し、HTTP 200 応答コードを使用して POST 応答の本文に返します。 応答のスキーマの詳細については、「task [/submit」を参照してください](#the-flexibility-of-tasksubmit)。 次のコードは、ラッパー オブジェクトに埋め込まれた [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) オブジェクトを含む HTTP 応答の本文の例を示しています。

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

    ボット `task/fetch` のイベントとその応答は、クライアント SDK の `microsoftTeams.tasks.startTask()` 関数と似ています。

1. Microsoft Teamsモジュールが表示されます。

次のセクションでは、タスク モジュールの結果の送信に関する詳細を説明します。

## <a name="submit-the-result-of-a-task-module"></a>タスク モジュールの結果を送信する

ユーザーがタスク モジュールを終了すると、結果をボットに送信し戻すのは、タブの動作と似ています。 詳細については、タスク [モジュールの結果を送信する例を参照してください](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)。 次のようにいくつかの違いがあります。

* HTML または JavaScript `TaskInfo.url`: ユーザー `microsoftTeams.tasks.submitTask()` が入力した値を検証したら、読みやすさを目的として、以下に示す SDK `submitTask()` 関数を呼び出します。 タスク モジュールを`submitTask()`閉じTeamsパラメーターを指定せずに呼び出しできますが、オブジェクトまたは文字列を渡す必要があります`submitHandler`。 最初のパラメーターとして渡します `result`。 Teams呼び出`submitHandler`す 、`err`、`null`、、`result`に渡したオブジェクトまたは文字列です`submitTask()`。 パラメーターを使用して `submitTask()` 呼び出す `result` 場合は、文字列または文字列の `appId` 配列を渡す必要 `appId` があります。 これにより、Teams送信するアプリがタスク モジュールを呼び出したアプリと同じことを検証できます。 ボットは、 を含むメッセージを `task/submit` 受信します `result`。 詳細については、「ペイロードと [メッセージ」 `task/fetch` を参照 `task/submit` してください](#payload-of-taskfetch-and-tasksubmit-messages)。
* アダプティブ カード : `TaskInfo.card`ユーザー `task/submit` が入力したアダプティブ カード本文は、ユーザーがボタンを選択すると、メッセージを介してボットに送信 `Action.Submit` されます。

次のセクションでは、 の柔軟性に関する詳細を示します `task/submit`。

## <a name="the-flexibility-of-tasksubmit"></a>タスク/送信の柔軟性

ユーザーがボットから呼び出されたタスク モジュールで終了すると、ボットは常にメッセージを受信 `task/submit invoke` します。 次のようにメッセージに応答する場合、いくつかの `task/submit` オプションがあります。

| HTTP 本文の応答                      | シナリオ                                |
| --------------------------------------- | --------------------------------------- |
| メッセージを無視しない`task/submit` | 最も単純な応答は応答なしです。 ユーザーがタスク モジュールを使い終わったときにボットが応答する必要はありません。 |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teamsポップアップ メッセージ ボックスに値`value`を表示します。 |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | アダプティブ カードのシーケンスを、ウィザードまたはマルチステップ エクスペリエンスで一緒にチェーンできます。 |

> [!NOTE]
> アダプティブ カードをシーケンスにチェーン化する方法は、高度なシナリオです。 このNode.jsサンプル アプリがサポートしています。 詳細については、「タスク モジュール[のMicrosoft Teams」を参照Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)。

次のセクションでは、ペイロードとメッセージの詳細について `task/fetch` 説明 `task/submit` します。

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>タスク/フェッチおよびタスク/送信メッセージのペイロード

このセクションでは、ボットがボットまたは Bot Framework オブジェクトを受信するときに受`task/fetch``task/submit`け取るスキーマを定義`Activity`します。 次の表に、ペイロードとメッセージのプロパティを `task/fetch` 示 `task/submit` します。

| プロパティ | 説明                          |
| -------- | ------------------------------------ |
| `type`   | は常です `invoke`。           |
| `name`   | は、または `task/fetch` です `task/submit`。 |
| `value`  | 開発者定義のペイロードです。 オブジェクトの構造は`value`、オブジェクトから送信される構造とTeams。 ただし、この場合は異なります。 これは、Bot Framework `value` `Action.Submit` (`task/fetch`つまり) とアダプティブ カードアクションの両方からの動的フェッチのサポートが必要です`data`。 ボットにTeams`context`、またはに含まれているものに加えて、ボットに通信する方法が必要`value`です`data`。<br/><br/>'value' と 'data' を親オブジェクトに結合します。<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

次のセクションでは、メッセージの受信`task/fetch``task/submit`と応答、およびメッセージの呼び出しの例を示Node.js。

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

Bot Framework カードアクションのスキーマはアダプティブ カード `Action.Submit` アクションとは異なります。また、タスク モジュールを呼び出す方法も異なります。 オブジェクト `data` にはオブジェクト `Action.Submit` が含 `msteams` まれているので、カード内の他のプロパティに干渉しません。 次の表に、各カード アクションの例を示します。

| Bot Framework カードアクション                              | アダプティブ カード アクション.Submit アクション                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|タスク モジュールのサンプル ボット-V4 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

ステップ バイ [ステップ ガイドに従って](../../sbs-botbuilder-taskmodule.yml)、タスク モジュール ボットを作成およびフェッチTeams。

## <a name="see-also"></a>関連項目

* [Microsoft Teamsタスク モジュールのサンプル コードをNode.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
