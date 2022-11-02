---
title: タブ削除のページを作成する
author: surbhigupta
description: インストール後にタブを再構成できるようにする方法について説明します。 Microsoft Teams アプリで削除と変更のオプションをサポートすることで、ユーザー エクスペリエンスを拡張します。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 423cc386ca416fe116eb0bcb62c1238cae5547ff
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819941"
---
# <a name="create-a-removal-page"></a>削除ページを作成する

アプリで削除と変更のオプションをサポートすることで、ユーザー エクスペリエンスを拡張および強化できます。 Teams を使用すると、ユーザーはチャネルまたはグループ タブの名前を変更または削除でき、ユーザーはインストール後にタブを再構成できます。 さらに、タブの削除エクスペリエンスを使用すると、コンテンツを削除またはアーカイブするための削除後オプションがユーザーに提供されます。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>インストール後にタブを再構成できるようにする

タブ `manifest.json` の機能を定義します。 tab インスタンス `canUpdateConfiguration` プロパティは、作成後にユーザーがタブを変更または再構成できるかどうかを示すブール値を受け取ります。 次の表に、プロパティの詳細を示します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`canUpdateConfiguration`|ブール型|||タブの構成のインスタンスを作成後にユーザーが更新できるかどうかを示す値。 既定値は `true` です。 |

タブがチャネルまたはグループ チャットにアップロードされると、Teams によってタブの右クリック ドロップダウン メニューが追加されます。使用可能なオプションは、設定によって `canUpdateConfiguration` 決まります。 次の表に、設定の詳細を示します。

| `canUpdateConfiguration`| true   | false | 説明 |
| ----------------------- | :----: | ----- | ----------- |
|     Settings            |   √    |       |ページは `configurationUrl` iFrame に再読み込みされ、ユーザーはタブを再構成できます。 |
|     名前の変更              |   √    |   √   | ユーザーは、タブ バーに表示されるタブ名を変更できます。          |
|     削除              |   √    |   √   |  `removeURL`プロパティと値が **構成ページ** に含まれている場合、**削除ページ** は iFrame に読み込まれ、ユーザーに表示されます。 削除ページが含まれていない場合、ユーザーに確認ダイアログ ボックスが表示されます。          |

## <a name="create-a-tab-removal-page-for-your-application"></a>アプリケーションのタブ削除ページを作成する

オプションの削除ページはホストする HTML ページであり、タブが削除されると表示されます。 削除ページ URL は、構成ページ内の `setConfig()` メソッド (または `setSettings()` TeamsJS v.2.0.0 より前) によって指定されます。 アプリ内のすべてのページと同様に、削除ページは [Teams タブの前提条件](../../../tabs/how-to/tab-requirements.md)に準拠している必要があります。

### <a name="register-a-remove-handler"></a>削除ハンドラーを登録する

必要に応じて、削除ページ ロジック内で、ユーザーが既存のタブ構成を `registerOnRemoveHandler((RemoveEvent) => {}` 削除するときにイベント ハンドラーを呼び出すことができます。 メソッドはインターフェイスを [`RemoveEvent`](/javascript/api/@microsoft/teams-js/pages.config.removeevent?view=msteams-client-js-latest&preserve-view=true) 受け取り、ユーザーがコンテンツを削除しようとしたときにハンドラーでコードを実行します。 メソッドは、タブ コンテンツに基づくリソースの削除などのクリーンアップ操作を実行するために使用されます。 一度に登録できる削除ハンドラーは 1 つだけです。

インターフェイスでは `RemoveEvent` 、次の 2 つのメソッドを持つオブジェクトについて説明します。

* 関数が `notifySuccess()` 必要です。 基になるリソースの削除が成功し、そのコンテンツを削除できることを示します。

* 関数は `notifyFailure(string)` 省略可能です。 基になるリソースの削除に失敗し、そのコンテンツを削除できないことを示します。 省略可能な文字列パラメーターは、エラーの理由を指定します。 指定した場合、この文字列はユーザーに表示されます。それ以外の場合は、一般的なエラーが表示されます。

#### <a name="use-the-getconfig-function"></a>関数を使用する`getConfig()`

(以前`getSettings()`の) を使用`getConfig()`して、削除するタブ コンテンツを割り当てることができます。 関数は `getConfig()` 、Config オブジェクトで解決される promise を返し、取得できる有効な設定プロパティ値を提供します。

#### <a name="use-the-getcontext-function"></a>関数を使用する`getContext()`

を使用 `getContext()` して、フレームが実行されている現在のコンテキストを取得できます。 関数は `getContext()` 、Context オブジェクトで解決される promise を返します。 Context オブジェクトは、削除ページ ロジックで使用できる有効な `Context` プロパティ値を提供し、削除ページに表示するコンテンツを決定します。

#### <a name="include-authentication"></a>認証を含める

ユーザーがタブ コンテンツを削除できるようにする前に、認証が必要です。 コンテキスト情報は、認証要求と承認ページ URL の構築に役立ちます。 タブについては、「 [Microsoft Teams 認証フロー」を参照](~/tabs/how-to/authentication/auth-flow-tab.md)してください。 タブ ページで使用されているすべてのドメインが、アプリ マニフェストの配列に `validDomains` 一覧表示されていることを確認します。

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

ユーザーがタブのドロップダウン メニューから **[削除**] を選択すると、Teams は **構成ページ** で割り当てられたオプション`removeUrl`のページを iFrame に読み込みます。 ユーザーが呼び出す`pages.config.setValidityState(true)`関数が`onClick()`読み込まれたボタンが表示され、削除ページ iFrame の下部に表示される **[削除**] ボタンが有効になります。

削除ハンドラーが実行された後、 `removeEvent.notifySuccess()` または `removeEvent.notifyFailure()` コンテンツの削除結果を Teams に通知します。

>[!NOTE]
>
> * 承認されたユーザーによるタブの制御が禁止されないようにするために、Teams は成功と失敗の両方のケースでタブを削除します。
> * イベント ハンドラーを `registerOnRemoveHandler` 呼び出すと、メソッドに応答するのに 15 秒が発生します。 既定では、 を呼び出`setValidityState(true)`さない場合でも、Teams では 5 秒後に **[削除]** ボタンが有効になります。
> * ユーザーが **[削除**] を選択すると、アクションが完了したかどうかにかかわらず、30 秒後にタブが削除されます。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [モバイルのタブ](~/tabs/design/tabs-mobile.md)

## <a name="see-also"></a>関連項目

* [Teams の [ビルド] タブ](../../what-are-tabs.md)
* [Teams のアプリ マニフェストのスキーマ](../../../resources/schema/manifest-schema.md)
* [RemoveEvent インターフェイス](/javascript/api/@microsoft/teams-js/pages.config.removeevent)
* [タブのコンテキストを取得する](../access-teams-context.md)
* [プライベート タブを作成する](../create-personal-tab.md)
* [チャネル タブまたはグループ タブを作成する](../create-channel-group-tab.md)
