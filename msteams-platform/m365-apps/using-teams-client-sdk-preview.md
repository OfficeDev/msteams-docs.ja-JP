---
title: Microsoft Teams JavaScript クライアント SDK v2 プレビュー
description: JavaScript クライアント SDK v2 プレビュー Microsoft Teams変更点を理解する
ms.date: 11/15/2021
ms.topic: conceptual
ms.custom: m365apps
ms.openlocfilehash: 646bebc22a31f01ea98cb367b8c8292b07c2e8f3
ms.sourcegitcommit: 239807b74aa222452559509d49c4f2808cd9c9ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2021
ms.locfileid: "61391340"
---
# <a name="microsoft-teams-javascript-client-sdk-v2-preview"></a>Microsoft Teams JavaScript クライアント SDK v2 プレビュー

Microsoft Teams [JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true)クライアント SDK v2 プレビューでは、Teams 開発者が Outlook および Office で実行する Teams アプリを拡張する機能を有効にするために、既存の Teams SDK (、または単に) がリファクタ `@microsoft/teams-js` `TeamsJS` [リングされました](overview.md)。 機能的な観点から、TeamsJS SDK v2 Preview ( ) は現在の TeamsJS SDK のスーパーセットであり、Outlook および Office で Teams アプリをホストする機能を追加しながら、既存の Teams アプリ機能をサポートします。 `@microsoft/teams-js@next`

TeamsJS SDK v2 Preview には、他のアプリケーションで実行するためにコードが考慮する必要がある重要な 2 つのMicrosoft 365があります。

* [**コールバック関数は Promise オブジェクトを返す。**](#callbacks-converted-to-promises) コールバック パラメーターを持つすべての既存の関数が最新化され、非同期操作の処理とコードの読みやすさが向上するために JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) オブジェクトが返されます。

 - [**API が機能に *整理されました*。**](#apis-organized-into-capabilities) 機能は、、などの同様の機能を提供する API の論理的なグループと `authentication` `calendar` `mail` `monetization` `meeting` 考えてできます `sharing` 。

 次のセクションで[Teams Toolkit](https://aka.ms/teams-toolkit)説明Visual Studio Code、Teams アプリの更新プロセスを簡略化するために、Teams Toolkit拡張機能を使用できます。

> [!NOTE]
> 既存のアプリを Teamsで実行するには、次OutlookとOffice両方が必要です。
> 1. 以降の依存関係 `@microsoft/teams-js@2.0.0-beta.1` 、および
> 2. このドキュメントで説明されている必要な変更に従って既存のアプリケーション コードを変更します。
>
>  既存のアプリから参照 (または後で) Teams、コードが変更された API を呼び出した場合、廃止の警告 `@microsoft/teams-js@2.0.0-beta.1` が表示されます。 既存の Teams アプリが TeamsJS SDK v2 プレビューで動作するコードを更新できるまで、Teams で作業を続行するには、API 変換レイヤー (現在の SDK をマッピングして SDK API 呼び出しをプレビューする) が用意されています。 この記事で説明されている変更を使用してコードを更新すると、個人用タブは、OutlookおよびOffice。

## <a name="updating-to-the-teams-client-sdk-v2-preview"></a>クライアント SDK v2 プレビュー Teams更新する

TeamsJS SDK v2 プレビューを使用するように Teams アプリを更新する最も簡単な方法[](https://aka.ms/teams-toolkit)は、Teams Toolkit拡張機能を使用Visual Studio Code。 このセクションでは、これを行う手順について説明します。 コードを手動で更新する場合は、必要な API の変更の詳細については[](#apis-organized-into-capabilities)[、「Promises](#callbacks-converted-to-promises)に変換されたコールバックと API を機能に整理する」セクションを参照してください。

### <a name="1-install-the-latest-teams-toolkit-vs-code-extension"></a>1. 最新の拡張機能をTeams Toolkit VS Codeする

[拡張機能 *Visual Studio Codeマーケット* プレースで、Teams Toolkit **を検索** し、バージョン以降 `2.10.0` をインストールします。 ツールキットには、プロセスを支援する 2 つのコマンドがあります。

1. マニフェスト スキーマを更新するコマンド
1. SDK 参照を更新してサイトを呼び出すコマンド

他のアプリケーションで個人用タブ アプリを実行する必要Teams 2 つのMicrosoft 365次に示します。

### <a name="2-updating-the-manifest"></a>2. マニフェストの更新

# <a name="teams-toolkit"></a>[Teams Toolkit](#tab/manifest-teams-toolkit)

1. コマンド パレット *を開きます*。 `Ctrl+Shift+P`
1. **[Teams: Teamsを** アップグレードしてOutlookアプリOfficeをサポートし、アプリ マニフェスト ファイルを選択します。 変更は、その場で行います。

# <a name="manual-steps"></a>[手動の手順](#tab/manifest-manual)

アプリ マニフェストTeams開き、次の `$schema` 値 `manifestVersion` を使用して更新します。

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

個人用アプリのTeams Toolkit使用した場合は、マニフェスト ファイルの変更を検証し、エラーを特定するために使用することもできます。 コマンド パレットを開き、Teams: マニフェスト ファイルを検証するか、Teams Toolkit の [展開] メニューからオプションを選択します (Visual Studio Code の左側にある Teams アイコン `Ctrl+Shift+P` を探します)。 

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit [展開] メニューの [マニフェスト ファイルの検証] オプションを選択します。":::

### <a name="2-update-sdk-references"></a>2. SDK 参照の更新

アプリを OutlookおよびOfficeするには [、npm](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0-beta.1)パッケージ (または後のベータ版) に依存 `@microsoft/teams-js@2.0.0-beta.1` する *必要* があります。 これらの手順を手動で実行し、API の変更の詳細については [、「Callbacks](#callbacks-converted-to-promises) に変換された Promise と API を機能に整理する」のセクションを [参照してください](#apis-organized-into-capabilities)。

1. 次[のTeams Toolkit](https://aka.ms/teams-toolkit) `v2.10.0` 確認する
1. コマンド パレット *を開きます*。 `Ctrl+Shift+P`
1. コマンドを実行する `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

完了すると、ユーティリティは TeamsJS SDK v2 Preview (以降) の依存関係を使用してファイルを更新し、ファイルとファイルは次の形式 `package.json` `@microsoft/teams-js@2.0.0-beta.1` `*.js/.ts` `*.jsx/.tsx` で更新されます。

> [!div class="checklist"]
> * `package.json` TeamsJS SDK v2 Preview への参照
> * TeamsJS SDK v2 プレビューのインポート ステートメント
> * [TeamsJS SDK](#apis-organized-into-capabilities) v2 プレビューへの関数、列挙、およびインターフェイスの呼び出し
> * `TODO`コンテキスト インターフェイスの変更によって影響を受け得る可能性がある領域を確認するコメント[リマインダー](#updates-to-the-context-interface)
> * `TODO` コールバック スタイル関数からの [promises](#callbacks-converted-to-promises) 関数への変換がツールが見つかったすべての呼び出しサイトでうまくいったと確認するためのコメントリマインダー

> [!IMPORTANT]
> html ファイル内のコードはアップグレード ツールではサポートされません。手動で変更する必要があります。

## <a name="callbacks-converted-to-promises"></a>Promise に変換されたコールバック

Teamsコールバック パラメーターを受け取った API が更新され、JavaScript Promise オブジェクトが[返](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)されます。 これには、次の API が含まれます。

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, core.executeDeepLink, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, media.captureImage, media.getMedia, media.selectMedia, media.viewImages, media.scanBarCode, meeting.getAppContentStageSharingCapabilities, meeting.getAuthenticationTokenForAnonymousUser, meeting.getIncomingClientAudioState, meeting.getLiveStreamState, meeting.getMeetingDetails, meeting.requestStartLiveStreaming, meeting.requestStopLiveStreaming, meeting.shareAppContentToStage, meeting.stopSharingAppContentToStage, meeting.toggleIncomingClientAudio, meeting.getAppContentStageSharingState, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.config.setConfig, pages.config.getConfig, people.selectPeople, ChildAppWindow.postMessage, ParentAppWindow.postMessage
```

Promises を使用するには、コードがこれらの API を呼び出す方法を更新する必要があります。 たとえば、コードが次のような api Teams呼び出している場合は、次のようになります。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

このコード:

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => { /* ... */ });
```

次に更新する必要があります。

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

...または同等の `async/await` パターン:

```js
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context = await app.getContext();
  /*...*/
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

このコード:

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context: microsoftTeams.Context) => {
  /* ... */
});
```

次に更新する必要があります。

```TypeScript
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

...または同等の `async/await` パターン:

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

---

> [!TIP]
> Teams Toolkit を使用して TeamsJS SDK v2[](#updating-to-the-teams-client-sdk-v2-preview)プレビューのコードを更新すると、必要な更新プログラムに対して、クライアント コード内のコメントのフラグ `TODO` が設定されます。

## <a name="apis-organized-into-capabilities"></a>機能に整理された API

機能 *とは* 、同様の機能を提供する API の論理グループです。 ホストは、Microsoft Teams、Outlook、Officeと考える場合があります。 ホストは、その機能内で定義されているすべての API をサポートする場合、特定の機能をサポートします。 ホストは機能を部分的に実装できません。  機能には、ダイアログや認証などの機能ベースまたはコンテンツ *ベースの機能**があります*。 また、タブ/ページやボットなどのアプリケーションの種類や、その他のグループ化に対する機能も用意されています。

TeamsJS SDK v2 プレビューでは、API は JavaScript 名前空間の関数として定義され、名前は必要な機能と一致します。 アプリがダイアログ機能をサポートするホストで実行されている場合、アプリは (名前空間で定義されている他のダイアログ関連の API に加えて) などの API を安全に呼び出 `dialog.open` します。 一方、アプリがホストでサポートされていない API を呼び出す場合、API は例外をスローします。

### <a name="differentiate-your-app-experience"></a>アプリ エクスペリエンスを区別する

実行時に特定の機能のホストサポートを確認するには、その機能 (名前空間) で関数 `isSupported()` を呼び出します。 サポートされている `true` 場合とサポートされていない場合は返され、必要に応じてアプリの `false` 動作を調整できます。 これにより、アプリはサポートするホストの UI と機能を明るくみ、サポートしないホストでは引き続き実行できます。

アプリが実行されているホストの名前は、コンテキスト インターフェイス ( ) の *hostName* プロパティとして公開され、実行時に呼び出すことによってクエリ `app.Context.app.host.name` を実行できます `getContext` 。 URL プレースホルダー値 `{hostName}` [として使用することもできます](../tabs/how-to/access-teams-context.md#get-context-by-inserting-url-placeholder-values)。 ベスト プラクティスは *、hostName メカニズムを注意* して使用する方法です。

* **hostName プロパティ** の値に基づいて、ホスト内で特定の機能が使用できる、または使用できないと想定し、 *使用* できません。 代わりに、機能のサポート ( ) を確認します `isSupported` 。
* **hostName を使用***して API 呼び出* しをゲートしない。 代わりに、機能のサポート ( ) を確認します `isSupported` 。
* **hostName** *を使用して* 、実行中のホストに基づいてアプリケーションのテーマを区別します。 たとえば、Microsoft Teamsで実行する場合はMicrosoft Teams Teamsのアクセントカラーとして、Outlookで実行する場合は青色を使用Outlook。
* **hostName** *を使用して* 、実行しているホストに基づいてユーザーに表示されるメッセージを区別します。 たとえば、「Office で実行中にタスクを管理する *」Office on the web、Teams* で実行中にタスクを管理するをMicrosoft Teams。

### <a name="namespaces"></a>名前空間

TeamsJS SDK v2 Preview は、名前空間を使用して API を機能に整理します。 特に重要ないくつかの新しい名前空間は、*アプリ*、*ページ*、*ダイアログ、**および teamsCore です*。

#### <a name="app-namespace"></a>*アプリの* 名前空間

名前空間には、アプリ全体の使用状況に必要なトップ レベルの API が含 `app` Microsoft Teams、Office、Outlook。 他のさまざまな TeamsJS 名前空間のすべての API が `app` TeamsJS SDK v2 プレビューの名前空間に移動されました。

| 元の名前空間 `global (window)` | 新しい名前空間 `app` |
| - | - |
| `initialize` | `app.initialize` |
| `getContext` | `app.getContext` |
| `registerOnThemeChangeHandler` | `app.registerOnThemeChangeHandler` |

| 元の名前空間 `appInitialization` | 新しい名前空間 `app` |
| - | - |
| `appInitialization.notifyAppLoaded` | `app.notifyAppLoaded` |
| `appInitialization.notifySuccess` | `app.notifySuccess` |
| `appInitialization.notifyFailure` | `app.notifyFailure` |
| `appInitialization.notifyExpectedFailure` | `app.notifyExpectedFailure` |
| `appInitialization.FailedReason` enum | `app.FailedReason` |
| `appInitialization.ExpectedFailureReason` enum | `app.ExpectedFailureReason` |
| `appInitialization.IFailedRequest` enum | `app.IFailedRequest` |
| `appInitialization.IExpectedFailureRequest` enum | `app.IExpectedFailureRequest` |

#### <a name="core-namespace"></a>*コア* 名前空間

名前空間 `core` には、ディープ リンクの機能が含まれています。

| 元の名前空間 `publicAPIs` | 新しい名前空間 `core` |
| - | - |
| `shareDeepLink` | `core.shareDeepLink` |
| `executeDeepLink` | `core.executeDeepLink` |

#### <a name="pages-namespace"></a>*pages* 名前空間

名前空間には、さまざまなクライアント内で web ページを実行および移動するための機能が含Microsoft 365、Teams、Office、Outlook。 `pages` また、サブ名前空間として実装されたいくつかのサブ機能も含まれています。

| 元の名前空間 `global (window)` | 新しい名前空間 `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame` (名前の変更) |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |

##### <a name="pagestabs"></a>*pages.tabs*

| 元の名前空間 `global (window)` | 新しい名前空間 `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |
| ` navigateToTab` | `pages.tabs.navigateToTab` |

| 元の名前空間 `navigation` | 新しい名前空間 `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

##### <a name="pagesconfig"></a>*pages.config*

| 元の名前空間 `settings` | 新しい名前空間 `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig` (名前の変更)
| `settings.getSettings` | `pages.config.getConfig` (名前の変更)
| `settings.setValidityState`| `pages.config.setValidityState`
| `settings.initialize` | `pages.config.initialize`
| `settings.registerOnSaveHandler`| `pages.config.registerOnSaveHandler`
| `settings.registerOnRemoveHandler` | `pages.config.registerOnRemoveHandler`
| `settings.Settings` インターフェイス | `pages.config.Config` (名前の変更)
| `settings.SaveEvent` インターフェイス | `pages.config.SaveEvent` (名前の変更)
| `settings.RemoveEvent` インターフェイス | `pages.config.RemoveEvent` (名前の変更)
| `settings.SaveParameters` インターフェイス | `pages.config.SaveParameters` (名前の変更)
| `settings.SaveEventImpl` インターフェイス | `pages.config.SaveEventImpl` (名前の変更)

| 元の名前空間 `global (window)` | 新しい名前空間 `pages.config` |
| - | - |
| `registerEnterSettingsHandler` | `pages.config.registerChangeConfigHandler` (名前の変更)

##### <a name="pagesbackstack"></a>*pages.backStack*

| 元の名前空間 `navigation` | 新しい名前空間 `pages.backStack`  |
| - | - |
| `navigation.navigateBack` | `pages.backStack.navigateBack`

| 元の名前空間 `global (window)` | 新しい名前空間 `pages.backStack`  |
| - | - |
| `registerBackButtonHandler` | `pages.backStack.registerBackButtonHandler`

##### <a name="pagesappbutton"></a>*pages.appButton*

| 元の名前空間 `global (window)` | 新しい名前空間 `pages.appButton`  |
| - | - |
| `registerAppButtonClickHandler` | `pages.appButton.onClick` (名前の変更)
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter` (名前の変更)
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave` (名前の変更)
| `FrameContext` インターフェイス | `pages.appButton.FrameInfo` (名前の変更)) |

#### <a name="dialog-namespace"></a>*dialog* 名前空間

TeamsJS *タスク名前空間* の名前がダイアログに変更 *され*、次の API の名前が変更されました。

| 元の名前空間 `tasks` | 新しい名前空間 `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open` (名前の変更) |
| `tasks.submitTasks` | `dialog.submit` (名前の変更) |
| `tasks.updateTasks` | `dialog.resize` (名前の変更) |
| `tasks.TaskModuleDimension` enum | `dialog.DialogDimension` (名前の変更) |
| `tasks.TaskInfo` インターフェイス | `dialog.DialogInfo` (名前の変更) |

#### <a name="teamscore-namespace"></a>*teamsCore* 名前空間

TeamsJS SDK を一般化して、Office や Outlook などの他の Microsoft 365 ホストを実行するために、Teams 固有の機能 (もともとはグローバル名前空間) が *teamsCore 名前空間に移動* されました。

| 元の名前空間 `global (window)` | 新しい名前空間 `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`
| `registerFocusEnterHandler` | `teamsCore.registerFocusEnterHandler`

### <a name="updates-to-the-context-interface"></a>コンテキスト インターフェイス *の* 更新

インターフェイスは名前空間に移動され、Outlook および Office で実行されるだけでなく、Outlook と Office で実行される同様のプロパティをグループ化 `Context` `app` Teams。

ホスト アプリケーションに応じて個人用タブでユーザー エクスペリエンスを区別するための新しいプロパティ `app.Context.app.host.name` が追加されました。

TeamsJS SDK v2 プレビュー ソースの関数を確認して、変更  [`transformLegacyContextToAppContext`](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/src/public/app.ts) を視覚化することもできます。

| インターフェイスの元の `Context` 名前 | 新しい場所 `app.Context` |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *NOT IN Teams SDK v2 Preview* |
| `appSessionId` | `app.Context.app.sessionId`|
| `channelId`| `app.Context.channel.id` |
| `channelName`| `app.Context.channel.displayName`|
| `channelRelativeUrl` | `app.Context.channel.relativeUrl`|
| `channelType`| `app.Context.channel.membershipType` |
| `chatId` | `app.Context.chat.id`|
| `defaultOneNoteSectionId`| `app.Context.channel.defaultOneNoteSectionId`|
| `entityId` | `app.Context.page.id`|
| `frameContext` | `app.Context.page.frameContext`|
| `groupId`| `app.Context.team.groupId` |
| `hostClientType` | `app.Context.app.host.clientType`|
| `hostTeamGroupId`| `app.Context.channel.ownerGroupId` |
| `hostTeamTenantId` | `app.Context.channel.ownerTenantId`|
| `isCallingAllowed` | `app.Context.user.isCallingAllowed`|
| `isFullScreen` | `app.Context.page.isFullScreen`|
| `isMultiWindow`| `app.Context.page.isMultiWindow` |
| `isPSTNCallingAllowed` | `app.Context.user.isPSTNCallingAllowed`|
| `isTeamArchived` | `app.Context.team.isArchived`|
| `locale` | `app.Context.app.locale` |
| `loginHint`| `app.Context.user.loginHint` |
| `meetingId`| `app.Context.meeting.id` |
| `osLocaleInfo` | `app.Context.app.osLocaleInfo` |
| `parentMessageId`| `app.Context.app.parentMessageId`|
| `ringId` | `app.Context.app.host.ringId`|
| `sessionId`| `app.Context.app.host.sessionId` |
| `sourceOrigin` | `app.Context.page.sourceOrigin`|
| `subEntityId`| `app.Context.page.subPageId` |
| `teamId` | `app.Context.team.internalId`|
| `teamSiteDomain` | `app.Context.sharepointSite.domain`|
| `teamSitePath` | `app.Context.sharepointSite.path`|
| `teamSiteUrl`| `app.Context.sharepointSite.url` |
| `teamTemplateId` | `app.Context.team.templateId`|
| `teamType` | `app.Context.team.type`|
| `tenantSKU`| `app.Context.user.tenant.teamsSku` |
| `tid`| `app.Context.user.tenant.id` |
| `upn` | `app.Context.user.userPrincipalName` |
|` userClickTime`| `app.Context.app.userClickTime`|
| `userFileOpenPreference` | `app.Context.app.userFileOpenPreference` |
| `userLicenseType`| `app.Context.user.licenseType` |
| `userObjectId` | `app.Context.user.id`|
| ` userTeamRole` | `app.Context.team.userRole`|
| `userDisplayName` | `app.Context.user.displayName` |
| N/A | `app.Context.app.host.name`|

## <a name="next-steps"></a>次の手順

[また、TeamsJS SDK v2 Preview changelog](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/CHANGELOG.md)および[TeamsJS SDK v2 Preview API リファレンス](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true)の変更点の詳細について説明します。

アプリで実行されているアプリをテストするTeams、OutlookをOfficeしてください。

> [!div class="nextstepaction"]
> [アプリをTeams拡張Microsoft 365](overview.md)
