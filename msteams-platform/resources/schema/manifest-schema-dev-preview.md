---
title: 開発者プレビュー マニフェスト スキーマ リファレンス
description: マニフェストでサポートされているMicrosoft Teamsのスキーマについて説明します。
ms.topic: reference
keywords: チーム マニフェスト スキーマ 開発者プレビュー
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: b52d52f96312dc2978844b07a0f7ebb1d817166d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566706"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a>Microsoft Teamsの開発者プレビュー マニフェスト スキーマ

> [!NOTE]
> プログラムと参加方法については、「 [開発者プレビュー](~/resources/dev-preview/developer-preview-intro.md) 」を参照してください。
> 開発者プレビューを使用していない場合は、このバージョンのマニフェストを使用しないでください。 [「参照: マニフェストの公開バージョンのMicrosoft Teams](~/resources/schema/manifest-schema.md)のマニフェスト スキーマ」を参照してください。

Microsoft Teams マニフェストは、アプリがMicrosoft Teams製品にどのように統合するかを示します。 マニフェストは、 でホストされているスキーマに準拠している必要があります [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) 。

利用可能な機能の詳細については[、「Microsoft Teamsのパブリック開発者向けプレビューの機能](~/resources/dev-preview/developer-preview-features.md)」を参照してください。

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

*オプションですが、推奨* &ndash; 糸

マニフェストの JSON スキーマを参照する https:// URL。

## <a name="manifestversion"></a>マニフェストバージョン

**必須** &ndash; 糸

このマニフェストが使用しているマニフェスト スキーマのバージョン。 "devPreview" にする必要があります。

## <a name="version"></a>version

**必須** &ndash; 糸

特定のアプリのバージョン。 マニフェスト内の何かを更新する場合は、バージョンもインクリメントする必要があります。 このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。 このアプリがストアに提出された場合、新しいマニフェストを再提出し、再検証する必要があります。 その後、このアプリのユーザーは、それが承認された後、数時間で自動的に新しい更新されたマニフェストを取得します。

アプリがアクセス許可を要求した場合、ユーザーはアップグレードを要求され、アプリに再び同意するように求められます。

このバージョンの文字列は [、semver](http://semver.org/) 標準 (MAJOR.マイナー。パッチ)。

## <a name="id"></a>id

**必須** &ndash; マイクロソフト アプリ ID

このアプリのマイクロソフトが生成した一意の識別子。 Microsoft Bot Frameworkを介してボットを登録した場合、またはタブの Web アプリが既に Microsoft にサインインしている場合は、ID が既に用意されている必要があります。 それ以外の場合は、 Microsoft アプリケーション登録ポータル ([マイ アプリケーション](https://apps.dev.microsoft.com)) で新しい ID を生成し、ここに入力し、 [ボットを追加](~/bots/how-to/create-a-bot-for-teams.md)するときに再利用する必要があります。

## <a name="packagename"></a>パッケージ名

**必須** &ndash; 糸

逆ドメイン表記で、このアプリの一意の識別子。たとえば、com.example.myapp を使用します。

## <a name="developer"></a>developer

**必須**

会社に関する情報を指定します。 AppSource (以前のOfficeストア) に送信されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`name`|32 文字|✔|開発者の表示名。|
|`websiteUrl`|2048 文字|✔|開発者の web サイトへの https:// URL。 このリンクをクリックすると、ユーザーは会社または製品固有のランディング ページに移動します。|
|`privacyUrl`|2048 文字|✔|開発者のプライバシー ポリシーの https:// URL。|
|`termsOfUseUrl`|2048 文字|✔|開発者の使用条件の https:// URL。|
|`mpnId`|10 文字|✔|**オプション** アプリを構築するパートナー組織を識別するマイクロソフト パートナー ネットワーク ID。|

## <a name="localizationinfo"></a>ローカリゼーション情報

**Optional**

既定の言語の指定と、追加の言語ファイルへのポインタを許可します。 [ローカライズ](~/concepts/build-and-test/apps-localization.md)を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`defaultLanguageTag`|4 文字|✔|この最上位のマニフェスト ファイル内の文字列の言語タグ。|

### <a name="localizationinfoadditionallanguages"></a>ローカリゼーション情報.追加言語

追加の言語翻訳を指定するオブジェクトの配列。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`languageTag`|4 文字|✔|指定されたファイル内の文字列の言語タグ。|
|`file`|4 文字|✔|翻訳された文字列を含む .json ファイルへの相対ファイル パス。|

## <a name="name"></a>name

**必須**

Teams エクスペリエンスのユーザーに表示される、アプリ エクスペリエンスの名前。 AppSource に送信されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。 の値 `short` は同 `full` じであってはなりません。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|30 文字|✔|アプリの短い表示名。|
|`full`|100 文字||アプリの完全名は、アプリの完全名が 30 文字を超える場合に使用されます。|

## <a name="description"></a>説明

**必須**

ユーザーにアプリを記述します。 AppSource に送信されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。

説明が自分のエクスペリエンスを正確に説明し、潜在顧客がエクスペリエンスの内容を理解するのに役立つ情報を提供するようにします。 また、外部アカウントが使用する必要がある場合は、完全な説明に注意する必要があります。 の値 `short` は同 `full` じであってはなりません。  短い説明は、長い説明の中で繰り返してはならず、他のアプリ名を含めてはいけません。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|80 文字|✔|スペースが限られている場合に使用するアプリ エクスペリエンスの簡単な説明。|
|`full`|4000 文字|✔|アプリの完全な説明。|

## <a name="icons"></a>アイコン

**必須**

Teams アプリ内で使用されるアイコン。 アイコン ファイルは、アップロード パッケージの一部として含める必要があります。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`outline`|2048 文字|✔|透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。|
|`color`|2048 文字|✔|フルカラーの 192x192 PNG アイコンへの相対ファイル パス。|

## <a name="accentcolor"></a>アクセントカラー

**必須** &ndash; 糸

アウトライン アイコンと共に、および背景として使用する色。

値は、たとえば '#' で始まる有効な HTML カラー コードである必要があります `#4464ee` 。

## <a name="configurabletabs"></a>構成可能なタブ

**Optional**

アプリエクスペリエンスにチーム チャネル タブ エクスペリエンスがあり、追加前に追加の構成が必要な場合に使用します。 構成可能なタブはチームスコープでのみサポートされ、現在はアプリごとに 1 つのタブのみがサポートされています。

オブジェクトは、 type のすべての要素を持つ配列です `object` 。 このブロックは、構成可能なチャネル タブ ソリューションを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|String|2048 文字|✔|タブの構成時に使用する https:// URL。|
|`canUpdateConfiguration`|Boolean|||タブの構成のインスタンスを作成後にユーザーが更新できるかどうかを示す値。 デフォルト： `true`|
|`scopes`|列挙型の配列|1|✔|現在、構成可能なタブは `team` 、 および スコープのみをサポート `groupchat` します。 |
|`sharePointPreviewImage`|String|2048||SharePointで使用するタブ プレビュー イメージへの相対ファイル パス。 サイズ 1024x768。 |
|`supportedSharePointHosts`|列挙型の配列|1||SharePointでタブを使用できるようにする方法を定義します。 オプションは `sharePointFullPage` 、 `sharePointWebPart` |

## <a name="statictabs"></a>静的タブ

**Optional**

ユーザーが手動で追加しなくても、既定で "固定" できるタブのセットを定義します。 スコープで宣言された静的タブ `personal` は、常にアプリの個人的なエクスペリエンスに固定されます。 スコープで宣言された静的タブ `team` は、現在サポートされていません。

オブジェクトは、型のすべての要素を持つ配列 (最大 16 個の要素) です `object` 。 このブロックは、静的タブ ソリューションを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`entityId`|String|64 文字|✔|タブが表示するエンティティの一意の識別子。|
|`name`|String|128 文字|✔|チャネル インターフェイスのタブの表示名。|
|`contentUrl`|String|2048 文字|✔|Teams キャンバスに表示されるエンティティ UI を指す https:// URL。|
|`websiteUrl`|String|2048 文字||ユーザーがブラウザーで表示することを選択した場合に指す https:// URL。|
|`scopes`|列挙型の配列|1|✔|現在、静的タブはスコープのみをサポート `personal` するため、個人用エクスペリエンスの一部としてのみプロビジョニングできます。|

## <a name="bots"></a>ボット

**Optional**

ボット ソリューションを、既定のコマンド プロパティなどのオプション情報と共に定義します。

オブジェクトは配列です (最大 1 つの要素のみ &mdash; 、現在、1 つのアプリに 1 つのボットしか許可されていません) 型のすべての要素を持つ `object` . このブロックは、ボット エクスペリエンスを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|String|64 文字|✔|Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 これは、 [全体的なアプリ ID](#id)と同じである可能性があります。|
|`needsChannelSelector`|Boolean|||ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。 デフォルト： `false`|
|`isNotificationOnly`|Boolean|||ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。 デフォルト： `false`|
|`supportsFiles`|Boolean|||パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。 デフォルト： `false`|
|`scopes`|列挙型の配列|3|✔|ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。 これらのオプションは非排他的です。|

### <a name="botscommandlists"></a>コマンドリスト

ボットがユーザーに推奨できるコマンドのリスト(オプション)。 オブジェクトは、型のすべての要素を持つ配列 (最大 2 つの要素) です `object` 。 詳細については [、「Bot メニュー](~/bots/how-to/create-a-bot-commands-menu.md)」を参照してください。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`items.scopes`|列挙型の配列|3|✔|コマンド リストが有効なスコープを指定します。 `team`、`personal`、`groupchat` の中から選択できます。|
|`items.commands`|オブジェクトの配列|10|✔|ボットがサポートするコマンドの配列:<br>`title`: ボットコマンド名(文字列、32)。<br>`description`: コマンド構文とその引数の簡単な説明または例 (文字列、128)。|

## <a name="connectors"></a>コネクタ

**Optional**

`connectors`ブロックは、アプリのOffice 365コネクタを定義します。

オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) `object` です。 このブロックは、コネクタを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|String|2048 文字|✔|コネクタの構成時に使用する https:// URL。|
|`connectorId`|String|64 文字|✔|コネクタ開発者ダッシュボード の ID と一致する [コネクタの](https://aka.ms/connectorsdashboard)一意の識別子。|
|`scopes`|列挙型の配列|1|✔|コネクタが、 のチャネルのコンテキストでのエクスペリエンスを提供 `team` するか、個々のユーザーに限定されたエクスペリエンス ( ) を提供するかを指定 `personal` します。 現在、スコープのみが `team` サポートされています。|

## <a name="composeextensions"></a>コン成拡張

**Optional**

アプリのメッセージング拡張機能を定義します。

> [!NOTE]
> 機能の名前は、2017 年 11 月に "拡張の構成" から "メッセージング拡張機能" に変更されましたが、マニフェスト名はそのまま残り、既存の拡張機能が機能し続けます。

オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) `object` です。 このブロックは、メッセージング拡張機能を提供するソリューションにのみ必要です。

|名前| 型 | 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|String|64|✔|Bot Framework に登録されているメッセージング拡張機能をサポートするボットの一意の Microsoft アプリ ID。 これは、 [全体的なアプリ ID](#id)と同じである可能性があります。|
|`canUpdateConfiguration`|Boolean|||メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。 既定値は `false` です。|
|`commands`|オブジェクトの配列|10|✔|メッセージング拡張機能がサポートするコマンドの配列|

### <a name="composeextensionscommands"></a>コンスタブスエクステンション.コマンド

メッセージング拡張機能では、1 つ以上のコマンドを宣言する必要があります。 各コマンドは、UI ベースのエントリ ポイントからの潜在的な操作としてMicrosoft Teamsに表示されます。 最大 10 個のコマンドがあります。

各コマンド項目は、次の構造を持つオブジェクトです。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|String|64 文字|✔|コマンドの ID。|
|`type`|String|64 文字||コマンドの種類。 または の 1 つ `query` `action` デフォルト： `query`|
|`title`|String|32 文字|✔|わかりやすいコマンド名。|
|`description`|String|128 文字||このコマンドの目的を示すためにユーザーに表示される説明。|
|`initialRun`|Boolean|||コマンドをパラメーターなしで最初に実行するかどうかを示すブール値。 デフォルト： `false`|
|`context`|文字列 (String) の配列|3||メッセージ拡張を呼び出すことができる場所を定義します。 、 、、を任意に組み合わせて `compose` `commandBox` `message` 使用できます。 既定値は `["compose", "commandBox"]` です|
|`fetchTask`|Boolean|||タスク モジュールを動的にフェッチするかどうかを示すブール値。|
|`taskInfo`|オブジェクト|||メッセージング拡張コマンドを使用する場合にプリロードするタスクモジュールを指定します。|
|`taskInfo.title`|String|64||初期ダイアログ タイトル。|
|`taskInfo.width`|String|||ダイアログ幅 - ピクセル単位の数値またはデフォルトのレイアウト ("大きい"、"中""、"小" など)|
|`taskInfo.height`|String|||ダイアログの高さ - ピクセル単位の数値または既定のレイアウト ("大きい"、"中""、"小" など)|
|`taskInfo.url`|String|||初期の Web ビュー URL。|
|`messageHandlers`|オブジェクトの配列|5||特定の条件が満たされた場合にアプリを呼び出すことを許可するハンドラーのリスト。 ドメインも に表示する必要があります `validDomains` 。|
|`messageHandlers.type`|String|||メッセージ ハンドラーの種類。 `"link"` である必要があります。|
|`messageHandlers.value.domains`|文字列 (String) の配列|||リンク メッセージ ハンドラーが登録できるドメインの配列。|
|`parameters`|オブジェクトの配列|5|✔|コマンドが受け取るパラメーターのリスト。 最小: 1;最大: 5|
|`parameter.name`|String|64 文字|✔|クライアントに表示されるパラメータの名前。 これはユーザー要求に含まれます。|
|`parameter.title`|String|32 文字|✔|パラメーターのわかりやすいタイトルです。|
|`parameter.description`|String|128 文字||このパラメーターの目的を説明するわかりやすい文字列。|
|`parameter.inputType`|String|128 文字||のタスク モジュールに表示されるコントロールの種類を定義 `fetchTask: true` します。 の一 `text` つ `textarea` 、 、 、 、 `number` 、 `date` 、 `time` `toggle` 、 `choiceset`|
|`parameter.choices`|オブジェクトの配列|10||の選択肢オプション `choiceset` です。 の場合にのみ `parameter.inputType` 使用 `choiceset` します。|
|`parameter.choices.title`|String|128||選択したタイトル。|
|`parameter.choices.value`|String|512||Value of the choice.|

## <a name="permissions"></a>permissions

**Optional**

`string`アプリが要求するアクセス許可を指定する配列で、エンド ユーザーに拡張機能の実行方法を知ることができます。 次のオプションは非排他的です。

* `identity`&emsp;ユーザー ID 情報が必要です。
* `messageTeamMembers`&emsp;チーム メンバーにダイレクト メッセージを送信する権限が必要です。

アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは更新されたアプリを初めて実行するときに同意プロセスを繰り返します。

## <a name="devicepermissions"></a>デバイスアクセス許可

**オプション** 文字列の配列

アプリがアクセスを要求できるユーザーのデバイスのネイティブ機能を指定します。 オプションは、次のとおりです。

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>有効なドメイン

**省略可能** な ( **省略可能) (省略可能な** 場合は必須)

アプリがコンテンツを読み込むと想定している有効なドメインのリスト。 ドメインの一覧には、 などのワイルドカードを含めることができます `*.example.com` 。 これは、ドメインの 1 つのセグメントと完全に一致します。一致させる必要がある場合は `a.b.example.com` `*.*.example.com` 、 を使用します。 タブ構成またはコンテンツ UI がタブ構成の使用以外のドメインに移動する必要がある場合は、ここでそのドメインを指定する必要があります。

ただし、アプリでサポートする ID プロバイダーのドメインを含める必要 **はありません** 。 たとえば、Google ID を使用して認証するには、accounts.google.com にリダイレクトする必要がありますが、accounts.google.com を に含めるべきではありません `validDomains[]` 。

> [!IMPORTANT]
> 直接またはワイルドカードを使用して、コントロールの外側にあるドメインを追加しないでください。 たとえば、 `yourapp.onmicrosoft.com` 有効ですが、 `*.onmicrosoft.com` 無効です。

オブジェクトは、 type のすべての要素を持つ配列です `string` 。

## <a name="webapplicationinfo"></a>アプリケーション情報

**Optional**

ユーザーが AAD アプリにシームレスにサインインできるように、AAD アプリ ID とGraph情報を指定します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|String|36 文字|✔|アプリの AAD アプリケーション ID。 この ID は GUID である必要があります。|
|`resource`|String|2048 文字|✔|SSO の認証トークンを取得するためのアプリのリソース URL。|

## <a name="configurableproperties"></a>構成可能なプロパティ

**オプション** - 配列

`configurableProperties`このブロックは、管理者がカスタマイズできるアプリのプロパティTeams定義します。 詳細については、「 [Microsoft Teams でアプリをカスタマイズする](/MicrosoftTeams/customize-apps)」を参照してください。

> [!NOTE]
> 最低 1 つのプロパティを定義する必要があります。 このブロックには最大 9 つのプロパティを定義できます。
> ベスト プラクティスとして、アプリのユーザーとユーザーがアプリをカスタマイズするときに従うカスタマイズ ガイドラインを提供する必要があります。 

次のプロパティを定義できます。
* `name`: 管理者がアプリの表示名を変更できるようにします。
* `shortDescription`: 管理者がアプリの簡単な説明を変更できるようにします。
* `longDescription`: 管理者がアプリの詳細な説明を変更できるようにします。
* `smallImageUrl`: マニフェストの `outline` `icons` ブロック内のプロパティです。
* `largeImageUrl`: マニフェストの `color` `icons` ブロック内のプロパティです。
* `accentColor`: アウトライン アイコンの背景と組み合わせて使用する色です。
* `websiteUrl`: 開発者のウェブサイトへの https:// URLです。
* `privacyUrl`: 開発者のプライバシー ポリシーへの https:// URL です。
* `termsOfUseUrl`: 開発者の利用規約の https:// URL です。

## <a name="defaultinstallscope"></a>デフォルトインストールスコープ

**省略可能** - 文字列

既定でこのアプリに対して定義されているインストール スコープを指定します。 定義されたスコープは、ユーザーがアプリを追加しようとしたときにボタンに表示されるオプションになります。 オプションは、次のとおりです。
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>分類の機能

**オプション** - オブジェクト

グループのインストール スコープが選択されると、ユーザーがアプリをインストールするときに既定の機能が定義されます。 オプションは、次のとおりです。
* `team`
* `groupchat`
* `meetings`
 
|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`team`|string|||選択したインストールスコープが `team` の場合、このフィールドは使用可能なデフォルトの機能を指定します。 オプション : `tab` 、 `bot` 、 、 、 `connector`|
|`groupchat`|string|||選択したインストールスコープが `groupchat` の場合、このフィールドは使用可能なデフォルトの機能を指定します。 オプション : `tab` 、 `bot` 、 、 、 `connector`|
|`meetings`|string|||選択したインストールスコープが `meetings` の場合、このフィールドは使用可能なデフォルトの機能を指定します。 オプション : `tab` 、 `bot` 、 、 、 `connector`|

