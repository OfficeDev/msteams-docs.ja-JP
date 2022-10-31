---
title: ボットと SDK
author: surbhigupta
description: この記事では、Microsoft Teams ボット用のツールと Bot Framework SDK (C#、Python、Java、JavaScript) について説明し、長所と短所について説明します。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 2a6e4201603bd30262cfcd275e8f995dcc730e9a
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791672"
---
# <a name="bots-and-sdks"></a>ボットと SDK

次のいずれかのツールまたは機能を使用して、Microsoft Teams で動作するボットを作成できます。

* [Microsoft Bot Framework SDK](#bots-with-the-microsoft-bot-framework)
* [Azure Active Directory](~/bots/how-to/authentication/auth-aad-sso-bots.md#develop-an-sso-teams-bot)
* [開発者ポータル](~/concepts/build-and-test/manage-your-apps-in-developer-portal.md#configure)
* [Power Virtual Agents](#bots-with-power-virtual-agents)
* [仮想アシスタント](~/samples/virtual-assistant.md)
* [Webhook とコネクタ](#bots-with-webhooks-and-connectors)

## <a name="bots-with-the-microsoft-bot-framework"></a>Microsoft Bot Framework を使用したボット

Teams ボットは以下から構成されます。

* お客様がホストし、公開している Web サービス。
* Web サービスの Bot Framework 登録。
* Teams クライアントを Web サービスに接続する、Teams アプリ パッケージ。

> [!TIP]
> 開発者ポータルを使用して Web サービスを Bot Framework に登録し、アプリの構成を指定します。 詳細については、「[Microsoft Teams の開発者ポータルを使用してアプリを管理する](~/concepts/build-and-test/teams-developer-portal.md)」を参照してください。

[Bot Framework](https://dev.botframework.com/) は、C#、Java、Python、JavaScript を使用してボットを作成するために使用される豊富な SDK です。 Bot Framework に基づくボットが既にある場合は、Teams で動作するようにボットを簡単に変更できます。 用意されている [SDK](/microsoftteams/platform/#pivot=sdk-tools) を活用するため、C# か Node.js を使用してください。 これらのパッケージは、基本的な Bot Builder SDK のクラスとメソッドを次のように拡張します。

* Office 365 コネクタ カードなどの専用のカードを使用する。
* アクティビティに関する Teams 固有のチャネル データを設定する。
* メッセージ拡張要求を処理する。

> [!IMPORTANT]
> You can develop Teams apps in any web programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly. But you must perform token handling in all cases.

## <a name="bots-with-power-virtual-agents"></a>Power Virtual Agents を使用したボット

[Power Virtual Agent](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) は、Microsoft Power platform および Bot Framework で構築された チャット ボット サービスです。 Power Virtual Agent の開発プロセスでは、ガイド付きのコーディングされていないグラフィカル インターフェイス アプローチを使用して、チーム メンバーが高度な仮想エージェントを簡単に作成して管理できるようにします。 [Power Virtual Agents ポータル](https://powervirtualagents.microsoft.com)でチャットボットを作成した後、簡単に [Teams と統合](how-to/add-power-virtual-agents-bot-to-teams.md) できます。 作業を開始する方法の詳細については、「[Power Virtual Agents のドキュメント](/power-virtual-agents)」を参照してください。

>[!NOTE]
>Microsoft Power Platform を使用して、Teams アプリ ストアに発行するアプリを作成することはできません。 Microsoft Power Platform アプリは、組織のアプリ ストアにのみ発行できます。

## <a name="bots-with-webhooks-and-connectors"></a>Webhook とコネクタを使用したボット

Webhook とコネクタは、ボットを Web サービスに接続します。 Webhook とコネクタを使用すると、ワークフローやその他のシンプルなコマンドの作成など、基本的なやり取りを行うためのボットを作成することができます。 これらは、作成するチームでのみ使用でき、会社のワークフローに固有の単純なプロセスを対象としています。 詳細については、「[Webhook とコネクタとは](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)」を参照してください。

## <a name="advantages-of-bots"></a>ボットの利点

Microsoft Teams のボットは、1 対 1 の会話、グループ チャット、チーム内のチャネルで扱うことができます。 各スコープに、会話ボット向けの機能と条件があります。

| チャネル | グループ チャット | 1 対 1 のチャット |
| :-- | :-- | :-- |
| 大規模なリーチ | 減少したメンバー | 従来の方法 |
| 簡潔な個々のやり取り | ボットへの @メンション  | Q&A ボット |
| ボットへの @メンション | チャネルと同様 | ジョークを言ったり、メモを取ったりするボット |

### <a name="in-a-channel"></a>チャネル

チャネルには、最大 2,000 人まで、複数のユーザーによるスレッド形式の会話が含まれます。 これにより、ボットが大規模になる可能性がでてきますが、それぞれの対話を簡潔にする必要があります。 従来のマルチターン操作は機能しません。 多くの情報を収集するためには、対話型カードまたはタスク モジュールを使用するか、1 対 1 の会話に変更する必要があります。 ボットは、 の `@mentioned`メッセージにのみアクセスできます。 Microsoft Graph および組織レベルのアクセス許可を使用して会話から追加のメッセージを取得できます。

ボットは、次の場合にチャネルで適切に機能します。

* ユーザーが追加情報を取得するための対話型カードを提供する通知。
* 投票やアンケート調査などのフィードバック シナリオ。
* 単一の要求または応答サイクルは対話を解決し、結果は複数のメンバーで会話をする場合に役立ちます。
* 素晴らしい猫の画像を取得したり、勝者をランダムに選んだりできる、交流または娯楽を目的としたボット。

### <a name="in-a-group-chat"></a>グループ チャット

グループ チャットは、3 人以上のユーザー同士で行われる非スレッドの会話です。 チャネルよりもメンバーは少なく、一時的な会話が多いのが特徴です。 チャネルと同様に、ボットは直接アクセスできるメッセージ `@mentioned` にのみアクセスできます。

チャネルでボットの方がうまく機能する場合は、グループ チャットでもうまく機能します。

### <a name="in-a-one-to-one-chat"></a>1 対 1 のチャット

1 対 1 のチャットは、会話ボットがユーザーとやり取りする従来の方法です。 1 対 1 の会話ボットの例を次に示します。

* Q&A ボット
* 他のシステムでワークフローを開始するボット。
* ジョークを伝えるボット。
* メモを取るボット。
1 対 1 のチャットボットを作成する前に、会話ベースのインターフェイスが機能を提示する最善の方法であるかどうかを検討してください。

## <a name="disadvantages-of-bots"></a>ボットの欠点

ボットとユーザーの間のダイアログが広範になると、タスクの完了に要する時間が長くなり、複雑になります。 過剰なコマンド (特に広範なコマンド) をサポートするボットは、成功しないか、ユーザーによって肯定的に表示されます。

### <a name="have-multi-turn-experiences-in-chat"></a>チャットではマルチターンのやり取りが交わされる

広範なダイアログでは、開発者が状態を維持する必要があります。 この状態を終了するには、ユーザーがタイムアウトするか、[ **キャンセル**] を選択する必要があります。 また、このプロセスは面倒です。 たとえば、次の会話シナリオを参照してください。

ユーザー: Megan との会議をスケジュールして。

ボット: 200 件の結果が見つかりました。苗字と名前を含めてください。

ユーザー: Megan Bowen との会議をスケジュールして。

ボット: かしこまりました。Megan Bowen との会議を何時にご希望ですか?

ユーザー: 午後 1 時に。

ボット: 何日のですか?

### <a name="support-too-many-commands"></a>サポートするコマンドの数が多すぎる

現在のボット メニューにはコマンドが 6 つしか表示されないため、それ以外のコマンドは滅多に使用されなくなります。 幅広いアシストを提供するボットより、特定の分野を深く掘り下げるボットの方がうまくいきます。

### <a name="maintain-a-large-knowledge-base"></a>維持するサポート情報が大規模である

ボットの欠点の 1 つは、ランクなしの応答を使用して大規模な取得サポート情報を維持するのが難しいことです。 ボットは、長いリストから答えを調べ出すようなものではなく、短く簡潔なやり取りに最適です。

## <a name="code-snippets"></a>コード スニペット

次のコードは、チャネル チーム スコープのボット アクティビティの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}

```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});

```

---

次のコードは、1 対 1 のチャットのボット アクティビティの例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

// Handle message activity
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    turnContext.Activity.RemoveRecipientMention();
    var text = turnContext.Activity.Text.Trim().ToLower();
  await turnContext.SendActivityAsync(MessageFactory.Text($"Your message is {text}."), cancellationToken);
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
this.onMessage(async (context, next) => {
    await context.sendActivity(MessageFactory.text("Your message is:" + context.activity.text));
    await next();
});
```

---

## <a name="code-sample"></a>コード サンプル

|サンプルの名前 | 説明 | .NETCore | Node.js | Python|
|----------------|-----------------|--------------|----------------|-------|
| Teams 会話ボット | メッセージングと会話イベントの処理。 |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|
| ボット サンプル | ボット サンプルのセット | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) |[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs)|[表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python)|

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ボットのアクティビティ ハンドラー](~/bots/bot-basics.md)

## <a name="see-also"></a>関連項目

* [通話と会議のボット](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [ボットの会話](~/bots/how-to/conversations/conversation-basics.md)
* [Bot コマンド メニュー](~/bots/how-to/create-a-bot-commands-menu.md)
* [Bot Framework Composerでカスタム トリガーを作成する](/composer/how-to-create-custom-triggers)
* [Microsoft Teams でのボットの認証フロー](~/bots/how-to/authentication/auth-flow-bot.md)
* [ボットでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [ボットを Azure に発行する](/azure/bot-service/bot-builder-deploy-az-cli)
* [Bot Framework Connector サービスの API リファレンス](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference)
