---
title: パブリック開発者プレビュー マニフェスト スキーマ リファレンス
description: Microsoft Teamsでサポートされているすべてのコンポーネントのサンプル マニフェスト ファイルと説明について説明します。
ms.topic: reference
ms.localizationpriority: medium
ms.date: 11/15/2021
ms.openlocfilehash: deaf094ab18ddd2ebe70ea9594f41c108398bf32
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142738"
---
# <a name="reference-public-developer-preview-manifest-schema-for-microsoft-teams"></a>参照: Microsoft Teams のパブリック開発者プレビュー マニフェスト スキーマ

開発者プレビューを有効にする方法については、「[Microsoft Teams のパブリック開発者プレビュー](~/resources/dev-preview/developer-preview-intro.md)」を参照してください。

> [!NOTE]
> [Outlook および Office で Teams の個人用タブやメッセージ拡張機能](../../m365-apps/overview.md)を実行するなどの開発者プレビュー機能を使用していない場合は、代わりに [GA 機能のアプリ マニフェスト](~/resources/schema/manifest-schema.md)を使用します。

Microsoft Teams マニフェストは、アプリが Microsoft Teams プラットフォームにどのように統合されるかを説明します。 マニフェストは、[`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) でホストされているスキーマに準拠している必要があります。

## <a name="sample-full-manifest"></a>完全なマニフェストのサンプル

```json
{
    "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion": "devPreview",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "packageName": "com.example.myapp",
    "devicePermissions": [
        "geolocation",
        "media"
    ],
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
            "scopes": [
                "team",
                "groupchat"
            ]"context": []
        }
    ],
    "staticTabs": [
        {
            "entityId": "idForPage",
            "name": "Display name of tab",
            "contentUrl": "https://contoso.com/content?host=msteams",
            "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
            "websiteUrl": "https://contoso.com/content",
            "scopes": [
                "personal"
            ]
        }
    ],
    "bots": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "needsChannelSelector": false,
            "isNotificationOnly": false,
            "scopes": [
                "team",
                "personal",
                "groupchat"
            ],
            "supportsFiles": true,
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
                            "title": "Command N",
                            "description": "Description of Command N"
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
            "configurationUrl": "https://contoso.com/teamsconnector/configure",
            "scopes": [
                "team"
            ]
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
                    "type": "search",
                    "context": [
                        "compose",
                        "commandBox"
                    ],
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
                    "type": "action",
                    "fetchTask": true,
                    "context": [
                        "message"
                    ],
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
                    "id": "exampleMessageHandler",
                    "title": "Message Handler",
                    "description": "Domains that will create a preview when pasted into the compose box",
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
    ],
    "webApplicationInfo": {
        "id": "AAD App ID",
        "resource": "Resource URL for acquiring auth token for SSO"
    },
    "authorization": {
        "permissions": {
            "resourceSpecific": [
                {
                    "type": "Application",
                    "name": "ChannelSettings.Read.Group"
                },
                {
                    "type": "Delegated",
                    "name": "ChannelMeetingParticipant.Read.Group"
                }
            ]
        }
    },
    "configurableProperties": [
        "name",
        "shortDescription",
        "longDescription",
        "smallImageUrl",
        "largeImageUrl",
        "accentColor",
        "developerUrl",
        "privacyUrl",
        "termsOfUseUrl"
    ],
    "defaultInstallScope": "meetings",
    "defaultGroupCapability": {
        "meetings": "tab",
        "team": "bot",
        "groupchat": "bot"
    },
    "subscriptionOffer": {
        "offerId": "publisherId.offerId"
    },
    "meetingExtensionDefinition": {
        "scenes": [
            {
                "id": "9082c811-7e6a-4174-8173-6ccd57d377e6",
                "name": "Getting started sample",
                "file": "scenes/sceneMetadata.json",
                "preview": "scenes/scenePreview.png",
                "maxAudience": 15,
                "seatsReservedForOrganizersOrPresenters": 0
            },
            {
                "id": "afeaed22-f89b-48e1-98b4-46a514344e4a",
                "name": "Sample-1",
                "file": "scenes/sceneMetadata.json",
                "preview": "scenes/scenePreview.png",
                "maxAudience": 15,
                "seatsReservedForOrganizersOrPresenters": 3
            }
        ]
    }
}
```

スキーマは次のプロパティを定義します。

## <a name="schema"></a>$schema

*省略可能 (ただし推奨されます)* &ndash; 文字列

マニフェストの JSON スキーマを参照する `https://` URL。

## <a name="manifestversion"></a>manifestVersion

**必須** &ndash; 文字列

このマニフェストが使用しているマニフェスト スキーマのバージョン。

## <a name="version"></a>version

**必須** &ndash; 文字列

特定のアプリのバージョン。 マニフェストで何かを更新する場合は、バージョンもインクリメントする必要があります。 このように、新しいマニフェストをインストールすると、既存のマニフェストが上書きされ、ユーザーは新機能を取得します。 このアプリがストアに送信された場合は、新しいマニフェストを再送信して再検証する必要があります。 その後、このアプリのユーザーは、承認された後、数時間後に新しく更新されたマニフェストを自動的に取得します。

アプリに必要なアクセス許可が変更された場合、ユーザーは、アップグレードを行いアプリに再同意するように求められます。

このバージョン文字列は、[semver](http://semver.org/) 標準 (MAJOR.MINOR.PATCH) に従う必要があります。

## <a name="id"></a>id

**必須** &ndash; Microsoft アプリ ID

Microsoft が生成したこのアプリの一意の識別子。 Microsoft Bot Frameworkを介してボットを登録している場合、またはタブの Web アプリが Microsoft に既にサインインしている場合は、ID を既に持っており、ここに入力する必要があります。 それ以外の場合は、Microsoft アプリケーション登録ポータル ([マイ アプリケーション](https://apps.dev.microsoft.com)) で新しい ID を生成し、ここに入力し、ボットを [追加](~/bots/how-to/create-a-bot-for-teams.md)するときに再利用する必要があります。

## <a name="packagename"></a>packageName

**必須** &ndash; 文字列

逆ドメイン表記のこのアプリの一意の識別子。たとえば、com.example.myapp などです。

## <a name="developer"></a>developer

必須:

会社に関する情報を指定します。 AppSource (以前の Office ストア) に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`name`|32 文字|✔️|開発者の表示名。|
|`websiteUrl`|2048 文字|✔️|開発者の Web サイトの The https:// URL。 このリンクは、ユーザーを会社または製品固有のランディング ページに移動する必要があります。|
|`privacyUrl`|2048 文字|✔️|開発者のプライバシー ポリシーの https:// URL。|
|`termsOfUseUrl`|2048 文字|✔️|開発者の使用条件の https:// URL。|
|`mpnId`|10 文字|✔️|**省略可能** アプリを構築しているパートナー組織を識別するMicrosoft パートナー ネットワーク ID。|

## <a name="localizationinfo"></a>localizationInfo

オプション: 

既定の言語の指定と、追加の言語ファイルへのポインターを許可します。 [ローカリゼーション](~/concepts/build-and-test/apps-localization.md)を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`defaultLanguageTag`|4 文字|✔️|このトップ レベルのマニフェスト ファイル内の文字列の言語タグ。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

追加の言語翻訳を指定するオブジェクトの配列。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`languageTag`|4 文字|✔️|提供されたファイルの文字列の言語タグ。|
|`file`|4 文字|✔️|翻訳された文字列を含む .json ファイルへの相対ファイル パス。|

## <a name="name"></a>name

必須:

Teams エクスペリエンスでユーザーに表示されるアプリ エクスペリエンスの名前。 AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。 の値 `short` と `full` 同じにしないでください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|30 文字|✔️|アプリの短い表示名。|
|`full`|100 文字||アプリのフル ネーム。アプリのフル ネームが 30 文字を超える場合に使用されます。|

## <a name="description"></a>description

必須:

ユーザーに、アプリについて説明します。AppSource に送信されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。

説明が、あなたの経験を正確に説明し、潜在的な顧客があなたの経験が何かを理解するのに役立つ情報を提供することを確認してください。 また、完全な説明で、使用に外部アカウントが必要かどうかにも注意する必要があります。 の値 `short` と `full` 同じにしないでください。  短い説明を長い説明の中で繰り返すことはできません。また、他のアプリ名を含めることはできません。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|80 文字|✔️|スペースが限られている場合に使用される、アプリ エクスペリエンスの簡単な説明。|
|`full`|4,000 文字|✔️|アプリの完全な説明。|

## <a name="icons"></a>アイコン

必須:

Teams アプリ内で使用されるアイコン。 アイコン ファイルは、アップロード パッケージの一部として含まれている必要があります。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`outline`|2048 文字|✔️|透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。|
|`color`|2048 文字|✔️|フル カラーの 192x192 PNG アイコンへの相対ファイル パス。|

## <a name="accentcolor"></a>accentColor

**必須** &ndash; 文字列

アウトライン アイコンの背景と共に使用する色。

値は、'#' で始まる有効な HTML カラー コードである必要があります (例; `#4464ee`)。

## <a name="configurabletabs"></a>configurableTabs

オプション: 

アプリ エクスペリエンスに、追加する前に追加の構成が必要なチーム チャネル タブ エクスペリエンスがある場合に使用されます。 構成可能なタブはチーム スコープでのみサポートされており、現在、アプリごとに 1 つのタブのみがサポートされています。

オブジェクトは、型 `object` のすべての要素を含む配列です。 このブロックは、構成可能なチャネル タブ ソリューションを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|String|2048 文字|✔️|タブを構成するときに使用する https:// URL。|
|`canUpdateConfiguration`|ブール値|||作成後にユーザーがタブの構成のインスタンスを更新できるかどうかを示す値。既定値: `true`|
|`scopes`|列挙型の配列|1|✔️|現在、構成可能なタブは、`team` スコープと `groupchat` スコープのみをサポートしています。 |
|`context` |列挙型の配列|6 ||[タブがサポートされている](../../tabs/how-to/access-teams-context.md) `contextItem` スコープのセット。 既定値: `channelTab`, `privateChatTab`, `meetingChatTab`, `meetingDetailsTab`, `meetingSidePanel`, `meetingStage`|
|`sharePointPreviewImage`|String|2048||SharePoint で使用するタブ プレビュー イメージへの相対ファイル パス。サイズ 1024 x 768。 |
|`supportedSharePointHosts`|列挙型の配列|1||SharePoint でタブを使用できるようにする方法を定義します。オプションは `sharePointFullPage` と `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

オプション: 

ユーザーが手動で追加せずに、既定で "ピン留め" できるタブのセットを定義します。 `personal` スコープで宣言された静的タブは、常にアプリの個人的なエクスペリエンスに固定されます。 `team` スコープで宣言された静的タブは現在サポートされていません。

**staticTabs** ブロックで `contentUrl` の代わりに `contentBotId` を指定して、アダプティブ カードを使用してタブをレンダリングします。

オブジェクトは配列で (要素は最大で 16 つ)、`object` タイプのすべての要素が含まれます。 このブロックは、静的タブ ソリューションを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`entityId`|String|64 文字|✔️|タブが表示されるエンティティの一意の識別子。|
|`name`|String|128 文字|✔️|チャネル インターフェイスのタブの表示名。|
|`contentUrl`|String|2048 文字|✔️|Teams キャンバスに表示されるエンティティ UI を指す https:// URL。|
|`contentBotId`|   | | | Bot Framework ポータルでボットに指定された Microsoft Teams アプリ ID。 |
|`websiteUrl`|String|2048 文字||ユーザーがブラウザでの表示を選択した場合に示す https:// URL。|
|`scopes`|列挙型の配列|1|✔️|現在、静的タブは `personal` スコープのみをサポートしています。つまり、個人的なエクスペリエンスの一部としてのみプロビジョニングできます。|

## <a name="bots"></a>ボット

オプション: 

既定のコマンド プロパティなどのオプション情報とともに、ボット ソリューションを定義します。

オブジェクトは、型 `object` のすべての要素を含む配列 (最大で 1 つの要素&mdash;のみ、現在アプリごとに 1 つのボットのみが許可されています) です。 このブロックは、ボット エクスペリエンスを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|String|64 文字|✔️|Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 これは、全体的な[アプリ ID](#id) と同じにすることができます。|
|`needsChannelSelector`|ブール値|||ボットを特定のチャネルに追加するためのユーザー用ヒントをボットで使用するかどうかの説明。既定: `false`|
|`isNotificationOnly`|ブール値|||ボットが会話ボットではなく、一方向の通知専用ボットであるかどうかを示します。既定値: `false`|
|`supportsFiles`|ブール値|||ボットが個人用チャットでファイルをアップロード/ダウンロードできるかどうかを示します。既定値: `false`|
|`scopes`|列挙型の配列|3|✔️|ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。これらのオプションは非排他的です。|

### <a name="botscommandlists"></a>bots.commandLists

ボットがユーザーに推奨できるコマンドのオプションの一覧。 オブジェクトは、型 `object` のすべての要素を持つ配列 (最大 2 つの要素) です。ボットがサポートするスコープごとに個別のコマンド リストを定義する必要があります。 詳細については、「[ボット メニュー](~/bots/how-to/create-a-bot-commands-menu.md)」を参照してください。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`items.scopes`|列挙型の配列|3|✔️|コマンド リストが有効なスコープを指定します。オプションは、 `team`、 `personal`、および `groupchat`です。|
|`items.commands`|オブジェクトの配列|10|✔️|ボットがサポートするコマンドの配列:<br>`title`: ボット コマンドの名前 (文字列、32)。<br>`description`: コマンド構文とその引数 (文字列、128) の簡単な説明または例。|

## <a name="connectors"></a>コネクタ

オプション: 

`connectors` ブロックは、アプリの Office 365 コネクタを定義します。

オブジェクトは配列で (要素は最大で 1 つ)、`object` タイプのすべての要素が含まれます。 このブロックは、Connector を提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|String|2048 文字|✔️|コネクタを構成するときに使用する https:// URL。|
|`connectorId`|String|64 文字|✔️|[コネクタ開発者ダッシュボード](https://aka.ms/connectorsdashboard)の ID に一致するコネクタの一意の識別子です。|
|`scopes`|列挙型の配列|1|✔️|コネクタが `team`のチャネルのコンテキストでエクスペリエンスを提供するか、個々のユーザーのみを対象としたエクスペリエンスを提供するかを指定します (`personal`)。現時点では、 `team` スコープのみがサポートされています。|

## <a name="composeextensions"></a>composeExtensions

オプション: 

アプリのメッセージ拡張機能を定義します。

> [!NOTE]
> 機能の名前は、2017 年 11 月に "作成拡張機能" から "メッセージ拡張機能" に変更されましたが、マニフェスト名は同じままであるため、既存の拡張機能は引き続き機能します。

オブジェクトは配列で (要素は最大で 1 つ)、`object` タイプのすべての要素が含まれます。 このブロックは、メッセージ拡張機能を提供するソリューションにのみ必要です。

|名前| 種類 | 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|String|64|✔️|ボット フレームワークに登録されている、メッセージ拡張機能をサポートするボットの一意の Microsoft アプリ ID。 これは、全体的な[アプリ ID](#id) と同じにすることができます。|
|`canUpdateConfiguration`|ブール値|||メッセージ拡張機能の構成をユーザーが更新できるかどうかを示す値。既定は `false` です。|
|`commands`|オブジェクトの配列|10|✔️|メッセージ拡張機能がサポートするコマンドの配列|

### <a name="composeextensionscommands"></a>composeExtensions.commands

メッセージ拡張機能は、1 つ以上のコマンドを宣言する必要があります。 各コマンドは、UI ベースのエントリ ポイントからの潜在的な相互作用として Microsoft Teams に表示されます。 最大 10 個のコマンドがあります。

各コマンド 項目は、次の構造を持つオブジェクトです。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|String|64 文字|✔️|コマンドの ID。|
|`type`|String|64 文字||コマンドの種類。 `query` または `action` のいずれか。 既定: `query`|
|`title`|String|32 文字|✔️|ユーザーフレンドリーなコマンド名。|
|`description`|String|128 文字||このコマンドの目的を示すためにユーザーに表示される説明。|
|`initialRun`|Boolean|||コマンドをパラメーターなしで最初に実行する必要があるかどうかを示すブール値。 既定: `false`|
|`context`|文字列 (String) の配列|3||メッセージ拡張機能の呼び出し先を定義します。 `compose`、`commandBox`、`message` の任意の組み合わせ。 既定値は `["compose", "commandBox"]` です|
|`fetchTask`|ブール値|||タスク モジュールを動的にフェッチする必要があるかどうかを示すブール値。|
|`taskInfo`|オブジェクト|||メッセージ拡張コマンドを使用するときにプリロードするタスク モジュールを指定します。|
|`taskInfo.title`|String|64||最初のダイアログ タイトル。|
|`taskInfo.width`|String|||ダイアログの幅 - ピクセル単位の数値、または '大'、'中'、'小' などの既定のレイアウト。|
|`taskInfo.height`|String|||ダイアログの高さ - ピクセル単位の数値、または '大'、'中'、'小' などの既定のレイアウト。|
|`taskInfo.url`|String|||初期 Web ビュー URL。|
|`messageHandlers`|オブジェクトの配列|5||特定の条件が満たされた場合にアプリを呼び出すことができるハンドラーの一覧。ドメインは `validDomains` にも一覧表示されている必要があります。|
|`messageHandlers.type`|String|||メッセージ ハンドラーの種類。`"link"`でなければなりません。|
|`messageHandlers.value.domains`|文字列 (String) の配列|||リンク メッセージ ハンドラーが登録できるドメインの配列。|
|`parameters`|オブジェクトの配列|5|✔️|コマンドが取得するパラメーターの一覧。 最小: 1; 最大: 5|
|`parameter.name`|String|64 文字|✔️|クライアントに表示されるパラメーターの名前。これはユーザーの要求に含まれています。|
|`parameter.title`|String|32 文字|✔️|パラメーターのユーザーフレンドリーなタイトル。|
|`parameter.description`|String|128 文字||このパラメーターの目的を説明するユーザーフレンドリーな文字列。|
|`parameter.inputType`|String|128 文字||`fetchTask: true` のタスク モジュールに表示されるコントロールの型を定義します。 `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset` の 1 つ。|
|`parameter.choices`|オブジェクトの配列|10||`choiceset` の選択オプション。 `parameter.inputType` が `choiceset` である場合にのみ使用してください。|
|`parameter.choices.title`|String|128||選択したタイトル。|
|`parameter.choices.value`|String|512||Value of the choice.|

## <a name="permissions"></a>アクセス許可

オプション: 

アプリが要求するアクセス許可を指定する配列 `string`。拡張機能の実行方法をエンド ユーザーに知らせます。 次のオプションは、非排他的です。

* `identity`&emsp; にはユーザー ID 情報が必要です。
* `messageTeamMembers`&emsp; にはチーム メンバーに直接メッセージを送信するためのアクセス許可が必要です。

アプリを更新するときにこれらのアクセス許可を変更すると、ユーザーは更新されたアプリを初めて実行するときに同意プロセスを繰り返すことになります。

## <a name="devicepermissions"></a>devicePermissions

**省略可能** 文字列の配列

アプリがアクセスを要求する可能性のあるユーザーのデバイス上のネイティブ機能を指定します。オプションは次のとおりです。

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**省略可能**、特に明記されている場合は **必須** を除く

アプリがコンテンツの読み込みを期待する有効なドメインのリスト。 ドメイン リストには、`*.example.com` などのワイルドカードを含めることができます。 これは、ドメインの 1 つのセグメントと正確に一致します。`a.b.example.com` と一致させる必要がある場合は、`*.*.example.com` を使用してください。 タブ構成またはコンテンツ UI が、タブ構成に使用するドメイン以外のドメインに移動する必要がある場合は、そのドメインをここで指定する必要があります。

ただし、サポートする ID プロバイダーのドメインをアプリに含める必要は **ありません**。 たとえば、Google ID を使用して認証を行うには、accounts.google.com にリダイレクトする必要がありますが、accounts.google.com `validDomains[]`を含めてはなりません。

> [!IMPORTANT]
> 直接またはワイルドカードを使用して、制御できないドメインを追加しないでください。 たとえば、`yourapp.onmicrosoft.com` は有効ですが、`*.onmicrosoft.com` は無効です。

オブジェクトは、型 `string` のすべての要素を含む配列です。

## <a name="webapplicationinfo"></a>WebApplicationInfo

オプション: 

ユーザーが Azure AD アプリにシームレスにサインインできるように、Microsoft Azure Active Directory (Azure AD) アプリ ID とGraph情報を指定します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|String|36 文字|✔️|アプリの Microsoft Azure Active Directory (Azure AD) アプリケーション ID。 この ID は GUID である必要があります。|
|`resource`|String|2048 文字|✔️|SSO の認証トークンを取得するためのアプリのリソース URL。|
|`applicationPermissions`|配列|最大 100 アイテム|✔️|アプリケーションのリソースのアクセス許可。|

## <a name="graphconnector"></a>graphConnector

**省略可能** — オブジェクト

アプリの Graph コネクタ構成を指定します。 これが存在する場合は [、webApplicationInfo.id](#webapplicationinfo) も指定する必要があります。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`notificationUrl`|string|2048 文字|✔️|アプリケーションの Graph コネクタ通知を送信する URL。|

## <a name="showloadingindicator"></a>showLoadingIndicator

**省略可能** — ブール値

アプリまたはタブの読み込み中に読み込みインジケーターを表示するかどうかを示します。 既定値は **false** です。
> [!NOTE]
> アプリマニフェストで `showLoadingIndicator` を true として選択した場合、ページを正しく読み込むには、「[ネイティブの読み込みインジケーターを表示する](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)」ドキュメントの説明に従って、タブとタスクモジュールのコンテンツページを変更します。

## <a name="isfullscreen"></a>IsFullScreen

 **省略可能** — ブール値

タブ ヘッダー バーの有無にかかわらず、個人用アプリがレンダリングされる場所を示します。既定値は **false** です。

> [!NOTE]
> `isFullScreen` は、組織に発行されたアプリでのみ機能します。

## <a name="activities"></a>activities

**省略可能** — オブジェクト

アプリがユーザー アクティビティ フィードを投稿するために使用するプロパティを定義します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`activityTypes`|オブジェクトの配列|128 項目| | アプリがユーザーのアクティビティ フィードに投稿できるアクティビティの種類を提供します。|

### <a name="activitiesactivitytypes"></a>activity.activityTypes

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`type`|string|32 文字|✔️|通知の種類。 *以下を参照してください*。|
|`description`|string|128 文字|✔️|通知の簡単な説明。 *以下を参照してください*。|
|`templateText`|string|128 文字|✔️|例: "あなたに {actor} が作成したタスク {taskId}"|

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

## <a name="configurableproperties"></a>configurableProperties

**オプション** - 配列

`configurableProperties` ブロックは、チーム管理者がカスタマイズできるアプリのプロパティを定義します。 詳細については、「[アプリのカスタマイズを有効にする](~/concepts/design/enable-app-customization.md)」を参照してください。

> [!NOTE]
> 少なくとも 1 つのプロパティを定義する必要があります。 このブロックでは、最大 9 つのプロパティを定義できます。

次のプロパティを定義できます。

* `name`: アプリの表示名。
* `shortDescription`: アプリの簡単な説明。
* `longDescription`: アプリの詳細な説明。
* `smallImageUrl`: アプリのアウトライン アイコン。
* `largeImageUrl`: アプリの色アイコン。
* `accentColor`: アウトライン アイコンの背景と共に使用する色。
* `developerUrl`: 開発者の Web サイトの HTTPS URL。
* `privacyUrl`: 開発者のプライバシー ポリシーの HTTPS URL。
* `termsOfUseUrl`: 開発者の使用条件の HTTPS URL。

## <a name="defaultinstallscope"></a>defaultInstallScope

**省略可能** - 文字列

このアプリに既定で定義されているインストール スコープを指定します。 定義されたスコープは、ユーザーがアプリを追加しようとしたときにボタンに表示されるオプションになります。 オプションは、次のとおりです。

* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

**省略可能** - オブジェクト

グループのインストール スコープを選択すると、ユーザーがアプリをインストールするときに既定の機能が定義されます。オプションは次のとおりです。

* `team`
* `groupchat`
* `meetings`

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`team`|string|||選択したインストール スコープが `team`の場合、このフィールドは使用可能な既定の機能を指定します。オプション: `tab`、 `bot`、または `connector`。|
|`groupchat`|文字列|||選択したインストール スコープが `groupchat`の場合、このフィールドは使用可能な既定の機能を指定します。オプション: `tab`、 `bot`、または `connector`。|
|`meetings`|文字列|||選択したインストール スコープが `meetings`の場合、このフィールドは使用可能な既定の機能を指定します。オプション: `tab`、 `bot`、または `connector`。|

## <a name="subscriptionoffer"></a>subscriptionOffer

**省略可能** - オブジェクト

アプリに関連付けられている SaaS オファーを指定します。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`offerId`| string | 2,048 文字 | ✔️ | パブリッシャー ID とオファー ID を含む一意の識別子。 [パートナー センター](https://partner.microsoft.com/dashboard)で確認できます。文字列は `publisherId.offerId`として書式設定する必要があります。|

## <a name="meetingextensiondefinition"></a>meetingExtensionDefinition

**省略可能** - オブジェクト

会議拡張機能の定義を指定します。詳細については、「[Teamsのカスタム Together Mode シーン](../../apps-in-teams-meetings/teams-together-mode.md)」を参照してください。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`scenes`|オブジェクトの配列| 5 個の項目||会議でサポートされているシーン。|

### <a name="meetingextensiondefinitionscenes"></a>meetingExtensionDefinition.scenes

|名前| 型|最大サイズ|必須 |説明|
|---|---|---|---|---|
|`id`|||✔️| シーンの一意の識別子。 この ID は GUID である必要があります。 |
|`name`| string | 128 文字 |✔️| シーンの名前。 |
|`file`|||✔️| シーンの metadata json ファイルへの相対ファイル パス。 |
|`preview`|||✔️| シーンの PNG プレビュー アイコンへの相対ファイル パス。 |
|`maxAudience`| integer | 50  |✔️| シーンでサポートされている対象ユーザーの最大数。 |
|`seatsReservedForOrganizersOrPresenters`| integer | 50 |✔️| 開催者または発表者用に予約されたシートの数。|

## <a name="authorization"></a>承認

**省略可能** - オブジェクト

アプリの承認に関する情報を指定して統合します。

|名前| 型|最大サイズ|必須 |説明|
|---|---|---|---|---|
|`permissions`||||アプリを実行する必要があるアクセス許可の一覧。|

### <a name="authorizationpermissions"></a>authorization.permissions

|名前| 型|最大サイズ|必須 |説明|
|---|---|---|---|---|
|`resourceSpecific`| オブジェクトの配列|16 項目||リソース インスタンス レベルでのデータ アクセスを保護するアクセス許可。|

### <a name="authorizationpermissionsresourcespecific"></a>authorization.permissions.resourceSpecific

|名前| 型|最大サイズ|必須 |説明|
|---|---|---|---|---|
|`type`|string||✔️| リソース固有のアクセス許可の種類。オプション: `Application` と `Delegated`。|
|`name`|string|128 文字|✔️|リソース固有のアクセス許可の名前。 詳細については、「[リソース固有のアプリケーションのアクセス許可](#resource-specific-application-permissions)」および「[リソース固有の委任されたアクセス許可](#resource-specific-delegated-permissions)」を参照してください|

#### <a name="resource-specific-application-permissions"></a>リソース固有のアプリケーションのアクセス許可

アプリケーションのアクセス許可により、アプリはサインインしたユーザーなしでデータにアクセスできます。 アプリケーションのアクセス許可については、「[MS Graph および MS BotSDK のリソース固有の同意](../../graph-api/rsc/resource-specific-consent.md)」を参照してください。

#### <a name="resource-specific-delegated-permissions"></a>リソース固有の委任されたアクセス許可

委任されたアクセス許可を使用すると、アプリはサインインしているユーザーの代わりにデータにアクセスできます。

* **チームのリソース固有の委任されたアクセス許可**

    |**[名前]**|**説明**|
    |---|---|
    |`ChannelMeetingParticipant.Read.Group`| サインインしたユーザーの代理で、このチームに関連付けられたチャネル会議の名前、役割、ID、参加時間と退会時間などの参加者情報を読み取ることができるようにします。|
    |`InAppPurchase.Allow.Group`| サインインしているユーザーの代わりに、このチームのユーザーにマーケットプレース オファーを表示し、アプリ内での購入を完了できるようにします。|
    |`ChannelMeetingStage.Write.Group`| サインインしているユーザーの代わりに、このチームに関連付けられているチャネル会議の会議ステージにコンテンツをアプリが表示できるようにします。|

* **チャットまたは会議用のリソース固有の委任されたアクセス許可**

    |**[名前]**|**説明**|
    |---|---|
    |`InAppPurchase.Allow.Chat`|サインインしているユーザーの代わりに、このチャットや関連する任意の会議のユーザーにマーケットプレース オファーを表示し、アプリ内での購入を完了できるようにします。|
    |`MeetingStage.Write.Chat`|サインインしているユーザーの代わりに、このチャットに関連付けられている会議の会議ステージにコンテンツをアプリが表示できるようにします。|
    |`OnlineMeetingParticipant.Read.Chat`|サインインしたユーザーの代理で、このチャットに関連付けられた会議の名前、役割、ID、参加時間と退会時間などの参加者情報を読み取ることができるようにします。|
    |`OnlineMeetingParticipant.ToggleIncomingAudio.Chat`|サインインしているユーザーの代わりに、このチャットに関連付けられている会議の参加者の着信オーディオをアプリで切り替えられるようにします。|

* **ユーザーのリソース固有の委任されたアクセス許可**

    |**[名前]**|**説明**|
    |---|---|
    |`InAppPurchase.Allow.User`|サインインしているユーザーの代わりに、アプリでユーザー マーケットプレース オファーを表示し、アプリ内でユーザーの購入を完了できるようにします。|

* **Teamsライブ共有に対するリソース固有のアクセス許可**

   |名前| 説明 |
   | ----- | ----- |
   |`LiveShareSession.ReadWrite.Chat`|<!--- need info --->|
   |`LiveShareSession.ReadWrite.Channel`|<!--- need info --->|
   |`MeetingStage.Write.Chat`|<!--- need info --->|
   |`OnlineMeetingIncomingAudio.Detect.Chat`|<!--- need info --->|

## <a name="see-also"></a>関連項目

* [Microsoft Teams アプリの構造を理解する](~/concepts/design/app-structure.md)
* [アプリのカスタマイズを有効にする](~/concepts/design/enable-app-customization.md)
* [アプリをローカライズする](~/concepts/build-and-test/apps-localization.md)
* [メディア機能を統合する](~/concepts/device-capabilities/media-capabilities.md)
