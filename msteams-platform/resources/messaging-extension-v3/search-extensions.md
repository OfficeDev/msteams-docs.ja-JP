---
title: メッセージング拡張機能を使用した検索
description: 検索ベースのメッセージング拡張機能を開発する方法について説明します。
keywords: teams メッセージング拡張メッセージング拡張検索
ms.date: 07/20/2019
ms.openlocfilehash: c220d976fa3e9920c8d4bb332a793b23d9b294c4
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228046"
---
# <a name="search-with-messaging-extensions"></a>メッセージング拡張機能を使用した検索

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

検索ベースのメッセージング拡張機能を使用すると、サービスを照会して、その情報をカードの形式でメッセージに投稿することができます。

![メッセージング拡張カードの例](~/assets/images/compose-extensions/ceexample.png)

次のセクションでは、これを行う方法について説明します。

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a>検索の種類メッセージの拡張子

検索ベースのメッセージング拡張機能に`type`ついて`query`は、パラメーターをに設定します。 単一の検索コマンドを含むマニフェストの例を次に示します。 1つのメッセージング拡張機能には、最大10個の異なるコマンドを関連付けることができます。 これには、複数の検索と複数のアクションベースのコマンドの両方を含めることができます。

#### <a name="complete-app-manifest-example"></a>完全なアプリマニフェストの例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

アプリをアップロードすることで、メッセージング拡張機能をテストできます。

メッセージング拡張機能を開くには、いずれかのチャットまたはチャネルに移動します。 [新規作成] ボックスの [**その他のオプション**(**&#8943;**)] ボタンをクリックして、メッセージング拡張機能を選択します。

## <a name="add-event-handlers"></a>イベントハンドラーを追加する

ほとんどの作業では、 `onQuery`メッセージング拡張ウィンドウでのすべての操作を処理するイベントが必要になります。

マニフェストにが`canUpdateConfiguration`に`true`設定されている場合は、メッセージング拡張機能の [**設定**] メニュー項目を`onQuerySettingsUrl`有効`onSettingsUpdate`にして、とも処理する必要があります。

### <a name="handle-onquery-events"></a>OnQuery イベントを処理する

メッセージング拡張機能は、 `onQuery`メッセージング拡張ウィンドウで何らかの問題が発生した場合、またはウィンドウに送信された場合に、イベントを受信します。

メッセージング拡張機能が構成ページを使用している場合`onQuery`は、のハンドラーで、格納されている構成情報があるかどうかをまずチェックする必要があります。メッセージング拡張機能が構成されてい`config`ない場合は、構成ページへのリンクを含む応答を返します。 構成ページからの応答もによって`onQuery`処理されることに注意してください。 (唯一の例外は、の`onQuerySettingsUrl`ハンドラーによって構成ページが呼び出されたときです。次のセクションを参照してください)。

メッセージング拡張機能で認証が必要な場合は、ユーザー状態情報を確認してください。ユーザーがサインインしていない場合は、このトピックで後述する「[認証](#authentication)」の手順に従ってください。

次に、が`initialRun`設定されているかどうかを確認します。その場合は、指示の提供や応答の一覧などの適切なアクションを実行します。

ハンドラーの残りの部分で`onQuery`は、ユーザーに情報の入力を求め、プレビューカードの一覧を表示し、ユーザーが選択したカードを返します。

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>OnQuerySettingsUrl と onSettingsUpdate イベントを処理する

イベント`onQuerySettingsUrl`と`onSettingsUpdate`イベントは連携して、[**設定**] メニュー項目を有効にします。

![設定メニュー項目の場所のスクリーンショット](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

の`onQuerySettingsUrl`ハンドラーは、構成ページの URL を返します。構成ページが閉じられると、の`onSettingsUpdate`ハンドラーは、返された状態を受け入れて保存します。 (の1つのケースで`onQuery`は、構成ページから応答を受信し*ません*)。

## <a name="receive-and-respond-to-queries"></a>クエリを受信して応答する

メッセージング拡張機能へのすべての要求は、 `Activity`コールバック URL にポストされたオブジェクトによって実行されます。 要求には、ID やパラメーターの値など、ユーザーコマンドに関する情報が含まれています。 また、この要求は、ユーザーやテナント ID など、拡張機能が呼び出されたコンテキストに関するメタデータと共に、チャット ID またはチャネルとチーム Id も提供します。

### <a name="receive-user-requests"></a>ユーザー要求を受信する

ユーザーがクエリを実行すると、Microsoft Teams はサービスを標準 Bot フレームワーク`Activity`オブジェクトに送信します。 サービスは、次の表に示す`Activity`ように`type` `invoke` 、がサポート`name`されている`composeExtension`型に設定されていて、に設定されているのロジックを実行する必要があります。

標準の bot アクティビティプロパティに加えて、ペイロードには次の要求メタデータが含まれています。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。で`invoke`ある必要があります。 |
|`name`| サービスに対して発行されるコマンドの種類。 現在、次の種類がサポートされています。 <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト id。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.channel.id`| チャネル ID (チャネルで要求が行われた場合)。 |
|`channelData.team.id`| チーム ID (チャネルで要求が行われた場合)。 |
|`clientInfo`|ユーザーのメッセージの送信に使用されるクライアントソフトウェアに関するオプションのメタデータ。 エンティティには、次の2つのプロパティを含めることができます。<br>この`country`フィールドには、ユーザーが検出した場所が含まれています。<br>この`platform`フィールドには、メッセージングクライアントプラットフォームが記述されています。 <br>その他の情報については、 *「* [IRI 以外のエンティティの種類– clientinfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)」を参照してください。|

要求パラメーター自体は、次のプロパティを含む value オブジェクトにあります。

| プロパティ名 | 用途 |
|---|---|
| `commandId` | アプリマニフェストで宣言されているコマンドのいずれかと一致する、ユーザーによって起動されたコマンドの名前。 |
| `parameters` | パラメーターの配列。 各 parameter オブジェクトには、ユーザーによって提供されるパラメータ値とともにパラメータ名が含まれています。 |
| `queryOptions` | 改ページのパラメーター: <br>`skip`: このクエリの skip count <br>`count`: 返される要素の数 |

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

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>新規作成メッセージボックスに挿入されたリンクからの要求を受信する

または、外部サービスを検索する代わりに、[作成] メッセージボックスに挿入された URL を使用してサービスを照会し、カードを返すことができます。 次のスクリーンショットでは、ユーザーが Azure DevOps で作業項目の URL を貼り付けて、メッセージング拡張機能がカードに解決されたことを示しています。

![Link unfurling の例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

この方法でメッセージング拡張機能がリンクを操作できるようにするには、まず`messageHandlers` 、次の例に示すように、最初に、アプリケーションマニフェストに配列を追加する必要があります。

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

アプリマニフェストをリッスンするためにドメインを追加したら、次の呼び出し要求に[応答](#respond-to-user-requests)するように bot コードを変更する必要があります。

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

アプリが複数の項目を返す場合は、最初の項目のみが使用されます。

### <a name="respond-to-user-requests"></a>ユーザー要求に応答する

ユーザーがクエリを実行すると、Microsoft Teams はサービスに対して同期 HTTP 要求を発行します。 その時点で、コードには、要求に対する HTTP 応答を提供する5秒の時間があります。 この間、サービスは、追加の参照、または要求の提供に必要なその他のビジネスロジックを実行できます。

サービスは、ユーザークエリに一致する結果で応答する必要があります。 応答は、HTTP 状態コード`200 OK`と、次の本文を含む有効な application/json オブジェクトを示す必要があります。

|プロパティ名|用途|
|---|---|
|`composeExtension`|最上位レベルの応答封筒。|
|`composeExtension.type`|応答の種類。 次の種類がサポートされています。 <br>`result`: 検索結果の一覧を表示します。 <br>`auth`: ユーザーに認証を要求する <br>`config`: メッセージング拡張機能をセットアップするようにユーザーに要求します。 <br>`message`: テキスト形式のメッセージが表示されます。 |
|`composeExtension.attachmentLayout`|添付ファイルのレイアウトを指定します。 種類`result`の応答に使用されます。 <br>現在、次の種類がサポートされています。 <br>`list`: サムネイル、タイトル、テキストフィールドを含む card オブジェクトのリスト <br>`grid`: サムネイル画像のグリッド |
|`composeExtension.attachments`|有効な attachment オブジェクトの配列。 種類`result`の応答に使用されます。 <br>現在、次の種類がサポートされています。 <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|推奨されるアクション。 種類`auth`または`config`の応答に使用されます。 |
|`composeExtension.text`|表示するメッセージ。 種類`message`の応答に使用されます。 |

#### <a name="response-card-types-and-previews"></a>応答カードの種類とプレビュー

次の種類の添付ファイルがサポートされています。

* [サムネイルカード](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [英雄カード](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 コネクタカード](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [アダプティブカード](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

概要については、「[カード](~/task-modules-and-cards/what-are-cards.md)」を参照してください。

サムネイルおよびヒーローカードの種類を使用する方法については、「[カードおよびカードのアクションを追加](~/task-modules-and-cards/cards/cards-actions.md)する」を参照してください。

Office 365 コネクタカードに関するその他のドキュメントについては、「 [office 365 コネクタカードの使用](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)」を参照してください。

結果リストは、Microsoft Teams UI に各アイテムのプレビューと共に表示されます。 プレビューは、次の2つの方法のいずれかで生成されます。

* `attachment`オブジェクト内で`preview`プロパティを使用します。 添付`preview`ファイルには、ヒーローまたはサムネイルカードのみを指定できます。
* 添付ファイルの基本`title`、 `text`、および`image`プロパティから抽出されます。 これらのプロパティは、 `preview`プロパティが設定されておらず、これらのプロパティを使用できる場合にのみ使用されます。

プレビュープロパティを設定するだけで、アダプティブまたは Office 365 のコネクタカードのプレビューを結果リストに表示することができます。結果が既にヒーローまたはサムネイルカードである場合は、この手順は必要ありません。 プレビューの添付ファイルを使用する場合は、ヒーローまたは Thumbnail カードである必要があります。 Preview プロパティが指定されていない場合、カードのプレビューは失敗し、何も表示されません。

#### <a name="response-example"></a>応答の例

この例では、異なるカード形式が混在する2つの結果を含む応答を示します。 Office 365 コネクタとアダプティブ。 応答に1枚のカード形式を維持したい場合がありますが、前述し`preview`たように、 `attachments`コレクション内の各要素のプロパティが、ヒーローまたは thumbnail 形式でプレビューを明示的に定義する必要があることを示しています。

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
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
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

マニフェスト内に`initialRun`が`true`設定されている場合、Microsoft Teams は、ユーザーが最初にメッセージング拡張機能を開いたときに "既定" クエリを発行します。 サービスは、一連の事前設定された結果を使用してこのクエリに応答できます。 これは、たとえば、最近表示されたアイテム、お気に入り、またはユーザー入力に依存しないその他の情報を表示する場合に便利です。

既定のクエリは、通常のユーザークエリと同じ構造を持っています`initialRun`が、文字列値`true`があるパラメーターは除きます。

#### <a name="request-example-for-a-default-query"></a>既定のクエリの要求の例

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

サービスへのすべての要求には、要求を実行したユーザーの難読化された ID、およびユーザーの表示名と Azure Active Directory オブジェクト ID が含まれます。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

と`id` `aadObjectId`の値は、認証された Teams のユーザーのものであることが保証されています。 これらは、サービスの資格情報またはキャッシュされた状態を検索するためのキーとして使用できます。 さらに、各要求には、ユーザーの Azure Active Directory テナント ID が含まれています。これは、ユーザーの組織を識別するために使用できます。 該当する場合、要求には、要求の発行元であるチームおよびチャネル Id も含まれます。

## <a name="authentication"></a>認証

サービスでユーザー認証が必要な場合は、メッセージング拡張機能を使用できるようにするには、ユーザーにサインインする必要があります。 ユーザーにサインインする bot またはタブを書いてある場合は、このセクションを理解しておく必要があります。

順序は次のとおりです。

1. ユーザーがクエリを発行するか、既定のクエリがサービスに自動的に送信されます。
2. サービスは、ユーザーが Teams ユーザー ID を調べて最初に認証されているかどうかを確認します。
3. ユーザーが認証されていない場合は`auth` 、認証 URL `openUrl`を含む推奨されるアクションを使用して応答を返信に送り返します。
4. Microsoft Teams クライアントは、指定された認証 URL を使用して、web ページをホストするポップアップウィンドウを起動します。
5. ユーザーがサインインした後、ウィンドウを閉じて、Teams クライアントに "認証コード" を送信する必要があります。
6. Teams クライアントは、手順5で渡された認証コードを含む、サービスに対してクエリを再度発行します。

サービスは、手順6で受信した認証コードが手順5と一致することを確認する必要があります。 これにより、悪意のあるユーザーがサインインフローをスプーフィングしたり、侵害したりすることを防ぐことができます。 これにより、"ループを閉じる" というセキュリティで保護された認証シーケンスが完了します。

### <a name="respond-with-a-sign-in-action"></a>サインインアクションで応答する

認証されていないユーザーにサインインを求めるメッセージを表示するに`openUrl`は、認証 URL を含む種類の推奨されるアクションで応答します。

#### <a name="response-example-for-a-sign-in-action"></a>サインインアクションの応答の例

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
> チームのポップアップでサインインするために、URL のドメイン部分は、アプリの有効なドメインの一覧に含まれている必要があります。 (マニフェストスキーマの[Validdomains](~/resources/schema/manifest-schema.md#validdomains)を参照してください)。

### <a name="start-the-sign-in-flow"></a>サインインフローを開始する

サインイン手順は、ポップアップウィンドウ内に表示されるようにする必要があります。 これは、メッセージパッシングを使用する[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client)と統合する必要があります。

Microsoft Teams 内部で実行されている他の組み込みエクスペリエンスと同様に、ウィンドウ内`microsoftTeams.initialize()`のコードは最初に呼び出す必要があります。 コードで OAuth フローを実行すると、Teams ユーザー ID をウィンドウに渡すことができます。これにより、OAuth サインイン URL に渡されます。

### <a name="complete-the-sign-in-flow"></a>サインインフローを完了する

サインイン要求が完了し、ページにリダイレクトされたら、次の手順を実行します。

1. セキュリティコードを生成します。 (これはランダムな数値になることがあります。)このコードを、サインインフロー (OAuth 2.0 トークンなど) で取得した資格情報と共にサービスにキャッシュする必要があります。
2. を`microsoftTeams.authentication.notifySuccess`呼び出して、セキュリティコードを渡します。

この時点で、ウィンドウが閉じられ、Teams クライアントに制御が渡されます。 クライアントは、元のユーザークエリと、 `state`プロパティのセキュリティコードを再発行することができるようになります。 コードでは、セキュリティコードを使用して、前に保存した資格情報を参照して認証シーケンスを完了し、ユーザー要求を完了できます。

#### <a name="reissued-request-example"></a>再発行した要求の例

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

Bot ビルダー SDK for .NET を使用してクエリを受信して処理するには`invoke` 、受信アクティビティのアクションの種類を確認してから、NuGet パッケージの[各 Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)でヘルパーメソッドを使用して、メッセージング拡張アクティビティであるかどうかを確認します。

#### <a name="example-code-in-net"></a>.NET でのコード例

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

#### <a name="example-code-in-nodejs"></a>Node.js のコード例

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
[Bot フレームワークサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)*も参照してください*。
