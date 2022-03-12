---
title: '[タスク モジュール] タブでタスク モジュールMicrosoft Teamsする'
description: 各タブからタスク モジュールを呼び出し、Teams SDK を使用して結果を送信するMicrosoft Teams説明します。 コード サンプルが含まれています。
ms.localizationpriority: medium
ms.topic: how-to
keywords: タスク モジュールチームがクライアント SDK をタブする
ms.openlocfilehash: 43b58a4f8ec1176c2d931f130a33c6610a078187
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453643"
---
# <a name="use-task-modules-in-tabs"></a>タブでタスク モジュールを使用する

タブにタスク モジュールを追加して、データ入力を必要とするワークフローに対するユーザー エクスペリエンスを簡略化します。 タスク モジュールを使用すると、Microsoft のポップアップで入力Teams-Awareを収集できます。 この例の良い例は、Planner カードの編集です。 タスク モジュールを使用して、同様のエクスペリエンスを作成できます。

タスク モジュール機能をサポートするために、クライアント SDK に 2 つの新[しいTeams追加されます](/javascript/api/overview/msteams-client)。 次のコードは、これら 2 つの関数の例を示しています。

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

タブからタスク モジュールを呼び出す場合は、`microsoftTeams.tasks.startTask()`[TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) オブジェクトとオプションのコールバック関数を渡します`submitHandler`。 次の 2 つのケースを考慮する必要があります。

* の値は `TaskInfo.url` URL に設定されます。 タスク モジュール ウィンドウが表示され、 `TaskModule.url` 内部として読み `<iframe>` 込まれます。 そのページ呼び出しの JavaScript `microsoftTeams.initialize()`。 ページに関数`submitHandler`が存在`microsoftTeams.tasks.startTask()``submitHandler``err`し、呼び出し時にエラーが発生した場合は、同じことを示すエラー文字列に設定して呼び出されます。 詳細については、「タスク モジュールの [呼び出しエラー」を参照してください](#task-module-invocation-errors)。
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

これは `submitHandler` 非常に単純で、コンソールの値または `err` コンソールに `result` エコーされます。

## <a name="submit-the-result-of-a-task-module"></a>タスク モジュールの結果を送信する

この `submitHandler` 関数は Web ページに存在 `TaskInfo.url` し、で使用されます `TaskInfo.url`。 タスク モジュールを呼び出す際`submitHandler``err`にエラーが発生した場合、関数は、エラーが発生したことを示す文字列ですぐに[呼び出されます](#task-module-invocation-errors)。 この `submitHandler` 関数は、ユーザーがタスク モジュール `err` の右上にある X を選択して閉じるときに、文字列を使用して呼び出されます。

呼び出しエラーが発生し、ユーザーが X を選択して閉じない場合、ユーザーは終了するとボタンを選択します。 タスク モジュール内の URL かアダプティブ カードかによって、次のセクションでは、発生する内容の詳細を示します。

### <a name="html-or-javascript-taskinfourl"></a>HTML または JavaScript `TaskInfo.url`

ユーザーの入力を検証した後、と呼ばれる `microsoftTeams.tasks.submitTask()` SDK 関数を呼び出します `submitTask()`。 タスク `submitTask()` モジュールを閉じる必要がある場合Teamsパラメーターなしで呼び出します。 オブジェクトまたは文字列を自分のオブジェクトに渡します `submitHandler`。

結果を最初のパラメーターとして渡します。 Teams、渡`submitHandler`したオブジェクト`result` `err` `null`または文字列が where で呼び出されます。`submitTask()` パラメーターを使用して `submitTask()` 呼び出す `result` 場合は、文字列または文字列の `appId` 配列を渡す必要 `appId` があります。 これにより、Teams送信するアプリが呼び出されたタスク モジュールと同じことを検証できます。

### <a name="adaptive-card-taskinfocard"></a>アダプティブ カード `TaskInfo.card`

タスク `submitHandler` `Action.Submit` モジュールを a で呼び出し、ユーザーがボタンを選択すると、カード内の値がの値として返されます `result`。 ユーザーが上部右側の Esc キーまたは X キーを `err` 選択すると、代わりに返されます。 アプリにタブに加`appId``completionBotId`えてボットが含まれている場合は、ボットの値をオブジェクトに含める必要`TaskInfo`があります。 ユーザーが入力したアダプティブ `task/submit invoke` カード本文は、ユーザーがボタンを選択すると、メッセージを使用してボットに送信 `Action.Submit` されます。 受信するオブジェクトのスキーマは、タスク/フェッチおよびタスク/送信メッセージで受け取る [スキーマと非常に似ています](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)。 唯一の違いは、JSON オブジェクトのスキーマがアダプティブ カード オブジェクトで、アダプティブ カード オブジェクトを含むオブジェクトではなく、アダプティブ カード オブジェクトである点[です。](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)

次のセクションでは、タスク モジュールの結果を送信する例を示します。

## <a name="example-of-submitting-the-result-of-a-task-module"></a>タスク モジュールの結果を送信する例

詳細については、タスク モジュールの [HTML フォームを参照してください](#example-of-invoking-a-task-module)。 次のコードは、フォームが定義されている場所の例を示しています。

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

このフォームには 5 つのフィールドがありますが、この例では、3 つの値だけが必要です。 `name``email``favoriteBook`

次のコードは、呼び出す関数の例 `validateForm()` を示しています `submitTask()`。

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

次の表に、次の値を `err` 使用して受信できる値を示します `submitHandler`。

| 問題 | エラー メッセージの値 `err` |
| ------- | ------------------------------ |
| 両方の値と `TaskInfo.url` 指定 `TaskInfo.card` された値。 | カードと URL の両方の値が指定されました。 一方または他の両方を使用できますが、両方は許可されません。 |
| 指定も `TaskInfo.url` 指定 `TaskInfo.card` もされていません。 | カードまたは URL の値を指定する必要があります。 |
| 無効です `appId`。 | アプリ ID が無効です。 |
| ユーザーが X ボタンを選択し、閉じる。 | ユーザーがタスク モジュールを取り消したり閉じたりしました。 |

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|タスク モジュールのサンプル タブとボット-V3 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ボットからのタスク モジュールの使用](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>関連項目

[タスク モジュールを呼び出して閉じる](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
