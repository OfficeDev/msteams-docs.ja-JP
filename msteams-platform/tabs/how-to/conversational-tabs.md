---
title: 会話タブを作成する
author: surbhigupta
description: チャネル タブの会話サブエンティティ チャットを作成し、コード サンプルを使用して会話を管理する方法について説明します
keywords: teams タブ チャネル構成可能
ms.topic: conceptual
ms.author: lomeybur
ms.localizationpriority: medium
ms.openlocfilehash: ddf14d9d7dabe5b20cc21181783dc5c33f29eff9
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111655"
---
# <a name="create-conversational-tabs"></a>会話タブを作成する

会話サブエンティティは、ユーザーがタブ内のサブエンティティに関する会話を行えるようにする方法を提供します。エンティティとも呼ばれるタブ全体について話し合うのではなく、特定のタスク、患者、営業案件などです。 従来のチャネルまたは構成可能なタブを使用すると、ユーザーはタブに関する会話を行うことができますが、ユーザーにはより集中した会話が必要です。 より集中的な会話の要件は、一元的なディスカッションを行うためにコンテンツが多すぎる場合、またはコンテンツが時間の経過と共に変化し、表示されるコンテンツと無関係になるために発生する可能性があります。 会話サブエンティティは、動的タブに対してより集中した会話エクスペリエンスを提供します。

会話のサブエンティティは、チャネルでのみサポートされます。 これらは、個人用タブまたは静的タブから使用して、チャネルに既にピン留めされているタブで会話を作成または続行できます。 静的タブは、ユーザーが複数のチャネルで発生している会話を表示してアクセスするための 1 つの場所を指定する場合に便利です。

## <a name="prerequisites"></a>前提条件

会話のサブエンティティをサポートするには、タブ Web アプリケーションでバックエンド データベース内のサブエンティティ↔会話間のマッピングを格納する機能が必要です。 これは`conversationId`提供されていますが、ユーザーが会話を続行するには、それを`conversationId`保存してTeamsに返す必要があります。

## <a name="start-a-new-conversation"></a>新しい会話を開始する

新しい会話を開始するには、関数を使用します `openConversation()` 。 会話の開始と続行はすべて、このメソッドによって処理されます。 ユーザーの観点から、実行するアクションに応じて関数への入力が変わります。これにより、会話を開始するか会話を続行するか、画面の右側に会話パネルが開きます。

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation は、** チャネルで会話を開始するために次の入力を受け取ります。

* **subEntityId**: 特定のサブエンティティの ID。 たとえば、task-123 です。
* **entityId**: タブ インスタンスが作成されたときの ID。 ID は、同じタブ インスタンスを参照するために重要です。
* **channelId**: タブ インスタンスが存在するチャネル。
   > [!NOTE]
   > チャネル タブの **channelId** は省略可能です。 ただし、チャネルタブと静的タブ間で実装を維持する場合は、同じ方法をお勧めします。
* **title**: チャット パネルでユーザーに表示されるタイトル。

これらの値のほとんどは、API から `getContext` 取得することもできます。

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

次の図は、会話パネルを示しています。

![Conversational サブエンティティ - 会話を開始する](~/assets/images/tabs/conversational-subentities/start-conversation.png)

ユーザーが会話を開始する場合は、そのイベントのコールバックをリッスンして **conversationId** を取得して保存することが重要です。

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

`conversationResponse`オブジェクトには、開始された会話に関連する情報が含まれています。 後で使用できるように、この応答オブジェクトのすべてのプロパティを保存することをお勧めします。

## <a name="continue-a-conversation"></a>会話を続行する

会話が開始されると、後続の呼び出し `openConversation()` が必要になります。また、 [新しい会話を開始](#start-a-new-conversation)する場合と同じ入力を指定するだけでなく、 **conversationId** も含めます。 適切な会話が表示されているユーザーの会話パネルが開きます。 ユーザーは、新規メッセージまたは受信メッセージをリアルタイムで表示できます。

次の図は、適切な会話を含む会話パネルを示しています。

![Conversational サブエンティティ - 会話を続行する](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a>会話を強化する

タブにサブ [エンティティへのディープ リンクが含まれていることが重要です](~/concepts/build-and-test/deep-links.md)。 たとえば、ユーザーがチャネル会話からタブ シックレットディープ リンクを選択します。 必要な動作は、ディープ リンクを受け取り、そのサブエンティティを開き、そのサブエンティティの会話パネルを開く動作です。

個人用タブまたは静的タブから会話サブエンティティをサポートするために、実装で何も変更する必要はありません。 既にピン留めされているチャネル タブからの会話の開始または継続のみがサポートされます。 静的タブをサポートすると、ユーザーがすべてのサブエンティティと対話するための 1 つの場所を提供できます。 静的タブで会話ビューを`subEntityId``entityId``channelId`開くときに適切なプロパティを持つチャネルでタブが最初に作成されたときに、保存することが重要です。

## <a name="close-a-conversation"></a>会話を閉じる

関数を呼び出 `closeConversation()` すことで、会話ビューを手動で閉じることができます。

```javascript
microsoftTeams.conversations.closeConversation();
```

また、会話ビューがユーザーによって閉じられるときにイベントをリッスンすることもできます。

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | C# |Node.js|
|-------------|-------------|------|----|
|[会話の作成] タブ| 会話の作成タブをデモンストレーションするためのタブ サンプル アプリをMicrosoft Teamsします。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブ余白の変更](~/resources/removing-tab-margins.md)

## <a name="see-also"></a>関連項目

* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループの作成] タブ](~/tabs/how-to/create-channel-group-tab.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
* [アダプティブ カードを使用してタブをビルドする](~/tabs/how-to/build-adaptive-card-tabs.md)
