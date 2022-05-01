---
title: Microsoft Teams タブでタスク モジュールを使用する
description: Teams タブからタスク モジュールを呼び出し、Microsoft Teams クライアント SDK を使用してその結果を送信する方法について説明します。 これにはコード サンプルが含まれています。
ms.localizationpriority: high
ms.topic: how-to
keywords: タスク モジュール teams タブ クライアント sdk
ms.openlocfilehash: eb199842a60832e6eb77575a7438cc9f52db6e09
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111228"
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

タブからタスク モジュールを呼び出すには、`microsoftTeams.tasks.startTask()` を使用して [[TaskInfo オブジェクト]](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) とオプションの `submitHandler` コールバック関数を渡します。 2 つの状況を検討する必要があります。

* `TaskInfo.url` の値は URL に設定されます。 タスク モジュール ウィンドウが表示され、`TaskModule.url` がその中に `<iframe>` としてロードされます。 そのページの JavaScript が `microsoftTeams.initialize()` を呼び出します。 ページに `submitHandler` 関数があり、`microsoftTeams.tasks.startTask()` の呼び出し時にエラーが発生した場合、`submitHandler` は、同じことを示すエラー文字列に設定された `err` で呼び出されます。 詳細については、「 [タスク モジュールの呼び出しエラー](#task-module-invocation-errors)」を参照してください。
* `taskInfo.card` の値は、[アダプティブ カードの JSON](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment) です。 ユーザーがアダプティブカードのボタンを閉じるか押したときに呼び出す JavaScript `submitHandler` 関数はありません。 ユーザーが入力したものを受け取る唯一の方法は、結果をボットに渡すことです。 タブからアダプティブ カード タスク モジュールを使用するには、アプリにボットを含め、ユーザーからの応答を取得する必要があります。

次のセクションでは、タスク モジュールを呼び出す例を示します。

## <a name="example-of-invoking-a-task-module"></a>タスク モジュールを呼び出す例

次の画像は、メッセージング拡張機能検索コマンド タスク モジュールを示しています。

:::image type="content" source="../../assets/images/task-module/task-module-custom-form.png" alt-text="タスク モジュールのユーザー設定フォーム":::

次のコードは、[[タスク モジュールのサンプル]](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample) から調整されています。

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

`submitHandler` は非常にシンプルで、`err` または `result` の値をコンソールにエコーします。

## <a name="submit-the-result-of-a-task-module"></a>タスク モジュールの結果を送信する

`submitHandler` 関数は `TaskInfo.url` Web ページにあり、`TaskInfo.url` で使用されます。 タスク モジュールの呼び出し時にエラーが発生した場合、`submitHandler` 関数は、[ エラーが発生した ](#task-module-invocation-errors) を示す `err` 文字列ですぐに呼び出されます。 `submitHandler` 関数は、ユーザーがタスク モジュールの右上にある X を選択して閉じるときに、`err` 文字列で呼び出されます。

呼び出しエラーがなく、ユーザーが X を選択して無視しない場合、ユーザーは完了時にボタンを選択します。 タスク モジュールの URL またはアダプティブ カードのどちらであるかに応じて、次のセクションで何が発生するかについて詳しく説明します。

### <a name="html-or-javascript-taskinfourl"></a>HTML または JavaScript `TaskInfo.url`

ユーザーの入力を検証した後、`submitTask()` と呼ばれる `microsoftTeams.tasks.submitTask()` SDK 関数を呼び出します。 チームにタスク モジュールを閉じさせたいだけの場合は、パラメータなしで `submitTask()` を呼び出します。 オブジェクトまたは文字列を `submitHandler` に渡すことができます。

最初のパラメーターとして結果を渡します。 Teams は `submitHandler` を呼び出します。`err` は `null` で、`result` は `submitTask()` に渡したオブジェクトまたは文字列です。 `result`パラメータを使用して `submitTask()` を呼び出す場合は、`appId` または `appId` 文字列の配列を渡す必要があります。 これにより、Teams は、結果を送信するアプリが呼び出されたタスク モジュールと同じであることを検証できます。

### <a name="adaptive-card-taskinfocard"></a>アダプティブ カード `TaskInfo.card`

`submitHandler` を使用してタスクモジュールを呼び出し、ユーザーが `Action.Submit` ボタンを選択すると、カード内の値が `result` の値として返されます。 ユーザーが右上の Esc キーまたは X を選択すると、代わりに `err` が返されます。 アプリにタブに加えてボットが含まれている場合は、ボットの `appId` を `completionBotId` の値として `TaskInfo` オブジェクトに含めることができます。 ユーザーが入力したアダプティブ カードの本文は、ユーザーが `Action.Submit` ボタンを選択すると、`task/submit invoke` メッセージを使用してボットに送信されます。 受け取るオブジェクトのスキーマは、[ タスク/フェッチおよびタスク/送信メッセージで受け取るスキーマ ](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages) と非常によく似ています。 唯一の違いは、JSON オブジェクトのスキーマが Adaptive Card オブジェクトであるのに対し、[アダプティブ カードがボットで使用される場合](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)としてアダプティブ カード オブジェクトを含むオブジェクトであるということです。

次のセクションでは、タスク モジュールの結果を送信する例を示します。

## <a name="example-of-submitting-the-result-of-a-task-module"></a>タスク モジュールの結果を送信する例

詳細については、 「[タスク モジュールの HTML フォームを](#example-of-invoking-a-task-module)」参照してください。 次のコードは、フォームが定義されている場所の例を示しています。

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

このフォームには 5 つのフィールドがありますが、この例では、`name`、`email`、および `favoriteBook` の 3 つの値のみが必要です。

次のコードは、`submitTask()` を呼び出す `validateForm()` 関数の例を示しています。

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

次の表に、`submitHandler` が受け取ることができる `err` の可能性のある値を示します。

| 問題 | `err` の値であるエラー メッセージ |
| ------- | ------------------------------ |
| `TaskInfo.url` と `TaskInfo.card` の両方の値が指定されました。 | カードおよび URL の両方の値が指定されました。両方ではなく、どちらか一方が許可されます。 |
| `TaskInfo.url` も `TaskInfo.card` も指定されていません。 | カードまたは URL の値を指定する必要があります。 |
| 無効な `appId` | アプリ ID が無効です。 |
| ユーザーが選択した [X] ボタンを閉じます。 | ユーザーがタスク モジュールをキャンセルまたは終了しました。 |

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|タスク モジュールのサンプル タブとボット - V3 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ボットでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>関連項目

[タスク モジュールを呼び出して閉じる](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
