---
title: マニフェスト スキーマ参照
description: アプリケーションのマニフェスト スキーマについてMicrosoft Teams
ms.topic: reference
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams マニフェスト スキーマ
ms.openlocfilehash: e542378a45262312978d0d091439938907b974ac
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888287"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>リファレンス: マニフェスト スキーマのMicrosoft Teams

このTeamsマニフェストは、アプリが製品に統合する方法Microsoft Teamsします。 マニフェストは、 でホストされるスキーマに準拠している必要があります [`https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json) 。 以前のバージョン 1.0、1.1,...,、1.11 もサポートされています (URL で "v1.x" を使用)。
各バージョンで行われた変更の詳細については、「マニフェスト変更 [ログ」を参照してください](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)。

次のスキーマ サンプルは、すべての機能拡張オプションを示しています。

## <a name="sample-full-manifest"></a>完全なマニフェストのサンプル

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
  "manifestVersion": "1.11",
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
          "description": "Command Description; e.g., Add a customer",
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
        },
         {
          "id": "exampleCmd3",
          "title": "Example Command 3",
          "type": "action",
          "context": [
            "compose",
            "commandBox",
            "message"
          ],
          "description": "Command Description; e.g., Add a customer",
          "fetchTask": false,
          "taskInfo": {
            "title": "Initial dialog title",
            "width": "Dialog width",
            "height": "Dialog height",
            "url": "Initial webview URL"
          }
        }
      ],
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
    ]
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
  "defaultBlockUntilAdminAction": true,
  "publisherDocsUrl": "https://website.com/app-info",
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  },
 "configurableProperties": {
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "developerUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  }
}
```

スキーマは、次のプロパティを定義します。

## <a name="schema"></a>$schema

省略可能ですが、推奨される文字列

マニフェスト https:// JSON スキーマを参照する URL を指定します。

## <a name="manifestversion"></a>manifestVersion

**必須**—string

このマニフェストが使用しているマニフェスト スキーマのバージョン。 1.10 である必要があります。

## <a name="version"></a>version

**必須**—string

特定のアプリのバージョン。 マニフェストで何かを更新する場合は、バージョンもインクリメントする必要があります。 これにより、新しいマニフェストがインストールされた場合、既存のマニフェストが上書きされ、ユーザーは新しい機能を受け取ります。 このアプリがストアに送信されると、新しいマニフェストを再送信して再評価する必要があります。 アプリユーザーは、マニフェストが承認された後、数時間以内に新しい更新されたマニフェストを自動的に受信します。

アプリでアクセス許可の要求が変更された場合、ユーザーはアプリのアップグレードと再調整を求めるメッセージが表示されます。

このバージョンの文字列は [、semver](http://semver.org/) 標準 (MAJOR) に従う必要があります。MINOR。PATCH)。

## <a name="id"></a>id

**必須**—Microsoft アプリ ID

ID は、アプリの Microsoft が生成する一意の識別子です。 ボットがアカウントを通じて登録されている場合は、id をMicrosoft Bot Framework。 タブの Web アプリが既に Microsoft にサインインしている場合は、ID を持っています。 ここに ID を入力する必要があります。 それ以外の場合は、Microsoft アプリケーション登録ポータルで新しい ID [を生成する必要があります](https://aka.ms/appregistrations)。 ボットを追加する場合は、同じ ID を使用します。

> [!NOTE]
> AppSource で既存のアプリに更新プログラムを提出する場合は、マニフェスト内の ID を変更することはできません。

## <a name="developer"></a>developer

**必須**—object

会社に関する情報を指定します。 アプリがストアに送信Teams、これらの値はストア登録情報の情報と一致している必要があります。 詳細については、「ストア発行ガイドラインTeams[を参照してください](~/concepts/deploy-and-publish/appsource/publish.md)。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`name`|32 文字|✔|開発者の表示名。|
|`websiteUrl`|2048 文字|✔|開発者 https:// WEB サイトの URL を指定します。 このリンクは、ユーザーを会社または製品固有のランディング ページに移動する必要があります。|
|`privacyUrl`|2048 文字|✔|開発者 https:// のプライバシー ポリシーの URL を指定します。|
|`termsOfUseUrl`|2048 文字|✔|開発者 https:// の使用条件の URL を指定します。|
|`mpnId`|10 文字| |**省略可能** アプリを構築するパートナー組織を識別する Microsoft パートナー ネットワーク ID。|

## <a name="name"></a>name

**必須**—object

アプリ エクスペリエンスのユーザーに表示されるアプリ エクスペリエンスのTeamsします。 AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。 の値と `short` 異 `full` なる値を指定する必要があります。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|30 文字|✔|アプリの短い表示名。|
|`full`|100 文字||完全なアプリ名が 30 文字を超える場合に使用されるアプリの完全な名前。|

## <a name="description"></a>description

**必須**—object

アプリをユーザーに説明します。 AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。

説明に自分のエクスペリエンスが記述され、潜在的な顧客が自分のエクスペリエンスの内容を理解するのに役立ちます。 外部アカウントを使用する必要がある場合は、完全な説明に注意する必要があります。 の値と `short` 異 `full` なる値を指定する必要があります。 短い説明は長い説明の中で繰り返す事はできないので、他のアプリ名を含めずにしてください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|80 文字|✔|スペースが制限されている場合に使用されるアプリ エクスペリエンスの簡単な説明。|
|`full`|4000 文字|✔|アプリの完全な説明。|

## <a name="packagename"></a>packageName

**省略** 可能な —string

逆ドメイン表記のアプリの一意の識別子。たとえば、com.example.myapp などです。 最大長: 64 文字

## <a name="localizationinfo"></a>localizationInfo

**省略** 可能な —object

既定の言語の指定を許可し、より多くの言語ファイルへのポインターを提供します。 詳細については、「ローカライズ」を [参照してください](~/concepts/build-and-test/apps-localization.md)。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`defaultLanguageTag`||✔|このトップ レベルのマニフェスト ファイル内の文字列の言語タグ。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

より多くの言語翻訳を指定するオブジェクトの配列。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`languageTag`||✔|指定されたファイル内の文字列の言語タグ。|
|`file`||✔|翻訳された文字列を含む .json ファイルへの相対ファイル パス。|

## <a name="icons"></a>アイコン

**必須**—object

アプリ内で使用Teamsアイコン。 アイコン ファイルは、アップロード パッケージの一部として含める必要があります。 詳細については、「アイコン」を [参照してください](../../concepts/build-and-test/apps-package.md#app-icons)。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`outline`|32 x 32 ピクセル|✔|透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。|
|`color`|192 x 192 ピクセル|✔|フル カラーの 192x192 PNG アイコンへの相対ファイル パス。|

## <a name="accentcolor"></a>accentColor

**必須**—HTML の 16 進カラー コード

アウトライン アイコンの背景として使用する色。

値は、'#' で始まる有効な HTML カラー コードである必要があります `#4464ee` 。

## <a name="configurabletabs"></a>configurableTabs

**省略** 可能な —array

アプリ エクスペリエンスに、追加する前に追加の構成が必要なチーム チャネル タブ エクスペリエンスがある場合に使用します。 構成可能なタブは、スコープ内でのみサポート `team` `groupchat` され、同じタブを複数回構成できます。 ただし、マニフェストで定義できるのは 1 回のみです。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 文字|✔|タブ https:// する際に使用する URL を指定します。|
|`scopes`|列挙型の配列|1|✔|現在、構成可能なタブは、スコープ `team` とスコープ `groupchat` のみをサポートしています。 |
|`canUpdateConfiguration`|ブール値|||作成後に、タブの構成のインスタンスをユーザーが更新できるかどうかを示す値。 既定値: **true 。**|
|`context` |列挙型の配列|6 ||タブが `contextItem` サポートされているスコープ [のセット](../../tabs/how-to/access-teams-context.md)です。 既定値: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.|
|`sharePointPreviewImage`|string|2048||タブ プレビュー イメージへの相対ファイル パスを使用して、SharePoint。 サイズは 1024x768 です。 |
|`supportedSharePointHosts`|列挙型の配列|1||タブを使用してタブを使用する方法をSharePoint。 オプションは `sharePointFullPage` 次のとおりです。 `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**省略** 可能な —array

ユーザーが手動で追加せずに、既定で "ピン留め" できるタブのセットを定義します。 スコープ内で宣言された静的タブ `personal` は、常にアプリの個人用エクスペリエンスにピン留めされます。 スコープで宣言されている静的タブ `team` は現在サポートされていません。

このアイテムは、型のすべての要素を持つ配列 (最大 16 要素) です `object` 。 このブロックは、静的タブ ソリューションを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`entityId`|string|64 文字|✔|タブが表示されるエンティティの一意の識別子。|
|`name`|string|128 文字|✔|チャネル インターフェイスのタブの表示名。|
|`contentUrl`|string||✔|この https:// キャンバスに表示するエンティティ UI を示すTeamsします。|
|`websiteUrl`|string|||ユーザー https:// ブラウザーで表示することを選択した場合に示す URL を指定します。|
|`searchUrl`|string|||ユーザー https:// 検索クエリを参照する URL を指定します。|
|`scopes`|列挙型の配列|1|✔|現在、静的タブはスコープのみをサポートしています。つまり、個人用エクスペリエンスの一部としてのみ `personal` プロビジョニングできます。|
|`context` | 列挙型の配列| 2|| タブが `contextItem` サポートされているスコープのセット。|

> [!NOTE]
>  サード パーティの開発者は searchUrl 機能を使用できません。
> 関連するコンテンツを表示したり、認証フローを開始したりするために、タブにコンテキスト依存の情報が必要な場合は、「Get context for your [Microsoft Teams タブ」を参照してください](../../tabs/how-to/access-teams-context.md)。

## <a name="bots"></a>bots

**省略** 可能な —array

既定のコマンド プロパティなどのオプションの情報と共に、ボット ソリューションを定義します。

アイテムは、型のすべての要素を持つ配列 (現在、1 つのボットにつき 1 つのボットしか許可されていない要素の最大数 &mdash; ) です `object` 。 このブロックは、ボット エクスペリエンスを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|string|64 文字|✔|Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 ID は、アプリ全体の ID と [同じにできます](#id)。|
|`scopes`|列挙型の配列|3|✔|ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。 これらのオプションは非排他的です。|
|`needsChannelSelector`|ブール値|||ボットがユーザー ヒントを使用して特定のチャネルにボットを追加するかどうかを説明します。 既定値: **`false`**|
|`isNotificationOnly`|ブール値|||ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。 既定値: **`false`**|
|`supportsFiles`|ブール値|||パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。 既定値: **`false`**|
|`supportsCalling`|ブール値|||ボットがオーディオ通話をサポートする場所を示す値。 **重要**: このプロパティは現在実験的です。 実験的なプロパティは完全ではない可能性があります。また、完全に利用可能になる前に変更が加わる可能性があります。  このプロパティはテストと探索の目的でのみ提供され、実稼働アプリケーションでは使用できません。 既定値: **`false`**|
|`supportsVideo`|ブール値|||ボットがビデオ通話をサポートする場所を示す値。 **重要**: このプロパティは現在実験的です。 実験的なプロパティは完全ではない可能性があります。また、完全に利用可能になる前に変更が加わる可能性があります。  このプロパティはテストと探索の目的でのみ提供され、実稼働アプリケーションでは使用できません。 既定値: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

ボットがユーザーに推奨できるコマンドのオプションの一覧。 オブジェクトは、型のすべての要素を持つ配列 (最大 2 つの要素) です。ボットがサポートするスコープごとに個別のコマンド リストを `object` 定義する必要があります。 詳細については [、「Bot メニュー」を参照してください](~/bots/how-to/create-a-bot-commands-menu.md)。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`items.scopes`|列挙型の配列|3|✔|コマンド リストが有効なスコープを指定します。 `team`、`personal`、`groupchat` の中から選択できます。|
|`items.commands`|オブジェクトの配列|10|✔|ボットがサポートするコマンドの配列:<br>`title`: ボット コマンドの名前 (文字列、32)<br>`description`: コマンド構文とその引数の簡単な説明または例 (文字列、128)。|

### <a name="botscommandlistscommands"></a>bots.commandLists.command

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|title|string|12 |✔|ボット コマンド名。|
|description|string|128 文字|✔|単純なテキストの説明、またはコマンド構文とその引数の例。|

## <a name="connectors"></a>コネクタ

**省略** 可能な —array

ブロック `connectors` は、アプリOffice 365コネクタを定義します。

オブジェクトは、型のすべての要素を持つ配列 (最大 1 つの要素) です `object` 。 このブロックは、Connector を提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 文字|✔|コネクタ https:// する際に使用する URL を指定します。|
|`scopes`|列挙型の配列|1|✔|Connector がチャネルのコンテキストでエクスペリエンスを提供するかどうか、または個々のユーザー () にスコープを設定したエクスペリエンスを提供するかどうかを `team` 指定します `personal` 。 現在、スコープ `team` だけがサポートされています。|
|`connectorId`|string|64 文字|✔|コネクタ開発者ダッシュボードの ID に一致するコネクタの一 [意の識別子](https://aka.ms/connectorsdashboard)です。|

## <a name="composeextensions"></a>composeExtensions

**省略** 可能な —array

アプリのメッセージング拡張機能を定義します。

> [!NOTE]
> 機能の名前は、2017 年 11 月に "作成拡張機能" から "メッセージング拡張機能" に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は変わりません。

アイテムは、型のすべての要素を持つ配列 (最大 1 つの要素) です `object` 。 このブロックは、メッセージング拡張機能を提供するソリューションにのみ必要です。

|名前| 型 | 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|string|64|✔|ボット フレームワークに登録されているメッセージング拡張機能をバックするボットの一意の Microsoft アプリ ID。 ID は、アプリ全体の ID と同じにできます。|
|`commands`|オブジェクトの配列|10|✔|メッセージング拡張機能がサポートするコマンドの配列。|
|`canUpdateConfiguration`|ブール値|||メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。 既定値: **false**|
|`messageHandlers`|オブジェクトの配列|5||特定の条件が満たされた場合にアプリを呼び出すことができるハンドラーの一覧。|
|`messageHandlers.type`|string|||メッセージ ハンドラーの種類。 `"link"` である必要があります。|
|`messageHandlers.value.domains`|文字列の配列|||リンク メッセージ ハンドラーが登録できるドメインの配列。|

### <a name="composeextensionscommands"></a>composeExtensions.commands

メッセージング拡張機能では、最大 10 のコマンドで 1 つ以上のコマンドを宣言する必要があります。 各コマンドは、MICROSOFT TEAMSエントリ ポイントからの潜在的な対話として表示されます。

各コマンド 項目は、次の構造を持つオブジェクトです。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|string|64 文字|✔|コマンドの ID。|
|`title`|string|32 文字|✔|ユーザーフレンドリーなコマンド名。|
|`type`|string|64 文字||コマンドの種類。 または `query` の 1 `action` つ。 既定: **クエリ** です。|
|`description`|string|128 文字||このコマンドの目的を示すためにユーザーに表示される説明。|
|`initialRun`|ブール値|||ブール値は、コマンドがパラメーターを使用して最初に実行されるかどうかを示します。 既定値は **false** です。|
|`context`|文字列の配列|3||メッセージ拡張機能の呼び出し先を定義します。 `compose`、 の任意の `commandBox` 組み合 `message` わせ。 既定値は `["compose","commandBox"]` です。|
|`fetchTask`|ブール値|||タスク モジュールを動的にフェッチする必要があるかどうかを示すブール値。 既定値は **false** です。|
|`taskInfo`|object|||メッセージング拡張機能コマンドを使用する場合に事前読み込みするタスク モジュールを指定します。|
|`taskInfo.title`|string|64 文字||最初のダイアログ タイトル。|
|`taskInfo.width`|string|||ダイアログの幅 - ピクセル単位の数値または既定のレイアウト ('large'、'medium'、または 'small' など)。|
|`taskInfo.height`|string|||ダイアログの高さ - ピクセル単位の数値、または 'large'、'medium'、または 'small' などの既定のレイアウト。|
|`taskInfo.url`|string|||初期 Webview URL。|
|`parameters`|オブジェクトの配列|5 つのアイテム|✔|コマンドが受け取るパラメーターの一覧。 最小: 1;最大: 5。|
|`parameters.name`|string|64 文字|✔|クライアントに表示されるパラメーターの名前。 パラメーター名は、ユーザー要求に含まれます。|
|`parameters.title`|string|32 文字|✔|パラメーターのユーザーフレンドリーなタイトル。|
|`parameters.description`|string|128 文字||このパラメーターの目的を説明するユーザーフレンドリーな文字列。|
|`parameters.value`|string|512 文字||パラメーターの初期値。|
|`parameters.inputType`|string|128 文字||タスク モジュールに表示されるコントロールの種類を定義します `fetchTask: true` 。 の 1 `text, textarea, number, date, time, toggle, choiceset` つ。|
|`parameters.choices`|オブジェクトの配列|10 アイテム||の選択肢 `choiceset` オプションです。 の場合にのみ `parameter.inputType` 使用します `choiceset` 。|
|`parameters.choices.title`|string|128 文字|✔|選択したタイトル。|
|`parameters.choices.value`|string|512 文字|✔|Value of the choice.|

## <a name="permissions"></a>アクセス許可

**省略** 可能 —文字列の配列

アプリが要求するアクセス許可を指定する 、拡張機能の動作をエンド ユーザーに知らせる配列 `string` 。 次のオプションは、非排他的です。

* `identity`&emsp;ユーザー ID 情報が必要です。
* `messageTeamMembers`&emsp;チーム メンバーに直接メッセージを送信するためのアクセス許可が必要です。

アプリの更新中にこれらのアクセス許可を変更すると、更新されたアプリの実行後にユーザーが同意プロセスを繰り返します。 詳細については、「アプリの [更新」を参照してください](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)。

## <a name="devicepermissions"></a>devicePermissions

**省略** 可能 —文字列の配列

アプリがアクセスを要求するユーザーのデバイス上のネイティブ機能を提供します。 オプションは、次のとおりです。

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**省略** 可能です 。ただし **、必須の** 場合は省略可能です。

アプリがクライアント内で読み込むと予想される Web サイトの有効なドメインTeamsします。 ドメインの一覧には、ワイルドカード (たとえば) を含めできます `*.example.com` 。 有効なドメインは、ドメインの 1 つのセグメントと完全に一致します。一致する必要がある場合は、 `a.b.example.com` を使用します `*.*.example.com` 。 タブ構成またはコンテンツ UI がタブ構成以外の他のドメインに移動する場合は、ここでそのドメインを指定する必要があります。

サポート **する** ID プロバイダーのドメインをアプリに含めない。 たとえば、Google ID を使用して認証を行う場合は、accounts.google.com にリダイレクトする必要があります。ただし、accounts.google.com を含 accounts.google.com 必要があります `validDomains[]` 。

Teams機能するために独自の url をSharePointするアプリには、有効なドメイン リストに "{teamsitedomain}" が含まれます。

> [!IMPORTANT]
> 直接またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しません。 たとえば、 `yourapp.onmicrosoft.com` 有効ですが、 `*.onmicrosoft.com` 無効です。

オブジェクトは、型のすべての要素を持つ配列です `string` 。

## <a name="webapplicationinfo"></a>webApplicationInfo

**省略** 可能な —object

ユーザーがアプリAzure Active DirectoryシームレスAADを支援するために、アプリ ID と Microsoft Graph情報を提供します。 アプリがアプリに登録されているAAD、アプリ ID を指定する必要があります。 管理者は、管理者センターでアクセス許可を簡単に確認し、Teamsを許可できます。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|string|36 文字|✔|AADのアプリケーション ID を指定します。 この ID は GUID である必要があります。|
|`resource`|string|2048 文字|✔|SSO の認証トークンを取得するためのアプリのリソース URL。 </br> **注:** SSO を使用していない場合は、エラー応答を回避するために、このフィールドにダミーの文字列値をアプリ マニフェストに https://notapplicable 入力してください。 |
|`applicationPermissions`|文字列の配列|128 文字||詳細なリソース [固有の同意を指定します](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)。|

## <a name="showloadingindicator"></a>showLoadingIndicator

**省略** 可能な —boolean

アプリまたはタブの読み込み時に読み込みインジケーターを表示するかどうかを示します。 既定値は **false** です。
>[!NOTE]
>アプリ マニフェストで true を選択した場合、ページを正しく読み込むには、「ネイティブ読み込みインジケーター ドキュメントを表示する」の説明に従って、タブとタスク モジュールのコンテンツ ページを `showLoadingIndicator` [変更](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) します。


## <a name="isfullscreen"></a>isFullScreen

 **省略** 可能な —boolean

タブ ヘッダー バーの付きまたはなしで個人用アプリがレンダリングされる場所を示します。 既定値は **false** です。

> [!NOTE]
> `isFullScreen`タブとストア アプリSharePointでのみ動作します。

## <a name="activities"></a>activities

**省略** 可能な —object

アプリがユーザー アクティビティ フィードの投稿に使用するプロパティを定義します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`activityTypes`|オブジェクトの配列|128 アイテム| | アプリがユーザーアクティビティ フィードに投稿できるアクティビティの種類を指定します。|

### <a name="activitiesactivitytypes"></a>activity.activityTypes

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`type`|string|32 文字|✔|通知の種類。 *以下を参照してください*。|
|`description`|string|128 文字|✔|通知の簡単な説明。 *以下を参照してください*。|
|`templateText`|string|128 文字|✔|例: "{actor} が作成したタスク {taskId} for you"|

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

## <a name="configurableproperties"></a>configurableProperties

**オプション** - 配列

この `configurableProperties` ブロックは、管理者がカスタマイズできるアプリTeams定義します。 詳細については、「アプリのカスタマイズを [有効にする」を参照してください](~/concepts/design/enable-app-customization.md)。 アプリのカスタマイズ機能は、カスタム アプリまたは LOB アプリではサポートされていません。

> [!NOTE]
> 少なくとも 1 つのプロパティを定義する必要があります。 このブロックでは、最大 9 つのプロパティを定義できます。

次のプロパティを定義できます。

* `name`: アプリの表示名。
* `shortDescription`: アプリの簡単な説明です。
* `longDescription`: アプリの長い説明。
* `smallImageUrl`: アプリのアウトライン アイコン。
* `largeImageUrl`: アプリの色アイコン。
* `accentColor`: 使用する色とアウトライン アイコンの背景。
* `developerUrl`: 開発者の Web サイトの HTTPS URL。
* `privacyUrl`: 開発者のプライバシー ポリシーの HTTPS URL。
* `termsOfUseUrl`: 開発者の使用条件の HTTPS URL。

## <a name="defaultblockuntiladminaction"></a>defaultBlockUntilAdminAction

**省略** 可能な —boolean
 
プロパティ `defaultBlockUntilAdminAction` が true に **設定されている場合**、管理者が許可するまで、アプリは既定でユーザーから非表示になります。 true に **設定すると**、アプリは、すべてのテナントとエンド ユーザーに対して非表示になります。 テナント管理者は、管理者センターでアプリをTeamsし、アプリを許可またはブロックするアクションを実行できます。 既定値は **false** です。 既定のアプリ ブロックの詳細については、「管理者が承認[するまでアプリTeams非表示にする」を参照してください](~/concepts/design/enable-app-customization.md#hide-teams-app-until-admin-approves)。


## <a name="publisherdocsurl"></a>publisherDocsUrl

**省略** 可能 - 文字列

**最大サイズ** - 128 文字

プロパティはに依存します `defaultBlockUntilAdminAction` 。 プロパティが true に設定されている場合は、既定でブロックされているアプリを許可する前に、管理者がガイドラインを取得する情報ページに `defaultBlockUntilAdminAction` HTTPS URL `publisherDocsUrl` を提供します。

## <a name="see-also"></a>関連項目

* [アプリ構造Microsoft Teams理解する](~/concepts/design/app-structure.md)
* [アプリのカスタマイズを有効にする](~/concepts/design/enable-app-customization.md)
* [アプリをローカライズする](~/concepts/build-and-test/apps-localization.md)
* [メディア機能を統合する](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Developer Preview マニフェスト スキーマ参照 - Teams](~/resources/schema/manifest-schema-dev-preview.md)
