---
title: タブ削除のページを作成する
author: surbhigupta
description: インストール後にタブを再構成できるようにする方法について説明します。 Microsoft Teams アプリで削除オプションと変更オプションをサポートすることで、ユーザー エクスペリエンスを拡張します。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 40d6024d01b608c99347e9df65883906d7cb276d
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560450"
---
# <a name="create-a-removal-page"></a>削除ページを作成する

アプリの削除オプションと変更オプションをサポートすることで、ユーザー エクスペリエンスを拡張および強化できます。 Teams を使用すると、ユーザーはチャネルタブまたはグループ タブの名前を変更または削除でき、ユーザーはインストール後にタブを再構成できます。 さらに、タブの削除エクスペリエンスでは、コンテンツを削除またはアーカイブするための削除後のオプションがユーザーに提供されます。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>インストール後にタブを再構成できるようにする

`manifest.json`タブの機能と機能を定義します。 Tab インスタンス `canUpdateConfiguration` プロパティは、作成後にユーザーがタブを変更または再構成できるかどうかを示すブール値を受け取ります。 次の表に、プロパティの詳細を示します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`canUpdateConfiguration`|ブール型|||タブの構成のインスタンスを作成後にユーザーが更新できるかどうかを示す値。 既定値は `true` です。 |

タブがチャネルまたはグループ チャットにアップロードされると、Teams によってタブの右クリック ドロップダウン メニューが追加されます。使用可能なオプションは、設定によって `canUpdateConfiguration` 決まります。 次の表に、設定の詳細を示します。

| `canUpdateConfiguration`| true   | false | 説明 |
| ----------------------- | :----: | ----- | ----------- |
|     Settings            |   √    |       |`configurationUrl`ページは iFrame で再読み込みされ、ユーザーはタブを再構成できます。 |
|     名前の変更              |   √    |   √   | ユーザーは、タブ バーに表示されるタブ名を変更できます。          |
|     削除              |   √    |   √   |  プロパティと値が`removeURL`**構成ページ** に含まれている場合、**削除ページ** は iFrame に読み込まれ、ユーザーに表示されます。 削除ページが含まれていない場合は、ユーザーに確認ダイアログ ボックスが表示されます。          |

## <a name="create-a-tab-removal-page-for-your-application"></a>アプリケーションのタブ削除ページを作成する

オプションの削除ページは、ホストする HTML ページであり、タブが削除されたときに表示されます。 削除ページの URL は、構成ページ内の `setConfig()` メソッド (または `setSettings()` TeamsJS v.2.0.0 より前) によって指定されます。 アプリ内のすべてのページと同様に、削除ページは [Teams タブの前提条件](../../../tabs/how-to/tab-requirements.md)に準拠している必要があります。

### <a name="register-a-remove-handler"></a>削除ハンドラーを登録する

必要に応じて、削除ページ ロジック内で、ユーザーが既存の `registerOnRemoveHandler((RemoveEvent) => {}` タブ構成を削除したときにイベント ハンドラーを呼び出すことができます。 このメソッドはインターフェイスを [`RemoveEvent`](/javascript/api/@microsoft/teams-js/pages.config.removeevent?view=msteams-client-js-latest&preserve-view=true) 取り込み、ユーザーがコンテンツを削除しようとしたときにハンドラー内のコードを実行します。 このメソッドは、基になるリソースを削除してタブ コンテンツを供給するなど、クリーンアップ操作を実行するために使用されます。 一度に登録できる削除ハンドラーは 1 つだけです。

インターフェイスは `RemoveEvent` 、次の 2 つのメソッドを使用してオブジェクトを記述します。

* 関数が `notifySuccess()` 必要です。 これは、基になるリソースの削除が成功し、そのコンテンツを削除できることを示します。

* 関数は `notifyFailure(string)` 省略可能です。 これは、基になるリソースの削除に失敗し、そのコンテンツを削除できないことを示します。 省略可能な文字列パラメーターは、エラーの理由を指定します。 指定した場合、この文字列はユーザーに表示されます。それ以外の場合は、一般的なエラーが表示されます。

#### <a name="use-the-getconfig-function"></a>関数を使用する`getConfig()`

(以前の`getSettings()`) を使用`getConfig()`して、削除するタブ コンテンツを割り当てることができます。 この関数は `getConfig()` 、Config オブジェクトを使用して解決する promise を返し、取得できる有効な設定プロパティ値を提供します。

#### <a name="use-the-getcontext-function"></a>関数を使用する`getContext()`

フレームが実行されている現在のコンテキストを取得するために使用 `getContext()` できます。 この関数は `getContext()` 、Context オブジェクトで解決される Promise を返します。 Context オブジェクトは、削除ページ ロジックで使用できる有効な `Context` プロパティ値を提供し、削除ページに表示するコンテンツを決定します。

#### <a name="include-authentication"></a>認証を含める

ユーザーがタブコンテンツを削除できるようにするには、認証が必要です。 コンテキスト情報は、認証要求と承認ページ URL の作成に役立ちます。 タブについては、 [Microsoft Teams の認証フローに関するページを参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。 タブ ページで使用されているすべてのドメインが、アプリ マニフェストの配列に `validDomains` 一覧表示されていることを確認します。

タブ削除コード ブロックの例を次に示します。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    await microsoftTeams.app.initialize();
    pages.config.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        const configPromise = pages.getConfig();
        configPromise.
            then((configuration) => {
                configuration.contentUrl = "...";
                removeEvent.notifySuccess()}).
            catch((error) => {removeEvent.notifyFailure("failure message")});
    });

    const onClick() => {
        pages.config.setValidityState(true);
    }
  </script>
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    microsoftTeams.initialize();
    microsoftTeams.settings.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        microsoftTeams.settings.getSettings((settings) => {
        settings.contentUrl = "..."
        });
        removeEvent.notifySuccess();
    });

    const onClick() => {
        microsoftTeams.settings.setValidityState(true);
    }
  </script>
</body>
```

***

ユーザーがタブのドロップダウン メニューから **[削除**] を選択すると、Teams は **構成ページ** に割り当てられているオプション `removeUrl` ページを iFrame に読み込みます。 ユーザーには、呼び出`pages.config.setValidityState(true)`す関数が`onClick()`読み込まれたボタンが表示され、削除ページ iFrame の下部に表示される **[削除**] ボタンが有効になります。

削除ハンドラーが実行された後、 `removeEvent.notifySuccess()` または `removeEvent.notifyFailure()` コンテンツの削除結果を Teams に通知します。

>[!NOTE]
>
> * 承認されたユーザーのタブに対する制御が禁止されないようにするために、Teams は成功と失敗の両方のケースでタブを削除します。
> * イベント ハンドラーを `registerOnRemoveHandler` 呼び出すと、メソッドに応答するまでに 15 秒かかります。 既定では、Teams では、呼び出`setValidityState(true)`さない場合でも 5 秒後に **[削除]** ボタンが有効になります。
> * ユーザーが **[削除]** を選択すると、アクションが完了したかどうかに関係なく、Teams は 30 秒後にタブを削除します。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [モバイルのタブ](~/tabs/design/tabs-mobile.md)

## <a name="see-also"></a>関連項目

* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネル] または [グループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [構成ページを作成する](~/tabs/how-to/create-tab-pages/configuration-page.md)
