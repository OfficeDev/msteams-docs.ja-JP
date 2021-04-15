---
title: タスク モジュールの作成と送信
author: clearab
description: 最初の呼び出しアクションを処理し、アクション メッセージング拡張機能コマンドからタスク モジュールで応答する方法
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 12af2d788c0579414b544e7e2fd7f07a77d45919
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696277"
---
# <a name="create-and-send-the-task-module"></a>タスク モジュールの作成と送信

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

アダプティブ カードまたは埋め込み Web ビューを使用してタスク モジュールを作成できます。 タスク モジュールを作成するには、最初の呼び出し要求と呼ばれるプロセスを実行する必要があります。 このドキュメントでは、最初の呼び出し要求、1:1 チャット、グループ チャット、チャネル (新しい投稿)、チャネル (スレッドへの返信)、およびコマンド ボックスからタスク モジュールが呼び出された場合のペイロード アクティビティ プロパティについて説明します。 
> [!NOTE]
> アプリ マニフェストで定義されたパラメーターをタスク モジュールに設定しない場合は、アダプティブ カードまたは埋め込み Web ビューを使用するユーザー用のタスク モジュールを作成する必要があります。

## <a name="the-initial-invoke-request"></a>最初の呼び出し要求

最初の呼び出し要求のプロセスで、サービスは型のオブジェクトを受け取り、アダプティブ カードまたは埋め込み Web ビューへの URL を含むオブジェクトで応答する `Activity` `composeExtension/fetchTask` `task` 必要があります。 ボットアクティビティの標準プロパティと共に、最初の呼び出しペイロードには次の要求メタデータが含まれます。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 この値は、 である必要があります `invoke` 。 |
|`name`| サービスに発行されるコマンドの種類。 この値は、 である必要があります `composeExtension/fetchTask` 。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.channel.id`| チャネル ID (チャネルで要求が行われた場合)。 |
|`channelData.team.id`| チーム ID (チャネルで要求が行われた場合)。 |
|`value.commandId` | 呼び出されたコマンドの ID が含まれる。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 この値は、 である必要があります `compose` 。 |
|`value.context.theme` | ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。 は、または `default` `contrast` である必要があります `dark` 。 |

### <a name="example"></a>例

最初の呼び出し要求のコードは、次の例で示されています。

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a>タスク モジュールが 1:1 チャットから呼び出された場合のペイロード アクティビティプロパティ 

タスク モジュールが 1:1 チャットから呼び出された場合のペイロード アクティビティのプロパティは、次のように表示されます。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 この値は、 である必要があります `invoke` 。 |
|`name`| サービスに発行されるコマンドの種類。 この値は、 である必要があります `composeExtension/fetchTask` 。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.source.name`| タスク モジュールの呼び出し元のソース名。 |
|`ChannelData.legacy. replyToId`| このメッセージが返信であるメッセージの ID を取得または設定します。 |
|`value.commandId` | 呼び出されたコマンドの ID が含まれる。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 この値は、 である必要があります `compose` 。 |
|`value.context.theme` | ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。 は、または `default` `contrast` である必要があります `dark` 。 |

### <a name="example"></a>例

タスク モジュールが 1:1 チャットから呼び出された場合のペイロード アクティビティプロパティは、次の例で示されています。

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```
## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a>グループ チャットからタスク モジュールが呼び出された場合のペイロード アクティビティのプロパティ 

タスク モジュールがグループ チャットから呼び出された場合のペイロード アクティビティのプロパティは、次のように表示されます。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 この値は、 である必要があります `invoke` 。 |
|`name`| サービスに発行されるコマンドの種類。 この値は、 である必要があります `composeExtension/fetchTask` 。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.source.name`| タスク モジュールの呼び出し元のソース名。 |
|`ChannelData.legacy. replyToId`| このメッセージが返信であるメッセージの ID を取得または設定します。 |
|`value.commandId` | 呼び出されたコマンドの ID が含まれる。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 この値は、 である必要があります `compose` 。 |
|`value.context.theme` | ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。 は、または `default` `contrast` である必要があります `dark` 。 |

### <a name="example"></a>例

タスク モジュールがグループ チャットから呼び出された場合のペイロード アクティビティプロパティは、次の例で示されています。

```json
{
  "type": "invoke",
  "id": "f:bf72031f-a17e-f99c-48dc-5c0714950d87",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "groupChat",
    "id": "19:d77be72390a1416e9644261e9064fa00@thread.skype",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "213167a1e3b6428b93e186ea5407c759",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a>チャネルからタスク モジュールが呼び出された場合のペイロード アクティビティ プロパティ (新しい投稿) 

タスク モジュールがチャネル (新しい投稿) から呼び出された場合のペイロード アクティビティプロパティは、次のように表示されます。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 この値は、 である必要があります `invoke` 。 |
|`name`| サービスに発行されるコマンドの種類。 この値は、 である必要があります `composeExtension/fetchTask` 。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.channel.id`| チャネル ID (チャネルで要求が行われた場合)。 |
|`channelData.team.id`| チーム ID (チャネルで要求が行われた場合)。 |
|`channelData.source.name`| タスク モジュールの呼び出し元のソース名。 |
|`ChannelData.legacy. replyToId`| このメッセージが返信であるメッセージの ID を取得または設定します。 |
|`value.commandId` | 呼び出されたコマンドの ID が含まれる。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 この値は、 である必要があります `compose` 。 |
|`value.context.theme` | ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。 、、または `default` `contrast` である必要があります `dark` 。 |

### <a name="example"></a>例

タスク モジュールがチャネル (新しい投稿) から呼び出された場合のペイロード アクティビティ プロパティは、次の例で示されています。

```json
{
  "type": "invoke",
  "id": "f:a5fbb109-c989-c449-ee83-71ac99919d4b",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "5336640edc7748b28ce2df43f5b45963",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a>チャネルからタスク モジュールが呼び出された場合のペイロード アクティビティ プロパティ (スレッドに返信) 

タスク モジュールがチャネルから呼び出された場合のペイロード アクティビティ プロパティ (スレッドへの返信) は、次のように表示されます。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 この値は、 である必要があります `invoke` 。 |
|`name`| サービスに発行されるコマンドの種類。 この値は、 である必要があります `composeExtension/fetchTask` 。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.channel.id`| チャネル ID (チャネルで要求が行われた場合)。 |
|`channelData.team.id`| チーム ID (チャネルで要求が行われた場合)。 |
|`channelData.source.name`| タスク モジュールの呼び出し元のソース名。 |
|`ChannelData.legacy. replyToId`| このメッセージが返信であるメッセージの ID を取得または設定します。 |
|`value.commandId` | 呼び出されたコマンドの ID が含まれる。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 この値は、 である必要があります `compose` 。 |
|`value.context.theme` | ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。 は、または `default` `contrast` である必要があります `dark` 。 |

### <a name="example"></a>例

タスク モジュールがチャネルから呼び出された場合のペイロード アクティビティ プロパティ (スレッドへの返信) は、次の例で示されています。

```json
{
  "type": "invoke",
  "id": "f:19ccc884-c792-35ef-2f40-d0ff43dcca71",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype;messageid=1611060744833",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "message",
    "requestId": "7f7d22efe5414818becebcec649a7912",
    "messagePayload": {
      "linkToMessage": "https://teams.microsoft.com/l/message/19:6decf54d86d945e4b3924b63a9161a78@thread.skype/1611060744833",
      "id": "1611060744833",
      "replyToId": null,
      "createdDateTime": "2021-01-19T12:52:24.833Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "<div><div><at id=\"0\">Testing outgoing Webhook-Nikitha</at> - Hi</div>\n</div>"
      },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc",
          "displayName": "Olo Brockhouse"
        },
        "application": null
      },
      "reactions": [],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Testing outgoing Webhook-Nikitha",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": null,
            "application": {
              "applicationIdentityType": "webhook",
              "id": "b8c1c68c-e290-4bdd-81c3-266f310751dc",
              "displayName": "Testing outgoing Webhook-Nikitha"
            }
          }
        }
      ],
      "attachments": []
    },
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a>タスク モジュールがコマンド ボックスから呼び出された場合のペイロード アクティビティ プロパティ 

タスク モジュールがコマンド ボックスから呼び出された場合のペイロード アクティビティ プロパティは、次のように表示されます。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 この値は、 である必要があります `invoke` 。 |
|`name`| サービスに発行されるコマンドの種類。 この値は、 である必要があります `composeExtension/fetchTask` 。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.source.name`| タスク モジュールの呼び出し元のソース名。 |
|`value.commandId` | 呼び出されたコマンドの ID が含まれる。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 この値は、 である必要があります `compose` 。 |
|`value.context.theme` | ユーザーのクライアント テーマは、埋め込み Web ビューの書式設定に役立ちます。 、、または `default` `contrast` である必要があります `dark` 。 |

### <a name="example"></a>例

タスク モジュールがコマンド ボックスから呼び出された場合のペイロード アクティビティ プロパティは、次の例で示されています。

```json
{
  "type": "invoke",
  "id": "f:172560f1-95f9-3189-edb2-b7612cd1a3cd",
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "compose",
    "requestId": "d2ce690cdc2b4920a538e75882610a30",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

### <a name="example"></a>例 

次のコード セクションは、要求の例 `fetchTask` です。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a>メッセージからの最初の呼び出し要求

ボットがメッセージから呼び出されると、最初の呼び出し要求のオブジェクトに、メッセージング拡張機能が呼び出されるメッセージの詳細が `value` 含まれている必要があります。 配列 `reactions` と配列は省略可能で、元のメッセージにリアクションやメンションがない場合は `mentions` 存在しません。 次のセクションは、オブジェクトの例 `value` です。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a>fetchTask に応答する

アダプティブ カードまたは Web URL を持つオブジェクト、または単純な文字列メッセージを含むオブジェクトを使用して、呼び出し要求 `task` `taskInfo` に応答します。

|プロパティ名|用途|
|---|---|
|`type`| フォームを表示 `continue` するか、単純な `message` ポップアップを表示できます。 |
|`value`| フォーム `taskInfo` のオブジェクト、またはメッセージ `string` の a。 |

taskInfo オブジェクトのスキーマは次の値です。

|プロパティ名|用途|
|---|---|
|`title`| タスク モジュールのタイトル。|
|`height`| 整数 (ピクセル単位) または 、 `small` 、 のいずれか `medium` である必要があります `large` 。|
|`width`| 整数 (ピクセル単位) または 、 `small` 、 のいずれか `medium` である必要があります `large` 。|
|`card`| フォームを定義するアダプティブ カード (使用している場合)。
|`url`| 埋め込み Web ビューとしてタスク モジュール内で開く URL。|
|`fallbackUrl`| クライアントがタスク モジュール機能をサポートしていない場合、この URL はブラウザー タブで開きます。 |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a>アダプティブ カードを使用して fetchTask に応答する

アダプティブ カードを使用する場合は、アダプティブ カードを含むオブジェクトでオブジェクト `task` `value` に応答する必要があります。

#### <a name="example"></a>例

次のコード セクションは、アダプティブ カードで `fetchTask` 応答する例です。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

このサンプルでは、Bot Framework SDK に加えて [AdaptiveCards NuGet](https://www.nuget.org/packages/AdaptiveCards) パッケージを使用します。

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="create-a-task-module-with-an-embedded-web-view"></a>埋め込み Web ビューを使用してタスク モジュールを作成する

埋め込み Web ビューを使用する場合は、読み込む Web フォームへの URL を含むオブジェクトを持つオブジェクトに応答 `task` `value` する必要があります。 読み込む URL のドメインは、アプリのマニフェストの配列 `validDomains` に含める必要があります。 埋め込み Web ビューの構築の詳細については、タスク モジュールの [ドキュメントを参照してください](~/task-modules-and-cards/what-are-task-modules.md)。 

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

### <a name="request-to-install-your-conversational-bot"></a>会話型ボットのインストールを要求する

アプリに会話型ボットが含まれている場合は、会話にボットをインストールし、タスク モジュールを読み込む。 ボットは、タスク モジュールの追加コンテキストを取得する場合に便利です。 このシナリオの例は、名簿をフェッチして、ユーザー選択コントロールまたはチーム内のチャネルの一覧を設定します。

メッセージング拡張機能が呼び出しを受信したら、ボットが現在のコンテキストにインストールされていることを確認して、フロー `composeExtension/fetchTask` を容易にしてください。 たとえば、取得名簿呼び出しでフローを確認します。 ボットがインストールされていない場合は、ユーザーにボットのインストールを要求するアクションを含むアダプティブ カードを返します。 ユーザーは、チェックのためにその場所にアプリをインストールする権限を持っている必要があります。 アプリのインストールが失敗した場合、ユーザーは管理者に連絡するメッセージを受信します。

#### <a name="example"></a>例 

次のコード セクションは、応答の例です。

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

会話型ボットのインストール後、別の呼び出しメッセージを受け `name = composeExtension/submitAction` 取ります `value.data.msteams.justInTimeInstall = true` 。

#### <a name="example"></a>例 

次のコード セクションは、呼び出しに対するタスク応答の例です。

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

呼び出しに対するタスク応答は、インストールされているボットのタスク応答と似ている必要があります。

#### <a name="example"></a>例 

次のコード セクションは、アダプティブ カードを使用したアプリの just-in time インストールの例です。 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="code-sample"></a>コード サンプル

| サンプルの名前           | 説明 | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Teams メッセージング拡張機能アクション| アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams メッセージング拡張機能の検索   |  検索コマンドを定義し、検索に応答する方法について説明します。        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"] 
> [操作コマンドを定義する](~/messaging-extensions/how-to/action-commands/define-action-command.md)


## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"] 
> [[アクションに応答] コマンド](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

