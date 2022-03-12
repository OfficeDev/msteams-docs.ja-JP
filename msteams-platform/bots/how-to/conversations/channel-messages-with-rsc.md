---
title: RSC のチャネル メッセージをすべて受信する
author: surbhigupta12
description: RSC アクセス許可を持つすべてのチャネル メッセージを受信する
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: b18b4f64d34abc1dec71c526c1f604978dc77cdf
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453454"
---
# <a name="receive-all-channel-messages-with-rsc"></a>RSC のチャネル メッセージをすべて受信する

リソース固有の同意 (RSC) アクセス許可モデルは、もともと api 用に開発Teams Graphボット シナリオに拡張されています。

RSC を使用すると、ボットがチーム内の標準チャネル間でユーザー メッセージを受信する同意をチームの所有者に要求@mentioned。 この機能は、アプリで有効`ChannelMessage.Read.Group`になっている RSC のマニフェストでアクセス許可をTeamsします。 構成後、チームの所有者はアプリのインストール プロセス中に同意を付与できます。

アプリで RSC を有効にする方法の詳細については、「リソース固有の同意」を参照[Teams。](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest)

## <a name="enable-bots-to-receive-all-channel-messages"></a>ボットがすべてのチャネル メッセージを受信可能にする

`ChannelMessage.Read.Group` RSC アクセス許可はボットに拡張されます。 ユーザーの同意を得た場合、このアクセス許可を使用すると、グラフ アプリケーションは会話内のすべてのメッセージを取得し、ボットはメッセージにアクセスせずにすべてのチャネル メッセージを受信@mentioned。

> [!NOTE]
>
> * すべてのメッセージ データにアクセスする必要Teamsサービスは、チャネルやチャットでアーカイブされたデータGraphアクセスできる api を使用する必要があります。
> * ボットは、チーム内の `ChannelMessage.Read.Group` ユーザーの魅力的なエクスペリエンスを構築および強化するために、RSC アクセス許可を適切に使用する必要があります。または、ユーザーがストアの承認に合格しない必要があります。 アプリの説明には、ボットが読み取ったデータを使用する方法が含まれる必要があります。
> * 大量 `ChannelMessage.Read.Group` の顧客データを抽出する方法として、RSC アクセス許可をボットで使用することはできません。

## <a name="update-app-manifest"></a>アプリ マニフェストの更新

ボットがすべてのチャネル メッセージを受信するには、プロパティで指定されたアクセス許可を持つ Teamsアプリ マニフェストで RSC `ChannelMessage.Read.Group` を構成する必要`webApplicationInfo`があります。
![アプリ マニフェストの更新](~/bots/how-to/conversations/Media/appmanifest.png)

オブジェクトの例を次に示 `webApplicationInfo` します。

* **id**: Microsoft Azure Active Directory (Azure AD) アプリ ID。 これは、ボット ID と同じものにできます。
* **resource**: 任意の文字列。 このフィールドは RSC で操作を行う必要がありますが、エラー応答を回避するには、値を追加する必要があります。
* **applicationPermissions**: アプリの RSC アクセス許可を `ChannelMessage.Read.Group` 指定する必要があります。 詳細については、「リソース固有 [のアクセス許可」を参照してください](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)。

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

## <a name="sideload-in-a-team"></a>チームのサイドロード

テストするチームにサイドロードするには、RSC を持つチーム内のすべてのチャネル メッセージを、次の方法で受信@mentioned。

1. チームを選択または作成します。
1. 左側のウィンドウから &#x25CF;&#x25CF;&#x25CF; 省略記号を選択します。 ドロップダウン メニューが表示されます。
1. ドロップダウン **メニューから [チーム** の管理] を選択します。 詳細が表示されます。

   ![チームでのアプリの管理](~/bots/how-to/conversations/Media/managingteam.png)

1. **[アプリ]** を選択します。 複数のアプリが表示されます。
1. 右下 **アップロードカスタム アプリを** 選択します。

    ![カスタム アプリのアップロード](~/bots/how-to/conversations/Media/uploadingcustomapp.png)

1. [開く] ダイアログ ボックスから **アプリ パッケージを** 選択します。
1. [**開く**]を選択します。

    ![アプリ パッケージの選択](~/bots/how-to/conversations/Media/selectapppackage.png)

1. アプリ **の詳細** ポップアップから [追加] を選択して、選択したチームにボットを追加します。

    ![ボットの追加](~/bots/how-to/conversations/Media/addingbot.png)

1. チャネルを選択し、ボットのチャネルにメッセージを入力します。

    ボットは、メッセージを受信せずにメッセージを@mentioned。

    ![ボットがメッセージを受信する](~/bots/how-to/conversations/Media/botreceivingmessage.png)

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
|RSC アクセス許可を持つチャネル メッセージ| Microsoft Teams、ボットが RSC を使用してすべてのチャネル メッセージを受信する方法を示すサンプル アプリ@mentioned。| [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## <a name="see-also"></a>関連項目

* [ボットの会話](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [リソース固有の同意](/microsoftteams/resource-specific-consent)
* [リソース固有の同意をテストする](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [アップロードカスタム アプリのTeams](~/concepts/deploy-and-publish/apps-upload.md)
