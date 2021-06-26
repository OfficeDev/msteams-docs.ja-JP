---
title: '[タスク モジュール] タブでタスク Microsoft Teams使用する'
description: クライアント SDK を使用して、Teamsタブからタスク モジュールMicrosoft Teams説明します。
localization_priority: Normal
ms.topic: how-to
keywords: タスク モジュールチームがクライアント SDK をタブする
ms.openlocfilehash: 8afd2c93261f28aa7ced4c98d29be27dca35f8b1
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140553"
---
# <a name="use-task-modules-in-tabs"></a>タブでタスク モジュールを使用する

タブにタスク モジュールを追加して、データ入力を必要とするワークフローに対するユーザー エクスペリエンスを簡略化します。 タスク モジュールを使用すると、Microsoft のポップアップで入力をTeams-Awareできます。 この例の良い例は、Planner カードの編集です。 タスク モジュールを使用して、同様のエクスペリエンスを作成できます。

タスク モジュール機能をサポートするために、クライアント SDK に 2 つの[Teams追加されます](/javascript/api/overview/msteams-client)。 次のコードは、これら 2 つの関数の例を示しています。

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

タブからタスク モジュールを呼び出し、タスク モジュールの結果を送信する方法を確認できます。

## <a name="invoke-a-task-module-from-a-tab"></a>タブからタスク モジュールを呼び出す

タブからタスク モジュールを呼び出す場合は `microsoftTeams.tasks.startTask()` [、TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) オブジェクトとオプションのコールバック関数を渡 `submitHandler` します。 次の 2 つのケースを考慮する必要があります。

* の値 `TaskInfo.url` は URL に設定されます。 タスク モジュール ウィンドウが表示され `TaskModule.url` 、内部として `<iframe>` 読み込まれます。 そのページ呼び出しの JavaScript `microsoftTeams.initialize()` 。 ページに関数が存在し、呼び出し時にエラーが発生した場合は、同じことを示すエラー文字列に設定して `submitHandler` `microsoftTeams.tasks.startTask()` 呼び `submitHandler` `err` 出されます。 詳細については、「タスク モジュールの呼び [出しエラー」を参照してください](#task-module-invocation-errors)。
* 値はアダプティブ `taskInfo.card` カード [の JSON です](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)。 ユーザーがアダプティブ カードのボタンを閉じるか押すと、呼び出す JavaScript `submitHandler` 関数はありません。 ユーザーが入力した情報を受け取る唯一の方法は、結果をボットに渡す方法です。 タブからアダプティブ カード タスク モジュールを使用するには、アプリにボットを含め、ユーザーからの応答を取得する必要があります。

次のセクションでは、タスク モジュールを呼び出す例を示します。

## <a name="example-of-invoking-a-task-module"></a>タスク モジュールの呼び出しの例

次の図は、タスク モジュールを表示します。

![タスク モジュール - カスタム フォーム](~/assets/images/task-module/task-module-custom-form.png)

次のコードは、タスク モジュール [のサンプルから適合しています](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample)。

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

これは `submitHandler` 非常に単純で、コンソールの値またはコンソール `err` `result` にエコーされます。

## <a name="submit-the-result-of-a-task-module"></a>タスク モジュールの結果を送信する

この `submitHandler` 関数は Web ページに `TaskInfo.url` 存在し、で使用されます `TaskInfo.url` 。 タスク モジュールを呼び出す際にエラーが発生した場合、関数は直ちに呼び出され、発生したエラーを示す `submitHandler` `err` 文字列 [が表示されます](#task-module-invocation-errors)。 この関数は、ユーザーがタスク モジュールの右上にある X を選択して閉じるときに、文字列を使用して `submitHandler` `err` 呼び出されます。

呼び出しエラーが発生し、ユーザーが X を選択して閉じない場合、ユーザーは終了するとボタンを選択します。 タスク モジュール内の URL かアダプティブ カードかによって、次のセクションでは、発生する内容の詳細を示します。

### <a name="html-or-javascript-taskinfourl"></a>HTML または JavaScript `TaskInfo.url`

ユーザーの入力を検証した後、と呼ばれる `microsoftTeams.tasks.submitTask()` SDK 関数を呼び出します `submitTask()` 。 タスク `submitTask()` モジュールを閉じる必要がある場合Teamsパラメーターなしで呼び出します。 オブジェクトまたは文字列を自分のオブジェクトに渡します `submitHandler` 。

結果を最初のパラメーターとして渡します。 Teams、渡したオブジェクトまたは文字列が where で `submitHandler` `err` `null` `result` 呼び出されます `submitTask()` 。 パラメーターを使用 `submitTask()` して呼び出 `result` す場合は、文字列または文字列の `appId` 配列を渡す必要 `appId` があります。 これにより、Teams送信するアプリが呼び出されたタスク モジュールと同じことを検証できます。

### <a name="adaptive-card-taskinfocard"></a>アダプティブ カード `TaskInfo.card`

タスク モジュールを a で呼び出し、ユーザーがボタンを選択すると、カード内の値がの値 `submitHandler` `Action.Submit` として返されます `result` 。 ユーザーが上部右側の Esc キーまたは X キーを選択すると `err` 、代わりに返されます。 アプリにタブに加えてボットが含まれている場合は、ボットの値をオブジェクトに含 `appId` `completionBotId` `TaskInfo` める必要があります。 ユーザーが入力したアダプティブ カード本文は、ユーザーがボタンを選択すると、メッセージを使用してボット `task/submit invoke` に送信 `Action.Submit` されます。 受信するオブジェクトのスキーマは、タスク/フェッチおよびタスク/送信メッセージで受け取る [スキーマと非常に似ています](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)。 唯一の違いは、JSON オブジェクトのスキーマがアダプティブ カード オブジェクトで、アダプティブ カード オブジェクトを含むオブジェクト[](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)ではなく、アダプティブ カード オブジェクトである点です。

次のセクションでは、タスク モジュールの結果を送信する例を示します。

## <a name="example-of-submitting-the-result-of-a-task-module"></a>タスク モジュールの結果を送信する例

詳細については、タスク モジュールの [HTML フォームを参照してください](#example-of-invoking-a-task-module)。 次のコードは、フォームが定義されている場所の例を示しています。

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

このフォームには 5 つのフィールドがありますが、この例では、3 つの値だけが必要 `name` です。 `email` `favoriteBook`

次のコードは、呼び出す関数 `validateForm()` の例を示しています `submitTask()` 。

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

次のセクションでは、タスク モジュールの呼び出しの問題とそのエラー メッセージを示します。

## <a name="task-module-invocation-errors"></a>タスク モジュール呼び出しのエラー

次の表に、次の値を使用 `err` して受信できる値を示します `submitHandler` 。

| 問題 | エラー メッセージの値 `err` |
| ------- | ------------------------------ |
| 両方の値と `TaskInfo.url` 指定 `TaskInfo.card` された値。 | カードと URL の両方の値が指定されました。 一方または他の両方を使用できますが、両方は許可されません。 |
| 指定も `TaskInfo.url` `TaskInfo.card` 指定もされていません。 | カードまたは URL の値を指定する必要があります。 |
| 無効 `appId` です。 | アプリ ID が無効です。 |
| ユーザーが X ボタンを選択し、閉じる。 | ユーザーがタスク モジュールを取り消したり閉じたりしました。 |

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|タスク モジュールのサンプル タブとボット-V3 | タスク モジュールを作成するためのサンプル。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a>関連項目

[タスク モジュールの呼び出しと終了](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ボットからのタスク モジュールの使用](~/task-modules-and-cards/task-modules/task-modules-bots.md)
