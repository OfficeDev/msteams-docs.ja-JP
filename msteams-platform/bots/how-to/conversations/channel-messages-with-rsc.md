---
title: RSC のチャネル メッセージをすべて受信する
author: surbhigupta12
description: ボットが RSC アクセス許可を使用して@mentionedすることなく、すべてのチャネル メッセージを受信できるようにします。 マニフェストの webApplicationInfo または承認セクションを参照してください。
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: db51bcddaa22a115330129ddc677f0401c8bd523
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2022
ms.locfileid: "67586911"
---
# <a name="receive-all-channel-messages-with-rsc"></a>RSC のチャネル メッセージをすべて受信する

Teams Graph API 用にもともと開発されたリソース固有の同意 (RSC) アクセス許可モデルは、ボットのシナリオに拡張されています。

RSC を使用して、チームの所有者に対して、@mention することなく、チーム内の標準チャネル間でユーザー メッセージを受信することにボットが同意するように要求できるようになりました。 この機能は、RSC 対応 Teams アプリのマニフェストで `ChannelMessage.Read.Group` アクセス許可を指定することで有効になります。 構成後、チーム所有者はアプリのインストール プロセス中に同意を付与できます。

アプリの RSC を有効にする方法の詳細については、[Teams のリソース固有の同意](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest)に関するページを参照してください。

## <a name="enable-bots-to-receive-all-channel-messages"></a>ボットがすべてのチャネル メッセージを受信できるようにする

`ChannelMessage.Read.Group` RSC アクセス許可はボットに拡張されます。 このアクセス許可により、グラフ アプリケーションは会話内のすべてのメッセージを取得し、ボットは @メンションすることなくすべてのチャネル メッセージを受信できます。

> [!NOTE]
>
> * すべての Teams メッセージ データにアクセスする必要があるサービスでは、チャネルやチャットでアーカイブされたデータへのアクセスを提供する Graph API を使用する必要があります。
> * ボットは、チーム内の `ChannelMessage.Read.Group` ユーザーの魅力的なエクスペリエンスを構築および強化するために RSC アクセス許可を適切に使用する必要があります。または、ストアの承認を渡しません。 アプリの説明には、ボットが読み取るデータの使用方法を含める必要があります。
> * `ChannelMessage.Read.Group` RSC アクセス許可は、大量の顧客データを抽出する方法としてボットで使用することはできません。

## <a name="update-app-manifest"></a>アプリ マニフェストの更新

ボットがすべてのチャネル メッセージを受信するには、Teams アプリ マニフェストで `webApplicationInfo` プロパティで指定された `ChannelMessage.Read.Group` 権限を使用して RSC を構成する必要があります。

:::image type="content" source="~/bots/how-to/conversations/Media/appmanifest.png" alt-text="アプリ マニフェストの更新のスクリーンショット。":::

`webApplicationInfo` オブジェクトの例を次に示します。

* **id**: Microsoft Azure Active Directory (Azure AD) アプリ ID。 これは、ボット ID と同じにすることができます。
* **resource**: 任意の文字列。 このフィールドには RSC での操作はありませんが、エラー応答を回避するために追加して値を指定する必要があります。
* **applicationPermissions**: `ChannelMessage.Read.Group` を使用したアプリの RSC 権限を指定する必要があります。 詳細については、「[リソース固有のアクセス許可](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)」を参照してください。

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

テストするチームにサイドローディングするには、RSC を使用するチーム内のすべてのチャネル メッセージを @メンションせずに受信するかどうかを指定します。

1. チームを選択または作成します。
1. 左側のウィンドウから省略記号 &#x25CF;&#x25CF;&#x25CF; を選択します。 ドロップダウン メニューが表示されます。
1. ドロップダウン メニューから **[表示]** を選択します。 アプリの詳細が表示されます。

   :::image type="content" source="Media/managingteam.png" alt-text="Teams アプリケーションでのチームオプションの管理のスクリーンショット。":::

1. **[アプリ]** を選択します。 複数のアプリが表示されます。

1. 右下から **[カスタム アプリのアップロード]** を選択します

      :::image type="content" source="Media/uploadingcustomapp.png" alt-text="カスタム アプリ オプションをアップロードするスクリーンショット。":::
  
1. **[開く]** ダイアログ ボックスからアプリ パッケージを選択します。

1. [**開く**]を選択します。

      :::image type="content" source="Media/selectapppackage.png" alt-text="開いているダイアログ ボックスのスクリーンショット。アプリ パッケージを選択します。" lightbox="Media/selectapppackage.png":::

1. アプリの詳細ポップアップから **[追加]** を選択し、選択したチームにボットを追加します。

      :::image type="content" source="Media/addingbot.png" alt-text="チームにボットを追加する [追加] ボタンのスクリーンショット。" lightbox="Media/addingbot.png":::

1. チャネルを選択し、ボットのチャネルにメッセージを入力します。

    ボットは、@メンションされずにメッセージを受信します。

      :::image type="content" source="Media/botreceivingmessage.png" alt-text="チャネルでメッセージを受信しているボットのスクリーンショット。" lightbox="Media/botreceivingmessage.png":::

## <a name="code-snippets"></a>コード スニペット

次のコードは、アプリケーション エラーの理由の例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text("Using RSC the bot can receive messages across channels in team without being @mentioned."));
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
this.onMessage(async (context, next) => {
   await context.sendActivity(MessageFactory.text("Using RSC the bot can receive messages across channles in team without being @mentioned."))
   await next();
});
```

---

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | C# |Node.js|
|-------------|-------------|------|----|
|RSC アクセス許可を持つチャネル メッセージ| Microsoft Teams のサンプル アプリは、ボットが @メンションされることなく RSC を使用してすべてのチャネル メッセージを受信する方法を示しています。| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## <a name="see-also"></a>関連項目

* [ボットの会話](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [リソース固有の同意](/microsoftteams/resource-specific-consent)
* [リソース固有の同意のアクセス許可をテストする](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Teams にカスタム アプリをアップロードする](~/concepts/deploy-and-publish/apps-upload.md)
* [チャネル内のメッセージに対する返信を一覧表示する](/graph/api/chatmessage-list-replies?view=graph-rest-1.0&tabs=http&preserve-view=true)
