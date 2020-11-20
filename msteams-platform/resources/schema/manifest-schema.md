---
title: マニフェストスキーマの参照
description: Microsoft Teams のマニフェストスキーマについて説明します。
keywords: teams マニフェストスキーマ
author: laujan
ms.author: lajanuar
ms.openlocfilehash: 3bf8bcc0ff99228b5dafded319df6f21ade56c2b
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346687"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>リファレンス: Microsoft Teams のマニフェストスキーマ

Microsoft Teams のマニフェストでは、アプリを Microsoft Teams 製品に統合する方法について説明します。 マニフェストは、でホストされているスキーマに準拠している必要があり [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) ます。 以前のバージョン 1.0-1.4 もサポートされています (URL で "v1" を使用します)。

次のスキーマサンプルは、すべての拡張オプションを示しています。

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

*省略可能 (ただし推奨* ) 文字列

マニフェストの JSON スキーマを参照する https://URL。

## <a name="manifestversion"></a>manifestVersion

**必須** -文字列

このマニフェストが使用しているマニフェストスキーマのバージョン。 "1.7" である必要があります。

## <a name="version"></a>バージョン

**必須** -文字列

特定のアプリのバージョン。 マニフェスト内の内容を更新する場合は、そのバージョンも同時にインクリメントする必要があります。 このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。 このアプリがストアに送信された場合は、新しいマニフェストを再送信して再検証する必要があります。 その後、このアプリのユーザーは、承認後に数時間以内に新しい更新されたマニフェストを自動的に取得します。

アプリによって要求されたアクセス許可が変更された場合、ユーザーはアプリをアップグレードして再同意するように求められます。

このバージョンの文字列は、 [semver](http://semver.org/) 標準 (メジャー) に従う必要があります。間隔.パッチ)。

## <a name="id"></a>id

**必須** -MICROSOFT アプリ ID

このアプリの一意の Microsoft 生成識別子。 Microsoft Bot フレームワークを介して bot を登録した場合、またはタブの web アプリが Microsoft によって既にサインインしている場合は、既に ID があるので、ここで入力する必要があります。 それ以外の場合は、Microsoft アプリケーション登録ポータル ([My Applications](https://apps.dev.microsoft.com)) で新しい ID を生成し、ここで入力してから、bot を追加するときにそれを再利用する必要があります。注: AppSource で既存のアプリに更新を送信する場合は、マニフェスト内の ID を変更しないでください。

## <a name="developer"></a>developer

**Required** -オブジェクト

会社に関する情報を指定します。 AppSource (旧称 Office ストア) に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。 追加情報については、 [発行に関するガイドライン](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) を参照してください。

|Name| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`name`|32文字|✔|開発者の表示名。|
|`websiteUrl`|2048 文字|✔|開発者の web サイトへの https://URL。 このリンクは、ユーザーを会社または製品固有のランディングページに移動する必要があります。|
|`privacyUrl`|2048 文字|✔|開発者のプライバシーポリシーへの https://URL。|
|`termsOfUseUrl`|2048 文字|✔|開発者の使用条件への https://URL。|
|`mpnId`|10文字| |**省略可能** アプリを構築するパートナー組織を識別する Microsoft パートナーのネットワーク ID。|

## <a name="name"></a>name

**Required** -オブジェクト

Teams でユーザーに表示されるアプリの動作の名前です。 AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。 との値 `short` を同じにすることはでき `full` ません。

|Name| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|30 文字|✔|アプリの短い表示名。|
|`full`|100 文字||アプリの完全な名前。アプリの完全な名前が30文字を超えている場合に使用されます。|

## <a name="description"></a>description

**Required** -オブジェクト

ユーザーに対してアプリを記述します。 AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。

説明に正確に表示されていることを確認し、お客様が快適な動作を理解するのに役立つ情報を提供します。 また、外部アカウントが使用するために必要な場合は、詳細な説明にも注意してください。 との値 `short` を同じにすることはでき `full` ません。  短い説明を長い説明の中で繰り返すことはできません。他のアプリ名を含めることはできません。

|Name| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|80文字|✔|スペースが制限されている場合に使用する、アプリの使用状況の簡単な説明。|
|`full`|4000文字|✔|アプリの詳細な説明。|

## <a name="packagename"></a>packageName

**省略可能** (string)

逆引きドメイン表記でのこのアプリの一意識別子。たとえば、例のようになります。 最大長: 64 文字

## <a name="localizationinfo"></a>localizationInfo

**Optional** -オブジェクト

既定の言語の指定、および追加の言語ファイルへのポインターを許可します。 「 [ローカライズ](~/concepts/build-and-test/apps-localization.md)」を参照してください。

|Name| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`defaultLanguageTag`||✔|このトップレベルマニフェストファイル内の文字列の言語タグ。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo. additionalLanguages

追加の言語の翻訳を指定するオブジェクトの配列。

|Name| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`languageTag`||✔|指定されたファイル内の文字列の言語タグ。|
|`file`||✔|翻訳された文字列を含む json ファイルへの相対ファイルパス。|

## <a name="icons"></a>アイコン

**Required** -オブジェクト

Teams アプリ内で使用されるアイコン。 アイコンファイルは、アップロードパッケージの一部として含める必要があります。 詳細については、「 [アイコン](~/concepts/build-and-test/apps-package.md#icons) 」を参照してください。

|Name| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`outline`|32 x 32 ピクセル|✔|透明な32x32 の PNG アウトラインアイコンへの相対ファイルパス。|
|`color`|192 x 192 ピクセル|✔|フルカラー 192x192 PNG アイコンへの相対ファイルパス。|

## <a name="accentcolor"></a>アクセントカラー

**オプション** -HTML 16 進カラーコード

とと組み合わせてアウトラインアイコンの背景として使用する色。

この値は、' # ' で始まる有効な HTML カラーコードである必要があります (例 `#4464ee` :)。

## <a name="configurabletabs"></a>の各タブ

**省略可能** -配列

アプリの機能に、追加の構成を必要とするチームチャネルのタブがある場合に使用されます。 構成可能なタブは teams スコープ (個人ではない) でのみサポートされており、現在、アプリごとに **1 つ** のタブのみがサポートされています。

|Name| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|文字列|2048 文字|✔|タブを構成するときに使用する https://URL。|
|`scopes`|列挙型の配列|1-d|✔|現在、構成可能なタブでは、およびスコープのみがサポートさ `team` `groupchat` れています。 |
|`canUpdateConfiguration`|ブール値|||作成後にタブの構成のインスタンスをユーザーが更新できるかどうかを示す値。 既定値は **true** です。|
|`context` |列挙型の配列|6 ||`contextItem`タブがサポートされているスコープのセット。 既定値: **[Channeltab、privateChatTab、meetingChatTab、会議の設定]**。|
|`sharePointPreviewImage`|文字列|2048||SharePoint で使用するタブプレビュー画像への相対ファイルパス。 サイズ1024x768。 |
|`supportedSharePointHosts`|列挙型の配列|1-d||SharePoint でどのようにタブを使用できるようにするかを定義します。 オプション `sharePointFullPage` と `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**省略可能** -配列

ユーザーが手動で追加せずに、既定で "固定" できるタブのセットを定義します。 スコープ内で宣言 `personal` されている静的タブは、常にアプリの個人の環境に固定されます。 スコープ内で宣言されている静的タブ `team` は現在サポートされていません。

この項目は、型のすべての要素を含む配列 (最大16個の要素) です `object` 。 このブロックは、静的なタブソリューションを提供するソリューションに対してのみ必要です。

|Name| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`entityId`|文字列|64 文字|✔|タブに表示されるエンティティの一意識別子。|
|`name`|文字列|128文字|✔|チャネルインターフェイスのタブの表示名。|
|`contentUrl`|文字列||✔|Teams キャンバスに表示されるエンティティ UI をポイントする https://URL。|
|`websiteUrl`|文字列|||ユーザーがブラウザーで表示をポイントしたかどうかを示す https://URL。|
|`searchUrl`|文字列|||ユーザーの検索クエリを指す https://URL。|
|`scopes`|列挙型の配列|1-d|✔|現時点では、静的タブではスコープのみがサポート `personal` されます。つまり、個人の利便性の一環としてのみプロビジョニングできます。|
|`context` | 列挙型の配列| pbm-2|| `contextItem`タブがサポートされているスコープのセット。|

> [!NOTE]
> 関連するコンテンツを表示したり、認証フローを開始したりするために、タブにコンテキスト依存情報が必要な場合は、「 [Microsoft Teams のコンテキストを取得する」タブ](../../tabs/how-to/access-teams-context.md)を *参照してください*。

## <a name="bots"></a>bot

**省略可能** -配列

Bot ソリューションと、既定のコマンドプロパティなどのオプション情報を定義します。

アイテムが配列の場合 (現時点では1つの要素のみ &mdash; が可能)、その型のすべての要素が含まれ `object` ます。 このブロックは、bot の環境を提供するソリューションにのみ必要です。

|Name| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|文字列|64 文字|✔|Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 これは、アプリの全体的な [ID](#id)と同じである場合もあります。|
|`scopes`|列挙型の配列|1/3|✔|ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。 これらのオプションは非排他的です。|
|`needsChannelSelector`|ブール値|||ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。 限り **`false`**|
|`isNotificationOnly`|ブール値|||ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。 限り `**false**`|
|`supportsFiles`|ブール値|||パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。 限り **`false`**|
|`supportsCalling`|ブール値|||Bot が音声通話をサポートするかどうかを示す値。 **重要**: このプロパティは現在実験的なものです。 実験的なプロパティは完成していない可能性があり、完全に使用できるようになる前に変更が行われる可能性があります。  テストと調査の目的でのみ提供されており、運用アプリケーションでは使用しないでください。 限り **`false`**|
|`supportsVideo`|ブール値|||Bot がビデオ通話をサポートする場所を示す値。 **重要**: このプロパティは現在実験的なものです。 実験的なプロパティは完成していない可能性があり、完全に使用できるようになる前に変更が行われる可能性があります。  テストと調査の目的でのみ提供されており、運用アプリケーションでは使用しないでください。 限り **`false`**|

### <a name="botscommandlists"></a>bot リスト

Bot がユーザーに推奨できるコマンドのオプションの一覧。 Object は、型のすべての要素を含む配列 (最大2つの要素) です `object` 。 bot がサポートするスコープごとに個別のコマンドリストを定義する必要があります。 詳細については、「 [Bot メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。

|Name| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`items.scopes`|列挙型の配列|1/3|✔|コマンド リストが有効なスコープを指定します。 `team`、`personal`、`groupchat` の中から選択できます。|
|`items.commands`|オブジェクトの配列|10  |✔|ボットがサポートするコマンドの配列:<br>`title`: ボット コマンドの名前 (文字列、32)<br>`description`: コマンドの構文およびその構文の引数
の簡単な説明または例 (文字列、128)|

### <a name="botscommandlistscommands"></a>bot のリストコマンド

|Name| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|title|string|12 |✔|Bot コマンド名|
|description|string|128文字|✔|簡単なテキストの説明、またはコマンド構文とその引数の例。|

## <a name="connectors"></a>コネクタ

**省略可能** -配列

ブロックは、 `connectors` アプリの Office 365 コネクタを定義します。

Object は、type のすべての要素を含む配列 (最大1つの要素) です `object` 。 このブロックは、コネクタを提供するソリューションに対してのみ必要です。

|Name| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|文字列|2048 文字|✔|コネクタを構成するときに使用する https://URL。|
|`scopes`|列挙型の配列|1-d|✔|コネクタが内のチャネルのコンテキストで、 `team` または個別のユーザー単独 () にスコープ設定された環境での動作を提供するかどうかを指定し `personal` ます。 現時点では、 `team` 範囲のみがサポートされています。|
|`connectorId`|文字列|64 文字|✔|コネクタ [開発者ダッシュボード](https://aka.ms/connectorsdashboard)の ID と一致するコネクタの一意識別子。|

## <a name="composeextensions"></a>この機能

**省略可能** -配列

アプリのメッセージング拡張機能を定義します。

> [!NOTE]
> この機能の名前は、2017年11月に「[作成] 拡張機能」から「messaging extension」に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は同じままです。

Item は、type のすべての要素を含む配列 (最大1つの要素) です `object` 。 このブロックは、メッセージング拡張機能を提供するソリューションに対してのみ必要です。

|Name| 種類 | 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|文字列|64|✔|Bot フレームワークに登録されているメッセージング拡張機能をバックアップする bot の一意の Microsoft アプリ ID。 これは、アプリの全体的な ID と同じである場合もあります。|
|`commands`|オブジェクトの配列|10  |✔|メッセージング拡張機能がサポートするコマンドの配列|
|`canUpdateConfiguration`|ブール値|||メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。 既定値: **false**|
|`messageHandlers`|オブジェクトの配列|5 ||特定の条件が満たされたときにアプリを呼び出せるようにするハンドラーの一覧。 ドメインも、にリストされている必要があります。 `validDomains`|
|`messageHandlers.type`|文字列|||メッセージハンドラの種類。 `"link"` である必要があります。|
|`messageHandlers.value.domains`|文字列の配列|||リンクメッセージハンドラが登録できるドメインの配列。|

### <a name="composeextensionscommands"></a>このコマンドの機能

メッセージング拡張機能は、1つ以上のコマンドを宣言する必要があります。 各コマンドは、Microsoft Teams に UI ベースのエントリポイントからの潜在的な操作として表示されます。 最大10個のコマンドがあります。

各コマンド項目は、次の構造を持つオブジェクトです。

|Name| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|文字列|64 文字|✔|コマンドの ID。|
|`title`|文字列|32文字|✔|ユーザーフレンドリなコマンド名。|
|`type`|文字列|64 文字||コマンドの種類。 またはのいずれか `query` `action` です。 既定値: **query**。|
|`description`|文字列|128文字||このコマンドの目的を示すためにユーザーに表示される説明。|
|`initialRun`|ブール値|||パラメーターを指定せずにコマンドを最初に実行する必要があるかどうかを示すブール値。 既定値: **false**|
|`context`|文字列の配列|1/3||メッセージの内線番号をから呼び出すことができる場所を定義します。 、、の任意の組み合わせ `compose` `commandBox` `message` 。 既定値は `["compose","commandBox"]` です。|
|`fetchTask`|ブール値|||タスクモジュールを動的にフェッチする必要があるかどうかを示すブール値。 既定値: **false**|
|`taskInfo`|object|||メッセージ拡張コマンドの使用時に、タスクモジュールを事前に読み込むように指定します。|
|`taskInfo.title`|文字列|64 文字||最初のダイアログのタイトル。|
|`taskInfo.width`|文字列|||ダイアログの幅。ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。|
|`taskInfo.height`|文字列|||ダイアログの高さ-ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。|
|`taskInfo.url`|文字列|||最初の webview の URL。|
|`parameters`|オブジェクトの配列|5アイテム|✔|コマンドが実行するパラメーターの一覧。 最小値: 1、最大: 5|
|`parameters.name`|文字列|64 文字|✔|クライアントに表示されるパラメーターの名前。 これは、ユーザー要求に含まれています。|
|`parameters.title`|文字列|32文字|✔|パラメーターのユーザーフレンドリなタイトル。|
|`parameters.description`|文字列|128文字||このパラメーターの目的を説明するユーザーフレンドリ文字列。|
|`parameters.value`|文字列|512文字||パラメータの初期値。|
|`parameters.inputType`|文字列|128文字||のタスクモジュールに表示されるコントロールの種類を定義 `fetchTask: true` します。 のいずれか `text, textarea, number, date, time, toggle, choiceset` です。|
|`parameters.choices`|オブジェクトの配列|10アイテム||の選択オプション `choiceset` 。 がである場合にのみ使用 `parameter.inputType` `choiceset` します。|
|`parameters.choices.title`|文字列|128文字|✔|選択項目のタイトル。|
|`parameters.choices.value`|文字列|512文字|✔|Value of the choice.|

## <a name="permissions"></a>アクセス許可

**省略可能** -文字列の配列

`string`アプリが要求するアクセス許可を指定する配列。これにより、エンドユーザーは拡張機能の動作を知ることができます。 非排他的なオプションは次のとおりです。

* `identity`&emsp;ユーザー id 情報が必要
* `messageTeamMembers`&emsp;チームメンバーに直接メッセージを送信するためのアクセス許可が必要

アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは、更新されたアプリを初めて実行したときに同意プロセスを繰り返すようになります。 詳細については [、「アプリの更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) 」を参照してください。

## <a name="devicepermissions"></a>devicePermissions

**省略可能** -文字列の配列

アプリがアクセスを要求することができる、ユーザーのデバイスのネイティブ機能を指定します。 オプションは、次のとおりです。

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**省略可能**(記載個所に **必要な** 場合を除く)

アプリが Teams クライアント内で読み込むことが想定されている web サイトの有効なドメインの一覧。 ドメインリストには、たとえば、ワイルドカードを含めることができ `*.example.com` ます。 これは、1つのドメインのセグメントに一致します。に一致させる必要がある場合は `a.b.example.com` 、を使用 `*.*.example.com` します。 タブ構成またはコンテンツ UI が他のドメインに移動する必要がある場合 (タブの構成に使用するものを除く)、そのドメインをここで指定する必要があります。

ただし、アプリでサポートする id プロバイダーのドメインを含める必要は **ありません** 。 たとえば、Google ID を使用して認証するには、accounts.google.com にリダイレクトする必要がありますが、に accounts.google.com を含めることはできません `validDomains[]` 。

自分の sharepoint Url が適切に機能する必要がある Teams アプリは、有効なドメインリストに "{teamsitedomain}" を含めることができます。

> [!IMPORTANT]
> 直接に、またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しないでください。 たとえば、は有効ですが、有効では `yourapp.onmicrosoft.com` `*.onmicrosoft.com` ありません。

Object は、型のすべての要素を含む配列です `string` 。

## <a name="webapplicationinfo"></a>webApplicationInfo

**Optional** -オブジェクト

Aad アプリ ID とグラフ情報を指定して、ユーザーが AAD アプリにシームレスにサインインできるようにします。

|Name| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|文字列|36文字|✔|アプリの AAD アプリケーション id。 この id は GUID である必要があります。|
|`resource`|文字列|2048 文字|✔|SSO の認証トークンを取得するためのアプリのリソース url。|
|`applicationPermissions`|文字列の配列|128文字||[リソース固有の](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)詳細な同意を指定する|

## <a name="showloadingindicator"></a>showLoadingIndicator

**Optional** -boolean

アプリ/タブが読み込まれているときに、読み込みインジケーターを表示するかどうかを指定します。 既定値: **false**
>[!NOTE]
>アプリマニフェストで "showLoadingIndicator: true" を設定した場合、ページが正しく読み込まれるようにするには、「 [ネイティブロードインジケーター](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) ドキュメントを表示する」で説明されているプロトコルに従って、タブおよびタスクモジュールのコンテンツページを変更する必要があります。


## <a name="isfullscreen"></a>isFullScreen

 **Optional** -boolean

個人用アプリがタブヘッダーバーを使用して、または表示せずにレンダリングされる場所を指定します。 既定値: **false**

## <a name="activities"></a>アクティビティ

**Optional** -オブジェクト

アプリがユーザーアクティビティフィードに投稿するときに使用するプロパティを定義します。

|Name| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`activityTypes`|オブジェクトの配列|128アイテム| | アプリがユーザーアクティビティフィードに投稿できるアクティビティの種類を指定します。|

### <a name="activitiesactivitytypes"></a>アクティビティの種類

|Name| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`type`|文字列|32文字|✔|通知の種類。 *以下を参照して* ください。|
|`description`|文字列|128文字|✔|通知の簡単な説明。 *以下を参照して* ください。|
|`templateText`|文字列|128文字|✔|Ex: "{actor} ' のタスク {taskId} が作成されました"|

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
