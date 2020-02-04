---
title: Microsoft Teams のタブでタスクモジュールを使用する
description: Microsoft Teams クライアント SDK を使用して Teams タブからタスクモジュールを呼び出す方法について説明します。
keywords: タスクモジュールチームタブクライアント sdk
ms.openlocfilehash: e10958195713f338a9b5e0a0672d8b6a29da9264
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675059"
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

タスクモジュールをタブから呼び出して、 `microsoftTeams.tasks.startTask()` [taskinfo オブジェクト](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)とオプション`submitHandler`のコールバック関数を渡す方法。 前述したように、次の2つのケースを考慮する必要があります。

1. の`TaskInfo.url`値は、URL に設定されます。 タスクモジュールウィンドウが表示さ`TaskModule.url`れ、そのウィンドウ`<iframe>`内に読み込まれます。 そのページの JavaScript がを`microsoftTeams.initialize()`呼び出す必要があります。 `submitHandler`ページ上に関数があり、呼び出し`microsoftTeams.tasks.startTask()`時にエラーが発生した場合`submitHandler`は、[以下](#task-module-invocation-errors)に`err`示すように、エラーを示すエラー文字列に set を指定して呼び出されます。
1. の`taskInfo.card`値は、[アダプティブカードの JSON](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)です。 この例では、ユーザーがアダプティブカード`submitHandler`上のボタンを閉じたり押したりしたときに呼び出す JavaScript 関数はありません。ユーザーが入力した結果を取得する唯一の方法は、結果を bot に渡すことです。 タブからアダプティブカードタスクモジュールを使用するには、アプリがユーザーから情報を取得する bot を含んでいる必要があります。 これについては、以下で説明します。

## <a name="example-invoking-a-task-module"></a>例: タスクモジュールを呼び出す

次のコードは、[タスクモジュールサンプル](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples)から適用されます。 タスクモジュールは以下のようになります。

![タスクモジュール-ユーザー設定フォーム](~/assets/images/task-module/task-module-custom-form.png)

`submitHandler`は非常に単純です。または`err` `result` 、コンソールの値のみを echo 出力します。

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

関数`submitHandler`は、で`TaskInfo.url`使用されます。 関数`submitHandler`は`TaskInfo.url` web ページに存在します。 タスクモジュールの呼び出し時にエラーが発生した`submitHandler`場合は、[エラーが発生](#task-module-invocation-errors)し`err`たことを示す文字列を使用して、関数が直ちに呼び出されます。 この`submitHandler`関数は、ユーザーがタスク`err`モジュールの右上にある X を押したときに、文字列を使用しても呼び出されます。

呼び出しエラーがなく、ユーザーが X を押してそれを破棄しなかった場合、ユーザーは終了時にボタンを押したことになります。 タスクモジュールの URL であるか、アダプティブカードであるかによって、次のようになります。

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript (`TaskInfo.url`)

ユーザーが入力したことを確認したら、SDK `microsoftTeams.tasks.submitTask()`関数を呼び出します (読みやすさ`submitTask()`を目的として、以降を参照)。 タスクモジュールを`submitTask()`閉じるだけの場合は、パラメーターを指定せずに呼び出すことができ`submitHandler`ますが、ほとんどの場合、オブジェクトまたは文字列をに渡すことが必要になります。

結果を最初のパラメーターとして渡します。 Teams は、 `submitHandler`を`err`呼び出し`null` `result` 、渡されたオブジェクト/文字列になり`submitTask()`ます。 `result`パラメーターを指定し`submitTask()`て呼び出しを行う場合`appId`は、または文字列の`appId`配列を渡す**必要があり**ます。これにより、チームは、結果を送信しているアプリがタスクモジュールを呼び出したものと同じであることを確認できます。

### <a name="adaptive-card-taskinfocard"></a>アダプティブカード (`TaskInfo.card`)

でタスクモジュールを呼び出した場合`submitHandler`、ユーザーが`Action.Submit`ボタンを押すと、カード内の値はの`result`値として返されます。 ユーザーが Esc ボタンを押すか、X を押すと`err` 、代わりにが返されます。 または、アプリにタブに加えて bot が含まれている場合は、 `appId`その bot のを`TaskInfo`オブジェクト内の`completionBotId`の値として簡単に含めることができます。 ユーザーが`Action.Submit`ボタンを押したときに、ユーザーが入力したアダプティブカードの本文が、 `task/submit invoke`メッセージによって bot に送信されます。 受け取るオブジェクトのスキーマは、[タスク/フェッチおよびタスク/送信メッセージのために受け取るスキーマ](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)によく似ています。唯一の違いは、JSON オブジェクトのスキーマは、インテリカードを[bot と組み合わせて使用する場合](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)と同様に、アダプティブカードオブジェクトを*格納*しているオブジェクトではなく、アダプティブカードオブジェクトであるということです。

## <a name="example-submitting-the-result-of-a-task-module"></a>例: タスクモジュールの結果を提出する

前述の[タスクモジュールのフォーム](#example-invoking-a-task-module)を HTML フォームで取り消します。 フォームが定義されている場所は次のとおりです。

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

このフォームには5つのフィールドがありますが、この例では、、 `name` `email`、およびの3つのフィールド`favoriteBook`の値のみを対象としています。

を呼び出す`submitTask()`関数`validateForm()`を次に示します。

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

## <a name="task-module-invocation-errors"></a>タスクモジュール呼び出しエラー

で受信可能な値`err`は`submitHandler`次のとおりです。

| 問題 | エラーメッセージ (の`err`値) |
| ------- | ------------------------------ |
| と`TaskInfo.card`の両方`TaskInfo.url`の値が指定されました。 | カードと url の両方の値が指定されています。 どちらか一方のみが許可されます。 |
| `TaskInfo.url`また`TaskInfo.card`は指定されません。 | "カードまたは url のいずれかに値を指定する必要があります。" |
| 無効`appId`です。 | "無効な appId"。 |
| ユーザーが X ボタンを押して、それを閉じる。 | "ユーザーがタスクモジュールを取り消しまたは終了しました。" |
