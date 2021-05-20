---
title: JavaScript クライアント SDK を使用したタブやその他のホストされたエクスペリエンスの構築
author: heath-hamilton
ms.author: surbhigupta
description: でホストされているアプリ エクスペリエンスを構築するのに役立つMicrosoft Teams JavaScript クライアント SDK の概要Teams <iframe>.
localization_priority: Normal
keywords: チームタブグループチャンネル設定可能静的なSDK JavaScript個人
ms.topic: conceptual
ms.openlocfilehash: d3dfadda7f2a56e32ecf8e5b67df3b9831c52739
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566657"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Microsoft Teams JavaScript クライアント SDK を使用したタブやその他のホストされたエクスペリエンスの構築

Microsoft Teams JavaScript クライアント SDK は、Teamsでホストされたエクスペリエンスを作成するのに役立ちます。

SDK は、次のTeams機能のいずれかを使用してアプリを開発する場合に役立ちます。

* [タブ](../../tabs/what-are-tabs.md)
* [タスク モジュール](../../task-modules-and-cards/what-are-task-modules.md)

たとえば、SDK は、ユーザーがTeams クライアントで[行ったテーマの変更に対してタブを反応](../../build-your-first-app/build-personal-tab.md)させることができます。

## <a name="getting-started"></a>作業を開始する

開発の設定に応じて、次のいずれかの操作を行います。

* [npm または Yarn を使用して SDK をインストールする](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)

## <a name="common-sdk-functions"></a>一般的な SDK 関数

一般的に使用される SDK 関数については、次の表を参照してください。 [SDK リファレンス ドキュメント](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)では、より包括的な情報を提供します。


### <a name="basic-functions"></a>基本機能

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | SDK を初期化します。 この関数は、他の SDK 呼び出しの前に呼び出す必要があります。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| ページが実行されている現在の状態を取得します。 コールバックは **Context** オブジェクトを取得します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-&preserve-view=true)<br/>[コンテキスト obj](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Teamsライブラリを初期化し、contentUrl と web サイト Url に応じてタブの[フレームコンテキスト](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)を設定します。 これにより、ウェブサイトに移動またはリロード機能が正しい URL で動作することを保証します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | コンテンツ Url と webUrl に応じてタブの [フレーム コンテキスト](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) を設定します。 これにより、ウェブサイトに移動またはリロード機能が正しい URL で動作することを保証します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |ユーザーがタブの全画面表示またはウィンドウ表示を切り替えたときに登録されるハンドラー。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-&preserve-view=true)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerFullScreenHandler__isFullScreen__boolean_____void_&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |ユーザーがタブを再構成するために有効な **設定** ボタンを選択したときに登録されるハンドラー。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |アプリが所有するタブを取得します。 コールバックは **、TabInformation** オブジェクトを取得します。 オブジェクト **は** 省略可能なパラメーターです。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[タブ情報 obj](/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|ユーザーの最近使用したタブを取得します。 コールバックは **、TabInformation** オブジェクトを取得します。 オブジェクト **は** 省略可能なパラメーターです。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[タブ情報 obj](/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[タブインスタンス obj](/javascript/api/@microsoft/teams-js/tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|**DeepLinkParameters** オブジェクトを入力として受け取り、ユーザーが *タブ内* のコンテンツに移動するために使用できるディープ リンク ダイアログ ボックスを共有します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-&preserve-view=true)<br/>[ディープリンク obj](/javascript/api/@microsoft/teams-js/deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|必要な **deepLink** を入力として受け取り、ユーザーを URL に移動したり、Teams *内の* アプリを開いたりインストールしたりするクライアント アクションをトリガーします。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|**TabInstance** オブジェクトを入力として受け取り、指定したタブ インスタンスに移動します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-&preserve-view=true)<br/>[タブインスタンス obj](/javascript/api/@microsoft/teams-js/tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>認証名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|呼び出し元が指定したパラメーターを使用して新しいウィンドウを開く認証要求を開始します。 オプションの入力値は **、認証パラメーター** オブジェクトによって定義されます。|[function](/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[認証 obj](/javascript/api/@microsoft/teams-js/authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|認証要求を開始したフレームに、要求が成功したことを通知し、認証ウィンドウを閉じます。|[function](/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|認証要求を開始したフレームに、要求が失敗したことを通知し、認証ウィンドウを閉じます。|[function](/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|

### <a name="settings-namespace"></a>設定名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|初期値は false です。 有効性状態が true の場合に **、[保存]** または [ **削除** ] ボタンをアクティブにします。|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|現在のインスタンスの設定を取得します。 コールバックは **、設定** オブジェクトを取得します。|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)<br/>[設定 obj](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|現在のインスタンスの設定を構成します。 有効な設定は **、設定** オブジェクトによって定義されます。|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)<br/>[設定 obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|ユーザーが **[保存** ] ボタンを選択したときに登録されるハンドラー。 このハンドラーは、コンテンツを供給する基になるリソースを作成または更新するために使用する必要があります。|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|ユーザーが **[削除** ] ボタンを選択したときに登録されるハンドラー。 このハンドラーは、コンテンツに電力を供給する基になるリソースを削除するために使用する必要があります。|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>タスク モジュール名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|**TaskInfo** オブジェクトを入力として受け取り、アプリがタスク モジュールを開くことを許可します。 オプションの **submitHandler** は、タスク モジュールが完了したときに登録されます。 |[function](/javascript/api/@microsoft/teams-js/tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[タスク情報 obj](/javascript/api/@microsoft/teams-js/taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|タスク モジュールを送信します。 オプションの **result** 文字列パラメーターは、ボットまたはアプリに送信される結果であり、通常は JSON オブジェクトまたはシリアル化です。オプションの **appIds** 文字列または文字列配列パラメーターは、呼び出しがタスク モジュールを呼び出したものと同じ appId から発信されたことを検証する際に役立ちます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)|
