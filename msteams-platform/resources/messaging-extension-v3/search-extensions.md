---
title: メッセージ拡張機能を使用して検索する
description: この記事では、検索ベースのメッセージ拡張機能を開発する方法について説明します
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 07/20/2019
ms.openlocfilehash: 20dbc7c5a65ee44f3b40eda29a20d6d37e8a81f0
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190015"
---
# <a name="search-with-message-extensions"></a>メッセージ拡張機能を使用して検索する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

検索ベースのメッセージ拡張機能を使用すると、サービスに対してクエリを実行し、その情報をカードの形式でメッセージに直接投稿できます。

![メッセージ拡張カードの例](~/assets/images/compose-extensions/ceexample.png)

次のセクションでは、これを行う方法について説明します。

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

## <a name="search-type-message-extensions"></a>検索の種類のメッセージ拡張機能

検索ベースのメッセージ拡張機能の場合は、パラメーター`query`を `type` . 1 つの検索コマンドを使用したマニフェストの例を次に示します。 1 つのメッセージ拡張機能に、最大 10 個の異なるコマンドを関連付けることができます。 これには、複数の検索コマンドと複数のアクション ベースのコマンドの両方を含めることができます。

### <a name="complete-app-manifest-example"></a>完全なアプリ マニフェストの例

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

## <a name="test-via-uploading"></a>アップロードによるテスト

アプリをアップロードすることで、メッセージ拡張機能をテストできます。

メッセージ拡張機能を開くには、任意のチャットまたはチャネルに移動します。 作成ボックスの **[その他のオプション** (**&#8943;**)] ボタンを選択し、メッセージ拡張機能を選択します。

## <a name="add-event-handlers"></a>イベント ハンドラーを追加する

ほとんどの作業には、メッセージ拡張ウィンドウ内のすべての対話を処理するイベントが含 `onQuery` まれます。

マニフェストで設定`canUpdateConfiguration``true`した場合は、メッセージ拡張機能の設定メニュー項目を有効にし、処理と`onSettingsUpdate`処理も行う`onQuerySettingsUrl`必要があります。

## <a name="handle-onquery-events"></a>onQuery イベントを処理する

メッセージ拡張機能は、 `onQuery` メッセージ拡張機能ウィンドウで何かが発生するか、ウィンドウに送信されたときにイベントを受け取ります。

メッセージ拡張機能で構成ページが使用されている場合は、ハンドラー `onQuery` で保存されている構成情報を最初に確認する必要があります。メッセージ拡張機能が構成されていない場合は、構成ページへのリンクを含む応答を返します `config` 。 構成ページからの応答も `onQuery`、 . 唯一の例外は、構成ページがハンドラー `onQuerySettingsUrl`によって呼び出される場合です。次のセクションを参照してください。

メッセージ拡張機能で認証が必要な場合は、ユーザー状態情報を確認します。 ユーザーがサインインしていない場合は、このトピックの後半の「 [認証](#authentication) 」セクションの手順に従います。

次に、設定されているかどうかを `initialRun` 確認します。設定されている場合は、指示や応答の一覧の提供など、適切なアクションを実行します。

ハンドラー `onQuery` の残りの部分では、ユーザーに情報の入力を求め、プレビュー カードの一覧を表示し、ユーザーが選択したカードを返します。

## <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>onQuerySettingsUrl イベントと onSettingsUpdate イベントを処理する

イベントと`onSettingsUpdate`イベントは`onQuerySettingsUrl`連携して **、設定** メニュー項目を有効にします。

![設定メニュー項目の場所のスクリーンショット](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

ハンドラーは `onQuerySettingsUrl` 構成ページの URL を返します。構成ページが閉じた後、返 `onSettingsUpdate` された状態を受け入れて保存します。 これは、構成ページから応答を受け取 *らない* ケース`onQuery`です。

## <a name="receive-and-respond-to-queries"></a>クエリの受信と応答

メッセージ拡張機能に対するすべての要求は、コールバック URL にポストされるオブジェクトを介して `Activity` 行われます。 要求には、ID やパラメーター値など、ユーザー コマンドに関する情報が含まれています。 また、この要求には、チャット ID やチャネル ID、チーム ID など、拡張機能が呼び出されたコンテキストに関するメタデータも提供されます。

### <a name="receive-user-requests"></a>ユーザー要求を受信する

ユーザーがクエリを実行すると、サービスに標準の Bot Framework `Activity` オブジェクトが送信Microsoft Teams。 次の表に示すように、サービスは`type`、サポートされている型に`invoke`設定および`name`設定されている`composeExtension`ロジック`Activity`を実行する必要があります。

標準のボット アクティビティ プロパティに加えて、ペイロードには次の要求メタデータが含まれています。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。を指定する `invoke`必要があります。 |
|`name`| サービスに対して発行されるコマンドの種類。 現在、次の種類がサポートされています。 <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーのMicrosoft Azure Active Directory (Azure AD) オブジェクト ID。 |
|`channelData.tenant.id`| Microsoft Azure Active Directory (Azure AD) テナント ID。 |
|`channelData.channel.id`| チャネル ID (要求がチャネルで行われた場合)。 |
|`channelData.team.id`| チーム ID (要求がチャネルで行われた場合)。 |
|`clientInfo`|ユーザーのメッセージの送信に使用されるクライアント ソフトウェアに関する省略可能なメタデータ。 エンティティには、次の 2 つのプロパティを含めることができます。<br>`country`このフィールドには、ユーザーの検出された場所が含まれます。<br>このフィールドでは `platform` 、メッセージング クライアント プラットフォームについて説明します。 <br>詳細については、「[IRI 以外のエンティティの種類 - clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)*」を参照してください*。|

要求パラメーターは value オブジェクトにあります。これには、次のプロパティが含まれます。

| プロパティ名 | 用途 |
|---|---|
| `commandId` | アプリ マニフェストで宣言されているコマンドの 1 つに一致する、ユーザーによって呼び出されるコマンドの名前。 |
| `parameters` | パラメーターの配列: 各パラメーター オブジェクトには、パラメーター名と、ユーザーが指定したパラメーター値が含まれます。 |
| `queryOptions` | ページ分割パラメーター: <br>`skip`: このクエリのカウントをスキップする <br>`count`: 返される要素の数 |

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

外部サービスを検索する代わりに 、メッセージの作成ボックスに挿入された URL を使用して、サービスにクエリを実行し、カードを返すことができます。 下のスクリーンショットでは、メッセージ拡張機能がカードに解決されたAzure DevOpsの作業項目の URL にユーザーが貼り付けています。

![リンク展開の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

メッセージ拡張機能でこの方法でリンクを操作できるようにするには、次の例のように、まずアプリ マニフェストに配列を追加 `messageHandlers` する必要があります。

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

### <a name="respond-to-user-requests"></a>ユーザー要求に応答する

ユーザーがクエリを実行すると、Teamsサービスに同期 HTTP 要求が発行されます。 この間、コードは要求に対する HTTP 応答を提供するために 5 秒かかります。 この間、サービスは追加のルックアップ、または要求の処理に必要なその他のビジネス ロジックを実行できます。

サービスは、ユーザー クエリと一致する結果で応答する必要があります。 応答は、HTTP 状態コードと、次の `200 OK` 本文を持つ有効な application/json オブジェクトを示す必要があります。

|プロパティ名|用途|
|---|---|
|`composeExtension`|最上位レベルの応答エンベロープ。|
|`composeExtension.type`|応答の種類。 次の種類がサポートされています。 <br>`result`: 検索結果の一覧を表示します <br>`auth`: ユーザーに認証を求めるメッセージを表示します <br>`config`: ユーザーにメッセージ拡張機能の設定を求めるメッセージを表示します <br>`message`: テキスト形式のメッセージを表示する |
|`composeExtension.attachmentLayout`|添付ファイルのレイアウトを指定します。 型の応答に使用されます `result`。 <br>現在、次の種類がサポートされています。 <br>`list`: サムネイル、タイトル、テキスト フィールドを含むカード オブジェクトの一覧 <br>`grid`: サムネイル 画像のグリッド |
|`composeExtension.attachments`|有効な添付ファイル オブジェクトの配列。 型の応答に使用されます `result`。 <br>現在、次の種類がサポートされています。 <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|推奨されるアクション。 型 `auth` または `config`. |
|`composeExtension.text`|表示するメッセージ。 型の応答に使用されます `message`。 |

#### <a name="response-card-types-and-previews"></a>応答カードの種類とプレビュー

次の添付ファイルの種類がサポートされています。

* [サムネイル カード](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [ヒーロー カード](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 コネクタ カード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [アダプティブ カード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

詳細については、「 [カード](~/task-modules-and-cards/what-are-cards.md) 」を参照してください。

サムネイルカードとヒーロー カードの種類を使用する方法については、「 [カードとカードアクションを追加](~/task-modules-and-cards/cards/cards-actions.md)する」を参照してください。

Office 365 コネクタ カードに関するその他のドキュメントについては、「[Office 365 コネクタ カードの使用](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)」を参照してください。

結果の一覧がMicrosoft Teams UI に表示され、各項目のプレビューが表示されます。 プレビューは、次の 2 つの方法のいずれかで生成されます。

* オブジェクト内の `preview` プロパティを `attachment` 使用します。 添付ファイルは `preview` 、ヒーロー カードまたはサムネイル カードにのみ使用できます。
* 添付ファイルの基本 `title`プロパティ `text`、プロパティ `image` から抽出されます。 これらは、プロパティが設定されておらず、 `preview` これらのプロパティが使用可能な場合にのみ使用されます。

アダプティブ コネクタ カードまたはOffice 365 コネクタ カードのプレビューは、プレビュー プロパティを設定するだけで結果一覧に表示できます。 これは、結果が既にヒーロー カードまたはサムネイル カードである場合は必要ありません。 プレビュー添付ファイルを使用する場合は、ヒーロー カードまたはサムネイル カードである必要があります。 プレビュー プロパティが指定されていない場合、カードのプレビューは失敗し、何も表示されません。

#### <a name="response-example"></a>応答の例

次の例は、2 つの結果を含む応答を示しています。カード形式は異なります。Office 365 コネクタとアダプティブです。 応答で 1 つのカード形式を使用したい場合がありますが、コレクション内の各要素のプロパティで`attachments`、前述のようにヒーロー形式またはサムネイル形式でプレビューを明示的に定義する方法`preview`を示します。

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

マニフェストに設定`initialRun`した場合、ユーザーが最初に`true`メッセージ拡張機能を開いたときに、Microsoft Teamsは "既定の" クエリを発行します。 サービスは、事前設定された結果のセットを使用して、このクエリに応答できます。 これは、最近表示されたアイテム、お気に入り、またはユーザー入力に依存しないその他の情報を表示する場合に便利です。

既定のクエリは、文字列値`true`が `initialRun` .

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

サービスに対するすべての要求には、要求を実行したユーザーの難読化された ID と、ユーザーの表示名とMicrosoft Azure Active Directory (Azure AD) オブジェクト ID が含まれます。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

値と`aadObjectId`値は`id`、認証されたTeams ユーザーの値であることが保証されます。 資格情報またはサービス内のキャッシュされた状態を検索するためのキーとして使用できます。 さらに、各要求には、ユーザーの組織を識別するために使用できるユーザーのMicrosoft Azure Active Directory (Azure AD) テナント ID が含まれています。 該当する場合、要求には、要求の送信元となったチーム ID とチャネル ID も含まれます。

## <a name="authentication"></a>認証

サービスでユーザー認証が必要な場合は、ユーザーがメッセージ拡張機能を使用する前に、ユーザーにサインインする必要があります。 ユーザーにサインインするボットまたはタブを作成した場合は、このセクションをよく理解しておく必要があります。

シーケンスは次のとおりです。

1. ユーザーがクエリを発行するか、既定のクエリがサービスに自動的に送信されます。
2. サービスは、Teamsユーザー ID を調べることで、ユーザーが最初に認証されたかどうかを確認します。
3. ユーザーが認証されていない場合は、認証 URL を含む推奨されるアクションを含`openUrl`む応答を返信`auth`します。
4. Microsoft Teams クライアントは、特定の認証 URL を使用して Web ページをホストするポップアップ ウィンドウを起動します。
5. ユーザーがサインインしたら、ウィンドウを閉じて、Teams クライアントに "認証コード" を送信する必要があります。
6. その後、Teams クライアントは、手順 5 で渡した認証コードを含むクエリをサービスに再発行します。

サービスは、手順 6 で受信した認証コードが手順 5 の認証コードと一致することを確認する必要があります。これにより、悪意のあるユーザーがサインイン フローのスプーフィングや侵害を試みないようにします。 これにより、安全な認証シーケンスを終了させるための 「ループを閉じる」 効果があります。

### <a name="respond-with-a-sign-in-action"></a>サインイン アクションで応答する

認証されていないユーザーにサインインを求めるには、認証 URL を含む `openUrl` 型の推奨アクションで応答します。

#### <a name="response-example-for-a-sign-in-action"></a>サインイン アクションの応答の例

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
> サインイン エクスペリエンスをTeamsポップアップでホストするには、URL のドメイン部分がアプリの有効なドメインの一覧に含まれている必要があります。 詳細については、「マニフェスト スキーマの[validDomains](~/resources/schema/manifest-schema.md#validdomains)」 を参照してください。

### <a name="start-the-sign-in-flow"></a>サインイン フローを開始する

サインイン エクスペリエンスは応答性が高く、ポップアップ ウィンドウ内に収まる必要があります。 メッセージ パッシングを使用する [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) と統合する必要があります。

Teams内で実行されている他の埋め込みエクスペリエンスと同様に、ウィンドウ内のコードは最初に呼び出す`microsoftTeams.initialize()`必要があります。 コードで OAuth フローを実行する場合は、ウィンドウにTeamsユーザー ID を渡し、それを OAuth サインイン URL に渡すことができます。

### <a name="complete-the-sign-in-flow"></a>サインイン フローを完了する

サインイン要求が完了し、ページにリダイレクトされたら、次の手順を実行する必要があります。

1. セキュリティ コードを生成します。 (ランダムな数値を指定できます)。このコードは、OAuth 2.0 トークンなどのサインイン フローで取得した資格情報と共に、サービスにキャッシュする必要があります。
2. `microsoftTeams.authentication.notifySuccess` を呼び出して、セキュリティ コードを渡します。

この時点でウィンドウが閉じ、コントロールがTeams クライアントに渡されます。 クライアントは、プロパティ内のセキュリティ コードと共に、元のユーザー クエリを `state` 再発行できるようになりました。 コードでは、セキュリティ コードを使用して、前に保存した資格情報を検索して認証シーケンスを完了し、ユーザー要求を完了できます。

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

Bot Builder SDK for .NET でクエリを受け取って処理するには、受信アクティビティのアクションの種類を確認`invoke`し、NuGet パッケージ [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)のヘルパー メソッドを使用して、メッセージ拡張アクティビティであるかどうかを判断します。

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

[Bot Framework サンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
