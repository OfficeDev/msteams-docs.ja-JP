---
title: タブ削除のページを作成する
author: laujan
description: タブ削除ページを作成する方法
keywords: チーム タブ グループ の構成可能な削除削除
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: e1a1f38a2bcb3b5bc4bc54f469c8727e44d8695e
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566671"
---
# <a name="modify-or-remove-a-channel-group-tab"></a>チャネル グループ タブを変更または削除する

アプリの削除および変更オプションをサポートすることで、ユーザー エクスペリエンスを拡張および強化できます。 Teams、ユーザーはチャンネル/グループタブの名前を変更したり削除したりすることができ、インストール後にユーザーがタブを再構成することを許可することができます。 また、タブの削除には、タブが削除されたときにコンテンツに何が起こるかを指定したり、コンテンツの削除やアーカイブなどの削除後のオプションをユーザーに提供したりすることが含まれます。

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>インストール後にタブを再構成できるようにする

上 **のmanifest.js** は、タブの機能を定義します。 タブインスタンス `canUpdateConfiguration` プロパティは、ユーザーがタブの作成後にタブを変更または再構成できるかどうかを示すブール値を受け取ります。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`canUpdateConfiguration`|Boolean|||タブの構成のインスタンスを作成後にユーザーが更新できるかどうかを示す値。 デフォルト： `true`|

タブがチャンネルまたはグループチャットにアップロードされると、Teamsタブの右クリックドロップダウンメニューが追加されます。使用可能なオプションは、設定によって決まります `canUpdateConfiguration` 。

| `canUpdateConfiguration`| true   | false | 説明 |
| ----------------------- | :----: | ----- | ----------- |
|     設定            |   √    |       |`configurationUrl`ページが IFrame に再読み込みされ、ユーザーはタブを再構成できます。  |
|     名前の変更              |   √    |   √   | ユーザーは、タブバーに表示されるタブ名を変更できます。          |
|     削除              |   √    |   √   |  `removeURL`プロパティと値が **構成ページ** に含まれている場合、**削除ページ** は IFrame に読み込まれ、ユーザーに表示されます。 削除ページが含まれていない場合、ユーザーには確認ダイアログ ボックスが表示されます。          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>アプリケーションのタブ削除ページを作成する

省略可能な削除ページは、ホストする HTML ページで、タブが削除されると表示されます。 削除ページの URL は、 `setSettings()` 構成ページ内のメソッドによって指定されます。 アプリのすべてのページと同様に、削除ページは[Teams タブの要件](../../../tabs/how-to/tab-requirements.md)に準拠している必要があります。

### <a name="register-a-remove-handler"></a>削除ハンドラーを登録する

必要に応じて、削除ページロジック内で、 `registerOnRemoveHandler((RemoveEvent) => {}` ユーザーが既存のタブ構成を削除したときにイベントハンドラーを呼び出すことができます。 このメソッドは [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) 、ユーザーがコンテンツを削除しようとしたときに、インターフェイスを取得してハンドラー内のコードを実行します。 これは、タブの内容に電力を供給する基になるリソースを削除するなどのクリーンアップ操作を実行するために使用されます。 一度に登録できる削除ハンドラは 1 つだけです。

`RemoveEvent`このインターフェイスは、2 つのメソッドを持つオブジェクトを記述します。

* `notifySuccess()`関数は必須です。 基になるリソースの削除が成功し、その内容を削除できることを示します。

* `notifyFailure(string)`この関数はオプションです。 基になるリソースの削除が失敗し、その内容を削除できないことを示します。 省略可能な文字列パラメーターは、失敗の理由を指定します。 指定した場合、この文字列はユーザーに表示されます。それ以外の場合は、一般的なエラーが表示されます。

#### <a name="use-the-getsettings-function"></a>関数を使用する `getSettings()`

を使用 `getSettings()` して、削除するタブコンテンツを指定できます。 関数は `getSettings((Settings) =>{})` を取 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) り込み、取得できる有効な設定プロパティ値を提供します。

#### <a name="use-the-getcontext-function"></a>関数を使用する `getContext()`

を使用 `getContext()` して、フレームが実行されている現在のコンテキストを取得できます。 `getContext((Context) =>{})`この関数は、 [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) を使用して有効な `Context` プロパティ値を提供し、削除ページのロジックで使用して削除ページに表示するコンテンツを決定します。

#### <a name="include-authentication"></a>認証を含める

ユーザーがタブの内容を削除できるようにする前に、認証が必要になる場合があります。 コンテキスト情報は、認証要求と承認ページ URL の構築に役立ちます。 [タブMicrosoft Teams認証フローを](~/tabs/how-to/authentication/auth-flow-tab.md)参照してください。 タブページで使用されているすべてのドメインがアレイにリストされていることを確認します `manifest.json` `validDomains` 。

以下は、タブ削除コードブロックの例です。

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

ユーザーがタブのドロップダウン メニューから **[削除]** を選択すると、Teamsはオプション ページ `removeUrl` (**構成ページ** で指定) を IFrame に読み込みます。 ここでは、削除 `onClick()` `microsoftTeams.settings.setValidityState(true)` ページ IFrame の下部にある **[削除** ] ボタンを呼び出して有効にする関数を読み込んだボタンが表示されます。

削除ハンドラの実行後、 `removeEvent.notifySuccess()` または `removeEvent.notifyFailure()` コンテンツ削除の結果をTeamsに通知します。

>[!NOTE]
> * 承認されたユーザーによるタブの制御が禁止されないようにするには、Teams成功と失敗の両方のケースでタブを削除します。
> * Teamsタブが .\ を呼び出していない場合でも、5 秒後に **[削除**] ボタンを有効 `setValidityState()` にします。
> * ユーザーが **[削除**] を選択すると、Teamsは、操作が完了したかどうかに関係なく、30 秒後にタブを削除します。
