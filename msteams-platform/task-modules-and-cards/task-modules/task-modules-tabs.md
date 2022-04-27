---
title: Microsoft Teams タブでタスク モジュールを使用する
description: Teams タブからタスク モジュールを呼び出し、Microsoft Teams クライアント SDK を使用してその結果を送信する方法について説明します。 これにはコード サンプルが含まれています。
ms.localizationpriority: medium
ms.topic: how-to
keywords: タスク モジュール teams タブ クライアント sdk
ms.openlocfilehash: 63ac1df5b9cdbbba46ba204103a9a5c989b3a323
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073759"
---
# <a name="use-task-modules-in-tabs"></a>タブでタスク モジュールを使用する

タブにタスク モジュールを追加して、データ入力を必要とするワークフローのユーザー エクスペリエンスを簡略化します。 タスク モジュールを使用すると、Microsoft Teams-Aware ポップアップに入力を収集できます。 その良い例として、Planner カードの編集があります。 タスク モジュールを使用して、同様のエクスペリエンスを作成できます。

タスク モジュール機能をサポートするために、[Teams クライアント SDK](/javascript/api/overview/msteams-client) に 2 つの新しい関数が追加されます。 次のコードは、これら 2 つの関数の例を示しています。

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

タブ `microsoftTeams.tasks.startTask()` からタスク モジュールを呼び出すには、 [TaskInfo オブジェクト](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) とオプション `submitHandler` のコールバック関数を渡します。 考慮すべきケースは 2 つあります。

* の値 `TaskInfo.url` は URL に設定されます。 タスク モジュール ウィンドウが表示され、 `TaskModule.url` その中として `<iframe>` 読み込まれます。 そのページの JavaScript が呼び出されます `microsoftTeams.initialize()`。 ページに関数があり `submitHandler` 、呼び出 `microsoftTeams.tasks.startTask()`し時にエラーが発生した場合は、 `submitHandler` 同じエラー文字列に設定して呼び出されます `err` 。 詳細については、「 [タスク モジュールの呼び出しエラー](#task-module-invocation-errors)」を参照してください。
* の値 `taskInfo.card` は [、アダプティブ カードの JSON です](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)。 ユーザーがアダプティブ カードのボタンを閉じたり押したりしたときに呼び出す JavaScript `submitHandler` 関数はありません。 ユーザーが入力したものを受け取る唯一の方法は、結果をボットに渡すことです。 タブからアダプティブ カード タスク モジュールを使用するには、アプリにボットを含め、ユーザーからの応答を取得する必要があります。

次のセクションでは、タスク モジュールを呼び出す例を示します。

## <a name="example-of-invoking-a-task-module"></a>タスク モジュールを呼び出す例

次の図は、タスク モジュールを示しています。

:::image type="content" source="../../assets/images/task-module/task-module-custom-form.png" alt-text="タスク モジュールのユーザー設定フォーム":::

次のコードは、 [タスク モジュールのサンプル](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample)から調整されています。

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

これは `submitHandler` 非常にシンプルで、本体の `err` 値または `result` 本体にエコーされます。

## <a name="submit-the-result-of-a-task-module"></a>タスク モジュールの結果を送信する

この関数は `submitHandler` Web ページに`TaskInfo.url`存在し、.`TaskInfo.url` タスク モジュールの呼び出し時にエラーが発生した場合、 `submitHandler` 関数は、発生したエラーを `err` 示す文字列ですぐに呼び出 [されます](#task-module-invocation-errors)。 ユーザー `submitHandler` がタスク モジュールの右上にある X を選択して閉じると、この関数は文字列で呼び出 `err` されます。

呼び出しエラーがなく、ユーザーが X を選択して無視しない場合、ユーザーは完了時にボタンを選択します。 タスク モジュールの URL かアダプティブ カードかに応じて、次のセクションでは、発生する内容の詳細を説明します。

### <a name="html-or-javascript-taskinfourl"></a>HTML または JavaScript `TaskInfo.url`

ユーザーの入力を検証した後、次と`submitTask()`呼ばれる SDK 関数を呼び出`microsoftTeams.tasks.submitTask()`します。 タスク モジュールを閉じるTeams場合は、パラメーターを指定せずに呼び出`submitTask()`します。 オブジェクトまたは文字列 `submitHandler`を渡すことができます。

最初のパラメーターとして結果を渡します。 Teamsは、`submitHandler`渡したオブジェクトまたは文字列の場所`err``null`と`result`場所を`submitTask()`呼び出します。 パラメーターを使用して`result`呼び出す`submitTask()`場合は、文字列の配列または文字列の`appId`配列を`appId`渡す必要があります。 これにより、結果を送信するアプリが呼び出されたタスク モジュールと同じであることを検証するTeamsが許可されます。

### <a name="adaptive-card-taskinfocard"></a>アダプティブ カード `TaskInfo.card`

タスク モジュールを呼び出し、`submitHandler`ユーザーがボタンを`Action.Submit`選択すると、カード内の値が .`result` ユーザーが右上にある Esc キーまたは X キーを選択した場合は、 `err` 代わりに返されます。 アプリにタブに加えてボットが含まれている場合は、オブジェクトの値`completionBotId``TaskInfo`としてボットを含`appId`めることができます。 ユーザーが入力したアダプティブ カード本体は、ユーザーがボタンを選択したときにメッセージを `task/submit invoke` 使用してボットに `Action.Submit` 送信されます。 受信するオブジェクトのスキーマは、 [タスク/フェッチおよびタスク/送信メッセージに対して受信するスキーマと](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)よく似ています。 唯一の違いは、JSON オブジェクトのスキーマがアダプティブ カード オブジェクトであり、アダプティブ カードが [ボットで使用される場合と同様に、アダプティブ カード](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages) オブジェクトを含むオブジェクトとは対照的です。

次のセクションでは、タスク モジュールの結果を送信する例を示します。

## <a name="example-of-submitting-the-result-of-a-task-module"></a>タスク モジュールの結果を送信する例

詳細については、 [タスク モジュールの HTML フォームを](#example-of-invoking-a-task-module)参照してください。 次のコードは、フォームが定義されている場所の例を示しています。

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

このフォームには 5 つのフィールドがありますが、この例では 3 つの値のみが必要です。値は 、 `name`. `email``favoriteBook`

次のコードは、呼び出`submitTask()`す関数の例を`validateForm()`示しています。

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

次のセクションでは、タスク モジュールの呼び出しに関する問題とそのエラー メッセージについて説明します。

## <a name="task-module-invocation-errors"></a>タスク モジュール呼び出しのエラー

次の表は、次の `err` ユーザーが受け取ることができる値を `submitHandler`示しています。

| 問題 | の値であるエラー メッセージ `err` |
| ------- | ------------------------------ |
| 両方 `TaskInfo.url` の値と `TaskInfo.card` 指定された値。 | カードと URL の両方の値が指定されました。 どちらか一方は許可されますが、両方は許可されません。 |
| どちらも指定も`TaskInfo.url``TaskInfo.card`しません。 | カードまたは URL の値を指定する必要があります。 |
| 無効です `appId`。 | アプリ ID が無効です。 |
| ユーザーが選択した [X] ボタンを閉じます。 | ユーザーがタスク モジュールをキャンセルまたは終了しました。 |

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|タスク モジュールのサンプル タブとボット-V3 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ボットからのタスク モジュールの使用](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>関連項目

[タスク モジュールを呼び出して閉じる](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
