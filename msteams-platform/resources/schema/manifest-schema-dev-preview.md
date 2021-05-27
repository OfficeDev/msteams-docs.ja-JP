---
title: Developer Preview マニフェスト スキーマ参照
description: マニフェストでサポートされているスキーマについて説明Microsoft Teams
ms.topic: reference
keywords: teams マニフェスト スキーマ Developer Preview
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: a5c75046b950484a897fa2720444899c4817989c
ms.sourcegitcommit: 25c02757fe207cdff916ba63aa215f88e24e1d6f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2021
ms.locfileid: "52667419"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a>開発者プレビュー マニフェスト スキーマ (Microsoft Teams

> [!NOTE]
> プログラムの詳細と参加方法については、「Developer Preview」 を [参照してください](~/resources/dev-preview/developer-preview-intro.md)。
> 開発者プレビューを使用していない場合は、このバージョンのマニフェストを使用する必要があります。 マニフェスト[のパブリック バージョンについては、「リファレンス: Microsoft Teams](~/resources/schema/manifest-schema.md)マニフェスト スキーマ」を参照してください。

このMicrosoft Teamsマニフェストは、アプリが製品に統合する方法Microsoft Teamsします。 マニフェストは、 でホストされるスキーマに準拠している必要があります [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) 。

利用可能な機能の詳細については、「パブリック サイトの機能」を参照Developer Preview[を参照Microsoft Teams。](~/resources/dev-preview/developer-preview-features.md)

## <a name="sample-full-manifest"></a>完全なマニフェストのサンプル

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "devPreview",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "devicePermissions" : [ "geolocation", "media" ],
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "localizationInfo": {
    "defaultLanguageTag": "es-es",
    "additionalLanguages": [
      {
        "languageTag": "en-us",
        "file": "en-us.json"
      }
    ]
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters"
  },
  "description": {
    "short": "Short description of your app",
    "full": "Full description of your app"
  },
  "icons": {
    "outline": "%FILENAME-32x32px%",
    "color": "%FILENAME-192x192px"
  },
  "accentColor": "%HEX-COLOR%",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content?host=msteams",
      "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
      "websiteUrl": "https://contoso.com/content",
      "scopes": [ "personal" ]
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
  "connectors": [
    {
      "connectorId": "GUID-FROM-CONNECTOR-DEV-PORTAL%",
      "configurationUrl": "https://contoso.com/teamsconnector/configure",
      "scopes": [ "team"]
    }
  ],
  "composeExtensions": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "type" : "search",
          "context" : ["compose", "commandBox"],
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "description": "Enter the keywords to search for"
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "type" : "action",
          "fetchTask" : true,
          "context" : ["message"],
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType" : "text"
            }
          ]
        },
        {
          "id": "exampleMessageHandler",
          "title": "Message Handler",
          "description": "Domains that will create a preview when pasted into the compose box",
          "messageHandlers": [
            {
              "type" : "link",
              "value" : {
                "domains" : [
                  "mysite.someplace.com",
                  "othersite.someplace.com"
                ]
              }
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers",
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ],
  "webApplicationInfo": {
    "id": "AAD App ID",
    "resource": "Resource URL for acquiring auth token for SSO",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelSettings.Read.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "ChannelMessage.Read.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group",
      "Member.ReadWrite.Group",
      "Owner.ReadWrite.Group"
    ],
  },
   "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "websiteUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ],
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  }
}
```

スキーマは、次のプロパティを定義します。

## <a name="schema"></a>$schema

*省略可能ですが、推奨* &ndash; 文字列

マニフェスト https:// JSON スキーマを参照する URL を指定します。

## <a name="manifestversion"></a>manifestVersion

**必須** &ndash; 文字列

このマニフェストが使用しているマニフェスト スキーマのバージョン。 "devPreview" である必要があります。

## <a name="version"></a>version

**必須** &ndash; 文字列

特定のアプリのバージョン。 マニフェストで何かを更新する場合は、バージョンも増分する必要があります。 このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。 このアプリがストアに送信された場合、新しいマニフェストを再送信して再検証する必要があります。 次に、このアプリのユーザーは、承認された後、数時間で新しい更新されたマニフェストを自動的に取得します。

アプリがアクセス許可の変更を要求した場合、ユーザーはアプリのアップグレードと再同意を求めるメッセージが表示されます。

このバージョンの文字列は [、semver](http://semver.org/) 標準 (MAJOR) に従う必要があります。MINOR。PATCH)。

## <a name="id"></a>id

**必須** &ndash; Microsoft アプリ ID

このアプリの Microsoft が生成した一意の識別子。 ボットを Microsoft Bot Framework 経由で登録している場合、またはタブの Web アプリが既に Microsoft にサインインしている場合は、既に ID を持っている必要があります。ここで入力する必要があります。 それ以外の場合は、Microsoft アプリケーション登録ポータル[(My Applications)](https://apps.dev.microsoft.com)で新しい ID を生成し、ここに入力し、ボットを追加するときに再利用 [する必要があります](~/bots/how-to/create-a-bot-for-teams.md)。

## <a name="packagename"></a>packageName

**必須** &ndash; 文字列

逆ドメイン表記でこのアプリの一意の識別子。たとえば、com.example.myapp などです。

## <a name="developer"></a>developer

**必須**

会社に関する情報を指定します。 AppSource に送信されたアプリ (以前Officeストア) の場合、これらの値は AppSource エントリの情報と一致する必要があります。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`name`|32 文字|✔|開発者の表示名。|
|`websiteUrl`|2048 文字|✔|開発者 https:// WEB サイトの URL を指定します。 このリンクは、ユーザーを会社または製品固有のランディング ページに移動する必要があります。|
|`privacyUrl`|2048 文字|✔|開発者 https:// のプライバシー ポリシーの URL を指定します。|
|`termsOfUseUrl`|2048 文字|✔|開発者 https:// の使用条件の URL を指定します。|
|`mpnId`|10 文字|✔|**省略可能** アプリを構築するパートナー組織を識別する Microsoft パートナー ネットワーク ID。|

## <a name="localizationinfo"></a>localizationInfo

**Optional**

既定の言語の指定と、追加の言語ファイルへのポインターを許可します。 「ローカライズ」 [を参照してください](~/concepts/build-and-test/apps-localization.md)。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`defaultLanguageTag`|4 文字|✔|このトップ レベルのマニフェスト ファイル内の文字列の言語タグ。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

追加の言語変換を指定するオブジェクトの配列。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`languageTag`|4 文字|✔|指定されたファイル内の文字列の言語タグ。|
|`file`|4 文字|✔|翻訳された文字列を含む .json ファイルへの相対ファイル パス。|

## <a name="name"></a>name

**必須**

アプリ エクスペリエンスのユーザーに表示されるアプリ エクスペリエンスのTeamsします。 AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。 の値 `short` と `full` 同じ値にしない必要があります。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|30 文字|✔|アプリの短い表示名。|
|`full`|100 文字||完全なアプリ名が 30 文字を超える場合に使用されるアプリの完全な名前。|

## <a name="description"></a>説明

**必須**

アプリをユーザーに説明します。 AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。

説明がエクスペリエンスを正確に説明し、潜在的な顧客がエクスペリエンスの内容を理解するのに役立つ情報を提供します。 また、外部アカウントの使用が必要な場合は、完全な説明に注意してください。 の値 `short` と `full` 同じ値にしない必要があります。  短い説明は、長い説明の中で繰り返し実行し、他のアプリ名を含めずに行う必要があります。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|80 文字|✔|スペースが制限されている場合に使用されるアプリ エクスペリエンスの簡単な説明。|
|`full`|4000 文字|✔|アプリの完全な説明。|

## <a name="icons"></a>アイコン

**必須**

アプリ内で使用Teamsアイコン。 アイコン ファイルは、アップロード パッケージの一部として含める必要があります。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`outline`|2048 文字|✔|透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。|
|`color`|2048 文字|✔|フル カラーの 192x192 PNG アイコンへの相対ファイル パス。|

## <a name="accentcolor"></a>accentColor

**必須** &ndash; 文字列

アウトライン アイコンと組み合わせて、背景として使用する色。

値は、'#' で始まる有効な HTML カラー コードである必要があります `#4464ee` 。

## <a name="configurabletabs"></a>configurableTabs

**Optional**

アプリ エクスペリエンスに、追加する前に追加の構成が必要なチーム チャネル タブ エクスペリエンスがある場合に使用します。 構成可能なタブは teams スコープでのみサポートされ、現在はアプリごとに 1 つのタブしかサポートされていません。

オブジェクトは、型のすべての要素を持つ配列です `object` 。 このブロックは、構成可能なチャネル タブ ソリューションを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|String|2048 文字|✔|タブ https:// する際に使用する URL を指定します。|
|`canUpdateConfiguration`|Boolean|||作成後に、タブの構成のインスタンスをユーザーが更新できるかどうかを示す値。 既定値: `true`|
|`scopes`|列挙型の配列|1|✔|現在、構成可能なタブは、スコープ `team` とスコープ `groupchat` のみをサポートしています。 |
|`sharePointPreviewImage`|String|2048||タブ プレビュー イメージへの相対ファイル パスを使用して、SharePoint。 サイズは 1024x768 です。 |
|`supportedSharePointHosts`|列挙型の配列|1||タブをタブで使用する方法を定義SharePoint。 オプションは `sharePointFullPage` 次のとおりです。 `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Optional**

ユーザーが手動で追加せずに、既定で "ピン留め" できるタブのセットを定義します。 スコープ内で宣言された静的タブ `personal` は、常にアプリの個人用エクスペリエンスにピン留めされます。 スコープで宣言されている静的タブ `team` は現在サポートされていません。

staticTabs ブロックではなく、アダプティブ カードを使用してタブ `contentBotId` `contentUrl` **をレンダリング** します。

オブジェクトは、型のすべての要素を持つ配列 (最大 16 要素) です `object` 。 このブロックは、静的タブ ソリューションを提供するソリューションにのみ必要です。


|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`entityId`|String|64 文字|✔|タブが表示されるエンティティの一意の識別子。|
|`name`|String|128 文字|✔|チャネル インターフェイスのタブの表示名。|
|`contentUrl`|String|2048 文字|✔|この https:// キャンバスに表示するエンティティ UI を示すTeamsします。|
|`contentBotId`|   | | | ボット Microsoft Teamsで指定されたアプリ ID を指定します。 |
|`websiteUrl`|String|2048 文字||ユーザー https:// ブラウザーで表示することを選択した場合に示す URL を指定します。|
|`scopes`|列挙型の配列|1|✔|現在、静的タブはスコープのみをサポートしています。つまり、個人用エクスペリエンスの一部としてのみ `personal` プロビジョニングできます。|

## <a name="bots"></a>bots

**Optional**

既定のコマンド プロパティなどのオプションの情報と共に、ボット ソリューションを定義します。

オブジェクトは、型のすべての要素を持つ配列 (現在、1 つのボットにつき 1 つのボットしか許可されていない &mdash; 最大 1 つの要素) です `object` 。 このブロックは、ボット エクスペリエンスを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|String|64 文字|✔|Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 これは、アプリ全体の ID と同じ [可能性があります](#id)。|
|`needsChannelSelector`|Boolean|||ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。 既定値: `false`|
|`isNotificationOnly`|Boolean|||ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。 既定値: `false`|
|`supportsFiles`|Boolean|||パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。 既定値: `false`|
|`scopes`|列挙型の配列|3|✔|ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。 これらのオプションは非排他的です。|

### <a name="botscommandlists"></a>bots.commandLists

ボットがユーザーに推奨できるコマンドのオプションの一覧。 オブジェクトは、型のすべての要素を持つ配列 (最大 2 つの要素) です。ボットがサポートするスコープごとに個別のコマンド リストを `object` 定義する必要があります。 詳細については、「Bot メニュー [」を参照してください](~/bots/how-to/create-a-bot-commands-menu.md)。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`items.scopes`|列挙型の配列|3|✔|コマンド リストが有効なスコープを指定します。 `team`、`personal`、`groupchat` の中から選択できます。|
|`items.commands`|オブジェクトの配列|10|✔|ボットがサポートするコマンドの配列:<br>`title`: bot コマンド名 (文字列、32)。<br>`description`: コマンド構文とその引数の簡単な説明または例 (文字列、128)。|

## <a name="connectors"></a>コネクタ

**Optional**

ブロック `connectors` は、アプリOffice 365コネクタを定義します。

オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) です `object` 。 このブロックは、Connector を提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|String|2048 文字|✔|コネクタ https:// する際に使用する URL を指定します。|
|`connectorId`|String|64 文字|✔|コネクタ開発者ダッシュボードの ID に一致するコネクタの一 [意の識別子](https://aka.ms/connectorsdashboard)です。|
|`scopes`|列挙型の配列|1|✔|Connector がチャネルのコンテキストでエクスペリエンスを提供するかどうか、または個々のユーザー () にスコープを設定したエクスペリエンスを提供するかどうかを `team` 指定します `personal` 。 現在、スコープ `team` だけがサポートされています。|

## <a name="composeextensions"></a>composeExtensions

**Optional**

アプリのメッセージング拡張機能を定義します。

> [!NOTE]
> 機能の名前は、2017 年 11 月に "作成拡張機能" から "メッセージング拡張機能" に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は変わりません。

オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) です `object` 。 このブロックは、メッセージング拡張機能を提供するソリューションにのみ必要です。

|名前| 型 | 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|String|64|✔|ボット フレームワークに登録されているメッセージング拡張機能をバックするボットの一意の Microsoft アプリ ID。 これは、アプリ全体の ID と同じ [可能性があります](#id)。|
|`canUpdateConfiguration`|Boolean|||メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。 既定値は `false` です。|
|`commands`|オブジェクトの配列|10|✔|メッセージング拡張機能がサポートするコマンドの配列|

### <a name="composeextensionscommands"></a>composeExtensions.commands

メッセージング拡張機能は、1 つ以上のコマンドを宣言する必要があります。 各コマンドは、MICROSOFT TEAMSエントリ ポイントからの潜在的な対話として表示されます。 最大 10 のコマンドがあります。

各コマンド 項目は、次の構造を持つオブジェクトです。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|String|64 文字|✔|コマンドの ID。|
|`type`|String|64 文字||コマンドの種類。 または `query` の 1 `action` つ。 既定値: `query`|
|`title`|String|32 文字|✔|ユーザーフレンドリーなコマンド名。|
|`description`|String|128 文字||このコマンドの目的を示すためにユーザーに表示される説明。|
|`initialRun`|Boolean|||パラメーターを指定してコマンドを最初に実行するかどうかを示すブール値。 既定値: `false`|
|`context`|文字列 (String) の配列|3||メッセージ拡張機能の呼び出し先を定義します。 `compose`、 の任意の `commandBox` 組み合 `message` わせ。 既定値は `["compose", "commandBox"]` です|
|`fetchTask`|Boolean|||タスク モジュールを動的にフェッチする必要があるかどうかを示すブール値。|
|`taskInfo`|オブジェクト|||メッセージング拡張機能コマンドを使用するときにプリロードするタスク モジュールを指定します。|
|`taskInfo.title`|String|64||最初のダイアログ タイトル。|
|`taskInfo.width`|String|||ダイアログの幅 - ピクセル単位の数値または既定のレイアウト ('large'、'medium'、または 'small' など)。|
|`taskInfo.height`|String|||ダイアログの高さ - ピクセル単位の数値、または 'large'、'medium'、または 'small' などの既定のレイアウト。|
|`taskInfo.url`|String|||初期 Webview URL。|
|`messageHandlers`|オブジェクトの配列|5||特定の条件が満たされた場合にアプリを呼び出すことができるハンドラーの一覧。 ドメインもに一覧表示する必要があります `validDomains` 。|
|`messageHandlers.type`|String|||メッセージ ハンドラーの種類。 `"link"` である必要があります。|
|`messageHandlers.value.domains`|文字列 (String) の配列|||リンク メッセージ ハンドラーが登録できるドメインの配列。|
|`parameters`|オブジェクトの配列|5|✔|コマンドが受け取るパラメーターの一覧。 最小: 1;最大: 5|
|`parameter.name`|String|64 文字|✔|クライアントに表示されるパラメーターの名前。 これは、ユーザー要求に含まれます。|
|`parameter.title`|String|32 文字|✔|パラメーターのユーザーフレンドリーなタイトル。|
|`parameter.description`|String|128 文字||このパラメーターの目的を説明するユーザーフレンドリーな文字列。|
|`parameter.inputType`|String|128 文字||タスク モジュールに表示されるコントロールの種類を定義します `fetchTask: true` 。 、 `text` `textarea` 、 、 、 、 の `number` `date` `time` `toggle` 1 `choiceset` つ。|
|`parameter.choices`|オブジェクトの配列|10||の選択肢 `choiceset` オプションです。 の場合にのみ `parameter.inputType` 使用します `choiceset` 。|
|`parameter.choices.title`|String|128||選択したタイトル。|
|`parameter.choices.value`|String|512||Value of the choice.|

## <a name="permissions"></a>permissions

**Optional**

アプリが要求するアクセス許可を指定する配列で、エンド ユーザーは拡張機能の実行 `string` 方法を知る必要があります。 次のオプションは、非排他的です。

* `identity`&emsp;ユーザー ID 情報が必要です。
* `messageTeamMembers`&emsp;チーム メンバーに直接メッセージを送信するためのアクセス許可が必要です。

アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは更新されたアプリを初めて実行するときに同意プロセスを繰り返します。

## <a name="devicepermissions"></a>devicePermissions

**省略可能** 文字列の配列

アプリがアクセスを要求できるユーザーのデバイス上のネイティブ機能を指定します。 オプションは、次のとおりです。

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**省略** 可能です ( **必須の場合** は除く)

アプリがコンテンツの読み込みを期待する有効なドメインの一覧。 ドメインの一覧には、ワイルドカードを含め、たとえば、 を含めできます `*.example.com` 。 これは、ドメインの 1 つのセグメントと完全に一致します。一致する必要がある場合は、 `a.b.example.com` を使用します `*.*.example.com` 。 タブ構成またはコンテンツ UI で、タブ構成に使用するドメイン以外のドメインに移動する必要がある場合は、ここでそのドメインを指定する必要があります。

ただし、 **サポート** する ID プロバイダーのドメインをアプリに含める必要はありません。 たとえば、Google ID を使用して認証するには、Accounts.google.com にリダイレクトする必要がありますが、accounts.google.com に含める必要はありません `validDomains[]` 。

> [!IMPORTANT]
> 直接またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しません。 たとえば、有効 `yourapp.onmicrosoft.com` ですが、 `*.onmicrosoft.com` 無効です。

オブジェクトは、型のすべての要素を持つ配列です `string` 。

## <a name="webapplicationinfo"></a>webApplicationInfo

**Optional**

ユーザーが AAD アプリにシームレスにサインインGraphに役立つ AAD アプリ ID とユーザー情報を指定します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|String|36 文字|✔|アプリの AAD アプリケーション ID。 この ID は GUID である必要があります。|
|`resource`|String|2048 文字|✔|SSO の認証トークンを取得するためのアプリのリソース URL。|
|`applicationPermissions`|配列|最大 100 アイテム|✔|アプリケーションのリソースのアクセス許可。|

## <a name="configurableproperties"></a>configurableProperties

**オプション** - 配列

この `configurableProperties` ブロックは、管理者がカスタマイズできるアプリTeams定義します。 詳細については、「アプリのカスタマイズ[」を参照Microsoft Teams。](/MicrosoftTeams/customize-apps)

> [!NOTE]
> 少なくとも 1 つのプロパティを定義する必要があります。 このブロックでは、最大 9 つのプロパティを定義できます。
> ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。 

次のプロパティを定義できます。
* `name`: 管理者がアプリの表示名を変更できます。
* `shortDescription`: 管理者がアプリの簡単な説明を変更できます。
* `longDescription`: 管理者がアプリの詳細な説明を変更できます。
* `smallImageUrl`: マニフェストの `outline` ブロック内 `icons` のプロパティです。
* `largeImageUrl`: マニフェストの `color` ブロック内 `icons` のプロパティです。
* `accentColor`: アウトライン アイコンと組み合わせて、背景として使用する色です。
* `websiteUrl`: 開発者の https:// の URL です。
* `privacyUrl`: 開発者の https:// の URL です。
* `termsOfUseUrl`: 開発者の https:// の URL です。

## <a name="defaultinstallscope"></a>defaultInstallScope

**省略** 可能 - 文字列

既定では、このアプリに対して定義されているインストール スコープを指定します。 定義されたスコープは、ユーザーがアプリを追加しようとするときにボタンに表示されるオプションになります。 オプションは、次のとおりです。
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

**省略可能** - オブジェクト

グループ インストール スコープを選択すると、ユーザーがアプリをインストールするときに既定の機能が定義されます。 オプションは、次のとおりです。
* `team`
* `groupchat`
* `meetings`
 
|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`team`|string|||選択したインストール スコープが次の場合 `team` 、このフィールドは使用可能な既定の機能を指定します。 オプション: `tab` `bot` 、、または `connector` 。|
|`groupchat`|string|||選択したインストール スコープが次の場合 `groupchat` 、このフィールドは使用可能な既定の機能を指定します。 オプション: `tab` `bot` 、、または `connector` 。|
|`meetings`|string|||選択したインストール スコープが次の場合 `meetings` 、このフィールドは使用可能な既定の機能を指定します。 オプション: `tab` `bot` 、、または `connector` 。|

