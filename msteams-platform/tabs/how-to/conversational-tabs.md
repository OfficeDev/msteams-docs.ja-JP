---
title: 会話タブを作成する
author: surbhigupta
description: Microsoft Teams で会話タブを作成して、会話を開始、続行、拡張、閉じる方法について説明します。
ms.topic: conceptual
ms.author: lomeybur
ms.localizationpriority: high
ms.openlocfilehash: fa54221a413b19704d80ec62feb1cf068e42d1a0
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820123"
---
# <a name="create-conversational-tabs"></a>会話タブを作成する

会話サブエンティティは、ユーザーがタブ内のサブエンティティに関する会話を行えるようにする方法を提供します。特定のタスク、患者、営業案件など、タブ全体 (エンティティとも呼ばれます) について説明する代わりに。 従来のチャネルまたは構成可能なタブを使用すると、ユーザーはタブに関する会話を行うことができますが、より集中した会話が必要です。 集中型の会話の要件は、集中型のディスカッションができないコンテンツが多すぎる場合、またはコンテンツが時間の経過と同時に変化したために、表示されるコンテンツとは無関係な会話になる可能性があります。 会話サブエンティティは、動的タブに焦点を当てた会話エクスペリエンスを提供します。

会話サブエンティティは、チャネルでのみサポートされます。 個人用または静的タブから使用して、チャネルに既にピン留めされているタブで会話を作成または続行できます。 静的タブは、ユーザーが複数のチャネルで発生している会話を表示およびアクセスするための 1 つの場所を指定する場合に便利です。

## <a name="prerequisites"></a>前提条件

会話型サブエンティティをサポートするには、タブ Web アプリケーションに、バックエンド データベース内のサブエンティティ↔の会話間のマッピングを格納する機能が必要です。 `conversationId`は提供されますが、ユーザーが会話を続けるには、それを`conversationId`格納して Teams に返す必要があります。

## <a name="start-a-new-conversation"></a>新しい会話を開始する

新しい会話を開始するには、 関数を使用します `openConversation()` 。 会話の開始と継続はすべて、このメソッドによって処理されます。 関数への入力は、ユーザーの観点から見ると、会話を開始したり会話を続けたりするために、画面の右側にある会話パネルを開くアクションによって変わります。

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation** は、チャネルで会話を開始するために次の入力を受け取ります。

* **subEntityId**: 特定のサブエンティティの ID。 たとえば、task-123 です。
* **entityId**: タブ インスタンスの作成時の ID。 ID は、同じタブ インスタンスを参照するために重要です。
* **channelId**: タブ インスタンスが存在するチャネル。
   > [!NOTE]
   > **channelId** はチャネル タブでは省略可能です。 ただし、チャネルと静的タブ間で実装を同じにしておく場合は、お勧めします。
* **title**: チャット パネルでユーザーに表示されるタイトル。

これらの値のほとんどは、API (`microsoftTeams.getContext()`TeamsJS v1) から[`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true)取得することもできます。 詳細については、「[PageInfo インターフェイス](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true)」を参照してください。

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

次の図は、会話パネルを示しています。

:::image type="content" source="../../assets/images/tabs/conversational-subentities/start-conversation.png" alt-text="会話を開始する":::

ユーザーが会話を開始する場合は、そのイベントのコールバックをリッスンして **conversationId** を取得して保存することが重要です。

```javascript
⁠microsoftTeams.conversations.openConversation({
    ...,
    onStartConversation: (conversationResponse) => {
        ⁠// console.log(conversationResponse)
    },
});
```

オブジェクトには `conversationResponse` 、開始された会話に関連する情報が含まれています。 後で使用するために、この応答オブジェクトのすべてのプロパティを保存することをお勧めします。

## <a name="continue-a-conversation"></a>会話を続ける

会話が開始されると、後続の呼び出し `openConversation()` が必要になります。新 [しい会話の開始](#start-a-new-conversation)時と同じ入力も提供しますが、 **conversationId** も含めます。 適切な会話が表示されたユーザーの会話パネルが開きます。 ユーザーは、新しいメッセージまたは受信メッセージをリアルタイムで表示できます。

次の図は、適切な会話を含む会話パネルを示しています。

:::image type="content" source="../../assets/images/tabs/conversational-subentities/continue-conversation.png" alt-text="会話を続ける":::

## <a name="enhance-a-conversation"></a>会話を強化する

タブには [、サブエンティティへのディープ リンクが](~/concepts/build-and-test/deep-links.md)含まれていることが重要です。 たとえば、チャネル会話からタブ chiclet ディープ リンクを選択するユーザーなどです。 想定される動作は、ディープ リンクを受信し、そのサブエンティティを開き、そのサブエンティティの会話パネルを開きます。

個人用または静的タブの会話サブエンティティをサポートするには、実装で何も変更する必要はありません。 既にピン留めされているチャネル タブからの会話の開始または継続のみがサポートされます。 静的タブをサポートすると、ユーザーがすべてのサブエンティティと対話するための 1 つの場所を提供できます。 静的タブで会話ビューを`subEntityId`開くときに適切なプロパティを持つには、タブが最初にチャネルに作成されたときに、 、 `entityId``channelId` を保存することが重要です。

## <a name="close-a-conversation"></a>会話を閉じる

関数を呼び出すことで、会話ビューを `closeConversation()` 手動で閉じることができます。

```javascript
microsoftTeams.conversations.closeConversation();
```

また、ユーザーが会話ビューで **[閉じる (X)]** を選択したときにイベントをリッスンすることもできます。

```javascript
⁠microsoftTeams.conversations.openConversation({
    ...,
    onCloseConversation: (conversationResponse) => {
        ⁠// console.log(conversationResponse)
    },
});
```

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | C# |Node.js|
|-------------|-------------|------|----|
|[会話の作成] タブ| [会話の作成] タブを示す Microsoft Teams タブ サンプル アプリ。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タブ余白の変更](~/resources/removing-tab-margins.md)

## <a name="see-also"></a>関連項目

* [Teams の [ビルド] タブ](../what-are-tabs.md)
* [プライベート タブを作成する](create-personal-tab.md)
* [チャネル タブまたはグループ タブを作成する](create-channel-group-tab.md)
* [アダプティブ カードを使用してタブをビルドする](build-adaptive-card-tabs.md)
* [モバイルのタブ](~/tabs/design/tabs-mobile.md)
