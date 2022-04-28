---
title: RSC のチャネル メッセージをすべて受信する
author: surbhigupta12
description: RSC アクセス許可を持つすべてのチャネル メッセージを受信する
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: a78910b083943e5296f3e0d50eae00a713f194aa
ms.sourcegitcommit: e40383d9081bf117030f7e6270140e6b94214e8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65102075"
---
# <a name="receive-all-channel-messages-with-rsc"></a>RSC のチャネル メッセージをすべて受信する

Teams Graph API 用にもともと開発されたリソース固有の同意 (RSC) アクセス許可モデルは、ボットのシナリオに拡張されています。

RSC を使用して、チームの所有者に対して、@mentionedすることなく、チーム内の標準チャネル間でユーザー メッセージを受信することにボットが同意するように要求できるようになりました。 この機能は、RSC 対応Teams アプリのマニフェストでアクセス許可を指定`ChannelMessage.Read.Group`することで有効になります。 構成後、チーム所有者はアプリのインストール プロセス中に同意を付与できます。

アプリの RSC を有効にする方法の詳細については、[Teamsのリソース固有の同意に](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest)関するページを参照してください。

## <a name="enable-bots-to-receive-all-channel-messages"></a>ボットがすべてのチャネル メッセージを受信できるようにする

`ChannelMessage.Read.Group` RSC アクセス許可はボットに拡張されます。 このアクセス許可により、グラフ アプリケーションは会話内のすべてのメッセージを取得し、ボットは@mentionedすることなくすべてのチャネル メッセージを受信できます。

> [!NOTE]
>
> * すべてのTeamsメッセージ データにアクセスする必要があるサービスでは、チャネルやチャットでアーカイブされたデータへのアクセスを提供するGraph API を使用する必要があります。
> * ボットは、チーム内の `ChannelMessage.Read.Group` ユーザーの魅力的なエクスペリエンスを構築および強化するために RSC アクセス許可を適切に使用する必要があります。または、ストアの承認を渡しません。 アプリの説明には、ボットが読み取るデータの使用方法を含める必要があります。
> * RSC アクセス許可は `ChannelMessage.Read.Group` 、大量の顧客データを抽出する方法としてボットで使用することはできません。

## <a name="update-app-manifest"></a>アプリ マニフェストの更新

ボットですべてのチャネル メッセージを受信するには、プロパティで指定されたアクセス許可を使用して、Teams アプリ マニフェスト`ChannelMessage.Read.Group`で RSC を構成する`webApplicationInfo`必要があります。

![アプリ マニフェストの更新](~/bots/how-to/conversations/Media/appmanifest.png)


オブジェクトの例を次に `webApplicationInfo` 示します。

* **id**: Microsoft Azure Active Directory (Azure AD) アプリ ID。 これは、ボット ID と同じにすることができます。
* **resource**: 任意の文字列。 このフィールドには RSC での操作はありませんが、エラー応答を回避するために追加して値を指定する必要があります。
* **applicationPermissions**: アプリの RSC アクセス許可を `ChannelMessage.Read.Group` 指定する必要があります。 詳細については、 [リソース固有のアクセス許可に関するページを](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)参照してください。

次のコードは、アプリ マニフェストの例を示しています。

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team"></a>チーム内のサイドロード

テストするチームにサイドローディングするには、RSC を使用するチーム内のすべてのチャネル メッセージを@mentionedせずに受信するかどうかを指定します。

1. チームを選択または作成します。
1. 左側のウィンドウから省略記号 &#x25CF;&#x25CF;&#x25CF; を選択します。 ドロップダウン メニューが表示されます。
1. ドロップダウン メニューから [ **チームの管理** ] を選択します。 詳細が表示されます。

   ![チームでのアプリの管理](~/bots/how-to/conversations/Media/managingteam.png)

      :::image type="content" source="Media/managingteam.png" alt-text="チームの管理"border="true":::

1. **[アプリ]** を選択します。 複数のアプリが表示されます。
1. 右下隅から **カスタム アプリアップロード** 選択します。

      :::image type="content" source="Media/uploadingcustomapp.png" alt-text="カスタム アプリのアップロード":::
  
1. [ **開く** ] ダイアログ ボックスからアプリ パッケージを選択します。
1. [**開く**]を選択します。

      :::image type="content" source="Media/selectapppackage.png" alt-text="アプリ パッケージを選択する"lightbox="Media/selectapppackage.png"border="true":::

1. アプリの詳細ポップアップから [ **追加]** を選択し、選択したチームにボットを追加します。

      :::image type="content" source="Media/addingbot.png" alt-text="ボットの追加"lightbox="Media/addingbot.png"border="true":::

1. チャネルを選択し、ボットのチャネルにメッセージを入力します。

    ボットは、@mentionedされずにメッセージを受信します。

      :::image type="content" source="Media/botreceivingmessage.png" alt-text="メッセージを受信するボット"lightbox="Media/botreceivingmessage.png"border="true":::

## <a name="code-snippets"></a>コード スニペット

次のコードは、RSC アクセス許可の例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text("Using RSC the bot can recieve messages across channels in team without being @mentioned."));
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
this.onMessage(async (context, next) => {
   await context.sendActivity(MessageFactory.text("Using RSC the bot can recieve messages across channles in team without being @mentioned."))
   await next();
});
```

---

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | C# |Node.js|
|-------------|-------------|------|----|
|RSC アクセス許可を持つチャネル メッセージ| Microsoft Teams@mentionedすることなく、ボットが RSC を使用してすべてのチャネル メッセージを受信する方法を示すサンプル アプリです。| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## <a name="see-also"></a>関連項目

* [ボットの会話](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [リソース固有の同意](/microsoftteams/resource-specific-consent)
* [リソース固有の同意をテストする](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Teamsでカスタム アプリをアップロードする](~/concepts/deploy-and-publish/apps-upload.md)
