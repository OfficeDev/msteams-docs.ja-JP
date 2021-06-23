---
title: 会話タブを作成する
author: surbhigupta
description: チャネル タブの会話型サブエンティティ チャットを作成する
keywords: teams タブ チャネル構成可能
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: 343cbe26ded2792489640ae3d86ec94c7c6db72b
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069227"
---
# <a name="create-conversational-tabs"></a>会話タブを作成する

会話サブエンティティは、ユーザーがタブ全体 (エンティティとも呼ばれる) を議論する代わりに、特定のタスク、患者、販売機会などのサブエンティティに関する会話をタブ内で行う方法を提供します。 従来のチャネルまたは構成可能なタブを使用すると、ユーザーはタブに関する会話を行えますが、ユーザーは、より集中した会話を望む場合があります。 一元的なディスカッションを行うコンテンツが多すぎる場合や、時間の間にコンテンツが変更された場合に、より集中した会話の要件が発生し、表示されるコンテンツに関係ありません。 会話サブエンティティは、動的タブに対して、より集中した会話エクスペリエンスを提供します。

会話型サブエンティティはチャネルでのみサポートされます。 ただし、個人タブまたは静的タブから使用して、チャネルに既にピン留めされているタブで会話を作成または続行できます。 静的タブは、ユーザーが複数のチャネルで発生する会話を表示およびアクセスするために 1 つの場所を提供する場合に便利です。

## <a name="prerequisites"></a>前提条件

会話型サブエンティティをサポートするには、タブ Web アプリケーションがバックエンド データベース内のサブエンティティと会話間のマッピング↔する機能が必要です。 弊社は、お客様に提供しますが、ユーザーが会話を継続するために、その情報を保存し、Teamsに戻す責任 `conversationId` `conversationId` があります。

## <a name="start-a-new-conversation"></a>新しい会話を開始する

新しい会話を開始するには、関数を使用 `openConversation()` します。 会話の開始と継続は、すべてこのメソッドによって処理されます。ただし、関数への入力は、実行するアクションに応じて変わります。 ユーザーの観点から、会話を開始するか、会話を続行するために、画面の右側に会話パネルが開きます。

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation は、** チャネルで会話を開始するために次の入力を受け取る。

* **subEntityId**: これは、特定のサブエンティティの ID です。 たとえば、task-123。
* **entityId**: これは、作成されたタブ インスタンスの ID です。 ID は、同じタブ インスタンスを参照することが重要です。
* **channelId**: これは、タブ インスタンスが存在するチャネルです。
   > [!NOTE]
   > **channelId は**、チャネル タブのオプションです。 ただし、チャネルと静的タブ間で実装を同じに維持する場合は、お勧めします。
* **title**: これは、チャット パネルでユーザーに表示されるタイトルです。

これらの値の大部分は、API から取得 `getContext` することもできます。

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

これにより、会話パネルが開きます。

![Conversationl Sub Entities - 会話の開始](~/assets/images/tabs/conversational-subentities/start-conversation.png)

ユーザーが会話を開始する場合は、conversationId を取得して保存するために、そのイベントのコールバックをリッスンすることが **重要です**。

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

オブジェクト `conversationReponse` には、開始し始めた会話に関連する情報が含まれる。 後で再利用するために、この応答オブジェクトのすべてのプロパティを保存することをお勧めします。

## <a name="continue-a-conversation"></a>会話を続ける

会話の開始後、以降の呼び出しでは、[新しいチャネル タブの会話を開始する] と同じ入力を入力する必要がありますが `openConversation()` **、conversationId も含める必要があります**。 [](#Starting a new channel tab conversation) 適切な会話が表示されているユーザーの会話パネルが開きます。 ユーザーは、新しいメッセージまたは受信メッセージをリアルタイムで表示できます。

![Conversationl Sub Entities - Continue Conversation](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a>会話を強化する

最後に、タブがサブエンティティへのディープリンクを使用 [することが重要です](~/concepts/build-and-test/deep-links.md)。 たとえば、チャネル会話からタブ のシックレットディープリンクをクリックするとします。 想定される動作は、ディープリンクを受信し、そのサブエンティティを開き、その特定のサブエンティティの会話パネルを開く動作です。

個人タブまたは静的タブから会話サブエンティティをサポートするには、実装について何も変更する必要はありません。 既にピン留めされているチャネル タブからの会話の開始または継続のみをサポートします。 静的タブをサポートすると、ユーザーがすべてのサブエンティティを操作するための 1 つの場所を提供できます。 ただし、静的タブで会話ビューを開く際に適切なプロパティを持つには、チャネル内にタブが最初に作成されている場合に、 を保存することが `subEntityId` `entityId` 重要です `channelId` 。

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
