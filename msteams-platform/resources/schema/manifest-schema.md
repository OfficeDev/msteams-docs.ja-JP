---
title: マニフェスト スキーマの参照
description: Microsoft Teams のマニフェスト スキーマについて説明します
ms.topic: reference
ms.author: lajanuar
ms.localizationpriority: high
keywords: teams マニフェスト スキーマ
ms.openlocfilehash: 14f1bdaa546fd18612e9869efc2f1216c1aef8db
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453769"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a>参照: Microsoft Teams のマニフェスト スキーマ

Teams マニフェストは、アプリが Microsoft Teams 製品にどのように統合されるかを説明します。 マニフェストは、[`https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json) でホストされているスキーマに準拠している必要があります。 以前のバージョン 1.0、1.1、... 1.12 もサポートされています (URL で "v1.x" を使用)。
各バージョンで行われた変更の詳細については、[マニフェスト変更ログ](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)を参照してください。

次のスキーマ サンプルは、すべての拡張オプションを示しています。

## <a name="sample-full-manifest"></a>完全なマニフェストのサンプル

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json",
    "manifestVersion": "1.12",
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
            "context": [
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
            "context": [
                "personalTab",
                "channelTab"
            ],
            "name": "Display name of tab",
            "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
            "websiteUrl": "https://contoso.com/content (displayed in web browser)",
            "searchUrl": "https://contoso.com/content (displayed in web browser)"
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

省略可能 (ただし推奨されます) — 文字列

マニフェストの JSON スキーマを参照する https:// URL。

## <a name="manifestversion"></a>manifestVersion

**必須** — 文字列

このマニフェストが使用しているマニフェスト スキーマのバージョン。

## <a name="version"></a>version

**必須** — 文字列

特定のアプリのバージョン。 マニフェストで何かを更新する場合は、バージョンもインクリメントする必要があります。 このように、新しいマニフェストがインストールされると、既存のマニフェストが上書きされ、ユーザーは新しい機能を受け取ります。 このアプリがストアに送信されたら、新しいマニフェストを再送信して再検証する必要があります。 アプリのユーザーは、マニフェストが承認されてから数時間以内に、新しく更新されたマニフェストを自動的に受け取ります。

アプリが権限の変更を要求した場合、ユーザーはアプリをアップグレードして再承認するよう求められます。

このバージョン文字列は、[semver](http://semver.org/) 標準 (MAJOR.MINOR.PATCH) に従う必要があります。

## <a name="id"></a>id

**必須** — Microsoft アプリ ID

ID は、Microsoft が生成したアプリの一意の識別子です。 ボットが Microsoft Bot Framework を介して登録されている場合は、ID があります。 タブの Web アプリが既に Microsoft にサインインしている場合は、ID があります。 ここに ID を入力する必要があります。 それ以外の場合は、[Microsoft アプリケーション登録ポータル](https://aka.ms/appregistrations)で新しい ID を生成する必要があります。 ボットを追加する場合は、同じ ID を使用してください。

> [!NOTE]
> AppSource で既存のアプリに更新を送信する場合は、マニフェストの ID を変更しないでください。

## <a name="developer"></a>developer

**必須**— オブジェクト

会社に関する情報を指定します。 Teams ストアに送信されるアプリの場合、これらの値はストア リストの情報と一致する必要があります。 詳細については、[Teams ストアの公開ガイドライン](~/concepts/deploy-and-publish/appsource/publish.md)を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`name`|32 文字|✔|開発者の表示名。|
|`websiteUrl`|2048 文字|✔|開発者の Web サイトの The https:// URL。 このリンクは、ユーザーを会社または製品固有のランディング ページに移動する必要があります。|
|`privacyUrl`|2048 文字|✔|開発者のプライバシー ポリシーの https:// URL。|
|`termsOfUseUrl`|2048 文字|✔|開発者の使用条件の https:// URL。|
|`mpnId`|10 文字| |**省略可能** アプリを構築しているパートナー組織を識別するMicrosoft パートナー ネットワーク ID。|

## <a name="name"></a>name

**必須**— オブジェクト

Teams エクスペリエンスでユーザーに表示されるアプリ エクスペリエンスの名前。 AppSource に送信されるアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。 `short` と `full` の値は異なっている必要があります。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|30 文字|✔|アプリの短い表示名。|
|`full`|100 文字||アプリのフル ネーム。アプリのフル ネームが 30 文字を超える場合に使用されます。|

## <a name="description"></a>description

**必須**— オブジェクト

ユーザーに、アプリについて説明します。AppSource に送信されたアプリの場合、これらの値は AppSource エントリの情報と一致する必要があります。

説明があなたの経験をについて述べており、潜在的な顧客があなたの経験が何をするかを理解するのに役立つことを確認してください。 外部アカウントを使用する必要がある場合は、完全な説明にするよう気を配る必要があります。 `short` と `full` の値は異なっている必要があります。 短い説明を長い説明の中で繰り返すことはできません。また、他のアプリ名を含めることはできません。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`short`|80 文字|✔|スペースが限られている場合に使用される、アプリ エクスペリエンスの簡単な説明。|
|`full`|4,000 文字|✔|アプリの完全な説明。|

## <a name="packagename"></a>packageName

**省略可能** — 文字列

逆引きドメイン表記でのアプリの一意識別子。たとえば、com.example.myapp などです。最大長: 64 文字。

## <a name="localizationinfo"></a>localizationInfo

**省略可能** — オブジェクト

既定の言語の指定を許可し、より多くの言語ファイルへのポインターを提供します。詳細については、「[ローカライズ](~/concepts/build-and-test/apps-localization.md)」を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`defaultLanguageTag`||✔|このトップ レベルのマニフェスト ファイル内の文字列の言語タグ。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

より多くの言語翻訳を指定するオブジェクトの配列。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`languageTag`||✔|提供されたファイルの文字列の言語タグ。|
|`file`||✔|翻訳された文字列を含む .json ファイルへの相対ファイル パス。|

## <a name="icons"></a>アイコン

**必須**— オブジェクト

Teams アプリ内で使用されるアイコン。 アイコン ファイルは、アップロード パッケージの一部として含まれている必要があります。 詳細については、[アイコン](../../concepts/build-and-test/apps-package.md#app-icons)を参照してください。

|名前| 最大サイズ | 必須 | 説明|
|---|---|---|---|
|`outline`|32 x 32 ピクセル|✔|透明な 32x32 PNG アウトライン アイコンへの相対ファイル パス。|
|`color`|192 x 192 ピクセル|✔|フル カラーの 192x192 PNG アイコンへの相対ファイル パス。|

## <a name="accentcolor"></a>accentColor

**必須** — HTML の 16 進数カラー コード

アウトライン アイコンの背景として使用する色。

値は、'#' で始まる有効な HTML カラー コードである必要があります (例; `#4464ee`)。

## <a name="configurabletabs"></a>configurableTabs

**省略可能** — 配列

アプリ エクスペリエンスにチーム チャネル タブ エクスペリエンスがあり、追加する前に追加の構成が必要な場合に使用されます。 構成可能なタブは、`team` スコープおよび `groupchat` スコープでのみサポートされており、同じタブを複数回構成できます。 ただし、マニフェストで定義できるのは 1 回のみです。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 文字|✔|タブを構成するときに使用する https:// URL。|
|`scopes`|列挙型の配列|1|✔|現在、構成可能なタブは、`team` スコープと `groupchat` スコープのみをサポートしています。 |
|`canUpdateConfiguration`|ブール値|||作成後にユーザーがタブの構成のインスタンスを更新できるかどうかを示す値。既定値: **true**。|
|`context` |列挙型の配列|6 ||[タブがサポートされている](../../tabs/how-to/access-teams-context.md) `contextItem` スコープのセット。 既定値: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**。|
|`sharePointPreviewImage`|string|2048||SharePoint で使用するタブ プレビュー イメージへの相対ファイル パス。サイズ 1024 x 768。 |
|`supportedSharePointHosts`|列挙型の配列|1||SharePoint でタブを使用できるようにする方法を定義します。オプションは `sharePointFullPage` と `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**省略可能** — 配列

ユーザーが手動で追加せずに、既定で "ピン留め" できるタブのセットを定義します。 `personal` スコープで宣言された静的タブは、常にアプリの個人的なエクスペリエンスに固定されます。 `team` スコープで宣言された静的タブは現在サポートされていません。

このアイテムは、型 `object` のすべての要素を持つ配列 (最大 16 要素) です。 このブロックは、静的タブ ソリューションを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`entityId`|string|64 文字|✔|タブが表示されるエンティティの一意の識別子。|
|`name`|string|128 文字|✔|チャネル インターフェイスのタブの表示名。|
|`contentUrl`|string||✔|Teams キャンバスに表示されるエンティティ UI を指す https:// URL。|
|`websiteUrl`|string|||ユーザーがブラウザでの表示を選択した場合に示す https:// URL。|
|`searchUrl`|string|||ユーザーの検索クエリを指すhttps:// URL。|
|`scopes`|列挙型の配列|1|✔|現在、静的タブは `personal` スコープのみをサポートしています。つまり、個人的なエクスペリエンスの一部としてのみプロビジョニングできます。|
|`context` | 列挙型の配列| 2|| タブがサポートされている `contextItem` 個のスコープのセット。|

> [!NOTE]
> サードパーティの開発者は searchUrl 機能を使用できません。関連するコンテンツを表示したり、認証フローを開始したりするために、タブにコンテキスト依存の情報が必要な場合は、「 [Microsoft Teams タブのコンテキストを取得する](../../tabs/how-to/access-teams-context.md)」を参照してください。

## <a name="bots"></a>ボット

**省略可能** — 配列

既定のコマンド プロパティなどのオプション情報とともに、ボット ソリューションを定義します。

アイテムは、型 `object` のすべての要素を含む配列 (最大で 1 つの要素&mdash;のみ、現在アプリごとに 1 つのボットのみが許可されています) です。 このブロックは、ボット エクスペリエンスを提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|string|64 文字|✔|Bot Framework に登録された、ボット用の一意の Microsoft アプリ ID。 ID は、全体的な[アプリ ID](#id) と同じにすることができます。|
|`scopes`|列挙型の配列|3|✔|ボットがエクスペリエンスを提供するのは、`team` 内のチャネルのコンテキスでなのか、グループ チャット (`groupchat`) でなのか、あるいは個別のユーザーのみをエクスペリエンスの対象にする (`personal`) のかを指定します。これらのオプションは非排他的です。|
|`needsChannelSelector`|ブール値|||ボットがユーザー ヒントを使用してボットを特定のチャネルに追加するかどうかを説明します。既定値: **`false`**|
|`isNotificationOnly`|Boolean|||ボットが会話ボットではなく、一方向の通知専用ボットであるかどうかを示します。既定値: **`false`**|
|`supportsFiles`|Boolean|||ボットが個人用チャットでファイルをアップロード/ダウンロードできるかどうかを示します。既定値: **`false`**|
|`supportsCalling`|ブール値|||ボットが音声通話をサポートしている場所を示す値。 **重要**: このプロパティは現在実験中です。 実験的なプロパティは完全ではない可能性があり、完全に利用可能になる前に変更される可能性があります。  このプロパティは、テストと探索の目的でのみ提供されており、本番アプリケーションで使用することはできません。 既定値: **`false`**|
|`supportsVideo`|Boolean|||ボットがビデオ通話をサポートしている場所を示す値。 **重要**: このプロパティは現在実験中です。 実験的なプロパティは完全ではない可能性があり、完全に利用可能になる前に変更される可能性があります。  このプロパティは、テストと探索の目的でのみ提供されており、本番アプリケーションで使用することはできません。 既定値: **`false`**|

### <a name="botscommandlists"></a>bots.commandLists

ボットがユーザーに推奨できるコマンドのオプションの一覧。 オブジェクトは、型 `object` のすべての要素を持つ配列 (最大 2 つの要素) です。 ボットがサポートするスコープごとに個別のコマンド リストを定義する必要があります。 詳細については、「[ボット メニュー](~/bots/how-to/create-a-bot-commands-menu.md)」を参照してください。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`items.scopes`|列挙型の配列|3|✔|コマンド リストが有効なスコープを指定します。オプションは、 `team`、 `personal`、および `groupchat`です。|
|`items.commands`|オブジェクトの配列|10|✔|ボットがサポートするコマンドの配列:<br>`title`: ボット コマンドの名前 (文字列、32)<br>`description`: コマンド構文とその引数 (文字列、128) の簡単な説明または例。|

### <a name="botscommandlistscommands"></a>bots.commandLists.command

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|title|string|12 |✔|ボット コマンド名。|
|description|string|128 文字|✔|簡単なテキストの説明またはコマンド構文とその引数の例。|

## <a name="connectors"></a>コネクタ

**省略可能** — 配列

`connectors` ブロックは、アプリの Office 365 コネクタを定義します。

オブジェクトは、型`object`のすべての要素を持つ配列 (最大 1 つの要素) です。 このブロックは、Connector を提供するソリューションにのみ必要です。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 文字|✔|コネクタを構成するときに使用する https:// URL。|
|`scopes`|列挙型の配列|1|✔|コネクタが `team`のチャネルのコンテキストでエクスペリエンスを提供するか、個々のユーザーのみを対象としたエクスペリエンスを提供するかを指定します (`personal`)。現時点では、 `team` スコープのみがサポートされています。|
|`connectorId`|string|64 文字|✔|[コネクタ開発者ダッシュボード](https://aka.ms/connectorsdashboard)の ID に一致するコネクタの一意の識別子です。|

## <a name="composeextensions"></a>composeExtensions

**省略可能** — 配列

アプリのメッセージング拡張機能を定義します。

> [!NOTE]
> 機能の名前は、2017 年 11 月に "作成拡張機能" から "メッセージング拡張機能" に変更されましたが、マニフェスト名は同じままであるため、既存の拡張機能は引き続き機能します。

アイテムは、型 `object` のすべての要素を持つ配列 (最大 1 つの要素) です。 このブロックは、メッセージング拡張機能を提供するソリューションにのみ必要です。

|名前| 種類 | 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`botId`|string|64|✔|ボット フレームワークに登録されている、メッセージング拡張機能をサポートするボットの一意の Microsoft アプリ ID。 ID は、全体のアプリ ID と同じにできます。|
|`commands`|オブジェクトの配列|10|✔|メッセージング拡張機能がサポートするコマンドの配列。|
|`canUpdateConfiguration`|Boolean|||メッセージング拡張機能の構成をユーザーが更新できるかどうかを示す値。既定値: **false** です。|
|`messageHandlers`|オブジェクトの配列|5||特定の条件が満たされた場合にアプリを呼び出すことができるハンドラーの一覧。|
|`messageHandlers.type`|string|||メッセージ ハンドラーの種類。`"link"`でなければなりません。|
|`messageHandlers.value.domains`|文字列の配列|||リンク メッセージ ハンドラーが登録できるドメインの配列。|

### <a name="composeextensionscommands"></a>composeExtensions.commands

メッセージング拡張機能では、最大 10 のコマンドで 1 つ以上のコマンドを宣言する必要があります。 各コマンドは、UI ベースのエントリ ポイントからの潜在的な相互作用として Microsoft Teams に表示されます。

各コマンド 項目は、次の構造を持つオブジェクトです。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|string|64 文字|✔|コマンドの ID。|
|`title`|string|32 文字|✔|ユーザーフレンドリーなコマンド名。|
|`type`|string|64 文字||コマンドの種類。 `query` または `action` のいずれか。 既定: **クエリ**|
|`description`|string|128 文字||このコマンドの目的を示すためにユーザーに表示される説明。|
|`initialRun`|Boolean|||ブール値は、コマンドがパラメーターなしで最初に実行されるかどうかを示します。既定値は **false** です。|
|`context`|文字列の配列|3||メッセージ拡張機能の呼び出し先を定義します。 `compose`、`commandBox`、`message` の任意の組み合わせ。 既定値は `["compose","commandBox"]` です。|
|`fetchTask`|Boolean|||タスク モジュールを動的にフェッチする必要があるかどうかを示すブール値。既定値は **false** です。|
|`taskInfo`|object|||メッセージング拡張コマンドを使用するときにプリロードするタスク モジュールを指定します。|
|`taskInfo.title`|string|64 文字||最初のダイアログ タイトル。|
|`taskInfo.width`|string|||ダイアログの幅 - ピクセル単位の数値、または '大'、'中'、'小' などの既定のレイアウト。|
|`taskInfo.height`|string|||ダイアログの高さ - ピクセル単位の数値、または '大'、'中'、'小' などの既定のレイアウト。|
|`taskInfo.url`|string|||初期 Web ビュー URL。|
|`parameters`|オブジェクトの配列|5 個の項目|✔|コマンドが取得するパラメーターの一覧。 最小: 1; 最大: 5。|
|`parameters.name`|string|64 文字|✔|クライアントに表示されるパラメーターの名前。パラメーター名はユーザー要求に含まれます。|
|`parameters.title`|string|32 文字|✔|パラメーターのユーザーフレンドリーなタイトル。|
|`parameters.description`|string|128 文字||このパラメーターの目的を説明するユーザーフレンドリーな文字列。|
|`parameters.value`|string|512 文字||パラメーターの初期値。 現在、値はサポートされていません|
|`parameters.inputType`|string|128 文字||`fetchTask: true` のタスク モジュールに表示されるコントロールの種類を定義します。`text, textarea, number, date, time, toggle, choiceset`の 1 つ。|
|`parameters.choices`|オブジェクトの配列|10 個||`choiceset` の選択オプションです。 `parameter.inputType` が `choiceset` である場合にのみ使用してください。|
|`parameters.choices.title`|string|128 文字|✔|選択したタイトル。|
|`parameters.choices.value`|string|512 文字|✔|Value of the choice.|

## <a name="permissions"></a>アクセス許可

**省略可能** —文字列の配列

`string`の配列。アプリが要求するアクセス許可を指定します。これにより、拡張機能の動作がエンド ユーザーに通知されます。次のオプションは非排他的です。

* `identity`&emsp; にはユーザー ID 情報が必要です。
* `messageTeamMembers`&emsp; にはチーム メンバーに直接メッセージを送信するためのアクセス許可が必要です。

アプリの更新中にこれらのアクセス許可を変更すると、ユーザーは更新されたアプリを実行した後に同意プロセスを繰り返します。詳細については、「 [アプリの更新](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)」を参照してください。

## <a name="devicepermissions"></a>devicePermissions

**省略可能** —文字列の配列

アプリがアクセスを要求するユーザーのデバイス上のネイティブ機能を提供します。オプションは次のとおりです。

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**省略可能** です。ただし **、必須の** 場合は省略可能です。

アプリが Teams クライアント内にロードすることを予測する Web サイトの有効なドメインのリスト。 ドメイン リストには、`*.example.com` などのワイルドカードを含めることができます。 有効なドメインは、ドメインの 1 つのセグメントと正確に一致します。 `a.b.example.com` と一致させる必要がある場合は、`*.*.example.com` を使用してください。 タブ構成またはコンテンツ UI がタブ構成以外のドメインに移動する場合は、そのドメインをここで指定する必要があります。

サポートする ID プロバイダーのドメインをアプリに含め **ない** でください。 たとえば、Google ID を使用して認証するには、accounts.google.com にリダイレクトする必要がありますが、`validDomains[]` に accounts.google.com を含めないでください。

正常に機能するために独自の SharePoint URL を必要とする Teams アプリでは、有効なドメインリストに "{teamsitedomain}" が含まれています。

> [!IMPORTANT]
> 直接またはワイルドカードを使用して、制御できないドメインを追加しないでください。 たとえば、`yourapp.onmicrosoft.com` は有効ですが、`*.onmicrosoft.com` は無効です。

オブジェクトは、型 `string` のすべての要素を含む配列です。

## <a name="webapplicationinfo"></a>WebApplicationInfo

**省略可能** — オブジェクト

Azure Active Directory アプリ ID と Microsoft Graph 情報を提供して、ユーザーがアプリにシームレスにサインインできるようにします。 アプリが Microsoft Azure Active Directory (Azure AD) に登録されている場合は、アプリ ID を提供する必要があります。 管理者は、Teams 管理センターで権限を簡単に確認して同意を与えることができます。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`id`|string|36 文字|✔|Azure AD のアプリケーション ID を指定します。 この ID は GUID である必要があります。|
|`resource`|string|2048 文字|✔|SSO の認証トークンを取得するためのアプリのリソース URL。 </br> **注:** SSO を使用していない場合は、エラー応答を回避するために、このフィールドにダミーの文字列値 (たとえば、https://notapplicable) をアプリ マニフェストに入力してください。 |

## <a name="showloadingindicator"></a>showLoadingIndicator

**省略可能** — ブール値

アプリまたはタブの読み込み中に読み込みインジケーターを表示するかどうかを示します。既定値は **false** です。
>[!NOTE]
>アプリマニフェストで `showLoadingIndicator` を true として選択した場合、ページを正しく読み込むには、「[ネイティブの読み込みインジケーターを表示する](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)」ドキュメントの説明に従って、タブとタスクモジュールのコンテンツページを変更します。

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
|`type`|string|32 文字|✔|通知の種類。 *以下を参照してください*。|
|`description`|string|128 文字|✔|通知の簡単な説明。 *以下を参照してください*。|
|`templateText`|string|128 文字|✔|例: "あなたに {actor} が作成したタスク {taskId}"|

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

## <a name="configurableproperties"></a>configurableProperties

**オプション** - 配列

`configurableProperties` ブロックは、チーム管理者がカスタマイズできるアプリのプロパティを定義します。 詳細については、「[アプリのカスタマイズを有効にする](~/concepts/design/enable-app-customization.md)」を参照してください。 アプリのカスタマイズ機能は、カスタム アプリまたは LOB アプリではサポートされていません。

> [!NOTE]
> 少なくとも 1 つのプロパティを定義する必要があります。 このブロックでは、最大 9 つのプロパティを定義できます。

次のプロパティを定義できます。

* `name`: アプリの表示名。
* `shortDescription`: アプリの簡単な説明。
* `longDescription`: アプリの長い説明。
* `smallImageUrl`: アプリのアウトライン アイコン。
* `largeImageUrl`: アプリの色アイコン。
* `accentColor`: 使用する色とアウトライン アイコンの背景。
* `developerUrl`: 開発者の Web サイトの HTTPS URL。
* `privacyUrl`: 開発者のプライバシー ポリシーの HTTPS URL。
* `termsOfUseUrl`: 開発者の使用条件の HTTPS URL。

## <a name="defaultblockuntiladminaction"></a>defaultBlockUntilAdminAction

**省略可能** — ブール値

`defaultBlockUntilAdminAction` プロパティ が **true** に 設定されている場合、管理者が許可するまで、アプリは既定でユーザーから非表示になります。 **true** に 設定すると、アプリは、すべてのテナントとエンド ユーザーに対して非表示になります。 テナント管理者は、Teams 管理センターでアプリを確認し、アプリを許可またはブロックするためのアクションを実行できます。 既定値は **false** です。 既定のアプリ ブロックの詳細については、「[管理者が承認するまで Teams アプリを非表示にする](~/concepts/design/enable-app-customization.md#hide-teams-app-until-admin-approves)」を参照してください。

## <a name="publisherdocsurl"></a>publisherDocsUrl

**省略可能** - 文字列

**最大サイズ** - 128 文字

`publisherDocsUrl` は、管理者がアプリを許可する前にガイドラインを取得するための情報ページの HTTPS URL であり、既定ではブロックされています。 また、テナント管理者に役立つ可能性のあるアプリに関する指示や情報を提供するためにも使用できます。

## <a name="subscriptionoffer"></a>subscriptionOffer

**省略可能** - オブジェクト

アプリに関連付けられている SaaS オファーを指定します。

|名前| 型|最大サイズ|必須|説明|
|---|---|---|---|---|
|`offerId`| string | 2,048 文字 | ✔ | パブリッシャー ID とオファー ID を含む一意の識別子。 [パートナー センター](https://partner.microsoft.com/dashboard)で確認できます。文字列は `publisherId.offerId`として書式設定する必要があります。|

## <a name="meetingextensiondefinition"></a>meetingExtensionDefinition

**省略可能** - オブジェクト

会議拡張機能の定義を指定します。詳細については、「[Teamsのカスタム Together Mode シーン](../../apps-in-teams-meetings/teams-together-mode.md)」を参照してください。

|名前| 型| 最大サイズ | 必須 | 説明|
|---|---|---|---|---|
|`scenes`|オブジェクトの配列| 5 個の項目||会議でサポートされているシーン。|

### <a name="meetingextensiondefinitionscenes"></a>meetingExtensionDefinition.scenes

|名前| 型|最大サイズ|必須 |説明|
|---|---|---|---|---|
|`id`|||✔| シーンの一意の識別子。 この ID は GUID である必要があります。 |
|`name`| string | 128 文字 |✔| シーンの名前。 |
|`file`|||✔| シーンの metadata json ファイルへの相対ファイル パス。 |
|`preview`|||✔| シーンの PNG プレビュー アイコンへの相対ファイル パス。 |
|`maxAudience`| integer | 50  |✔| シーンでサポートされている対象ユーザーの最大数。 |
|`seatsReservedForOrganizersOrPresenters`| integer | 50 |✔| 開催者または発表者用に予約されたシートの数。|

## <a name="authorization"></a>承認

**省略可能** — オブジェクト

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
|`type`|string||✔| リソース固有のアクセス許可の種類。オプション: `Application` と `Delegated`。|
|`name`|string|128 文字|✔|リソース固有のアクセス許可の名前。 詳細については、「[リソース固有のアプリケーションのアクセス許可](#resource-specific-application-permissions)」および「[リソース固有の委任されたアクセス許可](#resource-specific-delegated-permissions)」を参照してください|

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

## <a name="see-also"></a>関連項目

* [Microsoft Teams アプリの構造を理解する](~/concepts/design/app-structure.md)
* [アプリのカスタマイズを有効にする](~/concepts/design/enable-app-customization.md)
* [アプリをローカライズする](~/concepts/build-and-test/apps-localization.md)
* [メディア機能を統合する](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Microsoft Teams の開発者向けパブリック プレビュー マニフェスト スキーマ](manifest-schema-dev-preview.md)
