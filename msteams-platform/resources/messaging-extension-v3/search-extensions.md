---
title: メッセージング拡張機能を使用して検索する
description: 検索ベースのメッセージング拡張機能を開発する方法について説明します。
keywords: teams メッセージング拡張機能メッセージング拡張機能の検索
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 07/20/2019
ms.openlocfilehash: ecaa841e6f8870b7e7c9284535082c4ec08112f2
ms.sourcegitcommit: 9bdd930523041377b52dadffbd8cd52a86a047d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2022
ms.locfileid: "62443987"
---
# <a name="search-with-messaging-extensions"></a>メッセージング拡張機能を使用して検索する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

検索ベースのメッセージング拡張機能を使用すると、サービスにクエリを実行し、その情報をカードの形式でメッセージに投稿できます。

![メッセージング拡張機能カードの例](~/assets/images/compose-extensions/ceexample.png)

次のセクションでは、これを行う方法について説明します。

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a>検索の種類のメッセージ拡張機能

検索ベースのメッセージング拡張機能では、パラメーターをに `type` 設定します `query`。 次に、1 つの検索コマンドを使用するマニフェストの例を示します。 1 つのメッセージング拡張機能には、最大 10 種類のコマンドを関連付けできます。 これには、複数の検索と複数のアクション ベースのコマンドの両方が含まれます。

#### <a name="complete-app-manifest-example"></a>アプリ マニフェストの完全な例

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

メッセージング拡張機能をテストするには、アプリをアップロードします。

メッセージング拡張機能を開くには、チャットまたはチャネルに移動します。 作成ボックス **で [その****他**&#8943;] ボタンを選択し、メッセージング拡張機能を選択します。

## <a name="add-event-handlers"></a>イベント ハンドラーの追加

ほとんどの作業にはイベントが含まれる `onQuery` ので、メッセージング拡張機能ウィンドウのすべての操作を処理します。

マニフェストでに設定`canUpdateConfiguration``true`した場合は、メッセージング拡張機能 **設定メニュー項目** を有効にし、およびを処理する必要`onQuerySettingsUrl`があります。`onSettingsUpdate`

### <a name="handle-onquery-events"></a>onQuery イベントの処理

メッセージング拡張機能は、メッセージング拡張機能 `onQuery` ウィンドウで何かが発生した場合、またはウィンドウに送信された場合にイベントを受け取ります。

メッセージング拡張機能で`onQuery``config`構成ページを使用する場合、ハンドラーは最初に格納されている構成情報を確認する必要があります。メッセージング拡張機能が構成されていない場合は、構成ページへのリンクを含む応答を返します。 構成ページからの応答もによって処理 `onQuery`されます。 唯一の例外は、構成ページがハンドラーによって呼び出される場合です。 `onQuerySettingsUrl`次のセクションを参照してください。

メッセージング拡張機能で認証が必要な場合は、ユーザーの状態情報を確認します。ユーザーがサインインしていない場合は、このトピックの「認証 [」セクションの](#authentication) 指示に従います。

次に、設定されているかどうかを `initialRun` 確認します。設定されている場合は、指示や応答の一覧などの適切なアクションを実行します。

ハンドラーの残りの部分では `onQuery` 、ユーザーに情報の入力を求め、プレビュー カードの一覧を表示し、ユーザーが選択したカードを返します。

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>onQuerySettingsUrl イベントと onSettingsUpdate イベントの処理

イベント`onQuerySettingsUrl`とイベント`onSettingsUpdate`が一緒に機能して **、設定を** 有効にできます。

![メニュー項目の場所設定スクリーンショット](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

構成ページの `onQuerySettingsUrl` URL `onSettingsUpdate` を返すハンドラー。構成ページが閉じると、返された状態を受け入れて保存します。 これは、構成ページから応答`onQuery`*を* 受信しない 1 つのケースです。

## <a name="receive-and-respond-to-queries"></a>クエリの受信と応答

メッセージング拡張機能へのすべての要求は、コールバック URL に `Activity` 投稿されるオブジェクトを介して行われます。 要求には、ID やパラメーター値など、ユーザー コマンドに関する情報が含まれます。 この要求では、ユーザー ID やテナント ID など、拡張機能が呼び出されたコンテキストに関するメタデータと、チャット ID やチャネル ID、チーム ID も提供されます。

### <a name="receive-user-requests"></a>ユーザー要求の受信

ユーザーがクエリを実行すると、Microsoft Teams標準的な Bot Framework オブジェクトが送信`Activity`されます。 サービスは、次の`Activity` `name` `type` `invoke` `composeExtension`表に示すように、サポートされている型に設定されているロジックを実行する必要があります。

標準のボット アクティビティ プロパティに加えて、ペイロードには次の要求メタデータが含まれます。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。する必要があります `invoke`。 |
|`name`| サービスに発行されるコマンドの種類。 現在、次の種類がサポートされています。 <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| Microsoft Azure Active Directory送信Azure ADのオブジェクト ID を指定します。 |
|`channelData.tenant.id`| Microsoft Azure Active Directory (Azure AD) テナント ID。 |
|`channelData.channel.id`| チャネル ID (チャネルで要求が行われた場合)。 |
|`channelData.team.id`| チーム ID (チャネルで要求が行われた場合)。 |
|`clientInfo`|ユーザーのメッセージの送信に使用されるクライアント ソフトウェアに関するオプションのメタデータ。 エンティティには、次の 2 つのプロパティを含めることができます。<br>フィールド `country` には、ユーザーの検出された場所が含まれる。<br>このフィールド `platform` は、メッセージング クライアント プラットフォームについて説明します。 <br>詳細については、「[Non-IRI エンティティ型 — clientInfo」を参照してください](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)。|

要求パラメーター自体は、次のプロパティを含む value オブジェクトに含まれています。

| プロパティ名 | 用途 |
|---|---|
| `commandId` | アプリ マニフェストで宣言されているコマンドの 1 つと一致する、ユーザーによって呼び出されるコマンドの名前。 |
| `parameters` | パラメーターの配列: 各パラメーター オブジェクトには、ユーザーが指定したパラメーター値と共に、パラメーター名が含まれます。 |
| `queryOptions` | ページネーション パラメーター: <br>`skip`: このクエリのスキップ カウント <br>`count`: 返す要素の数 |

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

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>作成メッセージ ボックスに挿入されたリンクから要求を受信する

外部サービスの検索に代わる (または追加) として、作成メッセージ ボックスに挿入された URL を使用してサービスにクエリを実行し、カードを返します。 下のスクリーンショットでは、ユーザーがメッセージング拡張機能がカードに解決したAzure DevOpsワーク アイテムの URL に貼り付けます。

![リンクの分岐解除の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

メッセージング拡張機能でリンク `messageHandlers` を操作するには、次の例のように、まず配列をアプリ マニフェストに追加する必要があります。

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

アプリ マニフェストをリッスンするドメインを追加したら、ボット コードを変更して、以下の呼び出し要求に応答する[](#respond-to-user-requests)必要があります。

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

アプリが複数のアイテムを返す場合は、最初のアイテムだけが使用されます。

### <a name="respond-to-user-requests"></a>ユーザー要求に応答する

ユーザーがクエリを実行すると、Microsoft Teamsに同期 HTTP 要求が発行されます。 その時点で、要求に対する HTTP 応答を提供する 5 秒のコードがあります。 この間、サービスは追加の参照、または要求を処理するために必要なその他のビジネス ロジックを実行できます。

サービスは、ユーザー クエリに一致する結果で応答する必要があります。 応答は、HTTP 状態コードと、 `200 OK` 次の本文を持つ有効な application/json オブジェクトを示す必要があります。

|プロパティ名|用途|
|---|---|
|`composeExtension`|トップ レベルの応答エンベロープ。|
|`composeExtension.type`|応答の種類。 次の種類がサポートされています。 <br>`result`: 検索結果の一覧を表示します。 <br>`auth`: ユーザーに認証を求める <br>`config`: メッセージング拡張機能のセットアップをユーザーに求める <br>`message`: テキスト形式のメッセージを表示する |
|`composeExtension.attachmentLayout`|添付ファイルのレイアウトを指定します。 型の応答に使用されます `result`。 <br>現在、次の種類がサポートされています。 <br>`list`: サムネイル、タイトル、およびテキスト フィールドを含むカード オブジェクトのリスト <br>`grid`: サムネイル画像のグリッド |
|`composeExtension.attachments`|有効な添付ファイル オブジェクトの配列。 型の応答に使用されます `result`。 <br>現在、次の種類がサポートされています。 <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|推奨されるアクション。 型または . の応答に `auth` 使用されます `config`。 |
|`composeExtension.text`|表示するメッセージ。 型の応答に使用されます `message`。 |

#### <a name="response-card-types-and-previews"></a>応答カードの種類とプレビュー

次の添付ファイルの種類がサポートされています。

* [サムネイル カード](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [ヒーロー カード](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 コネクタ カード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

詳細については、「カードの [概要」](~/task-modules-and-cards/what-are-cards.md) を参照してください。

サムネイルカードとヒーロー カードの種類を使用する方法については、「Add [card and card actions」を参照してください](~/task-modules-and-cards/cards/cards-actions.md)。

コネクタ カードの詳細については、「Office 365コネクタ カードの[使用Office 365参照してください](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。

結果リストは、各アイテムのプレビュー Microsoft Teams UI に表示されます。 プレビューは、次の 2 つの方法で生成されます。

* オブジェクト内の `preview` プロパティを使用 `attachment` する。 添付 `preview` ファイルには、ヒーロー カードまたはサムネイル カードのみを指定できます。
* 添付ファイルの基本 、 `title`および `text`プロパティ `image` から抽出されます。 これらは、プロパティが設定されていない場合 `preview` にのみ使用され、これらのプロパティを使用できます。

プレビュー プロパティを設定するだけで、アダプティブ コネクタ カードまたは Office 365 Connector カードのプレビューを結果リストに表示できます。結果が既にヒーロー カードまたはサムネイル カードである場合、これは必要ありません。 プレビュー添付ファイルを使用する場合は、ヒーロー カードまたはサムネイル カードである必要があります。 preview プロパティを指定しない場合、カードのプレビューは失敗し、何も表示されません。

#### <a name="response-example"></a>応答の例

次の使用例は、2 つの結果を持つ応答を示し、異なるカード形式 (コネクタとアダプティブOffice 365混在しています。 応答で `preview` `attachments` 1 つのカード形式に固執する場合は、コレクション内の各要素のプロパティが、前述のようにヒーロー形式またはサムネイル形式でプレビューを明示的に定義する必要がある方法を示しています。

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

マニフェストで設定`initialRun`した`true`場合、Microsoft Teamsが最初にメッセージング拡張機能を開くと、"既定" クエリが発行されます。 サービスは、事前に設定された結果のセットでこのクエリに応答できます。 これは、最近表示されたアイテム、お気に入り、またはユーザー入力に依存しないその他の情報を表示する場合に便利です。

既定のクエリは、文字列 `initialRun` 値が . を持つパラメーターを除き、通常のユーザー クエリと同じ構造を持っています `true`。

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

サービスへのすべての要求には、要求を実行したユーザーの難読化された ID と、ユーザーの表示名と Microsoft Azure Active Directory (Azure AD) オブジェクト ID が含まれます。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

値`id`と`aadObjectId`値は、認証されたユーザーの値Teamsされます。 資格情報またはサービス内のキャッシュされた状態を参照するためのキーとして使用できます。 さらに、各要求には、ユーザー Microsoft Azure Active Directory (Azure AD) テナント ID が含まれているので、ユーザーの組織を識別するために使用できます。 該当する場合、要求には、要求の発信元であるチームとチャネルの ID も含まれる。

## <a name="authentication"></a>認証

サービスでユーザー認証が必要な場合は、メッセージング拡張機能を使用する前にユーザーにサインインする必要があります。 ユーザーにサインインするボットまたはタブを記述している場合は、このセクションをよく理解している必要があります。

シーケンスは次のとおりです。

1. ユーザーがクエリを発行するか、既定のクエリがサービスに自動的に送信されます。
2. サービスは、ユーザーが最初にユーザー ID を調Teamsチェックします。
3. ユーザーが認証されていない場合は、`auth``openUrl`認証 URL を含む推奨されるアクションを含む応答を返します。
4. クライアントMicrosoft Teams、指定した認証 URL を使用して Web ページをホストするポップアップ ウィンドウを起動します。
5. ユーザーがサインインした後、ウィンドウを閉じて、"認証コード" をクライアントにTeamsします。
6. 次Teamsクライアントは、手順 5 で渡された認証コードを含むクエリをサービスに再発行します。

サービスは、手順 6 で受信した認証コードが手順 5 の認証コードと一致することを確認する必要があります。 これにより、悪意のあるユーザーがサインイン フローのスプーフィングや侵害を試みない。 これにより、効果的に "ループを閉じる" と、セキュリティで保護された認証シーケンスが完了します。

### <a name="respond-with-a-sign-in-action"></a>サインイン アクションで応答する

認証されていないユーザーに `openUrl` サインインを求めるメッセージを表示するには、認証 URL を含む種類の推奨されるアクションで応答します。

#### <a name="response-example-for-a-sign-in-action"></a>サインイン アクションの応答例

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
> サインイン エクスペリエンスを Teams ポップアップでホストするには、URL のドメイン部分がアプリの有効なドメインの一覧にある必要があります。 詳細については、マニフェスト [スキーマの validDomains](~/resources/schema/manifest-schema.md#validdomains) を参照してください。

### <a name="start-the-sign-in-flow"></a>サインイン フローを開始する

サインイン エクスペリエンスは応答性が高く、ポップアップ ウィンドウ内に収まる必要があります。 メッセージの受け渡しを[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) と統合する必要があります。

他の埋め込みエクスペリエンスが Microsoft Teamsで実行されている場合と同様に、ウィンドウ内のコードは最初に呼び出す必要があります`microsoftTeams.initialize()`。 コードで OAuth フローを実行する場合は、Teams ユーザー ID をウィンドウに渡し、OAuth サインイン URL に渡します。

### <a name="complete-the-sign-in-flow"></a>サインイン フローを完了する

サインイン要求が完了し、ページにリダイレクトすると、次の手順を実行する必要があります。

1. セキュリティ コードを生成します。 (ランダムな数値を指定できます)。このコードは、OAuth 2.0 トークンなどのサインイン フローで取得した資格情報と共に、サービスにキャッシュする必要があります。
2. セキュリティ コード `microsoftTeams.authentication.notifySuccess` を呼び出して渡します。

この時点で、ウィンドウが閉じ、コントロールがクライアントにTeamsされます。 クライアントは、プロパティのセキュリティ コードと共に、元のユーザー クエリを再発行 `state` できます。 コードでは、セキュリティ コードを使用して、以前に格納された資格情報を参照して認証シーケンスを完了し、ユーザー要求を完了できます。

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

## <a name="sdk-support"></a>SDK のサポート

### <a name="net"></a>.NET

.NET `invoke` 用ボット ビルダー SDK を使用してクエリを受信および処理するには、受信アクティビティのアクションの種類を確認し、NuGet パッケージ [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) のヘルパー メソッドを使用して、メッセージング拡張機能アクティビティかどうかを判断できます。

#### <a name="example-code-in-net"></a>.NET のコード例

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

#### <a name="example-code-in-nodejs"></a>コードの例 (Node.js

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

[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
