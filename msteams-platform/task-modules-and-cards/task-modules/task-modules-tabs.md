---
title: '[タスク モジュール] タブでのタスク Microsoft Teams使用する'
description: クライアント SDK を使用してタスク モジュールTeamsタブからMicrosoft Teams説明します。
localization_priority: Normal
ms.topic: how-to
keywords: タスク モジュールチームがクライアント SDK をタブする
ms.openlocfilehash: 5e85fd0662b8a15d6b98d9c2d2dfa5137b05fa39
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019525"
---
# <a name="using-task-modules-in-tabs"></a>タブでタスク モジュールを使用する

タブにタスク モジュールを追加すると、データ入力が必要なワークフローに対するユーザー エクスペリエンスが大幅に簡素化されます。 タスク モジュールを使用すると、ユーザーが認識できるポップアップTeamsを収集できます。 この例の良い例は、Planner カードの編集です。タスク モジュールを使用して同様のエクスペリエンスを作成できます。

タスク モジュール機能をサポートするために、次の 2 つの新しい機能がクライアント[SDK Microsoft Teams追加されました](/javascript/api/overview/msteams-client)。

```typescript
microsoftTeams.tasks.startTask(
    taskInfo: TaskInfo,
    submitHandler?: (err: string, result: string | any) => void
): void;

microsoftTeams.tasks.submitTask(
    result?: string | any,
    appIds?: string | string[]
): void;
```

それぞれの動作を見てみよ。

## <a name="invoking-a-task-module-from-a-tab"></a>タブからのタスク モジュールの呼び出し

タブからタスク モジュールを呼び出す場合は `microsoftTeams.tasks.startTask()` [、TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) オブジェクトとオプションのコールバック関数を渡 `submitHandler` します。 前述したように、次の 2 つのケースを考慮する必要があります。

1. の値 `TaskInfo.url` は URL に設定されます。 タスク モジュール ウィンドウが表示され `TaskModule.url` 、内部として `<iframe>` 読み込まれます。 そのページの JavaScript を呼び出す必要があります `microsoftTeams.initialize()` 。 ページに関数が存在し、呼び出し時にエラーが発生した場合は、次に説明するようにエラーを示すエラー文字列に設定して `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` 呼び出 [されます](#task-module-invocation-errors)。
1. 値はアダプティブ `taskInfo.card` カード [の JSON です](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)。 この場合、ユーザーがアダプティブ カードのボタンを閉じるか押した場合に呼び出す JavaScript 関数は明らかではありません。ユーザーが入力した値を受け取る唯一の方法は、結果をボットに渡す方法です。 `submitHandler` タブからアダプティブ カード タスク モジュールを使用するには、ユーザーから情報を取得するために、アプリにボットを含める必要があります。 これは以下で説明します。

## <a name="example-invoking-a-task-module"></a>例: タスク モジュールの呼び出し

以下のコードは、タスク モジュールの [サンプルから適合しています](~/task-modules-and-cards/what-are-task-modules.md#code-sample)。 タスク モジュールの外観を次に示します。

![タスク モジュール - カスタム フォーム](~/assets/images/task-module/task-module-custom-form.png)

これは `submitHandler` 非常に単純です。コンソールの値またはコンソール `err` に `result` エコーします。

```javascript
let taskInfo = {
    title: null,
    height: null,
    width: null,
    url: null,
    card: null,
    fallbackUrl: null,
    completionBotId: null,
};

taskInfo.url = "https://contoso.com/teamsapp/customform";
taskInfo.title = "Custom Form";
taskInfo.height = 510;
taskInfo.width = 430;
submitHandler = (err, result) => {
    console.log(`Submit handler - err: ${err}`);
    console.log(`Submit handler - result\rName: ${result.name}\rEmail: ${result.email}\rFavorite book: ${result.favoriteBook}`);
};
microsoftTeams.tasks.startTask(taskInfo, submitHandler);
```

## <a name="submitting-the-result-of-a-task-module"></a>タスク モジュールの結果の送信

この `submitHandler` 関数は、 と一緒に使用されます `TaskInfo.url` 。 関数 `submitHandler` は Web ページに `TaskInfo.url` 存在します。 タスク モジュールを呼び出す際にエラーが発生した場合、関数は直ちに呼び出され、どのエラーが発生したのかを `submitHandler` `err` 示す文字列 [が表示されます](#task-module-invocation-errors)。 この関数は、ユーザーがタスク モジュールの右上にある X を押すと、文字列 `submitHandler` `err` で呼び出されます。

呼び出しエラーが発生し、ユーザーが X キーを押して閉じなかった場合、ユーザーは終了するとボタンを押します。 タスク モジュールの URL かアダプティブ カードかによって、次の処理が実行されます。

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript ( `TaskInfo.url` )

ユーザーが入力した情報を検証したら、SDK 関数を呼び出します (以下、読みやすさの目的 `microsoftTeams.tasks.submitTask()` `submitTask()` で呼び出します)。 Teams がタスク モジュールを閉じるだけで、ほとんどの場合、オブジェクトまたは文字列を自分のタスク モジュールに渡す場合は、パラメーターを指定せずに呼び出 `submitTask()` します `submitHandler` 。

結果を最初のパラメーターとして渡します。 Teamsが呼 `submitHandler` び出 `err` され、渡 `null` された `result` オブジェクト/文字列になります `submitTask()` 。 パラメーターを使用して呼び出す場合は、文字列の配列または配列を渡す必要があります `submitTask()` `result`  `appId` `appId` 。これにより、Teams は、結果を送信するアプリがタスク モジュールを呼び出したアプリと同じことを検証できます。

### <a name="adaptive-card-taskinfocard"></a>アダプティブ カード ( `TaskInfo.card` )

タスク モジュールを呼び出した場合、ユーザーがボタンを押すと、カード内の値がの値 `submitHandler` `Action.Submit` として返されます `result` 。 ユーザーが Esc ボタンを押すか、X キーを押すと `err` 、代わりに返されます。 または、タブに加えてアプリにボットが含まれている場合は、単にボットの値をオブジェクトに `appId` `completionBotId` 含 `TaskInfo` める必要があります。 アダプティブ カード本文 (ユーザーが入力した場合) は、ユーザーがボタンを押すと、メッセージを介してボット `task/submit invoke` に送信 `Action.Submit` されます。 受信するオブジェクトのスキーマは、タスク/フェッチおよびタスク/送信メッセージで受け取る[スキーマと非常に似ています](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)。唯一の違いは、JSON オブジェクトのスキーマがアダプティブ カード オブジェクトで、アダプティブカード オブジェクトを含むオブジェクト[](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)ではなく、アダプティブ カード オブジェクトである点です。

## <a name="example-submitting-the-result-of-a-task-module"></a>例: タスク モジュールの結果の送信

上記の [タスク モジュールのフォームを](#example-invoking-a-task-module) HTML フォームで呼び出します。 フォームが定義されている場所を次に示します。

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

このフォームには 5 つのフィールドがありますが、この例では、3 つのフィールドの値にのみ関心 `name` があります。 `email` `favoriteBook`

呼び出す `validateForm()` 関数を次に示します `submitTask()` 。

```javascript
function validateForm() {
    var customerInfo = {
        name: document.forms["customerForm"]["name"].value,
        email: document.forms["customerForm"]["email"].value,
        favoriteBook: document.forms["customerForm"]["favoriteBook"].value
    }
    microsoftTeams.tasks.submitTask(customerInfo, "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx");
    return true;
}
```

## <a name="task-module-invocation-errors"></a>タスク モジュール呼び出しのエラー

以下に、ユーザーが受 `err` け取る可能性の値を示します `submitHandler` 。

| 問題 | エラー メッセージ (値 `err` ) |
| ------- | ------------------------------ |
| 両方の値と `TaskInfo.url` 指定 `TaskInfo.card` された値。 | "カードと URL の両方の値が指定されました。 一方または他の両方は許可されません。 |
| 指定も `TaskInfo.url` `TaskInfo.card` 指定もされていません。 | "カードまたは URL の値を指定する必要があります。 |
| 無効 `appId` です。 | "無効な appId" |
| ユーザーが X ボタンを押し、閉じる。 | "ユーザーがタスク モジュールを取り消し/閉じた。 |
