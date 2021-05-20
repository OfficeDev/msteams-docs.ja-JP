---
title: メッセージング拡張機能を使用した検索
description: 検索ベースのメッセージング拡張機能の開発方法について説明します。
keywords: チーム メッセージング拡張機能のメッセージング拡張機能の検索
ms.topic: how-to
localization_priority: Normal
ms.date: 07/20/2019
ms.openlocfilehash: 515472838ff2ad35ef5dd295043ec27c53edb4f1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566732"
---
# <a name="search-with-messaging-extensions"></a>メッセージング拡張機能を使用した検索

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

検索ベースのメッセージング拡張機能を使用すると、サービスにクエリを実行し、その情報をカード形式でメッセージに送信できます。

![メッセージング拡張カードの例](~/assets/images/compose-extensions/ceexample.png)

次のセクションでは、この方法について説明します。

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a>検索の種類のメッセージの拡張子

検索ベースのメッセージング拡張機能のパラメーターを `type` `query` に設定します。 以下は、単一の検索コマンドを持つマニフェストの例です。 1 つのメッセージング拡張機能には、最大 10 個の異なるコマンドを関連付けることができます。 これには、複数の検索と複数のアクション ベースのコマンドの両方を含めることができます。

#### <a name="complete-app-manifest-example"></a>完全なアプリ マニフェストの例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.bing",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://bingbotservice.azurewebsites.net/",
    "privacyUrl": "http://bingbotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://bingbotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "Bing",
    "full": "Bing"
  },
  "description": {
    "short": "Find Bing search results",
    "full": "Find Bing search results and share them with your team members."
  },
  "icons": {
    "outline": "bing-outline.jpg",
    "color": "bing-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "bingbotservice.azurewebsites.net",
    "*.bingbotservice.azurewebsites.net"
  ]
}
```

### <a name="test-via-uploading"></a>アップロードによるテスト

アプリをアップロードして、メッセージング拡張機能をテストできます。

メッセージング拡張機能を開くには、チャットまたはチャネルのいずれかに移動します。 作成ボックスの [ **その他のオプション** ] (**&#8943;**) を選択し、メッセージング拡張機能を選択します。

## <a name="add-event-handlers"></a>イベント ハンドラーの追加

ほとんどの作業には `onQuery` 、メッセージング拡張機能ウィンドウ内のすべての対話を処理するイベントが含まれます。

`canUpdateConfiguration`マニフェストで に設定 `true` した場合は、メッセージング拡張機能の **設定** メニュー項目を有効にし、 および を処理する必要があります `onQuerySettingsUrl` `onSettingsUpdate` 。

### <a name="handle-onquery-events"></a>クエリ イベントの処理

メッセージング拡張機能は、メッセージング `onQuery` 拡張機能ウィンドウで何かが発生するか、ウィンドウに送信されたときにイベントを受信します。

メッセージング拡張機能が構成ページを使用する場合、ハンドラー `onQuery` は最初に格納されている構成情報をチェックする必要があります `config` 。 構成ページからの応答も によって処理されます。 `onQuery` 唯一の例外は、構成ページが ハンドラによって呼び出される場合です `onQuerySettingsUrl` 。

メッセージング拡張機能で認証が必要な場合は、ユーザー状態情報を確認します。ユーザーがサインインしていない場合は、このトピックの後半にある [「認証](#authentication) 」の手順に従ってください。

次に、設定されているかどうかを確認 `initialRun` し、設定されている場合は、指示や応答のリストを提供するなど、適切なアクションを実行します。

ハンドラーの残りの部分では `onQuery` 、ユーザーに情報を求めるプロンプトが表示され、プレビュー カードの一覧が表示され、ユーザーが選択したカードが返されます。

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>イベントを処理します。

`onQuerySettingsUrl`イベントと イベントが `onSettingsUpdate` 連携して **、設定** メニュー項目を有効にします。

![メニュー項目の場所設定スクリーンショット](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

ハンドラーは `onQuerySettingsUrl` 構成ページの URL を返し、構成ページが閉じた後、 `onSettingsUpdate` 返された状態を受け入れて保存するためのハンドラー。 これは、 `onQuery` 構成ページからの応答を受信 *しない* 1 つのケースです。

## <a name="receive-and-respond-to-queries"></a>クエリの受信と応答

メッセージング拡張機能へのすべての要求は、コールバック URL `Activity` にポストされるオブジェクトを介して行われます。 要求には、ID やパラメーター値など、ユーザー コマンドに関する情報が含まれています。 また、ユーザー ID やチャネル ID、チーム ID など、拡張機能が呼び出されたコンテキストに関するメタデータも提供されます。

### <a name="receive-user-requests"></a>ユーザー要求の受信

ユーザーがクエリを実行すると、Microsoft Teamsはサービスに標準 Bot Framework オブジェクトを送信 `Activity` します。 サービスは、 `Activity` `type` 次の表に `invoke` `name` 示すように、サポートされている型に設定された に対して `composeExtension` 、そのロジックを実行する必要があります。

標準のボット アクティビティ プロパティに加えて、ペイロードには次の要求メタデータが含まれます。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。にする必要があります `invoke` 。 |
|`name`| サービスに対して発行されるコマンドのタイプ。 現在、次のタイプがサポートされています。 <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求Azure Active Directory送信したユーザーのオブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.channel.id`| チャネル ID (要求がチャネルで行われた場合)。 |
|`channelData.team.id`| チーム ID (要求がチャネルで行われた場合)。 |
|`clientInfo`|ユーザーのメッセージを送信するために使用されるクライアント ソフトウェアに関するオプションのメタデータ。 エンティティには、次の 2 つのプロパティを含めることができます。<br>`country`フィールドには、ユーザーが検出した場所が含まれます。<br>`platform`このフィールドは、メッセージング・クライアント・プラットフォームを記述します。 <br>詳細については、「[非 IRI エンティティ型 - clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)」を *参照* してください。|

要求パラメーター自体は、次のプロパティを含む value オブジェクトにあります。

| プロパティ名 | 用途 |
|---|---|
| `commandId` | アプリ マニフェストで宣言されているコマンドの 1 つと一致する、ユーザーが呼び出したコマンドの名前。 |
| `parameters` | パラメーターの配列: 各パラメーター オブジェクトには、ユーザーが指定したパラメーター値とパラメーター名が含まれます。 |
| `queryOptions` | ページ調整パラメータ: <br>`skip`: このクエリのスキップ数 <br>`count`: 返す要素の数 |

#### <a name="request-example"></a>要求の例

```json
{
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  "type": "invoke",
  "timestamp": "2017-05-01T15:45:51.876Z",
  "localTimestamp": "2017-05-01T08:45:51.876-07:00",
  "id": "f:622749630322482883",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
    "name": "Larry Jin",
    "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
  },
  "conversation": {
    "id": "19:skypespaces_8198cfe0dd2647ae91930f0974768a40@thread.skype"
  },
  "recipient": {
    "id": "28:b4922ea1-5315-4fd0-9b21-d941ab06e39f",
    "name": "TheComposeExtensionDev"
  },
  "entities": [
    {
    "type": "clientInfo",
      "country": "US",
      "platform": "Windows"
    }
  ]
}
```

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>作成メッセージ ボックスに挿入されたリンクからの要求を受信する

外部サービスを検索する代わりに、作成メッセージ ボックスに挿入された URL を使用して、サービスにクエリを実行してカードを返すことができます。 下のスクリーンショットでは、ユーザーが、メッセージング拡張機能がカードに解決した Azure DevOps作業項目の URL に貼り付けられています。

![リンクの展開の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

メッセージング拡張機能がリンクをこのように対話できるようにするには、 `messageHandlers` まず、次の例のように、アプリ マニフェストに配列を追加する必要があります。

```json
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
]
```

アプリ マニフェストをリッスンするドメインを追加したら、次の呼び出し要求に [応答](#respond-to-user-requests) するようにボット コードを変更する必要があります。

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

アプリが複数のアイテムを返す場合は、最初のアイテムのみが使用されます。

### <a name="respond-to-user-requests"></a>ユーザーの要求に応答する

ユーザーがクエリを実行すると、Microsoft Teamsはサービスに同期 HTTP 要求を発行します。 その時点で、リクエストに対する HTTP 応答を提供するコードは 5 秒です。 この間、サービスは追加のルックアップ、または要求を処理するために必要なその他のビジネス ロジックを実行できます。

サービスは、ユーザー クエリに一致する結果を返す必要があります。 応答は、HTTP ステータス コード `200 OK` と、次の本文を持つ有効なアプリケーション/json オブジェクトを示す必要があります。

|プロパティ名|用途|
|---|---|
|`composeExtension`|最上位の応答エンベロープ。|
|`composeExtension.type`|応答の種類です。 サポートされている型は次のとおりです。 <br>`result`: 検索結果の一覧を表示します <br>`auth`: ユーザーに認証を求めます <br>`config`: メッセージング拡張機能の設定をユーザーに要求します。 <br>`message`: テキスト形式のメッセージを表示する |
|`composeExtension.attachmentLayout`|添付ファイルのレイアウトを指定します。 タイプの応答に使用 `result` します。 <br>現在、次のタイプがサポートされています。 <br>`list`: サムネイル、タイトル、テキストフィールドを含むカードオブジェクトのリスト <br>`grid`: サムネイル画像のグリッド |
|`composeExtension.attachments`|有効な添付オブジェクトの配列。 タイプの応答に使用 `result` します。 <br>現在、次のタイプがサポートされています。 <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|推奨されるアクション。 型または の応答に `auth` 使用 `config` します。 |
|`composeExtension.text`|表示するメッセージ。 タイプの応答に使用 `message` します。 |

#### <a name="response-card-types-and-previews"></a>応答カードの種類とプレビュー

次の添付ファイルの種類をサポートします。

* [サムネイル カード](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [ヒーロー カード](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365コネクタカード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

詳細については、「概要については [カード](~/task-modules-and-cards/what-are-cards.md) 」を参照してください。

サムネイルとヒーロー カードの種類の使用方法については、「 [カードと](~/task-modules-and-cards/cards/cards-actions.md)カード アクションを追加する」を参照してください。

Office 365 コネクタ カードに関するその他のドキュメントについては[、「Office 365 コネクタ カードの使用](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)」を参照してください。

結果一覧は、各項目のプレビューと共にMicrosoft Teams UI に表示されます。 プレビューは、次の 2 つの方法のいずれかで生成されます。

* `preview`オブジェクト内でプロパティを使用 `attachment` します。 `preview`添付ファイルは、ヒーローカードまたはサムネールカードのみとなります。
* `title`添付ファイルの基本プロパティ `text` 、および プロパティから抽出 `image` されます。 これらのプロパティは、プロパティが `preview` 設定されておらず、これらのプロパティが使用可能な場合にのみ使用されます。

結果リストにアダプティブ カードまたはOffice 365 コネクタ カードのプレビューを表示するには、そのプレビュー プロパティを設定するだけで済みます。結果がすでにヒーローカードまたはサムネイルカードである場合、これは必要ありません。 プレビュー添付ファイルを使用する場合は、ヒーローカードまたはサムネールカードのいずれかでなければなりません。 プレビュー プロパティを指定しないと、カードのプレビューは失敗し、何も表示されません。

#### <a name="response-example"></a>応答の例

この例では、異なるカード形式(Office 365コネクタとアダプティブ)を混在させる 2 つの結果を含む応答を示します。 応答にカード形式を 1 つ使用する必要が生じるでしょうが、 `preview` コレクション内の各要素のプロパティが `attachments` 、前述のように hero またはサムネイル形式でプレビューを明示的に定義する必要がある方法を示します。

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

### <a name="default-query"></a>既定のクエリ

`initialRun`マニフェストで に設定 `true` すると、Microsoft Teamsは、ユーザーが最初にメッセージング拡張機能を開いたときに"既定の" クエリを発行します。 サービスは、事前に設定された結果のセットでこのクエリに応答できます。 これは、最近表示したアイテム、お気に入り、またはユーザー入力に依存しないその他の情報を表示する場合などに役立ちます。

既定のクエリは、通常のユーザー クエリと同じ構造 `initialRun` を持ちますが、文字列値が を持つパラメーターを使用 `true` する場合を除く。

#### <a name="request-example-for-a-default-query"></a>既定のクエリの要求例

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="identify-the-user"></a>ユーザーを識別する

サービスに対するすべての要求には、要求を実行したユーザーの難読化された ID と、ユーザーの表示名とAzure Active Directoryオブジェクト ID が含まれます。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

`id`および `aadObjectId` 値は、認証されたTeamsユーザーの値であることが保証されます。 資格情報またはサービス内のキャッシュされた状態を検索するためのキーとして使用できます。 さらに、各要求には、ユーザーのAzure Active Directoryテナント ID が含まれており、ユーザーの組織を識別するために使用できます。 該当する場合、要求の送信元のチーム ID とチャネル ID も含まれます。

## <a name="authentication"></a>認証

サービスでユーザー認証が必要な場合は、ユーザーがメッセージング拡張機能を使用する前に、ユーザーにサインインする必要があります。 ボットまたはユーザーにサインするタブを作成した場合は、このセクションをよく理解しておく必要があります。

シーケンスは次のとおりです。

1. ユーザーがクエリを発行するか、既定のクエリがサービスに自動的に送信されます。
2. サービスは、ユーザーが最初に認証されたかどうかを、Teamsユーザー ID を検査して確認します。
3. ユーザーが認証されていない場合は、認証 URL を `auth` `openUrl` 含む推奨アクションを含む応答を返します。
4. Microsoft Teamsクライアントは、指定された認証 URL を使用して Web ページをホストするポップアップ ウィンドウを起動します。
5. ユーザーがサインインした後、ウィンドウを閉じ、Teamsクライアントに「認証コード」を送信する必要があります。
6. Teams クライアントは、手順 5 で渡された認証コードを含む、サービスにクエリを再発行します。

サービスは、手順 6 で受信した認証コードが手順 5 の認証コードと一致することを確認する必要があります。 これにより、悪意のあるユーザーがサインイン フローを偽装したり、侵害したりしないようにします。 これは事実上、安全な認証シーケンスを終了するために「ループを閉じる」。

### <a name="respond-with-a-sign-in-action"></a>サインインアクションで応答する

認証されていないユーザーにサインインを求めるには、認証 URL を含む種類の推奨アクション `openUrl` を使用して応答します。

#### <a name="response-example-for-a-sign-in-action"></a>サインインアクションの応答例

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
> サインイン エクスペリエンスをTeamsポップアップでホストするには、URL のドメイン部分がアプリの有効なドメインの一覧に含まれる必要があります。 詳細については、「マニフェスト スキーマ [内の有効なドメイン](~/resources/schema/manifest-schema.md#validdomains) 」を参照してください。

### <a name="start-the-sign-in-flow"></a>サインイン フローを開始する

サインイン エクスペリエンスは応答性が高く、ポップアップ ウィンドウ内に収まる必要があります。 メッセージパッシングを使用する[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)と統合する必要があります。

Microsoft Teams内で実行されている他の埋め込みエクスペリエンスと同様に、ウィンドウ内のコードは、最初に呼び出す必要があります `microsoftTeams.initialize()` 。 コードで OAuth フローを実行する場合は、Teamsユーザー ID をウィンドウに渡し、その ID を OAuth サインイン URL に渡すことができます。

### <a name="complete-the-sign-in-flow"></a>サインイン フローを完了する

サインイン要求が完了し、ページにリダイレクトされると、次の手順を実行する必要があります。

1. セキュリティ コードを生成します。 (これは乱数を指定できます)。このコードは、OAuth 2.0 トークンなどのサインイン フローを通じて取得された資格情報と共に、サービスにキャッシュする必要があります。
2. `microsoftTeams.authentication.notifySuccess`セキュリティ コードを呼び出して渡します。

この時点で、ウィンドウが閉じ、制御がTeams クライアントに渡されます。 クライアントは、プロパティのセキュリティ コードと共に、元のユーザー クエリを再発行できるようになりました `state` 。 コードでは、セキュリティ コードを使用して、以前に保存された資格情報を検索して認証シーケンスを完了し、ユーザー要求を完了できます。

#### <a name="reissued-request-example"></a>再発行された要求の例

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "type": "clientInfo",
        "country": "US",
        "platform": "Web",
        
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="sdk-support"></a>SDK サポート

### <a name="net"></a>.NET

ボット ビルダー SDK for .NET でクエリを受信して処理するには、 `invoke` 受信アクティビティのアクションの種類を確認し、NuGet パッケージ[Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)のヘルパー メソッドを使用して、メッセージング拡張機能アクティビティであるかどうかを判断します。

#### <a name="example-code-in-net"></a>NET のコード例

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
    if (activity.Type == ActivityTypes.Invoke) // Received an invoke
    {
        if (activity.IsComposeExtensionQuery())
        {
            // This is the response object that will get sent back to the messaging extension request.
            ComposeExtensionResponse invokeResponse = null;

            // This helper method gets the query as an object.
            var query = activity.GetComposeExtensionQueryData();

            if (query.CommandId != null && query.Parameters != null && query.Parameters.Count > 0)
            {
                // query.Parameters has the parameters sent by client
                var results = new ComposeExtensionResult()
                {
                    AttachmentLayout = "list",
                    Type = "result",
                    Attachments = new List<ComposeExtensionAttachment>(),
                };
                invokeResponse.ComposeExtension = results;
            }

            // Return the response
            return Request.CreateResponse<ComposeExtensionResponse>(HttpStatusCode.OK, invokeResponse);
        } else
        {
            // Handle other types of Invoke activities here.
        }
    } else {
      // Failure case catch-all.
      var response = Request.CreateResponse(HttpStatusCode.BadRequest);
      response.Content = new StringContent("Invalid request! This API supports only messaging extension requests. Check your query and try again");
      return response;
    }
}
```

### <a name="nodejs"></a>Node.js

#### <a name="example-code-in-nodejs"></a>Node.jsのコード例

```javascript
require('dotenv').config();

import * as restify from 'restify';
import * as builder from 'botbuilder';
import * as teamBuilder from 'botbuilder-teams';

class App {
    run() {
        const server = restify.createServer();
        let teamChatConnector = new teamBuilder.TeamsChatConnector({
            appId: process.env.MICROSOFT_APP_ID,
            appPassword: process.env.MICROSOFT_APP_PASSWORD
        });

        // Command ID must match what's defined in manifest
        teamChatConnector.onQuery('<%= commandId %>',
            (event: builder.IEvent,
            query: teamBuilder.ComposeExtensionQuery,
            callback: (err: Error, result: teamBuilder.IComposeExtensionResponse, statusCode: number) => void) => {
                // Check for initialRun; i.e., when you should return default results
                // if (query.parameters[0].name === 'initialRun') {}

                // Check query.queryOptions.count and query.queryOptions.skip for paging

                // Return auth response
                // let response = teamBuilder.ComposeExtensionResponse.auth().actions([
                //     builder.CardAction.openUrl(null, 'https://authUrl', 'Please sign in')
                // ]).toResponse();

                // Return config response
                // let response = teamBuilder.ComposeExtensionResponse.config().actions([
                //     builder.CardAction.openUrl(null, 'https://configUrl', 'Please sign in')
                // ]).toResponse();

                // Return result response
                let response = teamBuilder.ComposeExtensionResponse.result('list').attachments([
                    new builder.ThumbnailCard()
                        .title('Test thumbnail card')
                        .text('This is a test thumbnail card')
                        .images([new builder.CardImage().url('https://bot-framework.azureedge.net/bot-icons-v1/bot-framework-default-9.png')])
                        .toAttachment()
                ]).toResponse();
                callback(null, response, 200);
            });
        server.post('/api/composeExtension', teamChatConnector.listen());
        server.listen(process.env.PORT, () => console.log(`listening to port:` + process.env.PORT));
    }
}

const app = new App();
app.run();
```

## <a name="see-also"></a>関連項目

[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
