---
title: タブ削除のページを作成する
author: laujan
description: '[方法] タブ削除ページを作成する'
keywords: teams タブグループチャネルの構成可能な削除削除
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4ee060b8ef1f439ed4f8e4007e63606ce34c3d24
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964593"
---
# <a name="modify-or-remove-a-channel-group-tab"></a>チャネルグループタブの変更または削除

アプリでの削除および変更オプションをサポートすることで、ユーザーの作業を拡張し、強化することができます。 Teams を使用すると、ユーザーは [チャネル/グループ] タブの名前を変更または削除することができ、インストール後にタブを再構成することができます。 また、タブ削除の操作では、タブが削除されたときにコンテンツに何が起きるかを指定したり、コンテンツの削除やアーカイブなどの削除後のオプションをユーザーに提供したりすることができます。

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>インストール後にタブを再構成できるようにする

**manifest.jsで**は、タブの機能を定義します。 Tab インスタンスプロパティは、 `canUpdateConfiguration` 作成後にユーザーがタブを変更または再構成できるかどうかを示すブール値を受け取ります。

|Name| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`canUpdateConfiguration`|ブール型|||作成後にタブの構成のインスタンスをユーザーが更新できるかどうかを示す値。 限り `true`|

タブがチャネルまたはグループチャットにアップロードされると、チームはタブに右クリックされたドロップダウンメニューを追加します。使用可能なオプションは、次の設定によって決まり `canUpdateConfiguration` ます。

| `canUpdateConfiguration`| true   | false | 説明 |
| ----------------------- | :----: | ----- | ----------- |
|     設定            |   √    |       |`configurationUrl`ページが IFrame に再読み込みされ、ユーザーがタブを再設定できるようになります。  |
|     名前の変更              |   √    |   √   | ユーザーは、タブバーに表示されるタブ名を変更できます。          |
|     削除              |   √    |   √   |  `removeURL`プロパティと値が [**構成] ページ**に含まれている場合は、**削除ページ**が IFrame に読み込まれ、ユーザーに表示されます。 削除ページが含まれていない場合は、ユーザーに確認のダイアログボックスが表示されます。          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>アプリケーションのタブ削除ページを作成する

オプションの削除ページは、ホストする HTML ページで、タブが削除されるときに表示されます。 削除ページの URL は、構成ページ内のメソッドによって指定され `setSettings()` ます。 アプリ内のすべてのページと同様に、削除ページは [Teams のタブ要件](~/tabs/how-to/add-tab.md)に準拠している必要があります。

### <a name="register-a-remove-handler"></a>削除ハンドラーを登録する

必要に応じて、削除ページロジック内で、 `registerOnRemoveHandler((RemoveEvent) => {}` ユーザーが既存のタブ構成を削除したときに、イベントハンドラーを呼び出すことができます。 メソッドはインターフェイスを取得 [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) し、ユーザーがコンテンツを削除しようとしたときにハンドラー内のコードを実行します。 これを使用して、基になるリソースを削除するなどのクリーンアップ操作を実行して、タブのコンテンツを電源にします。 一度に登録できる削除ハンドラーは1つだけです。

この `RemoveEvent` インターフェイスは、次の2つのメソッドを使用してオブジェクトを記述します。

* `notifySuccess()`関数が必要です。 これは、基になるリソースの削除が正常に終了し、そのコンテンツを削除できることを示します。

* `notifyFailure(string)`関数はオプションです。 基になるリソースの削除が失敗し、そのコンテンツを削除できないことを示します。 オプションの文字列パラメーターは、失敗の理由を指定します。 指定した場合、この文字列がユーザーに表示されます。それ以外の場合は、一般的なエラーが表示されます。

#### <a name="use-the-getsettings-function"></a>関数を使用する `getSettings()`

を使用し `getSettings()` て、削除するタブの内容を指定できます。 `getSettings((Settings) =>{})`関数は、を使用して、 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 取得できる有効な設定プロパティ値を提供します。

#### <a name="use-the-getcontext-function"></a>関数を使用する `getContext()`

を使用して、 `getContext()` フレームが実行されている現在のコンテキストを取得できます。 関数は、を使用して、削除ページ `getContext((Context) =>{})` [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) `Context` に表示するコンテンツを決定するために削除ページロジックで使用できる有効なプロパティ値を提供します。

#### <a name="include-authentication"></a>認証を含める

ユーザーがタブの内容を削除できるようにするには、認証が必要な場合があります。 コンテキスト情報を使用して、認証要求および認証ページの Url を作成することができます。 [タブについては、「Microsoft Teams の認証フロー」を](~/tabs/how-to/authentication/auth-flow-tab.md)参照してください。 タブページで使用されているすべてのドメインが配列に含まれていることを確認してください `manifest.json` `validDomains` 。

タブ削除コードブロックの例を次に示します。

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

ユーザーがタブのドロップダウンメニューから [ **削除** ] を選択すると、Teams は、 `removeUrl` ( **構成ページ**で指定されている) 省略可能なページを IFrame に読み込みます。 ここでは、削除 `onClick()` `microsoftTeams.settings.setValidityState(true)` ページの IFrame の下部にある [ **削除** ] ボタンを呼び出して有効にする関数と共に、ユーザーにボタンが表示されます。

削除ハンドラーの実行後、 `removeEvent.notifySuccess()` または `removeEvent.notifyFailure()` チームにコンテンツ削除の結果が通知されます。

>[!NOTE]
>承認されたユーザーのコントロールがタブで禁止されないようにするために、Teams は成功とエラーの両方の場合にタブを削除します。
>Teams では、タブが呼び出されていない場合でも、5秒後に [ **削除** ] ボタンが有効になり `setValidityState()` ます。
>ユーザーが [チームの **削除** ] を選択すると、操作が完了したかどうかにかかわらず、30秒後にタブが削除されます。
