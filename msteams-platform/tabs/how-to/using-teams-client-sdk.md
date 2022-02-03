---
title: JavaScript クライアント SDK でタブやその他のホストされたエクスペリエンスを構築する
author: heath-hamilton
ms.author: surbhigupta
description: JavaScript クライアント SDK Microsoft Teamsの概要。これは、JavaScript クライアント SDK でホストされるTeamsアプリ エクスペリエンスの構築に役立ちます。 <iframe>. これには、基本的な機能、認証名前空間、および設定名前空間が含まれます。
ms.localizationpriority: medium
keywords: teams タブ グループ チャネル構成可能な静的 SDK JavaScript 個人用
ms.topic: conceptual
ms.openlocfilehash: 1c8f36348a5227726e466e3d3a8ffb3e6eadd19d
ms.sourcegitcommit: 58a24422bb04a529b6629a56803ed2efabc17cb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2022
ms.locfileid: "62323191"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>JavaScript クライアント SDK を使用してタブやその他のホストMicrosoft Teamsエクスペリエンスを構築する

JavaScript Microsoft Teams SDK を使用すると、Teams でホストされたエクスペリエンスを作成できます。つまり、アプリ のコンテンツを iframe に表示します。

SDK は、次の機能を使用してアプリを開発Teamsです。

* [タブ](../../tabs/what-are-tabs.md)
* [タスク モジュール](../../task-modules-and-cards/what-are-task-modules.md)

たとえば、SDK は、ユーザーがクライアント[](../../build-your-first-app/build-personal-tab.md#3-update-your-tab-theme)で行ったテーマの変更にタブをTeamsできます。

## <a name="getting-started"></a>はじめに

開発の基本設定に応じて、次のいずれかを実行します。

* [npm または Yarn を使用して SDK をインストールする](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* [SDK の複製 (GitHub)](https://github.com/OfficeDev/microsoft-teams-library-js)

## <a name="common-sdk-functions"></a>一般的な SDK 関数

一般的に使用される SDK 関数については、次の表を参照してください。 [SDK リファレンス ドキュメントは、より](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)包括的な情報を提供します。

### <a name="basic-functions"></a>基本関数

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | SDK を初期化します。 この関数は、他の SDK 呼び出しの前に呼び出す必要があります。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-initialize&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| ページが実行されている現在の状態を取得します。 コールバックは Context オブジェクトを **取得** します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)<br/>[context obj](/javascript/api/@microsoft/teams-js/@microsoft.teams-js?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | コンテンツ ライブラリをTeamsし、contentUrl と websiteUrl に応じて[](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)タブのフレーム コンテキストを設定します。 これにより、web サイトへの移動/再読み込み機能が正しい URL で動作します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-initializewithframecontext&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | contentUrl と websiteUrl [](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) に応じてタブのフレーム コンテキストを設定します。 これにより、web サイトへの移動/再読み込み機能が正しい URL で動作します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-setframecontext&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |ユーザーがタブのフルスクリーン/ウィンドウ ビューを切り替えたときに登録されるハンドラー。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-registerfullscreenhandler&preserve-view=true)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-registerfullscreenhandler&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |ユーザーが有効なタブ ボタンを選択してタブを再構成 **設定登録される** ハンドラー。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |アプリが所有するタブを取得します。 コールバックは **TabInformation オブジェクトを取得** します。 **TabInstanceParameters オブジェクト** はオプションのパラメーターです。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-gettabinstances&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|ユーザーの最近使用したタブを取得します。 コールバックは **TabInformation オブジェクトを取得** します。 **TabInstanceParameters オブジェクト** はオプションのパラメーターです。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-getmrutabinstances&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|**DeepLinkParameters** オブジェクトを入力として受け取り、ユーザーがタブ内のコンテンツに移動するために使用できるディープ リンク ダイアログ *ボックスを共有します*。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-sharedeeplink&preserve-view=true)<br/>[deepLink obj](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|必要な **deepLink** を入力として受け取り、ユーザーを URL に移動したり、クライアントアクション (開く、インストールするなど) *をトリガーしたり* します。Teams。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-executedeeplink&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|**TabInstance オブジェクトを** 入力として受け取り、指定したタブ インスタンスに移動します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-navigatetotab&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>認証名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|呼び出し元が提供するパラメーターを含む新しいウィンドウを開く認証要求を開始します。 オプションの入力値は **、AuthenticateParameters オブジェクトによって定義** されます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|要求が成功したという認証要求を開始したフレームに通知し、認証ウィンドウを閉じます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|認証要求を開始したフレームに、要求が失敗したと通知し、認証ウィンドウを閉じます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.getAuthToken(authTokenRequest: AuthTokenRequest)`|アプリに代わってAzure ADトークンを発行する要求を送信します。 トークンの有効期限が切れていない場合は、キャッシュからトークンを取得できます。 それ以外の場合は、新しいトークンを取得Azure AD要求が送信されます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true)|

### <a name="settings-namespace"></a>設定名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|初期値は false です。 有効状態 **が true の場合****は、[** 保存] または [削除] ボタンをアクティブにします。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|現在のインスタンスの設定を取得します。 コールバックは、**オブジェクトの設定** します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|現在のインスタンスの設定を構成します。 有効な設定は、オブジェクト **によって設定** されます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|ユーザーが [保存] ボタンを選択すると **登録されるハンドラー** 。 このハンドラーは、コンテンツに電力を供給する基になるリソースを作成または更新するために使用する必要があります。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|ユーザーが [削除] ボタンを選択すると **登録されるハンドラー** 。 このハンドラーは、コンテンツに電力を供給する基になるリソースを削除するために使用する必要があります。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>タスク モジュールの名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|**TaskInfo オブジェクトを** 入力として受け取り、アプリがタスク モジュールを開くことを許可します。 オプションの **submitHandler は** 、タスク モジュールが完了すると登録されます。 |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|タスク モジュールを送信します。 オプションの **結果** 文字列パラメーターは、ボットまたはアプリに送信される結果であり、通常は JSON オブジェクトまたはシリアル化です。省略可能 **な appIds** 文字列または文字列配列パラメーターは、タスク モジュールを呼び出した appId と同じ appId から呼び出された呼び出しを検証する際に便利です。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-tasks-submittask&preserve-view=true)|
