---
title: Microsoft Teams JavaScript クライアント SDK を使用してタブやその他のホストされたエクスペリエンスを構築する
author: heath-hamilton
ms.author: surbhigupta
description: このモジュールでは、Microsoft Teams JavaScript クライアント SDK を学習します。これは、以下でホストされているアプリ エクスペリエンスの構築に役立ちます <iframe> でホストされたアプリ エクスペリエンスの構築に役立つ Microsoft Teams JavaScript クライアント SDK の概要。
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: 165b08b3936afe03f492d8e6983c5504d38bad8b
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189509"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Microsoft Teams JavaScript クライアント SDK を使用してタブやその他のホストされたエクスペリエンスを構築する

Microsoft Teams JavaScript クライアント SDK は、Teams、Office、Outlook でホストされたエクスペリエンスを作成するのに役立ちます。これらのサービスで、アプリ コンテンツは [iframe](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) でホストされます。 SDK は、次の Teams 機能を備えたアプリを開発するのに役立ちます。

* [タブ](../../tabs/what-are-tabs.md)
* [ダイアログ (タスク モジュール)](../../task-modules-and-cards/what-are-task-modules.md)

バージョン `2.0.0` 以降、既存の Teams クライアント SDK (`@microsoft/teams-js`、または単に `TeamsJS`) がリファクタリングされ、[Teams アプリが Microsoft Teams に加えて Outlook と Office で実行](/microsoftteams/platform/m365-apps/overview)できるようになりました。 機能的な観点から見て、TeamsJS の最新バージョンでは、既存のすべての Teams アプリ (v.1.x.x) の機能がサポートされ、Outlook と Office で Teams アプリをホストするオプション機能が追加されています。

さまざまなアプリ シナリオについて、現在のバージョン管理ガイダンスを次に示します。

[!INCLUDE [pre-release-label](~/includes/teamjs-version-details.md)]

この記事の残りの部分では、Teams JavaScript クライアント SDK の構造と最新の更新プログラムについて説明します。

### <a name="microsoft-365-support-running-teams-apps-in-office-and-outlook"></a>Microsoft 365 サポート (Office および Outlook でTeams アプリを実行する)

TeamsJS v.2.0 では、特定の種類の Teams アプリをMicrosoft 365 エコシステム全体で実行する機能が導入されています。 現在、Teams アプリの他の Microsoft 365 アプリケーション ホスト (Office と Outlook を含む) では、Teams プラットフォーム用に構築できるアプリケーションの種類と機能のサブセットがサポートされています。 このサポートは、時間の経過と共に拡張されます。 Teams アプリのホスト サポートの概要については、「[Teams アプリを Microsoft 365 全体に拡張する](../../m365-apps/overview.md)」を参照してください。

次の表は、Teams タブとダイアログ (タスク モジュール) 機能 (パブリックの名前空間) と、他の Microsoft 365 ホストで実行するためのサポートの拡張の一覧です。

> [!TIP]
> その機能 (名前空間) で `isSupported()` 関数を呼び出して、特定の機能の実行時にホスト サポートを確認します。

|機能 | ホストのサポート | 備考 |
|-----------|--------------|-------|
| アプリ | Teams、Outlook、Office | 名前空間はアプリの初期化とライフサイクルを表します。 |
| appInitialization| | 非推奨。 `app` 名前空間に置き換えられました。 |
| appInstallDialog | Teams||
| 認証 | Teams、Outlook、Office | |
| calendar | Teams、Outlook ||
| 通話 | Teams||
| チャット |Teams||
| ダイアログ | Teams、Outlook、Office | ダイアログ (以前は *タスク モジュール* という名前でした) を表す名前空間。 「[ダイアログ](#dialogs)」のメモを参照してください。 |
| 場所 |Teams| 「[アプリのアクセス許可](#app-permissions)」のメモを参照してください。|
| mail | Outlook (Windows デスクトップのみ)||
| メディア |Teams| 「[アプリのアクセス許可](#app-permissions)」のメモを参照してください。|
| ページ | Teams、Outlook、Office | ページ ナビゲーションを表す名前空間。 「[ディープ リンクの設定](#deep-linking)」のメモを参照してください。 |
| people |Teams||
| 設定 || 非推奨。 `pages.config` に置き換えられました。|
| 共有 | Teams||
| tasks | | 非推奨。 `dialog` 機能に置き換えられました。 「[ダイアログ](#dialogs)」のメモを参照してください。|
| teamsCore | Teams | Teams 固有の機能を含む名前空間。|
| video | Teams||

#### <a name="app-permissions"></a>アプリのアクセス許可

ユーザーが [デバイスのアクセス許可](../../concepts/device-capabilities/device-capabilities-overview.md) (*位置情報* など) を付与する必要のあるアプリ機能は、Teams の外部で実行されるアプリではまだサポートされていません。 現在、Outlook または Office で実行しているときに [設定] またはアプリ ヘッダーでアプリのアクセス許可を確認する方法はありません。 Office または Outlook で実行されている Teams アプリが、デバイスのアクセス許可をトリガーする TeamsJS (または HTML5) API を呼び出すと、その API はエラーを生成し、ユーザーの同意を求めるシステム ダイアログを表示できません。

現在のガイダンスとして、エラーをキャッチするようにコードを変更してください。

* 機能を使用する前に、機能の [isSupported()](#differentiate-your-app-experience) を確認してください。 `media`、`meeting`、および `files` は *isSupported* 呼び出しをまだサポートしておらず、Teams の外部ではまだ機能しません。
* TeamsJS と HTML5 API を呼び出すときに、エラーをキャッチして処理します。

API がサポートされていないか、エラーを生成する場合、ロジックを追加して正常に機能させるか、回避策を提示します。 例として以下のようなものがあります。

* ユーザーにアプリの Web サイトに移動するように指示します。
* フローを完了するために Teams 内でアプリを使用するようにユーザーに指示します。
* 機能がまだ利用できないことをユーザーに通知します。

また、ベスト プラクティスは、アプリ マニフェストで、使用しているデバイスのアクセス許可のみが指定されているようにすることです。

#### <a name="deep-linking"></a>ディープ リンク

TeamsJS バージョン 2.0 より前は、すべてのディープ リンク シナリオは `shareDeepLink` (アプリの特定の部分 *へ* のリンクを生成するため) および `executeDeepLink` (アプリ *から*、またはアプリ *内* へのディープリンクに移動するため) を使用して処理されていました。 TeamsJS v.2.0 では、アプリ ホスト (Teams だけでなく Office と Outlook) 全体で一貫した方法でアプリ内のページ (およびサブページ) に移動するための新しい API (`navigateToApp`) が導入されています。 ディープ リンク シナリオの更新されたガイダンスを次に示します。

##### <a name="deep-links-into-your-app"></a>アプリへのディープ リンク

ユーザーが共有するためのコピー可能なリンクを生成して表示するには、`pages.shareDeepLink` (TeamsJS v.2.0 より前は *shareDeepLink* と呼ばれていました) を使用します。 クリックすると、(リンク パスで指定された) アプリケーション ホスト用にアプリがまだインストールされていない場合は、アプリのインストールを求めるメッセージがユーザーに表示されます。

##### <a name="navigation-within-your-app"></a>アプリ内の移動

新しい `pages.navigateToApp` API を使用して、ホスト アプリケーション内でアプリ内を移動します。

この API を使用することは、アプリで URL を作成したり、アプリケーション ホストごとに異なるディープ リンク形式を管理したりすることなく、ディープ リンクに移動するのと同じです (以前は、現在非推奨の *executeDeepLink* が使用されていました)。

##### <a name="deep-links-out-of-your-app"></a>アプリ外へのディープ リンク

アプリから現在のホストのさまざまな領域へのディープ リンクを生成するには、TeamsJS SDK が提供する厳密に型指定された API を使用します。 たとえば、*calendar* 機能を使用して、アプリからスケジュール設定ダイアログや予定表アイテムを開きます。

アプリから同じホストで実行中の他のアプリへのディープ リンクを生成するには、`pages.navigateToApp` を使用します。

その他の外部へのディープ リンク シナリオでは、`app.openLink` を使用できます。これは、現在 (TeamsJS v.2.0 以降で) 非推奨になった *executeDeepLink* API と同様の機能を提供します。

#### <a name="dialogs"></a>ダイアログ

Microsoft 365 開発者エコシステム全体の既存の概念との整合性を向上させるため、TeamsJS のバージョン 2.0 以降、[タスク モジュール](../../task-modules-and-cards/what-are-task-modules.md)の Teams プラットフォームの概念は *ダイアログ* という名前に変更されました。 そのため、`tasks` 名前空間は使用されなくなり、代わりに新しい `dialog` 名前空間が使用されます。

この新しいダイアログ機能は、HTML ベースのダイアログをサポートするための主要な機能 (`dialog`) と、ボットベースのダイアログ開発のためのサブ機能 (`dialog.bot`) に分けられます。

ダイアログ機能では、[アダプティブ カード ダイアログ](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)はまだサポートされていません。 アダプティブ カードベースのダイアログは、引き続き `tasks.startTask()` を使用して呼び出す必要があります。

現在、`dialog.open` 関数は HTMl ベースのダイアログを開くためにのみ機能し、新しく開いたダイアログにメッセージを渡す (`ChildAppWindow.postMessage`) ために使用できるコールバック関数 (`PostMessageChannel`) を返します。  `dialog.open` は (Promise ではなく) コールバックを返します。これは、コールバックではアプリの実行でダイアログの終了の待機を一時停止する必要がないためです (したがって、さまざまなユーザー操作パターンにおける柔軟性が向上します)。

## <a name="whats-new-in-teamsjs-version-20"></a>TeamsJS バージョン 2.0 の新機能

TeamsJS バージョン 1.x.x と v.2.0.0 以降には、2 つの大きな変更があります。

* [**コールバック関数が Promise オブジェクトを返すようになりました。**](#callbacks-converted-to-promises) TeamsJS v.1.12 のコールバック パラメーターを持つほとんどの関数が新しくなり、非同期操作とコードの読みやすさを向上させるために JavaScript [Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) オブジェクトを返すようになりました。

* [**API が *機能* に編成されました。**](#apis-organized-into-capabilities) 機能は、`authentication`、`dialog`、`chat`、および `calendar` など、同様の機能を提供する API の論理的なグループと考えることができます。 各名前空間は、個別の機能を表します。

> [!TIP]
> Microsoft Visual Studio Code の [Teams Toolkit 拡張機能](https://aka.ms/teams-toolkit)を使用すると、既存の Teams アプリの [TeamsJS v.2.0 更新プロセス](#updating-to-the-teams-client-sdk-v200)を簡略化できます。

### <a name="backwards-compatibility"></a>下位互換性

既存の Teams アプリから `@microsoft/teams-js@2.0.0` (またはそれ以降) の参照を開始すると、変更された API を呼び出すコードについて非推奨の警告が表示されます。

既存の Teams アプリが、TeamsJS v.2 API パターンを使用するようにアプリケーション コードを更新できるようになるまで、Teams で引き続き動作できるように、API 変換レイヤー (v.1 SDK を v.2 SDK から v.2 SDK API 呼び出しにマッピングする) が提供されています。

#### <a name="teams-only-apps"></a>Teams 専用アプリ

アプリを Teams でのみ実行する (Office と Outlook では実行しない) 場合でも、ベスト プラクティスは、可能な限り早く最新の TeamsJS (*v.2.0* 以降) の参照を開始して、最新の機能強化、新機能、およびサポート (Teams 専用アプリの場合でも) の恩恵を受けることです。 TeamsJS v.1.12 は引き続きサポートされますが、新機能や機能強化は追加されません。

これができるようになったら、次の手順は、この記事で説明されている変更を使用して[既存のアプリケーション コードを更新する](#2-update-sdk-references)ことです。 それまでの間、v.1 から v.2 の API への変換レイヤーが下位互換性を提供し、既存の Teams アプリが TeamsJS バージョン 2.0 で引き続き機能するようにします。

#### <a name="teams-apps-running-across-microsoft-365"></a>Microsoft 365 全体で実行されている Teams アプリ

既存の Teams アプリを Outlook および Office で実行できるようにするには、次のすべてが必要です。

1. TeamsJS バージョン 2.0 ( `@microsoft/teams-js@2.0`) 以降の依存関係、

2. この記事で説明されている必要な変更に従って[既存のアプリケーション コードを変更する](#2-update-sdk-references)、および

3. バージョン 1.13 以降に[アプリ マニフェストに更新する](#3-update-the-manifest-optional)。

詳細については、「[Teams アプリを Microsoft 365 全体に拡張する](../../m365-apps/overview.md)」を参照してください。

### <a name="callbacks-converted-to-promises"></a>コールバックの Promise への変換

以前にコールバック パラメーターを受け取った Teams API が更新され、JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) オブジェクトを返すようになりました。 これには、以下の API が含まれます。

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, app.openLink, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, chat.getChatMembers, conversations.openConversation, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.getConfig, pages.config.setConfig, pages.backStack.navigateBack, people.selectPeople, teams.fullTrust.getConfigSetting, teams.fullTrust.joinedTeams.getUserJoinedTeams
```

Promises を使用するために、コードがこれらの API のいずれかを呼び出す方法を更新する必要があります。 たとえば、コードが次のような Teams API を呼び出しているとします。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

コード:

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => { /* ... */ });
```

これを次のように更新する必要があります:

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context) => {
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

コード:

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context: microsoftTeams.Context) => {
  /* ... */
});
```

これを次のように更新する必要があります:

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
> [Teams Toolkit を使用して TeamsJS v.2.0 に更新する](#updating-to-the-teams-client-sdk-v200)と、更新プログラムにフラグが付けられ、クライアント コードに `TODO` コメントが含まれます。

### <a name="apis-organized-into-capabilities"></a>API の機能への編成

*機能* は、同様の機能を提供する API の (名前空間を介した) 論理グループです。 タブ アプリのホストとして、Microsoft Teams、Outlook、Office が考えられます。 ホストは、特定の機能内で定義されているすべての API をサポートしている場合、その機能をサポートします。 ホストが機能を部分的に実装することはできません。 機能は、*認証* や *ダイアログ* のように、機能ベースまたはコンテンツ ベースです。 *ページ* などのアプリケーションの種類や他のグループの機能もあります。

TeamsJS v.2.0 以降では、API は JavaScript 名前空間の関数として定義されます。この名前は、必要な機能と一致します。 たとえば、アプリが *ダイアログ* 機能をサポートするホストで実行されている場合、アプリは (名前空間で定義されている他のダイアログ関連の API に加えて) `dialog.open` などの API を安全に呼び出すことができます。 アプリがそのホストでサポートされていない API を呼び出そうとすると、API は例外を生成します。 アプリを実行している現在のホストが特定の機能をサポートしているかどうかを確認するには、その名前空間の [isSupported()](#differentiate-your-app-experience) 関数を呼び出します。

#### <a name="differentiate-your-app-experience"></a>アプリ エクスペリエンスを差別化する

その機能 (名前空間) で `isSupported()` 関数を呼び出して、特定の機能の実行時にホスト サポートを確認できます。 サポートされている場合は `true` が返され、サポートされていない場合は `false` が返されます。必要に応じて、アプリの動作を調整できます。 これにより、アプリは、サポートするホストの UI と機能を明らかにしながら、サポートしないホストで引き続き実行できます。

アプリが実行されているホストの名前は、Context インターフェイス (`app.Context.app.host.name`) の *hostName* プロパティとして公開されます。これは、実行時に `getContext` を呼び出すことで照会できます。 `{hostName}` [URL プレースホルダー値](./access-teams-context.md#get-context-by-inserting-url-placeholder-values)としても使用できます。 ベスト プラクティスは、*hostName* メカニズムを控えめに使用することです。

* *hostName* プロパティ値に基づいて、特定の機能がホストで使用できる、またはできないとは **考えないでください**。 代わりに、機能サポート (`isSupported`) を確認します。
* *hostName* を使用して API 呼び出しをゲート **しないでください**。 代わりに、機能サポート (`isSupported`) を確認します。
* *hostName* は、実行中のホストに基づいてアプリケーションのテーマを区別するために **使用します**。 たとえば、Teamsで実行する場合は Microsoft Teams の紫色を主なアクセント カラーとして使用し、Outlook で実行する場合は Outlook の青を使用できます。
* *hostName* は、実行中のホストに基づいてユーザーに表示されるメッセージを区別するために **使用します**。 たとえば、Office on the web で実行する場合は *[タスクを Office で管理する]* を表示し、Teams で実行する場合は *[Teams でタスクを管理する]* を表示します。

#### <a name="namespaces"></a>名前空間

TeamsJS v.2.0 以降、API は名前空間として *機能* に編成されます。 特に重要な新しい名前空間には、*app*、*pages*、*dialog*、*teamsCore* があります。

##### <a name="app-namespace"></a>*app* 名前空間

`app` 名前空間には、Teams、Office、Outlook 全体におけるアプリの全体的な使用に必要な最上位レベルの API が含まれています。 他のさまざまな TeamsJS 名前空間のすべての API は、TeamsJS v.2.0 の時点で `app` 名前空間に移動しました。

| 元の名前空間 `global (window)` | 新しい名前空間 `app` |
| - | - |
| `executeDeepLink` | `app.openLink` (名前の変更) |
| `initialize` | `app.initialize` |
| `getContext` | `app.getContext` |
| `registerOnThemeChangeHandler` | `app.registerOnThemeChangeHandler` |

| 元の名前空間 `appInitialization` | 新しい名前空間 `app` |
| - | - |
| `appInitialization.notifyAppLoaded` | `app.notifyAppLoaded` |
| `appInitialization.notifySuccess` | `app.notifySuccess` |
| `appInitialization.notifyFailure` | `app.notifyFailure` |
| `appInitialization.notifyExpectedFailure` | `app.notifyExpectedFailure` |
| `appInitialization.FailedReason` 列挙 | `app.FailedReason` |
| `appInitialization.ExpectedFailureReason` 列挙 | `app.ExpectedFailureReason` |
| `appInitialization.IFailedRequest` 列挙 | `app.IFailedRequest` |
| `appInitialization.IExpectedFailureRequest` 列挙 | `app.IExpectedFailureRequest` |

##### <a name="pages-namespace"></a>*pages* 名前空間

`pages` 名前空間には、Teams、Office、Outlook などのさまざまな Microsoft 365 ホスト内で Web ページを実行および移動するための機能が含まれています。 また、サブ名前空間として実装されるいくつかのサブ機能も含まれています。

| 元の名前空間 `global (window)` | 新しい名前空間 `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame` (名前の変更) |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFocusEnterHandler` | `pages.registerFocusEnterHandler`
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |
| `shareDeepLink` | `pages.shareDeepLink` |

| 元の名前空間 `settings` | 新しい名前空間 `pages`  |
| - | - |
| `settings.getSettings` | `pages.getConfig` (名前の変更)

###### <a name="pagestabs"></a>*pages.tabs*

| 元の名前空間 `global (window)` | 新しい名前空間 `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |

| 元の名前空間 `navigation` | 新しい名前空間 `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

###### <a name="pagesconfig"></a>*pages.config*

| 元の名前空間 `settings` | 新しい名前空間 `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig` (名前の変更)
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
| `registerChangeConfigHandler` | `pages.config.registerChangeConfigHandler` (名前の変更)

###### <a name="pagesbackstack"></a>*pages.backStack*

| 元の名前空間 `navigation` | 新しい名前空間 `pages.backStack`  |
| - | - |
| `navigation.navigateBack` | `pages.backStack.navigateBack`

| 元の名前空間 `global (window)` | 新しい名前空間 `pages.backStack`  |
| - | - |
| `registerBackButtonHandler` | `pages.backStack.registerBackButtonHandler`

###### <a name="pagesappbutton"></a>*pages.appButton*

| 元の名前空間 `global (window)` | 新しい名前空間 `pages.appButton`  |
| - | - |
| `registerAppButtonClickHandler` | `pages.appButton.onClick` (名前の変更)
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter` (名前の変更)
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave` (名前の変更)
| `FrameContext` インターフェイス | `pages.appButton.FrameInfo` (名前の変更)) |

##### <a name="dialog-namespace"></a>*dialog* 名前空間

TeamsJS の *tasks* 名前空間の名前が *dialog* に変更され、次の API の名前が変更されました。

| 元の名前空間 `tasks` | 新しい名前空間 `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open` (名前の変更) |
| `tasks.submitTasks` | `dialog.submit` (名前の変更) |
| `tasks.updateTasks` | `dialog.update.resize` (名前の変更) |
| `tasks.TaskModuleDimension` 列挙 | `dialog.DialogDimension` (名前の変更) |
| `tasks.TaskInfo` インターフェイス | `dialog.DialogInfo` (名前の変更) |

さらに、この機能は、HTML ベースのダイアログをサポートするための主要な機能 (`dialog`) と、ボットベースのダイアログのサブ機能 (`dialog.bot`) に分けられます。

##### <a name="teamscore-namespace"></a>*teamsCore* 名前空間

TeamsJS SDK を一般化して、Office や Outlook などの他の Microsoft 365 ホストを実行するために、Teams 固有の機能 (元々は *global* 名前空間内) が *teamsCore* 名前空間に移動しました。

| 元の名前空間 `global (window)` | 新しい名前空間 `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`

#### <a name="updates-to-the-context-interface"></a>*Context* インターフェイスの更新

Teams に加えて Outlook と Office で実行するときのスケーラビリティを向上させるため、`Context` インターフェイスは `app` 名前空間に移動し、同様のプロパティがグループ化されるように更新されました。

タブがホスト アプリケーションに応じてユーザー エクスペリエンスを区別できるようにするため、新しいプロパティ `app.Context.app.host.name` が追加されました。

[TeamsJS v.2.0 ソース](https://github.com/OfficeDev/microsoft-teams-library-js/blob/main/packages/teams-js/src/public/app.ts) (*app.ts* ファイル) で `transformLegacyContextToAppContext` 関数を確認することで、変更を視覚化することもできます。

| `Context` インターフェイスでの元の名前 | `app.Context` の新しい場所 |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *NOT IN TeamsJS v.2.0* |
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
|`userClickTime`| `app.Context.app.userClickTime`|
| `userFileOpenPreference` | `app.Context.app.userFileOpenPreference` |
| `userLicenseType`| `app.Context.user.licenseType` |
| `userObjectId` | `app.Context.user.id`|
| `userTeamRole` | `app.Context.team.userRole`|
| `userDisplayName` | `app.Context.user.displayName` |
| 該当なし | `app.Context.app.host.name`|

## <a name="updating-to-the-teams-client-sdk-v200"></a>Teams クライアント SDK v.2.0.0 への更新

Teams アプリで TeamsJS v.2.0 を使用するために更新する最も簡単な方法は、Visual Studio Code の [Teams Toolkit 拡張機能](https://aka.ms/teams-toolkit)を使用することです。 このセクションでは、これを行う手順について順を追って説明します。 コードを手動で更新する場合、「[コールバックの Promise への変換](#callbacks-converted-to-promises)」と「[API の機能への編成](#apis-organized-into-capabilities)」を参照して、必要な API の変更の詳細を確認してください。

### <a name="1-install-the-latest-teams-toolkit-visual-studio-code-extension"></a>1. 最新の Teams Toolkit Visual Studio Code 拡張機能をインストールする

*Visual Studio Code 拡張機能 Marketplace* で、**Teams Toolkit** を検索し、バージョン `2.10.0` 以降をインストールします。

### <a name="2-update-sdk-references"></a>2. SDK 参照を更新する

Outlook および Office で実行するには、アプリが [npm パッケージ](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0) `@microsoft/teams-js@2.0.0` (またはそれ以降) に依存している必要があります。 これらの手順を手動で実行する方法と、API の変更の詳細については、「[コールバックの Promise への変換](#callbacks-converted-to-promises)」と「[API の機能への編成](#apis-organized-into-capabilities)」に関する以下のセクションを参照してください。

1. [Teams Toolkit](https://aka.ms/teams-toolkit) `v.2.10.0` 以降があることを確認します
1. *コマンド パレット* を開きます: `Ctrl+Shift+P`
1. コマンド `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps` を実行します。

完了後、ユーティリティは TeamsJS v.2.0 (`@microsoft/teams-js@2.0.0` 以降) の依存関係を使用して `package.json` ファイルを更新します。ファイル `*.js/.ts` と `*.jsx/.tsx` が更新され、次が含まれるようになります。

> [!div class="checklist"]
>
> * TeamsJS v.2.0 への `package.json` 参照
> * TeamsJS v.2.0 の Import ステートメント
> * TeamsJS v.2.0 への[関数、列挙型、インターフェイス呼び出し](#apis-organized-into-capabilities)
> * `TODO` コメント リマインダーを使用して、 [コンテキスト](#updates-to-the-context-interface) インターフェイスの変更の影響を受ける可能性がある領域を確認する
> * [コールバック関数を Promise に変換する](#callbacks-converted-to-promises)ための `TODO` コメント リマインダー

> [!IMPORTANT]
> .html ファイル内のコードはアップグレード ツールではサポートされていないため、手動で変更する必要があります。

### <a name="3-update-the-manifest-optional"></a>3. マニフェストを更新する (省略可能)

Office および Outlook で実行するように Teams アプリを更新する場合、アプリ マニフェストをバージョン 1.13 以降に更新する必要もあります。 これは、Teams Toolkit で簡単に行うか、手動で行うことができます。

# <a name="teams-toolkit"></a>[Teams ツールキット](#tab/manifest-teams-toolkit)

1. *コマンド パレット* を開きます: `Ctrl+Shift+P`
1. **Teams: Upgrade Teams manifest to support Outlook and Office apps** コマンドを実行し、アプリ マニフェスト ファイルを選択します。 変更が行われます。

# <a name="manual-steps"></a>[手動の手順](#tab/manifest-manual)

Teams アプリ マニフェストを開き、`$schema` と `manifestVersion` を次の値で更新します。

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

Teams ツールキットを使用して個人用アプリを作成した場合は、それを使用してマニフェスト ファイルの変更を検証し、エラーを特定することもできます。 コマンド パレットを開いてTeams を`Ctrl+Shift+P`見つけます **。マニフェスト ファイル** を検証するか、Teams ツールキットの [配置] メニューからオプションを選択します (Visual Studio Code の左側にある Teams アイコンを探します)。

:::image type="content" source="../../m365-apps/images/toolkit-validate-manifest-file.png" alt-text="Teams ツールキット [配置] メニューの [マニフェスト ファイルの検証] オプション":::

## <a name="next-steps"></a>次のステップ

* [TeamsJS リファレンス](/javascript/api/overview/msteams-client)を使用して、Microsoft Teams JavaScript クライアント SDK の使用を開始します。
* TeamsJS の最新の更新プログラムについては、[変更ログ](https://github.com/OfficeDev/microsoft-teams-library-js/blob/main/packages/teams-js/CHANGELOG.md)を確認してください。
