---
title: JavaScript クライアント SDK を使用してタブやその他のホストされたエクスペリエンスを構築する
author: heath-hamilton
ms.author: surbhigupta
description: ホストされた Teams アプリ エクスペリエンスの構築に役立つ Microsoft Teams JavaScript クライアント SDK の概要。 <iframe>. これには、基本関数、認証の名前空間、および設定の名前空間が含まれます。
ms.localizationpriority: medium
keywords: Teams タブ グループ チャンネル 構成可能な静的 SDK JavaScript 個人用
ms.topic: conceptual
ms.openlocfilehash: e5dcacc4dbd3cdf63fc479f3e24fedfd3b819223
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356274"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Microsoft Teams JavaScript クライアント SDK を使用してタブやその他のホストされたエクスペリエンスを構築する

Microsoft Teams JavaScript クライアント SDK は、Teams でホストされたエクスペリエンスを作成するのに役立ちます。それは、アプリ コンテンツを iframe に表示することを意味します。

SDK は、次のいずれの Teams 機能をも備えたアプリの開発に役立ちます:

* [タブ](../../tabs/what-are-tabs.md)
* [タスク モジュール](../../task-modules-and-cards/what-are-task-modules.md)

たとえば、SDK を使用すると、ユーザーがTeams クライアントで行う[テーマの変更にタブを反応](../../build-your-first-app/build-personal-tab.md#3-update-your-tab-theme)させることができます。

## <a name="getting-started"></a>はじめに

開発の設定に応じて、次のいずれかの操作を行います:

* [npm または Yarn を使用して SDK をインストールする](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* [SDK を複製する (GitHub)](https://github.com/OfficeDev/microsoft-teams-library-js)

## <a name="common-sdk-functions"></a>共通 SDK 関数

共用される SDK 関数を理解するには、次の表を参照してください。 [SDK リファレンス ドキュメント](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)には、より包括的な情報が記載されています。

### <a name="basic-functions"></a>基本的な関数

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | SDK を初期化する。 この関数は、他の SDK を呼び出す前に、呼び出される必要があります。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-initialize&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| ページが実行されている現在の状態を取得します。 コールバックは **Context** オブジェクトを再取得します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)<br/>[context obj](/javascript/api/@microsoft/teams-js/@microsoft.teams-js?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Teams ライブラリを初期化し、contentUrl と websiteUrl に応じてタブの [frame context](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) を設定します。 これにより、go-to-website/reload 機能が正しい URL 上で作動することを確実にします。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-initializewithframecontext&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | contentUrl と websiteUrl に応じて、タブの [frame context](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) を設定します。 これにより、go-to-website/reload 機能が正しい URL 上で作動することを確実にします。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-setframecontext&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: Boolean)` |ユーザーがタブの full-screen/windowed ビューを切り替えたときに登録されるハンドラー。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-registerfullscreenhandler&preserve-view=true)<br/>[Boolean](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-registerfullscreenhandler&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |ユーザーがタブを再構成するために、有効化された **設定** ボタンを選択したときに登録されるハンドラー。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |アプリがオーナーであるタブを取得する。 コールバックは、**TabInformation** オブジェクトを再取得します。 **TabInstanceParameters** オブジェクトはオプションのパラメーターです。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-gettabinstances&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|ユーザーが最近使用したタブを取得します。 コールバックは、**TabInformation** オブジェクトを再取得します。 **TabInstanceParameters** オブジェクトはオプションのパラメーターです。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-getmrutabinstances&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|**DeepLinkParameters** オブジェクトを入力として受け取り、ユーザーが *タブ内* でコンテンツ移動に利用できるディープ リンク ダイアログ ボックスを共有します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-sharedeeplink&preserve-view=true)<br/>[deepLink obj](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: Boolean, reason?: string))`|必要な **deepLink** を入力として受け取り、ユーザーを URL に引き渡すか—または、起動したりインストールするなど—*Teams 内* のアプリでクライアント アクションを誘起します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-executedeeplink&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: Boolean, reason?: string))`|**TabInstance** オブジェクトを入力として受け取り、指定されたタブ インスタンスに引き渡します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-navigatetotab&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>認証の名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|呼び出し元によって指定されたパラメーターを使用して、新規ウィンドウを開く認証要求を初期化します。 オプションの入力値は、**AuthenticateParameters** オブジェクトによって定義されます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|要求が成功したことを、認証要求を初期化したフレームに通知し、認証ウィンドウを閉じます|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|要求が失敗したことを、認証要求を開始したフレームに通知し、認証ウィンドウを閉じます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.getAuthToken(authTokenRequest: AuthTokenRequest)`|アプリの代理として、Azure AD トークンを発行する要求を送信します。 有効期限が切れていない場合は、トークンをキャッシュから取得できます。 それ以外の場合は、新しいトークンを取得するために Azure AD に要求が送信されます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true)|

### <a name="settings-namespace"></a>設定の名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: Boolean)`|既定値は false です。 有効性が true の場合、**[保存]** または **[削除]** ボタンをアクティブにします。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|現用インスタンスの設定を取得します。 コールバックは、**Settings** オブジェクトを再取得します。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: Boolean, reason?: string)`|現用インスタンスの設定を構成します。 有効な設定は、**Settings** オブジェクトによって定義されます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|ユーザーが **[保存]** ボタンを選択したときに登録されるハンドラー。 このハンドラーは、コンテンツを供給する基になるリソースを作成または更新するために使用する必要があります。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|ユーザーが **[削除]** ボタンを選択したときに登録されるハンドラー。 このハンドラーは、コンテンツを供給する基になるリソースを削除するために使用する必要があります。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>タスク モジュールの名前空間

| 関数  | 説明          | ドキュメント|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|**TaskInfo** オブジェクトを入力として受け取り、アプリがタスク モジュールを開くことを許可します。 オプションの **submitHandler** は、タスク モジュールの完了時に登録されます。 |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|タスク モジュールを提出します。 オプションの **result** 文字列パラメーターは、ボットまたはアプリに送信される結果であり、通常は JSON オブジェクトまたはシリアル化されています。オプションの **appIds** 文字列または文字列配列パラメーターは、呼び出しがタスク モジュールの呼び出し元と同じ appId から発行されたことを検証することを助けます。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-tasks-submittask&preserve-view=true)|
