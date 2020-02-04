---
title: タスクモジュールとは
author: clearab
description: Microsoft Teams アプリからユーザーに情報を収集または表示するためのモーダルポップアップエクスペリエンスを追加します。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 22fdc7a9dab1ff6f27e2b0d144e54676b6cca50e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675060"
---
# <a name="what-are-task-modules"></a>タスクモジュールとは

タスクモジュールを使用すると、Teams アプリケーションでモーダルポップアップエクスペリエンスを作成できます。 ポップアップの内部では、独自のカスタム HTML/JavaScript コードを実行し`<iframe>`たり、YouTube や Microsoft Stream ビデオなどのベースのウィジェットを表示したり、[アダプティブカード](/adaptive-cards/)を表示したりすることができます。 これらは特に、タスクを開始および完了したり、ビデオや Power BI ダッシュボードのようなリッチ情報を表示したりするのに便利です。 多くの場合、ポップアップは、タブや会話ベースのボットのようなタスクを開始および完了するユーザーのために、より自然に表示されます。

タスクモジュールは、Microsoft Teams のタブの基礎に基づいて構築されています。これらは基本的にはポップアップウィンドウ内のタブです。 これらは同じ SDK を使用します。そのため、タブを構築した場合は、タスクモジュールを作成する方法が既に90% になっています。

タスクモジュールは、次の3つの方法で呼び出すことができます。

* **チャネルまたは個人用タブ。** Microsoft Teams のタブ SDK を使用すると、タブのボタン、リンク、またはメニューからタスクモジュールを呼び出すことができます。[これについては、ここで詳しく説明し](~/task-modules-and-cards/task-modules/task-modules-tabs.md)ます。
* **Bot.** Bot から送信された[カード](~/task-modules-and-cards/cards/cards-reference.md)のボタン。 これは、ユーザーが bot を使用していることを確認するためにチャネル内のすべてのユーザーが必要ない場合に特に便利です。 たとえば、ユーザーがチャネル内の投票に応答する場合、作成中の投票の記録を表示するのはそれほど便利ではありません。 [これについては、ここで詳しく説明します。](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **深いリンクから Teams の外側。** 任意の場所からタスクモジュールを呼び出すための Url を作成することもできます。 [これについては、ここで詳しく説明します。](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a>タスクモジュールの外観

Bot から呼び出された場合のタスクモジュールは次のようになります (色の付いた長方形と番号付き円はありません)。

![タスクモジュールの例](~/assets/images/task-module/task-module-example.png)

これについて説明します。

1. アプリの[ `color`アイコン](~/resources/schema/manifest-schema.md#icons)。
2. アプリの[ `short`名前](~/resources/schema/manifest-schema.md#name)。
3. `title` [Taskinfo オブジェクト](#the-taskinfo-object)のプロパティで指定されたタスクモジュールのタイトル。
4. タスクモジュールの [閉じる/キャンセル] ボタン。 ユーザーがこのコードを押すと、[ここで](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)説明`err`したように、アプリはイベントを受け取ります。 (現時点では、タスクモジュールが bot から呼び出されたとき**に、この**イベントを検出することはできません)。
5. 青い四角形は、 `url` [taskinfo オブジェクト](#the-taskinfo-object)のプロパティを使用して独自の web ページを読み込む場合に、web ページが表示される場所です。 詳細については、以下の「[タスクモジュールのサイズ変更](#task-module-sizing)」セクションを参照してください。
6. `card` [Taskinfo オブジェクト](#the-taskinfo-object)のプロパティを使用してアダプティブカードを表示している場合は、スペースが自動的に追加されます。それ以外の場合は、[自分で処理](#task-module-css-for-htmljavascript-task-modules)する必要があります。
7. アダプティブカードボタンがここに表示されます。 独自のページを使用している場合は、独自のボタンを作成する必要があります。

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>タスクモジュールの呼び出しと消去の概要

タスクモジュールは、タブ、ボット、またはディープリンクから呼び出すことができ、一方で表示されるものは HTML またはアダプティブカードのどちらかになります。そのため、その呼び出し方法やユーザー操作の結果を処理する方法について、柔軟性が高くなります。 次の表は、この機能の概要を示しています。

| **呼び出しを経由する...** | **タスクモジュールは HTML/JavaScript** | **タスクモジュールはアダプティブカード** |
| --- | --- | --- |
| **タブ内の JavaScript** | 1. オプション`submitHandler(err, result)`のコールバック関数で`tasks.startTask()` Teams クライアント SDK 関数を使用する <br/><br/> 2. タスクモジュールコードで、ユーザーが終了したら、 `tasks.submitTask()` `result`オブジェクトをパラメーターとして Teams SDK 関数を呼び出します。 で`submitHandler` `tasks.startTask()`コールバックが指定されていた場合`result` 、Teams はそれをパラメーターとして呼び出します。<br/><br/> 3. 呼び出し`tasks.startTask()`時にエラーが発生した場合`submitHandler`は、代わりに`err`文字列で関数が呼び出されます。 <br/><br/> 4. そのケースを呼び出し`completionBotId` `teams.startTask()`たときに、そのケース`result`を bot に送信するように指定することもできます。 | 1. [Taskinfo オブジェクト](#the-taskinfo-object)を使用し`tasks.startTask()`て Teams クライアント SDK 関数を`TaskInfo.card`呼び出し、[タスクモジュール] ポップアップに表示するアダプティブカードの JSON を格納します。 <br/><br/> 2 `submitHandler` . で`tasks.startTask()`コールバックが指定されていた場合、 `err`を呼び出したときにエラーが発生`tasks.startTask()`した場合、またはユーザーが右上の X を使用してタスクモジュールのポップアップを閉じた場合、Teams は文字列を使用して呼び出します。 <br/><br/> 3. ユーザーが [送信] ボタンを押すと、その`data`オブジェクトはの`result`値として返されます。 |
| **[ボットカード] ボタン** | 1つのボットカードボタンは、ボタンの種類に応じて、ディープリンク URL、またはメッセージを`task/fetch`送信する2つの方法で、タスクモジュールを呼び出すことができます。 深いリンク Url のしくみについては、以下を参照してください。 <br/><br/> 2. ボタンの`type`アクション`task/fetch` (`Action.Submit`アダプティブカード用のボタンの種類) がある場合`task/fetch invoke`は、bot にイベント (カバーの下の HTTP POST) が送信され、bot は http 200 を使用して post に応答し、ボットは[taskinfo オブジェクト](#the-taskinfo-object)のラッパーを含む応答本文に応答します。 これについては[、「task/fetch を使用してタスクモジュールを呼び出す](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch)」で詳しく説明されています。<br/><br/> 3. Teams には、タスクモジュールが表示されます。ユーザーが終了したら、 `tasks.submitTask()` `result`オブジェクトをパラメーターとして Teams SDK 関数を呼び出します。 <br/><br/> 4. この bot は、 `task/submit invoke` `result`オブジェクトを含むメッセージを受信します。 `task/submit`メッセージに返信するには、次の3つの方法があります。そのためには、何もしない (タスクが正常に完了した) か、ユーザーにメッセージをポップアップウィンドウで表示するか、または別のタスクモジュールウィンドウ (つまりウィザードのような操作を作成する) を呼び出します。 この3つのオプションについ[ては、「タスク/送信に関する詳細な説明」](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)を参照してください。 | 1. Bot フレームワークカードのボタンと同様に、アダプティブカード上のボタンは、タスクモジュールを呼び出すための`Action.openUrl` 2 つの方法`task/fetch`を`Action.Submit`サポートしています。ボタンを使用した深いリンク url とボタンを使用する方法です。 <br/><br/> 2. アダプティブカードを使用したタスクモジュールは、HTML/JavaScript のケースと同じように動作します (左を参照)。 主な違いは、アダプティブカードを使用しているときに JavaScript が存在しないため、を呼び`tasks.submitTask()`出すことができないということです。 代わりに、チームはから`data` `Action.Submit`オブジェクトを取得し、それを`task/submit`イベントのペイロードとして返します ([ここで](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)説明します)。 |
| **ディープリンクの URL** <br/>[URL 構文](#task-module-deep-link-syntax) | 1. Teams がタスクモジュールを呼び出します。ディープリンクの`url`パラメーターで指定`<iframe>`されたの内部に表示される URL。 コールバックは`submitHandler`ありません。 <br/><br/> 2. タスクモジュールのページの JavaScript 内で、 `tasks.submitTask()` `result`オブジェクトをパラメーターとして閉じます。これは、タブまたはボットカードボタンから呼び出すときと同じです。 ただし、完了ロジックは少し異なります。 完了ロジックがクライアント上に存在する場合 (bot がない場合)、コールバックがない`submitHandler`ので、へ`tasks.submitTask()`の呼び出しの前のコードにすべての完了ロジックが含まれている必要があります。 呼び出しエラーはコンソールによってのみ報告されます。 Bot がある場合は、deep link で`completionBotId`パラメーターを指定して、イベントを`result` `task/submit`使用してオブジェクトを送信できます。 | 1. Teams がタスクモジュールを呼び出します。アダプティブカードの JSON カード本文は、ディープリンクの`card`パラメーターの URL エンコードされた値として指定されます。 <br/><br/> 2. ユーザーがタスクモジュールを閉じるには、タスクモジュールの右上にある [X `Action.Submit` ] をクリックするか、カードのボタンを押します。 を呼び出すこと`submitHandler`はできないので、アダプティブカードフィールドの値をに送信する bot が必要です。 ディープリンクの`completionBotId`パラメーターを使用して、 `task/submit invoke`イベントを使用してデータを送信する bot を指定します。 |

> [!NOTE]
> JavaScript からのタスクモジュールの呼び出しは、mobile ではサポートされていません。

## <a name="the-taskinfo-object"></a>TaskInfo オブジェクト

オブジェクト`TaskInfo`には、タスクモジュールのメタデータが含まれています。 オブジェクト定義は以下のとおりです。 (En 埋め込み`url` iFrame の場合) または`card` (アダプティブカードの場合) のいずれかを定義**する必要があり**ます。

| 属性 | 型 | 説明 |
| --- | --- | --- |
| `title` | string | アプリ名の下に表示され、アプリアイコンの右側に表示されます。 |
| `height` | number または string | タスクモジュールの高さを表す数値をピクセル、また`small` `medium`は、または`large`で指定できます。 [高さと幅を処理する方法については、以下を参照して](#task-module-sizing)ください。 |
| `width` | number または string | タスクモジュールの幅をピクセル、また`small` `medium`は、、または`large`の数値で指定できます。 [高さと幅を処理する方法については、以下を参照して](#task-module-sizing)ください。 |
| `url` | string | タスクモジュール内に`<iframe>`読み込まれたページの URL。 URL のドメインは、アプリのマニフェストのアプリの[Validdomains 配列](~/resources/schema/manifest-schema.md#validdomains)内にある必要があります。 |
| `card` | アダプティブカードまたはアダプティブカードのボットカード添付ファイル | タスクモジュールに表示されるアダプティブカードの JSON。 Bot から呼び出している場合は、Bot フレームワーク`attachment`オブジェクトでアダプティブカード JSON を使用する必要があります。 タブからは、アダプティブカードのみを使用します。 [次に例を示します。](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | クライアントがタスクモジュール機能をサポートしていない場合、この URL はブラウザタブで開かれます。 |
| `completionBotId` | string | ユーザーのタスクモジュールとの対話結果をに送信する bot アプリ ID を指定します。 指定した場合、bot は、 `task/submit invoke`イベントペイロードで JSON オブジェクトを含むイベントを受け取ります。 |

> [!NOTE]
> タスクモジュール機能を使用するには、読み込む Url のドメインがアプリのマニフェストの`validDomains`配列に含まれている必要があります。

## <a name="task-module-sizing"></a>タスクモジュールのサイズ変更

および`TaskInfo.width` `TaskInfo.height`の整数を使用して、高さと幅をピクセル単位で設定します。 ただし、チームのウィンドウと画面の解像度のサイズによっては、縦横比 (幅/高さ) を維持している場合に、比率が低くなります。

と`TaskInfo.width`の`TaskInfo.height`場合`"small"`、 `"medium"` `"large"`およびの場合、上の図の赤の四角形のサイズは、使用可能な領域の比率 (20%、50%、 `width` 60%、50%、66%(for `height`) です。

タブから起動されたタスクモジュールは、動的にサイズ変更できます。 呼び出し`tasks.startTask()`後に、newSize `tasks.updateTask(newSize)`オブジェクトの height プロパティと width プロパティの両方が taskinfo 仕様に準拠していることを呼び出します (例、 `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>HTML/JavaScript タスクモジュール用のタスクモジュール CSS

HTML/JavaScript ベースのタスクモジュールは、ヘッダーの下にあるタスクモジュールの領域全体にアクセスできます。 非常に高い柔軟性が提供されますが、ヘッダー要素に合わせてエッジの周囲にパディングを行い、不要なスクロールバーを使用しないようにするには、適切な CSS を提供する必要があります。 いくつかのユースケースの例を次に示します。

### <a name="example-1---youtube-video"></a>例 1-YouTube ビデオ

YouTube は、web ページにビデオを埋め込む機能を提供します。 簡単なスタブ web ページを使用すると、これをタスクモジュールに簡単に表示できます。

![YouTube ビデオ](~/assets/images/task-module/youtube-example.png)

CSS を使用しないこのページの HTML を次に示します。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  ⋮
</head>
<body>
  <div id="embed-container">
    <iframe width="1000" height="700" src="https://www.youtube.com/embed/rd0Rd8w3FZ0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen=""></iframe>
  </div>
</body>
</html>
```

CSS は次のようになります。

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 95%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

### <a name="example-2---powerapp"></a>例 2-PowerApp

同じ方法を使用して、PowerApp も埋め込むことができます。 個々の PowerApp の高さと幅はカスタマイズ可能なので、目的のプレゼンテーションを実現するには、高さと幅を調整しなければならない場合があります。

![Asset Management PowerApp](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

そして、CSS は次のとおりです。

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 94%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>アダプティブカードまたはアダプティブカードのボットカード添付ファイル

前述したように、を呼び出す`card`方法によっては、アダプティブカードを使用するか、またはアダプティブカードのボットカードの添付ファイル (添付ファイルオブジェクトにラップされたアダプティブカードのみ) を使用する必要があります。

タブから呼び出している場合は、アダプティブカードを使用する必要があります。 非常に簡単な例を次に示します。

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "text": "Here is a ninja cat:"
        },
        {
            "type": "Image",
            "url": "http://adaptivecards.io/content/cats/1.png",
            "size": "Medium"
        }
    ],
    "version": "1.0"
}
```

Bot から呼び出している場合は、次の例に示すように、アダプティブカードのボットカード添付ファイルを使用する必要があります。

```json
{
    "contentType": "application/vnd.microsoft.card.adaptive",
    "content": {
        "type": "AdaptiveCard",
        "body": [
            {
                "type": "TextBlock",
                "text": "Here is a ninja cat:"
            },
            {
                "type": "Image",
                "url": "http://adaptivecards.io/content/cats/1.png",
                "size": "Medium"
            }
        ],
        "version": "1.0"
    }
}
```

Bot またはタブから、アダプティブカードを含むタスクモジュールを呼び出しているかどうかを覚えておく必要があります。

## <a name="task-module-deep-link-syntax"></a>タスクモジュールの詳細なリンク構文

タスクモジュールの深さのリンクは、他の2つの情報`APP_ID`を含む[taskinfo オブジェクト](#the-taskinfo-object)のシリアル化だけで`BOT_APP_ID`あり、必要に応じて次のようにすることもできます。

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

データ型については、「」、「」 `<TaskInfo.url>` `<TaskInfo.width>`、 `<TaskInfo.card>`および`<TaskInfo.height>` `<TaskInfo.title>`「」の値については、「 [taskinfo オブジェクト](#the-taskinfo-object)」を参照してください。

> [!TIP]
> 特に、 `card`パラメーター (JavaScript の[ `encodeURI()`関数](https://www.w3schools.com/jsref/jsref_encodeURI.asp)など) を使用する場合は、URL が深いリンクをエンコードしていることを確認してください。

と`BOT_APP_ID`の情報を以下`APP_ID`に示します。

| 値 | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| `APP_ID` | string | はい | タスクモジュールを呼び出すアプリの[id](~/resources/schema/manifest-schema.md#id) 。 マニフェスト内の[Validdomains 配列](~/resources/schema/manifest-schema.md#validdomains)には`APP_ID` 、が URL にある`url`場合`url`のドメインが含まれている必要があります。 (アプリ ID は、タスクモジュールがタブまたは bot から呼び出されたときに既に知られています。これは`TaskInfo`、に含まれていないためです)。 |
| `BOT_APP_ID` | 文字列 | いいえ | の`completionBotId`値が指定されている`result`場合、オブジェクトは、指定`task/submit invoke`された bot へのメッセージによって送信されます。 `BOT_APP_ID`アプリのマニフェストでボットとして指定する必要があります。つまり、任意の bot に送信するだけではできません。 |

これ`APP_ID`は同じであること`BOT_APP_ID`に注意してください。多くの場合、アプリの ID として使用することをお勧めするので、アプリに bot がある場合は、それを使用することをお勧めします。

## <a name="keyboard-and-accessibility-guidelines"></a>キーボードとユーザー補助ガイドライン

HTML/JavaScript ベースのタスクモジュールを使用すると、アプリのタスクモジュールをキーボードで使用できることを確認する責任があります。 スクリーンリーダープログラムは、キーボードを使用して移動する機能にも依存します。 実用上の問題として、次の2つのことがあります。

1. HTML タグの[tabindex 属性](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex)を使用して、どの要素がフォーカスされているか、または (通常は<kbd>Tab</kbd>キーと Shift キーを<kbd>押しながら</kbd>tab キーを使用して) 連続したキーボードナビゲーションに参加するかどうかを制御します。
2. タスクモジュールの JavaScript で<kbd>Esc</kbd>キーを処理します。 これを行う方法を示すコードサンプルを次に示します。

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams では、キーボードナビゲーションがタスクモジュールヘッダーから HTML およびその逆に適切に動作することが保証されます。

## <a name="task-module-samples"></a>タスクモジュールのサンプル

* [Node.js/TypeScript サンプル](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs)
* [C#/.NET サンプル](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp)
