---
title: マニフェストスキーマの参照
description: Microsoft Teams のマニフェストによってサポートされるスキーマについて説明します。
keywords: teams マニフェストスキーマ
ms.openlocfilehash: 1a1a690e6e382dcad3ceb200ec02286e8c9171f8
ms.sourcegitcommit: 060b486c38b72a3e6b63b4d617b759174082a508
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2020
ms.locfileid: "41953489"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>リファレンス: Microsoft Teams のマニフェストスキーマ

Microsoft Teams のマニフェストでは、アプリを Microsoft Teams 製品に統合する方法について説明します。 マニフェストは、で[`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json)ホストされているスキーマに準拠している必要があります。 以前のバージョン 1.0-1.4 もサポートされています (URL で "v1" を使用します)。

次のスキーマサンプルは、すべての拡張オプションを示しています。

## <a name="sample-full-manifest"></a>完全なマニフェストのサンプル

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
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
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
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
        }
      ],
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
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ]
}
```

スキーマは、次のプロパティを定義します。

## <a name="schema"></a>$schema

*省略可能。ただし、推奨* &ndash;文字列

マニフェストの JSON スキーマを参照する https://URL。

## <a name="manifestversion"></a>manifestVersion

**必要な** &ndash;文字列

このマニフェストが使用しているマニフェストスキーマのバージョン。 "1.5" である必要があります。

## <a name="version"></a>バージョン

**必要な** &ndash;文字列

特定のアプリのバージョン。 マニフェスト内の内容を更新する場合は、そのバージョンも同時にインクリメントする必要があります。 このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。 このアプリがストアに送信された場合は、新しいマニフェストを再送信して再検証する必要があります。 その後、このアプリのユーザーは、承認後に数時間以内に新しい更新されたマニフェストを自動的に取得します。

アプリによって要求されたアクセス許可が変更された場合、ユーザーはアプリをアップグレードして再同意するように求められます。

このバージョンの文字列は、 [semver](http://semver.org/)標準 (メジャー) に従う必要があります。間隔.パッチ)。

## <a name="id"></a>id

**必要な** &ndash; Microsoft アプリ ID

このアプリの一意の Microsoft 生成識別子。 Microsoft Bot フレームワークを介して bot を登録した場合、またはタブの web アプリが Microsoft によって既にサインインしている場合は、既に ID があるので、ここで入力する必要があります。 それ以外の場合は、Microsoft アプリケーション登録ポータル ([My Applications](https://apps.dev.microsoft.com)) で新しい ID を生成し、ここで入力してから、bot を追加するときにそれを再利用する必要があります。注: AppSource で既存のアプリに更新を送信する場合は、マニフェスト内の ID を変更しないでください。

## <a name="packagename"></a>packageName

**必要な** &ndash;文字列

逆引きドメイン表記でのこのアプリの一意識別子。たとえば、例のようになります。

## <a name="developer"></a>developer

**Required**

会社に関する情報を指定します。 AppSource (旧称 Office ストア) に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。 追加情報については、[発行に関するガイドライン](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`name`|32文字|✔|開発者の表示名。|
|`websiteUrl`|2048 文字|✔|開発者の web サイトへの https://URL。 このリンクは、ユーザーを会社または製品固有のランディングページに移動する必要があります。|
|`privacyUrl`|2048 文字|✔|開発者のプライバシーポリシーへの https://URL。|
|`termsOfUseUrl`|2048 文字|✔|開発者の使用条件への https://URL。|
|`mpnId`|10文字| |**省略可能**アプリを構築するパートナー組織を識別する Microsoft パートナーのネットワーク ID。|

## <a name="localizationinfo"></a>localizationInfo

**Optional**

既定の言語の指定、および追加の言語ファイルへのポインターを許可します。 「[ローカライズ](~/concepts/build-and-test/apps-localization.md)」を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`defaultLanguageTag`||✔|このトップレベルマニフェストファイル内の文字列の言語タグ。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo. additionalLanguages

追加の言語の翻訳を指定するオブジェクトの配列。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`languageTag`||✔|指定されたファイル内の文字列の言語タグ。|
|`file`||✔|翻訳された文字列を含む json ファイルへの相対ファイルパス。|

## <a name="name"></a>name

**Required**

Teams でユーザーに表示されるアプリの動作の名前です。 AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。 との`short`値を`full`同じにすることはできません。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|30 文字|✔|アプリの短い表示名。|
|`full`|100 文字||アプリの完全な名前。アプリの完全な名前が30文字を超えている場合に使用されます。|

## <a name="description"></a>説明

**Required**

ユーザーに対してアプリを記述します。 AppSource に提出されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。

説明に正確に表示されていることを確認し、お客様が快適な動作を理解するのに役立つ情報を提供します。 また、外部アカウントが使用するために必要な場合は、詳細な説明にも注意してください。 との`short`値を`full`同じにすることはできません。  短い説明を長い説明の中で繰り返すことはできません。他のアプリ名を含めることはできません。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|80文字|✔|スペースが制限されている場合に使用する、アプリの使用状況の簡単な説明。|
|`full`|4000文字|✔|アプリの詳細な説明。|

## <a name="icons"></a>アイコン

**Required**

Teams アプリ内で使用されるアイコン。 アイコンファイルは、アップロードパッケージの一部として含める必要があります。 詳細については、「[アイコン](~/concepts/build-and-test/apps-package.md#icons)」を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`outline`|2048 文字|✔|透明な32x32 の PNG アウトラインアイコンへの相対ファイルパス。|
|`color`|2048 文字|✔|フルカラー 192x192 PNG アイコンへの相対ファイルパス。|

## <a name="accentcolor"></a>アクセントカラー

**必要な** &ndash;文字列

とと組み合わせてアウトラインアイコンの背景として使用する色。

この値は、' # ' で始まる有効な HTML カラーコードである必要`#4464ee`があります (例:)。

## <a name="configurabletabs"></a>の各タブ

**Optional**

アプリの機能に、追加の構成を必要とするチームチャネルのタブがある場合に使用されます。 構成可能なタブは teams スコープでのみサポートされており、現在、アプリごとに1つのタブのみがサポートされています。

Object は、型`object`のすべての要素を含む配列です。 このブロックは、構成可能なチャネルのタブソリューションを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|String|2048 文字|✔|タブを構成するときに使用する https://URL。|
|`canUpdateConfiguration`|ブール値|||作成後にタブの構成のインスタンスをユーザーが更新できるかどうかを示す値。 限り`true`|
|`scopes`|列挙型の配列|1 |✔|現在、構成可能なタブで`team`は`groupchat` 、およびスコープのみがサポートされています。 |
|`sharePointPreviewImage`|String|2048||SharePoint で使用するタブプレビュー画像への相対ファイルパス。 サイズ1024x768。 |
|`supportedSharePointHosts`|列挙型の配列|1 ||SharePoint でどのようにタブを使用できるようにするかを定義します。 オプション`sharePointFullPage`と`sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**Optional**

ユーザーが手動で追加せずに、既定で "固定" できるタブのセットを定義します。 スコープ内で`personal`宣言されている静的タブは、常にアプリの個人の環境に固定されます。 `team`スコープ内で宣言されている静的タブは現在サポートされていません。

Object は、型`object`のすべての要素を含む配列 (最大16個の要素) です。 このブロックは、静的なタブソリューションを提供するソリューションに対してのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`entityId`|String|64 文字|✔|タブに表示されるエンティティの一意識別子。|
|`name`|String|128文字|✔|チャネルインターフェイスのタブの表示名。|
|`contentUrl`|String|2048 文字|✔|Teams キャンバスに表示されるエンティティ UI をポイントする https://URL。|
|`websiteUrl`|String|2048 文字||ユーザーがブラウザーで表示をポイントしたかどうかを示す https://URL。|
|`scopes`|列挙型の配列|1 |✔|現時点では、静的タブで`personal`はスコープのみがサポートされます。つまり、個人の利便性の一環としてのみプロビジョニングできます。|

> [!NOTE]
> 関連するコンテンツを表示したり、認証フローを開始したりするために、タブにコンテキスト依存情報が必要な場合は、「 [Microsoft Teams のコンテキストを取得する」タブ](../../tabs/how-to/access-teams-context.md)を*参照してください*。

## <a name="bots"></a>bot

**Optional**

Bot ソリューションと、既定のコマンドプロパティなどのオプション情報を定義します。

オブジェクトが配列の場合 (現時点では1つ&mdash;の要素のうちの最大値は1つですが、現在は`object`アプリごとに1つの bot のみが許可されます)、型のすべての要素を使用します このブロックは、bot の環境を提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|String|64 文字|✔|Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 これは、アプリの全体的な[ID](#id)と同じである場合もあります。|
|`needsChannelSelector`|ブール値|||ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。 限り`false`|
|`isNotificationOnly`|ブール値|||ボットが会話ボットではなく、一方向性の通知専用ボットなのかどうかを示します。 限り`false`|
|`supportsFiles`|Boolean|||パーソナル チャットでのファイルのアップロード/ダウンロード機能をボットでサポートするかどうかを示します。 限り`false`|
|`scopes`|列挙型の配列|3 |✔|ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。 これらのオプションは非排他的です。|

### <a name="botscommandlists"></a>bot リスト

Bot がユーザーに推奨できるコマンドのオプションの一覧。 Object は、型`object`のすべての要素を含む配列 (最大2つの要素) です。bot がサポートするスコープごとに個別のコマンドリストを定義する必要があります。 詳細については、「 [Bot メニュー](~/bots/how-to/create-a-bot-commands-menu.md) 」を参照してください。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`items.scopes`|列挙型の配列|3 |✔|コマンド リストが有効なスコープを指定します。 `team`、`personal`、`groupchat` の中から選択できます。|
|`items.commands`|オブジェクトの配列|10 |✔|ボットがサポートするコマンドの配列:<br>`title`: ボット コマンドの名前 (文字列、32)<br>`description`: コマンドの構文およびその構文の引数
の簡単な説明または例 (文字列、128)|

## <a name="connectors"></a>コネクタ

**Optional**

ブロック`connectors`は、アプリの Office 365 コネクタを定義します。

Object は、type `object`のすべての要素を含む配列 (最大1つの要素) です。 このブロックは、コネクタを提供するソリューションに対してのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|String|2048 文字|✔|コネクタを構成するときに使用する https://URL。|
|`connectorId`|String|64 文字|✔|コネクタ[開発者ダッシュボード](https://aka.ms/connectorsdashboard)の ID と一致するコネクタの一意識別子。|
|`scopes`|列挙型の配列|1 |✔|コネクタが内`team`のチャネルのコンテキストで、または個別のユーザー単独 (`personal`) にスコープ設定された環境での動作を提供するかどうかを指定します。 現時点では、 `team`範囲のみがサポートされています。|

## <a name="composeextensions"></a>この機能

**Optional**

アプリのメッセージング拡張機能を定義します。

> [!NOTE]
> この機能の名前は、2017年11月に「[作成] 拡張機能」から「messaging extension」に変更されましたが、既存の拡張機能が引き続き機能するように、マニフェスト名は同じままです。

Object は、type `object`のすべての要素を含む配列 (最大1つの要素) です。 このブロックは、メッセージング拡張機能を提供するソリューションに対してのみ必要です。

|名前| 型 | 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|String|64|✔|Bot フレームワークに登録されているメッセージング拡張機能をバックアップする bot の一意の Microsoft アプリ ID。 これは、アプリの全体的な ID と同じである場合もあります。|
|`canUpdateConfiguration`|ブール値|||メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。 既定値は `false` です。|
|`commands`|オブジェクトの配列|10 |✔|メッセージング拡張機能がサポートするコマンドの配列|
|`messageHandlers`|オブジェクトの配列|5 ||特定の条件が満たされたときにアプリを呼び出せるようにするハンドラーの一覧。 ドメインも、にリストされている必要があります。`validDomains`|
|`messageHandlers.type`|String|||メッセージハンドラの種類。 `"link"` である必要があります。|
|`messageHandlers.value.domains`|文字列 (String) の配列|||リンクメッセージハンドラが登録できるドメインの配列。|

### <a name="composeextensionscommands"></a>このコマンドの機能

メッセージング拡張機能は、1つ以上のコマンドを宣言する必要があります。 各コマンドは、Microsoft Teams に UI ベースのエントリポイントからの潜在的な操作として表示されます。 最大10個のコマンドがあります。

各コマンド項目は、次の構造を持つオブジェクトです。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|String|64 文字|✔|コマンドの ID|
|`type`|String|64 文字||コマンドの種類。 または`query` `action`のいずれかです。 限り`query`|
|`title`|String|32文字|✔|ユーザーフレンドリなコマンド名|
|`description`|String|128文字||このコマンドの目的を示すためにユーザーに表示される説明。|
|`initialRun`|ブール値|||パラメーターを指定せずにコマンドを最初に実行する必要があるかどうかを示すブール値。 限り`false`|
|`context`|文字列 (String) の配列|3 ||メッセージの内線番号をから呼び出すことができる場所を定義します。 、 `commandBox`、 `message`の`compose`任意の組み合わせ。 既定値は`["compose", "commandBox"]`|
|`fetchTask`|ブール値|||タスクモジュールを動的に取得する必要があるかどうかを示すブール値。|
|`taskInfo`|オブジェクト|||メッセージ拡張コマンドの使用時にプリロードするタスクモジュールを指定する|
|`taskInfo.title`|String|64||最初のダイアログのタイトル|
|`taskInfo.width`|String|||ダイアログの幅。ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。|
|`taskInfo.height`|String|||ダイアログの高さ-ピクセル単位または既定のレイアウト (' large '、' medium '、または ' small ' など) のいずれかを指定します。|
|`taskInfo.url`|String|||最初の webview の URL|
|`parameters`|オブジェクトの配列|5 |✔|コマンドが実行するパラメーターの一覧。 最小値: 1、最大: 5|
|`parameter.name`|String|64 文字|✔|クライアントに表示されるパラメーターの名前。 これは、ユーザー要求に含まれています。|
|`parameter.title`|String|32文字|✔|パラメーターのユーザーフレンドリなタイトル。|
|`parameter.description`|String|128文字||このパラメーターの目的を説明するユーザーフレンドリ文字列。|
|`parameter.inputType`|String|128文字||の`fetchTask: true`タスクモジュールに表示されるコントロールの種類を定義します。 、 `text` `textarea` `number` `date`、、、、、のいずれかの`time` `toggle``choiceset`|
|`parameter.choices`|オブジェクトの配列|10 ||の選択オプション`choiceset`。 がである`parameter.inputType`場合にのみ使用します`choiceset`|
|`parameter.choices.title`|String|128||選択肢のタイトル|
|`parameter.choices.value`|String|512||選択肢の値|

## <a name="permissions"></a>アクセス許可

**Optional**

アプリが要求`string`するアクセス許可を指定する配列。これにより、エンドユーザーは拡張機能の動作を知ることができます。 非排他的なオプションは次のとおりです。

* `identity`&emsp;ユーザー id 情報が必要
* `messageTeamMembers`&emsp;チームメンバーに直接メッセージを送信するためのアクセス許可が必要

アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは、更新されたアプリを初めて実行したときに同意プロセスを繰り返すようになります。 詳細については[、「アプリの更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)」を参照してください。

## <a name="devicepermissions"></a>devicePermissions

**省略可能**文字列の配列

アプリがアクセスを要求することができる、ユーザーのデバイスのネイティブ機能を指定します。 オプションは次のとおりです。

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**省略可能**(記載個所に**必要な**場合を除く)

アプリが Teams クライアント内で読み込むことが想定されている web サイトの有効なドメインの一覧。 ドメインリストには、たとえば`*.example.com`、ワイルドカードを含めることができます。 これは、1つのドメインのセグメントに一致します。に一致`a.b.example.com`させる必要がある`*.*.example.com`場合は、を使用します。 タブ構成またはコンテンツ UI が他のドメインに移動する必要がある場合 (タブの構成に使用するものを除く)、そのドメインをここで指定する必要があります。

ただし、アプリでサポートする id プロバイダーのドメインを含める必要は**ありません**。 たとえば、Google ID を使用して認証するには、accounts.google.com にリダイレクトする必要がありますが、に`validDomains[]`accounts.google.com を含めることはできません。

自分の sharepoint Url が適切に機能する必要がある Teams アプリは、有効なドメインリストに "{teamsitedomain}" を含めることができます。

> [!IMPORTANT]
> 直接に、またはワイルドカードを使用して、コントロールの外部にあるドメインを追加しないでください。 たとえば、は`yourapp.onmicrosoft.com`有効`*.onmicrosoft.com`ですが、有効ではありません。

Object は、型`string`のすべての要素を含む配列です。

## <a name="webapplicationinfo"></a>webApplicationInfo

**Optional**

Aad アプリ ID とグラフ情報を指定して、ユーザーが AAD アプリにシームレスにサインインできるようにします。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|String|36文字|✔|アプリの AAD アプリケーション id。 この id は GUID である必要があります。|
|`resource`|String|2048 文字|✔|SSO の認証トークンを取得するためのアプリのリソース url。|
