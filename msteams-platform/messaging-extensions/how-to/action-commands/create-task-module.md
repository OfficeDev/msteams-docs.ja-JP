---
title: タスク モジュールの作成と送信
author: surbhigupta
description: コード例とサンプルを使用して、最初の呼び出しアクションを処理し、アクション メッセージングの拡張機能コマンドからタスク モジュールで応答する方法について説明します。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5daf262bfad3c88477ec0a1104e45b7cb9848aac
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65110352"
---
# <a name="create-and-send-the-task-module"></a>タスク モジュールの作成と送信

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

アダプティブ カードまたは埋め込み Web ビューを使用して、タスク モジュールを作成できます。 タスク モジュールを作成するには、最初の呼び出し要求と呼ばれるプロセスを実行する必要があります。 このドキュメントでは、最初の呼び出し要求と、タスク モジュールが 1 対 1 のチャット、グループ チャット、チャネル (新しい投稿)、チャネル (スレッドに返信)、コマンド ボックスから呼び出されたときのペイロード アクティビティ プロパティについて説明します。
> [!NOTE]
> アプリ マニフェストで定義されているパラメーターをタスク モジュールに設定しない場合は、アダプティブ カードまたは埋め込み Web ビューのいずれかを使用してユーザーにタスク モジュールを作成する必要があります。

## <a name="the-initial-invoke-request"></a>最初の呼び出し要求

最初の呼び出し要求の過程で、サービスは型 `composeExtension/fetchTask` の `Activity` オブジェクトを受信します。アダプティブ カードまたは埋め込み Web ビューへの URL を含む `task` オブジェクトで応答する必要があります。 最初の呼び出しペイロードには、標準のボット アクティビティ プロパティとともに次の要求メタデータが含まれます。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 `invoke` である必要があります。 |
|`name`| サービスに対して発行されるコマンドの種類。 `composeExtension/fetchTask` である必要があります。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.channel.id`| チャネル ID (要求がチャネルで行われた場合)。 |
|`channelData.team.id`| チーム ID (要求がチャネルで行われた場合)。 |
|`value.commandId` | 呼び出されたコマンドの ID が含まれます。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 `compose` である必要があります。 |
|`value.context.theme` | ユーザーのクライアント テーマ。これは、埋め込み Web ビューの書式設定に役立ちます。 `default`、`contrast`、または `dark` である必要があります。 |

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a>タスク モジュールが 1:1 チャットから呼び出されたときのペイロード アクティビティ プロパティ

タスク モジュールが 1:1 チャットから呼び出されたときのペイロード アクティビティ プロパティを以下に示します。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 `invoke` である必要があります。 |
|`name`| サービスに対して発行されるコマンドの種類。 `composeExtension/fetchTask` である必要があります。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.source.name`| タスク モジュールが呼び出されるソース名。 |
|`ChannelData.legacy. replyToId`| このメッセージが返信となるメッセージの ID を取得または設定します。 |
|`value.commandId` | 呼び出されたコマンドの ID が含まれます。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 `compose` である必要があります。 |
|`value.context.theme` | ユーザーのクライアント テーマ。これは、埋め込み Web ビューの書式設定に役立ちます。 `default`、`contrast`、または `dark` である必要があります。 |

### <a name="example"></a>例

次の例で、タスク モジュールが 1:1 チャットから呼び出されたときのペイロード アクティビティ プロパティを示します。

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a>タスク モジュールがグループ チャットから呼び出されたときのペイロード アクティビティ プロパティ

タスク モジュールがグループ チャットから呼び出されたときのペイロード アクティビティ プロパティを以下に示します。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 `invoke` である必要があります。 |
|`name`| サービスに対して発行されるコマンドの種類。 `composeExtension/fetchTask` である必要があります。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.source.name`| タスク モジュールが呼び出されるソース名。 |
|`ChannelData.legacy. replyToId`| このメッセージが返信となるメッセージの ID を取得または設定します。 |
|`value.commandId` | 呼び出されたコマンドの ID が含まれます。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 `compose` である必要があります。 |
|`value.context.theme` | ユーザーのクライアント テーマ。これは、埋め込み Web ビューの書式設定に役立ちます。 `default`、`contrast`、または `dark` である必要があります。 |

### <a name="example"></a>例

次の例で、タスク モジュールがグループ チャットから呼び出されたときのペイロード アクティビティ プロパティを示します。

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-meeting-chat"></a>タスク モジュールが会議チャットから呼び出されたときのペイロード アクティビティ プロパティ

次の例で、タスク モジュールが会議チャットから呼び出されたときのペイロード アクティビティ プロパティを示します。

```json
{
   "type": "invoke",
   "id": "f:4d271f11-4eed-622f-e820-6d82bf91692f",
   "channelId": "msteams",
   "from": {
      "id": "29:1yLsdbTM1UjxqqD8cjduNUCI1jm8xZaH3lx9u5JQ04t2bknuTCkP45TXdfROTOWk1LzN1AqTgFZUEqHIVGn_qUA",
      "name": "MOD Administrator",
      "aadObjectId": "ef16aa89-5b26-4a2c-aebb-761b551577c0"
   },
   "conversation": {
      "tenantId": "c9f9aafd-64ac-4f38-8e05-12feba3fb090",
      "id": "19:meeting_NTk4ZDY4ZmYtOWEzZS00OTRkLThhY2EtZmUzZmUzMDQyM2M0@thread.v2",
      "name": "Test meeting"
   },   
   "channelData": {
      "tenant": {
         "id": "c9f9aafd-64ac-4f38-8e05-12feba3fb090"
      },
      "source": {
         "name": "compose"
      },
      "meeting": {
         "id": "MCMxOTptZWV0aW5nX05UazRaRFk0Wm1ZdE9XRXpaUzAwT1RSa0xUaGhZMkV0Wm1VelptVXpNRFF5TTJNMEB0aHJlYWQudjIjMA=="
      }
   },
   "value": {
      "commandId": "Test",
      "commandContext": "compose",
      "requestId": "c46a6b53573f42b5bc801716e5ccc960",
      "context": {
         "theme": "default"
      }
   },
   "name": "composeExtension/fetchTask",
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a>タスク モジュールがチャネル (新しい投稿) から呼び出されたときのペイロード アクティビティ プロパティ

タスク モジュールがチャネル (新しい投稿) から呼び出されたときのペイロード アクティビティ プロパティを以下に示します。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 `invoke` である必要があります。 |
|`name`| サービスに対して発行されるコマンドの種類。 `composeExtension/fetchTask` である必要があります。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.channel.id`| チャネル ID (要求がチャネルで行われた場合)。 |
|`channelData.team.id`| チーム ID (要求がチャネルで行われた場合)。 |
|`channelData.source.name`| タスク モジュールが呼び出されるソース名。 |
|`ChannelData.legacy. replyToId`| このメッセージが返信となるメッセージの ID を取得または設定します。 |
|`value.commandId` | 呼び出されたコマンドの ID が含まれます。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 `compose` である必要があります。 |
|`value.context.theme` | ユーザーのクライアント テーマ。これは、埋め込み Web ビューの書式設定に役立ちます。 `default`、`contrast`、または `dark` である必要があります。 |

### <a name="example"></a>例

次の例で、タスク モジュールがチャネル (新しい投稿) から呼び出されたときのペイロード アクティビティ プロパティを示します。

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a>タスク モジュールがチャネル (スレッドに返信) から呼び出されたときのペイロード アクティビティ プロパティ

タスク モジュールがチャネル (スレッドに返信) から呼び出されたときのペイロード アクティビティ プロパティを以下に示します。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 `invoke` である必要があります。 |
|`name`| サービスに対して発行されるコマンドの種類。 `composeExtension/fetchTask` である必要があります。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.channel.id`| チャネル ID (要求がチャネルで行われた場合)。 |
|`channelData.team.id`| チーム ID (要求がチャネルで行われた場合)。 |
|`channelData.source.name`| タスク モジュールが呼び出されるソース名。 |
|`ChannelData.legacy. replyToId`| このメッセージが返信となるメッセージの ID を取得または設定します。 |
|`value.commandId` | 呼び出されたコマンドの ID が含まれます。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 `compose` である必要があります。 |
|`value.context.theme` | ユーザーのクライアント テーマ。これは、埋め込み Web ビューの書式設定に役立ちます。 `default`、`contrast`、または `dark` である必要があります。 |

### <a name="example"></a>例

次の例で、タスク モジュールがチャネル (スレッドに返信) から呼び出されたときのペイロード アクティビティ プロパティを示します。

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

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a>タスク モジュールがコマンド ボックスから呼び出されたときのペイロード アクティビティ プロパティ

タスク モジュールがコマンド ボックスから呼び出されたときのペイロード アクティビティ プロパティを以下に示します。

|プロパティ名|用途|
|---|---|
|`type`| 要求の種類。 `invoke` である必要があります。 |
|`name`| サービスに対して発行されるコマンドの種類。 `composeExtension/fetchTask` である必要があります。 |
|`from.id`| 要求を送信したユーザーの ID。 |
|`from.name`| 要求を送信したユーザーの名前。 |
|`from.aadObjectId`| 要求を送信したユーザーの Azure Active Directory オブジェクト ID。 |
|`channelData.tenant.id`| Azure Active Directory テナント ID。 |
|`channelData.source.name`| タスク モジュールが呼び出されるソース名。 |
|`value.commandId` | 呼び出されたコマンドの ID が含まれます。 |
|`value.commandContext` | イベントをトリガーしたコンテキスト。 `compose` である必要があります。 |
|`value.context.theme` | ユーザーのクライアント テーマ。これは、埋め込み Web ビューの書式設定に役立ちます。 `default`、`contrast`、または `dark` である必要があります。 |

### <a name="example"></a>例

次の例で、タスク モジュールがコマンド ボックスから呼び出されたときのペイロード アクティビティ プロパティを示します。

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

次のコード セクションは、`fetchTask` 要求の例です。

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

ボットがメッセージから呼び出されると、最初の呼び出し要求の `value` オブジェクトに、メッセージ拡張機能の呼び出し元のメッセージの詳細が含まれている必要があります。 `reactions` 配列と `mentions` 配列は省略可能であり、元のメッセージにリアクションやメンションがない場合は存在しません。
次のセクションは、`value` オブジェクトの例です。

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

アダプティブ カードまたは Web URL を持つ `taskInfo` オブジェクトか、単純な文字列メッセージを含む `task` オブジェクトを使用して、呼び出し要求に応答します。

|プロパティ名|用途|
|---|---|
|`type`| フォームを表示する `continue` か、単純なポップアップを表示する `message` のいずれかを指定できます。 |
|`value`| フォームの `taskInfo` オブジェクト、またはメッセージの `string` オブジェクトのいずれかです。 |

taskInfo オブジェクトのスキーマは次のとおりです。

|プロパティ名|用途|
|---|---|
|`title`| タスク モジュールのタイトル。|
|`height`| 整数 (ピクセル単位) か、`small`、`medium`、`large` のいずれかである必要があります。|
|`width`| 整数 (ピクセル単位) か、`small`、`medium`、`large` のいずれかである必要があります。|
|`card`| フォームを定義するアダプティブ カード (使用している場合)。
|`url`| 埋め込み Web ビューとしてタスク モジュール内で開く URL。|
|`fallbackUrl`| クライアントがタスク モジュール機能をサポートしていない場合、この URL がブラウザー タブで開かれます。 |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a>アダプティブ カードを使用して fetchTask に応答する

アダプティブ カードを使用する場合、アダプティブ カードを含む `value` オブジェクトと `task` オブジェクトで応答する必要があります。

#### <a name="example"></a>例

次のコード セクションは、アダプティブ カードを使用した `fetchTask` 応答の例です。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

このサンプルでは、Bot Framework SDK に加えて [AdaptiveCards NuGet パッケージ](https://www.nuget.org/packages/AdaptiveCards)を使用します。

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

埋め込み Web ビューを使用する場合、読み込む Web フォームへの URL を含む `value` オブジェクトを含む `task` オブジェクトで応答する必要があります。 読み込む URL のドメインは、アプリのマニフェストの `validDomains` 配列に含める必要があります。 埋め込み Web ビューの構築の詳細については、「[タスク モジュール」のドキュメント](~/task-modules-and-cards/what-are-task-modules.md)を参照してください。

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

アプリに会話型ボットが含まれている場合、会話にボットをインストールし、タスク モジュールを読み込みます。 ボットは、タスク モジュールの追加のコンテキストを取得するのに役立ちます。 このシナリオの例として、参加者一覧をフェッチして、ユーザー ピッカー コントロールまたはチーム内のチャネルの一覧を設定することが挙げられます。

メッセージ拡張機能が `composeExtension/fetchTask` 呼び出しを受信したら、フローを容易にするために、ボットが現在のコンテキストにインストールされているかどうかを確認します。 たとえば、参加者一覧の取得呼び出しでフローを確認します。 ボットがインストールされていない場合、ユーザーにボットのインストールを要求するアクションを含むアダプティブ カードを返します。 ユーザーには、確認のためにその場所にアプリをインストールするアクセス許可が必要です。 アプリのインストールに失敗した場合、ユーザーは管理者に問い合わせるメッセージを受信します。

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

会話型ボットのインストール後、`name = composeExtension/submitAction` と `value.data.msteams.justInTimeInstall = true` を含む別の呼び出しメッセージを受信します。

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

呼び出しに対するタスク応答は、インストールされているボットの応答と同じである必要があります。

#### <a name="example"></a>例

次のコード セクションは、アダプティブ カードを使用したアプリのジャストインタイム インストールの例です。

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
|Teams メッセージ拡張機能アクション| アクション コマンドを定義し、タスク モジュールを作成し、タスク モジュール送信アクションに応答する方法について説明します。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Teams メッセージ拡張機能検索   |  検索コマンドを定義し、検索に応答する方法について説明します。        |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [操作コマンドに返信する](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

## <a name="see-also"></a>関連項目

[操作コマンドを定義する](~/messaging-extensions/how-to/action-commands/define-action-command.md)
