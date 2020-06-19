---
title: Microsoft Teams のタブでタスクモジュールを使用する
description: Microsoft Teams クライアント SDK を使用して Teams タブからタスクモジュールを呼び出す方法について説明します。
keywords: タスクモジュールチームタブクライアント sdk
ms.openlocfilehash: e10958195713f338a9b5e0a0672d8b6a29da9264
ms.sourcegitcommit: 2a84a3c8b10771e37ce51bf603a967633947a3e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2020
ms.locfileid: "44801199"
---
# <a name="using-task-modules-in-tabs"></a>タブでタスクモジュールを使用する

タスクモジュールをタブに追加すると、データ入力を必要とするすべてのワークフローについて、ユーザーの操作が大幅に簡素化されます。 タスクモジュールを使用すると、チーム対応のポップアップで入力を収集できます。 プランナーカードを編集することをよく例を示します。タスクモジュールを使用して、同様の操作を作成できます。

タスクモジュール機能をサポートするために、 [Microsoft Teams クライアント SDK](/javascript/api/overview/msteams-client)に2つの新しい関数が追加されました。

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

それぞれがどのように機能するかを見てみましょう。

## <a name="invoking-a-task-module-from-a-tab"></a>タブからタスクモジュールを呼び出す

タスクモジュールをタブから呼び出し `microsoftTeams.tasks.startTask()` て、 [taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)とオプションの `submitHandler` コールバック関数を渡す方法。 前述したように、次の2つのケースを考慮する必要があります。

1. の値 `TaskInfo.url` は、URL に設定されます。 タスクモジュールウィンドウが表示され、 `TaskModule.url` そのウィンドウ内に読み込まれ `<iframe>` ます。 そのページの JavaScript がを呼び出す必要があり `microsoftTeams.initialize()` ます。 ページ上に関数があり、呼び出し時にエラーが発生した場合は、以下に示すように、エラーを `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` 示すエラー文字列に[below](#task-module-invocation-errors)set を指定して呼び出されます。
1. の値 `taskInfo.card` は、[アダプティブカードの JSON](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)です。 この場合、 `submitHandler` ユーザーがアダプティブカード上でボタンを閉じたり押したりしたときに呼び出す JavaScript 関数は存在しません。ユーザーが入力した内容を受信するには、結果を bot に渡す以外に方法はありません。 タブからアダプティブカードタスクモジュールを使用するには、アプリがユーザーから情報を取得する bot を含んでいる必要があります。 これについては、以下で説明します。

## <a name="example-invoking-a-task-module"></a>例: タスクモジュールを呼び出す

次のコードは、[タスクモジュールサンプル](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples)から適用されます。 タスクモジュールは以下のようになります。

![タスクモジュール-ユーザー設定フォーム](~/assets/images/task-module/task-module-custom-form.png)

は `submitHandler` 非常に単純で、またはコンソールの値をエコーするだけです `err` `result` 。

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

## <a name="submitting-the-result-of-a-task-module"></a>タスクモジュールの結果を提出する

`submitHandler`関数は、で使用され `TaskInfo.url` ます。 `submitHandler`関数は web ページに存在し `TaskInfo.url` ます。 タスクモジュールの呼び出し時にエラーが発生した場合は、 `submitHandler` `err` [エラーが発生した](#task-module-invocation-errors)ことを示す文字列を使用して、関数が直ちに呼び出されます。 この `submitHandler` 関数は、 `err` ユーザーがタスクモジュールの右上にある X を押したときに、文字列を使用しても呼び出されます。

呼び出しエラーがなく、ユーザーが X を押してそれを破棄しなかった場合、ユーザーは終了時にボタンを押したことになります。 タスクモジュールの URL であるか、アダプティブカードであるかによって、次のようになります。

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript ( `TaskInfo.url` )

ユーザーが入力したことを確認したら、 `microsoftTeams.tasks.submitTask()` SDK 関数を呼び出し `submitTask()` ます (読みやすさを目的として、以降を参照)。 `submitTask()`タスクモジュールを閉じるだけの場合は、パラメーターを指定せずに呼び出すことができますが、ほとんどの場合、オブジェクトまたは文字列をに渡すことが必要になり `submitHandler` ます。

結果を最初のパラメーターとして渡します。 Teams は、を呼び出し、 `submitHandler` `err` 渡され `null` `result` たオブジェクト/文字列になり `submitTask()` ます。 パラメーターを指定して呼び出しを行う場合 `submitTask()` `result` は、または文字列の配列を渡す**必要があり** `appId` `appId` ます。これにより、チームは、結果を送信しているアプリがタスクモジュールを呼び出したものと同じであることを確認できます。

### <a name="adaptive-card-taskinfocard"></a>アダプティブカード ( `TaskInfo.card` )

でタスクモジュールを呼び出した場合 `submitHandler` 、ユーザーがボタンを押すと、 `Action.Submit` カード内の値はの値として返され `result` ます。 ユーザーが Esc ボタンを押すか、X を押すと、 `err` 代わりにが返されます。 または、アプリにタブに加えて bot が含まれている場合は、その `appId` bot のをオブジェクト内のの値として簡単に含めることができ `completionBotId` `TaskInfo` ます。 ユーザーがボタンを押したときに、ユーザーが入力したアダプティブカードの本文が、メッセージによって bot に送信され `task/submit invoke` `Action.Submit` ます。 受け取るオブジェクトのスキーマは、[タスク/フェッチおよびタスク/送信メッセージのために受け取るスキーマ](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)によく似ています。唯一の違いは、JSON オブジェクトのスキーマは、インテリカードを[bot と組み合わせて使用する場合](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)と同様に、アダプティブカードオブジェクトを*格納*しているオブジェクトではなく、アダプティブカードオブジェクトであるということです。

## <a name="example-submitting-the-result-of-a-task-module"></a>例: タスクモジュールの結果を提出する

前述の[タスクモジュールのフォーム](#example-invoking-a-task-module)を HTML フォームで取り消します。 フォームが定義されている場所は次のとおりです。

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

このフォームには5つのフィールドがありますが、この例では、、、およびの3つのフィールドの値のみを対象としています。 `name` `email` `favoriteBook`

を呼び出す関数を次に示し `validateForm()` `submitTask()` ます。

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

で受信可能な値は次のとおりです `err` `submitHandler` 。

| 問題 | エラーメッセージ (の値 `err` ) |
| ------- | ------------------------------ |
| との両方の値 `TaskInfo.url` `TaskInfo.card` が指定されました。 | カードと url の両方の値が指定されています。 どちらか一方のみが許可されます。 |
| `TaskInfo.url`または `TaskInfo.card` 指定されません。 | "カードまたは url のいずれかに値を指定する必要があります。" |
| 無効 `appId` です。 | "無効な appId"。 |
| ユーザーが X ボタンを押して、それを閉じる。 | "ユーザーがタスクモジュールを取り消しまたは終了しました。" |
