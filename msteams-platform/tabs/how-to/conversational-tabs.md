---
title: 会話タブを作成する
author: surbhigupta
description: コード サンプルを使用して会話を管理するために、チャネル タブの会話サブエンティ チャットを作成する方法について学習します。
keywords: teams タブ チャネル構成可能
ms.topic: conceptual
ms.author: lomeybur
ms.localizationpriority: none
ms.openlocfilehash: 63f6310faa4bec78f246857cbd7c1368acee8edf
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889364"
---
# <a name="create-conversational-tabs"></a>会話タブを作成する

会話のサブエンテリティは、ユーザーがタブ内のサブエンテリティに関する会話を行う方法を提供します。特定のタスク、患者、販売機会など、タブ全体 (エンティティとも呼ばれる) を議論する代わりに。 従来のチャネルまたは構成可能なタブを使用すると、ユーザーはタブに関する会話を行えますが、ユーザーは、より集中した会話を必要とします。 一元的なディスカッションを行うコンテンツが多すぎる場合、または時間の間にコンテンツが変更され、表示されるコンテンツに関係のない会話になる場合、より集中した会話の要件が発生する可能性があります。 会話のサブエンテリティは、動的タブに対して、より集中した会話エクスペリエンスを提供します。

会話のサブエンテリティは、チャネルでのみサポートされます。 これらは、個人用タブまたは静的タブから使用して、チャネルに既にピン留めされているタブで会話を作成または続行できます。 静的タブは、ユーザーが複数のチャネルで発生する会話を表示およびアクセスするために 1 つの場所を提供する場合に便利です。

## <a name="prerequisites"></a>前提条件

会話のサブエンテリティをサポートするには、タブ Web アプリケーションがバックエンド データベース内のサブ↔マッピングを格納できる必要があります。 は指定されますが、ユーザーが会話を続行するには、Teamsを保存して返 `conversationId` `conversationId` す必要があります。

## <a name="start-a-new-conversation"></a>新しい会話を開始する

新しい会話を開始するには、関数を使用 `openConversation()` します。 会話の開始と続行はすべて、このメソッドによって処理されます。 関数への入力は、ユーザーの観点から、会話を開始するか、会話を続行するために、画面の右側に会話パネルを開きます。

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation は、** チャネルで会話を開始するために次の入力を受け取る。

* **subEntityId**: 特定のサブエンティの ID。 たとえば、task-123。
* **entityId**: 作成されたタブ インスタンスの ID。 ID は、同じタブ インスタンスを参照することが重要です。
* **channelId**: タブ インスタンスが存在するチャネル。
   > [!NOTE]
   > **channelId は**、チャネル タブのオプションです。 ただし、チャネルと静的タブ間で実装を同じにしておきたい場合は、お勧めします。
* **title**: チャット パネルでユーザーに表示されるタイトル。

これらの値の大部分は、API から取得 `getContext` することもできます。

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

次の図は、会話パネルを示しています。

![会話サブエンティティ - 会話の開始](~/assets/images/tabs/conversational-subentities/start-conversation.png)

ユーザーが会話を開始する場合は、そのイベントのコールバックをリッスンして conversationId を取得して保存することが **重要です**。

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

オブジェクト `conversationResponse` には、開始された会話に関連する情報が含まれる。 後で使用するために、この応答オブジェクトのすべてのプロパティを保存してください。

## <a name="continue-a-conversation"></a>会話を続ける

会話が開始されると、その後の呼び出しが必要になります。また、新しい会話を開始する場合と同じ入力を入力しますが `openConversation()` **、conversationId も含まれます**。 [](#start-a-new-conversation) 適切な会話が表示されているユーザーの会話パネルが開きます。 ユーザーは、新しいメッセージまたは受信メッセージをリアルタイムで表示できます。

次の図は、適切な会話を含む会話パネルを示しています。

![会話サブエンティティ - 会話の継続](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a>会話を強化する

タブにサブエンティへの [深いリンクが含まれる必要があります](~/concepts/build-and-test/deep-links.md)。 たとえば、チャネル会話からタブ のシックレットディープ リンクを選択したユーザー。 想定される動作は、ディープ リンクを受信し、そのサブエンティを開き、そのサブエンティの会話パネルを開きます。

個人用タブまたは静的タブから会話のサブエンテリティをサポートするには、実装内で何も変更する必要はありません。 既にピン留めされているチャネル タブからの会話の開始または継続のみをサポートします。 静的タブをサポートすることで、ユーザーがすべてのサブエンテリティを操作するための単一の場所を提供できます。 静的タブで会話ビューを開く際に適切なプロパティを持つには、チャネル内にタブが最初に作成されている場合に、、を保存することが `subEntityId` `entityId` `channelId` 重要です。

## <a name="close-a-conversation"></a>会話を閉じる

関数を呼び出すことによって、会話ビューを手動で閉 `closeConversation()` じできます。

```javascript
microsoftTeams.conversations.closeConversation();
```

ユーザーが会話ビューを閉じたときにイベントをリッスンできます。

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | C# |Node.js|
|-------------|-------------|------|----|
|[会話の作成] タブ| Microsoft Teams作成タブを示すタブ サンプル アプリを作成します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [タブ余白の変更](~/resources/removing-tab-margins.md)

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
* [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)
