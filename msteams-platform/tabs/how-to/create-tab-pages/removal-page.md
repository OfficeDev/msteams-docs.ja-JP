---
title: タブ削除のページを作成する
author: laujan
description: タブ削除ページを作成する方法
keywords: Teams タブ グループ チャネルの構成可能な削除の削除
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 49e2df47095999e9f9eea76ea341a44215bfacb3
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797884"
---
# <a name="modify-or-remove-a-channel-group-tab"></a>チャネル グループ タブを変更または削除する

アプリで削除と変更のオプションをサポートすることで、ユーザー エクスペリエンスを拡張および強化できます。 Teams を使用すると、ユーザーはチャネル/グループ タブの名前を変更または削除できます。また、インストール後にユーザーがタブを再構成することもできます。 さらに、タブ削除エクスペリエンスには、タブが削除された場合のコンテンツに対する処理の指定や、コンテンツの削除やアーカイブなどの削除後のオプションをユーザーに提供する操作も含まれます。

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>インストール後にタブを再構成する

ユーザー **manifest.jsタブ** の機能を定義します。 タブ インスタンス プロパティは、ユーザーがタブの作成後に変更または再構成できるかどうかを示すブール `canUpdateConfiguration` 値を受け取います。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`canUpdateConfiguration`|Boolean|||タブの構成のインスタンスを作成後にユーザーが更新できるかどうかを示す値。 既定値: `true`|

タブがチャネルまたはグループ チャットにアップロードされると、Teams はタブの右クリック ドロップダウン メニューを追加します。使用可能なオプションは、設定によって決 `canUpdateConfiguration` まります。

| `canUpdateConfiguration`| true   | false | 説明 |
| ----------------------- | :----: | ----- | ----------- |
|     設定            |   √    |       |ページ `configurationUrl` が IFrame に再読み込みされ、ユーザーはタブを再構成できます。  |
|     名前の変更              |   √    |   √   | ユーザーは、タブ バーに表示されるタブ名を変更できます。          |
|     削除              |   √    |   √   |  プロパティと値が構成ページに含まれている場合、削除ページは IFrame に読み込まれ `removeURL` 、ユーザーに表示されます。   削除ページが含まれていない場合は、ユーザーに確認ダイアログ ボックスが表示されます。          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>アプリケーションのタブ削除ページを作成する

オプションの削除ページは、ホストする HTML ページであり、タブが削除されると表示されます。 削除ページの URL は、構成ページ `setSettings()` 内のメソッドによって指定されます。 アプリ内のすべてのページと同様に、削除ページは Teams タブの要件 [に準拠している必要があります](../../../tabs/how-to/tab-requirements.md)。

### <a name="register-a-remove-handler"></a>削除ハンドラーを登録する

必要に応じて、削除ページ ロジック内で、ユーザーが既存のタブ構成を削除するときにイベント ハンドラー `registerOnRemoveHandler((RemoveEvent) => {}` を呼び出します。 このメソッドはインターフェイスを取り込み、ユーザーがコンテンツを削除しようとするときにハンドラーで [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) コードを実行します。 このプロパティは、基になるリソースを削除してタブ コンテンツを作成するなどのクリーンアップ操作を実行するために使用されます。 一度に登録できる削除ハンドラーは 1 つのみです。

インターフェイス `RemoveEvent` は、2 つのメソッドを持つオブジェクトを記述します。

* この `notifySuccess()` 関数は必須です。 基になるリソースの削除が成功し、そのコンテンツを削除できる状態を示します。

* この `notifyFailure(string)` 関数は省略可能です。 基になるリソースの削除が失敗し、そのコンテンツを削除できないことを示します。 オプションの文字列パラメーターは、失敗の理由を指定します。 指定した場合、この文字列はユーザーに表示されます。それ以外の場合は、汎用エラーが表示されます。

#### <a name="use-the-getsettings-function"></a>関数を使用 `getSettings()` する

削除する `getSettings()` タブ コンテンツを指定するために使用できます。 この `getSettings((Settings) =>{})` 関数は、取得 [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 可能な有効な設定プロパティ値を取り込み、提供します。

#### <a name="use-the-getcontext-function"></a>関数を使用 `getContext()` する

フレームが `getContext()` 実行されている現在のコンテキストを取得するために使用できます。 関数は、削除ページのロジックで使用できる有効なプロパティ値を取り込み、削除ページに表示するコンテンツ `getContext((Context) =>{})` [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) `Context` を決定します。

#### <a name="include-authentication"></a>認証を含める

ユーザーにタブ コンテンツの削除を許可する前に認証が必要になる場合があります。 コンテキスト情報は、認証要求と承認ページ URL の構築に役立ちます。 タブについては [、Microsoft Teams の認証フローを参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。 タブ ページで使用されているドメインすべてが配列に表示されます `manifest.json` `validDomains` 。

次に、タブ削除コード ブロックのサンプルを示します。

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

ユーザーがタブのドロップダウンメニューから [削除] を選択すると、Teams はオプションのページ (構成ページで指定) を IFrame に読み込 `removeUrl` む必要があります。  ここでは、ユーザーには、削除ページ IFrame の下部付近にある [削除] ボタンを呼び出す関数が読み込まれたボタン `onClick()` `microsoftTeams.settings.setValidityState(true)` が表示されます。 

削除ハンドラーの実行に従って、 `removeEvent.notifySuccess()` または `removeEvent.notifyFailure()` コンテンツ削除の結果を Teams に通知します。

>[!NOTE]
>承認されたユーザーによるタブに対する制御が禁止されない場合、Teams は成功と失敗の両方の場合にタブを削除します。\
>Teams は、 **タブが呼** び出されていない場合でも、5 秒後に [削除] ボタンを `setValidityState()` 有効にします。
>ユーザーが **[Teams** の削除] を選択すると、操作が完了したかどうかに関係なく、30 秒後にタブが削除されます。
