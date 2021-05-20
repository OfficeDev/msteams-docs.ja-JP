---
title: マニフェスト スキーマリファレンス
description: Microsoft Teamsのマニフェスト スキーマについて説明します。
ms.topic: reference
ms.author: lajanuar
localization_priority: Normal
keywords: チーム マニフェスト スキーマ
ms.openlocfilehash: 6c7cd02480f78d19aed269b5d78d0c6f470621d2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566447"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>リファレンス: Microsoft Teamsのマニフェスト スキーマ

Teamsマニフェストは、アプリがMicrosoft Teams製品にどのように統合するかを示します。 マニフェストは、 でホストされているスキーマに準拠している必要があります [`https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json) 。 以前のバージョン 1.0、1.1,..., 1.6 などもサポートされています (URL に "v1.x" を使用)。

次のスキーマ サンプルでは、すべての機能拡張オプションを示します。

## <a name="sample-full-manifest"></a>完全なマニフェストのサンプル

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.10/MicrosoftTeams.schema.json",
  "manifestVersion": "1.10",
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
  },
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
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
  ]              
}
```

スキーマは、次のプロパティを定義します。

## <a name="schema"></a>$schema

省略可能ですが推奨される文字列

マニフェストの JSON スキーマを参照する https:// URL。

## <a name="manifestversion"></a>マニフェストバージョン

**必須** — 文字列

このマニフェストが使用しているマニフェスト スキーマのバージョン。 1.10 でなければなりません。

## <a name="version"></a>version

**必須** — 文字列

特定のアプリのバージョン。 マニフェスト内の何かを更新する場合は、バージョンもインクリメントする必要があります。 このようにして、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新しい機能を受け取ります。 このアプリがストアに提出された場合、新しいマニフェストを再送信して再検証する必要があります。 アプリ ユーザーは、マニフェストが承認されてから数時間後に、更新された新しいマニフェストを自動的に受け取ります。

アプリがアクセス許可を要求する場合、ユーザーはアップグレードを要求され、アプリに再び同意するように求められます。

このバージョンの文字列は [、semver](http://semver.org/) 標準 (MAJOR.マイナー。パッチ)。

## <a name="id"></a>id

**必須** — マイクロソフト のアプリ ID

ID は、アプリの一意の Microsoft 生成識別子です。 ボットがMicrosoft Bot Frameworkを通じて登録されている場合、またはタブの Web アプリが既に Microsoft にサインインしている場合は、ID を取得できます。 ここに ID を入力する必要があります。 それ以外の場合は、 [Microsoft アプリケーション登録ポータル](https://aka.ms/appregistrations)で新しい ID を生成する必要があります。 ボットを追加する場合は、同じ ID を使用します。

> [!NOTE]
> AppSource で既存のアプリに更新プログラムを送信する場合、マニフェストの ID を変更しないでください。

## <a name="developer"></a>developer

**必須** — オブジェクト

会社に関する情報を指定します。 Teams ストアに送信されたアプリの場合、これらの値はストア登録情報の情報と一致している必要があります。 詳細については、「[ストア公開のTeamsのガイドライン](~/concepts/deploy-and-publish/appsource/publish.md)」を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`name`|32 文字|✔|開発者の表示名。|
|`websiteUrl`|2048 文字|✔|開発者の web サイトへの https:// URL。 このリンクをクリックすると、ユーザーは会社または製品固有のランディング ページに移動する必要があります。|
|`privacyUrl`|2048 文字|✔|開発者のプライバシー ポリシーの https:// URL。|
|`termsOfUseUrl`|2048 文字|✔|開発者の使用条件の https:// URL。|
|`mpnId`|10 文字| |**オプション** アプリを構築するパートナー組織を識別するマイクロソフト パートナー ネットワーク ID。|

## <a name="name"></a>name

**必須** — オブジェクト

Teams エクスペリエンスのユーザーに表示される、アプリ エクスペリエンスの名前。 AppSource に送信されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。 の値との値は `short` `full` 異なっている必要があります。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|30 文字|✔|アプリの短い表示名。|
|`full`|100 文字||アプリの完全名は、アプリの完全名が 30 文字を超える場合に使用されます。|

## <a name="description"></a>説明

**必須** — オブジェクト

ユーザーにアプリを記述します。 AppSource に送信されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。

説明が自分のエクスペリエンスを正確に説明し、潜在顧客がエクスペリエンスの内容を理解するのに役立つ情報を提供するようにします。 外部アカウントを使用する必要がある場合は、完全な説明を書き留める必要があります。 の値との値は `short` `full` 異なっている必要があります。 短い説明は、長い説明の中で繰り返してはならず、他のアプリ名を含めてはいけません。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|80 文字|✔|スペースが限られている場合に使用するアプリ エクスペリエンスの簡単な説明。|
|`full`|4000 文字|✔|アプリの完全な説明。|

## <a name="packagename"></a>パッケージ名

**省略可能** — 文字列

逆ドメイン表記でのアプリの一意の識別子。たとえば、com.example.myapp を使用します。 最大長: 64 文字

## <a name="localizationinfo"></a>ローカリゼーション情報

**オプション** — オブジェクト

既定の言語の指定と、追加の言語ファイルへのポインタを許可します。 詳細については、「 [ローカリゼーション](~/concepts/build-and-test/apps-localization.md)」を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`defaultLanguageTag`||✔|この最上位のマニフェスト ファイル内の文字列の言語タグ。|

### <a name="localizationinfoadditionallanguages"></a>ローカリゼーション情報.追加言語

追加の言語翻訳を指定するオブジェクトの配列。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`languageTag`||✔|指定されたファイル内の文字列の言語タグ。|
|`file`||✔|翻訳された文字列を含む .json ファイルへの相対ファイル パス。|

## <a name="icons"></a>アイコン

**必須** — オブジェクト

Teams アプリ内で使用されるアイコン。 アイコン ファイルは、アップロード パッケージの一部として含める必要があります。 詳細については [、アイコン](../../concepts/build-and-test/apps-package.md#app-icons) を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`outline`|32 x 32 ピクセル|✔|透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。|
|`color`|192 x 192 ピクセル|✔|フルカラーの 192x192 PNG アイコンへの相対ファイル パス。|

## <a name="accentcolor"></a>アクセントカラー

**オプション** — HTML 16 進数のカラーコード

アウトライン アイコンと共に、および背景として使用する色。

値は、たとえば '#' で始まる有効な HTML カラー コードである必要があります `#4464ee` 。

## <a name="configurabletabs"></a>構成可能なタブ

**オプション** — 配列

アプリエクスペリエンスにチーム チャネル タブ エクスペリエンスがあり、追加前に追加の構成が必要な場合に使用します。 構成可能なタブはチームスコープでのみサポートされ、同じタブを複数回構成できます。 ただし、マニフェストで定義できるのは 1 回だけです。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 文字|✔|タブの構成時に使用する https:// URL。|
|`scopes`|列挙型の配列|1|✔|現在、構成可能なタブは `team` 、 および スコープのみをサポート `groupchat` します。 |
|`canUpdateConfiguration`|boolean|||タブの構成のインスタンスを作成後にユーザーが更新できるかどうかを示す値。 デフォルト: **true**.|
|`context` |列挙型の配列|6||`contextItem`[タブがサポートされている](../../tabs/how-to/access-teams-context.md)範囲のセット。 デフォルト: **[チャンネルタブ、プライベートチャットタブ、ミーティングチャットタブ、会議詳細タブ]**|
|`sharePointPreviewImage`|string|2048||SharePointで使用するタブ プレビュー イメージへの相対ファイル パス。 サイズ 1024x768。 |
|`supportedSharePointHosts`|列挙型の配列|1||SharePointでタブを使用できるようにする方法を定義します。 オプションは `sharePointFullPage` 、 `sharePointWebPart` |

## <a name="statictabs"></a>静的タブ

**オプション** — 配列

ユーザーが手動で追加しなくても、既定で "固定" できるタブのセットを定義します。 スコープで宣言された静的タブ `personal` は、常にアプリの個人的なエクスペリエンスに固定されます。 スコープで宣言された静的タブ `team` は、現在サポートされていません。

この項目は、型のすべての要素を持つ配列 (最大 16 個の要素) です `object` 。 このブロックは、静的タブ ソリューションを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`entityId`|string|64 文字|✔|タブが表示するエンティティの一意の識別子。|
|`name`|string|128 文字|✔|チャネル インターフェイスのタブの表示名。|
|`contentUrl`|string||✔|Teams キャンバスに表示されるエンティティ UI を指す https:// URL。|
|`websiteUrl`|string|||ユーザーがブラウザーで表示することを選択した場合に指す https:// URL。|
|`searchUrl`|string|||ユーザーの検索クエリの https:// URL を指します。|
|`scopes`|列挙型の配列|1|✔|現在、静的タブはスコープのみをサポート `personal` するため、個人用エクスペリエンスの一部としてのみプロビジョニングできます。|
|`context` | 列挙型の配列| 2|| `contextItem`タブがサポートされている範囲のセット。|

> [!NOTE]
>  searchUrl 機能は、サードパーティの開発者には使用できません。
> タブで関連するコンテンツを表示したり、認証フローを作成したりするためにコンテキスト依存の情報が必要な場合は[、「Microsoft Teamsタブのコンテキストを取得する](../../tabs/how-to/access-teams-context.md)」を参照してください。

## <a name="bots"></a>ボット

**オプション** — 配列

ボット ソリューションを、既定のコマンド プロパティなどのオプション情報と共に定義します。

item は配列 (最大 1 つの要素のみ &mdash; アプリごとに許可される 1 つのボット) であり、すべての要素が type `object` . このブロックは、ボット エクスペリエンスを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|string|64 文字|✔|Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 これは、 [全体的なアプリ ID](#id)と同じである可能性があります。|
|`scopes`|列挙型の配列|3|✔|ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。 これらのオプションは非排他的です。|
|`needsChannelSelector`|boolean|||ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。 デフォルト： **`false`**|
|`isNotificationOnly`|boolean|||ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。 デフォルト： **`false`**|
|`supportsFiles`|boolean|||パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。 デフォルト： **`false`**|
|`supportsCalling`|boolean|||ボットがオーディオ呼び出しをサポートする場所を示す値。 **重要**: このプロパティは現在、実験的なものです。 実験プロパティは完全ではない可能性があり、完全に利用可能になる前に変更を受ける可能性があります。  テストと探索のみを目的として提供され、実稼働アプリケーションでは使用しないでください。 デフォルト： **`false`**|
|`supportsVideo`|boolean|||ボットがビデオ通話をサポートする場所を示す値。 **重要**: このプロパティは現在、実験的なものです。 実験プロパティは完全ではない可能性があり、完全に利用可能になる前に変更を受ける可能性があります。  テストと探索のみを目的として提供され、実稼働アプリケーションでは使用しないでください。 デフォルト： **`false`**|

### <a name="botscommandlists"></a>コマンドリスト

ボットがユーザーに推奨できるコマンドのリスト(オプション)。 オブジェクトは、型のすべての要素を持つ配列 (最大 2 つの要素) です `object` 。 詳細については [、「Bot メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`items.scopes`|列挙型の配列|3|✔|コマンド リストが有効なスコープを指定します。 `team`、`personal`、`groupchat` の中から選択できます。|
|`items.commands`|オブジェクトの配列|10|✔|ボットがサポートするコマンドの配列:<br>`title`: ボット コマンドの名前 (文字列、32)<br>`description`: コマンド構文とその引数の簡単な説明または例 (文字列、128)。|

### <a name="botscommandlistscommands"></a>コマンド

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|title|string|12 |✔|ボット コマンド名。|
|説明|string|128 文字|✔|単純な説明、またはコマンド構文とその引数の例。|

## <a name="connectors"></a>コネクタ

**オプション** — 配列

`connectors`ブロックは、アプリのOffice 365コネクタを定義します。

オブジェクトは、型のすべての要素を持つ配列 (最大 1 要素) `object` です。 このブロックは、コネクタを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 文字|✔|コネクタの構成時に使用する https:// URL。|
|`scopes`|列挙型の配列|1|✔|コネクタが、 のチャネルのコンテキストでのエクスペリエンスを提供 `team` するか、個々のユーザーに限定されたエクスペリエンス ( ) を提供するかを指定 `personal` します。 現在、スコープのみが `team` サポートされています。|
|`connectorId`|string|64 文字|✔|コネクタ開発者ダッシュボード の ID と一致する [コネクタの](https://aka.ms/connectorsdashboard)一意の識別子。|

## <a name="composeextensions"></a>コン成拡張

**オプション** — 配列

アプリのメッセージング拡張機能を定義します。

> [!NOTE]
> 機能の名前は、2017 年 11 月に "拡張の構成" から "メッセージング拡張機能" に変更されましたが、マニフェスト名はそのまま残り、既存の拡張機能が機能し続けます。

項目は、型のすべての要素を持つ配列 (最大 1 要素) `object` です。 このブロックは、メッセージング拡張機能を提供するソリューションにのみ必要です。

|名前| 型 | 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|string|64|✔|Bot Framework に登録されているメッセージング拡張機能をサポートするボットの一意の Microsoft アプリ ID。 これは、アプリ ID 全体と同じである可能性があります。|
|`commands`|オブジェクトの配列|10|✔|メッセージング拡張機能がサポートするコマンドの配列。|
|`canUpdateConfiguration`|boolean|||メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。 既定値: **false**|
|`messageHandlers`|オブジェクトの配列|5||特定の条件が満たされた場合にアプリを呼び出すことを許可するハンドラーのリスト。|
|`messageHandlers.type`|string|||メッセージ ハンドラーの種類。 `"link"` である必要があります。|
|`messageHandlers.value.domains`|文字列の配列|||リンク メッセージ ハンドラーが登録できるドメインの配列。|

### <a name="composeextensionscommands"></a>コンスタブスエクステンション.コマンド

メッセージング拡張機能は、1 つ以上のコマンドを宣言する必要があります。 各コマンドは、UI ベースのエントリ ポイントからの潜在的な操作としてMicrosoft Teamsに表示されます。 最大 10 個のコマンドがあります。

各コマンド項目は、次の構造を持つオブジェクトです。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|string|64 文字|✔|コマンドの ID。|
|`title`|string|32 文字|✔|わかりやすいコマンド名。|
|`type`|string|64 文字||コマンドの種類。 または の 1 つ `query` `action` デフォルト: **クエリ**.|
|`description`|string|128 文字||このコマンドの目的を示すためにユーザーに表示される説明。|
|`initialRun`|boolean|||ブール値は、コマンドが最初にパラメーターなしで実行されるかどうかを示します。 既定値は **false** です。|
|`context`|文字列の配列|3||メッセージ拡張を呼び出すことができる場所を定義します。 、 、、を任意に組み合わせて `compose` `commandBox` `message` 使用できます。 既定値は `["compose","commandBox"]` です。|
|`fetchTask`|boolean|||タスク モジュールを動的にフェッチする必要があるかどうかを示すブール値。 既定値は **false** です。|
|`taskInfo`|object|||メッセージング拡張コマンドを使用する場合にプリロードするタスク・モジュールを指定します。|
|`taskInfo.title`|string|64 文字||初期ダイアログ タイトル。|
|`taskInfo.width`|string|||ダイアログ幅 - ピクセル単位の数値またはデフォルトのレイアウト ("大きい"、"中""、"小" など)|
|`taskInfo.height`|string|||ダイアログの高さ - ピクセル単位の数値または既定のレイアウト ("大きい"、"中""、"小" など)|
|`taskInfo.url`|string|||初期の Web ビュー URL。|
|`parameters`|オブジェクトの配列|5項目|✔|コマンドが受け取るパラメーターのリスト。 最小: 1;最大: 5。|
|`parameters.name`|string|64 文字|✔|クライアントに表示されるパラメータの名前。 これはユーザー要求に含まれます。|
|`parameters.title`|string|32 文字|✔|パラメーターのわかりやすいタイトルです。|
|`parameters.description`|string|128 文字||このパラメーターの目的を説明するわかりやすい文字列。|
|`parameters.value`|string|512 文字||パラメータの初期値。|
|`parameters.inputType`|string|128 文字||のタスク モジュールに表示されるコントロールの種類を定義 `fetchTask: true` します。 の 1 つ `text, textarea, number, date, time, toggle, choiceset` 。|
|`parameters.choices`|オブジェクトの配列|10項目||の選択肢オプション `choiceset` です。 の場合にのみ `parameter.inputType` 使用 `choiceset` します。|
|`parameters.choices.title`|string|128 文字|✔|選択したタイトル。|
|`parameters.choices.value`|string|512 文字|✔|Value of the choice.|

## <a name="permissions"></a>permissions

**オプション** — 文字列の配列

`string`アプリが要求するアクセス許可を指定する配列で、エンド ユーザーに拡張機能の実行方法を知ることができます。 次のオプションは非排他的です。

* `identity`&emsp;ユーザー ID 情報が必要です。
* `messageTeamMembers`&emsp;チーム メンバーにダイレクト メッセージを送信する権限が必要です。

アプリの更新中にこれらのアクセス許可を変更すると、更新されたアプリを実行した後、ユーザーは同意プロセスを繰り返します。 詳しくは、 [アプリの更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) を参照してください。

## <a name="devicepermissions"></a>デバイスアクセス許可

**オプション** — 文字列の配列

アプリがアクセスを要求するユーザーのデバイスにネイティブ機能を提供します。 オプションは、次のとおりです。

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>有効なドメイン

**省略可能** な 、 **省略可能** な場合は必須です。

アプリがTeams クライアント内で読み込むと想定している Web サイトの有効なドメインの一覧。 ドメインの一覧には、ワイルドカードを含めることができます `*.example.com` 。 これは、ドメインの 1 つのセグメントと完全に一致します。一致させる必要がある場合は `a.b.example.com` `*.*.example.com` 、 を使用します。 タブ構成またはコンテンツ UI がタブ構成の使用以外のドメインに移動する必要がある場合は、ここでそのドメインを指定する必要があります。

アプリでサポートする ID プロバイダーのドメインを含める必要 **はありません** 。 たとえば、Google ID を使用して認証を行うには、accounts.google.com にリダイレクトする必要があります `validDomains[]` accounts.google.com。

Teams、自分の sharepoint URL が正常に機能する必要があるアプリには、有効なドメイン リストに "{teamsitedomain}" が含まれます。

> [!IMPORTANT]
> 直接またはワイルドカードを使用して、コントロールの外側にあるドメインを追加しないでください。 たとえば、 `yourapp.onmicrosoft.com` 有効なが、 `*.onmicrosoft.com` 無効です。

オブジェクトは、 type のすべての要素を持つ配列です `string` 。

## <a name="webapplicationinfo"></a>アプリケーション情報

**オプション** — オブジェクト

ユーザーがアプリにシームレスにサインインできるように、Azure Active Directory (AAD) アプリ ID と Microsoft Graph情報を提供します。 アプリが AAD に登録されている場合は、管理者が簡単にアクセス許可を確認し、管理センターで同意Teams付与できるように、アプリ ID を指定する必要があります。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|string|36 文字|✔|アプリの AAD アプリケーション ID。 この ID は GUID である必要があります。|
|`resource`|string|2048 文字|✔|SSO の認証トークンを取得するためのアプリのリソース URL。 </br> **注:** SSO を使用していない場合は、エラー応答を避けるために、このフィールドにダミーの文字列値をアプリ マニフェストに入力してください https://notapplicable 。 |
|`applicationPermissions`|文字列の配列|128 文字||詳細な [リソース固有の同意](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)を指定する :|

## <a name="showloadingindicator"></a>ショーローディングインジケータ

**オプション** — ブール値

アプリまたはタブの読み込み時に読み込みインジケーターを表示するかどうかを示します。 既定値は **false** です。
>[!NOTE]
>アプリ マニフェストで true として選択した場合 `showLoadingIndicator` は、ページを正しく読み込むように、「 [ネイティブ読み込みインジケーター](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) ドキュメントを表示する」の説明に従って、タブとタスク モジュールのコンテンツ ページを変更します。


## <a name="isfullscreen"></a>フルスクリーン

 **オプション** — ブール値

タブ ヘッダー バーを使用するか、またはタブ ヘッダー バーを使用せずに、個人用アプリをレンダリングする場所を指定します。 既定値は **false** です。

## <a name="activities"></a>activities

**オプション** — オブジェクト

ユーザーアクティビティフィードを投稿するためにアプリが使用するプロパティを定義します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`activityTypes`|オブジェクトの配列|128項目| | アプリがユーザーのアクティビティ フィードに投稿できるアクティビティの種類を指定します。|

### <a name="activitiesactivitytypes"></a>アクティビティ.アクティビティタイプ

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`type`|string|32 文字|✔|通知の種類。 *以下を参照してください*。|
|`description`|string|128 文字|✔|通知の簡単な説明。 *以下を参照してください*。|
|`templateText`|string|128 文字|✔|例: "{アクター} が作成したタスク {taskId}|

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


