---
title: 会話タブを作成する
author: surbhigupta
description: チャネル タブの会話型サブエンティティ チャットを作成する
keywords: teams タブ チャネル構成可能
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: fbc5e90842c892cfb7e14f845563d7d2ffb397bb
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140265"
---
# <a name="create-conversational-tabs"></a>会話タブを作成する

会話サブエンティティは、ユーザーがタブ全体 (エンティティとも呼ばれる) を議論する代わりに、特定のタスク、患者、販売機会などのサブエンティティに関する会話をタブ内で行う方法を提供します。 従来のチャネルまたは構成可能なタブを使用すると、ユーザーはタブに関する会話を行えますが、ユーザーは、より集中した会話を必要とします。 一元的なディスカッションを行うコンテンツが多すぎる場合、または時間の間にコンテンツが変更され、表示されるコンテンツに関係のない会話になる場合、より集中した会話の要件が発生する可能性があります。 会話サブエンティティは、動的タブに対して、より集中した会話エクスペリエンスを提供します。

会話型サブエンティティはチャネルでのみサポートされます。 これらは、個人用タブまたは静的タブから使用して、チャネルに既にピン留めされているタブで会話を作成または続行できます。 静的タブは、ユーザーが複数のチャネルで発生する会話を表示およびアクセスするために 1 つの場所を提供する場合に便利です。

## <a name="prerequisites"></a>前提条件

会話型サブエンティティをサポートするには、タブ Web アプリケーションがバックエンド データベース内のサブエンティティと会話間のマッピング↔する機能が必要です。 は指定されますが、ユーザーが会話を続行するには、Teamsを保存して返 `conversationId` `conversationId` す必要があります。

## <a name="start-a-new-conversation"></a>新しい会話を開始する

新しい会話を開始するには、関数を使用 `openConversation()` します。 会話の開始と続行はすべて、このメソッドによって処理されます。 関数への入力は、実行するアクションに応じて変わります。 ユーザーの観点から、会話を開始するか、会話を続行するために、画面の右側に会話パネルが開きます。

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation は、** チャネルで会話を開始するために次の入力を受け取る。

* **subEntityId**: これは、特定のサブエンティティの ID です。 たとえば、task-123。
* **entityId**: これは、作成されたタブ インスタンスの ID です。 ID は、同じタブ インスタンスを参照することが重要です。
* **channelId**: これは、タブ インスタンスが存在するチャネルです。
   > [!NOTE]
   > **channelId は**、チャネル タブのオプションです。 ただし、チャネルと静的タブ間で実装を同じにしておきたい場合は、お勧めします。
* **title**: これは、チャット パネルでユーザーに表示されるタイトルです。

これらの値の大部分は、API から取得 `getContext` することもできます。

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

次の図は、会話パネルを示しています。

![会話サブエンティティ - 会話の開始](~/assets/images/tabs/conversational-subentities/start-conversation.png)

ユーザーが会話を開始する場合は、conversationId を取得して保存するために、そのイベントのコールバックをリッスンすることが **重要です**。

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

オブジェクト `conversationResponse` には、開始された会話に関連する情報が含まれる。 後で使用するために、この応答オブジェクトのすべてのプロパティを保存してください。

## <a name="continue-a-conversation"></a>会話を続ける

会話の開始後、以降の呼び出しでは、新しい会話を開始する場合と同じ入力を入力する必要がありますが `openConversation()` **、conversationId も含める必要があります**。 [](#start-a-new-conversation) 適切な会話が表示されているユーザーの会話パネルが開きます。 ユーザーは、新しいメッセージまたは受信メッセージをリアルタイムで表示できます。

次の図は、適切な会話を含む会話パネルを示しています。

![会話サブエンティティ - 会話の継続](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a>会話を強化する

タブにサブエンティティへのディープリンクが [含まれる必要があります](~/concepts/build-and-test/deep-links.md)。 たとえば、チャネル会話からタブ シックレット ディープリンクを選択したユーザー。 想定される動作は、ディープリンクを受信し、そのサブエンティティを開き、そのサブエンティティの会話パネルを開きます。

個人タブまたは静的タブから会話サブエンティティをサポートするには、実装で何も変更する必要はありません。 既にピン留めされているチャネル タブからの会話の開始または継続のみをサポートします。 静的タブをサポートすることで、ユーザーがすべてのサブエンティティを操作するための 1 つの場所を提供できます。 静的タブで会話ビューを開く際に適切なプロパティを持つには、チャネル内にタブが最初に作成されている場合に、 を保存することが `subEntityId` `entityId` `channelId` 重要です。

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

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [前提条件](~/tabs/how-to/tab-requirements.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [コンテンツ ページを作成する](~/tabs/how-to/create-tab-pages/content-page.md)
* [構成ページを作成する](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [タブの削除ページを作成する](~/tabs/how-to/create-tab-pages/removal-page.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
* [タブのコンテキストを取得する](~/tabs/how-to/access-teams-context.md)
* [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)
* [タブのリンクの展開とステージ ビュー](~/tabs/tabs-link-unfurling.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブ余白の変更](~/resources/removing-tab-margins.md)