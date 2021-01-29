---
title: JavaScript クライアント SDK を使用したタブやその他のホスト型エクスペリエンスの構築
author: heath-hamilton
ms.author: surbhigupta
description: Microsoft Teams JavaScript クライアント SDK の概要。 <iframe>.
keywords: teams タブ グループ チャネル構成可能な静的 SDK JavaScript 個人用
ms.topic: conceptual
ms.openlocfilehash: 7ba900990507e2d32992d6d2c26fff07d7c84bd8
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2021
ms.locfileid: "50036998"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Microsoft Teams JavaScript クライアント SDK を使用したタブやその他のホスト型エクスペリエンスの構築

Microsoft Teams JavaScript クライアント SDK は、Teams でのホスト型エクスペリエンスの作成に役立ちます。つまり、アプリのコンテンツを iframe に表示します。

この SDK は、次の Teams 機能を備えるアプリを開発する場合に役立ちます。

* [タブ](../../tabs/what-are-tabs.md)
* [タスク モジュール](../../task-modules-and-cards/what-are-task-modules.md)

たとえば、SDK では、Teams [クライアントでユーザー](../../build-your-first-app/build-personal-tab.md#3-update-the-tab-theme) が行ったテーマの変更にタブを対応できます。

## <a name="getting-started"></a>はじめに

開発の基本設定に応じて、次のいずれかを実行します。

* [npm または The の SDK をインストールする](https://docs.microsoft.com/javascript/api/overview/msteams-client?view=msteams-client-js-latest)
* [SDK を複製する (GitHub)](https://github.com/OfficeDev/microsoft-teams-library-js)

## <a name="common-sdk-functions"></a>一般的な SDK 関数

一般的に使用される SDK 関数を理解するには、次の表を参照してください。 [SDK リファレンス ドキュメントには、より](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest)包括的な情報が含まれています。

### <a name="basic-functions"></a>基本的な関数

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | SDK を初期化します。 この関数は、他の SDK 呼び出しの前に呼び出す必要があります。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| ページが実行されている現在の状態を取得します。 コールバックは Context オブジェクトを **取得** します。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-&preserve-view=true)<br/>[context obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Teams ライブラリを初期化し、contentUrl と[](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)websiteUrl に応じてタブのフレーム コンテキストを設定します。 これにより、Web サイトへの移動/再読み込み機能が正しい URL で動作します。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | contentUrl と websiteUrl [に応じて](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) タブのフレーム コンテキストを設定します。 これにより、Web サイトへの移動/再読み込み機能が正しい URL で動作します。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |ユーザーがタブの全画面/ウィンドウビューを切り替えたときに登録されるハンドラー。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-&preserve-view=true)<br/>[boolean](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerFullScreenHandler__isFullScreen__boolean_____void_&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |ユーザーが有効な [設定] ボタンを選択してタブを再構成するときに登録されるハンドラー。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |アプリが所有するタブを取得します。 コールバックは **TabInformation オブジェクトを取得** します。 **TabInstanceParameters オブジェクト** はオプションのパラメーターです。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|ユーザーの最近使用したタブを取得します。 コールバックは **TabInformation オブジェクトを取得** します。 **TabInstanceParameters オブジェクト** はオプションのパラメーターです。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|**DeepLinkParameters** オブジェクトを入力として受け取り、ユーザーがタブ内のコンテンツに移動するために使用できるディープ リンク ダイアログ *ボックスを共有します*。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-&preserve-view=true)<br/>[deepLink obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|入力として必要な **deepLink** を受け取り、ユーザーを URL に移動するか、Teams 内のアプリを開く、インストールするなどのクライアント アクション *をトリガーします*。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|**TabInstance オブジェクトを入力として** 受け取り、指定されたタブ インスタンスに移動します。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-&preserve-view=true)<br/>[tabInstance obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>認証名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|呼び出し元が提供するパラメーターを使用して新しいウィンドウを開く認証要求を開始します。 オプションの入力値は **、AuthenticateParameters オブジェクトによって定義** されます。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|認証要求を開始したフレームに、要求が成功したと通知し、認証ウィンドウを閉じます。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|認証要求を開始したフレームに、要求が失敗したと通知し、認証ウィンドウを閉じます。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|

### <a name="settings-namespace"></a>設定の名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|初期値は false です。 有効性の状態 **が true** の **場合、[** 保存] ボタンまたは [削除] ボタンをアクティブにします。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|現在のインスタンスの設定を取得します。 コールバックは Settings オブジェクトを **取得** します。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|現在のインスタンスの設定を構成します。 有効な設定は **、Settings** オブジェクトによって定義されます。|[function](/https://docs.microsoft.com/en-us/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|ユーザーが [保存] ボタンを選択するときに **登録されるハンドラー** 。 このハンドラーは、コンテンツを提供する基になるリソースを作成または更新するために使用する必要があります。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|ユーザーが [削除] ボタンを選択するときに **登録されるハンドラー** 。 このハンドラーは、コンテンツを提供する基になるリソースを削除するために使用する必要があります。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>タスク モジュールの名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|**TaskInfo オブジェクトを** 入力として受け取り、アプリでタスク モジュールを開くことを許可します。 オプションの **submitHandler は** 、タスク モジュールが完了すると登録されます。 |[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|タスク モジュールを送信します。 オプションの **結果** 文字列パラメーターは、ボットまたはアプリに送信される結果であり、通常は JSON オブジェクトまたはシリアル化です。オプションの **appIds** 文字列または文字列配列パラメーターは、タスク モジュールを呼び出した appId と同じ appId から呼び出された呼び出しを検証する際に便利です。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)|
