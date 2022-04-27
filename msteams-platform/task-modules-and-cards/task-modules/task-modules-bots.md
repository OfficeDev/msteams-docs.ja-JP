---
title: Microsoft Teams ボットでタスク モジュールを使用する
description: Bot Framework カード、アダプティブ カード、ディープ リンクなど、Microsoft Teams ボットでタスク モジュールを使用する方法。
ms.localizationpriority: medium
ms.topic: how-to
keywords: タスク モジュール チーム ボットディープ リンク アダプティブ カード
ms.openlocfilehash: 7391f7e0d9da444831b98b4b6b69a97b35298800
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073773"
---
# <a name="use-task-modules-from-bots"></a>ボットでタスク モジュールを使用する

タスク モジュールは、ヒーロー、サムネイル、Office 365 コネクタであるアダプティブ カードと Bot Framework カードのボタンを使用して、Microsoft Teams ボットから呼び出すことができます。 タスク モジュールは、多くの場合、複数の会話手順よりも優れたユーザー エクスペリエンスです。 ボットの状態を追跡し、ユーザーがシーケンスを中断またはキャンセルできるようにします。

タスク モジュールを呼び出す方法は 2 つあります。

* 新しい種類の呼び出しメッセージ`task/fetch`: Bot Framework カードの[カード アクション](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)を使用するか`Action.Submit`、アダプティブ カードの[カード アクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) (タスク モジュールで `task/fetch`URL またはアダプティブ カード) を使用`invoke`すると、ボットから動的にフェッチされます。
* ディープ リンク URL: [タスク モジュールのディープ リンク構文](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)を使用すると、Bot Framework カードの[カード アクション](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl)とアダプティブ カードの`Action.OpenUrl`[カード アクション](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)をそれぞれ使用`openUrl`できます。 ディープ リンク URL では、タスク モジュールの URL またはアダプティブ カード本体は、サーバーのラウンドトリップを回避するために既に `task/fetch`認識されています。

> [!IMPORTANT]
> それぞれ `url` 、HTTPS `fallbackUrl` 暗号化プロトコルを実装する必要があります。

次のセクションでは、タスク モジュールを使用 `task/fetch`して呼び出す方法について詳しく説明します。

## <a name="invoke-a-task-module-using-taskfetch"></a>タスク/フェッチを使用してタスク モジュールを呼び出す

カード アクションの`value``invoke`オブジェクトが初期化されたとき、および`Action.Submit`ユーザーがボタンを選択すると、`invoke`メッセージがボットに送信されます。 メッセージに対する `invoke` HTTP 応答には、タスク モジュールの表示に使用Teamsラッパー オブジェクトに [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) オブジェクトが埋め込まれています。

:::image type="content" source="../../assets/images/task-module/task-module-invoke-request-response.png" alt-text="task/fetch 要求または応答":::

次の手順では、タスク/フェッチを使用してタスク モジュールを呼び出します。

1. この画像は、**購入**`invoke`カード アクションを使用した Bot Framework ヒーロー [カード](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)を示しています。 プロパティの `type` 値は `task/fetch` 、オブジェクトの `value` 残りの部分を任意にすることができます。
1. ボットは HTTP POST メッセージを `invoke` 受信します。
1. ボットは応答オブジェクトを作成し、HTTP 200 応答コードを使用して POST 応答の本文に返します。 応答のスキーマの詳細については、 [タスク/送信に関する説明を](#the-flexibility-of-tasksubmit)参照してください。 次のコードは、ラッパー オブジェクトに埋め込まれた [TaskInfo オブジェクト](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) を含む HTTP 応答の本文の例を示しています。

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

    `task/fetch`ボットのイベントとその応答は、クライアント SDK の`microsoftTeams.tasks.startTask()`関数に似ています。

1. タスク モジュールMicrosoft Teams表示されます。

次のセクションでは、タスク モジュールの結果の送信に関する詳細を説明します。

## <a name="submit-the-result-of-a-task-module"></a>タスク モジュールの結果を送信する

ユーザーがタスク モジュールを使い終わったら、結果をボットに送信する方法は、タブでの動作に似ています。 詳細については、 [タスク モジュールの結果を送信する例を](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)参照してください。 次のような違いがいくつかあります。

* HTML または JavaScript : `TaskInfo.url`ユーザーが入力した内容を検証したら、以降`submitTask()`で読みやすくするために呼び出す SDK 関数を呼び出`microsoftTeams.tasks.submitTask()`します。 タスク モジュールを閉じるTeamsが、オブジェクトまたは文字列`submitHandler`を渡す必要がある場合は、パラメーターなしで呼び出`submitTask()`すことができます。 最初のパラメーター `result`として渡します。. Teamsは、渡されたオブジェクトまたは文字列を呼び出`submitHandler``err``null`し`result`、指定します。`submitTask()` パラメーターを使用して`result`呼び出す`submitTask()`場合は、文字列の配列または文字列の`appId`配列を`appId`渡す必要があります。 これにより、Teamsは、結果を送信するアプリがタスク モジュールを呼び出したのと同じであることを検証できます。 ボットは、次のような`result`メッセージを`task/submit`受け取ります。 詳細については、「[ペイロードと`task/fetch``task/submit`メッセージ](#payload-of-taskfetch-and-tasksubmit-messages)」を参照してください。
* アダプティブ カード : ユーザーが`TaskInfo.card`入力したアダプティブ カード本体は、ユーザーがボタンを選択`Action.Submit`すると、メッセージを`task/submit`介してボットに送信されます。

次のセクションでは、 `task/submit`.

## <a name="the-flexibility-of-tasksubmit"></a>タスク/送信の柔軟性

ユーザーがボットから呼び出されたタスク モジュールで終了すると、ボットは常にメッセージを `task/submit invoke` 受信します。 メッセージに応答 `task/submit` する場合、次のようないくつかのオプションがあります。

| HTTP 本文の応答                      | シナリオ                                |
| --------------------------------------- | --------------------------------------- |
| メッセージを無視しない`task/submit` | 最も単純な応答は、まったく応答しません。 ユーザーがタスク モジュールを使用して完了したときに、ボットが応答する必要はありません。 |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teamsポップアップ メッセージ ボックスに値`value`が表示されます。 |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | アダプティブ カードのシーケンスをウィザードまたはマルチステップ エクスペリエンスで連結できます。 |

> [!NOTE]
> アダプティブ カードをシーケンスにチェーンすることは高度なシナリオです。 Node.jsサンプル アプリでサポートされています。 詳細については、「[Microsoft Teamsタスク モジュール Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)」を参照してください。

次のセクションでは、ペイロードとメッセージの `task/fetch` 詳細について `task/submit` 説明します。

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>タスク/フェッチおよびタスク/送信メッセージのペイロード

このセクションでは、ボットが Bot Framework `Activity` オブジェクトを`task/submit`受信したときに受け取る内容のスキーマを`task/fetch`定義します。 次の表に、ペイロードとメッセージのプロパティを`task/fetch``task/submit`示します。

| プロパティ | 説明                          |
| -------- | ------------------------------------ |
| `type`   | 常に `invoke`.           |
| `name`   | `task/fetch` `task/submit`または . |
| `value`  | 開発者が定義したペイロードです。 オブジェクトの`value`構造は、Teamsから送信されたものと同じです。 ただし、この場合は異なります。 Bot Framework からの動的フェッチ `task/fetch` (つまりアダプティブ カード `Action.Submit` アクション`data`) のサポートが`value`必要です。 ボットにTeams`context`を伝える方法は、ボットに含まれる`value`ものや`data`.<br/><br/>'value' と 'data' を親オブジェクトに結合します。<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

次のセクションでは、Node.jsでのメッセージの受信と応答 `task/fetch` と呼び出し `task/submit` の例を示します。

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>Node.jsおよび C でのタスク/フェッチおよびタスク/送信の呼び出しメッセージの例#

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

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Bot Framework カード アクションとアダプティブ カード アクション.Submit アクション

Bot Framework カード アクションのスキーマはアダプティブ カード `Action.Submit` アクションとは異なり、タスク モジュールを呼び出す方法も異なります。 オブジェクトには`data``Action.Submit`オブジェクトが`msteams`含まれているため、カード内の他のプロパティに干渉しません。 次の表は、各カード アクションの例を示しています。

| Bot Framework カード アクション                              | アダプティブ カード アクション.Submit アクション                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|タスク モジュールのサンプル ボット-V4 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

[ステップ バイ ステップ ガイドに](../../sbs-botbuilder-taskmodule.yml)従って、Teamsでタスク モジュール ボットを作成してフェッチします。

## <a name="see-also"></a>関連項目

* [Node.jsでタスク モジュールのサンプル コードをMicrosoft Teamsする](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Bot Framework Samples (Bot Framework のサンプル)](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
