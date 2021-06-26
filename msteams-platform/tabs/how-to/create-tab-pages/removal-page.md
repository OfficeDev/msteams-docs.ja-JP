---
title: タブ削除のページを作成する
author: surbhigupta
description: タブの削除ページを作成する方法
keywords: teams タブ グループ チャネル構成可能 削除
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1b4ef5435ad1be82726edbf02d7205c0b1feba06
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140195"
---
# <a name="create-a-removal-page"></a>削除ページを作成する

アプリで削除と変更のオプションをサポートすることで、ユーザー エクスペリエンスを拡張および強化できます。 Teamsを使用すると、チャネルまたはグループ タブの名前の変更や削除が可能で、インストール後にユーザーがタブを再構成できます。 さらに、タブの削除エクスペリエンスでは、削除後のオプションをユーザーに提供して、コンテンツを削除またはアーカイブできます。

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>インストール後にタブを再構成する

この **manifest.jsタブ** の機能を定義します。 tab instance プロパティは、ユーザーが作成後にタブを変更または再構成できるかどうかを示すブール値 `canUpdateConfiguration` を取得します。 次の表に、プロパティの詳細を示します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`canUpdateConfiguration`|Boolean|||作成後に、タブの構成のインスタンスをユーザーが更新できるかどうかを示す値。 既定値は `true` です。 |

タブがチャネルまたはグループ チャットにアップロードされると、Teamsの右クリック ドロップダウン メニューが追加されます。使用可能なオプションは、設定によって決 `canUpdateConfiguration` まります。 次の表に、設定の詳細を示します。

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     設定            |   √    |       |ページ `configurationUrl` が IFrame に再読み込みされ、ユーザーはタブを再構成できます。 |
|     名前の変更              |   √    |   √   | ユーザーは、タブ バーに表示されるタブ名を変更できます。          |
|     削除              |   √    |   √   |  プロパティと値が構成ページに含まれている場合は、削除ページが IFrame に読み込まれ `removeURL` 、ユーザーに表示されます。   削除ページが含まれていない場合は、ユーザーに確認ダイアログ ボックスが表示されます。          |

## <a name="create-a-tab-removal-page-for-your-application"></a>アプリケーションのタブ削除ページを作成する

オプションの削除ページは、ホストする HTML ページであり、タブが削除されると表示されます。 削除ページの URL は、構成ページ `setSettings()` 内のメソッドによって指定されます。 アプリのすべてのページと同様に、削除ページはタブの前提条件に準拠[Teams必要があります](../../../tabs/how-to/tab-requirements.md)。

### <a name="register-a-remove-handler"></a>削除ハンドラーを登録する

必要に応じて、削除ページ ロジック内で、ユーザーが既存のタブ構成を削除するときにイベント ハンドラー `registerOnRemoveHandler((RemoveEvent) => {}` を呼び出します。 ユーザーがコンテンツを削除しようとすると、メソッドはインターフェイスを取り込み、ハンドラーで [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) コードを実行します。 このメソッドは、基になるリソースを削除してタブ コンテンツに電力を供給するなどのクリーンアップ操作を実行するために使用されます。 一度に登録できる削除ハンドラーは 1 つのみです。

インターフェイス `RemoveEvent` は、2 つのメソッドを持つオブジェクトについて説明します。

* この `notifySuccess()` 関数は必須です。 基になるリソースの削除が成功し、そのコンテンツを削除できると示します。

* この `notifyFailure(string)` 関数はオプションです。 基になるリソースの削除が失敗し、そのコンテンツを削除できないことを示します。 省略可能な文字列パラメーターは、エラーの理由を指定します。 指定されている場合、この文字列はユーザーに表示されます。それ以外の場合は、汎用エラーが表示されます。

#### <a name="use-the-getsettings-function"></a>関数を使用 `getSettings()` する

削除するタブ `getSettings()` コンテンツを割り当てる場合に使用できます。 この `getSettings((Settings) =>{})` 関数は、取得できる [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) 有効な settings プロパティ値を取り込み、提供します。

#### <a name="use-the-getcontext-function"></a>関数を使用 `getContext()` する

フレームが実行 `getContext()` されている現在のコンテキストを取得するために使用できます。 この `getContext((Context) =>{})` 関数は、 を取り込 [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) む。 この関数は、削除ページ ロジックで使用できる有効なプロパティ値を提供し、削除ページに表示するコンテンツ `Context` を決定します。

#### <a name="include-authentication"></a>認証を含める

ユーザーがタブ コンテンツを削除するには、認証が必要です。 コンテキスト情報は、認証要求と承認ページ URL の作成に役立ちます。 タブについては[Microsoft Teamsの認証フローを参照してください](~/tabs/how-to/authentication/auth-flow-tab.md)。 タブ ページで使用されているドメインすべてが配列に一覧表示されます `manifest.json` `validDomains` 。

次に、タブの削除コード ブロックの例を示します。

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

ユーザーがタブのドロップダウン **メニューから**[削除] を選択すると、Teamsページに割り当てられている省略可能なページが `removeUrl` IFrame に読み込まれます。  ユーザーには、削除ページ IFrame の下部に表示される [削除] ボタンを呼び出して有効にする関数が読み込まれたボタン `onClick()` `microsoftTeams.settings.setValidityState(true)` が表示されます。 

削除ハンドラーが実行された後、またはコンテンツのTeams `removeEvent.notifySuccess()` `removeEvent.notifyFailure()` 結果を通知します。

>[!NOTE]
> * 承認されたユーザーによるタブの制御が禁止されなかTeams、成功と失敗の両方の場合にタブが削除されます。
> * Teamsが呼び **出** されていない場合でも、5 秒後に [削除] ボタンを有効にします `setValidityState()` 。
> * ユーザーが [削除] を選択するとTeamsが完了したかどうかに関係なく、30 秒後にタブが削除されます。

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [前提条件](~/tabs/how-to/tab-requirements.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [コンテンツ ページを作成する](~/tabs/how-to/create-tab-pages/content-page.md)
* [構成ページを作成する](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [タブのコンテキストを取得する](~/tabs/how-to/access-teams-context.md)
* [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)
* [タブのリンクの展開とステージ ビュー](~/tabs/tabs-link-unfurling.md)
* [会話タブを作成する](~/tabs/how-to/conversational-tabs.md)
* [タブ余白の変更](~/resources/removing-tab-margins.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [モバイルのタブ](~/tabs/design/tabs-mobile.md)