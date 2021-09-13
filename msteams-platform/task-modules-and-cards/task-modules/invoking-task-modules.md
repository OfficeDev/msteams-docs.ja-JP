---
title: タスク モジュールを呼び出して閉じる
description: タスク モジュールを呼び出して閉じる。
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: ab6425ae90c04e142e5d69f4a41ff49358731a23
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156475"
---
# <a name="invoke-and-dismiss-task-modules"></a>タスク モジュールを呼び出して閉じる

タスク モジュールは、タブ、ボット、またはディープ リンクから呼び出すことができます。 応答は、HTML、JavaScript、またはアダプティブ カードのいずれかです。 タスク モジュールの呼び出し方法と、ユーザーの操作の応答に対処する方法に関して、多くの柔軟性があります。 次の表に、この動作の概要を示します。

| using を使用して呼び出される | HTML または JavaScript のタスク モジュール | アダプティブ カード付きタスク モジュール |
| --- | --- | --- |
| タブ内の JavaScript | 1. オプションのコールバック関数Teamsクライアント SDK `tasks.startTask()` 関数を `submitHandler(err, result)` 使用します。 <br/><br/> 2. タスク モジュール コードで、ユーザーがアクションを実行した場合、Teams SDK 関数をパラメーターとして `tasks.submitTask()` `result` 呼び出します。 でコールバック `submitHandler` を指定した `tasks.startTask()` 場合、Teamsパラメーターとして `result` 呼び出されます。 呼び出し時にエラーが発生した場合は、代わりに文字列 `tasks.startTask()` `submitHandler` で関数 `err` が呼び出されます。 <br/><br/> 3. 呼び出し時に a `completionBotId` を指定できます `teams.startTask()` 。 その後 `result` 、代わりにボットに送信されます。 | 1. TaskInfo オブジェクトTeams、タスク モジュールポップアップに表示するアダプティブ カードの JSON を含むクライアント SDK 関数を呼び `tasks.startTask()` [](#the-taskinfo-object) `TaskInfo.card` 出します。 <br/><br/> 2. でコールバックを指定した場合、Teams は、呼び出し時にエラーが発生した場合、または右上の `submitHandler` `tasks.startTask()` `err` `tasks.startTask()` X を使用してタスク モジュールポップアップを閉じる場合に、文字列で呼び出します。 <br/><br/> 3. ユーザーがボタンを押すと、オブジェクトがの値 `Action.Submit` `data` として返されます `result` 。 |
| ボット カード ボタン | 1. ボット カード ボタンは、ボタンの種類に応じて、ディープ リンク URL またはメッセージを送信する 2 つの方法でタスク モジュールを呼び出 `task/fetch` します。 <br/><br/> 2. ボタンのアクションがアダプティブ カードのボタンの種類である場合、HTTP POST であるイベント `type` `task/fetch` `Action.Submit` `task/fetch invoke` がボットに送信されます。 ボットは、HTTP 200 で POST に応答し、TaskInfo オブジェクトのラッパーを含む [応答本文に応答します](#the-taskinfo-object)。 詳細については、「を使用して[タスク モジュールを呼 `task/fetch` び出す」を参照してください](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch)。 Teamsタスク モジュールを表示します。 <br/><br/> 3. ユーザーがアクションを実行した後、オブジェクトをパラメーター Teams SDK `tasks.submitTask()` `result` 関数を呼び出します。 ボットは、オブジェクト `task/submit invoke` を含むメッセージを受信 `result` します。 <br/><br/> 4. メッセージに応答するには、タスクが正常に完了した何もしないか、ポップアップ ウィンドウでユーザーにメッセージを表示するか、別のタスク モジュール ウィンドウを呼び出して、メッセージに応答する 3 つの異なる方法 `task/submit` があります。 詳細については、「に関[する詳細な説明 `task/submit` 」を参照してください](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 | <ul><li> Bot Framework カードのボタンと同様に、アダプティブ カードのボタンは、タスク モジュールの呼び出し、ボタンによるディープ リンク URL、およびボタンの使用の 2 つの方法を `Action.openUrl` `task/fetch` `Action.Submit` サポートします。 </li></ul> <br/><br/> <ul><li> アダプティブ カードを使用するタスク モジュールは、HTML または JavaScript の場合と非常に似て動作します。 主な違いは、アダプティブ カードを使用している場合は JavaScript が無いから、呼び出す方法がない点です `tasks.submitTask()` 。 代わりに、Teamsオブジェクトを取得し、 `data` `Action.Submit` イベントのペイロードとして返 `task/submit` します。 詳細については、「の柔軟性[」を参照 `task/submit` してください](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 </li></ul> |
| ディープ リンク URL <br/>[URL 構文](#task-module-deep-link-syntax) | 1. Teams、ディープ リンクのパラメーターで指定された内部に表示される URL であるタスク モジュール `<iframe>` `url` を呼び出します。 コールバック `submitHandler` はありません。 <br/><br/> 2. タスク モジュール内のページの JavaScript 内で、タブまたはボット カード ボタンから呼び出す場合と同じように、オブジェクトをパラメーターとして呼び出して閉じます `tasks.submitTask()` `result` 。 ただし、完了ロジックは若干異なります。 完了ロジックがボットがない場合は、クライアントに存在する場合、コールバックは存在しないので、完了ロジックは呼び出しの前のコードに `submitHandler` 存在する必要があります `tasks.submitTask()` 。 呼び出しエラーは、コンソールを通じてのみ報告されます。 ボットがある場合は、ディープ リンクでパラメーターを指定して、イベントを介して `completionBotId` `result` オブジェクトを送信 `task/submit` できます。 | 1. Teams、ディープ リンクのパラメーターの URL エンコード値として指定されたアダプティブ カードの JSON カード本文であるタスク モジュールを `card` 呼び出します。 <br/><br/> 2. ユーザーは、タスク モジュールの右上にある X を選択するか、カードのボタンを押してタスク モジュール `Action.Submit` を閉じます。 呼び出す必要が無い場合、ユーザーはアダプティブ カード フィールドの値を送信するボット `submitHandler` を持っている必要があります。 ユーザーはディープ リンクのパラメーターを使用して、イベントを使用してデータを送信するボット `completionBotId` を指定する必要 `task/submit invoke` があります。 |

次のセクションでは、タスク `TaskInfo` モジュールの特定の属性を定義するオブジェクトを指定します。

## <a name="the-taskinfo-object"></a>TaskInfo オブジェクト

オブジェクト `TaskInfo` には、タスク モジュールのメタデータが含まれています。 埋め `url` 込み iFrame 用またはアダプティブ `card` カード用に定義します。 次の表に、オブジェクト定義を示します。

| 属性 | 種類 | 説明 |
| --- | --- | --- |
| `title` | string | この属性は、アプリ名の下とアプリ アイコンの右側に表示されます。 |
| `height` | number または string | この属性には、タスク モジュールの高さをピクセル単位で表す数値、または `small` 、 `medium` 、 を指定できます `large` 。 詳細については、「タスク モジュールの [サイズ変更」を参照してください](#task-module-sizing)。 |
| `width` | number または string | この属性には、タスク モジュールの幅をピクセル単位で表す数値、または `small` 、 `medium` 、 を指定できます `large` 。 詳細については、「タスク モジュールの [サイズ変更」を参照してください](#task-module-sizing)。 |
| `url` | 文字列 | この属性は、タスク モジュール内に読み込まれるページ `<iframe>` の URL です。 URL のドメインは、アプリのマニフェスト内の [アプリの validDomains](~/resources/schema/manifest-schema.md#validdomains) 配列内にある必要があります。 |
| `card` | アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル | この属性は、アダプティブ カードがタスク モジュールに表示される JSON です。 ユーザーがボットから呼び出す場合は、Bot Framework オブジェクトでアダプティブ カード JSON を使用 `attachment` します。 タブから、ユーザーはアダプティブ カードを使用する必要があります。 詳細については、「アダプティブ カード [またはアダプティブ カード ボット カードの添付ファイル」を参照してください。](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | この属性は、クライアントがタスク モジュール機能をサポートしていない場合、ブラウザー タブで URL を開きます。 |
| `completionBotId` | string | この属性は、ユーザーがタスク モジュールとやり取りした結果を送信するボット アプリ ID を指定します。 指定した場合、ボットはイベント ペイロード `task/submit invoke` に JSON オブジェクトを含むイベントを受信します。 |

> [!NOTE]
> タスク モジュール機能では、読み込む URL のドメインがアプリのマニフェストの配列 `validDomains` に含まれている必要があります。

次のセクションでは、ユーザーがタスク モジュールの高さと幅を設定できるタスク モジュールのサイズ変更を指定します。

## <a name="task-module-sizing"></a>タスク モジュールのサイズ変更

の整数を使用 `TaskInfo.width` `TaskInfo.height` して、タスク モジュールの高さと幅をピクセル単位で設定します。 ただし、チームのウィンドウのサイズと画面の解像度に応じて、縦横比 (幅または高さ) を維持しながら、比例して縮小されます。

次の図の赤い四角形のサイズは、次の画像の場合 `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` 、20%、50%、および 60% の使用可能な領域と `width` 20%、50%、および 66% `height` の比率です。

![タスク モジュールの例](~/assets/images/task-module/task-module-example.png)

タブから呼び出されるタスク モジュールは、動的にサイズを変更できます。 呼び出し後、newSize オブジェクトの高さと幅のプロパティが TaskInfo の仕様に準拠している場所 `tasks.startTask()` `tasks.updateTask(newSize)` を呼び出します `{ height: 'medium', width: 'medium' }` 。

次のセクションでは、YouTube ビデオと PowerApp にタスク モジュールを埋め込む例を示します。

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>HTML または JavaScript タスク モジュールのタスク モジュール CSS

HTML または JavaScript ベースのタスク モジュールは、ヘッダーの下のタスク モジュールの領域全体にアクセスできます。 多くの柔軟性を提供しますが、ヘッダー要素に合わせてエッジをパディングし、不要なスクロール バーを回避する場合は、適切な CSS を提供する必要があります。 次のセクションでは、いくつかの使用例の例を示します。

**例 1: YouTube ビデオ**

YouTube では、Web ページにビデオを埋め込む機能が提供されています。 簡単なスタブ Web ページを使用して、タスク モジュール内の Web ページにビデオを埋め込むのは簡単です。

![YouTube ビデオ](~/assets/images/task-module/youtube-example.png)

次のコードは、CSS のない Web ページの HTML の例を示しています。

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

次のコードは、CSS の例を示しています。

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

**例 2: PowerApp**

ユーザーは、PowerApp を埋め込む場合にも同じ方法を使用できます。 個々の PowerApp の高さまたは幅をカスタマイズできるので、ユーザーは高さと幅を調整して、目的のプレゼンテーションを実現できます。

![アセット管理 PowerApp](~/assets/images/task-module/powerapp-example.png)

次のコードは、PowerApp の HTML の例を示しています。

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

次のコードは、CSS の例を示しています。

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

次のセクションでは、アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイルを使用してカードを呼び出す方法の詳細について説明します。

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル

呼び出し方法に応じて、アダプティブ カードまたはアダプティブ カード ボット カードの添付ファイル (添付ファイル オブジェクトにラップされたアダプティブ カード) を使用する `card` 必要があります。

タブから呼び出す場合、ユーザーはアダプティブ カードを使用する必要があります。

次のコードは、アダプティブ カードの例を示しています。

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

次のコードは、ボットから呼び出す際のアダプティブ カード ボット カードの添付ファイルの例を示しています。

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

次のセクションでは、オブジェクトと . を含むタスク モジュールのディープ リンク `TaskInfo` 構文の詳細について `APP_ID` 説明します `BOT_APP_ID` 。

## <a name="task-module-deep-link-syntax"></a>タスク モジュールのディープ リンク構文

タスク モジュールのディープ リンクは、TaskInfo オブジェクトのシリアル化であり、他の 2 つの詳細と、必要に応じて `APP_ID` 、 `BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

、、、のデータ型と許容値については `<TaskInfo.url>` `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` [、TaskInfo オブジェクトを参照してください](#the-taskinfo-object)。

> [!TIP]
> URL は、JavaScript の関数など、パラメーターを使用する場合にディープ リンク `card` をエンコード[ `encodeURI()` します](https://www.w3schools.com/jsref/jsref_encodeURI.asp)。

次の表に、以下の情報を `APP_ID` 示します `BOT_APP_ID` 。

| 値 | 型 | 必須 | 説明 |
| --- | --- | --- | --- |
| `APP_ID` | string | はい | タスク [モジュール](~/resources/schema/manifest-schema.md#id) を呼び出すアプリの ID。 マニフェスト [の validDomains 配列](~/resources/schema/manifest-schema.md#validdomains) には、URL に if の `APP_ID` `url` ドメイン `url` が含まれている必要があります。 アプリ ID は、タブまたはボットからタスク モジュールを呼び出す際に既に知られているので、 に含まれません `TaskInfo` 。 |
| `BOT_APP_ID` | 文字列 | いいえ | for の値を `completionBotId` 指定すると、指定したボットにメッセージ `result` を使用 `task/submit invoke` してオブジェクトが送信されます。 `BOT_APP_ID` アプリのマニフェストでボットとして指定する必要があります。つまり、ボットに送信することはできません。 |

> [!NOTE]
> `APP_ID` 多くの場合、アプリにアプリの ID として使用する推奨ボットがある場合は、同じ値 `BOT_APP_ID` を指定できます。

次のセクションでは、アプリのタスク モジュールでキーボードを使用する方法の詳細について説明します。

## <a name="keyboard-and-accessibility-guidelines"></a>キーボードとアクセシビリティのガイドライン

HTML または JavaScript ベースのタスク モジュールでは、アプリのタスク モジュールをキーボードで使用できる必要があります。 スクリーン リーダー プログラムは、キーボードを使用して移動する機能にも依存します。 これには、次の 2 つのことが含まれます。

* HTML タグ [で tabindex 属性](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) を使用して、フォーカスできる要素を制御します。 また、tabindex 属性を使用して、通常は Tab キーと <kbd>Shift-Tab</kbd> キーを使用して、シーケンシャル キーボード ナビゲーションに参加する場所 <kbd>を特定</kbd> します。
* タスク モジュール <kbd>の JavaScript</kbd> の Esc キーを処理します。 次のコードは、Esc キーを処理する方法の例 <kbd>を示</kbd> しています。

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

Microsoft Teamsタスク モジュール ヘッダーから HTML へのキーボード ナビゲーションが正しく機能し、その逆も同様です。

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|タスク モジュールのサンプル ボット-V4 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|タスク モジュールのサンプル タブとボット-V3 | タスク モジュールを作成するためのサンプル。 |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a>関連項目

* [デバイスのアクセス許可を要求する](~/concepts/device-capabilities/native-device-permissions.md)
* [メディア機能を統合する](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [QR スキャナーまたはバーコード スキャナー機能をアプリに統合Teams](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [場所の機能を統合Teams](~/concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
