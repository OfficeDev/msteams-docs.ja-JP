---
title: マニフェスト スキーマ リファレンス
description: Microsoft Teams のマニフェスト スキーマについて説明します。
keywords: teams マニフェスト スキーマ
author: laujan
ms.author: lajanuar
ms.openlocfilehash: 17626df3aa4b076190413c67d9a0ecd7cd2eed31
ms.sourcegitcommit: 4275a502f9f7742da2900c79e19551e481c9e48a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797053"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>リファレンス: Microsoft Teams のマニフェスト スキーマ

Microsoft Teams マニフェストは、アプリが Microsoft Teams 製品に統合される方法について説明します。 マニフェストは、ホストされているスキーマに準拠している必要があります [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) 。 以前のバージョンの 1.0-1.4 もサポートされています (URL で "v1.x" を使用)。

次のスキーマ サンプルは、すべての拡張オプションを示しています。

## <a name="sample-full-manifest"></a>完全なマニフェストのサンプル

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.8",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "localizationInfo": {
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
        "file": "en-us.json"
      }
    ]
  },
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters (<=100 chars)"
  },
  "description": {
    "short": "Short description of your app (<= 80 chars)",
    "full": "Full description of your app (<= 4000 chars)"
  },
  "icons": {
    "outline": "A relative path to a transparent .png icon — 32px X 32px",
    "color": "A relative path to a full color .png icon — 192px X 192px"
  },
  "accentColor": "A valid HTML color code.",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "scopes": [
        "team",
        "groupchat"
      ],
      "canUpdateConfiguration": true,
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
      ],
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": [
         "sharePointFullPage",
         "sharePointWebPart"
      ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "context":[
        "personalTab",
        "channelTab"
        ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser)",
       "searchUrl":  "https://contoso.com/content (displayed in web browser)"
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "scopes": [
        "team",
        "personal",
        "groupchat"
      ],
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "supportsFiles": true,
      "supportsCalling": false,
      "supportsVideo": true,
      "commandLists": [
        {
          "scopes": [
            "team",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command 2",
              "description": "Description of Command 2"
            }
          ]
        },
        {
          "scopes": [
            "personal",
            "groupchat"
          ],
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
      "scopes": [
        "team"
      ],
      "configurationUrl": "https://contoso.com/teamsconnector/configure"
    }
  ],
  "composeExtensions": [
    {
      "canUpdateConfiguration": true,
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "type": "query",
          "context": [
            "compose",
            "commandBox"
          ],
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "fetchTask": false,
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "inputType": "text",
              "description": "Enter the keywords to search for",
              "value": "Initial value for the parameter",
              "choices": [
                {
                  "title": "Title of the choice",
                  "value": "Value of the choice"
                }
              ]
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "type": "action",
          "context": [
            "message"
          ],
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "fetchTask": true,
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType": "text"
            }
          ]
        }
      ],
      "taskInfo": {
        "title": "Initial dialog title",
        "width": "Dialog width",
        "height": "Dialog height",
        "url": "Initial webview URL"
      },
      "messageHandlers": [
        {
          "type": "link",
          "value": {
            "domains": [
              "mysite.someplace.com",
              "othersite.someplace.com"
            ]
          }
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "devicePermissions": [
    "geolocation",
    "media",
    "notifications",
    "midi",
    "openExternal"
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
  "showLoadingIndicator": false,
  "isFullScreen": false,
  "activities": {
    "activityTypes": [
      {
        "type": "taskCreated",
        "description": "Task created activity",
        "templateText": "<team member> created task <taskId> for you"
      },
      {
        "type": "userMention",
        "description": "Personal mention activity",
        "templateText": "<team member> mentioned you"
      }
    ]
  }
}
```

スキーマは、次のプロパティを定義します。

## <a name="schema"></a>$schema

*省略可能、ただし推奨* — 文字列

マニフェストhttps:// JSON スキーマを参照する URL を指定します。

## <a name="manifestversion"></a>manifestVersion

**必須** — string

このマニフェストが使用しているマニフェスト スキーマのバージョン。 "1.7" である必要があります。

## <a name="version"></a>バージョン

**必須** — string

特定のアプリのバージョン。 マニフェストで何かを更新する場合は、バージョンもインクリメントする必要があります。 このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。 このアプリがストアに提出された場合、新しいマニフェストを再送信して再検証する必要があります。 その後、このアプリのユーザーは、承認された数時間後に新しい更新されたマニフェストを自動的に取得します。

アプリがアクセス許可の変更を要求した場合、ユーザーはアプリのアップグレードと再同意を求めるメッセージが表示されます。

このバージョン文字列は [、semver](http://semver.org/) 標準 (MAJOR.マイナー。PATCH)。

## <a name="id"></a>id

**必須** — Microsoft アプリ ID

このアプリの Microsoft によって生成された一意の識別子。 Microsoft Bot Framework 経由でボットを登録した場合、またはタブの Web アプリが既に Microsoft にサインインしている場合は、既に ID を持っている必要があります。この ID をここに入力する必要があります。 それ以外の場合は、Microsoft アプリケーション登録ポータル ([マイ](https://apps.dev.microsoft.com)アプリケーション) で新しい ID を生成し、ここに入力して、ボットを追加するときに再利用する必要があります。注: AppSource で既存のアプリに更新プログラムを提出する場合は、マニフェスト内の ID を変更することはできません。

## <a name="developer"></a>developer

**必須** — オブジェクト

会社に関する情報を指定します。 AppSource (以前はストアOffice提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。 その他の [情報については、発行ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`name`|32 文字|✔|開発者の表示名。|
|`websiteUrl`|2048 文字|✔|開発者https://の Web サイトの URL を指定します。 このリンクは、ユーザーを会社または製品固有のランディング ページに移動する必要があります。|
|`privacyUrl`|2048 文字|✔|このhttps://開発者のプライバシー ポリシーの URL を指定します。|
|`termsOfUseUrl`|2048 文字|✔|このhttps://開発者の利用規約の URL を示します。|
|`mpnId`|10 文字| |**省略可能** アプリを構築するパートナー組織を識別する Microsoft Partner Network ID。|

## <a name="name"></a>name

**必須** — オブジェクト

Teams エクスペリエンスでユーザーに表示されるアプリ エクスペリエンスの名前。 AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。 値は `short` 同じで `full` 、同じにすべきではありません。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|30 文字|✔|アプリの短い表示名。|
|`full`|100 文字||完全なアプリ名が 30 文字を超える場合に使用される、アプリの完全な名前。|

## <a name="description"></a>説明

**必須** — オブジェクト

アプリをユーザーに説明します。 AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。

説明がエクスペリエンスを正確に説明し、潜在的な顧客がエクスペリエンスの内容を理解するのに役立つ情報を提供します。 また、外部アカウントの使用が必要な場合は、完全な説明で注意する必要があります。 値は `short` 同じで `full` 、同じにすべきではありません。  簡単な説明は、詳細な説明の中で繰り返さず、他のアプリ名を含めずにしてください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|80 文字|✔|スペースが制限されている場合に使用される、アプリのエクスペリエンスの簡単な説明。|
|`full`|4,000 文字|✔|アプリの完全な説明。|

## <a name="packagename"></a>packageName

**省略可能** - 文字列

逆ドメイン表記でのこのアプリの一意識別子。たとえば、com.example.myapp などです。 最大長: 64 文字

## <a name="localizationinfo"></a>localizationInfo

**オプション** — オブジェクト

既定の言語の指定と、追加の言語ファイルへのポインターを許可します。 ローカライズを [参照してください](~/concepts/build-and-test/apps-localization.md)。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`defaultLanguageTag`||✔|このトップ レベルのマニフェスト ファイル内の文字列の言語タグ。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

追加の言語翻訳を指定するオブジェクトの配列。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`languageTag`||✔|指定されたファイル内の文字列の言語タグ。|
|`file`||✔|翻訳された文字列を含む .json ファイルへの相対ファイル パス。|

## <a name="icons"></a>アイコン

**必須** — オブジェクト

Teams アプリ内で使用されるアイコン。 アイコン ファイルは、アップロード パッケージの一部として含める必要があります。 詳細 [については、「アイコン](../../concepts/build-and-test/apps-package.md#app-icons) 」を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`outline`|32 x 32 ピクセル|✔|透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。|
|`color`|192 x 192 ピクセル|✔|フル カラーの 192x192 PNG アイコンへの相対ファイル パス。|

## <a name="accentcolor"></a>accentColor

**省略可能** - HTML 16 進カラー コード

アウトライン アイコンと組み合わせて使用し、背景として使用する色。

値は、'#' で始まる有効な HTML カラー コードである必要があります。次に例を示します `#4464ee` 。

## <a name="configurabletabs"></a>configurableTabs

**省略可能** - 配列

アプリエクスペリエンスにチーム チャネル タブ エクスペリエンスが含み、追加する前に追加の構成が必要な場合に使用されます。 構成可能なタブはチーム スコープでのみサポートされ (個人用ではない)、現在サポートされているのはアプリごとに 1 つのタブのみです。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 文字|✔|タブhttps://するときに使用する URL を指定します。|
|`scopes`|列挙型の配列|1 |✔|現在、構成可能なタブは、スコープ `team` とスコープのみを `groupchat` サポートしています。 |
|`canUpdateConfiguration`|ブール値|||タブの構成のインスタンスを作成後にユーザーが更新できるかどうかを示す値。 既定値: **true 。**|
|`context` |列挙型の配列|6 ||タブが `contextItem` サポートされる範囲のセット。 既定値: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|string|2048||SharePoint で使用するタブ プレビュー イメージへの相対ファイル パス。 サイズ 1024x768。 |
|`supportedSharePointHosts`|列挙型の配列|1 ||SharePoint でタブを使用する方法を定義します。 オプション `sharePointFullPage` は次のとおりです。 `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**省略可能** - 配列

ユーザーが手動で追加することなく、既定で "ピン留め" できる一連のタブを定義します。 スコープ内で宣言された静的タブ `personal` は、常にアプリの個人用エクスペリエンスに固定されます。 このスコープで宣言されている静的 `team` タブは現在サポートされていません。

この項目は、型のすべての要素を持つ配列 (最大 16 要素) です `object` 。 このブロックは、静的タブ ソリューションを提供するソリューションでのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`entityId`|string|64 文字|✔|タブが表示されるエンティティの一意の識別子。|
|`name`|string|128 文字|✔|チャネル インターフェイスのタブの表示名。|
|`contentUrl`|string||✔|次https:// Teams キャンバスに表示されるエンティティ UI を示す URL を指定します。|
|`websiteUrl`|string|||ユーザー https://ブラウザーで表示することを選択した場合にポイントする URL を指定します。|
|`searchUrl`|string|||ユーザー https://の検索クエリを指す URL を指定します。|
|`scopes`|列挙型の配列|1 |✔|現在、静的タブはスコープのみをサポートしています。つまり、個人用エクスペリエンスの一部としてのみ `personal` プロビジョニングできます。|
|`context` | 列挙型の配列| 2 || タブが `contextItem` サポートされる範囲のセット。|

> [!NOTE]
> タブに関連するコンテンツを表示したり、認証フローを開始したりするためにコンテキストに依存する情報が必要な場合は、「Microsoft Teams タブのコンテキストを[取得する」を参照してください](../../tabs/how-to/access-teams-context.md)。

## <a name="bots"></a>bots

**省略可能** - 配列

既定のコマンド プロパティなどのオプションの情報と共に、ボット ソリューションを定義します。

アイテムは、型のすべての要素を持つ配列 (現在、1 つのボットにつき 1 つのボットしか許可されていない要素の最大数 &mdash; ) です `object` 。 このブロックは、ボット エクスペリエンスを提供するソリューションでのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|string|64 文字|✔|Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 これは、アプリ全体の ID と同じ場合 [があります](#id)。|
|`scopes`|列挙型の配列|3 |✔|ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。 これらのオプションは非排他的です。|
|`needsChannelSelector`|ブール値|||ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。 既定値: **`false`**|
|`isNotificationOnly`|ブール値|||ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。 既定値: **`false`**|
|`supportsFiles`|ブール値|||パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。 既定値: **`false`**|
|`supportsCalling`|ブール値|||ボットが音声通話をサポートする場所を示す値。 **重要**: このプロパティは現在試験的です。 試験的なプロパティは完全ではなく、完全に使用可能になる前に変更が発生する可能性があります。  テストと調査のみを目的として提供され、実稼働アプリケーションでは使用できません。 既定値: **`false`**|
|`supportsVideo`|ブール値|||ボットがビデオ通話をサポートする場所を示す値。 **重要**: このプロパティは現在試験的です。 試験的なプロパティは完全ではなく、完全に使用可能になる前に変更が発生する可能性があります。  テストと調査のみを目的として提供され、実稼働アプリケーションでは使用できません。 既定値: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

ボットがユーザーに推奨できるコマンドのオプションの一覧。 オブジェクトは、型のすべての要素を持つ配列 (最大 2 つの要素) です。ボットがサポートするスコープごとに個別のコマンド リストを定義 `object` する必要があります。 詳細 [については、「ボット メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`items.scopes`|列挙型の配列|3 |✔|コマンド リストが有効なスコープを指定します。 `team`、`personal`、`groupchat` の中から選択できます。|
|`items.commands`|オブジェクトの配列|10 |✔|ボットがサポートするコマンドの配列:<br>`title`: ボット コマンドの名前 (文字列、32)<br>`description`: コマンドの構文およびその構文の引数
の簡単な説明または例 (文字列、128)|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|title|string|12 |✔|ボット コマンド名|
|説明|string|128 文字|✔|単純なテキストの説明、またはコマンド構文とその引数の例。|

## <a name="connectors"></a>コネクタ

**省略可能** - 配列

ブロック `connectors` は、アプリの Office 365 コネクタを定義します。

オブジェクトは、すべての種類の要素を持つ配列 (最大 1 つの要素) です `object` 。 このブロックは、コネクタを提供するソリューションでのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 文字|✔|コネクタhttps://するときに使用する URL を指定します。|
|`scopes`|列挙型の配列|1 |✔|コネクタがチャネルのコンテキストでエクスペリエンスを提供するか、または個々のユーザーを対象範囲としたエクスペリエンス `team` () を提供するかどうかを指定します `personal` 。 現時点では、 `team` スコープだけがサポートされています。|
|`connectorId`|string|64 文字|✔|コネクタ開発者ダッシュボードの ID と一致するコネクタの一 [意の識別子](https://aka.ms/connectorsdashboard)。|

## <a name="composeextensions"></a>composeExtensions

**省略可能** - 配列

アプリのメッセージング拡張機能を定義します。

> [!NOTE]
> この機能の名前は、2017 年 11 月に "作成拡張機能" から "メッセージング拡張機能" に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は変わりません。

アイテムは、すべての型の要素を持つ配列 (最大 1 つの要素) です `object` 。 このブロックは、メッセージング拡張機能を提供するソリューションでのみ必要です。

|名前| 種類 | 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|string|64|✔|Bot Framework に登録されている、メッセージング拡張機能をサポートするボットの一意の Microsoft アプリ ID。 これは、アプリ全体の ID と同じ場合があります。|
|`commands`|オブジェクトの配列|10 |✔|メッセージング拡張機能がサポートするコマンドの配列|
|`canUpdateConfiguration`|ブール値|||ユーザーがメッセージング拡張機能の構成を更新できるかどうかを示す値。 既定値: **false**|
|`messageHandlers`|オブジェクトの配列|5 ||特定の条件が満たされた場合にアプリを呼び出すことができるハンドラーの一覧。 ドメインも登録する必要があります。 `validDomains`|
|`messageHandlers.type`|string|||メッセージ ハンドラーの種類。 `"link"` である必要があります。|
|`messageHandlers.value.domains`|文字列の配列|||リンク メッセージ ハンドラーが登録できるドメインの配列。|

### <a name="composeextensionscommands"></a>composeExtensions.commands

メッセージング拡張機能では、1 つ以上のコマンドを宣言する必要があります。 各コマンドは、UI ベースのエントリ ポイントからの潜在的な対話操作として Microsoft Teams に表示されます。 最大 10 のコマンドがあります。

各コマンド項目は、次の構造を持つオブジェクトです。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|string|64 文字|✔|コマンドの ID。|
|`title`|string|32 文字|✔|ユーザーに分かしいコマンド名。|
|`type`|string|64 文字||コマンドの種類。 次のいずれかを `query` 指定します `action` 。 既定値: **クエリ** です。|
|`description`|string|128 文字||このコマンドの目的を示すためにユーザーに表示される説明。|
|`initialRun`|ブール値|||パラメーターを指定してコマンドを最初に実行するかどうかを示すブール値。 既定値: **false**|
|`context`|文字列の配列|3 ||メッセージ拡張を呼び出すことができる場所を定義します。 `compose`, の任意の組 `commandBox` み合 `message` わせ。 既定値は `["compose","commandBox"]` です。|
|`fetchTask`|ブール値|||タスク モジュールを動的にフェッチする必要かどうかを示すブール値。 既定値: **false**|
|`taskInfo`|object|||メッセージング拡張機能コマンドを使用するときに事前読み込むタスク モジュールを指定します。|
|`taskInfo.title`|string|64 文字||最初のダイアログ タイトル。|
|`taskInfo.width`|string|||ダイアログの幅: ピクセル単位の数値、または 'large'、'medium'、'small' などの既定のレイアウトのどちらかです。|
|`taskInfo.height`|string|||ダイアログの高さ : ピクセル単位の数値、または 'large'、'medium'、'small' などの既定のレイアウトのどちらかです。|
|`taskInfo.url`|string|||最初の Webview URL。|
|`parameters`|オブジェクトの配列|5 アイテム|✔|コマンドが受け取るパラメーターの一覧。 最小: 1;最大: 5。|
|`parameters.name`|string|64 文字|✔|クライアントに表示されるパラメーターの名前。 これはユーザー要求に含まれます。|
|`parameters.title`|string|32 文字|✔|パラメーターのユーザー フレンドリーなタイトル。|
|`parameters.description`|string|128 文字||このパラメーターの目的を説明するユーザー フレンドリーな文字列。|
|`parameters.value`|string|512 文字||パラメーターの初期値。|
|`parameters.inputType`|string|128 文字||タスク モジュールに表示されるコントロールの種類を定義します `fetchTask: true` 。 の 1 つ `text, textarea, number, date, time, toggle, choiceset` 。|
|`parameters.choices`|オブジェクトの配列|10 アイテム||The choice options for the `choiceset` . 次の場合にのみ `parameter.inputType` 使用します `choiceset` 。|
|`parameters.choices.title`|string|128 文字|✔|選択したタイトル。|
|`parameters.choices.value`|string|512 文字|✔|Value of the choice.|

## <a name="permissions"></a>アクセス許可

**オプション** - 文字列の配列

アプリが要求するアクセス許可を指定する配列です。エンド ユーザーは拡張機能の実行 `string` 方法を知っています。 次のオプションは非排他的です。

* `identity`&emsp;ユーザー ID 情報が必要
* `messageTeamMembers`&emsp;チーム メンバーに直接メッセージを送信するためのアクセス許可が必要

アプリの更新時にこれらのアクセス許可を変更すると、ユーザーは更新されたアプリを初めて実行するときに同意プロセスを繰り返す必要があります。 詳 [しくは、「アプリの更新」](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) をご覧ください。

## <a name="devicepermissions"></a>devicePermissions

**オプション** - 文字列の配列

アプリがアクセスを要求できるユーザーのデバイスのネイティブ機能を指定します。 オプションは、次のとおりです。

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**省略** 可能 。ただし **、省略可能 (省略可能** )、省略可能 (省略可能)、省略可能 (省略

アプリが Teams クライアント内で読み込む Web サイトの有効なドメインの一覧。 ドメイン一覧には、ワイルドカードを含めできます `*.example.com` 。 これは、ドメインの 1 つのセグメントと正確に一致します。if you need to match then `a.b.example.com` use `*.*.example.com` . タブ構成またはコンテンツ UI で、タブ構成に使用するドメイン以外のドメインに移動する必要がある場合は、ここでそのドメインを指定する必要があります。

ただし、 **アプリ** でサポートする ID プロバイダーのドメインを含める必要はありません。 たとえば、Google ID を使用して認証を行う場合は、accounts.google.com にリダイレクトする必要がありますが、accounts.google.com含めず `validDomains[]` にしてください。

機能するために独自の SharePoint URL を必要とする Teams アプリでは、有効なドメイン リストに "{teamsitedomain}" が含まれる場合があります。

> [!IMPORTANT]
> 直接またはワイルドカードを介して、制御の外部にあるドメインを追加しません。 たとえば、有効 `yourapp.onmicrosoft.com` ですが、 `*.onmicrosoft.com` 無効です。

オブジェクトは、型のすべての要素を持つ配列です `string` 。

## <a name="webapplicationinfo"></a>webApplicationInfo

**オプション** — オブジェクト

Azure Active Directory (Azure AD) アプリ ID と Microsoft Graph 情報を指定して、ユーザーがアプリにシームレスにサインインするのに役立ちます。 アプリが Azure AD に登録されている場合、管理者が Teams 管理センターでアクセス許可を簡単に確認し、同意を与えできるよう、アプリ ID を指定する必要があります。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|string|36 文字|✔|アプリの AAD アプリケーション ID。 この ID は GUID である必要があります。|
|`resource`|string|2048 文字|✔|SSO の認証トークンを取得するためのアプリのリソース URL。 </br> **注:** SSO を使用していない場合は、エラー応答を回避するために、このフィールドにダミー文字列値をアプリ マニフェストに入力 https://notapplicable してください。 |
|`applicationPermissions`|文字列の配列|128 文字||詳細なリソース [固有の同意を指定します](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)。|

## <a name="showloadingindicator"></a>showLoadingIndicator

**省略可能** - ブール値

アプリ/タブの読み込み中に読み込みインジケーターを表示するかどうかを示します。 既定値: **false**
>[!NOTE]
>アプリ マニフェストで "showLoadingIndicator : true" を設定した場合、ページが正しく読み込まれます。「ネイティブ読み込みインジケーター ドキュメントを表示する[](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)」で説明されているプロトコルに従って、タブとタスク モジュールのコンテンツ ページを変更する必要があります。


## <a name="isfullscreen"></a>isFullScreen

 **省略可能** - ブール値

個人用アプリがタブ ヘッダー バーを使用してレンダリングされる場所またはタブ ヘッダー バーなしで表示される場所を示します。 既定値: **false**

## <a name="activities"></a>アクティビティ

**オプション** — オブジェクト

アプリがユーザー アクティビティ フィードに投稿するために使用するプロパティを定義します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`activityTypes`|オブジェクトの配列|128 アイテム| | アプリがユーザー アクティビティ フィードに投稿できるアクティビティの種類を指定します。|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`type`|string|32 文字|✔|通知の種類。 *以下を参照してください*。|
|`description`|string|128 文字|✔|通知の簡単な説明。 *以下を参照してください*。|
|`templateText`|string|128 文字|✔|例: "{actor} created task {taskId} for you"|

```json
{
   "activities":{
      "activityTypes":[
         {
            "type":"taskCreated",
            "description":"Task Created Activity",
            "templateText":"{actor} created task {taskId} for you"
         },
         {
            "type":"teamMention",
            "description":"Team Mention Activity",
            "templateText":"{actor} mentioned team"
         },
         {
            "type":"channelMention",
            "description":"Channel Mention Activity",
            "templateText":"{actor} mentioned channel"
         },
         {
            "type":"userMention",
            "description":"Personal Mention Activity",
            "templateText":"{actor} mentioned user"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"creatorTaskCreated",
            "description":"Created Task Created",
            "templateText":"The Creator created task {taskId} for you"
         }
      ]
   }
}
```

***
>
>
