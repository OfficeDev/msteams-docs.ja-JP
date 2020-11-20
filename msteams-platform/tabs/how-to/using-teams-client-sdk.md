---
title: Teams クライアント SDK を使用する
author: laujan
description: Teams クライアント SDK を使用して、ユーザー設定のタブに Teams 対応機能を追加する方法
keywords: teams タブグループチャネルの構成可能な静的 SDK JavaScript personal
ms.topic: conceptual
ms.openlocfilehash: 0a701e3baff08b35592288408cf32d0a2a0a2584
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346785"
---
# <a name="using-the-teams-client-sdk"></a>Teams クライアント SDK を使用する

**Teams javascript クライアント SDK** および **teams javascript ライブラリ** は、 [Microsoft teams 開発者プラットフォーム](/microsoftteams/platform/)の一部であり、teams アプリケーションの作成を容易にするツールとプロセスを提供します。 Teams クライアント SDK は、npm パッケージとして配布されます。 最新バージョンについては、「」を参照して <https://www.npmjs.com/package/@microsoft/teams-js> ください。 Teams ライブラリは、にあり <https://github.com/OfficeDev/microsoft-teams-library-js> ます。

次の表に、タブ開発で一般的に使用される Teams ライブラリ関数の概要を示します。

## <a name="teams-sdk-public-api"></a>Teams SDK パブリック API 

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | Teams ライブラリを初期化します。 この関数は、他の SDK 呼び出しの前に呼び出す必要があります。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| ページが実行されている現在の状態を取得します。 コールバックは、 **コンテキスト** オブジェクトを取得します。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-&preserve-view=true)<br/>[context obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | ContentUrl と websiteUrl に応じて、Teams ライブラリを初期化し、タブの [フレームコンテキスト](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) を設定します。 これにより、web サイトへの移動/再読み込みの機能が正しい URL に対して動作するようになります。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | ContentUrl と websiteUrl に応じて、タブの [フレームコンテキスト](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) を設定します。 これにより、web サイトへの移動/再読み込みの機能が正しい URL に対して動作するようになります。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |ユーザーがタブの全画面表示/ウィンドウ表示を切り替えたときに登録されるハンドラー。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-&preserve-view=true)<br/>[boolean](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerFullScreenHandler__isFullScreen__boolean_____void_&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |ユーザーがタブを再構成するために [有効な **設定** ] ボタンを選択したときに登録されるハンドラー。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |アプリによって所有されているタブを取得します。 コールバックは、 **Tabinformation** オブジェクトを取得します。 **Tabinstanceparameters** オブジェクトは、省略可能なパラメーターです。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|ユーザーに対して最後に使用されたタブを取得します。 コールバックは、 **Tabinformation** オブジェクトを取得します。 **Tabinstanceparameters** オブジェクトは、省略可能なパラメーターです。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|**DeepLinkParameters** オブジェクトを入力として受け取り、ユーザーが *タブ内の* コンテンツに移動するために使用できるディープリンクダイアログボックスを共有します。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-&preserve-view=true)<br/>[ディープリンク obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|必要な **ディープリンク** を入力として受け取り、ユーザーを URL に移動するか、または *チーム内の* アプリを開く、インストールするなどのクライアントアクションをトリガーします。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|**Tabinstance** オブジェクトを入力として受け取り、指定された tab インスタンスに移動します。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-&preserve-view=true)<br/>[tabInstance obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinstance?view=msteams-client-js-latest&preserve-view=true)|

## <a name="authentication-namespace"></a>認証名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|呼び出し元によって提供されたパラメーターを使用して新しいウィンドウを開く認証要求を開始します。 オプションの入力値は、 **AuthenticateParameters** オブジェクトによって定義されます。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|認証要求を開始したフレームに、要求が成功したことを通知し、[認証] ウィンドウを閉じます。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|認証要求を開始したフレームに、要求が失敗したことを通知し、認証ウィンドウを閉じます。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|

## <a name="settings-namespace"></a>Settings 名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|初期値は false です。 有効状態が true の場合、[ **保存** ] または [ **削除** ] ボタンをアクティブにします。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|現在のインスタンスの設定を取得します。 コールバックは、 **Settings** オブジェクトを取得します。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|現在のインスタンスの設定を構成します。 有効な設定は、 **settings** オブジェクトによって定義されます。|[function](/https://docs.microsoft.com/en-us/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|ユーザーが [ **保存** ] ボタンを選択したときに登録されるハンドラー。 このハンドラーは、コンテンツを電源にする基礎となるリソースを作成または更新するために使用します。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|ユーザーが [ **削除** ] ボタンを選択したときに登録されるハンドラー。 このハンドラーを使用して、コンテンツを電源にしている基になっているリソースを削除します。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|

## <a name="tasks-namespace"></a>Tasks 名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|**Taskinfo** オブジェクトを入力として受け取り、アプリでタスクモジュールを開くことができるようにします。 オプションの **Submithandler** は、タスクモジュールが完了するときに登録されます。 |[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|タスクモジュールを送信します。 省略可能な **result** string パラメーターは、ボットまたはアプリに送信される結果で、通常は JSON オブジェクトまたはシリアル化です。省略可能な **Appids** 文字列または文字列配列パラメーターは、呼び出しがタスクモジュールを起動したものと同じ appId から発信されたことを検証するのに役立ちます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)|
