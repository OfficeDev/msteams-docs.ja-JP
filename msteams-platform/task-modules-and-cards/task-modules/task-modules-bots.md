---
title: Microsoft Teams ボットでタスク モジュールを使用する
description: Bot Framework カード、アダプティブ カード、ディープ リンクなど、Microsoft Teams ボットでタスク モジュールを使用する方法。
ms.localizationpriority: high
ms.topic: how-to
keywords: タスク モジュール チーム ボットディープ リンク アダプティブ カード
ms.openlocfilehash: 1074eee616ca7a5d78a071fb42c23d0010a8300d
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111333"
---
# <a name="use-task-modules-from-bots"></a>ボットでタスク モジュールを使用する

タスク モジュールは、ヒーロー、サムネイル、Office 365 コネクタであるアダプティブ カードと Bot Framework カードのボタンを使用して、Microsoft Teams ボットから呼び出すことができます。 タスク モジュールは、多くの場合、複数の会話手順よりも優れたユーザー エクスペリエンスです。 ボットの状態を追跡し、ユーザーがシーケンスを中断またはキャンセルできるようにします。

タスク モジュールを呼び出す方法は 2 つあります。

* 新しい種類の呼び出しメッセージ`task/fetch`: [ボット フレームワーク カード] の場合は`invoke` [カードアクション](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)を使用し、[アダプティブ カード] の場合は`Action.Submit`[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)を `task/fetch` で使用します。 URL または [アダプティブ カード] のいずれかのタスク モジュールは、ボットから動的にフェッチされます。
* ディープ リンク URL：[タスク モジュールのディープリンク構文](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)を使用すると、ボット フレームワークカード の場合は`openUrl` [カードアクション](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl)、または、アダプティブカードの場合`Action.OpenUrl`[カードアクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)にそれぞれなります。 ディープ リンク URL の場合、タスク モジュールの URL またはアダプティブ カード本体は、`task/fetch` との相対的なサーバー ラウンドトリップを回避することがすでにわかっています。

> [!IMPORTANT]
> 各 `url` および `fallbackUrl` は、HTTPS 暗号化プロトコルを実装する必要があります。

次のセクションでは、`task/fetch` を使用してタスク モジュールを呼び出す方法について詳しく説明します。

## <a name="invoke-a-task-module-using-taskfetch"></a>タスク/フェッチを使用してタスク モジュールを呼び出す

`invoke` カード アクションまたは `Action.Submit` の `value` オブジェクトが初期化され、ユーザーがボタンを選択すると、`invoke` メッセージがボットに送信されます。 `invoke` メッセージへの HTTP 応答には、ラッパー オブジェクトに埋め込まれた [ TaskInfo オブジェクト ](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) があり、Teams はこれを使用してタスク モジュールを表示します。

:::image type="content" source="../../assets/images/task-module/task-module-invoke-request-response.png" alt-text="タスク/フェッチ要求または応答":::

次の手順では、タスク/フェッチを使用してタスク モジュールを呼び出します。

1. この画像は、**購入**`invoke`[カード アクション](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)を備えたボット フレームワーク ヒーロー カードを示しています。 `type` プロパティの値は `task/fetch` であり、残りの `value` オブジェクトを選択できます。
1. ボットは `invoke` HTTP POST メッセージを受信します。
1. ボットは応答オブジェクトを作成し、それを HTTP 200 応答コードとともに POST 応答の本文に返します。 応答のスキーマの詳細については、[ タスク/送信に関する説明 ](#the-flexibility-of-tasksubmit) を参照してください。 次のコードは、ラッパー オブジェクトに埋め込まれた [TaskInfo オブジェクト](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) を含む HTTP 応答の本文の例を示しています。

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

    ボットに対する `task/fetch` イベントとその応答は、クライアント SDK の `microsoftTeams.tasks.startTask()` 関数に似ています。

1. Microsoft Teams はタスク モジュールを表示します。

次のセクションでは、タスク モジュールの結果を送信する方法について詳しく説明します。

## <a name="submit-the-result-of-a-task-module"></a>タスク モジュールの結果を送信する

ユーザーがタスク モジュールを終了したら、結果をボットに送信するのは、タブでの作業と同じです。 詳細については、[タスク モジュールの結果を送信する例](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)を参照してください。 次のようないくつかの違いがあります。

* `TaskInfo.url` である HTML または JavaScript: ユーザーが入力した内容を検証したら、読みやすくするために、以降 `submitTask()` と呼ばれる `microsoftTeams.tasks.submitTask()` SDK 関数を呼び出します。 Teams にタスク モジュールを閉じさせたい場合は、パラメータなしで `submitTask()` を呼び出すことができますが、オブジェクトまたは文字列を `submitHandler` に渡す必要があります。 最初のパラメーター `result` として渡します。. Teams は `submitHandler` を呼び出し、`err` は `null` であり、`result` は `submitTask()` に渡したオブジェクトまたは文字列です。 `result`パラメータを使用して `submitTask()` を呼び出す場合は、`appId` または `appId` 文字列の配列を渡す必要があります。 これにより、Teamsは、結果を送信するアプリがタスク モジュールを呼び出したアプリと同じであることを検証できます。 ボットは、`result` を含む `task/submit` メッセージを受信します。 詳細については、[ ペイロードの `task/fetch` および `task/submit`メッセージ](#payload-of-taskfetch-and-tasksubmit-messages) を参照してください。
* `TaskInfo.card` であるアダプティブ カード: ユーザーが入力したアダプティブ カード本体は、ユーザーが `Action.Submit` ボタンを選択すると、`task/submit` メッセージを介してボットに送信されます。

次のセクションでは、`task/submit` の柔軟性について詳しく説明します。

## <a name="the-flexibility-of-tasksubmit"></a>タスク/送信の柔軟性

ユーザーがボットから呼び出されたタスク モジュールを終了すると、ボットは常に `task/submit invoke` メッセージを受信します。 `task/submit` メッセージに応答するときは、次のようにいくつかのオプションがあります。

| HTTP 本文の応答                      | シナリオ                                |
| --------------------------------------- | --------------------------------------- |
| `task/submit` メッセージを無視するものはありません | 最も単純な応答は、まったく応答がないことです。 ユーザーがタスク モジュールを終了したときにボットが応答する必要はありません。 |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams は、ポップアップ メッセージ ボックスに `value` の値を表示します。 |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | アダプティブ カードのシーケンスをウィザードまたはマルチステップ エクスペリエンスで連結できます。 |

> [!NOTE]
> アダプティブ カードをシーケンスにチェーンすることは高度なシナリオです。 Node.js サンプル アプリはそれをサポートしています。 詳細については、「[Microsoft Teams タスク モジュール Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)」を参照してください。

次のセクションでは、`task/fetch` および `task/submit` メッセージのペイロードについて詳しく説明します。

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>タスク/フェッチおよびタスク/送信メッセージのペイロード

このセクションでは、ボットが `task/fetch` または `task/submit` ボット フレームワーク `Activity` オブジェクトを受信したときに受信するもののスキーマを定義します。 次の表に、`task/fetch` および `task/submit` メッセージのペイロードのプロパティを示します。

| プロパティ | 説明                          |
| -------- | ------------------------------------ |
| `type`   | 常に `invoke` です。           |
| `name`   | `task/fetch` または `task/submit` のいずれかです。 |
| `value`  | 開発者定義のペイロードです。 `value` オブジェクトの構造は、Teams から送信されるものと同じです。 ただし、この場合は異なります。 `value` であるボット フレームワークと `data` であるアダプティブ カード `Action.Submit` アクションの両方からの `task/fetch` である動的フェッチのサポートが必要です。 `value` または `data` に含まれているものに加えて、チーム `context` をボットに通信する方法が必要です。<br/><br/>'value' と 'data' を親オブジェクトに結合します。<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

次のセクションでは、Node.js で `task/fetch` および `task/submit` 呼び出しメッセージを受信して​​応答する例を示します。

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>Node.js および C# でのタスク/フェッチおよびタスク/送信呼び出しメッセージの例

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

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Bot Framework カード アクションと Adaptive Card Action.Submit アクション

Bot Framework カード アクションのスキーマは、アダプティブ カード `Action.Submit` アクションとは異なり、タスク モジュールを呼び出す方法も異なります。 `Action.Submit` の `data` オブジェクトには `msteams` オブジェクトが含まれているため、カードの他のプロパティに干渉しません。 次の表は、各カード アクションの例を示しています。

| Bot Framework カード アクション                              | Adaptive Card Action.Submit アクション                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|タスク モジュールのサンプル ボット - V4 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

[ステップ バイ ステップ ガイド](../../sbs-botbuilder-taskmodule.yml)に従って、Teams でタスク モジュール ボットを作成してフェッチします。

## <a name="see-also"></a>関連項目

* [Node.js の Microsoft Teams タスク モジュールのサンプル コード](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Bot Framework Samples (Bot Framework のサンプル)](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
