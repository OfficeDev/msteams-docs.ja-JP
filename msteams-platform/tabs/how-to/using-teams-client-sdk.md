---
title: Teams クライアント SDK の使用
author: laujan
description: Teams クライアント SDK を使用して、ユーザー設定のタブに Teams 対応機能を追加する方法
keywords: teams タブグループチャネルの構成可能な静的 SDK JavaScript personal
ms.topic: conceptual
ms.openlocfilehash: eac5a8ec03ba12d926346afb40ca9bc6e9dda8d6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675104"
---
# <a name="using-the-teams-client-sdk"></a>Teams クライアント SDK の使用

**Teams javascript クライアント SDK**および**teams javascript ライブラリ**は、 [Microsoft teams 開発者プラットフォーム](https://msdn.microsoft.com/microsoft-teams)の一部であり、teams アプリケーションの作成を容易にするツールとプロセスを提供します。 Teams クライアント SDK は、npm パッケージとして配布されます。 最新バージョンについては、「 <https://www.npmjs.com/package/@microsoft/teams-js>」を参照してください。 Teams ライブラリは、に<https://github.com/OfficeDev/microsoft-teams-library-js>あります。

次の表に、タブ開発で一般的に使用される Teams ライブラリ関数の概要を示します。

## <a name="teams-sdk-public-api"></a>Teams SDK パブリック API 

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    | -----        |
| `microsoftTeams.initialize()` | Teams ライブラリを初期化します。 この関数は、他の SDK 呼び出しの前に呼び出す必要があります。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-)|
|`microsoftTeams.getContext(callback: (context: Context)`| ページが実行されている現在の状態を取得します。 コールバックは、**コンテキスト**オブジェクトを取得します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-)<br/>[context obj](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |ユーザーがタブの全画面表示/ウィンドウ表示を切り替えたときに登録されるハンドラー。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest#isfullscreen)|
|`microsoftTeams.registerChangeSettingsHandler()` |ユーザーがタブを再構成するために [有効な**設定**] ボタンを選択したときに登録されるハンドラー。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |アプリによって所有されているタブを取得します。 コールバックは、 **Tabinformation**オブジェクトを取得します。 **Tabinstanceparameters**オブジェクトは、省略可能なパラメーターです。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|ユーザーに対して最後に使用されたタブを取得します。 コールバックは、 **Tabinformation**オブジェクトを取得します。 **Tabinstanceparameters**オブジェクトは、省略可能なパラメーターです。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.teaminformation?view=msteams-client-js-latest)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|**DeepLinkParameters**オブジェクトを入力として受け取り、ユーザーが*タブ内の*コンテンツに移動するために使用できるディープリンクダイアログボックスを共有します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-)<br/>[ディープリンク obj](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|必要な**ディープリンク**を入力として受け取り、ユーザーを URL に移動するか、または*チーム内の*アプリを開く、インストールするなどのクライアントアクションをトリガーします。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|**Tabinstance**オブジェクトを入力として受け取り、指定された tab インスタンスに移動します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest)|

## <a name="authentication-namespace"></a>認証名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|呼び出し元によって提供されたパラメーターを使用して新しいウィンドウを開く認証要求を開始します。 オプションの入力値は、 **AuthenticateParameters**オブジェクトによって定義されます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#authenticate-authenticateparameters-)<br/>[auth obj](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|認証要求を開始したフレームに、要求が成功したことを通知し、[認証] ウィンドウを閉じます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#notifysuccess-string--string-)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|認証要求を開始したフレームに、要求が失敗したことを通知し、認証ウィンドウを閉じます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#notifyfailure-string--string-)|

## <a name="settings-namespace"></a>Settings 名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|初期値は false です。 有効状態が true の場合、[**保存**] または [**削除**] ボタンをアクティブにします。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#setvaliditystate-boolean-)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|現在のインスタンスの設定を取得します。 コールバックは、 **Settings**オブジェクトを取得します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#getsettings--instancesettings--settings-----void-)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|現在のインスタンスの設定を構成します。 有効な設定は、 **settings**オブジェクトによって定義されます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#setsettings-settings-)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|ユーザーが [**保存**] ボタンを選択したときに登録されるハンドラー。 このハンドラーは、コンテンツを電源にする基礎となるリソースを作成または更新するために使用します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#registeronsavehandler--evt--saveevent-----void-)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|ユーザーが [**削除**] ボタンを選択したときに登録されるハンドラー。 このハンドラーを使用して、コンテンツを電源にしている基になっているリソースを削除します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#registeronremovehandler--evt--removeevent-----void-)|

## <a name="tasks-namespace"></a>Tasks 名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|**Taskinfo**オブジェクトを入力として受け取り、アプリでタスクモジュールを開くことができるようにします。 オプションの**Submithandler**は、タスクモジュールが完了するときに登録されます。 |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#starttask-taskinfo---err--string--result--string-----void-)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|タスクモジュールを送信します。 省略可能な**result** string パラメーターは、ボットまたはアプリに送信される結果で、通常は JSON オブジェクトまたはシリアル化です。省略可能な**Appids**文字列または文字列配列パラメーターは、呼び出しがタスクモジュールを起動したものと同じ appId から発信されたことを検証するのに役立ちます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---)|