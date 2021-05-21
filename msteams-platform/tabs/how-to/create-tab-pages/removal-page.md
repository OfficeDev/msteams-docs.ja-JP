---
title: タブ削除のページを作成する
author: laujan
description: タブの削除ページを作成する方法
keywords: teams タブ グループ チャネル構成可能 削除
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
# <a name="modify-or-remove-a-channel-group-tab"></a>チャネル グループ タブの変更または削除

アプリで削除と変更のオプションをサポートすることで、ユーザー エクスペリエンスを拡張および強化できます。 Teamsを使用すると、ユーザーはチャネル/グループ タブの名前を変更または削除できます。インストール後にユーザーがタブを再構成できます。 さらに、タブの削除エクスペリエンスには、タブが削除された場合にコンテンツに何が起こるかを指定したり、削除後のオプション (コンテンツの削除やアーカイブなど) をユーザーに提供したりすることもできます。

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>インストール後にタブを再構成する

この **manifest.jsタブ** の機能を定義します。 tab instance プロパティは、作成後にユーザーがタブを変更または再構成できるかどうかを示すブール型 `canUpdateConfiguration` (Boolean) の値を取得します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`canUpdateConfiguration`|ブール型|||作成後に、タブの構成のインスタンスをユーザーが更新できるかどうかを示す値。 既定値: `true`|

タブがチャネルまたはグループ チャットにアップロードされると、Teamsの右クリック ドロップダウン メニューが追加されます。使用可能なオプションは、次の設定によって決 `canUpdateConfiguration` まります。

| `canUpdateConfiguration`| true   | false | 説明 |
| ----------------------- | :----: | ----- | ----------- |
|     設定            |   √    |       |ページ `configurationUrl` が IFrame に再読み込みされ、ユーザーはタブを再構成できます。  |
|     名前の変更              |   √    |   √   | ユーザーは、タブ バーに表示されるタブ名を変更できます。          |
|     削除              |   √    |   √   |  プロパティと値が構成ページに含まれている場合は、削除ページが IFrame に読み込まれ `removeURL` 、ユーザーに表示されます。   削除ページが含まれていない場合は、ユーザーに確認ダイアログ ボックスが表示されます。          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>アプリケーションのタブ削除ページを作成する

オプションの削除ページは、ホストする HTML ページであり、タブが削除されると表示されます。 削除ページの URL は、構成ページ `setSettings()` 内のメソッドによって指定されます。 アプリ内のすべてのページと同様に、削除ページはタブの要件に準拠[Teams必要があります](../../../tabs/how-to/tab-requirements.md)。

### <a name="register-a-remove-handler"></a>削除ハンドラーを登録する

必要に応じて、削除ページ ロジック内で、ユーザーが既存のタブ構成を削除するときにイベント ハンドラー `registerOnRemoveHandler((RemoveEvent) => {}` を呼び出します。 ユーザーがコンテンツを削除しようとすると、メソッドはインターフェイスを取り込み、ハンドラーで [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) コードを実行します。 これは、タブ コンテンツに電力を供給する基になるリソースの削除などのクリーンアップ操作を実行するために使用されます。 一度に登録できる削除ハンドラーは 1 つのみです。

インターフェイス `RemoveEvent` は、2 つのメソッドを持つオブジェクトについて説明します。

* この `notifySuccess()` 関数は必須です。 基になるリソースの削除が成功し、そのコンテンツを削除できると示します。

* この `notifyFailure(string)` 関数はオプションです。 基になるリソースの削除が失敗し、そのコンテンツを削除できないことを示します。 省略可能な文字列パラメーターは、エラーの理由を指定します。 指定されている場合、この文字列はユーザーに表示されます。それ以外の場合は、汎用エラーが表示されます。

#### <a name="use-the-getsettings-function"></a>関数を使用 `getSettings()` する

削除する `getSettings()` タブ コンテンツを指定するために使用できます。 この `getSettings((Settings) =>{})` 関数は、取得できる [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 有効な settings プロパティ値を取り込み、提供します。

#### <a name="use-the-getcontext-function"></a>関数を使用 `getContext()` する

フレームが実行 `getContext()` されている現在のコンテキストを取得するために使用できます。 この関数は、削除ページ ロジックで使用できる有効なプロパティ値を取り込み、削除ページに表示するコンテンツ `getContext((Context) =>{})` [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) `Context` を決定します。

#### <a name="include-authentication"></a>認証を含める

ユーザーにタブ コンテンツの削除を許可する前に、認証が必要になる場合があります。 コンテキスト情報は、認証要求と承認ページ URL の作成に役立ちます。 タブについては[Microsoft Teamsの認証フローを参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。 タブ ページで使用されているドメインすべてが配列に一覧表示されます `manifest.json` `validDomains` 。

以下に、タブ削除コード ブロックの例を示します。

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

ユーザーがタブのドロップダウンメニューから [削除] を選択すると、Teams はオプションのページ (構成ページで指定) を `removeUrl` IFrame に読み込む。 ここでは、削除ページ IFrame の下部にある [削除] ボタンを呼び出して有効にする関数が読み込まれたボタンがユーザー `onClick()` `microsoftTeams.settings.setValidityState(true)` に表示されます。 

削除ハンドラーの実行に続き、またはコンテンツのTeams `removeEvent.notifySuccess()` `removeEvent.notifyFailure()` 結果を通知します。

>[!NOTE]
> * 承認されたユーザーによるタブの制御が禁止されない場合、Teams は成功と失敗の両方の場合にタブを削除します。\
> * Teamsが **.\** を呼び出していなくても、5 秒後に [削除] ボタンを `setValidityState()` 有効にします。
> * ユーザーが [削除]**を選択Teams** 操作が完了したかどうかに関係なく、30 秒後にタブが削除されます。
