---
title: Teams 会議の会議内通知を作成する
author: v-sdhakshina
description: この記事では、Microsoft Teams 会議の会議内通知とそのコード サンプルを作成する方法について説明します。
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: e62958535fa1bcbcdeb104b5fd5fdd2882250aa3
ms.sourcegitcommit: 372aade09e62ac7e5936215173a6632fbb042c9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/26/2022
ms.locfileid: "68699130"
---
# <a name="build-in-meeting-notification-for-teams-meeting"></a>Teams 会議の会議内通知を作成する

会議内通知は、参加者を関与させ、会議中に情報やフィードバックを収集するために使用されます。 会議中の通知をトリガーするには、[会議中の通知ペイロード](meeting-apps-apis.md#send-an-in-meeting-notification)を使用します。 通知ペイロード要求の一部として、表示するコンテンツがホストされている URL を含めます。

会議中の通知を表示するには、外部リソース URL を使用します。 会議チャットでデータを送信するには、`submitTask` メソッドを使用します。

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="スクリーンショットは、会議内ダイアログを使用する方法を示す例です。":::

また、Teams の表示画像と連絡先カードを、ユーザーのMRI とペイロードで渡された表示名を持つトークン `onBehalfOf` に基づいて、会議中の通知に追加することもできます。 ペイロードの例を次に示します:

```json
    {
       "type": "message",
       "text": "John Phillips assigned you a weekly todo",
       "summary": "Don't forget to meet with Marketing next week",
       "channelData": {
           onBehalfOf: [
             { 
               itemId: 0, 
               mentionType: 'person', 
               mri: context.activity.from.id, 
               displayname: context.activity.from.name 
             }
            ],
           "notification": {
           "alertInMeeting": true,
           "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
            }
        },
       "replyToId": "1493070356924"
    }
```

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-people-card.png" alt-text="このスクリーンショットは、Teams が会議内ダイアログで画像とユーザー カードを表示する方法を示しています。" border="true":::

## <a name="code-sample"></a>コード サンプル

サンプルの名前 | 説明 | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| 会議中の通知 | ボットを使用して会議内通知を実装する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

[詳細なガイド](../sbs-meeting-content-bubble.yml)に従って、Teams 会議で会議内通知を生成します。

## <a name="see-also"></a>関連項目

* [会議用のビルド タブ](~/apps-in-teams-meetings/build-tabs-for-meeting.md)
* [Teams 会議ステージ用のアプリを構築する](build-apps-for-teams-meeting-stage.md)
* [会議チャット用の拡張可能な会話を構築する](build-extensible-conversation-for-meeting-chat.md)
* [匿名ユーザー向けのアプリを構築する](build-apps-for-anonymous-user.md)
* [高度な会議 API](meeting-apps-apis.md)
